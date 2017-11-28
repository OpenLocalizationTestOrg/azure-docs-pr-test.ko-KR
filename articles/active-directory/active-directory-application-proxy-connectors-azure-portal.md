---
title: "분리 된 네트워크 및 Azure AD 응용 프로그램 프록시에서 커넥터 그룹을 사용 하 여 위치에서 응용 프로그램 aaaPublishing | Microsoft Docs"
description: "에서는 어떻게 toocreate에서 Azure AD 응용 프로그램 프록시 커넥터 그룹 및 관리 합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: 8c9a84b365eab28eaaeb343d4d1e2e6990537fec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a><span data-ttu-id="5010d-103">커넥터 그룹을 사용하여 별도의 네트워크 및 위치에서 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="5010d-103">Publish applications on separate networks and locations using connector groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5010d-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5010d-104">Azure portal</span></span>](active-directory-application-proxy-connectors-azure-portal.md)
> * [<span data-ttu-id="5010d-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="5010d-105">Azure classic portal</span></span>](active-directory-application-proxy-connectors.md)
>

<span data-ttu-id="5010d-106">고객은 점점 더 많은 시나리오와 응용 프로그램을 위해 Azure AD의 응용 프로그램 프록시를 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-106">Customers utilize Azure AD's Application Proxy for more and more scenarios and applications.</span></span> <span data-ttu-id="5010d-107">따라서 더 많은 토폴로지를 사용하여 응용 프로그램 프록시를 더욱 유연하게 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-107">So we've made App Proxy even more flexible by enabling more topologies.</span></span> <span data-ttu-id="5010d-108">특정 커넥터 tooserve 특정 응용 프로그램을 할당할 수 있도록 응용 프로그램 프록시 커넥터 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-108">You can create Application Proxy connector groups so that you can assign specific connectors tooserve specific applications.</span></span> <span data-ttu-id="5010d-109">이 기능을 사용 하면 더 많은 제어 및 방법 toooptimize 응용 프로그램 프록시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-109">This capability gives you more control and ways toooptimize your Application Proxy deployment.</span></span> 

<span data-ttu-id="5010d-110">각 응용 프로그램 프록시 커넥터 tooa 커넥터 그룹에 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-110">Each Application Proxy connector is assigned tooa connector group.</span></span> <span data-ttu-id="5010d-111">모든 커넥터를 커넥터 그룹을 같은 고가용성 및 부하 분산에 대 한 별도 단위를 프록시로 toohello 속하는 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-111">All hello connectors that belong toohello same connector group act as a separate unit for high-availability and load balancing.</span></span> <span data-ttu-id="5010d-112">모든 커넥터에 포함할 tooa 커넥터 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-112">All connectors belong tooa connector group.</span></span> <span data-ttu-id="5010d-113">그룹을 만들지 않는 경우 모든 커넥터는 기본 그룹에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-113">If you don't create groups, then all your connectors are in a default group.</span></span> <span data-ttu-id="5010d-114">관리자에 게 새 그룹 만들고 커넥터 toothem hello Azure 포털에서에서 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-114">Your admin can create new groups and assign connectors toothem in hello Azure portal.</span></span> 

<span data-ttu-id="5010d-115">모든 응용 프로그램 tooa 커넥터 그룹에 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-115">All applications are assigned tooa connector group.</span></span> <span data-ttu-id="5010d-116">그룹을 만들지 않는 경우 tooa 기본 그룹 응용 프로그램에 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-116">If you don't create groups, then all your applications are assigned tooa default group.</span></span> <span data-ttu-id="5010d-117">하지만 특정 커넥터 그룹과 함께 각 응용 프로그램 toowork를 그룹으로 커넥터를 구성 하는 경우 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-117">But if you organize your connectors into groups, you can set each application toowork with a specific connector group.</span></span> <span data-ttu-id="5010d-118">이 경우 해당 그룹의 유일한 hello 커넥터는 요청 시 hello 응용 프로그램을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-118">In this case, only hello connectors in that group serve hello application upon request.</span></span> <span data-ttu-id="5010d-119">이 기능은 응용 프로그램이 서로 다른 위치에서 호스트되는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-119">This feature is useful if your applications are hosted in different locations.</span></span> <span data-ttu-id="5010d-120">응용 프로그램은 항상 물리적으로 닫기 toothem 되는 커넥터를 통해 제공 됩니다 되도록 위치에 따라 커넥터 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-120">You can create connector groups based on location, so that applications are always served by connectors that are physically close toothem.</span></span>

>[!TIP] 
><span data-ttu-id="5010d-121">대규모 응용 프로그램 프록시 배포를 설정한 경우 모든 응용 프로그램 toohello 기본 커넥터 그룹을 할당 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="5010d-121">If you have a large Application Proxy deployment, don't assign any applications toohello default connector group.</span></span> <span data-ttu-id="5010d-122">이런 방식으로 새 커넥터 되지 않습니다 라이브 트래픽을 tooan 활성 커넥터 그룹을 할당할 때까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-122">That way, new connectors don't receive any live traffic until you assign them tooan active connector group.</span></span> <span data-ttu-id="5010d-123">이 구성 하면 수도 tooput 커넥터 유휴 모드에서 백 toohello 기본 그룹을 이동 하 여 사용자가 영향을 주지 않고 유지 관리를 수행할 수 있도록 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-123">This configuration also enables you tooput connectors in an idle mode by moving them back toohello default group, so that you can perform maintenance without impacting your users.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5010d-124">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5010d-124">Prerequisites</span></span>
<span data-ttu-id="5010d-125">toogroup 커넥터, toomake 있는지 있는 있습니다 [여러 명의 커넥터가 설치](active-directory-application-proxy-enable.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-125">toogroup your connectors, you have toomake sure you [installed multiple connectors](active-directory-application-proxy-enable.md).</span></span> <span data-ttu-id="5010d-126">Hello 새 커넥터를 설치할 때 자동으로 조인 **기본** 커넥터 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-126">When you install a new connector, it automatically joins hello **Default** connector group.</span></span>

## <a name="create-connector-groups"></a><span data-ttu-id="5010d-127">커넥터 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="5010d-127">Create connector groups</span></span>
<span data-ttu-id="5010d-128">이러한 단계 toocreate 원하는 수 만큼 커넥터 그룹을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-128">Use these steps toocreate as many connector groups as you want.</span></span> 

1. <span data-ttu-id="5010d-129">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-129">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="5010d-130">**Azure Active Directory** > **Enterprise 응용 프로그램** > **응용 프로그램 프록시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-130">Select **Azure Active Directory** > **Enterprise applications** > **Application proxy**.</span></span>
2. <span data-ttu-id="5010d-131">**새 커넥터 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-131">Select **New connector group**.</span></span> <span data-ttu-id="5010d-132">hello 새 커넥터 그룹 블레이드가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-132">hello New Connector Group blade appears.</span></span>

   ![새 커넥터 그룹 선택](./media/active-directory-application-proxy-connectors-azure-portal/new-group.png)

3. <span data-ttu-id="5010d-134">새 커넥터 그룹에 이름을 지정 하 고이 그룹에 속하는 커넥터 hello 드롭다운 메뉴 tooselect을 사용 하십시오.</span><span class="sxs-lookup"><span data-stu-id="5010d-134">Give your new connector group a name, then use hello dropdown menu tooselect which connectors belong in this group.</span></span>
4. <span data-ttu-id="5010d-135">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-135">Select **Save**.</span></span>

## <a name="assign-applications-tooyour-connector-groups"></a><span data-ttu-id="5010d-136">Tooyour 커넥터 그룹 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="5010d-136">Assign applications tooyour connector groups</span></span>
<span data-ttu-id="5010d-137">응용 프로그램 프록시를 사용하여 게시한 각 응용 프로그램에 대해 이 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-137">Use these steps for each application that you've published with Application Proxy.</span></span> <span data-ttu-id="5010d-138">먼저 게시, 또는 언제 든 지 이러한 단계 toochange hello 할당을 사용할 수 있습니다 때 응용 프로그램 tooa 커넥터 그룹을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-138">You can assign an application tooa connector group when you first publish it, or you can use these steps toochange hello assignment whenever you want.</span></span>   

1. <span data-ttu-id="5010d-139">디렉터리에 대 한 hello 관리 대시보드를 선택 **엔터프라이즈 응용 프로그램** > **모든 응용 프로그램** > hello tooassign tooa 커넥터 그룹을 만들려는 응용 프로그램 >  **응용 프로그램 프록시**합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-139">From hello management dashboard for your directory, select **Enterprise applications** > **All applications** > hello application you want tooassign tooa connector group > **Application Proxy**.</span></span>
2. <span data-ttu-id="5010d-140">사용 하 여 hello **커넥터 그룹** 드롭다운 메뉴 tooselect hello 그룹 응용 프로그램 toouse hello 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-140">Use hello **Connector Group** dropdown menu tooselect hello group you want hello application toouse.</span></span>
3. <span data-ttu-id="5010d-141">선택 **저장** tooapply hello 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-141">Select **Save** tooapply hello change.</span></span>

## <a name="use-cases-for-connector-groups"></a><span data-ttu-id="5010d-142">커넥터 그룹의 사용 사례</span><span class="sxs-lookup"><span data-stu-id="5010d-142">Use cases for connector groups</span></span> 

<span data-ttu-id="5010d-143">커넥터 그룹은 다음을 비롯한 다양한 시나리오에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-143">Connector groups are useful for various scenarios, including:</span></span>

### <a name="sites-with-multiple-interconnected-datacenters"></a><span data-ttu-id="5010d-144">여러 데이터 센터가 연결되어 있는 사이트</span><span class="sxs-lookup"><span data-stu-id="5010d-144">Sites with multiple interconnected datacenters</span></span>

<span data-ttu-id="5010d-145">많은 조직에는 서로 연결된 데이터 센터가 여러 개 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-145">Many organizations have a number of interconnected datacenters.</span></span> <span data-ttu-id="5010d-146">이 경우 원하는 tookeep hello 데이터 센터 내에서 많은 트래픽을 최대한 데이터 센터 간 링크는 비용이 많이 들고 느린 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-146">In this case, you want tookeep as much traffic within hello datacenter as possible because cross-datacenter links are expensive and slow.</span></span> <span data-ttu-id="5010d-147">각 데이터 센터 tooserve hello 응용 프로그램만 hello 데이터 센터 내에 있는 커넥터를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-147">You can deploy connectors in each datacenter tooserve only hello applications that reside within hello datacenter.</span></span> <span data-ttu-id="5010d-148">이 방법은 데이터 센터 간 링크를 최소화 하 고 tooyour 사용자 완전히 투명 한 경험을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-148">This approach minimizes cross-datacenter links and provides an entirely transparent experience tooyour users.</span></span>

### <a name="applications-installed-on-isolated-networks"></a><span data-ttu-id="5010d-149">격리된 네트워크에 설치된 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="5010d-149">Applications installed on isolated networks</span></span>

<span data-ttu-id="5010d-150">Hello 주요 회사 네트워크의 일부가 아닌 되는 네트워크에서 응용 프로그램을 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-150">Applications can be hosted in networks that are not part of hello main corporate network.</span></span> <span data-ttu-id="5010d-151">격리 된 네트워크 tooalso 응용 프로그램 격리 toohello 네트워크에 커넥터 그룹 전용 tooinstall 커넥터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-151">You can use connector groups tooinstall dedicated connectors on isolated networks tooalso isolate applications toohello network.</span></span> <span data-ttu-id="5010d-152">이는 일반적으로 타사 공급 업체가 조직의 특정 응용 프로그램을 유지 관리할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-152">This usually happens when a third-party vendor maintains a specific application for your organization.</span></span> 

<span data-ttu-id="5010d-153">커넥터 그룹을 더 안전한 toooutsource 응용 프로그램 관리 toothird 타사 공급 업체 및 있습니다 tooinstall 전용 특정 응용 프로그램을 보다 쉽게 게시 있는 네트워크에 대 한 커넥터 사용.</span><span class="sxs-lookup"><span data-stu-id="5010d-153">Connector groups allow you tooinstall dedicated connectors for those networks that publish only specific applications, making it easier and more secure toooutsource application management toothird-party vendors.</span></span>

### <a name="applications-installed-on-iaas"></a><span data-ttu-id="5010d-154">IaaS에 설치된 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="5010d-154">Applications installed on IaaS</span></span> 

<span data-ttu-id="5010d-155">클라우드 액세스를 위해 IaaS에 설치 된 응용 프로그램에 대 한 커넥터 그룹을 공통 서비스 toosecure hello 액세스 tooall hello 앱을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-155">For applications installed on IaaS for cloud access, connector groups provide a common service toosecure hello access tooall hello apps.</span></span> <span data-ttu-id="5010d-156">커넥터 그룹 추가 종속성이 회사 네트워크에 생성 하거나 hello 앱 환경을 조각 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="5010d-156">Connector groups don't create additional dependency on your corporate network, or fragment hello app experience.</span></span> <span data-ttu-id="5010d-157">커넥터는 각 클라우드 데이터 센터에 설치될 수 있으며 해당 네트워크에 있는 응용 프로그램만 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-157">Connectors can be installed on every cloud datacenter and serve only applications that reside in that network.</span></span> <span data-ttu-id="5010d-158">여러 커넥터 tooachieve 고가용성을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-158">You can install several connectors tooachieve high availability.</span></span>

<span data-ttu-id="5010d-159">예를 들어 여러 가상 컴퓨터를 사용 하는 조직을 tootheir 자체 호스팅되는 IaaS 가상 네트워크 연결을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-159">Take as an example an organization that has several virtual machines connected tootheir own IaaS hosted virtual network.</span></span> <span data-ttu-id="5010d-160">tooallow 직원 toouse 이러한 응용 프로그램 개인 네트워크는 사이트 간 VPN을 사용 하 여 연결 된 toohello 회사 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-160">tooallow employees toouse these applications, these private networks are connected toohello corporate network using site-to-site VPN.</span></span> <span data-ttu-id="5010d-161">이는 온-프레미스에 있는 직원들에게 좋은 경험을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-161">This provides a good experience for employees that are located on-premises.</span></span> <span data-ttu-id="5010d-162">하지만 원격 직원에 대 한 이상적인 아래 hello 다이어그램에서 볼 수 있듯이 추가 온-프레미스 인프라 tooroute 액세스 필요 하기 때문에 되지:</span><span class="sxs-lookup"><span data-stu-id="5010d-162">But, it may not be ideal for remote employees, because it requires additional on-premises infrastructure tooroute access, as you can see in hello diagram below:</span></span>

![Azure Ad Iaas 네트워크](./media/application-proxy-publish-apps-separate-networks/application-proxy-iaas-network.png)
  
<span data-ttu-id="5010d-164">Azure AD 응용 프로그램 프록시 커넥터 그룹을 사용 회사 네트워크에서 추가 종속성을 만들지 않고는 공통 서비스 toosecure hello 액세스 tooall 응용 프로그램을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-164">With Azure AD Application Proxy connector groups, you can enable a common service toosecure hello access tooall applications without creating additional dependency on your corporate network:</span></span>

![Azure AD Iaas - 여러 클라우드 공급 업체](./media/application-proxy-publish-apps-separate-networks/application-proxy-multiple-cloud-vendors.png)

### <a name="multi-forest--different-connector-groups-for-each-forest"></a><span data-ttu-id="5010d-166">다중 포리스트 - 포리스트마다 서로 다른 커넥터 그룹</span><span class="sxs-lookup"><span data-stu-id="5010d-166">Multi-forest – different connector groups for each forest</span></span>

<span data-ttu-id="5010d-167">응용 프로그램 프록시를 배포한 대부분의 고객은 KCD(Kerberos 제한 위임)를 수행하여 SSO(Single-Sign-On) 기능을 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-167">Most customers who have deployed Application Proxy are using its single-sign-on (SSO) capabilities by performing Kerberos Constrained Delegation (KCD).</span></span> <span data-ttu-id="5010d-168">tooachieve이 hello 커넥터의 컴퓨터 필요 toobe 조인된 tooa 도메인 hello 응용 프로그램으로 hello 사용자가 위임할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-168">tooachieve this, hello connector’s machines need toobe joined tooa domain that can delegate hello users toward hello application.</span></span> <span data-ttu-id="5010d-169">KCD는 포리스트 간 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-169">KCD supports cross-forest capabilities.</span></span> <span data-ttu-id="5010d-170">그러나 서로 간에 신뢰할 수 없는 고유한 다중 포리스트 환경이 있는 회사의 경우 모든 포리스트에 대해 단일 커넥터를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-170">But for companies who have distinct multi-forest environments with no trust between them, a single connector cannot be used for all forests.</span></span> 

<span data-ttu-id="5010d-171">이 경우 포리스트당 특정 커넥터를 배포할 수 있습니다 및 집합 tooserve 실행 된 응용 프로그램 게시 tooserve는 해당 특정 포리스트의 사용자가 hello만 합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-171">In this case, specific connectors can be deployed per forest, and set tooserve applications that were published tooserve only hello users of that specific forest.</span></span> <span data-ttu-id="5010d-172">각 커넥터 그룹마다 별도의 포리스트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-172">Each connector group represents a different forest.</span></span> <span data-ttu-id="5010d-173">Hello 테 넌 트와 대부분 hello 경험의는 포리스트 전반에 대 한 통합, 하는 동안 사용자가 Azure AD 그룹을 사용 하 여 tootheir 포리스트의 응용 프로그램을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-173">While hello tenant and most of hello experience is unified for all forests, users can be assigned tootheir forest applications using Azure AD groups.</span></span>
 
### <a name="disaster-recovery-sites"></a><span data-ttu-id="5010d-174">재해 복구 사이트</span><span class="sxs-lookup"><span data-stu-id="5010d-174">Disaster Recovery sites</span></span>

<span data-ttu-id="5010d-175">다음과 같이 사이트 구현 방법에 따라 DR(재해 복구) 사이트에서 수행할 수 있는 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-175">There are two different approaches you can take with a disaster recovery (DR) site, depending on how your sites are implemented:</span></span>

* <span data-ttu-id="5010d-176">DR 사이트가 있는 hello 주 사이트와 동일 하 게 하 고 있어서 액티브-액티브 모드에서 빌드되는 경우 동일한 hello 네트워킹과 AD 설정 hello DR 사이트에서 hello hello 커넥터를 만들 수 있습니다 hello 주 사이트와 동일한 커넥터 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-176">If your DR site is built in active-active mode where it is exactly like hello main site and has hello same networking and AD settings, you can create hello connectors on hello DR site in hello same connector group as hello main site.</span></span> <span data-ttu-id="5010d-177">이 통해 사용자에 대 한 Azure AD toodetect 장애 조치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-177">This enables Azure AD toodetect failovers for you.</span></span>
* <span data-ttu-id="5010d-178">DR 사이트는 hello 주 사이트에서 별도 hello DR 사이트에서 다른 커넥터 그룹을 만들 수 있습니다, 하나 1) 백업 응용 프로그램이 있는 경우 또는 2) 수동으로 필요에 따라 hello 기존 응용 프로그램 toohello DR 커넥터 그룹을 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-178">If your DR site is separate from hello main site, you can create a different connector group in hello DR site, and either 1) have backup applications or 2) manually divert hello existing application toohello DR connector group as needed.</span></span>
 
