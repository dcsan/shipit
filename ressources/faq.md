# Frequently asked questions!
extracted from the issues


## How can I call shipit programatically?
For example to call a shipit task from your own wrapper CLI.
This is undocumented but possible, 
[have a look at the test in branch v4](https://github.com/shipitjs/shipit/tree/master/packages/shipit-cli/tests)

```js
const shipitCli = path.resolve(__dirname, '../../shipit-cli/src/cli.js')
await exec(
        `babel-node ${shipitCli} --shipitfile ${shipitFile} test deploy`,
      )
```

## How do I wait for a task to finish?
You can use the `blTask` to create a blocking task.
If you use `async` make sure to `await` the internal task calls

```js
shipit.blTask('hello', async () => {
  await shipit.remote('echo "hello on remote"')
  await shipit.local('echo "hello from local"')
})
```

## How do I run a task against multiple environments?
