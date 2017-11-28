---
title: "Azure Active Directory 연결 상태 FAQ-aaaAzure | Microsoft Docs"
description: "이 FAQ는 Azure AD Connect Health에 대한 질문에 답변합니다. 이 FAQ에서는 청구 모델, 기능, 제한 사항 및 지원 hello를 포함 하 여 hello 서비스를 사용 하는 방법에 대 한 질문을 다룹니다."
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
ms.openlocfilehash: 3f15d9e9b557b09ef74ceff85806579dd51f2412
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-frequently-asked-questions"></a><span data-ttu-id="18ec4-104">Azure AD Connect Health에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="18ec4-104">Azure AD Connect Health frequently asked questions</span></span>
<span data-ttu-id="18ec4-105">이 문서는 질문과 대답 (Faq) (Azure AD) Azure Active Directory Connect Health에 대 한 답변 toofrequently 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-105">This article includes answers toofrequently asked questions (FAQs) about Azure Active Directory (Azure AD) Connect Health.</span></span> <span data-ttu-id="18ec4-106">이 Faq toouse 청구 모델, 기능, 제한 사항 및 지원 hello를 포함 하는 서비스를 hello 하는 방법에 대 한 질문을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-106">These FAQs cover questions about how toouse hello service, which includes hello billing model, capabilities, limitations, and support.</span></span>

## <a name="general-questions"></a><span data-ttu-id="18ec4-107">일반적인 질문</span><span class="sxs-lookup"><span data-stu-id="18ec4-107">General questions</span></span>
<span data-ttu-id="18ec4-108">**Q: 여러 Azure AD 디렉터리를 관리합니다. Azure Active Directory Premium가 toohello 전환 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="18ec4-108">**Q: I manage multiple Azure AD directories. How do I switch toohello one that has Azure Active Directory Premium?**</span></span>

<span data-ttu-id="18ec4-109">tooswitch 서로 다른 Azure AD 테 넌 트에서, 선택 hello 현재 로그인 **사용자 이름** 오른쪽 위 모서리 hello 되 고 hello 적절 한 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-109">tooswitch between different Azure AD tenants, select hello currently signed-in **User Name** on hello upper-right corner, and then choose hello appropriate account.</span></span> <span data-ttu-id="18ec4-110">Hello 계정 여기 나열 되지 않으면 경우 선택 **로그 아웃**, 한 후 Azure Active Directory Premium에는 hello 디렉터리의 hello 전역 관리자 자격 증명 사용에 toosign를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-110">If hello account is not listed here, select **Sign out**, and then use hello global admin credentials of hello directory that has Azure Active Directory Premium enabled toosign in.</span></span>

<span data-ttu-id="18ec4-111">**Q: Azure AD Connect Health에서 어떤 버전의 ID 역할을 지원하나요?**</span><span class="sxs-lookup"><span data-stu-id="18ec4-111">**Q: What version of identity roles are supported by Azure AD Connect Health?**</span></span>

<span data-ttu-id="18ec4-112">hello 다음 표에서 hello 역할 고 지원 되는 운영 체제 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-112">hello following table lists hello roles and supported operating system versions.</span></span>

|<span data-ttu-id="18ec4-113">역할</span><span class="sxs-lookup"><span data-stu-id="18ec4-113">Role</span></span>| <span data-ttu-id="18ec4-114">운영 체제/버전</span><span class="sxs-lookup"><span data-stu-id="18ec4-114">Operating system / Version</span></span>|
|--|--|
|<span data-ttu-id="18ec4-115">AD FS(Active Directory Federation Services)</span><span class="sxs-lookup"><span data-stu-id="18ec4-115">Active Directory Federation Services (AD FS)</span></span>| <ul> <li> <span data-ttu-id="18ec4-116">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="18ec4-116">Windows Server 2008 R2</span></span> </li><li> <span data-ttu-id="18ec4-117">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="18ec4-117">Windows Server 2012</span></span>  </li> <li><span data-ttu-id="18ec4-118">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="18ec4-118">Windows Server 2012 R2</span></span> </li> <li> <span data-ttu-id="18ec4-119">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="18ec4-119">Windows Server 2016</span></span>  </li> </ul>|
|<span data-ttu-id="18ec4-120">Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="18ec4-120">Azure AD Connect</span></span> | <span data-ttu-id="18ec4-121">버전 1.0.9125 이상</span><span class="sxs-lookup"><span data-stu-id="18ec4-121">Version 1.0.9125 or higher</span></span>|
|<span data-ttu-id="18ec4-122">AD DS(Active Directory Domain Services)</span><span class="sxs-lookup"><span data-stu-id="18ec4-122">Active Directory Domain Services (AD DS)</span></span>| <ul> <li> <span data-ttu-id="18ec4-123">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="18ec4-123">Windows Server 2008 R2</span></span> </li><li> <span data-ttu-id="18ec4-124">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="18ec4-124">Windows Server 2012</span></span>  </li> <li><span data-ttu-id="18ec4-125">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="18ec4-125">Windows Server 2012 R2</span></span> </li> <li> <span data-ttu-id="18ec4-126">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="18ec4-126">Windows Server 2016</span></span>  </li> </ul>|

