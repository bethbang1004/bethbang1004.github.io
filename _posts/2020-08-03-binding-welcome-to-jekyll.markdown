---
layout: post
title:  "Mac에서 Node.js 설치하기"
date:   2020-08-03 21:41:51 +0900
categories: Mac Node.js 설치
---

# Mac에서 Node.js 설치하기      
npm 명령어를 사용하기 위해 node.js를 설치하겠습니다.      

#### 첫번째,      
Chrome 검색창에 **Nodejs 설치** 를 검색합니다.   
![Alt text](/assets/search_node.png "nodejs_검색")   

#### 두번째,   
Mac OS 다운로드를 진행합니다.   
![Alt text](/assets/download.png "download")   

#### 세번째,   
다운받은 Nodejs를 설치합니다.       

#### 네번째,      
Terminal을 실행하여, 아래와 같은 명령어를 입력합니다.     
```   
npm install vue   
```
![Alt text](/assets/install_vue.png "install_vue")    

#### 다섯번째,   
전역으로 vue-cli를 설치합니다. 만약 로컬에만 설치하고 싶다면 -g 옵션을 생략하고 명령어를 작성하시면 됩니다(-g 옵션: global).   
**vue-cli: 기본 vue 개발 환경을 설정해주는 도구**
```
sudo npm install -g @vue/cli
```
![Alt text](/assets/vue_cli.png "vue_cli")    

#### 여섯번째,   
npm이 잘 설치되었는지 버전을 확인합니다.   
```
npm -version   
```
![Alt text](/assets/version.png "version")     

이로써, 설정이 완료되었습니다 :)   
