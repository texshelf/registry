# texshelf registry

This repository lists every template that `texshelf` and `typshelf` can
install. It holds no template files. Each template version is one manifest at
`templates/<name>/<version>.toml` that points at a commit in the author's own
repository.

Browse the result at [tex.jjsm.science](https://tex.jjsm.science).

## Add a template

1. Copy the manifest of a similar template to `templates/<name>/<version>.toml`.
2. Fill it in. `source.rev` has to be a full commit hash, and the license has
   to allow redistribution.
3. Run `texshelf validate templates/<name>/<version>.toml`.
4. Open a pull request.

The [manifest reference](https://github.com/texshelf/docs/blob/main/docs/manifest.md)
describes every field, and the
[publishing guide](https://github.com/texshelf/docs/blob/main/docs/publishing.md)
covers updates and local testing.

To update a template, add a new version file. Published versions are not
edited, so a project created last month can be recreated exactly.

## What CI does

On a pull request and on every push to `main`, `audit.yml` scans the template
files for risky content without compiling them: compiled programs, scripts,
shell commands, paths outside the template folder and leaked keys. A serious
finding fails the run. The result is also stored with each built version and
shown on the template's page, with a link to the full log.

On a pull request, `check.yml` also validates every manifest, then fetches and
compiles the templates the pull request touches, in a full TeX Live container
with shell-escape off. The PDFs and thumbnails are uploaded as an artifact for
review. Pull requests from forks run without secrets.

On a push to `main`, `publish.yml` calls the deploy workflow in
[texshelf/web](https://github.com/texshelf/web). That workflow builds the
archives, previews and `index.json` with `texshelf-registry`, builds the site,
and publishes both to tex.jjsm.science. Versions that have not changed are
reused from the previous run instead of being compiled again.

## The starting set

The first templates were imported to give the tooling something real to work
on: a CV, a résumé, a preprint, a homework sheet, a poster, a thesis, three
Typst templates from the Typst team, and the TeX-AST lab report. Each one
credits its authors and keeps its license. The `article`, `slides`, `letter`,
`book`, `article-typst` and `notes-typst` templates are maintained in
[texshelf/templates](https://github.com/texshelf/templates).

If you are the author of an imported template and want it changed or removed,
open an issue and it will be done.

## Taking part

Not sure whether a template fits, or you know one but it is not yours? Open a
[template request](https://github.com/texshelf/registry/issues/new/choose).
The [contributing guide](https://github.com/texshelf/.github/blob/main/CONTRIBUTING.md)
has the rest, and everyone taking part follows the
[code of conduct](https://github.com/texshelf/.github/blob/main/CODE_OF_CONDUCT.md).

## License

The manifests in this repository are released under CC0 1.0. The templates
they point to are not part of this repository and keep their own licenses.
