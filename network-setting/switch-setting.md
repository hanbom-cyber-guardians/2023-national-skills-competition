# Switch setting guide

## 초기화

비밀번호가 설정되어 있는 경우 초기화 해서 설정을 진행할 것
[cisco switch 공장초기화 가이드](https://jsson.tistory.com/74)

1.  serial cable로 switch와 연결
2.  스위치 전면부에 있는 mode 버튼을 클릭하며 파워케이블을 연결하여 부팅한다.
3.  mode버튼을 최소 5초간 누르고 있어야 한다
4.  putty를 이용해 serial 접속을 한다
5.  "dir flash:" 명령어로 config 파일들을 탐색한다.
6.  "del flash:config.text" 명령어로 기본설정을 제거한다.
7.  "reset" 명령어를 입력하여 재부팅한다.

## 설정

    en
    conf t
    interface g0/1
    no shut

사용하는 포트 마다 no shut 설정을 해줄 것
