---
title: "서비스 공급자에 대한 Log Analytics 기능 | Microsoft Docs"
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
ms.openlocfilehash: 8a67d9a9d345682e9e6c8f5c7779204a038f5f6a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="log-analytics-features-for-service-providers"></a><span data-ttu-id="bb99d-103">서비스 공급자에 대한 Log Analytics 기능</span><span class="sxs-lookup"><span data-stu-id="bb99d-103">Log Analytics features for Service Providers</span></span>
<span data-ttu-id="bb99d-104">Log Analytics는 MSP(Managed Service Providers), 대기업, ISV(Independent Software Vendor)를 지원하며 호스팅 서비스 공급자가 고객의 온-프레미스 또는 클라우드 인프라에서 서버를 관리하고 모니터링할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-104">Log Analytics can help managed service providers (MSPs), large enterprises, independent software vendors (ISVs), and hosting service providers manage and monitor servers in customer's on-premises or cloud infrastructure.</span></span> 

<span data-ttu-id="bb99d-105">대기업은 서비스 공급자와 많은 유사성을 공유하는데, 특히 중앙 IT 팀이 다양한 사업부의 IT 관리를 담당한다는 점이 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-105">Large enterprises share many similarities with service providers, particularly when there is a centralized IT team that is responsible for managing IT for many different business units.</span></span> <span data-ttu-id="bb99d-106">간단한 설명을 위해 이 문서에서는 *서비스 공급자*라는 용어를 사용하지만 기업 및 기타 고객에 대해서도 같은 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-106">For simplicity, this document uses the term *service provider* but the same functionality is also available for enterprises and other customers.</span></span>

