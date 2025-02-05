# :brain: eCRF Docker Guideline :kr:

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

## :brain: Hippocampus Segmentation Docker

### [[Docker Hub Link]](https://hub.docker.com/r/ajtwlsdnrms/hippo_seg)

### [[**Reference Link**]](https://github.com/bthyreau/hippodeep)

## Experiment Environment

```
GPU Model: NVIDIA A40
NVIDIA Driver Version: 535.161.08
Supply CUDA Version: 12.2
CPU RAM: 65368064 KiB total

Run-time on GPU: 13 s per subject
```

<br>

### Recommended Preprocessing Step

(Optional) These will improve the model's performance, and conversely, not performing the task may lead to poor results.

```
1. N4 Bias Correction      
2. Registration
```

### Detailed description of preprocessing

#### - N4 Bias Correction

- Bias Field in MRI image refers to the non-uniformity of signal intensity (illumination distortion) within the image.
- These bias fields are caused by various factors such as the device, scanning environment, and characteristics of biological tissue, and they affect the global brightness pattern of the image.
- It is necessary to improve the illumination uniformity of MRI and increase the accuracy of Hippocampus segmentation. This standardizes the model input data by reducing the variation of illumination intensity within the image.

<p align="center">
  <img width="400" alt="image" src="https://github.com/user-attachments/assets/82f40460-cdcf-436b-b7bc-218c275e9eb4">
</p>

<p align="center">
  N4 Bias field correction principle
</p>

<br>

#### - Registration

- Each patient or subject's MRI may have different posture, size, and orientation when scanned. These differences make it difficult to directly compare the brain structure of one subject with that of another.
- Align the input data to a standard space to ensure that model can more accurately segment the hippocampus structure of various subjects. In general, it is recommended to align to the Montreal Neurological Institute (MNI) space.

<p align="center">
  <img width="500" alt="image" src="https://github.com/user-attachments/assets/00a28a55-b3b0-4300-9ba8-0cadc80babfe">
</p>

<p align="center">
  Images before and after alignment with MNI template
</p>

<p align="right">
  (Red color: MNI Template)
</p>

<br>

### Docker Access Command :whale2:

```
docker run -it --network host --gpus all -v [Segmentation Subject Files Path]:/mnt hippo_seg /bin/bash
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

<p align="center">
  <img width="1694" alt="image" src="https://github.com/user-attachments/assets/5934d330-1264-4a5e-b4d8-5fecbc47013b">
</p>

<p align="right">
  (Red color: Segmented Hippocampus)
</p>

<br>

---

<br>

## :brain: hdbet Extraction Docker

### [[Docker Hub Link]](https://hub.docker.com/r/ajtwlsdnrms/hdbet)

### [[**Reference Link**]](https://github.com/MIC-DKFZ/HD-BET)

## Experiment Environment

```
GPU Model: NVIDIA A40
NVIDIA Driver Version: 535.161.08
Supply CUDA Version: 12.2
CPU RAM: 65368064 KiB total

Run-time on GPU: 43 s per subject
```

<br>

### Recommanded Preprocessing Steps

(Optional) These will improve the model's performance, and conversely, not performing the task may lead to poor results.

```
1. N4 Bias Correction      
2. Registration
```

### Detailed description of preprocessing

#### - N4 Bias Correction

- Bias Field in MRI image refers to the non-uniformity of signal intensity (illumination distortion) within the image.
- These bias fields are caused by various factors such as the device, scanning environment, and characteristics of biological tissue, and they affect the global brightness pattern of the image.
- It is necessary to improve the illumination uniformity of MRI and increase the accuracy of Hippocampus segmentation. This standardizes the model input data by reducing the variation of illumination intensity within the image.

<p align="center">
  <img width="400" alt="image" src="https://github.com/user-attachments/assets/82f40460-cdcf-436b-b7bc-218c275e9eb4">
</p>

<p align="center">
  N4 Bias field correction principle
</p>

<br>

#### - Registration

- Each patient or subject's MRI may have different posture, size, and orientation when scanned. These differences make it difficult to directly compare the brain structure of one subject with that of another.
- Align the input data to a standard space to ensure that model can more accurately segment the hippocampus structure of various subjects. In general, it is recommended to align to the Montreal Neurological Institute (MNI) space.

<p align="center">
  <img width="500" alt="image" src="https://github.com/user-attachments/assets/00a28a55-b3b0-4300-9ba8-0cadc80babfe">
</p>

<p align="center">
  Images before and after alignment with MNI template
</p>

<p align="right">
  (Red color: MNI Template)
</p>

<br>

### Docker Execution Command :whale2:

```
docker run -it --network host --gpus all -v [Extraction Subject Files Path]:/mnt vnmd/hdbet_bdsp /bin/bash
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

