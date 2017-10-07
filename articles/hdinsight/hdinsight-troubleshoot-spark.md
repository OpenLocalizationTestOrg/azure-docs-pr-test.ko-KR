---
title: "Azure HDInsight를 사용 하 여 Spark aaaTroubleshoot | Microsoft Docs"
description: "Apache Spark와 Azure HDInsight 작업에 대 한 toocommon 질문을 답변을 가져옵니다."
keywords: "Azure HDInsight, Spark, FAQ, 문제 해결 가이드, 일반적인 문제, 응용 프로그램 구성, Ambari"
services: Azure HDInsight
documentationcenter: na
author: arijitt
manager: 
editor: 
ms.assetid: 25D89586-DE5B-4268-B5D5-CC2CE12207ED
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: arijitt
ms.openlocfilehash: c9f910daf295462238a3143ae2589db6d383097f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-spark-by-using-azure-hdinsight"></a>Azure HDInsight를 사용한 Spark 문제 해결

Apache Ambari에 Apache Spark 페이로드를 작업할 때 hello 상위 문제와 그 해결 방법에 알아봅니다.

## <a name="how-do-i-configure-a-spark-application-by-using-ambari-on-clusters"></a>클러스터에서 Ambari를 사용하여 Spark 응용 프로그램을 구성하는 방법

### <a name="resolution-steps"></a>해결 단계:

