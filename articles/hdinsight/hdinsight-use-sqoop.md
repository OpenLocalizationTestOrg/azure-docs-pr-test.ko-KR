---
title: "Azure HDInsight(Hadoop)를 사용하여 Apache Sqoop 작업 실행 | Microsoft Docs"
description: "워크스테이션에서 Azure PowerShell을 사용하여 Hadoop 클러스터와 Azure SQL 데이터베이스 간에 Sqoop 가져오기 및 내보내기를 실행하는 방법에 대해 알아봅니다."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 2fdcc6b7-6ad5-4397-a30b-e7e389b66c7a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 8e77153493b6f37f5f48116b86bad6b25a50d1a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-sqoop-with-hadoop-in-hdinsight"></a><span data-ttu-id="36b43-103">HDInsight에서 Hadoop과 Sqoop 사용</span><span class="sxs-lookup"><span data-stu-id="36b43-103">Use Sqoop with Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="36b43-104">HDInsight에서 Sqoop을 사용하여 HDInsight 클러스터와 Azure SQL 데이터베이스 또는 SQL Server 데이터베이스 사이에서 가져오기 및 내보내는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-104">Learn how to use Sqoop in HDInsight to import and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

<span data-ttu-id="36b43-105">비구조적 및 반구조적 데이터(예: 로그 및 파일)를 처리하기 위해 당연히 Hadoop을 선택하지만 관계형 데이터베이스에 저장된 구조적 데이터를 처리해야 할 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-105">Although Hadoop is a natural choice for processing unstructured and semistructured data, such as logs and files, there may also be a need to process structured data that is stored in relational databases.</span></span>

<span data-ttu-id="36b43-106">[Sqoop][sqoop-user-guide-1.4.4]은 Hadoop 클러스터와 관계형 데이터베이스 간 데이터 전송을 위해 설계된 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-106">[Sqoop][sqoop-user-guide-1.4.4] is a tool designed to transfer data between Hadoop clusters and relational databases.</span></span> <span data-ttu-id="36b43-107">이 도구를 사용하면 SQL Server, MySQL, Oracle 등의 RDBMS(관계형 데이터베이스 관리 시스템)에서 HDFS(Hadoop Distributed File System)로 데이터를 가져오고, MapReduce 또는 Hive로 Hadoop의 데이터를 변환한 후 데이터를 RDBMS로 다시 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-107">You can use it to import data from a relational database management system (RDBMS) such as SQL Server, MySQL, or Oracle into the Hadoop distributed file system (HDFS), transform the data in Hadoop with MapReduce or Hive, and then export the data back into an RDBMS.</span></span> <span data-ttu-id="36b43-108">이 자습서에서는 관계형 데이터베이스에 SQL Server 데이터베이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-108">In this tutorial, you are using a SQL Server database for your relational database.</span></span>

<span data-ttu-id="36b43-109">HDInsight 클러스터에서 지원되는 Sqoop 버전을 보려면 [HDInsight에서 제공하는 클러스터 버전의 새로운 기능][hdinsight-versions]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36b43-109">For Sqoop versions that are supported on HDInsight clusters, see [What's new in the cluster versions provided by HDInsight?][hdinsight-versions]</span></span>

## <a name="understand-the-scenario"></a><span data-ttu-id="36b43-110">시나리오 이해</span><span class="sxs-lookup"><span data-stu-id="36b43-110">Understand the scenario</span></span>

<span data-ttu-id="36b43-111">HDInsight 클러스터는 일부 샘플 데이터와 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-111">HDInsight cluster comes with some sample data.</span></span> <span data-ttu-id="36b43-112">다음 두 샘플을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-112">You use the following two samples:</span></span>

