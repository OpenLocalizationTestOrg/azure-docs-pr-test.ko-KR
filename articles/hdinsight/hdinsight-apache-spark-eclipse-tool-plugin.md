---
title: "Toolkit for Eclipse-HDInsight Spark에 대 한 응용 프로그램 만들기 Scala aaaAzure | Microsoft Docs"
description: "Eclipse toodevelop Spark 작성 된 응용 프로그램 Scala에 대 한 Azure 도구 키트의 HDInsight 도구를 사용 하 고 전송할 tooan HDInsight Spark 클러스터에 hello Eclipse IDE에서 직접 있습니다."
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
ms.openlocfilehash: 3ab70857c1e81f591a1c7e29bc1706ec4899ff58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-eclipse-toocreate-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="42937-103">Azure 도구 키트를 사용 하 여 HDInsight 클러스터에 대 한 Eclipse toocreate Spark 응용 프로그램에 대 한</span><span class="sxs-lookup"><span data-stu-id="42937-103">Use Azure Toolkit for Eclipse toocreate Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="42937-104">Toodevelop Eclipse 용 Azure 도구 키트의 HDInsight 도구를 사용 하 여 멤버 Scala 작성 된 응용 프로그램 및 hello Eclipse IDE에서 직접 tooan Azure HDInsight Spark 클러스터에 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-104">Use HDInsight Tools in Azure Toolkit for Eclipse toodevelop Spark applications written in Scala and submit them tooan Azure HDInsight Spark cluster, directly from hello Eclipse IDE.</span></span> <span data-ttu-id="42937-105">Hello HDInsight 도구는 몇 가지 방법에서 플러그 인을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42937-105">You can use hello HDInsight Tools plug-in in a few different ways:</span></span>

* <span data-ttu-id="42937-106">toodevelop HDInsight Spark 클러스터에 있는 Scala Spark 응용 프로그램을 제출 하 고</span><span class="sxs-lookup"><span data-stu-id="42937-106">toodevelop and submit a Scala Spark application on an HDInsight Spark cluster</span></span>
* <span data-ttu-id="42937-107">tooaccess Azure HDInsight Spark 클러스터 리소스</span><span class="sxs-lookup"><span data-stu-id="42937-107">tooaccess your Azure HDInsight Spark cluster resources</span></span>
* <span data-ttu-id="42937-108">toodevelop 및 Scala Spark 응용 프로그램을 로컬로 실행</span><span class="sxs-lookup"><span data-stu-id="42937-108">toodevelop and run a Scala Spark application locally</span></span>

> [!IMPORTANT]
> <span data-ttu-id="42937-109">이 도구 사용된 toocreate를 수 있으며 Linux에서 HDInsight Spark 클러스터는에 대 한 응용 프로그램 제출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42937-109">This tool can be used toocreate and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="42937-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="42937-110">Prerequisites</span></span>

