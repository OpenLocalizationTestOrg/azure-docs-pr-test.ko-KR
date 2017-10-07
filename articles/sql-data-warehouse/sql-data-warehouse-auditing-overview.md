---
title: "Azure SQL 데이터 웨어하우스에 aaaAuditing | Microsoft Docs"
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
ms.openlocfilehash: 948de74fa052ef206cf1aa65c0d81f084b18cb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="auditing-in-azure-sql-data-warehouse"></a><span data-ttu-id="871d7-103">Azure SQL 데이터 웨어하우스 감사</span><span class="sxs-lookup"><span data-stu-id="871d7-103">Auditing in Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="871d7-104">감사</span><span class="sxs-lookup"><span data-stu-id="871d7-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="871d7-105">위협 감지</span><span class="sxs-lookup"><span data-stu-id="871d7-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

<span data-ttu-id="871d7-106">SQL 데이터 웨어하우스 감사 이벤트를 허용 하면 toorecord Azure 저장소 계정에 데이터베이스 tooan 감사 로그에 합니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-106">SQL Data Warehouse auditing allows you toorecord events in your database tooan audit log in your Azure Storage account.</span></span> <span data-ttu-id="871d7-107">감사는 규정 준수를 유지 관리하고, 데이터베이스 작업을 이해하고, 비즈니스 문제나 의심스러운 보안 위반을 나타낼 수 있는 불일치 및 이상 활동을 파악하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-107">Auditing can help you maintain regulatory compliance, understand  database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span> <span data-ttu-id="871d7-108">또한 드릴다운 보고서 및 분석을 위해 SQL Data Warehouse 감사 기능을 Microsoft Power BI와 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-108">SQL Data Warehouse auditing also integrates with Microsoft Power BI for drill-down reporting and analysis.</span></span>

<span data-ttu-id="871d7-109">감사 도구를 사용 하도록 설정 되 고 toocompliance 표준 준수를 용이 하 게 있지만 규정 준수를 보장 하지는 마십시오.</span><span class="sxs-lookup"><span data-stu-id="871d7-109">Auditing tools enable and facilitate adherence toocompliance standards but don't guarantee compliance.</span></span> <span data-ttu-id="871d7-110">Azure에 대 한 자세한 내용은 해당 지원 표준 준수를 프로그램에서 참조 hello <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure 보안 센터</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-110">For more information about Azure programs that support standards compliance, see hello <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Trust Center</a>.</span></span>

* <span data-ttu-id="871d7-111">[데이터베이스 감사 기본 사항]</span><span class="sxs-lookup"><span data-stu-id="871d7-111">[Database Auditing basics]</span></span>
* <span data-ttu-id="871d7-112">[데이터베이스에 대한 감사 설정]</span><span class="sxs-lookup"><span data-stu-id="871d7-112">[Set up auditing for your database]</span></span>
* <span data-ttu-id="871d7-113">[감사 로그 및 보고서 분석]</span><span class="sxs-lookup"><span data-stu-id="871d7-113">[Analyze audit logs and reports]</span></span>

## <span data-ttu-id="871d7-114"><a id="subheading-1"></a>Azure SQL 데이터 웨어하우스 데이터베이스 감사 기본 사항</span><span class="sxs-lookup"><span data-stu-id="871d7-114"><a id="subheading-1"></a>Azure SQL Data Warehouse Database Auditing basics</span></span>
<span data-ttu-id="871d7-115">SQL 데이터 웨어하우스 데이터베이스 감사를 사용하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-115">SQL Data Warehouse database auditing allows you to:</span></span>

