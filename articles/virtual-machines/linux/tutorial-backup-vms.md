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
ms.openlocfilehash: d0cbf7883a8737bcb10e9dd251c9792a12993f77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="back-up-linux--virtual-machines-in-azure"></a><span data-ttu-id="fab54-103">Azure에서 Linux 가상 컴퓨터 백업</span><span class="sxs-lookup"><span data-stu-id="fab54-103">Back up Linux  virtual machines in Azure</span></span>

<span data-ttu-id="fab54-104">정기적으로 백업을 수행하여 데이터를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="fab54-105">Azure Backup은 지역 중복 복구 자격 증명 모음에 저장되는 복구 지점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="fab54-106">복구 지점에서 복원하는 경우 전체 VM 또는 특정 파일만 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-106">When you restore from a recovery point, you can restore the whole VM or just specific files.</span></span> <span data-ttu-id="fab54-107">이 문서에서는 nginx를 실행하는 Linux VM으로 단일 파일을 복원하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-107">This article explains how to restore a single file to a Linux VM running nginx.</span></span> <span data-ttu-id="fab54-108">사용할 VM이 아직 없는 경우 [Linux 빠른 시작](quick-create-cli.md)을 사용하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-108">If you don't already have a VM to use, you can create one using the [Linux quickstart](quick-create-cli.md).</span></span> <span data-ttu-id="fab54-109">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fab54-110">VM 백업 만들기</span><span class="sxs-lookup"><span data-stu-id="fab54-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="fab54-111">매일 백업 예약</span><span class="sxs-lookup"><span data-stu-id="fab54-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="fab54-112">백업에서 파일 복원</span><span class="sxs-lookup"><span data-stu-id="fab54-112">Restore a file from a backup</span></span>



## <a name="backup-overview"></a><span data-ttu-id="fab54-113">백업 개요</span><span class="sxs-lookup"><span data-stu-id="fab54-113">Backup overview</span></span>

<span data-ttu-id="fab54-114">Azure Backup 서비스에서 백업을 시작하면 백업 확장을 트리거하여 특정 시점 스냅숏을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-114">When the Azure Backup service initiates a backup, it triggers the backup extension to take a point-in-time snapshot.</span></span> <span data-ttu-id="fab54-115">Azure Backup 서비스는 Linux에서 _VMSnapshotLinux_ 확장을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-115">The Azure Backup service uses the _VMSnapshotLinux_ extension in Linux.</span></span> <span data-ttu-id="fab54-116">VM을 실행하는 경우 확장은 첫 번째 VM 백업 중에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-116">The extension is installed during the first VM backup if the VM is running.</span></span> <span data-ttu-id="fab54-117">VM이 실행되고 있지 않을 경우 Backup 서비스가 기본 저장소의 스냅숏을 생성합니다(VM이 중지되었을 때는 응용 프로그램 쓰기가 수행되지 않음).</span><span class="sxs-lookup"><span data-stu-id="fab54-117">If the VM is not running, the Backup service takes a snapshot of the underlying storage (since no application writes occur while the VM is stopped).</span></span>

<span data-ttu-id="fab54-118">기본적으로 Azure Backup에서는 Linux VM용으로 파일 시스템 일치 백업을 가져옵니다. 그러나 [사전 스크립트 및 사후 스크립트 프레임워크를 사용하여 응용 프로그램 일치 백업](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent)을 가져오도록 Azure Backup을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-118">By default, Azure Backup takes a file system consistent backup for Linux VM but it can be configured to take [application consistent backup using pre-script and post-script framework](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span></span> <span data-ttu-id="fab54-119">Azure Backup 서비스가 스냅숏을 생성하면 데이터가 자격 증명 모음으로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-119">Once the Azure Backup service takes the snapshot, the data is transferred to the vault.</span></span> <span data-ttu-id="fab54-120">효율성을 극대화하기 위해 이 서비스는 이전 백업 이후에 변경된 데이터 블록만 식별하여 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-120">To maximize efficiency, the service identifies and transfers only the blocks of data that have changed since the previous backup.</span></span>

