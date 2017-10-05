---
title: "Azure SQL Data Warehouse 감사 | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스 감사 시작"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 0e6af148-b218-4b43-bb5f-907917d20330
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 08/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: f851c82ebeaa647f663d499a4d327c3479e36121
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="auditing-in-azure-sql-data-warehouse"></a><span data-ttu-id="50695-103">Azure SQL 데이터 웨어하우스 감사</span><span class="sxs-lookup"><span data-stu-id="50695-103">Auditing in Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="50695-104">감사</span><span class="sxs-lookup"><span data-stu-id="50695-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="50695-105">위협 감지</span><span class="sxs-lookup"><span data-stu-id="50695-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

<span data-ttu-id="50695-106">SQL Data Warehouse 감사를 사용하면 Azure Storage 계정의 감사 로그에 데이터베이스의 이벤트를 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50695-106">SQL Data Warehouse auditing allows you to record events in your database to an audit log in your Azure Storage account.</span></span> <span data-ttu-id="50695-107">감사는 규정 준수를 유지 관리하고, 데이터베이스 작업을 이해하고, 비즈니스 문제나 의심스러운 보안 위반을 나타낼 수 있는 불일치 및 이상 활동을 파악하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50695-107">Auditing can help you maintain regulatory compliance, understand  database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span> <span data-ttu-id="50695-108">또한 드릴다운 보고서 및 분석을 위해 SQL Data Warehouse 감사 기능을 Microsoft Power BI와 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="50695-108">SQL Data Warehouse auditing also integrates with Microsoft Power BI for drill-down reporting and analysis.</span></span>

<span data-ttu-id="50695-109">감사 도구를 사용하면 규정 준수 표준을 보다 쉽게 준수할 수 있지만 규정을 완전히 준수한다고 보장할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="50695-109">Auditing tools enable and facilitate adherence to compliance standards but don't guarantee compliance.</span></span> <span data-ttu-id="50695-110">표준 규정 준수를 지원하는 Azure 프로그램에 대한 자세한 내용은 <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure 보안 센터</a>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="50695-110">For more information about Azure programs that support standards compliance, see the <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Trust Center</a>.</span></span>

* <span data-ttu-id="50695-111">[데이터베이스 감사 기본 사항]</span><span class="sxs-lookup"><span data-stu-id="50695-111">[Database Auditing basics]</span></span>
* <span data-ttu-id="50695-112">[데이터베이스에 대한 감사 설정]</span><span class="sxs-lookup"><span data-stu-id="50695-112">[Set up auditing for your database]</span></span>
* <span data-ttu-id="50695-113">[감사 로그 및 보고서 분석]</span><span class="sxs-lookup"><span data-stu-id="50695-113">[Analyze audit logs and reports]</span></span>

## <span data-ttu-id="50695-114"><a id="subheading-1"></a>Azure SQL 데이터 웨어하우스 데이터베이스 감사 기본 사항</span><span class="sxs-lookup"><span data-stu-id="50695-114"><a id="subheading-1"></a>Azure SQL Data Warehouse Database Auditing basics</span></span>
<span data-ttu-id="50695-115">SQL 데이터 웨어하우스 데이터베이스 감사를 사용하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50695-115">SQL Data Warehouse database auditing allows you to:</span></span>

* <span data-ttu-id="50695-116">**유지** 합니다.</span><span class="sxs-lookup"><span data-stu-id="50695-116">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="50695-117">감사할 데이터베이스 동작의 범주를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50695-117">You can define categories of database actions  to be audited.</span></span>
* <span data-ttu-id="50695-118">**보고** 합니다.</span><span class="sxs-lookup"><span data-stu-id="50695-118">**Report** on database activity.</span></span> <span data-ttu-id="50695-119">미리 구성된 보고서 및 대시보드를 사용하여 활동 및 이벤트 보고를 빠르게 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50695-119">You can use preconfigured reports and a dashboard to get started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="50695-120">**분석** 합니다.</span><span class="sxs-lookup"><span data-stu-id="50695-120">**Analyze** reports.</span></span> <span data-ttu-id="50695-121">의심스러운 이벤트, 특별한 활동 및 추세를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50695-121">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="50695-122">다음 이벤트 범주에 대한 감사를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50695-122">You can configure auditing for the following event categories:</span></span>

