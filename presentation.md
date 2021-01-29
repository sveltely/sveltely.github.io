# 🖥️🔥

## Getting started with Svelte

Leona 🎙️ Chows 🎙️ Braden

+++

### What we will talk about

- 1️⃣ Folder Structure / Components (Braden)
- 2️⃣ State / Reactivity (Leona)
- 3️⃣ Template Logic (Chows)
- 4️⃣ Demo + Questions

---

## 🐿️ Braden

+++

### Local Development

```shell
npx degit sveltejs/template your-project-name

cd your-project-name

npm install

npm run dev
```

Notes: You can get a project template by running this command. It's similar to what
`create-react-app` does for you.

+++

### Components

- Single File Components

- Other Component features

+++

### Single File Components

```html
<script>
  let number = 51;
</script>

<h1>Favorite Number</h1>
<p>{number}</p>

<style>
  p {
    color: maroon;
  }
</style>
```

Notes:

You can keep your JavaScript, styles and markup relating to a component all in the same file.

+++

### Component Features

- ♻ Nested Components
- 📁 Props
- 🎯 Scoped styles

[Greeting Machine example](https://svelte.dev/repl/ec0f9c51e72947ad8da988be01d9c05d?version=3.32.0)

Notes: Usually when we were in React, if you want to pass data from parent component to child
component then you need to declare properties with `props`

But in Svelte nested components, you can indicate that a variable is allowed to be passed in by
using the `export` keyword in front of the variable declaration

Styles are scoped to the component, so you don't have to write crazy class names to target an
element on the page.

---

## 🐱 Leona

+++

### Reactivity

- Binding variables
- Reactive statements
- Events

Notes: OK, thanks a lot braden, now i'm gonna discuse about reactivity in Svelte,

+++

### Events

```svelte
<script>
  let count = 0;

  const increment = () => (count += 1);
</script>

<h1>{count}</h1>

<button on:click={increment}>Increment</button>
```

[Counter example](https://svelte.dev/repl/0031b184adc04c9da35f907efb7b0c28?version=3.32.0)

Notes:

Here we are calling the increment function when the user clicks the button. You can use
`on:(event_name)` to bind an element to any dom events.

+++

### Binding Variables

```svelte
<script>
  let name = "";

  const handleChange = (e) => {
    name = e.target.value;
  };
</script>

<h1>
  Hello {name || "??"}
</h1>

<input type="text" on:keyup={handleChange} />
```

[Text input example](https://svelte.dev/repl/373f2a9ce2c04e17abcdb2ca74773b36?version=3.32.0)

Notes: For this input element, if i wanna update the `name` variable, the only way i can do in react
is to add onChange event listener to the input, then i also have to update the state.

but in svelte, you can use the `bind: value` directive, which gives you two way data binding.

When the input changes, `name` updates, and when `name` changes , the input value will change too

+++

### Reactive Declarations

```svelte
<script>
  let count = 0;

  $: squared = count * count;

  const increment = () => (count += 1);
</script>

<h1>{count}<sup>2</sup> = {squared}</h1>

<button on:click={increment}>Increment</button>
```

[Squared Counter example](https://svelte.dev/repl/3896303961a74c338aea0bd2af629656?version=3.32.0)

Notes: With reactive declarations we don't need to listen for events to update a value which depends
on other variables.

The `$:` indicates that this line only runs when any variables on the right side of the equals are
changed.

---

## 🐶 Chows

+++

### Logic

| Type       | Block syntax          |
| ---------- | --------------------- |
| Lists      | `{#each} {/each}`     |
| Conditions | `{#if} {:else} {/if}` |
| Promises   | `{#await} {/await}`   |

+++

### List Rendering

```svelte
<script>
  let animals = [
    {photo: '🦁'},
    {photo: '🦊'},
    {photo: '🦄'},
    {photo: '🐭'},
    {photo: '🦎'},
  ];
</script>

{#each animals as animal, index (index)}
  <h1>{animal.photo}</h1>
{/each}
```

[Animals example](https://svelte.dev/repl/6c70f213b31f4f9485700cb65630ea2d?version=3.32.0)

Notes: You can iterate over a list of objects very easily in Svelte using the `each` block.

Saying `animals as animal, index` gives you access to each animal and their index inside the `each`
block.

The round parentheses at the end are for a unique key, just like the key property in React.

+++

### Conditional Rendering

```svelte
<script>
  let sleeping = ["Fred", "Prince", "Oscar"];
  let cats = [];

  const feed = () => (cats = [...cats, sleeping.pop()]);
</script>

{#if cats.length == 0}
  <h1>No cats here 😭</h1>
{:else}
  <ul>
    {#each cats as cat, index (index)}
      <li>{cat}</li>
    {/each}
  </ul>
{/if}

<button on:click={feed}>
  Bring out {cats.length > 0 ? "more" : ""} food
</button>
```

[Cat example](https://svelte.dev/repl/c23cb5f4607a46a8afbfcce076f78702?version=3.32.0)

+++

### Await Promises

```svelte
<script>
	let url = "https://swapi.dev/api/people/4/";

  let fetchPerson = fetch(url).then((res) => res.json());
</script>

{#await fetchPerson}
  <p>...loading</p>
{:then person}
  <h1>My name is {person.name}</h1>
{/await}
```

[Fetch example](https://svelte.dev/repl/5c1c2870c22e4fbdb6f88bc00e595d7c?version=3.32.0)

Notes:

If we want to fetch data from an API we can use the `{#await} {:then}` block to display it.

We can pass a promise to the `await` block.

Until `fetchPerson` is resolved, the `loading` paragraph will be displayed.

When `fetchPerson` resolves, you can display the value inside the `then` block.

---

### 🧪 Repair List example 💥

[`https://sveltely.github.io/todo`](https://sveltely.github.io/todo)

+++

## What's next?

![Our Slides](./qr.png)

- 🎞️ Our slides https://sveltely.github.io
- 🔥 [Official Svelte tutorial](https://svelte.dev/tutorial/basics)

Notes: We talked about components, reactiviity and logic. Hopefully you're interested

+++

## Any questions?

+++

# Thanks for listening
