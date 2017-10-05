---
title: "Azure AD 응용 프로그램 프록시에서 커넥터 그룹을 사용하여 별도의 네트워크와 위치에 응용 프로그램 게시 | Microsoft Docs"
description: "Azure AD 응용 프로그램 프록시에서 커넥터 그룹을 만들고 관리하는 방법에 대해 설명합니다."
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
ms.openlocfilehash: 1b08a0b376cbcae8522364c9b6ef22e9c0176438
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a><span data-ttu-id="746e7-103">커넥터 그룹을 사용하여 별도의 네트워크 및 위치에서 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="746e7-103">Publish applications on separate networks and locations using connector groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="746e7-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="746e7-104">Azure portal</span></span>](active-directory-application-proxy-connectors-azure-portal.md)
> * [<span data-ttu-id="746e7-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="746e7-105">Azure classic portal</span></span>](active-directory-application-proxy-connectors.md)
>

<span data-ttu-id="746e7-106">고객은 점점 더 많은 시나리오와 응용 프로그램을 위해 Azure AD의 응용 프로그램 프록시를 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-106">Customers utilize Azure AD's Application Proxy for more and more scenarios and applications.</span></span> <span data-ttu-id="746e7-107">따라서 더 많은 토폴로지를 사용하여 응용 프로그램 프록시를 더욱 유연하게 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-107">So we've made App Proxy even more flexible by enabling more topologies.</span></span> <span data-ttu-id="746e7-108">특정 응용 프로그램을 제공하는 특정 커넥터를 할당할 수 있도록 응용 프로그램 프록시 커넥터 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-108">You can create Application Proxy connector groups so that you can assign specific connectors to serve specific applications.</span></span> <span data-ttu-id="746e7-109">이 기능은 응용 프로그램 프록시 배포를 최적화하는 보다 많은 제어와 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-109">This capability gives you more control and ways to optimize your Application Proxy deployment.</span></span> 

<span data-ttu-id="746e7-110">각 응용 프로그램 프록시 커넥터는 커넥터 그룹에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-110">Each Application Proxy connector is assigned to a connector group.</span></span> <span data-ttu-id="746e7-111">동일한 커넥터 그룹에 속한 모든 커넥터는 고가용성 및 부하 분산을 위해 별도의 단위로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-111">All the connectors that belong to the same connector group act as a separate unit for high-availability and load balancing.</span></span> <span data-ttu-id="746e7-112">모든 커넥터는 커넥터 그룹에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-112">All connectors belong to a connector group.</span></span> <span data-ttu-id="746e7-113">그룹을 만들지 않는 경우 모든 커넥터는 기본 그룹에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-113">If you don't create groups, then all your connectors are in a default group.</span></span> <span data-ttu-id="746e7-114">관리자는 Azure Portal에서 새 그룹을 만들고 커넥터를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-114">Your admin can create new groups and assign connectors to them in the Azure portal.</span></span> 

<span data-ttu-id="746e7-115">모든 응용 프로그램은 커넥터 그룹에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-115">All applications are assigned to a connector group.</span></span> <span data-ttu-id="746e7-116">그룹을 만들지 않는 경우 모든 응용 프로그램은 기본 그룹에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-116">If you don't create groups, then all your applications are assigned to a default group.</span></span> <span data-ttu-id="746e7-117">그러나 커넥터를 그룹으로 구성하면 특정 커넥터 그룹과 함께 작동하도록 각 응용 프로그램을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-117">But if you organize your connectors into groups, you can set each application to work with a specific connector group.</span></span> <span data-ttu-id="746e7-118">이 경우 해당 그룹의 커넥터만 요청에 따라 응용 프로그램을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-118">In this case, only the connectors in that group serve the application upon request.</span></span> <span data-ttu-id="746e7-119">이 기능은 응용 프로그램이 서로 다른 위치에서 호스트되는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-119">This feature is useful if your applications are hosted in different locations.</span></span> <span data-ttu-id="746e7-120">응용 프로그램이 물리적으로 인접한 커넥터를 통해 항상 제공될 수 있도록 위치에 따라 커넥터 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-120">You can create connector groups based on location, so that applications are always served by connectors that are physically close to them.</span></span>

>[!TIP] 
><span data-ttu-id="746e7-121">대규모 응용 프로그램 프록시 배포가 있는 경우 기본 커넥터 그룹에 응용 프로그램을 할당하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="746e7-121">If you have a large Application Proxy deployment, don't assign any applications to the default connector group.</span></span> <span data-ttu-id="746e7-122">이런 방식으로 새 커넥터는 활성 커넥터 그룹에 할당될 때까지 라이브 트래픽을 수신하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-122">That way, new connectors don't receive any live traffic until you assign them to an active connector group.</span></span> <span data-ttu-id="746e7-123">또한 이 구성을 통해 사용자에 영향을 주지 않고 유지 관리를 수행할 수 있도록 기본 그룹으로 다시 이동하여 커넥터를 유휴 모드로 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-123">This configuration also enables you to put connectors in an idle mode by moving them back to the default group, so that you can perform maintenance without impacting your users.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="746e7-124">필수 조건</span><span class="sxs-lookup"><span data-stu-id="746e7-124">Prerequisites</span></span>
<span data-ttu-id="746e7-125">커넥터를 그룹화하려면 [여러 커넥터를 설치](active-directory-application-proxy-enable.md)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-125">To group your connectors, you have to make sure you [installed multiple connectors](active-directory-application-proxy-enable.md).</span></span> <span data-ttu-id="746e7-126">새 커넥터를 설치하면 자동으로 **기본** 커넥터 그룹을 조인합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-126">When you install a new connector, it automatically joins the **Default** connector group.</span></span>

## <a name="create-connector-groups"></a><span data-ttu-id="746e7-127">커넥터 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="746e7-127">Create connector groups</span></span>
<span data-ttu-id="746e7-128">이 단계를 사용하여 원하는 수 만큼 커넥터 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-128">Use these steps to create as many connector groups as you want.</span></span> 

1. <span data-ttu-id="746e7-129">[Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-129">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="746e7-130">**Azure Active Directory** > **Enterprise 응용 프로그램** > **응용 프로그램 프록시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-130">Select **Azure Active Directory** > **Enterprise applications** > **Application proxy**.</span></span>
2. <span data-ttu-id="746e7-131">**새 커넥터 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-131">Select **New connector group**.</span></span> <span data-ttu-id="746e7-132">새 커넥터 그룹 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-132">The New Connector Group blade appears.</span></span>

   ![새 커넥터 그룹 선택](./media/active-directory-application-proxy-connectors-azure-portal/new-group.png)

3. <span data-ttu-id="746e7-134">새 커넥터 그룹에 이름을 지정한 다음 드롭다운 메뉴를 사용하여 이 그룹에 속하는 커넥터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-134">Give your new connector group a name, then use the dropdown menu to select which connectors belong in this group.</span></span>
4. <span data-ttu-id="746e7-135">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-135">Select **Save**.</span></span>

## <a name="assign-applications-to-your-connector-groups"></a><span data-ttu-id="746e7-136">커넥터 그룹에 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="746e7-136">Assign applications to your connector groups</span></span>
<span data-ttu-id="746e7-137">응용 프로그램 프록시를 사용하여 게시한 각 응용 프로그램에 대해 이 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-137">Use these steps for each application that you've published with Application Proxy.</span></span> <span data-ttu-id="746e7-138">처음으로 게시할 때 응용 프로그램을 커넥터 그룹에 할당하거나 이 단계를 사용하여 언제든지 할당을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-138">You can assign an application to a connector group when you first publish it, or you can use these steps to change the assignment whenever you want.</span></span>   

1. <span data-ttu-id="746e7-139">디렉터리에 대한 관리 대시보드의 경우 **엔터프라이즈 응용 프로그램** > **모든 응용 프로그램** > 커넥터 그룹에 할당하려는 응용 프로그램 > **응용 프로그램 프록시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-139">From the management dashboard for your directory, select **Enterprise applications** > **All applications** > the application you want to assign to a connector group > **Application Proxy**.</span></span>
2. <span data-ttu-id="746e7-140">**커넥터 그룹** 드롭다운 메뉴를 사용하여 응용 프로그램에서 사용할 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-140">Use the **Connector Group** dropdown menu to select the group you want the application to use.</span></span>
3. <span data-ttu-id="746e7-141">**저장** 을 선택하여 변경 내용을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-141">Select **Save** to apply the change.</span></span>

## <a name="use-cases-for-connector-groups"></a><span data-ttu-id="746e7-142">커넥터 그룹의 사용 사례</span><span class="sxs-lookup"><span data-stu-id="746e7-142">Use cases for connector groups</span></span> 

<span data-ttu-id="746e7-143">커넥터 그룹은 다음을 비롯한 다양한 시나리오에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-143">Connector groups are useful for various scenarios, including:</span></span>

### <a name="sites-with-multiple-interconnected-datacenters"></a><span data-ttu-id="746e7-144">여러 데이터 센터가 연결되어 있는 사이트</span><span class="sxs-lookup"><span data-stu-id="746e7-144">Sites with multiple interconnected datacenters</span></span>

<span data-ttu-id="746e7-145">많은 조직에는 서로 연결된 데이터 센터가 여러 개 있습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-145">Many organizations have a number of interconnected datacenters.</span></span> <span data-ttu-id="746e7-146">이 경우 데이터 센터 간 링크가 비용이 높고 느리기 때문에 가능한 한 데이터 센터 내에서 많은 트래픽을 유지하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-146">In this case, you want to keep as much traffic within the datacenter as possible because cross-datacenter links are expensive and slow.</span></span> <span data-ttu-id="746e7-147">각 데이터 센터에서 커넥터를 배포하여 데이터 센터 내에 있는 응용 프로그램만 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-147">You can deploy connectors in each datacenter to serve only the applications that reside within the datacenter.</span></span> <span data-ttu-id="746e7-148">이 방법은 데이터 센터 간 링크를 최소화하고 사용자에게 완전히 투명한 경험을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-148">This approach minimizes cross-datacenter links and provides an entirely transparent experience to your users.</span></span>

### <a name="applications-installed-on-isolated-networks"></a><span data-ttu-id="746e7-149">격리된 네트워크에 설치된 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="746e7-149">Applications installed on isolated networks</span></span>

<span data-ttu-id="746e7-150">기본 회사 네트워크에 속하지 않은 네트워크에서 응용 프로그램을 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-150">Applications can be hosted in networks that are not part of the main corporate network.</span></span> <span data-ttu-id="746e7-151">커넥터 그룹을 사용하여 격리된 네트워크의 전용 커넥터를 설치하고 해당 네트워크에 응용 프로그램도 격리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-151">You can use connector groups to install dedicated connectors on isolated networks to also isolate applications to the network.</span></span> <span data-ttu-id="746e7-152">이는 일반적으로 타사 공급 업체가 조직의 특정 응용 프로그램을 유지 관리할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-152">This usually happens when a third-party vendor maintains a specific application for your organization.</span></span> 

<span data-ttu-id="746e7-153">커넥터 그룹을 사용하면 특정 응용 프로그램만 게시하는 네트워크에 전용 커넥터를 설치할 수 있으므로 응용 프로그램 관리를 타사 공급 업체에 보다 쉽고 안전하게 아웃소싱할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-153">Connector groups allow you to install dedicated connectors for those networks that publish only specific applications, making it easier and more secure to outsource application management to third-party vendors.</span></span>

### <a name="applications-installed-on-iaas"></a><span data-ttu-id="746e7-154">IaaS에 설치된 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="746e7-154">Applications installed on IaaS</span></span> 

<span data-ttu-id="746e7-155">클라우드 액세스를 위해 IaaS에 설치된 응용 프로그램의 경우 커넥터 그룹은 모든 앱에 대한 액세스를 보호하는 일반적인 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-155">For applications installed on IaaS for cloud access, connector groups provide a common service to secure the access to all the apps.</span></span> <span data-ttu-id="746e7-156">커넥터 그룹은 회사 네트워크에 추가 종속성을 만들거나 앱 경험을 조각화하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-156">Connector groups don't create additional dependency on your corporate network, or fragment the app experience.</span></span> <span data-ttu-id="746e7-157">커넥터는 각 클라우드 데이터 센터에 설치될 수 있으며 해당 네트워크에 있는 응용 프로그램만 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-157">Connectors can be installed on every cloud datacenter and serve only applications that reside in that network.</span></span> <span data-ttu-id="746e7-158">고가용성을 얻기 위해 커넥터를 여러 개 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-158">You can install several connectors to achieve high availability.</span></span>

<span data-ttu-id="746e7-159">예를 들어 IaaS 호스팅된 고유한 가상 네트워크에 연결된 가상 컴퓨터가 여러 개 있는 조직을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-159">Take as an example an organization that has several virtual machines connected to their own IaaS hosted virtual network.</span></span> <span data-ttu-id="746e7-160">직원들이 해당 응용 프로그램을 사용할 수 있도록 하기 위해 이러한 사설망은 사이트 간 VPN을 사용하여 회사 네트워크에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-160">To allow employees to use these applications, these private networks are connected to the corporate network using site-to-site VPN.</span></span> <span data-ttu-id="746e7-161">이는 온-프레미스에 있는 직원들에게 좋은 경험을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-161">This provides a good experience for employees that are located on-premises.</span></span> <span data-ttu-id="746e7-162">그러나 원격 직원에게는 아래 다이어그램과 같이 추가 온-프레미스 인프라가 액세스를 라우팅해야 하기 때문에 이상적이지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-162">But, it may not be ideal for remote employees, because it requires additional on-premises infrastructure to route access, as you can see in the diagram below:</span></span>

![Azure Ad Iaas 네트워크](./media/application-proxy-publish-apps-separate-networks/application-proxy-iaas-network.png)
  
<span data-ttu-id="746e7-164">Azure AD 응용 프로그램 프록시 커넥터 그룹을 사용하면 공통 서비스를 통해 회사 네트워크에 대한 추가 종속성을 만들지 않고도 모든 응용 프로그램에 대한 액세스를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-164">With Azure AD Application Proxy connector groups, you can enable a common service to secure the access to all applications without creating additional dependency on your corporate network:</span></span>

![Azure AD Iaas - 여러 클라우드 공급 업체](./media/application-proxy-publish-apps-separate-networks/application-proxy-multiple-cloud-vendors.png)

### <a name="multi-forest--different-connector-groups-for-each-forest"></a><span data-ttu-id="746e7-166">다중 포리스트 - 포리스트마다 서로 다른 커넥터 그룹</span><span class="sxs-lookup"><span data-stu-id="746e7-166">Multi-forest – different connector groups for each forest</span></span>

<span data-ttu-id="746e7-167">응용 프로그램 프록시를 배포한 대부분의 고객은 KCD(Kerberos 제한 위임)를 수행하여 SSO(Single-Sign-On) 기능을 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-167">Most customers who have deployed Application Proxy are using its single-sign-on (SSO) capabilities by performing Kerberos Constrained Delegation (KCD).</span></span> <span data-ttu-id="746e7-168">이를 위해 커넥터의 컴퓨터는 사용자를 응용 프로그램에 위임할 수 있는 도메인에 가입해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-168">To achieve this, the connector’s machines need to be joined to a domain that can delegate the users toward the application.</span></span> <span data-ttu-id="746e7-169">KCD는 포리스트 간 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-169">KCD supports cross-forest capabilities.</span></span> <span data-ttu-id="746e7-170">그러나 서로 간에 신뢰할 수 없는 고유한 다중 포리스트 환경이 있는 회사의 경우 모든 포리스트에 대해 단일 커넥터를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-170">But for companies who have distinct multi-forest environments with no trust between them, a single connector cannot be used for all forests.</span></span> 

<span data-ttu-id="746e7-171">이 경우 포리스트마다 특정 커넥터를 배포하고 해당 포리스트의 사용자만 제공하도록 게시된 응용 프로그램을 제공하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-171">In this case, specific connectors can be deployed per forest, and set to serve applications that were published to serve only the users of that specific forest.</span></span> <span data-ttu-id="746e7-172">각 커넥터 그룹마다 별도의 포리스트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-172">Each connector group represents a different forest.</span></span> <span data-ttu-id="746e7-173">테넌트와 대부분의 환경이 모든 포리스트에 대해 통합되지만 Azure AD 그룹을 사용하여 사용자를 포리스트 응용 프로그램에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-173">While the tenant and most of the experience is unified for all forests, users can be assigned to their forest applications using Azure AD groups.</span></span>
 
### <a name="disaster-recovery-sites"></a><span data-ttu-id="746e7-174">재해 복구 사이트</span><span class="sxs-lookup"><span data-stu-id="746e7-174">Disaster Recovery sites</span></span>

<span data-ttu-id="746e7-175">다음과 같이 사이트 구현 방법에 따라 DR(재해 복구) 사이트에서 수행할 수 있는 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-175">There are two different approaches you can take with a disaster recovery (DR) site, depending on how your sites are implemented:</span></span>

* <span data-ttu-id="746e7-176">DR 사이트가 주 사이트와 정확히 같고 네트워킹과 AD 설정이 동일한 활성-활성 모드로 만들어진 경우 주 사이트와 동일한 커넥터 그룹의 DR 사이트에 커넥터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-176">If your DR site is built in active-active mode where it is exactly like the main site and has the same networking and AD settings, you can create the connectors on the DR site in the same connector group as the main site.</span></span> <span data-ttu-id="746e7-177">이를 통해 Azure AD는 장애 복구를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-177">This enables Azure AD to detect failovers for you.</span></span>
* <span data-ttu-id="746e7-178">DR 사이트가 주 사이트와 별개인 경우 DR 사이트에 다른 커넥터 그룹을 만들고 필요에 따라 1) 백업 응용 프로그램을 만들거나 2) 수동으로 기존 응용 프로그램을 DR 커넥터 그룹으로 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-178">If your DR site is separate from the main site, you can create a different connector group in the DR site, and either 1) have backup applications or 2) manually divert the existing application to the DR connector group as needed.</span></span>
 
