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
  - password : 자기 비밀번호 (계속 빈칸으로 뜨는 것이 정상)
- cmd 
  - 신서버 : ssh gs20000@115.23.235.150
  - 구서버 : ssh -p 443 gs20000@115.23.235.135
  - 비번은 동일
- filezilla
  - filezilla client 설치
    - [다운로드 링크](https://filezilla-project.org/download.php?platform=win64)
  - 왼쪽 위 파일 -> 사이트 관리자
  - 
    
