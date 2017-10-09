---
title: "하이브 쿼리 인 하이브 테이블에서 데이터 aaaExplore | Microsoft Docs"
description: "Hive 쿼리를 사용하여 Hive 테이블의 데이터를 탐색합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0d46cea5-2b4c-4384-9bfa-fa20f6f75148
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 2ede3d41682aa08ced19284f7a83ec95e0c2a93a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-hive-tables-with-hive-queries"></a>Hive 쿼리를 사용하여 Hive 테이블의 데이터 탐색
이 문서는 HDInsight Hadoop 클러스터의 Hive 테이블에 사용 되는 tooexplore 데이터 예제 하이브 스크립트를 제공 합니다.

hello 다음 **메뉴** tootopics toouse 도구 tooexplore 데이터 저장소, 다양 한 환경에서 하는 방법을 설명 하는 링크입니다.

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a>필수 조건
이 문서에서는 사용자가 다음 작업을 수행한 것으로 가정합니다.

* Azure 저장소 계정을 만들었습니다. 지침이 필요한 경우 [Azure Storage 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account)를 참조하세요.
* Hello HDInsight 서비스를 사용 하 여 사용자 지정 된 Hadoop 클러스터 프로 비전 합니다. 지침이 필요한 경우 [고급 분석을 위한 Azure HDInsight Hadoop 클러스터 사용자 지정](machine-learning-data-science-customize-hadoop-cluster.md)을 참조하세요.
* hello 데이터가 Azure HDInsight Hadoop 클러스터에서 업로드 된 tooHive 테이블 되었습니다. 그렇지 않은 경우 hello 지침에 따라 [데이터 tooHive 테이블을 만들고 부하](machine-learning-data-science-move-hive-tables.md) tooupload 데이터 tooHive 먼저 테이블입니다.
* 원격 액세스 toohello 클러스터를 사용할 수 있습니다. 지침이 필요한 경우 참조 [액세스 hello Hadoop 클러스터의 헤드 노드](machine-learning-data-science-customize-hadoop-cluster.md#headnode)합니다.
* 방법에 대 한 지침이 필요한 경우 toosubmit 하이브 쿼리에서 참조 [어떻게 tooSubmit 하이브 쿼리](machine-learning-data-science-move-hive-tables.md#submit)

## <a name="example-hive-query-scripts-for-data-exploration"></a>데이터 탐색에 대한 예제 Hive 쿼리 스크립트
1. 파티션당 관찰 hello 개수`SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`
2. 하루 관찰 hello 개수`SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`
3. 범주 열에서 hello 수준을 가져오려면  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. 두 개의 범주 열 조합에 수준의 hello 수 가져오기`SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`
5. 숫자 열에 대 한 hello 분포 가져오기  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. 두 조인 테이블의 레코드 추출
   
        SELECT
            a.<common_columnname1> as <new_name1>,
            a.<common_columnname2> as <new_name2>,
            a.<a_column_name1> as <new_name3>,
            a.<a_column_name2> as <new_name4>,
            b.<b_column_name1> as <new_name5>,
            b.<b_column_name2> as <new_name6>
        FROM
            (
            SELECT <common_columnname1>,
                <common_columnname2>,
                <a_column_name1>,
                <a_column_name2>,
            FROM <databasename>.<tablename1>
            ) a
            join
            (
            SELECT <common_columnname1>,
                <common_columnname2>,
                <b_column_name1>,
                <b_column_name2>,
            FROM <databasename>.<tablename2>
            ) b
            ON a.<common_columnname1>=b.<common_columnname1> and a.<common_columnname2>=b.<common_columnname2>

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a>택시 여정 데이터 시나리오에 대한 추가 쿼리 스크립트
너무 관련 된 쿼리 예제[NYC 택시 여행 데이터](http://chriswhong.com/open-data/foil_nyc_taxi/) 시나리오에도 제공 되어 [GitHub 리포지토리](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts)합니다. 이러한 쿼리 이미 지정 된 데이터 스키마 않으며 제출 준비 toobe toorun 합니다.

