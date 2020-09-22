## Jest-Puppeteer-Starter

#### Configuration

1. setup dev server if necessary

   - uncomment the server options and edit `port` in `jest-puppeteer.config.js`
   - edit `testUrl` in `jest.config.js`
   - setup `server.js`

2. disable headless mode, `HEADLESS=false yarn test`

#### Features

- github actions
- snapshot on error, in `./__snapshot`
- custom matchers
  - create new matcher
    1. create a file in `matchers`.
    2. export your matcher and `expect.extend`
    3. export the file in `matchers/index.ts`
    ```typescript
    export(firstArg).newMatcher(...someArgs)
    ```
  - `matchers/goto.ts`
    ```
    expect(page).goto('/pathname-relative-to-testUrl')
    ```
- utils

  - `utils/socket.ts` handle socket lifecycle
  - `utils/newPage.ts` helper for open newPage

  ```typescript
  const createNewPage = newPageHelper('/pathname');
  const page = await createNewPage();
  await page.waitforNavigation();
  // ... some actions
  // remember to close the new page and context
  await page.close();
  await page.browserContext().close();

  // or pass the an async function
  // this will close the new page and context automatically
  await createNewPage(async () => {
    // some actions here
    //
  });
  ```
