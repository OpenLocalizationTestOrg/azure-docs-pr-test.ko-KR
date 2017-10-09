---
title: "디스크 tooa Azure에서 Linux VM aaaAttach | Microsoft Docs"
description: "데이터 tooattach tooa Linux VM 디스크 하는 방법에 대해 알아봅니다 hello 클래식 배포를 사용 하 여 모델 및 사용 하기 위해 있도록 hello 디스크를 초기화 합니다."
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
ms.openlocfilehash: c76d8479ac2b522d2b6df658cd28f242473f30ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-virtual-machine"></a><span data-ttu-id="e40d7-103">어떻게 tooAttach 데이터 디스크 tooa Linux 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="e40d7-103">How tooAttach a Data Disk tooa Linux Virtual Machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="e40d7-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e40d7-105">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="e40d7-106">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="e40d7-107">너무 어떻게 참조[hello 리소스 관리자 배포 모델을 사용 하 여 데이터 디스크 연결](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-107">See how too[attach a data disk using hello Resource Manager deployment model](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="e40d7-108">빈 디스크와 데이터 tooyour Azure Vm을 포함 하는 디스크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-108">You can attach both empty disks and disks that contain data tooyour Azure VMs.</span></span> <span data-ttu-id="e40d7-109">두 유형의 디스크 모두 Azure Storage 계정에 상주하는 .vhd 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-109">Both types of disks are .vhd files that reside in an Azure storage account.</span></span> <span data-ttu-id="e40d7-110">으로 모든 디스크 tooa Linux 컴퓨터를 추가 하는 hello 디스크를 연결한 후를 사용할 때는 tooinitialize 필요를 사용 하기 위해 있도록 서식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-110">As with adding any disk tooa Linux machine, after you attach hello disk you need tooinitialize and format it so it's ready for use.</span></span> <span data-ttu-id="e40d7-111">이 문서를 세부 정보 빈 디스크와 toothen 초기화 하 고 새 디스크를 포맷 하는 방법에 따라 데이터 tooyour Vm에도 이미 포함 하는 디스크를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-111">This article details attaching both empty disks and disks already containing data tooyour VMs, as well as how toothen initialize and format a new disk.</span></span>

> [!NOTE]
> <span data-ttu-id="e40d7-112">하나는 모범 사례 toouse 나 가상 컴퓨터의 데이터 디스크 toostore 분리 더 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-112">It's a best practice toouse one or more separate disks toostore a virtual machine's data.</span></span> <span data-ttu-id="e40d7-113">Azure 가상 컴퓨터를 만들면 운영 체제 디스크와 임시 디스크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-113">When you create an Azure virtual machine, it has an operating system disk and a temporary disk.</span></span> <span data-ttu-id="e40d7-114">**Hello 임시 디스크 toostore 영구 데이터를 사용 하지 마십시오.**</span><span class="sxs-lookup"><span data-stu-id="e40d7-114">**Do not use hello temporary disk toostore persistent data.**</span></span> <span data-ttu-id="e40d7-115">Hello 이름에서 알 수 있듯이 임시 저장소만 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-115">As hello name implies, it provides temporary storage only.</span></span> <span data-ttu-id="e40d7-116">Azure 저장소에 상주하지 않으므로 중복성이나 백업을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-116">It offers no redundancy or backup because it doesn't reside in Azure storage.</span></span>
> <span data-ttu-id="e40d7-117">임시 디스크 hello hello Azure Linux 에이전트에서 일반적으로 관리 되 고 자동으로 너무 탑재**/mnt/리소스** (또는 **/mnt** Ubuntu 이미지에).</span><span class="sxs-lookup"><span data-stu-id="e40d7-117">hello temporary disk is typically managed by hello Azure Linux Agent and automatically mounted too**/mnt/resource** (or **/mnt** on Ubuntu images).</span></span> <span data-ttu-id="e40d7-118">Hello 반면에, 데이터 디스크 이름은 수 있습니다 hello Linux 커널에 의해 다음과 같이 `/dev/sdc`, toopartition, 필요한 서식을 지정 하 고이 리소스를 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-118">On hello other hand, a data disk might be named by hello Linux kernel something like `/dev/sdc`, and you need toopartition, format, and mount this resource.</span></span> <span data-ttu-id="e40d7-119">Hello 참조 [Azure Linux 에이전트 사용자 가이드] [ Agent] 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-119">See hello [Azure Linux Agent User Guide][Agent] for details.</span></span>
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a><span data-ttu-id="e40d7-120">Linux에서 새 데이터 디스크 초기화</span><span class="sxs-lookup"><span data-stu-id="e40d7-120">Initialize a new data disk in Linux</span></span>
1. <span data-ttu-id="e40d7-121">SSH tooyour VM입니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-121">SSH tooyour VM.</span></span> <span data-ttu-id="e40d7-122">자세한 내용은 참조 [어떻게 Linux를 실행 하는 tooa 가상 컴퓨터에서 toolog][Logon]합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-122">For more information, see [How toolog on tooa virtual machine running Linux][Logon].</span></span>
2. <span data-ttu-id="e40d7-123">그런 다음 toofind hello 장치 식별자 hello 데이터 디스크 tooinitialize 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-123">Next you need toofind hello device identifier for hello data disk tooinitialize.</span></span> <span data-ttu-id="e40d7-124">두 가지 방법으로 toodo입니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-124">There are two ways toodo that:</span></span>
   
    <span data-ttu-id="e40d7-125">a) Grep hello에 SCSI 장치에 대 한 로그, 다음 명령을 hello와 같이:</span><span class="sxs-lookup"><span data-stu-id="e40d7-125">a) Grep for SCSI devices in hello logs, such as in hello following command:</span></span>
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    <span data-ttu-id="e40d7-126">최근 Ubuntu 분포에 대 한 toouse 할 수 있습니다 `sudo grep SCSI /var/log/syslog` 너무 로그인 때문에`/var/log/messages` 기본적으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-126">For recent Ubuntu distributions, you may need toouse `sudo grep SCSI /var/log/syslog` because logging too`/var/log/messages` might be disabled by default.</span></span>
   
    <span data-ttu-id="e40d7-127">표시 되는 hello 메시지에 추가 된 hello 마지막 데이터 디스크의 hello 식별자를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-127">You can find hello identifier of hello last data disk that was added in hello messages that are displayed.</span></span>
   
    ![Hello 디스크 메시지 가져오기](./media/attach-disk/scsidisklog.png)
   
    <span data-ttu-id="e40d7-129">또는</span><span class="sxs-lookup"><span data-stu-id="e40d7-129">OR</span></span>
   
    <span data-ttu-id="e40d7-130">b) 사용 하 여 hello `lsscsi` hello 장치 id 아웃 toofind 명령입니다. `lsscsi` 방법으로 설치할 수 있습니다 `yum install lsscsi` (Red Hat 분포 기반) 또는 `apt-get install lsscsi` (Debian 분포 기반).</span><span class="sxs-lookup"><span data-stu-id="e40d7-130">b) Use hello `lsscsi` command toofind out hello device id. `lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="e40d7-131">원하는 hello 디스크를 찾을 수 있습니다는 *lun* 또는 **논리 단위 번호**합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-131">You can find hello disk you are looking for by its *lun* or **logical unit number**.</span></span> <span data-ttu-id="e40d7-132">예를 들어 hello *lun* 첨부 hello 디스크에서 쉽게 볼 수에 대 한 `azure vm disk list <virtual-machine>` 로:</span><span class="sxs-lookup"><span data-stu-id="e40d7-132">For example, hello *lun* for hello disks you attached can be easily seen from `azure vm disk list <virtual-machine>` as:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="e40d7-133">hello 출력은 toohello 다음과 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-133">hello output is similar toohello following:</span></span>

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
   
    <span data-ttu-id="e40d7-134">출력을 hello 사용 하 여이 데이터를 비교 `lsscsi` hello 동일 샘플 가상 컴퓨터:</span><span class="sxs-lookup"><span data-stu-id="e40d7-134">Compare this data with hello output of `lsscsi` for hello same sample virtual machine:</span></span>
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    <span data-ttu-id="e40d7-135">각 행에 hello 튜플에 hello 마지막 번호는 hello *lun*합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-135">hello last number in hello tuple in each row is hello *lun*.</span></span> <span data-ttu-id="e40d7-136">자세한 내용은 `man lsscsi`를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e40d7-136">See `man lsscsi` for more information.</span></span>
3. <span data-ttu-id="e40d7-137">Hello 프롬프트에서 다음 명령을 toocreate hello 장치를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-137">At hello prompt, type hello following command toocreate your device:</span></span>
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. <span data-ttu-id="e40d7-138">메시지가 나타나면 입력  **n**  toocreate 파티션 합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-138">When prompted, type **n** toocreate a partition.</span></span>

    ![장치 만들기](./media/attach-disk/fdisknewpartition.png)

5. <span data-ttu-id="e40d7-140">메시지가 나타나면 입력 **p** toomake hello 파티션 hello 주 파티션 합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-140">When prompted, type **p** toomake hello partition hello primary partition.</span></span> <span data-ttu-id="e40d7-141">형식 **1** 첫 번째 파티션에 hello 하 한 다음 입력 toomake 실린더 hello에 대 한 tooaccept hello 기본값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-141">Type **1** toomake it hello first partition, and then type enter tooaccept hello default value for hello cylinder.</span></span> <span data-ttu-id="e40d7-142">일부 시스템에서는 수의 hello hello 기본값을 첫 번째 표시 하 고 hello 실린더 대신 마지막 섹터 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-142">On some systems, it can show hello default values of hello first and hello last sectors, instead of hello cylinder.</span></span> <span data-ttu-id="e40d7-143">이러한 기본값 tooaccept를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-143">You can choose tooaccept these defaults.</span></span>

    ![파티션 만들기](./media/attach-disk/fdisknewpartdetails.png)


6. <span data-ttu-id="e40d7-145">형식 **p** 분할 되 고 된 hello 디스크에 대 한 toosee hello 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-145">Type **p** toosee hello details about hello disk that is being partitioned.</span></span>

    ![디스크 정보 나열](./media/attach-disk/fdiskpartitiondetails.png)


7. <span data-ttu-id="e40d7-147">형식 **w** hello 디스크에 대 한 toowrite hello 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-147">Type **w** toowrite hello settings for hello disk.</span></span>

    ![Hello 디스크 변경 기록](./media/attach-disk/fdiskwritedisk.png)

8. <span data-ttu-id="e40d7-149">이제 hello 새 파티션에 hello 파일 시스템을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-149">Now you can create hello file system on hello new partition.</span></span> <span data-ttu-id="e40d7-150">Hello 파티션 번호 toohello 장치 ID를 추가 (다음 예제는 hello에 `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="e40d7-150">Append hello partition number toohello device ID (in hello following example `/dev/sdc1`).</span></span> <span data-ttu-id="e40d7-151">hello 다음 예제에서는 ext4에 파티션을 만듭니다 /dev/sdc1:</span><span class="sxs-lookup"><span data-stu-id="e40d7-151">hello following example creates an ext4 partition on /dev/sdc1:</span></span>
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![파일 시스템 만들기](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > <span data-ttu-id="e40d7-153">SuSE Linux Enterprise 11 시스템에서는 ext4 파일 시스템에 대해 읽기 전용 권한만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-153">SuSE Linux Enterprise 11 systems only support read-only access for ext4 file systems.</span></span> <span data-ttu-id="e40d7-154">이러한 시스템 ext4 아닌 ext3 tooformat hello 새 파일 시스템을 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-154">For these systems, it is recommended tooformat hello new file system as ext3 rather than ext4.</span></span>

9. <span data-ttu-id="e40d7-155">디렉터리 toomount hello 새 파일 시스템의 경우 다음과 같이 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-155">Make a directory toomount hello new file system, as follows:</span></span>
   
    ```bash
    sudo mkdir /datadrive
    ```

10. <span data-ttu-id="e40d7-156">마지막으로 다음과 같이 hello 드라이브를 탑재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-156">Finally you can mount hello drive, as follows:</span></span>
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    <span data-ttu-id="e40d7-157">hello 데이터 디스크가 현재으로 준비 toouse **/datadrive**합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-157">hello data disk is now ready toouse as **/datadrive**.</span></span>
   
    ![Hello 디렉터리 및 탑재 hello 디스크 만들기](./media/attach-disk/mkdirandmount.png)

11. <span data-ttu-id="e40d7-159">Hello 새 드라이브 너무/등/fstab를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-159">Add hello new drive too/etc/fstab:</span></span>
   
    <span data-ttu-id="e40d7-160">tooensure hello 드라이브 toohello /etc/fstab 파일을 추가 하는 다시 부팅 해야 자동으로 다시 탑재 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-160">tooensure hello drive is remounted automatically after a reboot it must be added toohello /etc/fstab file.</span></span> <span data-ttu-id="e40d7-161">또한 해당 hello UUID (전체적으로 Unique IDentifier) 방금 hello 장치 이름 (예: /dev/sdc1)이 아닌 /etc/fstab toorefer toohello 드라이브는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-161">In addition, it is highly recommended that hello UUID (Universally Unique IDentifier) is used in /etc/fstab toorefer toohello drive rather than just hello device name (i.e. /dev/sdc1).</span></span> <span data-ttu-id="e40d7-162">UUID는 hello를 사용 하 여 지정 된 위치로 hello 운영 체제 부팅 하는 동안 디스크 오류를 검색 하 고 장치 Id 할당 되 고 그런 다음 모든 나머지 데이터 디스크를 탑재 된 tooa 되 고 hello 잘못 된 디스크를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-162">Using hello UUID avoids hello incorrect disk being mounted tooa given location if hello OS detects a disk error during boot and any remaining data disks then being assigned those device IDs.</span></span> <span data-ttu-id="e40d7-163">toofind hello 새 드라이브의 UUID hello hello를 사용할 수 있습니다, **blkid** 유틸리티:</span><span class="sxs-lookup"><span data-stu-id="e40d7-163">toofind hello UUID of hello new drive, you can use hello **blkid** utility:</span></span>
   
    ```bash
    sudo -i blkid
    ```
   
    <span data-ttu-id="e40d7-164">hello 출력은 다음 예제와 비슷한 toohello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-164">hello output looks similar toohello following example:</span></span>
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > <span data-ttu-id="e40d7-165">Hello를 잘못 편집 **/등/fstab** 파일 경우 시스템 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-165">Improperly editing hello **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="e40d7-166">를 알 수 없는 경우 tooproperly이이 파일을 편집 하는 방법에 대 한 내용은 toohello 분포의 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e40d7-166">If unsure, refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="e40d7-167">또한 편집 하기 전에 hello /etc/fstab 파일의 백업을 만들어졌는지 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-167">It is also recommended that a backup of hello /etc/fstab file is created before editing.</span></span>

    <span data-ttu-id="e40d7-168">Hello을 열고 **/등/fstab** 파일 텍스트 편집기에서:</span><span class="sxs-lookup"><span data-stu-id="e40d7-168">Next, open hello **/etc/fstab** file in a text editor:</span></span>

    ```bash
    sudo vi /etc/fstab
    ```

    <span data-ttu-id="e40d7-169">이 예제에서 사용 하 여 hello UUID 값 hello에 대 한 새 **/개발/sdc1** hello 탑재 지점 및 hello 이전 단계에서 만든 장치 **/datadrive**합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-169">In this example, we use hello UUID value for hello new **/dev/sdc1** device that was created in hello previous steps, and hello mountpoint **/datadrive**.</span></span> <span data-ttu-id="e40d7-170">줄 toohello의 끝 다음 hello hello 추가 **/등/fstab** 파일:</span><span class="sxs-lookup"><span data-stu-id="e40d7-170">Add hello following line toohello end of hello **/etc/fstab** file:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    <span data-ttu-id="e40d7-171">또는 SuSE Linux 기반 시스템에서 약간 다른 형식 toouse 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-171">Or, on systems based on SuSE Linux you may need toouse a slightly different format:</span></span>

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > <span data-ttu-id="e40d7-172">hello `nofail` 옵션을 선택 하면 해당 hello hello 파일 시스템 손상 되었거나 hello 디스크 부팅 시 존재 하지 않는 경우에 VM을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-172">hello `nofail` option ensures that hello VM starts even if hello filesystem is corrupt or hello disk does not exist at boot time.</span></span> <span data-ttu-id="e40d7-173">이 옵션이 없으면 발생할 수에 설명 된 대로 동작 [없습니다 SSH tooLinux VM tooFSTAB 오류 인해](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-173">Without this option, you may encounter behavior as described in [Cannot SSH tooLinux VM due tooFSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span></span>

    <span data-ttu-id="e40d7-174">파일 시스템 hello 탑재 되어 이제 테스트할 수 있습니다 제대로 분리 하 고 다음 hello 파일 시스템 다시 탑재할 즉, 사용 하 여 hello 예제 탑재 지점 `/datadrive` hello에서 만든 이전 단계:</span><span class="sxs-lookup"><span data-stu-id="e40d7-174">You can now test that hello file system is mounted properly by unmounting and then remounting hello file system, i.e. using hello example mount point `/datadrive` created in hello earlier steps:</span></span>

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    <span data-ttu-id="e40d7-175">경우 hello `mount` 오류를 생성 하는 명령, 파일 hello/등/fstab 구문이 올바른지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e40d7-175">If hello `mount` command produces an error, check hello /etc/fstab file for correct syntax.</span></span> <span data-ttu-id="e40d7-176">추가 데이터 드라이브 또는 파티션을 만든 경우에는 /etc/fstab에 해당 드라이브나 파티션도 별도로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-176">If additional data drives or partitions are created, enter them into /etc/fstab separately as well.</span></span>

    <span data-ttu-id="e40d7-177">이 명령을 사용 하 여 hello 드라이브에 쓸 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-177">Make hello drive writable by using this command:</span></span>

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > <span data-ttu-id="e40d7-178">이후에 fstab 편집 하지 않고도 데이터 디스크를 제거 하는 hello VM toofail tooboot을 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-178">Subsequently removing a data disk without editing fstab could cause hello VM toofail tooboot.</span></span> <span data-ttu-id="e40d7-179">이 경우 경우가 종종, 대부분의 배포판 제공 하거나 hello `nofail` 및/또는 `nobootwait` 부팅 시 toomount hello 디스크에 오류가 발생 하는 경우에 시스템 tooboot 수 있는 fstab 옵션.</span><span class="sxs-lookup"><span data-stu-id="e40d7-179">If this is a common occurrence, most distributions provide either hello `nofail` and/or `nobootwait` fstab options that allow a system tooboot even if hello disk fails toomount at boot time.</span></span> <span data-ttu-id="e40d7-180">이러한 매개 변수에 대한 자세한 내용은 배포 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e40d7-180">Consult your distribution's documentation for more information on these parameters.</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="e40d7-181">Azure에서 Linux에 대한 TRIM/UNMAP 지원</span><span class="sxs-lookup"><span data-stu-id="e40d7-181">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="e40d7-182">일부 Linux 커널을 지원 TRIM/매핑 해제 작업 toodiscard hello 디스크에 사용 하지 않는 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-182">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="e40d7-183">이러한 작업은 표준 저장소 tooinform 페이지를 삭제 하는 Azure는 더 이상 올바르지와 무시할 수에서 주로 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-183">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="e40d7-184">큰 파일을 만들고 삭제하는 경우 페이지를 삭제하여 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-184">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="e40d7-185">두 가지 방법으로 Linux VM에서 tooenable TRIM을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-185">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="e40d7-186">일반적으로 권장 접근법 hello에 대 한 배포를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e40d7-186">As usual, consult your distribution for hello recommended approach:</span></span>

* <span data-ttu-id="e40d7-187">사용 하 여 hello `discard` 옵션에 탑재 `/etc/fstab`, 예:</span><span class="sxs-lookup"><span data-stu-id="e40d7-187">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```

* <span data-ttu-id="e40d7-188">일부 경우 hello에 `discard` 옵션에는 성능 문제가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e40d7-188">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="e40d7-189">Hello 또는 실행할 수 있습니다 `fstrim` hello 명령줄에서 수동으로 명령을 선택 하거나 추가 tooyour crontab toorun 정기적으로:</span><span class="sxs-lookup"><span data-stu-id="e40d7-189">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>
  
    <span data-ttu-id="e40d7-190">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="e40d7-190">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="e40d7-191">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="e40d7-191">**RHEL/CentOS**</span></span>
  
    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="e40d7-192">문제 해결</span><span class="sxs-lookup"><span data-stu-id="e40d7-192">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="e40d7-193">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e40d7-193">Next Steps</span></span>
<span data-ttu-id="e40d7-194">자세한 내용은 다음 문서는 hello에서 Linux VM을 사용 하 여 하는 방법에 대 한:</span><span class="sxs-lookup"><span data-stu-id="e40d7-194">You can read more about using your Linux VM in hello following articles:</span></span>

* <span data-ttu-id="e40d7-195">[어떻게 toolog Linux를 실행 하는 tooa 가상 컴퓨터][Logon]</span><span class="sxs-lookup"><span data-stu-id="e40d7-195">[How toolog on tooa virtual machine running Linux][Logon]</span></span>
* [<span data-ttu-id="e40d7-196">어떻게 toodetach Linux 가상 컴퓨터에서 디스크</span><span class="sxs-lookup"><span data-stu-id="e40d7-196">How toodetach a disk from a Linux virtual machine</span></span>](detach-disk.md)
* [<span data-ttu-id="e40d7-197">Hello Azure CLI를 사용 하 여 hello 클래식 배포 모델</span><span class="sxs-lookup"><span data-stu-id="e40d7-197">Using hello Azure CLI with hello Classic deployment model</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="e40d7-198">Azure에서 Linux VM에 RAID 구성</span><span class="sxs-lookup"><span data-stu-id="e40d7-198">Configure RAID on a Linux VM in Azure</span></span>](../configure-raid.md)
* [<span data-ttu-id="e40d7-199">Azure에서 Linux VM에 LVM 구성</span><span class="sxs-lookup"><span data-stu-id="e40d7-199">Configure LVM on a Linux VM in Azure</span></span>](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
