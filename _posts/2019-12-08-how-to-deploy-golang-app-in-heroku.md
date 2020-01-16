---
title: How to deploy golang app in heroku
layout: post
image: assets/images/heroku-yml.png
author: adiatma
categories: golang
---

Heroku is a platform as a service (Paas) that enable you to deploy and building web apps and save to the cloud. Heroku support any languages or framework like NodeJS, Golang, Ruby, PHP, Python, Scala, and Clojure.

You can be using heroku with premium and free features. please check this [link](https://www.heroku.com/pricing) to compare it.

Okay, today I'm trying to show you, about how to deploy web build with golang to heroku, before start, please make sure you have an account in heroku, if not please [register](https://signup.heroku.com/) before.

## Lets get started

First step create directory with name `deploy-golang-app-in-heroku` and initialize with go module `go mod init github.com/<your_username>/deploy-golang-app-in-heroku` so then this command automates generate new file `go.mod` in your root directory.


Please create `main.go` in the root directory and fill with the example script below.

```go
package main

import (
 "encoding/json"
 "fmt"
 _ "github.com/joho/godotenv/autoload"
 "log"
 "net/http"
 "os"
)

// Response types
type Response struct {
 Status int `json:"status"`
 Response string `json:"response"`
}

func main() {
 http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
 res := Response{}
 res.Status = http.StatusOK
 res.Response = "Hello Golang"
 json.NewEncoder(w).Encode(res)
 })

 log.Fatal(http.ListenAndServe(fmt.Sprintf(":%s", os.Getenv("PORT")), nil))
}
```

Okay next create file `.env` and fill with `PORT=8080` to define dynamic port, and then to read `.env` in golang I'm using `https://github.com/joho/godotenv` library.

Okay, next let's create `Dockerfile` to define all commands to using for build golang app, and save in root directory.

```Dockerfile
FROM golang:latest

ADD . /app

WORKDIR /app

RUN go mod download

RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build

RUN chmod +x ./deploy-golang-app-in-heroku

EXPOSE 8080

CMD ./deploy-golag-app-in-heroku
```

Next create file `heroku.yml` to building docker images like `docker-compose` in docker, for more references please [check this out](https://devcenter.heroku.com/articles/build-docker-images-heroku-yml).

```yml
build:
 docker:
 web: Dockerfile
 worker:
 dockerfile: Dockerfile
```

Okey finish, please push your code to github.

## Heroku Dashboard

Please login to [heroku dashboard](https://dashboard.heroku.com/), and create a new app suitable with your repo name to easy maintain in the future, I'm using same name with repository github.

Deployment method, please choose github and then connect with your repository.

Next, please go to the  `setting` menu in heroku, like image bellow, fill suitable with your `.env`.

<img src="{{ site.base_url }}/assets/images/config-var.png" />

Okey finish, please see the example [repo](https://github.com/adiatma/deploy-golang-app-in-heroku) and [demo](https://deploy-golang-app-in-heroku.herokuapp.com/) for this tutorial.

Thanks.