---
title: "Azure AD Privileged Identity Management 보안 마법사"
description: "Azure Active Directory Privileged Identity Management 확장을 처음 실행하면 보안 마법사가 표시됩니다. 이 문서는 마법사를 사용하는 단계를 설명합니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: a53a3719-8cc7-4fc7-8164-aafca192871b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: 260d178f3d8158411b3ad266e3b0d15edbebc722
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-security-wizard-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="bc1f2-104">Azure AD Privileged Identity Management에서 보안 마법사 사용</span><span class="sxs-lookup"><span data-stu-id="bc1f2-104">Using the security wizard in Azure AD Privileged Identity Management</span></span> 
<span data-ttu-id="bc1f2-105">조직에 대해 Azure PIM(Privileged Identity Management)을 처음 실행하면 마법사가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc1f2-105">If you're the first person to run Azure Privileged Identity Management (PIM) for your organization, you will be presented with a wizard.</span></span> <span data-ttu-id="bc1f2-106">마법사는 권한 있는 ID에 대한 보안 위험을 이해하고 위험을 줄이도록 PIM을 사용하는 방법을 이해하도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="bc1f2-106">The wizard helps you understand the security risks of privileged identities and how to use PIM to reduce those risks.</span></span> <span data-ttu-id="bc1f2-107">나중에 작업하려는 경우 마법사에서 기존 역할 할당을 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bc1f2-107">You don't need to make any changes to existing role assignments in the wizard, if you prefer to do it later.</span></span>

## <a name="what-to-expect"></a><span data-ttu-id="bc1f2-108">예상 프로그램</span><span class="sxs-lookup"><span data-stu-id="bc1f2-108">What to expect</span></span>
<span data-ttu-id="bc1f2-109">조직에서 PIM 사용을 시작하기 전에 모든 역할 할당은 영구적입니다. 현재 해당 권한이 필요하지 않는 경우에도 사용자는 항상 이러한 역할에 할당되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc1f2-109">Before your organization starts using PIM, all role assignments are permanent: the users are always in these roles even if they do not presently need their privileges.</span></span>  <span data-ttu-id="bc1f2-110">마법사의 첫 번째 단계에서는 권한이 높은 역할의 목록과 얼마나 많은 사용자가 현재 해당 역할에 있는지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bc1f2-110">The first step of the wizard shows you a list of high-privileged roles and how many users are currently in those roles.</span></span> <span data-ttu-id="bc1f2-111">특정 역할을 자세히 알아보면 익숙하지 않은 사용자에 대해 더 잘 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc1f2-111">You can drill in to a particular role to learn more about users if one or more of them are unfamiliar.</span></span>

<span data-ttu-id="bc1f2-112">마법사의 두 번째 단계는 관리자의 역할 할당을 변경할 기회를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1f2-112">The second step of the wizard gives you an opportunity to change administrator's role assignments.</span></span>  

> [!WARNING]
> <span data-ttu-id="bc1f2-113">Microsoft 계정이 아니라 조직 계정을 사용하는 적어도 한 명의 전역 관리자와 둘 이상의 권한 있는 역할 관리자가 있는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1f2-113">It is important that you have at least one global administrator, and more than one privileged role administrator with an organizational account (not a Microsoft account).</span></span> <span data-ttu-id="bc1f2-114">권한 있는 역할 관리자가 한 명인 경우 해당 계정이 삭제되면 조직은 PIM을 관리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bc1f2-114">If there is only one privileged role administrator, the organization will not be able to manage PIM if that account is deleted.</span></span>
> <span data-ttu-id="bc1f2-115">또한 사용자가 Microsoft 계정 (Skype나 Outlook.com과 같은 Microsoft 서비스에 로그인 하는 데 사용하는 계정)을 가진 경우 역할 할당을 영구적으로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="bc1f2-115">Also, keep role assignments permanent if a user has a Microsoft account (An account they use to sign in to Microsoft services like Skype and Outlook.com).</span></span> <span data-ttu-id="bc1f2-116">해당 역할의 활성화에 대해 MFA를 요구하려는 경우 해당 사용자가 잠기게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc1f2-116">If you plan to require MFA for activation for that role, that user will be locked out.</span></span>
> 
> 

<span data-ttu-id="bc1f2-117">항목을 변경한 후에는 마법사가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bc1f2-117">After you have made changes, the wizard will no longer show up.</span></span> <span data-ttu-id="bc1f2-118">다음에 사용자 또는 다른 권한 있는 역할 관리자가 PIM을 사용할 때 PIM 대시보드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc1f2-118">The next time you or another privileged role administrator use PIM, you will see the PIM dashboard.</span></span>  

* <span data-ttu-id="bc1f2-119">역할에서 사용자를 추가 또는 제거하거나 영구에서 적격으로 할당을 변경하려면 [사용자의 역할을 추가 또는 제거하는 방법](active-directory-privileged-identity-management-how-to-add-role-to-user.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bc1f2-119">If you would like to add or remove users from roles or change assignments from permanent to eligible, read more at [how to add or remove a user's role](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span></span>
* <span data-ttu-id="bc1f2-120">더 많은 사용자에게 PIM을 관리하기 위해 액세스 권한을 제공하려면 [PIM을 관리하기 위해 액세스 권한을 제공하는 방법](active-directory-privileged-identity-management-how-to-give-access-to-pim.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bc1f2-120">If you would like to give more users access to manage PIM, read more at [how to give access to manage in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc1f2-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bc1f2-121">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

