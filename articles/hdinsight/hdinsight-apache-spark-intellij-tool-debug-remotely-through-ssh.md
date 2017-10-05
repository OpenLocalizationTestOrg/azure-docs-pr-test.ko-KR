---
title: "IntelliJ용 Azure 도구 키트: SSH를 통해 원격으로 Spark 응용 프로그램 디버그 | Microsoft Docs"
description: "IntelliJ용 Azure 도구 키트의 HDInsight 도구를 사용하여 SSH를 통해 HDInsight 클러스터에서 응용 프로그램을 원격으로 디버그하는 방법에 대한 단계별 지침"
keywords: "IntelliJ 원격으로 디버그, IntelliJ 원격 디버깅, SSH, IntelliJ, HDInsight, IntelliJ 디버그, 디버깅"
services: hdinsight
documentationcenter: 
author: jejiang
manager: DJ
editor: Jenny Jiang
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 08/24/2017
ms.author: Jenny Jiang
ms.openlocfilehash: 19053e31d6eb097bc91a04ef9c6af5772aaa16da
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="debug-spark-applications-on-an-hdinsight-cluster-with-azure-toolkit-for-intellij-through-ssh"></a><span data-ttu-id="17df0-104">IntelliJ용 Azure 도구 키트를 사용하여 SSH를 통해 HDInsight 클러스터에서 Spark 응용 프로그램 디버그</span><span class="sxs-lookup"><span data-stu-id="17df0-104">Debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH</span></span>

<span data-ttu-id="17df0-105">이 문서에서는 IntelliJ용 Azure 도구 키트의 HDInsight 도구를 사용하여 HDInsight 클러스터에서 응용 프로그램을 원격으로 디버그하는 방법에 대한 단계별 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-105">This article provides step-by-step guidance on how to use HDInsight Tools in Azure Toolkit for IntelliJ to debug applications remotely on an HDInsight cluster.</span></span> <span data-ttu-id="17df0-106">프로젝트를 디버그하려는 경우 [IntelliJ용 Azure 도구 키트로 HDInsight Spark 응용 프로그램 디버그](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) 비디오를 시청할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-106">To debug your project, you can also view the [Debug HDInsight Spark applications with Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) video.</span></span>

<span data-ttu-id="17df0-107">**필수 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="17df0-107">**Prerequisites**</span></span>

