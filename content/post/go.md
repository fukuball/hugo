+++
title = "Go"
date = "2017-06-26T10:21:53+08:00"
draft = false
subtitle = ""
tags = []
comments = true
+++

# Go

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non
proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

```
package main

import "fmt"

func plus(a int, b int) int {
    return a + b
}

func plusPlus(a, b, c int) int {
    return a + b + c
}

func main() {
    res := plus(1, 2)
    fmt.Println("1+2 =", res)
    res = plusPlus(1, 2, 3)
    fmt.Println("1+2+3 =", res)
}
```