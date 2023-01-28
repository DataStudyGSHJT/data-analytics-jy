# Figure 
- 피겨 객체는 맷플롯립의 그래프 요소를 모두 담고 있는 최상위 객체이다.
- 그래프 그릴 때 자동으로 피겨가 생성되고, 그려진 후 삭제된다.
- 명시적으로 피겨 객체를 만들면 다양한 옵션을 제어할 수 있다.

```
import matplotlib.pyplot as plt

plt.scatter(ns_book7['도서권수'], ns_book7['대출건수'], alpha=0.1)
plt.show()
```

### figsize 매개변수
```
plt.figure(figsize=(900/72, 600/72))
plt.scatter(ns_book7['도서권수'], ns_book7['대출건수'], alpha=0.1)
plt.show()
```
- 튜플로 크기를 지정할 수 있음.
- 기본 그래프의 크기는 (6,4), 각각 너비와 높이.
- 단위는 인치.
- 컴퓨터의 PPI 에 따라 출력되는 크기가 다를 수 있다.


# rcParams(Runtime Configuration Parameters)
- 그래프 기본값을 관리하는 객체.
- 객체에 담긴 값 출력뿐 아니라 값을 변경할수도 있다.
- 변경 이후에 그려진 모든 그래프에 바뀐 설정이 적용된다.

```
# DPI 변경
plt.rcParams['figure.dpi'] = 100

# 스캐터 마커 모양 변경
plt.rcParams['scatter.marker'] = '*'
```


# Axis(축)
- 그래프에서 데이터 좌표를 표현한다.
- 맷플롯립에서는 Axis 클래스로 축 객체를 다룬다.

# Marker
- 그래프에 데이터를 표시하는 방법.
- rcParams 객체나 스캐터 함수의 marker 매개변수로 바꿀 수 있다.


# 서브플롯(subplot)
- 피겨 안에 포함된 그래프 영역, 맷플롯립의 Axes 클래스 객체를 일컫는다.
- 서브플롯은 두 개 이상의 Axis을 포함한다

```
fig, axs = plt.subplots(2)

axs[0].scatter(ns_book7['도서권수'], ns_book7['대출건수'], alpha=0.1)

axs[1].hist(ns_book7['대출건수'], bins=100)
axs[1].set_yscale('log')

fig.show()
```

# Nominal Data vs Ordinal Data
- 순서형 데이터(Ordinal Data): 성적, 등급 처럼 순서가 있는 데이터.
- 명목형 데이터(Nominal Data): 성별, 국가와 같이 순서를 매길 수 없는 데이터.


# line chart
- 데이터 포인트를 직선으로 연결한 그래프
- 시간별 추세를 표현하기 좋음


# bar chart
- 범주형, 명목형 데이터 값의 빈도를 막대 길이로 표현한 데이터





