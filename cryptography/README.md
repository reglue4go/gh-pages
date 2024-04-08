# Cryptography

{% include headOScoverage.md %}

> Table Of Contents
>
> -   [Introduction](#introduction)
> -   Available Structures
>     1.  [Aes Crypter](https://reglue4go.github.io/cryptography/aesCrypter)
>     1.  [Id Generator](https://reglue4go.github.io/cryptography/idGenerator)
>     1.  [Argon2 Hasher](https://reglue4go.github.io/cryptography/argon2Hasher)
>     1.  [Bcrypt Hasher](https://reglue4go.github.io/cryptography/bcryptHasher)
>     1.  [Id Transcoder](https://reglue4go.github.io/cryptography/idTranscoder)
>     1.  [Digester](https://reglue4go.github.io/cryptography/digester)
> -   [Unit Tests Matrix](#unit-tests-matrix)

## Introduction

The cryptography package provides an agnostic interface for data encrypting, decrypting, transcoding, identity generation and more.

```go
package main

import "github.com/reglue4go/cryptography"
import "github.com/reglue4go/cryptography/crypters"
import "github.com/reglue4go/cryptography/generators"

func main() {
	secretValue := "secret"
	defaultAlgorithm := "md5"
	encryptionKey := "6hdXj19qz9Nxaiu4CcVvtep3vPLhVfUL"

	digester := cryptography.NewDigester(defaultAlgorithm)

	md5 := digester.Make(secretValue)
	fmt.Printf("%v\n", md5)

	md5Check := digester.Check(secretValue, md5)
	fmt.Printf("%v\n", md5Check)
	// true

	sha256 := digester.SetAlgorithm("sha256").Make(secretValue)
	fmt.Printf("%v\n", sha256)

	sha256Check := digester.Check(secretValue, sha256)
	fmt.Printf("%v\n", sha256Check)
	// true

	ulid := generators.NewIdGenerator("ulid").Generate()
	fmt.Printf("%v\n", ulid)

	aesCrypter := crypters.NewAesCrypter(encryptionKey)

	encryptedSecret:= aesCrypter.Encrypt(secretValue)
	fmt.Printf("%v\n", encryptedSecret)

	decryptedSecret:= aesCrypter.Decrypt(encryptedSecret)
	fmt.Printf("%v\n", decryptedSecret == secretValue)
	// true
}

```

{% include footMatrixes.md %}
