1. Choose mode
(1) Overlay: 기존 영상 위에 얼굴을 덮어씌웁니다. 기본적인 합성 모드입니다.
(2) Hist-match: 색상 및 밝기 조정을 히스토그램 매칭을 통해 더 자연스럽게 만듭니다. 경계가 눈에 띄지 않도록 도와줍니다.
(3) Seamless: 얼굴 경계를 더 부드럽게 합성합니다. 피부색이 자연스럽게 섞이도록 합니다.
(4) Seamless-hist-match: Seamless와 Hist-match를 조합하여 경계와 색상 모두 자연스럽게 처리합니다. 추천.
(5) Raw-rgb: 얼굴 합성 결과의 원본 RGB 데이터를 출력합니다. 경계 조정이 없습니다.
(6) Raw-predict: 모델이 예측한 얼굴을 그대로 출력합니다. 디버깅용입니다.
추천 설정: (4) Seamless-hist-match
경계와 색상을 모두 부드럽게 처리하기 위해 적합합니다.

2. Choose mask mode
(4) Learned-prd*learned-dst: 소스와 대상의 학습된 마스크를 곱하여 사용합니다. 경계가 정교하게 보정됩니다.
(5) Learned-prd+learned-dst: 두 마스크를 합칩니다. 밝은 경계를 다룰 때 유용합니다.
(8) XSeg-prd*XSeg-dst: XSeg로 학습된 마스크를 곱합니다. 경계 처리가 더 섬세해질 수 있습니다.
(9) Learned-prdlearned-dstXSeg-prd*XSeg-dst: 모든 마스크를 곱하여 최대한 정교한 경계를 만듭니다. 추천.
추천 설정: (9) Learned-prdlearned-dstXSeg-prd*XSeg-dst
경계 처리를 가장 섬세하게 합니다.

3. Choose erode mask modifier (-400..400)
기본값은 0입니다.
양수로 설정하면 마스크 크기가 줄어들어 경계가 더 부드러워집니다.
음수로 설정하면 마스크 크기가 커져 얼굴 외곽 부분이 더 강조됩니다.
추천 설정: 20~50
경계를 부드럽게 하고 티가 나지 않도록 조정합니다.

4. Choose blur mask modifier (0..400)
마스크의 경계 블러 강도를 조절합니다.
높은 값일수록 경계가 부드러워지지만 너무 높으면 합성된 얼굴이 뭉개질 수 있습니다.
추천 설정: 30~70
경계를 적당히 부드럽게 하여 티가 나지 않도록 합니다.

5. Choose motion blur power (0..100)
움직임이 있는 장면에서 모션 블러를 추가하여 자연스럽게 만듭니다.
정적인 장면에서는 0으로 설정하는 것이 좋습니다.
추천 설정: 0~10
살짝만 적용하여 움직임에 맞는 자연스러움을 추가합니다.

6. Choose output face scale modifier (-50..50)
얼굴 크기를 조정합니다.
양수로 설정하면 얼굴이 커지고, 음수로 설정하면 얼굴이 작아집니다.
추천 설정: -5~5
얼굴 크기를 장면에 맞게 조정합니다.

7. Color transfer to predicted face
얼굴 색상을 대상에 맞게 조정합니다.
rct: 기본 추천 모드로, 얼굴 색상과 배경이 자연스럽게 섞입니다.
idt/idt-m: 정교한 색상 조정에 유리합니다. 피부 톤 차이가 큰 경우 유용합니다.
mix-m: 여러 모드를 혼합하여 결과를 개선합니다.
추천 설정: rct 또는 idt-m
피부 톤 차이에 따라 적절히 선택합니다.

8. Choose sharpen mode (0: None, 1: box, 2: gaussian)
1 (box): 디테일을 선명하게 만듭니다.
2 (gaussian): 선명도를 부드럽게 조정합니다.
추천 설정: 2 (gaussian)
선명도를 개선하며, 자연스러운 디테일을 보장합니다.

9. Choose blur/sharpen amount (-100..100)
얼굴 디테일의 선명도를 조정합니다.
음수로 설정하면 더 부드러워지고, 양수로 설정하면 더 선명해집니다.
추천 설정: 30~50
디테일을 살리면서도 부드럽게 처리합니다.

10. Choose super resolution power (0..100)
얼굴 이미지를 고해상도로 변환합니다.
값이 높을수록 선명도가 개선되지만 처리 시간이 길어질 수 있습니다.
추천 설정: 20~50
디테일을 강화하면서 속도도 적당히 유지합니다.

11. 이미지 디그레이드
Denoise power (0..500): 잡음을 제거하여 부드럽게 만듭니다. (50~150 추천)
Bicubic rescale power (0..100): 저해상도 효과를 추가합니다. (0 권장)
Color degrade power (0..100): 색상을 감소시켜 스타일 효과를 추가합니다. (0~10 권장)
최종 추천 설정 조합
Mode: (4) Seamless-hist-match
Mask mode: (9) Learned-prd*learned-dst*XSeg-prd*XSeg-dst
Erode mask: 20~50
Blur mask: 30~70
Motion blur: 0~10
Output face scale: -5~5
Color transfer: rct 또는 idt-m
Sharpen mode: (2) gaussian
Blur/sharpen amount: 30~50
Super resolution: 20~50
Denoise power: 50~150
Bicubic rescale power: 0
Color degrade power: 0~10


MergerConfig 00109.jpg:
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

