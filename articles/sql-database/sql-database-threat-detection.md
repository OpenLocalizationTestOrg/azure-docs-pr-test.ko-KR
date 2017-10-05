---
title: "위협 감지 - Azure SQL Database | Microsoft Docs"
description: "위협 감지는 데이터베이스에 대한 잠재적인 보안 위협을 나타내는 비정상적인 데이터베이스 활동을 감지합니다."
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
ms.openlocfilehash: bd3de9ed0131edc683763b0fe7f4a2ae74533944
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="sql-database-threat-detection"></a><span data-ttu-id="a0b31-103">SQL Database 위협 감지</span><span class="sxs-lookup"><span data-stu-id="a0b31-103">SQL Database Threat Detection</span></span>

<span data-ttu-id="a0b31-104">SQL 위협 감지는 데이터베이스를 액세스하거나 악용하려는 비정상적이고 잠재적으로 해로운 시도를 나타내는 비정상적인 활동을 감지합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b31-104">SQL Threat Detection detects anomalous activities indicating unusual and potentially harmful attempts to access or exploit databases.</span></span>

## <a name="overview"></a><span data-ttu-id="a0b31-105">개요</span><span class="sxs-lookup"><span data-stu-id="a0b31-105">Overview</span></span>

<span data-ttu-id="a0b31-106">SQL 위협 감지는 비정상적인 활동에 대한 보안 경고를 제공하여 잠재적인 위협이 발생하면 고객이 이를 감지하고 대응할 수 있도록 하는 새로운 차원의 보안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b31-106">SQL Threat Detection provides a new layer of security, which enables customers to detect and respond to potential threats as they occur by providing security alerts on anomalous activities.</span></span>  <span data-ttu-id="a0b31-107">사용자는 의심스러운 데이터베이스 활동, 잠재적 취약성 및 SQL 삽입 공격은 물론 비정상적인 데이터베이스 액세스 패턴에 대한 경고를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0b31-107">Users will receive an alert upon suspicious database activities, potential vulnerabilities, and SQL injection attacks, as well as anomalous database access patterns.</span></span> <span data-ttu-id="a0b31-108">SQL 위협 감지 경고는 의심스러운 활동에 대한 세부 정보 제공하고 위협을 조사하고 완화하는 방법에 대한 조치를 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b31-108">SQL Threat Detection alerts provide details of suspicious activity and recommend action on how to investigate and mitigate the threat.</span></span> <span data-ttu-id="a0b31-109">사용자는 데이터베이스의 데이터를 액세스, 침범 또는 악용하려는 시도로 인해 의심스러운 이벤트가 발생했는지를 판단하기 위해서 [SQL Database 감사](sql-database-auditing.md)를 사용하여 의심스러운 이벤트를 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b31-109">Users can explore the suspicious events using [SQL Database Auditing](sql-database-auditing.md) to determine if they result from an attempt to access, breach, or exploit data in the database.</span></span> <span data-ttu-id="a0b31-110">위협 감지는 보안 전문가가 되거나 고급 보안 모니터링 시스템을 관리할 필요 없이 데이터베이스에 대한 잠재적인 위협에 간단하게 대처할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b31-110">Threat Detection makes it simple to address potential threats to the database without the need to be a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="a0b31-111">예를 들어 SQL 삽입은 데이터 기반 응용 프로그램 공격에 사용되는 인터넷 상의 일반적인 웹 응용 프로그램 보안 문제 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="a0b31-111">For example, SQL injection is one of the common Web application security issues on the Internet, used to attack data-driven applications.</span></span> <span data-ttu-id="a0b31-112">공격자는 응용 프로그램의 취약성을 이용하여 악의적인 SQL 문을 응용 프로그램 항목 필드에 삽입하고 데이터베이스의 데이터를 침범하거나 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b31-112">Attackers take advantage of application vulnerabilities to inject malicious SQL statements into application entry fields, breaching or modifying data in the database.</span></span>

<span data-ttu-id="a0b31-113">SQL 위협 감지는 [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/)와 경고를 통합하며 보호되는 각 SQL Database 서버는 Azure Security Center 표준 계층과 동일한 가격($15/노드/월, 여기서 보호되는 각 SQL Database 서버를 하나의 노드로 계산)으로 비용이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0b31-113">SQL Threat Detection integrates alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/), and, each protected SQL Database server will be billed at the same price as Azure Security Center Standard tier, at $15/node/month, where each protected SQL Database server is counted as one node.</span></span> <span data-ttu-id="a0b31-114">이 서비스를 60일 동안 체험해 보세요.</span><span class="sxs-lookup"><span data-stu-id="a0b31-114">We invite you to try it out for 60 days for free.</span></span> 

