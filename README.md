# BDSP Docker Guideline

# 수정 중

```
docker1 page link
docker2 page link
docker3 page link
docker4 page link
```

<br>

---

<br>

## Hippocampus Docker 실행

### [[**참고 링크**]](https://github.com/bthyreau/hippodeep)

<br>

#### Docker 접속 명령어
```
docker run -it --network host --gpus all --shm-size=24G -v [Segmentation 대상 파일 경로]:/mnt bdsp/hippo_ecrf /bin/bash
```

#### Example
```
docker run -it --network host --gpus all --shm-size=24G -v /nasdata/T1_images/:/mnt bdsp/hippo_ecrf /bin/bash
```

### 접속 후 Hippocampus Segmentation 실행 명령어
```
cd /seg                         ⋯      Segmentation 실행 코드 경로 접속 명령어
sh deepseg1.sh ../mnt/          ⋯      코드 실행 명령어
```

### 실행 결과 

<img width="1694" alt="image" src="https://github.com/user-attachments/assets/47639e93-2c1f-489c-90f2-2332ceca2317">

<br>

---

<br>

## hdbet Docker 실행

### [[**참고 링크**]](https://github.com/MIC-DKFZ/HD-BET)

<br>

#### Docker 접속 명령어

```
docker run -it --network host --gpus all --shm-size=24G -v [Extraction 대상 파일 경로]:/mnt bdsp/hdbet_ecrf /bin/bash
```

#### Example
```
docker run -it --network host --gpus all --shm-size=24G -v /nasdata/T1_images/:/mnt bdsp/hdbet_ecrf /bin/bash
```

### 접속 후 Brain Extraction Tool 실행 명령어
```
cd HD_BET                                  ⋯      Extraction 실행 코드 경로 접속 명령어
hd-bet -i /mnt/                            ⋯      Extraction 실행 명령어 (입력 데이터 위치에 결과 데이터 출력)
hd-bet -i /mnt/ -o /mnt/[output_path]      ⋯      Extraction 실행 명령어 (지정한 위치에 결과 데이터 출력)
```

### 실행 결과

<img width="1593" alt="image" src="https://github.com/user-attachments/assets/6076afd9-c7d5-4e5e-9022-e31e5922cc19">

<br>

---

<br>

## haca3 Docker 실행

#### Docker 접속 명령어
```
docker run -it --network host --gpus all --shm-size=24G -v [Segmentation 대상 파일 경로]:/mnt haca3_ecrf /bin/bash
```

#### Example
```
docker run -it --network host --gpus all --shm-size=24G -v /nasdata/T1_images/:/mnt haca3_ecrf /bin/bash
```

### 접속 후 Hippocampus Segmentation 실행 명령어
```
cd /seg                         ⋯      Segmentation 실행 코드 경로 접속 명령어
sh deepseg1.sh ../mnt/          ⋯      코드 실행 명령어
```

<br>

---

<br>

## WMH Docker 실행

#### Docker 접속 명령어
```
docker run -it --network host --gpus all --shm-size=24G -v [Segmentation 대상 파일 경로]:/mnt pgs_wmh /bin/bash
```

#### Example
```
docker run -it --network host --gpus all --shm-size=24G -v /nasdata/T1_images/:/mnt pgs_wmh /bin/bash
```

### 접속 후 Hippocampus Segmentation 실행 명령어
```
cd /seg                         ⋯      Segmentation 실행 코드 경로 접속 명령어
sh deepseg1.sh ../mnt/          ⋯      코드 실행 명령어
```
