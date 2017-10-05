---
title: "Azure 데이터 카탈로그의 필수 구성 요소 | Microsoft Docs"
description: "Azure Data Catalog 시작에 필요한 필수 구성 요소에 대해 알아봅니다."
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
ms.openlocfilehash: 3fdef7bb58a5cd5dfbe4d37d9baf9c8e392ebe42
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-data-catalog-prerequisites"></a><span data-ttu-id="1a095-103">Azure 데이터 카탈로그의 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="1a095-103">Azure Data Catalog prerequisites</span></span>

<span data-ttu-id="1a095-104">Azure Data Catalog를 설정하기 전에 몇 가지 사항을 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a095-104">You need to take care of a few things before you can set up Azure Data Catalog.</span></span> <span data-ttu-id="1a095-105">걱정하지 마세요. 이 프로세스는 오래 걸리지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1a095-105">Don’t worry, this process does not take long.</span></span>

## <a name="azure-subscription"></a><span data-ttu-id="1a095-106">Azure 구독</span><span class="sxs-lookup"><span data-stu-id="1a095-106">Azure subscription</span></span>
<span data-ttu-id="1a095-107">데이터 카탈로그를 설정하려면 Azure 구독의 소유자 또는 공동 소유자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a095-107">To set up Data Catalog, you must be the owner or co-owner of an Azure subscription.</span></span>

<span data-ttu-id="1a095-108">Azure 구독에서는 데이터 카탈로그와 같은 클라우드 서비스 리소스에 대한 액세스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a095-108">Azure subscriptions help you organize access to cloud-service resources such as Data Catalog.</span></span> <span data-ttu-id="1a095-109">구독은 리소스 사용을 보고하고, 요금을 청구하고, 지불하는 방식을 제어할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a095-109">Subscriptions also help you control how resource usage is reported, billed, and paid for.</span></span> <span data-ttu-id="1a095-110">각 구독은 별도 청구 및 지불 설정을 가질 수 있으므로 부서, 프로젝트, 지사 등에 따라 다른 구독 및 계획이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a095-110">Each subscription can have a separate billing and payment setup, so you can have subscriptions and plans that vary by department, project, regional office, and so on.</span></span> <span data-ttu-id="1a095-111">모든 클라우드 서비스는 구독에 속하고 데이터 카탈로그를 설정하기 전에 구독을 보유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a095-111">Every cloud service belongs to a subscription, and you need to have a subscription before you set up Data Catalog.</span></span> <span data-ttu-id="1a095-112">자세한 내용은 [계정, 구독 및 관리 역할 관리](../active-directory/active-directory-assign-admin-roles.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1a095-112">To learn more, see [Manage accounts, subscriptions, and administrative roles](../active-directory/active-directory-assign-admin-roles.md).</span></span>

## <a name="azure-active-directory"></a><span data-ttu-id="1a095-113">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1a095-113">Azure Active Directory</span></span>
<span data-ttu-id="1a095-114">데이터 카탈로그를 설정하려면 Azure AD(Azure Active Directory) 사용자 계정으로 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a095-114">To set up Data Catalog, you must be signed in with an Azure Active Directory (Azure AD) user account.</span></span>

<span data-ttu-id="1a095-115">Azure AD는 클라우드 및 온-프레미스 모두에서 비즈니스가 ID와 액세스를 쉽게 관리하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1a095-115">Azure AD provides an easy way for your business to manage identity and access, both in the cloud and on-premises.</span></span> <span data-ttu-id="1a095-116">사용자는 클라우드 및 온-프레미스 웹 응용 프로그램에 SSO(Single Sign-on)를 위해 단일 회사 또는 학교 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a095-116">Users can use a single work or school account for single sign-in to any cloud and on-premises web application.</span></span> <span data-ttu-id="1a095-117">데이터 카탈로그는 로그인 인증에 Azure AD를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1a095-117">Data Catalog uses Azure AD to authenticate sign-in.</span></span> <span data-ttu-id="1a095-118">자세히 알아보려면 [Azure Active Directory란?](../active-directory/active-directory-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1a095-118">To learn more, see [What is Azure Active Directory?](../active-directory/active-directory-whatis.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1a095-119">[Azure Portal](http://portal.azure.com/)을 사용하여 사용자는 개인 Microsoft 계정 또는 Azure Active Directory 작업 또는 학교 계정으로 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a095-119">By using the [Azure portal](http://portal.azure.com/), you can sign in with either a personal Microsoft account or an Azure Active Directory work or school account.</span></span> <span data-ttu-id="1a095-120">Azure Portal을 사용하거나 [데이터 카탈로그 포털](http://www.azuredatacatalog.com)을 사용하여 데이터 카탈로그를 설정하려면 개인 계정이 아닌, Azure Active Directory 계정을 사용하여 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a095-120">To set up Data Catalog by using either the Azure portal or the [Data Catalog portal](http://www.azuredatacatalog.com), you must sign in with an Azure Active Directory account, not a personal account.</span></span>
>
>

## <a name="active-directory-policy-configuration"></a><span data-ttu-id="1a095-121">Active Directory 정책 구성</span><span class="sxs-lookup"><span data-stu-id="1a095-121">Active Directory policy configuration</span></span>
<span data-ttu-id="1a095-122">데이터 카탈로그 포털에 로그인할 수 있는 상황이 발생할 수 있지만, 데이터 원본 등록 도구에 로그인을 시도할 때 로그인하지 않도록 하는 오류 메시지가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1a095-122">You might encounter a situation where you can sign in to the Data Catalog portal, but when you attempt to sign in to the data source registration tool, you encounter an error message that prevents you from signing in.</span></span> <span data-ttu-id="1a095-123">이 문제 동작은 사용자가 회사 네트워크에 있는 경우 또는 회사 네트워크 외부에서 연결하는 경우에만 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a095-123">This problem behavior might occur only when you're on the company network, or it might occur only when you're connecting from outside the company network.</span></span>

<span data-ttu-id="1a095-124">데이터 원본 등록 도구가 폼 인증을 사용하여 Active Directory에 대한 사용자 자격 증명의 유효성 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1a095-124">The data source registration tool uses Forms Authentication to validate your user credentials against Active Directory.</span></span> <span data-ttu-id="1a095-125">로그인이 성공하려면 Azure Active Directory 관리자가 전역 인증 정책에서 폼 인증을 사용할 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a095-125">To help you sign in successfully, an Active Directory administrator must enable Forms Authentication in the Global Authentication Policy.</span></span>

<span data-ttu-id="1a095-126">전역 인증 정책에서 다음 스크린샷에 나와 있는 것처럼 인트라넷 및 엑스트라넷 연결을 위해 인증 방법을 개별적으로 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a095-126">In the Global Authentication Policy, authentication methods can be enabled separately for intranet and extranet connections, as shown in the following screenshot.</span></span> <span data-ttu-id="1a095-127">연결되어 있는 네트워크에 대해 폼 인증을 사용할 수 없는 경우 로그인 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a095-127">Sign-in errors might occur if Forms Authentication is not enabled for the network from which you're connecting.</span></span>

 ![Active Directory 전역 인증 정책](./media/data-catalog-prerequisites/global-auth-policy.png)

## <a name="next-steps"></a><span data-ttu-id="1a095-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1a095-129">Next steps</span></span>
<span data-ttu-id="1a095-130">자세한 내용은 [인증 정책 구성](https://technet.microsoft.com/library/dn486781.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1a095-130">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>
