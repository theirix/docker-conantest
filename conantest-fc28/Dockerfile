# Using:
#   docker build . -t conantest-fc28
#   docker run --rm -v=/path/to/conan-libfoo:/conan -it conantest-fc28
#
FROM fedora:28

RUN dnf install -y make autoconf libtool automake git gcc gcc-c++ python3-pip

RUN pip3 install conan

RUN conan profile new --detect default

# Add cmake installer
RUN sed -E -ibak "/^.build_requires/a \*: cmake\\/3.18.1" /root/.conan/profiles/default

RUN conan install cmake/3.18.1@

RUN conan remote add bincrafters "https://api.bintray.com/conan/bincrafters/public-conan"

WORKDIR /conan
VOLUME /conan

CMD conan create --build=missing . user/testing

