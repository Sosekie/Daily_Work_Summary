# PlantDream

## 3/14/2025

### Main Object:
Get HF format plant dataset.

### How things going:

1. Since LTX-Video using [crush-smol](https://huggingface.co/datasets/finetrainers/crush-smol), see details of it.


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