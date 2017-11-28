---
title: "Azure 저장소와 Azure PowerShell aaaUsing | Microsoft Docs"
description: "Toouse toocreate Azure 저장소에 대 한 Azure PowerShell cmdlet을 hello 하 및 저장소 계정, 관리 하는 방법을 알아봅니다 blob, 테이블, 큐 및 파일 사용 저장소 분석을 구성 및 쿼리하고 공유 액세스 서명을 생성 합니다."
services: storage
documentationcenter: na
author: robinsh
manager: timlt
ms.assetid: f4704f58-abc6-4f89-8b6d-1b1659746f5a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: befe7adda2384f8bcdb8b9f1a063e4eafc158271
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a><span data-ttu-id="1fbcc-103">Azure 저장소와 함께 Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="1fbcc-103">Using Azure PowerShell with Azure Storage</span></span>
## <a name="overview"></a><span data-ttu-id="1fbcc-104">개요</span><span class="sxs-lookup"><span data-stu-id="1fbcc-104">Overview</span></span>
<span data-ttu-id="1fbcc-105">Azure PowerShell은 cmdlet toomanage Windows PowerShell을 통해 Azure를 제공 하는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-105">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="1fbcc-106">작업 기반 명령줄 셸 및 시스템 관리를 위해 특별히 설계된 스크립트 언어로,</span><span class="sxs-lookup"><span data-stu-id="1fbcc-106">It is a task-based command-line shell and scripting language designed especially for system administration.</span></span> <span data-ttu-id="1fbcc-107">Powershell을 제어 하 고 Azure 서비스와 응용 프로그램의 hello 관리 자동화 쉽게 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-107">With PowerShell, you can easily control and automate hello administration of your Azure services and applications.</span></span> <span data-ttu-id="1fbcc-108">예를 들어 hello cmdlet tooperform hello hello를 통해 수행할 수 있는 동일한 작업을 사용할 수 있습니다 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-108">For example, you can use hello cmdlets tooperform hello same tasks that you can perform through hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="1fbcc-109">이 가이드에서는 살펴볼 것 어떻게 toouse hello [Azure 저장소 Cmdlet](/powershell/module/azurerm.storage/#storage) tooperform 다양 한 Azure 저장소와 개발 및 관리 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-109">In this guide, we'll explore how toouse hello [Azure Storage Cmdlets](/powershell/module/azurerm.storage/#storage) tooperform a variety of development and administration tasks with Azure Storage.</span></span>

<span data-ttu-id="1fbcc-110">이 가이드에서는 이전에 [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) 및 [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx)을 사용해 본 경험이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-110">This guide assumes that you have prior experience using [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) and [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span></span> <span data-ttu-id="1fbcc-111">hello 가이드 toodemonstrate hello 사용의 Azure 저장소에 있는 PowerShell 스크립트의 수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-111">hello guide provides a number of scripts toodemonstrate hello usage of PowerShell with Azure Storage.</span></span> <span data-ttu-id="1fbcc-112">각 스크립트를 실행 하기 전에 구성에 따라 hello 스크립트 변수를 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-112">You should update hello script variables based on your configuration before running each script.</span></span>

<span data-ttu-id="1fbcc-113">이 가이드의 hello 첫 번째 섹션에서 Azure 저장소 및 PowerShell 빠른 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-113">hello first section in this guide provides a quick glance at Azure Storage and PowerShell.</span></span> <span data-ttu-id="1fbcc-114">자세한 내용 및 지침은 hello에서 시작 [Azure PowerShell을 사용 하 여 Azure 저장소에 대 한 필수 구성 요소](#prerequisites-for-using-azure-powershell-with-azure-storage)합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-114">For detailed information and instructions, start from hello [Prerequisites for using Azure PowerShell with Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).</span></span>

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a><span data-ttu-id="1fbcc-115">5분 안에 Azure 저장소 및 PowerShell 시작하기</span><span class="sxs-lookup"><span data-stu-id="1fbcc-115">Getting started with Azure Storage and PowerShell in 5 minutes</span></span>
<span data-ttu-id="1fbcc-116">이 섹션에서는 5 분 후에 PowerShell 통해 Azure 저장소 tooaccess 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-116">This section shows you how tooaccess Azure Storage via PowerShell in 5 minutes.</span></span>