* <span data-ttu-id="17df0-108">**IntelliJ용 Azure 도구 키트의 HDInsight 도구**</span><span class="sxs-lookup"><span data-stu-id="17df0-108">**HDInsight Tools in Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="17df0-109">이 도구는 IntelliJ용 Azure 도구 키트의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-109">This tool is part of Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="17df0-110">자세한 내용은 [IntelliJ용 Azure 도구 키트 설치](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17df0-110">For more information, see [Install Azure Toolkit for IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).</span></span>
* <span data-ttu-id="17df0-111">**IntelliJ용 Azure 도구 키트**</span><span class="sxs-lookup"><span data-stu-id="17df0-111">**Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="17df0-112">이 도구 키트를 사용하여 HDInsight 클러스터용 Spark 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-112">Use this toolkit to create Spark applications for an HDInsight cluster.</span></span> <span data-ttu-id="17df0-113">자세한 내용은 [IntelliJ용 Azure 도구 키트를 사용하여 HDInsight 클러스터용 Spark 응용 프로그램 만들기](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin)의 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="17df0-113">For more information, follow the instructions in [Use Azure Toolkit for IntelliJ to create Spark applications for an HDInsight cluster](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).</span></span>
* <span data-ttu-id="17df0-114">**사용자 이름 및 암호 관리를 포함한 HDInsight SSH 서비스**.</span><span class="sxs-lookup"><span data-stu-id="17df0-114">**HDInsight SSH service with username and password management**.</span></span> <span data-ttu-id="17df0-115">자세한 내용은 [SSH를 사용하여 HDInsight(Hadoop)에 연결](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) 및 [SSH 터널링을 사용하여 Ambari 웹 UI, JobHistory, NameNode, Oozie 및 기타 웹 UI에 액세스](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17df0-115">For more information, see [Connect to HDInsight (Hadoop) by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Use SSH tunneling to access Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel).</span></span> 
 

## <a name="create-a-spark-scala-application-and-configure-it-for-remote-debugging"></a><span data-ttu-id="17df0-116">Spark Scala 응용 프로그램을 만들고 원격 디버깅을 위해 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-116">Create a Spark Scala application and configure it for remote debugging</span></span>

1. <span data-ttu-id="17df0-117">IntelliJ IDEA를 시작하고 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-117">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="17df0-118">**새 프로젝트** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-118">In the **New Project** dialog box, do the following:</span></span>

   <span data-ttu-id="17df0-119">a.</span><span class="sxs-lookup"><span data-stu-id="17df0-119">a.</span></span> <span data-ttu-id="17df0-120">**HDInsight**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-120">Select **HDInsight**.</span></span> 

   <span data-ttu-id="17df0-121">b.</span><span class="sxs-lookup"><span data-stu-id="17df0-121">b.</span></span> <span data-ttu-id="17df0-122">기본 설정에 따라 Java 또는 Scala 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-122">Select a Java or Scala template based on your preference.</span></span> <span data-ttu-id="17df0-123">다음 옵션 중에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-123">Select between the following options:</span></span>

      - <span data-ttu-id="17df0-124">**HDInsight의 Spark(Scala)**</span><span class="sxs-lookup"><span data-stu-id="17df0-124">**Spark on HDInsight (Scala)**</span></span>

      - <span data-ttu-id="17df0-125">**HDInsight의 Spark(Java)**</span><span class="sxs-lookup"><span data-stu-id="17df0-125">**Spark on HDInsight (Java)**</span></span>

      - <span data-ttu-id="17df0-126">**HDInsight의 Spark 클러스터 실행 샘플(Scala)** </span><span class="sxs-lookup"><span data-stu-id="17df0-126">**Spark on HDInsight Cluster Run Sample (Scala)**</span></span>

      <span data-ttu-id="17df0-127">이 예제에서는 **HDInsight의 Spark 클러스터 실행 샘플(Scala)** 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-127">This example uses a **Spark on HDInsight Cluster Run Sample (Scala)** template.</span></span>

   <span data-ttu-id="17df0-128">c.</span><span class="sxs-lookup"><span data-stu-id="17df0-128">c.</span></span> <span data-ttu-id="17df0-129">**빌드 도구** 목록에서 요구 사항에 따라 다음 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-129">In the **Build tool** list, select either of the following, according to your need:</span></span>

      - <span data-ttu-id="17df0-130">Scala 프로젝트 만들기 마법사 지원에 대해 **Maven**</span><span class="sxs-lookup"><span data-stu-id="17df0-130">**Maven**, for Scala project-creation wizard support</span></span>

      -  <span data-ttu-id="17df0-131">종속성 관리 및 Scala 프로젝트에 대한 빌드에 대해 **SBT**</span><span class="sxs-lookup"><span data-stu-id="17df0-131">**SBT**, for managing the dependencies and building for the Scala project</span></span> 

      ![디버그 프로젝트 만들기](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-create-projectfor-debug-remotely.png)

   <span data-ttu-id="17df0-133">d.</span><span class="sxs-lookup"><span data-stu-id="17df0-133">d.</span></span> <span data-ttu-id="17df0-134">**다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-134">Select **Next**.</span></span>     
 
3. <span data-ttu-id="17df0-135">다음 **새 프로젝트** 창에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-135">In the next **New Project** window, do the following:</span></span>

   ![Spark SDK 선택](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-new-project.png)

   <span data-ttu-id="17df0-137">a.</span><span class="sxs-lookup"><span data-stu-id="17df0-137">a.</span></span> <span data-ttu-id="17df0-138">프로젝트 이름과 프로젝트 위치를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-138">Enter a project name and project location.</span></span>

   <span data-ttu-id="17df0-139">b.</span><span class="sxs-lookup"><span data-stu-id="17df0-139">b.</span></span> <span data-ttu-id="17df0-140">**프로젝트 SDK** 드롭다운 목록에서 **Spark 2.x** 클러스터에 대해 **Java 1.8**을 선택하거나 **Spark 1.x** 클러스터에 대해 **Java 1.7**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-140">In the **Project SDK** drop-down list, select **Java 1.8** for **Spark 2.x** cluster or select **Java 1.7** for **Spark 1.x** cluster.</span></span>

   <span data-ttu-id="17df0-141">c.</span><span class="sxs-lookup"><span data-stu-id="17df0-141">c.</span></span> <span data-ttu-id="17df0-142">**Spark 버전** 드롭다운 목록에서 Scala 프로젝트 생성 마법사는 Spark SDK 및 Scala SDK에 대한 올바른 버전을 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-142">In the **Spark Version** drop-down list, the Scala project creation wizard integrates the correct version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="17df0-143">Spark 클러스터 2.0 이하 버전을 사용하는 경우 **Spark 1.x**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-143">If the spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="17df0-144">그렇지 않은 경우 **Spark 2.x**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-144">Otherwise, select **Spark 2.x.**</span></span> <span data-ttu-id="17df0-145">이 예제에서는 **Spark 2.0.2(Scala 2.11.8)**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-145">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

   <span data-ttu-id="17df0-146">d.</span><span class="sxs-lookup"><span data-stu-id="17df0-146">d.</span></span> <span data-ttu-id="17df0-147">**마침**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-147">Select **Finish**.</span></span>

4. <span data-ttu-id="17df0-148">**src** > **main** > **scala**를 선택하여 프로젝트에서 코드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-148">Select **src** > **main** > **scala** to open your code in the project.</span></span> <span data-ttu-id="17df0-149">이 예제에서는 **SparkCore_wasbloTest** 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-149">This example uses the **SparkCore_wasbloTest** script.</span></span>

5. <span data-ttu-id="17df0-150">**구성 편집** 메뉴에 액세스하려면 오른쪽 위 구석에 있는 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-150">To access the **Edit Configurations** menu, select the icon in the upper-right corner.</span></span> <span data-ttu-id="17df0-151">이 메뉴에서 원격 디버깅에 대한 구성을 만들거나 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-151">From this menu, you can create or edit the configurations for remote debugging.</span></span>

   ![구성 편집](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-edit-configurations.png) 

6. <span data-ttu-id="17df0-153">**실행/디버깅 구성** 대화 상자에서 더하기 기호(**+**)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-153">In the **Run/Debug Configurations** dialog box, select the plus sign (**+**).</span></span> <span data-ttu-id="17df0-154">그런 다음 **Spark 작업 제출** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-154">Then select the **Submit Spark Job** option.</span></span>

   ![새 구성 추가](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-add-new-Configuration.png)
7. <span data-ttu-id="17df0-156">**이름**, **Spark 클러스터** 및 **주 클래스 이름**에 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-156">Enter information for **Name**, **Spark cluster**, and **Main class name**.</span></span> <span data-ttu-id="17df0-157">그런 다음 **고급 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-157">Then select **Advanced configuration**.</span></span> 

   ![디버그 구성 실행](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-run-debug-configurations.png)

8. <span data-ttu-id="17df0-159">**Spark 제출 고급 구성** 대화 상자에서 **Spark 원격 디버그 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-159">In the **Spark Submission Advanced Configuration** dialog box, select **Enable Spark remote debug**.</span></span> <span data-ttu-id="17df0-160">SSH 사용자 이름을 입력하고 암호를 입력하거나 개인 키 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-160">Enter the SSH username, and then enter a password or use a private key file.</span></span> <span data-ttu-id="17df0-161">구성을 저장하려면 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-161">To save the configuration, select **OK**.</span></span>

   ![Spark 원격 디버그 설정](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-enable-spark-remote-debug.png)

9. <span data-ttu-id="17df0-163">이제 사용자가 입력한 이름으로 구성이 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-163">The configuration is now saved with the name you provided.</span></span> <span data-ttu-id="17df0-164">구성 세부 정보를 보려면 구성 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-164">To view the configuration details, select the configuration name.</span></span> <span data-ttu-id="17df0-165">변경하려면 **구성 편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-165">To make changes, select **Edit Configurations**.</span></span> 

10. <span data-ttu-id="17df0-166">구성 설정을 완료한 후에 원격 클러스터에 대해 프로젝트를 실행하거나 원격 디버깅을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-166">After you complete the configurations settings, you can run the project against the remote cluster or perform remote debugging.</span></span>

## <a name="learn-how-to-perform-remote-debugging"></a><span data-ttu-id="17df0-167">원격 디버깅을 수행하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="17df0-167">Learn how to perform remote debugging</span></span>
### <a name="scenario-1-perform-remote-run"></a><span data-ttu-id="17df0-168">시나리오 1: 원격 실행 수행</span><span class="sxs-lookup"><span data-stu-id="17df0-168">Scenario 1: Perform remote run</span></span>

<span data-ttu-id="17df0-169">이 섹션에서는 드라이버 및 실행기를 디버그하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-169">In this section, we show you how to debug drivers and executors.</span></span>

    import org.apache.spark.{SparkConf, SparkContext}

    object LogQuery {
      val exampleApacheLogs = List(
        """10.10.10.10 - "FRED" [18/Jan/2013:17:56:07 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 315 "http://referall.com/" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.350 "-" - "" 265 923 934 ""
          | 62.24.11.25 images.com 1358492167 - Whatup""".stripMargin.lines.mkString,
        """10.10.10.10 - "FRED" [18/Jan/2013:18:02:37 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 306 "http:/referall.com" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.352 "-" - "" 256 977 988 ""
          | 0 73.23.2.15 images.com 1358492557 - Whatup""".stripMargin.lines.mkString
      )
      def main(args: Array[String]) {
        val sparkconf = new SparkConf().setAppName("Log Query")
        val sc = new SparkContext(sparkconf)
        val dataSet = sc.parallelize(exampleApacheLogs)
        // scalastyle:off
        val apacheLogRegex =
          """^([\d.]+) (\S+) (\S+) \[([\w\d:/]+\s[+\-]\d{4})\] "(.+?)" (\d{3}) ([\d\-]+) "([^"]+)" "([^"]+)".*""".r
        // scalastyle:on
        /** Tracks the total query count and number of aggregate bytes for a particular group. */
        class Stats(val count: Int, val numBytes: Int) extends Serializable {
          def merge(other: Stats): Stats = new Stats(count + other.count, numBytes + other.numBytes)
          override def toString: String = "bytes=%s\tn=%s".format(numBytes, count)
        }
        def extractKey(line: String): (String, String, String) = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              if (user != "\"-\"") (ip, user, query)
              else (null, null, null)
            case _ => (null, null, null)
          }
        }
        def extractStats(line: String): Stats = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              new Stats(1, bytes.toInt)
            case _ => new Stats(1, 0)
          }
        }
        
        dataSet.map(line => (extractKey(line), extractStats(line)))
          .reduceByKey((a, b) => a.merge(b))
          .collect().foreach{
          case (user, query) => println("%s\t%s".format(user, query))}

        sc.stop()
      }
    }


