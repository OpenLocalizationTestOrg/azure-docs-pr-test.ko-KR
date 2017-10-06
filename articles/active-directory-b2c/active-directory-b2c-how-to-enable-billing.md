---
title: "Azure 구독 tooAzure AD B2C aaaHow tooLink | Microsoft Docs"
description: "Azure AD B2C 테 넌 트에 대 한 tooenable 청구 단계별 가이드를 Azure 구독에 있습니다."
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
ms.openlocfilehash: 07b2ed5f7f5f543c9cbb8e9a35107462448e9440
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="linking-an-azure-subscription-tooan-azure-b2c-tenant-toopay-for-usage-charges"></a><span data-ttu-id="41162-103">Azure 구독 tooan Azure B2C 테 넌 트 toopay 사용 요금에 대 한 연결</span><span class="sxs-lookup"><span data-stu-id="41162-103">Linking an Azure Subscription tooan Azure B2C tenant toopay for usage charges</span></span>

<span data-ttu-id="41162-104">Azure Active Directory B2C (또는 Azure AD B2C)에 대 한 지속적인 사용 요금 청구 tooan Azure 구독 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41162-104">Ongoing usage charges for Azure Active Directory B2C (or Azure AD B2C) are billed tooan Azure Subscription.</span></span> <span data-ttu-id="41162-105">Hello 테 넌 트 관리자 tooexplicitly 링크 hello Azure AD B2C 테 넌 트 tooan 자체 hello B2C 테 넌 트를 만든 후 Azure 구독에 대 한 필요는.</span><span class="sxs-lookup"><span data-stu-id="41162-105">It is necessary for hello tenant administrator tooexplicitly link hello Azure AD B2C tenant tooan Azure subscription after creating hello B2C tenant itself.</span></span>  <span data-ttu-id="41162-106">이 링크는 Azure AD "B2C 테 넌 트"를 만들어 구현할 hello 대상 Azure 구독에에서 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="41162-106">This link is achieved by creating an Azure AD "B2C Tenant" resource in hello target Azure subscription.</span></span> <span data-ttu-id="41162-107">많은 B2C 테 넌 트가 다른 Azure 리소스 (예: Vm, 데이터 저장소, LogicApps)와 함께 연결 된 tooa 단일 Azure 구독 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41162-107">Many B2C tenants can be linked tooa single Azure subscription along with other Azure resources (for example, VMs, Data storage, LogicApps)</span></span>


