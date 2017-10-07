---
title: "Azure HDInsight 하이브 ODBC 드라이버-hello로 aaaConnect Excel tooHadoop | Microsoft Docs"
description: "어떻게 tooset를 사용 하 여 hello Excel tooquery 데이터 Microsoft Excel에서 HDInsight 클러스터에 대 한 Microsoft 하이브 ODBC 드라이버에 알아봅니다."
keywords: hadoop excel, hive excel, hive odbc
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
tags: azure-portal
editor: cgronlun
ms.assetid: a7665a14-0211-4521-b3e7-3b26e8029cc0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: f01f89e7d4203c739d56079dc589fc11f4aa2174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-toohadoop-in-azure-hdinsight-with-hello-microsoft-hive-odbc-driver"></a><span data-ttu-id="e8b2d-104">Azure HDInsight의 Excel tooHadoop hello Microsoft 하이브 ODBC 드라이버를 사용 하 여 연결</span><span class="sxs-lookup"><span data-stu-id="e8b2d-104">Connect Excel tooHadoop in Azure HDInsight with hello Microsoft Hive ODBC driver</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="e8b2d-105">Microsoft의 빅 데이터 솔루션인 Azure HDInsight hello 하 여 배포 된 Apache Hadoop 클러스터와 Microsoft BI (Business Intelligence) 구성 요소를 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-105">Microsoft's Big Data solution integrates Microsoft Business Intelligence (BI) components with Apache Hadoop clusters that have been deployed by hello Azure HDInsight.</span></span> <span data-ttu-id="e8b2d-106">이 통합의 예로 hello 기능 tooconnect Excel toohello 하이브의 데이터 웨어하우스를 hello Microsoft 하이브 데이터베이스 ODBC (Open Connectivity) 드라이버를 사용 하 여 HDInsight의 Hadoop 클러스터.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-106">An example of this integration is hello ability tooconnect Excel toohello Hive data warehouse of a Hadoop cluster in HDInsight using hello Microsoft Hive Open Database Connectivity (ODBC) Driver.</span></span>

<span data-ttu-id="e8b2d-107">HDInsight 클러스터와 다른 데이터 소스와 연결 된 가능한 tooconnect hello 데이터 이기도, 다른 (비-HDInsight) 포함 하 여 Hadoop 클러스터 hello를 사용 하 여 Excel에서 Microsoft Power Query 추가 기능에 Excel 용입니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-107">It is also possible tooconnect hello data associated with an HDInsight cluster and other data sources, including other (non-HDInsight) Hadoop clusters, from Excel using hello Microsoft Power Query add-in for Excel.</span></span> <span data-ttu-id="e8b2d-108">설치 및 파워 쿼리 사용에 대 한 정보를 참조 하십시오. [파워 쿼리를 통해 Excel 연결 tooHDInsight][hdinsight-power-query]합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-108">For information on installing and using Power Query, see [Connect Excel tooHDInsight with Power Query][hdinsight-power-query].</span></span>

> [!NOTE]
> <span data-ttu-id="e8b2d-109">단계를 hello 하는 동안이 문서는 Linux 중 하나는 함께 사용할 수 있습니다 이거나 Windows 기반 HDInsight 클러스터를 Windows hello 클라이언트 워크스테이션에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-109">While hello steps in this article can be used with either a Linux or Windows-based HDInsight cluster, Windows is required for hello client workstation.</span></span>
> 
> 

<span data-ttu-id="e8b2d-110">**필수 조건**:</span><span class="sxs-lookup"><span data-stu-id="e8b2d-110">**Prerequisites**:</span></span>

<span data-ttu-id="e8b2d-111">이 문서를 시작 하기 전에 다음 항목 hello가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-111">Before you begin this article, you must have hello following items:</span></span>

