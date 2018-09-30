---
layout: post
title: XPlane Illuminate Plugin
subtitle: RGB Keyboard illumination integration for XPlane 11.
gh-repo: edwardandrew/xplane-illuminate
gh-badge: [star, fork, watch, follow]
tags: [project]
---
# XPlane 11
XPlane 11 is a cross platform flight simulator application developed by Laminar Research. Those that know me well should know that besides programming, I also have a passion for avaiation and as such spend quite a while using flight simulation programs.
# About this project
_XPlane-Illuminate_ is an XPlane Plugin that aims to provide functionality for users to add their own colour mappings to their RGB keyboards, powered by XPlane DataRefs.

I used Corsair's CUE SDK to drive the keyboard illumination, this was a surprisingly painless experience, the SDK is actually quite straight forward to use when referring to the documentation. 

I would like to add support for Razer and Logitech devices, however the only RGB keyboard that I currenly own is a Corsair one.

# Configuration
The plugin allows the user to create their own configurations, they define their own colors, conditions and select which keys will change color when these conditions are met. All this information is stored in a json file, which is parsed when the application loads.

There are three main parts to the json config file:
## Colors
Colors can be defined as variables, and then referred to by name later in the json file, this means a color with the name `background` can be defined in one place, and if the user wishes to change the value of this color, they only need to do it in one place.
## Conditions
Condtions have a friendly `name`,  take the string of the XPlane DataRef to be used, a `match` parameter and a `value` parameter which the condition will be matched on. Some XPlane DataRefs return arrays, for these DataRefs an `index` should be given, otherwise the index defaults to 0.

A condition will look similar to this:

``` 
{
  "name": "gearHandleDown",
  "dataRef": "sim/cockpit/switches/gear_handle_status",
  "match": "exactly",
  "value": 1
}
```
There are currently three accepted values for `match`:
- _exactly_
- _less\_than_
- _greater\_than_

This part of the file can currently get quite messy if you want to specify lots of conditions. So I'm open to suggestions here!
## Keys
Keys have an array of conditions, a `color` value and a `key` value. 

The key requires all of the conditions listed in the conditions array to be met before it will be triggered. The color is the color that the key will change when the conditions are met, and the key is which key will change color.

Currently, the value of `key` can either be a number which corresponds to the correct Corsair KeyCode, or a charcater such as `"w"`, and the plugin will attempt to find the correct key by the character.

A key entry will look similar to this:

```
{
  "conditions": [
    "gearHandleDown",
    "gearOneDown"
  ],
  "key": 93,
  "color": "green"
}
```
# Finally
This is a plugin which I will enjoy adding improvements to and I hope the flight simulation community can enjoy.

Feel free to checkout this repository on GitHub.
