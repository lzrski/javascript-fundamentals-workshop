* variables

  * `var`

  * accidental global variables

    * Why are they bad.
      * Shared state
      * Spooky effect at a distance
      * Hard to debug
      * Implicit

  * `let`

    A better `var`

  * `const`

    My word is my bond.

    Or is it?

    const a = [ 1, 2, 3 ]
    a[2] = 5

* Functions

  * First class (function as a value)

    * Callbacks

    * Composition

  * Scope

    * Closure

* Why is `this` so terrible?!

  ```javascript
  thing = { move: function (where) { this.location = where } }
  thing.move("table")
  console.log(thing.location)
  thing.move("next to the lamp")
  console.log(thing.location)

  // Simple example with setTimeout
  setTimeout(thing.move, 500, "closet")

  DB = {
    get: (whatever, callback) => setTimeout callback, 1000, "under the sofa"
  }

  DB.get("place", thing.move)
  ```

* BONUS: Promises

  > That's probably too much for one show. Let's do promises some other time.

  * The callback hell:
    ```coffeescript
    buy = (user, thing, callback) ->
      db.get "user", (user) ->
        db.get "thing", (thing) ->
          if (user.credit >= thing.price) and (thing.stockpile > 0)
            user.credit -= thing.price
            user.things = user.things.concat thing
            thing.stockpile -= 1
            db.set "user", user, () ->
              db.set "thing", thing, () ->
                callback true
          else
            callback false
    ```
  * The promised land:
    ```
    Promise
      .resolve db.get "user"
      .then (user) ->
        db.get "thing"
      .then (thing) ->

    ```
