---
title: "Azure HDInsight를 사용한 Spark 문제 해결 | Microsoft Docs"
description: "Apache Spark 및 Azure HDInsight 작업에 대한 일반적인 질문에 답합니다."
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
ms.openlocfilehash: cfed5f0f4f703821e83e3d365810c0e5ad22f035
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-spark-by-using-azure-hdinsight"></a><span data-ttu-id="985a6-104">Azure HDInsight를 사용한 Spark 문제 해결</span><span class="sxs-lookup"><span data-stu-id="985a6-104">Troubleshoot Spark by using Azure HDInsight</span></span>

<span data-ttu-id="985a6-105">Apache Ambari에서 Apache Spark 페이로드를 사용할 때의 주요 문제 및 해결 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-105">Learn about the top issues and their resolutions when working with Apache Spark payloads in Apache Ambari.</span></span>

## <a name="how-do-i-configure-a-spark-application-by-using-ambari-on-clusters"></a><span data-ttu-id="985a6-106">클러스터에서 Ambari를 사용하여 Spark 응용 프로그램을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="985a6-106">How do I configure a Spark application by using Ambari on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="985a6-107">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="985a6-107">Resolution steps</span></span>

<span data-ttu-id="985a6-108">이 프로시저 구성 값은 이전에 HDInsight에서 설정한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-108">The configuration values for this procedure were previously set in HDInsight.</span></span> <span data-ttu-id="985a6-109">설정해야 하는 Spark 구성 및 값을 결정하려면 [Spark 응용 프로그램 OutOfMemoryError 예외가 발생하는 원인](#what-causes-a-spark-application-outofmemoryerror-exception)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="985a6-109">To determine which Spark configurations need to be set and to what values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

1. <span data-ttu-id="985a6-110">클러스터 목록에서 **Spark2**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-110">In the list of clusters, select **Spark2**.</span></span>

    ![목록에서 클러스터 선택](media/hdinsight-troubleshoot-spark/update-config-1.png)

2. <span data-ttu-id="985a6-112">**Configs** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-112">Select the **Configs** tab.</span></span>

    ![Configs 탭 선택](media/hdinsight-troubleshoot-spark/update-config-2.png)

3. <span data-ttu-id="985a6-114">구성 목록에서 **Custom-spark2-defaults**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-114">In the list of configurations, select **Custom-spark2-defaults**.</span></span>

    ![custom-spark-defaults 선택](media/hdinsight-troubleshoot-spark/update-config-3.png)

4. <span data-ttu-id="985a6-116">**spark.executor.memory**와 같이 조정해야 하는 값 설정을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-116">Look for the value setting that you need to adjust, such as **spark.executor.memory**.</span></span> <span data-ttu-id="985a6-117">이 경우 **4608m**의 값이 너무 높습니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-117">In this case, the value of **4608m** is too high.</span></span>

    ![spark.executor.memory 필드 선택](media/hdinsight-troubleshoot-spark/update-config-4.png)

5. <span data-ttu-id="985a6-119">값을 권장 설정으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-119">Set the value to the recommended setting.</span></span> <span data-ttu-id="985a6-120">이 설정에는 **2048m** 값이 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-120">The value **2048m** is recommended for this setting.</span></span>

    ![값을 2048m으로 변경](media/hdinsight-troubleshoot-spark/update-config-5.png)

6. <span data-ttu-id="985a6-122">값을 저장하고 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-122">Save the value, and then save the configuration.</span></span> <span data-ttu-id="985a6-123">도구 모음에서 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-123">On the toolbar, select **Save**.</span></span>

    ![설정 및 구성 저장](media/hdinsight-troubleshoot-spark/update-config-6a.png)

    <span data-ttu-id="985a6-125">주의할 필요가 있는 구성이면 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-125">You are notified if any configurations need attention.</span></span> <span data-ttu-id="985a6-126">항목을 확인한 후 **계속 진행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-126">Note the items, and then select **Proceed Anyway**.</span></span> 

    ![계속 진행 선택](media/hdinsight-troubleshoot-spark/update-config-6b.png)

    <span data-ttu-id="985a6-128">구성 변경 내용에 대한 메모를 작성하고 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-128">Write a note about the configuration changes, and then select **Save**.</span></span>

    ![변경 내용에 대한 메모 입력](media/hdinsight-troubleshoot-spark/update-config-6c.png)

