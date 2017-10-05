---
title: Azure Active Directory Connect Health FAQ - Azure | Microsoft Docs
description: "이 FAQ는 Azure AD Connect Health에 대한 질문에 답변합니다. 이 FAQ는 요금 청구 모델, 기능, 제한 및 지원을 포함한 서비스 사용에 대한 질문을 다룹니다."
services: active-directory
documentationcenter: 
author: billmath
manager: samueld
editor: curtand
ms.assetid: f1b851aa-54d7-4cb4-8f5c-60680e2ce866
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 902e5bdfbbf04ab70989be8c41e16eb69e475908
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-health-frequently-asked-questions"></a><span data-ttu-id="3c043-104">Azure AD Connect Health에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="3c043-104">Azure AD Connect Health frequently asked questions</span></span>
<span data-ttu-id="3c043-105">이 문서에는 Azure AD(Azure Active Directory) Connect Health에 대한 FAQ(질문과 대답)가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-105">This article includes answers to frequently asked questions (FAQs) about Azure Active Directory (Azure AD) Connect Health.</span></span> <span data-ttu-id="3c043-106">이 FAQ에서는 청구 모델, 기능, 제한 및 지원을 포함한 서비스 사용 방법에 대해 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-106">These FAQs cover questions about how to use the service, which includes the billing model, capabilities, limitations, and support.</span></span>

## <a name="general-questions"></a><span data-ttu-id="3c043-107">일반적인 질문</span><span class="sxs-lookup"><span data-stu-id="3c043-107">General questions</span></span>
<span data-ttu-id="3c043-108">**Q: 여러 Azure AD 디렉터리를 관리합니다. Azure Active Directory Premium을 사용하는 디렉터리로 전환하려면 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="3c043-108">**Q: I manage multiple Azure AD directories. How do I switch to the one that has Azure Active Directory Premium?**</span></span>

<span data-ttu-id="3c043-109">오른쪽 위 모서리에 있는 현재 로그인한 **사용자 이름**을 선택하고 적절한 계정을 선택하면 여러 Azure AD 테넌트 간에 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-109">To switch between different Azure AD tenants, select the currently signed-in **User Name** on the upper-right corner, and then choose the appropriate account.</span></span> <span data-ttu-id="3c043-110">계정이 여기에 나열되어 있지 않으면 **로그아웃**을 선택한 다음 Azure Active Directory Premium을 사용하도록 설정된 디렉터리의 글로벌 관리자 자격 증명을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-110">If the account is not listed here, select **Sign out**, and then use the global admin credentials of the directory that has Azure Active Directory Premium enabled to sign in.</span></span>

<span data-ttu-id="3c043-111">**Q: Azure AD Connect Health에서 어떤 버전의 ID 역할을 지원하나요?**</span><span class="sxs-lookup"><span data-stu-id="3c043-111">**Q: What version of identity roles are supported by Azure AD Connect Health?**</span></span>

<span data-ttu-id="3c043-112">다음 테이블에는 역할 및 지원되는 운영 체제 버전이 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-112">The following table lists the roles and supported operating system versions.</span></span>

|<span data-ttu-id="3c043-113">역할</span><span class="sxs-lookup"><span data-stu-id="3c043-113">Role</span></span>| <span data-ttu-id="3c043-114">운영 체제/버전</span><span class="sxs-lookup"><span data-stu-id="3c043-114">Operating system / Version</span></span>|
|--|--|
|<span data-ttu-id="3c043-115">AD FS(Active Directory Federation Services)</span><span class="sxs-lookup"><span data-stu-id="3c043-115">Active Directory Federation Services (AD FS)</span></span>| <ul> <li> <span data-ttu-id="3c043-116">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="3c043-116">Windows Server 2008 R2</span></span> </li><li> <span data-ttu-id="3c043-117">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="3c043-117">Windows Server 2012</span></span>  </li> <li><span data-ttu-id="3c043-118">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="3c043-118">Windows Server 2012 R2</span></span> </li> <li> <span data-ttu-id="3c043-119">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="3c043-119">Windows Server 2016</span></span>  </li> </ul>|
|<span data-ttu-id="3c043-120">Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="3c043-120">Azure AD Connect</span></span> | <span data-ttu-id="3c043-121">버전 1.0.9125 이상</span><span class="sxs-lookup"><span data-stu-id="3c043-121">Version 1.0.9125 or higher</span></span>|
|<span data-ttu-id="3c043-122">AD DS(Active Directory Domain Services)</span><span class="sxs-lookup"><span data-stu-id="3c043-122">Active Directory Domain Services (AD DS)</span></span>| <ul> <li> <span data-ttu-id="3c043-123">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="3c043-123">Windows Server 2008 R2</span></span> </li><li> <span data-ttu-id="3c043-124">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="3c043-124">Windows Server 2012</span></span>  </li> <li><span data-ttu-id="3c043-125">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="3c043-125">Windows Server 2012 R2</span></span> </li> <li> <span data-ttu-id="3c043-126">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="3c043-126">Windows Server 2016</span></span>  </li> </ul>|

