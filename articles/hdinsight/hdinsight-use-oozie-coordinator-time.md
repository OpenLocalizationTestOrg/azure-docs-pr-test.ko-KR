---
title: "aaaUse HDInsight의 Hadoop Oozie 코디네이터 시간 기반 | Microsoft Docs"
description: "빅데이터 서비스인 HDInsight에서 시간 기준 Hadoop Oozie 코디네이터를 사용하는 방법을 알아봅니다. 자세한 방법을 toodefine Oozie 워크플로 및 코디네이터 및 작업을 제출 합니다."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00c3a395-d51a-44ff-af2d-1f116c4b1c83
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: aecbb5ee94a4234d1a7768bdb6de2a33508b1e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-toodefine-workflows-and-coordinate-jobs"></a><span data-ttu-id="76adf-104">Hadoop으로 Oozie 코디네이터 시간 기반을 사용 하 여 HDInsight toodefine 워크플로에서 작업 및 작업</span><span class="sxs-lookup"><span data-stu-id="76adf-104">Use time-based Oozie coordinator with Hadoop in HDInsight toodefine workflows and coordinate jobs</span></span>
<span data-ttu-id="76adf-105">이 문서에서는 시간에 따라 toodefine 워크플로 및 코디네이터 및 tootrigger 코디네이터 작업 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-105">In this article, you'll learn how toodefine workflows and coordinators, and how tootrigger hello coordinator jobs, based on time.</span></span> <span data-ttu-id="76adf-106">통해 유용한 toogo는 [HDInsight 사용 하 여 Oozie] [ hdinsight-use-oozie] 이 문서를 읽기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-106">It is helpful toogo through [Use Oozie with HDInsight][hdinsight-use-oozie] before you read this article.</span></span> <span data-ttu-id="76adf-107">또한 tooOozie를 예약할 수도 있습니다 Azure 데이터 팩터리를 사용 하 여 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-107">In addition tooOozie, you can also schedule jobs using Azure Data Factory.</span></span> <span data-ttu-id="76adf-108">Azure Data Factory toolearn 참조 [Data Factory와 사용 하 여 Pig 및 Hive](../data-factory/data-factory-data-transformation-activities.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-108">toolearn Azure Data Factory, see [Use Pig and Hive with Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="76adf-109">이 문서를 사용하려면 Windows 기반 HDInsight 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-109">This article requires a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="76adf-110">Linux 기반 클러스터에서 시간을 기준으로 작업을 비롯 한 Oozie를 사용 하는 방법은 참조 하십시오. [Hadoop toodefine 및 Linux 기반 HDInsight에서 워크플로 실행을 사용 하 여 Oozie](hdinsight-use-oozie-linux-mac.md)</span><span class="sxs-lookup"><span data-stu-id="76adf-110">For information on using Oozie, including time-based jobs, on a Linux-based cluster, see [Use Oozie with Hadoop toodefine and run a workflow on Linux-based HDInsight](hdinsight-use-oozie-linux-mac.md)</span></span>

## <a name="what-is-oozie"></a><span data-ttu-id="76adf-111">Oozie 정의</span><span class="sxs-lookup"><span data-stu-id="76adf-111">What is Oozie</span></span>
<span data-ttu-id="76adf-112">Apache Oozie는 Hadoop 작업을 관리하는 워크플로/코디네이션 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-112">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="76adf-113">Hello Hadoop 스택와도 통합 되어 하 고 Apache MapReduce Apache Pig, Apache Hive, Sqoop Apache Hadoop 작업을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-113">It is integrated with hello Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="76adf-114">사용 되는 tooschedule 작업은 Java 프로그램 셸 스크립트와 같은 특정 tooa 시스템 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-114">It can also be used tooschedule jobs that are specific tooa system, such as Java programs or shell scripts.</span></span>

<span data-ttu-id="76adf-115">hello 다음 그림이 보여줍니다 hello 워크플로 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-115">hello following image shows hello workflow you will implement:</span></span>

![워크플로 다이어그램][img-workflow-diagram]

<span data-ttu-id="76adf-117">hello 워크플로 두 개의 작업이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-117">hello workflow contains two actions:</span></span>

1. <span data-ttu-id="76adf-118">하이브 작업 log4j 로그 파일에 HiveQL 스크립트 toocount hello 로그 수준 유형의 각 항목을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-118">A Hive action runs a HiveQL script toocount hello occurrences of each log-level type in a log4j log file.</span></span> <span data-ttu-id="76adf-119">예를 들어 [로그 수준] 필드 tooshow hello 유형 및 hello 심각도 포함 된 필드의 줄의 각 log4j 로그 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-119">Each log4j log consists of a line of fields that contains a [LOG LEVEL] field tooshow hello type and hello severity, for example:</span></span>

        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...

    <span data-ttu-id="76adf-120">hello 하이브 스크립트 출력은 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-120">hello Hive script output is similar to:</span></span>

        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4

    <span data-ttu-id="76adf-121">Hive에 대한 자세한 내용은 [HDInsight와 함께 Hive 사용][hdinsight-use-hive]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="76adf-121">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="76adf-122">Sqoop 작업 hello HiveQL 작업 출력 tooa 테이블을 Azure SQL 데이터베이스에서 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-122">A Sqoop action exports hello HiveQL action output tooa table in an Azure SQL database.</span></span> <span data-ttu-id="76adf-123">Sqoop에 대한 자세한 내용은 [HDInsight에서 Sqoop 사용][hdinsight-use-sqoop]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="76adf-123">For more information about Sqoop, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="76adf-124">HDInsight 클러스터에서 지원 되 Oozie 버전에 대 한 참조 [HDInsight에서 제공 하는 hello 클러스터 버전의 새로운 기능?] [hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="76adf-124">For supported Oozie versions on HDInsight clusters, see [What's new in hello cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="76adf-125">필수 조건</span><span class="sxs-lookup"><span data-stu-id="76adf-125">Prerequisites</span></span>
<span data-ttu-id="76adf-126">이 자습서를 시작 하기 전에 hello 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-126">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="76adf-127">**Azure PowerShell이 포함된 워크스테이션**.</span><span class="sxs-lookup"><span data-stu-id="76adf-127">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="76adf-128">Azure 서비스 관리자를 사용하여 HDInsight 리소스를 관리하는 Azure PowerShell 지원은 더 이상 **지원되지 않고** 2017년 1월 1일에 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-128">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span></span> <span data-ttu-id="76adf-129">Azure 리소스 관리자와 함께 작동 하는이 문서 사용 hello 새 HDInsight cmdlet의 hello 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-129">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="76adf-130">Hello 단계에 따라 [설치 Azure PowerShell을 구성 하 고](/powershell/azureps-cmdlets-docs) tooinstall hello 최신 버전의 Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="76adf-130">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="76adf-131">해당 필요 toobe Azure 리소스 관리자와 함께 작동 하는 toouse hello 새로운 cmdlet 수정 스크립트가 있는 경우, 참조 [HDInsight 클러스터에 대 한 마이그레이션 tooAzure 리소스 관리자 기반 개발 도구](hdinsight-hadoop-development-using-azure-resource-manager.md) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-131">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="76adf-132">**HDInsight 클러스터**.</span><span class="sxs-lookup"><span data-stu-id="76adf-132">**An HDInsight cluster**.</span></span> <span data-ttu-id="76adf-133">HDInsight 클러스터를 만드는 방법에 대한 자세한 내용은 [HDInsight 클러스터 만들기][hdinsight-provision] 또는 [HDInsight 시작][hdinsight-get-started]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="76adf-133">For information about creating an HDInsight cluster, see [Create HDInsight clusters][hdinsight-provision], or [Get started with HDInsight][hdinsight-get-started].</span></span> <span data-ttu-id="76adf-134">Hello 데이터 toogo hello 자습서를 통해 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-134">You will need hello following data toogo through hello tutorial:</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="76adf-135">클러스터 속성</span><span class="sxs-lookup"><span data-stu-id="76adf-135">Cluster property</span></span></th><th><span data-ttu-id="76adf-136">Windows PowerShell 변수 이름</span><span class="sxs-lookup"><span data-stu-id="76adf-136">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="76adf-137">값</span><span class="sxs-lookup"><span data-stu-id="76adf-137">Value</span></span></th><th><span data-ttu-id="76adf-138">설명</span><span class="sxs-lookup"><span data-stu-id="76adf-138">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="76adf-139">HDInsight 클러스터 이름</span><span class="sxs-lookup"><span data-stu-id="76adf-139">HDInsight cluster name</span></span></td><td><span data-ttu-id="76adf-140">$clusterName</span><span class="sxs-lookup"><span data-stu-id="76adf-140">$clusterName</span></span></td><td></td><td><span data-ttu-id="76adf-141">hello HDInsight 클러스터는이 자습서를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-141">hello HDInsight cluster on which you will run this tutorial.</span></span></td></tr>
    <tr><td><span data-ttu-id="76adf-142">HDInsight 클러스터 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="76adf-142">HDInsight cluster username</span></span></td><td><span data-ttu-id="76adf-143">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="76adf-143">$clusterUsername</span></span></td><td></td><td><span data-ttu-id="76adf-144">hello HDInsight 클러스터 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-144">hello HDInsight cluster user name.</span></span> </td></tr>
    <tr><td><span data-ttu-id="76adf-145">HDInsight 클러스터 사용자 암호</span><span class="sxs-lookup"><span data-stu-id="76adf-145">HDInsight cluster user password</span></span> </td><td><span data-ttu-id="76adf-146">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="76adf-146">$clusterPassword</span></span></td><td></td><td><span data-ttu-id="76adf-147">hello HDInsight 클러스터 사용자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-147">hello HDInsight cluster user password.</span></span></td></tr>
    <tr><td><span data-ttu-id="76adf-148">Azure 저장소 계정 이름</span><span class="sxs-lookup"><span data-stu-id="76adf-148">Azure storage account name</span></span></td><td><span data-ttu-id="76adf-149">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="76adf-149">$storageAccountName</span></span></td><td></td><td><span data-ttu-id="76adf-150">Azure 저장소 계정 사용할 수 있는 toohello HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-150">An Azure Storage account available toohello HDInsight cluster.</span></span> <span data-ttu-id="76adf-151">이 자습서에 대 한 hello 클러스터 프로 비전 프로세스 중에 지정한 hello 기본 저장소 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-151">For this tutorial, use hello default storage account that you specified during hello cluster provision process.</span></span></td></tr>
    <tr><td><span data-ttu-id="76adf-152">Azure Blob 컨테이너 이름</span><span class="sxs-lookup"><span data-stu-id="76adf-152">Azure Blob container name</span></span></td><td><span data-ttu-id="76adf-153">$containerName</span><span class="sxs-lookup"><span data-stu-id="76adf-153">$containerName</span></span></td><td></td><td><span data-ttu-id="76adf-154">예를 들어 hello 기본 HDInsight 클러스터 파일 시스템에 사용 되는 hello Azure Blob 저장소 컨테이너를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-154">For this example, use hello Azure Blob storage container that is used for hello default HDInsight cluster file system.</span></span> <span data-ttu-id="76adf-155">기본적으로 hello hello HDInsight 클러스터와 동일한 이름을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-155">By default, it has hello same name as hello HDInsight cluster.</span></span></td></tr>
    </table><span data-ttu-id="76adf-156">
* **Azure SQL 데이터베이스**입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-156">
* **An Azure SQL database**.</span></span> <span data-ttu-id="76adf-157">워크스테이션에서 SQL 데이터베이스 서버 tooallow 액세스 hello에 대 한 방화벽 규칙을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-157">You must configure a firewall rule for hello SQL Database server tooallow access from your workstation.</span></span> <span data-ttu-id="76adf-158">Azure SQL 데이터베이스를 만들고 hello 방화벽을 구성 하는 방법에 대 한 지침은 [처음 사용 하는 Azure SQL 데이터베이스] [sql 데이터베이스-started].</span><span class="sxs-lookup"><span data-stu-id="76adf-158">For instructions about creating an Azure SQL database and configuring hello firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> <span data-ttu-id="76adf-159">이 문서에서는이 자습서에 필요한 hello Azure SQL 데이터베이스 테이블을 만들기 위한 Windows PowerShell 스크립트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-159">This article provides a Windows PowerShell script for creating hello Azure SQL database table that you need for this tutorial.</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="76adf-160">SQL 데이터베이스 속성</span><span class="sxs-lookup"><span data-stu-id="76adf-160">SQL database property</span></span></th><th><span data-ttu-id="76adf-161">Windows PowerShell 변수 이름</span><span class="sxs-lookup"><span data-stu-id="76adf-161">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="76adf-162">값</span><span class="sxs-lookup"><span data-stu-id="76adf-162">Value</span></span></th><th><span data-ttu-id="76adf-163">설명</span><span class="sxs-lookup"><span data-stu-id="76adf-163">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="76adf-164">SQL 데이터베이스 서버 이름</span><span class="sxs-lookup"><span data-stu-id="76adf-164">SQL database server name</span></span></td><td><span data-ttu-id="76adf-165">$sqlDatabaseServer</span><span class="sxs-lookup"><span data-stu-id="76adf-165">$sqlDatabaseServer</span></span></td><td></td><td><span data-ttu-id="76adf-166">hello SQL 데이터베이스 서버 toowhich Sqoop는 데이터를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-166">hello SQL database server toowhich Sqoop will export data.</span></span> </td></tr>
    <tr><td><span data-ttu-id="76adf-167">SQL 데이터베이스 로그인 이름</span><span class="sxs-lookup"><span data-stu-id="76adf-167">SQL database login name</span></span></td><td><span data-ttu-id="76adf-168">$sqlDatabaseLogin</span><span class="sxs-lookup"><span data-stu-id="76adf-168">$sqlDatabaseLogin</span></span></td><td></td><td><span data-ttu-id="76adf-169">SQL 데이터베이스 로그인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-169">SQL Database login name.</span></span></td></tr>
    <tr><td><span data-ttu-id="76adf-170">SQL 데이터베이스 로그인 암호</span><span class="sxs-lookup"><span data-stu-id="76adf-170">SQL database login password</span></span></td><td><span data-ttu-id="76adf-171">$sqlDatabaseLoginPassword</span><span class="sxs-lookup"><span data-stu-id="76adf-171">$sqlDatabaseLoginPassword</span></span></td><td></td><td><span data-ttu-id="76adf-172">SQL 데이터베이스 로그인 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-172">SQL Database login password.</span></span></td></tr>
    <tr><td><span data-ttu-id="76adf-173">SQL 데이터베이스 이름</span><span class="sxs-lookup"><span data-stu-id="76adf-173">SQL database name</span></span></td><td><span data-ttu-id="76adf-174">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="76adf-174">$sqlDatabaseName</span></span></td><td></td><td><span data-ttu-id="76adf-175">hello Azure SQL 데이터베이스 toowhich Sqoop는 데이터를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-175">hello Azure SQL database toowhich Sqoop will export data.</span></span> </td></tr>
    </table>

  > [!NOTE]
  > <span data-ttu-id="76adf-176">기본적으로 Azure SQL 데이터베이스는 Azure HDInsight 같은 Azure 서비스로부터의 연결을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-176">By default an Azure SQL database allows connections from Azure Services, such as Azure HDInsight.</span></span> <span data-ttu-id="76adf-177">이 방화벽 설정을 사용 하지 않으면 hello Azure 포털에서에서 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-177">If this firewall setting is disabled, you must enable it from hello Azure Portal.</span></span> <span data-ttu-id="76adf-178">SQL Database 만들기 및 방화벽 규칙 구성에 대한 지침은 [SQL Database 만들기 및 구성][sqldatabase-get-started]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="76adf-178">For instruction about creating a SQL Database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-get-started].</span></span>

