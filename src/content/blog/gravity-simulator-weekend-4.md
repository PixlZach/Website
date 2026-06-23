---
title: 'Gravity Simulator - Weekend 4'
description: 'Added multiple bodies with different sizes and velocities, and started working on body-to-body collision detection.'
pubDate: '2026-05-31'
heroImage: '../../assets/blog-placeholder-3.jpg'
---

This weekend I kept working on the gravity simulator. The main things I added were support for multiple balls at once with different properties, and I started laying the groundwork for collision detection between bodies.

## Multiple Bodies

Before, the simulator only had one ball. Now you can spawn multiple bodies at the same time, each with their own starting position, velocity, size, color, and density. Bigger bodies have more mass — mass is calculated as diameter squared times density, so a ball twice as wide is four times heavier.

Right now the sim starts with two balls: a larger aqua one moving slowly to the right, and a smaller blue one with more speed and a downward angle. They both fall under gravity and bounce off the walls independently.

## Starting Collision Detection

I added a `handleCollisions` method to the `Body` class that loops through all the other bodies and checks if the current one should interact with them. Right now the loop is there but the actual collision response logic is still empty — that's the next step.

Getting two balls to bounce off each other correctly is a lot more math than just bouncing off a wall. Wall collisions are simple because the wall doesn't move. Body-to-body collisions need to account for the angle they hit at, the mass of both objects, and how momentum transfers between them.

## What's Next

Filling in that collision logic is the main goal for next weekend. Once that's working I want to try adding more bodies and see how the simulation holds up with a bunch of them bouncing around at once.

Check out the full code on [GitHub](https://github.com/PixlZach/Physics_simulator).