<span data-ttu-id="18ec4-127">참고 hello 서비스에서 제공 하는 hello 기능 다를 수 있습니다는 hello 역할과 hello 운영 체제를 기반으로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-127">Note that hello features provided by hello service may differ based on hello role and hello operating system.</span></span> <span data-ttu-id="18ec4-128">즉, 모든 hello 기능 모든 운영 체제 버전에 대 한 제공 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-128">In other words, all hello features may not be available for all operating system versions.</span></span> <span data-ttu-id="18ec4-129">자세한 내용은 hello 기능 설명을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="18ec4-129">See hello feature descriptions for details.</span></span>

<span data-ttu-id="18ec4-130">**Q: 라이선스 수 않는 내 인프라 toomonitor 필요 합니까?**</span><span class="sxs-lookup"><span data-stu-id="18ec4-130">**Q: How many licenses do I need toomonitor my infrastructure?**</span></span>

* <span data-ttu-id="18ec4-131">hello 첫 번째 Connect Health Agent 하나 이상의 Azure AD Premium 라이선스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-131">hello first Connect Health Agent requires at least one Azure AD Premium license.</span></span>
* <span data-ttu-id="18ec4-132">등록된 추가 에이전트에는 각각 25개의 추가 Azure AD Premium 라이선스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-132">Each additional registered agent requires 25 additional Azure AD Premium licenses.</span></span>
* <span data-ttu-id="18ec4-133">에이전트 수에는 모든 모니터링 대상 역할 (AD FS, Azure AD Connect 및/또는 AD DS) 등록 되어 있는 에이전트의 해당 toohello 총 수입니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-133">Agent count is equivalent toohello total number of agents that are registered across all monitored roles (AD FS, Azure AD Connect, and/or AD DS).</span></span>

