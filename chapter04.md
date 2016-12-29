## Create Labels from Numeric Data with Quantize Scales

When we looked at linear scales, we saw an example of what's referred to as a continuous scale. What that means is that any value in this domain is going to be mapped to the corresponding value in this output range.

There's a continuous spectrum of values that could be used. We see 50 gets mapped to 300 here, but we could change this to any value we want, like 22, and in response, we get 132. It's just going to do that basic mapping.

What if you want to map your input to a specific set of output values? That's when the quantized scale comes into use. If we change this to say d3.scale.quantize, and then we'll update our variable name here, and then run this with 22 we get zero, which is a little bit confusing at first.

We can explain. What a quantized scale does is it looks at the cardinality of the output range, or the number of items in the output range. It breaks the domain into that many uniformly-sized pieces. If our domain here is zero to 100 and we have two elements in our output range, we're going to break that scale into two equal pieces.

Zero to 50, 50 to 100. 22 obviously, falls on the bottom half of that range, so it's going to be mapped to zero. An easier way to think about this, and something that it does tend to get used for sometimes, is mapping to colors.

Maybe we want to map anything that falls below 50 to red, anything above 50 to green. If we do that, we can see that 22 does, in fact, map to red. We can add a couple more values in here just to show how things work.

We'll actually put 50 in there, so we can see how that works. We'll do 88 and 99. You can see 50 actually gets mapped to green, and 88 and 99 do as well. Again, anything on that top half is going to be the second value. Anything on the bottom half is going to be the first value.

Now, where this gets a little more interesting is what if we have more than two values in our output range? If we change that to white, we're now going to see that 50 actually gets mapped to white. That's because we now have three values.

Our zero to 100 range is going to get broken into three pieces, zero to 33, 33 to 66, and on and on. Now, if we just get rid of this, I want to show one more thing that is unique to quantized scales, or at least different from the linear scales that we looked at before.

That is, instead of calling invert, we actually have a method called invertExtent. What we can do with invertExtent is similar to what we saw with invert, where we pass in a value from the output range, and it then maps back to what numbers in that domain are the boundaries for that value.

You can see here that white is going to map to any value between 33.3 repeating and 66.6 repeating. These kinds of scales can come in very handy for when you need to map all of your input data to a specific set of output values.

