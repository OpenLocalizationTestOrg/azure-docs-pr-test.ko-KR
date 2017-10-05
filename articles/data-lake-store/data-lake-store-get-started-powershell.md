---
title: "PowerShell을 사용하여 Azure Data Lake Store 시작 | Microsoft Docs"
description: "Azure PowerShell을 사용하여 데이터 레이크 저장소 계정을 만들고 기본 작업을 수행합니다."
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf85f369-f9aa-4ca1-9ae7-e03a78eb7290
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 23c9aaa089251bff5132652475f4daadc2c128fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-powershell"></a><span data-ttu-id="98eb5-103">Azure PowerShell을 사용하여 Azure 데이터 레이크 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="98eb5-103">Get started with Azure Data Lake Store using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="98eb5-104">포털</span><span class="sxs-lookup"><span data-stu-id="98eb5-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="98eb5-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="98eb5-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="98eb5-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="98eb5-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="98eb5-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="98eb5-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="98eb5-108">REST API</span><span class="sxs-lookup"><span data-stu-id="98eb5-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="98eb5-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="98eb5-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="98eb5-110">Node.JS</span><span class="sxs-lookup"><span data-stu-id="98eb5-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="98eb5-111">Python</span><span class="sxs-lookup"><span data-stu-id="98eb5-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="98eb5-112">Azure PowerShell을 사용하여 Azure 데이터 레이크 저장소 계정을 만들고 폴더 만들기, 데이터 파일 업로드 및 다운로드, 계정 삭제 등의 기본 작업을 수행하는 방법에 대해 알아봅니다. Data Lake Store에 대한 자세한 내용은 [Data Lake Store 개요](data-lake-store-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98eb5-112">Learn how to use Azure PowerShell to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98eb5-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="98eb5-113">Prerequisites</span></span>
<span data-ttu-id="98eb5-114">이 자습서를 시작하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-114">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="98eb5-115">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="98eb5-115">**An Azure subscription**.</span></span> <span data-ttu-id="98eb5-116">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98eb5-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="98eb5-117">**Azure PowerShell 1.0 이상**.</span><span class="sxs-lookup"><span data-stu-id="98eb5-117">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="98eb5-118">[Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98eb5-118">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="authentication"></a><span data-ttu-id="98eb5-119">인증</span><span class="sxs-lookup"><span data-stu-id="98eb5-119">Authentication</span></span>
<span data-ttu-id="98eb5-120">이 문서는 Data Lake Store에 Azure 계정 자격 증명을 입력하라는 메시지가 표시되는 보다 간단한 인증 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-120">This article uses a simpler authentication approach with Data Lake Store where you are prompted to enter your Azure account credentials.</span></span> <span data-ttu-id="98eb5-121">Data Lake Store 계정 및 파일 시스템에 대한 액세스 수준은 로그인한 사용자의 액세스 수준을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-121">The access level to Data Lake Store account and file system is then governed by the access level of the logged in user.</span></span> <span data-ttu-id="98eb5-122">하지만 Data Lake Store에 인증하는 다른 방법인 **최종 사용자 인증** 또는 **서비스간 인증**도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-122">However, there are other approaches as well to authenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="98eb5-123">지침 및 인증 방법에 대한 자세한 내용은 [최종 사용자 인증](data-lake-store-end-user-authenticate-using-active-directory.md) 또는 [서비스 간 인증](data-lake-store-authenticate-using-active-directory.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98eb5-123">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="98eb5-124">Azure 데이터 레이크 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="98eb5-124">Create an Azure Data Lake Store account</span></span>
1. <span data-ttu-id="98eb5-125">데스크톱에서 새 Windows PowerShell 창을 열고 다음 조각을 입력하여 Azure 계정에 로그인하고 구독을 설정한 다음 Data Lake Store 공급자를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-125">From your desktop, open a new Windows PowerShell window, and enter the following snippet to log in to your Azure account, set the subscription, and register the Data Lake Store provider.</span></span> <span data-ttu-id="98eb5-126">로그인하라는 메시지가 표시되면 구독 관리자/소유자 중 하나로 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-126">When prompted to log in, make sure you log in as one of the subscription admininistrators/owner:</span></span>

        # Log in to your Azure account
        Login-AzureRmAccount

        # List all the subscriptions associated to your account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. <span data-ttu-id="98eb5-127">Azure 데이터 레이크 저장소 계정은 Azure 리소스 그룹과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-127">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="98eb5-128">Azure 리소스 그룹을 만드는 작업부터 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-128">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="98eb5-129">![Azure 리소스 그룹 만들기](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Azure 리소스 그룹 만들기")</span><span class="sxs-lookup"><span data-stu-id="98eb5-129">![Create an Azure Resource Group](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")</span></span>
