## Get direct dependencies for build target
```
❯ go list -deps  -f '{{define "M"}}{{if not .Indirect}}{{.Path}}@{{.Version}}{{end}}{{end}}{{with .Module}}{{if not .Main}}{{if .Replace}}{{template "M" .Replace}}{{else}}{{template "M" .}}{{end}}{{end}}{{end}}' cmd/example.go
github.com/fatih/color@v1.13.0
```

```
github.com/fatih/color@v1.13.0
```

## Get indirect dependencies for build target

```
❯ go list -deps  -f '{{define "M"}}{{if .Indirect}}{{.Path}}@{{.Version}}{{end}}{{end}}{{with .Module}}{{if not .Main}}{{if .Replace}}{{template "M" .Replace}}{{else}}{{template "M" .}}{{end}}{{end}}{{end}}' cmd/example.go | sort -u
```
```
github.com/mattn/go-colorable@v0.1.9
github.com/mattn/go-isatty@v0.0.14
golang.org/x/sys@v0.0.0-20210630005230-0f9fa26af87c
```


## Get relationships for dependencies
```
❯ go mod graph
```

```
go-example github.com/fatih/color@v1.13.0
go-example github.com/mattn/go-colorable@v0.1.9
go-example github.com/mattn/go-isatty@v0.0.14
go-example golang.org/x/sys@v0.0.0-20210630005230-0f9fa26af87c
github.com/fatih/color@v1.13.0 github.com/mattn/go-colorable@v0.1.9
github.com/fatih/color@v1.13.0 github.com/mattn/go-isatty@v0.0.14
github.com/mattn/go-colorable@v0.1.9 github.com/mattn/go-isatty@v0.0.12
github.com/mattn/go-colorable@v0.1.9 golang.org/x/sys@v0.0.0-20200223170610-d5e6a3e2c0ae
github.com/mattn/go-isatty@v0.0.14 golang.org/x/sys@v0.0.0-20210630005230-0f9fa26af87c
github.com/mattn/go-isatty@v0.0.12 golang.org/x/sys@v0.0.0-20200116001909-b77594299b42
```
