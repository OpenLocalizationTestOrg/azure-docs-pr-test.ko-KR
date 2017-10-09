<!--author=alkohli last changed: 02/22/2016-->


### <a name="tooconfigure-and-register-hello-device"></a>tooconfigure 및 레지스터 hello 장치
1. StorSimple 장치 직렬 콘솔에 hello Windows PowerShell 인터페이스에 액세스 합니다. 참조 [PuTTY를 사용 하 여 장치 직렬 콘솔 tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console) 지침에 대 한 합니다. **있는지 toofollow hello 절차를 정확 하 게 것인지 수 tooaccess hello 콘솔 됩니다.**
2. 가 열리면 hello 세션에서 입력 한 시간 tooget 명령 프롬프트를 키를 누릅니다. 
3. 싶다는 의사를 tooset 장치에 대 한 증명된 toochoose hello 언어 됩니다. Hello 언어를 지정 하 고 enter 키를 누릅니다. 
   
    ![StorSimple 구성 및 등록 장치 1](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice1-U1-include.png)
4. 제공 되는 hello 직렬 콘솔 메뉴에서 옵션 1 toolog에 대 한 모든 권한을 선택 합니다. 
   
    ![StorSimple 등록 장치 2](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice2_U1-include.png)
   
     장치에 대 한 단계 5-12 tooconfigure hello 필요한 최소 네트워크 설정을 완료 합니다. **이러한 구성 단계 toobe hello hello 장치의 활성 컨트롤러에서 수행 해야 합니다.** hello 직렬 콘솔 메뉴 hello 배너 메시지에 hello 컨트롤러 상태를 나타냅니다. 연결 되어 있지 않으면 toohello 활성 컨트롤러를 분리 하 고 toohello 활성 컨트롤러를 연결 합니다.
5. Hello 명령 프롬프트에서 암호를 입력 합니다. hello 기본 장치 암호는 **Password1**합니다.
6. 다음 명령을 형식 hello: `Invoke-HcsSetupWizard`합니다. 
7. 설치 마법사는 hello 장치에 대 한 hello 네트워크 설정을 구성 하는 toohelp 표시 됩니다. Hello hello 다음 정보를 제공 합니다. 
   
   * Hello DATA 0 네트워크 인터페이스에 대 한 IP 주소
   * 서브넷 마스크
   * 게이트웨이
   * 주 DNS 서버의 IP 주소
     
        Hello 프로세스의 각 단계 후 네트워크 설정을 hello 시스템의 유효성 검사를 참고 합니다.
     
     > [!NOTE]
     > Hello 서브넷 마스크 및 hello DNS 설정 toobe 적용에 대 일 분 동안 toowait이 있을 수 있습니다. "확인 hello 네트워크 연결 tooData 0" 오류 메시지가 발생할 경우 활성 컨트롤러의 DATA 0 네트워크 인터페이스 hello에 hello 실제 네트워크 연결을 확인 합니다.
     > 
     > 
8. (선택 사항) 웹 프록시 서버를 구성합니다. 웹 프록시 구성은 선택 사항이지만 **웹 프록시를 사용하면 여기서만 구성할 수 있습니다**. 자세한 내용은 이동 너무[장치에 대 한 웹 프록시 구성](../articles/storsimple/storsimple-configure-web-proxy.md)합니다.
9. 장치에 대한 기본 NTP 서버를 구성합니다. 클라우드 서비스 공급자와 인증할 수 있도록 장치 시간을 동기화해야 하는 것처럼 NTP 서버가 필요합니다. 네트워크 사용자 데이터 센터 toohello 인터넷에서에서 NTP 트래픽이 toopass 허용 되는지 확인 합니다. 허용되지 않는 경우 내부 NTP 서버를 지정합니다. 
10. 보안상의 이유로 hello 첫 번째 세션 후 hello 장치 관리자 암호가 만료 되어 toochange 해야 it 이제 합니다. 메시지가 표시되면 장치 관리자 암호를 제공합니다. 유효한 장치 관리자 암호는 8자에서 15자 사이여야 합니다. hello 암호에 포함 해야 hello 다음의 3 개: 소문자, 대문자, 숫자 및 특수 문자.
    
    <br/>![StorSimple 등록 장치 5](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice5_U1-include.png)
11. hello hello 설치 마법사의 마지막 단계는 hello StorSimple Manager 서비스와 장치를 등록합니다. 이 경우 2 단계에서 얻은 hello 서비스 등록 키를 해야 합니다. Hello 등록 키를 제공한 후 toowait hello 장치를 등록 하기 전에 2-3 분 동안 할 수 있습니다.
    
    > [!NOTE]
    > 모든 시간 tooexit hello 설치 마법사에서 Ctrl + C를 눌러 수 있습니다. 모든 hello 네트워크 설정 (Data 0, 서브넷 마스크 및 게이트웨이 IP 주소)를 입력 하면 입력 한 내용을 유지 됩니다.
    > 
    > 
    
    ![StorSimple 등록 장치 6](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice6_U1-include.png)
12. Hello 장치를 등록 한 후에 서비스 데이터 암호화 키가 표시 됩니다. 이 키를 복사하고 안전한 위치에 저장합니다. **이 키는 hello 서비스 등록 키 tooregister 추가 장치를 StorSimple Manager 서비스 hello 함께 해야 합니다.** 너무 참조[StorSimple 보안](../articles/storsimple/storsimple-security.md) 이 키에 대 한 자세한 내용은 합니다.
    
    ![StorSimple 등록 장치 7](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice7_U1-include.png)    
    
    > [!NOTE]
    > hello 직렬 콘솔 창에서 toocopy hello 텍스트 hello 텍스트를 선택 하면 됩니다. Toopaste 수 있어야 다음 hello 클립보드 또는 텍스트 편집기에서. Ctrl 키를 사용 하지 않는 + C toocopy hello 서비스 데이터 암호화 키입니다. Ctrl + C를 사용 하면 tooexit hello 설치 마법사를 발생 합니다. 결과적으로, hello 장치 관리자 암호가 변경 되지 않습니다 및 hello 장치 toohello 기본 암호 되돌아갑니다.
    > 
    > 
13. Hello 직렬 콘솔을 종료 합니다.
14. Azure 클래식 포털 toohello 돌아간 완료 단계를 수행 하는 hello:
    
    1. 두 번 클릭 하 여 StorSimple Manager 서비스 tooaccess hello **빠른 시작** 페이지.
    2. **연결된 장치 보기**를 클릭합니다.
    3. Hello에 **장치** 페이지에서 해당 hello 장치 성공적으로 hello 상태를 조회 하 여 toohello 서비스 연결을 확인 합니다. hello 장치 상태가 **온라인**합니다.
       
        ![StorSimple 장치 페이지](./media/storsimple-configure-and-register-device-u1/HCS_DevicesPageM_U1-include.png) 
       
        Hello 장치 상태 이면 **오프 라인**, 몇 분까지 hello 장치 toocome 온라인 정도 기다립니다. 
       
        몇 분 후 hello 장치는 계속 오프 라인 상태 경우 toomake에 설명 된 대로 방화벽 네트워크가 구성 되어 있는지 필요 [네트워킹 StorSimple 장치에 대 한 요구 사항이](../articles/storsimple/storsimple-system-requirements.md)합니다. 
       
        Hello 서비스 버스 StorSimple Manager 서비스-장치 통신에 사용이 포트 9354를 아웃 바운드 통신을 위해 열려 있는지 확인 합니다.

