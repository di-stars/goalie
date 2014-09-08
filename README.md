# goalie

[![travis](https://travis-ci.org/intelekshual/go-simpleflake.svg)](https://travis-ci.org/intelekshual/goalie)

Simple ACLs in Go, because ACLs don't need to be complicated

## Installation

    $ go get -u github.com/intelekshual/goalie

## Usage

```go
import (
  "github.com/intelekshual/goalie
)

func main() {
  acl := goalie.NewMemoryProvider()
  // ...
}
```

Or, if you want to access your ACLs across processes, you can use the built-in RedisProvider.

```go
  acl := goalie.NewRedisProvider(map[string]string{
    "prefix": "goalie:",
    "network": "tcp",
    "address": ":6379"
  })
```

### Grant:

```go
if err := acl.Grant("luke-skywalker", "the-force"); err != nil {
  log.Fatal("Could not grant Luke Skywalker access to the Force")
}
```

### Assert:

```go
if ok, err := acl.Assert("luke-skywalker", "the-force"); err != nil {
  log.Fatal("Could not determine if Luke Skywalker has access to the Force")
}

if ok {
  log.Println("Luke Skywalker has the Force!")
} else {
  log.Println("Luke Skywalker doesn't have the Force!")
}

```

### Revoke:

```go
if err := acl.Revoke("luke-skywalker", "the-force"); err != nil {
  log.Fatal("Could not revoke Luke Skywalker's access to the Force")
}
```

## License

The MIT License (MIT)

Copyright (c) 2014 Robert Coker

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.