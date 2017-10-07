---
title: "Azure HDInsight Pig와 DataFu aaaUse | Microsoft Docs"
description: "DataFu는 Hadoop과 함께 사용하기 위한 라이브러리의 컬렉션입니다. HDInsight 클러스터에서 Pig와 함께 DataFu를 사용하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 0016721a-82be-4773-88ad-91e6b2c21cbb
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 357ad8f9694cc590115289877e752bdd242bdadc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-datafu-with-pig-on-hdinsight"></a>HDInsight에서 pig와 함께 DataFu 사용

자세한 내용은 방법 toouse HDInsight와 DataFu 합니다. DataFu는 Hadoop에서 Pig와 함께 사용하기 위한 오픈 소스 라이브러리의 컬렉션입니다.

## <a name="prerequisites"></a>필수 조건

* Azure 구독.

* Azure HDInsight 클러스터(Linux 또는 Windows 기반)

  > [!IMPORTANT]
  > Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

* [HDInsight에서 Pig 사용](hdinsight-use-pig.md)

## <a name="install-datafu-on-linux-based-hdinsight"></a>Linux 기반 HDInsight에 DataFu 설치

> [!IMPORTANT]
> DataFu는 Linux 기반 클러스터 버전 3.3 이상 및 Windows 기반 클러스터에 설치됩니다. 3.3 이전 버전의 Linux 기반 클러스터에 설치되지 않습니다.
>
> Windows 기반 또는 Linux 기반 클러스터 버전 3.3 이상 클러스터를 사용하는 경우 이 섹션을 건너뛸 수 있습니다.

DataFu 다운로드 하 고 hello Maven 저장소에서 설치할 수 있습니다. 다음 단계 tooadd DataFu tooyour HDInsight 클러스터 hello를 사용 합니다.

1. SSH를 사용 하 여 tooyour Linux 기반 HDInsight 클러스터를 연결 합니다. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

2. 다음 명령은 toodownload hello DataFu jar 파일 hello wget 유틸리티를 사용 하 여 hello를 사용 하 여 복사 하 브라우저 toobegin hello 다운로드가에 hello 링크를 붙여 넣습니다.

    ```
    wget http://central.maven.org/maven2/com/linkedin/datafu/datafu/1.2.0/datafu-1.2.0.jar
    ```

3. HDInsight 클러스터에 대 한 hello 파일 toodefault 저장소를 다음으로 업로드 합니다. Hello 파일을 기본 배치 저장소를 사용 하면 사용 가능한 tooall 노드 hello 클러스터의 합니다.

    ```
    hdfs dfs -put datafu-1.2.0.jar /example/jars
    ```

    > [!NOTE]
    > hello 이전 명령 저장에 hello jar `/example/jars` 이 디렉터리 hello 클러스터 저장소에 이미 있습니다. HDInsight 클러스터 저장소에 원하는 모든 위치를 사용할 수 있습니다.

## <a name="use-datafu-with-pig"></a>Pig와 함께 DataFu 사용

이 섹션의 단계 hello Pig를 사용 하 여 HDInsight의 익숙한 가정 합니다. HDInsight와 함께 Pig 사용에 대한 자세한 내용은 [Pig와 함께 HDInsight 사용](hdinsight-use-pig.md)을 참조하세요.

> [!IMPORTANT]
> Hello 단계를 사용 하 여 hello 이전 단원의 DataFu를 수동으로 설치한 경우이 사용 하기 전에 등록 해야 합니다.
>
> * 클러스터에서 Azure Storage를 사용하는 경우 `wasb://` 경로를 사용합니다. 예: `register wasb:///example/jars/datafu-1.2.0.jar`.
>
> * 클러스터에서 Azure Data Lake Store를 사용하는 경우 `adl://` 경로를 사용합니다. 예: `register adl://home/example/jars/datafu-1.2.0.jar`

종종 DataFu 함수에 대한 별칭을 정의합니다. hello 다음 예제에서는 정의의 별칭 `SHA`:

```piglatin
DEFINE SHA datafu.pig.hash.SHA();
```

