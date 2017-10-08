---
title: "aaaGetting Azure Multi-factor Authentication 서버를 시작 | Microsoft Docs"
description: "Tooget Azure MFA 서버를 시작 하는 방법을 설명 하는 hello Azure multi-factor authentication 페이지입니다."
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
ms.openlocfilehash: 92a6a586eb96375e92a9455ad64e67221001db81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-multi-factor-authentication-server"></a><span data-ttu-id="2414b-104">Azure Multi-factor Authentication 서버 hello로 시작</span><span class="sxs-lookup"><span data-stu-id="2414b-104">Getting started with hello Azure Multi-Factor Authentication Server</span></span>

<span data-ttu-id="2414b-105"><center>![MFA 온-프레미스](./media/multi-factor-authentication-get-started-server/server2.png)</center></span><span class="sxs-lookup"><span data-stu-id="2414b-105"><center>![MFA on-premises](./media/multi-factor-authentication-get-started-server/server2.png)</center></span></span>

<span data-ttu-id="2414b-106">Toouse 온-프레미스 Multi-factor Authentication 서버를 결정 했으므로 출발 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-106">Now that we have determined toouse on-premises Multi-Factor Authentication Server, let’s get going.</span></span> <span data-ttu-id="2414b-107">이 페이지에서는 hello 서버와 온-프레미스 Active directory 설정의 새 설치에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-107">This page covers a new installation of hello server and setting it up with on-premises Active Directory.</span></span> <span data-ttu-id="2414b-108">Hello MFA 서버 설치 이미 있고 tooupgrade 확인 하려는 경우 참조 [toohello 업그레이드 최신 Azure Multi-factor Authentication 서버](multi-factor-authentication-server-upgrade.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-108">If you already have hello MFA server installed and are looking tooupgrade, see [Upgrade toohello latest Azure Multi-Factor Authentication Server](multi-factor-authentication-server-upgrade.md).</span></span> <span data-ttu-id="2414b-109">방금 hello 웹 서비스 설치에 대 한 내용은 찾고 있는 경우 참조 [배포 hello Azure Multi-factor Authentication 서버 모바일 앱 웹 서비스](multi-factor-authentication-get-started-server-webservice.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-109">If you're looking for information on installing just hello web service, see [Deploying hello Azure Multi-Factor Authentication Server Mobile App Web Service](multi-factor-authentication-get-started-server-webservice.md).</span></span>

## <a name="plan-your-deployment"></a><span data-ttu-id="2414b-110">배포 계획</span><span class="sxs-lookup"><span data-stu-id="2414b-110">Plan your deployment</span></span>

<span data-ttu-id="2414b-111">Hello Azure Multi-factor Authentication 서버를 다운로드 하기 전에 부하 및 고가용성 요구 사항 이란에 대해 생각 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-111">Before you download hello Azure Multi-Factor Authentication Server, think about what your load and high availability requirements are.</span></span> <span data-ttu-id="2414b-112">이 정보 toodecide 위치와 방법을 사용 하 여 toodeploy 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-112">Use this information toodecide how and where toodeploy.</span></span>

<span data-ttu-id="2414b-113">좋은 지침은 정기적으로 tooauthenticate 원하는 hello 필요한 메모리 양은 사용자 수가 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-113">A good guideline for hello amount of memory you need is hello number of users you expect tooauthenticate on a regular basis.</span></span>

| <span data-ttu-id="2414b-114">사용자</span><span class="sxs-lookup"><span data-stu-id="2414b-114">Users</span></span> | <span data-ttu-id="2414b-115">RAM</span><span class="sxs-lookup"><span data-stu-id="2414b-115">RAM</span></span> |
| ----- | --- |
| <span data-ttu-id="2414b-116">1-10,000</span><span class="sxs-lookup"><span data-stu-id="2414b-116">1-10,000</span></span> | <span data-ttu-id="2414b-117">4GB</span><span class="sxs-lookup"><span data-stu-id="2414b-117">4 GB</span></span> |
| <span data-ttu-id="2414b-118">10,001-50,000</span><span class="sxs-lookup"><span data-stu-id="2414b-118">10,001-50,000</span></span> | <span data-ttu-id="2414b-119">8GB</span><span class="sxs-lookup"><span data-stu-id="2414b-119">8 GB</span></span> |
| <span data-ttu-id="2414b-120">50,001-100,000</span><span class="sxs-lookup"><span data-stu-id="2414b-120">50,001-100,000</span></span> | <span data-ttu-id="2414b-121">12GB</span><span class="sxs-lookup"><span data-stu-id="2414b-121">12 GB</span></span> |
| <span data-ttu-id="2414b-122">100,000-200,001</span><span class="sxs-lookup"><span data-stu-id="2414b-122">100,000-200,001</span></span> | <span data-ttu-id="2414b-123">16GB</span><span class="sxs-lookup"><span data-stu-id="2414b-123">16 GB</span></span> |
| <span data-ttu-id="2414b-124">200,001+</span><span class="sxs-lookup"><span data-stu-id="2414b-124">200,001+</span></span> | <span data-ttu-id="2414b-125">32GB</span><span class="sxs-lookup"><span data-stu-id="2414b-125">32 GB</span></span> |

<span data-ttu-id="2414b-126">고가용성을 위해 여러 서버를 tooset 필요 하거나 부하 분산 수행 했습니까?</span><span class="sxs-lookup"><span data-stu-id="2414b-126">Do you need tooset up multiple servers for high availability or load balancing?</span></span> <span data-ttu-id="2414b-127">이 구성을 Azure MFA 서버와 같은 방법으로 tooset의 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-127">There are a number of ways tooset up this configuration with Azure MFA Server.</span></span> <span data-ttu-id="2414b-128">첫 번째 Azure MFA 서버를 설치 하면 hello 마스터 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-128">When you install your first Azure MFA Server, it becomes hello master.</span></span> <span data-ttu-id="2414b-129">서버를 더 하위 수준 해지고 hello 마스터와 사용자 및 구성 작업을 자동으로 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-129">Any additional servers become subordinate, and automatically synchronize users and configuration with hello master.</span></span> <span data-ttu-id="2414b-130">그런 다음 주 서버를 구성할 수 있으며 역할 hello rest는 백업 또는 있습니다 모든 hello 서버 간의 부하 분산을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-130">Then, you can configure one primary server and have hello rest act as backup, or you can set up load balancing among all hello servers.</span></span>

<span data-ttu-id="2414b-131">Azure MFA 서버 마스터 되 면 오프 라인, 하위 서버 hello 계속 프로세스 2 단계 확인 요청 수입니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-131">When a master Azure MFA Server goes offline, hello subordinate servers can still process two-step verification requests.</span></span> <span data-ttu-id="2414b-132">그러나 추가할 수 없는 새 사용자 및 기존 사용자 hello 마스터는 온라인 또는 하위 항목이 승격 될 때까지 해당 설정을 업데이트할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-132">However, you can't add new users and existing users can't update their settings until hello master is back online or a subordinate gets promoted.</span></span>

### <a name="prepare-your-environment"></a><span data-ttu-id="2414b-133">환경 준비</span><span class="sxs-lookup"><span data-stu-id="2414b-133">Prepare your environment</span></span>

<span data-ttu-id="2414b-134">Azure Multi-factor Authentication을 사용 하는 hello 서버 hello 요구 사항을 준수를 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-134">Make sure hello server  that you're using for Azure Multi-Factor Authentication meets hello following requirements:</span></span>

| <span data-ttu-id="2414b-135">Azure Multi-Factor Authentication 서버 요구 사항</span><span class="sxs-lookup"><span data-stu-id="2414b-135">Azure Multi-Factor Authentication Server Requirements</span></span> | <span data-ttu-id="2414b-136">설명</span><span class="sxs-lookup"><span data-stu-id="2414b-136">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2414b-137">하드웨어</span><span class="sxs-lookup"><span data-stu-id="2414b-137">Hardware</span></span> |<li><span data-ttu-id="2414b-138">200MB의 하드 디스크 공간</span><span class="sxs-lookup"><span data-stu-id="2414b-138">200 MB of hard disk space</span></span></li><li><span data-ttu-id="2414b-139">x32 또는 x64 지원 프로세서</span><span class="sxs-lookup"><span data-stu-id="2414b-139">x32 or x64 capable processor</span></span></li><li><span data-ttu-id="2414b-140">1GB 이상 RAM</span><span class="sxs-lookup"><span data-stu-id="2414b-140">1 GB or greater RAM</span></span></li> |
| <span data-ttu-id="2414b-141">소프트웨어</span><span class="sxs-lookup"><span data-stu-id="2414b-141">Software</span></span> |<li><span data-ttu-id="2414b-142">Windows Server 2008 이상이 hello 호스트 서버인 경우 운영 체제</span><span class="sxs-lookup"><span data-stu-id="2414b-142">Windows Server 2008 or greater if hello host is a server OS</span></span></li><li><span data-ttu-id="2414b-143">Windows 7 또는 hello 호스트는 클라이언트 OS 증가 하면</span><span class="sxs-lookup"><span data-stu-id="2414b-143">Windows 7 or greater if hello host is a client OS</span></span></li><li><span data-ttu-id="2414b-144">Microsoft .NET 4.0 Framework</span><span class="sxs-lookup"><span data-stu-id="2414b-144">Microsoft .NET 4.0 Framework</span></span></li><li><span data-ttu-id="2414b-145">IIS 7.0 또는 설치 하는 경우 큰 hello 사용자 포털 또는 웹 서비스 SDK</span><span class="sxs-lookup"><span data-stu-id="2414b-145">IIS 7.0 or greater if installing hello user portal or web service SDK</span></span></li> |

### <a name="azure-mfa-server-components"></a><span data-ttu-id="2414b-146">Azure MFA 서버 구성 요소</span><span class="sxs-lookup"><span data-stu-id="2414b-146">Azure MFA Server Components</span></span>

<span data-ttu-id="2414b-147">Azure MFA 서버를 구성하는 세 가지 웹 구성 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-147">There are three web components that make up Azure MFA Server:</span></span>

* <span data-ttu-id="2414b-148">웹 서비스 SDK-통신할 때 다른 구성 요소를 hello 및 hello Azure MFA 응용 프로그램 서버에 설치 되어 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="2414b-148">Web Service SDK - Enables communication with hello other components and is installed on hello Azure MFA application server</span></span>
* <span data-ttu-id="2414b-149">사용자 포털-사용자가 tooenroll Azure Multi-factor Authentication (MFA)를 허용 하 고 자신의 계정을 관리할 수 있는 IIS 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-149">User Portal - An IIS web site that allows users tooenroll in Azure Multi-Factor Authentication (MFA) and maintain their accounts.</span></span>
* <span data-ttu-id="2414b-150">모바일 앱 웹 서비스-2 단계 인증에 대 한 hello Microsoft Authenticator 앱 처럼 모바일 앱을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-150">Mobile App Web Service - Enables using a mobile app like hello Microsoft Authenticator app for two-step verification.</span></span>

<span data-ttu-id="2414b-151">Hello에 모든 세 가지 구성 요소를 설치할 수 있습니다 동일한 서버 hello 서버는 인터넷에 연결 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="2414b-151">All three components can be installed on hello same server if hello server is internet-facing.</span></span> <span data-ttu-id="2414b-152">웹 서비스 SDK hello hello Azure MFA 응용 프로그램 서버에 설치 된 hello 구성 요소를 해제 하는 경우 및 hello 사용자 포털 및 모바일 앱 웹 서비스는 인터넷 연결 서버에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-152">If breaking up hello components, hello Web Service SDK is installed on hello Azure MFA application server and hello User Portal and Mobile App Web Service are installed on an internet-facing server.</span></span>

### <a name="azure-multi-factor-authentication-server-firewall-requirements"></a><span data-ttu-id="2414b-153">Azure Multi-Factor Authentication 방화벽 요구 사항</span><span class="sxs-lookup"><span data-stu-id="2414b-153">Azure Multi-Factor Authentication Server firewall requirements</span></span>

<span data-ttu-id="2414b-154">각 MFA 서버 포트 443 아웃 바운드 toohello 주소 다음에 수 toocommunicate 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-154">Each MFA server must be able toocommunicate on port 443 outbound toohello following addresses:</span></span>

* <span data-ttu-id="2414b-155">https://pfd.phonefactor.net</span><span class="sxs-lookup"><span data-stu-id="2414b-155">https://pfd.phonefactor.net</span></span>
* <span data-ttu-id="2414b-156">https://pfd2.phonefactor.net</span><span class="sxs-lookup"><span data-stu-id="2414b-156">https://pfd2.phonefactor.net</span></span>
* <span data-ttu-id="2414b-157">https://css.phonefactor.net</span><span class="sxs-lookup"><span data-stu-id="2414b-157">https://css.phonefactor.net</span></span>

<span data-ttu-id="2414b-158">포트 443에서 아웃 바운드 방화벽이 제한 된, hello 다음 IP 주소 범위를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-158">If outbound firewalls are restricted on port 443, open hello following IP address ranges:</span></span>

| <span data-ttu-id="2414b-159">IP 서브넷</span><span class="sxs-lookup"><span data-stu-id="2414b-159">IP Subnet</span></span> | <span data-ttu-id="2414b-160">네트워크 마스크</span><span class="sxs-lookup"><span data-stu-id="2414b-160">Netmask</span></span> | <span data-ttu-id="2414b-161">IP 범위</span><span class="sxs-lookup"><span data-stu-id="2414b-161">IP Range</span></span> |
|:---: |:---: |:---: |
| <span data-ttu-id="2414b-162">134.170.116.0/25</span><span class="sxs-lookup"><span data-stu-id="2414b-162">134.170.116.0/25</span></span> |<span data-ttu-id="2414b-163">255.255.255.128</span><span class="sxs-lookup"><span data-stu-id="2414b-163">255.255.255.128</span></span> |<span data-ttu-id="2414b-164">134.170.116.1 – 134.170.116.126</span><span class="sxs-lookup"><span data-stu-id="2414b-164">134.170.116.1 – 134.170.116.126</span></span> |
| <span data-ttu-id="2414b-165">134.170.165.0/25</span><span class="sxs-lookup"><span data-stu-id="2414b-165">134.170.165.0/25</span></span> |<span data-ttu-id="2414b-166">255.255.255.128</span><span class="sxs-lookup"><span data-stu-id="2414b-166">255.255.255.128</span></span> |<span data-ttu-id="2414b-167">134.170.165.1 – 134.170.165.126</span><span class="sxs-lookup"><span data-stu-id="2414b-167">134.170.165.1 – 134.170.165.126</span></span> |
| <span data-ttu-id="2414b-168">70.37.154.128/25</span><span class="sxs-lookup"><span data-stu-id="2414b-168">70.37.154.128/25</span></span> |<span data-ttu-id="2414b-169">255.255.255.128</span><span class="sxs-lookup"><span data-stu-id="2414b-169">255.255.255.128</span></span> |<span data-ttu-id="2414b-170">70.37.154.129 – 70.37.154.254</span><span class="sxs-lookup"><span data-stu-id="2414b-170">70.37.154.129 – 70.37.154.254</span></span> |

<span data-ttu-id="2414b-171">Hello 이벤트 확인 기능을 사용 하지 않는 경우 사용자가 장치에서 모바일 앱 tooverify를 hello 회사 네트워크에서 사용 하지 않는 hello 범위를 수행 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-171">If you aren't using hello Event Confirmation feature, and your users aren't using mobile apps tooverify from devices on hello corporate network, you only need hello following ranges:</span></span>

| <span data-ttu-id="2414b-172">IP 서브넷</span><span class="sxs-lookup"><span data-stu-id="2414b-172">IP Subnet</span></span> | <span data-ttu-id="2414b-173">네트워크 마스크</span><span class="sxs-lookup"><span data-stu-id="2414b-173">Netmask</span></span> | <span data-ttu-id="2414b-174">IP 범위</span><span class="sxs-lookup"><span data-stu-id="2414b-174">IP Range</span></span> |
|:---: |:---: |:---: |
| <span data-ttu-id="2414b-175">134.170.116.72/29</span><span class="sxs-lookup"><span data-stu-id="2414b-175">134.170.116.72/29</span></span> |<span data-ttu-id="2414b-176">255.255.255.248</span><span class="sxs-lookup"><span data-stu-id="2414b-176">255.255.255.248</span></span> |<span data-ttu-id="2414b-177">134.170.116.72 – 134.170.116.79</span><span class="sxs-lookup"><span data-stu-id="2414b-177">134.170.116.72 – 134.170.116.79</span></span> |
| <span data-ttu-id="2414b-178">134.170.165.72/29</span><span class="sxs-lookup"><span data-stu-id="2414b-178">134.170.165.72/29</span></span> |<span data-ttu-id="2414b-179">255.255.255.248</span><span class="sxs-lookup"><span data-stu-id="2414b-179">255.255.255.248</span></span> |<span data-ttu-id="2414b-180">134.170.165.72 – 134.170.165.79</span><span class="sxs-lookup"><span data-stu-id="2414b-180">134.170.165.72 – 134.170.165.79</span></span> |
| <span data-ttu-id="2414b-181">70.37.154.200/29</span><span class="sxs-lookup"><span data-stu-id="2414b-181">70.37.154.200/29</span></span> |<span data-ttu-id="2414b-182">255.255.255.248</span><span class="sxs-lookup"><span data-stu-id="2414b-182">255.255.255.248</span></span> |<span data-ttu-id="2414b-183">70.37.154.201 – 70.37.154.206</span><span class="sxs-lookup"><span data-stu-id="2414b-183">70.37.154.201 – 70.37.154.206</span></span> |

## <a name="download-hello-azure-multi-factor-authentication-server"></a><span data-ttu-id="2414b-184">Hello Azure Multi-factor Authentication 서버 다운로드</span><span class="sxs-lookup"><span data-stu-id="2414b-184">Download hello Azure Multi-Factor Authentication Server</span></span>

1. <span data-ttu-id="2414b-185">Toohello 로그인 [Azure 포털](https://portal.azure.com) 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-185">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="2414b-186">Hello 왼쪽에서 선택 **Active Directory**</span><span class="sxs-lookup"><span data-stu-id="2414b-186">On hello left, select **Active Directory**</span></span>
3. <span data-ttu-id="2414b-187">**사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-187">Click **Users and groups**</span></span>
4. <span data-ttu-id="2414b-188">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-188">Click **All users**</span></span>
5. <span data-ttu-id="2414b-189">**Multi-Factor Authentication**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-189">Click **Multi-Factor Authentication**</span></span>
6. <span data-ttu-id="2414b-190">**Multi-Factor Authentication** 섹션 아래에서 **서비스 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-190">Under **multi-factor authentication** section, select **service settings**</span></span>

   ![서비스 설정 페이지](./media/multi-factor-authentication-get-started-server/servicesettings.png)

6. <span data-ttu-id="2414b-192">Hello 서비스 설정 페이지에서 클릭에 hello hello 화면 맨 아래에 **Go toohello 포털**합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-192">On hello services settings page, at hello bottom of hello screen click **Go toohello portal**.</span></span> <span data-ttu-id="2414b-193">새 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-193">A new page opens.</span></span>
7. <span data-ttu-id="2414b-194">**다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-194">Click **Downloads**.</span></span>
8. <span data-ttu-id="2414b-195">Hello 클릭 **다운로드** 연결 하 고 hello 설치 관리자를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-195">Click hello **Download** link and save hello installer.</span></span>

   ![MFA 서버 다운로드](./media/multi-factor-authentication-get-started-server/download4.png)

9. <span data-ttu-id="2414b-197">이 페이지 하므로 계속 열어둡니다 tooit hello 설치 관리자를 실행 한 후 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-197">Keep this page open as we will refer tooit after running hello installer.</span></span>

## <a name="install-and-configure-hello-azure-multi-factor-authentication-server"></a><span data-ttu-id="2414b-198">설치 하 고 hello Azure Multi-factor Authentication 서버를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-198">Install and configure hello Azure Multi-Factor Authentication Server</span></span>

<span data-ttu-id="2414b-199">다운로드 한 hello 서버를 설치 하 고 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-199">Now that you have downloaded hello server you can install and configure it.</span></span> <span data-ttu-id="2414b-200">해당 hello 서버에 설치 하는 hello 계획 섹션에에서 나열 된 요구 사항을 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-200">Be sure that hello server you are installing it on meets requirements listed in hello planning section.</span></span>

1. <span data-ttu-id="2414b-201">Hello 실행 파일을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-201">Double-click hello executable.</span></span>
2. <span data-ttu-id="2414b-202">Hello 설치 폴더 선택 화면에서 해당 hello 폴더가 올바른지 확인 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-202">On hello Select Installation Folder screen, make sure that hello folder is correct and click **Next**.</span></span>
3. <span data-ttu-id="2414b-203">Hello 설치가 완료 되 면 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-203">Once hello installation is complete, click **Finish**.</span></span>  <span data-ttu-id="2414b-204">hello 구성 마법사를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-204">hello configuration wizard launches.</span></span>
4. <span data-ttu-id="2414b-205">Hello 구성 마법사 시작 화면에서 확인 **Skip을 사용 하 여 hello 인증 구성 마법사** 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-205">On hello configuration wizard welcome screen, check **Skip using hello Authentication Configuration Wizard** and click **Next**.</span></span>  <span data-ttu-id="2414b-206">hello 마법사가 닫히고 hello 서버를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-206">hello wizard closes and hello server starts.</span></span>

   ![클라우드](./media/multi-factor-authentication-get-started-server/skip2.png)

5. <span data-ttu-id="2414b-208">다시 hello 페이지 hello 서버에서 다운로드 한 म 클릭 hello **활성화 자격 증명 생성** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-208">Back on hello page that we downloaded hello server from, click hello **Generate Activation Credentials** button.</span></span> <span data-ttu-id="2414b-209">제공 된 hello 상자에 Azure MFA 서버 hello에이 정보를 복사 하 고 클릭 **Activate**합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-209">Copy this information into hello Azure MFA Server in hello boxes provided and click **Activate**.</span></span>

## <a name="send-users-an-email"></a><span data-ttu-id="2414b-210">사용자에게 전자 메일 보내기</span><span class="sxs-lookup"><span data-stu-id="2414b-210">Send users an email</span></span>

<span data-ttu-id="2414b-211">tooease 롤아웃, 사용자와 MFA 서버 toocommunicate 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-211">tooease rollout, allow MFA Server toocommunicate with your users.</span></span> <span data-ttu-id="2414b-212">MFA 서버에서 전자 메일 tooinform를 보낼 수에 2 단계 인증에 등록 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-212">MFA Server can send an email tooinform them that they have been enrolled for two-step verification.</span></span>

<span data-ttu-id="2414b-213">hello 전자 메일을 보내는 2 단계 인증에 대 한 사용자가 구성 하는 방법가 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-213">hello email you send should be determined by how you configure your users for two-step verification.</span></span> <span data-ttu-id="2414b-214">예를 들어 hello 회사 디렉터리에서 전화 번호 수 tooimport 인 경우 사용자가 어떤 tooexpect 알 수 있도록 hello 전자 메일 hello 기본 전화 번호를 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-214">For example, if you are able tooimport phone numbers from hello company directory, hello email should include hello default phone numbers so that users know what tooexpect.</span></span> <span data-ttu-id="2414b-215">전화 번호를 가져오지 않으면 또는 사용자가 toouse hello 모바일 응용 프로그램 의도 보냅니다 toocomplete 안내 전자 메일 계정 등록.</span><span class="sxs-lookup"><span data-stu-id="2414b-215">If you do not import phone numbers, or your users are going toouse hello mobile app, send them an email that directs them toocomplete their account enrollment.</span></span> <span data-ttu-id="2414b-216">Hello 전자 메일에 하이퍼링크 toohello Azure Multi-factor Authentication 사용자 포털을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-216">Include a hyperlink toohello Azure Multi-Factor Authentication User Portal in hello email.</span></span>

<span data-ttu-id="2414b-217">hello 전자 메일의 hello 콘텐츠 hello 사용자 (전화 통화, SMS 또는 모바일 앱)에 대해 설정 된 확인의 hello 방법에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-217">hello content of hello email also varies depending on hello method of verification that has been set for hello user (phone call, SMS, or mobile app).</span></span>  <span data-ttu-id="2414b-218">예를 들어 hello에서 사용자가 경우 필요한 toouse PIN 인증 시 hello 전자 메일 ¿ë à ú으로 어떤 초기 PIN 설정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-218">For example, if hello user is required toouse a PIN when they authenticate, hello email tells them what their initial PIN has been set to.</span></span>  <span data-ttu-id="2414b-219">사용자가 해당 첫 번째 확인 하는 동안 필요한 toochange PIN 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-219">Users are required toochange their PIN during their first verification.</span></span>

### <a name="configure-email-and-email-templates"></a><span data-ttu-id="2414b-220">전자 메일 및 전자 메일 템플릿 구성</span><span class="sxs-lookup"><span data-stu-id="2414b-220">Configure email and email templates</span></span>

<span data-ttu-id="2414b-221">이러한 전자 메일을 보내기 위한 hello 설정이 왼쪽된 tooset hello에 hello 전자 메일 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-221">Click hello email icon on hello left tooset up hello settings for sending these emails.</span></span> <span data-ttu-id="2414b-222">이 페이지는 hello를 확인 하 여 메일 서버와 송신 전자 메일의 SMTP hello 정보를 입력할 수 있는 **송신 toousers 전자 메일로** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-222">This page is where you can enter hello SMTP information of your mail server and send email by checking hello **Send emails toousers** check box.</span></span>

![MFA 서버 전자 메일 구성](./media/multi-factor-authentication-get-started-server/email1.png)

<span data-ttu-id="2414b-224">Hello 전자 메일 내용 탭에서 사용할 수 있는 toochoose 있는 hello 전자 메일 템플릿을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-224">On hello Email Content tab, you can see hello email templates that are available toochoose from.</span></span> <span data-ttu-id="2414b-225">사용자가 한 tooperform 2 단계 확인을 구성 방식에 따라 하기에 가장 적합 한 hello 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-225">Depending on how you have configured your users tooperform two-step verification, choose hello template that best suits you.</span></span>

![MFA 서버 전자 메일 템플릿](./media/multi-factor-authentication-get-started-server/email2.png)

## <a name="import-users-from-active-directory"></a><span data-ttu-id="2414b-227">Active Directory에서 사용자 가져오기</span><span class="sxs-lookup"><span data-stu-id="2414b-227">Import users from Active Directory</span></span>

<span data-ttu-id="2414b-228">해당 hello 서버가 설치 되어 이제 tooadd 사용자 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-228">Now that hello server is installed you will want tooadd users.</span></span> <span data-ttu-id="2414b-229">Toocreate 수동으로 Active Directory에서 사용자 가져오기 또는 Active Directory와 자동된 동기화를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-229">You can choose toocreate them manually, import users from Active Directory, or configure automated synchronization with Active Directory.</span></span>

### <a name="manual-import-from-active-directory"></a><span data-ttu-id="2414b-230">Active Directory에서 수동 가져오기</span><span class="sxs-lookup"><span data-stu-id="2414b-230">Manual import from Active Directory</span></span>

1. <span data-ttu-id="2414b-231">Azure MFA 서버 hello hello 왼쪽에서 선택 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-231">In hello Azure MFA Server, on hello left, select **Users**.</span></span>
2. <span data-ttu-id="2414b-232">Hello 맨 아래에 선택 **Active Directory에서 가져오기**합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-232">At hello bottom, select **Import from Active Directory**.</span></span>
3. <span data-ttu-id="2414b-233">이제 검색할 수 있습니다 하거나 개별 사용자 또는 검색 hello AD 디렉터리에 대 한 Ou에 대 한 해당 사용자와.</span><span class="sxs-lookup"><span data-stu-id="2414b-233">Now you can either search for individual users or search hello AD directory for OUs with users in them.</span></span>  <span data-ttu-id="2414b-234">이 경우 hello 사용자 OU 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-234">In this case, we specify hello users OU.</span></span>
4. <span data-ttu-id="2414b-235">Hello 오른쪽에 있는 모든 hello 사용자를 강조 표시 하 고 클릭 **가져오기**합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-235">Highlight all hello users on hello right and click **Import**.</span></span>  <span data-ttu-id="2414b-236">성공했음을 알려주는 팝업 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-236">You should receive a pop-up telling you that you were successful.</span></span>  <span data-ttu-id="2414b-237">닫기 hello 가져오기 창입니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-237">Close hello import window.</span></span>

   ![MFA 서버 사용자 가져오기](./media/multi-factor-authentication-get-started-server/import2.png)

### <a name="automated-synchronization-with-active-directory"></a><span data-ttu-id="2414b-239">Active Directory와 자동 동기화</span><span class="sxs-lookup"><span data-stu-id="2414b-239">Automated synchronization with Active Directory</span></span>

1. <span data-ttu-id="2414b-240">Azure MFA 서버 hello hello 왼쪽에서 선택 **디렉터리 통합**합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-240">In hello Azure MFA Server, on hello left, select **Directory Integration**.</span></span>
2. <span data-ttu-id="2414b-241">Toohello 이동 **동기화** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-241">Navigate toohello **Synchronization** tab.</span></span>
3. <span data-ttu-id="2414b-242">Hello 맨 아래에 선택 **추가**</span><span class="sxs-lookup"><span data-stu-id="2414b-242">At hello bottom, choose **Add**</span></span>
4. <span data-ttu-id="2414b-243">Hello에 **동기화 항목 추가** 나타나는 상자 선택 hello 도메인 OU **또는** 보안 그룹, 설정, 방법 기본값 및이 동기화에 대 한 기본 언어는 작업 및 클릭**추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-243">In hello **Add Synchronization Item** box that appears choose hello Domain, OU **or** security group, Settings, Method Defaults, and Language Defaults for this synchronization task and click **Add**.</span></span>
5. <span data-ttu-id="2414b-244">레이블이 hello 확인란 **Active Directory와 동기화 사용** 선택 하 고는 **동기화 간격** 1 분에서 24 시간 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-244">Check hello box labeled **Enable synchronization with Active Directory** and choose a **Synchronization interval** between one minute and 24 hours.</span></span>

## <a name="how-hello-azure-multi-factor-authentication-server-handles-user-data"></a><span data-ttu-id="2414b-245">Hello Azure Multi-factor Authentication 서버에서 사용자 데이터를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="2414b-245">How hello Azure Multi-Factor Authentication Server handles user data</span></span>

<span data-ttu-id="2414b-246">Hello Multi-factor Authentication (MFA) 서버 온-프레미스를 사용 하면 사용자의 데이터는 hello 온-프레미스 서버에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-246">When you use hello Multi-Factor Authentication (MFA) Server on-premises, a user’s data is stored in hello on-premises servers.</span></span> <span data-ttu-id="2414b-247">영구 사용자 데이터가 없으며 hello 클라우드에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-247">No persistent user data is stored in hello cloud.</span></span> <span data-ttu-id="2414b-248">Hello 사용자 2 단계 인증을 수행 하는 경우 MFA 서버 hello 데이터 toohello Azure MFA 클라우드 서비스 tooperform hello 확인을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-248">When hello user performs a two-step verification, hello MFA Server sends data toohello Azure MFA cloud service tooperform hello verification.</span></span> <span data-ttu-id="2414b-249">이러한 인증 요청 toohello 클라우드 서비스를 보내면 hello 다음 필드 보내집니다 hello 요청 및 로그 hello 고객의 인증/사용 현황 보고서에 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-249">When these authentication requests are sent toohello cloud service, hello following fields are sent in hello request and logs so that they are available in hello customer's authentication/usage reports.</span></span> <span data-ttu-id="2414b-250">Hello 필드 중 일부는 선택 사항 이므로 사용 하도록 설정 하거나 hello Multi-factor Authentication 서버 내에서 사용 하지 않도록 설정 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-250">Some of hello fields are optional so they can be enabled or disabled within hello Multi-Factor Authentication Server.</span></span> <span data-ttu-id="2414b-251">포트 443 아웃 바운드 통한 SSL/TLS를 사용 하는 hello와 MFA 서버 toohello MFA 클라우드 서비스에서에서 hello 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-251">hello communication from hello MFA Server toohello MFA cloud service uses SSL/TLS over port 443 outbound.</span></span> <span data-ttu-id="2414b-252">이러한 필드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-252">These fields are:</span></span>

* <span data-ttu-id="2414b-253">고유 ID - 사용자 이름 또는 내부 MFA 서버 ID </span><span class="sxs-lookup"><span data-stu-id="2414b-253">Unique ID - either username or internal MFA server ID</span></span>
* <span data-ttu-id="2414b-254">이름과 성(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="2414b-254">First and last name (optional)</span></span>
* <span data-ttu-id="2414b-255">메일 주소(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="2414b-255">Email address (optional)</span></span>
* <span data-ttu-id="2414b-256">전화 번호 - 음성 통화 또는 SMS 인증을 수행할 때</span><span class="sxs-lookup"><span data-stu-id="2414b-256">Phone number - when doing a voice call or SMS authentication</span></span>
* <span data-ttu-id="2414b-257">장치 토큰 - 모바일 앱 인증을 수행할 때</span><span class="sxs-lookup"><span data-stu-id="2414b-257">Device token - when doing mobile app authentication</span></span>
* <span data-ttu-id="2414b-258">인증 모드</span><span class="sxs-lookup"><span data-stu-id="2414b-258">Authentication mode</span></span>
* <span data-ttu-id="2414b-259">인증 결과</span><span class="sxs-lookup"><span data-stu-id="2414b-259">Authentication result</span></span>
* <span data-ttu-id="2414b-260">MFA 서버 이름</span><span class="sxs-lookup"><span data-stu-id="2414b-260">MFA Server name</span></span>
* <span data-ttu-id="2414b-261">MFA 서버 IP</span><span class="sxs-lookup"><span data-stu-id="2414b-261">MFA Server IP</span></span>
* <span data-ttu-id="2414b-262">클라이언트 IP - 사용 가능한 경우</span><span class="sxs-lookup"><span data-stu-id="2414b-262">Client IP – if available</span></span>

<span data-ttu-id="2414b-263">또한 toohello 위의 필드 hello 확인 결과 (성공/거부) 및 사유 hello 인증 데이터로 저장 되 고 hello 인증/사용 보고서를 통해 사용 가능한도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-263">In addition toohello fields above, hello verification result (success/denial) and reason for any denials is also stored with hello authentication data and available through hello authentication/usage reports.</span></span>

## <a name="back-up-and-restore-azure-mfa-server"></a><span data-ttu-id="2414b-264">Azure MFA 서버 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="2414b-264">Back up and restore Azure MFA Server</span></span>

<span data-ttu-id="2414b-265">양호한 백업 한지 확인 하는 모든 시스템으로는 중요 한 단계 tootake입니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-265">Making sure that you have a good backup is an important step tootake with any system.</span></span>

<span data-ttu-id="2414b-266">Azure MFA 서버를 설치한 tooback hello의 복사본을가지고 있는지 확인 하십시오. **C:\Program Files\multi-factor Authentication Server\Data** hello를 포함 하 여 폴더 **PhoneFactor.pfdata** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-266">tooback up Azure MFA Server, ensure that you have a copy of hello **C:\Program Files\Multi-Factor Authentication Server\Data** folder including hello **PhoneFactor.pfdata** file.</span></span> 

<span data-ttu-id="2414b-267">경우에는 복원에는 필요한 전체 hello 다음 단계:</span><span class="sxs-lookup"><span data-stu-id="2414b-267">In case a restore is needed complete hello following steps:</span></span>

1. <span data-ttu-id="2414b-268">새 서버에 Azure MFA 서버를 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-268">Reinstall Azure MFA Server on a new server.</span></span>
2. <span data-ttu-id="2414b-269">활성화 새 Azure MFA 서버 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-269">Activate hello new Azure MFA Server.</span></span>
3. <span data-ttu-id="2414b-270">Stop hello **MultiFactorAuth** 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-270">Stop hello **MultiFactorAuth** service.</span></span>
4. <span data-ttu-id="2414b-271">Hello 덮어쓰기 **PhoneFactor.pfdata** 복사본을 백업 하는 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-271">Overwrite hello **PhoneFactor.pfdata** with hello backed up copy.</span></span>
5. <span data-ttu-id="2414b-272">Hello 시작 **MultiFactorAuth** 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-272">Start hello **MultiFactorAuth** service.</span></span>

<span data-ttu-id="2414b-273">새 서버 hello 지금 실행 되 고 hello 원래 백업 구성 및 사용자 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-273">hello new server is now up and running with hello original backed-up configuration and user data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2414b-274">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2414b-274">Next steps</span></span>

- <span data-ttu-id="2414b-275">설정 및 구성 hello [사용자 포털](multi-factor-authentication-get-started-portal.md) 셀프 서비스 사용자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-275">Set up and configure hello [User Portal](multi-factor-authentication-get-started-portal.md) for user self-service.</span></span>
- <span data-ttu-id="2414b-276">설정 및 구성 Azure MFA 서버 함께 사용 hello [Active Directory Federation Service](multi-factor-authentication-get-started-adfs.md), [RADIUS 인증](multi-factor-authentication-get-started-server-radius.md), 또는 [LDAP 인증](multi-factor-authentication-get-started-server-ldap.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-276">Set up and configure hello Azure MFA Server with [Active Directory Federation Service](multi-factor-authentication-get-started-adfs.md), [RADIUS Authentication](multi-factor-authentication-get-started-server-radius.md), or [LDAP Authentication](multi-factor-authentication-get-started-server-ldap.md).</span></span>
- <span data-ttu-id="2414b-277">[RADIUS를 사용하여 원격 데스크톱 게이트웨이 및 Azure Multi-Factor Authentication 서버](multi-factor-authentication-get-started-server-rdg.md)를 설정 및 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-277">Set up and configure [Remote Desktop Gateway and Azure Multi-Factor Authentication Server using RADIUS](multi-factor-authentication-get-started-server-rdg.md).</span></span>
- <span data-ttu-id="2414b-278">[Hello Azure Multi-factor Authentication 서버 모바일 앱 웹 서비스를 배포](multi-factor-authentication-get-started-server-webservice.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2414b-278">[Deploy hello Azure Multi-Factor Authentication Server Mobile App Web Service](multi-factor-authentication-get-started-server-webservice.md).</span></span>
- <span data-ttu-id="2414b-279">[Azure Multi-Factor Authentication 및 타사 VPN을 사용한 고급 시나리오](multi-factor-authentication-advanced-vpn-configurations.md)</span><span class="sxs-lookup"><span data-stu-id="2414b-279">[Advanced scenarios with Azure Multi-Factor Authentication and third-party VPNs](multi-factor-authentication-advanced-vpn-configurations.md).</span></span>
