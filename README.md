# Lab 2: WebGL Circle Renderer

## Overview

This project focuses on optimizing the performance of WebGL applications, specifically in rendering multiple circles. It addresses common performance bottlenecks such as redundant object creation within rendering loops. The application provides controls to add and clear circles, with an FPS monitor to observe performance metrics.

## Files

* `index.js`: The main application logic. It initializes WebGL, sets up shaders, manages circle creation and rendering, and handles user interactions.
* `Circle.js`: Defines the `Circle` class, responsible for generating circle vertices, handling rendering, and managing its properties (position, color, size).
* `lib/cuon-utils.js`: A utility library for initializing shaders.
* `styles.css`: Contains CSS styles for the HTML elements.

## Setup

1.  **Dependencies:** A web browser with WebGL support.
2.  **Libraries:** The project uses `cuon-utils.js` for shader initialization.
3.  **FPS Monitoring:** The `stats.js` library is included to monitor frames per second (FPS), aiding in performance analysis.

## Code Highlights

###   `index.js`

* Imports necessary modules and assets.
* Defines vertex and fragment shaders for rendering colored points.
* Initializes the WebGL rendering context.
* Sets up HTML UI elements: a slider to control the number of circles added, "Add Shapes" and "Clear" buttons, and displays for circle count.
* Manages a global list of `Circle` objects (`g_shapesList`).
* The `addCircle()` function creates new `Circle` instances with random positions, colors, and sizes.
* The `renderAllShapes()` function clears the canvas and renders all circles in `g_shapesList`.
* The `tick()` function is the main rendering loop, which updates the FPS counter and calls `renderAllShapes()` at each frame.

###   `Circle.js`

* The `Circle` class represents a circle object with properties: `type`, `position`, `color`, `size`, and `segments`.
* The `generateVertices()` function calculates the vertices for the circle based on its position, size, and the number of segments. It creates triangles to approximate the circle.
* The `render()` function:
    * Sets the color uniform for the circle.
    * Generates vertices if they haven't been generated yet.
    * Creates a vertex buffer object (VBO) to store vertex data on the GPU (if it doesn't exist).
    * Binds the VBO and uploads the vertex data.
    * Sets up the vertex attribute pointer.
    * Draws the circle using `gl.TRIANGLES`.

## Performance Optimization

The key optimization in this project, as highlighted in the lab description, is the efficient management of buffers and vertex data. Instead of recreating buffers and vertex arrays every frame, the `Circle` class generates the vertices and creates the buffer only when necessary, reusing them for subsequent rendering. This significantly reduces the overhead and improves rendering performance, especially when dealing with a large number of objects.

## Running the Project

1.  Open the `index.html` file in a web browser.
2.  Use the slider to select the number of circles to add.
3.  Click the "Add Shapes" button to create and render the circles.
4.  Click the "Clear" button to remove all circles.
5.  Observe the FPS in the top-right corner to monitor performance.

## Lab 2 Specifics

This project was developed as part of a WebGL lab assignment focused on:

* Identifying and addressing performance bottlenecks in WebGL rendering.
* Understanding the importance of efficient buffer management.
* Implementing techniques to reduce redundant object creation.
* Using `stats.js` to monitor and analyze performance metrics.