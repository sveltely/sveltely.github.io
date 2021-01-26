# 🖥🔥

## Getting started with Svelte

Leona - Chows - Braden

+++

### What we will talk about

1. Components (Braden)

2. Reactivity (Leona)

3. Template Logic (Chows)

4. Demo + Questions

---

## Components

+++

### Project Template

```shell
npx degit sveltejs/template your-project-name
```

Notes: You can get a project template by running this command. It's similar to
what `create-react-app` does for you.

+++

### Single File Components

```html
<!-- Counter.svelte -->

<script>
  let count = 51;
</script>

<style>
  p {
    color: deepseagreen;
  }
</style>

<h1>Counter</h1>
<p>{count}</p>
```

Notes:

You can keep your JavaScript, styles and markup relating to a component all in
the same file. Styles a scoped to the component so you don't have to write crazy
class names to target an element on the page. 

---

# Demo

https://sveltely.github.io/todo
