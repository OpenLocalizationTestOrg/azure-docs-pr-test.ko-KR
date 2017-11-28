---
title: "aaaThreat 검색-Azure SQL 데이터베이스 | Microsoft Docs"
description: "위협 검색 잠재적 보안 위협을 toohello 데이터베이스 비정상 데이터베이스 작업을 검색 합니다."
services: sql-database
documentationcenter: 
author: rmatchoro
manager: jhubbard
editor: v-romcal
ms.assetid: b50d232a-4225-46ed-91e7-75288f55ee84
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/19/2017
ms.author: ronmat; ronitr
ms.openlocfilehash: 0879d20eff515a4e69358b5a98ceccf57fbd0ea2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-threat-detection"></a><span data-ttu-id="59b3e-103">SQL Database 위협 감지</span><span class="sxs-lookup"><span data-stu-id="59b3e-103">SQL Database Threat Detection</span></span>

<span data-ttu-id="59b3e-104">SQL 위협 요소 탐지 한 잠재적으로 위험한 시도 tooaccess 또는 악용 데이터베이스 비정상적인 작업을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b3e-104">SQL Threat Detection detects anomalous activities indicating unusual and potentially harmful attempts tooaccess or exploit databases.</span></span>

## <a name="overview"></a><span data-ttu-id="59b3e-105">개요</span><span class="sxs-lookup"><span data-stu-id="59b3e-105">Overview</span></span>

<span data-ttu-id="59b3e-106">SQL 위협 요소 탐지 새 고객 toodetect 있고 비정상적인 활동에서 보안 경고를 제공 하 여 발생 하는 대로 toopotential 위협 응답을 보안 계층을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b3e-106">SQL Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span>  <span data-ttu-id="59b3e-107">사용자는 의심스러운 데이터베이스 활동, 잠재적 취약성 및 SQL 삽입 공격은 물론 비정상적인 데이터베이스 액세스 패턴에 대한 경고를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59b3e-107">Users will receive an alert upon suspicious database activities, potential vulnerabilities, and SQL injection attacks, as well as anomalous database access patterns.</span></span> <span data-ttu-id="59b3e-108">SQL 위협 요소 탐지 경고의 의심 스러운 활동 세부 정보를 제공 및 방법에 대 한 작업을 권장 tooinvestigate hello 위협을 완화 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b3e-108">SQL Threat Detection alerts provide details of suspicious activity and recommend action on how tooinvestigate and mitigate hello threat.</span></span> <span data-ttu-id="59b3e-109">사용자가 사용 하 여 hello 의심 스러운 이벤트를 탐색할 수 [SQL 데이터베이스 감사](sql-database-auditing.md) 는 시도 tooaccess에서 발생 한 경우 toodetermine 위반를 주거나 이들을 착취 hello 데이터베이스의에서 데이터.</span><span class="sxs-lookup"><span data-stu-id="59b3e-109">Users can explore hello suspicious events using [SQL Database Auditing](sql-database-auditing.md) toodetermine if they result from an attempt tooaccess, breach, or exploit data in hello database.</span></span> <span data-ttu-id="59b3e-110">위협 요소 탐지 하면 간단한 tooaddress 잠재적인 위협 toohello 데이터베이스 없이 hello 필요 toobe 보안 전문가 또는 시스템 모니터링 하는 고급 보안을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b3e-110">Threat Detection makes it simple tooaddress potential threats toohello database without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="59b3e-111">예를 들어 SQL 주입 hello 일반적인 웹 응용 프로그램 보안 문제에 hello 인터넷을 사용 하는 tooattack 데이터 기반 응용 프로그램 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="59b3e-111">For example, SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="59b3e-112">공격자가 활용 응용 프로그램 취약점 tooinject 악의적인 SQL 문을 응용 프로그램 입력 필드에 졌는 지 또는 hello 데이터베이스에서 데이터를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b3e-112">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, breaching or modifying data in hello database.</span></span>

