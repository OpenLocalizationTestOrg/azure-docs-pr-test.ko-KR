---
title: "OMS(Operations Management Suite)에 Linux 컴퓨터 연결 | Microsoft Docs"
description: "이 문서에서는 Linux용 OMS 에이전트를 사용하여 Azure, 기타 클라우드 또는 온-프레미스에 호스트된 Linux 컴퓨터를 OMS에 연결하는 방법을 설명합니다."
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
ms.openlocfilehash: 1c05f68235aafd0fa098a3b0edaba1258df09380
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-linux-computers-to-operations-management-suite-oms"></a><span data-ttu-id="bd62c-103">OMS(Operations Management Suite)에 Linux 컴퓨터 연결</span><span class="sxs-lookup"><span data-stu-id="bd62c-103">Connect your Linux Computers to Operations Management Suite (OMS)</span></span> 

<span data-ttu-id="bd62c-104">Microsoft OMS(Operations Management Suite)를 사용하여 물리적 서버 또는 가상 컴퓨터로서 온-프레미스 데이터 센터에 상주하는 Linux 컴퓨터 및 컨테이너 솔루션(예: Docker), AWS(Amazon Web Services) 또는 Microsoft Azure와 같은 클라우드 호스티드 서비스에서 생성된 데이터를 수집하고 이러한 데이터로 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-104">With Microsoft Operations Management Suite (OMS), you can collect and act on data generated from Linux computers and container solutions like Docker, residing in your on-premises data center as physical servers or virtual machines, virtual machines in a cloud-hosted service like Amazon Web Services (AWS) or Microsoft Azure.</span></span> <span data-ttu-id="bd62c-105">변경 추적과 같이 OMS에서 사용할 수 있는 관리 솔루션을 사용하여 구성 변경으 식별하고, 업데이트 관리를 통해 소프트웨어 업데이트를 관리하여 Linux VM의 수명 주기를 사전에 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-105">You can also use management solutions available in OMS such as Change Tracking, to identify configuration changes, and Update Management to manage software updates to proactively manage the lifecycle of your Linux VMs.</span></span> 

