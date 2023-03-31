## boilerplate
```go
package main

func main() {

}
```

## types
```go
func foo(bar type) return_type {

}
```

## variable declaration
```go
foo := 5
//  assigning (shadowing)
foo = 1
```

## structs
```go
type Foo struct{
	x int
	y int
}

// initializing struct
bar := Foo{
	x: 1,
	y:2,
}
```
## print
```go
fmt.Printf("Point %+v", pos) // + for debug print
```