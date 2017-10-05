---
title: "Azure Application Insights에서 리소스, 역할 및 액세스 제어 | Microsoft Docs"
description: "조직 Insights의 소유자, 참여자 및 읽기 권한자입니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 49f736a5-67fe-4cc6-b1ef-51b993fb39bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: c979a8bfbeecacc7c0bbc112e02a4b68e874c219
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a><span data-ttu-id="53efa-103">Application Insights에서 리소스, 역할 및 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="53efa-103">Resources, roles, and access control in Application Insights</span></span>
<span data-ttu-id="53efa-104">[Microsoft Azure의 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)를 사용하여 Azure [Application Insights][start]의 데이터에 대한 읽기 및 업데이트 액세스를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-104">You can control who has read and update access to your data in Azure [Application Insights][start], by using [Role-based access control in Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="53efa-105">리소스 자체가 아닌 응용 프로그램 리소스가 속한 **리소스 그룹 또는 구독** 의 사용자에게 액세스 권한을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-105">Assign access to users in the **resource group or subscription** to which your application resource belongs - not in the resource itself.</span></span> <span data-ttu-id="53efa-106">**Application Insights 구성 요소 참여자** 역할을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-106">Assign the **Application Insights component contributor** role.</span></span> <span data-ttu-id="53efa-107">이렇게 하면 응용 프로그램 리소스와 함께 웹 테스트 및 경고에 대한 액세스를 통합적으로 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-107">This ensures uniform control of access to web tests and alerts along with your application resource.</span></span> <span data-ttu-id="53efa-108">[자세히 알아봅니다](#access).</span><span class="sxs-lookup"><span data-stu-id="53efa-108">[Learn more](#access).</span></span>
> 
> 

## <a name="resources-groups-and-subscriptions"></a><span data-ttu-id="53efa-109">리소스, 그룹 및 구독</span><span class="sxs-lookup"><span data-stu-id="53efa-109">Resources, groups and subscriptions</span></span>
<span data-ttu-id="53efa-110">먼저 몇 가지를 정의하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-110">First, some definitions:</span></span>

* <span data-ttu-id="53efa-111">**리소스** - Microsoft Azure 서비스의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-111">**Resource** - An instance of a Microsoft Azure service.</span></span> <span data-ttu-id="53efa-112">Application Insights는 응용 프로그램에서 보낸 원격 분석 데이터를 수집, 분석 및 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-112">Your Application Insights resource collects, analyzes and displays the telemetry data sent from your application.</span></span>  <span data-ttu-id="53efa-113">다른 유형의 Azure 리소스로는 웹 앱, 데이터베이스 및 VM이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-113">Other types of Azure resources include web apps, databases, and VMs.</span></span>
  
    <span data-ttu-id="53efa-114">리소스를 보려면 [Azure Portal][portal]을 열고 로그인한 다음 모든 리소스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-114">To see your resources, open the [Azure Portal][portal], sign in, and click All Resources.</span></span> <span data-ttu-id="53efa-115">리소스를 찾으려면 필터 필드에 리소스 이름의 일부를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-115">To find a resource, type part of its name in the filter field.</span></span>
  
    ![Azure 리소스 목록](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* <span data-ttu-id="53efa-117">[**리소스 그룹**][group] - 모든 리소스가 하나의 그룹에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-117">[**Resource group**][group] - Every resource belongs to one group.</span></span> <span data-ttu-id="53efa-118">그룹은 특히 액세스 제어에 대한 관련 리소스를 간편하게 관리할 수 있는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-118">A group is a convenient way to manage related resources, particularly for access control.</span></span> <span data-ttu-id="53efa-119">예를 들어 한 리소스 그룹에 웹 앱, 앱을 모니터링할 Application Insights 리소스, 내보낸 데이터를 보관할 저장소 리소스를 모두 집어넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-119">For example, into one resource group you could put a Web App, an Application Insights resource to monitor the app, and a Storage resource to keep exported data.</span></span>

    ![찾아보기, 리소스 그룹을 차례로 선택한 다음 그룹을 선택합니다.](./media/app-insights-resources-roles-access-control/11-group.png)

* <span data-ttu-id="53efa-121">[**구독**](https://manage.windowsazure.com) - Application Insights 또는 다른 Azure 리소스를 사용하려면 Azure 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-121">[**Subscription**](https://manage.windowsazure.com) - To use Application Insights or other Azure resources, you sign in to an Azure subscription.</span></span> <span data-ttu-id="53efa-122">모든 리소스 그룹은 Azure 구독에 속합니다. 여기에서 패키지를 선택하고, 조직 구독인 경우 멤버와 해당 액세스 권한을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-122">Every resource group belongs to one Azure subscription, where you choose your price package and, if it's an organization subscription, choose the members and their access permissions.</span></span>
* <span data-ttu-id="53efa-123">[**Microsoft 계정**][account] - Microsoft Azure 구독, XBox Live, Outlook.com 및 기타 Microsoft 서비스에 로그인하는 데 사용하는 사용자 이름 및 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-123">[**Microsoft account**][account] - The username and password that you use to sign in to Microsoft Azure subscriptions, XBox Live, Outlook.com, and other Microsoft services.</span></span>

## <span data-ttu-id="53efa-124"><a name="access"></a> 리소스 그룹의 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="53efa-124"><a name="access"></a> Control access in the resource group</span></span>
<span data-ttu-id="53efa-125">응용 프로그램에 대해 만든 리소스 외에도 경고 및 웹 테스트에 대한 별도의 리소스가 숨겨져 있다는 사실을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-125">It's important to understand that in addition to the resource you created for your application, there are also separate hidden resources for alerts and web tests.</span></span> <span data-ttu-id="53efa-126">이러한 리소스는 응용 프로그램과 동일한 [리소스 그룹](#resource-group) 에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-126">They are attached to the same [resource group](#resource-group) as your application.</span></span> <span data-ttu-id="53efa-127">웹 사이트 또는 저장소 같은 다른 Azure 서비스를 여기에 넣었을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-127">You might also have put other Azure services in there, such as websites or storage.</span></span>

![Application Insights의 리소스](./media/app-insights-resources-roles-access-control/00-resources.png)

<span data-ttu-id="53efa-129">이러한 리소스에 대한 액세스를 제어하기 위한 권장 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-129">To control access to these resources it's therefore recommended to:</span></span>

* <span data-ttu-id="53efa-130">**리소스 그룹 또는 구독** 수준에서 액세스를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-130">Control access at the **resource group or subscription** level.</span></span>
* <span data-ttu-id="53efa-131">사용자에게 **Application Insights 구성 요소 참여자** 역할을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-131">Assign the **Application Insights Component contributor** role to users.</span></span> <span data-ttu-id="53efa-132">그러면 그룹의 다른 서비스에 대한 액세스 권한을 제공하지 않아도 사용자가 웹 테스트, 경고 및 Application Insights 리소스를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-132">This allows them to edit web tests, alerts, and Application Insights resources, without providing access to any other services in the group.</span></span>

## <a name="to-provide-access-to-another-user"></a><span data-ttu-id="53efa-133">다른 사용자에 대한 액세스 권한 제공</span><span class="sxs-lookup"><span data-stu-id="53efa-133">To provide access to another user</span></span>
<span data-ttu-id="53efa-134">구독 또는 리소스 그룹에 대한 소유자 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-134">You must have Owner rights to the subscription or the resource group.</span></span>

<span data-ttu-id="53efa-135">사용자에게 [Microsoft 계정][account]이 있거나 해당 [조직의 Microsoft 계정](../active-directory/sign-up-organization.md)에 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-135">The user must have a [Microsoft Account][account], or access to their [organizational Microsoft Account](../active-directory/sign-up-organization.md).</span></span> <span data-ttu-id="53efa-136">개별 사용자에 대한 액세스 권한을 제공할 수 있으며 Azure Active Directory에 정의된 사용자 그룹에 대한 액세스 권한도 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-136">You can provide access to individuals, and also to user groups defined in Azure Active Directory.</span></span>

#### <a name="navigate-to-the-resource-group"></a><span data-ttu-id="53efa-137">리소스 그룹으로 이동</span><span class="sxs-lookup"><span data-stu-id="53efa-137">Navigate to the resource group</span></span>
<span data-ttu-id="53efa-138">그곳에서 사용자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-138">Add the user there.</span></span>

![응용 프로그램의 리소스 블레이드에서 필수 항목을 열고, 리소스 그룹을 열고, 설정/사용자를 선택합니다.](./media/app-insights-resources-roles-access-control/01-add-user.png)

<span data-ttu-id="53efa-141">또는 한 수준 더 올라가서 사용자를 구독에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-141">Or you could go up another level and add the user to the Subscription.</span></span>

#### <a name="select-a-role"></a><span data-ttu-id="53efa-142">역할 선택</span><span class="sxs-lookup"><span data-stu-id="53efa-142">Select a role</span></span>
![새 사용자에 대한 역할을 선택합니다.](./media/app-insights-resources-roles-access-control/03-role.png)

| <span data-ttu-id="53efa-144">역할</span><span class="sxs-lookup"><span data-stu-id="53efa-144">Role</span></span> | <span data-ttu-id="53efa-145">리소스 그룹에서 할 수 있는 일</span><span class="sxs-lookup"><span data-stu-id="53efa-145">In the resource group</span></span> |
| --- | --- |
| <span data-ttu-id="53efa-146">소유자</span><span class="sxs-lookup"><span data-stu-id="53efa-146">Owner</span></span> |<span data-ttu-id="53efa-147">사용자 액세스를 포함하여 모든 것을 변경할 수 있음</span><span class="sxs-lookup"><span data-stu-id="53efa-147">Can change anything, including user access</span></span> |
| <span data-ttu-id="53efa-148">참여자</span><span class="sxs-lookup"><span data-stu-id="53efa-148">Contributor</span></span> |<span data-ttu-id="53efa-149">모든 리소스를 포함하여 모든 것을 편집할 수 있음</span><span class="sxs-lookup"><span data-stu-id="53efa-149">Can edit anything, including all resources</span></span> |
| <span data-ttu-id="53efa-150">Application Insights 구성 요소 참여자</span><span class="sxs-lookup"><span data-stu-id="53efa-150">Application Insights Component contributor</span></span> |<span data-ttu-id="53efa-151">Application Insights 리소스, 웹 테스트 및 경고를 편집할 수 있음</span><span class="sxs-lookup"><span data-stu-id="53efa-151">Can edit Application Insights resources, web tests and alerts</span></span> |
| <span data-ttu-id="53efa-152">판독기</span><span class="sxs-lookup"><span data-stu-id="53efa-152">Reader</span></span> |<span data-ttu-id="53efa-153">모든 것을 볼 수 있지만 변경할 수는 없음</span><span class="sxs-lookup"><span data-stu-id="53efa-153">Can view but not change anything</span></span> |

<span data-ttu-id="53efa-154">'편집'에는 다음 항목을 만들고, 삭제하고, 업데이트하는 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-154">'Editing' includes creating, deleting and updating:</span></span>

* <span data-ttu-id="53efa-155">리소스</span><span class="sxs-lookup"><span data-stu-id="53efa-155">Resources</span></span>
* <span data-ttu-id="53efa-156">웹 테스트</span><span class="sxs-lookup"><span data-stu-id="53efa-156">Web tests</span></span>
* <span data-ttu-id="53efa-157">경고</span><span class="sxs-lookup"><span data-stu-id="53efa-157">Alerts</span></span>
* <span data-ttu-id="53efa-158">연속 내보내기</span><span class="sxs-lookup"><span data-stu-id="53efa-158">Continuous export</span></span>

#### <a name="select-the-user"></a><span data-ttu-id="53efa-159">사용자 선택</span><span class="sxs-lookup"><span data-stu-id="53efa-159">Select the user</span></span>

<span data-ttu-id="53efa-160">원하는 사용자가 디렉터리에 없는 경우 Microsoft 계정이 있는 사람을 초대할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-160">If the user you want isn't in the directory, you can invite anyone with a Microsoft account.</span></span>
<span data-ttu-id="53efa-161">Outlook.com, OneDrive, Windows Phone 또는 XBox Live를 사용하는 사람은 Microsoft 계정을 갖고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53efa-161">(If they use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, they have a Microsoft account.)</span></span>

## <a name="related-content"></a><span data-ttu-id="53efa-162">관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="53efa-162">Related content</span></span>

* [<span data-ttu-id="53efa-163">Azure의 역할 기반 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="53efa-163">Role based access control in Azure</span></span>](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md
