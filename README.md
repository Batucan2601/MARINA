# MARINA: An MLP-Attention Model for Multivariate Time-Series Analysis

This readme file is an outcome of the [CENG502 (Spring 2023)](https://ceng.metu.edu.tr/~skalkan/ADL/) project for reproducing a paper without an implementation. See [CENG502 (Spring 20223) Project List](https://github.com/CENG502-Projects/CENG502-Spring2023) for a complete list of all paper reproduction projects.

# 1. Introduction

he paper is published for CIKM 2022. The goal of the paper is to achieve better accuracies in multivarite time series anomaly detection.  Our goal was to train the model suggested in the paper 
and see the result for ourselves

## 1.1. Paper summary

Anomaly detection in multivariate time series is a hot-topic in deep learning. this paper proposes a unique idea in terms of data normalization. Rather than using static mean and variance which is done in similiar papers, This paper suggests a dynamic method of normalization in test set which increases mdel's performence overall. Combining this with spatial correlation and temporal correlation methods gives top notch performence on time series anomly detection. 

# 2. The method and my interpretation

## 2.1. The original method

The paper is divided into three sections, data normalization, temporal correlation, and spatial correlation 

# 2.1.1 Data Normalization
Traditionally; in normalization procedures test, validation and training datas should all be normalized before sending it into network. This paper also adopts this technique using mean as 0 and variance as 1, but only in training and validation sets. The procedure for test set is entirely different. In test set we update our mean and variance using previous mean and variances, This allows us to avoid the phenomenon known as concept drifting. Concept drifting refers to the phenomenon in data science where the statistical properties of a target variable or the relationships between features and the target variable change over time, which may cause huge distortions in our anomaly prediction platform , we might take anomalies as usual data because of it or vice versa. 

![image](https://github.com/Batucan2601/MARINA/assets/52931384/b59a8894-b9bf-46e0-af97-3e7eaffc6fd8)

In order to avoid this we use the following formulas in acquiring the next mean and next variances over time. 

![image](https://github.com/Batucan2601/MARINA/assets/52931384/7af2858a-1837-4919-98de-f6e670ee4a04)

Where E(x) is the expected value and  alpha is the weight coefficient. As you can see the mean and variance relies on their previou iterations.

# 2.1.2 Temporal Correlation Module
This module uses the correlation between historical and future points. Paper suggests that using simple MLP blocks rather than using complex architectures such as Transformers etc. gives both better computation speed and better accuracy in the end, therefore spatial module uses only MLP blocks and no other structure.
This module uses a window of size n  where with n data it tries to predict the future j points. This module uses a total of K MLP blocks, where each MLP block is also consisting of an Input subblock, cascading subblock and a forecasting subblock, which are also consisting of multi layer perceptron.

![image](https://github.com/Batucan2601/MARINA/assets/52931384/09cf59ea-4342-4a61-ba97-15d218cfa097)

The relation between those three blocks and MLP block is as follows

![image](https://github.com/Batucan2601/MARINA/assets/52931384/8e5fe23d-4a6c-4a8b-930e-5a6bb45ec4bc)

where X_I is the input subblock X_F is the forecasting subblock and X_C is the cascading subblock. X_O represents the output that is leaving the MLP block.
Paper suggests using 2 MLP block is enough for anomaly detection, therefore we used 2. 

# 2.1.3 Spatial Correlation Module

Spatial module works on each of the time-series separately therefore does not exploit the features of time based data like temporal correlation module. In order to extract the features between the elements in a time series data, paper suggests using multi head self attention mechanism in order to imitate graph neural netowrks which is a popular solution for this problem.
Each row of the output of Temporal correlation module has been used as a vertex; and the message passing is done via following

![image](https://github.com/Batucan2601/MARINA/assets/52931384/d986a80a-fb0b-4621-b783-79964c1f112c)

where X_O is the output from temporal module; Q, K, V are query, key and values in this self attention model respectively. 

# 2.1.4 Output Reshaping Module
Paper also uses a final outut reshaping module which is a simple MLP used in order to change the dimension of output

# Loss
Paper suggests using the frobenius norm for loss. Frobenius norm is basically the L2 norm which corresponds to the lenght of the vector. Therefore Frobenius Loss is the length of the difference of two vectors. Paper suggests using a threshold for this loss; if the threshold is exceeded model informs that this data is an anomaly.  
## 2.2. Our interpretation 
- The threshold for frobenius norm has not been specified therefore we tried many random thresholds for best performence. Best is around 1.85.
- We followed every constant given by paper for anomaly detection. The window length is 100; number of elements to predict in future is 1. Alpha used in normalization is 0.1 and so on.
- We moved the windows with interval of 5 rather than traditional 1 for testing.
- We could only test the dataset of SMAP.
- We did not used CUDA for training. It is not mentioned in the paper but looking at the time statistic it seems the authors also have not used CUDA support. Therefore in order to get the most similar result we also have not used it.
# 3. Experiments and results

## 3.1. Experimental setup

@TODO: Describe the setup of the original paper and whether you changed any settings.

## 3.2. Running the code

@TODO: Explain your code & directory structure and how other people can run it.

## 3.3. Results

@TODO: Present your results and compare them to the original paper. Please number your figures & tables as if this is a paper.

# 4. Conclusion

@TODO: Discuss the paper in relation to the results in the paper and your results.

# 5. References

@TODO: Provide your references here.

# Contact

@TODO: Provide your names & email addresses and any other info with which people can contact you.
