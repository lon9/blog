---
categories: [
  "Programming"
]
date: "2015-11-19T00:23:49+09:00"
description: "Twitter Streaming API broadcasts tweet or some activities in real time.  It's usefull to collect information for analizing big data, developing twitter alient app etc...  I introduce to use it with golang."
tags: [
  "Go"
]
title: "How To Use Twitter Streaming API With Go"
---

[ChimeraCoder/anaconda](https://github.com/ChimeraCoder/anaconda) is Twitter API client written with Golang.  This library support Twitter Streaming API, Here is a example for using Twitter Streaming API

```go
package main

import(
    "github.com/ChimeraCoder/anaconda"
    "net/url"
    "fmt"
)

func main(){
    anaconda.SetConsumerKey(<Consumer Key>)
    anaconda.SetConsumerSecret(<Consumer Secret>)
    client := anaconda.NewTwitterApi(<Access Token>, <Access Token Secret>)

    // Setting parameter using url.Values
    v := url.Values{}
    v.Set("locations", "<Locations>") // or v.Set("track", "<track>")
    s := client.PublicFilterStream(v)

    for{
      item := <-s.C
      switch status := item.(type){
      case anaconda.Tweet:
        fmt.Println(status.Text)
			deafult:
      }
    }
}
```


That's it.
It using goroutine, so we can take tweet whenever we like.