* <span data-ttu-id="e8b2d-112">**HDInsight 클러스터**.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-112">**An HDInsight cluster**.</span></span> <span data-ttu-id="e8b2d-113">하나의 toocreate 참조 [Azure HDInsight 시작][hdinsight-get-started]합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-113">toocreate one, see [Get started with Azure HDInsight][hdinsight-get-started].</span></span>
* <span data-ttu-id="e8b2d-114">**워크스테이션** </span><span class="sxs-lookup"><span data-stu-id="e8b2d-114">**A workstation** with Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="install-microsoft-hive-odbc-driver"></a><span data-ttu-id="e8b2d-115">Microsoft Hive ODBC 드라이버 설치</span><span class="sxs-lookup"><span data-stu-id="e8b2d-115">Install Microsoft Hive ODBC driver</span></span>
<span data-ttu-id="e8b2d-116">에서 다운로드 및 설치 Microsoft ODBC Driver 하이브 hello [다운로드 센터][hive-odbc-driver-download]합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-116">Download and install Microsoft Hive ODBC Driver from hello [Download Center][hive-odbc-driver-download].</span></span>

<span data-ttu-id="e8b2d-117">이 드라이버는 32비트 또는 64비트 버전의 Windows 7, Windows 8, Windows 10, Windows Server 2008 R2 및 Windows Server 2012에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-117">This driver can be installed on 32-bit or 64-bit versions of Windows 7, Windows 8, Windows 10, Windows Server 2008 R2, and Windows Server 2012.</span></span> <span data-ttu-id="e8b2d-118">hello 드라이버를 사용 하면 연결 tooAzure HDInsight (버전 1.6 이상) 및 Azure HDInsight 에뮬레이터 (v.1.0.0.0 및 이후 버전).</span><span class="sxs-lookup"><span data-stu-id="e8b2d-118">hello driver allows connection tooAzure HDInsight (version 1.6 and later) and Azure HDInsight Emulator (v.1.0.0.0 and later).</span></span> <span data-ttu-id="e8b2d-119">Hello ODBC 드라이버를 사용 하는 hello 응용 프로그램의 hello 버전과 일치 하는 hello 버전을 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-119">You shall install hello version that matches hello version of hello application where you use hello ODBC driver.</span></span> <span data-ttu-id="e8b2d-120">이 자습서에 대 한 hello 드라이버 Office Excel에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-120">For this tutorial, hello driver is used from Office Excel.</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="e8b2d-121">Hive ODBC 데이터 원본 만들기</span><span class="sxs-lookup"><span data-stu-id="e8b2d-121">Create Hive ODBC data source</span></span>
<span data-ttu-id="e8b2d-122">hello 다음 단계 방법을 보여 줍니다 toocreate 하이브 ODBC 데이터 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-122">hello following steps show you how toocreate a Hive ODBC Data Source.</span></span>

1. <span data-ttu-id="e8b2d-123">Windows 8 또는 Windows 10에서 hello Windows 키 tooopen hello 시작 화면에서를 누르고 다음 입력 **데이터 소스**합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-123">From Windows 8 or Windows 10, press hello Windows key tooopen hello Start screen, and then type **data sources**.</span></span>
2. <span data-ttu-id="e8b2d-124">Office 버전에 따라 **ODBC 데이터 원본 설정(32비트)** 또는 **ODBC 데이터 원본 설정(64비트)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-124">Click **Set up ODBC Data sources (32-bit)** or **Set up ODBC Data Sources (64-bit)** depending on your Office version.</span></span> <span data-ttu-id="e8b2d-125">Windows 7을 사용하는 경우 **관리 도구**에서 **ODBC 데이터 원본(32비트)** 또는 **ODBC 데이터 원본(64비트)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-125">If you are using Windows 7, choose **ODBC Data Sources (32 bit)** or **ODBC Data Sources (64 bit)** from **Administrative Tools**.</span></span> <span data-ttu-id="e8b2d-126">Hello 표시 **ODBC 데이터 원본 관리자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-126">You shall see hello **ODBC Data Source Administrator** dialog.</span></span>
   
    <span data-ttu-id="e8b2d-127">![OBDC 데이터 원본 관리자](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "ODBC 데이터 원본 관리자를 사용하여 DSN 구성")</span><span class="sxs-lookup"><span data-stu-id="e8b2d-127">![OBDC data source administrator](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "Configure a DSN using ODBC Data Source Administrator")</span></span>

