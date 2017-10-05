---
title: "Azure Multi-Factor Authentication 서버 시작하기 | Microsoft Docs"
description: "Azure MFA 서버 시작 방법을 설명하는 Azure 다단계 인증 페이지입니다."
services: multi-factor-authentication
keywords: "인증 서버, Azure Multi Factor Authentication 앱 활성화 페이지, 인증 서버 다운로드"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: e94120e4-ed77-44b8-84e4-1c5f7e186a6b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: ebc5fd442c1f0dd9841c1423c174a073d286911a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-the-azure-multi-factor-authentication-server"></a><span data-ttu-id="bfd9e-104">Azure Multi-Factor Authentication 서버로 시작하기</span><span class="sxs-lookup"><span data-stu-id="bfd9e-104">Getting started with the Azure Multi-Factor Authentication Server</span></span>

<span data-ttu-id="bfd9e-105"><center>![MFA 온-프레미스](./media/multi-factor-authentication-get-started-server/server2.png)</center></span><span class="sxs-lookup"><span data-stu-id="bfd9e-105"><center>![MFA on-premises](./media/multi-factor-authentication-get-started-server/server2.png)</center></span></span>

<span data-ttu-id="bfd9e-106">온-프레미스 Multi-Factor Authentication 서버를 사용할지 여부를 결정했으므로 다음으로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-106">Now that we have determined to use on-premises Multi-Factor Authentication Server, let’s get going.</span></span> <span data-ttu-id="bfd9e-107">이 페이지에서는 서버를 새롭게 설치하고 이를 온-프레미스 Active Directory를 사용하여 설정하는 것을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-107">This page covers a new installation of the server and setting it up with on-premises Active Directory.</span></span> <span data-ttu-id="bfd9e-108">MFA 서버가 이미 설치되어 있고 업그레이드를 고려하는 경우 [최신 Azure Multi-Factor Authentication 서버로 업그레이드](multi-factor-authentication-server-upgrade.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-108">If you already have the MFA server installed and are looking to upgrade, see [Upgrade to the latest Azure Multi-Factor Authentication Server](multi-factor-authentication-server-upgrade.md).</span></span> <span data-ttu-id="bfd9e-109">웹 서비스만 설치하는 정보는 [Azure Multi-Factor Authentication 서버 모바일 앱 웹 서비스 배포](multi-factor-authentication-get-started-server-webservice.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-109">If you're looking for information on installing just the web service, see [Deploying the Azure Multi-Factor Authentication Server Mobile App Web Service](multi-factor-authentication-get-started-server-webservice.md).</span></span>

## <a name="plan-your-deployment"></a><span data-ttu-id="bfd9e-110">배포 계획</span><span class="sxs-lookup"><span data-stu-id="bfd9e-110">Plan your deployment</span></span>

<span data-ttu-id="bfd9e-111">Azure Multi-Factor Authentication 서버를 다운로드하기 전에 로드 및 고가용성 요구 사항에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-111">Before you download the Azure Multi-Factor Authentication Server, think about what your load and high availability requirements are.</span></span> <span data-ttu-id="bfd9e-112">이 정보를 사용하여 배포 방법 및 위치를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-112">Use this information to decide how and where to deploy.</span></span>

<span data-ttu-id="bfd9e-113">필요한 메모리 양에 대한 올바른 지침은 정기적으로 인증해야 하는 사용자의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-113">A good guideline for the amount of memory you need is the number of users you expect to authenticate on a regular basis.</span></span>

| <span data-ttu-id="bfd9e-114">사용자</span><span class="sxs-lookup"><span data-stu-id="bfd9e-114">Users</span></span> | <span data-ttu-id="bfd9e-115">RAM</span><span class="sxs-lookup"><span data-stu-id="bfd9e-115">RAM</span></span> |
| ----- | --- |
| <span data-ttu-id="bfd9e-116">1-10,000</span><span class="sxs-lookup"><span data-stu-id="bfd9e-116">1-10,000</span></span> | <span data-ttu-id="bfd9e-117">4GB</span><span class="sxs-lookup"><span data-stu-id="bfd9e-117">4 GB</span></span> |
| <span data-ttu-id="bfd9e-118">10,001-50,000</span><span class="sxs-lookup"><span data-stu-id="bfd9e-118">10,001-50,000</span></span> | <span data-ttu-id="bfd9e-119">8GB</span><span class="sxs-lookup"><span data-stu-id="bfd9e-119">8 GB</span></span> |
| <span data-ttu-id="bfd9e-120">50,001-100,000</span><span class="sxs-lookup"><span data-stu-id="bfd9e-120">50,001-100,000</span></span> | <span data-ttu-id="bfd9e-121">12GB</span><span class="sxs-lookup"><span data-stu-id="bfd9e-121">12 GB</span></span> |
| <span data-ttu-id="bfd9e-122">100,000-200,001</span><span class="sxs-lookup"><span data-stu-id="bfd9e-122">100,000-200,001</span></span> | <span data-ttu-id="bfd9e-123">16GB</span><span class="sxs-lookup"><span data-stu-id="bfd9e-123">16 GB</span></span> |
| <span data-ttu-id="bfd9e-124">200,001+</span><span class="sxs-lookup"><span data-stu-id="bfd9e-124">200,001+</span></span> | <span data-ttu-id="bfd9e-125">32GB</span><span class="sxs-lookup"><span data-stu-id="bfd9e-125">32 GB</span></span> |

<span data-ttu-id="bfd9e-126">고가용성 또는 부하 분산을 위해 여러 개의 서버를 설정해야 하는가요?</span><span class="sxs-lookup"><span data-stu-id="bfd9e-126">Do you need to set up multiple servers for high availability or load balancing?</span></span> <span data-ttu-id="bfd9e-127">Azure MFA 서버로 이 구성을 설정하는 방법은 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-127">There are a number of ways to set up this configuration with Azure MFA Server.</span></span> <span data-ttu-id="bfd9e-128">첫 번째로 설치하는 Azure MFA 서버는 마스터 서버가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-128">When you install your first Azure MFA Server, it becomes the master.</span></span> <span data-ttu-id="bfd9e-129">추가되는 서버는 모두 하위 서버가 되며 사용자와 구성을 마스터 서버와 자동으로 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-129">Any additional servers become subordinate, and automatically synchronize users and configuration with the master.</span></span> <span data-ttu-id="bfd9e-130">그런 다음 하나의 주 서버를 구성하고 나머지 서버를 백업으로 사용하거나 모든 서버 간에 부하 분산을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-130">Then, you can configure one primary server and have the rest act as backup, or you can set up load balancing among all the servers.</span></span>

<span data-ttu-id="bfd9e-131">마스터 Azure MFA 서버가 오프라인 상태가 되면 하위 서버에서 2단계 인증 요청을 계속 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-131">When a master Azure MFA Server goes offline, the subordinate servers can still process two-step verification requests.</span></span> <span data-ttu-id="bfd9e-132">그러나 새 사용자를 추가할 수 없으며, 마스터가 다시 온라인 상태가 되거나 하위 서버가 승격될 때까지 기존 사용자는 해당 설정을 업데이트할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-132">However, you can't add new users and existing users can't update their settings until the master is back online or a subordinate gets promoted.</span></span>

### <a name="prepare-your-environment"></a><span data-ttu-id="bfd9e-133">환경 준비</span><span class="sxs-lookup"><span data-stu-id="bfd9e-133">Prepare your environment</span></span>

<span data-ttu-id="bfd9e-134">Azure Multi-Factor Authentication에 사용 중인 서버가 다음 요구 사항을 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-134">Make sure the server  that you're using for Azure Multi-Factor Authentication meets the following requirements:</span></span>

| <span data-ttu-id="bfd9e-135">Azure Multi-Factor Authentication 서버 요구 사항</span><span class="sxs-lookup"><span data-stu-id="bfd9e-135">Azure Multi-Factor Authentication Server Requirements</span></span> | <span data-ttu-id="bfd9e-136">설명</span><span class="sxs-lookup"><span data-stu-id="bfd9e-136">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="bfd9e-137">하드웨어</span><span class="sxs-lookup"><span data-stu-id="bfd9e-137">Hardware</span></span> |<li><span data-ttu-id="bfd9e-138">200MB의 하드 디스크 공간</span><span class="sxs-lookup"><span data-stu-id="bfd9e-138">200 MB of hard disk space</span></span></li><li><span data-ttu-id="bfd9e-139">x32 또는 x64 지원 프로세서</span><span class="sxs-lookup"><span data-stu-id="bfd9e-139">x32 or x64 capable processor</span></span></li><li><span data-ttu-id="bfd9e-140">1GB 이상 RAM</span><span class="sxs-lookup"><span data-stu-id="bfd9e-140">1 GB or greater RAM</span></span></li> |
| <span data-ttu-id="bfd9e-141">소프트웨어</span><span class="sxs-lookup"><span data-stu-id="bfd9e-141">Software</span></span> |<li><span data-ttu-id="bfd9e-142">호스트가 서버 OS인 경우 Windows Server 2008 이상</span><span class="sxs-lookup"><span data-stu-id="bfd9e-142">Windows Server 2008 or greater if the host is a server OS</span></span></li><li><span data-ttu-id="bfd9e-143">호스트가 클라이언트 OS인 경우 Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="bfd9e-143">Windows 7 or greater if the host is a client OS</span></span></li><li><span data-ttu-id="bfd9e-144">Microsoft .NET 4.0 Framework</span><span class="sxs-lookup"><span data-stu-id="bfd9e-144">Microsoft .NET 4.0 Framework</span></span></li><li><span data-ttu-id="bfd9e-145">사용자 포털 또는 웹 서비스 SDK를 설치하는 경우 IIS 7.0 이상</span><span class="sxs-lookup"><span data-stu-id="bfd9e-145">IIS 7.0 or greater if installing the user portal or web service SDK</span></span></li> |

### <a name="azure-mfa-server-components"></a><span data-ttu-id="bfd9e-146">Azure MFA 서버 구성 요소</span><span class="sxs-lookup"><span data-stu-id="bfd9e-146">Azure MFA Server Components</span></span>

<span data-ttu-id="bfd9e-147">Azure MFA 서버를 구성하는 세 가지 웹 구성 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-147">There are three web components that make up Azure MFA Server:</span></span>

* <span data-ttu-id="bfd9e-148">웹 서비스 SDK - 다른 구성 요소와 통신을 활성화하고 Azure MFA 응용 프로그램 서버에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-148">Web Service SDK - Enables communication with the other components and is installed on the Azure MFA application server</span></span>
* <span data-ttu-id="bfd9e-149">사용자 포털 - 사용자가 Azure MFA(Multi-Factor Authentication)에 등록하고 해당 계정을 유지 관리할 수 있는 IIS 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-149">User Portal - An IIS web site that allows users to enroll in Azure Multi-Factor Authentication (MFA) and maintain their accounts.</span></span>
* <span data-ttu-id="bfd9e-150">모바일 앱 웹 서비스 - 2단계 인증에 대해 Microsoft Authenticator 앱과 같은 모바일 앱을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-150">Mobile App Web Service - Enables using a mobile app like the Microsoft Authenticator app for two-step verification.</span></span>

<span data-ttu-id="bfd9e-151">서버를 인터넷에 연결하는 경우 세 가지 구성 요소를 모두 동일한 서버에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-151">All three components can be installed on the same server if the server is internet-facing.</span></span> <span data-ttu-id="bfd9e-152">구성 요소를 나누는 경우 웹 서비스 SDK는 Azure MFA 응용 프로그램 서버에 설치되고 사용자 포털 및 모바일 앱 웹 서비스는 인터넷 연결 서버에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-152">If breaking up the components, the Web Service SDK is installed on the Azure MFA application server and the User Portal and Mobile App Web Service are installed on an internet-facing server.</span></span>

### <a name="azure-multi-factor-authentication-server-firewall-requirements"></a><span data-ttu-id="bfd9e-153">Azure Multi-Factor Authentication 방화벽 요구 사항</span><span class="sxs-lookup"><span data-stu-id="bfd9e-153">Azure Multi-Factor Authentication Server firewall requirements</span></span>

<span data-ttu-id="bfd9e-154">각 MFA 서버는 다음 주소로 포트 443 아웃바운드에서 통신할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-154">Each MFA server must be able to communicate on port 443 outbound to the following addresses:</span></span>

* <span data-ttu-id="bfd9e-155">https://pfd.phonefactor.net</span><span class="sxs-lookup"><span data-stu-id="bfd9e-155">https://pfd.phonefactor.net</span></span>
* <span data-ttu-id="bfd9e-156">https://pfd2.phonefactor.net</span><span class="sxs-lookup"><span data-stu-id="bfd9e-156">https://pfd2.phonefactor.net</span></span>
* <span data-ttu-id="bfd9e-157">https://css.phonefactor.net</span><span class="sxs-lookup"><span data-stu-id="bfd9e-157">https://css.phonefactor.net</span></span>

<span data-ttu-id="bfd9e-158">아웃바운드 방화벽이 포트 443에서 제한되는 경우 다음 IP 주소 범위를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-158">If outbound firewalls are restricted on port 443, open the following IP address ranges:</span></span>

| <span data-ttu-id="bfd9e-159">IP 서브넷</span><span class="sxs-lookup"><span data-stu-id="bfd9e-159">IP Subnet</span></span> | <span data-ttu-id="bfd9e-160">네트워크 마스크</span><span class="sxs-lookup"><span data-stu-id="bfd9e-160">Netmask</span></span> | <span data-ttu-id="bfd9e-161">IP 범위</span><span class="sxs-lookup"><span data-stu-id="bfd9e-161">IP Range</span></span> |
|:---: |:---: |:---: |
| <span data-ttu-id="bfd9e-162">134.170.116.0/25</span><span class="sxs-lookup"><span data-stu-id="bfd9e-162">134.170.116.0/25</span></span> |<span data-ttu-id="bfd9e-163">255.255.255.128</span><span class="sxs-lookup"><span data-stu-id="bfd9e-163">255.255.255.128</span></span> |<span data-ttu-id="bfd9e-164">134.170.116.1 – 134.170.116.126</span><span class="sxs-lookup"><span data-stu-id="bfd9e-164">134.170.116.1 – 134.170.116.126</span></span> |
| <span data-ttu-id="bfd9e-165">134.170.165.0/25</span><span class="sxs-lookup"><span data-stu-id="bfd9e-165">134.170.165.0/25</span></span> |<span data-ttu-id="bfd9e-166">255.255.255.128</span><span class="sxs-lookup"><span data-stu-id="bfd9e-166">255.255.255.128</span></span> |<span data-ttu-id="bfd9e-167">134.170.165.1 – 134.170.165.126</span><span class="sxs-lookup"><span data-stu-id="bfd9e-167">134.170.165.1 – 134.170.165.126</span></span> |
| <span data-ttu-id="bfd9e-168">70.37.154.128/25</span><span class="sxs-lookup"><span data-stu-id="bfd9e-168">70.37.154.128/25</span></span> |<span data-ttu-id="bfd9e-169">255.255.255.128</span><span class="sxs-lookup"><span data-stu-id="bfd9e-169">255.255.255.128</span></span> |<span data-ttu-id="bfd9e-170">70.37.154.129 – 70.37.154.254</span><span class="sxs-lookup"><span data-stu-id="bfd9e-170">70.37.154.129 – 70.37.154.254</span></span> |

<span data-ttu-id="bfd9e-171">이벤트 확인 기능을 사용하지 않고 사용자가 모바일 앱을 사용하여 회사 네트워크의 장치에서 확인하지 않는 경우 다음 범위만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-171">If you aren't using the Event Confirmation feature, and your users aren't using mobile apps to verify from devices on the corporate network, you only need the following ranges:</span></span>

| <span data-ttu-id="bfd9e-172">IP 서브넷</span><span class="sxs-lookup"><span data-stu-id="bfd9e-172">IP Subnet</span></span> | <span data-ttu-id="bfd9e-173">네트워크 마스크</span><span class="sxs-lookup"><span data-stu-id="bfd9e-173">Netmask</span></span> | <span data-ttu-id="bfd9e-174">IP 범위</span><span class="sxs-lookup"><span data-stu-id="bfd9e-174">IP Range</span></span> |
|:---: |:---: |:---: |
| <span data-ttu-id="bfd9e-175">134.170.116.72/29</span><span class="sxs-lookup"><span data-stu-id="bfd9e-175">134.170.116.72/29</span></span> |<span data-ttu-id="bfd9e-176">255.255.255.248</span><span class="sxs-lookup"><span data-stu-id="bfd9e-176">255.255.255.248</span></span> |<span data-ttu-id="bfd9e-177">134.170.116.72 – 134.170.116.79</span><span class="sxs-lookup"><span data-stu-id="bfd9e-177">134.170.116.72 – 134.170.116.79</span></span> |
| <span data-ttu-id="bfd9e-178">134.170.165.72/29</span><span class="sxs-lookup"><span data-stu-id="bfd9e-178">134.170.165.72/29</span></span> |<span data-ttu-id="bfd9e-179">255.255.255.248</span><span class="sxs-lookup"><span data-stu-id="bfd9e-179">255.255.255.248</span></span> |<span data-ttu-id="bfd9e-180">134.170.165.72 – 134.170.165.79</span><span class="sxs-lookup"><span data-stu-id="bfd9e-180">134.170.165.72 – 134.170.165.79</span></span> |
| <span data-ttu-id="bfd9e-181">70.37.154.200/29</span><span class="sxs-lookup"><span data-stu-id="bfd9e-181">70.37.154.200/29</span></span> |<span data-ttu-id="bfd9e-182">255.255.255.248</span><span class="sxs-lookup"><span data-stu-id="bfd9e-182">255.255.255.248</span></span> |<span data-ttu-id="bfd9e-183">70.37.154.201 – 70.37.154.206</span><span class="sxs-lookup"><span data-stu-id="bfd9e-183">70.37.154.201 – 70.37.154.206</span></span> |

## <a name="download-the-azure-multi-factor-authentication-server"></a><span data-ttu-id="bfd9e-184">Azure Multi-Factor Authentication 서버 다운로드</span><span class="sxs-lookup"><span data-stu-id="bfd9e-184">Download the Azure Multi-Factor Authentication Server</span></span>

1. <span data-ttu-id="bfd9e-185">관리자로 [Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-185">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="bfd9e-186">왼쪽 창에서 **Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-186">On the left, select **Active Directory**</span></span>
3. <span data-ttu-id="bfd9e-187">**사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-187">Click **Users and groups**</span></span>
4. <span data-ttu-id="bfd9e-188">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-188">Click **All users**</span></span>
5. <span data-ttu-id="bfd9e-189">**Multi-Factor Authentication**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-189">Click **Multi-Factor Authentication**</span></span>
6. <span data-ttu-id="bfd9e-190">**Multi-Factor Authentication** 섹션 아래에서 **서비스 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-190">Under **multi-factor authentication** section, select **service settings**</span></span>

   ![서비스 설정 페이지](./media/multi-factor-authentication-get-started-server/servicesettings.png)

6. <span data-ttu-id="bfd9e-192">서비스 설정 페이지의 화면 아래쪽에서 **포털로 이동**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-192">On the services settings page, at the bottom of the screen click **Go to the portal**.</span></span> <span data-ttu-id="bfd9e-193">새 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-193">A new page opens.</span></span>
7. <span data-ttu-id="bfd9e-194">**다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-194">Click **Downloads**.</span></span>
8. <span data-ttu-id="bfd9e-195">**다운로드** 링크를 클릭하고 설치 프로그램을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-195">Click the **Download** link and save the installer.</span></span>

   ![MFA 서버 다운로드](./media/multi-factor-authentication-get-started-server/download4.png)

9. <span data-ttu-id="bfd9e-197">설치 관리자를 실행한 후 참조할 수 있도록 이 페이지를 열어둡니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-197">Keep this page open as we will refer to it after running the installer.</span></span>

## <a name="install-and-configure-the-azure-multi-factor-authentication-server"></a><span data-ttu-id="bfd9e-198">Azure Multi-Factor Authentication 서버 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="bfd9e-198">Install and configure the Azure Multi-Factor Authentication Server</span></span>

<span data-ttu-id="bfd9e-199">서버를 다운로드했으므로 이제 서버를 설치하고 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-199">Now that you have downloaded the server you can install and configure it.</span></span> <span data-ttu-id="bfd9e-200">설치하려는 서버가 계획 섹션에 나열된 요구 사항을 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-200">Be sure that the server you are installing it on meets requirements listed in the planning section.</span></span>

1. <span data-ttu-id="bfd9e-201">실행 파일을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-201">Double-click the executable.</span></span>
2. <span data-ttu-id="bfd9e-202">설치 폴더 선택 화면에서 해당 폴더가 정확한지 확인하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-202">On the Select Installation Folder screen, make sure that the folder is correct and click **Next**.</span></span>
3. <span data-ttu-id="bfd9e-203">설치가 완료되면 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-203">Once the installation is complete, click **Finish**.</span></span>  <span data-ttu-id="bfd9e-204">구성 마법사가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-204">The configuration wizard launches.</span></span>
4. <span data-ttu-id="bfd9e-205">구성 마법사 시작 화면에서 **인증 구성 마법사를 사용하여 건너뛰기**에 체크 표시하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-205">On the configuration wizard welcome screen, check **Skip using the Authentication Configuration Wizard** and click **Next**.</span></span>  <span data-ttu-id="bfd9e-206">마법사가 닫히고 서버가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-206">The wizard closes and the server starts.</span></span>

   ![클라우드](./media/multi-factor-authentication-get-started-server/skip2.png)

5. <span data-ttu-id="bfd9e-208">서버를 다운로드한 페이지로 돌아가서 **정품 인증 자격 증명 생성** 버튼을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-208">Back on the page that we downloaded the server from, click the **Generate Activation Credentials** button.</span></span> <span data-ttu-id="bfd9e-209">이 정보를 제공된 상자의 Azure MFA 서버에 복사하고 **활성화**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-209">Copy this information into the Azure MFA Server in the boxes provided and click **Activate**.</span></span>

## <a name="send-users-an-email"></a><span data-ttu-id="bfd9e-210">사용자에게 전자 메일 보내기</span><span class="sxs-lookup"><span data-stu-id="bfd9e-210">Send users an email</span></span>

<span data-ttu-id="bfd9e-211">출시를 용이하게 하려면 MFA 서버가 사용자와 통신하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-211">To ease rollout, allow MFA Server to communicate with your users.</span></span> <span data-ttu-id="bfd9e-212">MFA 서버는 2단계 인증에 등록되었음을 알리는 전자 메일을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-212">MFA Server can send an email to inform them that they have been enrolled for two-step verification.</span></span>

<span data-ttu-id="bfd9e-213">전자 메일을 보내는 작업은 2단계 인증에 사용자를 구성하는 방법으로 결정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-213">The email you send should be determined by how you configure your users for two-step verification.</span></span> <span data-ttu-id="bfd9e-214">예를 들어, 회사 디렉터리에서 전화 번호를 가져올 수 있었다면 사용자가 예상하는 것을 알 수 있도록 전자 메일에 기본 전화 번호가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-214">For example, if you are able to import phone numbers from the company directory, the email should include the default phone numbers so that users know what to expect.</span></span> <span data-ttu-id="bfd9e-215">전화 번호를 가져오지 않았거나 사용자가 모바일 앱을 사용하려는 경우 해당 계정 등록을 완료하도록 지시하는 이메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-215">If you do not import phone numbers, or your users are going to use the mobile app, send them an email that directs them to complete their account enrollment.</span></span> <span data-ttu-id="bfd9e-216">전자 메일에 Azure Multi-factor Authentication 사용자 포털에 대한 하이퍼링크를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-216">Include a hyperlink to the Azure Multi-Factor Authentication User Portal in the email.</span></span>

<span data-ttu-id="bfd9e-217">또한 전자 메일의 내용은 사용자에 대해 설정된 인증 방법(전화 통화, SMS, 모바일 앱)에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-217">The content of the email also varies depending on the method of verification that has been set for the user (phone call, SMS, or mobile app).</span></span>  <span data-ttu-id="bfd9e-218">예를 들어 사용자가 인증할 때 PIN을 사용해야 하는 경우 전자 메일은 초기 PIN 설정 내용을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-218">For example, if the user is required to use a PIN when they authenticate, the email tells them what their initial PIN has been set to.</span></span>  <span data-ttu-id="bfd9e-219">사용자는 처음 인증할 때 PIN을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-219">Users are required to change their PIN during their first verification.</span></span>

### <a name="configure-email-and-email-templates"></a><span data-ttu-id="bfd9e-220">전자 메일 및 전자 메일 템플릿 구성</span><span class="sxs-lookup"><span data-stu-id="bfd9e-220">Configure email and email templates</span></span>

<span data-ttu-id="bfd9e-221">왼쪽에 있는 전자 메일 아이콘을 클릭하여 이 전자 메일 보내기에 대한 설정을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-221">Click the email icon on the left to set up the settings for sending these emails.</span></span> <span data-ttu-id="bfd9e-222">이 페이지에서는 메일 서버의 SMTP 정보를 입력할 수 있으며 **전자 메일을 사용자에게 보내기** 확인란을 선택하여 전자 메일을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-222">This page is where you can enter the SMTP information of your mail server and send email by checking the **Send emails to users** check box.</span></span>

![MFA 서버 전자 메일 구성](./media/multi-factor-authentication-get-started-server/email1.png)

<span data-ttu-id="bfd9e-224">전자 메일 내용 탭에서 선택할 수 있는 전자 메일 템플릿을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-224">On the Email Content tab, you can see the email templates that are available to choose from.</span></span> <span data-ttu-id="bfd9e-225">사용자가 2단계 인증을 수행하도록 구성한 방법에 따라 가장 적합한 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-225">Depending on how you have configured your users to perform two-step verification, choose the template that best suits you.</span></span>

![MFA 서버 전자 메일 템플릿](./media/multi-factor-authentication-get-started-server/email2.png)

## <a name="import-users-from-active-directory"></a><span data-ttu-id="bfd9e-227">Active Directory에서 사용자 가져오기</span><span class="sxs-lookup"><span data-stu-id="bfd9e-227">Import users from Active Directory</span></span>

<span data-ttu-id="bfd9e-228">이제 서버가 설치되었으므로 사용자를 추가하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-228">Now that the server is installed you will want to add users.</span></span> <span data-ttu-id="bfd9e-229">사용자를 수동으로 만들거나, Active Directory에서 사용자를 가져오거나, Active Directory와 자동 동기화를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-229">You can choose to create them manually, import users from Active Directory, or configure automated synchronization with Active Directory.</span></span>

### <a name="manual-import-from-active-directory"></a><span data-ttu-id="bfd9e-230">Active Directory에서 수동 가져오기</span><span class="sxs-lookup"><span data-stu-id="bfd9e-230">Manual import from Active Directory</span></span>

1. <span data-ttu-id="bfd9e-231">Azure MFA 서버의 왼쪽에서 **사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-231">In the Azure MFA Server, on the left, select **Users**.</span></span>
2. <span data-ttu-id="bfd9e-232">아래쪽에서 **Active Directory에서 가져오기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-232">At the bottom, select **Import from Active Directory**.</span></span>
3. <span data-ttu-id="bfd9e-233">이제 개별 사용자를 검색하거나 해당 사용자로 OU에 대한 AD 디렉터리를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-233">Now you can either search for individual users or search the AD directory for OUs with users in them.</span></span>  <span data-ttu-id="bfd9e-234">이 경우 사용자 OU를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-234">In this case, we specify the users OU.</span></span>
4. <span data-ttu-id="bfd9e-235">오른쪽의 모든 사용자를 강조 표시하고 **가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-235">Highlight all the users on the right and click **Import**.</span></span>  <span data-ttu-id="bfd9e-236">성공했음을 알려주는 팝업 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-236">You should receive a pop-up telling you that you were successful.</span></span>  <span data-ttu-id="bfd9e-237">가져오기 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-237">Close the import window.</span></span>

   ![MFA 서버 사용자 가져오기](./media/multi-factor-authentication-get-started-server/import2.png)

### <a name="automated-synchronization-with-active-directory"></a><span data-ttu-id="bfd9e-239">Active Directory와 자동 동기화</span><span class="sxs-lookup"><span data-stu-id="bfd9e-239">Automated synchronization with Active Directory</span></span>

1. <span data-ttu-id="bfd9e-240">Azure MFA 서버의 왼쪽에서 **디렉터리 통합**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-240">In the Azure MFA Server, on the left, select **Directory Integration**.</span></span>
2. <span data-ttu-id="bfd9e-241">**동기화** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-241">Navigate to the **Synchronization** tab.</span></span>
3. <span data-ttu-id="bfd9e-242">아래에서 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-242">At the bottom, choose **Add**</span></span>
4. <span data-ttu-id="bfd9e-243">나타나는 **동기화 항목 추가** 상자에서 도메인, OU **또는** 보안 그룹, 설정, 메서드 기본값 및 이 동기화 작업의 기본 언어를 선택하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-243">In the **Add Synchronization Item** box that appears choose the Domain, OU **or** security group, Settings, Method Defaults, and Language Defaults for this synchronization task and click **Add**.</span></span>
5. <span data-ttu-id="bfd9e-244">레이블이 지정된 **Active Directory와 동기화 사용** 확인란을 선택하고 **동기화 간격**을 1분에서 24시간 사이로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-244">Check the box labeled **Enable synchronization with Active Directory** and choose a **Synchronization interval** between one minute and 24 hours.</span></span>

## <a name="how-the-azure-multi-factor-authentication-server-handles-user-data"></a><span data-ttu-id="bfd9e-245">Azure Multi-Factor Authentication 서버에서 사용자 데이터를 처리하는 방법</span><span class="sxs-lookup"><span data-stu-id="bfd9e-245">How the Azure Multi-Factor Authentication Server handles user data</span></span>

<span data-ttu-id="bfd9e-246">MFA(Multi-Factor Authentication) 서버 온-프레미스를 사용하면 사용자의 데이터가 온-프레미스 서버에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-246">When you use the Multi-Factor Authentication (MFA) Server on-premises, a user’s data is stored in the on-premises servers.</span></span> <span data-ttu-id="bfd9e-247">영구 사용자 데이터는 클라우드에 저장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-247">No persistent user data is stored in the cloud.</span></span> <span data-ttu-id="bfd9e-248">사용자가 2단계 인증을 수행하면 MFA 서버가 인증을 수행할 Azure MFA 클라우드 서비스에 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-248">When the user performs a two-step verification, the MFA Server sends data to the Azure MFA cloud service to perform the verification.</span></span> <span data-ttu-id="bfd9e-249">이러한 인증 요청이 클라우드 서비스에 전송되면 다음 필드가 요청 및 로그에 전송되어 고객의 인증/사용 보고서에서 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-249">When these authentication requests are sent to the cloud service, the following fields are sent in the request and logs so that they are available in the customer's authentication/usage reports.</span></span> <span data-ttu-id="bfd9e-250">일부 필드는 선택 사항이므로 Multi-Factor Authentication 서버 내에서 사용하거나 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-250">Some of the fields are optional so they can be enabled or disabled within the Multi-Factor Authentication Server.</span></span> <span data-ttu-id="bfd9e-251">MFA 서버에서 MFA 클라우드 서비스로의 통신은 포트 443 아웃바운드를 통해 연결된 SSL/TLS를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-251">The communication from the MFA Server to the MFA cloud service uses SSL/TLS over port 443 outbound.</span></span> <span data-ttu-id="bfd9e-252">이러한 필드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-252">These fields are:</span></span>

* <span data-ttu-id="bfd9e-253">고유 ID - 사용자 이름 또는 내부 MFA 서버 ID </span><span class="sxs-lookup"><span data-stu-id="bfd9e-253">Unique ID - either username or internal MFA server ID</span></span>
* <span data-ttu-id="bfd9e-254">이름과 성(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="bfd9e-254">First and last name (optional)</span></span>
* <span data-ttu-id="bfd9e-255">메일 주소(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="bfd9e-255">Email address (optional)</span></span>
* <span data-ttu-id="bfd9e-256">전화 번호 - 음성 통화 또는 SMS 인증을 수행할 때</span><span class="sxs-lookup"><span data-stu-id="bfd9e-256">Phone number - when doing a voice call or SMS authentication</span></span>
* <span data-ttu-id="bfd9e-257">장치 토큰 - 모바일 앱 인증을 수행할 때</span><span class="sxs-lookup"><span data-stu-id="bfd9e-257">Device token - when doing mobile app authentication</span></span>
* <span data-ttu-id="bfd9e-258">인증 모드</span><span class="sxs-lookup"><span data-stu-id="bfd9e-258">Authentication mode</span></span>
* <span data-ttu-id="bfd9e-259">인증 결과</span><span class="sxs-lookup"><span data-stu-id="bfd9e-259">Authentication result</span></span>
* <span data-ttu-id="bfd9e-260">MFA 서버 이름</span><span class="sxs-lookup"><span data-stu-id="bfd9e-260">MFA Server name</span></span>
* <span data-ttu-id="bfd9e-261">MFA 서버 IP</span><span class="sxs-lookup"><span data-stu-id="bfd9e-261">MFA Server IP</span></span>
* <span data-ttu-id="bfd9e-262">클라이언트 IP - 사용 가능한 경우</span><span class="sxs-lookup"><span data-stu-id="bfd9e-262">Client IP – if available</span></span>

<span data-ttu-id="bfd9e-263">위의 필드 외에도 인증 결과(성공/거부) 및 모든 거부 사유는 인증 데이터와 함께 저장되어 인증/사용 보고서를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-263">In addition to the fields above, the verification result (success/denial) and reason for any denials is also stored with the authentication data and available through the authentication/usage reports.</span></span>

## <a name="back-up-and-restore-azure-mfa-server"></a><span data-ttu-id="bfd9e-264">Azure MFA 서버 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="bfd9e-264">Back up and restore Azure MFA Server</span></span>

<span data-ttu-id="bfd9e-265">백업을 설정하는 것은 모든 시스템에서 수행할 중요한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-265">Making sure that you have a good backup is an important step to take with any system.</span></span>

<span data-ttu-id="bfd9e-266">Azure MFA 서버를 백업하려면 **PhoneFactor.pfdata** 파일을 포함한 **C:\Program Files\Multi-Factor Authentication Server\Data** 폴더의 복사본을 가지고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-266">To back up Azure MFA Server, ensure that you have a copy of the **C:\Program Files\Multi-Factor Authentication Server\Data** folder including the **PhoneFactor.pfdata** file.</span></span> 

<span data-ttu-id="bfd9e-267">복원이 필요한 경우에 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-267">In case a restore is needed complete the following steps:</span></span>

1. <span data-ttu-id="bfd9e-268">새 서버에 Azure MFA 서버를 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-268">Reinstall Azure MFA Server on a new server.</span></span>
2. <span data-ttu-id="bfd9e-269">새 Azure MFA 서버를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-269">Activate the new Azure MFA Server.</span></span>
3. <span data-ttu-id="bfd9e-270">**MultiFactorAuth** 서비스를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-270">Stop the **MultiFactorAuth** service.</span></span>
4. <span data-ttu-id="bfd9e-271">**PhoneFactor.pfdata**를 백업된 복사본으로 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-271">Overwrite the **PhoneFactor.pfdata** with the backed up copy.</span></span>
5. <span data-ttu-id="bfd9e-272">**MultiFactorAuth** 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-272">Start the **MultiFactorAuth** service.</span></span>

<span data-ttu-id="bfd9e-273">이제 원래 백업된 구성 및 사용자 데이터를 사용하여 새 서버가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-273">The new server is now up and running with the original backed-up configuration and user data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfd9e-274">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bfd9e-274">Next steps</span></span>

- <span data-ttu-id="bfd9e-275">사용자 셀프 서비스를 위해 [사용자 포털](multi-factor-authentication-get-started-portal.md)을 설정 및 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-275">Set up and configure the [User Portal](multi-factor-authentication-get-started-portal.md) for user self-service.</span></span>
- <span data-ttu-id="bfd9e-276">[Active Directory Federation Service](multi-factor-authentication-get-started-adfs.md), [RADIUS 인증](multi-factor-authentication-get-started-server-radius.md) 또는 [LDAP 인증](multi-factor-authentication-get-started-server-ldap.md)을 사용하여 Azure MFA 서버를 설정하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-276">Set up and configure the Azure MFA Server with [Active Directory Federation Service](multi-factor-authentication-get-started-adfs.md), [RADIUS Authentication](multi-factor-authentication-get-started-server-radius.md), or [LDAP Authentication](multi-factor-authentication-get-started-server-ldap.md).</span></span>
- <span data-ttu-id="bfd9e-277">[RADIUS를 사용하여 원격 데스크톱 게이트웨이 및 Azure Multi-Factor Authentication 서버](multi-factor-authentication-get-started-server-rdg.md)를 설정 및 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="bfd9e-277">Set up and configure [Remote Desktop Gateway and Azure Multi-Factor Authentication Server using RADIUS](multi-factor-authentication-get-started-server-rdg.md).</span></span>
- <span data-ttu-id="bfd9e-278">[Azure Multi-Factor Authentication 서버 모바일 앱 웹 서비스 배포](multi-factor-authentication-get-started-server-webservice.md)</span><span class="sxs-lookup"><span data-stu-id="bfd9e-278">[Deploy the Azure Multi-Factor Authentication Server Mobile App Web Service](multi-factor-authentication-get-started-server-webservice.md).</span></span>
- <span data-ttu-id="bfd9e-279">[Azure Multi-Factor Authentication 및 타사 VPN을 사용한 고급 시나리오](multi-factor-authentication-advanced-vpn-configurations.md)</span><span class="sxs-lookup"><span data-stu-id="bfd9e-279">[Advanced scenarios with Azure Multi-Factor Authentication and third-party VPNs](multi-factor-authentication-advanced-vpn-configurations.md).</span></span>
