<!--author=alkohli last changed: 07/19/2017-->

#### <a name="toocreate-a-volume"></a>toocreate 볼륨
1. Hello에서 hello 장치 hello 테이블 형식 목록에서 **장치** 블레이드에서 장치를 선택 합니다. **+ 볼륨 추가**를 클릭합니다.

    ![새 볼륨 추가](./media/storsimple-8000-create-volume-u2/step5createvol1.png)

2. Hello에 **볼륨 추가** 블레이드:
   
   1. hello **선택 장치** 필드는 현재 장치의 자동으로 채워집니다.

   2. Hello 드롭 다운 목록에서 볼륨 tooadd 해야 하는 hello 볼륨 컨테이너를 선택 합니다. 

   3.  볼륨의 **이름** 을 입력합니다. Hello 볼륨을 만든 후에 볼륨을 바꿀 수 없습니다.

   4. Hello 드롭 다운 목록에서 선택 hello **형식** 볼륨에 대 한 합니다. 로컬 보증, 낮은 대기 시간 및 높은 성능이 필요한 워크로드의 경우 **로컬로 고정** 볼륨을 선택합니다. 다른 모든 데이터에 대해서는 **계층화됨** 볼륨을 선택합니다. 아카이브 데이터에 이 볼륨을 사용하려면 **자주 액세스하지 않는 아카이브 데이터에 대해 이 볼륨 사용**을 선택합니다.
      
       계층화된 볼륨은 씬 프로비전되며 빠르게 만들 수 있습니다. 선택 하면 **자주 액세스 하지 않는 아카이브 데이터에이 볼륨 사용** 볼륨에 대 한 아카이브 데이터 변경 내용 hello 중복 제거 청크 크기에 대 한 대상으로 하는 계층화 된 볼륨에 대 한 too512 (kb)입니다. 이 필드를 선택 하지 않으면 해당 계층화 된 볼륨 hello 청크 크기는 64KB를 사용 합니다. 더 큰 중복 제거 청크 크기가 큰 않는 아카이브 데이터 toohello 클라우드의 hello 장치 tooexpedite hello 전송을 수 있습니다.
       
       로컬 고정된 볼륨 씩 프로 비전 하 고 hello hello 볼륨에 기본 데이터를 로컬 toohello 장치 상태를 유지 하 고 toohello 클라우드를 분산 하지 않습니다.  Hello 장치가 hello 로컬 계층에서 사용 가능한 공간을 확인 하는 로컬 고정된 볼륨을 만드는 경우의 hello tooprovision hello 볼륨 크기를 요청 했습니다. 로컬 고정된 볼륨 만들기의 hello 작동 hello 장치 toohello 클라우드에서 기존 데이터를 모두 포함 될 수 있습니다 및 toocreate hello 볼륨 hello 시간이 길어질 수 있습니다. hello 총 시간 hello 프로 비전 된 볼륨, 사용 가능한 네트워크 대역폭 및 장치의 hello 데이터의 hello 크기에 따라 달라 집니다.

   5. Hello 지정 **프로 비전 된 용량** 볼륨에 대 한 합니다. 선택 하는 hello 볼륨 종류에 따라 사용할 수 있는 hello 용량의 메모를 확인 합니다. hello 지정 hello 사용 가능한 공간 볼륨 크기를 초과할 수 없습니다.
      
       Too8.5 TB 로컬로 고정 된 볼륨 또는 hello 8100 장치에서 too200 TB 계층화 된 볼륨을 제공할 수 있습니다. Hello 큰 8600 장치의 too22.5 TB 로컬로 고정 된 볼륨 또는 too500 TB 계층화 된 볼륨을 제공할 수 있습니다. Hello 장치의 로컬 공간이 필요한 toohost hello 작업 계층화 된 볼륨의 집합 이므로 로컬 고정된 볼륨 만들기 hello 공간을 계층화 된 볼륨을 프로 비전에 사용할 수 있는 영향을 줍니다. 따라서 로컬로 고정된 볼륨을 만드는 경우 계층화된 볼륨을 만드는 데 사용할 수 있는 공간이 줄어듭니다. 마찬가지로, 계층화 된 볼륨을 만들면 로컬 고정된 볼륨 만들기에 대 한 hello 사용 가능한 공간이 줄어듭니다.
      
       8100 장치에서 로컬로 고정 된 양의 8.5 TB (최대 허용 크기)를 프로 비전 hello 장치에서 사용 가능한 모든 hello 로컬 공간이 소진 되었을 있습니다. Hello의 hello 장치 toohost hello 작업 집합에 로컬 공간이 없을 때부터 해당 지점에서 모든 계층화 된 볼륨을 만들 수 없습니다 볼륨 계층입니다. 기존의 계층화 된 볼륨에 사용할 수 있는 hello 공간을 영향이 있습니다. 예를 들어 대략 106TB의 계층화된 볼륨이 있는 8100 장치에서는 로컬 고정 볼륨에 대해 4TB의 공간만 사용할 수 있습니다.

    6. Hello에 **호스트 연결** 필드 hello 화살표를 클릭 합니다. 

        ![연결된 호스트](./media/storsimple-8000-create-volume-u2/step5createvol2.png)

    7. Hello에 **호스트 연결** 블레이드에서 기존 ACR을 선택 하거나 hello 다음 단계를 수행 하 여 새 ACR을 추가 합니다.

       1. ACR의 **이름** 을 지정합니다.
       2. 아래 **iSCSI 초기자 이름**, 제공 hello iSCSI 정규화 된 이름 (IQN) Windows 호스트의 합니다. IQN hello를 설정 하지 않은 경우 너무 이동[Get hello Windows Server 호스트의 IQN](#get-the-iqn-of-a-windows-server-host)합니다.

    9. **만들기**를 클릭합니다. 볼륨을 지정 하는 hello로 만들면 설정 합니다.

        ![만들기 클릭](./media/storsimple-8000-create-volume-u2/step5createvol3.png)

        > [!NOTE]
        > 여기서 만든 hello 볼륨 보호 되지 않는 알아야 합니다. 이 볼륨 tootake 예약 된 백업을 사용 하 여 toocreate 및 백업 정책을 연결 해야 합니다. 