<p align="center">
  <img width="1593" alt="image" src="https://github.com/user-attachments/assets/60bb5491-f1e2-4aca-9d30-4f6d75c71a6f">
</p>

<p align="right">
  (Red color: Extracted Brain)
</p>

<br>

---

<br>

## :brain: haca3 Harmonization Docker

### [[Docker Hub Link]](https://hub.docker.com/r/ajtwlsdnrms/haca3cna_v2)

## Experiment Environment

```
GPU Model: NVIDIA A40
NVIDIA Driver Version: 535.161.08
Supply CUDA Version: 12.2
CPU RAM: 63836.0 MiB total

Run-time on GPU: 10 s per subject
```

### Essential Preprocessing Steps

(Essential) This steps are essential for the performance of the model, and if not performed, you will definitely get poor results.

```
1. N4 Bias Correction
2. MNI152 Registration
```

### Detailed description of preprocessing

#### - N4 Bias Correction

- Bias Field in MRI image refers to the non-uniformity of signal intensity (illumination distortion) within the image.
- These bias fields are caused by various factors such as the device, scanning environment, and characteristics of biological tissue, and they affect the global brightness pattern of the image.
- It is necessary to improve the illumination uniformity of MRI and increase the accuracy of Hippocampus segmentation. This standardizes the model input data by reducing the variation of illumination intensity within the image.

<p align="center">
  <img width="400" alt="image" src="https://github.com/user-attachments/assets/82f40460-cdcf-436b-b7bc-218c275e9eb4">
</p>

<p align="center">
  N4 Bias field correction principle
</p>

<br>

#### - Registration

- Each patient or subject's MRI may have different posture, size, and orientation when scanned. These differences make it difficult to directly compare the brain structure of one subject with that of another.
- Align the input data to a standard space to ensure that model can more accurately segment the hippocampus structure of various subjects.
  
<p align="center">
  <img width="500" alt="image" src="https://github.com/user-attachments/assets/00a28a55-b3b0-4300-9ba8-0cadc80babfe">
</p>

<p align="center">
  Images before and after alignment with MNI template
</p>

<p align="right">
  (Red color: MNI Template)
</p>

<br>

### Docker Execution Command :whale2:

```
docker run --rm --gpus all -it -v [Harmonization Subject Files Path]:/workspace haca3cna_v2
```

### Harmonization Execution Commands after Access

```
cd ..                               ⋯       Access Path
python reshape.py /workspace/       ⋯       execute code to zero pad an image to the MNI152 template

# Harmonization Execution Command
haca3-test --in-path /workspace/D11004_COR_3D_T1_FSPGR_20151015083508_9_N4_resample_lin.nii.gz --target-image /workspace/N110132_Sag_IR-FSPGR_20220316124202_3_N4_lin.nii.gz --harmonization-model /pretrained_weights/CNA_onlyT1w_model.pt --fusion-model /pretrained_weights/fusion.pt --out-path /workspace/D11004_COR_3D_T1_FSPGR_20151015083508_9_N4_resample_lin.nii.gz --intermediate-out-dir /workspace/intermidate
```

### Result

<p align="center">
  <img width="574" alt="image" src="https://github.com/user-attachments/assets/635555b1-22fe-4442-9c28-846dce3c4f5b">
</p>

<br>

---

<br>

## :brain: WMH Segmentation Docker

### [[Docker Hub Link]](https://hub.docker.com/r/ajtwlsdnrms/pgs_wmh_gpu_v1)

## Experiment Environment

```
GPU Model: NVIDIA A40
NVIDIA Driver Version: 535.161.08
Supply CUDA Version: 12.3
CPU RAM: 65368064 KiB total

Run-time on GPU: 10 s per subject
```

### Essential Preprocessing Steps

(Essential) This steps are essential for the performance of the model, and if not performed, you will definitely get poor results.