7. <span data-ttu-id="985a6-130">구성이 저장될 때마다 서비스를 다시 시작하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-130">Whenever a configuration is saved, you are prompted to restart the service.</span></span> <span data-ttu-id="985a6-131">**다시 시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-131">Select **Restart**.</span></span>

    ![다시 시작 선택](media/hdinsight-troubleshoot-spark/update-config-7a.png)

    <span data-ttu-id="985a6-133">다시 시작을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-133">Confirm the restart.</span></span>

    ![다시 시작 확인 선택](media/hdinsight-troubleshoot-spark/update-config-7b.png)

    <span data-ttu-id="985a6-135">실행 중인 프로세스를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-135">You can review the processes that are running.</span></span>

    ![실행 중인 프로세스 검토](media/hdinsight-troubleshoot-spark/update-config-7c.png)

8. <span data-ttu-id="985a6-137">구성을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-137">You can add configurations.</span></span> <span data-ttu-id="985a6-138">구성 목록에서 **Custom-spark2-defaults**를 선택하고 **속성 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-138">In the list of configurations, select **Custom-spark2-defaults**, and then select **Add Property**.</span></span>

    ![속성 추가 선택](media/hdinsight-troubleshoot-spark/update-config-8.png)

9. <span data-ttu-id="985a6-140">새 속성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-140">Define a new property.</span></span> <span data-ttu-id="985a6-141">데이터 형식과 같은 특정 설정에 대한 대화 상자를 사용하여 단일 속성을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-141">You can define a single property by using a dialog box for specific settings such as the data type.</span></span> <span data-ttu-id="985a6-142">또는 줄당 하나의 정의를 사용하여 여러 속성을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-142">Or, you can define multiple properties by using one definition per line.</span></span> 

    <span data-ttu-id="985a6-143">이 예제에서 **spark.driver.memory** 속성의 값은 **4g**로 정의되었습니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-143">In this example, the **spark.driver.memory** property is defined with a value of **4g**.</span></span>

    ![새 속성 정의](media/hdinsight-troubleshoot-spark/update-config-9.png)

10. <span data-ttu-id="985a6-145">6단계와 7단계에서 설명한 대로 구성을 저장하고 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-145">Save the configuration, and then restart the service as described in steps 6 and 7.</span></span>

<span data-ttu-id="985a6-146">이러한 변경 내용은 클러스터 전체를 대상으로 하지만 Spark 작업을 제출할 때 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-146">These changes are cluster-wide but can be overridden when you submit the Spark job.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="985a6-147">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="985a6-147">Additional reading</span></span>

