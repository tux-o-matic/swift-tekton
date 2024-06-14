# Swift on Tekton
Artifacts to build containerized Swift applications with Tekton.

## Swift executables on Linux
Swift has supported Linux since version 2.2.
More recent version of Swift added the possibility to Linux executables with the statically linked [musl libc](https://musl.libc.org).
By building Swift applications for Linux with a statically linked C library, the binary can be shipped in a raw Linux container with minimal footprint and 0 dependency.

## Tekton CI
With the right builder image with a full toolchain, a Swift server application for Linux can be built with Tekton on Kubernetes cluster.

Tasks breakdown og a Pipeline would be:
git-clone > compile project > Buildah
