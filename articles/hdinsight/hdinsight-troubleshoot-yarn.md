---
title: "Azure HDInsight를 사용한 YARN 문제 해결 | Microsoft Docs"
description: "Apache Hadoop YARN 및 Azure HDInsight 작업에 대한 일반적인 질문에 답합니다."
keywords: "Azure HDInsight, YARN, FAQ, 문제 해결 가이드, 일반적인 질문"
services: Azure HDInsight
documentationcenter: na
author: arijitt
manager: 
editor: 
ms.assetid: F76786A9-99AB-4B85-9B15-CA03528FC4CD
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: arijitt
ms.openlocfilehash: 63f2d88ad59661b7fbcffd0aaeb94c58d40bdb73
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-yarn-by-using-azure-hdinsight"></a><span data-ttu-id="db64d-104">Azure HDInsight를 사용한 YARN 문제 해결</span><span class="sxs-lookup"><span data-stu-id="db64d-104">Troubleshoot YARN by using Azure HDInsight</span></span>

<span data-ttu-id="db64d-105">Apache Ambari에서 Apache Hadoop YARN 페이로드를 사용할 때의 주요 문제 및 해결 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="db64d-105">Learn about the top issues and their resolutions when working with Apache Hadoop YARN payloads in Apache Ambari.</span></span>

## <a name="how-do-i-create-a-new-yarn-queue-on-a-cluster"></a><span data-ttu-id="db64d-106">클러스터에서 새 YARN 큐를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="db64d-106">How do I create a new YARN queue on a cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="db64d-107">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="db64d-107">Resolution steps</span></span> 

<span data-ttu-id="db64d-108">Ambari에서 다음 단계를 사용하여 새 YARN 큐를 만들고 모든 큐에 용량이 균형 있게 할당되도록 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="db64d-108">Use the following steps in Ambari to create a new YARN queue, and then balance the capacity allocation among all the queues.</span></span> 

<span data-ttu-id="db64d-109">이 예제에서는 기존 큐 두 개(**default** 및 **thriftsvr**) 모두 새 큐(spark)를 50% 용량으로 하여 50% 용량에서 25% 용량으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="db64d-109">In this example, two existing queues (**default** and **thriftsvr**) both are changed from 50% capacity to 25% capacity, which gives the new queue (spark) 50% capacity.</span></span>
| <span data-ttu-id="db64d-110">큐</span><span class="sxs-lookup"><span data-stu-id="db64d-110">Queue</span></span> | <span data-ttu-id="db64d-111">용량</span><span class="sxs-lookup"><span data-stu-id="db64d-111">Capacity</span></span> | <span data-ttu-id="db64d-112">최대 용량</span><span class="sxs-lookup"><span data-stu-id="db64d-112">Maximum capacity</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="db64d-113">기본값</span><span class="sxs-lookup"><span data-stu-id="db64d-113">default</span></span> | <span data-ttu-id="db64d-114">25%</span><span class="sxs-lookup"><span data-stu-id="db64d-114">25%</span></span> | <span data-ttu-id="db64d-115">50%</span><span class="sxs-lookup"><span data-stu-id="db64d-115">50%</span></span> |
| <span data-ttu-id="db64d-116">thrftsvr</span><span class="sxs-lookup"><span data-stu-id="db64d-116">thrftsvr</span></span> | <span data-ttu-id="db64d-117">25%</span><span class="sxs-lookup"><span data-stu-id="db64d-117">25%</span></span> | <span data-ttu-id="db64d-118">50%</span><span class="sxs-lookup"><span data-stu-id="db64d-118">50%</span></span> |
| <span data-ttu-id="db64d-119">spark</span><span class="sxs-lookup"><span data-stu-id="db64d-119">spark</span></span> | <span data-ttu-id="db64d-120">50%</span><span class="sxs-lookup"><span data-stu-id="db64d-120">50%</span></span> | <span data-ttu-id="db64d-121">50%</span><span class="sxs-lookup"><span data-stu-id="db64d-121">50%</span></span> |

