---
title: "서비스 공급자의 분석 기능 aaaLog | Microsoft Docs"
description: "Log Analytics는 MSP(Managed Service Providers), 대기업, ISV(Independent Software Vendor)를 지원하며 호스팅 서비스 공급자가 고객의 온-프레미스 또는 클라우드 인프라에서 서버를 관리하고 모니터링할 수 있도록 합니다."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: c07f0b9f-ec37-480d-91ec-d9bcf6786464
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: richrund
ms.openlocfilehash: 3c0a93232293f90385c6c724be436cee1cf855f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-features-for-service-providers"></a><span data-ttu-id="b2e34-103">서비스 공급자에 대한 Log Analytics 기능</span><span class="sxs-lookup"><span data-stu-id="b2e34-103">Log Analytics features for Service Providers</span></span>
<span data-ttu-id="b2e34-104">Log Analytics는 MSP(Managed Service Providers), 대기업, ISV(Independent Software Vendor)를 지원하며 호스팅 서비스 공급자가 고객의 온-프레미스 또는 클라우드 인프라에서 서버를 관리하고 모니터링할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-104">Log Analytics can help managed service providers (MSPs), large enterprises, independent software vendors (ISVs), and hosting service providers manage and monitor servers in customer's on-premises or cloud infrastructure.</span></span> 

<span data-ttu-id="b2e34-105">대기업은 서비스 공급자와 많은 유사성을 공유하는데, 특히 중앙 IT 팀이 다양한 사업부의 IT 관리를 담당한다는 점이 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-105">Large enterprises share many similarities with service providers, particularly when there is a centralized IT team that is responsible for managing IT for many different business units.</span></span> <span data-ttu-id="b2e34-106">간단한 설명을 위해이 문서에서는 hello 용어 *서비스 공급자* hello 동일한 기능 뿐만 아니라 다른 고객과 기업에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-106">For simplicity, this document uses hello term *service provider* but hello same functionality is also available for enterprises and other customers.</span></span>

