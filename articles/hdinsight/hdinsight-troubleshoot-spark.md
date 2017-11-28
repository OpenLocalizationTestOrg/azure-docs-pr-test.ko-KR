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
# <a name="troubleshoot-spark-by-using-azure-hdinsight"></a><span data-ttu-id="c75c6-104">Azure HDInsight를 사용한 Spark 문제 해결</span><span class="sxs-lookup"><span data-stu-id="c75c6-104">Troubleshoot Spark by using Azure HDInsight</span></span>

<span data-ttu-id="c75c6-105">Apache Ambari에 Apache Spark 페이로드를 작업할 때 hello 상위 문제와 그 해결 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-105">Learn about hello top issues and their resolutions when working with Apache Spark payloads in Apache Ambari.</span></span>

## <a name="how-do-i-configure-a-spark-application-by-using-ambari-on-clusters"></a><span data-ttu-id="c75c6-106">클러스터에서 Ambari를 사용하여 Spark 응용 프로그램을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="c75c6-106">How do I configure a Spark application by using Ambari on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="c75c6-107">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="c75c6-107">Resolution steps</span></span>

<span data-ttu-id="c75c6-108">이 절차에 대 한 구성 값 hello HDInsight에서 이전에 설정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-108">hello configuration values for this procedure were previously set in HDInsight.</span></span> <span data-ttu-id="c75c6-109">Spark 구성을 toobe 집합과 toowhat 값이 필요한 toodetermine 참조 [Spark는 응용 프로그램 OutofMemoryError 예외를 발생 어떤](#what-causes-a-spark-application-outofmemoryerror-exception)합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-109">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

1. <span data-ttu-id="c75c6-110">클러스터의 hello 목록에서 선택 **Spark2**합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-110">In hello list of clusters, select **Spark2**.</span></span>

    ![목록에서 클러스터 선택](media/hdinsight-troubleshoot-spark/update-config-1.png)

2. <span data-ttu-id="c75c6-112">선택 hello **Configs** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-112">Select hello **Configs** tab.</span></span>

    ![Hello Configs 탭 선택](media/hdinsight-troubleshoot-spark/update-config-2.png)

3. <span data-ttu-id="c75c6-114">구성의 hello 목록에서 선택 **Custom spark2 기본값**합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-114">In hello list of configurations, select **Custom-spark2-defaults**.</span></span>

    ![custom-spark-defaults 선택](media/hdinsight-troubleshoot-spark/update-config-3.png)

4. <span data-ttu-id="c75c6-116">같은 tooadjust, 필요를 설정 하는 hello 값 찾기 위해 **spark.executor.memory**합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-116">Look for hello value setting that you need tooadjust, such as **spark.executor.memory**.</span></span> <span data-ttu-id="c75c6-117">이 경우의 값을 hello **4608 m** 너무 높습니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-117">In this case, hello value of **4608m** is too high.</span></span>

    ![Hello spark.executor.memory 필드 선택](media/hdinsight-troubleshoot-spark/update-config-4.png)

5. <span data-ttu-id="c75c6-119">집합 hello 값 toohello 권장 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-119">Set hello value toohello recommended setting.</span></span> <span data-ttu-id="c75c6-120">값 hello **2048 m** 이 설정에 대 한 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-120">hello value **2048m** is recommended for this setting.</span></span>

    ![변경 값 too2048m](media/hdinsight-troubleshoot-spark/update-config-5.png)

6. <span data-ttu-id="c75c6-122">Hello 값을 저장 하 고 hello 구성을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-122">Save hello value, and then save hello configuration.</span></span> <span data-ttu-id="c75c6-123">Hello 도구 모음에서 선택 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-123">On hello toolbar, select **Save**.</span></span>

    ![Hello 경고 메시지를 구성](media/hdinsight-troubleshoot-spark/update-config-6a.png)

    <span data-ttu-id="c75c6-125">주의할 필요가 있는 구성이면 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-125">You are notified if any configurations need attention.</span></span> <span data-ttu-id="c75c6-126">Hello 항목을 확인 한 후 선택 **그래도 계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-126">Note hello items, and then select **Proceed Anyway**.</span></span> 

    ![계속 진행 선택](media/hdinsight-troubleshoot-spark/update-config-6b.png)

    <span data-ttu-id="c75c6-128">Hello 구성 변경에 대 한 메모를 작성 한 다음 선택 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-128">Write a note about hello configuration changes, and then select **Save**.</span></span>

    ![Hello 변경에 대 한 메모를 입력 합니다.](media/hdinsight-troubleshoot-spark/update-config-6c.png)

