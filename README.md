# BDSP Docker Guideline


  
- [Hippocampus Segmentation Docker](#HippocampusSegmentationDocker실행)
- [hdbet Extraction Docker](##hdbetExtractionDocker실행)
- [haca3 Harmonization Docker](##haca3HarmonizationDocker실행)
- [WMH Segmentation Docker](##WMHSegmentationDocker실행)

<p align="center">
  <img width="900" alt="image" src="https://github.com/user-attachments/assets/15e17fbd-87b5-4753-9026-c494f5ee937c">
</p>

<br>

---

<br>

## Hippocampus Segmentation Docker 실행

### [[**참고 링크**]](https://github.com/bthyreau/hippodeep)

<br>

### 권장 전처리 과정

```
1. N4 Bias Correlation
```

#### Docker 접속 명령어 :whale2:
```
docker run -it --network host --gpus all --shm-size=24G -v [Segmentation 대상 파일 경로]:/mnt hippo_seg /bin/bash
```

#### Example
```
docker run -it --network host --gpus all --shm-size=24G -v /nasdata/T1_images/:/mnt hippo_ecrf /bin/bash
```

### 접속 후 Hippocampus Segmentation 실행 명령어
```
cd /seg                         ⋯      Segmentation 실행 코드 경로 접속 명령어
sh deepseg1.sh ../mnt/          ⋯      코드 실행 명령어
```

### Segmentation 결과 저장 경로
```
실행 대상 파일 경로에 저장됩니다.
```

### 실행 결과 

<img width="1694" alt="image" src="https://github.com/user-attachments/assets/47639e93-2c1f-489c-90f2-2332ceca2317">

<br>

---

<br>

## hdbet Extraction Docker 실행

### [[**참고 링크**]](https://github.com/MIC-DKFZ/HD-BET)

<br>

### 권장 전처리 과정

```
1. N4 Bias Correlation
```

#### Docker 접속 명령어 :whale2:

```
docker run -it --network host --gpus all --shm-size=24G -v [Extraction 대상 파일 경로]:/mnt vnmd/hdbet_bdsp /bin/bash
```

#### Example

```
docker run -it --network host --gpus all --shm-size=24G -v /nasdata/T1_images/:/mnt vnmd/hdbet_bdsp /bin/bash
```

### 접속 후 Brain Extraction Tool 실행 명령어

```
cd HD_BET                                  ⋯      Extraction 실행 코드 경로 접속 명령어
hd-bet -i /mnt/                            ⋯      Extraction 실행 명령어 (입력 데이터 위치에 결과 데이터 출력)
hd-bet -i /mnt/ -o /mnt/[output_path]      ⋯      Extraction 실행 명령어 (지정한 위치에 결과 데이터 출력)
```

### Extraction 결과 저장 경로
```
'hd-bet -i /mnt/' 명령어 실행 시, 실행 대상 파일 경로에 저장됩니다.
'hd-bet -i /mnt/ -o /mnt/[output_path]' 명령어 실행 시, '/mnt/[output_path]' 경로에 저장됩니다.

```

### 실행 결과

<img width="1593" alt="image" src="https://github.com/user-attachments/assets/6076afd9-c7d5-4e5e-9022-e31e5922cc19">

<br>

---

<br>

## haca3 Harmonization Docker 실행

### 필수 전처리 과정

```
1. N4 Bias Correlation
2. MNI152 Registration
```

#### Docker 접속 명령어 :whale2:

```
docker run --rm --gpus all -it -v [Harmonization 대상 파일 경로]:/workspace haca3cna_v2
```

#### Example

```
docker run --rm --gpus all -it -v /nasdata/T1_images/:/workspace haca3cna_v2
```

### 접속 후 T1 Harmonization 실행 명령어

```
cd ..                               ⋯       경로 이동
python reshape.py /workspace/       ⋯       MNI152 template에 맞춰진 이미지 zero padding 해주는 코드 실행
# Harmonization 실행 명령어
haca3-test --in-path /workspace/D11004_COR_3D_T1_FSPGR_20151015083508_9_N4_resample_lin.nii.gz --target-image /workspace/N110132_Sag_IR-FSPGR_20220316124202_3_N4_lin.nii.gz --harmonization-model /pretrained_weights/CNA_onlyT1w_model.pt --fusion-model /pretrained_weights/fusion.pt --out-path /workspace/D11004_COR_3D_T1_FSPGR_20151015083508_9_N4_resample_lin.nii.gz --intermediate-out-dir /workspace/intermidate
```

### 실행 결과

<img width="574" alt="image" src="https://github.com/user-attachments/assets/635555b1-22fe-4442-9c28-846dce3c4f5b">

<br>

---

<br>

## WMH Segmentation Docker 실행

### 필수 전처리 과정

```
1. N4 Bias Correlation
2. T1, FLAIR Co-Registration
3. Brain Extraction (ROBEX, hdbet, ...)
  - 기본적으로 flirt 명령어 사용.
  - flirt -dof 6 -in subject_T1.nii -ref subject_FLAIR.nii -out subject_T1_to_FLAIR -omat subject_T1_to_FLAIR.mat

Ex) flirt -dof 6 -in /nasdata3/cohort_FLAIR_2022-1/T1_N4/GH/L1_GH_04935_native_N4.nii -ref /nasdata3/cohort_FLAIR_2022-1/FLAIR/GH/L1_GH_04935/L1_GH_04935_FLAIR.nii -out /nasdata3/cohort_FLAIR_2022-1/FLAIR/GH/L1_GH_04935/T1_to_FLAIR -omat /nasdata3/cohort_FLAIR_2022-1/FLAIR/GH/L1_GH_04935/T1_to_FLAIR.mat
```

#### Docker 접속 명령어 :whale2:

```
docker run -it --network host --gpus all --shm-size=24G -v [Segmentation 대상 파일 경로]:/mnt pgs_wmh_gpu_v1 /bin/bash
```

#### Example

```
docker run -it --network host --gpus all --shm-size=24G -v /nasdata/T1_and_FLAIR_images/:/mnt pgs_wmh_gpu_v1 /bin/bash
```

### 접속 후 WMH Segmentation 실행 명령어

```
# WMH segmentation 실행 명령어 format
python WMHs_segmentation_PGS_gpu_division.py [subject_brain.nii] [subject_brain_mask.nii] [subject_FLAIR.nii] [subject_WMH.nii] [GPU_number]                         ⋯      

# WMH segmentation 실행 명령어 format 예시
python WMHs_segmentation_PGS_gpu_division.py ${sub_fold}_brain.nii ${sub_fold}_brain_mask.nii ${sub_fold}_FLAIR.nii ${sub_fold}/${sub_fold}_WMH.nii 5
```

### 실행 결과

<img width="1375" alt="image" src="https://github.com/user-attachments/assets/6ce9bf5c-c7cc-4d2b-b3c2-810b4cdf7012">
