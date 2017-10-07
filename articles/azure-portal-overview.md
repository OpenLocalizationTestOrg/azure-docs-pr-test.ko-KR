---
title: "aaaAzure 포털 개요 | Microsoft Docs"
description: "Toouse Microsoft Azure 포털을 hello 하는 방법에 대해 알아봅니다."
services: 
documentationcenter: 
author: davidwrede
manager: erikre
editor: jimbe
ms.assetid: 53cb9df1-c96a-4f4e-b022-18336cd3d697
ms.service: na
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/16/2015
ms.author: dwrede
ms.openlocfilehash: feca8b5e26e9cb373c5e8e688173d5856050bb28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-portal-overview"></a><span data-ttu-id="ebc30-103">Microsoft Azure 포털 개요</span><span class="sxs-lookup"><span data-stu-id="ebc30-103">Microsoft Azure portal overview</span></span>
<span data-ttu-id="ebc30-104">hello Microsoft Azure 포털은 프로 비전 하 고 Azure 리소스를 관리할 수 있는 중앙 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-104">hello Microsoft Azure portal is a central place where you can provision and manage your Azure resources.</span></span>  <span data-ttu-id="ebc30-105">이 자습서는 hello 포털에 설명 하 고 방법을 보여 줍니다 toouse 이러한 중요 한 기능:</span><span class="sxs-lookup"><span data-stu-id="ebc30-105">This tutorial will familiarize you with hello portal and show you how toouse some of these key capabilities:</span></span>

* <span data-ttu-id="ebc30-106">**포괄적인 마켓플레이스** 를 사용하여 구입하거나 프로비전할 수 있는 Microsoft 및 다른 공급 업체의 수천 개의 항목을 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-106">A **comprehensive marketplace** that lets you browse through thousands of items from Microsoft and other vendors that can be purchased and/or provisioned.</span></span>
* <span data-ttu-id="ebc30-107">A **통합 되 고 확장 가능 브라우저 환경** 쉽게 toofind hello 리소스에 대 한 중요 하 고 다양 한 관리 작업을 수행 하면입니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-107">A **unified and scalable browse experience** that makes it easy toofind hello resources you care about and perform various management operations.</span></span>
* <span data-ttu-id="ebc30-108">**일관적인 관리 페이지** (또는 블레이드)를 사용하면 노출 설정, 작업, 대금 청구 정보, 상태 모니터링 및 사용 현황 데이터 등 일관된 방식으로 Azure의 다양한 서비스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-108">**Consistent management pages** (or blades) that let you manage Azure’s wide variety of services through a consistent way of exposing settings, actions, billing information, health monitoring and usage data, and much more.</span></span>
* <span data-ttu-id="ebc30-109">A **개인 경험** 표시 hello에 로그인 할 때마다 toosee 표시할 정보를 사용자 지정 된 시작 화면을 만들 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-109">A **personal experience** that lets you create a customized start screen that shows hello information that you want toosee whenever you log in.</span></span>  <span data-ttu-id="ebc30-110">또한 타일을 포함 하는 hello 관리 블레이드 중 하나를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-110">You can also customize any of hello management blades that contain tiles.</span></span>
  
  ![Azure 포털 UI 개요][UIOrientation]

## <a name="before-you-get-started"></a><span data-ttu-id="ebc30-112">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="ebc30-112">Before you get started</span></span>
<span data-ttu-id="ebc30-113">이 자습서를 통해 유효한 Azure 구독이 toogo가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-113">You will need a valid Azure subscription toogo through this tutorial.</span></span>  <span data-ttu-id="ebc30-114">없는 경우 지금 [무료 평가판에 등록](https://azure.microsoft.com/pricing/free-trial/) 하세요.</span><span class="sxs-lookup"><span data-stu-id="ebc30-114">If you don’t have one, then [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/) today.</span></span>  <span data-ttu-id="ebc30-115">구독을 보유 hello 포털에 액세스할 수 있습니다 <https://portal.azure.com>합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-115">Once you have a subscription, you can access hello portal at <https://portal.azure.com>.</span></span>

## <a name="how-toocreate-a-resource"></a><span data-ttu-id="ebc30-116">어떻게 toocreate 리소스</span><span class="sxs-lookup"><span data-stu-id="ebc30-116">How toocreate a resource</span></span>
<span data-ttu-id="ebc30-117">Azure에는 수천 개의 항목을 한 곳에서 만들 수 있는 마켓플레이스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-117">Azure has a marketplace with thousands of items that you can create from one place.</span></span>  <span data-ttu-id="ebc30-118">새 Windows Server 2012 VM toocreate를 원하는 경우를 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-118">Let’s say you want toocreate a new Windows Server 2012 VM.</span></span>  <span data-ttu-id="ebc30-119">안녕하세요 + 새 허브는 큐 레이트 hello 시장에서 주요 범주 집합으로 프로그램 진입점입니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-119">hello +NEW hub is your entry point into a curated set of featured categories from hello marketplace.</span></span>  <span data-ttu-id="ebc30-120">각 범주에는 모든 범주 및 검색을 보여 주는 링크 toohello 전체 마켓플레이스와 함께 작은 추천된 항목 집합을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-120">Each category has a small set of featured items along with a link toohello full marketplace that shows all categories and search.</span></span> <span data-ttu-id="ebc30-121">toocreate 새 Windows Server 2012 VM hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-121">toocreate that new Windows Server 2012 VM, perform hello following actions:</span></span>  

