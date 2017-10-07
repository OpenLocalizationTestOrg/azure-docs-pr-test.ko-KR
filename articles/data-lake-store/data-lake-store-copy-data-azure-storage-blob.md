---
title: "데이터 레이크 저장소에 Azure 저장소 Blob 데이터로 aaaCopy | Microsoft Docs"
description: "Azure 저장소 Blob tooData 레이크 스토어에서 AdlCopy 도구 toocopy 데이터를 사용 하 여"
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
ms.openlocfilehash: a3d4172eaefe7395cdef2fff72691bd70f642b78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-from-azure-storage-blobs-toodata-lake-store"></a><span data-ttu-id="11ebf-103">Azure 저장소 Blob tooData Lake 저장소에서 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="11ebf-103">Copy data from Azure Storage Blobs tooData Lake Store</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="11ebf-104">DistCp 사용</span><span class="sxs-lookup"><span data-stu-id="11ebf-104">Using DistCp</span></span>](data-lake-store-copy-data-wasb-distcp.md)
> * [<span data-ttu-id="11ebf-105">AdlCopy 사용</span><span class="sxs-lookup"><span data-stu-id="11ebf-105">Using AdlCopy</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
>
>

<span data-ttu-id="11ebf-106">명령줄 도구를 제공 하는 azure 데이터 레이크 저장소 [AdlCopy](http://aka.ms/downloadadlcopy), 원본 hello에서 toocopy 데이터:</span><span class="sxs-lookup"><span data-stu-id="11ebf-106">Azure Data Lake Store provides a command line tool, [AdlCopy](http://aka.ms/downloadadlcopy), toocopy data from hello following sources:</span></span>

* <span data-ttu-id="11ebf-107">Azure 저장소 Blob에서 Data Lake Store로</span><span class="sxs-lookup"><span data-stu-id="11ebf-107">From Azure Storage Blobs into Data Lake Store.</span></span> <span data-ttu-id="11ebf-108">데이터 레이크 저장소 tooAzure 저장소 blob에서 AdlCopy toocopy 데이터를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-108">You cannot use AdlCopy toocopy data from Data Lake Store tooAzure Storage blobs.</span></span>
* <span data-ttu-id="11ebf-109">두 Azure Data Lake Store 계정 간</span><span class="sxs-lookup"><span data-stu-id="11ebf-109">Between two Azure Data Lake Store accounts.</span></span>

<span data-ttu-id="11ebf-110">또한, 두 가지 모드로 hello AdlCopy 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-110">Also, you can use hello AdlCopy tool in two different modes:</span></span>

* <span data-ttu-id="11ebf-111">**독립 실행형**hello 도구 데이터 레이크 저장소 리소스 tooperform hello 작업을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-111">**Standalone**, where hello tool uses Data Lake Store resources tooperform hello task.</span></span>
* <span data-ttu-id="11ebf-112">**Data Lake 분석 계정을 사용 하 여**에서 tooyour Data Lake 분석 계정에 할당 하는 hello 단위가 사용 되는 tooperform hello 복사 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-112">**Using a Data Lake Analytics account**, where hello units assigned tooyour Data Lake Analytics account are used tooperform hello copy operation.</span></span> <span data-ttu-id="11ebf-113">예측 가능한 방식으로 tooperform hello 복사 작업을 볼 때이 옵션 toouse 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-113">You might want toouse this option when you are looking tooperform hello copy tasks in a predictable manner.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11ebf-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="11ebf-114">Prerequisites</span></span>
<span data-ttu-id="11ebf-115">이 문서를 시작 하기 전에 hello 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-115">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="11ebf-116">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="11ebf-116">**An Azure subscription**.</span></span> <span data-ttu-id="11ebf-117">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11ebf-117">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="11ebf-118">**Azure 저장소 Blob** 컨테이너</span><span class="sxs-lookup"><span data-stu-id="11ebf-118">**Azure Storage Blobs** container with some data.</span></span>
* <span data-ttu-id="11ebf-119">**Azure 데이터 레이크 저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="11ebf-119">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="11ebf-120">방법에 대 한 지침은 toocreate 하나, 참조 [Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="11ebf-120">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="11ebf-121">**Azure Data Lake 분석 계정 (선택 사항)** -참조 [Azure Data Lake 분석 시작](../data-lake-analytics/data-lake-analytics-get-started-portal.md) 어떻게 toocreate 데이터 레이크 저장소에 대 한 지침은 계정.</span><span class="sxs-lookup"><span data-stu-id="11ebf-121">**Azure Data Lake Analytics account (optional)** - See [Get started with Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md) for instructions on how toocreate a Data Lake Store account.</span></span>
* <span data-ttu-id="11ebf-122">**AdlCopy 도구**.</span><span class="sxs-lookup"><span data-stu-id="11ebf-122">**AdlCopy tool**.</span></span> <span data-ttu-id="11ebf-123">Hello AdlCopy 도구를 설치 [http://aka.ms/downloadadlcopy](http://aka.ms/downloadadlcopy)합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-123">Install hello AdlCopy tool from [http://aka.ms/downloadadlcopy](http://aka.ms/downloadadlcopy).</span></span>

## <a name="syntax-of-hello-adlcopy-tool"></a><span data-ttu-id="11ebf-124">Hello AdlCopy 도구의 구문</span><span class="sxs-lookup"><span data-stu-id="11ebf-124">Syntax of hello AdlCopy tool</span></span>
<span data-ttu-id="11ebf-125">다음 구문 toowork hello AdlCopy 도구로 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="11ebf-125">Use hello following syntax toowork with hello AdlCopy tool</span></span>

    AdlCopy /Source <Blob or Data Lake Store source> /Dest <Data Lake Store destination> /SourceKey <Key for Blob account> /Account <Data Lake Analytics account> /Unit <Number of Analytics units> /Pattern

<span data-ttu-id="11ebf-126">hello 구문에서 매개 변수 hello은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-126">hello parameters in hello syntax are described below:</span></span>

| <span data-ttu-id="11ebf-127">옵션</span><span class="sxs-lookup"><span data-stu-id="11ebf-127">Option</span></span> | <span data-ttu-id="11ebf-128">설명</span><span class="sxs-lookup"><span data-stu-id="11ebf-128">Description</span></span> |
| --- | --- |
| <span data-ttu-id="11ebf-129">원본</span><span class="sxs-lookup"><span data-stu-id="11ebf-129">Source</span></span> |<span data-ttu-id="11ebf-130">Hello Azure 저장소 blob에 hello 원본 데이터의 hello 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-130">Specifies hello location of hello source data in hello Azure storage blob.</span></span> <span data-ttu-id="11ebf-131">hello 원본은 blob 컨테이너, blob 또는 다른 데이터 레이크 저장소 계정 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-131">hello source can be a blob container, a blob, or another Data Lake Store account.</span></span> |
| <span data-ttu-id="11ebf-132">Dest</span><span class="sxs-lookup"><span data-stu-id="11ebf-132">Dest</span></span> |<span data-ttu-id="11ebf-133">Hello 데이터 레이크 저장소 대상 toocopy를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-133">Specifies hello Data Lake Store destination toocopy to.</span></span> |
| <span data-ttu-id="11ebf-134">SourceKey</span><span class="sxs-lookup"><span data-stu-id="11ebf-134">SourceKey</span></span> |<span data-ttu-id="11ebf-135">Hello Azure 저장소 blob 원본에 대 한 hello 저장소 액세스 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-135">Specifies hello storage access key for hello Azure storage blob source.</span></span> <span data-ttu-id="11ebf-136">이 hello 소스는 blob 컨테이너 또는 blob 하는 경우에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-136">This is required only if hello source is a blob container or a blob.</span></span> |
| <span data-ttu-id="11ebf-137">계정</span><span class="sxs-lookup"><span data-stu-id="11ebf-137">Account</span></span> |<span data-ttu-id="11ebf-138">**옵션**.</span><span class="sxs-lookup"><span data-stu-id="11ebf-138">**Optional**.</span></span> <span data-ttu-id="11ebf-139">Toouse Azure Data Lake 분석 계정 toorun hello 복사 작업을 원하는 경우이 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-139">Use this if you want toouse Azure Data Lake Analytics account toorun hello copy job.</span></span> <span data-ttu-id="11ebf-140">Hello /Account 옵션을 사용 하 여 hello 구문에서 Data Lake 분석 계정 지정 하지 않은 경우 AdlCopy 기본 계정 toorun hello 작업을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-140">If you use hello /Account option in hello syntax but do not specify a Data Lake Analytics account, AdlCopy uses a default account toorun hello job.</span></span> <span data-ttu-id="11ebf-141">또한이 옵션을 사용 하는 경우 추가 해야 hello 원본 (Azure 저장소 Blob) 및 대상 (Azure 데이터 레이크 저장소) 데이터 원본으로 Data Lake 분석 계정에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-141">Also, if you use this option, you must add hello source (Azure Storage Blob) and destination (Azure Data Lake Store) as data sources for your Data Lake Analytics account.</span></span> |
| <span data-ttu-id="11ebf-142">Units</span><span class="sxs-lookup"><span data-stu-id="11ebf-142">Units</span></span> |<span data-ttu-id="11ebf-143">Hello hello 복사 작업에 사용할 데이터 레이크 분석 단위 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-143">Specifies hello number of Data Lake Analytics units that will be used for hello copy job.</span></span> <span data-ttu-id="11ebf-144">이 옵션은 hello를 사용 하는 경우 필수 **/계정** toospecify hello Data Lake 분석 계정 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-144">This option is mandatory if you use hello **/Account** option toospecify hello Data Lake Analytics account.</span></span> |
| <span data-ttu-id="11ebf-145">패턴</span><span class="sxs-lookup"><span data-stu-id="11ebf-145">Pattern</span></span> |<span data-ttu-id="11ebf-146">어떤 blob 또는 파일 toocopy 나타내는 regex 패턴을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-146">Specifies a regex pattern that indicates which blobs or files toocopy.</span></span> <span data-ttu-id="11ebf-147">AdlCopy는 대/소문자 구분 일치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-147">AdlCopy uses case-sensitive matching.</span></span> <span data-ttu-id="11ebf-148">기본 패턴 hello 패턴이 없는 toocopy 모든 항목은 지정 된 경우에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-148">hello default pattern used when no pattern is specified is toocopy all items.</span></span> <span data-ttu-id="11ebf-149">여러 파일 패턴을 지정할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-149">Specifying multiple file patterns is not supported.</span></span> |

## <a name="use-adlcopy-as-standalone-toocopy-data-from-an-azure-storage-blob"></a><span data-ttu-id="11ebf-150">Azure 저장소 blob에서 (독립 실행형)으로 AdlCopy toocopy 데이터 사용</span><span class="sxs-lookup"><span data-stu-id="11ebf-150">Use AdlCopy (as standalone) toocopy data from an Azure Storage blob</span></span>
1. <span data-ttu-id="11ebf-151">명령 프롬프트를 열고 toohello AdlCopy 설치 된 디렉터리를 일반적으로 이동 `%HOMEPATH%\Documents\adlcopy`합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-151">Open a command prompt and navigate toohello directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>
2. <span data-ttu-id="11ebf-152">Hello 소스 컨테이너 tooa 데이터 레이크 저장소에서에서 다음 명령을 toocopy hello 특정 blob을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-152">Run hello following command toocopy a specific blob from hello source container tooa Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    <span data-ttu-id="11ebf-153">예:</span><span class="sxs-lookup"><span data-stu-id="11ebf-153">For example:</span></span>

        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

    >[AZURE.NOTE] <span data-ttu-id="11ebf-154">위의 hello 구문 hello Data Lake 저장소 계정에서 hello 파일 toobe 복사한 tooa 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-154">hello syntax above specifies hello file toobe copied tooa folder in hello Data Lake Store account.</span></span> <span data-ttu-id="11ebf-155">AdlCopy 도구 hello 지정한 폴더 이름이 존재 하지 않는 경우 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-155">AdlCopy tool creates a folder if hello specified folder name does not exist.</span></span>

    <span data-ttu-id="11ebf-156">됩니다 증명된 tooenter hello 자격 증명에 대 한 hello Azure 구독이 있는 데이터 레이크 저장소 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-156">You will be prompted tooenter hello credentials for hello Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="11ebf-157">출력 유사한 toohello 다음을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-157">You will see an output similar toohello following:</span></span>

        Initializing Copy.
        Copy Started.
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.

1. <span data-ttu-id="11ebf-158">또한 다음 명령을 hello를 사용 하 여 하나의 컨테이너 toohello Data Lake 저장소 계정에서 모든 hello blob을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-158">You can also copy all hello blobs from one container toohello Data Lake Store account using hello following command:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/ /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>        

    <span data-ttu-id="11ebf-159">예:</span><span class="sxs-lookup"><span data-stu-id="11ebf-159">For example:</span></span>

        AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

### <a name="performance-considerations"></a><span data-ttu-id="11ebf-160">성능 고려 사항</span><span class="sxs-lookup"><span data-stu-id="11ebf-160">Performance considerations</span></span>

<span data-ttu-id="11ebf-161">Azure Blob 저장소 계정에서 복사 하는 경우 blob 저장소 면 hello에 복사 하는 동안 제한 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-161">If you are copying from an Azure Blob Storage account, you may be throttled during copy on hello blob storage side.</span></span> <span data-ttu-id="11ebf-162">이 복사 작업의 hello 성능이 저하 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-162">This will degrade hello performance of your copy job.</span></span> <span data-ttu-id="11ebf-163">Azure Blob 저장소의 hello 제한에 대 한 더 toolearn 참조에서 Azure 저장소 제한 [Azure 구독 및 서비스 제한](../azure-subscription-service-limits.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-163">toolearn more about hello limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span></span>

## <a name="use-adlcopy-as-standalone-toocopy-data-from-another-data-lake-store-account"></a><span data-ttu-id="11ebf-164">다른 데이터 레이크 저장소 계정에서 독립 실행형) (으로 AdlCopy toocopy 데이터 사용</span><span class="sxs-lookup"><span data-stu-id="11ebf-164">Use AdlCopy (as standalone) toocopy data from another Data Lake Store account</span></span>
<span data-ttu-id="11ebf-165">두 데이터 레이크 저장소 계정 간에 AdlCopy toocopy 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-165">You can also use AdlCopy toocopy data between two Data Lake Store accounts.</span></span>

1. <span data-ttu-id="11ebf-166">명령 프롬프트를 열고 toohello AdlCopy 설치 된 디렉터리를 일반적으로 이동 `%HOMEPATH%\Documents\adlcopy`합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-166">Open a command prompt and navigate toohello directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>
2. <span data-ttu-id="11ebf-167">데이터 레이크 저장소 계정 tooanother 하나에서 다음 명령 toocopy hello 특정 파일을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-167">Run hello following command toocopy a specific file from one Data Lake Store account tooanother.</span></span>

        AdlCopy /Source adl://<source_adls_account>.azuredatalakestore.net/<path_to_file> /dest adl://<dest_adls_account>.azuredatalakestore.net/<path>/

    <span data-ttu-id="11ebf-168">예:</span><span class="sxs-lookup"><span data-stu-id="11ebf-168">For example:</span></span>

        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/909f2b.log /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

   > [!NOTE]
   > <span data-ttu-id="11ebf-169">위의 hello 구문 hello 대상 데이터 레이크 저장소 계정에서 hello 파일 toobe 복사한 tooa 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-169">hello syntax above specifies hello file toobe copied tooa folder in hello destination Data Lake Store account.</span></span> <span data-ttu-id="11ebf-170">AdlCopy 도구 hello 지정한 폴더 이름이 존재 하지 않는 경우 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-170">AdlCopy tool creates a folder if hello specified folder name does not exist.</span></span>
   >
   >

    <span data-ttu-id="11ebf-171">됩니다 증명된 tooenter hello 자격 증명에 대 한 hello Azure 구독이 있는 데이터 레이크 저장소 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-171">You will be prompted tooenter hello credentials for hello Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="11ebf-172">출력 유사한 toohello 다음을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-172">You will see an output similar toohello following:</span></span>

        Initializing Copy.
        Copy Started.|
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.
3. <span data-ttu-id="11ebf-173">hello 다음 명령은 모든 파일 복사 hello 대상 데이터 레이크 저장소 계정에에서 hello 원본 데이터 레이크 저장소 계정 tooa 폴더에 있는 특정 폴더에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-173">hello following command copies all files from a specific folder in hello source Data Lake Store account tooa folder in hello destination Data Lake Store account.</span></span>

        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/ /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

### <a name="performance-considerations"></a><span data-ttu-id="11ebf-174">성능 고려 사항</span><span class="sxs-lookup"><span data-stu-id="11ebf-174">Performance considerations</span></span>

<span data-ttu-id="11ebf-175">AdlCopy를 독립 실행형 도구로 사용할 때는 hello 복사본 공유에서 실행 되, Azure 관리 되는 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-175">When using AdlCopy as a standalone tool, hello copy is run on shared, Azure managed resources.</span></span> <span data-ttu-id="11ebf-176">이 환경에서 발생할 수 있습니다 hello 성능 시스템 부하 및 사용 가능한 리소스에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-176">hello performance you may get in this environment depends on system load and available resources.</span></span> <span data-ttu-id="11ebf-177">이 모드는 임시로 작은 양을 전송하는 데 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-177">This mode is best used for small transfers on an ad hoc basis.</span></span> <span data-ttu-id="11ebf-178">매개 변수는 독립 실행형 도구로 AdlCopy를 사용 하는 경우 튜닝 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-178">No parameters need toobe tuned when using AdlCopy as a standalone tool.</span></span>

## <a name="use-adlcopy-with-data-lake-analytics-account-toocopy-data"></a><span data-ttu-id="11ebf-179">Data Lake 분석 계정) (으로 AdlCopy toocopy 데이터 사용</span><span class="sxs-lookup"><span data-stu-id="11ebf-179">Use AdlCopy (with Data Lake Analytics account) toocopy data</span></span>
<span data-ttu-id="11ebf-180">데이터 레이크 분석을 사용할 수도 있습니다 toorun hello AdlCopy 작업 toocopy 데이터를 Azure 저장소에서에서 blob tooData Lake 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-180">You can also use your Data Lake Analytics account toorun hello AdlCopy job toocopy data from Azure storage blobs tooData Lake Store.</span></span> <span data-ttu-id="11ebf-181">이 옵션을 hello 데이터 toobe 이동 기가바이트 및 단위를 hello 범위 이며 더 나은 및 예측 가능한 성능 처리량을 원하는 경우에 일반적으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-181">You would typically use this option when hello data toobe moved is in hello range of gigabytes and terabytes, and you want better and predictable performance throughput.</span></span>

<span data-ttu-id="11ebf-182">toouse AdlCopy toocopy hello 원본 (Azure 저장소 Blob)는 Azure 저장소 Blob에서 사용 하 여 Data Lake 분석 계정 Data Lake 분석 계정에 대 한 데이터 원본으로 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-182">toouse your Data Lake Analytics account with AdlCopy toocopy from an Azure Storage Blob, hello source (Azure Storage Blob) must be added as a data source for your Data Lake Analytics account.</span></span> <span data-ttu-id="11ebf-183">추가 데이터 소스 tooyour Data Lake 분석 계정을 추가 하는 방법에 지침은 [관리 Data Lake 분석 계정 데이터 원본](../data-lake-analytics/data-lake-analytics-manage-use-portal.md#manage-data-sources)합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-183">For instructions on adding additional data sources tooyour Data Lake Analytics account, see [Manage Data Lake Analytics account data sources](../data-lake-analytics/data-lake-analytics-manage-use-portal.md#manage-data-sources).</span></span>

> [!NOTE]
> <span data-ttu-id="11ebf-184">Data Lake 분석 계정을 사용 하 여 hello 소스로 Azure 데이터 레이크 저장소 계정에서 복사 하는 경우에 Data Lake 분석 계정 hello로 tooassociate hello Data Lake 저장소 계정이 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-184">If you are copying from an Azure Data Lake Store account as hello source using a Data Lake Analytics account, you do not need tooassociate hello Data Lake Store account with hello Data Lake Analytics account.</span></span> <span data-ttu-id="11ebf-185">hello 요구 사항 tooassociate hello 소스 저장소 Data Lake 분석 계정 hello로는 hello 소스에는 Azure 저장소 계정은 경우에입니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-185">hello requirement tooassociate hello source store with hello Data Lake Analytics account is only when hello source is an Azure Storage account.</span></span>
>
>

<span data-ttu-id="11ebf-186">Hello 명령 toocopy Data Lake 분석 계정을 사용 하 여 Azure 저장소 blob tooa Data Lake 저장소 계정에서 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-186">Run hello following command toocopy from an Azure Storage blob tooa Data Lake Store account using Data Lake Analytics account:</span></span>

    AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Account <data_lake_analytics_account> /Unit <number_of_data_lake_analytics_units_to_be_used>

<span data-ttu-id="11ebf-187">예:</span><span class="sxs-lookup"><span data-stu-id="11ebf-187">For example:</span></span>

    AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Account mydatalakeanalyticaccount /Units 2

<span data-ttu-id="11ebf-188">마찬가지로, hello 명령 toocopy Data Lake 분석 계정을 사용 하 여 Azure 저장소 blob tooa Data Lake 저장소 계정에서 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-188">Similarly, run hello following command toocopy from an Azure Storage blob tooa Data Lake Store account using Data Lake Analytics account:</span></span>

    AdlCopy /Source adl://mysourcedatalakestore.azuredatalakestore.net/mynewfolder/ /dest adl://mydestdatastore.azuredatalakestore.net/mynewfolder/ /Account mydatalakeanalyticaccount /Units 2

### <a name="performance-considerations"></a><span data-ttu-id="11ebf-189">성능 고려 사항</span><span class="sxs-lookup"><span data-stu-id="11ebf-189">Performance considerations</span></span>

<span data-ttu-id="11ebf-190">테라바이트 hello 범위에서 데이터를 복사, AdlCopy 사용자의 Azure Data Lake 분석 계정으로 사용 하 여 더 나은 및 예측 가능성이 더욱 뛰어난 성능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-190">When copying data in hello range of terabytes, using AdlCopy with your own Azure Data Lake Analytics account provides better and more predictable performance.</span></span> <span data-ttu-id="11ebf-191">튜닝 해야 하는 hello 매개 변수는 hello 복사 작업에 대 한 Azure 데이터 레이크 분석 단위 toouse hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-191">hello parameter that should be tuned is hello number of Azure Data Lake Analytics Units toouse for hello copy job.</span></span> <span data-ttu-id="11ebf-192">Hello 단위 수를 늘리면 복사 작업의 hello 성능이 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-192">Increasing hello number of units will increase hello performance of your copy job.</span></span> <span data-ttu-id="11ebf-193">복사 된 각 파일 toobe 최대 단위 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-193">Each file toobe copied can use maximum one unit.</span></span> <span data-ttu-id="11ebf-194">복사 될 파일의 hello 수보다 더 많은 단위를 지정 하는 성능을 증가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-194">Specifying more units than hello number of files being copied will not increase performance.</span></span>

## <a name="use-adlcopy-toocopy-data-using-pattern-matching"></a><span data-ttu-id="11ebf-195">패턴 일치를 사용 하 여 AdlCopy toocopy 데이터 사용</span><span class="sxs-lookup"><span data-stu-id="11ebf-195">Use AdlCopy toocopy data using pattern matching</span></span>
<span data-ttu-id="11ebf-196">이 섹션에서는 설명 어떻게 toouse AdlCopy toocopy data from a (아래 예에서 사용 하 여 Azure 저장소 Blob) 패턴 일치를 사용 하 여 tooa 대상 데이터 레이크 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-196">In this section, you learn how toouse AdlCopy toocopy data from a source (in our example below we use Azure Storage Blob) tooa destination Data Lake Store account using pattern matching.</span></span> <span data-ttu-id="11ebf-197">예를 들어 사용할 수 있습니다 hello 단계 toocopy 아래의 모든 파일 hello 원본 blob toohello 대상에서.csv 확장명으로.</span><span class="sxs-lookup"><span data-stu-id="11ebf-197">For example, you can use hello steps below toocopy all files with .csv extension from hello source blob toohello destination.</span></span>

1. <span data-ttu-id="11ebf-198">명령 프롬프트를 열고 toohello AdlCopy 설치 된 디렉터리를 일반적으로 이동 `%HOMEPATH%\Documents\adlcopy`합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-198">Open a command prompt and navigate toohello directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>
2. <span data-ttu-id="11ebf-199">다음 명령은 toocopy hello 모든 파일을 실행 *.csv 확장명으로 hello 소스 컨테이너 tooa 데이터 레이크 저장소에서에서 특정 blob에서:</span><span class="sxs-lookup"><span data-stu-id="11ebf-199">Run hello following command toocopy all files with *.csv extension from a specific blob from hello source container tooa Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Pattern *.csv

    <span data-ttu-id="11ebf-200">예:</span><span class="sxs-lookup"><span data-stu-id="11ebf-200">For example:</span></span>

        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/FoodInspectionData/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Pattern *.csv

## <a name="billing"></a><span data-ttu-id="11ebf-201">결제</span><span class="sxs-lookup"><span data-stu-id="11ebf-201">Billing</span></span>
* <span data-ttu-id="11ebf-202">청구 되는 독립 실행형으로 hello AdlCopy 도구를 사용 하 여 이동 하기 위한 송신 비용에 대 한 데이터를 hello 원본 Azure 저장소 계정에 없는 경우 데이터 레이크 저장소 hello으로 같은 지역을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-202">If you use hello AdlCopy tool as standalone you will be billed for egress costs for moving data, if hello source Azure Storage account is not in hello same region as hello Data Lake Store.</span></span>
* <span data-ttu-id="11ebf-203">데이터 레이크 분석을 hello AdlCopy 도구를 사용 하는 경우 계정, 표준 [요금이 청구 Data Lake 분석](https://azure.microsoft.com/pricing/details/data-lake-analytics/) 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-203">If you use hello AdlCopy tool with your Data Lake Analytics account, standard [Data Lake Analytics billing rates](https://azure.microsoft.com/pricing/details/data-lake-analytics/) will apply.</span></span>

## <a name="considerations-for-using-adlcopy"></a><span data-ttu-id="11ebf-204">AdlCopy 사용에 대한 고려 사항</span><span class="sxs-lookup"><span data-stu-id="11ebf-204">Considerations for using AdlCopy</span></span>
* <span data-ttu-id="11ebf-205">AdlCopy(버전 1.0.5)는 모두 수천 개가 넘는 파일과 폴더가 있는 원본에서 데이터를 복사하는 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-205">AdlCopy (for version 1.0.5), supports copying data from sources that collectively have more than thousands of files and folders.</span></span> <span data-ttu-id="11ebf-206">그러나 크기가 큰 데이터 집합을 복사 하는 문제가 발생 하는 경우 hello 파일/폴더를 여러 하위 폴더에 배포할 수 있고 hello 소스로 hello 경로 toothose 하위 폴더를 대신 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-206">However, if you encounter issues copying a large dataset, you can distribute hello files/folders into different sub-folders and use hello path toothose sub-folders as hello source instead.</span></span>

## <a name="performance-considerations-for-using-adlcopy"></a><span data-ttu-id="11ebf-207">AdlCopy 사용에 대한 성능 고려 사항</span><span class="sxs-lookup"><span data-stu-id="11ebf-207">Performance considerations for using AdlCopy</span></span>

<span data-ttu-id="11ebf-208">AdlCopy는 수천 개의 파일 및 폴더가 포함된 데이터의 복사를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-208">AdlCopy supports copying data containing thousands of files and folders.</span></span> <span data-ttu-id="11ebf-209">그러나 크기가 큰 데이터 집합을 복사 하는 문제가 발생 하는 경우 더 작은 하위 폴더로 hello 파일/폴더를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-209">However, if you encounter issues copying a large dataset, you can distribute hello files/folders into smaller sub-folders.</span></span> <span data-ttu-id="11ebf-210">AdlCopy는 임시 복사본용으로 빌드되었습니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-210">AdlCopy was built for ad hoc copies.</span></span> <span data-ttu-id="11ebf-211">사용을 고려해 야 반복적 toocopy 데이터를 보려고 [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) hello 복사 작업 중심 전체 관리 기능을 제공 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-211">If you are trying toocopy data on a recurring basis, you should consider using [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) that provides full management around hello copy operations.</span></span>

## <a name="release-notes"></a><span data-ttu-id="11ebf-212">릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="11ebf-212">Release notes</span></span>
* <span data-ttu-id="11ebf-213">1.0.13-toohello 데이터를 복사 하는 경우 동일한 Azure 데이터 레이크 저장소 계정에서 여러 adlcopy 명령 각각에 대 한 자격 증명은 더 이상 실행 tooreenter 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-213">1.0.13 - If you are copying data toohello same Azure Data Lake Store account across multiple adlcopy commands, you do not need tooreenter your credentials for each run anymore.</span></span> <span data-ttu-id="11ebf-214">이제 Adlcopy가 여러 번 실행할 때 해당 정보를 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="11ebf-214">Adlcopy will now cache that information across multiple runs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11ebf-215">다음 단계</span><span class="sxs-lookup"><span data-stu-id="11ebf-215">Next steps</span></span>
* [<span data-ttu-id="11ebf-216">데이터 레이크 저장소의 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="11ebf-216">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="11ebf-217">Azure 데이터 레이크 분석에 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="11ebf-217">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="11ebf-218">Azure HDInsight에 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="11ebf-218">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
