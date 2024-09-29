# Installing Go

[link](https://go.dev/doc/install)

1. Download latest Go Linux x86-64 version from https://go.dev/dl/ (1.23.1 in this case) and store it in `Downloads` folder.
2. `cd ~/Downloads`.
3. `sudo rm -rf /usr/local/go && sudo tar -C /usr/local -xzf ./go1.23.1.linux-amd64.tar.gz`.
4. Add `export PATH=$PATH:/usr/local/go/bin` to profile. (`code ~/.zshrc` and `source ~/.zshrc`)
5. `go version` to verify install.
6. Setup VSCode go plugin [link](https://marketplace.visualstudio.com/items?itemName=golang.go).
