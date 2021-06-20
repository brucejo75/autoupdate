## Autoupdate "Other" Client hook
There is a new API `AutoupdateHookOtherClient(appId, autoUpdate)`.

Using this API you can force autoupdates to "other" clients with DDP connections to this server.

`AutoupdateHookOtherClient` can set the `autoupdate` parameters of a meteor application with a specific `appId`.  Once these values have been set each of the connected instances with that `appId` will be notified that there is an update available via DDP.

- `appId` - the id of the application.  This can be found in the file `.meteor/.id`.
- `autoUpdate` - the autoupdate versions for each architecture.  The schema:
```javascript
{
  "versions": {
    "web.browser": {
      "version": "<String>",
      "versionNonRefreshable": "<String>",
      "versionRefreshable": "<String>",
      "versionReplaceable": "<String>",
    },
    "web.browser.legacy": {
      "version": "<String>",
      "versionNonRefreshable": "<String>",
      "versionRefreshable": "<String>",
      "versionReplaceable": "<String>",
    }
    "web.cordova": {
      "version": "<String>",
      "versionNonRefreshable": "<String>",
      "versionRefreshable": "<String>",
      "versionReplaceable": "<String>",
    }
  }
}
```

### Note
This feature was originally developed to support the `meteor-static-clients` program.  To facilitate working with `meteor-static-clients` there is a meteor package `autoupdate-static` which will monitor the `autoupdate.json` file emitted by `meteor-static-clients`.  When it detects a change it will call `AutoupdateHookOtherClient` with the parameters needed.
