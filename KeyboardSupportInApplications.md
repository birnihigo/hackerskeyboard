# Introduction #

This page is intended for developers who want to support the additional keys offered by Hacker's Keyboard in their application, as mentioned in FrequentlyAskedQuestions. Doing so is equivalent to supporting an external physical keyboard connected via USB or Bluetooth, so if you make the suggested changes your application should work with both.

## Enabling additional key support ##

Starting with Honeycomb (3.0), Android supports a full set of keycodes for key events: http://developer.android.com/reference/android/view/KeyEvent.html

Note that your application doesn't need to require Honeycomb to support these key events. Hacker's keyboard sends the corresponding numeric keycodes on all supported systems (>= 2.2), and you can manually handle these codes in your application while still building with an earlier SDK version.

See for example this [patch](http://code.google.com/p/android-vnc-viewer/issues/attachmentText?id=238&aid=2380001000&name=patch-android-vnc-viewer-extra-keys.diff&token=09e6531c6b7f55ac54723f4edf4103f1) for Android VNC Viewer's [issue 238](http://code.google.com/p/android-vnc-viewer/issues/detail?id=238):

```
  public boolean onKeyDown(int keyCode, KeyEvent evt) {
    switch (keyCode) {
    //...
    // Previously supported keys
    case KeyEvent.KEYCODE_DEL:           // ...
    case KeyEvent.KEYCODE_ENTER:         // ...
    case KeyEvent.KEYCODE_DPAD_CENTER:   // ...

    // new keys available in the 2.2 SDK:
    case KeyEvent.KEYCODE_TAB:           // ...
    case KeyEvent.KEYCODE_ALT_LEFT:      // ...
    case KeyEvent.KEYCODE_ALT_RIGHT:     // ...

    // new keys added in the 3.0 SDK:
    case 92 /* KEYCODE_PAGE_UP */:       // ...
    case 93 /* KEYCODE_PAGE_DOWN */:     // ...
    case 111 /* KEYCODE_ESCAPE */:       // ...
    case 112 /* KEYCODE_FORWARD_DEL */:  // ...
    case 113 /* KEYCODE_CTRL_LEFT */:    // ...
    //[...]
    case 122 /* KEYCODE_MOVE_HOME */:    // ...
    case 123 /* KEYCODE_MOVE_END */:     // ...
    case 124 /* KEYCODE_INSERT */:       // ...
    case 131 /* KEYCODE_F1 */:           // ...
    //[...]
    case 142 /* KEYCODE_F12 */:          // ...
```