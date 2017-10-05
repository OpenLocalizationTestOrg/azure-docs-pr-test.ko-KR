---
title: "보안 경고를 구성하는 방법 | Microsoft Docs"
description: "Azure Privileged Identity Management 확장에 대한 보안 경고를 구성하는 방법 배우기"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 4e0c911a-36c6-42a0-8f79-a01c03d2d04f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: e057120e31eeebc3da274536c09d6d9972854338
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-security-alerts-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="062b0-103">Azure AD Privileged Identity Management 에서 보안 경고를 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="062b0-103">How to configure security alerts in Azure AD Privileged Identity Management</span></span>
## <a name="security-alerts"></a><span data-ttu-id="062b0-104">보안 경고</span><span class="sxs-lookup"><span data-stu-id="062b0-104">Security alerts</span></span>
<span data-ttu-id="062b0-105">Azure Privileged Identity Management(PIM)은 사용자의 환경에 의심스럽거나 안전하지 않은 활동이 있을 때 경고를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-105">Azure Privileged Identity Management (PIM) generates alerts when there is suspicious or unsafe activity in your environment.</span></span> <span data-ttu-id="062b0-106">경고가 트리거될 때 PIM 대시보드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-106">When an alert is triggered, it shows up on the PIM dashboard.</span></span> <span data-ttu-id="062b0-107">경고를 선택하여 경고를 트리거하는 사용자 또는 역할을 나열하는 보고서를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-107">Select the alert to see a report that lists the users or roles that triggered the alert.</span></span>

![PIM 대시보드 보안 경고 - 스크린 샷][1]

| <span data-ttu-id="062b0-109">경고</span><span class="sxs-lookup"><span data-stu-id="062b0-109">Alert</span></span> | <span data-ttu-id="062b0-110">트리거</span><span class="sxs-lookup"><span data-stu-id="062b0-110">Trigger</span></span> | <span data-ttu-id="062b0-111">권장 사항</span><span class="sxs-lookup"><span data-stu-id="062b0-111">Recommendation</span></span> |
| --- | --- | --- |
| <span data-ttu-id="062b0-112">**역할이 PIM 외부에서 할당됨**</span><span class="sxs-lookup"><span data-stu-id="062b0-112">**Roles are being assigned outside of PIM**</span></span> |<span data-ttu-id="062b0-113">관리자가 PIM 인터페이스 외부에서 영구적으로 역할에 할당되었습니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-113">An administrator was permanently assigned to a role, outside of the PIM interface.</span></span> |<span data-ttu-id="062b0-114">새 역할 할당을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-114">Review the new role assignment.</span></span> <span data-ttu-id="062b0-115">다른 서비스는 영구 관리자만 할당할 수 있으므로 필요한 경우 그것을 적격 할당으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-115">Since other services can only assign permanent administrators, change it to an eligible assignment if necessary.</span></span> |
| <span data-ttu-id="062b0-116">**역할이 너무 자주 활성화됨**</span><span class="sxs-lookup"><span data-stu-id="062b0-116">**Roles are being activated too frequently**</span></span> |<span data-ttu-id="062b0-117">설정에 허용된 시간 내에 동일한 역할을 다시 활성화한 횟수가 너무 많습니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-117">There were too many reactivations of the same role within the time allowed in the settings.</span></span> |<span data-ttu-id="062b0-118">사용자에게 연락하여 역할을 그처럼 많이 활성화한 이유를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-118">Contact the user to see why they have activated the role so many times.</span></span> <span data-ttu-id="062b0-119">어쩌면 해당 작업을 끝내기에는 시간 제한이 너무 짧거나 또는 역할을 자동으로 활성화하기 위해 스크립트를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-119">Maybe the time limit is too short for them to complete their tasks, or maybe they're using scripts to automatically activate a role.</span></span> |
| <span data-ttu-id="062b0-120">**역할이 활성화를 위해 Multi-Factor Authentication을 필요로 하지 않음**</span><span class="sxs-lookup"><span data-stu-id="062b0-120">**Roles don't require multi-factor authentication for activation**</span></span> |<span data-ttu-id="062b0-121">MFA를 사용하도록 설정되지 않은 역할이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-121">There are roles without MFA enabled in the settings.</span></span> |<span data-ttu-id="062b0-122">가장 높은 권한을 가진 역할에 MFA가 필요하지만 모든 역할을 활성화하기 위해 MFA를 사용하도록 적극 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-122">We require MFA for the most highly privileged roles, but strongly encourage that you enable MFA for activation of all roles.</span></span> |
| <span data-ttu-id="062b0-123">**관리자가 권한 있는 역할을 사용 하지 않음**</span><span class="sxs-lookup"><span data-stu-id="062b0-123">**Administrators aren't using their privileged roles**</span></span> |<span data-ttu-id="062b0-124">최근에 해당 역할을 활성화하지 않은 적합한 관리자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-124">There are eligible administrators that haven’t activated their roles recently.</span></span> |<span data-ttu-id="062b0-125">더 이상 액세스가 필요 없는 사용자를 확인하기 위해 액세스 검토를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-125">Start an access review to determine the users that don't need access anymore.</span></span> |
| <span data-ttu-id="062b0-126">**전역 관리자가 너무 많음**</span><span class="sxs-lookup"><span data-stu-id="062b0-126">**There are too many global administrators**</span></span> |<span data-ttu-id="062b0-127">권장하는 것보다 전역 관리자가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-127">There are more global administrators than recommended.</span></span> |<span data-ttu-id="062b0-128">많은 수의 전역 관리자가 있을 경우, 사용자가 필요 이상으로 많은 사용 권한을 갖게 될 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-128">If you have a high number of global administrators, it's likely that users are getting more permissions than they need.</span></span> <span data-ttu-id="062b0-129">사용자를 낮은 권한의 역할로 이동하거나, 그 중 일부를 영구 할당 대신에 적격 할당으로 역할을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-129">Move users to less privileged roles, or make some of them eligible for the role instead of permanently assigned.</span></span> |

