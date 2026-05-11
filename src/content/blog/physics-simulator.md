---
title: 'Building a Gravity Physics Simulator in Java'
description: 'How I built a 2D physics simulator with gravity, wall collisions, and bouncing bodies using Java and JavaFX.'
pubDate: '2026-05-10'
heroImage: '../../assets/blog-placeholder-2.jpg'
---

I built a 2D gravity physics simulator in Java using JavaFX. The idea was simple: simulate bodies falling under gravity, bouncing off walls, and eventually colliding with each other.

## How It Works

Each object in the simulation is represented by a `Body` class that tracks its position, velocity, size, mass, and color.

```java
public Body(double x, double y, double vx, double vy, double diameter, double density, Color color) {
    this.x = x;
    this.y = y;
    this.vx = vx;
    this.vy = vy;
    this.diameter = diameter;
    this.mass = diameter * diameter * density;
    this.color = color;
}
```

Mass is calculated from the diameter squared times density, so bigger bodies are heavier.

## Physics Update Loop

Every frame, gravity is added to the vertical velocity and the position is updated:

```java
public void update(double grav) {
    vy += grav;
    x += vx;
    y += vy;
}
```

## Wall Collisions

When a body hits a wall it bounces back with some energy loss — 80% velocity on the axis it hit, and a little friction on the ground:

```java
public void handleWalls(double width, double height, double wall_length) {
    if (y > height - diameter / 2.0 - wall_length) {
        y = height - diameter / 2.0 - wall_length;
        vy = vy * -.8;
        vx *= .9;
    }
    if (x > width - diameter / 2.0 - wall_length) {
        x = width - diameter / 2.0 - wall_length;
        vx *= -.8;
    } else if (x < diameter / 2.0 + wall_length) {
        x = diameter / 2.0 + wall_length;
        vx *= -.8;
    }
}
```

## What's Next

Body-to-body collision detection is partially stubbed out — that's the next thing I want to implement. Once that's done I want to experiment with different gravity values and see how the simulation behaves.

Check out the full code on [GitHub](https://github.com/PixlZach/Physics_simulator).
