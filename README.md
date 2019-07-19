# A game with 1 pixel

The goal of this post is to answer a comment that I get quite frequently when I show my game: *Nice graphics, how did you did it ?*

I will focus on my less common use of particles: to make game objects. I won't go into details about the particles that I use for explosions

Before we dive in, a word about why I did it this way: I not good at drawing, or modeling, or sculpting.. But I can code, and I like to code. 

So I've done everything trough code. Here is how:

# Smart particles

We will start with a simple example, the paddle:

**Paddle screenshot**

My paddle is composed the way I do every object: with 'smart particles'. 

Each of these is a bag of data onto which the same behavior is applied. 

If I say that the game as 1 pixel, that's because each particle will draw a 1x1 white pixel and apply a tint to it's basic shader

## In practicle

In the paddle example, is a 3 by 8 grid of particles.

### Color

Each particles has an array of 7 colors and an index representing which color to pick from this array.

The way the animation here work is by changing this index each frame

That's how you would also get this "shock wave" effect when a ball hits the paddle: Sort the particles in regard to their distance of the point of impact, change the color index of the closest for one or two frames, and remove it from the list.

I have a gameplay mechanic that goes like this: When a ball hits the paddle, the paddle becomes hotter. When it's hot enough, it will shoot. So I also use the color index to make the paddle look 'hot'

### Movement

They also have other attributes such as the position they need to be, and their current offset from this position.

When I need to move them, I always tell them where I want them to go, and let them go there "on their own". 

In the case of the paddle, the further they are, the stronger they get pulled towards their destination. It makes for a snappy response, and a smooth arrival.

Once you've added this parameter, you can really make your particles come alive:

- When the paddle gets it, make the columns closer to the impact go down the most. An instant Y offset will provide instant feedback and smooth recovery. You can also add a bit of randomness spread on the lines to make it feel even more 'organic'
- When it moves, make the top react of little bit less, to give a 'jello' feeling to this 3 by 8 grid
- When the player tap the screen, make every particle move away from the center a bit. Like a small explosion, or breathing.
- Offset a single particle, sometimes, to show cracks in the structure
- Reverse to force to make it explode when the player dies
- Make the particle appear of screen and use this cool built in transition effect
- Add an angle to get varied animations
- When an object changes color, change the color array of each particle one by one to get a transition
- Have left over particles when a block dies that only light up when a ball is near 

A good example of those 'built in' transitions is the text. When a text object switch character, I will reuse as much particles of the previous char as possible and simply reassign them a new position.

# Tips and tricks

- Use patterns. Like in most cases, they will make your blobs of particles feel more real. A few examples that I use: only move in 8 directions, color based animations, no angles, same color arrays, 

# Gaussian

# Animation