### <a name="serve-multiple-companies-from-a-single-tenant"></a><span data-ttu-id="5010d-179">단일 테넌트에서 여러 회사 제공</span><span class="sxs-lookup"><span data-stu-id="5010d-179">Serve multiple companies from a single tenant</span></span>

<span data-ttu-id="5010d-180">여러 가지 다른 방법으로는 단일 서비스 공급자를 배포 하 고 Azure AD를 유지 관리 모델 tooimplement 관련 여러 회사에 대 한 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-180">There are many different ways tooimplement a model in which a single service provider deploys and maintains Azure AD related services for multiple companies.</span></span> <span data-ttu-id="5010d-181">커넥터 그룹 도움말 admin 님 안녕하세요 hello 커넥터와 다른 그룹으로 응용 프로그램을 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-181">Connector groups help hello admin segregate hello connectors and applications into different groups.</span></span> <span data-ttu-id="5010d-182">소규모 회사에 적합 한는 한 가지 방법은 것 toohave 단일 hello 서로 다른 회사에 들어 있는 도메인 이름 및 네트워크 하는 동안 Azure AD 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-182">One way, which is suitable for small companies, is toohave a single Azure AD tenant while hello different companies have their own domain name and networks.</span></span> <span data-ttu-id="5010d-183">또한 단일 IT 부서에서 규제 또는 비즈니스 상의 이유로 여러 회사에 서비스를 제공하는 M&A 시나리오 및 상황에서도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-183">This is also true for M&A scenarios and situations where a single IT division serves several companies for regulatory or business reasons.</span></span> 

