# Filesystem

{% include headOScoverage.md %}

> Table Of Contents
>
> -   [Introduction](#introduction)
> -   [Available Methods](#available-methods)
> -   [Method Listing](#method-listing)
> -   [Unit Tests Matrix](#unit-tests-matrix)

## Introduction

The filesystem package provides an expressive abstraction for working with local files.

```go
package main

import "github.com/reglue4go/filesystem"

func main() {
	if filesystem.Exists("./app.yml") {
		fmt.Printf("%v\n", "File found")
	} else {
		fmt.Printf("%v\n", "File missing")
	}
}
```

## Available Methods

| &#8230;                                 | &#8230;                                 | &#8230;                                         |
| :-------------------------------------- | :-------------------------------------- | :---------------------------------------------- |
| [AllFiles](#allfiles)                   | [Append](#append)                       | [Basename](#basename)                           |
| [Chmod](#chmod)                         | [CleanDirectory](#cleandirectory)       | [Copy](#copy)                                   |
| [CopyDirectory](#copydirectory)         | [CurrentDirectory](#currentdirectory)   | [CurrentExecutable](#currentexecutable)         |
| [Delete](#delete)                       | [DeleteDirectories](#deletedirectories) | [DeleteDirectory](#deletedirectory)             |
| [Directories](#directories)             | [Dirname](#dirname)                     | [EnsureDirectoryExists](#ensuredirectoryExists) |
| [Exists](#exists)                       | [Extension](#extension)                 | [Files](#files)                                 |
| [Get](#get)                             | [Glob](#glob)                           | [GuessExtension](#guessextension)               |
| [Hash](#hash)                           | [HasSameHash](#hassameHash)             | [IsDirectory](#isdirectory)                     |
| [IsEmptyDirectory](#isemptydirectory)   | [IsFile](#isfile)                       | [IsReadable](#isreadable)                       |
| [IsWritable](#iswritable)               | [LastModified](#lastmodified)           | [Lines](#lines)                                 |
| [Link](#link)                           | [MakeDirectory](#makedirectory)         | [MimeType](#mimetype)                           |
| [Missing](#missing)                     | [Move](#move)                           | [MoveDirectory](#movedirectory)                 |
| [Name](#name)                           | [Prepend](#prepend)                     | [Put](#put)                                     |
| [Realpath](#realpath)                   | [RealpathSystem](#realpathsystem)       | [Replace](#replace)                             |
| [ReplaceInFile](#replaceinfile)         | [Size](#size)                           | [TempDirectory](#tempdirectory)                 |
| [Tempnam](#tempnam)                     | [Type](#type)                           | [UserConfigDirectory](#userconfigdirectory)     |
| [UserHomeDirectory](#userhomedirectory) |                                         |                                                 |

## Method Listing

{% include footMatrixes.md %}
