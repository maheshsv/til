# Contributing to Github Go project

I have been trying to contribute to a Go [project](https://github.com/beego/bee) on Github and found it's a bit different than projects in other languages such as Python/Ruby/JavaScript.

Later I found an article [here](https://robots.thoughtbot.com/contributing-to-open-source-golang-projects).

The key difference is that:

**Project in other languages can be forked and cloned to local, anywhere. But for Go project, `go get` actually clone it to $GOPATH/src/github/github_username/repo and YOU MUST work on this directory, otherwise you may break the import.**

