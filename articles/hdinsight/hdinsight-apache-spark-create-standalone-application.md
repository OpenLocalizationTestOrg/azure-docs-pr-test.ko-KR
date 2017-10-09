---
title: "Azure HDInsight Spark 클러스터에서 aaaCreate Scala 앱 toorun | Microsoft Docs"
description: "Hello IntelliJ 아이디어를 제공한 Scala에 대 한 시스템 및 기존 Maven 때 전형 빌드 Scala Apache Maven으로 작성 한 Spark 응용 프로그램을 만듭니다."
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
ms.openlocfilehash: b25291b60921021486f55d78b4832a070a54d163
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-scala-maven-application-toorun-on-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="2cdb4-103">HDInsight의 Apache Spark 클러스터에서 Scala Maven 응용 프로그램 toorun 만들기</span><span class="sxs-lookup"><span data-stu-id="2cdb4-103">Create a Scala Maven application toorun on Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="2cdb4-104">자세한 내용은 방법 toocreate Scala IntelliJ 아이디어 Maven을 사용 하 여 작성 한 Spark 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-104">Learn how toocreate a Spark application written in Scala using Maven with IntelliJ IDEA.</span></span> <span data-ttu-id="2cdb4-105">hello 아티클은 hello 시스템을 작성 하 고 IntelliJ 아이디어를 제공한 Scala에 대 한 기존 Maven 때 전형으로 시작 하는 대로 Apache Maven을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-105">hello article uses Apache Maven as hello build system and starts with an existing Maven archetype for Scala provided by IntelliJ IDEA.</span></span>  <span data-ttu-id="2cdb4-106">IntelliJ 아이디어에 Scala 응용 프로그램을 만드는 단계를 수행 하는 hello 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-106">Creating a Scala application in IntelliJ IDEA involves hello following steps:</span></span>

* <span data-ttu-id="2cdb4-107">Maven hello 빌드 시스템으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-107">Use Maven as hello build system.</span></span>
* <span data-ttu-id="2cdb4-108">프로젝트 개체 모델 (POM) 파일 tooresolve Spark 모듈 종속성을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-108">Update Project Object Model (POM) file tooresolve Spark module dependencies.</span></span>
* <span data-ttu-id="2cdb4-109">Scala에서 응용 프로그램을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-109">Write your application in Scala.</span></span>
* <span data-ttu-id="2cdb4-110">제출 된 tooHDInsight Spark 클러스터 될 수 있는 jar 파일을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-110">Generate a jar file that can be submitted tooHDInsight Spark clusters.</span></span>
* <span data-ttu-id="2cdb4-111">리비를 사용 하 여 Spark 클러스터에서 hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-111">Run hello application on Spark cluster using Livy.</span></span>

