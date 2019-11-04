# docker-conantest

Handy containers for local conan dev.

Docker images:
- `theirix/conantest-deb`: debian stable with gcc
- `theirix/conantest-el6scl4`: centos 6 with SCL devtoolset-4 with gcc 5.3

Images are built from the directories with same names and pushed to docker hub.

Both containers install `cmake_installer/1.0@conan/stable`.

## Usage

Running build from a local `conan-libfoo` directory:

    docker run --rm -v=`pwd`:/conan -it theirix/conantest-deb

Running a shell to examine things later:

    docker run --rm -v=`pwd`:/conan -it theirix/conantest-deb /bin/bash
    $ conan create . user/testing

## Rebuilding

    cd conantest-deb && docker build . -t theirix/conantest-deb
    cd conantest-el6scl && docker build . -t theirix/conantest-el6scl

