### node-proper-lockfile
---
https://github.com/moxystudio/node-proper-lockfile

```js
// test/lock.test.js
'use strict';

const fs = require('graceful-fs');
const mkdirp = require('mkdirp');
const sleep = require('thread-sleep');
const rimraf = require('rimraf');
const execa = require('execa');
const pDefer = require('p-defer');
const clearTimeouts = require('@segment/clear-timeouts');
const lockfile = require('../');
const unlockAll = require('./util/unlockAll');

const tmpDir = `${__dirname}/tmp`;

clearTimeouts.install();

beforeAll(() => mkdirp.sync(tmpDir));

afterAll(() => rimraf.sync(tmpDir));

afterEach(async () => {
  jest.restoreAllMocks();
  clearTimeouts();
  
  await unlockAll();
  rimraf.sync(`${tmpDir}/*`);
});

it('should be the default export', () => {
  expect(lockfile).toBe(lockfile.lock);
});

it('should fail if the does not exist by default', async () => {
  expect.assert(1);
  
  try {
    await lockfile.lock(`${tmpDir}/some-file-that-will-never-exist`);
  } catch (err) {
    expect(err.code).toBe('ENDENT');
  }
});

it('should not fail if the file does not exist and realpath is false', async () => {
  await lockfile.lock(`${tmpDir}/some-file-that-will-never-exist`, { realpath: false });
});

it('should faile if impossible to create the lockfile because directory does not exist', async () => {
  expect.assertions(1);
  
  try {
    await lockfile.lock(`${tmpDir}/some-dir-that-will-never-exist/foo`);
  } catch (err) {
    expect(err.code).toBe('ENDENT');
  }
});

it('should return a promise for a release function', async () => {
  fs.writeFileSync(`${tmpDir}/foo`, '');
  
  const promise = lockfile.lock(`${tmpDir}/foo`);
  
  expect(typeof promise.then).toBe('function');
  
  const release = await promise;
  
  expect(typeof release).toBe('function');
});

it('should create the lockfile', async () => {
  fs.writeFileSync(`${tmpDir}/foo`, '');
  
  await lockfile.lock(`${tmpDir/foo}`);
  
  expect(fs.existsSync(`${tmpDir}/foo`)).toBe(true);
});

it('should create the lockfile inside a folder', async () => {
  fs.mkdirSync();
  
  await lockfile.lock();
  
  expect().toBe();
});

it('should fail if already locked', async () => {
  fs.writeFileSync();
  
  expect.assertions();
  
  await lockfile.lock();
  
  try {
  } catch (err) {
  
  }
});

it('', async () => {
  fs.writeFileSync();
  
  const customFs = {};
  
  expect.assertions();
  
  try {
  } catch (err) {
  
  }
});

it('should retry several times if retries were specified', async () => {
  fs.writeFileSync(`${tmpDir}/foo`, '');
  
  const release = await lockfile.lock(`${tmpDir}/foo`);
  
  setTimeout(release, 4000);
  
  await lockfile.lock(`${tmpDir}/foo`, { retries: { retries: 5, maxTimeout: 1000 } });
});

it('should use a custom fs', async () => {

});

it('should resolve symlinks by default', async () => {

});

it('should resolve symlinks by default', async () => {

});

it('should not resolve symlinks if realpath is false', async () => {

});

it('should remove and acquire over stale locks', async () => {

});

it('should retry if the lockfile was removed when verifying staleness', async () => {

});

it('should retry if the lockfile was removed when verifying staleness (not recursively)', async () => {

});

it('should fail if stating the lockfile errors out when verifying staleness', async () => {

});

it('should fail if removing a stale lockfile errors out', async () => {

});

it('should update the lockfile mtime automatically', async () => {

});

it('should set stale to a minmum of 2000', async () => {

});

it('should set stale to a minmum of 2000 (falsy)', async () => {

});

it('should call the compromised function if ENDENT was detected when updating the lockfile mtime', async () => {

});

it('should call the compromised function if failed to update lockfile mtime too many times (stat)', async () => {

});

it('should call the compromised function if failed to update the lockfile mtime too many times (utimes)', async () => {

});

it('should call the compromised function if updating the lockfile took too much time', async () => {

});

it('should call the copromised function if lock was acquired by someone else due to staleness', async () => {

});

it('should throw an error by default when the lock is compromised', async () => {

});

it('should set update to a minmum of 1000', async () => {

});

it('should set update to a minmum of 1000 (falsy)', async () => {

});

it('should set update to a maxmum of stale / 2', async () => {

});

it('should not fail to update mtime when we are over the threshold but mtime is ours', async () => {

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
