---
title: "Azure Storage Blobs에서 Data Lake Store로 데이터 복사 | Microsoft 문서"
description: "AdlCopy 도구를 사용하여 Azure 저장소 Blob에서 데이터 레이크 저장소로 데이터 복사"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: dc273ef8-96ef-47a6-b831-98e8a777a5c1
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 68f44991432a76c2ef1c79ec6dffdea4c62bcb17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="copy-data-from-azure-storage-blobs-to-data-lake-store"></a><span data-ttu-id="35c0a-103">Azure 저장소 Blob에서 데이터 레이크 저장소로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="35c0a-103">Copy data from Azure Storage Blobs to Data Lake Store</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="35c0a-104">DistCp 사용</span><span class="sxs-lookup"><span data-stu-id="35c0a-104">Using DistCp</span></span>](data-lake-store-copy-data-wasb-distcp.md)
> * [<span data-ttu-id="35c0a-105">AdlCopy 사용</span><span class="sxs-lookup"><span data-stu-id="35c0a-105">Using AdlCopy</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
>
>

<span data-ttu-id="35c0a-106">Azure Data Lake Store는 다음 원본에서 데이터를 복사하는 [AdlCopy](http://aka.ms/downloadadlcopy)라는 명령줄 도구를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-106">Azure Data Lake Store provides a command line tool, [AdlCopy](http://aka.ms/downloadadlcopy), to copy data from the following sources:</span></span>

* <span data-ttu-id="35c0a-107">Azure 저장소 Blob에서 Data Lake Store로</span><span class="sxs-lookup"><span data-stu-id="35c0a-107">From Azure Storage Blobs into Data Lake Store.</span></span> <span data-ttu-id="35c0a-108">데이터 레이크 저장소에서 Azure 저장소 Blob으로 데이터를 복사하는 데 AdlCopy를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-108">You cannot use AdlCopy to copy data from Data Lake Store to Azure Storage blobs.</span></span>
* <span data-ttu-id="35c0a-109">두 Azure Data Lake Store 계정 간</span><span class="sxs-lookup"><span data-stu-id="35c0a-109">Between two Azure Data Lake Store accounts.</span></span>

<span data-ttu-id="35c0a-110">또한 다음 두 가지 방법으로 AdlCopy 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-110">Also, you can use the AdlCopy tool in two different modes:</span></span>

* <span data-ttu-id="35c0a-111">**독립 실행형**, 여기서 도구는 데이터 레이크 저장소 리소스를 사용하여 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-111">**Standalone**, where the tool uses Data Lake Store resources to perform the task.</span></span>
* <span data-ttu-id="35c0a-112">**데이터 레이크 분석 계정 사용**, 여기서 데이터 레이크 분석 계정에 할당된 단위는 복사 작업을 수행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-112">**Using a Data Lake Analytics account**, where the units assigned to your Data Lake Analytics account are used to perform the copy operation.</span></span> <span data-ttu-id="35c0a-113">예측 가능한 방식으로 복사 작업을 수행하려는 경우 이 옵션을 사용 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-113">You might want to use this option when you are looking to perform the copy tasks in a predictable manner.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35c0a-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="35c0a-114">Prerequisites</span></span>
<span data-ttu-id="35c0a-115">이 문서를 시작하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-115">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="35c0a-116">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="35c0a-116">**An Azure subscription**.</span></span> <span data-ttu-id="35c0a-117">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35c0a-117">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="35c0a-118">**Azure 저장소 Blob** 컨테이너</span><span class="sxs-lookup"><span data-stu-id="35c0a-118">**Azure Storage Blobs** container with some data.</span></span>
* <span data-ttu-id="35c0a-119">**Azure 데이터 레이크 저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="35c0a-119">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="35c0a-120">만드는 방법에 대한 지침은 [Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="35c0a-120">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="35c0a-121">**Azure 데이터 레이크 분석 계정(선택 사항)** - 데이터 레이크 저장소 계정을 만드는 방법에 대한 지침은 [Azure 데이터 레이크 분석 시작](../data-lake-analytics/data-lake-analytics-get-started-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35c0a-121">**Azure Data Lake Analytics account (optional)** - See [Get started with Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md) for instructions on how to create a Data Lake Store account.</span></span>
* <span data-ttu-id="35c0a-122">**AdlCopy 도구**.</span><span class="sxs-lookup"><span data-stu-id="35c0a-122">**AdlCopy tool**.</span></span> <span data-ttu-id="35c0a-123">[http://aka.ms/downloadadlcopy](http://aka.ms/downloadadlcopy)에서 AdlCopy 도구를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-123">Install the AdlCopy tool from [http://aka.ms/downloadadlcopy](http://aka.ms/downloadadlcopy).</span></span>

## <a name="syntax-of-the-adlcopy-tool"></a><span data-ttu-id="35c0a-124">AdlCopy 도구 구문</span><span class="sxs-lookup"><span data-stu-id="35c0a-124">Syntax of the AdlCopy tool</span></span>
<span data-ttu-id="35c0a-125">다음 구문에 따라 AdlCopy 도구를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-125">Use the following syntax to work with the AdlCopy tool</span></span>

    AdlCopy /Source <Blob or Data Lake Store source> /Dest <Data Lake Store destination> /SourceKey <Key for Blob account> /Account <Data Lake Analytics account> /Unit <Number of Analytics units> /Pattern

<span data-ttu-id="35c0a-126">이 구문에서 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-126">The parameters in the syntax are described below:</span></span>

| <span data-ttu-id="35c0a-127">옵션</span><span class="sxs-lookup"><span data-stu-id="35c0a-127">Option</span></span> | <span data-ttu-id="35c0a-128">설명</span><span class="sxs-lookup"><span data-stu-id="35c0a-128">Description</span></span> |
| --- | --- |
| <span data-ttu-id="35c0a-129">원본</span><span class="sxs-lookup"><span data-stu-id="35c0a-129">Source</span></span> |<span data-ttu-id="35c0a-130">Azure 저장소 Blob에서 원본 데이터의 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-130">Specifies the location of the source data in the Azure storage blob.</span></span> <span data-ttu-id="35c0a-131">원본은 Blob 컨테이너, Blob 또는 다른 Data Lake Store 계정일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-131">The source can be a blob container, a blob, or another Data Lake Store account.</span></span> |
| <span data-ttu-id="35c0a-132">Dest</span><span class="sxs-lookup"><span data-stu-id="35c0a-132">Dest</span></span> |<span data-ttu-id="35c0a-133">복사할 데이터 레이크 저장소 대상을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-133">Specifies the Data Lake Store destination to copy to.</span></span> |
| <span data-ttu-id="35c0a-134">SourceKey</span><span class="sxs-lookup"><span data-stu-id="35c0a-134">SourceKey</span></span> |<span data-ttu-id="35c0a-135">Azure 저장소 Blob 원본에 대한 저장소 액세스 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-135">Specifies the storage access key for the Azure storage blob source.</span></span> <span data-ttu-id="35c0a-136">원본이 Blob 컨테이너 또는 Blob인 경우에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-136">This is required only if the source is a blob container or a blob.</span></span> |
| <span data-ttu-id="35c0a-137">계정</span><span class="sxs-lookup"><span data-stu-id="35c0a-137">Account</span></span> |<span data-ttu-id="35c0a-138">**옵션**.</span><span class="sxs-lookup"><span data-stu-id="35c0a-138">**Optional**.</span></span> <span data-ttu-id="35c0a-139">복사 작업을 실행하기 위해 Azure 데이터 레이크 분석 계정을 사용하려는 경우 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-139">Use this if you want to use Azure Data Lake Analytics account to run the copy job.</span></span> <span data-ttu-id="35c0a-140">구문에서 /Account 옵션을 사용하지만 데이터 레이크 분석 계정을 지정하지 않으면 AdlCopy는 기본 계정을 사용하여 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-140">If you use the /Account option in the syntax but do not specify a Data Lake Analytics account, AdlCopy uses a default account to run the job.</span></span> <span data-ttu-id="35c0a-141">또한 이 옵션을 사용하는 경우 원본(Azure 저장소 Blob) 및 대상(Azure 데이터 레이크 저장소)을 데이터 레이크 분석 계정에 대한 데이터 원본으로 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-141">Also, if you use this option, you must add the source (Azure Storage Blob) and destination (Azure Data Lake Store) as data sources for your Data Lake Analytics account.</span></span> |
| <span data-ttu-id="35c0a-142">Units</span><span class="sxs-lookup"><span data-stu-id="35c0a-142">Units</span></span> |<span data-ttu-id="35c0a-143">복사 작업에 사용할 데이터 레이크 분석 단위의 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-143">Specifies the number of Data Lake Analytics units that will be used for the copy job.</span></span> <span data-ttu-id="35c0a-144">이 옵션은 **/Account** 옵션을 사용하여 데이터 레이크 분석 계정을 지정하는 경우 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-144">This option is mandatory if you use the **/Account** option to specify the Data Lake Analytics account.</span></span> |
| <span data-ttu-id="35c0a-145">패턴</span><span class="sxs-lookup"><span data-stu-id="35c0a-145">Pattern</span></span> |<span data-ttu-id="35c0a-146">복사할 Blob 또는 파일을 나타내는 regex 패턴을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-146">Specifies a regex pattern that indicates which blobs or files to copy.</span></span> <span data-ttu-id="35c0a-147">AdlCopy는 대/소문자 구분 일치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-147">AdlCopy uses case-sensitive matching.</span></span> <span data-ttu-id="35c0a-148">패턴을 지정하지 않았을 때 사용되는 기본 패턴은 모든 항목을 복사하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-148">The default pattern used when no pattern is specified is to copy all items.</span></span> <span data-ttu-id="35c0a-149">여러 파일 패턴을 지정할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-149">Specifying multiple file patterns is not supported.</span></span> |

## <a name="use-adlcopy-as-standalone-to-copy-data-from-an-azure-storage-blob"></a><span data-ttu-id="35c0a-150">AdlCopy(독립 실행형)를 사용하여 Azure 저장소 Blob에서 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="35c0a-150">Use AdlCopy (as standalone) to copy data from an Azure Storage blob</span></span>
1. <span data-ttu-id="35c0a-151">명령 프롬프트를 열고 AdlCopy가 설치된 디렉터리로 이동합니다(일반적으로 `%HOMEPATH%\Documents\adlcopy`).</span><span class="sxs-lookup"><span data-stu-id="35c0a-151">Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>
2. <span data-ttu-id="35c0a-152">다음 명령을 실행하여 원본 컨테이너에서 데이터 레이크 저장소로 특정 BLOB를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-152">Run the following command to copy a specific blob from the source container to a Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    <span data-ttu-id="35c0a-153">예:</span><span class="sxs-lookup"><span data-stu-id="35c0a-153">For example:</span></span>

        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

    >[AZURE.NOTE] <span data-ttu-id="35c0a-154">위의 구문은 Data Lake Store 계정에서 폴더에 복사될 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-154">The syntax above specifies the file to be copied to a folder in the Data Lake Store account.</span></span> <span data-ttu-id="35c0a-155">지정한 폴더 이름이 존재하지 않는 경우 AdlCopy 도구는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-155">AdlCopy tool creates a folder if the specified folder name does not exist.</span></span>

    <span data-ttu-id="35c0a-156">Data Lake Store 계정이 있는 Azure 구독에 대한 자격 증명을 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-156">You will be prompted to enter the credentials for the Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="35c0a-157">다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-157">You will see an output similar to the following:</span></span>

        Initializing Copy.
        Copy Started.
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.

1. <span data-ttu-id="35c0a-158">다음 명령을 사용하여 한 컨테이너에서 데이터 레이크 저장소 계정으로 모든 BLOB를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-158">You can also copy all the blobs from one container to the Data Lake Store account using the following command:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/ /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>        

    <span data-ttu-id="35c0a-159">예:</span><span class="sxs-lookup"><span data-stu-id="35c0a-159">For example:</span></span>

        AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

### <a name="performance-considerations"></a><span data-ttu-id="35c0a-160">성능 고려 사항</span><span class="sxs-lookup"><span data-stu-id="35c0a-160">Performance considerations</span></span>

<span data-ttu-id="35c0a-161">Azure Blob Storage 계정에서 복사할 경우 Blob Storage 쪽에서 복사하는 동안 제한될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-161">If you are copying from an Azure Blob Storage account, you may be throttled during copy on the blob storage side.</span></span> <span data-ttu-id="35c0a-162">따라서 복사 작업의 성능이 저하됩니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-162">This will degrade the performance of your copy job.</span></span> <span data-ttu-id="35c0a-163">Azure Blob Storage의 제한에 대한 자세한 내용은 [Azure 구독 및 서비스 제한](../azure-subscription-service-limits.md)에서 Azure Storage 제한을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35c0a-163">To learn more about the limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span></span>

## <a name="use-adlcopy-as-standalone-to-copy-data-from-another-data-lake-store-account"></a><span data-ttu-id="35c0a-164">AdlCopy(독립 실행형)를 사용하여 다른 Data Lake Store 계정에서 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="35c0a-164">Use AdlCopy (as standalone) to copy data from another Data Lake Store account</span></span>
<span data-ttu-id="35c0a-165">AdlCopy를 사용하여 두 Data Lake Store 계정 간에 데이터를 복사할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-165">You can also use AdlCopy to copy data between two Data Lake Store accounts.</span></span>

1. <span data-ttu-id="35c0a-166">명령 프롬프트를 열고 AdlCopy가 설치된 디렉터리로 이동합니다(일반적으로 `%HOMEPATH%\Documents\adlcopy`).</span><span class="sxs-lookup"><span data-stu-id="35c0a-166">Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>
2. <span data-ttu-id="35c0a-167">하나의 Data Lake Store 계정에서 다른 계정으로 특정 파일을 복사하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-167">Run the following command to copy a specific file from one Data Lake Store account to another.</span></span>

        AdlCopy /Source adl://<source_adls_account>.azuredatalakestore.net/<path_to_file> /dest adl://<dest_adls_account>.azuredatalakestore.net/<path>/

    <span data-ttu-id="35c0a-168">예:</span><span class="sxs-lookup"><span data-stu-id="35c0a-168">For example:</span></span>

        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/909f2b.log /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

   > [!NOTE]
   > <span data-ttu-id="35c0a-169">위의 구문은 대상 Data Lake Store 계정에서 폴더에 복사될 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-169">The syntax above specifies the file to be copied to a folder in the destination Data Lake Store account.</span></span> <span data-ttu-id="35c0a-170">지정한 폴더 이름이 존재하지 않는 경우 AdlCopy 도구는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-170">AdlCopy tool creates a folder if the specified folder name does not exist.</span></span>
   >
   >

    <span data-ttu-id="35c0a-171">Data Lake Store 계정이 있는 Azure 구독에 대한 자격 증명을 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-171">You will be prompted to enter the credentials for the Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="35c0a-172">다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-172">You will see an output similar to the following:</span></span>

        Initializing Copy.
        Copy Started.|
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.
3. <span data-ttu-id="35c0a-173">다음 명령은 원본 Data Lake Store 계정의 특정 폴더에 있는 모든 파일을 대상 Data Lake Store 계정의 폴더로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-173">The following command copies all files from a specific folder in the source Data Lake Store account to a folder in the destination Data Lake Store account.</span></span>

        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/ /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

### <a name="performance-considerations"></a><span data-ttu-id="35c0a-174">성능 고려 사항</span><span class="sxs-lookup"><span data-stu-id="35c0a-174">Performance considerations</span></span>

<span data-ttu-id="35c0a-175">AdlCopy를 독립 실행형 도구로 사용할 때는 공유된 Azure 관리 리소스에서 복사본이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-175">When using AdlCopy as a standalone tool, the copy is run on shared, Azure managed resources.</span></span> <span data-ttu-id="35c0a-176">이 환경에서의 성능은 시스템 부하 및 사용 가능한 리소스에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-176">The performance you may get in this environment depends on system load and available resources.</span></span> <span data-ttu-id="35c0a-177">이 모드는 임시로 작은 양을 전송하는 데 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-177">This mode is best used for small transfers on an ad hoc basis.</span></span> <span data-ttu-id="35c0a-178">AdlCopy를 독립 실행형 도구로 사용하는 경우 매개 변수를 조정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-178">No parameters need to be tuned when using AdlCopy as a standalone tool.</span></span>

## <a name="use-adlcopy-with-data-lake-analytics-account-to-copy-data"></a><span data-ttu-id="35c0a-179">Data Lake Analytics 계정에 AdlCopy를 사용하여 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="35c0a-179">Use AdlCopy (with Data Lake Analytics account) to copy data</span></span>
<span data-ttu-id="35c0a-180">또한 데이터 레이크 분석 계정을 사용하여 Azure 저장소 Blob에서 데이터 레이크 저장소로 데이터 복사하는 AdlCopy 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-180">You can also use your Data Lake Analytics account to run the AdlCopy job to copy data from Azure storage blobs to Data Lake Store.</span></span> <span data-ttu-id="35c0a-181">이동할 데이터가 기가바이트 및 테라바이트 범위에 있고 보다 향상되고 예측 가능한 성능 처리량을 원하는 경우 일반적으로 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-181">You would typically use this option when the data to be moved is in the range of gigabytes and terabytes, and you want better and predictable performance throughput.</span></span>

<span data-ttu-id="35c0a-182">AdlCopy와 함께 Data Lake Analytics 계정을 사용하여 Azure 저장소 Blob에서 복사하려면 원본(Azure 저장소 Blob)을 Data Lake Analytics 계정의 데이터 원본으로 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-182">To use your Data Lake Analytics account with AdlCopy to copy from an Azure Storage Blob, the source (Azure Storage Blob) must be added as a data source for your Data Lake Analytics account.</span></span> <span data-ttu-id="35c0a-183">Data Lake Aanlytics 계정에 추가 데이터 원본을 추가하는 방법에 대한 지침은 [Data Lake Aanlytics 계정 데이터 원본 관리](../data-lake-analytics/data-lake-analytics-manage-use-portal.md#manage-data-sources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35c0a-183">For instructions on adding additional data sources to your Data Lake Analytics account, see [Manage Data Lake Analytics account data sources](../data-lake-analytics/data-lake-analytics-manage-use-portal.md#manage-data-sources).</span></span>

> [!NOTE]
> <span data-ttu-id="35c0a-184">Data Lake Analytics 계정을 사용하여 Azure Data Lake Store 계정을 원본으로 데이터를 복사하는 경우 Data Lake Store 계정을 Data Lake Analytics 계정에 연결할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-184">If you are copying from an Azure Data Lake Store account as the source using a Data Lake Analytics account, you do not need to associate the Data Lake Store account with the Data Lake Analytics account.</span></span> <span data-ttu-id="35c0a-185">원본 저장소를 Data Lake Analytics 계정에 연결하려는 경우 원본이 Azure 저장소 계정이기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-185">The requirement to associate the source store with the Data Lake Analytics account is only when the source is an Azure Storage account.</span></span>
>
>

<span data-ttu-id="35c0a-186">Data Lake Analytics 계정을 사용하여 Azure 저장소 Blob에서 Data Lake Store 계정으로 복사하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-186">Run the following command to copy from an Azure Storage blob to a Data Lake Store account using Data Lake Analytics account:</span></span>

    AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Account <data_lake_analytics_account> /Unit <number_of_data_lake_analytics_units_to_be_used>

<span data-ttu-id="35c0a-187">예:</span><span class="sxs-lookup"><span data-stu-id="35c0a-187">For example:</span></span>

    AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Account mydatalakeanalyticaccount /Units 2

<span data-ttu-id="35c0a-188">마찬가지로 Data Lake Analytics 계정을 사용하여 Azure 저장소 Blob에서 Data Lake Store 계정으로 복사하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-188">Similarly, run the following command to copy from an Azure Storage blob to a Data Lake Store account using Data Lake Analytics account:</span></span>

    AdlCopy /Source adl://mysourcedatalakestore.azuredatalakestore.net/mynewfolder/ /dest adl://mydestdatastore.azuredatalakestore.net/mynewfolder/ /Account mydatalakeanalyticaccount /Units 2

### <a name="performance-considerations"></a><span data-ttu-id="35c0a-189">성능 고려 사항</span><span class="sxs-lookup"><span data-stu-id="35c0a-189">Performance considerations</span></span>

<span data-ttu-id="35c0a-190">테라바이트 범위의 데이터를 복사할 때 사용자 고유의 Azure Data Lake Analytics 계정으로 AdlCopy를 사용하면 보다 예측 가능하고 더욱 뛰어난 성능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-190">When copying data in the range of terabytes, using AdlCopy with your own Azure Data Lake Analytics account provides better and more predictable performance.</span></span> <span data-ttu-id="35c0a-191">조정해야 할 매개 변수는 복사 작업에 사용할 Azure Data Lake Analytics 단위의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-191">The parameter that should be tuned is the number of Azure Data Lake Analytics Units to use for the copy job.</span></span> <span data-ttu-id="35c0a-192">단위 수를 늘리면 복사 작업의 성능이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-192">Increasing the number of units will increase the performance of your copy job.</span></span> <span data-ttu-id="35c0a-193">복사할 각 파일은 최대 하나의 단위를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-193">Each file to be copied can use maximum one unit.</span></span> <span data-ttu-id="35c0a-194">복사할 파일 수보다 더 많은 단위를 지정한다고 성능이 증가되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-194">Specifying more units than the number of files being copied will not increase performance.</span></span>

## <a name="use-adlcopy-to-copy-data-using-pattern-matching"></a><span data-ttu-id="35c0a-195">AdlCopy를 사용하여 패턴 일치를 통해 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="35c0a-195">Use AdlCopy to copy data using pattern matching</span></span>
<span data-ttu-id="35c0a-196">이 섹션에서는 AdlCopy를 사용하여 패턴 일치를 통해 원본(아래 예제에서는 Azure 저장소 Blob)의 데이터를 대상 Data Lake Store 계정으로 복사하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-196">In this section, you learn how to use AdlCopy to copy data from a source (in our example below we use Azure Storage Blob) to a destination Data Lake Store account using pattern matching.</span></span> <span data-ttu-id="35c0a-197">예를 들어 아래 단계를 사용하여 원본 Blob에서 확장명이 .csv인 모든 파일을 대상으로 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-197">For example, you can use the steps below to copy all files with .csv extension from the source blob to the destination.</span></span>

1. <span data-ttu-id="35c0a-198">명령 프롬프트를 열고 AdlCopy가 설치된 디렉터리로 이동합니다(일반적으로 `%HOMEPATH%\Documents\adlcopy`).</span><span class="sxs-lookup"><span data-stu-id="35c0a-198">Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>
2. <span data-ttu-id="35c0a-199">다음 명령을 실행하여 원본 컨테이너의 특정 Blob 중에서 확장명이 *.csv인 모든 파일을 Data Lake Store로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-199">Run the following command to copy all files with *.csv extension from a specific blob from the source container to a Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Pattern *.csv

    <span data-ttu-id="35c0a-200">예:</span><span class="sxs-lookup"><span data-stu-id="35c0a-200">For example:</span></span>

        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/FoodInspectionData/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Pattern *.csv

## <a name="billing"></a><span data-ttu-id="35c0a-201">결제</span><span class="sxs-lookup"><span data-stu-id="35c0a-201">Billing</span></span>
* <span data-ttu-id="35c0a-202">AdlCopy 도구를 독립 실행형으로 사용하는 경우 원본 Azure 저장소 계정이 데이터 레이크 저장소와 동일한 지역에 없는 경우 데이터 이동에 따른 송신 비용이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-202">If you use the AdlCopy tool as standalone you will be billed for egress costs for moving data, if the source Azure Storage account is not in the same region as the Data Lake Store.</span></span>
* <span data-ttu-id="35c0a-203">데이터 레이크 분석 계정과 함께 AdlCopy 도구를 사용하면 표준 [데이터 레이크 분석 청구 금액](https://azure.microsoft.com/pricing/details/data-lake-analytics/) 이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-203">If you use the AdlCopy tool with your Data Lake Analytics account, standard [Data Lake Analytics billing rates](https://azure.microsoft.com/pricing/details/data-lake-analytics/) will apply.</span></span>

## <a name="considerations-for-using-adlcopy"></a><span data-ttu-id="35c0a-204">AdlCopy 사용에 대한 고려 사항</span><span class="sxs-lookup"><span data-stu-id="35c0a-204">Considerations for using AdlCopy</span></span>
* <span data-ttu-id="35c0a-205">AdlCopy(버전 1.0.5)는 모두 수천 개가 넘는 파일과 폴더가 있는 원본에서 데이터를 복사하는 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-205">AdlCopy (for version 1.0.5), supports copying data from sources that collectively have more than thousands of files and folders.</span></span> <span data-ttu-id="35c0a-206">그러나 대량의 데이터 집합을 복사할 때 문제가 발생할 경우, 파일/폴더를 다른 하위 폴더에 배포하고 해당 하위 폴더에 대한 경로를 원본으로 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-206">However, if you encounter issues copying a large dataset, you can distribute the files/folders into different sub-folders and use the path to those sub-folders as the source instead.</span></span>

## <a name="performance-considerations-for-using-adlcopy"></a><span data-ttu-id="35c0a-207">AdlCopy 사용에 대한 성능 고려 사항</span><span class="sxs-lookup"><span data-stu-id="35c0a-207">Performance considerations for using AdlCopy</span></span>

<span data-ttu-id="35c0a-208">AdlCopy는 수천 개의 파일 및 폴더가 포함된 데이터의 복사를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-208">AdlCopy supports copying data containing thousands of files and folders.</span></span> <span data-ttu-id="35c0a-209">그러나 대량의 데이터 집합을 복사할 때 문제가 발생할 경우 파일/폴더를 더 작은 하위 폴더에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-209">However, if you encounter issues copying a large dataset, you can distribute the files/folders into smaller sub-folders.</span></span> <span data-ttu-id="35c0a-210">AdlCopy는 임시 복사본용으로 빌드되었습니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-210">AdlCopy was built for ad hoc copies.</span></span> <span data-ttu-id="35c0a-211">반복적으로 데이터를 복사하려는 경우 복사 작업 관련 전체 관리 기능을 제공하는 [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) 사용을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-211">If you are trying to copy data on a recurring basis, you should consider using [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) that provides full management around the copy operations.</span></span>

## <a name="release-notes"></a><span data-ttu-id="35c0a-212">릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="35c0a-212">Release notes</span></span>
* <span data-ttu-id="35c0a-213">1.0.13 - 여러 adlcopy 명령을 통해 데이터를 동일한 Azure Data Lake Store 계정에 복사하는 경우 실행할 때마다 자격 증명을 다시 입력할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-213">1.0.13 - If you are copying data to the same Azure Data Lake Store account across multiple adlcopy commands, you do not need to reenter your credentials for each run anymore.</span></span> <span data-ttu-id="35c0a-214">이제 Adlcopy가 여러 번 실행할 때 해당 정보를 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="35c0a-214">Adlcopy will now cache that information across multiple runs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35c0a-215">다음 단계</span><span class="sxs-lookup"><span data-stu-id="35c0a-215">Next steps</span></span>
* [<span data-ttu-id="35c0a-216">데이터 레이크 저장소의 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="35c0a-216">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="35c0a-217">Azure 데이터 레이크 분석에 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="35c0a-217">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="35c0a-218">Azure HDInsight에 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="35c0a-218">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
