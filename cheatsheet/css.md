---
label: CSS
---

### Resize
```
.element {
	resize: both;
}
Will work for elements which have overflow property set to visible, does not apply to inline elements.

```

### Shadow effect
```
.element:hover {
	bow-shadow: 12px 12px 12px rgba(0,0,0,0.1),
	-10px, -10px, 10px white; // can put inset for both
}
```

### min function
```
.container {
	width: 800px;
	max-width: 90%;
}

to

width: min(800px, 90%);
```

### clamp
```
.container {
	width: 50vw;
	min-width: 400px;
	max-width: 800px;
}

to 

// min, preferred, max
clamp (400px, 50vw, 800px)
```


### Glassmorphism
```
.glass {
	backdrop-filter; blur(10px);
}
```

### not() and has()
```
.button:not(:first-child) {}

// only applies to buttons that have svg as child element
.button:has(svg) {}
body:has(option[value="dark"]:checked) {
	--background: black;
	--text-color: white;
}
```

### Gradient on text
```
h1 {
	backgeound: linear-gradient(to right, red, blue);
	background-clip: text;
	color: transparent;
}
```

### Counter variables
```
:root {
	counter-reset: headings;
}
h2 {
	counter-increment: headings;
}
h2::before {
	content: counter(headings)
	background-color:
	border-radius:
	padding:
	width:
	text-align: center;
}

<h2>Auto numbering<h2>
```

### Swiper
```
<div class="wrapper">
	<div class="card">
	</div>
</div>

// wrapper and card must have same width
.wrapper {
	width: 300px;
	overflow-x: scroll;
	scroll-snap-type: x mandatory;
}
.card {
	scroll-snap-align: center;
	width: 300px;
}
```

### Animations
```
animation-duration: 3s; // how long is the duration
animation-name: spin; // assign keyframe defined below to element
animation-timing-function: ease-in-out; // speed curve of animation
animation-delay: 1s; // how long animation should wait before playing
animation-iteration-count: 1; // how many times it should play
animation-direction: normal; // play animation from first frame to last
animation-fill-mode: forwards; // when the animation should stop at
animation-play-state: running; // used to control animation state

change with js:
pauseButton.addEventListener('click', () => element.style.animationPlayState = "paused");

shortform:
animation: 3s spin ease-in-out 1s infinite alternate;

@keyframe spin {
	0%{}
	100% {
		transform: rotate(360deg);
		border-radius: 50%;
		scale: 2;
	}
}
```

### References
- https://www.youtube.com/watch?v=PL3Odw-k8W4
- https://www.youtube.com/watch?v=z2LQYsZhsFw