3. <span data-ttu-id="e8b2d-128">사용자 DNS에서 클릭 **추가** tooopen hello **새 데이터 원본 만들기** 마법사.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-128">From User DNS, click **Add** tooopen hello **Create New Data Source** wizard.</span></span>
4. <span data-ttu-id="e8b2d-129">**Microsoft Hive ODBC 드라이버**를 선택한 후 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-129">Select **Microsoft Hive ODBC Driver**, and then click **Finish**.</span></span> <span data-ttu-id="e8b2d-130">Hello 표시 **Microsoft 하이브 ODBC 드라이버 DNS 설정** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-130">You shall see hello **Microsoft Hive ODBC Driver DNS Setup** dialog.</span></span>
5. <span data-ttu-id="e8b2d-131">입력 하거나 다음 값에는 hello 선택:</span><span class="sxs-lookup"><span data-stu-id="e8b2d-131">Type or select hello following values:</span></span>
   
   | <span data-ttu-id="e8b2d-132">속성</span><span class="sxs-lookup"><span data-stu-id="e8b2d-132">Property</span></span> | <span data-ttu-id="e8b2d-133">설명</span><span class="sxs-lookup"><span data-stu-id="e8b2d-133">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="e8b2d-134">데이터 원본 이름</span><span class="sxs-lookup"><span data-stu-id="e8b2d-134">Data Source Name</span></span> |<span data-ttu-id="e8b2d-135">이름 tooyour 데이터 소스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-135">Give a name tooyour data source</span></span> |
   |  <span data-ttu-id="e8b2d-136">호스트</span><span class="sxs-lookup"><span data-stu-id="e8b2d-136">Host</span></span> |<span data-ttu-id="e8b2d-137">&lt;HDInsightClusterName>.azurehdinsight.net을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-137">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="e8b2d-138">예를 들면 myHDICluster.azurehdinsight.net과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-138">For example, myHDICluster.azurehdinsight.net</span></span> |
   |  <span data-ttu-id="e8b2d-139">포트</span><span class="sxs-lookup"><span data-stu-id="e8b2d-139">Port</span></span> |<span data-ttu-id="e8b2d-140"><strong>443</strong>을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-140">Use <strong>443</strong>.</span></span> <span data-ttu-id="e8b2d-141">(이 포트를 변경 하지 563 too443에서.)</span><span class="sxs-lookup"><span data-stu-id="e8b2d-141">(This port has been changed from 563 too443.)</span></span> |
   |  <span data-ttu-id="e8b2d-142">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="e8b2d-142">Database</span></span> |<span data-ttu-id="e8b2d-143"><strong>기본값</strong>을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-143">Use <strong>Default</strong>.</span></span> |
   |  <span data-ttu-id="e8b2d-144">메커니즘</span><span class="sxs-lookup"><span data-stu-id="e8b2d-144">Mechanism</span></span> |<span data-ttu-id="e8b2d-145"><strong>Azure HDInsight Service</strong> 선택</span><span class="sxs-lookup"><span data-stu-id="e8b2d-145">Select <strong>Azure HDInsight Service</strong></span></span> |
   |  <span data-ttu-id="e8b2d-146">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="e8b2d-146">User Name</span></span> |<span data-ttu-id="e8b2d-147">HDInsight 클러스터 HTTP 사용자의 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-147">Enter HDInsight cluster HTTP user username.</span></span> <span data-ttu-id="e8b2d-148">hello 기본 사용자 이름은 <strong>admin</strong>합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-148">hello default username is <strong>admin</strong>.</span></span> |
   |  <span data-ttu-id="e8b2d-149">암호</span><span class="sxs-lookup"><span data-stu-id="e8b2d-149">Password</span></span> |<span data-ttu-id="e8b2d-150">HDInsight 클러스터 사용자 암호 입력</span><span class="sxs-lookup"><span data-stu-id="e8b2d-150">Enter HDInsight cluster user password.</span></span> |
   
    </table>
   
    <span data-ttu-id="e8b2d-151">몇 가지 중요 한 매개 변수 toobe 클릭할 때 알고 있는 **고급 옵션**:</span><span class="sxs-lookup"><span data-stu-id="e8b2d-151">There are some important parameters toobe aware of when you click **Advanced Options**:</span></span>
   
   | <span data-ttu-id="e8b2d-152">매개 변수</span><span class="sxs-lookup"><span data-stu-id="e8b2d-152">Parameter</span></span> | <span data-ttu-id="e8b2d-153">설명</span><span class="sxs-lookup"><span data-stu-id="e8b2d-153">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="e8b2d-154">Use Native Query</span><span class="sxs-lookup"><span data-stu-id="e8b2d-154">Use Native Query</span></span> |<span data-ttu-id="e8b2d-155">옵션을 선택 하면 hello ODBC 드라이버는 HiveQL를 tooconvert TSQL 시도 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-155">When it is selected, hello ODBC driver does NOT try tooconvert TSQL into HiveQL.</span></span> <span data-ttu-id="e8b2d-156">순수 HiveQL 문을 제출하는 것이 확실한 경우에만 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-156">You shall use it only if you are 100% sure you are submitting pure HiveQL statements.</span></span> <span data-ttu-id="e8b2d-157">TooSQL 서버 또는 Azure SQL 데이터베이스를 연결할 때 그대로 두어야 선택 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-157">When connecting tooSQL Server or Azure SQL Database, you should leave it unchecked.</span></span> |
   |  <span data-ttu-id="e8b2d-158">Rows fetched per block</span><span class="sxs-lookup"><span data-stu-id="e8b2d-158">Rows fetched per block</span></span> |<span data-ttu-id="e8b2d-159">많은 수의 레코드를 인출 하는 경우이 매개 변수를 튜닝 최적의 성능이 필요한 tooensure 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-159">When fetching a large number of records, tuning this parameter may be required tooensure optimal performances.</span></span> |
   |  <span data-ttu-id="e8b2d-160">Default string column length, Binary column length, Decimal column scale</span><span class="sxs-lookup"><span data-stu-id="e8b2d-160">Default string column length, Binary column length, Decimal column scale</span></span> |<span data-ttu-id="e8b2d-161">hello 데이터 형식 길이 정밀도 데이터 반환 방법에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-161">hello data type lengths and precisions may affect how data is returned.</span></span> <span data-ttu-id="e8b2d-162">잘못 된 정보가 toobe 인해 반환 된 소멸자의 정밀도 및/또는 잘림 tooloss 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-162">They cause incorrect information toobe returned due tooloss of precision and/or truncation.</span></span> |

    <span data-ttu-id="e8b2d-163">![고급 옵션](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "고급 DSN 구성 옵션")</span><span class="sxs-lookup"><span data-stu-id="e8b2d-163">![Advanced options](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "Advanced DSN configuration options")</span></span>