### <a name="serve-multiple-companies-from-a-single-tenant"></a><span data-ttu-id="746e7-179">단일 테넌트에서 여러 회사 제공</span><span class="sxs-lookup"><span data-stu-id="746e7-179">Serve multiple companies from a single tenant</span></span>

<span data-ttu-id="746e7-180">단일 서비스 공급자가 여러 회사에 Azure AD 관련 서비스를 배포하고 유지 관리하는 모델을 구현하는 방법에는 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-180">There are many different ways to implement a model in which a single service provider deploys and maintains Azure AD related services for multiple companies.</span></span> <span data-ttu-id="746e7-181">관리자가 커넥터와 응용 프로그램을 여러 그룹으로 분리하는 데 커넥터 그룹이 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-181">Connector groups help the admin segregate the connectors and applications into different groups.</span></span> <span data-ttu-id="746e7-182">소규모 회사에 적합한 한 가지 방법은 단일 Azure AD 테넌트를 보유하지만 다른 회사는 자체의 도메인 이름과 네트워크를 보유하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-182">One way, which is suitable for small companies, is to have a single Azure AD tenant while the different companies have their own domain name and networks.</span></span> <span data-ttu-id="746e7-183">또한 단일 IT 부서에서 규제 또는 비즈니스 상의 이유로 여러 회사에 서비스를 제공하는 M&A 시나리오 및 상황에서도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-183">This is also true for M&A scenarios and situations where a single IT division serves several companies for regulatory or business reasons.</span></span> 

