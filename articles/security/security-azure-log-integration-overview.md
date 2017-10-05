---
title: "Azure 리소스에서 SIEM 시스템으로 로그 통합 | Microsoft Docs"
description: "Azure 로그 통합, 주요 기능 및 작동 원리에 대해 알아봅니다."
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TerryLanfear
ms.assetid: 9c1346e1-baf8-4975-b2f2-42ae05b2dc0a
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/10/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: 6c3a2ac18fdb7a7a722447af720b9dee28adef08
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="introduction-to-microsoft-azure-log-integration"></a><span data-ttu-id="d94bd-103">Microsoft Azure 로그 통합 소개</span><span class="sxs-lookup"><span data-stu-id="d94bd-103">Introduction to Microsoft Azure log integration</span></span>
<span data-ttu-id="d94bd-104">Azure 로그 통합, 주요 기능 및 작동 원리에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-104">Learn about Azure log integration, its key capabilities, and how it works.</span></span>

## <a name="overview"></a><span data-ttu-id="d94bd-105">개요</span><span class="sxs-lookup"><span data-stu-id="d94bd-105">Overview</span></span>

<span data-ttu-id="d94bd-106">Azure 로그 통합은 Azure 리소스의 원시 로그를 온-프레미스 SIEM(보안 정보 및 이벤트 관리) 시스템에 통합할 수 있게 해주는 무료 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-106">Azure log integration is a free solution that enables you to integrate raw logs from your Azure resources in to your on-premises Security Information and Event Management (SIEM) systems.</span></span>

<span data-ttu-id="d94bd-107">Azure 로그 통합은 Azure 리소스에서 Windows 이벤트 뷰어 로그, [Azure 활동 로그](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md), [Azure Security Center 경고](../security-center/security-center-intro.md) 및 [Azure 진단 로그](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)로부터 Windows 이벤트를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-107">Azure log integration collects Windows events from Windows Event Viewer logs, [Azure Activity Logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md), [Azure Security Center alerts](../security-center/security-center-intro.md), and [Azure Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) from Azure resources.</span></span> <span data-ttu-id="d94bd-108">이 통합을 통해 SIEM 솔루션에서 보안 이벤트를 집계하고, 상관 관계를 설정하고, 분석하고, 경고할 수 있도록 온-프레미스 또는 클라우드의 모든 자산에 대한 통합 대시보드를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-108">This integration helps your SIEM solution provide a unified dashboard for all your assets, on-premises or in the cloud, so that you can aggregate, correlate, analyze, and alert for security events.</span></span>

>[!NOTE]
<span data-ttu-id="d94bd-109">현재 지원되는 클라우드는 Azure Commercial 및 Azure Government뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-109">At this time, the only supported clouds are Azure commercial and Azure Government.</span></span> <span data-ttu-id="d94bd-110">다른 클라우드는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-110">Other clouds are not supported.</span></span>

![Azure 로그 통합][1]

## <a name="what-logs-can-i-integrate"></a><span data-ttu-id="d94bd-112">어떤 로그와 통합할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="d94bd-112">What logs can I integrate?</span></span>
<span data-ttu-id="d94bd-113">Azure에서는 모든 Azure 서비스에 대해 광범위한 로깅을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-113">Azure produces extensive logging for every Azure service.</span></span> <span data-ttu-id="d94bd-114">이러한 로그는 세 가지 유형의 로그를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-114">These logs represent three types of logs:</span></span>

