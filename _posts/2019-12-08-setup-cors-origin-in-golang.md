---
title: Setup CORS Origin in Golang
layout: post
author: adiatma
categories: golang
image: assets/images/cors.png
---

According to [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) Cors Origin Resource Sharing (CORS) is a mechanism that uses additional HTTP headers to tell browsers to give a web application running at one origin, access to selected resources from different origin.

CORS like a permissions access for communications HTTP in browsers, okay example you have a domain `http://frontend.com` and you request in javascript code to access `https://backend-api.com/` with using `fetch` or `axios` and getting data from server, and to able access from other origin you need to enable cors in `https://backend-api.com/`.

Okay, to enable CORS in golang we need to add some code in header response, below the example to using `net/http`.

```go
package main

import (
 "net/http"
)

func main() {
 http.HandleFunc("/", func(w http.ResposeWriter, r *http.Request) {
 // this keyword ("*") to allow all origin to access this endpoint
 w.Header().Set("Access-Control-Allow-Origin", "*")
 })
}
```

If using [gin-gonic](https://github.com/gin-gonic/gin) library please consider to using [gin-contrib](https://github.com/gin-contrib/cors) to enable cors.

```go
package main

import (
	"time"

	"github.com/gin-contrib/cors"
	"github.com/gin-gonic/gin"
)

func main() {
	router := gin.Default()
	// CORS for https://foo.com and https://github.com origins, allowing:
	// - PUT and PATCH methods
	// - Origin header
	// - Credentials share
	// - Preflight requests cached for 12 hours
	router.Use(cors.New(cors.Config{
		AllowOrigins:     []string{"https://foo.com"},
		AllowMethods:     []string{"PUT", "PATCH"},
		AllowHeaders:     []string{"Origin"},
		ExposeHeaders:    []string{"Content-Length"},
		AllowCredentials: true,
		AllowOriginFunc: func(origin string) bool {
			return origin == "https://github.com"
		},
		MaxAge: 12 * time.Hour,
	}))
	router.Run()
}
```

Okay, that is a short tutorial on how to enable CORS in golang.