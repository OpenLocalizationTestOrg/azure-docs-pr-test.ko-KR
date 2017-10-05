---
title: "Azure Active Directory의 라이선스 사용자 | Microsoft Docs"
description: "Azure Active Directory에서 본인 및 사용자의 라이선스를 허가하는 방법을 알아봅니다."
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
custom: it-pro
ms.openlocfilehash: c4509cdb003687083d0456c1957b19cf35ee056a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="quickstart-license-users-in-azure-active-directory"></a><span data-ttu-id="a253e-103">빠른 시작: Azure Active Directory에서 사용자의 라이선스</span><span class="sxs-lookup"><span data-stu-id="a253e-103">Quickstart: License users in Azure Active Directory</span></span>
<span data-ttu-id="a253e-104">라이선스 기반 Azure AD 서비스는 Azure 테넌트에서 Azure AD(Active Directory) 구독을 활성화하면 작동됩니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-104">License-based Azure AD services work by activating an Azure Active Directory (Azure AD) subscription in your Azure tenant.</span></span> <span data-ttu-id="a253e-105">구독이 활성화된 후 서비스 기능은 Azure AD 관리자가 관리하고 사용이 허가된 사용자가 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-105">After the subscription is active, service capabilities are managed by Azure AD administrators and used by licensed users.</span></span> <span data-ttu-id="a253e-106">Enterprise Mobility + Security, Azure AD Premium 또는 Azure AD Basic을 구매하면 디렉터리의 유효 기간 및 선불 라이선스를 포함하여 테넌트가 구독으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-106">When you purchase Enterprise Mobility + Security, Azure AD Premium, or Azure AD Basic, your tenant is updated with the subscription, including its validity period and prepaid licenses.</span></span> <span data-ttu-id="a253e-107">할당되거나 사용 가능한 라이선스 수를 포함한 구독 정보는 **라이선스** 타일을 열어 **Azure Active Directory** 아래에서 Azure Portal을 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-107">Your subscription information, including the number of assigned or available licenses, is available through the Azure portal under **Azure Active Directory** by opening the **Licenses** tile.</span></span> <span data-ttu-id="a253e-108">**라이선스** 블레이드는 사용자 라이선스 할당을 관리하기에 가장 적합한 위치이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-108">The **Licenses** blade is also the best place to manage your license assignments.</span></span>

<span data-ttu-id="a253e-109">유료 기능을 구성하기 위해서는 구독을 얻기만 하면 되지만, Azure AD 유료 기능에 대한 사용자 라이선스를 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-109">Although obtaining a subscription is all you need to configure paid capabilities, you must still assign user licenses for paid Azure AD paid features.</span></span> <span data-ttu-id="a253e-110">액세스 권한이 있어야 하거나 Azure AD 유료 기능을 통해 관리되는 모든 사용자에게 라이선스가 할당되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-110">Any user who should have access to, or who is managed through, an Azure AD paid feature must be assigned a license.</span></span> <span data-ttu-id="a253e-111">라이선스 할당은 Azure AD Premium, Basic 또는 Enterprise Mobility + Security 등의 구매한 서비스와 사용자 간의 매핑입니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-111">License assignment is a mapping between a user and a purchased service, such as Azure AD Premium, Basic, or Enterprise Mobility + Security.</span></span>

<span data-ttu-id="a253e-112">[그룹 기반 라이선스 할당](active-directory-licensing-whatis-azure-portal.md)을 사용하여 다음과 같은 규칙을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-112">You can use [group-based license assignment](active-directory-licensing-whatis-azure-portal.md) to set up rules such as the following:</span></span>
* <span data-ttu-id="a253e-113">디렉터리의 모든 사용자가 자동으로 라이선스를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-113">All users in your directory automatically get a license</span></span>
* <span data-ttu-id="a253e-114">해당하는 직위를 가진 모든 사용자가 라이선스를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-114">Everyone with the appropriate job title gets a license</span></span>
* <span data-ttu-id="a253e-115">[셀프 서비스 그룹](active-directory-accessmanagement-self-service-group-management.md)을 사용하여 조직의 다른 관리자에게 의사 결정을 위임할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-115">You can delegate the decision to other managers in the organization (by using [self-service groups](active-directory-accessmanagement-self-service-group-management.md))</span></span>

