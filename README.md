# Today I learned

## 2020.02.09
### Git basic command
* git init:Initialize repositury
* .git : repository
* git status : working tree status
* git add : add to staging area
* git add . : add all files to staging area
* git commit : create version
* git commit -m "Message"
* git commit -am "Message" : add + commit
* git log : show version
* git log -stat
* git log -p
* git diff
* git checkout commit-ID
* git checkout master

### Change git editor
* git config --global core.editor "nano"

### Reset
* git reset --hard commit-ID
* git reset --soft commit-ID 

### Display log(branch)
* git log --all --grape -- oneline

### Correct coCcommit massage
* git commit --amend  


## 2020.03.12
### Git remote
* git init
* git remote add origin "http adress"
* git pull origin master
* git add *
* git commit -m "Message"
* git push --set-upstream origin master


## 2020.03.20
### pyc compile(pyc_compile.py)  

<pre>
<code>
import py_compile  
py_compile.compile('py file name')
</code>
</pre> 

### bat file(2 python versions)  
C:\Anaconda3\python.exe pyc_compile.py  
C:\Anaconda3\envs\python36\python.exe pyc_compile.py


## 2020.03.23
### DataFrame Error Fix
* ValueError: If using all scalar values, you must pass an index  
* [참조](https://rfriend.tistory.com/482)  

<pre>
<code>
import pandas as pd  
df = pd.DataFrame({'col_1': 1, 'col_2': 2})
</code>
</pre>

* add an index
<pre>
<code>
df = pd.DataFrame({'col_1':1, 'col_2':2}, index=[0])
</code>
</pre>  

* use a list instead of scalar values
<pre>
<code>
df = pd.DataFrame({'col_1':[1], 'col_2':[2]})
</code>
</pre>  

* use pd.DataFrame.from_records() with a list
<pre>
<code>
df = pd.DataFrame.from_records([{'col_1':1, 'col_2':2}])
</code>
</pre>  

* use pd.DataFrame.from_dict([]) with a list
<pre>
<code>
df = pd.DataFrame.from_doct([{'col_1':1, 'col_2':2}])
</code>
</pre>


## 2020.03.27
### 동적 변수 생성
<pre>
<code>
data = ["first", "second", "third"]
for name in data:
    for i in range(1,4):
        globals()[name] = [x*i for x in range(3)]
</code>
</pre>

## 2020.03.28
### json 파일 생성
<pre>
<code>
import json

with open('?????.json', 'w', encoding='utf-8') as make_file:

    json.dump(json_data, make_file, indent="\t")
</code>
</pre>

### json 파일 open
<pre>
<code>
import json

with open('?????.json', 'r') as f:

    admin_info = json.load(f)

print(admin_info)
</code>
</pre>

### 환경변수 불러오기
<pre>
<code>
import os

admin_info_file = os.getenv('NAME')
</code>
</pre>


## 2020.04.02
### Numpy Zero-like
<pre>
<code>
>>> x = np.arange(6)
>>> x = x.reshape((2, 3))
>>> x
array([[0, 1, 2],
       [3, 4, 5]])
>>> np.zeros_like(x)
array([[0, 0, 0],
       [0, 0, 0]])
</code>
</pre>

## 2020.04.12
### Folium Marker icon ref.
 * https://getbootstrap.com/docs/3.3/components/#glyphicons-glyph

## 2020.04.15
### AWS SSH 연결
cmd / powershell 관리자모드로 실행  
ssh -i "AWSKEY.pem" ubuntu@ec2-IP주소.ap-northeast-2.compute.amazonaws.com  
### AWS server 구동
1. python3 application.py : 파이썬 서버 구동
2. Ctrl + Z : 프로세스 중지
3. bg : 백그라운드에서 서버 다시 구동
4. disown -h : 소유권 포기
### 중지
1. netstat -nap | grep {포트 번호}: 특정 포트 번호에서 돌아가는 프로세스를 확인하기
2. kill -9 {프로세스 번호}: 특정한 프로세스를 종료시키기
### 추가
1. jobs : 프로세스 확인
2. fg : 포어그라운드
### key파일없는 PC에서 원격 연결(homepage)
1. ssh mckam@13.125.57.95
2. PASSWORD
3. python3 application.py
4. Ctrl + Z
5. bg
6. disown -h

## 2020.04.16
### KAKAO MAPS API
* Geocoding
<pre>
<code>
url = 'https://dapi.kakao.com/v2/local/search/address.json?query='+addr
headers = {"Authorization": "KakaoAK {Private Key}"}
result = json.loads(str(requests.get(url,headers=headers).text))

if len(result['documents']) !=0:
    match_first = result['documents'][0]['address']
    return float(match_first['y']),float(match_first['x'])
else:
    return None, None
</code>
</pre>


## 2020.05.07
### install python anaconda 32bit envs
* set CONDA_FORCE_32BIT=1
* conda create -n XXXXXXX python=3.7 anaconda

### To activate envs.
* conda activate XXXXXXX
### To deactivate an active envs.
* conda deactivate


## 2020.05.18
### pandas string
<pre>
<code>
# 공백 제거
df['email_strip']  = df['email'].str.strip()  # 앞 뒤 공백을 제거
df['email_lstrip'] = df['email'].str.lstrip() # 앞 공백을 제거
df['email_rstrip'] = df['email'].str.rstrip() # 뒤 공백을 제거

# split(): 구분자를 기준으로 n개로 나눈다, expand=True이면 여러 컬럼, False이면 1개 컬럼에 리스트
df[['email_split_1', 'email_split_2']] = df['email'].str.split('@', n=1, expand=True)

# 치환
df['email_lower']      = df['email'].str.lower()      # 모두 소문자로 변경
df['email_upper']      = df['email'].str.upper()      # 모두 대문자로 변경
df['email_capitalize'] = df['email'].str.capitalize() # 앞문자 대문자로 변경
df['email_title']      = df['email'].str.title()      # 단위별 앞문자 대문자로 변경
df['email_swapcase']   = df['email'].str.swapcase()   # 소문자는 대문자, 대문자는 소문자로 변경 

# 입력 패턴 또는 글자를 대체, 예제에서는 .을 _로 변경
df['email_replace']    = df['email'].str.replace(pat='.', repl='_', regex=False)

# 문자열의 위치(인덱스)
df['email_find']    = df['email'].str.find(sub='.')           # 왼쪽부터 sub값 검색후 위치반환
df['email_findall'] = df['email'].str.findall(pat='[a-zA-Z]') # 찾은 모든 값 반환
df['email_rfind']   = df['email'].str.rfind(sub='.')          # 오른쪽부터 sub값 검색후 위치반환
df['email_index']   = df['email'].str.index(sub='.')          # 왼쪽부터 sub값 검색후 위치반환
df['email_rindex']  = df['email'].str.rindex(sub='.')         # 오른쪽부터 sub값 검색후 위치반환

# 길이 반환
df['email_len']   = df['email'].str.len()              

# 구성 확인
df['email_isalnum']   = df['email'].str.isalnum()   # 알파벳 또는 숫자로만 구성 여부
df['email_isalpha']   = df['email'].str.isalpha()   # 알파벳으로만 구성 여부
df['email_isdecimal'] = df['email'].str.isdecimal() # 숫자문자로만 구성 여부
df['email_isdigit']   = df['email'].str.isdigit()   # 숫자문자로만 구성 여부
df['email_islower']   = df['email'].str.islower()   # 소문자로만 구성 여부
df['email_isnumeric'] = df['email'].str.isnumeric() # 숫자문자로만 구성 여부
df['email_isspace']   = df['email'].str.isspace()   # 공백(Whitespace)으로만 구성 여부
df['email_istitle']   = df['email'].str.istitle()   # TitleCase형태로 구성 여부
df['email_isupper']   = df['email'].str.isupper()   # 대문자로만 구성 여부

# 문자열 패턴
df['email_startswith'] = df['email'].str.startswith(pat='h')     # 좌측값이 입력패턴과 일치 여부
df['email_endswith']   = df['email'].str.endswith(pat='com')     # 우측값이 입력패턴과 일치 여부
df['email_contains']   = df['email'].str.contains(pat='kr', regex=False) # 값 중 패턴포함 여부
df['email_match']      = df['email'].str.match(pat='[a-zA-Z@.]') # 입력패턴과 일치 여부
</code>
</pre>


## 2020.05.19
### OS Module
<pre>
<code>
# 파일 목록 얻기
glob.glob(wildcard) # 유닉스 경로명 패턴 스타일로 파일 목록을 얻을 수 있다.
os.listdir(path) # 지정된 디렉토리의 전체 파일 목록을 얻을 수 있다.
dircache.listdir(path) # os.listdir(path)와 동일한 파일 목록을 전달한다.

# 디렉토리 다루기
os.chdir(path) #작업하고 있는 디렉토리 변경
os.getcwd() # 현재 프로세스의 작업 디렉토리 얻기

# 파일 이름 다루기
os.path.abspath(filename) # 파일의 상대 경로를 절대 경로로 바꾸는 함수
os.path.exists(filename) # 주어진 경로의 파일이 있는지 확인하는 함수
os.curdir() # 현재 디렉토리 얻기
os.pardir() # 부모 디렉토리 얻기
os.sep() # 디렉토리 분리 문자 얻기

# 경로명 분리하기
os.path.basename(filename) # 파일명만 추출
os.path.dirname(filename) # 디렉토리 경로 추출
os.path.split(filename) # 경로와 파일명을 분리
os.path.splitdrive(filename) # 드라이브명과 나머지 분리 (MS Windows의 경우)
os.path.splitext(filename) # 확장자와 나머지 분리
</code>
</pre>


## 2020.05.21
### datetime
<pre>
<code>
import datetime
 
now = datetime.datetime.now()
print(now)          # 2018-07-28 12:11:32.669083

nowDate = now.strftime('%Y-%m-%d')
print(nowDate)      # 2018-07-28
 
nowTime = now.strftime('%H:%M:%S')
print(nowTime)      # 12:11:32
 
nowDatetime = now.strftime('%Y-%m-%d %H:%M:%S')
print(nowDatetime)  # 2018-07-28 12:11:32
</code>
</pre>


## 2020.06.02
### Class member variable
<pre>
<code>
A. dir
class Obj:
    def __init__(self):
        self.x = 9
obj=Obj()
print( dir(obj) )
>>> ['__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'x']

B. __dict__
print(obj.__dict__)
>>> {'x': 9}

</code>
</pre>

### 변수 존재 확인
1. Try / Exception
<pre>
<code>
try : 
     thevariable
exception NameError :
     print('The variablle wasn't defined'_
else :
     print('It is defined') 
</code>
</pre>     
2. variable
<pre>
<code>
if 'myVar' in locals(): # local variable 일 경우
if 'myVar' in globals(): # global variable 일 경우
if  hasattr(obj,'attr_name') : # obj name이 존재할 경우
</code>
</pre>    

## 2020.06.08
### AWS EC2 ubuntu 유저 생성(pem 파일없이 패스워드 사용 접속)
sudo useradd -s /bin/bash -m -d /home/mckam -g root USERNAME

sudo passwd USERNAME
PASSWORD

sudo chmod u+w /etc/sudoers

sudo nano /etc/sudoers
USERNAME ALL=(ALL:ALL) ALL

sudo nano /etc/ssh/sshd_config
PasswordAuthentication yes

sudo service ssh restart

ssh USERNAME@IP ADRESS
PASSWORD


## 2020.06.23
### Pandas DataFrame 중복제거
<pre>
<code>
df.drop_duplicates([A, B], keep='first') # A, B : 중복 여부 기준 Columns
</code>
</pre> 
### Pandas DataFrame index 초기화
<pre>
<code>
df.reset_index(drop=True)
</code>
</pre> 


## 2020.06.27
### 리스트형 내에서의 임의의 외부 숫자 위치 확인
<pre>
<code>
A = [1,4,6,7]
num = 5

A.append(num)
A.sort()
pos = A.index(num)
A.remove(num)
</code>
</pre>


## 2020.06.29
### 파일 실행
<pre>
<code>
import os

os.startfile(filename)
</code>
</pre>


## 2020.07.13
### 구글스프레드시트 주식 데이터 받기
### GOOGLEFINANCE
* KOSPI 지수 10일 데이터 =GOOGLEFINANCE("KRX:KOSPI", "price", Today()-10, Today(), "DAILY")  
* KOSDQ 지수 20일 데이터 =GOOGLEFINANCE("KOSDAQ:KOSDAQ", "price", Today()-20, Today(), "DAILY")  
* KOSPI 종목 현재가 =GOOGLEFINANCE("KRX:035720")  
* KOSDAQ 종목 현재가 =GOOGLEFINANCE("KOSDAQ:258790")
* NASDAQ 종목 현재가 =GOOGLEFINANCE("NASDAQ:SBUX")
* NYSE 종목 현재가 =GOOGLEFINANCE("NYSE:DIS")
 

## 2020.07.14
### SQLite3 데이터 중복 제거
* "DELETE FROM ??? WHERE rowid NOT IN  (SELECT Max(rowid) FROM ??? GROUP BY TITLE order by TITLE)"
* "DELETE FROM Holiday WHERE rowid NOT IN  (SELECT Max(rowid) FROM Holiday GROUP BY Holiday order by Holiday)"


## 2020.07.15
### SQLite3 DataFrame 저장
* df.to_sql('table', conn, if_exists='replace', index=False)


## 2020.07.16
### SQLite3 query
<pre>
<code>
select 시장구분, 종목코드, 종목명, 주식수, 전일종가, 전일종가*주식수 as 시가총액  
            from 종목코드    
            order by 시장구분, 종목코드  
</code>
</pre>


## 2020.07.20
### 크롤링 requests SSLError 해결
* requests.get(url, verify=False)


## 2020.08.08
### Pandas Sorting
<pre>
<code>
df.sort_values(by="A", ascending=False) # ascending=False : 내림차순
df.sort_values(['rank', 'rank1', 'rank2'], ascending=[True,True,True])
</code>
</pre> 
### Pandas Rank
<pre>
<code>
df['rank1'] = df['A'].rank(ascending=False)
</code>
</pre> 


## 2020.09.15
### Pandas String to DateTime
<pre>
<code>
df['col'] = pd.to_datetime(df['col'])
pd.to_datetime(pd.Series(['05/23/2005']))
pd.to_datetime(pd.Series(['05/23/2005']), format="%m/%d/%Y")
</code>
</pre> 


## 2020.09.25
### SQLite3 query
<pre>
<code>
query = """
    SELECT A.날짜, A.기간구분, A.종목코드, C.종목명, B.종가, A.매출액, A.영업이익, A.당기순이익, A.자산총계, A.부채총계, A.자본총계, A.자본금, 
        A.부채비율, A.유보율, A.영업이익률, A.순이익률, A.ROA, A.ROE, A.EPS, A.BPS, A.DPS, A.PER, 1/A.PER as RPER, A.PBR, A.발행주식수, A.배당수익률, C.종목상태
    FROM 재무정보 A, (select 종목코드, 종가 from 일별주가 where 일자 = (select max(일자) from 일별주가 where 일자 <= '%s')) B, 종목코드_주식 C
    WHERE 날짜='%s' and 기간구분='%s' and A.종목코드=B.종목코드 and A.종목코드=C.종목코드
    """ % (날짜, 날짜, 기간구분)
</code>
</pre>


## 2020.09.30
### R
<pre>
<code>
library(boot)
data(nodal)
data(nodal)
a<-c(2,4,6,7)
data <- nodal[,a]
glmModel <- glm(r~., data=data, family = "binomial")
summary(glmModel)
</code>
</pre> 
<pre>
<code>
Moving Averages
Calculate various moving averages (MA) of a series.
SMA(x, n = 10, ...)
</code>
</pre> 
<pre>
<code>
주성분분석 PCA(Principal Component Analysis)
college_s <- scale(college)
summary(college_s
fit <- princomp(college_s)
fit$loadings
</code>
</pre> 
<pre>
<code>
# 최적회귀_변수선택법
step(lm(출력변수~입력변수, 데이터세트), scope=list(lower=~1, upper=~입력변수), direction="변수선택방법")
# 예제
step(lm(y~1, data=df), scope=list(lower=~1, upper=~x1+x2+x3+x4), direction="forward")
</code>
</pre> 


## 2020.10.05
### R
<pre>
<code>
# 연관성 분석 apriori(arules 패키지)
> data(Groceries)
> inspect(Groceries[1:3])
> rules <- apriori(Froceries, parameter=list(support=0.01, confidence=0.3))
> inspect(sort(rules, by=c("lift"), decreasing=TRUE)[1:20])
</code>
</pre>
<pre>
<code>
# 군집분석(k-means)
> data(iris)
> newiris <- iris
> newiris$Species <- NULL
> kc <- kmeans(newiris, 3)
> table(iris$Species, kc$cluster)
> plot(newiris[c("Sepal.Length", "Sepal.Width")], col=kc$cluster)
</code>
</pre>


## 2020.10.09
### R
<pre>
<code>
# reshape 
# 1. melt
> aqm = melt(airquality, id=c('month', 'day'), na.rm=TRUE)
# 2. cast
> a <- cast(aqm, day~month~variable)
</code>
</pre>
<pre>
<code>
# sqldf
> sqldf("select * from [data frame]")
> sqldf("select * from [data frame] limit 10")
> sqldf("select * from [data frame] where [col] like 'char%' ")
</code>
</pre>

## 2020.10.10
### R
<pre>
<code>
# 데이터프레임 조회 
# 1. data.frame에서 바로 조회
> test[test$학과=='경영학과',]
# 2. subset으로 데이터셋 조회
> subset(test, subset=(학과=="경영학과"))
</code>
</pre>


## 2020.10.15
### R
<pre>
<code>
# 반복 
> rep(1,time=5)
> rep(1:4, each=2)
> rep(c, each=2
# 문자 붙이기
> A <- paste("a", "b", "c", sep="-")
> paste(A, c("e", "f"))
> paste(A, 10, sep="")
# 문자열 추출
> substr("Bigdataanalysis",1,4) -> Bigd
# 기초 통계
> mean(변수) # 평균
> sum(변수) # 합계
> median(변수) # 중앙값
> sd(변수) # 표준편차
> var(변수) # 분산
> cov(변수1, 변수2) # 공분산
> cor(변수1, 변수2) # 상관계수
# 파일 읽기
> read.table("파일이름", sep='구분자')
> read.csv("파일이름", header=T)
</code>
</pre>


## 2020.10.21
### R
<pre>
<code>
# 문자열 길이
> nchar("문자열")
# 문자열 연결
> paste("단어1", "단어2", sep='-')
> paste("the pi is approximately", pi)
# 하위문자열 추출
> substr("statistics", 1, 4)
# 날짜 조회
> format(Sys.Data(), '%a') # 요일조회
> format(Sys.Data(), '%b') # 축약된 월이름조회
> format(Sys.Data(), '%B') # 전체 월이름조회
> format(Sys.Data(), '%d') # 두자리 숫자의 일조회
> format(Sys.Data(), '%m') # 두자리 숫자의 월조회
> format(Sys.Data(), '%y') # 두자리 숫자의 연도조회
> format(Sys.Data(), '%Y') # 네자리 숫자의 연도조회
# 날짜 추출
> d <- as.Date("2014-12-25")
> start <- as.Date("2014-12-01")
> end <- as.Date("2014-12-25")
> seq(from=start, to=end, by=1)
</code>
</pre>


## 2020.10.26
### R
<pre>
<code>
# 상관분석
# 분산
> var(x, y=NULL, na.rm=FALSE)
# 공분산
> cov(x, y=NULL, use='everything', method=c('pearson', 'kendall', 'spearman'))
# 상관관계
> cor(x, y=NULL, use='everything', method=c('pearson', 'kendall', 'spearman'))
> rcorr(matrix(data명), type=c('pearson', 'kendall', 'spearman'))
</code>
</pre>

## 2020.10.28
### R
<pre>
<code>
# R 기초 문제
# 1
> x <- 1:100
> sum(x>50)

# 2
> x <- c(1,2,3,NA)
> mean(x)

# 3
> s <- c("Monday", "Tuesday", "Wednesday")
> substr(s, 1, 2)

# 4
> c(2,4,6,8) + c(1,3,5,7,9)

# 5
> set.seed(1000)
> sample(1:1000, 50)

# 6 잘못된 것 찾기
> x<-c(1:4)
> y<-c("apple","banana","orange")
> xy<-x(x,y)
## A. xy는 문자형 벡터
## B. xy의 길이는 7
## C. xy[1] + xy[2]의 결과는 3
## D. xy[5:7]은 y와 동일

# 7 다른 결과 찾기
> A <- cbind(c(1,2,3), c(4,5,6), c(7,8,9))
> colnames(A) <- c("A","B","C")
> rownames(A) <- c("r1","r2","r3")
## A[,"A"}
## A[-c(2,3),]
## A[,1]
## A[, -(2:3)]

# SQL 기초 문제
# 1. ( )는?
SELECT NAME, GENDER, SALARY
FROM CUSTOMERS
WHERE AGE (   ) 20 AND 30

# 2. 해당 SQL문 분석
select customer_name, 고객명, e_customer_name, 고객 영문명
from customer
where e_customer_name like '_A%';

# 3. xy에 대한 설명으로 부적절한 것은?
> x <- c(1:5)
> y <- seq(10,50,10)
> xy <- rbind(x,y)
- 1. 2x5 행렬이다.
- 2. xy[1,]은 x와 동일하다.
- 3. xy[,1]은 y와 동일하다.
- 4. Matrix 타입의 개체이다.
</code>
</pre>

### R reshape
# melt
melt(MYDATA, id=c("no", "day"))

# cast
cast(MD, no+variable~day)
cast(MD, no~variable, mean)
cast(MD, no-variable+day)


## 2020.11.13
### Python openpyxl
#### 1. 엑셀 파일 생성
<pre>
<code> 
from openpyxl import Workbook

# 파일명
fileName = 'TEST.xlsx'
 
# 워크북 생성
wb = Workbook()
 
# 저장
wb.save(fileName)
</code>
</pre>


#### 2. 값 입력
<pre>
<code> 
from openpyxl import Workbook
 
# 파일명
fileName = 'TEST.xlsx'
 
# 워크북 생성
wb = Workbook()
 
# 워크북 활성화
ws = wb.active
 
# 첫번째 입력방법
ws['A1'] = 1
 
# 두번째 입력방법
ws.cell(2,1,'B') # ws.cell(row=2, column=1, value=2)
 
# 세번째 입력방법
ws.append([2,'',4])
 
# 네번째 입력방법
for rng in ws['E1':'F3']:
    for cell in rng:
        cell.value = 'Hello'
 
# 다섯번째 입력방법
for r in range(4,7):
    ws.cell(r,1,'World') # [A4:A6]
 
# 저장
wb.save(fileName)
</code>
</pre>


#### 3. 값 출력
<pre>
<code> 
from openpyxl import Workbook
 
# 파일명
fileName = 'TEST.xlsx'
 
# 워크북 생성
wb = Workbook()
 
# 워크북 활성화
ws = wb.active
 
# 첫번째 입력방법
ws['A1'] = 1
 
# 두번째 입력방법
ws.cell(2,1,'B') # ws.cell(row=2, column=1, value=2)
 
# 세번째 입력방법
ws.append([2,'',4])
 
# 네번째 입력방법
for rng in ws['E1':'F3']:
    for cell in rng:
        cell.value = 'Hello'
 
# 다섯번째 입력방법
for r in range(4,7):
    ws.cell(r,1,'World') # [A4:A6]
 
# 첫번째 출력방법
print(ws['A1'])
 
# 두번째 출력방법
print(ws.cell(2,1).value)
 
# 세번째 출력방법
for rng in ws['E1':'F3']:
    for cell in rng:
        print(cell.value)
 
# 네번째 출력방법
for r in range(4,7):
    print(ws.cell(r,1).value) # [A4:A6]
 
# 저장
wb.save(fileName)
</code>
</pre>


#### 4. 함수 입력
<pre>
<code> 
from openpyxl import Workbook
 
# 파일명
fileName = 'TEST.xlsx'
 
# 워크북 생성
wb = Workbook()
 
# 워크북 활성화
ws = wb.active
 
ws['A1'] = 10
ws['A2'] = 20
ws['A3'] = 30
ws['A4'] = 40
ws['A5'] = '=SUM(A1:A4)' # 합계 함수
 
# 저장
wb.save(fileName)
</code>
</pre>


#### 5. 셀 서식
<pre>
<code> 
from openpyxl import Workbook
 
# 파일명
fileName = 'TEST.xlsx'
 
# 워크북 생성
wb = Workbook()
 
# 워크북 활성화
ws = wb.active
 
# A1 입력 + 형식변경
ws['A1'] = 1000
ws['A1'].number_format = '#,##0'
 
# A2 입력 + 형식변경
ws.cell(2,1,2000).number_format = '#,##0'
 
# B1, B2 입력 + B열 형식변경
ws['B1'] = 3000
ws['B2'] = 4000
for rng in ws['B:B']:
    rng.number_format = '#,##0'
 
# C1:D3 입력 + 형식변경
for rng in ws['C1':'D3']:
    for cell in rng:
        cell.value = 5000
        cell.number_format = '#,##0'
 
# E1, E2, E3 입력 + 형식변경
ws['E1'] = -250
ws['E2'] = 250
ws['E3'] = -300
ws['E4'] = 0
for rng in ws['E1':'E4']:
    for cell in rng:
        cell.number_format = '[RED]#,##0;[BLUE]-#,##0;"-"' # 양수면 빨강 음수면 파랑 0이면 -
 
# 저장
wb.save(fileName)
</code>
</pre>


#### 6. 셀 병합
<pre>
<code> 
from openpyxl import Workbook
from openpyxl.styles import Alignment
 
# 파일명
fileName = 'TEST.xlsx'
 
# 워크북 생성
wb = Workbook()
 
# 워크북 활성화
ws = wb.active
 
# A1:C1 병합
ws.merge_cells('A1:C1')
 
# 가운데맞춤
ws['A1'].alignment = Alignment('center', 'center') # Alignment(horizontal='center', vertical='center') 
 
# A1 입력
ws['A1'] = 'Hello World !'
 
# A1:C1 병합 해제
# ws.unmerge_cells('A1:C1')
 
# 저장
wb.save(fileName)
</code>
</pre>


#### 7. 마지막 행, 열 번호
<pre>
<code> 
from openpyxl import Workbook
 
# 파일명
fileName = 'TEST.xlsx'
 
# 워크북 생성
wb = Workbook()
 
# 워크북 활성화
ws = wb.active
 
# 마지막 행 구하기
print('입력 전: ' + str(ws.max_row))
 
# [A1:A10] 입력
for rng in ws['A1:A10']:
    for cell in rng:
        cell.value = 'Excel'
 
# 마지막 행 구하기
print('입력 후: ' + str(ws.max_row))
 
# 마지막 열 구하기
print('입력 전: ' + str(ws.max_column))
 
# [B1:G1] 입력
for rng in ws['B1:G1']:
    for cell in rng:
        cell.value = 'Python'
 
# 마지막 행 구하기
print('입력 후: ' + str(ws.max_column))
 
# 입력 된 열 구하기
for cell in ws['1:1'].__iter__():
    print(cell.value)
 
# 저장
wb.save(fileName)
</code>
</pre>


#### 8. 테두리
<pre>
<code> 
from openpyxl.styles import Border, Side
from openpyxl import Workbook, styles
 
# 파일명
 
fileName = 'TEST.xlsx'
 
# 워크북 생성
wb = Workbook()
 
# 워크북 활성화
ws = wb.active
 
# B2 입력
ws['B2'] = 'Hello'
# 왼쪽 테두리
ws['B2'].border = Border(left=Side(style='thin'))
# B3 입력
ws['B4'] = 'Excel'
# 왼쪽 테두리
ws['B4'].border = Border(Side('thin'))
 
# D2 입력
ws['D2'] = 'Hello'
# 오른쪽 테두리
ws['D2'].border = Border(right=Side(style='thin'))
# D4 입력
ws['D4'] = 'Excel'
# 오른쪽 테두리
ws['D4'].border = Border(None, Side('thin'))
 
# F2 입력
ws['F2'] = 'python'
# 모든 테두리
ws['F2'].border = Border(left=Side(style='thin'),right=Side(style='thin'),top=Side(style='thin'),bottom=Side(style='thin'))
# F4 입력
ws['F4'] = 'python'
# 모든 테두리
ws['F4'].border = Border(Side('thin'),Side('thin'),Side('thin'),Side('thin'))
 
# 사용자 스타일
THIN_BORDER = Border(Side('thin'),Side('thin'),Side('thin'),Side('thin'))
# H2 입력
ws['H2'] = 'Style'
# 모든 테두리
ws['H2'].border = THIN_BORDER
# H4 입력
ws['H4'] = 'Style'
# 모든 테두리
ws['H4'].border = THIN_BORDER
 
# 범위 테두리 설정
for rng in ws['J2:K10']:
    for cell in rng:
        cell.value = 'All' # [J2:K10] = 'All'
        cell.border = THIN_BORDER # [J2:K10] 모든테두리 설정
 
# 저장
wb.save(fileName)
</code>
</pre>


#### 9. 시트
<pre>
<code> 
from openpyxl.styles import Border, Side
from openpyxl import Workbook, styles
 
# 파일명
fileName = 'TEST.xlsx'
 
# 워크북 생성
wb = Workbook()
 
# 시트1 생성
ws_1 = wb.create_sheet()
 
# 시트2 생성
ws_2 = wb.create_sheet()

# 시트2 시트명 변경
ws_2.title = '시트2'
 
# 시트3 생성 (시트명 정의)
ws_3 = wb.create_sheet('시트3')
 
# 시트명 출력
for sheetName in wb.sheetnames:
    print(sheetName)
 
# 모든 워크시트 A1 입력
for wss in wb.worksheets:
    wss['A1'] = 'python'
 
# 특정 워크시트 A2 입력
ws = wb.get_sheet_by_name('시트3')
ws['A2'] = 'hello'
 
# 저장
wb.save(fileName)
</code>
</pre>


#### 10. Excel to Text
<pre>
<code> 
import openpyxl

def find_parks_not_in_us():
    # 엑셀파일(워크북) 열기
    wb = openpyxl.load_workbook('example.xlsx')
    
    # 워크시트 열기
    sheet = wb.get_sheet_by_name('Sheet1')
    
    # 결과를 저장할 리스트
    parklist = []
    
    # 파일을 로우 단위로 읽어 국가가 US가 아닌 로우를 파일로 쓴다.
    # 1. 파일을 읽을 범위를 결정
    # 2. 로우를 순회하면서 US가 아닌 로우를 리스트로 만든다.
    for row in sheet[2:sheet.max_row]:
        print(row)
        if row[5].value != 'US':
            parklist.append(row)
    wb.close()
    return parklist
    
def make_file(partlist):
    with open('parklist.txt', 'w', encoding='utf-8') as file:
        for item in parklist:
            part_str = make_parkstr(item)
            file.write(park_str + '\n')
            
def make_parkstr(t):
    result_str = ''
    
    for item in t:
        result_str += str(item.value) + '\t'
        
    return result_str
    
def main():
    parklist = find_parks_not_in_us()
    make_file(parklist)
    print('parklist.txt 파일이 생성되었습니다.')
    
if __name__ == '__main__':
    main()
</code>
</pre>


## 2021.01.10
### Python 가상환경 Batch 파일 실행
<pre>
<code>
call conda activate [env_name] 
call cd [path] 
call python [file_name.py]
</code>
</pre>


## 2021.01.13
### Pandas DataFrame 그림파일로 변환
<pre>
<code>
import dataframe_image as dfi

dfi.export(df, 'result.png')
</code>
</pre>


## 2021.01.16
### R
<pre>
<code>
# 차함수
> x <- c(1,2,4,5,7,9,10)
> y <- c(1,2,3,4,5,8,10)
> z <- setdiff(x, y)
7 9
> z <- setdiff(y, x)
3 8
# 교집합
> z <- intersect(x, y)
1 2 4 5 10
</code>
</pre>
