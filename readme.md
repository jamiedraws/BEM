<!-- Headings -->

# CSS Coding Practices

## The Next Guy's Problem

Let's imagine we're putting together a header on a webpage. What can I put inside of a header? Let's start with something simple, like a logo and a title. So, let's imagine what this could look like in html.

```html
<header>
	<img src="logo.svg" />
	<h1>Title of the website</h1>
</header>
```

Now, let's imagine what my css would look like.

```css
header {
}
header img {
}
header h1 {
}
```

Sure, I could get by with this alone. However, header elements can be used to describe other relationships besides the website itself. For instance, I could use a header element to describe the header of an article or a quote or a sidebar. Imagine these headers having a different look and feel.

The css I've written for the main header will also affect those other headers, whcih I probably don't want. This is where you'd start thinking about using css classes to solve the problem, right?

```css
.header {
}
.header-logo {
}
.header-title {
}
```

Okay, now my css is separated from my html so I can choose which headers I want my styling to apply to.

Imagine our website has two headers that look very similar to one another but are just colored differently. You're probably thinking about using the same css classes to handle most of the work, right? Okay, so say I do that. Now, they look exactly the same. So, how can I change the color for this other header?

Maybe, I just write another class that's supposed to overwrite the default styling.

```css
.header {
}
.header-logo {
}
.header-title {
}
.header-dark-theme {
}
```

My `.header-dark-theme` class can override the default styling. I know this problem I'm trying to solve and I know exactly where to put it. I've figure it out, now I'm done and I can move on.

6 months later, let's say you come along and maintain my css and you see these styles. You have to style another header similar to this but the html has been removed so you can't see how it was implemented before.

Sooooo, forget the html. Okay, maybe you can just ask me, right? Nope. I took a PTO day, I'm somewhere where internet is pretty spotty so who knows when I'll see your text. Now ask youself, where the heck do you put these classes? Where was the `.header-dark-theme` supposed to go?

If you don't know, are you likely to go and change my css? What if your changes to my code break something else? Well, you're probably going to decide it's just easier to style it from scratch, right?

Now, you've solved your problem, you're done and ready to move on buuuuut, this website still lives on. So, what about the next guy that will look at both your code and my code 6 months from now and have to maintain that?

What do you think the next guy is going to do?
