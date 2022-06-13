## Get dependencies for build target
```
❯ go list -deps -f '{{define "M"}}{{.Path}}@{{.Version}}{{end}}{{with .Module}}{{if not .Main}}{{if .Replace}}{{template "M" .Replace}}{{else}}{{template "M" .}}{{end}}{{end}}{{end}}' cmd/example.go | sort -u
```

```
github.com/fatih/color@v1.13.0
github.com/mattn/go-colorable@v0.1.9
github.com/mattn/go-isatty@v0.0.14
golang.org/x/sys@v0.0.0-20210630005230-0f9fa26af87c
```

```
❯ go build cmd/example.go && go version -m example
```
```
example: go1.17.2
	path	command-line-arguments
	mod	go-example	(devel)
	dep	github.com/fatih/color	v1.13.0	h1:8LOYc1KYPPmyKMuN8QV2DNRWNbLo6LZ0iLs8+mlH53w=
	dep	github.com/mattn/go-colorable	v0.1.9	h1:sqDoxXbdeALODt0DAeJCVp38ps9ZogZEAXjus69YV3U=
	dep	github.com/mattn/go-isatty	v0.0.14	h1:yVuAays6BHfxijgZPzw+3Zlu5yQgKGP2/hcQbHb7S9Y=
	dep	golang.org/x/sys	v0.0.0-20210630005230-0f9fa26af87c	h1:F1jZWGFhYfh0Ci55sIpILtKKK8p3i2/krTr0H1rg74I=
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
