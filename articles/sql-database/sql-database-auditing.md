---
title: "Azure SQL Database 감사 시작 | Microsoft Docs"
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
ms.openlocfilehash: f4324a59b5fa4c2e1ab5b1d7fc7e5fe986ea80f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-sql-database-auditing"></a><span data-ttu-id="dcf61-103">SQL 데이터베이스 감사 시작</span><span class="sxs-lookup"><span data-stu-id="dcf61-103">Get started with SQL database auditing</span></span>
<span data-ttu-id="dcf61-104">Azure SQL Database 감사는 데이터베이스 이벤트를 추적하고 Azure Storage 계정의 감사 로그에 이벤트를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-104">Azure SQL database auditing tracks database events and writes them to an audit log in your Azure storage account.</span></span> <span data-ttu-id="dcf61-105">또한</span><span class="sxs-lookup"><span data-stu-id="dcf61-105">Auditing also:</span></span>

* <span data-ttu-id="dcf61-106">감사는 규정 준수를 유지 관리하고, 데이터베이스 작업을 이해하고, 비즈니스 문제나 의심스러운 보안 위반을 나타낼 수 있는 불일치 및 이상 활동을 파악하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-106">Helps you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

* <span data-ttu-id="dcf61-107">감사를 사용하면 규정을 완전히 준수한다고 보장할 수는 없지만 규정 표준을 보다 쉽게 준수할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-107">Enables and facilitates adherence to compliance standards, although it doesn't guarantee compliance.</span></span> <span data-ttu-id="dcf61-108">표준 규정 준수를 지원하는 Azure 프로그램에 대한 자세한 내용은 [Azure 보안 센터](https://azure.microsoft.com/support/trust-center/compliance/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dcf61-108">For more information about Azure programs that support standards compliance, see the [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).</span></span>


## <span data-ttu-id="dcf61-109"><a id="subheading-1"></a>Azure SQL Database 감사 개요</span><span class="sxs-lookup"><span data-stu-id="dcf61-109"><a id="subheading-1"></a>Azure SQL database auditing overview</span></span>
<span data-ttu-id="dcf61-110">SQL Database 감사를 사용하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-110">You can use SQL database auditing to:</span></span>


