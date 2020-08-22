# mnist-draw-gradio
This repo is to show how to create your mnist-draw model by using gradio UI and deploy on Heroku Cloud.

It is accomplished by two major steps:

  - Train your own model
  - Deploy your Gradio app on Heroku

### Setup

Python 3.5+ is required for compatability with all required modules

```bash
# Clone this repository
git clone https://github.com/gawainchin/mnist-draw-gradio.git

# Go into the repository
cd mnist-draw-gradio

# Install required modules
pip install -r requirements.txt
```
Please make sure you have added your python 3 path
```
/Users/xxx/anaconda/bin/python3  #For example
```

### Model Training

Train your own model by running this:

```
python model.py
```
and replace the own model at /model/mnist_tf2.h5

### Heroku Deployment


If your have created your own Heroku account, you can create your dyno by running this:
```
heroku create
```
and push to the Heroku
```
git push heroku master
```
Give it a few minutes then you will see your app should be running on web!
