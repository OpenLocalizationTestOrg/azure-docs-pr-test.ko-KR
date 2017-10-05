---
title: "Privileged Identity Management 구독 - Azure | Microsoft Docs"
description: "테넌트에서 Azure AD Privileged Identity Management를 관리하고 사용하기 위한 구독 및 라이선스 요구 사항에 대해 설명합니다."
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: mwahl
ms.assetid: 34367721-8b42-4fab-a443-a2e55cdbf33d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: 62d8f80fa1bec3a1b75e316f0b0ee7be8cbefbff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-privileged-identity-management-subscription-requirements"></a><span data-ttu-id="1aef2-103">Azure Active Directory Privileged Identity Management 구독 요구 사항</span><span class="sxs-lookup"><span data-stu-id="1aef2-103">Azure Active Directory Privileged Identity Management subscription requirements</span></span>

<span data-ttu-id="1aef2-104">Azure AD Privileged Identity Management는 Azure AD의 Premium P2 버전의 일부로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aef2-104">Azure AD Privileged Identity Management is available as part of the Premium P2 edition of Azure AD.</span></span> <span data-ttu-id="1aef2-105">P2의 다른 기능과 Premium P1과 비교한 결과에 대한 자세한 내용은 [Azure Active Directory 버전](../active-directory-editions.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1aef2-105">For more information on the other features of P2 and how it compares to Premium P1, see [Azure Active Directory editions](../active-directory-editions.md).</span></span>

>[!NOTE]
<span data-ttu-id="1aef2-106">Azure AD(Azure Active Directory) Privileged Identity Management가 미리 보기로 제공될 때는 테넌트가 서비스를 시도할 때 라이선스가 확인되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="1aef2-106">When Azure Active Directory (Azure AD) Privileged Identity Management was in preview, there were no license checks for a tenant to try the service.</span></span>  <span data-ttu-id="1aef2-107">현재 Azure AD Privileged Identity Management가 일반 공급되므로 2016년 12월부터는 테넌트에서 Privileged Identity Management를 사용하려면 평가판 또는 유료 구독이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aef2-107">Now that Azure AD Privileged Identity Management has reached general availability, a trial or paid subscription must be present for the tenant to continue using Privileged Identity Management after December 2016.</span></span>
  

## <a name="confirm-your-trial-or-paid-subscription"></a><span data-ttu-id="1aef2-108">평가판 또는 유료 구독 확인</span><span class="sxs-lookup"><span data-stu-id="1aef2-108">Confirm your trial or paid subscription</span></span>

<span data-ttu-id="1aef2-109">조직에 평가판 또는 유료 구독이 있는지 잘 모를 경우 확실 하지 않은 Windows PowerShell V1용 Azure Active Directory 모듈에 포함된 명령을 사용하여 테넌트에 구독이 있는지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aef2-109">If you're not sure whether your organization has a trial or purchased subscription, then you can check whether there is a subscription in your tenant by using the commands included in Azure Active Directory Module for Windows PowerShell V1.</span></span> 
1. <span data-ttu-id="1aef2-110">PowerShell 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1aef2-110">Open a PowerShell window.</span></span>
2. <span data-ttu-id="1aef2-111">`Connect-MsolService`를 입력하여 테넌트의 사용자로 인증을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="1aef2-111">Enter `Connect-MsolService` to authenticate as a user in your tenant.</span></span>
3. <span data-ttu-id="1aef2-112">`Get-MsolSubscription | ft SkuPartNumber,IsTrial,Status`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1aef2-112">Enter `Get-MsolSubscription | ft SkuPartNumber,IsTrial,Status`.</span></span>

<span data-ttu-id="1aef2-113">이 명령은 테넌트의 구독 목록을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="1aef2-113">This command retrieves a list of the subscriptions in your tenant.</span></span> <span data-ttu-id="1aef2-114">반환되는 줄이 없으면 Azure AD Premium P2 평가판을 구하거나 Azure AD Premium P2 구독 또는 EMS E5 구독이 구매해야 Azure AD Privileged Identity Management를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aef2-114">If there are no lines returned, you will need to obtain an Azure AD Premium P2 trial, purchase an Azure AD Premium P2 subscription or EMS E5 subscription to use Azure AD Privileged Identity Management.</span></span>  <span data-ttu-id="1aef2-115">평가판을 구하고 Azure AD Privileged Identity Management 사용을 시작하려면 [Azure AD Privileged Identity Management 시작](../active-directory-privileged-identity-management-getting-started.md)을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="1aef2-115">To get a trial and start using Azure AD Privileged Identity Management, read [Get started with Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md).</span></span>

<span data-ttu-id="1aef2-116">이 명령이 SkuPartNumber가 "AAD_PREMIUM_P2"이거나 "EMSPREMIUM"이고 IsTrial이 "True"인 줄을 반환하는 경우 Azure AD Premium P2 평가판이 테넌트에 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1aef2-116">If this command returns a line in which SkuPartNumber is "AAD_PREMIUM_P2" or "EMSPREMIUM" and IsTrial is "True", this indicates an Azure AD Premium P2 trial is present in the tenant.</span></span>  <span data-ttu-id="1aef2-117">구독 상태를 사용하도록 설정하지 않고 Azure AD Premium P2 또는 EMS E5 구독을 구매하지 않은 경우 Azure AD Privileged Identity Management를 계속 사용하려면 Azure AD Premium P2 구독 또는 EMS E5 구독을 구입해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aef2-117">If the subscription status is not enabled, and you do not have an Azure AD Premium P2 or EMS E5 subscription purchase, then you must purchase an Azure AD Premium P2 subscription or EMS E5 subscription to continue using Azure AD Privileged Identity Management.</span></span>

