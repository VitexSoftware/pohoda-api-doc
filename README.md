# pohoda-api-doc
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
![Packaging: deb](https://img.shields.io/badge/packaging-.deb-red?logo=debian&logoColor=white)

A standalone, Sphinx-built reference guide for the **integration interfaces
of Stormware Pohoda** — XML import/export (`dataPack` / `responsePack`), the
**mServer** HTTP server and the **SQL database** — not any particular client
library. Compiled from the Stormware XSD schemas and the official
documentation at [stormware.cz/pohoda/xml](https://www.stormware.cz/pohoda/xml/),
and cross-checked against the reference client libraries:

- [riesenia/pohoda](https://github.com/riesenia/pohoda) (`php-pohoda-xml`)
- [php-vitexsoftware-pohoda-connector](https://github.com/VitexSoftware/PHP-Pohoda-Connector)
- [php-vitexsoftware-pohodaser](https://github.com/VitexSoftware/php-vitexsoftware-pohodaser)
- [php-spojenet-pohoda-sql](https://github.com/Spoje-NET/PohodaSQL)

Available in two languages, each producing its own Debian package:

- `cs/` → `pohoda-api-doc-cs` (Czech)
- `en/` → `pohoda-api-doc-en` (English)

Examples throughout use XML, the native format of the interface. Statements
not verified against an official source are marked *unverified* in the text.

## Building the HTML docs

```bash
pip install sphinx shibuya   # or: apt install python3-sphinx python3-shibuya-sphinx-theme
sphinx-build -b html cs cs/_build
sphinx-build -b html en en/_build
```

## Building the Debian packages

```bash
dpkg-buildpackage -us -uc -b
```

Produces `pohoda-api-doc-cs` and `pohoda-api-doc-en`, each installing its
HTML output to `/usr/share/doc/pohoda-api-doc-{cs,en}/html`, with an Apache2
config snippet enabled automatically and an Nginx snippet provided for
reference. See [`debian/Jenkinsfile`](debian/Jenkinsfile) for CI.

## Testing

```bash
./tests/test_docs_build.sh
```

Builds both `cs/` and `en/` with `-W` (warnings are errors) and checks that
both language trees have the same number of chapters.

## License

MIT — see [LICENSE](LICENSE). This is an independent compiled reference, not
an official publication of STORMWARE s.r.o.
