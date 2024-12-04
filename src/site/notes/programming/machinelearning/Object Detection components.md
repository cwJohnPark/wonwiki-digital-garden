---
{"dg-publish":true,"permalink":"/programming/machinelearning/object-detection-components/"}
---



1. 영역 추정
   Region Proposal
   객체가 특정 영역에 위치할 확률이 높은 부분을 추론
   
2. Detection을 위한 Deep Learning Network 구성
   Feature Extraction
   FPN
   Network Prediction

3. Detection 기타 구성 요소 
   IOU
   NMS
   mAP
   Anchor Box


일반 Object Detection 모델
1. Backbone
2. Neck
3. Head

Object Detection가 어려운 이유
- Classification과 Regression을 동시에 해야함 
- 다양한 크기와 유형의 오브젝트가 혼재함
- 실시간 Detect 성능
- 명확하지 않은 이미지를 인식
- 데이터 세트 부족
   