* <span data-ttu-id="36b43-113">*/example/data/sample.log*에 있는 log4j 로그 파일.</span><span class="sxs-lookup"><span data-stu-id="36b43-113">A log4j log file, which is located at */example/data/sample.log*.</span></span> <span data-ttu-id="36b43-114">이 파일에서 다음 로그가 추출됩니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-114">The following logs are extracted from the file:</span></span>
  
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
* <span data-ttu-id="36b43-115">*/hive/warehouse/hivesampletable*에 있는 데이터 파일을 참조하는 *hivesampletable*이라는 이름의 Hive 테이블.</span><span class="sxs-lookup"><span data-stu-id="36b43-115">A Hive table named *hivesampletable*, which references the data file located at */hive/warehouse/hivesampletable*.</span></span> <span data-ttu-id="36b43-116">이 테이블에는 일부 모바일 장치 데이터가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-116">The table contains some mobile device data.</span></span> 
  
  | <span data-ttu-id="36b43-117">필드</span><span class="sxs-lookup"><span data-stu-id="36b43-117">Field</span></span> | <span data-ttu-id="36b43-118">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="36b43-118">Data type</span></span> |
  | --- | --- |
  | <span data-ttu-id="36b43-119">clientid</span><span class="sxs-lookup"><span data-stu-id="36b43-119">clientid</span></span> |<span data-ttu-id="36b43-120">string</span><span class="sxs-lookup"><span data-stu-id="36b43-120">string</span></span> |
  | <span data-ttu-id="36b43-121">querytime</span><span class="sxs-lookup"><span data-stu-id="36b43-121">querytime</span></span> |<span data-ttu-id="36b43-122">string</span><span class="sxs-lookup"><span data-stu-id="36b43-122">string</span></span> |
  | <span data-ttu-id="36b43-123">market</span><span class="sxs-lookup"><span data-stu-id="36b43-123">market</span></span> |<span data-ttu-id="36b43-124">string</span><span class="sxs-lookup"><span data-stu-id="36b43-124">string</span></span> |
  | <span data-ttu-id="36b43-125">deviceplatform</span><span class="sxs-lookup"><span data-stu-id="36b43-125">deviceplatform</span></span> |<span data-ttu-id="36b43-126">string</span><span class="sxs-lookup"><span data-stu-id="36b43-126">string</span></span> |
  | <span data-ttu-id="36b43-127">devicemake</span><span class="sxs-lookup"><span data-stu-id="36b43-127">devicemake</span></span> |<span data-ttu-id="36b43-128">string</span><span class="sxs-lookup"><span data-stu-id="36b43-128">string</span></span> |
  | <span data-ttu-id="36b43-129">devicemodel</span><span class="sxs-lookup"><span data-stu-id="36b43-129">devicemodel</span></span> |<span data-ttu-id="36b43-130">string</span><span class="sxs-lookup"><span data-stu-id="36b43-130">string</span></span> |
  | <span data-ttu-id="36b43-131">state</span><span class="sxs-lookup"><span data-stu-id="36b43-131">state</span></span> |<span data-ttu-id="36b43-132">string</span><span class="sxs-lookup"><span data-stu-id="36b43-132">string</span></span> |
  | <span data-ttu-id="36b43-133">country</span><span class="sxs-lookup"><span data-stu-id="36b43-133">country</span></span> |<span data-ttu-id="36b43-134">string</span><span class="sxs-lookup"><span data-stu-id="36b43-134">string</span></span> |
  | <span data-ttu-id="36b43-135">querydwelltime</span><span class="sxs-lookup"><span data-stu-id="36b43-135">querydwelltime</span></span> |<span data-ttu-id="36b43-136">double</span><span class="sxs-lookup"><span data-stu-id="36b43-136">double</span></span> |
  | <span data-ttu-id="36b43-137">sessionid</span><span class="sxs-lookup"><span data-stu-id="36b43-137">sessionid</span></span> |<span data-ttu-id="36b43-138">bigint</span><span class="sxs-lookup"><span data-stu-id="36b43-138">bigint</span></span> |
  | <span data-ttu-id="36b43-139">sessionpagevieworder</span><span class="sxs-lookup"><span data-stu-id="36b43-139">sessionpagevieworder</span></span> |<span data-ttu-id="36b43-140">bigint</span><span class="sxs-lookup"><span data-stu-id="36b43-140">bigint</span></span> |

<span data-ttu-id="36b43-141">먼저 *sample.log*와 *hivesampletable*을 Azure SQL Database 또는 SQL Server에 내보낸 후 모바일 장치 데이터를 포함하는 테이블을 다음 경로를 통해 HDInsight에 다시 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-141">First, you export *sample.log* and *hivesampletable* to the Azure SQL database or to SQL Server, and then import the table that contains the mobile device data back to HDInsight by using the following path:</span></span>

    /tutorials/usesqoop/importeddata

## <a name="create-cluster-and-sql-database"></a><span data-ttu-id="36b43-142">클러스터 및 SQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="36b43-142">Create cluster and SQL database</span></span>
<span data-ttu-id="36b43-143">이 섹션에서는 Azure Portal 및 Azure Resource Manager 템플릿을 사용하는 자습서를 실행하기 위해 클러스터 및 SQL Database 스키마를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-143">This section shows you how to create a cluster, a SQL Database, and the SQL database schemas for running the tutorial using the Azure portal and an Azure Resource Manager template.</span></span> <span data-ttu-id="36b43-144">템플릿은 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-144">The template can be found in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span></span> <span data-ttu-id="36b43-145">Resource Manager 템플릿은 SQL Database에 테이블 스키마를 배포하는 bacpac 패키지를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-145">The Resource Manager template calls a bacpac package to deploy the table schemas to SQL database.</span></span>  <span data-ttu-id="36b43-146">bacpac 패키지는 공용 Blob 컨테이너 https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-146">The bacpac package is located in a public blob container, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span></span> <span data-ttu-id="36b43-147">Bacpac 파일에 대한 개인 컨테이너를 사용하려는 경우 템플릿에 다음 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-147">If you want to use a private container for the bacpac files, use the following values in the template:</span></span>
   
        "storageKeyType": "Primary",
        "storageKey": "<TheAzureStorageAccountKey>",

