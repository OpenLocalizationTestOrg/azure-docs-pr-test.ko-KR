---
title: "aaaGet은 SQL 데이터 웨어하우스 위협 검색 시작"
description: "위협 검색 tooget 시작 하는 방법"
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
ms.openlocfilehash: dec0b734849e7f52434e099db0b38fbf0bf6ad53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-threat-detection"></a><span data-ttu-id="e10d8-103">위협 감지 시작</span><span class="sxs-lookup"><span data-stu-id="e10d8-103">Get started with threat detection</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e10d8-104">감사</span><span class="sxs-lookup"><span data-stu-id="e10d8-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="e10d8-105">위협 감지</span><span class="sxs-lookup"><span data-stu-id="e10d8-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="e10d8-106">개요</span><span class="sxs-lookup"><span data-stu-id="e10d8-106">Overview</span></span>
<span data-ttu-id="e10d8-107">위협 검색 잠재적 보안 위협을 toohello 데이터베이스 비정상 데이터베이스 작업을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10d8-107">Threat Detection detects anomalous database activities indicating potential security threats toohello database.</span></span> <span data-ttu-id="e10d8-108">위협 감지는 미리 보기로 제공되며 SQL 데이터 웨어하우스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e10d8-108">Threat Detection is in preview and is supported for SQL Data Warehouse.</span></span>

<span data-ttu-id="e10d8-109">위협 요소 탐지 새 고객 toodetect 있고 비정상적인 활동에서 보안 경고를 제공 하 여 발생 하는 대로 toopotential 위협 응답을 보안 계층을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10d8-109">Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="e10d8-110">사용자가 사용 하 여 hello 의심 스러운 이벤트를 탐색할 수 [Azure SQL 데이터 웨어하우스 감사](sql-data-warehouse-auditing-overview.md) 는 시도 tooaccess에서 발생 한 경우 toodetermine 위반를 주거나 이들을 착취 hello 데이터 웨어하우스의 데이터에서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10d8-110">Users can explore hello suspicious events using [Azure SQL Data Warehouse Auditing](sql-data-warehouse-auditing-overview.md) toodetermine if they result from an attempt tooaccess, breach or exploit data in hello data warehouse.</span></span>
<span data-ttu-id="e10d8-111">위협 요소 탐지 간단한 tooaddress 잠재적 위협 toohello 데이터 보안 전문가 hello 필요 toobe 없이 웨어하우스 또는 시스템 모니터링 하는 고급 보안을 관리 하면 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e10d8-111">Threat Detection makes it simple tooaddress potential threats toohello data warehouse without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="e10d8-112">예를 들어 위협 감지는 잠재적인 SQL 삽입 시도를 나타내는 비정상적인 데이터베이스 활동을 감지합니다.</span><span class="sxs-lookup"><span data-stu-id="e10d8-112">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="e10d8-113">SQL 주입 hello 일반적인 웹 응용 프로그램 보안 문제에 hello 인터넷을 사용 하는 tooattack 데이터 기반 응용 프로그램 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="e10d8-113">SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="e10d8-114">공격자가 활용 응용 프로그램 취약점 tooinject 악의적인 SQL 문을 졌는 지 또는 hello 데이터베이스의 데이터 수정에 대 한 응용 프로그램 입력 필드에 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10d8-114">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, for breaching or modifying data in hello database.</span></span>

