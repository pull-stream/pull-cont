# pull-cont

pull-streams and continuables make friends!

## continuables

continuables are a like async callbacks, but more composable.
instead of taking a series of arguments, then a callback,
a continuable takes it's arguments, and returns a function
that takes exactly one argument: the callback.

this makes it easy represent a single async operation,
you can easily pass a continuable to another function.

[continuable](https://github.com/raynos/continuable) repo, bundle of best [cont](https://github.com/dominictarr/cont)inuables.

## example

pull-cont takes a continuable that returns a pull-stream, and makes it into a pull-stream.

It's like [pull-defer](https://github.com/pull-stream/pull-defer) but easier for simple cases.

``` js
var PullCont = require('pull-cont')

//create a pull-stream that reads a directory!
pull(
  PullCont(function (cb) {
    fs.readdir(directory, function (err, ls) {
      if(err) cb(err)
      else cb(null, pull.values(ls))
    })
  }),
  ...
)
```

if the continuable returns _another_ continuable, `pull-cont` will also call that recursively
until it gets a `pull-stream` source. I don't know, this might be useful for something.


## License

MIT

