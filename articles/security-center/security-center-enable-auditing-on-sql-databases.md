---
title: "Azure Security Center에서 SQL Database에 대한 감사 및 위협 감지 사용 | Microsoft Docs"
description: "이 문서는 Azure 보안 센터 권장 구성을 구현 하는 방법을 보여줍니다. * * SQL 데이터베이스 * *에 감사 및 위협 검색을 사용 합니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 224b6755-2b36-4ecd-9af8-139a198e0df1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: 8f4febdaa4497fee0dc690b59cd6eaa415c5e5cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-databases-in-azure-security-center"></a><span data-ttu-id="4b231-103">Azure Security Center에서 SQL Database에 대한 감사 및 위협 감지 사용</span><span class="sxs-lookup"><span data-stu-id="4b231-103">Enable auditing and threat detection on SQL databases in Azure Security Center</span></span>
<span data-ttu-id="4b231-104">감사 및 위협 감지를 아직 사용하도록 설정하지 않은 경우 모든 SQL 데이터베이스에 대한 감사 및 위협 감지를 켜는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4b231-104">Azure Security Center will recommend that you turn on auditing and threat detection for all SQL databases if auditing and threat detection is not already enabled.</span></span> <span data-ttu-id="4b231-105">감사 및 위협 감지는 규정 준수를 유지 관리하고, 데이터베이스 작업을 이해하고, 비즈니스 문제나 의심스러운 보안 위반을 나타낼 수 있는 불일치 및 이상 활동을 파악하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b231-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="4b231-106">감사를 설정한 후에는 보안 경고를 받을 수 있도록 위협 검색 설정 및 전자 메일을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b231-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails to receive security alerts.</span></span> <span data-ttu-id="4b231-107">위협 감지는 데이터베이스에 대한 잠재적인 보안 위협을 나타내는 비정상적인 데이터베이스 활동을 감지합니다.</span><span class="sxs-lookup"><span data-stu-id="4b231-107">Threat Detection detects anomalous database activities indicating potential security threats to the database.</span></span> <span data-ttu-id="4b231-108">이렇게 하면 잠재적인 위협 요소가 발생할 때 검색하고 대처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b231-108">This enables you to detect and respond to potential threats as they occur.</span></span>

<span data-ttu-id="4b231-109">이러한 권장 지침은 Azure SQL 서비스에만 적용되며 가상 컴퓨터에서 실행되는 SQL은 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4b231-109">This recommendation applies to the Azure SQL service only; it doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="4b231-110">이 문서에서는 배포 예제를 사용하여 서비스를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="4b231-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="4b231-111">단계별 가이드는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="4b231-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="4b231-112">권장 사항 구현</span><span class="sxs-lookup"><span data-stu-id="4b231-112">Implement the recommendation</span></span>
1. <span data-ttu-id="4b231-113">**권장 사항** 블레이드에서 **SQL Database에 감사 및 위협 감지 활성화**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b231-113">In the **Recommendations** blade, select **Enable Auditing & Threat detection on SQL databases**.</span></span>  <span data-ttu-id="4b231-114">이렇게 하면 **SQL 데이터베이스에 감사 및 위협 감지 활성화** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="4b231-114">This opens the **Enable Auditing & Threat detection on SQL databases** blade.</span></span>

   ![SQL 데이터베이스에 감사 활성화][1]
2. <span data-ttu-id="4b231-116">감사를 사용하도록 설정할 SQL 데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b231-116">Select a SQL database to enable auditing on.</span></span> <span data-ttu-id="4b231-117">그러면 **감사 및 위협 감지** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="4b231-117">This opens the **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="4b231-118">**감사 및 위협 감지** 블레이드의 **감사**에서 **켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b231-118">On the **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![감사 및 위협 감지 켜기][2]
4. <span data-ttu-id="4b231-120">[Azure Portal에서 SQL Database 위협 감지](../sql-database/sql-database-threat-detection-portal.md)의 단계에 따라 위협 감지를 켜고 구성하며, 비정상적인 활동이 검색될 때 보안 경고가 수신되는 전자 메일 목록을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b231-120">Follow the steps in [SQL Database Threat Detection in the Azure portal](../sql-database/sql-database-threat-detection-portal.md) to turn on and configure Threat Detection and to configure the list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="4b231-121">참고 항목</span><span class="sxs-lookup"><span data-stu-id="4b231-121">See also</span></span>
<span data-ttu-id="4b231-122">이 문서에서는 보안 센터 권장 사항 "SQL 데이터베이스에 감사 및 위협 감지 활성화"를 구현하는 방법을 보여 주었습니다.</span><span class="sxs-lookup"><span data-stu-id="4b231-122">This article showed you how to implement the Security Center recommendation "Enable Auditing & Threat detection on SQL databases."</span></span> <span data-ttu-id="4b231-123">SQL 데이터베이스 보안 유지에 대해 자세히 알아보려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b231-123">To learn more about securing your SQL database, see the following:</span></span>

* [<span data-ttu-id="4b231-124">SQL 데이터베이스 보안 설정</span><span class="sxs-lookup"><span data-stu-id="4b231-124">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="4b231-125">보안 센터에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b231-125">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="4b231-126">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -- Azure 구독 및 리소스 그룹에 대해 보안 정책을 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4b231-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="4b231-127">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4b231-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="4b231-128">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) –- Azure 리소스의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4b231-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="4b231-129">[Azure 보안 센터에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md) -- 보안 경고를 관리하고 대응하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4b231-129">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="4b231-130">[Azure 보안 센터를 사용하여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -- 파트너 솔루션의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4b231-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="4b231-131">[Azure 보안 센터 FAQ](security-center-faq.md) -- 서비스 사용에 관한 질문과 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4b231-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="4b231-132">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -- 최신 Azure 보안 뉴스 및 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4b231-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-databases/enable-auditing-on-sql-databases.png
[2]: ./media/security-center-enable-auditing-on-sql-databases/auditing-threat-detection-blade.png
