<!--author=alkohli last changed: 9/17/15-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a>toocomplete hello 최소 StorSimple 장치 설치
1. Hello에 **장치** 페이지에서 선택 hello 장치 hello 장치 이름 toogo toohello 특정 장치 페이지에 대 한 hello 화살표를 클릭 합니다. 
   
    ![장치가 온라인 상태의 장치 페이지](./media/storsimple-complete-minimum-device-setup/HCS_DevicesPageM-include.png) 
2. 빠른 시작 아이콘을 클릭 ![빠른 시작 아이콘](./media/storsimple-complete-minimum-device-setup/HCS_QuickStartIcon-include.png) tooaccess hello 장치 빠른 시작 페이지입니다. 클릭 **장치 설정 완료** toostart hello **장치 구성** 마법사.
   
    ![장치 빠른 시작 페이지](./media/storsimple-complete-minimum-device-setup/Device_Quick_Start_page_1M.png)
3. Hello에 **기본 설정** 페이지에서 다음 hello지 않습니다.
   
   1. 장치의 **이름** 을 제공합니다. hello 기본 장치 이름이 hello 장치 모델 및 일련 번호와 같은 정보를 반영합니다. 장치를 too64 문자 toomanage의 식별 이름에 할당할 수 있습니다.
   2. 집합 hello **시간대** hello 지리적 위치 장치 배포 되 고 있는 hello에 기반 합니다. 장치는 모든 예약된 작업에 대해 이 표준 시간대를 사용합니다.
   3. **DNS 설정** 아래에서 **보조 DNS 서버**의 주소를 제공합니다. I p v 6을 사용 하는 경우에 hello hello Windows PowerShell 인터페이스에서 입력 한 IPv6 접미사에 따라 hello 필드 입력 됩니다. 
      Hello 보조 DNS 서버가 구성 되지 않은 경우 됩니다 toosave 장치 구성을 허용 합니다.
   4. iSCSI 사용 인터페이스에서 iSCSI에 하나 이상의 네트워크를 사용하도록 설정합니다. 하나 이상의 네트워크 인터페이스 toobe 클라우드 사용 되어야 하며 인터페이스를 하나 사용할 수 있는 iSCSI toobe 필요 합니다. 데이터 0은 클라우드를 사용할 수 있도록 자동으로 설정됩니다.
      
      ![StorSimple 최소 장치 설치 기본 설정](./media/storsimple-complete-minimum-device-setup/HCS_MinDeviceSetupBasicSettings1-include.png)
4. Hello 화살표 아이콘을 클릭 합니다. ![StorSimple 화살표 아이콘](./media/storsimple-complete-minimum-device-setup/HCS_ArrowIcon-include.png)
5. Hello에 **네트워크 인터페이스** 페이지 hello 컨트롤러 0에 대 한 IP 주소 및 컨트롤러 1 고정을 제공 합니다. Hello DATA 0 인터페이스에 대해 구성 된 4 hello 고정 IPv4 형식 hello에 제공 된 IP 주소 필요 toobe. IPv6 구성을 위한 접두사를 입력 하는 경우 이러한 필드에 hello 고정 IP 주소를 자동으로 입력 됩니다.

    > [!NOTE] 
    > - hello 컨트롤러 고정 IP 주소 필요 toobe 사용 가능한 Ip 액세스할 수 있는 hello 서브넷 내에서 hello 장치 IP 주소입니다.
    > - hello 컨트롤러에 대 한 IP 주소를 고정 하는 hello hello 업데이트 toohello 장치를 서비스에 사용 됩니다 하 고 따라서 hello 고정 Ip 라우팅 가능 하 고 수 tooconnect toohello 인터넷 해야 합니다.

    ![StorSimple 최소 장치 설치 네트워크 인터페이스](./media/storsimple-complete-minimum-device-setup/HCS_MinDeviceSetupNetworkInterfaces2-include.png)

1. Hello 확인 아이콘을 클릭 ![StorSimple 확인 아이콘](./media/storsimple-complete-minimum-device-setup/HCS_CheckIcon-include.png)합니다.
   Toohello 장치 돌아가게 됩니다 **빠른 시작** 페이지.
   
   > [!NOTE]
   > 수정할 수 있습니다 모든 hello 다른 장치 설정을 언제 든 지 hello에 액세스 하 여 **구성** 페이지.
   > 
   > 

![동영상 사용 가능](./media/storsimple-complete-minimum-device-setup/Video_icon.png) **동영상 사용 가능**

toowatch toocomplete 최소 장치 설정 hello 하는 방법을 보여 주는 비디오에서 클릭 [여기](https://azure.microsoft.com/documentation/videos/minimum-storsimple-device-setup/)합니다.

