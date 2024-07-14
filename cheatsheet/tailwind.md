---
label: Tailwind
---

### container
Changes size based on browser.
```
tailwind.config.js

theme: {
	container: {
		center: true,
		padding: "2rem",
	}
}
```

### size
`size-48` gives height of 48 and width 48

### divide, gap and space
- `divide-y-8` gives border on y direction.
- `divide-red-500` changes border colour
- `gap-8` (needs flex or grid)
- `space-y-8` puts space in y direction

### line-clamp and truncate
- `line-clamp-3` Limits the number of lines of text.
- `truncate` will not be more than 1 line long.

### Gradients
- `bg-gradient-to-r from-red-500 to-blue-500`: Red to blue gradient
- `bg-gradient-to-r from-red-500 to-blue-500 via white`: Add in between colour at 50%
- `bg-gradient-to-r from-red-500 to-blue-500 via white from-20% via-70% to-90%`: Change the percentage

### ring
- `ring` `ring-red-500`: Add focus state using box-shadow without using border

### Animations
See `animate-*`

### Typography
`@tailwindcss/typography` and add `prose` class.

### References
- https://www.youtube.com/watch?v=x1RJ5Q09PqM