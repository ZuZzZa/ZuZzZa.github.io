# Device photos

Drop device photos here, one folder per device id:

    assets/devices/<device-id>/01.jpg
    assets/devices/<device-id>/02.jpg

Then list them in `data.json` under that project:

    "photos": [
      { "src": "assets/devices/<device-id>/01.jpg", "alt": "Short caption" },
      { "src": "assets/devices/<device-id>/02.jpg", "alt": "Short caption" }
    ]

The first photo is used as the cover on `#/devices`.
Recommended: landscape, 16:9 or 16:10, ~1600px wide, JPEG under ~400 KB.
An empty `photos` array simply renders the placeholder tile.
