---
layout: post
title:  "PyGame: Guess Two Cards pt1"
categories: dev
tags: [dev, pygame]
---

By starting reviewing endless possibilities of programming languages and engines, I'd like to start by stepping in a field I'm familiar with. I have some experience with C++, Java, JavaScript and PHP. There is a lot of game engines for first three langs. But Python is my most recent and I like it a lot. So why not to try do something with it? I can use [tkinter](https://docs.python.org/3/library/tkinter.html) to start making something with GUI or [PyGame](https://www.pygame.org/news) thats meant for building games, but it's 21 year old already. And I'm ok with that for now.

## What are we making?
As for project number one, I've picked something that should be simple to make (but for now I've no idea how to do it in PyGame).

It will be 4x4 grid of 16 cards, where all cards are mixed and you have to pic two.

![Guess Cards Sketch](/assets/20211109_guess-two-cards-pygame.png)

What I want to achieve by this? Well – creating new project, showing graphics on screen and mouse interactions are my main goal for now.

## What do we have?
As PyGame is quiet mature game engine, it has well writen documentation and a lot of tutorials (but a lot of them are non-existent by this time). So let's take a look at [PyGame modules](https://www.pygame.org/docs/tut/PygameIntro.html) :

|Module|Description|
|:--|:--|
|cdrom|playback (**Oh no, I don't have one** 😅)|
|cursors|load cursor images, includes standard cursors|
|display|control the display window or screen|
|draw|draw simple shapes onto a Surface|
|event|manage events and the event queue|
|font|create and render TrueType fonts|
|image|save and load images|
|joystick|manage joystick devices|
|key|manage the keyboard|
|mouse|manage the mouse|
|sndarray|manipulate sounds with numpy|
|surfarray|manipulate images with numpy|
|time|control timing|
|transform|scale, rotate, and flip images|

It looks like it won't be too hard to finish this little project. So, let's do it!

I'd start with basic shapes, and won't use **image** module for now. As I see it, I will need **display** module to create screen, then **draw** module, to add card objects. Card should flip on mouse click, so **mouse** or **event** module will help me here.

I don't care about animation right now, but if everything will go smooth, then probably **transform** will help me with card reveal animation. Also, maybe, **time** will be needed to achieve this.

## Small steps
As in any program, let's break down all this in small steps. As tiny as possible.

1. Create display. I could write all gaming logic before it, but then this won't be *playable* as intended. It would be very easy for CLI, but I want to learn GUI.
2. Draw any shape. It should be any solid color filled shape (rectangle pref).
3. Draw 4 shapes in a row.
4. Draw 4 x 4 grid of shapes.

This should be enough for day one. If I can do this, then I will be able to create objects and represent them as shapes on display, that will be back-end and I will do it later.

## Steps 1 and 2
Creating display is easy, you need to import `pygame` module and create surface with `pygame.display.set_mode(width, height)` command.

Adding rectangle shape was not hard also. It's `pygame.draw.rect(surface, color, pygame.Rect(x,y,width,height))`, adding it to game loop and with `pygame.display.flip()` refresh the screen.

Result:
![PyGame 1](/assets/20211109_pygame1.png)

Code:
```python
import pygame

pygame.init()

size = width, height = 640, 480
color = 125, 125, 125
coordinates = 50, 50, 80, 80

screen = pygame.display.set_mode(size)

while 1:
    for event in pygame.event.get():
        if event.type == pygame.QUIT: sys.exit()

    pygame.draw.rect(screen, color, pygame.Rect(coordinates))
    pygame.display.flip()
```

Documentation says that `Rect` has *border_radius* parameter. Let's make card to look more like playing card:

Result:
![PyGame 2](/assets/20211109_pygame2.png)

Code:
```python
import pygame, sys

pygame.init()

size = width, height = 640, 480
color = 125, 125, 125
coordinates = 50, 50, 80, 120

# Creating graphical window
screen = pygame.display.set_mode(size)




# Main loop
while 1:
    for event in pygame.event.get():
        if event.type == pygame.QUIT: sys.exit()

    pygame.draw.rect(screen, color, pygame.Rect(coordinates), border_radius=10)
    pygame.display.flip()
```

Ok, now I need to add 4 of these in a row. At first I thought that Rect asks for `x0, y0, x1, y1` coordinates. But after few tries to calculate object width and location I found out that it contains left upper corner `x, y` and `width, height` accordingly.

Result:
![PyGame 3](/assets/20211109_pygame3.png)

Code:
```python
import pygame, sys

pygame.init()

size = width, height = 640, 480
color1 = 125, 255, 125
color2 = 125, 125, 255

card_width = 60
card_height = 90
card_border_radius = 10

# Creating graphical window
screen = pygame.display.set_mode(size)

# Main loop
while 1:
    for event in pygame.event.get():
        if event.type == pygame.QUIT: sys.exit()

    pygame.draw.rect(screen, color1, pygame.Rect(100, 100, card_width, card_height), border_radius=10)
    pygame.draw.rect(screen, color2, pygame.Rect(150, 150, card_width, card_height), border_radius=10)
    pygame.display.flip()
```

Now with this short loop we can create 4 cards in a row:

```python
for x in range(4):
        space = (width - (card_width * 4)) / 5
        step_x = space + (card_width + space) * x
        pygame.draw.rect(screen, color1, pygame.Rect(step_x, 30, card_width, card_height), border_radius=10)
```

I added spacing calculation, so card are spaced evenly horizontally. Now I can replace hard coded values to variable `cards_in_a_row`.

`cards_in_a_row = 4`:
![PyGame 4](/assets/20211109_pygame4.png)

`cards_in_a_row = 7`:
![PyGame 5](/assets/20211109_pygame5.png)

And last thing for today, adding multiple rows!

Code:
```python
    for y in range(cards_in_a_col):
        v_space = (height - (card_height * cards_in_a_col)) / (cards_in_a_col + 1)
        step_y = v_space + (card_height + v_space) * y
        for x in range(cards_in_a_row):
            space = (width - (card_width * cards_in_a_row)) / (cards_in_a_row + 1)
            step_x = space + (card_width + space) * x
            pygame.draw.rect(screen, get_color(), pygame.Rect(step_x, step_y, card_width, card_height), border_radius=10)
````

Result (also added random colors just for fun):
![PyGame 6](/assets/20211109_pygame6.png)

That's it for today. This is very dirty ugly code, but for beginning I'm proud of myself. I could clean it up, but I want to do something more interesting tomorrow – mouse input.

Full today's code:

```python
import pygame, sys, random

pygame.init()

size = width, height = 640, 480
color1 = 125, 255, 125
color2 = 125, 125, 255

card_width = 60
card_height = 90
card_border_radius = 10

cards_in_a_col = 4
cards_in_a_row = 7

# Returns random colors every call, just for fun
def get_color():
    return random.randint(0,255), random.randint(0,255), random.randint(0,255)

screen = pygame.display.set_mode(size)

# Main loop
while 1:
    for event in pygame.event.get():
        if event.type == pygame.QUIT: sys.exit()

    for y in range(cards_in_a_col):
        v_space = (height - (card_height * cards_in_a_col)) / (cards_in_a_col + 1)
        step_y = v_space + (card_height + v_space) * y
        for x in range(cards_in_a_row):
            space = (width - (card_width * cards_in_a_row)) / (cards_in_a_row + 1)
            step_x = space + (card_width + space) * x
            pygame.draw.rect(screen, get_color(), pygame.Rect(step_x, step_y, card_width, card_height), border_radius=10)

    pygame.display.flip()
```
