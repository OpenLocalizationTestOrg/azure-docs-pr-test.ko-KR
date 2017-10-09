---
title: "PySpark 및 Scala를 사용 하 여 Azure에서 aaaHDInsight Spark 연습 | Microsoft Docs"
description: "Hello 안내는 hello 팀 데이터 과학 프로세스의 예제는 Azure HDInsight Spark toodo 예측 분석에 PySpark 및 Scala 사용 합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev
ms.openlocfilehash: f8b41a8cae414586570761ba4b4eb4c239cbb981
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="hdinsight-spark-data-science-walkthroughs-using-pyspark-and-scala-on-azure"></a>Azure에서 PySpark 및 Scala를 사용하여 HDInsight Spark 데이터 과학 연습

이 연습에서는 PySpark 및 Scala Azure Spark 클러스터 toodo 예측 분석에 사용합니다. Hello 팀 데이터 과학 프로세스에에서 설명 된 hello 단계를 따릅니다. Hello 팀 데이터 과학 프로세스의 개요를 참조 하십시오. [데이터 과학 프로세스](data-science-process-overview.md)합니다. HDInsight의 Spark의 개요를 참조 하십시오. [HDInsight의 소개 tooSpark](../hdinsight/hdinsight-apache-spark-overview.md)합니다.

Hello 팀 데이터 과학 프로세스를 실행 하는 추가 데이터 과학 연습 hello 별로 그룹화 되어 **플랫폼** 사용 하는 합니다. 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]

## <a name="predict-taxi-tips-using-pyspark-on-azure-spark"></a>Azure Spark에서 PySpark를 사용하여 택시 팁 예측

hello [Azure HDInsight의 Spark를 사용 하 여](machine-learning-data-science-spark-overview.md) 팁은 지불 하 고 hello 범위 포함 된 유료 toobe 예상 여부 연습에서는 뉴욕 택시 toopredict에서 데이터를 사용 합니다. Hello 팀 데이터 과학 프로세스를 사용 하는 시나리오에서 사용 하 여 프로그램 [Azure HDInsight Spark 클러스터](https://azure.microsoft.com/services/hdinsight/) toostore, 탐색 및 기능 hello 공개적으로 사용할 수 있는 NYC 택시 여정에서 엔지니어 데이터 및 데이터 집합이 있어 합니다. 이 개요 항목 설정 하면 HDInsight Spark 클러스터 및 hello Jupyter PySpark 전자 필기장 hello 연습의 나머지 부분 hello에에서 사용 합니다. 표시 하는 이러한 전자 필기장 tooexplore 데이터와 다음 방법을 toocreate 및 모델을 사용 합니다. 고급 데이터 탐색 및 노트북 표시 방법을 모델링 하는 hello tooinclude 교차 유효성 검사, 하이퍼 매개 변수 비우기 및 모델 평가 합니다.

### <a name="data-exploration-and-modeling-with-spark"></a>Spark로 데이터 탐색 및 모델링 
Hello 데이터 집합을 탐색 하 고, 점수를 만들고 hello 통해 작업 하 여 hello 기계 학습 모델을 평가 [hello Spark MLlib toolkit으로 데이터에 대 한 이진 분류 및 회귀 모델을 만들](machine-learning-data-science-spark-data-exploration-modeling.md) 항목입니다.

### <a name="model-consumption"></a>모델 사용
toolearn tooscore hello 분류 및 회귀 모델은이 항목에서 생성 하는 방법 참조 [점수 Spark 작성 기계 학습 모델을 평가 하 고](machine-learning-data-science-spark-model-consumption.md)합니다.

### <a name="cross-validation-and-hyperparameter-sweeping"></a>교차 유효성 검사 및 하이퍼 매개 변수 비우기
교차 유효성 검사 및 하이퍼 매개 변수 비우기를 사용하여 모델을 학습하는 방법은 [Spark로 고급 데이터 탐색 및 모델링](machine-learning-data-science-spark-advanced-data-exploration-modeling.md)을 참조하세요.


## <a name="predict-taxi-tips-using-scala-on-azure-spark"></a>Azure Spark에서 Scala를 사용하여 택시 팁 예측

hello [Azure의 Spark와 함께 사용 하 여 Scala](machine-learning-data-science-process-scala-walkthrough.md) 팁은 지불 하 고 hello 범위 포함 된 유료 toobe 예상 여부 연습에서는 뉴욕 택시 toopredict에서 데이터를 사용 합니다. Azure HDInsight Spark 클러스터에서 toouse Scala hello Spark 시스템 학습 라이브러리 (MLlib) 및 SparkML 감독 된 기계 학습 작업에 대 한 패키지 하는 방법을 보여 줍니다. Hello를 구성 하는 hello 작업 안내 합니다 [데이터 과학 프로세스](http://aka.ms/datascienceprocess): 데이터를 수집 하 고 탐색, 시각화, 기능 엔지니어링, 모델링 및 모델 소비 합니다. 작성 된 hello 모델에 물류 및 선형 회귀, 임의 포리스트 및 그라데이션 승격 된 트리에 포함 됩니다.


## <a name="next-steps"></a>다음 단계

Hello 팀 데이터 과학 프로세스를 구성 하는 hello 주요 구성 요소의 논의 알려면 [팀 데이터 과학 프로세스 개요](data-science-process-overview.md)합니다.

데이터 과학 프로젝트, 참조에 대 한 설명은 한 toostructure를 사용할 수 있는 hello 팀 데이터 과학 프로세스 수명 주기 [팀 데이터 과학 프로세스 수명 주기](data-science-process-lifecycle.md)합니다. hello 수명 주기에서 다음에 나오는 프로젝트 일반적으로 실행 될 때 시작 toofinish hello 단계를 간략하게 설명 합니다. 