<span data-ttu-id="50695-123">**일반 SQL** 및 수집된 감사 로그를 다음과 같이 분류하는 **매개 변수가 있는 SQL**</span><span class="sxs-lookup"><span data-stu-id="50695-123">**Plain SQL** and **Parameterized SQL** for which the collected audit logs are classified as</span></span>  

* <span data-ttu-id="50695-124">**데이터 액세스**</span><span class="sxs-lookup"><span data-stu-id="50695-124">**Access to data**</span></span>
* <span data-ttu-id="50695-125">**스키마 변경(DDL)**</span><span class="sxs-lookup"><span data-stu-id="50695-125">**Schema changes (DDL)**</span></span>
* <span data-ttu-id="50695-126">**데이터 변경(DML)**</span><span class="sxs-lookup"><span data-stu-id="50695-126">**Data changes (DML)**</span></span>
* <span data-ttu-id="50695-127">**계정, 역할 및 사용 권한(DCL)**</span><span class="sxs-lookup"><span data-stu-id="50695-127">**Accounts, roles, and permissions (DCL)**</span></span>
* <span data-ttu-id="50695-128">**저장 프로시저**, **로그인** 및 **트랜잭션 관리**.</span><span class="sxs-lookup"><span data-stu-id="50695-128">**Stored Procedure**, **Login** and, **Transaction Management**.</span></span>

<span data-ttu-id="50695-129">각 이벤트 범주에 대해 **성공** 및 **실패** 작업의 감사를 따로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="50695-129">For each Event Category, Auditing of **Success** and **Failure** operations are configured separately.</span></span>

<span data-ttu-id="50695-130">감사된 활동 및 이벤트에 대한 자세한 내용은 <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">감사 로그 형식 참조(doc 파일 다운로드)</a>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="50695-130">For more information about the activities and events audited, see the <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">Audit Log Format Reference (doc file download)</a>.</span></span>

<span data-ttu-id="50695-131">감사 로그는 Azure 저장소 계정에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="50695-131">Audit logs are stored in your Azure storage account.</span></span> <span data-ttu-id="50695-132">감사 로그의 보존 기간을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50695-132">You can define an audit log retention period.</span></span>

<span data-ttu-id="50695-133">특정 데이터베이스에 대해 또는 기본 서버 정책으로 감사 정책을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50695-133">An auditing policy can be defined for a specific database or as a default server policy.</span></span> <span data-ttu-id="50695-134">기본 서버 감사 정책은 특정 재정의 데이터베이스 감사 정책이 정의되지 않은 서버의 모든 데이터베이스에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="50695-134">A default server auditing policy applies to all databases on a server, which do not have a specific overriding database auditing policy defined.</span></span>

<span data-ttu-id="50695-135">감사를 설정하기 전에 ["하위 클라이언트"](sql-data-warehouse-auditing-downlevel-clients.md)를 사용 중인지 여부를 점검합니다.</span><span class="sxs-lookup"><span data-stu-id="50695-135">Before setting up audit auditing check if you are using a ["Downlevel Client."](sql-data-warehouse-auditing-downlevel-clients.md)</span></span>

## <span data-ttu-id="50695-136"><a id="subheading-2"></a>데이터베이스에 대한 감사 설정</span><span class="sxs-lookup"><span data-stu-id="50695-136"><a id="subheading-2"></a>Set up auditing for your database</span></span>
1. <span data-ttu-id="50695-137"><a href="https://portal.azure.com" target="_blank">Azure Portal</a>을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="50695-137">Launch the <a href="https://portal.azure.com" target="_blank">Azure portal</a>.</span></span>
2. <span data-ttu-id="50695-138">감사하려는 SQL Data Warehouse의 **설정** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="50695-138">Go to the **Settings** blade of the SQL Data Warehouse you want to audit.</span></span> <span data-ttu-id="50695-139">**설정** 블레이드에서 **감사 및 위협 감지**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="50695-139">In the **Settings** blade, select **Auditing & Threat detection**.</span></span>
   
    ![][1]
