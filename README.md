# YOLO_Trakcer
전에 YOLO를 구동할 때 frame skip알고리즘을 frame tracker로 바꿨습니다.
frame skip알고리즘은 아래를 참조해 주세요.
#
#### YOLO Frame skip(opencv)
https://github.com/kacel33/yolo_skip_frame
#### YOLO Frame skip(tensorrt-pytorch)
https://github.com/kacel33/yolo_frame_skip_trt
#


#### frame skip알고리즘은 yolo_frame에서 YOLO를 사용하고 skip_frame에서는 YOLO를 사용하지 않고 yolo_frame에서 얻은 BoundingBOX를 사용하는 것입니다. 이 알고리즘에서는 skip_frame수가 많아질수록 오차가 커질 것입니다. 저는 이 전에 1 frame을 skip해서 1.5배의 계산속도가 향상되었습니다.
#### frame_skip_number=1일 때는 오차가 사람이 알아보기 힘든 정도였지만 10정도가 되면 물체가 움직이므로 오차가 많이 커졌습니다.
## YOLO_Tracker에서 바뀐 점
+ 저는 YOLO를 많이 사용하지 않기 위해서 skip_frame을 tracker_frame으로 변경하였습니다.
* yolo_frame에서는 YOLO를 사용하여 물체를 detect합니다. tracker_frame에서는 yolo_frame에서 얻은 BoundingBOX를 이용하여 opencv Tracker함수로 tracking합니다.