* <span data-ttu-id="871d7-116">**유지** 합니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-116">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="871d7-117">감사 데이터베이스 작업 toobe의 범주를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-117">You can define categories of database actions  toobe audited.</span></span>
* <span data-ttu-id="871d7-118">**보고** 합니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-118">**Report** on database activity.</span></span> <span data-ttu-id="871d7-119">미리 구성 된 보고서 및 활동 및 이벤트 보고 신속 하 게 시작 하는 대시보드 tooget를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-119">You can use preconfigured reports and a dashboard tooget started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="871d7-120">**분석** 합니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-120">**Analyze** reports.</span></span> <span data-ttu-id="871d7-121">의심스러운 이벤트, 특별한 활동 및 추세를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-121">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="871d7-122">이벤트 범주에 따라 hello에 대 한 감사를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-122">You can configure auditing for hello following event categories:</span></span>

<span data-ttu-id="871d7-123">**일반 SQL** 및 **매개 변수가 있는 SQL** 로 분류 되어 수집 된 감사 로그는 hello에 대 한</span><span class="sxs-lookup"><span data-stu-id="871d7-123">**Plain SQL** and **Parameterized SQL** for which hello collected audit logs are classified as</span></span>  

* <span data-ttu-id="871d7-124">**액세스 toodata**</span><span class="sxs-lookup"><span data-stu-id="871d7-124">**Access toodata**</span></span>
* <span data-ttu-id="871d7-125">**스키마 변경(DDL)**</span><span class="sxs-lookup"><span data-stu-id="871d7-125">**Schema changes (DDL)**</span></span>
* <span data-ttu-id="871d7-126">**데이터 변경(DML)**</span><span class="sxs-lookup"><span data-stu-id="871d7-126">**Data changes (DML)**</span></span>
* <span data-ttu-id="871d7-127">**계정, 역할 및 사용 권한(DCL)**</span><span class="sxs-lookup"><span data-stu-id="871d7-127">**Accounts, roles, and permissions (DCL)**</span></span>
* <span data-ttu-id="871d7-128">**저장 프로시저**, **로그인** 및 **트랜잭션 관리**.</span><span class="sxs-lookup"><span data-stu-id="871d7-128">**Stored Procedure**, **Login** and, **Transaction Management**.</span></span>

<span data-ttu-id="871d7-129">각 이벤트 범주에 대해 **성공** 및 **실패** 작업의 감사를 따로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-129">For each Event Category, Auditing of **Success** and **Failure** operations are configured separately.</span></span>

<span data-ttu-id="871d7-130">Hello 활동 및 감사 된 이벤트에 대 한 자세한 내용은 참조 hello <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">감사 로그 형식 참조 (doc 파일 다운로드)</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-130">For more information about hello activities and events audited, see hello <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">Audit Log Format Reference (doc file download)</a>.</span></span>

<span data-ttu-id="871d7-131">감사 로그는 Azure 저장소 계정에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-131">Audit logs are stored in your Azure storage account.</span></span> <span data-ttu-id="871d7-132">감사 로그의 보존 기간을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-132">You can define an audit log retention period.</span></span>

<span data-ttu-id="871d7-133">특정 데이터베이스에 대해 또는 기본 서버 정책으로 감사 정책을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-133">An auditing policy can be defined for a specific database or as a default server policy.</span></span> <span data-ttu-id="871d7-134">기본 서버 감사 정책에는 특정 재정의 데이터베이스 감사 정책을 정의 되어 있지 않은 서버에 tooall 데이터베이스 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-134">A default server auditing policy applies tooall databases on a server, which do not have a specific overriding database auditing policy defined.</span></span>

<span data-ttu-id="871d7-135">감사를 설정하기 전에 ["하위 클라이언트"](sql-data-warehouse-auditing-downlevel-clients.md)를 사용 중인지 여부를 점검합니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-135">Before setting up audit auditing check if you are using a ["Downlevel Client."](sql-data-warehouse-auditing-downlevel-clients.md)</span></span>

