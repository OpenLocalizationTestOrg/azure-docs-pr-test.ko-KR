---
title: "Spark 클러스터에서 실행되는 Scala 앱 만들기 - Azure HDInsight | Microsoft Docs"
description: "Apache Maven을 빌드 시스템으로 사용하여 Scala에서 작성된 Spark 응용 프로그램 및 IntelliJ IDEA에서 제공하는 Scala에 대한 기존 Maven 원형을 만듭니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b2467a40-a340-4b80-bb00-f2c3339db57b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: 95dba08744357f8800b05e3d4b892e3a363d5985
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-scala-maven-application-to-run-on-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="31458-103">HDInsight의 Apache Spark 클러스터에서 실행할 Scala Maven 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="31458-103">Create a Scala Maven application to run on Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="31458-104">IntelliJ IDEA에서 Maven을 사용하여 Scala로 작성한 Spark 응용 프로그램을 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="31458-104">Learn how to create a Spark application written in Scala using Maven with IntelliJ IDEA.</span></span> <span data-ttu-id="31458-105">문서는 빌드 시스템으로 Apache Maven을 사용하고 IntelliJ IDEA에서 제공하는 Scala에 대한 기존 Maven 원형으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-105">The article uses Apache Maven as the build system and starts with an existing Maven archetype for Scala provided by IntelliJ IDEA.</span></span>  <span data-ttu-id="31458-106">IntelliJ IDEA에서 Scala 응용 프로그램 만들기는 다음 단계를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-106">Creating a Scala application in IntelliJ IDEA involves the following steps:</span></span>

* <span data-ttu-id="31458-107">빌드 시스템으로 Maven을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-107">Use Maven as the build system.</span></span>
* <span data-ttu-id="31458-108">POM(프로젝트 개체 모델) 파일을 업데이트하여 Spark 모듈 종속성을 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-108">Update Project Object Model (POM) file to resolve Spark module dependencies.</span></span>
* <span data-ttu-id="31458-109">Scala에서 응용 프로그램을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-109">Write your application in Scala.</span></span>
* <span data-ttu-id="31458-110">HDInsight Spark 클러스터에 제출할 수 있는 jar 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-110">Generate a jar file that can be submitted to HDInsight Spark clusters.</span></span>
* <span data-ttu-id="31458-111">Livy를 사용하여 Spark 클러스터에서 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-111">Run the application on Spark cluster using Livy.</span></span>

