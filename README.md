# Exploring-Convolutional-Layers-Through-Data-and-Experiments
In this course, neural networks are not treated as black boxes but as architectural components whose design choices affect performance, scalability, and interpretability. This assignment focuses on convolutional layers as a concrete example of how inductive bias is introduced into learning systems. 

This project explores convolutional neural networks as architectural components rather than black-box models. Using the Fashion-MNIST dataset, we analyze how convolutional layers introduce inductive bias, compare them against a non-convolutional baseline, and evaluate how architectural decisions impact learning and performance.

The project includes dataset exploration, baseline and CNN model design, controlled experiments on convolutional layers, and deployment of the final model as an inference endpoint using AWS SageMaker.

---

## Getting Started

These instructions will help you set up the project locally or in AWS SageMaker, reproduce the experiments, and understand the reasoning behind the architectural choices.

The main deliverable of this project is a Jupyter Notebook containing:
- Dataset exploration (EDA)
- Baseline neural network (non-convolutional)
- Convolutional neural network (CNN)
- Controlled experiments
- Deployment to SageMaker

---
## Dataset Description

The Fashion-MNIST dataset consists of 70,000 grayscale images of size 28×28 pixels, divided into 10 clothing categories such as T-shirt, trouser, sneaker, and bag. The dataset is split into 60,000 training samples and 10,000 test samples.

Each image is represented as a single-channel (grayscale) 2D tensor, making it well-suited for convolutional neural networks.
---


## Model Architecture

The baseline model consists of:
- Input layer (28×28 flattened)
- Fully connected dense layers
- Softmax output layer

The convolutional neural network consists of:
- Convolutional layers with ReLU activation
- Max pooling layers
- Fully connected layers
- Softmax output layer

### Prerequisites

The following software and services are required:

- Python 3.9 or 3.10
- pip (Python package manager)
- Jupyter Notebook or AWS SageMaker Studio
- AWS account with SageMaker permissions

Required Python libraries:

```
    numpy
    matplotlib
    tensorflow
   sagemaker
```


---

### Installing

Step 1:  Create and activate a virtual environment

```
python -m venv venv
source venv/bin/activate # Linux / Mac
venv\Scripts\activate # Windows
```


Step 2: Upgrade pip

```
pip install --upgrade pip

```


Step 3: Install required dependencies

```
pip install numpy matplotlib tensorflow sagemaker
```


Step 4: Start Jupyter Notebook (local execution)

```
Exploring-Convolutional-Layers-Through-Data-and-Experiments.ipynb
```


Step 5: Open the notebook and execute the cells sequentially.  
Note: The SageMaker deployment cell should be executed only once due to endpoint initialization time.

---

## Running the tests

This project does not include automated unit tests. Model evaluation is performed through training, validation, and inference

### End-to-end evaluation

The system is evaluated by:

- Training the model on the Fashion-MNIST training set
- Evaluating accuracy and loss on the test set
- Performing inference on unseen samples

Example:

```
test_loss, test_accuracy = model.evaluate(x_test, y_test)
print("Test accuracy:", test_accuracy)
```


These steps verify that the model generalizes to unseen data.

---

## Experimental Results

The baseline fully connected model achieved lower accuracy and showed signs of overfitting when compared to the convolutional model.

The CNN achieved higher validation and test accuracy, demonstrating better generalization due to spatial feature extraction. Increasing the number of convolutional layers improved performance up to a point, after which gains diminished while model complexity increased.



### Coding style and validation

The code follows standard Python and TensorFlow/Keras best practices:
- Clear variable naming
- Modular structure
- Markdown explanations for each section

No automated coding style tests are included.

---

## Deployment

The final CNN model is deployed using AWS SageMaker as a managed real-time inference endpoint.

Deployment steps:
1. Save the trained TensorFlow/Keras model
2. Upload the model artifact to Amazon S3
3. Create a TensorFlowModel object in SageMaker
4. Deploy the model to an endpoint
5. Perform inference using the endpoint
6. Delete the endpoint after testing to avoid unnecessary costs

Due to container initialization and environment setup, endpoint creation may take several minutes.

---

## Built With

* [TensorFlow](https://www.tensorflow.org/) – Deep learning framework
* [Keras](https://keras.io/) – High-level neural network API
* [NumPy](https://numpy.org/) – Numerical computing
* [Matplotlib](https://matplotlib.org/) – Data visualization
* [AWS SageMaker](https://aws.amazon.com/sagemaker/) – Model deployment and inference

---

## Interpretation

Convolutional layers outperformed the baseline model because they exploit the spatial structure of image data. By using local receptive fields and shared weights, convolution introduces an inductive bias that favors translation-invariant feature learning;This bias makes CNNs particularly effective for image-based tasks, while fully connected networks struggle to scale efficiently. Convolutional architectures may not be appropriate for problems where spatial locality is irrelevant, such as tabular or purely symbolic data


## Contributing

This project was developed as part of an academic assignment.  
Contributions are welcome provided they maintain clarity and documentation quality.

---

## Versioning

This project follows Semantic Versioning (SemVer).  
Available versions can be found in the repository tags.

---

## Authors

* **Roger Rodríguez** – Dataset analysis, model design, experiments, and deployment

---

## License

This project is licensed under the MIT License.  
See the LICENSE file for details.

---

## Acknowledgments

- Fashion-MNIST dataset by Zalando Research
- TensorFlow and Keras documentation
- AWS SageMaker official documentation and examples
- Course materials and reference notebooks

