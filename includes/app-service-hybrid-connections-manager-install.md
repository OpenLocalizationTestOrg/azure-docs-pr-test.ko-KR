
1. Hello에 **하이브리드 연결** 블레이드에서 만들어지면 방금 hello 하이브리드 연결을 클릭 한 다음 클릭 **수신기 설치**합니다.
   
    ![수신기 설정 클릭](./media/app-service-hybrid-connections-manager-install/D04ClickListenerSetup.png)
2. hello **하이브리드 연결 속성** 블레이드를 엽니다. 아래 **온-프레미스 하이브리드 연결 관리자**, 선택 **다운로드 하 고 수동으로 구성**다운로드 하는 hello HybridConnectionManager.msi 패키지를 저장 하 고 hello 게이트웨이 연결 문자열을 복사 합니다.
   
    ![Tooinstall 여기를 클릭합니다](./media/app-service-hybrid-connections-manager-install/D05ClickToInstallHCM.png)
3. 관리자 명령 프롬프트에서 다음 명령 toostart hello 설치 관리자는 hello를 입력 합니다.
   
        start HybridConnectionManager.msi
4. Hello 설치 관리자 실행을 클릭 **나중**, 다음 toohello %ProgramFiles%\Microsoft\HybridConnectionManager 폴더를 탐색, HCMConfigWizard.exe를 실행 하 고 클릭 **예** hello에 **사용자 계정 제어** 대화 상자.
5. 앞에서 복사한 hello 하이브리드 연결 문자열을 붙여 넣고 클릭 **확인**합니다. 
   
    ![설치](./media/app-service-hybrid-connections-manager-install/D08aHCMInstallManual.png)
6. Hello 설치 완료 되 면 클릭 **닫기**합니다.
   
    ![닫기 클릭](./media/app-service-hybrid-connections-manager-install/D09HCMInstallComplete.png)
   
    Hello에 **하이브리드 연결** 블레이드, hello **상태** 열 이제 표시 **연결 됨**합니다. 
   
    ![연결됨 상태](./media/app-service-hybrid-connections-manager-install/D10HCStatusConnected.png)

