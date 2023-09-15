---
title: Go Archive It!
slug: go-archive-it
date: "2023-08-15"
description: A lightweight archive management utility written in Go.
---
## Introduction

[go-archive-it](https://github.com/korbexmachina/go-archive-it) is a lightweight archive management utility written in Go. The archive instructions are defined in a human readable `.yaml` file. The format as of the writing of this post (Subject to change until v0.1.0) is as follows:

```yaml
vaultpath:
  - ~/example
  - ~/directories
  - ~/longer/example/path
archivepath: ~/path/to/archive
archivetype: 1
retention: 10
```

Note: An absolute path can be provided in place of the _~_, otherwise it is automatically expanded to the user's home directory.

This project began life as a python script called [archive-assistant](https://github.com/korbexmachina/archive-assistant) The goal of it's predecessor was primarily to maintain a rolling archive of my [Obsidian Vault](https://obsidian.md/), where I store my notes. 

### The Problem

My needs quickly outgrew the capabilities of my toy python script, and I realized that I needed a more robust solution, one with the following capabilities:

1. The ability to archive multiple directories based on a single config file
2. The ability to compile to a binary that can run on multiple machines without the need to configure an environment
3. Ideally multithreading, because compression can take a while on larger directories

After some consideration, I decided that a rewrite was in order.
### Why Go?

The first requirement could be achieved by simply tweaking the original python script, however I was trying to avoid external dependencies, for portability purposes due to the nature of python scripts.

The second requirement rules out python. Yes, I know there are ways to package python scripts for distribution with their dependencies but that felt like an unnecessary level of complexity. This pointed me in the direction of compiled languages.

Finally, the third requirement. This is more of a "Nice to have" than a need, but if I was going to rewrite this tool, I wanted to do it right, and since it doesn't matter what order the directories finish archiving in, multithreading seemed like a no-brainer.

I had heard that Go had great out of the box support for multithreading, as well as being easy to cross compile for multiple target operating systems. I also heard that it was very easy to learn, especially if you already know one or more _C-like_ languages. This was definitely my experience working on my first ever Go project; I went from zero to productive in just a few days of work.

---

## Development

### Runtime Configuration

The first thing I worked on was reading, writing, and validating the YAML config file which can be found at `~/.config/go-archive-it/config.yaml` I used a library called [yaml.v3](https://pkg.go.dev/gopkg.in/yaml.v3) (The only external dependency for this project) in order to marshal and un-marshal the YAML data. The following function handles the path validation for the config file.

```go
func ConfigExists(configPath string) {
    if _, err := os.Stat(configPath); os.IsNotExist(err) {
        log.Print("creating config directory")

            err := os.MkdirAll(filepath.Dir(configPath), os.ModePerm)
            if err != nil {
                log.Fatalf("Unable to create directory: %v", err)
            }

    config := Config{
        VaultPath: []string{"~/example", "~/directories"},
               ArchivePath: "~/archive",
               ArchiveType: 1,
               Retention: 10,
        }

        c, err := yaml.Marshal(config) // Serialize the struct
            if err != nil {
                log.Fatalf("Failed to serialize data: %v", err)
            }

        err = ioutil.WriteFile(
        configPath, c, os.ModeAppend | 0664)
            if err != nil {
                log.Fatalf("Unable to write file: %v", err)
            }

        log.Printf("Config Created at %s, make any neccesary 
        changes and run the program again", configPath)
            os.Exit(0)
    }
}
```

Starting at the top, the outer most _if_ statement checks if the path to the config file exists, if the path exists the function returns nothing and the program continues, otherwise any necessary path elements are created automatically, and the default values are written to the newly created `config.yaml` file. This was my first real encounter with Go error handling, I was pleasantly surprised by the way the language gently reminds you to handle errors in a logical way.

I then wrote a short function to load the config file and return the data in a __Config__ struct.

```go
func LoadConfig(configPath string) Config {
    var config Config

        file, err := ioutil.ReadFile(configPath)
        if err != nil {
            log.Fatalf("Unable to read file: %v", err)
        }

    err = yaml.Unmarshal(file, &config)
        if err != nil {
            log.Fatalf("Unable to parse file: %v", err)
        }

    return config
}
```

A __Config__ is defined as follows, the rest of the function is pretty self explanatory.

```go
type Config struct {
    VaultPath []string
        ArchivePath string
        ArchiveType uint8
        Retention uint8
}
```

### Creating The Archives

Actually creating the archives was pretty fun, and not too difficult thanks to the following _built-in_ libraries.

```go
"archive/tar"
"compress/gzip"
```

In order to create the tar files I simply had to iterate through a directory structure and add each file using a tar writer. Most of the code I actually had to write for this was just making sure each operation happened in the correct order, and that all the possible errors were handled. the code for gzipping the `.tar` files was similar, and I was able to simply chain the two writers together in order to achieve the desired result.

`archive.go` has several helper functions for creating the archive, but only two exposed functions `Archive` and `Cleanup`

`Archive` is responsible for calling the correct helper function based on the `archivetype` specified in the config file. Cleanup is responsible for checking if the number of currently stored archives exceeds the `retention` value specified in the config file. If the number of files exceeds the value of `retention` then the `Cleanup` function will delete the oldest archive.

### Main

The `main` function in `main.go` is actually pretty simple, it really just pulls everything else together, and expands any paths that need expanding. The interesting part was learning to use the `go` keyword for asynchronous execution, my implementation is as follows.

```go
var wg sync.WaitGroup
// The loop that actually runs everything
for _, path := range config.VaultPath {
    count++
        // Tilda expansion
        if path == "~" {
            path = dir
        } else if strings.HasPrefix(path, "~/") {
            path = filepath.Join(dir, path[2:])
        }

    wg.Add(1)
        go func(path string) {
            defer wg.Done()
                utils.Archive(path, archivePath, config.ArchiveType)
        }(path)

    wg.Add(1)
        go func(path string) {
            defer wg.Done()

                err := utils.Cleanup(
                filepath.Join(archivePath, 
                filepath.Base(path)), 
                config.Retention)

                if err != nil {
                    log.Fatalf("Failed to cleanup: %s", err)
                }
        }(path)
}
```

Using `sync.WaitGroup` was a very straightforward way to make sure that everything finished executing before the program finished. This was actually my first time implementing multithreading in any project, and I'm really happy with how smoothly it went.

---

## Releasing

I decided to distribute this tool via Homebrew, and so I created my own tap repository which can be found [here](https://github.com/korbexmachina/homebrew-tap). The process of setting up a tap repository was very easy, and actually pretty fun. The payoff of course is that if you have Homebrew installed, you can install go-archive-it with the following two commands.

```
brew tap korbexmachina/tap
brew install go-archive-it
```

---
## Conclusion

Overall, I'm super happy with how this went, if I were to make any technical changes, there are a few places where I could have returned an error and passed it further up instead of just logging and exiting. For a while during the earlier stages of development, I wasn't returning errors from any of my functions, I eventually realized this was not the intended way to solve problems in Go, and did some rewrites to start passing the errors further up instead of exiting the program while inside private functions. This has been a super fun project so far, and I hope to continue developing it going forward. Some ideas I have for additional features are:

1. The ability to set different retention values for each directory
2. The ability to specify a non-default config path at runtime

The only bug I have noticed so far is that the program seems to struggle with directories that start with `.`, I intend to fix this before `v0.1.0`.

That's all for now!

-Korben
