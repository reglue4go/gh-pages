# Environment

{% include headOScoverage.md %}

> Table Of Contents
>
> -   [Introduction](#introduction)
> -   [Available Methods](#available-methods)
> -   [Method Listing](#method-listing)
> -   [Unit Tests Matrix](#unit-tests-matrix)

## Introduction

The env package provides a convenient interface for loading environment and property files.

> <a href="https://reglue4go.github.io/env/example4properties" target="_blank">Properties File Example</a>

```go
package main

import (
	"github.com/reglue4go/env"
)

func main() {
	items := env.Read("DB_DATABASE=:memory:\nDB_PORT=3306")
	props := env.ReadProperties(
		"app.name=Go",
		"db.port=3306\nhost:localhost",
		"DB_DATABASE=:memory:\nDB_PORT=3306",
		"./app.properties",
	)

	value := items.Get("DB_PORT").ToInt()

	fmt.Printf("%v\n", value) // 3306

	value := props.MustGetString("host")

	fmt.Printf("%v\n", value) // "localhost"
}
```

## Available Methods

| &#8230;                           | &#8230;                   | &#8230;                 |
| :-------------------------------- | :------------------------ | :---------------------- |
| [Fill](#fill)                     | [Get](#get)               | [GetFluent](#getfluent) |
| [Load](#load)                     | [LoadRemote](#loadremote) | [Read](#read)           |
| [ReadProperties](#readproperties) | [ReadRemote](#readremote) | [Set](#set)             |

## Method Listing

#### [Set](#available-methods)

The Set method adds a key value pair environment variable:

```go
env.Set("USER", "bob")
env.Set("API_KEY", "e5akemy")
```

#### [ReadRemote](#available-methods)

The ReadRemote method reads values from io.Reader in to a Bag(map):

```go
if response, err := http.Get("https://website.com/config/.env.production"); err == nil {
	var items := env.ReadRemote(response.Body)

	value := items.Get("DB_PORT").ToInt()
	// 3306
}
```

#### [ReadProperties](#available-methods)

The ReadProperties method reads values from files, plain strings and io.Reader in to a Bag(map):

```go
var props := env.ReadProperties(
	"app.name=Go",
	"db.port=3306\nhost:localhost",
	"DB_DATABASE=:memory:\nDB_PORT=3306",
	"./app.properties",
)

value := props.MustGetString("DB_DATABASE")
// ":memory:"
```

#### [Read](#available-methods)

The Read method reads values from a file or plain string in to a Bag(map):

```go
var items := env.Read("DB_DATABASE=:memory:\nDB_PORT=3306")

value := items.Get("DB_PORT").ToInt()
// 3306
```

#### [LoadRemote](#available-methods)

The LoadRemote method reads values from an io.Reader in to environment variables:

```go
if response, err := http.Get("https://website.com/config/.env.production"); err == nil {
	env.Load(response.Body)
}
```

#### [Load](#available-methods)

The Load method reads values from a file or plain string in to environment variables:

```go
env.Load() // loads default .env
env.Load("DB_DATABASE=:memory:\nDB_PORT=3306") // loads plain string
env.Load("./env.local") // loads file
```

#### [GetFluent](#available-methods)

The GetFluent method retrieves the environment variable as a Fluent value:

```go
value := env.GetFluent("HTTP_PORT").ToInt()
// 80
```

#### [Get](#available-methods)

The Get method retrieves the environment variable as a string:

```go
value := env.Get("HTTP_PORT")
// "80"
```

#### [Fill](#available-methods)

The Fill method populates environment variables from a given map:

```go
env.Fill(map[string]string{
	"HTTP_PORT": "80",
	"APP_NAME": "recipes",
})
```

{% include footMatrixes.md %}
