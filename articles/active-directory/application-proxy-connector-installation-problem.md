---
title: "응용 프로그램 프록시 에이전트 커넥터 hello aaaProblem 설치 | Microsoft Docs"
description: "어떻게 tootroubleshoot 문제 수를 설치할 때 면 hello 응용 프로그램 프록시 에이전트 커넥터"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 07ac366a429083af0c9b87aa9df9cf3876132b90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-proxy-agent-connector"></a><span data-ttu-id="4d2bb-103">Hello 응용 프로그램 프록시 에이전트 커넥터를 설치 하는 문제</span><span class="sxs-lookup"><span data-stu-id="4d2bb-103">Problem installing hello Application Proxy Agent Connector</span></span>

<span data-ttu-id="4d2bb-104">Microsoft AAD 응용 프로그램 프록시 커넥터는 hello 클라우드 사용 가능한 끝점 toohello 내부 도메인에서 아웃 바운드 연결 tooestablish hello 연결을 사용 하는 내부 도메인 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="4d2bb-104">Microsoft AAD Application Proxy Connector is an internal domain component that uses outbound connections tooestablish hello connectivity from hello cloud available endpoint toohello internal domain.</span></span>

## <a name="general-problem-areas-with-connector-installation"></a><span data-ttu-id="4d2bb-105">커넥터 설치에 대한 일반적인 문제 영역</span><span class="sxs-lookup"><span data-stu-id="4d2bb-105">General Problem Areas with Connector installation</span></span>

<span data-ttu-id="4d2bb-106">커넥터의 hello 설치가 실패할 경우 hello 근본 원인을 일반적으로 hello 영역을 다음 중 하나:</span><span class="sxs-lookup"><span data-stu-id="4d2bb-106">When hello installation of a connector fails, hello root cause is usually one of hello following areas:</span></span>

1.  <span data-ttu-id="4d2bb-107">**연결** – toocomplete 성공적인 설치를 새 커넥터 요구 tooregister hello 및 이후의 트러스트 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2bb-107">**Connectivity** – toocomplete a successful installation, hello new connector needs tooregister and establish future trust properties.</span></span> <span data-ttu-id="4d2bb-108">이 toohello AAD 응용 프로그램 프록시 클라우드 서비스를 연결 하 여 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d2bb-108">This is done by connecting toohello AAD Application Proxy cloud service.</span></span>

2.  <span data-ttu-id="4d2bb-109">**트러스트 설정** – hello 새 커넥터는 자체 서명 된 인증서를 만들고 toohello 클라우드 서비스를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2bb-109">**Trust Establishment** – hello new connector creates a self-signed cert and registers toohello cloud service.</span></span>

3.  <span data-ttu-id="4d2bb-110">**Admin 님 안녕하세요의 인증** – 설치 하는 동안 hello 사용자 관리자 자격 증명 제공 해야 toocomplete hello 커넥터를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2bb-110">**Authentication of hello admin** – during installation, hello user must provide admin credentials toocomplete hello Connector installation.</span></span>

## <a name="verify-connectivity-toohello-cloud-application-proxy-service-and-microsoft-login-page"></a><span data-ttu-id="4d2bb-111">연결 toohello 클라우드 응용 프로그램 프록시 서비스와 Microsoft 로그인 페이지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2bb-111">Verify connectivity toohello Cloud Application Proxy service and Microsoft Login page</span></span>

<span data-ttu-id="4d2bb-112">**목표:** toohello AAD 응용 프로그램 프록시 등록 끝점 뿐 아니라 Microsoft 로그인 페이지 해당 hello 커넥터 컴퓨터 연결을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2bb-112">**Objective:** Verify that hello connector machine can connect toohello AAD Application Proxy registration endpoint as well as Microsoft login page.</span></span>

1.  <span data-ttu-id="4d2bb-113">브라우저와 go toohello 다음 웹 페이지를 열고: <https://aadap-portcheck.connectorporttest.msappproxy.net> , 해당 hello 연결 tooCentral 미국 확인 및 미국 동부 데이터 센터 9090 및 9091 포트와 함께 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2bb-113">Open a browser and go toohello following web page: <https://aadap-portcheck.connectorporttest.msappproxy.net> , and verify that hello connectivity tooCentral US and East US datacenters with ports 9090 and 9091 is working.</span></span>

2.  <span data-ttu-id="4d2bb-114">실패 한 경우 이러한 포트 (없는 경우 녹색 확인 표시), 해당 hello 방화벽을 확인 또는 백 엔드 프록시는 \*. msappproxy.net 포트 9090 및 9091 올바르게 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2bb-114">If any of those ports is not successful (doesn’t have a green checkmark), verify that hello Firewall or backend proxy has \*.msappproxy.net with ports 9090 and 9091 defined correctly.</span></span>

3.  <span data-ttu-id="4d2bb-115">브라우저 (별도 탭)을 열고 다음 웹 페이지 toohello 이동: <https://login.microsoftonline.com>, toothat 페이지를 로그인 할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2bb-115">Open a browser (separate tab) and go toohello following web page: <https://login.microsoftonline.com>, make sure that you can login toothat page.</span></span>

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a><span data-ttu-id="4d2bb-116">컴퓨터 및 백 엔드 구성 요소가 응용 프로그램 프록시 트러스트 인증서를 지원하는지 확인</span><span class="sxs-lookup"><span data-stu-id="4d2bb-116">Verify Machine and backend components support for Application Proxy trust cert</span></span>

