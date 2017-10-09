


## <a name="attach-an-empty-disk"></a>빈 디스크 연결
Azure hello.vhd 파일을 만들어 드립니다 및 hello 저장소 계정에 저장 하기 때문에 데이터 디스크는 간단한 방법을 tooadd를은 빈 디스크를 연결 합니다.

1. 클릭 **가상 컴퓨터 (클래식)**, 다음 선택 hello 적절 한 VM 및 합니다.

2. Hello 설정 메뉴를 클릭 **디스크**합니다.

   ![새로운 빈 디스크 연결](./media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. Hello 명령 모음에서 **새 연결**합니다.  
    hello **새 디스크 연결** 대화 상자가 나타납니다.

    ![새 디스크 연결](./media/howto-attach-disk-windows-linux/newdiskdetail.png)

    Hello 다음 정보를 입력 합니다.
    - **파일 이름**hello 기본 이름을 그대로 사용 하거나 hello.vhd 파일에 대해 다른 이름을 입력 합니다. hello 데이터 디스크는 hello.vhd 파일에 다른 이름을 입력 하는 경우에 자동으로 생성 된 이름을 사용 합니다.
    - 선택 hello **형식** hello 데이터 디스크의 합니다. 모든 가상 컴퓨터에서 표준 디스크를 지원합니다. 많은 가상 컴퓨터에서 프리미엄 디스크도 지원합니다.
    - 선택 hello **크기 (GB)** hello 데이터 디스크의 합니다.
    - **호스트 캐싱**에 대해 없음 또는 읽기 전용을 선택합니다.
    - Toofinish 확인을 클릭 합니다.

4. Hello 데이터 디스크를 만들고 연결 된 후 hello VM의 hello 디스크 섹션에 나열 됩니다.

   ![새 빈 데이터 디스크가 성공적으로 연결됨](./media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> 데이터 디스크를 추가한 후 toolog toohello VM에 필요 하 고 사용할 수 있도록 hello 디스크를 초기화 합니다.

## <a name="how-to-attach-an-existing-disk"></a>방법: 기존 디스크 연결
기존 디스크를 연결하려면 저장소 계정에 사용 가능한 .vhd가 있어야 합니다. 사용 하 여 hello [Add-azurevhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet tooupload hello.vhd 파일 toohello 저장소 계정입니다. 만든 hello.vhd 파일을 업로드 한 후 VM tooa를 연결할 수 있습니다.

1. 클릭 **가상 컴퓨터 (클래식)**, 다음 선택 hello 적절 한 가상 컴퓨터 및 합니다.

2. Hello 설정 메뉴를 클릭 **디스크**합니다.

3. Hello 명령 모음에서 **연결 기존**합니다.

    ![데이터 디스크 연결](./media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. **위치**를 클릭합니다. hello 사용 가능한 저장소 계정을 표시합니다. 다음으로 목록에서 해당 저장소 계정을 선택합니다.

    ![디스크 저장소 계정 제공](./media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. **저장소 계정**은 디스크 드라이브(vhds)가 있는 하나 이상의 컨테이너를 보유합니다. 나열 된 hello 적절 한 컨테이너를 선택 합니다.

    ![virtual-machines-windows의 컨테이너 제공](./media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. hello **vhd** 패널 hello 컨테이너에서 hello 디스크 드라이브를 나열 합니다. Hello 디스크 중 하나를 클릭 하 고 선택을 클릭 합니다.

    ![virtual-machines-windows의 디스크 이미지 제공](./media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. hello **기존 디스크 연결** hello 저장소 계정, 컨테이너 및 선택한 하드 디스크 (vhd) tooadd toohello 가상 컴퓨터를 포함 하는 hello 위치와 패널 다시 표시 됩니다.

  설정 **호스트 캐싱** toonone 또는 읽기 전용 다음 확인을 클릭 합니다.

    ![데이터 디스크 연결됨](./media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)
