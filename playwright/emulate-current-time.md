# Emulate current time

This feature is crucial for visual regression testing when a component relies on
the current time to render its output.

For instance, consider a calendar component used for selecting date ranges.
Without the ability to mock the current time, the component would produce
varying results each month. This inconsistency poses challenges for conducting
visual regression tests since updating the snapshots on a monthly basis is
inconvenient and undesirable.

This snippet can be used to mock the current time:

```ts
export async function setDate(page: Page, date: string): Promise<void> {
  const fakeDate = new Date(date).getTime()
  page.evaluate(`
        Date = class extends Date {
          constructor(...args) {
            if (args.length === 0) {
              super(${fakeDate});
            } else {
              super(...args);
            }
          }
        };
        const __DateNowOffset =
        ${fakeDate} - Date.now();
        const __DateNow = Date.now;
        Date.now = () => __DateNow() + __DateNowOffset;
        `)
}
```

It can be used like this:

```ts
test('calendar', async ({page}) => {
  page.on('load', () => {
    setDate(page, 'November 14 2022 13:37:11')
  })
})
```
