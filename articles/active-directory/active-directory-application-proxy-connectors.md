---
title: "클래식 포털 Azure AD 앱 프록시 커넥터 | Microsoft Docs"
description: "Azure AD 응용 프로그램 프록시에서 커넥터 그룹을 만들고 관리하는 방법에 대해 설명합니다."
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
ms.openlocfilehash: fc65c4053c45d9c16c62ee0fe65924133a4bb94a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a><span data-ttu-id="6fa1a-103">커넥터 그룹을 사용하여 별도의 네트워크 및 위치에서 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="6fa1a-103">Publish applications on separate networks and locations using connector groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6fa1a-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6fa1a-104">Azure portal</span></span>](active-directory-application-proxy-connectors-azure-portal.md)
> * [<span data-ttu-id="6fa1a-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="6fa1a-105">Azure classic portal</span></span>](active-directory-application-proxy-connectors.md)
>
>

<span data-ttu-id="6fa1a-106">커넥터 그룹은 다음을 비롯한 다양한 시나리오에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="6fa1a-106">Connector groups are useful for various scenarios, including:</span></span>

* <span data-ttu-id="6fa1a-107">여러 데이터 센터가 연결되어 있는 사이트.</span><span class="sxs-lookup"><span data-stu-id="6fa1a-107">Sites with multiple interconnected datacenters.</span></span> <span data-ttu-id="6fa1a-108">이 경우 데이터 센터 간 링크가 비용이 높고 느리기 때문에 가능한 한 데이터 센터 내에서 많은 트래픽을 유지하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fa1a-108">In this case, you want to keep as much traffic within the datacenter as possible because cross-datacenter links are expensive and slow.</span></span> <span data-ttu-id="6fa1a-109">각 데이터 센터에서 커넥터를 배포하여 데이터 센터 내에 있는 응용 프로그램만 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fa1a-109">You can deploy connectors in each datacenter to serve only the applications that reside within the datacenter.</span></span> <span data-ttu-id="6fa1a-110">이 방법은 데이터 센터 간 링크를 최소화하고 사용자에게 완전히 투명한 경험을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6fa1a-110">This approach minimizes cross-datacenter links and provides an entirely transparent experience to your users.</span></span>
* <span data-ttu-id="6fa1a-111">기본 회사 네트워크에 속하지 않은 격리된 네트워크에 설치된 응용 프로그램을 관리하는 경우.</span><span class="sxs-lookup"><span data-stu-id="6fa1a-111">Managing applications installed on isolated networks that are not part of the main corporate network.</span></span> <span data-ttu-id="6fa1a-112">커넥터 그룹을 사용하여 격리된 네트워크의 전용 커넥터를 설치하고 해당 네트워크에 응용 프로그램도 격리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fa1a-112">You can use connector groups to install dedicated connectors on isolated networks to also isolate applications to the network.</span></span>
* <span data-ttu-id="6fa1a-113">클라우드 액세스를 위해 IaaS에 설치된 응용 프로그램의 경우 커넥터 그룹은 모든 앱에 대한 액세스를 보호하는 일반적인 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6fa1a-113">For applications installed on IaaS for cloud access, connector groups provide a common service to secure the access to all the apps.</span></span> <span data-ttu-id="6fa1a-114">커넥터 그룹은 회사 네트워크에 추가 종속성을 만들거나 앱 경험을 조각화하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6fa1a-114">Connector groups don't create additional dependency on your corporate network, or fragment the app experience.</span></span> <span data-ttu-id="6fa1a-115">커넥터는 각 클라우드 데이터 센터에 설치될 수 있으며 이 네트워크에 있는 응용 프로그램만 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fa1a-115">Connectors can be installed on every cloud datacenter and serve only applications that reside in this network.</span></span> <span data-ttu-id="6fa1a-116">고가용성을 얻기 위해 커넥터를 여러 개 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fa1a-116">You can install several connectors to achieve high availability.</span></span>
* <span data-ttu-id="6fa1a-117">특정 커넥터가 포리스트별로 배포되고 특정 응용 프로그램을 처리하도록 설정될 수 있는 다중 포리스트 환경에 대한 지원.</span><span class="sxs-lookup"><span data-stu-id="6fa1a-117">Support for multi-forest environments in which specific connectors can be deployed per forest and set to serve specific applications.</span></span>
* <span data-ttu-id="6fa1a-118">커넥터 그룹은 재해 복구 사이트에서 장애 조치(failover)를 감지하는 데 사용하거나 기본 사이트의 백업으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fa1a-118">Connector groups can be used in Disaster Recovery sites to either detect failover or as backup for the main site.</span></span>
* <span data-ttu-id="6fa1a-119">커넥터 그룹은 단일 테넌트에서 여러 회사를 처리하는 데도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fa1a-119">Connector groups can also be used to serve multiple companies from a single tenant.</span></span>

## <a name="prerequisite-create-your-connectors"></a><span data-ttu-id="6fa1a-120">필수 조건: 커넥터 만들기</span><span class="sxs-lookup"><span data-stu-id="6fa1a-120">Prerequisite: Create your connectors</span></span>
<span data-ttu-id="6fa1a-121">커넥터를 그룹화하려면 [여러 커넥터를 설치](active-directory-application-proxy-enable.md)한 후 이름을 지정하고 그룹화합니다.</span><span class="sxs-lookup"><span data-stu-id="6fa1a-121">To group your connectors, [install multiple connectors](active-directory-application-proxy-enable.md), then name and group them.</span></span> <span data-ttu-id="6fa1a-122">마지막으로 특정 앱에 커넥터를 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fa1a-122">Finally you have to assign them to specific apps.</span></span>

## <a name="step-1-create-connector-groups"></a><span data-ttu-id="6fa1a-123">1단계: 커넥터 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="6fa1a-123">Step 1: Create connector groups</span></span>
<span data-ttu-id="6fa1a-124">원하는 수 만큼 커넥터 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fa1a-124">You can create as many connector groups as you want.</span></span> <span data-ttu-id="6fa1a-125">커넥터 그룹은 Azure 클래식 포털에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fa1a-125">Connector group creation is accomplished in the Azure classic portal.</span></span>

1. <span data-ttu-id="6fa1a-126">디렉터리를 선택하고 **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6fa1a-126">Select your directory and click **Configure**.</span></span>  
    <span data-ttu-id="6fa1a-127">![응용 프로그램 프록시 구성 스크린샷 - 커넥터 그룹 관리 클릭](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span><span class="sxs-lookup"><span data-stu-id="6fa1a-127">![Application proxy, configure screenshot - click manage connector groups](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span></span>
2. <span data-ttu-id="6fa1a-128">응용 프로그램 프록시에서 **커넥터 그룹 관리**를 클릭하고 그룹에 이름을 지정하여 커넥터 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6fa1a-128">Under Application Proxy, click **Manage Connector Groups** and create a connector group by giving the group a name.</span></span>  
    <span data-ttu-id="6fa1a-129">![응용 프로그램 프록시 커넥터 그룹 스크린샷 - 새 그룹 이름 지정](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span><span class="sxs-lookup"><span data-stu-id="6fa1a-129">![Application proxy connector groups screenshot - name new group](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span></span>

## <a name="step-2-assign-connectors-to-your-groups"></a><span data-ttu-id="6fa1a-130">2단계: 그룹에 커넥터 할당</span><span class="sxs-lookup"><span data-stu-id="6fa1a-130">Step 2: Assign connectors to your groups</span></span>
<span data-ttu-id="6fa1a-131">커넥터 그룹이 만들어지면 해당 그룹에 커넥터를 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6fa1a-131">Once the connector groups are created, move the connectors to the appropriate group.</span></span>

1. <span data-ttu-id="6fa1a-132">**응용 프로그램 프록시**에서 **커넥터 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6fa1a-132">Under **Application Proxy**, click **Manage Connectors**.</span></span>
2. <span data-ttu-id="6fa1a-133">**그룹**에서 각 커넥터에 대해 원하는 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6fa1a-133">Under **Group**, select the group you want for each connector.</span></span> <span data-ttu-id="6fa1a-134">커넥터가 새 그룹에서 활성화되는 데 최대 10분까지 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fa1a-134">It might take the connectors up to 10 minutes to become active in the new group.</span></span>  
    <span data-ttu-id="6fa1a-135">![응용 프로그램 프록시 커넥터 스크린샷 - 드롭다운 메뉴에서 그룹 선택](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span><span class="sxs-lookup"><span data-stu-id="6fa1a-135">![Application proxy connectors screenshot - select group from dropdown menu](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span></span>

## <a name="step-3-assign-applications-to-your-connector-groups"></a><span data-ttu-id="6fa1a-136">3단계: 커넥터 그룹에 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="6fa1a-136">Step 3: Assign applications to your connector groups</span></span>
<span data-ttu-id="6fa1a-137">마지막 단계는 각 응용 프로그램을 해당 응용 프로그램을 처리할 커넥터 그룹에 할당하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6fa1a-137">The last step is to set each application to the connector group that serves it.</span></span>

1. <span data-ttu-id="6fa1a-138">Azure 클래식 포털의 해당 디렉터리에서 그룹에 할당할 응용 프로그램을 선택하고 **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6fa1a-138">In the Azure classic portal, in your directory, select the Application you want to assign to the group and click **Configure**.</span></span>
2. <span data-ttu-id="6fa1a-139">**커넥터 그룹**에서 응용 프로그램에서 사용할 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6fa1a-139">Under **Connector group**, select the group you want the application to use.</span></span> <span data-ttu-id="6fa1a-140">이 변경은 즉시 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fa1a-140">This change is immediately applied.</span></span>  
    <span data-ttu-id="6fa1a-141">![응용 프로그램 프록시 커넥터 그룹 스크린샷 - 드롭다운 메뉴에서 그룹 선택](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span><span class="sxs-lookup"><span data-stu-id="6fa1a-141">![Application proxy connector group screenshot - select group from dropdown menu](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span></span>

## <a name="see-also"></a><span data-ttu-id="6fa1a-142">참고 항목</span><span class="sxs-lookup"><span data-stu-id="6fa1a-142">See also</span></span>
* [<span data-ttu-id="6fa1a-143">응용 프로그램 프록시 사용</span><span class="sxs-lookup"><span data-stu-id="6fa1a-143">Enable Application Proxy</span></span>](active-directory-application-proxy-enable.md)
* [<span data-ttu-id="6fa1a-144">Single Sign-On 사용</span><span class="sxs-lookup"><span data-stu-id="6fa1a-144">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="6fa1a-145">조건부 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="6fa1a-145">Enable conditional access</span></span>](active-directory-application-proxy-conditional-access.md)
* [<span data-ttu-id="6fa1a-146">응용 프로그램 프록시에서 발생한 문제 해결</span><span class="sxs-lookup"><span data-stu-id="6fa1a-146">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)

<span data-ttu-id="6fa1a-147">최신 뉴스 및 업데이트는 [응용 프로그램 프록시 블로그](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="6fa1a-147">For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
