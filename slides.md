---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
# some information about your slides, markdown enabled
title: Enhancing React Performance- Mastering Re-render Optimization
info: |
  ## React Next 2024
  Tal moskovich
# apply any unocss classes to the current slide
class: text-center
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# https://sli.dev/guide/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/guide/syntax#mdc-syntax
mdc: true
background: Hero.jpg
fonts:
  sans: rubik
---

# Enhancing React Performance: Mastering Re-render Optimization

## Tal Moskovich

<div class="flex pt-12 justify-center">
  <img src='/Site-Logo_H_ReactNext_website.png' width=100 />
</div>

<style>
  h1
  {
    color: white;
    -webkit-text-fill-color: white;
  }
</style>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
layout: center
transition: slide-down
---

# What Is the Most Joyful Thing in React?
<img src='/react-logo.svg' width=300 class='m-auto' />

<style>
  h1
  {
    font-size: 5rem;
    text-align: center;
    line-height: 6rem;
  }
</style>
---
layout: center
# class: bg-gradient-to-l from-purple-500 to-blue-400
transition: slide-down

---
# Avoiding Unnecessary <br> Re-rendering
<img src='/refresh.png' width=150 class='m-auto' />

<style>
  h1
  {
    font-size: 5rem;
    text-align: center;
    line-height: 6rem;
  }
</style>
---
layout: center
transition: slide-down

---

# Memoization
<div class="absolute left-120 top-20 inset-0 transform rotate-45 bg-red-500 w-4 h-100"></div>
<div class="absolute left-120 top-20 inset-0 transform -rotate-45 bg-red-500 w-4 h-100"></div>


<style>
  h1
  {
    font-size: 8rem;
    line-height: 9rem;
  }
</style>
---
layout: center
transition: slide-down

---

# React Compiler
<div class="absolute left-120 top-17 inset-0 transform rotate-45 bg-red-500 w-4 h-100"></div>
<div class="absolute left-120 top-17 inset-0 transform -rotate-45 bg-red-500 w-4 h-100"></div>


<style>
  h1
  {
    font-size: 6rem;
    line-height: 7rem;
  }
</style>
---
layout: center
transition: slide-down

---

# React Forget
<div class="absolute left-120 top-17 inset-0 transform rotate-45 bg-red-500 w-4 h-100"></div>
<div class="absolute left-120 top-17 inset-0 transform -rotate-45 bg-red-500 w-4 h-100"></div>


<style>
  h1
  {
    font-size: 6rem;
    line-height: 7rem;
  }
</style>
---
layout: center
transition: slide-down

---

# React Unforget
<div class="absolute left-120 top-17 inset-0 transform rotate-45 bg-red-500 w-4 h-100"></div>
<div class="absolute left-120 top-17 inset-0 transform -rotate-45 bg-red-500 w-4 h-100"></div>


<style>
  h1
  {
    font-size: 6rem;
    line-height: 7rem;
  }
</style>
---
layout: center

---

# Just Plain React!
<img src='/awesome.png' width=200 class='m-auto pt-10' />


<style>
  h1
  {
    font-size: 6rem;
    line-height: 7rem;
  }
</style>
---
layout: two-cols
class: self-center
---
# Hello, I'm Tal
<br>

🔥 **Committing Code &** <br>
**Pushing Personal Boundaries**
- 🧑‍💻 **Front-end Developer** @ Enpitech
- 🎧 **Podcaster & Lecturer** @ lotechni.dev
- 💡 **Proactivity Advocate**

<div class='flex pt-22 justify-start items-center'>
<img src='/enpitech.svg' class='h-20 -ml-8'/>
<img src='/lotechni.png' class='w-25'/>
</div>

::right::
<img src='/profile.png' class='w-80 m-auto' />

---
layout: two-cols-header
class: flex flex-col m-5 justify-center -mt-3
transition: slide-down

---

# Let's Start with a Quick(?) Example

::left::

````md magic-move {lines: true}
```tsx {2}
function App() {
  const [state, setState] = useState({});
}
```
```tsx {5,6}
function App() {
  const [state, setState] = useState({});

  return (
    <FormContext.Provider value={[state, setState]}>
    </FormContext.Provider>
  );
}
```
```tsx {6,7}
function App() {
  const [state, setState] = useState({});

  return (
    <FormContext.Provider value={[state, setState]}>
        <Form />
        <HeavyComponent /> /* A busy-awaited component */
    </FormContext.Provider>
  );
}
```
```tsx {11-15}
function App() {
  const [state, setState] = useState({});

  return (
    <FormContext.Provider value={[state, setState]}>
        <Form />
        <HeavyComponent /> /* A busy-awaited component */
    </FormContext.Provider>
  );
}

function Form() {
  const [state, setState] = useContext(FormContext);
  // ...just a basic form
}
```
````

