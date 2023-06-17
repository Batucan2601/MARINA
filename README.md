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


## 2.2. Our interpretation 

@TODO: Explain the parts that were not clearly explained in the original paper and how you interpreted them.

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
