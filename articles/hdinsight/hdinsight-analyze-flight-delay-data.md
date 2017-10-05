---
title: "HDInsight에서 Hadoop을 사용하여 비행 지연 데이터 분석 - Azure | Microsoft Docs"
description: "하나의 Windows PowerShell 스크립트를 사용하여 HDInsight 클러스터를 만들고, Hive 작업을 실행하고, Sqoop 작업을 실행하고, 클러스터를 삭제하는 방법을 알아봅니다."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00e26aa9-82fb-4dbe-b87d-ffe8e39a5412
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 77790136c9bd3a4e3f7dcabea2fbe0bcffb6eafe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-in-hdinsight"></a><span data-ttu-id="2d714-103">HDInsight의 Hive를 사용하여 비행 지연 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="2d714-103">Analyze flight delay data by using Hive in HDInsight</span></span>
<span data-ttu-id="2d714-104">Hive에서는 대규모 데이터의 요약, 쿼리, 분석에 적용할 수 있는 SQL 스타일 스크립트 언어인 *[HiveQL][hadoop-hiveql]*을 통해 Hadoop MapReduce 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-104">Hive provides a means of running Hadoop MapReduce jobs through an SQL-like scripting language called *[HiveQL][hadoop-hiveql]*, which can be applied towards summarizing, querying, and analyzing large volumes of data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2d714-105">이 문서의 단계에는 Windows 기반 HDInsight 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-105">The steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="2d714-106">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2d714-107">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d714-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="2d714-108">Linux 기반 클러스터를 사용하는 단계는 [HDInsight에서 Hive를 사용하여 비행 지연 데이터 분석(Linux)](hdinsight-analyze-flight-delay-data-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d714-108">For steps that work with a Linux-based cluster, see [Analyze flight delay data by using Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).</span></span>

<span data-ttu-id="2d714-109">Azure HDInsight의 주요 이점 중 하나는 데이터 저장소와 계산 기능을 분리할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-109">One of the major benefits of Azure HDInsight is the separation of data storage and compute.</span></span> <span data-ttu-id="2d714-110">HDInsight는 데이터 저장소로 Azure Blob 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-110">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="2d714-111">일반적인 작업은 세 부분으로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-111">A typical job involves three parts:</span></span>

1. <span data-ttu-id="2d714-112">**Azure Blob 저장소에 데이터 저장.**</span><span class="sxs-lookup"><span data-stu-id="2d714-112">**Store data in Azure Blob storage.**</span></span>  <span data-ttu-id="2d714-113">예를 들어 날씨 데이터, 센서 데이터, 웹 로그 및 이 자습서의 경우 비행 지연 데이터를 Azure Blob 저장소에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-113">For example, weather data, sensor data, web logs, and in this case, flight delay data are saved into Azure Blob storage.</span></span>
2. <span data-ttu-id="2d714-114">**작업 실행**</span><span class="sxs-lookup"><span data-stu-id="2d714-114">**Run jobs.**</span></span> <span data-ttu-id="2d714-115">데이터를 처리해야 할 때는 Windows PowerShell 스크립트나 클라이언트 응용 프로그램을 실행하여 HDInsight 클러스터를 만들고 작업을 실행한 다음 클러스터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-115">When it is time to process the data, you run a Windows PowerShell script (or a client application) to create an HDInsight cluster, run jobs, and delete the cluster.</span></span> <span data-ttu-id="2d714-116">작업의 출력 데이터는 Azure Blob 저장소에 저장되며</span><span class="sxs-lookup"><span data-stu-id="2d714-116">The jobs save output data to Azure Blob storage.</span></span> <span data-ttu-id="2d714-117">클러스터가 삭제된 후에도 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-117">The output data is retained even after the cluster is deleted.</span></span> <span data-ttu-id="2d714-118">따라서 사용한 데이터에 대해서만 비용을 지불하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-118">This way, you pay for only what you have consumed.</span></span>
3. <span data-ttu-id="2d714-119">**Azure Blob 저장소에서 출력을 검색**하거나 이 자습서에 설명된 것처럼 데이터를 Azure SQL 데이터베이스로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-119">**Retrieve the output from Azure Blob storage**, or in this tutorial, export the data to an Azure SQL database.</span></span>

<span data-ttu-id="2d714-120">아래 다이어그램에는 이 자습서에서 설명하는 시나리오와 구조가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-120">The following diagram illustrates the scenario and the structure of this tutorial:</span></span>

![HDI.FlightDelays.flow][img-hdi-flightdelays-flow]

<span data-ttu-id="2d714-122">다이어그램의 숫자는 섹션 제목에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-122">Note that the numbers in the diagram correspond to the section titles.</span></span> <span data-ttu-id="2d714-123">**M** 은 주 프로세스의 약어입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-123">**M** stands for the main process.</span></span> <span data-ttu-id="2d714-124">**A** 는 부록 콘텐츠의 약어입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-124">**A** stands for the content in the appendix.</span></span>

<span data-ttu-id="2d714-125">자습서에서는 주로 Windows PowerShell 스크립트를 사용하여 다음 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-125">The main portion of the tutorial shows you how to use one Windows PowerShell script to perform the following tasks:</span></span>

* <span data-ttu-id="2d714-126">HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="2d714-126">Create an HDInsight cluster.</span></span>
* <span data-ttu-id="2d714-127">클러스터에서 Hive 작업을 실행하여 공항에서의 평균 지연 계산.</span><span class="sxs-lookup"><span data-stu-id="2d714-127">Run a Hive job on the cluster to calculate average delays at airports.</span></span> <span data-ttu-id="2d714-128">비행 지연 데이터는 Azure Blob 저장소 계정에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-128">The flight delay data is stored in an Azure Blob storage account.</span></span>
* <span data-ttu-id="2d714-129">Sqoop작업을 실행하여 Azure SQL 데이터베이스로 Hive 작업 출력 내보내기</span><span class="sxs-lookup"><span data-stu-id="2d714-129">Run a Sqoop job to export the Hive job output to an Azure SQL database.</span></span>
* <span data-ttu-id="2d714-130">HDInsight 클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="2d714-130">Delete the HDInsight cluster.</span></span>

<span data-ttu-id="2d714-131">부록에서 비행 지연 데이터를 업로드하고, Hive 쿼리 문자열을 만들기/업로드하고, Azure SQL 데이터베이스에서 Sqoop 작업을 준비하기 위한 지침을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-131">In the appendixes, you can find the instructions for uploading flight delay data, creating/uploading a Hive query string, and preparing the Azure SQL database for the Sqoop job.</span></span>

> [!NOTE]
> <span data-ttu-id="2d714-132">이 문서의 단계는 Windows 기반 HDInsight 클러스터를 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-132">The steps in this document are specific to Windows-based HDInsight clusters.</span></span> <span data-ttu-id="2d714-133">Linux 기반 클러스터를 사용하는 단계는 [HDInsight에서 Hive를 사용하여 비행 지연 데이터 분석(Linux)](hdinsight-analyze-flight-delay-data-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d714-133">For steps that work with a Linux-based cluster, see [Analyze flight delay data using Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md)</span></span>

### <a name="prerequisites"></a><span data-ttu-id="2d714-134">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2d714-134">Prerequisites</span></span>
<span data-ttu-id="2d714-135">이 자습서를 시작하기 전에 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-135">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="2d714-136">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="2d714-136">**An Azure subscription**.</span></span> <span data-ttu-id="2d714-137">[Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d714-137">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="2d714-138">**Azure PowerShell이 포함된 워크스테이션**.</span><span class="sxs-lookup"><span data-stu-id="2d714-138">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2d714-139">Azure Service Manager를 사용하여 HDInsight 리소스를 관리하는 Azure PowerShell 지원은 더 이상 **지원되지 않고** 2017년 1월 1일에 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-139">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="2d714-140">이 문서의 단계에서는 Azure Resource Manager로 작동하는 새 HDInsight cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-140">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="2d714-141">[Azure PowerShell 설치 및 구성](/powershell/azureps-cmdlets-docs) 단계를 수행하여 최신 버전의 Azure PowerShell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-141">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="2d714-142">Azure Resource Manager로 작동하는 새로운 cmdlet을 사용하도록 수정해야 하는 스크립트가 있는 경우 자세한 내용은 [HDInsight 클러스터에 대한 Azure Resource Manager 기반 개발 도구에 마이그레이션](hdinsight-hadoop-development-using-azure-resource-manager.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d714-142">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

<span data-ttu-id="2d714-143">**이 자습서에서 사용하는 파일**</span><span class="sxs-lookup"><span data-stu-id="2d714-143">**Files used in this tutorial**</span></span>

<span data-ttu-id="2d714-144">이 자습서에서는 [Research and Innovative Technology Administration, Bureau of Transportation Statistics or RITA][rita-website](영문)의 항공사 비행 데이터 운항정시성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-144">This tutorial uses the on-time performance of airline flight data from [Research and Innovative Technology Administration, Bureau of Transportation Statistics or RITA][rita-website].</span></span>
<span data-ttu-id="2d714-145">데이터의 복사본은 공용 Blob 액세스 권한을 사용하여 Azure Blob 저장소 컨테이너에 업로드되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-145">A copy of the data has been uploaded to an Azure Blob storage container with the Public Blob access permission.</span></span>
<span data-ttu-id="2d714-146">PowerShell 스크립트의 일부는 데이터를 공용 blob 컨테이너에서 클러스터의 기본 blob 컨테이너로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-146">A part of your PowerShell script copies the data from the public blob container to the default blob container of your cluster.</span></span> <span data-ttu-id="2d714-147">HiveQL 스크립트도 같은 Blob 컨테이너에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-147">The HiveQL script is also copied to the same Blob container.</span></span>
<span data-ttu-id="2d714-148">자체 저장소 계정으로 데이터를 가져오고 업로드하는 방법과 HiveQL 스크립트 파일을 만들고 업로드하는 방법을 알아보려면 [부록 A](#appendix-a)와 [부록 B](#appendix-b)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d714-148">If you want to learn how to get/upload the data to your own Storage account, and how to create/upload the HiveQL script file, see [Appendix A](#appendix-a) and [Appendix B](#appendix-b).</span></span>

<span data-ttu-id="2d714-149">다음 표는 이 자습서에 사용된 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-149">The following table lists the files used in this tutorial:</span></span>

<table border="1">
<tr><th><span data-ttu-id="2d714-150">파일</span><span class="sxs-lookup"><span data-stu-id="2d714-150">Files</span></span></th><th><span data-ttu-id="2d714-151">설명</span><span class="sxs-lookup"><span data-stu-id="2d714-151">Description</span></span></th></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/flightdelays.hql</td><td><span data-ttu-id="2d714-152">Hive 작업에 사용되는 HiveQL 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-152">The HiveQL script file used by the Hive job.</span></span> <span data-ttu-id="2d714-153">이 스크립트는 공용 Blob 액세스 권한을 사용하여 Azure Blob 저장소 계정에 업로드되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-153">This script has been uploaded to an Azure Blob storage account with the public access.</span></span> <span data-ttu-id="2d714-154"><a href="#appendix-b">부록 B</a>에는 이 파일을 준비하고 고유한 Azure Blob 저장소 계정에 업로드하는 방법에 대한 지침이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-154"><a href="#appendix-b">Appendix B</a> has instructions on preparing and uploading this file to your own Azure Blob storage account.</span></span></td></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data</td><td><span data-ttu-id="2d714-155">Hive 작업의 입력 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-155">Input data for the Hive job.</span></span> <span data-ttu-id="2d714-156">이 데이터는 공용 액세스 권한을 사용하여 Azure Blob 저장소 계정에 업로드되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-156">The data has been uploaded to an Azure Blob storage account with the public access.</span></span> <span data-ttu-id="2d714-157"><a href="#appendix-a">부록 A</a>에는 데이터를 가져오기 고유한 Azure Blob 저장소 계정에 업로드하는 방법에 대한 지침이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-157"><a href="#appendix-a">Appendix A</a> has instructions on getting the data and uploading the data to your own Azure Blob storage account.</span></span></td></tr>
<tr><td><span data-ttu-id="2d714-158">\tutorials\flightdelays\output</span><span class="sxs-lookup"><span data-stu-id="2d714-158">\tutorials\flightdelays\output</span></span></td><td><span data-ttu-id="2d714-159">Hive 작업의 출력 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-159">The output path for the Hive job.</span></span> <span data-ttu-id="2d714-160">기본 컨테이너를 사용하여 출력 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-160">The default container is used for storing the output data.</span></span></td></tr>
<tr><td><span data-ttu-id="2d714-161">\tutorials\flightdelays\jobstatus</span><span class="sxs-lookup"><span data-stu-id="2d714-161">\tutorials\flightdelays\jobstatus</span></span></td><td><span data-ttu-id="2d714-162">기본 컨테이너의 Hive 작업 상태 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-162">The Hive job status folder on the default container.</span></span></td></tr>
</table>

## <a name="create-cluster-and-run-hivesqoop-jobs"></a><span data-ttu-id="2d714-163">클러스터 만들기 및 Hive/Sqoop 작업 실행</span><span class="sxs-lookup"><span data-stu-id="2d714-163">Create cluster and run Hive/Sqoop jobs</span></span>
<span data-ttu-id="2d714-164">Hadoop MapReduce에서는 작업을 일괄 처리 방식으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-164">Hadoop MapReduce is batch processing.</span></span> <span data-ttu-id="2d714-165">가장 비용 효율적으로 Hive 작업을 실행하는 방법은 작업의 클러스터를 만들고 완료된 작업은 삭제하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-165">The most cost-effective way to run a Hive job is to create a cluster for the job, and delete the job after the job is completed.</span></span> <span data-ttu-id="2d714-166">다음 스크립트에 전체 프로세스가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-166">The following script covers the whole process.</span></span>
<span data-ttu-id="2d714-167">HDInsight 클러스터를 만들고 Hive 작업을 실행하는 방법에 대한 자세한 내용은 [HDInsight에서 Hadoop 클러스터 만들기][hdinsight-provision] 및 [HDInsight에서 Hive 사용][hdinsight-use-hive]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d714-167">For more information on creating an HDInsight cluster and running Hive jobs, see [Create Hadoop clusters in HDInsight][hdinsight-provision] and [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

<span data-ttu-id="2d714-168">**Azure PowerShell로 Hive 쿼리를 실행하려면**</span><span class="sxs-lookup"><span data-stu-id="2d714-168">**To run the Hive queries by Azure PowerShell**</span></span>

1. <span data-ttu-id="2d714-169">[부록 C](#appendix-c)의 지침에 따라 Azure SQL 데이터베이스 및 Sqoop 작업 출력 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-169">Create an Azure SQL database and the table for the Sqoop job output by using the instructions in [Appendix C](#appendix-c).</span></span>
2. <span data-ttu-id="2d714-170">Windows PowerShell ISE를 열고 다음 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-170">Open Windows PowerShell ISE, and run the following script:</span></span>

    ```powershell
    $subscriptionID = "<Azure Subscription ID>"
    $nameToken = "<Enter an Alias>"

    ###########################################
    # You must configure the follwing variables
    # for an existing Azure SQL Database
    ###########################################
    $existingSqlDatabaseServerName = "<Azure SQL Database Server>"
    $existingSqlDatabaseLogin = "<Azure SQL Database Server Login>"
    $existingSqlDatabasePassword = "<Azure SQL Database Server login password>"
    $existingSqlDatabaseName = "<Azure SQL Database name>"

    $localFolder = "E:\Tutorials\Downloads\" # A temp location for copying files.
    $azcopyPath = "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy" # depends on the version, the folder can be different

    ###########################################
    # (Optional) configure the following variables
    ###########################################

    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2"

    $HDInsightClusterName = $namePrefix + "hdi"
    $httpUserName = "admin"
    $httpPassword = "<Enter the Password>"

    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $HDInsightClusterName # use the cluster name

    $existingSqlDatabaseTableName = "AvgDelays"
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$existingSqlDatabaseServerName.database.windows.net;user=$existingSqlDatabaseLogin@$existingSqlDatabaseServerName;password=$existingSqlDatabaseLogin;database=$existingSqlDatabaseName"

    $hqlScriptFile = "/tutorials/flightdelays/flightdelays.hql"

    $jobStatusFolder = "/tutorials/flightdelays/jobstatus"

    ###########################################
    # Login
    ###########################################
    try{
        $acct = Get-AzureRmSubscription
    }
    catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionID $subscriptionID

    ###########################################
    # Create a new HDInsight cluster
    ###########################################

    # Create ARM group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create the default storage account
    New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName -Location $location -Type Standard_LRS

    # Create the default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer -Name $defaultBlobContainerName -Context $defaultStorageAccountContext

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
        -DefaultStorageContainer $existingDefaultBlobContainerName

    ###########################################
    # Prepare the HiveQL script and source data
    ###########################################

    # Create the temp location
    New-Item -Path $localFolder -ItemType Directory -Force

    # Download the sample file from Azure Blob storage
    $context = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous
    $blobs = Get-AzureStorageBlob -Container "flightdelay" -Context $context
    #$blobs | Get-AzureStorageBlobContent -Context $context -Destination $localFolder

    # Upload data to default container

    $azcopycmd = "cmd.exe /C '$azcopyPath\azcopy.exe' /S /Source:'$localFolder' /Dest:'https://$defaultStorageAccountName.blob.core.windows.net/$defaultBlobContainerName/tutorials/flightdelays' /DestKey:$defaultStorageAccountKey"

    Invoke-Expression -Command:$azcopycmd

    ###########################################
    # Submit the Hive job
    ###########################################
    Use-AzureRmHDInsightCluster -ClusterName $HDInsightClusterName -HttpCredential $httpCredential
    $response = Invoke-AzureRmHDInsightHiveJob `
                    -Files $hqlScriptFile `
                    -DefaultContainer $defaultBlobContainerName `
                    -DefaultStorageAccountName $defaultStorageAccountName `
                    -DefaultStorageAccountKey $defaultStorageAccountKey `
                    -StatusFolder $jobStatusFolder

    write-Host $response

    ###########################################
    # Submit the Sqoop job
    ###########################################
    $exportDir = "wasb://$defaultBlobContainerName@$defaultStorageAccountName.blob.core.windows.net/tutorials/flightdelays/output"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
                    -Command "export --connect $sqlDatabaseConnectionString --table $sqlDatabaseTableName --export-dir $exportDir --fields-terminated-by \001 "
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ResourceGroupName $resourceGroupName `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -HttpCredential $httpCredential `
        -WaitTimeoutInSeconds 3600 `
        -Job $sqoopJob.JobId

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -DefaultContainer $existingDefaultBlobContainerName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    ###########################################
    # Delete the cluster
    ###########################################
    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName
    ```
3. <span data-ttu-id="2d714-171">SQL 데이터베이스에 연결하고 AvgDelays 테이블에서 도시별 평균 비행 지연을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-171">Connect to your SQL database and see average flight delays by city in the AvgDelays table:</span></span>

    ![HDI.FlightDelays.AvgDelays.Dataset][image-hdi-flightdelays-avgdelays-dataset]

- - -

## <span data-ttu-id="2d714-173"><a id="appendix-a"></a>부록 A - Azure Blob 저장소에 비행 지연 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="2d714-173"><a id="appendix-a"></a>Appendix A - Upload flight delay data to Azure Blob storage</span></span>
<span data-ttu-id="2d714-174">데이터 파일과 HiveQL 스크립트 파일을 업로드하려면( [부록 B](#appendix-b)참조) 약간의 계획이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-174">Uploading the data file and the HiveQL script files (see [Appendix B](#appendix-b)) requires some planning.</span></span> <span data-ttu-id="2d714-175">그 계획은 HDInsight 클러스터를 만들고 Hive 작업을 실행하기 전에 데이터 파일과 HiveQL 파일을 저장하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-175">The idea is to store the data files and the HiveQL file before creating an HDInsight cluster and running the Hive job.</span></span> <span data-ttu-id="2d714-176">다음 두 가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-176">You have two options:</span></span>

* <span data-ttu-id="2d714-177">**HDInsight 클러스터에서 기본 파일 시스템으로 사용하는 것과 같은 Azure 저장소 계정을 사용합니다.**</span><span class="sxs-lookup"><span data-stu-id="2d714-177">**Use the same Azure Storage account that will be used by the HDInsight cluster as the default file system.**</span></span> <span data-ttu-id="2d714-178">HDInsight 클러스터에는 저장소 계정 액세스 키가 포함되므로 추가로 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-178">Because the HDInsight cluster will have the Storage account access key, you don't need to make any additional changes.</span></span>
* <span data-ttu-id="2d714-179">**HDInsight 클러스터 기본 파일 시스템과 다른 Azure 저장소 계정을 사용합니다.**</span><span class="sxs-lookup"><span data-stu-id="2d714-179">**Use a different Azure Storage account from the HDInsight cluster default file system.**</span></span> <span data-ttu-id="2d714-180">이 경우 [HDInsight 클러스터 만들기 및 Hive/Sqoop 작업 실행](#runjob) 에 있는 Windows PowerShell 스크립트의 생성 부분을 수정하여 저장소 계정을 추가 저장소 계정으로서 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-180">If this is the case, you must modify the creation part of the Windows PowerShell script found in [Create HDInsight cluster and run Hive/Sqoop jobs](#runjob) to link the Storage account as an additional Storage account.</span></span> <span data-ttu-id="2d714-181">자세한 내용은 [HDInsight에서 Hadoop 클러스터 만들기][hdinsight-provision]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d714-181">For instructions, see [Create Hadoop clusters in HDInsight][hdinsight-provision].</span></span> <span data-ttu-id="2d714-182">그러면 HDInsight 클러스터가 저장소 계정의 액세스 키를 인식합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-182">The HDInsight cluster then knows the access key for the Storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="2d714-183">데이터 파일의 Blob 저장소 경로는 HiveQL 스크립트 파일에 하드 코드됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-183">The Blob storage path for the data file is hard coded in the HiveQL script file.</span></span> <span data-ttu-id="2d714-184">수정 내용에 따라 이를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-184">You must update it accordingly.</span></span>

<span data-ttu-id="2d714-185">**비행 데이터를 다운로드하려면**</span><span class="sxs-lookup"><span data-stu-id="2d714-185">**To download the flight data**</span></span>

1. <span data-ttu-id="2d714-186">[Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website](영문)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-186">Browse to [Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>
2. <span data-ttu-id="2d714-187">페이지에서 다음 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-187">On the page, select the following values:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="2d714-188">이름</span><span class="sxs-lookup"><span data-stu-id="2d714-188">Name</span></span></th><th><span data-ttu-id="2d714-189">값</span><span class="sxs-lookup"><span data-stu-id="2d714-189">Value</span></span></th></tr>
    <tr><td><span data-ttu-id="2d714-190">Filter Year</span><span class="sxs-lookup"><span data-stu-id="2d714-190">Filter Year</span></span></td><td><span data-ttu-id="2d714-191">2013</span><span class="sxs-lookup"><span data-stu-id="2d714-191">2013</span></span> </td></tr>
    <tr><td><span data-ttu-id="2d714-192">Filter Period</span><span class="sxs-lookup"><span data-stu-id="2d714-192">Filter Period</span></span></td><td><span data-ttu-id="2d714-193">January</span><span class="sxs-lookup"><span data-stu-id="2d714-193">January</span></span></td></tr>
    <tr><td><span data-ttu-id="2d714-194">필드</span><span class="sxs-lookup"><span data-stu-id="2d714-194">Fields</span></span></td><td><span data-ttu-id="2d714-195">*Year*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *Origin*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*, *LateAircraftDelay*(다른 모든 필드는 선택하지 않음)</span><span class="sxs-lookup"><span data-stu-id="2d714-195">*Year*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *Origin*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (clear all other fields)</span></span></td></tr>
    </table><span data-ttu-id="2d714-196">
3. **다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-196">
3. Click **Download**.</span></span>
<span data-ttu-id="2d714-197">4.</span><span class="sxs-lookup"><span data-stu-id="2d714-197">4.</span></span> <span data-ttu-id="2d714-198">압축 파일을 **C:\Tutorials\FlightDelays\2013Data** 폴더에 풉니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-198">Unzip the file to the **C:\Tutorials\FlightDelay\2013Data** folder.</span></span> <span data-ttu-id="2d714-199">각 파일은 CSV 파일이며 크기가 60GB 정도입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-199">Each file is a CSV file and is approximately 60GB in size.</span></span>
<span data-ttu-id="2d714-200">5.</span><span class="sxs-lookup"><span data-stu-id="2d714-200">5.</span></span> <span data-ttu-id="2d714-201">파일 이름을 데이터가 포함된 달로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-201">Rename the file to the name of the month that it contains data for.</span></span> <span data-ttu-id="2d714-202">예를 들어 1월 데이터가 포함된 파일의 이름은 *January.csv*가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-202">For example, the file containing the January data would be named *January.csv*.</span></span>
<span data-ttu-id="2d714-203">6.</span><span class="sxs-lookup"><span data-stu-id="2d714-203">6.</span></span> <span data-ttu-id="2d714-204">2단계와 5단계를 반복하여 2013년의 12개월에 해당하는 각 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-204">Repeat steps 2 and 5 to download a file for each of the 12 months in 2013.</span></span> <span data-ttu-id="2d714-205">자습서를 실행하려면 파일이 하나 이상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-205">You will need a minimum of one file to run the tutorial.</span></span>

<span data-ttu-id="2d714-206">**Azure Blob 저장소에 비행 지연 데이터를 업로드하려면**</span><span class="sxs-lookup"><span data-stu-id="2d714-206">**To upload the flight delay data to Azure Blob storage**</span></span>

1. <span data-ttu-id="2d714-207">매개 변수를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-207">Prepare the parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="2d714-208">변수 이름</span><span class="sxs-lookup"><span data-stu-id="2d714-208">Variable Name</span></span></th><th><span data-ttu-id="2d714-209">참고 사항</span><span class="sxs-lookup"><span data-stu-id="2d714-209">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="2d714-210">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="2d714-210">$storageAccountName</span></span></td><td><span data-ttu-id="2d714-211">데이터를 업로드할 Azure 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-211">The Azure Storage account where you want to upload the data to.</span></span></td></tr>
    <tr><td><span data-ttu-id="2d714-212">$blobContainerName</span><span class="sxs-lookup"><span data-stu-id="2d714-212">$blobContainerName</span></span></td><td><span data-ttu-id="2d714-213">데이터를 업로드할 Blob 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-213">The Blob container where you want to upload the data to.</span></span></td></tr>
    </table>
2. <span data-ttu-id="2d714-214">Azure PowerShell ISE를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-214">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="2d714-215">3.</span><span class="sxs-lookup"><span data-stu-id="2d714-215">3.</span></span> <span data-ttu-id="2d714-216">다음 스크립트를 스크립트 창에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-216">Paste the following script into the script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter the Azure storage account name for creating a new HDInsight cluster. If the account doesn't exist, the script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter the Azure blob container name for creating a new HDInsight cluster. If not specified, the HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #Region - Variables
    $localFolder = "C:\Tutorials\FlightDelay\2013Data"  # The source folder
    $destFolder = "tutorials/flightdelay/2013data"     #The blob name prefix for the files to be uploaded
    #EndRegion

    #Region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating the Azure Storage account and the Blob container..." -ForegroundColor Green
    # Validate the Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "The storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate the container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "The Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #Region - Copy the file from local workstation to Azure Blob storage
    if (test-path -Path $localFolder)
    {
        foreach ($item in Get-ChildItem -Path $localFolder){
            $fileName = "$localFolder\$item"
            $blobName = "$destFolder/$item"

            Write-Host "Copying $fileName to $blobName" -ForegroundColor Green

            Set-AzureStorageBlobContent -File $fileName -Container $blobContainerName -Blob $blobName -Context $storageContext
        }
    }
    else
    {
        Write-Host "The source folder on the workstation doesn't exist" -ForegroundColor Red
    }

    # List the uploaded files on HDInsight
    Get-AzureStorageBlob -Container $blobContainerName  -Context $storageContext -Prefix $destFolder
    #EndRegion
    ```
4. <span data-ttu-id="2d714-217">**F5** 키를 눌러 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-217">Press **F5** to run the script.</span></span>

<span data-ttu-id="2d714-218">다른 메서드를 사용하여 파일을 업로드하도록 선택한 경우에는 파일 경로가 tutorials/flightdelay/data여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-218">If you choose to use a different method for uploading the files, please make sure the file path is tutorials/flightdelay/data.</span></span> <span data-ttu-id="2d714-219">파일을 액세스하는 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-219">The syntax for accessing the files is:</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/tutorials/flightdelay/data

<span data-ttu-id="2d714-220">tutorials/flightdelay/data 경로는 파일을 업로드했을 때 만든 가상 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-220">The path tutorials/flightdelay/data is the virtual folder you created when you uploaded the files.</span></span> <span data-ttu-id="2d714-221">달마다 하나씩 12개의 파일이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-221">Verify that there are 12 files, one for each month.</span></span>

> [!NOTE]
> <span data-ttu-id="2d714-222">새 위치에서 읽으려면 Hive 쿼리를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-222">You must update the Hive query to read from the new location.</span></span>
>
> <span data-ttu-id="2d714-223">컨테이너 액세스 권한을 공용으로 구성하거나 저장소 계정을 HDInsight 클러스터에 바인딩해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-223">You must either configure the container access permission to be public or bind the Storage account to the HDInsight cluster.</span></span> <span data-ttu-id="2d714-224">그렇지 않으면 Hive 쿼리 문자열이 데이터 파일에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-224">Otherwise, the Hive query string will not be able to access the data files.</span></span>

- - -

## <span data-ttu-id="2d714-225"><a id="appendix-b"></a>부록 B - HiveQL 스크립트 만들기 및 업로드</span><span class="sxs-lookup"><span data-stu-id="2d714-225"><a id="appendix-b"></a>Appendix B - Create and upload a HiveQL script</span></span>
<span data-ttu-id="2d714-226">Azure PowerShell을 사용하여 여러 HiveQL 문을 한 번에 하나씩 실행하거나 HiveQL 문을 스크립트 파일에 패키지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-226">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package the HiveQL statement into a script file.</span></span> <span data-ttu-id="2d714-227">이 섹션에서는 HiveQL 스크립트를 만든 다음 Azure PowerShell을 사용하여 Azure Blob 저장소에 업로드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-227">This section shows you how to create a HiveQL script and upload the script to Azure Blob storage by using Azure PowerShell.</span></span> <span data-ttu-id="2d714-228">Hive에서는 HiveQL 스크립트를 Azure Blob 저장소에 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-228">Hive requires the HiveQL scripts to be stored in Azure Blob storage.</span></span>

<span data-ttu-id="2d714-229">HiveQL 스크립트는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-229">The HiveQL script will perform the following:</span></span>

1. <span data-ttu-id="2d714-230">**delays_raw 테이블을 삭제합니다**. 해당 테이블이 이미 있는 경우에 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-230">**Drop the delays_raw table**, in case the table already exists.</span></span>
2. <span data-ttu-id="2d714-231">**delays_raw 외부 Hive 테이블을 만듭니다**. 이 테이블은 비행 지연 파일이 있는 Blob 저장소 위치를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-231">**Create the delays_raw external Hive table** pointing to the Blob storage location with the flight delay files.</span></span> <span data-ttu-id="2d714-232">이 쿼리는 필드는 ","로 구분되고 줄은 "\n"로 끝나도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-232">This query specifies that fields are delimited by "," and that lines are terminated by "\n".</span></span> <span data-ttu-id="2d714-233">Hive가 필드 구분 기호인 쉼표와 필드 값(ORIGIN\_CITY\_NAME 및 DEST\_CITY\_NAME에 대한 필드 값의 경우)의 일부인 쉼표를 구분할 수 없기 때문에 필드 값에 쉼표가 포함될 경우 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-233">This poses a problem when field values contain commas because Hive cannot differentiate between a comma that is a field delimiter and a one that is part of a field value (which is the case in field values for ORIGIN\_CITY\_NAME and DEST\_CITY\_NAME).</span></span> <span data-ttu-id="2d714-234">이 문제를 해결하기 위해 쿼리는 TEMP 열을 만들어 열에 잘못 분할된 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-234">To address this, the query creates TEMP columns to hold data that is incorrectly split into columns.</span></span>
3. <span data-ttu-id="2d714-235">해당 테이블이 이미 있는 경우 **delays 테이블을 삭제합니다.**</span><span class="sxs-lookup"><span data-stu-id="2d714-235">**Drop the delays table**, in case the table already exists.</span></span>
4. <span data-ttu-id="2d714-236">**delays 테이블을 만듭니다**.</span><span class="sxs-lookup"><span data-stu-id="2d714-236">**Create the delays table**.</span></span> <span data-ttu-id="2d714-237">더 처리하기 전에 데이터를 정리하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-237">It is helpful to clean up the data before further processing.</span></span> <span data-ttu-id="2d714-238">이 쿼리는 delays_raw 테이블에서 새 테이블인 *delays*를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-238">This query creates a new table, *delays*, from the delays_raw table.</span></span> <span data-ttu-id="2d714-239">TEMP 열(앞에서 언급함)은 복사되지 않으며, **substring** 함수는 해당 데이터에서 따옴표를 제거하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-239">Note that the TEMP columns (as mentioned previously) are not copied, and that the **substring** function is used to remove quotation marks from the data.</span></span>
5. <span data-ttu-id="2d714-240">**평균 날씨 지연을 계산하고 그 결과를 도시 이름별로 그룹화합니다.**</span><span class="sxs-lookup"><span data-stu-id="2d714-240">**Compute the average weather delay and groups the results by city name.**</span></span> <span data-ttu-id="2d714-241">또한 결과를 Blob 저장소에 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-241">It will also output the results to Blob storage.</span></span> <span data-ttu-id="2d714-242">쿼리에서 데이터의 아포스트로피가 제거되고 **weather_delay**의 값이 null인 행은 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-242">Note that the query will remove apostrophes from the data and will exclude rows where the value for **weather_delay** is null.</span></span> <span data-ttu-id="2d714-243">이 작업은 이 자습서의 뒷부분에서 사용되는 Sqoop가 기본적으로 이러한 값을 정상적으로 처리하지 않기 때문에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-243">This is necessary because Sqoop, used later in this tutorial, doesn't handle those values gracefully by default.</span></span>

<span data-ttu-id="2d714-244">HiveQL 명령의 전체 목록을 보려면 [Hive 데이터 정의 언어][hadoop-hiveql](영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d714-244">For a full list of the HiveQL commands, see [Hive Data Definition Language][hadoop-hiveql].</span></span> <span data-ttu-id="2d714-245">각 HiveQL 명령은 세미콜론으로 끝나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-245">Each HiveQL command must terminate with a semicolon.</span></span>

<span data-ttu-id="2d714-246">**HiveQL 스크립트 파일을 만들려면**</span><span class="sxs-lookup"><span data-stu-id="2d714-246">**To create a HiveQL script file**</span></span>

1. <span data-ttu-id="2d714-247">매개 변수를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-247">Prepare the parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="2d714-248">변수 이름</span><span class="sxs-lookup"><span data-stu-id="2d714-248">Variable Name</span></span></th><th><span data-ttu-id="2d714-249">참고 사항</span><span class="sxs-lookup"><span data-stu-id="2d714-249">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="2d714-250">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="2d714-250">$storageAccountName</span></span></td><td><span data-ttu-id="2d714-251">HiveQL 스크립트를 업로드할 Azure 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-251">The Azure Storage account where you want to upload the HiveQL script to.</span></span></td></tr>
    <tr><td><span data-ttu-id="2d714-252">$blobContainerName</span><span class="sxs-lookup"><span data-stu-id="2d714-252">$blobContainerName</span></span></td><td><span data-ttu-id="2d714-253">HiveQL 스크립트를 업로드할 Blob 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-253">The Blob container where you want to upload the HiveQL script to.</span></span></td></tr>
    </table>
2. <span data-ttu-id="2d714-254">Azure PowerShell ISE를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-254">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="2d714-255">3.</span><span class="sxs-lookup"><span data-stu-id="2d714-255">3.</span></span> <span data-ttu-id="2d714-256">다음 스크립트를 복사하여 스크립트 창에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-256">Copy and paste the following script into the script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Blob storage variables
        [Parameter(Mandatory=$True,
                    HelpMessage="Enter the Azure storage account name for creating a new HDInsight cluster. If the account doesn't exist, the script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter the Azure blob container name for creating a new HDInsight cluster. If not specified, the HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #region - Define variables
    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    # The HiveQL script file is exported as this file before it's uploaded to Blob storage
    $hqlLocalFileName = "e:\tutorials\flightdelay\flightdelays.hql"

    # The HiveQL script file will be uploaded to Blob storage as this blob name
    $hqlBlobName = "tutorials/flightdelay/flightdelays.hql"

    # These two constants are used by the HiveQL script file
    #$srcDataFolder = "tutorials/flightdelay/data"
    $dstDataFolder = "/tutorials/flightdelay/output"
    #endregion

    #Region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating the Azure Storage account and the Blob container..." -ForegroundColor Green
    # Validate the Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "The storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate the container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "The Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #region - Validate the file and file path

    # Check if a file with the same file name already exists on the workstation
    Write-Host "`nvalidating the folder structure on the workstation for saving the HQL script file ..."  -ForegroundColor Green
    if (test-path $hqlLocalFileName){

        $isDelete = Read-Host 'The file, ' $hqlLocalFileName ', exists.  Do you want to overwirte it? (Y/N)'

        if ($isDelete.ToLower() -ne "y")
        {
            Exit
        }
    }

    # Create the folder if it doesn't exist
    $folder = split-path $hqlLocalFileName
    if (-not (test-path $folder))
    {
        Write-Host "`nCreating folder, $folder ..." -ForegroundColor Green

        new-item $folder -ItemType directory
    }
    #end region

    #region - Write the Hive script into a local file
    Write-Host "`nWriting the Hive script into a file on your workstation ..." `
                -ForegroundColor Green

    $hqlDropDelaysRaw = "DROP TABLE delays_raw;"

    $hqlCreateDelaysRaw = "CREATE EXTERNAL TABLE delays_raw (" +
            "YEAR string, " +
            "FL_DATE string, " +
            "UNIQUE_CARRIER string, " +
            "CARRIER string, " +
            "FL_NUM string, " +
            "ORIGIN_AIRPORT_ID string, " +
            "ORIGIN string, " +
            "ORIGIN_CITY_NAME string, " +
            "ORIGIN_CITY_NAME_TEMP string, " +
            "ORIGIN_STATE_ABR string, " +
            "DEST_AIRPORT_ID string, " +
            "DEST string, " +
            "DEST_CITY_NAME string, " +
            "DEST_CITY_NAME_TEMP string, " +
            "DEST_STATE_ABR string, " +
            "DEP_DELAY_NEW float, " +
            "ARR_DELAY_NEW float, " +
            "CARRIER_DELAY float, " +
            "WEATHER_DELAY float, " +
            "NAS_DELAY float, " +
            "SECURITY_DELAY float, " +
            "LATE_AIRCRAFT_DELAY float) " +
        "ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' " +
        "LINES TERMINATED BY '\n' " +
        "STORED AS TEXTFILE " +
        "LOCATION 'wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data';"

    $hqlDropDelays = "DROP TABLE delays;"

    $hqlCreateDelays = "CREATE TABLE delays AS " +
        "SELECT YEAR AS year, " +
            "FL_DATE AS flight_date, " +
            "substring(UNIQUE_CARRIER, 2, length(UNIQUE_CARRIER) -1) AS unique_carrier, " +
            "substring(CARRIER, 2, length(CARRIER) -1) AS carrier, " +
            "substring(FL_NUM, 2, length(FL_NUM) -1) AS flight_num, " +
            "ORIGIN_AIRPORT_ID AS origin_airport_id, " +
            "substring(ORIGIN, 2, length(ORIGIN) -1) AS origin_airport_code, " +
            "substring(ORIGIN_CITY_NAME, 2) AS origin_city_name, " +
            "substring(ORIGIN_STATE_ABR, 2, length(ORIGIN_STATE_ABR) -1)  AS origin_state_abr, " +
            "DEST_AIRPORT_ID AS dest_airport_id, " +
            "substring(DEST, 2, length(DEST) -1) AS dest_airport_code, " +
            "substring(DEST_CITY_NAME,2) AS dest_city_name, " +
            "substring(DEST_STATE_ABR, 2, length(DEST_STATE_ABR) -1) AS dest_state_abr, " +
            "DEP_DELAY_NEW AS dep_delay_new, " +
            "ARR_DELAY_NEW AS arr_delay_new, " +
            "CARRIER_DELAY AS carrier_delay, " +
            "WEATHER_DELAY AS weather_delay, " +
            "NAS_DELAY AS nas_delay, " +
            "SECURITY_DELAY AS security_delay, " +
            "LATE_AIRCRAFT_DELAY AS late_aircraft_delay " +
        "FROM delays_raw;"

    $hqlInsertLocal = "INSERT OVERWRITE DIRECTORY '$dstDataFolder' " +
        "SELECT regexp_replace(origin_city_name, '''', ''), " +
            "avg(weather_delay) " +
        "FROM delays " +
        "WHERE weather_delay IS NOT NULL " +
        "GROUP BY origin_city_name;"

    $hqlScript = $hqlDropDelaysRaw + $hqlCreateDelaysRaw + $hqlDropDelays + $hqlCreateDelays + $hqlInsertLocal

    $hqlScript | Out-File $hqlLocalFileName -Encoding ascii -Force
    #endregion

    #region - Upload the Hive script to the default Blob container
    Write-Host "`nUploading the Hive script to the default Blob container ..." -ForegroundColor Green

    # Create a storage context object
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Upload the file from local workstation to Blob storage
    Set-AzureStorageBlobContent -File $hqlLocalFileName -Container $blobContainerName -Blob $hqlBlobName -Context $destContext
    #endregion

    Write-host "`nEnd of the PowerShell script" -ForegroundColor Green
    ```

    <span data-ttu-id="2d714-257">스크립트에서 사용되는 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-257">Here are the variables used in the script:</span></span>

   * <span data-ttu-id="2d714-258">**$hqlLocalFileName** - 스크립트는 HiveQL 스크립트 파일을 Blob 저장소에 업로드하기 전에 로컬에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-258">**$hqlLocalFileName** - The script saves the HiveQL script file locally before uploading it to Blob storage.</span></span> <span data-ttu-id="2d714-259">이 상수가 해당 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-259">This is the file name.</span></span> <span data-ttu-id="2d714-260">기본값은 <u>C:\tutorials\flightdelay\flightdelays.hql</u>입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-260">The default value is <u>C:\tutorials\flightdelay\flightdelays.hql</u>.</span></span>
   * <span data-ttu-id="2d714-261">**$hqlBlobName** - Azure Blob 저장소에서 사용되는 HiveQL 스크립트 파일 Blob 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-261">**$hqlBlobName** - This is the HiveQL script file blob name used in the Azure Blob storage.</span></span> <span data-ttu-id="2d714-262">기본값은 tutorials/flightdelay/flightdelays.hql입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-262">The default value is tutorials/flightdelay/flightdelays.hql.</span></span> <span data-ttu-id="2d714-263">파일은 Azure Blob 저장소에 직접 기록되므로 Blob 이름 앞에는 "/"가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-263">Because the file will be written directly to Azure Blob storage, there is NOT a "/" at the beginning of the blob name.</span></span> <span data-ttu-id="2d714-264">Blob 저장소의 파일에 액세스하려면 파일 이름 앞에 "/"를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-264">If you want to access the file from Blob storage, you will need to add a "/" at the beginning of the file name.</span></span>
   * <span data-ttu-id="2d714-265">**$srcDataFolder** 및 **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"</span><span class="sxs-lookup"><span data-stu-id="2d714-265">**$srcDataFolder** and **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"</span></span>

- - -
## <span data-ttu-id="2d714-266"><a id="appendix-c"></a>부록 C - Azure SQL 데이터베이스에서 Sqoop 작업 출력 준비</span><span class="sxs-lookup"><span data-stu-id="2d714-266"><a id="appendix-c"></a>Appendix C - Prepare an Azure SQL database for the Sqoop job output</span></span>
<span data-ttu-id="2d714-267">**SQL 데이터베이스를 준비하려면(이 작업을 Sqoop 스크립트와 통합)**</span><span class="sxs-lookup"><span data-stu-id="2d714-267">**To prepare the SQL database (merge this with the Sqoop script)**</span></span>

1. <span data-ttu-id="2d714-268">매개 변수를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-268">Prepare the parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="2d714-269">변수 이름</span><span class="sxs-lookup"><span data-stu-id="2d714-269">Variable Name</span></span></th><th><span data-ttu-id="2d714-270">참고 사항</span><span class="sxs-lookup"><span data-stu-id="2d714-270">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="2d714-271">$sqlDatabaseServerName</span><span class="sxs-lookup"><span data-stu-id="2d714-271">$sqlDatabaseServerName</span></span></td><td><span data-ttu-id="2d714-272">Azure SQL 데이터베이스 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-272">The name of the Azure SQL database server.</span></span> <span data-ttu-id="2d714-273">새 서버를 만들려면 아무 내용도 입력하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-273">Enter nothing to create a new server.</span></span></td></tr>
    <tr><td><span data-ttu-id="2d714-274">$sqlDatabaseUsername</span><span class="sxs-lookup"><span data-stu-id="2d714-274">$sqlDatabaseUsername</span></span></td><td><span data-ttu-id="2d714-275">Azure SQL 데이터베이스 서버의 로그인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-275">The login name for the Azure SQL database server.</span></span> <span data-ttu-id="2d714-276">$sqlDatabaseServerName이 기본 서버이면 로그인 및 로그인 암호가 서버에서 인증하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-276">If $sqlDatabaseServerName is an existing server, the login and login password are used to authenticate with the server.</span></span> <span data-ttu-id="2d714-277">새 서버를 만드는 데도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-277">Otherwise they are used to create a new server.</span></span></td></tr>
    <tr><td><span data-ttu-id="2d714-278">$sqlDatabasePassword</span><span class="sxs-lookup"><span data-stu-id="2d714-278">$sqlDatabasePassword</span></span></td><td><span data-ttu-id="2d714-279">Azure SQL 데이터베이스 서버의 로그인 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-279">The login password for the Azure SQL database server.</span></span></td></tr>
    <tr><td><span data-ttu-id="2d714-280">$sqlDatabaseLocation</span><span class="sxs-lookup"><span data-stu-id="2d714-280">$sqlDatabaseLocation</span></span></td><td><span data-ttu-id="2d714-281">이 값은 새 Azure 데이터베이스 서버를 만드는 경우에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-281">This value is used only when you're creating a new Azure database server.</span></span></td></tr>
    <tr><td><span data-ttu-id="2d714-282">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="2d714-282">$sqlDatabaseName</span></span></td><td><span data-ttu-id="2d714-283">Sqoop 작업의 AvgDelays 테이블을 만드는 데 사용되는 SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-283">The SQL database used to create the AvgDelays table for the Sqoop job.</span></span> <span data-ttu-id="2d714-284">이 매개 변수를 비워 두면 HDISqoop라는 데이터베이스가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-284">Leaving it blank will create a database called HDISqoop.</span></span> <span data-ttu-id="2d714-285">Sqoop 작업 출력의 테이블 이름은 AvgDelays입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-285">The table name for the Sqoop job output is AvgDelays.</span></span> </td></tr>
    </table>
2. <span data-ttu-id="2d714-286">Azure PowerShell ISE를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-286">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="2d714-287">3.</span><span class="sxs-lookup"><span data-stu-id="2d714-287">3.</span></span> <span data-ttu-id="2d714-288">다음 스크립트를 복사하여 스크립트 창에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-288">Copy and paste the following script into the script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Resource group variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter the Azure resource group name. It will be created if it doesn't exist.")]
        [String]$resourceGroupName,

        # SQL database server variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter the Azure SQL Database Server Name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseServer,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter the Azure SQL Database admin user.")]
        [String]$sqlDatabaseLogin,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter the Azure SQL Database admin user password.")]
        [String]$sqlDatabasePassword,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter the region to create the Database in.")]
        [String]$sqlDatabaseLocation,   #For example, West US.

        # SQL database variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter the database name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseName # specify the database name if you have one created. Otherwise use "" to have the script create one for you.
    )

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Constants and variables

    # IP address REST service used for retrieving external IP address and creating firewall rules
    [String]$ipAddressRestService = "http://bot.whatismyipaddress.com"
    [String]$fireWallRuleName = "FlightDelay"

    # SQL database variables
    [String]$sqlDatabaseMaxSizeGB = 10

    #SQL query string for creating AvgDelays table
    [String]$sqlDatabaseTableName = "AvgDelays"
    [String]$sqlCreateAvgDelaysTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [origin_city_name] [nvarchar](50) NOT NULL,
                [weather_delay] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
                [origin_city_name] ASC
            )
            )"
    #endregion

    #Region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #region - Create and validate Azure resouce group
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $sqlDatabaseLocation
    }

    #EndRegion

    #region - Create and validate Azure SQL database server
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServer -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServer = (New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -SqlAdministratorCredentials $credential -Location $sqlDatabaseLocation).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServer." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-workstation" -StartIpAddress $workstationIPAddress -EndIpAddress $workstationIPAddress

        #To allow other Azure services to access the server add a firewall rule and set both the StartIpAddress and EndIpAddress to 0.0.0.0. Note that this allows Azure traffic from any Azure subscription to access the server.
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-Azureservices" -StartIpAddress "0.0.0.0" -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database

    try {
        Get-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName -Edition "Standard" -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region -  Execute an SQL command to create the AvgDelays table

    Write-Host "`nCreating SQL Database table ..."  -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = $sqlCreateAvgDelaysTable
    $cmd.executenonquery()

    $conn.close()

    Write-host "`nEnd of the PowerShell script" -ForegroundColor Green
    ```

   > [!NOTE]
   > <span data-ttu-id="2d714-289">스크립트는 REST(representational state transfer) 서비스 http://bot.whatismyipaddress.com을 사용하여 외부 IP 주소를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-289">The script uses a representational state transfer (REST) service, http://bot.whatismyipaddress.com, to retrieve your external IP address.</span></span> <span data-ttu-id="2d714-290">IP 주소는 SQL 데이터베이스 서버용 방화벽 규칙을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-290">The IP address is used for creating a firewall rule for your SQL database server.</span></span>

    <span data-ttu-id="2d714-291">스크립트에서 사용되는 일부 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-291">Here are some variables used in the script:</span></span>

   * <span data-ttu-id="2d714-292">**$ipAddressRestService** - 기본값은 http://bot.whatismyipaddress.com 입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-292">**$ipAddressRestService** - The default value is http://bot.whatismyipaddress.com.</span></span> <span data-ttu-id="2d714-293">외부 IP 주소를 가져오기 위한 공용 IP 주소 REST 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-293">It is a public IP address REST service for getting your external IP address.</span></span> <span data-ttu-id="2d714-294">원하는 경우 다른 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-294">You can use other services if you want.</span></span> <span data-ttu-id="2d714-295">서비스를 통해 검색된 외부 IP 주소를 사용하여 Azure SQL 데이터베이스 서버용 방화벽 규칙을 만듭니다. 따라서 Windows PowerShell 스크립트를 사용하여 워크스테이션에서 데이터베이스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-295">The external IP address retrieved through the service will be used to create a firewall rule for your Azure SQL database server, so that you can access the database from your workstation (by using a Windows PowerShell script).</span></span>
   * <span data-ttu-id="2d714-296">**$fireWallRuleName** - Azure SQL 데이터베이스 서버에 대한 방화벽 규칙의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-296">**$fireWallRuleName** - This is the name of the firewall rule for the Azure SQL database server.</span></span> <span data-ttu-id="2d714-297">기본 이름은 <u>FlightDelay</u>입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-297">The default name is <u>FlightDelay</u>.</span></span> <span data-ttu-id="2d714-298">원하는 경우 이름을 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-298">You can rename it if you want.</span></span>
   * <span data-ttu-id="2d714-299">**$sqlDatabaseMaxSizeGB** - 이 값은 새 Azure SQL 데이터베이스 서버를 만드는 경우에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-299">**$sqlDatabaseMaxSizeGB** - This value is used only when you're creating a new Azure SQL database server.</span></span> <span data-ttu-id="2d714-300">기본 크기는 10GB입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-300">The default value is 10GB.</span></span> <span data-ttu-id="2d714-301">이 자습서에서는 크기가 10GB이면 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-301">10GB is sufficient for this tutorial.</span></span>
   * <span data-ttu-id="2d714-302">**$sqlDatabaseName** - 이 값은 새 Azure SQL 데이터베이스를 만드는 경우에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-302">**$sqlDatabaseName** - This value is used only when you're creating a new Azure SQL database.</span></span> <span data-ttu-id="2d714-303">기본값은 HDISqoop입니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-303">The default value is HDISqoop.</span></span> <span data-ttu-id="2d714-304">이 상수의 이름을 바꾸는 경우에는 Sqoop Windows PowerShell 스크립트도 그에 따라 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-304">If you rename it, you must update the Sqoop Windows PowerShell script accordingly.</span></span>
4. <span data-ttu-id="2d714-305">**F5** 키를 눌러 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-305">Press **F5** to run the script.</span></span>
5. <span data-ttu-id="2d714-306">스크립트 출력의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-306">Validate the script output.</span></span> <span data-ttu-id="2d714-307">스크립트가 정상적으로 실행되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-307">Make sure the script ran successfully.</span></span>

## <span data-ttu-id="2d714-308"><a id="nextsteps"></a> 다음 단계</span><span class="sxs-lookup"><span data-stu-id="2d714-308"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="2d714-309">이제 파일을 Azure Blob 저장소로 업로드하는 방법, Azure Blob 저장소의 데이터를 사용하여 Hive 테이블을 채우는 방법, Hive 쿼리를 실행하는 방법, Sqoop을 사용하여 HDFS의 데이터를 Azure SQL 데이터베이스로 내보내는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="2d714-309">Now you understand how to upload a file to Azure Blob storage, how to populate a Hive table by using the data from Azure Blob storage, how to run Hive queries, and how to use Sqoop to export data from HDFS to an Azure SQL database.</span></span> <span data-ttu-id="2d714-310">자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d714-310">To learn more, see the following articles:</span></span>

* <span data-ttu-id="2d714-311">[HDInsight 시작][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="2d714-311">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="2d714-312">[HDInsight에서 Hive 사용][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="2d714-312">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="2d714-313">[HDInsight에서 Oozie 사용][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="2d714-313">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="2d714-314">[HDInsight에서 Sqoop 사용][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="2d714-314">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="2d714-315">[HDInsight에서 Pig 사용][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="2d714-315">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="2d714-316">[HDInsight용 Java MapReduce 프로그램 개발][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="2d714-316">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[rita-website]: http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time
[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[hadoop-hiveql]: https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL
[hadoop-shell-commands]: http://hadoop.apache.org/docs/r0.18.3/hdfs_shell.html

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx

[image-hdi-flightdelays-avgdelays-dataset]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.AvgDelays.DataSet.png
[img-hdi-flightdelays-run-hive-job-output]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.RunHiveJob.Output.png
[img-hdi-flightdelays-flow]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.Flow.png
