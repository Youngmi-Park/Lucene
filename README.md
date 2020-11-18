#  I. Lucene
###  1. What is Lucene?
  - 특징<br/>
    + 자바로 구현된 고성능 정보 검색(IR*, Information retrieval) 라이브러리<br/>
    + 애플리케이션에 정보 검색 기능 추가 가능<br/>
    + 안정적이며 무료로 사용할 수 있는 오픈 소스 프로젝트 - http://lucene.apache.org/<br/>
    + 소프트웨어 재단에서 아파치 소프트웨어 라이센스로 배포<br/><br/> 
  - 장점<br/>
    + API를 통해 최소한의 노력으로 전문(full-text)색인과 검색 기능 사용 가능<br/>
    + 간결하면서도 매우 강력<br/>
  
  <i>* IR (Information Retrieval): 문서를 검색하거나, 문서의 내용을 검색하거나, 문서와 연관된 메타 정보를 검색해 가는 과정</i>
 
# II. Lucene - Eclipse
###  2. Preparing the environment
   - Eclipse Install<br/>
   - Tomcat Install<br/>
   - Download Lucene 8.7.0 (https://lucene.apache.org/core/downloads.html)<br/>

###  3. How to Use
   (1) Eclipse 프로젝트 생성<br/>
   (2) Lucene import(Lucene 소스와 라이브러리를 추가하는 과정)<br/>
      + File System을 선택<br/>
      + Lucene 소스 디렉토리를 선택<br/>
      + select all<br/>
      + into folder에 프로젝트 선택<br/>
 
2020.11.17 라이브러리 인식에 문제가 생겨 일단 command-line으로 Lucene demo 소스 코드먼저 살펴봄.

<hr>
# III. Command line Lucene Demo
환경: Windows 10 / Java / Lucene-8.7.0
### 1. JAVA 환경변수 설정

### 2. 압출 풀고, 데모 위한 jar 4개 복사
 - jar	위치<br/>
   + lucene-core-{버전}.jar<br/>
   + lucene-queryparser-{버전}.jar<br/>	
   + lucene-analyzers-common-{버전}.jar<br/>
   + lucene-demo-{버전}.jar<br/>	

### 3.jar 압축 풀기
```jar xvf {파일명}.jar```
<img src='image](https://user-images.githubusercontent.com/53163222/99347881-8341ab80-28db-11eb-9a93-fb90c035f5ba.png'/>

나머지파일도 동일하게 진행<br/>

<img src='https://user-images.githubusercontent.com/53163222/99348222-6eb1e300-28dc-11eb-9f02-69e4085cb783.png'/>

위와 같이 폴더가 생성됨.<br/>

### 4. 색인 생성<br/>
java org.apache.lucene.demo.IndexFiles -docs {색인할 대상이 파일들이 있는 폴더 경로}
폴더 아래 있는 모든 텍스트 파일들의 색인을 만들게 된다.

<img src='https://user-images.githubusercontent.com/53163222/99349107-78d4e100-28de-11eb-9dab-049500bb4e98.png'/>

*텍스트 파일: 텍스트로 된 파일. html 같이 텍스트로 된 모든 파일을 뜻함. 단순히 txt를 말하는 것이 아님.

테스트 용으로 넣어둔 Lucene파일(lucene-8.7.0)를 대상으로 색인을 생성 
index 폴더가 새로 생기고 Lucene 소스코드 전체 index가 저장됨

<img src='https://user-images.githubusercontent.com/53163222/99349581-b1c18580-28df-11eb-84b0-966049573714.png'/>


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
<img src='https://user-images.githubusercontent.com/53163222/99483803-5c01e180-29a2-11eb-8c1b-10aa9f6355d1.png'/>

= 2208 total matching documents

*n: 다음페이지     q: 중단     숫자: 이동하고싶은 페이지
*Reference<br/>
검색과 색인, 그리고 강력한 지원군 루씬(Lucene) https://m.blog.naver.com/tmondev/220323614797

