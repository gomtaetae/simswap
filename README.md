# Face Swap Configuration Guide

## 1. Choose Mode
- **(1) Overlay**: 기본적인 얼굴 합성 모드  
- **(2) Hist-match**: 히스토그램 매칭을 통해 색상과 밝기 조정  
- **(3) Seamless**: 얼굴 경계를 부드럽게 합성  
- **(4) Seamless-hist-match** (추천): 색상과 경계를 자연스럽게 조합  
- **(5) Raw-rgb**: 원본 RGB 데이터를 출력  
- **(6) Raw-predict**: 모델 예측 결과를 그대로 출력 (디버깅용)  

## 2. Choose Mask Mode
- **(4) Learned-prd * learned-dst**: 소스와 대상의 학습된 마스크를 곱하여 사용  
- **(5) Learned-prd + learned-dst**: 두 마스크를 합쳐 밝은 경계 보정  
- **(8) XSeg-prd * XSeg-dst**: XSeg로 학습된 마스크를 곱하여 섬세한 경계 처리  
- **(9) Learned-prd * learned-dst * XSeg-prd * XSeg-dst** (추천): 최대한 정교한 경계 처리  

## 3. Choose Erode Mask Modifier (-400..400)
- 기본값: `0`  
- 추천값: `20~50` (경계를 부드럽게 조정)  

## 4. Choose Blur Mask Modifier (0..400)
- 추천값: `30~70` (경계를 적당히 부드럽게 처리)  

## 5. Choose Motion Blur Power (0..100)
- 추천값: `0~10` (살짝만 적용하여 자연스럽게 처리)  

## 6. Choose Output Face Scale Modifier (-50..50)
- 추천값: `-5~5` (장면에 맞게 얼굴 크기 조정)  

## 7. Choose Color Transfer to Predicted Face
- **rct** (추천): 얼굴 색상과 배경이 자연스럽게 섞임  
- **idt/idt-m**: 피부 톤 차이가 큰 경우 유용  
- **mix-m**: 여러 모드를 혼합하여 결과 개선  

## 8. Choose Sharpen Mode (0: None, 1: box, 2: gaussian)
- 추천값: `2 (gaussian)` (선명도를 개선하면서 자연스럽게 유지)  

## 9. Choose Blur/Sharpen Amount (-100..100)
- 추천값: `30~50` (디테일을 살리면서 부드러운 효과 유지)  

## 10. Choose Super Resolution Power (0..100)
- 추천값: `20~50` (디테일 강화 및 적절한 속도 유지)  

## 11. Image Degrade Options
- **Denoise Power (0..500)**: `50~150` (잡음 제거)  
- **Bicubic Rescale Power (0..100)**: `0` (저해상도 효과 X)  
- **Color Degrade Power (0..100)**: `0~10` (색상 감소 효과 추가)  

## Recommended Settings

Mode: (4) Seamless-hist-match
Mask mode: (9) Learned-prd * learned-dst * XSeg-prd * XSeg-dst
Erode mask: 2050
Blur mask: 3070
Motion blur: 010
Output face scale: -55
Color transfer: rct 또는 idt-m
Sharpen mode: (2) gaussian
Blur/sharpen amount: 3050
Super resolution: 2050
Denoise power: 50150
Bicubic rescale power: 0
Color degrade power: 010

## Example Configuration (MergerConfig 00109.jpg)

Mode: overlay
mask_mode: dst
erode_mask_modifier: 10
blur_mask_modifier: 150
motion_blur_power: 3
output_face_scale: 5
color_transfer_mode: rct
sharpen_mode : gaussian
blursharpen_amount : 0
super_resolution_power: 0
image_denoise_power: 250
bicubic_degrade_power: 0
color_degrade_power: 0


## 실행 명령어 (비디오 전환)
python test_video_swapsingle.py --isTrain false --name 512 --Arc_path ./checkpoints/arcface_checkpoint.tar --pic_a_path ./data/1.jpg --video_path ./data/1-1.mp4 --output_path ./output/result_512.mp4 --temp_path ./temp_results --gpu_ids 0