::right::
<iframe v-click src='http://localhost:3000' class='w-full h-110'></iframe>

---
layout: two-cols-header
---

# So, What Do We Have Here?

::left::
<div class="flex justify-center items-center">

<div class="absolute min-w-100">
````md magic-move {lines: true}
```tsx
function App() {
  return (
    ...
  );
}
```
```tsx {2,5,6}
function App() {
  const [state, setState] = useState({});

  return (
    <FormContext.Provider value={[state, setState]}>
    </FormContext.Provider>
  );
}
```
```tsx {6,7,12-15}
function App() {
  const [state, setState] = useState({});

  return (
    <FormContext.Provider value={[state, setState]}>
     <Form />
     <HeavyComponent /> /* A busy-awaited component */
    </FormContext.Provider>
  );
}

function Form() {
  const [state, setState] = useContext(FormContext);
  // ...just a basic form
}
```
```tsx {13}
function App() {
  const [state, setState] = useState({});

  return (
    <FormContext.Provider value={[state, setState]}>
     <Form />
     <HeavyComponent /> /* A busy-awaited component */
    </FormContext.Provider>
  );
}

function Form() {
  const [state, setState] = useContext(FormContext);
  // ...just a basic form
}
```
```tsx
//Re-rendering...
function App() {
  return (
    ...
  );
}
```
````
</div>
</div>


::right::
<div class="flex justify-center items-center">
<div class='absolute' v-click='[0, 1]'>

```mermaid {theme: 'dark', scale: 1.2}
graph
App
```
</div>
<div class='absolute' v-click='[1, 2]'>

```mermaid {theme: 'dark', scale: 1.2}
graph
App --> |State|P[FormContext.Provider]

```
</div>

<div class='absolute' v-click='[2, 4]'>

```mermaid {theme: 'dark', scale: 1.2}
graph
App --> |State|P[FormContext.Provider]
P --> |State-UseContext|Form
P -->C[HeavyComponent]
```
</div>
<div v-click="[3, 4]">
<arrow x1="550" y1="500" x2="600" y2="450" color="#953" width="2" arrowSize="1" />
<p class="absolute bottom-12 right-100 transform text-orange-500 -rotate-45">Typing...</p>
</div>
<div class='absolute' v-click='[4, 5]'>

```mermaid {theme: 'dark', scale: 1.2}
graph
App
```
</div>
</div>
---
layout: two-cols-header
class: flex flex-col m-5 justify-center -mt-3
transition: slide-down

---

# Maybe a Better One?

::left::
<v-click>
````md magic-move {lines: true}
```tsx{5,8,2}
function App() {
  const [state, setState] = useState({});

  return (
    <FormContext.Provider value={[state, setState]}>
        <Form />
        <HeavyComponent />
    </FormContext.Provider>
  );
}
```

```tsx{3,6}
function App() {
  return (
    <ContextWrapper>
        <Form />
        <HeavyComponent />
    </ContextWrapper>
  );
}
```

```tsx{3,6,10-18}
function App() {
  return (
    <ContextWrapper>
        <Form />
        <HeavyComponent />
    </ContextWrapper>
  );
}

function ContextWrapper({ children }) {
  const [state, setState] = useState({});

  return (
    <FormContext.Provider value={[state, setState]}>
      {children}
    </FormContext.Provider>
  );
}
```
````

</v-click>

::right::
<iframe v-click src='http://localhost:3000' class='w-full h-110'></iframe>
---
layout: two-cols-header
---

# How Did We Get Here?

::left::
<div class="flex justify-center items-center">

<div class="absolute min-w-100">
````md magic-move {lines: true}
```tsx
function App() {
  return (
    ...
  );
}
```

```tsx{3-6}
function App() {
  return (
    <ContextWrapper>
        <Form />
        <HeavyComponent />
    </ContextWrapper>
  );
}
```