1. <span data-ttu-id="17df0-170">중단점을 설정한 다음 **디버그** 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-170">Set up breaking points, and then select the **Debug** icon.</span></span>

   ![디버그 아이콘 선택](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-icon.png)

2. <span data-ttu-id="17df0-172">프로그램 실행이 중단점에 도달하면 **디버거** 창에 1개의 **드라이버** 탭과 2개의 **실행기** 탭이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-172">When the program execution reaches the breaking point, you see a **Driver** tab and two **Executor** tabs in the **Debugger** pane.</span></span> <span data-ttu-id="17df0-173">**프로그램 다시 시작** 아이콘을 선택하여 코드를 계속 실행합니다. 그런 다음 중단점에 도달하면 해당 **실행기** 탭에 초점이 맞춰집니다. 해당 **콘솔** 탭에서 실행 로그를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-173">Select the **Resume Program** icon to continue running the code, which then reaches the next breakpoint and focuses on the corresponding **Executor** tab. You can review the execution logs on the corresponding **Console** tab.</span></span>

   ![디버깅 탭](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debugger-tab.png)

### <a name="scenario-2-perform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="17df0-175">시나리오 2: 원격 디버깅 및 버그 수정 수행</span><span class="sxs-lookup"><span data-stu-id="17df0-175">Scenario 2: Perform remote debugging and bug fixing</span></span>
<span data-ttu-id="17df0-176">이 섹션에서는 간단한 수정을 위해 IntelliJ 디버깅 기능을 사용하여 변수 값을 동적으로 업데이트하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-176">In this section, we show you how to dynamically update the variable value by using the IntelliJ debugging capability for a simple fix.</span></span> <span data-ttu-id="17df0-177">다음 코드 예제에서는 대상 파일이 이미 있기 때문에 예외가 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-177">In the following code example, an exception is thrown because the target file already exists.</span></span>
  
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext

        object SparkCore_WasbIOTest {
          def main(arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkCore_WasbIOTest")
            val sc = new SparkContext(conf)
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            // Find the rows that have only one digit in the sixth column.
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)

            try {
              var target = "wasb:///HVACout2_testdebug1";
              rdd1.saveAsTextFile(target);
            } catch {
              case ex: Exception => {
                throw ex;
              }
            }
          }
        }


