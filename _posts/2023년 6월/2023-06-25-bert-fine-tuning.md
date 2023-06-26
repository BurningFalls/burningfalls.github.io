---
title: "[BERT] BERT fine-tuning: Multiclass Classification (Segment Analysis)"
excerpt: "BERT에게 58개의 감정 분류를 학습시키기 위해 fine-tuning을 수행한다."
date: 2023-6-25
last_modified_at: 2023-6-25
categories:
  - deep-learning
tags:
  - nlp
  - bert
  - fine-tuning
  - multiclass-classification
  - sentiment-analysis
---

## 0. 사용 코드 및 완성 모델

[Github link - burningfalls/fine-tuned-bert](https://github.com/BurningFalls/fine-tuned-bert)

[Hugging Face - burningfalls/my-fine-tuned-bert](https://huggingface.co/burningfalls/my-fine-tuned-bert) 

## 1. 모델 소개

이 글은 **BERT를 활용한 감정 분석 모델의 구현과 평가 결과**를 제시한다. 

`BERT(Bidirectional Encoder Representations from Transformers)`는 `자연어 처리(NLP)`를 위한 사전 학습(pre-trained) 모델 중 하나이다. 이 모델은 Google이 개발한 전이 학습 방법으로, Transformer라는 양방향 인코더를 기반으로 한다.

**BERT는 언어의 다양한 문맥과 의미를 이해**하기 위해 양방향으로 문장을 인코딩하는 능력을 갖추고 있다. BERT는 사전 학습과 `후속 작업(fine-tuning)`의 두 단계로 구성된다. 

사전 학습 단계에서는 대규모의 텍스트 데이터를 사용하여 모델의 파라미터가 사전 학습된다. 후속 작업 단계에서는 **사전 학습된 BERT 모델을 다양한 자연어 처리 작업에 맞게 세부적으로 조정**한다. 이를 위해 해당 작업에 맞는 데이터셋으로 모델을 추가로 학습시키는 과정을 거친다. 

`감정 분석(Sentiment Analysis)`, 문장 분류, 질문-답변 등 다양한 자연어 처리 작업에 BERT를 적용할 수 있다. BERT는 사전 학습된 언어 모델의 일종으로, 큰 양의 텍스트 데이터를 기반으로 다양한 자연어 처리 작업에 적용할 수 있는 강력한 기능을 제공한다. 

이 모델은 언어의 문맥을 이해하고, 문장의 의미를 추론하며, 문장 간의 관계를 파악하는 데에 매우 유용하다. 따라서, **BERT를 활용한 감정 분석 모델은 효과적으로 감정을 인식하고 분류하는 데에 활용될 수 있다.**

## 2. 데이터 전처리

### 2.1 데이터 불러오기

BERT를 사용한 감정 분석 fine-tuning을 위해, 문장과 문장의 감정에 대한 많은 데이터가 필요했다. 따라서, 이를 충족하는 **AI-Hub의 ‘감성 대화 말뭉치’ 데이터(Excel 파일)를 사용**했다. 

원래 데이터 구조는 [연령, 성별, 상황키워드, 신체질환, 감정_대분류, 감정_소분류, 사람문장1, 시스템문장1, 사람문장2, 시스템문장2, 사람문장3, 시스템문장3]로 이루어져 있다. **필요한 데이터는 문장과 그 문장의 상세한 감정 두 개** 이므로, [감정_소분류, 사람문장 1~3]를 선택했다. 사람문장을 `sentence`로, 감정_소분류를 `sub_sentiment`로 지정하였다. (만드는 과정에서 감정_대분류도 테스트하며 참고하였기 때문에, sentiment로 추출되어 있다.) 

아래는 Excel 데이터를 Pandas의 `read_excel` 함수를 통해 Dataframe 형태로 바꾼 데이터셋의 일부이다.

![dataset_sample](https://github.com/BurningFalls/algorithm-study/assets/30232837/8d3d34f8-d754-4394-84c0-68b196e40a73){: width="100%" height="100%"}{: .align-center}

### 2.2 결측값 및 중복 샘플 제거

```python
# 결측값 및 중복 샘플 제거
def drop_na_and_duplicates(df, col):
  df = df.dropna(how='any')
  df = df.drop_duplicates(subset=[col])
  df = df.reset_index(drop=True)
  return df

dataset = drop_na_and_duplilcates(dataset, dataset.colums[0])
```

불러온 데이터에서 결측값(`null`)을 가진 행을 제거하기 위해 `dropna` 함수를 사용하여 처리하였다. 이렇게 하여 데이터의 누락을 방지하고, 분석 작업에서의 오류를 예방했다. 또한, `drop_duplicates` 함수를 활용하여 sentence 열에서 중복된 샘플을 찾아 제거했다. 이를 통해, 중복으로 인한 데이터 왜곡을 방지하였다. 

이렇게 정제한 후의 결과로는 **총 144,723개의 데이터**가 남았다. 이는 충분한 양의 데이터로, 신뢰성 있는 감정 분석 모델의 학습에 적합하다고 할 수 있다. 데이터의 품질을 향상시키고 정확한 분석 결과를 얻기 위해, 결측값과 중복 샘플을 처리한 과정은 매우 중요했다.

![dataset_count](https://github.com/BurningFalls/algorithm-study/assets/30232837/655c9bdf-ed20-481f-bf5f-f79fc79ade92){: width="100%" height="100%"}{: .align-center}

### 2.3 라벨링 데이터와의 조인

`sub_sentiment`, 즉, 감정 소분류는 총 **58개의 감정을 포함**하고 있다. 이 58개의 감정은 아래 사진에 나와 있는 것과 동일하다. 각각의 감정은 1,500~2,500개의 데이터로 골고루 분포되어 있다.

![sentiment_count](https://github.com/BurningFalls/algorithm-study/assets/30232837/473c682e-fbd7-405f-a99f-2ad53c335c83){: width="100%" height="100%"}{: .align-center}

![sentiments](https://github.com/BurningFalls/algorithm-study/assets/30232837/a60eeabe-54f0-454d-9539-70eb74844eef){: width="100%" height="100%"}{: .align-center}

BERT Classification을 위해 분류를 숫자로 변환해야 했다. 따라서, 감정을 숫자로 라벨링하기 위해, 0부터 57까지의 라벨로 지정한 labeling Dataframe과 앞서 만든 dataset Dataframe을 Join 했다. dataset의 sub_sentiment 열과 labeling의 sentiment 열을 기준으로 조인해서, **[sentiment, label] 데이터프레임을 완성**시켰다. 아래는 데이터셋의 일부이다.

![dataset_sample](https://github.com/BurningFalls/algorithm-study/assets/30232837/b59db656-1471-42af-be20-13e8b82c6429){: width="100%" height="100%"}{: .align-center}

### 2.4 최대 문장 길이 설정

![max_seq_len](https://github.com/BurningFalls/algorithm-study/assets/30232837/b8e7e770-5f86-42e3-9fa8-8d4b924742b5){: width="100%" height="100%"}{: .align-center}

BERT에서는 `최대 문장 길이(max sequence length: max_seq_len)`를 일반적으로 64, 128, 256 등으로 설정한다. 이 데이터셋에서 가장 긴 문장의 길이는 156이다. 그러나, 길이가 128 초과 256 미만인 문장은 세 개로 매우 적다. 이에 따라, max_seq_len을 256으로 설정하면 padding이 많아져 메모리 사용량이 증가하고 성능도 저하될 수 있다. 그래서 **적절하게 128로 설정**했다. 
 
길이가 128을 초과하는 문장은 자동으로 잘려서 입력에 들어가게 된다. BERT 모델은 문장의 전반적인 의미를 이해하고 학습하기 때문에, 일반적으로 문장의 앞부분이 더 중요한 정보를 담고 있다. 따라서, 길이가 128을 넘어가는 부분은 잘려도 문장의 핵심 내용은 유지될 수 있다. 
 
이를 고려하여 적절한 최대 문장 길이를 설정하여 메모리 사용량을 효율적으로 관리하고 성능을 유지하는 것이 중요하다.

### 2.5 train/validation/test 데이터 분할

`훈련 집합(train set)`, `검증 집합(validation set)`, `테스트 집합(test set)`은 머신 러닝 모델을 학습하고 평가하기 위해 데이터를 분할하는 과정이다. 
 
**훈련 집합**은 모델을 학습하는 데 사용된다. 모델은 훈련 집합의 예제와 레이블을 사용하여 패턴을 학습하고 파라미터를 조정한다. 손실 함수를 최소화하고 최적의 가중치를 찾기 위해 훈련 집합을 사용한다. 
 
**검증 집합**은 모델의 성능을 평가하고 최적의 하이퍼파라미터를 선택하는 데 사용된다. 모델은 학습 중에 검증 집합의 예제와 레이블을 사용하여 성능을 평가한다. 이를 통해 `과적합(overfitting)`을 방지하고 일반화 성능을 추정한다. 모델의 학습 과정에서 검증 집합의 성능을 기준으로 `조기 종료(early stopping)` 등의 결정을 내릴 수 있다. 
 
**테스트 집합**은 최종 모델의 성능을 평가하기 위해 사용된다. 훈련과 검증을 마친 후, 모델의 성능을 신뢰성 있게 측정하기 위해 테스트 집합을 사용한다. 이는 모델이 이전에 보지 못한 데이터에 대해 얼마나 잘 일반화되는지 평가하는데 사용된다. 
 
데이터셋을 분할할 때 일반적인 규칙은 train, validation, test 데이터셋을 비율로 나누는 것이다. 일반적으로는 `6:2:2`의 비율로 분할되며, 훈련 집합은 전체 데이터의 약 60-80%를 차지하고, 검증 집합과 테스트 집합은 각각 전체 데이터의 약 10-20%를 차지한다. 이러한 비율은 일반화 성능을 최적화하기 위한 권장 비율이지만, 실제로는 데이터의 특성과 상황에 따라 조정될 수 있다.

```python 
from sklearn.model_selection import train_test_split

# train/validation/test dataset 분할
# train:val:test = 6:2:2
train_X, temp_X, train_y, temp_y = train_test_split(dataset_X, dataset_y, test_size=0.4, random_state=0)
val_X, test_X, val_y, test_y = train_test_split(temp_X, temp_y, test_size=0.5, random_state=0)
```

BERT fine-tuning에 사용할 데이터셋은 총 144,723개의 데이터로 구성되어 있다. 위에서 언급한 **권장 분할 비율 6:2:2에 따라 데이터셋을 분할**했다. 데이터 셋을 분할하기 위해 `sklearn.model_selection` 모듈의 `train_test_split` 함수를 사용했다. 이를 통해 `train_X`, `train_y`, `val_X`, `val_y`, `test_X`, `test_y`로 분할된 데이터를 얻을 수 있었다. 

또한, 분할 과정에서 `random_state` 파라미터를 사용하여 난수 발생기의 시드(seed)를 설정할 수 있다. 시드를 설정하면, 동일한 시드로 실행할 때마다 항상 동일한 분할 결과를 얻을 수 있어, 실험의 재현성을 보장할 수 있다. 

데이터가 감정별로 정렬되어 있었기 때문에 데이터를 무작위로 섞는 작업이 필요했다. 따라서, 특정 하이퍼파라미터 값을 변경하면서 최적의 값을 찾는 실험을 수행하고 일관성 있는 실험 결과를 얻기 위해 `random_state = 0`으로 설정했다.

![dataset_split](https://github.com/BurningFalls/algorithm-study/assets/30232837/8dfd7afa-89e2-436e-8c30-7bd59f49a16c){: width="100%" height="100%"}{: .align-center}

### 2.6 데이터셋 토크나이즈

```python
from transformers import BertTokenizerFast

tokenizer = BertTokenizerFast.from_pretrained("klue/bert-base", max_len=max_seq_len, truncation=True, padding=True)

train_X = tokenizer(train_X, truncation=True, padding=True)
val_X = tokenizer(val_X, truncation=True, padding=True)
```

​​BERT 모델에 입력으로 사용될 데이터를 tokenize하기 위해 `transformers` 라이브러리의 `BertTokenizerFast`를 활용했다. 이 과정에서 **klue/bert-base와 같은 사전 훈련된 BERT 모델의 tokenizer를 사용**했다. 해당 tokenizer를 활용하여 앞서 분할한 훈련 데이터셋의 입력 데이터(train_X)와 검증 데이터셋의 입력 데이터(val_X)를 전처리했다. 이를 통해 문장을 토큰화하고 특수 토큰(시작, 종료, 패딩)을 추가하여 BERT 모델의 입력 형식에 맞게 변환했다. 

또한, 훈련 데이터셋과 검증 데이터셋의 예측값(train_y, val_y)과 함께 (train_X, train_y), (val_X, val_y)를 쌍으로 묶고, 이를 `dictionary` 형태로 변환하여 데이터셋에 전달했다. 이렇게 구성된 데이터셋은 BERT 모델의 입력으로 사용될 수 있다.

## 3. 모델 파인튜닝

```python
from transformers import TFBertForSequenceClassification

optimizer = tf.keras.optimizers.Adam(learning_rate=2e-5)

model = TFBertForSequenceClassification.from_pretrained("klue/bert-base", num_labels=58, from_pt=True)
model.compile(optimizer=optimizer, loss=model.hf_compute_loss, metrics=['accuracy'])
```

BERT를 기반으로 한 sequence classification 모델을 학습하기 위해 `transformers` 라이브러리의 `TFBertForSequenceClassification` 모델을 활용했다. 이 과정에서 **사전 훈련된 BERT 모델 중 하나인 klue/bert-base의 모델을 불러왔다.** tokenize에 사용한 모델과 동일한 모델을 불러와야 호환성이 유지된다. 

**모델 학습에는 Adam이라는 현재 가장 많이 사용되는 최적화 알고리즘(optimizer)를 사용하였고, 학습률(learning rate)로는 2e-5(0.00002)를 설정**했다. 후술할 결과 분석에서 학습률에 따른 결과를 분석할 예정이다. `model.compile()`을 사용하여 모델을 컴파일할 때, 위에서 정의한 optimizer를 전달하고, 손실 함수(loss function)로는 모델의 `hf_compute_loss`를 사용했으며, 정확도를 측정하기 위해 `accuracy`를 설정했다.

```python
callback_earlystop = tf.keras.callbacks.EarlyStopping(
  monitor="val_accuracy",
  min_delta=0.001,
  patience=0
)
```

검증 세트의 정확도를 모니터링하고, 변화량(min_delta)이 0.001 이상 없을 경우 (patience) **조기 종료하는 EarlyStopping callback을 생성**했다. 변화량이 0.001 이상 없는 경우가 관찰되지 않았기 때문에, `patience`를 0으로 설정했다. (patience를 n(n≠0)으로 설정하면, 변화량이 0.001 이상 없는 경우가 n번 발생할 때까지 학습을 종료하지 않는다.) 

훈련 데이터셋과 검증 데이터셋은 `shuffle()` 함수를 사용하여 데이터를 섞은 후, `batch()` 함수를 사용하여 배치 크기를 `64`로 설정했다.

```python
model.fit(
  train_dataset, epochs=3, batch_size=64,
  validation_data = val_dataset,
  callbacks = [callback_earlystop]
)
```

최종적으로 전처리를 거친 train_dataset과 val_dataset, 불러온 모델, 정의한 callback을 활용하여 **model.fit()으로 모델을 훈련했다. epoch은 3으로 설정하고, batch size는 64로 설정했다.** epoch와 batch에 따른 결과 분석은 후술할 예정이다. 아래는 모델 훈련 결과 중 하나의 예시이다.

![model_training](https://github.com/BurningFalls/algorithm-study/assets/30232837/e164303f-e760-49f6-9207-8214628272c8){: width="100%" height="100%"}{: .align-center}

아래 내용은 **최적의 하이퍼파라미터 설정을 위해 값을 조정하면서 모델을 학습**시켰을 때의 분석 결과이다. `validation loss`가 감소하다가 증가하기 시작하는 시점에서 `overfitting`이 발생하므로, 해당 지점의 `validation accuracy`를 결과값으로 설정했다.

### 3.1 학습률 설정

![01-graph-bs-64-lr-5e3](https://github.com/BurningFalls/algorithm-study/assets/30232837/5cbd33d7-c9ab-4bd8-acd4-332e9a6c0fb6){: width="100%" height="100%"}{: .align-center}

![02-graph-bs-64-lr-1e3](https://github.com/BurningFalls/algorithm-study/assets/30232837/5807fe41-c834-40bc-95ff-321774c457ec){: width="100%" height="100%"}{: .align-center}

![03-graph-bs-64-lr-1e4](https://github.com/BurningFalls/algorithm-study/assets/30232837/5d59aa05-d5cb-4351-9ae0-5351549e711f){: width="100%" height="100%"}{: .align-center}

![04-graph-bs-64-lr-5e5](https://github.com/BurningFalls/algorithm-study/assets/30232837/93a6924c-0300-4dcd-815e-156d99df85f9){: width="100%" height="100%"}{: .align-center}

![05-graph-bs-64-lr-2e5](https://github.com/BurningFalls/algorithm-study/assets/30232837/3a712d4f-71c4-4063-a206-128c6e74aaa8){: width="100%" height="100%"}{: .align-center}

![06-graph-bs-64-lr-1e5](https://github.com/BurningFalls/algorithm-study/assets/30232837/ef9426c8-536a-4e4f-b830-0f7727a542bc){: width="100%" height="100%"}{: .align-center}

![07-graph-bs-64-lr-5e6](https://github.com/BurningFalls/algorithm-study/assets/30232837/da78490e-0f78-4eeb-9322-dc2e1ad4ac20){: width="100%" height="100%"}{: .align-center}

![08-graph-bs-64-lr-1e6](https://github.com/BurningFalls/algorithm-study/assets/30232837/e1db206b-4701-4c9f-8dc4-86f3d80e111b){: width="100%" height="100%"}{: .align-center}

![10-graph-bs-64](https://github.com/BurningFalls/algorithm-study/assets/30232837/d852c64e-adc7-4dff-a80a-566624af67be){: width="100%" height="100%"}{: .align-center}

다른 모든 파라미터를 고정시킨채로 `learning rate`만 변화시켜서 `epoch=10`으로 모델을 학습시켰다. 결과적으로 **learning rate가 2e-5일 때 accuracy가 0.2341로 가장 높음을 확인**할 수 있었다. 이를 토대로 최종적으로 `learning rate` 값을 `2e-5`로 설정했다. 추가적으로, 10 이후의 epoch에서는 유의미한 변화가 발견되지 않았으므로, 최대 epoch을 10으로 설정했다.

### 3.2 배치 사이즈 설정

![11-graph-bs-16-lr-2e5](https://github.com/BurningFalls/algorithm-study/assets/30232837/abaae11a-c988-4aeb-abc2-36002943e0ce){: width="100%" height="100%"}{: .align-center}

![12-graph-bs-32-lr-2e5](https://github.com/BurningFalls/algorithm-study/assets/30232837/2ea0ab87-cc1a-4085-9c34-1efd1f2bb297){: width="100%" height="100%"}{: .align-center}

![13-graph-bs-64-lr-2e5](https://github.com/BurningFalls/algorithm-study/assets/30232837/6c8ea17a-56a5-4499-9498-8735aaaac4d0){: width="100%" height="100%"}{: .align-center}

![14-graph-bs-128-lr-2e5](https://github.com/BurningFalls/algorithm-study/assets/30232837/d989201a-7ada-4410-b6f0-ab1ff7459a4e){: width="100%" height="100%"}{: .align-center}

![15-graph-lr-2e5](https://github.com/BurningFalls/algorithm-study/assets/30232837/ab8fd8ae-2f0a-4de0-bcf9-288ac83f659c){: width="100%" height="100%"}{: .align-center}

다른 모든 파라미터를 고정시킨채로 `batch size`만 변화시켜서 `epoch=10`으로 모델을 학습시켰다. 결과적으로 **batch size가 64일 때 accuracy가 0.2341로 가장 높음을 확인**할 수 있었다. 이를 바탕으로 최종적으로 `batch size` 값을 `64`로 설정했다. 추가적으로, 10 이후의 epoch에서는 유의미한 변화가 발견되지 않았으므로, 최대 epoch을 10으로 설정했다.

### 3.3 모델 정확도 분석

**sentiment classification을 위해 fine-tuning된 BERT 모델의 최대 정확도는 약 23.41%로 측정됐다.** 반면, fine-tuning 이전의 pre-trained 모델 `klue/bert-base`는 task classification(TC)에서 85.73%의 정확도를 보여준다. 

이 TC 작업은 두 개의 라벨(0과 1)만을 가지고 있기 때문에, 50%의 랜덤한 분류보다 우수한 성능을 보인다고 볼 수 있다. 그러나, 이 개발한 모델은 총 58개의 라벨을 가지고 있다. 따라서, 1/58 ≈ 0.0172 (약 1.72%)보다 훨씬 우수한 23.41%의 성능을 보여주고 있다. 

실제로 58개의 감정을 사람이 정확하게 구분하는 기준은 없으며, 개인마다 주관적인 감정 분류가 다를 수 있다. 따라서, BERT 모델의 출력 결과가 개인이 생각하는 정답(감정) 중에 포함된다면 맞다고 간주할 수 있다. 

이에 따라, **실제로 결과 값을 확인해본 결과, BERT 모델이 상당히 합리적인 감정 출력을 제공함을 확인할 수 있었다.** 아래는 최종 모델을 사용하여 도출해낸 결과 값인, 문장에서 추출한 감정의 예시이다.

![predict_examples](https://github.com/BurningFalls/algorithm-study/assets/30232837/1b2c5595-9b87-4abc-aec1-5c286de8bcb3){: width="100%" height="100%"}{: .align-center}

위 내용을 종합해보면, fine-tuning한 BERT 모델이 다양한 감정 분류 작업에서 상당히 신뢰할만한 성능을 보여주었다고 할 수 있다.

## 4. 모델 저장

```python
model.save_pretrained(MODEL_SAVE_PATH)
tokenizer.save_pretrained(MODEL_SAVE_PATH)
```

모델을 저장하기 위해 `model.save_pretrained()`와 `tokenizer.save_pretrained()` 함수를 사용했다. **저장한 모델은 다음과 같은 형태로 저장되었다.**

![predict_examples](https://github.com/BurningFalls/algorithm-study/assets/30232837/13c39ec2-ea4c-4980-a7d1-a5998add0809){: width="100%" height="100%"}{: .align-center}

1. `vocab.txt`: 이 파일은 BERT 모델이 이해하고 처리할 수 있는 모든 단어와 토큰들의 목록을 담고 있다. 모델 학습 과정에서 사용된 어휘와 인덱스 매핑 정보가 포함되어 있다.

1. `tokenizer_config.json`: 이 파일은 문장을 단어 또는 토큰 단위로 분리하는 역할을 담당하는 BERT 토크나이저의 구성(config)을 저장한다. 여기에는 토큰화 방법, 특수 토큰 처리 방식 등과 같은 config가 포함되어 있다.

1. `tokenizer.json`: 이 파일은 BERT 토크나이저의 내부 상태를 저장하며, 토크나이저 객체를 로드하고 사용하기 위한 정보를 담고 있다. 따라서, 모델을 훈련한 토크나이저 상태를 저장하고 있으며, 새로운 문장을 토큰화할 때 필요한 정보를 제공한다.

1. `tf_model.h5`: 이 파일은 BERT 모델의 가중치(weight)를 저장한 HDF5 파일이다. 모델의 신경망 가중치는 훈련된 모델의 핵심 요소로, 문장의 의미를 이해하고 예측을 수행하는데 사용된다.

1. `special_tokens_map.json`: 이 파일은 문장의 시작, 끝, 패딩 등과 같이 특별한 의미를 가지는 토큰인 특수 토큰(special token)에 대한 매핑 정보를 담고 있다.

1. `config.json`: 이 파일은 BERT 모델의 구성 정보를 저장한다. 모델의 아키텍처, 레이어 수, 히든 유닛 수 등과 같은 구성 정보가 포함되어 있다. 따라서, 모델을 로드하고 구성 정보를 확인하는데 사용된다.

## 5. 모델 불러오기

```python
# text classification을 위한 pipeline class import
from transformers import TextClassificationPipeline

# 저장했던 tokenizer, model을 불러옴
loaded_tokenizer = BertTokenizerFast.from_pretrained(MODEL_SAVE_PATH)
loaded_model = TFBertForSequenceClassification.from_pretrained(MODEL_SAVE_PATH)

# tokenizer, model을 pipeline에 할당
text_classifier = TextClassificationPipeline(
  tokenizer=loaded_tokenizer,
  model=loaded_model,
  framework='tf'
)

# pipeline 사용 예시
result = text_classifier("this is an example sentence")
predicted_label = result[0]['label']
predicted_score = result[0]['score']
```

모델을 불러오기 위해 `transformers` 라이브러리에서 텍스트 분류를 위한 파이프라인 클래스 `TextClassificationPipeline`을 import한다. 이 파이프라인을 사용하면, 텍스트 분류 모델을 쉽게 로드하고, 텍스트 입력에 대한 예측을 생성할 수 있다. `BertTokenizerFast.from_pretrained()`,`TFBertForSequenceClassification.from_pretrained()` 함수를 사용하여 저장한 모델을 불러왔다. 이때, 파이프라인 클래스에는 불러온 tokenizer와 model을 할당하고, framework를 `tf(tensorflow)`로 설정했다. 이렇게 **설정된 텍스트 분류 파이프라인(TextClassificationPipeline)은 입력 문장을 전달하여 해당 문장의 클래스 레이블 및 점수를 예측하는데 사용**됐다.

## 6. 모델 예측

앞서 분리해서 만든 테스트 데이터셋(28945개)을 입력으로 사용해서, 이전에서 생성한 파이프라인을 사용하여 모델의 예측을 수행한다. 아래는 일부 예시이다.

![predict_examples](https://github.com/BurningFalls/algorithm-study/assets/30232837/737d3693-59a6-4560-b037-36b9f48aca6e){: width="100%" height="100%"}{: .align-center}

위와 같이 **텍스트를 입력으로 주고, 모델은 해당 문장의 클래스 레이블과 예측 점수를 출력한다. 이를 통해, 모델이 주어진 문장에 대해 어떤 감정을 예측하는지 확인할 수 있다.**

## 7. 모델 평가

모델을 평가하기 위해 `sklearn.metric` 라이브러리의 `classification_report` 함수를 사용했다. 이 함수를 사용하여 이전에서 도출된 결과를 각각 `y_true`와 `y_pred`에 대입시켜 평가 결과를 측정했다. 측정값은 다음과 같다.

![evaluate_result](https://github.com/BurningFalls/algorithm-study/assets/30232837/18c59692-2f3e-4f6b-be4f-79575e7ece8c){: width="100%" height="100%"}{: .align-center}

1. `precision`(정밀도): 정밀도는 “양성”으로 예측한 샘플 중에서 실제로 “양성”인 샘플의 비율을 나타낸다. 즉, 모델이 “양성” 클래스를 얼마나 정확하게 예측하는지를 나타내는 지표이다. 정밀도 공식은 다음과 같다. ‘(정밀도)=TP/(TP+FP)’. 여기서 TP는 “양성”으로 예측하고 실제로 “양성”인 샘플의 수이고, FP는 “양성”으로 예측했지만 실제로는 “음성”인 샘플의 수이다.

1. `recall`(재현율): 재현율은 실제 “양성”인 샘플 중에서 모델이 “양성”으로 예측한 샘플의 비율을 나타낸다. 즉, 모델이 실제 “양성”인 샘플을 얼마나 잘 찾아내는지를 나타내는 지표이다. 재현율 공식은 다음과 같다. ‘(재현율)=TP/(TP+FN)’. 여기서 TP는 위와 동일하고, FN은 “음성”으로 예측했지만 실제로는 “양성”인 샘플의 수이다.

1. `f1-score`(F1 점수): F1 점수는 정밀도와 재현율의 조화 평균으로, 정밀도와 재현율을 동시에 고려하여 모델을 평가하는 지표로 사용된다. F1-score 공식은 다음과 같다. ‘(F1-score)=2*(precision*recall)/(precision+recall)’. F1-score는 정밀도와 재현율이 균형을 이룰 때, 가장 높은 값을 갖는다.

1. `support`: Support는 각 클래스별로 실제로 존재하는 샘플의 수를 의미한다.

1. `accuracy`(정확도): accuracy는 전체 샘플 중에서 올바르게 예측한 샘플의 비율을 나타낸다. 위에서 accuracy가 0.23으로 나타나고 있다. 이는 모델이 전체 샘플 중에서 약 23%만큼의 샘플을 정확하게 예측했다는 것을 의미한다.

1. `macro average`(매크로 평균): macro average는 각 클래스에 대한 지표들의 평균을 계산한 값이다. 위에서 macro average가 0.24, 0.23, 0.23으로 각각 표시되어 있다. 이 값들은 precision, recall, f1-score에 대한 macro average를 나타내며, 각 클래스의 성능을 동일한 가중치로 고려한 결과이다.

1. `weighted average`(가중 평균): weighted average는 각 클래스에 대한 지표들을 해당 클래스의 샘플 수로 가중치를 주어 계산한 평균값이다. 위에서 weighted average가 0.24, 0.23, 0.23으로 각각 표시되어 있다. 이 값들은 precision, recall, f1-score에 대한 weighted average를 나타내며, 각 클래스의 샘플 수에 따라 가중치를 부여한 결과이다.

## 8. 모델 원격 저장소에 올리기

`Hugging Face`는 자연어 처리 모델을 저장하고 공유할 수 있는 온라인 플랫폼이다. 사용자들은 Hugging Face를 통해 다양한 사전 훈련된 모델, 토크나이저, 임베딩, 데이터셋 등을 찾고 활용할 수 있으며, 자신이 훈련한 모델을 업로드하여 커뮤니티와 공유할 수도 있다. 

또한, Hugging Face는 github처럼 버전 관리를 지원하여 모델 및 자원이 이전 버전과 비교하고 효율적으로 작업할 수 있도록 도와준다. 이를 통해 자연어 처리 커뮤니티와의 협력과 지식 공유를 촉진하여 자연어 처리 작업을 보다 효율적으로 진행할 수 있다.

훈련한 BERT 모델을 웹 서버에 배포하는 것이 목표였지만, 대용량의 딥러닝 모델 파일을 로컬에 보유하고 있는 것은 어려움이 있었다. 또한, Github에 업로드하기 어려운 큰 파일이었다. 이러한 이유로 Hugging Face의 방식을 사용하여 모델을 업로드하기로 결정했다. **모델은 Hugging Face의 모델 저장소에 업로드되었다.**

[Hugging Face - burningfalls/my-fine-tuned-bert](https://huggingface.co/burningfalls/my-fine-tuned-bert) 

이를 통해, 로컬에 딥러닝 모델 파일을 보유하지 않고도, 몇 줄의 코드로 모델을 로드하고 사용할 수 있게 되었다.

![huggingface](https://github.com/BurningFalls/algorithm-study/assets/30232837/74d26e29-9cba-43e3-b63d-7b70e3e422f1){: width="100%" height="100%"}{: .align-center}

BERT 모델을 로드하는 방식도 약간 변경되었다. 이전에는 로컬에 저장된 모델 위치인 `MODEL_SAVE_PATH`에서 가져왔지만, 현재는 서버에서 직접 가져온다. 변경된 방법은 다음과 같다.

```python
from transformers import AutoTokenizer, TFAutoModelForSequenceClassification

BERT_PATH = "burningfalls/my-fine-tuned-bert"

loaded_tokenizer = AutoTokenizer.from_pretrained(BERT_PATH)
loaded_model = TFAutoModelForSequenceClassification.from_pretrained(BERT_PATH)
```

위와 같이 코드를 작성하면, Hugging Face에 업로드된 모델을 로드하여 사용할 수 있다.