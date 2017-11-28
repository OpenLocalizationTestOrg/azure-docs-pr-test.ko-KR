---
title: "응용 프로그램 프록시 에이전트 커넥터를 설치할 때 문제 발생 | Microsoft 문서"
description: "응용 프로그램 프록시 에이전트 커넥터를 설치할 때 발생하는 문제를 해결하는 방법"
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
ms.openlocfilehash: 91b3f6f3c8339647f568a509e9efd8e1fffb13dd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-installing-the-application-proxy-agent-connector"></a><span data-ttu-id="92a86-103">응용 프로그램 프록시 에이전트 커넥터를 설치할 때 문제 발생</span><span class="sxs-lookup"><span data-stu-id="92a86-103">Problem installing the Application Proxy Agent Connector</span></span>

<span data-ttu-id="92a86-104">Microsoft AAD 응용 프로그램 프록시 커넥터는 아웃바운드 연결을 사용하여 클라우드 사용 가능 끝점에서 내부 도메인으로의 연결을 설정하는 내부 도메인 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="92a86-104">Microsoft AAD Application Proxy Connector is an internal domain component that uses outbound connections to establish the connectivity from the cloud available endpoint to the internal domain.</span></span>

## <a name="general-problem-areas-with-connector-installation"></a><span data-ttu-id="92a86-105">커넥터 설치에 대한 일반적인 문제 영역</span><span class="sxs-lookup"><span data-stu-id="92a86-105">General Problem Areas with Connector installation</span></span>

<span data-ttu-id="92a86-106">커넥터 설치가 실패한 경우 근본 원인은 대개 다음 영역 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="92a86-106">When the installation of a connector fails, the root cause is usually one of the following areas:</span></span>

1.  <span data-ttu-id="92a86-107">**연결** – 성공적인 설치를 완료하려면 새 커넥터를 등록하고 향후 트러스트 속성을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92a86-107">**Connectivity** – to complete a successful installation, the new connector needs to register and establish future trust properties.</span></span> <span data-ttu-id="92a86-108">이 작업은 AAD 응용 프로그램 프록시 클라우드 서비스에 연결하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="92a86-108">This is done by connecting to the AAD Application Proxy cloud service.</span></span>

2.  <span data-ttu-id="92a86-109">**트러스트 설정** – 새 커넥터는 자체 서명된 인증서를 만들고 클라우드 서비스에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="92a86-109">**Trust Establishment** – the new connector creates a self-signed cert and registers to the cloud service.</span></span>

3.  <span data-ttu-id="92a86-110">**관리자 인증** – 설치 중 사용자가 커넥터 설치를 완료하려면 관리자 자격 증명을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92a86-110">**Authentication of the admin** – during installation, the user must provide admin credentials to complete the Connector installation.</span></span>

## <a name="verify-connectivity-to-the-cloud-application-proxy-service-and-microsoft-login-page"></a><span data-ttu-id="92a86-111">클라우드 응용 프로그램 프록시 서비스 및 Microsoft 로그인 페이지에 대한 연결 확인</span><span class="sxs-lookup"><span data-stu-id="92a86-111">Verify connectivity to the Cloud Application Proxy service and Microsoft Login page</span></span>

<span data-ttu-id="92a86-112">**목표:** 커넥터 컴퓨터가 Microsoft 로그인 페이지뿐만 아니라 AAD 응용 프로그램 프록시 등록 끝점에도 연결할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="92a86-112">**Objective:** Verify that the connector machine can connect to the AAD Application Proxy registration endpoint as well as Microsoft login page.</span></span>

1.  <span data-ttu-id="92a86-113">브라우저를 열고 <https://aadap-portcheck.connectorporttest.msappproxy.net> 웹 페이지로 이동하여 포트 9090 및 9091로 미국 중부 및 미국 동부 데이터센터에 대한 연결이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="92a86-113">Open a browser and go to the following web page: <https://aadap-portcheck.connectorporttest.msappproxy.net> , and verify that the connectivity to Central US and East US datacenters with ports 9090 and 9091 is working.</span></span>

2.  <span data-ttu-id="92a86-114">이러한 포트 중 하나라도 성공하지 못하면(녹색 체크 표시가 없으면) 방화벽 또는 백 엔드 프록시에서 \*.msappproxy.net이 포트 9090 및 9091로 올바르게 정의되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="92a86-114">If any of those ports is not successful (doesn’t have a green checkmark), verify that the Firewall or backend proxy has \*.msappproxy.net with ports 9090 and 9091 defined correctly.</span></span>