## <a name="sample-configurations"></a><span data-ttu-id="5010d-184">샘플 구성</span><span class="sxs-lookup"><span data-stu-id="5010d-184">Sample configurations</span></span>

<span data-ttu-id="5010d-185">구현할 수 있는 몇 가지 예는 커넥터 그룹을 다음 hello를 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-185">Some examples that you can implement, include hello following connector groups.</span></span>
 
### <a name="default-configuration--no-use-for-connector-groups"></a><span data-ttu-id="5010d-186">기본 구성 - 커넥터 그룹 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="5010d-186">Default configuration – no use for connector groups</span></span>

<span data-ttu-id="5010d-187">커넥터 그룹을 사용하지 않는 경우 구성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-187">If you don’t use connector groups, your configuration would look like this:</span></span>

![Azure AD - 커넥터 그룹 없음](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-1.png)
 
<span data-ttu-id="5010d-189">이 구성은 소규모 배포 및 테스트에 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-189">This configuration is sufficient for small deployments and tests.</span></span> <span data-ttu-id="5010d-190">또한 조직에 플랫 네트워크 토폴로지가 있는 경우에도 잘 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-190">It will also work well if your organization has a flat network topology.</span></span>
 
### <a name="default-configuration-and-an-isolated-network"></a><span data-ttu-id="5010d-191">기본 구성 및 격리된 네트워크</span><span class="sxs-lookup"><span data-stu-id="5010d-191">Default configuration and an isolated network</span></span>

