# Public Maven file repository

This repository serves Maven files anonymously over HTTPS. It is a static Git repository, not GitHub Packages.

- Releases: `https://raw.githubusercontent.com/spnettec/maven-repository/master/releases/`
- Snapshots: `https://raw.githubusercontent.com/spnettec/maven-repository/master/snapshots/`

Raw URLs are read-only download endpoints, not Maven deploy upload endpoints.
Stage approved Maven artifacts locally, review their files and checksums, then publish with an ordinary Git commit and push to `master`.
Preserve unrelated files and history. Never publish Git LFS pointers as Maven artifacts.
Same-version replacement is a reviewable Git change; consumers must refresh explicitly reviewed checksum locks and avoid stale local caches.
Versions remain a maintainer decision. Repeated binary replacement grows Git history.

## CI fork dependencies

The `com.github.heyoulin` artifacts listed in `fork-artifacts.sha256` are the minimum external fork dependencies required by the Nacos and Seata CI reactors:

- SOFA Bolt `1.6.20.1.B`: [fork source](https://github.com/spnettec/sofa-bolt).
- SOFA JRaft `1.4.1.B`: parent/extension POMs, core and gRPC adapter; [fork source](https://github.com/spnettec/sofa-jraft).
- Nacos `3.3.0.B`: client/API/common and required client plugins/adapters; [fork source](https://github.com/spnettec/nacos).

These are modified forks of their upstream projects. The 24 POM/JAR files are byte-for-byte copies of the existing private release artifacts, with SHA-256, SHA-1 and MD5 sidecars. The published GAVs were not changed or rebuilt. Parent POMs retain inherited license declarations; Apache-2.0 license texts and applicable NOTICE files are retained under `licenses/`. Third-party dependencies remain resolved from their normal repositories; unrelated private artifacts are not mirrored.

Seata itself is built in its own reactor and is not an external artifact required by these two CI runs; this initial dependency mirror does not claim to publish all Nacos or Seata server distributions. Fixed-version resolution uses the ordinary Maven path layout. Existing historical releases/snapshots are preserved.

Initial fork additions total 3,525,897 bytes of POM/JAR content; the largest file is 1,276,179 bytes, below GitHub's 50 MiB warning and 100 MiB hard limit. No LFS is used.