<span data-ttu-id="bd62c-106">Linux용 OMS 에이전트는 TCP 포트 443을 통해 OMS 서비스와 아웃바운드 통신을 수행하고, 컴퓨터가 인터넷을 통해 통신하기 위해 방화벽 또는 프록시 서버에 연결하는 경우 [HTTP 프록시 서버 또는 OMS 게이트웨이에서 사용하도록 에이전트 구성](#configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway)을 검토하여 적용해야 하는 구성 변경 내용을 이해하세요.</span><span class="sxs-lookup"><span data-stu-id="bd62c-106">The OMS Agent for Linux communicates outbound with the OMS service over TCP port 443, and if the computer connects to a firewall or proxy server to communicate over the Internet, review [Configuring the agent for use with an HTTP proxy server or OMS Gateway](#configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway) to understand what configuration changes will need to be applied.</span></span>  <span data-ttu-id="bd62c-107">System Center 2016 - Operations Manager 또는 Operations Manager 2012 R2를 사용하여 컴퓨터를 모니터링하는 경우 OMS 서비스와 멀티홈으로 구성되어 데이터를 수집하고 서비스로 전달할 수 있고 Operations Manager에서 계속 모니터링될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-107">If you are monitoring the computer with System Center 2016 - Operations Manager or Operations Manager 2012 R2, it can be multi-homed with the OMS service to collect data and forward to the service and still be monitored by Operations Manager.</span></span>  <span data-ttu-id="bd62c-108">OMS와 통합된 Operations Manager 관리 그룹에서 모니터링되는 Linux 컴퓨터는 데이터 원본에 대한 구성을 수신하거나 관리 그룹을 통해 수집된 데이터를 전달하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-108">Linux computers monitored by an Operations Manager management group that is integrated with OMS do not receive configuration for data sources and forward collected data through the management group.</span></span>  <span data-ttu-id="bd62c-109">OMS 에이전트는 둘 이상의 작업 영역에 보고하도록 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-109">The OMS agent cannot be configured to report to more than one workspace.</span></span>  

<span data-ttu-id="bd62c-110">IT 보안 정책이 네트워크의 컴퓨터가 인터넷에 연결하도록 허용하지 않을 경우 OMS 게이트웨이에 연결하여 구성 정보를 받고 사용하도록 설정한 솔루션에 따라 수집된 데이터를 보내도록 에이전트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-110">If your IT security policies do not allow computers on your network to connect to the Internet, the agent can be configured to connect to the OMS Gateway to receive configuration information and send collected data depending on the solution you have enabled.</span></span> <span data-ttu-id="bd62c-111">OMS Linux 에이전트가 OMS 게이트웨이를 통해 OMS 서비스와 통신할 수 있도록 구성하는 방법에 대한 자세한 내용 및 단계에 대해서는 [OMS 게이트웨이 사용하여 OMS에 컴퓨터 연결](log-analytics-oms-gateway.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bd62c-111">For more information and steps on how to configure your OMS Linux Agent to communicate through an OMS Gateway to the OMS service, see [Connect computers to OMS using the OMS Gateway](log-analytics-oms-gateway.md).</span></span>  

<span data-ttu-id="bd62c-112">다음 다이어그램은 방향 및 포트를 포함하여 에이전트 관리 Linux 컴퓨터와 OMS 간 연결을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-112">The following diagram depicts the connection between the agent-managed Linux computers and OMS, including the direction and ports.</span></span>

![OMS와 에이전트의 직접 통신 다이어그램](./media/log-analytics-agent-linux/log-analytics-agent-linux-communication.png)

## <a name="system-requirements"></a><span data-ttu-id="bd62c-114">시스템 요구 사항</span><span class="sxs-lookup"><span data-stu-id="bd62c-114">System requirements</span></span>
<span data-ttu-id="bd62c-115">시작하기 전에 다음 세부 정보를 검토하여 필수 구성 요소를 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-115">Before starting, review the following details to verify you meet the prerequisites.</span></span>

### <a name="supported-linux-operating-systems"></a><span data-ttu-id="bd62c-116">지원되는 Linux 운영 체제</span><span class="sxs-lookup"><span data-stu-id="bd62c-116">Supported Linux operating systems</span></span>
<span data-ttu-id="bd62c-117">다음 Linux 배포판이 공식적으로 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-117">The following Linux distributions are officially supported.</span></span>  <span data-ttu-id="bd62c-118">하지만, Linux용 OMS 에이전트는 나열되지 않은 그 밖의 배포에서 실행이 가능할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-118">However, the OMS Agent for Linux might also run on other distributions not listed.</span></span>

* <span data-ttu-id="bd62c-119">Amazon Linux 2012.09 ~ 2015.09(x86/x64)</span><span class="sxs-lookup"><span data-stu-id="bd62c-119">Amazon Linux 2012.09 to 2015.09 (x86/x64)</span></span>
* <span data-ttu-id="bd62c-120">CentOS Linux 5, 6 및 7(x86/x64)</span><span class="sxs-lookup"><span data-stu-id="bd62c-120">CentOS Linux 5, 6, and 7 (x86/x64)</span></span>
* <span data-ttu-id="bd62c-121">Oracle Linux 5, 6 및 7(x86/x64)</span><span class="sxs-lookup"><span data-stu-id="bd62c-121">Oracle Linux 5, 6, and 7 (x86/x64)</span></span>
* <span data-ttu-id="bd62c-122">Red Hat Enterprise Linux Server 5, 6 및 7(x86/x64)</span><span class="sxs-lookup"><span data-stu-id="bd62c-122">Red Hat Enterprise Linux Server 5, 6 and 7 (x86/x64)</span></span>
* <span data-ttu-id="bd62c-123">Debian GNU/Linux 6, 7, 8(x86/x64)</span><span class="sxs-lookup"><span data-stu-id="bd62c-123">Debian GNU/Linux 6, 7, and 8 (x86/x64)</span></span>
* <span data-ttu-id="bd62c-124">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS(x86/x64)</span><span class="sxs-lookup"><span data-stu-id="bd62c-124">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS (x86/x64)</span></span>
* <span data-ttu-id="bd62c-125">SUSE Linux Enterprise Server 11 및 12(x86/x64)</span><span class="sxs-lookup"><span data-stu-id="bd62c-125">SUSE Linux Enterprise Server 11 and 12 (x86/x64)</span></span>

### <a name="network"></a><span data-ttu-id="bd62c-126">네트워크</span><span class="sxs-lookup"><span data-stu-id="bd62c-126">Network</span></span>
<span data-ttu-id="bd62c-127">아래 정보는 Linux 에이전트가 OMS와 통신하는 데 필요한 프록시 및 방화벽 구성 정보를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-127">The information below list the proxy and firewall configuration information required for the Linux agent to communicate with OMS.</span></span> <span data-ttu-id="bd62c-128">트래픽은 네트워크에서 OMS 서비스로 아웃바운드됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-128">Traffic is outbound from your network to the OMS service.</span></span> 

|<span data-ttu-id="bd62c-129">에이전트 리소스</span><span class="sxs-lookup"><span data-stu-id="bd62c-129">Agent Resource</span></span>| <span data-ttu-id="bd62c-130">포트</span><span class="sxs-lookup"><span data-stu-id="bd62c-130">Ports</span></span> |  
|------|---------|  
|<span data-ttu-id="bd62c-131">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="bd62c-131">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="bd62c-132">포트 443</span><span class="sxs-lookup"><span data-stu-id="bd62c-132">Port 443</span></span>|   
|<span data-ttu-id="bd62c-133">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="bd62c-133">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="bd62c-134">포트 443</span><span class="sxs-lookup"><span data-stu-id="bd62c-134">Port 443</span></span>|   
|<span data-ttu-id="bd62c-135">*.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="bd62c-135">*.blob.core.windows.net/</span></span> | <span data-ttu-id="bd62c-136">포트 443</span><span class="sxs-lookup"><span data-stu-id="bd62c-136">Port 443</span></span>|   
|<span data-ttu-id="bd62c-137">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="bd62c-137">*.azure-automation.net</span></span> | <span data-ttu-id="bd62c-138">포트 443</span><span class="sxs-lookup"><span data-stu-id="bd62c-138">Port 443</span></span>|  

### <a name="package-requirements"></a><span data-ttu-id="bd62c-139">패키지 요구 사항</span><span class="sxs-lookup"><span data-stu-id="bd62c-139">Package requirements</span></span>

 <span data-ttu-id="bd62c-140">**필수 패키지**</span><span class="sxs-lookup"><span data-stu-id="bd62c-140">**Required package**</span></span>   | <span data-ttu-id="bd62c-141">**설명**</span><span class="sxs-lookup"><span data-stu-id="bd62c-141">**Description**</span></span>   | <span data-ttu-id="bd62c-142">**최소 버전**</span><span class="sxs-lookup"><span data-stu-id="bd62c-142">**Minimum version**</span></span>
--------------------- | --------------------- | -------------------
<span data-ttu-id="bd62c-143">Glibc</span><span class="sxs-lookup"><span data-stu-id="bd62c-143">Glibc</span></span> | <span data-ttu-id="bd62c-144">GNU C 라이브러리</span><span class="sxs-lookup"><span data-stu-id="bd62c-144">GNU C Library</span></span>   | <span data-ttu-id="bd62c-145">2.5-12</span><span class="sxs-lookup"><span data-stu-id="bd62c-145">2.5-12</span></span> 
<span data-ttu-id="bd62c-146">Openssl</span><span class="sxs-lookup"><span data-stu-id="bd62c-146">Openssl</span></span> | <span data-ttu-id="bd62c-147">OpenSSL 라이브러리</span><span class="sxs-lookup"><span data-stu-id="bd62c-147">OpenSSL Libraries</span></span> | <span data-ttu-id="bd62c-148">0.9.8e 또는 1.0</span><span class="sxs-lookup"><span data-stu-id="bd62c-148">0.9.8e or 1.0</span></span>
<span data-ttu-id="bd62c-149">Curl</span><span class="sxs-lookup"><span data-stu-id="bd62c-149">Curl</span></span> | <span data-ttu-id="bd62c-150">cURL 웹 클라이언트</span><span class="sxs-lookup"><span data-stu-id="bd62c-150">cURL web client</span></span> | <span data-ttu-id="bd62c-151">7.15.5</span><span class="sxs-lookup"><span data-stu-id="bd62c-151">7.15.5</span></span>
<span data-ttu-id="bd62c-152">Python-ctypes</span><span class="sxs-lookup"><span data-stu-id="bd62c-152">Python-ctypes</span></span> | | 
<span data-ttu-id="bd62c-153">PAM</span><span class="sxs-lookup"><span data-stu-id="bd62c-153">PAM</span></span> | <span data-ttu-id="bd62c-154">플러그형 인증 모듈</span><span class="sxs-lookup"><span data-stu-id="bd62c-154">Pluggable authentication Modules</span></span> | 

> [!NOTE]
>  <span data-ttu-id="bd62c-155">Syslog 메시지를 수집하려면 rsyslog 또는 syslog-ng가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-155">Either rsyslog or syslog-ng are required to collect syslog messages.</span></span> <span data-ttu-id="bd62c-156">Red Hat Enterprise Linux 버전 5, CentOS 및 Oracle Linux 버전(sysklog)에서는 syslog 이벤트 수집을 위한 기본 syslog 디먼이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-156">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="bd62c-157">이 배포의 해당 버전에서 syslog 데이터를 수집하려면 rsyslog 디먼을 설치하고 sysklog를 대체하도록 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-157">To collect syslog data from this version of these distributions, the rsyslog daemon should be installed and configured to replace sysklog,</span></span> 

<span data-ttu-id="bd62c-158">에이전트는 여러 패키지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-158">The agent includes multiple packages.</span></span> <span data-ttu-id="bd62c-159">다음 패키지를 포함하는 릴리스 파일은 `--extract`와 함께 shell 번들을 실행하면 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-159">The release file contains the following packages, available by running the shell bundle with `--extract`:</span></span>

<span data-ttu-id="bd62c-160">**패키지**</span><span class="sxs-lookup"><span data-stu-id="bd62c-160">**Package**</span></span> | <span data-ttu-id="bd62c-161">**버전**</span><span class="sxs-lookup"><span data-stu-id="bd62c-161">**Version**</span></span> | <span data-ttu-id="bd62c-162">**설명**</span><span class="sxs-lookup"><span data-stu-id="bd62c-162">**Description**</span></span>
----------- | ----------- | --------------
<span data-ttu-id="bd62c-163">omsagent</span><span class="sxs-lookup"><span data-stu-id="bd62c-163">omsagent</span></span> | <span data-ttu-id="bd62c-164">1.4.0</span><span class="sxs-lookup"><span data-stu-id="bd62c-164">1.4.0</span></span> | <span data-ttu-id="bd62c-165">Linux용 Operations Management Suite 에이전트</span><span class="sxs-lookup"><span data-stu-id="bd62c-165">The Operations Management Suite Agent for Linux</span></span>
<span data-ttu-id="bd62c-166">omsconfig</span><span class="sxs-lookup"><span data-stu-id="bd62c-166">omsconfig</span></span> | <span data-ttu-id="bd62c-167">1.1.1</span><span class="sxs-lookup"><span data-stu-id="bd62c-167">1.1.1</span></span> | <span data-ttu-id="bd62c-168">OMS 에이전트용 구성 에이전트</span><span class="sxs-lookup"><span data-stu-id="bd62c-168">Configuration agent for the OMS Agent</span></span>
<span data-ttu-id="bd62c-169">omi</span><span class="sxs-lookup"><span data-stu-id="bd62c-169">omi</span></span> | <span data-ttu-id="bd62c-170">1.2.0</span><span class="sxs-lookup"><span data-stu-id="bd62c-170">1.2.0</span></span> | <span data-ttu-id="bd62c-171">Open Management Infrastructure(OMI) -- 경량 CIM 서버</span><span class="sxs-lookup"><span data-stu-id="bd62c-171">Open Management Infrastructure (OMI) - a lightweight CIM Server</span></span>
<span data-ttu-id="bd62c-172">scx</span><span class="sxs-lookup"><span data-stu-id="bd62c-172">scx</span></span> | <span data-ttu-id="bd62c-173">1.6.3</span><span class="sxs-lookup"><span data-stu-id="bd62c-173">1.6.3</span></span> | <span data-ttu-id="bd62c-174">운영 체제 성능 메트릭용 OMI CIM 공급자</span><span class="sxs-lookup"><span data-stu-id="bd62c-174">OMI CIM Providers for operating system performance metrics</span></span>
<span data-ttu-id="bd62c-175">apache-cimprov</span><span class="sxs-lookup"><span data-stu-id="bd62c-175">apache-cimprov</span></span> | <span data-ttu-id="bd62c-176">1.0.1</span><span class="sxs-lookup"><span data-stu-id="bd62c-176">1.0.1</span></span> | <span data-ttu-id="bd62c-177">OMI용 Apache HTTP 서버 성능 모니터링 공급자.</span><span class="sxs-lookup"><span data-stu-id="bd62c-177">Apache HTTP Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="bd62c-178">Apache HTTP 서버가 감지되면 설치됨.</span><span class="sxs-lookup"><span data-stu-id="bd62c-178">Installed if Apache HTTP Server is detected.</span></span>
<span data-ttu-id="bd62c-179">mysql-cimprov</span><span class="sxs-lookup"><span data-stu-id="bd62c-179">mysql-cimprov</span></span> | <span data-ttu-id="bd62c-180">1.0.1</span><span class="sxs-lookup"><span data-stu-id="bd62c-180">1.0.1</span></span> | <span data-ttu-id="bd62c-181">OMI용 MySQL 서버 성능 모니터링 공급자.</span><span class="sxs-lookup"><span data-stu-id="bd62c-181">MySQL Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="bd62c-182">MySQL/MariaDB 서버가 감지되면 설치됨.</span><span class="sxs-lookup"><span data-stu-id="bd62c-182">Installed if MySQL/MariaDB server is detected.</span></span>
<span data-ttu-id="bd62c-183">docker-cimprov</span><span class="sxs-lookup"><span data-stu-id="bd62c-183">docker-cimprov</span></span> | <span data-ttu-id="bd62c-184">1.0.0</span><span class="sxs-lookup"><span data-stu-id="bd62c-184">1.0.0</span></span> | <span data-ttu-id="bd62c-185">OMI용 Docker 공급자.</span><span class="sxs-lookup"><span data-stu-id="bd62c-185">Docker provider for OMI.</span></span> <span data-ttu-id="bd62c-186">Docker가 감지되면 설치됨.</span><span class="sxs-lookup"><span data-stu-id="bd62c-186">Installed if Docker is detected.</span></span>

### <a name="compatibility-with-system-center-operations-manager"></a><span data-ttu-id="bd62c-187">System Center Operations Manager와의 호환성</span><span class="sxs-lookup"><span data-stu-id="bd62c-187">Compatibility with System Center Operations Manager</span></span>
<span data-ttu-id="bd62c-188">Linux 용 OMS 에이전트는 System Center Operations Manager 에이전트와 에이전트 바이너리를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-188">The OMS Agent for Linux shares agent binaries with the System Center Operations Manager agent.</span></span> <span data-ttu-id="bd62c-189">현재 Operations Manager로 관리되는 시스템에 Linux용 OMS 에이전트를 설치하면, 컴퓨터의 OMI 및 SCX 패키지가 새 버전으로 업그레이드됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-189">If you install the OMS Agent for Linux on a system currently managed by Operations Manager, it the OMI and SCX packages on the computer to a newer version.</span></span> <span data-ttu-id="bd62c-190">이 릴리스에서 OMS 및 Linux용 System Center 2016 - Linux 용 Operations Manager/Operations Manager 2012 R2 에이전트는 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-190">In this release, the OMS and System Center 2016 - Operations Manager/Operations Manager 2012 R2 agents for Linux are compatible.</span></span> 

> [!NOTE]
> <span data-ttu-id="bd62c-191">하지만 System Center 2012 SP1 이전 버전은 현재 OMS Agent for Linux와 호환되거나 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-191">System Center 2012 SP1 and earlier versions are currently not compatible or supported with the OMS Agent for Linux.</span></span><br>
> <span data-ttu-id="bd62c-192">Operations Manager로 모니터링되지 않는 컴퓨터에 OMS Agent for Linux를 설치한 다음, Operations Manager로 컴퓨터를 모니터링하려는 경우 컴퓨터를 검색하기 전에 [OMI 구성](#enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager)을 반드시 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-192">If the OMS Agent for Linux is installed to a computer that is not currently monitored by Operations Manager, and you then wish to monitor the computer with Operations Manager, you must modify the [OMI configuration](#enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager) prior to discovering the computer.</span></span> <span data-ttu-id="bd62c-193">**Operations Manager 에이전트가 OMS Agent for Linux보다 먼저 설치되면 이 단계가 필요하지 *않습니다*.**</span><span class="sxs-lookup"><span data-stu-id="bd62c-193">**This step is *not* needed if the Operations Manager agent is installed before the OMS Agent for Linux.**</span></span>

### <a name="system-configuration-changes"></a><span data-ttu-id="bd62c-194">시스템 구성 변경 내용</span><span class="sxs-lookup"><span data-stu-id="bd62c-194">System configuration changes</span></span>
<span data-ttu-id="bd62c-195">OMS Agent for Linux 패키지를 설치한 후에는 다음과 같은 시스템 수준의 구성 변경이 추가로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-195">After installing the OMS Agent for Linux packages, the following additional system-wide configuration changes are applied.</span></span> <span data-ttu-id="bd62c-196">이러한 아티팩트는 omsagent 패키지가 제거되면 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-196">These artifacts are removed when the omsagent package is uninstalled.</span></span>

* <span data-ttu-id="bd62c-197">`omsagent` 라는 이름의 권한 없는 사용자가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-197">A non-privileged user named: `omsagent` is created.</span></span> <span data-ttu-id="bd62c-198">이 계정으로 omsagent 디먼이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-198">This is the account the omsagent daemon runs as.</span></span>
* <span data-ttu-id="bd62c-199">sudoers "include" 파일은 /etc/sudoers.d/omsagent에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-199">A sudoers “include” file is created at /etc/sudoers.d/omsagent.</span></span> <span data-ttu-id="bd62c-200">그러면 omsagent에서 syslog 및 omsagent 데몬을 다시 시작할 수 있도록 허가됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-200">This authorizes omsagent to restart the syslog and omsagent daemons.</span></span> <span data-ttu-id="bd62c-201">설치된 sudo 버전에서 sudo “include” 지시문이 지원되지 않으면, 이 항목은 /etc/sudoers에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-201">If sudo “include” directives are not supported in the installed version of sudo, these entries are written to /etc/sudoers.</span></span>
* <span data-ttu-id="bd62c-202">syslog 구성은 이벤트 하위 집합을 에이전트에 전달하도록 수정됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-202">The syslog configuration is modified to forward a subset of events to the agent.</span></span> <span data-ttu-id="bd62c-203">자세한 내용은 아래의 **데이터 수집 구성** 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bd62c-203">For more information, see the **Configuring Data Collection** section below</span></span>

### <a name="upgrade-from-a-previous-release"></a><span data-ttu-id="bd62c-204">이전 릴리스에서 업그레이드</span><span class="sxs-lookup"><span data-stu-id="bd62c-204">Upgrade from a previous release</span></span>
<span data-ttu-id="bd62c-205">이 릴리스에서는 1.0.0-47보다 이전 버전에서 업그레이드하도록 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-205">Upgrade from versions earlier than 1.0.0-47 is supported in this release.</span></span> <span data-ttu-id="bd62c-206">`--upgrade` 명령을 사용하여 설치를 수행하면 에이전트의 모든 구성 요소가 최신 버전으로 업그레이드됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-206">Performing the installation with the `--upgrade` command upgrades all components of the agent to the latest version.</span></span>

## <a name="installing-the-agent"></a><span data-ttu-id="bd62c-207">에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="bd62c-207">Installing the agent</span></span>

<span data-ttu-id="bd62c-208">이 섹션에서는 각 에이전트 구성 요소에 대한 Debian 및 RPM 패키지를 포함하는 번들을 사용하여 Linux용 OMS 에이전트를 설치하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-208">This section describes how to install the OMS Agent for Linux using a bunndle, which contains Debian and RPM packages for each of the agent components.</span></span>  <span data-ttu-id="bd62c-209">직접 설치하거나 개별 패키지를 검색하도록 추출될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-209">It can be installed directly or extracted to retrieve the individual packages.</span></span>  

<span data-ttu-id="bd62c-210">[OMS 클래식 포털](https://mms.microsoft.com)로 전환하면 찾을 수 있는 OMS 작업 영역 ID 및 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-210">First you need your OMS workspace ID and key, which you can find by switching to the [OMS classic portal](https://mms.microsoft.com).</span></span>  <span data-ttu-id="bd62c-211">**개요** 페이지의 맨 위 메뉴에서 **설정**을 선택한 다음, **Connected Sources\Linux Servers**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-211">On the **Overview** page, from the top menu select **Settings**, and then navigate to **Connected Sources\Linux Servers**.</span></span>  <span data-ttu-id="bd62c-212">**작업 영역 ID** 및 **기본 키** 오른쪽에 값이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-212">You see the value to the right of **Workspace ID** and **Primary Key**.</span></span>  <span data-ttu-id="bd62c-213">두 항목을 복사하여 선호하는 편집기에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-213">Copy and paste both into your favorite editor.</span></span>    

1. <span data-ttu-id="bd62c-214">GitHub에서 최신 [Linux용 OMS 에이전트(x64)](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x64.sh) 또는 [Linux x86용 OMS 에이전트](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x86.sh)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-214">Download the latest [OMS Agent for Linux (x64)](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x64.sh) or [OMS Agent for Linux x86](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x86.sh) from GitHub.</span></span>  
2. <span data-ttu-id="bd62c-215">scp/sftp를 사용하여 Linux 컴퓨터로 해당 번들(x86 또는 x64)을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-215">Transfer the appropriate bundle (x86 or x64) to your Linux computer using scp/sftp.</span></span>
3. <span data-ttu-id="bd62c-216">`--install` 또는 `--upgrade` 인수를 사용하여 번들을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-216">Install the bundle by using the `--install` or `--upgrade` argument.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="bd62c-217">Linux용 System Center Operations Manager 에이전트가 이미 설치된 경우처럼 기존 패키지가 설치된 경우에는 `--upgrade` 인수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-217">If any existing packages are installed such as when the System Center Operations Manager agent for Linux is already installed, use the `--upgrade` argument.</span></span> <span data-ttu-id="bd62c-218">설치 중에 Operations Management Suite에 연결하려면 `-w <WorkspaceID>` 및 `-s <Shared Key>` 매개 변수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-218">To connect to Operations Management Suite during installation, provide the `-w <WorkspaceID>` and `-s <Shared Key>` parameters.</span></span>


#### <a name="to-install-and-onboard-directly"></a><span data-ttu-id="bd62c-219">직접 설치하고 직접 등록하려면</span><span class="sxs-lookup"><span data-stu-id="bd62c-219">To install and onboard directly</span></span>
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key>
```

#### <a name="to-upgrade-the-agent-package"></a><span data-ttu-id="bd62c-220">에이전트 패키지를 업그레이드하려면</span><span class="sxs-lookup"><span data-stu-id="bd62c-220">To upgrade the agent package</span></span>
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade
```

#### <a name="to-install-and-onboard-to-a-workspace-in-us-government-cloud"></a><span data-ttu-id="bd62c-221">미국 정부 클라우드의 작업 영역에 설치하고 등록하려면</span><span class="sxs-lookup"><span data-stu-id="bd62c-221">To install and onboard to a workspace in US Government Cloud</span></span>
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key> -d opinsights.azure.us
```

## <a name="configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway"></a><span data-ttu-id="bd62c-222">HTTP 프록시 서버 또는 OMS 게이트웨이에서 사용하도록 에이전트 구성</span><span class="sxs-lookup"><span data-stu-id="bd62c-222">Configuring the agent for use with an HTTP proxy server or OMS Gateway</span></span>
<span data-ttu-id="bd62c-223">OMS Agent for Linux는 HTTP 또는 HTTPS 프록시 서버 또는 OMS 게이트웨이를 통해 OMS 서비스와 통신하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-223">The OMS Agent for Linux supports communicating either through an HTTP or HTTPS proxy server or OMS Gateway to the OMS service.</span></span>  <span data-ttu-id="bd62c-224">익명 및 기본 인증(사용자 이름/암호) 둘 다 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-224">Both anonymous and basic authentication (username/password) is supported.</span></span>  

### <a name="proxy-configuration"></a><span data-ttu-id="bd62c-225">프록시 구성</span><span class="sxs-lookup"><span data-stu-id="bd62c-225">Proxy configuration</span></span>
<span data-ttu-id="bd62c-226">프록시 구성 값은 다음 구문을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-226">The proxy configuration value has the following syntax:</span></span>

`[protocol://][user:password@]proxyhost[:port]`

<span data-ttu-id="bd62c-227">속성</span><span class="sxs-lookup"><span data-stu-id="bd62c-227">Property</span></span>|<span data-ttu-id="bd62c-228">설명</span><span class="sxs-lookup"><span data-stu-id="bd62c-228">Description</span></span>
-|-
<span data-ttu-id="bd62c-229">프로토콜</span><span class="sxs-lookup"><span data-stu-id="bd62c-229">Protocol</span></span>|<span data-ttu-id="bd62c-230">HTTP 또는 HTTPS</span><span class="sxs-lookup"><span data-stu-id="bd62c-230">http or https</span></span>
<span data-ttu-id="bd62c-231">사용자</span><span class="sxs-lookup"><span data-stu-id="bd62c-231">user</span></span>|<span data-ttu-id="bd62c-232">프록시 인증을 위한 선택적 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="bd62c-232">Optional username for proxy authentication</span></span>
<span data-ttu-id="bd62c-233">password</span><span class="sxs-lookup"><span data-stu-id="bd62c-233">password</span></span>|<span data-ttu-id="bd62c-234">프록시 인증을 위한 선택적 암호</span><span class="sxs-lookup"><span data-stu-id="bd62c-234">Optional password for proxy authentication</span></span>
<span data-ttu-id="bd62c-235">proxyhost</span><span class="sxs-lookup"><span data-stu-id="bd62c-235">proxyhost</span></span>|<span data-ttu-id="bd62c-236">프록시 서버/OMS 게이트웨이의 주소 또는 FQDN</span><span class="sxs-lookup"><span data-stu-id="bd62c-236">Address or FQDN of the proxy server/OMS Gateway</span></span>
<span data-ttu-id="bd62c-237">포트</span><span class="sxs-lookup"><span data-stu-id="bd62c-237">port</span></span>|<span data-ttu-id="bd62c-238">프록시 서버/OMS 게이트웨이 대한 선택적 포트 번호</span><span class="sxs-lookup"><span data-stu-id="bd62c-238">Optional port number for the proxy server/OMS Gateway</span></span>

<span data-ttu-id="bd62c-239">예: `http://user01:password@proxy01.contoso.com:8080`</span><span class="sxs-lookup"><span data-stu-id="bd62c-239">For example: `http://user01:password@proxy01.contoso.com:8080`</span></span>

<span data-ttu-id="bd62c-240">설치 중에 또는 설치 후에 proxy.conf 구성 파일을 수정하여 프록시 서버를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-240">The proxy server can be specified during installation or by modifying the proxy.conf configuration file after installation.</span></span>   

### <a name="specify-proxy-configuration-during-installation"></a><span data-ttu-id="bd62c-241">설치 중 프록시 구성 지정</span><span class="sxs-lookup"><span data-stu-id="bd62c-241">Specify proxy configuration during installation</span></span>
<span data-ttu-id="bd62c-242">omsagent 설치 번들에 대한 `-p` 또는 `--proxy` 인수는 사용할 프록시 구성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-242">The `-p` or `--proxy` argument for the omsagent installation bundle specifies the proxy configuration to use.</span></span> 

```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -p http://<proxy user>:<proxy password>@<proxy address>:<proxy port> -w <workspace id> -s <shared key>
```

### <a name="define-the-proxy-configuration-in-a-file"></a><span data-ttu-id="bd62c-243">파일에 프록시 구성 정의</span><span class="sxs-lookup"><span data-stu-id="bd62c-243">Define the proxy configuration in a file</span></span>
<span data-ttu-id="bd62c-244">프록시 구성은 파일 `/etc/opt/microsoft/omsagent/proxy.conf` 및 `/etc/opt/microsoft/omsagent/conf/proxy.conf `에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-244">The proxy configuration can be set in the files `/etc/opt/microsoft/omsagent/proxy.conf`  and `/etc/opt/microsoft/omsagent/conf/proxy.conf `.</span></span> <span data-ttu-id="bd62c-245">이 파일을 직접 만들거나 편집할 수 있지만 파일에 omiuser 그룹 읽기 권한을 부여하도록 사용 권한을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-245">The files can be directly created or edited, but their permissions must be updated to grant the omiuser user read permission on the files.</span></span> <span data-ttu-id="bd62c-246">예:</span><span class="sxs-lookup"><span data-stu-id="bd62c-246">For example:</span></span>
```
proxyconf="https://proxyuser:proxypassword@proxyserver01:8080"
sudo echo $proxyconf >>/etc/opt/microsoft/omsagent/proxy.conf
sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf
sudo chmod 600 /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf  
sudo /opt/microsoft/omsagent/bin/service_control restart [<workspace id>]
```

### <a name="removing-the-proxy-configuration"></a><span data-ttu-id="bd62c-247">프록시 구성 제거</span><span class="sxs-lookup"><span data-stu-id="bd62c-247">Removing the proxy configuration</span></span>
<span data-ttu-id="bd62c-248">이전에 정의된 프록시 구성을 제거하고 직접 연결로 되돌리려면 proxy.conf 파일을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-248">To remove a previously defined proxy configuration and revert to direct connectivity, remove the proxy.conf file:</span></span>
```
sudo rm /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf
sudo /opt/microsoft/omsagent/bin/service_control restart 
```

## <a name="onboarding-with-operations-management-suite"></a><span data-ttu-id="bd62c-249">Operations Management Suite에 등록</span><span class="sxs-lookup"><span data-stu-id="bd62c-249">Onboarding with Operations Management Suite</span></span>
<span data-ttu-id="bd62c-250">번들 설치 동안 작업 영역 ID 및 키가 제공되지 않았으므로 나중에 에이전트를 Operations Management Suite에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-250">If a workspace ID and key were not provided during the bundle installation, the agent must be subsequently registered with Operations Management Suite.</span></span>

### <a name="onboarding-using-the-command-line"></a><span data-ttu-id="bd62c-251">명령줄을 사용하여 등록</span><span class="sxs-lookup"><span data-stu-id="bd62c-251">Onboarding using the command line</span></span>
<span data-ttu-id="bd62c-252">작업 영역에 대한 작업 영역 ID 및 키를 제공하여 omsadmin.sh 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-252">Run the omsadmin.sh command supplying the workspace id and key for your workspace.</span></span> <span data-ttu-id="bd62c-253">이 명령은 루트 권한(sudo 권한 상승)으로 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-253">This command must be run as root (with sudo elevation):</span></span>
```
cd /opt/microsoft/omsagent/bin
sudo ./omsadmin.sh -w <WorkspaceID> -s <Shared Key>
```

### <a name="onboarding-using-a-file"></a><span data-ttu-id="bd62c-254">파일을 사용하는 등록</span><span class="sxs-lookup"><span data-stu-id="bd62c-254">Onboarding using a file</span></span>
1.  <span data-ttu-id="bd62c-255">파일 `/etc/omsagent-onboard.conf`를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-255">Create the file `/etc/omsagent-onboard.conf`.</span></span> <span data-ttu-id="bd62c-256">이 파일은 루트에 대해 읽을 수 있고 쓸 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-256">The file must be readable and writable for root.</span></span>
`sudo vi /etc/omsagent-onboard.conf`
2.  <span data-ttu-id="bd62c-257">작업 영역 ID 및 공유 키를 사용하여 파일에 다음 줄을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-257">Insert the following lines in the file with your Workspace ID and Shared Key:</span></span>

        WORKSPACE_ID=<WorkspaceID>  
        SHARED_KEY=<Shared Key>  
   
3.  <span data-ttu-id="bd62c-258">다음 명령을 실행하여 OMS에 등록합니다. `sudo /opt/microsoft/omsagent/bin/omsadmin.sh`</span><span class="sxs-lookup"><span data-stu-id="bd62c-258">Run the following command to Onboard to OMS: `sudo /opt/microsoft/omsagent/bin/omsadmin.sh`</span></span>
4.  <span data-ttu-id="bd62c-259">이 파일은 등록이 성공적으로 수행되면 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-259">The file is deleted on successful onboarding.</span></span>

## <a name="enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager"></a><span data-ttu-id="bd62c-260">OMS Agent for Linux에서 System Center Operations Manager에 보고하도록 설정</span><span class="sxs-lookup"><span data-stu-id="bd62c-260">Enable the OMS Agent for Linux to report to System Center Operations Manager</span></span>
<span data-ttu-id="bd62c-261">OMS Agent for Linux에서 System Center Operations Manager 관리 그룹에 보고하도록 구성하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-261">Perform the following steps to configure the OMS Agent for Linux to report to a System Center Operations Manager management group.</span></span>  

1. <span data-ttu-id="bd62c-262">파일 `/etc/opt/omi/conf/omiserver.conf`</span><span class="sxs-lookup"><span data-stu-id="bd62c-262">Edit the file `/etc/opt/omi/conf/omiserver.conf`</span></span>
2. <span data-ttu-id="bd62c-263">**httpsport=** 로 시작되는 줄이 1270 포트를 지정하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-263">Ensure that the line beginning with **httpsport=** defines the port 1270.</span></span> <span data-ttu-id="bd62c-264">예: `httpsport=1270`</span><span class="sxs-lookup"><span data-stu-id="bd62c-264">Such as: `httpsport=1270`</span></span>
3. <span data-ttu-id="bd62c-265">OMI 서버를 다시 시작합니다. `sudo /opt/omi/bin/service_control restart`</span><span class="sxs-lookup"><span data-stu-id="bd62c-265">Restart the OMI server: `sudo /opt/omi/bin/service_control restart`</span></span>

## <a name="agent-logs"></a><span data-ttu-id="bd62c-266">에이전트 로그</span><span class="sxs-lookup"><span data-stu-id="bd62c-266">Agent logs</span></span>
<span data-ttu-id="bd62c-267">OMS Agent for Linux용 로그는 `/var/opt/microsoft/omsagent/<workspace id>/log/`에서 찾을 수 있습니다. omsconfig(에이전트 구성) 프로그램용 로그는 `/var/opt/microsoft/omsconfig/log/`에서 찾을 수 있습니다. OMI 및 SCX 구성 요소(성능 메트릭 데이터 제공)용 로그는 `/var/opt/omi/log/ and /var/opt/microsoft/scx/log`에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-267">The logs for the OMS Agent for Linux can be found at: `/var/opt/microsoft/omsagent/<workspace id>/log/` The logs for the omsconfig (agent configuration) program can be found at: `/var/opt/microsoft/omsconfig/log/` Logs for the OMI and SCX components (which provide performance metrics data) can be found at: `/var/opt/omi/log/ and /var/opt/microsoft/scx/log`</span></span>

### <a name="log-rotation-configuration"></a><span data-ttu-id="bd62c-268">로그 순환 구성##</span><span class="sxs-lookup"><span data-stu-id="bd62c-268">Log rotation configuration##</span></span>
<span data-ttu-id="bd62c-269">omsagent에 대한 로그 순환 구성은 `/etc/logrotate.d/omsagent-<workspace id>`에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-269">The log rotate configuration for omsagent can be found at: `/etc/logrotate.d/omsagent-<workspace id>`</span></span>

<span data-ttu-id="bd62c-270">기본 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-270">The default settings are:</span></span> 
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

## <a name="uninstalling-the-oms-agent-for-linux"></a><span data-ttu-id="bd62c-271">OMS Agent for Linux 제거</span><span class="sxs-lookup"><span data-stu-id="bd62c-271">Uninstalling the OMS Agent for Linux</span></span>
<span data-ttu-id="bd62c-272">`--purge` 인수로 번들.sh 파일을 실행하여 에이전트 패키지를 제거할 수 있습니다. 그러면 컴퓨터에서 에이전트와 해당 구성이 완전히 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-272">The agent packages can be uninstalled by running the bundle .sh file with the `--purge` argument, which completely removes the agent and its configuration from the computer.</span></span>   

```
> sudo rpm -e omsconfig
> sudo rpm -e omsagent
> sudo /opt/microsoft/scx/bin/uninstall
```

## <a name="troubleshooting"></a><span data-ttu-id="bd62c-273">문제 해결</span><span class="sxs-lookup"><span data-stu-id="bd62c-273">Troubleshooting</span></span>

### <a name="issue-unable-to-connect-through-proxy-to-oms"></a><span data-ttu-id="bd62c-274">문제: 프록시를 통해 OMS에 연결할 수 없음</span><span class="sxs-lookup"><span data-stu-id="bd62c-274">Issue: Unable to connect through proxy to OMS</span></span>

#### <a name="probable-causes"></a><span data-ttu-id="bd62c-275">가능한 원인</span><span class="sxs-lookup"><span data-stu-id="bd62c-275">Probable causes</span></span>
* <span data-ttu-id="bd62c-276">등록하는 동안 지정된 프록시가 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-276">The proxy specified during onboarding was incorrect</span></span>
* <span data-ttu-id="bd62c-277">OMS 서비스 끝점이 데이터 센터의 허용 목록에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-277">The OMS Service Endpoints are not whitelistested in your datacenter</span></span> 

#### <a name="resolutions"></a><span data-ttu-id="bd62c-278">해결 방법</span><span class="sxs-lookup"><span data-stu-id="bd62c-278">Resolutions</span></span>
1. <span data-ttu-id="bd62c-279">다음 명령과 `-v` 옵션을 사용하여 OMS Agent for Linux가 있는 OMS 서비스에 다시 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-279">Reonboard to the OMS Service with the OMS Agent for Linux by using the following command with the option `-v` enabled.</span></span> <span data-ttu-id="bd62c-280">OMS 서비스에 대한 프록시를 통해 연결되는 에이전트의 자세한 정보를 출력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-280">This allows verbose output of the agent connecting through the proxy to the OMS Service.</span></span> 
`/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`

2. <span data-ttu-id="bd62c-281">[HTTP 프록시 서버에서 사용하기 위해 에이전트 구성(#configuring the-agent-for-use-with-a-http-proxy-server)] 섹션을 검토하여 프록시 서버를 통해 통신하도록 에이전트를 적절히 구성했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-281">Review the section [Configuring the agent for use with an HTTP proxy server(#configuring the-agent-for-use-with-a-http-proxy-server) to verify you have properly configured the agent to communicate through a proxy server.</span></span>    
* <span data-ttu-id="bd62c-282">다음 OMS 서비스 끝점이 허용 목록에 있는지 한 번 더 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-282">Double check that the following OMS Service endpoints are whitelisted:</span></span>

    |<span data-ttu-id="bd62c-283">에이전트 리소스</span><span class="sxs-lookup"><span data-stu-id="bd62c-283">Agent Resource</span></span>| <span data-ttu-id="bd62c-284">포트</span><span class="sxs-lookup"><span data-stu-id="bd62c-284">Ports</span></span> |  
    |------|---------|  
    |<span data-ttu-id="bd62c-285">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="bd62c-285">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="bd62c-286">포트 443</span><span class="sxs-lookup"><span data-stu-id="bd62c-286">Port 443</span></span>|   
    |<span data-ttu-id="bd62c-287">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="bd62c-287">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="bd62c-288">포트 443</span><span class="sxs-lookup"><span data-stu-id="bd62c-288">Port 443</span></span>|   
    |<span data-ttu-id="bd62c-289">ods.systemcenteradvisor.com</span><span class="sxs-lookup"><span data-stu-id="bd62c-289">ods.systemcenteradvisor.com</span></span> | <span data-ttu-id="bd62c-290">포트 443</span><span class="sxs-lookup"><span data-stu-id="bd62c-290">Port 443</span></span>|   
    |<span data-ttu-id="bd62c-291">*.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="bd62c-291">*.blob.core.windows.net/</span></span> | <span data-ttu-id="bd62c-292">포트 443</span><span class="sxs-lookup"><span data-stu-id="bd62c-292">Port 443</span></span>|   

### <a name="issue-you-receive-a-403-error-when-trying-to-onboard"></a><span data-ttu-id="bd62c-293">문제: 등록하는 동안 403 오류 발생</span><span class="sxs-lookup"><span data-stu-id="bd62c-293">Issue: You receive a 403 error when trying to onboard</span></span>

#### <a name="probable-causes"></a><span data-ttu-id="bd62c-294">가능한 원인</span><span class="sxs-lookup"><span data-stu-id="bd62c-294">Probable causes</span></span>
* <span data-ttu-id="bd62c-295">Linux 서버의 날짜 및 시간이 올바르지 않습니다</span><span class="sxs-lookup"><span data-stu-id="bd62c-295">Date and Time is incorrect on Linux Server</span></span> 
* <span data-ttu-id="bd62c-296">사용된 작업 영역 ID 및 작업 영역 키가 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-296">Workspace ID and Workspace Key used are not correct</span></span>

#### <a name="resolution"></a><span data-ttu-id="bd62c-297">해결 방법</span><span class="sxs-lookup"><span data-stu-id="bd62c-297">Resolution</span></span>

1. <span data-ttu-id="bd62c-298">명령 시간을 사용하여 Linux 서버에서 시간을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-298">Check the time on your Linux server with the command date.</span></span> <span data-ttu-id="bd62c-299">시간이 현재 시간에서 +/-15분인 경우 등록이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-299">If the time is +/- 15 minutes from current time, then onboarding fails.</span></span> <span data-ttu-id="bd62c-300">이 문제를 해결하려면 Linux 서버의 날짜 및/또는 시간대를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-300">To correct this update the date and/or timezone of your Linux server.</span></span> 
2. <span data-ttu-id="bd62c-301">Linux용 OMS 에이전트 최신 버전이 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-301">Verify you have installed the latest version of the OMS Agent for Linux.</span></span>  <span data-ttu-id="bd62c-302">최신 버전은 시간 차이로 인해 등록 실패가 발생하는지 여부를 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-302">The newest version now notifies you if time skew is causing the onboarding failure.</span></span>
3. <span data-ttu-id="bd62c-303">이 항목 앞부분의 설치 지침에 따라 올바른 작업 영역 ID 및 작업 영역 키를 사용하여 다시 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-303">Reonboard using correct Workspace ID and Workspace Key following the installation instructions earlier in this topic.</span></span>

### <a name="issue-you-see-a-500-and-404-error-in-the-log-file-right-after-onboarding"></a><span data-ttu-id="bd62c-304">문제: 등록 직후에 로그 파일에 500 및 404 오류가 표시됨</span><span class="sxs-lookup"><span data-stu-id="bd62c-304">Issue: You see a 500 and 404 error in the log file right after onboarding</span></span>
<span data-ttu-id="bd62c-305">이 문제는 알려진 문제이며 Linux 데이터를 OMS 작업 영역으로 처음 업로드할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-305">This is a known issue that occurs on first upload of Linux data into an OMS workspace.</span></span> <span data-ttu-id="bd62c-306">이 문제는 전송되는 데이터 또는 서비스 환경에 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-306">This does not affect data being sent or service experience.</span></span>

### <a name="issue--you-are-not-seeing-any-data-in-the-oms-portal"></a><span data-ttu-id="bd62c-307">문제: OMS 포털에서 데이터가 보이지 않음</span><span class="sxs-lookup"><span data-stu-id="bd62c-307">Issue:  You are not seeing any data in the OMS portal</span></span>

#### <a name="probable-causes"></a><span data-ttu-id="bd62c-308">가능한 원인</span><span class="sxs-lookup"><span data-stu-id="bd62c-308">Probable causes</span></span>

- <span data-ttu-id="bd62c-309">OMS 서비스 등록이 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-309">Onboarding to the OMS Service failed</span></span>
- <span data-ttu-id="bd62c-310">OMS 서비스에 대한 연결이 차단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-310">Connection to the OMS Service is blocked</span></span>
- <span data-ttu-id="bd62c-311">Linux용 OMS 에이전트가 백업되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-311">OMS Agent for Linux data is backed up</span></span>

#### <a name="resolutions"></a><span data-ttu-id="bd62c-312">해결 방법</span><span class="sxs-lookup"><span data-stu-id="bd62c-312">Resolutions</span></span>
1. <span data-ttu-id="bd62c-313">`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` 파일이 있는지 확인하여 OMS 서비스 등록에 성공했는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-313">Check if onboarding the OMS Service was successful by checking if the following file exists: `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`</span></span>
2. <span data-ttu-id="bd62c-314">`omsadmin.sh` 명령줄 명령을 사용하여 다시 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-314">Reonboard using the `omsadmin.sh` command-line instructions</span></span>
3. <span data-ttu-id="bd62c-315">프록시를 사용하는 경우 앞서 제공된 프록시 문제 해결 단계를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bd62c-315">If using a proxy, refer to the proxy resolution steps provided earlier.</span></span>
4. <span data-ttu-id="bd62c-316">OMS Agent for Linux가 OMS 서비스와 통신할 수 없는 경우 에이전트의 데이터가 최대 버퍼 크기인 50MB로 대기될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-316">In some cases, when the OMS Agent for Linux cannot communicate with the OMS Service, data on the agent is queued to the full buffer size, which is 50 MB.</span></span> <span data-ttu-id="bd62c-317">명령 `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`를 실행하여 Linux용 OMS 에이전트를 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-317">The OMS Agent for Linux should be restarted by running the following command: `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`.</span></span> 

    >[!NOTE]
    ><span data-ttu-id="bd62c-318">이 문제는 에이전트 버전 1.1.0-28 및 이상에서 해결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bd62c-318">This issue is fixed in agent version 1.1.0-28 and later.</span></span>
> 