* <span data-ttu-id="d94bd-115">**컨트롤/관리 로그**는 [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) CREATE, UPDATE 및 DELETE 작업에 대한 가시성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-115">**Control/management logs** provide visibility into the [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) CREATE, UPDATE, and DELETE operations.</span></span> <span data-ttu-id="d94bd-116">Azure 활동 로그가 이 로그 유형에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-116">Azure Activity Logs is an example of this type of log.</span></span>
* <span data-ttu-id="d94bd-117">**데이터 평면 로그**는 Azure 리소스를 사용할 때 발생하는 이벤트에 대한 가시성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-117">**Data plane logs** provide visibility into the events raised as part of the usage of an Azure resource.</span></span> <span data-ttu-id="d94bd-118">이 로그 유형의 예는 Windows 가상 컴퓨터의 Windows 이벤트 뷰어에 있는 **시스템**, **보안** 및 **응용 프로그램** 채널이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-118">An example of this type of log is the Windows Event Viewer's **System**, **Security**, and **Application** channels in a Windows virtual machine.</span></span> <span data-ttu-id="d94bd-119">또 다른 예는 Azure Monitor를 통해 구성된 진단 로깅입니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-119">Another example is  Diagnostics Logging configured through Azure Monitor</span></span>
* <span data-ttu-id="d94bd-120">**처리된 이벤트**는 사용자 대신 처리된 경고 정보 및 분석된 이벤트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-120">**Processed events** provide analyzed event and alert information processed on your behalf.</span></span> <span data-ttu-id="d94bd-121">이 이벤트 유형의 예로 Azure Security Center 경고가 있습니다. Azure Security Center에서는 현재 보안 상태와 관련된 경고를 제공하기 위해 구독을 처리하고 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-121">An example of this type of event is Azure Security Center Alerts, where Azure Security Center has processed and analyzed your subscription to provide alerts relevant to your current security posture.</span></span>

<span data-ttu-id="d94bd-122">Azure 로그 통합은 ArcSight, QRadar 및 Splunk를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-122">Azure Log Integration supports ArcSight, QRadar, and Splunk.</span></span> <span data-ttu-id="d94bd-123">어떤 경우에서든 네이티브 커넥터가 있는지 여부를 평가하기 위해 SIEM 공급 업체에 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="d94bd-123">In all circumstances, please check with your SIEM vendor to assess whether they have a native connector.</span></span> <span data-ttu-id="d94bd-124">경우에 따라 네이티브 커넥터를 사용할 수 없는 경우 Azure 로그 통합을 사용하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-124">In some cases, you will not need to use Azure Log Integration when native connectors are available.</span></span> <span data-ttu-id="d94bd-125">지원되는 로그 형식에 대한 자세한 내용은 FAQ를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d94bd-125">For additional information on supported log types please visit the FAQ.</span></span>

>[!NOTE]
<span data-ttu-id="d94bd-126">Azure 로그 통합은 무료 솔루션이지만 로그 파일 정보 저장소로 인한 Azure Storage 비용이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-126">While Azure Log Integration is a free solution, there are Azure storage costs resulting from the log file information storage.</span></span>

<span data-ttu-id="d94bd-127">[Azure 로그 통합 MSDN 포럼](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration)을 통해 커뮤니티의 지원을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-127">Community assistance is available through the [Azure Log Integration MSDN Forum](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span></span> <span data-ttu-id="d94bd-128">이 포럼은 Azure 로그 통합을 최대한 활용하는 방법에 대한 질문, 답변, 팁, 요령 등 서로 지원할 수 있는 기능을 AzLog 커뮤니티에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-128">The forum provides the AzLog community the ability to support each other with questions, answers, tips, and tricks on how to get the most out of Azure Log Integration.</span></span> <span data-ttu-id="d94bd-129">또한 Azure 로그 통합 팀이 이 포럼을 모니터링하며 가능한 한 언제든지 도움을 드릴 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-129">In addition, the Azure Log Integration team monitors this forum and will help whenever we can.</span></span>

