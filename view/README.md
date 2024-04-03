# View

{% include headOScoverage.md %}

> Table Of Contents
>
> -   [Introduction](#introduction)
> -   [View Factory](#view-factory)
> -   [View Resolver](#view-resolver)
> -   [Unit Tests Matrix](#unit-tests-matrix)

## Introduction

Views separate your application logic from your presentation logic. They are stored in files or directly rendered from strings. View templates are usually written using the Golang templating language. A simple golang template looks like this:

{% raw %}

```html
<!-- View stored in templates/greeting.gohtml -->

<!DOCTYPE html>
<html lang="en">
	<body>
		<h1>Hello, 󠁻{{․}}</h1>
		󠁻 {{block "footer" ․}}
		<p>© 2024</p>
		{{end}}
	</body>
</html>
```

{% endraw %}

This view is stored at templates/greeting.gohtml and we may compile it like so:

```go
package main

import "github.com/reglue4go/view"

func main() {
	compiled := view.NewFactory("templates").Make("greeting.gohtml", "Jane")

	fmt.Printf("%v\n", compiled)
	/*
	<!DOCTYPE html>
	<html lang="en">
		<body>
			<h1>Hello, Jane</h1>

			<p>© 2024</p>
		</body>
	</html>
	*/
}
```

## View Factory

Rendering views is primarily handled by the view factory. A view factory instance can be reused multiple times for rendering templates.

```go
package main

import "github.com/reglue4go/view"

func main() {
	factory := view.NewFactory("templates")

	greetJane := factory.Make("greeting.gohtml", "Jane")

	fmt.Printf("%v\n", greetJane)
	/*
	<!DOCTYPE html>
	<html lang="en">
		<body>
			<h1>Hello, Jane</h1>

			<p>© 2024</p>
		</body>
	</html>
	*/

	greetBob := factory.Make("greeting.gohtml", "Bob")

	fmt.Printf("%v\n", greetBob)
	/*
	<!DOCTYPE html>
	<html lang="en">
		<body>
			<h1>Hello, Bob</h1>

			<p>© 2024</p>
		</body>
	</html>
	*/
}
```

## View Factory Methods

| &#8230;                         | &#8230;                         | &#8230;                               |
| :------------------------------ | :------------------------------ | :------------------------------------ |
| [CompilerViews](#compilerviews) | [DefaultLayout](#defaultlayout) | [Make](#make)                         |
| [MakeUsing](#makeusing)         | [Resolver](#resolver)           | [SetDefaultLayout](#setdefaultlayout) |

#### [CompilerViews](#view-factory-methods)

The CompilerViews method returns a list of views to be compiled. If the view factory has a default layout, it will be added to the list.

```go
package main

import "github.com/reglue4go/view"

func main() {
	list := view.NewFactory("templates").CompilerViews("greeting.gohtml")

	fmt.Printf("%v\n", list)
	// ["layouts/app.gohtml", "greeting.gohtml"]
}
```

#### [DefaultLayout](#view-factory-methods)

Most applications maintain the same general layout across various pages.
Layouts provide a convenient way of defining a single base template and then use it throughout the application.
The view factory DefaultLayout method returns the default layout for all views.
You can set the default layout by providing an optional template path argument to the DefaultLayout method.

```go
package main

import "github.com/reglue4go/view"

func main() {
	factory := view.NewFactory("templates")

	defaultLayout := factory.DefaultLayout()

	fmt.Printf("%v\n", defaultLayout)
	// "layouts/app"

	factory.DefaultLayout("layouts/blog")

	fmt.Printf("%v\n", factory.DefaultLayout())
	// "layouts/blog"
}
```

#### [Make](#view-factory-methods)

You may render a view by passing a file name with the .gohtml extension to the view factory Make method. The file extension determins the view compiler to be used. If you omit a file name extension, the assumed extension will be gohtml. When using a custom view compiler, the file name and extension must be provided.

```go
package main

import "github.com/reglue4go/view"

func main() {
	factory := view.NewFactory("templates")

	compiled := factory.Make("greeting.gohtml", "Jane")

	compiledAgain := factory.Make("greeting", "Jane")

	fmt.Printf("%v\n", compiled == compiledAgain)
	// true

	fmt.Printf("%v\n", compiled)
	/*
	<!DOCTYPE html>
	<html lang="en">
		<body>
			<h1>Hello, Jane</h1>

			<p>© 2024</p>
		</body>
	</html>
	*/
}
```

#### [MakeUsing](#view-factory-methods)

The MakeUsing method renders the template using a provided layout.

```go
compiled := view.NewFactory("templates").
	MakeUsing("layouts/email", "welcome", map[string]any{
		"address": "jane@gmail.io",
		"to": "jane",
	})
```

#### [Resolver](#view-factory-methods)

The Resolver method returns the view Resolver instance used by the factory.

```go
viewResolver := view.NewFactory("templates").Resolver()
```

#### [SetDefaultLayout](#view-factory-methods)

The SetDefaultLayout method sets the default layout to be used for all views.

```go
factory := view.NewFactory("templates").SetDefaultLayout("layouts/blog")

fmt.Printf("%v\n", factory.DefaultLayout())
// "layouts/blog"
```

## View Resolver

The view Resolver is responsible for locating views and associating them with verious compilers.

## View Resolver Methods

| &#8230;                                     | &#8230;                             | &#8230;                                   |
| :------------------------------------------ | :---------------------------------- | :---------------------------------------- |
| [AddCompiler](#addcompiler)                 | [AddLocation](#addlocation)         | [Compile](#compile)                       |
| [Data](#data)                               | [DefaultCompiler](#defaultcompiler) | [DefaultExtension](#defaultextension)     |
| [DotExtension](#dotextension)               | [Exists](#exists)                   | [Files](#files)                           |
| [IsLoaded](#isloaded)                       | [Load](#load)                       | [Locations](#locations)                   |
| [NormalizeName](#normalizename)             | [ResolveCompiler](#resolvecompiler) | [SetDefaultCompiler](#setdefaultcompiler) |
| [SetDefaultExtension](#setdefaultextension) | [SetLocation](#setlocation)         | [Share](#share)                           |
| [TagCompiler](#tagcompiler)                 | [Tags](#tags)                       | [TemplateCompilers](#templatecompilers)   |

#### [TemplateCompilers](#view-resolver-methods)

The TemplateCompilers method returns a map of registered extensions and their corresponding compilers.

#### [Tags](#view-resolver-methods)

The Tags method returns a map of registered tags and their corresponding aliases.

```go
tags := view.NewFactory("templates").Resolver().Tags()

fmt.Printf("%v\n", tags)
// map[htm:gohtml html:gohtml]

```

#### [TagCompiler](#view-resolver-methods)

Tags are aliases to existing view compilers. They are used to associate extensions with compilers. If you wish to use an HTML compiler for compiling files with .htm extension, simply tag the html compiler with an htm extension.

#### [Share](#view-resolver-methods)

The Share method adds a piece of shared data to the environment. Unlike the Data method, it can be chained.

```go
compiled := view.NewFactory("templates").Resolver().Share("Jane").Compile("greeting.gohtml")

```

#### [SetLocation](#view-resolver-methods)

The SetLocation method registers view locations and returns the Resolver instance.

```go
resolver := view.NewFactory().Resolver().SetLocation("templates", "themes/dark")

```

#### [SetDefaultExtension](#view-resolver-methods)

The SetDefaultExtension registers a default view file extension.

```go
resolver := view.NewFactory("templates").Resolver().SetDefaultExtension("amber")

```

#### [SetDefaultCompiler](#view-resolver-methods)

The SetDefaultCompiler registers a default template compiler callback. Whenever a compiler for an extension cannot be resolved, the default compiler will be used.

#### [ResolveCompiler](#view-resolver-methods)

The ResolveCompiler gets the compiler for a given extension.

#### [NormalizeName](#view-resolver-methods)

The NormalizeName method ensures an extension is included in the given view name.

```go
resolver := view.NewFactory("templates").Resolver()

extension := resolver.NormalizeName("greeting")

fmt.Printf("%v\n", extension == "greeting.gohtml")
// true

extension := resolver.DotExtension("greeting.gohtml")

fmt.Printf("%v\n", extension == "greeting.gohtml")
// true

```

#### [Locations](#view-resolver-methods)

The Locations method returns a list of registered view locations. If you provide a list of locations as arguments, they will be registered.

```go
resolver := view.NewFactory("templates").Resolver()

list := resolver.Locations("themes/default")

fmt.Printf("%v\n", list)
// ["templates" "themes/default"]

```

#### [Load](#view-resolver-methods)

The Load method locates and maps view files from the provided paths.

#### [IsLoaded](#view-resolver-methods)

The IsLoaded method determines if view files have been located.

#### [Files](#view-resolver-methods)

The Files method Get the views that have been located.

#### [Exists](#view-resolver-methods)

The Exists method determines if a given view exists.

```go
resolver := view.NewFactory("templates").Resolver()

found := resolver.Exists("greeting")

fmt.Printf("%v\n", found)
// true

```

#### [DotExtension](#view-resolver-methods)

The DotExtension method prefixes a dot in the file extension.

```go
resolver := view.NewFactory("templates").Resolver()

extension := resolver.DotExtension("gohtml")

fmt.Printf("%v\n", extension == ".gohtml")
// true

extension := resolver.DotExtension(".gohtml")

fmt.Printf("%v\n", extension == ".gohtml")
// true

```

#### [DefaultExtension](#view-resolver-methods)

#### [DefaultCompiler](#view-resolver-methods)

#### [Data](#view-resolver-methods)

The Data method returns a piece of shared data from the environment. You can optionally share a piece of data as a second argument.

```go
resolver := view.NewFactory("templates").Resolver()
resolver.Data("Jane")
compiled := resolver.Compile("greeting.gohtml")

```

#### [Compile](#view-resolver-methods)

The Compile method compiles a list of views and returns a string.

```go
factory := view.NewFactory("templates")
compiled := factory.Resolver().Compile("layouts/app.gohtml", "home.gohtml")

```

#### [AddLocation](#view-resolver-methods)

The AddLocation adds directories where view template files are located.

```go
factory := view.NewFactory("templates")
resolver := factory.Resolver().AddLocation("themes/light", "themes/dark").AddLocation("themes/default")

```

#### [AddCompiler](#view-resolver-methods)

The AddCompiler method registers a view extension and its compiler. Template compilers are view handler callbacks functions.
The first argument to the AddCompiler method is a view extension while second argument is a callback function.

```go
package main

import (
	"bytes"
 	"github.com/eknkc/amber"
 	"github.com/reglue4go/view"
 )

func main() {
	factory := view.NewFactory("templates")
	resolver := factory.Resolver()
	// register a view compiler for amber file extension
	resolver.AddCompiler("amber", func(resolver *view.Resolver, paths ...string) string {
		if len(paths) > 0 {
			name := resolver.NormalizeName(paths[0])
			file := resolver.Load().Files()[name]
			compiler := amber.New()
			if err := compiler.ParseFile(file); err == nil {
				if temp, err := compiler.Compile(); err == nil {
					var value bytes.Buffer
					temp.Execute(&value, resolver.Data())
					return value.String()
				}
			}
		}
		return ""
		},
	)

	compiled := factory.Make("greeting.amber", "Jane")
}

```

{% include footMatrixes.md %}
