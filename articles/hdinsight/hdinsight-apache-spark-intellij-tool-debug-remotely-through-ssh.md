---
title: "IntelliJ용 Azure 도구 키트: SSH를 통해 원격으로 Spark 응용 프로그램 디버그 | Microsoft Docs"
description: "HDInsight에 원격으로 IntelliJ toodebug 응용 프로그램에 대 한 Azure 도구 키트의 HDInsight 도구 toouse SSH를 통해 클러스터 하는 방법에 대 한 단계별 지침"
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
ms.openlocfilehash: bf3ab9d04c2ff9fcb6bbbdeefb11f55a12fbd845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-spark-applications-on-an-hdinsight-cluster-with-azure-toolkit-for-intellij-through-ssh"></a><span data-ttu-id="3c147-104">IntelliJ용 Azure 도구 키트를 사용하여 SSH를 통해 HDInsight 클러스터에서 Spark 응용 프로그램 디버그</span><span class="sxs-lookup"><span data-stu-id="3c147-104">Debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH</span></span>

<span data-ttu-id="3c147-105">이 문서는 방법에 대 한 단계별 지침을 제공 하는 HDInsight 클러스터에 원격으로 IntelliJ toodebug 응용 프로그램에 대 한 Azure 도구 키트의 HDInsight 도구 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-105">This article provides step-by-step guidance on how toouse HDInsight Tools in Azure Toolkit for IntelliJ toodebug applications remotely on an HDInsight cluster.</span></span> <span data-ttu-id="3c147-106">toodebug 프로젝트 hello를 볼 수도 있습니다 [IntelliJ 용 Azure 도구 키트에 HDInsight Spark 디버그 응용 프로그램](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) 비디오.</span><span class="sxs-lookup"><span data-stu-id="3c147-106">toodebug your project, you can also view hello [Debug HDInsight Spark applications with Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) video.</span></span>

<span data-ttu-id="3c147-107">**필수 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="3c147-107">**Prerequisites**</span></span>

* <span data-ttu-id="3c147-108">**IntelliJ용 Azure 도구 키트의 HDInsight 도구**</span><span class="sxs-lookup"><span data-stu-id="3c147-108">**HDInsight Tools in Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="3c147-109">이 도구는 IntelliJ용 Azure 도구 키트의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-109">This tool is part of Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="3c147-110">자세한 내용은 [IntelliJ용 Azure 도구 키트 설치](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c147-110">For more information, see [Install Azure Toolkit for IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).</span></span>
* <span data-ttu-id="3c147-111">**IntelliJ용 Azure 도구 키트**</span><span class="sxs-lookup"><span data-stu-id="3c147-111">**Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="3c147-112">HDInsight 클러스터에 대 한이 도구 키트 toocreate Spark 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-112">Use this toolkit toocreate Spark applications for an HDInsight cluster.</span></span> <span data-ttu-id="3c147-113">자세한 내용은 hello 지침에 따라 [HDInsight 클러스터에 대 한 IntelliJ toocreate Spark 응용 프로그램에 대 한 Azure 도구 키트 사용](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin)합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-113">For more information, follow hello instructions in [Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).</span></span>
* <span data-ttu-id="3c147-114">**사용자 이름 및 암호 관리를 포함한 HDInsight SSH 서비스**.</span><span class="sxs-lookup"><span data-stu-id="3c147-114">**HDInsight SSH service with username and password management**.</span></span> <span data-ttu-id="3c147-115">자세한 내용은 참조 [SSH를 사용 하 여 tooHDInsight (Hadoop) 연결](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) 및 [UI, JobHistory, NameNode, Oozie, 및 기타 웹 Ui를 사용 하 여 SSH 터널링 tooaccess Ambari 웹](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel)합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-115">For more information, see [Connect tooHDInsight (Hadoop) by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Use SSH tunneling tooaccess Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel).</span></span> 
 

## <a name="create-a-spark-scala-application-and-configure-it-for-remote-debugging"></a><span data-ttu-id="3c147-116">Spark Scala 응용 프로그램을 만들고 원격 디버깅을 위해 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-116">Create a Spark Scala application and configure it for remote debugging</span></span>