```
1. N4 Bias Correction
2. T1, FLAIR Co-Registration
3. Brain Extraction (ROBEX, HD-BET, ...)
  - Use the flirt commnad by default.
  - flirt -dof 6 -in subject_T1.nii -ref subject_FLAIR.nii -out subject_T1_to_FLAIR -omat subject_T1_to_FLAIR.mat

Ex) flirt -dof 6 -in /nasdata3/cohort_FLAIR_2022-1/T1_N4/GH/L1_GH_04935_native_N4.nii -ref /nasdata3/cohort_FLAIR_2022-1/FLAIR/GH/L1_GH_04935/L1_GH_04935_FLAIR.nii -out /nasdata3/cohort_FLAIR_2022-1/FLAIR/GH/L1_GH_04935/T1_to_FLAIR -omat /nasdata3/cohort_FLAIR_2022-1/FLAIR/GH/L1_GH_04935/T1_to_FLAIR.mat
```

### Detailed description of preprocessing

#### - N4 Bias Correction

- Bias Field in MRI image refers to the non-uniformity of signal intensity (illumination distortion) within the image.
- These bias fields are caused by various factors such as the device, scanning environment, and characteristics of biological tissue, and they affect the global brightness pattern of the image.
- It is necessary to improve the illumination uniformity of MRI and increase the accuracy of Hippocampus segmentation. This standardizes the model input data by reducing the variation of illumination intensity within the image.

<p align="center">
  <img width="400" alt="image" src="https://github.com/user-attachments/assets/82f40460-cdcf-436b-b7bc-218c275e9eb4">
</p>

<p align="center">
  N4 Bias field correction principle
</p>

<br>

#### - Co-Registration

- Co-registration is necessary when alignment between brain images taken at different times, modalities, or conditions is required. For example, when comparing MRI data of the same patient or analyzing changes over time even in images of the same modality, the location, size, and orientation of each image may be different. These differences hinder direct comparison or integrated analysis of image data.
- Co-registration solves this problem by aligning all images to the same coordinate system so that the same anatomical structures appear in the same locations. This enables integrated analysis of multimodal data, observation of temporal changes, and comparison between groups.
- Co-registration is performed to align FLAIR images to the same coordinate system as T1 images, thereby precisely matching the anatomical structures between the two images. This allows for more precise segmentation of white matter lesion signals appearing in FLAIR by utilizing structural information from T1.

<p align="center">
  <img width="500" alt="image" src="https://github.com/user-attachments/assets/99b5ff33-4833-40b4-baff-f693215a7a09">
</p>

<p align="center">
  Co-Registration before and after
</p>

<p align="right">
  (Red color: T1-weight image / Brain: FLAIR image)
</p>

<br>

#### Brain Extraction (ROBEX, HD-BET, ...)

- [hdbet Extraction Docker](#hdbet-extraction-docker)

- In WMH (White Matter Hyperintensities) segmentation, Brain Extraction is an important preprocessing step that separates only brain tissue and removes non-brain tissues such as skull, sacrum, and air. In magnetic resonance imaging sequences such as FLAIR, non-brain tissues can appear as high-intensity signals, which can be easily confused with lesions. Removing these non-brain tissues through brain region extraction allows the model to focus on lesions, thereby improving segmentation accuracy.
- In addition, brain region extraction increases computational efficiency by removing non-brain regions, enables standardization for comparison between data, and reduces noise to clearly distinguish the boundary between lesions and non-lesions. As a result, this process greatly improves the reliability and accuracy of WMH segmentation, making it essential for improving the quality of analysis and research results.

<p align="center">
  <img width="800" alt="image" src="https://github.com/user-attachments/assets/23bc2e73-5302-45e3-89b6-3939df777c2a">
</p>

<p align="center">
  Example of brain region extraction results using the HD-BET model
</p>

<p align="right">
  (Red color: Extracted Brain)
</p>

<br>

### Docker Execution Command :whale2:

```
docker run -it --network host --gpus all -v [Segmentation Subject Files Path]:/mnt pgs_wmh_gpu_v1 /bin/bash
```

### WMH Segmentation Execution Command after Access

```
# WMH segmentation Execution Command Format
python WMHs_segmentation_PGS_gpu_division.py /mnt/[subject_brain.nii] /mnt/[subject_brain_mask.nii] /mnt/[subject_FLAIR.nii] /mnt/[subject_WMH.nii] [GPU_number]                         ⋯      

# WMH segmentation Execution Command Format Example
python WMHs_segmentation_PGS_gpu_division.py /mnt/${sub_fold}_brain.nii /mnt/${sub_fold}_brain_mask.nii /mnt/${sub_fold}_FLAIR.nii /mnt/${sub_fold}/${sub_fold}_WMH.nii 5
```

### Result

<p align="center">
  <img width="350" alt="image" src="https://github.com/user-attachments/assets/d3dd8163-a3c4-44d0-8cf4-965ee677c4ea">
</p>

---
