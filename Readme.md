
# fork

[![Build status][travis-image]][travis-url]
[![Git tag][git-image]][git-url]
[![NPM version][npm-image]][npm-url]
[![Code style][standard-image]][standard-url]

Redux effects support for non blocking async calls.

## Installation

    $ npm install @floxjs/fork

## Usage

```js
import forkEffect, {fork, join} from '@floxjs/fork'

const store = applyMiddleware(flo(), forkEffect)(createStore)(reducer, {})

function * child () {
  yield delay(5)
  return 'foo'
}

store.dispatch(function * () {
  const task = yield fork(child)

  // do some things

  yield join(task) // => 'foo'

})
```

## API

### fork(fn)
Action creator.

- `fn` - function, generator, or iterator to fork

**Returns:** a task

### join(task)
Action creator.

- `task` - task to block on

**Returns:** result of task

### cancel(task)
Action creator. Throws error in running task with message: 'TaskCanceled'.

- `task` - task to cancel

### taskRunner(dispatch)
Runs tasks. Used internally by koax.

- `dispatch` - dispatch function

**Returns:** `dispatch`

### task.isRunning()

**Returns:** whether task is running

### task.result()

**Returns:** the result of the task

### task.error()

**Returns:** the error thrown by the task

###task.cancel()
Cancels task
## License

MIT

[travis-image]: https://img.shields.io/travis/floxjs/fork.svg?style=flat-square
[travis-url]: https://travis-ci.org/floxjs/fork
[git-image]: https://img.shields.io/github/tag/floxjs/fork.svg?style=flat-square
[git-url]: https://github.com/floxjs/fork
[standard-image]: https://img.shields.io/badge/code%20style-standard-brightgreen.svg?style=flat-square
[standard-url]: https://github.com/feross/standard
[npm-image]: https://img.shields.io/npm/v/@floxjs/fork.svg?style=flat-square
[npm-url]: https://npmjs.org/package/@floxjs/fork
