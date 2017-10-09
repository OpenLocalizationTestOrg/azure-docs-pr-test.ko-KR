hello 배포 스크립트는 로컬 컴퓨터 호환 가상 환경 이미 있음을 감지 hello 가상 환경 만드는 Azure에서 건너뜁니다.  이렇게 하면 배포 속도를 상당히 높일 수 있습니다.  이미 설치된 패키지를 pip가 건너뜁니다.

특정 상황에서는 수도 있습니다 tooforce delete 가상 환경에 해당 합니다.  합니다 toodo이 저장소의 일부로 tooinclude 가상 환경을 결정 한 경우.  또한이 방법이 필요할 toodo tooget 해야 할 경우 특정 패키지를 제거 또는 변경 toorequirements.txt를 테스트 합니다.

Azure에서 가상 환경에 기존 몇 가지 옵션 toomanage hello 가지가 있습니다.

### <a name="option-1-use-ftp"></a>옵션 1: FTP 사용
FTP 클라이언트와 toohello 서버를 연결 하 고 수 toodelete hello env 폴더 수 있습니다.  일부 FTP 클라이언트 (예: 웹 브라우저) 읽기 전용 및 허용 하지 toodelete 폴더 toomake 있는지 toouse 해당 기능을 사용 하 여 FTP 클라이언트는 해야 하므로 참고 합니다.  hello FTP 호스트 이름 및 사용자 hello에 웹 앱의 블레이드에 표시 된 [Azure 포털](https://portal.azure.com)합니다.

### <a name="option-2-toggle-runtime"></a>옵션 2: 런타임 설정/해제
Python의 원하는 버전 hello 일치 하지 않는 hello 배포 스크립트가 hello env 폴더를 삭제할 것 hello 팩트를 활용 하는 대신 다음과 같습니다.  효과적으로 hello 기존 환경을 삭제 되 고 새로 만드십시오.

1. Python의 스위치 tooa 다른 버전 (runtime.txt 또는 hello를 통해 **응용 프로그램 설정** 블레이드 hello Azure 포털에서에서)
2. 일부 변경 사항에 대해 git push 처리(있는 경우 모든 pip 설치 오류 무시)
3. Python의 뒤로 tooinitial 버전 전환
4. 일부 변경 사항에 대해 다시 git push 처리

### <a name="option-3-customize-deployment-script"></a>옵션 3: 배포 스크립트 사용자 지정
Hello 배포 스크립트를 사용자 지정한 경우에 hello을 변경할 수 있습니다 코딩할 deploy.cmd tooforce에 toodelete hello env 폴더입니다.

