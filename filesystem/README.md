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

#### [UserHomeDirectory](#available-methods)

The UserHomeDirectory method will return the path to operating system user home directory.

```go
path := filesystem.UserHomeDirectory()
```

#### [UserConfigDirectory](#available-methods)

The UserConfigDirectory method will return the path to operating system user config directory.

```go
path := filesystem.UserConfigDirectory()
```

#### [Type](#available-methods)

The Type method returns the file type of a given file. The returned value is either file or dir.

```go
value := filesystem.Type("./temp.log")
```

#### [Tempnam](#available-methods)

The Tempnam method creates a file with a unique filename with access permission set to 0600 in the specified directory.
The second parameter is a prefix to the temporal name.

```go
path := filesystem.Tempnam("./public/temp", "log")
```

#### [TempDirectory](#available-methods)

The TempDirectory method will return the path to operating system temporal directory.

```go
path := filesystem.TempDirectory()
```

#### [Size](#available-methods)

The Size method will gets the file size of a given file.

```go
size := filesystem.Size("./temp.log")
```

#### [ReplaceInFile](#available-methods)

The ReplaceInFile method will replace a given string within a given file.

```go
ok := filesystem.ReplaceInFile("long text", "article", "./temp.log")
```

#### [Replace](#available-methods)

The Replace method writes the contents of a file, replacing it atomically if it already exists.

```go
ok := filesystem.Replace("./temp.log", "Some long text contents")
```

#### [RealpathSystem](#available-methods)

The RealpathSystem method expands all symbolic links and returns canonicalized absolute pathname based on the given path prifix.
**~C~** prefix will expand from operating system user config directory.
**~T~** prefix will expand from operating system temp directory.
**~H~** prefix will expand from operating system user home directory.

```go
log1 := filesystem.RealpathSystem("~C~/data/temp.log")

log2 := filesystem.RealpathSystem("~T~/data/temp.log")

log3 := filesystem.RealpathSystem("~H~/data/temp.log")

log4 := filesystem.RealpathSystem("./data/temp.log")
```

#### [Realpath](#available-methods)

The Realpath method expands all symbolic links and returns canonicalized absolute pathname.

```go
path := filesystem.Realpath("./temp.log")
```

#### [Put](#available-methods)

The Put method may be used to write the contents of a file. If the put method is unable to write the file to disk, false will be returned.

```go
success := filesystem.Put("./temp.log", "Some long text contents")
```

#### [Prepend](#available-methods)

The Prepend method allows you to write to the beginning of a file:

```go
success := filesystem.Prepend("./temp.log", "Prepended Text")
```

#### [Name](#available-methods)

The Name method may be used to extract the file name from a file path.

```go
name := filesystem.Name("./public/images/cat.jpg")
```

#### [MoveDirectory](#available-methods)

The MoveDirectory method may be used to move an existing directory to a new location. You can overide any existing directory by providing true as a third argument.

```go
success := filesystem.MoveDirectory("./from/temp", "./to/backup/temp")
success := filesystem.MoveDirectory("./from/temp", "./to/backup/temp", true)
```

#### [Move](#available-methods)

The Move method may be used to rename or move an existing file to a new location.

```go
success := filesystem.Move("./from/file.jpg", "./to/file.jpg")
```

#### [Missing](#available-methods)

The Missing method may be used to determine if a file or directory is missing.

```go
ok := filesystem.Missing("./cat.jpg")
ok := filesystem.Missing("./backup")
```

#### [MimeType](#available-methods)

The MimeType method will obtain the MIME type of a given file.

```go
mime := filesystem.MimeType("./dog.png")
```

#### [MakeDirectory](#available-methods)

The MakeDirectory method will create the given directory, including any needed subdirectories.

```go
success := filesystem.MakeDirectory("./backup/temp")
```

#### [Link](#available-methods)

The Link method will create a symlink to the target file or directory.

```go
success := filesystem.Link("./temp.log", "./backup/temp.log")
```

#### [Lines](#available-methods)

The Lines method gets the contents of a file one line at a time returning an array of lines

```go
var list []string = filesystem.Lines("./temp.log")
```

#### [LastModified](#available-methods)

The LastModified method gets the file's last modification time.

```go
modifiedAt := filesystem.LastModified("./backup")
```

#### [IsWritable](#available-methods)

The IsWritable method determines if the given path is writable.

```go
ok := filesystem.IsWritable("./backup")
```

#### [IsReadable](#available-methods)

The IsReadable method determines if the given path is readable.

```go
ok := filesystem.IsReadable("./backup")
```

