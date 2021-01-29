# 🖥️🔥

## Getting started with Svelte

Leona 🎙️ Chows 🎙️ Braden

Notes:

Good morning, thanks for being here.

We are group 7. We have Braden, Leona and myself Chows.

Since we have been learning React recently, today we are going to give a brief
overview of the javascript framework Svelte.

Svelte is interesting because it makes writing a reactive application easier to
understand and with much less boilerplate code than React.

It compiles the code you write into vanilla JavaScript for the browser to run,
there is no virtual DOM.

+++

### What we will talk about

- 1️⃣ Local Dev / Components (Braden)
- 2️⃣ Reactivity (Leona)
- 3️⃣ Template Logic (Chows)

Notes:

Our presentation will take 10 - 15 minutes. Braden will start talking about the
development environment and Svelte components. Then Leona will talk about
reactivity and I will talk about template logic.

When we are finished talking, we will answer any questions for you.

Now I'm going to turn it over to Braden.

---

## 🐿️ Braden

Notes:

Thank you Chows, now I'm going to talk about the local development environment
for Svelte and a bit about how components work.

+++

### Getting Started

```shell
npx degit sveltejs/template your-project-name

cd your-project-name

npm install

npm run dev
```

Notes:

You can download a basic project template by running the top command. This is
similar to what `create-react-app` does for you.

You can then just change into the new folder and install the dependencies.

`npm run dev` will start a server on `localhost:5000`

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

In Svelte, you can write your JavaScript, CSS and HTML that are related all in
one `.svelte` file.

This is how it usually looks, you can use your JavaScript variables directly in
the HTML with curly braces.

+++

### Component Features

- - Nested Components
- - Props
- - Scoped styles

[Greeting Machine example](https://svelte.dev/repl/ec0f9c51e72947ad8da988be01d9c05d?version=3.32.0)

Notes:

Like in React, Svelte has the idea of nesting components and passing in data
with props.

Components also have scoped styles.

This mean that styles written in one component don't cascade outside of it.

You don't have to write crazy class names to target a specific element on a
page.

_OPEN LINK_

Let's check out this example.

Here I have two components called `App` and `Greeting`

At the top of this file I'm importing `Greeting` into my `App`

And in the HTML part of my `App` I'm using that `Greeting` component and passing
in a property called name, which has a string literal value.

So now I'll open up the Greeting component.

If you want to access the `name` property being passed in, you just need to
declare a variable with the same name as the property.

Then you use the `export` keyword in front of it to indicate that this component
can accept a property called name.

You can also give that variable a default value that will be used if nothing is
passed in.

I'll just show you the scoped styles.

Back in the `App`, the `h1` color doesn't cascade into the `Greeting`.

And the `Greeting` can still have it's own color.

Ok, that was a bit about how components are structured, Leona will tell us about
reactivity.

---

## 🐱 Leona

Notes:

OK, thanks a lot Braden.

+++

### Reactivity

- - Events
- - Binding variables
- - Reactive declarations

Notes:

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

Here we have a `count` variable and we are adding one it everytime we click the
button.

_CLICK BUTTON_

You can also add a modifier to an event that performs additional logic.

Like this one, I'll add the modifier `once` to the click event.

Now the `count` will only increment one time, no matter how many times I click
the button.

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

So you can see the `squared` variable is keeping in sync with the `count`.

That was a little bit about reactivity works in Svelte, now I'm gonna turn it
over to Chows.

---

## 🐶 Chows

Notes:

Thanks Leona

+++

### Template Logic

| Type       | Block syntax                |
| ---------- | --------------------------- |
| Lists      | `{#each} {/each}`           |
| Conditions | `{#if} {:else} {/if}`       |
| Promises   | `{#await} {:then} {/await}` |

Notes:

Now I'll talk about some of the blocks you can use in the HTML template part of
your component.

We have the `each` block for list rendering, and `if else` block for conditional
rendering, and also an `await` block that can handle data returned by a promise.

+++

### List Rendering

```svelte
<script>
  let animals = ['🦁','🦊','🦄','🐭','🦎'];
</script>

{#each animals as animal, index (index)}
  <h1>{animal}</h1>
{/each}
```

[Animals example](https://svelte.dev/repl/6c70f213b31f4f9485700cb65630ea2d?version=3.32.0)

Notes:

You can iterate over a list of objects very easily in Svelte using the `each`
block.

Saying `animals as animal, index` gives you access to each `animal` and their
index inside the `each` block.

The round parentheses at the end are for a unique key, just like the `key`
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

Notes:

Here we have an array of sleeping cats, and an empty array for eating cats.

My button at the bottom runs the `feed` function which wakes up cats with food.

I'm using an `if` block to display a message when no cats are eating.

And the `else` part will show which cats are eating.

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

If we want to fetch data from an API we can use the `await then` block to
display it.

We can pass a promise to the `await` block.

Until `fetchPerson` is resolved, the loading message will be displayed.

When `fetchPerson` resolves, you can display the value inside the `then` block.

That's all I have to say, about template logic, now Braden can wrap things up.

---

## In Summary

- - Single File Components
- - Reactivity
- - Template Logic

Notes:

Thanks Chows, so we saw how we can use single file components to organize our
applications, we saw how variables can be reactive in Svelte, and also how we
can use different blocks to display data in our HTML templates.

There are lots more interesting features that we didn't talk about.

---

## Thanks

![Our Slides](./qr.png)

- 🎞️ Our slides @ https://sveltely.github.io
- 🔥 Tutorial @ https://svelte.dev/tutorial/basics

Notes:

That brings us to the end of our presentation, thanks for listening.

If you thought any of what we showed you looked cool, then we encourage you to
read through the Official Svelte tutorial, it does a really good job of
explaining the different concepts.

+++

## Any questions?

Notes:

Does anyone have any questions?