## <a name="cloud-solution-provider"></a><span data-ttu-id="bb99d-107">클라우드 솔루션 공급자</span><span class="sxs-lookup"><span data-stu-id="bb99d-107">Cloud Solution Provider</span></span>
<span data-ttu-id="bb99d-108">[CSP(클라우드 솔루션 공급자)](https://partner.microsoft.com/Solutions/cloud-reseller-overview) 프로그램에 참여하는 파트너 및 서비스 공급자에게는 Log Analytics가 CSP 구독에서 사용할 수 있는 Azure 서비스 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-108">For partners and service providers who are part of the [Cloud Solution Provider (CSP)](https://partner.microsoft.com/Solutions/cloud-reseller-overview) program, Log Analytics is one of the Azure services available on a CSP subscription.</span></span> 

<span data-ttu-id="bb99d-109">Log Analytics의 경우 다음 기능을 *클라우드 솔루션 공급자* 구독에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-109">For Log Analytics, the following capabilities are enabled in *Cloud Solution Provider* subscriptions.</span></span>

<span data-ttu-id="bb99d-110">*CSP(클라우드 솔루션 공급자)*는 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-110">As a *Cloud Solution Provider* you can:</span></span>

* <span data-ttu-id="bb99d-111">테넌트(고객) 구독에 Log Analytics 작업 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-111">Create Log Analytics workspaces in a tenant (customer's) subscription.</span></span>
* <span data-ttu-id="bb99d-112">테넌트에서 만든 작업 영역에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-112">Access workspaces created by tenants.</span></span> 
* <span data-ttu-id="bb99d-113">Azure 사용자 관리를 사용하여 작업 영역에 대한 사용자 액세스를 추가 및 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-113">Add and remove user access to the workspace using Azure user management.</span></span> <span data-ttu-id="bb99d-114">OMS 포털의 테넌트 작업 영역에서 설정의 사용자 관리 페이지를 사용할 수 없는 경우</span><span class="sxs-lookup"><span data-stu-id="bb99d-114">When in a tenant’s workspace in the OMS portal the user management page under Settings is not available</span></span>
  * <span data-ttu-id="bb99d-115">Log Analytics에서는 아직 역할 기반 액세스를 지원하지 않으므로 Azure 포털에서 사용자에게 `reader` 권한을 부여하여 OMS 포털에서 구성을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-115">Log Analytics does not support role-based access yet - giving a user `reader` permission in the Azure portal allows them to make configuration changes in the OMS portal</span></span>

<span data-ttu-id="bb99d-116">테넌트의 구독에 로그인하려면 테넌트 식별자를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-116">To log in to a tenant’s subscription, you need to specify the tenant identifier.</span></span> <span data-ttu-id="bb99d-117">테넌트 식별자는 보통 로그인하는 데 사용한 전자 메일 주소의 마지막 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-117">The tenant identifier is often that last part of the e-mail address used to sign in.</span></span>

* <span data-ttu-id="bb99d-118">OMS 포털에서 포털에 대한 URL에 `?tenant=contoso.com`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-118">In the OMS portal, add `?tenant=contoso.com` in the URL for the portal.</span></span> <span data-ttu-id="bb99d-119">위치(예:`mms.microsoft.com/?tenant=contoso.com`</span><span class="sxs-lookup"><span data-stu-id="bb99d-119">For example, `mms.microsoft.com/?tenant=contoso.com`</span></span>
* <span data-ttu-id="bb99d-120">PowerShell에서는 `Add-AzureRmAccount` cmdlet을 사용할 때 `-Tenant contoso.com` 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-120">In PowerShell, use the `-Tenant contoso.com` parameter when using `Add-AzureRmAccount` cmdlet</span></span>
* <span data-ttu-id="bb99d-121">Azure 포털에서 `OMS portal` 링크를 사용하여 선택한 작업 영역에 대한 OMS 포털을 열고 로그인하면 테넌트 식별자가 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-121">The tenant identifier is automatically added when you use the `OMS portal` link from the Azure portal to open and log in to the OMS portal for the selected workspace</span></span>

<span data-ttu-id="bb99d-122">CSP(클라우드 솔루션 공급자)의 *고객*은 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-122">As a *customer* of a Cloud Solution Provider you can:</span></span>

* <span data-ttu-id="bb99d-123">CSP 구독에서 Log Analytics 작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="bb99d-123">Create log analytics workspaces in a CSP subscription</span></span>
* <span data-ttu-id="bb99d-124">CSP가 만든 작업 영역에 액세스</span><span class="sxs-lookup"><span data-stu-id="bb99d-124">Access workspaces created by the CSP</span></span>
  * <span data-ttu-id="bb99d-125">Azure 포털에서 `OMS portal` 링크를 사용하여 선택한 작업 영역에 대한 OMS 포털을 열고 로그인</span><span class="sxs-lookup"><span data-stu-id="bb99d-125">Use the `OMS portal` link from the Azure portal to open and log in to the OMS portal for the selected workspace</span></span>
* <span data-ttu-id="bb99d-126">OMS 포털의 설정에서 사용자 관리 페이지 보기 및 사용</span><span class="sxs-lookup"><span data-stu-id="bb99d-126">View and use the user management page under Settings in the OMS portal</span></span>

> [!NOTE]
> <span data-ttu-id="bb99d-127">Log Analytics에 대해 포함된 Backup 및 Site Recovery 솔루션을 Recovery Services 자격 증명 모음에 연결할 수 없으며 CSP 구독에서 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-127">The included Backup and Site Recovery solutions for Log Analytics are not able to connect to a Recovery Services vault and cannot be configured in a CSP subscription.</span></span> 
> 
> 

## <a name="managing-multiple-customers-using-log-analytics"></a><span data-ttu-id="bb99d-128">Log Analytics를 사용하여 여러 고객 관리</span><span class="sxs-lookup"><span data-stu-id="bb99d-128">Managing multiple customers using Log Analytics</span></span>
<span data-ttu-id="bb99d-129">관리하는 고객마다 Log Analytics 작업 영역을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-129">It is recommended that you create a Log Analytics workspace for each customer you manage.</span></span> <span data-ttu-id="bb99d-130">Log Analytics 작업 영역이 제공하는 정보:</span><span class="sxs-lookup"><span data-stu-id="bb99d-130">A Log Analytics workspace provides:</span></span>

* <span data-ttu-id="bb99d-131">저장할 데이터에 대한 지리적 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-131">A geographic location for data to be stored.</span></span> 
* <span data-ttu-id="bb99d-132">대금 청구에 대한 세분성</span><span class="sxs-lookup"><span data-stu-id="bb99d-132">Granularity for billing</span></span> 
* <span data-ttu-id="bb99d-133">데이터 격리</span><span class="sxs-lookup"><span data-stu-id="bb99d-133">Data isolation</span></span> 
* <span data-ttu-id="bb99d-134">고유한 구성</span><span class="sxs-lookup"><span data-stu-id="bb99d-134">Unique configuration</span></span>

<span data-ttu-id="bb99d-135">고객당 작업 영역을 만들면 각 고객의 데이터를 별도로 유지하고 각 고객의 사용 현황을 추적할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-135">By creating a workspace per customer, you are able to keep each customer’s data separate and also track the usage of each customer.</span></span>

<span data-ttu-id="bb99d-136">여러 작업 영역을 만들어야 하는 시기와 이유에 대한 자세한 내용은 [Log Analytics에 대한 액세스 관리](log-analytics-manage-access.md#determine-the-number-of-workspaces-you-need)에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-136">More details on when and why to create multiple workspaces is described in [manage access to log analytics](log-analytics-manage-access.md#determine-the-number-of-workspaces-you-need).</span></span>

<span data-ttu-id="bb99d-137">고객 작업 영역의 생성 및 구성은 [PowerShell](log-analytics-powershell-workspace-configuration.md), [Resource Manager 템플릿](log-analytics-template-workspace-configuration.md), [REST API](https://www.nuget.org/packages/Microsoft.Azure.Management.OperationalInsights/)를 사용하여 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-137">Creation and configuration of customer workspaces can be automated using [PowerShell](log-analytics-powershell-workspace-configuration.md), [Resource Manager templates](log-analytics-template-workspace-configuration.md), or using the [REST API](https://www.nuget.org/packages/Microsoft.Azure.Management.OperationalInsights/).</span></span>

<span data-ttu-id="bb99d-138">작업 영역 구성을 위해 Resource Manager 템플릿을 사용하면 작업 영역을 만들고 구성하는 데 사용할 수 있는 마스터 구성을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-138">The use of Resource Manager templates for workspace configuration allows you to have a master configuration that can be used to create and configure workspaces.</span></span> <span data-ttu-id="bb99d-139">사용자 요구 사항에 따라 자동으로 구성된 작업 영역이 고객에 대해 생성되는 것을 확신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-139">You can be confident that as workspaces are created for customers they are automatically configured to your requirements.</span></span> <span data-ttu-id="bb99d-140">요구 사항을 업데이트하면 템플릿이 업데이트된 후 기존 작업 영역에 다시 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-140">When you update your requirements, the template is updated and then reapplied the existing workspaces.</span></span> <span data-ttu-id="bb99d-141">이 프로세스는 기존 작업 영역이 새로운 표준을 충족하는지도 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-141">This process ensures that even existing workspaces meet your new standards.</span></span>    

<span data-ttu-id="bb99d-142">여러 Log Analytics 작업 영역을 관리할 때는 [경고](log-analytics-alerts.md) 기능을 사용하여 각 작업 영역을 기존의 티켓 시스템/운영 콘솔과 통합하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-142">When managing multiple Log Analytics workspaces, we recommend integrating each workspace with your existing ticketing system / operations console using the [Alerts](log-analytics-alerts.md) functionality.</span></span> <span data-ttu-id="bb99d-143">기존 시스템과 통합되므로 지원 담당자는 친숙한 프로세스를 계속 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-143">By integrating with your existing systems, support staff can continue to follow their familiar processes.</span></span> <span data-ttu-id="bb99d-144">Log Analytics는 각 작업 영역에서 사용자가 지정한 경고 기준을 정기적으로 확인하고 작업이 필요하면 경고를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-144">Log Analytics regularly checks each workspace against the alert criteria you specify and generates an alert when action is needed.</span></span>

<span data-ttu-id="bb99d-145">데이터에 대한 개인 설정된 보기는 Azure Portal의 [대시보드](../azure-portal/azure-portal-dashboards.md) 기능을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="bb99d-145">For personalized views of data, use the [dashboard](../azure-portal/azure-portal-dashboards.md) capability in the Azure portal.</span></span>  

<span data-ttu-id="bb99d-146">작업 영역 전반의 데이터를 요약하는 경영진 수준 보고서를 얻기 위해서는 Log Analytics와 [PowerBI](log-analytics-powerbi.md)의 통합을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-146">For executive level reports that summarize data across workspaces you can use the integration between Log Analytics and [PowerBI](log-analytics-powerbi.md).</span></span> <span data-ttu-id="bb99d-147">다른 보고 시스템과 통합이 필요한 경우 Search API(PowerShell 또는 [REST](log-analytics-log-search-api.md)를 통해)를 사용하여 쿼리를 실행하고 검색 결과를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb99d-147">If you need to integrate with another reporting system, you can use the Search API (via PowerShell or [REST](log-analytics-log-search-api.md)) to run queries and export search results.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb99d-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bb99d-148">Next Steps</span></span>
* <span data-ttu-id="bb99d-149">[Resource Manager 템플릿](log-analytics-template-workspace-configuration.md)을 사용하여 작업 영역 생성 및 구성 자동화</span><span class="sxs-lookup"><span data-stu-id="bb99d-149">Automate creation and configuration of workspaces using [Resource Manager templates](log-analytics-template-workspace-configuration.md)</span></span>
* <span data-ttu-id="bb99d-150">[PowerShell](log-analytics-powershell-workspace-configuration.md)을 사용하여 작업 영역 생성 자동화</span><span class="sxs-lookup"><span data-stu-id="bb99d-150">Automate creation of workspaces using [PowerShell](log-analytics-powershell-workspace-configuration.md)</span></span> 
* <span data-ttu-id="bb99d-151">[경고](log-analytics-alerts.md)를 사용하여 기존 시스템과 통합</span><span class="sxs-lookup"><span data-stu-id="bb99d-151">Use [Alerts](log-analytics-alerts.md) to integrate with existing systems</span></span>
* <span data-ttu-id="bb99d-152">[PowerBI](log-analytics-powerbi.md)를 사용하여 요약 보고서 생성</span><span class="sxs-lookup"><span data-stu-id="bb99d-152">Generate summary reports using [PowerBI](log-analytics-powerbi.md)</span></span>

