# Stringable

{% include headOScoverage.md %}

> Table Of Contents
>
> -   [Introduction](#introduction)
> -   [Available Methods](#available-methods)
> -   [Method Listing](#method-listing)
> -   [Unit Tests Matrix](#unit-tests-matrix)

## Introduction

The stringable package provides an expressive chainable interface for working with string values.

```go
package main

import "github.com/reglue4go/stringable"

func main() {
	title := stringable.New("Go").Append("LanG").Ucfirst().Value()

	fmt.Printf("%v\n", title)
	// Golang
}

```

## Available Methods

Each method available on the stringable instance may be chained to fluently manipulate the underlying value.
Almost every method returns a new stringable instance, allowing you to preserve the original copy of the value when necessary:

| &#8230;                             | &#8230;                       | &#8230;                           |
| :---------------------------------- | :---------------------------- | :-------------------------------- |
| [After](#after)                     | [AfterLast](#afterlast)       | [Append](#append)                 |
| [Basename](#basename)               | [Before](#before)             | [BeforeLast](#beforelast)         |
| [Between](#between)                 | [BetweenFirst](#betweenfirst) | [Camel](#camel)                   |
| [Contains](#contains)               | [ContainsAll](#containsall)   | [Dirname](#dirname)               |
| [Dump](#dump)                       | [EndsWith](#endswith)         | [Exactly](#exactly)               |
| [Explode](#explode)                 | [Headline](#headline)         | [IsEmpty](#isempty)               |
| [IsNotEmpty](#isnotempty)           | [Kebab](#Kebab)               | [Lcfirst](#lcfirst)               |
| [Length](#length)                   | [Limit](#limit)               | [Lower](#lower)                   |
| [Ltrim](#ltrim)                     | [NewLine](#newline)           | [Of](#Of)                         |
| [PadBoth](#padboth)                 | [PadLeft](#padleft)           | [PadRight](#padright)             |
| [Pipe](#pipe)                       | [Prepend](#prepend)           | [Remove](#remove)                 |
| [Repeat](#repeat)                   | [Replace](#replace)           | [ReplaceArray](#replacearray)     |
| [ReplaceFirst](#replacefirst)       | [Rtrim](#rtrim)               | [Slug](#slug)                     |
| [Snake](#snake)                     | [StartsWith](#startswith)     | [String](#string)                 |
| [Studly](#studly)                   | [Substr](#substr)             | [Title](#title)                   |
| [ToBoolean](#toboolean)             | [ToDate](#todate)             | [ToFloat](#tofloat)               |
| [ToInteger](#tointeger)             | [ToString](#tostring)         | [Trim](#trim)                     |
| [Ucfirst](#ucfirst)                 | [Unless](#unless)             | [Upper](#upper)                   |
| [Value](#value)                     | [When](#when)                 | [WhenContains](#whencontains)     |
| [WhenContainsAll](#whencontainsall) | [WhenEmpty](#whenempty)       | [WhenEndsWith](#whenendswith)     |
| [WhenExactly](#whenexactly)         | [WhenNotEmpty](#whennotempty) | [WhenNotExactly](#whennotexactly) |
| [WhenStartsWith](#whenstartswith)   | [Wrap](#wrap)                 | [ReplaceLast](#replacelast)       |
| [ReplaceNth](#replacenth)           |                               |                                   |

## Method Listing

#### [ReplaceNth](#available-methods)

The ReplaceNth method replaces the nth occurrence of a given value in a string:

```go
value := stringable.New("the fox jumps over the lazy dog").ReplaceNth("the", "A", 1).Value()
// "A fox jumps over the lazy dog"
```

#### [ReplaceLast](#available-methods)

The ReplaceLast method replaces the last occurrence of a given value in a string:

```go
value := stringable.New("the fox jumps over the lazy dog").ReplaceLast("the", "a").Value()
// "the fox jumps over a lazy dog"
```

#### [Wrap](#available-methods)

The Wrap method wraps the given string with an additional string or pair of strings:

```go
value := stringable.New("is").Wrap("This ", " golang")
// "This is golang"
```

#### [WhenStartsWith](#available-methods)

The WhenStartsWith method invokes the given closure if the string starts with the given sub-string. The closure will receive the string value:

```go
value := stringable.New("disney world").
	WhenStartsWith("disney", func(value string) string {
		return stringable.New(value).Title().String();
	}).Value()
// "Disney World"
```

#### [WhenNotExactly](#available-methods)

The WhenNotExactly method invokes the given closure if the string does not exactly match the given string. The closure will receive the string value

```go
value := stringable.New("alita").
	WhenNotExactly("Alita", func(value string) string {
		return stringable.New(value).Title().String();
	}).Value()
// "Alita"
```

#### [WhenNotEmpty](#available-methods)

The WhenNotEmpty method invokes the given closure if the string is not empty. If the closure returns a value, that value will also be returned by the whenNotEmpty method. If the closure does not return a value, the fluent string instance will be returned:

```go
value := stringable.New("Framework").
	WhenNotEmpty(func(value string) string {
		return stringable.New(value).Prepend("Gin ").String();
	}).Value()
// "Gin Framework"
```

#### [WhenExactly](#available-methods)

The WhenExactly method invokes the given closure if the string exactly matches the given string. The closure will receive the string value:

```go
value := stringable.New("Alita").
	WhenExactly("Alita", func(value string) string {
		return "99. " + value;
	}).Value()
// "99. Alita"
```

#### [WhenEndsWith](#available-methods)

The WhenEndsWith method invokes the given closure if the string ends with the given sub-string. The closure will receive the string value:

```go
value := stringable.New("disney world").
	WhenEndsWith("world", func(value string) string {
		return stringable.New(value).Title().String();
	}).Value()
// "Disney World"
```

#### [WhenEmpty](#available-methods)

The WhenEmpty method invokes the given closure if the string is empty. If the closure returns a value, that value will also be returned by the whenEmpty method. If the closure does not return a value, the fluent string instance will be returned:

```go
value := stringable.New(" ").
	WhenEmpty(func(value string) string {
		return "Avenger"
	}).Value()
// "Avenger"
```

#### [WhenContainsAll](#available-methods)

The WhenContainsAll method invokes the given closure if the string contains all of the given sub-strings. The closure will receive the string value:

```go
value := stringable.New("tony stark").
	WhenContainsAll([]string{"tony", "stark"}, func(value string) string {
		return stringable.New(value).Title().String();
	}).Value()
// "Tony Stark"
```

#### [WhenContains](#available-methods)

The WhenContains method invokes the given closure if the string contains the given value. The closure will receive the string value:

```go
value := stringable.New("tony stark").
	WhenContains("tony", func(value string) string {
		return stringable.New(value).Title().String();
	}).Value()
// "Tony Stark"
```

#### [When](#available-methods)

The When method invokes the given closure if a given condition is true. The closure will receive the string value:

```go
value := stringable.New("Birds").
	When(true, func(value string) string {
		return "Angry " + value
	}).Value()
// "Angry Birds"

value := stringable.New("Birds").
	When(false, func(value string) string {
		return "Angry " + value
	}, func(value string) string {
		return "Happy " + value
	}).Value()
// "Happy Birds"
```

#### [Value](#available-methods)

The Value method returns the underlying string value:

```go
value := stringable.New("This is my name").Value()
// "This is my name"
```

#### [Upper](#available-methods)

The Upper method converts the given string to uppercase:

```go
value := stringable.New("golang").Upper().Value()
// GOLANG
```

#### [Unless](#available-methods)

The Unless method applies the callback if the given "value" is (or resolves to) falsy.

```go
value := stringable.New("Birds").
	Unless(false, func(value string) string {
		return "Angry " + value
	}).Value()
// "Angry Birds"

value := stringable.New("Birds").
	Unless(true, func(value string) string {
		return "Angry " + value
	}, func(value string) string {
		return "Happy " + value
	}).Value()
// "Happy Birds"
```

#### [Ucfirst](#available-methods)

The Ucfirst method returns the given string with the first character capitalized:

```go
value := stringable.New("foo bar").Ucfirst()
// "Foo bar"
```

#### [Trim](#available-methods)

The Trim method trims the given string:

```go
value := stringable.New("$day$").Trim().Value()
// "day"
```

#### [ToString](#value)

The ToString method returns the underlying string value:

#### [ToInteger](#available-methods)

The ToInteger method returns an integer value from string:

```go
value := stringable.New("99").ToInteger()
// 99
```

#### [ToFloat](#available-methods)

The ToFloat method returns a float value from string:

```go
value := stringable.New("9.9").ToFloat()
// 9.9
```

#### [ToDate](#available-methods)

The ToDate method returns a date time instance from string value:

```go
value := stringable.New("now").ToDate().Format("2006-01-02 15:04:05")
// 2024-03-29 12:22:35.913399 +0400 +04 m=+0.000832834
```

#### [ToBoolean](#available-methods)

The ToBoolean method returns the underlying string value:

```go
value := stringable.New("true").ToBoolean()
value := stringable.New("True").ToBoolean()
// true
value := stringable.New("false").ToBoolean()
value := stringable.New("False").ToBoolean()
value := stringable.New("invalid").ToBoolean()
// false
```

#### [Title](#available-methods)

The Title method converts the given string to Title Case:

```go
value := stringable.New("a nice title uses the correct case").Title().Value()
// "A Nice Title Uses The Correct Case"
```

#### [Substr](#available-methods)

The Substr method returns the portion of the string specified by the given start and length parameters:

```go
value := stringable.New("Boney James").Substr(0, 5).Value()
// "Boney"
value := stringable.New("Boney James").Substr(-5, 0).Value()
// "James"
```

#### [Studly](#available-methods)

The Studly method converts the given string to StudlyCase:

```go
value := stringable.New("foo_bar").Studly().Value()
// "FooBar"
```

#### [String](#value)

The String method returns the underlying string value:

#### [StartsWith](#available-methods)

The StartsWith method determines if the given string begins with the given value:

```go
value := stringable.New("This is my name").StartsWith("This")
// true
```

#### [Snake](#available-methods)

The Snake method converts the given string to snake_case:

```go
value := stringable.New("fooBar").Snake().Value()
// "foo_bar"
```

#### [Slug](#available-methods)

The Slug method generates a URL friendly "slug" from the given string:

```go
value := stringable.New("Reglue Framework").Slug("-").Value()
// "reglue-framework"
```

#### [Rtrim](#available-methods)

The Rtrim method trims the right side of the given string:

```go
value := stringable.New("$day$").Rtrim().Value()
// "$day"
```

#### [ReplaceFirst](#available-methods)

The ReplaceFirst method replaces the first occurrence of a given value in a string:

```go
value := stringable.New("the quick brown fox jumps over the lazy dog").ReplaceFirst("the", "a").Value()
// "a quick brown fox jumps over the lazy dog"
```

#### [ReplaceArray](#available-methods)

The ReplaceArray method replaces a given value in the string sequentially using an array:

```go
value := stringable.New("The event will take place between ? and ?").ReplaceArray("?", "8:30", "9:00").Value()
// "The event will take place between 8:30 and 9:30"
```

#### [Replace](#available-methods)

The Replace method replaces a given string within the string:

```go
value := stringable.New("Golang 1.18.x").Replace("18.x", "22.x").Value()
// "Golang 1.22.x"
```

#### [Repeat](#available-methods)

The Repeat method repeats the given string:

```go
value := stringable.New("a").Repeat(5).Value()
// "aaaaa"
```

#### [Remove](#available-methods)

The Remove method removes the given value or array of values from the string:

```go
value := stringable.New("Go is quite beautiful!").Remove("quite").Value()
// "Go is beautiful!"
```

#### [Prepend](#available-methods)

The Prepend method prepends the given values onto the string:

```go
value := stringable.New("Go!").Prepend(" ", "Awesome").Value()
// "Awesome Go!"
```

#### [Pipe](#available-methods)

The Pipe method allows you to transform the string by passing its current value to the given callable:

```go
value := stringable.New("Angry").
	Pipe(func(value string) string {
		return value + " Birds"
	}).Value()
// "Angry Birds"
```

#### [PadRight](#available-methods)

The PadRight method pads the right side of a string with another string until the final string reaches the desired length:

```go
value := stringable.New("James").PadRight("10, '_'").Value()
// "James___"
```

#### [PadLeft](#available-methods)

The PadLeft method pads the left side of a string with another string until the final string reaches the desired length

```go
value := stringable.New("James").PadLeft("10, '_'").Value()
// "__James"
```

#### [PadBoth](#available-methods)

The PadBoth method pads both sides of a string with another string until the final string reaches the desired length:

```go
value := stringable.New("James").PadBoth("10, '_'").Value()
// "__James___"
```

#### [Of](#available-methods)

The Of method creates a new stringable instance:

```go
value := stringable.New("awesome").Of("Framework").Value()
// "Framework"
```

#### [NewLine](#available-methods)

The NewLine method appends an "end of line" character to a string:

```go
value := stringable.New("Reglue").NewLine().Append("Framework").Value()
// "Reglue"
// "Framework"
```

#### [Ltrim](#available-methods)

The Ltrim method trims the left side of the string:

```go
value := stringable.New("$day$").Ltrim().Value()
// "day$"
```

#### [Lower](#available-methods)

The Lower method converts the given string to lowercase:

```go
value := stringable.New("GOLANG").Lower().Value()
// golang
```

#### [Limit](#available-methods)

The Limit method truncates the given string to the specified length:

```go
value := stringable.New("The quick brown fox jumps over the lazy dog").Limit(20)
// "The quick brown fox..."
value := stringable.New("The quick brown fox jumps over the lazy dog").Limit(20, " ***")
// "The quick brown fox ***"
```

#### [Length](#available-methods)

The Length method returns the length of the given string:

```go
value := stringable.New("Golang").Length()
// 6
```

#### [Lcfirst](#available-methods)

The Lcfirst method returns the given string with the first character lowercased:

```go
value := stringable.New("Foo Bar").Lcfirst()
// "foo Bar"
```

#### [Kebab](#available-methods)

The Kebab method converts the given string to kebab-case:

```go
value := stringable.New("fooBar").Kebab()
// "foo-bar"
```

#### [IsNotEmpty](#available-methods)

The IsNotEmpty method determines if the given string is not empty:

```go
value := stringable.New(" ").IsNotEmpty()
// false
value := stringable.New("Golang").IsNotEmpty()
// true
```

#### [IsEmpty](#available-methods)

The IsEmpty method determines if the given string is empty:

```go
value := stringable.New(" ").IsEmpty()
// true
value := stringable.New("Golang").IsEmpty()
// false
```

#### [Headline](#available-methods)

The Headline method will convert strings delimited by casing, hyphens, or underscores into a space delimited string with each word's first letter capitalized:

```go
value := stringable.New("Email-Notification_Sent").Headline()
// "Email Notification Sent"
value := stringable.New("jane_doe").Headline(language.BritishEnglish)
// "Jane Doe"
```

#### [Explode](#available-methods)

The Explode method splits the string by the given delimiter and returns a collection containing each section of the split string:

```go
value := stringable.New("foo bar baz").Explode(" ")
// ["foo" "bar" "baz"]
```

#### [Exactly](#available-methods)

The Exactly method determines if the given string is an exact match with another string:

```go
value := stringable.New("Golang").Exactly("Golang")
// true
```

#### [EndsWith](#available-methods)

The EndsWith method determines if the given string ends with the given value:

```go
value := stringable.New("This is my name").EndsWith("name")
// true
```

#### [Dump](#available-methods)

The Dump method writes the string to standard output:

```go
value := stringable.New("Write to standard output").Dump().Value()
// "Write to standard output"
```

#### [Dirname](#available-methods)

The Dirname method returns the parent directory portion of the given string:

```go
value := stringable.New("/foo/bar/baz").Dirname().Value()
// "/foo/bar"
```

#### [ContainsAll](#available-methods)

The ContainsAll method determines if the given string contains all of the values in the given array:

```go
value := stringable.New("This is my name").ContainsAll("my", "name")
// true
```

#### [Contains](#available-methods)

The Contains method determines if the given string contains the given value. This method is case sensitive:

```go
value := stringable.New("This is my name").Contains("my")
// true
```

#### [Camel](#available-methods)

The Camel method converts the given string to camelCase:

```go
value := stringable.New("foo_bar").Camel().Value()
// "fooBar"
```

#### [BetweenFirst](#available-methods)

The BetweenFirst method returns the smallest possible portion of a string between two values:

```go
value := stringable.New("[a] bc [d]").BetweenFirst("[", "]").Value()
// "a"
```

#### [Between](#available-methods)

The Between method returns the portion of a string between two values:

```go
value := stringable.New("This is my name").Between("This", "name").Value()
// " is my "
```

#### [BeforeLast](#available-methods)

The BeforeLast method returns everything before the last occurrence of the given value in a string:

```go
value := stringable.New("This is my name").BeforeLast("is").Value()
// "This "
```

#### [Before](#available-methods)

The Before method returns everything before the given value in a string:

```go
value := stringable.New("This is my name").Before("my name").Value()
// "This is "
```

#### [Basename](#available-methods)

The Basename method will return the trailing name component of the given string:

```go
value := stringable.New("/foo/bar/baz").Basename().Value()
// "baz"
```

#### [Append](#available-methods)

The Append method appends the given values to the string:

```go
value := stringable.New("Paula").Append(" ", "White").Value()
// "Paula White"
```

#### [AfterLast](#available-methods)

The AfterLast method method returns everything after the last occurrence of the given value in a string. The entire string will be returned if the value does not exist within the string:

```go
value := stringable.New("internal.controllers.users.controller").AfterLast(".").Value()
// "controller"
```

#### [After](#available-methods)

The After method method returns everything after the given value in a string. The entire string will be returned if the value does not exist within the string:

```go
value := stringable.New("This is my name").After("This is").Value()
// " my name"
```

{% include footMatrixes.md %}
