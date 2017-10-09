<span data-ttu-id="28e6d-101">데이터 디스크 tooa Linux VM을 추가할 때 디스크 LUN 0에 존재 하지 않는 경우 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28e6d-101">When adding data disks tooa Linux VM, you may encounter errors if a disk does not exist at LUN 0.</span></span> <span data-ttu-id="28e6d-102">Hello를 사용 하 여 수동으로 디스크를 추가 하는 경우 `azure vm disk attach-new` 명령을 지정할 LUN (`--lun`) hello를 허용 하는 대신 Azure 플랫폼 toodetermine 적절 한 LUN hello, 주의 해야 하는 디스크 이미 존재 / LUN 0에 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e6d-102">If you are adding a disk manually using hello `azure vm disk attach-new` command and you specify a LUN (`--lun`) rather than allowing hello Azure platform toodetermine hello appropriate LUN, take care that a disk already exists / will exist at LUN 0.</span></span> 

<span data-ttu-id="28e6d-103">다음 코드 조각을 hello 출력을 보여 주는 예제는 hello 고려 `lsscsi`:</span><span class="sxs-lookup"><span data-stu-id="28e6d-103">Consider hello following example showing a snippet of hello output from `lsscsi`:</span></span>

```bash
[5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc 
[5:0:0:1]    disk    Msft     Virtual Disk     1.0   /dev/sdd 
```

<span data-ttu-id="28e6d-104">hello 두 개의 데이터 디스크 LUN 0 및 LUN 1에 있는 (hello의 첫 번째 열 hello `lsscsi` 출력 세부 사항 `[host:channel:target:lun]`).</span><span class="sxs-lookup"><span data-stu-id="28e6d-104">hello two data disks exist at LUN 0 and LUN 1 (hello first column in hello `lsscsi` output details `[host:channel:target:lun]`).</span></span> <span data-ttu-id="28e6d-105">양쪽 디스크가 모두 hello VM 내에서 accessbile 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e6d-105">Both disks should be accessbile from within hello VM.</span></span> <span data-ttu-id="28e6d-106">에 지정한 수동으로 hello 첫 번째 디스크 toobe LUN 1 및 LUN 2에 두 번째 디스크 hello에 추가 하는 경우 나타나지 않을 수 있습니다 hello 디스크에서 제대로 VM 내에서.</span><span class="sxs-lookup"><span data-stu-id="28e6d-106">If you had manually specified hello first disk toobe added at LUN 1 and hello second disk at LUN 2, you may not see hello disks correctly from within your VM.</span></span>

> [!NOTE]
> <span data-ttu-id="28e6d-107">Azure hello `host` 값은 다음 예에서 5 있지만 선택한 저장소의 hello 유형에 따라 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28e6d-107">hello Azure `host` value is 5 in these examples, but this may vary depending on hello type of storage you select.</span></span>
> 
> 

<span data-ttu-id="28e6d-108">Azure에 문제가 있지만 hello 방식으로 Linux는 hello 커널 hello SCSI 사양을 따릅니다.이 디스크 동작은 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="28e6d-108">This disk behavior is not an Azure problem, but hello way in which hello Linux kernel follows hello SCSI specifications.</span></span> <span data-ttu-id="28e6d-109">Hello Linux 커널을 hello SCSI 버스에 연결 된 장치가 검색 하는 경우 추가 장치에 대 한 검색 hello 시스템 toocontinue 되려면에서 LUN 0에는 장치를 찾을 수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e6d-109">When hello Linux kernel scans hello SCSI bus for attached devices, a device must be found at LUN 0 in order for hello system toocontinue scanning for additional devices.</span></span> <span data-ttu-id="28e6d-110">따라서 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e6d-110">As such:</span></span>

* <span data-ttu-id="28e6d-111">검토의 hello 출력 `lsscsi` LUN 0에가 디스크 데이터 디스크 tooverify를 추가한 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e6d-111">Review hello output of `lsscsi` after adding a data disk tooverify that you have a disk at LUN 0.</span></span>
* <span data-ttu-id="28e6d-112">디스크가 VM 내에서 올바르게 표시되지 않으면 디스크가 LUN 0에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="28e6d-112">If your disk does not show up correctly within your VM, verify a disk exists at LUN 0.</span></span>

