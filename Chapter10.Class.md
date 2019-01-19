클래스 정의하기 
==============
1. 클래스 정의
2. 캡슐화의 개념
3. 대화형 그래픽 프로그램 
---------------------

## 객체 다시 보기 

### 객체는 
1. 서로 관계 깊은 정보의 집합 
2. 이 정보를 조작하기 위한 일련의 연산	

#### 
* 정보는 객체 안의 인스턴스 변수에저장된다.
* 메서드라는 연산 은 객체 안의 함수를 말한다. 
* 인스턴스 변수와 메서드를 통틀어 attribute라고한다. 
* 모든 객체는 어떤 클래스의 인스턴스
----------------------------------------------------
### 대포알 예제 
###
```python
from math import sin, cos, radians 
def main():
    angle = float(input("Enter the launch angle (in degrees): "))
    vel = float(input("Enter the initial velocity (in meters/sec): "))
    hO = float(input("Enter the initial height (in meters): "))
    time = float(input( "Enter the time interval between position calculations: "))

    theta = radians(angle)

    xpos = 0
    ypos = hO
    xvel = vel * cos(theta)
    yvel = vel * sin(theta)

    while ypos >= 0.0:
        xpos = xpos + time * xvel
        yvel1 = yvel - time * 9.8
        ypos = ypos + time * (yvel + yvel1)/2.0
        yvel = yvel1

    print("\nDistance traveled: {0:0.1f} meters.".format(xpos))
```

위 코드를 

```python
def main():
    angle, vel, hO, time = getinputs()
    cball = Projectile(angle, vel, hO)
    while cball.getY() >= 0:
        cball.update(time)
    print ("\nDistance traveled: {0: 0 .if} meters.". format (cball.getXO))
```

에서 계산 도중의 변수들을 숨길 수 있게하는 것  함수에 인자가 너무 많을 때 즉 현재 xpos, ypos, xvel, yvel이 사용 되는 때 우리가 대포알의 성질을 이해하는 prohectile이라는 클래스를 가지고 있다면 조금 더 쉬워질 것임 .
이 클래스를 이용해 객체를 만들고 이 객체를 가리키는 변수 하나만으로 객체를 업데이트 하는 방식으로 주 알고리즘을 나타낼 수 있다. 

### 클래스 정의하기 

```
class 클래스 이름:
    변수1
    변수2 
    ,,,,,변수들 처리 ,,,,
    def 메소드1(인수):
    ,,,,,메소드 처리,,,,,,
    def 메소드2(인수):
    ,,,,,,메소드 처리,,,,,
    필요한 만큼 메소드 처리
```
+ 클래스의 장점은 재사용이 가능하다는 것 
+ 복사하여 여기저기 사용가능
+ 수정해야하는 부분이 생긴 경우

클래스 정의 중
1.  self == 셀프 인자 객체를 가르키는 인자 
2.  __init__ 객체를 생성하는 인자 및 객체의 인스턴스 객체를 어떤 값으로 초기화 하는 역할 
----------------------------------------------------------------------------------
## https://wikidocs.net/28

### 발사체 클래스 
```python
class Projectile:
    def __init__(self, angle, velocity, height):
        self.xpos = 0.0
        self.ypos =height
        theta = math.radians(angle)
        self.xvel =velocity* math.cos(theta)
        self.yvel =velocity* math.sin(theta) 
```
클래스 생성 
``` python
from math import sin, cos, radians

    class Projectile:
        def __init__(self, angle, velocity, height):
        self.xpos = 0.0
        self.ypos =height
        theta = math.radians(angle)
        self.xvel =velocity* math.cos(theta)
        self.yvel =velocity* math.sin(theta) 

        def update(self, time):
            self.xpos = self.xpos + time * self.xvel
            yvel1 = self.yvel - 9.8 * time
            self.ypos - self.ypos + time * (self.yvel + yvel1) / 2.0
            self.yvel = yvel1

        def detY(self):
            return self.ypos

        def getX(self):
            return self.xpos

    def getlnputs():
        a= float(input("Enter the launch angle (in degrees): "))
        v = float(input("Enter the initial velocity (in meters/sec): "))
        h = float(input("Enter the initial height (in meters): "))
        t = float(input( "Enter the time interval between position calculations: "))
        return a,v,h,t

    def main():
        angle, vel, hO, time = getlnputs()
        cball = Projectile(angle, vel, hO)
        while cball.getY() >= 0:
            cball.update(time)
            print ("\nDistance traveled: {0: 0 .if} meters.". format (cball.getXO)) 

```




-----------------------------------
번외편 - 클래스 하는 도중 스터디 분들 컴퓨터 런타임 시간이 3시간 연속이라면 쉬라고 자동으로 띄우는 프로그램 짜고 싶었는데 실패 .... 
```python
class Work:
	name=""
	def __init__(self, str):
		self.name = str
	
	def ShowMsg(self):
		print ("Hey" , self.name , "you work hard today, rest now")

Hy000jin = Work("Hy000jin") 
Hy000jin.ShowMsg()

parkjunha98 = Work("parkjunha98")
parkjunha98.ShowMsg()
```
