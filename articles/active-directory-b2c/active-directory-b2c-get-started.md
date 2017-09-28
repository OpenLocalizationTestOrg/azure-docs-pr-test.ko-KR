---
title: "Azure Active Directory B2C: Azure Active Directory B2C 테넌트 만들기 | Microsoft Docs"
description: "Azure Active Directory B2C 테넌트를 만드는 방법에 대한 항목"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: patricka
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/07/2017
ms.author: swkrish
ms.openlocfilehash: 8a1d4935397f59e5813afc6f04559e471187a779
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-the-azure-portal"></a><span data-ttu-id="8c319-103">Azure Portal에서 Azure Active Directory B2C 테넌트 만들기</span><span class="sxs-lookup"><span data-stu-id="8c319-103">Create an Azure Active Directory B2C tenant in the Azure portal</span></span>

<span data-ttu-id="8c319-104">이 Quickstart를 통해 몇 분 이내에 Microsoft Azure AD(Azure Active Directory) B2C 테넌트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c319-104">This Quickstart helps you create a Microsoft Azure Active Directory (Azure AD) B2C tenant in just a few minutes.</span></span> <span data-ttu-id="8c319-105">완료되면 B2C 응용 프로그램 등록에 사용할 B2C 테넌트를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="8c319-105">When you're finished, you have a B2C tenant to use for registering B2C applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c319-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8c319-106">Prerequisites</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-to-azure"></a><span data-ttu-id="8c319-107">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="8c319-107">Log in to Azure</span></span>

<span data-ttu-id="8c319-108">[Azure Portal](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8c319-108">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="8c319-109">Azure AD B2C 테넌트 만들기</span><span class="sxs-lookup"><span data-stu-id="8c319-109">Create an Azure AD B2C tenant</span></span>

<span data-ttu-id="8c319-110">B2C 기능은 기존 테넌트에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8c319-110">B2C features can't be enabled in your existing tenants.</span></span> <span data-ttu-id="8c319-111">Azure AD B2C 테넌트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c319-111">You need to create an Azure AD B2C tenant.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

<span data-ttu-id="8c319-112">축하합니다. Azure Active Directory B2C 테넌트를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="8c319-112">Congratulations, you have created an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="8c319-113">테넌트의 전역 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="8c319-113">You are a Global Administrator of the tenant.</span></span> <span data-ttu-id="8c319-114">필요에 따라 다른 전역 관리자를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c319-114">You can add other Global Administrators as required.</span></span> <span data-ttu-id="8c319-115">새 테넌트로 전환하려면 *새 테넌트 연결 관리*를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8c319-115">To switch to your new tenant, click the *manage your new tenant link*.</span></span>

![새 테넌트 연결 관리](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> <span data-ttu-id="8c319-117">프로덕션 앱에 대해 B2C 테넌트를 사용하려는 경우 [프로덕션 규모와 B2C 테넌트 미리 보기 비교](active-directory-b2c-reference-tenant-type.md)의 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8c319-117">If you are planning to use a B2C tenant for a production app, read the article on [production-scale vs. preview B2C tenants](active-directory-b2c-reference-tenant-type.md).</span></span> <span data-ttu-id="8c319-118">기존 B2C 테넌트를 삭제하고 동일한 도메인 이름으로 다시 만들어야 하는 경우 알려진 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="8c319-118">There are known issues when you delete an existing B2C tenant and re-create it with the same domain name.</span></span> <span data-ttu-id="8c319-119">다른 도메인 이름으로 B2C 테넌트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c319-119">You need to create a B2C tenant with a different domain name.</span></span>
>
>

## <a name="link-your-tenant-to-your-subscription"></a><span data-ttu-id="8c319-120">구독에 테넌트 연결</span><span class="sxs-lookup"><span data-stu-id="8c319-120">Link your tenant to your subscription</span></span>

<span data-ttu-id="8c319-121">모든 B2C 기능을 활성화하고 사용 요금을 지불하기 위해 Azure 구독에 Azure AD B2C 테넌트를 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c319-121">You need to link your Azure AD B2C tenant to your Azure subscription to enable all B2C functionality and pay for usage charges.</span></span> <span data-ttu-id="8c319-122">자세한 내용은 [이 문서](active-directory-b2c-how-to-enable-billing.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8c319-122">To learn more, read [this article](active-directory-b2c-how-to-enable-billing.md).</span></span> <span data-ttu-id="8c319-123">Azure AD B2C 테넌트를 Azure 구독에 연결하지 않으면 일부 기능이 차단되고 B2C 설정에 경고 메시지("이 B2C 테넌트에 연결된 구독이 없거나 구독에 유의해야 합니다.")가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c319-123">If you don't link your Azure AD B2C tenant to your Azure subscription, some functionality is blocked and, you see a warning message ("No Subscription linked to this B2C tenant or the Subscription needs your attention.") in the B2C settings.</span></span> <span data-ttu-id="8c319-124">프로덕션에 앱을 전달하기 전에 이 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c319-124">It is important that you take this step before you ship your apps into production.</span></span>

## <a name="easy-access-to-settings"></a><span data-ttu-id="8c319-125">설정에 대한 쉬운 액세스</span><span class="sxs-lookup"><span data-stu-id="8c319-125">Easy access to settings</span></span>

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

<span data-ttu-id="8c319-126">포털 위쪽에 있는 **리소스 검색**에 `Azure AD B2C`를 입력하여 블레이드에 액세스할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c319-126">You can also access the blade by entering `Azure AD B2C` in **Search resources** at the top of the portal.</span></span> <span data-ttu-id="8c319-127">결과 목록에서 **Azure AD B2C**를 선택하여 B2C 설정 블레이드에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c319-127">In the results list, select **Azure AD B2C** to access the B2C settings blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c319-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8c319-128">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8c319-129">B2C 테넌트에 B2C 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="8c319-129">Register your B2C application in a B2C tenant</span></span>](active-directory-b2c-app-registration.md)