3. <span data-ttu-id="50695-140">다음으로 **켜기** 단추를 클릭하여 감사를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="50695-140">Next, enable auditing by clicking the **ON** button.</span></span>
   
    ![][3]
4. <span data-ttu-id="50695-141">감사 구성 블레이드에서 **저장소 정보**를 선택하여 감사 로그 저장소 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="50695-141">In the auditing configuration blade, select **STORAGE DETAILS** to open the Audit Logs Storage blade.</span></span> <span data-ttu-id="50695-142">로그를 저장할 Azure 저장소 계정 및 보존 기간을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="50695-142">Select the Azure storage account where logs will be saved and, the retention period.</span></span> 
>[!TIP]
><span data-ttu-id="50695-143">미리 구성된 보고서 템플릿을 활용하려면 감사되는 모든 데이터베이스에 대해 동일한 저장소 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="50695-143">Use the same storage account for all audited databases to get the most out of the pre-configured reports templates.</span></span>
   
    ![][4]
5. <span data-ttu-id="50695-144">**확인** 단추를 클릭하여 저장소 세부 정보 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="50695-144">Click the **OK** button to save the storage details configuration.</span></span>
6. <span data-ttu-id="50695-145">아래에서 **이벤트별 로깅** 아래에서 **성공** 및 **실패**를 클릭하여 모든 이벤트를 기록하거나 개별 이벤트 범주를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="50695-145">Under **LOGGING BY EVENT**, click **SUCCESS** and **FAILURE** to log all events, or choose individual event categories.</span></span>
7. <span data-ttu-id="50695-146">데이터베이스에 대한 감사를 구성하는 경우 클라이언트의 연결 문자열을 변경하여 데이터 감사가 바르게 캡처되는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="50695-146">If you are configuring Auditing for a database, you may need to alter the connection string of your client to ensure data auditing is correctly captured.</span></span> <span data-ttu-id="50695-147">[연결 문자열에서 서버 FDQN 수정](sql-data-warehouse-auditing-downlevel-clients.md) 항목에서 하위 클라이언트 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="50695-147">Check the [Modify Server FDQN in the connection string](sql-data-warehouse-auditing-downlevel-clients.md) topic for downlevel client connections.</span></span>
8. <span data-ttu-id="50695-148">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="50695-148">Click **OK**.</span></span>

## <span data-ttu-id="50695-149"><a id="subheading-3"></a>감사 로그 및 보고서 분석</span><span class="sxs-lookup"><span data-stu-id="50695-149"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="50695-150">감사 로그는 설치 중에 선택한 Azure 저장소 계정의 **SQLDBAuditLogs** 접두사가 포함된 저장소 테이블의 컬렉션에 집계됩니다.</span><span class="sxs-lookup"><span data-stu-id="50695-150">Audit logs are aggregated in a collection of Store Tables with a **SQLDBAuditLogs** prefix in the Azure storage account you chose during setup.</span></span> <span data-ttu-id="50695-151"><a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure 저장소 탐색기</a>와 같은 도구를 사용하여 로그 파일을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50695-151">You can view log files using a tool such as <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure Storage Explorer</a>.</span></span>

<span data-ttu-id="50695-152">미리 구성된 대시보드 보고서 템플릿은 로그 데이터를 빠르게 분석하는 데 도움이 되는 <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">다운로드 가능 Excel 스프레드시트</a>로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50695-152">A preconfigured dashboard report template is available as a <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">downloadable Excel spreadsheet</a> to help you quickly analyze log data.</span></span> <span data-ttu-id="50695-153">감사 로그에 템플릿을 사용하려면 Excel 2013 이상과 파워 쿼리가 필요하며 이러한 프로그램은 <a href="http://www.microsoft.com/download/details.aspx?id=39379">여기</a>서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50695-153">To use the template on your audit logs, you need Excel 2013 or later and Power Query, which you can download <a href="http://www.microsoft.com/download/details.aspx?id=39379">here</a>.</span></span>

