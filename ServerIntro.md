# 연구용 리눅스 서버 사용법 정리
## 리눅스 서버란?
- 리눅스 : 리누스 토발즈가 제작한 운영체제 커널
- 많은 사람들이 이용하는 중 (서버 용도)
- 장점 : 적은 기본 메모리, 다중 사용자용 설계 -> 서버에 적합
- 단점 : 명령어를 외워야 된다. 
- 데비안, 우분투, 페도라, 수세 등 다양한 베포판 존재
## 학교 리눅스 서버
- 2가지 존재 (구서버, 신서버)
- 머신러닝, 인공지능 -> 신서버
- 운영체제 -> 구서버
- IP 주소 
  - 구서버 : 115.23.235.135
  - 신서버 : 115.23.235.150
## 접속 방법
- putty 프로그램 이용
  - putty 프로그램 설치 
    - [다운로드 링크](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) 
    - msi, exe 두 방법 모두 가능
  - ![puttystart](https://user-images.githubusercontent.com/90604899/169722194-239d76f4-ad5a-4003-9159-00a390cb40d7.png)
  - host name : 접속하고 싶은 서버의 IP 주소
    - 구서버 : 115.23.235.135
    - 신서버 : 115.23.235.150
  - 포트 : 서버에 어떤 포트로 접속할 것인지
    - 구서버 : 443
    - 신서버 : 22
  - key 얘기가 나오면 Accept
  - login as : gs학번 (아이디 치는 것)
- cmd 
  - 신서버 : `ssh gs20000@115.23.235.150`
  - 구서버 : `ssh -p 443 gs20000@115.23.235.135`
  - 비번은 동일
- filezilla
  - filezilla client 설치
    - [다운로드 링크](https://filezilla-project.org/download.php?platform=win64)
  - 왼쪽 위 파일 -> 사이트 관리자
  - ![filezilla](https://user-images.githubusercontent.com/90604899/169722502-9717cade-073d-4f75-a1dd-bf8a88d088c7.png)
  - New site 클릭
  - 프로토콜 : SFTP
  - 호스트 : 115.23.235.135 or 115.23.235.150
  - 포트 : 구서버=443, 신서버=22
  - 로그인유형 : 일반
  - 사용자 : gs학번
  - 비밀번호 : 자신의 비밀번호
  - 연결 클릭
  - 자신의 컴퓨터와 서버와의 저장공간 사이 연결 -> 양방향 전송 가능
## 기본 정보
- 사용자 계정
  - 아이디 : gs학번
  - 비번 : 아이디1234
- 홈디렉트리
  - 개인 디렉토리 (자동 할당)
    - /src/아이디
    - 용량 제한은 아직 없으나 과도하게 많을시 경고
  - 다른 디렉토리로 갈 일 거의 없음
- 권한
  - 다른 사람들 폴더 내부 파일 이름은 볼 수 있어도 내용은 볼 수 없다. or 실행은 할 수 없다. 
  - 관리자 권한 : 박종화 선생님, 송혁중 (gs20059)
    - 무언가를 까는데 관리자 권한이 필요하다면 개인적 연락
## 기본 명령어
- `cd` : 이동
- `ls` : 현재 있는 폴더의 파일들 출력
- `mkdir` : 폴더 만들기
- `cat` : 내부 텍스트 모두 보기
- `tail` : 뒤 문장들만 보기
- `vim` : 메모장 역할 in Linux
## 서버 정보 확인 방법
- `ps -ef` 
  - 현재 어떤 프로세스가 돌아가고 있는지
  - `ps -ef | grep 아이디`
     - 자신의 아이디 (계정)
- `htop`
  - 더 잘 정리된 서버 사용 화면
- `nvidia-smi`
  - 현재 GPU 사용량 표시
    - 10개의 GPU 사용량 보고 자기 프로그램 할당하기
## 파이썬 사용 방법
- 가상환경 사용방법
  - 다양한 패키지를 사용하고 원하는 버전이 다 다르다
  - 각자 개인용 가상환경을 만들어서 파이썬을 돌려야 한다.
  - 생성 방법
    - `mkvirtualenv 환경이름 -p python3`
  - 삭제 방법
    - `rmvirtualenv 환경이름`
  - 시작 방법
    - `workon 환경이름`
  - 종료 방법
    - `deactivate`
- jupyter notebook 사용방법
  - 설치 방법
    - 위의 가상환경을 키고 `pip install jupyter` 입력
  - 초기 설정
    - `jupyter notbook --generate-config`
    - `mkdir ~/.jupyter`
    - `cd ~/.jupyter`
    - `vim jupyter_notebook_config.py`
    - 내부에 내용이 있다면 `dd`, `shift+v+g`, `d` 를 순서대로 입력한다
    - `i`를 눌러 Insert Mode를 키고 다음과 같은 코드를 입력한다.
``` 
c=get_config()
c.NotebookApp.allow_origin='*'
c.NotebookApp.notebook_dir='/src/gs학번'
c.NotebookApp.ip='115.23.235.150'
c.NotebookApp.port=학번 
c.NotebookApp.open_browser=False
```
  - 키는 방법
    - `jupyter notebook --config ~/.jupyter/jupyter_notebok.config.py`
      - 밑에 뜨는 115.23.235.150~~~ 주소를 복사하여 사용하면 된다.
      - 이 방법은 cmd or putty를 끄면 jupyter도 닫힌다.
    - `nohup jupyter notebook --config ~/.jupyter/jupyter_notebok.config.py >jupyter.out`
      - 위 명령어를 치고 창을 꺼준다음 재접속한다. (창을 닫아라)
      - `vim ./~jupyter/jupyter.out`를 입력하면 주소가 보인다.
      - 이 방법은 백그라운드에서 실행되어 창을 꺼도 실행된다.
      - 서버 재시작 시 꺼지기 때문에 꺼지면 다시 위의 코드를 쳐주면 된다.
- python 사용 방법
  - jupyter 없이 python을 이용하고 싶다면 우선 테스트를 한 후 돌리는 것을 추천한다. (우리에게는 pycharm이 있다.)
  - vim으로 편집하면 개고생한다..
  - python main.py (python 파일명.py)로 실행하면 된다. 
    - 이때 디렉토리는 이동한 상태에서 해야된다 (cd 를 이용하자)
  - `nohup python main.py` > 출력 파일
    - ex) `nohup python main.py > test.out`
    - 백그라운드에서 실행 -> 컴퓨터를 꺼도 실행된다.
- GPU 이용 방법
  - 코드에 추가하기
    - jupyter 사람들에게 추천
    - 아래 코드를 추가하기
```
import os 
os.environ["CUDA_DEVICE_ORDER"]="PCI_BUS_ID" 
os.environ["CUDA_VISIBLE_DEVICES"]="사용할 GPU 숫자(0~9)"
```
  - python 실행할때 추가
    - `앞에다가 CUDA_VISIBLE_DEVICES=GPU 숫자`
    - nohup도 마찬가지다.
## C언어 사용 방법
- 부기장이 채울 예정
## java 사용 방법
- 부기장이 채울 예정
## DB 사용 방법
- 추후에 설명 예쩡
