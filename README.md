# Web Content Mining with News Article Dataset
We build a classifier that automatically extracts only useful information (e.g. content) from an article where there are lots of useless information (e.g. advertisement). We verify that our machine learning based model is better than rule based model (*InSciteCralwer*) through outer test, even though our problem is somewhat deterministic (rules are useful!). Also, machine learning based model was possible to predict articles with new types, which rule-based doesn't predict at all. Note that patterns cah be changed according to news-website, section of it and the time (developer-style).

![](/assets/pipeline.PNG)

The paper for this research has been published at the 2017-9th International Conference on Knowledge and Smart Technology (KST), named as [SVM-based Web Content Mining with Leaf Classification Unit from DOM-tree](http://ieeexplore.ieee.org/document/7886134/).

Here is the [presentation (.ppt)](https://1drv.ms/p/s!AllPqyV9kKUrgieYsNFYWKqCvjKo) for the conference. 


## Prerequisites
* python 3.5.2
* nltk 3.2.2
* scikit-learn 0.19.0
* bs4 4.5.1 (BeatifulSoup)
* pandas 0.20.3

## Dataset
We have collected about 2500 news articles published by 13 different news websites. You can download it in [here](https://drive.google.com/open?id=0By4RRGJEeCR5YjBiZVd2dkdQWms). Note that the data is just html file, which is not annotated. 

## Usage
```
python make_trainset.py
```
* Annotate data based on rule list (where is title, date, paragraph in each news website)
* Extract feature vectors out excel files
```
python main.py inner
```
* Train and test with the same kinds of news website (inner test) 
```
python main.py outer
```
* Train and test with the different kinds of news website (outer test)

#### Example
![](/assets/example.PNG)


## Contribution
* Web content mining using machine learning model with feature engineering (HTML syntax) 
* ML-based models robustly deal with new data drawn by **new news-websites**, which rule based can't predict well (shown from outer test) and deals with almost 100% to new data drawn by known news-websites, which rule based can perpectly predict. 
* Given small amount of dataset with high variance, SVM with kernel was best among logistic regression and multilayer neural network, etc.

## 주요내용
* 뉴스 웹 페이지의 광고,추천뉴스 등과 같은 노이즈 정보 필터링이 필요
* 뉴스 웹 페이지 포맷과 심지어 사이트의 포맷까지 시간에 따라 변하는 특징
* 소프트 의사결정을 하는 기계학습 기반 추출기 개발
* 효과적인 분류를 위해 리프 노드 분류 단위 설정
* 돔-트리 구조, 계층적 특징, 태그 정보를 활용한 자질 설계
   - 다양한 종류의 빈도수, 비율 기반 연속형 자질
   - 다양한 종류의 단어, 문자 기반 이산형 자질
* 규칙 기반과 버금가는 inner test 성능 & 규칙 기반을 훨씬 뛰어넘는 outer test 성능

## Summary

_About Models_
* Build the machine learning pipeline for this task.
* Not optimize hyperparameters of model in order to predict well new data from new websites.
* Test with n-fold cross validation for showing robustness for new websites.

_About Features_
* Domain knowledge: understanding HTML syntax
* Information Gain: (1) tree structure (2) hierarchical relationship (3) tag information (name, attribute, content)
* Feature Type: continuous feature (frequency, ratio), discrete feature (a certain word exist or not)

_About Dataset_
* If we have enough dataset, we may don't need outer test and neural networks would be the best and we can use text data as feature representations.
* Actually, the training data is annotated by myself with some rules extracted by *InSciteCralwer*. This is somewhat counterintuitive to use machine learning based models. But, we believed that when using machine learning based model with some rules, we can generalize well data with new rules. You can see the results on the outer test. 

_About Resources_
* Some materials about html files are: (tag name and attribute list)[[.xlsx]](https://1drv.ms/x/s!AllPqyV9kKUrg3qOK2DE7P-TSWW3), (page source for only paragraph)[[.doc]](https://1drv.ms/w/s!AllPqyV9kKUrg3mmTjb6YsLD_wzi), (page source for date and paragraph)[[.doc]](https://1drv.ms/w/s!AllPqyV9kKUrg3sV7zNGUFPfNsvQ)
* Rule-based model is *InSciteCralwer* made by KISTI [(korean paper)](http://semantics.kisti.re.kr/publications/files/DOMESTIC_JOURNAL/DJ-063.pdf). The limits of this model are described in [here](https://1drv.ms/w/s!AllPqyV9kKUrhCgbkwn5MvmfTz6S).
* Certificate of the conference [[link]](https://github.com/gritmind/web-content-mining/blob/master/assets/certificate_of_contributions.pdf)

## Further Study
* 단일 Bottom-up 프로세스을 넘어 Bottom-up과 Top-down이 결합된 하이브리드 방식 개발

## Acknowledgement
Korea Institute of Science and Technology Information (KISTI) <br>
University of Science and Technology (UST) <br>
2016.7 ~ 2016.10

