FROM golang:1.12 as builder

ENV GO111MODULE=on
ENV GOOS=linux
ENV GOARCH=amd64

COPY ./ /Users/atsushi/deploy-gke
WORKDIR /Users/atsushi/deploy-gke
RUN cd server && go build -o binfile
RUN chmod +x server/binfile

FROM alpine
ENV GOOS=linux
ENV GOARCH=amd64
EXPOSE 8080
COPY --from=builder /Users/atsushi/deploy-gke/server/binfile ./
RUN mkdir /lib64
RUN ln -s /lib/libc.musl-x86_64.so.1 /lib64/ld-linux-x86-64.so.2
CMD ["/binfile"]
