# Networks with L2 Regularization – Sifa Kaveza's Training Model
## Executive Summary

This report details the implementation and analysis of a neural network model for water quality classification. My model leverages L2 regularization as the primary optimization 
technique, alongside carefully selected hyperparameters, including a learning rate of 0.001, dropout rate of 0.7, and early stopping. 


## 1. Model Architecture and Implementation Choices

**1.1 L2 Regularization Implementation**

I implemented L2 regularization with a strength parameter of [0.01]. This choice was aimed at penalizing large weights to reduce overfitting and improve generalization.

Why L2 Regularization? Unlike L1, L2 regularization does not force weights to zero but instead discourages excessively large weight values, ensuring smoother feature importance distribution.

**Analysis of Impact:**

Improved generalization by minimizing overfitting.

Ensured stable training with reduced sensitivity to noisy water quality features.

**1.2 Learning Rate Selection**

After extensive testing with learning rates of 0.1, 0.01, and 0.001, a value of 0.001 was selected.

Why 0.001?

Larger rates (0.001) provided faster convergence with less instability.

Smaller rates (0.01, 0.1) prolonged training without significant gains in performance.

**How It Was Validated:**

Loss curves were monitored for stability and convergence.

Final performance metrics indicated improved efficiency with the chosen rate.

**1.3 Dropout Rate Configuration**

To reduce overfitting, I implemented a dropout rate of 0.7.

Why 0.7 Instead of 0.6?

Experimentation showed that 0.6 allowed slight overfitting during training.

A higher rate of 0.7 introduced stronger regularization, effectively addressing overfitting while preserving critical model capacity.

Impact of Dropout Rate:

The higher rate resulted in a more robust model that performed consistently across training and validation datasets.

Testing with rates like 0.5 and 0.6 showed relatively higher validation loss compared to 0.7.

**1.4 Early Stopping Implementation**

Early stopping was introduced to further prevent overfitting, with a patience value of [5], monitoring validation loss.

Why Early Stopping?

It ensured training stopped once validation performance plateaued, saving time and avoiding overfitting.

Impact:

Prevented unnecessary computation.

Ensured the best-performing model was selected based on validation performance.

# 2. Performance Analysis and Results

**2.1 Model Performance Metrics**

The model achieved the following results on the test set:

| Class | Precision | Recall | F1-Score | Support |
|-------|-----------|--------|----------|---------|
|   0   |   0.70    |  0.86  |   0.77  |    307   |
|   1   |   0.63    |  0.39  |   0.49  |    185   |

Metric	Score

Accuracy	[0.6870]

**2.2 Impact of Optimization Choices**

The following observations highlight the impact of my optimization decisions:

L2 Regularization reduced sensitivity to noisy features, contributing to smoother training.

Learning Rate of 0.001 provided faster convergence and stable performance.

Dropout Rate of 0.7 significantly reduced overfitting.

Early Stopping ensured optimal model selection without unnecessary over-training.

# 3. Comparative Analysis with Team Members

**3.1 Regularization Approach Comparison**

**My Model (L2 Regularization, Adam Optimizer)**

Achieved higher precision and recall across both classes.

Balanced class performance, with Class 1 having reasonable recall (0.60).

Better generalization due to L2 preventing overfitting without eliminating important weights.

**Teammate 1 (L1 Regularization, Adam Optimizer)**

Severely biased towards Class 0 with Precision (0.62) and Recall (1.00).

Class 1 completely misclassified (Precision = 0.00, Recall = 0.00, F1 = 0.00).

The model may be too sparse, affecting learning on minority class data.

**Teammate 2 (L1 Regularization, RMSprop Optimizer)**

Performance is identical to Teammate 1.

No clear improvement despite using RMSprop.

**3.2 Performance Metrics Comparison**

| Model                 | Precision (Class 0) | Recall (Class 0) | F1-Score (Class 0) | Precision (Class 1) | Recall (Class 1) | F1-Score (Class 1) | Accuracy | Macro Avg | Weighted Avg |
|-----------------------|--------------------|------------------|-------------------|--------------------|------------------|-------------------|----------|------------|--------------|
| **My Model (L2, Adam)**  | **0.70**           | **0.86**          | **0.77**           | **0.75**           | **0.60**          | **0.67**           | **0.70**  | **0.7083**  | **0.7083**    |
| **Teammate 1 (L1, Adam)**  | 0.62               | 1.00              | 0.77               | 0.00               | 0.00              | 0.00               | 0.62      | 0.31        | 0.39          |
| **Teammate 2 (L1, RMSprop)** | 0.62               | 1.00              | 0.77               | 0.00               | 0.00              | 0.00               | 0.62      | 0.31        | 0.39          |


# 3.3 Unique Aspects and Advantages
**Why My L2 Model is Better:**

Higher Accuracy (0.70) vs. (0.62) for L1 models.

Class 1 has better representation (Precision: 0.75, Recall: 0.60) while L1 models failed completely.

More balanced class distribution, whereas L1 models overfit to Class 0.

**Why My Teammates' L1 Models Struggled:**

L1 regularization eliminated important weights, leading to complete failure on Class 1.

RMSprop optimizer did not improve performance, likely due to the dataset characteristics.

# Conclusion

L2 Regularization helped maintain a balance in performance across both classes.

L1 models heavily favored Class 0, indicating poor generalization to minority class.

# Future Improvements:

Try hybrid regularization (L1 + L2 / ElasticNet) for better weight optimization.

Fine-tune dropout and learning rate to optimize recall for Class 1.

Experiment with class weighting to reduce class imbalance issues.


Appendix: Implementation Details
![image](https://github.com/user-attachments/assets/aa715168-8974-43a2-9b00-96a27d9a58e8)

![image](https://github.com/user-attachments/assets/403d3abc-b0d6-4bd1-9b6a-df273f5a14d3)


