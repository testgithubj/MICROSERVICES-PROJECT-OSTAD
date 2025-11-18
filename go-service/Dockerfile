FROM golang:1.24-alpine

# CGO + sqlite এর জন্য প্যাকেজ
RUN apk add --no-cache gcc g++ musl-dev sqlite-dev

WORKDIR /app

# আগে শুধু go.mod কপি করে dependency cache নেব
COPY go.mod ./
RUN go mod download

# এখন বাকি কোড কপি
COPY . .

# এখানে go.sum/ডিপেন্ডেন্সি সব ঠিক করে নেবে
RUN go mod tidy

# 👉 CGO_ENABLED=1 রেখে binary build
RUN CGO_ENABLED=1 GOOS=linux GOARCH=amd64 go build -o urlshortner

# runtime ENV
ENV DB_PATH=/data/go.db \
    REDIS_HOST=redis \
    REDIS_PORT=6379

VOLUME ["/data"]
EXPOSE 8000

CMD ["./urlshortner"]
