#### <a name="toostop-and-start-a-cloud-appliance"></a>toostop 및 클라우드 어플라이언스에 시작

1. 클라우드 어플라이언스에 toostop toohello VM 클라우드 장비에 대 한 이동 합니다.
    ![StorSimple Cloud Appliance 가상 컴퓨터](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)

2. Hello 명령 모음에서 클릭 **중지**합니다.

    ![StorSimple Cloud Appliance 가상 컴퓨터](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. 확인하라는 메시지가 표시되면 **예**를 클릭합니다.

    ![StorSimple Cloud Appliance 가상 컴퓨터](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. VM을 중지하면 할당 취소됩니다. 상태는 hello 클라우드 장비를 중지 하는 동안 **Deallocating**합니다. Hello 클라우드 어플라이언스에 중지 된 후에 상태가 **중지 됨 (할당 취소 됨)**합니다.

    ![StorSimple Cloud Appliance 가상 컴퓨터](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. VM 중지 되 고 나면 클릭 **시작** (단추를 사용할 수) toostart hello VM입니다. Hello 클라우드 장비 시작 된 후에 상태가 **Started**합니다.

    ![StorSimple Cloud Appliance 가상 컴퓨터](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

다음 cmdlet toostop hello를 사용 하 고 클라우드 장비를 시작 합니다.

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-cloud-appliance"></a>클라우드 어플라이언스에 toorestart

클라우드 어플라이언스에 toorestart toohello VM 클라우드 장비에 대 한 이동 합니다. Hello 명령 모음에서 클릭 **다시 시작**합니다. 메시지가 표시 되 면 hello를 다시 시작을 확인 합니다. 상태는 hello 클라우드 어플라이언스에 toouse 있습니다에 대 한 준비 되 면 **실행**합니다.

![StorSimple Cloud Appliance 가상 컴퓨터](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

다음 cmdlet toorestart 클라우드 어플라이언스에 hello를 사용 합니다.

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

