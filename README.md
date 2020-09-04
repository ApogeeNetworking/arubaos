# go-arubaos

## Installation

Install via **go get**:

```shell
go get -u github.com/drkchiloll/arubaos
```

## Usage
Basic usage can be found below

```go
package main

import (
    "encoding/json"
    "fmt"
    "log"
    
    "github.com/drkchiloll/arubaos"
)

func main() {
    // Used in Development for SelfSigned Certs
    ignoreSSL := true
    // lms == Local Mobility Switch; it could be a Mobility Master or Controller
    lms := arubaos.New("host/ip", "user", "pass", ignoreSSL)

    err := lms.Login()
    if err != nil {
        log.Fatalf("%v", err)
    }
    // Query Mobility Master for AP Database
    // Set Up a Filter to Limit Return Count AND
    // Specify a Configuration Path (to specific Controller(s))
    f := arubaos.AFilter{Count: 1000, CfgPath: "/md"}
    // uri=/configuration/object/apdatabase?config_path=/md&count=1000
    aps, err := lms.GetMMApDb(f)
    // GetMMApDb returns an []MMAp (refer to apdb.go)
}
```
