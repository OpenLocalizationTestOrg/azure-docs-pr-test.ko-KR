---
title: "IntelliJ용 Azure 도구 키트: HDInsight 클러스터용 Spark 응용 프로그램 만들기 | Microsoft Docs"
description: "IntelliJ toodevelop Spark 작성 된 응용 프로그램 Scala에 대 한 hello Azure 도구 키트를 사용 하 고 tooan HDInsight Spark 클러스터에 전송 합니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 73304272-6c8b-482e-af7c-cd25d95dab4d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 22cce014bb848a54e198e77a50bf13448012310e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toocreate-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="37b0e-103">Azure 도구 키트를 사용 하 여 HDInsight 클러스터에 대 한 IntelliJ toocreate Spark 응용 프로그램에 대 한</span><span class="sxs-lookup"><span data-stu-id="37b0e-103">Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="37b0e-104">IntelliJ 플러그 인 toodevelop Spark 작성 된 응용 프로그램 Scala에 대 한 hello Azure 도구 키트를 사용 하 여 하 고 tooan hello IntelliJ 통합된 개발 환경 (IDE)에서 직접 HDInsight Spark 클러스터 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-104">Use hello Azure Toolkit for IntelliJ plug-in toodevelop Spark applications written in Scala, and then submit them tooan HDInsight Spark cluster directly from hello IntelliJ integrated development environment (IDE).</span></span> <span data-ttu-id="37b0e-105">Hello 플러그 인에 몇 가지 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-105">You can use hello plug-in in a few ways:</span></span>

* <span data-ttu-id="37b0e-106">HDInsight Spark 클러스터에서 Scala Spark 응용 프로그램을 개발 및 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-106">Develop and submit a Scala Spark application on an HDInsight Spark cluster.</span></span>
* <span data-ttu-id="37b0e-107">Azure HDInsight Spark 클러스터 리소스에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-107">Access your Azure HDInsight Spark cluster resources.</span></span>
* <span data-ttu-id="37b0e-108">Scala Spark 응용 프로그램을 로컬로 개발 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-108">Develop and run a Scala Spark application locally.</span></span>

<span data-ttu-id="37b0e-109">toocreate 프로젝트, 보기 hello [hello IntelliJ 용 Azure 도구 키트로 Spark 응용 프로그램 만들기](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) 비디오.</span><span class="sxs-lookup"><span data-stu-id="37b0e-109">toocreate your project, view hello [Create Spark Applications with hello Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) video.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="37b0e-110">이 플러그 인 toocreate를 사용 하 여 수 있으며 Linux에서 HDInsight Spark 클러스터는에 대 한 응용 프로그램을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-110">You can use this plug-in toocreate and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="37b0e-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="37b0e-111">Prerequisites</span></span>

