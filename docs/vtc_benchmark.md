# Voice Type Classification

## Setup
```bash
cd voice-type-classifier
conda env create -f vtc.yml
conda activate pyannote

cd pyannote-audio
# First activate pyannote environment, then pip install inside the conda environment
pip install .
```

---

## VTC-ft

### Training
```bash
export EXP_DIR=/home/nele_pauline_suffo/projects/pyannote-audio-train/tutorials/models/multilabel_detection

cat ${EXP_DIR}/config.yml

pyannote-audio mlt train --subset=train --from=last --to=300 --parallel=16   --pretrained=$EXP_DIR/train/X.SpeakerDiarization.BBT2_LeaveOneDomainOut_paido.train/weights/0100.pt ${EXP_DIR} ChildLens.SpeakerDiarization.audio
```

### Validation
```bash
export EXP_DIR=/home/nele_pauline_suffo/projects/pyannote-audio-train/tutorials/models/multilabel_detection

export TRN_DIR=${EXP_DIR}/train/ChildLens.SpeakerDiarization.audio.train

pyannote-audio mlt validate --subset=development --from=0 --to=300 --every=5 ${TRN_DIR} ChildLens.SpeakerDiarization.audio
```

---

## VTC-cl

### Training
```bash
export EXP_DIR=/home/nele_pauline_suffo/projects/pyannote-audio-train/tutorials/models/multilabel_detection

cat ${EXP_DIR}/config.yml

pyannote-audio mlt train --subset=train --to=300 --parallel=16 ${EXP_DIR} ChildLens.SpeakerDiarization.audiocl
```

### Validation
```bash
export EXP_DIR=/home/nele_pauline_suffo/projects/pyannote-audio-train/tutorials/models/multilabel_detection

export TRN_DIR=${EXP_DIR}/train/ChildLens.SpeakerDiarization.audio.train
export TRN_DIR=${EXP_DIR}/train/ChildLens_v2.SpeakerDiarization.audio.train

pyannote-audio mlt validate --subset=development --from=0 --to=300 --every=5 ${TRN_DIR} ChildLens.SpeakerDiarization.audio

pyannote-audio mlt validate --subset=development --from=0 --to=300 --every=5 ${TRN_DIR} ChildLens_v2.SpeakerDiarization.audio
```
---

## Testing
```bash
./apply_og.sh /file/to/test_audio/ --device=gpu
./apply_ft.sh /file/to/test_audio/ --device=gpu
./apply_cl.sh /file/to/test_audio/ --device=gpu
```
