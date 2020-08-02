---
layout: post
title:  "Atom Editor 설치하기 + github 연동하기"
date:   2020-08-02 21:41:51 +0900
categories: github Atom 설치
---

# Vue.js 사용을 위한 Atom 설치   
무료로 사용가능한 Atom Editor를 설치 입니다. (Mac 설치 기준입니다).   

첫번째,      
Chrome 검색창에 Atom을 검색합니다.   
![Alt text](/assets/atom_search.png "atom_검색")   

두번째,   
본인의 OS에 맞는 다운로드를 진행합니다.   
![Alt text](/assets/atom_download.png "atom_download")   

세번째,   
Atom을 실행합니다.   
![Alt text](/assets/atom_start.png "atom_시작")   

# github 연동하기   
코드 업로드를 용이하게 사용하기 위해 pull, push를 atom 에서도 사용할 수 있게 github를 연동하겠습니다.   

첫번째,   
Chrome 검색창에 git 다운로드를 검색합니다.   
[git 다운로드]: https://git-scm.com/downloads

두번째,   
brew라는 명령어를 terminal에서 없다고 할 수 있습니다. 이럴 때는 homebrew를 설치합니다.  
[homebrew 설치]: https://brew.sh/index_ko  

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"   

```
![Alt text](/assets/homebrew_install.png "homebrew_설치")   

세번째,   
이제 brew 명령어를 사용하여 git을 설치합니다.   
![Alt text](/assets/brew_install.png "brew_install")   
```
brew install git   

또는
brew install -s git   

```   

네번째,   
git 계정을 연동합니다(git 계정이 없다면 만들어주세요).   
![Alt text](/assets/git_account.png "git_계정설정")   
```
git config --global user.name "git아이디"   
```

```
git config --global user.email "git이메일"
```

```
git config --list   
```

다섯번째,
이제 atom에서 git을 연동해볼까요?   
테스트로 github에 본인의 github.io와 연동하는 방법을 소개합니다(보통 블로그로 많이들 사용하시는 페이지가 될 수 있습니다).   
![Alt text](/assets/atom_git.png "atom_git_연동")   

여섯번째,   
