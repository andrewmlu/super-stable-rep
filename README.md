# SuperStableRep

This code is modified from that within the [StableRep repository](https://github.com/google-research/syn-rep-learn) from the paper [StableRep: Synthetic Images from Text-to-Image
Models Make Strong Visual Representation Learners](https://arxiv.org/abs/2306.00984). Yonglong Tian*, Lijie Fan*, Phillip Isola, Huiwen Chang, Dilip Krishnan.

The original StableRep repository can be found in the syn-rep-learn-main folder, while our implementation of SuperStableRep is in the super-stable-rep-main folder.

All code was copied and modified in accordance with the Apache 2.0 license.

## Usage

A typical example of deploying the base StableRep model would be as follows:

```commandline
python main_stablerep.py \
    --model base \
    --batch_size 43 \
    --epochs 15 --warmup_epochs 0.5 \
    --blr 2.0e-4 --weight_decay 0.1 --beta1 0.9 --beta2 0.98 \
    --num_workers 14 \
    --output_dir /path/to/output_model \
    --log_dir /path/to/output_log \
    --csv_path /path/to/csv_file \
    --folder_list /data/path/ \
    --n_img 6 --downsample --downsample_prob 0.05 --down_res 64 128
```

To run the SuperStableRep model with multi-negative contrastive learning, simply add the --neg flag to your arguments as follows:

```commandline
python main_stablerep.py \
    --model base \
    --batch_size 43 \
    --epochs 15 --warmup_epochs 0.5 \
    --blr 2.0e-4 --weight_decay 0.1 --beta1 0.9 --beta2 0.98 \
    --num_workers 14 \
    --output_dir /path/to/output_model \
    --log_dir /path/to/output_log \
    --csv_path /path/to/csv_file \
    --folder_list /data/path/ \
    --n_img 6 --downsample --downsample_prob 0.05 --down_res 64 128 \
    --neg
```

After training your model, run the a command like the following for linear probing on the ImageNet 2012 dataset:
```commandline
python drive/MyDrive/Super-Stable-Rep/main_linear.py --model base --data /path/to/imagenet \
  --pretrained /path/to/pre-trained/epoch_last.pth \
  --output-dir /path/to/linear_save \
  --log-dir /path/to/tensorboard_folder
  --num-classes 1000
```
