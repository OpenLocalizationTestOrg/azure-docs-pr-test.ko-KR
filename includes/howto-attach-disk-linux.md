
디스크에 대한 자세한 내용은 [Virtual Machines용 디스크 및 VHD 정보](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.

<a id="attachempty"></a>

## <a name="attach-an-empty-disk"></a>빈 디스크 연결
1. Azure CLI 1.0을 열려면 및 [tooyour Azure 구독 연결](../articles/xplat-cli-connect.md)합니다. Azure 서비스 관리 모드(`azure config mode asm`)에 있는지 확인합니다.
2. 입력 `azure vm disk attach-new` toocreate hello 다음 예제와 같이 새 디스크를 연결 합니다. 대체 *myVM* Linux 가상 컴퓨터의 hello 이름의 hello 디스크의 hello 크기 GB로 지정 하 고 *100GB* 이 예에서:

    ```azurecli
    azure vm disk attach-new myVM 100
    ```

3. hello 출력에 표시 되며 hello 데이터 디스크를 만들고 연결 된 후 `azure vm disk list <virtual-machine-name>` hello 다음 예제와 같이:
   
    ```azurecli
    azure vm disk list TestVM
    ```

    hello 비슷한 toohello 다음은 예제 출력:

    ```bash
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        myVM-2645b8030676c8f8.vhd  Linux
     data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

<a id="attachexisting"></a>

## <a name="attach-an-existing-disk"></a>기존 디스크 연결
기존 디스크를 연결하려면 저장소 계정에 사용 가능한 .vhd가 있어야 합니다.

1. Azure CLI 1.0을 열려면 및 [tooyour Azure 구독 연결](../articles/xplat-cli-connect.md)합니다. Azure 서비스 관리 모드(`azure config mode asm`)에 있는지 확인합니다.
2. Hello tooattach가 이미 원하는 VHD 업로드 tooyour Azure 구독을 확인 합니다.
   
    ```azurecli
    azure vm disk list
    ```

    hello 비슷한 toohello 다음은 예제 출력:

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
     data:    Name                                          OS
     data:    --------------------------------------------  -----
     data:    myTestVhd                                     Linux
     data:    TestVM-ubuntuVMasm-0-201508060029150744  Linux
     data:    TestVM-ubuntuVMasm-0-201508060040530369
     info:    vm disk list command OK
    ```

3. Hello 디스크를 찾지 못한 경우 원하는 toouse, 사용 하 여 로컬 VHD tooyour 구독을 업로드할 수 있습니다 `azure vm disk create` 또는 `azure vm disk upload`합니다. 예로 `disk create` hello 다음 예제와 같이 됩니다.
   
    ```azurecli
    azure vm disk create myVhd .\TempDisk\test.VHD -l "East US" -o Linux
    ```

    hello 비슷한 toohello 다음은 예제 출력:

    ```azurecli
    info:    Executing command vm disk create
    + Retrieving storage accounts
    info:    VHD size : 10 GB
    info:    Uploading 10485760.5 KB
    Requested:100.0% Completed:100.0% Running:   0 Time:   25s Speed:    82 KB/s
    info:    Finishing computing MD5 hash, 16% is complete.
    info:    https://mystorageaccount.blob.core.windows.net/disks/myVHD.vhd was
    uploaded successfully
    info:    vm disk create command OK
    ```
   
   사용할 수 있습니다 `azure vm disk upload` tooupload VHD tooa 특정 저장소 계정입니다. Azure 가상 컴퓨터 데이터 디스크 toomanage 명령을 hello에 대 한 자세한 읽기 [여기](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)합니다.

4. 연결한 이제 hello 원하는 VHD tooyour 가상 컴퓨터:
   
    ```azurecli
    azure vm disk attach myVM myVhd
    ```
   
   있는지 tooreplace 확인 *myVM* 가상 컴퓨터의 hello 이름의 및 *myVHD* 원하는 VHD와 합니다.

5. Hello 디스크가 연결 된 toohello 가상 컴퓨터를 확인할 수 있습니다 `azure vm disk list <virtual-machine-name>`:
   
    ```azurecli
    azure vm disk list myVM
    ```

    hello 비슷한 toohello 다음은 예제 출력:

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        TestVM-2645b8030676c8f8.vhd  Linux
     data:    1    10        test.VHD
     data:    0    100        TestVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

> [!NOTE]
> 데이터 디스크를 추가한 후 toolog toohello 가상 컴퓨터에 필요 하 고 hello 가상 컴퓨터 저장소에 대 한 hello 디스크를 사용할 수 있도록 hello 디스크를 초기화 합니다 (다음 hello toodo hello 디스크를 초기화 하는 방법에 자세한 내용은 단계 참조).
> 
> 

