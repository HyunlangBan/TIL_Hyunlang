## Replace a tab into 4 spaces
기존에 하고 있던 [Jump to Python](https://wikidocs.net/book/1)을 이어서 풀도록 하겠다.

문서파일을 읽어서 그 문서 파일 안에 있는 탭을 공백 4개로 바꿔주는 스크립트를 작성해야한다.

### 첫코드
```python
f = open("C:/Users/gusfk/Desktop/test.txt", 'r')
lines = f.readlines()
f.close()

for line in lines:
    if "\t" in line:
        line.replace("\t", "    ")


f = open("C:/Users/gusfk/Desktop/test.txt", 'w')
for i in range(len(lines)):
    f.write(line[i])
    f.close()

```

처음에는 이렇게 작성하였으나 출력 파일에서 아무것도 나타나지 않았다.
그래서 입력/출력 파일을 따로 만들고 입력 코드부터 차근차근 점검해보기로 했다.


```python
f = open("C:/Users/gusfk/Desktop/test.txt", 'r')
lines = f.readlines()
f.close()

for line in lines:
    if "\t" in line:
        line.replace("\t","tab")
        print(line)
```

입력 파일은

Life'\t'is too long

You    need Python

이었는데

결과는
```
Life	is long

```
이다.

문제: Tab을 찾아내지 못한다, 바꾸지도 못한다.

