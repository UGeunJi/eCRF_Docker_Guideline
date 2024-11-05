# :brain: BDSP Docker Guideline :kr:

## Section Jump Link
  
- [Hippocampus Segmentation Docker](#hippocampus-segmentation-docker)
- [hdbet Extraction Docker](#hdbet-extraction-docker)
- [haca3 Harmonization Docker](#haca3-harmonization-docker)
- [WMH Segmentation Docker](#wmh-segmentation-docker)

<br>

<p align="center">
  <img width="700" alt="image" src="https://github.com/user-attachments/assets/15e17fbd-87b5-4753-9026-c494f5ee937c">
</p>

<br>

---

<br>

## Hippocampus Segmentation Docker

### [[**Reference Link**]](https://github.com/bthyreau/hippodeep)

<br>

### Recommended Preprocessing Step

```
1. N4 Bias Correlation       ⋯      This will improve the model's performance
```

#### Docker Access Command :whale2:

```
docker run -it --network host --gpus all --shm-size=24G -v [Segmentation Subject Files Path]:/mnt hippo_seg /bin/bash
```

#### Example

```
docker run -it --network host --gpus all --shm-size=24G -v /nasdata/T1_images/:/mnt hippo_ecrf /bin/bash
```

### Hippocampus Segmentation Execution Commands after Access

```
cd /seg                         ⋯      Segmentation Execution Code Path Access Command
sh deepseg1.sh ../mnt/          ⋯      Code Execution Command
```

### Segmentation Result Save Path

```
It is saved in thed path of the executable target file.
```

### Result 

<img width="1694" alt="image" src="https://github.com/user-attachments/assets/47639e93-2c1f-489c-90f2-2332ceca2317">

<br>

---

<br>

## hdbet Extraction Docker

### [[**Reference Link**]](https://github.com/MIC-DKFZ/HD-BET)

<br>

### Recommanded Preprocessing Steps

```
1. N4 Bias Correlation       ⋯      This will improve the model's performance
```

#### Docker Execution Command :whale2:

```
docker run -it --network host --gpus all --shm-size=24G -v [Extraction 대상 파일 경로]:/mnt vnmd/hdbet_bdsp /bin/bash
```

#### Example

```
docker run -it --network host --gpus all --shm-size=24G -v /nasdata/T1_images/:/mnt vnmd/hdbet_bdsp /bin/bash
```

### Brain Extraction Tool Execution Commands after Access

```
cd HD_BET                                  ⋯      Extraction Execution Code Path Access Command
hd-bet -i /mnt/                            ⋯      Extraction Execution Command (Output result data at the input data path)
hd-bet -i /mnt/ -o /mnt/[output_path]      ⋯      Extraction Execution Command (Output result data to a specified path)
```

### Extraction Result Save Path
```
When executing the 'hd-bet -i /mnt/', it is saved in the execution target file path.
When executing the 'hd-bet -i /mnt/ -o /mnt/[output_path]', it is saved in '/mnt/[output_path]'.
```

### Result

<img width="1593" alt="image" src="https://github.com/user-attachments/assets/6076afd9-c7d5-4e5e-9022-e31e5922cc19">

<br>

---

<br>

## haca3 Harmonization Docker

### Essential Preprocessing Steps

```
1. N4 Bias Correlation
2. MNI152 Registration
```

#### Docker Execution Command :whale2:

```
docker run --rm --gpus all -it -v [Harmonization Subject Files Path]:/workspace haca3cna_v2
```

#### Example

```
docker run --rm --gpus all -it -v /nasdata/T1_images/:/workspace haca3cna_v2
```

### Harmonization Execution Commands after Access

```
cd ..                               ⋯       Access Path
python reshape.py /workspace/       ⋯       execute code to zero pad an image to the MNI152 template

# Harmonization Execution Command
haca3-test --in-path /workspace/D11004_COR_3D_T1_FSPGR_20151015083508_9_N4_resample_lin.nii.gz --target-image /workspace/N110132_Sag_IR-FSPGR_20220316124202_3_N4_lin.nii.gz --harmonization-model /pretrained_weights/CNA_onlyT1w_model.pt --fusion-model /pretrained_weights/fusion.pt --out-path /workspace/D11004_COR_3D_T1_FSPGR_20151015083508_9_N4_resample_lin.nii.gz --intermediate-out-dir /workspace/intermidate
```

### Result

<img width="574" alt="image" src="https://github.com/user-attachments/assets/635555b1-22fe-4442-9c28-846dce3c4f5b">

<br>

---

<br>

## WMH Segmentation Docker

### Essential Preprocessing Steps

```
1. N4 Bias Correlation
2. T1, FLAIR Co-Registration
3. Brain Extraction (ROBEX, hdbet, ...)
  - Use the flirt commnad by default.
  - flirt -dof 6 -in subject_T1.nii -ref subject_FLAIR.nii -out subject_T1_to_FLAIR -omat subject_T1_to_FLAIR.mat

Ex) flirt -dof 6 -in /nasdata3/cohort_FLAIR_2022-1/T1_N4/GH/L1_GH_04935_native_N4.nii -ref /nasdata3/cohort_FLAIR_2022-1/FLAIR/GH/L1_GH_04935/L1_GH_04935_FLAIR.nii -out /nasdata3/cohort_FLAIR_2022-1/FLAIR/GH/L1_GH_04935/T1_to_FLAIR -omat /nasdata3/cohort_FLAIR_2022-1/FLAIR/GH/L1_GH_04935/T1_to_FLAIR.mat
```

#### Docker Execution Command :whale2:

```
docker run -it --network host --gpus all --shm-size=24G -v [Segmentation 대상 파일 경로]:/mnt pgs_wmh_gpu_v1 /bin/bash
```

#### Example

```
docker run -it --network host --gpus all --shm-size=24G -v /nasdata/T1_and_FLAIR_images/:/mnt pgs_wmh_gpu_v1 /bin/bash
```

### WMH Segmentation Execution Command after Access

```
# WMH segmentation Execution Command Format
python WMHs_segmentation_PGS_gpu_division.py [subject_brain.nii] [subject_brain_mask.nii] [subject_FLAIR.nii] [subject_WMH.nii] [GPU_number]                         ⋯      

# WMH segmentation Execution Command Format Example
python WMHs_segmentation_PGS_gpu_division.py ${sub_fold}_brain.nii ${sub_fold}_brain_mask.nii ${sub_fold}_FLAIR.nii ${sub_fold}/${sub_fold}_WMH.nii 5
```

### Result

<img width="1375" alt="image" src="https://github.com/user-attachments/assets/6ce9bf5c-c7cc-4d2b-b3c2-810b4cdf7012">