<span data-ttu-id="36b43-148">Azure PowerShell을 사용하여 클러스터 및 SQL Database를 만들려면 [부록 A](#appendix-a---a-powershell-sample)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36b43-148">If you prefer to use Azure PowerShell to create the cluster and the SQL Database, see [Appendix A](#appendix-a---a-powershell-sample).</span></span>

1. <span data-ttu-id="36b43-149">Azure Portal에서 Resource Manager 템플릿을 열려면 다음 이미지를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-149">Click the following image to open a Resource Manager template in the Azure portal.</span></span>         
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-sql-database%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-use-sqoop/deploy-to-azure.png" alt="Deploy to Azure"></a>
   

2. <span data-ttu-id="36b43-150">다음과 같은 속성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-150">Enter the following properties:</span></span>

    - <span data-ttu-id="36b43-151">**구독**: Azure 구독을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-151">**Subscription**: Enter your Azure subscription.</span></span>
    - <span data-ttu-id="36b43-152">**리소스 그룹**: 새 Azure 리소스 그룹을 만들거나 기존 Azure 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-152">**Resource Group**: Create a new Azure Resource Group, or select an existing Resource Group.</span></span>  <span data-ttu-id="36b43-153">리소스 그룹은 관리 목적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-153">A Resource Group is for management purpose.</span></span>  <span data-ttu-id="36b43-154">개체에 대한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-154">It is a container for objects.</span></span>
    - <span data-ttu-id="36b43-155">**위치**: 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-155">**Location**: Select a region.</span></span>
    - <span data-ttu-id="36b43-156">**클러스터 이름**: Hadoop 클러스터의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-156">**ClusterName**: Enter a name for the Hadoop cluster.</span></span>
    - <span data-ttu-id="36b43-157">**클러스터 로그인 이름 및 암호**: 기본 로그인 이름은 admin입니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-157">**Cluster login name and password**: The default login name is admin.</span></span>
    - <span data-ttu-id="36b43-158">**SSH 사용자 이름 및 암호**.</span><span class="sxs-lookup"><span data-stu-id="36b43-158">**SSH user name and password**.</span></span>
    - <span data-ttu-id="36b43-159">**SQL 데이터베이스 서버 로그인 이름 및 암호**.</span><span class="sxs-lookup"><span data-stu-id="36b43-159">**SQL database server login name and password**.</span></span>
    - <span data-ttu-id="36b43-160">**_artifacts 위치**: 다른 위치에 직접 backpac 파일을 사용하려는 경우가 아니면 기본값을 그대로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-160">**_artifacts Location**: Use the default value unless you want to use your own backpac file in a different location.</span></span>
    - <span data-ttu-id="36b43-161">**_artifacts 위치 Sas 토큰**: 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-161">**_artifacts Location Sas Token**: Leave it blank.</span></span>
    - <span data-ttu-id="36b43-162">**Bacpac 파일 이름**: 자체 backpac 파일을 사용하려는 경우가 아니면 기본값을 그대로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-162">**Bacpac File Name**: Use the default value unless you want to use your own backpac file.</span></span>
     
     <span data-ttu-id="36b43-163">다음 값은 변수 섹션에서 하드 코드합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-163">The following values are hardcoded in the variables section:</span></span>
     
     | <span data-ttu-id="36b43-164">기본 저장소 계정 이름</span><span class="sxs-lookup"><span data-stu-id="36b43-164">Default storage account name</span></span> | <span data-ttu-id="36b43-165"><CluterName>store</span><span class="sxs-lookup"><span data-stu-id="36b43-165"><CluterName>store</span></span> |
     | --- | --- |
     | <span data-ttu-id="36b43-166">Azure SQL 데이터베이스 서버 이름</span><span class="sxs-lookup"><span data-stu-id="36b43-166">Azure SQL database server name</span></span> |<span data-ttu-id="36b43-167"><ClusterName>dbserver</span><span class="sxs-lookup"><span data-stu-id="36b43-167"><ClusterName>dbserver</span></span> |
     | <span data-ttu-id="36b43-168">Azure SQL 데이터베이스 이름</span><span class="sxs-lookup"><span data-stu-id="36b43-168">Azure SQL database name</span></span> |<span data-ttu-id="36b43-169"><ClusterName>db</span><span class="sxs-lookup"><span data-stu-id="36b43-169"><ClusterName>db</span></span> |
     
     <span data-ttu-id="36b43-170">이러한 값을 기록해 두십시오.</span><span class="sxs-lookup"><span data-stu-id="36b43-170">Please write down these values.</span></span>  <span data-ttu-id="36b43-171">이 정보는 자습서의 뒷부분에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-171">You need them later in the tutorial.</span></span>

<span data-ttu-id="36b43-172">3.**확인**을 클릭하여 매개 변수를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-172">3.Click **OK** to save the parameters.</span></span>

<span data-ttu-id="36b43-173">4.**사용자 지정 배포** 블레이드에서 **리소스 그룹** 드롭다운 상자를 클릭한 다음 **새로 만들기**를 클릭하여 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-173">4.From the **Custom deployment** blade, click **Resource group** dropdown box, and then click **New** to create a new resource group.</span></span> <span data-ttu-id="36b43-174">리소스 그룹은 클러스터, 종속 저장소 계정 및 기타 연결된 리소스를 그룹화하는 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-174">The resource group is a container that groups the cluster, the dependent storage account and other linked resource.</span></span>

<span data-ttu-id="36b43-175">5.**약관**을 클릭한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-175">5.Click **Legal terms**, and then click **Create**.</span></span>

<span data-ttu-id="36b43-176">6.**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-176">6.Click **Create**.</span></span> <span data-ttu-id="36b43-177">템플릿 배포에 배포 제출 중이라는 제목의 새 타일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-177">You see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="36b43-178">클러스터 및 SQL 데이터베이스를 만들려면 20분 정도가 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-178">It takes about around 20 minutes to create the cluster and SQL database.</span></span>

<span data-ttu-id="36b43-179">기존 Azure SQL 데이터베이스 또는 Microsoft SQL Server를 사용하기로 선택하는 경우</span><span class="sxs-lookup"><span data-stu-id="36b43-179">If you choose to use existing Azure SQL database or Microsoft SQL Server</span></span>

* <span data-ttu-id="36b43-180">**Azure SQL 데이터베이스**: 워크스테이션에서 액세스할 수 있도록 Azure SQL 데이터베이스 서버의 방화벽 규칙을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-180">**Azure SQL database**: You must configure a firewall rule for the Azure SQL database server to allow access from your workstation.</span></span> <span data-ttu-id="36b43-181">Azure SQL Database 만들기 및 방화벽 구성에 대한 자세한 내용은 [Azure SQL Database 사용 시작][sqldatabase-get-started]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36b43-181">For instructions about creating an Azure SQL database and configuring the firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="36b43-182">기본적으로 Azure SQL 데이터베이스는 Azure HDInsight 같은 Azure 서비스로부터의 연결을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-182">By default an Azure SQL database allows connections from Azure services, such as Azure HDInsight.</span></span> <span data-ttu-id="36b43-183">이 방화벽 설정을 사용하지 않도록 설정한 경우 Azure Portal에서 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-183">If this firewall setting is disabled, you need to enable it from the Azure portal.</span></span> <span data-ttu-id="36b43-184">Azure SQL Database 만들기 및 방화벽 규칙 구성에 대한 지침은 [SQL Database 만들기 및 구성][sqldatabase-create-configue]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36b43-184">For instruction about creating an Azure SQL database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-create-configue].</span></span>
  > 
  > 
* <span data-ttu-id="36b43-185">**SQL Server**: HDInsight 클러스터가 SQL Server와 같은 Azure의 가상 네트워크에 있으면 이 문서의 단계를 사용하여 SQL Server 데이터베이스에 대해 데이터 가져오기 및 내보내기를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-185">**SQL Server**: If your HDInsight cluster is on the same virtual network in Azure as SQL Server, you can use the steps in this article to import and export data to a SQL Server database.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="36b43-186">HDInsight는 위치 기반 가상 네트워크만 지원하며 현재 선호도 그룹 기반 가상 네트워크와는 연동되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-186">HDInsight supports only location-based virtual networks, and it does not currently work with affinity group-based virtual networks.</span></span>
  > 
  > 
  
  * <span data-ttu-id="36b43-187">가상 네트워크를 만들고 구성하려면 [Azure Portal을 사용하여 가상 네트워크 만들기](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)를 참조하세요</span><span class="sxs-lookup"><span data-stu-id="36b43-187">To create and configure a virtual network, see [Create a virtual network using the Azure portal](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>
    
    * <span data-ttu-id="36b43-188">데이터 센터에서 SQL Server를 사용할 때는 가상 네트워크를 *사이트 간* 또는 *지점 및 사이트 간*으로 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-188">When you are using SQL Server in your datacenter, you must configure the virtual network as *site-to-site* or *point-to-site*.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="36b43-189">**지점 및 사이트 간** 가상 네트워크의 경우 SQL Server가 VPN 클라이언트 구성 응용 프로그램을 실행해야 합니다. 이 응용 프로그램은 Azure 가상 네트워크 구성의 **대시보드**에서 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-189">For **point-to-site** virtual networks, SQL Server must be running the VPN client configuration application, which is available from the **Dashboard** of your Azure virtual network configuration.</span></span>
      > 
      > 
    * <span data-ttu-id="36b43-190">Azure 가상 컴퓨터에서 SQL Server를 사용할 때는 SQL Server를 호스트하는 가상 컴퓨터가 HDInsight와 같은 가상 네트워크의 멤버이면 모든 가상 네트워크 구성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-190">When you are using SQL Server on an Azure virtual machine, any virtual network configuration can be used if the virtual machine hosting SQL Server is a member of the same virtual network as HDInsight.</span></span>
  * <span data-ttu-id="36b43-191">가상 네트워크에 HDInsight 클러스터를 만들려면 [사용자 지정 옵션을 사용하여 HDInsight의 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="36b43-191">To create an HDInsight cluster on a virtual network, see [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="36b43-192">SQL Server는 인증도 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-192">SQL Server must also allow authentication.</span></span> <span data-ttu-id="36b43-193">이 문서의 단계를 완료하려면 SQL 서버 로그인을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-193">You must use a SQL Server login to complete the steps in this article.</span></span>
    > 
    > 

## <a name="run-sqoop-jobs"></a><span data-ttu-id="36b43-194">Sqoop 작업 실행</span><span class="sxs-lookup"><span data-stu-id="36b43-194">Run Sqoop jobs</span></span>
<span data-ttu-id="36b43-195">HDInsight는 다양한 메서드를 사용하여 Sqoop 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-195">HDInsight can run Sqoop jobs by using a variety of methods.</span></span> <span data-ttu-id="36b43-196">어떤 메서드가 적합한지 결정하는 다음 테이블을 사용하여 연습할 수 있는 링크를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="36b43-196">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="36b43-197">**이것을 사용** 하세요...</span><span class="sxs-lookup"><span data-stu-id="36b43-197">**Use this** if you want...</span></span> | <span data-ttu-id="36b43-198">... **대화형** 셸</span><span class="sxs-lookup"><span data-stu-id="36b43-198">...an **interactive** shell</span></span> | <span data-ttu-id="36b43-199">...**배치** 처리</span><span class="sxs-lookup"><span data-stu-id="36b43-199">...**batch** processing</span></span> | <span data-ttu-id="36b43-200">... **클러스터 운영 체제**</span><span class="sxs-lookup"><span data-stu-id="36b43-200">...with this **cluster operating system**</span></span> | <span data-ttu-id="36b43-201">... **클라이언트 운영 체제**</span><span class="sxs-lookup"><span data-stu-id="36b43-201">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="36b43-202">SSH</span><span class="sxs-lookup"><span data-stu-id="36b43-202">SSH</span></span>](hdinsight-use-sqoop-mac-linux.md) |<span data-ttu-id="36b43-203">✔</span><span class="sxs-lookup"><span data-stu-id="36b43-203">✔</span></span> |<span data-ttu-id="36b43-204">✔</span><span class="sxs-lookup"><span data-stu-id="36b43-204">✔</span></span> |<span data-ttu-id="36b43-205">Linux</span><span class="sxs-lookup"><span data-stu-id="36b43-205">Linux</span></span> |<span data-ttu-id="36b43-206">Linux, Unix, Mac OS X, 또는 Windows</span><span class="sxs-lookup"><span data-stu-id="36b43-206">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="36b43-207">Hadoop용 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="36b43-207">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="36b43-208">✔</span><span class="sxs-lookup"><span data-stu-id="36b43-208">✔</span></span> |<span data-ttu-id="36b43-209">Linux 또는or Windows</span><span class="sxs-lookup"><span data-stu-id="36b43-209">Linux or Windows</span></span> |<span data-ttu-id="36b43-210">Windows(당분간)</span><span class="sxs-lookup"><span data-stu-id="36b43-210">Windows (for now)</span></span> |
| [<span data-ttu-id="36b43-211">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="36b43-211">Azure PowerShell</span></span>](hdinsight-hadoop-use-sqoop-powershell.md) |&nbsp; |<span data-ttu-id="36b43-212">✔</span><span class="sxs-lookup"><span data-stu-id="36b43-212">✔</span></span> |<span data-ttu-id="36b43-213">Linux 또는or Windows</span><span class="sxs-lookup"><span data-stu-id="36b43-213">Linux or Windows</span></span> |<span data-ttu-id="36b43-214">Windows</span><span class="sxs-lookup"><span data-stu-id="36b43-214">Windows</span></span> |

## <a name="limitations"></a><span data-ttu-id="36b43-215">제한 사항</span><span class="sxs-lookup"><span data-stu-id="36b43-215">Limitations</span></span>
* <span data-ttu-id="36b43-216">대량 내보내기 - Linux 기반 HDInsight와 함께 Microsoft SQL Server 또는 Azure SQL 데이터베이스에 데이터를 내보내는 데 사용된 Sqoop 커넥터도 현재 대량 삽입을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-216">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="36b43-217">배치 - Linux 기반 HDInsight에서 삽입을 수행할 때 `-batch` 스위치를 사용하는 경우 Sqoop는 삽입 작업을 일괄 처리하는 대신 여러 번의 삽입 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-217">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36b43-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="36b43-218">Next steps</span></span>
<span data-ttu-id="36b43-219">이제 Sqoop을 사용하는 방법에 대해 알아봤습니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-219">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="36b43-220">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36b43-220">To learn more, see:</span></span>

* [<span data-ttu-id="36b43-221">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="36b43-221">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="36b43-222">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="36b43-222">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* <span data-ttu-id="36b43-223">[HDInsight와 함께 Oozie 사용][hdinsight-use-oozie]: Oozie 워크플로에서 Sqoop 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-223">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="36b43-224">[HDInsight를 사용하여 비행 지연 데이터 분석][hdinsight-analyze-flight-data]: Hive를 사용하여 비행 지연 데이터를 분석한 후 Sqoop을 사용하여 데이터를 Azure SQL Database로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-224">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="36b43-225">[HDInsight에 데이터 업로드][hdinsight-upload-data]: HDInsight/Azure Blob Storage에 데이터를 업로드하는 다른 방법을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-225">[Upload data to HDInsight][hdinsight-upload-data]: Find other methods for uploading data to HDInsight/Azure Blob storage.</span></span>

## <a name="appendix-a---a-powershell-sample"></a><span data-ttu-id="36b43-226">부록 A - PowerShell 샘플</span><span class="sxs-lookup"><span data-stu-id="36b43-226">Appendix A - a PowerShell sample</span></span>
<span data-ttu-id="36b43-227">PowerShell 샘플은 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-227">The PowerShell sample performs the following steps:</span></span>

1. <span data-ttu-id="36b43-228">Azure에 연결</span><span class="sxs-lookup"><span data-stu-id="36b43-228">Connect to Azure.</span></span>
2. <span data-ttu-id="36b43-229">Azure 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="36b43-229">Create an Azure resource group.</span></span> <span data-ttu-id="36b43-230">자세한 내용은 [Azure 리소스 관리자로 Azure PowerShell 사용](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="36b43-230">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)</span></span>
3. <span data-ttu-id="36b43-231">Azure SQL 데이터베이스 서버, Azure SQL 데이터베이스 및 두 개의 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-231">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span></span> 
   
    <span data-ttu-id="36b43-232">SQL Server를 대신 사용하는 경우에는 다음 문을 사용하여 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-232">If you use SQL Server instead, use the following statements to create the tables:</span></span>
   
        CREATE TABLE [dbo].[log4jlogs](
         [t1] [nvarchar](50),
         [t2] [nvarchar](50),
         [t3] [nvarchar](50),
         [t4] [nvarchar](50),
         [t5] [nvarchar](50),
         [t6] [nvarchar](50),
         [t7] [nvarchar](50))
   
        CREATE TABLE [dbo].[mobiledata](
         [clientid] [nvarchar](50),
         [querytime] [nvarchar](50),
         [market] [nvarchar](50),
         [deviceplatform] [nvarchar](50),
         [devicemake] [nvarchar](50),
         [devicemodel] [nvarchar](50),
         [state] [nvarchar](50),
         [country] [nvarchar](50),
         [querydwelltime] [float],
         [sessionid] [bigint],
         [sessionpagevieworder][bigint])
   
    <span data-ttu-id="36b43-233">데이터베이스 및 테이블을 검사하는 가장 쉬운 방법은 Visual Studio를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-233">The easiest way to examine the database and tables is to use Visual Studio.</span></span> <span data-ttu-id="36b43-234">Azure 포털을 사용하여 데이터베이스 서버와 데이터베이스를 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-234">The database server and the database can be examined using the Azure portal.</span></span>
4. <span data-ttu-id="36b43-235">HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="36b43-235">Create an HDInsight cluster.</span></span>
   
    <span data-ttu-id="36b43-236">클러스터를 검사하려면 Azure 포털 또는 Azure PowerShell을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-236">To examine the cluster, you can use the Azure portal or Azure PowerShell.</span></span>
5. <span data-ttu-id="36b43-237">원본 데이터 파일을 전처리합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-237">Pre-process the source data file.</span></span>
   
    <span data-ttu-id="36b43-238">이 자습서에서는 log4j 로그 파일(구분된 파일) 및 Hive 테이블을 Azure SQL Database로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-238">In this tutorial, you export a log4j log file (a delimited file) and a Hive table to an Azure SQL database.</span></span> <span data-ttu-id="36b43-239">구분된 파일의 이름은 */example/data/sample.log*입니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-239">The delimited file is called */example/data/sample.log*.</span></span> <span data-ttu-id="36b43-240">자습서의 앞부분에 log4j 로그 샘플이 몇 개 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-240">Earlier in the tutorial, you saw a few samples of log4j logs.</span></span> <span data-ttu-id="36b43-241">로그 파일에는 일부 빈 줄과 일부 다음과 유사한 줄이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-241">In the log file, there are some empty lines and some lines similar to these:</span></span>
   
        java.lang.Exception: 2012-02-03 20:11:35 SampleClass2 [FATAL] unrecoverable system problem at id 609774657
            at com.osa.mocklogger.MockLogger$2.run(MockLogger.java:83)
   
    <span data-ttu-id="36b43-242">이 데이터를 사용하는 다른 예제에서는 이 줄이 있어도 관계없지만 데이터를 Azure SQL 데이터베이스 또는 SQL Server로 가져오려면 이러한 예외를 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-242">This is fine for other examples that use this data, but we must remove these exceptions before we can import into the Azure SQL database or SQL Server.</span></span> <span data-ttu-id="36b43-243">빈 문자열이 있거나 Azure SQL Database 테이블에 정의된 필드 수보다 요소 수가 더 적은 경우 Sqoop 내보내기는 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-243">Sqoop export  fails if there is an empty string or a line with a fewer elements than the number of fields defined in the Azure SQL database table.</span></span> <span data-ttu-id="36b43-244">log4jlogs 테이블에는 7가지 문자열 형식 필드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-244">The log4jlogs table has 7 string-type fields.</span></span>
   
    <span data-ttu-id="36b43-245">이 절차를 통해 클러스터에서 새 파일(tutorials/usesqoop/data/sample.log)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-245">This procedure creates a new file on the cluster: tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="36b43-246">수정한 데이터 파일을 검사하려면 Azure 포털, Azure 저장소 탐색기 도구 또는 Azure PowerShell을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-246">To examine the modified data file, you can use the Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span> <span data-ttu-id="36b43-247">[HDInsight 시작][hdinsight-get-started]에는 파일을 다운로드하고 그 파일의 내용을 표시하는 Azure PowerShell 사용에 관한 코드 샘플이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-247">[Get started with HDInsight][hdinsight-get-started] has a code sample for using Azure PowerShell to download a file and display the file content.</span></span>
6. <span data-ttu-id="36b43-248">데이터 파일을 Azure SQL 데이터베이스로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-248">Export a data file to the Azure SQL database.</span></span>
   
    <span data-ttu-id="36b43-249">원본 파일은 tutorials/usesqoop/data/sample.log입니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-249">The source file is tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="36b43-250">데이터를 내보낸 테이블은 log4jlogs라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-250">The table where the data is exported to is called log4jlogs.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="36b43-251">연결 문자열 정보를 제외하면 이 섹션의 단계는 Azure SQL 데이터베이스 또는 SQL Server에 대해 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-251">Other than connection string information, the steps in this section should work for an Azure SQL database or for SQL Server.</span></span> <span data-ttu-id="36b43-252">이러한 단계는 다음 구성을 사용하여 테스트했습니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-252">These steps were tested by using the following configuration:</span></span>
   > 
   > * <span data-ttu-id="36b43-253">**Azure 가상 네트워크 지점 및 사이트 간 구성**: 개인 데이터 센터에서 HDInsight 클러스터를 SQL Server에 연결하는 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-253">**Azure virtual network point-to-site configuration**: A virtual network connected the HDInsight cluster to a SQL Server in a private datacenter.</span></span> <span data-ttu-id="36b43-254">자세한 내용은 [관리 포털에서 지점 및 사이트 간 VPN 구성](../vpn-gateway/vpn-gateway-point-to-site-create.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36b43-254">See [Configure a Point-to-Site VPN in the Management Portal](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>
   > * <span data-ttu-id="36b43-255">**Azure HDInsight 3.1**: 가상 네트워크에서 클러스터를 만드는 방법에 대한 자세한 내용은 [사용자 지정 옵션을 사용하여 HDInsight의 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36b43-255">**Azure HDInsight 3.1**: See [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster on a virtual network.</span></span>
   > * <span data-ttu-id="36b43-256">**SQL Server 2014**: 인증을 허용하고 VPN 클라이언트 구성 패키지를 실행하여 가상 네트워크에 안전하게 연결할 수 있도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-256">**SQL Server 2014**: Configured to allow authentication and running the VPN client configuration package to connect securely to the virtual network.</span></span>
   > 
   > 
7. <span data-ttu-id="36b43-257">Hive 테이블을 Azure SQL 데이터베이스로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-257">Export a Hive table to the Azure SQL database.</span></span>
8. <span data-ttu-id="36b43-258">mobiledata 테이블을 HDInsight 클러스터로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-258">Import the mobiledata table to the HDInsight cluster.</span></span>
   
    <span data-ttu-id="36b43-259">수정한 데이터 파일을 검사하려면 Azure 포털, Azure 저장소 탐색기 도구 또는 Azure PowerShell을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-259">To examine the modified data file, you can use the Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span>  <span data-ttu-id="36b43-260">[HDInsight 시작][hdinsight-get-started]에는 파일을 다운로드하고 그 파일의 내용을 표시하는 Azure PowerShell 사용에 관한 코드 샘플이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b43-260">[Get started with HDInsight][hdinsight-get-started] has a code sample about using Azure PowerShell to download a file and display the file content.</span></span>

### <a name="the-powershell-sample"></a><span data-ttu-id="36b43-261">PowerShell 샘플</span><span class="sxs-lookup"><span data-stu-id="36b43-261">The PowerShell sample</span></span>
    # Prepare an Azure SQL database to be used by the Sqoop tutorial

    #region - provide the following values

    $subscriptionID = "<Enter your Azure Subscription ID>"

    $sqlDatabaseLogin = "<Enter a SQL Database Login name>" #SQL Database server login
    $sqlDatabasePassword = "<Enter a Password>"

    $httpUserName = "admin"  #HDInsight cluster username
    $httpPassword = "<Enter a Password>"

    # used for creating Azure service names
    $nameToken = "<Enter an alias>" 
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")
    #endregion

    #region - variables

    # Resource group variables
    $resourceGroupName = $namePrefix + "rg"
    $location = "East US 2" # used by all Azure services defined in this tutorial

    # SQL database varialbes
    $sqlDatabaseServerName = $namePrefix + "sqldbserver"
    $sqlDatabaseName = $namePrefix + "sqldb"
    $sqlDatabaseConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $sqlDatabaseMaxSizeGB = 10

    # Used for retrieving external IP address and creating firewall rules
    $ipAddressRestService = "http://bot.whatismyipaddress.com"
    $fireWallRuleName = "UseSqoop"

    # Used for creating tables and clustered indexes
    $cmdCreateLog4jTable = "CREATE TABLE [dbo].[log4jlogs](
        [t1] [nvarchar](50),
        [t2] [nvarchar](50),
        [t3] [nvarchar](50),
        [t4] [nvarchar](50),
        [t5] [nvarchar](50),
        [t6] [nvarchar](50),
        [t7] [nvarchar](50))"

    $cmdCreateLog4jClusteredIndex = "CREATE CLUSTERED INDEX log4jlogs_clustered_index on log4jlogs(t1)"

    $cmdCreateMobileTable = " CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder][bigint])"

    $cmdCreateMobileDataClusteredIndex = "CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)"

    # HDInsight variables
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - Create Azure resouce group
    Write-Host "`nCreating an Azure resource group ..." -ForegroundColor Green
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    }
    #endregion

    #region - Create Azure SQL database server
    Write-Host "`nCreating an Azure SQL Database server ..." -ForegroundColor Green
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServerName -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServerName = (New-AzureRmSqlServer `
                                    -ResourceGroupName $resourceGroupName `
                                    -ServerName $sqlDatabaseServerName `
                                    -SqlAdministratorCredentials $credential `
                                    -Location $location).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServerName." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-workstation" `
            -StartIpAddress $workstationIPAddress `
            -EndIpAddress $workstationIPAddress

        #To allow other Azure services to access the server add a firewall rule and set both the StartIpAddress and EndIpAddress to 0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription to access the server.
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-Azureservices" `
            -StartIpAddress "0.0.0.0" `
            -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database
    Write-Host "`nCreating an Azure SQL database ..." -ForegroundColor Green

    try {
        Get-AzureRmSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName `
            -Edition "Standard" `
            -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region - Create tables
    Write-Host "Creating the log4jlogs table and the mobiledata table ..." -ForegroundColor Green

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create the log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jTable
    $ret = $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateLog4jClusteredIndex
    $cmd.ExecuteNonQuery()

    # Create the mobiledata table and index
    $cmd.CommandText = $cmdCreateMobileTable
    $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateMobileDataClusteredIndex
    $cmd.ExecuteNonQuery()

    $conn.close()

    #endregion


    #region - Create HDInsight cluster

    Write-Host "Creating the HDInsight cluster and the dependent services ..." -ForegroundColor Green

    # Create the default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create the default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create the HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $defaultBlobContainerName 

    # Validate the cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - pre-process the source file

    Write-Host "Preprocessing the source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define the connection string
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing the source and destination blob.
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $sourceBlob = $storageContainer.GetBlockBlobReference($sourceBlobName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)

    # Define a MemoryStream and a StreamReader for reading from the source file
    $stream = New-Object System.IO.MemoryStream
    $stream = $sourceBlob.OpenRead()
    $sReader = New-Object System.IO.StreamReader($stream)

    # Define a MemoryStream and a StreamWriter for writing into the destination file
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    # Pre-process the source blob
    $exString = "java.lang.Exception:"
    while(-Not $sReader.EndOfStream){
        $line = $sReader.ReadLine()
        $split = $line.Split(" ")

        # remove the "java.lang.Exception" from the first element of the array
        # for example: java.lang.Exception: 2012-02-03 19:11:02 SampleClass8 [WARN] problem finding id 153454612
        if ($split[0] -eq $exString){
            #create a new ArrayList to remove $split[0]
            $newArray = [System.Collections.ArrayList] $split
            $newArray.Remove($exString)

            # update $split and $line
            $split = $newArray
            $line = $newArray -join(" ")
        }

        # remove the lines that has less than 7 elements
        if ($split.count -ge 7){
            write-host $line
            $writeStream.WriteLine($line)
        }
    }

    # Write to the destination blob
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    #endregion

    #region - export a log file from the cluster to the SQL database

    Write-Host "Preprocessing the source file ..." -ForegroundColor Green

    $tableName_log4j = "log4jlogs"

    # Connection string for Azure SQL Database.
    # Comment if using SQL Server
    $connectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"
    # Connection string for SQL Server.
    # Uncomment if using SQL Server.
    #$connectionString = "jdbc:sqlserver://$sqlDatabaseServerName;user=$sqlDatabaseLogin;password=$sqlDatabasePassword;database=$sqlDatabaseName"

    $exportDir_log4j = "/tutorials/usesqoop/data"

    # Submit a Sqoop job
    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_log4j --export-dir $exportDir_log4j --input-fields-terminated-by \0x20 -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose
    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardError
    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardOutput

    #endregion

    #region - export a Hive table

    $tableName_mobile = "mobiledata"
    $exportDir_mobile = "/hive/warehouse/hivesampletable"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_mobile --export-dir $exportDir_mobile --fields-terminated-by \t -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion

    #region - import a database

    $targetDir_mobile = "/tutorials/usesqoop/importeddata/"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "import --connect $connectionString --table $tableName_mobile --target-dir $targetDir_mobile --fields-terminated-by \t --lines-terminated-by \n -m 1"

    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion



[azure-management-portal]: https://portal.azure.com/

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database/sql-database-get-started.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
