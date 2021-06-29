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
#
## 환경설정은 https://github.com/jkjung-avt/tensorrt_demos(Demo#5)로 하시면 됩니다.
tensorrt_demos폴더에 yolo_tracker.py를 옮겨주시고 실행해주세요.
## 코드 실행
<pre><code>python yolo_tracker.py --video {VIDEOFILE} -m {YOLOFILE} -n {tracker frame number}</code></pre>

## Example
<pre><code>python yolo_tracker.py --video video/original.mp4 -m yolov4-416 -n 10</code></pre>

# 실험결과
+ RTX3080에서 yolo_frame의 경우 0.006초, MOSSE_tracker_frame의 경우 0.01~0.02초가 나와서 오히려 더 느려졌습니다.  
+ tracker함수가 CPU에서 동작하기 때문에 느려진 것 같습니다.  
+ N은 10이하로 하는 것이 좋을 듯 합니다.  
+ CSRT는 너무 느려서 MOSSE로만 실험하였습니다.  
+ 이 아이디어의 의의는 skip_frame에서는 n이 많아야 2~3이 최대였는데, tracker_frame으로 변경 후 n을 더 크게 할 수 있다는 점에 있습니다.
### Tracker함수의 성능이 좋지 않았습니다.

# License
I refered source code of "https://github.com/jkjung-avt/tensorrt_demos" and change trt_yolo.py to yolo_tracker.py

