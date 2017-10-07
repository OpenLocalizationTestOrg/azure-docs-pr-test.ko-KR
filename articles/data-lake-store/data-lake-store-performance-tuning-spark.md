---
title: "데이터 레이크 저장소 Spark 성능 튜닝 지침 aaaAzure | Microsoft Docs"
description: "Azure Data Lake Store Spark 성능 조정 지침"
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: stewu
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/19/2016
ms.author: stewu
ms.openlocfilehash: da1d172e9cb1199ad95605ea1718e78559f79650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-spark-on-hdinsight-and-azure-data-lake-store"></a>HDInsight의 Spark 및 Azure Data Lake Store에 대한 성능 조정 지침

Spark에 성능을 조정 하는 경우에 클러스터에서 실행 되는 앱의 tooconsider hello 번호가 필요 합니다.  기본적으로 4를 실행할 수 있습니다 HDI 클러스터에서 동시에 응용 프로그램 (참고: hello 기본 설정은 주체 toochange입니다).  Hello 기본 설정을 무시 하 고 hello 클러스터 중 해당 앱에 사용할 수 있도록 더 적은 앱 toouse을 결정할 수 있습니다.  

## <a name="prerequisites"></a>필수 조건

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.
* **Azure 데이터 레이크 저장소 계정**. 방법에 대 한 지침은 toocreate 하나, 참조 [Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)
* **Azure HDInsight 클러스터** 액세스 tooa 데이터 레이크 저장소 계정 사용 합니다. [Data Lake Store가 있는 HDInsight 클러스터 만들기](data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요. Hello 클러스터에 대 한 원격 데스크톱을 사용 해야 합니다.
* **Azure Data Lake Store에서 실행 중인 Spark 클러스터**.  자세한 내용은 참조 [데이터 레이크 저장소에서 사용 하 여 HDInsight Spark 클러스터 tooanalyze 데이터](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-use-with-data-lake-store)
* **ADLS에서 성능 조정 지침**.  일반적인 성능 개념은 [Data Lake Store 성능 조정 지침](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)을 참조하세요. 

## <a name="parameters"></a>매개 변수

Spark 작업을 실행할 때 ADLS에서 조정 된 tooincrease 성능을 일 수 있는 hello 가장 중요 한 설정을 다음과 같습니다.

* **Num executor** -hello 실행 될 수 있는 동시 작업 수입니다.

* **Executor 메모리** -hello 할당 된 메모리 양이 tooeach 실행자입니다.

* **Executor 코어** -코어 수가 hello tooeach executor를 할당 합니다.                     

**Num executor** Num executor hello 병렬로 실행할 수 있는 작업의 최대 수를 설정 합니다.  동시에 실행할 수 있는 작업의 실제 수 hello hello 메모리 및 CPU 리소스를 클러스터에서 사용할 수 있는으로 제한 됩니다.

**Executor 메모리** hello tooeach 실행자 할당 되는 메모리 양입니다.  각 실행 기에 필요한 hello 메모리 hello 작업에 따라 달라 집니다.  복잡 한 작업에 대 한 hello 메모리에 더 높은 toobe가 필요합니다.  읽기 및 쓰기와 같은 간단한 작업의 경우 메모리 요구 사항은 낮습니다.  각 실행 기에 대 한 메모리 양이 hello Ambari에서 볼 수 있습니다.  Ambari를 tooSpark 이동한 hello Configs 탭을 표시 합니다.  

**Executor 코어** hello 실행자 당 실행 될 수 있는 병렬 스레드 수를 결정 하는 실행자 당 사용 되는 코어 hello 양을 설정 합니다.  예를 들어 경우 실행자 코어 = 2, 각 실행자 hello 실행자에 2 병렬 작업을 실행할 수 있습니다.  hello 실행자 코어 hello 작업에 종속 됩니다 필요 합니다.  I/O가 많은 작업에는 태스크당 큰 메모리가 필요하지 않으므로 각 실행기에서 더 많은 병렬 태스크를 처리할 수 있습니다.

기본적으로 HDInsight에서 Spark를 실행할 때 각 물리적 코어에 대해 2개의 가상 YARN 코어가 정의됩니다.  이 값은 여러 스레드에서 동시성 및 컨텍스트 전환 횟수 간에 적절한 균형을 제공합니다.  

## <a name="guidance"></a>지침

Spark 데이터 레이크 저장소에서 데이터를 분석 워크 로드 toowork 실행 하면서 데이터 레이크 저장소와 hello 가장 최근의 HDInsight 버전 tooget hello 최상의 성능을 사용 하는 것이 좋습니다. 더 많은 I/O 사용량이 작업을 사용 하는 경우 특정 매개 변수에서 구성 된 tooimprove 성능 될 수 있습니다.  Azure Data Lake Store는 높은 처리량을 처리할 수 있는 확장성 높은 저장소 플랫폼입니다.  Hello 작업 주로으로 구성 된 경우 읽기 또는 쓰기 다음 Azure 데이터 레이크 저장소에서 I/O tooand에 대 한 동시성을 늘려 성능을 향상 시킬 수 없습니다.

I/O 집약적인 작업에 대 한 몇 가지 일반적인 방법으로 tooincrease 동시성 가지가 있습니다.

**1 단계: 클러스터에서 실행 되는 응용 프로그램과 확인** – hello 현재 항목을 포함 하 여 hello 클러스터에서 실행 중인 응용 프로그램과 알고 있어야 합니다.  hello 기본값 설정은 날짜가 각 Spark에 대 한 4에서는 동시에 실행 되는 앱입니다.  따라서 각 앱에 사용할 수 있는 hello 클러스터의 25%만 해야 합니다.  tooget 더 나은 성능을 executor hello 수를 변경 하 여 hello 기본값을 재정의할 수 있습니다.  

**2 단계: 실행자 메모리 설정** – hello tooset hello 실행자 메모리를가 하는 것입니다.  hello 메모리 하락 toorun는 hello 작업에 종속 됩니다.  실행기당 메모리 할당량을 줄여 동시성을 높일 수 있습니다.  메모리 부족 예외가 표시 작업을 실행 하는 경우이 매개 변수에 대 한 hello 값을 늘리십시오 해야 합니다.  하나의 대체에서는 tooget 메모리가 더 높은 양의 메모리를 갖고 있는 클러스터를 사용 하 여 클러스터의 hello 크기 증가 합니다.  더 많은 메모리를 더 많은 executor toobe을 사용 하는 더 많은 동시성 의미를 사용 하 고 있습니다.

**3 단계: 설정 실행자 코어** – I/O가 많은 작업용 복잡 하 고 작업을 갖지 않는, 것이 좋은 toostart 실행자 당 병렬 태스크 수가 tooincrease hello 실행자 코어 수가 높은 합니다.  Executor 코어 too4 설정은 좋은 시작 합니다.   

    executor-cores = 4
Hello 실행자 코어 수를 늘리면 됩니다 제공 많은 병렬 처리 하므로 다른 실행자 코어를 테스트할 수 있습니다.  보다 복잡 한 작업 인 작업은, 실행자 당 코어 수가 hello 줄여야 합니다.  executor-cores가 4보다 높게 설정된 경우 가비지 수집이 부족하여 성능이 저하될 수 있습니다.

**4단계: 클러스터에서 YARN 메모리 양 결정** – 이 정보는 Ambari에서 제공됩니다.  TooYARN를 탐색 하 고 hello Configs 탭을 표시 합니다.  hello YARN 메모리가이 창에 표시 됩니다.  
참고: hello 창에 있는 동안 참고할 수 있습니다 hello 기본 YARN 컨테이너 크기입니다.  hello YARN 컨테이너 크기 실행자 매개 변수가 당 메모리와 동일 hello 됩니다.

    Total YARN memory = nodes * YARN memory per node
**5단계: num-executors 계산**

**메모리 제약 조건 계산** -hello num executor 매개 변수는 메모리 또는 CPU 제한 됩니다.  hello 메모리 제약 조건은 hello 응용 프로그램에 대 한 사용 가능한 YARN 메모리 양으로 결정 됩니다.  총 YARN 메모리를 가져와 executor-memory로 나눕니다.  hello 제약 조건 해제 되므로 앱 hello 수로 나눕니다 hello 수의 앱에 대 한 크기가 조정 toobe가 필요 합니다.

    Memory constraint = (total YARN memory / executor memory) / # of apps   
**CPU 제약 조건 계산** -hello CPU 제약 조건이 hello 총 가상 코어 hello 실행자 당 코어 수로 나눈 값으로 계산 됩니다.  각 물리적 코어당 2개의 가상 코어가 있습니다.  비슷한 toohello 메모리 제약 조건, 응용 프로그램의 hello 번호로 나누기를 한 있습니다.

    virtual cores = (nodes in cluster * # of physical cores in node * 2)
    CPU constraint = (total virtual cores / # of cores per executor) / # of apps
**Num executor 설정** – hello num executor 매개 변수 hello 메모리 제약 조건 및 제약 조건 hello CPU의 최소 hello을 수행 하 여 결정 됩니다. 

    num-executors = Min (total virtual Cores / # of cores per executor, available YARN memory / executor-memory)   
num-executors 수를 높게 설정한다고 성능이 반드시 향상되는 것은 아닙니다.  더 많은 실행기를 추가하면 각 실행기당 오버헤드가 더 추가되며 이로 인해 성능이 저하될 수 있다는 것을 고려해야 합니다.  Num executor hello 클러스터 리소스에 의해 제한 됩니다.    

## <a name="example-calculation"></a>계산 예

실행 중인 2 앱 hello를 포함 한 보아야 toorun 하는 클러스터 D4v2 8 개의 노드로 구성에 현재 있는 경우를 가정해 봅니다.  

**1 단계: 클러스터에서 실행 되는 응용 프로그램과 확인** – 2 있는지 알고 hello toorun 보아야 하나를 포함 하 여 클러스터에는 앱입니다.  

**2단계: executor-memory 설정** – 이 예의 경우 I/O 집약적인 작업에 대해 6GB의 실행기 메모리면 충분하다고 결정합니다.  

    executor-memory = 6GB
**3 단계: 설정 실행자 코어** – I/O 집약적인 작업 이므로, 각 실행자 too4에 대 한 코어의 hello 수 설정할 수 있습니다.  4 가비지 컬렉션 문제를 일으킬 수 있는 보다 실행자 toolarger 당 코어를 설정 합니다.  

    executor-cores = 4
**4 단계: 클러스터의 YARN 메모리 양을 결정** – 각 D4v2 25GB의 YARN 메모리에 out tooAmbari toofind 이동 했습니다.  8 개의 노드로 구성 되므로 hello YARN 메모리가 8에 곱합니다.

    Total YARN memory = nodes * YARN memory* per node
    Total YARN memory = 8 nodes * 25GB = 200GB
**5 단계: 계산 num executor** – hello num executor 매개 변수 hello 메모리 제약 조건 및 hello CPU 제약 조건 hello로 나눈 값의 최소 hello을 수행 하 여 결정 됩니다 # of Spark에서 실행 되는 앱입니다.    

**메모리 제약 조건 계산** – hello 메모리 제약 조건은 hello 총 YARN 메모리 실행자 당 hello 메모리로 나눈 값으로 계산 됩니다.

    Memory constraint = (total YARN memory / executor memory) / # of apps   
    Memory constraint = (200GB / 6GB) / 2   
    Memory constraint = 16 (rounded)
**CPU 제약 조건 계산** -hello CPU 제약 조건이 hello 총 yarn 코어 hello 실행자 당 코어 수로 나눈 값으로 계산 됩니다.
    
    YARN cores = nodes in cluster * # of cores per node * 2   
    YARN cores = 8 nodes * 8 cores per D14 * 2 = 128
    CPU constraint = (total YARN cores / # of cores per executor) / # of apps
    CPU constraint = (128 / 4) / 2
    CPU constraint = 16
**num-executors 설정**

    num-executors = Min (memory constraint, CPU constraint)
    num-executors = Min (16, 16)
    num-executors = 16    

