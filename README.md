# 도로 파손 객체 탐지 (Road Damage Object Detection) - YOLOv8

도로 이미지에서 **Pothole(포트홀)**, **Crack(균열)**, **Manhole(맨홀)** 을 탐지하는 Object Detection 프로젝트입니다. Ultralytics YOLOv8을 기반으로 학습하였으며, 모델 크기(YOLOv8n vs YOLOv8s)에 따른 성능 비교 실험을 포함합니다.

## 프로젝트 구조
Computer-Vision-Project_team8
│
├── road_damaged_YOLO.ipynb
├── README.md
├── dataset/
      ├── dataset.zip
      └── dataset.z01 ~ dataset.z07 

## 프로젝트 개요

| 항목 | 내용 |
|---|---|
| Task | Object Detection (도로 파손 종류 및 위치 탐지) |
| 클래스 | 0: Pothole, 1: Crack, 2: Manhole |
| Baseline 모델 | YOLOv8n |
| 비교 모델 | YOLOv8s |
| 데이터 분할 | Train 70% / Val 20% / Test 10% |
| 평가 지표 | Precision, Recall, mAP50, mAP50-95 |
| 실행 환경 | Google Colab (GPU: Tesla T4) |

## 데이터셋

- **이름**: Road Damage Dataset: Potholes, Cracks and Manholes
- **출처**: [Kaggle](https://www.kaggle.com/datasets/lorenzoarcioni/road-damage-dataset-potholes-cracks-and-manholes)
- **구성**: 이미지 2,009장 + YOLO 형식 라벨(`class_id x_center y_center width height`) 2,009개, 모든 이미지-라벨 1:1 매칭 확인됨
- **클래스 3종**: `0 Pothole`, `1 Crack`, `2 Manhole`

> 데이터는 `dataset/` 폴더에 분할 압축 파일(`dataset.zip`, `dataset.z01` ~ `dataset.z07`)로 포함되어 있지만, **노트북의 데이터 다운로드 셀(`kagglehub.dataset_download(...)`)을 실행해서 받는 것을 추천합니다.** 분할 압축 파일은 8개를 모두 같은 폴더에 받아 압축 해제 프로그램으로 합쳐야 하는 번거로움이 있는 반면, 다운로드 셀을 실행하면 위 Kaggle 링크의 데이터셋을 자동으로 받아 바로 사용할 수 있습니다.

## 실행 환경 및 실행 방법

본 노트북은 **Google Colab 환경**을 기준으로 작성되었습니다.

1. 'road_damaged_YOLO.ipynb'를 Google Colab에서 엽니다.
2. 런타임 유형을 GPU로 설정합니다.
3. 셀을 순서대로 실행합니다.
   - 셀 1~3: 라이브러리 설치 및 Kaggle 데이터셋 다운로드
   - 셀 4~16: 데이터 탐색, 시각화, train/val/test 분할
   - 셀 17~18: YOLOv8n 학습
   - 셀 19~23: 평가 및 예측 결과 저장
   - 셀 24: Confidence Threshold 비교 실험
   - 셀 25~27: YOLOv8s 추가 학습 및 모델 비교
   - 셀 28: 실험 설정 요약 출력

## 산출물

학습/평가 과정에서 아래와 같은 시각화 자료가 생성됩니다.

- 클래스 분포 그래프 ('class_distribution.png')
- 이미지당 객체 수 분포 ('objects_per_image_distribution.png')
- 라벨 시각화 예시 ('sample_labeled_images.png')
- 예측 결과 예시 ('prediction_samples.png')
- 학습 곡선 ('results.png')
- Confusion Matrix, PR Curve, F1 Curve
- 모델 비교 그래프 ('model_performance_comparison.png')
