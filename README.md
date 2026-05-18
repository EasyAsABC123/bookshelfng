# bookshelf

## Snapetech BookshelfNG fork

This public fork publishes SeerrNG-compatible images at:

    ghcr.io/snapetech/bookshelfng:softcover
    ghcr.io/snapetech/bookshelfng:hardcover

The `softcover` image includes a compatibility fix for SeerrNG and other
Readarr-compatible clients: `/api/v1/book/lookup` returns nested author and
edition metadata when Bookshelf can resolve it. Without that fix, softcover
lookups can return `editions: []` even when they include `foreignEditionId`,
which makes downstream book-add calls unreliable.

Use `softcover` when migrating an existing Readarr-compatible database. Use
`hardcover` only for a fresh deployment that is prepared for Hardcover metadata.

Image tags are published by GitHub Actions:

- `softcover`
- `softcover-v0.4.20`
- `softcover-v0.4.20.<run-number>`
- `hardcover`
- `hardcover-v0.4.20`
- `hardcover-v0.4.20.<run-number>`

If anonymous `docker pull ghcr.io/snapetech/bookshelfng:softcover` returns
`denied`, the GHCR package visibility still needs to be changed to public in
GitHub package settings, or Docker needs to be authenticated with package read
access.

## Upstream project

This is a revival of [Readarr](https://github.com/Readarr/Readarr). The images
published are configured to use working Goodreads or Hardcover metadata out of
the box.

Bookshelf is an ebook and audiobook collection manager for Usenet and BitTorrent
users. It can monitor multiple RSS feeds for new books from your favorite
authors and will grab, sort, and rename them. Note that only one type of a
given book is supported. If you want both an audiobook and ebook of a given
book you will need multiple instances.

## Getting Started

The container listens on port 8787 and expects a volume mounted at `/config`.

    docker run -p 8787:8787 -v ~/.config/bookshelf:/config ghcr.io/pennydreadful/bookshelf:hardcover

The `softcover` tags use [Goodreads](https://www.goodreads.com) as the metadata
provider. The quality of this metadata is generally poor and contains a lot of
slop. However, it is backward-compatible with existing Readarr databases and
functionality like Goodreads list imports should continue to work normally.

The `hardcover` tags use [Hardcover](https://hardcover.app/home) as a metadata
provider. This metadata is higher quality but isn't backward-compatible; if
you're already running Readarr you'll need to redeploy this from scratch.
Goodreads list imports haven't been tested and likely don't work.

## Support

This project won't use Discord for support. If you have a problem please file
an issue or start a discussion.

## Contributors & Developers

Help is very welcome. Priority is on fixing quality of life issues

- [ ] Monitor series.
- [ ] Support ebook and audio files in the same root.

Already done

- [x] Native support for MyAnonaMouse without Prowlarr.
- [x] Hardcover list import.
- [x] Improved matching.
- [x] Metadata is no longer cached locally.
- [x] Removed servarr analytics spyware.
- [x] Supports selfhosted metadata (UI or `METADATA_URL` env var).

## Sponsors

If you ever donated to [this](https://opencollective.com/readarr) project you
should request a refund. Those people don't deserve your money.

### License

The is a derivative work of the [Readarr](https://github.com/Readarr/Readarr)
and [Prowlarr](https://github.com/Prowlarr/Prowlarr) projects which are both
licensed [GPLv3](http://www.gnu.org/licenses/gpl.html). This project is
therefore also licensed under the terms of GPLv3.

Copyright 2025-2026
