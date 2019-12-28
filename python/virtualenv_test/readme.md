# vitualenv 환경 만들기 
> 목표 리눅스 깡똥 서버에서 offline 에서
> python tensorflow 돌릴 수 있도록 환경 설정

## 환경 
> 가상환경 생성 서버 환경 
>> 서버 centos 7.3
>> python 3.6.8

> 대상 서버 환경
>> 깡통 centos 7.5 예정
>> python3.6 및 gcc, rpm 만 설치되어 있음 (가정)

## 가상환경 생성
> 가상환경 생성 (python3.6 설치되있는 환경)
```
가상환경 생성
pip3 install virtualenv
virtualenv --python=python3 venv
virtualenv -p /usr/bin/python2.6 env
python -m venv env
가상환경 접속 
source venv/bin/activate
// 접속후 python 경로 확인하기 :  which python3
필요한 패키지 설치하기
ex) pip install tensorflow==1.15
    pip install joblib
가상환경 빠져 나오기
deactivate
```

## 기본 설치파일 준비
```
    - gcc 및 패키지 설치 준비 
1. 패키지 로컬 설치하기 : yum install --downloadonly --downloaddir=<directory> <package>
ex) yum install --downloadonly --downloaddir=./ gcc
    yum install --downloadonly --downloaddir=./ make
    yum install --downloadonly --downloaddir=/data/bin/zlib_devel zlib-devel
    yum install --downloadonly --downloaddir=/data/bin/openssl openssl
    yum install --downloadonly --downloaddir=/data/bin/openssl openssl-dev
2. 파이썬 설치파일 준비 (python 공식 페이지)
3. 설치 패키지
pip3 download virtualenv

export LD_LIBRARY_PATH=/data/env/lib
```

## 도커 대상서버 테스트(깡통 서버)
```
    - 의존성 패키지 설치
준비해둔 rpm 디렉토리로 이동하여 
rpm -Uvh *

    - python 설치
1. 파이썬.zip 압축 해제 
ex) tar xf Python-3.6.8
2. 압축해제한 디렉터리로 이동하여 빌드
./configure     --> gcc 설치 후 가능
make            --> make 설치 후 가능
make test
make install    --> zlib_devel 설치 후 가능

    - 패키지 설치
해당 패키지로 이동하여 python3 -m pip install "파일명"
<-- 패키지 설치시 openssh, openssh-dev 설치 후 가능
1. virtualenv  
    - 가상환경 접속
  ./bin/activate 경로변경
activate 편집
40번 라인의   VIRTUAL_ENV= 경로를 가상환경 시작 디렉토리로 변경
ex) VIRTUAL_ENV="/data/venv/env"
python3 link 파일을 설치된 파일로 연결
python 설치 위치 확인
which python3 
나온 경로를 대상 경로로 설정
ln -Tfs ~~나온경로~~ python3 
pip.py 경로변경 (pip3 등 전부) -> 가장위의 주석 부분 
python 링크 경로 변경  
-> python3만 바꾸면 python은 python3를 보기때문에 다바뀜
ln -Tfs [새로바꿀경로] [바꿀심볼릭링크]
(바꿀 위치는 대상 서버에서 python3 설치 후 which python3 로 나온 경로 삽입)
```