* <span data-ttu-id="42937-111">HDInsight의 Apache Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="42937-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="42937-112">자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="42937-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="42937-113">Oracle Java 개발 키트 버전 8 hello Eclipse IDE 런타임에 사용 되는입니다.</span><span class="sxs-lookup"><span data-stu-id="42937-113">Oracle Java Development Kit version 8, which is used for hello Eclipse IDE runtime.</span></span> <span data-ttu-id="42937-114">Hello에서 다운로드할 수 있습니다 [Oracle 웹 사이트](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-114">You can download it from hello [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="42937-115">Eclipse IDE.</span><span class="sxs-lookup"><span data-stu-id="42937-115">Eclipse IDE.</span></span> <span data-ttu-id="42937-116">이 문서에서는 Eclipse Neon을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-116">This article uses Eclipse Neon.</span></span> <span data-ttu-id="42937-117">Hello에서 설치할 수 있습니다 [Eclipse 웹 사이트](https://www.eclipse.org/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-117">You can install it from hello [Eclipse website](https://www.eclipse.org/downloads/).</span></span>   
* <span data-ttu-id="42937-118">Spark SDK.</span><span class="sxs-lookup"><span data-stu-id="42937-118">Spark SDK.</span></span> <span data-ttu-id="42937-119">[GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42937-119">You can download it from [GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).</span></span>


## <a name="install-hdinsight-tools-in-azure-toolkit-for-eclipse-and-scala-plugin"></a><span data-ttu-id="42937-120">Azure 도구 키트에 Eclipse 및 Scala 플러그 인에 대 한 HDInsight 도구를 설치</span><span class="sxs-lookup"><span data-stu-id="42937-120">Install HDInsight Tools in Azure Toolkit for Eclipse and Scala Plugin</span></span>
### <a name="install-hdinsight-tools"></a><span data-ttu-id="42937-121">HDInsight Tools 설치</span><span class="sxs-lookup"><span data-stu-id="42937-121">Install HDInsight Tools</span></span>
<span data-ttu-id="42937-122">Eclipse용 HDInsight Tools는 Eclipse용 Azure 도구 키트의 일부분으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="42937-122">HDInsight Tools for Eclipse is available as part of Azure Toolkit for Eclipse.</span></span> <span data-ttu-id="42937-123">설치 지침은 [Eclipse용 Azure 도구 키트 설치](../azure-toolkit-for-eclipse-installation.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="42937-123">For installation instructions, see [Installing Azure Toolkit for Eclipse](../azure-toolkit-for-eclipse-installation.md).</span></span>
### <a name="install-scala-plugin"></a><span data-ttu-id="42937-124">Scala 플러그 인 설치</span><span class="sxs-lookup"><span data-stu-id="42937-124">Install Scala Plugin</span></span>
<span data-ttu-id="42937-125">Intellij hello를 열 때 hello HDInsight 도구 자동 여부 Scala 플러그 인 설치 되어 있는지 여부를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-125">When you open hello Intellij, hello HDInsight Tools auto detects whether you installed Scala plugin or not.</span></span> <span data-ttu-id="42937-126">클릭 **확인** hello Eclipse 마켓플레이스 하 여 hello 지침 tooinstall toocontinue 및 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-126">Click **OK** toocontinue and follow hello instructions tooinstall by hello Eclipse Marketplace.</span></span>

 ![자동 설치 Scala 플러그 인](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala.png)

## <a name="sign-in-tooyour-azure-subscription"></a><span data-ttu-id="42937-128">Azure 구독 tooyour에 로그인</span><span class="sxs-lookup"><span data-stu-id="42937-128">Sign in tooyour Azure subscription</span></span>
1. <span data-ttu-id="42937-129">Hello Eclipse IDE를 시작 하 고 Azure 탐색기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="42937-129">Start hello Eclipse IDE and open Azure Explorer.</span></span> <span data-ttu-id="42937-130">Hello에 **창** 메뉴를 클릭 하 여 **보기 표시**, 클릭 하 고 **다른**합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-130">On hello **Window** menu, click **Show View**, and then click **Other**.</span></span> <span data-ttu-id="42937-131">Hello 대화 상자가 열리면 확장 **Azure**, 클릭 **Azure 탐색기**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-131">In hello dialog box that opens, expand **Azure**, click **Azure Explorer**, and then click **OK**.</span></span>

    ![보기 표시 대화 상자](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-1.png)
2. <span data-ttu-id="42937-133">마우스 오른쪽 단추로 클릭 hello **Azure** 노드를 차례로 클릭 한 다음 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-133">Right-click hello **Azure** node, and then click **Sign in**.</span></span>
3. <span data-ttu-id="42937-134">Hello에 **Azure 로그인** 대화 상자 hello 인증 방법을 선택 하 고 클릭 **로그인**, Azure 자격 증명을 입력 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42937-134">In hello **Azure Sign In** dialog box, choose hello authentication method, click **Sign in**, and enter your Azure credentials.</span></span>
   
    ![Azure 로그인 대화 상자](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-2.png)
4. <span data-ttu-id="42937-136">로그인, 후 hello **구독 선택** hello 자격 증명으로 연결 된 Azure 구독을 hello 모든 대화 상자 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="42937-136">After you're signed in, hello **Select Subscriptions** dialog box lists all hello Azure subscriptions associated with hello credentials.</span></span> <span data-ttu-id="42937-137">클릭 **선택** tooclose hello 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="42937-137">Click **Select** tooclose hello dialog box.</span></span>

    ![구독 선택 대화 상자](./media/hdinsight-apache-spark-eclipse-tool-plugin/Select-Subscriptions.png)
5. <span data-ttu-id="42937-139">Hello에 **Azure 탐색기** 탭을 확장 하 고 **HDInsight** 구독에서 HDInsight Spark 클러스터 toosee hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-139">On hello **Azure Explorer** tab, expand **HDInsight** toosee hello HDInsight Spark clusters under your subscription.</span></span>
   
    ![Azure 탐색기의 HDInsight Spark 클러스터](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-3.png)
6. <span data-ttu-id="42937-141">클러스터 이름 노드 toosee hello 리소스 (예를 들어 저장소 계정) hello 클러스터와 연결 된 추가로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42937-141">You can further expand a cluster name node toosee hello resources (for example, storage accounts) associated with hello cluster.</span></span>
   
    ![클러스터 이름 toosee 리소스를 확장합니다.](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-4.png)



## <a name="set-up-a-spark-scala-project-for-an-hdinsight-spark-cluster"></a><span data-ttu-id="42937-143">HDInsight Spark 클러스터에 Spark Scala 프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="42937-143">Set up a Spark Scala project for an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="42937-144">Hello Eclipse IDE 작업 영역에서 클릭 **파일**, 클릭 **새로**, 클릭 하 고 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-144">In hello Eclipse IDE workspace, click **File**, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="42937-145">Hello 새 프로젝트 마법사에서 확장 **HDInsight**선택, **(Scala) HDInsight의 Spark**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-145">In hello New Project wizard, expand **HDInsight**, select **Spark on HDInsight (Scala)**, and then click **Next**.</span></span>

    ![HDInsight (Scala) 프로젝트에서 Spark hello를 선택합니다.](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-2.png)
3. <span data-ttu-id="42937-147">hello Scala 프로젝트 만들기 마법사 자동 여부 Scala 플러그 인 설치 되어 있는지 여부를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-147">hello Scala project creation wizard auto detects whether you installed Scala plugin or not.</span></span> <span data-ttu-id="42937-148">클릭 **확인** toocontinue hello Scala 플러그 인을 다음에 따라 hello 지침 toorestart Eclipse 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-148">Click **OK** toocontinue downloading hello Scala plugin, then follow hello instructions toorestart Eclipse.</span></span>

    ![Scala 확인](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala-2.png)
4. <span data-ttu-id="42937-150">Hello에 **새 HDInsight Scala 프로젝트** 대화 상자에서 다음 값을 hello를 입력 한 다음 **다음**:</span><span class="sxs-lookup"><span data-stu-id="42937-150">In hello **New HDInsight Scala Project** dialog box, provide hello following values, and then click **Next**:</span></span>
   * <span data-ttu-id="42937-151">Hello 프로젝트에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-151">Enter a name for hello project.</span></span>
   * <span data-ttu-id="42937-152">Hello에 **JRE** 영역에서 다음 사항을 확인 **JRE 실행 환경을 사용 하 여** 너무 설정 되어**JavaSE 1.7** 이상.</span><span class="sxs-lookup"><span data-stu-id="42937-152">In hello **JRE** area, make sure that **Use an execution environment JRE** is set too**JavaSE-1.7** or later.</span></span>
   * <span data-ttu-id="42937-153">Spark SDK hello SDK 다운로드 toohello 위치 설정 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-153">Make sure that Spark SDK is set toohello location where you downloaded hello SDK.</span></span> <span data-ttu-id="42937-154">hello 링크 toohello 다운로드 위치에에서 연결 되어 hello [필수 구성 요소](#prerequisites) 이 문서의 앞부분에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42937-154">hello link toohello download location is included in hello [prerequisites](#prerequisites) earlier in this article.</span></span> <span data-ttu-id="42937-155">Hello에서 hello SDK를 다운로드할 수도 hello 대화 상자에 포함 된 링크.</span><span class="sxs-lookup"><span data-stu-id="42937-155">You can also download hello SDK from hello link included in hello dialog box.</span></span>

    ![새 HDInsight Scala 프로젝트 대화 상자](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-3.png)
5.  <span data-ttu-id="42937-157">Hello 다음 대화 상자에서 클릭 hello **라이브러리** 탭 하 고 hello 기본값을 유지 한 다음 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-157">In hello next dialog box, click hello **Libraries** tab and keep hello defaults, and then click **Finish**.</span></span> 
   
    ![라이브러리 탭](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-4.png)
  
## <a name="create-a-scala-application-for-an-hdinsight-spark-cluster"></a><span data-ttu-id="42937-159">HDInsight Spark 클러스터에 대한 Scala 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="42937-159">Create a Scala application for an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="42937-160">Hello 패키지 탐색기에서 Eclipse IDE에서에서 이전에 만든 hello 프로젝트를 마우스 오른쪽 단추로 클릭 **src**, 너무 가리킨**새로**, 클릭 하 고 **다른**합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-160">In hello Eclipse IDE, from Package Explorer, expand hello project that you created earlier, right-click **src**, point too**New**, and then click **Other**.</span></span>
2. <span data-ttu-id="42937-161">Hello에 **마법사 선택** 대화 상자에서 **Scala 마법사**, 클릭 **Scala 개체**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-161">In hello **Select a wizard** dialog box, expand **Scala Wizards**, click **Scala Object**, and then click **Next**.</span></span>
   
    ![마법사 대화 상자 선택](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-1.png)
3. <span data-ttu-id="42937-163">Hello에 **새 파일 만들기** hello 개체에 대 한 이름을 입력 하 고 클릭 하는 대화 상자, **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-163">In hello **Create New File** dialog box, enter a name for hello object, and then click **Finish**.</span></span>
   
    ![새 파일 대화 상자 만들기](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-2.png)
4. <span data-ttu-id="42937-165">Hello를 hello 텍스트 편집기에서 코드 다음에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="42937-165">Paste hello following code in hello text editor:</span></span>
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        object MyClusterApp{
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows that have only one digit in hello seventh column in hello CSV
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACOut")
          }        
        }
5. <span data-ttu-id="42937-166">HDInsight Spark 클러스터에서 hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-166">Run hello application on an HDInsight Spark cluster:</span></span>
   
   1. <span data-ttu-id="42937-167">패키지 탐색기에서 hello 프로젝트 이름을 마우스 오른쪽 단추로 클릭 한 다음 선택 **Spark 응용 프로그램 제출 tooHDInsight**합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-167">From Package Explorer, right-click hello project name, and then select **Submit Spark Application tooHDInsight**.</span></span>        
   2. <span data-ttu-id="42937-168">Hello에 **Spark 제출** 대화 상자에서 다음 값을 hello를 입력 한 다음 **전송**:</span><span class="sxs-lookup"><span data-stu-id="42937-168">In hello **Spark Submission** dialog box, provide hello following values, and then click **Submit**:</span></span>
      
      * <span data-ttu-id="42937-169">에 대 한 **클러스터 이름**, 선택 hello toorun 원하는 HDInsight Spark 클러스터 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="42937-169">For **Cluster Name**, select hello HDInsight Spark cluster on which you want toorun your application.</span></span>
      * <span data-ttu-id="42937-170">Hello Eclipse 프로젝트에서 아티팩트를 선택 하거나 하드 드라이브에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-170">Select an artifact from hello Eclipse project, or select one from a hard drive.</span></span> <span data-ttu-id="42937-171">hello 기본값 패키지 탐색기에서 마우스 오른쪽 단추로 클릭 하는 hello 항목에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="42937-171">hello default value depends on hello item you right-click from package explorer.</span></span>
      * <span data-ttu-id="42937-172">Hello에 **Main 클래스 이름** dropdownlist, 제출 마법사에는 선택한 프로젝트에서 모든 개체 이름이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42937-172">In hello **Main class name** dropdownlist, submission wizard displays all object names from your selected project.</span></span> <span data-ttu-id="42937-173">선택 하거나 하나를 입력 toorun 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-173">Select or input one that you want toorun.</span></span> <span data-ttu-id="42937-174">하드 디스크에서 아티팩트를 선택하는 경우 기본 클래스 이름을 직접 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-174">If you select artifact from hard disk, you need input main class name by yourself.</span></span> 
      * <span data-ttu-id="42937-175">이 예에서 응용 프로그램 코드 hello 어떤 명령줄 인수도 필요 하지 않거나 Jar 또는 파일 참조를 때문에 남아 있는 빈 입력란 hello를 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42937-175">Because hello application code in this example does not require any command-line arguments or reference JARs or files, you can leave hello remaining text boxes empty.</span></span>
        
       ![Spark 제출 대화 상자](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-3.png)
   3. <span data-ttu-id="42937-177">hello **Spark 제출** 탭 hello 진행률을 표시 하기 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-177">hello **Spark Submission** tab should start displaying hello progress.</span></span> <span data-ttu-id="42937-178">Hello hello 빨간색 단추를 클릭 하 여 hello 응용 프로그램을 중지할 수 있습니다 **Spark 제출** 창.</span><span class="sxs-lookup"><span data-stu-id="42937-178">You can stop hello application by clicking hello red button in hello **Spark Submission** window.</span></span> <span data-ttu-id="42937-179">Hello 지구 아이콘 (hello 이미지의 hello 파란색 상자로 표시 됨)를 클릭 하 여 실행이 특정 응용 프로그램에 대 한 hello 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42937-179">You can also view hello logs for this specific application run by clicking hello globe icon (denoted by hello blue box in hello image).</span></span>
      
       ![Spark 제출 창](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-4.png)

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-hdinsight-tools-in-azure-toolkit-for-eclipse"></a><span data-ttu-id="42937-181">Eclipse용 Azure 도구 키트의 HDInsight Tools를 사용하여 HDInsight Spark 클러스터 액세스 및 관리</span><span class="sxs-lookup"><span data-stu-id="42937-181">Access and manage HDInsight Spark clusters by using HDInsight Tools in Azure Toolkit for Eclipse</span></span>
<span data-ttu-id="42937-182">Hello 작업 출력을 액세스를 포함 하는 HDInsight 도구를 사용 하 여 다양 한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42937-182">You can perform various operations by using HDInsight Tools, including accessing hello job output.</span></span>

### <a name="access-hello-job-view"></a><span data-ttu-id="42937-183">액세스 hello 작업 보기</span><span class="sxs-lookup"><span data-stu-id="42937-183">Access hello job view</span></span>
1. <span data-ttu-id="42937-184">Azure 탐색기에서 확장 **HDInsight**hello Spark 클러스터 이름을 확장 하 고 클릭 **작업**합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-184">In Azure Explorer, expand **HDInsight**, expand hello Spark cluster name, and then click **Jobs**.</span></span> 

    ![작업 보기 노드](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. <span data-ttu-id="42937-186">Hello 클릭 **작업** 노드.</span><span class="sxs-lookup"><span data-stu-id="42937-186">Click on hello **Jobs** node.</span></span> <span data-ttu-id="42937-187">hello HDInsight 도구 자동 검색 여부 hello E (fx) clipse 플러그 인을 설치 여부.</span><span class="sxs-lookup"><span data-stu-id="42937-187">hello HDInsight Tools auto-detects whether you installed hello E(fx)clipse plugin or not.</span></span> <span data-ttu-id="42937-188">클릭 **확인** toocontinue 및 따라 hello 지침은 tooinstall Eclipse 마켓플레이스 hello 및 Eclipse를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-188">Click **OK** toocontinue and follow hello instructions tooinstall hello Eclipse Marketplace and restart Eclipse.</span></span>

    ![E(fx)clipse 설치](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-efxclipse.png)

3. <span data-ttu-id="42937-190">Hello에서 열기 hello 작업 보기 **작업** 노드.</span><span class="sxs-lookup"><span data-stu-id="42937-190">Open hello Job View from hello **Jobs** node.</span></span> <span data-ttu-id="42937-191">Hello 오른쪽 창에서 hello **Spark 작업 보기** hello 클러스터에서 실행 된 모든 hello 응용 프로그램 탭에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42937-191">In hello right pane, hello **Spark Job View** tab displays all hello applications that were run on hello cluster.</span></span> <span data-ttu-id="42937-192">Hello을 구하려는 toosee 자세히 hello 응용 프로그램 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-192">Click hello name of hello application for which you want toosee more details.</span></span>

    ![응용 프로그램 세부 정보](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)
4. <span data-ttu-id="42937-194">Hello 작업 그래프에서 마우스 포인터를 기본 실행 중인 작업 정보를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42937-194">If you hover on hello job graph, it displays basic running job info.</span></span> <span data-ttu-id="42937-195">Hello 작업 그래프 클릭 하면 hello 단계 그래프 및 모든 작업을 생성 하는 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-195">Clicking on hello job graph shows hello stages graph and info that every job generates.</span></span>

    ![작업 단계 세부 정보](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

5. <span data-ttu-id="42937-197">Stderr 드라이버, 드라이버 Stdout 및 디렉터리 정보를 포함 하는 자주 사용 되는 로그가 hello에 나열 됩니다 **로그** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-197">Frequently used logs, including Driver Stderr, Driver Stdout, and Directory Info, are listed in hello **Log** tab.</span></span>

    ![로그 세부 정보](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)
6. <span data-ttu-id="42937-199">Hello 창의 위쪽에 hello hello 해당 하이퍼링크를 클릭 하 여 hello Spark 기록 UI 및 hello hello 응용 프로그램 수준에서 YARN UI를 열 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42937-199">You can also open hello Spark history UI and hello YARN UI (at hello application level) by clicking hello respective hyperlink at hello top of hello window.</span></span>

### <a name="access-hello-storage-container-for-hello-cluster"></a><span data-ttu-id="42937-200">Hello 클러스터에 대 한 액세스 hello 저장소 컨테이너</span><span class="sxs-lookup"><span data-stu-id="42937-200">Access hello storage container for hello cluster</span></span>
1. <span data-ttu-id="42937-201">Azure 탐색기에서 확장 hello **HDInsight** 루트 노드 toosee HDInsight Spark 클러스터에 사용할 수 있는 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="42937-201">In Azure Explorer, expand hello **HDInsight** root node toosee a list of HDInsight Spark clusters that are available.</span></span>
2. <span data-ttu-id="42937-202">Hello 클러스터 이름 toosee hello 저장소 계정 및 hello 클러스터에 대 한 hello 기본 저장소 컨테이너를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-202">Expand hello cluster name toosee hello storage account and hello default storage container for hello cluster.</span></span>
   
    ![저장소 계정 및 기본 저장소 컨테이너](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-5.png)
3. <span data-ttu-id="42937-204">Hello 클러스터와 연결 된 hello 저장소 컨테이너 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-204">Click hello storage container name associated with hello cluster.</span></span> <span data-ttu-id="42937-205">Hello 오른쪽 창에서 hello를 두 번 클릭 **HVACOut** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="42937-205">In hello right pane, double-click hello **HVACOut** folder.</span></span> <span data-ttu-id="42937-206">Hello 중 하나를 열려면 **파트-** hello 응용 프로그램의 toosee hello 출력 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="42937-206">Open one of hello **part-** files toosee hello output of hello application.</span></span>

### <a name="access-hello-spark-history-server"></a><span data-ttu-id="42937-207">Hello Spark 기록 서버에 액세스</span><span class="sxs-lookup"><span data-stu-id="42937-207">Access hello Spark history server</span></span>
1. <span data-ttu-id="42937-208">Azure 탐색기에서 Spark 클러스터 이름을 마우스 오른쪽 단추로 클릭한 다음 **Spark 기록 UI 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-208">In Azure Explorer, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> <span data-ttu-id="42937-209">메시지가 나타나면 hello 클러스터에 대 한 hello 관리자 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-209">When you're prompted, enter hello admin credentials for hello cluster.</span></span> <span data-ttu-id="42937-210">지정 해야 hello 클러스터를 프로 비전 할 때 이러한 합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-210">You must have specified these while provisioning hello cluster.</span></span>
2. <span data-ttu-id="42937-211">Hello Spark 기록 서버 대시보드 hello 응용 프로그램 실행이 방금 완료에 대 한 응용 프로그램 이름 toolook hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-211">In hello Spark history server dashboard, you use hello application name toolook for hello application that you just finished running.</span></span> <span data-ttu-id="42937-212">Hello 앞에 코드를 사용 하 여 hello 응용 프로그램 이름을 설정 `val conf = new SparkConf().setAppName("MyClusterApp")`합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-212">In hello preceding code, you set hello application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="42937-213">그러므로 Spark 응용 프로그램의 이름은 **MyClusterApp**입니다.</span><span class="sxs-lookup"><span data-stu-id="42937-213">Hence, your Spark application name was **MyClusterApp**.</span></span>

### <a name="start-hello-ambari-portal"></a><span data-ttu-id="42937-214">Hello Ambari 포털 시작</span><span class="sxs-lookup"><span data-stu-id="42937-214">Start hello Ambari portal</span></span>
1. <span data-ttu-id="42937-215">Azure 탐색기에서 Spark 클러스터 이름을 마우스 오른쪽 단추로 클릭한 다음 **클러스터 관리 포털(Ambari) 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-215">In Azure Explorer, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 
2. <span data-ttu-id="42937-216">메시지가 나타나면 hello 클러스터에 대 한 hello 관리자 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-216">When you're prompted, enter hello admin credentials for hello cluster.</span></span> <span data-ttu-id="42937-217">지정 해야 hello 클러스터를 프로 비전 할 때 이러한 합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-217">You must have specified these while provisioning hello cluster.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="42937-218">Azure 구독 관리</span><span class="sxs-lookup"><span data-stu-id="42937-218">Manage Azure subscriptions</span></span>
<span data-ttu-id="42937-219">Eclipse 용 Azure 도구 키트의 HDInsight 도구 기본적으로 모든 Azure 구독에서 hello Spark 클러스터를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-219">By default, HDInsight Tools in Azure Toolkit for Eclipse lists hello Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="42937-220">필요한 경우 tooaccess hello 클러스터 원하는 hello 구독을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42937-220">If necessary, you can specify hello subscriptions for which you want tooaccess hello cluster.</span></span> 

1. <span data-ttu-id="42937-221">Azure 탐색기에서 마우스 오른쪽 단추로 클릭 hello **Azure** 루트 노드를 찾은 다음 클릭 **구독 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-221">In Azure Explorer, right-click hello **Azure** root node, and then click **Manage Subscriptions**.</span></span> 
2. <span data-ttu-id="42937-222">Hello 대화 상자에서 tooaccess, 원하는 및 클릭 하지 않는 hello 구독에 대 한 hello 확인란의 선택을 취소 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-222">In hello dialog box, clear hello check boxes for hello subscription that you don't want tooaccess, and then click **Close**.</span></span> <span data-ttu-id="42937-223">클릭할 수도 있습니다 **로그 아웃** toosign Azure 구독에서 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="42937-223">You can also click **Sign Out** if you want toosign out of your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="42937-224">로컬로 Spark Scala 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="42937-224">Run a Spark Scala application locally</span></span>
<span data-ttu-id="42937-225">사용할 수 있습니다 HDInsight 도구 Azure 도구 키트에 Eclipse toorun Spark Scala 응용 프로그램에 대 한 로컬 워크스테이션에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-225">You can use HDInsight Tools in Azure Toolkit for Eclipse toorun Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="42937-226">일반적으로 이러한 응용 프로그램 저장소 컨테이너와 같은 toocluster 리소스에 액세스 하지 않아도 하 고 실행 하 고 로컬로 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42937-226">Typically, these applications don't need access toocluster resources such as a storage container, and you can run and test them locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="42937-227">필수 요소</span><span class="sxs-lookup"><span data-stu-id="42937-227">Prerequisite</span></span>
<span data-ttu-id="42937-228">에 설명 된 대로 예외가 발생할 수 hello 로컬 Spark Scala 응용 프로그램을 Windows 컴퓨터에서 실행 하는 동안 [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356)합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-228">While you're running hello local Spark Scala application on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span></span> <span data-ttu-id="42937-229">이 예외는 Windows에 **WinUtils.exe**가 없기 때문에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-229">This exception occurs because **WinUtils.exe** is missing in Windows.</span></span> 

<span data-ttu-id="42937-230">tooresolve 해야이 오류를 [hello 실행 파일을 다운로드](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa 위치 **C:\WinUtils\bin**합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-230">tooresolve this error, you must [download hello executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="42937-231">그런 다음 hello 환경 변수를 추가 해야 **HADOOP_HOME** 너무 hello hello 변수 값을 설정 하 고**C\WinUtils**합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-231">You must then add hello environment variable **HADOOP_HOME** and set hello value of hello variable too**C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="42937-232">로컬 Spark Scala 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="42937-232">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="42937-233">Eclipse를 시작하고 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="42937-233">Start Eclipse and create a project.</span></span> <span data-ttu-id="42937-234">Hello에 **새 프로젝트** 대화 상자, hello 선택 옵션을 다음을 확인 한 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-234">In hello **New Project** dialog box, make hello following choices, and then click **Next**.</span></span>
   
   * <span data-ttu-id="42937-235">Hello 왼쪽된 창에서 선택 **HDInsight**합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-235">In hello left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="42937-236">Hello 오른쪽 창에서 선택 **HDInsight의 로컬 실행 되는 샘플 (Scala)의 Spark**합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-236">In hello right pane, select **Spark on HDInsight Local Run Sample (Scala)**.</span></span>

    ![새 프로젝트 대화 상자](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run.png)
2. <span data-ttu-id="42937-238">tooprovide hello 프로젝트 세부 정보를 작업 단계 3-6에서 이전 섹션 hello [HDInsight Spark 클러스터에 대 한 Spark Scala 프로젝트 설정](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster)합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-238">tooprovide hello project details, follow steps 3 through 6 from hello earlier section [Set up a Spark Scala project for an HDInsight Spark cluster](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster).</span></span>
3. <span data-ttu-id="42937-239">샘플 코드를 추가 하는 hello 템플릿 (**LogQuery**) hello에서 **src** 폴더를 컴퓨터에 로컬로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42937-239">hello template adds a sample code (**LogQuery**) under hello **src** folder that you can run locally on your computer.</span></span>
   
    ![LogQuery 위치](./media/hdinsight-apache-spark-eclipse-tool-plugin/local-app.png)
4. <span data-ttu-id="42937-241">마우스 오른쪽 단추로 클릭 hello **LogQuery** 응용 프로그램을 너무 가리킨**계정으로 실행**, 클릭 하 고 **Scala 응용 프로그램 1**합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-241">Right-click hello **LogQuery** application, point too**Run As**, and then click **1 Scala Application**.</span></span> <span data-ttu-id="42937-242">Hello에서 다음과 같은 출력을 보게 **콘솔** hello 아래쪽에 탭:</span><span class="sxs-lookup"><span data-stu-id="42937-242">You will see an output like this in hello **Console** tab at hello bottom:</span></span>
   
   ![Spark 응용 프로그램 로컬 실행 결과](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="faq"></a><span data-ttu-id="42937-244">FAQ</span><span class="sxs-lookup"><span data-stu-id="42937-244">FAQ</span></span>
<span data-ttu-id="42937-245">응용 프로그램 tooAzure 데이터 레이크 저장소 toosubmit 선택 **Interactive'** hello Azure 로그인 프로세스 중 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="42937-245">toosubmit an application tooAzure Data Lake Store, choose **Interactive** mode during hello Azure sign-in process.</span></span> <span data-ttu-id="42937-246">**자동화된** 모드를 선택하는 경우 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42937-246">If you select **Automated** mode, you can get an error.</span></span>

![interative-signin](./media/hdinsight-apache-spark-eclipse-tool-plugin/interactive-authentication.png)

<span data-ttu-id="42937-248">현재 이 오류는 해결했습니다.</span><span class="sxs-lookup"><span data-stu-id="42937-248">Now, we resolved it.</span></span> <span data-ttu-id="42937-249">어떤 로그인 방법으로 Azure 데이터 레이크 클러스터 toosubmit 응용 프로그램을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42937-249">You can choose an Azure Data Lake Cluster toosubmit your application with any sign-in method.</span></span>

## <a name="feedback-and-known-issues"></a><span data-ttu-id="42937-250">사용자 의견 및 알려진 문제</span><span class="sxs-lookup"><span data-stu-id="42937-250">Feedback and known issues</span></span>
<span data-ttu-id="42937-251">현재 직접 Spark 출력 보기는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="42937-251">Currently, viewing Spark outputs directly is not supported.</span></span>

<span data-ttu-id="42937-252">모든 제안이 나 의견이, 또는이 도구를 사용할 때 문제가 발생 하는 경우 느껴집니다 무료 toosend us에 전자 메일 hdivstool@microsoft.com합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-252">If you have any suggestions or feedback, or if you encounter any problems when using this tool, feel free toosend us an email at hdivstool@microsoft.com.</span></span>

## <span data-ttu-id="42937-253"><a name="seealso"></a>참고 항목</span><span class="sxs-lookup"><span data-stu-id="42937-253"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="42937-254">개요: Azure HDInsight에서 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="42937-254">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="42937-255">시나리오</span><span class="sxs-lookup"><span data-stu-id="42937-255">Scenarios</span></span>
* [<span data-ttu-id="42937-256">BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="42937-256">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="42937-257">기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="42937-257">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="42937-258">Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark</span><span class="sxs-lookup"><span data-stu-id="42937-258">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="42937-259">Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="42937-259">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="42937-260">HDInsight의 Spark를 사용하여 웹 사이트 로그 분석</span><span class="sxs-lookup"><span data-stu-id="42937-260">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="42937-261">응용 프로그램 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="42937-261">Creating and running applications</span></span>
* [<span data-ttu-id="42937-262">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="42937-262">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="42937-263">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="42937-263">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="42937-264">도구 및 확장</span><span class="sxs-lookup"><span data-stu-id="42937-264">Tools and extensions</span></span>
* [<span data-ttu-id="42937-265">IntelliJ toocreate에 대 한 Azure 도구 키트를 사용 하 고 스파크 Scala 응용 프로그램 제출</span><span class="sxs-lookup"><span data-stu-id="42937-265">Use Azure Toolkit for IntelliJ toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="42937-266">Azure 도구 키트를 사용 하 여 VPN 통해 원격으로 IntelliJ toodebug Spark 응용 프로그램에 대 한</span><span class="sxs-lookup"><span data-stu-id="42937-266">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="42937-267">SSH 통해 원격으로 IntelliJ toodebug Spark 응용 프로그램에 대 한 Azure 도구 키트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-267">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="42937-268">Hortonworks 샌드박스에서 IntelliJ용 HDInsight Tools 사용</span><span class="sxs-lookup"><span data-stu-id="42937-268">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="42937-269">HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용</span><span class="sxs-lookup"><span data-stu-id="42937-269">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="42937-270">HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널</span><span class="sxs-lookup"><span data-stu-id="42937-270">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="42937-271">Jupyter 노트북에서 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="42937-271">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="42937-272">Jupyter 사용자 컴퓨터에 설치 하 고 tooan HDInsight Spark 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-272">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="42937-273">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="42937-273">Managing resources</span></span>
* [<span data-ttu-id="42937-274">Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="42937-274">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="42937-275">HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그</span><span class="sxs-lookup"><span data-stu-id="42937-275">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

