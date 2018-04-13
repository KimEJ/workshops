---
layout: tutorial
category: 데비안 패키지 만들기
title: 3. 패키지 만들기
order: 3
---
### 시작하기 전에
- 프로젝트명은 "hello"로 합시다.
- 다음과 같이 디렉토리를 만들어 줍시다.

    ```bash
    ├ hello
    │   └── src //패키징 하기 위한 소스와 Makefile등이 들어있는 디렉토리
    ```

### Debian 디렉토리 생성
    - "dh_make"명령을 사용해서 debian디렉토리 생성
    - 불필요한 템플릿 파일을 제거
    - 주요 파일에 대한 내용 작성
- 다음 명령어를 사용하여 debian디렉토리를 생성해줍니다.
    ``````bash
    dh_make --native -p hello_1.0.0 -c mit -s
    
