FROM linuxkit/alpine:1b05307ae8152e3d38f79e297b0632697a30c65c AS mirror

RUN mkdir -p /out/etc/apk && cp -r /etc/apk/* /out/etc/apk/
RUN apk add --no-cache --initdb -p /out \
    alpine-baselayout \
    busybox \
    git \
    go \
    musl-dev
RUN rm -rf /out/etc/apk /out/lib/apk /out/var/cache

FROM scratch
ENV GOPATH=/go PATH=$PATH:/go/bin
COPY --from=mirror /out/ /
COPY --from=mirror /go/bin/ /go/bin/
COPY /compile.sh /compile.sh
ENTRYPOINT ["/compile.sh"]