## <a name="cloud-solution-provider"></a><span data-ttu-id="b2e34-107">클라우드 솔루션 공급자</span><span class="sxs-lookup"><span data-stu-id="b2e34-107">Cloud Solution Provider</span></span>
<span data-ttu-id="b2e34-108">파트너 및 hello의 일부인 서비스 공급자에 대 한 [클라우드 솔루션 공급자 (CSP)](https://partner.microsoft.com/Solutions/cloud-reseller-overview) 프로그램, 로그 분석 CSP 구독에서 사용할 수 있는 Azure 서비스는 hello 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-108">For partners and service providers who are part of hello [Cloud Solution Provider (CSP)](https://partner.microsoft.com/Solutions/cloud-reseller-overview) program, Log Analytics is one of hello Azure services available on a CSP subscription.</span></span> 

<span data-ttu-id="b2e34-109">사용할 수 있는 기능을 수행 하는 hello 로그 분석에 대 한 *클라우드 솔루션 공급자* 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-109">For Log Analytics, hello following capabilities are enabled in *Cloud Solution Provider* subscriptions.</span></span>

<span data-ttu-id="b2e34-110">*CSP(클라우드 솔루션 공급자)*는 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-110">As a *Cloud Solution Provider* you can:</span></span>

* <span data-ttu-id="b2e34-111">테넌트(고객) 구독에 Log Analytics 작업 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-111">Create Log Analytics workspaces in a tenant (customer's) subscription.</span></span>
* <span data-ttu-id="b2e34-112">테넌트에서 만든 작업 영역에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-112">Access workspaces created by tenants.</span></span> 
* <span data-ttu-id="b2e34-113">추가 하 고 Azure 사용자 관리를 사용 하 여 사용자 액세스 toohello 작업을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-113">Add and remove user access toohello workspace using Azure user management.</span></span> <span data-ttu-id="b2e34-114">Hello OMS의에서 테 넌 트의 작업 영역에서 포털 hello 사용자 관리 페이지의 설정에서 사용할 수 없는 경우</span><span class="sxs-lookup"><span data-stu-id="b2e34-114">When in a tenant’s workspace in hello OMS portal hello user management page under Settings is not available</span></span>
  * <span data-ttu-id="b2e34-115">역할 기반 액세스 아직-사용자 지정 로그 분석 지원 하지 않습니다 `reader` hello Azure 포털에에서는 권한이 있도록 toomake 구성 변경 내용을 hello OMS 포털에서</span><span class="sxs-lookup"><span data-stu-id="b2e34-115">Log Analytics does not support role-based access yet - giving a user `reader` permission in hello Azure portal allows them toomake configuration changes in hello OMS portal</span></span>

<span data-ttu-id="b2e34-116">tooa 테 넌 트의 구독에서 toolog, toospecify hello 테 넌 트 식별자가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-116">toolog in tooa tenant’s subscription, you need toospecify hello tenant identifier.</span></span> <span data-ttu-id="b2e34-117">hello 테 넌 트 식별자는 마지막 부분의에 hello 전자 메일 주소 사용 toosign 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-117">hello tenant identifier is often that last part of hello e-mail address used toosign in.</span></span>

* <span data-ttu-id="b2e34-118">Hello OMS 포털에서 추가 `?tenant=contoso.com` hello 포털에 대 한 hello url입니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-118">In hello OMS portal, add `?tenant=contoso.com` in hello URL for hello portal.</span></span> <span data-ttu-id="b2e34-119">예를 들어 `mms.microsoft.com/?tenant=contoso.com`</span><span class="sxs-lookup"><span data-stu-id="b2e34-119">For example, `mms.microsoft.com/?tenant=contoso.com`</span></span>
* <span data-ttu-id="b2e34-120">PowerShell에서 hello를 사용 하 여 `-Tenant contoso.com` 매개 변수를 사용 하는 경우 `Add-AzureRmAccount` cmdlet</span><span class="sxs-lookup"><span data-stu-id="b2e34-120">In PowerShell, use hello `-Tenant contoso.com` parameter when using `Add-AzureRmAccount` cmdlet</span></span>
* <span data-ttu-id="b2e34-121">hello 테 넌 트 식별자는 hello를 사용 하는 경우에 자동으로 추가 됩니다 `OMS portal` hello Azure 포털 tooopen에서에서에 연결 하 고 선택한 hello 작업 영역에 대 한 toohello OMS 포털에 로그인</span><span class="sxs-lookup"><span data-stu-id="b2e34-121">hello tenant identifier is automatically added when you use hello `OMS portal` link from hello Azure portal tooopen and log in toohello OMS portal for hello selected workspace</span></span>

<span data-ttu-id="b2e34-122">CSP(클라우드 솔루션 공급자)의 *고객*은 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-122">As a *customer* of a Cloud Solution Provider you can:</span></span>

* <span data-ttu-id="b2e34-123">CSP 구독에서 Log Analytics 작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="b2e34-123">Create log analytics workspaces in a CSP subscription</span></span>
* <span data-ttu-id="b2e34-124">Hello CSP 만든 액세스 작업 영역</span><span class="sxs-lookup"><span data-stu-id="b2e34-124">Access workspaces created by hello CSP</span></span>
  * <span data-ttu-id="b2e34-125">사용 하 여 hello `OMS portal` hello Azure 포털 tooopen에서에서에 연결 하 고 선택한 hello 작업 영역에 대 한 toohello OMS 포털에 로그인</span><span class="sxs-lookup"><span data-stu-id="b2e34-125">Use hello `OMS portal` link from hello Azure portal tooopen and log in toohello OMS portal for hello selected workspace</span></span>
* <span data-ttu-id="b2e34-126">보기 및 hello OMS 포털에서 설정 되는 hello 사용자 관리 페이지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-126">View and use hello user management page under Settings in hello OMS portal</span></span>

> [!NOTE]
> <span data-ttu-id="b2e34-127">hello 포함 백업 및 로그 분석에 대 한 사이트 복구 솔루션은 수 tooconnect tooa 복구 서비스 자격 증명 모음 CSP 구독에서 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-127">hello included Backup and Site Recovery solutions for Log Analytics are not able tooconnect tooa Recovery Services vault and cannot be configured in a CSP subscription.</span></span> 
> 
> 

## <a name="managing-multiple-customers-using-log-analytics"></a><span data-ttu-id="b2e34-128">Log Analytics를 사용하여 여러 고객 관리</span><span class="sxs-lookup"><span data-stu-id="b2e34-128">Managing multiple customers using Log Analytics</span></span>
<span data-ttu-id="b2e34-129">관리하는 고객마다 Log Analytics 작업 영역을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-129">It is recommended that you create a Log Analytics workspace for each customer you manage.</span></span> <span data-ttu-id="b2e34-130">Log Analytics 작업 영역이 제공하는 정보:</span><span class="sxs-lookup"><span data-stu-id="b2e34-130">A Log Analytics workspace provides:</span></span>

* <span data-ttu-id="b2e34-131">저장 된 데이터 toobe에 대 한 지리적 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-131">A geographic location for data toobe stored.</span></span> 
* <span data-ttu-id="b2e34-132">대금 청구에 대한 세분성</span><span class="sxs-lookup"><span data-stu-id="b2e34-132">Granularity for billing</span></span> 
* <span data-ttu-id="b2e34-133">데이터 격리</span><span class="sxs-lookup"><span data-stu-id="b2e34-133">Data isolation</span></span> 
* <span data-ttu-id="b2e34-134">고유한 구성</span><span class="sxs-lookup"><span data-stu-id="b2e34-134">Unique configuration</span></span>

<span data-ttu-id="b2e34-135">고객당 작업 영역을 만들면 수 tookeep 각 고객의 데이터를 별도 하는 또한 각 고객의 hello 사용을 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-135">By creating a workspace per customer, you are able tookeep each customer’s data separate and also track hello usage of each customer.</span></span>

<span data-ttu-id="b2e34-136">시기 및 이유 toocreate 여러 작업 영역에서 설명 하는 대 한 자세한 내용은 [액세스 toolog 분석 관리](log-analytics-manage-access.md#determine-the-number-of-workspaces-you-need)합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-136">More details on when and why toocreate multiple workspaces is described in [manage access toolog analytics](log-analytics-manage-access.md#determine-the-number-of-workspaces-you-need).</span></span>

<span data-ttu-id="b2e34-137">고객 작업의 생성 및 구성을 사용 하 여 자동화할 수 [PowerShell](log-analytics-powershell-workspace-configuration.md), [리소스 관리자 템플릿을](log-analytics-template-workspace-configuration.md), 또는 hello를 사용 하 여 [REST API](https://www.nuget.org/packages/Microsoft.Azure.Management.OperationalInsights/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-137">Creation and configuration of customer workspaces can be automated using [PowerShell](log-analytics-powershell-workspace-configuration.md), [Resource Manager templates](log-analytics-template-workspace-configuration.md), or using hello [REST API](https://www.nuget.org/packages/Microsoft.Azure.Management.OperationalInsights/).</span></span>

<span data-ttu-id="b2e34-138">hello 템플릿 사용 하 여 리소스 관리자 작업 영역 구성에 대 한 사용된 toocreate 하 고 작업 영역을 구성할 수 있는 마스터 구성 toohave가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-138">hello use of Resource Manager templates for workspace configuration allows you toohave a master configuration that can be used toocreate and configure workspaces.</span></span> <span data-ttu-id="b2e34-139">작업 영역에 대해 만들어지는 고객은 자동으로 구성 tooyour 요구 사항을 확신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-139">You can be confident that as workspaces are created for customers they are automatically configured tooyour requirements.</span></span> <span data-ttu-id="b2e34-140">요구 사항 업데이트 하면 hello 템플릿을 업데이트 되 고 hello 기존 작업 영역 다시 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-140">When you update your requirements, hello template is updated and then reapplied hello existing workspaces.</span></span> <span data-ttu-id="b2e34-141">이 프로세스는 기존 작업 영역이 새로운 표준을 충족하는지도 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-141">This process ensures that even existing workspaces meet your new standards.</span></span>    

<span data-ttu-id="b2e34-142">여러 개의 로그 분석 작업 영역을 관리 하는 경우 각 작업 영역의 기존 발권 시스템 통합는 것이 좋습니다  ¼ ײ hello를 사용 하 여 / [경고](log-analytics-alerts.md) 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-142">When managing multiple Log Analytics workspaces, we recommend integrating each workspace with your existing ticketing system / operations console using hello [Alerts](log-analytics-alerts.md) functionality.</span></span> <span data-ttu-id="b2e34-143">기존 시스템에 통합 하 여 친숙 한 프로세스 지원부 toofollow 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-143">By integrating with your existing systems, support staff can continue toofollow their familiar processes.</span></span> <span data-ttu-id="b2e34-144">정기적으로 로그 분석은 사용자가 지정한 hello 경고 조건에 대 한 각 작업 영역을 확인 하 고 조치도 필요 하지 않으면 경고를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-144">Log Analytics regularly checks each workspace against hello alert criteria you specify and generates an alert when action is needed.</span></span>

<span data-ttu-id="b2e34-145">데이터의 개인 설정 된 보기에 대 한 hello를 사용 하 여 [대시보드](../azure-portal/azure-portal-dashboards.md) hello Azure 포털의에서 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-145">For personalized views of data, use hello [dashboard](../azure-portal/azure-portal-dashboards.md) capability in hello Azure portal.</span></span>  

<span data-ttu-id="b2e34-146">Executive 수준에 대 한 보고서 작업 영역에서는 전체에서 데이터를 요약 하는 로그 분석 간의 통합 hello 및 [PowerBI](log-analytics-powerbi.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e34-146">For executive level reports that summarize data across workspaces you can use hello integration between Log Analytics and [PowerBI](log-analytics-powerbi.md).</span></span> <span data-ttu-id="b2e34-147">보고 하는 다른 시스템과 toointegrate 해야 할 경우 hello 검색 API를 사용할 수 있습니다 (PowerShell을 통해 또는 [REST](log-analytics-log-search-api.md)) toorun 쿼리 및 내보내기에 대 한 검색 결과.</span><span class="sxs-lookup"><span data-stu-id="b2e34-147">If you need toointegrate with another reporting system, you can use hello Search API (via PowerShell or [REST](log-analytics-log-search-api.md)) toorun queries and export search results.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2e34-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b2e34-148">Next Steps</span></span>
* <span data-ttu-id="b2e34-149">[Resource Manager 템플릿](log-analytics-template-workspace-configuration.md)을 사용하여 작업 영역 생성 및 구성 자동화</span><span class="sxs-lookup"><span data-stu-id="b2e34-149">Automate creation and configuration of workspaces using [Resource Manager templates](log-analytics-template-workspace-configuration.md)</span></span>
* <span data-ttu-id="b2e34-150">[PowerShell](log-analytics-powershell-workspace-configuration.md)을 사용하여 작업 영역 생성 자동화</span><span class="sxs-lookup"><span data-stu-id="b2e34-150">Automate creation of workspaces using [PowerShell](log-analytics-powershell-workspace-configuration.md)</span></span> 
* <span data-ttu-id="b2e34-151">사용 하 여 [경고](log-analytics-alerts.md) 기존 시스템과 toointegrate</span><span class="sxs-lookup"><span data-stu-id="b2e34-151">Use [Alerts](log-analytics-alerts.md) toointegrate with existing systems</span></span>
* <span data-ttu-id="b2e34-152">[PowerBI](log-analytics-powerbi.md)를 사용하여 요약 보고서 생성</span><span class="sxs-lookup"><span data-stu-id="b2e34-152">Generate summary reports using [PowerBI](log-analytics-powerbi.md)</span></span>

