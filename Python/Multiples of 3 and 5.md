## Multiple of 3 and 5

```
If we list all the natural numbers below 10 that are multiples of 3 or 5, we get 3, 5, 6 and 9. The sum of these multiples is 23.

Find the sum of all the multiples of 3 or 5 below 1000.
```

My Answer:
```python
result = 0

for i in range(1,1000):
# 0은 더해도 0이므로 range(1000) 가능
    if (i % 3 == 0) or (i % 5 ==0):
        result += i

print(result)
```

Top Recommended Answer:
```python
sum([x for x in range(1000) if x%3==0 or x%5==0]) 
```
List Comprehension을 사용
```
[표현식 for 항목 in 반복가능객체 if 조건문]
```
이 표현법에 좀 더 익숙해져보자.
