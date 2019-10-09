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






















it('should allow ceil\'ed second precision mtime', async () => {
  fs.writeFileSync(`${tmpDir}/foo`, '');
  
  const customFs = {
    ...fs,
    stat(path, cb) {
      fs.stat(path, (err, stat) => {
        if (err) {
          return cb(err);
        }
        
        stat.mtime = new Date(Math.ceil(stat.mtime.getTime() / 1000) * 1000);
        cb(null, stat);
      });
    },
  };
  
  await lockfile.lock(`${tmpDir}/foo`, {
    fs: customFs,
    update: 1000,
  });
  
  await pDelay(3000);
});
```

```
```

```
```