> [!IMPORTANT]
> <span data-ttu-id="41162-108">사용 대금 청구 및 B2C hello 페이지 다음에 가격 책정에 대 한 최신 정보를 hello: [Azure AD B2C 가격 책정](
https://azure.microsoft.com/pricing/details/active-directory-b2c/)</span><span class="sxs-lookup"><span data-stu-id="41162-108">hello latest information on usage billing and pricing for B2C is at hello following page: [Azure AD B2C Pricing](
https://azure.microsoft.com/pricing/details/active-directory-b2c/)</span></span>

## <a name="step-1---create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="41162-109">1단계 - Azure AD B2C 테넌트 만들기</span><span class="sxs-lookup"><span data-stu-id="41162-109">Step 1 - Create an Azure AD B2C Tenant</span></span>
<span data-ttu-id="41162-110">먼저 B2C 테넌트 만들기를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41162-110">B2C tenant creation must be completed first.</span></span> <span data-ttu-id="41162-111">이미 대상 B2C 테넌트를 만든 경우에는 이 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="41162-111">Skip this step if you have already created your target B2C Tenant.</span></span> [<span data-ttu-id="41162-112">Azure AD B2C 시작</span><span class="sxs-lookup"><span data-stu-id="41162-112">Get started with Azure AD B2C</span></span>](active-directory-b2c-get-started.md)

## <a name="step-2---open-azure-portal-in-hello-azure-ad-tenant-that-shows-your-azure-subscription"></a><span data-ttu-id="41162-113">2 단계-Azure AD 테 넌 트 Azure 구독을 보여 주는 hello에 Azure 포털 열기</span><span class="sxs-lookup"><span data-stu-id="41162-113">Step 2 - Open Azure portal in hello Azure AD Tenant that shows your Azure subscription</span></span>
<span data-ttu-id="41162-114">Toohello 이동 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="41162-114">Navigate toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="41162-115">Azure AD 테 넌 트 hello toouse 원하는 Azure 구독을 보여 주는 toohello를 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="41162-115">Switch toohello Azure AD Tenant that shows hello Azure subscription you would like toouse.</span></span> <span data-ttu-id="41162-116">이 Azure AD 테 넌 트는 hello B2C 테 넌 트와에서 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="41162-116">This Azure AD tenant is different from hello B2C tenant.</span></span> <span data-ttu-id="41162-117">Hello Azure 포털 내에서 hello hello 대시보드 tooselect hello Azure AD 테 넌 트의 오른쪽 위에 hello 계정 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="41162-117">Within hello Azure portal, click hello account name on hello upper right of hello dashboard tooselect hello Azure AD Tenant.</span></span> <span data-ttu-id="41162-118">Azure 구독에 필요한 tooproceed입니다.</span><span class="sxs-lookup"><span data-stu-id="41162-118">An Azure subscription is needed tooproceed.</span></span> [<span data-ttu-id="41162-119">Azure 구독 가져오기</span><span class="sxs-lookup"><span data-stu-id="41162-119">Get an Azure Subscription</span></span>](https://account.windowsazure.com/signup?showCatalog=True)

![Azure AD 테 넌 트 tooyour 전환](./media/active-directory-b2c-how-to-enable-billing/SelectAzureADTenant.png)

## <a name="step-3---create-a-b2c-tenant-resource-in-azure-marketplace"></a><span data-ttu-id="41162-121">3단계 - Azure Marketplace에서 B2C 테넌트 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="41162-121">Step 3 - Create a B2C Tenant resource in Azure Marketplace</span></span>
<span data-ttu-id="41162-122">마켓플레이스 hello hello 대시보드의 맨 왼쪽된 위에 있는 hello 마켓플레이스 아이콘을 클릭 하거나 hello 녹색 "+"를 선택 하 여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="41162-122">Open Marketplace by clicking hello Marketplace icon, or selecting hello green "+" in hello upper left corner of hello dashboard.</span></span>  <span data-ttu-id="41162-123">Azure Active Directory B2C를 검색하고 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="41162-123">Search for and select Azure Active Directory B2C.</span></span> <span data-ttu-id="41162-124">만들기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="41162-124">Select Create.</span></span>

![Marketplace 선택](./media/active-directory-b2c-how-to-enable-billing/marketplace.png)

![AD B2C 검색](./media/active-directory-b2c-how-to-enable-billing/searchb2c.png)

<span data-ttu-id="41162-127">hello Azure AD B2C 리소스 만들기 대화 상자에서는 hello 매개 변수 뒤:</span><span class="sxs-lookup"><span data-stu-id="41162-127">hello Azure AD B2C Resource create dialog covers hello following parameters:</span></span>

1. <span data-ttu-id="41162-128">Azure AD B2C 테 넌 트-hello 드롭다운에서 Azure AD B2C 테 넌 트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="41162-128">Azure AD B2C Tenant – Select an Azure AD B2C Tenant from hello dropdown.</span></span>  <span data-ttu-id="41162-129">적격 Azure AD B2C 테넌트만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="41162-129">Only eligible Azure AD B2C tenants show.</span></span>  <span data-ttu-id="41162-130">적격 B2C 테 넌 트에는 다음이 조건을 충족: hello, hello B2C 테 넌 트의 전역 관리자가 아니며 hello B2C 테 넌 트에 현재 연결된 tooan Azure 구독</span><span class="sxs-lookup"><span data-stu-id="41162-130">Eligible B2C tenants meet these conditions: You are hello global administrator of hello B2C tenant, and hello B2C tenant is not currently associated tooan Azure subscription</span></span>

2. <span data-ttu-id="41162-131">Azure AD B2C 리소스 이름-은 hello B2C 테 넌 트의 미리 선택 된 toomatch hello 도메인 이름</span><span class="sxs-lookup"><span data-stu-id="41162-131">Azure AD B2C Resource name - is preselected toomatch hello domain name of hello B2C Tenant</span></span>

3. <span data-ttu-id="41162-132">구독 - 관리자이거나 공동 관리자인 활성 Azure 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="41162-132">Subscription - An active Azure subscription in which you are an administrator or a co-administrator.</span></span>  <span data-ttu-id="41162-133">여러 Azure AD B2C 테 넌 트 tooone Azure 구독을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41162-133">Multiple Azure AD B2C Tenants may be added tooone Azure subscription</span></span>

4. <span data-ttu-id="41162-134">리소스 그룹 및 리소스 그룹 위치 - 이 아티팩트를 사용하면 여러 Azure 리소스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41162-134">Resource Group and Resource Group location - This artifact helps you organize multiple Azure resources.</span></span>  <span data-ttu-id="41162-135">이 선택은 B2C 테넌트 위치, 성능 또는 청구 상태에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41162-135">This choice has no impact on your B2C tenant location, performance, or billing status</span></span>

5. <span data-ttu-id="41162-136">쉬운 액세스 tooyour B2C 테 넌 트 청구 정보 및 hello B2C 테 넌 트 설정에 대 한 toodashboard 고정 ![B2C 리소스 만들기](./media/active-directory-b2c-how-to-enable-billing/createresourceb2c.png)</span><span class="sxs-lookup"><span data-stu-id="41162-136">Pin toodashboard for easiest access tooyour B2C tenant billing information and hello B2C tenant settings ![Create B2C Resource](./media/active-directory-b2c-how-to-enable-billing/createresourceb2c.png)</span></span>

## <a name="step-4---manage-your-b2c-tenant-resources-optional"></a><span data-ttu-id="41162-137">4단계 - B2C 테넌트 리소스 관리(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="41162-137">Step 4 - Manage your B2C Tenant resources (optional)</span></span>
<span data-ttu-id="41162-138">배포가 완료 되 면 관련 Azure 구독 및는 "B2C 테 넌 트" 리소스를 새 hello 대상 리소스 그룹에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41162-138">Once deployment is complete, a new "B2C Tenant" resource is created in hello target resource group and related Azure subscription.</span></span>  <span data-ttu-id="41162-139">다른 "Azure" 리소스와 함께 추가된 "B2C 테넌트" 유형의 새로운 리소스가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="41162-139">You should see a new resource of type "B2C Tenant" added alongside your other Azure resources.</span></span>

![B2C 리소스 만들기](./media/active-directory-b2c-how-to-enable-billing/b2cresourcedashboard.png)

<span data-ttu-id="41162-141">수 있는 hello B2C 테 넌 트 리소스를 클릭 하면</span><span class="sxs-lookup"><span data-stu-id="41162-141">By clicking hello B2C tenant resource, you are able to</span></span>
- <span data-ttu-id="41162-142">구독 이름 tooreview 청구 정보를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="41162-142">Click Subscription name tooreview billing information.</span></span> <span data-ttu-id="41162-143">청구 및 사용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41162-143">See Billing & Usage.</span></span>
- <span data-ttu-id="41162-144">Azure AD B2C 설정 tooopen tooyour B2C 테 넌 트 설정 블레이드에서에서 직접 새 브라우저 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="41162-144">Click Azure AD B2C Settings tooopen a new browser tab directly in tooyour B2C tenant Settings blade</span></span>
- <span data-ttu-id="41162-145">지원 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="41162-145">Submit a support request</span></span>
- <span data-ttu-id="41162-146">프로그램 B2C 테 넌 트 리소스 tooanother 이동 Azure 구독 또는 리소스 그룹 tooanother 합니다.</span><span class="sxs-lookup"><span data-stu-id="41162-146">Move your B2C tenant resource tooanother Azure Subscription, or tooanother Resource Group.</span></span>  <span data-ttu-id="41162-147">사용 요금이 이 선택에 따라 Azure 구독에 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="41162-147">This choice changes which Azure subscription receives usage charges.</span></span>

![B2C 리소스 설정](./media/active-directory-b2c-how-to-enable-billing/b2cresourcesettings.png)

## <a name="known-issues"></a><span data-ttu-id="41162-149">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="41162-149">Known Issues</span></span>
- <span data-ttu-id="41162-150">B2C 테넌트 삭제.</span><span class="sxs-lookup"><span data-stu-id="41162-150">B2C Tenant deletion.</span></span> <span data-ttu-id="41162-151">B2C 테 넌 트를 만든 경우 삭제 하 고 다시 사용 하 여 만든 동일한 도메인 이름을 hello도 삭제 하십시오 hello 사용 하 여 hello "연결" 리소스를 다시 만드는 동일한 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="41162-151">If a B2C Tenant is created, deleted, and re-created with hello same domain name, please also delete and re-create hello "Linking" resource with hello same domain name.</span></span>  <span data-ttu-id="41162-152">"모든 리소스" 아래에서 리소스를 hello Azure 포털을 통해 hello 구독 테 넌 트의 "연결" 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41162-152">You will find this "Linking" resource under "All resources" in hello subscription tenant via hello Azure portal.</span></span>
- <span data-ttu-id="41162-153">지역별 리소스 위치에 자체적인 제한 적용.</span><span class="sxs-lookup"><span data-stu-id="41162-153">Self-imposed restrictions on regional resource location.</span></span>  <span data-ttu-id="41162-154">드물지만 사용자가 Azure 리소스 만들기에 대해 지역별 제한을 구축했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41162-154">In rare cases, a user may have established a regional restriction for Azure resource creation.</span></span>  <span data-ttu-id="41162-155">이 제한 사항은 Azure 구독 및 B2C 테 넌 트 간의 링크 hello hello 생성이 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41162-155">This restriction may prevent hello creation of hello Link between an Azure subscription and a B2C Tenant.</span></span> <span data-ttu-id="41162-156">toomitigate,이 제한 사항은 완화 하세요.</span><span class="sxs-lookup"><span data-stu-id="41162-156">toomitigate, please relax this restriction.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41162-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="41162-157">Next steps</span></span>
<span data-ttu-id="41162-158">각 B2C 테넌트에 대해 이러한 단계가 완료되면 Azure 직접 또는 기업 계약 세부 정보에 따라 비용이 Azure 구독에 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="41162-158">Once these steps are complete for each of your B2C tenants, your Azure subscription is billed in accordance with your Azure Direct or Enterprise Agreement details.</span></span>
- <span data-ttu-id="41162-159">Azure 구독을 선택한 상태에서 사용 현황 및 청구 검토</span><span class="sxs-lookup"><span data-stu-id="41162-159">Review usage and billing within your selected Azure subscription</span></span>
- <span data-ttu-id="41162-160">Hello를 사용 하 여 자세한 날짜별으로 사용 현황 보고서를 검토 [사용 현황 보고 API](active-directory-b2c-reference-usage-reporting-api.md)</span><span class="sxs-lookup"><span data-stu-id="41162-160">Review detailed day-by-day usage reports using hello [Usage Reporting API](active-directory-b2c-reference-usage-reporting-api.md)</span></span>
