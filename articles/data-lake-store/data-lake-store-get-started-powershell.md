---
title: "Azure 데이터 레이크 저장소 aaaUse PowerShell tooget 시작 | Microsoft Docs"
description: "Azure PowerShell toocreate 데이터 레이크 저장소 계정을 사용 하 고 기본 작업 수행"
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
ms.openlocfilehash: 9c958bfd63e412ec0b0a4113a149f61aee026bc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-powershell"></a><span data-ttu-id="1b49a-103">Azure PowerShell을 사용하여 Azure 데이터 레이크 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="1b49a-103">Get started with Azure Data Lake Store using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1b49a-104">포털</span><span class="sxs-lookup"><span data-stu-id="1b49a-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="1b49a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b49a-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="1b49a-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="1b49a-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="1b49a-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="1b49a-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="1b49a-108">REST API</span><span class="sxs-lookup"><span data-stu-id="1b49a-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="1b49a-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1b49a-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="1b49a-110">Node.JS</span><span class="sxs-lookup"><span data-stu-id="1b49a-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="1b49a-111">Python</span><span class="sxs-lookup"><span data-stu-id="1b49a-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="1b49a-112">Azure 데이터 레이크는 저장 하는 Azure PowerShell toocreate toouse 방법에 대해 알아봅니다 계정 및 폴더를 만들어 업로드 및 다운로드 데이터 파일 등의 기본 작업 수행, 계정, 등을 삭제 합니다. Data Lake Store에 대한 자세한 내용은 [Data Lake Store 개요](data-lake-store-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b49a-112">Learn how toouse Azure PowerShell toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b49a-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1b49a-113">Prerequisites</span></span>
<span data-ttu-id="1b49a-114">이 자습서를 시작 하기 전에 hello 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-114">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="1b49a-115">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="1b49a-115">**An Azure subscription**.</span></span> <span data-ttu-id="1b49a-116">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b49a-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="1b49a-117">**Azure PowerShell 1.0 이상**.</span><span class="sxs-lookup"><span data-stu-id="1b49a-117">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="1b49a-118">참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-118">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="authentication"></a><span data-ttu-id="1b49a-119">인증</span><span class="sxs-lookup"><span data-stu-id="1b49a-119">Authentication</span></span>
<span data-ttu-id="1b49a-120">이 문서에서는 간단한 인증 방법이 증명된 tooenter 있는 데이터 레이크 저장소와 Azure 계정 자격 증명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-120">This article uses a simpler authentication approach with Data Lake Store where you are prompted tooenter your Azure account credentials.</span></span> <span data-ttu-id="1b49a-121">hello 액세스 수준 tooData Lake 저장소 계정 및 파일 시스템은 다음 hello 로그인 한 사용자의 hello 액세스 수준을 통해 제어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-121">hello access level tooData Lake Store account and file system is then governed by hello access level of hello logged in user.</span></span> <span data-ttu-id="1b49a-122">그러나 여러 가지 다른 접근 방법이 데이터 레이크 저장소와 잘 tooauthenticate로 요소인 **최종 사용자 인증** 또는 **서비스 간 인증**합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-122">However, there are other approaches as well tooauthenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="1b49a-123">지침 및 방법에 대 한 자세한 내용은 tooauthenticate, 참조 [최종 사용자 인증](data-lake-store-end-user-authenticate-using-active-directory.md) 또는 [서비스 간 인증](data-lake-store-authenticate-using-active-directory.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-123">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="1b49a-124">Azure 데이터 레이크 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="1b49a-124">Create an Azure Data Lake Store account</span></span>
1. <span data-ttu-id="1b49a-125">바탕 화면에서 새 Windows PowerShell 창을 열고 입력 hello 조각 toolog tooyour Azure 계정에에서 따라, hello 구독을 설정 하 고 hello 데이터 레이크 저장소 공급자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-125">From your desktop, open a new Windows PowerShell window, and enter hello following snippet toolog in tooyour Azure account, set hello subscription, and register hello Data Lake Store provider.</span></span> <span data-ttu-id="1b49a-126">, 입력 정보 요청된 toolog 있는지 확인 하는 경우 로그인 할 hello 구독 admininistrators/소유자 중 하나로:</span><span class="sxs-lookup"><span data-stu-id="1b49a-126">When prompted toolog in, make sure you log in as one of hello subscription admininistrators/owner:</span></span>

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. <span data-ttu-id="1b49a-127">Azure 데이터 레이크 저장소 계정은 Azure 리소스 그룹과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-127">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="1b49a-128">Azure 리소스 그룹을 만드는 작업부터 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-128">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="1b49a-129">![Azure 리소스 그룹 만들기](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Azure 리소스 그룹 만들기")</span><span class="sxs-lookup"><span data-stu-id="1b49a-129">![Create an Azure Resource Group](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")</span></span>
3. <span data-ttu-id="1b49a-130">Azure 데이터 레이크 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-130">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="1b49a-131">지정한 hello 이름은 소문자와 숫자만 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-131">hello name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="1b49a-132">![Azure Data Lake Store 계정 만들기](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Azure Data Lake Store 계정 만들기")</span><span class="sxs-lookup"><span data-stu-id="1b49a-132">![Create an Azure Data Lake Store account](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake Store account")</span></span>
4. <span data-ttu-id="1b49a-133">Hello 계정을 성공적으로 만들어졌는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-133">Verify that hello account is successfully created.</span></span>

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    <span data-ttu-id="1b49a-134">이 출력 하는 hello **True**합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-134">hello output for this should be **True**.</span></span>

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a><span data-ttu-id="1b49a-135">Azure 데이터 레이크 저장소에서 디렉터리 구조 만들기</span><span class="sxs-lookup"><span data-stu-id="1b49a-135">Create directory structures in your Azure Data Lake Store</span></span>
<span data-ttu-id="1b49a-136">Azure 데이터 레이크 저장소 계정 toomanage에서 디렉터리를 만들고 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-136">You can create directories under your Azure Data Lake Store account toomanage and store data.</span></span>

1. <span data-ttu-id="1b49a-137">루트 디렉터리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-137">Specify a root directory.</span></span>

        $myrootdir = "/"
2. <span data-ttu-id="1b49a-138">라는 새 디렉터리를 만듭니다 **mynewdirectory** hello 지정된 루트 아래 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-138">Create a new directory called **mynewdirectory** under hello specified root.</span></span>

        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. <span data-ttu-id="1b49a-139">해당 hello 새 디렉터리 성공적으로 만들어지면 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-139">Verify that hello new directory is successfully created.</span></span>

        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir

    <span data-ttu-id="1b49a-140">Hello 다음과 같은 출력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-140">It should show an output like hello following:</span></span>

    <span data-ttu-id="1b49a-141">![디렉터리 확인](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "디렉터리 확인")</span><span class="sxs-lookup"><span data-stu-id="1b49a-141">![Verify Directory](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verify Directory")</span></span>

## <a name="upload-data-tooyour-azure-data-lake-store"></a><span data-ttu-id="1b49a-142">업로드 데이터 tooyour Azure 데이터 레이크 저장소</span><span class="sxs-lookup"><span data-stu-id="1b49a-142">Upload data tooyour Azure Data Lake Store</span></span>
<span data-ttu-id="1b49a-143">Hello 루트 수준 또는 tooa 만든 디렉터리를 hello 계정 내에서 직접 tooData 데이터 레이크 저장소에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-143">You can upload your data tooData Lake Store directly at hello root level or tooa directory that you created within hello account.</span></span> <span data-ttu-id="1b49a-144">아래 hello 조각은 보여 방법을 tooupload 몇 가지 샘플 데이터 toohello 디렉터리 (**mynewdirectory**) hello 이전 섹션에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-144">hello snippets below demonstrate how tooupload some sample data toohello directory (**mynewdirectory**) you created in hello previous section.</span></span>

<span data-ttu-id="1b49a-145">몇 가지 샘플 데이터 tooupload를 찾고 hello를 얻을 수 있습니다 **Ambulance 데이터** hello 폴더 [Azure 데이터 레이크 Git 리포지토리](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData)합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-145">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="1b49a-146">Hello 파일을 다운로드 하 고 C:\sampledata\ 같은 컴퓨터에 로컬 디렉터리에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-146">Download hello file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a><span data-ttu-id="1b49a-147">데이터 레이크 저장소에서 데이터 이름 바꾸기, 다운로드 및 삭제</span><span class="sxs-lookup"><span data-stu-id="1b49a-147">Rename, download, and delete data from your Data Lake Store</span></span>
<span data-ttu-id="1b49a-148">toorename 파일에 다음 명령을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="1b49a-148">toorename a file, use hello following command:</span></span>

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="1b49a-149">toodownload 파일에 다음 명령을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="1b49a-149">toodownload a file, use hello following command:</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

<span data-ttu-id="1b49a-150">toodelete 파일에 다음 명령을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="1b49a-150">toodelete a file, use hello following command:</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="1b49a-151">메시지가 표시 되 면 입력 **Y** toodelete hello 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-151">When prompted, enter **Y** toodelete hello item.</span></span> <span data-ttu-id="1b49a-152">둘 이상의 파일 toodelete를 설정한 경우에 쉼표로 구분 하 여 모든 hello 경로 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-152">If you have more than one file toodelete, you can provide all hello paths separated by comma.</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a><span data-ttu-id="1b49a-153">Azure 데이터 레이크 저장소 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="1b49a-153">Delete your Azure Data Lake Store account</span></span>
<span data-ttu-id="1b49a-154">데이터 레이크 저장소 계정 명령 toodelete 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-154">Use hello following command toodelete your Data Lake Store account.</span></span>

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

<span data-ttu-id="1b49a-155">메시지가 표시 되 면 입력 **Y** toodelete hello 계정.</span><span class="sxs-lookup"><span data-stu-id="1b49a-155">When prompted, enter **Y** toodelete hello account.</span></span>

## <a name="performance-guidance-while-using-powershell"></a><span data-ttu-id="1b49a-156">PowerShell을 사용하는 동안 성능 지침</span><span class="sxs-lookup"><span data-stu-id="1b49a-156">Performance guidance while using PowerShell</span></span>

<span data-ttu-id="1b49a-157">다음 hello 데이터 레이크 저장소와 PowerShell toowork를 사용 하는 동안 hello 최상의 성능이 튜닝된 tooget 일 수 있는 가장 중요 한 설정은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-157">Below are hello most important settings that can be tuned tooget hello best performance while using PowerShell toowork with Data Lake Store:</span></span>

| <span data-ttu-id="1b49a-158">속성</span><span class="sxs-lookup"><span data-stu-id="1b49a-158">Property</span></span>            | <span data-ttu-id="1b49a-159">기본값</span><span class="sxs-lookup"><span data-stu-id="1b49a-159">Default</span></span> | <span data-ttu-id="1b49a-160">설명</span><span class="sxs-lookup"><span data-stu-id="1b49a-160">Description</span></span> |
|---------------------|---------|-------------|
| <span data-ttu-id="1b49a-161">PerFileThreadCount</span><span class="sxs-lookup"><span data-stu-id="1b49a-161">PerFileThreadCount</span></span>  | <span data-ttu-id="1b49a-162">10</span><span class="sxs-lookup"><span data-stu-id="1b49a-162">10</span></span>      | <span data-ttu-id="1b49a-163">이 매개 변수를 업로드 하거나 다운로드 각 파일에 대 한 병렬 스레드의 toochoose hello 수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-163">This parameter enables you toochoose hello number of parallel threads for uploading or downloading each file.</span></span> <span data-ttu-id="1b49a-164">이 숫자 hello 파일당 할당 될 수 있는 최대 스레드를 나타내지 않으며 해당 시나리오에 따라 덜 스레드를 발생할 수 있습니다 (예: 20 스레드에 게 요청 하는 경우에 하나의 스레드 1KB 파일을 업로드 하는 경우 얻을 수 있습니다).</span><span class="sxs-lookup"><span data-stu-id="1b49a-164">This number represents hello max threads that can be allocated per file, but you may get less threads depending on your scenario (e.g. if you are uploading a 1KB file, you will get one thread even if you ask for 20 threads).</span></span>  |
| <span data-ttu-id="1b49a-165">ConcurrentFileCount</span><span class="sxs-lookup"><span data-stu-id="1b49a-165">ConcurrentFileCount</span></span> | <span data-ttu-id="1b49a-166">10</span><span class="sxs-lookup"><span data-stu-id="1b49a-166">10</span></span>      | <span data-ttu-id="1b49a-167">이 매개 변수는 특히 폴더 업로드 또는 다운로드를 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-167">This parameter is specifically for uploading or downloading folders.</span></span> <span data-ttu-id="1b49a-168">이 매개 변수는 hello 업로드 또는 다운로드 될 수 있는 동시 파일 수를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-168">This parameter determines hello number of concurrent files that can be uploaded or downloaded.</span></span> <span data-ttu-id="1b49a-169">이 숫자는 hello 업로드 또는 다운로드 한 번에 수 있는 동시 파일의 최대 수를 나타내지 않으며 적은 동시성 시나리오에 따라 발생할 수 있습니다 (예: 두 개의 파일을 업로드 하는 경우에 게 요청 하는 경우에 두 개의 동시 파일 업로드 얻을 수 있습니다 15 개)입니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-169">This number represents hello maximum number of concurrent files that can be uploaded or downloaded at one time, but you may get less concurrency depending on your scenario (e.g. if you are uploading two files, you will get two concurrent file uploads even if you ask for 15).</span></span> |

<span data-ttu-id="1b49a-170">**예제**</span><span class="sxs-lookup"><span data-stu-id="1b49a-170">**Example**</span></span>

<span data-ttu-id="1b49a-171">이 명령은 파일 및 100 개의 동시 파일 당 20 개의 스레드를 사용 하 여 Azure 데이터 레이크 저장소 toohello 사용자의 로컬 드라이브에서 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-171">This command downloads files from Azure Data Lake Store toohello user's local drive using 20 threads per file and 100 concurrent files.</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

### <a name="how-do-i-determine-hello-value-tooset-for-these-parameters"></a><span data-ttu-id="1b49a-172">이러한 매개 변수에 대해 값 tooset hello를 확인 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="1b49a-172">How do I determine hello value tooset for these parameters?</span></span>

<span data-ttu-id="1b49a-173">다음은 사용할 수 있는 몇 가지 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-173">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="1b49a-174">**1 단계: hello 총 스레드 수를 확인할** -계산 hello 총 스레드 수 toouse 먼저 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-174">**Step 1: Determine hello total thread count** - You should start by calculating hello total thread count toouse.</span></span> <span data-ttu-id="1b49a-175">일반적으로 물리적 코어당 6개의 스레드를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-175">As a general guideline, you should use 6 threads for each physical core.</span></span>

        Total thread count = total physical cores * 6

    <span data-ttu-id="1b49a-176">**예제**</span><span class="sxs-lookup"><span data-stu-id="1b49a-176">**Example**</span></span>

    <span data-ttu-id="1b49a-177">코어 16 개 있는 D14 VM에서 명령 hello PowerShell 실행</span><span class="sxs-lookup"><span data-stu-id="1b49a-177">Assuming you are running hello PowerShell commands from a D14 VM that has 16 cores</span></span>

        Total thread count = 16 cores * 6 = 96 threads


* <span data-ttu-id="1b49a-178">**2 단계: 계산 PerFileThreadCount** -우리의 PerFileThreadCount hello 파일의 hello 크기에 따라 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-178">**Step 2: Calculate PerFileThreadCount**  - We calculate our PerFileThreadCount based on hello size of hello files.</span></span> <span data-ttu-id="1b49a-179">파일의 2.5 g B 보다 작은 경우 없습니다 필요 toochange이 매개이 변수는 hello 기본값 10을 하기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-179">For files smaller than 2.5GB, there is no need toochange this parameter because hello default of 10 is sufficient.</span></span> <span data-ttu-id="1b49a-180">2.5 g B 보다 큰 파일에 대 한 hello 자료에 대 한 첫 번째 2.5 g B hello와 파일 크기에서의 경우 256mb 이상 증가할 때마다 추가 대 한 1 개의 스레드를 추가 하는 대로 10 개 스레드를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-180">For files larger than 2.5GB, you should use 10 threads as hello base for hello first 2.5GB and add 1 thread for each additional 256MB increase in file size.</span></span> <span data-ttu-id="1b49a-181">더 큰 크기의 파일 범위로 폴더를 복사하는 경우 보다 작은 파일 크기로 그룹화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-181">If you are copying a folder with a large range of file sizes, consider grouping them into similar file sizes.</span></span> <span data-ttu-id="1b49a-182">다른 파일 크기를 사용하면 성능이 저하될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-182">Having dissimilar file sizes may cause non-optimal performance.</span></span> <span data-ttu-id="1b49a-183">그렇지 않은 경우 가능한 toogroup 유사한 파일 크기, PerFileThreadCount hello 가장 큰 파일 크기에 따라 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-183">If that's not possible toogroup similar file sizes, you should set PerFileThreadCount based on hello largest file size.</span></span>

        PerFileThreadCount = 10 threads for hello first 2.5GB + 1 thread for each additional 256MB increase in file size

    <span data-ttu-id="1b49a-184">**예제**</span><span class="sxs-lookup"><span data-stu-id="1b49a-184">**Example**</span></span>

    <span data-ttu-id="1b49a-185">1GB too10GB에서 이르는 100 개의 파일을 했 고, 가장 큰 hello로 10GB 파일 hello 다음과 같은 읽어오는 수식에 대 한 크기 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-185">Assuming you have 100 files ranging from 1GB too10GB, we use hello 10GB as hello largest file size for equation, which would read like hello following.</span></span>

        PerFileThreadCount = 10 + ((10GB - 2.5GB) / 256MB) = 40 threads

* <span data-ttu-id="1b49a-186">**3 단계: 계산 ConcurrentFilecount** -수식 뒤 hello를 기반으로 사용 하 여 hello 총 스레드 수 및 PerFileThreadCount toocalculate ConcurrentFileCount 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-186">**Step 3: Calculate ConcurrentFilecount** - Use hello total thread count and PerFileThreadCount toocalculate ConcurrentFileCount based on hello following equation.</span></span>

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    <span data-ttu-id="1b49a-187">**예제**</span><span class="sxs-lookup"><span data-stu-id="1b49a-187">**Example**</span></span>

    <span data-ttu-id="1b49a-188">사용 되 고 여기서 hello 예제 값을 기반으로</span><span class="sxs-lookup"><span data-stu-id="1b49a-188">Based on hello example values we have been using</span></span>

        96 = 40 * ConcurrentFileCount

    <span data-ttu-id="1b49a-189">따라서 **ConcurrentFileCount** 은 **2.4**, 너무 반올림 수 우리는**2**합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-189">So, **ConcurrentFileCount** is **2.4**, which we can round off too**2**.</span></span>

### <a name="further-tuning"></a><span data-ttu-id="1b49a-190">추가 조정</span><span class="sxs-lookup"><span data-stu-id="1b49a-190">Further tuning</span></span>

<span data-ttu-id="1b49a-191">다양 한 파일 크기 toowork와 있기 때문에 사용자의 추가 조정 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-191">You might require further tuning because there is a range of file sizes toowork with.</span></span> <span data-ttu-id="1b49a-192">위의 계산 hello hello 파일의 전체 또는 대부분은 더 큰와 더 가깝기 때문 toohello 10GB 범위 하는 경우에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-192">hello above calculation works well if all or most of hello files are larger and closer toohello 10GB range.</span></span> <span data-ttu-id="1b49a-193">그렇지 않고 작은 파일이 많고 파일 크기가 매우 다양한 경우 PerFileThreadCount를 줄이면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-193">If instead, there are many different files sizes with many files being smaller, then you could reduce PerFileThreadCount.</span></span> <span data-ttu-id="1b49a-194">Hello PerFileThreadCount를 줄여 ConcurrentFileCount 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-194">By reducing hello PerFileThreadCount, we can increase ConcurrentFileCount.</span></span> <span data-ttu-id="1b49a-195">따라서이 파일의 대부분은 hello 5GB 범위에서 더 작은을 활용해 서 가정할 경우 우리는 계산 다시 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-195">So, if we assume that most of our files are smaller in hello 5GB range, we can re-do our calculation:</span></span>

    PerFileThreadCount = 10 + ((5GB - 2.5GB) / 256MB) = 20

<span data-ttu-id="1b49a-196">따라서 **ConcurrentFileCount** 이제 4.8 형식인 96/20으로 반올림 됩니다 너무**4**합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-196">So, **ConcurrentFileCount** will now be 96/20, which is 4.8, rounded off too**4**.</span></span>

<span data-ttu-id="1b49a-197">Hello를 변경 하 여 이러한 설정을 tootune를 계속할 수 **PerFileThreadCount** 파일 크기의 hello 분포에 따라 위와 아래로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-197">You can continue tootune these settings by changing hello **PerFileThreadCount** up and down depending on hello distribution of your file sizes.</span></span>

### <a name="limitation"></a><span data-ttu-id="1b49a-198">제한 사항</span><span class="sxs-lookup"><span data-stu-id="1b49a-198">Limitation</span></span>

* <span data-ttu-id="1b49a-199">**파일의 수를 사용 하면 ConcurrentFileCount 보다 작으면**: 업로드 하려는 파일 hello 수는 hello 보다 작은 경우 **ConcurrentFileCount** 를 계산한 다음 줄여야  **ConcurrentFileCount** toobe 같으면 toohello 파일 수입니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-199">**Number of files is less than ConcurrentFileCount**: If hello number of files you are uploading is smaller than hello **ConcurrentFileCount** that you calculated, then you should reduce **ConcurrentFileCount** toobe equal toohello number of files.</span></span> <span data-ttu-id="1b49a-200">나머지 모든 스레드 tooincrease를 사용할 수 있습니다 **PerFileThreadCount**합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-200">You can use any remaining threads tooincrease **PerFileThreadCount**.</span></span>

* <span data-ttu-id="1b49a-201">**너무 많은 스레드가**: 계산 클러스터 크기를 늘리지 않고도 너무 많은 스레드를 늘려야 하는 경우, 실행 하면 성능이 저하 되 hello 위험이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-201">**Too many threads**: If you increase thread count too much without increasing your cluster size, you run hello risk of degraded performance.</span></span> <span data-ttu-id="1b49a-202">CPU hello에 컨텍스트 전환 하는 경우 경합 문제 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-202">There can be contention issues when context-switching on hello CPU.</span></span>

* <span data-ttu-id="1b49a-203">**부족 하 여 동시성**: hello 동시성은 부족 한 경우 클러스터 너무 작을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-203">**Insufficient concurrency**: If hello concurrency is not sufficient, then your cluster may be too small.</span></span> <span data-ttu-id="1b49a-204">더 많은 동시성 제공 하 여 클러스터의 노드 hello 수를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-204">You can increase hello number of nodes in your cluster which will give you more concurrency.</span></span>

* <span data-ttu-id="1b49a-205">**제한 오류**: 동시성이 너무 높으면 제한 오류가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-205">**Throttling errors**: You may see throttling errors if your concurrency is too high.</span></span> <span data-ttu-id="1b49a-206">제한 오류를 표시 하는 경우 hello 동시성도 감소 하거나 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b49a-206">If you are seeing throttling errors, you should either reduce hello concurrency or contact us.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b49a-207">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1b49a-207">Next steps</span></span>
* [<span data-ttu-id="1b49a-208">데이터 레이크 저장소의 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="1b49a-208">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="1b49a-209">Azure 데이터 레이크 분석에 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="1b49a-209">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="1b49a-210">Azure HDInsight에 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="1b49a-210">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

