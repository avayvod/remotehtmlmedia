# A proposal for remote playback API for the HTMLMediaElement

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
  attribute EventHandler onchange;

  // a complimentary field to the 
  readonly attribute boolean isRemote;

  // starts the remote playback from the current position; UA shows the device
  // picker; onchange will fire as if the UA would start the remote playback
  void start();

  // allows the page to stop the playback, local playback may continue from the
  // current position
  void stop();
}

partial interface HTMLSourceElement {
  // if true (by default) the src attribute can be used for remote playback; 
  // else, playing this source remotely is disabled.
  attribute boolean allowRemotePlayback=true;
}

```
