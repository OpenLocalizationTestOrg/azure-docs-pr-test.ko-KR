### <a name="prepare-for-a-push-installation-on-a-windows-computer"></a>Windows 컴퓨터에서 푸시 설치 준비

1. Hello Windows 컴퓨터와 hello 프로세스 서버 간의 네트워크 연결 인지 확인 합니다.
2. 해당 hello 프로세스 서버 tooaccess hello 컴퓨터를 사용할 수 있는 계정을 만듭니다. hello 계정 (로컬 또는 도메인) 관리자 권한이 있어야 합니다. (에이전트 업데이트 및 hello 강제 설치에 대해서만이 계정을 사용 합니다.)

   > [!NOTE]
   > 도메인 계정을 사용 하지 않는 hello 로컬 컴퓨터에서 원격 사용자 액세스 제어를 사용 하지 않도록 설정 합니다. hello 찾아 레지스트리 키 아래에서 원격 사용자 액세스 제어 toodisable 추가 새 DWORD: **LocalAccountTokenFilterPolicy**합니다. Hello 값을 너무 설정**1**합니다. toodo 명령에서이 프롬프트를 hello 다음 명령을 실행 합니다.  
   `REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`
   >
   >
2. 원하는 tooprotect, hello 컴퓨터에서 Windows 방화벽에서 **앱 또는 기능 방화벽을 통해 허용**합니다. **파일 및 프린터 공유**와 **WMI(Windows Management Instrumentation)**를 사용하도록 설정합니다. Tooa 도메인에 속해 있는 컴퓨터에 대 한 그룹 정책 개체 (GPO)를 사용 하 여 hello 방화벽 설정을 구성할 수 있습니다.

   ![방화벽 설정](./media/site-recovery-prepare-push-install-mob-svc-win/mobility1.png)

3. Hello CSPSConfigtool에서 만든 계정을 추가 합니다.
    1.  Tooyour 구성 서버에 로그인 합니다.
    2.  **cspsconfigtool.exe**를 엽니다. (이 hello %ProgramData%\home\svsystems\bin 폴더와 hello 바탕 화면에서 바로 가기를 사용할 수 있습니다.)
    3.  Hello에 **계정 관리** 탭에서 **계정 추가**합니다.
    4.  사용자가 만든 hello 계정을 추가 합니다.
    5.  컴퓨터에 대 한 복제를 사용 하도록 설정 하면 사용 하 여 hello 자격 증명을 입력 합니다.
