---
title: "특정 사용자가 응용 프로그램에 액세스할 수 있는 시점 파악 | Microsoft Docs"
description: "매우 중요한 사용자가 Azure AD를 사용하여 사용자를 프로비저닝하도록 구성한 응용 프로그램에 액세스할 수 있는 시기를 찾는 방법"
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
ms.openlocfilehash: fcefb31904cfb77022db0358e9feee6a0479db81
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="find-out-when-a-specific-user-will-be-able-to-access-an-application"></a><span data-ttu-id="4630c-103">특정 사용자가 응용 프로그램에 액세스할 수 있는 시점 파악</span><span class="sxs-lookup"><span data-stu-id="4630c-103">Find out when a specific user will be able to access an application</span></span>
<span data-ttu-id="4630c-104">응용 프로그램에서 자동 사용자 프로비저닝을 사용하는 경우 Azure AD는 정기적으로 예약된 시간 간격(일반적으로 10분 간격)으로 [사용자 및 그룹 할당](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)과 같은 항목을 기반으로 앱에서 사용자 계정을 자동으로 프로비저닝하고 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="4630c-104">When using automatic user provisioning with an application, Azure AD automatically provision and update user accounts in an app based on things like [user and group assignment](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) at a regularly scheduled time interval, typically every 10 minutes.</span></span>

## <a name="how-long-does-it-take"></a><span data-ttu-id="4630c-105">소요 시간</span><span class="sxs-lookup"><span data-stu-id="4630c-105">How long does it take?</span></span>

<span data-ttu-id="4630c-106">지정된 사용자를 프로비저닝하는 데 걸리는 시간은 주로 초기 "전체" 동기화가 이미 발생했는지 여부에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="4630c-106">The time it takes for a given user to be provisioned depends mainly on whether or not an initial “full” sync has already occurred.</span></span>

<span data-ttu-id="4630c-107">Azure AD와 앱 간의 첫 번째 동기화는 Azure AD 디렉터리의 크기와 프로비저닝 범위에 있는 사용자 수에 따라 20분에서 몇 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4630c-107">The first sync between Azure AD and an app can take anywhere from 20 minutes to several hours, depending on the size of the Azure AD directory and the number of users in scope for provisioning.</span></span> 

<span data-ttu-id="4630c-108">프로비저닝 서비스는 초기 동기화 후에 두 시스템의 상태를 나타내는 워터마크를 저장하므로, 초기 동기화 이후의 후속 동기화가 빨라져(예: 10분 이내) 후속 동기화의 성능이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="4630c-108">Subsequent syncs after the initial sync be faster (e.g. within 10 minutes), as the provisioning service stores watermarks that represent the state of both systems after the initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-to-check-the-status-of-a-user"></a><span data-ttu-id="4630c-109">사용자의 상태를 확인하는 방법</span><span class="sxs-lookup"><span data-stu-id="4630c-109">How to check the status of a user</span></span>

<span data-ttu-id="4630c-110">선택한 사용자에 대한 프로비저닝 상태를 보려면 Azure AD의 감사 로그를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4630c-110">To see the provisioning status for a selected user, consult the Audit logs in Azure AD.</span></span>

<span data-ttu-id="4630c-111">프로비저닝 감사 로그는 Azure Portal의 **Azure Active Directory &gt; 엔터프라이즈 앱 &gt; \[응용 프로그램 이름\] &gt; 감사 로그** 탭에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4630c-111">The provisioning audit logs can be accessed in the Azure portal, in the **Azure Active Directory &gt; Enterprise Apps &gt; \[Application Name\] &gt; Audit Logs** tab.</span></span> <span data-ttu-id="4630c-112">**계정 프로비저닝** 범주의 로그를 필터링하여 해당 앱의 프로비저닝 이벤트만 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4630c-112">Filter the logs on the **Account Provisioning** category to only see the provisioning events for that app.</span></span> <span data-ttu-id="4630c-113">특성 매핑에서 사용자에 대해 구성된 "일치 ID"를 기반으로 사용자를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4630c-113">You can search for users based on the “matching ID” that was configured for them in the attribute mappings.</span></span> 

<span data-ttu-id="4630c-114">예를 들어 Azure AD 측에서 "사용자 계정 이름" 또는 "메일 주소"를 일치하는 특성으로 구성하고 프로비저닝하지 않는 사용자의 값이 "audrey@contoso.com"인 경우 감사 로그에서 "audrey@contoso.com"을 검색한 후 반환된 항목을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="4630c-114">For example, if you configured the “user principal name” or “email address” as the matching attribute on the Azure AD side, and the user not being provisioning has a value of “audrey@contoso.com”, then search the audit logs for “audrey@contoso.com” and review then entries returned.</span></span>

<span data-ttu-id="4630c-115">프로비저닝 감사 로그에는 다음을 포함하여 프로비저닝 서비스에서 수행한 모든 작업이 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="4630c-115">The provisioning audit logs record all the operations performed by the provisioning service, including:</span></span>

* <span data-ttu-id="4630c-116">프로비저닝 범위에 있는 할당된 사용자에 대해 Azure AD 쿼리</span><span class="sxs-lookup"><span data-stu-id="4630c-116">Querying Azure AD for assigned users that are in scope for provisioning</span></span>
* <span data-ttu-id="4630c-117">해당 사용자의 존재에 대해 대상 앱 쿼리</span><span class="sxs-lookup"><span data-stu-id="4630c-117">Querying the target app for the existence of those users</span></span>
* <span data-ttu-id="4630c-118">시스템 간의 사용자 개체 비교</span><span class="sxs-lookup"><span data-stu-id="4630c-118">Comparing the user objects between the system</span></span>
* <span data-ttu-id="4630c-119">비교를 기반으로 대상 시스템에서 사용자 계정 추가, 업데이트 또는 비활성화</span><span class="sxs-lookup"><span data-stu-id="4630c-119">Adding, updating, or disabling the user account in the target system based on the comparison</span></span>

## <a name="next-steps"></a><span data-ttu-id="4630c-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4630c-120">Next steps</span></span>
<span data-ttu-id="4630c-121">[Azure Active Directory를 사용하여 SaaS 응용 프로그램의 사용자를 자동으로 프로비저닝 및 프로비저닝 해제](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''</span><span class="sxs-lookup"><span data-stu-id="4630c-121">[Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''</span></span>
