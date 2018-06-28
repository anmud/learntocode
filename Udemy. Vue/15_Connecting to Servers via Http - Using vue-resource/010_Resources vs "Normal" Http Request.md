# Resources vs "Normal" Http Request

This is important to hightlight - `resources` are only the alternative to use `http.post` and `http.get` which is perfectly fine and which might be the better solution in a lot of cases where you don't want to create reusable `resources`, but only need to send from time to time a `request` here and then there. 