<!--author=SharS last changed: 02/04/2016-->

#### <a name="toocreate-a-volume"></a>toocreate 볼륨
1. Hello 장치에서 **빠른 시작** 페이지 **볼륨 추가**합니다. Hello 추가 볼륨 마법사를 시작합니다.
2. Hello 볼륨 마법사를 아래에서 추가 **기본 설정**, 다음 hello지 않습니다.
   
   1. 볼륨의 **이름** 을 지정합니다.
   2. Hello 지정 **프로 비전 된 용량** GB 또는 TB에서 볼륨에 대 한 합니다. 볼륨 용량은 hello 물리적 장치에 대 한 1GB ~ 64TB 사이 여야 합니다.
   3. Hello 드롭 다운 목록에서 선택 hello **사용 유형을** 볼륨에 대 한 합니다. 
   4. 이 볼륨 않는 아카이브 데이터를 사용 하는 경우 선택 hello **자주 액세스 하지 않는 아카이브 데이터에이 볼륨 사용** 확인란 합니다. 기타 모든 경우에는 **계층화된 볼륨**을 선택합니다. (계층화된 볼륨이 이전에는 기본 볼륨이었습니다.)
      
        ![볼륨 추가](./media/storsimple-create-volume/ScreenshotUpdate1VolumeFlow.png)
      
      1. Hello 화살표 아이콘을 클릭 합니다. ![화살표 아이콘](./media/storsimple-create-volume/HCS_ArrowIcon-include.png) toogo toohello 다음 페이지입니다.
3. Hello에 **추가 설정을** 대화 상자, 새로운 액세스 제어 레코드 (ACR) 추가:
   
   1. ACR의 **이름** 을 지정합니다.
   2. 아래 **iSCSI 초기자 이름**, 제공 hello iSCSI 정규화 된 이름 (IQN) Windows 호스트의 합니다. IQN hello를 설정 하지 않은 경우 너무 이동[Get hello Windows Server 호스트의 IQN](#get-the-iqn-of-a-windows-server-host)합니다.
   3. Hello를 선택 하 여 기본 백업을 사용 하도록 설정한 것이 좋습니다 **이 볼륨에 대 한 기본 백업 사용** 확인란 합니다. hello 기본 백업에서 22 시 30 매일 (장치 시간) 실행 하 고이 볼륨의 클라우드 스냅숏을 만드는 하는 정책을 만듭니다.
      
      > [!NOTE]
      > 여기에 hello 백업을 사용 하는지, 되돌릴 수 없습니다. 이 설정은 tooedit hello 볼륨 toomodify 필요 합니다.
      > 
      > 
      
        ![볼륨 추가](./media/storsimple-create-volume/AddVolume2-include.png)
4. Hello 확인 아이콘을 클릭 합니다. ![확인 아이콘](./media/storsimple-create-volume/HCS_CheckIcon-include.png)에서도 확인할 수 있습니다. 지정 된 hello로 볼륨을 만들 수는 설정입니다.

![동영상 사용 가능](./media/storsimple-create-volume/Video_icon.png) **동영상 사용 가능**

toowatch 보여 주는 비디오에서 toocreate StorSimple 볼륨을 클릭 하는 방법을 [여기](https://azure.microsoft.com/documentation/videos/create-a-storsimple-volume/)합니다.