<span data-ttu-id="50695-154">템플릿에는 가상의 샘플 데이터가 포함되어 있으며 Azure 저장소 계정에서 직접 감사 로그를 가져오도록 파워 쿼리를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50695-154">The template has fictional sample data in it, and you can set up Power Query to import your audit log directly from your Azure storage account.</span></span>

## <span data-ttu-id="50695-155"><a id="subheading-4"></a>Storage 키 다시 생성</span><span class="sxs-lookup"><span data-stu-id="50695-155"><a id="subheading-4"></a>Storage key regeneration</span></span>
<span data-ttu-id="50695-156">프로덕션에서는 저장소 키를 주기적으로 새로 고치게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50695-156">In production, you are likely to refresh your storage keys periodically.</span></span> <span data-ttu-id="50695-157">키를 새로 고칠 때 정책을 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="50695-157">When refreshing your keys, you need to save the policy.</span></span> <span data-ttu-id="50695-158">프로세스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="50695-158">The process is as follows:</span></span>

1. <span data-ttu-id="50695-159">감사 구성 블레이드(위에 나온 감사 설정 섹션의 설명 참조)에서 **Storage 액세스 키**를 *기본*에서 *보조*로 전환하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="50695-159">In the auditing configuration blade (described above in the setup auditing section) switch the **Storage Access Key** from *Primary* to *Secondary* and **SAVE**.</span></span>

   ![][4]
2. <span data-ttu-id="50695-160">스토리지 구성 블레이드로 이동하고 **기본 액세스 키** 를 *다시 생성*합니다.</span><span class="sxs-lookup"><span data-stu-id="50695-160">Go to the storage configuration blade and **regenerate** the *Primary Access Key*.</span></span>
3. <span data-ttu-id="50695-161">감사 구성 블레이드로 돌아가서 **저장소 액세스 키**를 *보조*에서 *기본*으로 전환하고 **저장**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="50695-161">Go back to the auditing configuration blade, switch the **Storage Access Key** from *Secondary* to *Primary* and press **SAVE**.</span></span>
4. <span data-ttu-id="50695-162">저장소 UI로 돌아와서 **보조 선택키** 를 *다시 생성* 합니다(다음 키 새로 고침 주기를 위한 준비).</span><span class="sxs-lookup"><span data-stu-id="50695-162">Go back to the storage UI and **regenerate** the *Secondary Access Key* (as preparation for the next keys refresh cycle.</span></span>

## <span data-ttu-id="50695-163"><a id="subheading-5"></a>Automation(PowerShell/REST API)</span><span class="sxs-lookup"><span data-stu-id="50695-163"><a id="subheading-5"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="50695-164">또한 다음 자동화 도구를 사용하여 Azure SQL Data Warehouse에서 감사를 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50695-164">You can also configure auditing in Azure SQL Data Warehouse by using the following automation tools:</span></span>

* <span data-ttu-id="50695-165">**PowerShell cmdlet**:</span><span class="sxs-lookup"><span data-stu-id="50695-165">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="50695-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="50695-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="50695-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="50695-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="50695-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="50695-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="50695-169">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="50695-169">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="50695-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="50695-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="50695-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="50695-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="50695-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="50695-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

<!--Anchors-->
[데이터베이스 감사 기본 사항]: #subheading-1
[데이터베이스에 대한 감사 설정]: #subheading-2
[감사 로그 및 보고서 분석]: #subheading-3


<!--Image references-->
[1]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing.png
[2]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-inherit.png
[3]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-enable.png
[4]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-storage-account.png
[5]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-dashboard.png


<!--Link references-->
[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy