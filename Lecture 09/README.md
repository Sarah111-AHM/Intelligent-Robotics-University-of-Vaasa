# Intelligent Robotics – Lecture 9: Autonomous Systems

**Instructor:** Mahmoud Elsanhoury – University of Vaasa

This lecture covers the definition of autonomous systems, machine learning types (supervised, unsupervised, reinforcement), neural networks, computer vision for lane detection, sensor fusion, and autopilot training/testing.

---

## Automatic vs. Autonomous – Recap

| Automatic | Autonomous |
|-----------|------------|
| Pre-programmed for minor actions | Analyzes environment and makes decisions |
| No decision making | Takes proper decisions based on data |
| Example: Normal car | Example: Self-driving car |

**Autonomous Definition:**  
A system that allows a machine to operate unsupervised for specific tasks, equipped with resources (databases, algorithms, formulas) to acquire environmental information, analyze, reason, and decide.  
> Every autonomous system is automatic, but not every automatic system is autonomous.

---

## What an Autonomous System (e.g., Self-Driving Car) Requires

### 1. Machine Learning

#### Supervised Learning
- **Regression** (predict continuous values)
- **Classification** (predict categories)
- **Anomaly detection**
- **Semi-supervised clustering**

**Bonus Q:** Difference between clustering and classification?  
- **Clustering:** Group data points by similarity without prior labels (unsupervised or semi-supervised).  
- **Classification:** Assign data points to predefined labels (supervised).

**Linear Regression Example:**  
Minimize mean squared error:  
\[
\xi = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2
\]

#### Neural Networks
- Inspired by biological neurons (threshold ~ -55mV, electrochemical signals).
- Feedforward network: input layer → hidden layer(s) → output layer.
- **Backpropagation algorithm:** Propagates error backward to adjust weights.
- **Overfitting:** Too many layers/neurons → memorizes instead of generalizing.
- **Underfitting:** Network too small → cannot capture the mapping.

Other supervised algorithms: Decision Tree, Logistic Regression, Naive Bayes, SVM.

#### Unsupervised Learning
- **Clustering:** K-means
- **Dimensionality reduction:** PCA (Principal Component Analysis)

#### Reinforcement Learning
- Agent learns by interacting with environment, receiving rewards/punishments.
- Example: OpenAI agents move using x/y forces and rotation, sense objects with lidar-like sensors within a frontal cone.

---

### 2. Computer Vision

Enables object detection, edge detection, lane detection.

**Lane Detection Pipeline (OpenCV):**
1. Input image (color)
2. Convert to grayscale
3. Gaussian blur (smoothing)
4. Canny edge detection
5. Region selection mask
6. Hough transform to draw lane lines

### 3. Sensor Fusion

Why fuse sensors?  
- ↑ Accuracy  
- ↑ Redundancy  
- ↑ Confidence  
- ↓ Errors  
- ↑ Integrity  

> "One system to mix them all" – combining cameras, lidar, radar, GPS, IMU, etc.

---

## Building and Testing an Autopilot

- **Training:** Use large datasets to adjust model weights.
- **Testing:** Use simulators before real-world deployment.
- **Warning:** Non-optimal weights or different test dataset → **CRASH**.
- **Solution:** Optimal training + system redundancy (sensor fusion).

---

## Key Takeaways

1. **Autonomous ≠ automatic** – autonomy requires perception, reasoning, and decision-making.
2. **Machine learning** is essential: supervised (regression, classification), unsupervised (clustering, PCA), and reinforcement learning.
3. **Neural networks** use backpropagation; balance overfitting vs. underfitting.
4. **Computer vision** enables lane detection via edge detection and region masking.
5. **Sensor fusion** improves accuracy, redundancy, confidence, and reduces errors.
6. **Autopilot development** requires large datasets, simulators, and careful weight optimization to avoid crashes.

---

**Next:** Sensor fusion techniques and multi-sensor integration.
