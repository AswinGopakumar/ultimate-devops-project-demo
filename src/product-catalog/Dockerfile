FROM golang:1.22-alpine AS build

WORKDIR /usr/src/app

COPY go.mod .

RUN go mod download

COPY . .

RUN go build -o /go/bin/product-catalog ./


FROM alpine AS release

WORKDIR /ust/src/app/

COPY ./products ./products

COPY --from=build /go/bin/product-catalog ./
ENV PRODUCT_CATALOG_PORT 8088
ENTRYPOINT ["./product-catalog"]
