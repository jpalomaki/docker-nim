FROM buildpack-deps:bookworm

ENV PATH=/opt/nim/bin:$PATH

# TODO: Figure out where the rest of the linux tarballs (arm64 etc) are
RUN set -eux; \
    dpkgArch="$(dpkg --print-architecture)"; \
    case "${dpkgArch##*-}" in \
        amd64) nimArch='x64'; sha256='ca1ffec35439a02b3102faf1c1caf5a033f929832b7fa2c76b3a6a7216f14f01' ;; \
        *) echo >&2 "Unsupported CPU architecture: ${dpkgArch}"; exit 1 ;; \
    esac; \
    wget -O nim.tar.xz "https://nim-lang.org/download/nim-2.0.0-linux_${nimArch}.tar.xz"; \
    echo "${sha256} nim.tar.xz" | sha256sum -c; \
    mkdir /opt/nim; \
    tar --extract --directory /opt/nim --strip-components=1 --file nim.tar.xz; \
    rm nim.tar.xz; \
    nim --version; \
    nimble --version
