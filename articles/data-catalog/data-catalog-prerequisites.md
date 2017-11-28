---
title: "aaaAzure 데이터 카탈로그의 필수 구성 요소 | Microsoft Docs"
description: "Azure Data Catalog 시작 tooget 필요한 hello 필수 구성 요소에 알아봅니다."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: ef497a54-dc4d-4820-b5bf-c361b64b964d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0c8e768e5846c61b542b746d7ad80121725a9ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-prerequisites"></a><span data-ttu-id="1a2d0-103">Azure 데이터 카탈로그의 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="1a2d0-103">Azure Data Catalog prerequisites</span></span>

<span data-ttu-id="1a2d0-104">Azure Data Catalog를 설정 하려면 먼저 몇 가지 care of tootake를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a2d0-104">You need tootake care of a few things before you can set up Azure Data Catalog.</span></span> <span data-ttu-id="1a2d0-105">걱정하지 마세요. 이 프로세스는 오래 걸리지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1a2d0-105">Don’t worry, this process does not take long.</span></span>

## <a name="azure-subscription"></a><span data-ttu-id="1a2d0-106">Azure 구독</span><span class="sxs-lookup"><span data-stu-id="1a2d0-106">Azure subscription</span></span>
<span data-ttu-id="1a2d0-107">tooset 데이터 카탈로그를 hello 소유자 또는 Azure 구독의 공동 소유자를 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a2d0-107">tooset up Data Catalog, you must be hello owner or co-owner of an Azure subscription.</span></span>

