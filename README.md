### node-proper-lockfile
---
https://github.com/moxystudio/node-proper-lockfile

```js
// test/lock.test.js


clearTimeouts.install();

beforeAll(() => mkdirp.sync(tmpDir));

afterAll(() => rimraf.sync(tmpDir));

afterEach(async () => {
  jest.restoreAllMocks();
  clearTimeouts();
  
  await unlockAll();
  rimraf.sync(`${tmpDir}/*`);
});




```

```
```

```
```