#### <a name="to-perform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="17df0-178">원격 디버깅 및 버그 수정을 수행하려면</span><span class="sxs-lookup"><span data-stu-id="17df0-178">To perform remote debugging and bug fixing</span></span>
1. <span data-ttu-id="17df0-179">두 개의 중단점을 설정하고 **디버그** 아이콘을 선택하여 원격 디버깅 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-179">Set up two breaking points, and then select the **Debug** icon to start the remote debugging process.</span></span>

2. <span data-ttu-id="17df0-180">첫 번째 중단점에서 코드가 중지되고 **변수** 창에 매개 변수 및 변수 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-180">The code stops at the first breaking point, and the parameter and variable information are shown in the **Variables** pane.</span></span> 

3. <span data-ttu-id="17df0-181">**프로그램 다시 시작** 아이콘을 선택하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-181">Select the **Resume Program** icon to continue.</span></span> <span data-ttu-id="17df0-182">두 번째 지점에서 코드가 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-182">The code stops at the second point.</span></span> <span data-ttu-id="17df0-183">예상대로 예외가 catch됩니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-183">The exception is caught as expected.</span></span>

  ![오류 throw](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-throw-error.png) 

4. <span data-ttu-id="17df0-185">**프로그램 다시 시작** 아이콘을 다시 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-185">Select the **Resume Program** icon again.</span></span> <span data-ttu-id="17df0-186">**HDInsight Spark 제출** 창에 “작업 실행 실패” 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-186">The **HDInsight Spark Submission** window displays a "job run failed" error.</span></span>

  ![오류 전송](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-error-submission.png) 

