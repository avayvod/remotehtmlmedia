# A proposal for remote playback API for the HTMLMediaElement

[A flow supported by Chrome on Android for default controls](http://avayvod.github.io/chrome-android-remote-playback.pdf)

```js

// |remote| gathers all remote playback related methods together.
partial interface HTMLMediaElement {
  attribute RemotePlayback remote;
};

interface RemotePlayback : EventTarget {
  // allow the page to be notified if it should show remote playback UI
  Promise<Availability> getAvailability();

  // notifies the page when the media starts or stops playing remotely;
  // also called if the browser initiates the remote playback
  attribute EventHandler onstatechange;

  // a complimentary field to the |onstatechange| event.
  readonly attribute PresentationSessionState state;

  // starts the remote playback from the current position; UA shows the device
  // picker; onchange will fire as if the UA would start the remote playback
  Promise start();

  // allows the page to stop the playback, local playback may continue from the
  // current position
  Promise stop();
}

partial interface HTMLSourceElement {
  // if false (by default) the src attribute can be used for remote playback; 
  // else, playing this source remotely is disabled.
  attribute boolean disallowRemotePlayback=false;
}

```
