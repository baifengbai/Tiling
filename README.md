## Tiling

Quickly construct tilings of regular polygons using a simple API.

Scroll down for a tutorial. Here are some examples.

![Sample](http://i.imgur.com/VgkrtDb.gif)

### How To

Before creating a new pattern, set these flags to make it easier.

    SCALE = 128
    SHOW_LABELS = True

The first step is to create a Model that will hold our polygons.

    model = Model()

Next, we will place our first polygon at the origin. We need only specify its
number of sides. Let's add a hexagon.

    model.append(Shape(6))

At this point we can run the following code to render the model.

    model.render(dc)

![Image](http://i.imgur.com/BF9AZDw.png)

Now, let's add squares adjacent to all of the hexagon's edges.

    a = model.add_all([0], range(6), 4)

The first parameter, [0], specifies which shapes we're attaching to. Here,
we're only attaching to one shape and it was the first one created, so it's
referred to by a zero.

The second parameter, range(6), specifies the edges we're attaching to. In this
case we want to attach to all six sides of the hexagon.

The third parameter, 4, specifies the number of sides for the new shapes. In
this case, squares.

The return value tracks the identifiers of the newly created squares so we can
refer to them later.

![Image](http://i.imgur.com/DwFKcL7.png)

Next comes the cool part. We can attach triangles to all of the squares we just
created by using the previous return value. Here, we are adding triangles to
edge number 1 of each of those squares.

    b = model.add_all(a, [1], 3)

![Image](http://i.imgur.com/lkgFqrN.png)

Now we'll add more hexagons which will represent the repeating positions of
our template.

    c = model.add_all(a, [2], 6)

![Image](http://i.imgur.com/8mHYBoo.png)

Now that we have positions for repeating the pattern, we can use the
recursive_render function to automatically fill in the rest of the surface
with our pattern.

    model.recursive_render(dc, c)

![Image](http://i.imgur.com/vh2oQKB.png)

Here's all the code needed for this pattern:

    model = Model()
    model.append(Shape(6, fill=RED))
    a = model.add_all([0], range(6), 4)
    b = model.add_all(a, [1], 3)
    c = model.add_all(a, [2], 6, fill=RED)
    model.recursive_render(dc, c)

Once finished, you can turn off the helper labels and adjust the scale as
desired.

![Image](http://i.imgur.com/RETztFc.png)
