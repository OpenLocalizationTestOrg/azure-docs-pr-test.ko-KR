<!--author=alkohli last changed: 12/01/15-->


#### <a name="tooconfigure-and-register-hello-device"></a>tooconfigure 및 레지스터 hello 장치
1. StorSimple 장치 직렬 콘솔에 hello Windows PowerShell 인터페이스에 액세스 합니다. 참조 [PuTTY를 사용 하 여 장치 직렬 콘솔 tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console) 지침에 대 한 합니다. **있는지 toofollow hello 절차를 정확 하 게 것인지 수 tooaccess hello 콘솔 됩니다.**
2. 가 열리면 hello 세션에서 입력 한 시간 tooget 명령 프롬프트를 키를 누릅니다. 
3. 싶다는 의사를 tooset 장치에 대 한 증명된 toochoose hello 언어 됩니다. Hello 언어를 지정 하 고 enter 키를 누릅니다. 
   
    ![StorSimple 구성 및 등록 장치 1](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice1-include.png)
4. 제공 되는 hello 직렬 콘솔 메뉴에서 옵션 1 toolog에 대 한 모든 권한을 선택 합니다. 
   
    ![StorSimple 등록 장치 2](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice2-include.png)
   
     장치에 대 한 단계 5-12 tooconfigure hello 필요한 최소 네트워크 설정을 완료 합니다. **이러한 구성 단계 toobe hello hello 장치의 활성 컨트롤러에서 수행 해야 합니다.** hello 직렬 콘솔 메뉴 hello 배너 메시지에 hello 컨트롤러 상태를 나타냅니다. 연결 되어 있지 않으면 toohello 활성 컨트롤러를 분리 하 고 toohello 활성 컨트롤러를 연결 합니다.
5. Hello 명령 프롬프트에서 암호를 입력 합니다. hello 기본 장치 암호는 **Password1**합니다.
6. Hello 다음 명령을 입력 합니다.
   
     `Invoke-HcsSetupWizard` 
7. 설치 마법사는 hello 장치에 대 한 hello 네트워크 설정을 구성 하는 toohelp 표시 됩니다. Hello hello 다음 정보를 제공 합니다. 
   
   * Hello DATA 0 네트워크 인터페이스에 대 한 IP 주소
   * 서브넷 마스크
   * 게이트웨이
   * 주 DNS 서버의 IP 주소
   * 주 NTP 서버의 IP 주소
     
     > [!NOTE]
     > Hello 서브넷 마스크 및 hello DNS 설정 toobe 적용에 대 일 분 동안 toowait이 있을 수 있습니다. "hello 장치가 준비 되지 않았습니다."가 발생 하는 경우 활성 컨트롤러의 hello DATA 0 네트워크 인터페이스에서 되는 검사 hello 실제 네트워크 연결 오류 메시지입니다.
     > 
     > 
8. (선택 사항) 웹 프록시 서버를 구성합니다. 웹 프록시 구성은 선택 사항이지만 **웹 프록시를 사용하면 여기서만 구성할 수 있습니다**. 자세한 내용은 이동 너무[장치에 대 한 웹 프록시 구성](../articles/storsimple/storsimple-configure-web-proxy.md)합니다. 이 단계는 문제를 실행 하면 참조에 대 한 지침 tootroubleshooting [웹 프록시 구성 하는 동안 오류가 발생](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-during-the-optional-web-proxy-settings)합니다.

     > [!NOTE]
     > 모든 시간 tooexit hello 설치 마법사에서 Ctrl + C를 눌러 수 있습니다. 이 명령을 실행하기 전에 적용된 모든 설정은 유지됩니다.

1. 보안상의 이유로 hello 첫 번째 세션 후 hello 장치 관리자 암호가 만료 되어 toochange 해야 후속 세션에 대 한 것입니다. 메시지가 표시되면 장치 관리자 암호를 제공합니다. 유효한 장치 관리자 암호는 8자에서 15자 사이여야 합니다. hello 암호 소문자, 대문자, 숫자 및 특수 문자 조합을 포함 해야 합니다.
2. hello StorSimple 스냅숏 관리자 암호도 여기서 설정 됩니다. StorSimple 스냅숏 관리자를 실행하는 Windows 호스트로 장치를 인증하는 경우 이 암호를 사용합니다. 메시지가 표시 되 면 14 too15 문자 암호를 제공 합니다. hello 암호 조합이 포함 되어야 hello 다음의 3: 소문자, 대문자, 숫자 및 특수 문자. 
   
   ![StorSimple 등록 장치 4](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice4-include.png)
   
   Hello StorSimple 관리자 서비스 인터페이스에서 hello StorSimple 스냅숏 관리자 암호를 재설정할 수 있습니다. 자세한 단계에 대 한 이동 너무[hello StorSimple Manager 서비스를 사용 하 여 hello StorSimple 암호 변경](../articles/storsimple/storsimple-change-passwords.md)합니다.
   
   tootroubleshoot이 단계에서는 모든 문제에 대 한 tootroubleshooting 지침 참조 [오류 관련 toopasswords](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-related-to-device-administrator-and-storsimple-snapshot-manager-passwords)합니다.
