# Using:
#   docker build . -t conantest-el6scl4
#   docker run --rm -v=/path/to/conan-libfoo:/conan -it conantest-el6scl4
#
FROM centos:6

# install devtoolset-4 (gcc5, fresh compiler)
# and python27 (needed for conan installation) SCL collections
RUN yum install -y centos-release-scl redhat-lsb-core && \
    yum install -y make autoconf libtool automake git devtoolset-4-gcc devtoolset-4-gcc-c++ python27-python-pip

RUN scl enable python27 -- pip install conan

# It will autodetect gcc5 from SCL
RUN scl enable devtoolset-4 python27 -- conan profile new --detect default

# Add cmake installer
RUN sed -E -ibak "/^.build_requires/a \*: cmake\\/3.18.1" /root/.conan/profiles/default

RUN conan install cmake/3.18.1@

RUN conan remote add bincrafters "https://api.bintray.com/conan/bincrafters/public-conan"

WORKDIR /conan
VOLUME /conan

CMD scl enable devtoolset-4 python27 -- conan create --build=missing . user/testing

