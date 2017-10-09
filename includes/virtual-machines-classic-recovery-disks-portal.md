Azure에서 가상 컴퓨터 (VM) 부팅 또는 디스크 오류가 발생 하는 경우 문제 해결 단계는 자체 hello 가상 하드 디스크에서 tooperform을 할 수 있습니다. 일반적인 예로 hello VM 부팅을 성공적으로 방지 하는 실패 한 응용 프로그램 업데이트는 것입니다. 이 문서에서는 설명 방법을 toouse Azure 포털 tooconnect에 가상 하드 디스크 tooanother VM toofix 오류 원래 VM을 다시 만듭니다.

## <a name="recovery-process-overview"></a>복구 프로세스 개요
hello 문제 해결 과정은 다음과 같습니다.

1. Hello 문제를 발생 하는 VM을 삭제 하 않지만 hello 가상 하드 디스크를 보존 합니다.
2. 첨부 하 고 문제 해결에 대 한 hello 가상 하드 디스크 tooanother VM에 탑재 합니다.
3. Toohello VM 문제 해결을 연결 합니다. 파일을 편집 하거나 hello 원래 가상 하드 디스크에 toofix 오류 도구를 실행 합니다.
4. 탑재 해제 하 고 VM의 문제를 해결 하는 hello에서 hello 가상 하드 디스크를 분리 합니다.
5. Hello 원래 가상 하드 디스크를 사용 하 여 VM을 만듭니다.

## <a name="delete-hello-original-vm"></a>삭제 hello 원본 VM
가상 하드 디스크와 VM은 Azure의 두 가지 별개의 리소스입니다. 가상 하드 디스크는 hello 운영 체제, 응용 프로그램 및 구성 저장 됩니다. hello VM hello 크기 또는 위치를 정의 하 고 가상 하드 디스크 또는 가상 네트워크 인터페이스 카드 (NIC) 등의 리소스를 참조 하는 메타 데이터만입니다. 각 가상 하드 디스크는 해당 디스크가 연결 된 tooa VM 때 할당 된 임대를 가져옵니다. 데이터 디스크를 연결 하 고 hello VM에서 실행 중인 동안에 분리 수, 있지만 hello VM 리소스는 삭제 하지 않는 한 hello OS 디스크를 분리할 수 없습니다. 해당 VM 중지 및 할당 취소 된 상태에 있을 경우에 hello 임대 tooassociate hello OS 디스크 tooa VM을 계속 합니다.

첫 번째 단계 toorecovering hello VM은 자체 toodelete hello VM 리소스입니다. VM 삭제 hello 저장소 계정의 hello 가상 하드 디스크를 유지합니다. VM을 삭제 하는 hello, 후 hello 가상 하드 디스크 tooanother VM tootroubleshoot 연결 수 있으며 hello 오류를 해결할 수 있습니다. 

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다. 
2. Hello 왼쪽에 hello 메뉴를 클릭 **가상 컴퓨터 (클래식)**합니다.
3. 선택 hello에 hello 문제가 VM 클릭 **디스크**, 고 hello 가상 하드 디스크의 hello 이름을 식별 합니다. 
4. Hello 운영 체제 가상 하드 디스크를 선택 하 고 hello 확인 **위치** 해당 가상 하드 디스크가 포함 된 tooidentify hello 저장소 계정입니다. 다음 예제는 hello, 문자열을 바로 앞 hello "입니다. blob.core.windows.net" hello 저장소 계정 이름입니다.

    ```
    https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd
    ```

    ![VM의 위치에 대 한 hello 이미지](./media/virtual-machines-classic-recovery-disks-portal/vm-location.png)

5. Hello VM을 마우스 오른쪽 단추로 클릭 한 다음 선택 **삭제**합니다. Hello 디스크 hello VM을 삭제 하는 경우 선택 하지 않은 있는지 확인 합니다.
6. 새 복구 VM을 만듭니다. 이 VM hello에 있어야 합니다. 동일한 지역 및 리소스 그룹 (클라우드 서비스) hello 문제 VM입니다.
7. Hello 복구 VM을 선택한 다음 선택 **디스크** > **기존 연결**합니다.
8. tooselect 기존 가상 하드 디스크를 클릭 **VHD 파일**:

    ![기존 VHD 찾아보기](./media/virtual-machines-classic-recovery-disks-portal/select-vhd-location.png)

9. Hello 저장소 계정을 선택 > VHD 컨테이너 > hello 가상 하드 디스크를 hello 클릭 **선택** tooconfirm 단추를 선택 합니다.

    ![기존 VHD 선택](./media/virtual-machines-classic-recovery-disks-portal/select-vhd.png)

10. 이제 선택한 VHD를 선택 **확인** tooattach hello 기존 가상 하드 디스크입니다.
11. 몇 초 후 hello **디스크** VM에 대 한이 창에 데이터 디스크로 연결 된 기존 가상 하드 디스크에 표시 됩니다.

    ![데이터 디스크로 연결된 기존 가상 하드 디스크](./media/virtual-machines-classic-recovery-disks-portal/attached-disk.png)

## <a name="fix-issues-on-hello-original-virtual-hard-disk"></a>Hello 원래 가상 하드 디스크에서 문제를 수정 합니다.
Hello 기존 가상 하드 디스크를 탑재 하는 경우 모든 유지 관리 및 문제 해결 단계는 필요에 따라 이제 수행할 수 있습니다. Hello 문제를 해결 한 후 단계를 수행 하는 hello로 계속 합니다.

## <a name="unmount-and-detach-hello-original-virtual-hard-disk"></a>분리 및 hello 원래 가상 하드 디스크를 분리 합니다.
모든 오류가 해결 되 면 탑재 해제 하 고 hello 기존 가상 하드 디스크 문제 해결 VM에서 분리 합니다. Hello 가상 하드 디스크 toohello VM 문제 해결을 연결 하는 hello 임대가 해제 될 때까지 다른 VM과 함께 가상 하드 디스크를 사용할 수 없습니다.  

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다. 
2. Hello 왼쪽에 hello 메뉴에서 선택 **가상 컴퓨터 (클래식)**합니다.
3. Hello 복구를 VM을 찾습니다. 디스크를 마우스 오른쪽 단추로 클릭 hello 디스크를 선택한 다음 선택 **분리**합니다.

## <a name="create-a-vm-from-hello-original-hard-disk"></a>Hello 원래 하드 디스크에서 VM 만들기

원래 가상 하드 디스크에서 VM에서 사용할 toocreate [Azure 클래식 포털](https://manage.windowsazure.com)합니다.

1. [Azure 클래식 포털](https://manage.windowsazure.com)에 로그인합니다.
2. Hello 포털의 hello 맨 아래에 선택 **새로** > **계산** > **가상 컴퓨터** > **갤러리에서** .
3. Hello에 **이미지 선택** 섹션에서 **내 디스크**을 다음 선택 hello 원래 가상 하드 디스크 및 합니다. Hello 위치 정보를 확인 합니다. 이 hello 영역 hello VM 배포 되어야 합니다. Hello 다음 단추를 선택 합니다.
4. Hello에 **가상 컴퓨터 구성** 섹션 hello VM 이름을 입력 하 고 hello VM 크기를 선택 합니다.