<span data-ttu-id="4d2bb-117">**목표:** hello 커넥터 컴퓨터, 백 엔드 프록시 및 방화벽 이후의 트러스트에 대 한 hello 커넥터에서 만든 hello 인증서를 지원할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2bb-117">**Objective:** Verify that hello connector machine, backend proxy and firewall can support hello certificate created by hello connector for future trust.</span></span>

>[!NOTE]
><span data-ttu-id="4d2bb-118">hello 커넥터 toocreate TLS1.2에서 지원 되는 SHA512 cert 하려고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2bb-118">hello connector tries toocreate a SHA512 cert that is supported by TLS1.2.</span></span> <span data-ttu-id="4d2bb-119">Hello 컴퓨터 또는 hello 백 엔드 방화벽 및 프록시 TLS1.2을 지원 하지 않으면 hello 설치가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2bb-119">If hello machine or hello backend firewall and proxy does not support TLS1.2, hello installation fail.</span></span>
>
>

<span data-ttu-id="4d2bb-120">**tooresolve hello 문제:**</span><span class="sxs-lookup"><span data-stu-id="4d2bb-120">**tooresolve hello issue:**</span></span>

1.  <span data-ttu-id="4d2bb-121">Hello 컴퓨터 TLS1.2 지원-TLS 1.2를 지원 해야 2012 r 2 후 모든 Windows 버전을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2bb-121">Verify hello machine supports TLS1.2 – All Windows versions after 2012 R2 should support TLS 1.2.</span></span> <span data-ttu-id="4d2bb-122">커넥터 컴퓨터에서 2012 r 2의 버전 또는 이전, 있어야 다음 Kb hello 컴퓨터에 설치 되어 해당 hello: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span><span class="sxs-lookup"><span data-stu-id="4d2bb-122">If your connector machine is from a version of 2012 R2 or prior, make sure that hello following KBs are installed on hello machine: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span></span>

2.  <span data-ttu-id="4d2bb-123">네트워크 관리자는 hello 백 엔드 프록시 및 방화벽 차단 하지 않는지 SHA512 나가는 트래픽용 tooverify에 게 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2bb-123">Contact your network admin and ask tooverify that hello backend proxy and firewall do not block SHA512 for outgoing traffic.</span></span>

## <a name="verify-admin-is-used-tooinstall-hello-connector"></a><span data-ttu-id="4d2bb-124">관리자가 사용 되는 tooinstall hello 커넥터를 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4d2bb-124">Verify admin is used tooinstall hello connector</span></span>

<span data-ttu-id="4d2bb-125">**목표:** tooinstall hello 커넥터 게 hello 사용자가 올바른 자격 증명 관리자를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2bb-125">**Objective:** Verify that hello user who tries tooinstall hello connector is an administrator with correct credentials.</span></span> <span data-ttu-id="4d2bb-126">현재 hello 사용자 설치 toosucceed hello에 대 한 전역 관리자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2bb-126">Currently, hello user must be a global administrator for hello installation toosucceed.</span></span>

<span data-ttu-id="4d2bb-127">**tooverify hello 자격 증명이 올바른지:**</span><span class="sxs-lookup"><span data-stu-id="4d2bb-127">**tooverify hello credentials are correct:**</span></span>

<span data-ttu-id="4d2bb-128">너무 연결<https://login.microsoftonline.com> 및 동일한 자격 증명 hello 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2bb-128">Connect too<https://login.microsoftonline.com> and use hello same credentials.</span></span> <span data-ttu-id="4d2bb-129">Hello 로그인이 성공 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2bb-129">Make sure hello login is successful.</span></span> <span data-ttu-id="4d2bb-130">너무 이동 하 여 hello 사용자 역할을 확인할 수 있습니다**Azure Active Directory**  - &gt; **사용자 및 그룹**  - &gt; **모든 사용자가**.</span><span class="sxs-lookup"><span data-stu-id="4d2bb-130">You can check hello user role by going too**Azure Active Directory** -&gt; **Users and Groups** -&gt; **All Users**.</span></span> 

<span data-ttu-id="4d2bb-131">사용자 계정에 다음 "의 디렉터리 역할" hello 나타나는 메뉴를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2bb-131">Select your user account, then “Directory Role” in hello resulting menu.</span></span> <span data-ttu-id="4d2bb-132">해당 hello 선택한 역할 "전역 관리자" 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4d2bb-132">Verify that hello selected role is “Global administrator”.</span></span> <span data-ttu-id="4d2bb-133">Hello의 다음이 단계를 따라 페이지 수 없습니다 tooaccess 인 경우 전역 관리자가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4d2bb-133">If you are unable tooaccess any of hello pages along these steps, you are not a global administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d2bb-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4d2bb-134">Next steps</span></span>
[<span data-ttu-id="4d2bb-135">Azure AD 응용 프로그램 프록시 커넥터 이해</span><span class="sxs-lookup"><span data-stu-id="4d2bb-135">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
