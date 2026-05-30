# Discovery

In this file, I'll write about my discoveries when trying to understand and debug how
Infuse interacts with Jellyfin.

## Correct Endpoint

I intercepted the network traffic between Infuse and Jellyfin using `tcpdump` and analyzed
it with [Wireshark](https://www.wireshark.org/). In that, I discovered that Infuse uses the
Jellyfin API endpoint `/UserItems/Resume` to fetch the top-row content.

While the Jellyfin web UI uses these two endpoints to fetch the Continue Watching and Next Up items:
  - `/Users/{id}/Items/Resume` — Continue Watching
  - `/Shows/NextUp` — Next Up

Infuse uses another endpoint for `Continue Watching`:
  - `/UserItems/Resume` — Continue Watching

So what I did was to create a middleware for that specific endpoint that Infuse uses. That
way, only Infuse is affected by the plugin.