1. <span data-ttu-id="e8b2d-164">클릭 **테스트** tootest hello 데이터 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-164">Click **Test** tootest hello data source.</span></span> <span data-ttu-id="e8b2d-165">표시 hello 데이터 소스를 올바르게 구성 된 경우 *테스트 완료 되었습니다!*합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-165">When hello data source is configured correctly, it shows *TESTS COMPLETED SUCCESSFULLY!*.</span></span>
2. <span data-ttu-id="e8b2d-166">클릭 **확인** tooclose hello 테스트 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-166">Click **OK** tooclose hello Test dialog.</span></span> <span data-ttu-id="e8b2d-167">새 데이터 원본을 hello hello에 나열 되어야은 **ODBC 데이터 원본 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-167">hello new data source shall be listed on hello **ODBC Data Source Administrator**.</span></span>
3. <span data-ttu-id="e8b2d-168">클릭 **확인** tooexit hello 마법사.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-168">Click **OK** tooexit hello wizard.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="e8b2d-169">HDInsight에서 Excel로 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="e8b2d-169">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="e8b2d-170">hello 다음 단계에서는 hello 방식으로 하이브 테이블에서 데이터를 tooimport hello 이전 섹션에서 만든 hello ODBC 데이터 원본을 사용 하 여 Excel 통합 문서에.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-170">hello following steps describe hello way tooimport data from a Hive table into an Excel workbook using hello ODBC data source that you created in hello previous section.</span></span>