## <a name="configure-security-alert-settings"></a><span data-ttu-id="062b0-130">보안 경고 설정 구성</span><span class="sxs-lookup"><span data-stu-id="062b0-130">Configure security alert settings</span></span>
<span data-ttu-id="062b0-131">PIM의 일부 보안 경고를 환경 및 보안 목표에 맞게 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-131">You can customize some of the security alerts in PIM to work with your environment and security goals.</span></span> <span data-ttu-id="062b0-132">설정 블레이드에 도달하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-132">Follow these steps to reach the settings blade:</span></span>

1. <span data-ttu-id="062b0-133">[Azure 포털](https://portal.azure.com/) 에 로그인하고 대시보드에서 **Azure AD Privileged Identity Management** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-133">Sign in to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** tile from the dashboard.</span></span>
2. <span data-ttu-id="062b0-134">**권한 있는 역할 관리** > **설정** > **경고 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-134">Select **Managed privileged roles** > **Settings** > **Alerts settings**.</span></span>
   
    ![보안 경고 설정으로 이동][2]

### <a name="roles-are-being-activated-too-frequently-alert"></a><span data-ttu-id="062b0-136">"역할이 너무 자주 활성화됨" 경고</span><span class="sxs-lookup"><span data-stu-id="062b0-136">"Roles are being activated too frequently" alert</span></span>
<span data-ttu-id="062b0-137">사용자가 지정된 기간 내에 동일한 권한 있는 역할을 여러 번 활성화한다면 이 경고가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-137">This alert triggers if a user activates the same privileged role multiple times within a specified period.</span></span> <span data-ttu-id="062b0-138">기간 및 활성화 횟수를 모두 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-138">You can configure both the time period and the number of activations.</span></span>

* <span data-ttu-id="062b0-139">**활성화 갱신 기간**: 의심스러운 갱신을 추적하는 데 사용할 기간을 일, 시, 분, 초로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-139">**Activation renewal timeframe**: Specify in days, hours, minutes, and second the time period you want to use to track suspicious renewals.</span></span>
* <span data-ttu-id="062b0-140">**활성화 갱신 회수**: 선택한 기간 내에 경고할만하다고 생각되는 활성화 회수를 2~100 사이로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-140">**Number of activation renewals**: Specify the number of activations, from 2 to 100, that you consider worthy of alert, within the timeframe you chose.</span></span> <span data-ttu-id="062b0-141">슬라이더를 이동하거나 텍스트 상자에 숫자를 입력하여 이 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-141">You can change this setting by moving the slider, or typing a number in the text box.</span></span>

### <a name="there-are-too-many-global-administrators-alert"></a><span data-ttu-id="062b0-142">"전역 관리자가 너무 많음" 경고</span><span class="sxs-lookup"><span data-stu-id="062b0-142">"There are too many global administrators" alert</span></span>
<span data-ttu-id="062b0-143">PIM은 서로 다른 두 조건이 충족되고, 그 두 조건을 모두 구성할 수 있을 때 이 경고를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-143">PIM triggers this alert if two different criteria are met, and you can configure both of them.</span></span> <span data-ttu-id="062b0-144">첫째, 전역 관리자의 특정 임계값에 도달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-144">First, you need to reach a certain threshold of global administrators.</span></span> <span data-ttu-id="062b0-145">둘째, 총 역할 할당의 특정 비율이 전역 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-145">Second, a certain percentage of your total role assignments must be global administrators.</span></span> <span data-ttu-id="062b0-146">이런 측정값의 하나만 충족된다면 경고가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-146">If you only meet one of these measurements, the alert does not appear.</span></span>  

* <span data-ttu-id="062b0-147">**전역 관리자 최소 수**: 안전하지 않다고 생각하는 전역 관리자 수를 2와 100 사이에서 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-147">**Minimum number of Global Administrators**: Specify the number of global administrators, from 2 to 100, that you consider an unsafe amount.</span></span>
* <span data-ttu-id="062b0-148">**전역 관리자 비율**: 사용자 환경에 안전하지 않는 전역 관리자 비율을 0%과 100% 사이에서 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-148">**Percentage of global administrators**: Specify the percentage of administrators who are global administrators, from 0% to 100%, that is unsafe in your environment.</span></span>

### <a name="administrators-arent-using-their-privileged-roles-alert"></a><span data-ttu-id="062b0-149">“관리자가 권한 있는 역할을 사용 하지 않음” 경고</span><span class="sxs-lookup"><span data-stu-id="062b0-149">"Administrators aren't using their privileged roles" alert</span></span>
<span data-ttu-id="062b0-150">사용자가 특정 시간 동안 역할을 활성화하지 않는다면 이 경고가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-150">This alert triggers if a user goes a certain amount of time without activating a role.</span></span>

* <span data-ttu-id="062b0-151">**일 수**: 사용자가 역할을 활성화하지 않고 지낼 수 있는 일 수를 0 과 100 사이에서 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="062b0-151">**Number of days**: Specify the number of days, from 0 to 100, that a user can go without activating a role.</span></span>

## <a name="next-steps"></a><span data-ttu-id="062b0-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="062b0-152">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_dash.png
[2]: ./media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_settings.png
