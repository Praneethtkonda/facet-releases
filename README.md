# Facet releases

This public repository hosts customer-downloadable Facet release assets. Source code lives in the private Facet repository; this repository is only the distribution surface for tagged releases.

For each tag, download:

1. the `facet_<version>_<os>_<arch>` CLI archive for your workstation or server;
2. `checksums.txt` and verify the archive;
3. optionally, the offline image bundle for your Linux server's edition and architecture.

Example:

```sh
VERSION=v0.1.0
curl -L -O https://github.com/Praneethtkonda/facet-releases/releases/download/${VERSION}/facet_${VERSION#v}_linux_amd64.tar.gz
curl -L -O https://github.com/Praneethtkonda/facet-releases/releases/download/${VERSION}/checksums.txt
sha256sum --check --ignore-missing checksums.txt
tar xzf facet_${VERSION#v}_linux_amd64.tar.gz
sudo install -m 0755 facet /usr/local/bin/facet
facet install --edition plus --yes
```

Offline Docker install:

```sh
VERSION=v0.1.0
EDITION=plus
ARCH=amd64
curl -L -O https://github.com/Praneethtkonda/facet-releases/releases/download/${VERSION}/facet-bundle_${VERSION#v}_${EDITION}_linux_${ARCH}.tar
curl -L -O https://github.com/Praneethtkonda/facet-releases/releases/download/${VERSION}/facet-bundle_${VERSION#v}_${EDITION}_linux_${ARCH}.json
curl -L -O https://github.com/Praneethtkonda/facet-releases/releases/download/${VERSION}/sha256sums.txt
sha256sum --check --ignore-missing sha256sums.txt
facet install --edition ${EDITION} --offline . --yes
```

Offline Kubernetes (RKE2) install: also download `facet-rke2_${VERSION#v}_linux_${ARCH}.tar` (RKE2 and helm) into the same folder, then run `sudo facet install --target rke2 --edition ${EDITION} --offline .`. If RKE2 is not installed, the installer offers to install it from the kit.

Offline bundles are published for final releases (not release candidates). If a bundle is split into `.part000`, `.part001`, ... files, download all parts plus the `.json` sidecar and `sha256sums.txt`, then pass the directory to `facet install --offline`.

Facet is proprietary commercial software. A signed licence file is required after the trial period.
