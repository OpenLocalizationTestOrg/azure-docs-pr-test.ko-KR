---
title: "Hortonworks 샌드박스에서 IntelliJ용 Azure 도구 키트 사용 | Microsoft Docs"
description: "Hortonworks 샌드박스에서 IntelliJ용 Azure 도구 키트의 HDInsight Tools 사용 방법을 알아봅니다."
keywords: "hadoop 도구,hive 쿼리,intellij,hortonworks 샌드박스,intellij용 azure 도구 키트"
services: HDInsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: b587cc9b-a41a-49ac-998f-b54d6c0bdfe0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: c49f185db5a035f70a711bf309b973182d94a2b0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a><span data-ttu-id="e2892-104">Hortonworks 샌드박스에서 IntelliJ용 HDInsight Tools 사용</span><span class="sxs-lookup"><span data-stu-id="e2892-104">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>

<span data-ttu-id="e2892-105">IntelliJ용 HDInsight Tools를 사용하여 워크스테이션에서 실행되는 [Hortonworks 샌드박스](http://hortonworks.com/products/sandbox/)에서 Apache Scala 응용 프로그램을 개발한 다음 응용 프로그램을 테스트하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-105">Learn how to use HDInsight Tools for IntelliJ to develop Apache Scala applications and then test the applications on [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) running on your workstation.</span></span> 

<span data-ttu-id="e2892-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/)는 컴퓨터 소프트웨어를 개발하기 위한 Java IDE(통합 개발 환경)입니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) is a Java-integrated development environment (IDE) for developing computer software.</span></span> <span data-ttu-id="e2892-107">Hortonworks 샌드박스에서 응용 프로그램을 개발하고 테스트한 후에 [Azure HDInsight](hdinsight-hadoop-introduction.md)로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-107">After you have developed and tested your applications on Hortonworks Sandbox, you can move them to [Azure HDInsight](hdinsight-hadoop-introduction.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2892-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e2892-108">Prerequisites</span></span>

<span data-ttu-id="e2892-109">이 자습서를 시작하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-109">Before you begin this tutorial, you must have:</span></span>

- <span data-ttu-id="e2892-110">로컬 환경에서 실행되는 Hortonworks 샌드박스의 HDP(Hortonworks Data Platform) 2.4.</span><span class="sxs-lookup"><span data-stu-id="e2892-110">Hortonworks Data Platform (HDP) 2.4 on Hortonworks Sandbox running on your local environment.</span></span> <span data-ttu-id="e2892-111">HDP를 구성하려면 [가상 컴퓨터에서 Hadoop 샌드박스를 사용하여 Hadoop 에코 시스템 시작](hdinsight-hadoop-emulator-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e2892-111">To configure HDP, see [Get started in the Hadoop ecosystem with a Hadoop sandbox on a virtual machine](hdinsight-hadoop-emulator-get-started.md).</span></span> 
    >[!NOTE]
    ><span data-ttu-id="e2892-112">IntelliJ용 HDInsight Tools는 HDP 2.4에서만 테스트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-112">HDInsight Tools for IntelliJ has been tested only with HDP 2.4.</span></span> <span data-ttu-id="e2892-113">HDP 2.4를 가져오려면 [Hortonworks 샌드박스 다운로드 사이트](http://hortonworks.com/downloads/#sandbox)에서 **Hortonworks 샌드박스 보관**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-113">To get HDP 2.4, expand **Hortonworks Sandbox Archive** on the [Hortonworks Sandbox downloads site](http://hortonworks.com/downloads/#sandbox).</span></span>

- <span data-ttu-id="e2892-114">[JDK(Java Developer Kit) 버전 1.8 이상](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="e2892-114">[Java Developer Kit (JDK) version 1.8 or later](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span> <span data-ttu-id="e2892-115">JDK는 IntelliJ용 Azure 도구 키트에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-115">JDK is required by the Azure Toolkit for IntelliJ.</span></span>

- <span data-ttu-id="e2892-116">[IntelliJ IDEA Community Edition](https://www.jetbrains.com/idea/download)과 [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) 플러그 인 및 [IntelliJ용 Azure 도구 키트](../azure-toolkit-for-intellij.md) 플러그 인.</span><span class="sxs-lookup"><span data-stu-id="e2892-116">[IntelliJ IDEA community edition](https://www.jetbrains.com/idea/download) with the [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) plug-in and the [Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md) plug-in.</span></span> <span data-ttu-id="e2892-117">IntelliJ용 HDInsight Tools는 IntelliJ용 Azure 도구 키트의 일부로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-117">HDInsight Tools for IntelliJ is available as a part of the Azure Toolkit for IntelliJ.</span></span> 

  <span data-ttu-id="e2892-118">플러그 인을 설치하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-118">To install the plug-ins, do the following:</span></span>

  1. <span data-ttu-id="e2892-119">IntelliJ IDEA를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-119">Open IntelliJ IDEA.</span></span>
  2. <span data-ttu-id="e2892-120">**시작** 화면에서 **구성**을 선택한 다음 **플러그 인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-120">On the **Welcome** screen, select **Configure**, and then select **Plugins**.</span></span>
  3. <span data-ttu-id="e2892-121">왼쪽 아래 모서리에서 **JetBrains 플러그 인 설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-121">Select **Install JetBrains plugin** in the lower-left corner.</span></span>
  4. <span data-ttu-id="e2892-122">검색 기능을 사용하여 **Scala**를 검색한 후 **설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-122">Use the search function to search for **Scala**, and then select **Install**.</span></span>
  5. <span data-ttu-id="e2892-123">**IntelliJ IDEA 다시 시작**을 선택하여 설치를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-123">Select **Restart IntelliJ IDEA** to complete the installation.</span></span>
  6. <span data-ttu-id="e2892-124">4~5단계를 반복하여 **IntelliJ용 Azure 도구 키트**를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-124">Repeat step 4 and 5 to install the **Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="e2892-125">자세한 내용은 [IntelliJ용 Azure 도구 키트 설치](../azure-toolkit-for-intellij-installation.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e2892-125">For more information, see [Install the Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="create-a-spark-scala-application"></a><span data-ttu-id="e2892-126">Spark Scala 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="e2892-126">Create a Spark Scala application</span></span>

<span data-ttu-id="e2892-127">이 섹션에서는 IntelliJ IDEA를 사용하여 샘플 Scala 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-127">In this section, you create a sample Scala project by using IntelliJ IDEA.</span></span> <span data-ttu-id="e2892-128">다음 섹션에서는 프로젝트를 제출하기 전에 Hortonworks 샌드박스(에뮬레이터)에 IntelliJ IDEA를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-128">In the next section, you link IntelliJ IDEA to the Hortonworks Sandbox (emulator) before you submit the project.</span></span>

1. <span data-ttu-id="e2892-129">워크스테이션에서 IntelliJ IDEA를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-129">Open IntelliJ IDEA from your workstation.</span></span> <span data-ttu-id="e2892-130">**새 프로젝트** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-130">In the **New Project** dialog box, do the following:</span></span>

   <span data-ttu-id="e2892-131">a.</span><span class="sxs-lookup"><span data-stu-id="e2892-131">a.</span></span> <span data-ttu-id="e2892-132">**HDInsight** > **HDInsight의 Spark(Scala)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-132">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="e2892-133">b.</span><span class="sxs-lookup"><span data-stu-id="e2892-133">b.</span></span> <span data-ttu-id="e2892-134">**빌드 도구** 목록에서 요구 사항에 따라 다음 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-134">In the **Build tool** list, select either of the following, according to your need:</span></span>

    * <span data-ttu-id="e2892-135">Scala 프로젝트 만들기 마법사 지원에 대해 **Maven**</span><span class="sxs-lookup"><span data-stu-id="e2892-135">**Maven**, for Scala project-creation wizard support</span></span>
    * <span data-ttu-id="e2892-136">종속성 관리 및 Scala 프로젝트에 대한 빌드에 대해 **SBT**</span><span class="sxs-lookup"><span data-stu-id="e2892-136">**SBT**, for managing the dependencies and building for the Scala project</span></span>

   ![새 프로젝트 대화 상자](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. <span data-ttu-id="e2892-138">**다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-138">Select **Next**.</span></span>

3. <span data-ttu-id="e2892-139">다음 **새 프로젝트** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-139">In the next **New Project** dialog box, do the following:</span></span>

    ![IntelliJ Scala 프로젝트 속성 만들기](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    <span data-ttu-id="e2892-141">a.</span><span class="sxs-lookup"><span data-stu-id="e2892-141">a.</span></span> <span data-ttu-id="e2892-142">**프로젝트 이름** 상자에 프로젝트 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-142">In the **Project name** box, enter a project name.</span></span>

    <span data-ttu-id="e2892-143">b.</span><span class="sxs-lookup"><span data-stu-id="e2892-143">b.</span></span> <span data-ttu-id="e2892-144">**프로젝트 위치** 상자에 프로젝트 위치를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-144">In the **Project location** box, enter a project location.</span></span>

    <span data-ttu-id="e2892-145">c.</span><span class="sxs-lookup"><span data-stu-id="e2892-145">c.</span></span> <span data-ttu-id="e2892-146">**프로젝트 SDK** 드롭다운 목록 옆의 **새로 만들기**를 선택하고 **JDK**를 선택한 다음 Java JDK 버전 1.7 이상의 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-146">Next to the **Project SDK** drop-down list, select **New**, select **JDK**, and then specify the folder of Java JDK version 1.7 or later.</span></span> <span data-ttu-id="e2892-147">Spark 2.x 클러스터에 대해 **Java 1.8**을 선택하거나 Spark 1.x 클러스터에 대해 **Java 1.7**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-147">Select **Java 1.8** for the Spark 2.x cluster, or select **Java 1.7** for the Spark 1.x cluster.</span></span> <span data-ttu-id="e2892-148">기본 위치는 C:\Program Files\Java\jdk1.8.x_xxx입니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-148">The default location is C:\Program Files\Java\jdk1.8.x_xxx.</span></span>

    <span data-ttu-id="e2892-149">d.</span><span class="sxs-lookup"><span data-stu-id="e2892-149">d.</span></span> <span data-ttu-id="e2892-150">**Spark 버전** 드롭다운 목록에서 Scala 프로젝트 생성 마법사는 Spark SDK 및 Scala SDK에 대한 적절한 버전을 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-150">In the **Spark version** drop-down list, Scala project creation wizard integrates the proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="e2892-151">Spark 클러스터 2.0 이하 버전을 사용하는 경우 **Spark 1.x**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-151">If the Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="e2892-152">그렇지 않은 경우 **Spark 2.x**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-152">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="e2892-153">이 예제에서는 Spark 1.6.2(Scala 2.10.5)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-153">This example uses Spark 1.6.2 (Scala 2.10.5).</span></span> <span data-ttu-id="e2892-154">Scala 2.10.x가 표시된 리포지토리를 사용하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-154">Make sure that you are using the repository marked Scala 2.10.x.</span></span> <span data-ttu-id="e2892-155">Scala 2.11.x가 표시된 리포지토리를 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="e2892-155">Do not use the repository marked Scala 2.11.x.</span></span>

4. <span data-ttu-id="e2892-156">**마침**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-156">Select **Finish**.</span></span>

5. <span data-ttu-id="e2892-157">**프로젝트** 뷰가 열려 있지 않은 경우 **Alt + 1** 키를 눌러 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-157">If the **Project** view is not already open, press **Alt+1** to open it.</span></span>

6. <span data-ttu-id="e2892-158">**프로젝트 탐색기**에서 프로젝트를 확장한 다음 **src**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-158">In **Project Explorer**, expand the project, and then select **src**.</span></span>

7. <span data-ttu-id="e2892-159">**src**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **Scala 클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-159">Right-click **src**, point to **New**, and then select **Scala class**.</span></span>

8. <span data-ttu-id="e2892-160">**이름** 상자에 이름을 입력하고 **종류** 상자에서 **개체**를 선택한 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-160">In the **Name** box, enter a name, in the **Kind** box, select **Object**, and then select **OK**.</span></span>

    ![새 Scala 클래스 만들기 창](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. <span data-ttu-id="e2892-162">.scala 파일에서 다음 코드를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-162">In the .scala file, paste the following code:</span></span>

        import java.util.Random
        import org.apache.spark.{SparkConf, SparkContext}
        import org.apache.spark.SparkContext._

        /**
        * Usage: GroupByTest [numMappers] [numKVPairs] [valSize] [numReducers]
        */
        object GroupByTest {
            def main(args: Array[String]) {
                val sparkConf = new SparkConf().setAppName("GroupBy Test")
                var numMappers = 3
                var numKVPairs = 10
                var valSize = 10
                var numReducers = 2

                val sc = new SparkContext(sparkConf)

                val pairs1 = sc.parallelize(0 until numMappers, numMappers).flatMap { p =>
                val ranGen = new Random
                var arr1 = new Array[(Int, Array[Byte])](numKVPairs)
                for (i <- 0 until numKVPairs) {
                    val byteArr = new Array[Byte](valSize)
                    ranGen.nextBytes(byteArr)
                    arr1(i) = (ranGen.nextInt(Int.MaxValue), byteArr)
                }
                arr1
                }.cache
                // Enforce that everything has been calculated and in cache
                pairs1.count

                println(pairs1.groupByKey(numReducers).count)
            }
        }

10. <span data-ttu-id="e2892-163">**빌드** 메뉴에서 **프로젝트 빌드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-163">On the **Build** menu, select **Build project**.</span></span> <span data-ttu-id="e2892-164">컴파일이 성공적으로 완료되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-164">Make sure that the compilation has been completed successfully.</span></span>


## <a name="link-to-the-hortonworks-sandbox"></a><span data-ttu-id="e2892-165">Hortonworks 샌드박스에 연결</span><span class="sxs-lookup"><span data-stu-id="e2892-165">Link to the Hortonworks Sandbox</span></span>

<span data-ttu-id="e2892-166">Hortonworks 샌드박스(에뮬레이터)에 연결하려면 기존 IntelliJ 응용 프로그램이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-166">Before you can link to a Hortonworks Sandbox (emulator), you must have an existing IntelliJ application.</span></span>

<span data-ttu-id="e2892-167">에뮬레이터에 연결하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-167">To link to an emulator, do the following:</span></span>

1. <span data-ttu-id="e2892-168">IntelliJ에서 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-168">Open the project in IntelliJ.</span></span>

2. <span data-ttu-id="e2892-169">**보기** 메뉴에서 **도구 창**, **Azure 탐색기**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-169">On the **View** menu, select **Tools Windows**, and then select **Azure Explorer**.</span></span>

3. <span data-ttu-id="e2892-170">**Azure**를 확장하고 **HDInsight**를 마우스 오른쪽 단추로 클릭한 다음 **에뮬레이터에 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-170">Expand **Azure**, right-click **HDInsight**, and then select **Link an Emulator**.</span></span>

4. <span data-ttu-id="e2892-171">**새 에뮬레이터 연결** 창에서 Hortonworks 샌드박스의 루트 계정에 대해 구성한 암호를 입력하고 다음 스크린샷의 값과 유사한 값을 입력한 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-171">In the **Link A New Emulator** window, enter the password that you've configured for the root account of the Hortonworks Sandbox, enter values similar to those in the following screenshot, and then select **OK**.</span></span> 

   !["새 에뮬레이터 연결" 창](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. <span data-ttu-id="e2892-173">에뮬레이터를 구성하려면 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-173">To configure the emulator, select **Yes**.</span></span>

<span data-ttu-id="e2892-174">에뮬레이터가 성공적으로 연결되면 HDInsight 노드에 에뮬레이터(Hortonworks 샌드박스)가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-174">When the emulator is connected successfully, the emulator (Hortonworks Sandbox) is listed in the HDInsight node.</span></span>

## <a name="submit-the-spark-scala-application-to-the-hortonworks-sandbox"></a><span data-ttu-id="e2892-175">Hortonworks 샌드박스에 Spark Scala 응용 프로그램 제출</span><span class="sxs-lookup"><span data-stu-id="e2892-175">Submit the Spark Scala application to the Hortonworks Sandbox</span></span>

<span data-ttu-id="e2892-176">IntelliJ IDEA를 에뮬레이터에 연결한 후에는 프로젝트를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-176">After you have linked IntelliJ IDEA to the emulator, you can submit your project.</span></span>

<span data-ttu-id="e2892-177">에뮬레이터에 프로젝트를 제출하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-177">To submit a project to an emulator, do the following:</span></span>

1. <span data-ttu-id="e2892-178">**프로젝트 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **HDInsight에 Spark 응용 프로그램 제출**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-178">In **Project Explorer**, right-click the project, and then select **Submit Spark application to HDInsight**.</span></span>

2. <span data-ttu-id="e2892-179">다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-179">Do the following:</span></span>

    <span data-ttu-id="e2892-180">a.</span><span class="sxs-lookup"><span data-stu-id="e2892-180">a.</span></span> <span data-ttu-id="e2892-181">**Spark 클러스터(Linux만 해당)** 드롭다운 목록에서 로컬 Hortonworks 샌드박스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-181">In the **Spark cluster (Linux only)** drop-down list, select your local Hortonworks Sandbox.</span></span>

    <span data-ttu-id="e2892-182">b.</span><span class="sxs-lookup"><span data-stu-id="e2892-182">b.</span></span> <span data-ttu-id="e2892-183">**기본 클래스 이름** 상자에서 기본 클래스 이름을 선택하거나 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-183">In the **Main class name** box, choose or enter the main class name.</span></span> <span data-ttu-id="e2892-184">이 자습서의 경우 이름은 **GroupByTest**입니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-184">For this tutorial, the name is **GroupByTest**.</span></span>

3. <span data-ttu-id="e2892-185">**제출**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-185">Select **Submit**.</span></span> <span data-ttu-id="e2892-186">작업 제출 로그가 Spark 제출 도구 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2892-186">The job submission logs are shown in the Spark submission tool window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2892-187">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e2892-187">Next steps</span></span>

- <span data-ttu-id="e2892-188">IntelliJ용 HDInsight Tools를 사용하여 HDInsight용 Spark 응용 프로그램을 만드는 방법을 알아보려면 [IntelliJ용 Azure 도구 키트의 HDInsight 도구를 사용하여 HDInsight Spark Linux 클러스터용 Spark 응용 프로그램 만들기](hdinsight-apache-spark-intellij-tool-plugin.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="e2892-188">To learn how to create Spark applications for HDInsight by using HDInsight Tools for IntelliJ, go to [Use HDInsight Tools in Azure Toolkit for IntelliJ to create Spark applications for HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>

- <span data-ttu-id="e2892-189">IntelliJ용 HDInsight Toolos 관련 비디오를 시청하려면 [Spark 개발을 위한 IntelliJ용 HDInsight Tools 소개](https://www.youtube.com/watch?v=YTZzYVgut6c)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="e2892-189">To watch a video of HDInsight Tools for IntelliJ, go to [Introduce HDInsight Tools for IntelliJ for Spark Development](https://www.youtube.com/watch?v=YTZzYVgut6c).</span></span>

- <span data-ttu-id="e2892-190">SSH를 통해 HDInsight에서 원격으로 이 도구 키트를 사용하여 Spark 응용 프로그램을 디버그하는 방법을 알아보려면 [IntelliJ용 Azure 도구 키트를 사용하여 SSH를 통해 HDInsight 클러스터에서 원격으로 Spark 응용 프로그램 디버그](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="e2892-190">To learn how to debug Spark applications by using the toolkit remotely on HDInsight through SSH, go to [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span></span>

- <span data-ttu-id="e2892-191">VPN을 통해 HDInsight에서 원격으로 이 도구 키트를 사용하여 Spark 응용 프로그램을 디버그하는 방법을 알아보려면 [HDInsight Spark Linux 클러스터에서 IntelliJ용 Azure 도구 키트의 HDInsight Tools를 사용하여 Spark 응용 프로그램을 원격으로 디버그](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="e2892-191">To learn how to debug Spark applications by using the toolkit remotely on HDInsight through VPN, go to [Use HDInsight Tools in Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span></span>

- <span data-ttu-id="e2892-192">Eclipse용 HDInsight Tools를 사용하여 Spark 응용 프로그램을 만드는 방법을 알아보려면 [Eclipse용 Azure 도구 키트의 HDInsight Tools를 사용하여 Spark 응용 프로그램 만들기](hdinsight-apache-spark-eclipse-tool-plugin.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="e2892-192">To learn how to use HDInsight Tools for Eclipse to create a Spark application, go to [Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications](hdinsight-apache-spark-eclipse-tool-plugin.md).</span></span>

- <span data-ttu-id="e2892-193">Eclipse용 HDInsight Tools 관련 비디오를 시청하려면 [Eclipse용 HDInsight Tools를 사용하여 Spark 응용 프로그램 만들기](https://mix.office.com/watch/1rau2mopb6fha)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="e2892-193">To watch a video of HDInsight Tools for Eclipse, go to [Use HDInsight Tool for Eclipse to create Spark applications](https://mix.office.com/watch/1rau2mopb6fha).</span></span>
