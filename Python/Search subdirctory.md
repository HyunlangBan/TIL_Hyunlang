### Search Subdirectory
특정 디렉터리부터 시작해서 그 하위 모든 파일 중 파이썬 파일(*.py)만 출력하기

하위 디렉토리를 어떻게 하면 다 확인할 수 있을까부터 막막했다.
하지만 저번에 배웠던 glob함수가 기억났고 이걸로 서브디렉토리들도 확인할 수 있지 않을까 생각되어
구글링을 했더니 고대로 나왔다..하하

```python
import sys
import glob

cur_path = sys.argv[1]
print(cur_path)

for filename in glob.iglob(cur_path+'/**/*.cpp', recursive=True):
    print(filename)

```

내가 이전에 실습하느라 저장해놓은 cpp파일들이 많아서 cpp파일들로 해봤더니 아주 잘 나온다.

```python
python ttt.py C:/Users/gusfk/desktop
```
로 실행했고


결과는
```
...
C:/Users/gusfk/desktop\CSC265\quiz2_1.cpp
C:/Users/gusfk/desktop\CSC265\RSA.cpp
C:/Users/gusfk/desktop\CSC265\rsubset.cpp
C:/Users/gusfk/desktop\CSC265\test.cpp
C:/Users/gusfk/desktop\CSC265\매\ham_graph.cpp
C:/Users/gusfk/desktop\Discrete Structure\PA1\primes.cpp
C:/Users/gusfk/desktop\Discrete Structure\PA2\powerset.cpp
C:/Users/gusfk/desktop\Discrete Structure\PA3\rsubset.cpp
C:/Users/gusfk/desktop\Discrete Structure\PA5\graph.cpp
C:/Users/gusfk/desktop\Discrete Structure\PA6\ham_graph.cpp
C:/Users/gusfk/desktop\Discrete Structure\PA7\graph_template_breadth_first.cpp
C:/Users/gusfk/desktop\Discrete Structure\PA8\djikstra.cpp
C:/Users/gusfk/desktop\git_hban\git_cpp\books.cpp
C:/Users/gusfk/desktop\git_hban\git_cpp\lab2-part1.cpp
C:/Users/gusfk/desktop\git_hban\git_cpp\lab2-part2.cpp
C:/Users/gusfk/desktop\git_hban\git_cpp\lab2-part3.cpp
C:/Users/gusfk/desktop\git_hban\git_cpp\lab3-part1.cpp
....
```
위와 같이 다양한 하위 폴더들에서 찾아낸 것을 볼 수 있다.

>glob에서 **가 무슨 의미인지 확인해보니
>
>In other words, while /x/*/y will match:
>
>/x/a/y
>/x/b/y
>and so on (only one directory level in the wildcard section), the double asterisk /x/**/y will also match things like:
>
>/x/any/number/of/levels/y
>
>라고 한다.
>
>https://stackoverflow.com/questions/32604656/what-is-the-glob-character

---

### 예시답안
```python
import os

def search(dirname):
    try:
        ## 해당 위치에 있는 모든 파일과 폴더들을 리스트에 담는다.
        filenames = os.listdir(dirname)   
        ## 리스트에 담긴 이름들을 하나씩 확인한다.
        for filename in filenames:
            ## 정확한 path를 설정하기 위해서 앞서 설정했던 위치와 join한다.(os.path.join: 경로와 파일명을 합침)
            full_filename = os.path.join(dirname, filename)
            ## 만약 full_filename이 디렉토리라면 다시 search함수를 다시 적용한다.
            if os.path.isdir(full_filename):
                search(full_filename)
            ##아니라면 확장자가 .py인지를 확인하고 출력한다.
            else:
                ## os.path.splitext: 파일명에서 확장자만 따로 떨어뜨린다. (경로 , 확장자)로 출력되기 때문에 인덱스로 확장자만 선택
                ext = os.path.splitext(full_filename)[-1]
                if ext == '.py': 
                    print(full_filename)
    ## PermissionError: os.listdir를 수행할 때 권한이 없는 디렉터리에 접근하더라도 프로그램이 오류로 종료되지 않고 그냥 수행되도록
    except PermissionError:
        pass

search("c:/")
```
나는 glob모듈을 사용해서 짧게 만들 수 있었고 이 답안은 os의 여러 함수들을 이용하여 재귀함수를 다 구현하였다.
glob모듈에서 recursion을 저렇게 간단하게 만들 수 있다니 감동적이다.
