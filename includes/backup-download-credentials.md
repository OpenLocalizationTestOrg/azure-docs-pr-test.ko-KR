## <a name="using-vault-credentials-tooauthenticate-with-hello-azure-backup-service"></a>자격 증명 모음 자격 증명 tooauthenticate hello Azure 백업 서비스 사용
hello 온-프레미스 서버 (Windows 클라이언트 또는 Windows Server 또는 Data Protection Manager 서버) toobe tooAzure 데이터를 백업할 수 전에 백업 자격 증명으로 인증 해야 합니다. "자격 증명 모음 자격 증명"을 사용 하 여 hello 인증이 수행 됩니다. 자격 증명 모음 자격 증명의 hello 개념은 Azure PowerShell에서 사용 되는 "게시 설정" 파일의 비슷한 toohello 개념입니다.

### <a name="what-is-hello-vault-credential-file"></a>Hello 자격 증명 모음 자격 증명 파일 이란 무엇 인가요?
hello 자격 증명 모음 자격 증명 파일은 각 백업 자격 증명 모음에 대 한 hello 포털에서 생성 한 인증서입니다. hello 포털 hello 공개 키 toohello 서비스 ACS (액세스 제어)를 업로드합니다. hello hello 인증서의 개인 키를 사용할 수 있는 toohello 사용자 hello 시스템 등록 워크플로에 대 한 입력으로 제공 된 hello 워크플로의 일부분으로 이루어집니다. Hello hello Azure 백업 서비스에서에서 컴퓨터 toosend 백업 데이터 tooan 식별 된 자격 증명 모음을 인증 합니다.

자격 증명 모음 hello hello 등록 워크플로 중에 사용 됩니다. 자격 증명 모음 파일 손상 되지 않도록 hello hello 사용자의 책임 tooensure 이며 Rogue 사용자의 hello 손에 올 경우 hello 자격 증명 모음 자격 증명 파일 일 수 있습니다 tooregister 사용 되는 다른 컴퓨터에 대해 동일한 자격 증명 모음 hello 합니다. 그러나 hello 백업 데이터 toohello 고객에 속한 암호로 암호화 되어, 기존 백업 데이터를 손상 될 수 없습니다. toomitigate이이 내용이 자격 증명 모음 자격 증명이 설정 tooexpire 48hrs에 있습니다. 여러 번 – 백업 자격 증명 모음의 자격 증명 모음 hello를 다운로드할 수 있습니다 나타나지만 hello 등록 워크플로 중만 hello 최신 자격 증명 모음 자격 증명 파일을 적용할 수 있습니다.

### <a name="download-hello-vault-credential-file"></a>Hello 자격 증명 모음 자격 증명 파일을 다운로드
hello Azure 포털에서에서 보안 채널을 통해 hello 자격 증명 모음 자격 증명 파일이 다운로드 됩니다. hello Azure 백업 서비스 hello hello 인증서의 개인 키를 인식 하지 않으며 hello 개인 키 hello 포털 또는 hello 서비스에 유지 되지 않습니다. 다음 단계 toodownload hello 자격 증명 모음 자격 증명 파일 tooa 로컬 컴퓨터 hello를 사용 합니다.

1. Toohello 로그인 [관리 포털](https://manage.windowsazure.com/)
2. 클릭 **복구 서비스** hello 왼쪽된 탐색 창 및 선택 hello 백업 자격 증명 모음 만든입니다. Hello 클라우드 아이콘 tooget toohello hello 백업 자격 증명 모음의 빠른 시작 뷰를 클릭 합니다.
   
   ![빠른 보기](./media/backup-download-credentials/quickview.png)
3. Hello 빠른 시작 페이지에서 클릭 **자격 증명 모음 다운로드**합니다. hello 포털 다운로드 하는 데 사용할 수 있는 hello 자격 증명 모음 자격 증명 파일을 생성 합니다.
   
   ![다운로드](./media/backup-download-credentials/downloadvc.png)
4. hello 포털 hello 자격 증명 모음 이름 및 hello의 조합을 현재 날짜를 사용 하 여 자격 증명 모음 자격 증명을 생성 합니다. 클릭 **저장** toodownload hello 자격 증명 모음 자격 증명 toohello 로컬 계정의 다운로드 폴더 또는 hello 자격 증명 모음 자격 증명에 대 한 위치 메뉴 toospecify 저장 hello에서 다른 이름으로 저장을 선택 합니다.

### <a name="note"></a>참고
* Hello 자격 증명 모음 자격 증명은 컴퓨터에서 액세스할 수 있는 위치에 저장 되어 있음을 확인 합니다. 파일 공유/SMB에 저장 되는지를 hello 액세스 권한을 확인 합니다.
* hello 자격 증명 모음 자격 증명 파일이 hello 등록 워크플로 중에 사용 됩니다.
* hello 자격 증명 모음 자격 증명 파일 48hrs 후에 만료 되며 hello 포털에서 다운로드할 수 있습니다.
* Azure 백업 toohello 참조 [FAQ](../articles/backup/backup-azure-backup-faq.md) hello 워크플로에 대 한 모든 질문에 대 한 합니다.