```tsx{3,6,10-18}
function App() {
  return (
    <ContextWrapper>
        <Form />
        <HeavyComponent />
    </ContextWrapper>
  );
}

function ContextWrapper({ children }) {
  const [state, setState] = useState({});

  return (
    <FormContext.Provider value={[state, setState]}>
      {children}
    </FormContext.Provider>
  );
}
```
```tsx
function App() {
  return (
    <ContextWrapper>
        <Form />
        <HeavyComponent />
    </ContextWrapper>
  );
}

function ContextWrapper({ children }) {
  const [state, setState] = useState({});

  return (
    <FormContext.Provider value={[state, setState]}>
      {children}
    </FormContext.Provider>
  );
}
```
```tsx
function App() {
  return (
    <ContextWrapper>
        <Form /> //Re-rendered because context changing
        <HeavyComponent /> // 🤯 NOT RE-RENDERED
    </ContextWrapper>
  );
}

  /*
  Re-rendered because state changing
  */
function ContextWrapper({ children }) {
  const [state, setState] = useState({});

  return (
    <FormContext.Provider value={[state, setState]}>
      {children}
    </FormContext.Provider>
  );
}
```
````
</div>
</div>


::right::
<div class="flex justify-center items-center">
<div class='absolute' v-click='[0, 1]'>

```mermaid {theme: 'dark', scale: 1}
graph
App
```
</div>
<div class='absolute' v-click='[1, 2]'>

```mermaid {theme: 'dark', scale: 1}
graph
App --> ContextWrapper
App -.-> Form
App -.-> HeavyComponent

```
</div>

<div class='absolute' v-click='[2, 4]'>

```mermaid {theme: 'dark', scale: 1}
graph
App --> ContextWrapper
ContextWrapper --> |State|P[FormContext.Provider]
P --> |State-UseContext|Form
P -->HeavyComponent
App -.-> Form
App -.-> HeavyComponent
```
</div>
<div v-click="[3, 4]">
<arrow x1="600" y1="500" x2="650" y2="450" color="#953" width="2" arrowSize="1" />
<p class="absolute bottom-12 right-88 transform text-orange-500 -rotate-45">Typing...</p>
</div>
<div class='absolute' v-click='[4, 5]'>

```mermaid {theme: 'dark', scale: 1.2}
graph
App -.-> HeavyComponent
```
</div>
</div>
---
layout: two-cols-header
---

# How Isn't HeavyComponent Re-Rendered?

::left::
It's all about how React works!

<div class="min-w-300">
<v-clicks>

- 🧳 **Props are Objects**

- 📂 **Props are saved in the Fiber nodes** (the "Virtual DOM")

Therefore:

- 🔄 **Props Objects are re-created on each render**

But what about `children`?

- 🧩 **Children can be considered as a reference to other (rendered) Fiber nodes**

- 🧬 **Children save their referential identity from the previous render**

Therefore:

- 🛡️ **Our HeavyComponent isn't re-rendered!**

</v-clicks>
</div>

::right::
<div class="absolute top-50 right-20 min-w-50">
````md magic-move {at:'1'}
```tsx
function Component(props) {
  return (...)
}
```

```tsx
function Component(props) {
  return (...)
}
```

```tsx
function Component({...}) {
  return (...)
}
```
```tsx
function Component({...}) {
  return (...)
}
```
```tsx
function Component
({children}:{children: ReactNode}) 
{
  return (...)
}
```
````
</div>
<div v-click="[1, 4]">
<arrow x1="850" y1="170" x2="850" y2="200" color="#953" width="2" arrowSize="1" />
<p class="absolute top-25 right-20 transform text-orange-500 text-center">A reference to an object <br> in the Fiber node</p>
</div>
<div v-click='5'>
<arrow x1="850" y1="180" x2="850" y2="230" color="#953" width="2" arrowSize="1" />
<p class="absolute top-30 right-20 transform text-orange-500 text-center">ReactNode is actually a Fiber node</p>
</div>

<!--
Here is another comment.
-->
---
layout: two-cols-header
class: flex flex-col m-5 justify-center -mt-3
transition: slide-down

---

# Will It Also Work?

::left::
<v-click>
````md magic-move {lines: true}

```tsx{4,5}
function App() {
  return (
    <ContextWrapper>
        <Form />
        <HeavyComponent />
    </ContextWrapper>
  );
}
```
```tsx{4,5}
function App() {
  return (
    <ContextWrapper
        form={<Form />}
        heavyComponent={<HeavyComponent />}
    />
  );
}
```

```tsx{4,5,10,15,16}
function App() {
  return (
    <ContextWrapper
        form={<Form />}
        heavyComponent={<HeavyComponent />}
    />
  );
}

function ContextWrapper({ form, heavyComponent }) {
  const [state, setState] = useState({});

  return (
    <FormContext.Provider value={[state, setState]}>
      {form}
      {heavyComponent}
    </FormContext.Provider>
  );
}
```
````

</v-click>

::right::
<iframe v-click src='http://localhost:3000' class='w-full h-110'></iframe>

