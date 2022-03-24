.PHONY: build test dist snapshot dev-requirements requirements
VERSION := $(shell git describe --always |sed -e "s/^v//")

build:
	mkdir -p build
	go build -ldflags "-s -w -X main.version=$(VERSION)" -o build/chirpstack-packet-multiplexer cmd/chirpstack-packet-multiplexer/main.go

clean:
	rm -rf build
	rm -rf dist
	rm -rf docs/public

test:
	go vet ./...
	go test -v ./...

dist:
	goreleaser
	mkdir -p dist/upload/tar
	mkdir -p dist/upload/deb
	mv dist/*.tar.gz dist/upload/tar
	mv dist/*.deb dist/upload/deb

snapshot:
	goreleaser --snapshot

dev-requirements:
	go install golang.org/x/tools/cmd/stringer
	go install github.com/goreleaser/goreleaser
	go install github.com/goreleaser/nfpm

