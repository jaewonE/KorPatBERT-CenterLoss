# KorPatBERT-CenterLoss

> 본 레포지토리는 2024년 특허청 & 강남대학교 데이터분석 모델링 경진대회 주제인 **특허 문서의 IPC 국제특허분류 코드 분류**를 수행하기 위해 작성되었습니다.

본 연구에서는 객체 탐지를 위해 고안된 CenterLoss 기법을 자연어 처리(NLP) 모델인 KorPatBERT에 접목하였습니다. 이를 통해 단순히 KorPatBERT를 적용했을 때보다 3.82% 향상된 성능을 도출하였으며, CenterLoss의 토큰 시각화를 통해 모델의 설명 가능성을 확보하였습니다. 그 결과, 대회에서 가장 우수한 예측 성능을 인정받아 1등(최우수)을 수상하였습니다.

들어가기에 앞서, 친절히 **KorPatBERT** 모델을 제공해주신 **한국특허정보원**에 깊은 감사를 드립니다.

- **Main Report**: [KorPatBERT_CenterLoss.pdf](https://github.com/jaewonE/KorPatBERT-CenterLoss/blob/main/KorPatBERT_CenterLoss.pdf)
- **Main Notebook**: [korpatbert-centerLoss.ipynb](https://github.com/jaewonE/KorPatBERT-CenterLoss/blob/main/src/korpatbert/korpatbert-centerLoss.ipynb)
- **Main Presentation**: [presentation.pptx](https://github.com/jaewonE/KorPatBERT-CenterLoss/blob/main/doc/presentation.pptx), [presentation.pdf](https://github.com/jaewonE/KorPatBERT-CenterLoss/blob/main/doc/presentation.pdf)
- **Award**: [Award.jpg](https://github.com/jaewonE/KorPatBERT-CenterLoss/blob/main/Award.jpg), [picture](https://github.com/jaewonE/KorPatBERT-CenterLoss/blob/main/Award_picture.jpg)

## Abstract

IPC(국제특허분류) 코드는 전 세계적으로 통용되는 표준화된 분류 체계로, 특허 문서를 효율적으로 관리하고 검색하는 데 필수적인 도구입니다. 현재 국내에서는 한국특허기술진흥원 등 전문 기관에서 수작업으로 특허의 기술 내용을 분석하여 IPC 및 CPC 코드를 부여하고 있으나, 이는 막대한 시간과 비용을 수반합니다. 이를 보조하기 위해 기존의 기계학습 기반 자동 분류 연구가 진행되어 왔으나, 텍스트의 문맥적 의미를 충분히 반영하지 못하거나 신조어 및 신기술 용어 처리에 한계를 보여왔습니다.

최근에는 이러한 한계를 극복하기 위해 BERT와 같은 자연어 처리(NLP) 모델을 활용한 연구가 활발히 진행되고 있습니다. 그러나 일반적인 NLP 기반 방법론은 데이터 클래스 불균형(Class Imbalance) 문제에 취약하여, 데이터가 부족한 소외 분야(Cold Fields)에서 재현율(Recall)이 저하되거나 모델이 과적합되는 문제가 발생하기에 특허 문서 분류에 있어 활용성이 제한됩니다.

본 연구는 **2024년 강남대학교 데이터분석 모델링 경진대회**의 일환으로, 이러한 문제를 해결하기 위해 한국어 특허 문서에 특화된 사전 학습 모델인 **KorPatBERT**와 특징 벡터의 응집력을 강화하는 **CenterLoss** 함수를 결합한 IPC 코드 분류 모델을 제안합니다. 본 모델은 KorPatBERT를 통해 추출된 문맥 벡터에 CenterLoss를 적용하여 클래스 간 분별력을 높이는 한편, 특징 공간 내에서 데이터 간의 거리와 관계를 재정립합니다. 이를 통해 KNN과 유사한 방식으로 토큰 간의 분산 및 관계성을 시각화하고, 결과적으로 모델의 설명력을 강화하는 데 목적을 둡니다.

대회 데이터셋을 활용하여 **G06F, G06Q, G16H** 세 가지 주요 서브클래스에 대한 분류 성능을 평가한 결과, **91.03%의 정확도**를 달성하였습니다. 이는 동일한 하이퍼파라미터 환경에서 KorPatBERT만을 단독으로 사용했을 때보다 **3.82% 향상된 성능**입니다. 결론적으로, 본 연구에서 제안하는 기법이 특허 문서 분류 시 발생하는 클래스 불균형 문제를 완화하고 모델의 일반화 성능을 높이는 데 유효함을 확인하였습니다.

> **Keywords**: IPC Classification, KorPatBERT, CenterLoss, KNN, Class Imbalance

## 파일 구성 및 설명

본 레포지토리의 파일은 연구 결과 보고서, 데이터셋, 그리고 제안 모델과 비교 모델의 소스 코드로 구성되어 있습니다. 하지만 규정과 계약에 따라 경진대회 데이터셋과 KorPatBERT의 가중치는 공개되어 있지 않습니다.

#### 1. Main Report

- **KorPatBERT_CenterLoss.pdf**: 본 연구의 배경, 방법론, 실험 결과 및 분석 내용을 정리한 최종 보고서입니다.

#### 2. Document

- [presentation.pptx](https://github.com/jaewonE/KorPatBERT-CenterLoss/blob/main/doc/presentation.pptx): 발표 파일
- [presentation.pdf](https://github.com/jaewonE/KorPatBERT-CenterLoss/blob/main/doc/presentation.pdf): 발표 자료(PPT의 PDF)

#### 3. Dataset(비공개)

2024년 강남대학교 데이터분석 모델링 경진대회에서 제공된 데이터셋입니다.

- **DS학술제-모델링경진대회\_Train.xlsx**(비공개): 모델 학습을 위한 데이터셋
- **DS학술제-모델링경진대회\_Valid.xlsx**(비공개): 모델 성능 평가를 위한 검증 데이터셋

#### 4. Source Code(src 폴더)

##### A. 제안 모델 (KorPatBERT 기반, src/korpatbert 폴더)

본 연구의 핵심인 특허 전용 언어모델(KorPatBERT)을 활용한 모델링 코드입니다.

- **korpatbert-centerLoss.ipynb**: KorPatBERT에 CenterLoss를 적용한 제안 모델의 학습 및 구현 코드 (**Main**)
- **test-korpatbert-centerLoss.ipynb**: 학습된 제안 모델을 테스트 데이터셋으로 평가하기 위한 테스트 코드
- **korpatbert.ipynb**: 성능 비교를 위한 KorPatBERT 단독 사용(Softmax only) 모델 코드
- **korpatbert-centerLoss.h5**(비공개): 학습이 완료된 제안 모델의 가중치(Weights) 파일

##### B. 비교 모델 1 (KoBERT 기반, src/kobert 폴더)

특허 전용 모델이 아닌 일반 한국어 BERT 모델(KoBERT)을 적용한 비교군입니다.

- **kobert-centerLoss.ipynb**: KoBERT에 CenterLoss를 적용한 모델 코드
- **kobert.ipynb**: KoBERT 단독 사용 모델 코드

##### C. 비교 모델 2 (전통적 기계학습, src/ml 폴더)

딥러닝 모델과의 성능 비교를 위해 구현한 기계학습 알고리즘 코드입니다.

- **knn.ipynb**: K-Nearest Neighbors (KNN) 기반 분류 코드
- **svm.ipynb**: Support Vector Machine (SVM) 기반 분류 코드
- **naive_bayesian.ipynb**: Naive Bayes 기반 분류 코드

## 주의사항

- 본 연구는 python 3.8.20 버전에서 다음 주요 라이브러리를 사용하여 작성되었습니다.
  - numpy==1.19.2
  - tensorflow==2.5.0
  - keras==2.6.0
  - bert-for-tf2==0.14.5
  - konlpy==0.6.0
  - matplotlib==3.4.2
  - mecab-python3==1.0.4
  - plotly==5.1.0
  - python-mecab-ko==1.3.7
  - python-mecab-ko-dic==2.1.1.post2
  - scikit-learn==1.3.2
  - scipy==1.6.2
  - soynlp==0.0.493
- KorPatBERT 모델은 한국특허정보원에서 제공한 모델으로 "assets/특허분야 사전학습 언어모델(KorPatBERT) 사용자 매뉴얼.pdf" 파일을 참고하여 설치 및 사용하셔야 합니다.
- 한국어 형태소 분석을 위해서는 mecab-ko가 필수적으로 필요하며 mecab.zip 파일의 압축 해제 후 "assets/특허분야 사전학습 언어모델(KorPatBERT) 사용자 매뉴얼.pdf"에 따라 설치하여 사용하셔야 합니다.
- KorPatBERT 모델의 가중치 파일은 "pretrained.zip" 파일의 압축 해제 후 사용하실 수 있습니다.
