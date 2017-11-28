---
title: "PowerShell에서 Mahout HDInsight를 사용하여 추천 생성 - Azure | Microsoft Docs"
description: "Apache Mahout Machine Learning 라이브러리를 사용하여 클라이언트에서 실행 중인 PowerShell에서 HDInsight(Hadoop)로 영화 추천을 생성하는 방법을 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 07b57208-32aa-4e59-900a-6c934fa1b7a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 934de9ca2df48b29ef7a56d5729d59d77875ea7b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-hadoop-in-hdinsight-powershell"></a><span data-ttu-id="afa3e-103">HDInsight(PowerShell)의 Hadoop 및 Apache Mahout을 사용하여 영화 추천 생성</span><span class="sxs-lookup"><span data-stu-id="afa3e-103">Generate movie recommendations by using Apache Mahout with Hadoop in HDInsight (PowerShell)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="afa3e-104">Azure HDInsight에서 [Apache Mahout](http://mahout.apache.org) 기계 학습 라이브러리를 사용하여 영화 추천을 생성하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-104">Learn how to use the [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight to generate movie recommendations.</span></span> <span data-ttu-id="afa3e-105">이 문서의 예제는 Azure PowerShell을 사용하여 Mahout 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-105">The example in this document uses Azure PowerShell to run Mahout jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afa3e-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="afa3e-106">Prerequisites</span></span>

* <span data-ttu-id="afa3e-107">Linux 기반 HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-107">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="afa3e-108">HDInsight 클러스터 만들기에 대한 자세한 내용은 [HDInsight에서 Linux 기반 Hadoop 사용 시작][getstarted]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="afa3e-108">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="afa3e-109">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="afa3e-110">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="afa3e-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="afa3e-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="afa3e-111">Azure PowerShell</span></span>](/powershell/azure/overview)

## <span data-ttu-id="afa3e-112"><a name="recommendations"></a>Azure PowerShell을 사용하여 추천 생성</span><span class="sxs-lookup"><span data-stu-id="afa3e-112"><a name="recommendations"></a>Generate recommendations by using Azure PowerShell</span></span>

> [!WARNING]
> <span data-ttu-id="afa3e-113">이 섹션의 작업은 Azure PowerShell을 사용하여 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-113">The job in this section works by using Azure PowerShell.</span></span> <span data-ttu-id="afa3e-114">Mahout에 제공되는 대부분의 클래스는 현재 Azure PowerShell에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-114">Many of the classes provided with Mahout do not currently work with Azure PowerShell.</span></span> <span data-ttu-id="afa3e-115">Azure PowerShell에서 작동하지 않는 클래스의 목록은 [문제 해결](#troubleshooting) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="afa3e-115">For a list of classes that do not work with Azure PowerShell, see the [Troubleshooting](#troubleshooting) section.</span></span>
>
> <span data-ttu-id="afa3e-116">SSH를 사용하여 HDInsight에 연결하고 클러스터에서 Mahout 예제를 직접 실행하는 예제의 경우 [Mahout 및 HDInsight (SSH)를 사용하여 영화 추천 생성](hdinsight-hadoop-mahout-linux-mac.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="afa3e-116">For an example of using SSH to connect to HDInsight and run Mahout examples directly on the cluster, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

<span data-ttu-id="afa3e-117">Mahout에서 제공하는 기능 중 하나가 추천 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-117">One of the functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="afa3e-118">이 엔진은 `userID`, `itemId` 및 `prefValue`(항목에 대한 사용자 선호도) 형식의 데이터를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-118">This engine accepts data in the format of `userID`, `itemId`, and `prefValue` (the users preference for the item).</span></span> <span data-ttu-id="afa3e-119">Mahout은 데이터를 사용하여 특정 품목에 대한 선호도를 가진 사용자를 결정합니다. 이 결과는 추천에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-119">Mahout uses the data to determine users with like-item preferences, which can be used to make recommendations.</span></span>

<span data-ttu-id="afa3e-120">다음 예제는 추천 프로세스가 작동하는 방식을 간단히 요약한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-120">The following example is a simplified walk-through of how the recommendation process works:</span></span>

* <span data-ttu-id="afa3e-121">**동시 발생**: Joe, Alice 및 Bob은 모두 *스타워즈*, *제국의 역습* 및 *제다이의 귀환*을 좋아합니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-121">**co-occurrence**: Joe, Alice, and Bob all liked *Star Wars*, *The Empire Strikes Back*, and *Return of the Jedi*.</span></span> <span data-ttu-id="afa3e-122">Mahout은 이러한 영화 중 하나를 좋아하면서 다른 두 개도 좋아하는 사용자를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-122">Mahout determines that users who like any one of these movies also like the other two.</span></span>

* <span data-ttu-id="afa3e-123">**동시 발생**: Bob 및 Alice는 *보이지 않는 위협*, *클론의 습격* 및 *시스의 복수*도 좋아합니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-123">**co-occurrence**: Bob and Alice also liked *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span></span> <span data-ttu-id="afa3e-124">Mahout은 이전의 3개 영화를 좋아하는 사용자가 이러한 영화도 좋아하는지를 판단합니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-124">Mahout determines that users who liked the previous three movies also like these movies.</span></span>

* <span data-ttu-id="afa3e-125">**유사성 추천**: Joe가 첫 3개 영화를 좋아하므로, Mahout은 유사한 선호도를 가진 다른 사람이 좋아하지만 Joe는 본(좋아하거나 평가한) 적이 없는 영화를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-125">**Similarity recommendation**: Because Joe liked the first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="afa3e-126">이 경우 Mahout은 *보이지 않는 위협*, *클론의 습격* 및 *시스의 복수*를 추천합니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-126">In this case, Mahout recommends *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span></span>

### <a name="understanding-the-data"></a><span data-ttu-id="afa3e-127">데이터 이해</span><span class="sxs-lookup"><span data-stu-id="afa3e-127">Understanding the data</span></span>

<span data-ttu-id="afa3e-128">[GroupLens Research][movielens]에서 Mahout과 호환되는 형식으로 영화에 대한 평가 데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-128">[GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="afa3e-129">이 데이터는 클러스터의 기본 저장소인 `/HdiSamples//HdiSamples/MahoutMovieData`에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-129">This data is available on the default storage for your cluster at `/HdiSamples//HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="afa3e-130">`moviedb.txt`(영화 정보) 및 `user-ratings.txt`의 두 가지 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-130">There are two files, `moviedb.txt` (information about the movies) and `user-ratings.txt`.</span></span> <span data-ttu-id="afa3e-131">`user-ratings.txt` 파일은 분석 중 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-131">The `user-ratings.txt` file is used during analysis.</span></span> <span data-ttu-id="afa3e-132">`moviedb.txt` 파일은 분석 결과를 표시할 때 사용자에게 친숙한 텍스트를 제공하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-132">The `moviedb.txt` file is used to provide user-friendly text when displaying the results of the analysis.</span></span>

<span data-ttu-id="afa3e-133">user-ratings.txt에 포함된 데이터의 구조는 `userID`, `movieID`, `userRating` 및 `timestamp`이며, 각 사용자의 영화 등급 평가를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-133">The data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="afa3e-134">다음은 데이터의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-134">Here is an example of the data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

### <a name="run-the-job"></a><span data-ttu-id="afa3e-135">작업 실행</span><span class="sxs-lookup"><span data-stu-id="afa3e-135">Run the job</span></span>

<span data-ttu-id="afa3e-136">다음 Windows PowerShell 스크립트를 사용하여 영화 데이터로 Mahout 추천 엔진을 사용하는 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-136">Use the following Windows PowerShell script to run a job that uses the Mahout recommendation engine with the movie data:</span></span>

> [!NOTE]
> <span data-ttu-id="afa3e-137">이 파일은 HDInsight 클러스터에 연결하고 작업을 실행하는 데 사용하는 정보를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-137">This file prompts you for information that is used to connect to your HDInsight cluster and run jobs.</span></span> <span data-ttu-id="afa3e-138">작업을 완료하고 output.txt 파일을 다운로드하는 데 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-138">It may take several minutes for the jobs to complete and download the output.txt file.</span></span>

<span data-ttu-id="afa3e-139">[!code-powershell[기본](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]</span><span class="sxs-lookup"><span data-stu-id="afa3e-139">[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]</span></span>

> [!NOTE]
> <span data-ttu-id="afa3e-140">Mahout 작업은 작업을 처리하는 동안 생성된 임시 데이터를 제거하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-140">Mahout jobs do not remove temporary data that is created while processing the job.</span></span> <span data-ttu-id="afa3e-141">이 `--tempDir` 매개 변수는 쉽게 삭제할 수 있도록 임시 파일을 특정 디렉터리로 분리하기 위해 예제 작업에서 지정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-141">The `--tempDir` parameter is specified in the example job to isolate the temporary files into a specific directory.</span></span>

<span data-ttu-id="afa3e-142">Mahout 작업은 STDOUT로 출력을 반환하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-142">The Mahout job does not return the output to STDOUT.</span></span> <span data-ttu-id="afa3e-143">대신 지정된 출력 디렉터리에 **part-r-00000**으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-143">Instead, it stores it in the specified output directory as **part-r-00000**.</span></span> <span data-ttu-id="afa3e-144">이 스크립트는 이 파일을 워크스테이션의 현재 디렉터리에서 **output.txt** 에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-144">The script downloads this file to **output.txt** in the current directory on your workstation.</span></span>

<span data-ttu-id="afa3e-145">다음 텍스트는 이 파일의 내용에 대한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-145">The following text is an example of the content of this file:</span></span>

    1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
    2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
    3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
    4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

<span data-ttu-id="afa3e-146">첫 번째 열은 `userID`입니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-146">The first column is the `userID`.</span></span> <span data-ttu-id="afa3e-147">'[' 및 ']'에 포함된 값은 `movieId`:`recommendationScore`입니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-147">The values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

<span data-ttu-id="afa3e-148">또한 스크립트는 출력의 가독성을 개선하도록 서식 지정하는 데 필요한 `moviedb.txt` 및 `user-ratings.txt` 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-148">The script also downloads the `moviedb.txt` and `user-ratings.txt` files, which are needed to format the output to be more readable.</span></span>

### <a name="view-the-output"></a><span data-ttu-id="afa3e-149">출력 보기</span><span class="sxs-lookup"><span data-stu-id="afa3e-149">View the output</span></span>

<span data-ttu-id="afa3e-150">생성된 출력을 응용 프로그램에서 사용할 수 있긴 하지만 사용자에게 친숙한 형식은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-150">Although the generated output might be OK for use in an application, it's not user-friendly.</span></span> <span data-ttu-id="afa3e-151">서버의 `moviedb.txt`를 사용하여 영화 이름으로 `movieId`를 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-151">The `moviedb.txt` from the server can be used to resolve the `movieId` to a movie name.</span></span> <span data-ttu-id="afa3e-152">다음 PowerShell 스크립트를 사용하여 영화 이름과 함께 추천 항목을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-152">Use the following PowerShell script to display recommendations with movie names:</span></span>

<span data-ttu-id="afa3e-153">[!code-powershell[기본](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]</span><span class="sxs-lookup"><span data-stu-id="afa3e-153">[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]</span></span>

<span data-ttu-id="afa3e-154">다음 명령을 사용하여 사용자에게 친숙한 형식으로 추천 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-154">Use the following command to display the recommendations in a user-friendly format:</span></span> 

```powershell
.\show-recommendation.ps1 -userId 4 -userDataFile .\user-ratings.txt -movieFile .\moviedb.txt -recommendationFile .\output.txt
```

<span data-ttu-id="afa3e-155">다음 텍스트와 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-155">The output is similar to the following text:</span></span>

    Reading movies descriptions
    Reading rated movies
    Reading recommendations
    Rated movies
    ---------------------------
    Movie                                    Rating
    -----                                    ------
    Devil's Own, The (1997)                  1
    Alien: Resurrection (1997)               3
    187 (1997)                               2
    (lines ommitted)

    ---------------------------
    Recommended movies
    ---------------------------

    Movie                                    Score
    -----                                    -----
    Good Will Hunting (1997)                 4.6504064
    Swingers (1996)                          4.6862745
    Wings of the Dove, The (1997)            4.6666665
    People vs. Larry Flynt, The (1996)       4.834559
    Everyone Says I Love You (1996)          4.707071
    Secrets & Lies (1996)                    4.818182
    That Thing You Do! (1996)                4.75
    Grosse Pointe Blank (1997)               4.8235292
    Donnie Brasco (1997)                     4.6792455
    Lone Star (1996)                         4.7099237

## <span data-ttu-id="afa3e-156"><a name="troubleshooting"></a>문제 해결</span><span class="sxs-lookup"><span data-stu-id="afa3e-156"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="cannot-overwrite-files"></a><span data-ttu-id="afa3e-157">파일을 덮어쓸 수 없음</span><span class="sxs-lookup"><span data-stu-id="afa3e-157">Cannot overwrite files</span></span>

<span data-ttu-id="afa3e-158">Mahout 작업은 처리 중 생성된 임시 파일을 정리하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-158">Mahout jobs do not clean up temporary files that were created during processing.</span></span> <span data-ttu-id="afa3e-159">또한 이 작업은 기존 출력 파일을 덮어쓰지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-159">In addition, the jobs do not overwrite existing output file.</span></span>

<span data-ttu-id="afa3e-160">Mahout 작업을 실행할 때 오류를 방지하려면 실행 사이에 임시 및 출력 파일을 삭제하세요.</span><span class="sxs-lookup"><span data-stu-id="afa3e-160">To avoid errors when running Mahout jobs, delete temporary and output files between runs.</span></span> <span data-ttu-id="afa3e-161">이 문서의 이전 스크립트에서 생성된 파일을 제거하려면 다음 PowerShell 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-161">To remove the files created by the earlier scripts in this document, use the following PowerShell script:</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
$creds=Get-Credential -Message "Enter the login for the cluster"

#Get the cluster info so we can get the resource group, storage, etc.
$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName = $clusterInfo.DefaultStorageAccount.split('.')[0]
$container = $clusterInfo.DefaultStorageContainer
$storageAccountKey = (Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage context and upload the file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

#Azure PowerShell can't delete blobs using wildcard,
#so have to get a list and delete one at a time
# Start with the output
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/out"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
# Next the temp files
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/temp"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
```

### <span data-ttu-id="afa3e-162"><a name="nopowershell"></a>Azure PowerShell에서 작동하지 않는 클래스</span><span class="sxs-lookup"><span data-stu-id="afa3e-162"><a name="nopowershell"></a>Classes that do not work with Azure PowerShell</span></span>

<span data-ttu-id="afa3e-163">Windows PowerShell에서 사용하는 경우 다음 클래스를 사용하는 Mahout 작업은 다양한 오류 메시지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-163">Mahout jobs that use the following classes return various error messages when used from Windows PowerShell:</span></span>

* <span data-ttu-id="afa3e-164">org.apache.mahout.utils.clustering.ClusterDumper</span><span class="sxs-lookup"><span data-stu-id="afa3e-164">org.apache.mahout.utils.clustering.ClusterDumper</span></span>
* <span data-ttu-id="afa3e-165">org.apache.mahout.utils.SequenceFileDumper</span><span class="sxs-lookup"><span data-stu-id="afa3e-165">org.apache.mahout.utils.SequenceFileDumper</span></span>
* <span data-ttu-id="afa3e-166">org.apache.mahout.utils.vectors.lucene.Driver</span><span class="sxs-lookup"><span data-stu-id="afa3e-166">org.apache.mahout.utils.vectors.lucene.Driver</span></span>
* <span data-ttu-id="afa3e-167">org.apache.mahout.utils.vectors.arff.Driver</span><span class="sxs-lookup"><span data-stu-id="afa3e-167">org.apache.mahout.utils.vectors.arff.Driver</span></span>
* <span data-ttu-id="afa3e-168">org.apache.mahout.text.WikipediaToSequenceFile</span><span class="sxs-lookup"><span data-stu-id="afa3e-168">org.apache.mahout.text.WikipediaToSequenceFile</span></span>
* <span data-ttu-id="afa3e-169">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span><span class="sxs-lookup"><span data-stu-id="afa3e-169">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span></span>
* <span data-ttu-id="afa3e-170">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span><span class="sxs-lookup"><span data-stu-id="afa3e-170">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span></span>
* <span data-ttu-id="afa3e-171">org.apache.mahout.classifier.sgd.TrainLogistic</span><span class="sxs-lookup"><span data-stu-id="afa3e-171">org.apache.mahout.classifier.sgd.TrainLogistic</span></span>
* <span data-ttu-id="afa3e-172">org.apache.mahout.classifier.sgd.RunLogistic</span><span class="sxs-lookup"><span data-stu-id="afa3e-172">org.apache.mahout.classifier.sgd.RunLogistic</span></span>
* <span data-ttu-id="afa3e-173">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="afa3e-173">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span></span>
* <span data-ttu-id="afa3e-174">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="afa3e-174">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span></span>
* <span data-ttu-id="afa3e-175">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="afa3e-175">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span></span>
* <span data-ttu-id="afa3e-176">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span><span class="sxs-lookup"><span data-stu-id="afa3e-176">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span></span>
* <span data-ttu-id="afa3e-177">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span><span class="sxs-lookup"><span data-stu-id="afa3e-177">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span></span>
* <span data-ttu-id="afa3e-178">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span><span class="sxs-lookup"><span data-stu-id="afa3e-178">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span></span>
* <span data-ttu-id="afa3e-179">org.apache.mahout.classifier.df.tools.Describe</span><span class="sxs-lookup"><span data-stu-id="afa3e-179">org.apache.mahout.classifier.df.tools.Describe</span></span>

<span data-ttu-id="afa3e-180">이러한 클래스를 사용하는 작업을 실행하려면 SSH를 사용하여 HDInsight 클러스터에 연결하고 명령줄에서 작업을 실행하세요.</span><span class="sxs-lookup"><span data-stu-id="afa3e-180">To run jobs that use these classes, connect to the HDInsight cluster using SSH and run the jobs from the command line.</span></span> <span data-ttu-id="afa3e-181">SSH를 사용하여 Mahout 작업을 실행하는 예제는 [Mahout 및 HDInsight(SSH)를 사용하여 영화 추천 생성](hdinsight-hadoop-mahout-linux-mac.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="afa3e-181">For an example of using SSH to run Mahout jobs, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="afa3e-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="afa3e-182">Next steps</span></span>

<span data-ttu-id="afa3e-183">이제 Mahout을 사용하는 방법을 배웠으므로 HDInsight에서 데이터로 작업하는 다른 방법을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="afa3e-183">Now that you have learned how to use Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="afa3e-184">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="afa3e-184">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="afa3e-185">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="afa3e-185">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="afa3e-186">HDInsight에서 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="afa3e-186">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[build]: http://mahout.apache.org/developers/buildingmahout.html
[aps]: /powershell/azureps-cmdlets-docs
[movielens]: http://grouplens.org/datasets/movielens/
[100k]: http://files.grouplens.org/datasets/movielens/ml-100k.zip
[getstarted]: hdinsight-hadoop-linux-tutorial-get-started.md
[upload]: hdinsight-upload-data.md
[ml]: http://en.wikipedia.org/wiki/Machine_learning
[forest]: http://en.wikipedia.org/wiki/Random_forest
[enableremote]: ./media/hdinsight-mahout/enableremote.png
[connect]: ./media/hdinsight-mahout/connect.png
[hadoopcli]: ./media/hdinsight-mahout/hadoopcli.png
[tools]: https://github.com/Blackmist/hdinsight-tools