3.  <span data-ttu-id="92a86-115">브라우저(별도 탭)를 열고 <https://login.microsoftonline.com>을 방문하여 해당 페이지에 로그인할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="92a86-115">Open a browser (separate tab) and go to the following web page: <https://login.microsoftonline.com>, make sure that you can login to that page.</span></span>

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a><span data-ttu-id="92a86-116">컴퓨터 및 백 엔드 구성 요소가 응용 프로그램 프록시 트러스트 인증서를 지원하는지 확인</span><span class="sxs-lookup"><span data-stu-id="92a86-116">Verify Machine and backend components support for Application Proxy trust cert</span></span>

<span data-ttu-id="92a86-117">**목표:** 커넥터 컴퓨터, 백 엔드 프록시 및 방화벽이 향후 트러스트를 위해 커넥터가 만든 인증서를 지원할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="92a86-117">**Objective:** Verify that the connector machine, backend proxy and firewall can support the certificate created by the connector for future trust.</span></span>

>[!NOTE]
><span data-ttu-id="92a86-118">커넥터는 TLS1.2에서 지원하는 SHA512 인증서를 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="92a86-118">The connector tries to create a SHA512 cert that is supported by TLS1.2.</span></span> <span data-ttu-id="92a86-119">컴퓨터 또는 백 엔드 방화벽 및 프록시가 TLS1.2를 지원하지 않으면 설치가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="92a86-119">If the machine or the backend firewall and proxy does not support TLS1.2, the installation fail.</span></span>
>
>

<span data-ttu-id="92a86-120">**이 문제를 해결하려면:**</span><span class="sxs-lookup"><span data-stu-id="92a86-120">**To resolve the issue:**</span></span>

1.  <span data-ttu-id="92a86-121">컴퓨터가 TLS1.2를 지원하는지 확인합니다. 2012 R2 이후의 모든 Windows 버전은 TLS1.2를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="92a86-121">Verify the machine supports TLS1.2 – All Windows versions after 2012 R2 should support TLS 1.2.</span></span> <span data-ttu-id="92a86-122">커넥터 컴퓨터가 2012 R2 또는 이전 버전인 경우 컴퓨터에 <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2> KB가 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="92a86-122">If your connector machine is from a version of 2012 R2 or prior, make sure that the following KBs are installed on the machine: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span></span>

2.  <span data-ttu-id="92a86-123">네트워크 관리자에게 문의하여 백 엔드 프록시와 방화벽이 나가는 트래픽에 대해 SHA512를 차단하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="92a86-123">Contact your network admin and ask to verify that the backend proxy and firewall do not block SHA512 for outgoing traffic.</span></span>

## <a name="verify-admin-is-used-to-install-the-connector"></a><span data-ttu-id="92a86-124">관리자가 커넥터를 설치했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="92a86-124">Verify admin is used to install the connector</span></span>

<span data-ttu-id="92a86-125">**목표:** 커넥터를 설치하려고 하는 사용자가 올바른 자격 증명을 가진 관리자인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="92a86-125">**Objective:** Verify that the user who tries to install the connector is an administrator with correct credentials.</span></span> <span data-ttu-id="92a86-126">현재 설치가 성공하려면 사용자가 전역 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92a86-126">Currently, the user must be a global administrator for the installation to succeed.</span></span>

<span data-ttu-id="92a86-127">**자격 증명이 올바른지 확인하려면:**</span><span class="sxs-lookup"><span data-stu-id="92a86-127">**To verify the credentials are correct:**</span></span>

<span data-ttu-id="92a86-128"><https://login.microsoftonline.com>에 연결하여 동일한 자격 증명을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="92a86-128">Connect to <https://login.microsoftonline.com> and use the same credentials.</span></span> <span data-ttu-id="92a86-129">로그인이 성공하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="92a86-129">Make sure the login is successful.</span></span> <span data-ttu-id="92a86-130">**Azure Active Directory** -&gt; **사용자 및 그룹** -&gt; **모든 사용자**로 이동하여 사용자 역할을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92a86-130">You can check the user role by going to **Azure Active Directory** -&gt; **Users and Groups** -&gt; **All Users**.</span></span> 

<span data-ttu-id="92a86-131">사용자 계정을 선택한 다음 결과 메뉴에서 "디렉터리 역할"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92a86-131">Select your user account, then “Directory Role” in the resulting menu.</span></span> <span data-ttu-id="92a86-132">선택한 역할이 "전역 관리자"인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="92a86-132">Verify that the selected role is “Global administrator”.</span></span> <span data-ttu-id="92a86-133">이 단계에서 페이지에 액세스할 수 없으면 전역 관리자가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="92a86-133">If you are unable to access any of the pages along these steps, you are not a global administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92a86-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="92a86-134">Next steps</span></span>
[<span data-ttu-id="92a86-135">Azure AD 응용 프로그램 프록시 커넥터 이해</span><span class="sxs-lookup"><span data-stu-id="92a86-135">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
