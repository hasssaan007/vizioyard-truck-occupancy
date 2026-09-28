# VizioYard - Lane-Based Truck Occupancy Detection

> **Showcase page.** This repository is a public showcase of a **private repository**:
> it contains a description of the work only, with **no source code**.

A **monocular computer-vision system** that determines which parking lanes in a logistics yard are free and which are occupied by trucks, from a single fixed camera. No depth sensor, no stereo rig.

Built as a semester research project with Viziosense for a beverage-logistics warehouse.

## The problem

A yard camera sees trucks at wildly different scales and angles. Bounding boxes alone cannot tell you *which lane* a truck occupies, because boxes overlap lanes the vehicle does not stand in.

## The approach

1. **Lane geometry as 2D polygons.** Lanes are annotated once on an empty-yard reference image and stored as polygons, then extruded into pseudo-3D prisms for visualisation.
2. **Segmentation, not just detection.** YOLOv8 segmentation gives per-vehicle masks instead of rectangles.
3. **Ground-contact footprint reasoning.** Occupancy is decided by where a vehicle actually *touches the ground*, intersected with the lane polygons, which removes the false positives that boxes produce for tall vehicles seen at an angle.
4. **Optional manual 3D boxes** per lane, used as an override so occupied lanes can be rendered as true truck volumes.

## Annotation tooling

I also built the two interactive tools the pipeline depends on:

- **2D lane annotator** - draw lane polygons, save and load per image, append or replace by lane ID, with a 3D extrusion preview
- **3D box annotator** - lane-aligned truck volumes in 4-point, 8-point or 16-point modes, drag-to-fit editing, merge-safe saving, and a read-only viewer

## Stack

Python, OpenCV, YOLOv8 (detection and segmentation), NumPy, polygon geometry and projective reasoning, custom annotation GUIs

---

*Source code is private. This page documents the work; code can be shared on request.*
