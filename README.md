<h1 align='center'>Diego</h1>

## Summary

Diego is a `Deep Learning Neural Network` model built using `Python` & `TensorFlow`. It can identify a dog's breed.
For training the model I've used the [Dog Breed Identification](https://www.kaggle.com/c/dog-breed-identification/data)
dataset. The project is created in `Jupyter Notebook`.

## Creating the model

Firstly, I've used `Anaconda` to create a `Virtual Environment` for the project & installed the respective version of
`Nvidia`'s `CUDA Toolkit` & `cuDNN` library to use `TensorFlow-gpu`. 

I've processed the data using `Pandas`, visualized the data using `Matplotlib` & then used `NumPy`to create a `ndarray`
object of all the breeds present in the dataset. This process allowed me to convert the labels(dog breeds) to `Booleans`.

After that, I've split the data for training & validation using `scikit-learn`. Then, I've processed the training images
& created data batches to feed the data to the model. For the first attempt I took only 1000 images to make sure everything
is working properly.

For the model, I've used the `ResNet50 V2 CNN` from `TensorFlow Hub` & created a model using `Keras`. Then, using `Tensorboard`, I've
created `model callback` & `early stopping` for the model.

## Training the model

I trained the model with the 1000 images. It ran for 13 `epochs`, had a loss of 0.0626 on training data & 1.7570 on the
validation data. On those 1000 images it got 100% accuracy on training data & 58% accuracy on validation data. Obviously the model
was overfitting.

So I used the `Adam` optimizer with a `learning_rate` of 0.0005, which performed the best in this particular scenario & used
`data augmentation` to avoid the overfitting issue. Then I trained the model with the complete data. The final model got 99% accuracy
on training data.

## Saving the model

I've used the `TensorFlow`'s `model.save()` method to save the model in `.h5` format, so that instead of retraining the model everytime,
I can simply load the model whenever required.

## Deployment

I've deployed the model using `TensorFlow Serving`, `Docker` & created a `RESTful API` for getting predictions from the model.
You can check that on my [Portfolio Website's works section](https://adfolio.herokuapp.com/works.html).

To deploy the model, firstly I've used the `os` library to create a directory and the `shutil` library to clean the directory, then saved the
trained model's `signature graph`, `weights` and `variables` using the `keras`'s `save_model()` method. After that, I've created a `Dockerfile` to download
`TensorFlow Serving` and deploy the model on that. Finally, I've deployed the `Docker Image` on `Heroku` to run the model successfully.

As the project got pretty large in size, I used `Docker` to avoid the project size issue on `Heroku` as well as any kind of dependency issue.

You can check this repo for the source code of this project
