---
title: "Azure SQL 데이터베이스 감사 시작 aaaGet | Microsoft Docs"
description: "Azure SQL Database 감사 시작"
services: sql-database
documentationcenter: 
author: giladm
manager: jhubbard
editor: giladm
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: giladm
ms.openlocfilehash: 5494c602d702ac41992520f900c393a98cc7c989
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-auditing"></a><span data-ttu-id="a0782-103">SQL 데이터베이스 감사 시작</span><span class="sxs-lookup"><span data-stu-id="a0782-103">Get started with SQL database auditing</span></span>
<span data-ttu-id="a0782-104">Azure SQL 데이터베이스 감사 데이터베이스 이벤트를 추적 하 고 Azure 저장소 계정에 tooan 감사 로그를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-104">Azure SQL database auditing tracks database events and writes them tooan audit log in your Azure storage account.</span></span> <span data-ttu-id="a0782-105">또한</span><span class="sxs-lookup"><span data-stu-id="a0782-105">Auditing also:</span></span>

* <span data-ttu-id="a0782-106">감사는 규정 준수를 유지 관리하고, 데이터베이스 작업을 이해하고, 비즈니스 문제나 의심스러운 보안 위반을 나타낼 수 있는 불일치 및 이상 활동을 파악하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-106">Helps you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

* <span data-ttu-id="a0782-107">사용 하도록 설정 하 고 규정 준수를 보장 하지 않습니다는 않지만 준수 toocompliance 표준을 촉진 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-107">Enables and facilitates adherence toocompliance standards, although it doesn't guarantee compliance.</span></span> <span data-ttu-id="a0782-108">Azure에 대 한 자세한 내용은 해당 지원 표준 준수를 프로그램에서 참조 hello [Azure 보안 센터](https://azure.microsoft.com/support/trust-center/compliance/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-108">For more information about Azure programs that support standards compliance, see hello [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).</span></span>


## <span data-ttu-id="a0782-109"><a id="subheading-1"></a>Azure SQL Database 감사 개요</span><span class="sxs-lookup"><span data-stu-id="a0782-109"><a id="subheading-1"></a>Azure SQL database auditing overview</span></span>
<span data-ttu-id="a0782-110">SQL Database 감사를 사용하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-110">You can use SQL database auditing to:</span></span>


