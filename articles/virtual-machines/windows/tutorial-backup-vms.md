---
title: "Azure Windows VM 백업 | Microsoft Docs"
description: "Azure Backup을 통해 Windows VM을 백업하여 보호합니다."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 8e58a2290e5034ef393f65cbcddb86e18cf4a6ec
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="back-up-windows-virtual-machines-in-azure"></a><span data-ttu-id="1b336-103">Azure에서 Windows 가상 컴퓨터 백업</span><span class="sxs-lookup"><span data-stu-id="1b336-103">Back up Windows virtual machines in Azure</span></span>

<span data-ttu-id="1b336-104">정기적으로 백업을 수행하여 데이터를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="1b336-105">Azure Backup은 지역 중복 복구 자격 증명 모음에 저장되는 복구 지점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="1b336-106">복구 지점에서 복원하는 경우 전체 VM 또는 특정 파일만 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-106">When you restore from a recovery point, you can restore the whole VM or just specific files.</span></span> <span data-ttu-id="1b336-107">이 문서에서는 Windows Server 및 IIS를 실행하는 VM으로 단일 파일을 복원하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-107">This article explains how to restore a single file to a VM running Windows Server and IIS.</span></span> <span data-ttu-id="1b336-108">사용할 VM이 아직 없는 경우 [Windows 빠른 시작](quick-create-portal.md)을 사용하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-108">If you don't already have a VM to use, you can create one using the [Windows quickstart](quick-create-portal.md).</span></span> <span data-ttu-id="1b336-109">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1b336-110">VM 백업 만들기</span><span class="sxs-lookup"><span data-stu-id="1b336-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="1b336-111">매일 백업 예약</span><span class="sxs-lookup"><span data-stu-id="1b336-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="1b336-112">백업에서 파일 복원</span><span class="sxs-lookup"><span data-stu-id="1b336-112">Restore a file from a backup</span></span>




## <a name="backup-overview"></a><span data-ttu-id="1b336-113">백업 개요</span><span class="sxs-lookup"><span data-stu-id="1b336-113">Backup overview</span></span>

<span data-ttu-id="1b336-114">Azure Backup 서비스에서 백업 작업을 시작하면 백업 확장을 트리거하여 특정 시점 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-114">When the Azure Backup service initiates a backup job, it triggers the backup extension to take a point-in-time snapshot.</span></span> <span data-ttu-id="1b336-115">Azure Backup 서비스는 _VMSnapshot_ 확장을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-115">The Azure Backup service uses the _VMSnapshot_ extension.</span></span> <span data-ttu-id="1b336-116">VM을 실행하는 경우 확장은 첫 번째 VM 백업 중에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-116">The extension is installed during the first VM backup if the VM is running.</span></span> <span data-ttu-id="1b336-117">VM이 실행되고 있지 않을 경우 Backup 서비스가 기본 저장소의 스냅숏을 생성합니다(VM이 중지되었을 때는 응용 프로그램 쓰기가 수행되지 않음).</span><span class="sxs-lookup"><span data-stu-id="1b336-117">If the VM is not running, the Backup service takes a snapshot of the underlying storage (since no application writes occur while the VM is stopped).</span></span>

<span data-ttu-id="1b336-118">Windows VM의 스냅숏을 생성할 때 Backup 서비스는 가상 컴퓨터의 디스크에 대한 일관된 스냅숏을 가져오도록 VSS(볼륨 섀도 복사본 서비스)와 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-118">When taking a snapshot of Windows VMs, the Backup service coordinates with the Volume Shadow Copy Service (VSS) to get a consistent snapshot of the virtual machine's disks.</span></span> <span data-ttu-id="1b336-119">Azure Backup 서비스가 스냅숏을 생성하면 데이터가 자격 증명 모음으로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-119">Once the Azure Backup service takes the snapshot, the data is transferred to the vault.</span></span> <span data-ttu-id="1b336-120">효율성을 극대화하기 위해 이 서비스는 이전 백업 이후에 변경된 데이터 블록만 식별하여 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-120">To maximize efficiency, the service identifies and transfers only the blocks of data that have changed since the previous backup.</span></span>

