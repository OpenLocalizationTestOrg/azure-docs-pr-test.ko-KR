---
title: "Azure RemoteApp에 필요한 컬렉션의 종류는 무엇입니까? | Microsoft Docs"
description: "Azure RemoteApp과 함께 사용할 수 있는 컬렉션의 형식에 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c13ec78d-07e9-4646-8194-cf3efafc1760
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 10f6c0533027767b6635ebff1e6a9872bde06a68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="what-kind-of-collection-do-you-need-for-azure-remoteapp"></a><span data-ttu-id="1a963-104">Azure RemoteApp에 필요한 컬렉션의 종류는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="1a963-104">What kind of collection do you need for Azure RemoteApp?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1a963-105">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-105">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="1a963-106">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="1a963-106">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="1a963-107">Azure RemoteApp를 사용하면 어떠한 장치의 사용자와도 앱 및 리소스를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-107">Azure RemoteApp lets you share apps and resources with users on any device.</span></span> <span data-ttu-id="1a963-108">앱 및 리소스를 포함할 컬렉션을 만든 다음 해당 컬렉션을 사용자와 공유하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-108">We do this by creating collections to hold the apps and resources, and then you share those collections with users.</span></span> <span data-ttu-id="1a963-109">서로 다른 네트워크 및 인증 옵션을 사용하는 두 가지 컬렉션 옵션이 있습니다. 어느 옵션이 사용자에게 적합합니까?</span><span class="sxs-lookup"><span data-stu-id="1a963-109">There are 2 different collection options, with different network and authentication options - which is right for you?</span></span>

<span data-ttu-id="1a963-110">Azure RemoteApp 컬렉션을 최대한 활용하는 데 필요한 여러 가지 고려 사항과 선택을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-110">Let's walk through the different considerations and choices you need to make to get the most out of your Azure RemoteApp collection.</span></span> 

## <a name="quick-differences-between-the-collection-types"></a><span data-ttu-id="1a963-111">컬렉션 유형 간의 차이점 요약</span><span class="sxs-lookup"><span data-stu-id="1a963-111">Quick differences between the collection types</span></span>
|  | <span data-ttu-id="1a963-112">클라우드</span><span class="sxs-lookup"><span data-stu-id="1a963-112">Cloud</span></span> | <span data-ttu-id="1a963-113">하이브리드</span><span class="sxs-lookup"><span data-stu-id="1a963-113">Hybrid</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a963-114">기존 VNET 사용</span><span class="sxs-lookup"><span data-stu-id="1a963-114">Use an existing VNET</span></span> |<span data-ttu-id="1a963-115">예</span><span class="sxs-lookup"><span data-stu-id="1a963-115">Yes</span></span> |<span data-ttu-id="1a963-116">예</span><span class="sxs-lookup"><span data-stu-id="1a963-116">Yes</span></span> |
| <span data-ttu-id="1a963-117">AD에 연결된 계정(DirSync)이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-117">Requires AD-connected accounts (DirSync)</span></span> |<span data-ttu-id="1a963-118">아니요</span><span class="sxs-lookup"><span data-stu-id="1a963-118">No</span></span> |<span data-ttu-id="1a963-119">예</span><span class="sxs-lookup"><span data-stu-id="1a963-119">Yes</span></span> |
| <span data-ttu-id="1a963-120">도메인 가입이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-120">Requires domain join</span></span> |<span data-ttu-id="1a963-121">아니요</span><span class="sxs-lookup"><span data-stu-id="1a963-121">No</span></span> |<span data-ttu-id="1a963-122">예</span><span class="sxs-lookup"><span data-stu-id="1a963-122">Yes</span></span> |
| <span data-ttu-id="1a963-123">도메인 컨트롤러를 VNET에 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-123">Requires domain controller accessible to VNET</span></span> |<span data-ttu-id="1a963-124">아니요</span><span class="sxs-lookup"><span data-stu-id="1a963-124">No</span></span> |<span data-ttu-id="1a963-125">예</span><span class="sxs-lookup"><span data-stu-id="1a963-125">Yes</span></span> |

