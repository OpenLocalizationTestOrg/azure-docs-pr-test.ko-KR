<!--author=alkohli last changed: 08/21/17-->

#### <a name="toodownload-hotfixes"></a>toodownload 핫픽스

Hello hello Microsoft Update 카탈로그에서에서 단계 toodownload hello 소프트웨어 업데이트를 다음을 수행 합니다.

1. Internet Explorer를 시작 하 고 탐색 너무[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com)합니다.
2. Microsoft Update 카탈로그 hello를 사용 하 여이 컴퓨터에 처음으로 이면 클릭 **설치** 때 메시지 표시 tooinstall hello Microsoft Update 카탈로그 추가 기능입니다.

    ![카탈로그 설치](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. Hello Microsoft Update 카탈로그의 hello 검색 상자에 hello 기술 자료 (KB) 번호를 입력 hello 핫픽스의 원하는 toodownload, 예를 들어 **4037264**, 클릭 하 고 **검색**합니다.
   
    hello 핫픽스 목록이 표시 되 면 예를 들어 **StorSimple 8000 시리즈에 대 한 누적 소프트웨어 번들 업데이트 5.0**합니다.
   
    ![카탈로그 검색](./media/storsimple-install-update5-hotfix/update-catalog-search.png)

4. **다운로드**를 클릭합니다. 지정 하거나 **찾아보기** tooa 로컬 위치 hello tooappear 다운로드 합니다. Hello 파일 클릭 toodownload toohello 위치 및 폴더를 지정 합니다. hello 폴더 hello 장치에서 연결할 수 있는 tooa 복사한 네트워크 공유 될 수도 있습니다.
5. 위의 hello 표에 나열 된 모든 추가 핫픽스에 대 한 검색 (**4037266**), 및 hello 테이블 앞에 나열 된 toohello 특정 폴더에 파일 다운로드 hello에 해당 합니다.

> [!NOTE]
> hello 핫픽스 두 컨트롤러 toodetect hello 피어 컨트롤러에서 잠재적인 오류 메시지에서 액세스할 수 있어야 합니다.
>
> hello 핫픽스 3 별도 폴더에 복사 해야 합니다. 예를 들어에 hello 장치 소프트웨어/Ci/MDS 에이전트 업데이트를 복사할 수 있습니다 _FirstOrderUpdate_ hello 모든 폴더를 다른 정기적인 업데이트 hello에 복사할 수 없습니다 _SecondOrderUpdate_ 폴더 및 유지 관리 모드 업데이트에서 복사한 _ThirdOrderUpdate_ 폴더입니다.

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a>tooinstall 일반 모드 핫픽스를 확인 합니다.

Hello 단계 tooinstall 다음을 수행 하 고 일반 모드 핫픽스를 확인 합니다. 이미 설치 하는 경우에 Azure 포털 hello를 사용 하 여 너무 건너 뛸[설치 하 고 유지 관리 모드 핫픽스 확인](#to-install-and-verify-maintenance-mode-hotfixes)합니다.

1. StorSimple 장치 직렬 콘솔에 액세스 hello Windows PowerShell 인터페이스 tooinstall hello 핫픽스 합니다. 에 따라 hello에 필요한 세부 정보 [사용 PuTTy tooconnect toohello 직렬 콘솔](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)합니다. Hello 명령 프롬프트에를 눌러 **Enter**합니다.
2. 선택 **옵션 1** toolog 전체 액세스 권한이 있는 toohello 장치에 있습니다. Hello 핫픽스 hello 수동 컨트롤러에 먼저 설치 해야 하는 것이 좋습니다.
3. tooinstall hello 핫픽스, 형식 hello 명령 프롬프트에서:
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    명령 위에 hello 공유 경로에 DNS를 사용 하지 않고 IP를 사용 합니다. hello credential 매개 변수는 인증 된 공유에 액세스 하는 경우에 사용 됩니다.
   
    Hello 자격 증명 매개 변수 tooaccess 공유를 사용 하는 것이 좋습니다. 열려 있는 너무 일반적으로 "everyone 이라는"도 공유 toounauthenticated 사용자 열.
   
4. 메시지가 표시 되 면 hello 암호를 제공 합니다. Hello 첫 번째 주문 업데이트를 설치 하기 위한 샘플 출력은 다음과 같습니다. 첫 번째 주문 업데이트 hello toopoint toohello 특정 파일이 필요합니다.

    >[!NOTE] 
    > Hello를 설치 해야 _HcsSoftwareUpdate.exe_ 첫 번째입니다. 이 설치가 완료된 후에 _CisMdsAgentUpdate.exe_를 설치합니다.
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts hello hotfix installation and could reboot one or
        both of hello controllers. If hello device is serving I/Os, these will not
        be disrupted. Are you sure you want toocontinue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
5. 형식 **Y** 때 메시지 표시 tooconfirm hello 핫픽스를 설치 합니다.
6. Hello를 사용 하 여 hello 업데이트를 모니터링할 `Get-HcsUpdateStatus` cmdlet. hello 업데이트 hello 수동 컨트롤러에서 먼저 완료 됩니다. Hello 수동 컨트롤러 업데이트 되, 장애 조치 됩니다 hello 업데이트 후에 적용 되 면 다른 컨트롤러를 hello 합니다. hello 컨트롤러를 모두 업데이트 하는 경우 hello 업데이트가 완료 되었습니다.
   
    hello 다음 샘플은 출력 hello 업데이트 진행 중에서입니다. hello `RunInprogress` 은 `True` hello 업데이트가 진행 중 설정 된 경우입니다.

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 07/28/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     다음 샘플 출력 hello 해당 hello 업데이트가 완료 된 나타냅니다. hello `RunInProgress` 은 `False` hello 업데이트 제거가 완료 합니다.
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 07/28/2017 9:15:55 AM
    LastUpdateTimestamp : 07/28/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > 경우에 따라서는 cmdlet 보고서 hello `False` hello 업데이트 중인 경우 계속 진행 합니다. 핫픽스 hello tooensure 완료, 몇 분 정도 기다렸다가,이 명령을 다시 실행 및 해당 hello 확인 `RunInProgress` 은 `False`합니다. 인 경우 hello 핫픽스 완료 되었습니다.

7. Hello 소프트웨어 업데이트가 완료 되 면 hello 시스템 소프트웨어 버전을 확인 합니다. 형식:
   
    `Get-HcsSystem`
   
    다음 버전 hello를 표시 되어야 합니다.
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 5.0`
   *  `HcsSoftwareVersion: 6.3.9600.17845`
   
    Hello 업데이트를 적용 한 후 hello 버전 번호가 변경 되지 않으면 해당 hello 핫픽스가 tooapply 못한 나타냅니다. 이 경우 추가 지원을 받으려면 [Microsoft 지원](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) 에 문의하세요.
     
    > [!IMPORTANT]
    > Hello hello 통해 활성 컨트롤러를 다시 시작 해야 `Restart-HcsController` 적용 하기 전에 cmdlet hello 다음 업데이트 합니다.
     
8. Tooinstall hello 3-6 단계를 반복 _CisMDSAgentupdate.exe_ 에이전트 다운로드 tooyour _FirstOrderUpdate_ 폴더입니다.
8. 3-6 단계 tooinstall hello 두 번째 주문 업데이트를 반복 합니다. 

    > [!NOTE] 
    > 두 번째 주문 업데이트에 대 한 여러 업데이트가 방금 hello를 실행 하 여 설치 수 `Start-HcsHotfix cmdlet` toohello 폴더는 두 번째 주문 업데이트의 위치를 가리키는 합니다. hello cmdlet hello 폴더에서 사용할 수 있는 모든 hello 업데이트 실행 됩니다. 업데이트가 이미 설치 되어 있는 경우 hello 업데이트 논리에서는 하는 검색 하 고 해당 업데이트를 적용 되지 않습니다.

    Hello를 사용 하 여 모든 hello 핫픽스를 설치 했으면 `Get-HcsSystem` cmdlet. hello 버전 이어야 합니다.
    
    * `CisAgentVersion:  1.0.9724.0`
    * `MdsAgentVersion: 35.2.2.0`
    * `Lsisas2Version: 2.0.78.00`


#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a>tooinstall 유지 관리 모드 핫픽스를 확인 합니다.

KB4037263 tooinstall 디스크 펌웨어 업데이트를 사용 합니다. 이러한 업데이트가 중단 되 고 약 30 분 toocomplete를 수행 합니다. 선택할 수 있습니다 tooinstall 계획 된 유지 관리 창에서 이러한 연결 toohello 장치 직렬 콘솔에서.

> [!NOTE] 
> 디스크 펌웨어 이미 최신 상태 이면 이러한 업데이트 tooinstall 필요 하지는 않습니다. Hello 실행 `Get-HcsUpdateAvailability` hello 장치 직렬 콘솔 toocheck 업데이트 사용할 수 있고 여부 hello에서 cmdlet은 중단 (유지 관리 모드) 또는 무중단 (일반 모드)를 업데이트 합니다. 업데이트 합니다.

tooinstall hello 디스크 펌웨어 업데이트 아래 hello 지침을 따릅니다.

1. Hello 유지 관리 모드에서 hello 장치를 배치 합니다. 

    > [!NOTE] 
    > 유지 관리 모드에서 tooa 장치를 연결할 때 Windows PowerShell 원격을 사용 하지 마십시오. 대신 hello 장치 컨트롤러 hello 장치 직렬 콘솔을 통해 연결 된 경우에이 cmdlet을 실행 합니다.

    유지 관리 모드에서 tooplace hello 컨트롤러 입력 합니다.
   
    `Enter-HcsMaintenanceMode`
   
    샘플 출력은 다음과 같습니다.
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8600
        Name: Update4-8600-mystorsimple
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    두 hello 컨트롤러 유지 관리 모드로 다시 시작 합니다.
2. tooinstall hello 디스크 펌웨어 업데이트, 유형:
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    샘플 출력은 다음과 같습니다.
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. Hello 설치 진행률 사용 하 여 모니터링 `Get-HcsUpdateStatus` 명령입니다. hello 업데이트가 완료 되 면 hello `RunInProgress` 쪽 변경`False`합니다.
4. Hello 설치가 완료 되 면 유지 관리 모드 핫픽스가 설치 되어 있는 hello hello 컨트롤러 다시 시작 됩니다. 모든 권한이 있는 옵션 1로 로그인 하 고 hello 디스크 펌웨어 버전을 확인 합니다. 형식:
   
   `Get-HcsFirmwareVersion`
   
   hello는 디스크 펌웨어 버전이 필요 합니다.
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N003, 0107`
   
   샘플 출력은 다음과 같습니다.
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8600
       Name: Update4-8600-mystorsimple
       Software Version: 6.3.9600.17845
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected tooController1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
           ActiveBIOS:0.45.0010
              BackupBIOS:0.45.0006
              MainCPLD:17.0.000b
              ActiveBMCRoot:2.0.001F
              BackupBMCRoot:2.0.001F
              BMCBoot:2.0.0002
              LsiFirmware:20.00.04.00
              LsiBios:07.37.00.00
              Battery1Firmware:06.2C
              Battery2Firmware:06.2C
              DomFirmware:X231600
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0x9134777A
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x19
              CanisterVPDCRC:0x142F7DC2
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:1.00|1.05
              PCM1VPDStructure:0x05
              PCM1VPDCRC:0x41BEF99C
              PCM2Firmware:1.00|1.05
              PCM2VPDStructure:0x05
              PCM2VPDCRC:0x41BEF99C

           EbodFirmware
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0xB23150F8
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x14
              CanisterVPDCRC:0xBAA55828
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:3.11
              PCM1VPDStructure:0x03
              PCM1VPDCRC:0x6B58AD13
              PCM2Firmware:3.11
              PCM2VPDStructure:0x03
              PCM2VPDCRC:0x6B58AD13

           DisksFirmware
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
   
    Hello 실행 `Get-HcsFirmwareVersion` 소프트웨어 버전 hello 하는 hello 두 번째 컨트롤러 tooverify에 명령 업데이트 되었습니다. 그런 다음 hello 유지 관리 모드를 종료할 수 있습니다. 따라서 toodo 다음 각 장치 컨트롤러에 대 한 명령을 hello를 입력 합니다.
   
   `Exit-HcsMaintenanceMode`

5. 유지 관리 모드를 종료 하는 hello 컨트롤러 다시 시작 합니다. Hello 디스크 펌웨어 후 업데이트를 적용 하 고 hello 장치 반환 toohello Azure 포털의 유지 관리 모드 종료 되었습니다. Note 24 시간 동안 hello 유지 관리 모드 업데이트를 설치한 hello 포털이 표시 되지 않습니다.