## <a name="sample-configurations"></a><span data-ttu-id="746e7-184">샘플 구성</span><span class="sxs-lookup"><span data-stu-id="746e7-184">Sample configurations</span></span>

<span data-ttu-id="746e7-185">구현할 수 있는 몇 가지 예에는 다음 커넥터 그룹이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-185">Some examples that you can implement, include the following connector groups.</span></span>
 
### <a name="default-configuration--no-use-for-connector-groups"></a><span data-ttu-id="746e7-186">기본 구성 - 커넥터 그룹 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="746e7-186">Default configuration – no use for connector groups</span></span>

<span data-ttu-id="746e7-187">커넥터 그룹을 사용하지 않는 경우 구성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-187">If you don’t use connector groups, your configuration would look like this:</span></span>

![Azure AD - 커넥터 그룹 없음](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-1.png)
 
<span data-ttu-id="746e7-189">이 구성은 소규모 배포 및 테스트에 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-189">This configuration is sufficient for small deployments and tests.</span></span> <span data-ttu-id="746e7-190">또한 조직에 플랫 네트워크 토폴로지가 있는 경우에도 잘 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-190">It will also work well if your organization has a flat network topology.</span></span>
 
### <a name="default-configuration-and-an-isolated-network"></a><span data-ttu-id="746e7-191">기본 구성 및 격리된 네트워크</span><span class="sxs-lookup"><span data-stu-id="746e7-191">Default configuration and an isolated network</span></span>