1. <span data-ttu-id="3c147-117">IntelliJ IDEA를 시작하고 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-117">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="3c147-118">Hello에 **새 프로젝트** 대화 상자에서 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-118">In hello **New Project** dialog box, do hello following:</span></span>

   <span data-ttu-id="3c147-119">a.</span><span class="sxs-lookup"><span data-stu-id="3c147-119">a.</span></span> <span data-ttu-id="3c147-120">**HDInsight**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-120">Select **HDInsight**.</span></span> 

   <span data-ttu-id="3c147-121">b.</span><span class="sxs-lookup"><span data-stu-id="3c147-121">b.</span></span> <span data-ttu-id="3c147-122">기본 설정에 따라 Java 또는 Scala 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-122">Select a Java or Scala template based on your preference.</span></span> <span data-ttu-id="3c147-123">Hello 다음 옵션 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-123">Select between hello following options:</span></span>

      - <span data-ttu-id="3c147-124">**HDInsight의 Spark(Scala)**</span><span class="sxs-lookup"><span data-stu-id="3c147-124">**Spark on HDInsight (Scala)**</span></span>

      - <span data-ttu-id="3c147-125">**HDInsight의 Spark(Java)**</span><span class="sxs-lookup"><span data-stu-id="3c147-125">**Spark on HDInsight (Java)**</span></span>

      - <span data-ttu-id="3c147-126">**HDInsight의 Spark 클러스터 실행 샘플(Scala)** </span><span class="sxs-lookup"><span data-stu-id="3c147-126">**Spark on HDInsight Cluster Run Sample (Scala)**</span></span>

      <span data-ttu-id="3c147-127">이 예제에서는 **HDInsight의 Spark 클러스터 실행 샘플(Scala)** 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-127">This example uses a **Spark on HDInsight Cluster Run Sample (Scala)** template.</span></span>

   <span data-ttu-id="3c147-128">c.</span><span class="sxs-lookup"><span data-stu-id="3c147-128">c.</span></span> <span data-ttu-id="3c147-129">Hello에 **빌드 도구** 목록 hello tooyour 필요에 따라, 다음 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-129">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      - <span data-ttu-id="3c147-130">Scala 프로젝트 만들기 마법사 지원에 대해 **Maven**</span><span class="sxs-lookup"><span data-stu-id="3c147-130">**Maven**, for Scala project-creation wizard support</span></span>

      -  <span data-ttu-id="3c147-131">**SBT**, hello 종속성을 관리 하 고 hello Scala 프로젝트에 대 한 구성 하기 위한</span><span class="sxs-lookup"><span data-stu-id="3c147-131">**SBT**, for managing hello dependencies and building for hello Scala project</span></span> 

      ![디버그 프로젝트 만들기](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-create-projectfor-debug-remotely.png)

   <span data-ttu-id="3c147-133">d.</span><span class="sxs-lookup"><span data-stu-id="3c147-133">d.</span></span> <span data-ttu-id="3c147-134">**다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-134">Select **Next**.</span></span>     
 
3. <span data-ttu-id="3c147-135">Hello에 다음 **새 프로젝트** 창에서 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-135">In hello next **New Project** window, do hello following:</span></span>

   ![Hello Spark SDK를 선택 합니다.](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-new-project.png)

   <span data-ttu-id="3c147-137">a.</span><span class="sxs-lookup"><span data-stu-id="3c147-137">a.</span></span> <span data-ttu-id="3c147-138">프로젝트 이름과 프로젝트 위치를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-138">Enter a project name and project location.</span></span>

   <span data-ttu-id="3c147-139">b.</span><span class="sxs-lookup"><span data-stu-id="3c147-139">b.</span></span> <span data-ttu-id="3c147-140">Hello에 **프로젝트 SDK** 드롭 다운 목록 **Java 1.8** 에 대 한 **2.x 멤버** 클러스터 또는 선택 **Java 1.7** 에 대 한 **Spark 1입니다. x** 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-140">In hello **Project SDK** drop-down list, select **Java 1.8** for **Spark 2.x** cluster or select **Java 1.7** for **Spark 1.x** cluster.</span></span>

   <span data-ttu-id="3c147-141">c.</span><span class="sxs-lookup"><span data-stu-id="3c147-141">c.</span></span> <span data-ttu-id="3c147-142">Hello에 **Spark 버전** 드롭 다운 목록에서 hello Scala 프로젝트 만들기 마법사 Spark SDK 및 Scala SDK에 대 한 hello 올바른 버전을 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-142">In hello **Spark Version** drop-down list, hello Scala project creation wizard integrates hello correct version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="3c147-143">Hello spark 클러스터 버전이 2.0 보다 이전 이면 선택 **1.x 멤버**합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-143">If hello spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="3c147-144">그렇지 않은 경우 **Spark 2.x**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-144">Otherwise, select **Spark 2.x.**</span></span> <span data-ttu-id="3c147-145">이 예제에서는 **Spark 2.0.2(Scala 2.11.8)**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-145">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

   <span data-ttu-id="3c147-146">d.</span><span class="sxs-lookup"><span data-stu-id="3c147-146">d.</span></span> <span data-ttu-id="3c147-147">**마침**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-147">Select **Finish**.</span></span>

