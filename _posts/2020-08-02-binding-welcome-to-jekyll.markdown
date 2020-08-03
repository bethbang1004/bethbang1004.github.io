---
layout: post
title:  "Atom Editor 설치하기 + github 연동하기"
date:   2020-08-02 21:41:51 +0900
categories: github Atom 설치
---

# Vue.js 사용을 위한 Atom 설치   
무료로 사용가능한 Atom Editor를 설치 입니다. (Mac 설치 기준입니다).   

#### 첫번째,      
Chrome 검색창에 Atom을 검색합니다.   
![Alt text](/assets/atom_search.png "atom_검색")   

#### 두번째,   
본인의 OS에 맞는 다운로드를 진행합니다.   
![Alt text](/assets/atom_download.png "atom_download")   

#### 세번째,   
Atom을 실행합니다.   
![Alt text](/assets/atom_start.png "atom_시작")   

# github 연동하기   
코드 업로드를 용이하게 사용하기 위해 pull, push를 atom 에서도 사용할 수 있게 github를 연동하겠습니다.  
* 본인의 github에 url과 settings가 모두 설정 되어 있다고 가정하고 git연동을 작성하였습니다.   


#### 첫번째,   
Chrome 검색창에 git 다운로드를 검색합니다.   
[git 다운로드]: (https://git-scm.com/downloads)

#### 두번째,   
brew라는 명령어를 terminal에서 없다고 할 수 있습니다. 이럴 때는 homebrew를 설치합니다.  
[homebrew 설치]: (https://brew.sh/index_ko)

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"   

```
![Alt text](/assets/homebrew_install.png "homebrew_설치")   

#### 세번째,   
이제 brew 명령어를 사용하여 git을 설치합니다.   
![Alt text](/assets/brew_install.png "brew_install")   
```
brew install git   

또는
brew install -s git   

```   

#### 네번째,
이제 atom에서 git을 연동해볼까요?   
테스트로 github에 본인의 github.io와 연동하는 방법을 소개합니다(보통 블로그로 많이들 사용하시는 페이지가 될 수 있습니다).   
![Alt text](/assets/atom_git.png "atom_git_연동")   

#### 다섯번째,   
Create Repository를 클릭하여 연동할 git 이름을 작성합니다.   
저처럼 새로 만드셔도 좋아요(예. testProject).   
![Alt text](/assets/repository.png "git_repository")   

#### 여섯번째,  
본인의 github 페이지에서 소스 파일을 다운 받습니다.  
꼭 본인의 github 페이지를 다운받지 않으셔도, 참고할 github가 있다면 그 파일을 다운 받으시면 됩니다.   
[예시 jekyll theme download]: (https://github.com/samarsault/plainwhite-jekyll)   
![Alt text](/assets/git_down_zip.png "git_down_zip")   

#### 일곱번째,   
다운받은 파일을 아까 만들었던 폴더로 이동 시킵니다.   
그리고 zip 파일을 풀어 줍니다. 그러면 폴더 하나가 생기게 됩니다.     
zip 파일은 삭제하여 줍니다.   
![Alt text](/assets/unzip.png "unzip")  

#### 여덟번째,       
Terminal에서 testProject폴더의 경로로 이동하여 git 계정을 연동합니다(git 계정이 없다면 만들어주세요).   
![Alt text](/assets/git_account.png "git_계정설정")   
```
git config --global user.name "git아이디"   

git config --global user.email "git이메일"

git config --list   
```

#### 아홉번째,   
atom으로 돌아가서 testProject 하위로 압축을 풀었던 폴더가 잘 들어 갔는지 확인합니다.   
![Alt text](/assets/atom_set.png "atom_set")    

#### 열번째,   
commit을 하여 적용해 봅니다.   
사진과 같이 Stage All > Commit message 작성 > Commit to master 순으로 클릭하여 주세요.   
![Alt text](/assets/commit.png "commit")   


그러면 본인의 github.io에 내용이 업로드 된 것을 확인 할 수 있습니다.   
