---
title: "SQL 데이터 웨어하우스 위협 감지 시작"
description: "위협 감지를 시작하는 시기"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: c9073dd9-6c62-4735-8457-dfb9f859c900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: f4a2376fe4fb710d031c35ca7fdbf4c7bb0f3caa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-threat-detection"></a><span data-ttu-id="ae909-103">위협 감지 시작</span><span class="sxs-lookup"><span data-stu-id="ae909-103">Get started with threat detection</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ae909-104">감사</span><span class="sxs-lookup"><span data-stu-id="ae909-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="ae909-105">위협 감지</span><span class="sxs-lookup"><span data-stu-id="ae909-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="ae909-106">개요</span><span class="sxs-lookup"><span data-stu-id="ae909-106">Overview</span></span>
<span data-ttu-id="ae909-107">위협 감지는 데이터베이스에 대한 잠재적인 보안 위협을 나타내는 비정상적인 데이터베이스 활동을 감지합니다.</span><span class="sxs-lookup"><span data-stu-id="ae909-107">Threat Detection detects anomalous database activities indicating potential security threats to the database.</span></span> <span data-ttu-id="ae909-108">위협 감지는 미리 보기로 제공되며 SQL 데이터 웨어하우스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ae909-108">Threat Detection is in preview and is supported for SQL Data Warehouse.</span></span>

<span data-ttu-id="ae909-109">위협 감지는 비정상적인 활동에 대한 보안 경고를 제공하여 잠재적인 위협이 발생하면 고객이 이를 감지하고 대응할 수 있도록 하는 새로운 차원의 보안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ae909-109">Threat Detection provides a new layer of security, which enables customers to detect and respond to potential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="ae909-110">사용자는 데이터 웨어하우스의 데이터를 액세스, 침해 또는 악용하려는 시도로 인해 의심스러운 이벤트가 발생했는지를 판단하기 위해서 [Azure SQL Data Warehouse 감사](sql-data-warehouse-auditing-overview.md) 를 사용하여 의심스러운 이벤트를 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae909-110">Users can explore the suspicious events using [Azure SQL Data Warehouse Auditing](sql-data-warehouse-auditing-overview.md) to determine if they result from an attempt to access, breach or exploit data in the data warehouse.</span></span>
<span data-ttu-id="ae909-111">위협 감지는 보안 전문가가 되거나 고급 보안 모니터링 시스템을 관리할 필요 없이 데이터 웨어하우스에 대한 잠재적인 위협에 간단하게 대처할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae909-111">Threat Detection makes it simple to address potential threats to the data warehouse without the need to be a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="ae909-112">예를 들어 위협 감지는 잠재적인 SQL 삽입 시도를 나타내는 비정상적인 데이터베이스 활동을 감지합니다.</span><span class="sxs-lookup"><span data-stu-id="ae909-112">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="ae909-113">SQL 삽입은 데이터 기반 응용 프로그램 공격에 사용되는 인터넷 상의 일반적인 웹 응용 프로그램 보안 문제 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="ae909-113">SQL injection is one of the common Web application security issues on the Internet, used to attack data-driven applications.</span></span> <span data-ttu-id="ae909-114">공격자는 데이터베이스의 데이터를 침범하거나 수정하기 위해 응용 프로그램의 취약성을 이용하여 악의적인 SQL 문을 응용 프로그램 항목 필드에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="ae909-114">Attackers take advantage of application vulnerabilities to inject malicious SQL statements into application entry fields, for breaching or modifying data in the database.</span></span>