* <span data-ttu-id="a0782-111">**유지** 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-111">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="a0782-112">감사 데이터베이스 작업 toobe의 범주를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-112">You can define categories of database actions toobe audited.</span></span>
* <span data-ttu-id="a0782-113">**보고** 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-113">**Report** on database activity.</span></span> <span data-ttu-id="a0782-114">미리 구성 된 보고서 및 활동 및 이벤트 보고 신속 하 게 시작 하는 대시보드 tooget를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-114">You can use preconfigured reports and a dashboard tooget started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="a0782-115">**분석** 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-115">**Analyze** reports.</span></span> <span data-ttu-id="a0782-116">의심스러운 이벤트, 특별한 활동 및 추세를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-116">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="a0782-117">Hello에 설명 된 대로 다양 한 유형의 이벤트 범주에 대 한 감사를 구성할 수 [데이터베이스에 대 한 감사를 설정](#subheading-2) 섹션.</span><span class="sxs-lookup"><span data-stu-id="a0782-117">You can configure auditing for different types of event categories, as explained in hello [Set up auditing for your database](#subheading-2) section.</span></span>

<span data-ttu-id="a0782-118">감사 로그는 Azure 구독에서 tooAzure Blob 저장소를 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-118">Audit logs are written tooAzure Blob storage on your Azure subscription.</span></span>


## <span data-ttu-id="a0782-119"><a id="subheading-8"></a>서버 수준 및 데이터베이스 수준 감사 정책 정의</span><span class="sxs-lookup"><span data-stu-id="a0782-119"><a id="subheading-8"></a>Define server-level vs. database-level auditing policy</span></span>

<span data-ttu-id="a0782-120">특정 데이터베이스에 대해 또는 기본 서버 정책으로 감사 정책을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-120">An auditing policy can be defined for a specific database or as a default server policy:</span></span>

* <span data-ttu-id="a0782-121">서버 정책 tooall 기존 및 새로 만든된 데이터베이스 hello 서버에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-121">A server policy applies tooall existing and newly created databases on hello server.</span></span>

* <span data-ttu-id="a0782-122">경우 *서버 blob 감사를 사용할 수*, 것 *toohello 데이터베이스를 항상 적용* (즉, hello 데이터베이스는 감사) hello 데이터베이스에 관계 없이 감사 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-122">If *server blob auditing is enabled*, it *always applies toohello database* (that is, hello database will be audited), regardless of hello database auditing settings.</span></span>

* <span data-ttu-id="a0782-123">Blob에 대 한 감사 hello 데이터베이스 추가 tooenabling에 것 hello 서버에서 사용 하도록 설정 됩니다 *하지* 재정의 하거나 hello 서버 blob 감사 hello 설정을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-123">Enabling blob auditing on hello database, in addition tooenabling it on hello server, will *not* override or change any of hello settings of hello server blob auditing.</span></span> <span data-ttu-id="a0782-124">두 감사는 함께 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-124">Both audits will exist side by side.</span></span> <span data-ttu-id="a0782-125">즉, hello 데이터베이스 (hello 서버 정책에서 한 번 및 한 번 hello 데이터베이스 정책에 의해) 동시에 두 번 감사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-125">In other words, hello database will be audited twice in parallel (once by hello server policy and once by hello database policy).</span></span>

   > [!NOTE]
   > <span data-ttu-id="a0782-126">다음과 같은 경우가 아니면 서버 Blob 감사 및 데이터베이스 Blob 감사를 함께 활성화하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-126">You should avoid enabling both server blob auditing and database blob auditing together, unless:</span></span>
    > * <span data-ttu-id="a0782-127">다른 toouse 원하는 *저장소 계정* 또는 *보존 기간* 특정 데이터베이스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-127">You want toouse a different *storage account* or *retention period* for a specific database.</span></span>
    > * <span data-ttu-id="a0782-128">Tooaudit 이벤트 또는 형식 범주에 대해 원하는 이벤트 형식에서 다른 특정 데이터베이스 또는 hello hello 서버에 있는 데이터베이스의 hello 나머지 부분에 대 한 감사가 수행 되는 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-128">You want tooaudit event types or categories for a specific database that differ from event types or categories that are being audited for hello rest of hello databases on hello server.</span></span> <span data-ttu-id="a0782-129">예를 들어 특정 데이터베이스에 대해서만 감사 toobe 해야 하는 테이블 삽입을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-129">For example, you might have table inserts that need toobe audited only for a specific database.</span></span>
   > 
   > <span data-ttu-id="a0782-130">그렇지 않은 경우 blob만 서버 수준 감사 및 leave hello 데이터베이스 수준 감사는 모든 데이터베이스에 대 한 비활성화를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-130">Otherwise, we recommended that you enable only server-level blob auditing and leave hello database-level auditing disabled for all databases.</span></span>


## <span data-ttu-id="a0782-131"><a id="subheading-2"></a>데이터베이스에 대한 감사 설정</span><span class="sxs-lookup"><span data-stu-id="a0782-131"><a id="subheading-2"></a>Set up auditing for your database</span></span>
<span data-ttu-id="a0782-132">hello 다음 섹션에서는 hello Azure 포털을 사용 하 여 감사의 hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-132">hello following section describes hello configuration of auditing using hello Azure portal.</span></span>

1. <span data-ttu-id="a0782-133">Toohello 이동 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-133">Go toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a0782-134">Toohello 이동 **설정을** hello tooaudit 원하는 SQL 데이터베이스/SQL server의 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-134">Go toohello **Settings** blade of hello SQL database/SQL server you want tooaudit.</span></span> <span data-ttu-id="a0782-135">Hello에 **설정** 블레이드를 **감사 및 위협 검색**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-135">In hello **Settings** blade, select **Auditing & Threat detection**.</span></span>

    <span data-ttu-id="a0782-136"><a id="auditing-screenshot"></a> ![탐색 창][1]</span><span class="sxs-lookup"><span data-stu-id="a0782-136"><a id="auditing-screenshot"></a> ![Navigation pane][1]</span></span>
3. <span data-ttu-id="a0782-137">Hello tooset는 서버 감사 정책 (tooall 기존 및 새로 만든된 데이터베이스는이 서버에 적용 됩니다)를 원하는 경우 선택할 수 있습니다 **서버 설정을 보려면** hello 데이터베이스 감사 블레이드에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-137">If you prefer tooset up a server auditing policy (which will apply tooall existing and newly created databases on this server), you can select hello **View server settings** link in hello database auditing blade.</span></span> <span data-ttu-id="a0782-138">보거나 수 있습니다 다음 hello 서버에 대 한 감사 설정을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-138">You can then view or modify hello server auditing settings.</span></span>

    ![탐색 창][2]
4. <span data-ttu-id="a0782-140">에 대 한 hello 데이터베이스 수준 (더하기 tooor 서버 수준 감사 하는 대신)에 대 한 감사 tooenable blob을 선호 하는 경우 **감사**선택, **ON**, 및에 대 한 **형식 감사** 를 선택 **Blob**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-140">If you prefer tooenable blob auditing on hello database level (in addition tooor instead of server-level auditing), for **Auditing**, select **ON**, and for **Auditing type**, select  **Blob**.</span></span>

    <span data-ttu-id="a0782-141">서버 blob 감사를 사용 하는 경우 hello 구성 된 데이터베이스 감사 hello 서버 blob 감사와 함께 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-141">If server blob auditing is enabled, hello database-configured audit will exist side by side with hello server blob audit.</span></span>  

    ![탐색 창][3]
5. <span data-ttu-id="a0782-143">tooopen hello **감사 로그 저장소** 블레이드를 **저장소 세부 정보**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-143">tooopen hello **Audit Logs Storage** blade, select **Storage Details**.</span></span> <span data-ttu-id="a0782-144">Hello Azure 저장소 계정에 로그를 저장할 선택한 후 삭제 이전 로그는 hello 후 hello 보존 기간을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-144">Select hello Azure storage account where logs will be saved, and then select hello retention period, after which hello old logs will be deleted.</span></span> <span data-ttu-id="a0782-145">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-145">Then click **OK**.</span></span> 
   >[!TIP] 
   ><span data-ttu-id="a0782-146">hello 감사 보고서 템플릿 사용 하 여 최대한 활용 tooget hello hello 감사 된 모든 데이터베이스에 대해 동일한 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-146">tooget hello most out of hello auditing reports templates, use hello same storage account for all audited databases.</span></span> 

    <span data-ttu-id="a0782-147"><a id="storage-screenshot"></a> ![탐색 창][4]</span><span class="sxs-lookup"><span data-stu-id="a0782-147"><a id="storage-screenshot"></a> ![Navigation pane][4]</span></span>
6. <span data-ttu-id="a0782-148">Toocustomize hello 감사 이벤트를 하려는 경우 PowerShell을 통해이 작업을 수행 하거나 REST API hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-148">If you want toocustomize hello audited events, you can do this via PowerShell or hello REST API.</span></span> <span data-ttu-id="a0782-149">자세한 내용은 참조 hello [자동화 (PowerShell/REST API)](#subheading-7) 섹션.</span><span class="sxs-lookup"><span data-stu-id="a0782-149">For more details, see hello [Automation (PowerShell/REST API)](#subheading-7) section.</span></span>
7. <span data-ttu-id="a0782-150">감사 설정을 구성 하 고 나면 hello 새로운 위협 검색 기능 설정 및 전자 메일 tooreceive 보안 경고를 구성 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-150">After you've configured your auditing settings, you can turn on hello new threat detection feature and configure emails tooreceive security alerts.</span></span> <span data-ttu-id="a0782-151">위협 감지를 사용하면 잠재적인 보안 위협을 나타낼 수 있는 비정상적인 데이터베이스 활동에 대해 사전 경고를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-151">When you use threat detection, you receive proactive alerts on anomalous database activities that can indicate potential security threats.</span></span> <span data-ttu-id="a0782-152">자세한 내용은 [위협 감지 시작](sql-database-threat-detection-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0782-152">For more details, see [Getting started with threat detection](sql-database-threat-detection-get-started.md).</span></span>
8. <span data-ttu-id="a0782-153">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-153">Click **Save**.</span></span>





## <span data-ttu-id="a0782-154"><a id="subheading-3"></a>감사 로그 및 보고서 분석</span><span class="sxs-lookup"><span data-stu-id="a0782-154"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="a0782-155">감사 로그는 hello 설치 도중에 선택한 Azure 저장소 계정에서에서 집계 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-155">Audit logs are aggregated in hello Azure storage account you chose during setup.</span></span> <span data-ttu-id="a0782-156">[Azure Storage 탐색기](http://storageexplorer.com/) 등의 도구를 사용하여 감사 로그를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-156">You can explore audit logs by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="a0782-157">Blob 감사 로그는 **sqldbauditlogs**라는 컨테이너 내부에 Blob 파일 컬렉션으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-157">Blob auditing logs are saved as a collection of blob files within a container named **sqldbauditlogs**.</span></span>

<span data-ttu-id="a0782-158">Hello 계층 hello blob 감사 로그 저장소 폴더, blob 명명 규칙 및 로그 형식에 대 한 자세한 내용은 참조 hello [Blob 감사 로그 형식 참조 (.docx 파일 다운로드)](https://go.microsoft.com/fwlink/?linkid=829599)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-158">For further details about hello hierarchy of hello blob audit logs storage folder, blob naming conventions, and log format, see hello [Blob Audit Log Format Reference (.docx file download)](https://go.microsoft.com/fwlink/?linkid=829599).</span></span>

<span data-ttu-id="a0782-159">몇 가지가 tooview blob 감사 로그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-159">There are several methods you can use tooview blob auditing logs:</span></span>

* <span data-ttu-id="a0782-160">사용 하 여 hello [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-160">Use hello [Azure portal](https://portal.azure.com).</span></span>  <span data-ttu-id="a0782-161">열기 hello 관련 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-161">Open hello relevant database.</span></span> <span data-ttu-id="a0782-162">At hello 맨 hello 데이터베이스 **감사 및 위협 검색** 블레이드에서 클릭 **감사 로그 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-162">At hello top of hello database's **Auditing & Threat detection** blade, click **View audit logs**.</span></span>

    ![탐색 창][7]

    <span data-ttu-id="a0782-164">**감사 레코드** 수 tooview hello 로그 거 야 하는 블레이드에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-164">An **Audit records** blade opens, from which you'll be able tooview hello logs.</span></span>

    - <span data-ttu-id="a0782-165">클릭 하 여 특정 날짜를 볼 수 있습니다 **필터** hello의 hello 위쪽 **감사 레코드** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-165">You can view specific dates by clicking **Filter** at hello top of hello **Audit records** blade.</span></span>
    - <span data-ttu-id="a0782-166">서버 정책 또는 데이터베이스 정책 감사에서 생성된 감사 레코드 사이를 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-166">You can switch between audit records that were created by a server policy or database policy audit.</span></span>

       ![탐색 창][8]

* <span data-ttu-id="a0782-168">Hello 시스템 함수를 사용 하 여 **sys.fn_get_audit_file** (T-SQL) tooreturn hello 감사 로그 데이터를 테이블 형식에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-168">Use hello system function **sys.fn_get_audit_file** (T-SQL) tooreturn hello audit log data in tabular format.</span></span> <span data-ttu-id="a0782-169">이 함수를 사용 하 여에 대 한 자세한 내용은 참조 hello [sys.fn_get_audit_file 설명서](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-169">For more information on using this function, see hello [sys.fn_get_audit_file documentation](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span></span>


* <span data-ttu-id="a0782-170">SQL Server Management Studio에서 **감사 파일 병합** 사용(SSMS 17부터 지원):</span><span class="sxs-lookup"><span data-stu-id="a0782-170">Use **Merge Audit Files** in SQL Server Management Studio (starting with SSMS 17):</span></span>  
    1. <span data-ttu-id="a0782-171">Hello SSMS 메뉴에서 선택 **파일** > **열려** > **감사 파일 병합**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-171">From hello SSMS menu, select **File** > **Open** > **Merge Audit Files**.</span></span>

        ![탐색 창][9]
    2. <span data-ttu-id="a0782-173">hello **감사 파일 추가** 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-173">hello **Add Audit Files** dialog box opens.</span></span> <span data-ttu-id="a0782-174">Hello 중 하나를 선택 **추가** 옵션을 선택 하는 로컬 toomerge 감사 파일이 되는지 여부를 디스크 또는 Azure 저장소에서 가져올 (하면 Azure 저장소 세부 정보 및 계정 키 필요한 tooprovide 됩니다).</span><span class="sxs-lookup"><span data-stu-id="a0782-174">Select one of hello **Add** options to choose whether toomerge audit files from a local disk or import them from Azure Storage (you will be required tooprovide your Azure Storage details and account key).</span></span>

    3. <span data-ttu-id="a0782-175">모든 파일 toomerge를 추가한 후 클릭 **확인** toocomplete hello 병합 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-175">After all files toomerge have been added, click **OK** toocomplete hello merge operation.</span></span>

    4. <span data-ttu-id="a0782-176">ssms에서 보고 하 고, 분석할 뿐 내보내기 것 tooan XEL 또는 CSV 파일 또는 tooa 테이블 수 있는 hello 병합 된 파일이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-176">hello merged file opens in SSMS, where you can view and analyze it, as well as export it tooan XEL or CSV file or tooa table.</span></span>

* <span data-ttu-id="a0782-177">사용 하 여 hello [응용 프로그램 동기화](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) 작성 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-177">Use hello [sync application](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) that we have created.</span></span> <span data-ttu-id="a0782-178">Azure에서 실행 하 고 OMS에 Operations Management Suite (OMS) 로그 분석 공용 Api toopush SQL 감사 로그를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-178">It runs in Azure and utilizes Operations Management Suite (OMS) Log Analytics public APIs toopush SQL audit logs into OMS.</span></span> <span data-ttu-id="a0782-179">hello OMS 로그 분석 대시보드를 통해 사용할 수 있도록 OMS 로그 분석에 SQL 감사 로그를 밀어 하는 hello 동기화 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-179">hello sync application pushes SQL audit logs into OMS Log Analytics for consumption via hello OMS Log Analytics dashboard.</span></span> 

* <span data-ttu-id="a0782-180">Power BI를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-180">Use Power BI.</span></span> <span data-ttu-id="a0782-181">Power BI에서 감사 로그 데이터를 보고 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-181">You can view and analyze audit log data in Power BI.</span></span> <span data-ttu-id="a0782-182">자세한 내용은 [Power BI 및 다운로드 가능한 템플릿 액세스](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0782-182">Learn more about [Power BI, and access a downloadable template](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span></span>

* <span data-ttu-id="a0782-183">Hello 포털을 통해 또는 같은 도구를 사용 하 여 Azure 저장소 blob 컨테이너에서 로그 파일을 다운로드 [Azure 저장소 탐색기](http://storageexplorer.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-183">Download log files from your Azure Storage blob container via hello portal or by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
    * <span data-ttu-id="a0782-184">로컬 로그 파일을 다운로드 한 후 두 번 눌러 hello 파일 tooopen 고 SSMS의 hello 로그를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-184">After you have downloaded a log file locally, you can double-click hello file tooopen, view, and analyze hello logs in SSMS.</span></span>
    * <span data-ttu-id="a0782-185">또한 Azure Storage 탐색기를 통해 동시에 여러 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-185">You can also download multiple files simultaneously via Azure Storage Explorer.</span></span> <span data-ttu-id="a0782-186">특정 하위 폴더 (예를 들어 특정 날짜에 대 한 모든 로그 파일이 포함 된 하위)를 마우스 오른쪽 단추로 클릭 하 고 선택 **다른 이름으로 저장** toosave 로컬 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-186">Right-click a specific subfolder (for example, a subfolder that includes all log files for a specific date) and select **Save as** toosave in a local folder.</span></span>

* <span data-ttu-id="a0782-187">추가 방법:</span><span class="sxs-lookup"><span data-stu-id="a0782-187">Additional methods:</span></span>
   * <span data-ttu-id="a0782-188">여러 개의 파일 (또는 hello이이 목록에서 이전 항목에 설명 된 대로 하루 종일 로그 파일을 포함 하는 하위 폴더)를 다운로드 한 후 병합 로컬로 앞에서 설명한 hello SSMS 병합 감사 파일 지침에 설명 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-188">After downloading several files (or a subfolder that includes log files for an entire day, as described in hello previous item in this list), you can merge them locally as described in hello SSMS Merge Audit Files instructions described earlier.</span></span>

   * <span data-ttu-id="a0782-189">프로그래밍 방식으로 Blob 감사 로그를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-189">View blob auditing logs programmatically:</span></span>

     * <span data-ttu-id="a0782-190">사용 하 여 hello [확장 이벤트 판독기](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-190">Use hello [Extended Events Reader](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# library.</span></span>
     * <span data-ttu-id="a0782-191">PowerShell을 사용하여 [확장 이벤트 파일을 쿼리](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-191">[Query Extended Events Files](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) by using PowerShell.</span></span>




## <span data-ttu-id="a0782-192"><a id="subheading-5"></a>프로덕션 사례</span><span class="sxs-lookup"><span data-stu-id="a0782-192"><a id="subheading-5"></a>Production practices</span></span>
<!--hello description in this section refers toopreceding screen captures.-->

### <span data-ttu-id="a0782-193"><a id="subheading-6">지역에서 복제된 데이터베이스 감사</a></span><span class="sxs-lookup"><span data-stu-id="a0782-193"><a id="subheading-6">Auditing geo-replicated databases</a></span></span>
<span data-ttu-id="a0782-194">지리적으로 복제 된 데이터베이스를 사용할 때 가능한 tooset hello 주 데이터베이스, 보조 데이터베이스 hello 또는 hello 감사 유형에 따라 둘 다에 감사를 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-194">When you use geo-replicated databases, it is possible tooset up auditing on either hello primary database, hello secondary database, or both, depending on hello audit type.</span></span>

<span data-ttu-id="a0782-195">(있는지 blob 감사 해도 해당 켜거나 감사 설정 hello 주 데이터베이스 에서만에서 된다는 점에 유의) 이러한 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="a0782-195">Follow these instructions (remember that blob auditing can be turned on or off only from hello primary database auditing settings):</span></span>

* <span data-ttu-id="a0782-196">**주 데이터베이스**.</span><span class="sxs-lookup"><span data-stu-id="a0782-196">**Primary database**.</span></span> <span data-ttu-id="a0782-197">Hello에 설명 된 대로 blob 감사 hello 데이터베이스 자체 또는 hello 서버에 대 한 설정 [데이터베이스에 대 한 감사를 설정](#subheading-2) 섹션.</span><span class="sxs-lookup"><span data-stu-id="a0782-197">Turn on blob auditing, either on hello server or on hello database itself, as described in hello [Set up auditing for your database](#subheading-2) section.</span></span>
* <span data-ttu-id="a0782-198">**보조 데이터베이스**.</span><span class="sxs-lookup"><span data-stu-id="a0782-198">**Secondary database**.</span></span> <span data-ttu-id="a0782-199">Hello에 설명 된 대로 blob hello 주 데이터베이스에서 감사 설정 [데이터베이스에 대 한 감사를 설정](#subheading-2) 섹션.</span><span class="sxs-lookup"><span data-stu-id="a0782-199">Turn on blob auditing on hello primary database, as described in hello [Set up auditing for your database](#subheading-2) section.</span></span> 
   * <span data-ttu-id="a0782-200">Hello에서 blob 감사를 사용할 수 있어야 *주 데이터베이스 자체*, hello 서버가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-200">Blob auditing must be enabled on hello *primary database itself*, not hello server.</span></span>
   * <span data-ttu-id="a0782-201">Blob 감사 hello 주 데이터베이스에서 활성화 된 후 것도 사용 가능해 집니다 hello 보조 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-201">After blob auditing is enabled on hello primary database, it will also become enabled on hello secondary database.</span></span>

     >[!IMPORTANT]
     ><span data-ttu-id="a0782-202">기본적으로 hello 보조 데이터베이스에 대 한 저장소 설정을 hello 됩니다 동일한 toothose hello 주 데이터베이스의 지역 간 트래픽 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-202">By default, hello storage settings for hello secondary database will be identical toothose of hello primary database, causing cross-regional traffic.</span></span> <span data-ttu-id="a0782-203">보조 서버 hello에 대 한 blob 감사 hello 보조 서버 저장소 설정에 로컬 저장소를 구성 및 사용 하 여이 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-203">You can avoid this by enabling blob auditing on hello secondary server and configuring local storage in hello secondary server storage settings.</span></span> <span data-ttu-id="a0782-204">그러면 hello 보조 데이터베이스와 해당 감사 로그 toolocal 저장소를 저장 하는 각 데이터베이스에 결과 대 한 저장소 위치 hello 재정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-204">This will override hello storage location for hello secondary database and result in each database saving its audit logs toolocal storage.</span></span>  
<br>

### <span data-ttu-id="a0782-205"><a id="subheading-6">저장소 키 다시 생성</a></span><span class="sxs-lookup"><span data-stu-id="a0782-205"><a id="subheading-6">Storage key regeneration</a></span></span>
<span data-ttu-id="a0782-206">프로덕션 환경에서 저장소 키를 주기적으로 가능성이 toorefresh 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-206">In production, you are likely toorefresh your storage keys periodically.</span></span> <span data-ttu-id="a0782-207">키를 새로 고치거 나, tooresave hello 감사 정책을 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-207">When refreshing your keys, you need tooresave hello auditing policy.</span></span> <span data-ttu-id="a0782-208">hello 프로세스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-208">hello process is as follows:</span></span>

1. <span data-ttu-id="a0782-209">열기 hello **저장소 세부 정보** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-209">Open hello **Storage Details** blade.</span></span> <span data-ttu-id="a0782-210">Hello에 **저장소 액세스 키** 상자 **보조**를 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-210">In hello **Storage Access Key** box, select **Secondary**, and click **OK**.</span></span> <span data-ttu-id="a0782-211">클릭 **저장** 구성 블레이드를 감사 하는 hello hello 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-211">Then click **Save** at hello top of hello auditing configuration blade.</span></span>

    ![탐색 창][5]
2. <span data-ttu-id="a0782-213">Toohello 저장소 구성 블레이드로 이동 하 고 hello 기본 액세스 키 다시 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-213">Go toohello storage configuration blade and regenerate hello primary access key.</span></span>

    ![탐색 창][6]
3. <span data-ttu-id="a0782-215">감사 구성 블레이드 toohello 돌아가서 hello 저장소 액세스 키 보조 tooprimary에서 전환한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-215">Go back toohello auditing configuration blade, switch hello storage access key from secondary tooprimary, and then click **OK**.</span></span> <span data-ttu-id="a0782-216">클릭 **저장** 구성 블레이드를 감사 하는 hello hello 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-216">Then click **Save** at hello top of hello auditing configuration blade.</span></span>
4. <span data-ttu-id="a0782-217">Toohello 저장소 구성 블레이드 및 (hello 다음 키 새로 고침 주기는 준비 과정)에서 보조 액세스 키 다시 생성 hello 다시 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-217">Go back toohello storage configuration blade and regenerate hello secondary access key (in preparation for hello next key's refresh cycle).</span></span>

## <span data-ttu-id="a0782-218"><a id="subheading-7"></a>Automation(PowerShell/REST API)</span><span class="sxs-lookup"><span data-stu-id="a0782-218"><a id="subheading-7"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="a0782-219">또한 hello 다음 자동화 도구를 사용 하 여 Azure SQL 데이터베이스에서 감사를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0782-219">You can also configure auditing in Azure SQL Database by using hello following automation tools:</span></span>

* <span data-ttu-id="a0782-220">**PowerShell cmdlet**:</span><span class="sxs-lookup"><span data-stu-id="a0782-220">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="a0782-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="a0782-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="a0782-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="a0782-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="a0782-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="a0782-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="a0782-224">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="a0782-224">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="a0782-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="a0782-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="a0782-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="a0782-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="a0782-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="a0782-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

   <span data-ttu-id="a0782-228">스크립트 예제는 [PowerShell을 사용하여 감사 및 위협 감지 구성](scripts/sql-database-auditing-and-threat-detection-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0782-228">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

* <span data-ttu-id="a0782-229">**REST API - Blob 감사**</span><span class="sxs-lookup"><span data-stu-id="a0782-229">**REST API - Blob auditing**:</span></span>

   * [<span data-ttu-id="a0782-230">데이터베이스 Blob 감사 정책 만들기 또는 업데이트</span><span class="sxs-lookup"><span data-stu-id="a0782-230">Create or Update Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695939.aspx)
   * [<span data-ttu-id="a0782-231">서버 Blob 감사 정책 만들기 또는 업데이트</span><span class="sxs-lookup"><span data-stu-id="a0782-231">Create or Update Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771861.aspx)
   * [<span data-ttu-id="a0782-232">데이터베이스 Blob 감사 정책 가져오기</span><span class="sxs-lookup"><span data-stu-id="a0782-232">Get Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695938.aspx)
   * [<span data-ttu-id="a0782-233">서버 Blob 감사 정책 가져오기</span><span class="sxs-lookup"><span data-stu-id="a0782-233">Get Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771860.aspx)
   * [<span data-ttu-id="a0782-234">서버 Blob 감사 작업 결과 가져오기</span><span class="sxs-lookup"><span data-stu-id="a0782-234">Get Server Blob Auditing Operation Result</span></span>](https://msdn.microsoft.com/library/azure/mt771862.aspx)


<!--Anchors-->
[Azure SQL Database Auditing overview]: #subheading-1
[Set up auditing for your database]: #subheading-2
[Analyze audit logs and reports]: #subheading-3
[Practices for usage in production]: #subheading-5
[Storage Key Regeneration]: #subheading-6
[Automation (PowerShell / REST API)]: #subheading-7
[Blob/Table differences in Server auditing policy inheritance]: (#subheading-8)  

<!--Image references-->
[1]: ./media/sql-database-auditing-get-started/1_auditing_get_started_settings.png
[2]: ./media/sql-database-auditing-get-started/2_auditing_get_started_server_inherit.png
[3]: ./media/sql-database-auditing-get-started/3_auditing_get_started_turn_on.png
[4]: ./media/sql-database-auditing-get-started/4_auditing_get_started_storage_details.png
[5]: ./media/sql-database-auditing-get-started/5_auditing_get_started_storage_key_regeneration.png
[6]: ./media/sql-database-auditing-get-started/6_auditing_get_started_regenerate_key.png
[7]: ./media/sql-database-auditing-get-started/7_auditing_get_started_blob_view_audit_logs.png
[8]: ./media/sql-database-auditing-get-started/8_auditing_get_started_blob_audit_records.png
[9]: ./media/sql-database-auditing-get-started/9_auditing_get_started_ssms_1.png
[10]: ./media/sql-database-auditing-get-started/10_auditing_get_started_ssms_2.png

[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy
