# Etrigan Core

## EtriganError

EtriganError allows us to provide meaningful error messages that retain context and have
immutable identifiers for improved logging and alerting.

The error name should contain only letters and numbers, in upper-camel case.
E.g. `MyAppError`

You might extend `EtriganError` to declare available errors ahead of time:

```ts
class MyAppError extends EtriganError {
    constructor(message: string, innerError?: Error) {
        super('MyAppError', message, innerError)
    }
}
```

Then use your error:

```ts
throw new MyAppError('a thing went wrong')
```

You should wrap errors from external APIs for additional context:

```ts
try {
    const foo = bar()
} catch (err) {
    throw new MyAppError('Cannot foo right now', err)
}
```

This will give us a nice, hearty log message:

MyAppError: Cannot foo right now: BarError: i can haz cheezburger?
