# When to use BEM and When not to use BEM

First things first! We have to ask the question, do I need BEM? Well, do you? The answer should always depend on what you're styling.

## There is no Repeatable Design Pattern

```html
<header class="header">
	<img class="header__logo" src="logo.svg" />
	<h1 class="header__title">Title of the website</h1>
</header>
```

Given the HTML above, we're styling a header that contains an image and a title. Okay, now we're looking at our comp, right? We only see one header in the whole comp. There's no other pattern in the comp that looks close to this header.

While BEM helps us clearly spell out how our header module would look, it's also a lot of extra typing that we're doing while fully knowing this section is unique.

The CSS looks like this.

```css
.header {
}

.header__logo {
}

.header__title {
}
```

This is fine, but if we wanted to simplify our code, we could. Instead of BEM, we can reduce it to this.

```css
.header {
}

.header > img {
}

.header > h1 {
}
```

Thus, our HTML would be simplified too.

```html
<header class="header">
	<img src="logo.svg" />
	<h1>Title of the Website</h1>
</header>
```

Sure, it's not BEM anymore but it still clearly communicates what it's doing. We're still thinking about this header as a module but we're also simplifying our code so that's smaller and easier to read and CSS by itself can help us convey this.

Our goal should always be clear communication so that the next guy can read our code and understand what is going on.

## There are too Many of the Same Elements

On the other hand, maybe you have to follow a design pattern for a bullet-list. Imagine this piece of HTML.

```html
<ul>
	<li>Item</li>
	<li>Item</li>
	<li>Item</li>
	<li>Item</li>
	<li>Item</li>
	<li>Item</li>
	<li>Item</li>
	<li>Item</li>
	<li>Item</li>
	<li>Item</li>
</ul>
```

```css
ul {
}

li {
}
```

We can't make every bullet-list look the same. There's some that need to follow a different design pattern.

Now, let's say we apply BEM on this bullet-list to solve this design pattern.

```css
.list {
}

.list__item {
}
```

That looks splendid! Now, let's see how we apply these classes to our HTML.

```html
<ul class="list">
	<li class="list__item">Item</li>
	<li class="list__item">Item</li>
	<li class="list__item">Item</li>
	<li class="list__item">Item</li>
	<li class="list__item">Item</li>
	<li class="list__item">Item</li>
	<li class="list__item">Item</li>
	<li class="list__item">Item</li>
	<li class="list__item">Item</li>
	<li class="list__item">Item</li>
</ul>
```

Oh man, the HTML is now fat and looks like a copy pasta mess. It sure did look a lot cleaner before.

If we think about **D.R.Y.** _Don't Repeat Yourself_ as a principle, we are totally repeating ourselves while knowing just how silly this code looks.

We can do better while still turning this into a design pattern.

```css
.list {
}

.list > li {
}
```

We can take advantage of using a single class name in this case since we know what we're styling is a bullet-list and we know that the `<ul>` and `<li>` have a semantic relationship.

Instead of BEM, we're relying on simple CSS selectors and basic HTML semantics to define exactly what our module does. The simpler our HTML & CSS is, the easier it is for our peers to understand it.

## Using BEM as the Next Guy

Let's say I'm the next guy that works on your project and I look through your CSS code. I have to make some edits to the header and I'll need to borrow a few elements for a second header.

As the next guy, I should be able to:

1. Maintain your code
2. Improve your code
3. Extend your code with my own code

First, I have a look at the CSS.

```css
.header {
}

.header > img {
}

.header > h1 {
}
```

Next, I have a look at the HTML.

```html
<header class="header">
	<img src="logo.svg" />
	<h1>Title of the Website</h1>
</header>
```

Now, I have to change the HTML in order to build out my edit. This edit requires me to make the logo and title side-by-side.

```html
<header class="header">
	<div>
		<img src="logo.svg" />
	</div>
	<div>
		<h1>Title of the Website</h1>
	</div>
</header>
```

By adding these divs, I've broken the current CSS styling and now I will have to fix the CSS. I could update it so it would look like this.

```css
.header {
}

.header img {
}

.header h1 {
}
```

While this fixes the styling on my main header, I need to remember that I'll be styling a second header and that second header is not going to be using an h1 element. It's going to be using an h2 element, so I need to figure out how to support it.

I could get fancy and chain another CSS selector like this.

```css
.header h1,
.header h2 {
}
```

Sure, okay. This could work for now but it is starting to look more complicated already. If I need to apply the same styling to another element that isn't an h1 or h2, then I'll have to chain that selector to the stack and it'll be even harder to maintain.

The fact that I had to chain this selector once should be enough to tell me that I've just repeated myself. I have violated the DRY principle.

Instead of chaining, I could create a new class and use BEM to clarify this class is related to the header.

```css
.header__title {
}
```

In this case, replacing the chained selector with a single class name can solve the same problem and even better, it's simplified, it's agnostic to which HTML element is in the module and it clearly communicates that it's a child of the `.header` module.

```html
<header class="header">
	<div class="header__item">
		<img class="header__logo" src="logo.svg" />
	</div>
	<div class="header__item">
		<h1 class="header__title">Title of the Website</h1>
	</div>
</header>
```

```css
.header {
	display: flex;
	flex-wrap: wrap;
}

.header__item {
	flex: 1 1;
}

.header__logo {
	display: block;
}

.header__title {
	font-size: 2em;
}
```

Let's review the list of things that I should be able to do, as the next guy.

-   [x] Was I able to maintain your code?
    -   I could read and understand what your code was doing
-   [x] Was I able to improve your code?
    -   I replaced two selectors with class names and followed BEM to define their relationship
-   [x] Was I able to extend your code with my own code?
    -   I introduced a new class name into the module

```html
<header class="header header--post">
	<div class="header__item">
		<img class="header__logo" src="thumbnail.svg" />
	</div>
	<div class="header__item">
		<h2 class="header__title">Title of the Post</h2>
	</div>
</header>

<header class="header header--mini">
	<div class="header__item">
		<img class="header__logo" src="thumbnail.svg" />
	</div>
	<div class="header__item">
		<h3 class="header__title">Title of the Mini Section</h3>
	</div>
</header>
```

```css
.header--post {
}

.header--mini {
}
```

Check it out. I'm able to reuse all of the styling that is defined in the `.header` module for 3 different headers and I'm using the modifiers `.header--post` and `.header--mini` to create variance.

## The Next Guy After Me

After I finish this project and move on, I can feel confident that the next guy can read my code.

Given him understanding basic HTML & CSS and understanding how to read and write in the BEM format, the next guy should be able to maintain my code, improve my code and extend my code with his own code, just as I was able to do with you.

Think about it. When code is complex or cryptic, it's hard for peers to understand it. If the next guy doesn't understand it, he won't maintain it. He will write it from scratch again and add it to the bottom of the code, and when he's done, the next guy after him will go through the same thing again. The code is untouchable and the maintainence cycle grows with more burden.

When the code is simple and clear, it's easier for peers to understand it. The next guy can touch the code and make it better. The maintainence cycle grows with more certainty.
