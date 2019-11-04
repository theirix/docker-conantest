# Using:
#   docker build . -t conantest-deb
#   docker run --rm -v=/path/to/conan-libfoo:/conan -it conantest-deb
#
FROM debian:stable

RUN apt-get update && \
    apt-get install -y gcc libtool-bin automake autoconf binutils python3-pip vim-nox && \
    rm -rf /var/lib/apt/lists/*

RUN pip3 install conan

RUN conan profile new --detect default

# Add cmake installer
RUN sed -E -ibak "/^.build_requires/a \*: cmake_installer\\/1.0@conan\\/stable" /root/.conan/profiles/default

RUN conan install cmake_installer/1.0@conan/stable

RUN conan remote add bincrafters "https://api.bintray.com/conan/bincrafters/public-conan"

WORKDIR /conan
VOLUME /conan

CMD conan create --build=missing . user/testing

