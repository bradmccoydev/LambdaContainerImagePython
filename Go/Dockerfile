FROM golang:1.15 as builder
ADD go.mod go.sum main.go /go/src/
WORKDIR /go/src
RUN go mod tidy
RUN CGO_ENABLED=0 go build main.go

FROM public.ecr.aws/lambda/go as runtime


FROM debian:stable-slim
RUN mkdir -p /var/task /usr/local/bin /var/runtime
COPY --from=runtime /lambda-entrypoint.sh /
COPY --from=runtime /usr/local/bin/aws-lambda-rie /usr/local/bin
COPY --from=runtime /var/runtime/lib* /var/runtime/
COPY --from=runtime /var/runtime/aws-lambda-go /var/runtime/
RUN ln -s /var/runtime/aws-lambda-go /var/runtime/bootstrap
COPY --from=builder /go/src/example /var/task/
ENTRYPOINT ["/lambda-entrypoint.sh"]
CMD ["example"]