> [!NOTE]
> <span data-ttu-id="2cdb4-112">또한 HDInsight 반복 되는 개념 IntelliJ 플러그 인 도구 tooease hello 프로세스 만들기 및 제출 하는 응용 프로그램 tooan Linux에서 HDInsight Spark 클러스터를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-112">HDInsight also provides an IntelliJ IDEA plugin tool tooease hello process of creating and submitting applications tooan HDInsight Spark cluster on Linux.</span></span> <span data-ttu-id="2cdb4-113">자세한 내용은 참조 [IntelliJ 아이디어 toocreate 용 HDInsight 도구 플러그인을 사용 하 여 Spark 응용 프로그램을 제출 하 고](hdinsight-apache-spark-intellij-tool-plugin.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-113">For more information, see [Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark applications](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="2cdb4-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2cdb4-114">Prerequisites</span></span>

* <span data-ttu-id="2cdb4-115">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-115">An Azure subscription.</span></span> <span data-ttu-id="2cdb4-116">[Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="2cdb4-117">HDInsight의 Apache Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="2cdb4-118">자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="2cdb4-119">Oracle Java Development 키트.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-119">Oracle Java Development kit.</span></span> <span data-ttu-id="2cdb4-120">[여기](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="2cdb4-121">Java IDE.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-121">A Java IDE.</span></span> <span data-ttu-id="2cdb4-122">이 문서에서는 IntelliJ IDEA 15.0.1을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-122">This article uses IntelliJ IDEA 15.0.1.</span></span> <span data-ttu-id="2cdb4-123">[여기](https://www.jetbrains.com/idea/download/)에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-scala-plugin-for-intellij-idea"></a><span data-ttu-id="2cdb4-124">IntelliJ IDEA용 Scala 플러그 인 설치</span><span class="sxs-lookup"><span data-stu-id="2cdb4-124">Install Scala plugin for IntelliJ IDEA</span></span>
<span data-ttu-id="2cdb4-125">IntelliJ 아이디어 설치 Scala 플러그 인을 사용 하도록 설정 하지 확인 하지 못했습니다 IntelliJ 아이디어를 시작 하 고 hello 단계 tooinstall hello 플러그 인을 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-125">If IntelliJ IDEA installation did not not prompt for enabling Scala plugin, launch IntelliJ IDEA and go through hello following steps tooinstall hello plugin:</span></span>

1. <span data-ttu-id="2cdb4-126">IntelliJ IDEA를 시작하고 시작 화면에서 **구성**을 클릭한 다음 **플러그 인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-126">Start IntelliJ IDEA and from welcome screen click **Configure** and then click **Plugins**.</span></span>
   
    ![scala 플러그 인 활성화](./media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. <span data-ttu-id="2cdb4-128">Hello 다음 화면에서 클릭 **플러그 인 설치 JetBrains** hello 하단 왼쪽된 모서리 쪽에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-128">In hello next screen, click **Install JetBrains plugin** from hello lower left corner.</span></span> <span data-ttu-id="2cdb4-129">Hello에 **JetBrains 플러그 인 찾아보기** 열리면 Scala 검색 하 고 클릭 한 다음 대화 상자가 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-129">In hello **Browse JetBrains Plugins** dialog box that opens, search for Scala and then click **Install**.</span></span>
   
    ![scala 플러그 인 설치](./media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. <span data-ttu-id="2cdb4-131">Hello 플러그 인이 성공적으로 설치 된 후 클릭 hello **IntelliJ 아이디어를 다시 시작 단추** toorestart hello IDE.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-131">After hello plugin installs successfully, click hello **Restart IntelliJ IDEA button** toorestart hello IDE.</span></span>

## <a name="create-a-standalone-scala-project"></a><span data-ttu-id="2cdb4-132">독립 실행형 Scala 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="2cdb4-132">Create a standalone Scala project</span></span>
1. <span data-ttu-id="2cdb4-133">IntelliJ IDEA를 시작하고 새 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-133">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="2cdb4-134">Hello 새 프로젝트 대화 상자에서 확인 클릭 및 선택 항목을 다음 hello **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-134">In hello new project dialog box, make hello following choices, and then click **Next**.</span></span>
   
    ![Maven 프로젝트 만들기](./media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * <span data-ttu-id="2cdb4-136">선택 **Maven** hello 프로젝트 형식을 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-136">Select **Maven** as hello project type.</span></span>
   * <span data-ttu-id="2cdb4-137">**프로젝트 SDK**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-137">Specify a **Project SDK**.</span></span> <span data-ttu-id="2cdb4-138">새로 만들기를 클릭 하 고 toohello Java 설치 디렉터리를 일반적으로 이동 `C:\Program Files\Java\jdk1.8.0_66`합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-138">Click New and navigate toohello Java installation directory, typically `C:\Program Files\Java\jdk1.8.0_66`.</span></span>
   * <span data-ttu-id="2cdb4-139">선택 hello **아키타 로부터 만들기** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-139">Select hello **Create from archetype** option.</span></span>
   * <span data-ttu-id="2cdb4-140">아키타의 hello 목록에서 선택 **tools.archetypes:scala 아키타 단순 org.scala**합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-140">From hello list of archetypes, select **org.scala-tools.archetypes:scala-archetype-simple**.</span></span> <span data-ttu-id="2cdb4-141">Hello 오른쪽 디렉터리 구조를 만들고 필요한 hello 기본 종속성 toowrite Scala 프로그램을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-141">This will create hello right directory structure and download hello required default dependencies toowrite Scala program.</span></span>
2. <span data-ttu-id="2cdb4-142">**GroupId**, **ArtifactId** 및 **버전**에 관련 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-142">Provide relevant values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="2cdb4-143">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-143">Click **Next**.</span></span>
3. <span data-ttu-id="2cdb4-144">Hello 다음 대화 상자에서 지정할 수 있는 Maven 홈 디렉터리 및 기타 사용자 설정, hello 기본값을 적용 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-144">In hello next dialog box, where you specify Maven home directory and other user settings, accept hello defaults and click **Next**.</span></span>
4. <span data-ttu-id="2cdb4-145">Hello 마지막 대화 상자에서 프로젝트 이름 및 위치를 지정 하 고 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-145">In hello last dialog box, specify a project name and location and then click **Finish**.</span></span>
5. <span data-ttu-id="2cdb4-146">Hello 삭제 **MySpec.Scala** 파일 **src\test\scala\com\microsoft\spark\example**합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-146">Delete hello **MySpec.Scala** file at **src\test\scala\com\microsoft\spark\example**.</span></span> <span data-ttu-id="2cdb4-147">Hello 응용 프로그램에 대 한이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-147">You do not need this for hello application.</span></span>
6. <span data-ttu-id="2cdb4-148">필요한 경우에 hello 기본 소스 및 테스트 파일을 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-148">If required, rename hello default source and test files.</span></span> <span data-ttu-id="2cdb4-149">Hello IntelliJ 아이디어에에서 hello 왼쪽된 창에서 이동 너무**src\main\scala\com.microsoft.spark.example**합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-149">From hello left pane in hello IntelliJ IDEA, navigate too**src\main\scala\com.microsoft.spark.example**.</span></span> <span data-ttu-id="2cdb4-150">마우스 오른쪽 단추로 클릭 **App.scala**, 클릭 **리팩터링**, 이름 바꾸기 파일을 클릭 하 고 hello 대화 상자에서 hello hello 응용 프로그램에 대 한 새 이름을 입력 한 다음 **리팩터링**합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-150">Right-click **App.scala**, click **Refactor**, click Rename file, and in hello dialog box, provide hello new name for hello application and then click **Refactor**.</span></span>
   
    ![파일 이름 바꾸기](./media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. <span data-ttu-id="2cdb4-152">Hello 이후 단계에서는 hello Spark Scala 응용 프로그램에 대 한 hello pom.xml toodefine hello 종속성을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-152">In hello subsequent steps, you will update hello pom.xml toodefine hello dependencies for hello Spark Scala application.</span></span> <span data-ttu-id="2cdb4-153">이러한 종속성에 대 한 toobe 다운로드 하 고 자동으로 해결 Maven을 적절 하 게 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-153">For those dependencies toobe downloaded and resolved automatically, you must configure Maven accordingly.</span></span>
   
    ![자동 다운로드를 위해 Maven 구성](./media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. <span data-ttu-id="2cdb4-155">Hello에서 **파일** 메뉴를 클릭 하 여 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-155">From hello **File** menu, click **Settings**.</span></span>
   2. <span data-ttu-id="2cdb4-156">Hello에 **설정** 대화 상자에서 너무 이동**빌드, 실행, 배포** > **빌드 도구** > **Maven**  >  **가져오기**합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-156">In hello **Settings** dialog box, navigate too**Build, Execution, Deployment** > **Build Tools** > **Maven** > **Importing**.</span></span>
   3. <span data-ttu-id="2cdb4-157">Hello 옵션을 너무 선택**가져오기 Maven 프로젝트를 자동으로**합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-157">Select hello option too**Import Maven projects automatically**.</span></span>
   4. <span data-ttu-id="2cdb4-158">**적용**을 클릭한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-158">Click **Apply**, and then click **OK**.</span></span>
8. <span data-ttu-id="2cdb4-159">Hello Scala 소스 파일 tooinclude 응용 프로그램 코드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-159">Update hello Scala source file tooinclude your application code.</span></span> <span data-ttu-id="2cdb4-160">및 hello hello 코드 다음에 함께 존재 하는 샘플 코드를 대체 열고 hello 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-160">Open and replace hello existing sample code with hello following code and save hello changes.</span></span> <span data-ttu-id="2cdb4-161">이 코드 hello HVAC.csv (모든 HDInsight Spark 클러스터에서 사용 가능)에서 hello 데이터를 읽고, hello에 있는 행만 한 자릿수 hello 6 번째 열을 검색 및 너무 hello 출력을 기록**/HVACOut** hello 기본 저장소 hello 클러스터에 대 한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-161">This code reads hello data from hello HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that only have one digit in hello sixth column, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>
   
        package com.microsoft.spark.example
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        /**
          * Test IO toowasb
          */
        object WasbIOTest {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("WASBIOTest")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows which have only one digit in hello 7th column in hello CSV
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACout")
          }
        }
9. <span data-ttu-id="2cdb4-162">Hello pom.xml를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-162">Update hello pom.xml.</span></span>
   
   1. <span data-ttu-id="2cdb4-163">내에서 `<project>\<properties>` hello 다음 추가:</span><span class="sxs-lookup"><span data-stu-id="2cdb4-163">Within `<project>\<properties>` add hello following:</span></span>
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. <span data-ttu-id="2cdb4-164">내에서 `<project>\<dependencies>` hello 다음 추가:</span><span class="sxs-lookup"><span data-stu-id="2cdb4-164">Within `<project>\<dependencies>` add hello following:</span></span>
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      <span data-ttu-id="2cdb4-165">변경 내용을 toopom.xml를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-165">Save changes toopom.xml.</span></span>
10. <span data-ttu-id="2cdb4-166">Hello.jar 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-166">Create hello .jar file.</span></span> <span data-ttu-id="2cdb4-167">IntelliJ IDEA는 프로젝트의 아티팩트로 JAR을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-167">IntelliJ IDEA enables creation of JAR as an artifact of a project.</span></span> <span data-ttu-id="2cdb4-168">Hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-168">Perform hello following steps.</span></span>
    
    1. <span data-ttu-id="2cdb4-169">Hello에서 **파일** 메뉴를 클릭 하 여 **프로젝트 구조**합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-169">From hello **File** menu, click **Project Structure**.</span></span>
    2. <span data-ttu-id="2cdb4-170">Hello에 **프로젝트 구조** 대화 상자에서 클릭 **아티팩트** 다음 hello 및 기호를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-170">In hello **Project Structure** dialog box, click **Artifacts** and then click hello plus symbol.</span></span> <span data-ttu-id="2cdb4-171">Hello 팝업 대화 상자에서 클릭 **JAR**, 클릭 하 고 **종속성이 있는 모듈에서**합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-171">From hello pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>
       
        ![JAR 만들기](./media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. <span data-ttu-id="2cdb4-173">Hello에 **모듈에서 JAR 만들** 대화 상자에서 hello 줄임표를 클릭 (![줄임표](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) hello에 대 한 **Main 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-173">In hello **Create JAR from Modules** dialog box, click hello ellipsis (![ellipsis](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) against hello **Main Class**.</span></span>
    4. <span data-ttu-id="2cdb4-174">Hello에 **Main 클래스 선택** 대화 상자, 기본적으로 표시 하 고 클릭 선택 hello 클래스 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-174">In hello **Select Main Class** dialog box, select hello class that appears by default and then click **OK**.</span></span>
       
        ![JAR 만들기](./media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. <span data-ttu-id="2cdb4-176">Hello에 **모듈에서 JAR 만들** 대화 상자, 반드시 해당 hello 옵션 너무**toohello 대상 JAR 추출** 을 선택한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-176">In hello **Create JAR from Modules** dialog box, make sure that hello option too**extract toohello target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="2cdb4-177">이렇게 하면 모든 종속성이 있는 단일 JAR이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-177">This creates a single JAR with all dependencies.</span></span>
       
        ![JAR 만들기](./media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. <span data-ttu-id="2cdb4-179">hello 출력 레이아웃 탭 hello Maven 프로젝트의 일부분으로 포함 된 모든 hello jar를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-179">hello output layout tab lists all hello jars that are included as part of hello Maven project.</span></span> <span data-ttu-id="2cdb4-180">선택할 수 있으며 더는 hello Scala 응용 프로그램 삭제 hello 의존 하지 않고 직접입니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-180">You can select and delete hello ones on which hello Scala application has no direct dependency.</span></span> <span data-ttu-id="2cdb4-181">제거할 수는 여기 만들기는 hello 응용 프로그램에 대 한 마지막을 제외 하 고 모두 hello (**SparkSimpleApp 컴파일 출력**).</span><span class="sxs-lookup"><span data-stu-id="2cdb4-181">For hello application we are creating here, you can remove all but hello last one (**SparkSimpleApp compile output**).</span></span> <span data-ttu-id="2cdb4-182">Hello jar toodelete를 선택 하 고 hello를 클릭 한 다음 **삭제** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-182">Select hello jars toodelete and then click hello **Delete** icon.</span></span>
       
        ![JAR 만들기](./media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        <span data-ttu-id="2cdb4-184">있는지 확인 **확인을 토대로** 내용이 해당 hello jar hello 프로젝트를 작성 하거나 업데이트할 때마다 생성 되는 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-184">Make sure **Build on make** box is selected, which ensures that hello jar is created every time hello project is built or updated.</span></span> <span data-ttu-id="2cdb4-185">**적용**을 클릭한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-185">Click **Apply** and then **OK**.</span></span>
    7. <span data-ttu-id="2cdb4-186">Hello 메뉴 모음에서 **빌드**, 클릭 하 고 **프로젝트 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-186">From hello menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="2cdb4-187">클릭할 수도 있습니다 **빌드 아티팩트** toocreate hello jar.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-187">You can also click **Build Artifacts** toocreate hello jar.</span></span> <span data-ttu-id="2cdb4-188">hello 출력 jar 아래에 생성 됩니다 **\out\artifacts**합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-188">hello output jar is created under **\out\artifacts**.</span></span>
       
        ![JAR 만들기](./media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-hello-application-on-hello-spark-cluster"></a><span data-ttu-id="2cdb4-190">Hello Spark 클러스터에서 hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-190">Run hello application on hello Spark cluster</span></span>
<span data-ttu-id="2cdb4-191">수행 해야 toorun hello hello 클러스터에서 응용 프로그램을 hello 다음:</span><span class="sxs-lookup"><span data-stu-id="2cdb4-191">toorun hello application on hello cluster, you must do hello following:</span></span>

* <span data-ttu-id="2cdb4-192">**Hello 응용 프로그램 jar toohello Azure 저장소 blob 복사** hello 클러스터와 연결 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-192">**Copy hello application jar toohello Azure storage blob** associated with hello cluster.</span></span> <span data-ttu-id="2cdb4-193">사용할 수 있습니다 [ **AzCopy**](../storage/common/storage-use-azcopy.md), 명령줄 유틸리티, toodo 되므로 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-193">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, toodo so.</span></span> <span data-ttu-id="2cdb4-194">Tooupload 데이터를 사용할 수 있는 다른 클라이언트를도 많이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-194">There are a lot of other clients as well that you can use tooupload data.</span></span> <span data-ttu-id="2cdb4-195">[HDInsight에서 Hadoop 작업용 데이터 업로드](hdinsight-upload-data.md)에서 자세한 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-195">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
* <span data-ttu-id="2cdb4-196">**원격으로 리비 toosubmit 응용 프로그램 작업을 사용 하 여** toohello Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-196">**Use Livy toosubmit an application job remotely** toohello Spark cluster.</span></span> <span data-ttu-id="2cdb4-197">HDInsight의 Spark 클러스터 리비 REST 끝점 tooremotely 전송 Spark 작업을 노출 하는 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-197">Spark clusters on HDInsight includes Livy that exposes REST endpoints tooremotely submit Spark jobs.</span></span> <span data-ttu-id="2cdb4-198">자세한 내용은 [HDInsight의 Spark 클러스터와 함께 Livy를 사용하여 원격으로 Spark 작업 제출](hdinsight-apache-spark-livy-rest-interface.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-198">For more information, see [Submit Spark jobs remotely using Livy with Spark clusters on HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="2cdb4-199">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2cdb4-199">Next step</span></span>

<span data-ttu-id="2cdb4-200">이 방법에 대해 배웠습니다 문서 toocreate Spark scala 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-200">In this article you learned how toocreate a Spark scala application.</span></span> <span data-ttu-id="2cdb4-201">고급 toohello 다음 문서 toolearn 어떻게 toorun HDInsight Spark에이 응용 프로그램 사용 하 여 클러스터 리비 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cdb4-201">Advance toohello next article toolearn how toorun this application on an HDInsight Spark cluster using Livy.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="2cdb4-202">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="2cdb4-202">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

