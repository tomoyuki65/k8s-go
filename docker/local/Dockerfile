FROM golang:1.24-alpine

WORKDIR /go/src

COPY ./src .

# モジュールの依存関係をインストール
RUN if [ -f ./go.mod ]; then \
      go install; \
    fi

# air をインストール
RUN go install github.com/air-verse/air@latest

EXPOSE 8080