그런 다음 hello 입력된 데이터에 대 한 라틴 Pig 스크립트 toogenerate 해시에서에서이 별칭을 사용할 수 있습니다. 예를 들어 hello 다음 코드 hello 위치 hello 입력된 데이터에는 해시 값으로 바꿉니다.

```piglatin
raw = LOAD '/HdiSamples/HdiSamples/SensorSampleData/building/building.csv' USING
    org.apache.pig.piggybank.storage.CSVExcelStorage(',', 'NO_MULTILINE', 'UNIX', 'SKIP_INPUT_HEADER') AS
    (int1:int,
     id1:chararray,
     int2:int,
     id2:chararray,
     location:chararray);
mask = FOREACH raw GENERATE int1, id1, int2, id2, SHA(location);
DUMP mask;
```

다음 출력 hello이 발생 합니다.

    (1,M1,25,AC1000,aa5ab35a9174c2062b7f7697b33fafe5ce404cf5fecf6bfbbf0dc96ba0d90046)
    (2,M2,27,FN39TG,7a1ca4ef7515f7276bae7230545829c27810c9d9e98ab2c06066bee6270d5153)
    (3,M3,28,JDNS77,07f62b021771d3cf67e2e1faf18769cc5e5c119ad7d4d1847a11e11d6d5a7ecb)
    (4,M4,17,GG1919,aed8f531aa7e785be255bc435e2582e74c58defedebcb629eeabf365b809bd6f)
    (5,M5,3,ACMAX22,1ed8c7e56c947bebc0cfcf88c4ea0f02c944568f71df893a99970e4f0c78cddc)
    (6,M6,9,AC1000,c96dd81db196cca5f57bd4270bbb9d9e9d1b242d67f9364005ee1dfdc2632523)
    (7,M7,13,FN39TG,3e049d78d958038ac6bd5dcf038075cc73362b4956aaf7308c3a69c8eca76297)
    (8,M8,25,JDNS77,c1ef40ce0484c698eb4bd27fe56c1e7b68d74f9780ed674210d0e5013dae45e9)
    (9,M9,11,GG1919,a7d355b26bda6bf1196ccffead0b2cf2b81f0a9de5b4876b44407f1dc07e51e6)
    (10,M10,23,ACMAX22,10436829032f361a3de50048de41755140e581467bc1895e6c1a17f423e42d10)
    (11,M11,14,AC1000,348841ef53dbd5a64008a86be432973db790774fb28b59b0d99702a3188b3705)
    (12,M12,26,FN39TG,aed8f531aa7e785be255bc435e2582e74c58defedebcb629eeabf365b809bd6f)
    (13,M13,25,JDNS77,ed9ad13611d7164839dd3feaf9a7f6a75a4138f389e0d45f8e07fa38da1116a2)
    (14,M14,17,GG1919,80db4ccdca106d37b920206331fcfe3e9e50a9e763d89b54ce3ad5ac8cf30f03)
    (15,M15,19,ACMAX22,3552ac0c032467fbf592cb4d10c5c9267800c01e343ad8ca557256d882ae9327)
    (16,M16,23,AC1000,07c67d76ef92ac9853588e098983fefba4ba5965f8fec95f42ab0d04c27865ba)
    (17,M17,11,FN39TG,557c1599d9a04895d3817d293e0806a4419a14de31958386182798d0d2ed3a56)
    (18,M18,25,JDNS77,dbc74a36d8e7439c45c64d856388506cc9b1218619cef979c3d605115a7a4546)
    (19,M19,14,GG1919,be55ef3f4c4e6c2d9c2afe2a33ac90ad0f50d4de7f9163999877e2a9ca5a54f8)
    (20,M20,19,ACMAX22,ea0b937ea317101ee2c26b03a4843a19ceced8a2b9673c3cf409a726ca2b0fd8)

## <a name="next-steps"></a>다음 단계

DataFu 또는 Pig에 대 한 자세한 내용은 다음 문서는 hello를 참조 하세요.

* [Apache DataFu Pig 가이드](http://datafu.incubator.apache.org/docs/datafu/guide.html)
* [HDInsight에서 Pig 사용](hdinsight-use-pig.md)
