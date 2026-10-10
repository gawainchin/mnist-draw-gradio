# mnist-draw-gradio

## MNIST Draw: from a custom CGI interface to Gradio

This repository is the main portfolio overview for two implementations of the same demonstration: draw a digit (0–9) and display a model's classification scores. The [earlier `mnist-draw` repository](https://github.com/gawainchin/mnist-draw) preserves the custom browser interface, TFLearn CNN, and CGI workflow. This later implementation uses a TensorFlow/Keras dense network, a Gradio sketchpad, and Heroku deployment configuration. Both repositories retain their own code and Git histories.

**Historical demonstration; runtime unverified.** Training, local execution, and current hosted availability have not been verified. The checked-in dependencies and deployment files are legacy context. See the [original setup and deployment workflow](docs/legacy-setup.md) for the preserved commands and historical demo URL.

## Two implementations, one project story

| Aspect | Earlier: `mnist-draw` | Later: `mnist-draw-gradio` |
| --- | --- | --- |
| Model definition | [TFLearn CNN](https://github.com/gawainchin/mnist-draw/blob/master/cgi-bin/model.py): two convolution/pooling stages, followed by dense layers and a 10-class softmax output | [Keras sequential model](model.py): `Flatten(28 × 28)` → `Dense(128, relu)` → `Dense(10, softmax)` |
| Training | [TFLearn MNIST loader and training script](https://github.com/gawainchin/mnist-draw/blob/master/cgi-bin/train.py), saving `models/model.tfl` | [Keras MNIST loader and training script](model.py), saving `model/mnist_tf2.h5` and a best-validation checkpoint |
| Drawing interface | [Custom HTML canvas](https://github.com/gawainchin/mnist-draw/blob/master/index.html) with Fabric.js and [JavaScript](https://github.com/gawainchin/mnist-draw/blob/master/js/custom.js); an explicit Predict action and a D3 chart for all 10 scores | [Gradio Sketchpad and Label](app.py), configured with `live=True` and the top three classes |
| Inference | [CGI handler](https://github.com/gawainchin/mnist-draw/blob/master/cgi-bin/mnist.py) decodes a posted image, inverts/normalizes pixels, resizes to 28 × 28, loads a TFLearn checkpoint, and returns JSON | [Python callback](app.py) passes the image supplied by Gradio to a Keras model loaded at application startup and returns a label-to-score dictionary |
| Serving and deployment | Original local workflow: `python -m http.server --cgi 8000` | [Procfile](Procfile) starts the app through [setup.sh](setup.sh), which sets Gradio's host and port for Heroku |

The CNN processes local image structure through convolution and pooling; the later dense model flattens the image before classification. This is a change in architecture, not evidence that either model is more accurate. The repositories do not establish a shared benchmark for comparing accuracy, latency, or reliability on hand-drawn input.

The earlier implementation makes the browser controls, image preprocessing, and JSON request/response handling explicit. Gradio supplies the drawing and results components around a Python callback, reducing custom interface code while depending on the library's preprocessing and legacy API. Heroku's process configuration adds a hosted deployment workflow beyond the earlier local CGI instructions. These are implementation and deployment tradeoffs; the presence of deployment files does not verify a running service.

## Explore the later implementation

- [model.py](model.py) defines the network, loads MNIST, and contains training callbacks.
- [app.py](app.py) loads [model/mnist_tf2.h5](model/mnist_tf2.h5) and connects inference to the Gradio interface.
- [requirements.txt](requirements.txt) records the historical dependencies, including TensorFlow 2.0.0 and an unpinned Gradio dependency.
- [docs/legacy-setup.md](docs/legacy-setup.md) preserves installation, training, and Heroku notes with their legacy status.

The training script monitors validation loss and saves [model/mnist_tf2_best.h5](model/mnist_tf2_best.h5) as a best-validation checkpoint; the app loads `mnist_tf2.h5`. The scripts and bundled model files are preserved, and their runtime behavior has not been revalidated.

## Project history and attribution

The [earlier repository](https://github.com/gawainchin/mnist-draw) is a modified version of [rhammell/mnist-draw](https://github.com/rhammell/mnist-draw), as credited in its original README. Its upstream history and attribution remain part of this project story. The comparison here describes observable differences between the checked-in implementations without claiming exclusive authorship of the original application or a measured improvement in model quality.
