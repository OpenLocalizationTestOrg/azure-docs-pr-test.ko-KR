<span data-ttu-id="9088d-101">연결 된 tooa 가상 컴퓨터 (VM) 되는 데이터 디스크를 더 이상 해야 하는 경우 쉽게 분리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9088d-101">When you no longer need a data disk that's attached tooa virtual machine (VM), you can easily detach it.</span></span> <span data-ttu-id="9088d-102">Hello VM에서에서 디스크를 분리 하는 경우 hello 디스크가 없는 저장소에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="9088d-102">When you detach a disk from hello VM, hello disk is not removed it from storage.</span></span> <span data-ttu-id="9088d-103">Hello toouse hello 디스크에 기존 데이터를 다시 선택 하면 다시 연결할 수 toohello 동일한 VM 이거나 다른 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="9088d-103">If you want toouse hello existing data on hello disk again, you can reattach it toohello same VM, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="9088d-104">Azure의 VM은 운영 체제 디스크, 로컬 임시 디스크, 선택적 데이터 디스크 등 다양한 유형의 디스크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9088d-104">A VM in Azure uses different types of disks - an operating system disk, a local temporary disk, and optional data disks.</span></span> <span data-ttu-id="9088d-105">자세한 내용은 [Virtual Machines용 디스크 및 VHD 정보](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9088d-105">For details, see [About Disks and VHDs for Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="9088d-106">또한 hello VM을 삭제 하지 않는 한 운영 체제 디스크를 분리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9088d-106">You cannot detach an operating system disk unless you also delete hello VM.</span></span>

## <a name="find-hello-disk"></a><span data-ttu-id="9088d-107">Hello 디스크 찾기</span><span class="sxs-lookup"><span data-stu-id="9088d-107">Find hello disk</span></span>
<span data-ttu-id="9088d-108">VM에서 디스크를 분리 하려면 먼저 toofind hello hello 디스크 toobe 분리에 대 한 식별자 LUN 번호를 아웃 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9088d-108">Before you can detach a disk from a VM you need toofind out hello LUN number, which is an identifier for hello disk toobe detached.</span></span> <span data-ttu-id="9088d-109">다음이 단계를 수행 하는 toodo:</span><span class="sxs-lookup"><span data-stu-id="9088d-109">toodo that, follow these steps:</span></span>

1. <span data-ttu-id="9088d-110">Azure CLI를 열고 및 [tooyour Azure 구독 연결](../articles/xplat-cli-connect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9088d-110">Open Azure CLI and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="9088d-111">Azure 서비스 관리 모드(`azure config mode asm`)에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9088d-111">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="9088d-112">있는 디스크를 연결 된 tooyour VM에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9088d-112">Find out which disks are attached tooyour VM.</span></span> <span data-ttu-id="9088d-113">hello 다음 예에서는 나열 hello 라는 VM에 대 한 디스크 `myVM`:</span><span class="sxs-lookup"><span data-stu-id="9088d-113">hello following example lists disks for hello VM named `myVM`:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="9088d-114">hello 비슷한 toohello 다음은 예제 출력:</span><span class="sxs-lookup"><span data-stu-id="9088d-114">hello output is similar toohello following example:</span></span>

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

3. <span data-ttu-id="9088d-115">Hello LUN 또는 hello **논리 단위 번호** toodetach hello 디스크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9088d-115">Note hello LUN or hello **logical unit number** for hello disk that you want toodetach.</span></span>

## <a name="remove-operating-system-references-toohello-disk"></a><span data-ttu-id="9088d-116">운영 체제 참조 toohello 디스크 제거</span><span class="sxs-lookup"><span data-stu-id="9088d-116">Remove operating system references toohello disk</span></span>
<span data-ttu-id="9088d-117">Hello Linux 게스트에서 hello 디스크를 분리 하기 전에 hello 디스크의 모든 파티션을 사용 하지 않는 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9088d-117">Before detaching hello disk from hello Linux guest, you should make sure that all partitions on hello disk are not in use.</span></span> <span data-ttu-id="9088d-118">해당 hello 운영 체제 tooremount 시도 하지 않습니다 확인 후 다시 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="9088d-118">Ensure that hello operating system does not attempt tooremount them after a reboot.</span></span> <span data-ttu-id="9088d-119">다음이 단계 실행 시기 만들었을 것 hello 구성 취소 [연결](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) hello 디스크.</span><span class="sxs-lookup"><span data-stu-id="9088d-119">These steps undo hello configuration you likely created when [attaching](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) hello disk.</span></span>

1. <span data-ttu-id="9088d-120">사용 하 여 hello `lsscsi` 명령 toodiscover hello 디스크 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="9088d-120">Use hello `lsscsi` command toodiscover hello disk identifier.</span></span> <span data-ttu-id="9088d-121">`lsscsi`는 `yum install lsscsi`(Red Hat 기반 배포) 또는 `apt-get install lsscsi`(Debian 기반 배포)를 통해 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9088d-121">`lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="9088d-122">Hello LUN 번호를 사용 하 여 원하는 hello 디스크 식별자를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9088d-122">You can find hello disk identifier you are looking for by using hello LUN number.</span></span> <span data-ttu-id="9088d-123">각 행에 hello 튜플에 hello 마지막 번호는 hello LUN입니다.</span><span class="sxs-lookup"><span data-stu-id="9088d-123">hello last number in hello tuple in each row is hello LUN.</span></span> <span data-ttu-id="9088d-124">다음 예제에서 hello에 `lsscsi`, LUN 0에 매핑합니다 너무  */개발/sdc*</span><span class="sxs-lookup"><span data-stu-id="9088d-124">In hello following example from `lsscsi`, LUN 0 maps too*/dev/sdc*</span></span>

    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```

2. <span data-ttu-id="9088d-125">사용 하 여 `fdisk -l <disk>` hello 디스크 toobe 분리와 연결 된 toodiscover hello 파티션 합니다.</span><span class="sxs-lookup"><span data-stu-id="9088d-125">Use `fdisk -l <disk>` toodiscover hello partitions associated with hello disk toobe detached.</span></span> <span data-ttu-id="9088d-126">hello 다음 보여 주는 예제에 대 한 hello 출력 `/dev/sdc`:</span><span class="sxs-lookup"><span data-stu-id="9088d-126">hello following example shows hello output for `/dev/sdc`:</span></span>

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

3. <span data-ttu-id="9088d-127">Hello 디스크에 대해 나열 된 각 파티션에 탑재 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="9088d-127">Unmount each partition listed for hello disk.</span></span> <span data-ttu-id="9088d-128">hello 다음 예제에서는 분리 `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="9088d-128">hello following example unmounts `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

4. <span data-ttu-id="9088d-129">사용 하 여 hello `blkid` 모든 파티션에 대 한 명령 toodiscovery hello Uuid입니다.</span><span class="sxs-lookup"><span data-stu-id="9088d-129">Use hello `blkid` command toodiscovery hello UUIDs for all partitions.</span></span> <span data-ttu-id="9088d-130">hello 비슷한 toohello 다음은 예제 출력:</span><span class="sxs-lookup"><span data-stu-id="9088d-130">hello output is similar toohello following example:</span></span>

    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

5. <span data-ttu-id="9088d-131">Hello에서 항목을 제거할 **/등/fstab** hello 디스크 toobe 분리에 대 한 모든 파티션에 대 한 hello 장치 경로 또는 Uuid와 연결 된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9088d-131">Remove entries in hello **/etc/fstab** file associated with either hello device paths or UUIDs for all partitions for hello disk toobe detached.</span></span>  <span data-ttu-id="9088d-132">이 예제에서는 해당 항목이 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9088d-132">Entries for this example might be:</span></span>

    ```sh  
   UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults   1   2
   ```

    <span data-ttu-id="9088d-133">또는</span><span class="sxs-lookup"><span data-stu-id="9088d-133">or</span></span>
   
   ```sh   
   /dev/sdc1   /datadrive   ext4   defaults   1   2
   ```

## <a name="detach-hello-disk"></a><span data-ttu-id="9088d-134">Hello 디스크를 분리</span><span class="sxs-lookup"><span data-stu-id="9088d-134">Detach hello disk</span></span>
<span data-ttu-id="9088d-135">준비 toodetach 하는 hello 디스크 및 운영 체제 참조 제거 hello의 hello LUN 번호를 찾은 다음 해당:</span><span class="sxs-lookup"><span data-stu-id="9088d-135">After you find hello LUN number of hello disk and removed hello operating system references, you're ready toodetach it:</span></span>

1. <span data-ttu-id="9088d-136">Hello 명령을 실행 하 여 hello 가상 컴퓨터에서 hello 선택한 디스크를 분리 `azure vm disk detach
   <virtual-machine-name> <LUN>`합니다.</span><span class="sxs-lookup"><span data-stu-id="9088d-136">Detach hello selected disk from hello virtual machine by running hello command `azure vm disk detach
<virtual-machine-name> <LUN>`.</span></span> <span data-ttu-id="9088d-137">hello 다음 예제에서는 분리 LUN `0` hello 라는 VM에서에서 `myVM`:</span><span class="sxs-lookup"><span data-stu-id="9088d-137">hello following example detaches LUN `0` from hello VM named `myVM`:</span></span>
   
    ```azurecli
    azure vm disk detach myVM 0
    ```

2. <span data-ttu-id="9088d-138">실행 하 여 hello 디스크 분리 가져온 경우를 확인할 수 있습니다 `azure vm disk list` 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9088d-138">You can check if hello disk got detached by running `azure vm disk list` again.</span></span> <span data-ttu-id="9088d-139">다음 예제에서는 hello hello 라는 VM `myVM`:</span><span class="sxs-lookup"><span data-stu-id="9088d-139">hello following example checks hello VM named `myVM`:</span></span>
   
    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="9088d-140">hello는 비슷한 toohello 다음 hello 데이터 디스크 연결 끊은 보여 주는 예제 출력:</span><span class="sxs-lookup"><span data-stu-id="9088d-140">hello output is similar toohello following example, which shows hello data disk is no longer attached:</span></span>

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

<span data-ttu-id="9088d-141">분리 hello 디스크 저장소에 남아 있지만 더 이상 tooa 연결 된 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="9088d-141">hello detached disk remains in storage but is no longer attached tooa virtual machine.</span></span>