<span data-ttu-id="1fbcc-117">**새 tooAzure:** Microsoft Azure 구독 및 해당 구독과 연결 된 Microsoft 계정을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-117">**New tooAzure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="1fbcc-118">Azure 구입 옵션에 대한 자세한 내용은 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/), [구입 옵션](https://azure.microsoft.com/pricing/purchase-options/) 및 [회원 제안](https://azure.microsoft.com/pricing/member-offers/)(MSDN, Microsoft 파트너 네트워크, BizSpark 및 기타 Microsoft 프로그램의 회원인 경우)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="1fbcc-119">Azure 구독에 대한 자세한 내용은 [Azure AD(Azure Active Directory)에서 관리자 역할 할당](https://msdn.microsoft.com/library/azure/hh531793.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="1fbcc-120">**Microsoft Azure 구독 및 계정을 만든 후:**</span><span class="sxs-lookup"><span data-stu-id="1fbcc-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="1fbcc-121">다운로드 하 여 hello 최신 설치 [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest)합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-121">Download and install hello latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span></span>
2. <span data-ttu-id="1fbcc-122">시작 Windows PowerShell 통합된 스크립팅 환경 (ISE): 로컬 컴퓨터에서 이동 toohello **시작** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-122">Start Windows PowerShell Integrated Scripting Environment (ISE): In your local computer, go toohello **Start** menu.</span></span> <span data-ttu-id="1fbcc-123">형식 **관리 도구** toorun 클릭 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-123">Type **Administrative Tools** and click toorun it.</span></span> <span data-ttu-id="1fbcc-124">Hello에 **관리 도구** 창을 마우스 오른쪽 단추로 클릭 **Windows PowerShell ISE**, 클릭 **관리자 권한으로 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-124">In hello **Administrative Tools** window, right-click **Windows PowerShell ISE**, click **Run as Administrator**.</span></span>
3. <span data-ttu-id="1fbcc-125">**Windows PowerShell ISE**, 클릭 **파일** > **새로** toocreate 새 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-125">In **Windows PowerShell ISE**, click **File** > **New** toocreate a new script file.</span></span>
4. <span data-ttu-id="1fbcc-126">이제 기본 PowerShell 명령을 tooaccess Azure 저장소를 보여 주는 간단한 스크립트를 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-126">Now, we'll give you a simple script that shows basic PowerShell commands tooaccess Azure Storage.</span></span> <span data-ttu-id="1fbcc-127">hello 스크립트 Azure 계정 자격 증명 tooadd Azure 계정 toohello 로컬 PowerShell 환경을 요청 우선 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-127">hello script will first ask your Azure account credentials tooadd your Azure account toohello local PowerShell environment.</span></span> <span data-ttu-id="1fbcc-128">그런 다음 hello 스크립트 hello 기본 Azure 구독 설정 하 고 Azure에서 새 저장소 계정을 만드는 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-128">Then, hello script will set hello default Azure subscription and create a new storage account in Azure.</span></span> <span data-ttu-id="1fbcc-129">다음으로 hello 스크립트는 새 컨테이너를이 새 저장소 계정에서 만들고 기존 이미지 파일 (blob) toothat 컨테이너를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-129">Next, hello script will create a new container in this new storage account and upload an existing image file (blob) toothat container.</span></span> <span data-ttu-id="1fbcc-130">해당 컨테이너의 모든 blob를 나열 하는 hello 스크립트, 후 로컬 컴퓨터에서 새 대상 디렉터리를 만들 되며 hello 이미지 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-130">After hello script lists all blobs in that container, it will create a new destination directory in your local computer and download hello image file.</span></span>
5. <span data-ttu-id="1fbcc-131">다음 코드 섹션 hello에서 hello 설명 간의 hello 스크립트를 선택 **#begin** 및 **#end**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-131">In hello following code section, select hello script between hello remarks **#begin** and **#end**.</span></span> <span data-ttu-id="1fbcc-132">Toocopy CTRL + C를 눌러 해당 toohello 클립보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-132">Press CTRL+C toocopy it toohello clipboard.</span></span>

    ```powershell
    # begin
    # Update with hello name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name tooyour new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name tooyour new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account toohello local PowerShell environment.
    Add-AzureAccount
       
    # Set a default Azure subscription.
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
       
    # Create a new storage account.
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $Location
       
    # Set a default storage account.
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
       
    # Create a new container.
    New-AzureStorageContainer -Name $ContainerName -Permission Off
       
    # Upload a blob into a container.
    Set-AzureStorageBlobContent -Container $ContainerName -File $ImageToUpload
       
    # List all blobs in a container.
    Get-AzureStorageBlob -Container $ContainerName
       
    # Download blobs from hello container:
    # Get a reference tooa list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create hello destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into hello local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. <span data-ttu-id="1fbcc-133">**Windows PowerShell ISE**, CTRL + V toocopy hello 스크립트 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-133">In **Windows PowerShell ISE**, press CTRL+V toocopy hello script.</span></span> <span data-ttu-id="1fbcc-134">**파일** > **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-134">Click **File** > **Save**.</span></span> <span data-ttu-id="1fbcc-135">Hello에 **다른 이름으로 저장** 대화 상자 창에서 "mystoragescript."와 같은 hello 스크립트 파일의 형식 hello 이름</span><span class="sxs-lookup"><span data-stu-id="1fbcc-135">In hello **Save As** dialog window, type hello name of hello script file, such as "mystoragescript."</span></span> <span data-ttu-id="1fbcc-136">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-136">Click **Save**.</span></span>
7. <span data-ttu-id="1fbcc-137">이제, 구성 설정에 기반 하 여 tooupdate hello 스크립트 변수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-137">Now, you need tooupdate hello script variables based on your configuration settings.</span></span> <span data-ttu-id="1fbcc-138">Hello를 업데이트 해야 **$SubscriptionName** 변수를 사용자의 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-138">You must update hello **$SubscriptionName** variable with your own subscription.</span></span> <span data-ttu-id="1fbcc-139">Hello 스크립트에 지정 된 대로 다른 변수 hello를 유지 하거나 원하는 대로 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-139">You can keep hello other variables as specified in hello script or update them as you wish.</span></span>
   
   * <span data-ttu-id="1fbcc-140">**$SubscriptionName:** 변수를 사용자 고유의 구독 이름으로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-140">**$SubscriptionName:** You must update this variable with your own subscription name.</span></span> <span data-ttu-id="1fbcc-141">Hello 구독의 세 가지 방법으로 toolocate hello 이름 다음의 하나를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-141">Follow one of hello following three ways toolocate hello name of your subscription:</span></span>
     
    <span data-ttu-id="1fbcc-142">a.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-142">a.</span></span> <span data-ttu-id="1fbcc-143">**Windows PowerShell ISE**, 클릭 **파일** > **새로** toocreate 새 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-143">In **Windows PowerShell ISE**, click **File** > **New** toocreate a new script file.</span></span> <span data-ttu-id="1fbcc-144">복사 hello 다음 스크립트 toohello 새 스크립트 파일을 클릭 하 여 **디버그** > **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-144">Copy hello following script toohello new script file and click **Debug** > **Run**.</span></span> <span data-ttu-id="1fbcc-145">hello 다음 스크립트는 먼저 Azure 계정 자격 증명 tooadd Azure 계정 toohello 로컬 PowerShell 환경 묻고 모든 hello 구독 연결된 toohello 로컬 PowerShell 세션을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-145">hello following script will first ask your Azure account credentials tooadd your Azure account toohello local PowerShell environment and then show all hello subscriptions that are connected toohello local PowerShell session.</span></span> <span data-ttu-id="1fbcc-146">이 자습서를 수행 하면서 toouse 되도록 hello 구독의 hello 이름 메모를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-146">Take a note of hello name of hello subscription that you want toouse while following this tutorial:</span></span>
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    <span data-ttu-id="1fbcc-147">b.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-147">b.</span></span> <span data-ttu-id="1fbcc-148">hello에서 구독 이름을 toolocate 및 복사 [Azure 포털](https://portal.azure.com)hello hello 왼쪽에 허브 메뉴에서 클릭 **구독**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-148">toolocate and copy your subscription name in hello [Azure portal](https://portal.azure.com), in hello Hub menu on hello left, click **Subscriptions**.</span></span> <span data-ttu-id="1fbcc-149">이 가이드의 hello 스크립트를 실행 하는 동안 toouse 되도록 구독 hello 이름을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-149">Copy hello name of subscription that you want toouse while running hello scripts in this guide.</span></span>
     
     ![Azure portal](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    <span data-ttu-id="1fbcc-151">c.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-151">c.</span></span> <span data-ttu-id="1fbcc-152">hello에서 구독 이름을 toolocate 및 복사 [Azure 클래식 포털](https://manage.windowsazure.com/), 아래로 스크롤하여 클릭 **설정을** hello hello 포털의 왼쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-152">toolocate and copy your subscription name in hello [Azure Classic Portal](https://manage.windowsazure.com/), scroll down and click **Settings** on hello left side of hello portal.</span></span> <span data-ttu-id="1fbcc-153">클릭 **구독** toosee 구독 목록이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-153">Click **Subscriptions** toosee a list of your subscriptions.</span></span> <span data-ttu-id="1fbcc-154">이 가이드에서 제공 하는 hello 스크립트를 실행 하는 동안 toouse를 원하는 구독의 hello 이름을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-154">Copy hello name of subscription that you want toouse while running hello scripts given in this guide.</span></span>
     
     ![Azure 클래식 포털](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * <span data-ttu-id="1fbcc-156">**$StorageAccountName:** hello 스크립트에 이름이 지정 된 hello를 사용 하거나 저장소 계정에 대 한 새 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-156">**$StorageAccountName:** Use hello given name in hello script or enter a new name for your storage account.</span></span> <span data-ttu-id="1fbcc-157">**중요:** hello hello 저장소 계정의 이름으로 Azure에서 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-157">**Important:** hello name of hello storage account must be unique in Azure.</span></span> <span data-ttu-id="1fbcc-158">소문자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-158">It must be lowercase, too!</span></span>
   * <span data-ttu-id="1fbcc-159">**$Location:** hello 스크립트에 제공 "West US" hello를 사용 하거나 미국 동부, 유럽 북부, 등 다른 Azure 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-159">**$Location:** Use hello given "West US" in hello script or choose other Azure locations, such as East US, North Europe, and so on.</span></span>
   * <span data-ttu-id="1fbcc-160">**$ContainerName:** hello 스크립트에 이름이 지정 된 hello를 사용 하거나 컨테이너에 대해 새 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-160">**$ContainerName:** Use hello given name in hello script or enter a new name for your container.</span></span>
   * <span data-ttu-id="1fbcc-161">**$ImageToUpload:** 로컬 컴퓨터에 같은 경로 tooa 그림을 입력: "C:\Images\HelloWorld.png"입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-161">**$ImageToUpload:** Enter a path tooa picture on your local computer, such as: "C:\Images\HelloWorld.png".</span></span>
   * <span data-ttu-id="1fbcc-162">**$DestinationFolder:** Enter와 같은 Azure 저장소에서 다운로드 경로 tooa 로컬 디렉터리 toostore 파일: "C:\DownloadImages"입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-162">**$DestinationFolder:** Enter a path tooa local directory toostore files downloaded from Azure Storage, such as: "C:\DownloadImages".</span></span>
8. <span data-ttu-id="1fbcc-163">Hello "mystoragescript.ps1" 파일에 있는 hello 스크립트 변수를 업데이트 한 후 클릭 **파일** > **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-163">After updating hello script variables in hello "mystoragescript.ps1" file, click **File** > **Save**.</span></span> <span data-ttu-id="1fbcc-164">클릭 **디버그** > **실행** 하거나 키를 눌러 **F5** toorun hello 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-164">Then, click **Debug** > **Run** or press **F5** toorun hello script.</span></span>  

<span data-ttu-id="1fbcc-165">Hello 스크립트를 실행 한 후 다운로드 한 hello 이미지 파일을 포함 하는 로컬 대상 폴더가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-165">After hello script runs, you should have a local destination folder that includes hello downloaded image file.</span></span> <span data-ttu-id="1fbcc-166">다음 스크린 샷 hello 출력을 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-166">hello following screenshot shows an example output:</span></span>

![Blob 다운로드](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> <span data-ttu-id="1fbcc-168">hello "Azure 저장소 및 시작 PowerShell 5 분 이내에" 섹션에 제공 된 간략 한 소개 방법 toouse Azure 저장소와 Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-168">hello "Getting started with Azure Storage and PowerShell in 5 minutes" section provided a quick introduction on how toouse Azure PowerShell with Azure Storage.</span></span> <span data-ttu-id="1fbcc-169">자세한 내용 및 지침은 좋습니다 tooread hello를 다음 섹션.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-169">For detailed information and instructions, we encourage you tooread hello following sections.</span></span>
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a><span data-ttu-id="1fbcc-170">Azure 저장소에서 Azure PowerShell을 사용하기 위한 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="1fbcc-170">Prerequisites for using Azure PowerShell with Azure Storage</span></span>
<span data-ttu-id="1fbcc-171">위에서 설명한 것 처럼는 Azure 구독 및 계정 toorun hello PowerShell cmdlet이이 가이드에 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-171">You need an Azure subscription and account toorun hello PowerShell cmdlets given in this guide, as described above.</span></span>

<span data-ttu-id="1fbcc-172">Azure PowerShell은 cmdlet toomanage Windows PowerShell을 통해 Azure를 제공 하는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-172">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="1fbcc-173">설치 및 Azure PowerShell을 설정에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-173">For information on installing and setting up Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="1fbcc-174">다운로드 및 설치 하거나는 toohello 최신 Azure PowerShell 모듈을이 가이드를 사용 하기 전에 업그레이드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-174">We recommend that you download and install or upgrade toohello latest Azure PowerShell module before using this guide.</span></span>

<span data-ttu-id="1fbcc-175">Hello 표준 Windows PowerShell 콘솔 또는 Windows PowerShell 통합 스크립팅 환경 (ISE) hello hello cmdlet을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-175">You can run hello cmdlets in hello standard Windows PowerShell console or hello Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="1fbcc-176">예를 들어 tooopen **Windows PowerShell ISE**toohello 시작 메뉴를 이동, 관리 도구를 입력 한 toorun 클릭 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-176">For example, tooopen **Windows PowerShell ISE**, go toohello Start menu, type Administrative Tools and click toorun it.</span></span> <span data-ttu-id="1fbcc-177">Hello 관리 도구 창 Windows PowerShell ISE를 마우스 오른쪽 단추로 클릭 하 고 관리자 권한으로 실행을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-177">In hello Administrative Tools window, right-click Windows PowerShell ISE, click Run as Administrator.</span></span>

## <a name="how-toomanage-storage-accounts-in-azure"></a><span data-ttu-id="1fbcc-178">Azure에서 toomanage 저장소 계정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1fbcc-178">How toomanage storage accounts in Azure</span></span>

<span data-ttu-id="1fbcc-179">PowerShell 사용한 Azure에서 저장소 계정 관리에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-179">Let's take a look at managing storage accounts in Azure with PowerShell</span></span>

### <a name="how-tooset-a-default-azure-subscription"></a><span data-ttu-id="1fbcc-180">어떻게 tooset 기본 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="1fbcc-180">How tooset a default Azure subscription</span></span>
<span data-ttu-id="1fbcc-181">Azure PowerShell을 사용 하 여 Azure 저장소의 경우 필요한 tooauthenticate Azure Active Directory 인증 또는 인증서 기반 인증을 통해 Azure 사용 하 여 클라이언트 환경 toomanage 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-181">toomanage Azure Storage using Azure PowerShell, you need tooauthenticate your client environment with Azure via Azure Active Directory authentication or certificate-based authentication.</span></span> <span data-ttu-id="1fbcc-182">자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-182">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tutorial.</span></span> <span data-ttu-id="1fbcc-183">이 가이드에서는 hello Azure Active Directory 인증을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-183">This guide uses hello Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="1fbcc-184">Windows PowerShell ISE에서 다음 명령을 tooadd hello Azure 계정 toohello 로컬 PowerShell 환경을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-184">In Windows PowerShell ISE, type hello following command tooadd your Azure account toohello local PowerShell environment:</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="1fbcc-185">Hello "tooMicrosoft Azure에에서 로그인" 창, hello 전자 메일 주소를 입력 및 해당 계정과 연결 된 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-185">In hello "Sign in tooMicrosoft Azure" window, type hello email address and password associated with your account.</span></span> <span data-ttu-id="1fbcc-186">Azure 인증 및 hello 자격 증명 정보를 저장 하 고 hello 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-186">Azure authenticates and saves hello credential information, and then closes hello window.</span></span>

3. <span data-ttu-id="1fbcc-187">다음 명령은 tooview hello Azure 로컬 PowerShell 환경에서 계정 및 계정 나열 되어 있는지 확인 하는 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-187">Next, run hello following command tooview hello Azure accounts in your local PowerShell environment, and verify that your account is listed:</span></span>
   
    ```powershell
    Get-AzureAccount
    ```
4. <span data-ttu-id="1fbcc-188">그런 다음, hello cmdlet tooview 다음 모든 hello 구독 연결된 toohello 로컬 PowerShell 세션을 실행 하 고 구독 나열 되어 있는지 확인:</span><span class="sxs-lookup"><span data-stu-id="1fbcc-188">Then, run hello following cmdlet tooview all hello subscriptions that are connected toohello local PowerShell session, and verify that your subscription is listed:</span></span>

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. <span data-ttu-id="1fbcc-189">tooset 기본 Azure 구독 hello Select-azuresubscription cmdlet을 실행 하는 중:</span><span class="sxs-lookup"><span data-stu-id="1fbcc-189">tooset a default Azure subscription, run hello Select-AzureSubscription cmdlet:</span></span>

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. <span data-ttu-id="1fbcc-190">Hello Get-azuresubscription cmdlet을 실행 하 여 hello hello 기본 구독 이름을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-190">Verify hello name of hello default subscription by running hello Get-AzureSubscription cmdlet:</span></span>

    ```powershell
    Get-AzureSubscription -Default
    ```

7. <span data-ttu-id="1fbcc-191">사용할 수 있는 PowerShell cmdlet을 실행 하는 Azure 저장소에 대 한 hello 모든 toosee:</span><span class="sxs-lookup"><span data-stu-id="1fbcc-191">toosee all hello available PowerShell cmdlets for Azure Storage, run:</span></span>
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-toocreate-a-new-azure-storage-account"></a><span data-ttu-id="1fbcc-192">어떻게 toocreate 새 Azure 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="1fbcc-192">How toocreate a new Azure storage account</span></span>
<span data-ttu-id="1fbcc-193">Azure 저장소 toouse 저장소 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-193">toouse Azure storage, you will need a storage account.</span></span> <span data-ttu-id="1fbcc-194">컴퓨터 tooconnect tooyour 구독을 구성한 후 새 Azure 저장소 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-194">You can create a new Azure storage account after you have configured your computer tooconnect tooyour subscription.</span></span>

1. <span data-ttu-id="1fbcc-195">Hello Get AzureLocation cmdlet toofind 모든 hello 사용 가능한 데이터 센터 위치를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-195">Run hello Get-AzureLocation cmdlet toofind all hello available datacenter locations:</span></span>

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. <span data-ttu-id="1fbcc-196">다음으로 hello 새로 AzureStorageAccount cmdlet toocreate를 새 저장소 계정을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-196">Next, run hello New-AzureStorageAccount cmdlet toocreate a new storage account.</span></span> <span data-ttu-id="1fbcc-197">hello 다음 예제에서는 새 저장소 계정을 만듭니다 hello "West US" 데이터 센터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-197">hello following example creates a new storage account in hello "West US" datacenter.</span></span>
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> <span data-ttu-id="1fbcc-198">사용자의 저장소 계정 hello 이름은 Azure 내에서 고유 해야 하며 소문자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-198">hello name of your storage account must be unique within Azure and must be lowercase.</span></span> <span data-ttu-id="1fbcc-199">명명 규칙 및 제한에 대해서는 [Azure Storage 계정 정보](storage-create-storage-account.md) 및 [컨테이너, Blob, 메타데이터 이름 명명 및 참조](http://msdn.microsoft.com/library/azure/dd135715.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-199">For naming conventions and restrictions, see [About Azure Storage Accounts](storage-create-storage-account.md) and [Naming and Referencing Containers, Blobs, and Metadata](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span></span>
> 
> 

### <a name="how-tooset-a-default-azure-storage-account"></a><span data-ttu-id="1fbcc-200">어떻게 tooset 기본 Azure 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="1fbcc-200">How tooset a default Azure storage account</span></span>
<span data-ttu-id="1fbcc-201">구독에서 여러 저장소 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-201">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="1fbcc-202">그 중 하나를 선택 하 고 hello 기본 저장소 계정 저장소 모든 hello에 대 한 명령을 hello에 동일한으로 설정할 수 있습니다 PowerShell 세션입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-202">You can choose one of them and set it as hello default storage account for all hello storage commands in hello same PowerShell session.</span></span> <span data-ttu-id="1fbcc-203">이렇게 하면 toorun hello Azure PowerShell 저장소 명령을 hello 저장소 컨텍스트를 명시적으로 지정 하지 않고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-203">This enables you toorun hello Azure PowerShell storage commands without specifying hello storage context explicitly.</span></span>

1. <span data-ttu-id="1fbcc-204">구독에 대 한 기본 저장소 계정을 tooset hello 집합 AzureSubscription cmdlet을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-204">tooset a default storage account for your subscription, you can run hello Set-AzureSubscription cmdlet.</span></span>

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. <span data-ttu-id="1fbcc-205">그런 다음, hello Get-azuresubscription cmdlet tooverify hello 저장소 계정의 기본 구독 계정에 연결 되어 있는지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-205">Next, run hello Get-AzureSubscription cmdlet tooverify that hello storage account is associated with your default subscription account.</span></span> <span data-ttu-id="1fbcc-206">이 명령은 현재 저장소 계정을 포함 하 여 hello 현재 구독에서 hello 구독 속성을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-206">This command returns hello subscription properties on hello current subscription including its current storage account.</span></span>

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-toolist-all-azure-storage-accounts-in-a-subscription"></a><span data-ttu-id="1fbcc-207">어떻게 toolist 모든 Azure 저장소 계정에 구독</span><span class="sxs-lookup"><span data-stu-id="1fbcc-207">How toolist all Azure storage accounts in a subscription</span></span>
<span data-ttu-id="1fbcc-208">각 Azure 구독 too100 저장소 계정이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-208">Each Azure subscription can have up too100 storage accounts.</span></span> <span data-ttu-id="1fbcc-209">Hello 제한에 최신 정보를 참조 하십시오. [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-209">For hello most up-to-date information on limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="1fbcc-210">Hello hello 이름과 hello 현재 구독에 대 한 hello 저장소 계정의 상태 아웃 cmdlet toofind 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-210">Run hello following cmdlet toofind out hello name and status of hello storage accounts in hello current subscription:</span></span>

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-toocreate-an-azure-storage-context"></a><span data-ttu-id="1fbcc-211">어떻게 toocreate Azure 저장소 컨텍스트</span><span class="sxs-lookup"><span data-stu-id="1fbcc-211">How toocreate an Azure storage context</span></span>
<span data-ttu-id="1fbcc-212">Azure 저장소 컨텍스트가 PowerShell tooencapsulate hello 저장소 자격 증명에는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-212">Azure storage context is an object in PowerShell tooencapsulate hello storage credentials.</span></span> <span data-ttu-id="1fbcc-213">Hello 저장소 계정 및 액세스 키를 명시적으로 지정 하지 않고 있습니다 tooauthenticate 요청을 통해 저장소 컨텍스트를 사용 하 여 모든 후속 cmdlet을 실행 하는 동안 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-213">Using a storage context while running any subsequent cmdlet enables you tooauthenticate your request without specifying hello storage account and its access key explicitly.</span></span> <span data-ttu-id="1fbcc-214">저장소 계정 이름과 액세스 키, SAS(공유 액세스 서명) 토큰, 연결 문자열, 익명 등을 다양한 방식으로 저장소 컨텍스트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-214">You can create a storage context in many ways, such as using storage account name and access key, shared access signature (SAS) token, connection string, or anonymous.</span></span> <span data-ttu-id="1fbcc-215">자세한 내용은 [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-215">For more information, see [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span></span>  

<span data-ttu-id="1fbcc-216">저장소 컨텍스트 hello 세 가지 방법으로 toocreate 다음 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-216">Use one of hello following three ways toocreate a storage context:</span></span>

* <span data-ttu-id="1fbcc-217">Hello 실행 [Get AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet toofind Azure 저장소 계정에 대 한 기본 저장소 액세스 키 hello 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-217">Run hello [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet toofind out hello primary storage access key for your Azure storage account.</span></span> <span data-ttu-id="1fbcc-218">그런 다음 호출 하는 hello [새로 AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet toocreate 저장소 컨텍스트:</span><span class="sxs-lookup"><span data-stu-id="1fbcc-218">Next, call hello [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet toocreate a storage context:</span></span>

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* <span data-ttu-id="1fbcc-219">Azure 저장소 컨테이너에 대 한 공유 액세스 서명 토큰을 생성 하 고 toocreate 저장소 컨텍스트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-219">Generate a shared access signature token for an Azure storage container and use it toocreate a storage context:</span></span>

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    <span data-ttu-id="1fbcc-220">자세한 내용은 [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) 및 [SAS(공유 액세스 서명) 사용](storage-dotnet-shared-access-signature-part-1.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-220">For more information, see [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) and [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span></span>

* <span data-ttu-id="1fbcc-221">일부 경우에 새 저장소 컨텍스트를 만들 때 toospecify hello 서비스 끝점을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-221">In some cases, you may want toospecify hello service endpoints when you create a new storage context.</span></span> <span data-ttu-id="1fbcc-222">저장소 계정에 대 한 사용자 지정 도메인 이름을 hello Blob 서비스에 등록 하거나 toouse 공유 액세스 서명을 저장소 리소스에 액세스 하기 위해 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-222">This might be necessary when you have registered a custom domain name for your storage account with hello Blob service or you want toouse a shared access signature for accessing storage resources.</span></span> <span data-ttu-id="1fbcc-223">연결 문자열에 hello 서비스 끝점을 설정 하 고 다음과 같이 toocreate 새 저장소 컨텍스트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-223">Set hello service endpoints in a connection string and use it toocreate a new storage context as shown below:</span></span>

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

<span data-ttu-id="1fbcc-224">방법에 대 한 자세한 내용은 tooconfigure 저장소 연결 문자열 참조 [연결 문자열 구성](storage-configure-connection-string.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-224">For more information on how tooconfigure a storage connection string, see [Configuring Connection Strings](storage-configure-connection-string.md).</span></span>

<span data-ttu-id="1fbcc-225">컴퓨터를 설정 하 고 학습 방법을 toomanage 구독 및 Azure PowerShell을 사용 하 여 저장소 계정 toohello 어떻게 toomanage Azure blob는 다음 섹션 toolearn 이동한 다음 blob 스냅숏을 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-225">Now that you have set up your computer and learned how toomanage subscriptions and storage accounts using Azure PowerShell, go toohello next section toolearn how toomanage Azure blobs and blob snapshots.</span></span>

### <a name="how-tooretrieve-and-regenerate-azure-storage-keys"></a><span data-ttu-id="1fbcc-226">어떻게 tooretrieve 및 재생성 Azure 저장소 키</span><span class="sxs-lookup"><span data-stu-id="1fbcc-226">How tooretrieve and regenerate Azure storage keys</span></span>
<span data-ttu-id="1fbcc-227">Azure 저장소 계정과 두 계정 키를 함께 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-227">An Azure Storage account comes with two account keys.</span></span> <span data-ttu-id="1fbcc-228">다음 cmdlet tooretrieve hello 키에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-228">You can use hello following cmdlet tooretrieve your keys.</span></span>

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

<span data-ttu-id="1fbcc-229">다음 cmdlet tooretrieve 특정 키 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-229">Use hello following cmdlet tooretrieve a specific key.</span></span> <span data-ttu-id="1fbcc-230">유효한 값은 Primary 및 Secondary입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-230">Valid values are Primary and Secondary.</span></span>  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

<span data-ttu-id="1fbcc-231">Tooregenerate 원하는 경우 키를 hello 다음 cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-231">If you would like tooregenerate your keys, use hello following cmdlet.</span></span> <span data-ttu-id="1fbcc-232">-KeyType에 대한 유효한 값은 "Primary" 및 "Secondary"입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-232">Valid values for -KeyType are "Primary" and "Secondary"</span></span>

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-toomanage-azure-blobs"></a><span data-ttu-id="1fbcc-233">어떻게 toomanage Azure blob</span><span class="sxs-lookup"><span data-stu-id="1fbcc-233">How toomanage Azure blobs</span></span>
<span data-ttu-id="1fbcc-234">Azure Blob 저장소는 많은 양의 텍스트 또는 이진 데이터를 액세스할 수 있는에서 아무 곳 이나 HTTP 또는 HTTPS를 통해 hello world에 같은 구조화 되지 않은 데이터를 저장 하기 위한 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-234">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="1fbcc-235">이 섹션에서는 hello Azure Blob 저장소 서비스 개념에 익숙하다고 이미 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-235">This section assumes that you are already familiar with hello Azure Blob Storage Service concepts.</span></span> <span data-ttu-id="1fbcc-236">자세한 내용은 [.NET을 사용하여 Blob Storage 시작](storage-dotnet-how-to-use-blobs.md) 및 [Blob Service 개념](http://msdn.microsoft.com/library/azure/dd179376.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-236">For detailed information, see [Get started with Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="how-toocreate-a-container"></a><span data-ttu-id="1fbcc-237">어떻게 toocreate 컨테이너</span><span class="sxs-lookup"><span data-stu-id="1fbcc-237">How toocreate a container</span></span>
<span data-ttu-id="1fbcc-238">Azure 저장소의 모든 Blob은 컨테이너에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-238">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="1fbcc-239">Hello New-azurestoragecontainer cmdlet을 사용 하 여 개인 컨테이너를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-239">You can create a private container using hello New-AzureStorageContainer cmdlet:</span></span>

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> <span data-ttu-id="1fbcc-240">익명 읽기 액세스의 세가지 수준은 **해제**, **Blob** 및 **컨테이너**입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-240">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="1fbcc-241">익명 tooprevent tooblobs, 집합 hello 권한 매개 변수를 너무 액세스**오프**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-241">tooprevent anonymous access tooblobs, set hello Permission parameter too**Off**.</span></span> <span data-ttu-id="1fbcc-242">기본적으로 hello 새 컨테이너는 전용 포트 이며 hello 계정 소유자만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-242">By default, hello new container is private and can be accessed only by hello account owner.</span></span> <span data-ttu-id="1fbcc-243">tooallow 익명 공용 읽기 tooblob 리소스에 액세스 하지만 toocontainer 메타 데이터 또는 toohello 목록이 아니라 hello 컨테이너의 blob, hello 권한 매개 변수를 너무 설정**Blob**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-243">tooallow anonymous public read access tooblob resources, but not toocontainer metadata or toohello list of blobs in hello container, set hello Permission parameter too**Blob**.</span></span> <span data-ttu-id="1fbcc-244">tooallow 전체 공용 읽기 액세스 tooblob 리소스, 컨테이너 메타 데이터 및 hello hello 컨테이너의 blob 목록, hello 권한 매개 변수를 너무 설정**컨테이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-244">tooallow full public read access tooblob resources, container metadata, and hello list of blobs in hello container, set hello Permission parameter too**Container**.</span></span> <span data-ttu-id="1fbcc-245">자세한 내용은 참조 [익명 읽기 권한을 toocontainers 및 blob 관리](storage-manage-access-to-resources.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-245">For more information, see [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md).</span></span>
> 
> 

### <a name="how-tooupload-a-blob-into-a-container"></a><span data-ttu-id="1fbcc-246">어떻게 tooupload blob 컨테이너에</span><span class="sxs-lookup"><span data-stu-id="1fbcc-246">How tooupload a blob into a container</span></span>
<span data-ttu-id="1fbcc-247">Azure Blob Storage는 블록 Blob 및 페이지 Blob을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-247">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="1fbcc-248">자세한 내용은 [블록 Blob,추가 Blob 및 페이지 Blob 이해](http://msdn.microsoft.com/library/azure/ee691964.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-248">For more information, see [Understanding Block Blobs, Append BLobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="1fbcc-249">tooupload blob tooa 컨테이너에서 hello를 사용할 수 있습니다 [Set-azurestorageblobcontent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-249">tooupload blobs in tooa container, you can use hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet.</span></span> <span data-ttu-id="1fbcc-250">기본적으로이 명령은 hello 로컬 파일 tooa 블록 blob을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-250">By default, this command uploads hello local files tooa block blob.</span></span> <span data-ttu-id="1fbcc-251">toospecify hello 유형 hello blob hello-BlobType 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-251">toospecify hello type for hello blob, you can use hello -BlobType parameter.</span></span>

<span data-ttu-id="1fbcc-252">hello 다음 실행 하는 예제 hello [Get-childitem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet tooget 모든 hello hello 지정 된 폴더에 파일을 다음으로 전달 toohello 다음 cmdlet hello 파이프라인 연산자를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-252">hello following example runs hello [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet tooget all hello files in hello specified folder, and then passes them toohello next cmdlet by using hello pipeline operator.</span></span> <span data-ttu-id="1fbcc-253">hello [Set-azurestorageblobcontent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet hello 로컬 파일 tooyour 컨테이너에 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-253">hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet uploads hello local files tooyour container:</span></span>

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-toodownload-blobs-from-a-container"></a><span data-ttu-id="1fbcc-254">Toodownload는 컨테이너에서 blob 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1fbcc-254">How toodownload blobs from a container</span></span>
<span data-ttu-id="1fbcc-255">다음 예제는 hello toodownload 컨테이너에서 blob 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-255">hello following example demonstrates how toodownload blobs from a container.</span></span> <span data-ttu-id="1fbcc-256">연결 tooAzure 저장소를 먼저 설정 하는 hello 예제 hello 저장소 계정 이름 및 해당 기본 액세스 키를 포함 하는 hello 저장소 계정 컨텍스트를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-256">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its primary access key.</span></span> <span data-ttu-id="1fbcc-257">그런 다음 hello 예제 hello를 사용 하 여 blob 참조를 검색 [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-257">Then, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet.</span></span> <span data-ttu-id="1fbcc-258">다음으로 hello 사용 하 여 예제 hello [Get AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) hello 로컬 대상 폴더로 cmdlet toodownload blob 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-258">Next, hello example uses hello [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet toodownload blobs into hello local destination folder.</span></span>

```powershell
#Define hello variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-toocopy-blobs-from-one-storage-container-tooanother"></a><span data-ttu-id="1fbcc-259">저장소 컨테이너 tooanother 하나에서 toocopy blob 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1fbcc-259">How toocopy blobs from one storage container tooanother</span></span>
<span data-ttu-id="1fbcc-260">저장소 계정 및 지역에 걸쳐 비동기적으로 Blob을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-260">You can copy blobs across storage accounts and regions asynchronously.</span></span> <span data-ttu-id="1fbcc-261">hello 다음 예제에서 두 개의 다른 저장소 계정에서 하나의 저장 컨테이너 tooanother toocopy blob 방법을입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-261">hello following example demonstrates how toocopy blobs from one storage container tooanother in two different storage accounts.</span></span> <span data-ttu-id="1fbcc-262">hello 예제 먼저 원본 및 대상 저장소 계정에 대 한 변수를 설정 하 고 그런 다음 각 계정에 대 한 저장소 컨텍스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-262">hello example first sets variables for source and destination storage accounts, and then creates a storage context for each account.</span></span> <span data-ttu-id="1fbcc-263">Hello 예제 hello를 사용 하 여 hello 소스 컨테이너 toohello 대상 컨테이너에서 blob를 복사 하는 다음으로, [시작 AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-263">Next, hello example copies blobs from hello source container toohello destination container using hello [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet.</span></span> <span data-ttu-id="1fbcc-264">hello 예제 hello 원본 및 대상 저장소 계정 및 컨테이너 이미 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-264">hello example assumes that hello source and destination storage accounts and containers already exist.</span></span>

```powershell
#Define hello source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define hello destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference tooblobs in hello source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container tooanother.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

<span data-ttu-id="1fbcc-265">이 예제에서는 비동기 복사본을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-265">Note that this example performs an asynchronous copy.</span></span> <span data-ttu-id="1fbcc-266">Hello를 실행 하 여 각 복사본의 hello 상태를 모니터링할 수 있습니다 [Get AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-266">You can monitor hello status of each copy by running hello [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.</span></span>

### <a name="how-toocopy-blobs-from-a-secondary-location"></a><span data-ttu-id="1fbcc-267">보조 위치에서 toocopy blob 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1fbcc-267">How toocopy blobs from a secondary location</span></span>
<span data-ttu-id="1fbcc-268">Hello RA GRS를 활성화 계정의 보조 위치에서 blob을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-268">You can copy blobs from hello secondary location of a RA-GRS-enabled account.</span></span>

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-toodelete-a-blob"></a><span data-ttu-id="1fbcc-269">어떻게 toodelete blob</span><span class="sxs-lookup"><span data-stu-id="1fbcc-269">How toodelete a blob</span></span>
<span data-ttu-id="1fbcc-270">toodelete blob 가져오려면 먼저 blob 참조를에 hello 제거 AzureStorageBlob cmdlet을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-270">toodelete a blob, first get a blob reference and then call hello Remove-AzureStorageBlob cmdlet on it.</span></span> <span data-ttu-id="1fbcc-271">다음 예에서는 hello 특정된 컨테이너의 모든 hello blob을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-271">hello following example deletes all hello blobs in a given container.</span></span> <span data-ttu-id="1fbcc-272">hello 예에서는 먼저 저장소 계정에 대 한 변수를 설정 하 고 저장소 컨텍스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-272">hello example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="1fbcc-273">Hello 예제 hello를 사용 하 여 blob 참조를 검색 하는 다음으로, [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet을 실행 하는 hello [제거 AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet tooremove blob에서 Azure 저장소의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-273">Next, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet tooremove blobs from a container in Azure storage.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooall hello blobs in hello container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-toomanage-azure-blob-snapshots"></a><span data-ttu-id="1fbcc-274">Toomanage Azure blob 스냅숏을 방법</span><span class="sxs-lookup"><span data-stu-id="1fbcc-274">How toomanage Azure blob snapshots</span></span>
<span data-ttu-id="1fbcc-275">Azure를 사용하면 Blob의 스냅숏을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-275">Azure lets you create a snapshot of a blob.</span></span> <span data-ttu-id="1fbcc-276">스냅숏은 특정 시점에 생성된 Blob의 읽기 전용 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-276">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="1fbcc-277">스냅숏이 생성된 후에는 읽거나 복사하거나 삭제할 수 있지만 수정할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-277">Once a snapshot has been created, it can be read, copied, or deleted, but not modified.</span></span> <span data-ttu-id="1fbcc-278">스냅숏은 시점에 표시 된 대로 blob 방법을 tooback를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-278">Snapshots provide a way tooback up a blob as it appears at a moment in time.</span></span> <span data-ttu-id="1fbcc-279">자세한 내용은 [Blob의 스냅숏 만들기](http://msdn.microsoft.com/library/azure/hh488361.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-279">For more information, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span>

### <a name="how-toocreate-a-blob-snapshot"></a><span data-ttu-id="1fbcc-280">어떻게 toocreate blob 스냅숏</span><span class="sxs-lookup"><span data-stu-id="1fbcc-280">How toocreate a blob snapshot</span></span>
<span data-ttu-id="1fbcc-281">toocreate는 blob의 스냅숏은 blob 참조를 먼저 가져온 고 hello 호출 `ICloudBlob.CreateSnapshot` 메서드를 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-281">toocreate a snaphot of a blob, first get a blob reference and then call hello `ICloudBlob.CreateSnapshot` method on it.</span></span> <span data-ttu-id="1fbcc-282">hello 다음 예제에서는 먼저 저장소 계정에 대 한 변수를 설정 하 고 저장소 컨텍스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-282">hello following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="1fbcc-283">Hello 예제 hello를 사용 하 여 blob 참조를 검색 하는 다음으로, [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet을 실행 하는 hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) 메서드 toocreate 스냅숏으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-283">Next, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method toocreate a snapshot.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of hello blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-toolist-a-blobs-snapshots"></a><span data-ttu-id="1fbcc-284">어떻게 toolist blob의 스냅숏</span><span class="sxs-lookup"><span data-stu-id="1fbcc-284">How toolist a blob's snapshots</span></span>
<span data-ttu-id="1fbcc-285">Blob에 대해 원하는 수 만큼 많은 스냅샷을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-285">You can create as many snapshots as you want for a blob.</span></span> <span data-ttu-id="1fbcc-286">Blob tootrack와 연결 된 hello 스냅숏을 표시 하 여 최신 스냅숏을 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-286">You can list hello snapshots associated with your blob tootrack your current snapshots.</span></span> <span data-ttu-id="1fbcc-287">hello 다음 예제에서는 미리 정의 된 blob 및 호출 hello [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) 해당 blob의 toolist hello 스냅숏을 cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-287">hello following example uses a predefined blob and calls hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet toolist hello snapshots of that blob.</span></span>  

```powershell
#Define hello blob name.
$BlobName = "yourblobname"

#List hello snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-toocopy-a-snapshot-of-a-blob"></a><span data-ttu-id="1fbcc-288">어떻게 toocopy blob의 스냅숏</span><span class="sxs-lookup"><span data-stu-id="1fbcc-288">How toocopy a snapshot of a blob</span></span>
<span data-ttu-id="1fbcc-289">Blob toorestore hello 스냅숏에 대 한 스냅숏을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-289">You can copy a snapshot of a blob toorestore hello snapshot.</span></span> <span data-ttu-id="1fbcc-290">자세한 내용 및 제한 사항에 대해서는 [Blob의 스냅숏 만들기](http://msdn.microsoft.com/library/azure/hh488361.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-290">For detailed information and restrictions, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span> <span data-ttu-id="1fbcc-291">hello 다음 예제에서는 먼저 저장소 계정에 대 한 변수를 설정 하 고 저장소 컨텍스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-291">hello following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="1fbcc-292">다음으로 hello 예제는 hello 컨테이너 및 blob 이름 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-292">Next, hello example defines hello container and blob name variables.</span></span> <span data-ttu-id="1fbcc-293">hello를 사용 하 여 blob 참조를 검색 하는 hello 예제 [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet을 실행 하는 hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) 메서드 toocreate 스냅숏으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-293">hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method toocreate a snapshot.</span></span> <span data-ttu-id="1fbcc-294">그런 다음 hello 실행 하는 예제 hello [시작 AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) hello ICloudBlob 개체를 사용 하 여 hello 원본 blob에 대 한 blob의 cmdlet toocopy hello 스냅숏을 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-294">Then, hello example runs hello [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet toocopy hello snapshot of a blob using hello ICloudBlob object for hello source blob.</span></span> <span data-ttu-id="1fbcc-295">있는지 tooupdate hello 변수 기반 hello 예제를 실행 하기 전에 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-295">Be sure tooupdate hello variables based on your configuration before running hello example.</span></span> <span data-ttu-id="1fbcc-296">다음 예에서는 해당 hello에서는 원본 및 대상 컨테이너는 hello 가정 하 고 hello 원본 blob가 이미 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-296">Note that hello following example assumes that hello source and destination containers, and hello source blob already exist.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define hello variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy hello snapshot tooanother container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

<span data-ttu-id="1fbcc-297">Toomanage Azure blob 하는 방법을 배웠습니다 하 고 Azure PowerShell을 사용 하 여 스냅숏을 blob toohello 다음 섹션 toolearn 방법 toomanage 테이블, 큐 및 파일을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-297">Now that you have learned how toomanage Azure blobs and blob snapshots with Azure PowerShell, go toohello next section toolearn how toomanage tables, queues, and files.</span></span>

## <a name="how-toomanage-azure-tables-and-table-entities"></a><span data-ttu-id="1fbcc-298">Azure toomanage 테이블과 테이블 엔터티</span><span class="sxs-lookup"><span data-stu-id="1fbcc-298">How toomanage Azure tables and table entities</span></span>
<span data-ttu-id="1fbcc-299">Azure 테이블 저장소 서비스에 사용할 수 있는 NoSQL 데이터 저장소는 비관계형 구조적된 데이터의 거 대 한 집합 toostore 및 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-299">Azure Table storage service is a NoSQL datastore, which you can use toostore and query huge sets of structured, non-relational data.</span></span> <span data-ttu-id="1fbcc-300">hello hello 서비스의 주요 구성 요소는 테이블, 엔터티 및 속성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-300">hello main components of hello service are tables, entities, and properties.</span></span> <span data-ttu-id="1fbcc-301">테이블은 엔터티 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-301">A table is a collection of entities.</span></span> <span data-ttu-id="1fbcc-302">엔터티는 속성의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-302">An entity is a set of properties.</span></span> <span data-ttu-id="1fbcc-303">각 엔터티는 모든 이름-값 쌍으로 된 too252 속성을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-303">Each entity can have up too252 properties, which are all name-value pairs.</span></span> <span data-ttu-id="1fbcc-304">이 섹션에서는 hello Azure 테이블 저장소 서비스 개념에 익숙하다고 이미 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-304">This section assumes that you are already familiar with hello Azure Table Storage Service concepts.</span></span> <span data-ttu-id="1fbcc-305">자세한 내용은 참조 [테이블 서비스 데이터 모델 이해 hello](http://msdn.microsoft.com/library/azure/dd179338.aspx) 및 [.NET을 사용 하 여 Azure 테이블 저장소 시작](storage-dotnet-how-to-use-tables.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-305">For detailed information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) and [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="1fbcc-306">다음 하위 섹션으로 구성 하는 hello, Azure PowerShell을 사용 하 여 Azure 테이블 저장소 toomanage을 서비스 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-306">In hello following subsections, you'll learn how toomanage Azure Table storage service using Azure PowerShell.</span></span> <span data-ttu-id="1fbcc-307">hello 가이드에서 다루는 시나리오 포함 **만드는**, **삭제**, 및 **검색** **테이블**,으로 **추가**, **쿼리**, 및 **테이블 엔터티 삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-307">hello scenarios covered include **creating**, **deleting**, and **retrieving** **tables**, as well as **adding**, **querying**, and **deleting table entities**.</span></span>

### <a name="how-toocreate-a-table"></a><span data-ttu-id="1fbcc-308">어떻게 toocreate 테이블</span><span class="sxs-lookup"><span data-stu-id="1fbcc-308">How toocreate a table</span></span>
<span data-ttu-id="1fbcc-309">모든 테이블은 Azure 저장소 계정에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-309">Every table must reside in an Azure storage account.</span></span> <span data-ttu-id="1fbcc-310">hello 다음 예제에서는 어떻게 toocreate Azure 저장소의 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-310">hello following example demonstrates how toocreate a table in Azure Storage.</span></span> <span data-ttu-id="1fbcc-311">연결 tooAzure 저장소를 먼저 설정 하는 hello 예제 hello 저장소 계정 이름과 액세스 키를 포함 하는 hello 저장소 계정 컨텍스트를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-311">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="1fbcc-312">Hello 사용 하 여 다음으로, [새로 AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet toocreate Azure 저장소의 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-312">Next, it uses hello [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet toocreate a table in Azure Storage.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-tooretrieve-a-table"></a><span data-ttu-id="1fbcc-313">어떻게 tooretrieve 테이블</span><span class="sxs-lookup"><span data-stu-id="1fbcc-313">How tooretrieve a table</span></span>
<span data-ttu-id="1fbcc-314">저장소 계정에서 한 테이블 또는 모든 테이블을 쿼리하고 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-314">You can query and retrieve one or all tables in a Storage account.</span></span> <span data-ttu-id="1fbcc-315">hello 다음 예제에서는 방법을 사용 하 여 지정 된 테이블 tooretrieve hello [Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-315">hello following example demonstrates how tooretrieve a given table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span>

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

<span data-ttu-id="1fbcc-316">매개 변수 없이 hello AzureStorageTable Get cmdlet을 호출 하는 경우 저장소 계정에 대 한 저장소 테이블을 모두 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-316">If you call hello Get-AzureStorageTable cmdlet without any parameters, it gets all storage tables for a Storage account.</span></span>

### <a name="how-toodelete-a-table"></a><span data-ttu-id="1fbcc-317">어떻게 toodelete 테이블</span><span class="sxs-lookup"><span data-stu-id="1fbcc-317">How toodelete a table</span></span>
<span data-ttu-id="1fbcc-318">Hello를 사용 하 여 저장소 계정에서 테이블을 삭제할 수 [제거 AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-318">You can delete a table from a storage account by using hello [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.</span></span>  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-toomanage-table-entities"></a><span data-ttu-id="1fbcc-319">어떻게 toomanage 테이블 엔터티</span><span class="sxs-lookup"><span data-stu-id="1fbcc-319">How toomanage table entities</span></span>
<span data-ttu-id="1fbcc-320">현재, Azure PowerShell는 toomanage 테이블 엔터티 cmdlet을 직접 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-320">Currently, Azure PowerShell does not provide cmdlets toomanage table entities directly.</span></span> <span data-ttu-id="1fbcc-321">tooperform 테이블 엔터티에 대 한 작업을 hello에 지정 된 hello 클래스를 사용할 수 있습니다 [.NET 용 Azure 저장소 클라이언트 라이브러리](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-321">tooperform operations on table entities, you can use hello classes given in hello [Azure Storage Client Library for .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span></span>

#### <a name="how-tooadd-table-entities"></a><span data-ttu-id="1fbcc-322">어떻게 tooadd 테이블 엔터티</span><span class="sxs-lookup"><span data-stu-id="1fbcc-322">How tooadd table entities</span></span>
<span data-ttu-id="1fbcc-323">먼저 tooadd은 엔터티 tooa 테이블 엔터티 속성을 정의 하는 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-323">tooadd an entity tooa table, first create an object that defines your entity properties.</span></span> <span data-ttu-id="1fbcc-324">Too255 속성을 3 개의 시스템 속성을 포함 하 여 있을 수 있는 엔터티: **PartitionKey**, **RowKey**, 및 **타임 스탬프**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-324">An entity can have up too255 properties, including 3 system properties: **PartitionKey**, **RowKey**, and **Timestamp**.</span></span> <span data-ttu-id="1fbcc-325">삽입 하 고 hello 값을 업데이트 하는 일을 담당 **PartitionKey** 및 **RowKey**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-325">You are responsible for inserting and updating hello values of **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="1fbcc-326">hello 서버 관리의 hello 값 **타임 스탬프**를 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-326">hello server manages hello value of **Timestamp**, which cannot be modified.</span></span> <span data-ttu-id="1fbcc-327">함께 hello **PartitionKey** 및 **RowKey** 테이블 내의 모든 엔터티를 고유 하 게 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-327">Together hello **PartitionKey** and **RowKey** uniquely identify every entity within a table.</span></span>

* <span data-ttu-id="1fbcc-328">**PartitionKey**: hello 엔터티에 저장 되어 있는 hello 파티션을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-328">**PartitionKey**: Determines hello partition that hello entity is stored in.</span></span>
* <span data-ttu-id="1fbcc-329">**RowKey**: hello 파티션 내의 hello 엔터티를 고유 하 게 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-329">**RowKey**: Uniquely identifies hello entity within hello partition.</span></span>

<span data-ttu-id="1fbcc-330">Too252 엔터티에 대 한 사용자 지정 속성을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-330">You may define up too252 custom properties for an entity.</span></span> <span data-ttu-id="1fbcc-331">자세한 내용은 참조 [테이블 서비스 데이터 모델 이해 hello](http://msdn.microsoft.com/library/azure/dd179338.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-331">For more information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="1fbcc-332">hello 다음 예제에서는 어떻게 tooadd 엔터티 tooa 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-332">hello following example demonstrates how tooadd entities tooa table.</span></span> <span data-ttu-id="1fbcc-333">hello 예제에는 tooretrieve employee 테이블 hello 하 한에 몇 개의 엔터티를 추가 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-333">hello example shows how tooretrieve hello employee table and add several entities into it.</span></span> <span data-ttu-id="1fbcc-334">먼저, 연결 tooAzure 저장소를 설정 hello 저장소 계정 이름과 액세스 키를 포함 하는 hello 저장소 계정 컨텍스트를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-334">First, it establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="1fbcc-335">다음으로 hello를 사용 하 여 테이블을 지정 하는 hello 검색 [Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-335">Next, it retrieves hello given table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="1fbcc-336">Hello 테이블이 존재 하지 않는 경우 hello [새로 AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet은 사용 되는 toocreate Azure 저장소의 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-336">If hello table does not exist, hello [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet is used toocreate a table in Azure Storage.</span></span> <span data-ttu-id="1fbcc-337">다음으로 hello 예제 각 엔터티의 파티션과 행 키는 지정 하 여 tooadd 엔터티 toohello 테이블 엔터티 추가 사용자 지정 함수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-337">Next, hello example defines a custom function Add-Entity tooadd entities toohello table by specifying each entity's partition and row key.</span></span> <span data-ttu-id="1fbcc-338">엔터티 추가 hello 함수 호출 hello [New-object](http://technet.microsoft.com/library/hh849885.aspx) hello cmdlet [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) 클래스 toocreate 엔터티 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-338">hello Add-Entity function calls hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on hello [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) class toocreate an entity object.</span></span> <span data-ttu-id="1fbcc-339">Hello 예제 hello를 호출 하는 나중 [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) 이 엔터티 개체 tooadd 메서드 것 tooa 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-339">Later, hello example calls hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) method on this entity object tooadd it tooa table.</span></span>

```powershell
#Function Add-Entity: Adds an employee entity tooa table.
function Add-Entity() {
    [CmdletBinding()]
    param(
       $table,
       [String]$partitionKey,
       [String]$rowKey,
       [String]$name,
       [Int]$id
    )

  $entity = New-Object -TypeName Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity -ArgumentList $partitionKey, $rowKey
  $entity.Properties.Add("Name", $name)
  $entity.Properties.Add("ID", $id)

  $result = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Insert($entity))
}

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve hello table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities tooa table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-tooquery-table-entities"></a><span data-ttu-id="1fbcc-340">어떻게 tooquery 테이블 엔터티</span><span class="sxs-lookup"><span data-stu-id="1fbcc-340">How tooquery table entities</span></span>
<span data-ttu-id="1fbcc-341">tooquery 테이블을 사용 하 여 hello [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-341">tooquery a table, use hello [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) class.</span></span> <span data-ttu-id="1fbcc-342">hello 다음 예에서는 가정 어떻게 hello에 지정 된 hello 스크립트 이미 실행 한이 가이드의 tooadd 엔터티 섹션.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-342">hello following example assumes that you've already run hello script given in hello How tooadd entities section of this guide.</span></span> <span data-ttu-id="1fbcc-343">연결 tooAzure 저장소를 먼저 설정 하는 hello 예제 hello 저장소 계정 이름과 액세스 키를 포함 하는 hello 저장소 컨텍스트를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-343">hello example first establishes a connection tooAzure Storage using hello storage context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="1fbcc-344">다음으로 hello를 사용 하 여 tooretrieve hello 이전에 만든 "직원" 테이블 시도 [Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-344">Next, it tries tooretrieve hello previously created "Employees" table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="1fbcc-345">호출 hello [New-object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet hello Microsoft.WindowsAzure.Storage.Table.TableQuery 클래스에 새 쿼리 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-345">Calling hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on hello Microsoft.WindowsAzure.Storage.Table.TableQuery class creates a new query object.</span></span> <span data-ttu-id="1fbcc-346">hello 예제 값이 문자열 필터에 지정 된 대로 1 인에 'ID' 열이 있어야 하는 hello 엔터티를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-346">hello example looks for hello entities that have an 'ID' column whose value is 1 as specified in a string filter.</span></span> <span data-ttu-id="1fbcc-347">자세한 내용은 [테이블 및 엔터티 쿼리](http://msdn.microsoft.com/library/azure/dd894031.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-347">For detailed information, see [Querying Tables and Entities](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span></span> <span data-ttu-id="1fbcc-348">이 쿼리를 실행 하면 hello 필터 조건과 일치 하는 모든 엔터티를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-348">When you run this query, it returns all entities that match hello filter criteria.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference tooa table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns tooselect.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute hello query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with hello table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-toodelete-table-entities"></a><span data-ttu-id="1fbcc-349">어떻게 toodelete 테이블 엔터티</span><span class="sxs-lookup"><span data-stu-id="1fbcc-349">How toodelete table entities</span></span>
<span data-ttu-id="1fbcc-350">파티션 및 행 키를 사용하여 엔터티를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-350">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="1fbcc-351">hello 다음 예에서는 가정 어떻게 hello에 지정 된 hello 스크립트 이미 실행 한이 가이드의 tooadd 엔터티 섹션.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-351">hello following example assumes that you've already run hello script given in hello How tooadd entities section of this guide.</span></span> <span data-ttu-id="1fbcc-352">연결 tooAzure 저장소를 먼저 설정 하는 hello 예제 hello 저장소 계정 이름과 액세스 키를 포함 하는 hello 저장소 컨텍스트를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-352">hello example first establishes a connection tooAzure Storage using hello storage context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="1fbcc-353">다음으로 hello를 사용 하 여 tooretrieve hello 이전에 만든 "직원" 테이블 시도 [Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-353">Next, it tries tooretrieve hello previously created "Employees" table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="1fbcc-354">Hello 테이블이 있을 경우 hello 호출 하 여 hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) 메서드 tooretrieve 엔터티는 파티션 및 행 키 값에 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-354">If hello table exists, hello example calls hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) method tooretrieve an entity based on its partition and row key values.</span></span> <span data-ttu-id="1fbcc-355">그런 다음 hello 엔터티 toohello 전달 [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) 메서드 toodelete 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-355">Then, pass hello entity toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) method toodelete.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If hello table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together hello PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete hello entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-toomanage-azure-queues-and-queue-messages"></a><span data-ttu-id="1fbcc-356">방법 toomanage Azure 큐 및 메시지 큐</span><span class="sxs-lookup"><span data-stu-id="1fbcc-356">How toomanage Azure queues and queue messages</span></span>
<span data-ttu-id="1fbcc-357">Azure 큐 저장소는 많은 수의 액세스할 수 있는에서 아무 곳 이나 HTTP 또는 HTTPS를 사용 하 여 인증 된 호출을 통해 hello world에 메시지를 저장 하기 위한 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-357">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="1fbcc-358">이 섹션에서는 hello Azure 큐 저장소 서비스 개념에 익숙하다고 이미 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-358">This section assumes that you are already familiar with hello Azure Queue Storage Service concepts.</span></span> <span data-ttu-id="1fbcc-359">자세한 내용은 [.NET을 사용하여 Azure 큐 저장소 시작](storage-dotnet-how-to-use-queues.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-359">For detailed information, see [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md).</span></span>

<span data-ttu-id="1fbcc-360">이 섹션 안내해 toomanage Azure 큐 저장소 서비스 Azure PowerShell을 사용 하 여 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-360">This section will show you how toomanage Azure Queue storage service using Azure PowerShell.</span></span> <span data-ttu-id="1fbcc-361">hello 가이드에서 다루는 시나리오 포함 **삽입** 및 **삭제** 메시지를 큐와 **만드는**, **삭제**, 및 **대기열 검색**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-361">hello scenarios covered include **inserting** and **deleting** queue messages, as well as **creating**, **deleting**, and **retrieving queues**.</span></span>

### <a name="how-toocreate-a-queue"></a><span data-ttu-id="1fbcc-362">어떻게 toocreate 큐</span><span class="sxs-lookup"><span data-stu-id="1fbcc-362">How toocreate a queue</span></span>
<span data-ttu-id="1fbcc-363">hello 다음 예에서는 먼저 설정 연결 tooAzure 저장소 hello 저장소 계정 이름과 액세스 키를 포함 하는 hello 저장소 계정 컨텍스트를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-363">hello following example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="1fbcc-364">다음으로 호출 [새로 AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet toocreate 'queuename' 라는 큐.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-364">Next, it calls [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet toocreate a queue named 'queuename'.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

<span data-ttu-id="1fbcc-365">Azure 큐 서비스에 대한 명명 규칙에 대해서는 [큐 및 메타데이터 이름 지정](http://msdn.microsoft.com/library/azure/dd179349.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-365">For information on naming conventions for Azure Queue Service, see [Naming Queues and Metadata](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

### <a name="how-tooretrieve-a-queue"></a><span data-ttu-id="1fbcc-366">어떻게 tooretrieve 큐</span><span class="sxs-lookup"><span data-stu-id="1fbcc-366">How tooretrieve a queue</span></span>
<span data-ttu-id="1fbcc-367">쿼리할 수 있으며 특정 큐 또는 저장소 계정에 모든 hello 큐 목록을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-367">You can query and retrieve a specific queue or a list of all hello queues in a Storage account.</span></span> <span data-ttu-id="1fbcc-368">hello 다음 예제에서는 방법을 사용 하 여 지정 된 큐 tooretrieve hello [Get AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-368">hello following example demonstrates how tooretrieve a specified queue using hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.</span></span>

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

<span data-ttu-id="1fbcc-369">Hello를 호출 하는 경우 [Get AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) 매개 변수 없이 cmdlet을 모든 hello 큐 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-369">If you call hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet without any parameters, it gets a list of all hello queues.</span></span>

### <a name="how-toodelete-a-queue"></a><span data-ttu-id="1fbcc-370">어떻게 toodelete 큐</span><span class="sxs-lookup"><span data-stu-id="1fbcc-370">How toodelete a queue</span></span>
<span data-ttu-id="1fbcc-371">toodelete는 큐와 모든 hello 메시지에 포함 된, hello 제거 AzureStorageQueue cmdlet을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-371">toodelete a queue and all hello messages contained in it, call hello Remove-AzureStorageQueue cmdlet.</span></span> <span data-ttu-id="1fbcc-372">다음 예제는 hello 사용 하 여 지정 된 큐 toodelete 제거 AzureStorageQueue cmdlet hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-372">hello following example shows how toodelete a specified queue using hello Remove-AzureStorageQueue cmdlet.</span></span>

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-tooinsert-a-message-into-a-queue"></a><span data-ttu-id="1fbcc-373">어떻게 tooinsert 큐에 메시지</span><span class="sxs-lookup"><span data-stu-id="1fbcc-373">How tooinsert a message into a queue</span></span>
<span data-ttu-id="1fbcc-374">기존 큐에 메시지 tooinsert hello의 새 인스턴스를 먼저 만든 [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-374">tooinsert a message into an existing queue, first create a new instance of hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="1fbcc-375">그런 다음 호출 하는 hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) 메서드.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-375">Next, call hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method.</span></span> <span data-ttu-id="1fbcc-376">문자열(UTF-8 형식) 또는 바이트 배열에서 CloudQueueMessage를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-376">A CloudQueueMessage can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="1fbcc-377">다음 예제는 hello tooadd tooa 큐 메시지 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-377">hello following example demonstrates how tooadd message tooa queue.</span></span> <span data-ttu-id="1fbcc-378">연결 tooAzure 저장소를 먼저 설정 하는 hello 예제 hello 저장소 계정 이름과 액세스 키를 포함 하는 hello 저장소 계정 컨텍스트를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-378">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="1fbcc-379">다음으로 hello를 사용 하 여 hello 지정 된 큐를 검색 [Get AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-379">Next, it retrieves hello specified queue using hello [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span></span> <span data-ttu-id="1fbcc-380">Hello 큐가 있는 hello 경우 [New-object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet은 사용 되는 toocreate hello 인스턴스의 [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-380">If hello queue exists, hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet is used toocreate an instance of hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="1fbcc-381">Hello 예제 hello를 호출 하는 나중 [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) 이 메시지 개체 tooadd 메서드 것 tooa 큐입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-381">Later, hello example calls hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method on this message object tooadd it tooa queue.</span></span> <span data-ttu-id="1fbcc-382">큐를 검색 하 고 'MessageInfo' hello 메시지를 삽입 하는 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-382">Here is code which retrieves a queue and inserts hello message 'MessageInfo':</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If hello queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of hello CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message toohello queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-toode-queue-at-hello-next-message"></a><span data-ttu-id="1fbcc-383">Hello에서 toode queue 다음 어떻게 메시지</span><span class="sxs-lookup"><span data-stu-id="1fbcc-383">How toode-queue at hello next message</span></span>
<span data-ttu-id="1fbcc-384">다음 코드는 2단계를 거쳐 큐에서 메시지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-384">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="1fbcc-385">Hello를 호출 하는 경우 [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) 메서드를 hello 다음에 메시지가 큐입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-385">When you call hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) method, you get hello next message in a queue.</span></span> <span data-ttu-id="1fbcc-386">반환 된 메시지 **GetMessage** 보이지 않는 tooany이이 큐에서 메시지를 읽을 다른 코드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-386">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="1fbcc-387">toofinish 제거 hello 큐에서에서 메시지를 hello 호출 해야 hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) 메서드.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-387">toofinish removing hello message from hello queue, you must also call hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) method.</span></span> <span data-ttu-id="1fbcc-388">이 2 단계 프로세스의 메시지를 제거 하는 코드 tooprocess toohardware 또는 소프트웨어 오류가, 코드의 다른 인스턴스는 메시지를 가져올 수 없으면 동일한 메시지 hello 고 다시 시도 하십시오 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-388">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="1fbcc-389">코드 호출 **DeleteMessage** 직후 hello 메시지를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-389">Your code calls **DeleteMessage** right after hello message has been processed.</span></span>

```powershell
# Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get hello message object from hello queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete hello message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-toomanage-azure-file-shares-and-files"></a><span data-ttu-id="1fbcc-390">방법 toomanage Azure 파일 공유 및 파일</span><span class="sxs-lookup"><span data-stu-id="1fbcc-390">How toomanage Azure file shares and files</span></span>
<span data-ttu-id="1fbcc-391">Azure 파일 저장소 hello 표준 SMB 프로토콜을 사용 하 여 응용 프로그램에 대 한 공유 저장소를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-391">Azure File storage offers shared storage for applications using hello standard SMB protocol.</span></span> <span data-ttu-id="1fbcc-392">Microsoft Azure 가상 컴퓨터 및 클라우드 서비스를 통해 탑재 된 공유 응용 프로그램 구성 요소에서 파일 데이터를 공유할 수 및 온-프레미스 응용 프로그램 hello 파일 저장소 API 또는 Azure PowerShell을 통해 공유에 파일 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-392">Microsoft Azure virtual machines and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share via hello File storage API or Azure PowerShell.</span></span>

<span data-ttu-id="1fbcc-393">Azure File Storage에 대한 자세한 내용은 [Windows에서 Azure File Storage 시작](storage-dotnet-how-to-use-files.md) 및 [파일 서비스 REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-393">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) and [File Service REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span></span>

## <a name="how-tooset-and-query-storage-analytics"></a><span data-ttu-id="1fbcc-394">어떻게 tooset 및 쿼리 저장소 분석</span><span class="sxs-lookup"><span data-stu-id="1fbcc-394">How tooset and query storage analytics</span></span>
<span data-ttu-id="1fbcc-395">사용할 수 있습니다 [Azure Storage Analytics](storage-analytics.md) Azure 저장소 계정 및 요청에 대 한 로그 데이터에 대 한 toocollect 메트릭을 전송 tooyour 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-395">You can use [Azure Storage Analytics](storage-analytics.md) toocollect metrics for your Azure storage accounts and log data about requests sent tooyour storage account.</span></span> <span data-ttu-id="1fbcc-396">저장소 계정 및 저장소 로깅 toodiagnose 저장소 메트릭을 toomonitor hello 상태를 사용 하 여 수 있으며 저장소 계정을 사용 하 여 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-396">You can use storage metrics toomonitor hello health of a storage account, and storage logging toodiagnose and troubleshoot issues with your storage account.</span></span> <span data-ttu-id="1fbcc-397">사용 하 여 모니터링을 구성할 수 있습니다 hello Azure 포털 또는 Windows PowerShell 또는 프로그래밍 방식으로 hello 저장소 클라이언트 라이브러리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-397">You can configure monitoring using hello Azure portal or Windows PowerShell, or programmatically using hello storage client library.</span></span> <span data-ttu-id="1fbcc-398">저장소 로깅에는 저장소 계정에 성공 및 실패 한 요청에 대 한 toorecord 세부 정보를 사용 하면를 서버 쪽을 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-398">Storage logging happens server-side and enables you toorecord details for both successful and failed requests in your storage account.</span></span> <span data-ttu-id="1fbcc-399">이러한 로그 읽기, 쓰기 및 삭제 작업에 대해 사용자 테이블, 큐 및 blob으로 실패 한 요청에 대 한 hello 이유의 toosee 세부 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-399">These logs enable you toosee details of read, write, and delete operations against your tables, queues, and blobs as well as hello reasons for failed requests.</span></span>

<span data-ttu-id="1fbcc-400">tooenable 보기 저장소 메트릭 데이터 PowerShell을 사용 하 여 확인 하려면 어떻게 해야 toolearn [어떻게 tooenable 저장소 메트릭을 PowerShell을 사용 하 여](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell)합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-400">toolearn how tooenable and view Storage Metrics data using PowerShell, see [How tooenable Storage Metrics using PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span></span>

<span data-ttu-id="1fbcc-401">tooenable 및 검색 하 고 저장소 로깅을 사용 하 여 데이터 PowerShell을 확인 하려면 어떻게 해야 toolearn [어떻게 tooenable 저장소 PowerShell을 사용 하 여 로깅을](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) 및 [저장소 로깅 로그 데이터 찾기](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata)합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-401">toolearn how tooenable and retrieve Storage Logging data using PowerShell, see [How tooenable Storage Logging using PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) and [Finding your Storage Logging log data](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span></span>
<span data-ttu-id="1fbcc-402">저장소 메트릭 및 저장소 tootroubleshoot 저장소 문제를 기록 사용에 대 한 자세한 내용은 참조 하십시오. [모니터링, 진단 및 문제 해결 Microsoft Azure 저장소](storage-monitoring-diagnosing-troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-402">For detailed information on using Storage Metrics and Storage Logging tootroubleshoot storage issues, see [Monitoring, Diagnosing, and Troubleshooting Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).</span></span>

## <a name="how-toomanage-shared-access-signature-sas-and-stored-access-policy"></a><span data-ttu-id="1fbcc-403">어떻게 toomanage 공유 액세스 서명 (SAS) 및 저장 된 액세스 정책</span><span class="sxs-lookup"><span data-stu-id="1fbcc-403">How toomanage Shared Access Signature (SAS) and Stored Access Policy</span></span>
<span data-ttu-id="1fbcc-404">공유 액세스 서명이 Azure 저장소를 사용 하 여 모든 응용 프로그램에 대 한 hello 보안 모델의 중요 한 부분이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-404">Shared access signatures are an important part of hello security model for any application using Azure Storage.</span></span> <span data-ttu-id="1fbcc-405">제한 된 권한 tooyour 저장소 계정 tooclients hello 계정 키 없는 제공 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-405">They are useful for providing limited permissions tooyour storage account tooclients that should not have hello account key.</span></span> <span data-ttu-id="1fbcc-406">기본적으로 hello 소유자만 hello 저장소 계정의 blob, 테이블 및 해당 계정 내에서 큐를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-406">By default, only hello owner of hello storage account may access blobs, tables, and queues within that account.</span></span> <span data-ttu-id="1fbcc-407">서비스 또는 응용 프로그램을 필요한 경우 toomake 이러한 리소스 사용 가능한 tooother 클라이언트 액세스 키를 공유 하지 않고 세 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-407">If your service or application needs toomake these resources available tooother clients without sharing your access key, you have three options:</span></span>

* <span data-ttu-id="1fbcc-408">컨테이너의 사용 권한 toopermit 익명 읽기 권한을 toohello 컨테이너와 그 blob를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-408">Set a container's permissions toopermit anonymous read access toohello container and its blobs.</span></span> <span data-ttu-id="1fbcc-409">테이블 또는 큐에 대해서는 이렇게 할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-409">This is not allowed for tables or queues.</span></span>
* <span data-ttu-id="1fbcc-410">특정 시간 간격에 대 한 제한 된 액세스 권한 toocontainers, blob, 큐 및 테이블을 부여 하는 공유 액세스 서명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-410">Use a shared access signature that grants restricted access rights toocontainers, blobs, queues, and tables for a specific time interval.</span></span>
* <span data-ttu-id="1fbcc-411">컨테이너 또는 해당 blob에 대 한, 큐 또는 테이블에 대 한 저장 된 액세스 정책 tooobtain 추가 수준을 공유 액세스 서명에 대 한 제어를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-411">Use a stored access policy tooobtain an additional level of control over shared access signatures for a container or its blobs, for a queue, or for a table.</span></span> <span data-ttu-id="1fbcc-412">hello 저장 된 액세스 정책을 사용 하면 toochange hello 시작 시간, 만료 시간 또는 서명에 대 한 사용 권한 또는 toorevoke 뒤 발행 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-412">hello stored access policy allows you toochange hello start time, expiry time, or permissions for a signature, or toorevoke it after it has been issued.</span></span>

<span data-ttu-id="1fbcc-413">공유 액세스 서명은 다음 두 가지 형식 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-413">A shared access signature can be in one of two forms:</span></span>

* <span data-ttu-id="1fbcc-414">**임시 SAS**:는 임시 SAS, hello 시작 시간, 만료 시간을 만들고 SAS hello에 대 한 권한을 모두 hello SAS URI에 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-414">**Ad hoc SAS**: When you create an ad hoc SAS, hello start time, expiry time, and permissions for hello SAS are all specified on hello SAS URI.</span></span> <span data-ttu-id="1fbcc-415">이 유형의 SAS는 컨테이너, Blob, 테이블 또는 큐에서 만들 수 있으며, 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-415">This type of SAS may be created on a container, blob, table, or queue and it is non-revocable.</span></span>
* <span data-ttu-id="1fbcc-416">**저장 된 액세스 정책 사용 하 여 SAS**: 저장 된 액세스 정책은 리소스 컨테이너는 blob 컨테이너, 테이블 또는 큐-에서 정의 되 고 하나 이상의 공유 액세스 서명에 대 한 toomanage 제약 조건을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-416">**SAS with stored access policy**: A stored access policy is defined on a resource container a blob container, table, or queue - and you can use it toomanage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="1fbcc-417">저장 된 액세스 정책을 사용 하 여 SAS를 연결 하면 hello SAS hello 제약 조건을 상속-hello 시작 시간, 만료 시간 및 사용 권한-hello 저장 된 액세스 정책을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-417">When you associate a SAS with a stored access policy, hello SAS inherits hello constraints - hello start time, expiry time, and permissions - defined for hello stored access policy.</span></span> <span data-ttu-id="1fbcc-418">이 유형의 SAS는 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-418">This type of SAS is revocable.</span></span>

<span data-ttu-id="1fbcc-419">자세한 내용은 참조 [공유 액세스 서명 (SAS)를 사용 하 여](storage-dotnet-shared-access-signature-part-1.md) 및 [익명 읽기 권한을 toocontainers 및 blob 관리](storage-manage-access-to-resources.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-419">For more information, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) and [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md).</span></span>

<span data-ttu-id="1fbcc-420">Hello 다음 섹션에서는 살펴보겠습니다 어떻게 toocreate Azure 테이블에 대 한 공유 액세스 서명 토큰 및 저장 된 액세스 정책.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-420">In hello next sections, you will learn how toocreate a shared access signature token and stored access policy for Azure tables.</span></span> <span data-ttu-id="1fbcc-421">Azure PowerShell은 컨테이너, Blob, 큐에 대해 유사한 cmdlet을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-421">Azure PowerShell provides similar cmdlets for containers, blobs, and queues as well.</span></span> <span data-ttu-id="1fbcc-422">이 섹션의 toorun hello 스크립트 다운로드 hello [Azure PowerShell 버전 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) 이상.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-422">toorun hello scripts in this section, download hello [Azure PowerShell version 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) or later.</span></span>

### <a name="how-toocreate-a-policy-based-shared-access-signature-token"></a><span data-ttu-id="1fbcc-423">어떻게 정책 기반 toocreate 공유 액세스 서명 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-423">How toocreate a policy-based Shared Access Signature token</span></span>
<span data-ttu-id="1fbcc-424">Hello 새로 AzureStorageTableStoredAccessPolicy cmdlet toocreate 새 저장 된 액세스 정책을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-424">Use hello New-AzureStorageTableStoredAccessPolicy cmdlet toocreate a new stored access policy.</span></span> <span data-ttu-id="1fbcc-425">그런 다음 hello 호출 [새로 AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate Azure 저장소 테이블에 대 한 새 정책 기반의 공유 액세스 서명 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-425">Then, call hello [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate a new policy-based shared access signature token for an Azure Storage table.</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-toocreate-an-ad-hoc-non-revocable-shared-access-signature-token"></a><span data-ttu-id="1fbcc-426">어떻게 toocreate 특별 한 (비 재생산할) 공유 액세스 서명 토큰</span><span class="sxs-lookup"><span data-stu-id="1fbcc-426">How toocreate an ad hoc (non-revocable) Shared Access Signature token</span></span>
<span data-ttu-id="1fbcc-427">사용 하 여 hello [새로 AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate 새 임시 (비 재생산할) 공유 액세스 서명 토큰을 Azure 저장소 테이블:</span><span class="sxs-lookup"><span data-stu-id="1fbcc-427">Use hello [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate a new ad hoc (non-revocable) Shared Access Signature token for an Azure Storage table:</span></span>

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-toocreate-a-stored-access-policy"></a><span data-ttu-id="1fbcc-428">어떻게 toocreate 저장 된 액세스 정책</span><span class="sxs-lookup"><span data-stu-id="1fbcc-428">How toocreate a stored access policy</span></span>
<span data-ttu-id="1fbcc-429">Azure 저장소 테이블에 대 한 새로운 AzureStorageTableStoredAccessPolicy hello cmdlet toocreate 새 저장 된 액세스 정책을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-429">Use hello New-AzureStorageTableStoredAccessPolicy cmdlet toocreate a new stored access policy for an Azure Storage table:</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-tooupdate-a-stored-access-policy"></a><span data-ttu-id="1fbcc-430">어떻게 tooupdate 저장 된 액세스 정책</span><span class="sxs-lookup"><span data-stu-id="1fbcc-430">How tooupdate a stored access policy</span></span>
<span data-ttu-id="1fbcc-431">Azure 저장소 테이블에 대 한 hello 집합 AzureStorageTableStoredAccessPolicy cmdlet tooupdate 기존 저장 된 액세스 정책을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-431">Use hello Set-AzureStorageTableStoredAccessPolicy cmdlet tooupdate an existing stored access policy for an Azure Storage table:</span></span>

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-toodelete-a-stored-access-policy"></a><span data-ttu-id="1fbcc-432">어떻게 toodelete 저장 된 액세스 정책</span><span class="sxs-lookup"><span data-stu-id="1fbcc-432">How toodelete a stored access policy</span></span>
<span data-ttu-id="1fbcc-433">Azure 저장소 테이블에 저장된 된 액세스 정책을 제거 AzureStorageTableStoredAccessPolicy hello cmdlet toodelete를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-433">Use hello Remove-AzureStorageTableStoredAccessPolicy cmdlet toodelete a stored access policy on an Azure Storage table:</span></span>

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-toouse-azure-storage-for-us-government-and-azure-china"></a><span data-ttu-id="1fbcc-434">어떻게 미국 정부 및 Azure 중국에 대 한 Azure 저장소 toouse</span><span class="sxs-lookup"><span data-stu-id="1fbcc-434">How toouse Azure Storage for U.S. government and Azure China</span></span>
<span data-ttu-id="1fbcc-435">[미국 정부용 Azure Government](https://azure.microsoft.com/features/gov/), [글로벌 Azure용 AzureCloud](https://portal.azure.com) 및 [중국의 21Vianet에서 운영하는 Azure용 AzureChinaCloud](http://www.windowsazure.cn/) 등의 Azure 환경은 Microsoft Azure의 독자적인 배포입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-435">An Azure environment is an independent deployment of Microsoft Azure, such as [Azure Government for U.S. government](https://azure.microsoft.com/features/gov/), [AzureCloud for global Azure](https://portal.azure.com), and [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span> <span data-ttu-id="1fbcc-436">미국 정부 및 Azure 중국을 위한 새로운 Azure 환경을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-436">You can deploy new Azure environments for U.S government and Azure China.</span></span>

<span data-ttu-id="1fbcc-437">Azure 저장소와 AzureChinaCloud toouse toocreate AzureChinaCloud와 연결 된 저장소 컨텍스트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-437">toouse Azure Storage with AzureChinaCloud, you need toocreate a storage context that is associated with AzureChinaCloud.</span></span> <span data-ttu-id="1fbcc-438">이러한 단계 tooget 시작을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-438">Follow these steps tooget you started:</span></span>

1. <span data-ttu-id="1fbcc-439">Hello 실행 [Get AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello 사용 가능한 Azure 환경:</span><span class="sxs-lookup"><span data-stu-id="1fbcc-439">Run hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello available Azure environments:</span></span>
   
    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="1fbcc-440">Azure 중국 계정 tooWindows PowerShell을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-440">Add an Azure China account tooWindows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. <span data-ttu-id="1fbcc-441">AzureChinaCloud 계정에 대한 저장소 컨텍스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-441">Create a storage context for an AzureChinaCloud account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

<span data-ttu-id="1fbcc-442">toouse Azure 저장소와 [미국 Azure Government](https://azure.microsoft.com/features/gov/)에서 Azure 저장소를 사용하려면 새 환경을 정의한 다음 이 환경으로 새 저장소 컨텍스트를 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-442">toouse Azure Storage with [U.S. Azure Government](https://azure.microsoft.com/features/gov/), you should define a new environment and then create a new storage context with this environment:</span></span>

1. <span data-ttu-id="1fbcc-443">Hello 실행 [Get AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello 사용 가능한 Azure 환경:</span><span class="sxs-lookup"><span data-stu-id="1fbcc-443">Run hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello available Azure environments:</span></span>

    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="1fbcc-444">Azure 미국 정부 계정 tooWindows PowerShell을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-444">Add an Azure US Government account tooWindows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. <span data-ttu-id="1fbcc-445">AzureUSGovernment 계정에 대한 저장소 컨텍스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-445">Create a storage context for an AzureUSGovernment account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
<span data-ttu-id="1fbcc-446">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-446">For more information, see:</span></span>

* <span data-ttu-id="1fbcc-447">[Microsoft Azure Government 개발자 가이드](../azure-government-developer-guide.md)</span><span class="sxs-lookup"><span data-stu-id="1fbcc-447">[Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>
* [<span data-ttu-id="1fbcc-448">중국 서비스에서 응용 프로그램을 만들 때의 차이점 개요</span><span class="sxs-lookup"><span data-stu-id="1fbcc-448">Overview of Differences When Creating an Application on China Service</span></span>](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a><span data-ttu-id="1fbcc-449">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1fbcc-449">Next Steps</span></span>
<span data-ttu-id="1fbcc-450">이 가이드에서 배운 어떻게 toomanage Azure PowerShell 포함 Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-450">In this guide, you've learned how toomanage Azure Storage with Azure PowerShell.</span></span> <span data-ttu-id="1fbcc-451">다음은 자세한 내용을 확인할 수 있는 몇 가지 관련 항목 및 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbcc-451">Here are some related articles and resources for learning more about them.</span></span>

* [<span data-ttu-id="1fbcc-452">Azure 저장소 설명서</span><span class="sxs-lookup"><span data-stu-id="1fbcc-452">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="1fbcc-453">Azure 저장소 PowerShell Cmdlet(영문)</span><span class="sxs-lookup"><span data-stu-id="1fbcc-453">Azure Storage PowerShell Cmdlets</span></span>](/powershell/module/azurerm.storage/#storage)
* [<span data-ttu-id="1fbcc-454">Windows PowerShell 참조</span><span class="sxs-lookup"><span data-stu-id="1fbcc-454">Windows PowerShell Reference</span></span>](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How toomanage storage accounts in Azure]: #manageaccount
[How tooset a default Azure subscription]: #setdefsub
[How toocreate a new Azure storage account]: #createaccount
[How tooset a default Azure storage account]: #defaultaccount
[How toolist all Azure storage accounts in a subscription]: #listaccounts
[How toocreate an Azure storage context]: #createctx
[How toomanage Azure blobs and blob snapshots]: #manageblobs
[How toocreate a container]: #container
[How tooupload a blob into a container]: #uploadblob
[How toodownload blobs from a container]: #downblob
[How toocopy blobs from one storage container tooanother]: #copyblob
[How toodelete a blob]: #deleteblob
[How toomanage Azure blob snapshots]: #manageshots
[How toocreate a blob snapshot]: #createshot
[How toolist snapshots of a blob]: #listshot
[How toocopy a snapshot of a blob]: #copyshot
[How toomanage Azure tables and table entities]: #managetables
[How toocreate a table]: #createtable
[How tooretrieve a table]: #gettable
[How toodelete a table]: #remtable
[How toomanage table entities]: #mngentity
[How tooadd table entities]: #addentity
[How tooquery table entities]: #queryentity
[How toodelete table entities]: #deleteentity
[How toomanage Azure queues and queue messages]: #managequeues
[How toocreate a queue]: #createqueue
[How tooretrieve a queue]: #getqueue
[How toodelete a queue]: #remqueue
[How toomanage queue messages]: #mngqueuemsg
[How tooinsert a message into a queue]: #addqueuemsg
[How toode-queue at hello next message]: #dequeuemsg
[How toomanage Azure file shares and files]: #files
[How tooset and query storage analytics]: #stganalytics
[How toomanage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How toouse Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
