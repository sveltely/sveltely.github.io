# 🖥️🔥

## Getting started with Svelte

Leona 🎙️ Chows 🎙️ Braden

Notes:

Good morning, thanks for being here.

We are group 7. We have Braden, Leona and myself Chows.

Today we are going to give a brief overview of the javascript framework Svelte.

Svelte is interesting because it makes writing a reactive application easier to
understand and with much less boilerplate code than React.

It compiles the code you write into vanilla JavaScript for the browser to run
(no virtual DOM).

+++

### What we will talk about

- 1️⃣ Local Dev / Components (Braden)
- 2️⃣ Reactivity (Leona)
- 3️⃣ Template Logic (Chows)
- 4️⃣ Demo + Questions

Notes:

It will take 10 - 15 minutes. Braden will start talking about the development
environment and Svelte components. Then Leona will talk about reactivity and I
will talk about template logic.

When we are finished talking, Leona will give a short demo and we will answer
any questions for you.

---

## 🐿️ Braden

Notes:

Now I'm going to turn it over to Braden.

+++

### Getting Started

```shell
npx degit sveltejs/template your-project-name

cd your-project-name

npm install

npm run dev
```

Notes:

Thank you Chows, now I'm going to talk about the local development environment
for Svelte and a bit about how components work.

You can get a project template by running the first command. This is similar to
what `create-react-app` does for you.

You can then change directories into your new project folder and run
`npm install` to get all the dependencies.

Once that's finished installing you can do `npm run dev` to start the local
development server.

+++

### Single File Components

```svelte
<!-- Number.svelte -->

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

In Svelte, you can write your JavaScript, CSS and HTML that relate to a
component all in one `.svelte` file.

If you take a look in the source directory, you'll see a component called
`App.svelte`.

This is the top level component.

+++

### Component Features

- ♻ Nested Components
- 📁 Props
- 🎯 Scoped styles

[Greeting Machine example](https://svelte.dev/repl/ec0f9c51e72947ad8da988be01d9c05d?version=3.32.0)

Notes:

Like in React, Svelte has the idea of nesting components and passing in data
with props.

A feature that I find interesting, is scoped styles.

This mean that styles written in a Svelte component do not cascade outside of
it.

You don't have to write crazy class names to target an element on a page.

_OPEN LINK_

Let's check out this example.

Here I have two components called `App` and `Greeting`

At the top of the file I'm importing `Greeting` into my `App`

On line 6 I'm passing in a property to the `Greeting` component called name, and
its value it just a string literal.

So now I'll open up the Greeting component.

Like you know in React you access the data passed in with the `props` variable.

In Svelte you just declare a variable with the name as the prop and then use the
`export` keyword in front of it to indicate that it's a prop.

You can also set a default value that will be use if the prop is not passed in.

I'll just show you the scoped styles.

The `h1` color in the `App` doesn't cascade into the `Greeting`.

And the `Greeting` can have it's own color too.

---

## 🐱 Leona

Notes:

Ok, that was a bit about how components are structured, Leona will tell us about
reactivity.

+++

### Reactivity

- - Events
- - Binding variables
- - Reactive declarations

Notes:

OK, thanks a lot Braden.

I'll talk about how you can handle DOM events, variable binding and reactive
declarations in Svelte.

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

[Counter example](https://svelte.dev/repl/49eee179638f4da09d7a7d40de3b20b9?version=3.32.0)

Notes:

In Svelte you can use `on:(event_name)` to bind an element to any DOM event.

You can pass a handler function inside curly braces just like in React.

_OPEN LINK_

Here we have a `count` variable and we are incrementing it everytime the user
clicks the button.

You can also add a modifier to an event that performs additional logic.

Like this one, I'll add the modifier `once` to the click event.

Now the `count` will only ever increment one time, no matter how many times I
click the button.

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

Notes:

For this input element at the bottom, if I wanna update the `name` variable with
whatever I type in, the only way I can do that in React is to add an onChange
event listener, and then update the state.

This is how it might look in React. We are listening for the keyup event and
then updating the name variable.

_OPEN LINK_

But in Svelte, you can use the `bind:value` directive, which gives you two-way
data binding without the need to listen for events.

_ADD `bind:value` to `<input>`_

When the input changes, `name` updates, and if the `name` changes (like when you
might want to set it to an empty string), the input value will change as well.

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

Notes:

With reactive declarations we don't need to listen for events to update a value
which depends on other variables.

The `$:` indicates that this line only runs when any variables on the right side
of the equals are changed.

_OPEN LINK_

So just like my counter example before, this is the same, but I've added a
reactive declartion called `squared` which is related to the `count` variable.

_CLICK BUTTON_

So you can see that the `squared` variable is keeping in sync with the `count`.

---

## 🐶 Chows

Notes:

That was a little bit about Svelte reactivity, now I'm gonna turn it over to
Chows.

+++

### Template Logic

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

Notes: You can iterate over a list of objects very easily in Svelte using the
`each` block.

Saying `animals as animal, index` gives you access to each animal and their
index inside the `each` block.

The round parentheses at the end are for a unique key, just like the key
property in React.

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

If we want to fetch data from an API we can use the `{#await} {:then}` block to
display it.

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

Notes: We talked about components, reactiviity and logic. Hopefully you're
interested

+++

## Any questions?

+++

# Thanks for listening
