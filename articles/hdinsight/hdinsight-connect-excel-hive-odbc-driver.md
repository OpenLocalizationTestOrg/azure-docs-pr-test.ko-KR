---
title: "Hive ODBC 드라이버로 Hadoop에 Excel 연결 - Azure HDInsight | Microsoft Docs"
description: "Excel용 Microsoft Hive ODBC 드라이버를 설정하고 Microsoft Excel의 HDInsight 클러스터에서 데이터를 쿼리하는 데 사용하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 7818093e42c34ee671a035cde783a6622fb2a798
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-excel-to-hadoop-in-azure-hdinsight-with-the-microsoft-hive-odbc-driver"></a><span data-ttu-id="b4753-104">Microsoft Hive ODBC 드라이버로 Azure HDInsight의 Hadoop에 Excel 연결</span><span class="sxs-lookup"><span data-stu-id="b4753-104">Connect Excel to Hadoop in Azure HDInsight with the Microsoft Hive ODBC driver</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="b4753-105">Microsoft의 빅 데이터 솔루션은 Microsoft BI(비즈니스 인텔리전스) 구성 요소를 Azure HDInsight가 배포한 Apache Hadoop 클러스터와 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-105">Microsoft's Big Data solution integrates Microsoft Business Intelligence (BI) components with Apache Hadoop clusters that have been deployed by the Azure HDInsight.</span></span> <span data-ttu-id="b4753-106">이 통합의 예로 Microsoft Hive ODBC(Open Database Connectivity) 드라이버를 사용하여 HDInsight Hadoop 클러스터의 Hive 데이터 웨어하우스에 Excel을 연결하는 기능을 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-106">An example of this integration is the ability to connect Excel to the Hive data warehouse of a Hadoop cluster in HDInsight using the Microsoft Hive Open Database Connectivity (ODBC) Driver.</span></span>

<span data-ttu-id="b4753-107">Excel에서 Microsoft Excel용 파워 쿼리 추가 기능을 사용하여 HDInsight 클러스터 및 기타 데이터 원본(예: 기타(비 HDInsight) Hadoop 클러스터)과 연결된 데이터를 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-107">It is also possible to connect the data associated with an HDInsight cluster and other data sources, including other (non-HDInsight) Hadoop clusters, from Excel using the Microsoft Power Query add-in for Excel.</span></span> <span data-ttu-id="b4753-108">파워 쿼리 설치 및 사용에 대한 자세한 내용은 [HDInsight에 파워 쿼리로 Excel 연결][hdinsight-power-query]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4753-108">For information on installing and using Power Query, see [Connect Excel to HDInsight with Power Query][hdinsight-power-query].</span></span>

> [!NOTE]
> <span data-ttu-id="b4753-109">이 문서의 단계는 Linux 또는 Windows 기반 HDInsight 클러스터와 함께 사용할 수 있지만, Windows는 클라이언트 워크스테이션에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-109">While the steps in this article can be used with either a Linux or Windows-based HDInsight cluster, Windows is required for the client workstation.</span></span>
> 
> 

<span data-ttu-id="b4753-110">**필수 조건**:</span><span class="sxs-lookup"><span data-stu-id="b4753-110">**Prerequisites**:</span></span>

<span data-ttu-id="b4753-111">이 문서를 시작하기 전에 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-111">Before you begin this article, you must have the following items:</span></span>

* <span data-ttu-id="b4753-112">**HDInsight 클러스터**.</span><span class="sxs-lookup"><span data-stu-id="b4753-112">**An HDInsight cluster**.</span></span> <span data-ttu-id="b4753-113">만들려면 [Azure HDInsight 시작][hdinsight-get-started]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4753-113">To create one, see [Get started with Azure HDInsight][hdinsight-get-started].</span></span>
* <span data-ttu-id="b4753-114">**워크스테이션** </span><span class="sxs-lookup"><span data-stu-id="b4753-114">**A workstation** with Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="install-microsoft-hive-odbc-driver"></a><span data-ttu-id="b4753-115">Microsoft Hive ODBC 드라이버 설치</span><span class="sxs-lookup"><span data-stu-id="b4753-115">Install Microsoft Hive ODBC driver</span></span>
<span data-ttu-id="b4753-116">[다운로드 센터][hive-odbc-driver-download]에서 Microsoft Hive ODBC 드라이버를 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-116">Download and install Microsoft Hive ODBC Driver from the [Download Center][hive-odbc-driver-download].</span></span>

