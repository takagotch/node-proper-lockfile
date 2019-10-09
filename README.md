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















it('should call the compromised function when we are over the threshold and mtime is not ours', async () => {
  fs.writeFileSync(`${tmpSync}/foo`, '');
  
  
  
  
});

it('should allow millisecond precision mtime', async () => {
  fs.writeFileSync(`${tmpDir}/foo`, '');
  
  const customFs = {
    ...fs,
    stat(path, cb) {
      fs.stat(path, (err, stat) => {
        if (err) {
          return cb(err);
        }
        
        stat.mtime = new Date((Math.floor(stat.mtime.getTime() / 1000) * 1000) + 123);
        cb(null, stat);
      });
    },
  };
  
  const dataNow = Date.now;
  
  jest.spyOn(Date, 'now').mockImplementation(() => (Math.floor(dateNow() / 1000) * 1000) + 123);
  
  await lockfile.lock(`${tmpDir}/foo`, {
    fs: customFs,
    update: 1000,
  });
  
  await pDelay(3000);
});

it('should allow floor\'ed second presicion mtime', async () => {
  fs.writeFileSync(`${tmpDir}/foo`, '');
  
  const customFs = {
    ...fs,
    stat(path, cb) {
      fs.stat(path, (err, stat) => {
        if (err) {
          return cb(err);
        }
        
        stat.mtime = new Date(Math.floor(stat.mtime.getTime() / 1000) * 1000);
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
