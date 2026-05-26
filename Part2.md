# Part 2: Neural Networks (60 marks)

There are three tasks for this part of the assignment. (Plus an extra task for AIML420 students.)

## Task a: Training a Simple Perceptron on Linearly Separable Data

*(20 marks for AIML320, 15 marks for AIML420)*

Your first task is to implement a simple perceptron from scratch and evaluate how well it performs on a binary classification task using a predetermined train and test set.

You will use:

- `SeaSynTrain.csv` as the training set
- `SeaSynTest.csv` as the test set

Each dataset contains:

- 3 continuous features: `attrib1`, `attrib2`, and `attrib3`
- 1 target column: `class`, with values 0 or 1

Submit your implementation of the Perceptron, along with the code for evaluating its performance, in a single file called `perceptron`.

### Instructions

- Use accuracy as your evaluation metric.
- Train the perceptron using different numbers of epochs:

  ```
  [1, 5, 10, 15, 20, 50, 60, 80, 100, 120, 150, 200]
  ```

- In your report, show the test set accuracy after training for each number of epochs.
- Then, answer the following:

  > How does increasing the number of epochs affect the model's accuracy?

You can present your results in a table like this:

| Model (epoch)    | Accuracy |
| ---------------- | -------- |
| Perceptron (1)   |          |
| Perceptron (5)   |          |
| Perceptron (10)  |          |
| ...              | ...      |
| Perceptron (150) |          |
| Perceptron (200) |          |

## Task b: Training a Simple Perceptron on Non-Linearly Separable Data

*(20 marks for AIML320, 15 marks for AIML420)*

In this task, you will reuse your Perceptron implementation to evaluate its performance on a dataset that is not linearly separable. This will help you explore the limitations of a linear classifier. Precisely, you will use:

- `RingSynTrain.csv` as the training set
- `RingSynTest.csv` as the test set

Each dataset contains:

- 2 continuous features: `x1` and `x2`
- 1 target column: `class`, with values 0 or 1

Use the Perceptron implementation from Task (a) and evaluate (using the accuracy metric) on this dataset.

### Instructions

- Use accuracy as your evaluation metric.
- Train the perceptron using different numbers of epochs:

  ```
  [1, 5, 10, 15, 20, 50, 60, 80, 100, 120, 150, 200]
  ```

- In your report, show the test set accuracy after training for each number of epochs.
- Then, answer the following:

  > How well does the perceptron perform on this dataset?

You can present your results in a table like this:

| Model (epoch)    | Accuracy |
| ---------------- | -------- |
| Perceptron (1)   |          |
| Perceptron (5)   |          |
| Perceptron (10)  |          |
| ...              | ...      |
| Perceptron (150) |          |
| Perceptron (200) |          |

## Task c: Training an MLP on Non-Linearly Separable Data

*(20 marks for AIML320, 15 marks for AIML420)*

In this task, you will evaluate how a simple Multi-Layer Perceptron (MLP) handles the same non-linearly separable dataset from Task b. Unlike the perceptron you implemented from scratch, here you must use an existing implementation, for example, from scikit-learn or another library of your choice.

Use the same dataset as in Task b: i.e. `RingSynTrain` (for training) and `RingSynTest` (for testing).

### Instructions

- Use a standard MLP classifier implementation from a library (e.g., `sklearn.neural_network.MLPClassifier`).
- Use a simple architecture — for example, one hidden layer with 4 to 10 neurons. Submit your code in a file called `mlp`.
- You don't need to test lots of configurations. Just pick one setup that seems reasonable, run it, and evaluate it using accuracy. Then in your report, answer the questions below:

  > How does the performance of the MLP compare to the Perceptron from Task b on this dataset?
  >
  > Was the MLP able to better capture the structure of the data? Why or why not?

## Task d: Activation Function Comparison

*(AIML420 mandatory, 15 marks)*

In this task, you will investigate the effect of different activation functions on MLP performance.

**Dataset:** `RingSynTrain.csv` (training set) and `RingSynTest.csv` (test set)
**Features:** `x1`, `x2`
**Target:** `class` (0 or 1)

### Instructions

1. Train MLPs with two different activation functions: sigmoid and relu.
2. Use the same architecture as in Task c (i.e. one hidden layer with 4–10 neurons). (You can use the same `mlp` code file, or submit a second one, `mlp2`.)
3. Evaluate each model on `RingSynTest.csv` and compare convergence speed and test accuracy.
4. In your report, answer the following questions:

   > - Which activation function performed best and why?
   > - How does activation choice affect learning dynamics?
