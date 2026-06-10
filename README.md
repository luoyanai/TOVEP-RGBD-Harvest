# TOVEP-RGBD-Harvest

RGB-D dataset for greenhouse fruit harvesting perception (mango, orange, pepper, strawberry).

## Directory layout

```
TOVEP-RGBD-Harvest/
├── README.md
├── annotations/
│   ├── decision_gt_index.json
│   └── decision_gt/
│       ├── mango/
│       │   ├── mango_frame_0001.json
│       │   └── ...
│       ├── orange/
│       ├── pepper/
│       └── strawberry/
├── metadata/
│   ├── camera_intrinsics.json
│   ├── class_labels.json
│   ├── dataset_info.json
│   ├── gt_frames.json
│   └── splits.json
└── rgbd/
    ├── train/
    │   ├── mango/
    │   │   ├── mango_frame_0001_rgb.png
    │   │   ├── mango_frame_0001.npz
    │   │   └── ...
    │   ├── orange/
    │   ├── pepper/
    │   └── strawberry/
    └── val/
        ├── mango/
        ├── orange/
        ├── pepper/
        └── strawberry/
```

Under `rgbd/{split}/{crop}/`, each frame is `{crop}_frame_{id}_rgb.png` and `{crop}_frame_{id}.npz`.

## Splits

| Split | Frames | Description |
|-------|--------|-------------|
| decision_gt | 220 | Expert decision-GT subset; **final VLM evaluation only** |
| rep_val | 1103 | TOVEP validation, early stopping, representation metrics |
| train | 3366 | TOVEP training only |
| val_pool | 1323 | TOVEP acquisition pool |

Train and val come from **different acquisition batches**. Expert decision labels are **not** used for TOVEP training or model selection.

### Per-crop counts

| Crop | Total | Train | Val pool | Rep. val | Decision GT |
|------|-------|-------|----------|----------|-------------|
| mango | 1071 | 736 | 335 | 280 | 55 |
| orange | 1025 | 707 | 318 | 263 | 55 |
| pepper | 1062 | 727 | 335 | 280 | 55 |
| strawberry | 1531 | 1196 | 335 | 280 | 55 |
| **Total** | **4689** | **3366** | **1323** | **1103** | **220** |

## Decision-GT annotations

Expert harvesting-decision labels for 220 frames (`decision_gt_v1`) are under `annotations/decision_gt/{crop}/`. Class IDs are in `metadata/class_labels.json`.

- **`targets`**: all harvestable fruits in the frame; each entry is valid GT.
- **`primary_target_id`**: recommended primary target for single-target evaluation (`target_id = 1`).

Pose convention: camera frame; `R = Rz(yaw) * Ry(pitch) * Rx(roll)`; `orientation_rpy_deg` is `[roll, pitch, yaw]` in degrees. Intrinsics: `metadata/camera_intrinsics.json`.

## Data access

- **RGB-D images** (`rgbd/`, ~2.5 GB): download from Mendeley Data (DOI: to be assigned).
- **This repository** contains annotations, metadata, README, and the VLM evaluation prompt.

## Citation & License

(Add citation and license here before public release.)
