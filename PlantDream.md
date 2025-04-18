# PlantDream

## TODO
[ ] For artifacts, using refine network on LTX
    - [ ] 
[ ] Rewrite plantdream





## 4/16/2025

### Main Object:
Integrate LTX into PlantDream.

### How things going:
[ ] Integrate GS results with DreamGaussian4D, replace LGM.






## 4/15/2025

### Main Object:
Integrate LTX into PlantDream.

### How things going:

[x] Follow orbit camera system

[x] Try to replace SVD with LTX-Video.
    - [x] Using CLIP/BLIP caption generation pipeline to get prompt.
    - [x] Replace by LTX-Video.
    - [x] Padding more space.

[ ] Replace zero123 with LTX-Video.
    - [x] Zero123's sds cannot be used for training at all and will cause reconstruction to fail!
    - [ ] All three of SVD's loss counterparts work poorly. Try replacing SVD with LTX.





## 4/14/2025

### Main Object:
Testing model usability

### How things going:
[x] Inference
[x] VRAM problem
[x] Test on real dataset





## 4/11/2025 - 4/13/2025

### Main Object:
Finish finetuning

### How things going:
[x] Finish finetuning






## 4/9/2025 - 4/10/2025

### Main Object:
Finish finetuning

### How things going:

[x] Extract one frame every 5 frames(Problems with few changes in the picture).

[x] Give each video a detailed caption, specifically “image content + plant growth”, which can be done using CLIP. LTX is very concerned about the quality of the prompt.

[x] On 5090, train a initial model first.
    - Not so good, static.

[x] On 4090, do data processing.
    Processing video: 1087 Days Of Plant Growth In 15 Minutes-69.mp4
    Processed video saved to: PerfectVideoClips768x512_processed/PerfectVideoClips768x512_10/1087 Days Of Plant Growth In 15 Minutes-69.mp4
    Identified plant species: Amaranth
    Identified growth stage: seedling
    Identified camera view: close-up
    Generated final caption: a photography of a plant with green leaves in a container With plant species of Amaranth, growth stage at seedling, close-up camera.

[x] Have a nice sleep.

[ ] Use multires for training (the forums say that a few hundred videos converge easily, but a few thousand videos don't work well, and you need multi-sized videos).

[ ] In addition to multi-size images, it is also possible to group the current dataset, e.g., to train a model specifically for “plant seeds breaking out of the ground”.

[x] Watermark, using laion + prompt to remove it.

[x] Camera motion, using optical flow + prompt to remove it.
    - If there is camera movement, then both global and local are high, then camera_motion_score is high against camera movement;
    - If the camera didn't move and the plant is growing but only appears in some of the panels, then the overall global_motion_score is low, and a few panels in the localized area are high and others are low, then camera_motion_score is low, in line with the camera not moving.
    - If the camera didn't move and the plant growth covered the whole screen, then camera_motion_score is also high, which is a problem. But let's not solve this problem at this stage.
    Current: camera_motion_score = global_motion_score * median(normalized_local_scores)

[ ] CLIP species may have problem, try plant classification method.
    - https://huggingface.co/foduucom/plant-leaf-detection-and-classification, but limited set of plant classes (≈46).
 



## 4/7/2025

### Main Object:
Run Finetuning

### How things going:

[x] Get caption for each clip
    - extract key frames
    - get caption
[x] Input should be (caption, image)
    - LTX has problem in validation period, OOM




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