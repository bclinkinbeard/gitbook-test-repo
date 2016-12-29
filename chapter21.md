## Build an Area Chart

For this example we're going to be plotting stock data. We have a data.json file where we've got an array of objects where each object has a ticker property and a values array. That values array has objects in it with a close property and a date property -- the date that the stock closed at whatever price.

We've got Amazon here and we also have Google and our data runs from September 30th of 2016 to July 1st of 2016. If we come over here to our app code we can see that we've got the shell set up here. We've got a call to d3.json to load that file. Now we can go ahead and just get into the business of creating our chart from that data.

The first thing we're going to do is create a function that will parse the date strings that we have. We're dealing with four-digit year/two-digit month/two-digit day. We can create a parsing function for that using the d3.timeparse method.

Capital Y/M/D is the format that maps to the data that we have in our json file and now we have a function called parse time that we'll be able to use to parse our data. Now that we have that set up, we can iterate over our data and make sure that everything is converted to the right format that we need.

First we'll iterate over the base array and get each company object out. Then we'll iterate over each of the value objects for the company and we'll use our parse time function to parse the date and then we're just going to make sure that close is actually a number, so we'll do that here as well.

Now that our date is parsed we can go ahead and create our scales. Since we're going to be plotting the dates along the x axis we're going to create a time scale with d3.scaletime. Then for our domain we need to do a little bit of work here to dig in and get these values from the second level down.

We're going to call d3.min and then pass in the data array. But once we get each of those company objects out, we need to do an additional call to d3.min and pass in that array of values and tell it to look at the date property on each of those objects.

The second number in our domain is going to be the same exact logic, but we're going to find the max value instead of the min and so there's our domain and we'll set our range to be from zero to the width of our chart. Now that our x scale is created we can go ahead and call svg.appendg. You always want to have a fresh graphics container for your axes.

Then we'll call the attribute method to set the transform attribute and give that a call to translate to move it down by the height of our chart so that our x axis is at the bottom. Then finally we'll do .call and then pass in d3.axisbottom, and then pass in our x scale to that. We're creating a bottom-oriented x axis using our x scale and setting it at the bottom of the chart.

Now if we save this we see that we do in fact have a x axis that runs roughly from the beginning of July -- it looks like July 3rd is the first date there -- to September 25th. You can see we have a little bit of overlap, so maybe we want to add some directives here on how many tics that the scale should have.

Let's try doing, let's say, 10 tics. That's still too many. Maybe five? Not a lot of precision in our x axis, but that's OK for now. We're not really going to be worried about specific date things lining up. Now we can move onto our y scale.

Our y scale is just going to be a linear scale, so we'll just say y scale equals d3.scalelinear, and we need to do the same sort of work that we did for our x scale in order to find the minimum and maximum values.

I'm just going to grab this code from up here, paste it down here, and then this time the difference is instead of looking at the date property on these we're going to be looking at the close property. We'll just update these and the rest of that code can actually stay the same.

For our range, we're again going to set our height as the beginning value and zero as the second so that again, we can have that sort of inverted relationship so that on our chart, larger values are shown closer to the top of the page, which actually maps to smaller y values in an svg context.

With the scale created, we can again do essentially the same thing we did before, where we call svg.append. Create a fresh graphics container. This time we don't even need to translate it, since it's going to be at the top left. We'll just say .call and then we'll call d3.axis left to create a left-oriented axis and we'll pass in our y scale.

If we save that, we can see that now we have our y axis in place, which runs from a little bit less than 700 to say, maybe 850, 860, something like that. Now that we have parsed our data and pulled the values out that we need to create our axes, let's look at how we actually create our area chart shapes.

The first thing we're going to do is create what's called an area generator. To do that, we'll call d3.area and then we're going to tell it how to find the x position. That's going to use a standard callback like we have seen plenty of times before. We're just going to use our x scale and pass it the date property.

Next, and where things get a little bit different from what we've seen before, we need to set the y zero property. When you're creating areas, what you're actually doing is telling it where to put the bottom of the shape and the top of the shape. The y zero property is going to tell it where to draw that bottom of the shape.

For this we don't actually need anything from our data itself. We're just going to get the minimum value of our y scale. We're going to call our y scale, but instead of passing in a value from our data object, we're going to pass in the minimum value from our y scale by saying y scale.domain and then the first item from that array.

The y1 property is how we set the top position. For this one we're going to do another standard data callback and then we're going to pass the d.close property to our y scale. Now we have defined our area generator in this property called area, which is actually a function.

Now if we come down and do just a standard data join we'll see how to use this. We can just say svg.selectall. This time we'll use a CSS selector and call it .area, because we're going to be creating path objects, and we can't select all the paths because our axes use paths as well.

Once we've selected all of the items within area class, we will say .data, pass in our data array, and then tell it we want to work on our enter selection. For our enter selection, we want to append a path for everything in that enter selection. We can go ahead and give it that area class, just so we've got everything configured properly there.

Now we can set the d attribute. The d attribute is how path objects have their shapes and positions defined. In this case, we're going to have our regular data callback, but this time we're going to call our area generator and pass in d.values.

Remember, the values array is our array of objects with date and close properties on it, and that's what we're going to pass to our area generator. Our area generator is then going to use these callbacks that we defined here to pull those date and close properties off.

That takes care of everything that we need to define the elements. But we do need to set a couple of styles so that we can see everything.

We're going to set the stroke style first and we'll set that actually to some predefined colors that I found, which are essentially Amazon orange and Google blue, and we're just going to use the index of our lines here. The first line that gets drawn will be the Amazon line. The second will be Google. Not super-robust code there, but for these demonstration purposes it's simple and straightforward.

We're also going to set the stroke width to two just so we get a little bit thicker of a line than we normally would. We're going to set the fill style using those same colors that we used for the stroke.

Lastly we will set the fill opacity so that we can see through these shapes a little bit since they're going to be stacked on top of each other. We'll just set that to 0.5.

Now if we save this, we get our shapes. We can see our orange shape here. This is our Amazon stock price, which ends up way up here. Google's down here. But we've got our nice shapes there on top of one another.

We can go back here and add a little bit of a curve to our area generator by using the .curve property there, and then we're just going to use the d3.curve Catmull Rom property, which is just one of the types of curves that's built into d3. Then we're going to call it .alpha, pass it a 0.5. That'll just give us a nice, smooth curve between all of our data points here.

This is just a standard chart like we normally see where we're loading in some data. We are doing a little bit of data processing that we haven't always seen before. But then we're just using the data that's loaded to create our x and y scales and axes.

The area chart itself really just comes down to creating this area generator, where we tell it how to find its x position, its top y and bottom y positions, and then instead of drawing regular shapes like we've seen before, we're actually going to create path shapes and set the d attribute based on that area generator.

