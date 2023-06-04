# MMdetection(目标检测）  
```
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=   all | maxDets=100 ] = 0.804  
 Average Precision  (AP) @[ IoU=0.50      | area=   all | maxDets=100 ] = 0.964  
 Average Precision  (AP) @[ IoU=0.75      | area=   all | maxDets=100 ] = 0.964  
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= small | maxDets=100 ] = -1.000  
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=medium | maxDets=100 ] = -1.000  
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= large | maxDets=100 ] = 0.804  
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets=  1 ] = 0.838  
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets= 10 ] = 0.838  
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets=100 ] = 0.838  
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= small | maxDets=100 ] = -1.000  
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=medium | maxDets=100 ] = -1.000  
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= large | maxDets=100 ] = 0.838  
 mmengine - INFO - bbox_mAP_copypaste: 0.804 0.964 0.964 -1.000 -1.000 0.804  
 mmengine - INFO - Epoch(val) [200][11/11]    coco/bbox_mAP: 0.8040  coco/bbox_mAP_50: 0.9640  coco/bbox_mAP_75: 0.9640  coco/bbox_mAP_s: -1.0000  coco/bbox_mAP_m: -1.0000  coco/bbox_mAP_l: 0.8040  data_time: 0.6236  time: 0.6592  
```   
# MMPose(关键点检测）  
```
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=   all | maxDets= 20 ] =  0.663
 Average Precision  (AP) @[ IoU=0.50      | area=   all | maxDets= 20 ] =  1.000
 Average Precision  (AP) @[ IoU=0.75      | area=   all | maxDets= 20 ] =  0.860
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=medium | maxDets= 20 ] = -1.000
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= large | maxDets= 20 ] =  0.663
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets= 20 ] =  0.683
 Average Recall     (AR) @[ IoU=0.50      | area=   all | maxDets= 20 ] =  1.000
 Average Recall     (AR) @[ IoU=0.75      | area=   all | maxDets= 20 ] =  0.881
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=medium | maxDets= 20 ] = -1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= large | maxDets= 20 ] =  0.683
 mmengine - INFO - Evaluating PCKAccuracy (normalized by ``"bbox_size"``)...
 mmengine - INFO - Evaluating AUC...
 mmengine - INFO - Evaluating NME...
 mmengine - INFO - Epoch(test) [6/6]    coco/AP: 0.662770  coco/AP .5: 1.000000  coco/AP .75: 0.859795  coco/AP (M): -1.000000  coco/AP (L): 0.662770  coco/AR: 0.683333  coco/AR .5: 1.000000  coco/AR .75: 0.880952  coco/AR (M): -1.000000  coco/AR (L): 0.683333  PCK: 0.945578  AUC: 0.087925  NME: 0.049558  data_time: 1.709038  time: 2.485353
```
