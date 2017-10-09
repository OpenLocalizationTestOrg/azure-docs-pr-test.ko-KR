UnifiedSetup.exe [/ ServerMode < CS/P >] [/ InstallDrive <DriveLetter>] [/ MySQLCredsFilePath <MySQL credentials file path>] [/ VaultCredsFilePath <Vault credentials file path>] [/ EnvType < VMWare/NonVMWare >] [/ PSIP < 데이터 전송에 사용 되는 IP 주소 toobe] [/CSIP <IP address of CS toobe registered with>] [/ PassphraseFilePath <Passphrase file path>]

매개 변수

* /ServerMode: 필수. 두 hello 구성 및 프로세스 서버를 설치 하는지 여부, 또는 hello 프로세스 서버에만 지정 합니다. 입력 값: CS, PS.
* InstallLocation: 필수. 구성 요소가 설치 되어 있는 hello hello 폴더입니다.
* /MySQLCredsFilePath. 필수. hello 파일 경로 hello MySQL 서버 자격 증명 저장 됩니다. hello 파일이 형식 이어야 합니다.
* [MySQLCredentials]
* MySQLRootPassword = "<Password>"
* MySQLUserPassword = "<Password>"
* /VaultCredsFilePath. 필수. hello 자격 증명 모음 자격 증명 파일의 hello 위치
* /EnvType. 필수. hello 유형의 설치 합니다. 값: VMware, NonVMware
* /PSIP 및 /CSIP. 필수. hello hello 프로세스 서버와 구성 서버 IP 주소입니다.
* /PassphraseFilePath. 필수. hello 암호 파일의 hello 위치입니다.
* /ByPassProxy. 선택 사항입니다. 프록시 없이 tooAzure를 연결 하는 hello 구성 서버를 지정 합니다.
* /ProxySettingsFilePath. 선택 사항입니다. 프록시 설정 (hello 기본 프록시 인증 또는 사용자 지정 프록시 필요). hello 파일이 형식 이어야 합니다.
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address>"
* ProxyPort = "<Port>"
* ProxyUserName="<User Name>"
* ProxyPassword="<Password>"
* DataTransferSecurePort. 선택 사항입니다. 복제 데이터에 대 한 hello 포트 번호입니다.
* SkipSpaceCheck. 선택 사항입니다. 캐시에 대한 공간 확인을 건너뜁니다.
* AcceptThirdpartyEULA. 필수. Hello 제 3 자 EULA를 허용합니다.
* ShowThirdpartyEULA. 필수. 타사 EULA를 표시합니다. 입력으로 제공되는 경우 다른 모든 매개 변수가 무시됩니다.