3. <span data-ttu-id="98eb5-130">Azure 데이터 레이크 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-130">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="98eb5-131">지정하는 이름은 소문자와 숫자만 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-131">The name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="98eb5-132">![Azure Data Lake Store 계정 만들기](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Azure Data Lake Store 계정 만들기")</span><span class="sxs-lookup"><span data-stu-id="98eb5-132">![Create an Azure Data Lake Store account](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake Store account")</span></span>
4. <span data-ttu-id="98eb5-133">계정이 성공적으로 만들어졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-133">Verify that the account is successfully created.</span></span>

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    <span data-ttu-id="98eb5-134">이에 대한 출력은 **True**여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-134">The output for this should be **True**.</span></span>

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a><span data-ttu-id="98eb5-135">Azure 데이터 레이크 저장소에서 디렉터리 구조 만들기</span><span class="sxs-lookup"><span data-stu-id="98eb5-135">Create directory structures in your Azure Data Lake Store</span></span>
<span data-ttu-id="98eb5-136">Azure 데이터 레이크 저장소 계정에서 디렉터리를 만들어 데이터를 관리하고 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-136">You can create directories under your Azure Data Lake Store account to manage and store data.</span></span>

1. <span data-ttu-id="98eb5-137">루트 디렉터리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-137">Specify a root directory.</span></span>

        $myrootdir = "/"
