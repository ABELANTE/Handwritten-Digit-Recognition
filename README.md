# Handwritten Digit Recognition

A Deep Learning project for handwritten digit classification using the **MNIST dataset** and **TensorFlow/Keras**.

The project builds and compares three different neural network approaches:

* Single-Layer Neural Network
* Artificial Neural Network (ANN)
* Convolutional Neural Network (CNN)

The objective is to understand how different neural network architectures perform on an image classification problem.

---

## 📌 Project Overview

Handwritten digit recognition is a multi-class image classification problem where the model identifies digits from **0 to 9**.

In this project, the MNIST dataset is used to train and compare three different neural network architectures. The models are evaluated and compared to understand how performance changes as the network architecture becomes more suitable for image data.

The CNN achieved the best evaluation accuracy among the three models.

> **Note:** In this project, the MNIST test dataset (`mnist_test.csv`) is used as the validation dataset during model training and is also used for final evaluation. Therefore, the reported evaluation accuracy should not be interpreted as performance on a completely unseen test dataset.

---

## 🎯 Objectives

* Understand the structure of the MNIST dataset.
* Perform data exploration and preprocessing.
* Normalize image pixel values.
* Convert flattened pixel data into image dimensions.
* Encode labels for multi-class classification.
* Build and train different neural network architectures.
* Compare model performance.
* Visualize training and validation results.
* Understand why CNNs are effective for image classification.

---

## 📂 Project Structure

```text
Handwritten-Digit-Recognition/
│
├── data/                         # Download separately from Kaggle
│   ├── mnist_train.csv
│   └── mnist_test.csv
│
├── notebooks/
│   └── handwritten_digit_recognition.ipynb
│
├── .gitignore
├── LICENSE
├── README.md
└── requirements.txt
```

### Directory Description

| Path               | Description                                                            |
| ------------------ | ---------------------------------------------------------------------- |
| `data/`            | MNIST training and testing CSV files. Download separately from Kaggle. |
| `notebooks/`       | Jupyter Notebook containing the complete project                       |
| `requirements.txt` | Required Python dependencies                                           |
| `.gitignore`       | Files excluded from Git tracking                                       |
| `LICENSE`          | Project license                                                        |
| `README.md`        | Project documentation                                                  |

---

# 📊 Dataset

This project uses the **MNIST in CSV** dataset from Kaggle.

