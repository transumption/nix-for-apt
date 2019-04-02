## Setup

```sh
wget -qO - https://transumption.gitlab.io/nix-for-apt/key.asc | sudo apt-key add -
echo 'deb http://transumption.gitlab.io/nix-for-apt v1 main' | sudo tee /etc/apt/sources.list.d/nix.list

sudo apt update
sudo apt install nix
```

Tested on Debian 10 and Ubuntu 18.10.

### CI

If you want to set up your own instance of this CI, you will need to set
`KEY` [protected variable][] to Base64-encoded secret GPG key.

To generate a new key, run:

```sh
(
  export GNUPGHOME=$(mktemp -d)
  gpg1 --batch --gen-key keygen
  gpg1 --export-secret-keys | (base64 -w0; echo)
)
```

[protected variable]: https://docs.gitlab.com/ee/ci/variables/#protected-variables