<span data-ttu-id="1a2d0-108">Azure 구독에는 데이터 카탈로그 같은 toocloud 서비스 리소스 액세스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a2d0-108">Azure subscriptions help you organize access toocloud-service resources such as Data Catalog.</span></span> <span data-ttu-id="1a2d0-109">구독은 리소스 사용을 보고하고, 요금을 청구하고, 지불하는 방식을 제어할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a2d0-109">Subscriptions also help you control how resource usage is reported, billed, and paid for.</span></span> <span data-ttu-id="1a2d0-110">각 구독은 별도 청구 및 지불 설정을 가질 수 있으므로 부서, 프로젝트, 지사 등에 따라 다른 구독 및 계획이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a2d0-110">Each subscription can have a separate billing and payment setup, so you can have subscriptions and plans that vary by department, project, regional office, and so on.</span></span> <span data-ttu-id="1a2d0-111">모든 클라우드 서비스 tooa 구독 속하고 데이터 카탈로그를 설정 하기 전에 toohave 구독 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a2d0-111">Every cloud service belongs tooa subscription, and you need toohave a subscription before you set up Data Catalog.</span></span> <span data-ttu-id="1a2d0-112">toolearn 더 참조 [계정, 구독 및 관리 역할 관리](../active-directory/active-directory-assign-admin-roles.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a2d0-112">toolearn more, see [Manage accounts, subscriptions, and administrative roles](../active-directory/active-directory-assign-admin-roles.md).</span></span>

## <a name="azure-active-directory"></a><span data-ttu-id="1a2d0-113">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1a2d0-113">Azure Active Directory</span></span>
<span data-ttu-id="1a2d0-114">tooset 데이터 카탈로그를 있습니다 서명 해야 Azure Active Directory (Azure AD) 사용자 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a2d0-114">tooset up Data Catalog, you must be signed in with an Azure Active Directory (Azure AD) user account.</span></span>

<span data-ttu-id="1a2d0-115">Azure AD 비즈니스 toomanage id 및 액세스 방법으로 hello 클라우드 및 온-프레미스에서 모두에 대 한는 쉬운 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1a2d0-115">Azure AD provides an easy way for your business toomanage identity and access, both in hello cloud and on-premises.</span></span> <span data-ttu-id="1a2d0-116">사용자에 단일 로그인 tooany 클라우드에 대 한 단일 회사 또는 학교 계정의 사용할 수 있으며 온-프레미스 웹 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="1a2d0-116">Users can use a single work or school account for single sign-in tooany cloud and on-premises web application.</span></span> <span data-ttu-id="1a2d0-117">데이터 카탈로그는 Azure AD tooauthenticate 로그인에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a2d0-117">Data Catalog uses Azure AD tooauthenticate sign-in.</span></span> <span data-ttu-id="1a2d0-118">toolearn 더 참조 [Azure Active Directory 란?](../active-directory/active-directory-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a2d0-118">toolearn more, see [What is Azure Active Directory?](../active-directory/active-directory-whatis.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1a2d0-119">Hello를 사용 하 여 [Azure 포털](http://portal.azure.com/)을 서명할 수 개인 Microsoft 계정 또는 Azure Active Directory를 사용 하 여 회사 또는 학교 계정.</span><span class="sxs-lookup"><span data-stu-id="1a2d0-119">By using hello [Azure portal](http://portal.azure.com/), you can sign in with either a personal Microsoft account or an Azure Active Directory work or school account.</span></span> <span data-ttu-id="1a2d0-120">Azure 포털 또는 hello에 중 하나를 사용 하 여 데이터 카탈로그를 tooset hello [Data Catalog 포털](http://www.azuredatacatalog.com), 개인 계정이 아닌 계정을 Azure Active Directory를 사용 하 여 로그인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a2d0-120">tooset up Data Catalog by using either hello Azure portal or hello [Data Catalog portal](http://www.azuredatacatalog.com), you must sign in with an Azure Active Directory account, not a personal account.</span></span>
>
>

## <a name="active-directory-policy-configuration"></a><span data-ttu-id="1a2d0-121">Active Directory 정책 구성</span><span class="sxs-lookup"><span data-stu-id="1a2d0-121">Active Directory policy configuration</span></span>
<span data-ttu-id="1a2d0-122">Toosign toohello 데이터 원본 등록 도구에서 시도할 때 하지만 toohello Data Catalog 포털에 로그인 할 수 있는 상황이 발생할 수 있습니다, 로그인 하면 오류 메시지가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a2d0-122">You might encounter a situation where you can sign in toohello Data Catalog portal, but when you attempt toosign in toohello data source registration tool, you encounter an error message that prevents you from signing in.</span></span> <span data-ttu-id="1a2d0-123">Hello 회사 네트워크에서 또는 외부 hello 회사 네트워크에서 연결 때만 발생할 수 있습니다 때에이 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a2d0-123">This problem behavior might occur only when you're on hello company network, or it might occur only when you're connecting from outside hello company network.</span></span>

<span data-ttu-id="1a2d0-124">hello 데이터 원본 등록 도구는 폼 인증 toovalidate Active Directory에 대해 사용자 자격 증명을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1a2d0-124">hello data source registration tool uses Forms Authentication toovalidate your user credentials against Active Directory.</span></span> <span data-ttu-id="1a2d0-125">toohelp 성공적으로 로그인을 Active Directory 관리자는 hello 전역 인증 정책에서에서 폼 인증을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a2d0-125">toohelp you sign in successfully, an Active Directory administrator must enable Forms Authentication in hello Global Authentication Policy.</span></span>

<span data-ttu-id="1a2d0-126">Hello 전역 인증 정책, 인증 방법 스크린 샷 다음 hello와 같이 설정을 변경 하려면 별도로 인트라넷 및 익스트라넷 연결을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a2d0-126">In hello Global Authentication Policy, authentication methods can be enabled separately for intranet and extranet connections, as shown in hello following screenshot.</span></span> <span data-ttu-id="1a2d0-127">연결 중인 hello 네트워크에 대 한 폼 인증을 사용 하지 않는 경우 로그인 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a2d0-127">Sign-in errors might occur if Forms Authentication is not enabled for hello network from which you're connecting.</span></span>

 ![Active Directory 전역 인증 정책](./media/data-catalog-prerequisites/global-auth-policy.png)

## <a name="next-steps"></a><span data-ttu-id="1a2d0-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1a2d0-129">Next steps</span></span>
<span data-ttu-id="1a2d0-130">자세한 내용은 [인증 정책 구성](https://technet.microsoft.com/library/dn486781.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1a2d0-130">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>
