# Object Detection 조사

# Person / Vehicle / Object Detection

### Abstract

---

- 사람, 자동차 모두 object detection의 범주에 속하므로 object detection 네트워크에 대해 조사함

![Object%20Detection%20%E1%84%8C%E1%85%A9%E1%84%89%E1%85%A1%203f94683e7b084b1eabd42739bb9566f7/Untitled.png](Object%20Detection%20%E1%84%8C%E1%85%A9%E1%84%89%E1%85%A1%203f94683e7b084b1eabd42739bb9566f7/Untitled.png)

- generic object detection network
    - FoveaBox : classification + bounding box
        - 사전에 anchor box를 정의하지 않아도 됨
    - CornerNet : classificatioin + bounding box
        - lite 버전의 경우 영상 처리 속도가 빠름
- semantic segmentation network
    - BANet-R : object detection
        - 블러가 있는 영상에 강점을 가짐
        - 블러 처리 속도가 가장 빠름

## 1. Generic Object Detection (Bounding Box)

---

### FoveaBox

---

![Object%20Detection%20%E1%84%8C%E1%85%A9%E1%84%89%E1%85%A1%203f94683e7b084b1eabd42739bb9566f7/Untitled%201.png](Object%20Detection%20%E1%84%8C%E1%85%A9%E1%84%89%E1%85%A1%203f94683e7b084b1eabd42739bb9566f7/Untitled%201.png)

- 특징
    1. 기존 object detection SOTA 모델들이 사용하는 **anchor box를 사용하지 않음**
        - anchor box

            ![Object%20Detection%20%E1%84%8C%E1%85%A9%E1%84%89%E1%85%A1%203f94683e7b084b1eabd42739bb9566f7/Untitled%202.png](Object%20Detection%20%E1%84%8C%E1%85%A9%E1%84%89%E1%85%A1%203f94683e7b084b1eabd42739bb9566f7/Untitled%202.png)

            - object의 다양한 scale과 aspect ratio에 대한 참고 역할
            - anchor가 모델의 성능에 영향을 끼침
    2. anchor reference없이 **object가 존재할 확률,  bounding box 좌표를 학습**

        ![Object%20Detection%20%E1%84%8C%E1%85%A9%E1%84%89%E1%85%A1%203f94683e7b084b1eabd42739bb9566f7/Untitled%203.png](Object%20Detection%20%E1%84%8C%E1%85%A9%E1%84%89%E1%85%A1%203f94683e7b084b1eabd42739bb9566f7/Untitled%203.png)

    3. 부가 기능을 추가하지 않고 standard COCO, Pascal VOC object detection benchmark에서 **state of the art를 달성**함

        ![Object%20Detection%20%E1%84%8C%E1%85%A9%E1%84%89%E1%85%A1%203f94683e7b084b1eabd42739bb9566f7/Untitled%204.png](Object%20Detection%20%E1%84%8C%E1%85%A9%E1%84%89%E1%85%A1%203f94683e7b084b1eabd42739bb9566f7/Untitled%204.png)

        ![Object%20Detection%20%E1%84%8C%E1%85%A9%E1%84%89%E1%85%A1%203f94683e7b084b1eabd42739bb9566f7/Untitled%205.png](Object%20Detection%20%E1%84%8C%E1%85%A9%E1%84%89%E1%85%A1%203f94683e7b084b1eabd42739bb9566f7/Untitled%205.png)

        - paper : [https://arxiv.org/ftp/arxiv/papers/1904/1904.03797.pdf](https://arxiv.org/ftp/arxiv/papers/1904/1904.03797.pdf)
        - github : [https://github.com/taokong/FoveaBox](https://github.com/taokong/FoveaBox)

---

### CornerNet

---

![Object%20Detection%20%E1%84%8C%E1%85%A9%E1%84%89%E1%85%A1%203f94683e7b084b1eabd42739bb9566f7/Untitled%206.png](Object%20Detection%20%E1%84%8C%E1%85%A9%E1%84%89%E1%85%A1%203f94683e7b084b1eabd42739bb9566f7/Untitled%206.png)

- 특징
    1. 다른 Classification Network에 비해 평균 성능이 높음

        ![Object%20Detection%20%E1%84%8C%E1%85%A9%E1%84%89%E1%85%A1%203f94683e7b084b1eabd42739bb9566f7/Untitled%207.png](Object%20Detection%20%E1%84%8C%E1%85%A9%E1%84%89%E1%85%A1%203f94683e7b084b1eabd42739bb9566f7/Untitled%207.png)

    2. lite버전의 경우 YOLOv3보다 준수한 성능을 보임

        ![Object%20Detection%20%E1%84%8C%E1%85%A9%E1%84%89%E1%85%A1%203f94683e7b084b1eabd42739bb9566f7/Untitled%208.png](Object%20Detection%20%E1%84%8C%E1%85%A9%E1%84%89%E1%85%A1%203f94683e7b084b1eabd42739bb9566f7/Untitled%208.png)

        ![Object%20Detection%20%E1%84%8C%E1%85%A9%E1%84%89%E1%85%A1%203f94683e7b084b1eabd42739bb9566f7/Untitled%209.png](Object%20Detection%20%E1%84%8C%E1%85%A9%E1%84%89%E1%85%A1%203f94683e7b084b1eabd42739bb9566f7/Untitled%209.png)

- paper : [https://arxiv.org/pdf/1904.08900.pdf](https://arxiv.org/pdf/1904.08900.pdf)
- 깃허브 : [https://github.com/princeton-vl/CornerNet-Lite](https://github.com/princeton-vl/CornerNet-Lite)

---

## 2. Semantic Segmentation

---

### BANet-R

---

![Object%20Detection%20%E1%84%8C%E1%85%A9%E1%84%89%E1%85%A1%203f94683e7b084b1eabd42739bb9566f7/Untitled%2010.png](Object%20Detection%20%E1%84%8C%E1%85%A9%E1%84%89%E1%85%A1%203f94683e7b084b1eabd42739bb9566f7/Untitled%2010.png)

- 특징
    1. Object Detection을 학습

        ![Object%20Detection%20%E1%84%8C%E1%85%A9%E1%84%89%E1%85%A1%203f94683e7b084b1eabd42739bb9566f7/Untitled%2011.png](Object%20Detection%20%E1%84%8C%E1%85%A9%E1%84%89%E1%85%A1%203f94683e7b084b1eabd42739bb9566f7/Untitled%2011.png)

    2. 이미지 블러를 single forward pass로 처리하여 deblurring 네트워크 중 속도가 가장 빠름

        ![Object%20Detection%20%E1%84%8C%E1%85%A9%E1%84%89%E1%85%A1%203f94683e7b084b1eabd42739bb9566f7/Untitled%2012.png](Object%20Detection%20%E1%84%8C%E1%85%A9%E1%84%89%E1%85%A1%203f94683e7b084b1eabd42739bb9566f7/Untitled%2012.png)

        ![Object%20Detection%20%E1%84%8C%E1%85%A9%E1%84%89%E1%85%A1%203f94683e7b084b1eabd42739bb9566f7/Untitled%2013.png](Object%20Detection%20%E1%84%8C%E1%85%A9%E1%84%89%E1%85%A1%203f94683e7b084b1eabd42739bb9566f7/Untitled%2013.png)

        - paper : [http://cvteam.net/projects/ICCV19-SOD/BANet.html](http://cvteam.net/projects/ICCV19-SOD/BANet.html)