> [!NOTE]
> <span data-ttu-id="76adf-179">Hello 테이블의 채우기 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-179">Fill-in hello values in hello tables.</span></span> <span data-ttu-id="76adf-180">이 자습서를 완료하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-180">It will be helpful for going through this tutorial.</span></span>

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a><span data-ttu-id="76adf-181">Oozie 워크플로 정의 및 hello 관련 HiveQL 스크립트</span><span class="sxs-lookup"><span data-stu-id="76adf-181">Define Oozie workflow and hello related HiveQL script</span></span>
<span data-ttu-id="76adf-182">Oozie 워크플로 정의는 hPDL(XML 프로세스 정의 언어)로 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-182">Oozie workflows definitions are written in hPDL (an XML process definition language).</span></span> <span data-ttu-id="76adf-183">hello 기본 워크플로 파일 이름은 *workflow.xml*합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-183">hello default workflow file name is *workflow.xml*.</span></span>  <span data-ttu-id="76adf-184">다음 배포 toohello HDInsight 클러스터가이 자습서의 뒷부분에 나오는 Azure PowerShell을 사용 하 여 쿼리하고 hello 워크플로 파일을 로컬로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-184">You will save hello workflow file locally, and then deploy it toohello HDInsight cluster by using Azure PowerShell later in this tutorial.</span></span>

