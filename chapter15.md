## Margin Convention

Most charts use axes to label and provide context to the data that they're displaying, and while D3 provides APIs for creating these axes, it relies on a simple convention to make room for these axes. In this lesson, we'll take a look at the margin convention, which is used widely within the D3 community.

I've simplified our example here, so we just have the chart style, and I've updated the sizing so that it fits in this window perfectly without any scaling. There are no items within the chart div to begin with, and our JavaScript file has been completely cleared out.

To keep things as simple as possible, we're going to fill this space with one single rec. The first thing we'll do is create a root svg element. We'll give it dimensions that match the size of our container div, and then we'll create a rectangle with the same dimensions as well. We'll give our rectangle a simple fill and stroke, so that we can see exactly where it lies.

Now we have an svg element that fills the space of our div and a rectangle that fill the space of the svg. Now we can go ahead and create our margins.

In the D3 margin convention, you create an object named Margin and give it properties of Top, Right, Bottom, and Left. We'll set everything to zero to begin with so that we can see the effects as we update things.

Next, we're going to create variables to hold our width and our height. Our width variable will hold the value of our original width minus the horizontal properties of our margin object, so Margin Left and Margin Right.

Similarly, our height will be our original height minus the top and bottom properties of our margin object. We'll then adjust the values that we apply to the svg tag by using the width and height variables, but adding back in the margins that we removed previously.

This means that the svg elements, width and height attributes, will match the numbers that we provided above before the margin properties are subtracted. In order to use these margins, however, we need to create a new element that will house the rest of our visualization. We're going to append a graphics container by calling Append G, and then we'll move that container according to the properties defined in our margin.

To do this, we'll set the Transform attribute of our graphics container. We're going to use an ES6 template string and call the Translate method, passing in the Margin Left and Margin Top properties.

Next, we can update our code that actually populates the chart, and set the width and height of our rectangle element to the width and height variables that we have calculated above. Our chart doesn't look any different yet, and that's because all of our margin properties are set to zero.

Let's go ahead and change that, and set the bottom and left margin properties to 25. Now we can see our rectangle is, in fact, moved over and up by 25 pixels. To understand what's going on here, the width variable is actually going to be holding 400 as its value, because we've set it to 425 and then subtracted the left and right properties, where the left is 25 right now, and the right is zero.

Similarly, height is going to hold a value of 600, because we've started with 625 and subtracted the 25 from our bottom margin.

When we create the root svg tag, we add those margin properties back in so that they hold the values of those numbers at the beginning. If we go inspect our page, we can see that our width and height properties are, in fact, set to 425 and 625.

Where the benefit comes in is that everything after this initial element creation can simply use the width and height properties and ignore all of the margins completely. To show that this is flexible and works for multiple elements, we'll go ahead and copy our rectangle and create another one, and we'll set each of them to be half the width.

We'll move the second one over, and now we can see that we have two rectangles side by side, both respecting the margins. If we were to add in a top and a right margin, you can see that those values are still respected as well.

To recap, we created our margin object with Top, Right, Bottom, and Left properties. We then created width and height variables that take those margin properties into account. We constructed our svg element and set its width and height to the full numeric values by adding the margin properties back in.

We then created a graphics container and moved it according to the left and top margins, so that all graphics created after that were already starting from the proper point.

One thing to note here is that this svg variable is actually going to be holding the selection that corresponds to this graphic element, so while not a technically accurate variable name, it does provide us with a simplified reference for the rest of our code.

Once everything's created and configured properly, we can go ahead and add shapes to our chart as normal, concerning ourselves only with the width and height variables and ignoring margins entirely.

