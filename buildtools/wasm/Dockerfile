FROM alpine:3
ARG TARGETARCH

RUN apk add binaryen curl xz
RUN mkdir -p /zig && curl -L https://ziglang.org/builds/zig-linux-$(echo $TARGETARCH | sed "s/amd64/x86_64/" | sed "s/arm64/aarch64/")-0.12.0-dev.3283+b8920bceb.tar.xz | tar -xJ --strip-components 1 -C /zig

ADD buildtools/wasm/version.txt version.txt
RUN mkdir -p /workspace && curl -L https://github.com/arwalk/zig-protobuf/archive/v1.0.3.tar.gz | tar -xz --strip-components 1 -C /workspace
WORKDIR /workspace

RUN /zig/zig build -Dtarget=wasm32-wasi --release=safe

CMD ["cp", "zig-out/bin/protoc-gen-zig.wasm", "/out/"]
