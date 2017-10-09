## <a name="prepare-your-intel-nuc"></a>Intel NUC 준비

toocomplete hello 하드웨어 설치 해야합니다.

- Hello 키트에 포함 된 Intel NUC toohello 전원 공급 장치를 연결 합니다.
- 이더넷 케이블을 사용 하 여 Intel NUC tooyour 네트워크를 연결 합니다.

이제 Intel NUC 게이트웨이 장치 hello 하드웨어 설치를 완료 했습니다.

### <a name="sign-in-and-access-hello-terminal"></a>로그인 및 액세스 hello 터미널

환경을 사용 하는 두 가지 옵션 tooaccess 터미널 Intel NUC에:

- 키보드 연결 된 tooyour Intel NUC를 모니터링 하는 경우에 hello 셸 직접 액세스할 수 있습니다. hello 기본 자격 증명이 username **루트** 및 암호 **루트**합니다.

- Hello 셸 데스크톱 컴퓨터의 SSH를 사용 하 여 Intel NUC에 액세스 합니다.

#### <a name="sign-in-with-ssh"></a>SSH를 사용하여 로그인

SSH 사용 하 여 toosign, Intel NUC의 hello IP 주소가 필요 합니다. 키보드 연결 된 tooyour Intel NUC 모니터링을 사용 하 여 hello `ifconfig` toofind hello IP 주소가 명령입니다. 또는 tooyour 라우터 toolist hello 주소의 네트워크 장치를 연결 합니다.

사용자 이름 **root** 및 암호 **root**로 로그인합니다.

#### <a name="optional-share-a-folder-on-your-intel-nuc"></a>선택 사항: Intel NUC에서 폴더 공유

필요에 따라 데스크톱 환경에 Intel NUC tooshare 폴더를 할 수 있습니다. 공유 폴더를 사용 하면 있습니다 toouse 데스크톱 원하는 텍스트 편집기 (예: [Visual Studio Code](https://code.visualstudio.com/) 또는 [Sublime 텍스트](http://www.sublimetext.com/)) tooedit 파일을 사용 하는 대신 Intel NUC 프로그램 `nano` 또는 `vi`.

Intel NUC hello에 Samba 서버를 구성 하는 Windows와 함께 폴더 tooshare 합니다. 또는 hello Intel NUC 데스크톱 컴퓨터에서 SFTP 클라이언트를에 hello SFTP 서버를 사용 합니다.
