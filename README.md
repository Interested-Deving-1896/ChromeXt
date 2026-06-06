[update-readmes]   Mode: rewrite — migrating to template structure...
# ChromeXt

[![Built with Ona](https://ona.com/build-with-ona.svg)](https://app.ona.com/#https://github.com/Interested-Deving-1896/ChromeXt)

<!-- AI:start:what-it-does -->
_Description pending._
<!-- AI:end:what-it-does -->

## Architecture

<!-- AI:start:architecture -->
_Architecture documentation pending._
<!-- AI:end:architecture -->

## Install

<!-- Add installation instructions here. This section is yours — the AI will not modify it. -->

```bash
git clone https://github.com/Interested-Deving-1896/ChromeXt.git
cd ChromeXt
```

## Usage


<p align="center"><a href="https://www.youtube.com/watch?v=1Qm4dU-XnJM"><img src="https://img.youtube.com/vi/1Qm4dU-XnJM/0.jpg" /></a></p>

ChromeXt requires **Xposed framework**.

For root users, install [LSPosed](https://github.com/JingMatrix/LSPosed) first,
pick up the latest built APK from my repo's [GitHub Actions](https://github.com/JingMatrix/ChromeXt/actions) and install it.

For non-root users,
I modify a bit [LSPatch](https://github.com/JingMatrix/LSPatch) to support `ChromeXt`; here is how to use it:
1. Download the latest `lspatch-release` from my [GitHub Actions](https://github.com/JingMatrix/LSPatch/actions).
2. Download the latest `ChromeXt.apk` from my [GitHub Actions](https://github.com/JingMatrix/ChromeXt/actions).
3. Extract previously downloaded files to get files `lspatch.jar` (with some suffix) and `ChromeXt-signed.apk`.
4. Patch your APK (taking `arm64_ChromePublic.apk` as example) using the following command: `java -jar lspatch.jar arm64_ChromePublic.apk -d -v -m ChromeXt-signed.apk --force --injectdex`. If `java` environment is not available, please consider using the provided `manager` APK (and check the `Inject loader dex` option).
5. Install the patched APK, which might require you to first uninstall the one on your devices.

Notes: currently _to download_ files from `GitHub Actions`, one needs to log in GitHub.

The author uploads releases to [Xposed-Modules-Repo](https://github.com/Xposed-Modules-Repo/org.matrix.chromext/releases) when needed, but not that frequently.

You can then install UserScripts from popular sources: URLs that ends with `.user.js`.

### Supported API

Currently, ChromeXt supports almost all [Tampermonkey APIs](https://www.tampermonkey.net/documentation.php?locale=en):

1. @name (colons not allowed), @namespace, @description and so on
2. @match (conform to the [Chrome Standard](https://developer.chrome.com/docs/extensions/mv2/match_patterns/), supports [regular expressions](https://developer.android.com/reference/java/util/regex/Pattern))
3. @include = @match, @exclude
4. @run-at: document-start, document-end, document-idle (the default and fallback value)
5. @grant: GM_addStyle, GM_addElement, GM_xmlhttpRequest, GM_openInTab, GM_registerMenuCommand (shown in the `Resources` panel of eruda), GM_unregisterMenuCommand, GM_download, unsafeWindow (= window)
6. @grant: GM_setValue, GM_getValue (less powerful than GM.getValue), GM_listValues, GM_addValueChangeListener, GM_removeValueChangeListener, GM_setClipboard, GM_cookie, GM_notification, window.close
7. @require, @resource (without [Subresource Integrity](https://www.tampermonkey.net/documentation.php#api:Subresource_Integrity))
8. @inject-into, @sandox: by default, imported scripts using `@require` can define/overwrite global JavaScript objects; one can set `@inject-into content` or `@sandbox DOM` to disable this behavior
9. @noframes: note that, to load UserScripts for frames, there must be a script with `@grant frames` on the main page

These APIs are implemented differently from the official ones, please refer to the source files
[Local.kt](app/src/main/java/org/matrix/chromext/script/Local.kt) and
[GM.js](app/src/main/assets/GM.js) if you have doubts or questions.

Moreover, there is the powerful (also dangerous) `GM.ChromeXt` API, which must be declared by `@grant GM.ChromeXt` to _unlock_ its usage.
It is locked by default so that the users are protected from malicious UserScripts exploiting ChromeXt.
This API allows scripts to use the JavaScript method `ChromeXt.dispatch(action, payload)`, which is fundamental to implement other APIs. (Hence, one can find usage examples in [GM.js](app/src/main/assets/GM.js)).
Dispatched `action` and `payload` are handled by [Listener.kt](app/src/main/java/org/matrix/chromext/Listener.kt).

### UserScripts manager front end

To manage scripts installed by `ChromeXt`, here are a simple front end hosted on [github.io](https://jingmatrix.github.io/ChromeXt/) and two mirrors of it (in case that you have connection issues): [onrender.com](https://jianyu-ma.onrender.com/ChromeXt/), [netlify.app](https://jianyu-ma.netlify.app/ChromeXt/).

### Edit scripts before installing them

If you cancel the prompt of installing a new UserScript, then you can edit it directly in Chrome.
Use the `Install UserScript` page menu to install your modified UserScript.

### DevTools for developers

From the three dots page menu, ChromeXt offers you the
1. `Developer tools` menu for the UserScript manager front end,
2. `Eruda console` menu for other pages.

~~For `Edge` browser, these menus are moved to the page info menu,
which locates at the left corner inside the URL input bar.~~

For WebView based browsers and _Samsung Internet_, these menu items are presented in the context menu.

## Configuration

<!-- Document configuration options here. This section is yours — the AI will not modify it. -->

## CI

<!-- AI:start:ci -->
_CI documentation pending._
<!-- AI:end:ci -->

## Mirror chain

<!-- AI:start:mirror-chain -->
This repo is maintained in [`Interested-Deving-1896/ChromeXt`](https://github.com/Interested-Deving-1896/ChromeXt) and mirrored through:

```
Interested-Deving-1896/ChromeXt  ──►  OpenOS-Project-OSP/ChromeXt  ──►  OpenOS-Project-Ecosystem-OOC/ChromeXt
```

Changes flow downstream automatically via the hourly mirror chain in
[`fork-sync-all`](https://github.com/Interested-Deving-1896/fork-sync-all).
Direct commits to OSP or OOC are detected and opened as PRs back to `Interested-Deving-1896`.
<!-- AI:end:mirror-chain -->

## Contributors

<!-- AI:start:contributors -->
_Contributors pending._
<!-- AI:end:contributors -->

## Origins

<!-- AI:start:origins -->
_Original project — no upstream fork._
<!-- AI:end:origins -->

## Resources

<!-- AI:start:resources -->
_No additional resource files found._
<!-- AI:end:resources -->

## License

<!-- AI:start:license -->
[GPL-3.0](https://github.com/Interested-Deving-1896/ChromeXt/blob/master/LICENSE) © 2026 [Interested-Deving-1896](https://github.com/Interested-Deving-1896)
<!-- AI:end:license -->
