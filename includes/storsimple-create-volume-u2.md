<!--author=alkohli last changed: 08/16/2016-->

#### <a name="toocreate-a-volume"></a>toocreate 볼륨
1. Hello 장치에서 **빠른 시작** 페이지 **볼륨 추가** toostart hello 추가 볼륨 마법사.
2. Hello 볼륨 마법사를 아래에서 추가 **기본 설정**:
   
   1. 볼륨의 **이름** 을 입력합니다.
   2. Hello 드롭 다운 목록에서 선택 hello **사용 유형을** 볼륨에 대 한 합니다. 로컬 보증, 낮은 대기 시간 및 높은 성능이 필요한 워크로드의 경우 **로컬로 고정** 볼륨을 선택합니다. 다른 모든 데이터에 대해서는 **계층화됨** 볼륨을 선택합니다. 아카이브 데이터에 이 볼륨을 사용하려면 **자주 액세스하지 않는 아카이브 데이터에 대해 이 볼륨 사용**을 선택합니다. 
      
       로컬 고정된 볼륨 씩 프로 비전 하 고 hello hello 볼륨에 기본 데이터를 로컬 toohello 장치 상태를 유지 하 고 toohello 클라우드를 분산 하지 않습니다.  Hello 장치가 hello 로컬 계층에서 사용 가능한 공간을 확인 하는 로컬 고정된 볼륨을 만드는 경우의 hello tooprovision hello 볼륨 크기를 요청 했습니다. 로컬 고정된 볼륨 만들기의 hello 작동 hello 장치 toohello 클라우드에서 기존 데이터를 모두 포함 될 수 있습니다 및 toocreate hello 볼륨 hello 시간이 길어질 수 있습니다. hello 총 시간 hello 프로 비전 된 볼륨, 사용 가능한 네트워크 대역폭 및 장치의 hello 데이터의 hello 크기에 따라 달라 집니다. 
      
       계층화된 볼륨은 씬 프로비전되며 빠르게 만들 수 있습니다. 선택 하면 **자주 액세스 하지 않는 아카이브 데이터에이 볼륨 사용** 볼륨에 대 한 아카이브 데이터 변경 내용 hello 중복 제거 청크 크기에 대 한 대상으로 하는 계층화 된 볼륨에 대 한 too512 (kb)입니다. 이 필드를 선택 하지 않으면 해당 계층화 된 볼륨 hello 청크 크기는 64KB를 사용 합니다. 더 큰 중복 제거 청크 크기가 큰 않는 아카이브 데이터 toohello 클라우드의 hello 장치 tooexpedite hello 전송을 수 있습니다.
   3. Hello 지정 **프로 비전 된 용량** 볼륨에 대 한 합니다. 선택 하는 hello 볼륨 종류에 따라 사용할 수 있는 hello 용량의 메모를 확인 합니다. hello 지정 hello 사용 가능한 공간 볼륨 크기를 초과할 수 없습니다.
      
       Too8.5 TB 로컬로 고정 된 볼륨 또는 hello 8100 장치에서 too200 TB 계층화 된 볼륨을 제공할 수 있습니다. Hello 큰 8600 장치의 too22.5 TB 로컬로 고정 된 볼륨 또는 too500 TB 계층화 된 볼륨을 제공할 수 있습니다. Hello 장치의 로컬 공간이 필요한 toohost hello 작업 계층화 된 볼륨의 집합 이므로 로컬 고정된 볼륨 만들기 hello 공간을 계층화 된 볼륨을 프로 비전에 사용할 수 있는 영향을 줍니다. 따라서 로컬로 고정된 볼륨을 만드는 경우 계층화된 볼륨을 만드는 데 사용할 수 있는 공간이 줄어듭니다. 마찬가지로, 계층화 된 볼륨을 만들면 로컬 고정된 볼륨 만들기에 대 한 hello 사용 가능한 공간이 줄어듭니다.
      
       8100 장치에서 로컬로 고정 된 양의 8.5 TB (최대 허용 크기)를 프로 비전 hello 장치에서 사용 가능한 모든 hello 로컬 공간이 소진 되었을 있습니다. 됩니다 수 toocreate 계층화 된 볼륨에서 볼륨을 계층화 된 포인트부터 같이 hello의 hello 장치 toohost hello 작업 집합에 로컬 공간이 인지 합니다. 기존의 계층화 된 볼륨에 사용할 수 있는 hello 공간을 영향이 있습니다. 예를 들어 대략 106TB의 계층화된 볼륨이 있는 8100 장치에서는 로컬 고정 볼륨에 대해 4TB의 공간만 사용할 수 있습니다.
      
       hello 다음 그림에 나와 hello **기본 설정** 로컬 고정된 볼륨에 대 한 대화 상자.
      
        ![로컬 볼륨 추가](./media/storsimple-create-volume-u2/add-local-volume-include.png)
      
       hello 다음 그림에 나와 hello **기본 설정** 계층화 된 볼륨에 대 한 대화 상자.
      
        ![로컬 볼륨 추가](./media/storsimple-create-volume-u2/add-tiered-volume-include.png)
   
   1. Hello 화살표 아이콘을 클릭 합니다. ![화살표 아이콘](./media/storsimple-create-volume-u2/HCS_ArrowIcon-include.png) toogo toohello 다음 페이지입니다.
3. Hello에 **추가 설정을** 대화 상자, 새로운 액세스 제어 레코드 (ACR) 추가:
   
   1. ACR의 **이름** 을 지정합니다.
   2. 아래 **iSCSI 초기자 이름**, 제공 hello iSCSI 정규화 된 이름 (IQN) Windows 호스트의 합니다. IQN hello를 설정 하지 않은 경우 너무 이동[Get hello Windows Server 호스트의 IQN](#get-the-iqn-of-a-windows-server-host)합니다.
   3. 아래 **이 볼륨에 대 한 기본 백업?**선택, hello **사용** 확인란 합니다. hello 기본 백업에서 22 시 30 매일 (장치 시간) 실행 하 고이 볼륨의 클라우드 스냅숏을 만드는 하는 정책을 만듭니다.
      
      > [!NOTE]
      > 여기에 hello 백업을 사용 하는지, 되돌릴 수 없습니다. 이 설정은 tooedit hello 볼륨 toomodify 필요합니다.
      > 
      > 
      
      ![볼륨 추가](./media/storsimple-create-volume-u2/AddVolumeAdditionalSettings1.png)
4. Hello 확인 아이콘을 클릭 합니다. ![확인 아이콘](./media/storsimple-create-volume-u2/HCS_CheckIcon-include.png)에서도 확인할 수 있습니다. 볼륨을 지정 하는 hello로 만들면 설정 합니다.