7. <span data-ttu-id="c75c6-130">구성을 저장 될 때마다 메시지가 표시 되 toorestart hello 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-130">Whenever a configuration is saved, you are prompted toorestart hello service.</span></span> <span data-ttu-id="c75c6-131">**다시 시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-131">Select **Restart**.</span></span>

    ![다시 시작 선택](media/hdinsight-troubleshoot-spark/update-config-7a.png)

    <span data-ttu-id="c75c6-133">Hello를 다시 시작을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-133">Confirm hello restart.</span></span>

    ![다시 시작 확인 선택](media/hdinsight-troubleshoot-spark/update-config-7b.png)

    <span data-ttu-id="c75c6-135">Hello 실행 중인 프로세스를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-135">You can review hello processes that are running.</span></span>

    ![실행 중인 프로세스 검토](media/hdinsight-troubleshoot-spark/update-config-7c.png)

8. <span data-ttu-id="c75c6-137">구성을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-137">You can add configurations.</span></span> <span data-ttu-id="c75c6-138">구성의 hello 목록에서 선택 **Custom spark2 기본값**를 선택한 후 **속성 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-138">In hello list of configurations, select **Custom-spark2-defaults**, and then select **Add Property**.</span></span>

    ![속성 추가 선택](media/hdinsight-troubleshoot-spark/update-config-8.png)

9. <span data-ttu-id="c75c6-140">새 속성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-140">Define a new property.</span></span> <span data-ttu-id="c75c6-141">Hello 데이터 형식과 같은 특정 설정에 대 한 대화 상자를 사용 하 여 단일 속성을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-141">You can define a single property by using a dialog box for specific settings such as hello data type.</span></span> <span data-ttu-id="c75c6-142">또는 줄당 하나의 정의를 사용하여 여러 속성을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-142">Or, you can define multiple properties by using one definition per line.</span></span> 

    <span data-ttu-id="c75c6-143">이 예제에서는 hello **spark.driver.memory** 속성의 값으로 정의 된 **4g**합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-143">In this example, hello **spark.driver.memory** property is defined with a value of **4g**.</span></span>

    ![새 속성 정의](media/hdinsight-troubleshoot-spark/update-config-9.png)

10. <span data-ttu-id="c75c6-145">Hello 구성을 저장 하 고 6-7 단계에 설명 된 대로 hello 서비스를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-145">Save hello configuration, and then restart hello service as described in steps 6 and 7.</span></span>

<span data-ttu-id="c75c6-146">이러한 변경 내용은 클러스터 전체 있더라도 hello Spark 작업을 제출 하는 경우에 재정의 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-146">These changes are cluster-wide but can be overridden when you submit hello Spark job.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="c75c6-147">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="c75c6-147">Additional reading</span></span>