## <a name="set-up-threat-detection-for-your-database"></a><span data-ttu-id="ae909-115">데이터베이스에 대한 위협 감지 설정</span><span class="sxs-lookup"><span data-stu-id="ae909-115">Set up threat detection for your database</span></span>
1. <span data-ttu-id="ae909-116">[https://portal.azure.com](https://portal.azure.com)에서 Azure 포털을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ae909-116">Launch the Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ae909-117">모니터링할 SQL 데이터 웨어하우스의 구성 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ae909-117">Navigate to the configuration blade of the SQL Data Warehouse you want to monitor.</span></span> <span data-ttu-id="ae909-118">설정 블레이드에서 **감사 및 위협 감지**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae909-118">In the Settings blade, select **Auditing & Threat Detection**.</span></span>
   
    ![탐색 창][1]
3. <span data-ttu-id="ae909-120">**감사 및 위협 감지** 구성 블레이드에서 감사를 **켜면** 위협 감지 설정이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae909-120">In the **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display the Threat detection settings.</span></span>
   
    ![탐색 창][2]
4. <span data-ttu-id="ae909-122">위협 감지를 **켭니다**</span><span class="sxs-lookup"><span data-stu-id="ae909-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="ae909-123">비정상적인 데이터 웨어하우스 활동이 감지되는 경우 보안 경고를 수신할 이메일 목록을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ae909-123">Configure the list of emails that will receive security alerts upon detection of anomalous data warehouse activities.</span></span>
6. <span data-ttu-id="ae909-124">**감사 및 위협 감지** 구성 블레이드에서 **저장**을 클릭하여 새로운 또는 업데이트된 감사 및 위협 감지 정책을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ae909-124">Click **Save** in the **Auditing & Threat detection** configuration blade to save the new or updated auditing and threat detection policy.</span></span>
   
    ![탐색 창][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="ae909-126">의심스러운 이벤트 감지 시 비정상적인 데이터 웨어하우스 활동 살펴보기</span><span class="sxs-lookup"><span data-stu-id="ae909-126">Explore anomalous data warehouse activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="ae909-127">비정상적인 데이터베이스 활동이 감지되면 이메일 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae909-127">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="ae909-128">이메일에는 비정상적인 활동의 특징, 데이터베이스 이름, 서버 이름, 이벤트 시간을 포함하여 의심스러운 보안 이벤트에 대한 정보가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae909-128">The email will provide information on the suspicious security event including the nature of the anomalous activities, database name, server name and the event time.</span></span> <span data-ttu-id="ae909-129">또한 가능한 원인에 대한 정보와 데이터베이스에 대한 잠재적인 위협을 조사하고 완화시키기 위해 권장되는 조치가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae909-129">In addition, it will provide information on possible causes and recommended actions to investigate and mitigate the potential threat to the database.</span></span><br/>
   
    ![탐색 창][4]
2. <span data-ttu-id="ae909-131">이메일에서 **Azure SQL 감사 로그** 링크를 클릭하면 Azure 클래식 포털이 열리고 의심스러운 이벤트가 발생한 무렵의 시간에 해당하는 감사 레코드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae909-131">In the email, click on the **Azure SQL Auditing Log** link, which will launch the Azure Classic Portal and show the relevant Auditing records around the time of the suspicious event.</span></span>
   
    ![탐색 창][5]
3. <span data-ttu-id="ae909-133">의심스러운 데이터베이스 활동에 대한 세부 정보(예: SQL 문, 실패 원인, 클라이언트 IP)를 보려면 감사 레코드를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae909-133">Click on the audit records to view more details on the suspicious database activities such as SQL statement, failure reason and client IP.</span></span>
   
    ![탐색 창][6]
4. <span data-ttu-id="ae909-135">미리 구성된 Excel 템플릿을 열고 의심스러운 이벤트가 발생한 무렵의 시간에 대한 감사 로그를 가져와서 심층적인 분석을 실행하려면 감사 레코드 블레이드에서 **Excel에서 열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae909-135">In the Auditing Records blade, click  **Open in Excel** to open a pre-configured excel template to import and run deeper analysis of the audit log around the time of the suspicious event.</span></span><br/><span data-ttu-id="ae909-136">
   **참고:** Excel 2010 이상의 경우 파워 쿼리 및 **빠른 결합** 설정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ae909-136">
**Note:** In Excel 2010 or later, Power Query and the **Fast Combine** setting is required</span></span>
   
    ![탐색 창][7]
5. <span data-ttu-id="ae909-138">**빠른 결합** 설정을 구성하려면 - **파워 쿼리** 리본 탭에서 **옵션**을 선택하여 옵션 대화 상자를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ae909-138">To configure the **Fast Combine** setting - In the **POWER QUERY** ribbon tab, select **Options** to display the Options dialog.</span></span> <span data-ttu-id="ae909-139">개인 정보 섹션을 선택하고 두 번째 옵션 '개인 정보 보호 수준을 무시하고 잠재적으로 성능 향상'을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae909-139">Select the Privacy section and choose the second option - 'Ignore the Privacy Levels and potentially improve performance':</span></span>
   
    ![탐색 창][8]
6. <span data-ttu-id="ae909-141">SQL 감사 로그를 로드하려면, 설정 탭의 매개 변수가 바르게 설정되었는지 확인한 후 '데이터' 리본을 선택하고 '모두 새로 고침' 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae909-141">To load SQL audit logs, ensure that the parameters in the settings tab are set correctly and then select the 'Data' ribbon and click the 'Refresh All' button.</span></span>
   
    ![탐색 창][9]
7. <span data-ttu-id="ae909-143">**SQL 감사 로그** 시트에 결과가 표시되며 사용자는 이를 통해 감지된 비정상적인 활동을 심층적으로 분석하고 응용 프로그램의 보안 이벤트에 대한 영향을 완화시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae909-143">The results appear in the **SQL Audit Logs** sheet which enables you to run deeper analysis of the anomalous activities that were detected, and mitigate the impact of the security event in your application.</span></span>

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-data-warehouse-security-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-data-warehouse-security-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-data-warehouse-security-threat-detection/4_td_email.png
[5]: ./media/sql-data-warehouse-security-threat-detection/5_td_audit_records.png
[6]: ./media/sql-data-warehouse-security-threat-detection/6_td_audit_record_details.png
[7]: ./media/sql-data-warehouse-security-threat-detection/7_td_audit_records_open_excel.png
[8]: ./media/sql-data-warehouse-security-threat-detection/8_td_excel_fast_combine.png
[9]: ./media/sql-data-warehouse-security-threat-detection/9_td_excel_parameters.png
