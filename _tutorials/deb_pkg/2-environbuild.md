---
layout: tutorial
category: 데비안 패키지 만들기
title: 2. 환경구축
order: 2
---

## 필요한 도구들
### 패키징을 위한 패키지
- ubuntu-dev-tools
    - 패키징을 쉽게 도와주는 tool들을 가지고 있는 패키지
    - devscripts, dpkg-dev, binutild 등의 패키지가 포함되어있음
- devscripts
    - Debian 패키지 관리를 도와주는 script들을 가지고 있는 패키지
    - Dch, debclean, debi, debpkg, debbuild 등의 패키지가 포함되어있음
- dh-make
    - Debian패키지를 만들기 위한 debian디렉토리를 생성해주는 툴
    - Upstream source code를 사용하거나 native debian package를 만들 수 있음

### 패키징 환경을 위한 패키지
- pbuilder
    - 시스템과 분리된 독립된 환경에서 패키지를 빌드할 수 있도록 해주는 tool
    - debootstrp을 이용해서, chroot환경을 만들어줌
- gnupg
    - 전자서명을 위한 도구
    - LaunchPad에 업로드할 패키지를 서명하기 위한 tool
- haveged
    - 난수를 생성하는 도구
    
1. Commiter 정보 등록
    - commit log에 자동으로 작성자와 작성자 메일이 등록되에 설정
    - ~/.bashrc나 ~/.zshrs같은 환경설정 파일에 등록
    - Debian과 Ubuntu에서 사용 가능
        ```bash
        export DEBFULLNAME="Eojin Kim"
        export DEBEMAIL="test@test.com"
        ```
    - Ubuntu에서만 사용 가능
        ```bash
        export UBUMAIL="Eojin Kim <test@test.com>"
        ```
        
1. pbuild환경설정
    - 빌드를 위한 깔끔한 환경을 제공해 줌
    - 시스템의 설정을 수정하지 않고 다양한 빌드환경을 만들어줌
    - Ubuntu나 Debian의 다양한 릴리즈 환경을 지원
    - *pbuilder-dist <release> create* 명령을 사용
        - Ex) pbuilder-dist xenial create
        - Ex) pbuilder-dist zesty create
    ![pbuilder](image/pbuilder.PNG)
