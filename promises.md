## BONUS: Promises

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

    ```javascript
    Promise
      .resolve db.get "user"
      .then (user) ->
        db.get "thing"
      .then (thing) ->
        user.credit -= thing.price
        user.things = user.things.concat thing
        thing.stockpile -= 1

        return
        // oops... now the user is out of scope
    ```

> TODO: Finish the promises stuff