5. <span data-ttu-id="17df0-188">IntelliJ 디버깅 기능을 사용하여 변수 값을 동적으로 업데이트하려면 **디버그**를 다시 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-188">To dynamically update the variable value by using the IntelliJ debugging capability, select **Debug** again.</span></span> <span data-ttu-id="17df0-189">**변수** 창이 다시 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-189">The **Variables** pane appears again.</span></span> 

6. <span data-ttu-id="17df0-190">**디버그** 탭에서 대상을 마우스 오른쪽 단추로 클릭한 다음 **값 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-190">Right-click the target on the **Debug** tab, and then select **Set Value**.</span></span> <span data-ttu-id="17df0-191">다음으로 변수의 새 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-191">Next, enter a new value for the variable.</span></span> <span data-ttu-id="17df0-192">그런 다음 **Enter** 키를 선택하여 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-192">Then select **Enter** to save the value.</span></span> 

  ![값 설정](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-set-value.png) 

7. <span data-ttu-id="17df0-194">**프로그램 다시 시작** 아이콘을 선택하여 프로그램을 계속 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-194">Select the **Resume Program** icon to continue to run the program.</span></span> <span data-ttu-id="17df0-195">이번에는 예외가 catch되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-195">This time, no exception is caught.</span></span> <span data-ttu-id="17df0-196">예외 없이 프로젝트가 성공적으로 실행되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17df0-196">You can see that the project runs successfully without any exceptions.</span></span>

  ![예외 없이 디버그](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-without-exception.png)