1. <span data-ttu-id="db64d-122">**Ambari 뷰** 아이콘을 선택한 다음, 그리드 패턴을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db64d-122">Select the **Ambari Views** icon, and then select the grid pattern.</span></span> <span data-ttu-id="db64d-123">다음으로, **YARN 큐 관리자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db64d-123">Next, select **YARN Queue Manager**.</span></span>

    ![Ambari 뷰 아이콘 선택](media/hdinsight-troubleshoot-yarn/create-queue-1.png)
2. <span data-ttu-id="db64d-125">**default** 큐를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db64d-125">Select the **default** queue.</span></span>

    ![default 큐 선택](media/hdinsight-troubleshoot-yarn/create-queue-2.png)
3. <span data-ttu-id="db64d-127">**default** 큐의 경우 **용량**을 50%에서 25%로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="db64d-127">For the **default** queue, change the **capacity** from 50% to 25%.</span></span> <span data-ttu-id="db64d-128">**thriftsvr** 큐의 경우 **용량**을 25%로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="db64d-128">For the **thriftsvr** queue, change the **capacity** to 25%.</span></span>

    ![default 및 thriftsvr 큐에 대해 용량을 25%로 변경](media/hdinsight-troubleshoot-yarn/create-queue-3.png)
4. <span data-ttu-id="db64d-130">새 큐를 만들려면 **큐 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db64d-130">To create a new queue, select **Add Queue**.</span></span>

    ![큐 추가 선택](media/hdinsight-troubleshoot-yarn/create-queue-4.png)

5. <span data-ttu-id="db64d-132">새 큐 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="db64d-132">Name the new queue.</span></span>

    ![큐 이름을 Spark로 지정](media/hdinsight-troubleshoot-yarn/create-queue-5.png)  

6. <span data-ttu-id="db64d-134">**용량** 값을 50%로 두고 **작업** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db64d-134">Leave the **capacity** values at 50%, and then select the **Actions** button.</span></span>

    ![작업 단추 선택](media/hdinsight-troubleshoot-yarn/create-queue-6.png)  
7. <span data-ttu-id="db64d-136">**큐 저장 및 새로 고침**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db64d-136">Select **Save and Refresh Queues**.</span></span>

    ![큐 저장 및 새로 고침 선택](media/hdinsight-troubleshoot-yarn/create-queue-7.png)  

<span data-ttu-id="db64d-138">이러한 변경 내용은 YARN Scheduler UI에 즉시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="db64d-138">These changes are visible immediately on the YARN Scheduler UI.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="db64d-139">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="db64d-139">Additional reading</span></span>

