# 웹 공격

## SQL Injection

* Easy Level
> SQL문을 살펴보면 "SELECT first_name, last_name FROM users WHERE user_id = '$id" 이렇한 형태로 주어진 것을 확인할 수 있다.
> 입력창안에 1을 넣었을 경우 1 user_id 가 1인 first name 과 last name을 출력해준다. 때문에 or '1' = '1를 넣어준다. 이렇게 될 경우에 "SELECT first_name, last_name FROM users where user_id = ''OR 1 = 1 #
> 위 SQL문을 확인해 보면 '를 이용해 where 절에 싱글쿼터를 닫아준다 그 후 or 1=1을 이용해 where절을 모두 참으로 만들어주고 #을 이용해 나머지 부분을 주석처리 해준다. 
* Medium Level

> Medium Level 같은 경우에는 직접 입력하는 것이 아니라 input type = checkbox 형태인 것 을 확인할 수 있다. 이럴경우에는 Burp Suite를 사용한다. Input을 넘기기전에 intercept를 하여 input의 형태를 변환해주는 것이다. input의 원래 값은 id=1&Submit=Submit 이렇게 되어있는 것을 볼 수 있다. 하지만 우리는 이것을 id = 1 or 1 = 1# 이렇게 변형을 준다. 이렇게 되면 id의 값이 or로 인해서 무조건 true가 되는 것을 볼 수가 있다. 
* Hard Level


## SQL Injection Blind
* Easy Level
> SQL Injection Blind는 입력을 넣었을 경우 true or false 형태로 반환을 해준다. 이를 이용하여 원하는 정보를 SQL문을 통해 얻을 수 있는 데 예를 들면 1 'and ascii(substr((select first_name from users where user_id = '1'), 1, 1)) > 91 #. 이것이 무슨 의미를 갖냐면, user의 firstname의 첫번째 문자의 ascii코드가 91 보다 크냐고 물어보는 것이다. 이렇게 입력할 경우에 답을 true나 false 얻을 수 있고, 이것을 기반하여 여러가지 SQL문을 주어 얻고자 하는 정보를 추려낼 수 있다.
> 하지만 이렇게 할 경우에는 하나 하나 다 넣어줘야하는 번거로움이 있기 때문에, 파이썬을 이용한 Tool을 사용한다. 이 TOOL은 자동으로 모든 경우의 수를 SQL문으로 넣어줘 해킹을 가능하게 해준다. 

* Medium Level
> Medium level 또한 Easy Level과 접근이 비슷합니다. 다른 것은 단지 GET 방식에서 POSt방식으로 바뀐다는 부분입니다. 때문에 SQLMAP에서 파이썬으로 모든 경우의 수를 줄 때 --data 를 입력으로 넣어줘야 합니다 . 

## XSS Stored
* Easy Level
> XSS는 웹 어플리케이션에서 스크립트 구문 (<,>)를 필터링하지 않을 시에 사용자가 고의적으로 악성 스크립트르 삽입하는 것이 가능하다.
게시판 등 사용자가 글을 작성 시킬 수 있는 공간에 악성 스크립트가 저장되어 타 사용자가 악성스크립트가 삽입된 게시글을 열람시 정보가 탈취되는 취약점이 있다.
``` html
    <script> alert("hello") </script> 
```
>이렇게 XSS를 넣고 제출할 경우 XSS script가 실행이 되면서 hello 라고 알림창이 뜨는 것을 볼 수가 있다. 이것을 활용해 다른 사용자가 이 게시물을 열었을 때 세션정보를 얻을 수 있다. 세션정보를 얻은 후 그 세션정보로 웹사이트의 대한 권한을 얻을 수 도 있다. 

* Medium Level
> Medium level같은 경우에는 script가 쓰여질 경우 웹사이트에서 그것을 빈칸으로 대체한다. 때문에 전 처럼 XSS를 넣었을 경우에는 그냥 alert("...") 메세지가 출력이 된다.
``` html
    <sc<script>ript> alert("hello") </scri<script>pt>
```
>이런 형식으로 넣어준다. 문제점은 이런 형식으로 메세지칸에 넣어주면 소스코드에서 모든 메세지 앞에 "/"를 넣어주는 구문이 있기 때문에 XSS가 실행이 되지 않는다. 이걸 우회하기 위해 NAME 필드에 저 script 구문을 넣어준다. NAME 필드는 input의 사이즈를 10으로 한정지었기 때문에 google inspect element를 사용하여 길이를 늘려준다. 그 후 SCRIPT 구문을 넣어주어 웹 공격을 실시하면 된다.

## Command Injection

*Easy Level
> Command Injection 은 말 그대로 command에서 입력하는 명령어를 넣어주는 방법이다. Input 창에 ip주소를 넣었을 때, ping을 결과로 출력을 해주지만 예를 들면
``` cmd
127.0.0.1 && ls
```
이런 형태로 넣어주면 그 다음 명령어인 ls 까지 실행되는 것을 확인할 수 있다. && 으로 넣어줘도 되고 ||로 넣어줘도 되고 | 또는 & 하나만 넣어도 다 실행되는 것을 확인할 수 있다.

*Medium
> Medium 같은 경우에는 소스코드에서 "&&"나 ";"를 빈칸으로 바꿔저는 구문이 있다. 그러므로 "&" 나 "||" 문자들을 써줘서 구문을 우회해준다.

* High
> High Level 같은 경우에는 대부분에 AND와 OR를 표현하는 문자가 소스코드 구문에서 막혀있지만 단 한 가지 "|" 가 유효하다. 떄문에 이 문자를 활용하여 우회하면 된다.

## File Upload
*Easy
> Easy Level같은 경우에는 단순히 php파일을 업로드하면 된다. php파일에서 아래에 있는 코드 형식으로 넣어준다.
``` php
<pre>
<?php system($_GET['cmd']) ?>
</pre>
```
> get방식으로 cmd를 변수로 받아드려 system 함수를 실행시키는 방식이다. 
소스코드에서 파일의 타입을 구분하고 있지 않기 때문에 php파일이 업로드가 가능하다. php 파일을 업로드 한 후 hackable/uploads 경로로 가서 그 경로에서 php파일을 누르게 되면 그 안에 있는 코드들이 실행된다. 

*Medium
>  Medium Level 같은 경우에는 소스코드에서 파일 형식을 JPEG 나 PNG일 때만 업로드가 가능하게 된다. 왜 그렇나 소스코드를 보면 소스코드에서 사이즈 제한을 두기 때문이다. 이것을 우회할려면 지난 번 처럼 intercept를 한 후에 content-type을 보면 image/png가 아닌 것을 볼 수 있다. 이것을 단순히 image/png으로 바꿔주고 /hackable/uploads를 가서 php 파일을 실행하면 php파일안에 있는 명령들을 실행할 수 가 있다.
