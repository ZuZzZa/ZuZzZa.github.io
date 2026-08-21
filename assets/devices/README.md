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

## Metadata policy (hard rule)

This is a public repo — every committed image MUST be stripped of all
metadata first. No EXIF (GPS location, device model, serial numbers,
timestamps), no XMP, no ICC, no thumbnails, no comments. This applies to
originals too: never commit a photo straight from a phone or camera,
even temporarily — git history keeps it forever.

Strip by re-encoding pixels only, e.g.:

    # Pillow
    from PIL import Image
    im = Image.open("in.jpg").convert("RGB")
    clean = Image.new("RGB", im.size); clean.paste(im)
    clean.save("out.jpg", quality=86, optimize=True)

    # or ImageMagick / exiftool
    magick in.jpg -strip out.jpg
    exiftool -all= -o out.jpg in.jpg

Verify before committing:

    exiftool out.jpg          # should show only size/format fields
    python3 -c "from PIL import Image; print(len(Image.open('out.jpg').getexif()))"   # 0
