---
title: "Azure Active Directory 테넌트 상호 작용의 특징 | Microsoft Docs"
description: "완전히 독립적인 리소스로 테넌트를 파악하여 Azure Active Directory 테넌트 관리"
services: active-tenant
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 2b862b75-14df-45f2-a8ab-2a3ff1e2eb08
ms.service: active-tenant
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/27/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017;it-pro
ms.reviewer: piotrci
ms.openlocfilehash: d25d2c731034d0785bbd404ec693c4c41d913d01
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a><span data-ttu-id="e015e-103">여러 Azure Active Directory 테넌트 간의 상호 작용 방식 이해</span><span class="sxs-lookup"><span data-stu-id="e015e-103">Understand how multiple Azure Active Directory tenants interact</span></span>

<span data-ttu-id="e015e-104">Azure AD(Azure Active Directory)의 각 테넌트는 완전히 독립된 리소스로, 관리하는 다른 테넌트와 논리적으로 독립된 피어입니다.</span><span class="sxs-lookup"><span data-stu-id="e015e-104">In Azure Active Directory (Azure AD), each tenent is a fully independent resource: a peer that is logically independent from the other tenants that you manage.</span></span> <span data-ttu-id="e015e-105">또한 테넌트 간에는 부모-자식 관계가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e015e-105">There is no parent-child relationship between tenants.</span></span> <span data-ttu-id="e015e-106">테넌트 간 독립성에는 리소스 독립성, 관리 독립성 및 동기화 독립성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e015e-106">This independence between tenants includes resource independence, administrative independence, and synchronization independence.</span></span>

## <a name="resource-independence"></a><span data-ttu-id="e015e-107">리소스 독립성</span><span class="sxs-lookup"><span data-stu-id="e015e-107">Resource independence</span></span>
* <span data-ttu-id="e015e-108">한 테넌트에서 리소스를 만들거나 삭제해도 다른 테넌트의 리소스에 영향을 주지 않습니다. 단, 외부 사용자는 부분적으로 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="e015e-108">If you create or delete a resource in one tenant, it has no impact on any resource in another tenant, with the partial exception of external users.</span></span> 
* <span data-ttu-id="e015e-109">단일 테넌트에서 도메인 이름 중 하나를 사용하는 경우 다른 테넌트를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e015e-109">If you use one of your domain names with one tenant, it cannot be used with any other tenant.</span></span>

## <a name="administrative-independence"></a><span data-ttu-id="e015e-110">관리 독립성</span><span class="sxs-lookup"><span data-stu-id="e015e-110">Administrative independence</span></span>
<span data-ttu-id="e015e-111">'Contoso' 테넌트의 관리자가 아닌 사용자가 테스트 테넌트 'Test'를 만들면 다음과 같이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e015e-111">If a non-administrative user of tenant 'Contoso' creates a test tenant 'Test,' then:</span></span>

* <span data-ttu-id="e015e-112">기본적으로 테넌트를 만드는 사용자는 해당하는 새 테넌트에서 외부 사용자로 추가되고 해당 테넌트의 전역 관리자 역할이 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="e015e-112">By default, the user who creates a tenant is added as an external user in that new tenant, and assigned the global administrator role in that tenant.</span></span>
* <span data-ttu-id="e015e-113">'Test'의 관리자가 'Test' 테넌트에 대한 관리 권한을 특별히 부여하지 않으면 'Contoso' 테넌트의 관리자는 이 디렉터리에 대한 직접 관리 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e015e-113">The administrators of tenant 'Contoso' have no direct administrative privileges to tenant 'Test,' unless an administrator of 'Test' specifically grants them these privileges.</span></span> <span data-ttu-id="e015e-114">그러나 'Contoso'의 관리자가 'Test'를 만든 사용자 계정을 제어하는 경우 'Test' 테넌트에 대한 액세스를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e015e-114">However, administrators of 'Contoso' can control access to tenant 'Test' if they control the user account that created 'Test.'</span></span>
* <span data-ttu-id="e015e-115">단일 테넌트의 사용자에 관리자 역할을 추가/제거하는 경우 변경은 다른 테넌트에서 사용자가 가진 관리자 역할에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e015e-115">If you add/remove an administrator role for a user in one tenant, the change does not affect the administrator roles that the user has in another tenant.</span></span>

## <a name="synchronization-independence"></a><span data-ttu-id="e015e-116">동기화 독립성</span><span class="sxs-lookup"><span data-stu-id="e015e-116">Synchronization independence</span></span>
<span data-ttu-id="e015e-117">각 Azure AD 테넌트를 독립적으로 구성하여 다음 중 하나의 단일 인스턴스에서 데이터를 동기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e015e-117">You can configure each Azure AD tenant independently to get data synchronized from a single instance of either:</span></span>

* <span data-ttu-id="e015e-118">데이터를 단일 AD 포리스트와 동기화하는 Azure AD Connect 도구</span><span class="sxs-lookup"><span data-stu-id="e015e-118">The Azure AD Connect tool, to synchronize data with a single AD forest.</span></span>
* <span data-ttu-id="e015e-119">데이터를 하나 이상의 온-프레미스 포리스트 및/또는 Azure AD 이외의 데이터 원본과 동기화하는 Forefront Identity Manager용 Azure Active 테넌트 커넥터</span><span class="sxs-lookup"><span data-stu-id="e015e-119">The Azure Active tenant Connector for Forefront Identity Manager, to synchronize data with one or more on-premises forests, and/or non-Azure AD data sources.</span></span>

## <a name="add-an-azure-ad-tenant"></a><span data-ttu-id="e015e-120">Azure AD 테넌트 추가</span><span class="sxs-lookup"><span data-stu-id="e015e-120">Add an Azure AD tenant</span></span>
<span data-ttu-id="e015e-121">Azure Portal에서 Azure AD 테넌트를 추가하려면 Azure AD 전역 관리자인 계정으로 [Azure Portal](https://portal.azure.com)에 로그인하고 왼쪽에서 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e015e-121">To add an Azure AD tenant in the Azure portal, sign in to [the Azure portal](https://portal.azure.com) with an account that is an Azure AD global administrator, and, on the left, select **New**.</span></span>

> [!NOTE]
> <span data-ttu-id="e015e-122">다른 Azure 리소스와 달리 테넌트는 Azure 구독의 자식 리소스가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e015e-122">Unlike other Azure resources, your tenants are not child resources of an Azure subscription.</span></span> <span data-ttu-id="e015e-123">Azure 구독이 취소되거나 만료되는 경우 Azure PowerShell, Azure Graph API 또는 Office 365 관리 센터를 사용하여 테넌트 데이터에 계속 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e015e-123">If your Azure subscription is canceled or expired, you can still access your tenant data using Azure PowerShell, the Azure Graph API, or the Office 365 Admin Center.</span></span> <span data-ttu-id="e015e-124">다른 구독을 테넌트와 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e015e-124">You can also associate another subscription with the tenant.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="e015e-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e015e-125">Next steps</span></span>
<span data-ttu-id="e015e-126">Azure AD 라이선스 문제 및 모범 사례에 대한 광범위한 개요는 [Azure Active 테넌트 라이선스란?](active-directory-licensing-whatis-azure-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e015e-126">For a broad overview of Azure AD licensing issues and best practices, see [What is Azure Active tenant licensing?](active-directory-licensing-whatis-azure-portal.md)</span></span>