<span data-ttu-id="59b3e-113">경고를 통합 하는 SQL 위협 요소 탐지 [Azure 보안 센터](https://azure.microsoft.com/en-us/services/security-center/), 이며 각 보호 된 SQL 데이터베이스 서버 hello 동일 가격에서 $15/노드/월, SQL 보호 된 각 위치에서 Azure 보안 센터 표준 계층으로 청구 됩니다 데이터베이스 서버는 하나의 노드만으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59b3e-113">SQL Threat Detection integrates alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/), and, each protected SQL Database server will be billed at hello same price as Azure Security Center Standard tier, at $15/node/month, where each protected SQL Database server is counted as one node.</span></span> <span data-ttu-id="59b3e-114">Tootry 초대 아웃에 대 한 일 동안 무료로 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b3e-114">We invite you tootry it out for 60 days for free.</span></span> 

## <a name="set-up-threat-detection-for-your-database-in-hello-azure-portal"></a><span data-ttu-id="59b3e-115">위협 요소 탐지 hello Azure 포털에서에서 데이터베이스에 대 한 설정</span><span class="sxs-lookup"><span data-stu-id="59b3e-115">Set up threat detection for your database in hello Azure portal</span></span>
1. <span data-ttu-id="59b3e-116">시작 hello Azure 포털에서 [https://portal.azure.com](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="59b3e-116">Launch hello Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="59b3e-117">Hello toomonitor 사용할 SQL 데이터베이스의 구성 블레이드에서 toohello 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b3e-117">Navigate toohello configuration blade of hello SQL Database you want toomonitor.</span></span> <span data-ttu-id="59b3e-118">Hello 설정 블레이드에서 선택 **감사 및 위협 요소 탐지**합니다.</span><span class="sxs-lookup"><span data-stu-id="59b3e-118">In hello Settings blade, select **Auditing & Threat Detection**.</span></span> 
    <span data-ttu-id="59b3e-119">![탐색 창][1]</span><span class="sxs-lookup"><span data-stu-id="59b3e-119">![Navigation pane][1]</span></span>
3. <span data-ttu-id="59b3e-120">Hello에 **감사 및 위협 요소 탐지** 구성 블레이드 turn **ON** 감사 hello 위협 검색 설정이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59b3e-120">In hello **Auditing & Threat Detection** configuration blade turn **ON** Auditing, which will display hello threat detection settings.</span></span>
  
    ![탐색 창][2]
4. <span data-ttu-id="59b3e-122">위협 감지를 **켭니다**</span><span class="sxs-lookup"><span data-stu-id="59b3e-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="59b3e-123">검색 비정상 데이터베이스 작업에 대해 보안 경고를 받을 전자 메일의 hello 목록을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b3e-123">Configure hello list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>
6. <span data-ttu-id="59b3e-124">클릭 **저장** hello에 **감사 및 위협 검색** 블레이드 toosave hello 신규 또는 업데이트 된 감사 및 위협 검색 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b3e-124">Click **Save** in hello **Auditing & Threat detection** blade toosave hello new or updated auditing and threat detection settings.</span></span>
       
    ![탐색 창][3]

## <a name="set-up-threat-detection-using-powershell"></a><span data-ttu-id="59b3e-126">PowerShell을 사용하여 위협 감지 설정</span><span class="sxs-lookup"><span data-stu-id="59b3e-126">Set up threat detection using PowerShell</span></span>

<span data-ttu-id="59b3e-127">스크립트 예제는 [PowerShell을 사용하여 감사 및 위협 감지 구성](scripts/sql-database-auditing-and-threat-detection-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59b3e-127">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

## <a name="explore-anomalous-database-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="59b3e-128">의심스러운 이벤트 감지 시 비정상적인 데이터베이스 활동 살펴보기</span><span class="sxs-lookup"><span data-stu-id="59b3e-128">Explore anomalous database activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="59b3e-129">비정상적인 데이터베이스 활동이 감지되면 이메일 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59b3e-129">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="59b3e-130">hello 전자 메일 hello 비정상적인 활동, 데이터베이스 이름, 서버 이름, 응용 프로그램 이름 및 hello 이벤트 시간의 hello 특성을 포함 하 여 hello 의심 되는 보안 이벤트를 처리 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b3e-130">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name, application name, and hello event time.</span></span> <span data-ttu-id="59b3e-131">또한 hello 전자 메일 가능한 원인에 정보를 제공 합니다 및 권장 동작 tooinvestigate 않으며 hello 잠재적인 위협 toohello 데이터베이스 완화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59b3e-131">In addition, hello email will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span><br/>
     
    ![탐색 창][4]
2. <span data-ttu-id="59b3e-133">hello 전자 메일 경고는 직접 링크 toohello SQL 감사 로그를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b3e-133">hello email alert includes a direct link toohello SQL Audit log.</span></span> <span data-ttu-id="59b3e-134">Azure 포털 및 열립니다 hello SQL 감사 레코드 hello 의심 스러운 이벤트의 hello 시간대이 링크를 실행 하는 hello를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59b3e-134">Clicking on this link launches hello Azure portal and opens hello SQL Audit records around hello time of hello suspicious event.</span></span> <span data-ttu-id="59b3e-135">실행 된 toofind hello SQL 문을 쉽게 만드는 hello 의심 스러운 데이터베이스 작업에 대 한 자세한 내용은 감사 레코드 tooview 클릭 (액세스 한 사용자, 했다는 것 언제) hello 이벤트 올 바르 거 나 악성 했는지 확인 하 고 (예: 응용 프로그램 tooSQL 주입 취약점을 악용, 등 중요 한 데이터 위반 하는 다른 사용자).</span><span class="sxs-lookup"><span data-stu-id="59b3e-135">Click on an audit record tooview more details on hello suspicious database activities, making it easier toofind hello SQL statements that were executed (who accessed, what they did and when) and determine if hello event was legitimate or malicious (e.g. application vulnerability tooSQL injection was exploited, someone breached sensitive data, etc.).</span></span><br/><span data-ttu-id="59b3e-136">
   ![탐색 창][5]</span><span class="sxs-lookup"><span data-stu-id="59b3e-136">
![Navigation pane][5]</span></span>


## <a name="explore-threat-detection-alerts-for-your-database-in-hello-azure-portal"></a><span data-ttu-id="59b3e-137">탐색 hello Azure 포털에서에서 데이터베이스에 대 한 위협을 감지 경고</span><span class="sxs-lookup"><span data-stu-id="59b3e-137">Explore threat detection alerts for your database in hello Azure portal</span></span>

<span data-ttu-id="59b3e-138">SQL Database 위협 감지는 경고를 [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/)와 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="59b3e-138">SQL Database Threat Detection integrates its alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/).</span></span> <span data-ttu-id="59b3e-139">내에서 발생 하는 위협 상태의 Azure 포털 트랙 hello hello hello 데이터베이스 블레이드 라이브 SQL 보안 타일입니다.</span><span class="sxs-lookup"><span data-stu-id="59b3e-139">A live SQL security tile within hello database blade in hello Azure portal tracks hello status of active threats.</span></span> 

   ![탐색 창][6]
   
1. <span data-ttu-id="59b3e-141">Hello SQL 보안 타일을 클릭 하면 hello Azure 보안 센터 경고 블레이드를 시작 하 고 활성 SQL 위협이 hello 데이터베이스에서 검색의 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b3e-141">Clicking on hello SQL security tile launches hello Azure Security Center alerts blade and provides an overview of active SQL threats detected on hello database.</span></span> 

  ![탐색 창][7]

2. <span data-ttu-id="59b3e-143">특정 경고를 클릭하면 이 위협을 조사하고 향후 위협을 수정하기 위한 추가 세부 정보 및 조치가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="59b3e-143">Clicking on a specific alert provides additional details and actions for investigating this threat and remediating future threats.</span></span>

  ![탐색 창][8]


## <a name="next-steps"></a><span data-ttu-id="59b3e-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="59b3e-145">Next steps</span></span>

* <span data-ttu-id="59b3e-146">위협 요소 탐지에 대 한 자세한 정보, hello 방문 [Azure 블로그](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span><span class="sxs-lookup"><span data-stu-id="59b3e-146">Learn more about Threat Detection, visit hello [Azure blog](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span></span> 
* <span data-ttu-id="59b3e-147">[Azure SQL Database 감사](sql-database-auditing.md)에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="59b3e-147">Learn more about [Azure SQL Database Auditing](sql-database-auditing.md)</span></span>
* <span data-ttu-id="59b3e-148">[Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="59b3e-148">Learn more about [Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span></span>
* <span data-ttu-id="59b3e-149">가격 책정에 대 한 자세한 내용은 hello를 참조 하십시오 [SQL 데이터베이스 가격 페이지](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span><span class="sxs-lookup"><span data-stu-id="59b3e-149">For more details on pricing, please see hello [SQL Database Pricing page](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span></span>  
* <span data-ttu-id="59b3e-150">PowerShell 스크립트 예제는 [PowerShell을 사용하여 감사 및 위협 감지 구성](scripts/sql-database-auditing-and-threat-detection-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59b3e-150">For a PowerShell script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md)</span></span>



<!--Image references-->
[1]: ./media/sql-database-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-database-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-database-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-database-threat-detection/4_td_email.png
[5]: ./media/sql-database-threat-detection/5_td_audit_record_details.png
[6]: ./media/sql-database-threat-detection/6_td_security_tile_view_alerts.png
[7]: ./media/sql-database-threat-detection/7_td_SQL_security_alerts_list.png
[8]: ./media/sql-database-threat-detection/8_td_SQL_security_alert_details.png


