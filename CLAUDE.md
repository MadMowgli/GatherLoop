# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

GatherLoop is a Lua add-on for WoW Forever. It takes GatherLite's known spawn points for the resources the player picks, groups them into clusters, and draws the clusters plus one closed farming loop on the world map.

## Current state

`GatherLoop.toc` targets `## Interface: 16001`, declares the saved variable `GatherLoopDB`, and loads `Core.lua`, which has not been written yet. There is no build script, linter config or test suite. Update this file once any of those exist.

## Running

WoW add-ons have no build step. The client loads the folder from `<WoW install>/Interface/AddOns/GatherLoop/`, and the `.toc` file must be named `GatherLoop.toc` to match the folder. The client loads only the Lua files listed in the `.toc`, in that order, so add new files there. After editing files, run `/reload` in game to load the changes.

## Intended architecture

The README describes a four-stage pipeline:

1. **Input**: read spawn points from GatherLite's node database, filtered to the resources the player selected. GatherLite is a separate add-on, declared as a hard dependency in the `.toc`. GatherLoop relies on the shape of GatherLite's data, which it does not control.
2. **Clustering**: group nearby spawn points into clusters.
3. **Routing**: compute one closed loop through the clusters.
4. **Rendering**: draw the clusters and the loop on the world map.
