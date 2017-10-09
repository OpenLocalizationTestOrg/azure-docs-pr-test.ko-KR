---
title: "Mahout 및 HDInsight SSH ()-Azure 사용 하 여 aaaGenerate 권장 사항 | Microsoft Docs"
description: "Toouse Apache Mahout 시스템 라이브러리 toogenerate 영화 권장 사항 (Hadoop) HDInsight와 학습 hello 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c78ec37c-9a8c-4bb6-9e38-0bdb9e89fbd7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: fedac9ceb4268f8421bce4623a5ad271041b8b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-linux-based-hadoop-in-hdinsight-ssh"></a><span data-ttu-id="00839-103">HDInsight(SSH)의 Linux 기반 Hadoop와 함께 Apache Mahout를 사용하여 영화 추천 생성</span><span class="sxs-lookup"><span data-stu-id="00839-103">Generate movie recommendations by using Apache Mahout with Linux-based Hadoop in HDInsight (SSH)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="00839-104">자세한 내용은 방법 toouse hello [Apache Mahout](http://mahout.apache.org) Azure HDInsight toogenerate 영화 권장 사항이 포함 된 시스템 학습 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="00839-104">Learn how toouse hello [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight toogenerate movie recommendations.</span></span>

<span data-ttu-id="00839-105">Mahout은 Apache Hadoop용 [Machine Learning][ml] 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="00839-105">Mahout is a [machine learning][ml] library for Apache Hadoop.</span></span> <span data-ttu-id="00839-106">Mahout에는 필터링, 분류 및 클러스터링과 같은 데이터 처리를 위한 알고리즘이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="00839-106">Mahout contains algorithms for processing data, such as filtering, classification, and clustering.</span></span> <span data-ttu-id="00839-107">이 문서에서는 영화 친구 보았습니다 기반으로 하는 추천 엔진 toogenerate 영화 권장을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="00839-107">In this article, you use a recommendation engine toogenerate movie recommendations that are based on movies your friends have seen.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00839-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="00839-108">Prerequisites</span></span>

* <span data-ttu-id="00839-109">Linux 기반 HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="00839-109">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="00839-110">HDInsight 클러스터 만들기에 대한 자세한 내용은 [HDInsight에서 Linux 기반 Hadoop 사용 시작][getstarted]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00839-110">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="00839-111">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="00839-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="00839-112">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00839-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="00839-113">SSH 클라이언트.</span><span class="sxs-lookup"><span data-stu-id="00839-113">An SSH client.</span></span> <span data-ttu-id="00839-114">자세한 내용은 참조 hello [SSH HDInsight를 사용](hdinsight-hadoop-linux-use-ssh-unix.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="00839-114">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="mahout-versioning"></a><span data-ttu-id="00839-115">Mahout 버전 관리</span><span class="sxs-lookup"><span data-stu-id="00839-115">Mahout versioning</span></span>

<span data-ttu-id="00839-116">HDInsight에서 Mahout hello 버전에 대 한 자세한 내용은 참조 [HDInsight 버전 및 Hadoop 구성 요소가](hdinsight-component-versioning.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="00839-116">For more information about hello version of Mahout in HDInsight, see [HDInsight versions and Hadoop components](hdinsight-component-versioning.md).</span></span>

## <span data-ttu-id="00839-117"><a name="recommendations"></a>이해 권장 사항</span><span class="sxs-lookup"><span data-stu-id="00839-117"><a name="recommendations"></a>Understanding recommendations</span></span>

<span data-ttu-id="00839-118">Mahout에서 제공 하는 hello 함수 중 하나에 추천 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="00839-118">One of hello functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="00839-119">이 엔진 hello 형식의의 데이터를 수용 `userID`, `itemId`, 및 `prefValue` (hello hello 항목에 대 한 기본 설정).</span><span class="sxs-lookup"><span data-stu-id="00839-119">This engine accepts data in hello format of `userID`, `itemId`, and `prefValue` (hello preference for hello item).</span></span> <span data-ttu-id="00839-120">Mahout 분석 toodetermine 공동 발생을 수행할 수: *가진 사용자는 항목에 대 한 기본 설정도 있습니다 이러한 기본 설정을 다른 항목*합니다.</span><span class="sxs-lookup"><span data-stu-id="00839-120">Mahout can then perform co-occurance analysis toodetermine: *users who have a preference for an item also have a preference for these other items*.</span></span> <span data-ttu-id="00839-121">Mahout 사용된 toomake 권장 될 수 있는 유사 항목 기본 설정이 있는 사용자를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00839-121">Mahout then determines users with like-item preferences, which can be used toomake recommendations.</span></span>

<span data-ttu-id="00839-122">hello 다음 워크플로 동영상 데이터를 사용 하는 간단한 예제.</span><span class="sxs-lookup"><span data-stu-id="00839-122">hello following workflow is a simplified example that uses movie data:</span></span>

* <span data-ttu-id="00839-123">**공동 발생**: Joe, Alice와 Bob 모든 좋아하는 *별 전쟁*, *제국 공격 다시 hello*, 및 *hello 제다이 반환*합니다.</span><span class="sxs-lookup"><span data-stu-id="00839-123">**Co-occurance**: Joe, Alice, and Bob all liked *Star Wars*, *hello Empire Strikes Back*, and *Return of hello Jedi*.</span></span> <span data-ttu-id="00839-124">Mahout은 사용자도 이러한 동영상 같은 다른 두 hello 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="00839-124">Mahout determines that users who like any one of these movies also like hello other two.</span></span>

* <span data-ttu-id="00839-125">**공동 발생**: Alice와 Bob도 빴 *Phantom의 위협 hello*, *hello 복제본의 공격*, 및 *Sith hello의 복수*합니다.</span><span class="sxs-lookup"><span data-stu-id="00839-125">**Co-occurance**: Bob and Alice also liked *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span> <span data-ttu-id="00839-126">Mahout은 hello 이전 세 영화도 좋아 한 사용자 등 이러한 세 가지 동영상 차단 하는 것을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00839-126">Mahout determines that users who liked hello previous three movies also like these three movies.</span></span>

* <span data-ttu-id="00839-127">**유사성 권장**: 때문에 Joe 처음 세 개의 영화 hello 빴, Mahout 영화에서 마음 비슷한 기본 설정과 다른 보이지만 Joe에 (빴/등급) 조사 하지 합니다.</span><span class="sxs-lookup"><span data-stu-id="00839-127">**Similarity recommendation**: Because Joe liked hello first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="00839-128">Mahout 권장 하는 경우에 *Phantom의 위협 hello*, *hello 복제본의 공격*, 및 *Sith hello의 복수*합니다.</span><span class="sxs-lookup"><span data-stu-id="00839-128">In this case, Mahout recommends *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span>

### <a name="understanding-hello-data"></a><span data-ttu-id="00839-129">Hello 데이터 이해</span><span class="sxs-lookup"><span data-stu-id="00839-129">Understanding hello data</span></span>

<span data-ttu-id="00839-130">편의를 위해 [GroupLens Research][movielens]에서 Mahout과 호환되는 형식으로 영화에 대한 평가 데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="00839-130">Conveniently, [GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="00839-131">이 데이터는 클러스터의 기본 저장소( `/HdiSamples/HdiSamples/MahoutMovieData`)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00839-131">This data is available on your cluster's default storage at `/HdiSamples/HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="00839-132">`moviedb.txt` 및 `user-ratings.txt` 등 두 가지 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00839-132">There are two files, `moviedb.txt` and `user-ratings.txt`.</span></span> <span data-ttu-id="00839-133">hello 사용자 ratings.txt 파일이 moviedb.txt hello hello 분석 결과 표시할 때 사용 되는 tooprovide 친숙 한 텍스트 정보는 분석 하는 동안 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00839-133">hello user-ratings.txt file is used during analysis, while moviedb.txt is used tooprovide user-friendly text information when displaying hello results of hello analysis.</span></span>

<span data-ttu-id="00839-134">hello 사용자 ratings.txt에 포함 된 데이터의 구조는의 `userID`, `movieID`, `userRating`, 및 `timestamp`, 각 사용자 등급 동영상을 지정 하는 방식을 높은 우리 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="00839-134">hello data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="00839-135">Hello 데이터의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="00839-135">Here is an example of hello data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

## <a name="run-hello-analysis"></a><span data-ttu-id="00839-136">Hello 분석 실행</span><span class="sxs-lookup"><span data-stu-id="00839-136">Run hello analysis</span></span>

<span data-ttu-id="00839-137">SSH 연결 toohello 클러스터에서 사용 하 여 hello 다음 명령 toorun hello 권장 구성 작업 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00839-137">From an SSH connection toohello cluster, use hello following command toorun hello recommendation job:</span></span>

```bash
mahout recommenditembased -s SIMILARITY_COOCCURRENCE -i /HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt -o /example/data/mahoutout --tempDir /temp/mahouttemp
```

> [!NOTE]
> <span data-ttu-id="00839-138">hello 작업이 몇 분 toocomplete 걸리고 여러 MapReduce 작업 실행 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00839-138">hello job may take several minutes toocomplete, and may run multiple MapReduce jobs.</span></span>

## <a name="view-hello-output"></a><span data-ttu-id="00839-139">Hello 출력 보기</span><span class="sxs-lookup"><span data-stu-id="00839-139">View hello output</span></span>

1. <span data-ttu-id="00839-140">Hello 작업이 완료 되 면 다음 명령 tooview hello 생성 된 출력 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="00839-140">Once hello job completes, use hello following command tooview hello generated output:</span></span>

    ```bash
    hdfs dfs -text /example/data/mahoutout/part-r-00000
    ```

    <span data-ttu-id="00839-141">다음과 같이 hello 출력이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00839-141">hello output appears as follows:</span></span>

        1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
        2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
        3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
        4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

    <span data-ttu-id="00839-142">hello 첫 번째 열은 hello `userID`합니다.</span><span class="sxs-lookup"><span data-stu-id="00839-142">hello first column is hello `userID`.</span></span> <span data-ttu-id="00839-143">hello에 포함 된 값 ' [' 및 ']'은 `movieId`:`recommendationScore`합니다.</span><span class="sxs-lookup"><span data-stu-id="00839-143">hello values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

2. <span data-ttu-id="00839-144">Hello moviedb.txt, tooprovide 함께 hello 출력 하는 방법은 hello 권장 사항에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00839-144">You can use hello output, along with hello moviedb.txt, tooprovide more information on hello recommendations.</span></span> <span data-ttu-id="00839-145">먼저 다음 명령을 hello를 사용 하 여 로컬로 toocopy hello 파일:</span><span class="sxs-lookup"><span data-stu-id="00839-145">First, we need toocopy hello files locally using hello following commands:</span></span>

    ```bash
    hdfs dfs -get /example/data/mahoutout/part-r-00000 recommendations.txt
    hdfs dfs -get /HdiSamples/HdiSamples/MahoutMovieData/* .
    ```

    <span data-ttu-id="00839-146">이 명령은 복사본 hello 라는 출력 데이터 tooa 파일 **recommendations.txt** hello 동영상 데이터 파일 뿐만 아니라 hello 현재 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00839-146">This command copies hello output data tooa file named **recommendations.txt** in hello current directory, along with hello movie data files.</span></span>

3. <span data-ttu-id="00839-147">다음 명령 toocreate hello 데이터 hello 권장 사항 출력에 대 한 동영상 이름을 조회 하는 Python 스크립트 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="00839-147">Use hello following command toocreate a Python script that looks up movie names for hello data in hello recommendations output:</span></span>

    ```bash
    nano show_recommendations.py
    ```

    <span data-ttu-id="00839-148">Hello 편집기가 열리고 때는 hello 콘텐츠로 사용 hello 파일의 텍스트를 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="00839-148">When hello editor opens, use hello following text as hello contents of hello file:</span></span>

   ```python
   #!/usr/bin/env python

   import sys

   if len(sys.argv) != 5:
        print "Arguments: userId userDataFilename movieFilename recommendationFilename"
        sys.exit(1)

   userId, userDataFilename, movieFilename, recommendationFilename = sys.argv[1:]

   print "Reading Movies Descriptions"
   movieFile = open(movieFilename)
   movieById = {}
   for line in movieFile:
       tokens = line.split("|")
       movieById[tokens[0]] = tokens[1:]
   movieFile.close()

   print "Reading Rated Movies"
   userDataFile = open(userDataFilename)
   ratedMovieIds = []
   for line in userDataFile:
       tokens = line.split("\t")
       if tokens[0] == userId:
           ratedMovieIds.append((tokens[1],tokens[2]))
   userDataFile.close()

   print "Reading Recommendations"
   recommendationFile = open(recommendationFilename)
   recommendations = []
   for line in recommendationFile:
       tokens = line.split("\t")
       if tokens[0] == userId:
           movieIdAndScores = tokens[1].strip("[]\n").split(",")
           recommendations = [ movieIdAndScore.split(":") for movieIdAndScore in movieIdAndScores ]
           break
   recommendationFile.close()

   print "Rated Movies"
   print "------------------------"
   for movieId, rating in ratedMovieIds:
       print "%s, rating=%s" % (movieById[movieId][0], rating)
   print "------------------------"

   print "Recommended Movies"
   print "------------------------"
   for movieId, score in recommendations:
       print "%s, score=%s" % (movieById[movieId][0], score)
   print "------------------------"
   ```

    <span data-ttu-id="00839-149">키를 눌러 **Ctrl-X**, **Y**, 마지막으로 **Enter** toosave hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="00839-149">Press **Ctrl-X**, **Y**, and finally **Enter** toosave hello data.</span></span>

4. <span data-ttu-id="00839-150">Hello Python 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="00839-150">Run hello Python script.</span></span> <span data-ttu-id="00839-151">hello 다음 명령을 가정 모든 hello 파일 다운로드 되었는지 hello 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00839-151">hello following command assumes you are in hello directory where all hello files were downloaded:</span></span>

    ```bash
    python show_recommendations.py 4 user-ratings.txt moviedb.txt recommendations.txt
    ```

    <span data-ttu-id="00839-152">이 명령은 사용자 ID 4에 대해 생성 된 hello 권장 사항을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="00839-152">This command looks at hello recommendations generated for user ID 4.</span></span>

    * <span data-ttu-id="00839-153">hello **사용자 ratings.txt** 파일은 등급이 지정 된 사용 되는 tooretrieve 영화 합니다.</span><span class="sxs-lookup"><span data-stu-id="00839-153">hello **user-ratings.txt** file is used tooretrieve movies that have been rated.</span></span>

    * <span data-ttu-id="00839-154">hello **moviedb.txt** 파일은 hello 영화 사용 되는 tooretrieve hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="00839-154">hello **moviedb.txt** file is used tooretrieve hello names of hello movies.</span></span>

    * <span data-ttu-id="00839-155">hello **recommendations.txt** 가 사용 되는 tooretrieve이이 사용자에 대 한 hello 영화 권장 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="00839-155">hello **recommendations.txt** is used tooretrieve hello movie recommendations for this user.</span></span>

     <span data-ttu-id="00839-156">hello이이 명령에서 비슷한 toohello 팔 로우 텍스트 출력:</span><span class="sxs-lookup"><span data-stu-id="00839-156">hello output from this command is similar toohello following text:</span></span>

        <span data-ttu-id="00839-157">점수를 7 년 동안 Tibet (1997)에서 = 5.0 인 경우 인디애나 Jones와 마지막 치기 전에 말일 세 (1989) hello 점수 = 5.0 인 경우 Jaws (1975) 점수 = 5.0 인 경우 의미 및 Sensibility (1995) 점수 = 5.0 인 독립 기념일 (ID4) (1996 년) 점수 = 5.0 인 경우 내 가장 친한 친구의 (1997)으로 청첩장 점수 = 5.0 인 경우 Jerry Maguire (1996 년 ), 점수 = 5.0 인 경우 Scream 2 (1997) 점수 = 5.0 인 경우 시간 tooKill, (1996), 점수를 매길 = 5.0 인 경우</span><span class="sxs-lookup"><span data-stu-id="00839-157">Seven Years in Tibet (1997), score=5.0   Indiana Jones and hello Last Crusade (1989), score=5.0   Jaws (1975), score=5.0   Sense and Sensibility (1995), score=5.0   Independence Day (ID4) (1996), score=5.0   My Best Friend's Wedding (1997), score=5.0   Jerry Maguire (1996), score=5.0   Scream 2 (1997), score=5.0   Time tooKill, A (1996), score=5.0</span></span>

## <a name="delete-temporary-data"></a><span data-ttu-id="00839-158">임시 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="00839-158">Delete temporary data</span></span>

<span data-ttu-id="00839-159">Mahout 작업 hello 작업을 처리 하는 동안 만든 임시 데이터를 제거 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00839-159">Mahout jobs do not remove temporary data that is created while processing hello job.</span></span> <span data-ttu-id="00839-160">hello `--tempDir` 매개 변수를 쉽게 삭제에 대 한 특정 경로에 hello 예제 작업 tooisolate hello 임시 파일에 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00839-160">hello `--tempDir` parameter is specified in hello example job tooisolate hello temporary files into a specific path for easy deletion.</span></span> <span data-ttu-id="00839-161">tooremove hello 임시 파일을 hello 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="00839-161">tooremove hello temp files, use hello following command:</span></span>

```bash
hdfs dfs -rm -f -r /temp/mahouttemp
```

> [!WARNING]
> <span data-ttu-id="00839-162">Toorun hello 명령을 다시 들어 hello 출력 디렉터리를 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00839-162">If you want toorun hello command again, you must also delete hello output directory.</span></span> <span data-ttu-id="00839-163">이 디렉터리 toodelete 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="00839-163">Use hello following toodelete this directory:</span></span>
>
> `hdfs dfs -rm -f -r /example/data/mahoutout`


## <a name="next-steps"></a><span data-ttu-id="00839-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="00839-164">Next steps</span></span>

<span data-ttu-id="00839-165">배웠습니다 했으므로 toouse Mahout, HDInsight의 데이터로 작업 하는 다른 방법을 검색 하는 방법을:</span><span class="sxs-lookup"><span data-stu-id="00839-165">Now that you have learned how toouse Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="00839-166">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="00839-166">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="00839-167">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="00839-167">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="00839-168">HDInsight에서 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="00839-168">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[build]: http://mahout.apache.org/developers/buildingmahout.html
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
