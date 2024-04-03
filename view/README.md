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

```go
/* View stored in templates/greeting.gohtml: Note that this code has been commented to prevent markdown parsing.

	<!DOCTYPE html>
	<html lang="en">
		<body>
			<h1>Hello, {{.}}</h1>

			{{block "footer" .}}
			<p>© 2024</p>
			{{end}}
		</body>
	</html>
*/
```

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

#### [Tags](#view-resolver-methods)

#### [TagCompiler](#view-resolver-methods)

#### [Share](#view-resolver-methods)

#### [SetLocation](#view-resolver-methods)

#### [SetDefaultExtension](#view-resolver-methods)

#### [SetDefaultCompiler](#view-resolver-methods)

#### [ResolveCompiler](#view-resolver-methods)

#### [NormalizeName](#view-resolver-methods)

#### [Locations](#view-resolver-methods)

#### [Load](#view-resolver-methods)

#### [IsLoaded](#view-resolver-methods)

#### [Files](#view-resolver-methods)

#### [Exists](#view-resolver-methods)

#### [DotExtension](#view-resolver-methods)

#### [DefaultExtension](#view-resolver-methods)

#### [DefaultCompiler](#view-resolver-methods)

#### [Data](#view-resolver-methods)

#### [Compile](#view-resolver-methods)

#### [AddLocation](#view-resolver-methods)

#### [AddCompiler](#view-resolver-methods)

```go
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="utf-8" />
		<meta
			name="viewport"
			content="width=device-width, initial-scale=1" />
		<title>{{block "title" .}}Default Title{{end}}</title>
		<link
			crossorigin="anonymous"
			rel="stylesheet"
			href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" />
		{{block "head" .}}{{end}}
	</head>
	<body>
		{{block "header" .}}This is the header{{end}}
		{{block "body" .}}This is the body{{end}}
		{{block "footer" .}}This is the footer{{end}}
		<script
			crossorigin="anonymous"
			src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>
		{{block "foot" .}}{{end}}
	</body>
</html>
```

{% include footMatrixes.md %}
