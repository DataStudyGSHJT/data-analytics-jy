# 객체지향 API(Objected-orientd API)
- 명시적으로 피겨 객체와 서브플롯 객체를 만들고, 해당 객체의 메서드를 사용하여 맷플롯립 그래프를 그리는 방법
- 맷플롯립 사용해서 그래프 그리는 방식은 두 가지(pyplot, 객체지향 API 방식)

### pyplot 방식 예시
```
import matplotlib.pyplot as plt

plt.rcParams['figure.dpi'] = 100
plt.plot([1, 4, 9, 16])
plt.title('simple line graph')
plt.show()
```

### 객체지향 API 방식 예시
```
fig, ax = plt.subplots()
ax.plot([1, 4, 9, 16])
ax.set_title('simple line graph')
fig.show()
```

# Color map
<img width="827" alt="image" src="https://user-images.githubusercontent.com/35182238/215870867-c5939063-599c-4088-b516-dc09aba3fd0b.png">

- 맷플롯립에서 그래프를 그리는 데 사용하기 위해 사전에 정의한 색상 리스트
- 값에 따른 색상을 다르게 표현, 기본은 컬러맵은 virdis


# Color bar
- 컬러맵의 색깔이 어떤 값에 대응하는지 참조 정보를 제공하는 막대

```
fig, ax = plt.subplots(figsize=(10, 8))

sc = ax.scatter(ns_book8['발행년도'], ns_book8['출판사'], 
                linewidths=0.5, edgecolors='k', alpha=0.3,
                s=ns_book8['대출건수']**1.3, c=ns_book8['대출건수'], 
                # jet 컬러맵을 사용
                cmap='jet')
ax.set_title('출판사별 발행도서')

# 컬러맵을 figure에 표시
fig.colorbar(sc)

fig.show()
```

# 스택 영역 그래프(Stacked area chart)
<img width="703" alt="image" src="https://user-images.githubusercontent.com/35182238/215870938-6eab688e-98bb-41e7-9f7c-180fdd23b1b7.png">


- 여러 개의 선 그래프를 y축 방향으로 쌓은 그래프, 선 아래로 색상이 채워져 영역 형태로 표현된다
```
fig, ax = plt.subplots(figsize=(8, 6))
# 위에서 추출한 year_cols 을 x축
ax.stackplot(year_cols, ns_book10.loc[top10_pubs].fillna(0), labels=top10_pubs)
# ns_book10[ns_book10.loc[top10_pubs].fillna(0)].plot.area(ax=ax, title='년도별 대출건수', xlim=(1985, 2025)))

ax.set_title('년도별 대출건수')
# 왼쪽에 표시
ax.legend(loc='upper left')

# x 축 limit 설정
ax.set_xlim(1985, 2025)
fig.show()
```

# pivot table
<img width="979" alt="image" src="https://user-images.githubusercontent.com/35182238/215871328-f959cc79-c937-4c61-a872-bf98e5813148.png">

- 테이블 형태의 데이터를 평균, 합 등의 방식으로 집계하여 만든 요약표

```
# 출판사를 index로 발행년도를 column 으로 데이터 구조를 바꿈
# fill_value 으로 누락값을 초기화해주면 추후에 데이터프레임.fillna(0) 할 필요 없음.
ns_book10 = ns_book9.pivot_table(index='출판사', columns='발행년도', fill_value=0)
ns_book10.head()

ns_book11 = ns_book7[top30_pubs_idx].pivot_table(
    index='발행년도', columns='출판사', 
    values='대출건수', aggfunc=np.sum)
ns_book11.loc[2000:2005]
```

# 스택 막대 그래프(Stacked bar chart)
<img width="536" alt="image" src="https://user-images.githubusercontent.com/35182238/215871009-3fabb1c7-8254-494d-8a97-e4b5d9a2ec9a.png">

- 여러 개의 그래프를 y 축 방향으로 쌓은 그래프
- 막대 위에 막대가 누적되듯이 표현된다
- 맷플롯립에서는 이 기능을 제공하지 않아 시작 위치를 조정하는 식으로 그려야함. 판다스에서는 제공함.

```
zip: 여러 개의 순회 가능한(iterable) 객체를 인자로 받고, 
각 객체가 담고 있는 원소를 튜플의 형태로 차례로 접근할 수 있는 반복자(iterator)를 반환
원소끼리 더한 배열
height3 = [a + b for a, b in zip(height1, height2)]

plt.bar(range(5), height3, width=0.5)
plt.bar(range(5), height1, width=0.5)
plt.show()
```

# 원 그래프(Pie chart)
<img width="571" alt="image" src="https://user-images.githubusercontent.com/35182238/215871060-8cafa402-c03c-48e9-9776-f4b1927eabdf.png">

- 전체 데이터에 대한 비율을 부채꼴로 나타낸 그래프
```
plt.pie([10,9], labels=['A제품', 'B제품'], startangle=90)
plt.title('제품의 매출비율')
plt.show()

or

fig, ax = plt.subplots(figsize=(8, 6))
ax.pie(data, labels=labels)
ax.set_title('출판사 도서비율')
fig.show()
```



