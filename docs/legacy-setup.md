# Legacy setup and deployment notes

**Historical reference; runtime unverified.** These notes preserve the original Gradio installation, training, and Heroku workflow. They have not been tested against a current Python environment, current package releases, or a current Heroku service. Return to the [portfolio overview](../README.md), or see the separate [CGI variant guide](../legacy/README.md).

Run the Gradio commands from the repository root in its own environment. The app loads `./model/mnist_tf2.h5`, and the training script writes under `./model/`. Use the root [requirements.txt](../requirements.txt) for this variant; the TFLearn requirements under `legacy/mnist-draw/` belong to a separate stack and are not combined with it.

## Original setup

The original README specified Python 3.5+. Treat that as a historical requirement, not a verified compatibility range for the dependencies in [requirements.txt](../requirements.txt).

```bash
# Clone this repository
git clone https://github.com/gawainchin/mnist-draw-gradio.git

# Go into the repository
cd mnist-draw-gradio

# Install the recorded dependencies
pip install -r requirements.txt
```

The original notes also asked users to select their Python 3 executable, giving this example path:

```text
/Users/xxx/anaconda/bin/python3
```

## Original model training

From the repository root, the original training command was:

```bash
python model.py
```

[model.py](../model.py) loads MNIST through Keras and saves the model to `model/mnist_tf2.h5`, the path loaded by [app.py](../app.py). Its checkpoint callback also saves `model/mnist_tf2_best.h5` when validation loss improves. The original instructions allowed replacing `model/mnist_tf2.h5` with a model trained by the user. Training and compatibility of replacement models have not been verified.

## Original Heroku workflow

The original instructions assumed a Heroku account and used these commands from the repository root:

```bash
heroku create
git push heroku master
```

The [Procfile](../Procfile) contains `web: source setup.sh && python app.py`. [setup.sh](../setup.sh) sets `GRADIO_SERVER_NAME=0.0.0.0` and `GRADIO_SERVER_PORT` from Heroku's `PORT` environment variable. These files describe the historical deployment configuration; current platform compatibility and successful deployment are unverified.

The original README linked to [this historical Heroku demo](https://boiling-river-49417.herokuapp.com) and advised allowing time for the server to start. The URL is retained as project history; its current availability, startup time, and application behavior are unverified.