## <span data-ttu-id="17df0-198"><a name="seealso"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="17df0-198"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="17df0-199">개요: Azure HDInsight에서 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="17df0-199">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="17df0-200">데모</span><span class="sxs-lookup"><span data-stu-id="17df0-200">Demo</span></span>
* <span data-ttu-id="17df0-201">Scala 프로젝트 만들기(비디오): [Spark Scala 응용 프로그램 만들기](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="17df0-201">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="17df0-202">원격 디버그(비디오): [IntelliJ용 Azure 도구 키트를 사용하여 HDInsight 클러스터에서 원격으로 Spark 응용 프로그램 디버그](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="17df0-202">Remote debug (video): [Use Azure Toolkit for IntelliJ to debug Spark applications remotely on an HDInsight cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="17df0-203">시나리오</span><span class="sxs-lookup"><span data-stu-id="17df0-203">Scenarios</span></span>
* [<span data-ttu-id="17df0-204">BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="17df0-204">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="17df0-205">기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="17df0-205">Spark with Machine Learning: Use Spark in HDInsight to analyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="17df0-206">기계 학습과 Spark: 음식 검사 결과를 예측하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="17df0-206">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="17df0-207">Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="17df0-207">Spark Streaming: Use Spark in HDInsight to build real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="17df0-208">HDInsight의 Spark를 사용하여 웹 사이트 로그 분석</span><span class="sxs-lookup"><span data-stu-id="17df0-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="17df0-209">응용 프로그램 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="17df0-209">Create and run applications</span></span>
* [<span data-ttu-id="17df0-210">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="17df0-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="17df0-211">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="17df0-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="17df0-212">도구 및 확장</span><span class="sxs-lookup"><span data-stu-id="17df0-212">Tools and extensions</span></span>
* [<span data-ttu-id="17df0-213">IntelliJ용 Azure 도구 키트를 사용하여 HDInsight 클러스터용 Spark 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="17df0-213">Use Azure Toolkit for IntelliJ to create Spark applications for an HDInsight cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="17df0-214">IntelliJ용 Azure 도구 키트를 사용하여 VPN을 통해 원격으로 Spark 응용 프로그램 디버그</span><span class="sxs-lookup"><span data-stu-id="17df0-214">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="17df0-215">Hortonworks 샌드박스에서 IntelliJ용 HDInsight Tools 사용</span><span class="sxs-lookup"><span data-stu-id="17df0-215">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="17df0-216">Eclipse용 Azure 도구 키트의 HDInsight 도구를 사용하여 Spark 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="17df0-216">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="17df0-217">HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용</span><span class="sxs-lookup"><span data-stu-id="17df0-217">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="17df0-218">HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널</span><span class="sxs-lookup"><span data-stu-id="17df0-218">Kernels available for Jupyter notebook in the Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="17df0-219">Jupyter 노트북에서 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="17df0-219">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="17df0-220">컴퓨터에 Jupyter를 설치하고 HDInsight Spark 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="17df0-220">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="17df0-221">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="17df0-221">Manage resources</span></span>
* [<span data-ttu-id="17df0-222">Azure HDInsight에서 Apache Spark 클러스터에 대한 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="17df0-222">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="17df0-223">HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그</span><span class="sxs-lookup"><span data-stu-id="17df0-223">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
