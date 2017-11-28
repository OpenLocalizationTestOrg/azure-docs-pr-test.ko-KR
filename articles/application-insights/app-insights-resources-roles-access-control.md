---
title: "Azure Application Insights에서 aaaResources, 역할 및 액세스 제어 | Microsoft Docs"
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
ms.openlocfilehash: a6f6ca0443b5f60239f094606e124f856967d8ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a><span data-ttu-id="72d5d-103">Application Insights에서 리소스, 역할 및 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="72d5d-103">Resources, roles, and access control in Application Insights</span></span>
<span data-ttu-id="72d5d-104">사용자에 대 한 읽기 및 Azure에서 액세스 tooyour 데이터 업데이트를 제어할 수 있습니다 [Application Insights][start]를 사용 하 여 [Microsoft Azure에서 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-104">You can control who has read and update access tooyour data in Azure [Application Insights][start], by using [Role-based access control in Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="72d5d-105">Hello에 대 한 액세스 toousers 할당 **리소스 그룹이 나 구독** toowhich hello 리소스 자체에 없는 응용 프로그램 리소스-속합니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-105">Assign access toousers in hello **resource group or subscription** toowhich your application resource belongs - not in hello resource itself.</span></span> <span data-ttu-id="72d5d-106">Hello 할당 **Application Insights 구성 요소 기여자** 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-106">Assign hello **Application Insights component contributor** role.</span></span> <span data-ttu-id="72d5d-107">이렇게 하면 액세스 tooweb 테스트 및 응용 프로그램 리소스와 함께 경고의 균일 한 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-107">This ensures uniform control of access tooweb tests and alerts along with your application resource.</span></span> <span data-ttu-id="72d5d-108">[자세히 알아봅니다](#access).</span><span class="sxs-lookup"><span data-stu-id="72d5d-108">[Learn more](#access).</span></span>
> 
> 

## <a name="resources-groups-and-subscriptions"></a><span data-ttu-id="72d5d-109">리소스, 그룹 및 구독</span><span class="sxs-lookup"><span data-stu-id="72d5d-109">Resources, groups and subscriptions</span></span>
<span data-ttu-id="72d5d-110">먼저 몇 가지를 정의하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-110">First, some definitions:</span></span>

* <span data-ttu-id="72d5d-111">**리소스** - Microsoft Azure 서비스의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-111">**Resource** - An instance of a Microsoft Azure service.</span></span> <span data-ttu-id="72d5d-112">Application Insights 리소스를 수집 하 고 분석 하 고 응용 프로그램에서 보낸 hello 원격 분석 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-112">Your Application Insights resource collects, analyzes and displays hello telemetry data sent from your application.</span></span>  <span data-ttu-id="72d5d-113">다른 유형의 Azure 리소스로는 웹 앱, 데이터베이스 및 VM이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-113">Other types of Azure resources include web apps, databases, and VMs.</span></span>
  
    <span data-ttu-id="72d5d-114">에서는 리소스를 열고 toosee hello [Azure 포털][portal], 로그인 한 모든 리소스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-114">toosee your resources, open hello [Azure Portal][portal], sign in, and click All Resources.</span></span> <span data-ttu-id="72d5d-115">toofind 리소스에 hello 필터 필드에 해당 이름의 형식 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-115">toofind a resource, type part of its name in hello filter field.</span></span>
  
    ![Azure 리소스 목록](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* <span data-ttu-id="72d5d-117">[**리소스 그룹** ] [ group] -모든 리소스가 속해 tooone 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-117">[**Resource group**][group] - Every resource belongs tooone group.</span></span> <span data-ttu-id="72d5d-118">그룹은 편리한 방법은 toomanage 관련 데 특정 하 게 액세스 제어의 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-118">A group is a convenient way toomanage related resources, particularly for access control.</span></span> <span data-ttu-id="72d5d-119">예를 들어 웹 응용 프로그램, Application Insights 리소스 toomonitor hello 앱 및 저장소 리소스 tookeep 빠뜨릴 수 그룹 하나의 리소스에 데이터를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-119">For example, into one resource group you could put a Web App, an Application Insights resource toomonitor hello app, and a Storage resource tookeep exported data.</span></span>

    ![찾아보기, 리소스 그룹을 차례로 선택한 다음 그룹을 선택합니다.](./media/app-insights-resources-roles-access-control/11-group.png)

* <span data-ttu-id="72d5d-121">[**구독** ](https://manage.windowsazure.com) -tooan Azure 구독에에서 로그인 할 toouse Application Insights 또는 기타 Azure 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-121">[**Subscription**](https://manage.windowsazure.com) - toouse Application Insights or other Azure resources, you sign in tooan Azure subscription.</span></span> <span data-ttu-id="72d5d-122">모든 리소스 그룹이 속한 tooone Azure 구독을 여기서 있습니다 가격 패키지를 선택 하 고는 조직이 구독 하는 경우 hello 멤버 및 해당 액세스 권한을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-122">Every resource group belongs tooone Azure subscription, where you choose your price package and, if it's an organization subscription, choose hello members and their access permissions.</span></span>
* <span data-ttu-id="72d5d-123">[**Microsoft 계정** ] [ account] -사용자 이름 및 암호 toosign 사용 하 여 tooMicrosoft Azure의에서 hello 구독, XBox Live, Outlook.com 및 다른 Microsoft 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-123">[**Microsoft account**][account] - hello username and password that you use toosign in tooMicrosoft Azure subscriptions, XBox Live, Outlook.com, and other Microsoft services.</span></span>

## <span data-ttu-id="72d5d-124"><a name="access"></a>Hello 리소스 그룹에 대 한 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="72d5d-124"><a name="access"></a> Control access in hello resource group</span></span>
<span data-ttu-id="72d5d-125">것이 중요 한 toounderstand 더하기 toohello 리소스 응용 프로그램에 대해 만든에서 개가 또한 경고 및 웹 테스트에 대 한 숨겨진된 리소스를 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-125">It's important toounderstand that in addition toohello resource you created for your application, there are also separate hidden resources for alerts and web tests.</span></span> <span data-ttu-id="72d5d-126">연결 된 toohello는 동일한 [리소스 그룹](#resource-group) 응용 프로그램으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-126">They are attached toohello same [resource group](#resource-group) as your application.</span></span> <span data-ttu-id="72d5d-127">웹 사이트 또는 저장소 같은 다른 Azure 서비스를 여기에 넣었을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-127">You might also have put other Azure services in there, such as websites or storage.</span></span>

![Application Insights의 리소스](./media/app-insights-resources-roles-access-control/00-resources.png)

<span data-ttu-id="72d5d-129">toocontrol toothese 리소스에 액세스 하는 것은 좋습니다 따라서:</span><span class="sxs-lookup"><span data-stu-id="72d5d-129">toocontrol access toothese resources it's therefore recommended to:</span></span>

* <span data-ttu-id="72d5d-130">Hello에 대 한 액세스 제어 **리소스 그룹이 나 구독** 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-130">Control access at hello **resource group or subscription** level.</span></span>
* <span data-ttu-id="72d5d-131">Hello 할당 **응용 프로그램 Insights 구성 요소 기여자** 역할 toousers 합니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-131">Assign hello **Application Insights Component contributor** role toousers.</span></span> <span data-ttu-id="72d5d-132">이렇게 하면 tooedit 웹 테스트, 경고 및 Application Insights 리소스 액세스 tooany hello 그룹의 다른 서비스를 제공 하지 않고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-132">This allows them tooedit web tests, alerts, and Application Insights resources, without providing access tooany other services in hello group.</span></span>

## <a name="tooprovide-access-tooanother-user"></a><span data-ttu-id="72d5d-133">tooprovide 액세스 tooanother 사용자</span><span class="sxs-lookup"><span data-stu-id="72d5d-133">tooprovide access tooanother user</span></span>
<span data-ttu-id="72d5d-134">소유자 권한 toohello 구독 또는 hello 리소스 그룹이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-134">You must have Owner rights toohello subscription or hello resource group.</span></span>

<span data-ttu-id="72d5d-135">hello 사용자에 게 있어야는 [Microsoft 계정][account], tootheir 액세스 또는 [조직 Microsoft 계정](../active-directory/sign-up-organization.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-135">hello user must have a [Microsoft Account][account], or access tootheir [organizational Microsoft Account](../active-directory/sign-up-organization.md).</span></span> <span data-ttu-id="72d5d-136">액세스 tooindividuals 및 Azure Active Directory에 정의 된 toouser 그룹을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-136">You can provide access tooindividuals, and also toouser groups defined in Azure Active Directory.</span></span>

#### <a name="navigate-toohello-resource-group"></a><span data-ttu-id="72d5d-137">Toohello 리소스 그룹 이동</span><span class="sxs-lookup"><span data-stu-id="72d5d-137">Navigate toohello resource group</span></span>
<span data-ttu-id="72d5d-138">Hello 사용자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-138">Add hello user there.</span></span>

![응용 프로그램의 리소스 블레이드에서 Essentials를 열고 hello 리소스 그룹을 열고 있습니다 설정/사용자를 선택 합니다.](./media/app-insights-resources-roles-access-control/01-add-user.png)

<span data-ttu-id="72d5d-141">또는 폴더을 hello 사용자 toohello 구독을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-141">Or you could go up another level and add hello user toohello Subscription.</span></span>

#### <a name="select-a-role"></a><span data-ttu-id="72d5d-142">역할 선택</span><span class="sxs-lookup"><span data-stu-id="72d5d-142">Select a role</span></span>
![Hello 새 사용자에 대 한 역할을 선택 합니다.](./media/app-insights-resources-roles-access-control/03-role.png)

| <span data-ttu-id="72d5d-144">역할</span><span class="sxs-lookup"><span data-stu-id="72d5d-144">Role</span></span> | <span data-ttu-id="72d5d-145">Hello 리소스 그룹에서</span><span class="sxs-lookup"><span data-stu-id="72d5d-145">In hello resource group</span></span> |
| --- | --- |
| <span data-ttu-id="72d5d-146">소유자</span><span class="sxs-lookup"><span data-stu-id="72d5d-146">Owner</span></span> |<span data-ttu-id="72d5d-147">사용자 액세스를 포함하여 모든 것을 변경할 수 있음</span><span class="sxs-lookup"><span data-stu-id="72d5d-147">Can change anything, including user access</span></span> |
| <span data-ttu-id="72d5d-148">참여자</span><span class="sxs-lookup"><span data-stu-id="72d5d-148">Contributor</span></span> |<span data-ttu-id="72d5d-149">모든 리소스를 포함하여 모든 것을 편집할 수 있음</span><span class="sxs-lookup"><span data-stu-id="72d5d-149">Can edit anything, including all resources</span></span> |
| <span data-ttu-id="72d5d-150">Application Insights 구성 요소 참여자</span><span class="sxs-lookup"><span data-stu-id="72d5d-150">Application Insights Component contributor</span></span> |<span data-ttu-id="72d5d-151">Application Insights 리소스, 웹 테스트 및 경고를 편집할 수 있음</span><span class="sxs-lookup"><span data-stu-id="72d5d-151">Can edit Application Insights resources, web tests and alerts</span></span> |
| <span data-ttu-id="72d5d-152">판독기</span><span class="sxs-lookup"><span data-stu-id="72d5d-152">Reader</span></span> |<span data-ttu-id="72d5d-153">모든 것을 볼 수 있지만 변경할 수는 없음</span><span class="sxs-lookup"><span data-stu-id="72d5d-153">Can view but not change anything</span></span> |

<span data-ttu-id="72d5d-154">'편집'에는 다음 항목을 만들고, 삭제하고, 업데이트하는 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-154">'Editing' includes creating, deleting and updating:</span></span>

* <span data-ttu-id="72d5d-155">리소스</span><span class="sxs-lookup"><span data-stu-id="72d5d-155">Resources</span></span>
* <span data-ttu-id="72d5d-156">웹 테스트</span><span class="sxs-lookup"><span data-stu-id="72d5d-156">Web tests</span></span>
* <span data-ttu-id="72d5d-157">경고</span><span class="sxs-lookup"><span data-stu-id="72d5d-157">Alerts</span></span>
* <span data-ttu-id="72d5d-158">연속 내보내기</span><span class="sxs-lookup"><span data-stu-id="72d5d-158">Continuous export</span></span>

#### <a name="select-hello-user"></a><span data-ttu-id="72d5d-159">Hello 사용자 선택</span><span class="sxs-lookup"><span data-stu-id="72d5d-159">Select hello user</span></span>

<span data-ttu-id="72d5d-160">원하는 hello 사용자를 hello 디렉터리에 없는 경우 Microsoft 계정으로 모든 사용자를 초대할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-160">If hello user you want isn't in hello directory, you can invite anyone with a Microsoft account.</span></span>
<span data-ttu-id="72d5d-161">Outlook.com, OneDrive, Windows Phone 또는 XBox Live를 사용하는 사람은 Microsoft 계정을 갖고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72d5d-161">(If they use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, they have a Microsoft account.)</span></span>

## <a name="related-content"></a><span data-ttu-id="72d5d-162">관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="72d5d-162">Related content</span></span>

* [<span data-ttu-id="72d5d-163">Azure의 역할 기반 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="72d5d-163">Role based access control in Azure</span></span>](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md