<span data-ttu-id="fab54-121">데이터 전송이 완료되면 스냅숏이 제거되고 복구 지점이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-121">When the data transfer is complete, the snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="fab54-122">백업 만들기</span><span class="sxs-lookup"><span data-stu-id="fab54-122">Create a backup</span></span>
<span data-ttu-id="fab54-123">간단한 예약된 매일 백업을 Recovery Services 자격 증명 모음에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-123">Create a simple scheduled daily backup to a Recovery Services Vault.</span></span> 

1. <span data-ttu-id="fab54-124">[Azure Portal](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-124">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="fab54-125">왼쪽 메뉴에서 **가상 컴퓨터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-125">In the menu on the left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="fab54-126">목록에서 백업할 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-126">From the list, select a VM to back up.</span></span>
4. <span data-ttu-id="fab54-127">VM 블레이드의 **설정** 섹션에서 **백업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-127">On the VM blade, in the **Settings** section, click **Backup**.</span></span> <span data-ttu-id="fab54-128">**백업 사용** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-128">The **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="fab54-129">**Recovery Services 자격 증명 모음**에서 **새로 만들기**를 클릭하고 새 자격 증명 모음의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-129">In **Recovery Services vault**, click **Create new** and provide the name for the new vault.</span></span> <span data-ttu-id="fab54-130">새 자격 증명 모음이 가상 컴퓨터와 동일한 리소스 그룹과 위치에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-130">A new vault is created in the same Resource Group and location as the virtual machine.</span></span>
6. <span data-ttu-id="fab54-131">**백업 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-131">Click **Backup policy**.</span></span> <span data-ttu-id="fab54-132">이 예제에서는 기본값을 그대로 유지하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-132">For this example, keep the defaults and click **OK**.</span></span>
7. <span data-ttu-id="fab54-133">**백업 사용** 블레이드에서 **백업 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-133">On the **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="fab54-134">이렇게 하면 기본 일정에 따라 매일 백업이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-134">This creates a daily backup based on the default schedule.</span></span>
10. <span data-ttu-id="fab54-135">초기 복구 지점을 만들려면 **백업** 블레이드에서 **지금 백업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-135">To create an initial recovery point, on the **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="fab54-136">**지금 백업** 블레이드에서 달력 모양 아이콘을 클릭하고 달력 컨트롤을 사용하여 이 복구 지점을 유지할 마지막 날을 선택하고 **백업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-136">On the **Backup Now** blade, click the calendar icon, use the calendar control to select the last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="fab54-137">VM에 대한 **백업** 블레이드에서 완료된 복구 지점의 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-137">In the **Backup** blade for your VM, you will see the number of recovery points that are complete.</span></span>

    ![복구 지점](./media/tutorial-backup-vms/backup-complete.png)

<span data-ttu-id="fab54-139">첫 번째 백업에는 약 20분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-139">The first backup takes about 20 minutes.</span></span> <span data-ttu-id="fab54-140">백업이 완료되면 이 자습서의 다음 부분으로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-140">Proceed to the next part of this tutorial after your backup is finished.</span></span>

## <a name="restore-a-file"></a><span data-ttu-id="fab54-141">파일 복원</span><span class="sxs-lookup"><span data-stu-id="fab54-141">Restore a file</span></span>

<span data-ttu-id="fab54-142">실수로 파일을 삭제하거나 변경한 경우 [파일 복구]를 사용하여 백업 자격 증명 모음에서 파일을 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-142">If you accidentally delete or make changes to a file, you can use File Recovery to recover the file from your backup vault.</span></span> <span data-ttu-id="fab54-143">파일 복구는 VM에서 실행되는 스크립트를 사용하여 복구 지점을 로컬 드라이브로 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-143">File Recovery uses a script that runs on the VM, to mount the recovery point as local drive.</span></span> <span data-ttu-id="fab54-144">이러한 드라이브는 12시간 동안 탑재된 상태로 유지되므로 복구 지점에서 파일을 복사하여 VM에 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-144">These drives will remain mounted for 12 hours so that you can copy files from the recovery point and restore them to the VM.</span></span>  

<span data-ttu-id="fab54-145">이 예제에서는 기본 nginx 웹 페이지인 /var/www/html/index.nginx-debian.html을 복구하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-145">In this example, we show how to recover the default nginx web page /var/www/html/index.nginx-debian.html.</span></span> <span data-ttu-id="fab54-146">이 예제에서 VM의 공용 IP 주소는 *13.69.75.209*입니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-146">The public IP address of our VM in this example is *13.69.75.209*.</span></span> <span data-ttu-id="fab54-147">다음을 사용하여 VM의 IP 주소를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-147">You can find the IP address of your vm using:</span></span>

 ```bash 
 az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
 ```

 
1. <span data-ttu-id="fab54-148">로컬 컴퓨터에서 브라우저를 열고 VM의 공용 IP 주소를 입력하여 기본 nginx 웹 페이지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-148">On your local computer, open a browser and type in the public IP address of your VM to see the default nginx web page.</span></span>

    ![기본 nginx 웹 페이지](./media/tutorial-backup-vms/nginx-working.png)

1. <span data-ttu-id="fab54-150">VM에 SSH를 수행합니다</span><span class="sxs-lookup"><span data-stu-id="fab54-150">SSH into your VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
2. <span data-ttu-id="fab54-151">/var/www/html/index.nginx-debian.html을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-151">Delete /var/www/html/index.nginx-debian.html.</span></span>

    ```bash
    sudo rm /var/www/html/index.nginx-debian.html
    ```
    
4. <span data-ttu-id="fab54-152">로컬 컴퓨터에서 Ctrl+F5를 눌러 브라우저를 새로 고친 다음 기본 nginx 페이지가 사라졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-152">On your local computer, refresh the browser by hitting CTRL + F5 to see that default nginx page is gone.</span></span>

    ![기본 nginx 웹 페이지](./media/tutorial-backup-vms/nginx-broken.png)
    
1. <span data-ttu-id="fab54-154">로컬 컴퓨터에서 [Azure Portal](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-154">On your local computer, sign in to the [Azure portal](https://portal.azure.com/).</span></span>
6. <span data-ttu-id="fab54-155">왼쪽 메뉴에서 **가상 컴퓨터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-155">In the menu on the left, select **Virtual machines**.</span></span> 
7. <span data-ttu-id="fab54-156">목록에서 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-156">From the list, select the VM.</span></span>
8. <span data-ttu-id="fab54-157">VM 블레이드의 **설정** 섹션에서 **백업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-157">On the VM blade, in the **Settings** section, click **Backup**.</span></span> <span data-ttu-id="fab54-158">**백업** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-158">The **Backup** blade opens.</span></span> 
9. <span data-ttu-id="fab54-159">블레이드 위쪽의 메뉴에서 **파일 복구**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-159">In the menu at the top of the blade, select **File Recovery**.</span></span> <span data-ttu-id="fab54-160">**파일 복구** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-160">The **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="fab54-161">**1단계: 복구 지점 선택**의 드롭다운에서 복구 지점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-161">In **Step 1: Select recovery point**, select a recovery point from the drop-down.</span></span>
11. <span data-ttu-id="fab54-162">**2단계: 스크립트를 다운로드하여 파일 찾아보기 및 복구**에서 **실행 파일 다운로드** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-162">In **Step 2: Download script to browse and recover files**, click the **Download Executable** button.</span></span> <span data-ttu-id="fab54-163">다운로드한 파일을 로컬 컴퓨터에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-163">Save the downloaded file to your local computer.</span></span>
7. <span data-ttu-id="fab54-164">**스크립트 다운로드**를 클릭하여 스크립트 파일을 로컬로 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-164">Click **Download script** to download the script file locally.</span></span>
8. <span data-ttu-id="fab54-165">Bash 프롬프트를 열고 다음을 입력한 다음 *Linux_myVM_05-05-2017.sh*를 다운로드한 스크립트의 올바른 경로와 파일 이름으로, *azureuser*를 VM의 사용자 이름으로 그리고 *13.69.75.209*를 VM에 대한 공용 IP 주소로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-165">Open a Bash prompt and type the following, replacing *Linux_myVM_05-05-2017.sh* with the correct path and filename for the script that you downloaded, *azureuser* with the username for the VM and *13.69.75.209* with the public IP address for your VM.</span></span>
    
    ```bash
    scp Linux_myVM_05-05-2017.sh azureuser@13.69.75.209:
    ```
    
9. <span data-ttu-id="fab54-166">로컬 컴퓨터에서 VM에 대한 SSH 연결을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-166">On your local computer, open an SSH connection to the VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
    
10. <span data-ttu-id="fab54-167">VM에서 스크립트 파일에 실행 권한을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-167">On your VM, add execute permissions to the script file.</span></span>

    ```bash
    chmod +x Linux_myVM_05-05-2017.sh
    ```
    
11. <span data-ttu-id="fab54-168">VM에서 스크립트를 실행하여 복구 지점을 파일 시스템으로 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-168">On your VM, run the script to mount the recovery point as a filesystem.</span></span>

    ```bash
    ./Linux_myVM_05-05-2017.sh
    ```
    
12. <span data-ttu-id="fab54-169">스크립트의 출력에서 탑재 지점에 대한 경로를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-169">The output from the script gives you the path for the mount point.</span></span> <span data-ttu-id="fab54-170">출력은 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-170">The output looks similar to this:</span></span>

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
                          
    Connecting to recovery point using ISCSI service...
    
    Connection succeeded!
    
    Please wait while we attach volumes of the recovery point to this machine...
                         
    ************ Volumes of the recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath 

    1)  | /dev/sdc  |  /dev/sdc1  |  /home/azureuser/myVM-20170505191055/Volume1

    ************ Open File Explorer to browse for files. ************

    After recovery, to remove the disks and close the connection to the recovery point, please click 'Unmount Disks' in step 3 of the portal.

    Please enter 'q/Q' to exit...
    ```

12. <span data-ttu-id="fab54-171">VM에서 기본 nginx 웹 페이지를 탑재 지점에서 파일을 삭제한 위치로 다시 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-171">On your VM, copy the nginx default web page from the mount point back to where you deleted the file.</span></span>

    ```bash
    sudo cp ~/myVM-20170505191055/Volume1/var/www/html/index.nginx-debian.html /var/www/html/
    ```
    
17. <span data-ttu-id="fab54-172">로컬 컴퓨터에서 기본 nginx 페이지를 보여 주는 VM의 IP 주소에 연결된 브라우저 탭을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-172">On your local computer, open the browser tab where you are connected to the IP address of the VM showing the nginx default page.</span></span> <span data-ttu-id="fab54-173">Ctrl+F5를 눌러 브라우저 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-173">Press CTRL + F5 to refresh the browser page.</span></span> <span data-ttu-id="fab54-174">이제 기본 페이지가 다시 작동하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-174">You should now see that the default page is working again.</span></span>

    ![기본 nginx 웹 페이지](./media/tutorial-backup-vms/nginx-working.png)

18. <span data-ttu-id="fab54-176">로컬 컴퓨터에서 Azure Portal의 브라우저 탭으로 돌아가서 **3단계: 복구 후 디스크 분리**에서 **디스크 분리** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-176">On your local computer, go back to the browser tab for the Azure portal and in **Step 3: Unmount the disks after recovery** click the **Unmount Disks** button.</span></span> <span data-ttu-id="fab54-177">이 단계를 수행하지 않으면 12시간 후에 탑재 지점에 대한 연결이 자동으로 끊깁니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-177">If you forget to do this step, the connection to the mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="fab54-178">12시간이 지나면 새 스크립트를 다운로드하여 새 탑재 지점을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-178">After those 12 hours, you need to download a new script to create a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="fab54-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fab54-179">Next steps</span></span>

<span data-ttu-id="fab54-180">이 자습서에서는 다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-180">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fab54-181">VM 백업 만들기</span><span class="sxs-lookup"><span data-stu-id="fab54-181">Create a backup of a VM</span></span>
> * <span data-ttu-id="fab54-182">매일 백업 예약</span><span class="sxs-lookup"><span data-stu-id="fab54-182">Schedule a daily backup</span></span>
> * <span data-ttu-id="fab54-183">백업에서 파일 복원</span><span class="sxs-lookup"><span data-stu-id="fab54-183">Restore a file from a backup</span></span>

<span data-ttu-id="fab54-184">가상 컴퓨터 모니터링에 대해 알아보려면 다음 자습서로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="fab54-184">Advance to the next tutorial to learn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fab54-185">가상 컴퓨터 모니터링</span><span class="sxs-lookup"><span data-stu-id="fab54-185">Monitor virtual machines</span></span>](tutorial-monitoring.md)

