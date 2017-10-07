---
title: "Azure 저장소 계정, 컨테이너 또는 Vhd를 삭제 하면 aaaTroubleshoot 오류 | Microsoft Docs"
description: "Azure Storage 계정, 컨테이너 또는 VHD를 삭제하는 경우 발생하는 오류 문제 해결"
services: storage
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: storage
ms.assetid: 17403aa1-fe8d-45ec-bc33-2c0b61126286
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 77361593e2c924d39aba853e0807dc3188f50e60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a><span data-ttu-id="25bfe-103">Azure Storage 계정, 컨테이너 또는 VHD를 삭제하는 경우 발생하는 오류 문제 해결</span><span class="sxs-lookup"><span data-stu-id="25bfe-103">Troubleshoot errors when you delete Azure storage accounts, containers, or VHDs</span></span>

<span data-ttu-id="25bfe-104">오류가 발생할 수 있습니다는 Azure 저장소 계정, 컨테이너 또는 가상 하드 디스크 (VHD) toodelete 할 때 hello에 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-104">You might receive errors when you try toodelete an Azure storage account, container, or virtual hard disk (VHD) in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="25bfe-105">이 문서에서는 Azure 리소스 관리자 배포에서 가이드 toohelp 해결 hello 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-105">This article provides troubleshooting guidance toohelp resolve hello problem in an Azure Resource Manager deployment.</span></span>

