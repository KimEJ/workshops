---
layout: tutorial
category: 런치패드에 가입하기
title: 5. SSH Key를 등록하기
order: 5
---
1. 다음 명령을 입력하여 ssh key를 생성합니다.
    ```bash
    ssh-keygen
    ```
    ![SSH key](img/ssh_key.PNG){: width="50%" height="50%"}
    
1. SSH Key를 복사해 LaunchPad 프로필에 복사합니다.
    ```bash
    cat ~/.ssh/id_rsa.pub
    ```
    
    ![SSH key](img/key.PNG){: width="50%" height="50%"}
    ![userpage](img/user_page2.PNG)
    ![keycopy](img/keycopy.PNG){: width="70%" height="70%"}

1. 런치패드 가입이 끝났습니다!
