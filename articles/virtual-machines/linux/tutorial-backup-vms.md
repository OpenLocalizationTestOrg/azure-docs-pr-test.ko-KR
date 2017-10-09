---
title: "Azure Linux VM 백업 | Microsoft Docs"
description: "Azure Backup을 통해 Linux VM을 백업하여 보호합니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 7c00392d5185a2f067f2ee2717529dcbde1e71f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-linux--virtual-machines-in-azure"></a><span data-ttu-id="8d237-103">Azure에서 Linux 가상 컴퓨터 백업</span><span class="sxs-lookup"><span data-stu-id="8d237-103">Back up Linux  virtual machines in Azure</span></span>

<span data-ttu-id="8d237-104">정기적으로 백업을 수행하여 데이터를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="8d237-105">Azure Backup은 지역 중복 복구 자격 증명 모음에 저장되는 복구 지점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="8d237-106">복원할 수는 복구 지점에서 복원할 때는 전체 VM 또는 특정 파일 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-106">When you restore from a recovery point, you can restore hello whole VM or just specific files.</span></span> <span data-ttu-id="8d237-107">이 문서에서는 toorestore 단일 tooa Linux VM 실행 중인 nginx 파일 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-107">This article explains how toorestore a single file tooa Linux VM running nginx.</span></span> <span data-ttu-id="8d237-108">VM toouse 없는 경우 하나를 만들 수 있습니다 hello를 사용 하 여 [Linux 퀵 스타트](quick-create-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-108">If you don't already have a VM toouse, you can create one using hello [Linux quickstart](quick-create-cli.md).</span></span> <span data-ttu-id="8d237-109">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8d237-110">VM 백업 만들기</span><span class="sxs-lookup"><span data-stu-id="8d237-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="8d237-111">매일 백업 예약</span><span class="sxs-lookup"><span data-stu-id="8d237-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="8d237-112">백업에서 파일 복원</span><span class="sxs-lookup"><span data-stu-id="8d237-112">Restore a file from a backup</span></span>



## <a name="backup-overview"></a><span data-ttu-id="8d237-113">백업 개요</span><span class="sxs-lookup"><span data-stu-id="8d237-113">Backup overview</span></span>

<span data-ttu-id="8d237-114">백업을 시작 하는 hello Azure 백업 서비스를 hello 예비 내선 번호 tootake를 지정 시간에 스냅숏으로 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-114">When hello Azure Backup service initiates a backup, it triggers hello backup extension tootake a point-in-time snapshot.</span></span> <span data-ttu-id="8d237-115">Azure 백업 서비스 hello hello를 사용 하 여 _VMSnapshotLinux_ Linux에서 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-115">hello Azure Backup service uses hello _VMSnapshotLinux_ extension in Linux.</span></span> <span data-ttu-id="8d237-116">hello 확장 hello VM을 실행 하는 경우 hello 첫 번째 VM 백업 하는 동안 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-116">hello extension is installed during hello first VM backup if hello VM is running.</span></span> <span data-ttu-id="8d237-117">Hello VM 실행 되지 않는 경우, hello 백업 서비스는 hello (응용 프로그램 쓰기가 수행 되지 hello VM을 중지 하는 동안) 이후 기본 저장소의 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-117">If hello VM is not running, hello Backup service takes a snapshot of hello underlying storage (since no application writes occur while hello VM is stopped).</span></span>

<span data-ttu-id="8d237-118">기본적으로 Azure 백업에서는 파일 시스템 일관성 백업을 Linux VM에 대 한 구성된 tootake 수 없지만 [전 스크립트와 사후 스크립트 프레임 워크를 사용 하 여 응용 프로그램 일치 백업을](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent)합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-118">By default, Azure Backup takes a file system consistent backup for Linux VM but it can be configured tootake [application consistent backup using pre-script and post-script framework](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span></span> <span data-ttu-id="8d237-119">Hello Azure 백업 서비스는 hello 스냅숏을, 되 면 hello 데이터는 전송 된 toohello 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-119">Once hello Azure Backup service takes hello snapshot, hello data is transferred toohello vault.</span></span> <span data-ttu-id="8d237-120">toomaximize 효율성 hello 서비스를 식별 하 고 hello 이전 백업 이후에 변경 된 데이터의 hello 블록만 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-120">toomaximize efficiency, hello service identifies and transfers only hello blocks of data that have changed since hello previous backup.</span></span>

<span data-ttu-id="8d237-121">Hello 데이터 전송이 완료 되 면 hello 스냅숏을 제거 되 고 복구 지점이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-121">When hello data transfer is complete, hello snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="8d237-122">백업 만들기</span><span class="sxs-lookup"><span data-stu-id="8d237-122">Create a backup</span></span>
<span data-ttu-id="8d237-123">간단한 예약 된 매일 백업 tooa 복구 서비스 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-123">Create a simple scheduled daily backup tooa Recovery Services Vault.</span></span> 

1. <span data-ttu-id="8d237-124">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8d237-125">Hello hello 왼쪽 메뉴에서 선택 **가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-125">In hello menu on hello left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="8d237-126">Hello 목록에서 VM tooback를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-126">From hello list, select a VM tooback up.</span></span>
4. <span data-ttu-id="8d237-127">Hello에 hello VM 블레이드에서 **설정** 섹션에서 클릭 **백업**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-127">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="8d237-128">hello **백업 사용** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-128">hello **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="8d237-129">**복구 서비스 자격 증명 모음**, 클릭 **새로 만들기** hello hello 새 자격 증명 모음 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-129">In **Recovery Services vault**, click **Create new** and provide hello name for hello new vault.</span></span> <span data-ttu-id="8d237-130">새 자격 증명 모음에서에서 만든 hello 동일한 리소스 그룹 및 hello 가상 컴퓨터로 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-130">A new vault is created in hello same Resource Group and location as hello virtual machine.</span></span>
6. <span data-ttu-id="8d237-131">**백업 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-131">Click **Backup policy**.</span></span> <span data-ttu-id="8d237-132">이 예에서는 hello 기본값을 유지 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-132">For this example, keep hello defaults and click **OK**.</span></span>
7. <span data-ttu-id="8d237-133">Hello에 **백업 사용** 블레이드에서 클릭 **백업 사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-133">On hello **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="8d237-134">이렇게 하면 hello 기본 일정에 따라 매일 백업을 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-134">This creates a daily backup based on hello default schedule.</span></span>
10. <span data-ttu-id="8d237-135">초기 복구 지점 hello에 toocreate **백업** 블레이드 클릭 **지금 백업**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-135">toocreate an initial recovery point, on hello **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="8d237-136">Hello에 **지금 백업** 블레이드에서 hello 달력 아이콘을 hello 달력 컨트롤 tooselect hello 마지막 날이 복구 지점을 유지 하 고 클릭을 사용 하 여 **백업**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-136">On hello **Backup Now** blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="8d237-137">Hello에 **백업** 블레이드에서 VM에 대 한 완료 된 복구 지점 hello 수가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-137">In hello **Backup** blade for your VM, you will see hello number of recovery points that are complete.</span></span>

    ![복구 지점](./media/tutorial-backup-vms/backup-complete.png)

<span data-ttu-id="8d237-139">hello 첫 번째 백업에는 20 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-139">hello first backup takes about 20 minutes.</span></span> <span data-ttu-id="8d237-140">백업이 완료 된 후 toohello이이 자습서의 다음 단계를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-140">Proceed toohello next part of this tutorial after your backup is finished.</span></span>

## <a name="restore-a-file"></a><span data-ttu-id="8d237-141">파일 복원</span><span class="sxs-lookup"><span data-stu-id="8d237-141">Restore a file</span></span>

<span data-ttu-id="8d237-142">실수로 삭제 하거나 변경 tooa 파일 확인을 하는 경우에 백업 자격 증명 모음에서 파일 복구 toorecover hello 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-142">If you accidentally delete or make changes tooa file, you can use File Recovery toorecover hello file from your backup vault.</span></span> <span data-ttu-id="8d237-143">파일 복구 hello VM에서 실행 되는 스크립트를 사용 하 여 로컬 드라이브로 toomount hello 복구 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-143">File Recovery uses a script that runs on hello VM, toomount hello recovery point as local drive.</span></span> <span data-ttu-id="8d237-144">이러한 드라이브 남습니다 탑재 된 12 시간 동안 hello 복구 지점에서 파일을 복사 하 고 toohello VM을 복원할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-144">These drives will remain mounted for 12 hours so that you can copy files from hello recovery point and restore them toohello VM.</span></span>  

<span data-ttu-id="8d237-145">이 예제에서는 toorecover 기본 nginx 웹 페이지 /var/www/html/index.nginx-debian.html hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-145">In this example, we show how toorecover hello default nginx web page /var/www/html/index.nginx-debian.html.</span></span> <span data-ttu-id="8d237-146">이 예에서 VM의 공용 IP 주소 hello는 *13.69.75.209*합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-146">hello public IP address of our VM in this example is *13.69.75.209*.</span></span> <span data-ttu-id="8d237-147">사용 하 여 vm의 hello IP 주소를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-147">You can find hello IP address of your vm using:</span></span>

 ```bash 
 az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
 ```

 
1. <span data-ttu-id="8d237-148">로컬 컴퓨터의 VM toosee hello 기본 nginx 웹 페이지의 hello 공용 IP 주소에서 유형과 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-148">On your local computer, open a browser and type in hello public IP address of your VM toosee hello default nginx web page.</span></span>

    ![기본 nginx 웹 페이지](./media/tutorial-backup-vms/nginx-working.png)

1. <span data-ttu-id="8d237-150">VM에 SSH를 수행합니다</span><span class="sxs-lookup"><span data-stu-id="8d237-150">SSH into your VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
2. <span data-ttu-id="8d237-151">/var/www/html/index.nginx-debian.html을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-151">Delete /var/www/html/index.nginx-debian.html.</span></span>

    ```bash
    sudo rm /var/www/html/index.nginx-debian.html
    ```
    
4. <span data-ttu-id="8d237-152">로컬 컴퓨터에서 CTRL 키를 눌러 hello 브라우저를 새로 고치려면 + 기본 nginx 페이지 F5 toosee는 사라집니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-152">On your local computer, refresh hello browser by hitting CTRL + F5 toosee that default nginx page is gone.</span></span>

    ![기본 nginx 웹 페이지](./media/tutorial-backup-vms/nginx-broken.png)
    
1. <span data-ttu-id="8d237-154">로컬 컴퓨터에서 toohello에 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-154">On your local computer, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
6. <span data-ttu-id="8d237-155">Hello hello 왼쪽 메뉴에서 선택 **가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-155">In hello menu on hello left, select **Virtual machines**.</span></span> 
7. <span data-ttu-id="8d237-156">Hello 목록에서 hello VM을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-156">From hello list, select hello VM.</span></span>
8. <span data-ttu-id="8d237-157">Hello에 hello VM 블레이드에서 **설정** 섹션에서 클릭 **백업**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-157">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="8d237-158">hello **백업** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-158">hello **Backup** blade opens.</span></span> 
9. <span data-ttu-id="8d237-159">Hello hello 블레이드의 hello 위쪽 메뉴에서 선택 **파일 복구**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-159">In hello menu at hello top of hello blade, select **File Recovery**.</span></span> <span data-ttu-id="8d237-160">hello **파일 복구** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-160">hello **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="8d237-161">**1 단계: 복구 지점을 선택**를 hello 드롭다운 목록에서 복구 지점을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-161">In **Step 1: Select recovery point**, select a recovery point from hello drop-down.</span></span>
11. <span data-ttu-id="8d237-162">**2 단계: 스크립트 toobrowse 다운로드 하 고 파일을 복구할**, hello 클릭 **실행 파일을 다운로드** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-162">In **Step 2: Download script toobrowse and recover files**, click hello **Download Executable** button.</span></span> <span data-ttu-id="8d237-163">로컬 컴퓨터를 tooyour hello 다운로드 한 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-163">Save hello downloaded file tooyour local computer.</span></span>
7. <span data-ttu-id="8d237-164">클릭 **스크립트 다운로드** toodownload hello 스크립트 파일을 로컬입니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-164">Click **Download script** toodownload hello script file locally.</span></span>
8. <span data-ttu-id="8d237-165">Bash 프롬프트 유형과 hello 뒤, 대체 열고 *Linux_myVM_05-05-2017.sh* hello 경로 파일 이름을 다운로드 한 hello 스크립트에 대 한 올바른 *azureuser* hello VM에 대 한 hello 사용자 이름으로 및 *13.69.75.209* hello VM에 대 한 공용 IP 주소와 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-165">Open a Bash prompt and type hello following, replacing *Linux_myVM_05-05-2017.sh* with hello correct path and filename for hello script that you downloaded, *azureuser* with hello username for hello VM and *13.69.75.209* with hello public IP address for your VM.</span></span>
    
    ```bash
    scp Linux_myVM_05-05-2017.sh azureuser@13.69.75.209:
    ```
    
9. <span data-ttu-id="8d237-166">로컬 컴퓨터에서 SSH 연결 toohello VM을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-166">On your local computer, open an SSH connection toohello VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
    
10. <span data-ttu-id="8d237-167">VM에서 추가 권한 toohello 스크립트 파일을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-167">On your VM, add execute permissions toohello script file.</span></span>

    ```bash
    chmod +x Linux_myVM_05-05-2017.sh
    ```
    
11. <span data-ttu-id="8d237-168">VM에서 hello 스크립트 toomount hello 복구 지점 파일 시스템으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-168">On your VM, run hello script toomount hello recovery point as a filesystem.</span></span>

    ```bash
    ./Linux_myVM_05-05-2017.sh
    ```
    
12. <span data-ttu-id="8d237-169">hello는 hello 탑재 지점에 대 한 경로 hello hello 스크립트 제공에서 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-169">hello output from hello script gives you hello path for hello mount point.</span></span> <span data-ttu-id="8d237-170">hello 출력은 유사한 toothis 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-170">hello output looks similar toothis:</span></span>

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
                          
    Connecting toorecovery point using ISCSI service...
    
    Connection succeeded!
    
    Please wait while we attach volumes of hello recovery point toothis machine...
                         
    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath 

    1)  | /dev/sdc  |  /dev/sdc1  |  /home/azureuser/myVM-20170505191055/Volume1

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