<span data-ttu-id="25bfe-106">이 문서는 Azure 문제 해결 되지 않습니다를 방문 하 여 Azure 포럼에 hello [MSDN 및 스택 오버플로](https://azure.microsoft.com/support/forums/)합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-106">If this article doesn't address your Azure problem, visit hello Azure forums on [MSDN and Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="25bfe-107">이러한 포럼에 문제를 게시할 수 있습니다 또는 too@AzureSupport Twitter에서.</span><span class="sxs-lookup"><span data-stu-id="25bfe-107">You can post your problem on these forums or too@AzureSupport on Twitter.</span></span> <span data-ttu-id="25bfe-108">또한 선택 하 여 Azure 지원 요청을 제출할 수 있습니다 **지원을 받는** hello에 [Azure 지원](https://azure.microsoft.com/support/options/) 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-108">Also, you can file an Azure support request by selecting **Get support** on hello [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="25bfe-109">증상</span><span class="sxs-lookup"><span data-stu-id="25bfe-109">Symptoms</span></span>
### <a name="scenario-1"></a><span data-ttu-id="25bfe-110">시나리오 1</span><span class="sxs-lookup"><span data-stu-id="25bfe-110">Scenario 1</span></span>
<span data-ttu-id="25bfe-111">리소스 관리자 배포에서 저장소 계정에 VHD toodelete을 시도할 때 hello 다음과 같은 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-111">When you try toodelete a VHD in a storage account in a Resource Manager deployment, you receive hello following error message:</span></span>

<span data-ttu-id="25bfe-112">**Toodelete blob 'vhds/BlobName.vhd'에 실패 했습니다. 오류: 현재 임대에 hello blob 있고 hello 요청에 임대 ID가 없습니다. 지정 되었습니다.**</span><span class="sxs-lookup"><span data-stu-id="25bfe-112">**Failed toodelete blob 'vhds/BlobName.vhd'. Error: There is currently a lease on hello blob and no lease ID was specified in hello request.**</span></span>

<span data-ttu-id="25bfe-113">가상 컴퓨터 (VM) hello toodelete를 시도 하는 VHD 한 임 대권을 있으므로이 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-113">This problem can occur because a virtual machine (VM) has a lease on hello VHD that you are trying toodelete.</span></span>

### <a name="scenario-2"></a><span data-ttu-id="25bfe-114">시나리오 2</span><span class="sxs-lookup"><span data-stu-id="25bfe-114">Scenario 2</span></span>
<span data-ttu-id="25bfe-115">리소스 관리자 배포에서 저장소 계정에서 컨테이너 toodelete을 시도할 때 hello 다음과 같은 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-115">When you try toodelete a container in a storage account in a Resource Manager deployment, you receive hello following error message:</span></span>

<span data-ttu-id="25bfe-116">**Vhd를' toodelete 저장소 컨테이너'에 실패 했습니다. 오류: 현재 임대에 hello 컨테이너 있고 hello 요청에 임대 ID가 없습니다. 지정 되었습니다.**</span><span class="sxs-lookup"><span data-stu-id="25bfe-116">**Failed toodelete storage container 'vhds'. Error: There is currently a lease on hello container and no lease ID was specified in hello request.**</span></span>

<span data-ttu-id="25bfe-117">이 문제는 hello 컨테이너 임대 상태 hello에에서 잠겨 있는 VHD에 있기 때문에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-117">This problem can occur because hello container has a VHD that is locked in hello lease state.</span></span>

### <a name="scenario-3"></a><span data-ttu-id="25bfe-118">시나리오 3</span><span class="sxs-lookup"><span data-stu-id="25bfe-118">Scenario 3</span></span>
<span data-ttu-id="25bfe-119">리소스 관리자 배포에서 저장소 계정을 toodelete을 시도할 때 hello 다음과 같은 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-119">When you try toodelete a storage account in a Resource Manager deployment, you receive hello following error message:</span></span>

<span data-ttu-id="25bfe-120">**Toodelete 저장소 계정 'StorageAccountName'에 실패 했습니다. 오류: tooits 아티팩트가 사용 중이기 때문 hello 저장소 계정을 삭제할 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="25bfe-120">**Failed toodelete storage account 'StorageAccountName'. Error: hello storage account cannot be deleted due tooits artifacts being in use.**</span></span>

<span data-ttu-id="25bfe-121">이 문제는 hello 저장소 계정 hello 임대 상태에 있는 VHD를 포함 하기 때문에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-121">This problem can occur because hello storage account contains a VHD that is in hello lease state.</span></span>

## <a name="solution"></a><span data-ttu-id="25bfe-122">해결 방법</span><span class="sxs-lookup"><span data-stu-id="25bfe-122">Solution</span></span> 
<span data-ttu-id="25bfe-123">tooresolve hello VM에 연결 하 고 이러한 문제를 hello hello 오류가 발생 하는 VHD를 식별 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-123">tooresolve these problems, you must identify hello VHD that is causing hello error and hello associated VM.</span></span> <span data-ttu-id="25bfe-124">그런 다음 (데이터 디스크)에 대 한 hello VM에서에서 VHD hello를 분리 하거나 hello hello VHD (OS 디스크)를 사용 하는 VM을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-124">Then, detach hello VHD from hello VM (for data disks) or delete hello VM that is using hello VHD (for OS disks).</span></span> <span data-ttu-id="25bfe-125">이 hello 임대 hello VHD에서에서 제거 하 고 삭제 toobe 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-125">This removes hello lease from hello VHD and allows it toobe deleted.</span></span> 

<span data-ttu-id="25bfe-126">toodo,이 중 하나를이 사용 메서드를 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="25bfe-126">toodo this, use one of hello following methods:</span></span>

### <a name="method-1---use-azure-storage-explorer"></a><span data-ttu-id="25bfe-127">방법 1 - Azure Storage 탐색기 사용</span><span class="sxs-lookup"><span data-stu-id="25bfe-127">Method 1 - Use Azure storage explorer</span></span>

### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a><span data-ttu-id="25bfe-128">1 단계 확인 hello hello 저장소 계정 삭제를 방지 하는 VHD</span><span class="sxs-lookup"><span data-stu-id="25bfe-128">Step 1 Identify hello VHD that prevent deletion of hello storage account</span></span>

1. <span data-ttu-id="25bfe-129">Hello 저장소 계정을 삭제 하면 hello 다음과 같은 메시지 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-129">When you delete hello storage account, you will receive a message dialog such as hello following:</span></span> 

    ![hello 저장소 계정을 삭제할 때 메시지](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="25bfe-131">Hello 확인 **디스크 URL** tooidentify hello 저장소 계정 및 hello 하지 못한다는 VHD hello 저장소 계정을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-131">Check hello **Disk URL** tooidentify hello storage account and hello VHD that prevents you delete hello storage account.</span></span> <span data-ttu-id="25bfe-132">Hello 하기 전에 두 문자열의 다음 예제는 hello, ". blob.core.windows.net" hello 저장소 계정 이름이 며, "SCCM2012-2015-08-28.vhd" hello VHD 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-132">In hello following example, hello string before “.blob.core.windows.net “ is hello storage account name, and "SCCM2012-2015-08-28.vhd" is hello VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-hello-vhd-by-using-azure-storage-explorer"></a><span data-ttu-id="25bfe-133">Azure 저장소 탐색기를 사용 하 여 2 단계 삭제 hello VHD</span><span class="sxs-lookup"><span data-stu-id="25bfe-133">Step 2 Delete hello VHD by using Azure Storage Explorer</span></span>

1. <span data-ttu-id="25bfe-134">다운로드 및 설치 최신 버전의 hello [Azure 저장소 탐색기](http://storageexplorer.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-134">Download and Install hello latest version of [Azure Storage Explorer](http://storageexplorer.com/).</span></span> <span data-ttu-id="25bfe-135">이 도구는 microsoft Windows, macOS 및 Linux에서 데이터를 Azure 저장소 사용 tooeasily 작업을 허용 하는 독립 실행형 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-135">This tool is a standalone app from Microsoft that allows you tooeasily work with Azure Storage data on Windows, macOS and Linux.</span></span>
2. <span data-ttu-id="25bfe-136">Azure Storage 탐색기를 열고 왼쪽 막대에서</span><span class="sxs-lookup"><span data-stu-id="25bfe-136">Open Azure Storage Explorer, select</span></span> ![계정 아이콘](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) <span data-ttu-id="25bfe-138">hello 왼쪽된 모음에서 Azure 환경을 선택한 다음에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-138">on hello left bar, select your Azure environment, and then sign in.</span></span>

3. <span data-ttu-id="25bfe-139">모든 구독 또는 toodelete 원하는 hello 저장소 계정이 포함 된 hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-139">Select all subscriptions or hello subscription that contains hello storage account you want toodelete.</span></span>

    ![구독 추가](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. <span data-ttu-id="25bfe-141">Hello 디스크 URL 앞에서 hello에서를 얻 었 toohello 저장소 계정을 이동 **Blob 컨테이너** > **vhd** hello 저장소 계정을 삭제 하지 못한다는 VHD hello에 대 한 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-141">Go toohello storage account that we obtained from hello disk URL earlier, select hello **Blob Containers** > **vhds** and search for hello VHD that prevents you delete hello storage account.</span></span>
5. <span data-ttu-id="25bfe-142">Hello VHD 발견 되 면 hello 확인 **VM 이름** toofind hello VM이이 VHD를 사용 하는 열입니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-142">If hello VHD is found,  check hello **VM Name** column toofind hello VM that is using this VHD.</span></span>

    ![VM 확인](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. <span data-ttu-id="25bfe-144">Azure 포털을 사용 하 여 hello VHD에서에서 hello 임대를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-144">Remove hello lease from hello VHD by using Azure portal.</span></span> <span data-ttu-id="25bfe-145">자세한 내용은 참조 [hello VHD에서에서 제거 hello 임대](#remove-the-lease-from-the-vhd)합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-145">For more information, see [Remove hello lease from hello VHD](#remove-the-lease-from-the-vhd).</span></span> 

7. <span data-ttu-id="25bfe-146">Toohello Azure 저장소 탐색기로 이동 하 고 hello VHD를 마우스 오른쪽 단추로 클릭 한 다음 삭제를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-146">Go toohello Azure Storage Explorer, right-click hello VHD and then select delete.</span></span>

8. <span data-ttu-id="25bfe-147">Hello 저장소 계정을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-147">Delete hello storage account.</span></span>

### <a name="method-2---use-azure-portal"></a><span data-ttu-id="25bfe-148">방법 2 - Azure Portal 사용</span><span class="sxs-lookup"><span data-stu-id="25bfe-148">Method 2 - Use Azure portal</span></span> 

#### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a><span data-ttu-id="25bfe-149">1 단계: hello hello 저장소 계정 삭제를 방지 하는 VHD를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-149">Step 1: Identify hello VHD that prevent deletion of hello storage account</span></span>

1. <span data-ttu-id="25bfe-150">Hello 저장소 계정을 삭제 하면 hello 다음과 같은 메시지 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-150">When you delete hello storage account, you will receive a message dialog such as hello following:</span></span> 

    ![hello 저장소 계정을 삭제할 때 메시지](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="25bfe-152">Hello 확인 **디스크 URL** tooidentify hello 저장소 계정 및 hello 하지 못한다는 VHD hello 저장소 계정을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-152">Check hello **Disk URL** tooidentify hello storage account and hello VHD that prevents you delete hello storage account.</span></span> <span data-ttu-id="25bfe-153">Hello 하기 전에 두 문자열의 다음 예제는 hello, ". blob.core.windows.net" hello 저장소 계정 이름이 며, "SCCM2012-2015-08-28.vhd" hello VHD 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-153">In hello following example, hello string before “.blob.core.windows.net “ is hello storage account name, and "SCCM2012-2015-08-28.vhd" is hello VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. <span data-ttu-id="25bfe-154">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-154">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
3. <span data-ttu-id="25bfe-155">Hello 허브 메뉴에서 선택 **모든 리소스**합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-155">On hello Hub menu, select **All resources**.</span></span> <span data-ttu-id="25bfe-156">Toohello 저장소 계정을 선택한 후 선택 **Blob** > **vhd**합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-156">Go toohello storage account, and then select **Blobs** > **vhds**.</span></span>

    ![Hello 저장소 계정 및 강조 표시 하는 hello "vhd" 컨테이너와 hello 포털의 스크린샷](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. <span data-ttu-id="25bfe-158">Hello를 이전 hello 디스크 URL에서 가져온 VHD를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-158">Locate hello VHD that we obtained from hello disk URL earlier.</span></span> <span data-ttu-id="25bfe-159">그런 다음 VM을 사용 하 여 결정 VHD hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-159">Then, determine which VM is using hello VHD.</span></span> <span data-ttu-id="25bfe-160">일반적으로, VM hello VHD의 이름을 확인 하 여 hello VHD를 보유 하는 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-160">Usually, you can determine which VM holds hello VHD by checking name of hello VHD:</span></span>

<span data-ttu-id="25bfe-161">Resource Manager 개발 모델의 VM</span><span class="sxs-lookup"><span data-stu-id="25bfe-161">VM in Resource Manager development  model</span></span>

   * <span data-ttu-id="25bfe-162">OS 디스크는 일반적으로 VMName-YYYY-MM-DD-HHMMSS.vhd 명명 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-162">OS disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="25bfe-163">데이터 디스크는 일반적으로 VMName-YYYY-MM-DD-HHMMSS.vhd 명명 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-163">Data disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

<span data-ttu-id="25bfe-164">Classic 개발 모델의 VM</span><span class="sxs-lookup"><span data-stu-id="25bfe-164">VM in Classic development model</span></span>

   * <span data-ttu-id="25bfe-165">OS 디스크는 일반적으로 CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd 명명 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-165">OS disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="25bfe-166">데이터 디스크는 일반적으로 CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd 명명 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-166">Data disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

#### <a name="step-2-remove-hello-lease-from-hello-vhd"></a><span data-ttu-id="25bfe-167">2 단계: hello VHD에서에서 hello 임대를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-167">Step 2: Remove hello lease from hello VHD</span></span>

<span data-ttu-id="25bfe-168">[Hello 임대 hello VHD에서에서 제거](#remove-the-lease-from-the-vhd), 한 다음 hello 저장소 계정을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-168">[Remove hello lease from hello VHD](#remove-the-lease-from-the-vhd), and then delete hello storage account.</span></span>

## <a name="what-is-a-lease"></a><span data-ttu-id="25bfe-169">임대란?</span><span class="sxs-lookup"><span data-stu-id="25bfe-169">What is a lease?</span></span>
<span data-ttu-id="25bfe-170">임대는 사용 되는 toocontrol 액세스 tooa blob (VHD 등) 일 수 있는 잠금입니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-170">A lease is a lock that can be used toocontrol access tooa blob (for example, a VHD).</span></span> <span data-ttu-id="25bfe-171">Blob를 임대할 hello blob hello 임대의 hello 소유자만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-171">When a blob is leased, only hello owners of hello lease can access hello blob.</span></span> <span data-ttu-id="25bfe-172">임대가 이유 뒤 hello에 대 한 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-172">A lease is important for hello following reasons:</span></span>

* <span data-ttu-id="25bfe-173">여러 소유자 toowrite toohello 시도 하는 경우 데이터가 손상 되지 않게 hello에 hello blob의 동일한 부분이 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-173">It prevents data corruption if multiple owners try toowrite toohello same portion of hello blob at hello same time.</span></span>
* <span data-ttu-id="25bfe-174">Hello blob 항목 적극적으로 사용 하는 경우 (예를 들어 VM)이 삭제 되지 않도록 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-174">It prevents hello blob from being deleted if something is actively using it (for example, a VM).</span></span>
* <span data-ttu-id="25bfe-175">Hello 저장소 계정 항목 적극적으로 사용 하는 경우 (예를 들어 VM)이 삭제 되지 않도록 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-175">It prevents hello storage account from being deleted if something is actively using it (for example, a VM).</span></span>

### <a name="remove-hello-lease-from-hello-vhd"></a><span data-ttu-id="25bfe-176">Hello VHD에서에서 hello 임대를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-176">Remove hello lease from hello VHD</span></span>
<span data-ttu-id="25bfe-177">Hello VHD는 운영 체제 디스크를 hello VM tooremove hello 임대를 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-177">If hello VHD is an OS disk, you must delete hello VM tooremove hello lease:</span></span>

1. <span data-ttu-id="25bfe-178">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-178">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="25bfe-179">Hello에 **허브** 메뉴 선택 **가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-179">On hello **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="25bfe-180">Hello hello VHD에 임대를 보유 하는 VM을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-180">Select hello VM that holds a lease on hello VHD.</span></span>
4. <span data-ttu-id="25bfe-181">아무 것도 적극적으로 사용 hello 가상 컴퓨터와는 하면 더 이상 필요 hello 가상 컴퓨터를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-181">Make sure that nothing is actively using hello virtual machine, and that you no longer need hello virtual machine.</span></span>
5. <span data-ttu-id="25bfe-182">Hello의 hello 위쪽 **VM 세부 정보** 블레이드를 **삭제**, 클릭 하 고 **예** tooconfirm 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-182">At hello top of hello **VM details** blade, select **Delete**, and then click **Yes** tooconfirm.</span></span>
6. <span data-ttu-id="25bfe-183">hello VM은 삭제 되어야 하지만 hello VHD를 보존할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-183">hello VM should be deleted, but hello VHD can be retained.</span></span> <span data-ttu-id="25bfe-184">그러나 hello VHD 해야에 더 이상 없는 임대 것입니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-184">However, hello VHD should no longer have a lease on it.</span></span> <span data-ttu-id="25bfe-185">Hello 임대 toobe 출시 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-185">It may take a few minutes for hello lease toobe released.</span></span> <span data-ttu-id="25bfe-186">임대 hello tooverify 릴리스, 너무 이동**모든 리소스** > **저장소 계정 이름** > **Blob**  >  **vhd**합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-186">tooverify that hello lease is released, go too**All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="25bfe-187">Hello에 **속성 Blob** 창, hello **임대 상태** 값 해야 **잠금 해제 됨**합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-187">In hello **Blob properties** pane, hello **Lease Status** value should be **Unlocked**.</span></span>

<span data-ttu-id="25bfe-188">데이터 디스크 VHD hello 이면 hello VM tooremove hello 임대에서 hello VHD를 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-188">If hello VHD is a data disk, detach hello VHD from hello VM tooremove hello lease:</span></span>

1. <span data-ttu-id="25bfe-189">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-189">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="25bfe-190">Hello에 **허브** 메뉴 선택 **가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-190">On hello **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="25bfe-191">Hello hello VHD에 임대를 보유 하는 VM을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-191">Select hello VM that holds a lease on hello VHD.</span></span>
4. <span data-ttu-id="25bfe-192">선택 **디스크** hello에 **VM 세부 정보** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-192">Select **Disks** on hello **VM details** blade.</span></span>
5. <span data-ttu-id="25bfe-193">Hello VHD에 임대를 보유 하는 hello 데이터 디스크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-193">Select hello data disk that holds a lease on hello VHD.</span></span> <span data-ttu-id="25bfe-194">VHD에 연결 된 확인할 수 있습니다 hello VHD의 hello URL을 확인 하 여 hello 디스크.</span><span class="sxs-lookup"><span data-stu-id="25bfe-194">You can determine which VHD is attached in hello disk by checking hello URL of hello VHD.</span></span>
6. <span data-ttu-id="25bfe-195">아무 것도 적극적으로 사용 하 고 있는지 hello 데이터 디스크 확실 하 게 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-195">Determine with certainty that nothing is actively using hello data disk.</span></span>
7. <span data-ttu-id="25bfe-196">클릭 **분리** hello에 **세부 정보를 디스크** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-196">Click **Detach** on hello **Disk details** blade.</span></span>
8. <span data-ttu-id="25bfe-197">hello 디스크 VM hello에서 분리할 수 이제 해야 하며, VHD hello 더 이상 임대에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-197">hello disk should now be detached from hello VM, and hello VHD should no longer have a lease on it.</span></span> <span data-ttu-id="25bfe-198">Hello 임대 toobe 출시 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-198">It may take a few minutes for hello lease toobe released.</span></span> <span data-ttu-id="25bfe-199">해제 된 임대 hello tooverify, 너무 이동**모든 리소스** > **저장소 계정 이름** > **Blob**  >  **vhd**합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-199">tooverify that hello lease has been released, go too**All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="25bfe-200">Hello에 **속성 Blob** 창, hello **임대 상태** 값 해야 **잠금 해제 됨**합니다.</span><span class="sxs-lookup"><span data-stu-id="25bfe-200">In hello **Blob properties** pane, hello **Lease Status** value should be **Unlocked**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25bfe-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="25bfe-201">Next steps</span></span>
* [<span data-ttu-id="25bfe-202">저장소 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="25bfe-202">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
* [<span data-ttu-id="25bfe-203">Toobreak hello (PowerShell) Microsoft Azure에서 blob 저장소의 임대를 잠그는 방법을</span><span class="sxs-lookup"><span data-stu-id="25bfe-203">How toobreak hello locked lease of blob storage in Microsoft Azure (PowerShell)</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
