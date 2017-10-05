---
title: "그룹의 동적 구성원 자격 문제 해결| Microsoft Docs"
description: "Azure AD의 그룹에 대한 동적 멤버 자격 문제 해결 팁입니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 89bb04b6-a379-49c2-8465-fe386641816a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 32947e8cc69c9a48d9a285bf0a37ab3398571f86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a><span data-ttu-id="e0a59-103">그룹의 동적 멤버 자격 문제 해결</span><span class="sxs-lookup"><span data-stu-id="e0a59-103">Troubleshooting dynamic memberships for groups</span></span>
<span data-ttu-id="e0a59-104">**그룹에 대한 규칙을 구성했으나 그룹에서 구성원이 업데이트되지 않음**</span><span class="sxs-lookup"><span data-stu-id="e0a59-104">**I configured a rule on a group but no memberships get updated in the group**</span></span><br/><span data-ttu-id="e0a59-105">**구성** 탭에서 **위임된 그룹 관리 사용** 설정이 **예**로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a59-105">Verify that the **Enable delegated group management** setting is set to **Yes** in the **Configure** tab.</span></span> <span data-ttu-id="e0a59-106">이 설정은 Azure Active Directory Premium 라이선스를 할당한 사용자로 로그인하는 경우에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0a59-106">You will see this setting only if you are signed in as a user to whom an Azure Active Directory Premium license is assigned.</span></span> <span data-ttu-id="e0a59-107">규칙의 사용자 특성 값을 확인합니다. 규칙을 충족하는 사용자가 있나요?</span><span class="sxs-lookup"><span data-stu-id="e0a59-107">Verify the values for user attributes on the rule: are there users that satisfy the rule?</span></span>

<span data-ttu-id="e0a59-108">**규칙을 구성했으나 규칙의 기존 구성원이 제거됨**</span><span class="sxs-lookup"><span data-stu-id="e0a59-108">**I configured a rule, but now the existing members of the rule are removed**</span></span><br/><span data-ttu-id="e0a59-109">이는 정상적인 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="e0a59-109">This is expected behavior.</span></span> <span data-ttu-id="e0a59-110">규칙을 사용하도록 설정하거나 변경하면 그룹의 기존 멤버가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0a59-110">Existing members of the group are removed when a rule is enabled or changed.</span></span> <span data-ttu-id="e0a59-111">규칙 평가에서 반환된 사용자는 그룹에 멤버로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0a59-111">The users returned from evaluation of the rule are added as members to the group.</span></span>     

<span data-ttu-id="e0a59-112">**규칙을 추가하거나 변경하는 즉시 멤버 자격 변경 내용이 표시되지 않는 이유는?**</span><span class="sxs-lookup"><span data-stu-id="e0a59-112">**I don’t see membership changes instantly when I add or change a rule, why not?**</span></span><br/><span data-ttu-id="e0a59-113">위임된 구성원은 비동기식 백그라운드 프로세스에서 주기적으로 평가되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="e0a59-113">Dedicated membership evaluation is done periodically in an asynchronous background process.</span></span> <span data-ttu-id="e0a59-114">프로세스에서 걸리는 시간은 디렉터리의 사용자 수와 규칙 결과로 만들어진 그룹의 크기로 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0a59-114">How long the process takes is determined by the number of users in your directory and the size of the group created as a result of the rule.</span></span> <span data-ttu-id="e0a59-115">일반적으로 사용자 수가 적은 디렉터리에는 2-3분 내에 그룹 멤버 자격 변경 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0a59-115">Typically, directories with small numbers of users will see the group membership changes in less than a few minutes.</span></span> <span data-ttu-id="e0a59-116">사용자 수가 많은 디렉터리는 채우는 데 30분 이상이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0a59-116">Directories with a large number of users can take 30 minutes or longer to populate.</span></span>

### <a name="next-steps"></a><span data-ttu-id="e0a59-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e0a59-117">Next steps</span></span>
<span data-ttu-id="e0a59-118">이러한 문서는 Azure Active Directory에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e0a59-118">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="e0a59-119">Azure Active Directory 그룹을 사용하여 리소스에 대한 액세스 관리</span><span class="sxs-lookup"><span data-stu-id="e0a59-119">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="e0a59-120">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="e0a59-120">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="e0a59-121">Azure Active Directory란?</span><span class="sxs-lookup"><span data-stu-id="e0a59-121">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="e0a59-122">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="e0a59-122">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
