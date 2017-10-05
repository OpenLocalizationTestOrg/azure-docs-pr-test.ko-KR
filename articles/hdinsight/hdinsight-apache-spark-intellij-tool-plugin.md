---
title: "IntelliJ용 Azure 도구 키트: HDInsight 클러스터용 Spark 응용 프로그램 만들기 | Microsoft Docs"
description: "IntelliJ용 Azure 도구 키트를 사용하여 Scala로 작성된 Spark 응용 프로그램을 개발한 후 HDInsight Spark 클러스터로 제출합니다."
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
ms.openlocfilehash: 19cb8f436fa4d86f323013a5d4b3b50bf6c80a1a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-toolkit-for-intellij-to-create-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="78f28-103">IntelliJ용 Azure 도구 키트를 사용하여 HDInsight 클러스터용 Spark 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="78f28-103">Use Azure Toolkit for IntelliJ to create Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="78f28-104">IntelliJ 플러그 인용 Azure 도구 키트를 사용하여 Scala로 작성된 Spark 응용 프로그램을 개발한 후 IntelliJ IDE(통합 개발 환경)에서 직접 HDInsight Spark 클러스터로 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-104">Use the Azure Toolkit for IntelliJ plug-in to develop Spark applications written in Scala, and then submit them to an HDInsight Spark cluster directly from the IntelliJ integrated development environment (IDE).</span></span> <span data-ttu-id="78f28-105">다음과 같은 몇 가지 방식으로 플러그 인을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-105">You can use the plug-in in a few ways:</span></span>

* <span data-ttu-id="78f28-106">HDInsight Spark 클러스터에서 Scala Spark 응용 프로그램을 개발 및 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-106">Develop and submit a Scala Spark application on an HDInsight Spark cluster.</span></span>
* <span data-ttu-id="78f28-107">Azure HDInsight Spark 클러스터 리소스에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-107">Access your Azure HDInsight Spark cluster resources.</span></span>
* <span data-ttu-id="78f28-108">Scala Spark 응용 프로그램을 로컬로 개발 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-108">Develop and run a Scala Spark application locally.</span></span>

<span data-ttu-id="78f28-109">프로젝트를 만들려면 [IntelliJ용 Azure 도구 키트를 사용하여 Spark 응용 프로그램 만들기](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) 비디오를 시청하세요.</span><span class="sxs-lookup"><span data-stu-id="78f28-109">To create your project, view the [Create Spark Applications with the Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) video.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="78f28-110">이 플러그 인을 사용하면 Linux의 HDInsight Spark 클러스터용 응용 프로그램만 만들고 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-110">You can use this plug-in to create and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="78f28-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="78f28-111">Prerequisites</span></span>

