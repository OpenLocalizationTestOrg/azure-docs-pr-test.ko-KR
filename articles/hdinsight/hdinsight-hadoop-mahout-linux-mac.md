---
title: "Mahout 및 HDInsight(SSH)를 사용하여 추천 생성 - Azure | Microsoft Docs"
description: "Apache Mahout 기계 학습 라이브러리를 사용하여 HDInsight(Hadoop)에서 영화 추천을 생성하는 방법을 알아봅니다."
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
ms.openlocfilehash: 28450d72f19a5467d88bc787d11f6c37c5afbf9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-linux-based-hadoop-in-hdinsight-ssh"></a><span data-ttu-id="113aa-103">HDInsight(SSH)의 Linux 기반 Hadoop와 함께 Apache Mahout를 사용하여 영화 추천 생성</span><span class="sxs-lookup"><span data-stu-id="113aa-103">Generate movie recommendations by using Apache Mahout with Linux-based Hadoop in HDInsight (SSH)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="113aa-104">Azure HDInsight에서 [Apache Mahout](http://mahout.apache.org) 기계 학습 라이브러리를 사용하여 영화 추천을 생성하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-104">Learn how to use the [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight to generate movie recommendations.</span></span>

<span data-ttu-id="113aa-105">Mahout은 Apache Hadoop용 [Machine Learning][ml] 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-105">Mahout is a [machine learning][ml] library for Apache Hadoop.</span></span> <span data-ttu-id="113aa-106">Mahout에는 필터링, 분류 및 클러스터링과 같은 데이터 처리를 위한 알고리즘이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-106">Mahout contains algorithms for processing data, such as filtering, classification, and clustering.</span></span> <span data-ttu-id="113aa-107">이 문서에서는 권장 엔진을 사용하여 친구가 본 영화를 기준으로 영화 권장을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-107">In this article, you use a recommendation engine to generate movie recommendations that are based on movies your friends have seen.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="113aa-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="113aa-108">Prerequisites</span></span>

* <span data-ttu-id="113aa-109">Linux 기반 HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-109">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="113aa-110">HDInsight 클러스터 만들기에 대한 자세한 내용은 [HDInsight에서 Linux 기반 Hadoop 사용 시작][getstarted]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="113aa-110">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="113aa-111">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="113aa-112">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="113aa-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="113aa-113">SSH 클라이언트.</span><span class="sxs-lookup"><span data-stu-id="113aa-113">An SSH client.</span></span> <span data-ttu-id="113aa-114">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="113aa-114">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="mahout-versioning"></a><span data-ttu-id="113aa-115">Mahout 버전 관리</span><span class="sxs-lookup"><span data-stu-id="113aa-115">Mahout versioning</span></span>

<span data-ttu-id="113aa-116">HDInsight 클러스터의 Mahout 버전에 대한 자세한 내용은 [HDInsight 버전 및 Hadoop 구성 요소](hdinsight-component-versioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="113aa-116">For more information about the version of Mahout in HDInsight, see [HDInsight versions and Hadoop components](hdinsight-component-versioning.md).</span></span>

## <span data-ttu-id="113aa-117"><a name="recommendations"></a>이해 권장 사항</span><span class="sxs-lookup"><span data-stu-id="113aa-117"><a name="recommendations"></a>Understanding recommendations</span></span>

<span data-ttu-id="113aa-118">Mahout에서 제공하는 기능 중 하나가 추천 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-118">One of the functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="113aa-119">이 엔진은 `userID`, `itemId` 및 `prefValue`(항목에 대한 선호도) 형식의 데이터를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-119">This engine accepts data in the format of `userID`, `itemId`, and `prefValue` (the preference for the item).</span></span> <span data-ttu-id="113aa-120">그런 다음 Mahout에서 동시 발생 분석을 수행하여 *특정 항목에 대한 선호도를 가진 사용자가 다른 항목에 대한 선호도도 갖고 있는지*확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-120">Mahout can then perform co-occurance analysis to determine: *users who have a preference for an item also have a preference for these other items*.</span></span> <span data-ttu-id="113aa-121">Mahout은 좋아하는 항목 선호도를 가진 사용자를 확인하며, 이 선호도는 추천하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-121">Mahout then determines users with like-item preferences, which can be used to make recommendations.</span></span>

<span data-ttu-id="113aa-122">다음 워크플로는 영화 데이터를 사용하는 단순한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-122">The following workflow is a simplified example that uses movie data:</span></span>

* <span data-ttu-id="113aa-123">**동시 발생**: Joe, Alice 및 Bob은 모두 *스타워즈*, *제국의 역습* 및 *제다이의 귀환*을 좋아합니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-123">**Co-occurance**: Joe, Alice, and Bob all liked *Star Wars*, *The Empire Strikes Back*, and *Return of the Jedi*.</span></span> <span data-ttu-id="113aa-124">Mahout은 이러한 영화 중 하나를 좋아하면서 다른 두 개도 좋아하는 사용자를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-124">Mahout determines that users who like any one of these movies also like the other two.</span></span>

* <span data-ttu-id="113aa-125">**동시 발생**: Bob 및 Alice는 *보이지 않는 위협*, *클론의 습격* 및 *시스의 복수*도 좋아합니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-125">**Co-occurance**: Bob and Alice also liked *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span></span> <span data-ttu-id="113aa-126">Mahout은 이전의 3개 영화를 좋아했던 사용자가 이 3개 영화도 좋아하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-126">Mahout determines that users who liked the previous three movies also like these three movies.</span></span>

* <span data-ttu-id="113aa-127">**유사성 추천**: Joe가 첫 3개 영화를 좋아하므로, Mahout은 유사한 선호도를 가진 다른 사람이 좋아하지만 Joe는 본(좋아하거나 평가한) 적이 없는 영화를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-127">**Similarity recommendation**: Because Joe liked the first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="113aa-128">이 경우 Mahout은 *보이지 않는 위협*, *클론의 습격* 및 *시스의 복수*를 추천합니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-128">In this case, Mahout recommends *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span></span>

### <a name="understanding-the-data"></a><span data-ttu-id="113aa-129">데이터 이해</span><span class="sxs-lookup"><span data-stu-id="113aa-129">Understanding the data</span></span>

<span data-ttu-id="113aa-130">편의를 위해 [GroupLens Research][movielens]에서 Mahout과 호환되는 형식으로 영화에 대한 평가 데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-130">Conveniently, [GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="113aa-131">이 데이터는 클러스터의 기본 저장소( `/HdiSamples/HdiSamples/MahoutMovieData`)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-131">This data is available on your cluster's default storage at `/HdiSamples/HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="113aa-132">`moviedb.txt` 및 `user-ratings.txt` 등 두 가지 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-132">There are two files, `moviedb.txt` and `user-ratings.txt`.</span></span> <span data-ttu-id="113aa-133">user-ratings.txt 파일은 분석 중에 사용되지만 moviedb.txt는 분석 결과를 표시할 때 사용자에게 친숙한 텍스트 정보를 제공하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-133">The user-ratings.txt file is used during analysis, while moviedb.txt is used to provide user-friendly text information when displaying the results of the analysis.</span></span>

<span data-ttu-id="113aa-134">user-ratings.txt에 포함된 데이터의 구조는 `userID`, `movieID`, `userRating` 및 `timestamp`이며, 각 사용자의 영화 등급 평가를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-134">The data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="113aa-135">다음은 데이터의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-135">Here is an example of the data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

## <a name="run-the-analysis"></a><span data-ttu-id="113aa-136">분석 실행</span><span class="sxs-lookup"><span data-stu-id="113aa-136">Run the analysis</span></span>

<span data-ttu-id="113aa-137">클러스터에 대한 SSH 연결에서 다음 명령을 사용하여 권장 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-137">From an SSH connection to the cluster, use the following command to run the recommendation job:</span></span>

```bash
mahout recommenditembased -s SIMILARITY_COOCCURRENCE -i /HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt -o /example/data/mahoutout --tempDir /temp/mahouttemp
```

> [!NOTE]
> <span data-ttu-id="113aa-138">작업을 완료하려면 몇 분정도 걸릴 수 있으며 여러 MapReduce 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-138">The job may take several minutes to complete, and may run multiple MapReduce jobs.</span></span>

## <a name="view-the-output"></a><span data-ttu-id="113aa-139">출력 보기</span><span class="sxs-lookup"><span data-stu-id="113aa-139">View the output</span></span>

1. <span data-ttu-id="113aa-140">작업이 완료되면 다음 명령을 사용하여 생성된 결과를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-140">Once the job completes, use the following command to view the generated output:</span></span>

    ```bash
    hdfs dfs -text /example/data/mahoutout/part-r-00000
    ```

    <span data-ttu-id="113aa-141">출력은 다음과 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-141">The output appears as follows:</span></span>

        1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
        2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
        3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
        4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

    <span data-ttu-id="113aa-142">첫 번째 열은 `userID`입니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-142">The first column is the `userID`.</span></span> <span data-ttu-id="113aa-143">'[' 및 ']'에 포함된 값은 `movieId`:`recommendationScore`입니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-143">The values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

2. <span data-ttu-id="113aa-144">moviedb.txt와 함께 출력을 사용하여 권장 사항에 대한 자세한 내용을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-144">You can use the output, along with the moviedb.txt, to provide more information on the recommendations.</span></span> <span data-ttu-id="113aa-145">먼저, 다음 명령을 사용하여 파일을 로컬로 복사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-145">First, we need to copy the files locally using the following commands:</span></span>

    ```bash
    hdfs dfs -get /example/data/mahoutout/part-r-00000 recommendations.txt
    hdfs dfs -get /HdiSamples/HdiSamples/MahoutMovieData/* .
    ```

    <span data-ttu-id="113aa-146">이 명령은 영화 데이터 파일과 함께 현재 디렉터리에 있는 **recommendations.txt**라는 파일에 출력 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-146">This command copies the output data to a file named **recommendations.txt** in the current directory, along with the movie data files.</span></span>

3. <span data-ttu-id="113aa-147">다음 명령을 사용하여 권장 사항 출력에서 데이터에 대한 영화 이름을 찾는 Python 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-147">Use the following command to create a Python script that looks up movie names for the data in the recommendations output:</span></span>

    ```bash
    nano show_recommendations.py
    ```

    <span data-ttu-id="113aa-148">편집기가 열리면 파일의 내용으로 다음 텍스트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-148">When the editor opens, use the following text as the contents of the file:</span></span>

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

    <span data-ttu-id="113aa-149">**Ctrl-X**, **Y**, **Enter** 키를 차례로 눌러 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-149">Press **Ctrl-X**, **Y**, and finally **Enter** to save the data.</span></span>

4. <span data-ttu-id="113aa-150">Python 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-150">Run the Python script.</span></span> <span data-ttu-id="113aa-151">다음 명령에서는 모든 파일이 다운로드된 디렉터리에 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-151">The following command assumes you are in the directory where all the files were downloaded:</span></span>

    ```bash
    python show_recommendations.py 4 user-ratings.txt moviedb.txt recommendations.txt
    ```

    <span data-ttu-id="113aa-152">이 명령은 사용자 ID 4에 대해 생성된 권장을 조사합니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-152">This command looks at the recommendations generated for user ID 4.</span></span>

    * <span data-ttu-id="113aa-153">**user-ratings.txt** 파일은 등급이 평가된 영화를 검색하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-153">The **user-ratings.txt** file is used to retrieve movies that have been rated.</span></span>

    * <span data-ttu-id="113aa-154">**moviedb.txt** 파일은 영화의 이름을 검색하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-154">The **moviedb.txt** file is used to retrieve the names of the movies.</span></span>

    * <span data-ttu-id="113aa-155">**recommendations.txt** 파일은 이 사용자의 영화 권장을 검색하는데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-155">The **recommendations.txt** is used to retrieve the movie recommendations for this user.</span></span>

     <span data-ttu-id="113aa-156">이 명령의 출력은 다음 텍스트와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-156">The output from this command is similar to the following text:</span></span>

        <span data-ttu-id="113aa-157">Seven Years in Tibet (1997), score=5.0   Indiana Jones and the Last Crusade (1989), score=5.0   Jaws (1975), score=5.0   Sense and Sensibility (1995), score=5.0   Independence Day (ID4) (1996), score=5.0   My Best Friend's Wedding (1997), score=5.0   Jerry Maguire (1996), score=5.0   Scream 2 (1997), score=5.0   Time to Kill, A (1996), score=5.0</span><span class="sxs-lookup"><span data-stu-id="113aa-157">Seven Years in Tibet (1997), score=5.0   Indiana Jones and the Last Crusade (1989), score=5.0   Jaws (1975), score=5.0   Sense and Sensibility (1995), score=5.0   Independence Day (ID4) (1996), score=5.0   My Best Friend's Wedding (1997), score=5.0   Jerry Maguire (1996), score=5.0   Scream 2 (1997), score=5.0   Time to Kill, A (1996), score=5.0</span></span>

## <a name="delete-temporary-data"></a><span data-ttu-id="113aa-158">임시 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="113aa-158">Delete temporary data</span></span>

<span data-ttu-id="113aa-159">Mahout 작업은 작업을 처리하는 동안 생성된 임시 데이터를 제거하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-159">Mahout jobs do not remove temporary data that is created while processing the job.</span></span> <span data-ttu-id="113aa-160">이 `--tempDir` 매개 변수는 쉽게 삭제할 수 있도록 임시 파일을 특정 경로로 분리하기 위해 예제 작업에서 지정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-160">The `--tempDir` parameter is specified in the example job to isolate the temporary files into a specific path for easy deletion.</span></span> <span data-ttu-id="113aa-161">임시 파일을 제거하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-161">To remove the temp files, use the following command:</span></span>

```bash
hdfs dfs -rm -f -r /temp/mahouttemp
```

> [!WARNING]
> <span data-ttu-id="113aa-162">명령을 다시 실행하려는 경우 출력 디렉터리도 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-162">If you want to run the command again, you must also delete the output directory.</span></span> <span data-ttu-id="113aa-163">이 디렉터리를 삭제하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-163">Use the following to delete this directory:</span></span>
>
> `hdfs dfs -rm -f -r /example/data/mahoutout`


## <a name="next-steps"></a><span data-ttu-id="113aa-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="113aa-164">Next steps</span></span>

<span data-ttu-id="113aa-165">이제 Mahout을 사용하는 방법을 배웠으므로 HDInsight에서 데이터로 작업하는 다른 방법을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="113aa-165">Now that you have learned how to use Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="113aa-166">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="113aa-166">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="113aa-167">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="113aa-167">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="113aa-168">HDInsight에서 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="113aa-168">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

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
