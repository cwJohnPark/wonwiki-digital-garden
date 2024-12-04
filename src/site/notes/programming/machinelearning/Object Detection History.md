---
{"dg-publish":true,"permalink":"/programming/machinelearning/object-detection-history/"}
---

2012년 AlexNet의 CNN 도입으로 객체 인식 분야가 크게 발전함

PASCAL VOC는 유명한 컴페티션
mAP는 성능 지표
2011년에는 40% 초반이었음
합성곱 신경망(CNN) 도입이후로  mAP지표가 50% 이상으로 발전함

객체 인식 발전
1. Classification: 이미지 하나를 단순하게 분류
2. Localization: 이미지 하나에 하나의 객체를 인식함
3. Detection: 이미지 하나에 여러 개의 객체를 인식함
4. Segmentation: 이미지 하나에 여러 개의 객체를 각각 픽셀 단위로 바운딩 박스를 지정함

2012년 이전: VJ Det, HOG Det, DPM
2012년 이후: AlexNet, RCNN

**Two-stage detector**
RCNN
SPPNet
Fast RCNN
Faster RCNN

Two-stage detector는 실시간 적용이 어렵다.

**One-stage detector**
YOLO
SSD
Retina-Net
YOLOv3
EfficientDet

One-stage detector는 실시간에 적합하다.

