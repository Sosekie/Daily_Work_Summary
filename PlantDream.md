# PlantDream

- optical flow RAFT, visualize the area to see it is wrong.
- LTX, image input-output.
- Data washing.
- sds loss.

## 4/7/2025

### Main Object:
Run Finetuning

### How things going:

[ ] Get caption for each clip
    - extract key frames
    - get caption
[ ] Input should be (caption, image)





## 3/14/2025 - 3/15/2025

### Main Object:
Get HF format plant dataset.

### How things going:

1. LTX-Video Type Datasets
    - [x] Since LTX-Video using [crush-smol](https://huggingface.co/datasets/finetrainers/crush-smol), see details of it.
    - [x] Finetune on plant_time_lapse dataset.
    - [x] Create examples/training/sft/ltx_video/plant_time_lapse
    - [x] input images
    - [ ] Inference stucked (image size( ), prompt length(no))
    - [ ] Check settings ("id_token": "PIKA_CRUSH", --enable_precomputation).
2. Datasets
    - [ ] Generate new prompt (using first and last frames?)
    - [ ] Num of frames (speed)
    - [ ] Camera motion
    - [ ] **Process Youtube Video manually.**

    - 1. histogram，optical flow，pixel level rgb
    - 2. resnet feature，dino feature (take t and t+1 frame and plot 0-1, 1-2, 2-3)
    - ![dino](dino.jpg)





## 3/13/2025

### Main Object:
Get HF format plant dataset.

### How things going:

1. Trying [finetrainers](https://github.com/a-r-r-o-w/finetrainers?tab=readme-ov-file#support-matrix).
    - Getting [Dataset](https://github.com/a-r-r-o-w/finetrainers/blob/main/docs/dataset/README.md#two-file-format).
        - Go through [video-dataset-scripts](https://github.com/huggingface/video-dataset-scripts?tab=readme-ov-file#video-dataset-scripts).
            - Go through [video_processing](https://github.com/huggingface/video-dataset-scripts/tree/main/video_processing).
                - [x] Run [Folder to Parquet](https://github.com/huggingface/video-dataset-scripts/tree/main/video_processing#folder-to-parquet)
                - [x] Run [Extract frames](https://github.com/huggingface/video-dataset-scripts/tree/main/video_processing#extract-frames)
                - [x] Run [Add Captions](https://github.com/huggingface/video-dataset-scripts/tree/main/video_processing#add-captions), cost about 6 hours.
                - [x] Run [Add Watermark Laion Score](https://github.com/huggingface/video-dataset-scripts/tree/main/video_processing#add-watermark-laion-score).
                - [Failed] Run [Add Motion Score](https://github.com/huggingface/video-dataset-scripts/tree/main/video_processing#add-motion-score), use our exist score instead.
        - [x] Moving all steps to cluster.
            - [x] Uploading zip.

    - [x] Trying [LTX-Video](https://github.com/a-r-r-o-w/finetrainers/blob/main/docs/models/ltx_video.md).