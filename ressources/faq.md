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
`shipit.remote()` is returning a promise, you have to return it, else Shipit will not wait.

```js
  shipit.blTask('yarn-server', function () {
    let cmd1 = `cd ${deployDir}/server && yarn install --frozen-lockfile`
    return shipit.remote(cmd1)
  })
```

If you use `async` make sure to `await` the internal task calls

```js
shipit.blTask('hello', async () => {
  await shipit.remote('echo "hello on remote"')
  await shipit.local('echo "hello from local"')
})
```

see https://github.com/shipitjs/shipit/issues/176

## How to run a task against multiple environments?


## How do I obtain the environment currently deploying
`shipit.environment` has the info, but the best way to achieve it actually is to create another entry in the configuration. Relying directly on environment is not a good thing...
https://github.com/shipitjs/shipit/issues/174

## Sharing config file info with your own app
https://github.com/shipitjs/shipit/issues/180

## How to stop local env var expansion with shipit.remote

    await shipit.remote('printenv PATH')
  
or escape your path 

    await shipit.remote(`echo \$PATH`)

https://github.com/shipitjs/shipit/issues/152