<span data-ttu-id="1b336-121">데이터 전송이 완료되면 스냅숏이 제거되고 복구 지점이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-121">When the data transfer is complete, the snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="1b336-122">백업 만들기</span><span class="sxs-lookup"><span data-stu-id="1b336-122">Create a backup</span></span>
<span data-ttu-id="1b336-123">간단한 예약된 매일 백업을 Recovery Services 자격 증명 모음에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-123">Create a simple scheduled daily backup to a Recovery Services Vault.</span></span> 

1. <span data-ttu-id="1b336-124">[Azure Portal](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-124">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1b336-125">왼쪽 메뉴에서 **가상 컴퓨터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-125">In the menu on the left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="1b336-126">목록에서 백업할 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-126">From the list, select a VM to back up.</span></span>
4. <span data-ttu-id="1b336-127">VM 블레이드의 **설정** 섹션에서 **백업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-127">On the VM blade, in the **Settings** section, click **Backup**.</span></span> <span data-ttu-id="1b336-128">**백업 사용** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-128">The **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="1b336-129">**Recovery Services 자격 증명 모음**에서 **새로 만들기**를 클릭하고 새 자격 증명 모음의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-129">In **Recovery Services vault**, click **Create new** and provide the name for the new vault.</span></span> <span data-ttu-id="1b336-130">새 자격 증명 모음이 가상 컴퓨터와 동일한 리소스 그룹과 위치에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-130">A new vault is created in the same Resource Group and location as the virtual machine.</span></span>
6. <span data-ttu-id="1b336-131">**백업 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-131">Click **Backup policy**.</span></span> <span data-ttu-id="1b336-132">이 예제에서는 기본값을 그대로 유지하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-132">For this example, keep the defaults and click **OK**.</span></span>
7. <span data-ttu-id="1b336-133">**백업 사용** 블레이드에서 **백업 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-133">On the **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="1b336-134">이렇게 하면 기본 일정에 따라 매일 백업이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-134">This creates a daily backup based on the default schedule.</span></span>
10. <span data-ttu-id="1b336-135">초기 복구 지점을 만들려면 **백업** 블레이드에서 **지금 백업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-135">To create an initial recovery point, on the **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="1b336-136">**지금 백업** 블레이드에서 달력 모양 아이콘을 클릭하고 달력 컨트롤을 사용하여 이 복구 지점을 유지할 마지막 날을 선택하고 **백업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-136">On the **Backup Now** blade, click the calendar icon, use the calendar control to select the last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="1b336-137">VM에 대한 **백업** 블레이드에서 완료된 복구 지점의 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-137">In the **Backup** blade for your VM, you will see the number of recovery points that are complete.</span></span>

    ![복구 지점](./media/tutorial-backup-vms/backup-complete.png)
    
<span data-ttu-id="1b336-139">첫 번째 백업에는 약 20분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-139">The first backup takes about 20 minutes.</span></span> <span data-ttu-id="1b336-140">백업이 완료되면 이 자습서의 다음 부분으로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-140">Proceed to the next part of this tutorial after your backup is finished.</span></span>

## <a name="recover-a-file"></a><span data-ttu-id="1b336-141">파일 복구</span><span class="sxs-lookup"><span data-stu-id="1b336-141">Recover a file</span></span>

<span data-ttu-id="1b336-142">실수로 파일을 삭제하거나 변경한 경우 파일 복구를 사용하여 백업 자격 증명 모음에서 파일을 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-142">If you accidentally delete or make changes to a file, you can use File Recovery to recover the file from your backup vault.</span></span> <span data-ttu-id="1b336-143">파일 복구는 VM에서 실행되는 스크립트를 사용하여 복구 지점을 로컬 드라이브로 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-143">File Recovery uses a script that runs on the VM, to mount the recovery point as local drive.</span></span> <span data-ttu-id="1b336-144">이러한 드라이브는 12시간 동안 탑재된 상태로 유지되므로 복구 지점에서 파일을 복사하여 VM에 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-144">These drives will remain mounted for 12 hours so that you can copy files from the recovery point and restore them to the VM.</span></span>  

<span data-ttu-id="1b336-145">이 예제에서는 IIS에 대한 기본 웹 페이지에 사용되는 이미지 파일을 복구하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-145">In this example, we show how to recover the image file that is used in the default web page for IIS.</span></span> 

1. <span data-ttu-id="1b336-146">브라우저를 열고 기본 IIS 페이지를 표시하는 VM의 IP 주소에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-146">Open a browser and connect to the IP address of the VM to show the default IIS page.</span></span>

    ![기본 IIS 웹 페이지](./media/tutorial-backup-vms/iis-working.png)

2. <span data-ttu-id="1b336-148">VM에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-148">Connect to the VM.</span></span>
3. <span data-ttu-id="1b336-149">VM에서 **파일 탐색기**를 열고 \inetpub\wwwroot로 이동한 다음, 파일 **iisstart.png**를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-149">On the VM, open **File Explorer** and navigate to \inetpub\wwwroot and delete the file **iisstart.png**.</span></span>
4. <span data-ttu-id="1b336-150">로컬 컴퓨터에서 브라우저를 새로 고쳐서 기본 IIS 페이지에 대한 이미지가 사라졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-150">On your local computer, refresh the browser to see that the image on the default IIS page is gone.</span></span>

    ![기본 IIS 웹 페이지](./media/tutorial-backup-vms/iis-broken.png)

5. <span data-ttu-id="1b336-152">로컬 컴퓨터에서 새 탭을 열고 [Azure Portal](https://portal.azure.com)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-152">On your local computer, open a new tab and go the the [Azure portal](https://portal.azure.com).</span></span>
6. <span data-ttu-id="1b336-153">왼쪽 메뉴에서 **가상 컴퓨터**를 선택하고 목록에서 VM 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-153">In the menu on the left, select **Virtual machines** and select the VM form the list.</span></span>
8. <span data-ttu-id="1b336-154">VM 블레이드의 **설정** 섹션에서 **백업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-154">On the VM blade, in the **Settings** section, click **Backup**.</span></span> <span data-ttu-id="1b336-155">**백업** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-155">The **Backup** blade opens.</span></span> 
9. <span data-ttu-id="1b336-156">블레이드 위쪽의 메뉴에서 **파일 복구**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-156">In the menu at the top of the blade, select **File Recovery**.</span></span> <span data-ttu-id="1b336-157">**파일 복구** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-157">The **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="1b336-158">**1단계: 복구 지점 선택**의 드롭다운에서 복구 지점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-158">In **Step 1: Select recovery point**, select a recovery point from the drop-down.</span></span>
11. <span data-ttu-id="1b336-159">**2단계: 스크립트를 다운로드하여 파일 찾아보기 및 복구**에서 **실행 파일 다운로드** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-159">In **Step 2: Download script to browse and recover files**, click the **Download Executable** button.</span></span> <span data-ttu-id="1b336-160">파일을 **다운로드** 폴더에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-160">Save the file to your **Downloads** folder.</span></span>
12. <span data-ttu-id="1b336-161">로컬 컴퓨터에서 **파일 탐색기**를 열고 **다운로드** 폴더로 이동하여 다운로드한 .exe 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-161">On your local computer, open **File Explorer** and navigate to your **Downloads** folder and copy the downloaded .exe file.</span></span> <span data-ttu-id="1b336-162">파일 이름은 VM 이름을 앞에 붙이게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-162">The filename will be prefixed by your VM name.</span></span> 
13. <span data-ttu-id="1b336-163">VM에서(RDP 연결을 통해) VM의 데스크톱에 .exe 파일을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-163">On your VM (over the RDP connection) paste the .exe file to the Desktop of your VM.</span></span> 
14. <span data-ttu-id="1b336-164">VM의 바탕 화면으로 이동한 다음 .exe를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-164">Navigate to the desktop of your VM and double-click on the .exe.</span></span> <span data-ttu-id="1b336-165">그러면 명령 프롬프트가 시작되고, 사용자가 액세스할 수 있는 파일 공유로 복구 지점을 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-165">This will launch a command prompt and then mount the recovery point as a file share that you can access.</span></span> <span data-ttu-id="1b336-166">공유 만들기가 끝나면 **q**를 입력하여 명령 프롬프트를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-166">When it is finished creating the share, type **q** to close the command prompt.</span></span>
15. <span data-ttu-id="1b336-167">VM에서 **파일 탐색기**를 열어 파일 공유에 사용된 드라이브 문자로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-167">On your VM, open **File Explorer** and navigate to the drive letter that was used for the file share.</span></span>
16. <span data-ttu-id="1b336-168">\inetpub\wwwroot로 이동하여 파일 공유의 **iisstart.png**를 복사하여 \inetpub\wwwroot에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-168">Navigate to \inetpub\wwwroot and copy **iisstart.png** from the file share and paste it into \inetpub\wwwroot.</span></span> <span data-ttu-id="1b336-169">예를 들어 F:\inetpub\wwwroot\iisstart.png를 복사하여 c:\inetpub\wwwroot에 붙여넣어 파일을 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-169">For example, copy F:\inetpub\wwwroot\iisstart.png and paste it into c:\inetpub\wwwroot to recover the file.</span></span>
17. <span data-ttu-id="1b336-170">로컬 컴퓨터에서 IIS 기본 페이지를 보여 주는 VM의 IP 주소에 연결된 브라우저 탭을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-170">On your local computer, open the browser tab where you are connected to the IP address of the VM showing the IIS default page.</span></span> <span data-ttu-id="1b336-171">CTRL+F5를 눌러 브라우저 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-171">Press CTRL + F5 to refresh the browser page.</span></span> <span data-ttu-id="1b336-172">이제 이미지가 복원되었음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-172">You should now see that the image has been restored.</span></span>
18. <span data-ttu-id="1b336-173">로컬 컴퓨터에서 Azure Portal의 브라우저 탭으로 돌아가서 **3단계: 복구 후 디스크 분리**에서 **디스크 분리** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-173">On your local computer, go back to the browser tab for the Azure portal and in **Step 3: Unmount the disks after recovery** click the **Unmount Disks** button.</span></span> <span data-ttu-id="1b336-174">이 단계를 수행하지 않으면 12시간 후에 탑재 지점에 대한 연결이 자동으로 끊깁니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-174">If you forget to do this step, the connection to the mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="1b336-175">12시간이 지나면 새 스크립트를 다운로드하여 새 탑재 지점을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-175">After those 12 hours, you need to download a new script to create a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1b336-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1b336-176">Next steps</span></span>

<span data-ttu-id="1b336-177">이 자습서에서는 다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-177">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1b336-178">VM 백업 만들기</span><span class="sxs-lookup"><span data-stu-id="1b336-178">Create a backup of a VM</span></span>
> * <span data-ttu-id="1b336-179">매일 백업 예약</span><span class="sxs-lookup"><span data-stu-id="1b336-179">Schedule a daily backup</span></span>
> * <span data-ttu-id="1b336-180">백업에서 파일 복원</span><span class="sxs-lookup"><span data-stu-id="1b336-180">Restore a file from a backup</span></span>

<span data-ttu-id="1b336-181">가상 컴퓨터 모니터링에 대해 알아보려면 다음 자습서로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="1b336-181">Advance to the next tutorial to learn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1b336-182">가상 컴퓨터 모니터링</span><span class="sxs-lookup"><span data-stu-id="1b336-182">Monitor virtual machines</span></span>](tutorial-monitoring.md)









