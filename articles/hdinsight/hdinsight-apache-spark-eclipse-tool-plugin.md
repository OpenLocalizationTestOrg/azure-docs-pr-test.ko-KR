---
title: "Eclipse용 Azure 도구 키트 - HDInsight Spark용 Scala 응용 프로그램 만들기 | Microsoft Docs"
description: "Eclipse용 Azure 도구 키트의 HDInsight Tools를 사용하여 Scala로 작성된 Spark 응용 프로그램을 개발한 후 Eclipse IDE에서 직접 HDInsight Spark 클러스터로 제출합니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f6c79550-5803-4e13-b541-e86c4abb420b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 4bcb1987a62c0b7f4965e6fd257315e820004238
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-toolkit-for-eclipse-to-create-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="32660-103">Eclipse용 Azure 도구 키트를 사용하여 HDInsight 클러스터용 Spark 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="32660-103">Use Azure Toolkit for Eclipse to create Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="32660-104">Eclipse용 Azure 도구 키트의 HDInsight Tools를 사용하여 Scala로 작성된 Spark 응용 프로그램을 개발하고 Eclipse IDE에서 직접 Azure HDInsight Spark 클러스터로 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-104">Use HDInsight Tools in Azure Toolkit for Eclipse to develop Spark applications written in Scala and submit them to an Azure HDInsight Spark cluster, directly from the Eclipse IDE.</span></span> <span data-ttu-id="32660-105">다음과 같은 방법으로 HDInsight Tools 플러그 인을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32660-105">You can use the HDInsight Tools plug-in in a few different ways:</span></span>

* <span data-ttu-id="32660-106">HDInsight Spark 클러스터에서 Scala Spark 응용 프로그램을 개발 및 제출하려면</span><span class="sxs-lookup"><span data-stu-id="32660-106">To develop and submit a Scala Spark application on an HDInsight Spark cluster</span></span>
* <span data-ttu-id="32660-107">Azure HDInsight Spark 클러스터 리소스에 액세스하려면</span><span class="sxs-lookup"><span data-stu-id="32660-107">To access your Azure HDInsight Spark cluster resources</span></span>
* <span data-ttu-id="32660-108">Scala Spark 응용 프로그램을 로컬로 개발 및 실행하려면</span><span class="sxs-lookup"><span data-stu-id="32660-108">To develop and run a Scala Spark application locally</span></span>

> [!IMPORTANT]
> <span data-ttu-id="32660-109">이 도구를 사용하면 Linux의 HDInsight Spark 클러스터용 응용 프로그램만 만들고 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32660-109">This tool can be used to create and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="32660-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="32660-110">Prerequisites</span></span>

