## AD DS 설치
```shell
1.서버 관리자(Server Manager) 열기:
-  "역할 및 기능 추가"를 클릭한 후 "다음" 클릭
-  "역할 기반 또는 기능 기반 설치" 선택 후 "다음" 클릭
-  서버 선택 페이지에서 현재 서버 선택 후 "다음" 클릭

2.Active Directory 도메인 서비스 역할 추가
-  역할 선택 페이지에서 "Active Directory 도메인 서비스"를 선택하고 "다음" 클릭
-  필요한 기능 추가 확인 창에서 "기능 추가" 클릭
-  추가 기능 선택 페이지를 모두 넘기고 우측 하단 "설치" 클릭
```

##  도메인 컨트롤러 구성
```shell
1. Active Directory 도메인 서비스 설정:
- 설치 후 "Active Directory 도메인 서비스" 알림 플래그 클릭 -> "Promote this server to a domain controller" 클릭
2. 배포 구성:
- "Add a new forest" 선택 후 이름을 'nicekorea.com'으로 입력 후 "다음" 클릭
3. 도메인 컨트롤러 옵션 설정:
- 기능 수준을 Windows Server2016 이상으로 설정, DNS 서버 및 글로벌 카탈로그(GC)역할 선택
- Directory Services Restore Mode(DSRM) 암호를 "Cyber2023$$"로 설정 후 "다음" 클릭
4. DNS 옵션 설정:
- DNS 위임 설정 경고를 무시하고 "다음" 클릭
- NetBIOS 이름을 'NICEKOREA'로 설정하고 "다음 클릭"(가만히 기다리면 자동으로 입력됨)
5. 경로 설정:
- 폴더 경로를 모두 기본값으로 두고 "다음" 클릭
6. 검토 및 설치: 
- 구성 요약 검토 후 "다음" 클릭, 설치
- 이후 자동 재부팅됨
```

## DNS 서버 설정

```shell
서버 관리자 탭에서 "도구(Tools)" 메뉴 -> "DNS" 선택
1. 정방향 조회 영역 추가:
- DNS 관리 콘솔에서 서버 이름을 확장하고, "정방향 조회 영역"을 확장하여 'nicekorea.com' 확인
- 만약 없다면 "정방향 조회 영역"을 우클릭하여 "New zone"을 선택
- Wizard 창에서 영역 이름 설정을 제외하고 모두 "다음" 클릭, 영역 이름은 'nicekorea.com' 을 입력
- 동적 업데이트 허용 옵션 설정 후 "다음", "마침"
2. 역방향 조회 영역 추가:
- "역방향 조회 영역"을 마우스 우클릭하여 "New Zone" 선택
- 기본 영역으로 설정 후 "다음"을 눌러 IPv4 역방향 조회 영역 선택 후 "다음" 클릭
- 네트워크 ID를 '172.20.200'으로 입력 후 "다음" 클릭
- 동적 업데이트 허용 옵션 설정 후 "다음", "마침"
3. host 레코드 추가
- 정방향 조회 영역에서 'nicekorea.com' 우클릭하여 "new host(A or AAAA)" 클릭
- 이름 필드에 [host] 입력 후 IP 주소를 입력
- PTR 생성 클릭 후 add host 클릭
```


## 사용자 추가
```shell
1. 조직 구성
- 서버 관리자 - 도구 - Active Directory User and Computers 클릭
- 도메인 'nicekorea.com'을 확장하과, 상위 노드를 오른쪽 클릭한 후 "새로 만들기(New)" -> "조직 구성 단위(Organizational Unit)" 선택
- 'Sales', 'Managers', 'Webs'로 각각 입력하여 세 개의 OU를 생성
2. 그룹 추가
- 각각의 OU 우클릭 - New - Group 선택
- Sales OU: Sales
- Managers OU: Managers
- Webs OU: Webs
3. 사용자 추가
- 각각의 OU를 우클릭 - New  - User 선택
- Sales OU: group)Sales user)kim, park
- Managers OU: group)Managers user) mgr01, mgr02
- Webs OU: group)Webs user)webadmin
이후 그룹의 members에서 각 user 추가 
- 암호를 설정하고, "Change password at next logon"옵션 끄기 다음 마침
이후엔 만든 그룹, 사용자 properties 들어가서 서로 연동
``` 