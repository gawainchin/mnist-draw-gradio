# Project history and preservation

This repository consolidates the two MNIST Draw implementations into one portfolio entry point. The later Keras/Gradio variant remains at the root. The earlier TFLearn/CGI variant is retained under [legacy/mnist-draw](../legacy/mnist-draw); see its [guide](../legacy/README.md) for historical working-directory and setup notes. Runtime, training, and hosted availability remain unverified.

## Source snapshots

| Variant | Original source | Published snapshot used |
| --- | --- | --- |
| Later Keras/Gradio | [gawainchin/mnist-draw-gradio](https://github.com/gawainchin/mnist-draw-gradio) | `b9790fc087bc304184ac4f4076035ce224fad627` |
| Earlier TFLearn/CGI | [gawainchin/mnist-draw](https://github.com/gawainchin/mnist-draw) | `4d4dbf2ec0331e06d7d67c386a84078a7efb4d31` |

The earlier application is a modified version of [rhammell/mnist-draw](https://github.com/rhammell/mnist-draw), as credited in the imported [original README](../legacy/mnist-draw/README.md). Its history includes upstream commits by Bob Hammell. The later implementation's checked-in model definition, interface, and deployment files differ from that legacy application; this documentation makes no claim of exclusive authorship of the original concept or a measured improvement in model quality.

## Evolution evidence

The README's background is grounded in GitHub repository creation metadata and the preserved commit records:

| Stage | Recorded evidence | Observable change |
| --- | --- | --- |
| Upstream application, July 2017 | Bob Hammell's `1e4497e67f211bd9a2a3dcc226fd5076d5b055b6`, dated July 11, 2017 | Adds the custom browser application, TFLearn CNN, training script, and CGI inference handler |
| Gawain's earlier repository, January 2019 | Repository created January 31, 2019; `56e2d47afe516bc6683d242e716b7e8e330b620d`, authored as `gawainchin1` that day | Adds OpenCV resizing to 28 × 28 in the CGI inference path and the four compressed MNIST files, alongside other uploaded changes |
| Gradio implementation, August 2020 | Repository created August 22, 2020; `97282cf45f78b8ad45307d8f368475549e8932dd`, authored by Gawain Chin that day | Records the Keras Flatten/Dense model definition, Gradio app, model artifacts, dependencies, and Heroku process files |
| Consolidation | Unsquashed subtree merge `1651bf2e186fc63f4effcfa1fb504a335c87cb07` | Places the unchanged earlier snapshot under the legacy prefix while retaining its original ancestry |

The imported history predates the creation of Gawain's earlier GitHub repository; those upstream dates should not be read as the creation date of his repository or as his authorship of the original CNN/interface. The commit evidence describes checked-in changes, not their motivation, originality, measured accuracy, or successful deployment. The later model definition is a dense network, separate from the legacy CNN.

These records can be inspected without running the applications:

```bash
git show --stat 1e4497e67f211bd9a2a3dcc226fd5076d5b055b6
git show 56e2d47afe516bc6683d242e716b7e8e330b620d -- cgi-bin/mnist.py
git show --stat 97282cf45f78b8ad45307d8f368475549e8932dd
```

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

The unchanged imported README retains its original clone/setup URLs, TFLearn documentation URL, and external Imgur animation at `http://i.imgur.com/fmIa0e5.gif`. The [canonical overview](../README.md) also embeds that exact URL as a labeled historical CGI interface example. Neither source snapshot contains a standalone tracked screenshot or animation file, and the original Gradio README has no image embed. The animation's current availability remains unverified; no replacement screenshot or unrelated image has been added.

Treat the imported setup instructions as historical source material; the [legacy guide](../legacy/README.md) gives the consolidated clone location and working directories. The [Gradio setup notes](legacy-setup.md) retain the historical Heroku URL with its current availability unverified. Original CDN dependencies remain unchanged.

Original repository URLs remain provenance references. Importing Git commits does not migrate GitHub issues, PRs, releases, stars, permissions, or other service metadata, and does not redirect existing links. Whether the predecessor repository is retained, archived, or deleted is a separate decision; consolidation itself does not change either remote's state.