4. <span data-ttu-id="3c147-148">선택 **src** > **주** > **scala** tooopen hello 프로젝트의 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-148">Select **src** > **main** > **scala** tooopen your code in hello project.</span></span> <span data-ttu-id="3c147-149">이 예에서는 hello **SparkCore_wasbloTest** 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-149">This example uses hello **SparkCore_wasbloTest** script.</span></span>

5. <span data-ttu-id="3c147-150">tooaccess hello **구성 편집** 메뉴, hello 오른쪽 위 모서리에 있는 select hello 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-150">tooaccess hello **Edit Configurations** menu, select hello icon in hello upper-right corner.</span></span> <span data-ttu-id="3c147-151">이 메뉴에서 만들 수도 있고 원격 디버깅을 위해 hello 구성을 편집 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-151">From this menu, you can create or edit hello configurations for remote debugging.</span></span>

   ![구성 편집](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-edit-configurations.png) 

6. <span data-ttu-id="3c147-153">Hello에 **실행/디버그 구성을** 대화 상자, 선택 hello 더하기 기호 (**+**).</span><span class="sxs-lookup"><span data-stu-id="3c147-153">In hello **Run/Debug Configurations** dialog box, select hello plus sign (**+**).</span></span> <span data-ttu-id="3c147-154">다음 hello 선택 **Spark 작업 제출** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-154">Then select hello **Submit Spark Job** option.</span></span>

   ![새 구성 추가](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-add-new-Configuration.png)
7. <span data-ttu-id="3c147-156">**이름**, **Spark 클러스터** 및 **주 클래스 이름**에 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-156">Enter information for **Name**, **Spark cluster**, and **Main class name**.</span></span> <span data-ttu-id="3c147-157">그런 다음 **고급 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-157">Then select **Advanced configuration**.</span></span> 

   ![디버그 구성 실행](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-run-debug-configurations.png)

8. <span data-ttu-id="3c147-159">Hello에 **Spark 제출 고급 구성을** 대화 상자에서 **Spark 사용 원격 디버그**합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-159">In hello **Spark Submission Advanced Configuration** dialog box, select **Enable Spark remote debug**.</span></span> <span data-ttu-id="3c147-160">Hello SSH 사용자 이름을 입력 한 암호를 입력 하거나 개인 키 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-160">Enter hello SSH username, and then enter a password or use a private key file.</span></span> <span data-ttu-id="3c147-161">선택 toosave hello 구성 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-161">toosave hello configuration, select **OK**.</span></span>

   ![Spark 원격 디버그 설정](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-enable-spark-remote-debug.png)

9. <span data-ttu-id="3c147-163">이제 hello 구성 제공한 hello 이름으로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-163">hello configuration is now saved with hello name you provided.</span></span> <span data-ttu-id="3c147-164">tooview hello 구성 세부 사항은 선택 hello 구성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-164">tooview hello configuration details, select hello configuration name.</span></span> <span data-ttu-id="3c147-165">toomake 변경 선택 **구성 편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-165">toomake changes, select **Edit Configurations**.</span></span> 

10. <span data-ttu-id="3c147-166">Hello 구성 설정을 완료 한 후 hello 원격 클러스터에 대해 hello 프로젝트를 실행 하거나 원격 디버깅을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-166">After you complete hello configurations settings, you can run hello project against hello remote cluster or perform remote debugging.</span></span>

## <a name="learn-how-tooperform-remote-debugging"></a><span data-ttu-id="3c147-167">자세한 내용은 방법 tooperform 원격 디버깅</span><span class="sxs-lookup"><span data-stu-id="3c147-167">Learn how tooperform remote debugging</span></span>
### <a name="scenario-1-perform-remote-run"></a><span data-ttu-id="3c147-168">시나리오 1: 원격 실행 수행</span><span class="sxs-lookup"><span data-stu-id="3c147-168">Scenario 1: Perform remote run</span></span>

<span data-ttu-id="3c147-169">이 섹션에서는 보여줍니다 어떻게 toodebug 드라이버와 단일 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-169">In this section, we show you how toodebug drivers and executors.</span></span>

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
        /** Tracks hello total query count and number of aggregate bytes for a particular group. */
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


1. <span data-ttu-id="3c147-170">중단점을 설정 하 고 다음 hello 선택 **디버그** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-170">Set up breaking points, and then select hello **Debug** icon.</span></span>

   ![Hello 디버그 아이콘 선택](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-icon.png)