* <span data-ttu-id="32660-111">HDInsight의 Apache Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="32660-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="32660-112">자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32660-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="32660-113">Eclipse IDE 런타임에 사용되는 Oracle Java Development 키트 버전 8입니다.</span><span class="sxs-lookup"><span data-stu-id="32660-113">Oracle Java Development Kit version 8, which is used for the Eclipse IDE runtime.</span></span> <span data-ttu-id="32660-114">[Oracle 웹 사이트](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32660-114">You can download it from the [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="32660-115">Eclipse IDE.</span><span class="sxs-lookup"><span data-stu-id="32660-115">Eclipse IDE.</span></span> <span data-ttu-id="32660-116">이 문서에서는 Eclipse Neon을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-116">This article uses Eclipse Neon.</span></span> <span data-ttu-id="32660-117">[Eclipse 웹 사이트](https://www.eclipse.org/downloads/)에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32660-117">You can install it from the [Eclipse website](https://www.eclipse.org/downloads/).</span></span>   
* <span data-ttu-id="32660-118">Spark SDK.</span><span class="sxs-lookup"><span data-stu-id="32660-118">Spark SDK.</span></span> <span data-ttu-id="32660-119">[GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32660-119">You can download it from [GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).</span></span>


## <a name="install-hdinsight-tools-in-azure-toolkit-for-eclipse-and-scala-plugin"></a><span data-ttu-id="32660-120">Azure 도구 키트에 Eclipse 및 Scala 플러그 인에 대 한 HDInsight 도구를 설치</span><span class="sxs-lookup"><span data-stu-id="32660-120">Install HDInsight Tools in Azure Toolkit for Eclipse and Scala Plugin</span></span>
### <a name="install-hdinsight-tools"></a><span data-ttu-id="32660-121">HDInsight Tools 설치</span><span class="sxs-lookup"><span data-stu-id="32660-121">Install HDInsight Tools</span></span>
<span data-ttu-id="32660-122">Eclipse용 HDInsight Tools는 Eclipse용 Azure 도구 키트의 일부분으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="32660-122">HDInsight Tools for Eclipse is available as part of Azure Toolkit for Eclipse.</span></span> <span data-ttu-id="32660-123">설치 지침은 [Eclipse용 Azure 도구 키트 설치](../azure-toolkit-for-eclipse-installation.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32660-123">For installation instructions, see [Installing Azure Toolkit for Eclipse](../azure-toolkit-for-eclipse-installation.md).</span></span>
### <a name="install-scala-plugin"></a><span data-ttu-id="32660-124">Scala 플러그 인 설치</span><span class="sxs-lookup"><span data-stu-id="32660-124">Install Scala Plugin</span></span>
<span data-ttu-id="32660-125">Intellij을 열 때 HDInsight 도구 자동 여부 Scala 플러그 인 설치 되어 있는지 여부를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-125">When you open the Intellij, the HDInsight Tools auto detects whether you installed Scala plugin or not.</span></span> <span data-ttu-id="32660-126">클릭 **확인** 계속 하려면 Eclipse 마켓플레이스에서 설치 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="32660-126">Click **OK** to continue and follow the instructions to install by the Eclipse Marketplace.</span></span>

 ![자동 설치 Scala 플러그 인](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala.png)

## <a name="sign-in-to-your-azure-subscription"></a><span data-ttu-id="32660-128">Azure 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-128">Sign in to your Azure subscription</span></span>
1. <span data-ttu-id="32660-129">Eclipse IDE를 시작하고 Azure 탐색기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="32660-129">Start the Eclipse IDE and open Azure Explorer.</span></span> <span data-ttu-id="32660-130">**창** 메뉴에서 **보기 표시**를 클릭한 다음 **기타**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-130">On the **Window** menu, click **Show View**, and then click **Other**.</span></span> <span data-ttu-id="32660-131">열린 대화 상자에서 **Azure**를 확장하고 **Azure 탐색기**를 클릭한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-131">In the dialog box that opens, expand **Azure**, click **Azure Explorer**, and then click **OK**.</span></span>

    ![보기 표시 대화 상자](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-1.png)
2. <span data-ttu-id="32660-133">**Azure** 노드를 마우스 오른쪽 단추로 클릭한 다음 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-133">Right-click the **Azure** node, and then click **Sign in**.</span></span>
3. <span data-ttu-id="32660-134">**Azure 로그인** 대화 상자에서 인증 모드를 선택하고 **로그인**을 클릭하고 Azure 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-134">In the **Azure Sign In** dialog box, choose the authentication method, click **Sign in**, and enter your Azure credentials.</span></span>
   
    ![Azure 로그인 대화 상자](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-2.png)
4. <span data-ttu-id="32660-136">로그인하고 나면 **구독 선택** 대화 상자에 자격 증명과 연결된 모든 Azure 구독의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="32660-136">After you're signed in, the **Select Subscriptions** dialog box lists all the Azure subscriptions associated with the credentials.</span></span> <span data-ttu-id="32660-137">**선택**을 클릭하여 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="32660-137">Click **Select** to close the dialog box.</span></span>

    ![구독 선택 대화 상자](./media/hdinsight-apache-spark-eclipse-tool-plugin/Select-Subscriptions.png)
5. <span data-ttu-id="32660-139">**Azure 탐색기** 탭에서 **HDInsight**를 확장하여 구독에서 HDInsight Spark 클러스터를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-139">On the **Azure Explorer** tab, expand **HDInsight** to see the HDInsight Spark clusters under your subscription.</span></span>
   
    ![Azure 탐색기의 HDInsight Spark 클러스터](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-3.png)
6. <span data-ttu-id="32660-141">클러스터 이름 노드를 더 확장하여 클러스터와 연결된 리소스(예: 저장소 계정)를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32660-141">You can further expand a cluster name node to see the resources (for example, storage accounts) associated with the cluster.</span></span>
   
    ![클러스터 이름을 확장하여 리소스 표시](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-4.png)



## <a name="set-up-a-spark-scala-project-for-an-hdinsight-spark-cluster"></a><span data-ttu-id="32660-143">HDInsight Spark 클러스터에 Spark Scala 프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="32660-143">Set up a Spark Scala project for an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="32660-144">Eclipse IDE 작업 영역에서 **파일**, **새로 만들기** 및 **프로젝트**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-144">In the Eclipse IDE workspace, click **File**, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="32660-145">새 프로젝트 마법사에서 **HDInsight**를 확장하고 **HDInsight의 Spark(Scala)**를 선택한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-145">In the New Project wizard, expand **HDInsight**, select **Spark on HDInsight (Scala)**, and then click **Next**.</span></span>

    ![HDInsight의 Spark(Scala) 프로젝트 선택](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-2.png)
3. <span data-ttu-id="32660-147">Scala 프로젝트 생성 마법사는 Scala 플러그 인이 설치되어 있는지 여부를 자동으로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-147">The Scala project creation wizard auto detects whether you installed Scala plugin or not.</span></span> <span data-ttu-id="32660-148">클릭 **확인** 다운로드 Scala 플러그 인을 계속 하려면 다음 지침을 따릅니다 Eclipse를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-148">Click **OK** to continue downloading the Scala plugin, then follow the instructions to restart Eclipse.</span></span>

    ![Scala 확인](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala-2.png)
4. <span data-ttu-id="32660-150">**새 HDInsight Scala 프로젝트** 대화 상자에서 다음 값을 입력한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-150">In the **New HDInsight Scala Project** dialog box, provide the following values, and then click **Next**:</span></span>
   * <span data-ttu-id="32660-151">프로젝트의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-151">Enter a name for the project.</span></span>
   * <span data-ttu-id="32660-152">**JRE** 영역에서 **JRE 실행 환경 사용**을 **JavaSE-1.7** 이상으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-152">In the **JRE** area, make sure that **Use an execution environment JRE** is set to **JavaSE-1.7** or later.</span></span>
   * <span data-ttu-id="32660-153">Spark SDK가 SDK를 다운로드한 위치로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-153">Make sure that Spark SDK is set to the location where you downloaded the SDK.</span></span> <span data-ttu-id="32660-154">다운로드 위치에 대한 링크는 이 문서 앞부분의 [필수 구성 요소](#prerequisites) 에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32660-154">The link to the download location is included in the [prerequisites](#prerequisites) earlier in this article.</span></span> <span data-ttu-id="32660-155">대화 상자에 포함된 링크에서 SDK를 다운로드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32660-155">You can also download the SDK from the link included in the dialog box.</span></span>

    ![새 HDInsight Scala 프로젝트 대화 상자](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-3.png)
5.  <span data-ttu-id="32660-157">다음 대화 상자에서 **라이브러리** 탭을 클릭하고 기본값을 유지한 다음 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-157">In the next dialog box, click the **Libraries** tab and keep the defaults, and then click **Finish**.</span></span> 
   
    ![라이브러리 탭](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-4.png)
  
## <a name="create-a-scala-application-for-an-hdinsight-spark-cluster"></a><span data-ttu-id="32660-159">HDInsight Spark 클러스터에 대한 Scala 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="32660-159">Create a Scala application for an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="32660-160">Eclipse IDE의 패키지 탐색기에서 앞서 만든 프로젝트를 확장하고 **src**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **기타**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-160">In the Eclipse IDE, from Package Explorer, expand the project that you created earlier, right-click **src**, point to **New**, and then click **Other**.</span></span>
2. <span data-ttu-id="32660-161">**마법사 선택** 대화 상자에서 **Scala 마법사**를 확장하고 **Scala 개체**, **다음**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-161">In the **Select a wizard** dialog box, expand **Scala Wizards**, click **Scala Object**, and then click **Next**.</span></span>
   
    ![마법사 대화 상자 선택](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-1.png)
3. <span data-ttu-id="32660-163">**새 파일 만들기** 대화 상자에서 개체 이름을 입력한 다음 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-163">In the **Create New File** dialog box, enter a name for the object, and then click **Finish**.</span></span>
   
    ![새 파일 대화 상자 만들기](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-2.png)
4. <span data-ttu-id="32660-165">텍스트 편집기에 다음 코드를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="32660-165">Paste the following code in the text editor:</span></span>
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        object MyClusterApp{
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find the rows that have only one digit in the seventh column in the CSV
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACOut")
          }        
        }
5. <span data-ttu-id="32660-166">HDInsight Spark 클러스터에서 응용 프로그램 실행:</span><span class="sxs-lookup"><span data-stu-id="32660-166">Run the application on an HDInsight Spark cluster:</span></span>
   
   1. <span data-ttu-id="32660-167">패키지 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭한 다음 **HDInsight에 Spark 응용 프로그램 제출**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-167">From Package Explorer, right-click the project name, and then select **Submit Spark Application to HDInsight**.</span></span>        
   2. <span data-ttu-id="32660-168">**Spark 제출** 대화 상자에 다음 값을 제공한 다음 **제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-168">In the **Spark Submission** dialog box, provide the following values, and then click **Submit**:</span></span>
      
      * <span data-ttu-id="32660-169">**클러스터 이름**의 경우 응용 프로그램을 실행하려는 HDInsight Spark 클러스터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-169">For **Cluster Name**, select the HDInsight Spark cluster on which you want to run your application.</span></span>
      * <span data-ttu-id="32660-170">Eclipse 프로젝트에서 아티팩트를 선택하거나 하드 디스크에서 아티팩트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-170">Select an artifact from the Eclipse project, or select one from a hard drive.</span></span> <span data-ttu-id="32660-171">기본값은 패키지 탐색기에서 마우스 오른쪽 단추로 클릭한 항목에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="32660-171">The default value depends on the item you right-click from package explorer.</span></span>
      * <span data-ttu-id="32660-172">**기본 클래스 이름** 드롭다운 목록에서 제출 마법사에는 선택한 프로젝트의 모든 개체 이름이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="32660-172">In the **Main class name** dropdownlist, submission wizard displays all object names from your selected project.</span></span> <span data-ttu-id="32660-173">실행하려는 이름을 선택하거나 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-173">Select or input one that you want to run.</span></span> <span data-ttu-id="32660-174">하드 디스크에서 아티팩트를 선택하는 경우 기본 클래스 이름을 직접 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-174">If you select artifact from hard disk, you need input main class name by yourself.</span></span> 
      * <span data-ttu-id="32660-175">이 예제의 응용 프로그램 코드에는 명령줄 인수가 필요하지 않고 JAR 또는 파일을 참조하지 않으므로 나머지 텍스트 상자를 비워둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32660-175">Because the application code in this example does not require any command-line arguments or reference JARs or files, you can leave the remaining text boxes empty.</span></span>
        
       ![Spark 제출 대화 상자](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-3.png)
   3. <span data-ttu-id="32660-177">**Spark 제출** 탭에 진행 상태가 표시되기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-177">The **Spark Submission** tab should start displaying the progress.</span></span> <span data-ttu-id="32660-178">**Spark 제출** 창에서 빨간색 단추를 클릭하여 응용 프로그램을 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32660-178">You can stop the application by clicking the red button in the **Spark Submission** window.</span></span> <span data-ttu-id="32660-179">구형 아이콘(이미지에 파란색 상자로 표시됨)을 클릭하여 특정 응용 프로그램을 실행하는 로그를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32660-179">You can also view the logs for this specific application run by clicking the globe icon (denoted by the blue box in the image).</span></span>
      
       ![Spark 제출 창](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-4.png)

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-hdinsight-tools-in-azure-toolkit-for-eclipse"></a><span data-ttu-id="32660-181">Eclipse용 Azure 도구 키트의 HDInsight Tools를 사용하여 HDInsight Spark 클러스터 액세스 및 관리</span><span class="sxs-lookup"><span data-stu-id="32660-181">Access and manage HDInsight Spark clusters by using HDInsight Tools in Azure Toolkit for Eclipse</span></span>
<span data-ttu-id="32660-182">HDInsight Tools를 사용하여 작업 출력에 액세스를 포함한 다양한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32660-182">You can perform various operations by using HDInsight Tools, including accessing the job output.</span></span>

### <a name="access-the-job-view"></a><span data-ttu-id="32660-183">작업 보기 액세스</span><span class="sxs-lookup"><span data-stu-id="32660-183">Access the job view</span></span>
1. <span data-ttu-id="32660-184">Azure 탐색기에서 **HDInsight**, Spark 클러스터 이름을 차례로 확장한 다음 **작업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-184">In Azure Explorer, expand **HDInsight**, expand the Spark cluster name, and then click **Jobs**.</span></span> 

    ![작업 보기 노드](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. <span data-ttu-id="32660-186">클릭는 **작업** 노드.</span><span class="sxs-lookup"><span data-stu-id="32660-186">Click on the **Jobs** node.</span></span> <span data-ttu-id="32660-187">HDInsight 도구 자동 검색 여부 (fx) E clipse 플러그 인의 설치 여부.</span><span class="sxs-lookup"><span data-stu-id="32660-187">The HDInsight Tools auto-detects whether you installed the E(fx)clipse plugin or not.</span></span> <span data-ttu-id="32660-188">클릭 **확인** 계속 하려면 Eclipse 마켓플레이스를 설치 하 고 Eclipse를 다시 시작 하는 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="32660-188">Click **OK** to continue and follow the instructions to install the Eclipse Marketplace and restart Eclipse.</span></span>

    ![E(fx)clipse 설치](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-efxclipse.png)

3. <span data-ttu-id="32660-190">**작업** 노드에서 작업 보기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="32660-190">Open the Job View from the **Jobs** node.</span></span> <span data-ttu-id="32660-191">오른쪽 창의 **Spark 작업 보기** 탭에는 클러스터에서 실행된 모든 응용 프로그램이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="32660-191">In the right pane, the **Spark Job View** tab displays all the applications that were run on the cluster.</span></span> <span data-ttu-id="32660-192">자세한 내용을 보려면 원하는 응용 프로그램 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-192">Click the name of the application for which you want to see more details.</span></span>

    ![응용 프로그램 세부 정보](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)
4. <span data-ttu-id="32660-194">작업 그래프에서 마우스 포인터를 기본 실행 중인 작업 정보를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32660-194">If you hover on the job graph, it displays basic running job info.</span></span> <span data-ttu-id="32660-195">작업 그래프 클릭 하면 단계 그래프 및 모든 작업을 생성 하는 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-195">Clicking on the job graph shows the stages graph and info that every job generates.</span></span>

    ![작업 단계 세부 정보](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

5. <span data-ttu-id="32660-197">Stderr 드라이버, 드라이버 Stdout 및 디렉터리 정보를 포함 하는 자주 사용 되는 로그에 나열 됩니다는 **로그** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-197">Frequently used logs, including Driver Stderr, Driver Stdout, and Directory Info, are listed in the **Log** tab.</span></span>

    ![로그 세부 정보](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)
6. <span data-ttu-id="32660-199">창 맨 위에 있는 해당 하이퍼링크를 클릭하여 Spark 기록 UI 및 YARN UI(응용 프로그램 수준)를 열 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32660-199">You can also open the Spark history UI and the YARN UI (at the application level) by clicking the respective hyperlink at the top of the window.</span></span>

### <a name="access-the-storage-container-for-the-cluster"></a><span data-ttu-id="32660-200">클러스터에 대한 저장소 컨테이너 액세스</span><span class="sxs-lookup"><span data-stu-id="32660-200">Access the storage container for the cluster</span></span>
1. <span data-ttu-id="32660-201">Azure 탐색기에서 **HDInsight** 루트 노드를 확장하여 사용할 수 있는 HDInsight Spark 클러스터의 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-201">In Azure Explorer, expand the **HDInsight** root node to see a list of HDInsight Spark clusters that are available.</span></span>
2. <span data-ttu-id="32660-202">클러스터 이름을 확장하여 클러스터에 대한 저장소 계정 및 기본 저장소 컨테이너를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-202">Expand the cluster name to see the storage account and the default storage container for the cluster.</span></span>
   
    ![저장소 계정 및 기본 저장소 컨테이너](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-5.png)
3. <span data-ttu-id="32660-204">클러스터와 연결된 저장소 컨테이너 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-204">Click the storage container name associated with the cluster.</span></span> <span data-ttu-id="32660-205">오른쪽 창에서 **HVACOut** 폴더를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-205">In the right pane, double-click the **HVACOut** folder.</span></span> <span data-ttu-id="32660-206">**파트-** 파일 중 하나를 열어 응용 프로그램의 출력을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-206">Open one of the **part-** files to see the output of the application.</span></span>

### <a name="access-the-spark-history-server"></a><span data-ttu-id="32660-207">Spark 기록 서버 액세스</span><span class="sxs-lookup"><span data-stu-id="32660-207">Access the Spark history server</span></span>
1. <span data-ttu-id="32660-208">Azure 탐색기에서 Spark 클러스터 이름을 마우스 오른쪽 단추로 클릭한 다음 **Spark 기록 UI 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-208">In Azure Explorer, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> <span data-ttu-id="32660-209">메시지가 표시되면 클러스터에 대한 관리자 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-209">When you're prompted, enter the admin credentials for the cluster.</span></span> <span data-ttu-id="32660-210">이러한 항목은 클러스터를 프로비전하는 동안 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-210">You must have specified these while provisioning the cluster.</span></span>
2. <span data-ttu-id="32660-211">Spark 기록 서버 대시보드에서 응용 프로그램 이름을 사용하여 방금 실행을 마친 응용 프로그램을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32660-211">In the Spark history server dashboard, you use the application name to look for the application that you just finished running.</span></span> <span data-ttu-id="32660-212">위의 코드에서 `val conf = new SparkConf().setAppName("MyClusterApp")`을 사용하여 응용 프로그램 이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-212">In the preceding code, you set the application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="32660-213">그러므로 Spark 응용 프로그램의 이름은 **MyClusterApp**입니다.</span><span class="sxs-lookup"><span data-stu-id="32660-213">Hence, your Spark application name was **MyClusterApp**.</span></span>

### <a name="start-the-ambari-portal"></a><span data-ttu-id="32660-214">Ambari 포털 시작</span><span class="sxs-lookup"><span data-stu-id="32660-214">Start the Ambari portal</span></span>
1. <span data-ttu-id="32660-215">Azure 탐색기에서 Spark 클러스터 이름을 마우스 오른쪽 단추로 클릭한 다음 **클러스터 관리 포털(Ambari) 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-215">In Azure Explorer, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 
2. <span data-ttu-id="32660-216">메시지가 표시되면 클러스터에 대한 관리자 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-216">When you're prompted, enter the admin credentials for the cluster.</span></span> <span data-ttu-id="32660-217">이러한 항목은 클러스터를 프로비전하는 동안 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-217">You must have specified these while provisioning the cluster.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="32660-218">Azure 구독 관리</span><span class="sxs-lookup"><span data-stu-id="32660-218">Manage Azure subscriptions</span></span>
<span data-ttu-id="32660-219">기본적으로 Eclipse용 Azure 도구 키트의 HDInsight Tools에는 모든 Azure 구독의 Spark 클러스터가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="32660-219">By default, HDInsight Tools in Azure Toolkit for Eclipse lists the Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="32660-220">필요한 경우 클러스터에 액세스하려는 구독을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32660-220">If necessary, you can specify the subscriptions for which you want to access the cluster.</span></span> 

1. <span data-ttu-id="32660-221">Azure 탐색기에서 **Azure** 루트 노드를 마우스 오른쪽 단추로 클릭한 다음 **구독 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-221">In Azure Explorer, right-click the **Azure** root node, and then click **Manage Subscriptions**.</span></span> 
2. <span data-ttu-id="32660-222">대화 상자에서 액세스하지 않으려는 구독의 확인란 선택을 취소하고 **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-222">In the dialog box, clear the check boxes for the subscription that you don't want to access, and then click **Close**.</span></span> <span data-ttu-id="32660-223">Azure 구독에서 로그아웃하려는 경우 **로그아웃**을 클릭할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32660-223">You can also click **Sign Out** if you want to sign out of your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="32660-224">로컬로 Spark Scala 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="32660-224">Run a Spark Scala application locally</span></span>
<span data-ttu-id="32660-225">Eclipse용 Azure 도구 키트의 HDInsight Tools를 사용하여 워크스테이션에서 Spark Scala 응용 프로그램을 로컬로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32660-225">You can use HDInsight Tools in Azure Toolkit for Eclipse to run Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="32660-226">일반적으로 이러한 응용 프로그램은 저장소 컨테이너와 같은 클러스터 리소스에 액세스할 필요가 없으므로 로컬로 실행하고 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32660-226">Typically, these applications don't need access to cluster resources such as a storage container, and you can run and test them locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="32660-227">필수 요소</span><span class="sxs-lookup"><span data-stu-id="32660-227">Prerequisite</span></span>
<span data-ttu-id="32660-228">Windows 컴퓨터에서 로컬 Spark Scala 응용 프로그램을 실행하는 동안 [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356)에서 설명한 예외가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32660-228">While you're running the local Spark Scala application on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span></span> <span data-ttu-id="32660-229">이 예외는 Windows에 **WinUtils.exe**가 없기 때문에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-229">This exception occurs because **WinUtils.exe** is missing in Windows.</span></span> 

<span data-ttu-id="32660-230">이 오류를 해결하려면 [실행 파일을 다운로드](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe)하여 **C:\WinUtils\bin** 등의 위치에 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-230">To resolve this error, you must [download the executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="32660-231">그런 다음 **HADOOP_HOME** 환경 변수를 추가하고 이 변수 값을 **C\WinUtils**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-231">You must then add the environment variable **HADOOP_HOME** and set the value of the variable to **C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="32660-232">로컬 Spark Scala 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="32660-232">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="32660-233">Eclipse를 시작하고 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="32660-233">Start Eclipse and create a project.</span></span> <span data-ttu-id="32660-234">**새 프로젝트** 대화 상자에서 다음과 같이 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-234">In the **New Project** dialog box, make the following choices, and then click **Next**.</span></span>
   
   * <span data-ttu-id="32660-235">왼쪽 창에서 **HDInsight**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-235">In the left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="32660-236">오른쪽 창에서 **HDInsight의 Spark 로컬 실행 샘플(Scala)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-236">In the right pane, select **Spark on HDInsight Local Run Sample (Scala)**.</span></span>

    ![새 프로젝트 대화 상자](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run.png)
2. <span data-ttu-id="32660-238">프로젝트 세부 정보를 제공하려면 이전의 [HDInsight Spark 클러스터용 Spark Scala 프로젝트 설정](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster) 섹션의 3-6단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="32660-238">To provide the project details, follow steps 3 through 6 from the earlier section [Set up a Spark Scala project for an HDInsight Spark cluster](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster).</span></span>
3. <span data-ttu-id="32660-239">템플릿은 컴퓨터에서 로컬로 실행할 수 있는 샘플 코드(**LogQuery**)를 **src** 폴더 아래에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-239">The template adds a sample code (**LogQuery**) under the **src** folder that you can run locally on your computer.</span></span>
   
    ![LogQuery 위치](./media/hdinsight-apache-spark-eclipse-tool-plugin/local-app.png)
4. <span data-ttu-id="32660-241">**LogQuery** 응용 프로그램을 마우스 오른쪽 단추로 클릭하고 **다음으로 실행**을 가리킨 다음 **1 Scala 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-241">Right-click the **LogQuery** application, point to **Run As**, and then click **1 Scala Application**.</span></span> <span data-ttu-id="32660-242">**콘솔** 탭 아래쪽에 다음과 같은 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="32660-242">You will see an output like this in the **Console** tab at the bottom:</span></span>
   
   ![Spark 응용 프로그램 로컬 실행 결과](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="faq"></a><span data-ttu-id="32660-244">FAQ</span><span class="sxs-lookup"><span data-stu-id="32660-244">FAQ</span></span>
<span data-ttu-id="32660-245">응용 프로그램을 Azure Data Lake Store에 제출하려면 Azure 로그인 프로세스 중에 **대화형** 모드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32660-245">To submit an application to Azure Data Lake Store, choose **Interactive** mode during the Azure sign-in process.</span></span> <span data-ttu-id="32660-246">**자동화된** 모드를 선택하는 경우 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32660-246">If you select **Automated** mode, you can get an error.</span></span>

![interative-signin](./media/hdinsight-apache-spark-eclipse-tool-plugin/interactive-authentication.png)

<span data-ttu-id="32660-248">현재 이 오류는 해결했습니다.</span><span class="sxs-lookup"><span data-stu-id="32660-248">Now, we resolved it.</span></span> <span data-ttu-id="32660-249">임의의 로그인 방법으로 응용 프로그램을 제출하기 위해 Azure Data Lake 클러스터를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32660-249">You can choose an Azure Data Lake Cluster to submit your application with any sign-in method.</span></span>

## <a name="feedback-and-known-issues"></a><span data-ttu-id="32660-250">사용자 의견 및 알려진 문제</span><span class="sxs-lookup"><span data-stu-id="32660-250">Feedback and known issues</span></span>
<span data-ttu-id="32660-251">현재 직접 Spark 출력 보기는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="32660-251">Currently, viewing Spark outputs directly is not supported.</span></span>

<span data-ttu-id="32660-252">제안 또는 피드백이 있거나 이 도구를 사용할 때 문제가 발생하는 경우 hdivstool@microsoft.com으로 메일을 보내 주시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="32660-252">If you have any suggestions or feedback, or if you encounter any problems when using this tool, feel free to send us an email at hdivstool@microsoft.com.</span></span>

## <span data-ttu-id="32660-253"><a name="seealso"></a>참고 항목</span><span class="sxs-lookup"><span data-stu-id="32660-253"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="32660-254">개요: Azure HDInsight에서 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="32660-254">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="32660-255">시나리오</span><span class="sxs-lookup"><span data-stu-id="32660-255">Scenarios</span></span>
* [<span data-ttu-id="32660-256">BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="32660-256">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="32660-257">기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="32660-257">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="32660-258">기계 학습과 Spark: 음식 검사 결과를 예측하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="32660-258">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="32660-259">Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="32660-259">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="32660-260">HDInsight의 Spark를 사용하여 웹 사이트 로그 분석</span><span class="sxs-lookup"><span data-stu-id="32660-260">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="32660-261">응용 프로그램 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="32660-261">Creating and running applications</span></span>
* [<span data-ttu-id="32660-262">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="32660-262">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="32660-263">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="32660-263">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="32660-264">도구 및 확장</span><span class="sxs-lookup"><span data-stu-id="32660-264">Tools and extensions</span></span>
* [<span data-ttu-id="32660-265">IntelliJ용 Azure 도구 키트를 사용하여 Spark Scala 응용 프로그램 만들기 및 제출</span><span class="sxs-lookup"><span data-stu-id="32660-265">Use Azure Toolkit for IntelliJ to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="32660-266">IntelliJ용 Azure 도구 키트를 사용하여 VPN을 통해 원격으로 Spark 응용 프로그램 디버그</span><span class="sxs-lookup"><span data-stu-id="32660-266">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="32660-267">IntelliJ용 Azure 도구 키트를 사용하여 SSH를 통해 원격으로 Spark 응용 프로그램 디버그</span><span class="sxs-lookup"><span data-stu-id="32660-267">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="32660-268">Hortonworks 샌드박스에서 IntelliJ용 HDInsight Tools 사용</span><span class="sxs-lookup"><span data-stu-id="32660-268">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="32660-269">HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용</span><span class="sxs-lookup"><span data-stu-id="32660-269">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="32660-270">HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널</span><span class="sxs-lookup"><span data-stu-id="32660-270">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="32660-271">Jupyter 노트북에서 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="32660-271">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="32660-272">컴퓨터에 Jupyter를 설치하고 HDInsight Spark 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="32660-272">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="32660-273">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="32660-273">Managing resources</span></span>
* [<span data-ttu-id="32660-274">Azure HDInsight에서 Apache Spark 클러스터에 대한 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="32660-274">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="32660-275">HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그</span><span class="sxs-lookup"><span data-stu-id="32660-275">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

