---
title: "Azure Active Directory B2C: Azure Active Directory B2C 테넌트 만들기 | Microsoft Docs"
description: "Toocreate Azure Active Directory B2C 테 넌 트의 항목을"
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
ms.openlocfilehash: e8b257d66c1f66ffb84f5d3d21b30b42eddcbac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-hello-azure-portal"></a><span data-ttu-id="df0c1-103">Hello Azure 포털에서에서 Azure Active Directory B2C 테 넌 트 만들기</span><span class="sxs-lookup"><span data-stu-id="df0c1-103">Create an Azure Active Directory B2C tenant in hello Azure portal</span></span>

<span data-ttu-id="df0c1-104">Sipi가 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="df0c1-104">Edited by Sipi.</span></span>

<span data-ttu-id="df0c1-105">이 Quickstart를 통해 몇 분 이내에 Microsoft Azure AD(Azure Active Directory) B2C 테넌트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df0c1-105">This Quickstart helps you create a Microsoft Azure Active Directory (Azure AD) B2C tenant in just a few minutes.</span></span> <span data-ttu-id="df0c1-106">완료 되 면 B2C 응용 프로그램을 등록 하기 위한 B2C 테 넌 트 toouse를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df0c1-106">When you're finished, you have a B2C tenant toouse for registering B2C applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df0c1-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="df0c1-107">Prerequisites</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-tooazure"></a><span data-ttu-id="df0c1-108">TooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="df0c1-108">Log in tooAzure</span></span>

<span data-ttu-id="df0c1-109">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="df0c1-109">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="df0c1-110">Azure AD B2C 테넌트 만들기</span><span class="sxs-lookup"><span data-stu-id="df0c1-110">Create an Azure AD B2C tenant</span></span>

<span data-ttu-id="df0c1-111">B2C 기능은 기존 테넌트에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="df0c1-111">B2C features can't be enabled in your existing tenants.</span></span> <span data-ttu-id="df0c1-112">Azure AD B2C 테 넌 트 toocreate가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="df0c1-112">You need toocreate an Azure AD B2C tenant.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

<span data-ttu-id="df0c1-113">축하합니다. Azure Active Directory B2C 테넌트를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="df0c1-113">Congratulations, you have created an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="df0c1-114">Hello 테 넌 트의 전역 관리자가.</span><span class="sxs-lookup"><span data-stu-id="df0c1-114">You are a Global Administrator of hello tenant.</span></span> <span data-ttu-id="df0c1-115">필요에 따라 다른 전역 관리자를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df0c1-115">You can add other Global Administrators as required.</span></span> <span data-ttu-id="df0c1-116">tooswitch tooyour 새 테 넌 트를 hello 클릭 *새로운 테 넌 트 연결 관리*합니다.</span><span class="sxs-lookup"><span data-stu-id="df0c1-116">tooswitch tooyour new tenant, click hello *manage your new tenant link*.</span></span>

![새 테넌트 연결 관리](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> <span data-ttu-id="df0c1-118">Toouse 프로덕션 응용 프로그램에 대 한 B2C 테 넌 트가 계획에 hello 문서를 읽어 보세요. [미리 보기 B2C 테 넌 트 및 프로덕션 규모](active-directory-b2c-reference-tenant-type.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="df0c1-118">If you are planning toouse a B2C tenant for a production app, read hello article on [production-scale vs. preview B2C tenants](active-directory-b2c-reference-tenant-type.md).</span></span> <span data-ttu-id="df0c1-119">알려진 문제 기존 B2C를 삭제 하는 경우 테 넌 트 및 다시 hello로 만드는 동일한 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="df0c1-119">There are known issues when you delete an existing B2C tenant and re-create it with hello same domain name.</span></span> <span data-ttu-id="df0c1-120">다른 도메인 이름의 B2C 테 넌 트 toocreate가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="df0c1-120">You need toocreate a B2C tenant with a different domain name.</span></span>
>
>

## <a name="link-your-tenant-tooyour-subscription"></a><span data-ttu-id="df0c1-121">테 넌 트 tooyour 구독 연결</span><span class="sxs-lookup"><span data-stu-id="df0c1-121">Link your tenant tooyour subscription</span></span>

<span data-ttu-id="df0c1-122">Toolink 해야 Azure AD B2C 테 넌 트 tooyour Azure 구독 tooenable 모든 B2C 기능 및 사용 요금에 대 한 비용을 지불 합니다.</span><span class="sxs-lookup"><span data-stu-id="df0c1-122">You need toolink your Azure AD B2C tenant tooyour Azure subscription tooenable all B2C functionality and pay for usage charges.</span></span> <span data-ttu-id="df0c1-123">toolearn 더 읽기 [이 여기서](active-directory-b2c-how-to-enable-billing.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="df0c1-123">toolearn more, read [this article](active-directory-b2c-how-to-enable-billing.md).</span></span> <span data-ttu-id="df0c1-124">Azure AD B2C 테 넌 트 tooyour Azure 구독을 연결 하지 않는 경우 일부 기능이 액세스가 차단 되 고 ("연결 된 toothis B2C 테 넌 트 또는 구독 hello 구독이 필요 주의.") hello B2C 설정에서 경고 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df0c1-124">If you don't link your Azure AD B2C tenant tooyour Azure subscription, some functionality is blocked and, you see a warning message ("No Subscription linked toothis B2C tenant or hello Subscription needs your attention.") in hello B2C settings.</span></span> <span data-ttu-id="df0c1-125">프로덕션에 앱을 전달하기 전에 이 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df0c1-125">It is important that you take this step before you ship your apps into production.</span></span>

## <a name="easy-access-toosettings"></a><span data-ttu-id="df0c1-126">쉽게 액세스할 수 있도록 toosettings</span><span class="sxs-lookup"><span data-stu-id="df0c1-126">Easy access toosettings</span></span>

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

<span data-ttu-id="df0c1-127">입력 하 여 hello 블레이드에 액세스할 수도 있습니다 `Azure AD B2C` 에 **리소스 검색** hello 위쪽 hello 포털의.</span><span class="sxs-lookup"><span data-stu-id="df0c1-127">You can also access hello blade by entering `Azure AD B2C` in **Search resources** at hello top of hello portal.</span></span> <span data-ttu-id="df0c1-128">Hello 결과 목록에서 선택 **Azure AD B2C** tooaccess hello B2C 설정 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="df0c1-128">In hello results list, select **Azure AD B2C** tooaccess hello B2C settings blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df0c1-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="df0c1-129">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="df0c1-130">B2C 테넌트에 B2C 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="df0c1-130">Register your B2C application in a B2C tenant</span></span>](active-directory-b2c-app-registration.md)
