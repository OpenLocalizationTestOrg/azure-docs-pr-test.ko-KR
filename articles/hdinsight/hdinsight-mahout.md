---
title: "Mahout HDInsight PowerShell-Azure에서에서 사용 하 여 aaaGenerate 권장 사항 | Microsoft Docs"
description: "Toouse HDInsight (Hadoop)로 toogenerate 영화 권장 구성을 라이브러리 클라이언트에서 실행 되는 PowerShell 스크립트에서 학습 하는 Apache Mahout 컴퓨터 hello 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 675a2cd8ecaf7fc797d6cd094e4e58f9aca7ed92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-hadoop-in-hdinsight-powershell"></a><span data-ttu-id="9854b-103">HDInsight(PowerShell)의 Hadoop 및 Apache Mahout을 사용하여 영화 추천 생성</span><span class="sxs-lookup"><span data-stu-id="9854b-103">Generate movie recommendations by using Apache Mahout with Hadoop in HDInsight (PowerShell)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="9854b-104">자세한 내용은 방법 toouse hello [Apache Mahout](http://mahout.apache.org) Azure HDInsight toogenerate 영화 권장 사항이 포함 된 시스템 학습 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-104">Learn how toouse hello [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight toogenerate movie recommendations.</span></span> <span data-ttu-id="9854b-105">이 문서에 hello 예제는 Azure PowerShell toorun Mahout 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-105">hello example in this document uses Azure PowerShell toorun Mahout jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9854b-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9854b-106">Prerequisites</span></span>

* <span data-ttu-id="9854b-107">Linux 기반 HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-107">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="9854b-108">HDInsight 클러스터 만들기에 대한 자세한 내용은 [HDInsight에서 Linux 기반 Hadoop 사용 시작][getstarted]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9854b-108">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9854b-109">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9854b-110">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9854b-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="9854b-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9854b-111">Azure PowerShell</span></span>](/powershell/azure/overview)

## <span data-ttu-id="9854b-112"><a name="recommendations"></a>Azure PowerShell을 사용하여 추천 생성</span><span class="sxs-lookup"><span data-stu-id="9854b-112"><a name="recommendations"></a>Generate recommendations by using Azure PowerShell</span></span>

