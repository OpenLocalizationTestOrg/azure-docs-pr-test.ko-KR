---
title: "HDInsight의 Apache Storm aaaTwitter 추세 주제 | Microsoft Docs"
description: "어떻게 toouse Trident toocreate Twitter에 대 한 추세 항목을 결정 하는 Apache Storm 토폴로지를 기반으로 해시에 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 63b280ea-5c07-4dc8-a35f-dccf5a96ba93
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/14/2017
ms.author: larryfr
ms.openlocfilehash: 0281b495d10833c63868b36856c96369b139c553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a>HDInsight에서 Apache Storm을 사용하여 Twitter 추세 항목 확인

Toouse Trident toocreate 스톰 토폴로지를 결정 하는 방법 추세에 대해 알아봅니다 Twitter에 대 한 항목 (해시 태그).

Trident는 조인, 집계, 그룹화, 함수 및 필터와 같은 도구를 제공하는 높은 수준의 추상화입니다. 또한 Trident는 상태 저장, 증분 처리를 수행하기 위한 기본 요소를 추가합니다. 이 문서에 사용 되는 hello 예제는 사용자 지정 배출구 및 함수와 Trident 토폴로지입니다. 또한 Trident에서 제공한 몇 가지 기본 함수를 사용합니다.

## <a name="requirements"></a>요구 사항

* <a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java 및 hello JDK 1.8</a>

* <a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a>

* <a href="http://git-scm.com/" target="_blank">Git</a>

* Twitter 개발자 계정

## <a name="download-hello-project"></a>Hello 프로젝트 다운로드

다음 코드 tooclone hello 프로젝트 로컬로 hello를 사용 합니다.

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-hello-topology"></a>Hello 토폴로지 이해

hello 다음 다이어그램의이 토폴로지를 통해 데이터 흐름 방식을 보여 줍니다.

![토폴로지](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> 이 다이어그램은 토폴로지 hello의 단순화 된 보기입니다. Hello 구성 요소의 여러 인스턴스 hello 클러스터 내의 hello 노드 간에 배포 됩니다.


hello hello 토폴로지를 구현 하는 Trident 코드는 다음과 같습니다.

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

이 코드는 hello 다음 작업을 수행 합니다.

1. Hello 배출구에서 스트림을 만듭니다. hello 배출구 Twitter에서 트 윗을 검색 하 고 특정 키워드 (love, 음악 및이 예제의 커피)에 대 한이 필터링 합니다.

2. HashtagExtractor, 사용자 지정 함수는 각 윗에서 사용 되는 tooextract 해시 태그입니다. hello 해시 태그는 내보낸된 toohello 스트림입니다.

3. hello 스트림 해시 태그에 의해 그룹화 되 고 tooan aggregator에 전달 합니다. 이 집계는 각 해시 태그가 발생한 횟수를 계산합니다. 이 데이터는 메모리에 유지됩니다. 마지막으로, hello 해시 태그 및 hello 수를 포함 하는 새 스트림을 내보내집니다.

4. hello **FirstN** 어셈블리는 적용 된 tooreturn hello 상위 10 개의 값만을 hello 수 필드를 기반 합니다.

> [!NOTE]
> Trident 사용한 작업에 대 한 자세한 내용은 참조 hello [Trident API 개요](http://storm.apache.org/releases/current/Trident-API-Overview.html) 문서.

### <a name="hello-spout"></a>hello 배출구

hello 배출구 **TwitterSpout**를 사용 하 여 [Twitter4j](http://twitter4j.org/en/) Twitter에서 tooretrieve 트 윗 합니다. Hello 단어에 대 한 필터가 만들어집니다 __선호__, **음악**, 및 **커피**합니다. Hello 필터와 일치 하는 들어오는 윗 (상태) 연결 된 차단 큐에 저장 됩니다. 마지막으로 항목을 hello 큐 해제 가져오고 toohello 토폴로지 내보내집니다.

### <a name="hello-hashtagextractor"></a>hello HashtagExtractor

tooextract 해시 태그 [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) hello 트 윗에 포함 된 모든 해시 태그 tooretrieve 사용된 됩니다. 이 다음 내보낸된 toohello 스트림 합니다.

## <a name="configure-twitter"></a>Twitter 구성

Twitter에서 hello 소비자 및 액세스 토큰 정보 필요한 tooread 가져올 및 hello 단계 tooregister 새 Twitter 응용 프로그램을 다음 사용:

1. 너무 이동[Twitter 앱](https://apps.twitter.com) hello 클릭 **새 앱 만들기** 단추입니다. Hello 형태로 데이터를 입력할 때 상태로 hello **콜백 URL** 필드를 빈 합니다.

2. Hello 앱을 만든 경우 클릭 hello **키와 액세스 토큰이** 탭 합니다.

3. 복사 hello **소비자 키** 및 **소비자 암호** 정보입니다.

4. Hello 페이지의 hello 맨 아래에 선택 **내 액세스 토큰 만들기** 토큰이 존재 합니다. Hello 토큰 생성 된 경우, 복사 hello **액세스 토큰** 및 **액세스 토큰 암호** 정보입니다.

5. Hello에 **TwitterSpoutTopology** 프로젝트 열기, 이전에 복제 된 hello **resources/twitter4j.properties** 파일 hello 이전 단계에서 수집한 hello 정보를 추가 하 고 다음 hello 파일 저장 .

## <a name="build-hello-topology"></a>Hello 토폴로지 빌드

다음 코드 toobuild hello 프로젝트 hello를 사용 합니다.

        cd [directoryname]
        mvn compile

## <a name="test-hello-topology"></a>테스트 hello 토폴로지

다음 명령을 로컬로 토폴로지 tootest hello hello를 사용 합니다.

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

Hello 토폴로지 시작 된 후 태그와 hello 토폴로지 별로 내보낸 수를 hello 해시를 포함 하는 디버그 정보가 표시 됩니다. hello 출력 텍스트 다음 비슷한 toohello 같아야 합니다.

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a>다음 단계

Hello 토폴로지 로컬로 테스트할 했으므로 검색 방법을 toodeploy hello 토폴로지: [배포 HDInsight의 Apache Storm 토폴로지를 관리할 및](hdinsight-storm-deploy-monitor-topology.md)합니다.

다음 스톰 항목 hello 관심이 수도 있습니다.

* [Maven을 사용하여 HDInsight의 Storm용 Java 토폴로지 개발](hdinsight-storm-develop-java-topology.md)
* [Visual Studio를 사용하여 HDInsight의 Storm용 C# 토폴로지 개발](hdinsight-storm-develop-csharp-visual-studio-topology.md)

HDinsight에 대한 추가 Storm 예제:

* [HDInsight의 Storm에 대한 예제 토폴로지](hdinsight-storm-example-topology.md)

