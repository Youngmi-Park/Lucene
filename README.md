# Lucene
## I. What is Lucene?
  - 특징<br/>
    + 자바로 구현된 고성능 정보 검색(IR*, Information retrieval) 라이브러리<br/>
    + 애플리케이션에 정보 검색 기능 추가 가능<br/>
    + 안정적이며 무료로 사용할 수 있는 오픈 소스 프로젝트 - http://lucene.apache.org/<br/>
    + 소프트웨어 재단에서 아파치 소프트웨어 라이센스로 배포<br/><br/> 
  - 장점<br/>
    + API를 통해 최소한의 노력으로 전문(full-text)색인과 검색 기능 사용 가능<br/>
    + 간결하면서도 매우 강력<br/>
  
  <i>* IR (Information Retrieval): 문서를 검색하거나, 문서의 내용을 검색하거나, 문서와 연관된 메타 정보를 검색해 가는 과정</i>
 
### indexing
문서 전체를 두고 검색을 하기위해서는 모든 문서를 대상으로 하나씩 단어나 구문을 찾아야한다. 문서의 양이 많아지고 한 문서의 크기가 커질수록 속도는 느려진다. 원문에서 단어를 추출하고 검색하기 좋은 형태의 문서로 만들어 리스트화 해두면 특정 단어의 위치로 바로 이동할 수 있다.

### indexing과정
  1. 검색 대상 텍스트 확보
  2. 크롤러(crawler)가 색인할 대상 문서 수집
  3. 루씬 문서 생성
     + 원본문서를 루씬의 개별 문서 단위(document)로 변환
     + 텍스트를 추출하고 원하는 텍스트만 필터링하는 작업 필요
     + 루씬 문서는 여러 필드로 구성(제목, 본문, 저자, 링크 등)
  4.문서 텍스트 분석
     + 토큰(token) 생성
     + 어떤 단위로 토큰 할 것인지 결정 필요
     + 동의어, 단수/복수형, 기본형, 대소문자 등의 이슈 처리
     + 루씬 프로젝트에는 다수의 텍스트 분석기 내장
  5. 색인에 문서 추가
     + 색인 과정이 끝난 문서를 색인에 추가

*Lucene는 색인파일을 만들기 위해서 IndexWriter를 제공한다.
### searching 과정
  1. 검색을 하기 위해서 색인 파일의 경로를 알아낸다.
  2. 이를 이용해서, IndexSearcher 생성. (인덱스 파일로부터 검색을 하기 위함)
  3. Analyzer 사용해서 검색어(검색 키워드) 분석 
  4. QueryParser 사용해서 루신에서 사용 가능한 쿼리로 변환
  5. 그렇게 나온 쿼리가 Query 클래스


## II. Lucene - Eclipse
###  1. Preparing the environment
   - Eclipse Install<br/>
   - Tomcat Install<br/>
   - Download Lucene 8.7.0 (https://lucene.apache.org/core/downloads.html)<br/>

###  2. How to Use
   (1) Eclipse 프로젝트 생성<br/>
   (2) Lucene import(Lucene 소스와 라이브러리를 추가하는 과정)<br/>
      + File System을 선택<br/>
      + Lucene 소스 디렉토리를 선택<br/>
      + select all<br/>
      + into folder에 프로젝트 선택<br/>
 
2020.11.17 라이브러리 인식에 문제가 생겨 일단 command-line으로 Lucene demo 소스 코드먼저 살펴봄.

## III. Command line Lucene Demo

환경: Windows 10 / Java / Lucene-8.7.0

### 1. JAVA 환경변수 설정

### 2. 압출 풀고, 데모 위한 jar 4개 복사
 - lucene-core-{버전}.jar<br/>
 - lucene-queryparser-{버전}.jar<br/>	
 - lucene-analyzers-common-{버전}.jar<br/>
 - lucene-demo-{버전}.jar<br/>	

### 3.jar 압축 풀기
```
jar xvf {파일명}.jar
```
<img width="50%" src='https://user-images.githubusercontent.com/53163222/99347881-8341ab80-28db-11eb-9a93-fb90c035f5ba.png'/>

나머지파일도 동일하게 진행<br/>

<img src='https://user-images.githubusercontent.com/53163222/99348222-6eb1e300-28dc-11eb-9f02-69e4085cb783.png'/>

위와 같이 폴더가 생성됨.<br/>

### 4. Index 생성<br/>
java org.apache.lucene.demo.IndexFiles -docs {Index를 생성할 대상 파일들이 있는 폴더 경로}
폴더 안에 있는 모든 텍스트 파일들의 Index를 만들게 된다.

<img width="80%" src='https://user-images.githubusercontent.com/53163222/99349107-78d4e100-28de-11eb-9dab-049500bb4e98.png'/>

*텍스트 파일: 텍스트로 된 파일. html 같이 텍스트로 된 모든 파일을 뜻함. 단순히 txt를 말하는 것이 아님.

테스트 용으로 넣어둔 Lucene파일(lucene-8.7.0)를 대상으로 색인을 생성 
index 폴더가 새로 생기고 Lucene 소스코드 전체 index가 저장됨

<img width="20%" src='https://user-images.githubusercontent.com/53163222/99349581-b1c18580-28df-11eb-84b0-966049573714.png'/>


### 5. 검색

cmd창에 명령어 입력
```
java org.apache.lucene.demo.SearchFiles
```

쿼리(검색) 창이 나옴
```
C:\Users\s_py9\LuceneDemoTest>java org.apache.lucene.demo.SearchFiles
Enter query:
```

Q1. 'String'이 몇 개 있는지 알고싶다.
<img width="80%" src='https://user-images.githubusercontent.com/53163222/99483803-5c01e180-29a2-11eb-8c1b-10aa9f6355d1.png'/>

= 2208 total matching documents

>n: 다음페이지         q: 중단          숫자: 이동하고싶은 페이지

<hr> 

# Lire
## I. What is Lire

Java GPL library for CBIR(content based image retrieval) based on Lucene including multiple low level global and local features and different indexing strategies including bag of visual words and hashing.

- 제공하는 기능
  + Indexing photos
  + Searching photos
  + Browsing the created index
  + Creating mosaic images based on indexed images

## II. Lire Demo

### 1. Lire Demo 다운받기
Lire Demo (https://code.google.com/archive/p/lire/downloads)
-provides a simple GUI interface for

### 2. Lire Demo 실행하기
```
" java -jar LireDemo.jar "
```
Windows의 경우 두 번 클릭해도 실행가능하다.

![image](https://user-images.githubusercontent.com/53163222/99487172-14328880-29a9-11eb-8496-6e925a701080.png)
위와 같은 실행화면이 나타난다.

*Reference<br/>
검색과 색인, 그리고 강력한 지원군 루씬(Lucene) https://m.blog.naver.com/tmondev/220323614797
SemanticMetadata-Lire http://www.semanticmetadata.net/lire/

