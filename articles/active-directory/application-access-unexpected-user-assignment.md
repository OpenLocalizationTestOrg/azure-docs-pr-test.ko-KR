---
title: "응용 프로그램에 사용자를 할당하는 방법 | Microsoft Docs"
description: "테넌트의 응용 프로그램에 사용자가 할당되는 방법 이해"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 916238ba402a2555bac620d7f08e02799d981ae0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-assign-users-to-applications"></a><span data-ttu-id="22693-103">응용 프로그램에 사용자를 할당하는 방법</span><span class="sxs-lookup"><span data-stu-id="22693-103">How to assign users to applications</span></span>

<span data-ttu-id="22693-104">이 문서에서는 테넌트의 응용 프로그램에 사용자가 할당되는 방법을 이해하는 데 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="22693-104">This article help you to understand how users get assigned to an application in your tenant.</span></span>

## <a name="how-do-users-get-assigned-to-an-application-in-azure-ad"></a><span data-ttu-id="22693-105">Azure AD의 응용 프로그램에 사용자가 할당되는 방법</span><span class="sxs-lookup"><span data-stu-id="22693-105">How do users get assigned to an application in Azure AD?</span></span>

<span data-ttu-id="22693-106">사용자는 응용 프로그램에 액세스하려면 어떤 방식으로든 먼저 응용 프로그램에 할당되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22693-106">For a user to access an application, they must first be assigned to it in some way.</span></span> <span data-ttu-id="22693-107">할당은 관리자, 비즈니스 대리자, 경우에 따라 사용자 자신이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22693-107">Assignment can be performed by an administrator, a business delegate, or sometimes, the user themselves.</span></span> <span data-ttu-id="22693-108">아래에서는 사용자가 응용 프로그램에 할당될 수 있는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="22693-108">Below describes the ways users can get assigned to applications:</span></span>

1.  <span data-ttu-id="22693-109">관리자가 응용 프로그램에 직접 [사용자를 할당](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span><span class="sxs-lookup"><span data-stu-id="22693-109">An administrator [assigns a user](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) to the application directly</span></span>

2.  <span data-ttu-id="22693-110">관리자가 다음을 포함하여 해당 사용자가 응용 프로그램의 구성원인 [그룹 할당](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span><span class="sxs-lookup"><span data-stu-id="22693-110">An administrator [assigns a group](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) that the user is a member of to the application, including:</span></span>

  * <span data-ttu-id="22693-111">온-프레미스에서 동기화된 그룹</span><span class="sxs-lookup"><span data-stu-id="22693-111">A group that was synchronized from on-premises</span></span>

  * <span data-ttu-id="22693-112">클라우드에서 만든 정적 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="22693-112">A static security group created in the cloud</span></span>

  * <span data-ttu-id="22693-113">클라우드에서 만든 [동적 보안 그룹](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal)</span><span class="sxs-lookup"><span data-stu-id="22693-113">A [dynamic security group](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) created in the cloud</span></span>

  * <span data-ttu-id="22693-114">클라우드에서 만든 Office 365 그룹</span><span class="sxs-lookup"><span data-stu-id="22693-114">An Office 365 group created in the cloud</span></span>

  * <span data-ttu-id="22693-115">[모든 사용자](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) 그룹</span><span class="sxs-lookup"><span data-stu-id="22693-115">The [All Users](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) group</span></span>

3.  <span data-ttu-id="22693-116">관리자가 [셀프 서비스 응용 프로그램 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access)를 통해 사용자가 **비즈니스 승인 없이** [응용 프로그램 액세스 패널](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **앱 추가**를 사용하여 응용 프로그램을 추가하도록 허용</span><span class="sxs-lookup"><span data-stu-id="22693-116">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to allow a user to add an application using the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature **without business approval**</span></span>

4.  <span data-ttu-id="22693-117">관리자가 [셀프 서비스 응용 프로그램 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access)를 통해 사용자가 **선택된 비즈니스 승인자 집합의 사전 승인이 있는 경우에만** [응용 프로그램 액세스 패널](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **앱 추가**를 사용하여 응용 프로그램을 추가하도록 허용</span><span class="sxs-lookup"><span data-stu-id="22693-117">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to allow a user to add an application using the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature, but only w**ith prior approval from a selected set of business approvers**</span></span>

5.  <span data-ttu-id="22693-118">관리자가 [셀프 서비스 그룹 관리](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management)를 통해 사용자가 **비즈니스 승인 없이** 응용 프로그램이 할당된 그룹에 가입하도록 허용</span><span class="sxs-lookup"><span data-stu-id="22693-118">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) to allow a user to join a group that an application is assigned to **without business approval**</span></span>

6.  <span data-ttu-id="22693-119">관리자가 [셀프 서비스 그룹 관리](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management)를 통해 사용자가 **선택된 비즈니스 승인자 집합의 사전 승인이 있는 경우에만** 응용 프로그램이 할당된 그룹에 가입하도록 허용</span><span class="sxs-lookup"><span data-stu-id="22693-119">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) to allow a user to join a group that an application is assigned to, but only **with prior approval from a selected set of business approvers**</span></span>

7.  <span data-ttu-id="22693-120">관리자가 [Microsoft Office 365](http://products.office.com/)와 같은 자사 응용 프로그램에 대해 직접, 사용자에게 라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="22693-120">An administrator assigns a license to a user directly for a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

8.  <span data-ttu-id="22693-121">관리자가 해당 [Microsoft Office 365](http://products.office.com/)와 같은 자사 응용 프로그램의 구성원인 그룹에 라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="22693-121">An administrator assigns a license to a group that the user is a member of to a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

9.  <span data-ttu-id="22693-122">[관리자가 모든 사용자가 사용할 수 있게 응용 프로그램에 동의](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent)한 후 사용자가 응용 프로그램에 로그인</span><span class="sxs-lookup"><span data-stu-id="22693-122">An [administrator consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to be used by all users and then a user signs in to the application</span></span>

10. <span data-ttu-id="22693-123">사용자가 응용 프로그램에 로그인하여 [응용 프로그램에 직접 동의](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent)</span><span class="sxs-lookup"><span data-stu-id="22693-123">A user [consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) themselves by signing in to the application</span></span>

## <a name="next-steps"></a><span data-ttu-id="22693-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="22693-124">Next steps</span></span>
[<span data-ttu-id="22693-125">Azure Active Directory로 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="22693-125">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
