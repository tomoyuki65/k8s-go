####################
# ビルドステージ
####################
FROM golang:1.24-alpine AS builder

WORKDIR /go/src

COPY ./src .

# 依存関係を反映
RUN go install

# ビルド
RUN go build -o main .

####################
# 実行ステージ
####################
FROM alpine:3.21

WORKDIR /go/src

# コンテナ用ユーザー作成
RUN addgroup --system --gid 1001 appuser && \
    adduser --system --uid 1001 appuser

# ビルドステージで作成したバイナリをコピー
COPY --from=builder ./go/src/main .

# ポートを設定
EXPOSE 8080

# コンテナ起動ユーザー
USER appuser

# APIサーバー起動コマンド
CMD ["./main"]