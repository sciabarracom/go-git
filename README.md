我是光年实验室高级招聘经理。
我在github上访问了你的开源项目，你的代码超赞。你最近有没有在看工作机会，我们在招软件开发工程师，拉钩和BOSS等招聘网站也发布了相关岗位，有公司和职位的详细信息。
我们公司在杭州，业务主要做流量增长，是很多大型互联网公司的流量顾问。公司弹性工作制，福利齐全，发展潜力大，良好的办公环境和学习氛围。
公司官网是http://www.gnlab.com,公司地址是杭州市西湖区古墩路紫金广场B座，若你感兴趣，欢迎与我联系，
电话是0571-88839161，手机号：18668131388，微信号：echo 'bGhsaGxoMTEyNAo='|base64 -D ,静待佳音。如有打扰，还请见谅，祝生活愉快工作顺利。

![go-git logo](https://cdn.rawgit.com/src-d/artwork/02036484/go-git/files/go-git-github-readme-header.png)
[![GoDoc](https://godoc.org/gopkg.in/src-d/go-git.v4?status.svg)](https://godoc.org/github.com/src-d/go-git) [![Build Status](https://travis-ci.org/src-d/go-git.svg)](https://travis-ci.org/src-d/go-git) [![Build status](https://ci.appveyor.com/api/projects/status/nyidskwifo4py6ub?svg=true)](https://ci.appveyor.com/project/mcuadros/go-git) [![codecov.io](https://codecov.io/github/src-d/go-git/coverage.svg)](https://codecov.io/github/src-d/go-git) [![Go Report Card](https://goreportcard.com/badge/github.com/src-d/go-git)](https://goreportcard.com/report/github.com/src-d/go-git)

*go-git* is a highly extensible git implementation library written in **pure Go**.

It can be used to manipulate git repositories at low level *(plumbing)* or high level *(porcelain)*, through an idiomatic Go API. It also supports several types of storage, such as in-memory filesystems, or custom implementations thanks to the [`Storer`](https://godoc.org/gopkg.in/src-d/go-git.v4/plumbing/storer) interface.

It's being actively developed since 2015 and is being used extensively by [source{d}](https://sourced.tech/) and [Keybase](https://keybase.io/blog/encrypted-git-for-everyone), and by many other libraries and tools.

Comparison with git
-------------------

*go-git* aims to be fully compatible with [git](https://github.com/git/git), all the *porcelain* operations are implemented to work exactly as *git* does.

*git* is a humongous project with years of development by thousands of contributors, making it challenging for *go-git* to implement all the features. You can find a comparison of *go-git* vs *git* in the [compatibility documentation](COMPATIBILITY.md).


Installation
------------

The recommended way to install *go-git* is:

```
go get -u gopkg.in/src-d/go-git.v4/...
```

> We use [gopkg.in](http://labix.org/gopkg.in) to version the API, this means that when `go get` clones the package, it's the latest tag matching `v4.*` that is cloned and not the master branch.

Examples
--------

> Please note that the `CheckIfError` and `Info` functions  used in the examples are from the [examples package](https://github.com/src-d/go-git/blob/master/_examples/common.go#L17) just to be used in the examples.


### Basic example

A basic example that mimics the standard `git clone` command

```go
// Clone the given repository to the given directory
Info("git clone https://github.com/src-d/go-git")

_, err := git.PlainClone("/tmp/foo", false, &git.CloneOptions{
    URL:      "https://github.com/src-d/go-git",
    Progress: os.Stdout,
})

CheckIfError(err)
```

Outputs:
```
Counting objects: 4924, done.
Compressing objects: 100% (1333/1333), done.
Total 4924 (delta 530), reused 6 (delta 6), pack-reused 3533
```

### In-memory example

Cloning a repository into memory and printing the history of HEAD, just like `git log` does


```go
// Clones the given repository in memory, creating the remote, the local
// branches and fetching the objects, exactly as:
Info("git clone https://github.com/src-d/go-siva")

r, err := git.Clone(memory.NewStorage(), nil, &git.CloneOptions{
    URL: "https://github.com/src-d/go-siva",
})

CheckIfError(err)

// Gets the HEAD history from HEAD, just like this command:
Info("git log")

// ... retrieves the branch pointed by HEAD
ref, err := r.Head()
CheckIfError(err)


// ... retrieves the commit history
cIter, err := r.Log(&git.LogOptions{From: ref.Hash()})
CheckIfError(err)

// ... just iterates over the commits, printing it
err = cIter.ForEach(func(c *object.Commit) error {
	fmt.Println(c)
	return nil
})
CheckIfError(err)
```

Outputs:
```
commit ded8054fd0c3994453e9c8aacaf48d118d42991e
Author: Santiago M. Mola <santi@mola.io>
Date:   Sat Nov 12 21:18:41 2016 +0100

    index: ReadFrom/WriteTo returns IndexReadError/IndexWriteError. (#9)

commit df707095626f384ce2dc1a83b30f9a21d69b9dfc
Author: Santiago M. Mola <santi@mola.io>
Date:   Fri Nov 11 13:23:22 2016 +0100

    readwriter: fix bug when writing index. (#10)

    When using ReadWriter on an existing siva file, absolute offset for
    index entries was not being calculated correctly.
...
```

You can find this [example](_examples/log/main.go) and many others in the [examples](_examples) folder.

Contribute
----------

[Contributions](https://github.com/src-d/go-git/issues?q=is%3Aissue+is%3Aopen+label%3A%22help+wanted%22) are more than welcome, if you are interested please take a look to
our [Contributing Guidelines](CONTRIBUTING.md).

License
-------
Apache License Version 2.0, see [LICENSE](LICENSE)