#### [IsFile](#available-methods)

The IsFile method determines if the given path is a file.

```go
ok := filesystem.IsFile("./backup")
```

#### [IsEmptyDirectory](#available-methods)

The IsEmptyDirectory method determines if the given path is a directory that does not contain any other files or directories.

```go
ok := filesystem.IsEmptyDirectory("./backup")
```

#### [IsDirectory](#available-methods)

The IsDirectory method determines if the given path is a directory.

```go
ok := filesystem.IsDirectory("./temp.log")
```

#### [HasSameHash](#available-methods)

The HasSameHash method determines if two files are the same by comparing their hashes.

```go
ok := filesystem.HasSameHash("./temp.log", "./backup/temp.log")
```

#### [Hash](#available-methods)

The Hash method generates a hash value using the contents of a given file.

```go
value := filesystem.Hash("./temp.log")
```

#### [GuessExtension](#available-methods)

The GuessExtension method returns the file extension from the mime-type of a given file.

```go
path := filesystem.GuessExtension("./public/images") // ""

path := filesystem.GuessExtension("./public/images/cat.jpg") // "jpg"
```

#### [Glob](#available-methods)

The Glob method returns a list of all path names matching a given pattern:

```go
items := filesystem.Glob("*.jpg")
```

#### [Get](#available-methods)

The Get method may be used to retrieve the contents of a file.

```go
contents := filesystem.Get("./temp.log")
```

#### [Files](#available-methods)

The Files method returns a list of all of the files in a given directory:

```go
items := filesystem.Files("./public")
```

#### [Extension](#available-methods)

The Extension method returns the file extension of the given path.

```go
path := filesystem.Extension("./public/images") // ""

path := filesystem.Extension("./public/images/cat.jpg") // "jpg"
```

#### [Exists](#available-methods)

The Exists method may be used to determine if a file exists on the disk.

```go
success := filesystem.Exists("./temp")
```

#### [EnsureDirectoryExists](#available-methods)

The EnsureDirectoryExists method determines if a directory exists or creates the directory if it does not exists.

```go
success := filesystem.EnsureDirectoryExists("./temp")
```

#### [Dirname](#available-methods)

The Dirname method returns the parent directory from a path.

```go
path := filesystem.Dirname("./public/images")
// "./public"

path := filesystem.Dirname("./public/images/cat.jpg")
// "./public/images"
```

#### [Directories](#available-methods)

The Directories method returns a list of all the directories within a given directory.

```go
items := filesystem.Directories("./public")
```

#### [DeleteDirectory](#available-methods)

The DeleteDirectory method may be used to remove a directory and all of its files.

```go
success := filesystem.DeleteDirectory("./temp")
```

#### [DeleteDirectories](#available-methods)

The DeleteDirectories method may be used to remove all of the directories within a given directory.

```go
success := filesystem.DeleteDirectories("./temp")
```

#### [Delete](#available-methods)

The Delete method may be used to remove the file at a given path.

```go
success := filesystem.Delete("./public/temp.log")
```

#### [CurrentExecutable](#available-methods)

The CurrentExecutable method may be used to get the path of the executable that started the current process.

```go
path := filesystem.CurrentExecutable()
```

#### [CurrentDirectory](#available-methods)

The CurrentDirectory method may be used to get path for the current working directory.

```go
path := filesystem.CurrentDirectory()
```

#### [CopyDirectory](#available-methods)

The CopyDirectory method may be used to copy a directory from one location to another.

```go
success := filesystem.CopyDirectory("./from/public", "./to/backup")
```

#### [Copy](#available-methods)

The Copy method may be used to copy an existing file to a new location on the disk.

```go
success := filesystem.Copy("./from/file.jpg", "./to/file.jpg")
```

#### [CleanDirectory](#available-methods)

The CleanDirectory method will empty the specified directory of all files and folders.

```go
success := filesystem.CleanDirectory("./temp")
```

#### [Chmod](#available-methods)

The Chmod method will get or set UNIX mode of a file or directory

```go
success := filesystem.Chmod("./public/temp.log", 775)
```

#### [Basename](#available-methods)

The Basename method will return the trailing name component of the given path.

```go
name := filesystem.Basename("./public/temp.log")
// temp.log
```

#### [Append](#available-methods)

The Append method allows you to write to the end of a file:

```go
success := filesystem.Append("./temp.log", "Appended Text")
```

#### [AllFiles](#available-methods)

The AllFiles method retrieves a list of all files within a given directory including all subdirectories:

```go
items := filesystem.AllFiles("./public")
```

{% include footMatrixes.md %}