<span data-ttu-id="1aef2-118">Azure AD Premium P2는 [Microsoft 기업계약](https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx), [오픈 볼륨 라이선스 프로그램](https://www.microsoft.com/en-us/licensing/licensing-programs/open-license.aspx) 및 [클라우드 솔루션 공급자](https://partner.microsoft.com/en-US/cloud-solution-provider) 프로그램을 통해 구입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aef2-118">Azure AD Premium P2 is available through a [Microsoft Enterprise Agreement](https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx), the [Open Volume License Program](https://www.microsoft.com/en-us/licensing/licensing-programs/open-license.aspx), and the [Cloud Solution Providers program](https://partner.microsoft.com/en-US/cloud-solution-provider).</span></span> <span data-ttu-id="1aef2-119">또한 Azure 및 Office 365 구독자는 Azure AD Premium P2를 온라인으로 구입할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aef2-119">Azure and Office 365 subscribers can also buy Azure AD Premium P2 online.</span></span>  <span data-ttu-id="1aef2-120">Azure AD Premium 가격 책정 및 온라인 주문 방법에 대한 자세한 내용은 [Azure Active Directory 가격 책정](https://azure.microsoft.com/en-us/pricing/details/active-directory/)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aef2-120">More information on Azure AD Premium pricing and how to order online can be found at [Azure Active Directory Pricing](https://azure.microsoft.com/en-us/pricing/details/active-directory/).</span></span>

## <a name="azure-ad-privileged-identity-management-is-not-available-in-tenant"></a><span data-ttu-id="1aef2-121">Azure AD Privileged Identity Management를 테넌트에서 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="1aef2-121">Azure AD Privileged Identity Management is not available in tenant</span></span>

<span data-ttu-id="1aef2-122">다음과 같은 경우 Azure AD Privileged Identity Management를 테넌트에서 더 이상 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1aef2-122">Azure AD Privileged Identity Management will no longer be available in your tenant if:</span></span>
- <span data-ttu-id="1aef2-123">조직이 미리 보기 상태이며 Azure AD Premium P2 구독 또는 EMS E5 구독을 구입하지 않은 상태에서 Azure AD Privileged Identity Management를 사용하고 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="1aef2-123">Your organization was using Azure AD Privileged Identity Management when it was in preview and does not purchase Azure AD Premium P2 subscription or EMS E5 subscription.</span></span>
- <span data-ttu-id="1aef2-124">조직이 만료된 Azure AD Premium P2 또는 EMS E5 평가판을 보유하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aef2-124">Your organization had an Azure AD Premium P2 or EMS E5 trial that expired.</span></span>
- <span data-ttu-id="1aef2-125">조직이 구입한 구독이 만료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1aef2-125">Your organization had a purchased subscription that expired.</span></span>

<span data-ttu-id="1aef2-126">Azure AD Premium P2 구독 또는 EMS E5 구독이 만료되거나 미리 보기의 Azure AD Privileged Identity Management를 사용하던 조직이 Azure AD Premium P2 또는 EMS E5 구독을 구입하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="1aef2-126">When an Azure AD Premium P2 subscription or EMS E5 subscription expires, or an organization that was using Azure AD Privileged Identity Management in preview does not obtain Azure AD Premium P2 or EMS E5 subscription:</span></span>

- <span data-ttu-id="1aef2-127">Azure AD 역할에 대한 영구 역할 할당은 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1aef2-127">Permanent role assignments to Azure AD roles will be unaffected.</span></span>
- <span data-ttu-id="1aef2-128">사용자가 권한 있는 역할을 활성화하거나, 권한 있는 액세스를 관리하거나, 권한 있는 역할의 액세스 검토를 수행하기 위해 더 이상 Azure Portal의 Azure AD Privileged Identity Management 확장과 Azure AD Privileged Identity Management의 Graph API cmdlet 및 PowerShell 인터페이스를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1aef2-128">The Azure AD Privileged Identity Management extension in the Azure portal, as well as the Graph API cmdlets and PowerShell interfaces of Azure AD Privileged Identity Management, will no longer be available for users to activate privileged roles, manage privileged access, or perform access reviews of privileged roles.</span></span>
- <span data-ttu-id="1aef2-129">사용자가 더 이상 권한 있는 역할을 활성화할 수 없으므로 Azure AD 역할의 적격 역할 할당이 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aef2-129">Eligible role assignments of Azure AD roles will be removed, as users will no longer be able to activate privileged roles.</span></span>
- <span data-ttu-id="1aef2-130">Azure AD 역할에 대해 진행 중인 모든 액세스 검토가 종료되고 Azure AD Privileged Identity Management 구성 설정이 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aef2-130">Any ongoing access reviews of Azure AD roles will end, and Azure AD Privileged Identity Management configuration settings will be removed.</span></span>
- <span data-ttu-id="1aef2-131">Azure AD Privileged Identity Management는 더 이상 역할 할당 변경에 대한 전자 메일을 전송하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1aef2-131">Azure AD Privileged Identity Management will no longer send emails on role assignment changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1aef2-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1aef2-132">Next steps</span></span>

- [<span data-ttu-id="1aef2-133">Azure AD Privileged Identity Management 시작</span><span class="sxs-lookup"><span data-stu-id="1aef2-133">Get started with Azure AD Privileged Identity Management</span></span>](../active-directory-privileged-identity-management-getting-started.md)
- [<span data-ttu-id="1aef2-134">Azure AD Privileged Identity Management의 역할</span><span class="sxs-lookup"><span data-stu-id="1aef2-134">Roles in Azure AD Privileged Identity Management</span></span>](../active-directory-privileged-identity-management-roles.md)
