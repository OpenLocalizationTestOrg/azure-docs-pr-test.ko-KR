---
title: "Azure AD 응용 프로그램 프록시 커넥터를 포털 aaaClassic | Microsoft Docs"
description: "에서는 어떻게 toocreate에서 Azure AD 응용 프로그램 프록시 커넥터 그룹 및 관리 합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b283796a-9679-4c79-b703-802bb850f65d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 43559b0f4ffc3c7dbbf00901e89ac276d01796e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a><span data-ttu-id="84c55-103">커넥터 그룹을 사용하여 별도의 네트워크 및 위치에서 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="84c55-103">Publish applications on separate networks and locations using connector groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="84c55-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="84c55-104">Azure portal</span></span>](active-directory-application-proxy-connectors-azure-portal.md)
> * [<span data-ttu-id="84c55-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="84c55-105">Azure classic portal</span></span>](active-directory-application-proxy-connectors.md)
>
>

<span data-ttu-id="84c55-106">커넥터 그룹은 다음을 비롯한 다양한 시나리오에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="84c55-106">Connector groups are useful for various scenarios, including:</span></span>

* <span data-ttu-id="84c55-107">여러 데이터 센터가 연결되어 있는 사이트.</span><span class="sxs-lookup"><span data-stu-id="84c55-107">Sites with multiple interconnected datacenters.</span></span> <span data-ttu-id="84c55-108">이 경우 원하는 tookeep hello 데이터 센터 내에서 많은 트래픽을 최대한 데이터 센터 간 링크는 비용이 많이 들고 느린 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84c55-108">In this case, you want tookeep as much traffic within hello datacenter as possible because cross-datacenter links are expensive and slow.</span></span> <span data-ttu-id="84c55-109">각 데이터 센터 tooserve hello 응용 프로그램만 hello 데이터 센터 내에 있는 커넥터를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84c55-109">You can deploy connectors in each datacenter tooserve only hello applications that reside within hello datacenter.</span></span> <span data-ttu-id="84c55-110">이 방법은 데이터 센터 간 링크를 최소화 하 고 tooyour 사용자 완전히 투명 한 경험을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="84c55-110">This approach minimizes cross-datacenter links and provides an entirely transparent experience tooyour users.</span></span>
* <span data-ttu-id="84c55-111">Hello 주요 회사 네트워크의 일부가 아닌 있는 격리 된 네트워크에 설치 된 응용 프로그램을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="84c55-111">Managing applications installed on isolated networks that are not part of hello main corporate network.</span></span> <span data-ttu-id="84c55-112">격리 된 네트워크 tooalso 응용 프로그램 격리 toohello 네트워크에 커넥터 그룹 전용 tooinstall 커넥터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84c55-112">You can use connector groups tooinstall dedicated connectors on isolated networks tooalso isolate applications toohello network.</span></span>
* <span data-ttu-id="84c55-113">클라우드 액세스를 위해 IaaS에 설치 된 응용 프로그램에 대 한 커넥터 그룹을 공통 서비스 toosecure hello 액세스 tooall hello 앱을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="84c55-113">For applications installed on IaaS for cloud access, connector groups provide a common service toosecure hello access tooall hello apps.</span></span> <span data-ttu-id="84c55-114">커넥터 그룹 추가 종속성이 회사 네트워크에 생성 하거나 hello 앱 환경을 조각 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="84c55-114">Connector groups don't create additional dependency on your corporate network, or fragment hello app experience.</span></span> <span data-ttu-id="84c55-115">커넥터는 각 클라우드 데이터 센터에 설치될 수 있으며 이 네트워크에 있는 응용 프로그램만 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84c55-115">Connectors can be installed on every cloud datacenter and serve only applications that reside in this network.</span></span> <span data-ttu-id="84c55-116">여러 커넥터 tooachieve 고가용성을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84c55-116">You can install several connectors tooachieve high availability.</span></span>
* <span data-ttu-id="84c55-117">특정 커넥터 포리스트당 배포 하 고 tooserve 특정 응용 프로그램 설정 될 수 있는 다중 포리스트 환경에 대 한 지원.</span><span class="sxs-lookup"><span data-stu-id="84c55-117">Support for multi-forest environments in which specific connectors can be deployed per forest and set tooserve specific applications.</span></span>
* <span data-ttu-id="84c55-118">커넥터 그룹 tooeither 장애 조치를 감지 하거나에 대 한 백업으로 주 hello 재해 복구 사이트에서 사용할 수 있습니다 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="84c55-118">Connector groups can be used in Disaster Recovery sites tooeither detect failover or as backup for hello main site.</span></span>
* <span data-ttu-id="84c55-119">커넥터 그룹 수도 tooserve 사용 되는 단일 테 넌 트의 여러 회사 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84c55-119">Connector groups can also be used tooserve multiple companies from a single tenant.</span></span>

## <a name="prerequisite-create-your-connectors"></a><span data-ttu-id="84c55-120">필수 조건: 커넥터 만들기</span><span class="sxs-lookup"><span data-stu-id="84c55-120">Prerequisite: Create your connectors</span></span>
<span data-ttu-id="84c55-121">toogroup 커넥터, [여러 명의 커넥터가 설치](active-directory-application-proxy-enable.md), 한 다음 이름을 지정 하 고 그룹화 합니다.</span><span class="sxs-lookup"><span data-stu-id="84c55-121">toogroup your connectors, [install multiple connectors](active-directory-application-proxy-enable.md), then name and group them.</span></span> <span data-ttu-id="84c55-122">Tooassign가 마지막으로 해당 toospecific 앱.</span><span class="sxs-lookup"><span data-stu-id="84c55-122">Finally you have tooassign them toospecific apps.</span></span>

## <a name="step-1-create-connector-groups"></a><span data-ttu-id="84c55-123">1단계: 커넥터 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="84c55-123">Step 1: Create connector groups</span></span>
<span data-ttu-id="84c55-124">원하는 수 만큼 커넥터 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84c55-124">You can create as many connector groups as you want.</span></span> <span data-ttu-id="84c55-125">커넥터 그룹을 만들 hello Azure 클래식 포털에서에서 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84c55-125">Connector group creation is accomplished in hello Azure classic portal.</span></span>

1. <span data-ttu-id="84c55-126">디렉터리를 선택하고 **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="84c55-126">Select your directory and click **Configure**.</span></span>  
    <span data-ttu-id="84c55-127">![응용 프로그램 프록시 구성 스크린샷 - 커넥터 그룹 관리 클릭](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span><span class="sxs-lookup"><span data-stu-id="84c55-127">![Application proxy, configure screenshot - click manage connector groups](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span></span>
2. <span data-ttu-id="84c55-128">응용 프로그램 프록시를 아래에서 클릭 **커넥터 그룹 관리** 고 hello 그룹 이름을 제공 하 여 커넥터 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84c55-128">Under Application Proxy, click **Manage Connector Groups** and create a connector group by giving hello group a name.</span></span>  
    <span data-ttu-id="84c55-129">![응용 프로그램 프록시 커넥터 그룹 스크린샷 - 새 그룹 이름 지정](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span><span class="sxs-lookup"><span data-stu-id="84c55-129">![Application proxy connector groups screenshot - name new group](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span></span>

## <a name="step-2-assign-connectors-tooyour-groups"></a><span data-ttu-id="84c55-130">2 단계: tooyour 그룹 커넥터 할당</span><span class="sxs-lookup"><span data-stu-id="84c55-130">Step 2: Assign connectors tooyour groups</span></span>
<span data-ttu-id="84c55-131">Hello 커넥터 그룹을 만든 후 hello 커넥터 toohello 적절 한 그룹을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="84c55-131">Once hello connector groups are created, move hello connectors toohello appropriate group.</span></span>

1. <span data-ttu-id="84c55-132">**응용 프로그램 프록시**에서 **커넥터 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="84c55-132">Under **Application Proxy**, click **Manage Connectors**.</span></span>
2. <span data-ttu-id="84c55-133">아래 **그룹**선택, 각 커넥터에 대해 원하는 hello 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="84c55-133">Under **Group**, select hello group you want for each connector.</span></span> <span data-ttu-id="84c55-134">Hello 새 그룹에 활성 too10 분 toobecome hello 커넥터가 걸릴 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84c55-134">It might take hello connectors up too10 minutes toobecome active in hello new group.</span></span>  
    <span data-ttu-id="84c55-135">![응용 프로그램 프록시 커넥터 스크린샷 - 드롭다운 메뉴에서 그룹 선택](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span><span class="sxs-lookup"><span data-stu-id="84c55-135">![Application proxy connectors screenshot - select group from dropdown menu](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span></span>

## <a name="step-3-assign-applications-tooyour-connector-groups"></a><span data-ttu-id="84c55-136">3 단계: tooyour 커넥터 그룹 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="84c55-136">Step 3: Assign applications tooyour connector groups</span></span>
<span data-ttu-id="84c55-137">hello 마지막 단계는 tooset 서비스를 제공 하는 각 응용 프로그램 toohello 커넥터 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="84c55-137">hello last step is tooset each application toohello connector group that serves it.</span></span>

1. <span data-ttu-id="84c55-138">Hello 디렉터리에 Azure 클래식 포털에서에서 선택 hello tooassign toohello 그룹을 클릭 하 여 응용 프로그램 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="84c55-138">In hello Azure classic portal, in your directory, select hello Application you want tooassign toohello group and click **Configure**.</span></span>
2. <span data-ttu-id="84c55-139">아래 **커넥터 그룹**선택, 응용 프로그램 toouse hello 원하는 hello 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="84c55-139">Under **Connector group**, select hello group you want hello application toouse.</span></span> <span data-ttu-id="84c55-140">이 변경은 즉시 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="84c55-140">This change is immediately applied.</span></span>  
    <span data-ttu-id="84c55-141">![응용 프로그램 프록시 커넥터 그룹 스크린샷 - 드롭다운 메뉴에서 그룹 선택](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span><span class="sxs-lookup"><span data-stu-id="84c55-141">![Application proxy connector group screenshot - select group from dropdown menu](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span></span>

## <a name="see-also"></a><span data-ttu-id="84c55-142">참고 항목</span><span class="sxs-lookup"><span data-stu-id="84c55-142">See also</span></span>
* [<span data-ttu-id="84c55-143">응용 프로그램 프록시 사용</span><span class="sxs-lookup"><span data-stu-id="84c55-143">Enable Application Proxy</span></span>](active-directory-application-proxy-enable.md)
* [<span data-ttu-id="84c55-144">Single Sign-On 사용</span><span class="sxs-lookup"><span data-stu-id="84c55-144">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="84c55-145">조건부 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="84c55-145">Enable conditional access</span></span>](active-directory-application-proxy-conditional-access.md)
* [<span data-ttu-id="84c55-146">응용 프로그램 프록시에서 발생한 문제 해결</span><span class="sxs-lookup"><span data-stu-id="84c55-146">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)

<span data-ttu-id="84c55-147">Hello 최신 뉴스 및 업데이트에 대 한 체크 아웃 hello [응용 프로그램 프록시 블로그](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="84c55-147">For hello latest news and updates, check out hello [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
