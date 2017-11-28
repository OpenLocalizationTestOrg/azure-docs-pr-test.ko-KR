---
title: "aaaHow tooAssign 사용자 tooapplications | Microsoft Docs"
description: "사용자가 테 넌 트에 tooan 응용 프로그램 가져오기 할당 하는 방법을 이해합니다"
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
ms.openlocfilehash: 4df60c7d723140d0d1bbd6ba8b34aa4e762d1138
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-tooapplications"></a><span data-ttu-id="43849-103">어떻게 tooassign 사용자 tooapplications</span><span class="sxs-lookup"><span data-stu-id="43849-103">How tooassign users tooapplications</span></span>

<span data-ttu-id="43849-104">이 문서가 도움이 toounderstand 방법을 사용자가 테 넌 트에 응용 프로그램 tooan 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="43849-104">This article help you toounderstand how users get assigned tooan application in your tenant.</span></span>

## <a name="how-do-users-get-assigned-tooan-application-in-azure-ad"></a><span data-ttu-id="43849-105">어떻게 사용자가 할당 않았는지 Azure AD에서 응용 프로그램 tooan?</span><span class="sxs-lookup"><span data-stu-id="43849-105">How do users get assigned tooan application in Azure AD?</span></span>

<span data-ttu-id="43849-106">사용자 tooaccess 응용 프로그램에 대 한 처음 할당 해야 어떤 방식으로든에서 tooit 합니다.</span><span class="sxs-lookup"><span data-stu-id="43849-106">For a user tooaccess an application, they must first be assigned tooit in some way.</span></span> <span data-ttu-id="43849-107">할당 수 수행한 관리자, 비즈니스 대리자 또는 경우에 따라서는 hello 사용자 자체.</span><span class="sxs-lookup"><span data-stu-id="43849-107">Assignment can be performed by an administrator, a business delegate, or sometimes, hello user themselves.</span></span> <span data-ttu-id="43849-108">아래 사용자도 tooapplications 할당 수 hello 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="43849-108">Below describes hello ways users can get assigned tooapplications:</span></span>

1.  <span data-ttu-id="43849-109">관리자가 [은 사용자를 할당](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) 직접 toohello 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="43849-109">An administrator [assigns a user](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) toohello application directly</span></span>

2.  <span data-ttu-id="43849-110">관리자 [그룹 할당](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) 해당 hello 사용자가 toohello 응용 프로그램의 구성원 포함:</span><span class="sxs-lookup"><span data-stu-id="43849-110">An administrator [assigns a group](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) that hello user is a member of toohello application, including:</span></span>

  * <span data-ttu-id="43849-111">온-프레미스에서 동기화된 그룹</span><span class="sxs-lookup"><span data-stu-id="43849-111">A group that was synchronized from on-premises</span></span>

  * <span data-ttu-id="43849-112">Hello 클라우드에서 만든 정적 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="43849-112">A static security group created in hello cloud</span></span>

  * <span data-ttu-id="43849-113">A [동적 보안 그룹](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) hello 클라우드에서 만든</span><span class="sxs-lookup"><span data-stu-id="43849-113">A [dynamic security group](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) created in hello cloud</span></span>

  * <span data-ttu-id="43849-114">Hello 클라우드에서 만든는 Office 365 그룹</span><span class="sxs-lookup"><span data-stu-id="43849-114">An Office 365 group created in hello cloud</span></span>

  * <span data-ttu-id="43849-115">hello [모든 사용자에 게](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) 그룹</span><span class="sxs-lookup"><span data-stu-id="43849-115">hello [All Users](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) group</span></span>

3.  <span data-ttu-id="43849-116">관리자를 사용 하면 [셀프 서비스 응용 프로그램 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) hello를 사용 하 여 응용 프로그램 사용자 tooadd tooallow [응용 프로그램 액세스 패널로](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **앱 추가** 기능**비즈니스 승인 없이**</span><span class="sxs-lookup"><span data-stu-id="43849-116">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow a user tooadd an application using hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature **without business approval**</span></span>

4.  <span data-ttu-id="43849-117">관리자를 사용 하면 [셀프 서비스 응용 프로그램 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) hello를 사용 하 여 응용 프로그램 사용자 tooadd tooallow [응용 프로그램 액세스 패널로](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **앱 추가** 기능을 사용 하지만 w **선택한 비즈니스 승인자 집합에서 i 번째 사전 승인**</span><span class="sxs-lookup"><span data-stu-id="43849-117">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow a user tooadd an application using hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature, but only w**ith prior approval from a selected set of business approvers**</span></span>

5.  <span data-ttu-id="43849-118">관리자를 사용 하면 [셀프 서비스 그룹 관리](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow 사용자 toojoin 응용 프로그램은 너무 할당 그룹**비즈니스 승인 없이**</span><span class="sxs-lookup"><span data-stu-id="43849-118">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow a user toojoin a group that an application is assigned too**without business approval**</span></span>

6.  <span data-ttu-id="43849-119">관리자를 사용 하면 [셀프 서비스 그룹 관리](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow 사용자 toojoin 하지만 응용 프로그램에 할당 된 그룹 **선택된 된 비즈니스 승인자 집합의 사전 승인으로**</span><span class="sxs-lookup"><span data-stu-id="43849-119">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow a user toojoin a group that an application is assigned to, but only **with prior approval from a selected set of business approvers**</span></span>

7.  <span data-ttu-id="43849-120">관리자 할당 첫 번째 파티 응용 프로그램에 대 한 직접 라이선스 tooa 사용자 같은 [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="43849-120">An administrator assigns a license tooa user directly for a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

8.  <span data-ttu-id="43849-121">Hello 사용자 라이선스 tooa 그룹 멤버인 tooa 첫 번째 파티와 응용 프로그램의 같은 프로그램 관리자 할당 [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="43849-121">An administrator assigns a license tooa group that hello user is a member of tooa first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

9.  <span data-ttu-id="43849-122">[관리자가 tooan 응용 프로그램을 승인](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toobe 모든 사용자가 사용 하 고 toohello 응용 프로그램에서 사용자가 로그인 한 다음</span><span class="sxs-lookup"><span data-stu-id="43849-122">An [administrator consents tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toobe used by all users and then a user signs in toohello application</span></span>

10. <span data-ttu-id="43849-123">사용자 [tooan 응용 프로그램 동의](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toohello 응용 프로그램에 로그인 하면 자체</span><span class="sxs-lookup"><span data-stu-id="43849-123">A user [consents tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) themselves by signing in toohello application</span></span>

## <a name="next-steps"></a><span data-ttu-id="43849-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="43849-124">Next steps</span></span>
[<span data-ttu-id="43849-125">Azure Active Directory로 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="43849-125">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
