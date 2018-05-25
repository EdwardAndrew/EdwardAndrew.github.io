---
layout: post
title: GoWeather
subtitle:
gh-repo: edwardandrew/goweather
gh-badge: [star, fork, watch, follow]
tags: [project]
---

- I'm currently working on this project, so more content will get getting added to this post as the project progresses. I will alter the date to ensure the order remains reverse chronological!

I've been toying with the idea of using Go for sometime now, and today I decided to finally look into writing my first program.

After following [A Tour of GO](https://tour.golang.org/welcome/1) and taking a look a the [standard library](https://golang.org/pkg/#stdlib) I felt comfortable enough to begin pulling in data from an API. I've recently been configuring [polybar](https://github.com/jaagr/polybar) on my machine and I've been considering adding some weather data onto it and I thought this seemed like a nice little project that could be leveraged to gain *some* experience with the language. I looked up (free) weather APIs and [OpenWeatherMap](https://www.openweathermap.org/) seemed to be the go to option.  

### defer
The first thing that really stood out to me with Go was being able to defer a function call until *after* the it's parent function has already returned. This is often used when working with the `net/http` library as http requests should call a `response.Body.Close()` function after any necessary processes have finished on `Body`. So natually this call can be deferred, so `Body` is safe to use until the end of the function.
```go
defer response.Body.Close()
```

### JSON Handling

I love how Go handles JSON, while the principle of mapping JSON data into a struct isn't new. It is done in a very clean and readable manner, as Go only requires that all the source files have the package declaration (and are all passed into the compiler!) these structs can be neatly placed into their own file without the need to add include statements in other files. Below are the first 20 lines of `OpenWeatherMapTypes.go`.
```go
package main

type OpenWeatherMapWeatherResponse struct {
    Coord OpenWeatherMapCoord `json:"coord"`
    Weather []OpenWeatherMapWeather `json:"weather"`
    Base string `json:"base"`
    Main OpenWeatherMapMain `json:"main"`
    Visibility int `json:"visibility"`
    Wind OpenWeatherMapWind `json:"wind"`
    Clouds OpenWeatherMapClouds `json:"clouds"`
    Dt int64 `json:"dt"`
    Sys OpenWeatherMapSys `json:"sys"`
    Id int `json:"id"`
    Name string `json:"name"`
    Cod int `json:"cod"`
}
```

### Progression - May 23rd
So far I've only spend a few hours on this project and it's been my first time ever using Go. I really like the language so far and I can see myself using it for more projects in the future. 

However, I've managed to get the application to take your API key and Location as arguemnts and it will output the temperature at the specified location in Celsius. Not very feature rich! However all of the data is being received from the API so I think the next task is writing a more advanced system for parsing all the arguments and outputting the information. I quite like the idea of being able to use  an arbitrary number of arguments and the system will just output all the data. This would mean people can `cut` or `grep` the outputted data  as they please!
