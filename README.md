# mnist-draw-gradio

## MNIST Draw: from a custom CGI interface to Gradio

This repository brings together two implementations of the same demonstration: draw a digit (0–9) and display a model's classification scores. The later TensorFlow/Keras and Gradio implementation is at the repository root, alongside its Heroku deployment configuration. The earlier custom browser interface, TFLearn CNN, and CGI workflow are preserved under [legacy/mnist-draw](legacy/mnist-draw), with their original Git history.

**Historical demonstration; runtime unverified.** Training, local execution, and current hosted availability have not been verified. The checked-in dependencies and deployment files are legacy context. See the [Gradio setup and deployment notes](docs/legacy-setup.md) or the [CGI variant guide](legacy/README.md) for the preserved workflows. The two dependency stacks remain separate.

## Project background

- **2017–2019: custom browser and CGI application.** The earlier application builds on [rhammell/mnist-draw](https://github.com/rhammell/mnist-draw), whose retained July 2017 commits contain the TFLearn CNN and browser interface. Gawain's `mnist-draw` repository was created in January 2019. Its January 31 adaptation commit, recorded under `gawainchin1`, adds OpenCV resizing to 28 × 28 before inference and bundles MNIST data; the original CNN and interface remain credited to the upstream project.
- **2020: Keras and Gradio implementation.** The Gradio repository was created on August 22, 2020. Gawain Chin's implementation commit that day records a Keras `Flatten → Dense(128) → Dense(10)` model, Gradio drawing/results components, and Heroku process configuration. This changes both the model definition and the interface/deployment stack.
- **Consolidation: one portfolio repository.** Both variants now live here, with the legacy files unchanged and all 25 original legacy commits retained. The shared story documents the implementation choices and their history; runtime and model-quality comparisons remain unverified.

The [history notes](docs/history.md) record the repository dates and commit evidence behind this background.

## Historical interface example

This is the original animation embedded in the legacy application's README, showing its custom canvas and classification chart. The external URL is preserved exactly; its current availability has not been revalidated. It illustrates the historical CGI variant, not a verified current deployment or the later Gradio interface.

<p>
<img src="http://i.imgur.com/fmIa0e5.gif" width="600" alt="Original historical MNIST Draw CGI interface animation">
</p>

[Original animation link](http://i.imgur.com/fmIa0e5.gif) · [Unchanged original README](legacy/mnist-draw/README.md)

## Two implementations, one project story

| Aspect | Earlier CGI variant: `legacy/mnist-draw/` | Later Gradio variant: repository root |
| --- | --- | --- |
| Model definition | [TFLearn CNN](legacy/mnist-draw/cgi-bin/model.py): two convolution/pooling stages, followed by dense layers and a 10-class softmax output | [Keras sequential model](model.py): `Flatten(28 × 28)` → `Dense(128, relu)` → `Dense(10, softmax)` |
| Training | [TFLearn MNIST loader and training script](legacy/mnist-draw/cgi-bin/train.py), saving `models/model.tfl` relative to its working directory | [Keras MNIST loader and training script](model.py), saving `model/mnist_tf2.h5` and a best-validation checkpoint |
| Drawing interface | [Custom HTML canvas](legacy/mnist-draw/index.html) with Fabric.js and [JavaScript](legacy/mnist-draw/js/custom.js); an explicit Predict action and a D3 chart for all 10 scores | [Gradio Sketchpad and Label](app.py), configured with `live=True` and the top three classes |
| Inference | [CGI handler](legacy/mnist-draw/cgi-bin/mnist.py) decodes a posted image, inverts/normalizes pixels, resizes to 28 × 28, loads a TFLearn checkpoint, and returns JSON | [Python callback](app.py) passes the image supplied by Gradio to a Keras model loaded at application startup and returns a label-to-score dictionary |
| Serving and deployment | [Historical local CGI workflow](legacy/README.md), launched from the legacy variant's directory | [Procfile](Procfile) starts the app through [setup.sh](setup.sh), which sets Gradio's host and port for Heroku |

The CNN processes local image structure through convolution and pooling; the later dense model flattens the image before classification. This is a change in architecture, not evidence that either model is more accurate. The preserved implementations do not establish a shared benchmark for comparing accuracy, latency, or reliability on hand-drawn input.

The earlier implementation makes the browser controls, image preprocessing, and JSON request/response handling explicit. Gradio supplies the drawing and results components around a Python callback, reducing custom interface code while depending on the library's preprocessing and legacy API. Heroku's process configuration adds a hosted deployment workflow beyond the earlier local CGI instructions. These are implementation and deployment tradeoffs; the presence of deployment files does not verify a running service. Consolidation preserves these differences rather than connecting the two model stacks.

## Explore the later implementation

- [model.py](model.py) defines the network, loads MNIST, and contains training callbacks.
- [app.py](app.py) loads [model/mnist_tf2.h5](model/mnist_tf2.h5) and connects inference to the Gradio interface.
- [requirements.txt](requirements.txt) records the historical dependencies, including TensorFlow 2.0.0 and an unpinned Gradio dependency.
- [docs/legacy-setup.md](docs/legacy-setup.md) preserves installation, training, and Heroku notes with their legacy status.

The training script monitors validation loss and saves [model/mnist_tf2_best.h5](model/mnist_tf2_best.h5) as a best-validation checkpoint; the app loads `mnist_tf2.h5`. The scripts and bundled model files are preserved, and their runtime behavior has not been revalidated.

## Project history and attribution

The legacy application is a modified version of [rhammell/mnist-draw](https://github.com/rhammell/mnist-draw), as credited in its unchanged [original README](legacy/mnist-draw/README.md). The imported source snapshot and its 25 original commits retain that attribution and upstream ancestry. The comparison here describes observable differences without claiming exclusive authorship of the original application or a measured improvement in model quality.

See [docs/history.md](docs/history.md) for source repositories, pinned commits, history access, and preservation details. This repository is the consolidated portfolio entry point; the original repository URLs remain provenance references.