## <a name="cloud-collections"></a><span data-ttu-id="1a963-126">클라우드 컬렉션</span><span class="sxs-lookup"><span data-stu-id="1a963-126">Cloud collections</span></span>
* <span data-ttu-id="1a963-127">신속하게 만들기 - 컬렉션이 신속하게 프로비전되므로 앱이 사용자에게 더 빨리 다가갑니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-127">Quick to create - the collection is quickly provisioned, meaning your apps get to users quicker.</span></span>
* <span data-ttu-id="1a963-128">자신의 앱을 가져오거나 우리의 앱을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-128">Bring your own apps or share ours.</span></span> <span data-ttu-id="1a963-129">사용자 지정 이미지(Azure VM에서 빌드된) 또는 구독에 포함된 이미지 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-129">You can use a custom image (built from an Azure VM) or one of the images included with your subscription.</span></span>
* <span data-ttu-id="1a963-130">사용자의 컬렉션과 온-프레미스 도메인 사이의 연결을 구성하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-130">You don't need to configure a connection between your collection and your on-premises domain.</span></span>
* <span data-ttu-id="1a963-131">하지만 선택적으로 자기만의 Azure VNET를 사용하여 데이터 공유를 위해 온-프레미스 환경에 대한 액세스를 제공하거나 Windows 이외의 인증을 SQL Server 같은 리소스에 사용할 수 있습니다(데이터베이스 인증을 사용하여).</span><span class="sxs-lookup"><span data-stu-id="1a963-131">But you can optionally use your own Azure VNET to provide access into your on-premises environment for data sharing or to use non-Windows authentication into resources like SQL Server (using database authentication).</span></span>

<span data-ttu-id="1a963-132">그렇다면 어떻게 만드나요?</span><span class="sxs-lookup"><span data-stu-id="1a963-132">Ok, how do I create one?</span></span>

* <span data-ttu-id="1a963-133">클라우드 전용입니까?</span><span class="sxs-lookup"><span data-stu-id="1a963-133">Cloud only?</span></span> <span data-ttu-id="1a963-134">포털에서 **빠른 생성** 옵션으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-134">Create with the **Quick Create** option in the portal.</span></span>
* <span data-ttu-id="1a963-135">클라우드 + VNET입니까?</span><span class="sxs-lookup"><span data-stu-id="1a963-135">Cloud + VNET?</span></span> <span data-ttu-id="1a963-136">**VNET을 사용하여 만들기** 옵션을 사용하여 만들지만 도메인에 가입을 선택하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="1a963-136">Create using the **Create with VNET** option but do NOT choose to join a domain.</span></span>

