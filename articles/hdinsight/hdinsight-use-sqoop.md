---
title: "Azure HDInsight (Hadoop)와 aaaRun Apache Sqoop 작업 | Microsoft Docs"
description: "워크스테이션 toorun Sqoop에서에서 Azure PowerShell toouse 가져오고 Hadoop 클러스터와 Azure SQL 데이터베이스 내보내기에 대해 알아봅니다."
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
ms.openlocfilehash: bdac507704937d77921c9c13d70aa2434c7e3be4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-sqoop-with-hadoop-in-hdinsight"></a><span data-ttu-id="69121-103">HDInsight에서 Hadoop과 Sqoop 사용</span><span class="sxs-lookup"><span data-stu-id="69121-103">Use Sqoop with Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="69121-104">자세한 내용은 방법 HDInsight tooimport 및 HDInsight 클러스터와 Azure SQL 데이터베이스 또는 SQL Server 데이터베이스 간에 내보내기에서 Sqoop toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-104">Learn how toouse Sqoop in HDInsight tooimport and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

<span data-ttu-id="69121-105">Hadoop 로그 파일과 같은 구조화 되지 않은 작업과 구조화 된 데이터를 처리 하기 위한 자연 스러운 선택 되어도 수도 있습니다 관계형 데이터베이스에 저장 된 필요 tooprocess 구조화 된 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="69121-105">Although Hadoop is a natural choice for processing unstructured and semistructured data, such as logs and files, there may also be a need tooprocess structured data that is stored in relational databases.</span></span>

<span data-ttu-id="69121-106">[Sqoop] [ sqoop-user-guide-1.4.4] 은 설계 된 도구 tootransfer Hadoop 클러스터 및 관계형 데이터베이스 간에 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="69121-106">[Sqoop][sqoop-user-guide-1.4.4] is a tool designed tootransfer data between Hadoop clusters and relational databases.</span></span> <span data-ttu-id="69121-107">사용할 수 있습니다 (RDBMS) 관계형 데이터베이스 관리 시스템에서 tooimport 데이터와 같은 SQL Server, MySQL 또는 hello distributed Hadoop 파일 시스템 (HDFS)에 Oracle에서 Hadoop MapReduce 또는 하이브를 hello 데이터 변환한 다음에 다시 hello 데이터를 내보낼는 RDBMS 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-107">You can use it tooimport data from a relational database management system (RDBMS) such as SQL Server, MySQL, or Oracle into hello Hadoop distributed file system (HDFS), transform hello data in Hadoop with MapReduce or Hive, and then export hello data back into an RDBMS.</span></span> <span data-ttu-id="69121-108">이 자습서에서는 관계형 데이터베이스에 SQL Server 데이터베이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-108">In this tutorial, you are using a SQL Server database for your relational database.</span></span>

