---
layout: post
title: Unity Plugin - Terrain Heatmaps
subtitle: Data visualisation using Unity
tags: [project]
---
## Terrain Heatmaps

Terrain Heatmaps is a Unity 3D plugin that allows data visualisation on Unity's default Terrain object, it works across all of Unity's supported platforms.

### Custom Data

You can use the heatmap to display any kind of data you like, for example quantity of in-game resources or real world weather data. The plugin allows the user to plugin in raw data directly into each point on the heatmap, or apply custom heatmap datum objects to their objects and use brushes with settings such as opacity, blending modes.

### Data Filtering

A heatmap supports multiple data-sets that can be filtered by using Unity’s tag system. One data set may be weather data, another topological data and so on.

### Texture Interpolation

Low resolution heatmaps can utilise either nearest-neighbour when speed is critical or bi-linear interpolation to improve their appearance.

### Realtime Updates

The heatmaps can be updated and edited in real-time, this allows the user to see the visualisation change over time and interact with it.

### Serializable

The heat-maps created by the plugin are fully serialized with Unity’s standard serilization system, meaning no data files need to be stored on the machine locally and any changes made during Unity’s ‘Play Mode’ are reverted afterwards (like default Unity objects) , everything can be stored in the usual Unity project save file.

### Custom Textures

The tool allows the use of any colour or texture for the data visualisation, this allows the tool to also be used to create landscapes by swapping out the default block colours for photo-realistic textures and normal maps.