1. <span data-ttu-id="ebc30-122">Windows Server 2012이 추천 목록 hello 계산 범주에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-122">Windows Server 2012 is featured, so you can select it from hello Compute category.</span></span>  
2. <span data-ttu-id="ebc30-123">양식에서 몇 가지 기본 입력 항목을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-123">Fill out some basic inputs on a form.</span></span>
3. <span data-ttu-id="ebc30-124">'만들기'를 클릭 하 고 VM tooprovision를 즉시 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-124">Click ‘Create’ and your VM will begin tooprovision immediately.</span></span>

<span data-ttu-id="ebc30-125">알림 허브 경우 알려 리소스를 만들고 관리 블레이드가 열리고 hello (항상 검색할 수 있습니다 tooresources 나중에).</span><span class="sxs-lookup"><span data-stu-id="ebc30-125">hello notifications hub will alert you when your resource has been created and a management blade will open (you can always browse tooresources later).</span></span>

![포털 범주][PortalCategories]

## <a name="how-toofind-your-resources"></a><span data-ttu-id="ebc30-127">어떻게 toofind 리소스</span><span class="sxs-lookup"><span data-stu-id="ebc30-127">How toofind your resources</span></span>
<span data-ttu-id="ebc30-128">자주 액세스 한 리소스 tooyour 시작 보드 항상 고정할 수 있습니다 하지만 자주 액세스 하지 않는 toobrowse toosomething 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-128">You can always pin frequently accessed resources tooyour startboard, but you might need toobrowse toosomething that you don’t frequently access.</span></span>  <span data-ttu-id="ebc30-129">아래 표시 된 hello 찾아보기 허브 리소스를 프로그램 방식으로 tooget tooall입니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-129">hello browse hub shown below is your way tooget tooall of your resources.</span></span>  <span data-ttu-id="ebc30-130">구독에 의해 필터링, 열을 선택/조정 고 이동할 수 toohello 관리 블레이드 개별 항목을 클릭 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-130">You can filter by subscription, choose/resize columns, and navigate toohello management blades by clicking on individual items.</span></span>

![찾아보기 허브][BrowseHub]

## <a name="how-toomanage-and-delegate-access-tooa-resource"></a><span data-ttu-id="ebc30-132">Toomanage 및 대리자 tooa 리소스에 액세스 방법</span><span class="sxs-lookup"><span data-stu-id="ebc30-132">How toomanage and delegate access tooa resource</span></span>
<span data-ttu-id="ebc30-133">이 블레이드에서 있습니다 수 toohello 가상 컴퓨터를 원격 데스크톱을 사용 하 여 연결, 주요 성능 메트릭을 모니터링할 제어 액세스 toothis VM 역할 기반 액세스 (RBAC)를 사용 하 여 hello VM을 구성 하 고 다른 중요 한 관리 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-133">From this blade you can connect toohello virtual machine using remote desktop, monitor key performance metrics, control access toothis VM using role based access (RBAC), configure hello VM, and perform other important management tasks.</span></span>  <span data-ttu-id="ebc30-134">역할 기반 액세스를 위임 규모에 중요 한 toomanaging 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-134">Delegating access based on role is critical toomanaging at scale.</span></span>  <span data-ttu-id="ebc30-135">클릭 [여기](active-directory/role-based-access-control-configure.md) toolearn 항목에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-135">Click [here](active-directory/role-based-access-control-configure.md) toolearn more about it.</span></span> <span data-ttu-id="ebc30-136">toodelegate tooa 리소스에 액세스 hello 다음 작업을 수행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ebc30-136">toodelegate access tooa resource, perform hello following actions:</span></span>

1. <span data-ttu-id="ebc30-137">Tooyour 리소스를 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-137">Browse tooyour resource.</span></span>
2. <span data-ttu-id="ebc30-138">Hello Essentials 섹션에서 ' 모든 설정을'를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-138">Click ‘All settings’ in hello Essentials section.</span></span>
3. <span data-ttu-id="ebc30-139">Hello 설정 목록에서 '사용자'를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-139">Click ‘Users’ in hello settings list.</span></span>
4. <span data-ttu-id="ebc30-140">Hello 명령 모음에서 [추가]를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-140">Click ‘Add’ in hello command bar.</span></span>
5. <span data-ttu-id="ebc30-141">사용자 및 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-141">Choose a user and a role.</span></span>

![리소스 관리][ManageResource]

