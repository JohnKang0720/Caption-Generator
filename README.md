# 🖼️ Image Caption Generator

## 1. Context

This project focuses on generating descriptive captions for obstacle images commonly encountered in urban environments. These include traffic lights (red and green), construction signs, and ATMs — both when in use and when idle. The aim is to enable systems to semantically understand these visual cues, potentially assisting in autonomous navigation, surveillance, or context-aware urban monitoring applications.

---

## 2. Preprocessing Captions

To enhance the quality and consistency of captions during training, several text preprocessing techniques were applied:

- **Lemmatization**: Reduced words to their base form to unify similar concepts (e.g., *running* → *run*).
- **Stemming**: Stripped suffixes to normalize words further (e.g., *construction* → *construct*).
- **Regex Cleaning**: Removed unwanted characters, digits, and punctuation to streamline inputs for the model.

These preprocessing steps helped create a cleaner, more learnable caption dataset for training.

---

## 3. Feature Extraction

Two convolutional neural network architectures were explored to extract visual features from images:

- **ResNet**: While powerful, the use of global average pooling in ResNet led to some loss of spatial detail.
- **VGG16**: Performed better overall due to its use of fully connected layers, which helped retain richer spatial and semantic information.

**VGG16** was ultimately chosen as the primary feature extractor for this task, resulting in improved caption quality during testing.

---

## 4. The Captioning Model

The core of the caption generator is a sequence model built using an **LSTM** (Long Short-Term Memory) architecture. It consists of:

- **Dual Input Structure**:
  - Image features (from VGG16).
  - Text sequences (tokenized captions).
  
- **Bidirectional LSTM**: Integrating a bidirectional LSTM significantly improved model comprehension and test performance by capturing dependencies in both forward and backward directions.

- **Training Results**:
  - Epochs: 20  
  - Final Training Loss: **0.8541**

- **Test Results**:
    - Testing was done on multiple real-life obstracle images -- construction zones and lights
    - BLEU score was used to measure accuracy, which were satisfactory, but because there are so many possible words that can be predicted, some have low scores.
 
This architecture effectively learns to generate contextual captions based on both visual features and learned linguistic patterns. 