# Project history and preservation

This repository consolidates the two MNIST Draw implementations into one portfolio entry point. The later Keras/Gradio variant remains at the root. The earlier TFLearn/CGI variant is retained under [legacy/mnist-draw](../legacy/mnist-draw); see its [guide](../legacy/README.md) for historical working-directory and setup notes. Runtime, training, and hosted availability remain unverified.

## Source snapshots

| Variant | Original source | Published snapshot used |
| --- | --- | --- |
| Later Keras/Gradio | [gawainchin/mnist-draw-gradio](https://github.com/gawainchin/mnist-draw-gradio) | `b9790fc087bc304184ac4f4076035ce224fad627` |
| Earlier TFLearn/CGI | [gawainchin/mnist-draw](https://github.com/gawainchin/mnist-draw) | `4d4dbf2ec0331e06d7d67c386a84078a7efb4d31` |

The earlier application is a modified version of [rhammell/mnist-draw](https://github.com/rhammell/mnist-draw), as credited in the imported [original README](../legacy/mnist-draw/README.md). Its history includes upstream commits by Bob Hammell. The later implementation's checked-in model definition, interface, and deployment files differ from that legacy application; this documentation makes no claim of exclusive authorship of the original concept or a measured improvement in model quality.

All 19 files from the earlier published snapshot are imported unchanged, including its original README, dependency encoding, TFLearn model artifacts, compressed MNIST data, vendored browser asset, and tracked Python bytecode. The later variant's original source, dependency, deployment, and model files remain unchanged. Neither source snapshot includes a repository-level LICENSE file. Existing files and any notices are preserved; consolidation does not assign a new license.

## Original Git history

The legacy snapshot was imported using `git subtree add --prefix=legacy/mnist-draw` without squashing. The import joins the original tip as a second parent, retaining all 25 original commit IDs and their ancestry. The original source trees still use their original root paths; the import commit places the snapshot under the legacy prefix in the consolidated working tree.

The annotated tag `legacy-mnist-draw-original-4d4dbf2` identifies the unchanged source tip. In a full clone containing the import, original history can also be inspected directly by its pinned SHA:

```bash
# Original CGI changes before consolidation
git log 4d4dbf2ec0331e06d7d67c386a84078a7efb4d31 -- cgi-bin/mnist.py

# Inspect the original README at its original root path
git show 4d4dbf2ec0331e06d7d67c386a84078a7efb4d31:README.md

# Confirm the original tip is retained in the consolidated ancestry
git merge-base --is-ancestor 4d4dbf2ec0331e06d7d67c386a84078a7efb4d31 HEAD
```

The history view for the new `legacy/mnist-draw/` prefix may begin at the import. Use the original SHA and original paths to inspect earlier changes. A shallow clone may omit the historical commits.

To preserve this ancestry when publishing the consolidation, use a **merge commit**, rather than squash or rebase merging. Squash or rebase would not retain the imported original ancestry on the canonical branch. The source tag should be published explicitly if used as a public reference. No existing published commits are rewritten by this import.

## Historical links and repository context

The unchanged imported README retains its original clone/setup URLs, TFLearn documentation URL, and external Imgur animation. Treat those instructions as historical source material; the [legacy guide](../legacy/README.md) gives the consolidated clone location and working directories. The [Gradio setup notes](legacy-setup.md) retain the historical Heroku URL with its current availability unverified. Original CDN dependencies remain unchanged.

Original repository URLs remain provenance references. Importing Git commits does not migrate GitHub issues, PRs, releases, stars, permissions, or other service metadata, and does not redirect existing links. Whether the predecessor repository is retained, archived, or deleted is a separate decision; consolidation itself does not change either remote's state.