<span data-ttu-id="69121-109">HDInsight 클러스터에서 지원 되는 Sqoop 버전에서는 참조 [HDInsight에서 제공 하는 hello 클러스터 버전의 새로운 기능?][hdinsight-versions]</span><span class="sxs-lookup"><span data-stu-id="69121-109">For Sqoop versions that are supported on HDInsight clusters, see [What's new in hello cluster versions provided by HDInsight?][hdinsight-versions]</span></span>

## <a name="understand-hello-scenario"></a><span data-ttu-id="69121-110">Hello 시나리오를 이해합니다</span><span class="sxs-lookup"><span data-stu-id="69121-110">Understand hello scenario</span></span>

<span data-ttu-id="69121-111">HDInsight 클러스터는 일부 샘플 데이터와 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="69121-111">HDInsight cluster comes with some sample data.</span></span> <span data-ttu-id="69121-112">다음 두 개의 샘플 hello 사용:</span><span class="sxs-lookup"><span data-stu-id="69121-112">You use hello following two samples:</span></span>

* <span data-ttu-id="69121-113">*/example/data/sample.log*에 있는 log4j 로그 파일.</span><span class="sxs-lookup"><span data-stu-id="69121-113">A log4j log file, which is located at */example/data/sample.log*.</span></span> <span data-ttu-id="69121-114">다음 로그 hello hello 파일에서 추출 된:</span><span class="sxs-lookup"><span data-stu-id="69121-114">hello following logs are extracted from hello file:</span></span>
  
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
* <span data-ttu-id="69121-115">명명 된 Hive 테이블 *hivesampletable*, 참조 데이터 파일에 있는 hello는 */hive/warehouse/hivesampletable*합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-115">A Hive table named *hivesampletable*, which references hello data file located at */hive/warehouse/hivesampletable*.</span></span> <span data-ttu-id="69121-116">hello 테이블 일부 모바일 장치 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-116">hello table contains some mobile device data.</span></span> 
  
  | <span data-ttu-id="69121-117">필드</span><span class="sxs-lookup"><span data-stu-id="69121-117">Field</span></span> | <span data-ttu-id="69121-118">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="69121-118">Data type</span></span> |
  | --- | --- |
  | <span data-ttu-id="69121-119">clientid</span><span class="sxs-lookup"><span data-stu-id="69121-119">clientid</span></span> |<span data-ttu-id="69121-120">string</span><span class="sxs-lookup"><span data-stu-id="69121-120">string</span></span> |
  | <span data-ttu-id="69121-121">querytime</span><span class="sxs-lookup"><span data-stu-id="69121-121">querytime</span></span> |<span data-ttu-id="69121-122">string</span><span class="sxs-lookup"><span data-stu-id="69121-122">string</span></span> |
  | <span data-ttu-id="69121-123">market</span><span class="sxs-lookup"><span data-stu-id="69121-123">market</span></span> |<span data-ttu-id="69121-124">string</span><span class="sxs-lookup"><span data-stu-id="69121-124">string</span></span> |
  | <span data-ttu-id="69121-125">deviceplatform</span><span class="sxs-lookup"><span data-stu-id="69121-125">deviceplatform</span></span> |<span data-ttu-id="69121-126">string</span><span class="sxs-lookup"><span data-stu-id="69121-126">string</span></span> |
  | <span data-ttu-id="69121-127">devicemake</span><span class="sxs-lookup"><span data-stu-id="69121-127">devicemake</span></span> |<span data-ttu-id="69121-128">string</span><span class="sxs-lookup"><span data-stu-id="69121-128">string</span></span> |
  | <span data-ttu-id="69121-129">devicemodel</span><span class="sxs-lookup"><span data-stu-id="69121-129">devicemodel</span></span> |<span data-ttu-id="69121-130">string</span><span class="sxs-lookup"><span data-stu-id="69121-130">string</span></span> |
  | <span data-ttu-id="69121-131">state</span><span class="sxs-lookup"><span data-stu-id="69121-131">state</span></span> |<span data-ttu-id="69121-132">string</span><span class="sxs-lookup"><span data-stu-id="69121-132">string</span></span> |
  | <span data-ttu-id="69121-133">country</span><span class="sxs-lookup"><span data-stu-id="69121-133">country</span></span> |<span data-ttu-id="69121-134">string</span><span class="sxs-lookup"><span data-stu-id="69121-134">string</span></span> |
  | <span data-ttu-id="69121-135">querydwelltime</span><span class="sxs-lookup"><span data-stu-id="69121-135">querydwelltime</span></span> |<span data-ttu-id="69121-136">double</span><span class="sxs-lookup"><span data-stu-id="69121-136">double</span></span> |
  | <span data-ttu-id="69121-137">sessionid</span><span class="sxs-lookup"><span data-stu-id="69121-137">sessionid</span></span> |<span data-ttu-id="69121-138">bigint</span><span class="sxs-lookup"><span data-stu-id="69121-138">bigint</span></span> |
  | <span data-ttu-id="69121-139">sessionpagevieworder</span><span class="sxs-lookup"><span data-stu-id="69121-139">sessionpagevieworder</span></span> |<span data-ttu-id="69121-140">bigint</span><span class="sxs-lookup"><span data-stu-id="69121-140">bigint</span></span> |

<span data-ttu-id="69121-141">먼저, 내보낸 *sample.log* 및 *hivesampletable* toohello Azure SQL 데이터베이스 또는 서버 tooSQL 및 hello 모바일 장치 데이터를 포함 하는 가져오기 hello 테이블 tooHDInsight hello를 사용 하 여 백업 다음 경로:</span><span class="sxs-lookup"><span data-stu-id="69121-141">First, you export *sample.log* and *hivesampletable* toohello Azure SQL database or tooSQL Server, and then import hello table that contains hello mobile device data back tooHDInsight by using hello following path:</span></span>

    /tutorials/usesqoop/importeddata

## <a name="create-cluster-and-sql-database"></a><span data-ttu-id="69121-142">클러스터 및 SQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="69121-142">Create cluster and SQL database</span></span>
<span data-ttu-id="69121-143">이 섹션에서는 클러스터 toocreate, SQL 데이터베이스 및 hello SQL 데이터베이스 스키마가 실행 중인 hello 자습서를 사용 하 여에 대 한 Azure 포털 및 Azure 리소스 관리자 템플릿 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="69121-143">This section shows you how toocreate a cluster, a SQL Database, and hello SQL database schemas for running hello tutorial using hello Azure portal and an Azure Resource Manager template.</span></span> <span data-ttu-id="69121-144">hello 서식 파일에서 확인할 수 있습니다 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/)합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-144">hello template can be found in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span></span> <span data-ttu-id="69121-145">리소스 관리자 템플릿 hello bacpac 패키지 toodeploy hello 테이블 스키마 tooSQL 데이터베이스를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-145">hello Resource Manager template calls a bacpac package toodeploy hello table schemas tooSQL database.</span></span>  <span data-ttu-id="69121-146">hello bacpac 패키지 https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac 공용 blob 컨테이너에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69121-146">hello bacpac package is located in a public blob container, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span></span> <span data-ttu-id="69121-147">Hello bacpac 파일에 대 한 toouse 개인 컨테이너를 원하는 경우 다음 hello 서식 파일의 값에는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-147">If you want toouse a private container for hello bacpac files, use hello following values in hello template:</span></span>
   
        "storageKeyType": "Primary",
        "storageKey": "<TheAzureStorageAccountKey>",

