# Object Detection in an Urban Environment

The project write up as well as the setup instructions can be found in objectDetectionInUrbanEnvironments042823.pdf. pptx with the movies is available [here](https://docs.google.com/presentation/d/1aZ3bF0jNx8HkGZAjNCiPTCNZAYKPoRaq/edit?usp=share_link&ouid=100895622648891722365&rtpof=true&sd=true). Please note that if links in the ppt do not open by clicking - please paste them in browser (and vice versa).

Pipelines use an SSD Resnet 50 640x640 model as a fine tune checkpoint - download it from [pretrained model](http://download.tensorflow.org/models/object_detection/tf2/20200711/ssd_resnet50_v1_fpn_640x640_coco17_tpu-8.tar.gz) and place in
```
/home/workspace/nd013-c1-vision-starter/experiments/pretrained_model
```

Fine tune checkpoint for Augmentations2 can be downloaded from [here](https://drive.google.com/drive/folders/1oOOhnG_BqQTSs-cGAWOwWGdQD5OHZ62r?usp=share_link)
and should be placed in the folder
```
/home/workspace/nd013-c1-vision-starter/augs3-start-wth-augs2/exported
```
before executing the corresponding pipeline augs3-start-wth-augs2. See pdf for more details

Training, evaluation and testing - same as in project's instructions:
* a training process:
```
python experiments/model_main_tf2.py --model_dir=experiments/reference/ --pipeline_config_path=experiments/reference/pipeline_new.config
```
* an evaluation process:
```
python experiments/model_main_tf2.py --model_dir=experiments/reference/ --pipeline_config_path=experiments/reference/pipeline_new.config --checkpoint_dir=experiments/reference/
```
* exporting model
```
python experiments/exporter_main_v2.py --input_type image_tensor --pipeline_config_path experiments/reference/pipeline_new.config --trained_checkpoint_dir experiments/reference/ --output_directory experiments/reference/exported/
```
* creating a video
```
python inference_video.py --labelmap_path label_map.pbtxt --model_path experiments/reference/exported/saved_model --tf_record_path /data/waymo/testing/segment-12200383401366682847_2552_140_2572_140_with_camera_labels.tfrecord --config_path experiments/reference/pipeline_new.config --output_path animation.gif
```
