---
title: "aaaConnect 프로그램 Linux 컴퓨터 tooOperations Management Suite (OMS) | Microsoft Docs"
description: "이 문서에서는 tooconnect Linux 컴퓨터 다른 클라우드 또는 온-프레미스 tooOMS Linux 용 OMS 에이전트 hello를 사용 하 여 Azure에서 호스트 되는 방법을 설명 합니다."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: magoedte
ms.openlocfilehash: cb4fc671d0678f9fadc689c6ba7d719213aa61b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toooperations-management-suite-oms"></a><span data-ttu-id="9fe56-103">프로그램 Linux 컴퓨터 tooOperations Management Suite (OMS) 연결</span><span class="sxs-lookup"><span data-stu-id="9fe56-103">Connect your Linux Computers tooOperations Management Suite (OMS)</span></span> 

<span data-ttu-id="9fe56-104">Microsoft OMS(Operations Management Suite)를 사용하여 물리적 서버 또는 가상 컴퓨터로서 온-프레미스 데이터 센터에 상주하는 Linux 컴퓨터 및 컨테이너 솔루션(예: Docker), AWS(Amazon Web Services) 또는 Microsoft Azure와 같은 클라우드 호스티드 서비스에서 생성된 데이터를 수집하고 이러한 데이터로 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-104">With Microsoft Operations Management Suite (OMS), you can collect and act on data generated from Linux computers and container solutions like Docker, residing in your on-premises data center as physical servers or virtual machines, virtual machines in a cloud-hosted service like Amazon Web Services (AWS) or Microsoft Azure.</span></span> <span data-ttu-id="9fe56-105">업데이트 관리 toomanage 소프트웨어 업데이트 tooproactively Linux Vm의 hello 수명 주기 관리 및 변경 내용 추적, tooidentify 구성 변경 등 OMS에서 사용할 수 있는 관리 솔루션을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-105">You can also use management solutions available in OMS such as Change Tracking, tooidentify configuration changes, and Update Management toomanage software updates tooproactively manage hello lifecycle of your Linux VMs.</span></span> 

