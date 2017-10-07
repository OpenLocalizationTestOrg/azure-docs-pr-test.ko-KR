---
title: "특정 사용자 수 tooaccess 응용 프로그램을 수 있습니다 때 aaaFind | Microsoft Docs"
description: "어떻게 toofind 때 매우 중요 한 사용자 수 수 tooaccess 응용 프로그램에 대해 구성한 Azure AD를 통해 사용자 프로비저닝을"
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
ms.openlocfilehash: bb9520499dcc8bbbe6fae05c5238c8852815ea0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-when-a-specific-user-will-be-able-tooaccess-an-application"></a><span data-ttu-id="84b5a-103">확인 하 여 특정 사용자가 응용 프로그램 수 tooaccess 됩니다</span><span class="sxs-lookup"><span data-stu-id="84b5a-103">Find out when a specific user will be able tooaccess an application</span></span>
<span data-ttu-id="84b5a-104">응용 프로그램에서 자동 사용자 프로비저닝을 사용하는 경우 Azure AD는 정기적으로 예약된 시간 간격(일반적으로 10분 간격)으로 [사용자 및 그룹 할당](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)과 같은 항목을 기반으로 앱에서 사용자 계정을 자동으로 프로비저닝하고 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="84b5a-104">When using automatic user provisioning with an application, Azure AD automatically provision and update user accounts in an app based on things like [user and group assignment](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) at a regularly scheduled time interval, typically every 10 minutes.</span></span>

## <a name="how-long-does-it-take"></a><span data-ttu-id="84b5a-105">소요 시간</span><span class="sxs-lookup"><span data-stu-id="84b5a-105">How long does it take?</span></span>

<span data-ttu-id="84b5a-106">사용자를 프로 비전 하는 지정 된 사용자 toobe 걸리는 hello 시간은 주로 초기 "완전히" 동기화 작업이 이미 수행 여부에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="84b5a-106">hello time it takes for a given user toobe provisioned depends mainly on whether or not an initial “full” sync has already occurred.</span></span>

<span data-ttu-id="84b5a-107">Azure AD 간의 첫 번째 동기화 hello 및 앱 hello Azure AD 디렉터리와 hello 사용자 프로 비전에 대 한 범위에가 수의 hello 크기에 따라 20 분 tooseveral 시간에서 아무 곳 이나 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b5a-107">hello first sync between Azure AD and an app can take anywhere from 20 minutes tooseveral hours, depending on hello size of hello Azure AD directory and hello number of users in scope for provisioning.</span></span> 

<span data-ttu-id="84b5a-108">Hello 초기 동기화 후 후속 동기화 속도가 더 빠를 수 (예: 10 분) 내에서 서비스를 프로 비전 하는 hello 후속 동기화 성능을 향상 시킬 수 hello 초기 동기화 후 두 시스템의 hello 상태를 나타내는 워터 마크를 저장소로 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b5a-108">Subsequent syncs after hello initial sync be faster (e.g. within 10 minutes), as hello provisioning service stores watermarks that represent hello state of both systems after hello initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-toocheck-hello-status-of-a-user"></a><span data-ttu-id="84b5a-109">Toocheck은 사용자의 상태를 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="84b5a-109">How toocheck hello status of a user</span></span>

<span data-ttu-id="84b5a-110">선택한 사용자에 대 한 toosee hello 프로 비전 상태 hello Azure AD에서 감사 로그를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="84b5a-110">toosee hello provisioning status for a selected user, consult hello Audit logs in Azure AD.</span></span>

<span data-ttu-id="84b5a-111">감사 로그를 프로 비전 하는 hello hello hello에서 Azure 포털에에서 액세스할 수 있습니다 **Azure Active Directory &gt; 엔터프라이즈 앱 &gt; \[응용 프로그램 이름\] &gt; 감사 로그**탭 합니다. 필터 hello hello 로그온 **계정 프로 비전** 범주 tooonly hello 이러한 앱에 대 한 이벤트를 프로 비전을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="84b5a-111">hello provisioning audit logs can be accessed in hello Azure portal, in hello **Azure Active Directory &gt; Enterprise Apps &gt; \[Application Name\] &gt; Audit Logs** tab. Filter hello logs on hello **Account Provisioning** category tooonly see hello provisioning events for that app.</span></span> <span data-ttu-id="84b5a-112">ID에 따라 hello "일치 하는" hello 특성 매핑을에 구성 된 사용자에 대 한 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b5a-112">You can search for users based on hello “matching ID” that was configured for them in hello attribute mappings.</span></span> 

<span data-ttu-id="84b5a-113">예를 들어 hello "사용자 계정 이름" 또는 "전자 메일 주소" hello Azure AD 쪽에서 특성을 일치 하는 hello로 구성 했으며 hello 사용자 프로 비전이 아닌 값이 "audrey@contoso.com", 검색 hello 감사 로그에 대 한"audrey@contoso.com" 다음을 검토 하 고 항목을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b5a-113">For example, if you configured hello “user principal name” or “email address” as hello matching attribute on hello Azure AD side, and hello user not being provisioning has a value of “audrey@contoso.com”, then search hello audit logs for “audrey@contoso.com” and review then entries returned.</span></span>

<span data-ttu-id="84b5a-114">서비스를 프로 비전 하는 hello 수행한 작업을 hello 모든 레코드를 기록 하는 감사를 프로 비전 하는 hello 포함 하 여:</span><span class="sxs-lookup"><span data-stu-id="84b5a-114">hello provisioning audit logs record all hello operations performed by hello provisioning service, including:</span></span>

* <span data-ttu-id="84b5a-115">프로비저닝 범위에 있는 할당된 사용자에 대해 Azure AD 쿼리</span><span class="sxs-lookup"><span data-stu-id="84b5a-115">Querying Azure AD for assigned users that are in scope for provisioning</span></span>
* <span data-ttu-id="84b5a-116">해당 사용자의 존재 여부 hello에 대 한 쿼리 hello 대상 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="84b5a-116">Querying hello target app for hello existence of those users</span></span>
* <span data-ttu-id="84b5a-117">Hello 시스템 간에 hello 사용자 개체를 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="84b5a-117">Comparing hello user objects between hello system</span></span>
* <span data-ttu-id="84b5a-118">추가, 업데이트 또는 hello 비교 기반 hello 대상 시스템에 사용자 계정을 hello를 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="84b5a-118">Adding, updating, or disabling hello user account in hello target system based on hello comparison</span></span>

## <a name="next-steps"></a><span data-ttu-id="84b5a-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="84b5a-119">Next steps</span></span>
<span data-ttu-id="84b5a-120">[사용자 프로 비전 및 프로 비전 해제 tooSaaS Azure Active Directory와 응용 프로그램을 자동화](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)'</span><span class="sxs-lookup"><span data-stu-id="84b5a-120">[Automate User Provisioning and Deprovisioning tooSaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''</span></span>
