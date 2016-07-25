# variables

## `var`

* Easy peasy

  ```javascript
  var x = 10
  var y = 20
  x = 30
  var x = 40
  ```

* Scope is not quite as one could expected.

  ```javascript
  var x = 10
  var y = 20

  if (x < y) {
      var x = x + y
      console.log(`Do something with our new x (${x})...`)
  }
  console.log(`The value of x is now ${x}. Who would have funk?`)
  ```

* More practical example

  ```javascript
  for (var i = 0; i < 3; i += 1) {
    var button = document.createElement("button")
    button.textContent = `Button ${i}`
    button.addEventListener("click", (event) =>
      console.log(`button ${i} clicked`)
    )
    document
      .querySelector("#user-content-buttons")
      .appendChild(button)
  }
  ```

  <div id="user-content-buttons"></div>

## `let`

A better `var`.

* Can't redeclare

* Scope is more intuitive

## `const`

* Like let, but value is constant.

* My word is my bond.

  ```javascript
  const the_budget_for_your_project = 10000000
  the_budget_for_your_project = 1000
  ```

* Or is it?

  ```javascript
  const your_project = {
    name: "Improve website",
    scope: "Fix a typo on the landing page"
    budget: 2000
  }

  console.log(`Signed up to ${your_project.scope} for ${your_project.budget}€`)

  your_project.budget = 1000
  your_project.scope = "Fix a typo on the landing page and also make it responsive, reactive, cloud connected, with better off-line first engagement and working on IE 4 running on our CEO's Windows CE device. Also the tax-and-accounting department has issues with the agile way you organically treated vertical integration with our enterprise IOT platform. We need more synergy here ASAP! Also please cross-pollinate our team IP."

  console.log(`Now you need to ${your_project.scope}. You have ${your_project.budget}€ to make it happen.`)
  ```

* So what is a value anyway?

  ```javascript
  const o1 = { a: 1, b: 2 }
  const o2 = o1
  o2.b = 200
  console.log(o1);
  ```

## accidental global variables

Why are global variables bad?

* Shared state

  State is the root of most evil **Ⓐ**

  If you share your state it get's dirty. It is bad for our health.

  ![how often do you share?](./cat-uses-my-toothbrush.jpg)

* Spooky effect at a distance

  ```javascript
  // counter.js
  count = function() {
      if (typeof n === "undefined") {
          n = 0
      }
      n = n + 1
      return n
  }

  // geometry.js
  area = function (x, y) {
      n = x * y
      return n
  }
  ```

* Hard to debug

* Indicators of poor architecture

* Look out!

  You can still make a global variable even if you use `var`!

  ```html
  <!DOCTYPE html>
  <html>
    <head>
      <meta charset="utf-8">
      <title>Empty document</title>
    </head>
    <body>

      <script>
      var fn = function() { return a }
      </script>

      <script>
      var a = 1;
      </script>

      <script>
        console.log(fn())
        console.log(window.a)
      </script>

    </body>
  </html>
  ```

## Functions

* First class

  a function is a value

  ```javascript
  const red_plastic = { color: "red" }
  const yellow_plastic = { color: "yellow" }
  const black_plastic = { color: "black" }

  const duck_machine = (plastic) => `A bunch of ${plastic.color} rubber ducks.`

  console.log(duck_machine(red_plastic))
  console.log(duck_machine(yellow_plastic))

  const engineer = (machine) => (input) => `${machine(input)}.. with a batman logo on them!`

  const better_duck_machine = engineer(duck_machine)

  console.log(better_duck_machine(black_plastic))
  ```

* Callbacks

  Let's revisit our buttons example...

* Closures

  A function, when it's being created remembers it's scope. Every time you call it, the scope will be the same.

  ```javascript
  const wrapper = () => {
      let x = 10
      return (y) => x + y
  }

  const x = 1
  console.log(x);

  const wrapped = wrapper()
  console.log(wrapped(20))
  ```

## Why is `this` so terrible?!

```javascript
thing = {
  move: function (where) {
    this.location = where
  }
}

thing.move("on the table")
console.log(`The thing is ${thing.location}`)
thing.move("next to the lamp")
console.log(`The thing is ${thing.location}`)

setTimeout(thing.move, 500, "in the outer space")
```