3. hello hello 설치 마법사의 마지막 단계는 hello StorSimple Manager 서비스와 장치를 등록합니다. 이 경우 2 단계에서 얻은 hello 서비스 등록 키를 해야 합니다. Hello 등록 키를 제공한 후 toowait hello 장치를 등록 하기 전에 2-3 분 동안 할 수 있습니다.
   
   tootroubleshoot 모든 가능한 장치 등록 오류 참조 너무[장치 등록 도중 발생 한 오류](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-during-device-registration)합니다. 상세한 문제 해결을 참조할 수도 있습니다 너무[단계별 문제 해결 예제](../articles/storsimple/storsimple-troubleshoot-deployment.md#step-by-step-storsimple-troubleshooting-example)합니다.
4. Hello 장치를 등록 한 후에 서비스 데이터 암호화 키가 표시 됩니다. 이 키를 복사하고 안전한 위치에 저장합니다.
   
   > [!WARNING]
   > 이 키는 hello 서비스 등록 키 tooregister 추가 장치를 StorSimple Manager 서비스 hello 함께 해야 합니다. 너무 참조[StorSimple 보안](../articles/storsimple/storsimple-security.md) 이 키에 대 한 자세한 내용은 합니다.
   > 
   > 
   
    ![StorSimple 등록 장치 6](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice6-include.png)
   
    hello 직렬 콘솔 창에서 toocopy hello 텍스트 hello 텍스트를 선택 하면 됩니다. Toopaste 수 있어야 다음 hello 클립보드 또는 텍스트 편집기에서. Ctrl 키를 사용 하지 않는 + C toocopy hello 서비스 데이터 암호화 키입니다. Ctrl + C를 사용 하면 tooexit hello 설치 마법사를 발생 합니다. 결과적으로, hello 장치 관리자 암호와 hello StorSimple 스냅숏 관리자 암호가 변경 되지 않습니다 및 hello 장치 toohello 기본 암호 되돌아갑니다.
5. Hello 직렬 콘솔을 종료 합니다.
6. Azure 클래식 포털 toohello 돌아간 완료 단계를 수행 하는 hello:
   
   1. 두 번 클릭 하 여 StorSimple Manager 서비스 tooaccess hello **빠른 시작** 페이지.
   2. **연결된 장치 보기**를 클릭합니다.
   3. Hello에 **장치** 페이지에서 해당 hello 장치 성공적으로 hello 상태를 조회 하 여 toohello 서비스 연결을 확인 합니다. hello 장치 상태가 **온라인**합니다. Hello 장치 상태 이면 **오프 라인**, 몇 분까지 hello 장치 toocome 온라인 정도 기다립니다.
   
   ![StorSimple 장치 페이지](./media/storsimple-configure-and-register-device/HCS_DevicesPageM-include.png) 
   
   > [!IMPORTANT]
   > Hello 장치가 온라인 후이 단계의 hello 시작 부분에서 분리 했습니다 hello 네트워크 케이블을 연결 합니다.
   > 
   > 

Hello 장치를 등록 및 온라인 상태로 전환 하지 않습니다, 후 hello를 실행할 수 있습니다 `Test-HcsmConnection -Verbose` 네트워크 연결이 hello tooensure 정상입니다. Hello에 대 한 자세한 사용 현황이이 cmdlet의 이동 너무[Test-hcsmconnection 용 cmdlet 참조](https://technet.microsoft.com/library/dn715782.aspx)합니다.

![동영상 사용 가능](./media/storsimple-configure-and-register-device/Video_icon.png) **동영상 사용 가능**

toowatch 보여 주는 비디오에서 어떻게 tooconfigure 및 레지스터를 StorSimple 용 Windows PowerShell을 통해 장치 클릭 [여기](https://azure.microsoft.com/documentation/videos/initialize-the-storsimple-appliance/)합니다.

