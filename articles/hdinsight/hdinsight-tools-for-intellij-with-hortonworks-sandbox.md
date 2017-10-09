---
title: "Hortonworks 샌드박스와 IntelliJ 용 Azure 도구 키트 aaaUse | Microsoft Docs"
description: "자세한 내용은 Hortonworks 샌드박스와 IntelliJ 용 Azure 도구 키트에서 toouse HDInsight 도구 방법입니다."
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
ms.openlocfilehash: 2bf97068a9cec99fcc7b4ff9469b91d8cbe2a8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a><span data-ttu-id="8476f-104">Hortonworks 샌드박스에서 IntelliJ용 HDInsight Tools 사용</span><span class="sxs-lookup"><span data-stu-id="8476f-104">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>

<span data-ttu-id="8476f-105">IntelliJ toodevelop Apache Scala 응용 프로그램 및 테스트에 대 한 toouse HDInsight 도구에 응용 프로그램을 hello 하는 방법에 대해 알아봅니다 [Hortonworks 샌드박스](http://hortonworks.com/products/sandbox/) 워크스테이션에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-105">Learn how toouse HDInsight Tools for IntelliJ toodevelop Apache Scala applications and then test hello applications on [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) running on your workstation.</span></span> 

<span data-ttu-id="8476f-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/)는 컴퓨터 소프트웨어를 개발하기 위한 Java IDE(통합 개발 환경)입니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) is a Java-integrated development environment (IDE) for developing computer software.</span></span> <span data-ttu-id="8476f-107">개발 하에서 Hortonworks 샌드박스 응용 프로그램을 테스트 한 후 이동할 수 있습니다 너무[Azure HDInsight](hdinsight-hadoop-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-107">After you have developed and tested your applications on Hortonworks Sandbox, you can move them too[Azure HDInsight](hdinsight-hadoop-introduction.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8476f-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8476f-108">Prerequisites</span></span>

<span data-ttu-id="8476f-109">이 자습서를 시작하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-109">Before you begin this tutorial, you must have:</span></span>

- <span data-ttu-id="8476f-110">로컬 환경에서 실행되는 Hortonworks 샌드박스의 HDP(Hortonworks Data Platform) 2.4.</span><span class="sxs-lookup"><span data-stu-id="8476f-110">Hortonworks Data Platform (HDP) 2.4 on Hortonworks Sandbox running on your local environment.</span></span> <span data-ttu-id="8476f-111">tooconfigure HDP, 참조 [가상 컴퓨터에서 Hadoop 샌드박스와 hello Hadoop 에코 시스템에서 시작](hdinsight-hadoop-emulator-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-111">tooconfigure HDP, see [Get started in hello Hadoop ecosystem with a Hadoop sandbox on a virtual machine](hdinsight-hadoop-emulator-get-started.md).</span></span> 
    >[!NOTE]
    ><span data-ttu-id="8476f-112">IntelliJ용 HDInsight Tools는 HDP 2.4에서만 테스트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-112">HDInsight Tools for IntelliJ has been tested only with HDP 2.4.</span></span> <span data-ttu-id="8476f-113">tooget HDP 2.4 확장 **Hortonworks 샌드박스 보관** hello에 [Hortonworks 샌드박스 다운로드 사이트](http://hortonworks.com/downloads/#sandbox)합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-113">tooget HDP 2.4, expand **Hortonworks Sandbox Archive** on hello [Hortonworks Sandbox downloads site](http://hortonworks.com/downloads/#sandbox).</span></span>

- <span data-ttu-id="8476f-114">[JDK(Java Developer Kit) 버전 1.8 이상](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="8476f-114">[Java Developer Kit (JDK) version 1.8 or later](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span> <span data-ttu-id="8476f-115">IntelliJ에 대 한 hello Azure 도구 키트 JDK가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-115">JDK is required by hello Azure Toolkit for IntelliJ.</span></span>

- <span data-ttu-id="8476f-116">[IntelliJ 아이디어 community edition](https://www.jetbrains.com/idea/download) hello로 [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) 플러그 인 및 hello [IntelliJ 용 Azure 도구 키트](../azure-toolkit-for-intellij.md) 플러그 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-116">[IntelliJ IDEA community edition](https://www.jetbrains.com/idea/download) with hello [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) plug-in and hello [Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md) plug-in.</span></span> <span data-ttu-id="8476f-117">IntelliJ 용 HDInsight 도구 hello IntelliJ 용 Azure 도구 키트의 일부분으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-117">HDInsight Tools for IntelliJ is available as a part of hello Azure Toolkit for IntelliJ.</span></span> 

  <span data-ttu-id="8476f-118">플러그 인 tooinstall hello, 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-118">tooinstall hello plug-ins, do hello following:</span></span>

  1. <span data-ttu-id="8476f-119">IntelliJ IDEA를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-119">Open IntelliJ IDEA.</span></span>
  2. <span data-ttu-id="8476f-120">Hello에 **시작** 화면에서 **구성**를 선택한 후 **플러그 인**합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-120">On hello **Welcome** screen, select **Configure**, and then select **Plugins**.</span></span>
  3. <span data-ttu-id="8476f-121">선택 **플러그 인 설치 JetBrains** hello 왼쪽 아래 모퉁이에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-121">Select **Install JetBrains plugin** in hello lower-left corner.</span></span>
  4. <span data-ttu-id="8476f-122">에 대 한 검색 함수 toosearch hello를 사용 하 여 **Scala**를 선택한 후 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-122">Use hello search function toosearch for **Scala**, and then select **Install**.</span></span>
  5. <span data-ttu-id="8476f-123">선택 **IntelliJ 아이디어를 다시 시작** toocomplete hello 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-123">Select **Restart IntelliJ IDEA** toocomplete hello installation.</span></span>
  6. <span data-ttu-id="8476f-124">4, 5 단계를 반복 tooinstall hello **IntelliJ 용 Azure 도구 키트**합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-124">Repeat step 4 and 5 tooinstall hello **Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="8476f-125">자세한 내용은 참조 [IntelliJ 용 Azure 도구 키트 설치 hello](../azure-toolkit-for-intellij-installation.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-125">For more information, see [Install hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="create-a-spark-scala-application"></a><span data-ttu-id="8476f-126">Spark Scala 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="8476f-126">Create a Spark Scala application</span></span>

<span data-ttu-id="8476f-127">이 섹션에서는 IntelliJ IDEA를 사용하여 샘플 Scala 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-127">In this section, you create a sample Scala project by using IntelliJ IDEA.</span></span> <span data-ttu-id="8476f-128">다음 섹션인 hello hello 프로젝트를 제출 하기 전에 IntelliJ 아이디어 toohello Hortonworks 샌드박스 (에뮬레이터)를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-128">In hello next section, you link IntelliJ IDEA toohello Hortonworks Sandbox (emulator) before you submit hello project.</span></span>

1. <span data-ttu-id="8476f-129">워크스테이션에서 IntelliJ IDEA를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-129">Open IntelliJ IDEA from your workstation.</span></span> <span data-ttu-id="8476f-130">Hello에 **새 프로젝트** 대화 상자에서 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-130">In hello **New Project** dialog box, do hello following:</span></span>

   <span data-ttu-id="8476f-131">a.</span><span class="sxs-lookup"><span data-stu-id="8476f-131">a.</span></span> <span data-ttu-id="8476f-132">**HDInsight** > **HDInsight의 Spark(Scala)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-132">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="8476f-133">b.</span><span class="sxs-lookup"><span data-stu-id="8476f-133">b.</span></span> <span data-ttu-id="8476f-134">Hello에 **빌드 도구** 목록 hello tooyour 필요에 따라, 다음 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-134">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

    * <span data-ttu-id="8476f-135">Scala 프로젝트 만들기 마법사 지원에 대해 **Maven**</span><span class="sxs-lookup"><span data-stu-id="8476f-135">**Maven**, for Scala project-creation wizard support</span></span>
    * <span data-ttu-id="8476f-136">**SBT**, hello 종속성을 관리 하 고 hello Scala 프로젝트에 대 한 구성 하기 위한</span><span class="sxs-lookup"><span data-stu-id="8476f-136">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

   ![hello 새 프로젝트 대화 상자](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. <span data-ttu-id="8476f-138">**다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-138">Select **Next**.</span></span>

3. <span data-ttu-id="8476f-139">Hello에 다음 **새 프로젝트** 대화 상자에서 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-139">In hello next **New Project** dialog box, do hello following:</span></span>

    ![IntelliJ Scala 프로젝트 속성 만들기](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    <span data-ttu-id="8476f-141">a.</span><span class="sxs-lookup"><span data-stu-id="8476f-141">a.</span></span> <span data-ttu-id="8476f-142">Hello에 **프로젝트 이름을** 상자에 프로젝트 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-142">In hello **Project name** box, enter a project name.</span></span>

    <span data-ttu-id="8476f-143">b.</span><span class="sxs-lookup"><span data-stu-id="8476f-143">b.</span></span> <span data-ttu-id="8476f-144">Hello에 **프로젝트 위치** 상자에 프로젝트 위치를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-144">In hello **Project location** box, enter a project location.</span></span>

    <span data-ttu-id="8476f-145">c.</span><span class="sxs-lookup"><span data-stu-id="8476f-145">c.</span></span> <span data-ttu-id="8476f-146">다음 toohello **프로젝트 SDK** 드롭 다운 목록 **새로**선택, **JDK**, Java JDK 버전 1.7 이상을의 hello 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-146">Next toohello **Project SDK** drop-down list, select **New**, select **JDK**, and then specify hello folder of Java JDK version 1.7 or later.</span></span> <span data-ttu-id="8476f-147">선택 **Java 1.8** hello Spark 2.x 클러스터 또는 선택에 대 한 **Java 1.7** hello Spark 1.x 클러스터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-147">Select **Java 1.8** for hello Spark 2.x cluster, or select **Java 1.7** for hello Spark 1.x cluster.</span></span> <span data-ttu-id="8476f-148">hello 기본 위치는 C:\Program Files\Java\jdk1.8.x_xxx입니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-148">hello default location is C:\Program Files\Java\jdk1.8.x_xxx.</span></span>

    <span data-ttu-id="8476f-149">d.</span><span class="sxs-lookup"><span data-stu-id="8476f-149">d.</span></span> <span data-ttu-id="8476f-150">Hello에 **Spark 버전** 드롭 다운 목록에서 Scala 프로젝트 만들기 마법사 Spark SDK 및 Scala SDK에 대 한 hello 적절 한 버전을 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-150">In hello **Spark version** drop-down list, Scala project creation wizard integrates hello proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="8476f-151">Hello Spark 클러스터 버전이 2.0 보다 이전 이면 선택 **1.x 멤버**합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-151">If hello Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="8476f-152">그렇지 않은 경우 **Spark2.x**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-152">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="8476f-153">이 예제에서는 Spark 1.6.2(Scala 2.10.5)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-153">This example uses Spark 1.6.2 (Scala 2.10.5).</span></span> <span data-ttu-id="8476f-154">Scala 표시 hello 저장소를 사용 하 고 있는지 확인 2.10.x 합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-154">Make sure that you are using hello repository marked Scala 2.10.x.</span></span> <span data-ttu-id="8476f-155">Scala 표시 hello 저장소를 사용 하지 마십시오 2.11.x 합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-155">Do not use hello repository marked Scala 2.11.x.</span></span>

4. <span data-ttu-id="8476f-156">**마침**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-156">Select **Finish**.</span></span>

5. <span data-ttu-id="8476f-157">경우 hello **프로젝트** 뷰가 이미 열려 있지 않으면, 키를 눌러 **Alt + 1** tooopen 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-157">If hello **Project** view is not already open, press **Alt+1** tooopen it.</span></span>

6. <span data-ttu-id="8476f-158">**프로젝트 탐색기**hello 프로젝트를 확장 한 다음 선택, **src**합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-158">In **Project Explorer**, expand hello project, and then select **src**.</span></span>

7. <span data-ttu-id="8476f-159">마우스 오른쪽 단추로 클릭 **src**, 너무 가리킨**새로**를 선택한 후 **Scala 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-159">Right-click **src**, point too**New**, and then select **Scala class**.</span></span>

8. <span data-ttu-id="8476f-160">Hello에 **이름** 상자 hello에 이름을 입력 합니다 **종류** 상자 **개체**를 선택한 후 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-160">In hello **Name** box, enter a name, in hello **Kind** box, select **Object**, and then select **OK**.</span></span>

    ![hello 새 Scala 클래스 만들기 창](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. <span data-ttu-id="8476f-162">Hello.scala 파일에서 코드 다음 hello를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-162">In hello .scala file, paste hello following code:</span></span>

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

10. <span data-ttu-id="8476f-163">Hello에 **빌드** 메뉴 선택 **빌드 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-163">On hello **Build** menu, select **Build project**.</span></span> <span data-ttu-id="8476f-164">Hello 컴파일 성공적으로 완료 되었음을 나타내는 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-164">Make sure that hello compilation has been completed successfully.</span></span>


## <a name="link-toohello-hortonworks-sandbox"></a><span data-ttu-id="8476f-165">Toohello Hortonworks 샌드박스 연결</span><span class="sxs-lookup"><span data-stu-id="8476f-165">Link toohello Hortonworks Sandbox</span></span>

<span data-ttu-id="8476f-166">Tooa Hortonworks 샌드박스 (에뮬레이터)를 클릭 하십시오. 기존 IntelliJ 응용 프로그램이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-166">Before you can link tooa Hortonworks Sandbox (emulator), you must have an existing IntelliJ application.</span></span>

<span data-ttu-id="8476f-167">toolink tooan 에뮬레이터 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-167">toolink tooan emulator, do hello following:</span></span>

1. <span data-ttu-id="8476f-168">IntelliJ에서 열기 hello 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-168">Open hello project in IntelliJ.</span></span>

2. <span data-ttu-id="8476f-169">Hello에 **보기** 메뉴 선택 **도구 창을**를 선택한 후 **Azure 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-169">On hello **View** menu, select **Tools Windows**, and then select **Azure Explorer**.</span></span>

3. <span data-ttu-id="8476f-170">**Azure**를 확장하고 **HDInsight**를 마우스 오른쪽 단추로 클릭한 다음 **에뮬레이터에 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-170">Expand **Azure**, right-click **HDInsight**, and then select **Link an Emulator**.</span></span>

4. <span data-ttu-id="8476f-171">Hello에 **링크는 새 에뮬레이터** 창의 hello Hortonworks 샌드박스의 hello 루트 계정에 대 한 구성 하 값 비슷한 toothose hello 스크린 샷, 뒤에 입력 한 다음 선택 하는 hello 암호를 입력 **확인** .</span><span class="sxs-lookup"><span data-stu-id="8476f-171">In hello **Link A New Emulator** window, enter hello password that you've configured for hello root account of hello Hortonworks Sandbox, enter values similar toothose in hello following screenshot, and then select **OK**.</span></span> 

   ![hello "링크는 새 에뮬레이터" 창](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. <span data-ttu-id="8476f-173">선택 tooconfigure hello 에뮬레이터 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-173">tooconfigure hello emulator, select **Yes**.</span></span>

<span data-ttu-id="8476f-174">Hello 에뮬레이터 성공적으로 연결 되 면 hello 에뮬레이터 (Hortonworks 샌드박스) hello HDInsight 노드에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-174">When hello emulator is connected successfully, hello emulator (Hortonworks Sandbox) is listed in hello HDInsight node.</span></span>

## <a name="submit-hello-spark-scala-application-toohello-hortonworks-sandbox"></a><span data-ttu-id="8476f-175">Hello Spark Scala 응용 프로그램 toohello Hortonworks 샌드박스 제출</span><span class="sxs-lookup"><span data-stu-id="8476f-175">Submit hello Spark Scala application toohello Hortonworks Sandbox</span></span>

<span data-ttu-id="8476f-176">IntelliJ 아이디어 toohello 에뮬레이터에 연결한 후에 프로젝트를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-176">After you have linked IntelliJ IDEA toohello emulator, you can submit your project.</span></span>

<span data-ttu-id="8476f-177">프로젝트 tooan 에뮬레이터 toosubmit 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-177">toosubmit a project tooan emulator, do hello following:</span></span>

1. <span data-ttu-id="8476f-178">**프로젝트 탐색기**를 hello 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 선택 **제출 Spark 응용 프로그램 tooHDInsight**합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-178">In **Project Explorer**, right-click hello project, and then select **Submit Spark application tooHDInsight**.</span></span>

2. <span data-ttu-id="8476f-179">다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-179">Do hello following:</span></span>

    <span data-ttu-id="8476f-180">a.</span><span class="sxs-lookup"><span data-stu-id="8476f-180">a.</span></span> <span data-ttu-id="8476f-181">Hello에 **Spark 클러스터 (Linux에만 해당)** 드롭 다운 목록에서 지역 Hortonworks 샌드박스에 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-181">In hello **Spark cluster (Linux only)** drop-down list, select your local Hortonworks Sandbox.</span></span>

    <span data-ttu-id="8476f-182">b.</span><span class="sxs-lookup"><span data-stu-id="8476f-182">b.</span></span> <span data-ttu-id="8476f-183">Hello에 **Main 클래스 이름** 상자의 선택 하거나 hello 주 클래스 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-183">In hello **Main class name** box, choose or enter hello main class name.</span></span> <span data-ttu-id="8476f-184">이 자습서에 대 한 hello 이름이 **GroupByTest**합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-184">For this tutorial, hello name is **GroupByTest**.</span></span>

3. <span data-ttu-id="8476f-185">**제출**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-185">Select **Submit**.</span></span> <span data-ttu-id="8476f-186">hello 작업 제출 로그 hello Spark 제출 도구 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-186">hello job submission logs are shown in hello Spark submission tool window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8476f-187">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8476f-187">Next steps</span></span>

- <span data-ttu-id="8476f-188">IntelliJ, 용 HDInsight 도구를 사용 하 여 HDInsight의 toocreate Spark에 응용 프로그램 너무 이동 toolearn[HDInsight Spark Linux 클러스터에 대 한 IntelliJ toocreate Spark 응용 프로그램에 대 한 Azure 도구 키트의 HDInsight 도구를 사용 하 여](hdinsight-apache-spark-intellij-tool-plugin.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-188">toolearn how toocreate Spark applications for HDInsight by using HDInsight Tools for IntelliJ, go too[Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate Spark applications for HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>

- <span data-ttu-id="8476f-189">IntelliJ, 용 HDInsight 도구에 대 한 비디오 toowatch 너무 이동[Spark 개발을 위한 IntelliJ 용 HDInsight 도구 소개](https://www.youtube.com/watch?v=YTZzYVgut6c)합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-189">toowatch a video of HDInsight Tools for IntelliJ, go too[Introduce HDInsight Tools for IntelliJ for Spark Development](https://www.youtube.com/watch?v=YTZzYVgut6c).</span></span>

- <span data-ttu-id="8476f-190">toolearn toodebug Spark 응용 프로그램을 사용 하 여 hello toolkit SSH 통해 HDInsight에 원격으로 어떻게 이동 너무[SSH 통해 IntelliJ 용 Azure 도구 키트에 HDInsight 클러스터에서 Spark 응용 프로그램을 원격으로 디버그](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-190">toolearn how toodebug Spark applications by using hello toolkit remotely on HDInsight through SSH, go too[Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span></span>

- <span data-ttu-id="8476f-191">toolearn toodebug Spark 응용 프로그램을 사용 하 여 VPN 통해 HDInsight에 원격으로 도구 키트 hello 방법 이동 너무[HDInsight Spark Linux 클러스터에 원격으로 IntelliJ toodebug Spark 응용 프로그램에 대 한 Azure 도구 키트의 HDInsight 도구를 사용 하 여](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-191">toolearn how toodebug Spark applications by using hello toolkit remotely on HDInsight through VPN, go too[Use HDInsight Tools in Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span></span>

- <span data-ttu-id="8476f-192">Eclipse toocreate Spark는 응용 프로그램에 대 한 HDInsight 도구 toouse 너무 이동 toolearn[Azure Toolkit for Eclipse toocreate Spark 응용 프로그램에서에서 사용 하 여 HDInsight 도구](hdinsight-apache-spark-eclipse-tool-plugin.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-192">toolearn how toouse HDInsight Tools for Eclipse toocreate a Spark application, go too[Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications](hdinsight-apache-spark-eclipse-tool-plugin.md).</span></span>

- <span data-ttu-id="8476f-193">Eclipse 용 HDInsight 도구에 대 한 비디오 toowatch 너무 이동[Eclipse toocreate Spark 응용 프로그램에 대 한 HDInsight 도구 사용](https://mix.office.com/watch/1rau2mopb6fha)합니다.</span><span class="sxs-lookup"><span data-stu-id="8476f-193">toowatch a video of HDInsight Tools for Eclipse, go too[Use HDInsight Tool for Eclipse toocreate Spark applications](https://mix.office.com/watch/1rau2mopb6fha).</span></span>
