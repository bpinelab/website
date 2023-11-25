# Tutrial for developers

## How I developed this template

- Create a new repository in my Github account.
- Open the repository with Github codespace.
- Get the latest hugo binary and place it in the specific path.
```
wget  https://github.com/gohugoio/hugo/releases/download/v0.120.4/hugo_extended_0.120.4_linux-amd64.tar.gz
tar xvfz tar xvfz hugo_extended_0.120.4_linux-amd64.tar.gz -C /usr/local/hugo/bin
```
- Copy docsy-example site.
```
hugo new site . --force
```
- 