- <span data-ttu-id="37b0e-112">HDInsight Linux의 Apache Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-112">An Apache Spark cluster on HDInsight Linux.</span></span> <span data-ttu-id="37b0e-113">자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="37b0e-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
- <span data-ttu-id="37b0e-114">Oracle Java Development 키트.</span><span class="sxs-lookup"><span data-stu-id="37b0e-114">Oracle Java Development Kit.</span></span> <span data-ttu-id="37b0e-115">Hello에서 설치할 수 있습니다 [Oracle 웹 사이트](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-115">You can install it from hello [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
- <span data-ttu-id="37b0e-116">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="37b0e-116">IntelliJ IDEA.</span></span> <span data-ttu-id="37b0e-117">이 문서에서는 버전 2017.1을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-117">This article uses version 2017.1.</span></span> <span data-ttu-id="37b0e-118">Hello에서 설치할 수 있습니다 [JetBrains 웹 사이트](https://www.jetbrains.com/idea/download/)합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-118">You can install it from hello [JetBrains website](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-azure-toolkit-for-intellij"></a><span data-ttu-id="37b0e-119">IntelliJ용 Azure 도구 키트 설치</span><span class="sxs-lookup"><span data-stu-id="37b0e-119">Install Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="37b0e-120">설치 지침에 대해서는 [IntelliJ용 Azure 도구 키트 설치](../azure-toolkit-for-intellij-installation.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="37b0e-120">For installation instructions, see [Install Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="sign-in-tooyour-azure-subscription"></a><span data-ttu-id="37b0e-121">Azure 구독 tooyour에 로그인</span><span class="sxs-lookup"><span data-stu-id="37b0e-121">Sign in tooyour Azure subscription</span></span>

1. <span data-ttu-id="37b0e-122">Hello IntelliJ IDE를 시작 하 고 Azure 탐색기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-122">Start hello IntelliJ IDE, and open Azure Explorer.</span></span> <span data-ttu-id="37b0e-123">Hello에 **보기** 메뉴 선택 **도구 창**를 선택한 후 **Azure 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-123">On hello **View** menu, select **Tool Windows**, and then select **Azure Explorer**.</span></span>
       
   ![hello Azure 탐색기 링크](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. <span data-ttu-id="37b0e-125">마우스 오른쪽 단추로 클릭 hello **Azure** 노드를 선택한 후 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-125">Right-click hello **Azure** node, and then select **Sign In**.</span></span>

3. <span data-ttu-id="37b0e-126">Hello에 **Azure 로그인** 대화 상자에서 **로그인**, 한 다음 Azure 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-126">In hello **Azure Sign In** dialog box, select **Sign in**, and then enter your Azure credentials.</span></span>

    ![hello Azure 로그인 대화 상자](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. <span data-ttu-id="37b0e-128">로그인, 후 hello **구독 선택** 연관 된 Azure 구독을 hello 모든 대화 상자 목록 hello 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-128">After you're signed in, hello **Select Subscriptions** dialog box lists all hello Azure subscriptions that are associated with hello credentials.</span></span> <span data-ttu-id="37b0e-129">선택 hello **선택** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-129">Select hello **Select** button.</span></span>

    ![hello 구독 선택 대화 상자](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. <span data-ttu-id="37b0e-131">Hello에 **Azure 탐색기** 탭을 확장 하 고 **HDInsight** 구독에 있는 tooview hello HDInsight Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-131">On hello **Azure Explorer** tab, expand **HDInsight** tooview hello HDInsight Spark clusters that are in your subscription.</span></span>
   
    ![Azure 탐색기의 HDInsight Spark 클러스터](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. <span data-ttu-id="37b0e-133">tooview hello 리소스 (예를 들어 저장소 계정) hello 클러스터와 연결 된 클러스터 이름 노드를 추가로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-133">tooview hello resources (for example, storage accounts) that are associated with hello cluster, you can further expand a cluster-name node.</span></span>
   
    ![확장된 클러스터-이름 노드](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="37b0e-135">HDInsight Spark 클러스터에서 Spark Scala 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="37b0e-135">Run a Spark Scala application on an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="37b0e-136">IntelliJ IDEA를 시작하고 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-136">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="37b0e-137">Hello에 **새 프로젝트** 대화 상자에서 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-137">In hello **New Project** dialog box, do hello following:</span></span> 

   <span data-ttu-id="37b0e-138">a.</span><span class="sxs-lookup"><span data-stu-id="37b0e-138">a.</span></span> <span data-ttu-id="37b0e-139">**HDInsight** > **HDInsight의 Spark(Scala)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-139">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="37b0e-140">b.</span><span class="sxs-lookup"><span data-stu-id="37b0e-140">b.</span></span> <span data-ttu-id="37b0e-141">Hello에 **빌드 도구** 목록 hello tooyour 필요에 따라, 다음 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-141">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      * <span data-ttu-id="37b0e-142">Scala 프로젝트 만들기 마법사 지원에 대해 **Maven**</span><span class="sxs-lookup"><span data-stu-id="37b0e-142">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="37b0e-143">**SBT**, hello 종속성을 관리 하 고 hello Scala 프로젝트에 대 한 구성 하기 위한</span><span class="sxs-lookup"><span data-stu-id="37b0e-143">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

    ![hello 새 프로젝트 대화 상자](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. <span data-ttu-id="37b0e-145">**다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-145">Select **Next**.</span></span>

3. <span data-ttu-id="37b0e-146">hello Scala 프로젝트 만들기 마법사는 자동으로 hello Scala 플러그 인을 설치 했는데 있는지 여부를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-146">hello Scala project-creation wizard automatically detects whether you've installed hello Scala plug-in.</span></span> <span data-ttu-id="37b0e-147">**설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-147">Select **Install**.</span></span>

   ![Scala 플러그 인 검사](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. <span data-ttu-id="37b0e-149">플러그 인을 선택 Scala toodownload hello **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-149">toodownload hello Scala plug-in, select **OK**.</span></span> <span data-ttu-id="37b0e-150">Hello 지침 toorestart IntelliJ 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-150">Follow hello instructions toorestart IntelliJ.</span></span> 

   ![hello Scala 플러그 인 설치 대화 상자](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. <span data-ttu-id="37b0e-152">Hello에 **새 프로젝트** 창에서 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-152">In hello **New Project** window, do hello following:</span></span>  

    ![Hello Spark SDK를 선택합니다.](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   <span data-ttu-id="37b0e-154">a.</span><span class="sxs-lookup"><span data-stu-id="37b0e-154">a.</span></span> <span data-ttu-id="37b0e-155">프로젝트 이름 및 위치를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-155">Enter a project name and location.</span></span>

   <span data-ttu-id="37b0e-156">b.</span><span class="sxs-lookup"><span data-stu-id="37b0e-156">b.</span></span> <span data-ttu-id="37b0e-157">Hello에 **프로젝트 SDK** 드롭 다운 목록 **Java 1.8** hello Spark 2.x 클러스터 또는 선택에 대 한 **Java 1.7** hello Spark 1.x 클러스터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-157">In hello **Project SDK** drop-down list, select **Java 1.8** for hello Spark 2.x cluster, or select **Java 1.7** for hello Spark 1.x cluster.</span></span>

   <span data-ttu-id="37b0e-158">c.</span><span class="sxs-lookup"><span data-stu-id="37b0e-158">c.</span></span> <span data-ttu-id="37b0e-159">Hello에 **Spark 버전** 드롭 다운 목록에서 Scala 프로젝트 만들기 마법사 Spark SDK 및 Scala SDK에 대 한 hello 적절 한 버전을 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-159">In hello **Spark version** drop-down list, Scala project creation wizard integrates hello proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="37b0e-160">Hello Spark 클러스터 버전이 2.0 보다 이전 이면 선택 **1.x 멤버**합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-160">If hello Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="37b0e-161">그렇지 않은 경우 **Spark2.x**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-161">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="37b0e-162">이 예제에서는 **Spark 2.0.2(Scala 2.11.8)**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-162">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

6. <span data-ttu-id="37b0e-163">**마침**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-163">Select **Finish**.</span></span>

7. <span data-ttu-id="37b0e-164">hello Spark 프로젝트를 아티팩트를 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-164">hello Spark project automatically creates an artifact for you.</span></span> <span data-ttu-id="37b0e-165">tooview hello 아티팩트 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-165">tooview hello artifact, do hello following:</span></span>

   <span data-ttu-id="37b0e-166">a.</span><span class="sxs-lookup"><span data-stu-id="37b0e-166">a.</span></span> <span data-ttu-id="37b0e-167">Hello에 **파일** 메뉴 선택 **프로젝트 구조**합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-167">On hello **File** menu, select **Project Structure**.</span></span>

   <span data-ttu-id="37b0e-168">b.</span><span class="sxs-lookup"><span data-stu-id="37b0e-168">b.</span></span> <span data-ttu-id="37b0e-169">Hello에 **프로젝트 구조** 대화 상자에서 **아티팩트** 만들어진 tooview hello 기본 아티팩트입니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-169">In hello **Project Structure** dialog box, select **Artifacts** tooview hello default artifact that is created.</span></span> <span data-ttu-id="37b0e-170">Hello 더하기 기호를 선택 하 여 사용자 고유의 아티팩트를 만들 수도 있습니다 (**+**).</span><span class="sxs-lookup"><span data-stu-id="37b0e-170">You can also create your own artifact by selecting hello plus sign (**+**).</span></span>

      ![Hello 대화 상자에서 아티팩트 정보](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. <span data-ttu-id="37b0e-172">Hello 다음을 수행 하 여 응용 프로그램 소스 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-172">Add your application source code by doing hello following:</span></span>

   <span data-ttu-id="37b0e-173">a.</span><span class="sxs-lookup"><span data-stu-id="37b0e-173">a.</span></span> <span data-ttu-id="37b0e-174">프로젝트 탐색기에서 마우스 오른쪽 단추로 클릭 **src**, 너무 가리킨**새로**를 선택한 후 **Scala 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-174">In Project Explorer, right-click **src**, point too**New**, and then select **Scala Class**.</span></span>
      
      ![프로젝트 탐색기에서 Scala 클래스 만들기에 대한 명령](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   <span data-ttu-id="37b0e-176">b.</span><span class="sxs-lookup"><span data-stu-id="37b0e-176">b.</span></span> <span data-ttu-id="37b0e-177">Hello에 **새 Scala 클래스 만들기** 대화 상자, 이름을 제공 하 고, 선택 **개체** hello에 **종류** 상자를 선택한 후 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-177">In hello **Create New Scala Class** dialog box, provide a name, select **Object** in hello **Kind** box, and then select **OK**.</span></span>
      
      ![새 Scala 클래스 만들기 대화 상자](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   <span data-ttu-id="37b0e-179">c.</span><span class="sxs-lookup"><span data-stu-id="37b0e-179">c.</span></span> <span data-ttu-id="37b0e-180">Hello에 **MyClusterApp.scala** 파일, 코드 다음 hello를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-180">In hello **MyClusterApp.scala** file, paste hello following code.</span></span> <span data-ttu-id="37b0e-181">hello 코드 HVAC.csv (모든 HDInsight Spark 클러스터에서 사용 가능)에서 hello 데이터를 읽고, hello hello CSV 파일의 일곱 번째 열에는 하나의 진수가 hello 행을 검색 및 너무 hello 출력을 기록**/HVACOut** hello 기본 hello 클러스터에 대 한 저장소 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-181">hello code reads hello data from HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that have only one digit in hello seventh column in hello CSV file, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>

        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
    
        object MyClusterApp{
            def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
    
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
    
            //find hello rows that have only one digit in hello seventh column in hello CSV file
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
    
            rdd1.saveAsTextFile("wasb:///HVACOut")
            }
    
        }

9. <span data-ttu-id="37b0e-182">Hello 다음을 수행 하 여 HDInsight Spark 클러스터에서 hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-182">Run hello application on an HDInsight Spark cluster by doing hello following:</span></span>

   <span data-ttu-id="37b0e-183">a.</span><span class="sxs-lookup"><span data-stu-id="37b0e-183">a.</span></span> <span data-ttu-id="37b0e-184">프로젝트 탐색기에서 hello 프로젝트 이름을 마우스 오른쪽 단추로 클릭 한 다음 선택 **Spark 응용 프로그램 제출 tooHDInsight**합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-184">In Project Explorer, right-click hello project name, and then select **Submit Spark Application tooHDInsight**.</span></span>
      
      ![hello Spark 응용 프로그램 제출 tooHDInsight 명령](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   <span data-ttu-id="37b0e-186">b.</span><span class="sxs-lookup"><span data-stu-id="37b0e-186">b.</span></span> <span data-ttu-id="37b0e-187">하면 Azure 구독 자격 증명된 tooenter 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-187">You are prompted tooenter your Azure subscription credentials.</span></span> <span data-ttu-id="37b0e-188">Hello에 **Spark 제출** 대화 상자에서 다음 값을 hello를 지정 하 고 다음 선택 **전송**합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-188">In hello **Spark Submission** dialog box, provide hello following values, and then select **Submit**.</span></span>
      
      * <span data-ttu-id="37b0e-189">에 대 한 **클러스터 (Linux에만 해당) 멤버**, 선택 hello toorun 원하는 HDInsight Spark 클러스터 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-189">For **Spark clusters (Linux only)**, select hello HDInsight Spark cluster on which you want toorun your application.</span></span>

      * <span data-ttu-id="37b0e-190">Hello IntelliJ 프로젝트에서 아티팩트를 선택 하거나 hello 하드 드라이브에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-190">Select an artifact from hello IntelliJ project, or select one from hello hard drive.</span></span>

      * <span data-ttu-id="37b0e-191">Hello에 **Main 클래스 이름** 상자 선택 hello 줄임표 (**...** ) hello 주 클래스에서 응용 프로그램 소스 코드를 선택한 다음 선택 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-191">In hello **Main class name** box, select hello ellipsis (**...**), select hello main class in your application source code, and then select **OK**.</span></span>

        ![hello Main 클래스 선택 대화 상자](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * <span data-ttu-id="37b0e-193">이 예에서 응용 프로그램 코드 hello 명령줄 인수도 필요 하지 않거나 Jar 또는 파일 참조를 때문에 남아 있는 빈 상자 hello를 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-193">Because hello application code in this example does not require command-line arguments or reference JARs or files, you can leave hello remaining boxes empty.</span></span> <span data-ttu-id="37b0e-194">모든 hello 정보를 제공한 후 hello 대화 상자 이미지를 수행 하는 hello와 비슷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-194">After you provide all hello information, hello dialog box should resemble hello following image.</span></span>
        
        ![hello Spark 제출 대화 상자](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   <span data-ttu-id="37b0e-196">c.</span><span class="sxs-lookup"><span data-stu-id="37b0e-196">c.</span></span> <span data-ttu-id="37b0e-197">hello **Spark 제출** hello hello 창의 맨 아래에 탭 hello 진행률을 표시 하기 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-197">hello **Spark Submission** tab at hello bottom of hello window should start displaying hello progress.</span></span> <span data-ttu-id="37b0e-198">Hello에 빨간색 hello 단추를 선택 하 여 hello 응용 프로그램을 중지할 수도 있습니다 **Spark 제출** 창.</span><span class="sxs-lookup"><span data-stu-id="37b0e-198">You can also stop hello application by selecting hello red button in hello **Spark Submission** window.</span></span>
      
      ![hello Spark 전송 창](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      <span data-ttu-id="37b0e-200">toolearn tooaccess hello 작업 출력 참조 hello "액세스 IntelliJ 용 Azure 도구 키트를 사용 하 여 HDInsight Spark 클러스터를 관리 하 고"이이 문서의 뒷부분에 나오는 섹션.</span><span class="sxs-lookup"><span data-stu-id="37b0e-200">toolearn how tooaccess hello job output, see hello "Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ" section later in this article.</span></span>

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="37b0e-201">HDInsight Spark 클러스터에서 Spark Scala 응용 프로그램 실행 또는 디버그</span><span class="sxs-lookup"><span data-stu-id="37b0e-201">Run or debug a Spark Scala application on an HDInsight Spark cluster</span></span>
<span data-ttu-id="37b0e-202">또한 hello Spark 응용 프로그램 toohello 클러스터를 제출 하는 또 다른 방법은 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-202">We also recommend another way of submitting hello Spark application toohello cluster.</span></span> <span data-ttu-id="37b0e-203">Hello에서 hello 매개 변수를 설정 하 여 그렇게 할 수 **실행/디버그 구성을** IDE.</span><span class="sxs-lookup"><span data-stu-id="37b0e-203">You can do so by setting hello parameters in hello **Run/Debug configurations** IDE.</span></span> <span data-ttu-id="37b0e-204">자세한 내용은 [IntelliJ용 Azure 도구 키트를 사용하여 SSH를 통해 HDInsight 클러스터에서 원격으로 Spark 응용 프로그램 디버그](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="37b0e-204">For more information, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a><span data-ttu-id="37b0e-205">IntelliJ용 Azure 도구 키트를 사용하여 HDInsight Spark 클러스터 액세스 및 관리</span><span class="sxs-lookup"><span data-stu-id="37b0e-205">Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="37b0e-206">IntelliJ용 Azure 도구 키트를 사용하여 다양한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-206">You can perform various operations by using Azure Toolkit for IntelliJ.</span></span>

### <a name="access-hello-job-view"></a><span data-ttu-id="37b0e-207">액세스 hello 작업 보기</span><span class="sxs-lookup"><span data-stu-id="37b0e-207">Access hello job view</span></span>
1. <span data-ttu-id="37b0e-208">Azure 탐색기에서 확장 **HDInsight**hello Spark 클러스터 이름을 확장 하 고 다음 선택 **작업**합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-208">In Azure Explorer, expand **HDInsight**, expand hello Spark cluster name, and then select **Jobs**.</span></span>  

    ![작업 보기 노드](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. <span data-ttu-id="37b0e-210">Hello 오른쪽 창에서 hello **Spark 작업 보기** hello 클러스터에서 실행 된 모든 hello 응용 프로그램 탭에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-210">In hello right pane, hello **Spark Job View** tab displays all hello applications that were run on hello cluster.</span></span> <span data-ttu-id="37b0e-211">보려는 toosee 자세히 hello 응용 프로그램의 hello 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-211">Select hello name of hello application for which you want toosee more details.</span></span>

    ![응용 프로그램 세부 정보](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. <span data-ttu-id="37b0e-213">toodisplay 기본 실행 중인 작업 정보를 hello 작업 그래프를 가리키도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-213">toodisplay basic running job information, hover over hello job graph.</span></span> <span data-ttu-id="37b0e-214">모든 작업을 생성 하는 정보와 tooview hello 단계 그래프 hello 작업 그래프에서 노드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-214">tooview hello stages graph and information that every job generates, select a node on hello job graph.</span></span>

    ![작업 단계 세부 정보](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. <span data-ttu-id="37b0e-216">tooview 자주 사용 되는 로그와 같은 *드라이버 Stderr*, *드라이버 Stdout*, 및 *디렉터리 정보*선택, hello **로그** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-216">tooview frequently used logs, such as *Driver Stderr*, *Driver Stdout*, and *Directory Info*, select hello **Log** tab.</span></span>

    ![로그 세부 정보](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. <span data-ttu-id="37b0e-218">또한 hello hello 창의 맨 아래에 링크를 선택 하 여 hello Spark 기록 UI 및 hello hello 응용 프로그램 수준에서 YARN UI를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-218">You can also view hello Spark history UI and hello YARN UI (at hello application level) by selecting a link at hello top of hello window.</span></span>

### <a name="access-hello-spark-history-server"></a><span data-ttu-id="37b0e-219">Hello Spark 기록 서버에 액세스</span><span class="sxs-lookup"><span data-stu-id="37b0e-219">Access hello Spark history server</span></span>
1. <span data-ttu-id="37b0e-220">Azure 탐색기에서 **HDInsight**를 확장하고, 마우스 오른쪽 단추로 Spark 클러스터 이름을 클릭한 다음 **Spark 기록 UI 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-220">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> 

2. <span data-ttu-id="37b0e-221">메시지가 나타나면 hello 클러스터를 설정할 때 지정 하는 hello 클러스터 관리 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-221">When you're prompted, enter hello cluster's admin credentials, which you specified when you set up hello cluster.</span></span>

3. <span data-ttu-id="37b0e-222">대시보드에서 hello Spark 기록 서버 hello 응용 프로그램 실행이 방금 완료에 대 한 응용 프로그램 이름 toolook hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-222">On hello Spark history server dashboard, you can use hello application name toolook for hello application that you just finished running.</span></span> <span data-ttu-id="37b0e-223">Hello 앞에 코드를 사용 하 여 hello 응용 프로그램 이름을 설정 `val conf = new SparkConf().setAppName("MyClusterApp")`합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-223">In hello preceding code, you set hello application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="37b0e-224">따라서 Spark 응용 프로그램 이름은 **MyClusterApp**입니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-224">Therefore, your Spark application name is **MyClusterApp**.</span></span>

### <a name="start-hello-ambari-portal"></a><span data-ttu-id="37b0e-225">Hello Ambari 포털 시작</span><span class="sxs-lookup"><span data-stu-id="37b0e-225">Start hello Ambari portal</span></span>
1. <span data-ttu-id="37b0e-226">Azure 탐색기에서 **HDInsight**를 확장하고, 마우스 오른쪽 단추로 Spark 클러스터 이름을 클릭한 다음 **클러스터 관리 포털(Ambari) 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-226">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 

2. <span data-ttu-id="37b0e-227">메시지가 나타나면 hello 클러스터에 대 한 hello 관리자 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-227">When you're prompted, enter hello admin credentials for hello cluster.</span></span> <span data-ttu-id="37b0e-228">이러한 자격 증명 hello 클러스터 설치 과정에서 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-228">You specified these credentials during hello cluster setup process.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="37b0e-229">Azure 구독 관리</span><span class="sxs-lookup"><span data-stu-id="37b0e-229">Manage Azure subscriptions</span></span>
<span data-ttu-id="37b0e-230">기본적으로 IntelliJ 용 Azure 도구 키트는 모든 Azure 구독에서 hello Spark 클러스터를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-230">By default, Azure Toolkit for IntelliJ lists hello Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="37b0e-231">필요한 경우 tooaccess hello 구독을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-231">If necessary, you can specify hello subscriptions that you want tooaccess.</span></span> 

1. <span data-ttu-id="37b0e-232">Azure 탐색기에서 마우스 오른쪽 단추로 클릭 hello **Azure** 루트 노드를 선택한 후 **구독 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-232">In Azure Explorer, right-click hello **Azure** root node, and then select **Manage Subscriptions**.</span></span> 

2. <span data-ttu-id="37b0e-233">선택을 취소 hello 확인란 다음 toohello 구독 tooaccess, 원하는 되 고 다음을 선택 하지 않는 hello 대화 상자에서 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-233">In hello dialog box, clear hello check boxes next toohello subscriptions that you don't want tooaccess, and then select **Close**.</span></span> <span data-ttu-id="37b0e-234">선택할 수도 있습니다 **로그 아웃** toosign Azure 구독에서 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="37b0e-234">You can also select **Sign Out** if you want toosign out of your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="37b0e-235">로컬로 Spark Scala 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="37b0e-235">Run a Spark Scala application locally</span></span>
<span data-ttu-id="37b0e-236">사용할 수 있습니다 Azure 도구 키트 IntelliJ toorun Spark Scala 응용 프로그램에 대 한 로컬 워크스테이션에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-236">You can use Azure Toolkit for IntelliJ toorun Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="37b0e-237">hello 응용 프로그램 일반적으로 액세스 하지 않기 필요 toocluster 주고받는 저장 컨테이너 및 실행 하 고 로컬로 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-237">hello applications usually don't need access toocluster resources, such as storage containers, and you can run and test them locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="37b0e-238">필수 요소</span><span class="sxs-lookup"><span data-stu-id="37b0e-238">Prerequisite</span></span>
<span data-ttu-id="37b0e-239">에 설명 된 대로 예외를 hello 로컬 Spark Scala 응용 프로그램을 Windows 컴퓨터에서 실행 하는 동안 발생할 수 있습니다 [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356)합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-239">While you're running hello local Spark Scala application on a Windows computer, you might get an exception, as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span></span> <span data-ttu-id="37b0e-240">hello 예외가 Windows에서 WinUtils.exe 없기 때문에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-240">hello exception occurs because WinUtils.exe is missing on Windows.</span></span> 

<span data-ttu-id="37b0e-241">tooresolve이이 오류를 [hello 실행 파일을 다운로드](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa 위치와 같은 **C:\WinUtils\bin**합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-241">tooresolve this error, [download hello executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa location such as **C:\WinUtils\bin**.</span></span> <span data-ttu-id="37b0e-242">그런 다음 hello 환경 변수를 추가 **HADOOP_HOME**, 너무 hello hello 변수 값을 설정 하 고**C\WinUtils**합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-242">Then, add hello environment variable **HADOOP_HOME**, and set hello value of hello variable too**C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="37b0e-243">로컬 Spark Scala 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="37b0e-243">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="37b0e-244">IntelliJ IDEA를 시작하고 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-244">Start IntelliJ IDEA, and create a project.</span></span> 

2. <span data-ttu-id="37b0e-245">Hello에 **새 프로젝트** 대화 상자에서 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-245">In hello **New Project** dialog box, do hello following:</span></span>
   
    <span data-ttu-id="37b0e-246">a.</span><span class="sxs-lookup"><span data-stu-id="37b0e-246">a.</span></span> <span data-ttu-id="37b0e-247">**HDInsight** > **HDInsight의 Spark 로컬 실행 샘플(Scala)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-247">Select **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)**.</span></span>

    <span data-ttu-id="37b0e-248">b.</span><span class="sxs-lookup"><span data-stu-id="37b0e-248">b.</span></span> <span data-ttu-id="37b0e-249">Hello에 **빌드 도구** 목록 hello tooyour 필요에 따라, 다음 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-249">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      * <span data-ttu-id="37b0e-250">Scala 프로젝트 만들기 마법사 지원에 대해 **Maven**</span><span class="sxs-lookup"><span data-stu-id="37b0e-250">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="37b0e-251">**SBT**, hello 종속성을 관리 하 고 hello Scala 프로젝트에 대 한 구성 하기 위한</span><span class="sxs-lookup"><span data-stu-id="37b0e-251">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

    ![hello 새 프로젝트 대화 상자](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. <span data-ttu-id="37b0e-253">**다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-253">Select **Next**.</span></span>
 
4. <span data-ttu-id="37b0e-254">Hello 다음 창에서 수행 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-254">In hello next window, do hello following:</span></span>
   
    <span data-ttu-id="37b0e-255">a.</span><span class="sxs-lookup"><span data-stu-id="37b0e-255">a.</span></span> <span data-ttu-id="37b0e-256">프로젝트 이름 및 위치를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-256">Enter a project name and location.</span></span>

    <span data-ttu-id="37b0e-257">b.</span><span class="sxs-lookup"><span data-stu-id="37b0e-257">b.</span></span> <span data-ttu-id="37b0e-258">Hello에 **프로젝트 SDK** 드롭 다운 목록 1.7 버전 보다 최신인 Java 버전을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-258">In hello **Project SDK** drop-down list, select a Java version that's later than version 1.7.</span></span>

    <span data-ttu-id="37b0e-259">c.</span><span class="sxs-lookup"><span data-stu-id="37b0e-259">c.</span></span> <span data-ttu-id="37b0e-260">Hello에 **Spark 버전** 드롭 다운 목록, 버전, 선택 hello Scala toouse 원하는: Scala Spark 2.0 또는 Scala 2.11.x 2.10.x Spark 1.6에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-260">In hello **Spark Version** drop-down list, select hello version of Scala that you want toouse: Scala 2.11.x for Spark 2.0 or Scala 2.10.x for Spark 1.6.</span></span>

    ![hello 새 프로젝트 대화 상자](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. <span data-ttu-id="37b0e-262">**마침**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-262">Select **Finish**.</span></span>

6. <span data-ttu-id="37b0e-263">샘플 코드를 추가 하는 hello 템플릿 (**LogQuery**) hello에서 **src** 폴더를 컴퓨터에 로컬로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-263">hello template adds a sample code (**LogQuery**) under hello **src** folder that you can run locally on your computer.</span></span>
   
    ![LogQuery 위치](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. <span data-ttu-id="37b0e-265">마우스 오른쪽 단추로 클릭 hello **LogQuery** 응용 프로그램을 마우스 선택 **실행 'LogQuery'**합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-265">Right-click hello **LogQuery** application, and then select **Run 'LogQuery'**.</span></span> <span data-ttu-id="37b0e-266">Hello에 **실행** 탭 hello 다음과 같은 출력 hello 맨 아래에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-266">On hello **Run** tab at hello bottom, you see an output like hello following:</span></span>
   
   ![Spark 응용 프로그램 로컬 실행 결과](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-toouse-azure-toolkit-for-intellij"></a><span data-ttu-id="37b0e-268">IntelliJ에 대 한 기존 IntelliJ 아이디어 응용 프로그램 toouse Azure 도구 키트 변환</span><span class="sxs-lookup"><span data-stu-id="37b0e-268">Convert existing IntelliJ IDEA applications toouse Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="37b0e-269">Hello Spark Scala는 기존 응용 프로그램에서에서 만든 IntelliJ 아이디어 toobe Azure 도구 키트 호환 IntelliJ에 대 한 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-269">You can convert hello existing Spark Scala applications that you created in IntelliJ IDEA toobe compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="37b0e-270">그런 다음 hello 플러그 인 toosubmit hello 응용 프로그램 tooan HDInsight Spark 클러스터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-270">You can then use hello plug-in toosubmit hello applications tooan HDInsight Spark cluster.</span></span>

1. <span data-ttu-id="37b0e-271">응용 프로그램에 대해 기존 Spark Scala IntelliJ 아이디어를 통해 생성 된, hello 관련된.iml 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-271">For an existing Spark Scala application that was created through IntelliJ IDEA, open hello associated .iml file.</span></span>

2. <span data-ttu-id="37b0e-272">Hello 루트에 수준은 **모듈** hello 다음과 같은 요소:</span><span class="sxs-lookup"><span data-stu-id="37b0e-272">At hello root level is a **module** element like hello following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   <span data-ttu-id="37b0e-273">Hello 요소 tooadd 편집 `UniqueKey="HDInsightTool"` 하는 hello 하므로 **모듈** 요소 hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-273">Edit hello element tooadd `UniqueKey="HDInsightTool"` so that hello **module** element looks like hello following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. <span data-ttu-id="37b0e-274">Hello 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-274">Save hello changes.</span></span> <span data-ttu-id="37b0e-275">이제 응용 프로그램이 IntelliJ용 Azure 도구 키트와 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-275">Your application should now be compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="37b0e-276">프로젝트 탐색기에서 hello 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-276">You can test it by right-clicking hello project name in Project Explorer.</span></span> <span data-ttu-id="37b0e-277">hello 팝업 메뉴에는 이제 hello 옵션에 **Spark 응용 프로그램 제출 tooHDInsight**합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-277">hello pop-up menu now has hello option **Submit Spark Application tooHDInsight**.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="37b0e-278">문제 해결</span><span class="sxs-lookup"><span data-stu-id="37b0e-278">Troubleshooting</span></span>

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a><span data-ttu-id="37b0e-279">로컬 실행에서 *더 큰 힙 크기를 사용하세요.* 오류 발생</span><span class="sxs-lookup"><span data-stu-id="37b0e-279">Error in local run: *Please use a larger heap size*</span></span>
<span data-ttu-id="37b0e-280">로컬 실행 하는 동안 32 비트 Java SDK를 사용 하 여 Spark 1.6에서 다음 오류 hello를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-280">In Spark 1.6, if you're using a 32-bit Java SDK during local run, you might encounter hello following errors:</span></span>

    Exception in thread "main" java.lang.IllegalArgumentException: System memory 259522560 must be at least 4.718592E8. Please use a larger heap size.
        at org.apache.spark.memory.UnifiedMemoryManager$.getMaxMemory(UnifiedMemoryManager.scala:193)
        at org.apache.spark.memory.UnifiedMemoryManager$.apply(UnifiedMemoryManager.scala:175)
        at org.apache.spark.SparkEnv$.create(SparkEnv.scala:354)
        at org.apache.spark.SparkEnv$.createDriverEnv(SparkEnv.scala:193)
        at org.apache.spark.SparkContext.createSparkEnv(SparkContext.scala:288)
        at org.apache.spark.SparkContext.<init>(SparkContext.scala:457)
        at LogQuery$.main(LogQuery.scala:53)
        at LogQuery.main(LogQuery.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:606)
        at com.intellij.rt.execution.application.AppMain.main(AppMain.java:144)

<span data-ttu-id="37b0e-281">이러한 오류 hello 힙 크기 Spark toorun에 없기 때문에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-281">These errors happen because hello heap size is not large enough for Spark toorun.</span></span> <span data-ttu-id="37b0e-282">Spark에는 적어도 471MB가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-282">Spark requires at least 471 MB.</span></span> <span data-ttu-id="37b0e-283">자세한 내용은 [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081)을 참조하세요. 하나의 간단한 솔루션은 64 비트 Java SDK toouse입니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-283">(For more information, see [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081).) One simple solution is toouse a 64-bit Java SDK.</span></span> <span data-ttu-id="37b0e-284">Hello 다음 옵션을 추가 하 여 IntelliJ의 hello JVM 설정 또한 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-284">You can also change hello JVM settings in IntelliJ by adding hello following options:</span></span>

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![IntelliJ에 "VM 옵션" 상자 옵션 toohello 추가](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a><span data-ttu-id="37b0e-286">FAQ</span><span class="sxs-lookup"><span data-stu-id="37b0e-286">FAQ</span></span>
<span data-ttu-id="37b0e-287">응용 프로그램 tooAzure 데이터 레이크 저장소 toosubmit 선택 **Interactive'** hello Azure 로그인 프로세스 중 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-287">toosubmit an application tooAzure Data Lake Store, choose **Interactive** mode during hello Azure sign-in process.</span></span> <span data-ttu-id="37b0e-288">**자동화된** 모드를 선택하는 경우 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-288">If you select **Automated** mode, you can get an error.</span></span>

![interative-signin](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

<span data-ttu-id="37b0e-290">현재 이 오류는 해결했습니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-290">Now, we resolved it.</span></span> <span data-ttu-id="37b0e-291">어떤 로그인 방법으로 Azure 데이터 레이크 클러스터 toosubmit 응용 프로그램을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-291">You can choose an Azure Data Lake Cluster toosubmit your application with any sign-in method.</span></span>

## <a name="feedback-and-known-issues"></a><span data-ttu-id="37b0e-292">사용자 의견 및 알려진 문제</span><span class="sxs-lookup"><span data-stu-id="37b0e-292">Feedback and known issues</span></span>
<span data-ttu-id="37b0e-293">현재 직접 Spark 출력 보기는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-293">Currently, viewing Spark outputs directly is not supported.</span></span>

<span data-ttu-id="37b0e-294">제안 또는 피드백이 있거나 이 플러그 인을 사용할 때 문제가 발생하는 경우 hdivstool@microsoft.com으로 메일을 보내 주시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-294">If you have any suggestions or feedback, or if you encounter any problems when you use this plug-in, email us at hdivstool@microsoft.com.</span></span>

## <span data-ttu-id="37b0e-295"><a name="seealso"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="37b0e-295"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="37b0e-296">개요: Azure HDInsight에서 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="37b0e-296">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="37b0e-297">데모</span><span class="sxs-lookup"><span data-stu-id="37b0e-297">Demo</span></span>
* <span data-ttu-id="37b0e-298">Scala 프로젝트 만들기(비디오): [Spark Scala 응용 프로그램 만들기](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="37b0e-298">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="37b0e-299">원격 디버그 (비디오): [HDInsight 클러스터에 원격으로 IntelliJ toodebug Spark 응용 프로그램에 대 한 Azure 도구 키트 사용](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="37b0e-299">Remote debug (video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="37b0e-300">시나리오</span><span class="sxs-lookup"><span data-stu-id="37b0e-300">Scenarios</span></span>
* [<span data-ttu-id="37b0e-301">BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="37b0e-301">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="37b0e-302">Spark와 기계 학습: HVAC 데이터를 사용 하 여 온도 구축 하는 HDInsight tooanalyze에서 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="37b0e-302">Spark with Machine Learning: Use Spark in HDInsight tooanalyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="37b0e-303">Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark</span><span class="sxs-lookup"><span data-stu-id="37b0e-303">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="37b0e-304">HDInsight toobuild 실시간 스트리밍 응용 프로그램에서 사용 하 여 Spark Spark 스트리밍:</span><span class="sxs-lookup"><span data-stu-id="37b0e-304">Spark Streaming: Use Spark in HDInsight toobuild real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="37b0e-305">HDInsight의 Spark를 사용하여 웹 사이트 로그 분석</span><span class="sxs-lookup"><span data-stu-id="37b0e-305">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="37b0e-306">응용 프로그램 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="37b0e-306">Creating and running applications</span></span>
* [<span data-ttu-id="37b0e-307">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="37b0e-307">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="37b0e-308">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="37b0e-308">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="37b0e-309">도구 및 확장</span><span class="sxs-lookup"><span data-stu-id="37b0e-309">Tools and extensions</span></span>
* [<span data-ttu-id="37b0e-310">Azure 도구 키트를 사용 하 여 VPN 통해 원격으로 IntelliJ toodebug Spark 응용 프로그램에 대 한</span><span class="sxs-lookup"><span data-stu-id="37b0e-310">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="37b0e-311">SSH 통해 원격으로 IntelliJ toodebug Spark 응용 프로그램에 대 한 Azure 도구 키트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-311">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="37b0e-312">Hortonworks 샌드박스에서 IntelliJ용 HDInsight Tools 사용</span><span class="sxs-lookup"><span data-stu-id="37b0e-312">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="37b0e-313">Azure Toolkit for Eclipse toocreate Spark 응용 프로그램에서에서 사용 하 여 HDInsight 도구</span><span class="sxs-lookup"><span data-stu-id="37b0e-313">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="37b0e-314">HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용</span><span class="sxs-lookup"><span data-stu-id="37b0e-314">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="37b0e-315">HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널</span><span class="sxs-lookup"><span data-stu-id="37b0e-315">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="37b0e-316">Jupyter 노트북에서 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="37b0e-316">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="37b0e-317">Jupyter 사용자 컴퓨터에 설치 하 고 tooan HDInsight Spark 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-317">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="37b0e-318">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="37b0e-318">Managing resources</span></span>
* [<span data-ttu-id="37b0e-319">Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b0e-319">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="37b0e-320">HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그</span><span class="sxs-lookup"><span data-stu-id="37b0e-320">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