2. <span data-ttu-id="3c147-172">Hello 프로그램 실행 hello 주요 지점에 도달 하는 경우 참조는 **드라이버** 탭 및 두 개의 **실행자** hello 탭 **디버거** 창.</span><span class="sxs-lookup"><span data-stu-id="3c147-172">When hello program execution reaches hello breaking point, you see a **Driver** tab and two **Executor** tabs in hello **Debugger** pane.</span></span> <span data-ttu-id="3c147-173">선택 hello **Resume 프로그램** 다음 hello 다음 중단점에 도달 하 고 해당 하는 hello에 중점을 두고 hello 코드를 실행 하는 아이콘 toocontinue **실행자** 탭 합니다. Hello 해당 hello 실행 로그를 검토할 수 있습니다 **콘솔** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-173">Select hello **Resume Program** icon toocontinue running hello code, which then reaches hello next breakpoint and focuses on hello corresponding **Executor** tab. You can review hello execution logs on hello corresponding **Console** tab.</span></span>

   ![디버깅 탭](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debugger-tab.png)

### <a name="scenario-2-perform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="3c147-175">시나리오 2: 원격 디버깅 및 버그 수정 수행</span><span class="sxs-lookup"><span data-stu-id="3c147-175">Scenario 2: Perform remote debugging and bug fixing</span></span>
<span data-ttu-id="3c147-176">이 섹션에서는 보여줍니다 toodynamically 업데이트 hello를 사용 하 여 변수 값의 디버깅 기능을 해결 하는 방법에 대 한 IntelliJ hello 방법.</span><span class="sxs-lookup"><span data-stu-id="3c147-176">In this section, we show you how toodynamically update hello variable value by using hello IntelliJ debugging capability for a simple fix.</span></span> <span data-ttu-id="3c147-177">다음 코드 예제는 hello, hello 대상 파일이 이미 있기 때문에 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-177">In hello following code example, an exception is thrown because hello target file already exists.</span></span>
  
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext

        object SparkCore_WasbIOTest {
          def main(arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkCore_WasbIOTest")
            val sc = new SparkContext(conf)
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            // Find hello rows that have only one digit in hello sixth column.
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


#### <a name="tooperform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="3c147-178">tooperform 원격 디버깅 및 버그 수정</span><span class="sxs-lookup"><span data-stu-id="3c147-178">tooperform remote debugging and bug fixing</span></span>
1. <span data-ttu-id="3c147-179">두 중단점을 설정 하 고 다음 hello 선택 **디버그** 아이콘 toostart hello 원격 프로세스를 디버깅 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-179">Set up two breaking points, and then select hello **Debug** icon toostart hello remote debugging process.</span></span>

2. <span data-ttu-id="3c147-180">hello 코드 hello 첫 번째 주요 지점에서 중지 하 고 hello 매개 변수 및 변수 정보 hello 에서처럼 **변수** 창.</span><span class="sxs-lookup"><span data-stu-id="3c147-180">hello code stops at hello first breaking point, and hello parameter and variable information are shown in hello **Variables** pane.</span></span> 

3. <span data-ttu-id="3c147-181">선택 hello **Resume 프로그램** 아이콘 toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-181">Select hello **Resume Program** icon toocontinue.</span></span> <span data-ttu-id="3c147-182">hello 코드 hello 두 번째 요소에서 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-182">hello code stops at hello second point.</span></span> <span data-ttu-id="3c147-183">예상 대로 hello 예외가 검색 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-183">hello exception is caught as expected.</span></span>

  ![오류 throw](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-throw-error.png) 

4. <span data-ttu-id="3c147-185">선택 hello **Resume 프로그램** 아이콘을 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-185">Select hello **Resume Program** icon again.</span></span> <span data-ttu-id="3c147-186">hello **HDInsight Spark 제출** "작업 실행 실패" 오류 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-186">hello **HDInsight Spark Submission** window displays a "job run failed" error.</span></span>

  ![오류 전송](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-error-submission.png) 

5. <span data-ttu-id="3c147-188">toodynamically 업데이트 hello hello IntelliJ 디버깅 기능을 사용 하 여 변수 값을 선택 **디버그** 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-188">toodynamically update hello variable value by using hello IntelliJ debugging capability, select **Debug** again.</span></span> <span data-ttu-id="3c147-189">hello **변수** 창이 다시 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-189">hello **Variables** pane appears again.</span></span> 

6. <span data-ttu-id="3c147-190">Hello에서 마우스 오른쪽 단추로 클릭 hello 대상 **디버그** 탭을 선택한 다음 선택 **값 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-190">Right-click hello target on hello **Debug** tab, and then select **Set Value**.</span></span> <span data-ttu-id="3c147-191">다음으로 hello 변수에 대 한 새 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-191">Next, enter a new value for hello variable.</span></span> <span data-ttu-id="3c147-192">그런 다음 선택 **Enter** toosave hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-192">Then select **Enter** toosave hello value.</span></span> 

  ![값 설정](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-set-value.png) 

7. <span data-ttu-id="3c147-194">선택 hello **Resume 프로그램** 아이콘 toocontinue toorun hello 프로그램.</span><span class="sxs-lookup"><span data-stu-id="3c147-194">Select hello **Resume Program** icon toocontinue toorun hello program.</span></span> <span data-ttu-id="3c147-195">이번에는 예외가 catch되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-195">This time, no exception is caught.</span></span> <span data-ttu-id="3c147-196">모든 예외 없이 성공적으로 실행 되는 해당 hello 프로젝트를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-196">You can see that hello project runs successfully without any exceptions.</span></span>

  ![예외 없이 디버그](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-without-exception.png)

## <span data-ttu-id="3c147-198"><a name="seealso"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="3c147-198"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="3c147-199">개요: Azure HDInsight에서 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="3c147-199">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="3c147-200">데모</span><span class="sxs-lookup"><span data-stu-id="3c147-200">Demo</span></span>
* <span data-ttu-id="3c147-201">Scala 프로젝트 만들기(비디오): [Spark Scala 응용 프로그램 만들기](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="3c147-201">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="3c147-202">원격 디버그 (비디오): [HDInsight 클러스터에 원격으로 IntelliJ toodebug Spark 응용 프로그램에 대 한 Azure 도구 키트 사용](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="3c147-202">Remote debug (video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on an HDInsight cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="3c147-203">시나리오</span><span class="sxs-lookup"><span data-stu-id="3c147-203">Scenarios</span></span>
* [<span data-ttu-id="3c147-204">BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="3c147-204">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="3c147-205">Spark와 기계 학습: HVAC 데이터를 사용 하 여 온도 구축 하는 HDInsight tooanalyze에서 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="3c147-205">Spark with Machine Learning: Use Spark in HDInsight tooanalyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="3c147-206">Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark</span><span class="sxs-lookup"><span data-stu-id="3c147-206">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="3c147-207">HDInsight toobuild 실시간 스트리밍 응용 프로그램에서 사용 하 여 Spark Spark 스트리밍:</span><span class="sxs-lookup"><span data-stu-id="3c147-207">Spark Streaming: Use Spark in HDInsight toobuild real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="3c147-208">HDInsight의 Spark를 사용하여 웹 사이트 로그 분석</span><span class="sxs-lookup"><span data-stu-id="3c147-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="3c147-209">응용 프로그램 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="3c147-209">Create and run applications</span></span>
* [<span data-ttu-id="3c147-210">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="3c147-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="3c147-211">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="3c147-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="3c147-212">도구 및 확장</span><span class="sxs-lookup"><span data-stu-id="3c147-212">Tools and extensions</span></span>
* [<span data-ttu-id="3c147-213">Azure 도구 키트를 사용 하 여 HDInsight 클러스터에 대 한 IntelliJ toocreate Spark 응용 프로그램에 대 한</span><span class="sxs-lookup"><span data-stu-id="3c147-213">Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="3c147-214">Azure 도구 키트를 사용 하 여 VPN 통해 원격으로 IntelliJ toodebug Spark 응용 프로그램에 대 한</span><span class="sxs-lookup"><span data-stu-id="3c147-214">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="3c147-215">Hortonworks 샌드박스에서 IntelliJ용 HDInsight Tools 사용</span><span class="sxs-lookup"><span data-stu-id="3c147-215">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="3c147-216">Azure Toolkit for Eclipse toocreate Spark 응용 프로그램에서에서 사용 하 여 HDInsight 도구</span><span class="sxs-lookup"><span data-stu-id="3c147-216">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="3c147-217">HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용</span><span class="sxs-lookup"><span data-stu-id="3c147-217">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="3c147-218">HDInsight 용 Spark 클러스터 hello에서에서 Jupyter 노트북에 사용할 수 있는 커널</span><span class="sxs-lookup"><span data-stu-id="3c147-218">Kernels available for Jupyter notebook in hello Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="3c147-219">Jupyter 노트북에서 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="3c147-219">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="3c147-220">Jupyter 사용자 컴퓨터에 설치 하 고 tooan HDInsight Spark 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-220">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="3c147-221">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="3c147-221">Manage resources</span></span>
* [<span data-ttu-id="3c147-222">Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c147-222">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="3c147-223">HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그</span><span class="sxs-lookup"><span data-stu-id="3c147-223">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
