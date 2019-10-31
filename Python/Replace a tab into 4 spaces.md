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

### 수정코드
```python
for line in lines:
    print("\n" in line)
    print("\t" in line)

    if "\n" in line:
        line = line.replace("\n", "")
        print(line)

    if "\t" in line:
        line = line.replace("\t", "[4spaces]")
        print(line)
    else:
        print(line)
```

```
['Life\tis long\n', 'You    need python']
True
True
Life	is long
Life[4spaces]is long
False
False
You    need python
```

print를 통해 tab을 잘 인식하고 있으며 4개의 공백으로 바꿔지는 것을 확인할 수 있다.

하지만 lines를 그대로 가져오면 replace를 해도 리스트 안에 담긴 line은 그대로이므로 바뀐 결과들을 담을 `new_list`를 만들었다.

### 파일 출력 코드
```python
f = open("C:/Users/gusfk/Desktop/result.txt", 'w')

print(new_list)

for i in range(len(new_list)):
    f.write(new_list[i])

f.close()
```
여기서 처음에 for문 안에서 f.close()를 했더니 다음에 반복될때 닫힌 파일이라고 쓸 수가 없다고 했다. **close()의 위치에 주의하자!!**

출력 파일을 보니 "\n"을 처음에 지워버려서(리스트 안에 있을때 거슬려서 그냥 지웠더니 한줄로 작성이 되어버렸다.) 그 코드를 지웠다.


### 최종결과물
```python
f = open("C:/Users/gusfk/Desktop/test.txt", 'r')
lines = f.readlines()
f.close()

new_list = [] 
for line in lines:

    if "\t" in line:
        line = line.replace("\t", "____")
        new_list.append(line)
    else:
        new_list.append(line)

f = open("C:/Users/gusfk/Desktop/result.txt", 'w')

for i in range(len(new_list)):
    f.write(new_list[i])

f.close()

```
다음과 같다.

tab은 4개의 sapces로 잘 변환되었고 입출력 모두 정상적으로 작동하였다.



---
### 예시답안
