---
title: "Azure HDInsight에서 Hadoop으로 aaaAnalyze 비행 연착 데이터 | Microsoft Docs"
description: "Toouse 하나의 Windows PowerShell 스크립트 toocreate를 HDInsight 클러스터에 Hive 작업을 실행할 Sqoop 작업을 실행 하는 방법을 알아보고 hello 클러스터를 삭제 합니다."
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
ms.openlocfilehash: 6ebaee65d9b270e5dc2141dd1265011d372f497d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-in-hdinsight"></a><span data-ttu-id="c9a3d-103">HDInsight의 Hive를 사용하여 비행 지연 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="c9a3d-103">Analyze flight delay data by using Hive in HDInsight</span></span>
<span data-ttu-id="c9a3d-104">Hive에서는 대규모 데이터의 요약, 쿼리, 분석에 적용할 수 있는 SQL 스타일 스크립트 언어인 *[HiveQL][hadoop-hiveql]*을 통해 Hadoop MapReduce 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-104">Hive provides a means of running Hadoop MapReduce jobs through an SQL-like scripting language called *[HiveQL][hadoop-hiveql]*, which can be applied towards summarizing, querying, and analyzing large volumes of data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c9a3d-105">hello이 문서의 단계는 Windows 기반 HDInsight 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-105">hello steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="c9a3d-106">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c9a3d-107">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="c9a3d-108">Linux 기반 클러스터를 사용하는 단계는 [HDInsight에서 Hive를 사용하여 비행 지연 데이터 분석(Linux)](hdinsight-analyze-flight-delay-data-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-108">For steps that work with a Linux-based cluster, see [Analyze flight delay data by using Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).</span></span>

<span data-ttu-id="c9a3d-109">Hello Azure HDInsight의 주요 이점 중 하나에 데이터 저장소 및 계산의 hello 분리입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-109">One of hello major benefits of Azure HDInsight is hello separation of data storage and compute.</span></span> <span data-ttu-id="c9a3d-110">HDInsight는 데이터 저장소로 Azure Blob 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-110">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="c9a3d-111">일반적인 작업은 세 부분으로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-111">A typical job involves three parts:</span></span>

1. <span data-ttu-id="c9a3d-112">**Azure Blob 저장소에 데이터 저장.**</span><span class="sxs-lookup"><span data-stu-id="c9a3d-112">**Store data in Azure Blob storage.**</span></span>  <span data-ttu-id="c9a3d-113">예를 들어 날씨 데이터, 센서 데이터, 웹 로그 및 이 자습서의 경우 비행 지연 데이터를 Azure Blob 저장소에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-113">For example, weather data, sensor data, web logs, and in this case, flight delay data are saved into Azure Blob storage.</span></span>
2. <span data-ttu-id="c9a3d-114">**작업 실행**</span><span class="sxs-lookup"><span data-stu-id="c9a3d-114">**Run jobs.**</span></span> <span data-ttu-id="c9a3d-115">Windows PowerShell 스크립트 (또는 클라이언트 응용 프로그램)를 실행 하는 시간 tooprocess hello 데이터 이면 toocreate는 HDInsight 클러스터 작업을 실행 하 고 hello 클러스터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-115">When it is time tooprocess hello data, you run a Windows PowerShell script (or a client application) toocreate an HDInsight cluster, run jobs, and delete hello cluster.</span></span> <span data-ttu-id="c9a3d-116">hello 작업 출력 데이터 tooAzure Blob 저장소에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-116">hello jobs save output data tooAzure Blob storage.</span></span> <span data-ttu-id="c9a3d-117">hello 출력 데이터는 hello 클러스터를 삭제 한 후에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-117">hello output data is retained even after hello cluster is deleted.</span></span> <span data-ttu-id="c9a3d-118">따라서 사용한 데이터에 대해서만 비용을 지불하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-118">This way, you pay for only what you have consumed.</span></span>
3. <span data-ttu-id="c9a3d-119">**Azure Blob 저장소에서 hello 출력을 검색**, 또는이 자습서에서는 hello 데이터 tooan Azure SQL 데이터베이스 내보내기.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-119">**Retrieve hello output from Azure Blob storage**, or in this tutorial, export hello data tooan Azure SQL database.</span></span>

<span data-ttu-id="c9a3d-120">hello 다음 다이어그램에서는 hello 시나리오와이 자습서의 hello 구조 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-120">hello following diagram illustrates hello scenario and hello structure of this tutorial:</span></span>

![HDI.FlightDelays.flow][img-hdi-flightdelays-flow]

<span data-ttu-id="c9a3d-122">Hello 다이어그램에서 hello 숫자 toohello 섹션 제목을 모니터는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-122">Note that hello numbers in hello diagram correspond toohello section titles.</span></span> <span data-ttu-id="c9a3d-123">**M** 는 hello 주 프로세스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-123">**M** stands for hello main process.</span></span> <span data-ttu-id="c9a3d-124">**A** 는 hello 부록에서 hello 콘텐츠를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-124">**A** stands for hello content in hello appendix.</span></span>

<span data-ttu-id="c9a3d-125">hello 자습서의 주요 부분이 hello toouse 하나의 Windows PowerShell 스크립트 tooperform hello 다음 작업 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-125">hello main portion of hello tutorial shows you how toouse one Windows PowerShell script tooperform hello following tasks:</span></span>

* <span data-ttu-id="c9a3d-126">HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="c9a3d-126">Create an HDInsight cluster.</span></span>
* <span data-ttu-id="c9a3d-127">공항에 hello 클러스터 toocalculate 평균 지연에서 하이브 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-127">Run a Hive job on hello cluster toocalculate average delays at airports.</span></span> <span data-ttu-id="c9a3d-128">hello 비행 연착 데이터는 Azure Blob 저장소 계정에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-128">hello flight delay data is stored in an Azure Blob storage account.</span></span>
* <span data-ttu-id="c9a3d-129">Sqoop 작업 tooexport hello 하이브 작업 출력 tooan Azure SQL 데이터베이스를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-129">Run a Sqoop job tooexport hello Hive job output tooan Azure SQL database.</span></span>
* <span data-ttu-id="c9a3d-130">Hello HDInsight 클러스터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-130">Delete hello HDInsight cluster.</span></span>

<span data-ttu-id="c9a3d-131">Hello 부록 비행 연착 데이터를 업로드, Hive 쿼리 문자열 만들기/업로드 하 고 hello Sqoop 작업에 대 한 hello Azure SQL 데이터베이스를 준비 하기 위한 hello 지침을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-131">In hello appendixes, you can find hello instructions for uploading flight delay data, creating/uploading a Hive query string, and preparing hello Azure SQL database for hello Sqoop job.</span></span>

> [!NOTE]
> <span data-ttu-id="c9a3d-132">이 문서의 hello 단계는 특정 tooWindows 기반 HDInsight 클러스터 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-132">hello steps in this document are specific tooWindows-based HDInsight clusters.</span></span> <span data-ttu-id="c9a3d-133">Linux 기반 클러스터를 사용하는 단계는 [HDInsight에서 Hive를 사용하여 비행 지연 데이터 분석(Linux)](hdinsight-analyze-flight-delay-data-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-133">For steps that work with a Linux-based cluster, see [Analyze flight delay data using Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md)</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c9a3d-134">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c9a3d-134">Prerequisites</span></span>
<span data-ttu-id="c9a3d-135">이 자습서를 시작 하기 전에 다음 항목 hello가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-135">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="c9a3d-136">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-136">**An Azure subscription**.</span></span> <span data-ttu-id="c9a3d-137">[Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-137">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="c9a3d-138">**Azure PowerShell이 포함된 워크스테이션**.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-138">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c9a3d-139">Azure Service Manager를 사용하여 HDInsight 리소스를 관리하는 Azure PowerShell 지원은 더 이상 **지원되지 않고** 2017년 1월 1일에 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-139">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="c9a3d-140">Azure 리소스 관리자와 함께 작동 하는이 문서 사용 hello 새 HDInsight cmdlet의 hello 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-140">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="c9a3d-141">Hello 단계에 따라 [설치 Azure PowerShell을 구성 하 고](/powershell/azureps-cmdlets-docs) tooinstall hello 최신 버전의 Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-141">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="c9a3d-142">해당 필요 toobe Azure 리소스 관리자와 함께 작동 하는 toouse hello 새로운 cmdlet 수정 스크립트가 있는 경우, 참조 [HDInsight 클러스터에 대 한 마이그레이션 tooAzure 리소스 관리자 기반 개발 도구](hdinsight-hadoop-development-using-azure-resource-manager.md) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-142">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

<span data-ttu-id="c9a3d-143">**이 자습서에서 사용하는 파일**</span><span class="sxs-lookup"><span data-stu-id="c9a3d-143">**Files used in this tutorial**</span></span>

<span data-ttu-id="c9a3d-144">이 자습서에서 airline 비행 데이터의 지정 된 시간에 성능 hello를 사용 하 여 [연구 혁신적인 기술을 관리, 운송 Bureau 통계 또는 RITA][rita-website]합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-144">This tutorial uses hello on-time performance of airline flight data from [Research and Innovative Technology Administration, Bureau of Transportation Statistics or RITA][rita-website].</span></span>
<span data-ttu-id="c9a3d-145">된 데이터는 hello 사본을 hello 공용 Blob 액세스 권한이 tooan Azure Blob 저장소 컨테이너를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-145">A copy of hello data has been uploaded tooan Azure Blob storage container with hello Public Blob access permission.</span></span>
<span data-ttu-id="c9a3d-146">PowerShell 스크립트의 일부 hello 공용 blob 컨테이너 toohello 기본 blob 컨테이너에서 클러스터의 hello 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-146">A part of your PowerShell script copies hello data from hello public blob container toohello default blob container of your cluster.</span></span> <span data-ttu-id="c9a3d-147">이 스크립트는 또한 HiveQL hello 복사 toohello 동일한 Blob 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-147">hello HiveQL script is also copied toohello same Blob container.</span></span>
<span data-ttu-id="c9a3d-148">Toolearn 하려는 경우 어떻게 tooget/업로드 hello 데이터 tooyour 소유 저장소 계정당 하나만 그리고 toocreate/업로드 hello HiveQL 스크립트 파일을 어떻게 참조 [부록 A](#appendix-a) 및 [부록 B](#appendix-b)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-148">If you want toolearn how tooget/upload hello data tooyour own Storage account, and how toocreate/upload hello HiveQL script file, see [Appendix A](#appendix-a) and [Appendix B](#appendix-b).</span></span>

<span data-ttu-id="c9a3d-149">hello 다음 표에이 자습서에 사용 된 hello 파일.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-149">hello following table lists hello files used in this tutorial:</span></span>

<table border="1">
<tr><th><span data-ttu-id="c9a3d-150">파일</span><span class="sxs-lookup"><span data-stu-id="c9a3d-150">Files</span></span></th><th><span data-ttu-id="c9a3d-151">설명</span><span class="sxs-lookup"><span data-stu-id="c9a3d-151">Description</span></span></th></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/flightdelays.hql</td><td><span data-ttu-id="c9a3d-152">하이브 작업 hello hello HiveQL 스크립트 파일 사용.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-152">hello HiveQL script file used by hello Hive job.</span></span> <span data-ttu-id="c9a3d-153">이 스크립트는 업로드 된 tooan hello 공용 액세스를 사용 하는 Azure Blob 저장소 계정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-153">This script has been uploaded tooan Azure Blob storage account with hello public access.</span></span> <span data-ttu-id="c9a3d-154"><a href="#appendix-b">부록 B</a> 를 준비 하 고 업로드 하는이 파일 tooyour 직접 Azure Blob 저장소 계정에 대 한 지침을 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-154"><a href="#appendix-b">Appendix B</a> has instructions on preparing and uploading this file tooyour own Azure Blob storage account.</span></span></td></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data</td><td><span data-ttu-id="c9a3d-155">Hello 하이브 작업에 대 한 입력된 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-155">Input data for hello Hive job.</span></span> <span data-ttu-id="c9a3d-156">hello 데이터가 업로드 tooan hello 공용 액세스를 사용 하는 Azure Blob 저장소 계정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-156">hello data has been uploaded tooan Azure Blob storage account with hello public access.</span></span> <span data-ttu-id="c9a3d-157"><a href="#appendix-a">부록 A</a> 지침에 hello 데이터 가져오기 및 hello 데이터 tooyour 직접 Azure Blob 저장소 계정에 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-157"><a href="#appendix-a">Appendix A</a> has instructions on getting hello data and uploading hello data tooyour own Azure Blob storage account.</span></span></td></tr>
<tr><td><span data-ttu-id="c9a3d-158">\tutorials\flightdelays\output</span><span class="sxs-lookup"><span data-stu-id="c9a3d-158">\tutorials\flightdelays\output</span></span></td><td><span data-ttu-id="c9a3d-159">hello hello 하이브 작업에 대 한 출력 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-159">hello output path for hello Hive job.</span></span> <span data-ttu-id="c9a3d-160">hello 기본 컨테이너 hello 출력 데이터를 저장 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-160">hello default container is used for storing hello output data.</span></span></td></tr>
<tr><td><span data-ttu-id="c9a3d-161">\tutorials\flightdelays\jobstatus</span><span class="sxs-lookup"><span data-stu-id="c9a3d-161">\tutorials\flightdelays\jobstatus</span></span></td><td><span data-ttu-id="c9a3d-162">hello 하이브 작업 상태에 폴더 hello 기본 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-162">hello Hive job status folder on hello default container.</span></span></td></tr>
</table>

## <a name="create-cluster-and-run-hivesqoop-jobs"></a><span data-ttu-id="c9a3d-163">클러스터 만들기 및 Hive/Sqoop 작업 실행</span><span class="sxs-lookup"><span data-stu-id="c9a3d-163">Create cluster and run Hive/Sqoop jobs</span></span>
<span data-ttu-id="c9a3d-164">Hadoop MapReduce에서는 작업을 일괄 처리 방식으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-164">Hadoop MapReduce is batch processing.</span></span> <span data-ttu-id="c9a3d-165">hello 대부분 비용 효율적인 방식으로 toorun 하이브 작업 toocreate hello 작업에 대 한 클러스터 이며 hello 작업이 완료 되 면 hello 작업을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-165">hello most cost-effective way toorun a Hive job is toocreate a cluster for hello job, and delete hello job after hello job is completed.</span></span> <span data-ttu-id="c9a3d-166">다음 스크립트에서는 hello에 대 한 전체 프로세스를 수행 하는 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-166">hello following script covers hello whole process.</span></span>
<span data-ttu-id="c9a3d-167">HDInsight 클러스터를 만들고 Hive 작업을 실행하는 방법에 대한 자세한 내용은 [HDInsight에서 Hadoop 클러스터 만들기][hdinsight-provision] 및 [HDInsight에서 Hive 사용][hdinsight-use-hive]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-167">For more information on creating an HDInsight cluster and running Hive jobs, see [Create Hadoop clusters in HDInsight][hdinsight-provision] and [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

<span data-ttu-id="c9a3d-168">**Azure PowerShell에서 toorun hello 하이브 쿼리**</span><span class="sxs-lookup"><span data-stu-id="c9a3d-168">**toorun hello Hive queries by Azure PowerShell**</span></span>

1. <span data-ttu-id="c9a3d-169">지침에 hello를 사용 하 여 hello Sqoop 작업 출력에 대 한 Azure SQL 데이터베이스와 hello 테이블을 만들 [부록 C](#appendix-c)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-169">Create an Azure SQL database and hello table for hello Sqoop job output by using hello instructions in [Appendix C](#appendix-c).</span></span>
2. <span data-ttu-id="c9a3d-170">Windows PowerShell ISE를 열고 다음 스크립트는 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-170">Open Windows PowerShell ISE, and run hello following script:</span></span>

    ```powershell
    $subscriptionID = "<Azure Subscription ID>"
    $nameToken = "<Enter an Alias>"

    ###########################################
    # You must configure hello follwing variables
    # for an existing Azure SQL Database
    ###########################################
    $existingSqlDatabaseServerName = "<Azure SQL Database Server>"
    $existingSqlDatabaseLogin = "<Azure SQL Database Server Login>"
    $existingSqlDatabasePassword = "<Azure SQL Database Server login password>"
    $existingSqlDatabaseName = "<Azure SQL Database name>"

    $localFolder = "E:\Tutorials\Downloads\" # A temp location for copying files.
    $azcopyPath = "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy" # depends on hello version, hello folder can be different

    ###########################################
    # (Optional) configure hello following variables
    ###########################################

    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2"

    $HDInsightClusterName = $namePrefix + "hdi"
    $httpUserName = "admin"
    $httpPassword = "<Enter hello Password>"

    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $HDInsightClusterName # use hello cluster name

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

    # Create hello default storage account
    New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName -Location $location -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer -Name $defaultBlobContainerName -Context $defaultStorageAccountContext

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
        -DefaultStorageContainer $existingDefaultBlobContainerName

    ###########################################
    # Prepare hello HiveQL script and source data
    ###########################################

    # Create hello temp location
    New-Item -Path $localFolder -ItemType Directory -Force

    # Download hello sample file from Azure Blob storage
    $context = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous
    $blobs = Get-AzureStorageBlob -Container "flightdelay" -Context $context
    #$blobs | Get-AzureStorageBlobContent -Context $context -Destination $localFolder

    # Upload data toodefault container

    $azcopycmd = "cmd.exe /C '$azcopyPath\azcopy.exe' /S /Source:'$localFolder' /Dest:'https://$defaultStorageAccountName.blob.core.windows.net/$defaultBlobContainerName/tutorials/flightdelays' /DestKey:$defaultStorageAccountKey"

    Invoke-Expression -Command:$azcopycmd

    ###########################################
    # Submit hello Hive job
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
    # Submit hello Sqoop job
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
    # Delete hello cluster
    ###########################################
    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName
    ```
3. <span data-ttu-id="c9a3d-171">Tooyour SQL 데이터베이스를 연결 하 고 hello AvgDelays 표에 도시별 평균 비행 연착 정보를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-171">Connect tooyour SQL database and see average flight delays by city in hello AvgDelays table:</span></span>

    ![HDI.FlightDelays.AvgDelays.Dataset][image-hdi-flightdelays-avgdelays-dataset]

- - -

## <span data-ttu-id="c9a3d-173"><a id="appendix-a"></a>부록 A-업로드 비행 지연 데이터 tooAzure Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="c9a3d-173"><a id="appendix-a"></a>Appendix A - Upload flight delay data tooAzure Blob storage</span></span>
<span data-ttu-id="c9a3d-174">Hello 데이터 파일 및 hello HiveQL 스크립트 파일을 업로드 (참조 [부록 B](#appendix-b)) 일부 계획이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-174">Uploading hello data file and hello HiveQL script files (see [Appendix B](#appendix-b)) requires some planning.</span></span> <span data-ttu-id="c9a3d-175">hello 개념 toostore hello 데이터 파일 및 HDInsight 클러스터를 만들고 hello 하이브 작업을 실행 하기 전에 hello HiveQL 파일은입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-175">hello idea is toostore hello data files and hello HiveQL file before creating an HDInsight cluster and running hello Hive job.</span></span> <span data-ttu-id="c9a3d-176">다음 두 가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-176">You have two options:</span></span>

* <span data-ttu-id="c9a3d-177">**사용 하 여 hello 동일 hello 기본 파일 시스템으로 hello HDInsight 클러스터에서 사용할 Azure 저장소 계정입니다.**</span><span class="sxs-lookup"><span data-stu-id="c9a3d-177">**Use hello same Azure Storage account that will be used by hello HDInsight cluster as hello default file system.**</span></span> <span data-ttu-id="c9a3d-178">Hello HDInsight 클러스터 hello 저장소 계정 액세스 키를 더 추가 변경 toomake 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-178">Because hello HDInsight cluster will have hello Storage account access key, you don't need toomake any additional changes.</span></span>
* <span data-ttu-id="c9a3d-179">**Hello HDInsight 클러스터 기본 파일 시스템에서에서 다른 Azure 저장소 계정을 사용 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c9a3d-179">**Use a different Azure Storage account from hello HDInsight cluster default file system.**</span></span> <span data-ttu-id="c9a3d-180">Hello 상황에 hello 생성 부분이 hello Windows PowerShell에서 발견 된 스크립트를 수정 해야 [만들 HDInsight 클러스터와 실행된 Hive/Sqoop 작업](#runjob) toolink hello 추가 저장소 계정으로 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-180">If this is hello case, you must modify hello creation part of hello Windows PowerShell script found in [Create HDInsight cluster and run Hive/Sqoop jobs](#runjob) toolink hello Storage account as an additional Storage account.</span></span> <span data-ttu-id="c9a3d-181">자세한 내용은 [HDInsight에서 Hadoop 클러스터 만들기][hdinsight-provision]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-181">For instructions, see [Create Hadoop clusters in HDInsight][hdinsight-provision].</span></span> <span data-ttu-id="c9a3d-182">hello HDInsight 클러스터는 다음 hello 저장소 계정에 대 한 hello 액세스 키를 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-182">hello HDInsight cluster then knows hello access key for hello Storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="c9a3d-183">hello HiveQL 스크립트 파일에서 코딩 된 데이터 파일은 하드 hello에 대 한 hello Blob 저장소 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-183">hello Blob storage path for hello data file is hard coded in hello HiveQL script file.</span></span> <span data-ttu-id="c9a3d-184">수정 내용에 따라 이를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-184">You must update it accordingly.</span></span>

<span data-ttu-id="c9a3d-185">**toodownload hello 비행 데이터**</span><span class="sxs-lookup"><span data-stu-id="c9a3d-185">**toodownload hello flight data**</span></span>

1. <span data-ttu-id="c9a3d-186">너무 찾아보기[연구 및 운송 통계 Bureau 혁신적인 기술을 관리][rita-website]합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-186">Browse too[Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>
2. <span data-ttu-id="c9a3d-187">Hello 페이지에서 다음 값에는 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-187">On hello page, select hello following values:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="c9a3d-188">이름</span><span class="sxs-lookup"><span data-stu-id="c9a3d-188">Name</span></span></th><th><span data-ttu-id="c9a3d-189">값</span><span class="sxs-lookup"><span data-stu-id="c9a3d-189">Value</span></span></th></tr>
    <tr><td><span data-ttu-id="c9a3d-190">Filter Year</span><span class="sxs-lookup"><span data-stu-id="c9a3d-190">Filter Year</span></span></td><td><span data-ttu-id="c9a3d-191">2013</span><span class="sxs-lookup"><span data-stu-id="c9a3d-191">2013</span></span> </td></tr>
    <tr><td><span data-ttu-id="c9a3d-192">Filter Period</span><span class="sxs-lookup"><span data-stu-id="c9a3d-192">Filter Period</span></span></td><td><span data-ttu-id="c9a3d-193">January</span><span class="sxs-lookup"><span data-stu-id="c9a3d-193">January</span></span></td></tr>
    <tr><td><span data-ttu-id="c9a3d-194">필드</span><span class="sxs-lookup"><span data-stu-id="c9a3d-194">Fields</span></span></td><td><span data-ttu-id="c9a3d-195">*Year*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *Origin*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*, *LateAircraftDelay*(다른 모든 필드는 선택하지 않음)</span><span class="sxs-lookup"><span data-stu-id="c9a3d-195">*Year*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *Origin*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (clear all other fields)</span></span></td></tr>
    </table><span data-ttu-id="c9a3d-196">
3. **다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-196">
3. Click **Download**.</span></span>
<span data-ttu-id="c9a3d-197">4.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-197">4.</span></span> <span data-ttu-id="c9a3d-198">Hello 파일 toohello의 압축을 푸는 **C:\Tutorials\FlightDelay\2013Data** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-198">Unzip hello file toohello **C:\Tutorials\FlightDelay\2013Data** folder.</span></span> <span data-ttu-id="c9a3d-199">각 파일은 CSV 파일이며 크기가 60GB 정도입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-199">Each file is a CSV file and is approximately 60GB in size.</span></span>
<span data-ttu-id="c9a3d-200">5.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-200">5.</span></span> <span data-ttu-id="c9a3d-201">Hello 파일 toohello 이름에 대 한 데이터를 포함 하는 hello 달의 이름을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-201">Rename hello file toohello name of hello month that it contains data for.</span></span> <span data-ttu-id="c9a3d-202">Hello 년 1 월 데이터를 포함 하는 hello 파일의 이름이 예를 들어 *January.csv*합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-202">For example, hello file containing hello January data would be named *January.csv*.</span></span>
<span data-ttu-id="c9a3d-203">6.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-203">6.</span></span> <span data-ttu-id="c9a3d-204">2013에서 12 개월 각각 hello에 대 한 단계 2와 5 단계 toodownload 파일을 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-204">Repeat steps 2 and 5 toodownload a file for each of hello 12 months in 2013.</span></span> <span data-ttu-id="c9a3d-205">하나의 파일 toorun hello 자습서의 최소가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-205">You will need a minimum of one file toorun hello tutorial.</span></span>

<span data-ttu-id="c9a3d-206">**tooupload hello 비행 지연 데이터 tooAzure Blob 저장소**</span><span class="sxs-lookup"><span data-stu-id="c9a3d-206">**tooupload hello flight delay data tooAzure Blob storage**</span></span>

1. <span data-ttu-id="c9a3d-207">Hello 매개 변수를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-207">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="c9a3d-208">변수 이름</span><span class="sxs-lookup"><span data-stu-id="c9a3d-208">Variable Name</span></span></th><th><span data-ttu-id="c9a3d-209">참고 사항</span><span class="sxs-lookup"><span data-stu-id="c9a3d-209">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="c9a3d-210">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="c9a3d-210">$storageAccountName</span></span></td><td><span data-ttu-id="c9a3d-211">hello tooupload hello 데이터를 저장할 Azure 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-211">hello Azure Storage account where you want tooupload hello data to.</span></span></td></tr>
    <tr><td><span data-ttu-id="c9a3d-212">$blobContainerName</span><span class="sxs-lookup"><span data-stu-id="c9a3d-212">$blobContainerName</span></span></td><td><span data-ttu-id="c9a3d-213">tooupload hello 데이터를 저장할 Blob 컨테이너를 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-213">hello Blob container where you want tooupload hello data to.</span></span></td></tr>
    </table>
2. <span data-ttu-id="c9a3d-214">Azure PowerShell ISE를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-214">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="c9a3d-215">3.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-215">3.</span></span> <span data-ttu-id="c9a3d-216">Hello를 hello 스크립트 창에 스크립트를 다음에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-216">Paste hello following script into hello script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #Region - Variables
    $localFolder = "C:\Tutorials\FlightDelay\2013Data"  # hello source folder
    $destFolder = "tutorials/flightdelay/2013data"     #hello blob name prefix for hello files toobe uploaded
    #EndRegion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #Region - Copy hello file from local workstation tooAzure Blob storage
    if (test-path -Path $localFolder)
    {
        foreach ($item in Get-ChildItem -Path $localFolder){
            $fileName = "$localFolder\$item"
            $blobName = "$destFolder/$item"

            Write-Host "Copying $fileName too$blobName" -ForegroundColor Green

            Set-AzureStorageBlobContent -File $fileName -Container $blobContainerName -Blob $blobName -Context $storageContext
        }
    }
    else
    {
        Write-Host "hello source folder on hello workstation doesn't exist" -ForegroundColor Red
    }

    # List hello uploaded files on HDInsight
    Get-AzureStorageBlob -Container $blobContainerName  -Context $storageContext -Prefix $destFolder
    #EndRegion
    ```
4. <span data-ttu-id="c9a3d-217">키를 눌러 **F5** toorun hello 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-217">Press **F5** toorun hello script.</span></span>

<span data-ttu-id="c9a3d-218">Toouse hello 파일을 업로드 하기 위한 다른 방법을 선택 하면 파일 경로 hello 자습서/flightdelay/데이터 인지를 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-218">If you choose toouse a different method for uploading hello files, please make sure hello file path is tutorials/flightdelay/data.</span></span> <span data-ttu-id="c9a3d-219">hello hello 파일에 액세스 하기 위한 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-219">hello syntax for accessing hello files is:</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/tutorials/flightdelay/data

<span data-ttu-id="c9a3d-220">hello 경로 자습서/flightdelay/데이터는 hello 파일을 업로드 했을 때 만들었으므로 hello 가상 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-220">hello path tutorials/flightdelay/data is hello virtual folder you created when you uploaded hello files.</span></span> <span data-ttu-id="c9a3d-221">달마다 하나씩 12개의 파일이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-221">Verify that there are 12 files, one for each month.</span></span>

> [!NOTE]
> <span data-ttu-id="c9a3d-222">Hello 하이브 쿼리 tooread hello 새 위치에서 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-222">You must update hello Hive query tooread from hello new location.</span></span>
>
> <span data-ttu-id="c9a3d-223">Hello 컨테이너 액세스 권한을 toobe 공용 구성 하거나 hello 저장소 계정 toohello HDInsight 클러스터를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-223">You must either configure hello container access permission toobe public or bind hello Storage account toohello HDInsight cluster.</span></span> <span data-ttu-id="c9a3d-224">그렇지 않으면 hello 하이브 쿼리 문자열 hello 데이터 파일 수 tooaccess 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-224">Otherwise, hello Hive query string will not be able tooaccess hello data files.</span></span>

- - -

## <span data-ttu-id="c9a3d-225"><a id="appendix-b"></a>부록 B - HiveQL 스크립트 만들기 및 업로드</span><span class="sxs-lookup"><span data-stu-id="c9a3d-225"><a id="appendix-b"></a>Appendix B - Create and upload a HiveQL script</span></span>
<span data-ttu-id="c9a3d-226">Azure PowerShell을 사용 하는 스크립트 파일에 한 번, 패키지 hello HiveQL 문은에 여러 HiveQL 문은 하나 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-226">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package hello HiveQL statement into a script file.</span></span> <span data-ttu-id="c9a3d-227">이 섹션에서는 어떻게 toocreate HiveQL 스크립트 및 업로드 hello 스크립트 tooAzure Blob 저장소 Azure PowerShell을 사용 하 여 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-227">This section shows you how toocreate a HiveQL script and upload hello script tooAzure Blob storage by using Azure PowerShell.</span></span> <span data-ttu-id="c9a3d-228">하이브는 hello HiveQL 스크립트 toobe Azure Blob 저장소에 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-228">Hive requires hello HiveQL scripts toobe stored in Azure Blob storage.</span></span>

<span data-ttu-id="c9a3d-229">hello HiveQL 스크립트 hello 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-229">hello HiveQL script will perform hello following:</span></span>

1. <span data-ttu-id="c9a3d-230">**Hello delays_raw 테이블을 삭제**hello 테이블이 이미 존재 하는 경우, 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-230">**Drop hello delays_raw table**, in case hello table already exists.</span></span>
2. <span data-ttu-id="c9a3d-231">**Hello delays_raw 외부 하이브 테이블 만들기** hello 비행 지연 파일을 toohello Blob 저장소 위치를 가리키는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-231">**Create hello delays_raw external Hive table** pointing toohello Blob storage location with hello flight delay files.</span></span> <span data-ttu-id="c9a3d-232">이 쿼리는 필드는 ","로 구분되고 줄은 "\n"로 끝나도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-232">This query specifies that fields are delimited by "," and that lines are terminated by "\n".</span></span> <span data-ttu-id="c9a3d-233">필드 값 하이브는 필드 구분 기호는 쉼표와 필드 값의 일부인 하나를 구별할 수 없으므로 쉼표를 사용할 경우 이것은 문제가 (원점에 대 한 필드 값의 대/소문자 hello 변수인\_도시\_이름과 DEST\_ 도시\_이름).</span><span class="sxs-lookup"><span data-stu-id="c9a3d-233">This poses a problem when field values contain commas because Hive cannot differentiate between a comma that is a field delimiter and a one that is part of a field value (which is hello case in field values for ORIGIN\_CITY\_NAME and DEST\_CITY\_NAME).</span></span> <span data-ttu-id="c9a3d-234">tooaddress이,이 hello 쿼리 열으로 잘못 분할은 toohold 데이터 임시 열을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-234">tooaddress this, hello query creates TEMP columns toohold data that is incorrectly split into columns.</span></span>
3. <span data-ttu-id="c9a3d-235">**Hello 지연 테이블을 삭제**hello 테이블이 이미 존재 하는 경우, 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-235">**Drop hello delays table**, in case hello table already exists.</span></span>
4. <span data-ttu-id="c9a3d-236">**Hello 지연 테이블 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-236">**Create hello delays table**.</span></span> <span data-ttu-id="c9a3d-237">추가 처리 전에 hello 데이터를 유용한 tooclean 것 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-237">It is helpful tooclean up hello data before further processing.</span></span> <span data-ttu-id="c9a3d-238">이 쿼리는 새 테이블을 만듭니다 *지연*, hello delays_raw 테이블에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-238">This query creates a new table, *delays*, from hello delays_raw table.</span></span> <span data-ttu-id="c9a3d-239">참고 (앞서 언급 했 듯이) hello TEMP 열 복사 되지 않습니다 및 그 hello **부분 문자열** 함수는 hello 데이터에서 사용 되는 tooremove 따옴표입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-239">Note that hello TEMP columns (as mentioned previously) are not copied, and that hello **substring** function is used tooremove quotation marks from hello data.</span></span>
5. <span data-ttu-id="c9a3d-240">**도시 이름별으로 hello 평균 날씨 지연 및 그룹 hello 결과 계산 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c9a3d-240">**Compute hello average weather delay and groups hello results by city name.**</span></span> <span data-ttu-id="c9a3d-241">Hello 결과 tooBlob 저장소를 출력도 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-241">It will also output hello results tooBlob storage.</span></span> <span data-ttu-id="c9a3d-242">짧으며 hello 쿼리 아포스트로피 hello 데이터에서 제거 됩니다 hello에 대 한 값에 행을 제외 합니다 **weather_delay** null입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-242">Note that hello query will remove apostrophes from hello data and will exclude rows where hello value for **weather_delay** is null.</span></span> <span data-ttu-id="c9a3d-243">이 작업은 이 자습서의 뒷부분에서 사용되는 Sqoop가 기본적으로 이러한 값을 정상적으로 처리하지 않기 때문에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-243">This is necessary because Sqoop, used later in this tutorial, doesn't handle those values gracefully by default.</span></span>

<span data-ttu-id="c9a3d-244">전체 hello HiveQL 명령 목록을 참조 하십시오. [데이터 정의 언어 하이브][hadoop-hiveql]합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-244">For a full list of hello HiveQL commands, see [Hive Data Definition Language][hadoop-hiveql].</span></span> <span data-ttu-id="c9a3d-245">각 HiveQL 명령은 세미콜론으로 끝나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-245">Each HiveQL command must terminate with a semicolon.</span></span>

<span data-ttu-id="c9a3d-246">**toocreate HiveQL 스크립트 파일**</span><span class="sxs-lookup"><span data-stu-id="c9a3d-246">**toocreate a HiveQL script file**</span></span>

1. <span data-ttu-id="c9a3d-247">Hello 매개 변수를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-247">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="c9a3d-248">변수 이름</span><span class="sxs-lookup"><span data-stu-id="c9a3d-248">Variable Name</span></span></th><th><span data-ttu-id="c9a3d-249">참고 사항</span><span class="sxs-lookup"><span data-stu-id="c9a3d-249">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="c9a3d-250">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="c9a3d-250">$storageAccountName</span></span></td><td><span data-ttu-id="c9a3d-251">hello tooupload hello HiveQL 스크립트를 저장할 Azure 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-251">hello Azure Storage account where you want tooupload hello HiveQL script to.</span></span></td></tr>
    <tr><td><span data-ttu-id="c9a3d-252">$blobContainerName</span><span class="sxs-lookup"><span data-stu-id="c9a3d-252">$blobContainerName</span></span></td><td><span data-ttu-id="c9a3d-253">tooupload hello HiveQL 스크립트를 저장할 Blob 컨테이너를 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-253">hello Blob container where you want tooupload hello HiveQL script to.</span></span></td></tr>
    </table>
2. <span data-ttu-id="c9a3d-254">Azure PowerShell ISE를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-254">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="c9a3d-255">3.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-255">3.</span></span> <span data-ttu-id="c9a3d-256">복사한 hello 스크립트 창에 스크립트를 다음 hello를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-256">Copy and paste hello following script into hello script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Blob storage variables
        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #region - Define variables
    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    # hello HiveQL script file is exported as this file before it's uploaded tooBlob storage
    $hqlLocalFileName = "e:\tutorials\flightdelay\flightdelays.hql"

    # hello HiveQL script file will be uploaded tooBlob storage as this blob name
    $hqlBlobName = "tutorials/flightdelay/flightdelays.hql"

    # These two constants are used by hello HiveQL script file
    #$srcDataFolder = "tutorials/flightdelay/data"
    $dstDataFolder = "/tutorials/flightdelay/output"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #region - Validate hello file and file path

    # Check if a file with hello same file name already exists on hello workstation
    Write-Host "`nvalidating hello folder structure on hello workstation for saving hello HQL script file ..."  -ForegroundColor Green
    if (test-path $hqlLocalFileName){

        $isDelete = Read-Host 'hello file, ' $hqlLocalFileName ', exists.  Do you want toooverwirte it? (Y/N)'

        if ($isDelete.ToLower() -ne "y")
        {
            Exit
        }
    }

    # Create hello folder if it doesn't exist
    $folder = split-path $hqlLocalFileName
    if (-not (test-path $folder))
    {
        Write-Host "`nCreating folder, $folder ..." -ForegroundColor Green

        new-item $folder -ItemType directory
    }
    #end region

    #region - Write hello Hive script into a local file
    Write-Host "`nWriting hello Hive script into a file on your workstation ..." `
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

    #region - Upload hello Hive script toohello default Blob container
    Write-Host "`nUploading hello Hive script toohello default Blob container ..." -ForegroundColor Green

    # Create a storage context object
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Upload hello file from local workstation tooBlob storage
    Set-AzureStorageBlobContent -File $hqlLocalFileName -Container $blobContainerName -Blob $hqlBlobName -Context $destContext
    #endregion

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

    <span data-ttu-id="c9a3d-257">Hello 스크립트에 사용 되는 hello 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-257">Here are hello variables used in hello script:</span></span>

   * <span data-ttu-id="c9a3d-258">**$hqlLocalFileName** -hello 스크립트 파일을 저장 hello HiveQL 스크립트 로컬로 업로드 하기 전에 tooBlob 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-258">**$hqlLocalFileName** - hello script saves hello HiveQL script file locally before uploading it tooBlob storage.</span></span> <span data-ttu-id="c9a3d-259">Hello 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-259">This is hello file name.</span></span> <span data-ttu-id="c9a3d-260">hello 기본값은 <u>C:\tutorials\flightdelay\flightdelays.hql</u>합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-260">hello default value is <u>C:\tutorials\flightdelay\flightdelays.hql</u>.</span></span>
   * <span data-ttu-id="c9a3d-261">**$hqlBlobName** -hello Azure Blob 저장소에에서 사용 된 hello HiveQL 스크립트 파일 blob 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-261">**$hqlBlobName** - This is hello HiveQL script file blob name used in hello Azure Blob storage.</span></span> <span data-ttu-id="c9a3d-262">hello 기본값은 tutorials/flightdelay/flightdelays.hql입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-262">hello default value is tutorials/flightdelay/flightdelays.hql.</span></span> <span data-ttu-id="c9a3d-263">없기 때문에 hello 파일이 기록 될 직접 tooAzure Blob 저장소, 하지는 "/" hello blob 이름의 hello 시작 부분에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-263">Because hello file will be written directly tooAzure Blob storage, there is NOT a "/" at hello beginning of hello blob name.</span></span> <span data-ttu-id="c9a3d-264">Blob 저장소에서 tooaccess hello 파일을 사용 하도록 하려는 경우는 "/" hello hello 파일 이름 앞에 tooadd를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-264">If you want tooaccess hello file from Blob storage, you will need tooadd a "/" at hello beginning of hello file name.</span></span>
   * <span data-ttu-id="c9a3d-265">**$srcDataFolder** 및 **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"</span><span class="sxs-lookup"><span data-stu-id="c9a3d-265">**$srcDataFolder** and **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"</span></span>

- - -
## <span data-ttu-id="c9a3d-266"><a id="appendix-c"></a>부록 C-hello Sqoop 작업 출력에 대 한 Azure SQL 데이터베이스 준비</span><span class="sxs-lookup"><span data-stu-id="c9a3d-266"><a id="appendix-c"></a>Appendix C - Prepare an Azure SQL database for hello Sqoop job output</span></span>
<span data-ttu-id="c9a3d-267">**tooprepare hello SQL 데이터베이스 (병합이 Sqoop 스크립트 hello로)**</span><span class="sxs-lookup"><span data-stu-id="c9a3d-267">**tooprepare hello SQL database (merge this with hello Sqoop script)**</span></span>

1. <span data-ttu-id="c9a3d-268">Hello 매개 변수를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-268">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="c9a3d-269">변수 이름</span><span class="sxs-lookup"><span data-stu-id="c9a3d-269">Variable Name</span></span></th><th><span data-ttu-id="c9a3d-270">참고 사항</span><span class="sxs-lookup"><span data-stu-id="c9a3d-270">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="c9a3d-271">$sqlDatabaseServerName</span><span class="sxs-lookup"><span data-stu-id="c9a3d-271">$sqlDatabaseServerName</span></span></td><td><span data-ttu-id="c9a3d-272">hello hello Azure SQL 데이터베이스 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-272">hello name of hello Azure SQL database server.</span></span> <span data-ttu-id="c9a3d-273">아무것도 입력 toocreate 새 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-273">Enter nothing toocreate a new server.</span></span></td></tr>
    <tr><td><span data-ttu-id="c9a3d-274">$sqlDatabaseUsername</span><span class="sxs-lookup"><span data-stu-id="c9a3d-274">$sqlDatabaseUsername</span></span></td><td><span data-ttu-id="c9a3d-275">hello hello Azure SQL 데이터베이스 서버에 대 한 로그인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-275">hello login name for hello Azure SQL database server.</span></span> <span data-ttu-id="c9a3d-276">$SqlDatabaseServerName 기존 서버 이면 hello 로그인 및 로그인 암호가 사용 되는 tooauthenticate hello 서버와는입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-276">If $sqlDatabaseServerName is an existing server, hello login and login password are used tooauthenticate with hello server.</span></span> <span data-ttu-id="c9a3d-277">그렇지 않으면 새 서버를 사용 하는 toocreate 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-277">Otherwise they are used toocreate a new server.</span></span></td></tr>
    <tr><td><span data-ttu-id="c9a3d-278">$sqlDatabasePassword</span><span class="sxs-lookup"><span data-stu-id="c9a3d-278">$sqlDatabasePassword</span></span></td><td><span data-ttu-id="c9a3d-279">hello hello Azure SQL 데이터베이스 서버에 대 한 로그인 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-279">hello login password for hello Azure SQL database server.</span></span></td></tr>
    <tr><td><span data-ttu-id="c9a3d-280">$sqlDatabaseLocation</span><span class="sxs-lookup"><span data-stu-id="c9a3d-280">$sqlDatabaseLocation</span></span></td><td><span data-ttu-id="c9a3d-281">이 값은 새 Azure 데이터베이스 서버를 만드는 경우에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-281">This value is used only when you're creating a new Azure database server.</span></span></td></tr>
    <tr><td><span data-ttu-id="c9a3d-282">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="c9a3d-282">$sqlDatabaseName</span></span></td><td><span data-ttu-id="c9a3d-283">hello Sqoop 작업에 대 한 toocreate hello AvgDelays 표를 사용 하는 hello SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-283">hello SQL database used toocreate hello AvgDelays table for hello Sqoop job.</span></span> <span data-ttu-id="c9a3d-284">이 매개 변수를 비워 두면 HDISqoop라는 데이터베이스가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-284">Leaving it blank will create a database called HDISqoop.</span></span> <span data-ttu-id="c9a3d-285">hello Sqoop 작업 출력에 대 한 hello 테이블 이름은 AvgDelays를입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-285">hello table name for hello Sqoop job output is AvgDelays.</span></span> </td></tr>
    </table>
2. <span data-ttu-id="c9a3d-286">Azure PowerShell ISE를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-286">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="c9a3d-287">3.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-287">3.</span></span> <span data-ttu-id="c9a3d-288">복사한 hello 스크립트 창에 스크립트를 다음 hello를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-288">Copy and paste hello following script into hello script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Resource group variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure resource group name. It will be created if it doesn't exist.")]
        [String]$resourceGroupName,

        # SQL database server variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database Server Name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseServer,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user.")]
        [String]$sqlDatabaseLogin,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user password.")]
        [String]$sqlDatabasePassword,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello region toocreate hello Database in.")]
        [String]$sqlDatabaseLocation,   #For example, West US.

        # SQL database variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello database name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseName # specify hello database name if you have one created. Otherwise use "" toohave hello script create one for you.
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

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
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

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
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

    #region -  Execute an SQL command toocreate hello AvgDelays table

    Write-Host "`nCreating SQL Database table ..."  -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = $sqlCreateAvgDelaysTable
    $cmd.executenonquery()

    $conn.close()

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

   > [!NOTE]
   > <span data-ttu-id="c9a3d-289">hello 스크립트 사용 하 여 representational 상태 (transfer) 서비스, http://bot.whatismyipaddress.com, tooretrieve 외부 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-289">hello script uses a representational state transfer (REST) service, http://bot.whatismyipaddress.com, tooretrieve your external IP address.</span></span> <span data-ttu-id="c9a3d-290">hello IP 주소는 SQL 데이터베이스 서버에 대 한 방화벽 규칙을 만드는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-290">hello IP address is used for creating a firewall rule for your SQL database server.</span></span>

    <span data-ttu-id="c9a3d-291">Hello 스크립트에 사용 되는 일부 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-291">Here are some variables used in hello script:</span></span>

   * <span data-ttu-id="c9a3d-292">**$ipAddressRestService** -hello 기본값은 http://bot.whatismyipaddress.com 합니다. 외부 IP 주소를 가져오기 위한 공용 IP 주소 REST 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-292">**$ipAddressRestService** - hello default value is http://bot.whatismyipaddress.com. It is a public IP address REST service for getting your external IP address.</span></span> <span data-ttu-id="c9a3d-293">원하는 경우 다른 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-293">You can use other services if you want.</span></span> <span data-ttu-id="c9a3d-294">hello 서비스를 통해 검색 된 hello 외부 IP 주소 (사용 하 여 Windows PowerShell 스크립트) 워크스테이션에서 hello 데이터베이스에 액세스할 수 있도록 Azure SQL 데이터베이스 서버에 대 한 방화벽 규칙 사용된 toocreate 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-294">hello external IP address retrieved through hello service will be used toocreate a firewall rule for your Azure SQL database server, so that you can access hello database from your workstation (by using a Windows PowerShell script).</span></span>
   * <span data-ttu-id="c9a3d-295">**$fireWallRuleName** -hello Azure SQL 데이터베이스 서버에 대 한 hello 방화벽 규칙의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-295">**$fireWallRuleName** - This is hello name of hello firewall rule for hello Azure SQL database server.</span></span> <span data-ttu-id="c9a3d-296">기본 이름은 hello <u>FlightDelay</u>합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-296">hello default name is <u>FlightDelay</u>.</span></span> <span data-ttu-id="c9a3d-297">원하는 경우 이름을 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-297">You can rename it if you want.</span></span>
   * <span data-ttu-id="c9a3d-298">**$sqlDatabaseMaxSizeGB** - 이 값은 새 Azure SQL 데이터베이스 서버를 만드는 경우에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-298">**$sqlDatabaseMaxSizeGB** - This value is used only when you're creating a new Azure SQL database server.</span></span> <span data-ttu-id="c9a3d-299">hello 기본값은 10GB입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-299">hello default value is 10GB.</span></span> <span data-ttu-id="c9a3d-300">이 자습서에서는 크기가 10GB이면 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-300">10GB is sufficient for this tutorial.</span></span>
   * <span data-ttu-id="c9a3d-301">**$sqlDatabaseName** - 이 값은 새 Azure SQL 데이터베이스를 만드는 경우에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-301">**$sqlDatabaseName** - This value is used only when you're creating a new Azure SQL database.</span></span> <span data-ttu-id="c9a3d-302">hello 기본값은 HDISqoop입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-302">hello default value is HDISqoop.</span></span> <span data-ttu-id="c9a3d-303">이름을 변경한 후 hello Sqoop Windows PowerShell 스크립트를 적절 하 게 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-303">If you rename it, you must update hello Sqoop Windows PowerShell script accordingly.</span></span>
4. <span data-ttu-id="c9a3d-304">키를 눌러 **F5** toorun hello 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-304">Press **F5** toorun hello script.</span></span>
5. <span data-ttu-id="c9a3d-305">Hello 스크립트 출력의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-305">Validate hello script output.</span></span> <span data-ttu-id="c9a3d-306">Hello 스크립트가 성공적으로 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-306">Make sure hello script ran successfully.</span></span>

## <span data-ttu-id="c9a3d-307"><a id="nextsteps"></a> 다음 단계</span><span class="sxs-lookup"><span data-stu-id="c9a3d-307"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="c9a3d-308">알아야 이제 방법을 파일 tooAzure Blob 저장소 tooupload hello 데이터 Azure Blob 저장소를 사용 하 여 toopopulate 하이브 테이블 방법 어떻게 toorun 하이브 쿼리를 방법과 toouse HDFS tooan Azure SQL 데이터베이스에서 Sqoop tooexport 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="c9a3d-308">Now you understand how tooupload a file tooAzure Blob storage, how toopopulate a Hive table by using hello data from Azure Blob storage, how toorun Hive queries, and how toouse Sqoop tooexport data from HDFS tooan Azure SQL database.</span></span> <span data-ttu-id="c9a3d-309">더 toolearn hello 다음 문서를 참조:</span><span class="sxs-lookup"><span data-stu-id="c9a3d-309">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="c9a3d-310">[HDInsight 시작][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="c9a3d-310">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="c9a3d-311">[HDInsight에서 Hive 사용][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="c9a3d-311">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="c9a3d-312">[HDInsight에서 Oozie 사용][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="c9a3d-312">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="c9a3d-313">[HDInsight에서 Sqoop 사용][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="c9a3d-313">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="c9a3d-314">[HDInsight에서 Pig 사용][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="c9a3d-314">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="c9a3d-315">[HDInsight용 Java MapReduce 프로그램 개발][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="c9a3d-315">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

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