<span data-ttu-id="76adf-185">HiveQL 스크립트 파일을 호출 하는 hello hello 워크플로에서 하이브 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-185">hello Hive action in hello workflow calls a HiveQL script file.</span></span> <span data-ttu-id="76adf-186">이 스크립트 파일에는 세 개의 HiveQL 문이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-186">This script file contains three HiveQL statements:</span></span>

1. <span data-ttu-id="76adf-187">**DROP TABLE 문 hello** 있는 경우 삭제 hello log4j Hive 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-187">**hello DROP TABLE statement** deletes hello log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="76adf-188">**CREATE TABLE 문 hello** log4j Hive 외부 테이블 hello log4j 로그 파일의 toohello 위치를 가리키는 만듭니다</span><span class="sxs-lookup"><span data-stu-id="76adf-188">**hello CREATE TABLE statement** creates a log4j Hive external table, which points toohello location of hello log4j log file;</span></span>
3. <span data-ttu-id="76adf-189">**hello log4j 로그 파일의 위치를 hello**합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-189">**hello location of hello log4j log file**.</span></span> <span data-ttu-id="76adf-190">hello 필드 구분 기호는 ",".</span><span class="sxs-lookup"><span data-stu-id="76adf-190">hello field delimiter is ",".</span></span> <span data-ttu-id="76adf-191">hello 기본 줄 구분은 "\n"입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-191">hello default line delimiter is "\n".</span></span> <span data-ttu-id="76adf-192">하이브 외부 테이블 toorun hello Oozie 워크플로 여러 번을 원하는 경우에 hello 원래 위치에서 제거 되 고 사용 되는 tooavoid hello 데이터 파일은.</span><span class="sxs-lookup"><span data-stu-id="76adf-192">A Hive external table is used tooavoid hello data file being removed from hello original location, in case you want toorun hello Oozie workflow multiple times.</span></span>
4. <span data-ttu-id="76adf-193">**hello 덮어쓰기 삽입 문** 에서 각 로그 수준 형식의 hello 발생 수를 세 log4j Hive 테이블 hello와 hello 출력 tooan Azure Blob 저장소 위치를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-193">**hello INSERT OVERWRITE statement** counts hello occurrences of each log-level type from hello log4j Hive table, and it saves hello output tooan Azure Blob storage location.</span></span>

> [!NOTE]
> <span data-ttu-id="76adf-194">알려진 Hive 경로 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-194">There is a known Hive path issue.</span></span> <span data-ttu-id="76adf-195">Oozie 작업을 제출할 때 이 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-195">You will run into this problem when submitting an Oozie job.</span></span> <span data-ttu-id="76adf-196">hello TechNet Wiki에서 확인할 수 있습니다 hello 문제 해결에 대 한 지침을 hello: [HDInsight Hive 오류: 수 없습니다 toorename][technetwiki-hive-error]합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-196">hello instructions for fixing hello issue can be found on hello TechNet Wiki: [HDInsight Hive error: Unable toorename][technetwiki-hive-error].</span></span>

<span data-ttu-id="76adf-197">**toodefine hello HiveQL 스크립트 파일 toobe hello 워크플로 통해 호출**</span><span class="sxs-lookup"><span data-stu-id="76adf-197">**toodefine hello HiveQL script file toobe called by hello workflow**</span></span>

1. <span data-ttu-id="76adf-198">콘텐츠를 수행 하는 hello로 텍스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-198">Create a text file with hello following content:</span></span>

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    <span data-ttu-id="76adf-199">Hello 스크립트에 사용 되는 세 개의 변수 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-199">There are three variables used in hello script:</span></span>

   * <span data-ttu-id="76adf-200">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="76adf-200">${hiveTableName}</span></span>
   * <span data-ttu-id="76adf-201">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="76adf-201">${hiveDataFolder}</span></span>
   * <span data-ttu-id="76adf-202">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="76adf-202">${hiveOutputFolder}</span></span>

     <span data-ttu-id="76adf-203">hello 워크플로 정의 파일 (이 자습서에서는 workflow.xml)는 런타임 시 이러한 값 toothis HiveQL 스크립트를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-203">hello workflow definition file (workflow.xml in this tutorial) will pass these values toothis HiveQL script at run time.</span></span>
