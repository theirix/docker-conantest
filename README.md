# docker-conantest

Handy containers for local conan dev.

Docker images:
- `theirix/conantest-deb`: Debian 10 with gcc 8
- `theirix/conantest-fc28`: Fedora 28 with gcc 8
- `theirix/conantest-fc24`: Fedora 24 with gcc 6

Unsupported images:
- `theirix/conantest-el6scl4`: centos 6 with SCL devtoolset-4 with gcc 5.3. Does not support Python 3 so latest Conan cannot be installed.

Images are built from the directories with same names and pushed to Docker Hub.

All containers have preinstalled Conan 1.28, compiler and a build requirement `cmake/3.18.1`.

## Usage

Run a package build from a local `conan-libfoo` directory:

    docker run --rm -v=`pwd`:/conan -it theirix/conantest-deb

Run a package install from a local `conan-app` directory:

    docker run --rm -v=`pwd`:/conan -it theirix/conantest-deb conan install .

Running a shell to examine things later:

    docker run --rm -v=`pwd`:/conan -it theirix/conantest-deb /bin/bash
    $ conan create . user/testing

## Rebuilding images

    cd conantest-deb && docker build . -t theirix/conantest-deb