## <a name="hybrid-collections"></a><span data-ttu-id="1a963-137">하이브리드 컬렉션</span><span class="sxs-lookup"><span data-stu-id="1a963-137">Hybrid collections</span></span>
* <span data-ttu-id="1a963-138">온-프레미스 네트워크 + Azure VNET에 대한 전체 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-138">Provide full access to on-premises network + Azure VNET.</span></span>
* <span data-ttu-id="1a963-139">앱 및 데이터에 대한 도메인 조인 액세스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-139">Includes domain join access for apps and data.</span></span> <span data-ttu-id="1a963-140">원격 응용 프로그램은 사용자의 온-프레미스 Active Directory에 대해 인증한 다음 사용자 도메인의 리소스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-140">Remote applications can authentication against your on-premises Active Directory - they can then access resources in your domain.</span></span>
* <span data-ttu-id="1a963-141">기존 시스템 센터 솔루션 및 Windows 그룹 정책을 사용하여 고급 모니터링 및 관리를 사용하도록 설정합니다(Windows Server 2012 R2에서 만든 사용자 지정 이미지를 통해).</span><span class="sxs-lookup"><span data-stu-id="1a963-141">Enable advanced monitoring and management with existing System Center solutions and Windows Group Policies (through a custom image built on Windows Server 2012 R2)</span></span>
* <span data-ttu-id="1a963-142">Azure VNET을 로컬 VNET에 연결하는 [Express 경로](https://azure.microsoft.com/services/expressroute/) 를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-142">Support [ExpressRoute](https://azure.microsoft.com/services/expressroute/) to connect your Azure VNET to your local VNET.</span></span>

<span data-ttu-id="1a963-143">**VNET을 사용하여 만들기** 옵션을 사용하여 만들고 도메인에 가입을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-143">Create using the **Create with VNET** option and DO choose to join a domain.</span></span>

## <a name="authentication-options"></a><span data-ttu-id="1a963-144">인증 옵션</span><span class="sxs-lookup"><span data-stu-id="1a963-144">Authentication options</span></span>
<span data-ttu-id="1a963-145">Azure RemoteApp은 Microsoft 계정과 Azure Active Directory 계정을 모두 지원하지만 일부 컬렉션은 일부 방법을 지원하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-145">Azure RemoteApp supports both Microsoft accounts and Azure Active Directory accounts, but not all collections support all methods.</span></span> 

| <span data-ttu-id="1a963-146">계정 유형</span><span class="sxs-lookup"><span data-stu-id="1a963-146">Account type</span></span> |  | <span data-ttu-id="1a963-147">클라우드</span><span class="sxs-lookup"><span data-stu-id="1a963-147">Cloud</span></span> | <span data-ttu-id="1a963-148">클라우드 + VNET</span><span class="sxs-lookup"><span data-stu-id="1a963-148">Cloud + VNET</span></span> | <span data-ttu-id="1a963-149">하이브리드</span><span class="sxs-lookup"><span data-stu-id="1a963-149">Hybrid</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="1a963-150">Microsoft 계정</span><span class="sxs-lookup"><span data-stu-id="1a963-150">Microsoft Account</span></span> | |<span data-ttu-id="1a963-151">예</span><span class="sxs-lookup"><span data-stu-id="1a963-151">Yes</span></span> |<span data-ttu-id="1a963-152">예</span><span class="sxs-lookup"><span data-stu-id="1a963-152">Yes</span></span> |<span data-ttu-id="1a963-153">아니요</span><span class="sxs-lookup"><span data-stu-id="1a963-153">No</span></span> |
| <span data-ttu-id="1a963-154">Azure AD(Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="1a963-154">Azure Active Directory (Azure AD)</span></span> | | | | |
| <span data-ttu-id="1a963-155">Azure AD만</span><span class="sxs-lookup"><span data-stu-id="1a963-155">Azure AD only</span></span> |<span data-ttu-id="1a963-156">예</span><span class="sxs-lookup"><span data-stu-id="1a963-156">Yes</span></span> |<span data-ttu-id="1a963-157">예</span><span class="sxs-lookup"><span data-stu-id="1a963-157">Yes</span></span> |<span data-ttu-id="1a963-158">아니요</span><span class="sxs-lookup"><span data-stu-id="1a963-158">No</span></span> | |
| <span data-ttu-id="1a963-159">암호 동기화를 사용하는 AD Connect</span><span class="sxs-lookup"><span data-stu-id="1a963-159">AD Connect with password sync</span></span> |<span data-ttu-id="1a963-160">예</span><span class="sxs-lookup"><span data-stu-id="1a963-160">Yes</span></span> |<span data-ttu-id="1a963-161">예</span><span class="sxs-lookup"><span data-stu-id="1a963-161">Yes</span></span> |<span data-ttu-id="1a963-162">예</span><span class="sxs-lookup"><span data-stu-id="1a963-162">Yes</span></span> | |
| <span data-ttu-id="1a963-163">암호 동기화를 사용하지 않는 AD Connect</span><span class="sxs-lookup"><span data-stu-id="1a963-163">AD Connect without password sync</span></span> |<span data-ttu-id="1a963-164">예</span><span class="sxs-lookup"><span data-stu-id="1a963-164">Yes</span></span> |<span data-ttu-id="1a963-165">예</span><span class="sxs-lookup"><span data-stu-id="1a963-165">Yes</span></span> |<span data-ttu-id="1a963-166">아니요</span><span class="sxs-lookup"><span data-stu-id="1a963-166">No</span></span> | |
| <span data-ttu-id="1a963-167">AD FS를 사용하는 AD Connect</span><span class="sxs-lookup"><span data-stu-id="1a963-167">AD Connect with AD FS</span></span> |<span data-ttu-id="1a963-168">예</span><span class="sxs-lookup"><span data-stu-id="1a963-168">Yes</span></span> |<span data-ttu-id="1a963-169">예</span><span class="sxs-lookup"><span data-stu-id="1a963-169">Yes</span></span> |<span data-ttu-id="1a963-170">예</span><span class="sxs-lookup"><span data-stu-id="1a963-170">Yes</span></span> | |
| <span data-ttu-id="1a963-171">타사 Azure 지원 ID 공급자(예: Ping)</span><span class="sxs-lookup"><span data-stu-id="1a963-171">3rd-party Azure-supported identity providers (such as Ping)</span></span> |<span data-ttu-id="1a963-172">예</span><span class="sxs-lookup"><span data-stu-id="1a963-172">Yes</span></span> |<span data-ttu-id="1a963-173">예</span><span class="sxs-lookup"><span data-stu-id="1a963-173">Yes</span></span> |<span data-ttu-id="1a963-174">예</span><span class="sxs-lookup"><span data-stu-id="1a963-174">Yes</span></span> | |
| <span data-ttu-id="1a963-175">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="1a963-175">Multi-Factor Authentication</span></span> | |<span data-ttu-id="1a963-176">예</span><span class="sxs-lookup"><span data-stu-id="1a963-176">Yes</span></span> |<span data-ttu-id="1a963-177">예</span><span class="sxs-lookup"><span data-stu-id="1a963-177">Yes</span></span> |<span data-ttu-id="1a963-178">예</span><span class="sxs-lookup"><span data-stu-id="1a963-178">Yes</span></span> |

### <a name="cloud-and-cloud--vnet"></a><span data-ttu-id="1a963-179">클라우드 및 클라우드 + VNET</span><span class="sxs-lookup"><span data-stu-id="1a963-179">Cloud and Cloud + VNET</span></span>
<span data-ttu-id="1a963-180">클라우드 컬렉션을 사용하면 Microsoft 계정, Azure AD 계정 또는 둘의 혼합을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-180">With cloud collections, you can use Microsoft accounts, Azure AD accounts, or a mix of the two.</span></span> <span data-ttu-id="1a963-181">사용자에게 가장 적합한 계정을 사 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-181">Use the accounts that work best for your users.</span></span>

<span data-ttu-id="1a963-182">Microsoft 계정을 사용하기 위한 특정 요구 사항이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-182">There are no specific requirements for using Microsoft accounts.</span></span> 

<span data-ttu-id="1a963-183">Azure AD 계정을 사용하려는 경우 Azure AD 테넌트가 구독에 연결된 테넌트와 일치하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-183">If you want to use Azure AD accounts, you need to make sure that your Azure AD tenant matches the one associated with your subscription.</span></span> <span data-ttu-id="1a963-184">Azure RemoteApp 구독을 만들 때 사용한 Azure AD 테넌트는 사용자의 구독에 자동으로 연결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-184">When you created your Azure RemoteApp subscription, the Azure AD tenant you were using was automatically associated with your subscription.</span></span> <span data-ttu-id="1a963-185">권한을 부여하는 모든 Azure AD 사용자는 같은 테넌트여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-185">Any Azure AD user you give permission to needs to be that same tenant.</span></span> <span data-ttu-id="1a963-186">필요한 경우 구독과 관련된 [Azure AD 테넌트를 변경](remoteapp-changetenant.md) 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-186">If needed, you can [change the Azure AD tenant](remoteapp-changetenant.md) associated with your subscription.</span></span>

### <a name="hybrid-or-cloud--azure-ad--ad"></a><span data-ttu-id="1a963-187">하이브리드(또는 클라우드 + Azure AD + AD)</span><span class="sxs-lookup"><span data-stu-id="1a963-187">Hybrid (or cloud + Azure AD + AD)</span></span>
<span data-ttu-id="1a963-188">Azure AD + 온-프레미스 Active Directory 사용은 하이브리드 컬렉션에 대한 전제 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-188">Using Azure AD + on-premises Active Directory is a prerequisite for a hybrid collection.</span></span> <span data-ttu-id="1a963-189">두 디렉터리를 통합하려면 AD Connect를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-189">You need to use AD Connect to integrate the two directories.</span></span> <span data-ttu-id="1a963-190">하지만 AD 연결을 구성하는 방법의 경우 몇 가지 선택이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-190">But you do have some choice when it comes to how you configure AD Connect.</span></span> 

<span data-ttu-id="1a963-191">암호 동기화 사용 또는 AD 페더레이션 사용 등 두 가지 AD Connect 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-191">There are 2 AD Connect scenarios - using password synchronization or using AD federation.</span></span> <span data-ttu-id="1a963-192">[AD Connect 정보](../active-directory/active-directory-aadconnect.md) 를 체크 아웃하여 둘 중 가장 적합한 시나리오를 알아냅니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-192">Check out the [AD Connect information](../active-directory/active-directory-aadconnect.md) to figure out which of these works best for you.</span></span>

<span data-ttu-id="1a963-193">또한 Azure AD + AD를 클라우드 컬렉션과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-193">You can also use Azure AD + AD with a cloud collection.</span></span> <span data-ttu-id="1a963-194">같은 설정 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-194">Make sure you follow the same set up steps.</span></span>

<span data-ttu-id="1a963-195">Azure AD 및 Active Directory를 구성하는 데 필요한 단계는 [Azure RemoteApp에 대한 Azure AD + Active Directory 요구 사항](remoteapp-ad.md) 을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="1a963-195">Check out [Azure AD + Active Directory requirements for Azure RemoteApp](remoteapp-ad.md) for the steps required to configure Azure AD and Active Directory.</span></span>

## <a name="go-create-your-collection"></a><span data-ttu-id="1a963-196">사용자의 컬렉션을 만드십시오!</span><span class="sxs-lookup"><span data-stu-id="1a963-196">Go create your collection!</span></span>
<span data-ttu-id="1a963-197">알겠습니다. 방법을 알았으므로 첫 번째 Azure RemoteApp 컬렉션을 만드는 한 가지만 남았습니다.</span><span class="sxs-lookup"><span data-stu-id="1a963-197">Ok, I think we've figured it out now, so there's just one thing left to do - create your first Azure RemoteApp collection.</span></span>

<span data-ttu-id="1a963-198">[클라우드 컬렉션 만들기](remoteapp-create-cloud-deployment.md) 또는 [하이브리드 컬렉션을 만들기](remoteapp-create-hybrid-deployment.md) - 그냥 만들어만 보세요!</span><span class="sxs-lookup"><span data-stu-id="1a963-198">[Create a cloud collection](remoteapp-create-cloud-deployment.md) or [create a hybrid collection](remoteapp-create-hybrid-deployment.md) - just get creating.</span></span>