<span data-ttu-id="3c043-127">서비스에서 제공하는 기능은 역할 및 운영 체제에 따라 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-127">Note that the features provided by the service may differ based on the role and the operating system.</span></span> <span data-ttu-id="3c043-128">즉, 운영 체제 버전에 따라 일부 기능이 제공되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-128">In other words, all the features may not be available for all operating system versions.</span></span> <span data-ttu-id="3c043-129">자세한 내용은 기능 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c043-129">See the feature descriptions for details.</span></span>

<span data-ttu-id="3c043-130">**Q: 내 인프라를 모니터링하려면 라이선스가 몇 개 필요한가요?**</span><span class="sxs-lookup"><span data-stu-id="3c043-130">**Q: How many licenses do I need to monitor my infrastructure?**</span></span>

* <span data-ttu-id="3c043-131">첫 번째 Connect Health 에이전트에는 하나 이상의 Azure AD Premium 라이선스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-131">The first Connect Health Agent requires at least one Azure AD Premium license.</span></span>
* <span data-ttu-id="3c043-132">등록된 추가 에이전트에는 각각 25개의 추가 Azure AD Premium 라이선스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-132">Each additional registered agent requires 25 additional Azure AD Premium licenses.</span></span>
* <span data-ttu-id="3c043-133">에이전트 수는 모든 모니터링된 역할(AD FS, Azure AD Connect 및/또는 AD DS)에 등록된 에이전트의 총 수와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-133">Agent count is equivalent to the total number of agents that are registered across all monitored roles (AD FS, Azure AD Connect, and/or AD DS).</span></span>

