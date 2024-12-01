# KorPatBERT-CenterLoss

> 201904008 곽재원, 202104218 백종민

들어가기 전에, 친절히 KorPatBERT 모델을 제공해주신 **한국특허정보원**에게 감사드립니다.

## Abstract

IPC(국제특허분류) 코드는 특허 문서를 체계적으로 분류하고 검색하는 데 필수적인 도구로, 전 세계적으로 통용되는 표준화된 분류 체계입니다. 현재 국내에서는 한국특허기술진흥원에서 특허 실용신안 및 PCT 국제특허 출원에 대해 기술 내용을 파악하고 적절한 IPC 코드와 CPC 코드를 부여하고 있습니다. 그러나 이러한 작업은 수작업으로 이루어져 많은 시간과 비용이 소요됩니다. 방대한 특허 출원 문서의 분석을 보조하기 위해 다양한 데이터 마이닝 및 기계학습 알고리즘이 적용되고 있으나, 이러한 방법들은 충분한 문맥적 의미를 포착하지 못하고, 새롭게 등장하는 기술 분야나 용어에 유연하게 대응하기 어렵다는 한계가 있습니다.

이에 따라 최근에는 문맥적 의미와 표현을 잘 포착하고 다국어를 지원하는 BERT 모델 등 자연어 처리(NLP)를 활용한 IPC 자동분류 연구가 증가하고 있습니다. 그러나 이러한 NLP 기반 방법은 클래스 불균형의 영향을 크게 받아, 활발하지 않은 분야(Cold Fields)에서 정확도와 재현율(Recall)이 낮아지며 모델 과적합의 위험성이 있습니다.

본 연구에서는 한국어 특허 문서로 사전 학습된 KorPatBERT 모델을 통해 특징 벡터를 추출하고, CenterLoss 손실 함수를 적용하여 KNN 기계학습 알고리즘 기반의 IPC 자동분류 방법을 제안합니다. 강남대학교 특허코드 분류 경진대회 데이터셋을 사용하여 G06F, G06Q, G16H 총 3가지 서브클래스 레벨의 분류를 수행한 결과, 91.03%의 정확도를 달성하였습니다. 이는 동일한 하이퍼파라미터로 KorPatBERT를 적용했을 때보다 3.82% 향상된 성능입니다.

이를 통해 IPC 서브클래스 레벨까지의 분류 수행 시 NLP 기법에서 발생하는 클래스 불균형 및 모델 과적합을 방지하는 데 기여할 수 있음을 확인하였습니다.

> Keyword: IPC, KorPatBERT, CenterLoss, KNN

## 파일 설명

- **KorPatBERT와 CenterLoss를 활용한 KNN 기반 IPC 자동분류 연구.pdf**: 본 연구의 내용 정리된 PDF 파일.
- dataset: 강남대학교 특허코드 분류 경진대회 데이터셋
  - DS학술제-모델링경진대회\_Train.xlsx: 학습 데이터셋
  - DS학술제-모델링경진대회\_Valid.xlsx: 테스트 데이터셋
- 기계학습 알고리즘: 기계학습 알고리즘과 BERT 기반의 모델의 성능 비교를 위해 작성된 코드.
  - knn.ipynb: KNN 알고리즘을 이용한 IPC 자동분류 코드
  - svm.ipynb: SVM 알고리즘을 이용한 IPC 자동분류 코드
  - naive_bayesian.ipynb: Naive Bayesian 알고리즘을 이용한 IPC 자동분류 코드
- KorPatBERT를 사용하지 않은 모델(KoBert 사용)
  - kobert.ipynb: KoBERT 모델을 이용한 IPC 자동분류 코드
  - kobert-centerLoss.ipynb: KoBERT 모델에 CenterLoss를 적용한 IPC 자동분류 코드
- KorPatBERT를 사용한 모델
  - korpatbert.ipynb: KorPatBERT 모델을 이용한 IPC 자동분류 코드
  - **korpatbert-centerLoss.ipynb**: KorPatBERT 모델에 CenterLoss를 적용한 IPC 자동분류 코드
  - **test-korpatbert-centerLoss.ipynb**: KorPatBERT 모델에 CenterLoss를 적용한 IPC 자동분류 코드(테스트용)
  - korpatbert-centerLoss.h5: KorPatBERT 모델에 CenterLoss를 적용한 모델의 가중치 파일

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
