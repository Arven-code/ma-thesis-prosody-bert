# Data

This repository does not include raw data or audio.

This thesis uses the **Gleason Corpus** from CHILDES / TalkBank and focuses on
parent–child interactions (Mother, Father, Dinner sessions). The analysis pairs each
child utterance with the immediately preceding caregiver turn, then extracts
F0-based prosodic statistics from the caregiver span and combines them with
textual representations for classification. 

## Source
- CHILDES / TalkBank – Gleason corpus (.cha transcripts + linked media)
- Original recordings were produced in the mid-1970s.

Please obtain the corpus through the official TalkBank/CHILDES access route.

## Expected folder structure
data/
  raw/
    cha/                # original .cha files
    audio/              # original or extracted .wav
  interim/
    txt/                # cleaned transcripts
  processed/
    utterances.csv      # transcript + labels + speaker + timestamps
    pairs.csv           # child turn paired with caregiver preceder
  features/
    f0_features.csv     # per caregiver span F0 stats
    text_embeddings/    # optional cached embeddings
  splits/
    train.csv
    valid.csv
    test.csv

## Key files and columns

### processed/utterances.csv
Minimum fields:
- `transcript`
- `label`  (1.0 = child error, 2.0 = child success after prior error)
- `speaker` (e.g., MOT, FAT, CHI)
- `start_sec`, `end_sec` (CHAT-aligned)

### processed/pairs.csv
Each child utterance paired with:
- preceding caregiver turn containing the repeated target word when possible,
  otherwise the closest earlier caregiver turn.

Fields:
- `child_utterance_id`
- `caregiver_utterance_id`
- `target_word` (optional)
- `speaker_caregiver` (MOT/FAT)

### features/f0_features.csv
Extracted from caregiver spans using `librosa.pyin`.
Suggested fields:
- `f0_mean`, `f0_median`
- `f0_std`, `f0_iqr`
- `f0_p10`, `f0_p90`
- `f0_range`, `f0_cv`
- `f0_slope`, `dF0_iqr`
- `voicing_rate`, `frames`

## Notes
- Audio and transcripts are not redistributed here.
- This repo only contains code and empty placeholders for reproducibility.