**Dataset:** [MNIST in CSV](https://www.kaggle.com/datasets/oddrationale/mnist-in-csv)

### Dataset Information

| Dataset  | Samples | Columns |
| -------- | ------: | ------: |
| Training |  60,000 |     785 |
| Testing  |  10,000 |     785 |

Each row contains:

```text
1 Label + 784 Pixel Values
```

The 784 pixel values represent a:

```text
28 × 28
```

grayscale image.

Pixel values range from `0` to `255`, while the label represents a digit from `0` to `9`.

---

# ⚙️ Installation & Setup

Follow the steps below to run the project locally.

## 1. Clone the Repository

```bash
git clone https://github.com/harshalk2022/Handwritten-Digit-Recognition.git
```

Navigate to the project directory:

```bash
cd Handwritten-Digit-Recognition
```

---

## 2. Create a Virtual Environment

```bash
python -m venv venv
```

### Activate — Git Bash

```bash
source venv/Scripts/activate
```

### Activate — Windows CMD

```cmd
venv\Scripts\activate
```

After activation, the terminal should show something similar to:

```text
(venv)
```

---

## 3. Download the Dataset

The dataset is **required** to run the notebook and is not downloaded automatically.

Download the dataset from Kaggle:

**[MNIST in CSV](https://www.kaggle.com/datasets/oddrationale/mnist-in-csv)**

After downloading and extracting the dataset, you should have:

```text
mnist_train.csv
mnist_test.csv
```

---

## 4. Place the Dataset in the `data` Folder

Place both CSV files inside the project's `data/` directory.

The structure should look like:

```text
Handwritten-Digit-Recognition/
│
├── data/
│   ├── mnist_train.csv
│   └── mnist_test.csv
│
├── notebooks/
│   └── handwritten_digit_recognition.ipynb
│
├── .gitignore
├── LICENSE
├── README.md
└── requirements.txt
```

The notebook expects the dataset files at:

```text
data/mnist_train.csv
data/mnist_test.csv
```

**Make sure the filenames and folder location are correct before running the notebook.**

> The `data/` directory is excluded from Git using `.gitignore`, so the dataset must be downloaded separately.

---

## 5. Install Dependencies

With the virtual environment activated:

```bash
pip install -r requirements.txt
```

---

## 6. Run the Jupyter Notebook

Start Jupyter Notebook:

```bash
jupyter notebook
```

Open:

```text
notebooks/handwritten_digit_recognition.ipynb
```

Run the notebook cells sequentially.

---

# 🔄 Project Workflow

```text
MNIST CSV Dataset
       ↓
Load Dataset
       ↓
Data Exploration
       ↓
Check Missing Values
       ↓
Separate Features & Labels
       ↓
Normalize Pixel Values
       ↓
Reshape Images
       ↓
One-Hot Encode Labels
       ↓
Train Models
       │
       ├── Single-Layer Neural Network
       │
       ├── ANN
       │
       └── CNN
       ↓
Evaluate Models
       ↓
Compare Accuracy
       ↓
Visualize Results
       ↓
Select Best Performing Model
```

---

# 🔍 Data Exploration

The notebook performs basic exploration of the dataset, including:

* Dataset shape
* Column names
* Data types
* Missing-value checking
* Sample records
* Training and testing dataset inspection

The training dataset contains:

```text
60,000 rows × 785 columns
```

and the testing dataset contains:

```text
10,000 rows × 785 columns
```

---

# ⚙️ Data Preprocessing

The dataset contains flattened `28 × 28` images represented by 784 pixel values.

The following preprocessing steps are performed.

## 1. Separate Features and Labels

The `label` column is separated from the pixel values.

```python
X_train = df.drop("label", axis=1).values
y_train = df["label"].values

X_test = df_test.drop("label", axis=1).values
y_test = df_test["label"].values
```

---

## 2. Normalize Pixel Values

Pixel values are converted from `0–255` to `0–1`.

```python
X_train = X_train.astype("float32") / 255.0
X_test = X_test.astype("float32") / 255.0
```

Normalization helps the neural networks train more effectively.

---

## 3. Reshape Images

The flattened pixel values are reshaped into image dimensions.

For the CNN:

```python
X_train_cnn = X_train.reshape(-1, 28, 28, 1)
X_test_cnn = X_test.reshape(-1, 28, 28, 1)
```

The CNN input shape is:

```text
28 × 28 × 1
```

where `1` represents the grayscale channel.

---

## 4. One-Hot Encode Labels

The digit labels are converted into one-hot encoded vectors.

```python
y_train_cat = to_categorical(y_train, 10)
y_test_cat = to_categorical(y_test, 10)
```

For example, digit `5` becomes:

```text
[0, 0, 0, 0, 0, 1, 0, 0, 0, 0]
```

---

# 🧠 Models

## 1. Single-Layer Neural Network

A simple linear/softmax classifier is used as the baseline model.

### Architecture

```text
Input Image
     ↓
Flatten
     ↓
Dense(10, Softmax)
     ↓
Prediction
```

### Configuration

```text
Optimizer : SGD
Loss      : Categorical Crossentropy
Metric    : Accuracy
Epochs    : 5
Batch Size: 32
```

### Evaluation Accuracy

**90.88%**

---

## 2. Artificial Neural Network (ANN)

The ANN uses multiple fully connected layers.

### Architecture

```text
Input Image
     ↓
Flatten
     ↓
Dense(128, ReLU)
     ↓
Dense(64, ReLU)
     ↓
Dense(10, Softmax)
     ↓
Prediction
```

### Configuration

```text
Optimizer : Adam
Loss      : Categorical Crossentropy
Metric    : Accuracy
Epochs    : 5
Batch Size: 32
```

### Evaluation Accuracy

**97.70%**

---

## 3. Convolutional Neural Network (CNN)

The CNN uses convolution and pooling layers to learn spatial features from handwritten digit images.

### Architecture

```text
Input Image
     ↓
Conv2D(32, 3×3, ReLU)
     ↓
MaxPooling2D(2×2)
     ↓
Conv2D(64, 3×3, ReLU)
     ↓
MaxPooling2D(2×2)
     ↓
Flatten
     ↓
Dense(128, ReLU)
     ↓
Dropout(0.5)
     ↓
Dense(10, Softmax)
     ↓
Prediction
```

### Configuration

```text
Optimizer : Adam
Loss      : Categorical Crossentropy
Metric    : Accuracy
Epochs    : 5
Batch Size: 32
Dropout   : 0.5
```

### Evaluation Accuracy

**99.07%**

---

# 📈 Model Comparison

| Model                       | Type             | Evaluation Accuracy |
| --------------------------- | ---------------- | ------------------: |
| Single-Layer Neural Network | Linear / Softmax |          **90.88%** |
| ANN                         | Fully Connected  |          **97.70%** |
| CNN                         | Convolutional    |          **99.07%** |

### Result

```text
CNN > ANN > Single-Layer Neural Network
```

The CNN achieved the highest evaluation accuracy among the three models.

This demonstrates the advantage of convolutional layers for image classification, as CNNs can learn spatial patterns and local features from images.

> **Evaluation note:** The same MNIST test dataset is used as validation data during training and for final evaluation in this project. Therefore, these values should not be considered performance on a completely unseen test dataset.

---

# 📊 Visualization

The notebook contains visualizations for:

* Training accuracy
* Validation accuracy
* Training loss
* Validation loss
* Model accuracy comparison
* Sample digit predictions

These visualizations help analyze the training process and compare the performance of the different models.

---

# 🛠️ Technologies Used

* **Python 3.11**
* **NumPy**
* **Pandas**
* **Matplotlib**
* **Seaborn**
* **Scikit-learn**
* **TensorFlow**
* **Keras**
* **Jupyter Notebook**
* **Git**
* **GitHub**

---

# 💡 Key Learnings

* Understanding the structure of image datasets.
* Representing `28 × 28` images using 784 pixel values.
* Normalizing image pixel values.
* Reshaping flattened data into image tensors.
* One-hot encoding for multi-class classification.
* Building neural networks using TensorFlow/Keras.
* Understanding fully connected neural networks.
* Understanding convolution and pooling layers.
* Understanding dropout.
* Comparing different Deep Learning architectures.
* Evaluating and visualizing model performance.

---

# 🚀 Future Improvements

* Add data augmentation.
* Experiment with different CNN architectures.
* Tune hyperparameters.
* Add Early Stopping.
* Add a confusion matrix.
* Save the trained CNN model.
* Create a separate inference script.
* Build a Streamlit interface for handwritten digit drawing.
* Deploy the model using FastAPI.
* Test the model on custom handwritten digit images.

---

# 📚 Dataset Source

The dataset was obtained from Kaggle:

**[MNIST in CSV](https://www.kaggle.com/datasets/oddrationale/mnist-in-csv)**

The dataset must be downloaded separately and placed inside the project's `data/` directory as described in the **Installation & Setup** section.

---

# 👨‍💻 Author

**Harshal Khandalkar**

GitHub: [harshalk2022](https://github.com/harshalk2022)

---

# 📄 License

This project is licensed under the **MIT License**.

See the [LICENSE](LICENSE) file for more information.
