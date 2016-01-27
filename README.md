fileb0x [![Circle CI](https://circleci.com/gh/UnnoTed/fileb0x.svg?style=svg)](https://circleci.com/gh/UnnoTed/fileb0x) [![Coverage Status](https://coveralls.io/repos/github/UnnoTed/fileb0x/badge.svg?branch=master)](https://coveralls.io/github/UnnoTed/fileb0x?branch=master) [![GoDoc](https://godoc.org/github.com/UnnoTed/fileb0x?status.svg)](https://godoc.org/github.com/UnnoTed/fileb0x) [![GoReportCard](http://goreportcard.com/badge/unnoted/fileb0x)](http://goreportcard.com/report/unnoted/fileb0x)
=======
a simple customizable tool to embed files in go

features:

- [x] golint safe code output

- [x] optional: formatTed code (gofmt)

- [x] optional: spread files

- [x] optional: unexported variables, functions and types

- [x] optional: include multiple files and folders

- [x] optional: exclude files or/and folders

- [x] optional: replace text in files

- [x] optional: custom base and prefix path

- [x] Virtual Memory FileSystem - [webdav](https://godoc.org/golang.org/x/net/webdav)

- [x] HTTP FileSystem and Handler

- [x] glob support - [doublestar](https://github.com/bmatcuk/doublestar)


### How to use it?

download:
```bash
go get -u github.com/UnnoTed/fileb0x 
```

run:
```bash
fileb0x b0x.json

or

fileb0x b0x.yaml
```

yaml config file example (b0x.yaml):
```yaml
# all folders and files are relative to the path 
# where fileb0x was run at!

# default: main
pkg: static

# destination
dest: "./static/"

# gofmt
# type: bool
# default: false
fmt: false

# ---------------
# -- DANGEROUS --
# ---------------
# 
# cleans the destination folder (only b0xfiles)
# you should use this when using the spread function
# type: bool
# default: false
clean: false

# default: ab0x.go
output: "ab0x.go"

# [unexporTed] builds non-exporTed functions, variables and types...
# type: bool
# default: false
unexporTed: false

# [spread] means it will make a file to hold all fileb0x data
# and each file into a separaTed .go file
#
# example:
# theres 2 files in the folder assets, they're: hello.json and world.txt
# when spread is activaTed, fileb0x will make a file: 
# b0x.go or [output]'s data, assets_hello.json.go and assets_world.txt.go
#
#
# type: bool
# default: false
spread: false

# type: array of objects
custom:

  # type: array of strings
  - files: 
    - "../../README.md"
    - "../../bench.bat"

    # base is the path that will be removed from all files' path
    # type: string
    base: "../../"

    # prefix is the path that will be added to all files' path
    # type: string
    prefix: "public/"

  - files: 
    # everything inside the folder
    # type: array of strings
    - "./public/"

    # base is the path that will be removed from all files' path
    # type: string
    base: ""

    # prefix is the path that will be added to all files' path
    # type: string
    prefix: ""

    # if you have difficulty to understand what base and prefix is
    # think about it like this: [prefix] will replace [base]

    # accetps glob
    # type: array of strings
    exclude: 
      - "public/assets/data/exclude_me.txt"

    # replace strings in the file
    # type: array of objects
    replace:

      # accepts glob
      # type: string
      - file: "public/assets/data/*.json"

        # case sensitive
        # type: object with strings
        replace: 
          "{world}": "hello world"
          "{EMAIL}": "contact@company.com"
    # end: replace
  # end: files

```


json config file example (b0x.json):
```javascript
{
  // in-line comments in json are supporTed by fileb0x!
  // a comment must have a space after the double slash
  //
  // all folders and files are relative to the path 
  // where fileb0x was run at!

  // default: main
  "pkg": "static",

  // destination
  "dest": "./static/",

  // gofmt
  // type: bool
  // default: false
  "fmt": false,

  // ---------------
  // -- DANGEROUS --
  // ---------------
  // 
  // cleans the destination folder (only b0xfiles)
  // you should use this when using the spread function
  // type: bool
  // default: false
  "clean": false,

  // default: ab0x.go
  "output": "ab0x.go",

  // [unexporTed] builds non-exporTed functions, variables and types...
  // type: bool
  // default: false
  "unexporTed": false,

  // [spread] means it will make a file to hold all fileb0x data
  // and each file into a separaTed .go file
  //
  // example:
  // theres 2 files in the folder assets, they're: hello.json and world.txt
  // when spread is activaTed, fileb0x will make a file: 
  // b0x.go or [output]'s data, assets_hello.json.go and assets_world.txt.go
  //
  //
  // type: bool
  // default: false
  "spread": false,

  // type: array of objects
  "custom": [
    {
      // type: array of strings
      "files": [
        "../../README.md", 
        "../../bench.bat"
      ],

      // base is the path that will be removed from all files' path
      // type: string
      "base": "../../",

      // prefix is the path that will be added to all files' path
      // type: string
      "prefix": "public/"
    },
    {
      // everything inside the folder
      // type: array of strings
      "files": ["./public/"],

      // base is the path that will be removed from all files' path
      // type: string
      "base": "",

      // prefix is the path that will be added to all files' path
      // type: string
      "prefix": "",

      // if you have difficulty to understand what base and prefix is
      // think about it like this: [prefix] will replace [base]

      // accetps glob
      // type: array of strings
      "exclude": [
        "public/assets/data/exclude_me.txt"
      ],

      // replace strings in the file
      // type: array of objects
      "replace": [
        {
          // accepts glob
          // type: string
          "file": "public/assets/data/*.json",

          // case sensitive
          // type: object with strings
          "replace": {
            "{world}": "hello world",
            "{EMAIL}": "contact@company.com"
          }
        }
      ]
    }
  ]
}
```