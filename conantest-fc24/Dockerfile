# Using:
#   docker build . -t conantest-fc24
#   docker run --rm -v=/path/to/conan-libfoo:/conan -it conantest-fc24
#
FROM fedora:24

RUN dnf install -y make autoconf libtool automake git gcc gcc-c++ \
			zlib-devel bzip2 bzip2-devel readline-devel sqlite \
			sqlite-devel openssl-devel xz xz-devel libffi-devel findutils

RUN git clone git://github.com/yyuu/pyenv.git .pyenv

ENV PYENV_ROOT $HOME/.pyenv
ENV PATH $PYENV_ROOT/shims:$PYENV_ROOT/bin:$PATH

RUN pyenv install 3.6.11
RUN pyenv global 3.6.11
RUN pyenv rehash

RUN pip install conan

RUN conan profile new --detect default

# Add cmake installer
RUN sed -E -ibak "/^.build_requires/a \*: cmake\\/3.18.1" /root/.conan/profiles/default

RUN conan install cmake/3.18.1@

RUN conan remote add bincrafters "https://api.bintray.com/conan/bincrafters/public-conan"

WORKDIR /conan
VOLUME /conan

CMD conan create --build=missing . user/testing