2. <span data-ttu-id="76adf-204">Hello 파일으로 저장 **C:\Tutorials\UseOozie\useooziewf.hql** ANSI (ASCII) 인코딩을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-204">Save hello file as **C:\Tutorials\UseOozie\useooziewf.hql** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="76adf-205">(텍스트 편집기에서 이 옵션을 제공하지 않는 경우 메모장을 사용하세요.) 이 스크립트 파일에는 hello 자습서의 뒷부분에 나오는 배포 toohello HDInsight 클러스터 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-205">(Use Notepad if your text editor doesn't provide this option.) This script file will be deployed toohello HDInsight cluster later in hello tutorial.</span></span>

<span data-ttu-id="76adf-206">**toodefine 워크플로**</span><span class="sxs-lookup"><span data-stu-id="76adf-206">**toodefine a workflow**</span></span>

1. <span data-ttu-id="76adf-207">콘텐츠를 수행 하는 hello로 텍스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-207">Create a text file with hello following content:</span></span>

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start too= "RunHiveScript"/>

        <action name="RunHiveScript">
            <hive xmlns="uri:oozie:hive-action:0.2">
                <job-tracker>${jobTracker}</job-tracker>
                <name-node>${nameNode}</name-node>
                <configuration>
                    <property>
                        <name>mapred.job.queue.name</name>
                        <value>${queueName}</value>
                    </property>
                </configuration>
                <script>${hiveScript}</script>
                <param>hiveTableName=${hiveTableName}</param>
                <param>hiveDataFolder=${hiveDataFolder}</param>
                <param>hiveOutputFolder=${hiveOutputFolder}</param>
            </hive>
            <ok to="RunSqoopExport"/>
            <error to="fail"/>
        </action>

        <action name="RunSqoopExport">
            <sqoop xmlns="uri:oozie:sqoop-action:0.2">
                <job-tracker>${jobTracker}</job-tracker>
                <name-node>${nameNode}</name-node>
                <configuration>
                    <property>
                        <name>mapred.compress.map.output</name>
                        <value>true</value>
                    </property>
                </configuration>
            <arg>export</arg>
            <arg>--connect</arg>
            <arg>${sqlDatabaseConnectionString}</arg>
            <arg>--table</arg>
            <arg>${sqlDatabaseTableName}</arg>
            <arg>--export-dir</arg>
            <arg>${hiveOutputFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\001"</arg>
            </sqoop>
            <ok to="end"/>
            <error to="fail"/>
        </action>

        <kill name="fail">
            <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>

        <end name="end"/>
    </workflow-app>
    ```

    <span data-ttu-id="76adf-208">Hello 워크플로에 정의 된 두 가지 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-208">There are two actions defined in hello workflow.</span></span> <span data-ttu-id="76adf-209">hello 시작 tooaction은 *RunHiveScript*합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-209">hello start-tooaction is *RunHiveScript*.</span></span> <span data-ttu-id="76adf-210">Hello 매크로 함수를 실행 하는 경우 *확인*, hello 다음 작업은 *RunSqoopExport*합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-210">If hello action runs *OK*, hello next action is *RunSqoopExport*.</span></span>

    <span data-ttu-id="76adf-211">hello RunHiveScript는 여러 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-211">hello RunHiveScript has several variables.</span></span> <span data-ttu-id="76adf-212">Azure PowerShell을 사용 하 여 워크스테이션에서 hello Oozie 작업을 제출 하는 경우에 hello 값을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-212">You will pass hello values when you submit hello Oozie job from your workstation by using Azure PowerShell.</span></span>

    <span data-ttu-id="76adf-213">워크플로 변수</span><span class="sxs-lookup"><span data-stu-id="76adf-213">Workflow variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="76adf-214">워크플로 변수</span><span class="sxs-lookup"><span data-stu-id="76adf-214">Workflow variables</span></span></th><th><span data-ttu-id="76adf-215">설명</span><span class="sxs-lookup"><span data-stu-id="76adf-215">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="76adf-216">${jobTracker}</span><span class="sxs-lookup"><span data-stu-id="76adf-216">${jobTracker}</span></span></td><td><span data-ttu-id="76adf-217">Hello Hadoop 작업 트래커의 hello URL을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-217">Specify hello URL of hello Hadoop job tracker.</span></span> <span data-ttu-id="76adf-218">HDInsight 클러스터 버전 3.0 및 2.0에는 <strong>jobtrackerhost:9010</strong>을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-218">Use <strong>jobtrackerhost:9010</strong> on HDInsight cluster version 3.0 and 2.0.</span></span></td></tr>
    <tr><td><span data-ttu-id="76adf-219">${nameNode}</span><span class="sxs-lookup"><span data-stu-id="76adf-219">${nameNode}</span></span></td><td><span data-ttu-id="76adf-220">Hello Hadoop 이름 노드의 hello URL을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-220">Specify hello URL of hello Hadoop name node.</span></span> <span data-ttu-id="76adf-221">기본 파일 시스템 wasb hello를 사용 하 여: / / 주소, 예를 들어 <i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;. blob.core.windows.net</i>합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-221">Use hello default file system wasb:// address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
    <tr><td><span data-ttu-id="76adf-222">${queueName}</span><span class="sxs-lookup"><span data-stu-id="76adf-222">${queueName}</span></span></td><td><span data-ttu-id="76adf-223">에 제출할 작업 hello hello 큐 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-223">Specifies hello queue name that hello job will be submitted to.</span></span> <span data-ttu-id="76adf-224"><strong>기본값</strong>을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-224">Use <strong>default</strong>.</span></span></td></tr>
    </table>

    <span data-ttu-id="76adf-225">Hive 작업 변수</span><span class="sxs-lookup"><span data-stu-id="76adf-225">Hive action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="76adf-226">Hive 작업 변수</span><span class="sxs-lookup"><span data-stu-id="76adf-226">Hive action variable</span></span></th><th><span data-ttu-id="76adf-227">설명</span><span class="sxs-lookup"><span data-stu-id="76adf-227">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="76adf-228">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="76adf-228">${hiveDataFolder}</span></span></td><td><span data-ttu-id="76adf-229">Create Table 하이브 명령 hello에 대 한 hello 소스 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-229">hello source directory for hello Hive Create Table command.</span></span></td></tr>
    <tr><td><span data-ttu-id="76adf-230">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="76adf-230">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="76adf-231">hello 덮어쓰기 삽입 문 hello에 대 한 출력 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-231">hello output folder for hello INSERT OVERWRITE statement.</span></span></td></tr>
    <tr><td><span data-ttu-id="76adf-232">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="76adf-232">${hiveTableName}</span></span></td><td><span data-ttu-id="76adf-233">hello log4j 데이터 파일을 참조 하는 hello Hive 테이블의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-233">hello name of hello Hive table that references hello log4j data files.</span></span></td></tr>
    </table>

    <span data-ttu-id="76adf-234">Sqoop 작업 변수</span><span class="sxs-lookup"><span data-stu-id="76adf-234">Sqoop action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="76adf-235">Sqoop 작업 변수</span><span class="sxs-lookup"><span data-stu-id="76adf-235">Sqoop action variable</span></span></th><th><span data-ttu-id="76adf-236">설명</span><span class="sxs-lookup"><span data-stu-id="76adf-236">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="76adf-237">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="76adf-237">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="76adf-238">SQL 데이터베이스 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-238">SQL Database connection string.</span></span></td></tr>
    <tr><td><span data-ttu-id="76adf-239">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="76adf-239">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="76adf-240">hello Azure SQL 데이터베이스 테이블 toowhere hello 데이터를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-240">hello Azure SQL database table toowhere hello data will be exported.</span></span></td></tr>
    <tr><td><span data-ttu-id="76adf-241">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="76adf-241">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="76adf-242">하이브 덮어쓰기 삽입 문 hello에 대 한 hello 출력 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-242">hello output folder for hello Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="76adf-243">이 hello hello Sqoop 내보내기 (내보내기-dir)에 대 한 같은 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-243">This is hello same folder for hello Sqoop export (export-dir).</span></span></td></tr>
    </table>

    <span data-ttu-id="76adf-244">Oozie 워크플로 및 hello 워크플로 동작을 사용 하는 방법에 대 한 자세한 내용은 참조 [Apache Oozie 4.0 설명서] [ apache-oozie-400] (버전에 대 한 HDInsight 클러스터 3.0) 또는 [Apache Oozie 3.3.2 설명서] [ apache-oozie-332] (버전에 대 한 HDInsight 클러스터 2.1).</span><span class="sxs-lookup"><span data-stu-id="76adf-244">For more information about Oozie workflow and using hello workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

1. <span data-ttu-id="76adf-245">Hello 파일으로 저장 **C:\Tutorials\UseOozie\workflow.xml** ANSI (ASCII) 인코딩을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-245">Save hello file as **C:\Tutorials\UseOozie\workflow.xml** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="76adf-246">(텍스트 편집기에서 이 옵션을 제공하지 않는 경우 메모장을 사용하세요.)</span><span class="sxs-lookup"><span data-stu-id="76adf-246">(Use Notepad if your text editor doesn't provide this option.)</span></span>

<span data-ttu-id="76adf-247">**toodefine 코디네이터**</span><span class="sxs-lookup"><span data-stu-id="76adf-247">**toodefine coordinator**</span></span>

1. <span data-ttu-id="76adf-248">콘텐츠를 수행 하는 hello로 텍스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-248">Create a text file with hello following content:</span></span>

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    <span data-ttu-id="76adf-249">Hello 정의 파일에 사용 되는 다섯 개의 변수 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-249">There are five variables used in hello definition file:</span></span>

   | <span data-ttu-id="76adf-250">변수</span><span class="sxs-lookup"><span data-stu-id="76adf-250">Variable</span></span> | <span data-ttu-id="76adf-251">설명</span><span class="sxs-lookup"><span data-stu-id="76adf-251">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="76adf-252">${coordFrequency}</span><span class="sxs-lookup"><span data-stu-id="76adf-252">${coordFrequency}</span></span> |<span data-ttu-id="76adf-253">작업 일시 중지 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-253">Job pause time.</span></span> <span data-ttu-id="76adf-254">빈도는 항상 분 단위로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-254">Frequency is always expressed in minutes.</span></span> |
   | <span data-ttu-id="76adf-255">${coordStart}</span><span class="sxs-lookup"><span data-stu-id="76adf-255">${coordStart}</span></span> |<span data-ttu-id="76adf-256">작업 시작 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-256">Job start time.</span></span> |
   | <span data-ttu-id="76adf-257">${coordEnd}</span><span class="sxs-lookup"><span data-stu-id="76adf-257">${coordEnd}</span></span> |<span data-ttu-id="76adf-258">작업 종료 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-258">Job end time.</span></span> |
   | <span data-ttu-id="76adf-259">${coordTimezone}</span><span class="sxs-lookup"><span data-stu-id="76adf-259">${coordTimezone}</span></span> |<span data-ttu-id="76adf-260">Oozie는 일광 절약 시간제(UTC를 사용하여 일반적으로 표시 됨)없이 고정된 시간대에서 코디네이터 작업을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-260">Oozie processes coordinator jobs in a fixed time zone with no daylight saving time (typically represented by using UTC).</span></span> <span data-ttu-id="76adf-261">이 표준 시간대 hello "Oozie 처리 표준 시간대입니다." 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-261">This time zone is referred as hello "Oozie processing timezone."</span></span> |
   | <span data-ttu-id="76adf-262">${wfPath}</span><span class="sxs-lookup"><span data-stu-id="76adf-262">${wfPath}</span></span> |<span data-ttu-id="76adf-263">hello workflow.xml에 대 한 hello 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-263">hello path for hello workflow.xml.</span></span>  <span data-ttu-id="76adf-264">Hello 워크플로 파일 이름을 hello 기본 파일 이름 (workflow.xml) 없는 경우에 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-264">If hello workflow file name is not hello default file name (workflow.xml), you must specify it.</span></span> |
2. <span data-ttu-id="76adf-265">Hello 파일으로 저장 **C:\Tutorials\UseOozie\coordinator.xml** hello ANSI (ASCII) 인코딩을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-265">Save hello file as **C:\Tutorials\UseOozie\coordinator.xml** by using hello ANSI (ASCII) encoding.</span></span> <span data-ttu-id="76adf-266">(텍스트 편집기에서 이 옵션을 제공하지 않는 경우 메모장을 사용하세요.)</span><span class="sxs-lookup"><span data-stu-id="76adf-266">(Use Notepad if your text editor doesn't provide this option.)</span></span>

## <a name="deploy-hello-oozie-project-and-prepare-hello-tutorial"></a><span data-ttu-id="76adf-267">Hello Oozie 프로젝트를 배포 하 고 hello 자습서 준비</span><span class="sxs-lookup"><span data-stu-id="76adf-267">Deploy hello Oozie project and prepare hello tutorial</span></span>
<span data-ttu-id="76adf-268">Azure PowerShell 스크립트 tooperform hello 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-268">You will run an Azure PowerShell script tooperform hello following:</span></span>

* <span data-ttu-id="76adf-269">복사 hello HiveQL 스크립트 (useoozie.hql) tooAzure Blob 저장소, wasb:///tutorials/useoozie/useoozie.hql 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-269">Copy hello HiveQL script (useoozie.hql) tooAzure Blob storage, wasb:///tutorials/useoozie/useoozie.hql.</span></span>
* <span data-ttu-id="76adf-270">Workflow.xml toowasb:///tutorials/useoozie/workflow.xml를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-270">Copy workflow.xml toowasb:///tutorials/useoozie/workflow.xml.</span></span>
* <span data-ttu-id="76adf-271">Coordinator.xml toowasb:///tutorials/useoozie/coordinator.xml를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-271">Copy coordinator.xml toowasb:///tutorials/useoozie/coordinator.xml.</span></span>
* <span data-ttu-id="76adf-272">복사 hello 데이터 파일 (/ example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-272">Copy hello data file (/example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span></span>
* <span data-ttu-id="76adf-273">Sqoop 내보내기 데이터를 저장할 Azure SQL 데이터베이스 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-273">Create an Azure SQL database table for storing Sqoop export data.</span></span> <span data-ttu-id="76adf-274">hello 테이블 이름이 *log4jLogCount*합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-274">hello table name is *log4jLogCount*.</span></span>

<span data-ttu-id="76adf-275">**HDInsight 저장소 이해**</span><span class="sxs-lookup"><span data-stu-id="76adf-275">**Understand HDInsight storage**</span></span>

<span data-ttu-id="76adf-276">HDInsight는 데이터 저장소로 Azure Blob 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-276">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="76adf-277">wasb: / /는 Microsoft의 Azure Blob 저장소에 hello distributed Hadoop 파일 시스템 (HDFS)의 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-277">wasb:// is Microsoft's implementation of hello Hadoop distributed file system (HDFS) in Azure Blob storage.</span></span> <span data-ttu-id="76adf-278">자세한 내용은 [HDInsight와 함께 Azure Blob Storage 사용][hdinsight-storage]을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="76adf-278">For more information, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="76adf-279">HDInsight 클러스터를 프로 비전 할 때 Azure Blob 저장소 계정과 해당 계정에서 특정 컨테이너로 지정 됩니다 hello 기본 파일 시스템으로 같은 HDFS.</span><span class="sxs-lookup"><span data-stu-id="76adf-279">When you provision an HDInsight cluster, an Azure Blob storage account and a specific container from that account is designated as hello default file system, like in HDFS.</span></span> <span data-ttu-id="76adf-280">또한 toothis 저장소 계정을 추가할 수 있습니다 hello에서 추가 저장소 계정을 동일한 Azure 구독 또는 hello 프로 비전 프로세스 중 각기 다른 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="76adf-280">In addition toothis storage account, you can add additional storage accounts from hello same Azure subscription or from different Azure subscriptions during hello provisioning process.</span></span> <span data-ttu-id="76adf-281">저장소 계정 추가에 대한 지침은 [HDInsight 클러스터 프로비전][hdinsight-provision]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="76adf-281">For instructions about adding additional storage accounts, see [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="76adf-282">이 자습서에 사용 된 toosimplify hello Azure PowerShell 스크립트를 모두 hello 파일이 hello 기본 파일 시스템 컨테이너에 저장 된 위치에 */자습서/useoozie*합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-282">toosimplify hello Azure PowerShell script used in this tutorial, all of hello files are stored in hello default file system container located at */tutorials/useoozie*.</span></span> <span data-ttu-id="76adf-283">기본적으로이 컨테이너는 hello HDInsight 클러스터 이름을 이름이 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-283">By default, this container has hello same name as hello HDInsight cluster name.</span></span>
<span data-ttu-id="76adf-284">hello 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-284">hello syntax is:</span></span>

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> <span data-ttu-id="76adf-285">Hello만 *wasb: / /* 구문을 HDInsight 클러스터 버전 3.0에서에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-285">Only hello *wasb://* syntax is supported in HDInsight cluster version 3.0.</span></span> <span data-ttu-id="76adf-286">이전 hello *asv: / /* 구문을 HDInsight 2.1와 1.6 클러스터에서 사용할 수 있지만 3.0 HDInsight 클러스터에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-286">hello older *asv://* syntax is supported in HDInsight 2.1 and 1.6 clusters, but it is not supported in HDInsight 3.0 clusters.</span></span>
>
> <span data-ttu-id="76adf-287">wasb hello: / / 경로 가상 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-287">hello wasb:// path is a virtual path.</span></span> <span data-ttu-id="76adf-288">자세한 내용은 [HDInsight와 함께 Azure Blob Storage 사용][hdinsight-storage]을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="76adf-288">For more information see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="76adf-289">Hello 기본 파일 시스템 컨테이너에 저장 된 파일의 Uri (사용 하 고 workflow.xml 예를 들어)를 수행 하는 hello를 사용 하 여 HDInsight에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-289">A file that is stored in hello default file system container can be accessed from HDInsight by using any of hello following URIs (I am using workflow.xml as an example):</span></span>

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

<span data-ttu-id="76adf-290">Hello 저장소 계정에서 직접 tooaccess hello 파일을 원하는 경우 hello blob hello 파일에 대 한 이름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-290">If you want tooaccess hello file directly from hello storage account, hello blob name for hello file is:</span></span>

    tutorials/useoozie/workflow.xml

<span data-ttu-id="76adf-291">**Hive 내부 테이블 및 외부 테이블 이해**</span><span class="sxs-lookup"><span data-stu-id="76adf-291">**Understand Hive internal and external tables**</span></span>

<span data-ttu-id="76adf-292">몇 가지 방법으로 하이브 내부 및 외부 테이블에 대 한 tooknow 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-292">There are a few things you need tooknow about Hive internal and external tables:</span></span>

* <span data-ttu-id="76adf-293">CREATE TABLE 명령을 hello를 내부 테이블에는 관리 되는 테이블이 라고도 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-293">hello CREATE TABLE command creates an internal table, also known as a managed table.</span></span> <span data-ttu-id="76adf-294">hello 기본 컨테이너에서 hello 데이터 파일이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-294">hello data file must be located in hello default container.</span></span>
* <span data-ttu-id="76adf-295">CREATE TABLE 명령을 hello hello 데이터 toohello 파일/hive/웨어하우스/이동<TableName> hello 기본 컨테이너의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-295">hello CREATE TABLE command moves hello data file toohello /hive/warehouse/<TableName> folder in hello default container.</span></span>
* <span data-ttu-id="76adf-296">CREATE EXTERNAL TABLE 명령 hello 외부 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-296">hello CREATE EXTERNAL TABLE command creates an external table.</span></span> <span data-ttu-id="76adf-297">hello 기본 컨테이너 외부 hello 데이터 파일이 위치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-297">hello data file can be located outside hello default container.</span></span>
* <span data-ttu-id="76adf-298">CREATE EXTERNAL TABLE 명령 hello hello 데이터 파일을 이동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-298">hello CREATE EXTERNAL TABLE command does not move hello data file.</span></span>
* <span data-ttu-id="76adf-299">CREATE EXTERNAL TABLE 명령 hello hello 위치 절에 지정 된 hello 폴더 아래의 하위 폴더도 모두를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-299">hello CREATE EXTERNAL TABLE command doesn't allow any subfolders under hello folder that is specified in hello LOCATION clause.</span></span> <span data-ttu-id="76adf-300">이 hello 자습서 hello sample.log 파일의 복사본을 만들어 하는 이유는 hello 이유.</span><span class="sxs-lookup"><span data-stu-id="76adf-300">This is hello reason why hello tutorial makes a copy of hello sample.log file.</span></span>

<span data-ttu-id="76adf-301">자세한 내용은 [HDInsight: Hive 내부 및 외부 테이블 소개][cindygross-hive-tables]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="76adf-301">For more information, see [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables].</span></span>

<span data-ttu-id="76adf-302">**tooprepare hello 자습서**</span><span class="sxs-lookup"><span data-stu-id="76adf-302">**tooprepare hello tutorial**</span></span>

1. <span data-ttu-id="76adf-303">Windows PowerShell ISE 열기 hello (hello Windows 8 시작 화면에 입력 **PowerShell_ISE**, 클릭 하 고 **Windows PowerShell ISE**합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-303">Open hello Windows PowerShell ISE (in hello Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="76adf-304">자세한 내용은 [Windows 8 및 Windows에서 Windows PowerShell 시작][powershell-start]을 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="76adf-304">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="76adf-305">Hello 아래쪽 창에 명령 tooconnect tooyour Azure 구독을 다음 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-305">In hello bottom pane, run hello following command tooconnect tooyour Azure subscription:</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="76adf-306">하면 Azure 계정 자격 증명된 tooenter 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-306">You will be prompted tooenter your Azure account credentials.</span></span> <span data-ttu-id="76adf-307">이 메서드는 구독 연결을 추가 하는 시간이 초과 있으며, 12 시간 후 있습니다 toorun hello cmdlet 다시 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-307">This method of adding a subscription connection times out, and after 12 hours, you will have toorun hello cmdlet again.</span></span>

   > [!NOTE]
   > <span data-ttu-id="76adf-308">여러 Azure 구독이 있는 hello 기본 구독이 지원 되지 않으면 원하는 toouse hello 사용 하 여 hello <strong>Select-azuresubscription</strong> cmdlet tooselect 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-308">If you have multiple Azure subscriptions and hello default subscription is not hello one you want toouse, use hello <strong>Select-AzureSubscription</strong> cmdlet tooselect a subscription.</span></span>

3. <span data-ttu-id="76adf-309">Hello hello 스크립트 창에 스크립트를 다음 복사한 다음 hello 처음 여섯 개의 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-309">Copy hello following script into hello script pane, and then set hello first six variables:</span></span>

    ```powershell
    # WASB variables
    $storageAccountName = "<StorageAccountName>"
    $containerName = "<BlobStorageContainerName>"

    # SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    # Oozie files for hello tutorial
    $hiveQLScript = "C:\Tutorials\UseOozie\useooziewf.hql"
    $workflowDefinition = "C:\Tutorials\UseOozie\workflow.xml"
    $coordDefinition =  "C:\Tutorials\UseOozie\coordinator.xml"

    # WASB folder for storing hello Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use hello long path here
    ```

    <span data-ttu-id="76adf-310">참조 hello에 대 한 자세한 설명은 hello 변수, [필수 구성 요소](#prerequisites) 이 자습서의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-310">For more descriptions of hello variables, see hello [Prerequisites](#prerequisites) section in this tutorial.</span></span>

4. <span data-ttu-id="76adf-311">Hello toohello 스크립트 hello 스크립트 창에서 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-311">Append hello following toohello script in hello script pane:</span></span>

    ```powershell
    # Create a storage context object
    $storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

    function uploadOozieFiles()
    {
        Write-Host "Copy HiveQL script, workflow definition and coordinator definition ..." -ForegroundColor Green
        Set-AzureStorageBlobContent -File $hiveQLScript -Container $containerName -Blob "$destFolder/useooziewf.hql" -Context $destContext
        Set-AzureStorageBlobContent -File $workflowDefinition -Container $containerName -Blob "$destFolder/workflow.xml" -Context $destContext
        Set-AzureStorageBlobContent -File $coordDefinition -Container $containerName -Blob "$destFolder/coordinator.xml" -Context $destContext
    }

    function prepareHiveDataFile()
    {
        Write-Host "Make a copy of hello sample.log file ... " -ForegroundColor Green
        Start-CopyAzureStorageBlob -SrcContainer $containerName -SrcBlob "example/data/sample.log" -Context $destContext -DestContainer $containerName -destBlob "$destFolder/data/sample.log" -DestContext $destContext
    }

    function prepareSQLDatabase()
    {
        # SQL query string for creating log4jLogsCount table
        $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [Level] [nvarchar](10) NOT NULL,
                [Total] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
            [Level] ASC
            )
            )"

        #Create hello log4jLogsCount table
        Write-Host "Create Log4jLogsCount table ..." -ForegroundColor Green
        $conn = New-Object System.Data.SqlClient.SqlConnection
        $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
        $conn.open()
        $cmd = New-Object System.Data.SqlClient.SqlCommand
        $cmd.connection = $conn
        $cmd.commandtext = $cmdCreateLog4jCountTable
        $cmd.executenonquery()

        $conn.close()
    }

    # upload workflow.xml, coordinator.xml, and ooziewf.hql
    uploadOozieFiles;

    # make a copy of example/data/sample.log tooexample/data/log4j/sample.log
    prepareHiveDataFile;

    # create log4jlogsCount table on SQL database
    prepareSQLDatabase;
    ```

5. <span data-ttu-id="76adf-312">클릭 **스크립트 실행** 하거나 키를 눌러 **F5** toorun hello 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-312">Click **Run Script** or press **F5** toorun hello script.</span></span> <span data-ttu-id="76adf-313">hello 출력 비슷합니다 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-313">hello output will be similar to:</span></span>

    ![자습서 준비 출력][img-preparation-output]

## <a name="run-hello-oozie-project"></a><span data-ttu-id="76adf-315">Hello Oozie 프로젝트 실행</span><span class="sxs-lookup"><span data-stu-id="76adf-315">Run hello Oozie project</span></span>
<span data-ttu-id="76adf-316">Azure PowerShell은 Oozie 작업을 정의하는 데 현재 어떤 cmdlet도 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-316">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="76adf-317">Hello를 사용할 수 있습니다 **Invoke-restmethod** cmdlet tooinvoke Oozie 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-317">You can use hello **Invoke-RestMethod** cmdlet tooinvoke Oozie web services.</span></span> <span data-ttu-id="76adf-318">hello Oozie 웹 서비스 API는 HTTP 나머지 JSON API.</span><span class="sxs-lookup"><span data-stu-id="76adf-318">hello Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="76adf-319">Hello Oozie 웹 서비스 API에 대 한 자세한 내용은 참조 [Apache Oozie 4.0 설명서] [ apache-oozie-400] (버전에 대 한 HDInsight 클러스터 3.0) 또는 [Apache Oozie 3.3.2 설명서] [ apache-oozie-332] (버전에 대 한 HDInsight 클러스터 2.1).</span><span class="sxs-lookup"><span data-stu-id="76adf-319">For more information about hello Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

<span data-ttu-id="76adf-320">**toosubmit Oozie 작업**</span><span class="sxs-lookup"><span data-stu-id="76adf-320">**toosubmit an Oozie job**</span></span>

1. <span data-ttu-id="76adf-321">열기 hello Windows PowerShell ISE (Windows 8 시작 화면에 입력 **PowerShell_ISE**, 클릭 하 고 **Windows PowerShell ISE**합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-321">Open hello Windows PowerShell ISE (in Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="76adf-322">자세한 내용은 [Windows 8 및 Windows에서 Windows PowerShell 시작][powershell-start]을 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="76adf-322">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="76adf-323">그러나 복사 hello 다음 hello 스크립트 창으로 스크립팅 하 고 다음 집합 hello 먼저 14 개의 변수 (건너뛸 **$storageUri**).</span><span class="sxs-lookup"><span data-stu-id="76adf-323">Copy hello following script into hello script pane, and then set hello first fourteen variables (however, skip **$storageUri**).</span></span>

    ```powershell
    #HDInsight cluster variables
    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterUserPassword>"

    #Azure Blob storage (WASB) variables
    $storageAccountName = "<StorageAccountName>"
    $storageContainerName = "<BlobContainerName>"
    $storageUri="wasb://$storageContainerName@$storageAccountName.blob.core.windows.net"

    #Azure SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "<SQLDatabaseloginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"

    #Oozie WF/coordinator variables
    $coordStart = "2014-03-21T13:45Z"
    $coordEnd = "2014-03-21T13:45Z"
    $coordFrequency = "1440"    # in minutes, 24h x 60m = 1440m
    $coordTimezone = "UTC"    #UTC/GMT

    $oozieWFPath="$storageUri/tutorials/useoozie"  # hello default name is workflow.xml. And you don't need toospecify hello file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$sqlDatabaseServer.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServer;password=$sqlDatabaseLoginPassword;database=$sqlDatabaseName"
    $sqlDatabaseTableName = "log4jLogsCount"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)
    ```

    <span data-ttu-id="76adf-324">참조 hello에 대 한 자세한 설명은 hello 변수, [필수 구성 요소](#prerequisites) 이 자습서의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-324">For more descriptions of hello variables, see hello [Prerequisites](#prerequisites) section in this tutorial.</span></span>

    <span data-ttu-id="76adf-325">$coordstart 및 $coordend는 hello 워크플로 시작 및 종료 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-325">$coordstart and $coordend are hello workflow starting and ending time.</span></span> <span data-ttu-id="76adf-326">toofind hello UTC/GMT 시간 bing.com에 "utc 시간"을 검색 합니다. hello $coordFrequency toorun hello 워크플로에서 분 단위 빈도입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-326">toofind out hello UTC/GMT time, search "utc time" on bing.com. hello $coordFrequency is how often in minutes you want toorun hello workflow.</span></span>
3. <span data-ttu-id="76adf-327">Hello toohello 스크립트 다음에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-327">Append hello following toohello script.</span></span> <span data-ttu-id="76adf-328">이 부분 hello Oozie 페이로드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-328">This part defines hello Oozie payload:</span></span>

    ```powershell
    #OoziePayload used for Oozie web service submission
    $OoziePayload =  @"
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
            <name>nameNode</name>
            <value>$storageUrI</value>
        </property>

        <property>
            <name>jobTracker</name>
            <value>jobtrackerhost:9010</value>
        </property>

        <property>
            <name>queueName</name>
            <value>default</value>
        </property>

        <property>
            <name>oozie.use.system.libpath</name>
            <value>true</value>
        </property>

        <property>
            <name>oozie.coord.application.path</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>wfPath</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>coordStart</name>
            <value>$coordStart</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>$coordEnd</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>$coordFrequency</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>$coordTimezone</value>
        </property>

        <property>
            <name>hiveScript</name>
            <value>$hiveScript</value>
        </property>

        <property>
            <name>hiveTableName</name>
            <value>$hiveTableName</value>
        </property>

        <property>
            <name>hiveDataFolder</name>
            <value>$hiveDataFolder</value>
        </property>

        <property>
            <name>hiveOutputFolder</name>
            <value>$hiveOutputFolder</value>
        </property>

        <property>
            <name>sqlDatabaseConnectionString</name>
            <value>&quot;$sqlDatabaseConnectionString&quot;</value>
        </property>

        <property>
            <name>sqlDatabaseTableName</name>
            <value>$SQLDatabaseTableName</value>
        </property>

        <property>
            <name>user.name</name>
            <value>admin</value>
        </property>

    </configuration>
    "@
    ```

   > [!NOTE]
   > <span data-ttu-id="76adf-329">hello 주요한 차이점 비교 toohello 워크플로 제출 페이로드 파일은 hello 변수 **oozie.coord.application.path**합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-329">hello major difference compared toohello workflow submission payload file is hello variable **oozie.coord.application.path**.</span></span> <span data-ttu-id="76adf-330">워크플로 작업을 제출할 때는 대신 **oozie.wf.application.path** 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-330">When you submit a workflow job, you use **oozie.wf.application.path** instead.</span></span>

4. <span data-ttu-id="76adf-331">Hello toohello 스크립트 다음에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-331">Append hello following toohello script.</span></span> <span data-ttu-id="76adf-332">이 부분 hello Oozie 웹 서비스 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-332">This part checks hello Oozie web service status:</span></span>

    ```powershell
    function checkOozieServerStatus()
    {
        Write-Host "Checking Oozie server status..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/admin/status"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds -OutVariable $OozieServerStatus

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieServerSatus = $jsonResponse[0].("systemMode")
        Write-Host "Oozie server status is $oozieServerSatus..."

        if($oozieServerSatus -notmatch "NORMAL")
        {
            Write-Host "Oozie server status is $oozieServerSatus...cannot submit Oozie jobs. Check hello server status and re-run hello job."
            exit 1
        }
    }
    ```

5. <span data-ttu-id="76adf-333">Hello toohello 스크립트 다음에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-333">Append hello following toohello script.</span></span> <span data-ttu-id="76adf-334">이 부분은 Oozie 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-334">This part creates an Oozie job:</span></span>

    ```powershell
    function createOozieJob()
    {
        # create Oozie job
        Write-Host "Sending hello following Payload toohello cluster:" -ForegroundColor Green
        Write-Host "`n--------`n$OoziePayload`n--------"
        $clusterUriCreateJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $creds -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName -debug -Verbose

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieJobId = $jsonResponse[0].("id")
        Write-Host "Oozie job id is $oozieJobId..."

        return $oozieJobId
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="76adf-335">워크플로 작업을 전송 하면 hello 작업이 만들어진 후에 다른 웹 서비스 호출 toostart hello 작업을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-335">When you submit a workflow job, you must make another web service call toostart hello job after hello job is created.</span></span> <span data-ttu-id="76adf-336">이 경우 hello 코디네이터 작업 시간에 의해 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-336">In this case, hello coordinator job is triggered by time.</span></span> <span data-ttu-id="76adf-337">hello 작업이 자동으로 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-337">hello job will start automatically.</span></span>

6. <span data-ttu-id="76adf-338">Hello toohello 스크립트 다음에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-338">Append hello following toohello script.</span></span> <span data-ttu-id="76adf-339">이 부분 hello Oozie 작업 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-339">This part checks hello Oozie job status:</span></span>

    ```powershell
    function checkOozieJobStatus($oozieJobId)
    {
        # get job status
        Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until hello job metadata is populated in hello Oozie metastore..." -ForegroundColor Green
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

        Write-Host "Getting job status and waiting for hello job toocomplete..." -ForegroundColor Green
        $clusterUriGetJobStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")

        while($JobStatus -notmatch "SUCCEEDED|KILLED")
        {
            Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for hello job toocomplete..."
            Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
            $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
            $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
            $JobStatus = $jsonResponse[0].("status")
        }

        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!"
        if($JobStatus -notmatch "SUCCEEDED")
        {
            Write-Host "Check logs at http://headnode0:9014/cluster for detais."
            exit -1
        }
    }
    ```

7. <span data-ttu-id="76adf-340">(선택 사항) Hello toohello 스크립트 다음에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-340">(Optional) Append hello following toohello script.</span></span>

    ```powershell
    function listOozieJobs()
    {
        Write-Host "Listing Oozie jobs..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds

        write-host "Job ID                                   App Name        Status      Started                         Ended"
        write-host "----------------------------------------------------------------------------------------------------------------------------------"
        foreach($job in $response.workflows)
        {
            Write-Host $job.id "`t" $job.appName "`t" $job.status "`t" $job.startTime "`t" $job.endTime
        }
    }

    function ShowOozieJobLog($oozieJobId)
    {
        Write-Host "Showing Oozie job info..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/$oozieJobId" + "?show=log"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds
        write-host $response
    }

    function killOozieJob($oozieJobId)
    {
        Write-Host "Killing hello Oozie job $oozieJobId..." -ForegroundColor Green
        $clusterUriStartJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=kill" #Valid values for hello 'action' parameter are 'start', 'suspend', 'resume', 'kill', 'dryrun', 'rerun', and 'change'.
        $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $creds | Format-Table -HideTableHeaders -debug
    }
    ```

8. <span data-ttu-id="76adf-341">Hello toohello 스크립트에 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-341">Append hello following toohello script:</span></span>

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

    <span data-ttu-id="76adf-342">Toorun hello에 대 한 추가 기능을 원하는 경우 hello # 기호를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-342">Remove hello # signs if you want toorun hello additional functions.</span></span>
9. <span data-ttu-id="76adf-343">HDinsight 클러스터 버전이 2.1인 경우 "https://$clusterName.azurehdinsight.net:443/oozie/v2/"를 "https://$clusterName.azurehdinsight.net:443/oozie/v1/"로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-343">If your HDinsight cluster is version 2.1, replace "https://$clusterName.azurehdinsight.net:443/oozie/v2/" with "https://$clusterName.azurehdinsight.net:443/oozie/v1/".</span></span> <span data-ttu-id="76adf-344">HDInsight 클러스터 버전 2.1 지원의 버전이 아닌 2 hello 웹 서비스를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-344">HDInsight cluster version 2.1 does not supports version 2 of hello web services.</span></span>
10. <span data-ttu-id="76adf-345">클릭 **스크립트 실행** 하거나 키를 눌러 **F5** toorun hello 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-345">Click **Run Script** or press **F5** toorun hello script.</span></span> <span data-ttu-id="76adf-346">hello 출력 비슷합니다 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-346">hello output will be similar to:</span></span>

     ![자습서 실행 워크플로 출력][img-runworkflow-output]
11. <span data-ttu-id="76adf-348">Tooyour SQL 데이터베이스 toosee hello 내보낸 데이터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-348">Connect tooyour SQL Database toosee hello exported data.</span></span>

<span data-ttu-id="76adf-349">**toocheck hello 작업 오류 로그**</span><span class="sxs-lookup"><span data-stu-id="76adf-349">**toocheck hello job error log**</span></span>

<span data-ttu-id="76adf-350">워크플로 tootroubleshoot hello Oozie 로그 파일에 있습니다 C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log hello 클러스터 헤드 노드에에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-350">tootroubleshoot a workflow, hello Oozie log file can be found at C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log from hello cluster headnode.</span></span> <span data-ttu-id="76adf-351">RDP에 대 한 자세한 내용은 참조 [관리 HDInsight 클러스터를 사용 하 여 Azure 포털 hello][hdinsight-admin-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-351">For information on RDP, see [Administering HDInsight clusters using hello Azure portal][hdinsight-admin-portal].</span></span>

<span data-ttu-id="76adf-352">**toorerun hello 자습서**</span><span class="sxs-lookup"><span data-stu-id="76adf-352">**toorerun hello tutorial**</span></span>

<span data-ttu-id="76adf-353">toorerun hello 워크플로 hello 다음 작업을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-353">toorerun hello workflow, you must perform hello following tasks:</span></span>

* <span data-ttu-id="76adf-354">Hello 하이브 스크립트 출력 파일을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-354">Delete hello Hive script output file.</span></span>
* <span data-ttu-id="76adf-355">Hello log4jLogsCount 테이블에서 hello 데이터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-355">Delete hello data in hello log4jLogsCount table.</span></span>

<span data-ttu-id="76adf-356">다음은 사용할 수 있는 Windows PowerShell 스크립트 샘플입니다:</span><span class="sxs-lookup"><span data-stu-id="76adf-356">Here is a sample Windows PowerShell script that you can use:</span></span>

```powershell
$storageAccountName = "<AzureStorageAccountName>"
$containerName = "<ContainerName>"

#SQL database variables
$sqlDatabaseServer = "<SQLDatabaseServerName>"
$sqlDatabaseLogin = "<SQLDatabaseLoginName>"
$sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>"
$sqlDatabaseName = "<SQLDatabaseName>"
$sqlDatabaseTableName = "log4jLogsCount"

Write-host "Delete hello Hive script output file ..." -ForegroundColor Green
$storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
$destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey
Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $containerName

Write-host "Delete all hello records from hello log4jLogsCount table ..." -ForegroundColor Green
$conn = New-Object System.Data.SqlClient.SqlConnection
$conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
$conn.open()
$cmd = New-Object System.Data.SqlClient.SqlCommand
$cmd.connection = $conn
$cmd.commandtext = "delete from $sqlDatabaseTableName"
$cmd.executenonquery()

$conn.close()
```

## <a name="next-steps"></a><span data-ttu-id="76adf-357">다음 단계</span><span class="sxs-lookup"><span data-stu-id="76adf-357">Next steps</span></span>
<span data-ttu-id="76adf-358">이 자습서에서는 방법에 대해 배웠습니다 toodefine Oozie 워크플로 및 Oozie 코디네이터 라면 및 Oozie 코디네이터 toorun Azure PowerShell을 사용 하 여 작업 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="76adf-358">In this tutorial, you learned how toodefine an Oozie workflow and an Oozie coordinator, and how toorun an Oozie coordinator job by using Azure PowerShell.</span></span> <span data-ttu-id="76adf-359">더 toolearn hello 다음 문서를 참조:</span><span class="sxs-lookup"><span data-stu-id="76adf-359">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="76adf-360">[HDInsight 시작][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="76adf-360">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="76adf-361">[HDInsight에서 Azure Blob Storage 사용][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="76adf-361">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="76adf-362">[Azure PowerShell을 사용하여 HDInsight 클러스터 관리][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="76adf-362">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="76adf-363">[데이터 tooHDInsight 업로드][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="76adf-363">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="76adf-364">[HDInsight에서 Sqoop 사용][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="76adf-364">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="76adf-365">[HDInsight에서 Hive 사용][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="76adf-365">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="76adf-366">[HDInsight에서 Pig 사용][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="76adf-366">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="76adf-367">[HDInsight용 Java MapReduce 프로그램 개발][hdinsight-develop-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="76adf-367">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-java-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-develop-java-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.RunCoord.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
