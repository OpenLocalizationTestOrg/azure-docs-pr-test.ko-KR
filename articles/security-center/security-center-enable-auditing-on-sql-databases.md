---
title: "SQL에서 aaaEnable 감사 및 위협 감지 Azure 보안 센터에서 데이터베이스 | Microsoft Docs"
description: "이 문서에서는 어떻게 tooimplement hello Azure 보안 센터 권장 * * SQL 데이터베이스 * *에 감사 및 위협 검색을 사용 합니다."
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
ms.openlocfilehash: c94140acf37cabaca3e681ba5db79d6827e7b9db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-databases-in-azure-security-center"></a><span data-ttu-id="adb45-103">Azure Security Center에서 SQL Database에 대한 감사 및 위협 감지 사용</span><span class="sxs-lookup"><span data-stu-id="adb45-103">Enable auditing and threat detection on SQL databases in Azure Security Center</span></span>
<span data-ttu-id="adb45-104">감사 및 위협 감지를 아직 사용하도록 설정하지 않은 경우 모든 SQL 데이터베이스에 대한 감사 및 위협 감지를 켜는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="adb45-104">Azure Security Center will recommend that you turn on auditing and threat detection for all SQL databases if auditing and threat detection is not already enabled.</span></span> <span data-ttu-id="adb45-105">감사 및 위협 감지는 규정 준수를 유지 관리하고, 데이터베이스 작업을 이해하고, 비즈니스 문제나 의심스러운 보안 위반을 나타낼 수 있는 불일치 및 이상 활동을 파악하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adb45-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="adb45-106">감사를 설정한 후에 위협 요소 탐지 설정 및 전자 메일 tooreceive 보안 경고를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adb45-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails tooreceive security alerts.</span></span> <span data-ttu-id="adb45-107">위협 검색 잠재적 보안 위협을 toohello 데이터베이스 비정상 데이터베이스 작업을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="adb45-107">Threat Detection detects anomalous database activities indicating potential security threats toohello database.</span></span> <span data-ttu-id="adb45-108">이 toodetect 있으며 나타나는 순서 대로 toopotential 위협에 대응 합니다.</span><span class="sxs-lookup"><span data-stu-id="adb45-108">This enables you toodetect and respond toopotential threats as they occur.</span></span>

<span data-ttu-id="adb45-109">이 권장 사항은 적용 toohello Azure SQL 서비스에만 사용 합니다. 가상 컴퓨터에서 실행 되는 SQL 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="adb45-109">This recommendation applies toohello Azure SQL service only; it doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="adb45-110">이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="adb45-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="adb45-111">단계별 가이드는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="adb45-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="adb45-112">Hello 권장 구성 구현</span><span class="sxs-lookup"><span data-stu-id="adb45-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="adb45-113">Hello에 **권장 사항을** 블레이드를 **SQL 데이터베이스에서 감사를 사용 하도록 설정 및 위협 검색**합니다.</span><span class="sxs-lookup"><span data-stu-id="adb45-113">In hello **Recommendations** blade, select **Enable Auditing & Threat detection on SQL databases**.</span></span>  <span data-ttu-id="adb45-114">Hello 열립니다 **SQL 데이터베이스에서 감사를 사용 하도록 설정 및 위협 검색** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="adb45-114">This opens hello **Enable Auditing & Threat detection on SQL databases** blade.</span></span>

   ![SQL 데이터베이스에 감사 활성화][1]
2. <span data-ttu-id="adb45-116">SQL 데이터베이스 tooenable에 대 한 감사를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="adb45-116">Select a SQL database tooenable auditing on.</span></span> <span data-ttu-id="adb45-117">Hello 열립니다 **감사 및 위협 요소 탐지** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="adb45-117">This opens hello **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="adb45-118">Hello에 **감사 및 위협 요소 탐지** 블레이드를 **ON** 아래 **감사**합니다.</span><span class="sxs-lookup"><span data-stu-id="adb45-118">On hello **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![감사 및 위협 감지 켜기][2]
4. <span data-ttu-id="adb45-120">Hello 단계에 따라 [hello Azure 포털에서에서 SQL 데이터베이스 위협 검색](../sql-database/sql-database-threat-detection-portal.md) tooturn에 위협 요소 탐지와 tooconfigure hello 목록 검색 비정상적인 활동에 대해 보안 경고를 받을 전자 메일 주소 및 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="adb45-120">Follow hello steps in [SQL Database Threat Detection in hello Azure portal](../sql-database/sql-database-threat-detection-portal.md) tooturn on and configure Threat Detection and tooconfigure hello list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="adb45-121">참고 항목</span><span class="sxs-lookup"><span data-stu-id="adb45-121">See also</span></span>
<span data-ttu-id="adb45-122">이 문서에 설명 했습니다 어떻게 tooimplement hello 보안 센터 권장 사항 사용 감사 및 위협 검색"SQL 데이터베이스에 대."</span><span class="sxs-lookup"><span data-stu-id="adb45-122">This article showed you how tooimplement hello Security Center recommendation "Enable Auditing & Threat detection on SQL databases."</span></span> <span data-ttu-id="adb45-123">SQL 데이터베이스를 보호에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="adb45-123">toolearn more about securing your SQL database, see hello following:</span></span>

* [<span data-ttu-id="adb45-124">SQL 데이터베이스 보안 설정</span><span class="sxs-lookup"><span data-stu-id="adb45-124">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="adb45-125">보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="adb45-125">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="adb45-126">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -자세한 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="adb45-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="adb45-127">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="adb45-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="adb45-128">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="adb45-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="adb45-129">[Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="adb45-129">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="adb45-130">[Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="adb45-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="adb45-131">[Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.</span><span class="sxs-lookup"><span data-stu-id="adb45-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="adb45-132">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -hello 최신 Azure 보안 뉴스 및 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="adb45-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-databases/enable-auditing-on-sql-databases.png
[2]: ./media/security-center-enable-auditing-on-sql-databases/auditing-threat-detection-blade.png
