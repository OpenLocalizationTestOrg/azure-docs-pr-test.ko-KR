<!--author=SharS last changed: 02/22/2016-->

### <a name="tooconfigure-and-register-hello-device"></a>tooconfigure 및 레지스터 hello 장치
1. StorSimple 장치 직렬 콘솔에 hello Windows PowerShell 인터페이스에 액세스 합니다. 참조 [PuTTY를 사용 하 여 장치 직렬 콘솔 tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) 지침에 대 한 합니다. **있는지 toofollow hello 절차를 정확 하 게 것인지 수 tooaccess hello 콘솔 됩니다.**
2. 가 열리면 hello 세션에서 입력 한 시간 tooget 명령 프롬프트를 키를 누릅니다.
3. 싶다는 의사를 tooset 장치에 대 한 증명된 toochoose hello 언어 됩니다. Hello 언어를 지정 하 고 enter 키를 누릅니다.
   
    ![StorSimple 구성 및 등록 장치 1](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice1-gov-include.png)
4. 제공 되는 hello 직렬 콘솔 메뉴에서 옵션 1 toolog에 대 한 모든 권한을 선택 합니다.
   
    ![StorSimple 등록 장치 2](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice2-gov-include.png)
5. Hello 장치에 대 한 단계 tooconfigure hello 필요한 최소 네트워크 설정을 다음을 수행 합니다.
   
   > [!IMPORTANT]
   > 이러한 구성 단계 toobe hello hello 장치의 활성 컨트롤러에서 수행 해야 합니다. hello 직렬 콘솔 메뉴 hello 배너 메시지에 hello 컨트롤러 상태를 나타냅니다. Toohello 활성 컨트롤러를 연결 하지는 끊고 toohello 활성 컨트롤러를 연결 합니다.
   > 
   > 
   
   1. Hello 명령 프롬프트에서 암호를 입력 합니다. hello 기본 장치 암호는 **Password1**합니다.
   2. Hello 다음 명령을 입력 합니다.
      
        `Invoke-HcsSetupWizard`
   3. 설치 마법사는 hello 장치에 대 한 hello 네트워크 설정을 구성 하는 toohelp 표시 됩니다. Hello 다음 정보를 제공 합니다.
      
      * 데이터 0 네트워크 인터페이스의 IP 주소
      * 서브넷 마스크
      * 게이트웨이
      * 주 DNS 서버의 IP 주소
      * 주 NTP 서버의 IP 주소
      
      > [!NOTE]
      > Hello 서브넷 마스크 및 DNS 설정이 toobe 적용에 대 일 분 동안 toowait이 있을 수 있습니다.
      > 
      > 
   4. 선택적으로 웹 프록시 서버를 구성합니다.
      
      > [!IMPORTANT]
      > 웹 프록시 구성은 선택 사항이지만 웹 프록시를 사용하면 여기서만 구성할 수 있습니다. 자세한 내용은 이동 너무[장치에 대 한 웹 프록시 구성](../articles/storsimple/storsimple-configure-web-proxy.md)합니다.
      > 
      > 
6. Ctrl + C를 눌러 tooexit hello 설정 마법사입니다.
7. 다음과 같이 hello 업데이트를 설치 합니다.
   
   1. Hello cmdlet tooset Ip 두 hello 컨트롤러에서 다음을 사용 합니다.
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. Hello 명령 프롬프트에서 실행 `Get-HcsUpdateAvailability`합니다. 업데이트를 사용할 수 있는지 알림을 표시해야 합니다.
   3. `Start-HcsUpdate`을 실행합니다. 모든 노드에서 이 명령을 실행할 수 있습니다. Hello 첫 번째 컨트롤러에서 업데이트가 적용 됩니다, hello 컨트롤러 조치 실패 하 고에 업데이트가 적용 되며 hello hello 다른 컨트롤러.
      
      실행 하 여 hello hello 업데이트 진행률을 모니터링할 수 있습니다 `Get-HcsUpdateStatus`합니다.    
      
      hello 다음 샘플은 출력 hello 업데이트 진행 중에서입니다.
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ````
      
      다음 샘플 출력 hello 해당 hello 업데이트가 완료 된 나타냅니다.
      
      ```
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ```
      
      업데이트를 포함 하 여 hello 모든 tooapply hello Windows 업데이트 too11 시간이 걸릴 수 있습니다.
8. (기본적으로 toohello 공용 Azure 클래식 포털을 가리킴) 이므로 cmdlet toopoint hello 장치 toohello Microsoft Azure Government 포털 다음 hello를 실행 합니다. 두 컨트롤러가 모두 다시 시작됩니다. 각 컨트롤러 다시 시작 되 면 볼 수 있도록 toosimultaneously tooboth 컨트롤러를 연결 하는 두 개의 PuTTY 세션을 사용 하는 것이 좋습니다.
   
    `Set-CloudPlatform -AzureGovt_US`
   
   확인 메시지가 표시됩니다. Hello 기본값을 그대로 (**Y**).