1. <span data-ttu-id="e8b2d-171">Excel에서 새 통합 문서나 기존 통합 문서를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-171">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="e8b2d-172">Hello에서 **데이터** 탭을 클릭 **데이터 가져오기**, 클릭 **기타 원본**, 클릭 하 고 **에서 ODBC** toolaunch hello  **데이터 연결 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-172">From hello **Data** tab, click **Get Data**, click **From Other Sources**, and then click **From ODBC** toolaunch hello **Data Connection Wizard**.</span></span>
   
    <span data-ttu-id="e8b2d-173">![데이터 연결 마법사 열기](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "데이터 연결 마법사 열기")</span><span class="sxs-lookup"><span data-stu-id="e8b2d-173">![Open data connection wizard](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "Open data connection wizard")</span></span>
4. <span data-ttu-id="e8b2d-174">선택 hello 데이터 원본 이름 hello 마지막 섹션에서 만든 등록 한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-174">Select hello data source name that you created in hello last section, and then click **OK**.</span></span>
5. <span data-ttu-id="e8b2d-175">Hadoop 사용자 이름을 입력 하십시오 (hello 기본 이름은 관리자) 암호를 hello와 클릭 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-175">Enter Hadoop user name (hello default name is admin) and hello password, and then click **Connect**.</span></span>
6. <span data-ttu-id="e8b2d-176">탐색 창에서 **HIVE**를 확장하고 **default**를 확장한 후 **hivesampletable**을 클릭하고 **로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-176">On Navigator, expand **HIVE**, expand **default**, click **hivesampletable**, and then click **Load**.</span></span> <span data-ttu-id="e8b2d-177">걸리는 시간은 몇 초 전에 데이터를 가져온된 tooExcel 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-177">It takes a few seconds before data gets imported tooExcel.</span></span>

    <span data-ttu-id="e8b2d-178">![HDInsight Hive ODBC 탐색기](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "데이터 연결 열기 마법사")</span><span class="sxs-lookup"><span data-stu-id="e8b2d-178">![HDInsight Hive ODBC navigator](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "Open data connection wizard")</span></span>


## <a name="next-steps"></a><span data-ttu-id="e8b2d-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e8b2d-179">Next steps</span></span>
<span data-ttu-id="e8b2d-180">이 문서에서는 toouse hello HDInsight 서비스에서에서 Microsoft 하이브 ODBC 드라이버 tooretrieve 데이터를 Excel로 hello 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-180">In this article, you learned how toouse hello Microsoft Hive ODBC driver tooretrieve data from hello HDInsight Service into Excel.</span></span> <span data-ttu-id="e8b2d-181">마찬가지로, SQL 데이터베이스에 hello HDInsight 서비스에서에서 데이터를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-181">Similarly, you can retrieve data from hello HDInsight Service into SQL Database.</span></span> <span data-ttu-id="e8b2d-182">HDInsight 서비스에 대 한 가능한 tooupload 데이터 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-182">It is also possible tooupload data into an HDInsight Service.</span></span> <span data-ttu-id="e8b2d-183">toolearn 더 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e8b2d-183">toolearn more, see:</span></span>

* <span data-ttu-id="e8b2d-184">[HDInsight를 사용하여 비행 지연 데이터 분석][hdinsight-analyze-flight-data]</span><span class="sxs-lookup"><span data-stu-id="e8b2d-184">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]</span></span>
* <span data-ttu-id="e8b2d-185">[데이터 tooHDInsight 업로드][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="e8b2d-185">[Upload Data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="e8b2d-186">[HDInsight에서 Sqoop 사용][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="e8b2d-186">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-get-started]: hdinsight-hadoop-tutorial-get-started-windows.md

[hive-odbc-driver-download]: http://go.microsoft.com/fwlink/?LinkID=286698


