# Attention-based | MultiHead | CNLSTM | for RUL prediction

This repository demonstrates the implementation of an attention-based multihead convolution long-short term memory network (AMCNLSTM), similar to one of the models presented in [this work](https://arxiv.org/abs/2109.01761). A multihead model is a form of ensemble that has been found to produce state-of-the-art results on a number of tasks. In this work, the attention-based multihead model is used for improved remaining useful life prediction of aircraft engines. 

A deep AMCNLSTM network is trained using the FD001 subset in the NASA's [C-MAPSS dataset](https://ti.arc.nasa.gov/tech/dash/groups/pcoe/prognostic-data-repository/). This implementation also utilizes the threshold approach called [piecewise RUL](https://github.com/abiodun-ayodeji/Predictive-Maintenance) to define the engine pre-degradation cycle when the engine is assumed to operate in a normal state. This implementation also uses selected sensor readings, and functions are provided to experiment with other subsets of the C-MAPSS dataset.

# Dataset

The dataset (FD001) is a subset of the original C-MAPSS dataset provided by NASA. Data cleaning and preprocessing is done by the functions provided in the notebook. The code in the notebook can also be used to evaluate the predictive power of the model on other data subsets (e.g. FD002, FD003, and FD004) provided [here](dataset).

# Model
Each head of the AMCNLSTM RUL estimator has two one-dimensional convolution layers, separated by LeakyRelu and BatchNormalization layer. It also has one LSTM layer, and a self-attention layer which is then max-pooled and flattened. Each head is used to learn the patterns in each feature in the training input. The output from each head is then concatenated, and a dense layer is used as the prediction output.  

This is the graph of an AMCNLSTM predictor with ten input features:

![Attention-based multihead model](AMCNLSTM.png)

# Usage

You may load the model checkpoint and predict the RUL directly. You may also evaluate the model on other data subsets from C-MAPSS. The preprocessing steps are the same, simply change the path to the data subset and run the notebook.



# Links:

[1] A. Ayodeji et al, ["Causal augmented ConvNet: A temporal memory dilated convolution model for long-sequence time series prediction"](https://www.sciencedirect.com/science/article/pii/S0019057821002810), ISA Transactions, 2021.

[2] A. Ayodeji, A., Wang, W., Su, J., Yuan J., Liu, X. ["An empirical evaluation of attention-based multi-head 
models for turbofan engine remaining useful life prediction"](https://arxiv.org/abs/2109.01761). ArXiv,2021.
