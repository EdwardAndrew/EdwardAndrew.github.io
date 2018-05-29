---
layout: post
title: GoWeather
subtitle: First Go project
gh-repo: edwardandrew/goweather
gh-badge: [star, fork, watch, follow]
tags: [project]
---
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

### May 23rd
So far I've only spend a few hours on this project and it's been my first time ever using Go. I really like the language so far and I can see myself using it for more projects in the future. 

However, I've managed to get the application to take your API key and Location as arguemnts and it will output the temperature at the specified location in Celsius. Not very feature rich! However all of the data is being received from the API so I think the next task is writing a more advanced system for parsing all the arguments and outputting the information. I quite like the idea of being able to use  an arbitrary number of arguments and the system will just output all the data. This would mean people can `cut` or `grep` the output as they please!

### May 28th
While I didn't have much time today, I managed to spend a few minutes looking into the token parsing system mentioned above. 

The Go standard library already has a nice way of achieving this using the [flag package](https://golang.org/pkg/flag/).

Using the flag package, flags can easily be specified in the following style:
```go
apiKey := flag.String("key", "REQUIRED", "OpenWeatherMap Current Weather API key")
```
This needs to be followed by a call to `flag.Parse()`. This example will create the `-key` flag, it's value can be assigned quite easily by using `-key=VALUE`. The second paramter is the default value and the final parameter is the help text. Go's flag package has the rather neat function of automatically generating a `-h` or `--help` text for your application, the final parameter is the help text this is displayed when this command used. I chose to set the default value as required as it will appear more readable when a user uses the `--help` facility. This is what the output of `--help` will look like:
```
-key string
        OpenWeatherMap Current Weather API key (default "REQUIRED")
```
### May 29th - Finish
I finished the rest of the application today as it now functions as I intended. I used a switch statement to parse the tail of the arguments and output the value associated with it. The implied break statement in each case is a good feature, it defintely makes the code more readable. As you can see from the example, I also decided to include short versions of the commands!

```go
switch strings.ToLower(requestedData) {
        case "longitude", "lon":
            fmt.Println(requestedData, ":", weatherData.Coord.Lon)
        case "latitude", "lat":
            fmt.Println(requestedData, ":", weatherData.Coord.Lat)
        case "weatherid", "wid":
            fmt.Println(requestedData, ":", weatherData.Weather[0].Id)
        case "weatherdesc", "wd":
            fmt.Println(requestedData, ":", weatherData.Weather[0].Description)
        case "weathericon", "wi":
            fmt.Println(requestedData, ":", weatherData.Weather[0].Icon)
        case "base":
            fmt.Println(requestedData, ":", weatherData.Base)
        case "tempc", "tc":
            fmt.Println(requestedData, ":", KelvinToCelsius(weatherData.Main.Temp))
        .......
```

## Summary
This has been a nice project as an introduction to Go. But I think it's also worth noting that this is also my first project which I've blogged and also undertaken purely for the experience of using new technologies so I think I'll be summarising both of these. 

After using *DuckDuckGo* a little and doing some research, it paints a nice picture of the things Go can be used for ([see here](http://go-lang.cat-v.org/go-code)). As I've used C++ quite heavily in the past, I found it quite alien to not be putting any semicolons at the end of my statements and the type inference uses syntax that I have only seen in Prolog / answer set programming languages, however theres a nice element of familiarity with pointers and splices.

It's been cool to actually make progress updates on the project, it seems like a very effective way of ensuring that projects actually get completed and don't just get forgotten about. 

I enjoyed this little project so I think I will come back to Go with another idea in the future!
