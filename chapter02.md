## Convert Input Data to Output Values with Linear Scales

One of the most fundamental tasks of data visualization is mapping from abstract data values to a visual representation. What we mean by that is taking something like a test score and converting it into something visual, like a column height, or a color, or an opacity.

The simplest and most straightforward way to do that in D3 is by using a linear scale, which we can do simply by calling d3.scale.linear. A linear scale is a type of continuous scale, which is a scale that takes a continuous input domain and maps it to a continuous output range, while maintaining proportions.

That's admittedly not entirely clear, so let's look at an example. Since we used the example of test scores, we'll set up a domain of zero to 100, representing the range of possible values of scores. We represent this with a two-item array, with zero being the first number, and 100 being the second.

Next, we need to set up the output range, which we'll initially set to just zero and one. This will allow us to essentially normalize any values that get passed into the scale, so that they fall somewhere between zero and one.

We can see how this works by passing in an example value and logging out the result. We'll start by passing in a zero, which is obviously a very bad test score. We can see that it gets output as zero. We've passed in the minimum value from our domain, and the output is the minimum value from our output range.

If we were to pass in 100, our maximum value in our domain, we get back one, the maximum value in our output range. To make things complete, we'll also pass in 50, which is obviously the halfway point of our input domain.

You can see we do, in fact, get back 0.5. Everything is proportionally mapped from our input domain to our output range. If we were using this scale to map to something like a column width, our range would be zero to whatever our maximum column width is.

Let's say maybe it's 600. That's the width of our chart. If we change our output range here and save this, we can now see that the same input values get mapped to zero, 300, and 600, which is what we would expect, given a full range of zero to 600 as our possibilities.

The maximum value in our domain gets mapped to the maximum value in our output range again, and the same thing with the midpoint value. Now, what if somebody got extra credit on their test, so instead of 100, they got 105?

If we log that out, we can see that that actually maps to 630, which if our chart is only 600 pixels wide, using that value is going to cause a problem. Sometimes, we'll need to use the clamp method of the scale.

If we set clamp to true and then rerun our example, you can see that 105 still gets mapped to 600, because we've clamped the maximum output of the scale. Clamping also works for the minimum. If somehow, somebody got a -20 on the test, we're still just going to show a bar that has no width rather than a negative width, which obviously is impossible.

The last thing to show is that you can go in reverse. While we've been providing values from our domain and mapping them to our range, we can go in the opposite direction by using the invert method. If we say linearscale.invert and pass in 300, that'll get mapped back to 50 from our input domain.