- [<span data-ttu-id="db64d-140">YARN CapacityScheduler</span><span class="sxs-lookup"><span data-stu-id="db64d-140">YARN CapacityScheduler</span></span>](https://hadoop.apache.org/docs/r2.7.2/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html)


## <a name="how-do-i-download-yarn-logs-from-a-cluster"></a><span data-ttu-id="db64d-141">클러스터에서 YARN 로그를 다운로드하는 방법</span><span class="sxs-lookup"><span data-stu-id="db64d-141">How do I download YARN logs from a cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="db64d-142">해결 단계:</span><span class="sxs-lookup"><span data-stu-id="db64d-142">Resolution steps</span></span> 

1. <span data-ttu-id="db64d-143">SSH(Secure Shell) 클라이언트를 사용하여 HDInsight 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="db64d-143">Connect to the HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="db64d-144">자세한 내용은 [더 보기](#additional-reading-2)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db64d-144">For more information, see [Additional reading](#additional-reading-2).</span></span>

2. <span data-ttu-id="db64d-145">현재 실행 중인 YARN 응용 프로그램의 모든 응용 프로그램 ID를 나열하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db64d-145">To list all the application IDs of the YARN applications that are currently running, run the following command:</span></span>

    ```apache
    yarn top
    ```
    <span data-ttu-id="db64d-146">ID가 **APPLICATIONID** 열에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="db64d-146">The IDs are listed in the **APPLICATIONID** column.</span></span> <span data-ttu-id="db64d-147">**APPLICATIONID** 열에서 로그를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db64d-147">You can download logs from the **APPLICATIONID** column.</span></span>

    ```apache
    YARN top - 18:00:07, up 19d, 0:14, 0 active users, queue(s): root
    NodeManager(s): 4 total, 4 active, 0 unhealthy, 0 decommissioned, 0 lost, 0 rebooted
    Queue(s) Applications: 2 running, 10 submitted, 0 pending, 8 completed, 0 killed, 0 failed
    Queue(s) Mem(GB): 97 available, 3 allocated, 0 pending, 0 reserved
    Queue(s) VCores: 58 available, 2 allocated, 0 pending, 0 reserved
    Queue(s) Containers: 2 allocated, 0 pending, 0 reserved

                      APPLICATIONID USER             TYPE      QUEUE   #CONT  #RCONT  VCORES RVCORES     MEM    RMEM  VCORESECS    MEMSECS %PROGR       TIME NAME
     application_1490377567345_0007 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628407    2442611  10.00   18:20:20 Thrift JDBC/ODBC Server
     application_1490377567345_0006 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628430    2442645  10.00   18:20:20 Thrift JDBC/ODBC Server
    ```

3. <span data-ttu-id="db64d-148">모든 응용 프로그램 마스터에 대한 YARN 컨테이너 로그를 다운로드하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db64d-148">To download YARN container logs for all application masters, use the following command:</span></span>
   
    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am ALL > amlogs.txt
    ```

    <span data-ttu-id="db64d-149">amlogs.txt라는 로그 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="db64d-149">This command creates a log file named amlogs.txt.</span></span> 

4. <span data-ttu-id="db64d-150">최신 응용 프로그램 마스터에 대한 YARN 컨테이너 로그만 다운로드하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db64d-150">To download YARN container logs for only the latest application master, use the following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am -1 > latestamlogs.txt
    ```

    <span data-ttu-id="db64d-151">latestamlogs.txt라는 로그 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="db64d-151">This command creates a log file named latestamlogs.txt.</span></span> 

4. <span data-ttu-id="db64d-152">처음 두 개 응용 프로그램 마스터에 대한 YARN 컨테이너 로그를 다운로드하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db64d-152">To download YARN container logs for the first two application masters, use the following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am 1,2 > first2amlogs.txt 
    ```

    <span data-ttu-id="db64d-153">first2amlogs.txt라는 로그 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="db64d-153">This command creates a log file named first2amlogs.txt.</span></span> 

5. <span data-ttu-id="db64d-154">모든 YARN 컨테이너 로그를 다운로드하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db64d-154">To download all YARN container logs, use the following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> > logs.txt
    ```

    <span data-ttu-id="db64d-155">logs.txt라는 로그 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="db64d-155">This command creates a log file named logs.txt.</span></span> 

6. <span data-ttu-id="db64d-156">특정 컨테이너에 대한 YARN 컨테이너 로그를 다운로드하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db64d-156">To download the YARN container log for a specific container, use the following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -containerId <container_id> > containerlogs.txt 
    ```

    <span data-ttu-id="db64d-157">containerlogs.txt라는 로그 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="db64d-157">This command creates a log file named containerlogs.txt.</span></span>

### <span data-ttu-id="db64d-158"><a name="additional-reading-2"></a>추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="db64d-158"><a name="additional-reading-2"></a>Additional reading</span></span>

- [<span data-ttu-id="db64d-159">SSH를 사용하여 HDInsight(Hadoop)에 연결</span><span class="sxs-lookup"><span data-stu-id="db64d-159">Connect to HDInsight (Hadoop) by using SSH</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)
- [<span data-ttu-id="db64d-160">Apache Hadoop YARN 개념 및 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="db64d-160">Apache Hadoop YARN concepts and applications</span></span>](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/)