## <a name="how-tooget-help"></a><span data-ttu-id="ebc30-143">Tooget 도움말 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ebc30-143">How tooget help</span></span>
<span data-ttu-id="ebc30-144">문제가 발생한 경우 걱정하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-144">If you ever have a problem, we’re here for you.</span></span>  <span data-ttu-id="ebc30-145">hello 포털 hello 올바른 방향으로 가리킬 수 있는 도움말 및 지원 페이지를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-145">hello portal has a help and support page that can point you in hello right direction.</span></span>  <span data-ttu-id="ebc30-146">에 따라 프로그램 [지원 플랜](https://azure.microsoft.com/support/plans/), hello 포털에서 직접 지원 티켓을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-146">Depending on your [support plan](https://azure.microsoft.com/support/plans/), you can also create support tickets directly in hello portal.</span></span>  <span data-ttu-id="ebc30-147">지원 티켓을 만든 후 hello 포털 내에서 hello 티켓의 hello 수명 주기를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-147">After creating a support ticket, you can manage hello lifecycle of hello ticket from within hello portal.</span></span> <span data-ttu-id="ebc30-148">Toohello 도움말을 볼 수 있습니다 및 tooBrowse 이동 하 여 지원 페이지 도움말 + 지원-> 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-148">You can get toohello help and support page by navigating tooBrowse -> Help + support.</span></span>  

![도움말 및 지원][HelpSupport]

## <a name="summary"></a><span data-ttu-id="ebc30-150">요약</span><span class="sxs-lookup"><span data-stu-id="ebc30-150">Summary</span></span>
<span data-ttu-id="ebc30-151">이 자습서에서 배운 내용을 검토하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-151">Let’s review what you learned in this tutorial:</span></span>

* <span data-ttu-id="ebc30-152">방법, toosign 한 구독 및 toohello 포털을 찾아볼 학습</span><span class="sxs-lookup"><span data-stu-id="ebc30-152">You learned how toosign up, get a subscription, and browse toohello portal</span></span>
* <span data-ttu-id="ebc30-153">Hello 포털 UI 방향 및 방법에 대해 배웠습니다 있습니다 toocreate 및 찾아보기 리소스</span><span class="sxs-lookup"><span data-stu-id="ebc30-153">You got oriented with hello portal UI and learned how toocreate and browse resources</span></span>
* <span data-ttu-id="ebc30-154">방법에 대해 배웠습니다 toocreate 리소스 및 리소스 찾아보기</span><span class="sxs-lookup"><span data-stu-id="ebc30-154">You learned how toocreate a resource and browse resources</span></span>
* <span data-ttu-id="ebc30-155">Hello 구조 또는 관리 블레이드 및 여러 유형의 리소스 일관 되 게 관리 하는 방법을 배운</span><span class="sxs-lookup"><span data-stu-id="ebc30-155">You learned about hello structure or management blades and how you can consistently manage different types of resources</span></span>
* <span data-ttu-id="ebc30-156">Toocustomize 포털 toobring hello 하는 방법을 알아보았습니다 hello toohello 중심적 역할에 대 한 중요 정보</span><span class="sxs-lookup"><span data-stu-id="ebc30-156">You learned how toocustomize hello portal toobring hello information you care about toohello front and center</span></span>
* <span data-ttu-id="ebc30-157">역할을 사용 하 여 toocontrol 액세스 tooresources 기반 (RBAC) 액세스 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-157">You learned how toocontrol access tooresources using role based access (RBAC)</span></span>
* <span data-ttu-id="ebc30-158">Tooget 도움말 및 지원 방법을 학습</span><span class="sxs-lookup"><span data-stu-id="ebc30-158">You learned how tooget help and support</span></span>

<span data-ttu-id="ebc30-159">hello Microsoft Azure 포털은 근본적으로 개발 하 고 hello 클라우드에서 응용 프로그램 관리를 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-159">hello Microsoft Azure portal radically simplifies building and managing your applications in hello cloud.</span></span>  <span data-ttu-id="ebc30-160">Hello 살펴보기 [관리 블로그](https://azure.microsoft.com/blog/topics/management/) tookeep toodate 지속적으로 하는 대로 [수신 toofeedback](https://feedback.azure.com/forums/223579-azure-preview-portal/) 개선 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-160">Take a look at hello [management blog](https://azure.microsoft.com/blog/topics/management/) tookeep up toodate as we’re constantly [listening toofeedback](https://feedback.azure.com/forums/223579-azure-preview-portal/) and making improvements.</span></span>  <span data-ttu-id="ebc30-161">[ScottGu의 블로그](http://weblogs.asp.net/scottgu) 모든 Azure 업데이트에 대 한 또 다른 좋은 곳 toolook 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebc30-161">[ScottGu’s blog](http://weblogs.asp.net/scottgu) is another great place toolook for all Azure updates.</span></span>

[UIOrientation]: ./media/azure-portal-how-to-use/azure_portal_1.png
[PortalCategories]: ./media/azure-portal-how-to-use/azure_portal_2.png
[BrowseHub]: ./media/azure-portal-how-to-use/azure_portal_3.png
[ManageResource]: ./media/azure-portal-how-to-use/azure_portal_4.png
[CustomizeBlades]: ./media/azure-portal-how-to-use/azure_portal_5.png
[HelpSupport]: ./media/azure-portal-how-to-use/azure_portal_6.png
