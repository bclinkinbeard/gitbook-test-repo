## Convert Dates to Numeric Values with Time Scales

While mapping from one numeric value to another is pretty simple and straightforward, doing the same thing with dates and times is quite a bit more difficult in JavaScript. For example, it's not exactly easy to say what date falls exactly in the middle between today and January 1st.

Luckily for us, D3 provides a time scale. To use that, we're just going to say var timescale equals d3.scaleTime. We will again use the domain and range methods. In this case, our domain is going to be a date representing January 1st as the minimum value, and a date representing today as the maximum value.

For our range, we'll just use 0 and 100 for the sake of simplicity. Now we have a time scale that will map dates that fall between January 1st and right now to values between 0 and 100. Let's see what happens if we pass in a date with May 15th as the date.

Now, that returns 61 with some decimals. It sounds like we need to go back a little bit. Maybe, it's April 15th. We're getting pretty close there. Now, just so we can see a couple more examples, if we were to pass in January 15th, that's going to equal about six.

If we were to pass in now again, that's actually going to return just slightly over 100, which is basically because between the time we created the domain here, and got the value for this date here, a little bit of time passed.

Maybe just a few milliseconds in that execution period, but it is a difference, so it's beyond that maximum value of 100. Now, if we really wanted to find the middle point value, we could actually use another feature of scales in D3. That is the invert method.

If we say time scale.invert(50), it's then going to tell us that actually, April 20th, precisely at 7:19 AM and 48 seconds, that is the midpoint between when this code ran, and January 1st. Now if we run this again, you'll see that the time stamp will actually change because it's recomputing that value between right now.

You can see this makes working with dates a whole lot easier, whether you're going from date to output value, or in the reverse, finding what date corresponds to a specific point on your output range.

