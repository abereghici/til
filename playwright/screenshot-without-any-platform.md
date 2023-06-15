# Screenshot without any platform in screenshot name

Playwright automatically appends the platform name to the screenshot name, which
may not always be desirable, particularly when the CI platform is Linux while
the local environment is MacOS. As a result, the screenshot names differ between
CI and local setups, leading to test failures.

One way to solve this is to remove the platform name from the screenshot name.

```ts
export const configureSnapshotPath =
  () =>
  ({}: any, testInfo: TestInfo): void => {
    const originalSnapshotPath = testInfo.snapshotPath

    testInfo.snapshotPath = snapshotName => {
      const result = originalSnapshotPath
        .apply(testInfo, [snapshotName])
        .replace('.txt', '.json')
        .replace('-chromium', '')
        .replace('-linux', '')
        .replace('-darwin', '')

      return result
    }
  }
```

And use it like this:

```ts
test.beforeEach(configureSnapshotPath())
```
