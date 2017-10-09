연결 된 tooa 가상 컴퓨터 (VM) 되는 데이터 디스크를 더 이상 해야 하는 경우 쉽게 분리할 수 없습니다. Hello VM에서에서 디스크를 분리 하는 경우 hello 디스크가 없는 저장소에서 제거 합니다. Hello toouse hello 디스크에 기존 데이터를 다시 선택 하면 다시 연결할 수 toohello 동일한 VM 이거나 다른 컴퓨터입니다.  

> [!NOTE]
> Azure의 VM은 운영 체제 디스크, 로컬 임시 디스크, 선택적 데이터 디스크 등 다양한 유형의 디스크를 사용합니다. 자세한 내용은 [Virtual Machines용 디스크 및 VHD 정보](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요. 또한 hello VM을 삭제 하지 않는 한 운영 체제 디스크를 분리할 수 없습니다.

## <a name="find-hello-disk"></a>Hello 디스크 찾기
VM에서 디스크를 분리 하려면 먼저 toofind hello hello 디스크 toobe 분리에 대 한 식별자 LUN 번호를 아웃 해야 합니다. 다음이 단계를 수행 하는 toodo:

1. Azure CLI를 열고 및 [tooyour Azure 구독 연결](../articles/xplat-cli-connect.md)합니다. Azure 서비스 관리 모드(`azure config mode asm`)에 있는지 확인합니다.
2. 있는 디스크를 연결 된 tooyour VM에 알아봅니다. hello 다음 예에서는 나열 hello 라는 VM에 대 한 디스크 `myVM`:

    ```azurecli
    azure vm disk list myVM
    ```

    hello 비슷한 toohello 다음은 예제 출력:

    ```azurecli
    * Fetching disk images
    * Getting virtual machines
    * Getting VM disks
      data:    Lun  Size(GB)  Blob-Name                         OS
      data:    ---  --------  --------------------------------  -----
      data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
      data:    0    30        myDataDisk.vhd
      info:    vm disk list command OK
    ```

3. Hello LUN 또는 hello **논리 단위 번호** toodetach hello 디스크에 대 한 합니다.

## <a name="remove-operating-system-references-toohello-disk"></a>운영 체제 참조 toohello 디스크 제거
Hello Linux 게스트에서 hello 디스크를 분리 하기 전에 hello 디스크의 모든 파티션을 사용 하지 않는 있는지 확인 해야 합니다. 해당 hello 운영 체제 tooremount 시도 하지 않습니다 확인 후 다시 부팅 합니다. 다음이 단계 실행 시기 만들었을 것 hello 구성 취소 [연결](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) hello 디스크.

1. 사용 하 여 hello `lsscsi` 명령 toodiscover hello 디스크 식별자입니다. `lsscsi`는 `yum install lsscsi`(Red Hat 기반 배포) 또는 `apt-get install lsscsi`(Debian 기반 배포)를 통해 설치할 수 있습니다. Hello LUN 번호를 사용 하 여 원하는 hello 디스크 식별자를 찾을 수 있습니다. 각 행에 hello 튜플에 hello 마지막 번호는 hello LUN입니다. 다음 예제에서 hello에 `lsscsi`, LUN 0에 매핑합니다 너무  */개발/sdc*

    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```

2. 사용 하 여 `fdisk -l <disk>` hello 디스크 toobe 분리와 연결 된 toodiscover hello 파티션 합니다. hello 다음 보여 주는 예제에 대 한 hello 출력 `/dev/sdc`:

    ```bash
    Disk /dev/sdc: 1098.4 GB, 1098437885952 bytes, 2145386496 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x5a1d2a1a
    
        Device Boot      Start         End      Blocks   Id  System
    /dev/sdc1            2048  2145386495  1072692224   83  Linux
    ```

3. Hello 디스크에 대해 나열 된 각 파티션에 탑재 해제 합니다. hello 다음 예제에서는 분리 `/dev/sdc1`:

    ```bash
    sudo umount /dev/sdc1
    ```

4. 사용 하 여 hello `blkid` 모든 파티션에 대 한 명령 toodiscovery hello Uuid입니다. hello 비슷한 toohello 다음은 예제 출력:

    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

5. Hello에서 항목을 제거할 **/등/fstab** hello 디스크 toobe 분리에 대 한 모든 파티션에 대 한 hello 장치 경로 또는 Uuid와 연결 된 파일입니다.  이 예제에서는 해당 항목이 다음과 같을 수 있습니다.

    ```sh  
   UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults   1   2
   ```

    또는
   
   ```sh   
   /dev/sdc1   /datadrive   ext4   defaults   1   2
   ```

## <a name="detach-hello-disk"></a>Hello 디스크를 분리
준비 toodetach 하는 hello 디스크 및 운영 체제 참조 제거 hello의 hello LUN 번호를 찾은 다음 해당:

1. Hello 명령을 실행 하 여 hello 가상 컴퓨터에서 hello 선택한 디스크를 분리 `azure vm disk detach
   <virtual-machine-name> <LUN>`합니다. hello 다음 예제에서는 분리 LUN `0` hello 라는 VM에서에서 `myVM`:
   
    ```azurecli
    azure vm disk detach myVM 0
    ```

2. 실행 하 여 hello 디스크 분리 가져온 경우를 확인할 수 있습니다 `azure vm disk list` 다시 합니다. 다음 예제에서는 hello hello 라는 VM `myVM`:
   
    ```azurecli
    azure vm disk list myVM
    ```

    hello는 비슷한 toohello 다음 hello 데이터 디스크 연결 끊은 보여 주는 예제 출력:

    ```azurecli
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
     info:    vm disk list command OK
    ```

분리 hello 디스크 저장소에 남아 있지만 더 이상 tooa 연결 된 가상 컴퓨터.