<span data-ttu-id="b4753-117">이 드라이버는 32비트 또는 64비트 버전의 Windows 7, Windows 8, Windows 10, Windows Server 2008 R2 및 Windows Server 2012에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-117">This driver can be installed on 32-bit or 64-bit versions of Windows 7, Windows 8, Windows 10, Windows Server 2008 R2, and Windows Server 2012.</span></span> <span data-ttu-id="b4753-118">드라이버는 Azure HDInsight(버전 1.6 이상) 및 Azure HDInsight Emulator(v.1.0.0.0 이상)에 대한 연결을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-118">The driver allows connection to Azure HDInsight (version 1.6 and later) and Azure HDInsight Emulator (v.1.0.0.0 and later).</span></span> <span data-ttu-id="b4753-119">ODBC 드라이버를 사용하는 응용 프로그램 버전에 맞는 버전을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-119">You shall install the version that matches the version of the application where you use the ODBC driver.</span></span> <span data-ttu-id="b4753-120">이 자습서에서는 Office Excel에서 드라이버를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-120">For this tutorial, the driver is used from Office Excel.</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="b4753-121">Hive ODBC 데이터 원본 만들기</span><span class="sxs-lookup"><span data-stu-id="b4753-121">Create Hive ODBC data source</span></span>
<span data-ttu-id="b4753-122">다음 단계에 따라 Hive ODBC 데이터 원본을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-122">The following steps show you how to create a Hive ODBC Data Source.</span></span>

1. <span data-ttu-id="b4753-123">Windows 8 또는 Windows 10에서 Windows 키를 눌러 시작 화면을 연 후 **data sources**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-123">From Windows 8 or Windows 10, press the Windows key to open the Start screen, and then type **data sources**.</span></span>
2. <span data-ttu-id="b4753-124">Office 버전에 따라 **ODBC 데이터 원본 설정(32비트)** 또는 **ODBC 데이터 원본 설정(64비트)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-124">Click **Set up ODBC Data sources (32-bit)** or **Set up ODBC Data Sources (64-bit)** depending on your Office version.</span></span> <span data-ttu-id="b4753-125">Windows 7을 사용하는 경우 **관리 도구**에서 **ODBC 데이터 원본(32비트)** 또는 **ODBC 데이터 원본(64비트)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-125">If you are using Windows 7, choose **ODBC Data Sources (32 bit)** or **ODBC Data Sources (64 bit)** from **Administrative Tools**.</span></span> <span data-ttu-id="b4753-126">**ODBC 데이터 원본 관리자** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-126">You shall see the **ODBC Data Source Administrator** dialog.</span></span>
   
    <span data-ttu-id="b4753-127">![OBDC 데이터 원본 관리자](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "ODBC 데이터 원본 관리자를 사용하여 DSN 구성")</span><span class="sxs-lookup"><span data-stu-id="b4753-127">![OBDC data source administrator](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "Configure a DSN using ODBC Data Source Administrator")</span></span>