12. <span data-ttu-id="8d237-171">VM을 복사 hello nginx 기본 웹 페이지 hello 파일 hello 탑재 지점 백 toowhere에서 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-171">On your VM, copy hello nginx default web page from hello mount point back toowhere you deleted hello file.</span></span>

    ```bash
    sudo cp ~/myVM-20170505191055/Volume1/var/www/html/index.nginx-debian.html /var/www/html/
    ```
    
17. <span data-ttu-id="8d237-172">로컬 컴퓨터에 연결 되어 있는 hello 브라우저 탭을 열고 toohello IP 주소를 hello VM hello nginx 기본 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-172">On your local computer, open hello browser tab where you are connected toohello IP address of hello VM showing hello nginx default page.</span></span> <span data-ttu-id="8d237-173">CTRL + f 5를 눌러 toorefresh hello 브라우저 페이지.</span><span class="sxs-lookup"><span data-stu-id="8d237-173">Press CTRL + F5 toorefresh hello browser page.</span></span> <span data-ttu-id="8d237-174">이제 해당 hello 표시 기본 페이지가 다시 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-174">You should now see that hello default page is working again.</span></span>

    ![기본 nginx 웹 페이지](./media/tutorial-backup-vms/nginx-working.png)

18. <span data-ttu-id="8d237-176">로컬 컴퓨터에 돌아가서 toohello 브라우저 탭과 hello Azure 포털에 대 한 **3 단계: 복구 후 hello 디스크를 마운트 해제** hello 클릭 **디스크 분리** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-176">On your local computer, go back toohello browser tab for hello Azure portal and in **Step 3: Unmount hello disks after recovery** click hello **Unmount Disks** button.</span></span> <span data-ttu-id="8d237-177">이 단계를 toodo을 잊은 경우 hello 연결 toohello "탑재 지점" 닫혀 자동으로 12 시간 후입니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-177">If you forget toodo this step, hello connection toohello mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="8d237-178">이러한 12 시간 후 새 스크립트 toocreate 새 "탑재 지점" toodownload를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-178">After those 12 hours, you need toodownload a new script toocreate a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8d237-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8d237-179">Next steps</span></span>

<span data-ttu-id="8d237-180">이 자습서에서는 다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-180">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8d237-181">VM 백업 만들기</span><span class="sxs-lookup"><span data-stu-id="8d237-181">Create a backup of a VM</span></span>
> * <span data-ttu-id="8d237-182">매일 백업 예약</span><span class="sxs-lookup"><span data-stu-id="8d237-182">Schedule a daily backup</span></span>
> * <span data-ttu-id="8d237-183">백업에서 파일 복원</span><span class="sxs-lookup"><span data-stu-id="8d237-183">Restore a file from a backup</span></span>

<span data-ttu-id="8d237-184">가상 컴퓨터를 모니터링 하는 방법에 대 한 다음 자습서 toolearn toohello를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d237-184">Advance toohello next tutorial toolearn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8d237-185">가상 컴퓨터 모니터링</span><span class="sxs-lookup"><span data-stu-id="8d237-185">Monitor virtual machines</span></span>](tutorial-monitoring.md)