<span data-ttu-id="d94bd-130">[지원 요청](../azure-supportability/how-to-create-azure-support-request.md)을 열 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-130">You can also open a [support request](../azure-supportability/how-to-create-azure-support-request.md).</span></span> <span data-ttu-id="d94bd-131">지원 요청을 열려면 지원을 요청하는 서비스로 **로그 통합**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-131">To do this, select **Log Integration** as the service for which you are requesting support.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d94bd-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d94bd-132">Next steps</span></span>
<span data-ttu-id="d94bd-133">이 문서에서는 Azure 로그 통합을 소개했습니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-133">In this document, you were introduced to Azure log integration.</span></span> <span data-ttu-id="d94bd-134">Azure 로그 통합 및 지원되는 로그 유형에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d94bd-134">To learn more about Azure log integration and the types of logs supported, see the following:</span></span>

* <span data-ttu-id="d94bd-135">[Microsoft Azure 로그 통합](https://www.microsoft.com/download/details.aspx?id=53324) – Azure 로그 통합에 대한 세부 정보, 시스템 요구 사항 및 설치 지침을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-135">[Microsoft Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) – Download Center for details, system requirements, and install instructions on Azure log integration.</span></span>
* <span data-ttu-id="d94bd-136">[Azure 로그 통합 시작](security-azure-log-integration-get-started.md) - 이 자습서에서는 Azure 로그 통합을 설치하고 Azure WAD 저장소, Azure 활동 로그, Azure Security Center 경고 및 의 Azure Active Directory 감사 로그의 로그를 통합하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-136">[Get started with Azure log integration](security-azure-log-integration-get-started.md) - This tutorial walks you through installation of Azure log integration and integrating logs from Azure WAD storage, Azure Activity Logs, Azure Security Center alerts and Azure Active Directory audit logs.</span></span>
* <span data-ttu-id="d94bd-137">[파트너 구성 단계](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – 이 블로그 게시물에서는 Splunk, HP ArcSight, IBM QRadar 등의 파트너 솔루션과 함께 작동하도록 Azure 로그 통합을 구성하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-137">[Partner configuration steps](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – This blog post shows you how to configure Azure log integration to work with partner solutions Splunk, HP ArcSight, and IBM QRadar.</span></span> <span data-ttu-id="d94bd-138">이 블로그를 통해 파트너 솔루션을 구성하는 최신 방식을 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-138">This blog represents our current position on configuring the partner solutions.</span></span> <span data-ttu-id="d94bd-139">어떤 경우든 먼저 파트너 솔루션 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d94bd-139">In all cases, please refer to partner solution documentation first.</span></span>
* <span data-ttu-id="d94bd-140">[Syslog를 통해 QRadar로 활동 및 ASC 경고 전송](https://blogs.msdn.microsoft.com/azuresecurity/2016/09/24/integrate-azure-logs-to-qradar/) - 이 블로그 게시물은 syslog를 통해 QRadar로 활동 및 Azure Security Center 경고를 보내는 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-140">[Activity and ASC alerts over syslog to QRadar](https://blogs.msdn.microsoft.com/azuresecurity/2016/09/24/integrate-azure-logs-to-qradar/) – This blog post provides the steps to send Activity and Azure Security Center alerts over syslog to QRadar</span></span>
* <span data-ttu-id="d94bd-141">[Azure 로그 통합 FAQ(질문과 대답)](security-azure-log-integration-faq.md) - 이 FAQ는 Azure 로그 통합에 대한 질문에 답변합니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-141">[Azure log Integration frequently asked questions (FAQ)](security-azure-log-integration-faq.md) - This FAQ answers questions about Azure log integration.</span></span>
* <span data-ttu-id="d94bd-142">[Azure 로그 통합과 Security Center 경고 통합](../security-center/security-center-integrating-alerts-with-log-integration.md) - 이 문서에서는 Azure Security Center 경고와 Azure 로그 통합을 동기화하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d94bd-142">[Integrating Security Center alerts with Azure log Integration](../security-center/security-center-integrating-alerts-with-log-integration.md) – This document shows you how to sync Azure Security Center alerts with Azure Log Integration.</span></span>

<!--Image references-->
[1]: ./media/security-azure-log-integration-overview/azure-log-integration.png
