# iframe-token-example
Example case on how to pass a confidential token to iframe contents in a somewhat secure way.

This case expects the token to be a single-use token.

## iframe sandbox
Whenever you activate the iframe sandbox, the origin of the framed page will be set to 'null'.
So it will not longer be possible to execute a `frame.contentWindow.postMessage(token, 'http://my-framed-origin');`.
If we use `frame.contentWindow.postMessage(token, '*');` however, it will work since we are broadcasting to everything in the frame.

The question here is what we think is the least of all evil:
1. Enable sandbox, preventing breakout from the framed page to our own, but having the token leaked to all of the framed contents origins.
2. Leave sandbox disabled, allowing breakout from the framed page but only sending the token to a single origin in the frame.
