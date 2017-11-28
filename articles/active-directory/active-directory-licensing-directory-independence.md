---
title: "Azure Active Directory의 aaaCharacteristics intercaction 테 넌 트 | Microsoft Docs"
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
ms.openlocfilehash: 57b677665c7cb4aee63f518c39d26754fe71a999
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a><span data-ttu-id="2c6f8-103">여러 Azure Active Directory 테넌트 간의 상호 작용 방식 이해</span><span class="sxs-lookup"><span data-stu-id="2c6f8-103">Understand how multiple Azure Active Directory tenants interact</span></span>

<span data-ttu-id="2c6f8-104">각 테 넌 트 Azure Active Directory (Azure AD)에 완전 한 독립 리소스:와 논리적으로 별도의 피어 hello 관리 하는 다른 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="2c6f8-104">In Azure Active Directory (Azure AD), each tenent is a fully independent resource: a peer that is logically independent from hello other tenants that you manage.</span></span> <span data-ttu-id="2c6f8-105">또한 테넌트 간에는 부모-자식 관계가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2c6f8-105">There is no parent-child relationship between tenants.</span></span> <span data-ttu-id="2c6f8-106">테넌트 간 독립성에는 리소스 독립성, 관리 독립성 및 동기화 독립성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c6f8-106">This independence between tenants includes resource independence, administrative independence, and synchronization independence.</span></span>

## <a name="resource-independence"></a><span data-ttu-id="2c6f8-107">리소스 독립성</span><span class="sxs-lookup"><span data-stu-id="2c6f8-107">Resource independence</span></span>
* <span data-ttu-id="2c6f8-108">만들거나 한 테 넌 트에 리소스를 삭제 하는 경우 외부 사용자의 hello 부분 예외와 함께 다른 테 넌 트의 리소스에 영향을 주어에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c6f8-108">If you create or delete a resource in one tenant, it has no impact on any resource in another tenant, with hello partial exception of external users.</span></span> 
* <span data-ttu-id="2c6f8-109">단일 테넌트에서 도메인 이름 중 하나를 사용하는 경우 다른 테넌트를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2c6f8-109">If you use one of your domain names with one tenant, it cannot be used with any other tenant.</span></span>

## <a name="administrative-independence"></a><span data-ttu-id="2c6f8-110">관리 독립성</span><span class="sxs-lookup"><span data-stu-id="2c6f8-110">Administrative independence</span></span>
<span data-ttu-id="2c6f8-111">'Contoso' 테넌트의 관리자가 아닌 사용자가 테스트 테넌트 'Test'를 만들면 다음과 같이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c6f8-111">If a non-administrative user of tenant 'Contoso' creates a test tenant 'Test,' then:</span></span>

* <span data-ttu-id="2c6f8-112">기본적으로 hello 만드는 사용자에 게 테 넌 트는 새 테 넌 트 및 해당 테 넌 트의 전역 관리자 역할 할당 된 hello 해당 외부 사용자로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c6f8-112">By default, hello user who creates a tenant is added as an external user in that new tenant, and assigned hello global administrator role in that tenant.</span></span>
* <span data-ttu-id="2c6f8-113">'Contoso' 테 넌 트의 관리자 hello 's t'의 관리자 구체적으로 부여 이러한 권한이 없는 직접 관리 권한이 tootenant 'Test' 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c6f8-113">hello administrators of tenant 'Contoso' have no direct administrative privileges tootenant 'Test,' unless an administrator of 'Test' specifically grants them these privileges.</span></span> <span data-ttu-id="2c6f8-114">그러나 통해 'Contoso'의 관리자가 만든 'Test' hello 사용자 계정을 제어 하는 경우 액세스 tootenant 's t'를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c6f8-114">However, administrators of 'Contoso' can control access tootenant 'Test' if they control hello user account that created 'Test.'</span></span>
* <span data-ttu-id="2c6f8-115">Hello 변경 않습니다 해당 hello hello 관리자 역할 하지 영향을 한 테 넌 트의 사용자에 대 한 관리자 역할을 추가/제거 하는 경우 사용자가 다른 테 넌 트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c6f8-115">If you add/remove an administrator role for a user in one tenant, hello change does not affect hello administrator roles that hello user has in another tenant.</span></span>

