# NPM Workspaces Example

A simple example showing how you can use `npm workspaces` and invoke the
run command for workspace packages much like the [`yarn workspaces run`](https://classic.yarnpkg.com/en/docs/cli/workspaces/#toc-yarn-workspaces-run) command.

At the time of writing official documentation is lacking and exists mainly in the form of the  [RFC](https://github.com/npm/rfcs/blob/26e8ac6ee176943d6522d5d057fab05e37655e1c/accepted/0000-workspaces.md).

This example outlines a short custom `package.json` `script` that can replicate the behavior. e.g:

```
npm run workspace package-a test -- -u
```

## How can I run npm workspace scripts from my project root?

Add this script to your root `package.json`

```
"scripts": {
	"workspace": "run(){ cd $1 && npm run $2 -- ${@:3}; }; run"
}
```

Invoke with:

```
npm run workspace <workspace-name> <command> [-- <args>]
````

## Demo
- Clone the repo
- Ensure you are using *npm* version **7.0.0+** (bundled with *Node.js* **v15+**)
- `npm install` in the project root directory
- Invoke a workspace script with
```
npm run workspace <workspace-name> <command> [-- <args>]
```

### Command Examples

```
npm run workspace package-b test
npm run workspace nested-packages/nested-a log

npm run workspace package-b log -- arg1 arg2
npm run workspace package-b log -- --flag1 -f2
npm run workspace package-b test -- -u
````