> [!WARNING]
> <span data-ttu-id="9854b-113">이 섹션의 작업 hello Azure PowerShell을 사용 하 여 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-113">hello job in this section works by using Azure PowerShell.</span></span> <span data-ttu-id="9854b-114">많은 Mahout와 함께 제공 되는 hello 클래스의 작동 하지 않습니다 현재 Azure PowerShell을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-114">Many of hello classes provided with Mahout do not currently work with Azure PowerShell.</span></span> <span data-ttu-id="9854b-115">목록이 Azure PowerShell과 함께 작동 하지 않는 클래스에 대 한 참조 hello [문제 해결](#troubleshooting) 섹션.</span><span class="sxs-lookup"><span data-stu-id="9854b-115">For a list of classes that do not work with Azure PowerShell, see hello [Troubleshooting](#troubleshooting) section.</span></span>
>
> <span data-ttu-id="9854b-116">SSH tooconnect tooHDInsight 및 실행된 Mahout 예제를 사용 하 여 hello 클러스터에서 직접의 예제를 보려면 [Mahout 및 HDInsight SSH () 사용 하 여 영화 권장 구성 생성](hdinsight-hadoop-mahout-linux-mac.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-116">For an example of using SSH tooconnect tooHDInsight and run Mahout examples directly on hello cluster, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

<span data-ttu-id="9854b-117">Mahout에서 제공 하는 hello 함수 중 하나에 추천 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-117">One of hello functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="9854b-118">이 엔진 hello 형식의의 데이터를 수용 `userID`, `itemId`, 및 `prefValue` (hello hello 항목에 대 한 사용자 기본 설정).</span><span class="sxs-lookup"><span data-stu-id="9854b-118">This engine accepts data in hello format of `userID`, `itemId`, and `prefValue` (hello users preference for hello item).</span></span> <span data-ttu-id="9854b-119">Mahout은 hello 데이터 toodetermine 사용자 사용된 toomake 권장 될 수 있는 유사한 항목 기본 설정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-119">Mahout uses hello data toodetermine users with like-item preferences, which can be used toomake recommendations.</span></span>

<span data-ttu-id="9854b-120">hello 다음 예제는 hello 권장 프로세스의 작동 방식을 단순화 연습:</span><span class="sxs-lookup"><span data-stu-id="9854b-120">hello following example is a simplified walk-through of how hello recommendation process works:</span></span>

* <span data-ttu-id="9854b-121">**동시 발생**: Joe, Alice와 Bob 모든 좋아하는 *별 전쟁*, *제국 공격 다시 hello*, 및 *hello 제다이 반환*합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-121">**co-occurrence**: Joe, Alice, and Bob all liked *Star Wars*, *hello Empire Strikes Back*, and *Return of hello Jedi*.</span></span> <span data-ttu-id="9854b-122">Mahout은 사용자도 이러한 동영상 같은 다른 두 hello 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-122">Mahout determines that users who like any one of these movies also like hello other two.</span></span>

* <span data-ttu-id="9854b-123">**동시 발생**: Alice와 Bob도 빴 *Phantom의 위협 hello*, *hello 복제본의 공격*, 및 *Sith hello의 복수*합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-123">**co-occurrence**: Bob and Alice also liked *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span> <span data-ttu-id="9854b-124">Mahout은 hello 이전 세 영화도 좋아 한 사용자가 이러한 동영상 등 차단 하는 것을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-124">Mahout determines that users who liked hello previous three movies also like these movies.</span></span>

* <span data-ttu-id="9854b-125">**유사성 권장**: 때문에 Joe 처음 세 개의 영화 hello 빴, Mahout 영화에서 마음 비슷한 기본 설정과 다른 보이지만 Joe에 (빴/등급) 조사 하지 합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-125">**Similarity recommendation**: Because Joe liked hello first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="9854b-126">Mahout 권장 하는 경우에 *Phantom의 위협 hello*, *hello 복제본의 공격*, 및 *Sith hello의 복수*합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-126">In this case, Mahout recommends *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span>

### <a name="understanding-hello-data"></a><span data-ttu-id="9854b-127">Hello 데이터 이해</span><span class="sxs-lookup"><span data-stu-id="9854b-127">Understanding hello data</span></span>

<span data-ttu-id="9854b-128">[GroupLens Research][movielens]에서 Mahout과 호환되는 형식으로 영화에 대한 평가 데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-128">[GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="9854b-129">클러스터에 대 한 hello 기본 저장소에서이 데이터를 사용할 `/HdiSamples//HdiSamples/MahoutMovieData`합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-129">This data is available on hello default storage for your cluster at `/HdiSamples//HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="9854b-130">두 개의 파일이 `moviedb.txt` (hello 영화에 대 한 정보) 및 `user-ratings.txt`합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-130">There are two files, `moviedb.txt` (information about hello movies) and `user-ratings.txt`.</span></span> <span data-ttu-id="9854b-131">hello `user-ratings.txt` 분석 하는 동안 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-131">hello `user-ratings.txt` file is used during analysis.</span></span> <span data-ttu-id="9854b-132">hello `moviedb.txt` 파일은 사용 되는 tooprovide 알기 쉬운 텍스트 hello hello 분석 결과 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-132">hello `moviedb.txt` file is used tooprovide user-friendly text when displaying hello results of hello analysis.</span></span>

<span data-ttu-id="9854b-133">hello 사용자 ratings.txt에 포함 된 데이터의 구조는의 `userID`, `movieID`, `userRating`, 및 `timestamp`, 각 사용자 등급 동영상을 지정 하는 방식을 높은 우리 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-133">hello data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="9854b-134">Hello 데이터의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-134">Here is an example of hello data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

### <a name="run-hello-job"></a><span data-ttu-id="9854b-135">Hello 작업 실행</span><span class="sxs-lookup"><span data-stu-id="9854b-135">Run hello job</span></span>

<span data-ttu-id="9854b-136">Windows PowerShell 스크립트 toorun hello 영화 데이터로 hello Mahout 추천 엔진을 사용 하는 작업을 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-136">Use hello following Windows PowerShell script toorun a job that uses hello Mahout recommendation engine with hello movie data:</span></span>

> [!NOTE]
> <span data-ttu-id="9854b-137">이 파일에 대 한 정보를 사용 하는 tooconnect tooyour HDInsight 클러스터와 실행된 작업 메시지 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-137">This file prompts you for information that is used tooconnect tooyour HDInsight cluster and run jobs.</span></span> <span data-ttu-id="9854b-138">작업 toocomplete hello에 대 일 분 정도 걸릴 하 고 hello output.txt 라는 파일을 다운로드 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-138">It may take several minutes for hello jobs toocomplete and download hello output.txt file.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]

> [!NOTE]
> <span data-ttu-id="9854b-139">Mahout 작업 hello 작업을 처리 하는 동안 만든 임시 데이터를 제거 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-139">Mahout jobs do not remove temporary data that is created while processing hello job.</span></span> <span data-ttu-id="9854b-140">hello `--tempDir` 매개 변수는 특정 디렉터리로 hello 예제 작업 tooisolate hello 임시 파일에 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-140">hello `--tempDir` parameter is specified in hello example job tooisolate hello temporary files into a specific directory.</span></span>

<span data-ttu-id="9854b-141">hello Mahout 작업 hello 출력 tooSTDOUT 반환 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-141">hello Mahout job does not return hello output tooSTDOUT.</span></span> <span data-ttu-id="9854b-142">대신 저장 hello 지정한 출력 디렉터리에 **파트-r-00000**합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-142">Instead, it stores it in hello specified output directory as **part-r-00000**.</span></span> <span data-ttu-id="9854b-143">hello 스크립트이 파일 다운로드 하 여이 너무**output.txt 라는** hello 워크스테이션에서 현재 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-143">hello script downloads this file too**output.txt** in hello current directory on your workstation.</span></span>

<span data-ttu-id="9854b-144">hello 다음 텍스트는이 파일의 hello 콘텐츠의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-144">hello following text is an example of hello content of this file:</span></span>

    1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
    2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
    3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
    4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

<span data-ttu-id="9854b-145">hello 첫 번째 열은 hello `userID`합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-145">hello first column is hello `userID`.</span></span> <span data-ttu-id="9854b-146">hello에 포함 된 값 ' [' 및 ']'은 `movieId`:`recommendationScore`합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-146">hello values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

<span data-ttu-id="9854b-147">hello 스크립트 다운로드 hello `moviedb.txt` 및 `user-ratings.txt` 필요한 tooformat hello 출력 toobe 더 쉽게 읽을 수 있는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-147">hello script also downloads hello `moviedb.txt` and `user-ratings.txt` files, which are needed tooformat hello output toobe more readable.</span></span>

### <a name="view-hello-output"></a><span data-ttu-id="9854b-148">Hello 출력 보기</span><span class="sxs-lookup"><span data-stu-id="9854b-148">View hello output</span></span>

<span data-ttu-id="9854b-149">Hello 생성 된 출력 수는 있지만 확인 응용 프로그램에서 사용 하기 위해, 사용자에 게 친숙있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-149">Although hello generated output might be OK for use in an application, it's not user-friendly.</span></span> <span data-ttu-id="9854b-150">hello `moviedb.txt` 서버 hello에서 사용 되는 tooresolve hello 될 수 있습니다 `movieId` tooa 영화 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-150">hello `moviedb.txt` from hello server can be used tooresolve hello `movieId` tooa movie name.</span></span> <span data-ttu-id="9854b-151">영화 이름의 PowerShell 스크립트 toodisplay 권장 사항을 따르면 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-151">Use hello following PowerShell script toodisplay recommendations with movie names:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]

<span data-ttu-id="9854b-152">사용자에 게 친숙 한 형태로 표시 명령 toodisplay hello 권장 사항을 따르면 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-152">Use hello following command toodisplay hello recommendations in a user-friendly format:</span></span> 

```powershell
.\show-recommendation.ps1 -userId 4 -userDataFile .\user-ratings.txt -movieFile .\moviedb.txt -recommendationFile .\output.txt
```

<span data-ttu-id="9854b-153">hello는 텍스트 다음 비슷한 toohello 출력:</span><span class="sxs-lookup"><span data-stu-id="9854b-153">hello output is similar toohello following text:</span></span>

    Reading movies descriptions
    Reading rated movies
    Reading recommendations
    Rated movies
    ---------------------------
    Movie                                    Rating
    -----                                    ------
    Devil's Own, hello (1997)                  1
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
    Wings of hello Dove, hello (1997)            4.6666665
    People vs. Larry Flynt, hello (1996)       4.834559
    Everyone Says I Love You (1996)          4.707071
    Secrets & Lies (1996)                    4.818182
    That Thing You Do! (1996)                4.75
    Grosse Pointe Blank (1997)               4.8235292
    Donnie Brasco (1997)                     4.6792455
    Lone Star (1996)                         4.7099237

## <span data-ttu-id="9854b-154"><a name="troubleshooting"></a>문제 해결</span><span class="sxs-lookup"><span data-stu-id="9854b-154"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="cannot-overwrite-files"></a><span data-ttu-id="9854b-155">파일을 덮어쓸 수 없음</span><span class="sxs-lookup"><span data-stu-id="9854b-155">Cannot overwrite files</span></span>

<span data-ttu-id="9854b-156">Mahout 작업은 처리 중 생성된 임시 파일을 정리하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-156">Mahout jobs do not clean up temporary files that were created during processing.</span></span> <span data-ttu-id="9854b-157">또한 hello 작업은 기존 출력 파일을 덮어쓰지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-157">In addition, hello jobs do not overwrite existing output file.</span></span>

<span data-ttu-id="9854b-158">tooavoid 오류 Mahout 작업을 실행할 때 실행 간에 임시 및 출력 파일을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-158">tooavoid errors when running Mahout jobs, delete temporary and output files between runs.</span></span> <span data-ttu-id="9854b-159">만든 tooremove hello 파일 hello로이 문서의 이전 스크립트는 PowerShell 스크립트 뒤 hello 사용:</span><span class="sxs-lookup"><span data-stu-id="9854b-159">tooremove hello files created by hello earlier scripts in this document, use hello following PowerShell script:</span></span>

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

#Get hello cluster info so we can get hello resource group, storage, etc.
$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName = $clusterInfo.DefaultStorageAccount.split('.')[0]
$container = $clusterInfo.DefaultStorageContainer
$storageAccountKey = (Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage context and upload hello file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

#Azure PowerShell can't delete blobs using wildcard,
#so have tooget a list and delete one at a time
# Start with hello output
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/out"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
# Next hello temp files
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/temp"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
```

### <span data-ttu-id="9854b-160"><a name="nopowershell"></a>Azure PowerShell에서 작동하지 않는 클래스</span><span class="sxs-lookup"><span data-stu-id="9854b-160"><a name="nopowershell"></a>Classes that do not work with Azure PowerShell</span></span>

<span data-ttu-id="9854b-161">아래의 클래스가 hello를 사용 하는 mahout 작업이 Windows PowerShell에서 사용 될 때 다양 한 오류 메시지를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-161">Mahout jobs that use hello following classes return various error messages when used from Windows PowerShell:</span></span>

* <span data-ttu-id="9854b-162">org.apache.mahout.utils.clustering.ClusterDumper</span><span class="sxs-lookup"><span data-stu-id="9854b-162">org.apache.mahout.utils.clustering.ClusterDumper</span></span>
* <span data-ttu-id="9854b-163">org.apache.mahout.utils.SequenceFileDumper</span><span class="sxs-lookup"><span data-stu-id="9854b-163">org.apache.mahout.utils.SequenceFileDumper</span></span>
* <span data-ttu-id="9854b-164">org.apache.mahout.utils.vectors.lucene.Driver</span><span class="sxs-lookup"><span data-stu-id="9854b-164">org.apache.mahout.utils.vectors.lucene.Driver</span></span>
* <span data-ttu-id="9854b-165">org.apache.mahout.utils.vectors.arff.Driver</span><span class="sxs-lookup"><span data-stu-id="9854b-165">org.apache.mahout.utils.vectors.arff.Driver</span></span>
* <span data-ttu-id="9854b-166">org.apache.mahout.text.WikipediaToSequenceFile</span><span class="sxs-lookup"><span data-stu-id="9854b-166">org.apache.mahout.text.WikipediaToSequenceFile</span></span>
* <span data-ttu-id="9854b-167">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span><span class="sxs-lookup"><span data-stu-id="9854b-167">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span></span>
* <span data-ttu-id="9854b-168">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span><span class="sxs-lookup"><span data-stu-id="9854b-168">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span></span>
* <span data-ttu-id="9854b-169">org.apache.mahout.classifier.sgd.TrainLogistic</span><span class="sxs-lookup"><span data-stu-id="9854b-169">org.apache.mahout.classifier.sgd.TrainLogistic</span></span>
* <span data-ttu-id="9854b-170">org.apache.mahout.classifier.sgd.RunLogistic</span><span class="sxs-lookup"><span data-stu-id="9854b-170">org.apache.mahout.classifier.sgd.RunLogistic</span></span>
* <span data-ttu-id="9854b-171">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="9854b-171">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span></span>
* <span data-ttu-id="9854b-172">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="9854b-172">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span></span>
* <span data-ttu-id="9854b-173">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="9854b-173">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span></span>
* <span data-ttu-id="9854b-174">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span><span class="sxs-lookup"><span data-stu-id="9854b-174">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span></span>
* <span data-ttu-id="9854b-175">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span><span class="sxs-lookup"><span data-stu-id="9854b-175">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span></span>
* <span data-ttu-id="9854b-176">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span><span class="sxs-lookup"><span data-stu-id="9854b-176">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span></span>
* <span data-ttu-id="9854b-177">org.apache.mahout.classifier.df.tools.Describe</span><span class="sxs-lookup"><span data-stu-id="9854b-177">org.apache.mahout.classifier.df.tools.Describe</span></span>

<span data-ttu-id="9854b-178">이러한 클래스를 사용 하는 toorun 작업 SSH를 사용 하 여 toohello HDInsight 클러스터에 연결 하 고 hello 명령줄에서 hello 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-178">toorun jobs that use these classes, connect toohello HDInsight cluster using SSH and run hello jobs from hello command line.</span></span> <span data-ttu-id="9854b-179">SSH toorun Mahout 작업을 사용 하 여 예제를 보려면 [Mahout 및 HDInsight SSH () 사용 하 여 영화 권장 구성 생성](hdinsight-hadoop-mahout-linux-mac.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9854b-179">For an example of using SSH toorun Mahout jobs, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9854b-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9854b-180">Next steps</span></span>

<span data-ttu-id="9854b-181">배웠습니다 했으므로 toouse Mahout, HDInsight의 데이터로 작업 하는 다른 방법을 검색 하는 방법을:</span><span class="sxs-lookup"><span data-stu-id="9854b-181">Now that you have learned how toouse Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="9854b-182">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="9854b-182">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="9854b-183">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="9854b-183">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="9854b-184">HDInsight에서 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="9854b-184">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

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
