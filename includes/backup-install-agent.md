## <a name="download-install-and-register-hello-azure-backup-agent"></a>다운로드, 설치 및 hello Azure 백업 에이전트를 등록 합니다.
Hello Azure 백업 자격 증명 모음을 만든 후 각 백업 데이터와 응용 프로그램 수 있는 Windows 컴퓨터 (Windows Server, Windows 클라이언트, System Center Data Protection Manager 서버 또는 Azure 백업 서버 컴퓨터)에 에이전트를 설치 tooAzure 합니다.

1. Toohello 로그인 [관리 포털](https://manage.windowsazure.com/)
2. 클릭 **복구 서비스**을 선택한 후 hello 백업 자격 증명 모음의 서버와 tooregister 되도록 합니다. 해당 백업 자격 증명 모음에 대 한 hello 빠른 시작 페이지가 표시 됩니다.
   
    ![빠른 시작](./media/backup-install-agent/quickstart.png)
3. Hello 빠른 시작 페이지에서 클릭 hello **For Windows Server 또는 System Center Data Protection Manager 또는 Windows 클라이언트** 옵션에서 **에이전트 다운로드**합니다. 클릭 **저장** toocopy 것 toohello 로컬 컴퓨터입니다.
   
    ![에이전트 저장](./media/backup-install-agent/agent.png)
4. Hello 에이전트가 설치 되 면 두 번 클릭 MARSAgentInstaller.exe toolaunch hello hello Azure 백업 에이전트를 설치 합니다. Hello 설치 폴더 및 hello 에이전트에 필요한 스크래치 폴더를 선택 합니다. 지정 된 hello 캐시 위치는 hello 백업 데이터의 5% 이상 사용 가능한 공간에 있어야 합니다.
5. 프록시 서버 tooconnect toohello를 사용 하는 경우 인터넷 hello에 **프록시 구성을** 화면에서 hello 프록시 서버 정보를 입력 합니다. 인증 된 프록시를 사용 하면이 화면에 hello 사용자 이름 및 암호 세부 정보를 입력 합니다.
6. hello Azure 백업 에이전트 설치.NET Framework 4.5 및 Windows PowerShell (것 사용할 수 없는 경우 이미) toocomplete hello 설치 합니다.
7. Hello 에이전트가 설치 되 면 클릭 hello **tooRegistration 계속** hello 워크플로와 단추 toocontinue 합니다.
   
   ![등록](./media/backup-install-agent/register.png)
8. Hello 자격 증명 모음 자격 증명 화면에서 이전에 다운로드 된 tooand 선택 hello 자격 증명 모음 자격 증명 파일을 찾습니다.
   
    ![자격 증명 모음 자격 증명](./media/backup-install-agent/vc.png)
   
    hello 자격 증명 모음 자격 증명 파일이 48에만 유효 합니다. (hello 포털에서 다운로드 된) 후에 시간입니다. 이 화면 (예: "자격 증명 모음 자격 증명 파일이 만료 제공")에 오류가 발생 하는 경우 Azure 포털 로그인 toohello hello 자격 증명 모음 다운로드 파일을 다시입니다.
   
    Hello 설치 응용 프로그램에서 액세스할 수 있는 위치에 해당 hello 자격 증명 모음 자격 증명 파일을 사용할 수 있는지 확인 합니다. 발생 하는 경우 액세스 관련된 오류 복사 hello에 대 한 자격 증명 모음 자격 증명 파일을이 컴퓨터의 임시 위치 tooa hello 작업을 다시 시도 합니다.
   
    오류가 발생 하면 잘못 된 자격 증명 모음 자격 증명 (예: "잘못 된 자격 증명 모음 자격 증명 제공") hello 파일 손상 되었거나 않습니다 연관 되지 않은 한 hello 최신 자격 hello 복구 서비스입니다. Hello hello 포털에서 새 자격 증명 모음 자격 증명 파일을 다운로드 한 후 작업을 다시 시도 하십시오. Hello hello 사용자가 클릭 하는 경우이 오류는 일반적으로 발생 **자격 증명 모음 다운로드** hello 연속적으로 Azure 포털에서에서 옵션입니다. 이 경우에 hello 두 번째 자격 증명 모음 자격 증명 파일은 유효 합니다.
9. Hello에 **암호화 설정** 화면에서 암호를 생성 하거나 (최소 16 자) 암호를 제공할 수 있습니다. 안전한 위치에 toosave hello 암호를 기억 합니다.
   
    ![암호화](./media/backup-install-agent/encryption.png)
   
   > [!WARNING]
   > 암호를 분실 하거나 잊어버린; 경우 hello Microsoft는 hello 백업 데이터를 복구할 수 없습니다. hello 최종 사용자 hello 암호화의 암호를 소유 하 고 hello 최종 사용자가 사용 되는 hello 암호에 대 한 가시성 갖고 있지 않습니다. 복구 작업 중 필요한는 hello 파일을 안전한 위치에 저장 하십시오.
   > 
   > 
10. Hello를 클릭 한 후 **마침** 단추, hello 컴퓨터 등록 하는 성공적으로 toohello 자격 증명 모음 사용자가 지금 준비 toostart tooMicrosoft Azure 백업 합니다.
11. Microsoft Azure 백업 독립 실행형을 사용 하는 경우에 hello를 클릭 하 여 hello 등록 워크플로 중에 지정 하는 hello 설정을 수정할 수 있습니다 **속성 변경** hello Azure 백업 mmc 스냅인에서 옵션입니다.
    
    ![속성 변경](./media/backup-install-agent/change.png)
    
    또는 Data Protection Manager를 사용할 때는 hello를 클릭 하 여 hello 등록 워크플로 중에 지정한 hello 설정을 수정할 수 **구성** 옵션을 선택 하 여 **온라인** hello에서 **관리** 탭 합니다.
    
    ![Azure 백업 구성](./media/backup-install-agent/configure.png)

