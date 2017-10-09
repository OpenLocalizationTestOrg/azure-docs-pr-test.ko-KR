---
title: "Azure 트래픽 관리자 프로필 aaaManage | Microsoft Docs"
description: "이 문서는 Azure Traffic Manager 프로필을 만들고, 사용하거나 사용하지 않도록 설정하며, 삭제하는 데 도움이 됩니다."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: f06e0365-0a20-4d08-b7e1-e56025e64f66
ms.service: traffic-manager
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: kumud
ms.openlocfilehash: 0c6ab0c451581d039514a9de0b525b3937e45a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-traffic-manager-profile"></a><span data-ttu-id="bff5c-103">Azure 트래픽 관리자 프로필 관리</span><span class="sxs-lookup"><span data-stu-id="bff5c-103">Manage an Azure Traffic Manager profile</span></span>

<span data-ttu-id="bff5c-104">트래픽 관리자 프로필 트래픽 tooyour 클라우드 서비스 또는 웹 사이트 끝점의 메서드 toocontrol hello 배포 트래픽 라우팅을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-104">Traffic Manager profiles use traffic-routing methods toocontrol hello distribution of traffic tooyour cloud services or website endpoints.</span></span> <span data-ttu-id="bff5c-105">이 문서에서는 설명 방법을 toocreate 하 고 이러한 프로필을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-105">This article explains how toocreate and manage these profiles.</span></span>

## <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="bff5c-106">Traffic Manager 프로필 만들기</span><span class="sxs-lookup"><span data-stu-id="bff5c-106">Create a Traffic Manager profile</span></span>

<span data-ttu-id="bff5c-107">Hello Azure 포털을 사용 하 여 트래픽 관리자 프로필을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-107">You can create a Traffic Manager profile by using hello Azure portal.</span></span> <span data-ttu-id="bff5c-108">프로필을 만든 후 끝점, 모니터링 및 기타 설정을 hello Azure 포털에서에서 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-108">After creating your profile, you can configure endpoints, monitoring, and other settings in hello Azure portal.</span></span> <span data-ttu-id="bff5c-109">트래픽 관리자 프로필 별로 too200 끝점을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-109">Traffic Manager supports up too200 endpoints per profile.</span></span> <span data-ttu-id="bff5c-110">하지만 대부분의 사용 시나리오에는 적은 수의 끝점만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-110">However, most usage scenarios require only a few of endpoints.</span></span>

### <a name="toocreate-a-traffic-manager-profile"></a><span data-ttu-id="bff5c-111">toocreate 트래픽 관리자 프로필</span><span class="sxs-lookup"><span data-stu-id="bff5c-111">toocreate a Traffic Manager profile</span></span>

