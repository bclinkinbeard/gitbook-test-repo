## Build a Column Chart

Now that we have basic elements like axes and margins in place, let's create something a little more real like a column chart. The first thing we're going to do is get rid of our placeholder rectangle here. If we save that, we've just got a nice blank chart with our axes.

In order to create a real-ish chart, we need some data. I'm going to paste in some data here. You can see it's just an array named data of simple objects that each have a score property and a subject property. Once we have our data, we're going to come down here.

We need to modify our X scale because when you're creating bar charts or column charts in D3, there's a special kind of scale that you need to use which is a band scale. We're going to call D3.scaleband to create that kind of scale.

The domain for a band scale is a little bit different. In a band scale, your domain needs to hold all of the values that are going to be plotted on that corresponding axis or all of the values that could be plotted. In our case, we want to use our subjects. We're just going to map our array of objects to an array of subject names.

We'll just say data.map. Use a nice little arrow function here, and return the subject property.

Now that we have that in place, we can come down here and do our data join. We're going to say SVG.selectall. We're going to use a rect element this time, an SVG rectangle. Then we're going to join it to our data. We're going to say our inter-selection which is again where we have data but no dom element.

Any time we come across that scenario, we want you to append a new rect shape. That's our data join. That's going to create our rectangles.

But in order to make them visible, we need to set their X, Y width and height properties. For the X property, we're just going to use our X scale and pass in our subject since that's what we want plotted along the X axis.

For the Y attribute, we're just going to use our Y scale, but of course this time, we're interested in the score property since that's our vertical element. For the width attribute, we're also going to use something unique to band scales which is this bandwidth method, which is essentially an internal calculated value that will set the width of the bands.

Lastly, we need to set our height. In this one, we're again going to use our arrow function. We forgot the arrow function here. We're just going to do that. For our height, we need to take our height and then subtract our Y scale value for the score. Our Y is just going to use the Y scale value. Our height is going to be the height minus the Y scale.

The reason we're doing it like that, if we look up here at our Y, you'll see that our range puts the height first and then zero, which inverts our scale which is what allows us to have the maximum value here at the top and the minimum value here at the bottom. Since that's the opposite of the way coordinates work in SVG, we need to flip those values.

In SVG, a Y value of zero is going to be at the top of the page here. As you go down the page, the Y value increases. We've swapped those to create an inverted scale. When we're setting the Y property, we're essentially just setting where that bar is going to start being drawn. It's going to be drawn using that property minus the height, so it goes from wherever it starts down to the bottom.

Now that everything is in place, we can save our code. We do in fact get our X axis here, but we forgot to set the fill style on our rectangles which you need in order for it to show up. We're just going to set a steel blue fill. If we save this, we can see we do have our bars here.

Things are a little bit crowded. In order to fix that, we're going to come up here and use another method that is unique to band scales at least in this context. That is we're going to set the padding. We're going to set it initially to 0.2. You'll see that gives us a nice little amount of padding.

The values that are accepted by padding run from zero to one. Zero is what we got by default. That's no padding. If we were to set 0.5, that's going to give us a padding that is equal to the band width itself. Anything above 0.5 is going to make the bands actually smaller than the gaps, which is probably not what you want. I generally go with something like 0.2, makes things nice and comfortable.

One thing to note is you can actually control the inner padding and the outer padding separately. If you were to set outer padding to say 0.5, that gives you a nice amount of space on the sides here, but you still get that narrow gap in the middle.

Lastly, there is also an align property that tells it how to distribute the whole set of items. If we were to set the...We forgot to set that back to regular padding. If we've got a padding here of 0.2 and set align to zero, it's going to have everything all the way left. If we were to change it to one, it's going to be all the way right.

Generally, you're not going to use that you just want it centered.

That's a pretty nice little column chart here. We could even go and if we want to give a style for our rect here, maybe we want to set the fill in the CSS here. Then we can create a hover style so that we get a little more interesting colors here. We'll set the fill to turquoise on hover.

If we save this and come over here, it's not going to react until we remove this hard coded fill. Save that. Come over here. Now we can rollover these, and we do in fact get that color change.

What I want to show is if we add data to our source array here, so we've added three more subjects here with their scores. If we save that, you can see that the band sizes are in fact updated, so everything still fits. Everything gets recalculated which is nice.

But our labels have started to run into each other down here which is something that'll happen when you have a lot of items. What we're going to do, we're going to give ourselves some extra room on the bottom here. If we save that, we get a nice little amount of space there.

If we come down here, this call to .call where we pass in the X axis, that's what's actually creating the SVG elements that make up our X axis. If want to effect the labels in there which are text elements, we can simply say select all text.

We're going to set a style called text anchor to end. Then we're going to set the transform attribute to -45 degrees of rotation.

If we save that, now our labels are in fact rotated. They no longer run into each other or overlap. The alignment isn't perfect. You'll need to play with that based on your styles and things, but you do at least get labels that are readable.

We've still got our response if I call in here from before in our initial creation of the SVG. We should be able to come over here and resize this, and our chart does in fact update to be scaled.

