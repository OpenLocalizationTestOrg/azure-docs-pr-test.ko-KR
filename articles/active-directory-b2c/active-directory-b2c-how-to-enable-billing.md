---
title: "Azure AD B2C에 Azure 구독을 연결하는 방법 | Microsoft Docs"
description: "Azure AD B2C 테넌트에 대한 요금을 Azure 구독에 청구하는 단계별 가이드입니다."
services: active-directory-b2c
documentationcenter: dev-center-name
author: rojasja
manager: mbaldwin
ms.service: active-directory-b2c
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/05/2016
ms.author: joroja
ms.openlocfilehash: 5b9955b2af7f20a79981315fa33a0eb5380a5465
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="linking-an-azure-subscription-to-an-azure-b2c-tenant-to-pay-for-usage-charges"></a><span data-ttu-id="10dde-103">Azure 구독을 Azure B2C 테넌트와 연결하여 사용 요금 지불</span><span class="sxs-lookup"><span data-stu-id="10dde-103">Linking an Azure Subscription to an Azure B2C tenant to pay for usage charges</span></span>

<span data-ttu-id="10dde-104">Azure AD B2C(Azure Active Directory B2C)에 대한 사용 요금은 Azure 구독에 지속적으로 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-104">Ongoing usage charges for Azure Active Directory B2C (or Azure AD B2C) are billed to an Azure Subscription.</span></span> <span data-ttu-id="10dde-105">테넌트 관리자는 B2C 테넌트 자체를 만든 후에 Azure AD B2C 테넌트를 Azure 구독에 명시적으로 연결할 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-105">It is necessary for the tenant administrator to explicitly link the Azure AD B2C tenant to an Azure subscription after creating the B2C tenant itself.</span></span>  <span data-ttu-id="10dde-106">이 연결은 대상 Azure 구독에 Azure AD "B2C 테넌트" 리소스를 만들어서 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-106">This link is achieved by creating an Azure AD "B2C Tenant" resource in the target Azure subscription.</span></span> <span data-ttu-id="10dde-107">많은 B2C 테넌트는 다른 Azure 리소스(예: VM, 데이터 저장소, LogicApps)와 함께 단일 Azure 구독에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-107">Many B2C tenants can be linked to a single Azure subscription along with other Azure resources (for example, VMs, Data storage, LogicApps)</span></span>