## <span data-ttu-id="871d7-136"><a id="subheading-2"></a>데이터베이스에 대한 감사 설정</span><span class="sxs-lookup"><span data-stu-id="871d7-136"><a id="subheading-2"></a>Set up auditing for your database</span></span>
1. <span data-ttu-id="871d7-137">Hello 시작 <a href="https://portal.azure.com" target="_blank">Azure 포털</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-137">Launch hello <a href="https://portal.azure.com" target="_blank">Azure portal</a>.</span></span>
2. <span data-ttu-id="871d7-138">Toohello 이동 **설정을** hello tooaudit 원하는 SQL 데이터 웨어하우스의 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-138">Go toohello **Settings** blade of hello SQL Data Warehouse you want tooaudit.</span></span> <span data-ttu-id="871d7-139">Hello에 **설정** 블레이드를 **감사 및 위협 검색**합니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-139">In hello **Settings** blade, select **Auditing & Threat detection**.</span></span>
   
    ![][1]
3. <span data-ttu-id="871d7-140">다음으로 hello를 클릭 하 여 감사를 활성화 **ON** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-140">Next, enable auditing by clicking hello **ON** button.</span></span>
   
    ![][3]
4. <span data-ttu-id="871d7-141">감사 구성 블레이드 hello, 선택 **저장소 세부 정보** tooopen hello 감사 로그 저장소 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-141">In hello auditing configuration blade, select **STORAGE DETAILS** tooopen hello Audit Logs Storage blade.</span></span> <span data-ttu-id="871d7-142">Hello 로그를 저장할 Azure 저장소 계정 및 hello 선택 보존 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-142">Select hello Azure storage account where logs will be saved and, hello retention period.</span></span> 
>[!TIP]
><span data-ttu-id="871d7-143">사용 하 여 hello hello 최대한 활용 하는 모든 감사 데이터베이스 tooget hello에 대 한 동일한 저장소 계정을 미리 구성 된 서식 파일을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-143">Use hello same storage account for all audited databases tooget hello most out of hello pre-configured reports templates.</span></span>
   
    ![][4]
5. <span data-ttu-id="871d7-144">Hello 클릭 **확인** 단추 toosave hello 저장소 세부 정보 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-144">Click hello **OK** button toosave hello storage details configuration.</span></span>
6. <span data-ttu-id="871d7-145">**이벤트를 로깅 하나씩**, 클릭 **성공** 및 **오류** toolog 모든 이벤트를 하거나 개별 이벤트 범주를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-145">Under **LOGGING BY EVENT**, click **SUCCESS** and **FAILURE** toolog all events, or choose individual event categories.</span></span>
7. <span data-ttu-id="871d7-146">데이터베이스에 대 한 감사를 구성 하는 경우에 데이터 감사 올바로 캡처 프로그램 클라이언트 tooensure의 tooalter hello 연결 문자열을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-146">If you are configuring Auditing for a database, you may need tooalter hello connection string of your client tooensure data auditing is correctly captured.</span></span> <span data-ttu-id="871d7-147">Hello 확인 [hello 연결 문자열에서 서버 FDQN 수정](sql-data-warehouse-auditing-downlevel-clients.md) 하위 수준 클라이언트 연결에 대 한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-147">Check hello [Modify Server FDQN in hello connection string](sql-data-warehouse-auditing-downlevel-clients.md) topic for downlevel client connections.</span></span>
8. <span data-ttu-id="871d7-148">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-148">Click **OK**.</span></span>

## <span data-ttu-id="871d7-149"><a id="subheading-3"></a>감사 로그 및 보고서 분석</span><span class="sxs-lookup"><span data-stu-id="871d7-149"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="871d7-150">감사 로그는 저장소 테이블 컬렉션에 집계 되는 **SQLDBAuditLogs** hello 설치 도중에 선택한 Azure 저장소 계정에에서는 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-150">Audit logs are aggregated in a collection of Store Tables with a **SQLDBAuditLogs** prefix in hello Azure storage account you chose during setup.</span></span> <span data-ttu-id="871d7-151"><a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure 저장소 탐색기</a>와 같은 도구를 사용하여 로그 파일을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-151">You can view log files using a tool such as <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure Storage Explorer</a>.</span></span>