> [!TIP]
> <span data-ttu-id="a253e-116">고급 시나리오 및 Office 365 라이선스 시나리오를 비롯한 그룹에 대한 라이선스 할당의 자세한 내용은 [Azure Active Directory에서 그룹 멤버 자격에 따라 사용자에게 라이선스 할당](active-directory-licensing-group-assignment-azure-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a253e-116">For a detailed discussion of license assignment to groups, including advanced scenarios and Office 365 licensing scenarios, see [Assign licenses to users by group membership in Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md).</span></span>

## <a name="assign-licenses-to-users-and-groups"></a><span data-ttu-id="a253e-117">사용자 및 그룹에 라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="a253e-117">Assign licenses to users and groups</span></span>
<span data-ttu-id="a253e-118">활성 구독을 사용하면 먼저 자신에게 라이선스를 할당하고 구독에 포함된 예상된 기능을 모두 표시하도록 브라우저를 새로 고쳐야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-118">Using an active subscription, you should first assign a license to yourself and refresh your browser to ensure that you see all of the expected features included with your subscription.</span></span> <span data-ttu-id="a253e-119">다음 단계는 유료 Azure AD 기능에 액세스해야 할 사용자에게 라이선스를 할당하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-119">The next step is to assign licenses to the users who need access to paid Azure AD features.</span></span> <span data-ttu-id="a253e-120">라이선스를 할당하는 쉬운 방법은 개인 대신 사용자의 그룹에 라이선스를 할당하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-120">An easy way to assign licenses is to assign licenses to groups of users rather than to individuals.</span></span> <span data-ttu-id="a253e-121">그룹에게 라이선스를 할당하면 모든 그룹 구성원에게 라이선스가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-121">When you assign licenses to a group, all group members are assigned a license.</span></span> <span data-ttu-id="a253e-122">사용자가 그룹에서 추가 또는 제거될 경우 해당 라이선스가 자동으로 할당 또는 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-122">If users are added or removed from the group, the appropriate license is automatically assigned or removed.</span></span> 

> [!NOTE]
> <span data-ttu-id="a253e-123">일부 Microsoft 서비스는 모든 위치에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-123">Some Microsoft services are not available in all locations.</span></span> <span data-ttu-id="a253e-124">사용자에게 라이선스를 할당하려면 먼저 관리자가 해당 사용자에 대해 “**사용 위치**” 속성을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-124">Before a license can be assigned to a user, the administrator must specify the **Usage location** property for the user.</span></span> <span data-ttu-id="a253e-125">Azure Portal의 **사용자** &gt; **프로필** &gt; **설정**에서 이 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-125">You can set this property under **User** &gt; **Profile** &gt; **Settings** in the Azure portal.</span></span> <span data-ttu-id="a253e-126">그룹 라이선스 할당을 사용할 때 사용 위치가 지정되지 않은 사용자는 디렉터리의 위치를 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-126">When using group license assignment, any user whose usage location is not specified inherits the location of the directory.</span></span>

<span data-ttu-id="a253e-127">라이선스를 할당하려면 **Azure Active Directory** &gt; **라이선스** &gt; **모든 제품** 아래에서 제품을 하나 이상 선택하고 명령 모음에서 **할당** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-127">To assign a license, under **Azure Active Directory** &gt; **Licenses** &gt; **All Products**, select one or more products, and then select **Assign** on the command bar.</span></span>

![할당할 라이선스 선택](media/license-users-groups/select-license-to-assign.png)

<span data-ttu-id="a253e-129">**사용자 및 그룹** 블레이드를 사용하여 여러 사용자나 그룹을 선택하거나 제품의 서비스 계획을 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-129">You can use the **Users and groups** blade to choose multiple users or groups or to disable service plans in the product.</span></span> <span data-ttu-id="a253e-130">맨 위에 있는 검색 상자를 사용하여 사용자 및 그룹 이름을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-130">Use the search box on top to search for user and group names.</span></span>

![라이선스 할당을 위한 사용자 또는 그룹 선택](media/license-users-groups/select-user-for-license-assignment.png)

<span data-ttu-id="a253e-132">라이선스를 그룹에 할당할 때는 모든 사용자가 라이선스를 상속하기 전에 그룹 크기에 따라 다소 시간이 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-132">When you assign licenses to a group, it can take some time before all users inherit the license depending on the size of the group.</span></span> <span data-ttu-id="a253e-133">**그룹** 블레이드의 **라이선스** 타일 아래에서 처리 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-133">You can check the processing status on the **Group** blade, under the **Licenses** tile.</span></span>

![라이선스 할당 상태](media/license-users-groups/license-assignment-status.png)

<span data-ttu-id="a253e-135">Azure AD 라이선스 할당 중에 할당 오류가 발생할 수 있지만 Azure AD 및 Enterprise Mobility + Security 제품을 관리할 경우에는 상대적으로 드물게 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-135">Assignment errors can occur during Azure AD license assignment but are relatively rare when managing Azure AD and Enterprise Mobility + Security products.</span></span> <span data-ttu-id="a253e-136">잠재적 할당 오류는 다음으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-136">Potential assignment errors are limited to:</span></span>
- <span data-ttu-id="a253e-137">할당 충돌: 사용자에게 이전에 할당된 라이선스가 현재 라이선스와 호환되지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="a253e-137">Assignment conflict: When a user was previously assigned a license that is incompatible with the current license.</span></span> <span data-ttu-id="a253e-138">이런 경우, 새 라이선스를 할당하려면 현재 라이선스를 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-138">In this case, assigning the new license requires removing the current one.</span></span>
- <span data-ttu-id="a253e-139">사용 가능한 라이선스 수 초과: 할당된 그룹의 사용자 수가 사용 가능한 라이선스 수를 초과한 경우 없는 라이선스로 인해 사용자의 할당 상태가 할당 실패로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-139">Exceeded available licenses: When the number of users in assigned groups exceeds the available licenses, a user's assignment status reflects a failure to assign due to missing licenses.</span></span>

### <a name="azure-ad-b2b-collaboration-licensing"></a><span data-ttu-id="a253e-140">Azure AD B2B 공동 작업 라이선스</span><span class="sxs-lookup"><span data-stu-id="a253e-140">Azure AD B2B collaboration licensing</span></span>

<span data-ttu-id="a253e-141">B2B 공동 작업을 통해 게스트 사용자를 Azure AD 테넌트로 초대해서 Azure AD 서비스 및 사용 가능하게 설정할 Azure 리소스에 대한 액세스 권한을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-141">B2B collaboration allows you to invite guest users into your Azure AD tenant to provide access to Azure AD services and any Azure resources you make available.</span></span>  

<span data-ttu-id="a253e-142">B2B 사용자를 초대한 후 Azure AD에서 응용 프로그램에 할당하는 과정은 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-142">There is no charge for inviting B2B users and assigning them to an application in Azure AD.</span></span> <span data-ttu-id="a253e-143">게스트 사용자당 최대 10개 앱과 3개의 기본 보고서도 B2B 공동 작업 사용자에게 무료로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-143">Up to 10 apps per guest user and 3 basic reports are also free for B2B collaboration users.</span></span> <span data-ttu-id="a253e-144">파트너의 Azure AD 테넌트에서 게스트 사용자에게 적절한 라이선스가 할당되어 있으면 여러분의 테넌트에서도 게스트 사용자에게 사용이 허가됩니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-144">If your guest user has any appropriate licenses assigned in the partner's Azure AD tenant, they'll be licensed in yours as well.</span></span>

<span data-ttu-id="a253e-145">필수는 아니지만 유료 Azure AD 기능에 대한 액세스 권한을 제공하려면 해당 B2B 게스트 사용자는 적절한 Azure AD 라이선스의 사용 허가를 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-145">It's not required, but if you want to provide access to paid Azure AD features, those B2B guest users must be licensed with appropriate Azure AD licenses.</span></span> <span data-ttu-id="a253e-146">Azure AD 유료 라이선스가 있는 초대하는 테넌트는 테넌트에 초대된 5명의 추가 게스트 사용자에게 B2B 공동 작업 사용자 권한을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-146">An inviting tenant with an Azure AD paid license can assign B2B collaboration user rights to an additional five guest users invited to the tenant.</span></span> <span data-ttu-id="a253e-147">시나리오와 정보는 [B2B 공동 작업 라이선스 지침](active-directory-b2b-licensing.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a253e-147">For scenarios and information, see [B2B collaboration licensing guidance](active-directory-b2b-licensing.md).</span></span>

## <a name="view-assigned-licenses"></a><span data-ttu-id="a253e-148">할당된 라이선스 보기</span><span class="sxs-lookup"><span data-stu-id="a253e-148">View assigned licenses</span></span>

<span data-ttu-id="a253e-149">할당된 라이선스 및 사용 가능한 라이선스에 대한 요약 보기는 **Azure Active Directory** &gt; **라이선스** &gt; **모든 제품** 아래 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-149">A summary view of assigned and available licenses is displayed under **Azure Active Directory** &gt; **Licenses** &gt; **All products**.</span></span>

![라이선스 요약 보기](media/license-users-groups/view-license-summary.png)

<span data-ttu-id="a253e-151">특정 제품을 선택할 때 사용 가능한 할당된 사용자 및 그룹의 자세한 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-151">A detailed list of assigned users and groups is available when selecting a specific product.</span></span> <span data-ttu-id="a253e-152">**허가된 사용자**에는 현재 라이선스를 사용 중인 모든 사용자와 함께 라이선스가 사용자에게 직접 할당되었는지, 그룹에서 상속되는지 여부가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-152">The **Licensed Users** list shows all users currently consuming a license and whether the license was assigned directly to the user or if it is inherited from a group.</span></span>

![라이선스 세부 정보 보기](media/license-users-groups/view-license-detail.png)

<span data-ttu-id="a253e-154">마찬가지로 **허가된 그룹**은 라이선스가 할당된 모든 그룹을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-154">Similarly, the **Licensed Groups** list shows all groups to which licenses have been assigned.</span></span> <span data-ttu-id="a253e-155">사용자 또는 그룹을 선택하면 해당 개체에 할당된 모든 라이선스를 보여 주는 **라이선스** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-155">Select a user or group to open the **Licenses** blade, which shows all licenses assigned to that object.</span></span>

## <a name="remove-a-license"></a><span data-ttu-id="a253e-156">라이선스 제거</span><span class="sxs-lookup"><span data-stu-id="a253e-156">Remove a license</span></span>

<span data-ttu-id="a253e-157">라이선스를 제거하려면 사용자 또는 그룹으로 이동하고 **라이선스** 타일이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-157">To remove a license, go to the user or group, and open the **Licenses** tile.</span></span> <span data-ttu-id="a253e-158">라이선스를 선택하고 **제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-158">Select the license, and click **Remove**.</span></span>

![라이선스 제거](media/license-users-groups/remove-license.png)

<span data-ttu-id="a253e-160">그룹에서 사용자에 상속된 라이선스는 직접 제거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-160">Licenses inherited by the user from a group cannot be removed directly.</span></span> <span data-ttu-id="a253e-161">대신, 라이선스를 상속하는 그룹에서 사용자를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-161">Instead, remove the user from the group from which they are inheriting the license.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a253e-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a253e-162">Next steps</span></span>
<span data-ttu-id="a253e-163">이 빠른 시작에서는 Azure AD 디렉터리의 사용자 및 그룹에 라이선스를 할당하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-163">In this quickstart, you’ve learned how to assign licenses to users and groups in Azure AD directory.</span></span> 

<span data-ttu-id="a253e-164">다음 링크를 통해 Azure Portal에서 Azure AD에 구독 라이선스 할당을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a253e-164">You can use the following link to configure subscription license assignments in Azure AD from the Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a253e-165">Azure AD 라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="a253e-165">Assign Azure AD licenses</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Overview) 