<span data-ttu-id="69121-148">Toouse Azure PowerShell toocreate hello 클러스터와 SQL 데이터베이스 hello를 선호 하는 경우 참조 [부록 A](#appendix-a---a-powershell-sample)합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-148">If you prefer toouse Azure PowerShell toocreate hello cluster and hello SQL Database, see [Appendix A](#appendix-a---a-powershell-sample).</span></span>

1. <span data-ttu-id="69121-149">다음 이미지 tooopen hello Azure 포털에서에서 리소스 관리자 템플릿으로 hello를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-149">Click hello following image tooopen a Resource Manager template in hello Azure portal.</span></span>         
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-sql-database%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-use-sqoop/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   

2. <span data-ttu-id="69121-150">Hello 다음과 같은 속성을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-150">Enter hello following properties:</span></span>

    - <span data-ttu-id="69121-151">**구독**: Azure 구독을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-151">**Subscription**: Enter your Azure subscription.</span></span>
    - <span data-ttu-id="69121-152">**리소스 그룹**: 새 Azure 리소스 그룹을 만들거나 기존 Azure 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-152">**Resource Group**: Create a new Azure Resource Group, or select an existing Resource Group.</span></span>  <span data-ttu-id="69121-153">리소스 그룹은 관리 목적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69121-153">A Resource Group is for management purpose.</span></span>  <span data-ttu-id="69121-154">개체에 대한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="69121-154">It is a container for objects.</span></span>
    - <span data-ttu-id="69121-155">**위치**: 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-155">**Location**: Select a region.</span></span>
    - <span data-ttu-id="69121-156">**ClusterName**: hello Hadoop 클러스터에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-156">**ClusterName**: Enter a name for hello Hadoop cluster.</span></span>
    - <span data-ttu-id="69121-157">**로그인 이름 및 암호를 클러스터**: hello 기본 로그인 이름은 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="69121-157">**Cluster login name and password**: hello default login name is admin.</span></span>
    - <span data-ttu-id="69121-158">**SSH 사용자 이름 및 암호**.</span><span class="sxs-lookup"><span data-stu-id="69121-158">**SSH user name and password**.</span></span>
    - <span data-ttu-id="69121-159">**SQL 데이터베이스 서버 로그인 이름 및 암호**.</span><span class="sxs-lookup"><span data-stu-id="69121-159">**SQL database server login name and password**.</span></span>
    - <span data-ttu-id="69121-160">**위치 _artifacts**: toouse 고유한 backpac 파일을 다른 위치에 사용 하려는 경우가 아니면 hello 기본값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-160">**_artifacts Location**: Use hello default value unless you want toouse your own backpac file in a different location.</span></span>
    - <span data-ttu-id="69121-161">**_artifacts 위치 Sas 토큰**: 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="69121-161">**_artifacts Location Sas Token**: Leave it blank.</span></span>
    - <span data-ttu-id="69121-162">**Bacpac 파일 이름**: toouse backpac 파일을 직접 사용 하려는 경우가 아니면 hello 기본값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-162">**Bacpac File Name**: Use hello default value unless you want toouse your own backpac file.</span></span>
     
     <span data-ttu-id="69121-163">다음 값에는 hello는 hello 변수 섹션에서 하드 코드 됨.</span><span class="sxs-lookup"><span data-stu-id="69121-163">hello following values are hardcoded in hello variables section:</span></span>
     
     | <span data-ttu-id="69121-164">기본 저장소 계정 이름</span><span class="sxs-lookup"><span data-stu-id="69121-164">Default storage account name</span></span> | <span data-ttu-id="69121-165"><CluterName>store</span><span class="sxs-lookup"><span data-stu-id="69121-165"><CluterName>store</span></span> |
     | --- | --- |
     | <span data-ttu-id="69121-166">Azure SQL 데이터베이스 서버 이름</span><span class="sxs-lookup"><span data-stu-id="69121-166">Azure SQL database server name</span></span> |<span data-ttu-id="69121-167"><ClusterName>dbserver</span><span class="sxs-lookup"><span data-stu-id="69121-167"><ClusterName>dbserver</span></span> |
     | <span data-ttu-id="69121-168">Azure SQL 데이터베이스 이름</span><span class="sxs-lookup"><span data-stu-id="69121-168">Azure SQL database name</span></span> |<span data-ttu-id="69121-169"><ClusterName>db</span><span class="sxs-lookup"><span data-stu-id="69121-169"><ClusterName>db</span></span> |
     
     <span data-ttu-id="69121-170">이러한 값을 기록해 두십시오.</span><span class="sxs-lookup"><span data-stu-id="69121-170">Please write down these values.</span></span>  <span data-ttu-id="69121-171">Hello 자습서의 뒷부분에 나오는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-171">You need them later in hello tutorial.</span></span>

<span data-ttu-id="69121-172">3. 클릭 **확인** toosave hello 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="69121-172">3.Click **OK** toosave hello parameters.</span></span>

<span data-ttu-id="69121-173">4. hello에서 **사용자 지정 배포** 블레이드에서 클릭 **리소스 그룹** 드롭다운 상자를 선택한 다음 클릭 **새로** toocreate 새 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="69121-173">4.From hello **Custom deployment** blade, click **Resource group** dropdown box, and then click **New** toocreate a new resource group.</span></span> <span data-ttu-id="69121-174">hello 리소스 그룹은 hello 클러스터, hello 종속 저장소 계정 및 다른 링크 된 리소스를 그룹화 하는 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="69121-174">hello resource group is a container that groups hello cluster, hello dependent storage account and other linked resource.</span></span>

<span data-ttu-id="69121-175">5.**약관**을 클릭한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-175">5.Click **Legal terms**, and then click **Create**.</span></span>

<span data-ttu-id="69121-176">6.**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-176">6.Click **Create**.</span></span> <span data-ttu-id="69121-177">템플릿 배포에 배포 제출 중이라는 제목의 새 타일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="69121-177">You see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="69121-178">약 20 분 toocreate hello 클러스터 및 SQL 데이터베이스에 대 한 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-178">It takes about around 20 minutes toocreate hello cluster and SQL database.</span></span>

<span data-ttu-id="69121-179">Toouse 기존 Azure SQL 데이터베이스 또는 Microsoft SQL Server를 선택 하는 경우</span><span class="sxs-lookup"><span data-stu-id="69121-179">If you choose toouse existing Azure SQL database or Microsoft SQL Server</span></span>

* <span data-ttu-id="69121-180">**Azure SQL 데이터베이스**: 워크스테이션에서 Azure SQL 데이터베이스 서버 tooallow 액세스 hello에 대 한 방화벽 규칙을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-180">**Azure SQL database**: You must configure a firewall rule for hello Azure SQL database server tooallow access from your workstation.</span></span> <span data-ttu-id="69121-181">Azure SQL 데이터베이스를 만들고 hello 방화벽을 구성 하는 방법에 대 한 지침은 [Azure SQL 데이터베이스를 사용 하 여 시작][sqldatabase-get-started]합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-181">For instructions about creating an Azure SQL database and configuring hello firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="69121-182">기본적으로 Azure SQL 데이터베이스는 Azure HDInsight 같은 Azure 서비스로부터의 연결을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-182">By default an Azure SQL database allows connections from Azure services, such as Azure HDInsight.</span></span> <span data-ttu-id="69121-183">이 방화벽 설정을 비활성화 해야 tooenable hello Azure 포털에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-183">If this firewall setting is disabled, you need tooenable it from hello Azure portal.</span></span> <span data-ttu-id="69121-184">Azure SQL Database 만들기 및 방화벽 규칙 구성에 대한 지침은 [SQL Database 만들기 및 구성][sqldatabase-create-configue]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69121-184">For instruction about creating an Azure SQL database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-create-configue].</span></span>
  > 
  > 
* <span data-ttu-id="69121-185">**SQL Server**: hello에 HDInsight 클러스터에 있으면 동일한 가상 네트워크 SQL Server와 Azure의 hello 단계가 문서 tooimport 및 내보내기 데이터 tooa SQL Server 데이터베이스에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69121-185">**SQL Server**: If your HDInsight cluster is on hello same virtual network in Azure as SQL Server, you can use hello steps in this article tooimport and export data tooa SQL Server database.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="69121-186">HDInsight는 위치 기반 가상 네트워크만 지원하며 현재 선호도 그룹 기반 가상 네트워크와는 연동되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69121-186">HDInsight supports only location-based virtual networks, and it does not currently work with affinity group-based virtual networks.</span></span>
  > 
  > 
  
  * <span data-ttu-id="69121-187">toocreate 가상 네트워크 구성, 참조 및 [hello Azure 포털을 사용 하 여 가상 네트워크 만들기](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-187">toocreate and configure a virtual network, see [Create a virtual network using hello Azure portal](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>
    
    * <span data-ttu-id="69121-188">SQL Server 데이터 센터를 사용 하는 경우에 hello와 가상 네트워크 구성 해야 *사이트 간* 또는 *지점 및 사이트*합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-188">When you are using SQL Server in your datacenter, you must configure hello virtual network as *site-to-site* or *point-to-site*.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="69121-189">에 대 한 **지점-사이트** 가상 네트워크, SQL Server를 실행 해야 hello VPN 클라이언트 hello에서 사용할 수 있는 구성 응용 프로그램 **대시보드** Azure 가상 네트워크 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-189">For **point-to-site** virtual networks, SQL Server must be running hello VPN client configuration application, which is available from hello **Dashboard** of your Azure virtual network configuration.</span></span>
      > 
      > 
    * <span data-ttu-id="69121-190">SQL Server를 호스트 하는 hello 가상 컴퓨터가 hello의 멤버인 경우 모든 가상 네트워크 구성을 사용할 수 있습니다는 Azure 가상 컴퓨터에서 SQL 서버를 사용 하는 경우 HDInsight와 동일한 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="69121-190">When you are using SQL Server on an Azure virtual machine, any virtual network configuration can be used if hello virtual machine hosting SQL Server is a member of hello same virtual network as HDInsight.</span></span>
  * <span data-ttu-id="69121-191">가상 네트워크에는 HDInsight 클러스터 toocreate 참조 [만들기 Hadoop 사용자 지정 옵션을 사용 하 여 HDInsight 클러스터를](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="69121-191">toocreate an HDInsight cluster on a virtual network, see [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="69121-192">SQL Server는 인증도 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-192">SQL Server must also allow authentication.</span></span> <span data-ttu-id="69121-193">SQL Server 로그인 toocomplete hello이 문서의 단계를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-193">You must use a SQL Server login toocomplete hello steps in this article.</span></span>
    > 
    > 

## <a name="run-sqoop-jobs"></a><span data-ttu-id="69121-194">Sqoop 작업 실행</span><span class="sxs-lookup"><span data-stu-id="69121-194">Run Sqoop jobs</span></span>
<span data-ttu-id="69121-195">HDInsight는 다양한 메서드를 사용하여 Sqoop 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69121-195">HDInsight can run Sqoop jobs by using a variety of methods.</span></span> <span data-ttu-id="69121-196">어느 방법이 적합 한, 테이블 toodecide 다음 hello를 사용 하 여 다음 연습은 hello 링크를 따라 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-196">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="69121-197">**이것을 사용** 하세요...</span><span class="sxs-lookup"><span data-stu-id="69121-197">**Use this** if you want...</span></span> | <span data-ttu-id="69121-198">... **대화형** 셸</span><span class="sxs-lookup"><span data-stu-id="69121-198">...an **interactive** shell</span></span> | <span data-ttu-id="69121-199">...**배치** 처리</span><span class="sxs-lookup"><span data-stu-id="69121-199">...**batch** processing</span></span> | <span data-ttu-id="69121-200">... **클러스터 운영 체제**</span><span class="sxs-lookup"><span data-stu-id="69121-200">...with this **cluster operating system**</span></span> | <span data-ttu-id="69121-201">... **클라이언트 운영 체제**</span><span class="sxs-lookup"><span data-stu-id="69121-201">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="69121-202">SSH</span><span class="sxs-lookup"><span data-stu-id="69121-202">SSH</span></span>](hdinsight-use-sqoop-mac-linux.md) |<span data-ttu-id="69121-203">✔</span><span class="sxs-lookup"><span data-stu-id="69121-203">✔</span></span> |<span data-ttu-id="69121-204">✔</span><span class="sxs-lookup"><span data-stu-id="69121-204">✔</span></span> |<span data-ttu-id="69121-205">Linux</span><span class="sxs-lookup"><span data-stu-id="69121-205">Linux</span></span> |<span data-ttu-id="69121-206">Linux, Unix, Mac OS X, 또는 Windows</span><span class="sxs-lookup"><span data-stu-id="69121-206">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="69121-207">Hadoop용 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="69121-207">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="69121-208">✔</span><span class="sxs-lookup"><span data-stu-id="69121-208">✔</span></span> |<span data-ttu-id="69121-209">Linux 또는or Windows</span><span class="sxs-lookup"><span data-stu-id="69121-209">Linux or Windows</span></span> |<span data-ttu-id="69121-210">Windows(당분간)</span><span class="sxs-lookup"><span data-stu-id="69121-210">Windows (for now)</span></span> |
| [<span data-ttu-id="69121-211">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="69121-211">Azure PowerShell</span></span>](hdinsight-hadoop-use-sqoop-powershell.md) |&nbsp; |<span data-ttu-id="69121-212">✔</span><span class="sxs-lookup"><span data-stu-id="69121-212">✔</span></span> |<span data-ttu-id="69121-213">Linux 또는or Windows</span><span class="sxs-lookup"><span data-stu-id="69121-213">Linux or Windows</span></span> |<span data-ttu-id="69121-214">Windows</span><span class="sxs-lookup"><span data-stu-id="69121-214">Windows</span></span> |

## <a name="limitations"></a><span data-ttu-id="69121-215">제한 사항</span><span class="sxs-lookup"><span data-stu-id="69121-215">Limitations</span></span>
* <span data-ttu-id="69121-216">대량 내보내기-와 Linux 기반 HDInsight, hello Sqoop 사용 커넥터 tooexport 데이터 tooMicrosoft SQL Server 또는 Azure SQL 데이터베이스 현재 대량 삽입을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69121-216">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="69121-217">일괄 처리-Linux 기반 HDInsight와 hello를 사용 하는 경우 `-batch` 삽입 수행 시 전환, Sqoop hello 삽입 작업을 일괄 처리 하는 대신 여러 개의 삽입이 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-217">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69121-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="69121-218">Next steps</span></span>
<span data-ttu-id="69121-219">파악 했으므로 이제 어떻게 toouse Sqoop 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-219">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="69121-220">toolearn 더 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="69121-220">toolearn more, see:</span></span>

* [<span data-ttu-id="69121-221">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="69121-221">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="69121-222">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="69121-222">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* <span data-ttu-id="69121-223">[HDInsight와 함께 Oozie 사용][hdinsight-use-oozie]: Oozie 워크플로에서 Sqoop 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-223">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="69121-224">[HDInsight를 사용 하 여 비행 연착 데이터를 분석][hdinsight-analyze-flight-data]: tooanalyze 비행 하이브 사용 하 여 데이터를 지연 하 고 다음 Sqoop tooexport 데이터 tooan Azure SQL 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-224">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="69121-225">[데이터 tooHDInsight 업로드][hdinsight-upload-data]: 데이터 tooHDInsight/Azure Blob 저장소에 업로드 하기 위한 다른 방법을 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-225">[Upload data tooHDInsight][hdinsight-upload-data]: Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

## <a name="appendix-a---a-powershell-sample"></a><span data-ttu-id="69121-226">부록 A - PowerShell 샘플</span><span class="sxs-lookup"><span data-stu-id="69121-226">Appendix A - a PowerShell sample</span></span>
<span data-ttu-id="69121-227">hello PowerShell 샘플 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-227">hello PowerShell sample performs hello following steps:</span></span>

1. <span data-ttu-id="69121-228">TooAzure를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-228">Connect tooAzure.</span></span>
2. <span data-ttu-id="69121-229">Azure 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="69121-229">Create an Azure resource group.</span></span> <span data-ttu-id="69121-230">자세한 내용은 [Azure 리소스 관리자로 Azure PowerShell 사용](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="69121-230">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)</span></span>
3. <span data-ttu-id="69121-231">Azure SQL 데이터베이스 서버, Azure SQL 데이터베이스 및 두 개의 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69121-231">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span></span> 
   
    <span data-ttu-id="69121-232">SQL Server를 대신 사용 하는 경우 다음 문은 toocreate hello 표 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-232">If you use SQL Server instead, use hello following statements toocreate hello tables:</span></span>
   
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
   
    <span data-ttu-id="69121-233">hello 가장 쉬운 방법은 tooexamine hello 데이터베이스 및 테이블에는 Visual Studio toouse입니다.</span><span class="sxs-lookup"><span data-stu-id="69121-233">hello easiest way tooexamine hello database and tables is toouse Visual Studio.</span></span> <span data-ttu-id="69121-234">hello 데이터베이스 서버 및 데이터베이스 hello hello Azure 포털을 사용 하 여 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69121-234">hello database server and hello database can be examined using hello Azure portal.</span></span>
4. <span data-ttu-id="69121-235">HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="69121-235">Create an HDInsight cluster.</span></span>
   
    <span data-ttu-id="69121-236">tooexamine hello 클러스터 hello Azure 포털 또는 Azure PowerShell을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69121-236">tooexamine hello cluster, you can use hello Azure portal or Azure PowerShell.</span></span>
5. <span data-ttu-id="69121-237">Hello 원본 데이터 파일을 전처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-237">Pre-process hello source data file.</span></span>
   
    <span data-ttu-id="69121-238">이 자습서에서는 log4j 로그 파일 (구분 기호로 분리 된 파일) 및 Hive 테이블 tooan Azure SQL 데이터베이스를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="69121-238">In this tutorial, you export a log4j log file (a delimited file) and a Hive table tooan Azure SQL database.</span></span> <span data-ttu-id="69121-239">hello 구분 기호로 분리 된 파일 이라고 */example/data/sample.log*합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-239">hello delimited file is called */example/data/sample.log*.</span></span> <span data-ttu-id="69121-240">Hello 자습서의 앞부분에 나오는 준다는 사실을 알았습니다 log4j 로그의 몇 가지 샘플.</span><span class="sxs-lookup"><span data-stu-id="69121-240">Earlier in hello tutorial, you saw a few samples of log4j logs.</span></span> <span data-ttu-id="69121-241">Hello 로그 파일에는 일부 빈 줄 및 줄 비슷한 toothese 일부:</span><span class="sxs-lookup"><span data-stu-id="69121-241">In hello log file, there are some empty lines and some lines similar toothese:</span></span>
   
        java.lang.Exception: 2012-02-03 20:11:35 SampleClass2 [FATAL] unrecoverable system problem at id 609774657
            at com.osa.mocklogger.MockLogger$2.run(MockLogger.java:83)
   
    <span data-ttu-id="69121-242">이 데이터를 사용 하는 다른 예에 대 한 문제가 있지만 전에 hello Azure SQL 데이터베이스 또는 SQL Server로 가져올 수 있습니다 이러한 예외를 제거 해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="69121-242">This is fine for other examples that use this data, but we must remove these exceptions before we can import into hello Azure SQL database or SQL Server.</span></span> <span data-ttu-id="69121-243">빈 문자열이 나 더 적은 있는 선 경우 Sqoop 내보내기 실패 함 hello Azure SQL 데이터베이스 테이블에 정의 된 필드의 hello 수보다 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="69121-243">Sqoop export  fails if there is an empty string or a line with a fewer elements than hello number of fields defined in hello Azure SQL database table.</span></span> <span data-ttu-id="69121-244">hello log4jlogs 테이블 7 문자열 형식 필드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69121-244">hello log4jlogs table has 7 string-type fields.</span></span>
   
    <span data-ttu-id="69121-245">이 절차에서는 hello 클러스터에서 새 파일을 만듭니다: tutorials/usesqoop/data/sample.log 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-245">This procedure creates a new file on hello cluster: tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="69121-246">tooexamine hello 수정 된 데이터 파일을 hello Azure 포털, Azure 저장소 탐색기 도구를 사용 하는 또는 Azure PowerShell을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69121-246">tooexamine hello modified data file, you can use hello Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span> <span data-ttu-id="69121-247">[HDInsight 시작] [ hdinsight-get-started] 코드는 Azure PowerShell toodownload 파일 사용에 대 한 샘플링 하 여 hello 파일 콘텐츠를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-247">[Get started with HDInsight][hdinsight-get-started] has a code sample for using Azure PowerShell toodownload a file and display hello file content.</span></span>
6. <span data-ttu-id="69121-248">데이터 파일 toohello Azure SQL 데이터베이스를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="69121-248">Export a data file toohello Azure SQL database.</span></span>
   
    <span data-ttu-id="69121-249">hello 소스 파일은 tutorials/usesqoop/data/sample.log입니다.</span><span class="sxs-lookup"><span data-stu-id="69121-249">hello source file is tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="69121-250">hello 데이터를 내보낸된 toois hello 테이블 log4jlogs를 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69121-250">hello table where hello data is exported toois called log4jlogs.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="69121-251">연결 문자열 정보를 이외의 SQL Server 또는 Azure SQL 데이터베이스에 대 한이 섹션의 단계 hello 작동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-251">Other than connection string information, hello steps in this section should work for an Azure SQL database or for SQL Server.</span></span> <span data-ttu-id="69121-252">다음이 단계를 같은 구성이 hello를 사용 하 여 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-252">These steps were tested by using hello following configuration:</span></span>
   > 
   > * <span data-ttu-id="69121-253">**Azure 가상 네트워크 지점-사이트 구성**: 가상 네트워크 hello HDInsight 클러스터 tooa SQL Server 개인 데이터 센터에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-253">**Azure virtual network point-to-site configuration**: A virtual network connected hello HDInsight cluster tooa SQL Server in a private datacenter.</span></span> <span data-ttu-id="69121-254">참조 [hello 관리 포털에서에서 지점 및 사이트 간 VPN 구성](../vpn-gateway/vpn-gateway-point-to-site-create.md) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-254">See [Configure a Point-to-Site VPN in hello Management Portal](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>
   > * <span data-ttu-id="69121-255">**Azure HDInsight 3.1**: 가상 네트워크에서 클러스터를 만드는 방법에 대한 자세한 내용은 [사용자 지정 옵션을 사용하여 HDInsight의 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69121-255">**Azure HDInsight 3.1**: See [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster on a virtual network.</span></span>
   > * <span data-ttu-id="69121-256">**SQL Server 2014**: tooallow 인증 및 실행 중인 hello VPN 클라이언트 구성 패키지 tooconnect를 안전 하 게 구성 toohello 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="69121-256">**SQL Server 2014**: Configured tooallow authentication and running hello VPN client configuration package tooconnect securely toohello virtual network.</span></span>
   > 
   > 
7. <span data-ttu-id="69121-257">하이브 테이블 toohello Azure SQL 데이터베이스를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="69121-257">Export a Hive table toohello Azure SQL database.</span></span>
8. <span data-ttu-id="69121-258">Hello mobiledata 테이블 toohello HDInsight 클러스터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="69121-258">Import hello mobiledata table toohello HDInsight cluster.</span></span>
   
    <span data-ttu-id="69121-259">tooexamine hello 수정 된 데이터 파일을 hello Azure 포털, Azure 저장소 탐색기 도구를 사용 하는 또는 Azure PowerShell을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69121-259">tooexamine hello modified data file, you can use hello Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span>  <span data-ttu-id="69121-260">[HDInsight 시작] [ hdinsight-get-started] 코드는 Azure PowerShell toodownload 파일 사용에 대 한 샘플링 하 여 hello 파일 콘텐츠를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="69121-260">[Get started with HDInsight][hdinsight-get-started] has a code sample about using Azure PowerShell toodownload a file and display hello file content.</span></span>

### <a name="hello-powershell-sample"></a><span data-ttu-id="69121-261">hello PowerShell 샘플</span><span class="sxs-lookup"><span data-stu-id="69121-261">hello PowerShell sample</span></span>
    # Prepare an Azure SQL database toobe used by hello Sqoop tutorial

    #region - provide hello following values

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

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
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

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
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
    Write-Host "Creating hello log4jlogs table and hello mobiledata table ..." -ForegroundColor Green

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create hello log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jTable
    $ret = $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateLog4jClusteredIndex
    $cmd.ExecuteNonQuery()

    # Create hello mobiledata table and index
    $cmd.CommandText = $cmdCreateMobileTable
    $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateMobileDataClusteredIndex
    $cmd.ExecuteNonQuery()

    $conn.close()

    #endregion


    #region - Create HDInsight cluster

    Write-Host "Creating hello HDInsight cluster and hello dependent services ..." -ForegroundColor Green

    # Create hello default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create hello HDInsight cluster
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

    # Validate hello cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - pre-process hello source file

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define hello connection string
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing hello source and destination blob.
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $sourceBlob = $storageContainer.GetBlockBlobReference($sourceBlobName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)

    # Define a MemoryStream and a StreamReader for reading from hello source file
    $stream = New-Object System.IO.MemoryStream
    $stream = $sourceBlob.OpenRead()
    $sReader = New-Object System.IO.StreamReader($stream)

    # Define a MemoryStream and a StreamWriter for writing into hello destination file
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    # Pre-process hello source blob
    $exString = "java.lang.Exception:"
    while(-Not $sReader.EndOfStream){
        $line = $sReader.ReadLine()
        $split = $line.Split(" ")

        # remove hello "java.lang.Exception" from hello first element of hello array
        # for example: java.lang.Exception: 2012-02-03 19:11:02 SampleClass8 [WARN] problem finding id 153454612
        if ($split[0] -eq $exString){
            #create a new ArrayList tooremove $split[0]
            $newArray = [System.Collections.ArrayList] $split
            $newArray.Remove($exString)

            # update $split and $line
            $split = $newArray
            $line = $newArray -join(" ")
        }

        # remove hello lines that has less than 7 elements
        if ($split.count -ge 7){
            write-host $line
            $writeStream.WriteLine($line)
        }
    }

    # Write toohello destination blob
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    #endregion

    #region - export a log file from hello cluster toohello SQL database

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

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
