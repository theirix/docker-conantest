# docker-conantest

Handy containers for local conan dev.

Containers:
- conantest-deb: debian 9 with gcc 6
- conantest-el6scl4: centos 6 with SCL devtoolset-4 with gcc 5.3

Both containers install `cmake_installer/1.0@conan/stable`.

## Usage

Building containers:

    cd conantest-deb && docker build . -t conantest-deb
    cd conantest-el6scl && docker build . -t conantest-el6scl

Running build from a local `conan-libfoo` directory:

    docker run --rm -v=`pwd`:/conan -it conantest-deb

Running a shell to examine things later:
    
		docker run --rm -v=`pwd`:/conan -it conantest-deb /bin/bash
    $ conan create . user/testing
