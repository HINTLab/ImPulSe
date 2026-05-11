# Supplmentary Materials of MedIA Submission

This is the code of *Template-Guided Reconstruction of Pulmonary Segments with Neural Implicit Functions*.

## Table of Contents
```
configs/                # configs of each experiment
data/                   # dataset, dataloader and data transforms
models/                 # losses and pytorch models of the proposed ImPulSe2
utils/                  # logger and metrics
train.py                # training script of ImPulSe2
predict.py              # inference script of ImPulSe2
```

## Lung3D dataset folder structure

Shape-based Dataset we used in this project is now availble in: .

    lung3d/
    ├── lung3d_00002
        ├── airway.nii.gz
        ├── artery.nii.gz
        ├── interseg.nii.gz
        ├── lobe.nii.gz
        ├── lungsegment.nii.gz
        ├── vein.nii.gz
        ├── preprocessed.npz
    ├── lung3d_00003
    ├── lung3d_00006
    ├── ...
    ├── lung3d.csv

Each preprocessed.npz file contains the proprocessed (cropped and resized 3D shape of airway(B), artery(A), vein(V) and lobe(L)) shapes of anatomies, as well as necessary information during inference, and the ground truth target lung segments in original resolusion.

We have also released our training, validation, and test splits in the lung3d.csv file.
Link to the proposed Lung3D dataset:
https://zenodo.org/records/20114109

## Usage

### Dependencies

This project depends on the following libraries:

* torch==1.11.0 
* torchvision==0.12.0 
* tensorboardx==2.6.2.2 
* numpy==1.19.2
* pandas==1.2.0
* SimpleITK>=2.1.0

### Installation 
```
git clone https://github.com/YFZhu22/ImPulSe2.git
cd ImPulSe2
pip install -r requirement.txt
```

### ImPulSe2 Training
Before executing train.py, ensure to modify the input data path, data splits file path, and the output path within the train.py script:
```
data_dir = "/lung3d" # path to the input dataset
df = pd.read_csv("/lung3d.csv") # path to the file containing data splits

......

log_dir = "/media/dntech/_mnt_storage/yufei/data/lung_segment/tim/logs"  # path for storing checkpoints and TensorBoard files

```
And modify the path to the weights of pretrianed template networks in the `configs/lbav_configs.py`.
```
template_weights_path = "./models/pretrained_template_weights.pth"
```

Then run the training script.
```
python train.py
```

### ImPulSe2 Inference
You should specify the path to the weights you intend to use in the `configs/lbav_configs.py`.
```
model_weights_path = "./models/model_weights.pth"
```

Modify the output path in the `predict.py`.
```
output_dir = f"/media/dntech/_mnt_storage/yufei/data/lung_segment/valtest_data/outputs/pred/{args.cfg.upper()}"
```
Then run the inference script.
```
python predict.py
```

