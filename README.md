# dental-cbct-3d-segmentation

Automated segmentation of dental anatomy from 3D CBCT scans using a 3D U-Net. Built during a funded research internship at **NIT Calicut** in collaboration with KMCT Hospital.

---

## What it does

Segments six anatomical structures from volumetric dental CT scans:
- Edentulous (missing tooth) regions
- Mandible & Mandibular nerve
- Upper & lower teeth
- Maxilla / upper skull

Outputs are compatible with **3D Slicer** for clinical visualization and implant planning.

---

## Results

| Structure | Dice Score |
|---|---|
| Mandible | 0.65 |
| Lower Teeth | 0.63 |
| Maxilla & Upper Skull | 0.62 |
| Upper Teeth | 0.61 |
| Other | 0.59 |
| Edentulous Region | 0.58 |
| Mandibular Nerve | 0.55 |

**Mean Dice: ~0.60** across 167 manually annotated CBCT scans.

---

## Stack

`Python` `PyTorch` `MONAI` `SimpleITK` `nibabel` `3D Slicer`

---

## Pipeline

```
DICOM → NIfTI conversion
      → Preprocessing (resampling, normalization, augmentation)
      → 3D U-Net training (500 epochs, Dice + CE loss, Adam lr=1e-4)
      → Prediction export → 3D Slicer visualization
```

---

## Dataset

167 CBCT scans with manual segmentation masks annotated in 3D Slicer.  
> Dataset not publicly available due to patient privacy constraints.

---

## Possible Extensions
- Transformer-based architectures (Swin-UNETR)
- Larger, more diverse dataset
- Bone density estimation for implant planning