3. <span data-ttu-id="b4753-128">사용자 DNS에서 **추가**를 클릭하여 **새 데이터 원본 만들기** 마법사를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-128">From User DNS, click **Add** to open the **Create New Data Source** wizard.</span></span>
4. <span data-ttu-id="b4753-129">**Microsoft Hive ODBC 드라이버**를 선택한 후 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-129">Select **Microsoft Hive ODBC Driver**, and then click **Finish**.</span></span> <span data-ttu-id="b4753-130">**Microsoft Hive ODBC Driver DNS Setup** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-130">You shall see the **Microsoft Hive ODBC Driver DNS Setup** dialog.</span></span>
5. <span data-ttu-id="b4753-131">다음 값을 입력하거나 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-131">Type or select the following values:</span></span>
   
   | <span data-ttu-id="b4753-132">속성</span><span class="sxs-lookup"><span data-stu-id="b4753-132">Property</span></span> | <span data-ttu-id="b4753-133">설명</span><span class="sxs-lookup"><span data-stu-id="b4753-133">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="b4753-134">데이터 원본 이름</span><span class="sxs-lookup"><span data-stu-id="b4753-134">Data Source Name</span></span> |<span data-ttu-id="b4753-135">데이터 원본에 이름 지정</span><span class="sxs-lookup"><span data-stu-id="b4753-135">Give a name to your data source</span></span> |
   |  <span data-ttu-id="b4753-136">호스트</span><span class="sxs-lookup"><span data-stu-id="b4753-136">Host</span></span> |<span data-ttu-id="b4753-137">&lt;HDInsightClusterName>.azurehdinsight.net을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-137">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="b4753-138">예를 들면 myHDICluster.azurehdinsight.net과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-138">For example, myHDICluster.azurehdinsight.net</span></span> |
   |  <span data-ttu-id="b4753-139">포트</span><span class="sxs-lookup"><span data-stu-id="b4753-139">Port</span></span> |<span data-ttu-id="b4753-140"><strong>443</strong>을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-140">Use <strong>443</strong>.</span></span> <span data-ttu-id="b4753-141">(이 포트는 563에서 443으로 변경됨)</span><span class="sxs-lookup"><span data-stu-id="b4753-141">(This port has been changed from 563 to 443.)</span></span> |
   |  <span data-ttu-id="b4753-142">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="b4753-142">Database</span></span> |<span data-ttu-id="b4753-143"><strong>기본값</strong>을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-143">Use <strong>Default</strong>.</span></span> |
   |  <span data-ttu-id="b4753-144">메커니즘</span><span class="sxs-lookup"><span data-stu-id="b4753-144">Mechanism</span></span> |<span data-ttu-id="b4753-145"><strong>Azure HDInsight Service</strong> 선택</span><span class="sxs-lookup"><span data-stu-id="b4753-145">Select <strong>Azure HDInsight Service</strong></span></span> |
   |  <span data-ttu-id="b4753-146">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="b4753-146">User Name</span></span> |<span data-ttu-id="b4753-147">HDInsight 클러스터 HTTP 사용자의 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-147">Enter HDInsight cluster HTTP user username.</span></span> <span data-ttu-id="b4753-148">기본 사용자 이름은 <strong>admin</strong>입니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-148">The default username is <strong>admin</strong>.</span></span> |
   |  <span data-ttu-id="b4753-149">암호</span><span class="sxs-lookup"><span data-stu-id="b4753-149">Password</span></span> |<span data-ttu-id="b4753-150">HDInsight 클러스터 사용자 암호 입력</span><span class="sxs-lookup"><span data-stu-id="b4753-150">Enter HDInsight cluster user password.</span></span> |
   
    </table>
   
    <span data-ttu-id="b4753-151">**고급 옵션**을 클릭할 때 알아야 할 중요한 매개 변수가 몇 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-151">There are some important parameters to be aware of when you click **Advanced Options**:</span></span>
   
   | <span data-ttu-id="b4753-152">매개 변수</span><span class="sxs-lookup"><span data-stu-id="b4753-152">Parameter</span></span> | <span data-ttu-id="b4753-153">설명</span><span class="sxs-lookup"><span data-stu-id="b4753-153">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="b4753-154">Use Native Query</span><span class="sxs-lookup"><span data-stu-id="b4753-154">Use Native Query</span></span> |<span data-ttu-id="b4753-155">선택하면 ODBC 드라이버가 TSQL을 HiveQL로 변환하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-155">When it is selected, the ODBC driver does NOT try to convert TSQL into HiveQL.</span></span> <span data-ttu-id="b4753-156">순수 HiveQL 문을 제출하는 것이 확실한 경우에만 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-156">You shall use it only if you are 100% sure you are submitting pure HiveQL statements.</span></span> <span data-ttu-id="b4753-157">SQL Server 또는 Azure SQL 데이터베이스에 연결하는 경우에는 이 옵션을 선택 취소한 상태로 둬야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-157">When connecting to SQL Server or Azure SQL Database, you should leave it unchecked.</span></span> |
   |  <span data-ttu-id="b4753-158">Rows fetched per block</span><span class="sxs-lookup"><span data-stu-id="b4753-158">Rows fetched per block</span></span> |<span data-ttu-id="b4753-159">많은 수의 레코드를 가져오는 경우 최적의 성능을 위해 이 매개 변수를 조정해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-159">When fetching a large number of records, tuning this parameter may be required to ensure optimal performances.</span></span> |
   |  <span data-ttu-id="b4753-160">Default string column length, Binary column length, Decimal column scale</span><span class="sxs-lookup"><span data-stu-id="b4753-160">Default string column length, Binary column length, Decimal column scale</span></span> |<span data-ttu-id="b4753-161">데이터 형식 길이 및 정밀도는 데이터가 반환되는 방식에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-161">The data type lengths and precisions may affect how data is returned.</span></span> <span data-ttu-id="b4753-162">정밀도 손실 및/또는 잘림으로 인해 잘못된 정보가 반환될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-162">They cause incorrect information to be returned due to loss of precision and/or truncation.</span></span> |

    <span data-ttu-id="b4753-163">![고급 옵션](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "고급 DSN 구성 옵션")</span><span class="sxs-lookup"><span data-stu-id="b4753-163">![Advanced options](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "Advanced DSN configuration options")</span></span>