<span data-ttu-id="3c043-134">라이선스 정보는 [Azure AD 가격 책정 페이지](https://aka.ms/aadpricing)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-134">Licensing information is also found on the [Azure AD Pricing page](https://aka.ms/aadpricing).</span></span>

<span data-ttu-id="3c043-135">예제:</span><span class="sxs-lookup"><span data-stu-id="3c043-135">Example:</span></span>

| <span data-ttu-id="3c043-136">등록된 에이전트</span><span class="sxs-lookup"><span data-stu-id="3c043-136">Registered agents</span></span> | <span data-ttu-id="3c043-137">필요한 라이선스</span><span class="sxs-lookup"><span data-stu-id="3c043-137">Licenses needed</span></span> | <span data-ttu-id="3c043-138">모니터링 구성 예제</span><span class="sxs-lookup"><span data-stu-id="3c043-138">Example monitoring configuration</span></span> |
| ------ | --------------- | --- |
| <span data-ttu-id="3c043-139">1</span><span class="sxs-lookup"><span data-stu-id="3c043-139">1</span></span> | <span data-ttu-id="3c043-140">1</span><span class="sxs-lookup"><span data-stu-id="3c043-140">1</span></span> | <span data-ttu-id="3c043-141">Azure AD Connect 서버 1개</span><span class="sxs-lookup"><span data-stu-id="3c043-141">1 Azure AD Connect server</span></span> |
| <span data-ttu-id="3c043-142">2</span><span class="sxs-lookup"><span data-stu-id="3c043-142">2</span></span> | <span data-ttu-id="3c043-143">26</span><span class="sxs-lookup"><span data-stu-id="3c043-143">26</span></span>| <span data-ttu-id="3c043-144">Azure AD Connect 서버 1개 및 도메인 컨트롤러 1개</span><span class="sxs-lookup"><span data-stu-id="3c043-144">1 Azure AD Connect server and 1 domain controller</span></span> |
| <span data-ttu-id="3c043-145">3</span><span class="sxs-lookup"><span data-stu-id="3c043-145">3</span></span> | <span data-ttu-id="3c043-146">51</span><span class="sxs-lookup"><span data-stu-id="3c043-146">51</span></span> | <span data-ttu-id="3c043-147">AD FS(Active Directory Federation Services) 서버 1개, AD FS 프록시 1개, 도메인 컨트롤러 1개</span><span class="sxs-lookup"><span data-stu-id="3c043-147">1 Active Directory Federation Services (AD FS) server, 1 AD FS proxy, and 1 domain controller</span></span> |
| <span data-ttu-id="3c043-148">4</span><span class="sxs-lookup"><span data-stu-id="3c043-148">4</span></span> | <span data-ttu-id="3c043-149">76</span><span class="sxs-lookup"><span data-stu-id="3c043-149">76</span></span> | <span data-ttu-id="3c043-150">AD FS 서버 1개, AD FS 프록시 1개, 도메인 컨트롤러 2개</span><span class="sxs-lookup"><span data-stu-id="3c043-150">1 AD FS server, 1 AD FS proxy, and 2 domain controllers</span></span> |
| <span data-ttu-id="3c043-151">5</span><span class="sxs-lookup"><span data-stu-id="3c043-151">5</span></span> | <span data-ttu-id="3c043-152">101</span><span class="sxs-lookup"><span data-stu-id="3c043-152">101</span></span> | <span data-ttu-id="3c043-153">Azure AD Connect 서버 1개, AD FS 서버 1개, AD FS 프록시 1개, 도메인 컨트롤러 2개</span><span class="sxs-lookup"><span data-stu-id="3c043-153">1 Azure AD Connect server, 1 AD FS server, 1 AD FS proxy, and 2 domain controllers</span></span> |


## <a name="installation-questions"></a><span data-ttu-id="3c043-154">설치 관련 질문</span><span class="sxs-lookup"><span data-stu-id="3c043-154">Installation questions</span></span>

<span data-ttu-id="3c043-155">**Q: 개별 서버에 Azure AD Connect Health Agent를 설치하면 어떤 영향이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="3c043-155">**Q: What is the impact of installing the Azure AD Connect Health Agent on individual servers?**</span></span>

<span data-ttu-id="3c043-156">Microsoft Azure AD Connect Health 에이전트, AD FS, 웹 응용 프로그램 프록시 서버, Azure AD Connect(sycn) 서버, 도메인 컨트롤러를 설치해도 CPU, 메모리 사용량, 네트워크 대역폭 및 저장소에는 최소한의 영향만 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-156">The impact of installing the Microsoft Azure AD Connect Health Agent, AD FS, web application proxy servers, Azure AD Connect (sync) servers, domain controllers is minimal with respect to the CPU, memory consumption, network bandwidth, and storage.</span></span>

<span data-ttu-id="3c043-157">다음 숫자는 근사값입니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-157">The following numbers are an approximation:</span></span>

* <span data-ttu-id="3c043-158">CPU 사용량: 1-5% 증가</span><span class="sxs-lookup"><span data-stu-id="3c043-158">CPU consumption: ~1-5% increase.</span></span>
* <span data-ttu-id="3c043-159">메모리 사용량: 전체 시스템 메모리의 최대 10%</span><span class="sxs-lookup"><span data-stu-id="3c043-159">Memory consumption: Up to 10 % of the total system memory.</span></span>

> [!NOTE]
> <span data-ttu-id="3c043-160">에이전트가 Azure와 통신할 수 없는 경우 에이전트는 정의된 최대 한도까지 데이터를 로컬로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-160">If the agent cannot communicate with Azure, the agent stores the data locally for a defined maximum limit.</span></span> <span data-ttu-id="3c043-161">Agent는 "최소 최근 서비스" 단위로 "캐시된" 데이터를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-161">The agent overwrites the “cached” data on a “least recently serviced” basis.</span></span>
>
>

* <span data-ttu-id="3c043-162">Azure AD Connect Health 에이전트의 로컬 버퍼 저장소: ~20MB.</span><span class="sxs-lookup"><span data-stu-id="3c043-162">Local buffer storage for Azure AD Connect Health Agents: ~20 MB.</span></span>
* <span data-ttu-id="3c043-163">AD FS 서버의 경우 모든 감사 데이터를 덮어쓰기 전에 처리하려면 Azure AD Connect Health 에이전트의 AD FS 감사 채널에 1,024MB(1GB)의 디스크 공간을 프로비전하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-163">For AD FS servers, we recommend that you provision a disk space of 1,024 MB (1 GB) for the AD FS audit channel for Azure AD Connect Health Agents to process all the audit data before it is overwritten.</span></span>

<span data-ttu-id="3c043-164">**Q: Azure AD Connect Health Agent를 설치하는 동안 내 서버를 재부팅해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="3c043-164">**Q: Will I have to reboot my servers during the installation of the Azure AD Connect Health Agents?**</span></span>

<span data-ttu-id="3c043-165">아니요.</span><span class="sxs-lookup"><span data-stu-id="3c043-165">No.</span></span> <span data-ttu-id="3c043-166">에이전트를 설치하는 데 서버를 재부팅할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-166">The installation of the agents will not require you to reboot the server.</span></span> <span data-ttu-id="3c043-167">그러나 일부 필수 구성 요소 설치 단계에서 서버를 재부팅해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-167">However, installation of some prerequisite steps might require a reboot of the server.</span></span>

<span data-ttu-id="3c043-168">예를 들어 Windows Server 2008 R2에 .NET 4.5 Framework를 설치하는 경우 서버를 재부팅해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-168">For example, on Windows Server 2008 R2, installation of .NET 4.5 Framework requires a server reboot.</span></span>

<span data-ttu-id="3c043-169">**Q: Azure AD Connect Health는 통과 HTTP 프록시를 통해 작동하나요?**</span><span class="sxs-lookup"><span data-stu-id="3c043-169">**Q: Does Azure AD Connect Health work through a pass-through HTTP proxy?**</span></span>

<span data-ttu-id="3c043-170">예.</span><span class="sxs-lookup"><span data-stu-id="3c043-170">Yes.</span></span> <span data-ttu-id="3c043-171">진행 중인 작업의 경우 HTTP 프록시를 사용하여 아웃바운드 http 요청을 전달하도록 Health Agent를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-171">For ongoing operations, you can configure the Health Agent to use an HTTP proxy to forward outbound HTTP requests.</span></span>
<span data-ttu-id="3c043-172">[Health 에이전트에 대한 HTTP 프록시 구성](active-directory-aadconnect-health-agent-install.md#configure-azure-ad-connect-health-agents-to-use-http-proxy)을 자세히 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="3c043-172">Read more about [configuring HTTP Proxy for Health Agents](active-directory-aadconnect-health-agent-install.md#configure-azure-ad-connect-health-agents-to-use-http-proxy).</span></span>

<span data-ttu-id="3c043-173">에이전트를 등록하는 동안 프록시를 구성해야 하는 경우 Internet Explorer 프록시 설정을 미리 수정해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-173">If you need to configure a proxy during agent registration, you might need to modify your Internet Explorer Proxy settings beforehand.</span></span>

1. <span data-ttu-id="3c043-174">Internet Explorer > **설정** > **인터넷 옵션** > **연결** > **LAN 설정**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-174">Open Internet Explorer > **Settings** > **Internet Options** > **Connections** > **LAN Settings**.</span></span>
2. <span data-ttu-id="3c043-175">**사용자 LAN의 프록시 서버 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-175">Select **Use a Proxy Server for your LAN**.</span></span>
3. <span data-ttu-id="3c043-176">HTTP 및 HTTPS/보안의 프록시 포트가 다른 경우 **고급**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-176">Select **Advanced** if you have different proxy ports for HTTP and HTTPS/Secure.</span></span>

<span data-ttu-id="3c043-177">**Q: Azure AD Connect Health는 HTTP 프록시에 연결할 때 기본 인증을 지원하나요?**</span><span class="sxs-lookup"><span data-stu-id="3c043-177">**Q: Does Azure AD Connect Health support Basic authentication when connecting to HTTP proxies?**</span></span>

<span data-ttu-id="3c043-178">아니요.</span><span class="sxs-lookup"><span data-stu-id="3c043-178">No.</span></span> <span data-ttu-id="3c043-179">기본 인증에 필요한 임의 사용자 이름/암호를 지정하는 메커니즘은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-179">A mechanism to specify an arbitrary user name and password for Basic authentication is not currently supported.</span></span>

<span data-ttu-id="3c043-180">**Q: Azure AD Connect Health Agent가 작동하도록 하기 위해 열어야 하는 방화벽 포트는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="3c043-180">**Q: What firewall ports do I need to open for the Azure AD Connect Health Agent to work?**</span></span>

<span data-ttu-id="3c043-181">방화벽 포트 및 기타 연결 요구 사항 목록은 [요구 사항 섹션](active-directory-aadconnect-health-agent-install.md#requirements)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c043-181">See the [requirements section](active-directory-aadconnect-health-agent-install.md#requirements) for the list of firewall ports and other connectivity requirements.</span></span>

<span data-ttu-id="3c043-182">**Q: Azure AD Connect Health 포털에 같은 이름을 가진 두 대의 서버가 표시되는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="3c043-182">**Q: Why do I see two servers with the same name in the Azure AD Connect Health portal?**</span></span>

<span data-ttu-id="3c043-183">서버에서 에이전트를 제거해도 해당 서버가 Azure AD Connect Health 포털에서 자동으로 제거되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-183">When you remove an agent from a server, the server is not automatically removed from the Azure AD Connect Health portal.</span></span> <span data-ttu-id="3c043-184">서버에서 에이전트를 수동으로 제거하거나 서버 자체를 제거한 경우 Azure AD Connect Health 포털에서 서버 항목을 수동으로 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-184">If you manually remove an agent from a server or remove the server itself, you need to manually delete the server entry from the Azure AD Connect Health portal.</span></span>

<span data-ttu-id="3c043-185">서버를 이미지로 다시 설치하거나 같은 세부 정보(예: 컴퓨터 이름)를 사용하여 새 서버를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-185">You might reimage a server or create a new server with the same details (such as machine name).</span></span> <span data-ttu-id="3c043-186">Azure AD Connect Health 포털에서 이미 등록된 서버를 제거하지 않고 새 서버에 에이전트를 설치하면 이름이 같은 두 개의 항목이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-186">If you did not remove the already registered server from the Azure AD Connect Health portal, and you installed the agent on the new server, you might see two entries with the same name.</span></span>

<span data-ttu-id="3c043-187">이 경우 이전 서버에 소속된 항목을 수동으로 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-187">In this case, manually delete the entry that belongs to the older server.</span></span> <span data-ttu-id="3c043-188">이 서버에 대한 데이터는 오래된 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-188">The data for this server should be out of date.</span></span>

## <a name="health-agent-registration-and-data-freshness"></a><span data-ttu-id="3c043-189">Health Agent 등록 및 데이터 새로 고침</span><span class="sxs-lookup"><span data-stu-id="3c043-189">Health Agent registration and data freshness</span></span>

<span data-ttu-id="3c043-190">**Q: Health Agent 등록 오류가 발생하는 일반적인 원인은 무엇이며 어떻게 해결해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="3c043-190">**Q: What are common reasons for the Health Agent registration failures and how do I troubleshoot issues?**</span></span>

<span data-ttu-id="3c043-191">Health Agent는 다음과 같은 원인으로 등록에 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-191">The health agent can fail to register due to the following possible reasons:</span></span>

* <span data-ttu-id="3c043-192">방화벽이 트래픽을 차단하고 있어서 에이전트가 필수 끝점과 통신할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-192">The agent cannot communicate with the required endpoints because a firewall is blocking traffic.</span></span> <span data-ttu-id="3c043-193">특히 웹 응용 프로그램 프록시 서버에서 자주 발생하는 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-193">This is particularly common on web application proxy servers.</span></span> <span data-ttu-id="3c043-194">필수 끝점 및 포트에 아웃바운드 통신을 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-194">Make sure that you have allowed outbound communication to the required endpoints and ports.</span></span> <span data-ttu-id="3c043-195">자세한 내용은 [요구 사항 섹션](active-directory-aadconnect-health-agent-install.md#requirements)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c043-195">See the [requirements section](active-directory-aadconnect-health-agent-install.md#requirements) for details.</span></span>
* <span data-ttu-id="3c043-196">아웃바운드 통신은 네트워크 계층에서 SSL 검사를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-196">Outbound communication is subjected to an SSL inspection by the network layer.</span></span> <span data-ttu-id="3c043-197">이로 인해 에이전트에서 사용하는 인증서가 검사 서버/엔터티로 교체되고, 에이전트 등록을 완료하는 단계가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-197">This causes the certificate that the agent uses to be replaced by the inspection server/entity, and the steps to complete the agent registration fail.</span></span>
* <span data-ttu-id="3c043-198">사용자는 에이전트의 등록을 수행하기 위한 액세스 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-198">The user does not have access to perform the registration of the agent.</span></span> <span data-ttu-id="3c043-199">전역 관리자는 기본적으로 액세스 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-199">Global admins have access by default.</span></span> <span data-ttu-id="3c043-200">[역할 기반 액세스 제어](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control)를 사용하여 다른 사용자에 대한 액세스를 위임할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-200">You can use [Role Based Access Control](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control) to delegate access to other users.</span></span>

<span data-ttu-id="3c043-201">**Q: "Health Service 데이터가 최신 상태가 아닙니다."라는 경고가 표시됩니다. 이 문제를 어떻게 해결하나요?**</span><span class="sxs-lookup"><span data-stu-id="3c043-201">**Q: I am getting alerted that "Health Service data is not up to date." How do I troubleshoot the issue?**</span></span>

<span data-ttu-id="3c043-202">Azure AD Connect Health는 2시간 동안 서버에서 데이터 지점을 수신하지 않으면 이 경고를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-202">Azure AD Connect Health generates the alert when it does not receive all the data points from the server in the last two hours.</span></span> <span data-ttu-id="3c043-203">이 경고가 발생하는 여러 이유가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-203">There can be multiple reasons for this alert.</span></span>

* <span data-ttu-id="3c043-204">방화벽이 트래픽을 차단하고 있어서 에이전트가 필수 끝점과 통신할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-204">The agent cannot communicate with the required endpoints because a firewall is blocking traffic.</span></span> <span data-ttu-id="3c043-205">특히 웹 응용 프로그램 프록시 서버에서 자주 발생하는 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-205">This is particularly common on web application proxy servers.</span></span> <span data-ttu-id="3c043-206">필수 끝점 및 포트에 아웃바운드 통신을 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-206">Make sure that you have allowed outbound communication to the required end points and ports.</span></span> <span data-ttu-id="3c043-207">자세한 내용은 [요구 사항 섹션](active-directory-aadconnect-health-agent-install.md#requirements)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c043-207">See the [requirements section](active-directory-aadconnect-health-agent-install.md#requirements) for details.</span></span>
* <span data-ttu-id="3c043-208">아웃바운드 통신은 네트워크 계층에서 SSL 검사를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-208">Outbound communication is subjected to an SSL inspection by the network layer.</span></span> <span data-ttu-id="3c043-209">이로 인해 에이전트에서 사용하는 인증서가 검사 서버/엔터티로 교체되고, Azure AD Connect Health 서비스로 데이터를 업로드하는 프로세스가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-209">This causes the certificate that the agent uses to be replaced by the inspection server/entity, and the process fails to upload data to the Azure AD Connect Health service.</span></span>
* <span data-ttu-id="3c043-210">에이전트에 기본 제공된 연결 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-210">You can use the connectivity command built into the agent.</span></span> <span data-ttu-id="3c043-211">[자세히 알아보기](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service).</span><span class="sxs-lookup"><span data-stu-id="3c043-211">[Read more](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service).</span></span>
* <span data-ttu-id="3c043-212">또한 에이전트는 인증되지 않은 HTTP 프록시를 통해 아웃바운드 연결을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-212">The agents also support outbound connectivity via an unauthenticated HTTP Proxy.</span></span> <span data-ttu-id="3c043-213">[자세히 알아보기](active-directory-aadconnect-health-agent-install.md##configure-azure-ad-connect-health-agents-to-use-http-proxy).</span><span class="sxs-lookup"><span data-stu-id="3c043-213">[Read more](active-directory-aadconnect-health-agent-install.md##configure-azure-ad-connect-health-agents-to-use-http-proxy).</span></span>

## <a name="operations-questions"></a><span data-ttu-id="3c043-214">작업 관련 질문</span><span class="sxs-lookup"><span data-stu-id="3c043-214">Operations questions</span></span>
<span data-ttu-id="3c043-215">**Q: 웹 응용 프로그램 프록시 서버에 대한 감사를 사용하도록 설정해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="3c043-215">**Q: Do I need to enable auditing on the web application proxy servers?**</span></span>

<span data-ttu-id="3c043-216">아니요, 웹 응용 프로그램 프록시 서버에서 감사를 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-216">No, auditing does not need to be enabled on the web application proxy servers.</span></span>

<span data-ttu-id="3c043-217">**Q: Azure AD Connect Health 경고는 어떻게 해결하나요?**</span><span class="sxs-lookup"><span data-stu-id="3c043-217">**Q: How do Azure AD Connect Health Alerts get resolved?**</span></span>

<span data-ttu-id="3c043-218">Azure AD Connect Health 경고는 성공 조건에서 해결됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-218">Azure AD Connect Health alerts get resolved on a success condition.</span></span> <span data-ttu-id="3c043-219">Azure AD Connect Health 에이전트가 정기적으로 성공 조건을 검색하여 서비스에 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-219">Azure AD Connect Health Agents detect and report the success conditions to the service periodically.</span></span> <span data-ttu-id="3c043-220">일부 경고의 경우 시간을 기준으로 경고가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-220">For a few alerts, the suppression is time-based.</span></span> <span data-ttu-id="3c043-221">즉, 동일한 오류 조건이 경고 생성으로부터 72시간 내에 관찰되지 않으면 경고가 자동으로 해결됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-221">In other words, if the same error condition is not observed within 72 hours from alert generation, the alert is automatically resolved.</span></span>

<span data-ttu-id="3c043-222">**Q: "테스트 인증 요청(가상 트랜잭션)이 토큰을 가져오지 못했습니다."라는 경고를 받았습니다. 이 문제를 어떻게 해결하나요?**</span><span class="sxs-lookup"><span data-stu-id="3c043-222">**Q: I am getting alerted that "Test Authentication Request (Synthetic Transaction) failed to obtain a token." How do I troubleshoot the issue?**</span></span>

<span data-ttu-id="3c043-223">AD FS용 Azure AD Connect Health는 AD FS 서버에 설치된 상태 에이전트가 상태 에이전트에서 시작되는 가상 트랜잭션의 일부로 토큰을 가져오는 데 실패한 경우 이 경고를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-223">Azure AD Connect Health for AD FS generates this alert when the Health Agent installed on an AD FS server fails to obtain a token as part of a synthetic transaction initiated by the Health Agent.</span></span> <span data-ttu-id="3c043-224">상태 에이전트는 로컬 시스템 컨텍스트를 사용하고 자체 신뢰 당사자에 대한 토큰을 가져오려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-224">The Health agent uses the local system context and attempts to get a token for a self relying party.</span></span> <span data-ttu-id="3c043-225">이는 AD FS가 토큰을 발급 중인 상태인지 확인하는 범용 테스트입니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-225">This is a catch-all test to ensure that AD FS is in a state of issuing tokens.</span></span>

<span data-ttu-id="3c043-226">종종 이 테스트는 상태 에이전트가 AD FS 팜 이름을 확인할 수 없기 때문에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-226">Most often this test fails because the Health Agent is unable to resolve the AD FS farm name.</span></span> <span data-ttu-id="3c043-227">이는 AD FS 서버가 네트워크 부하 분산 장치 뒤에 있고 요청이 부하 분산 장치 뒤에 있는 노드에서 시작하는 경우 발생할 수 있습니다(부하 분산 장치 앞에 있는 일반 클라이언트와는 대조적으로).</span><span class="sxs-lookup"><span data-stu-id="3c043-227">This can happen if the AD FS servers are behind a network load balancers and the request gets initiated from a node that's behind the load balancer (as opposed to a regular client that is in front of the load balancer).</span></span> <span data-ttu-id="3c043-228">이는 AD FS 팜 이름(예: sts.contoso.com)에 대해 AD FS 서버의 IP 주소 또는 루프백 IP 주소(127.0.0.1)를 포함하도록 "C:\Windows\System32\drivers\etc" 아래에 있는 "hosts" 파일을 업데이트하여 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-228">This can be fixed by updating the "hosts" file located under "C:\Windows\System32\drivers\etc" to include the IP address of the AD FS server or a loopback IP address (127.0.0.1) for the AD FS farm name (such as sts.contoso.com).</span></span> <span data-ttu-id="3c043-229">호스트 파일을 추가하면 네트워크 호출을 단락(short-circuit)하므로 상태 에이전트에서 토큰을 가져올 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-229">Adding the host file will short-circuit the network call, thus allowing the Health Agent to get the token.</span></span>

<span data-ttu-id="3c043-230">**Q: 내 컴퓨터가 최근 랜섬웨어 공격에 대해 패치되지 않았다는 전자 메일을 받았습니다. 이 전자 메일을 받은 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="3c043-230">**Q: I got an email indicating my machines are NOT patched for the recent ransomeware attacks. Why did I receive this email?**</span></span>

<span data-ttu-id="3c043-231">Azure AD Connect Health 서비스는 필요한 패치가 설치되었는지 확인하기 위해 모니터링하는 모든 컴퓨터를 검색했습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-231">Azure AD Connect Health service scanned all the machines it monitors to ensure the required patches were installed.</span></span> <span data-ttu-id="3c043-232">하나 이상의 컴퓨터에 중요한 패치가 없는 경우 테넌트 관리자에게 전자 메일이 전송되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-232">The email was sent to the tenant administrators if at least one machine did not have the critical patches.</span></span> <span data-ttu-id="3c043-233">이를 결정하기 위해 다음 논리가 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-233">The following logic was used to make this determination.</span></span>
1. <span data-ttu-id="3c043-234">컴퓨터에 설치된 모든 핫픽스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-234">Find all the hotfixes installed on the machine.</span></span>
2. <span data-ttu-id="3c043-235">정의된 목록에서 핫픽스 중 하나 이상이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-235">Check if at least one of the HotFixes from the defined list is present.</span></span>
3. <span data-ttu-id="3c043-236">있는 경우 컴퓨터가 보호되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-236">If Yes, the machine is protected.</span></span> <span data-ttu-id="3c043-237">그렇지 않은 경우 컴퓨터가 공격에 대해 위험에 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-237">If Not, the machine is at risk for the attack.</span></span>

<span data-ttu-id="3c043-238">다음 PowerShell 스크립트를 사용하여 이 검사를 수동으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-238">You can use the following PowerShell script to perform this check manually.</span></span> <span data-ttu-id="3c043-239">위의 논리를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="3c043-239">It implements the above logic.</span></span>

```
Function CheckForMS17-010 ()
{
    $hotfixes = "KB3205409", "KB3210720", "KB3210721", "KB3212646", "KB3213986", "KB4012212", "KB4012213", "KB4012214", "KB4012215", "KB4012216", "KB4012217", "KB4012218", "KB4012220", "KB4012598", "KB4012606", "KB4013198", "KB4013389", "KB4013429", "KB4015217", "KB4015438", "KB4015546", "KB4015547", "KB4015548", "KB4015549", "KB4015550", "KB4015551", "KB4015552", "KB4015553", "KB4015554", "KB4016635", "KB4019213", "KB4019214", "KB4019215", "KB4019216", "KB4019263", "KB4019264", "KB4019472", "KB4015221", "KB4019474", "KB4015219", "KB4019473"

    #checks the computer it's run on if any of the listed hotfixes are present
    $hotfix = Get-HotFix -ComputerName $env:computername | Where-Object {$hotfixes -contains $_.HotfixID} | Select-Object -property "HotFixID"

    #confirms whether hotfix is found or not
    if (Get-HotFix | Where-Object {$hotfixes -contains $_.HotfixID})
    {
        "Found HotFix: " + $hotfix.HotFixID
    } else {
        "Didn't Find HotFix"
    }
}

CheckForMS17-010

```



## <a name="related-links"></a><span data-ttu-id="3c043-240">관련 링크</span><span class="sxs-lookup"><span data-stu-id="3c043-240">Related links</span></span>
* [<span data-ttu-id="3c043-241">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="3c043-241">Azure AD Connect Health</span></span>](active-directory-aadconnect-health.md)
* [<span data-ttu-id="3c043-242">Azure AD Connect Health 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="3c043-242">Azure AD Connect Health Agent installation</span></span>](active-directory-aadconnect-health-agent-install.md)
* [<span data-ttu-id="3c043-243">Azure AD Connect Health 작업</span><span class="sxs-lookup"><span data-stu-id="3c043-243">Azure AD Connect Health operations</span></span>](active-directory-aadconnect-health-operations.md)
* [<span data-ttu-id="3c043-244">AD FS와 함께 Azure AD Connect Health 사용</span><span class="sxs-lookup"><span data-stu-id="3c043-244">Using Azure AD Connect Health with AD FS</span></span>](active-directory-aadconnect-health-adfs.md)
* [<span data-ttu-id="3c043-245">동기화에 대한 Azure AD Connect Health 사용</span><span class="sxs-lookup"><span data-stu-id="3c043-245">Using Azure AD Connect Health for sync</span></span>](active-directory-aadconnect-health-sync.md)
* [<span data-ttu-id="3c043-246">AD DS와 함께 Azure AD Connect Health 사용</span><span class="sxs-lookup"><span data-stu-id="3c043-246">Using Azure AD Connect Health with AD DS</span></span>](active-directory-aadconnect-health-adds.md)
* [<span data-ttu-id="3c043-247">Azure AD Connect Health 버전 내역</span><span class="sxs-lookup"><span data-stu-id="3c043-247">Azure AD Connect Health version history</span></span>](active-directory-aadconnect-health-version-history.md)
