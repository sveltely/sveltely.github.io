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

### A basic project template

```shell
npx degit sveltejs/template your-project-name
```

Notes: You can get a project template by running this command. It's similar to
what `create-react-app` does for you.

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

You can keep your JavaScript, styles and markup relating to a component all in
the same file. Styles a scoped to the component so you don't have to write crazy
class names to target an element on the page.

+++

### Component Features

- ♻ Importing other components
- 📁 Props
- 🎯 Scoped styles

[Greeting Machine example](https://svelte.dev/repl/ec0f9c51e72947ad8da988be01d9c05d?version=3.32.0)

---

## 🐱 Leona

+++

### Reactivity

- Binding variables
- Events
- Reactive statements

+++

### Binding Variables

```svelte
<script>
  let name = "";
</script>

<h1>
  Hello {name || '??'}
</h1>

<input type="text" bind:value={name} />
```

[Text input example](https://svelte.dev/repl/373f2a9ce2c04e17abcdb2ca74773b36?version=3.32.0)

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

Notes: Here we are calling the increment function when the user clicks the
button. You can use `on:event_name` to bind an element to any dom events.

+++

### Reactive Statements

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

Notes: With reactive statements we don't need to listen for events to update a
value.

The `$:` indicates the this line only runs when any variables in the statement,
or on the right side of the equals are changed.

---

## 🐶 Chows

+++

### Logic

| Block      | Syntax                |
| ---------- | --------------------- |
| Lists      | `{#each} {/each}`     |
| Conditions | `{#if} {:else} {/if}` |
| Promises   | `{#await} {/await}`   |

+++

### List Rendering

```svelte
<script>
  let animals = [
    {id: 1, photo: '🦁'},
    {id: 2, photo: '🦊'},
    {id: 3, photo: '🦄'},
    {id: 4, photo: '🐭'},
    {id: 5, photo: '🦎'},
  ];
</script>

{#each animals as animal (animal.id)}
  <h1>{animal.photo}</h1>
{/each}
```

[Animal example](https://svelte.dev/repl/8c60289cdbde409eab41811e09f779fc?version=3.32.0)

Notes: You can iterate over a list of objects very easily in Svelte using the
`each` block.

You can say `each animals as animal` and then have access to the animal object
inside the `each` block.

The round parentheses at the end of the `each` block are for a unique key
identifying each object.

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
  let vader = fetch("https://swapi.dev/api/people/4/")
              .then((res) => res.json());
  let planet = fetch("https://swapi.dev/api/planets/1/")
              .then((res) => res.json());
</script>

{#await vader}
  <p>...waiting</p>
{:then vader}
  <h1>My name is {vader.name}</h1>
  <p>
    My homeworld is
    {#await planet then planet}
      {planet.name}
    {/await}
  </p>
{/await}
```

[Fetch example](https://svelte.dev/repl/5c1c2870c22e4fbdb6f88bc00e595d7c?version=3.32.0)

---

### 🧪 Repair List example 💥

[`https://sveltely.github.io/todo`](https://sveltely.github.io/todo)

+++

## What's next?

![Our Slides](./qr.png)

- 🎞️ Our slides https://sveltely.github.io
- 🔥 [Official Svelte tutorial](https://svelte.dev/tutorial/basics)

Notes: We talked about components, reactiviity and logic. Hopefully you're
interested

+++

## Any questions?

+++

# Thanks for listening