1. <span data-ttu-id="b4753-164">**테스트** 를 클릭하여 데이터 원본을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-164">Click **Test** to test the data source.</span></span> <span data-ttu-id="b4753-165">원본이 올바르게 구성된 경우 *테스트를 성공적으로 완료했습니다.*가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-165">When the data source is configured correctly, it shows *TESTS COMPLETED SUCCESSFULLY!*.</span></span>
2. <span data-ttu-id="b4753-166">**확인** 을 클릭하여 테스트 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-166">Click **OK** to close the Test dialog.</span></span> <span data-ttu-id="b4753-167">새 데이터 원본이 **ODBC 데이터 원본 관리자**에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-167">The new data source shall be listed on the **ODBC Data Source Administrator**.</span></span>
3. <span data-ttu-id="b4753-168">**확인** 을 클릭하여 마법사를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-168">Click **OK** to exit the wizard.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="b4753-169">HDInsight에서 Excel로 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="b4753-169">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="b4753-170">다음 단계는 이전 섹션에서 만든 ODBC 데이터 원본을 사용하여 Hive 테이블에서 Excel 통합 문서로 데이터를 가져오는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-170">The following steps describe the way to import data from a Hive table into an Excel workbook using the ODBC data source that you created in the previous section.</span></span>

1. <span data-ttu-id="b4753-171">Excel에서 새 통합 문서나 기존 통합 문서를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-171">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="b4753-172">**데이터** 탭에서 **데이터 가져오기**를 클릭한 다음 **다른 데이터 원본에서**를 클릭하고 **ODBC에서**를 클릭하여 **데이터 연결 마법사**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-172">From the **Data** tab, click **Get Data**, click **From Other Sources**, and then click **From ODBC** to launch the **Data Connection Wizard**.</span></span>
   
    <span data-ttu-id="b4753-173">![데이터 연결 마법사 열기](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "데이터 연결 마법사 열기")</span><span class="sxs-lookup"><span data-stu-id="b4753-173">![Open data connection wizard](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "Open data connection wizard")</span></span>
4. <span data-ttu-id="b4753-174">마지막 섹션에서 만든 데이터 원본 이름을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-174">Select the data source name that you created in the last section, and then click **OK**.</span></span>
5. <span data-ttu-id="b4753-175">Hadoop 사용자 이름(기본 이름은 admin) 및 암호를 입력한 다음 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-175">Enter Hadoop user name (the default name is admin) and the password, and then click **Connect**.</span></span>
6. <span data-ttu-id="b4753-176">탐색 창에서 **HIVE**를 확장하고 **default**를 확장한 후 **hivesampletable**을 클릭하고 **로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-176">On Navigator, expand **HIVE**, expand **default**, click **hivesampletable**, and then click **Load**.</span></span> <span data-ttu-id="b4753-177">데이터를 Excel로 가져올 때까지 몇 초 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-177">It takes a few seconds before data gets imported to Excel.</span></span>

    <span data-ttu-id="b4753-178">![HDInsight Hive ODBC 탐색기](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "데이터 연결 열기 마법사")</span><span class="sxs-lookup"><span data-stu-id="b4753-178">![HDInsight Hive ODBC navigator](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "Open data connection wizard")</span></span>


## <a name="next-steps"></a><span data-ttu-id="b4753-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b4753-179">Next steps</span></span>
<span data-ttu-id="b4753-180">이 문서에서는 Microsoft Hive ODBC 드라이버를 사용하여 HDInsight Service에서 Excel로 데이터를 가져오는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-180">In this article, you learned how to use the Microsoft Hive ODBC driver to retrieve data from the HDInsight Service into Excel.</span></span> <span data-ttu-id="b4753-181">마찬가지로 HDInsight Service에서 SQL 데이터베이스로 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-181">Similarly, you can retrieve data from the HDInsight Service into SQL Database.</span></span> <span data-ttu-id="b4753-182">데이터를 HDInsight Service에 업로드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4753-182">It is also possible to upload data into an HDInsight Service.</span></span> <span data-ttu-id="b4753-183">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4753-183">To learn more, see:</span></span>

* <span data-ttu-id="b4753-184">[HDInsight를 사용하여 비행 지연 데이터 분석][hdinsight-analyze-flight-data]</span><span class="sxs-lookup"><span data-stu-id="b4753-184">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]</span></span>
* <span data-ttu-id="b4753-185">[HDInsight에 데이터 업로드][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="b4753-185">[Upload Data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="b4753-186">[HDInsight에서 Sqoop 사용][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="b4753-186">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-get-started]: hdinsight-hadoop-tutorial-get-started-windows.md

[hive-odbc-driver-download]: http://go.microsoft.com/fwlink/?LinkID=286698


