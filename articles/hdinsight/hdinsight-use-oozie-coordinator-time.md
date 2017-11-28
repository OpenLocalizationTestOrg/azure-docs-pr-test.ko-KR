---
title: "HDInsight에서 시간 기준 Hadoop Oozie 코디네이터 사용 | Microsoft Docs"
description: "빅데이터 서비스인 HDInsight에서 시간 기준 Hadoop Oozie 코디네이터를 사용하는 방법을 알아봅니다. 또한 Oozie 워크플로와 코디네이터를 정의하고 작업을 제출하는 방법도 알아봅니다."
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
ms.openlocfilehash: 600a70c74a16e2601a874f804ac2e8382c8bfa90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-to-define-workflows-and-coordinate-jobs"></a><span data-ttu-id="2aaf6-104">HDInsight에서 Hadoop과 함께 시간 기준 Oozie 코디네이터를 사용하여 워크플로 정의 및 작업 조정</span><span class="sxs-lookup"><span data-stu-id="2aaf6-104">Use time-based Oozie coordinator with Hadoop in HDInsight to define workflows and coordinate jobs</span></span>
<span data-ttu-id="2aaf6-105">이 문서에서는 워크플로 및 코디네이터를 정의하는 방법, 시간을 기준으로 코디네이터 작업을 트리거하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-105">In this article, you'll learn how to define workflows and coordinators, and how to trigger the coordinator jobs, based on time.</span></span> <span data-ttu-id="2aaf6-106">이 문서를 시작하기 전에 [HDInsight에서 Oozie 사용][hdinsight-use-oozie]을 확인하는 것이 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-106">It is helpful to go through [Use Oozie with HDInsight][hdinsight-use-oozie] before you read this article.</span></span> <span data-ttu-id="2aaf6-107">Oozie 외에도 Azure 데이터 팩터리를 사용하여 작업을 예약할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-107">In addition to Oozie, you can also schedule jobs using Azure Data Factory.</span></span> <span data-ttu-id="2aaf6-108">Azure 데이터 팩터리를 알아보려면 [데이터 팩터리에서 Pig 및 Hive 사용](../data-factory/data-factory-data-transformation-activities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-108">To learn Azure Data Factory, see [Use Pig and Hive with Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2aaf6-109">이 문서를 사용하려면 Windows 기반 HDInsight 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-109">This article requires a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="2aaf6-110">Linux 기반 클러스터에서 시간 기준의 작업을 포함하여 Oozie 사용에 대한 자세한 내용은 [Oozie를 Hadoop와 함께 사용하여 Linux 기반 HDInsight 워크플로 정의 및 실행](hdinsight-use-oozie-linux-mac.md)</span><span class="sxs-lookup"><span data-stu-id="2aaf6-110">For information on using Oozie, including time-based jobs, on a Linux-based cluster, see [Use Oozie with Hadoop to define and run a workflow on Linux-based HDInsight](hdinsight-use-oozie-linux-mac.md)</span></span>

## <a name="what-is-oozie"></a><span data-ttu-id="2aaf6-111">Oozie 정의</span><span class="sxs-lookup"><span data-stu-id="2aaf6-111">What is Oozie</span></span>
<span data-ttu-id="2aaf6-112">Apache Oozie는 Hadoop 작업을 관리하는 워크플로/코디네이션 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-112">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="2aaf6-113">Hadoop 스택과 통합되며 Apache MapReduce, Apache Pig, Apache Hive, Apache Sqoop에 Hadoop 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-113">It is integrated with the Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="2aaf6-114">또한 Java 프로그램이나 셸 스크립트와 같이 시스템에 고유한 작업을 예약하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-114">It can also be used to schedule jobs that are specific to a system, such as Java programs or shell scripts.</span></span>

<span data-ttu-id="2aaf6-115">다음 이미지는 사용자가 구현할 워크플로를 보여줍니다:</span><span class="sxs-lookup"><span data-stu-id="2aaf6-115">The following image shows the workflow you will implement:</span></span>

![워크플로 다이어그램][img-workflow-diagram]

<span data-ttu-id="2aaf6-117">워크플로에는 두 동작이 포함됩니다:</span><span class="sxs-lookup"><span data-stu-id="2aaf6-117">The workflow contains two actions:</span></span>

1. <span data-ttu-id="2aaf6-118">Hive 작업은 log4j 로그 파일에서 각 로그 수준 유형의 수를 계산하는 HiveQL 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-118">A Hive action runs a HiveQL script to count the occurrences of each log-level type in a log4j log file.</span></span> <span data-ttu-id="2aaf6-119">각 log4j 로그는 유형과 심각도를 표시하는 [LOG LEVEL] 필드가 포함된 필드의 줄로 구성되어 있습니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-119">Each log4j log consists of a line of fields that contains a [LOG LEVEL] field to show the type and the severity, for example:</span></span>

        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...

    <span data-ttu-id="2aaf6-120">Hive 스크립트 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-120">The Hive script output is similar to:</span></span>

        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4

    <span data-ttu-id="2aaf6-121">Hive에 대한 자세한 내용은 [HDInsight와 함께 Hive 사용][hdinsight-use-hive]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-121">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="2aaf6-122">HiveQL 작업 출력을 Azure SQL 데이터베이스의 테이블에 내보내는 Sqoop 작업.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-122">A Sqoop action exports the HiveQL action output to a table in an Azure SQL database.</span></span> <span data-ttu-id="2aaf6-123">Sqoop에 대한 자세한 내용은 [HDInsight에서 Sqoop 사용][hdinsight-use-sqoop]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-123">For more information about Sqoop, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="2aaf6-124">HDInsight 클러스터에서 지원되는 Oozie 버전에 대해서는 [HDInsight에서 제공하는 클러스터 버전의 새로운 기능][hdinsight-versions]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-124">For supported Oozie versions on HDInsight clusters, see [What's new in the cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="2aaf6-125">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2aaf6-125">Prerequisites</span></span>
<span data-ttu-id="2aaf6-126">이 자습서를 시작하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-126">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="2aaf6-127">**Azure PowerShell이 포함된 워크스테이션**.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-127">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2aaf6-128">Azure 서비스 관리자를 사용하여 HDInsight 리소스를 관리하는 Azure PowerShell 지원은 더 이상 **지원되지 않고** 2017년 1월 1일에 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-128">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span></span> <span data-ttu-id="2aaf6-129">이 문서의 단계에서는 Azure Resource Manager로 작동하는 새 HDInsight cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-129">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="2aaf6-130">[Azure PowerShell 설치 및 구성](/powershell/azureps-cmdlets-docs) 단계를 수행하여 최신 버전의 Azure PowerShell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-130">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="2aaf6-131">Azure Resource Manager로 작동하는 새로운 cmdlet을 사용하도록 수정해야 하는 스크립트가 있는 경우 자세한 내용은 [HDInsight 클러스터에 대한 Azure Resource Manager 기반 개발 도구에 마이그레이션](hdinsight-hadoop-development-using-azure-resource-manager.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-131">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="2aaf6-132">**HDInsight 클러스터**.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-132">**An HDInsight cluster**.</span></span> <span data-ttu-id="2aaf6-133">HDInsight 클러스터를 만드는 방법에 대한 자세한 내용은 [HDInsight 클러스터 만들기][hdinsight-provision] 또는 [HDInsight 시작][hdinsight-get-started]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-133">For information about creating an HDInsight cluster, see [Create HDInsight clusters][hdinsight-provision], or [Get started with HDInsight][hdinsight-get-started].</span></span> <span data-ttu-id="2aaf6-134">자습서를 완료하려면 다음 데이터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-134">You will need the following data to go through the tutorial:</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="2aaf6-135">클러스터 속성</span><span class="sxs-lookup"><span data-stu-id="2aaf6-135">Cluster property</span></span></th><th><span data-ttu-id="2aaf6-136">Windows PowerShell 변수 이름</span><span class="sxs-lookup"><span data-stu-id="2aaf6-136">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="2aaf6-137">값</span><span class="sxs-lookup"><span data-stu-id="2aaf6-137">Value</span></span></th><th><span data-ttu-id="2aaf6-138">설명</span><span class="sxs-lookup"><span data-stu-id="2aaf6-138">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="2aaf6-139">HDInsight 클러스터 이름</span><span class="sxs-lookup"><span data-stu-id="2aaf6-139">HDInsight cluster name</span></span></td><td><span data-ttu-id="2aaf6-140">$clusterName</span><span class="sxs-lookup"><span data-stu-id="2aaf6-140">$clusterName</span></span></td><td></td><td><span data-ttu-id="2aaf6-141">이 자습서를 실행할 HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-141">The HDInsight cluster on which you will run this tutorial.</span></span></td></tr>
    <tr><td><span data-ttu-id="2aaf6-142">HDInsight 클러스터 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="2aaf6-142">HDInsight cluster username</span></span></td><td><span data-ttu-id="2aaf6-143">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="2aaf6-143">$clusterUsername</span></span></td><td></td><td><span data-ttu-id="2aaf6-144">HDInsight 클러스터 사용자 이름.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-144">The HDInsight cluster user name.</span></span> </td></tr>
    <tr><td><span data-ttu-id="2aaf6-145">HDInsight 클러스터 사용자 암호</span><span class="sxs-lookup"><span data-stu-id="2aaf6-145">HDInsight cluster user password</span></span> </td><td><span data-ttu-id="2aaf6-146">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="2aaf6-146">$clusterPassword</span></span></td><td></td><td><span data-ttu-id="2aaf6-147">HDInsight 클러스터 사용자의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-147">The HDInsight cluster user password.</span></span></td></tr>
    <tr><td><span data-ttu-id="2aaf6-148">Azure 저장소 계정 이름</span><span class="sxs-lookup"><span data-stu-id="2aaf6-148">Azure storage account name</span></span></td><td><span data-ttu-id="2aaf6-149">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="2aaf6-149">$storageAccountName</span></span></td><td></td><td><span data-ttu-id="2aaf6-150">Azure 저장소 계정은 HDInsight 클러스터에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-150">An Azure Storage account available to the HDInsight cluster.</span></span> <span data-ttu-id="2aaf6-151">이 자습서의 경우 클러스터 프로비전 프로세스 도중에 지정된 기본 저장소 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-151">For this tutorial, use the default storage account that you specified during the cluster provision process.</span></span></td></tr>
    <tr><td><span data-ttu-id="2aaf6-152">Azure Blob 컨테이너 이름</span><span class="sxs-lookup"><span data-stu-id="2aaf6-152">Azure Blob container name</span></span></td><td><span data-ttu-id="2aaf6-153">$containerName</span><span class="sxs-lookup"><span data-stu-id="2aaf6-153">$containerName</span></span></td><td></td><td><span data-ttu-id="2aaf6-154">이 예에서는 기본 HDInsight 클러스터 파일 시스템에 사용되는 Azure Blob 저장소 컨테이너를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-154">For this example, use the Azure Blob storage container that is used for the default HDInsight cluster file system.</span></span> <span data-ttu-id="2aaf6-155">기본적으로 컨테이너 이름은 HDInsight 클러스터 이름과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-155">By default, it has the same name as the HDInsight cluster.</span></span></td></tr>
    </table><span data-ttu-id="2aaf6-156">
* **Azure SQL 데이터베이스**입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-156">
* **An Azure SQL database**.</span></span> <span data-ttu-id="2aaf6-157">워크스테이션에서 액세스할 수 있도록 SQL 데이터베이스 서버의 방화벽 규칙을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-157">You must configure a firewall rule for the SQL Database server to allow access from your workstation.</span></span> <span data-ttu-id="2aaf6-158">Azure SQL Database 만들기 및 방화벽 구성에 대한 자세한 내용은 [Azure SQL Database 사용 시작][sqldatabase-get-started]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-158">For instructions about creating an Azure SQL database and configuring the firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> <span data-ttu-id="2aaf6-159">이 문서에는 이 자습서에 필요한 Azure SQL 데이터베이스 테이블을 만들기 위한 Windows PowerShell 스크립트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-159">This article provides a Windows PowerShell script for creating the Azure SQL database table that you need for this tutorial.</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="2aaf6-160">SQL 데이터베이스 속성</span><span class="sxs-lookup"><span data-stu-id="2aaf6-160">SQL database property</span></span></th><th><span data-ttu-id="2aaf6-161">Windows PowerShell 변수 이름</span><span class="sxs-lookup"><span data-stu-id="2aaf6-161">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="2aaf6-162">값</span><span class="sxs-lookup"><span data-stu-id="2aaf6-162">Value</span></span></th><th><span data-ttu-id="2aaf6-163">설명</span><span class="sxs-lookup"><span data-stu-id="2aaf6-163">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="2aaf6-164">SQL 데이터베이스 서버 이름</span><span class="sxs-lookup"><span data-stu-id="2aaf6-164">SQL database server name</span></span></td><td><span data-ttu-id="2aaf6-165">$sqlDatabaseServer</span><span class="sxs-lookup"><span data-stu-id="2aaf6-165">$sqlDatabaseServer</span></span></td><td></td><td><span data-ttu-id="2aaf6-166">Sqoop에서 데이터를 내보낼 SQL 데이터베이스 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-166">The SQL database server to which Sqoop will export data.</span></span> </td></tr>
    <tr><td><span data-ttu-id="2aaf6-167">SQL 데이터베이스 로그인 이름</span><span class="sxs-lookup"><span data-stu-id="2aaf6-167">SQL database login name</span></span></td><td><span data-ttu-id="2aaf6-168">$sqlDatabaseLogin</span><span class="sxs-lookup"><span data-stu-id="2aaf6-168">$sqlDatabaseLogin</span></span></td><td></td><td><span data-ttu-id="2aaf6-169">SQL 데이터베이스 로그인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-169">SQL Database login name.</span></span></td></tr>
    <tr><td><span data-ttu-id="2aaf6-170">SQL 데이터베이스 로그인 암호</span><span class="sxs-lookup"><span data-stu-id="2aaf6-170">SQL database login password</span></span></td><td><span data-ttu-id="2aaf6-171">$sqlDatabaseLoginPassword</span><span class="sxs-lookup"><span data-stu-id="2aaf6-171">$sqlDatabaseLoginPassword</span></span></td><td></td><td><span data-ttu-id="2aaf6-172">SQL 데이터베이스 로그인 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-172">SQL Database login password.</span></span></td></tr>
    <tr><td><span data-ttu-id="2aaf6-173">SQL 데이터베이스 이름</span><span class="sxs-lookup"><span data-stu-id="2aaf6-173">SQL database name</span></span></td><td><span data-ttu-id="2aaf6-174">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="2aaf6-174">$sqlDatabaseName</span></span></td><td></td><td><span data-ttu-id="2aaf6-175">Sqoop에서 데이터를 내보낼 Azure SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-175">The Azure SQL database to which Sqoop will export data.</span></span> </td></tr>
    </table>

  > [!NOTE]
  > <span data-ttu-id="2aaf6-176">기본적으로 Azure SQL 데이터베이스는 Azure HDInsight 같은 Azure 서비스로부터의 연결을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-176">By default an Azure SQL database allows connections from Azure Services, such as Azure HDInsight.</span></span> <span data-ttu-id="2aaf6-177">이 방화벽 설정을 사용하지 않도록 설정한 경우 Azure 포털에서 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-177">If this firewall setting is disabled, you must enable it from the Azure Portal.</span></span> <span data-ttu-id="2aaf6-178">SQL Database 만들기 및 방화벽 규칙 구성에 대한 지침은 [SQL Database 만들기 및 구성][sqldatabase-get-started]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-178">For instruction about creating a SQL Database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-get-started].</span></span>

> [!NOTE]
> <span data-ttu-id="2aaf6-179">테이블의 채우기 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-179">Fill-in the values in the tables.</span></span> <span data-ttu-id="2aaf6-180">이 자습서를 완료하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-180">It will be helpful for going through this tutorial.</span></span>

## <a name="define-oozie-workflow-and-the-related-hiveql-script"></a><span data-ttu-id="2aaf6-181">Oozie 워크플로 및 관련 HiveQL 스크립트 정의</span><span class="sxs-lookup"><span data-stu-id="2aaf6-181">Define Oozie workflow and the related HiveQL script</span></span>
<span data-ttu-id="2aaf6-182">Oozie 워크플로 정의는 hPDL(XML 프로세스 정의 언어)로 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-182">Oozie workflows definitions are written in hPDL (an XML process definition language).</span></span> <span data-ttu-id="2aaf6-183">기본 워크플로 파일 이름은 *workflow.xml*입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-183">The default workflow file name is *workflow.xml*.</span></span>  <span data-ttu-id="2aaf6-184">워크플로 파일을 로컬로 저장하고 이 자습서의 뒷부분에 나오는 Azure PowerShell을 사용하여 HDInsight 클러스터에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-184">You will save the workflow file locally, and then deploy it to the HDInsight cluster by using Azure PowerShell later in this tutorial.</span></span>

<span data-ttu-id="2aaf6-185">워크플로의 Hive 작업은 HiveQL 스크립트 파일을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-185">The Hive action in the workflow calls a HiveQL script file.</span></span> <span data-ttu-id="2aaf6-186">이 스크립트 파일에는 세 개의 HiveQL 문이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-186">This script file contains three HiveQL statements:</span></span>

1. <span data-ttu-id="2aaf6-187">**DROP TABLE 문** 은 log4j Hive 테이블이 있는 경우 이 테이블을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-187">**The DROP TABLE statement** deletes the log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="2aaf6-188">**CREATE TABLE 문** 은 log4j 로그 파일 위치를 가리키는 log4j Hive 외부 테이블을 만듭니다;</span><span class="sxs-lookup"><span data-stu-id="2aaf6-188">**The CREATE TABLE statement** creates a log4j Hive external table, which points to the location of the log4j log file;</span></span>
3. <span data-ttu-id="2aaf6-189">**log4j Hive 외부 테이블의 위치**입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-189">**The location of the log4j log file**.</span></span> <span data-ttu-id="2aaf6-190">필드 구분 기호는 ","입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-190">The field delimiter is ",".</span></span> <span data-ttu-id="2aaf6-191">기본 줄 구분 기호는 "\n"입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-191">The default line delimiter is "\n".</span></span> <span data-ttu-id="2aaf6-192">Hive 외부 테이블은 Oozie 워크플로를 여러 번 실행하려는 경우 데이터 파일이 원래 위치에서 제거되지 않도록 하기 위해서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-192">A Hive external table is used to avoid the data file being removed from the original location, in case you want to run the Oozie workflow multiple times.</span></span>
4. <span data-ttu-id="2aaf6-193">**INSERT OVERWRITE 문** 은 log4j Hive 테이블에서 각 로그 수준 유형의 수를 계산하고 그 출력 결과를 Azure Blob 저장소 위치에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-193">**The INSERT OVERWRITE statement** counts the occurrences of each log-level type from the log4j Hive table, and it saves the output to an Azure Blob storage location.</span></span>

> [!NOTE]
> <span data-ttu-id="2aaf6-194">알려진 Hive 경로 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-194">There is a known Hive path issue.</span></span> <span data-ttu-id="2aaf6-195">Oozie 작업을 제출할 때 이 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-195">You will run into this problem when submitting an Oozie job.</span></span> <span data-ttu-id="2aaf6-196">TechNet Wiki에서 문제 해결을 위한 지침을 찾을 수 있습니다: [HDInsight 하이브 오류: 이름을 바꿀 수 없습니다][technetwiki-hive-error].</span><span class="sxs-lookup"><span data-stu-id="2aaf6-196">The instructions for fixing the issue can be found on the TechNet Wiki: [HDInsight Hive error: Unable to rename][technetwiki-hive-error].</span></span>

<span data-ttu-id="2aaf6-197">**HiveQL 스크립트 파일을 워크플로에서 호출하도록 정의하려면**</span><span class="sxs-lookup"><span data-stu-id="2aaf6-197">**To define the HiveQL script file to be called by the workflow**</span></span>

1. <span data-ttu-id="2aaf6-198">다음 내용이 포함된 텍스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-198">Create a text file with the following content:</span></span>

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    <span data-ttu-id="2aaf6-199">스크립트에서 사용되는 3개의 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-199">There are three variables used in the script:</span></span>

   * <span data-ttu-id="2aaf6-200">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="2aaf6-200">${hiveTableName}</span></span>
   * <span data-ttu-id="2aaf6-201">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="2aaf6-201">${hiveDataFolder}</span></span>
   * <span data-ttu-id="2aaf6-202">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="2aaf6-202">${hiveOutputFolder}</span></span>

     <span data-ttu-id="2aaf6-203">워크플로 정의 파일(이 자습서에서는 workflow.xml)은 런타임 시 이러한 값을 이 HiveQL 스크립트에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-203">The workflow definition file (workflow.xml in this tutorial) will pass these values to this HiveQL script at run time.</span></span>
2. <span data-ttu-id="2aaf6-204">ANSI(ASCII) 인코딩을 사용하여 파일을 **C:\Tutorials\UseOozie\useooziewf.hql**로 저장하세요.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-204">Save the file as **C:\Tutorials\UseOozie\useooziewf.hql** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="2aaf6-205">(텍스트 편집기에서 이 옵션을 제공하지 않는 경우 메모장을 사용하세요.) 이 스크립트 파일은 자습서의 뒷부분에 나오는 HDInsight 클러스터에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-205">(Use Notepad if your text editor doesn't provide this option.) This script file will be deployed to the HDInsight cluster later in the tutorial.</span></span>

<span data-ttu-id="2aaf6-206">**워크플로를 정의하려면**</span><span class="sxs-lookup"><span data-stu-id="2aaf6-206">**To define a workflow**</span></span>

1. <span data-ttu-id="2aaf6-207">다음 내용이 포함된 텍스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-207">Create a text file with the following content:</span></span>

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start to = "RunHiveScript"/>

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

    <span data-ttu-id="2aaf6-208">워크플로에 2가지 작업이 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-208">There are two actions defined in the workflow.</span></span> <span data-ttu-id="2aaf6-209">시작 작업은 *RunHiveScript*입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-209">The start-to action is *RunHiveScript*.</span></span> <span data-ttu-id="2aaf6-210">작업이 *확인*를 실행하면 다음 작업은 *RunSqoopExport*입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-210">If the action runs *OK*, the next action is *RunSqoopExport*.</span></span>

    <span data-ttu-id="2aaf6-211">RunHiveScript에는 몇 개의 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-211">The RunHiveScript has several variables.</span></span> <span data-ttu-id="2aaf6-212">Azure PowerShell을 사용하여 워크스테이션에서 Oozie 작업을 제출할 때 이러한 값을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-212">You will pass the values when you submit the Oozie job from your workstation by using Azure PowerShell.</span></span>

    <span data-ttu-id="2aaf6-213">워크플로 변수</span><span class="sxs-lookup"><span data-stu-id="2aaf6-213">Workflow variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="2aaf6-214">워크플로 변수</span><span class="sxs-lookup"><span data-stu-id="2aaf6-214">Workflow variables</span></span></th><th><span data-ttu-id="2aaf6-215">설명</span><span class="sxs-lookup"><span data-stu-id="2aaf6-215">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="2aaf6-216">${jobTracker}</span><span class="sxs-lookup"><span data-stu-id="2aaf6-216">${jobTracker}</span></span></td><td><span data-ttu-id="2aaf6-217">Hadoop 작업 추적기의 URL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-217">Specify the URL of the Hadoop job tracker.</span></span> <span data-ttu-id="2aaf6-218">HDInsight 클러스터 버전 3.0 및 2.0에는 <strong>jobtrackerhost:9010</strong>을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-218">Use <strong>jobtrackerhost:9010</strong> on HDInsight cluster version 3.0 and 2.0.</span></span></td></tr>
    <tr><td><span data-ttu-id="2aaf6-219">${nameNode}</span><span class="sxs-lookup"><span data-stu-id="2aaf6-219">${nameNode}</span></span></td><td><span data-ttu-id="2aaf6-220">Hadoop 이름 노드의 URL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-220">Specify the URL of the Hadoop name node.</span></span> <span data-ttu-id="2aaf6-221"><i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>과 같은 기본 파일 시스템 wasb:// 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-221">Use the default file system wasb:// address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
    <tr><td><span data-ttu-id="2aaf6-222">${queueName}</span><span class="sxs-lookup"><span data-stu-id="2aaf6-222">${queueName}</span></span></td><td><span data-ttu-id="2aaf6-223">작업을 제출할 큐 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-223">Specifies the queue name that the job will be submitted to.</span></span> <span data-ttu-id="2aaf6-224"><strong>기본값</strong>을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-224">Use <strong>default</strong>.</span></span></td></tr>
    </table>

    <span data-ttu-id="2aaf6-225">Hive 작업 변수</span><span class="sxs-lookup"><span data-stu-id="2aaf6-225">Hive action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="2aaf6-226">Hive 작업 변수</span><span class="sxs-lookup"><span data-stu-id="2aaf6-226">Hive action variable</span></span></th><th><span data-ttu-id="2aaf6-227">설명</span><span class="sxs-lookup"><span data-stu-id="2aaf6-227">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="2aaf6-228">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="2aaf6-228">${hiveDataFolder}</span></span></td><td><span data-ttu-id="2aaf6-229">Hive Create Table 명령의 소스 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-229">The source directory for the Hive Create Table command.</span></span></td></tr>
    <tr><td><span data-ttu-id="2aaf6-230">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="2aaf6-230">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="2aaf6-231">INSERT OVERWRITE 문의 출력 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-231">The output folder for the INSERT OVERWRITE statement.</span></span></td></tr>
    <tr><td><span data-ttu-id="2aaf6-232">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="2aaf6-232">${hiveTableName}</span></span></td><td><span data-ttu-id="2aaf6-233">log4j 데이터 파일을 참조하는 Hive 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-233">The name of the Hive table that references the log4j data files.</span></span></td></tr>
    </table>

    <span data-ttu-id="2aaf6-234">Sqoop 작업 변수</span><span class="sxs-lookup"><span data-stu-id="2aaf6-234">Sqoop action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="2aaf6-235">Sqoop 작업 변수</span><span class="sxs-lookup"><span data-stu-id="2aaf6-235">Sqoop action variable</span></span></th><th><span data-ttu-id="2aaf6-236">설명</span><span class="sxs-lookup"><span data-stu-id="2aaf6-236">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="2aaf6-237">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="2aaf6-237">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="2aaf6-238">SQL 데이터베이스 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-238">SQL Database connection string.</span></span></td></tr>
    <tr><td><span data-ttu-id="2aaf6-239">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="2aaf6-239">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="2aaf6-240">데이터를 내보낼 Azure SQL 데이터베이스 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-240">The Azure SQL database table to where the data will be exported.</span></span></td></tr>
    <tr><td><span data-ttu-id="2aaf6-241">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="2aaf6-241">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="2aaf6-242">Hive INSERT OVERWRITE 문의 출력 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-242">The output folder for the Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="2aaf6-243">이 폴더는 Sqoop 내보내기(내보내기 디렉터리)와 동일한 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-243">This is the same folder for the Sqoop export (export-dir).</span></span></td></tr>
    </table>

    <span data-ttu-id="2aaf6-244">Oozie 워크플로 및 워크플로 작업 사용에 대한 자세한 내용은 [Apache Oozie 4.0 설명서][apache-oozie-400](HDInsight 클러스터 버전 3.0의 경우) 또는 [Apache Oozie 3.3.2 설명서][apache-oozie-332](HDInsight 클러스터 버전 2.1의 경우)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-244">For more information about Oozie workflow and using the workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

1. <span data-ttu-id="2aaf6-245">ANSI(ASCII) 인코딩을 사용하여 파일을**C:\Tutorials\UseOozie\workflow.xml**로 저장하세요.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-245">Save the file as **C:\Tutorials\UseOozie\workflow.xml** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="2aaf6-246">(텍스트 편집기에서 이 옵션을 제공하지 않는 경우 메모장을 사용하세요.)</span><span class="sxs-lookup"><span data-stu-id="2aaf6-246">(Use Notepad if your text editor doesn't provide this option.)</span></span>

<span data-ttu-id="2aaf6-247">**코디네이터를 정의하려면**</span><span class="sxs-lookup"><span data-stu-id="2aaf6-247">**To define coordinator**</span></span>

1. <span data-ttu-id="2aaf6-248">다음 내용이 포함된 텍스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-248">Create a text file with the following content:</span></span>

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    <span data-ttu-id="2aaf6-249">정의 파일에는 5개의 변수가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-249">There are five variables used in the definition file:</span></span>

   | <span data-ttu-id="2aaf6-250">변수</span><span class="sxs-lookup"><span data-stu-id="2aaf6-250">Variable</span></span> | <span data-ttu-id="2aaf6-251">설명</span><span class="sxs-lookup"><span data-stu-id="2aaf6-251">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="2aaf6-252">${coordFrequency}</span><span class="sxs-lookup"><span data-stu-id="2aaf6-252">${coordFrequency}</span></span> |<span data-ttu-id="2aaf6-253">작업 일시 중지 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-253">Job pause time.</span></span> <span data-ttu-id="2aaf6-254">빈도는 항상 분 단위로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-254">Frequency is always expressed in minutes.</span></span> |
   | <span data-ttu-id="2aaf6-255">${coordStart}</span><span class="sxs-lookup"><span data-stu-id="2aaf6-255">${coordStart}</span></span> |<span data-ttu-id="2aaf6-256">작업 시작 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-256">Job start time.</span></span> |
   | <span data-ttu-id="2aaf6-257">${coordEnd}</span><span class="sxs-lookup"><span data-stu-id="2aaf6-257">${coordEnd}</span></span> |<span data-ttu-id="2aaf6-258">작업 종료 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-258">Job end time.</span></span> |
   | <span data-ttu-id="2aaf6-259">${coordTimezone}</span><span class="sxs-lookup"><span data-stu-id="2aaf6-259">${coordTimezone}</span></span> |<span data-ttu-id="2aaf6-260">Oozie는 일광 절약 시간제(UTC를 사용하여 일반적으로 표시 됨)없이 고정된 시간대에서 코디네이터 작업을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-260">Oozie processes coordinator jobs in a fixed time zone with no daylight saving time (typically represented by using UTC).</span></span> <span data-ttu-id="2aaf6-261">해당 시간대는 "Oozie 처리 시간대"라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-261">This time zone is referred as the "Oozie processing timezone."</span></span> |
   | <span data-ttu-id="2aaf6-262">${wfPath}</span><span class="sxs-lookup"><span data-stu-id="2aaf6-262">${wfPath}</span></span> |<span data-ttu-id="2aaf6-263">workflow.xml의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-263">The path for the workflow.xml.</span></span>  <span data-ttu-id="2aaf6-264">워크플로 파일 이름이 기본 파일 이름(workflow.xml)이 아닌 경우 기본 파일 이름을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-264">If the workflow file name is not the default file name (workflow.xml), you must specify it.</span></span> |
2. <span data-ttu-id="2aaf6-265">ANSI(ASCII) 인코딩을 사용하여 파일을 **C:\Tutorials\UseOozie\coordinator.xml**로 저장하세요.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-265">Save the file as **C:\Tutorials\UseOozie\coordinator.xml** by using the ANSI (ASCII) encoding.</span></span> <span data-ttu-id="2aaf6-266">(텍스트 편집기에서 이 옵션을 제공하지 않는 경우 메모장을 사용하세요.)</span><span class="sxs-lookup"><span data-stu-id="2aaf6-266">(Use Notepad if your text editor doesn't provide this option.)</span></span>

## <a name="deploy-the-oozie-project-and-prepare-the-tutorial"></a><span data-ttu-id="2aaf6-267">Oozie 프로젝트 배포 및 자습서 준비</span><span class="sxs-lookup"><span data-stu-id="2aaf6-267">Deploy the Oozie project and prepare the tutorial</span></span>
<span data-ttu-id="2aaf6-268">Azure PowerShell 스크립트를 실행하여 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-268">You will run an Azure PowerShell script to perform the following:</span></span>

* <span data-ttu-id="2aaf6-269">HiveQL 스크립트(useoozie.hql)를 Azure Blob Storage wasb:///tutorials/useoozie/useoozie.hql에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-269">Copy the HiveQL script (useoozie.hql) to Azure Blob storage, wasb:///tutorials/useoozie/useoozie.hql.</span></span>
* <span data-ttu-id="2aaf6-270">workflow.xml을 wasb:///tutorials/useoozie/workflow.xml에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-270">Copy workflow.xml to wasb:///tutorials/useoozie/workflow.xml.</span></span>
* <span data-ttu-id="2aaf6-271">coordinator.xml을 wasb:///tutorials/useoozie/coordinator.xml에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-271">Copy coordinator.xml to wasb:///tutorials/useoozie/coordinator.xml.</span></span>
* <span data-ttu-id="2aaf6-272">데이터 파일(/example/data/sample.log)을 wasb:///tutorials/useoozie/data/sample.log에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-272">Copy the data file (/example/data/sample.log) to wasb:///tutorials/useoozie/data/sample.log.</span></span>
* <span data-ttu-id="2aaf6-273">Sqoop 내보내기 데이터를 저장할 Azure SQL 데이터베이스 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-273">Create an Azure SQL database table for storing Sqoop export data.</span></span> <span data-ttu-id="2aaf6-274">테이블 이름은 *log4jLogCount*입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-274">The table name is *log4jLogCount*.</span></span>

<span data-ttu-id="2aaf6-275">**HDInsight 저장소 이해**</span><span class="sxs-lookup"><span data-stu-id="2aaf6-275">**Understand HDInsight storage**</span></span>

<span data-ttu-id="2aaf6-276">HDInsight는 데이터 저장소로 Azure Blob 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-276">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="2aaf6-277">wasb://는 Azure Blob Storage에서 Microsoft의 HDFS(Hadoop 분산 파일 시스템)를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-277">wasb:// is Microsoft's implementation of the Hadoop distributed file system (HDFS) in Azure Blob storage.</span></span> <span data-ttu-id="2aaf6-278">자세한 내용은 [HDInsight와 함께 Azure Blob Storage 사용][hdinsight-storage]을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-278">For more information, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="2aaf6-279">HDInsight 클러스터를 프로비전할 때 Azure Blob 저장소 계정 및 이 계정에서 오는 특정 컨테이너가 HDFS의 경우와 같이 기본 파일 시스템으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-279">When you provision an HDInsight cluster, an Azure Blob storage account and a specific container from that account is designated as the default file system, like in HDFS.</span></span> <span data-ttu-id="2aaf6-280">프로비전 프로세스에서는 이 저장소 계정 외에도 동일하거나 다른 Azure 구독의 저장소 계정을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-280">In addition to this storage account, you can add additional storage accounts from the same Azure subscription or from different Azure subscriptions during the provisioning process.</span></span> <span data-ttu-id="2aaf6-281">저장소 계정 추가에 대한 지침은 [HDInsight 클러스터 프로비전][hdinsight-provision]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-281">For instructions about adding additional storage accounts, see [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="2aaf6-282">이 자습서에 사용된 Azure PowerShell 스크립트를 간소화하려면 모든 파일이 */tutorials/useoozie*에 있는 기본 파일 시스템 컨테이너에 저장되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-282">To simplify the Azure PowerShell script used in this tutorial, all of the files are stored in the default file system container located at */tutorials/useoozie*.</span></span> <span data-ttu-id="2aaf6-283">기본적으로 이 컨테이너 이름은 HDInsight 클러스터 이름과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-283">By default, this container has the same name as the HDInsight cluster name.</span></span>
<span data-ttu-id="2aaf6-284">구문은 다음과 같습니다:</span><span class="sxs-lookup"><span data-stu-id="2aaf6-284">The syntax is:</span></span>

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> <span data-ttu-id="2aaf6-285">HDInsight 클러스터 버전 3.0에서는 *wasb://* 구문만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-285">Only the *wasb://* syntax is supported in HDInsight cluster version 3.0.</span></span> <span data-ttu-id="2aaf6-286">이전 *asv://* 구문은 HDInsight 2.1 및 1.6 클러스터에서 지원되지만, HDInsight 3.0 클러스터에서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-286">The older *asv://* syntax is supported in HDInsight 2.1 and 1.6 clusters, but it is not supported in HDInsight 3.0 clusters.</span></span>
>
> <span data-ttu-id="2aaf6-287">wasb:// 경로는 가상 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-287">The wasb:// path is a virtual path.</span></span> <span data-ttu-id="2aaf6-288">자세한 내용은 [HDInsight와 함께 Azure Blob Storage 사용][hdinsight-storage]을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-288">For more information see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="2aaf6-289">기본 파일 시스템 컨테이너에 저장된 파일은 다음 URI 중 아무거나 사용하여 HDInsight에서 액세스할 수 있습니다(여기서는 예제로 workflow.xml를 사용합니다).</span><span class="sxs-lookup"><span data-stu-id="2aaf6-289">A file that is stored in the default file system container can be accessed from HDInsight by using any of the following URIs (I am using workflow.xml as an example):</span></span>

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

<span data-ttu-id="2aaf6-290">저장소 계정에서 바로 파일에 액세스하려는 경우 파일의 Blob 이름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-290">If you want to access the file directly from the storage account, the blob name for the file is:</span></span>

    tutorials/useoozie/workflow.xml

<span data-ttu-id="2aaf6-291">**Hive 내부 테이블 및 외부 테이블 이해**</span><span class="sxs-lookup"><span data-stu-id="2aaf6-291">**Understand Hive internal and external tables**</span></span>

<span data-ttu-id="2aaf6-292">Hive 내부 테이블 및 외부 테이블에 대해 알아야 할 사항이 몇 가지 있습니다:</span><span class="sxs-lookup"><span data-stu-id="2aaf6-292">There are a few things you need to know about Hive internal and external tables:</span></span>

* <span data-ttu-id="2aaf6-293">CREATE TABLE 명령은 관리되는 테이블이라고도 하는 내부 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-293">The CREATE TABLE command creates an internal table, also known as a managed table.</span></span> <span data-ttu-id="2aaf6-294">데이터 파일은 기본 컨테이너에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-294">The data file must be located in the default container.</span></span>
* <span data-ttu-id="2aaf6-295">CREATE TABLE 명령은 데이터 파일을 기본 컨테이너의 /hive/warehouse/<TableName> 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-295">The CREATE TABLE command moves the data file to the /hive/warehouse/<TableName> folder in the default container.</span></span>
* <span data-ttu-id="2aaf6-296">CREATE EXTERNAL TABLE 명령은 외부 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-296">The CREATE EXTERNAL TABLE command creates an external table.</span></span> <span data-ttu-id="2aaf6-297">데이터 파일은 기본 컨테이너가 아닌 곳에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-297">The data file can be located outside the default container.</span></span>
* <span data-ttu-id="2aaf6-298">CREATE EXTERNAL TABLE 명령은 데이터 파일을 이동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-298">The CREATE EXTERNAL TABLE command does not move the data file.</span></span>
* <span data-ttu-id="2aaf6-299">CREATE EXTERNAL TABLE 명령은 LOCATION 절에 지정된 폴더 아래에 하위 폴더를 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-299">The CREATE EXTERNAL TABLE command doesn't allow any subfolders under the folder that is specified in the LOCATION clause.</span></span> <span data-ttu-id="2aaf6-300">이 때문에 자습서에서는 sample.log 파일의 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-300">This is the reason why the tutorial makes a copy of the sample.log file.</span></span>

<span data-ttu-id="2aaf6-301">자세한 내용은 [HDInsight: Hive 내부 및 외부 테이블 소개][cindygross-hive-tables]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-301">For more information, see [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables].</span></span>

<span data-ttu-id="2aaf6-302">**자습서를 준비하려면**</span><span class="sxs-lookup"><span data-stu-id="2aaf6-302">**To prepare the tutorial**</span></span>

1. <span data-ttu-id="2aaf6-303">Windows PowerShell ISE를 엽니다. (Windows 8 시작 화면에서 **PowerShell_ISE**를 입력한 후 **Windows PowerShell ISE**를 클릭하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-303">Open the Windows PowerShell ISE (in the Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="2aaf6-304">자세한 내용은 [Windows 8 및 Windows에서 Windows PowerShell 시작][powershell-start]을 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="2aaf6-304">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="2aaf6-305">아래 창에서 다음 명령을 실행하여 Azure 구독에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-305">In the bottom pane, run the following command to connect to your Azure subscription:</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="2aaf6-306">Azure 계정 자격 증명을 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-306">You will be prompted to enter your Azure account credentials.</span></span> <span data-ttu-id="2aaf6-307">구독 연결을 추가하는 이 메서드의 시간이 초과하여 12시간 후에는 cmdlet을 다시 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-307">This method of adding a subscription connection times out, and after 12 hours, you will have to run the cmdlet again.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2aaf6-308">여러 Azure 구독이 있고 기본 구독이 사용하려는 구독이 아닌 경우 <strong>Select-AzureSubscription</strong> cmdlet을 사용하여 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-308">If you have multiple Azure subscriptions and the default subscription is not the one you want to use, use the <strong>Select-AzureSubscription</strong> cmdlet to select a subscription.</span></span>

3. <span data-ttu-id="2aaf6-309">다음 스크립트를 스크립트 창에 복사한 다음 처음 6개의 변수를 설정합니다:</span><span class="sxs-lookup"><span data-stu-id="2aaf6-309">Copy the following script into the script pane, and then set the first six variables:</span></span>

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

    # Oozie files for the tutorial
    $hiveQLScript = "C:\Tutorials\UseOozie\useooziewf.hql"
    $workflowDefinition = "C:\Tutorials\UseOozie\workflow.xml"
    $coordDefinition =  "C:\Tutorials\UseOozie\coordinator.xml"

    # WASB folder for storing the Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use the long path here
    ```

    <span data-ttu-id="2aaf6-310">변수에 대한 자세한 설명은 이 자습서에서 [필수 조건](#prerequisites) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-310">For more descriptions of the variables, see the [Prerequisites](#prerequisites) section in this tutorial.</span></span>

4. <span data-ttu-id="2aaf6-311">스크립트 창의 스크립트에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-311">Append the following to the script in the script pane:</span></span>

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
        Write-Host "Make a copy of the sample.log file ... " -ForegroundColor Green
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

        #Create the log4jLogsCount table
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

    # make a copy of example/data/sample.log to example/data/log4j/sample.log
    prepareHiveDataFile;

    # create log4jlogsCount table on SQL database
    prepareSQLDatabase;
    ```

5. <span data-ttu-id="2aaf6-312">**스크립트 실행**을 클릭하거나 **F5** 키를 눌러 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-312">Click **Run Script** or press **F5** to run the script.</span></span> <span data-ttu-id="2aaf6-313">다음과 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-313">The output will be similar to:</span></span>

    ![자습서 준비 출력][img-preparation-output]

## <a name="run-the-oozie-project"></a><span data-ttu-id="2aaf6-315">Oozie 프로젝트 실행</span><span class="sxs-lookup"><span data-stu-id="2aaf6-315">Run the Oozie project</span></span>
<span data-ttu-id="2aaf6-316">Azure PowerShell은 Oozie 작업을 정의하는 데 현재 어떤 cmdlet도 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-316">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="2aaf6-317">**Invoke-RestMethod** cmdlet을 사용하여 Oozie 웹 서비스를 불러올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-317">You can use the **Invoke-RestMethod** cmdlet to invoke Oozie web services.</span></span> <span data-ttu-id="2aaf6-318">Oozie 웹 서비스 API는 HTTP REST JSON API입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-318">The Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="2aaf6-319">Oozie 웹 서비스 API에 대한 자세한 내용은 [Apache Oozie 4.0 설명서][apache-oozie-400](HDInsight 클러스터 버전 3.0의 경우) 또는 [Apache Oozie 3.3.2 설명서][apache-oozie-332](HDInsight 클러스터 버전 2.1의 경우)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-319">For more information about the Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

<span data-ttu-id="2aaf6-320">**Oozie 작업을 제출하려면**</span><span class="sxs-lookup"><span data-stu-id="2aaf6-320">**To submit an Oozie job**</span></span>

1. <span data-ttu-id="2aaf6-321">Windows PowerShell ISE를 엽니다. (Windows 8 시작 화면에서 **PowerShell_ISE**를 입력한 후에 **Windows PowerShell ISE**를 클릭하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-321">Open the Windows PowerShell ISE (in Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="2aaf6-322">자세한 내용은 [Windows 8 및 Windows에서 Windows PowerShell 시작][powershell-start]을 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="2aaf6-322">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="2aaf6-323">다음 스크립트를 스크립트 창에 복사한 후 처음 14개 변수를 설정합니다(하지만 **$storageUri**는 건너뜀).</span><span class="sxs-lookup"><span data-stu-id="2aaf6-323">Copy the following script into the script pane, and then set the first fourteen variables (however, skip **$storageUri**).</span></span>

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

    $oozieWFPath="$storageUri/tutorials/useoozie"  # The default name is workflow.xml. And you don't need to specify the file name.
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

    <span data-ttu-id="2aaf6-324">변수에 대한 자세한 설명은 이 자습서에서 [필수 조건](#prerequisites) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-324">For more descriptions of the variables, see the [Prerequisites](#prerequisites) section in this tutorial.</span></span>

    <span data-ttu-id="2aaf6-325">$coordstart 및 $coordend는 워크플로 시작 시간 및 끝 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-325">$coordstart and $coordend are the workflow starting and ending time.</span></span> <span data-ttu-id="2aaf6-326">UTC/GMT 시간을 찾으려면 bing.com에서 "utc time"을 검색하세요. $coordFrequency는 워크플로를 실행할 빈도(분)입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-326">To find out the UTC/GMT time, search "utc time" on bing.com. The $coordFrequency is how often in minutes you want to run the workflow.</span></span>
3. <span data-ttu-id="2aaf6-327">스크립트에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-327">Append the following to the script.</span></span> <span data-ttu-id="2aaf6-328">이 부분은 Oozie 페이로드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-328">This part defines the Oozie payload:</span></span>

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
   > <span data-ttu-id="2aaf6-329">워크플로 제출 페이로드 파일과 비교할 때 주요 차이점은 **oozie.coord.application.path**변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-329">The major difference compared to the workflow submission payload file is the variable **oozie.coord.application.path**.</span></span> <span data-ttu-id="2aaf6-330">워크플로 작업을 제출할 때는 대신 **oozie.wf.application.path** 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-330">When you submit a workflow job, you use **oozie.wf.application.path** instead.</span></span>

4. <span data-ttu-id="2aaf6-331">스크립트에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-331">Append the following to the script.</span></span> <span data-ttu-id="2aaf6-332">이 부분은 Oozie 웹 서비스 상태를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-332">This part checks the Oozie web service status:</span></span>

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
            Write-Host "Oozie server status is $oozieServerSatus...cannot submit Oozie jobs. Check the server status and re-run the job."
            exit 1
        }
    }
    ```

5. <span data-ttu-id="2aaf6-333">스크립트에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-333">Append the following to the script.</span></span> <span data-ttu-id="2aaf6-334">이 부분은 Oozie 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-334">This part creates an Oozie job:</span></span>

    ```powershell
    function createOozieJob()
    {
        # create Oozie job
        Write-Host "Sending the following Payload to the cluster:" -ForegroundColor Green
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
   > <span data-ttu-id="2aaf6-335">워크플로 작업을 제출하는 경우 이 작업이 만들어진 후에 시작되도록 다른 웹 서비스를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-335">When you submit a workflow job, you must make another web service call to start the job after the job is created.</span></span> <span data-ttu-id="2aaf6-336">이 경우 코디네이터 작업은 시간별로 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-336">In this case, the coordinator job is triggered by time.</span></span> <span data-ttu-id="2aaf6-337">작업이 자동으로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-337">The job will start automatically.</span></span>

6. <span data-ttu-id="2aaf6-338">스크립트에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-338">Append the following to the script.</span></span> <span data-ttu-id="2aaf6-339">이 부분은 Oozie 작업 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-339">This part checks the Oozie job status:</span></span>

    ```powershell
    function checkOozieJobStatus($oozieJobId)
    {
        # get job status
        Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until the job metadata is populated in the Oozie metastore..." -ForegroundColor Green
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

        Write-Host "Getting job status and waiting for the job to complete..." -ForegroundColor Green
        $clusterUriGetJobStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")

        while($JobStatus -notmatch "SUCCEEDED|KILLED")
        {
            Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for the job to complete..."
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

7. <span data-ttu-id="2aaf6-340">(선택 사항) 스크립트에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-340">(Optional) Append the following to the script.</span></span>

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
        Write-Host "Killing the Oozie job $oozieJobId..." -ForegroundColor Green
        $clusterUriStartJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=kill" #Valid values for the 'action' parameter are 'start', 'suspend', 'resume', 'kill', 'dryrun', 'rerun', and 'change'.
        $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $creds | Format-Table -HideTableHeaders -debug
    }
    ```

8. <span data-ttu-id="2aaf6-341">스크립트에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-341">Append the following to the script:</span></span>

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

    <span data-ttu-id="2aaf6-342">추가 함수를 실행하려는 경우 # 기호를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-342">Remove the # signs if you want to run the additional functions.</span></span>
9. <span data-ttu-id="2aaf6-343">HDinsight 클러스터 버전이 2.1인 경우 "https://$clusterName.azurehdinsight.net:443/oozie/v2/"를 "https://$clusterName.azurehdinsight.net:443/oozie/v1/"로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-343">If your HDinsight cluster is version 2.1, replace "https://$clusterName.azurehdinsight.net:443/oozie/v2/" with "https://$clusterName.azurehdinsight.net:443/oozie/v1/".</span></span> <span data-ttu-id="2aaf6-344">HDInsight 클러스터 버전 2.1은 웹 서비스의 버전 2를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-344">HDInsight cluster version 2.1 does not supports version 2 of the web services.</span></span>
10. <span data-ttu-id="2aaf6-345">**스크립트 실행**을 클릭하거나 **F5** 키를 눌러 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-345">Click **Run Script** or press **F5** to run the script.</span></span> <span data-ttu-id="2aaf6-346">다음과 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-346">The output will be similar to:</span></span>

     ![자습서 실행 워크플로 출력][img-runworkflow-output]
11. <span data-ttu-id="2aaf6-348">SQL 데이터베이스에 연결하여 내보낸 데이터를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-348">Connect to your SQL Database to see the exported data.</span></span>

<span data-ttu-id="2aaf6-349">**작업 오류 로그를 검사하려면**</span><span class="sxs-lookup"><span data-stu-id="2aaf6-349">**To check the job error log**</span></span>

<span data-ttu-id="2aaf6-350">워크플로 문제를 해결하기 위해 클러스터 headnode에서 C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log에 있는 Oozie 로그 파일을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-350">To troubleshoot a workflow, the Oozie log file can be found at C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log from the cluster headnode.</span></span> <span data-ttu-id="2aaf6-351">RDP에 대한 자세한 내용은 [Azure Portal을 사용하여 HDInsight 클러스터 관리][hdinsight-admin-portal]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-351">For information on RDP, see [Administering HDInsight clusters using the Azure portal][hdinsight-admin-portal].</span></span>

<span data-ttu-id="2aaf6-352">**자습서를 다시 실행하려면**</span><span class="sxs-lookup"><span data-stu-id="2aaf6-352">**To rerun the tutorial**</span></span>

<span data-ttu-id="2aaf6-353">워크플로를 다시 실행하려면 다음을 수행해야 합니다:</span><span class="sxs-lookup"><span data-stu-id="2aaf6-353">To rerun the workflow, you must perform the following tasks:</span></span>

* <span data-ttu-id="2aaf6-354">Hive 스크립트 출력 파일 삭제.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-354">Delete the Hive script output file.</span></span>
* <span data-ttu-id="2aaf6-355">log4jLogsCount 테이블의 데이터 삭제.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-355">Delete the data in the log4jLogsCount table.</span></span>

<span data-ttu-id="2aaf6-356">다음은 사용할 수 있는 Windows PowerShell 스크립트 샘플입니다:</span><span class="sxs-lookup"><span data-stu-id="2aaf6-356">Here is a sample Windows PowerShell script that you can use:</span></span>

```powershell
$storageAccountName = "<AzureStorageAccountName>"
$containerName = "<ContainerName>"

#SQL database variables
$sqlDatabaseServer = "<SQLDatabaseServerName>"
$sqlDatabaseLogin = "<SQLDatabaseLoginName>"
$sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>"
$sqlDatabaseName = "<SQLDatabaseName>"
$sqlDatabaseTableName = "log4jLogsCount"

Write-host "Delete the Hive script output file ..." -ForegroundColor Green
$storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
$destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey
Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $containerName

Write-host "Delete all the records from the log4jLogsCount table ..." -ForegroundColor Green
$conn = New-Object System.Data.SqlClient.SqlConnection
$conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
$conn.open()
$cmd = New-Object System.Data.SqlClient.SqlCommand
$cmd.connection = $conn
$cmd.commandtext = "delete from $sqlDatabaseTableName"
$cmd.executenonquery()

$conn.close()
```

## <a name="next-steps"></a><span data-ttu-id="2aaf6-357">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2aaf6-357">Next steps</span></span>
<span data-ttu-id="2aaf6-358">이 자습서에서는 Oozie 워크플로를 정의하는 방법, Oozie 코디네이터 및 Azure PowerShell을 사용하여 Oozie 코디네이터 작업을 실행하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-358">In this tutorial, you learned how to define an Oozie workflow and an Oozie coordinator, and how to run an Oozie coordinator job by using Azure PowerShell.</span></span> <span data-ttu-id="2aaf6-359">자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2aaf6-359">To learn more, see the following articles:</span></span>

* <span data-ttu-id="2aaf6-360">[HDInsight 시작][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="2aaf6-360">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="2aaf6-361">[HDInsight에서 Azure Blob Storage 사용][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="2aaf6-361">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="2aaf6-362">[Azure PowerShell을 사용하여 HDInsight 클러스터 관리][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="2aaf6-362">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="2aaf6-363">[HDInsight에 데이터 업로드][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="2aaf6-363">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="2aaf6-364">[HDInsight에서 Sqoop 사용][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="2aaf6-364">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="2aaf6-365">[HDInsight에서 Hive 사용][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="2aaf6-365">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="2aaf6-366">[HDInsight에서 Pig 사용][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="2aaf6-366">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="2aaf6-367">[HDInsight용 Java MapReduce 프로그램 개발][hdinsight-develop-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="2aaf6-367">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-java-mapreduce]</span></span>

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