> [!NOTE]
> <span data-ttu-id="31458-112">또한 HDInsight는 Linux의 HDInsight Spark 클러스터에 대한 응용 프로그램을 만들고 제출하는 과정을 용이하게 하는 IntelliJ IDEA 플러그 인 도구를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-112">HDInsight also provides an IntelliJ IDEA plugin tool to ease the process of creating and submitting applications to an HDInsight Spark cluster on Linux.</span></span> <span data-ttu-id="31458-113">자세한 내용은 [IntelliJ IDEA용 HDInsight 도구 플러그 인을 사용하여 Spark 응용 프로그램 만들기 및 제출](hdinsight-apache-spark-intellij-tool-plugin.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31458-113">For more information, see [Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark applications](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="31458-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="31458-114">Prerequisites</span></span>

* <span data-ttu-id="31458-115">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="31458-115">An Azure subscription.</span></span> <span data-ttu-id="31458-116">[Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31458-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="31458-117">HDInsight의 Apache Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="31458-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="31458-118">자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31458-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="31458-119">Oracle Java Development 키트.</span><span class="sxs-lookup"><span data-stu-id="31458-119">Oracle Java Development kit.</span></span> <span data-ttu-id="31458-120">[여기](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31458-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="31458-121">Java IDE.</span><span class="sxs-lookup"><span data-stu-id="31458-121">A Java IDE.</span></span> <span data-ttu-id="31458-122">이 문서에서는 IntelliJ IDEA 15.0.1을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-122">This article uses IntelliJ IDEA 15.0.1.</span></span> <span data-ttu-id="31458-123">[여기](https://www.jetbrains.com/idea/download/)에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31458-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-scala-plugin-for-intellij-idea"></a><span data-ttu-id="31458-124">IntelliJ IDEA용 Scala 플러그 인 설치</span><span class="sxs-lookup"><span data-stu-id="31458-124">Install Scala plugin for IntelliJ IDEA</span></span>
<span data-ttu-id="31458-125">IntelliJ IDEA 설치가 Scala 플러그 인 활성화를 묻지 않은 경우 IntelliJ IDEA를 시작하고 다음 단계를 진행하여 플러그 인을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-125">If IntelliJ IDEA installation did not not prompt for enabling Scala plugin, launch IntelliJ IDEA and go through the following steps to install the plugin:</span></span>

1. <span data-ttu-id="31458-126">IntelliJ IDEA를 시작하고 시작 화면에서 **구성**을 클릭한 다음 **플러그 인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-126">Start IntelliJ IDEA and from welcome screen click **Configure** and then click **Plugins**.</span></span>
   
    ![scala 플러그 인 활성화](./media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. <span data-ttu-id="31458-128">다음 화면에서 왼쪽 아래 모서리에서 **JetBrains 플러그 인 설치** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-128">In the next screen, click **Install JetBrains plugin** from the lower left corner.</span></span> <span data-ttu-id="31458-129">열린 **JetBrains 플러그 인 찾아보기** 대화 상자에서Scala를 검색한 다음 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-129">In the **Browse JetBrains Plugins** dialog box that opens, search for Scala and then click **Install**.</span></span>
   
    ![scala 플러그 인 설치](./media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. <span data-ttu-id="31458-131">플러그 인이 성공적으로 설치되면 **IntelliJ IDEA 다시 시작 단추** 를 클릭하여 IDE를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-131">After the plugin installs successfully, click the **Restart IntelliJ IDEA button** to restart the IDE.</span></span>

## <a name="create-a-standalone-scala-project"></a><span data-ttu-id="31458-132">독립 실행형 Scala 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="31458-132">Create a standalone Scala project</span></span>
1. <span data-ttu-id="31458-133">IntelliJ IDEA를 시작하고 새 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31458-133">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="31458-134">새 프로젝트 대화 상자에서 다음과 같이 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-134">In the new project dialog box, make the following choices, and then click **Next**.</span></span>
   
    ![Maven 프로젝트 만들기](./media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * <span data-ttu-id="31458-136">프로젝트 유형으로 **Maven** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-136">Select **Maven** as the project type.</span></span>
   * <span data-ttu-id="31458-137">**프로젝트 SDK**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-137">Specify a **Project SDK**.</span></span> <span data-ttu-id="31458-138">새로 만들기를 클릭하여 Java 설치 디렉터리, 일반적으로 `C:\Program Files\Java\jdk1.8.0_66`(으)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-138">Click New and navigate to the Java installation directory, typically `C:\Program Files\Java\jdk1.8.0_66`.</span></span>
   * <span data-ttu-id="31458-139">**원형으로부터 만들기** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-139">Select the **Create from archetype** option.</span></span>
   * <span data-ttu-id="31458-140">원형 목록에서 **org.scala-tools.archetypes:scala-archetype-simple**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-140">From the list of archetypes, select **org.scala-tools.archetypes:scala-archetype-simple**.</span></span> <span data-ttu-id="31458-141">이는 올바른 디렉터리 구조를 만들고 Scala 프로그램 작성에 필요한 기본 종속성을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-141">This will create the right directory structure and download the required default dependencies to write Scala program.</span></span>
2. <span data-ttu-id="31458-142">**GroupId**, **ArtifactId** 및 **버전**에 관련 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-142">Provide relevant values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="31458-143">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="31458-143">Click **Next**.</span></span>
3. <span data-ttu-id="31458-144">Maven 홈 디렉터리 및 기타 사용자 설정을 지정하는 다음 대화 상자에서 기본값을 적용하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-144">In the next dialog box, where you specify Maven home directory and other user settings, accept the defaults and click **Next**.</span></span>
4. <span data-ttu-id="31458-145">마지막 대화 상자에서 프로젝트 이름 및 위치를 지정한 다음 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-145">In the last dialog box, specify a project name and location and then click **Finish**.</span></span>
5. <span data-ttu-id="31458-146">**src\test\scala\com\microsoft\spark\example**에서 **MySpec.Scala** 파일을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-146">Delete the **MySpec.Scala** file at **src\test\scala\com\microsoft\spark\example**.</span></span> <span data-ttu-id="31458-147">응용 프로그램에 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="31458-147">You do not need this for the application.</span></span>
6. <span data-ttu-id="31458-148">필요한 경우 기본 원본 및 테스트 파일의 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="31458-148">If required, rename the default source and test files.</span></span> <span data-ttu-id="31458-149">IntelliJ IDEA의 왼쪽 창에서 **src\main\scala\com.microsoft.spark.example**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-149">From the left pane in the IntelliJ IDEA, navigate to **src\main\scala\com.microsoft.spark.example**.</span></span> <span data-ttu-id="31458-150">**App.scala**를 마우스 오른쪽 단추로 클릭하고, **리팩터링**, [파일 이름 바꾸기]를 차례로 클릭하며, 대화 상자에서 응용 프로그램의 새 이름을 제공한 다음 **리팩터링**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-150">Right-click **App.scala**, click **Refactor**, click Rename file, and in the dialog box, provide the new name for the application and then click **Refactor**.</span></span>
   
    ![파일 이름 바꾸기](./media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. <span data-ttu-id="31458-152">이후 단계에서는 pom.xml을 업데이트하여 Spark Scala 응용 프로그램에 대한 종속성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-152">In the subsequent steps, you will update the pom.xml to define the dependencies for the Spark Scala application.</span></span> <span data-ttu-id="31458-153">다운로드되고 자동으로 해결되는 이러한 종속성의 경우 Maven을 적절하게 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-153">For those dependencies to be downloaded and resolved automatically, you must configure Maven accordingly.</span></span>
   
    ![자동 다운로드를 위해 Maven 구성](./media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. <span data-ttu-id="31458-155">**파일** 메뉴에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-155">From the **File** menu, click **Settings**.</span></span>
   2. <span data-ttu-id="31458-156">**설정** 대화 상자에서 **빌드, 실행, 배포** > **빌드 도구** > **Maven** > **가져오기**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-156">In the **Settings** dialog box, navigate to **Build, Execution, Deployment** > **Build Tools** > **Maven** > **Importing**.</span></span>
   3. <span data-ttu-id="31458-157">**Maven 프로젝트 자동으로 가져오기**에 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-157">Select the option to **Import Maven projects automatically**.</span></span>
   4. <span data-ttu-id="31458-158">**적용**을 클릭한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-158">Click **Apply**, and then click **OK**.</span></span>
8. <span data-ttu-id="31458-159">Scala 소스 파일을 업데이트하여 응용 프로그램 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-159">Update the Scala source file to include your application code.</span></span> <span data-ttu-id="31458-160">기존 샘플 코드를 열고 다음 코드로 바꾸고 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-160">Open and replace the existing sample code with the following code and save the changes.</span></span> <span data-ttu-id="31458-161">이 코드는 HVAC.csv(모든 HDInsight Spark 클러스터에서 사용 가능)에서 데이터를 읽고, 여섯 번째 열에 한 자리만 있는 행을 검색하고, 출력을 클러스터의 기본 저장 컨테이너 아래의 **/HVACOut** 에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="31458-161">This code reads the data from the HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that only have one digit in the sixth column, and writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>
   
        package com.microsoft.spark.example
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        /**
          * Test IO to wasb
          */
        object WasbIOTest {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("WASBIOTest")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find the rows which have only one digit in the 7th column in the CSV
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACout")
          }
        }
9. <span data-ttu-id="31458-162">pom.xml를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-162">Update the pom.xml.</span></span>
   
   1. <span data-ttu-id="31458-163">`<project>\<properties>`에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-163">Within `<project>\<properties>` add the following:</span></span>
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. <span data-ttu-id="31458-164">`<project>\<dependencies>`에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-164">Within `<project>\<dependencies>` add the following:</span></span>
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      <span data-ttu-id="31458-165">pom.xml에 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-165">Save changes to pom.xml.</span></span>
10. <span data-ttu-id="31458-166">.jar 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31458-166">Create the .jar file.</span></span> <span data-ttu-id="31458-167">IntelliJ IDEA는 프로젝트의 아티팩트로 JAR을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31458-167">IntelliJ IDEA enables creation of JAR as an artifact of a project.</span></span> <span data-ttu-id="31458-168">다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-168">Perform the following steps.</span></span>
    
    1. <span data-ttu-id="31458-169">**파일** 메뉴에서 **프로젝트 구조**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-169">From the **File** menu, click **Project Structure**.</span></span>
    2. <span data-ttu-id="31458-170">**프로젝트 구조** 대화 상자에서 **아티팩트**를 클릭한 다음 +(더하기) 기호를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-170">In the **Project Structure** dialog box, click **Artifacts** and then click the plus symbol.</span></span> <span data-ttu-id="31458-171">팝업 대화 상자에서 **JAR**, **종속성이 있는 모듈에서**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-171">From the pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>
       
        ![JAR 만들기](./media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. <span data-ttu-id="31458-173">**모듈에서 JAR 만들기** 대화 상자에서 **주 클래스**에 대한 ![ellipsis](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png)(줄임표)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-173">In the **Create JAR from Modules** dialog box, click the ellipsis (![ellipsis](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) against the **Main Class**.</span></span>
    4. <span data-ttu-id="31458-174">**주 클래스 선택** 대화 상자에서 기본적으로 표시되는 클래스를 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-174">In the **Select Main Class** dialog box, select the class that appears by default and then click **OK**.</span></span>
       
        ![JAR 만들기](./media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. <span data-ttu-id="31458-176">**모듈에서 JAR 만들** 대화 상자에서 **대상 JAR에 추출** 옵션이 선택되었는지 확인한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-176">In the **Create JAR from Modules** dialog box, make sure that the option to **extract to the target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="31458-177">이렇게 하면 모든 종속성이 있는 단일 JAR이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="31458-177">This creates a single JAR with all dependencies.</span></span>
       
        ![JAR 만들기](./media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. <span data-ttu-id="31458-179">출력 레이아웃 탭에는 Maven 프로젝트의 일부분으로 포함된 jar이 모두 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="31458-179">The output layout tab lists all the jars that are included as part of the Maven project.</span></span> <span data-ttu-id="31458-180">직접 종속성이 없는 Scala 응용 프로그램을 선택하고 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31458-180">You can select and delete the ones on which the Scala application has no direct dependency.</span></span> <span data-ttu-id="31458-181">여기에서 만드는 응용 프로그램의 경우 마지막 것(**SparkSimpleApp 컴파일 출력**)을 제외한 모두를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31458-181">For the application we are creating here, you can remove all but the last one (**SparkSimpleApp compile output**).</span></span> <span data-ttu-id="31458-182">jar을 선택하여 삭제한 다음 **삭제** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-182">Select the jars to delete and then click the **Delete** icon.</span></span>
       
        ![JAR 만들기](./media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        <span data-ttu-id="31458-184">프로젝트를 작성하거나 업데이트할 때마다 jar이 생성되는지 확인하는 **Build on make** 확인란이 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-184">Make sure **Build on make** box is selected, which ensures that the jar is created every time the project is built or updated.</span></span> <span data-ttu-id="31458-185">**적용**을 클릭한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-185">Click **Apply** and then **OK**.</span></span>
    7. <span data-ttu-id="31458-186">메뉴 모음에서 **빌드**를 클릭한 다음 **프로젝트 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-186">From the menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="31458-187">**빌드 아티팩트** 를 클릭하여 jar을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31458-187">You can also click **Build Artifacts** to create the jar.</span></span> <span data-ttu-id="31458-188">**\out\artifacts** 아래에 출력 jar이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="31458-188">The output jar is created under **\out\artifacts**.</span></span>
       
        ![JAR 만들기](./media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-the-application-on-the-spark-cluster"></a><span data-ttu-id="31458-190">Spark 클러스터에서 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="31458-190">Run the application on the Spark cluster</span></span>
<span data-ttu-id="31458-191">클러스터에서 응용 프로그램을 실행하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-191">To run the application on the cluster, you must do the following:</span></span>

* <span data-ttu-id="31458-192">**Azure 저장소 Blob에 응용 프로그램 jar을 복사** 합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-192">**Copy the application jar to the Azure storage blob** associated with the cluster.</span></span> <span data-ttu-id="31458-193">[**AzCopy**](../storage/common/storage-use-azcopy.md) 명령줄 유틸리티를 사용하면 이렇게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31458-193">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, to do so.</span></span> <span data-ttu-id="31458-194">데이터를 업로드하는 데 사용할 수 있는 다른 클라이언트도 많이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31458-194">There are a lot of other clients as well that you can use to upload data.</span></span> <span data-ttu-id="31458-195">[HDInsight에서 Hadoop 작업용 데이터 업로드](hdinsight-upload-data.md)에서 자세한 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31458-195">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
* <span data-ttu-id="31458-196">**Livy를 사용하여 응용 프로그램 작업을 원격으로** Spark 클러스터에 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="31458-196">**Use Livy to submit an application job remotely** to the Spark cluster.</span></span> <span data-ttu-id="31458-197">HDInsight의 Spark 클러스터에는 Spark 작업을 원격으로 제출하는 REST 끝점을 노출하는 Livy가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="31458-197">Spark clusters on HDInsight includes Livy that exposes REST endpoints to remotely submit Spark jobs.</span></span> <span data-ttu-id="31458-198">자세한 내용은 [HDInsight의 Spark 클러스터와 함께 Livy를 사용하여 원격으로 Spark 작업 제출](hdinsight-apache-spark-livy-rest-interface.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31458-198">For more information, see [Submit Spark jobs remotely using Livy with Spark clusters on HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="31458-199">다음 단계</span><span class="sxs-lookup"><span data-stu-id="31458-199">Next step</span></span>

<span data-ttu-id="31458-200">이 문서에서는 Spark Scala 응용 프로그램을 만드는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="31458-200">In this article you learned how to create a Spark scala application.</span></span> <span data-ttu-id="31458-201">다음 문서를 진행하여 Livy를 사용하여 HDInsight Spark 클러스터에서 이 응용 프로그램을 실행하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="31458-201">Advance to the next article to learn how to run this application on an HDInsight Spark cluster using Livy.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="31458-202">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="31458-202">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

