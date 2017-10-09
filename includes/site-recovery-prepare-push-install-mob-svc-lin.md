### <a name="prepare-for-a-push-installation-on-a-linux-server"></a>Linux 서버에서 푸시 설치 준비

1. Hello Linux 컴퓨터와 hello 프로세스 서버 간의 네트워크 연결 인지 확인 합니다.
2. 해당 hello 프로세스 서버 tooaccess hello 컴퓨터를 사용할 수 있는 계정을 만듭니다. hello 계정 이어야 합니다는 **루트** hello 소스 Linux 서버에 있는 사용자입니다. (업데이트 및 hello 강제 설치에 대해서만이 계정을 사용 합니다.)
3. Hello 소스 Linux 서버에 모든 네트워크 어댑터와 관련 된 hello 로컬 호스트 이름 tooIP 주소 매핑하는 항목에 해당 hello /etc/hosts 파일을 확인 합니다.
4. Hello 최신 openssh, openssh-서버 및 openssl 패키지 tooreplicate hello 컴퓨터에 설치 합니다.
5. SSH(보안 셸)가 22 포트에서 사용되고 실행 중인지 확인합니다.
6. Hello sshd_config 파일에서 SFTP 하위 시스템 및 암호 인증을 사용 합니다.
  1.  **루트**로 로그인합니다.
  2.  hello 파일/등/ssh/sshd_config 파일으로 시작 하는 hello 줄 찾기 **PasswordAuthentication**합니다.
  3.  Hello 줄 주석을 제거 하 고 hello 값도 변경**예**합니다.
  4.  로 시작 하는 찾기 hello 줄 **하위 시스템** hello 줄에서 주석 처리 제거 합니다.

     ![Linux](./media/site-recovery-prepare-push-install-mob-svc-lin/mobility2.png)
  5. Hello를 다시 시작 **sshd** 서비스입니다.

7. Hello CSPSConfigtool에서 만든 계정을 추가 합니다.
    1.  Tooyour 구성 서버에 로그인 합니다.
    2.  **cspsconfigtool.exe**를 엽니다. (이 hello %ProgramData%\home\svsystems\bin 폴더와 hello 바탕 화면에서 바로 가기를 사용할 수 있습니다.)
    3.  Hello에 **계정 관리** 탭을 클릭 **계정 추가**합니다.
    4.  사용자가 만든 hello 계정을 추가 합니다. 
    5.  컴퓨터에 대 한 복제를 사용 하도록 설정 하면 사용 하 여 hello 자격 증명을 입력 합니다.