## <a name="set-up-threat-detection-for-your-database-in-the-azure-portal"></a><span data-ttu-id="a0b31-115">Azure Portal에서 데이터베이스에 대한 위협 검색 설정</span><span class="sxs-lookup"><span data-stu-id="a0b31-115">Set up threat detection for your database in the Azure portal</span></span>
1. <span data-ttu-id="a0b31-116">[https://portal.azure.com](https://portal.azure.com)에서 Azure Portal을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b31-116">Launch the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a0b31-117">모니터링할 SQL Database의 구성 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b31-117">Navigate to the configuration blade of the SQL Database you want to monitor.</span></span> <span data-ttu-id="a0b31-118">설정 블레이드에서 **감사 및 위협 감지**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b31-118">In the Settings blade, select **Auditing & Threat Detection**.</span></span> 
    <span data-ttu-id="a0b31-119">![탐색 창][1]</span><span class="sxs-lookup"><span data-stu-id="a0b31-119">![Navigation pane][1]</span></span>
3. <span data-ttu-id="a0b31-120">**감사 및 위협 감지** 구성 블레이드에서 감사를 **켜면** 위협 감지 설정이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0b31-120">In the **Auditing & Threat Detection** configuration blade turn **ON** Auditing, which will display the threat detection settings.</span></span>
  
    ![탐색 창][2]
4. <span data-ttu-id="a0b31-122">위협 감지를 **켭니다**</span><span class="sxs-lookup"><span data-stu-id="a0b31-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="a0b31-123">비정상적인 데이터베이스 활동이 감지되는 경우 보안 경고를 수신할 이메일 목록을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b31-123">Configure the list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>
6. <span data-ttu-id="a0b31-124">**감사 및 위협 감지** 블레이드에서 **저장**을 클릭하여 새로운 또는 업데이트된 감사 및 위협 감지 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b31-124">Click **Save** in the **Auditing & Threat detection** blade to save the new or updated auditing and threat detection settings.</span></span>
       
    ![탐색 창][3]

## <a name="set-up-threat-detection-using-powershell"></a><span data-ttu-id="a0b31-126">PowerShell을 사용하여 위협 감지 설정</span><span class="sxs-lookup"><span data-stu-id="a0b31-126">Set up threat detection using PowerShell</span></span>

<span data-ttu-id="a0b31-127">스크립트 예제는 [PowerShell을 사용하여 감사 및 위협 감지 구성](scripts/sql-database-auditing-and-threat-detection-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0b31-127">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

## <a name="explore-anomalous-database-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="a0b31-128">의심스러운 이벤트 감지 시 비정상적인 데이터베이스 활동 살펴보기</span><span class="sxs-lookup"><span data-stu-id="a0b31-128">Explore anomalous database activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="a0b31-129">비정상적인 데이터베이스 활동이 감지되면 이메일 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0b31-129">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="a0b31-130">전자 메일에는 비정상적인 활동의 특징, 데이터베이스 이름, 서버 이름, 응용 프로그램 이름, 이벤트 시간을 비롯한 의심스러운 보안 이벤트에 대한 정보가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0b31-130">The email will provide information on the suspicious security event including the nature of the anomalous activities, database name, server name, application name, and the event time.</span></span> <span data-ttu-id="a0b31-131">또한 전자 메일에는 가능한 원인에 대한 정보 및 데이터베이스에 대한 잠재적인 위협을 조사하고 완화시키기 위해 권장되는 조치가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0b31-131">In addition, the email will provide information on possible causes and recommended actions to investigate and mitigate the potential threat to the database.</span></span><br/>
     
    ![탐색 창][4]
2. <span data-ttu-id="a0b31-133">전자 메일 경고에는 SQL 감사 로그에 대한 직접 링크가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0b31-133">The email alert includes a direct link to the SQL Audit log.</span></span> <span data-ttu-id="a0b31-134">이 링크를 클릭하면 Azure Portal이 열리고 의심스러운 이벤트가 발생한 시점의 SQL 감사 레코드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a0b31-134">Clicking on this link launches the Azure portal and opens the SQL Audit records around the time of the suspicious event.</span></span> <span data-ttu-id="a0b31-135">의심스러운 데이터베이스 활동에 대한 자세한 내용을 보려면 감사 레코드를 클릭하여 실행된 SQL 문을 더 쉽게 찾아서(액세스한 사람, 수행한 작업 및 수행 시기) 이벤트가 합법적인지 또는 악의적인지(예: SQL 삽입에 대한 응용 프로그램 취약점이 악용되어 누군가가 중요한 데이터를 침범했는지 등)를 판단하세요.</span><span class="sxs-lookup"><span data-stu-id="a0b31-135">Click on an audit record to view more details on the suspicious database activities, making it easier to find the SQL statements that were executed (who accessed, what they did and when) and determine if the event was legitimate or malicious (e.g. application vulnerability to SQL injection was exploited, someone breached sensitive data, etc.).</span></span><br/><span data-ttu-id="a0b31-136">
   ![탐색 창][5]</span><span class="sxs-lookup"><span data-stu-id="a0b31-136">
![Navigation pane][5]</span></span>


## <a name="explore-threat-detection-alerts-for-your-database-in-the-azure-portal"></a><span data-ttu-id="a0b31-137">Azure Portal에서 데이터베이스에 대한 위협 감지 경고 탐색</span><span class="sxs-lookup"><span data-stu-id="a0b31-137">Explore threat detection alerts for your database in the Azure portal</span></span>

<span data-ttu-id="a0b31-138">SQL Database 위협 감지는 경고를 [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/)와 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b31-138">SQL Database Threat Detection integrates its alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/).</span></span> <span data-ttu-id="a0b31-139">Azure Portal의 데이터베이스 블레이드 내 실제 SQL 보안 타일은 활성 위협의 상태를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b31-139">A live SQL security tile within the database blade in the Azure portal tracks the status of active threats.</span></span> 

   ![탐색 창][6]
   
1. <span data-ttu-id="a0b31-141">SQL 보안 타일을 클릭하면 Azure Security Center 경고 블레이드가 시작되고 데이터베이스에서 감지된 활성 SQL 위협에 대한 개요가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0b31-141">Clicking on the SQL security tile launches the Azure Security Center alerts blade and provides an overview of active SQL threats detected on the database.</span></span> 

  ![탐색 창][7]

2. <span data-ttu-id="a0b31-143">특정 경고를 클릭하면 이 위협을 조사하고 향후 위협을 수정하기 위한 추가 세부 정보 및 조치가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0b31-143">Clicking on a specific alert provides additional details and actions for investigating this threat and remediating future threats.</span></span>

  ![탐색 창][8]


## <a name="next-steps"></a><span data-ttu-id="a0b31-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a0b31-145">Next steps</span></span>

* <span data-ttu-id="a0b31-146">위협 감지에 대해 자세히 알아보려면 [Azure 블로그](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0b31-146">Learn more about Threat Detection, visit the [Azure blog](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span></span> 
* <span data-ttu-id="a0b31-147">[Azure SQL Database 감사](sql-database-auditing.md)에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="a0b31-147">Learn more about [Azure SQL Database Auditing](sql-database-auditing.md)</span></span>
* <span data-ttu-id="a0b31-148">[Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="a0b31-148">Learn more about [Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span></span>
* <span data-ttu-id="a0b31-149">가격 책정에 대한 자세한 내용은 [SQL Database 가격 책정 페이지](https://azure.microsoft.com/en-us/pricing/details/sql-database/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0b31-149">For more details on pricing, please see the [SQL Database Pricing page](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span></span>  
* <span data-ttu-id="a0b31-150">PowerShell 스크립트 예제는 [PowerShell을 사용하여 감사 및 위협 감지 구성](scripts/sql-database-auditing-and-threat-detection-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0b31-150">For a PowerShell script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md)</span></span>



<!--Image references-->
[1]: ./media/sql-database-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-database-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-database-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-database-threat-detection/4_td_email.png
[5]: ./media/sql-database-threat-detection/5_td_audit_record_details.png
[6]: ./media/sql-database-threat-detection/6_td_security_tile_view_alerts.png
[7]: ./media/sql-database-threat-detection/7_td_SQL_security_alerts_list.png
[8]: ./media/sql-database-threat-detection/8_td_SQL_security_alert_details.png