<span data-ttu-id="5010d-192">이 구성은 발전 된 hello 기본 IaaS 가상 네트워크와 같은 격리 된 네트워크에서 실행 되는 특정 응용 프로그램은 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-192">This configuration is an evolution of hello default one, in which there is a specific app that runs in an isolated network such as IaaS virtual network:</span></span> 

![Azure AD - 커넥터 그룹 없음](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-2.png)
 
### <a name="recommended-configuration--several-specific-groups-and-a-default-group-for-idle"></a><span data-ttu-id="5010d-194">권장 구성 - 여러 특정 그룹 및 유휴 상태의 기본 그룹</span><span class="sxs-lookup"><span data-stu-id="5010d-194">Recommended configuration – several specific groups and a default group for idle</span></span>

<span data-ttu-id="5010d-195">권장 구성 크고 복잡 한 조직에 대 한 hello은 유휴 상태가 되거나 새로 설치 된 커넥터에 사용 되는 모든 응용 프로그램을 제공 하지 않는 그룹으로 toohave hello 기본 커넥터 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-195">hello recommended configuration for large and complex organizations is toohave hello default connector group as a group that doesn’t serve any applications and is used for idle or newly installed connectors.</span></span> <span data-ttu-id="5010d-196">모든 응용 프로그램은 사용자 지정된 커넥터 그룹을 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-196">All applications are served using customized connector groups.</span></span> <span data-ttu-id="5010d-197">이렇게 하면 위에서 설명한 hello 시나리오의 모든 hello 복잡 한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-197">This enables all hello complexity of hello scenarios described above.</span></span>

<span data-ttu-id="5010d-198">Hello 아래 예제에서는 hello 회사에는 두 데이터 센터, A와 B를 각 사이트를 제공 하는 두 명의 연결선으로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-198">In hello example below, hello company has two datacenters, A and B, with two connectors that serve each site.</span></span> <span data-ttu-id="5010d-199">각 사이트에는 실행되는 다양한 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5010d-199">Each site has different applications that run on it.</span></span> 

![Azure AD - 커넥터 그룹 없음](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-3.png)
 
## <a name="next-steps"></a><span data-ttu-id="5010d-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5010d-201">Next steps</span></span>

* [<span data-ttu-id="5010d-202">Azure AD 응용 프로그램 프록시 커넥터 이해</span><span class="sxs-lookup"><span data-stu-id="5010d-202">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
* [<span data-ttu-id="5010d-203">Single Sign-On 사용</span><span class="sxs-lookup"><span data-stu-id="5010d-203">Enable single-sign on</span></span>](application-proxy-sso-overview.md)