<span data-ttu-id="9fe56-106">hello OMS 에이전트 hello 컴퓨터 hello 인터넷을 통해 tooa 방화벽 또는 프록시 서버 toocommunicate 연결 및 TCP 포트 443 통해 Linux OMS 서비스 hello로 아웃 바운드 통신에 대 한 검토 [구성 hello에 사용할 에이전트를 HTTP 프록시 서버 또는 게이트웨이 OMS](#configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway) 구성을 변경 toounderstand toobe 적용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-106">hello OMS Agent for Linux communicates outbound with hello OMS service over TCP port 443, and if hello computer connects tooa firewall or proxy server toocommunicate over hello Internet, review [Configuring hello agent for use with an HTTP proxy server or OMS Gateway](#configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway) toounderstand what configuration changes will need toobe applied.</span></span>  <span data-ttu-id="9fe56-107">System Center 2016-Operations Manager 또는 Operations Manager 2012 r 2를 사용 하 여 hello 컴퓨터를 모니터링 하는 경우 hello OMS 서비스 toocollect 데이터 및 전달 toohello 서비스를 사용한 다중 홈 일 수 있으며 여전히 Operations Manager로 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-107">If you are monitoring hello computer with System Center 2016 - Operations Manager or Operations Manager 2012 R2, it can be multi-homed with hello OMS service toocollect data and forward toohello service and still be monitored by Operations Manager.</span></span>  <span data-ttu-id="9fe56-108">OMS와 통합 된 Operations Manager 관리 그룹에서 모니터링 하는 Linux 컴퓨터는 데이터 원본에 대 한 구성을 수신 하지 않음 및 앞으로 hello 관리 그룹을 통해 데이터를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-108">Linux computers monitored by an Operations Manager management group that is integrated with OMS do not receive configuration for data sources and forward collected data through hello management group.</span></span>  <span data-ttu-id="9fe56-109">hello OMS 에이전트에는 하나의 작업 영역 보다 구성된 tooreport toomore 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-109">hello OMS agent cannot be configured tooreport toomore than one workspace.</span></span>  

<span data-ttu-id="9fe56-110">Hello 에이전트 구성된 tooconnect toohello OMS 게이트웨이 tooreceive 구성 정보 수 있고 있는 hello 솔루션에 따라 수집 된 데이터를 보낼 경우 IT 보안 정책을 네트워크 tooconnect toohello 인터넷에서 컴퓨터를 허용 하지 않으므로, 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-110">If your IT security policies do not allow computers on your network tooconnect toohello Internet, hello agent can be configured tooconnect toohello OMS Gateway tooreceive configuration information and send collected data depending on hello solution you have enabled.</span></span> <span data-ttu-id="9fe56-111">자세한 내용 및 단계 tooconfigure OMS 게이트웨이 toohello OMS 서비스를 통해 OMS Linux 에이전트 toocommunicate 프로그램 참조에 대 한 [hello OMS 게이트웨이 사용 하 여 컴퓨터 tooOMS 연결](log-analytics-oms-gateway.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-111">For more information and steps on how tooconfigure your OMS Linux Agent toocommunicate through an OMS Gateway toohello OMS service, see [Connect computers tooOMS using hello OMS Gateway](log-analytics-oms-gateway.md).</span></span>  

<span data-ttu-id="9fe56-112">hello 다음 다이어그램은 Linux 컴퓨터를 에이전트 관리 하는 hello와 hello 방향 및 포트를 포함 하 여 OMS로 hello 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-112">hello following diagram depicts hello connection between hello agent-managed Linux computers and OMS, including hello direction and ports.</span></span>

![OMS와 에이전트의 직접 통신 다이어그램](./media/log-analytics-agent-linux/log-analytics-agent-linux-communication.png)

## <a name="system-requirements"></a><span data-ttu-id="9fe56-114">시스템 요구 사항</span><span class="sxs-lookup"><span data-stu-id="9fe56-114">System requirements</span></span>
<span data-ttu-id="9fe56-115">을 시작 하기 전에 다음 세부 정보 tooverify hello 필수 조건을 충족 하는 hello를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-115">Before starting, review hello following details tooverify you meet hello prerequisites.</span></span>

### <a name="supported-linux-operating-systems"></a><span data-ttu-id="9fe56-116">지원되는 Linux 운영 체제</span><span class="sxs-lookup"><span data-stu-id="9fe56-116">Supported Linux operating systems</span></span>
<span data-ttu-id="9fe56-117">다음의 Linux 배포판 hello 공식적으로 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-117">hello following Linux distributions are officially supported.</span></span>  <span data-ttu-id="9fe56-118">그러나 Linux 용 OMS 에이전트 hello 나열 되지 않은 다른 배포 에서도 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-118">However, hello OMS Agent for Linux might also run on other distributions not listed.</span></span>

* <span data-ttu-id="9fe56-119">Amazon Linux 2012.09 too2015.09 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="9fe56-119">Amazon Linux 2012.09 too2015.09 (x86/x64)</span></span>
* <span data-ttu-id="9fe56-120">CentOS Linux 5, 6 및 7(x86/x64)</span><span class="sxs-lookup"><span data-stu-id="9fe56-120">CentOS Linux 5, 6, and 7 (x86/x64)</span></span>
* <span data-ttu-id="9fe56-121">Oracle Linux 5, 6 및 7(x86/x64)</span><span class="sxs-lookup"><span data-stu-id="9fe56-121">Oracle Linux 5, 6, and 7 (x86/x64)</span></span>
* <span data-ttu-id="9fe56-122">Red Hat Enterprise Linux Server 5, 6 및 7(x86/x64)</span><span class="sxs-lookup"><span data-stu-id="9fe56-122">Red Hat Enterprise Linux Server 5, 6 and 7 (x86/x64)</span></span>
* <span data-ttu-id="9fe56-123">Debian GNU/Linux 6, 7, 8(x86/x64)</span><span class="sxs-lookup"><span data-stu-id="9fe56-123">Debian GNU/Linux 6, 7, and 8 (x86/x64)</span></span>
* <span data-ttu-id="9fe56-124">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS(x86/x64)</span><span class="sxs-lookup"><span data-stu-id="9fe56-124">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS (x86/x64)</span></span>
* <span data-ttu-id="9fe56-125">SUSE Linux Enterprise Server 11 및 12(x86/x64)</span><span class="sxs-lookup"><span data-stu-id="9fe56-125">SUSE Linux Enterprise Server 11 and 12 (x86/x64)</span></span>

### <a name="network"></a><span data-ttu-id="9fe56-126">네트워크</span><span class="sxs-lookup"><span data-stu-id="9fe56-126">Network</span></span>
<span data-ttu-id="9fe56-127">방화벽 구성 정보와 hello 정보 hello 프록시 목록 아래에 필요한 hello OMS와 함께 Linux 에이전트 toocommunicate입니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-127">hello information below list hello proxy and firewall configuration information required for hello Linux agent toocommunicate with OMS.</span></span> <span data-ttu-id="9fe56-128">트래픽은은 네트워크 toohello OMS 서비스에서 아웃 바운드입니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-128">Traffic is outbound from your network toohello OMS service.</span></span> 

|<span data-ttu-id="9fe56-129">에이전트 리소스</span><span class="sxs-lookup"><span data-stu-id="9fe56-129">Agent Resource</span></span>| <span data-ttu-id="9fe56-130">포트</span><span class="sxs-lookup"><span data-stu-id="9fe56-130">Ports</span></span> |  
|------|---------|  
|<span data-ttu-id="9fe56-131">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="9fe56-131">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="9fe56-132">포트 443</span><span class="sxs-lookup"><span data-stu-id="9fe56-132">Port 443</span></span>|   
|<span data-ttu-id="9fe56-133">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="9fe56-133">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="9fe56-134">포트 443</span><span class="sxs-lookup"><span data-stu-id="9fe56-134">Port 443</span></span>|   
|<span data-ttu-id="9fe56-135">*.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="9fe56-135">*.blob.core.windows.net/</span></span> | <span data-ttu-id="9fe56-136">포트 443</span><span class="sxs-lookup"><span data-stu-id="9fe56-136">Port 443</span></span>|   
|<span data-ttu-id="9fe56-137">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="9fe56-137">*.azure-automation.net</span></span> | <span data-ttu-id="9fe56-138">포트 443</span><span class="sxs-lookup"><span data-stu-id="9fe56-138">Port 443</span></span>|  

### <a name="package-requirements"></a><span data-ttu-id="9fe56-139">패키지 요구 사항</span><span class="sxs-lookup"><span data-stu-id="9fe56-139">Package requirements</span></span>

 <span data-ttu-id="9fe56-140">**필수 패키지**</span><span class="sxs-lookup"><span data-stu-id="9fe56-140">**Required package**</span></span>   | <span data-ttu-id="9fe56-141">**설명**</span><span class="sxs-lookup"><span data-stu-id="9fe56-141">**Description**</span></span>   | <span data-ttu-id="9fe56-142">**최소 버전**</span><span class="sxs-lookup"><span data-stu-id="9fe56-142">**Minimum version**</span></span>
--------------------- | --------------------- | -------------------
<span data-ttu-id="9fe56-143">Glibc</span><span class="sxs-lookup"><span data-stu-id="9fe56-143">Glibc</span></span> | <span data-ttu-id="9fe56-144">GNU C 라이브러리</span><span class="sxs-lookup"><span data-stu-id="9fe56-144">GNU C Library</span></span>   | <span data-ttu-id="9fe56-145">2.5-12</span><span class="sxs-lookup"><span data-stu-id="9fe56-145">2.5-12</span></span> 
<span data-ttu-id="9fe56-146">Openssl</span><span class="sxs-lookup"><span data-stu-id="9fe56-146">Openssl</span></span> | <span data-ttu-id="9fe56-147">OpenSSL 라이브러리</span><span class="sxs-lookup"><span data-stu-id="9fe56-147">OpenSSL Libraries</span></span> | <span data-ttu-id="9fe56-148">0.9.8e 또는 1.0</span><span class="sxs-lookup"><span data-stu-id="9fe56-148">0.9.8e or 1.0</span></span>
<span data-ttu-id="9fe56-149">Curl</span><span class="sxs-lookup"><span data-stu-id="9fe56-149">Curl</span></span> | <span data-ttu-id="9fe56-150">cURL 웹 클라이언트</span><span class="sxs-lookup"><span data-stu-id="9fe56-150">cURL web client</span></span> | <span data-ttu-id="9fe56-151">7.15.5</span><span class="sxs-lookup"><span data-stu-id="9fe56-151">7.15.5</span></span>
<span data-ttu-id="9fe56-152">Python-ctypes</span><span class="sxs-lookup"><span data-stu-id="9fe56-152">Python-ctypes</span></span> | | 
<span data-ttu-id="9fe56-153">PAM</span><span class="sxs-lookup"><span data-stu-id="9fe56-153">PAM</span></span> | <span data-ttu-id="9fe56-154">플러그형 인증 모듈</span><span class="sxs-lookup"><span data-stu-id="9fe56-154">Pluggable authentication Modules</span></span> | 

> [!NOTE]
>  <span data-ttu-id="9fe56-155">Rsyslog 또는 syslog-ng 중 하나는 필수 toocollect syslog 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-155">Either rsyslog or syslog-ng are required toocollect syslog messages.</span></span> <span data-ttu-id="9fe56-156">Red Hat Enterprise Linux, CentOS 및 Oracle Linux 버전 (sysklog)의 버전 5에 hello 기본 syslog 디먼은 syslog 이벤트 수집이 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-156">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="9fe56-157">이 버전의,이 배포에서 syslog 데이터 toocollect hello rsyslog 디먼을 설치 해야 하며 tooreplace sysklog를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-157">toocollect syslog data from this version of these distributions, hello rsyslog daemon should be installed and configured tooreplace sysklog,</span></span> 

<span data-ttu-id="9fe56-158">hello 에이전트는 여러 패키지에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-158">hello agent includes multiple packages.</span></span> <span data-ttu-id="9fe56-159">hello 릴리스 파일 hello 포함 되어 있는지와 함께 hello 셸 번들을 실행 하 여 사용할 수 있는 패키지를 다음 `--extract`:</span><span class="sxs-lookup"><span data-stu-id="9fe56-159">hello release file contains hello following packages, available by running hello shell bundle with `--extract`:</span></span>

<span data-ttu-id="9fe56-160">**패키지**</span><span class="sxs-lookup"><span data-stu-id="9fe56-160">**Package**</span></span> | <span data-ttu-id="9fe56-161">**버전**</span><span class="sxs-lookup"><span data-stu-id="9fe56-161">**Version**</span></span> | <span data-ttu-id="9fe56-162">**설명**</span><span class="sxs-lookup"><span data-stu-id="9fe56-162">**Description**</span></span>
----------- | ----------- | --------------
<span data-ttu-id="9fe56-163">omsagent</span><span class="sxs-lookup"><span data-stu-id="9fe56-163">omsagent</span></span> | <span data-ttu-id="9fe56-164">1.4.0</span><span class="sxs-lookup"><span data-stu-id="9fe56-164">1.4.0</span></span> | <span data-ttu-id="9fe56-165">hello Linux 용 Operations Management Suite 에이전트</span><span class="sxs-lookup"><span data-stu-id="9fe56-165">hello Operations Management Suite Agent for Linux</span></span>
<span data-ttu-id="9fe56-166">omsconfig</span><span class="sxs-lookup"><span data-stu-id="9fe56-166">omsconfig</span></span> | <span data-ttu-id="9fe56-167">1.1.1</span><span class="sxs-lookup"><span data-stu-id="9fe56-167">1.1.1</span></span> | <span data-ttu-id="9fe56-168">Hello OMS 에이전트에 대 한 구성 에이전트</span><span class="sxs-lookup"><span data-stu-id="9fe56-168">Configuration agent for hello OMS Agent</span></span>
<span data-ttu-id="9fe56-169">omi</span><span class="sxs-lookup"><span data-stu-id="9fe56-169">omi</span></span> | <span data-ttu-id="9fe56-170">1.2.0</span><span class="sxs-lookup"><span data-stu-id="9fe56-170">1.2.0</span></span> | <span data-ttu-id="9fe56-171">Open Management Infrastructure(OMI) -- 경량 CIM 서버</span><span class="sxs-lookup"><span data-stu-id="9fe56-171">Open Management Infrastructure (OMI) - a lightweight CIM Server</span></span>
<span data-ttu-id="9fe56-172">scx</span><span class="sxs-lookup"><span data-stu-id="9fe56-172">scx</span></span> | <span data-ttu-id="9fe56-173">1.6.3</span><span class="sxs-lookup"><span data-stu-id="9fe56-173">1.6.3</span></span> | <span data-ttu-id="9fe56-174">운영 체제 성능 메트릭용 OMI CIM 공급자</span><span class="sxs-lookup"><span data-stu-id="9fe56-174">OMI CIM Providers for operating system performance metrics</span></span>
<span data-ttu-id="9fe56-175">apache-cimprov</span><span class="sxs-lookup"><span data-stu-id="9fe56-175">apache-cimprov</span></span> | <span data-ttu-id="9fe56-176">1.0.1</span><span class="sxs-lookup"><span data-stu-id="9fe56-176">1.0.1</span></span> | <span data-ttu-id="9fe56-177">OMI용 Apache HTTP 서버 성능 모니터링 공급자.</span><span class="sxs-lookup"><span data-stu-id="9fe56-177">Apache HTTP Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="9fe56-178">Apache HTTP 서버가 감지되면 설치됨.</span><span class="sxs-lookup"><span data-stu-id="9fe56-178">Installed if Apache HTTP Server is detected.</span></span>
<span data-ttu-id="9fe56-179">mysql-cimprov</span><span class="sxs-lookup"><span data-stu-id="9fe56-179">mysql-cimprov</span></span> | <span data-ttu-id="9fe56-180">1.0.1</span><span class="sxs-lookup"><span data-stu-id="9fe56-180">1.0.1</span></span> | <span data-ttu-id="9fe56-181">OMI용 MySQL 서버 성능 모니터링 공급자.</span><span class="sxs-lookup"><span data-stu-id="9fe56-181">MySQL Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="9fe56-182">MySQL/MariaDB 서버가 감지되면 설치됨.</span><span class="sxs-lookup"><span data-stu-id="9fe56-182">Installed if MySQL/MariaDB server is detected.</span></span>
<span data-ttu-id="9fe56-183">docker-cimprov</span><span class="sxs-lookup"><span data-stu-id="9fe56-183">docker-cimprov</span></span> | <span data-ttu-id="9fe56-184">1.0.0</span><span class="sxs-lookup"><span data-stu-id="9fe56-184">1.0.0</span></span> | <span data-ttu-id="9fe56-185">OMI용 Docker 공급자.</span><span class="sxs-lookup"><span data-stu-id="9fe56-185">Docker provider for OMI.</span></span> <span data-ttu-id="9fe56-186">Docker가 감지되면 설치됨.</span><span class="sxs-lookup"><span data-stu-id="9fe56-186">Installed if Docker is detected.</span></span>

### <a name="compatibility-with-system-center-operations-manager"></a><span data-ttu-id="9fe56-187">System Center Operations Manager와의 호환성</span><span class="sxs-lookup"><span data-stu-id="9fe56-187">Compatibility with System Center Operations Manager</span></span>
<span data-ttu-id="9fe56-188">Linux 용 OMS 에이전트 hello hello System Center Operations Manager 에이전트와 에이전트 이진 파일을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-188">hello OMS Agent for Linux shares agent binaries with hello System Center Operations Manager agent.</span></span> <span data-ttu-id="9fe56-189">Operations Manager에서 현재 관리 시스템에 Linux 용 OMS 에이전트 hello를 설치한 경우에 OMI 및 SCX 패키지가 hello 컴퓨터 tooa 최신 버전 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-189">If you install hello OMS Agent for Linux on a system currently managed by Operations Manager, it hello OMI and SCX packages on hello computer tooa newer version.</span></span> <span data-ttu-id="9fe56-190">이 릴리스에서 OMS hello 및 System Center 2016-Linux 용 Operations Manager/Operations Manager 2012 R2 에이전트는 호환입니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-190">In this release, hello OMS and System Center 2016 - Operations Manager/Operations Manager 2012 R2 agents for Linux are compatible.</span></span> 

> [!NOTE]
> <span data-ttu-id="9fe56-191">System Center 2012 SP1 및 이전 버전 현재 호환 또는 아닌 지원 되는 Linux 용 OMS 에이전트 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-191">System Center 2012 SP1 and earlier versions are currently not compatible or supported with hello OMS Agent for Linux.</span></span><br>
> <span data-ttu-id="9fe56-192">Hello Linux 용 OMS 에이전트는 Operations Manager에서 모니터링 하지 않는 tooa 설치 된 컴퓨터 이며 toomonitor hello 컴퓨터를 Operations Manager를 다음 원하는 수정 해야 hello [OMI 구성을](#enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager) 이전 toodiscovering hello 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-192">If hello OMS Agent for Linux is installed tooa computer that is not currently monitored by Operations Manager, and you then wish toomonitor hello computer with Operations Manager, you must modify hello [OMI configuration](#enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager) prior toodiscovering hello computer.</span></span> <span data-ttu-id="9fe56-193">**이 단계는 *하지* Linux 용 OMS 에이전트 hello 전에 hello Operations Manager 에이전트가 설치 된 경우에 필요 합니다.**</span><span class="sxs-lookup"><span data-stu-id="9fe56-193">**This step is *not* needed if hello Operations Manager agent is installed before hello OMS Agent for Linux.**</span></span>

### <a name="system-configuration-changes"></a><span data-ttu-id="9fe56-194">시스템 구성 변경 내용</span><span class="sxs-lookup"><span data-stu-id="9fe56-194">System configuration changes</span></span>
<span data-ttu-id="9fe56-195">Linux 패키지에 대 한 hello OMS 에이전트를 설치한 후 hello 다음과 같은 추가 시스템 차원 구성 변경 내용이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-195">After installing hello OMS Agent for Linux packages, hello following additional system-wide configuration changes are applied.</span></span> <span data-ttu-id="9fe56-196">이러한 아티팩트는 omsagent 패키지 hello 때 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-196">These artifacts are removed when hello omsagent package is uninstalled.</span></span>

* <span data-ttu-id="9fe56-197">`omsagent` 라는 이름의 권한 없는 사용자가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-197">A non-privileged user named: `omsagent` is created.</span></span> <span data-ttu-id="9fe56-198">이 hello 계정을 hello omsagent 디먼이 실행으로입니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-198">This is hello account hello omsagent daemon runs as.</span></span>
* <span data-ttu-id="9fe56-199">sudoers "include" 파일은 /etc/sudoers.d/omsagent에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-199">A sudoers “include” file is created at /etc/sudoers.d/omsagent.</span></span> <span data-ttu-id="9fe56-200">Omsagent toorestart hello syslog 및 omsagent 디먼을이 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-200">This authorizes omsagent toorestart hello syslog and omsagent daemons.</span></span> <span data-ttu-id="9fe56-201">Sudo "include" 지시문은 hello 설치 된 버전의 sudo에서 지원 되지 않는, 이러한 항목에는 너무/등/sudoers 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-201">If sudo “include” directives are not supported in hello installed version of sudo, these entries are written too/etc/sudoers.</span></span>
* <span data-ttu-id="9fe56-202">hello syslog 구성이 수정 된 tooforward 이벤트 toohello 에이전트의 하위 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-202">hello syslog configuration is modified tooforward a subset of events toohello agent.</span></span> <span data-ttu-id="9fe56-203">자세한 내용은 참조 hello **데이터 수집 구성** 아래 섹션</span><span class="sxs-lookup"><span data-stu-id="9fe56-203">For more information, see hello **Configuring Data Collection** section below</span></span>

### <a name="upgrade-from-a-previous-release"></a><span data-ttu-id="9fe56-204">이전 릴리스에서 업그레이드</span><span class="sxs-lookup"><span data-stu-id="9fe56-204">Upgrade from a previous release</span></span>
<span data-ttu-id="9fe56-205">이 릴리스에서는 1.0.0-47보다 이전 버전에서 업그레이드하도록 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-205">Upgrade from versions earlier than 1.0.0-47 is supported in this release.</span></span> <span data-ttu-id="9fe56-206">Hello로 hello 설치 수행 `--upgrade` hello 에이전트 toohello 최신 버전의 모든 구성 요소를 업그레이드 하는 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-206">Performing hello installation with hello `--upgrade` command upgrades all components of hello agent toohello latest version.</span></span>

## <a name="installing-hello-agent"></a><span data-ttu-id="9fe56-207">Hello 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="9fe56-207">Installing hello agent</span></span>

<span data-ttu-id="9fe56-208">이 섹션에서는 각 hello 에이전트 구성 요소에 대 한 tooinstall hello Debian 및 RPM을 포함 하는 bunndle를 사용 하 여 Linux 용 OMS 에이전트 패키지 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-208">This section describes how tooinstall hello OMS Agent for Linux using a bunndle, which contains Debian and RPM packages for each of hello agent components.</span></span>  <span data-ttu-id="9fe56-209">직접 설치 하거나, tooretrieve hello 개별 패키지를 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-209">It can be installed directly or extracted tooretrieve hello individual packages.</span></span>  

<span data-ttu-id="9fe56-210">OMS 작업 영역 ID 및 toohello 전환 하 여 찾을 수 있는 키를 먼저 [OMS 클래식 포털](https://mms.microsoft.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-210">First you need your OMS workspace ID and key, which you can find by switching toohello [OMS classic portal](https://mms.microsoft.com).</span></span>  <span data-ttu-id="9fe56-211">Hello에 **개요** hello 상단 메뉴 선택에서 페이지에서 **설정**를 이동한 후 너무**Sources\Linux 연결 된 서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-211">On hello **Overview** page, from hello top menu select **Settings**, and then navigate too**Connected Sources\Linux Servers**.</span></span>  <span data-ttu-id="9fe56-212">Hello 값 toohello 오른쪽의 참조 **작업 영역 ID** 및 **기본 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-212">You see hello value toohello right of **Workspace ID** and **Primary Key**.</span></span>  <span data-ttu-id="9fe56-213">두 항목을 복사하여 선호하는 편집기에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-213">Copy and paste both into your favorite editor.</span></span>    

1. <span data-ttu-id="9fe56-214">최신 버전 다운로드 hello [(x64) Linux 용 OMS 에이전트](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x64.sh) 또는 [x86 Linux 용 OMS 에이전트](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x86.sh) GitHub에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-214">Download hello latest [OMS Agent for Linux (x64)](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x64.sh) or [OMS Agent for Linux x86](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x86.sh) from GitHub.</span></span>  
2. <span data-ttu-id="9fe56-215">Hello 적절 한 번들 (x86 또는 x64) tooyour Linux 컴퓨터 scp/sftp를 사용 하 여 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-215">Transfer hello appropriate bundle (x86 or x64) tooyour Linux computer using scp/sftp.</span></span>
3. <span data-ttu-id="9fe56-216">Hello를 사용 하 여 설치 hello 번들 `--install` 또는 `--upgrade` 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-216">Install hello bundle by using hello `--install` or `--upgrade` argument.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="9fe56-217">Linux 용 System Center Operations Manager 에이전트 hello 이미 설치 되어 같은 기존 패키지가 설치 된 경우 사용 하 여 hello `--upgrade` 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-217">If any existing packages are installed such as when hello System Center Operations Manager agent for Linux is already installed, use hello `--upgrade` argument.</span></span> <span data-ttu-id="9fe56-218">설치 하는 동안 tooconnect tooOperations 관리 제품군을 제공 hello `-w <WorkspaceID>` 및 `-s <Shared Key>` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-218">tooconnect tooOperations Management Suite during installation, provide hello `-w <WorkspaceID>` and `-s <Shared Key>` parameters.</span></span>


#### <a name="tooinstall-and-onboard-directly"></a><span data-ttu-id="9fe56-219">tooinstall 직접 등록</span><span class="sxs-lookup"><span data-stu-id="9fe56-219">tooinstall and onboard directly</span></span>
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key>
```

#### <a name="tooupgrade-hello-agent-package"></a><span data-ttu-id="9fe56-220">tooupgrade hello 에이전트 패키지</span><span class="sxs-lookup"><span data-stu-id="9fe56-220">tooupgrade hello agent package</span></span>
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade
```

#### <a name="tooinstall-and-onboard-tooa-workspace-in-us-government-cloud"></a><span data-ttu-id="9fe56-221">tooinstall 및 미국 정부 클라우드에서 온보드 tooa 작업 영역</span><span class="sxs-lookup"><span data-stu-id="9fe56-221">tooinstall and onboard tooa workspace in US Government Cloud</span></span>
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key> -d opinsights.azure.us
```

## <a name="configuring-hello-agent-for-use-with-an-http-proxy-server-or-oms-gateway"></a><span data-ttu-id="9fe56-222">HTTP 프록시 서버 또는 게이트웨이 OMS와 사용 하기 위해 hello 에이전트 구성</span><span class="sxs-lookup"><span data-stu-id="9fe56-222">Configuring hello agent for use with an HTTP proxy server or OMS Gateway</span></span>
<span data-ttu-id="9fe56-223">hello Linux 용 OMS 에이전트는 HTTP 또는 HTTPS 프록시 서버 또는 게이트웨이 OMS toohello OMS 서비스를 통해 통신을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-223">hello OMS Agent for Linux supports communicating either through an HTTP or HTTPS proxy server or OMS Gateway toohello OMS service.</span></span>  <span data-ttu-id="9fe56-224">익명 및 기본 인증(사용자 이름/암호) 둘 다 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-224">Both anonymous and basic authentication (username/password) is supported.</span></span>  

### <a name="proxy-configuration"></a><span data-ttu-id="9fe56-225">프록시 구성</span><span class="sxs-lookup"><span data-stu-id="9fe56-225">Proxy configuration</span></span>
<span data-ttu-id="9fe56-226">hello 프록시 구성 값 hello 구문 다음에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-226">hello proxy configuration value has hello following syntax:</span></span>

`[protocol://][user:password@]proxyhost[:port]`

<span data-ttu-id="9fe56-227">속성</span><span class="sxs-lookup"><span data-stu-id="9fe56-227">Property</span></span>|<span data-ttu-id="9fe56-228">설명</span><span class="sxs-lookup"><span data-stu-id="9fe56-228">Description</span></span>
-|-
<span data-ttu-id="9fe56-229">프로토콜</span><span class="sxs-lookup"><span data-stu-id="9fe56-229">Protocol</span></span>|<span data-ttu-id="9fe56-230">HTTP 또는 HTTPS</span><span class="sxs-lookup"><span data-stu-id="9fe56-230">http or https</span></span>
<span data-ttu-id="9fe56-231">사용자</span><span class="sxs-lookup"><span data-stu-id="9fe56-231">user</span></span>|<span data-ttu-id="9fe56-232">프록시 인증을 위한 선택적 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="9fe56-232">Optional username for proxy authentication</span></span>
<span data-ttu-id="9fe56-233">password</span><span class="sxs-lookup"><span data-stu-id="9fe56-233">password</span></span>|<span data-ttu-id="9fe56-234">프록시 인증을 위한 선택적 암호</span><span class="sxs-lookup"><span data-stu-id="9fe56-234">Optional password for proxy authentication</span></span>
<span data-ttu-id="9fe56-235">proxyhost</span><span class="sxs-lookup"><span data-stu-id="9fe56-235">proxyhost</span></span>|<span data-ttu-id="9fe56-236">주소 또는 FQDN hello 프록시 서버/oms 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="9fe56-236">Address or FQDN of hello proxy server/OMS Gateway</span></span>
<span data-ttu-id="9fe56-237">포트</span><span class="sxs-lookup"><span data-stu-id="9fe56-237">port</span></span>|<span data-ttu-id="9fe56-238">Hello 프록시 서버/OMS 게이트웨이 대 한 선택적 포트 번호</span><span class="sxs-lookup"><span data-stu-id="9fe56-238">Optional port number for hello proxy server/OMS Gateway</span></span>

<span data-ttu-id="9fe56-239">예: `http://user01:password@proxy01.contoso.com:8080`</span><span class="sxs-lookup"><span data-stu-id="9fe56-239">For example: `http://user01:password@proxy01.contoso.com:8080`</span></span>

<span data-ttu-id="9fe56-240">설치 중에 또는 설치 후 hello proxy.conf 구성 파일을 수정 하 여 hello 프록시 서버를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-240">hello proxy server can be specified during installation or by modifying hello proxy.conf configuration file after installation.</span></span>   

### <a name="specify-proxy-configuration-during-installation"></a><span data-ttu-id="9fe56-241">설치 중 프록시 구성 지정</span><span class="sxs-lookup"><span data-stu-id="9fe56-241">Specify proxy configuration during installation</span></span>
<span data-ttu-id="9fe56-242">hello `-p` 또는 `--proxy` hello omsagent 설치 번들에 대 한 인수는 hello 프록시 구성 toouse를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-242">hello `-p` or `--proxy` argument for hello omsagent installation bundle specifies hello proxy configuration toouse.</span></span> 

```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -p http://<proxy user>:<proxy password>@<proxy address>:<proxy port> -w <workspace id> -s <shared key>
```

### <a name="define-hello-proxy-configuration-in-a-file"></a><span data-ttu-id="9fe56-243">Hello 프록시 구성 파일에 정의</span><span class="sxs-lookup"><span data-stu-id="9fe56-243">Define hello proxy configuration in a file</span></span>
<span data-ttu-id="9fe56-244">hello 프록시 구성을 hello 파일에서 설정할 수 있습니다 `/etc/opt/microsoft/omsagent/proxy.conf` 및 `/etc/opt/microsoft/omsagent/conf/proxy.conf `합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-244">hello proxy configuration can be set in hello files `/etc/opt/microsoft/omsagent/proxy.conf`  and `/etc/opt/microsoft/omsagent/conf/proxy.conf `.</span></span> <span data-ttu-id="9fe56-245">hello 파일을 직접 생성 하거나, 편집 하지만 해당 사용 권한을 업데이트 toogrant hello omiuser 사용자 hello 파일에 대해 읽기 권한을 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-245">hello files can be directly created or edited, but their permissions must be updated toogrant hello omiuser user read permission on hello files.</span></span> <span data-ttu-id="9fe56-246">예:</span><span class="sxs-lookup"><span data-stu-id="9fe56-246">For example:</span></span>
```
proxyconf="https://proxyuser:proxypassword@proxyserver01:8080"
sudo echo $proxyconf >>/etc/opt/microsoft/omsagent/proxy.conf
sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf
sudo chmod 600 /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf  
sudo /opt/microsoft/omsagent/bin/service_control restart [<workspace id>]
```

### <a name="removing-hello-proxy-configuration"></a><span data-ttu-id="9fe56-247">Hello 프록시 구성을 제거 하는</span><span class="sxs-lookup"><span data-stu-id="9fe56-247">Removing hello proxy configuration</span></span>
<span data-ttu-id="9fe56-248">이전에 정의 된 프록시 구성 tooremove toodirect 연결 되돌릴, hello proxy.conf 파일을 제거 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-248">tooremove a previously defined proxy configuration and revert toodirect connectivity, remove hello proxy.conf file:</span></span>
```
sudo rm /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf
sudo /opt/microsoft/omsagent/bin/service_control restart 
```

## <a name="onboarding-with-operations-management-suite"></a><span data-ttu-id="9fe56-249">Operations Management Suite에 등록</span><span class="sxs-lookup"><span data-stu-id="9fe56-249">Onboarding with Operations Management Suite</span></span>
<span data-ttu-id="9fe56-250">작업 영역 ID 및 키 hello 번들 설치 도중 제공 되지 않았습니다 hello 에이전트 Operations Management Suite로 이후에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-250">If a workspace ID and key were not provided during hello bundle installation, hello agent must be subsequently registered with Operations Management Suite.</span></span>

### <a name="onboarding-using-hello-command-line"></a><span data-ttu-id="9fe56-251">Hello 명령줄을 사용 하는 온 보 딩</span><span class="sxs-lookup"><span data-stu-id="9fe56-251">Onboarding using hello command line</span></span>
<span data-ttu-id="9fe56-252">작업 영역에 대 한 키 및 hello 작업 영역 id를 제공 하는 hello omsadmin.sh 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-252">Run hello omsadmin.sh command supplying hello workspace id and key for your workspace.</span></span> <span data-ttu-id="9fe56-253">이 명령은 루트 권한(sudo 권한 상승)으로 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-253">This command must be run as root (with sudo elevation):</span></span>
```
cd /opt/microsoft/omsagent/bin
sudo ./omsadmin.sh -w <WorkspaceID> -s <Shared Key>
```

### <a name="onboarding-using-a-file"></a><span data-ttu-id="9fe56-254">파일을 사용하는 등록</span><span class="sxs-lookup"><span data-stu-id="9fe56-254">Onboarding using a file</span></span>
1.  <span data-ttu-id="9fe56-255">Hello 파일을 만들 `/etc/omsagent-onboard.conf`합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-255">Create hello file `/etc/omsagent-onboard.conf`.</span></span> <span data-ttu-id="9fe56-256">읽기 및 쓰기 가능한 루트에 대 한 hello 파일 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-256">hello file must be readable and writable for root.</span></span>
`sudo vi /etc/omsagent-onboard.conf`
2.  <span data-ttu-id="9fe56-257">작업 영역 ID와 공유 키 hello 파일에 있는 줄을 다음 hello를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-257">Insert hello following lines in hello file with your Workspace ID and Shared Key:</span></span>

        WORKSPACE_ID=<WorkspaceID>  
        SHARED_KEY=<Shared Key>  
   
3.  <span data-ttu-id="9fe56-258">다음 명령은 tooOnboard tooOMS hello를 실행 합니다.`sudo /opt/microsoft/omsagent/bin/omsadmin.sh`</span><span class="sxs-lookup"><span data-stu-id="9fe56-258">Run hello following command tooOnboard tooOMS: `sudo /opt/microsoft/omsagent/bin/omsadmin.sh`</span></span>
4.  <span data-ttu-id="9fe56-259">등록에 hello 파일이 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-259">hello file is deleted on successful onboarding.</span></span>

## <a name="enable-hello-oms-agent-for-linux-tooreport-toosystem-center-operations-manager"></a><span data-ttu-id="9fe56-260">Linux tooreport tooSystem Center Operations Manager에 대 한 hello OMS 에이전트를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="9fe56-260">Enable hello OMS Agent for Linux tooreport tooSystem Center Operations Manager</span></span>
<span data-ttu-id="9fe56-261">Hello Linux tooreport tooa System Center Operations Manager 관리 그룹에 대 한 단계 tooconfigure hello OMS 에이전트를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-261">Perform hello following steps tooconfigure hello OMS Agent for Linux tooreport tooa System Center Operations Manager management group.</span></span>  

1. <span data-ttu-id="9fe56-262">Hello 파일 편집`/etc/opt/omi/conf/omiserver.conf`</span><span class="sxs-lookup"><span data-stu-id="9fe56-262">Edit hello file `/etc/opt/omi/conf/omiserver.conf`</span></span>
2. <span data-ttu-id="9fe56-263">로 시작 하는 hello 줄 확인 **httpsport =** hello 포트 1270을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-263">Ensure that hello line beginning with **httpsport=** defines hello port 1270.</span></span> <span data-ttu-id="9fe56-264">예: `httpsport=1270`</span><span class="sxs-lookup"><span data-stu-id="9fe56-264">Such as: `httpsport=1270`</span></span>
3. <span data-ttu-id="9fe56-265">Hello OMI 서버를 다시 시작 합니다.`sudo /opt/omi/bin/service_control restart`</span><span class="sxs-lookup"><span data-stu-id="9fe56-265">Restart hello OMI server: `sudo /opt/omi/bin/service_control restart`</span></span>

## <a name="agent-logs"></a><span data-ttu-id="9fe56-266">에이전트 로그</span><span class="sxs-lookup"><span data-stu-id="9fe56-266">Agent logs</span></span>
<span data-ttu-id="9fe56-267">hello Linux 용 OMS 에이전트에서 찾을 수 있습니다에 대 한 로그를 hello: `/var/opt/microsoft/omsagent/<workspace id>/log/` hello omsconfig (에이전트 구성) 프로그램에서 확인할 수 있습니다에 대 한 로그를 hello: `/var/opt/microsoft/omsconfig/log/` hello OMI 및 SCX 구성 요소 (성능 메트릭 데이터 제공)에 대 한 로그에서 찾을 수 있습니다.`/var/opt/omi/log/ and /var/opt/microsoft/scx/log`</span><span class="sxs-lookup"><span data-stu-id="9fe56-267">hello logs for hello OMS Agent for Linux can be found at: `/var/opt/microsoft/omsagent/<workspace id>/log/` hello logs for hello omsconfig (agent configuration) program can be found at: `/var/opt/microsoft/omsconfig/log/` Logs for hello OMI and SCX components (which provide performance metrics data) can be found at: `/var/opt/omi/log/ and /var/opt/microsoft/scx/log`</span></span>

### <a name="log-rotation-configuration"></a><span data-ttu-id="9fe56-268">로그 순환 구성##</span><span class="sxs-lookup"><span data-stu-id="9fe56-268">Log rotation configuration##</span></span>
<span data-ttu-id="9fe56-269">omsagent에 대 한 hello 로그 회전 구성에서 찾을 수 있습니다.`/etc/logrotate.d/omsagent-<workspace id>`</span><span class="sxs-lookup"><span data-stu-id="9fe56-269">hello log rotate configuration for omsagent can be found at: `/etc/logrotate.d/omsagent-<workspace id>`</span></span>

<span data-ttu-id="9fe56-270">hello 기본 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-270">hello default settings are:</span></span> 
```
/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log {
    rotate 5
    missingok
    notifempty
    compress
    size 50k
    copytruncate
}
```

## <a name="uninstalling-hello-oms-agent-for-linux"></a><span data-ttu-id="9fe56-271">Linux 용 OMS 에이전트 제거 hello</span><span class="sxs-lookup"><span data-stu-id="9fe56-271">Uninstalling hello OMS Agent for Linux</span></span>
<span data-ttu-id="9fe56-272">hello 에이전트 패키지는 제거할 수 hello로 실행 중인 hello 번들.sh 파일 `--purge` hello 에이전트와 해당 구성의 hello 컴퓨터에서 완전히 제거 하는 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-272">hello agent packages can be uninstalled by running hello bundle .sh file with hello `--purge` argument, which completely removes hello agent and its configuration from hello computer.</span></span>   

```
> sudo rpm -e omsconfig
> sudo rpm -e omsagent
> sudo /opt/microsoft/scx/bin/uninstall
```

## <a name="troubleshooting"></a><span data-ttu-id="9fe56-273">문제 해결</span><span class="sxs-lookup"><span data-stu-id="9fe56-273">Troubleshooting</span></span>

### <a name="issue-unable-tooconnect-through-proxy-toooms"></a><span data-ttu-id="9fe56-274">프록시 tooOMS 통해 없습니다 tooconnect 문제:</span><span class="sxs-lookup"><span data-stu-id="9fe56-274">Issue: Unable tooconnect through proxy tooOMS</span></span>

#### <a name="probable-causes"></a><span data-ttu-id="9fe56-275">가능한 원인</span><span class="sxs-lookup"><span data-stu-id="9fe56-275">Probable causes</span></span>
* <span data-ttu-id="9fe56-276">온 보 딩 하는 동안 지정 된 hello 프록시 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-276">hello proxy specified during onboarding was incorrect</span></span>
* <span data-ttu-id="9fe56-277">사용할 수 없는 데이터 센터에서 whitelistested hello OMS 서비스 끝점</span><span class="sxs-lookup"><span data-stu-id="9fe56-277">hello OMS Service Endpoints are not whitelistested in your datacenter</span></span> 

#### <a name="resolutions"></a><span data-ttu-id="9fe56-278">해결 방법</span><span class="sxs-lookup"><span data-stu-id="9fe56-278">Resolutions</span></span>
1. <span data-ttu-id="9fe56-279">다음 명령을 hello 옵션을 사용 하는 hello를 사용 하 여 hello Linux 용 OMS 에이전트와 OMS 서비스 Reonboard toohello `-v` 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-279">Reonboard toohello OMS Service with hello OMS Agent for Linux by using hello following command with hello option `-v` enabled.</span></span> <span data-ttu-id="9fe56-280">이렇게 하면 hello 프록시 toohello OMS 서비스를 통해 연결 하는 hello 에이전트의 자세한 정보를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-280">This allows verbose output of hello agent connecting through hello proxy toohello OMS Service.</span></span> 
`/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`

2. <span data-ttu-id="9fe56-281">Hello 섹션을 검토 [구성 hello에 사용할 에이전트를 HTTP 프록시 server(#configuring the-agent-for-use-with-a-http-proxy-server) tooverify 제대로 구성한 프록시 서버를 통해 에이전트 toocommunicate hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-281">Review hello section [Configuring hello agent for use with an HTTP proxy server(#configuring the-agent-for-use-with-a-http-proxy-server) tooverify you have properly configured hello agent toocommunicate through a proxy server.</span></span>    
* <span data-ttu-id="9fe56-282">OMS 서비스 끝점 다음 hello 다시 확인은 허용 목록.</span><span class="sxs-lookup"><span data-stu-id="9fe56-282">Double check that hello following OMS Service endpoints are whitelisted:</span></span>

    |<span data-ttu-id="9fe56-283">에이전트 리소스</span><span class="sxs-lookup"><span data-stu-id="9fe56-283">Agent Resource</span></span>| <span data-ttu-id="9fe56-284">포트</span><span class="sxs-lookup"><span data-stu-id="9fe56-284">Ports</span></span> |  
    |------|---------|  
    |<span data-ttu-id="9fe56-285">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="9fe56-285">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="9fe56-286">포트 443</span><span class="sxs-lookup"><span data-stu-id="9fe56-286">Port 443</span></span>|   
    |<span data-ttu-id="9fe56-287">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="9fe56-287">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="9fe56-288">포트 443</span><span class="sxs-lookup"><span data-stu-id="9fe56-288">Port 443</span></span>|   
    |<span data-ttu-id="9fe56-289">ods.systemcenteradvisor.com</span><span class="sxs-lookup"><span data-stu-id="9fe56-289">ods.systemcenteradvisor.com</span></span> | <span data-ttu-id="9fe56-290">포트 443</span><span class="sxs-lookup"><span data-stu-id="9fe56-290">Port 443</span></span>|   
    |<span data-ttu-id="9fe56-291">*.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="9fe56-291">*.blob.core.windows.net/</span></span> | <span data-ttu-id="9fe56-292">포트 443</span><span class="sxs-lookup"><span data-stu-id="9fe56-292">Port 443</span></span>|   

### <a name="issue-you-receive-a-403-error-when-trying-tooonboard"></a><span data-ttu-id="9fe56-293">문제: tooonboard 동안 403 오류 수신</span><span class="sxs-lookup"><span data-stu-id="9fe56-293">Issue: You receive a 403 error when trying tooonboard</span></span>

#### <a name="probable-causes"></a><span data-ttu-id="9fe56-294">가능한 원인</span><span class="sxs-lookup"><span data-stu-id="9fe56-294">Probable causes</span></span>
* <span data-ttu-id="9fe56-295">Linux 서버의 날짜 및 시간이 올바르지 않습니다</span><span class="sxs-lookup"><span data-stu-id="9fe56-295">Date and Time is incorrect on Linux Server</span></span> 
* <span data-ttu-id="9fe56-296">사용된 작업 영역 ID 및 작업 영역 키가 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-296">Workspace ID and Workspace Key used are not correct</span></span>

#### <a name="resolution"></a><span data-ttu-id="9fe56-297">해결 방법</span><span class="sxs-lookup"><span data-stu-id="9fe56-297">Resolution</span></span>

1. <span data-ttu-id="9fe56-298">Hello 시 Linux 서버 hello 명령 날짜를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-298">Check hello time on your Linux server with hello command date.</span></span> <span data-ttu-id="9fe56-299">Hello 시간이 현재 시간 으로부터 15 분 + /-경우에 온 보 딩 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-299">If hello time is +/- 15 minutes from current time, then onboarding fails.</span></span> <span data-ttu-id="9fe56-300">toocorrect이 업데이트 hello 날짜 및/또는 Linux 서버에의 표준 시간대입니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-300">toocorrect this update hello date and/or timezone of your Linux server.</span></span> 
2. <span data-ttu-id="9fe56-301">Linux 용 hello 최신 버전의 hello OMS 에이전트를 설치 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-301">Verify you have installed hello latest version of hello OMS Agent for Linux.</span></span>  <span data-ttu-id="9fe56-302">최신 버전 hello 이제 알려 줍니다 시간차 hello 온 보 딩 오류로 인해 발생 한 경우.</span><span class="sxs-lookup"><span data-stu-id="9fe56-302">hello newest version now notifies you if time skew is causing hello onboarding failure.</span></span>
3. <span data-ttu-id="9fe56-303">올바른 작업 영역 ID와이 항목의 앞부분에 나오는 hello 설치 지침에 따라 작업 영역 키를 사용 하 여 Reonboard 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-303">Reonboard using correct Workspace ID and Workspace Key following hello installation instructions earlier in this topic.</span></span>

### <a name="issue-you-see-a-500-and-404-error-in-hello-log-file-right-after-onboarding"></a><span data-ttu-id="9fe56-304">온 보 딩 직후 hello 로그 파일에서 500 및 404 오류를 참조 문제:</span><span class="sxs-lookup"><span data-stu-id="9fe56-304">Issue: You see a 500 and 404 error in hello log file right after onboarding</span></span>
<span data-ttu-id="9fe56-305">이 문제는 알려진 문제이며 Linux 데이터를 OMS 작업 영역으로 처음 업로드할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-305">This is a known issue that occurs on first upload of Linux data into an OMS workspace.</span></span> <span data-ttu-id="9fe56-306">이 문제는 전송되는 데이터 또는 서비스 환경에 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-306">This does not affect data being sent or service experience.</span></span>

### <a name="issue--you-are-not-seeing-any-data-in-hello-oms-portal"></a><span data-ttu-id="9fe56-307">문제:이 표시 되지 않는 hello OMS 포털에서 모든 데이터</span><span class="sxs-lookup"><span data-stu-id="9fe56-307">Issue:  You are not seeing any data in hello OMS portal</span></span>

#### <a name="probable-causes"></a><span data-ttu-id="9fe56-308">가능한 원인</span><span class="sxs-lookup"><span data-stu-id="9fe56-308">Probable causes</span></span>

- <span data-ttu-id="9fe56-309">온 보 딩 toohello OMS 서비스 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-309">Onboarding toohello OMS Service failed</span></span>
- <span data-ttu-id="9fe56-310">OMS 서비스에서 차단 되는 연결 toohello</span><span class="sxs-lookup"><span data-stu-id="9fe56-310">Connection toohello OMS Service is blocked</span></span>
- <span data-ttu-id="9fe56-311">Linux용 OMS 에이전트가 백업되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-311">OMS Agent for Linux data is backed up</span></span>

#### <a name="resolutions"></a><span data-ttu-id="9fe56-312">해결 방법</span><span class="sxs-lookup"><span data-stu-id="9fe56-312">Resolutions</span></span>
1. <span data-ttu-id="9fe56-313">온 보 딩 hello OMS 서비스로 hello 다음 파일이 있는 경우를 확인 하 여 성공 했는지 여부를 확인 합니다.`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`</span><span class="sxs-lookup"><span data-stu-id="9fe56-313">Check if onboarding hello OMS Service was successful by checking if hello following file exists: `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`</span></span>
2. <span data-ttu-id="9fe56-314">Hello를 사용 하 여 Reonboard `omsadmin.sh` 명령줄 지침</span><span class="sxs-lookup"><span data-stu-id="9fe56-314">Reonboard using hello `omsadmin.sh` command-line instructions</span></span>
3. <span data-ttu-id="9fe56-315">프록시를 사용 하는 경우 이전에 제공 된 toohello 프록시 해결 단계를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="9fe56-315">If using a proxy, refer toohello proxy resolution steps provided earlier.</span></span>
4. <span data-ttu-id="9fe56-316">경우에 따라 Linux 용 OMS 에이전트 hello hello OMS 서비스와 통신할 수 없는 경우 hello 에이전트 데이터가 큐에 대기 중인된 toohello 가득 찬 버퍼 크기는 50MB입니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-316">In some cases, when hello OMS Agent for Linux cannot communicate with hello OMS Service, data on hello agent is queued toohello full buffer size, which is 50 MB.</span></span> <span data-ttu-id="9fe56-317">hello 다음 명령을 실행 하 여 hello Linux 용 OMS 에이전트를 다시 시작 해야: `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`합니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-317">hello OMS Agent for Linux should be restarted by running hello following command: `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`.</span></span> 

    >[!NOTE]
    ><span data-ttu-id="9fe56-318">이 문제는 에이전트 버전 1.1.0-28 및 이상에서 해결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9fe56-318">This issue is fixed in agent version 1.1.0-28 and later.</span></span>
> 