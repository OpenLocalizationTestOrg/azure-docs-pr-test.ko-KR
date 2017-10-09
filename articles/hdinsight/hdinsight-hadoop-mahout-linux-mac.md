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
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-linux-based-hadoop-in-hdinsight-ssh"></a>HDInsight(SSH)의 Linux 기반 Hadoop와 함께 Apache Mahout를 사용하여 영화 추천 생성

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

자세한 내용은 방법 toouse hello [Apache Mahout](http://mahout.apache.org) Azure HDInsight toogenerate 영화 권장 사항이 포함 된 시스템 학습 라이브러리입니다.

Mahout은 Apache Hadoop용 [Machine Learning][ml] 라이브러리입니다. Mahout에는 필터링, 분류 및 클러스터링과 같은 데이터 처리를 위한 알고리즘이 포함됩니다. 이 문서에서는 영화 친구 보았습니다 기반으로 하는 추천 엔진 toogenerate 영화 권장을 사용 합니다.

## <a name="prerequisites"></a>필수 조건

* Linux 기반 HDInsight 클러스터입니다. HDInsight 클러스터 만들기에 대한 자세한 내용은 [HDInsight에서 Linux 기반 Hadoop 사용 시작][getstarted]을 참조하세요.

> [!IMPORTANT]
> Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

* SSH 클라이언트. 자세한 내용은 참조 hello [SSH HDInsight를 사용](hdinsight-hadoop-linux-use-ssh-unix.md) 문서.

## <a name="mahout-versioning"></a>Mahout 버전 관리

HDInsight에서 Mahout hello 버전에 대 한 자세한 내용은 참조 [HDInsight 버전 및 Hadoop 구성 요소가](hdinsight-component-versioning.md)합니다.

## <a name="recommendations"></a>이해 권장 사항

Mahout에서 제공 하는 hello 함수 중 하나에 추천 엔진입니다. 이 엔진 hello 형식의의 데이터를 수용 `userID`, `itemId`, 및 `prefValue` (hello hello 항목에 대 한 기본 설정). Mahout 분석 toodetermine 공동 발생을 수행할 수: *가진 사용자는 항목에 대 한 기본 설정도 있습니다 이러한 기본 설정을 다른 항목*합니다. Mahout 사용된 toomake 권장 될 수 있는 유사 항목 기본 설정이 있는 사용자를 결정 합니다.

hello 다음 워크플로 동영상 데이터를 사용 하는 간단한 예제.

* **공동 발생**: Joe, Alice와 Bob 모든 좋아하는 *별 전쟁*, *제국 공격 다시 hello*, 및 *hello 제다이 반환*합니다. Mahout은 사용자도 이러한 동영상 같은 다른 두 hello 있는지 확인 합니다.

* **공동 발생**: Alice와 Bob도 빴 *Phantom의 위협 hello*, *hello 복제본의 공격*, 및 *Sith hello의 복수*합니다. Mahout은 hello 이전 세 영화도 좋아 한 사용자 등 이러한 세 가지 동영상 차단 하는 것을 결정 합니다.

* **유사성 권장**: 때문에 Joe 처음 세 개의 영화 hello 빴, Mahout 영화에서 마음 비슷한 기본 설정과 다른 보이지만 Joe에 (빴/등급) 조사 하지 합니다. Mahout 권장 하는 경우에 *Phantom의 위협 hello*, *hello 복제본의 공격*, 및 *Sith hello의 복수*합니다.

### <a name="understanding-hello-data"></a>Hello 데이터 이해

편의를 위해 [GroupLens Research][movielens]에서 Mahout과 호환되는 형식으로 영화에 대한 평가 데이터를 제공합니다. 이 데이터는 클러스터의 기본 저장소( `/HdiSamples/HdiSamples/MahoutMovieData`)에서 사용할 수 있습니다.

`moviedb.txt` 및 `user-ratings.txt` 등 두 가지 파일이 있습니다. hello 사용자 ratings.txt 파일이 moviedb.txt hello hello 분석 결과 표시할 때 사용 되는 tooprovide 친숙 한 텍스트 정보는 분석 하는 동안 사용 됩니다.

hello 사용자 ratings.txt에 포함 된 데이터의 구조는의 `userID`, `movieID`, `userRating`, 및 `timestamp`, 각 사용자 등급 동영상을 지정 하는 방식을 높은 우리 지시 합니다. Hello 데이터의 예는 다음과 같습니다.

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

## <a name="run-hello-analysis"></a>Hello 분석 실행

SSH 연결 toohello 클러스터에서 사용 하 여 hello 다음 명령 toorun hello 권장 구성 작업 수 있습니다.

```bash
mahout recommenditembased -s SIMILARITY_COOCCURRENCE -i /HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt -o /example/data/mahoutout --tempDir /temp/mahouttemp
```

> [!NOTE]
> hello 작업이 몇 분 toocomplete 걸리고 여러 MapReduce 작업 실행 될 수 있습니다.

## <a name="view-hello-output"></a>Hello 출력 보기

1. Hello 작업이 완료 되 면 다음 명령 tooview hello 생성 된 출력 hello를 사용 합니다.

    ```bash
    hdfs dfs -text /example/data/mahoutout/part-r-00000
    ```

    다음과 같이 hello 출력이 됩니다.

        1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
        2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
        3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
        4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

    hello 첫 번째 열은 hello `userID`합니다. hello에 포함 된 값 ' [' 및 ']'은 `movieId`:`recommendationScore`합니다.

2. Hello moviedb.txt, tooprovide 함께 hello 출력 하는 방법은 hello 권장 사항에 사용할 수 있습니다. 먼저 다음 명령을 hello를 사용 하 여 로컬로 toocopy hello 파일:

    ```bash
    hdfs dfs -get /example/data/mahoutout/part-r-00000 recommendations.txt
    hdfs dfs -get /HdiSamples/HdiSamples/MahoutMovieData/* .
    ```

    이 명령은 복사본 hello 라는 출력 데이터 tooa 파일 **recommendations.txt** hello 동영상 데이터 파일 뿐만 아니라 hello 현재 디렉터리에 있습니다.

3. 다음 명령 toocreate hello 데이터 hello 권장 사항 출력에 대 한 동영상 이름을 조회 하는 Python 스크립트 hello를 사용 합니다.

    ```bash
    nano show_recommendations.py
    ```

    Hello 편집기가 열리고 때는 hello 콘텐츠로 사용 hello 파일의 텍스트를 다음 hello를 사용 합니다.

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

    키를 눌러 **Ctrl-X**, **Y**, 마지막으로 **Enter** toosave hello 데이터입니다.

4. Hello Python 스크립트를 실행 합니다. hello 다음 명령을 가정 모든 hello 파일 다운로드 되었는지 hello 디렉터리에 있습니다.

    ```bash
    python show_recommendations.py 4 user-ratings.txt moviedb.txt recommendations.txt
    ```

    이 명령은 사용자 ID 4에 대해 생성 된 hello 권장 사항을 살펴봅니다.

    * hello **사용자 ratings.txt** 파일은 등급이 지정 된 사용 되는 tooretrieve 영화 합니다.

    * hello **moviedb.txt** 파일은 hello 영화 사용 되는 tooretrieve hello 이름입니다.

    * hello **recommendations.txt** 가 사용 되는 tooretrieve이이 사용자에 대 한 hello 영화 권장 사항입니다.

     hello이이 명령에서 비슷한 toohello 팔 로우 텍스트 출력:

        점수를 7 년 동안 Tibet (1997)에서 = 5.0 인 경우 인디애나 Jones와 마지막 치기 전에 말일 세 (1989) hello 점수 = 5.0 인 경우 Jaws (1975) 점수 = 5.0 인 경우 의미 및 Sensibility (1995) 점수 = 5.0 인 독립 기념일 (ID4) (1996 년) 점수 = 5.0 인 경우 내 가장 친한 친구의 (1997)으로 청첩장 점수 = 5.0 인 경우 Jerry Maguire (1996 년 ), 점수 = 5.0 인 경우 Scream 2 (1997) 점수 = 5.0 인 경우 시간 tooKill, (1996), 점수를 매길 = 5.0 인 경우

## <a name="delete-temporary-data"></a>임시 데이터 삭제

Mahout 작업 hello 작업을 처리 하는 동안 만든 임시 데이터를 제거 하지 않습니다. hello `--tempDir` 매개 변수를 쉽게 삭제에 대 한 특정 경로에 hello 예제 작업 tooisolate hello 임시 파일에 지정 됩니다. tooremove hello 임시 파일을 hello 다음 명령을 사용 합니다.

```bash
hdfs dfs -rm -f -r /temp/mahouttemp
```

> [!WARNING]
> Toorun hello 명령을 다시 들어 hello 출력 디렉터리를 삭제 해야 합니다. 이 디렉터리 toodelete 다음 hello를 사용 합니다.
>
> `hdfs dfs -rm -f -r /example/data/mahoutout`


## <a name="next-steps"></a>다음 단계

배웠습니다 했으므로 toouse Mahout, HDInsight의 데이터로 작업 하는 다른 방법을 검색 하는 방법을:

* [HDInsight에서 Hive 사용](hdinsight-use-hive.md)
* [HDInsight에서 Pig 사용](hdinsight-use-pig.md)
* [HDInsight에서 MapReduce 사용](hdinsight-use-mapreduce.md)

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