<span data-ttu-id="871d7-152">미리 구성 된 대시보드 보고서 서식 파일은 사용할 수는 <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">Excel 스프레드시트를 다운로드할 수 있는</a> toohelp 로그 데이터를 신속 하 게 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-152">A preconfigured dashboard report template is available as a <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">downloadable Excel spreadsheet</a> toohelp you quickly analyze log data.</span></span> <span data-ttu-id="871d7-153">Excel 2013 이상 및 다운로드할 수 있는 파워 쿼리 필요한 감사 로그에 toouse hello 템플릿을 <a href="http://www.microsoft.com/download/details.aspx?id=39379">여기</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-153">toouse hello template on your audit logs, you need Excel 2013 or later and Power Query, which you can download <a href="http://www.microsoft.com/download/details.aspx?id=39379">here</a>.</span></span>

<span data-ttu-id="871d7-154">hello 서식 파일에는 가상의 예제 데이터, 및를 설정할 수 있습니다 파워 쿼리 tooimport 감사 로그 Azure 저장소 계정에서 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-154">hello template has fictional sample data in it, and you can set up Power Query tooimport your audit log directly from your Azure storage account.</span></span>

## <span data-ttu-id="871d7-155"><a id="subheading-4"></a>Storage 키 다시 생성</span><span class="sxs-lookup"><span data-stu-id="871d7-155"><a id="subheading-4"></a>Storage key regeneration</span></span>
<span data-ttu-id="871d7-156">프로덕션 환경에서 저장소 키를 주기적으로 가능성이 toorefresh 됩니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-156">In production, you are likely toorefresh your storage keys periodically.</span></span> <span data-ttu-id="871d7-157">키를 새로 고치거 나, toosave hello 정책이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-157">When refreshing your keys, you need toosave hello policy.</span></span> <span data-ttu-id="871d7-158">hello 프로세스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-158">hello process is as follows:</span></span>

1. <span data-ttu-id="871d7-159">위에서 설명한 감사 섹션 hello 설치 프로그램의 구성 블레이드에서 감사 hello에서 전환 hello **저장소 액세스 키** 에서 *기본* 너무*보조* 및  **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-159">In hello auditing configuration blade (described above in hello setup auditing section) switch hello **Storage Access Key** from *Primary* too*Secondary* and **SAVE**.</span></span>

   ![][4]
2. <span data-ttu-id="871d7-160">이동 toohello 저장소 구성 블레이드 및 **다시 생성** hello *기본 액세스 키*합니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-160">Go toohello storage configuration blade and **regenerate** hello *Primary Access Key*.</span></span>
3. <span data-ttu-id="871d7-161">감사 구성 블레이드, 스위치 hello toohello 돌아가서 **저장소 액세스 키** 에서 *보조* 너무*기본* 누릅니다 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-161">Go back toohello auditing configuration blade, switch hello **Storage Access Key** from *Secondary* too*Primary* and press **SAVE**.</span></span>
4. <span data-ttu-id="871d7-162">로 돌아가려면 toohello 저장소 UI 및 **다시 생성** hello *보조 액세스 키* (hello에 대 한 준비 과정으로 다음 키 새로 고침 주기 합니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-162">Go back toohello storage UI and **regenerate** hello *Secondary Access Key* (as preparation for hello next keys refresh cycle.</span></span>

## <span data-ttu-id="871d7-163"><a id="subheading-5"></a>Automation(PowerShell/REST API)</span><span class="sxs-lookup"><span data-stu-id="871d7-163"><a id="subheading-5"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="871d7-164">Hello 다음 자동화 도구를 사용 하 여 감사 Azure SQL 데이터 웨어하우스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="871d7-164">You can also configure auditing in Azure SQL Data Warehouse by using hello following automation tools:</span></span>

* <span data-ttu-id="871d7-165">**PowerShell cmdlet**:</span><span class="sxs-lookup"><span data-stu-id="871d7-165">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="871d7-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="871d7-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="871d7-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="871d7-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="871d7-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="871d7-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="871d7-169">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="871d7-169">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="871d7-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="871d7-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="871d7-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="871d7-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="871d7-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="871d7-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

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