## <a name="synchronization-independence"></a><span data-ttu-id="2c6f8-116">동기화 독립성</span><span class="sxs-lookup"><span data-stu-id="2c6f8-116">Synchronization independence</span></span>
<span data-ttu-id="2c6f8-117">구성한 각 Azure AD 테 넌 트 하지 독립적으로 tooget 데이터의 단일 인스턴스에서 동기화:</span><span class="sxs-lookup"><span data-stu-id="2c6f8-117">You can configure each Azure AD tenant independently tooget data synchronized from a single instance of either:</span></span>

* <span data-ttu-id="2c6f8-118">단일 AD 포리스트의 사용 하 여 toosynchronize 데이터 hello Azure AD Connect 도구.</span><span class="sxs-lookup"><span data-stu-id="2c6f8-118">hello Azure AD Connect tool, toosynchronize data with a single AD forest.</span></span>
* <span data-ttu-id="2c6f8-119">Azure 활성 테 넌 트에 대 한 Forefront Identity Manager, 하나를 사용 하 여 toosynchronize 데이터 커넥터 hello 또는 자세히 온-프레미스 포리스트 및/또는 비 Azure AD의 데이터 원본.</span><span class="sxs-lookup"><span data-stu-id="2c6f8-119">hello Azure Active tenant Connector for Forefront Identity Manager, toosynchronize data with one or more on-premises forests, and/or non-Azure AD data sources.</span></span>

## <a name="add-an-azure-ad-tenant"></a><span data-ttu-id="2c6f8-120">Azure AD 테넌트 추가</span><span class="sxs-lookup"><span data-stu-id="2c6f8-120">Add an Azure AD tenant</span></span>
<span data-ttu-id="2c6f8-121">너무 tooadd hello Azure 포털에서에서 Azure AD 테 넌 트에 로그인[Azure 포털 hello](https://portal.azure.com) Azure AD 전역 관리자 계정으로 및에서 hello 왼쪽, 선택 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c6f8-121">tooadd an Azure AD tenant in hello Azure portal, sign in too[hello Azure portal](https://portal.azure.com) with an account that is an Azure AD global administrator, and, on hello left, select **New**.</span></span>

> [!NOTE]
> <span data-ttu-id="2c6f8-122">다른 Azure 리소스와 달리 테넌트는 Azure 구독의 자식 리소스가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="2c6f8-122">Unlike other Azure resources, your tenants are not child resources of an Azure subscription.</span></span> <span data-ttu-id="2c6f8-123">Azure 구독 취소 또는 만료 된 경우 Azure PowerShell, Azure Graph API hello 또는 hello Office 365 관리 센터를 사용 하 여 테 넌 트 데이터를 계속 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c6f8-123">If your Azure subscription is canceled or expired, you can still access your tenant data using Azure PowerShell, hello Azure Graph API, or hello Office 365 Admin Center.</span></span> <span data-ttu-id="2c6f8-124">Hello 테 넌 트와 다른 구독을 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c6f8-124">You can also associate another subscription with hello tenant.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="2c6f8-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2c6f8-125">Next steps</span></span>
<span data-ttu-id="2c6f8-126">Azure AD 라이선스 문제 및 모범 사례에 대한 광범위한 개요는 [Azure Active 테넌트 라이선스란?](active-directory-licensing-whatis-azure-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c6f8-126">For a broad overview of Azure AD licensing issues and best practices, see [What is Azure Active tenant licensing?](active-directory-licensing-whatis-azure-portal.md)</span></span>