[<span data-ttu-id="c75c6-148">HDInsight 클러스터에서 Spark 작업 제출(영문)</span><span class="sxs-lookup"><span data-stu-id="c75c6-148">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-a-jupyter-notebook-on-clusters"></a><span data-ttu-id="c75c6-149">클러스터에서 Jupyter Notebook을 사용하여 Spark 응용 프로그램을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="c75c6-149">How do I configure a Spark application by using a Jupyter notebook on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="c75c6-150">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="c75c6-150">Resolution steps</span></span>

1. <span data-ttu-id="c75c6-151">Spark 구성을 toobe 집합과 toowhat 값이 필요한 toodetermine 참조 [Spark는 응용 프로그램 OutofMemoryError 예외를 발생 어떤](#what-causes-a-spark-application-outofmemoryerror-exception)합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-151">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="c75c6-152">Hello hello 후 hello Jupyter 노트북의 첫 번째 셀에 **% % 구성** 지시문을 올바른 JSON 형식에 있는 hello Spark 구성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-152">In hello first cell of hello Jupyter notebook, after hello **%%configure** directive, specify hello Spark configurations in valid JSON format.</span></span> <span data-ttu-id="c75c6-153">필요에 따라 hello 실제 값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-153">Change hello actual values as necessary:</span></span>

    ![구성 추가](media/hdinsight-troubleshoot-spark/add-configuration-cell.png)

### <a name="additional-reading"></a><span data-ttu-id="c75c6-155">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="c75c6-155">Additional reading</span></span>

[<span data-ttu-id="c75c6-156">HDInsight 클러스터에서 Spark 작업 제출(영문)</span><span class="sxs-lookup"><span data-stu-id="c75c6-156">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-livy-on-clusters"></a><span data-ttu-id="c75c6-157">클러스터에서 Livy를 사용하여 Spark 응용 프로그램을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="c75c6-157">How do I configure a Spark application by using Livy on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="c75c6-158">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="c75c6-158">Resolution steps</span></span>

1. <span data-ttu-id="c75c6-159">Spark 구성을 toobe 집합과 toowhat 값이 필요한 toodetermine 참조 [Spark는 응용 프로그램 OutofMemoryError 예외를 발생 어떤](#what-causes-a-spark-application-outofmemoryerror-exception)합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-159">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

2. <span data-ttu-id="c75c6-160">CURL 같은 REST 클라이언트를 사용 하 여 hello Spark 응용 프로그램 tooLivy를 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-160">Submit hello Spark application tooLivy by using a REST client like cURL.</span></span> <span data-ttu-id="c75c6-161">명령 비슷한 toohello 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-161">Use a command similar toohello following.</span></span> <span data-ttu-id="c75c6-162">필요에 따라 hello 실제 값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-162">Change hello actual values as necessary:</span></span>

    ```apache
    curl -k --user 'username:password' -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://container@storageaccountname.blob.core.windows.net/example/jars/sparkapplication.jar", "className":"com.microsoft.spark.application", "numExecutors":4, "executorMemory":"4g", "executorCores":2, "driverMemory":"8g", "driverCores":4}'  
    ```

### <a name="additional-reading"></a><span data-ttu-id="c75c6-163">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="c75c6-163">Additional reading</span></span>

[<span data-ttu-id="c75c6-164">HDInsight 클러스터에서 Spark 작업 제출(영문)</span><span class="sxs-lookup"><span data-stu-id="c75c6-164">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-spark-submit-on-clusters"></a><span data-ttu-id="c75c6-165">클러스터에서 spark-submit을 사용하여 Spark 응용 프로그램을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="c75c6-165">How do I configure a Spark application by using spark-submit on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="c75c6-166">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="c75c6-166">Resolution steps</span></span>

1. <span data-ttu-id="c75c6-167">Spark 구성을 toobe 집합과 toowhat 값이 필요한 toodetermine 참조 [Spark는 응용 프로그램 OutofMemoryError 예외를 발생 어떤](#what-causes-a-spark-application-outofmemoryerror-exception)합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-167">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="c75c6-168">Spark 셸 명령을 비슷한 toohello 다음을 사용 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-168">Launch spark-shell by using a command similar toohello following.</span></span> <span data-ttu-id="c75c6-169">필요에 따라 hello hello 구성의 실제 값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-169">Change hello actual value of hello configurations as necessary:</span></span> 

    ```apache
    spark-submit --master yarn-cluster --class com.microsoft.spark.application --num-executors 4 --executor-memory 4g --executor-cores 2 --driver-memory 8g --driver-cores 4 /home/user/spark/sparkapplication.jar
    ```

### <a name="additional-reading"></a><span data-ttu-id="c75c6-170">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="c75c6-170">Additional reading</span></span>

[<span data-ttu-id="c75c6-171">HDInsight 클러스터에서 Spark 작업 제출(영문)</span><span class="sxs-lookup"><span data-stu-id="c75c6-171">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="what-causes-a-spark-application-outofmemoryerror-exception"></a><span data-ttu-id="c75c6-172">Spark 응용 프로그램 OutofMemoryError 예외를 발생시키는 원인</span><span class="sxs-lookup"><span data-stu-id="c75c6-172">What causes a Spark application OutofMemoryError exception</span></span>

### <a name="detailed-description"></a><span data-ttu-id="c75c6-173">자세한 설명</span><span class="sxs-lookup"><span data-stu-id="c75c6-173">Detailed description</span></span>

<span data-ttu-id="c75c6-174">hello Spark 응용 프로그램 종류의 예외를 확인할 수 없는 다음 hello로 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-174">hello Spark application fails, with hello following types of uncaught exceptions:</span></span>

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

### <a name="probable-cause"></a><span data-ttu-id="c75c6-175">가능한 원인:</span><span class="sxs-lookup"><span data-stu-id="c75c6-175">Probable cause</span></span>

<span data-ttu-id="c75c6-176">힙 메모리 부족 toohello Java 가상 컴퓨터 (Jvm)가 할당 되는 하는 hello 가장 가능성이 높은이 예외가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-176">hello most likely cause of this exception is that not enough heap memory is allocated toohello Java virtual machines (JVMs).</span></span> <span data-ttu-id="c75c6-177">이러한 Jvm hello Spark 응용 프로그램의 일부로 단일 실행 또는 드라이버 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-177">These JVMs are launched as executors or drivers as part of hello Spark application.</span></span> 

### <a name="resolution-steps"></a><span data-ttu-id="c75c6-178">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="c75c6-178">Resolution steps</span></span>

1. <span data-ttu-id="c75c6-179">Hello hello 데이터 hello Spark 응용 프로그램 핸들의 최대 크기를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-179">Determine hello maximum size of hello data hello Spark application handles.</span></span> <span data-ttu-id="c75c6-180">Hello hello 입력된 데이터를 hello 입력된 데이터 및 hello 응용 프로그램은 hello 중간 데이터 변환을 추가 하는 경우 생성 되는 hello 출력 데이터를 변환 하 여 생성 되는 hello 중간 데이터의 최대 크기에 따라 추측 값을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-180">You can make a guess based on hello maximum size of hello input data, hello intermediate data that's produced by transforming hello input data, and hello output data that's produced when hello application is further transforming hello intermediate data.</span></span> <span data-ttu-id="c75c6-181">초기에 공식적으로 추측할 수 없는 경우 이 프로세스를 반복할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-181">This process can be an iterative if you can't make an initial formal guess.</span></span> 

2. <span data-ttu-id="c75c6-182">해당 hello HDInsight 클러스터 toouse에 메모리 및 코어 tooaccommodate hello Spark 응용 프로그램의 관점에서 충분 한 리소스가 하실 거죠 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c75c6-182">Make sure that hello HDInsight cluster that you're going toouse has enough resources in terms of memory and cores tooaccommodate hello Spark application.</span></span> <span data-ttu-id="c75c6-183">Hello 값에 대 한 hello YARN UI의 hello 클러스터 메트릭 섹션을 확인 하 여이 확인할 수 있습니다의 **사용 메모리** vs. **Memory Total** 값, **VCores Used** 값과 **VCores Total** 값을 검토하여 이를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-183">You can determine this by viewing hello cluster metrics section of hello YARN UI for hello values of **Memory Used** vs. **Memory Total**, and **VCores Used** vs. **VCores Total**.</span></span>

3. <span data-ttu-id="c75c6-184">Spark 다음 hello hello 사용 가능한 메모리 및 코어의 90%를 초과 하면 안 되는 구성을 tooappropriate 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-184">Set hello following Spark configurations tooappropriate values, which should not exceed 90% of hello available memory and cores.</span></span> <span data-ttu-id="c75c6-185">hello 값 hello Spark 응용 프로그램의 hello 메모리 요구 사항에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c75c6-185">hello values should be well within hello memory requirements of hello Spark application:</span></span> 

    ```apache
    spark.executor.instances (Example: 8 for 8 executor count) 
    spark.executor.memory (Example: 4g for 4 GB) 
    spark.yarn.executor.memoryOverhead (Example: 384m for 384 MB) 
    spark.executor.cores (Example: 2 for 2 cores per executor) 
    spark.driver.memory (Example: 8g for 8GB) 
    spark.driver.cores (Example: 4 for 4 cores)   
    spark.yarn.driver.memoryOverhead (Example: 384m for 384MB) 
    ```

    <span data-ttu-id="c75c6-186">hello 다음 명령을 실행 하는 모든 단일 실행에서 사용 하는 hello 총 메모리를 tooget:</span><span class="sxs-lookup"><span data-stu-id="c75c6-186">tooget hello total memory used by all executors, run hello following command:</span></span> 
    
    ```apache
    spark.executor.instances * (spark.executor.memory + spark.yarn.executor.memoryOverhead) 
    ```
    <span data-ttu-id="c75c6-187">hello 다음 명령을 실행 하는 hello 드라이버를 사용 하는 hello 총 메모리를 tooget:</span><span class="sxs-lookup"><span data-stu-id="c75c6-187">tooget hello total memory used by hello driver, run hello following command:</span></span>
    
    ```apache
    spark.driver.memory + spark.yarn.driver.memoryOverhead
    ```

### <a name="additional-reading"></a><span data-ttu-id="c75c6-188">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="c75c6-188">Additional reading</span></span>

- [<span data-ttu-id="c75c6-189">Spark 메모리 관리 개요(영문)</span><span class="sxs-lookup"><span data-stu-id="c75c6-189">Spark memory management overview</span></span>](http://spark.apache.org/docs/latest/tuning.html#memory-management-overview)
- [<span data-ttu-id="c75c6-190">HDInsight 클러스터에서 Spark 응용 프로그램 디버그</span><span class="sxs-lookup"><span data-stu-id="c75c6-190">Debug a Spark application on an HDInsight cluster</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/)

