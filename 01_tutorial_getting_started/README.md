# Getting Started

1. Create `go.mod` to create a module. This is used to manage imports from other modules as well.

   Create it using `go mod init location`. If you are publishing your go module, this is the location where people can download it from. In this case just use `hello_world` as the location. And this will create the following `go.mod` file.

   ```
   module hello_world

   go 1.23.1
   ```

2. Run go program using `go run .` (this will compile and run all the go files in the directory).

   In go, a directory can only contain a single package. So there will always be one entry-point when you run the above command.

To use external packages like published on https://pkg.go.dev/

1. Search for package like https://pkg.go.dev/search?q=quote
2. Copy the name of the package from the top `rsc.io/quote/v4` and import it in your project as `import "rsc.io/quote/v4"`. And then run `go mod tidy` from command-line.

This would create `go.sum` file, which is used for authenticating packages. And also, add the entry in `go.mod` for the package.

Every package has a name `rsc.io/quote` and then optionally the version `rsc.io/quote/v4`.
