---
title: "Microsoft Azure 저장소 탐색기를 사용하여 Azure DevTest Labs에 VHD 파일 업로드 | Microsoft Docs"
description: "Microsoft Azure 저장소 탐색기를 사용하여 랩의 저장소 계정에 VHD 파일 업로드"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 502e2536fb0fd2e9dfc4c7b85a6fb4e18202f38f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-vhd-file-to-labs-storage-account-using-microsoft-azure-storage-explorer"></a><span data-ttu-id="ad905-103">Microsoft Azure 저장소 탐색기를 사용하여 랩의 저장소 계정에 VHD 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="ad905-103">Upload VHD file to lab's storage account using Microsoft Azure Storage Explorer</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="ad905-104">Azure DevTest Labs에서는 VHD 파일을 사용하여 가상 컴퓨터를 프로비저닝을 사용하는 데 사용하는 사용자 지정 이미지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-104">In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines.</span></span> <span data-ttu-id="ad905-105">이 문서에서는 [Microsoft Azure 저장소 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md)를 사용하여 랩의 저장소 계정에 VHD 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-105">This article illustrates how to use [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to upload a VHD file to a lab's storage account.</span></span> <span data-ttu-id="ad905-106">VHD 파일을 업로드하면 [다음 단계 섹션](#next-steps)은 업로드된 VHD 파일에서 사용자 지정 이미지를 만드는 방법을 자세히 설명하는 일부 문서를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-106">Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file.</span></span> <span data-ttu-id="ad905-107">Azure의 디스크 및 VHD에 대한 자세한 내용은 [가상 컴퓨터용 디스크 및 VHD 정보](../virtual-machines/linux/about-disks-and-vhds.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad905-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="ad905-108">단계별 지침</span><span class="sxs-lookup"><span data-stu-id="ad905-108">Step-by-step instructions</span></span>

<span data-ttu-id="ad905-109">다음 단계는 [Microsoft Azure 저장소 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md)를 사용하여 DevTest Labs로 VHD 파일을 업로드하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-109">The following steps walk you through uploading a VHD file to DevTest Labs using [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>

1. <span data-ttu-id="ad905-110">[Microsoft Azure 저장소 탐색기 최신 버전을 다운로드하여 설치합니다](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="ad905-110">[Download and install the latest version of the Microsoft Azure Storage Explorer](http://www.storageexplorer.com).</span></span>

1. <span data-ttu-id="ad905-111">Azure Portal을 사용하여 랩의 저장소 계정 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-111">Get the name of the lab's storage account using the Azure portal:</span></span>

    1. <span data-ttu-id="ad905-112">[Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-112">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
    
    1. <span data-ttu-id="ad905-113">**추가 서비스**를 선택한 후 목록에서 **DevTest Labs**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-113">Select **More services**, and then select **DevTest Labs** from the list.</span></span>
    
    1. <span data-ttu-id="ad905-114">랩 목록에서 원하는 랩을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-114">From the list of labs, select the desired lab.</span></span>  
    
    1. <span data-ttu-id="ad905-115">랩의 블레이드에서 **구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-115">On the lab's blade, select **Configuration**.</span></span> 
    
    1. <span data-ttu-id="ad905-116">랩의 **구성** 블레이드에서 **사용자 지정 이미지(VHD)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-116">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>
    
    1. <span data-ttu-id="ad905-117">**사용자 지정 이미지** 블레이드에서 **+추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-117">On the **Custom images** blade, Select **+Add**.</span></span> 
    
    1. <span data-ttu-id="ad905-118">**사용자 지정 이미지** 블레이드에서 **VHD**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-118">On the **Custom image** blade, select **VHD**.</span></span>
    
    1. <span data-ttu-id="ad905-119">**VHD** 블레이드에서 **PowerShell을 사용하여 VHD 업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-119">On the **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>
    
        ![PowerShell을 사용하여 VHD 업로드][0]
    
    1. <span data-ttu-id="ad905-121">**PowerShell을 사용하여 이미지 업로드** 블레이드는 **Add-AzureVhd** cmdlet에 대한 호출을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-121">The **Upload an image using PowerShell** blade displays a call to the **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="ad905-122">첫 번째 매개 변수(*대상*)는 다음 형식으로 랩에 대한 저장소 계정 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-122">The first parameter (*Destination*) contains the storage account name for the lab in the following format:</span></span>
    
        <span data-ttu-id="ad905-123">https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...</span><span class="sxs-lookup"><span data-stu-id="ad905-123">https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...</span></span> 

    1. <span data-ttu-id="ad905-124">이후 단계에서 사용되므로 저장소 계정 이름을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-124">Make note of the storage account name as it is used in later steps.</span></span>
    
1. <span data-ttu-id="ad905-125">저장소 탐색기를 사용하여 Azure 구독 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-125">Connect to an Azure subscription account using Storage Explorer.</span></span>

    > [!TIP] 
    > 
    > <span data-ttu-id="ad905-126">저장소 탐색기는 여러 가지 연결 옵션을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-126">Storage Explorer supports several connection options.</span></span> <span data-ttu-id="ad905-127">이 섹션에서는 Azure 구독과 연결된 저장소 계정에 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-127">This section illustrates connecting to a storage account associated with your Azure subscription.</span></span> <span data-ttu-id="ad905-128">저장소 탐색기에서 지원하는 다른 연결 옵션을 보려면 [저장소 탐색기 시작](../vs-azure-tools-storage-manage-with-storage-explorer.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad905-128">To see the other connection options supported by Storage Explorer, refer to the article, [Getting started with Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>
 
    1. <span data-ttu-id="ad905-129">저장소 탐색기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-129">Open Storage Explorer.</span></span>
    
    1. <span data-ttu-id="ad905-130">저장소 탐색기에서 **Azure 계정 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-130">In Storage Explorer, select **Azure Account settings**.</span></span> 
    
        ![Azure 계정 설정][1]
    
    1. <span data-ttu-id="ad905-132">왼쪽 창에 로그인한 Microsoft 계정이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-132">The left pane displays the Microsoft accounts you've logged in to.</span></span> <span data-ttu-id="ad905-133">다른 계정에 연결하려면 **계정 추가**를 선택하고 대화 상자를 따라서 하나 이상의 활성 Azure 구독에 연결된 Microsoft 계정을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-133">To connect to another account, select **Add an account**, and follow the dialogs to sign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>
    
        ![계정 추가][2]
    
    1. <span data-ttu-id="ad905-135">Microsoft 계정으로 성공적으로 로그인하면 왼쪽 창이 해당 계정과 연결된 Azure 구독으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-135">Once you successfully sign in with a Microsoft account, the left pane populates with the Azure subscriptions associated with that account.</span></span> <span data-ttu-id="ad905-136">작업하려는 Azure 구독을 선택한 후 **적용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-136">Select the Azure subscriptions with which you want to work, and then select **Apply**.</span></span> <span data-ttu-id="ad905-137">(나열된 Azure 구독을 모두 선택하거나 하나도 선택하지 않는 **모든 구독** 토글을 선택합니다.)</span><span class="sxs-lookup"><span data-stu-id="ad905-137">(Selecting **All subscriptions** toggles the selection of all or none of the listed Azure subscriptions.)</span></span>
    
        ![Azure 구독 선택][3]
    
    1. <span data-ttu-id="ad905-139">왼쪽 창은 선택한 Azure 구독과 연결된 저장소 계정을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-139">The left pane displays the storage accounts associated with the selected Azure subscriptions.</span></span>
    
        ![선택한 Azure 구독][4]

1. <span data-ttu-id="ad905-141">랩의 저장소 계정 찾기:</span><span class="sxs-lookup"><span data-stu-id="ad905-141">Locate the lab's storage account:</span></span>

    1. <span data-ttu-id="ad905-142">저장소 계정 왼쪽 창에서 랩을 소유한 Azure 구독에 해당하는 노드를 찾아 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-142">In the Storage Explorer left pane, locate, and expand the node for the Azure subscription that owns the lab.</span></span>
    
    1. <span data-ttu-id="ad905-143">구독 노드 아래에서 **저장소 계정**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-143">Under the subscription's node, expand **Storage Accounts**.</span></span>

    1. <span data-ttu-id="ad905-144">**Blob 컨테이너**, **파일 공유**, **큐** 및 **테이블**에 대한 노드가 나타나도록 랩의 저장소 계정 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-144">Expand the lab's storage account node to reveal nodes for **Blob Containers**, **File Shares**, **Queues**, and **Tables**.</span></span>
    
    1. <span data-ttu-id="ad905-145">**Blob 컨테이너** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-145">Expand the **Blob Containers** node.</span></span>
    
    1. <span data-ttu-id="ad905-146">오른쪽 창에 내용을 표시할 업로드 Blob 컨테이너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-146">Select the uploads blob container to display its contents in the right pane.</span></span>
        
        ![업로드 디렉터리][5]

1. <span data-ttu-id="ad905-148">저장소 탐색기를 사용하여 VHD 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="ad905-148">Upload the VHD file using Storage Explorer:</span></span>

    1. <span data-ttu-id="ad905-149">저장소 탐색기 오른쪽 창에 랩의 저장소 계정에 대한 **업로드** Blob 컨테이너에 Blob 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-149">In the Storage Explorer right pane, you should see a listing of the blobs in the **uploads** blob container of the lab's storage account.</span></span> <span data-ttu-id="ad905-150">Blob 편집기 도구 모음에서 **업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-150">On the blob editor toolbar, select **Upload**</span></span> 
        
        ![업로드 단추][6]
    
    1. <span data-ttu-id="ad905-152">**업로드** 드롭다운 메뉴에서 **파일 업로드...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-152">From the **Upload** drop-down menu, select **Upload files...**.</span></span>
    
    1. <span data-ttu-id="ad905-153">**파일 업로드** 대화 상자에서 줄임표를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-153">On the **Upload files** dialog, select the ellipsis.</span></span>
        
        ![파일 선택][8]  

    1. <span data-ttu-id="ad905-155">**업로드할 파일 선택** 대화 상자에서 원하는 VHD 파일을 찾아 선택한 후 **열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-155">On the **Select files to upload** dialog, browse to the desired VHD file, select it, and then select **Open**.</span></span>
    
    1. <span data-ttu-id="ad905-156">**파일 업로드** 대화 상자로 돌아가 **Blob 유형**을 **페이지 Blob**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-156">When returned to the **Upload files** dialog, change **Blob type** to **Page Blob**.</span></span>
    
    1. <span data-ttu-id="ad905-157">**업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-157">Select **Upload**.</span></span>

        ![파일 선택][9]  
    
    1. <span data-ttu-id="ad905-159">저장소 탐색기 **활동 로그** 창에 업로드 취소 링크와 함께 다운로드 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-159">The Storage Explorer **Activity Log** pane shows the download status (along with links to cancel the upload).</span></span> <span data-ttu-id="ad905-160">VHD 파일을 업로드하는 프로세스는 VHD 파일 크기 및 연결 속도에 따라 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad905-160">The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed.</span></span> 

        ![파일 업로드 상태][10]  

## <a name="next-steps"></a><span data-ttu-id="ad905-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ad905-162">Next steps</span></span>

- [<span data-ttu-id="ad905-163">Azure Portal을 사용하여 VHD 파일에서 Azure DevTest Labs에 사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="ad905-163">Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="ad905-164">PowerShell을 사용하여 VHD 파일에서 Azure DevTest Labs에 사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="ad905-164">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

[0]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-image-using-psh.png
[1]: ./media/devtest-lab-upload-vhd-using-storage-explorer/settings-icon.png
[2]: ./media/devtest-lab-upload-vhd-using-storage-explorer/add-account-link.png
[3]: ./media/devtest-lab-upload-vhd-using-storage-explorer/subscriptions-list.png
[4]: ./media/devtest-lab-upload-vhd-using-storage-explorer/storage-accounts-list.png
[5]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-dir.png
[6]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-button.png
[7]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-files.png
[8]: ./media/devtest-lab-upload-vhd-using-storage-explorer/select-file.png
[9]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-file.png
[10]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-status.png