<span data-ttu-id="18ec4-134">Hello에서 라이선스 정보를 찾을 수 또한 [Azure AD 가격 책정 페이지](https://aka.ms/aadpricing)합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-134">Licensing information is also found on hello [Azure AD Pricing page](https://aka.ms/aadpricing).</span></span>

<span data-ttu-id="18ec4-135">예제:</span><span class="sxs-lookup"><span data-stu-id="18ec4-135">Example:</span></span>

| <span data-ttu-id="18ec4-136">등록된 에이전트</span><span class="sxs-lookup"><span data-stu-id="18ec4-136">Registered agents</span></span> | <span data-ttu-id="18ec4-137">필요한 라이선스</span><span class="sxs-lookup"><span data-stu-id="18ec4-137">Licenses needed</span></span> | <span data-ttu-id="18ec4-138">모니터링 구성 예제</span><span class="sxs-lookup"><span data-stu-id="18ec4-138">Example monitoring configuration</span></span> |
| ------ | --------------- | --- |
| <span data-ttu-id="18ec4-139">1</span><span class="sxs-lookup"><span data-stu-id="18ec4-139">1</span></span> | <span data-ttu-id="18ec4-140">1</span><span class="sxs-lookup"><span data-stu-id="18ec4-140">1</span></span> | <span data-ttu-id="18ec4-141">Azure AD Connect 서버 1개</span><span class="sxs-lookup"><span data-stu-id="18ec4-141">1 Azure AD Connect server</span></span> |
| <span data-ttu-id="18ec4-142">2</span><span class="sxs-lookup"><span data-stu-id="18ec4-142">2</span></span> | <span data-ttu-id="18ec4-143">26</span><span class="sxs-lookup"><span data-stu-id="18ec4-143">26</span></span>| <span data-ttu-id="18ec4-144">Azure AD Connect 서버 1개 및 도메인 컨트롤러 1개</span><span class="sxs-lookup"><span data-stu-id="18ec4-144">1 Azure AD Connect server and 1 domain controller</span></span> |
| <span data-ttu-id="18ec4-145">3</span><span class="sxs-lookup"><span data-stu-id="18ec4-145">3</span></span> | <span data-ttu-id="18ec4-146">51</span><span class="sxs-lookup"><span data-stu-id="18ec4-146">51</span></span> | <span data-ttu-id="18ec4-147">AD FS(Active Directory Federation Services) 서버 1개, AD FS 프록시 1개, 도메인 컨트롤러 1개</span><span class="sxs-lookup"><span data-stu-id="18ec4-147">1 Active Directory Federation Services (AD FS) server, 1 AD FS proxy, and 1 domain controller</span></span> |
| <span data-ttu-id="18ec4-148">4</span><span class="sxs-lookup"><span data-stu-id="18ec4-148">4</span></span> | <span data-ttu-id="18ec4-149">76</span><span class="sxs-lookup"><span data-stu-id="18ec4-149">76</span></span> | <span data-ttu-id="18ec4-150">AD FS 서버 1개, AD FS 프록시 1개, 도메인 컨트롤러 2개</span><span class="sxs-lookup"><span data-stu-id="18ec4-150">1 AD FS server, 1 AD FS proxy, and 2 domain controllers</span></span> |
| <span data-ttu-id="18ec4-151">5</span><span class="sxs-lookup"><span data-stu-id="18ec4-151">5</span></span> | <span data-ttu-id="18ec4-152">101</span><span class="sxs-lookup"><span data-stu-id="18ec4-152">101</span></span> | <span data-ttu-id="18ec4-153">Azure AD Connect 서버 1개, AD FS 서버 1개, AD FS 프록시 1개, 도메인 컨트롤러 2개</span><span class="sxs-lookup"><span data-stu-id="18ec4-153">1 Azure AD Connect server, 1 AD FS server, 1 AD FS proxy, and 2 domain controllers</span></span> |


## <a name="installation-questions"></a><span data-ttu-id="18ec4-154">설치 관련 질문</span><span class="sxs-lookup"><span data-stu-id="18ec4-154">Installation questions</span></span>

<span data-ttu-id="18ec4-155">**Q: 개별 서버에 설치 하는 hello Azure AD Connect Health Agent의 hello 영향 란 무엇입니까?**</span><span class="sxs-lookup"><span data-stu-id="18ec4-155">**Q: What is hello impact of installing hello Azure AD Connect Health Agent on individual servers?**</span></span>

<span data-ttu-id="18ec4-156">hello Microsoft Azure AD Connect Health Agent를 AD FS 웹 응용 프로그램 프록시 서버, Azure AD Connect (동기화) 서버, 도메인 컨트롤러 설치의 hello 영향 존중 toohello CPU, 메모리 사용, 네트워크 대역폭 및 저장소와 최소화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-156">hello impact of installing hello Microsoft Azure AD Connect Health Agent, AD FS, web application proxy servers, Azure AD Connect (sync) servers, domain controllers is minimal with respect toohello CPU, memory consumption, network bandwidth, and storage.</span></span>

<span data-ttu-id="18ec4-157">숫자 다음 hello는 근사값:</span><span class="sxs-lookup"><span data-stu-id="18ec4-157">hello following numbers are an approximation:</span></span>

* <span data-ttu-id="18ec4-158">CPU 사용량: 1-5% 증가</span><span class="sxs-lookup"><span data-stu-id="18ec4-158">CPU consumption: ~1-5% increase.</span></span>
* <span data-ttu-id="18ec4-159">메모리 사용량: hello 전체 시스템 메모리 중 too10 %를 차지 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-159">Memory consumption: Up too10 % of hello total system memory.</span></span>

> [!NOTE]
> <span data-ttu-id="18ec4-160">Hello 에이전트는 Azure와 통신할 수 없는, hello 에이전트 로컬로 정의 된 최대 한도 대 한 hello 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-160">If hello agent cannot communicate with Azure, hello agent stores hello data locally for a defined maximum limit.</span></span> <span data-ttu-id="18ec4-161">hello 에이전트 hello "캐시 된" "서비스 least recently"에 따라 데이터를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-161">hello agent overwrites hello “cached” data on a “least recently serviced” basis.</span></span>
>
>

* <span data-ttu-id="18ec4-162">Azure AD Connect Health 에이전트의 로컬 버퍼 저장소: ~20MB.</span><span class="sxs-lookup"><span data-stu-id="18ec4-162">Local buffer storage for Azure AD Connect Health Agents: ~20 MB.</span></span>
* <span data-ttu-id="18ec4-163">AD FS 서버를 프로 비전 1, 024MB (1GB)의 디스크 공간에 대 한 Azure AD Connect Health Agent tooprocess hello AD FS 감사 채널에 대 한 모든 hello 감사 데이터는 덮어쓰기 전에 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-163">For AD FS servers, we recommend that you provision a disk space of 1,024 MB (1 GB) for hello AD FS audit channel for Azure AD Connect Health Agents tooprocess all hello audit data before it is overwritten.</span></span>

<span data-ttu-id="18ec4-164">**Q: 해야 합니까 tooreboot 내 서버 hello hello Azure AD Connect Health Agent 설치 하는 동안?**</span><span class="sxs-lookup"><span data-stu-id="18ec4-164">**Q: Will I have tooreboot my servers during hello installation of hello Azure AD Connect Health Agents?**</span></span>

<span data-ttu-id="18ec4-165">아니요.</span><span class="sxs-lookup"><span data-stu-id="18ec4-165">No.</span></span> <span data-ttu-id="18ec4-166">hello 에이전트의 hello 설치 tooreboot hello 서버를 요구 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-166">hello installation of hello agents will not require you tooreboot hello server.</span></span> <span data-ttu-id="18ec4-167">하지만, 일부 필수 단계가 설치 hello 서버를 다시 부팅을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-167">However, installation of some prerequisite steps might require a reboot of hello server.</span></span>

<span data-ttu-id="18ec4-168">예를 들어 Windows Server 2008 R2에 .NET 4.5 Framework를 설치하는 경우 서버를 재부팅해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-168">For example, on Windows Server 2008 R2, installation of .NET 4.5 Framework requires a server reboot.</span></span>

<span data-ttu-id="18ec4-169">**Q: Azure AD Connect Health는 통과 HTTP 프록시를 통해 작동하나요?**</span><span class="sxs-lookup"><span data-stu-id="18ec4-169">**Q: Does Azure AD Connect Health work through a pass-through HTTP proxy?**</span></span>

<span data-ttu-id="18ec4-170">예.</span><span class="sxs-lookup"><span data-stu-id="18ec4-170">Yes.</span></span> <span data-ttu-id="18ec4-171">진행 중인 작업에 대 한 hello Health Agent toouse는 HTTP 프록시 tooforward 아웃 바운드 HTTP 요청을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-171">For ongoing operations, you can configure hello Health Agent toouse an HTTP proxy tooforward outbound HTTP requests.</span></span>
<span data-ttu-id="18ec4-172">[Health 에이전트에 대한 HTTP 프록시 구성](active-directory-aadconnect-health-agent-install.md#configure-azure-ad-connect-health-agents-to-use-http-proxy)을 자세히 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="18ec4-172">Read more about [configuring HTTP Proxy for Health Agents](active-directory-aadconnect-health-agent-install.md#configure-azure-ad-connect-health-agents-to-use-http-proxy).</span></span>

<span data-ttu-id="18ec4-173">에이전트 등록 하는 동안 프록시 tooconfigure 해야 할 경우 해야 toomodify Internet Explorer 프록시 설정을 미리 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-173">If you need tooconfigure a proxy during agent registration, you might need toomodify your Internet Explorer Proxy settings beforehand.</span></span>

1. <span data-ttu-id="18ec4-174">Internet Explorer > **설정** > **인터넷 옵션** > **연결** > **LAN 설정**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-174">Open Internet Explorer > **Settings** > **Internet Options** > **Connections** > **LAN Settings**.</span></span>
2. <span data-ttu-id="18ec4-175">**사용자 LAN의 프록시 서버 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-175">Select **Use a Proxy Server for your LAN**.</span></span>
3. <span data-ttu-id="18ec4-176">HTTP 및 HTTPS/보안의 프록시 포트가 다른 경우 **고급**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-176">Select **Advanced** if you have different proxy ports for HTTP and HTTPS/Secure.</span></span>

<span data-ttu-id="18ec4-177">**Q: tooHTTP 프록시를 연결할 때 Azure AD Connect Health 기본 인증을 지원 합니까?**</span><span class="sxs-lookup"><span data-stu-id="18ec4-177">**Q: Does Azure AD Connect Health support Basic authentication when connecting tooHTTP proxies?**</span></span>

<span data-ttu-id="18ec4-178">아니요.</span><span class="sxs-lookup"><span data-stu-id="18ec4-178">No.</span></span> <span data-ttu-id="18ec4-179">메커니즘 toospecify 임의의 사용자 이름 및 기본 인증에 대 한 암호를 현재 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-179">A mechanism toospecify an arbitrary user name and password for Basic authentication is not currently supported.</span></span>

<span data-ttu-id="18ec4-180">**Q: 방화벽 포트 수행할 tooopen hello Azure AD Connect Health Agent toowork 필요 합니까?**</span><span class="sxs-lookup"><span data-stu-id="18ec4-180">**Q: What firewall ports do I need tooopen for hello Azure AD Connect Health Agent toowork?**</span></span>

<span data-ttu-id="18ec4-181">Hello 참조 [요구 사항 섹션](active-directory-aadconnect-health-agent-install.md#requirements) hello 목록이 방화벽 포트 및 기타 연결 요구 사항에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-181">See hello [requirements section](active-directory-aadconnect-health-agent-install.md#requirements) for hello list of firewall ports and other connectivity requirements.</span></span>

<span data-ttu-id="18ec4-182">**Q: 두 서버 hello Azure AD Connect Health 포털에서 이름과 같은 이름을 hello로 나타나는 이유는 무엇입니까?**</span><span class="sxs-lookup"><span data-stu-id="18ec4-182">**Q: Why do I see two servers with hello same name in hello Azure AD Connect Health portal?**</span></span>

<span data-ttu-id="18ec4-183">서버에서 에이전트를 제거 하면 hello 서버 hello Azure AD Connect Health 포털에서 자동으로 제거 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-183">When you remove an agent from a server, hello server is not automatically removed from hello Azure AD Connect Health portal.</span></span> <span data-ttu-id="18ec4-184">수동으로 서버에서 에이전트를 제거 하거나 hello 서버 자체를 제거, toomanually hello Azure AD Connect Health 포털에서 hello 서버 항목 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-184">If you manually remove an agent from a server or remove hello server itself, you need toomanually delete hello server entry from hello Azure AD Connect Health portal.</span></span>

<span data-ttu-id="18ec4-185">서버를 이미지로 다시 설치 하거나 동일한 정보 (예: 컴퓨터 이름) hello로 새 서버를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-185">You might reimage a server or create a new server with hello same details (such as machine name).</span></span> <span data-ttu-id="18ec4-186">Hello로 두 개의 항목에 표시 될 수 hello Azure AD Connect Health 포털에서 hello 이미 등록 된 서버를 제거 하지 않은 새 서버 hello에 hello 에이전트를 설치 하는 경우 동일한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-186">If you did not remove hello already registered server from hello Azure AD Connect Health portal, and you installed hello agent on hello new server, you might see two entries with hello same name.</span></span>

<span data-ttu-id="18ec4-187">Toohello 이전 버전의 서버에 속하는 hello 항목을이 경우 수동으로 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-187">In this case, manually delete hello entry that belongs toohello older server.</span></span> <span data-ttu-id="18ec4-188">이 서버에 대 한 hello 데이터 만료 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-188">hello data for this server should be out of date.</span></span>

## <a name="health-agent-registration-and-data-freshness"></a><span data-ttu-id="18ec4-189">Health Agent 등록 및 데이터 새로 고침</span><span class="sxs-lookup"><span data-stu-id="18ec4-189">Health Agent registration and data freshness</span></span>

<span data-ttu-id="18ec4-190">**Q: 정의 hello 상태 에이전트 등록 오류에 대 한 일반적인 이유 및 문제를 해결 하려면 어떻게 합니까?**</span><span class="sxs-lookup"><span data-stu-id="18ec4-190">**Q: What are common reasons for hello Health Agent registration failures and how do I troubleshoot issues?**</span></span>

<span data-ttu-id="18ec4-191">hello 상태 에이전트 못하는 toohello 다음 인해 tooregister 가능한 이유:</span><span class="sxs-lookup"><span data-stu-id="18ec4-191">hello health agent can fail tooregister due toohello following possible reasons:</span></span>

* <span data-ttu-id="18ec4-192">방화벽에서 트래픽이 차단 hello 에이전트 hello 필요한 끝점와 통신할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-192">hello agent cannot communicate with hello required endpoints because a firewall is blocking traffic.</span></span> <span data-ttu-id="18ec4-193">특히 웹 응용 프로그램 프록시 서버에서 자주 발생하는 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-193">This is particularly common on web application proxy servers.</span></span> <span data-ttu-id="18ec4-194">아웃 바운드 통신 toohello 필요한 끝점 및 포트를 허용 하지 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-194">Make sure that you have allowed outbound communication toohello required endpoints and ports.</span></span> <span data-ttu-id="18ec4-195">Hello 참조 [요구 사항 섹션](active-directory-aadconnect-health-agent-install.md#requirements) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-195">See hello [requirements section](active-directory-aadconnect-health-agent-install.md#requirements) for details.</span></span>
* <span data-ttu-id="18ec4-196">아웃 바운드 통신이 hello 네트워크 계층으로 발전 하 여 tooan SSL 검사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-196">Outbound communication is subjected tooan SSL inspection by hello network layer.</span></span> <span data-ttu-id="18ec4-197">그러면 hello 인증서 hello 에이전트가 toobe hello 검사 서버/엔터티, 교체를 사용 하 고 hello 단계 toocomplete hello 에이전트 등록에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-197">This causes hello certificate that hello agent uses toobe replaced by hello inspection server/entity, and hello steps toocomplete hello agent registration fail.</span></span>
* <span data-ttu-id="18ec4-198">hello 사용자 액세스 tooperform hello 등록 hello 에이전트의가 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-198">hello user does not have access tooperform hello registration of hello agent.</span></span> <span data-ttu-id="18ec4-199">전역 관리자는 기본적으로 액세스 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-199">Global admins have access by default.</span></span> <span data-ttu-id="18ec4-200">사용할 수 있습니다 [역할 기반 액세스 제어](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control) toodelegate 액세스 tooother 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-200">You can use [Role Based Access Control](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control) toodelegate access tooother users.</span></span>

<span data-ttu-id="18ec4-201">**Q: am 가져오는 경고를 발생 "상태 관리 서비스 데이터 아닌지 toodate를." Hello 문제를 해결 하려면 어떻게 해야 합니까?**</span><span class="sxs-lookup"><span data-stu-id="18ec4-201">**Q: I am getting alerted that "Health Service data is not up toodate." How do I troubleshoot hello issue?**</span></span>

<span data-ttu-id="18ec4-202">Azure AD Connect Health 수신 되지 않으면 모든 hello 데이터 요소 hello에 대 한 hello 서버에서 마지막 2 시간 hello 경고를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-202">Azure AD Connect Health generates hello alert when it does not receive all hello data points from hello server in hello last two hours.</span></span> <span data-ttu-id="18ec4-203">이 경고가 발생하는 여러 이유가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-203">There can be multiple reasons for this alert.</span></span>

* <span data-ttu-id="18ec4-204">방화벽에서 트래픽이 차단 hello 에이전트 hello 필요한 끝점와 통신할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-204">hello agent cannot communicate with hello required endpoints because a firewall is blocking traffic.</span></span> <span data-ttu-id="18ec4-205">특히 웹 응용 프로그램 프록시 서버에서 자주 발생하는 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-205">This is particularly common on web application proxy servers.</span></span> <span data-ttu-id="18ec4-206">아웃 바운드 통신 toohello 필요한 끝점 및 포트를 허용 하지 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-206">Make sure that you have allowed outbound communication toohello required end points and ports.</span></span> <span data-ttu-id="18ec4-207">Hello 참조 [요구 사항 섹션](active-directory-aadconnect-health-agent-install.md#requirements) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-207">See hello [requirements section](active-directory-aadconnect-health-agent-install.md#requirements) for details.</span></span>
* <span data-ttu-id="18ec4-208">아웃 바운드 통신이 hello 네트워크 계층으로 발전 하 여 tooan SSL 검사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-208">Outbound communication is subjected tooan SSL inspection by hello network layer.</span></span> <span data-ttu-id="18ec4-209">그러면 hello 인증서 hello 에이전트가 toobe hello 검사 서버/엔터티, 교체를 사용 하 고 hello 프로세스 tooupload 데이터 toohello Azure AD Connect Health 서비스는 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-209">This causes hello certificate that hello agent uses toobe replaced by hello inspection server/entity, and hello process fails tooupload data toohello Azure AD Connect Health service.</span></span>
* <span data-ttu-id="18ec4-210">Hello 에이전트에 기본 제공 되는 hello 연결 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-210">You can use hello connectivity command built into hello agent.</span></span> <span data-ttu-id="18ec4-211">[자세히 알아보기](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service).</span><span class="sxs-lookup"><span data-stu-id="18ec4-211">[Read more](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service).</span></span>
* <span data-ttu-id="18ec4-212">또한 hello 에이전트 인증 되지 않은 HTTP 프록시를 통해 아웃 바운드 연결을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-212">hello agents also support outbound connectivity via an unauthenticated HTTP Proxy.</span></span> <span data-ttu-id="18ec4-213">[자세히 알아보기](active-directory-aadconnect-health-agent-install.md##configure-azure-ad-connect-health-agents-to-use-http-proxy).</span><span class="sxs-lookup"><span data-stu-id="18ec4-213">[Read more](active-directory-aadconnect-health-agent-install.md##configure-azure-ad-connect-health-agents-to-use-http-proxy).</span></span>

## <a name="operations-questions"></a><span data-ttu-id="18ec4-214">작업 관련 질문</span><span class="sxs-lookup"><span data-stu-id="18ec4-214">Operations questions</span></span>
<span data-ttu-id="18ec4-215">**Q: 웹 응용 프로그램 프록시 서버 hello에 대 한 감사 tooenable 필요 합니까?**</span><span class="sxs-lookup"><span data-stu-id="18ec4-215">**Q: Do I need tooenable auditing on hello web application proxy servers?**</span></span>

<span data-ttu-id="18ec4-216">아니요, 감사 toobe hello 웹 응용 프로그램 프록시 서버에서 활성화 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-216">No, auditing does not need toobe enabled on hello web application proxy servers.</span></span>

<span data-ttu-id="18ec4-217">**Q: Azure AD Connect Health 경고는 어떻게 해결하나요?**</span><span class="sxs-lookup"><span data-stu-id="18ec4-217">**Q: How do Azure AD Connect Health Alerts get resolved?**</span></span>

<span data-ttu-id="18ec4-218">Azure AD Connect Health 경고는 성공 조건에서 해결됩니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-218">Azure AD Connect Health alerts get resolved on a success condition.</span></span> <span data-ttu-id="18ec4-219">Azure AD Connect Health Agent 탐지 및 hello 성공 조건 toohello 서비스를 정기적으로 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-219">Azure AD Connect Health Agents detect and report hello success conditions toohello service periodically.</span></span> <span data-ttu-id="18ec4-220">몇 가지 경고에 대 한 hello 억제 (suppression)은 시간 기반입니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-220">For a few alerts, hello suppression is time-based.</span></span> <span data-ttu-id="18ec4-221">즉, hello 동일한 오류가 발견 되지 않으면 경고 생성에서 72 시간 이내, hello 경고가 자동으로 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-221">In other words, if hello same error condition is not observed within 72 hours from alert generation, hello alert is automatically resolved.</span></span>

<span data-ttu-id="18ec4-222">**Q: am 가져오는 경고를 발생 시킬 "테스트 인증 요청 (가상 트랜잭션) 못했음을 tooobtain 토큰입니다." Hello 문제를 해결 하려면 어떻게 해야 합니까?**</span><span class="sxs-lookup"><span data-stu-id="18ec4-222">**Q: I am getting alerted that "Test Authentication Request (Synthetic Transaction) failed tooobtain a token." How do I troubleshoot hello issue?**</span></span>

<span data-ttu-id="18ec4-223">AD FS에 대 한 azure AD Connect Health hello 상태 에이전트는 AD FS 서버에 설치 된 hello 상태 에이전트에 의해 시작 되는 가상 트랜잭션의 일부로 tooobtain 토큰을 실패 한 경우이 경고를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-223">Azure AD Connect Health for AD FS generates this alert when hello Health Agent installed on an AD FS server fails tooobtain a token as part of a synthetic transaction initiated by hello Health Agent.</span></span> <span data-ttu-id="18ec4-224">hello Health agent hello 로컬 시스템 컨텍스트를 사용 하 고 자체 신뢰 당사자에 대 한 tooget 토큰을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-224">hello Health agent uses hello local system context and attempts tooget a token for a self relying party.</span></span> <span data-ttu-id="18ec4-225">이 AD FS 토큰을 발급의 상태에 있는 범용 테스트 tooensure입니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-225">This is a catch-all test tooensure that AD FS is in a state of issuing tokens.</span></span>

<span data-ttu-id="18ec4-226">가장 자주 hello Health Agent는 없습니다 tooresolve hello AD FS 팜 이름 때문에이 테스트에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-226">Most often this test fails because hello Health Agent is unable tooresolve hello AD FS farm name.</span></span> <span data-ttu-id="18ec4-227">이 오류는 hello AD FS 서버는 네트워크 부하 분산 장치 뒤에 hello 요청이 가져옵니다 (부하 분산 장치 hello 앞에 있는 일반 클라이언트 것과 반대로 tooa)으로 hello 부하 분산 장치 뒤에 있는 노드에서 시작 하는 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-227">This can happen if hello AD FS servers are behind a network load balancers and hello request gets initiated from a node that's behind hello load balancer (as opposed tooa regular client that is in front of hello load balancer).</span></span> <span data-ttu-id="18ec4-228">이 hello AD FS 팜 이름 (예: sts.contoso.com)에 대 한 hello "호스트"에 있는 파일에 "C:\Windows\System32\drivers\etc" hello AD FS 서버의 tooinclude hello IP 주소 또는 루프백 IP 주소 (127.0.0.1)를 업데이트 하 여 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-228">This can be fixed by updating hello "hosts" file located under "C:\Windows\System32\drivers\etc" tooinclude hello IP address of hello AD FS server or a loopback IP address (127.0.0.1) for hello AD FS farm name (such as sts.contoso.com).</span></span> <span data-ttu-id="18ec4-229">Hello 호스트 파일을 추가 합니다 단락 (short-circuit) hello 네트워크 호출을 hello Health Agent tooget hello 토큰 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-229">Adding hello host file will short-circuit hello network call, thus allowing hello Health Agent tooget hello token.</span></span>

<span data-ttu-id="18ec4-230">**Q: 내 컴퓨터 hello 최근 ransomeware 공격에 대 한 패치가 적용 되지 않은 표시 된 전자 메일을 수신 합니다. 이 전자 메일을 받은 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="18ec4-230">**Q: I got an email indicating my machines are NOT patched for hello recent ransomeware attacks. Why did I receive this email?**</span></span>

<span data-ttu-id="18ec4-231">Azure AD Connect Health 서비스 tooensure hello 필요한 패치를 모니터링 하는 컴퓨터에 설치 된 모든 hello를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-231">Azure AD Connect Health service scanned all hello machines it monitors tooensure hello required patches were installed.</span></span> <span data-ttu-id="18ec4-232">하나 이상의 컴퓨터에 중요 한 패치 hello 없는 hello 전자 메일 toohello 테 넌 트 관리자를 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-232">hello email was sent toohello tenant administrators if at least one machine did not have hello critical patches.</span></span> <span data-ttu-id="18ec4-233">다음 논리 hello 사용된 toomake이이 결정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-233">hello following logic was used toomake this determination.</span></span>
1. <span data-ttu-id="18ec4-234">Hello 컴퓨터에 설치 된 모든 hello 핫픽스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-234">Find all hello hotfixes installed on hello machine.</span></span>
2. <span data-ttu-id="18ec4-235">현재 인지 hello에서 핫픽스 hello 중 하나 이상 정의 목록을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-235">Check if at least one of hello HotFixes from hello defined list is present.</span></span>
3. <span data-ttu-id="18ec4-236">그렇다면 hello 컴퓨터 보호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-236">If Yes, hello machine is protected.</span></span> <span data-ttu-id="18ec4-237">그렇지 않은 경우 hello 컴퓨터 hello 공격에 대 한 위험에 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-237">If Not, hello machine is at risk for hello attack.</span></span>

<span data-ttu-id="18ec4-238">수동으로 진행할 수 있습니다 다음 PowerShell 스크립트 tooperform hello이이 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-238">You can use hello following PowerShell script tooperform this check manually.</span></span> <span data-ttu-id="18ec4-239">Hello 위에 논리를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="18ec4-239">It implements hello above logic.</span></span>

```
Function CheckForMS17-010 ()
{
    $hotfixes = "KB3205409", "KB3210720", "KB3210721", "KB3212646", "KB3213986", "KB4012212", "KB4012213", "KB4012214", "KB4012215", "KB4012216", "KB4012217", "KB4012218", "KB4012220", "KB4012598", "KB4012606", "KB4013198", "KB4013389", "KB4013429", "KB4015217", "KB4015438", "KB4015546", "KB4015547", "KB4015548", "KB4015549", "KB4015550", "KB4015551", "KB4015552", "KB4015553", "KB4015554", "KB4016635", "KB4019213", "KB4019214", "KB4019215", "KB4019216", "KB4019263", "KB4019264", "KB4019472", "KB4015221", "KB4019474", "KB4015219", "KB4019473"

    #checks hello computer it's run on if any of hello listed hotfixes are present
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



## <a name="related-links"></a><span data-ttu-id="18ec4-240">관련 링크</span><span class="sxs-lookup"><span data-stu-id="18ec4-240">Related links</span></span>
* [<span data-ttu-id="18ec4-241">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="18ec4-241">Azure AD Connect Health</span></span>](active-directory-aadconnect-health.md)
* [<span data-ttu-id="18ec4-242">Azure AD Connect Health 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="18ec4-242">Azure AD Connect Health Agent installation</span></span>](active-directory-aadconnect-health-agent-install.md)
* [<span data-ttu-id="18ec4-243">Azure AD Connect Health 작업</span><span class="sxs-lookup"><span data-stu-id="18ec4-243">Azure AD Connect Health operations</span></span>](active-directory-aadconnect-health-operations.md)
* [<span data-ttu-id="18ec4-244">AD FS와 함께 Azure AD Connect Health 사용</span><span class="sxs-lookup"><span data-stu-id="18ec4-244">Using Azure AD Connect Health with AD FS</span></span>](active-directory-aadconnect-health-adfs.md)
* [<span data-ttu-id="18ec4-245">동기화에 대한 Azure AD Connect Health 사용</span><span class="sxs-lookup"><span data-stu-id="18ec4-245">Using Azure AD Connect Health for sync</span></span>](active-directory-aadconnect-health-sync.md)
* [<span data-ttu-id="18ec4-246">AD DS와 함께 Azure AD Connect Health 사용</span><span class="sxs-lookup"><span data-stu-id="18ec4-246">Using Azure AD Connect Health with AD DS</span></span>](active-directory-aadconnect-health-adds.md)
* [<span data-ttu-id="18ec4-247">Azure AD Connect Health 버전 내역</span><span class="sxs-lookup"><span data-stu-id="18ec4-247">Azure AD Connect Health version history</span></span>](active-directory-aadconnect-health-version-history.md)
