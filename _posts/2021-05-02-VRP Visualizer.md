---

layout: single

title: "VRP visualizer"

classes: wide

---

## Summary

## VRP Visualizer 개발 목적

- VRP 알고리즘의 결과물인 배달 경로를 1. solver와 분리된 환경에서 2. 실시간으로 시각화하기 위해 VRP Visualizer를 새로 개발하였습니다.
- 기존 VRP simualtor의 단점
  - 기존 VRP simulator의 GUI는 데이터 입력을 수동으로 처리해야하여 실시간 시각화가 불가능했습니다.
  - 지도 및 아이콘이 직관적이지 않아 변경이 필요했으나 GUI의 추가/변형이 어렵기 때문에 VRP simulator를 재활용하기 어려웠습니다.
- 개선 방안
  - solver의 성능에 영향을 끼치면 안되기 때문에 solver와 분리된 환경에서 동작하도록하였습니다.
    - solver로부터 라이더의 현재위치/목적지/배달가방 용량등의 데이터를 통신받아 visualizer 프로세스에서 이를 시각화합니다.
  - 새로 입력된 데이터를 자동으로 업데이트하여 실시간 시각화가 가능하도록 하였습니다.

## Class Diagram

![image](https://user-images.githubusercontent.com/57242033/116805277-33d8fa00-ab60-11eb-971a-c1cf03f3d612.png)

## Flow Chart

## Class


### Vehicle
- 역할

  - 배달 차량의 클래스인 Vehicle은 현재 위치와 목표 위치를 바탕으로 차량의 움직임을 구현합니다.

- function

  - ```__init__(screen, start, target, rad)```

    ```python
    def __init__(self,screen,start,target,rad=25):
            self.node_current = np.array(start)
            self.node_target = np.array(target)
            self.speed = list((self.node_target-self.node_current)/120)
            
            self.vehicle = Rect(list(self.node_current-[rad,rad])+[2*rad,2*rad])
    
            
            self.screen = screen
            
            pygame.draw.ellipse(self.screen,(0, 0, 255),self.vehicle)
    ```

    - 차량 객체의 초기값을 설정합니다.
    - 입력받은 값대로 현재 위치, 목표 위치를 저장하고 속도를 연산하여 저장합니다.
    - 현재 위치를 토대로 차량 도형을 생성하고 입력받은 screen상에 도형을 출력합니다.

  - ```move()```

    ```python
    def move(self):
            self.vehicle.move_ip(self.speed)
            self.node_current = self.vehicle.center
            pygame.draw.ellipse(self.screen,(0, 0, 255),self.vehicle)
    ```

    ![vehicle1](https://user-images.githubusercontent.com/57242033/116806928-2d03b480-ab6b-11eb-8ec9-fa4a3558f372.png)

    - 차량의 현재 좌표를 원의 중앙 좌표로 설정합니다.
    - 현재 좌표 - 목표 좌표를 frame으로 나눠 속도를 구합니다.
    - 매 프레임마다 계산한 속도만큼 이동하여 차량의 움직임을 구현합니다.
    - 원은 박스의 좌상단을 기준으로 생성되므로 $(x-r,y-r)$에 원을 생성합니다.

  - ```isArrived()```

    ```python
    def isArrived(self):
            distance = self.node_current - self.node_target
            distance = np.linalg.norm(distance)
    
            if distance < 1:
                return True
            else:
                return False
    ```

    - 목적지 도착 여부는 차량의 중심이 목표 좌표와 일치하는지로  판단합니다.
    - 다만 차량이 소수점 단위의 속도를 가져 정확하게 일치하지 않을 수 있습니다.
    - 따라서 현재 좌표와 목표 좌표의 L2-norm이 1보다 작은지로 판단합니다.

- Elements

  1. node_current

     - 현재 x, y 좌표값
     - numpy array (1x2)
  2. node_target
  
     - 목적지 x, y 좌표값
     - numpy array (1x2)
  3. speed

- Vehicle전체 소스 코드

```python
import pygame
from pygame.locals import *
from pygame.rect import *

import numpy as np

class Vehicle():
    def __init__(self,screen,start,target,rad=25):
        self.node_current = np.array(start)
        self.node_target = np.array(target)
        self.speed = list((self.node_target-self.node_current)/120)
        
        self.vehicle = Rect(list(self.node_current-[rad,rad])+[2*rad,2*rad])

        
        self.screen = screen
        
        pygame.draw.ellipse(self.screen,(0, 0, 255),self.vehicle)
        
    def move(self):
        self.vehicle.move_ip(self.speed)
        self.node_current = self.vehicle.center
        pygame.draw.ellipse(self.screen,(0, 0, 255),self.vehicle)
        
    def isArrived(self):
        distance = self.node_current - self.node_target
        distance = np.linalg.norm(distance)

        if distance < 1:
            return True
        else:
            return False
```

### Customer

### Store


### Manager