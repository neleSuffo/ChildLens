# Replication Instructions for BMN Model on ChildLens Dataset

This repository contains scripts to process the ChildLens dataset, extract features, and train the BMN model to replicate the reported results.

---

## 1. Prepare Annotations

**Command:**
```bash
python generate_combined_annotations.py
```

**Requires:**
- Individual annotation `.json` files.

**Description:**
Combines all SuperAnnotate annotations into a single `combined_annotations.json` file, including only the following activities:
- `playing_with_object`
- `reading_a_book`
- `drawing`

---

## 2. Process Annotations

**Command 1:**
```bash
python generate_video_info.py
```
Generates `video_info.csv` with training/testing split.

**Requires:**
- `combined_annotations.json`

**Executes:**
- Collects relevant video information such as number of frames and subset assignment.

**Command 2:**
```bash
python process_annotations.py
```

**Requires:**
- `combined_annotations.json`
- `video_info.csv`

**Executes:**
- Splits `combined_annotations.json` into `full/train/val/test` sets.

---

## 3. Prepare Videos

**Command:**
```bash
python split_videos_and_frames.py
```

**Requires:**
- Videos stored in `video/` folder.

**Executes:**
- Splits all videos into predefined chunks of equal size to reduce memory usage.

---

## 4. Extract RGB and Flow

**Command:**
```bash
python extract_frames.py
```

**Requires:**
- Videos in `video_input_dir`

**Executes:**
- Extracts frames and optical flow (`x_flow`, `y_flow`) for all videos.

---

## 5. Generate File List for ActivityNet

**Command:**
```bash
python generate_rawframes_filelist.py
```

**Requires:**
- `split_annotations.json`
- `video_info.csv`
- Extracted raw frames

**Executes:**
- Generates `.txt` files containing:
  - Video file path
  - Number of frames
  - Label for full videos and video clips

---

## 6. Extract ActivityNet Features

**Command:**
```bash
python feature_extraction.py
```

**Requires:**
- `train_video.txt`
- `val_video.txt`
- Raw frames

**Executes:**
- Extracts features for each video file.
- Run separately for `train_video.txt` and `val_video.txt`.

---

## 7. Generate Final Features

**Command:**
```bash
python feature_postprocessing.py
```

**Requires:**
- Extracted RGB and flow features

**Executes:**
- Combines RGB and flow features into one `.csv` file per video.

**Working directory:**  
```bash
$MMACTION2/
```

---

## 8. Train BMN Model

**Command:**
```bash
bash tools/dist_train.sh configs/localization/bmn/bmn_2xb8-400x100-9e_childlens-feature.py 1 --work-dir /home/nele_pauline_suffo/outputs/bmn > output.log 2>&1
```

**Requires:**
Final directory should contain:
- `anet_train_video.txt`
- `anet_val_video.txt`
- `anet_train_clip.txt`
- `anet_val_clip.txt`
- `activity_net.v1-3.min.json`
- `mmaction_feat/`
  - `v_01.csv`
  - `v_02.csv`
  - ...
- `rawframes/`
  - `v_01/`
    - `img_00000.jpg`
    - `flow_x_00000.jpg`
    - `flow_y_00000.jpg`
  - ...

**Executes:**
- Trains the BMN model and saves the best-performing model.