2. <span data-ttu-id="98eb5-138">지정된 루트 아래 **mynewdirectory** 라는 새 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-138">Create a new directory called **mynewdirectory** under the specified root.</span></span>

        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. <span data-ttu-id="98eb5-139">새 디렉터리가 성공적으로 만들어졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-139">Verify that the new directory is successfully created.</span></span>

        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir

    <span data-ttu-id="98eb5-140">다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-140">It should show an output like the following:</span></span>

    <span data-ttu-id="98eb5-141">![디렉터리 확인](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "디렉터리 확인")</span><span class="sxs-lookup"><span data-stu-id="98eb5-141">![Verify Directory](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verify Directory")</span></span>

## <a name="upload-data-to-your-azure-data-lake-store"></a><span data-ttu-id="98eb5-142">Azure 데이터 레이크 저장소에 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="98eb5-142">Upload data to your Azure Data Lake Store</span></span>
<span data-ttu-id="98eb5-143">루트 수준에서 데이터 레이크 저장소에 직접 데이터를 업로드하거나 계정 내에서 만든 디렉터리에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-143">You can upload your data to Data Lake Store directly at the root level or to a directory that you created within the account.</span></span> <span data-ttu-id="98eb5-144">아래 코드 조각은 이전 섹션에서 만든 디렉터리(**mynewdirectory**)에 일부 샘플 데이터를 업로드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-144">The snippets below demonstrate how to upload some sample data to the directory (**mynewdirectory**) you created in the previous section.</span></span>

<span data-ttu-id="98eb5-145">업로드할 일부 샘플 데이터를 찾는 경우 **Azure 데이터 레이크 Git 리포지토리** 의 [Ambulance Data](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData)폴더에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-145">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="98eb5-146">파일을 다운로드하고 컴퓨터의 로컬 디렉터리(예: C:\sampledata\)에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-146">Download the file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a><span data-ttu-id="98eb5-147">데이터 레이크 저장소에서 데이터 이름 바꾸기, 다운로드 및 삭제</span><span class="sxs-lookup"><span data-stu-id="98eb5-147">Rename, download, and delete data from your Data Lake Store</span></span>
<span data-ttu-id="98eb5-148">파일의 이름을 바꾸려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-148">To rename a file, use the following command:</span></span>

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="98eb5-149">파일을 다운로드하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-149">To download a file, use the following command:</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

<span data-ttu-id="98eb5-150">파일을 삭제하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-150">To delete a file, use the following command:</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="98eb5-151">메시지가 표시되면 **Y** 를 입력하여 항목을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-151">When prompted, enter **Y** to delete the item.</span></span> <span data-ttu-id="98eb5-152">삭제할 파일이 둘 이상 있는 경우 쉼표로 구분하여 모든 경로를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-152">If you have more than one file to delete, you can provide all the paths separated by comma.</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a><span data-ttu-id="98eb5-153">Azure 데이터 레이크 저장소 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="98eb5-153">Delete your Azure Data Lake Store account</span></span>
<span data-ttu-id="98eb5-154">다음 명령을 사용하여 데이터 레이크 저장소 계정을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-154">Use the following command to delete your Data Lake Store account.</span></span>

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

<span data-ttu-id="98eb5-155">메시지가 표시되면 **Y** 를 입력하여 계정을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-155">When prompted, enter **Y** to delete the account.</span></span>

## <a name="performance-guidance-while-using-powershell"></a><span data-ttu-id="98eb5-156">PowerShell을 사용하는 동안 성능 지침</span><span class="sxs-lookup"><span data-stu-id="98eb5-156">Performance guidance while using PowerShell</span></span>

<span data-ttu-id="98eb5-157">Data Lake Store와 함께 PowerShell을 사용하는 동안 최상의 성능을 얻기 위해 조정할 수 있는 가장 중요한 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-157">Below are the most important settings that can be tuned to get the best performance while using PowerShell to work with Data Lake Store:</span></span>

| <span data-ttu-id="98eb5-158">속성</span><span class="sxs-lookup"><span data-stu-id="98eb5-158">Property</span></span>            | <span data-ttu-id="98eb5-159">기본값</span><span class="sxs-lookup"><span data-stu-id="98eb5-159">Default</span></span> | <span data-ttu-id="98eb5-160">설명</span><span class="sxs-lookup"><span data-stu-id="98eb5-160">Description</span></span> |
|---------------------|---------|-------------|
| <span data-ttu-id="98eb5-161">PerFileThreadCount</span><span class="sxs-lookup"><span data-stu-id="98eb5-161">PerFileThreadCount</span></span>  | <span data-ttu-id="98eb5-162">10</span><span class="sxs-lookup"><span data-stu-id="98eb5-162">10</span></span>      | <span data-ttu-id="98eb5-163">이 매개 변수로 각 파일의 업로드 또는 다운로드를 위한 병렬 스레드 수를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-163">This parameter enables you to choose the number of parallel threads for uploading or downloading each file.</span></span> <span data-ttu-id="98eb5-164">이 숫자는 파일당 할당할 수 있는 최대 스레드 수를 나타내지만 시나리오에 따라 스레드 수가 줄어들 수 있습니다(예를 들어 1KB 파일을 업로드하는 경우 20개의 스레드를 요청해도 하나의 스레드가 발생합니다).</span><span class="sxs-lookup"><span data-stu-id="98eb5-164">This number represents the max threads that can be allocated per file, but you may get less threads depending on your scenario (e.g. if you are uploading a 1KB file, you will get one thread even if you ask for 20 threads).</span></span>  |
| <span data-ttu-id="98eb5-165">ConcurrentFileCount</span><span class="sxs-lookup"><span data-stu-id="98eb5-165">ConcurrentFileCount</span></span> | <span data-ttu-id="98eb5-166">10</span><span class="sxs-lookup"><span data-stu-id="98eb5-166">10</span></span>      | <span data-ttu-id="98eb5-167">이 매개 변수는 특히 폴더 업로드 또는 다운로드를 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-167">This parameter is specifically for uploading or downloading folders.</span></span> <span data-ttu-id="98eb5-168">이 매개 변수는 업로드 또는 다운로드할 수 있는 동시 파일 수를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-168">This parameter determines the number of concurrent files that can be uploaded or downloaded.</span></span> <span data-ttu-id="98eb5-169">이 숫자는 한 번에 업로드 또는 다운로드할 수 있는 최대 동시 파일 수를 나타내지만 시나리오에 따라 동시 수가 줄어들 수 있습니다(예를 들어 두 개 파일을 업로드하는 경우 15개를 요청해도 두 개의 동시 파일 업로드가 발생합니다).</span><span class="sxs-lookup"><span data-stu-id="98eb5-169">This number represents the maximum number of concurrent files that can be uploaded or downloaded at one time, but you may get less concurrency depending on your scenario (e.g. if you are uploading two files, you will get two concurrent file uploads even if you ask for 15).</span></span> |

<span data-ttu-id="98eb5-170">**예제**</span><span class="sxs-lookup"><span data-stu-id="98eb5-170">**Example**</span></span>

<span data-ttu-id="98eb5-171">이 명령은 파일당 20개의 스레드와 100개의 동시 파일을 사용하여 Azure Data Lake Store에서 사용자의 로컬 드라이브로 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-171">This command downloads files from Azure Data Lake Store to the user's local drive using 20 threads per file and 100 concurrent files.</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

### <a name="how-do-i-determine-the-value-to-set-for-these-parameters"></a><span data-ttu-id="98eb5-172">이러한 매개 변수에 대한 설정 값은 어떻게 결정하나요?</span><span class="sxs-lookup"><span data-stu-id="98eb5-172">How do I determine the value to set for these parameters?</span></span>

<span data-ttu-id="98eb5-173">다음은 사용할 수 있는 몇 가지 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-173">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="98eb5-174">**1단계: 총 스레드 수 확인** - 사용할 총 스레드 수를 계산하는 것으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-174">**Step 1: Determine the total thread count** - You should start by calculating the total thread count to use.</span></span> <span data-ttu-id="98eb5-175">일반적으로 물리적 코어당 6개의 스레드를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-175">As a general guideline, you should use 6 threads for each physical core.</span></span>

        Total thread count = total physical cores * 6

    <span data-ttu-id="98eb5-176">**예제**</span><span class="sxs-lookup"><span data-stu-id="98eb5-176">**Example**</span></span>

    <span data-ttu-id="98eb5-177">16개의 코어가 있는 D14 VM에서 PowerShell 명령을 실행 중이라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-177">Assuming you are running the PowerShell commands from a D14 VM that has 16 cores</span></span>

        Total thread count = 16 cores * 6 = 96 threads


* <span data-ttu-id="98eb5-178">**2단계: PerFileThreadCount 계산**  - 파일 크기를 기반으로 PerFileThreadCount를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-178">**Step 2: Calculate PerFileThreadCount**  - We calculate our PerFileThreadCount based on the size of the files.</span></span> <span data-ttu-id="98eb5-179">2.5GB 미만 파일인 경우 기본값인 10이면 충분하므로 이 매개 변수를 변경하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-179">For files smaller than 2.5GB, there is no need to change this parameter because the default of 10 is sufficient.</span></span> <span data-ttu-id="98eb5-180">2.5GB 초과 파일인 경우 처음 2.5GB를 기준으로 10개 스레드를 사용하고 파일 크기가 256MB 증가당 1개 스레드를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-180">For files larger than 2.5GB, you should use 10 threads as the base for the first 2.5GB and add 1 thread for each additional 256MB increase in file size.</span></span> <span data-ttu-id="98eb5-181">더 큰 크기의 파일 범위로 폴더를 복사하는 경우 보다 작은 파일 크기로 그룹화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-181">If you are copying a folder with a large range of file sizes, consider grouping them into similar file sizes.</span></span> <span data-ttu-id="98eb5-182">다른 파일 크기를 사용하면 성능이 저하될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-182">Having dissimilar file sizes may cause non-optimal performance.</span></span> <span data-ttu-id="98eb5-183">유사한 파일 크기를 그룹화할 수 없는 경우 가장 큰 파일 크기를 기준으로 PerFileThreadCount를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-183">If that's not possible to group similar file sizes, you should set PerFileThreadCount based on the largest file size.</span></span>

        PerFileThreadCount = 10 threads for the first 2.5GB + 1 thread for each additional 256MB increase in file size

    <span data-ttu-id="98eb5-184">**예제**</span><span class="sxs-lookup"><span data-stu-id="98eb5-184">**Example**</span></span>

    <span data-ttu-id="98eb5-185">1GB ~ 10GB 범위의 100개 파일이 있다고 가정하면 수식에서 가장 큰 파일 크기로 10GB를 사용하며 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-185">Assuming you have 100 files ranging from 1GB to 10GB, we use the 10GB as the largest file size for equation, which would read like the following.</span></span>

        PerFileThreadCount = 10 + ((10GB - 2.5GB) / 256MB) = 40 threads

* <span data-ttu-id="98eb5-186">**3단계: ConcurrentFilecount 계산** - 총 스레드 수와 PerFileThreadCount를 사용하여 다음 수식에 따라 ConcurrentFileCount를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-186">**Step 3: Calculate ConcurrentFilecount** - Use the total thread count and PerFileThreadCount to calculate ConcurrentFileCount based on the following equation.</span></span>

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    <span data-ttu-id="98eb5-187">**예제**</span><span class="sxs-lookup"><span data-stu-id="98eb5-187">**Example**</span></span>

    <span data-ttu-id="98eb5-188">사용 중인 예제 값 기준</span><span class="sxs-lookup"><span data-stu-id="98eb5-188">Based on the example values we have been using</span></span>

        96 = 40 * ConcurrentFileCount

    <span data-ttu-id="98eb5-189">따라서 **ConcurrentFileCount**는 **2.4**이고 **2**로 반올림할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-189">So, **ConcurrentFileCount** is **2.4**, which we can round off to **2**.</span></span>

### <a name="further-tuning"></a><span data-ttu-id="98eb5-190">추가 조정</span><span class="sxs-lookup"><span data-stu-id="98eb5-190">Further tuning</span></span>

<span data-ttu-id="98eb5-191">작동하는 파일 크기 범위가 다양하므로 추가 조정이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-191">You might require further tuning because there is a range of file sizes to work with.</span></span> <span data-ttu-id="98eb5-192">위의 계산은 모든 또는 대부분의 파일이 10GB 범위보다 크거나 비슷한 경우 잘 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-192">The above calculation works well if all or most of the files are larger and closer to the 10GB range.</span></span> <span data-ttu-id="98eb5-193">그렇지 않고 작은 파일이 많고 파일 크기가 매우 다양한 경우 PerFileThreadCount를 줄이면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-193">If instead, there are many different files sizes with many files being smaller, then you could reduce PerFileThreadCount.</span></span> <span data-ttu-id="98eb5-194">PerFileThreadCount를 줄여서 ConcurrentFileCount를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-194">By reducing the PerFileThreadCount, we can increase ConcurrentFileCount.</span></span> <span data-ttu-id="98eb5-195">따라서 대부분의 파일이 5GB 범위보다 작다면 계산을 다시 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-195">So, if we assume that most of our files are smaller in the 5GB range, we can re-do our calculation:</span></span>

    PerFileThreadCount = 10 + ((5GB - 2.5GB) / 256MB) = 20

<span data-ttu-id="98eb5-196">즉, **ConcurrentFileCount**는 96/20(4.8)이 되고 **4**로 반올림됩니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-196">So, **ConcurrentFileCount** will now be 96/20, which is 4.8, rounded off to **4**.</span></span>

<span data-ttu-id="98eb5-197">파일 크기 분포에 따라 **PerFileThreadCount**를 늘리거나 줄여 이러한 설정을 계속해서 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-197">You can continue to tune these settings by changing the **PerFileThreadCount** up and down depending on the distribution of your file sizes.</span></span>

### <a name="limitation"></a><span data-ttu-id="98eb5-198">제한 사항</span><span class="sxs-lookup"><span data-stu-id="98eb5-198">Limitation</span></span>

* <span data-ttu-id="98eb5-199">**파일 수가 ConcurrentFileCount보다 작음**: 업로드 중인 파일 수가 계산한 **ConcurrentFileCount**보다 작은 경우 **ConcurrentFileCount**가 파일 수와 같도록 줄여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-199">**Number of files is less than ConcurrentFileCount**: If the number of files you are uploading is smaller than the **ConcurrentFileCount** that you calculated, then you should reduce **ConcurrentFileCount** to be equal to the number of files.</span></span> <span data-ttu-id="98eb5-200">나머지 스레드를 사용하여 **PerFileThreadCount**를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-200">You can use any remaining threads to increase **PerFileThreadCount**.</span></span>

* <span data-ttu-id="98eb5-201">**스레드 수 너무 많음**: 클러스터 크기를 늘리지 않고 스레드 수를 너무 늘리면 성능 저하 위험이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-201">**Too many threads**: If you increase thread count too much without increasing your cluster size, you run the risk of degraded performance.</span></span> <span data-ttu-id="98eb5-202">CPU에서 컨텍스트 전환 시 경합 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-202">There can be contention issues when context-switching on the CPU.</span></span>

* <span data-ttu-id="98eb5-203">**동시성 부족**: 동시성이 부족한 경우 클러스터가 너무 작을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-203">**Insufficient concurrency**: If the concurrency is not sufficient, then your cluster may be too small.</span></span> <span data-ttu-id="98eb5-204">더 많은 동시성을 제공하도록 클러스터에서 노드 수를 늘릴 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="98eb5-204">You can increase the number of nodes in your cluster which will give you more concurrency.</span></span>

* <span data-ttu-id="98eb5-205">**제한 오류**: 동시성이 너무 높으면 제한 오류가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98eb5-205">**Throttling errors**: You may see throttling errors if your concurrency is too high.</span></span> <span data-ttu-id="98eb5-206">제한 오류가 표시되면 동시성을 줄이거나 문의해 주세요.</span><span class="sxs-lookup"><span data-stu-id="98eb5-206">If you are seeing throttling errors, you should either reduce the concurrency or contact us.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98eb5-207">다음 단계</span><span class="sxs-lookup"><span data-stu-id="98eb5-207">Next steps</span></span>
* [<span data-ttu-id="98eb5-208">데이터 레이크 저장소의 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="98eb5-208">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="98eb5-209">Azure 데이터 레이크 분석에 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="98eb5-209">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="98eb5-210">Azure HDInsight에 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="98eb5-210">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