9. 다음과 같은 cmdlet tooresume 설정이 hello를 실행 합니다.
   
    `Invoke-HcsSetupWizard`
   
    ![설치 마법사 다시 시작](./media/storsimple-configure-and-register-device-gov-u2/HCS_ResumeSetup-gov-include.png)
   
   설치 프로그램을 다시 시작할 때 hello 마법사는 hello 업데이트 2 버전 됩니다.
10. Hello 네트워크 설정을 적용 합니다. 각 설정에 동의하면 유효성 검사 메시지가 나타납니다.
11. 보안상의 이유로 hello 첫 번째 세션 후 hello 장치 관리자 암호가 만료 되어 toochange 해야 it 이제 합니다. 메시지가 표시되면 장치 관리자 암호를 제공합니다. 유효한 장치 관리자 암호는 8자에서 15자 사이여야 합니다. hello 암호에 포함 해야 hello 다음의 3 개: 소문자, 대문자, 숫자 및 특수 문자.
    
    <br/>![StorSimple 등록 장치 5](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice5_gov-include.png)
12. hello hello 설치 마법사의 마지막 단계는 hello StorSimple Manager 서비스와 장치를 등록합니다. 이렇게 하면 됩니다 필요 hello에서 얻은 서비스 등록 키 [2 단계: Get hello 서비스 등록 키](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key)합니다. Hello 등록 키를 제공한 후 toowait hello 장치를 등록 하기 전에 2-3 분 동안 할 수 있습니다.
    
    > [!NOTE]
    > 모든 시간 tooexit hello 설치 마법사에서 Ctrl + C를 눌러 수 있습니다. 모든 hello 네트워크 설정 (Data 0, 서브넷 마스크 및 게이트웨이 IP 주소)를 입력 하면 입력 한 내용을 유지 됩니다.
    > 
    > 
    
    ![StorSimple 등록 진행률](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegistrationProgress-gov-include.png)
13. Hello 장치를 등록 한 후에 서비스 데이터 암호화 키가 표시 됩니다. 이 키를 복사하고 안전한 위치에 저장합니다. **이 키는 hello 서비스 등록 키 tooregister 추가 장치를 StorSimple Manager 서비스 hello 함께 해야 합니다.** 너무 참조[StorSimple 보안](../articles/storsimple/storsimple-security.md) 이 키에 대 한 자세한 내용은 합니다.
    
    ![StorSimple 등록 장치 7](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > hello 직렬 콘솔 창에서 toocopy hello 텍스트 hello 텍스트를 선택 하면 됩니다. Toopaste 수 있어야 다음 hello 클립보드 또는 텍스트 편집기에서.
    > 
    > Ctrl 키를 사용 하지 않는 + C toocopy hello 서비스 데이터 암호화 키입니다. Ctrl + C를 사용 하면 tooexit hello 설치 마법사를 발생 합니다. 결과적으로, hello 장치 관리자 암호가 변경 되지 않습니다 및 hello 장치 toohello 기본 암호 되돌아갑니다.
    > 
    > 
14. Hello 직렬 콘솔을 종료 합니다.
15. Toohello Azure Government 포털을 반환 하 고 hello 다음 단계를 완료 합니다.
    
    1. 두 번 클릭 하 여 StorSimple Manager 서비스 tooaccess hello **빠른 시작** 페이지.
    2. **연결된 장치 보기**를 클릭합니다.
    3. Hello에 **장치** 페이지에서 해당 hello 장치 성공적으로 hello 상태를 조회 하 여 toohello 서비스 연결을 확인 합니다. hello 장치 상태가 **온라인**합니다.
       
        ![StorSimple 장치 페이지](./media/storsimple-configure-and-register-device-gov-u2/HCS_DeviceOnline-gov-include.png)
       
        Hello 장치 상태 이면 **오프 라인**, 몇 분까지 hello 장치 toocome 온라인 정도 기다립니다.
       
        몇 분 후 hello 장치는 계속 오프 라인 상태 경우 toomake에 설명 된 대로 방화벽 네트워크가 구성 되어 있는지 필요 [네트워킹 StorSimple 장치에 대 한 요구 사항이](../articles/storsimple/storsimple-system-requirements.md)합니다.
       
        Hello 서비스 버스 StorSimple Manager 서비스-장치 통신에 사용이 포트 9354를 아웃 바운드 통신을 위해 열려 있는지 확인 합니다.

