## Vite incorrect CSS flattening

- `npm run dev` — open http://localhost:5173, the text should be red
- `npm run build` — open http://localhost:4173, the text should be red, but is black

### Issue:

Given the following CSS:
```css
.foo {
  :where(& > .bar) {
    color: red;
  }
}
```

In a production build, this is flattened as:
```css
.foo :where(>.bar){color:red}
```
This CSS is invalid because `:where(…)` doesn't accept relative selectors.

But I expect it to be flattened as this instead:
```css
:where(.foo>.bar){color:red}
```
