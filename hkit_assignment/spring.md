# 1 수행형 과제

## 1.1 목표 시스템의 환경 요구 사항에 대한 분석 능력 [p.5]
* 목표 시스템을 정하고, 그에 해당하는 환경을 분석해 보자.
  - 목표 시스템 : 급,상여, 퇴직금, 연말정산을 계산하는 급여관리 웹 애플리케이션 시스템
  - 환경
    - 개발 언어 : Java, HtML5, CSS3, Spring, jQuery, Javascript, Ajax, SQL
    - 개발 인원 및 기간 : 4명, 12개월
    - 개발 HW 사양 : AP서버(2) -> CPU(787,273tmpC 이상), 메모리(47,756MB 이상)
                    DB서버(1) -> CPU(198,363tmpC 이상), 메모리(15,750MB 이상)
                    웹 서버(2) -> CPU(249,389tpmC 이상). 메모리(5,793MB 이상)
                    개발 서버(1) -> CPU(184,865tpmC 이상), 메모리(4,010MB 이상)

## 1.2 개발 도구들의 역할에 대한 파악도 [p.7]
* 목표 시스템 개발에 활용한 도구들을 나열하고 역할에 설명해 보자.
```
  - Visual Studio Code : HTML5, CSS3 사용하기 위함
  - Eclipse : Java, jQuery, Javascripta 사용하기 위함
  - MySql : sql 사용하기 위함
```
## 1.3 형상관리 지침의 이해와 환경 구축 능력 [p.22]
* 형상관리(SCM)의 정의를 설명해 보자.
```
소프트웨어의 개발 과정에서 발생하는 산출물의 변경 사항을 버전 관리하기 위한 일련의 활동
```

* 각자 형상관리툴에 이름과 이메일을 등록해 보자.(등록된 내용은 출력해서 붙여 넣기)
```console
diff.astextplain.textconv=astextplain
filter.lfs.clean=git-lfs clean -- %f
filter.lfs.smudge=git-lfs smudge -- %f
filter.lfs.process=git-lfs filter-process
filter.lfs.required=true
http.sslbackend=openssl
http.sslcainfo=C:/Users/Hajin_2/AppData/Local/Programs/Git/mingw64/ssl/certs/ca-
bundle.crt
core.autocrlf=true
core.fscache=true
core.symlinks=false
credential.helper=manager
user.name=JJins
user.email=nanee9556@gmail.com
```


# 2 실행형 과제

