# Historical TFLearn and CGI variant

The [mnist-draw](mnist-draw) directory preserves the earlier handwritten digit classification application: a custom browser canvas, a TFLearn CNN, and a Python CGI endpoint. It is a modified version of [rhammell/mnist-draw](https://github.com/rhammell/mnist-draw), as credited in its unchanged [original README](mnist-draw/README.md).

**Historical reference; runtime unverified.** The original 19 tracked files are retained byte-for-byte, including code, model checkpoints, MNIST data, dependencies, and interface assets. Setup, training, CGI compatibility, and application behavior have not been tested against current environments. Start with the [portfolio overview](../README.md) for the comparison with the root Gradio implementation, or [history notes](../docs/history.md) for provenance.

## Setup and working directory

Clone the consolidated repository, then enter the legacy variant's directory:

```bash
git clone https://github.com/gawainchin/mnist-draw-gradio.git
cd mnist-draw-gradio/legacy/mnist-draw
pip install -r requirements.txt
```

These are legacy instructions, not a verified installation recipe. Use a separate environment for this variant. Its [requirements.txt](mnist-draw/requirements.txt) remains separate from the root Keras/Gradio requirements and retains its original UTF-16 encoding.

The original README specified Python 3.5+ and asked users to select their Python 3 executable, giving `/Users/xxx/anaconda/bin/python3` as an example. Those notes are historical, not a verified compatibility range or a required path on another machine.

## Original local usage

From `legacy/mnist-draw/`, the original server command is:

```bash
python -m http.server --cgi 8000
```

The original workflow opens `http://localhost:8000/index.html`, draws a digit, and clicks **Predict**. [index.html](mnist-draw/index.html) and [js/custom.js](mnist-draw/js/custom.js) display all 10 classification scores in a D3 bar chart. **Clear** resets the canvas and chart. Historical notes advised allowing up to one minute for processing and described a warning icon and console messages for errors; no current timing has been measured.

Keep the working directory at `legacy/mnist-draw/` when starting the server. [cgi-bin/mnist.py](mnist-draw/cgi-bin/mnist.py) loads `cgi-bin/models/model.tfl` relative to that directory. Starting the CGI server from the consolidated repository root would not match this path assumption. The relative CSS, JavaScript, and CGI URLs in the original HTML and JavaScript remain unchanged.

The original [interface animation](http://i.imgur.com/fmIa0e5.gif) is retained as a historical external link in the imported README. It is not a new screenshot or evidence of a current working demo. The original Bootstrap, Font Awesome, jQuery, and D3 CDN URLs in the HTML also remain external dependencies.

## Model and training notes

[cgi-bin/model.py](mnist-draw/cgi-bin/model.py) defines the TFLearn CNN. [cgi-bin/train.py](mnist-draw/cgi-bin/train.py) loads MNIST through TFLearn and saves `models/model.tfl` relative to its working directory. From the consolidated repository root, the historical training layout is:

```bash
cd legacy/mnist-draw/cgi-bin
python train.py
```

Training remains unverified. The supplied checkpoint data, index, metadata, and [checkpoint pointer](mnist-draw/cgi-bin/models/checkpoint) are retained under [cgi-bin/models](mnist-draw/cgi-bin/models). The pointer file contains an original absolute Windows path; it has not been rewritten. The four original compressed MNIST files remain under [mnist](mnist-draw/mnist).

When **Predict** is clicked, the JavaScript posts a canvas data URL to the CGI script. That script decodes the image, inverts and normalizes pixels, resizes to 28 × 28 using OpenCV, loads the TFLearn checkpoint, and returns JSON predictions or an error. The root Gradio application uses its own Keras model and dependencies; the two variants are not combined into a shared runtime.
