# Using:
#   docker build . -t conantest-deb
#   docker run --rm -v=/path/to/conan-libfoo:/conan -it conantest-deb
#
FROM debian:stable

RUN apt update -y
RUN apt install -y gcc libtool-bin automake autoconf binutils python-pip

RUN pip install conan

RUN conan profile new --detect default

# Add cmake installer
RUN sed -E -ibak "/^.build_requires/a \*: cmake_installer\\/1.0@conan\\/stable" /root/.conan/profiles/default

WORKDIR /conan
VOLUME /conan

CMD conan create --build=missing . user/testing

