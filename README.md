# ViT

- "an image is worth 16*16 words: transformer for image recognition at scale" 논문 참고
-	이미지 자체를 standard transformer에 직접적으로 넣어주는 형식으로 모델을 구성
(이미지를 패치 단위로 쪼개 “토큰화” 시켜줌)
-	패치에 linear embedding 적용 후, sequence로 만들어준 형태로 transformer 입력으로 들어감
-	중간 사이즈의 데이터셋에 학습을 시킬 경우, 별도의 강력한 regularization 없이 기존 ResNets 대비 훌륭한 성능을 보여주지 못함
(transformer 구조 자체가 CNN 구조에 비해 inductive bias가 부족하여 많은 양의 데이터 없이는 일반화가 제대로 이루어지지 않았을 것으로 추정)
-	그러나 큰 사이즈의 데이터셋에서 학습 시킬 경우, 위의 구조적 한계(lack of inductive bias)를 극복 가능함
-	ViT는 충분한 크기의 데이터셋에서 사전학습 후, 보다 적은 데이터셋을 가진 task에 transfer learning 시킬 때 좋은 성능을 보임
- model architecture
![ViT](https://github.com/ornni/ViT/blob/main/ViT.png?raw=true)

---

requirements

- Tensorflow version: 2.8.0
- Python version: 3.10.7
- library: Numpy, Pandas, tqdm, os, glob, datetime, PIL, matplotlib, warnings, tensorflow, tensorflow_addons, keras

---

데이터는 특정 대회 사이트를 사용했으므로 데이터를 다운로드 받아 사용해야함 <br/>
이후 모델 돌리기 전 데이터 경로를 바꾼 후에 Vision-Transformer.ipynb 파일을 실행시키면 돌아감 <br/>
데이터 경로: https://dacon.io/competitions/official/236082/overview/description 

---

모델의 디테일은 psudocode에서 별 두개로 표시됨 <br/>
ViT 모델의 도식도대로 진행 <br/>
단, transfer learning은 진행하지 않음 <br/>

---

revision

- 정확도를 높이고 일반화 성능을 높이기 위한 방법을 다양히 적용해본다.
- image의 width와 height 변경
- mlp 레이어 추가
- data augmentation 추가
- parameter 변경 (dropout, tran_test_split, validation_split, epoch)

---

pseudocode

1. Import library
2. Data load
3. Figure hyperparameters
- image의 width와 height 변경
- parameter 변경 (dropout, tran_test_split, validation_split, epoch)
4. Data augmentation
- contrast, translation, rotation 추가
5. Implement Multi-Layer Perceptron (MLP)**
- layer 추가
7. Implement Patch creation as a Layer
9. Implement the patch Encoding Later
10. Build ViT Model**
11. Compile, Train, Evaluate the Model
12. Predict
- test accuracy는 39.6%로같음
- test top 5 accuracy가 70.38%에서 77.94%로 증가
