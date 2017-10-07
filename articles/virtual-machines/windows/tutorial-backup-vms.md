---
title: Windows Azure Vm aaaBackup | Microsoft Docs
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
ms.openlocfilehash: 1cd3e1940a83aacd160cba3c8613b63b6f3c11d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-virtual-machines-in-azure"></a><span data-ttu-id="52136-103">Azure에서 Windows 가상 컴퓨터 백업</span><span class="sxs-lookup"><span data-stu-id="52136-103">Back up Windows virtual machines in Azure</span></span>

<span data-ttu-id="52136-104">정기적으로 백업을 수행하여 데이터를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52136-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="52136-105">Azure Backup은 지역 중복 복구 자격 증명 모음에 저장되는 복구 지점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52136-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="52136-106">복원할 수는 복구 지점에서 복원할 때는 전체 VM 또는 특정 파일 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-106">When you restore from a recovery point, you can restore hello whole VM or just specific files.</span></span> <span data-ttu-id="52136-107">이 문서에서는 단일 toorestore tooa VM 파일 하는 방법을 설명 Windows 서버 및 IIS를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-107">This article explains how toorestore a single file tooa VM running Windows Server and IIS.</span></span> <span data-ttu-id="52136-108">VM toouse 없는 경우 하나를 만들 수 있습니다 hello를 사용 하 여 [Windows 퀵 스타트](quick-create-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-108">If you don't already have a VM toouse, you can create one using hello [Windows quickstart](quick-create-portal.md).</span></span> <span data-ttu-id="52136-109">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="52136-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="52136-110">VM 백업 만들기</span><span class="sxs-lookup"><span data-stu-id="52136-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="52136-111">매일 백업 예약</span><span class="sxs-lookup"><span data-stu-id="52136-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="52136-112">백업에서 파일 복원</span><span class="sxs-lookup"><span data-stu-id="52136-112">Restore a file from a backup</span></span>




## <a name="backup-overview"></a><span data-ttu-id="52136-113">백업 개요</span><span class="sxs-lookup"><span data-stu-id="52136-113">Backup overview</span></span>

<span data-ttu-id="52136-114">백업 작업을 시작 하는 hello Azure 백업 서비스 hello 예비 내선 번호 tootake를 지정 시간에 스냅숏으로 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-114">When hello Azure Backup service initiates a backup job, it triggers hello backup extension tootake a point-in-time snapshot.</span></span> <span data-ttu-id="52136-115">Azure 백업 서비스 hello hello를 사용 하 여 _VMSnapshot_ 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-115">hello Azure Backup service uses hello _VMSnapshot_ extension.</span></span> <span data-ttu-id="52136-116">hello 확장 hello VM을 실행 하는 경우 hello 첫 번째 VM 백업 하는 동안 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="52136-116">hello extension is installed during hello first VM backup if hello VM is running.</span></span> <span data-ttu-id="52136-117">Hello VM 실행 되지 않는 경우, hello 백업 서비스는 hello (응용 프로그램 쓰기가 수행 되지 hello VM을 중지 하는 동안) 이후 기본 저장소의 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52136-117">If hello VM is not running, hello Backup service takes a snapshot of hello underlying storage (since no application writes occur while hello VM is stopped).</span></span>

<span data-ttu-id="52136-118">Windows Vm의 스냅숏을 만드는, hello 백업 서비스 hello 가상 컴퓨터의 디스크의 일관 된 스냅숏을 hello 볼륨 섀도 복사본 서비스 (VSS) tooget와 동등 합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-118">When taking a snapshot of Windows VMs, hello Backup service coordinates with hello Volume Shadow Copy Service (VSS) tooget a consistent snapshot of hello virtual machine's disks.</span></span> <span data-ttu-id="52136-119">Hello Azure 백업 서비스는 hello 스냅숏을, 되 면 hello 데이터는 전송 된 toohello 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="52136-119">Once hello Azure Backup service takes hello snapshot, hello data is transferred toohello vault.</span></span> <span data-ttu-id="52136-120">toomaximize 효율성 hello 서비스를 식별 하 고 hello 이전 백업 이후에 변경 된 데이터의 hello 블록만 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-120">toomaximize efficiency, hello service identifies and transfers only hello blocks of data that have changed since hello previous backup.</span></span>

<span data-ttu-id="52136-121">Hello 데이터 전송이 완료 되 면 hello 스냅숏을 제거 되 고 복구 지점이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="52136-121">When hello data transfer is complete, hello snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="52136-122">백업 만들기</span><span class="sxs-lookup"><span data-stu-id="52136-122">Create a backup</span></span>
<span data-ttu-id="52136-123">간단한 예약 된 매일 백업 tooa 복구 서비스 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52136-123">Create a simple scheduled daily backup tooa Recovery Services Vault.</span></span> 

1. <span data-ttu-id="52136-124">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="52136-125">Hello hello 왼쪽 메뉴에서 선택 **가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-125">In hello menu on hello left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="52136-126">Hello 목록에서 VM tooback를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-126">From hello list, select a VM tooback up.</span></span>
4. <span data-ttu-id="52136-127">Hello에 hello VM 블레이드에서 **설정** 섹션에서 클릭 **백업**합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-127">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="52136-128">hello **백업 사용** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="52136-128">hello **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="52136-129">**복구 서비스 자격 증명 모음**, 클릭 **새로 만들기** hello hello 새 자격 증명 모음 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-129">In **Recovery Services vault**, click **Create new** and provide hello name for hello new vault.</span></span> <span data-ttu-id="52136-130">새 자격 증명 모음에서에서 만든 hello 동일한 리소스 그룹 및 hello 가상 컴퓨터로 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="52136-130">A new vault is created in hello same Resource Group and location as hello virtual machine.</span></span>
6. <span data-ttu-id="52136-131">**백업 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-131">Click **Backup policy**.</span></span> <span data-ttu-id="52136-132">이 예에서는 hello 기본값을 유지 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-132">For this example, keep hello defaults and click **OK**.</span></span>
7. <span data-ttu-id="52136-133">Hello에 **백업 사용** 블레이드에서 클릭 **백업 사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-133">On hello **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="52136-134">이렇게 하면 hello 기본 일정에 따라 매일 백업을 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="52136-134">This creates a daily backup based on hello default schedule.</span></span>
10. <span data-ttu-id="52136-135">초기 복구 지점 hello에 toocreate **백업** 블레이드 클릭 **지금 백업**합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-135">toocreate an initial recovery point, on hello **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="52136-136">Hello에 **지금 백업** 블레이드에서 hello 달력 아이콘을 hello 달력 컨트롤 tooselect hello 마지막 날이 복구 지점을 유지 하 고 클릭을 사용 하 여 **백업**합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-136">On hello **Backup Now** blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="52136-137">Hello에 **백업** 블레이드에서 VM에 대 한 완료 된 복구 지점 hello 수가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="52136-137">In hello **Backup** blade for your VM, you will see hello number of recovery points that are complete.</span></span>

    ![복구 지점](./media/tutorial-backup-vms/backup-complete.png)
    
<span data-ttu-id="52136-139">hello 첫 번째 백업에는 20 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="52136-139">hello first backup takes about 20 minutes.</span></span> <span data-ttu-id="52136-140">백업이 완료 된 후 toohello이이 자습서의 다음 단계를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-140">Proceed toohello next part of this tutorial after your backup is finished.</span></span>

## <a name="recover-a-file"></a><span data-ttu-id="52136-141">파일 복구</span><span class="sxs-lookup"><span data-stu-id="52136-141">Recover a file</span></span>

<span data-ttu-id="52136-142">실수로 삭제 하거나 변경 tooa 파일 확인을 하는 경우에 백업 자격 증명 모음에서 파일 복구 toorecover hello 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52136-142">If you accidentally delete or make changes tooa file, you can use File Recovery toorecover hello file from your backup vault.</span></span> <span data-ttu-id="52136-143">파일 복구 hello VM에서 실행 되는 스크립트를 사용 하 여 로컬 드라이브로 toomount hello 복구 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="52136-143">File Recovery uses a script that runs on hello VM, toomount hello recovery point as local drive.</span></span> <span data-ttu-id="52136-144">이러한 드라이브 남습니다 탑재 된 12 시간 동안 hello 복구 지점에서 파일을 복사 하 고 toohello VM을 복원할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-144">These drives will remain mounted for 12 hours so that you can copy files from hello recovery point and restore them toohello VM.</span></span>  

<span data-ttu-id="52136-145">이 예제에서는 toorecover IIS에 대 한 hello 기본 웹 페이지에 사용 되는 이미지 파일을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="52136-145">In this example, we show how toorecover hello image file that is used in hello default web page for IIS.</span></span> 

1. <span data-ttu-id="52136-146">브라우저를 열고 hello VM tooshow hello 기본 IIS 페이지의 toohello IP 주소를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-146">Open a browser and connect toohello IP address of hello VM tooshow hello default IIS page.</span></span>

    ![기본 IIS 웹 페이지](./media/tutorial-backup-vms/iis-working.png)

2. <span data-ttu-id="52136-148">Toohello VM을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-148">Connect toohello VM.</span></span>
3. <span data-ttu-id="52136-149">Hello VM에서 엽니다 **파일 탐색기** too\inetpub\wwwroot 이동 하 고 hello 파일을 삭제 하 고 **iisstart.png**합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-149">On hello VM, open **File Explorer** and navigate too\inetpub\wwwroot and delete hello file **iisstart.png**.</span></span>
4. <span data-ttu-id="52136-150">로컬 컴퓨터의 이미지 hello 기본 IIS 페이지 hello 새로 고침 hello 브라우저 toosee 사라지게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="52136-150">On your local computer, refresh hello browser toosee that hello image on hello default IIS page is gone.</span></span>

    ![기본 IIS 웹 페이지](./media/tutorial-backup-vms/iis-broken.png)

5. <span data-ttu-id="52136-152">로컬 컴퓨터에를 열고 새 탭 이동 hello hello [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-152">On your local computer, open a new tab and go hello hello [Azure portal](https://portal.azure.com).</span></span>
6. <span data-ttu-id="52136-153">Hello hello 왼쪽 메뉴에서 선택 **가상 컴퓨터** 및 선택 hello VM 양식 hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="52136-153">In hello menu on hello left, select **Virtual machines** and select hello VM form hello list.</span></span>
8. <span data-ttu-id="52136-154">Hello에 hello VM 블레이드에서 **설정** 섹션에서 클릭 **백업**합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-154">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="52136-155">hello **백업** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="52136-155">hello **Backup** blade opens.</span></span> 
9. <span data-ttu-id="52136-156">Hello hello 블레이드의 hello 위쪽 메뉴에서 선택 **파일 복구**합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-156">In hello menu at hello top of hello blade, select **File Recovery**.</span></span> <span data-ttu-id="52136-157">hello **파일 복구** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="52136-157">hello **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="52136-158">**1 단계: 복구 지점을 선택**를 hello 드롭다운 목록에서 복구 지점을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-158">In **Step 1: Select recovery point**, select a recovery point from hello drop-down.</span></span>
11. <span data-ttu-id="52136-159">**2 단계: 스크립트 toobrowse 다운로드 하 고 파일을 복구할**, hello 클릭 **실행 파일을 다운로드** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="52136-159">In **Step 2: Download script toobrowse and recover files**, click hello **Download Executable** button.</span></span> <span data-ttu-id="52136-160">Hello 파일 tooyour 저장 **다운로드** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="52136-160">Save hello file tooyour **Downloads** folder.</span></span>
12. <span data-ttu-id="52136-161">로컬 컴퓨터에서 엽니다 **파일 탐색기** tooyour 이동 **다운로드** 폴더 및 복사 hello.exe 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-161">On your local computer, open **File Explorer** and navigate tooyour **Downloads** folder and copy hello downloaded .exe file.</span></span> <span data-ttu-id="52136-162">VM 이름으로 접두사가 hello 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="52136-162">hello filename will be prefixed by your VM name.</span></span> 
13. <span data-ttu-id="52136-163">(RDP 연결 hello)를 통해 VM에 hello.exe 파일 toohello를 VM의 데스크톱에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="52136-163">On your VM (over hello RDP connection) paste hello .exe file toohello Desktop of your VM.</span></span> 
14. <span data-ttu-id="52136-164">VM의 toohello 데스크톱 이동한 hello.exe를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-164">Navigate toohello desktop of your VM and double-click on hello .exe.</span></span> <span data-ttu-id="52136-165">명령 프롬프트를 시작 되 고 액세스할 수 있는 파일 공유로 복구 지점을 hello를 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-165">This will launch a command prompt and then mount hello recovery point as a file share that you can access.</span></span> <span data-ttu-id="52136-166">완료 되 면 입력 hello 공유를 만들 **q** tooclose hello 명령 프롬프트입니다.</span><span class="sxs-lookup"><span data-stu-id="52136-166">When it is finished creating hello share, type **q** tooclose hello command prompt.</span></span>
15. <span data-ttu-id="52136-167">VM을 열고 **파일 탐색기** hello 파일 공유에 사용 된 toohello 드라이브 문자를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-167">On your VM, open **File Explorer** and navigate toohello drive letter that was used for hello file share.</span></span>
16. <span data-ttu-id="52136-168">복사 및 too\inetpub\wwwroot 탐색 **iisstart.png** hello 파일에서 공유 하 고 \inetpub\wwwroot에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="52136-168">Navigate too\inetpub\wwwroot and copy **iisstart.png** from hello file share and paste it into \inetpub\wwwroot.</span></span> <span data-ttu-id="52136-169">예를 들어 F:\inetpub\wwwroot\iisstart.png 복사한 c:\inetpub\wwwroot toorecover hello 파일에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="52136-169">For example, copy F:\inetpub\wwwroot\iisstart.png and paste it into c:\inetpub\wwwroot toorecover hello file.</span></span>
17. <span data-ttu-id="52136-170">로컬 컴퓨터에 연결 되어 있는 hello 브라우저 탭을 열고 toohello IP 주소를 hello VM hello IIS 기본 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-170">On your local computer, open hello browser tab where you are connected toohello IP address of hello VM showing hello IIS default page.</span></span> <span data-ttu-id="52136-171">CTRL + f 5를 눌러 toorefresh hello 브라우저 페이지.</span><span class="sxs-lookup"><span data-stu-id="52136-171">Press CTRL + F5 toorefresh hello browser page.</span></span> <span data-ttu-id="52136-172">이제 해당 hello 표시 이미지 복원 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="52136-172">You should now see that hello image has been restored.</span></span>
18. <span data-ttu-id="52136-173">로컬 컴퓨터에 돌아가서 toohello 브라우저 탭과 hello Azure 포털에 대 한 **3 단계: 복구 후 hello 디스크를 마운트 해제** hello 클릭 **디스크 분리** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="52136-173">On your local computer, go back toohello browser tab for hello Azure portal and in **Step 3: Unmount hello disks after recovery** click hello **Unmount Disks** button.</span></span> <span data-ttu-id="52136-174">이 단계를 toodo을 잊은 경우 hello 연결 toohello "탑재 지점" 닫혀 자동으로 12 시간 후입니다.</span><span class="sxs-lookup"><span data-stu-id="52136-174">If you forget toodo this step, hello connection toohello mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="52136-175">이러한 12 시간 후 새 스크립트 toocreate 새 "탑재 지점" toodownload를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-175">After those 12 hours, you need toodownload a new script toocreate a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="52136-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="52136-176">Next steps</span></span>

<span data-ttu-id="52136-177">이 자습서에서는 다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="52136-177">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="52136-178">VM 백업 만들기</span><span class="sxs-lookup"><span data-stu-id="52136-178">Create a backup of a VM</span></span>
> * <span data-ttu-id="52136-179">매일 백업 예약</span><span class="sxs-lookup"><span data-stu-id="52136-179">Schedule a daily backup</span></span>
> * <span data-ttu-id="52136-180">백업에서 파일 복원</span><span class="sxs-lookup"><span data-stu-id="52136-180">Restore a file from a backup</span></span>

<span data-ttu-id="52136-181">가상 컴퓨터를 모니터링 하는 방법에 대 한 다음 자습서 toolearn toohello를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="52136-181">Advance toohello next tutorial toolearn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="52136-182">가상 컴퓨터 모니터링</span><span class="sxs-lookup"><span data-stu-id="52136-182">Monitor virtual machines</span></span>](tutorial-monitoring.md)