* <span data-ttu-id="dcf61-111">**유지** 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-111">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="dcf61-112">감사할 데이터베이스 동작의 범주를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-112">You can define categories of database actions to be audited.</span></span>
* <span data-ttu-id="dcf61-113">**보고** 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-113">**Report** on database activity.</span></span> <span data-ttu-id="dcf61-114">미리 구성된 보고서 및 대시보드를 사용하여 활동 및 이벤트 보고를 빠르게 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-114">You can use preconfigured reports and a dashboard to get started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="dcf61-115">**분석** 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-115">**Analyze** reports.</span></span> <span data-ttu-id="dcf61-116">의심스러운 이벤트, 특별한 활동 및 추세를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-116">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="dcf61-117">[데이터베이스에 대한 감사 설정](#subheading-2) 섹션에 설명된 대로 여러 이벤트 범주 유형에 대해 감사를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-117">You can configure auditing for different types of event categories, as explained in the [Set up auditing for your database](#subheading-2) section.</span></span>

<span data-ttu-id="dcf61-118">감사 로그는 Azure 구독의 Azure Blob Storage에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-118">Audit logs are written to Azure Blob storage on your Azure subscription.</span></span>


## <span data-ttu-id="dcf61-119"><a id="subheading-8"></a>서버 수준 및 데이터베이스 수준 감사 정책 정의</span><span class="sxs-lookup"><span data-stu-id="dcf61-119"><a id="subheading-8"></a>Define server-level vs. database-level auditing policy</span></span>

<span data-ttu-id="dcf61-120">특정 데이터베이스에 대해 또는 기본 서버 정책으로 감사 정책을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-120">An auditing policy can be defined for a specific database or as a default server policy:</span></span>

* <span data-ttu-id="dcf61-121">서버에 있는 모든 기존 데이터베이스 및 새로 만든 데이터베이스에 서버 정책이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-121">A server policy applies to all existing and newly created databases on the server.</span></span>

* <span data-ttu-id="dcf61-122">*서버 Blob 감사가 설정된* 경우 데이터베이스 감사 설정에 관계 없이 *항상 데이터베이스에 적용됩니다*(즉, 데이터베이스가 감사됨).</span><span class="sxs-lookup"><span data-stu-id="dcf61-122">If *server blob auditing is enabled*, it *always applies to the database* (that is, the database will be audited), regardless of the database auditing settings.</span></span>

* <span data-ttu-id="dcf61-123">서버에서 활성화하는 것 외에도 데이터베이스에 대한 Blob 감사를 활성화하는 것은 서버 Blob 감사 설정을 재정의 또는 변경하지 *않습니다*.</span><span class="sxs-lookup"><span data-stu-id="dcf61-123">Enabling blob auditing on the database, in addition to enabling it on the server, will *not* override or change any of the settings of the server blob auditing.</span></span> <span data-ttu-id="dcf61-124">두 감사는 함께 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-124">Both audits will exist side by side.</span></span> <span data-ttu-id="dcf61-125">즉, 데이터베이스는 동시에 두 번 감사됩니다(서버 정책에서 한 번, 데이터베이스 정책에서 한번).</span><span class="sxs-lookup"><span data-stu-id="dcf61-125">In other words, the database will be audited twice in parallel (once by the server policy and once by the database policy).</span></span>

   > [!NOTE]
   > <span data-ttu-id="dcf61-126">다음과 같은 경우가 아니면 서버 Blob 감사 및 데이터베이스 Blob 감사를 함께 활성화하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-126">You should avoid enabling both server blob auditing and database blob auditing together, unless:</span></span>
    > * <span data-ttu-id="dcf61-127">특정 데이터베이스에 대해 다른 *저장소 계정* 또는 *보존 기간*을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-127">You want to use a different *storage account* or *retention period* for a specific database.</span></span>
    > * <span data-ttu-id="dcf61-128">특정 데이터베이스에 대해, 서버의 나머지 데이터베이스에 대해 감사되는 이벤트 유형 또는 범주와 다른 이벤트 유형 또는 범주를 감사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-128">You want to audit event types or categories for a specific database that differ from event types or categories that are being audited for the rest of the databases on the server.</span></span> <span data-ttu-id="dcf61-129">예를 들어 특정 데이터베이스에 대해서만 감사해야 하는 테이블 삽입이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-129">For example, you might have table inserts that need to be audited only for a specific database.</span></span>
   > 
   > <span data-ttu-id="dcf61-130">그렇지 않으면 서버 수준 Blob 감사만 활성화하고 모든 데이터베이스에 대해 데이터베이스 수준 감사를 비활성화로 유지하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-130">Otherwise, we recommended that you enable only server-level blob auditing and leave the database-level auditing disabled for all databases.</span></span>


## <span data-ttu-id="dcf61-131"><a id="subheading-2"></a>데이터베이스에 대한 감사 설정</span><span class="sxs-lookup"><span data-stu-id="dcf61-131"><a id="subheading-2"></a>Set up auditing for your database</span></span>
<span data-ttu-id="dcf61-132">다음 섹션에서는 Azure Portal을 사용하여 감사 구성을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-132">The following section describes the configuration of auditing using the Azure portal.</span></span>

1. <span data-ttu-id="dcf61-133">[Azure 포털](https://portal.azure.com)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-133">Go to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="dcf61-134">감사할 SQL Database/SQL Server의 **설정** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-134">Go to the **Settings** blade of the SQL database/SQL server you want to audit.</span></span> <span data-ttu-id="dcf61-135">**설정** 블레이드에서 **감사 및 위협 감지**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-135">In the **Settings** blade, select **Auditing & Threat detection**.</span></span>

    <span data-ttu-id="dcf61-136"><a id="auditing-screenshot"></a> ![탐색 창][1]</span><span class="sxs-lookup"><span data-stu-id="dcf61-136"><a id="auditing-screenshot"></a> ![Navigation pane][1]</span></span>
3. <span data-ttu-id="dcf61-137">이 서버의 모든 기존 및 새로 만든 데이터베이스에 적용되는 서버 감사 정책을 설정하려면 데이터베이스 감사 블레이드에서 **서버 설정 보기** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-137">If you prefer to set up a server auditing policy (which will apply to all existing and newly created databases on this server), you can select the **View server settings** link in the database auditing blade.</span></span> <span data-ttu-id="dcf61-138">그런 다음 서버 감사 설정을 보거나 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-138">You can then view or modify the server auditing settings.</span></span>

    ![탐색 창][2]
4. <span data-ttu-id="dcf61-140">서버 수준 감사 대신 또는 추가로 데이터베이스 수준에서 Blob 감사를 사용하려면 **감사**에 대해 **설정**을 선택하고 **감사 형식**에 대해 **Blob**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-140">If you prefer to enable blob auditing on the database level (in addition to or instead of server-level auditing), for **Auditing**, select **ON**, and for **Auditing type**, select  **Blob**.</span></span>

    <span data-ttu-id="dcf61-141">서버 Blob 감사가 활성화되면 데이터베이스 구성 감사가 서버 Blob 감사와 나란히 존재하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-141">If server blob auditing is enabled, the database-configured audit will exist side by side with the server blob audit.</span></span>  

    ![탐색 창][3]
5. <span data-ttu-id="dcf61-143">**감사 로그 저장소** 블레이드를 열려면 **저장소 세부 정보**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-143">To open the **Audit Logs Storage** blade, select **Storage Details**.</span></span> <span data-ttu-id="dcf61-144">로그가 저장되는 Azure Storage 계정을 선택하고, 이 기간 후 오래된 로그가 삭제되는 보존 기간을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-144">Select the Azure storage account where logs will be saved, and then select the retention period, after which the old logs will be deleted.</span></span> <span data-ttu-id="dcf61-145">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-145">Then click **OK**.</span></span> 
   >[!TIP] 
   ><span data-ttu-id="dcf61-146">감사 보고서 템플릿을 활용하려면 감사되는 모든 데이터베이스에 동일한 저장소 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-146">To get the most out of the auditing reports templates, use the same storage account for all audited databases.</span></span> 

    <span data-ttu-id="dcf61-147"><a id="storage-screenshot"></a> ![탐색 창][4]</span><span class="sxs-lookup"><span data-stu-id="dcf61-147"><a id="storage-screenshot"></a> ![Navigation pane][4]</span></span>
6. <span data-ttu-id="dcf61-148">감사 이벤트를 사용자 지정하려면 PowerShell 또는 REST API를 통해 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-148">If you want to customize the audited events, you can do this via PowerShell or the REST API.</span></span> <span data-ttu-id="dcf61-149">자세한 내용은 [Automation(PowerShell/REST API)](#subheading-7) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dcf61-149">For more details, see the [Automation (PowerShell/REST API)](#subheading-7) section.</span></span>
7. <span data-ttu-id="dcf61-150">감사 설정을 구성했으면 새로운 위협 감지 기능을 켜고, 보안 경고를 받을 전자 메일을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-150">After you've configured your auditing settings, you can turn on the new threat detection feature and configure emails to receive security alerts.</span></span> <span data-ttu-id="dcf61-151">위협 감지를 사용하면 잠재적인 보안 위협을 나타낼 수 있는 비정상적인 데이터베이스 활동에 대해 사전 경고를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-151">When you use threat detection, you receive proactive alerts on anomalous database activities that can indicate potential security threats.</span></span> <span data-ttu-id="dcf61-152">자세한 내용은 [위협 감지 시작](sql-database-threat-detection-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dcf61-152">For more details, see [Getting started with threat detection](sql-database-threat-detection-get-started.md).</span></span>
8. <span data-ttu-id="dcf61-153">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-153">Click **Save**.</span></span>





## <span data-ttu-id="dcf61-154"><a id="subheading-3"></a>감사 로그 및 보고서 분석</span><span class="sxs-lookup"><span data-stu-id="dcf61-154"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="dcf61-155">감사 로그는 설치 중에 선택한 Azure 저장소 계정에 집계됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-155">Audit logs are aggregated in the Azure storage account you chose during setup.</span></span> <span data-ttu-id="dcf61-156">[Azure Storage 탐색기](http://storageexplorer.com/) 등의 도구를 사용하여 감사 로그를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-156">You can explore audit logs by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="dcf61-157">Blob 감사 로그는 **sqldbauditlogs**라는 컨테이너 내부에 Blob 파일 컬렉션으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-157">Blob auditing logs are saved as a collection of blob files within a container named **sqldbauditlogs**.</span></span>

<span data-ttu-id="dcf61-158">Blob 감사 로그 저장소 폴더의 계층 구조, Blob 명명 규칙 및 로그 형식에 대한 자세한 내용은 [감사 로그 형식 참조(doc 파일 다운로드)](https://go.microsoft.com/fwlink/?linkid=829599)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dcf61-158">For further details about the hierarchy of the blob audit logs storage folder, blob naming conventions, and log format, see the [Blob Audit Log Format Reference (.docx file download)](https://go.microsoft.com/fwlink/?linkid=829599).</span></span>

<span data-ttu-id="dcf61-159">Blob 감사 로그를 볼 수 있는 여러 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-159">There are several methods you can use to view blob auditing logs:</span></span>

* <span data-ttu-id="dcf61-160">[Azure Portal을 사용](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-160">Use the [Azure portal](https://portal.azure.com).</span></span>  <span data-ttu-id="dcf61-161">관련 데이터베이스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-161">Open the relevant database.</span></span> <span data-ttu-id="dcf61-162">데이터베이스의 **감사 및 위협 감지** 블레이드 맨 위에서 **감사 로그 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-162">At the top of the database's **Auditing & Threat detection** blade, click **View audit logs**.</span></span>

    ![탐색 창][7]

    <span data-ttu-id="dcf61-164">**감사 레코드** 블레이드가 열리고, 여기서 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-164">An **Audit records** blade opens, from which you'll be able to view the logs.</span></span>

    - <span data-ttu-id="dcf61-165">**감사 레코드** 블레이드의 맨 위쪽에서 **필터**를 클릭하여 특정 날짜를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-165">You can view specific dates by clicking **Filter** at the top of the **Audit records** blade.</span></span>
    - <span data-ttu-id="dcf61-166">서버 정책 또는 데이터베이스 정책 감사에서 생성된 감사 레코드 사이를 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-166">You can switch between audit records that were created by a server policy or database policy audit.</span></span>

       ![탐색 창][8]

* <span data-ttu-id="dcf61-168">시스템 함수 **sys.fn_get_audit_file**(T-SQL)을 사용하여 테이블 형식의 감사 로그 데이터를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-168">Use the system function **sys.fn_get_audit_file** (T-SQL) to return the audit log data in tabular format.</span></span> <span data-ttu-id="dcf61-169">이 함수 사용에 대한 자세한 내용은 [sys.fn_get_audit_file 설명서](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dcf61-169">For more information on using this function, see the [sys.fn_get_audit_file documentation](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span></span>


* <span data-ttu-id="dcf61-170">SQL Server Management Studio에서 **감사 파일 병합** 사용(SSMS 17부터 지원):</span><span class="sxs-lookup"><span data-stu-id="dcf61-170">Use **Merge Audit Files** in SQL Server Management Studio (starting with SSMS 17):</span></span>  
    1. <span data-ttu-id="dcf61-171">SSMS 메뉴에서 **파일** > **열기** > **감사 파일 병합**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-171">From the SSMS menu, select **File** > **Open** > **Merge Audit Files**.</span></span>

        ![탐색 창][9]
    2. <span data-ttu-id="dcf61-173">**감사 파일 추가** 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-173">The **Add Audit Files** dialog box opens.</span></span> <span data-ttu-id="dcf61-174">**추가** 옵션 중 하나를 선택하여 로컬 디스크에서 감사 파일을 병합할지 또는 Azure Storage에서 감사 파일을 가져올지(Azure Storage 세부 정보 및 계정 키를 제공해야 함) 선택합니다</span><span class="sxs-lookup"><span data-stu-id="dcf61-174">Select one of the **Add** options to choose whether to merge audit files from a local disk or import them from Azure Storage (you will be required to provide your Azure Storage details and account key).</span></span>

    3. <span data-ttu-id="dcf61-175">병합할 모든 파일을 추가했으면 **확인**을 클릭하여 병합 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-175">After all files to merge have been added, click **OK** to complete the merge operation.</span></span>

    4. <span data-ttu-id="dcf61-176">병합된 파일이 SSMS에서 열립니다. 여기에서 파일을 보고 분석할 수 있을 뿐만 아니라 XEL 또는 CSV 파일이나 테이블로 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-176">The merged file opens in SSMS, where you can view and analyze it, as well as export it to an XEL or CSV file or to a table.</span></span>

* <span data-ttu-id="dcf61-177">Microsoft에서 만든 [동기화 응용 프로그램](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-177">Use the [sync application](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) that we have created.</span></span> <span data-ttu-id="dcf61-178">이 응용 프로그램은 Azure에서 실행되며 OMS(Operations Management Suite) Log Analytics 공용 API를 사용하여 SQL 감사 로그를 OMS에 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-178">It runs in Azure and utilizes Operations Management Suite (OMS) Log Analytics public APIs to push SQL audit logs into OMS.</span></span> <span data-ttu-id="dcf61-179">동기화 응용 프로그램은 OMS Log Analytics 대시보드를 통해 사용할 수 있도록 OMS Log Analytics에 SQL 감사 로그를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-179">The sync application pushes SQL audit logs into OMS Log Analytics for consumption via the OMS Log Analytics dashboard.</span></span> 

* <span data-ttu-id="dcf61-180">Power BI를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-180">Use Power BI.</span></span> <span data-ttu-id="dcf61-181">Power BI에서 감사 로그 데이터를 보고 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-181">You can view and analyze audit log data in Power BI.</span></span> <span data-ttu-id="dcf61-182">자세한 내용은 [Power BI 및 다운로드 가능한 템플릿 액세스](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dcf61-182">Learn more about [Power BI, and access a downloadable template](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span></span>

* <span data-ttu-id="dcf61-183">포털을 통해 또는 [Azure Storage 탐색기](http://storageexplorer.com/) 같은 도구를 사용하여 Azure Storage Blob 컨테이너에서 로그 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-183">Download log files from your Azure Storage blob container via the portal or by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
    * <span data-ttu-id="dcf61-184">로그 파일을 로컬에 다운로드한 후에는 해당 파일을 두 번 클릭하여 열고, SSMS에서 로그를 살펴보고 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-184">After you have downloaded a log file locally, you can double-click the file to open, view, and analyze the logs in SSMS.</span></span>
    * <span data-ttu-id="dcf61-185">또한 Azure Storage 탐색기를 통해 동시에 여러 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-185">You can also download multiple files simultaneously via Azure Storage Explorer.</span></span> <span data-ttu-id="dcf61-186">특정 하위 폴더(예: 특정 날짜에 대한 모든 로그 파일이 포함된 하위 폴더)를 마우스 오른쪽 단추로 클릭하고 **다른 이름으로 저장**을 선택하여 로컬 폴더에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-186">Right-click a specific subfolder (for example, a subfolder that includes all log files for a specific date) and select **Save as** to save in a local folder.</span></span>

* <span data-ttu-id="dcf61-187">추가 방법:</span><span class="sxs-lookup"><span data-stu-id="dcf61-187">Additional methods:</span></span>
   * <span data-ttu-id="dcf61-188">여러 파일(또는 이 목록의 이전 항목에 설명된 대로 하루 전체에 대한 로그 파일이 포함된 하위 폴더)을 다운로드한 후 SSMS 감사 파일 병합 지침에 설명된 대로 파일을 로컬로 병합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-188">After downloading several files (or a subfolder that includes log files for an entire day, as described in the previous item in this list), you can merge them locally as described in the SSMS Merge Audit Files instructions described earlier.</span></span>

   * <span data-ttu-id="dcf61-189">프로그래밍 방식으로 Blob 감사 로그를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-189">View blob auditing logs programmatically:</span></span>

     * <span data-ttu-id="dcf61-190">[확장 이벤트 판독기](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-190">Use the [Extended Events Reader](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# library.</span></span>
     * <span data-ttu-id="dcf61-191">PowerShell을 사용하여 [확장 이벤트 파일을 쿼리](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/)합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-191">[Query Extended Events Files](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) by using PowerShell.</span></span>




## <span data-ttu-id="dcf61-192"><a id="subheading-5"></a>프로덕션 사례</span><span class="sxs-lookup"><span data-stu-id="dcf61-192"><a id="subheading-5"></a>Production practices</span></span>
<!--The description in this section refers to preceding screen captures.-->

### <span data-ttu-id="dcf61-193"><a id="subheading-6">지역에서 복제된 데이터베이스 감사</a></span><span class="sxs-lookup"><span data-stu-id="dcf61-193"><a id="subheading-6">Auditing geo-replicated databases</a></span></span>
<span data-ttu-id="dcf61-194">지역에서 복제된 데이터베이스를 사용하는 경우 감사 유형에 따라 주 데이터베이스, 보조 데이터베이스 또는 둘 모두에 감사를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-194">When you use geo-replicated databases, it is possible to set up auditing on either the primary database, the secondary database, or both, depending on the audit type.</span></span>

<span data-ttu-id="dcf61-195">다음 지침을 따릅니다(Blob 감사는 주 데이터베이스 감사 설정에서만 켜고 끌 수 있음).</span><span class="sxs-lookup"><span data-stu-id="dcf61-195">Follow these instructions (remember that blob auditing can be turned on or off only from the primary database auditing settings):</span></span>

* <span data-ttu-id="dcf61-196">**주 데이터베이스**.</span><span class="sxs-lookup"><span data-stu-id="dcf61-196">**Primary database**.</span></span> <span data-ttu-id="dcf61-197">[데이터베이스에 대한 감사 설정](#subheading-2) 섹션에 설명된 대로 서버 또는 데이터베이스 자체에서 Blob 감사를 켭니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-197">Turn on blob auditing, either on the server or on the database itself, as described in the [Set up auditing for your database](#subheading-2) section.</span></span>
* <span data-ttu-id="dcf61-198">**보조 데이터베이스**.</span><span class="sxs-lookup"><span data-stu-id="dcf61-198">**Secondary database**.</span></span> <span data-ttu-id="dcf61-199">[데이터베이스에 대한 감사 설정](#subheading-2) 섹션에 설명된 대로 주 데이터베이스에서 Blob 감사를 켭니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-199">Turn on blob auditing on the primary database, as described in the [Set up auditing for your database](#subheading-2) section.</span></span> 
   * <span data-ttu-id="dcf61-200">Blob 감사는 서버가 아니라 *주 데이터베이스 자체*에서 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-200">Blob auditing must be enabled on the *primary database itself*, not the server.</span></span>
   * <span data-ttu-id="dcf61-201">주 데이터베이스에서 Blob 감사가 활성화되면 보조 데이터베이스에서도 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-201">After blob auditing is enabled on the primary database, it will also become enabled on the secondary database.</span></span>

     >[!IMPORTANT]
     ><span data-ttu-id="dcf61-202">기본적으로는 보조 데이터베이스의 저장소 설정은 주 데이터베이스와 동일하기 때문에 지역 간 트래픽이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-202">By default, the storage settings for the secondary database will be identical to those of the primary database, causing cross-regional traffic.</span></span> <span data-ttu-id="dcf61-203">보조 서버에서 Blob 감사를 활성화하고 보조 서버 저장소 설정에서 로컬 저장소를 구성하면 이를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-203">You can avoid this by enabling blob auditing on the secondary server and configuring local storage in the secondary server storage settings.</span></span> <span data-ttu-id="dcf61-204">이 구성은 보조 데이터베이스의 저장소 위치를 재정의하며 각 데이터베이스에서 해당 감사 로그를 로컬 저장소에 저장하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-204">This will override the storage location for the secondary database and result in each database saving its audit logs to local storage.</span></span>  
<br>

### <span data-ttu-id="dcf61-205"><a id="subheading-6">저장소 키 다시 생성</a></span><span class="sxs-lookup"><span data-stu-id="dcf61-205"><a id="subheading-6">Storage key regeneration</a></span></span>
<span data-ttu-id="dcf61-206">프로덕션에서는 저장소 키를 주기적으로 새로 고치게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-206">In production, you are likely to refresh your storage keys periodically.</span></span> <span data-ttu-id="dcf61-207">키를 새로 고칠 때 감사 정책을 다시 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-207">When refreshing your keys, you need to resave the auditing policy.</span></span> <span data-ttu-id="dcf61-208">프로세스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-208">The process is as follows:</span></span>

1. <span data-ttu-id="dcf61-209">**저장소 세부 정보** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-209">Open the **Storage Details** blade.</span></span> <span data-ttu-id="dcf61-210">**저장소 액세스 키** 상자에서 **보조**를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-210">In the **Storage Access Key** box, select **Secondary**, and click **OK**.</span></span> <span data-ttu-id="dcf61-211">그런 다음 감사 구성 블레이드의 맨 위에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-211">Then click **Save** at the top of the auditing configuration blade.</span></span>

    ![탐색 창][5]
2. <span data-ttu-id="dcf61-213">스토리지 구성 블레이드로 이동하고 기본 액세스 키를 다시 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-213">Go to the storage configuration blade and regenerate the primary access key.</span></span>

    ![탐색 창][6]
3. <span data-ttu-id="dcf61-215">감사 구성 블레이드로 돌아가서 저장소 액세스 키를 보조에서 기본으로 전환하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-215">Go back to the auditing configuration blade, switch the storage access key from secondary to primary, and then click **OK**.</span></span> <span data-ttu-id="dcf61-216">그런 다음 감사 구성 블레이드의 맨 위에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-216">Then click **Save** at the top of the auditing configuration blade.</span></span>
4. <span data-ttu-id="dcf61-217">저장소 구성 블레이드로 돌아와서 보조 액세스 키를 다시 생성합니다(다음 키 새로 고침 주기를 위한 준비).</span><span class="sxs-lookup"><span data-stu-id="dcf61-217">Go back to the storage configuration blade and regenerate the secondary access key (in preparation for the next key's refresh cycle).</span></span>

## <span data-ttu-id="dcf61-218"><a id="subheading-7"></a>Automation(PowerShell/REST API)</span><span class="sxs-lookup"><span data-stu-id="dcf61-218"><a id="subheading-7"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="dcf61-219">또한 다음 자동화 도구를 사용하여 Azure SQL Database에서 감사를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf61-219">You can also configure auditing in Azure SQL Database by using the following automation tools:</span></span>

* <span data-ttu-id="dcf61-220">**PowerShell cmdlet**:</span><span class="sxs-lookup"><span data-stu-id="dcf61-220">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="dcf61-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="dcf61-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="dcf61-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="dcf61-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="dcf61-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="dcf61-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="dcf61-224">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="dcf61-224">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="dcf61-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="dcf61-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="dcf61-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="dcf61-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="dcf61-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="dcf61-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

   <span data-ttu-id="dcf61-228">스크립트 예제는 [PowerShell을 사용하여 감사 및 위협 감지 구성](scripts/sql-database-auditing-and-threat-detection-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dcf61-228">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

* <span data-ttu-id="dcf61-229">**REST API - Blob 감사**</span><span class="sxs-lookup"><span data-stu-id="dcf61-229">**REST API - Blob auditing**:</span></span>

   * [<span data-ttu-id="dcf61-230">데이터베이스 Blob 감사 정책 만들기 또는 업데이트</span><span class="sxs-lookup"><span data-stu-id="dcf61-230">Create or Update Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695939.aspx)
   * [<span data-ttu-id="dcf61-231">서버 Blob 감사 정책 만들기 또는 업데이트</span><span class="sxs-lookup"><span data-stu-id="dcf61-231">Create or Update Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771861.aspx)
   * [<span data-ttu-id="dcf61-232">데이터베이스 Blob 감사 정책 가져오기</span><span class="sxs-lookup"><span data-stu-id="dcf61-232">Get Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695938.aspx)
   * [<span data-ttu-id="dcf61-233">서버 Blob 감사 정책 가져오기</span><span class="sxs-lookup"><span data-stu-id="dcf61-233">Get Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771860.aspx)
   * [<span data-ttu-id="dcf61-234">서버 Blob 감사 작업 결과 가져오기</span><span class="sxs-lookup"><span data-stu-id="dcf61-234">Get Server Blob Auditing Operation Result</span></span>](https://msdn.microsoft.com/library/azure/mt771862.aspx)


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
