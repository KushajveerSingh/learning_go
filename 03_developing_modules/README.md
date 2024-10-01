# Developing Modules

General process

1. Develop the module locally, by using its local path (using `replace` command).
2. Publish v0 and keep working on it till you are ready for v1. In v0, no stability is guaranteed. Release alphas and betas.
3. Publish v1, which is a stable release. v1 does not have to be backward compatible with v0.
4. If a breaking change needs to be introduced, create v2. By breaking change we mean, the user code has to change, to use the new version.

Stable release means

- Users can upgrade to minor and patch version without breaking their own code.
- There will be not changes to module's public API, that break backward compatibility.
- No exported types would be removed, without breaking backward compatibility.
- Future changes to API, like adding a new field to a struct will be backward compatible and will be included in a new minor release.
- Bug fixes and security fixes will be included in patch release or minor release.

Semantic versioning

- patch release - no changes to public API. Also, your package's dependencies should only be upgraded to patch version as well.
- minor release - make non-breaking changes to module's public API i.e. the calling code should not break.

`go get` can be used to get source code for packages your code imports. This is how it works

1. From `import` statements in go source code, get all the modules paths.
2. Using the URL locate the module source and then download it to the local module cache.

How to organize modules. Use this file structure for a module

```
example.com/mymodule

LICENSE
go.mod
go.sum
internal/
    - auth/
        - auth.go
    - hash/
        - hash.go
- package1/
    - func1.go
- package2/
    - func2.go
```

You can publish each module in a separate git repo or have multiple modules in a single repo as well. So package `modname` would be stored in `modname` github repo. And then you can import it as `import "github.com/KushajveerSingh/modname"`.

Also, move packages to `internal` that you don't want to expose to public. You are free to make changes to packages in internal without worrying about backwards compatibility. Putting the packages in `internal` makes them accessible only within the module or parent directory.

You can have a single module exporting multiple packages, which people can install separately.

```
example.com/modname
- go.mod
- go.sum
- package1
    - func.go
- package2
    - func.go
```

Users can install these as

```
go install github.com/KushajveerSingh/modname/package1@latest
go install github.com/KushajveerSingh/modname/package1@latest
```

`cmd` directory is used to put files that pull everything together to make a binary. Like setup logic for running the application, such as parsing command-line flags and calling functions from other parts of your project.

```
cmd/
    - package1/
        - main.go
    - package2/
        - main.go
```

And then install these as

```
go install github.com/KushajveerSingh/modname/cmd/package1@latest
go install github.com/KushajveerSingh/modname/cmd/package1@latest
```

For web servers, you won't have packages for export. So have everything inside `internal`. And use `cmd` folder to store all the commands.