이 절차에 대 한 구성 값 hello HDInsight에서 이전에 설정 되었습니다. Spark 구성을 toobe 집합과 toowhat 값이 필요한 toodetermine 참조 [Spark는 응용 프로그램 OutofMemoryError 예외를 발생 어떤](#what-causes-a-spark-application-outofmemoryerror-exception)합니다. 

1. 클러스터의 hello 목록에서 선택 **Spark2**합니다.

    ![목록에서 클러스터 선택](media/hdinsight-troubleshoot-spark/update-config-1.png)

2. 선택 hello **Configs** 탭 합니다.

    ![Hello Configs 탭 선택](media/hdinsight-troubleshoot-spark/update-config-2.png)

3. 구성의 hello 목록에서 선택 **Custom spark2 기본값**합니다.

    ![custom-spark-defaults 선택](media/hdinsight-troubleshoot-spark/update-config-3.png)

4. 같은 tooadjust, 필요를 설정 하는 hello 값 찾기 위해 **spark.executor.memory**합니다. 이 경우의 값을 hello **4608 m** 너무 높습니다.

    ![Hello spark.executor.memory 필드 선택](media/hdinsight-troubleshoot-spark/update-config-4.png)

5. 집합 hello 값 toohello 권장 설정입니다. 값 hello **2048 m** 이 설정에 대 한 것이 좋습니다.

    ![변경 값 too2048m](media/hdinsight-troubleshoot-spark/update-config-5.png)

6. Hello 값을 저장 하 고 hello 구성을 저장 합니다. Hello 도구 모음에서 선택 **저장**합니다.

    ![Hello 경고 메시지를 구성](media/hdinsight-troubleshoot-spark/update-config-6a.png)

    주의할 필요가 있는 구성이면 알림이 표시됩니다. Hello 항목을 확인 한 후 선택 **그래도 계속**합니다. 

    ![계속 진행 선택](media/hdinsight-troubleshoot-spark/update-config-6b.png)

    Hello 구성 변경에 대 한 메모를 작성 한 다음 선택 **저장**합니다.

    ![Hello 변경에 대 한 메모를 입력 합니다.](media/hdinsight-troubleshoot-spark/update-config-6c.png)

7. 구성을 저장 될 때마다 메시지가 표시 되 toorestart hello 서비스입니다. **다시 시작**을 선택합니다.

    ![다시 시작 선택](media/hdinsight-troubleshoot-spark/update-config-7a.png)

    Hello를 다시 시작을 확인 합니다.

    ![다시 시작 확인 선택](media/hdinsight-troubleshoot-spark/update-config-7b.png)

    Hello 실행 중인 프로세스를 검토할 수 있습니다.

    ![실행 중인 프로세스 검토](media/hdinsight-troubleshoot-spark/update-config-7c.png)

8. 구성을 추가할 수 있습니다. 구성의 hello 목록에서 선택 **Custom spark2 기본값**를 선택한 후 **속성 추가**합니다.

    ![속성 추가 선택](media/hdinsight-troubleshoot-spark/update-config-8.png)

9. 새 속성을 정의합니다. Hello 데이터 형식과 같은 특정 설정에 대 한 대화 상자를 사용 하 여 단일 속성을 정의할 수 있습니다. 또는 줄당 하나의 정의를 사용하여 여러 속성을 정의할 수 있습니다. 

    이 예제에서는 hello **spark.driver.memory** 속성의 값으로 정의 된 **4g**합니다.

    ![새 속성 정의](media/hdinsight-troubleshoot-spark/update-config-9.png)

10. Hello 구성을 저장 하 고 6-7 단계에 설명 된 대로 hello 서비스를 다시 시작 합니다.

이러한 변경 내용은 클러스터 전체 있더라도 hello Spark 작업을 제출 하는 경우에 재정의 될 수 있습니다.

### <a name="additional-reading"></a>추가 참조 자료

[HDInsight 클러스터에서 Spark 작업 제출(영문)](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-a-jupyter-notebook-on-clusters"></a>클러스터에서 Jupyter Notebook을 사용하여 Spark 응용 프로그램을 구성하는 방법

### <a name="resolution-steps"></a>해결 단계:

1. Spark 구성을 toobe 집합과 toowhat 값이 필요한 toodetermine 참조 [Spark는 응용 프로그램 OutofMemoryError 예외를 발생 어떤](#what-causes-a-spark-application-outofmemoryerror-exception)합니다.

2. Hello hello 후 hello Jupyter 노트북의 첫 번째 셀에 **% % 구성** 지시문을 올바른 JSON 형식에 있는 hello Spark 구성을 지정 합니다. 필요에 따라 hello 실제 값을 변경 합니다.

    ![구성 추가](media/hdinsight-troubleshoot-spark/add-configuration-cell.png)

### <a name="additional-reading"></a>추가 참조 자료

[HDInsight 클러스터에서 Spark 작업 제출(영문)](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-livy-on-clusters"></a>클러스터에서 Livy를 사용하여 Spark 응용 프로그램을 구성하는 방법

### <a name="resolution-steps"></a>해결 단계:

1. Spark 구성을 toobe 집합과 toowhat 값이 필요한 toodetermine 참조 [Spark는 응용 프로그램 OutofMemoryError 예외를 발생 어떤](#what-causes-a-spark-application-outofmemoryerror-exception)합니다. 

2. CURL 같은 REST 클라이언트를 사용 하 여 hello Spark 응용 프로그램 tooLivy를 제출 합니다. 명령 비슷한 toohello 다음을 사용 합니다. 필요에 따라 hello 실제 값을 변경 합니다.

    ```apache
    curl -k --user 'username:password' -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://container@storageaccountname.blob.core.windows.net/example/jars/sparkapplication.jar", "className":"com.microsoft.spark.application", "numExecutors":4, "executorMemory":"4g", "executorCores":2, "driverMemory":"8g", "driverCores":4}'  
    ```

### <a name="additional-reading"></a>추가 참조 자료

[HDInsight 클러스터에서 Spark 작업 제출(영문)](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-spark-submit-on-clusters"></a>클러스터에서 spark-submit을 사용하여 Spark 응용 프로그램을 구성하는 방법

### <a name="resolution-steps"></a>해결 단계:

1. Spark 구성을 toobe 집합과 toowhat 값이 필요한 toodetermine 참조 [Spark는 응용 프로그램 OutofMemoryError 예외를 발생 어떤](#what-causes-a-spark-application-outofmemoryerror-exception)합니다.

2. Spark 셸 명령을 비슷한 toohello 다음을 사용 하 여 시작 합니다. 필요에 따라 hello hello 구성의 실제 값을 변경 합니다. 

    ```apache
    spark-submit --master yarn-cluster --class com.microsoft.spark.application --num-executors 4 --executor-memory 4g --executor-cores 2 --driver-memory 8g --driver-cores 4 /home/user/spark/sparkapplication.jar
    ```

### <a name="additional-reading"></a>추가 참조 자료

[HDInsight 클러스터에서 Spark 작업 제출(영문)](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="what-causes-a-spark-application-outofmemoryerror-exception"></a>Spark 응용 프로그램 OutofMemoryError 예외를 발생시키는 원인

### <a name="detailed-description"></a>자세한 설명

hello Spark 응용 프로그램 종류의 예외를 확인할 수 없는 다음 hello로 실패 합니다.

```apache
ERROR Executor: Exception in task 7.0 in stage 6.0 (TID 439) 

java.lang.OutOfMemoryError 
    at java.io.ByteArrayOutputStream.hugeCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.grow(Unknown Source) 
    at java.io.ByteArrayOutputStream.ensureCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.write(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.drain(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.setBlockDataMode(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject0(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject(Unknown Source) 
    at org.apache.spark.serializer.JavaSerializationStream.writeObject(JavaSerializer.scala:44) 
    at org.apache.spark.serializer.JavaSerializerInstance.serialize(JavaSerializer.scala:101) 
    at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:239) 
    at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source) 
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source) 
    at java.lang.Thread.run(Unknown Source) 
```

```apache
ERROR SparkUncaughtExceptionHandler: Uncaught exception in thread Thread[Executor task launch worker-0,5,main] 

java.lang.OutOfMemoryError 
    at java.io.ByteArrayOutputStream.hugeCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.grow(Unknown Source) 
    at java.io.ByteArrayOutputStream.ensureCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.write(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.drain(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.setBlockDataMode(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject0(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject(Unknown Source) 
    at org.apache.spark.serializer.JavaSerializationStream.writeObject(JavaSerializer.scala:44) 
    at org.apache.spark.serializer.JavaSerializerInstance.serialize(JavaSerializer.scala:101) 
    at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:239) 
    at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source) 
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source) 
    at java.lang.Thread.run(Unknown Source) 
```

### <a name="probable-cause"></a>가능한 원인:

힙 메모리 부족 toohello Java 가상 컴퓨터 (Jvm)가 할당 되는 하는 hello 가장 가능성이 높은이 예외가 발생 합니다. 이러한 Jvm hello Spark 응용 프로그램의 일부로 단일 실행 또는 드라이버 시작 됩니다. 

### <a name="resolution-steps"></a>해결 단계:

1. Hello hello 데이터 hello Spark 응용 프로그램 핸들의 최대 크기를 결정 합니다. Hello hello 입력된 데이터를 hello 입력된 데이터 및 hello 응용 프로그램은 hello 중간 데이터 변환을 추가 하는 경우 생성 되는 hello 출력 데이터를 변환 하 여 생성 되는 hello 중간 데이터의 최대 크기에 따라 추측 값을 만들 수 있습니다. 초기에 공식적으로 추측할 수 없는 경우 이 프로세스를 반복할 수 있습니다. 

2. 해당 hello HDInsight 클러스터 toouse에 메모리 및 코어 tooaccommodate hello Spark 응용 프로그램의 관점에서 충분 한 리소스가 하실 거죠 있는지 확인 하십시오. Hello 값에 대 한 hello YARN UI의 hello 클러스터 메트릭 섹션을 확인 하 여이 확인할 수 있습니다의 **사용 메모리** vs. **Memory Total** 값, **VCores Used** 값과 **VCores Total** 값을 검토하여 이를 확인할 수 있습니다.

3. Spark 다음 hello hello 사용 가능한 메모리 및 코어의 90%를 초과 하면 안 되는 구성을 tooappropriate 값을 설정 합니다. hello 값 hello Spark 응용 프로그램의 hello 메모리 요구 사항에 있어야 합니다. 

    ```apache
    spark.executor.instances (Example: 8 for 8 executor count) 
    spark.executor.memory (Example: 4g for 4 GB) 
    spark.yarn.executor.memoryOverhead (Example: 384m for 384 MB) 
    spark.executor.cores (Example: 2 for 2 cores per executor) 
    spark.driver.memory (Example: 8g for 8GB) 
    spark.driver.cores (Example: 4 for 4 cores)   
    spark.yarn.driver.memoryOverhead (Example: 384m for 384MB) 
    ```

    hello 다음 명령을 실행 하는 모든 단일 실행에서 사용 하는 hello 총 메모리를 tooget: 
    
    ```apache
    spark.executor.instances * (spark.executor.memory + spark.yarn.executor.memoryOverhead) 
    ```
    hello 다음 명령을 실행 하는 hello 드라이버를 사용 하는 hello 총 메모리를 tooget:
    
    ```apache
    spark.driver.memory + spark.yarn.driver.memoryOverhead
    ```

### <a name="additional-reading"></a>추가 참조 자료

- [Spark 메모리 관리 개요(영문)](http://spark.apache.org/docs/latest/tuning.html#memory-management-overview)
- [HDInsight 클러스터에서 Spark 응용 프로그램 디버그](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/)