> [!IMPORTANT]
> <span data-ttu-id="10dde-108">B2C의 사용 요금 청구 및 가격 책정에 대한 최신 정보는 [Azure AD B2C 가격](
https://azure.microsoft.com/pricing/details/active-directory-b2c/) 페이지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-108">The latest information on usage billing and pricing for B2C is at the following page: [Azure AD B2C Pricing](
https://azure.microsoft.com/pricing/details/active-directory-b2c/)</span></span>

## <a name="step-1---create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="10dde-109">1단계 - Azure AD B2C 테넌트 만들기</span><span class="sxs-lookup"><span data-stu-id="10dde-109">Step 1 - Create an Azure AD B2C Tenant</span></span>
<span data-ttu-id="10dde-110">먼저 B2C 테넌트 만들기를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-110">B2C tenant creation must be completed first.</span></span> <span data-ttu-id="10dde-111">이미 대상 B2C 테넌트를 만든 경우에는 이 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-111">Skip this step if you have already created your target B2C Tenant.</span></span> [<span data-ttu-id="10dde-112">Azure AD B2C 시작</span><span class="sxs-lookup"><span data-stu-id="10dde-112">Get started with Azure AD B2C</span></span>](active-directory-b2c-get-started.md)

## <a name="step-2---open-azure-portal-in-the-azure-ad-tenant-that-shows-your-azure-subscription"></a><span data-ttu-id="10dde-113">2단계 - Azure 구독을 보여 주는 Azure AD 테넌트에서 Azure Portal 열기</span><span class="sxs-lookup"><span data-stu-id="10dde-113">Step 2 - Open Azure portal in the Azure AD Tenant that shows your Azure subscription</span></span>
<span data-ttu-id="10dde-114">[Azure Portal](https://portal.azure.com)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-114">Navigate to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="10dde-115">사용할 Azure 구독을 보여 주는 Azure AD 테넌트로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-115">Switch to the Azure AD Tenant that shows the Azure subscription you would like to use.</span></span> <span data-ttu-id="10dde-116">이 Azure AD 테넌트는 B2C 테넌트와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-116">This Azure AD tenant is different from the B2C tenant.</span></span> <span data-ttu-id="10dde-117">Azure Portal에서 대시보드의 오른쪽 위에 있는 계정 이름을 클릭하여 Azure AD 테넌트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-117">Within the Azure portal, click the account name on the upper right of the dashboard to select the Azure AD Tenant.</span></span> <span data-ttu-id="10dde-118">계속하려면 Azure 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-118">An Azure subscription is needed to proceed.</span></span> [<span data-ttu-id="10dde-119">Azure 구독 가져오기</span><span class="sxs-lookup"><span data-stu-id="10dde-119">Get an Azure Subscription</span></span>](https://account.windowsazure.com/signup?showCatalog=True)

![Azure AD 테넌트로 전환](./media/active-directory-b2c-how-to-enable-billing/SelectAzureADTenant.png)

## <a name="step-3---create-a-b2c-tenant-resource-in-azure-marketplace"></a><span data-ttu-id="10dde-121">3단계 - Azure Marketplace에서 B2C 테넌트 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="10dde-121">Step 3 - Create a B2C Tenant resource in Azure Marketplace</span></span>
<span data-ttu-id="10dde-122">[마켓플레이스] 아이콘을 클릭하거나 대시보드의 왼쪽 위 모서리에 있는 녹색 "+" 기호를 선택하여 마켓플레이스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-122">Open Marketplace by clicking the Marketplace icon, or selecting the green "+" in the upper left corner of the dashboard.</span></span>  <span data-ttu-id="10dde-123">Azure Active Directory B2C를 검색하고 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-123">Search for and select Azure Active Directory B2C.</span></span> <span data-ttu-id="10dde-124">만들기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-124">Select Create.</span></span>

![Marketplace 선택](./media/active-directory-b2c-how-to-enable-billing/marketplace.png)

![AD B2C 검색](./media/active-directory-b2c-how-to-enable-billing/searchb2c.png)

<span data-ttu-id="10dde-127">[Azure AD B2C 리소스 만들기] 대화 상자는 다음 매개 변수를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-127">The Azure AD B2C Resource create dialog covers the following parameters:</span></span>

1. <span data-ttu-id="10dde-128">Azure AD B2C 테넌트 - 드롭다운에서 [Azure AD B2C 테넌트]를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-128">Azure AD B2C Tenant – Select an Azure AD B2C Tenant from the dropdown.</span></span>  <span data-ttu-id="10dde-129">적격 Azure AD B2C 테넌트만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-129">Only eligible Azure AD B2C tenants show.</span></span>  <span data-ttu-id="10dde-130">적격 B2C 테넌트는 다음 두 조건을 충족합니다. 사용자가 B2C 테넌트의 전역 관리자이며, B2C 테넌트가 현재 Azure 구독과 연결되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-130">Eligible B2C tenants meet these conditions: You are the global administrator of the B2C tenant, and the B2C tenant is not currently associated to an Azure subscription</span></span>

2. <span data-ttu-id="10dde-131">Azure AD B2C 리소스 이름 - B2C 테넌트의 도메인 이름과 일치하도록 미리 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-131">Azure AD B2C Resource name - is preselected to match the domain name of the B2C Tenant</span></span>

3. <span data-ttu-id="10dde-132">구독 - 관리자이거나 공동 관리자인 활성 Azure 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-132">Subscription - An active Azure subscription in which you are an administrator or a co-administrator.</span></span>  <span data-ttu-id="10dde-133">하나의 Azure 구독에 여러 Azure AD B2C 테넌트를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-133">Multiple Azure AD B2C Tenants may be added to one Azure subscription</span></span>

4. <span data-ttu-id="10dde-134">리소스 그룹 및 리소스 그룹 위치 - 이 아티팩트를 사용하면 여러 Azure 리소스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-134">Resource Group and Resource Group location - This artifact helps you organize multiple Azure resources.</span></span>  <span data-ttu-id="10dde-135">이 선택은 B2C 테넌트 위치, 성능 또는 청구 상태에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-135">This choice has no impact on your B2C tenant location, performance, or billing status</span></span>

5. <span data-ttu-id="10dde-136">대시보드에 고정 - B2C 테넌트 청구 정보 및 B2C 테넌트 설정에 가장 쉽게 액세스할 수 있게 합니다. ![B2C 리소스 만들기](./media/active-directory-b2c-how-to-enable-billing/createresourceb2c.png)</span><span class="sxs-lookup"><span data-stu-id="10dde-136">Pin to dashboard for easiest access to your B2C tenant billing information and the B2C tenant settings ![Create B2C Resource](./media/active-directory-b2c-how-to-enable-billing/createresourceb2c.png)</span></span>

## <a name="step-4---manage-your-b2c-tenant-resources-optional"></a><span data-ttu-id="10dde-137">4단계 - B2C 테넌트 리소스 관리(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="10dde-137">Step 4 - Manage your B2C Tenant resources (optional)</span></span>
<span data-ttu-id="10dde-138">배포가 완료되면 대상 리소스 그룹 및 관련 Azure 구독에 새로운 "B2C 테넌트" 리소스가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-138">Once deployment is complete, a new "B2C Tenant" resource is created in the target resource group and related Azure subscription.</span></span>  <span data-ttu-id="10dde-139">다른 "Azure" 리소스와 함께 추가된 "B2C 테넌트" 유형의 새로운 리소스가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-139">You should see a new resource of type "B2C Tenant" added alongside your other Azure resources.</span></span>

![B2C 리소스 만들기](./media/active-directory-b2c-how-to-enable-billing/b2cresourcedashboard.png)

<span data-ttu-id="10dde-141">B2C 테넌트 리소스를 클릭하면 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-141">By clicking the B2C tenant resource, you are able to</span></span>
- <span data-ttu-id="10dde-142">구독 이름을 클릭하여 청구 정보를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-142">Click Subscription name to review billing information.</span></span> <span data-ttu-id="10dde-143">청구 및 사용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="10dde-143">See Billing & Usage.</span></span>
- <span data-ttu-id="10dde-144">Azure AD B2C 설정을 클릭하여 B2C 테넌트 설정 블레이드에서 직접 새 브라우저 탭을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-144">Click Azure AD B2C Settings to open a new browser tab directly in to your B2C tenant Settings blade</span></span>
- <span data-ttu-id="10dde-145">지원 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-145">Submit a support request</span></span>
- <span data-ttu-id="10dde-146">B2C 테넌트 리소스를 다른 Azure 구독 또는 다른 리소스 그룹으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-146">Move your B2C tenant resource to another Azure Subscription, or to another Resource Group.</span></span>  <span data-ttu-id="10dde-147">사용 요금이 이 선택에 따라 Azure 구독에 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-147">This choice changes which Azure subscription receives usage charges.</span></span>

![B2C 리소스 설정](./media/active-directory-b2c-how-to-enable-billing/b2cresourcesettings.png)

## <a name="known-issues"></a><span data-ttu-id="10dde-149">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="10dde-149">Known Issues</span></span>
- <span data-ttu-id="10dde-150">B2C 테넌트 삭제.</span><span class="sxs-lookup"><span data-stu-id="10dde-150">B2C Tenant deletion.</span></span> <span data-ttu-id="10dde-151">B2C 테넌트를 만들었다가 삭제한 후 동일한 도메인 이름으로 다시 만들 경우 동일한 도메인 이름을 사용하여 "연결" 리소스를 삭제한 후 다시 만드세요.</span><span class="sxs-lookup"><span data-stu-id="10dde-151">If a B2C Tenant is created, deleted, and re-created with the same domain name, please also delete and re-create the "Linking" resource with the same domain name.</span></span>  <span data-ttu-id="10dde-152">Azure Portal을 통해 구독 테넌트의 "모든 리소스"에서 이 "연결" 리소스를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-152">You will find this "Linking" resource under "All resources" in the subscription tenant via the Azure portal.</span></span>
- <span data-ttu-id="10dde-153">지역별 리소스 위치에 자체적인 제한 적용.</span><span class="sxs-lookup"><span data-stu-id="10dde-153">Self-imposed restrictions on regional resource location.</span></span>  <span data-ttu-id="10dde-154">드물지만 사용자가 Azure 리소스 만들기에 대해 지역별 제한을 구축했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-154">In rare cases, a user may have established a regional restriction for Azure resource creation.</span></span>  <span data-ttu-id="10dde-155">이 제한 때문에 Azure 구독과 테넌트 B2C 간에 연결을 만들지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-155">This restriction may prevent the creation of the Link between an Azure subscription and a B2C Tenant.</span></span> <span data-ttu-id="10dde-156">유연하게 작업하려면 이러한 제한을 완화하세요.</span><span class="sxs-lookup"><span data-stu-id="10dde-156">To mitigate, please relax this restriction.</span></span>

## <a name="next-steps"></a><span data-ttu-id="10dde-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="10dde-157">Next steps</span></span>
<span data-ttu-id="10dde-158">각 B2C 테넌트에 대해 이러한 단계가 완료되면 Azure 직접 또는 기업 계약 세부 정보에 따라 비용이 Azure 구독에 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="10dde-158">Once these steps are complete for each of your B2C tenants, your Azure subscription is billed in accordance with your Azure Direct or Enterprise Agreement details.</span></span>
- <span data-ttu-id="10dde-159">Azure 구독을 선택한 상태에서 사용 현황 및 청구 검토</span><span class="sxs-lookup"><span data-stu-id="10dde-159">Review usage and billing within your selected Azure subscription</span></span>
- <span data-ttu-id="10dde-160">[사용 현황 보고 API](active-directory-b2c-reference-usage-reporting-api.md)를 사용하여 자세한 일일 사용 현황 보고서 검토</span><span class="sxs-lookup"><span data-stu-id="10dde-160">Review detailed day-by-day usage reports using the [Usage Reporting API](active-directory-b2c-reference-usage-reporting-api.md)</span></span>