## <a name="set-up-threat-detection-for-your-database"></a><span data-ttu-id="e10d8-115">데이터베이스에 대한 위협 감지 설정</span><span class="sxs-lookup"><span data-stu-id="e10d8-115">Set up threat detection for your database</span></span>
1. <span data-ttu-id="e10d8-116">시작 hello Azure 포털에 [https://portal.azure.com](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="e10d8-116">Launch hello Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e10d8-117">SQL 데이터 웨어하우스 toomonitor 원하는 hello의 구성 블레이드에서 toohello 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10d8-117">Navigate toohello configuration blade of hello SQL Data Warehouse you want toomonitor.</span></span> <span data-ttu-id="e10d8-118">Hello 설정 블레이드에서 선택 **감사 및 위협 요소 탐지**합니다.</span><span class="sxs-lookup"><span data-stu-id="e10d8-118">In hello Settings blade, select **Auditing & Threat Detection**.</span></span>
   
    ![탐색 창][1]
3. <span data-ttu-id="e10d8-120">Hello에 **감사 및 위협 요소 탐지** 구성 블레이드 turn **ON** 감사를 위해 표시 하는 hello 위협 검색 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10d8-120">In hello **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display hello Threat detection settings.</span></span>
   
    ![탐색 창][2]
4. <span data-ttu-id="e10d8-122">위협 감지를 **켭니다**</span><span class="sxs-lookup"><span data-stu-id="e10d8-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="e10d8-123">비정상적인 데이터 웨어하우스 작업 검색에 대해 보안 경고를 받을 전자 메일의 hello 목록을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10d8-123">Configure hello list of emails that will receive security alerts upon detection of anomalous data warehouse activities.</span></span>
6. <span data-ttu-id="e10d8-124">클릭 **저장** hello에 **감사 및 위협 검색** 구성 블레이드 toosave hello 신규 또는 업데이트 된 감사 및 위협 검색 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="e10d8-124">Click **Save** in hello **Auditing & Threat detection** configuration blade toosave hello new or updated auditing and threat detection policy.</span></span>
   
    ![탐색 창][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="e10d8-126">의심스러운 이벤트 감지 시 비정상적인 데이터 웨어하우스 활동 살펴보기</span><span class="sxs-lookup"><span data-stu-id="e10d8-126">Explore anomalous data warehouse activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="e10d8-127">비정상적인 데이터베이스 활동이 감지되면 이메일 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e10d8-127">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="e10d8-128">hello 전자 메일 hello 비정상적인 활동, 데이터베이스 이름, 서버 이름 및 hello 이벤트 시간의 hello 특성을 포함 하 여 hello 의심 되는 보안 이벤트를 처리 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10d8-128">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name and hello event time.</span></span> <span data-ttu-id="e10d8-129">또한, 가능한 원인에 정보를 제공 합니다 및 작업 tooinvestigate 권장 하 고 hello 잠재적인 위협 toohello 데이터베이스 완화 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10d8-129">In addition, it will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span><br/>
   
    ![탐색 창][4]
2. <span data-ttu-id="e10d8-131">Hello 전자 메일의 hello에서 클릭 **Azure SQL 감사 로그** 링크를 hello Azure 클래식 포털을 시작 하 고 hello 의심 스러운 이벤트의 hello 시간대 hello 관련 된 감사 레코드가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e10d8-131">In hello email, click on hello **Azure SQL Auditing Log** link, which will launch hello Azure Classic Portal and show hello relevant Auditing records around hello time of hello suspicious event.</span></span>
   
    ![탐색 창][5]
3. <span data-ttu-id="e10d8-133">SQL 문 처럼 hello 데이터베이스 의심 스러운 활동에 대 한 자세한 내용은 hello 감사 레코드 tooview 클릭 실패 이유 및 클라이언트 IP입니다.</span><span class="sxs-lookup"><span data-stu-id="e10d8-133">Click on hello audit records tooview more details on hello suspicious database activities such as SQL statement, failure reason and client IP.</span></span>
   
    ![탐색 창][6]
4. <span data-ttu-id="e10d8-135">Hello 감사 레코드 블레이드에서 클릭 **Excel에서 열기** tooopen 미리 구성 된 excel 서식 파일 tooimport 및 hello 의심 스러운 이벤트의 hello 시간대 hello 감사 로그의 심층 분석을 실행된 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10d8-135">In hello Auditing Records blade, click  **Open in Excel** tooopen a pre-configured excel template tooimport and run deeper analysis of hello audit log around hello time of hello suspicious event.</span></span><br/><span data-ttu-id="e10d8-136">
   **참고:** Excel 2010 또는 나중에 파워 쿼리 및 hello **빠른 결합** 설정은 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="e10d8-136">
**Note:** In Excel 2010 or later, Power Query and hello **Fast Combine** setting is required</span></span>
   
    ![탐색 창][7]
5. <span data-ttu-id="e10d8-138">tooconfigure hello **빠른 결합** hello에 설정- **파워 쿼리** 리본 탭 **옵션** toodisplay hello 옵션 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="e10d8-138">tooconfigure hello **Fast Combine** setting - In hello **POWER QUERY** ribbon tab, select **Options** toodisplay hello Options dialog.</span></span> <span data-ttu-id="e10d8-139">Hello 개인 정보 섹션을 선택 하 고 hello 두 번째 옵션-'hello 개인 정보 수준을 무시 하 고 잠재적으로 성능 향상'를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10d8-139">Select hello Privacy section and choose hello second option - 'Ignore hello Privacy Levels and potentially improve performance':</span></span>
   
    ![탐색 창][8]
6. <span data-ttu-id="e10d8-141">tooload SQL 감사 로그 hello 매개 변수가 확인 hello 설정 탭에서 올바르게 설정 하 고 다음 hello '데이터' 리본 선택 hello ' 모두 새로 고침 ' 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10d8-141">tooload SQL audit logs, ensure that hello parameters in hello settings tab are set correctly and then select hello 'Data' ribbon and click hello 'Refresh All' button.</span></span>
   
    ![탐색 창][9]
7. <span data-ttu-id="e10d8-143">hello에 hello 결과가 표시 **SQL 감사 로그** 시트 발견 되 고 응용 프로그램에서 hello 보안 이벤트의 hello 영향을 완화 하는 hello 비정상적인 활동의 심층 분석 toorun 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e10d8-143">hello results appear in hello **SQL Audit Logs** sheet which enables you toorun deeper analysis of hello anomalous activities that were detected, and mitigate hello impact of hello security event in your application.</span></span>

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
