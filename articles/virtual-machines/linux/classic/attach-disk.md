---
title: "Azure의 Linux VM에 디스크 연결 | Microsoft Docs"
description: "클래식 배포 모델을 사용하여 Linux VM에 데이터 디스크를 연결하고 디스크를 사용 가능하도록 초기화하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4901384d-2a6f-4f46-bba0-337a348b7f87
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 017ba7197e11c2b222082833d5acabb9e542b762
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-attach-a-data-disk-to-a-linux-virtual-machine"></a><span data-ttu-id="ff9e9-103">Linux 가상 컴퓨터에 데이터 디스크를 연결하는 방법</span><span class="sxs-lookup"><span data-stu-id="ff9e9-103">How to Attach a Data Disk to a Linux Virtual Machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="ff9e9-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ff9e9-105">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="ff9e9-106">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="ff9e9-107">[리소스 관리자 배포 모델을 사용하여 데이터 디스크를 연결](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)하는 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-107">See how to [attach a data disk using the Resource Manager deployment model](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="ff9e9-108">빈 디스크와 데이터가 포함된 디스크를 모두 Azure VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-108">You can attach both empty disks and disks that contain data to your Azure VMs.</span></span> <span data-ttu-id="ff9e9-109">두 유형의 디스크 모두 Azure Storage 계정에 상주하는 .vhd 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-109">Both types of disks are .vhd files that reside in an Azure storage account.</span></span> <span data-ttu-id="ff9e9-110">Linux 컴퓨터에 디스크를 추가하는 것처럼 디스크를 연결한 후에는 사용할 준비를 하기 위해 디스크를 초기화하고 포맷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-110">As with adding any disk to a Linux machine, after you attach the disk you need to initialize and format it so it's ready for use.</span></span> <span data-ttu-id="ff9e9-111">이 문서에서는 새 디스크를 초기화하고 포맷하는 방법뿐만 아니라 빈 디스크와 이미 데이터가 있는 디스크를 모두 VM에 연결하는 방법에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-111">This article details attaching both empty disks and disks already containing data to your VMs, as well as how to then initialize and format a new disk.</span></span>

> [!NOTE]
> <span data-ttu-id="ff9e9-112">모범 사례는 별도 디스크를 하나 이상 사용하여 가상 컴퓨터의 데이터를 저장하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-112">It's a best practice to use one or more separate disks to store a virtual machine's data.</span></span> <span data-ttu-id="ff9e9-113">Azure 가상 컴퓨터를 만들면 운영 체제 디스크와 임시 디스크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-113">When you create an Azure virtual machine, it has an operating system disk and a temporary disk.</span></span> <span data-ttu-id="ff9e9-114">**임시 디스크를 사용하여 영구 데이터를 저장하지 마세요.**</span><span class="sxs-lookup"><span data-stu-id="ff9e9-114">**Do not use the temporary disk to store persistent data.**</span></span> <span data-ttu-id="ff9e9-115">이름이 의미하는 것과 같이 D 드라이브는 임시 저장소만 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-115">As the name implies, it provides temporary storage only.</span></span> <span data-ttu-id="ff9e9-116">Azure 저장소에 상주하지 않으므로 중복성이나 백업을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-116">It offers no redundancy or backup because it doesn't reside in Azure storage.</span></span>
> <span data-ttu-id="ff9e9-117">임시 디스크는 일반적으로 Azure Linux 에이전트에 의해 관리되며 **/mnt/resource**(또는 Ubuntu 이미지의 **/mnt**)에 자동으로 탑재됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-117">The temporary disk is typically managed by the Azure Linux Agent and automatically mounted to **/mnt/resource** (or **/mnt** on Ubuntu images).</span></span> <span data-ttu-id="ff9e9-118">반면, 데이터 디스크 이름은 Linux 커널에서 `/dev/sdc`와 같이 지정될 수 있으며 사용자가 이 리소스를 분할, 포맷 및 탑재해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-118">On the other hand, a data disk might be named by the Linux kernel something like `/dev/sdc`, and you need to partition, format, and mount this resource.</span></span> <span data-ttu-id="ff9e9-119">자세한 내용은 [Azure Linux 에이전트 사용자 가이드][Agent]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-119">See the [Azure Linux Agent User Guide][Agent] for details.</span></span>
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a><span data-ttu-id="ff9e9-120">Linux에서 새 데이터 디스크 초기화</span><span class="sxs-lookup"><span data-stu-id="ff9e9-120">Initialize a new data disk in Linux</span></span>
1. <span data-ttu-id="ff9e9-121">VM에 SSH를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-121">SSH to your VM.</span></span> <span data-ttu-id="ff9e9-122">자세한 내용은 [Linux를 실행하는 가상 컴퓨터에 로그온하는 방법][Logon]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-122">For more information, see [How to log on to a virtual machine running Linux][Logon].</span></span>
2. <span data-ttu-id="ff9e9-123">이제 초기화할 데이터 디스크의 장치 식별자를 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-123">Next you need to find the device identifier for the data disk to initialize.</span></span> <span data-ttu-id="ff9e9-124">이 작업을 수행하는 방법에는 다음 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-124">There are two ways to do that:</span></span>
   
    <span data-ttu-id="ff9e9-125">a) 다음 명령과 같이 로그에서 SCSI 장치를 grep합니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-125">a) Grep for SCSI devices in the logs, such as in the following command:</span></span>
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    <span data-ttu-id="ff9e9-126">최근 Ubuntu 배포의 경우 `/var/log/messages`에 대한 로깅이 기본적으로 사용하지 않도록 설정될 수 있으므로 `sudo grep SCSI /var/log/syslog`를 사용해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-126">For recent Ubuntu distributions, you may need to use `sudo grep SCSI /var/log/syslog` because logging to `/var/log/messages` might be disabled by default.</span></span>
   
    <span data-ttu-id="ff9e9-127">표시되는 메시지에서 추가된 마지막 데이터 디스크의 식별자를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-127">You can find the identifier of the last data disk that was added in the messages that are displayed.</span></span>
   
    ![디스크 메시지 가져오기](./media/attach-disk/scsidisklog.png)
   
    <span data-ttu-id="ff9e9-129">또는</span><span class="sxs-lookup"><span data-stu-id="ff9e9-129">OR</span></span>
   
    <span data-ttu-id="ff9e9-130">b) `lsscsi` 명령을 사용하여 장치 ID를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-130">b) Use the `lsscsi` command to find out the device id.</span></span> <span data-ttu-id="ff9e9-131">`lsscsi`는 `yum install lsscsi`(Red Hat 기반 배포) 또는 `apt-get install lsscsi`(Debian 기반 배포)를 통해 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-131">`lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="ff9e9-132">*lun* , 즉 **논리 단위 번호**를 사용하여 원하는 디스크를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-132">You can find the disk you are looking for by its *lun* or **logical unit number**.</span></span> <span data-ttu-id="ff9e9-133">예를 들어 연결한 디스크의 *lun*은 `azure vm disk list <virtual-machine>`에서 다음과 같이 쉽게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-133">For example, the *lun* for the disks you attached can be easily seen from `azure vm disk list <virtual-machine>` as:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="ff9e9-134">다음과 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-134">The output is similar to the following:</span></span>

    ```azurecli
    info:    Executing command vm disk list
    + Fetching disk images
    + Getting virtual machines
    + Getting VM disks
    data:    Lun  Size(GB)  Blob-Name                         OS
    data:    ---  --------  --------------------------------  -----
    data:         30        myVM-2645b8030676c8f8.vhd  Linux
    data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
    info:    vm disk list command OK
    ```
   
    <span data-ttu-id="ff9e9-135">이 데이터를 동일한 샘플 가상 컴퓨터에 대한 `lsscsi` 출력과 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-135">Compare this data with the output of `lsscsi` for the same sample virtual machine:</span></span>
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    <span data-ttu-id="ff9e9-136">각 행의 튜플에 있는 마지막 숫자는 *lun*입니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-136">The last number in the tuple in each row is the *lun*.</span></span> <span data-ttu-id="ff9e9-137">자세한 내용은 `man lsscsi`를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-137">See `man lsscsi` for more information.</span></span>
3. <span data-ttu-id="ff9e9-138">프롬프트에서 다음 명령을 입력하여 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-138">At the prompt, type the following command to create your device:</span></span>
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. <span data-ttu-id="ff9e9-139">메시지가 나타나면 입력  **n**  파티션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-139">When prompted, type **n** to create a partition.</span></span>

    ![장치 만들기](./media/attach-disk/fdisknewpartition.png)

5. <span data-ttu-id="ff9e9-141">프롬프트가 표시되면 **p** 를 입력하여 파티션을 주 파티션으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-141">When prompted, type **p** to make the partition the primary partition.</span></span> <span data-ttu-id="ff9e9-142">**1** 을 입력하여 첫 번째 파티션으로 설정한 다음 Enter 키를 입력하여 실린더에 대한 기본값을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-142">Type **1** to make it the first partition, and then type enter to accept the default value for the cylinder.</span></span> <span data-ttu-id="ff9e9-143">일부 시스템에서 실린더 대신 첫 번째 및 마지막 섹터의 기본값이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-143">On some systems, it can show the default values of the first and the last sectors, instead of the cylinder.</span></span> <span data-ttu-id="ff9e9-144">이러한 기본값을 수락하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-144">You can choose to accept these defaults.</span></span>

    ![파티션 만들기](./media/attach-disk/fdisknewpartdetails.png)


6. <span data-ttu-id="ff9e9-146">**p** 를 입력하여 분할되는 디스크에 대한 세부 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-146">Type **p** to see the details about the disk that is being partitioned.</span></span>

    ![디스크 정보 나열](./media/attach-disk/fdiskpartitiondetails.png)


7. <span data-ttu-id="ff9e9-148">**w** 를 입력하여 디스크에 대한 설정을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-148">Type **w** to write the settings for the disk.</span></span>

    ![디스크 변경 내용 쓰기](./media/attach-disk/fdiskwritedisk.png)

8. <span data-ttu-id="ff9e9-150">이제 새 파티션에 파일 시스템을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-150">Now you can create the file system on the new partition.</span></span> <span data-ttu-id="ff9e9-151">장치 ID에 파티션 번호를 추가합니다(다음 예제에서는 `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="ff9e9-151">Append the partition number to the device ID (in the following example `/dev/sdc1`).</span></span> <span data-ttu-id="ff9e9-152">다음 예제에서는 /dev/sdc1에 ext4 파티션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-152">The following example creates an ext4 partition on /dev/sdc1:</span></span>
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![파일 시스템 만들기](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > <span data-ttu-id="ff9e9-154">SuSE Linux Enterprise 11 시스템에서는 ext4 파일 시스템에 대해 읽기 전용 권한만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-154">SuSE Linux Enterprise 11 systems only support read-only access for ext4 file systems.</span></span> <span data-ttu-id="ff9e9-155">이 시스템에서 새 파일 시스템 형식을 ext4 대신 ext3으로 지정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-155">For these systems, it is recommended to format the new file system as ext3 rather than ext4.</span></span>

9. <span data-ttu-id="ff9e9-156">다음과 같이 새 파일 시스템을 탑재할 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-156">Make a directory to mount the new file system, as follows:</span></span>
   
    ```bash
    sudo mkdir /datadrive
    ```

10. <span data-ttu-id="ff9e9-157">마지막으로 다음과 같이 드라이브를 탑재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-157">Finally you can mount the drive, as follows:</span></span>
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    <span data-ttu-id="ff9e9-158">이제 데이터 디스크를 **/datadrive**로 사용할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-158">The data disk is now ready to use as **/datadrive**.</span></span>
   
    ![디렉터리를 만들고 디스크를 탑재](./media/attach-disk/mkdirandmount.png)

11. <span data-ttu-id="ff9e9-160">/etc/fstab에 새 드라이브를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-160">Add the new drive to /etc/fstab:</span></span>
   
    <span data-ttu-id="ff9e9-161">다시 부팅 후 드라이브가 자동으로 다시 탑재되도록 하려면 /etc/fstab 파일에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-161">To ensure the drive is remounted automatically after a reboot it must be added to the /etc/fstab file.</span></span> <span data-ttu-id="ff9e9-162">또한 /etc/fstab에 UUID(Universally Unique IDentifier)를 사용하여 장치 이름(즉, /dev/sdc1) 대신 드라이브를 가리키는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-162">In addition, it is highly recommended that the UUID (Universally Unique IDentifier) is used in /etc/fstab to refer to the drive rather than just the device name (i.e. /dev/sdc1).</span></span> <span data-ttu-id="ff9e9-163">UUID를 사용하면 운영 체제에서 부팅하는 동안 디스크 오류를 감지하므로 올바르지 않은 디스크가 지정된 위치에 탑재되지 않으며 나머지 데이터 디스크는 해당 장치 ID에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-163">Using the UUID avoids the incorrect disk being mounted to a given location if the OS detects a disk error during boot and any remaining data disks then being assigned those device IDs.</span></span> <span data-ttu-id="ff9e9-164">새 드라이브의 UUID를 찾으려면 **blkid** 유틸리티를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-164">To find the UUID of the new drive, you can use the **blkid** utility:</span></span>
   
    ```bash
    sudo -i blkid
    ```
   
    <span data-ttu-id="ff9e9-165">출력은 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-165">The output looks similar to the following example:</span></span>
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > <span data-ttu-id="ff9e9-166">**/etc/fstab** 파일을 부적절하게 편집하면 부팅할 수 없는 시스템이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-166">Improperly editing the **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="ff9e9-167">확실하지 않은 경우 배포 설명서에서 이 파일을 제대로 편집하는 방법에 대한 자세한 내용을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-167">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="ff9e9-168">또한 편집하기 전에 /etc/fstab 파일의 백업을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-168">It is also recommended that a backup of the /etc/fstab file is created before editing.</span></span>

    <span data-ttu-id="ff9e9-169">다음으로, 텍스트 편집기에서 **/etc/fstab** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-169">Next, open the **/etc/fstab** file in a text editor:</span></span>

    ```bash
    sudo vi /etc/fstab
    ```

    <span data-ttu-id="ff9e9-170">이 예제에서는 이전 단계에서 만든 새 **/dev/sdc1** 장치의 UUID 값과 탑재 지점 **/datadrive**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-170">In this example, we use the UUID value for the new **/dev/sdc1** device that was created in the previous steps, and the mountpoint **/datadrive**.</span></span> <span data-ttu-id="ff9e9-171">**/etc/fstab** 파일의 끝에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-171">Add the following line to the end of the **/etc/fstab** file:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    <span data-ttu-id="ff9e9-172">또는 SuSE Linux 기반 시스템에서는 약간 다른 형식을 사용해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-172">Or, on systems based on SuSE Linux you may need to use a slightly different format:</span></span>

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > <span data-ttu-id="ff9e9-173">`nofail` 옵션은 파일 시스템이 손상되었거나 디스크가 부팅 시 존재하지 않더라도 VM이 시작되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-173">The `nofail` option ensures that the VM starts even if the filesystem is corrupt or the disk does not exist at boot time.</span></span> <span data-ttu-id="ff9e9-174">이 옵션이 없으면 [FSTAB 오류로 인해 Linux에 SSH를 사용할 수 없음](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)(영문)에 설명되어 있는 동작이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-174">Without this option, you may encounter behavior as described in [Cannot SSH to Linux VM due to FSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span></span>

    <span data-ttu-id="ff9e9-175">파일 시스템을 탑재 해제했다가 다시 탑재하여 파일 시스템이 제대로 탑재되었는지 테스트할 수 있습니다. 예를 들면</span><span class="sxs-lookup"><span data-stu-id="ff9e9-175">You can now test that the file system is mounted properly by unmounting and then remounting the file system, i.e.</span></span> <span data-ttu-id="ff9e9-176">이전 단계에서 만든 예제 탑재 지점 `/datadrive`를 사용하여 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-176">using the example mount point `/datadrive` created in the earlier steps:</span></span>

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    <span data-ttu-id="ff9e9-177">`mount` 명령에서 오류가 발생하는 경우 /etc/fstab 파일에서 구문이 올바른지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-177">If the `mount` command produces an error, check the /etc/fstab file for correct syntax.</span></span> <span data-ttu-id="ff9e9-178">추가 데이터 드라이브 또는 파티션을 만든 경우에는 /etc/fstab에 해당 드라이브나 파티션도 별도로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-178">If additional data drives or partitions are created, enter them into /etc/fstab separately as well.</span></span>

    <span data-ttu-id="ff9e9-179">다음 명령을 사용하여 드라이브를 쓰기 가능하게 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-179">Make the drive writable by using this command:</span></span>

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > <span data-ttu-id="ff9e9-180">이후에 fstab을 편집하지 않고 데이터 디스크를 제거하면 VM이 부팅되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-180">Subsequently removing a data disk without editing fstab could cause the VM to fail to boot.</span></span> <span data-ttu-id="ff9e9-181">이런 경우가 자주 발생하면 대부분의 배포에서 디스크가 부팅 시 탑재되지 않더라도 시스템이 부팅되도록 하는 `nofail` 및/또는 `nobootwait` fstab 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-181">If this is a common occurrence, most distributions provide either the `nofail` and/or `nobootwait` fstab options that allow a system to boot even if the disk fails to mount at boot time.</span></span> <span data-ttu-id="ff9e9-182">이러한 매개 변수에 대한 자세한 내용은 배포 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-182">Consult your distribution's documentation for more information on these parameters.</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="ff9e9-183">Azure에서 Linux에 대한 TRIM/UNMAP 지원</span><span class="sxs-lookup"><span data-stu-id="ff9e9-183">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="ff9e9-184">일부 Linux 커널은 디스크에서 사용되지 않은 블록을 버릴 수 있도록 TRIM/UNMAP 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-184">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="ff9e9-185">이러한 작업은 Azure에 삭제된 페이지가 더 이상 유효하지 않으며 폐기될 수 있음을 알리는 데 표준 저장소에서 주로 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-185">These operations are primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="ff9e9-186">큰 파일을 만들고 삭제하는 경우 페이지를 삭제하여 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-186">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="ff9e9-187">Linux VM에서 TRIM 지원을 사용하는 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-187">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="ff9e9-188">평소와 같이 권장되는 방법에 대해 배포에 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-188">As usual, consult your distribution for the recommended approach:</span></span>

* <span data-ttu-id="ff9e9-189">`/etc/fstab`에 `discard` 탑재 옵션을 사용합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="ff9e9-189">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```

* <span data-ttu-id="ff9e9-190">일부 경우 `discard` 옵션에는 성능이 저하 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-190">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="ff9e9-191">또는 `fstrim` 명령을 명령줄에서 수동으로 실행하거나, 또는 정기적으로 실행하기 위해 crontab에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-191">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>
  
    <span data-ttu-id="ff9e9-192">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="ff9e9-192">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="ff9e9-193">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="ff9e9-193">**RHEL/CentOS**</span></span>
  
    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="ff9e9-194">문제 해결</span><span class="sxs-lookup"><span data-stu-id="ff9e9-194">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="ff9e9-195">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ff9e9-195">Next Steps</span></span>
<span data-ttu-id="ff9e9-196">다음 문서에서 Linux VM을 사용하는 방법을 읽어볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff9e9-196">You can read more about using your Linux VM in the following articles:</span></span>

* <span data-ttu-id="ff9e9-197">[Linux를 실행하는 가상 컴퓨터에 로그온하는 방법][Logon]</span><span class="sxs-lookup"><span data-stu-id="ff9e9-197">[How to log on to a virtual machine running Linux][Logon]</span></span>
* [<span data-ttu-id="ff9e9-198">Linux 가상 컴퓨터에서 디스크를 분리하는 방법</span><span class="sxs-lookup"><span data-stu-id="ff9e9-198">How to detach a disk from a Linux virtual machine</span></span>](detach-disk.md)
* [<span data-ttu-id="ff9e9-199">클래식 배포 모델에서 Azure CLI 사용</span><span class="sxs-lookup"><span data-stu-id="ff9e9-199">Using the Azure CLI with the Classic deployment model</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="ff9e9-200">Azure에서 Linux VM에 RAID 구성</span><span class="sxs-lookup"><span data-stu-id="ff9e9-200">Configure RAID on a Linux VM in Azure</span></span>](../configure-raid.md)
* [<span data-ttu-id="ff9e9-201">Azure에서 Linux VM에 LVM 구성</span><span class="sxs-lookup"><span data-stu-id="ff9e9-201">Configure LVM on a Linux VM in Azure</span></span>](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
