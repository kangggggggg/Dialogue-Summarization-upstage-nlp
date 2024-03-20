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

### Model descrition

- _Write model information and why your select this model_

### Modeling Process

- _Write model train and test process with capture_

## 5. Result

### Leader Board

- _Insert Leader Board Capture_
- _Write rank and score_

### Presentation

- _Insert your presentaion file(pdf) link_

## etc

### Meeting Log

- _Insert your meeting log link like Notion or Google Docs_

### Reference

- _Insert related reference_