1. <span data-ttu-id="bff5c-112">Toohello 브라우저에서 로그인 [Azure 포털](http://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-112">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="bff5c-113">아직 계정이 없는 경우 [1개월 무료 평가판](https://azure.microsoft.com/free/)을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-113">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="bff5c-114">Hello에 **허브** 메뉴를 클릭 **새로** > **네트워킹** > **스크롤하게**, 클릭 **트래픽 관리자** 프로필 tooopen hello **만들 트래픽 관리자 프로필** 블레이드에서 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-114">On hello **Hub** menu, click **New** > **Networking** > **See all**, click **Traffic Manager** profile tooopen hello **Create Traffic Manager profile** blade, then click **Create**.</span></span>
3. <span data-ttu-id="bff5c-115">Hello에 **만들 트래픽 관리자 프로필** 블레이드를 다음과 같이 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-115">On hello **Create Traffic Manager profile** blade, complete as follows:</span></span>
    1. <span data-ttu-id="bff5c-116">**이름**에서 사용자의 프로필에 사용할 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-116">In **Name**, provide a name for your profile.</span></span> <span data-ttu-id="bff5c-117">이 이름은 toobe hello trafficmanager.net 영역 내에서 고유 해야 하며 hello DNS 이름으로 인해 <name>를 사용 하는 tooaccess trafficmanager.net 트래픽 관리자 프로필.</span><span class="sxs-lookup"><span data-stu-id="bff5c-117">This name needs toobe unique within hello trafficmanager.net zone and results in hello DNS name <name>, trafficmanager.net, that is used tooaccess your Traffic Manager profile.</span></span>
    2. <span data-ttu-id="bff5c-118">**라우팅 메서드**선택, hello **우선 순위** 라우팅 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-118">In **Routing method**, select hello **Priority** routing method.</span></span>
    3. <span data-ttu-id="bff5c-119">**구독**, toocreate 아래에서이 프로필을 원하는 hello 구독 선택</span><span class="sxs-lookup"><span data-stu-id="bff5c-119">In **Subscription**, select hello subscription you want toocreate this profile under</span></span>
    4. <span data-ttu-id="bff5c-120">**리소스 그룹**, 새 리소스 그룹 tooplace 아래에서이 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-120">In **Resource Group**, create a new resource group tooplace this profile under.</span></span>
    5. <span data-ttu-id="bff5c-121">**리소스 그룹 위치**, hello 리소스 그룹의 hello 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-121">In **Resource group location**, select hello location of hello resource group.</span></span> <span data-ttu-id="bff5c-122">이 설정은 hello 리소스 그룹의 toohello 위치를 나타내며 hello 전체적으로 배포 될 트래픽 관리자 프로필에 어떠한 영향도 미치지.</span><span class="sxs-lookup"><span data-stu-id="bff5c-122">This setting refers toohello location of hello resource group, and has no impact on hello Traffic Manager profile that will be deployed globally.</span></span>
    6. <span data-ttu-id="bff5c-123">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-123">Click **Create**.</span></span>
    7. <span data-ttu-id="bff5c-124">트래픽 관리자 프로필의 hello 전역 배포 완료 되 면 hello 리소스 중 하나로 각 리소스 그룹에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-124">When hello global deployment of your Traffic Manager profile is complete, it is listed in respective resource group as one of hello resources.</span></span>

## <a name="disable-enable-or-delete-a-profile"></a><span data-ttu-id="bff5c-125">프로필 사용 안 함, 사용 또는 삭제</span><span class="sxs-lookup"><span data-stu-id="bff5c-125">Disable, enable, or delete a profile</span></span>

<span data-ttu-id="bff5c-126">트래픽 관리자는 사용자 요청 toohello 구성 된 끝점을 참조 하지 않는 하므로 기존 프로필을 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-126">You can disable an existing profile so that Traffic Manager does not refer user requests toohello configured endpoints.</span></span> <span data-ttu-id="bff5c-127">트래픽 관리자 프로필을 사용 하지 않으면 hello 프로필 및 hello 프로필에 포함 된 hello 정보 그대로 유지 하 고 hello 트래픽 관리자 인터페이스에서 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-127">When you disable a Traffic Manager profile, hello profile and hello information contained in hello profile remain intact and can be edited in hello Traffic Manager interface.</span></span>  <span data-ttu-id="bff5c-128">Hello 프로필을 다시 설정 하는 조회 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-128">Referrals resume when you re-enable hello profile.</span></span> <span data-ttu-id="bff5c-129">Hello Azure 포털에서에서 트래픽 관리자 프로필을 만들 때 자동으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-129">When you create a Traffic Manager profile in hello Azure portal, it's automatically enabled.</span></span> <span data-ttu-id="bff5c-130">프로필이 더 이상 필요하지 않으면 해당 프로필을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-130">If you decide a profile is no longer necessary, you can delete it.</span></span>

### <a name="toodisable-a-profile"></a><span data-ttu-id="bff5c-131">toodisable 프로필</span><span class="sxs-lookup"><span data-stu-id="bff5c-131">toodisable a profile</span></span>

1. <span data-ttu-id="bff5c-132">사용자 지정 도메인을 사용 하는 경우 인터넷 DNS 서버의 hello CNAME 레코드를 더 이상 tooyour 트래픽 관리자 프로필을 가리키도록 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-132">If you are using a custom domain name, change hello CNAME record on your Internet DNS server so that it no longer points tooyour Traffic Manager profile.</span></span>
2. <span data-ttu-id="bff5c-133">트래픽 중지 되 고 hello 트래픽 관리자 프로필 설정을 통해 toohello 끝점을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-133">Traffic stops being directed toohello endpoints through hello Traffic Manager profile settings.</span></span>
3. <span data-ttu-id="bff5c-134">Toohello 브라우저에서 로그인 [Azure 포털](http://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-134">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="bff5c-135">Hello hello 포털 검색 창에서 검색할 **트래픽 관리자 프로필** 이름을 toomodify를 원하고 hello에 hello 트래픽 관리자 프로필을 클릭 한 다음 결과 표시 하는 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-135">In hello portal’s search bar, search for hello **Traffic Manager profile** name that you want toomodify, and then click hello Traffic Manager profile in hello results that hello displayed.</span></span>
3. <span data-ttu-id="bff5c-136">Hello에 **트래픽 관리자 프로필** 블레이드에서 클릭 **개요**, hello 개요 블레이드에 클릭 **사용 하지 않도록 설정**, toodisable hello 트래픽 관리자 프로필을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-136">In hello **Traffic Manager profile** blade, click **Overview**, in hello Overview blade click **Disable**, and then confirm toodisable hello Traffic Manager profile.</span></span>

### <a name="tooenable-a-profile"></a><span data-ttu-id="bff5c-137">tooenable 프로필</span><span class="sxs-lookup"><span data-stu-id="bff5c-137">tooenable a profile</span></span>

1. <span data-ttu-id="bff5c-138">Toohello 브라우저에서 로그인 [Azure 포털](http://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-138">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="bff5c-139">Hello hello 포털 검색 창에서 검색할 **트래픽 관리자 프로필** 이름을 toomodify를 원하고 hello에 hello 트래픽 관리자 프로필을 클릭 한 다음 결과 표시 하는 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-139">In hello portal’s search bar, search for hello **Traffic Manager profile** name that you want toomodify, and then click hello Traffic Manager profile in hello results that hello displayed.</span></span>
3. <span data-ttu-id="bff5c-140">Hello에 **트래픽 관리자 프로필** 블레이드에서 클릭 **개요**, hello 개요 블레이드에서 다음을 클릭 하 고 **사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-140">In hello **Traffic Manager profile** blade, click **Overview**, and then in hello Overview blade click **Enable**.</span></span>
5. <span data-ttu-id="bff5c-141">사용자 지정 도메인을 사용 하는 경우 트래픽 관리자 프로필의 인터넷 DNS 서버 toopoint toohello 도메인 이름의 CNAME 리소스 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-141">If you are using a custom domain name, create a CNAME resource record on your Internet DNS server toopoint toohello domain name of your Traffic Manager profile.</span></span>
6. <span data-ttu-id="bff5c-142">트래픽은은 toohello 방향이 지정 된 끝점을 다시입니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-142">Traffic is directed toohello endpoints again.</span></span>

### <a name="toodelete-a-profile"></a><span data-ttu-id="bff5c-143">toodelete 프로필</span><span class="sxs-lookup"><span data-stu-id="bff5c-143">toodelete a profile</span></span>

1. <span data-ttu-id="bff5c-144">인터넷 DNS 서버의 DNS 리소스 레코드 hello에 더 이상 트래픽 관리자 프로필의 toohello 도메인 이름을 가리키는 CNAME 리소스 레코드를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-144">Ensure that hello DNS resource record on your Internet DNS server no longer uses a CNAME resource record that points toohello domain name of your Traffic Manager profile.</span></span>
2. <span data-ttu-id="bff5c-145">Hello hello 포털 검색 창에서 검색할 **트래픽 관리자 프로필** 이름을 toomodify를 원하고 hello에 hello 트래픽 관리자 프로필을 클릭 한 다음 결과 표시 하는 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-145">In hello portal’s search bar, search for hello **Traffic Manager profile** name that you want toomodify, and then click hello Traffic Manager profile in hello results that hello displayed.</span></span>
3. <span data-ttu-id="bff5c-146">Hello에 **트래픽 관리자 프로필** 블레이드에서 클릭 **개요**, hello 개요 블레이드에 클릭 **삭제**, toodelete hello 트래픽 관리자 프로필을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bff5c-146">In hello **Traffic Manager profile** blade, click **Overview**, in hello Overview blade click **Delete**, and then confirm toodelete hello Traffic Manager profile.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bff5c-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bff5c-147">Next steps</span></span>

* [<span data-ttu-id="bff5c-148">끝점 추가</span><span class="sxs-lookup"><span data-stu-id="bff5c-148">Add an endpoint</span></span>](traffic-manager-endpoints.md)
* [<span data-ttu-id="bff5c-149">우선 순위 라우팅 메서드 구성</span><span class="sxs-lookup"><span data-stu-id="bff5c-149">Configure Priority routing method</span></span>](traffic-manager-configure-priority-routing-method.md)
* [<span data-ttu-id="bff5c-150">지리적 라우팅 메서드 구성</span><span class="sxs-lookup"><span data-stu-id="bff5c-150">Configure Geographic routing method</span></span>](traffic-manager-configure-geographic-routing-method.md) 
* [<span data-ttu-id="bff5c-151">가중 라우팅 메서드 구성</span><span class="sxs-lookup"><span data-stu-id="bff5c-151">Configure Weighted routing method</span></span>](traffic-manager-configure-weighted-routing-method.md)
* [<span data-ttu-id="bff5c-152">성능 라우팅 메서드 구성</span><span class="sxs-lookup"><span data-stu-id="bff5c-152">Configure Performance routing method</span></span>](traffic-manager-configure-performance-routing-method.md)
