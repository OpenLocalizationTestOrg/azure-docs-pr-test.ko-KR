---
title: "Azure Storage와 함께 Azure PowerShell 사용 | Microsoft Docs"
description: "Azure 저장소의 PowerShell cmdlet을 생성 및 ; blob, 테이블, 큐, 그리고 파일;을 포함하는 관리 저장소 계정구성과 쿼리 저장소 분석, 공유액세스 서명을 만드는 방법을 알아봅니다."
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
ms.openlocfilehash: 51e3e93ebedd31370857e61a00139294bcee9237
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a><span data-ttu-id="f567f-103">Azure 저장소와 함께 Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="f567f-103">Using Azure PowerShell with Azure Storage</span></span>
## <a name="overview"></a><span data-ttu-id="f567f-104">개요</span><span class="sxs-lookup"><span data-stu-id="f567f-104">Overview</span></span>
<span data-ttu-id="f567f-105">Azure PowerShell은 Windows PowerShell을 통해 Azure를 관리하기 위한 cmdlet을 제공하는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-105">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span></span> <span data-ttu-id="f567f-106">작업 기반 명령줄 셸 및 시스템 관리를 위해 특별히 설계된 스크립트 언어로,</span><span class="sxs-lookup"><span data-stu-id="f567f-106">It is a task-based command-line shell and scripting language designed especially for system administration.</span></span> <span data-ttu-id="f567f-107">PowerShell을 사용하면 Azure 서비스 및 응용 프로그램의 관리를 을 쉽게 제어하고 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-107">With PowerShell, you can easily control and automate the administration of your Azure services and applications.</span></span> <span data-ttu-id="f567f-108">예를 들어 cmdlet을 사용하여 [Azure Portal](https://portal.azure.com)을 통해 수행할 수 있는 것과 동일한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-108">For example, you can use the cmdlets to perform the same tasks that you can perform through the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="f567f-109">이 가이드에서는 [Azure Storage Cmdlet](/powershell/module/azurerm.storage/#storage) 을 사용하여 Azure Storage와 다양한 개발 및 관리 작업을 수행할 수 있는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-109">In this guide, we'll explore how to use the [Azure Storage Cmdlets](/powershell/module/azurerm.storage/#storage) to perform a variety of development and administration tasks with Azure Storage.</span></span>

<span data-ttu-id="f567f-110">이 가이드에서는 이전에 [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) 및 [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx)을 사용해 본 경험이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-110">This guide assumes that you have prior experience using [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) and [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span></span> <span data-ttu-id="f567f-111">이 가이드는 Azure 저장소에서 PowerShell을 사용하는 방법을 보여 주는 몇 가지 스크립트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-111">The guide provides a number of scripts to demonstrate the usage of PowerShell with Azure Storage.</span></span> <span data-ttu-id="f567f-112">각 스크립트를 실행하기 전에 구성에 따라 스크립트 변수를 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-112">You should update the script variables based on your configuration before running each script.</span></span>

<span data-ttu-id="f567f-113">이 가이드의 첫 번째 섹션에서는 Azure 저장소 및 PowerShell의 간략 상태를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-113">The first section in this guide provides a quick glance at Azure Storage and PowerShell.</span></span> <span data-ttu-id="f567f-114">자세한 정보 및 지침을 보려면 [Azure 저장소에서 Azure PowerShell을 사용하기 위한 필수 구성 요소](#prerequisites-for-using-azure-powershell-with-azure-storage)에서 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-114">For detailed information and instructions, start from the [Prerequisites for using Azure PowerShell with Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).</span></span>

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a><span data-ttu-id="f567f-115">5분 안에 Azure 저장소 및 PowerShell 시작하기</span><span class="sxs-lookup"><span data-stu-id="f567f-115">Getting started with Azure Storage and PowerShell in 5 minutes</span></span>
<span data-ttu-id="f567f-116">이 섹션에서는 5분 안에 PowerShell을 통해 Azure 저장소에 액세스하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-116">This section shows you how to access Azure Storage via PowerShell in 5 minutes.</span></span>

<span data-ttu-id="f567f-117">**Azure에 새로 만들기:** Microsoft Azure 구독 및 해당 구독과 연결된 Microsoft 계정을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-117">**New to Azure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="f567f-118">Azure 구입 옵션에 대한 자세한 내용은 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/), [구입 옵션](https://azure.microsoft.com/pricing/purchase-options/) 및 [회원 제안](https://azure.microsoft.com/pricing/member-offers/)(MSDN, Microsoft 파트너 네트워크, BizSpark 및 기타 Microsoft 프로그램의 회원인 경우)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="f567f-119">Azure 구독에 대한 자세한 내용은 [Azure AD(Azure Active Directory)에서 관리자 역할 할당](https://msdn.microsoft.com/library/azure/hh531793.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="f567f-120">**Microsoft Azure 구독 및 계정을 만든 후:**</span><span class="sxs-lookup"><span data-stu-id="f567f-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="f567f-121">최신 [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest)을 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-121">Download and install the latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span></span>
2. <span data-ttu-id="f567f-122">Windows PowerShell ISE(통합 스크립팅 환경)를 시작합니다. 로컬 컴퓨터에서 **시작** 메뉴로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-122">Start Windows PowerShell Integrated Scripting Environment (ISE): In your local computer, go to the **Start** menu.</span></span> <span data-ttu-id="f567f-123">**관리 도구**를 입력하고 클릭하여 관리 도구를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-123">Type **Administrative Tools** and click to run it.</span></span> <span data-ttu-id="f567f-124">**관리 도구** 창에서 **Windows PowerShell ISE**를 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-124">In the **Administrative Tools** window, right-click **Windows PowerShell ISE**, click **Run as Administrator**.</span></span>
3. <span data-ttu-id="f567f-125">**Windows PowerShell ISE**에서 **파일** > **새로 만들기**를 클릭하여 새 스크립트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-125">In **Windows PowerShell ISE**, click **File** > **New** to create a new script file.</span></span>
4. <span data-ttu-id="f567f-126">이제 Azure Storage에 액세스할 수 있는 기본 PowerShell 명령을 보여 주는 간단한 스크립트를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-126">Now, we'll give you a simple script that shows basic PowerShell commands to access Azure Storage.</span></span> <span data-ttu-id="f567f-127">이 스크립트는 먼저 로컬 PowerShell 환경에 Azure 계정을 추가하기 위해 Azure 계정 자격 증명을 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-127">The script will first ask your Azure account credentials to add your Azure account to the local PowerShell environment.</span></span> <span data-ttu-id="f567f-128">그런 다음 이 스크립트는 기본 Azure 구독을 설정하고 Azure에 새 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-128">Then, the script will set the default Azure subscription and create a new storage account in Azure.</span></span> <span data-ttu-id="f567f-129">그런 다음 이 스크립트는 새 저장소 계정에 새 컨테이너를 만들고 해당 컨테이너에 기존 이미지 파일(Blob)을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-129">Next, the script will create a new container in this new storage account and upload an existing image file (blob) to that container.</span></span> <span data-ttu-id="f567f-130">스크립트가 해당 컨테이너의 모든 Blob을 나열한 후 로컬 컴퓨터에 새 대상 디렉터리를 만들고 이미지 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-130">After the script lists all blobs in that container, it will create a new destination directory in your local computer and download the image file.</span></span>
5. <span data-ttu-id="f567f-131">다음 코드 섹션에서 주석인 **#begin**과 **#end** 사이의 스크립트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-131">In the following code section, select the script between the remarks **#begin** and **#end**.</span></span> <span data-ttu-id="f567f-132">CTRL + C 키를 눌러 해당 스크립트를 클립보드로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-132">Press CTRL+C to copy it to the clipboard.</span></span>

    ```powershell
    # begin
    # Update with the name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name to your new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name to your new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account to the local PowerShell environment.
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
       
    # Download blobs from the container:
    # Get a reference to a list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create the destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into the local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. <span data-ttu-id="f567f-133">**Windows PowerShell ISE**에서, CTRL + V를 눌러 스크립트를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-133">In **Windows PowerShell ISE**, press CTRL+V to copy the script.</span></span> <span data-ttu-id="f567f-134">**파일** > **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-134">Click **File** > **Save**.</span></span> <span data-ttu-id="f567f-135">**다른 이름으로 저장** 대화 상자 창에 "mystoragescript"와 같은 스크립트 파일의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-135">In the **Save As** dialog window, type the name of the script file, such as "mystoragescript."</span></span> <span data-ttu-id="f567f-136">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-136">Click **Save**.</span></span>
7. <span data-ttu-id="f567f-137">이제, 구성 설정에 따라 스크립트 변수를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-137">Now, you need to update the script variables based on your configuration settings.</span></span> <span data-ttu-id="f567f-138">**$SubscriptionName** 변수를 사용자 고유의 구독으로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-138">You must update the **$SubscriptionName** variable with your own subscription.</span></span> <span data-ttu-id="f567f-139">스크립트에 지정된 다른 변수를 그대로 유지하거나 원하는 대로 해당 변수를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-139">You can keep the other variables as specified in the script or update them as you wish.</span></span>
   
   * <span data-ttu-id="f567f-140">**$SubscriptionName:** 변수를 사용자 고유의 구독 이름으로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-140">**$SubscriptionName:** You must update this variable with your own subscription name.</span></span> <span data-ttu-id="f567f-141">구독 이름을 찾으려면 다음 세 방법 중 하나를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-141">Follow one of the following three ways to locate the name of your subscription:</span></span>
     
    <span data-ttu-id="f567f-142">a.</span><span class="sxs-lookup"><span data-stu-id="f567f-142">a.</span></span> <span data-ttu-id="f567f-143">**Windows PowerShell ISE**에서 **파일** > **새로 만들기**를 클릭하여 새 스크립트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-143">In **Windows PowerShell ISE**, click **File** > **New** to create a new script file.</span></span> <span data-ttu-id="f567f-144">다음 스크립트를 새 스크립트 파일에 복사하고 **디버그** > **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-144">Copy the following script to the new script file and click **Debug** > **Run**.</span></span> <span data-ttu-id="f567f-145">다음 스크립트는 먼저 로컬 PowerShell 환경에 Azure 계정을 추가하기 위해 Azure 계정 자격 증명을 요구한 다음, 로컬 PowerShell 세션에 연결된 모든 구독을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-145">The following script will first ask your Azure account credentials to add your Azure account to the local PowerShell environment and then show all the subscriptions that are connected to the local PowerShell session.</span></span> <span data-ttu-id="f567f-146">이 자습서를 수행하는 동안 사용할 구독의 이름을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-146">Take a note of the name of the subscription that you want to use while following this tutorial:</span></span>
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    <span data-ttu-id="f567f-147">b.</span><span class="sxs-lookup"><span data-stu-id="f567f-147">b.</span></span> <span data-ttu-id="f567f-148">[Azure Portal](https://portal.azure.com)에서 구독 이름을 찾아서 복사하려면 왼쪽의 허브 메뉴에서 **구독**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-148">To locate and copy your subscription name in the [Azure portal](https://portal.azure.com), in the Hub menu on the left, click **Subscriptions**.</span></span> <span data-ttu-id="f567f-149">이 가이드에서 스크립트를 실행하는 동안 사용할 구독의 이름을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-149">Copy the name of subscription that you want to use while running the scripts in this guide.</span></span>
     
     ![Azure 포털](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    <span data-ttu-id="f567f-151">c.</span><span class="sxs-lookup"><span data-stu-id="f567f-151">c.</span></span> <span data-ttu-id="f567f-152">[Azure 클래식 포털](https://manage.windowsazure.com/)에서 구독 이름을 찾아서 복사하려면 아래로 스크롤하여 포털의 왼쪽에서 **설정** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-152">To locate and copy your subscription name in the [Azure Classic Portal](https://manage.windowsazure.com/), scroll down and click **Settings** on the left side of the portal.</span></span> <span data-ttu-id="f567f-153">구독 목록을 보려면 **구독** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-153">Click **Subscriptions** to see a list of your subscriptions.</span></span> <span data-ttu-id="f567f-154">이 가이드에서 제공하는 스크립트를 실행하는 동안 사용할 구독의 이름을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-154">Copy the name of subscription that you want to use while running the scripts given in this guide.</span></span>
     
     ![Azure 클래식 포털](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * <span data-ttu-id="f567f-156">**$StorageAccountName:** 스크립트에 지정된 이름을 사용하거나 사용자 저장소 계정에 대한 새 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-156">**$StorageAccountName:** Use the given name in the script or enter a new name for your storage account.</span></span> <span data-ttu-id="f567f-157">**중요:** 저장소 계정 이름은 Azure에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-157">**Important:** The name of the storage account must be unique in Azure.</span></span> <span data-ttu-id="f567f-158">소문자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-158">It must be lowercase, too!</span></span>
   * <span data-ttu-id="f567f-159">**$Location:** : 스크립트에 지정된 "West US(미국 서부)"를 사용하거나 미국 동부, 북유럽 등의 다른 Azure 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-159">**$Location:** Use the given "West US" in the script or choose other Azure locations, such as East US, North Europe, and so on.</span></span>
   * <span data-ttu-id="f567f-160">**$ContainerName:** : 스크립트에 지정된 이름을 사용하거나 사용자 컨테이너에 대한 새 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-160">**$ContainerName:** Use the given name in the script or enter a new name for your container.</span></span>
   * <span data-ttu-id="f567f-161">**$ImageToUpload:** 로컬 컴퓨터의 그림 경로(예: "C:\Images\HelloWorld.png")를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-161">**$ImageToUpload:** Enter a path to a picture on your local computer, such as: "C:\Images\HelloWorld.png".</span></span>
   * <span data-ttu-id="f567f-162">**$DestinationFolder:** Azure Storage에서 다운로드한 파일을 보관할 로컬 디렉터리의 경로(예: “C:\DownloadImages”)를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-162">**$DestinationFolder:** Enter a path to a local directory to store files downloaded from Azure Storage, such as: "C:\DownloadImages".</span></span>
8. <span data-ttu-id="f567f-163">"mystoragescript.ps1" 파일의 스크립트 변수를 업데이트한 후 **파일** > **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-163">After updating the script variables in the "mystoragescript.ps1" file, click **File** > **Save**.</span></span> <span data-ttu-id="f567f-164">그런 다음 **디버그** > **실행**을 클릭하거나 **F5** 키를 눌러 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-164">Then, click **Debug** > **Run** or press **F5** to run the script.</span></span>  

<span data-ttu-id="f567f-165">스크립트가 실행된 후 다운로드한 이미지 파일을 포함하는 로컬 대상 폴더가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-165">After the script runs, you should have a local destination folder that includes the downloaded image file.</span></span> <span data-ttu-id="f567f-166">다음 스크린샷은 예제 출력을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-166">The following screenshot shows an example output:</span></span>

![Blob 다운로드](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> <span data-ttu-id="f567f-168">"5분 안에 Azure 저장소 및 PowerShell 시작하기' 섹션에서는 Azure 저장소와 함께 Azure PowerShell을 사용하는 방법을 간략히 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-168">The "Getting started with Azure Storage and PowerShell in 5 minutes" section provided a quick introduction on how to use Azure PowerShell with Azure Storage.</span></span> <span data-ttu-id="f567f-169">자세한 정보 및 지침을 보려면 다음 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-169">For detailed information and instructions, we encourage you to read the following sections.</span></span>
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a><span data-ttu-id="f567f-170">Azure 저장소에서 Azure PowerShell을 사용하기 위한 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="f567f-170">Prerequisites for using Azure PowerShell with Azure Storage</span></span>
<span data-ttu-id="f567f-171">이 가이드에 제공된 PowerShell cmdlet을 실행하기 위해 위에서 설명한 Azure 구독 및 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-171">You need an Azure subscription and account to run the PowerShell cmdlets given in this guide, as described above.</span></span>

<span data-ttu-id="f567f-172">Azure PowerShell은 Windows PowerShell을 통해 Azure를 관리하기 위한 cmdlet을 제공하는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-172">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span></span> <span data-ttu-id="f567f-173">Azure PowerShell 설치 및 설정에 대한 자세한 내용은 [Azure PowerShell을 설치 및 구성하는 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-173">For information on installing and setting up Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="f567f-174">이 가이드를 사용하기 전에 최신 Azure PowerShell 모듈을 다운로드 및 설치하거나, 최신 버전으로 업그레이드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-174">We recommend that you download and install or upgrade to the latest Azure PowerShell module before using this guide.</span></span>

<span data-ttu-id="f567f-175">표준 Windows PowerShell 콘솔 또는 Windows PowerShell ISE(통합 스크립팅 환경)에서 cmdlet을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-175">You can run the cmdlets in the standard Windows PowerShell console or the Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="f567f-176">예를 들어, **Windows PowerShell ISE**를 열려면 시작 메뉴로 이동하여 관리 도구를 입력하고, 이 도구를 클릭하여 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-176">For example, to open **Windows PowerShell ISE**, go to the Start menu, type Administrative Tools and click to run it.</span></span> <span data-ttu-id="f567f-177">관리 도구 창에서 Windows PowerShell ISE를 마우스 오른쪽 단추로 클릭하고 관리자 권한으로 실행을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-177">In the Administrative Tools window, right-click Windows PowerShell ISE, click Run as Administrator.</span></span>

## <a name="how-to-manage-storage-accounts-in-azure"></a><span data-ttu-id="f567f-178">Azure에서 저장소 계정을 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-178">How to manage storage accounts in Azure</span></span>

<span data-ttu-id="f567f-179">PowerShell 사용한 Azure에서 저장소 계정 관리에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-179">Let's take a look at managing storage accounts in Azure with PowerShell</span></span>

### <a name="how-to-set-a-default-azure-subscription"></a><span data-ttu-id="f567f-180">기본 Azure 구독을 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-180">How to set a default Azure subscription</span></span>
<span data-ttu-id="f567f-181">Azure PowerShell을 사용하여 Azure 저장소를 관리하려면 Azure Active Directory 인증 또는 인증서 기반 인증을 통해 Azure에서 클라이언트 환경을 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-181">To manage Azure Storage using Azure PowerShell, you need to authenticate your client environment with Azure via Azure Active Directory authentication or certificate-based authentication.</span></span> <span data-ttu-id="f567f-182">자세한 내용은 [Azure PowerShell을 설치 및 구성하는 방법](/powershell/azure/overview) 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-182">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azure/overview) tutorial.</span></span> <span data-ttu-id="f567f-183">이 가이드에서는 Azure Active Directory 인증을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-183">This guide uses the Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="f567f-184">Windows PowerShell ISE에서 다음 명령을 입력하여 로컬 PowerShell 환경에 Azure 계정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-184">In Windows PowerShell ISE, type the following command to add your Azure account to the local PowerShell environment:</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="f567f-185">“Microsoft Azure에 로그인” 창에서 계정과 연결된 메일 주소와 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-185">In the "Sign in to Microsoft Azure" window, type the email address and password associated with your account.</span></span> <span data-ttu-id="f567f-186">Azure가 자격 증명 정보를 인증 및 저장한 후 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-186">Azure authenticates and saves the credential information, and then closes the window.</span></span>

3. <span data-ttu-id="f567f-187">이제, 다음 명령을 실행하여 로컬 PowerShell 환경에서 Azure 계정을 표시하고 자신의 계정이 나열되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-187">Next, run the following command to view the Azure accounts in your local PowerShell environment, and verify that your account is listed:</span></span>
   
    ```powershell
    Get-AzureAccount
    ```
4. <span data-ttu-id="f567f-188">다음 cmdlet을 실행하여 로컬 PowerShell 세션에 연결된 모든 구독을 표시하고 자신의 구독이 나열되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-188">Then, run the following cmdlet to view all the subscriptions that are connected to the local PowerShell session, and verify that your subscription is listed:</span></span>

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. <span data-ttu-id="f567f-189">기본 Azure 구독을 설정하려면 Select-azuresubscription cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-189">To set a default Azure subscription, run the Select-AzureSubscription cmdlet:</span></span>

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. <span data-ttu-id="f567f-190">Get-AzureSubscription cmdlet을 실행하여 기본 구독 이름을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-190">Verify the name of the default subscription by running the Get-AzureSubscription cmdlet:</span></span>

    ```powershell
    Get-AzureSubscription -Default
    ```

7. <span data-ttu-id="f567f-191">Azure 저장소에 사용 가능한 모든 PowerShell cmdlet을 보려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-191">To see all the available PowerShell cmdlets for Azure Storage, run:</span></span>
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-to-create-a-new-azure-storage-account"></a><span data-ttu-id="f567f-192">새 Azure 저장소 계정을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-192">How to create a new Azure storage account</span></span>
<span data-ttu-id="f567f-193">Azure 저장소를 사용하려면 저장소 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-193">To use Azure storage, you will need a storage account.</span></span> <span data-ttu-id="f567f-194">구독에 연결하도록 컴퓨터를 구성한 후 새 Azure 저장소 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-194">You can create a new Azure storage account after you have configured your computer to connect to your subscription.</span></span>

1. <span data-ttu-id="f567f-195">Get-AzureLocation cmdlet을 실행하여 사용 가능한 모든 데이터 센터 위치를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-195">Run the Get-AzureLocation cmdlet to find all the available datacenter locations:</span></span>

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. <span data-ttu-id="f567f-196">이제 New-AzureStorageAccount cmdlet을 실행하여 새 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-196">Next, run the New-AzureStorageAccount cmdlet to create a new storage account.</span></span> <span data-ttu-id="f567f-197">다음 예제는 "West US(미국 동부)" 데이터 센터에 새 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-197">The following example creates a new storage account in the "West US" datacenter.</span></span>
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> <span data-ttu-id="f567f-198">저장소 계정의 이름은 Azure 내에서 고유하며 소문자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-198">The name of your storage account must be unique within Azure and must be lowercase.</span></span> <span data-ttu-id="f567f-199">명명 규칙 및 제한에 대해서는 [Azure Storage 계정 정보](storage-create-storage-account.md) 및 [컨테이너, Blob, 메타데이터 이름 명명 및 참조](http://msdn.microsoft.com/library/azure/dd135715.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-199">For naming conventions and restrictions, see [About Azure Storage Accounts](storage-create-storage-account.md) and [Naming and Referencing Containers, Blobs, and Metadata](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span></span>
> 
> 

### <a name="how-to-set-a-default-azure-storage-account"></a><span data-ttu-id="f567f-200">기본 Azure 저장소 계정을 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-200">How to set a default Azure storage account</span></span>
<span data-ttu-id="f567f-201">구독에서 여러 저장소 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-201">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="f567f-202">그중 하나를 선택하고 동일한 PowerShell 세션의 모든 저장소 명령에 대한 기본 저장소 계정으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-202">You can choose one of them and set it as the default storage account for all the storage commands in the same PowerShell session.</span></span> <span data-ttu-id="f567f-203">이렇게 하면 저장소 컨텍스트를 명시적으로 지정하지 않고 Azure PowerShell 저장소 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-203">This enables you to run the Azure PowerShell storage commands without specifying the storage context explicitly.</span></span>

1. <span data-ttu-id="f567f-204">구독에 대한 기본 저장소 계정을 설정하려면 Set-AzureSubscription cmdlet을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-204">To set a default storage account for your subscription, you can run the Set-AzureSubscription cmdlet.</span></span>

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. <span data-ttu-id="f567f-205">이제 Get-AzureSubscription cmdlet을 실행하여 저장소 계정이 기본 구독 계정에 연결된 것인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-205">Next, run the Get-AzureSubscription cmdlet to verify that the storage account is associated with your default subscription account.</span></span> <span data-ttu-id="f567f-206">이 명령은 현재 저장소 계정을 비롯하여 현재 구독의 구독 속성을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-206">This command returns the subscription properties on the current subscription including its current storage account.</span></span>

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-to-list-all-azure-storage-accounts-in-a-subscription"></a><span data-ttu-id="f567f-207">구독에서 모든 Azure 저장소 계정을 나열하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-207">How to list all Azure storage accounts in a subscription</span></span>
<span data-ttu-id="f567f-208">각 Azure 구독에는 최대 100개의 저장소 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-208">Each Azure subscription can have up to 100 storage accounts.</span></span> <span data-ttu-id="f567f-209">제한 사항에 대한 최신 정보는 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-209">For the most up-to-date information on limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="f567f-210">다음 cmdlet을 실행하여 현재 구독에서 사용하는 저장소 계정의 이름 및 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-210">Run the following cmdlet to find out the name and status of the storage accounts in the current subscription:</span></span>

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-to-create-an-azure-storage-context"></a><span data-ttu-id="f567f-211">Azure 저장소 컨텍스트를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-211">How to create an Azure storage context</span></span>
<span data-ttu-id="f567f-212">Azure 저장소 컨텍스트는 저장소 자격 증명을 캡슐화하는 PowerShell의 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-212">Azure storage context is an object in PowerShell to encapsulate the storage credentials.</span></span> <span data-ttu-id="f567f-213">임의의 후속 cmdlet을 실행하는 동안 저장소 컨텍스트를 사용하면 저장소 계정 및 해당 액세스 키를 명시적으로 지정하지 않고 요청을 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-213">Using a storage context while running any subsequent cmdlet enables you to authenticate your request without specifying the storage account and its access key explicitly.</span></span> <span data-ttu-id="f567f-214">저장소 계정 이름과 액세스 키, SAS(공유 액세스 서명) 토큰, 연결 문자열, 익명 등을 다양한 방식으로 저장소 컨텍스트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-214">You can create a storage context in many ways, such as using storage account name and access key, shared access signature (SAS) token, connection string, or anonymous.</span></span> <span data-ttu-id="f567f-215">자세한 내용은 [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-215">For more information, see [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span></span>  

<span data-ttu-id="f567f-216">다음 세 방법 중 하나를 사용하여 저장소 컨텍스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-216">Use one of the following three ways to create a storage context:</span></span>

* <span data-ttu-id="f567f-217">[Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet을 실행하여 Azure 저장소 계정에 대한 기본 저장소 액세스 키를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-217">Run the [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet to find out the primary storage access key for your Azure storage account.</span></span> <span data-ttu-id="f567f-218">[New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet을 호출하여 저장소 컨텍스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-218">Next, call the [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet to create a storage context:</span></span>

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* <span data-ttu-id="f567f-219">Azure 저장소 컨테이너에 대한 공유 액세스 서명 토큰 생성을 생성하여 저장소 컨텍스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-219">Generate a shared access signature token for an Azure storage container and use it to create a storage context:</span></span>

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    <span data-ttu-id="f567f-220">자세한 내용은 [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) 및 [SAS(공유 액세스 서명) 사용](storage-dotnet-shared-access-signature-part-1.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-220">For more information, see [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) and [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span></span>

* <span data-ttu-id="f567f-221">일부 경우에는 새 저장소 컨텍스트를 만들 때 서비스 끝점을 지정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-221">In some cases, you may want to specify the service endpoints when you create a new storage context.</span></span> <span data-ttu-id="f567f-222">이런 작업은 Blob 서비스를 통해 저장소 계정에 대한 사용자 지정 도메인 이름을 등록하거나 저장소 리소스에 액세스하는 데 공유 액세스 서명을 사용 하려는 경우에 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-222">This might be necessary when you have registered a custom domain name for your storage account with the Blob service or you want to use a shared access signature for accessing storage resources.</span></span> <span data-ttu-id="f567f-223">연결 문자열에 서비스 끝점을 설정하고 아래와 같이 새 저장소 컨텍스트를 만드는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-223">Set the service endpoints in a connection string and use it to create a new storage context as shown below:</span></span>

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

<span data-ttu-id="f567f-224">저장소 연결 문자열을 구성하는 방법에 대한 자세한 내용은 [연결 문자열 구성](storage-configure-connection-string.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-224">For more information on how to configure a storage connection string, see [Configuring Connection Strings](storage-configure-connection-string.md).</span></span>

<span data-ttu-id="f567f-225">이제 컴퓨터를 설정하고 Azure PowerShell을 사용하여 구독 및 저장소 계정을 관리하는 방법을 알아보았으니, 다음 섹션으로 이동하여 Azure Blob 및 스냅숏 Blob을 관리하는 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-225">Now that you have set up your computer and learned how to manage subscriptions and storage accounts using Azure PowerShell, go to the next section to learn how to manage Azure blobs and blob snapshots.</span></span>

### <a name="how-to-retrieve-and-regenerate-azure-storage-keys"></a><span data-ttu-id="f567f-226">Azure 저장소 키 검색 및 다시 생성 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-226">How to retrieve and regenerate Azure storage keys</span></span>
<span data-ttu-id="f567f-227">Azure 저장소 계정과 두 계정 키를 함께 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-227">An Azure Storage account comes with two account keys.</span></span> <span data-ttu-id="f567f-228">다음 cmdlet을 사용하여 키를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-228">You can use the following cmdlet to retrieve your keys.</span></span>

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

<span data-ttu-id="f567f-229">다음 cmdlet을 사용하여 특정 키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-229">Use the following cmdlet to retrieve a specific key.</span></span> <span data-ttu-id="f567f-230">유효한 값은 Primary 및 Secondary입니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-230">Valid values are Primary and Secondary.</span></span>  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

<span data-ttu-id="f567f-231">키를 다시 생성하려는 경우 다음 cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-231">If you would like to regenerate your keys, use the following cmdlet.</span></span> <span data-ttu-id="f567f-232">-KeyType에 대한 유효한 값은 "Primary" 및 "Secondary"입니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-232">Valid values for -KeyType are "Primary" and "Secondary"</span></span>

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-to-manage-azure-blobs"></a><span data-ttu-id="f567f-233">Azure Blob 관리 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-233">How to manage Azure blobs</span></span>
<span data-ttu-id="f567f-234">Azure Blob Storage는 HTTP 또는 HTTPS를 통해 전 세계 어디에서든 액세스할 수 있는 다량의 구조화되지 않은 데이터(예: 텍스트 또는 이진 데이터)를 저장할 수 있는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-234">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="f567f-235">이 섹션에서는 Azure Blob Storage 서비스 개념에 이미 익숙하다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-235">This section assumes that you are already familiar with the Azure Blob Storage Service concepts.</span></span> <span data-ttu-id="f567f-236">자세한 내용은 [.NET을 사용하여 Blob Storage 시작](storage-dotnet-how-to-use-blobs.md) 및 [Blob Service 개념](http://msdn.microsoft.com/library/azure/dd179376.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-236">For detailed information, see [Get started with Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="how-to-create-a-container"></a><span data-ttu-id="f567f-237">컨테이너를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-237">How to create a container</span></span>
<span data-ttu-id="f567f-238">Azure 저장소의 모든 Blob은 컨테이너에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-238">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="f567f-239">New-AzureStorageContainer cmdlet을 사용하여 개인 컨테이너를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-239">You can create a private container using the New-AzureStorageContainer cmdlet:</span></span>

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> <span data-ttu-id="f567f-240">익명 읽기 액세스의 세가지 수준은 **해제**, **Blob** 및 **컨테이너**입니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-240">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="f567f-241">Blob에 대한 익명 액세스를 방지하려면 권한 매개 변수를 **해제**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-241">To prevent anonymous access to blobs, set the Permission parameter to **Off**.</span></span> <span data-ttu-id="f567f-242">기본적으로 새 컨테이너는 전용이며 계정 소유자만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-242">By default, the new container is private and can be accessed only by the account owner.</span></span> <span data-ttu-id="f567f-243">익명 공용 읽기 권한을 Blob 리소스에 대해 허용하지만 컨테이너 메타데이터나 컨테이너의 Blob 목록에 대해서는 허용하지 않으려면, 사용 권한 매개 변수를 **Blob**으로 설정하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-243">To allow anonymous public read access to blob resources, but not to container metadata or to the list of blobs in the container, set the Permission parameter to **Blob**.</span></span> <span data-ttu-id="f567f-244">Blob 리소스, 컨테이너 메타데이터 및 컨테이너의 Blob 목록에 대한 전체 공용 읽기 권한을 허용하려면, 권한 매개 변수를 **컨테이너**로 설정하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-244">To allow full public read access to blob resources, container metadata, and the list of blobs in the container, set the Permission parameter to **Container**.</span></span> <span data-ttu-id="f567f-245">자세한 내용은 [컨테이너 및 Blob에 대한 익명 읽기 권한 관리](storage-manage-access-to-resources.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-245">For more information, see [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span></span>
> 
> 

### <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="f567f-246">컨테이너에 Blob을 업로드하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-246">How to upload a blob into a container</span></span>
<span data-ttu-id="f567f-247">Azure Blob Storage는 블록 Blob 및 페이지 Blob을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-247">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="f567f-248">자세한 내용은 [블록 Blob,추가 Blob 및 페이지 Blob 이해](http://msdn.microsoft.com/library/azure/ee691964.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-248">For more information, see [Understanding Block Blobs, Append BLobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="f567f-249">컨테이너에 Blob을 업로드하기 위해 [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-249">To upload blobs in to a container, you can use the [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet.</span></span> <span data-ttu-id="f567f-250">기본적으로 이 명령은 로컬 파일을 블록 Blob에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-250">By default, this command uploads the local files to a block blob.</span></span> <span data-ttu-id="f567f-251">Blob의 종류를 지정하기 위해 -BlobType 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-251">To specify the type for the blob, you can use the -BlobType parameter.</span></span>

<span data-ttu-id="f567f-252">다음 예제에서는 [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet을 실행하여 지정된 폴더의 모든 파일을 가져온 다음 파이프라인 연산자를 사용하여 다음 cmdlet에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-252">The following example runs the [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet to get all the files in the specified folder, and then passes them to the next cmdlet by using the pipeline operator.</span></span> <span data-ttu-id="f567f-253">[Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet은 컨테이너에 로컬 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-253">The [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet uploads the local files to your container:</span></span>

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-to-download-blobs-from-a-container"></a><span data-ttu-id="f567f-254">컨테이너에서 Blob을 다운로드하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-254">How to download blobs from a container</span></span>
<span data-ttu-id="f567f-255">다음 예제에서는 컨테이너에서 Blob을 다운로드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-255">The following example demonstrates how to download blobs from a container.</span></span> <span data-ttu-id="f567f-256">이 예제는 먼저 저장소 계정 이름 및 해당 기본 액세스 키를 포함하는 저장소 계정 컨텍스트를 사용하여 Azure 저장소에 대한 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-256">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its primary access key.</span></span> <span data-ttu-id="f567f-257">그런 다음 [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet을 사용하여 Blob 참조를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-257">Then, the example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet.</span></span> <span data-ttu-id="f567f-258">그리고 [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet을 사용하여 로컬 대상 폴더에 Blob을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-258">Next, the example uses the [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet to download blobs into the local destination folder.</span></span>

```powershell
#Define the variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-to-copy-blobs-from-one-storage-container-to-another"></a><span data-ttu-id="f567f-259">저장소 컨테이너 간에 Blob을 복사하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-259">How to copy blobs from one storage container to another</span></span>
<span data-ttu-id="f567f-260">저장소 계정 및 지역에 걸쳐 비동기적으로 Blob을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-260">You can copy blobs across storage accounts and regions asynchronously.</span></span> <span data-ttu-id="f567f-261">다음 예제에서는 두 개의 저장소 계정으로 저장소 컨테이너 간에 Blob을 복사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-261">The following example demonstrates how to copy blobs from one storage container to another in two different storage accounts.</span></span> <span data-ttu-id="f567f-262">이 예제에서는 먼저 원본 및 대상 저장소 계정의 변수를 설정하고 각 계정에 대한 저장소 컨텍스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-262">The example first sets variables for source and destination storage accounts, and then creates a storage context for each account.</span></span> <span data-ttu-id="f567f-263">그런 다음, [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet을 사용하여 원본 컨테이너에서 대상 컨테이너로 Blob을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-263">Next, the example copies blobs from the source container to the destination container using the [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet.</span></span> <span data-ttu-id="f567f-264">이 예제에서는 원본 및 대상 저장소 계정과 컨테이너가 이미 존재한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-264">The example assumes that the source and destination storage accounts and containers already exist.</span></span>

```powershell
#Define the source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define the destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference to blobs in the source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container to another.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

<span data-ttu-id="f567f-265">이 예제에서는 비동기 복사본을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-265">Note that this example performs an asynchronous copy.</span></span> <span data-ttu-id="f567f-266">[Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet을 실행하여 각 복사본의 상태를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-266">You can monitor the status of each copy by running the [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.</span></span>

### <a name="how-to-copy-blobs-from-a-secondary-location"></a><span data-ttu-id="f567f-267">보조 위치에서 blob를 복사하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-267">How to copy blobs from a secondary location</span></span>
<span data-ttu-id="f567f-268">활성화 RA-GRS 계정의 보조 locatioon에서 blob을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-268">You can copy blobs from the secondary location of a RA-GRS-enabled account.</span></span>

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-to-delete-a-blob"></a><span data-ttu-id="f567f-269">Blob을 삭제하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-269">How to delete a blob</span></span>
<span data-ttu-id="f567f-270">Blob을 삭제하려면 먼저 Blob 참조를 가져온 다음 해당 참조에 대해 Remove-AzureStorageBlob cmdlet을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-270">To delete a blob, first get a blob reference and then call the Remove-AzureStorageBlob cmdlet on it.</span></span> <span data-ttu-id="f567f-271">다음 예제에서는 지정된 컨테이너의 모든 Blob을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-271">The following example deletes all the blobs in a given container.</span></span> <span data-ttu-id="f567f-272">이 예제에서는 먼저 저장소 계정에 대한 변수를 설정하고 저장소 컨텍스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-272">The example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="f567f-273">그런 다음, [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet을 사용하여 Blob 참조를 검색하고 [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet을 실행하여 Azure Storage의 컨테이너에서 Blob을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-273">Next, the example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs the [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet to remove blobs from a container in Azure storage.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference to all the blobs in the container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-to-manage-azure-blob-snapshots"></a><span data-ttu-id="f567f-274">Azure Blob 스냅숏을 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-274">How to manage Azure blob snapshots</span></span>
<span data-ttu-id="f567f-275">Azure를 사용하면 Blob의 스냅숏을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-275">Azure lets you create a snapshot of a blob.</span></span> <span data-ttu-id="f567f-276">스냅숏은 특정 시점에 생성된 Blob의 읽기 전용 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-276">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="f567f-277">스냅숏이 생성된 후에는 읽거나 복사하거나 삭제할 수 있지만 수정할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-277">Once a snapshot has been created, it can be read, copied, or deleted, but not modified.</span></span> <span data-ttu-id="f567f-278">스냅숏을 사용하면 특정 시점에서 표시된 대로 Blob을 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-278">Snapshots provide a way to back up a blob as it appears at a moment in time.</span></span> <span data-ttu-id="f567f-279">자세한 내용은 [Blob의 스냅숏 만들기](http://msdn.microsoft.com/library/azure/hh488361.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-279">For more information, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span>

### <a name="how-to-create-a-blob-snapshot"></a><span data-ttu-id="f567f-280">Blob 스냅숏을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-280">How to create a blob snapshot</span></span>
<span data-ttu-id="f567f-281">Blob을 만들려면 먼저 Blob 참조를 가져온 다음 그에 대한 `ICloudBlob.CreateSnapshot` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-281">To create a snaphot of a blob, first get a blob reference and then call the `ICloudBlob.CreateSnapshot` method on it.</span></span> <span data-ttu-id="f567f-282">다음 예제에서는 먼저 저장소 계정에 대한 변수를 설정하고 저장소 컨텍스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-282">The following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="f567f-283">그런 다음, [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet을 사용하여 Blob 참조를 검색하고 [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) 메서드를 실행하여 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-283">Next, the example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs the [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method to create a snapshot.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference to a blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of the blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-to-list-a-blobs-snapshots"></a><span data-ttu-id="f567f-284">Blob의 스냅숏을 나열하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-284">How to list a blob's snapshots</span></span>
<span data-ttu-id="f567f-285">Blob에 대해 원하는 수 만큼 많은 스냅샷을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-285">You can create as many snapshots as you want for a blob.</span></span> <span data-ttu-id="f567f-286">Blob에 연결된 스냅숏을 나열하여 최신 스냅숏을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-286">You can list the snapshots associated with your blob to track your current snapshots.</span></span> <span data-ttu-id="f567f-287">다음 예제에서는 미리 정의된 Blob을 사용하며 [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet을 호출하여 Blob의 스냅숏을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-287">The following example uses a predefined blob and calls the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet to list the snapshots of that blob.</span></span>  

```powershell
#Define the blob name.
$BlobName = "yourblobname"

#List the snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-to-copy-a-snapshot-of-a-blob"></a><span data-ttu-id="f567f-288">Blob의 스냅숏을 복사하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-288">How to copy a snapshot of a blob</span></span>
<span data-ttu-id="f567f-289">Blob의 스냅숏을 복사하여 Blob의 스냅숏을 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-289">You can copy a snapshot of a blob to restore the snapshot.</span></span> <span data-ttu-id="f567f-290">자세한 내용 및 제한 사항에 대해서는 [Blob의 스냅숏 만들기](http://msdn.microsoft.com/library/azure/hh488361.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-290">For detailed information and restrictions, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span> <span data-ttu-id="f567f-291">다음 예제에서는 먼저 저장소 계정에 대한 변수를 설정하고 저장소 컨텍스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-291">The following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="f567f-292">그런 다음, 컨테이너 및 Blob 이름 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-292">Next, the example defines the container and blob name variables.</span></span> <span data-ttu-id="f567f-293">이 예제는 [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet을 사용하여 Blob 참조를 검색하고 [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) 메서드를 실행하여 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-293">The example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs the [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method to create a snapshot.</span></span> <span data-ttu-id="f567f-294">그런 다음, [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet을 실행하여 원본 Blob에 대한 ICloudBlob 개체를 통해 Blob의 스냅숏을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-294">Then, the example runs the [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet to copy the snapshot of a blob using the ICloudBlob object for the source blob.</span></span> <span data-ttu-id="f567f-295">이 예제를 실행하기 전에 구성에 따라 변수를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-295">Be sure to update the variables based on your configuration before running the example.</span></span> <span data-ttu-id="f567f-296">다음 예제에서는 원본 및 대상 컨테이너와 원본 Blob이 이미 존재한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-296">Note that the following example assumes that the source and destination containers, and the source blob already exist.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define the variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference to a blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy the snapshot to another container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

<span data-ttu-id="f567f-297">이제 Azure PowerShell을 사용하여 Azure Blob 및 Blob 스냅숏을 관리하는 방법을 알아보았으니, 다음 섹션으로 이동하여 테이블, 큐 및 파일을 관리하는 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-297">Now that you have learned how to manage Azure blobs and blob snapshots with Azure PowerShell, go to the next section to learn how to manage tables, queues, and files.</span></span>

## <a name="how-to-manage-azure-tables-and-table-entities"></a><span data-ttu-id="f567f-298">Azure 테이블 및 테이블 엔터티를 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-298">How to manage Azure tables and table entities</span></span>
<span data-ttu-id="f567f-299">Azure 테이블 저장소 서비스는 구조화된 비관계형 데이터의 거대 집합을 저장하고 쿼리하는 데 사용할 수 있는 NoSQL 데이터 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-299">Azure Table storage service is a NoSQL datastore, which you can use to store and query huge sets of structured, non-relational data.</span></span> <span data-ttu-id="f567f-300">서비스의 주요 구성 요소로는 테이블, 엔터티 및 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-300">The main components of the service are tables, entities, and properties.</span></span> <span data-ttu-id="f567f-301">테이블은 엔터티 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-301">A table is a collection of entities.</span></span> <span data-ttu-id="f567f-302">엔터티는 속성의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-302">An entity is a set of properties.</span></span> <span data-ttu-id="f567f-303">각 엔터티는 모두 이름 값 쌍으로 구성된 속성을 최대 252개 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-303">Each entity can have up to 252 properties, which are all name-value pairs.</span></span> <span data-ttu-id="f567f-304">이 섹션에서는 Azure 테이블 저장소 서비스 개념에 이미 익숙하다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-304">This section assumes that you are already familiar with the Azure Table Storage Service concepts.</span></span> <span data-ttu-id="f567f-305">자세한 내용은 [Table Service 데이터 모델 이해](http://msdn.microsoft.com/library/azure/dd179338.aspx) 및 [.NET을 사용하여 Azure Table Storage 시작](storage-dotnet-how-to-use-tables.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-305">For detailed information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) and [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="f567f-306">다음 하위 섹션에서는 Azure PowerShell을 사용하여 Azure Table Storage 서비스를 관리하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-306">In the following subsections, you'll learn how to manage Azure Table storage service using Azure PowerShell.</span></span> <span data-ttu-id="f567f-307">여기서 다루는 시나리오에는 **테이블** **생성**, **삭제** 및 **검색**뿐만 아니라 테이블 엔터티 **추가**, **쿼리** 및 **삭제**도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-307">The scenarios covered include **creating**, **deleting**, and **retrieving** **tables**, as well as **adding**, **querying**, and **deleting table entities**.</span></span>

### <a name="how-to-create-a-table"></a><span data-ttu-id="f567f-308">테이블을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-308">How to create a table</span></span>
<span data-ttu-id="f567f-309">모든 테이블은 Azure 저장소 계정에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-309">Every table must reside in an Azure storage account.</span></span> <span data-ttu-id="f567f-310">다음 예제에서는 Azure 저장소에 테이블을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-310">The following example demonstrates how to create a table in Azure Storage.</span></span> <span data-ttu-id="f567f-311">이 예제는 먼저 저장소 계정 이름 및 해당 액세스 키를 포함하는 저장소 계정 컨텍스트를 사용하여 Azure 저장소에 대한 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-311">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="f567f-312">그런 다음, [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet을 사용하여 Azure 저장소에 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-312">Next, it uses the [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet to create a table in Azure Storage.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-to-retrieve-a-table"></a><span data-ttu-id="f567f-313">테이블을 검색하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-313">How to retrieve a table</span></span>
<span data-ttu-id="f567f-314">저장소 계정에서 한 테이블 또는 모든 테이블을 쿼리하고 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-314">You can query and retrieve one or all tables in a Storage account.</span></span> <span data-ttu-id="f567f-315">다음 예제에서는 [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet을 사용하여 지정된 테이블을 검색하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-315">The following example demonstrates how to retrieve a given table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span>

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

<span data-ttu-id="f567f-316">매개 변수 없이 Get-AzureStorageTable cmdlet을 호출하는 경우 저장소 계정에 대한 모든 저장소 테이블을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-316">If you call the Get-AzureStorageTable cmdlet without any parameters, it gets all storage tables for a Storage account.</span></span>

### <a name="how-to-delete-a-table"></a><span data-ttu-id="f567f-317">테이블을 삭제하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-317">How to delete a table</span></span>
<span data-ttu-id="f567f-318">[Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet을 사용하여 저장소 계정에서 테이블을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-318">You can delete a table from a storage account by using the [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.</span></span>  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-to-manage-table-entities"></a><span data-ttu-id="f567f-319">테이블 엔터티를 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-319">How to manage table entities</span></span>
<span data-ttu-id="f567f-320">현재, Azure PowerShell은 테이블 엔터티를 직접 관리할 수 있는 cmdlet을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-320">Currently, Azure PowerShell does not provide cmdlets to manage table entities directly.</span></span> <span data-ttu-id="f567f-321">테이블 엔터티에 대한 작업을 수행하려면 [.NET용 Azure 저장소 클라이언트 라이브러리](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx)에 지정된 클래스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-321">To perform operations on table entities, you can use the classes given in the [Azure Storage Client Library for .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span></span>

#### <a name="how-to-add-table-entities"></a><span data-ttu-id="f567f-322">테이블 엔터티를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-322">How to add table entities</span></span>
<span data-ttu-id="f567f-323">테이블에 엔터티를 추가하려면 먼저 엔터티 속성을 정의하는 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-323">To add an entity to a table, first create an object that defines your entity properties.</span></span> <span data-ttu-id="f567f-324">엔터티는 3개의 시스템 속성 즉, **PartitionKey**, **RowKey** 및 **Timestamp**를 포함하여 최대 255개의 속성을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-324">An entity can have up to 255 properties, including 3 system properties: **PartitionKey**, **RowKey**, and **Timestamp**.</span></span> <span data-ttu-id="f567f-325">**PartitionKey** 및 **RowKey**의 값을 삽입 및 업데이트하는 작업은 사용자가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-325">You are responsible for inserting and updating the values of **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="f567f-326">서버는 수정할 수 없는 **Timestamp**값을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-326">The server manages the value of **Timestamp**, which cannot be modified.</span></span> <span data-ttu-id="f567f-327">**PartitionKey** 및 **RowKey**가 함께 테이블 내의 모든 엔터티를 고유하게 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-327">Together the **PartitionKey** and **RowKey** uniquely identify every entity within a table.</span></span>

* <span data-ttu-id="f567f-328">**PartitionKey**: 엔터티가 저장되는 파티션을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-328">**PartitionKey**: Determines the partition that the entity is stored in.</span></span>
* <span data-ttu-id="f567f-329">**RowKey**: 파티션 내에서 엔터티를 고유하게 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-329">**RowKey**: Uniquely identifies the entity within the partition.</span></span>

<span data-ttu-id="f567f-330">엔터티에 대한 사용자 지정 속성을 최대 252개 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-330">You may define up to 252 custom properties for an entity.</span></span> <span data-ttu-id="f567f-331">자세한 내용은 [테이블 서비스 데이터 모델 이해](http://msdn.microsoft.com/library/azure/dd179338.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-331">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="f567f-332">다음 예제에서는 테이블에 엔터티를 추가하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-332">The following example demonstrates how to add entities to a table.</span></span> <span data-ttu-id="f567f-333">이 예제에는 직원 테이블을 검색하고 여기에 여러 엔터티를 추가하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-333">The example shows how to retrieve the employee table and add several entities into it.</span></span> <span data-ttu-id="f567f-334">먼저, 저장소 계정 이름 및 해당 액세스 키를 포함하는 저장소 계정 컨텍스트를 사용하여 Azure 저장소에 대한 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-334">First, it establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="f567f-335">그런 다음 [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet을 사용하여 지정된 테이블을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-335">Next, it retrieves the given table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="f567f-336">테이블이 없는 경우 [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet이 Azure 저장소에 테이블을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-336">If the table does not exist, the [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet is used to create a table in Azure Storage.</span></span> <span data-ttu-id="f567f-337">각 엔터티의 파티션 및 행 키를 지정하여 테이블에 엔터티를 추가하는 사용자 지정 Add-Entity를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-337">Next, the example defines a custom function Add-Entity to add entities to the table by specifying each entity's partition and row key.</span></span> <span data-ttu-id="f567f-338">Add-Entity 함수는 [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) 클래스에 대한 [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet을 호출하여 엔터티 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-338">The Add-Entity function calls the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on the [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) class to create an entity object.</span></span> <span data-ttu-id="f567f-339">나중에, 이 예제는 이 엔터티 개체에 대한 [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) 메서드를 호출하여 테이블에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-339">Later, the example calls the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) method on this entity object to add it to a table.</span></span>

```powershell
#Function Add-Entity: Adds an employee entity to a table.
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

#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve the table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities to a table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-to-query-table-entities"></a><span data-ttu-id="f567f-340">테이블 엔터티를 쿼리하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-340">How to query table entities</span></span>
<span data-ttu-id="f567f-341">테이블을 쿼리하기 위해 [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-341">To query a table, use the [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) class.</span></span> <span data-ttu-id="f567f-342">다음 예제에서는 가이드의 엔터티를 추가하는 방법 섹션에 지정된 스크립트를 이미 실행한 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-342">The following example assumes that you've already run the script given in the How to add entities section of this guide.</span></span> <span data-ttu-id="f567f-343">이 예제는 먼저 저장소 계정 이름 및 해당 액세스 키를 포함하는 저장소 컨텍스트를 사용하여 Azure 저장소에 대한 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-343">The example first establishes a connection to Azure Storage using the storage context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="f567f-344">그런 다음 [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet을 사용하여 앞서 만든 “Employees” 테이블을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-344">Next, it tries to retrieve the previously created "Employees" table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="f567f-345">Microsoft.WindowsAzure.Storage.Table.TableQuery 클래스에 대해 [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet을 호출하면 새 쿼리 개체가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-345">Calling the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on the Microsoft.WindowsAzure.Storage.Table.TableQuery class creates a new query object.</span></span> <span data-ttu-id="f567f-346">이 예제에서는 값이 문자열 필터에 지정된 대로 1 인 ‘ID’ 열을 포함하는 엔터티를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-346">The example looks for the entities that have an 'ID' column whose value is 1 as specified in a string filter.</span></span> <span data-ttu-id="f567f-347">자세한 내용은 [테이블 및 엔터티 쿼리](http://msdn.microsoft.com/library/azure/dd894031.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-347">For detailed information, see [Querying Tables and Entities](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span></span> <span data-ttu-id="f567f-348">이 쿼리를 실행하면 필터 조건과 일치하는 모든 엔터티가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-348">When you run this query, it returns all entities that match the filter criteria.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference to a table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns to select.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute the query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with the table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-to-delete-table-entities"></a><span data-ttu-id="f567f-349">테이블 엔터티를 삭제하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-349">How to delete table entities</span></span>
<span data-ttu-id="f567f-350">파티션 및 행 키를 사용하여 엔터티를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-350">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="f567f-351">다음 예제에서는 가이드의 엔터티를 추가하는 방법 섹션에 지정된 스크립트를 이미 실행한 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-351">The following example assumes that you've already run the script given in the How to add entities section of this guide.</span></span> <span data-ttu-id="f567f-352">이 예제는 먼저 저장소 계정 이름 및 해당 액세스 키를 포함하는 저장소 컨텍스트를 사용하여 Azure 저장소에 대한 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-352">The example first establishes a connection to Azure Storage using the storage context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="f567f-353">그런 다음 [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet을 사용하여 앞서 만든 “Employees” 테이블을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-353">Next, it tries to retrieve the previously created "Employees" table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="f567f-354">테이블이 있는 경우 이 예제는 [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) 메서드를 호출하여 파티션 및 행 키 값을 기준으로 엔터티를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-354">If the table exists, the example calls the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) method to retrieve an entity based on its partition and row key values.</span></span> <span data-ttu-id="f567f-355">그런 다음 엔터티를 삭제할 [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) 메서드로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-355">Then, pass the entity to the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) method to delete.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve the table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If the table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together the PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete the entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-to-manage-azure-queues-and-queue-messages"></a><span data-ttu-id="f567f-356">Azure 큐 및 큐 메시지를 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-356">How to manage Azure queues and queue messages</span></span>
<span data-ttu-id="f567f-357">Azure 큐 저장소는 HTTP 또는 HTTPS를 사용하여 인증된 호출을 통해 전 세계 어디에서나 액세스할 수 있는 다수의 메시지를 저장하기 위한 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-357">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="f567f-358">이 섹션에서는 Azure 큐 저장소 서비스 개념에 이미 익숙하다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-358">This section assumes that you are already familiar with the Azure Queue Storage Service concepts.</span></span> <span data-ttu-id="f567f-359">자세한 내용은 [.NET을 사용하여 Azure 큐 저장소 시작](storage-dotnet-how-to-use-queues.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-359">For detailed information, see [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md).</span></span>

<span data-ttu-id="f567f-360">이 섹션에서는 Azure PowerShell을 사용하여 Azure 큐 저장소 서비스를 관리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-360">This section will show you how to manage Azure Queue storage service using Azure PowerShell.</span></span> <span data-ttu-id="f567f-361">여기서 다루는 시나리오에는 큐 메시지 **삽입** 및 **삭제**뿐만 아니라 큐 **생성**, **삭제** 및 **검색**도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-361">The scenarios covered include **inserting** and **deleting** queue messages, as well as **creating**, **deleting**, and **retrieving queues**.</span></span>

### <a name="how-to-create-a-queue"></a><span data-ttu-id="f567f-362">큐를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-362">How to create a queue</span></span>
<span data-ttu-id="f567f-363">다음 예제는 먼저 저장소 계정 이름 및 해당 액세스 키를 포함하는 저장소 계정 컨텍스트를 사용하여 Azure 저장소에 대한 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-363">The following example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="f567f-364">그런 다음 [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet을 호출하여 ‘queuename’이라는 큐를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-364">Next, it calls [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet to create a queue named 'queuename'.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

<span data-ttu-id="f567f-365">Azure 큐 서비스에 대한 명명 규칙에 대해서는 [큐 및 메타데이터 이름 지정](http://msdn.microsoft.com/library/azure/dd179349.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-365">For information on naming conventions for Azure Queue Service, see [Naming Queues and Metadata](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

### <a name="how-to-retrieve-a-queue"></a><span data-ttu-id="f567f-366">큐를 검색하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-366">How to retrieve a queue</span></span>
<span data-ttu-id="f567f-367">저장소 계정의 특정 큐 또는 모든 큐의 목록을 쿼리하고 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-367">You can query and retrieve a specific queue or a list of all the queues in a Storage account.</span></span> <span data-ttu-id="f567f-368">다음 예제에서는 [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet을 사용하여 지정된 큐를 검색하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-368">The following example demonstrates how to retrieve a specified queue using the [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.</span></span>

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

<span data-ttu-id="f567f-369">매개 변수 없이 [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet을 호출하는 경우 모든 큐의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-369">If you call the [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet without any parameters, it gets a list of all the queues.</span></span>

### <a name="how-to-delete-a-queue"></a><span data-ttu-id="f567f-370">큐를 삭제하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-370">How to delete a queue</span></span>
<span data-ttu-id="f567f-371">큐와 해당 큐에 포함된 모든 메시지를 삭제하려면 Remove-AzureStorageQueue cmdlet을 호출하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-371">To delete a queue and all the messages contained in it, call the Remove-AzureStorageQueue cmdlet.</span></span> <span data-ttu-id="f567f-372">다음 예제에서는 Remove-AzureStorageQueue cmdlet을 사용하여 지정된 큐를 삭제하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-372">The following example shows how to delete a specified queue using the Remove-AzureStorageQueue cmdlet.</span></span>

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="f567f-373">큐에 메시지를 삽입하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-373">How to insert a message into a queue</span></span>
<span data-ttu-id="f567f-374">기존 큐에 메시지를 삽입하려면 먼저 [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) 클래스의 새 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-374">To insert a message into an existing queue, first create a new instance of the [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="f567f-375">그런 다음, [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-375">Next, call the [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method.</span></span> <span data-ttu-id="f567f-376">문자열(UTF-8 형식) 또는 바이트 배열에서 CloudQueueMessage를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-376">A CloudQueueMessage can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="f567f-377">다음 예제에서는 큐에 메시지를 추가하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-377">The following example demonstrates how to add message to a queue.</span></span> <span data-ttu-id="f567f-378">이 예제는 먼저 저장소 계정 이름 및 해당 액세스 키를 포함하는 저장소 계정 컨텍스트를 사용하여 Azure 저장소에 대한 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-378">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="f567f-379">그런 다음 [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet을 사용하여 지정된 큐를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-379">Next, it retrieves the specified queue using the [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span></span> <span data-ttu-id="f567f-380">큐가 있는 경우 [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet이 [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) 클래스의 인스턴스를 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-380">If the queue exists, the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet is used to create an instance of the [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="f567f-381">나중에, 이 예제는 이 메시지 개체에 대한 [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) 메서드를 호출하여 큐에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-381">Later, the example calls the [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method on this message object to add it to a queue.</span></span> <span data-ttu-id="f567f-382">다음은 큐를 검색하고 'MessageInfo' 메시지를 삽입하는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-382">Here is code which retrieves a queue and inserts the message 'MessageInfo':</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve the queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If the queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of the CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message to the queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-to-de-queue-at-the-next-message"></a><span data-ttu-id="f567f-383">다음 메시지에서 큐를 제거하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-383">How to de-queue at the next message</span></span>
<span data-ttu-id="f567f-384">다음 코드는 2단계를 거쳐 큐에서 메시지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-384">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="f567f-385">[Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) 메서드를 호출하면 큐에서 다음 메시지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-385">When you call the [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) method, you get the next message in a queue.</span></span> <span data-ttu-id="f567f-386">**GetMessage** 에서 반환된 메시지는 이 큐의 메시지를 읽는 다른 코드에는 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-386">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="f567f-387">큐에서 메시지 제거를 완료하려면 [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) 메서드도 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-387">To finish removing the message from the queue, you must also call the [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) method.</span></span> <span data-ttu-id="f567f-388">메시지를 제거하는 이 2단계 프로세스는 코드가 하드웨어 또는 소프트웨어 오류로 인해 메시지를 처리하지 못하는 경우 코드의 다른 인스턴스가 동일한 메시지를 가져와서 다시 시도할 수 있도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-388">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="f567f-389">코드는 메시지가 처리된 직후에 **DeleteMessage** 를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-389">Your code calls **DeleteMessage** right after the message has been processed.</span></span>

```powershell
# Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve the queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get the message object from the queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete the message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-to-manage-azure-file-shares-and-files"></a><span data-ttu-id="f567f-390">Azure 파일 공유 및 파일을 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-390">How to manage Azure file shares and files</span></span>
<span data-ttu-id="f567f-391">Azure 파일 저장소는 표준 SMB 프로토콜을 사용하여 응용 프로그램을 위한 공유 저장소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-391">Azure File storage offers shared storage for applications using the standard SMB protocol.</span></span> <span data-ttu-id="f567f-392">Microsoft Azure 가상 컴퓨터 및 클라우드 서비스는 탑재된 공유를 통해 여러 응용 프로그램 구성 요소에서 파일 데이터를 공유할 수 있으며 온-프레미스 응용 프로그램은 파일 저장소 API 또는 Azure PowerShell을 통해 공유의 파일 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-392">Microsoft Azure virtual machines and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share via the File storage API or Azure PowerShell.</span></span>

<span data-ttu-id="f567f-393">Azure File Storage에 대한 자세한 내용은 [Windows에서 Azure File Storage 시작](storage-dotnet-how-to-use-files.md) 및 [파일 서비스 REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-393">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) and [File Service REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span></span>

## <a name="how-to-set-and-query-storage-analytics"></a><span data-ttu-id="f567f-394">저장소 분석을 설정 및 쿼리하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-394">How to set and query storage analytics</span></span>
<span data-ttu-id="f567f-395">[Azure 저장소 분석](storage-analytics.md) 을 통해 Azure 저장소 계정에서 메트릭(저장소 메트릭)을 수집하고 저장소 계정에 전송된 요청에 대한 데이터(저장소 로깅)를 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-395">You can use [Azure Storage Analytics](storage-analytics.md) to collect metrics for your Azure storage accounts and log data about requests sent to your storage account.</span></span> <span data-ttu-id="f567f-396">저장소 메트릭을 사용하여 저장소 계정의 상태를 모니터링하고, 저장소 로깅을 사용하여 저장소 계정에 대한 문제를 진단 및 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-396">You can use storage metrics to monitor the health of a storage account, and storage logging to diagnose and troubleshoot issues with your storage account.</span></span> <span data-ttu-id="f567f-397">Azure Portal 또는 Windows PowerShell을 사용하거나 저장소 클라이언트 라이브러리를 사용하여 프로그래밍 방식으로 모니터링을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-397">You can configure monitoring using the Azure portal or Windows PowerShell, or programmatically using the storage client library.</span></span> <span data-ttu-id="f567f-398">저장소 로깅은 서버 쪽에서 발생하며, 이를 통해 저장소 계정의 성공한 요청 및 실패한 요청에 대한 세부 정보를 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-398">Storage logging happens server-side and enables you to record details for both successful and failed requests in your storage account.</span></span> <span data-ttu-id="f567f-399">이러한 로그를 사용하여 테이블, 큐 및 Blob에 대한 읽기, 쓰기 및 삭제 작업뿐만 아니라 실패한 요청의 이유에 대한 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-399">These logs enable you to see details of read, write, and delete operations against your tables, queues, and blobs as well as the reasons for failed requests.</span></span>

<span data-ttu-id="f567f-400">PowerShell을 사용하여 저장소 메트릭 데이터를 사용하도록 설정하고 확인하는 방법을 알아보려면 [PowerShell을 사용하여 저장소 메트릭을 사용하도록 설정하는 방법](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-400">To learn how to enable and view Storage Metrics data using PowerShell, see [How to enable Storage Metrics using PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span></span>

<span data-ttu-id="f567f-401">PowerShell을 사용하여 저장소 로깅 데이터를 사용하도록 설정하고 검색하는 방법을 알아보려면 [PowerShell을 사용하여 저장소 로깅을 활성화하는 방법](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell)과 [저장소 로깅 로그 데이터 찾기](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-401">To learn how to enable and retrieve Storage Logging data using PowerShell, see [How to enable Storage Logging using PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) and [Finding your Storage Logging log data](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span></span>
<span data-ttu-id="f567f-402">저장소 메트릭 및 저장소 로깅을 사용하여 저장소 문제를 해결하는 방법에 대한 자세한 정보는 [Microsoft Azure 저장소 모니터링, 진단 및 문제 해결](storage-monitoring-diagnosing-troubleshooting.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-402">For detailed information on using Storage Metrics and Storage Logging to troubleshoot storage issues, see [Monitoring, Diagnosing, and Troubleshooting Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).</span></span>

## <a name="how-to-manage-shared-access-signature-sas-and-stored-access-policy"></a><span data-ttu-id="f567f-403">SAS(공유 액세스 서명) 및 저장된 액세스 정책을 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-403">How to manage Shared Access Signature (SAS) and Stored Access Policy</span></span>
<span data-ttu-id="f567f-404">공유 액세스 서명은 Azure 저장소를 사용하는 모든 응용 프로그램에 대한 보안 모델의 중요한 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-404">Shared access signatures are an important part of the security model for any application using Azure Storage.</span></span> <span data-ttu-id="f567f-405">공유 액세스 서명은 저장소 계정에 대한 제한된 권한을 계정 키가 필요하지 않은 클라이언트에 제공하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-405">They are useful for providing limited permissions to your storage account to clients that should not have the account key.</span></span> <span data-ttu-id="f567f-406">기본적으로는 저장소 계정 소유자만 해당 계정 내의 Blob, 테이블 및 큐에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-406">By default, only the owner of the storage account may access blobs, tables, and queues within that account.</span></span> <span data-ttu-id="f567f-407">사용하는 서비스 또는 응용 프로그램에서 자신의 액세스 키를 공유하지 않고 다른 클라이언트가 이러한 리소스를 사용할 수 있도록 설정해야 할 경우 다음과 같은 세 가지 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-407">If your service or application needs to make these resources available to other clients without sharing your access key, you have three options:</span></span>

* <span data-ttu-id="f567f-408">컨테이너 및 해당 Blob에 대한 익명 읽기 액세스를 허용하도록 컨테이너의 사용 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-408">Set a container's permissions to permit anonymous read access to the container and its blobs.</span></span> <span data-ttu-id="f567f-409">테이블 또는 큐에 대해서는 이렇게 할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-409">This is not allowed for tables or queues.</span></span>
* <span data-ttu-id="f567f-410">일정 기간 동안 컨테이너, Blob, 큐 및 테이블에 제한된 액세스 권한을 부여하는 공유 액세스 서명을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-410">Use a shared access signature that grants restricted access rights to containers, blobs, queues, and tables for a specific time interval.</span></span>
* <span data-ttu-id="f567f-411">컨테이너나 해당 Blob, 큐 또는 테이블에 대한 공유 액세스 서명을 더 효과적으로 제어하기 위한 저장된 액세스 정책을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-411">Use a stored access policy to obtain an additional level of control over shared access signatures for a container or its blobs, for a queue, or for a table.</span></span> <span data-ttu-id="f567f-412">저장된 액세스 정책을 사용하여 시작 시간, 만료 시간 또는 서명 사용 권한을 변경하거나 발급 후에 서명을 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-412">The stored access policy allows you to change the start time, expiry time, or permissions for a signature, or to revoke it after it has been issued.</span></span>

<span data-ttu-id="f567f-413">공유 액세스 서명은 다음 두 가지 형식 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-413">A shared access signature can be in one of two forms:</span></span>

* <span data-ttu-id="f567f-414">**Ad hoc SAS**: 애드혹 SAS를 만들 때 SAS의 시작 시간, 만료 시간 및 사용 권한이 SAS URI에 모두 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-414">**Ad hoc SAS**: When you create an ad hoc SAS, the start time, expiry time, and permissions for the SAS are all specified on the SAS URI.</span></span> <span data-ttu-id="f567f-415">이 유형의 SAS는 컨테이너, Blob, 테이블 또는 큐에서 만들 수 있으며, 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-415">This type of SAS may be created on a container, blob, table, or queue and it is non-revocable.</span></span>
* <span data-ttu-id="f567f-416">**저장된 액세스 정책 사용 SAS:**저장된 액세스 정책은 리소스 컨테이너(Blob 컨테이너, 테이블 또는 큐)에서 정의되며, 하나 이상의 공유 액세스 서명에 대한 제약 조건을 관리하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-416">**SAS with stored access policy**: A stored access policy is defined on a resource container a blob container, table, or queue - and you can use it to manage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="f567f-417">SAS를 공유 액세스 정책과 연결할 경우 SAS는 저장된 액세스 정책에 대해 정의된 제약 조건(시작 시간, 만료 시간 및 사용 권한)을 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-417">When you associate a SAS with a stored access policy, the SAS inherits the constraints - the start time, expiry time, and permissions - defined for the stored access policy.</span></span> <span data-ttu-id="f567f-418">이 유형의 SAS는 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-418">This type of SAS is revocable.</span></span>

<span data-ttu-id="f567f-419">자세한 내용은 [SAS(공유 액세스 서명) 사용](storage-dotnet-shared-access-signature-part-1.md) 및 [컨테이너 및 Blob에 대한 익명 읽기 권한 관리](storage-manage-access-to-resources.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-419">For more information, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) and [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span></span>

<span data-ttu-id="f567f-420">다음 섹션에서는 Azure 테이블에 대한 공유 액세스 서명 토큰 및 저장된 액세스 정책을 만드는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-420">In the next sections, you will learn how to create a shared access signature token and stored access policy for Azure tables.</span></span> <span data-ttu-id="f567f-421">Azure PowerShell은 컨테이너, Blob, 큐에 대해 유사한 cmdlet을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-421">Azure PowerShell provides similar cmdlets for containers, blobs, and queues as well.</span></span> <span data-ttu-id="f567f-422">이 섹션의 스크립트를 실행하려면 [Azure PowerShell 버전 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) 이상을 다운로드하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-422">To run the scripts in this section, download the [Azure PowerShell version 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) or later.</span></span>

### <a name="how-to-create-a-policy-based-shared-access-signature-token"></a><span data-ttu-id="f567f-423">공유 액세스 서명 토큰에 따라 정책을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-423">How to create a policy-based Shared Access Signature token</span></span>
<span data-ttu-id="f567f-424">저장된 새 액세스 정책을 만들려면 New-AzureStorageTableStoredAccessPolicy cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-424">Use the New-AzureStorageTableStoredAccessPolicy cmdlet to create a new stored access policy.</span></span> <span data-ttu-id="f567f-425">그런 다음 [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet을 호출하여 Azure 저장소 테이블에 대한 새 정책 기반의 공유 액세스 서명 토큰을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-425">Then, call the [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet to create a new policy-based shared access signature token for an Azure Storage table.</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-to-create-an-ad-hoc-non-revocable-shared-access-signature-token"></a><span data-ttu-id="f567f-426">임시(취소 불가능한) 공유 액세스 서명 토큰을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-426">How to create an ad hoc (non-revocable) Shared Access Signature token</span></span>
<span data-ttu-id="f567f-427">Azure 저장소 테이블에 대한 임시(취소 불가능한) 공유 액세스 서명 토큰을 만들려면 [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-427">Use the [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet to create a new ad hoc (non-revocable) Shared Access Signature token for an Azure Storage table:</span></span>

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-to-create-a-stored-access-policy"></a><span data-ttu-id="f567f-428">저장된 액세스 정책을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-428">How to create a stored access policy</span></span>
<span data-ttu-id="f567f-429">Azure 저장소 테이블에 대해 저장된 새 액세스 정책을 만들려면 New-AzureStorageTableStoredAccessPolicy cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-429">Use the New-AzureStorageTableStoredAccessPolicy cmdlet to create a new stored access policy for an Azure Storage table:</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-to-update-a-stored-access-policy"></a><span data-ttu-id="f567f-430">저장된 액세스 정책을 업데이트하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-430">How to update a stored access policy</span></span>
<span data-ttu-id="f567f-431">Azure 저장소 테이블에 대해 저장된 기존 새 액세스 정책을 업데이트하려면 Set-AzureStorageTableStoredAccessPolicy cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-431">Use the Set-AzureStorageTableStoredAccessPolicy cmdlet to update an existing stored access policy for an Azure Storage table:</span></span>

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-to-delete-a-stored-access-policy"></a><span data-ttu-id="f567f-432">저장된 액세스 정책을 삭제하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-432">How to delete a stored access policy</span></span>
<span data-ttu-id="f567f-433">Azure 저장소 테이블에서 저장된 액세스 정책을 삭제하려면 Remove-AzureStorageTableStoredAccessPolicy cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-433">Use the Remove-AzureStorageTableStoredAccessPolicy cmdlet to delete a stored access policy on an Azure Storage table:</span></span>

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-to-use-azure-storage-for-us-government-and-azure-china"></a><span data-ttu-id="f567f-434">미국 정부 및 Azure 중국용 Azure 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="f567f-434">How to use Azure Storage for U.S. government and Azure China</span></span>
<span data-ttu-id="f567f-435">[미국 정부용 Azure Government](https://azure.microsoft.com/features/gov/), [글로벌 Azure용 AzureCloud](https://portal.azure.com) 및 [중국의 21Vianet에서 운영하는 Azure용 AzureChinaCloud](http://www.windowsazure.cn/) 등의 Azure 환경은 Microsoft Azure의 독자적인 배포입니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-435">An Azure environment is an independent deployment of Microsoft Azure, such as [Azure Government for U.S. government](https://azure.microsoft.com/features/gov/), [AzureCloud for global Azure](https://portal.azure.com), and [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span> <span data-ttu-id="f567f-436">미국 정부 및 Azure 중국을 위한 새로운 Azure 환경을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-436">You can deploy new Azure environments for U.S government and Azure China.</span></span>

<span data-ttu-id="f567f-437">AzureChinaCloud와 함께 Azure 저장소를 사용하려면 AzureChinaCloud와 연결된 저장소 컨텍스트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-437">To use Azure Storage with AzureChinaCloud, you need to create a storage context that is associated with AzureChinaCloud.</span></span> <span data-ttu-id="f567f-438">시작하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-438">Follow these steps to get you started:</span></span>

1. <span data-ttu-id="f567f-439">[Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet을 실행하여 사용 가능한 Azure 환경을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-439">Run the [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet to see the available Azure environments:</span></span>
   
    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="f567f-440">Windows PowerShell에 Azure 중국 계정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-440">Add an Azure China account to Windows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. <span data-ttu-id="f567f-441">AzureChinaCloud 계정에 대한 저장소 컨텍스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-441">Create a storage context for an AzureChinaCloud account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

<span data-ttu-id="f567f-442">[U.S. Azure Government](https://azure.microsoft.com/features/gov/)에서 Azure 저장소를 사용하려면 새 환경을 정의한 다음 이 환경으로 새 저장소 컨텍스트를 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-442">To use Azure Storage with [U.S. Azure Government](https://azure.microsoft.com/features/gov/), you should define a new environment and then create a new storage context with this environment:</span></span>

1. <span data-ttu-id="f567f-443">[Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet을 실행하여 사용 가능한 Azure 환경을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-443">Run the [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet to see the available Azure environments:</span></span>

    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="f567f-444">Windows PowerShell에 Azure 미국 정부 계정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-444">Add an Azure US Government account to Windows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. <span data-ttu-id="f567f-445">AzureUSGovernment 계정에 대한 저장소 컨텍스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-445">Create a storage context for an AzureUSGovernment account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
<span data-ttu-id="f567f-446">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f567f-446">For more information, see:</span></span>

* <span data-ttu-id="f567f-447">[Microsoft Azure Government 개발자 가이드](../azure-government-developer-guide.md)</span><span class="sxs-lookup"><span data-stu-id="f567f-447">[Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>
* [<span data-ttu-id="f567f-448">중국 서비스에서 응용 프로그램을 만들 때의 차이점 개요</span><span class="sxs-lookup"><span data-stu-id="f567f-448">Overview of Differences When Creating an Application on China Service</span></span>](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a><span data-ttu-id="f567f-449">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f567f-449">Next Steps</span></span>
<span data-ttu-id="f567f-450">이 가이드에서는 Azure PowerShell을 사용하여 Azure 저장소를 관리하는 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-450">In this guide, you've learned how to manage Azure Storage with Azure PowerShell.</span></span> <span data-ttu-id="f567f-451">다음은 자세한 내용을 확인할 수 있는 몇 가지 관련 항목 및 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="f567f-451">Here are some related articles and resources for learning more about them.</span></span>

* [<span data-ttu-id="f567f-452">Azure 저장소 설명서</span><span class="sxs-lookup"><span data-stu-id="f567f-452">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="f567f-453">Azure 저장소 PowerShell Cmdlet(영문)</span><span class="sxs-lookup"><span data-stu-id="f567f-453">Azure Storage PowerShell Cmdlets</span></span>](/powershell/module/azurerm.storage/#storage)
* [<span data-ttu-id="f567f-454">Windows PowerShell 참조</span><span class="sxs-lookup"><span data-stu-id="f567f-454">Windows PowerShell Reference</span></span>](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How to manage storage accounts in Azure]: #manageaccount
[How to set a default Azure subscription]: #setdefsub
[How to create a new Azure storage account]: #createaccount
[How to set a default Azure storage account]: #defaultaccount
[How to list all Azure storage accounts in a subscription]: #listaccounts
[How to create an Azure storage context]: #createctx
[How to manage Azure blobs and blob snapshots]: #manageblobs
[How to create a container]: #container
[How to upload a blob into a container]: #uploadblob
[How to download blobs from a container]: #downblob
[How to copy blobs from one storage container to another]: #copyblob
[How to delete a blob]: #deleteblob
[How to manage Azure blob snapshots]: #manageshots
[How to create a blob snapshot]: #createshot
[How to list snapshots of a blob]: #listshot
[How to copy a snapshot of a blob]: #copyshot
[How to manage Azure tables and table entities]: #managetables
[How to create a table]: #createtable
[How to retrieve a table]: #gettable
[How to delete a table]: #remtable
[How to manage table entities]: #mngentity
[How to add table entities]: #addentity
[How to query table entities]: #queryentity
[How to delete table entities]: #deleteentity
[How to manage Azure queues and queue messages]: #managequeues
[How to create a queue]: #createqueue
[How to retrieve a queue]: #getqueue
[How to delete a queue]: #remqueue
[How to manage queue messages]: #mngqueuemsg
[How to insert a message into a queue]: #addqueuemsg
[How to de-queue at the next message]: #dequeuemsg
[How to manage Azure file shares and files]: #files
[How to set and query storage analytics]: #stganalytics
[How to manage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How to use Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