[<span data-ttu-id="985a6-148">HDInsight 클러스터에서 Spark 작업 제출(영문)</span><span class="sxs-lookup"><span data-stu-id="985a6-148">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-a-jupyter-notebook-on-clusters"></a><span data-ttu-id="985a6-149">클러스터에서 Jupyter Notebook을 사용하여 Spark 응용 프로그램을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="985a6-149">How do I configure a Spark application by using a Jupyter notebook on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="985a6-150">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="985a6-150">Resolution steps</span></span>

1. <span data-ttu-id="985a6-151">설정해야 하는 Spark 구성 및 값을 결정하려면 [Spark 응용 프로그램 OutOfMemoryError 예외가 발생하는 원인](#what-causes-a-spark-application-outofmemoryerror-exception)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="985a6-151">To determine which Spark configurations need to be set and to what values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="985a6-152">Jupyter Notebook의 첫 번째 셀에서 **%%configure** 지시문 뒤에 유효한 JSON 형식의 Spark 구성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-152">In the first cell of the Jupyter notebook, after the **%%configure** directive, specify the Spark configurations in valid JSON format.</span></span> <span data-ttu-id="985a6-153">필요에 따라 실제 값을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-153">Change the actual values as necessary:</span></span>

    ![구성 추가](media/hdinsight-troubleshoot-spark/add-configuration-cell.png)

### <a name="additional-reading"></a><span data-ttu-id="985a6-155">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="985a6-155">Additional reading</span></span>

[<span data-ttu-id="985a6-156">HDInsight 클러스터에서 Spark 작업 제출(영문)</span><span class="sxs-lookup"><span data-stu-id="985a6-156">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-livy-on-clusters"></a><span data-ttu-id="985a6-157">클러스터에서 Livy를 사용하여 Spark 응용 프로그램을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="985a6-157">How do I configure a Spark application by using Livy on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="985a6-158">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="985a6-158">Resolution steps</span></span>

1. <span data-ttu-id="985a6-159">설정해야 하는 Spark 구성 및 값을 결정하려면 [Spark 응용 프로그램 OutOfMemoryError 예외가 발생하는 원인](#what-causes-a-spark-application-outofmemoryerror-exception)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="985a6-159">To determine which Spark configurations need to be set and to what values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

2. <span data-ttu-id="985a6-160">cURL 같은 REST 클라이언트를 사용하여 Livy로 Spark 응용 프로그램을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-160">Submit the Spark application to Livy by using a REST client like cURL.</span></span> <span data-ttu-id="985a6-161">다음과 유사한 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-161">Use a command similar to the following.</span></span> <span data-ttu-id="985a6-162">필요에 따라 실제 값을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-162">Change the actual values as necessary:</span></span>

    ```apache
    curl -k --user 'username:password' -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://container@storageaccountname.blob.core.windows.net/example/jars/sparkapplication.jar", "className":"com.microsoft.spark.application", "numExecutors":4, "executorMemory":"4g", "executorCores":2, "driverMemory":"8g", "driverCores":4}'  
    ```

### <a name="additional-reading"></a><span data-ttu-id="985a6-163">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="985a6-163">Additional reading</span></span>

[<span data-ttu-id="985a6-164">HDInsight 클러스터에서 Spark 작업 제출(영문)</span><span class="sxs-lookup"><span data-stu-id="985a6-164">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-spark-submit-on-clusters"></a><span data-ttu-id="985a6-165">클러스터에서 spark-submit을 사용하여 Spark 응용 프로그램을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="985a6-165">How do I configure a Spark application by using spark-submit on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="985a6-166">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="985a6-166">Resolution steps</span></span>

1. <span data-ttu-id="985a6-167">설정해야 하는 Spark 구성 및 값을 결정하려면 [Spark 응용 프로그램 OutOfMemoryError 예외가 발생하는 원인](#what-causes-a-spark-application-outofmemoryerror-exception)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="985a6-167">To determine which Spark configurations need to be set and to what values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="985a6-168">다음과 비슷한 명령을 사용하여 spark-shell을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-168">Launch spark-shell by using a command similar to the following.</span></span> <span data-ttu-id="985a6-169">필요에 따라 구성의 실제 값을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-169">Change the actual value of the configurations as necessary:</span></span> 

    ```apache
    spark-submit --master yarn-cluster --class com.microsoft.spark.application --num-executors 4 --executor-memory 4g --executor-cores 2 --driver-memory 8g --driver-cores 4 /home/user/spark/sparkapplication.jar
    ```

### <a name="additional-reading"></a><span data-ttu-id="985a6-170">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="985a6-170">Additional reading</span></span>

[<span data-ttu-id="985a6-171">HDInsight 클러스터에서 Spark 작업 제출(영문)</span><span class="sxs-lookup"><span data-stu-id="985a6-171">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="what-causes-a-spark-application-outofmemoryerror-exception"></a><span data-ttu-id="985a6-172">Spark 응용 프로그램 OutofMemoryError 예외를 발생시키는 원인</span><span class="sxs-lookup"><span data-stu-id="985a6-172">What causes a Spark application OutofMemoryError exception</span></span>

### <a name="detailed-description"></a><span data-ttu-id="985a6-173">자세한 설명</span><span class="sxs-lookup"><span data-stu-id="985a6-173">Detailed description</span></span>

<span data-ttu-id="985a6-174">Spark 응용 프로그램이 다음과 같은 유형의 확인(catch)할 수 없는 예외로 인해 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-174">The Spark application fails, with the following types of uncaught exceptions:</span></span>

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

### <a name="probable-cause"></a><span data-ttu-id="985a6-175">가능한 원인:</span><span class="sxs-lookup"><span data-stu-id="985a6-175">Probable cause</span></span>

<span data-ttu-id="985a6-176">이 예외의 가장 가능성 높은 원인은 JVM(Java Virtual Machine)에 할당된 힙 메모리가 충분하지 않다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-176">The most likely cause of this exception is that not enough heap memory is allocated to the Java virtual machines (JVMs).</span></span> <span data-ttu-id="985a6-177">이러한 JVM은 Spark 응용 프로그램의 일부로 실행기 또는 드라이버로서 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-177">These JVMs are launched as executors or drivers as part of the Spark application.</span></span> 

### <a name="resolution-steps"></a><span data-ttu-id="985a6-178">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="985a6-178">Resolution steps</span></span>

1. <span data-ttu-id="985a6-179">Spark 응용 프로그램에서 처리하는 데이터의 최대 크기를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-179">Determine the maximum size of the data the Spark application handles.</span></span> <span data-ttu-id="985a6-180">입력 데이터의 최대 크기, 입력 데이터 변환을 통해 생성되는 중간 데이터, 응용 프로그램이 중간 데이터를 추가적으로 변환할 때 생성되는 출력 데이터에 따라 이러한 크기를 추측해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-180">You can make a guess based on the maximum size of the input data, the intermediate data that's produced by transforming the input data, and the output data that's produced when the application is further transforming the intermediate data.</span></span> <span data-ttu-id="985a6-181">초기에 공식적으로 추측할 수 없는 경우 이 프로세스를 반복할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-181">This process can be an iterative if you can't make an initial formal guess.</span></span> 

2. <span data-ttu-id="985a6-182">사용할 HDInsight 클러스터가 Spark 응용 프로그램을 수용할 수 있는 메모리와 코어 등 충분한 리소스를 갖추고 있는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="985a6-182">Make sure that the HDInsight cluster that you're going to use has enough resources in terms of memory and cores to accommodate the Spark application.</span></span> <span data-ttu-id="985a6-183">YARN UI에서 Cluster Metrics 섹션에 있는 **Memory Used** 값과 Memory Total 값, VCores Used 값과 **Memory Total** 값, **VCores Used** 값과 **VCores Total** 값을 검토하여 이를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-183">You can determine this by viewing the cluster metrics section of the YARN UI for the values of **Memory Used** vs. **Memory Total**, and **VCores Used** vs. **VCores Total**.</span></span>

3. <span data-ttu-id="985a6-184">다음 Spark 구성을 사용 가능한 메모리 및 코어의 90%를 초과하지 않는 적절한 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-184">Set the following Spark configurations to appropriate values, which should not exceed 90% of the available memory and cores.</span></span> <span data-ttu-id="985a6-185">값은 Spark 응용 프로그램의 메모리 요구 사항을 벗어나지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-185">The values should be well within the memory requirements of the Spark application:</span></span> 

    ```apache
    spark.executor.instances (Example: 8 for 8 executor count) 
    spark.executor.memory (Example: 4g for 4 GB) 
    spark.yarn.executor.memoryOverhead (Example: 384m for 384 MB) 
    spark.executor.cores (Example: 2 for 2 cores per executor) 
    spark.driver.memory (Example: 8g for 8GB) 
    spark.driver.cores (Example: 4 for 4 cores)   
    spark.yarn.driver.memoryOverhead (Example: 384m for 384MB) 
    ```

    <span data-ttu-id="985a6-186">모든 실행기에서 사용되는 총 메모리를 가져오려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-186">To get the total memory used by all executors, run the following command:</span></span> 
    
    ```apache
    spark.executor.instances * (spark.executor.memory + spark.yarn.executor.memoryOverhead) 
    ```
    <span data-ttu-id="985a6-187">드라이버에서 사용되는 총 메모리를 가져오려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="985a6-187">To get the total memory used by the driver, run the following command:</span></span>
    
    ```apache
    spark.driver.memory + spark.yarn.driver.memoryOverhead
    ```

### <a name="additional-reading"></a><span data-ttu-id="985a6-188">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="985a6-188">Additional reading</span></span>

- [<span data-ttu-id="985a6-189">Spark 메모리 관리 개요(영문)</span><span class="sxs-lookup"><span data-stu-id="985a6-189">Spark memory management overview</span></span>](http://spark.apache.org/docs/latest/tuning.html#memory-management-overview)
- [<span data-ttu-id="985a6-190">HDInsight 클러스터에서 Spark 응용 프로그램 디버그</span><span class="sxs-lookup"><span data-stu-id="985a6-190">Debug a Spark application on an HDInsight cluster</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/)

