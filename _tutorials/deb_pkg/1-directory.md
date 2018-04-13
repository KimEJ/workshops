---
layout: tutorial
category: 데비안 패키지 만들기
title: 1. 패키지 디렉토리
order: 1
---

## 패키징이란
- Application과 그에 관련된 파일들을 쉽게 배포하고 설치하기 위해 묶는것입니다.
- 패키지를 만들고 배포하는 과정까지를 의미입니다.
- iOS나 Android에서 스토어에 App을 배포하는것과 유사합니다.

## Debian 디렉토리
- Debian package를 구성하기 위한 패키지 정보를 담은 디렉토리입니다.
- changelog, control, copyright, rules파일이 가장 중요합니다.
- compat, README, docs, wource/format등 여러 파일들이 있습니다.

### changelog
- Debian 패키지의 변경 기록을 적은 파일입니다.
- 패키지명과 버전, release버전, 변경내역등이 작성됩니다.

#### 작성법
- 버전은 "[upstream 버전]-[debian 버전][우분투 버전]"으로 작성됩니다.
	- Ex) 1.0.0-1ubuntu-1
	- Debian에 없는 패키지의 경우, debian버전을 0으로 표기
- 변경내역에 LaunchPad의 이슈가 있을경우, "LP: #[number]"로 작성합니다.
- 핵심 변경사항은 "*"를 사용해서 표기합니다.
- 핵심변경사항과 관련된 하위 변경사항은 "-"를 사용해서 표기합니다.
- 작성일자는 RFC 5322형식에 맞춰 작성합니다.

#### changelog의 예시
```bash
hello (1.0.0-0ubuntu1) xenial; urgency=medium

	[ kssim ]
	* Initial Release.
	* Major Point
		- Minor Point

	[ test ]
	* major

 -- Eojin Kim <test@test.com> Sat, 11 Mar 2018 09:35:34 +0900
```

### control
- 패키지의 메타 정보를 기록한 파일입니다.
    - Source패키지의 정보와 생성할 debian패키지의 정보를 작성합니다.
- Source패키지 정보
    - Source 이름, architecture, depends, description 등
- Maintainer
    - Ubuntu에서는 maintainer를 Ubuntu Developers로 설정합니다.

#### control의 예시
```bash
Source: hello
Section: misc
Priority: optional
Maintainer: Ubuntu Developers <ubuntu-devel-discuss@lists.ubuntu.com>
XSBC-Original-Maintainer: Eojin Kim <test@test.com>
Build-Depends: debhelper (>=9)
Standards-Virsion: 3.9.6
Hompage: https://test.com
#Vcs-Git: git://test.test.com/test/test.git
#Vcs-Browser: https://test.test.com/test/test.git

Package: hello
Architecture: any
Depends: ${shelibs:Depends}, ${misc:Depends}
Description: sample package.
 ubuntu packaging workshop sample package.
 
Package: hello-devany
Architecture: any
Depends: ${shelibs:Depends}, ${misc:Depends}
Description: developer library for sample package.
 ubuntu packaging workshop sample package.
```

### copyright
- 패키지 내부 파일들의 라이센스를 명시합니다.
- 파일별, 디렉토리별로 나눠서 작성할 수 있습니다.

#### copyright의 예시
```bash
Format: https://www.debian.org/doc/packaging-manuals/copyright-format/1.0/
Upstream-Name: hello
Source: <url://example.com>

Files: *
Copyright: <years> <put auther name and email here>
           <years> <likewise for another auther>
License: MIT

Files: debian/*
Copyright: 2018 Eojin Kim <test@test.com>
License: MIT

License: MIT
 Permission is hereby granted, free of charge, to any person
 obtaining a copy of this software and associated documentation
 files (the "Software"), to deal in the Software without
 restriction, including without limitation the rights to use,
 copy, modify, merge, publish, distribute, sublicense, and/or sell
 copies of the Software, and to permit persons to whom the
 Software is furnished to do so, subject to the following conditions:
 .
 The above copyright notice and this permission notice shall be
 included in all copies or substantial portions of the Software.
 .
 THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
 EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES
 OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
 NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT
 HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY,
 WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
 FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR
 OTHER DEALINGS IN THE SOFTWARE.
```

### rules
- Makefile과 같이 패키지의 빌드를 위한 파일입니다.
- debhelper에 의해 많은 부분이 자동화되어있습니다.
    - dh 명렁을 사용해서 빌드를 수행합니다.
    - 설정을 커스터마이징할 수 있습니다.
- 패키징로그는 "debian/package.debhelper.log"파일에 기록됩니다.

#### rules의 예시
```bash
#!/usr/bin/make -f
%:
    dh $@
    
override_dh_strip:
    dh_strip -Xfoo
```


```bash
#!/usr/bin/make -f
%:
    dh $@

override_dh_auto_build-indep:
    $(MAKE) -C docs
    
override_dh_auto_test-indep:

override_dh_auto_install-indep:
    $(MAKE) -C docs install
```

### 기타 파일
#### README, doc
- 패키지를 사용하기 위한 정보를 담은 파일입니다.
- README나 doc파일을 만들어 내용을 작성합니다.
    - doc파일은 upstream source에 대한 문서입니다.
    - README파일은 비표준적인 특징이 있는 경우 작성합니다.
    
#### source/format
- 초기 생성된 내용을 그대로 유지합니다.
- 소스 패키지의 버전을 명시합니다.
    - 1.0 : 기본 형식(Default값)
    - 3.0 (quilt) : upsteam과 분리된
    - 3.0 (native) : debian native 패키지 (upstream이 없음)

#### install
- dh_install에 의해서 옮겨지는 파일 목록입니다.
- 생성되는 패키지가 하나면, 파일명을 "install"로 설정합니다.
- 여러개의 패키지가 생성되면 "[패키지명].install"로 설정합니다.

#### watch
- upstream패키지를 debian패키지로 만들 때, 선택적으로 사용합니다.
- upstream패키지의 업데이트 상태를 확인합니다.
