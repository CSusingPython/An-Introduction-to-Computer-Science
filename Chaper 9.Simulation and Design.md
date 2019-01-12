Simulation and Design
=====================
1. pseudo-random numbers
2. MonteCarlo simulations
3. top-down and spiral design techniques
4. unit testing-implementation and debugging of complex programs
------------------------------------------------------

## 1. Pseudo-random Numbers & MonteCarlo simulations
### 
1. Our simulation program will have to deal with uncertain events.
2. Many simulations share this property of requiring events to occur with a certain likelihood.
3. These sorts of simulations are sometimes called Monte Carlo algorithms because the results depend on "chance" probabilities.

####
1. 파이썬의 경우 random 모듈을 사용해서 랜덤한 수를 뽑아낼 수 있음. 
2. 알고리즘 엔진은 Mersenne Twister 생성기가 사용됨.
3. 기본 유사난수 발생과 메르센 트위스터 구현 참고자료  [기본 유사 난수 발생과 메르센 트위스터 구현](https://kplus-biz.github.io/%EC%98%88%EC%A0%9C/2017/10/27/%EA%B8%B0%EB%B3%B8-%EC%9C%A0%EC%82%AC-%EB%82%9C%EC%88%98-%EB%B0%9C%EC%83%9D%EA%B3%BC-%EB%A9%94%EB%A5%B4%EC%84%BC-%ED%8A%B8%EC%9C%84%EC%8A%A4%ED%84%B0-%EA%B5%AC%ED%98%84/)

#### random 모듈의 대락적인 구조
```
import random
random.random()
```
#####
1. random 모듈 내부에는 Random이라는 클래스가 정의되어 있음.
2. 사용자가 random 모듈을 import 하는 순간 Random클래스는 자동적으로 인스턴스화 된다. (Random 클래스의 객체가 하나 생성되는 것)
3. _inst 가 Random 클래스의 객체이다. Random객체에는 random이라는 메소드가 있다. random=_inst.random 메소드를 binding해서 random이라고 사용하는 것 
4. 자세한 random에 대한 내용은 tistory 블로그 참조 [파이썬 random 모듈로 난수 생성하기](http://thrillfighter.tistory.com/416)

#### 몬테카를로 시뮬레이션 

1. 몬테카를로 시뮬레이션은 램덤의 숫자와 확률을 이용하여 문제를 해결하는 기법
2. 가장 간단한 예제는 원주율의 크기를 예측하는 프로그램을 만들어보는것 
- 반지름이 1인원과 그원을 둘러싼 사각형이 있다. 
- 이 사각형안에 무작위로 10000000 번의 점들을 직는다. 
- 이점들이 원 안에 떨어질 확률은 원 넓이/사각형 넓이, 즉 Pi/4임 
- 점들이 원안에 떨어지는 횟수는 10000000*(원의넓이(PI)/사각형 넓이)
- PI= numberOfHits/1000000

```
import random 
NUMBER_OF_TRIALS = 10000000
numberOfHits=0

for i in range(NUMBER_OF_TRIALS): #점이 떨어지는 위치 
	x=random.random()*2-1
	y=random.random()*2-1
	
	ifx*x+y*y<=1: #점이 떨어지는 위치가 원 안인 경우 numberOfHits에 +1
		numberOfHits+=1
		
pi=4*numberOfHits/MUMBER_OF_TRIALS

print("PL is",pi)

```
참고자료 [몬테카를로 메소드 및 원주율 정밀도](http://swlab.jnu.ac.kr/wordpress/2018/01/30/probability-and-statistics-monte-carlo-method/)
,[파이썬과 주가 몬테카를로 시뮬레이션](https://m.blog.naver.com/PostView.nhn?blogId=jihyeloves&logNo=220637704330&proxyReferer=https%3A%2F%2Fwww.google.com%2F)

## 3.top-down and spiral design techniques

### 하향식
1. 하항식 설계과정 
####  1. 여러개의 부분 문제로 알고리즘을 나타낸다. 
  2. 각 부분 문제사이의 인터페이스를 정의한다. 
  3. 각 부분 문제에 인터페이스를 준수하는 세부사항을 채워넣는다. 
  4. 모든 부분 문제에 대해 이 과정을 반복한다. 
  5. 참고자료 [Python을 사용하여 알고리즘 및 데이터 구조로 문제 해결](http://interactivepython.org/runestone/static/pythonds/index.html),[알고리즘 깃허브 공부자료](https://github.com/keon/algorithms)
#### 2.대체로 쓰일 수 있는 부분 프로토타이핑과 나선형 개발 
  1. prototype 명세 설계 구현 테스트 를 거쳐 전체문제를 한번에 해결하는 대신에 먼저  프로토타입에 대한 설계와 구현 그리고 테스트를 거친뒤에 프로토타입이 원하던 프로그램에 이를때까지 점진적으로 작은 개발주기를 돌며 기능을 추가해 나아가는 방식 

 ```
 from random import random
def simOneGame():
	scoreA = 0
	scoreB = 0
	serving = "A"
	for i in range(30):
		if serving == "A" :
			if random() < .5:
				scoreA = scoreA + 1
			else:
				serving = "B"
		else:
	if random() < .5:
		scoreB = scoreB + 1
	else:
		serving = "A"
print(scoreA, scoreB)
if __ name __ == '__ main __' : simOneGame()
```
  2. 반복문 몸체 끝 부분에 print명령문을 사용한것 중간 과정의 점ㅁ수를 출력하면 프로토타입 프로그램의 경기 양상 확인 가능 
  3. 교재의 선수 문제인 경우에서 일반적으로 승률을 정해서 이에 대해 n을 확인하여 구상한것과는 조금 다르게 50퍼센트의 확률을 이미 가정한 후에 이를 프로토타입으로 둔다.
  4. 인자추가 형식을 통해서 선수의 랠리 승률이 다르게 만드는 것 , 이후에 프로그램을 확장하는 것
  5. 익숙하지 않은 개발이나 초보 프로그래머에게 좋은 방법이라고 보임. 보완제의 성격 
## 4. unit testing-implementation and debugging of complex program