- <span data-ttu-id="78f28-112">HDInsight Linux의 Apache Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-112">An Apache Spark cluster on HDInsight Linux.</span></span> <span data-ttu-id="78f28-113">자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="78f28-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
- <span data-ttu-id="78f28-114">Oracle Java Development 키트.</span><span class="sxs-lookup"><span data-stu-id="78f28-114">Oracle Java Development Kit.</span></span> <span data-ttu-id="78f28-115">[Oracle 웹 사이트](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-115">You can install it from the [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
- <span data-ttu-id="78f28-116">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="78f28-116">IntelliJ IDEA.</span></span> <span data-ttu-id="78f28-117">이 문서에서는 버전 2017.1을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-117">This article uses version 2017.1.</span></span> <span data-ttu-id="78f28-118">[JetBrains 웹 사이트](https://www.jetbrains.com/idea/download/)에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-118">You can install it from the [JetBrains website](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-azure-toolkit-for-intellij"></a><span data-ttu-id="78f28-119">IntelliJ용 Azure 도구 키트 설치</span><span class="sxs-lookup"><span data-stu-id="78f28-119">Install Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="78f28-120">설치 지침에 대해서는 [IntelliJ용 Azure 도구 키트 설치](../azure-toolkit-for-intellij-installation.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="78f28-120">For installation instructions, see [Install Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="sign-in-to-your-azure-subscription"></a><span data-ttu-id="78f28-121">Azure 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-121">Sign in to your Azure subscription</span></span>

1. <span data-ttu-id="78f28-122">IntelliJ IDE를 시작하고 Azure 탐색기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-122">Start the IntelliJ IDE, and open Azure Explorer.</span></span> <span data-ttu-id="78f28-123">**보기** 메뉴에서 **도구 창**을 선택한 후 **Azure 탐색기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-123">On the **View** menu, select **Tool Windows**, and then select **Azure Explorer**.</span></span>
       
   ![Azure 탐색기 링크](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. <span data-ttu-id="78f28-125">**Azure** 노드를 마우스 오른쪽 단추로 클릭한 다음 **로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-125">Right-click the **Azure** node, and then select **Sign In**.</span></span>

3. <span data-ttu-id="78f28-126">**Azure 로그인** 대화 상자에서 **로그인**을 선택하고 Azure 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-126">In the **Azure Sign In** dialog box, select **Sign in**, and then enter your Azure credentials.</span></span>

    ![Azure 로그인 대화 상자](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. <span data-ttu-id="78f28-128">로그인하고 나면 **구독 선택** 대화 상자에 자격 증명과 연결된 모든 Azure 구독의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-128">After you're signed in, the **Select Subscriptions** dialog box lists all the Azure subscriptions that are associated with the credentials.</span></span> <span data-ttu-id="78f28-129">**선택** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-129">Select the **Select** button.</span></span>

    ![구독 선택 대화 상자](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. <span data-ttu-id="78f28-131">**Azure 탐색기** 탭에서 **HDInsight**를 확장하여 구독에 포함된 HDInsight Spark 클러스터를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-131">On the **Azure Explorer** tab, expand **HDInsight** to view the HDInsight Spark clusters that are in your subscription.</span></span>
   
    ![Azure 탐색기의 HDInsight Spark 클러스터](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. <span data-ttu-id="78f28-133">클러스터와 연결된 리소스(예: 저장소 계정)를 표시하려면 클러스터 이름 노드를 더 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-133">To view the resources (for example, storage accounts) that are associated with the cluster, you can further expand a cluster-name node.</span></span>
   
    ![확장된 클러스터-이름 노드](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="78f28-135">HDInsight Spark 클러스터에서 Spark Scala 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="78f28-135">Run a Spark Scala application on an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="78f28-136">IntelliJ IDEA를 시작하고 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-136">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="78f28-137">**새 프로젝트** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-137">In the **New Project** dialog box, do the following:</span></span> 

   <span data-ttu-id="78f28-138">a.</span><span class="sxs-lookup"><span data-stu-id="78f28-138">a.</span></span> <span data-ttu-id="78f28-139">**HDInsight** > **HDInsight의 Spark(Scala)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-139">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="78f28-140">b.</span><span class="sxs-lookup"><span data-stu-id="78f28-140">b.</span></span> <span data-ttu-id="78f28-141">**빌드 도구** 목록에서 요구 사항에 따라 다음 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-141">In the **Build tool** list, select either of the following, according to your need:</span></span>

      * <span data-ttu-id="78f28-142">Scala 프로젝트 만들기 마법사 지원에 대해 **Maven**</span><span class="sxs-lookup"><span data-stu-id="78f28-142">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="78f28-143">종속성 관리 및 Scala 프로젝트에 대한 빌드에 대해 **SBT**</span><span class="sxs-lookup"><span data-stu-id="78f28-143">**SBT**, for managing the dependencies and building for the Scala project</span></span>

    ![새 프로젝트 대화 상자](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. <span data-ttu-id="78f28-145">**다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-145">Select **Next**.</span></span>

3. <span data-ttu-id="78f28-146">Scala 프로젝트 생성 마법사는 Scala 플러그 인이 설치되어 있는지 여부를 자동으로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-146">The Scala project-creation wizard automatically detects whether you've installed the Scala plug-in.</span></span> <span data-ttu-id="78f28-147">**설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-147">Select **Install**.</span></span>

   ![Scala 플러그 인 검사](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. <span data-ttu-id="78f28-149">Scala 플러그 인을 다운로드하려면 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-149">To download the Scala plug-in, select **OK**.</span></span> <span data-ttu-id="78f28-150">지침에 따라 IntelliJ를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-150">Follow the instructions to restart IntelliJ.</span></span> 

   ![Scala 플러그 인 설치 대화 상자](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. <span data-ttu-id="78f28-152">**새 프로젝트** 창에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-152">In the **New Project** window, do the following:</span></span>  

    ![Spark SDK 선택](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   <span data-ttu-id="78f28-154">a.</span><span class="sxs-lookup"><span data-stu-id="78f28-154">a.</span></span> <span data-ttu-id="78f28-155">프로젝트 이름 및 위치를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-155">Enter a project name and location.</span></span>

   <span data-ttu-id="78f28-156">b.</span><span class="sxs-lookup"><span data-stu-id="78f28-156">b.</span></span> <span data-ttu-id="78f28-157">**프로젝트 SDK** 드롭다운 목록에서 Spark 2.x 클러스터에 대해 **Java 1.8**을 선택하거나 Spark 1.x 클러스터에 대해 **Java 1.7**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-157">In the **Project SDK** drop-down list, select **Java 1.8** for the Spark 2.x cluster, or select **Java 1.7** for the Spark 1.x cluster.</span></span>

   <span data-ttu-id="78f28-158">c.</span><span class="sxs-lookup"><span data-stu-id="78f28-158">c.</span></span> <span data-ttu-id="78f28-159">**Spark 버전** 드롭다운 목록에서 Scala 프로젝트 생성 마법사는 Spark SDK 및 Scala SDK에 대한 적절한 버전을 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-159">In the **Spark version** drop-down list, Scala project creation wizard integrates the proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="78f28-160">Spark 클러스터 2.0 이하 버전을 사용하는 경우 **Spark 1.x**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-160">If the Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="78f28-161">그렇지 않은 경우 **Spark2.x**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-161">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="78f28-162">이 예제에서는 **Spark 2.0.2(Scala 2.11.8)**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-162">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

6. <span data-ttu-id="78f28-163">**마침**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-163">Select **Finish**.</span></span>

7. <span data-ttu-id="78f28-164">Spark 프로젝트가 자동으로 아티팩트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-164">The Spark project automatically creates an artifact for you.</span></span> <span data-ttu-id="78f28-165">이 아티팩트를 보려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-165">To view the artifact, do the following:</span></span>

   <span data-ttu-id="78f28-166">a.</span><span class="sxs-lookup"><span data-stu-id="78f28-166">a.</span></span> <span data-ttu-id="78f28-167">**파일** 메뉴에서 **프로젝트 구조**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-167">On the **File** menu, select **Project Structure**.</span></span>

   <span data-ttu-id="78f28-168">b.</span><span class="sxs-lookup"><span data-stu-id="78f28-168">b.</span></span> <span data-ttu-id="78f28-169">**프로젝트 구조** 대화 상자에서 **아티팩트**를 선택하여 만들어지는 기본 아티팩트를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-169">In the **Project Structure** dialog box, select **Artifacts** to view the default artifact that is created.</span></span> <span data-ttu-id="78f28-170">더하기 기호(**+**)를 선택하여 사용자 고유의 아티팩트를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-170">You can also create your own artifact by selecting the plus sign (**+**).</span></span>

      ![대화 상자의 아티팩트 정보](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. <span data-ttu-id="78f28-172">다음을 수행하여 응용 프로그램 소스 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-172">Add your application source code by doing the following:</span></span>

   <span data-ttu-id="78f28-173">a.</span><span class="sxs-lookup"><span data-stu-id="78f28-173">a.</span></span> <span data-ttu-id="78f28-174">프로젝트 탐색기에서 **src**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **Scala 클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-174">In Project Explorer, right-click **src**, point to **New**, and then select **Scala Class**.</span></span>
      
      ![프로젝트 탐색기에서 Scala 클래스 만들기에 대한 명령](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   <span data-ttu-id="78f28-176">b.</span><span class="sxs-lookup"><span data-stu-id="78f28-176">b.</span></span> <span data-ttu-id="78f28-177">**새 Scala 클래스 만들기** 대화 상자에서 이름을 제공하고 **종류** 상자에 **개체**를 선택한 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-177">In the **Create New Scala Class** dialog box, provide a name, select **Object** in the **Kind** box, and then select **OK**.</span></span>
      
      ![새 Scala 클래스 만들기 대화 상자](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   <span data-ttu-id="78f28-179">c.</span><span class="sxs-lookup"><span data-stu-id="78f28-179">c.</span></span> <span data-ttu-id="78f28-180">**MyClusterApp.scala** 파일에 다음 코드를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-180">In the **MyClusterApp.scala** file, paste the following code.</span></span> <span data-ttu-id="78f28-181">이 코드는 HVAC.csv(모든 HDInsight Spark 클러스터에서 사용 가능)에서 데이터를 읽고, CSV 파일의 일곱 번째 열에 한 자리 수만 있는 행을 검색하고, 출력을 클러스터의 기본 저장 컨테이너 아래의 **/HVACOut**에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-181">The code reads the data from HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that have only one digit in the seventh column in the CSV file, and writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>

        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
    
        object MyClusterApp{
            def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
    
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
    
            //find the rows that have only one digit in the seventh column in the CSV file
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
    
            rdd1.saveAsTextFile("wasb:///HVACOut")
            }
    
        }

9. <span data-ttu-id="78f28-182">다음을 수행하여 HDInsight Spark 클러스터에서 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-182">Run the application on an HDInsight Spark cluster by doing the following:</span></span>

   <span data-ttu-id="78f28-183">a.</span><span class="sxs-lookup"><span data-stu-id="78f28-183">a.</span></span> <span data-ttu-id="78f28-184">프로젝트 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭한 다음 **HDInsight에 Spark 응용 프로그램 제출**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-184">In Project Explorer, right-click the project name, and then select **Submit Spark Application to HDInsight**.</span></span>
      
      ![HDInsight에 Spark 응용 프로그램 제출 명령](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   <span data-ttu-id="78f28-186">b.</span><span class="sxs-lookup"><span data-stu-id="78f28-186">b.</span></span> <span data-ttu-id="78f28-187">Azure 구독 자격 증명을 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-187">You are prompted to enter your Azure subscription credentials.</span></span> <span data-ttu-id="78f28-188">**Spark 제출** 대화 상자에 다음 값을 제공한 다음 **제출**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-188">In the **Spark Submission** dialog box, provide the following values, and then select **Submit**.</span></span>
      
      * <span data-ttu-id="78f28-189">**Spark 클러스터(Linux만 해당)**의 경우 응용 프로그램을 실행하려는 HDInsight Spark 클러스터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-189">For **Spark clusters (Linux only)**, select the HDInsight Spark cluster on which you want to run your application.</span></span>

      * <span data-ttu-id="78f28-190">IntelliJ 프로젝트에서 아티팩트를 선택하거나 하드 드라이브에서 아티팩트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-190">Select an artifact from the IntelliJ project, or select one from the hard drive.</span></span>

      * <span data-ttu-id="78f28-191">**주 클래스 이름** 상자에서 줄임표(**...**)를 선택하고 응용 프로그램 소스 코드에서 주 클래스를 선택한 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-191">In the **Main class name** box, select the ellipsis (**...**), select the main class in your application source code, and then select **OK**.</span></span>

        ![주 클래스 선택 대화 상자](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * <span data-ttu-id="78f28-193">이 예제의 응용 프로그램 코드에는 명령줄 인수가 필요하지 않거나 JAR 또는 파일을 참조하지 않으므로 나머지 상자를 비워둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-193">Because the application code in this example does not require command-line arguments or reference JARs or files, you can leave the remaining boxes empty.</span></span> <span data-ttu-id="78f28-194">모든 정보를 제공하면 대화 상자는 다음 이미지와 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-194">After you provide all the information, the dialog box should resemble the following image.</span></span>
        
        ![Spark 제출 대화 상자](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   <span data-ttu-id="78f28-196">c.</span><span class="sxs-lookup"><span data-stu-id="78f28-196">c.</span></span> <span data-ttu-id="78f28-197">창 아래쪽의 **Spark 제출** 탭에 진행 상태가 표시되기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-197">The **Spark Submission** tab at the bottom of the window should start displaying the progress.</span></span> <span data-ttu-id="78f28-198">또한 **Spark 제출** 창에서 빨간색 단추를 선택하여 응용 프로그램을 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-198">You can also stop the application by selecting the red button in the **Spark Submission** window.</span></span>
      
      ![Spark 제출 창](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      <span data-ttu-id="78f28-200">작업 출력에 액세스하는 방법을 알아보려면 이 문서의 뒷부분에 나오는 "IntelliJ용 Azure 도구 키트를 사용하여 HDInsight Spark 클러스터 액세스 및 관리" 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="78f28-200">To learn how to access the job output, see the "Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ" section later in this article.</span></span>

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="78f28-201">HDInsight Spark 클러스터에서 Spark Scala 응용 프로그램 실행 또는 디버그</span><span class="sxs-lookup"><span data-stu-id="78f28-201">Run or debug a Spark Scala application on an HDInsight Spark cluster</span></span>
<span data-ttu-id="78f28-202">Spark 응용 프로그램을 클러스터에 제출하는 또 다른 권장되는 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-202">We also recommend another way of submitting the Spark application to the cluster.</span></span> <span data-ttu-id="78f28-203">**구성 실행/디버그** IDE에서 매개 변수를 설정하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-203">You can do so by setting the parameters in the **Run/Debug configurations** IDE.</span></span> <span data-ttu-id="78f28-204">자세한 내용은 [IntelliJ용 Azure 도구 키트를 사용하여 SSH를 통해 HDInsight 클러스터에서 원격으로 Spark 응용 프로그램 디버그](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="78f28-204">For more information, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a><span data-ttu-id="78f28-205">IntelliJ용 Azure 도구 키트를 사용하여 HDInsight Spark 클러스터 액세스 및 관리</span><span class="sxs-lookup"><span data-stu-id="78f28-205">Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="78f28-206">IntelliJ용 Azure 도구 키트를 사용하여 다양한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-206">You can perform various operations by using Azure Toolkit for IntelliJ.</span></span>

### <a name="access-the-job-view"></a><span data-ttu-id="78f28-207">작업 보기 액세스</span><span class="sxs-lookup"><span data-stu-id="78f28-207">Access the job view</span></span>
1. <span data-ttu-id="78f28-208">Azure 탐색기에서 **HDInsight**, Spark 클러스터 이름을 차례로 확장한 다음 **작업**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-208">In Azure Explorer, expand **HDInsight**, expand the Spark cluster name, and then select **Jobs**.</span></span>  

    ![작업 보기 노드](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. <span data-ttu-id="78f28-210">오른쪽 창의 **Spark 작업 보기** 탭에는 클러스터에서 실행된 모든 응용 프로그램이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-210">In the right pane, the **Spark Job View** tab displays all the applications that were run on the cluster.</span></span> <span data-ttu-id="78f28-211">자세한 내용을 보려면 원하는 응용 프로그램 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-211">Select the name of the application for which you want to see more details.</span></span>

    ![응용 프로그램 세부 정보](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. <span data-ttu-id="78f28-213">실행 중인 기본 작업 정보를 표시하려면 작업 그래프 위로 마우스를 가져갑니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-213">To display basic running job information, hover over the job graph.</span></span> <span data-ttu-id="78f28-214">모든 작업이 생성하는 단계 그래프 및 정보를 보려면 작업 그래프에서 노드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-214">To view the stages graph and information that every job generates, select a node on the job graph.</span></span>

    ![작업 단계 세부 정보](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. <span data-ttu-id="78f28-216">*드라이버 Stderr*, *드라이버 Stdout* 및 *디렉터리 정보*와 같은 자주 사용되는 로그를 보려면 **로그** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-216">To view frequently used logs, such as *Driver Stderr*, *Driver Stdout*, and *Directory Info*, select the **Log** tab.</span></span>

    ![로그 세부 정보](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. <span data-ttu-id="78f28-218">창 맨 위에 있는 링크를 클릭하여 Spark 기록 UI 및 YARN UI(응용 프로그램 수준)를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-218">You can also view the Spark history UI and the YARN UI (at the application level) by selecting a link at the top of the window.</span></span>

### <a name="access-the-spark-history-server"></a><span data-ttu-id="78f28-219">Spark 기록 서버 액세스</span><span class="sxs-lookup"><span data-stu-id="78f28-219">Access the Spark history server</span></span>
1. <span data-ttu-id="78f28-220">Azure 탐색기에서 **HDInsight**를 확장하고, 마우스 오른쪽 단추로 Spark 클러스터 이름을 클릭한 다음 **Spark 기록 UI 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-220">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> 

2. <span data-ttu-id="78f28-221">메시지가 나타나면 클러스터를 설정할 때 지정한 클러스터의 관리자 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-221">When you're prompted, enter the cluster's admin credentials, which you specified when you set up the cluster.</span></span>

3. <span data-ttu-id="78f28-222">Spark 기록 서버 대시보드에서 응용 프로그램 이름을 사용하여 방금 실행을 마친 응용 프로그램을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-222">On the Spark history server dashboard, you can use the application name to look for the application that you just finished running.</span></span> <span data-ttu-id="78f28-223">위의 코드에서 `val conf = new SparkConf().setAppName("MyClusterApp")`을 사용하여 응용 프로그램 이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-223">In the preceding code, you set the application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="78f28-224">따라서 Spark 응용 프로그램 이름은 **MyClusterApp**입니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-224">Therefore, your Spark application name is **MyClusterApp**.</span></span>

### <a name="start-the-ambari-portal"></a><span data-ttu-id="78f28-225">Ambari 포털 시작</span><span class="sxs-lookup"><span data-stu-id="78f28-225">Start the Ambari portal</span></span>
1. <span data-ttu-id="78f28-226">Azure 탐색기에서 **HDInsight**를 확장하고, 마우스 오른쪽 단추로 Spark 클러스터 이름을 클릭한 다음 **클러스터 관리 포털(Ambari) 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-226">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 

2. <span data-ttu-id="78f28-227">메시지가 표시되면 클러스터에 대한 관리자 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-227">When you're prompted, enter the admin credentials for the cluster.</span></span> <span data-ttu-id="78f28-228">클러스터 설치 프로세스 동안 이러한 자격 증명을 지정했을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-228">You specified these credentials during the cluster setup process.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="78f28-229">Azure 구독 관리</span><span class="sxs-lookup"><span data-stu-id="78f28-229">Manage Azure subscriptions</span></span>
<span data-ttu-id="78f28-230">기본적으로 IntelliJ용 Azure 도구 키트에는 모든 Azure 구독의 Spark 클러스터가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-230">By default, Azure Toolkit for IntelliJ lists the Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="78f28-231">필요한 경우 액세스하려는 구독을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-231">If necessary, you can specify the subscriptions that you want to access.</span></span> 

1. <span data-ttu-id="78f28-232">Azure 탐색기에서 **Azure** 루트 노드를 마우스 오른쪽 단추로 클릭한 다음 **구독 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-232">In Azure Explorer, right-click the **Azure** root node, and then select **Manage Subscriptions**.</span></span> 

2. <span data-ttu-id="78f28-233">대화 상자에서 액세스하지 않으려는 구독 옆의 확인란을 선택 취소하고 **닫기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-233">In the dialog box, clear the check boxes next to the subscriptions that you don't want to access, and then select **Close**.</span></span> <span data-ttu-id="78f28-234">Azure 구독에서 로그아웃하려는 경우 **로그아웃**을 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-234">You can also select **Sign Out** if you want to sign out of your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="78f28-235">로컬로 Spark Scala 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="78f28-235">Run a Spark Scala application locally</span></span>
<span data-ttu-id="78f28-236">IntelliJ용 Azure 도구 키트를 사용하여 워크스테이션에서 Spark Scala 응용 프로그램을 로컬로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-236">You can use Azure Toolkit for IntelliJ to run Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="78f28-237">일반적으로 이러한 응용 프로그램은 저장소 컨테이너와 같은 클러스터 리소스에 액세스할 필요가 없으므로 로컬로 실행하고 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-237">The applications usually don't need access to cluster resources, such as storage containers, and you can run and test them locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="78f28-238">필수 요소</span><span class="sxs-lookup"><span data-stu-id="78f28-238">Prerequisite</span></span>
<span data-ttu-id="78f28-239">Windows 컴퓨터에서 로컬 Spark Scala 응용 프로그램을 실행하는 동안 [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356)에서 설명한 예외가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-239">While you're running the local Spark Scala application on a Windows computer, you might get an exception, as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span></span> <span data-ttu-id="78f28-240">이 예외는 Windows에 WinUtils.exe가 없기 때문에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-240">The exception occurs because WinUtils.exe is missing on Windows.</span></span> 

<span data-ttu-id="78f28-241">이 오류를 해결하려면 [실행 파일을 다운로드](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe)하여 **C:\WinUtils\bin** 등의 위치에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-241">To resolve this error, [download the executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location such as **C:\WinUtils\bin**.</span></span> <span data-ttu-id="78f28-242">그런 다음 **HADOOP_HOME** 환경 변수를 추가하고 이 변수 값을 **C\WinUtils**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-242">Then, add the environment variable **HADOOP_HOME**, and set the value of the variable to **C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="78f28-243">로컬 Spark Scala 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="78f28-243">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="78f28-244">IntelliJ IDEA를 시작하고 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-244">Start IntelliJ IDEA, and create a project.</span></span> 

2. <span data-ttu-id="78f28-245">**새 프로젝트** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-245">In the **New Project** dialog box, do the following:</span></span>
   
    <span data-ttu-id="78f28-246">a.</span><span class="sxs-lookup"><span data-stu-id="78f28-246">a.</span></span> <span data-ttu-id="78f28-247">**HDInsight** > **HDInsight의 Spark 로컬 실행 샘플(Scala)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-247">Select **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)**.</span></span>

    <span data-ttu-id="78f28-248">b.</span><span class="sxs-lookup"><span data-stu-id="78f28-248">b.</span></span> <span data-ttu-id="78f28-249">**빌드 도구** 목록에서 요구 사항에 따라 다음 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-249">In the **Build tool** list, select either of the following, according to your need:</span></span>

      * <span data-ttu-id="78f28-250">Scala 프로젝트 만들기 마법사 지원에 대해 **Maven**</span><span class="sxs-lookup"><span data-stu-id="78f28-250">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="78f28-251">종속성 관리 및 Scala 프로젝트에 대한 빌드에 대해 **SBT**</span><span class="sxs-lookup"><span data-stu-id="78f28-251">**SBT**, for managing the dependencies and building for the Scala project</span></span>

    ![새 프로젝트 대화 상자](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. <span data-ttu-id="78f28-253">**다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-253">Select **Next**.</span></span>
 
4. <span data-ttu-id="78f28-254">다음 창에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-254">In the next window, do the following:</span></span>
   
    <span data-ttu-id="78f28-255">a.</span><span class="sxs-lookup"><span data-stu-id="78f28-255">a.</span></span> <span data-ttu-id="78f28-256">프로젝트 이름 및 위치를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-256">Enter a project name and location.</span></span>

    <span data-ttu-id="78f28-257">b.</span><span class="sxs-lookup"><span data-stu-id="78f28-257">b.</span></span> <span data-ttu-id="78f28-258">**프로젝트 SDK** 드롭다운 목록에서 1.7 버전보다 최신인 Java 버전을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-258">In the **Project SDK** drop-down list, select a Java version that's later than version 1.7.</span></span>

    <span data-ttu-id="78f28-259">c.</span><span class="sxs-lookup"><span data-stu-id="78f28-259">c.</span></span> <span data-ttu-id="78f28-260">**Spark 버전** 드롭다운 목록에서 사용하려는 Scala 버전을 선택합니다. Spark 2.0의 경우는 Scala 2.11.x를, Spark 1.6의 경우는 Scala 2.10.x를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-260">In the **Spark Version** drop-down list, select the version of Scala that you want to use: Scala 2.11.x for Spark 2.0 or Scala 2.10.x for Spark 1.6.</span></span>

    ![새 프로젝트 대화 상자](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. <span data-ttu-id="78f28-262">**마침**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-262">Select **Finish**.</span></span>

6. <span data-ttu-id="78f28-263">템플릿은 컴퓨터에서 로컬로 실행할 수 있는 샘플 코드(**LogQuery**)를 **src** 폴더 아래에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-263">The template adds a sample code (**LogQuery**) under the **src** folder that you can run locally on your computer.</span></span>
   
    ![LogQuery 위치](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. <span data-ttu-id="78f28-265">**LogQuery** 응용 프로그램을 마우스 오른쪽 단추로 클릭한 다음 **"'LogQuery' 실행"**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-265">Right-click the **LogQuery** application, and then select **Run 'LogQuery'**.</span></span> <span data-ttu-id="78f28-266">아래쪽의 **실행** 탭에 다음과 같은 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-266">On the **Run** tab at the bottom, you see an output like the following:</span></span>
   
   ![Spark 응용 프로그램 로컬 실행 결과](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-to-use-azure-toolkit-for-intellij"></a><span data-ttu-id="78f28-268">IntelliJ용 Azure 도구 키트를 사용하도록 기존 IntelliJ IDEA 응용 프로그램 변환</span><span class="sxs-lookup"><span data-stu-id="78f28-268">Convert existing IntelliJ IDEA applications to use Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="78f28-269">IntelliJ IDEA에서 만든 기존 Spark Scala 응용 프로그램을 IntelliJ용 Azure 도구 키트와 호환되도록 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-269">You can convert the existing Spark Scala applications that you created in IntelliJ IDEA to be compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="78f28-270">이렇게 하면 플러그 인을 사용하여 HDInsight Spark 클러스터에 응용 프로그램을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-270">You can then use the plug-in to submit the applications to an HDInsight Spark cluster.</span></span>

1. <span data-ttu-id="78f28-271">IntelliJ IDEA를 통해 만들어진 기존 Spark Scala 응용 프로그램의 경우 관련된 .iml 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-271">For an existing Spark Scala application that was created through IntelliJ IDEA, open the associated .iml file.</span></span>

2. <span data-ttu-id="78f28-272">루트 수준에 다음과 같은 **module** 요소가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-272">At the root level is a **module** element like the following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   <span data-ttu-id="78f28-273">**module** 요소가 다음과 같이 표시되도록 해당 요소를 편집하여 `UniqueKey="HDInsightTool"`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-273">Edit the element to add `UniqueKey="HDInsightTool"` so that the **module** element looks like the following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. <span data-ttu-id="78f28-274">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-274">Save the changes.</span></span> <span data-ttu-id="78f28-275">이제 응용 프로그램이 IntelliJ용 Azure 도구 키트와 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-275">Your application should now be compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="78f28-276">프로젝트 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭하여 이 테스트를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-276">You can test it by right-clicking the project name in Project Explorer.</span></span> <span data-ttu-id="78f28-277">이제 팝업 메뉴에 **HDInsight에 Spark 응용 프로그램 제출** 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-277">The pop-up menu now has the option **Submit Spark Application to HDInsight**.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="78f28-278">문제 해결</span><span class="sxs-lookup"><span data-stu-id="78f28-278">Troubleshooting</span></span>

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a><span data-ttu-id="78f28-279">로컬 실행에서 *더 큰 힙 크기를 사용하세요.* 오류 발생</span><span class="sxs-lookup"><span data-stu-id="78f28-279">Error in local run: *Please use a larger heap size*</span></span>
<span data-ttu-id="78f28-280">Spark 1.6에서 로컬 실행 동안 32비트 Java SDK를 사용하는 경우 다음과 같은 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-280">In Spark 1.6, if you're using a 32-bit Java SDK during local run, you might encounter the following errors:</span></span>

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

<span data-ttu-id="78f28-281">이러한 오류는 힙 크기가 실행할 Spark에 대해 충분히 크지 않기 때문에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-281">These errors happen because the heap size is not large enough for Spark to run.</span></span> <span data-ttu-id="78f28-282">Spark에는 적어도 471MB가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-282">Spark requires at least 471 MB.</span></span> <span data-ttu-id="78f28-283">자세한 내용은 [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081)을 참조하세요. 한 가지 간단한 해결 방법은 64비트 Java SDK를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-283">(For more information, see [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081).) One simple solution is to use a 64-bit Java SDK.</span></span> <span data-ttu-id="78f28-284">또한 다음 옵션을 추가하여 IntelliJ의 JVM 설정을 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-284">You can also change the JVM settings in IntelliJ by adding the following options:</span></span>

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![IntelliJ의 "VM 옵션" 상자에 옵션 추가](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a><span data-ttu-id="78f28-286">FAQ</span><span class="sxs-lookup"><span data-stu-id="78f28-286">FAQ</span></span>
<span data-ttu-id="78f28-287">응용 프로그램을 Azure Data Lake Store에 제출하려면 Azure 로그인 프로세스 중에 **대화형** 모드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-287">To submit an application to Azure Data Lake Store, choose **Interactive** mode during the Azure sign-in process.</span></span> <span data-ttu-id="78f28-288">**자동화된** 모드를 선택하는 경우 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-288">If you select **Automated** mode, you can get an error.</span></span>

![interative-signin](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

<span data-ttu-id="78f28-290">현재 이 오류는 해결했습니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-290">Now, we resolved it.</span></span> <span data-ttu-id="78f28-291">임의의 로그인 방법으로 응용 프로그램을 제출하기 위해 Azure Data Lake 클러스터를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-291">You can choose an Azure Data Lake Cluster to submit your application with any sign-in method.</span></span>

## <a name="feedback-and-known-issues"></a><span data-ttu-id="78f28-292">사용자 의견 및 알려진 문제</span><span class="sxs-lookup"><span data-stu-id="78f28-292">Feedback and known issues</span></span>
<span data-ttu-id="78f28-293">현재 직접 Spark 출력 보기는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-293">Currently, viewing Spark outputs directly is not supported.</span></span>

<span data-ttu-id="78f28-294">제안 또는 피드백이 있거나 이 플러그 인을 사용할 때 문제가 발생하는 경우 hdivstool@microsoft.com으로 메일을 보내 주시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="78f28-294">If you have any suggestions or feedback, or if you encounter any problems when you use this plug-in, email us at hdivstool@microsoft.com.</span></span>

## <span data-ttu-id="78f28-295"><a name="seealso"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="78f28-295"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="78f28-296">개요: Azure HDInsight에서 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="78f28-296">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="78f28-297">데모</span><span class="sxs-lookup"><span data-stu-id="78f28-297">Demo</span></span>
* <span data-ttu-id="78f28-298">Scala 프로젝트 만들기(비디오): [Spark Scala 응용 프로그램 만들기](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="78f28-298">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="78f28-299">원격 디버그(비디오): [IntelliJ용 Azure 도구 키트를 사용하여 HDInsight 클러스터에서 원격으로 Spark 응용 프로그램 디버그](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="78f28-299">Remote debug (video): [Use Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="78f28-300">시나리오</span><span class="sxs-lookup"><span data-stu-id="78f28-300">Scenarios</span></span>
* [<span data-ttu-id="78f28-301">BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="78f28-301">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="78f28-302">기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="78f28-302">Spark with Machine Learning: Use Spark in HDInsight to analyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="78f28-303">기계 학습과 Spark: 음식 검사 결과를 예측하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="78f28-303">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="78f28-304">Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="78f28-304">Spark Streaming: Use Spark in HDInsight to build real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="78f28-305">HDInsight의 Spark를 사용하여 웹 사이트 로그 분석</span><span class="sxs-lookup"><span data-stu-id="78f28-305">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="78f28-306">응용 프로그램 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="78f28-306">Creating and running applications</span></span>
* [<span data-ttu-id="78f28-307">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="78f28-307">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="78f28-308">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="78f28-308">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="78f28-309">도구 및 확장</span><span class="sxs-lookup"><span data-stu-id="78f28-309">Tools and extensions</span></span>
* [<span data-ttu-id="78f28-310">IntelliJ용 Azure 도구 키트를 사용하여 VPN을 통해 원격으로 Spark 응용 프로그램 디버그</span><span class="sxs-lookup"><span data-stu-id="78f28-310">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="78f28-311">IntelliJ용 Azure 도구 키트를 사용하여 SSH를 통해 원격으로 Spark 응용 프로그램 디버그</span><span class="sxs-lookup"><span data-stu-id="78f28-311">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="78f28-312">Hortonworks 샌드박스에서 IntelliJ용 HDInsight Tools 사용</span><span class="sxs-lookup"><span data-stu-id="78f28-312">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="78f28-313">Eclipse용 Azure 도구 키트의 HDInsight 도구를 사용하여 Spark 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="78f28-313">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="78f28-314">HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용</span><span class="sxs-lookup"><span data-stu-id="78f28-314">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="78f28-315">HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널</span><span class="sxs-lookup"><span data-stu-id="78f28-315">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="78f28-316">Jupyter 노트북에서 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="78f28-316">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="78f28-317">컴퓨터에 Jupyter를 설치하고 HDInsight Spark 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="78f28-317">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="78f28-318">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="78f28-318">Managing resources</span></span>
* [<span data-ttu-id="78f28-319">Azure HDInsight에서 Apache Spark 클러스터에 대한 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="78f28-319">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="78f28-320">HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그</span><span class="sxs-lookup"><span data-stu-id="78f28-320">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

