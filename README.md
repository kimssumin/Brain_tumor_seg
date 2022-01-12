# Brain tumor segmentation

### **주제**:

post-contrast T1-weighted MR image로부터 자동으로 **tumor segmentation**할 수 있는 알고리즘의 개발

---

### **프로젝트의 목적**:

100명의 HGG(high grade glioma) brain tumor 환자의 post-contrast T1-weighted MR image와 이에 상응하는 label을 활용하여 새로운 HGG brain tumor환자의 post-contrast T1-weighted MR image로부터 tumor 영역을 자동으로 segmentation할 수 있는 알고리즘을 개발한다.

</br>

### **데이터설명**:

- nifti format

- array size: 240 x 240 x 155 (3D)

- voxel size: 1 mm x 1mm x 1mm

- unsigned integer (both t1ce and seg)

- skull striping, simple bias correction, image registration이 이미 행해진 데이터임.

- registration과정에서 발생한 영상데이터의 오류에 대해 주의가 필요함 (주로 가장 아래/위 슬라이스들에서 발견).

- label data (seg.nii.gz)는 1, 2, 4로 tumor의 세부 영역을 나누어 표현하고 있으며 각각은 아래와 같은 영역을 나타낸다.

  1: necrotic tumor core

  2: peritumoral edematous/invaded tissue

  4: gadolinium-enhancing tumor

  - Segmentation의 결과는 label data에서의 1 (necrotic tumor core)과 4 (gd-enhancing tumor)영역을 포함하고 있어야 하며, 이 두 영역에 해당하는 voxel은 1을 가지고, 나머지 voxel들은 모두 0을 가져야 함.

</br>

### **Method**

- Preprocessing : Normalization, Augmentation
- Modeling : UNet, Train : Validation = 8 : 2, epoch 150

  <img src="https://user-images.githubusercontent.com/96935132/149073722-ead7cae7-27ef-4b93-b007-eb87bcbdd6ab.PNG" width="400" height="200"/>

</br>

### **Result**

![image](https://user-images.githubusercontent.com/96935132/149072863-1d0f6fda-5ed2-4fdc-918c-a08f36bb6d3c.PNG)
