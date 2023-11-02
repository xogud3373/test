# 작동순서
## 1. Data preprocessing
### dd3d 모델은 kitti3d dataset 으로 학습되어 있음. 따라서, 이에 대한 dataloader가 구성되어 있음.
- custom dataset으로 inference하기 위해서 data preprocessing이 필요함.

1. 동영상 -> 이미지 변환

'''
python utils/video_to_image.py
'''

2. custom format -> kitti3d data format

'''
python utils/custom_to_kitti.py
'''

## 2. DD3D Inference
- 3d object detection을 진행
- 아래의 명령어를 통해 실행

'''
python scripts/dd3d_inference.py +experiments=dd3d_kitti_dla34 MODEL.CKPT=./od3d/dd3d/checkpoint/model_final.pth 
'''

- 최종 output은 다음의 경로에 생성됨.

'''
outputs/dd3d
'''

## 3. Tracking Inference
- tracking 진행
- 아래의 명령어를 통해 실행

'''
python scripts/tracking_inference.py
'''

- 최종 output은 다음의 경로에 생성됨.

'''
outputs/tracking
'''

## 4. Trajectory Inference
- tracking된 값과 3d object detection된 값을 토대로 사고 차량 검출 진행
- 검출된 사고 차량의 궤적 산출 및 사고 차량 bbox 검출
- 아래의 명령어를 통해 실행

'''
python scripts/trajectory.py
'''

- 최종 output은 다음의 경로에 생성됨.

'''
outputs/trajectory
outputs/accident_2dbox
'''
