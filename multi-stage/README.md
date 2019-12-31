# Test Multi Stage Build

## docker build .
```bash
# docker build .

Sending build context to Docker daemon  4.096kB
Step 1/9 : FROM alpine:3.10 as echo
 ---> 965ea09ff2eb
Step 2/9 : RUN echo "echo stage"
 ---> Using cache
 ---> 8fccb82362bd
Step 3/9 : FROM golang:1.12.9-alpine as builder
 ---> e0d646523991
Step 4/9 : RUN echo "build stage"
 ---> Using cache
 ---> 8bd95fb32229
Step 5/9 : COPY src/main.go .
 ---> Using cache
 ---> 1d435e1a3e7e
Step 6/9 : RUN go build -o /app main.go
 ---> Using cache
 ---> 801d51c242b1
Step 7/9 : FROM alpine:3.10
 ---> 965ea09ff2eb
Step 8/9 : CMD ["./app"]
 ---> Using cache
 ---> e2e26847692b
Step 9/9 : COPY --from=builder /app .
 ---> Using cache
 ---> df8c79186049
Successfully built df8c79186049
```

## docker build --target=echo .
```bash
# docker build --target=echo .

Sending build context to Docker daemon  5.632kB
Step 1/2 : FROM alpine:3.10 as echo
 ---> 965ea09ff2eb
Step 2/2 : RUN echo "echo stage"
 ---> Using cache
 ---> 8fccb82362bd
Successfully built 8fccb82362bd
```

## docker build --target=builder .
```
# docker build --target=builder .

Sending build context to Docker daemon  6.144kB
Step 1/6 : FROM alpine:3.10 as echo
 ---> 965ea09ff2eb
Step 2/6 : RUN echo "echo stage"
 ---> Using cache
 ---> 8fccb82362bd
Step 3/6 : FROM golang:1.12.9-alpine as builder
 ---> e0d646523991
Step 4/6 : RUN echo "build stage"
 ---> Using cache
 ---> 8bd95fb32229
Step 5/6 : COPY src/main.go .
 ---> Using cache
 ---> 1d435e1a3e7e
Step 6/6 : RUN go build -o /app main.go
 ---> Using cache
 ---> 801d51c242b1
Successfully built 801d51c242b1
```