---
---
# OK, But How?
Let's look at the code again:
````md magic-move {lines: true}
```tsx{none}
function App() {
  return (
    <ContextWrapper
        form={<Form />}
        heavyComponent={<HeavyComponent />}
    />
  );
}

function ContextWrapper({ form, heavyComponent }) {
  const [state, setState] = useState({});

  return (
    <FormContext.Provider value={[state, setState]}>
      {form}
      {heavyComponent}
    </FormContext.Provider>
  );
}
```
```tsx{4}
function App() {
  return (
    <ContextWrapper
        form={<Form />}
        heavyComponent={<HeavyComponent />}
    />
  );
}

function ContextWrapper({ form, heavyComponent }) {
  const [state, setState] = useState({});

  return (
    <FormContext.Provider value={[state, setState]}>
      {form}
      {heavyComponent}
    </FormContext.Provider>
  );
}
```
```tsx{5}
function App() {
  return (
    <ContextWrapper
        form={<Form />}
        heavyComponent={<HeavyComponent />}
    />
  );
}

function ContextWrapper({ form, heavyComponent }) {
  const [state, setState] = useState({});

  return (
    <FormContext.Provider value={[state, setState]}>
      {form}
      {heavyComponent}
    </FormContext.Provider>
  );
}
```
```tsx{15,16}
function App() {
  return (
    <ContextWrapper
        form={<Form />}
        heavyComponent={<HeavyComponent />}
    />
  );
}

function ContextWrapper({ form, heavyComponent }) {
  const [state, setState] = useState({});

  return (
    <FormContext.Provider value={[state, setState]}>
      {form}
      {heavyComponent}
    </FormContext.Provider>
  );
}
```
```tsx{15}
function App() {
  return (
    <ContextWrapper
        form={<Form />}
        heavyComponent={<HeavyComponent />}
    />
  );
}

function ContextWrapper({ form, heavyComponent }) {
  const [state, setState] = useState({});

  return (
    <FormContext.Provider value={[state, setState]}>
      {form}
      {heavyComponent}
    </FormContext.Provider>
  );
}
```
```tsx{4,10}
function App() {
  return (
    <ContextWrapper
        form={<Form />}
        heavyComponent={<HeavyComponent />}
    />
  );
}

function ContextWrapper({ form, heavyComponent }) {
  const [state, setState] = useState({});

  return (
    <FormContext.Provider value={[state, setState]}>
      {form}
      {heavyComponent}
    </FormContext.Provider>
  );
}
```
````
<div v-click="[1, 2]">
<arrow x1="300" y1="200" x2="260" y2="200" color="#953" width="2" arrowSize="1" />
<p class="absolute top-43 left-80 text-orange-500 text-center">`form` gets a rendered (ReactNode) value</p>
</div>
<div v-click="[2, 3]">
<arrow x1="470" y1="216" x2="410" y2="216" color="#953" width="2" arrowSize="1" />
<p class="absolute top-47 left-120 text-orange-500 text-center">`heavyComponent` gets a rendered (ReactNode) value</p>
</div>
<div v-click="[3,4]">
<arrow x1="320" y1="400" x2="270" y2="400" color="#953" width="2" arrowSize="1" />
<p class="absolute bottom-31 left-82 text-orange-500 text-center">'form' and 'heavyComponent' serves as slots</p>
</div>
<div v-click="[4,5]">
<arrow x1="320" y1="400" x2="270" y2="400" color="#953" width="2" arrowSize="1" />
<p class="absolute bottom-31 left-82 text-orange-500 text-center">Typing in 'form' initiates state change</p>
</div>
<div v-click="[5,6]">
<p class="absolute bottom-64 left-75 text-orange-500 text-center">Only 'Form' and 'ContextWrapper' are re-rendered! <br>And 'HeavyComponent' is "memoized"!</p>
</div>
---
layout: image-right
image: /developer.webp
---

# From Props Drilling to Component Drilling

<v-clicks>
 
 - If you give React the same element you gave it on the last render, **it won't bother re-rendering** that element.
 
 - "Lift" the expensive component to a parent where it will be rendered **less often**.
 
 - Then pass the expensive component **down as a prop**.

</v-clicks>
---
layout: image-right
image: '/lecture.png'
---
# Thanks For Listening!
## Tal Moskovich
<img src='/qrcode_github.com.png' class='w-20 m-auto pt-10' />
<p class='text-center'><a href='https://github.com/talmoskovich/ReactNext2024'>Code & Slides repo</a></p>
<img src='/qrcode_tmosko.com.png' class='w-20 m-auto pt-10' />
<p class='text-center'><a href='https://tmosko.com/hello'>Contact Me</a></p>