<span data-ttu-id="746e7-192">이 구성은 기본 구성이 진화한 것으로, IaaS 가상 네트워크와 같이 격리된 네트워크에서 실행되는 특정 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-192">This configuration is an evolution of the default one, in which there is a specific app that runs in an isolated network such as IaaS virtual network:</span></span> 

![Azure AD - 커넥터 그룹 없음](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-2.png)
 
### <a name="recommended-configuration--several-specific-groups-and-a-default-group-for-idle"></a><span data-ttu-id="746e7-194">권장 구성 - 여러 특정 그룹 및 유휴 상태의 기본 그룹</span><span class="sxs-lookup"><span data-stu-id="746e7-194">Recommended configuration – several specific groups and a default group for idle</span></span>

<span data-ttu-id="746e7-195">크고 복잡한 조직에 권장되는 구성은 기본 커넥터 그룹을 어떤 응용 프로그램도 제공하지 않고 유휴 또는 새로 설치된 커넥터에 사용되는 그룹으로 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-195">The recommended configuration for large and complex organizations is to have the default connector group as a group that doesn’t serve any applications and is used for idle or newly installed connectors.</span></span> <span data-ttu-id="746e7-196">모든 응용 프로그램은 사용자 지정된 커넥터 그룹을 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-196">All applications are served using customized connector groups.</span></span> <span data-ttu-id="746e7-197">이렇게 하면 위에서 설명한 모든 시나리오의 복잡성을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-197">This enables all the complexity of the scenarios described above.</span></span>

<span data-ttu-id="746e7-198">아래 예에서는 회사에 두 개의 데이터 센터(A 및 B)가 있고 두 개의 커넥터에서 각 사이트를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-198">In the example below, the company has two datacenters, A and B, with two connectors that serve each site.</span></span> <span data-ttu-id="746e7-199">각 사이트에는 실행되는 다양한 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="746e7-199">Each site has different applications that run on it.</span></span> 

![Azure AD - 커넥터 그룹 없음](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-3.png)
 
## <a name="next-steps"></a><span data-ttu-id="746e7-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="746e7-201">Next steps</span></span>

* [<span data-ttu-id="746e7-202">Azure AD 응용 프로그램 프록시 커넥터 이해</span><span class="sxs-lookup"><span data-stu-id="746e7-202">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
* [<span data-ttu-id="746e7-203">Single Sign-On 사용</span><span class="sxs-lookup"><span data-stu-id="746e7-203">Enable single-sign on</span></span>](application-proxy-sso-overview.md)


