[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/3DbKuh4a)

# Dialogue Summarization | 일상 대화 요약

## Team NLP 4조

| ![박패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![이패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![최패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![김패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![오패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![오패캠](https://avatars.githubusercontent.com/u/156163982?v=4) |
|:-------------------------------------------------------------:|:-------------------------------------------------------------:|:-------------------------------------------------------------:|:-------------------------------------------------------------:|:-------------------------------------------------------------:|:-------------------------------------------------------------:|
| [강승현](https://github.com/UpstageAILab)                        | [김형수](https://github.com/UpstageAILab)                        | [이소영A](https://github.com/UpstageAILab)                       | [김창희](https://github.com/UpstageAILab)                        | [진성준](https://github.com/UpstageAILab)                        | [김하연](https://github.com/UpstageAILab)                        |
| 팀장                                                            | 팀원                                                            | 팀원                                                            | 팀원                                                            | 팀원                                                            | 팀원                                                            |

## 0. Overview

### Environment

- **(컴퓨팅 환경)** 인당 RTX 3090 서버를 VSCode와 SSH로 연결하여 사용
- **(협업 환경)** Github, Wandb
- **(의사 소통)** Slack, Zoom

## 1. Competiton Info

### Overview

- 이번 대회는 Dialogue Summurization 대회로 일상 대화로 이루어진 대화문의 요약을 생성하는 대회입니다.

### Timeline

- March 08, 2024 - Start Date
- March 20, 2024 - Final submission deadline

## 2. Components

### Directory

```
├── README.md
├── changhee
│   ├── DS-T5.ipynb
│   └── cleaning_data.ipynb
├── hayeon
│   ├── kobart_gogamza_keyword.ipynb
│   ├── kot5_keyword.ipynb
│   └── test.csv
├── hyperparameter-tuning
│   ├── hp_tuning_ver_2
│   ├── hp_tuning_ver_3.ipynb
│   └── optuna_hsk.ipynb
├── seongjun
│   └── t501_lora_inference.ipynb
└── soyoung
    └── baseline_kot5.ipynb
```

## 3. Data descrption

### Dataset overview

- 이번 대회에 사용된 데이터는 모두 대화문 데이터이며 train data, validation data, test data는 각각 12,457개, 499개, 250개 입니다. 각각의 대화문은 최소 2명에서 최대 7명의 화자가 등장하며, 최소 2턴에서 최대 60턴까지 대화가 이어집니다. 대화문에서 발화자는 #Person"N"#으로 구분되어있습니다.
- 대화문에 존재하는 개인정보(예: 전화번호, 주소 등)는 다음과 같이 마스킹되어 있습니다.
  - 예) 전화번호 -> #PhoneNumber#

### EDA

- Train data, validation data, test data 에 존재하는 #..# 형식의 단어: 
  
  - `['#Address#', '#CarNumber#', '#CardNumber#', '#DateOfBirth#', '#Email#', '#PassportNumber#', '#Person#', '#Person1#', '#Person2#', '#Person3#', '#Person4#', '#Person5#', '#Person6#', '#Person7#', '#PhoneNumber#', '#SSN#']`

- Train data, validation data, test data를 `kobart-summarization`으로 tokenized 했을 때 각 대화문과 요약문의 길이 정보
  
  |         | **Train Data**                                                                   | **Validation Data**                                                              | **Test Data**                                                                     |
  | ------- |:-------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
  | **대화문** | mean: 158.597014<br/>min: 32<br/>25%: 105<br/>50%: 141<br/>75%: 197<br/>max: 950 | mean: 156.687375<br/>min: 46<br/>25%: 104<br/>50%: 139<br/>75%: 194<br/>max: 620 | mean: 163.146293<br/>min: 38<br/>25%: 103<br/>50%: 149<br/>75%: 204<br/>max: 1041 |
  | **요약문** | mean: 30.980734<br/>min: 7<br/>25%: 21<br/>50%: 29<br/>75%: 38<br/>max: 165      | mean: 28.795591<br/>min: 9<br/>25%: 19<br/>50%: 26<br/>75%: 35<br/>max: 89       |                                                                                   |

### Data Processing

- 

## 4. Modeling

**김창희**

- Hugging face의 모델 `psyche/KoT5-summarization`, `lcw99/t5-large-korean-text-summary`, `eenzeenee/t5-base-korean-summarization`을 사용하여 테스트

- `psyche/KoT5-summarization`을 사용했을 때 Train loss는 0, Validation Loss가 고정되는 문제가 있어 transformer의 trainer를 사용하지 않고 직접 training function을 구현하여 학습을 하였지만 baseline의 `digit82/kobart-summarization` 보다 성능이 좋지 못함

- `lcw99/t5-large-korean-text-summary`, `eenzeenee/t5-base-korean-summarization`를 사용하였을 때 Validation Loss가 가장 낮게 나오는 `lcw99/t5-large-korean-text-summary`모델을 선택

**김형수**

- EDA 과정에서 데이터셋의 대화문과 요약문 최대 길이가 베이스라인 코드의 `encoder_max_len`와 `decoder_max_len`보다 긴 것을 확인하고, `encoder_max_len`, `decoder_max_len`, `generation_max_length` 값을 조절해가며 학습. 
  
  - 최초 `final_result` 41.6394에서 42.0135로 점수 소폭 상승

- 추가로 더 많은 `Seq2SeqTrainer`의 하이퍼파라미터를 조절하여 튜닝하기 위하여 `optuna` 라이브러리를 임포트하여 하이퍼파라미터 튜닝

- `Trainer` 클래스의 `hyperparameter_search` 메서드를 사용하여 하이퍼파라미터`learning_rate`, `per_device_train_batch_size`, `per_device_eval_batch_size`, `weight_decay`, `lr_scheduler_type`, `optim`를 튜닝.
  
  - 최종 결과: `final_result`=> 42.1127

**진성준**

- 이소영님 께서 공유해주신 모델 학습 후 lora 추가 학습 사용 모델
  
  - `noahkim/KoT5_news_summarization`
    
    - `"generation_max_length"`: 200,
    - `"encoder_max_len"`: 1000,  
    - `"decoder_max_len"`: 2000,  
  - `LoRA`
    
    ```python
    from peft import LoraConfig, TaskType, get_peft_model, PeftModellora_config = LoraConfig(  
    r=32,  
    target_modules=["q","v"],  
    bias="none",  
    task_type=TaskType.SEQ_2_SEQ_LM  
    )  
    lora_model = get_peft_model(generate_model, lora_config)  
    ```

- 최종 결과: `final_result` => 42.8141, `rouge2` => 0.3260,  `rougeL` => 0.4325

**김하연**

- Improvement of Dialogue Summarization Using Keyword Extractor 참고, 키워드 기반 생성 요약 진행
![image](https://github.com/UpstageAILab/upstage-nlp-summarization-nlp4/assets/106041730/616194aa-4391-40d2-a70f-08bb74873ca7)

- pretrained model : gogamza/kobart-summarization

- Dialogue, Topic을 학습시킨 모델로 Test Topic 생성, Dialogue, Topic, Summary를 학습시킨 모델로 Test Summary 생성
  
  - 최종 결과: `final_result` => 41.8308, `rouge1` => 0.5135, `rouge2` => 0.3181,  `rougeL` => 0.4233

## 5. Result

### Leader Board

- **Leader Board**
  
  <p align="center">
  <img src = "https://github.com/UpstageAILab/upstage-nlp-summarization-nlp4/assets/73140315/2f04b6ec-6ecd-4f39-998f-da990752a622" width="90%" height="90%">
  </p>
- **final_result**: 41.4034
  
  **rouge1**: 0.5153
  
  **rouge2**: 0.3079
  
  **rougeL**: 0.4189

### Presentation

- _Insert your presentaion file(pdf) link_

## etc

### Meeting Log

- _Insert your meeting log link like Notion or Google Docs_

### Reference

- _Insert related reference_
