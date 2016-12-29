## Better Code Organization with selection.call()

D3's declarative API lends itself to large blocks of chained method calls like we see here.

While there's nothing inherently wrong with that, it can become a little bit unreadable at times, and sometimes you end up locking code inside of these long chains when it would be better served to be moved out into a function so that it can be reused elsewhere.

Let's look how to do that with our mouse over and mouse out handlers and move that code into some external functions.

First we'll do this for the code that scales our active bars horizontally. This is done using the call method of D3 selections, which allow you to pass a selection to a function.

The first thing we'll do is write a function that will handle this horizontal scaling of our active bars. We'll come up here and we'll write a new function called scale bar.

Any function that's called by selection.call is going to receive the selection as the first argument and then any optional arguments that were passed to it.

The first argument here is going to be called selection, and since we know that we're going to be scaling things, we'll call our second argument scale. Since this is the code that we're trying to recreate, we'll copy this here, and we'll just say selection.style transform scale X, and then make our value here dynamic.

This code says, take any selection that gets passed in here, set its transform style, call scale X, and use that scale that's passed in.

Now we need to update our code here, so that instead of setting the style directly we're going to say .call, and we'll call scale bar, and we'll pass it the scale of two.

Now that we have that set up here, let's do the same thing in our mouse out handler, but we obviously want to set the scale back to one there. We can save that and come over here and see that our code does still work.

Since we've externalized the specifics of this scale, we can then easily change this. Maybe we only want to scale it out one-and-a-half times. There we see we do in fact have that.

Not only have we made this more dynamic, but we've also made it more maintainable, in that we have this scale bar function, that we could pass any selection to this and it would transform the scale of it. In fact, if we put this same code at the end of our selection of the elements that are not hovered, we could give them their own scaling as well.

Let's make sure that the active item is scaled more than the non-active. Then, if we go over here now, we can see that everything does get scaled out when you start hovering, but the active item is bigger. That's not exactly useful, but it demonstrates the concept.

Now let's go ahead and convert this opacity styling to a separate function that can be called from selection.call as well. This time we'll call it fade, and again, selection's going to be our first argument and opacity will be the second.

Then we're just going to call style on the passed in selection and set its fill opacity to whatever value is passed in for opacity.

We'll update our code here to use the call method and specify that we want to call fade with an argument of 0.5 for the opacity parameter. We'll do the same thing in our mouse out, but with an opacity of one. Now we can see we're back to our working example, but our code has been moved out of our long chain and into these nice readable functions.

Another benefit to using call, in addition to the reusability and readability aspect, is that it makes things chainable because it also returns the selection that it's called on.

To demonstrate that, we'll create another function here called set fill, and this time it's going to be used to set the fill style, so we'll provide a color parameter. Now we can come down here and take our code that is currently scaling the active item, and add a call to set fill. We'll pass in teal, and we'll do the same thing for the mouse out where we set it back to light green.

Now we have this code that is passing this selection to two different functions, and we can see that we still get the expected behavior. The contrast on that isn't great, so let's change from teal to orange, and there we go. You can see how it's very easy to update the behavior simply by changing a parameter.

Now we have three lines here that are very readable and simple, that select and item or items and then pass that selection to multiple functions that will update those selections accordingly.

