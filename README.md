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

#### Docker 접속 명령어
```
docker run -it --network host --gpus all --shm-size=24G -v [Segmentation 대상 파일 경로]:/mnt hippo_ecrf /bin/bash
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

<br>

---

<br>


## hdbet Docker 실행

#### Docker 접속 명령어
```
docker run -it --network host --gpus all --shm-size=24G -v [Segmentation 대상 파일 경로]:/mnt hdbet_ecrf /bin/bash
```

#### Example
```
docker run -it --network host --gpus all --shm-size=24G -v /nasdata/T1_images/:/mnt hdbet_ecrf /bin/bash
```

### 접속 후 Hippocampus Segmentation 실행 명령어
```
cd /seg                         ⋯      Segmentation 실행 코드 경로 접속 명령어
sh deepseg1.sh ../mnt/          ⋯      코드 실행 명령어
```

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
