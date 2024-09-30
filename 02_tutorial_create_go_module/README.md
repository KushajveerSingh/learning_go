# Create Go Module

Create a local package in the folder `greetings`.

Create a sec ond package `hello` which would call `greetings`. Since we have not published `greetings`, we need to use the local path.

Use this command `go mod edit --replace example.com/greetings=../greetings`. And then `go mod tidy`.

This will also add the following in `go.mod` (with this _pseudo-version number_ instead of semantic version, that you would use when publishing the package)

```
replace example.com/greetings => ../greetings

require example.com/greetings v0.0.0-00010101000000-000000000000
```

And this would use the local package.

Function naming convention

- First letter uppercase - The function is accessible to packages outside the current one.
- First letter lowercase - The function is only accessible in its own package.

Creating tests

- The function name starts with `Test`, like `TestHelloEmpty`.
- `go test -v` command will execute all functions starting with `Test` in files with name `*_test.go`.

Compile and install the application

- `go run` is a shortcut for compiling and running the program.
- `go build` - compiles the package, along with their dependencies. This produces a binary in the current folder, which you can call to run the program.
- `go install` - compiles and install the packages. The difference from `go build` is you don't have to specify the executable path when running it.
  - `go list -f '{{.Target}}'` - use this to identify where the package will be installed (in my case it is `/home/kushaj/go/bin/hello)`
  - Add the path to system shell `export PATH=$PATH:/path/to/your/install/directory`.
  - You can change the install location using `go env -w GOBIN=/path/to/your/bin`.
  - Run `go install` after you are done and it should produce binary in the above location.
  - Run the application using `hello` instead of `./hello` (which you would have done with `go build`).