## 2.1 만들고자 하는 서비스의 서버프로그램 구현
![](https://github.com/HappyJJins/Jeong-Hajin/blob/master/hkit_assignment/index.png?raw=true)

## 2.2 서버프로그램에 대한 unit test 수행

### unit test 라이브러리 설치
* 설치
```console
$ pip3 install Flask
```

* 설치 결과
```console
Requirement already satisfied: flask in /home/hkit10/.local/lib/python3.8/site-packages (1.1.2)
Requirement already satisfied: Jinja2>=2.10.1 in /usr/lib/python3/dist-packages (from flask) (2.10.1)
Requirement already satisfied: click>=5.1 in /usr/lib/python3/dist-packages (from flask) (7.0)
Requirement already satisfied: Werkzeug>=0.15 in /home/hkit10/.local/lib/python3.8/site-packages (from flask) (1.0.1)
Requirement already satisfied: itsdangerous>=0.24 in /home/hkit10/.local/lib/python3.8/site-packages (from flask) (1.1.0)
```

### 테스트 파일 추가
* test_app.py
```python
import flask

app = flask.Flask(__name__)

with app.test_request_context('/'):
    assert flask.request.path == '/'
```

### unit test 실행

* 실행 방법
```console
$ pytest
```

* 실행 결과
```console

Command 'pytest' not found, but can be installed with:

apt install python-pytest
Please ask your administrator.

```

## 2.3 수행형 과제에서 선정한 서비스에 대한 공통 모듈 구현
![](https://github.com/HappyJJins/Jeong-Hajin/blob/master/hkit_assignment/board.png?raw=true)

## 2.4 공통 모듈에 대한 unit test 수행

### unit test 라이브러리 설치

### 테스트 파일 추가
* test_app.py
```python
import flask

app = flask.Flask(__name__)

with app.test_request_context('/'):
    assert flask.request.path == '/'

```

### unit test 실행

* 실행 방법
```console
$ pytest
```

* 실행 결과
```console

Command 'pytest' not found, but can be installed with:

apt install python-pytest
Please ask your administrator.

```


## 2.5 잠재적 보안 취약성 제거를 위한 secret_key or CSRF Protection 적용

### csrf 라이브러리 설치
* 설치
```console
$ pip3 install Flask-WTF
```
* 설치 결과 
```console
Collecting Flask-WTF
  Downloading Flask_WTF-0.14.3-py2.py3-none-any.whl (13 kB)
Requirement already satisfied: itsdangerous in /home/hkit10/.local/lib/python3.8/site-packages (from Flask-WTF) (1.1.0)
Requirement already satisfied: Flask in /home/hkit10/.local/lib/python3.8/site-packages (from Flask-WTF) (1.1.2)
Collecting WTForms
  Downloading WTForms-2.3.1-py2.py3-none-any.whl (169 kB)
     |████████████████████████████████| 169 kB 349 kB/s
Requirement already satisfied: click>=5.1 in /usr/lib/python3/dist-packages (from Flask->Flask-WTF) (7.0)
Requirement already satisfied: Jinja2>=2.10.1 in /usr/lib/python3/dist-packages (from Flask->Flask-WTF) (2.10.1)
Requirement already satisfied: Werkzeug>=0.15 in /home/hkit10/.local/lib/python3.8/site-packages (from Flask->Flask-WTF) (1.0.1)
Requirement already satisfied: MarkupSafe in /usr/lib/python3/dist-packages (from WTForms->Flask-WTF) (1.1.0)
Installing collected packages: WTForms, Flask-WTF
Successfully installed Flask-WTF-0.14.3 WTForms-2.3.1
```

### CSRF 적용
* app.py
```python
    :
    :
from flask_wtf.csrf import CSRFProtect

app = Flask(__name__)
app.secret_key = 'very secret'
csrf = CSRFProtect(app)
    :
    :
```
* getPosts.html
```html
{% extends "layout.html" %}

{% block section %}
<h2>게시물 리스트</h2>
<ul>
    {% for post in posts %}
    <li><a href="getPost.html?csrf_token={{ csrf_token() }}&no={{post.no}}">{{post.subject}}</a> - {{post.content}}</li>    {% endfor %}

</ul>
<a href="addPost.html">추가</a>
{% endblock %}
```

### 작동 확인
* 콘솔에서 확인
```console
hkit11@ubuntu:~/tinypetshop$ hkit10@ubuntu:~/tinypetshop$ python3 app.py
 * Serving Flask app "app" (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: on
Traceback (most recent call last):
  File "app.py", line 28, in <module>
    app.run(port="5110", host="0.0.0.0", debug=True)
  File "/home/hkit11/.local/lib/python3.8/site-packages/flask/app.py", line 990, in run
    run_simple(host, port, self, **options)
  File "/home/hkit11/.local/lib/python3.8/site-packages/werkzeug/serving.py", line 1030, in run_simple
    s.bind(server_address)
OSError: [Errno 98] Address already in use
```
* 브라우저에서 확인
[본인 화면 복사]
[샘플]
![](https://github.com/luibelstudy/hkit_2020_gonggong/blob/master/3.%20%EC%84%9C%EB%B2%84%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%A8%20%EA%B5%AC%ED%98%84/%ED%8F%89%EA%B0%80/hkit01.PNG?raw=true)
