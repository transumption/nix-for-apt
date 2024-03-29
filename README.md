## Setup

```sh
wget -O - https://transumption.gitlab.io/nix-for-apt/key.asc | sudo apt-key add -
echo 'deb [arch=amd64] http://transumption.gitlab.io/nix-for-apt buster main' \
  | sudo tee /etc/apt/sources.list.d/nix.list

sudo apt update
sudo apt install nix
```

See [`README.Debian`][] for usage.

### CI

If you want to set up your own instance of this CI, you will need to set
`APT_KEY` [protected variable][] to Base64-encoded secret GPG key.

To generate a new key, run:

```sh
(
  export GNUPGHOME=$(mktemp -d)
  gpg1 --batch --gen-key keygen
  gpg1 --export-secret-keys | (base64 -w0; echo)
)
```

If you plan to serve the repo to Debian users, I'd recommend to disable
"Settings -> Pages -> Force HTTPS" GitLab option, otherwise it will require
`apt-transport-https` package to be manually installed first.

## Thanks

All of the packaging work has been done by Thomas Koch.

[`README.Debian`]: https://salsa.debian.org/debian/nix/blob/master/debian/README.Debian
[protected variable]: https://docs.gitlab.com/ee/ci/variables/#protected-variables
