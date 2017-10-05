---
title: "Azure Log Analytics에 Windows 컴퓨터 연결 | Microsoft Docs"
description: "이 문서에서는 사용자 지정 버전의 MMA(Microsoft Monitoring Agent)를 사용하여 온-프레미스 인프라의 Windows 컴퓨터를 Log Analytics 서비스에 연결하는 단계를 보여 줍니다."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 932f7b8c-485c-40c1-98e3-7d4c560876d2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 48a0eaeb10d406d551c9e5870edde06809bd7544
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-windows-computers-to-the-log-analytics-service-in-azure"></a><span data-ttu-id="794c8-103">Azure에서 Log Analytics 서비스에 Windows 컴퓨터 연결</span><span class="sxs-lookup"><span data-stu-id="794c8-103">Connect Windows computers to the Log Analytics service in Azure</span></span>

<span data-ttu-id="794c8-104">이 문서에서는 사용자 지정 버전의 MMA(Microsoft Monitoring Agent)를 사용하여 온-프레미스 인프라의 Windows 컴퓨터를 OMS 작업 영역에 연결하는 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-104">This article shows the steps to connect Windows computers in your on-premises infrastructure to OMS workspaces by using a customized version of the Microsoft Monitoring Agent (MMA).</span></span> <span data-ttu-id="794c8-105">에이전트에서 Log Analytics 서비스에 데이터를 보내고 해당 데이터를 보고 사용할 수 있도록 등록하려는 전체 컴퓨터에 대한 에이전트를 설치 및 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-105">You need to install and connect agents for all of the computers that you want to onboard in order for them to send data to the Log Analytics service and to view and act on that data.</span></span> <span data-ttu-id="794c8-106">각 에이전트는 여러 작업 영역에 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-106">Each agent can report to multiple workspaces.</span></span>

<span data-ttu-id="794c8-107">Azure 자동화에서 설정, 명령줄 또는 DSC(필요한 상태 구성)를 사용하여 에이전트를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-107">You can install agents using Setup, command line, or with Desired State Configuration (DSC) in Azure Automation.</span></span>  

>[!NOTE]
<span data-ttu-id="794c8-108">Azure에서 실행되는 가상 컴퓨터의 경우 [가상 컴퓨터 확장](log-analytics-azure-vm-extension.md)을 사용하여 설치를 간소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-108">For virtual machines running in Azure, you can simplify installation by using the [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="794c8-109">에이전트는 인터넷 연결이 가능한 컴퓨터에서 연결을 사용하여 인터넷에 연결하고 OMS로 데이터를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-109">On computers with Internet connectivity, the agent uses the connection to the Internet to send data to OMS.</span></span> <span data-ttu-id="794c8-110">인터넷 연결이 없는 컴퓨터의 경우 프록시 또는 [OMS Gateway](log-analytics-oms-gateway.md)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-110">For computers that do not have Internet connectivity, you can use a proxy or the [OMS Gateway](log-analytics-oms-gateway.md).</span></span>

<span data-ttu-id="794c8-111">Windows 컴퓨터를 OMS에 연결하려면 간단한 3단계를 수행하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-111">Connecting your Windows computers to OMS is straightforward using three simple steps:</span></span>

1. <span data-ttu-id="794c8-112">OMS 포털에서 에이전트 설치 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-112">Download the agent setup file from the OMS portal</span></span>
2. <span data-ttu-id="794c8-113">선택한 방법을 사용하여 에이전트를 설치합니다</span><span class="sxs-lookup"><span data-stu-id="794c8-113">Install the agent using the method you choose</span></span>
3. <span data-ttu-id="794c8-114">에이전트를 구성하거나 필요한 경우 추가 작업 영역을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-114">Configure the agent or add additional workspaces, if necessary</span></span>

<span data-ttu-id="794c8-115">아래 다이어그램은 에이전트를 설치 및 구성한 이후 Windows 컴퓨터와 OMS 사이의 관계를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-115">The following diagram shows the relationship between your Windows computers and OMS after you’ve installed and configured agents.</span></span>

![oms-direct-agent-diagram](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

<span data-ttu-id="794c8-117">IT 보안 정책이 네트워크에서 컴퓨터를 인터넷에 연결하도록 허용하지 않는 경우 OMS 게이트웨이에 연결하도록 컴퓨터를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-117">If your IT security policies do not allow computers on your network to connect to the Internet, you can configure your computers to connect to the OMS Gateway.</span></span> <span data-ttu-id="794c8-118">서버가 OMS 게이트웨이를 통해 OMS 서비스와 통신할 수 있도록 구성하는 방법에 대한 자세한 내용 및 단계에 대해서는 [OMS 게이트웨이 사용하여 OMS에 컴퓨터 연결](log-analytics-oms-gateway.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="794c8-118">For more information and steps on how to configure your servers to communicate through an OMS Gateway to the OMS service, see [Connect computers to OMS using the OMS Gateway](log-analytics-oms-gateway.md).</span></span>

## <a name="system-requirements-and-required-configuration"></a><span data-ttu-id="794c8-119">시스템 요구 사항 및 필수 구성</span><span class="sxs-lookup"><span data-stu-id="794c8-119">System requirements and required configuration</span></span>
<span data-ttu-id="794c8-120">에이전트를 설치 또는 배포하기 전에 아래 정보를 검토하여 필수 조건을 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-120">Before you install or deploy agents, review the following details to ensure you meet the requirements.</span></span>

- <span data-ttu-id="794c8-121">OMS MMA는 Windows Server 2008 SP 1 이상 또는 Windows 7 SP1 이상을 실행 중인 컴퓨터에만 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-121">You can only install the OMS MMA on computers running Windows Server 2008 SP 1 or later or Windows 7 SP1 or later.</span></span>
- <span data-ttu-id="794c8-122">Azure 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-122">You need an Azure subscription.</span></span>  <span data-ttu-id="794c8-123">자세한 내용은 [Log Analytics 시작](log-analytics-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="794c8-123">For more information, see [Get started with Log Analytics](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="794c8-124">각 Windows 컴퓨터는 HTTPS 또는 OMS Gateway를 사용하여 인터넷에 연결할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-124">Each Windows computer must be able to connect to the Internet using HTTPS or to the OMS Gateway.</span></span> <span data-ttu-id="794c8-125">직접 연결하거나 프록시를 통하거나 OMS Gateway를 통해 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-125">This connection can be direct, via a proxy, or through the OMS Gateway.</span></span>
- <span data-ttu-id="794c8-126">OMS MMA를 독립 실행형 컴퓨터, 서버, 가상 컴퓨터에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-126">You can install the OMS MMA on stand-alone computers, servers, and virtual machines.</span></span> <span data-ttu-id="794c8-127">Azure에서 호스팅되는 가상 컴퓨터를 OMS에 연결하려면 [Log Analytics에 Azure 가상 컴퓨터 연결](log-analytics-azure-vm-extension.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="794c8-127">If you want to connect Azure-hosted virtual machines to OMS, see [Connect Azure virtual machines to Log Analytics](log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="794c8-128">에이전트는 다양한 리소스에 TCP 포트 443을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-128">The agent needs to use TCP port 443 for various resources.</span></span>

### <a name="network"></a><span data-ttu-id="794c8-129">네트워크</span><span class="sxs-lookup"><span data-stu-id="794c8-129">Network</span></span>

<span data-ttu-id="794c8-130">Windows 에이전트를 OMS 서비스에 연결하고 등록한 경우 포트 번호 및 도메인 URL을 비롯한 네트워크 리소스에 대한 액세스 권한을 가져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-130">For Windows agents to connect to and register with the OMS service, they must have access to network resources, including the port numbers and domain URLs.</span></span>

- <span data-ttu-id="794c8-131">프록시 서버의 경우 적절한 프록시 서버 리소스가 에이전트 설정에 구성되어 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-131">For proxy servers, you need to ensure that the appropriate proxy server resources are configured in agent settings.</span></span>
- <span data-ttu-id="794c8-132">인터넷에 대한 액세스를 제한하는 방화벽의 경우 사용자 또는 네트워킹 엔지니어는 OMS에 대한 액세스를 허용하도록 방화벽을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-132">For firewalls that restrict access to the Internet, you or your networking engineers need to configure your firewall to permit access to OMS.</span></span> <span data-ttu-id="794c8-133">에이전트 설정에서 아무 작업도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-133">No action is needed in agent settings.</span></span>

<span data-ttu-id="794c8-134">다음 표에서는 통신에 필요한 리소스를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-134">The following table shows resources needed for communication.</span></span>

>[!NOTE]
><span data-ttu-id="794c8-135">다음 리소스 중 일부는 Log Analytics의 이전 이름인 Operational Insights를 언급합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-135">Some of the following resources mention Operational Insights, which was a previous name for Log Analytics.</span></span>

| <span data-ttu-id="794c8-136">에이전트 리소스</span><span class="sxs-lookup"><span data-stu-id="794c8-136">Agent Resource</span></span> | <span data-ttu-id="794c8-137">포트</span><span class="sxs-lookup"><span data-stu-id="794c8-137">Ports</span></span> | <span data-ttu-id="794c8-138">HTTPS 검사 무시</span><span class="sxs-lookup"><span data-stu-id="794c8-138">Bypass HTTPS inspection</span></span> |
|---|---|---|
| <span data-ttu-id="794c8-139">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="794c8-139">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="794c8-140">443</span><span class="sxs-lookup"><span data-stu-id="794c8-140">443</span></span> | <span data-ttu-id="794c8-141">예</span><span class="sxs-lookup"><span data-stu-id="794c8-141">Yes</span></span> |
| <span data-ttu-id="794c8-142">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="794c8-142">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="794c8-143">443</span><span class="sxs-lookup"><span data-stu-id="794c8-143">443</span></span> | <span data-ttu-id="794c8-144">예</span><span class="sxs-lookup"><span data-stu-id="794c8-144">Yes</span></span> |
| <span data-ttu-id="794c8-145">*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="794c8-145">*.blob.core.windows.net</span></span> | <span data-ttu-id="794c8-146">443</span><span class="sxs-lookup"><span data-stu-id="794c8-146">443</span></span> | <span data-ttu-id="794c8-147">예</span><span class="sxs-lookup"><span data-stu-id="794c8-147">Yes</span></span> |
| <span data-ttu-id="794c8-148">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="794c8-148">*.azure-automation.net</span></span> | <span data-ttu-id="794c8-149">443</span><span class="sxs-lookup"><span data-stu-id="794c8-149">443</span></span> | <span data-ttu-id="794c8-150">예</span><span class="sxs-lookup"><span data-stu-id="794c8-150">Yes</span></span> |



## <a name="download-the-agent-setup-file-from-oms"></a><span data-ttu-id="794c8-151">OMS에서 에이전트 설치 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="794c8-151">Download the agent setup file from OMS</span></span>
1. <span data-ttu-id="794c8-152">OMS 포털의 **개요** 페이지에서 **설정** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-152">In the OMS portal, on the **Overview** page, click the **Settings** tile.</span></span>  <span data-ttu-id="794c8-153">위쪽에서 **연결된 원본** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-153">Click the **Connected Sources** tab at the top.</span></span>  
    <span data-ttu-id="794c8-154">![연결된 원본 탭](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span><span class="sxs-lookup"><span data-stu-id="794c8-154">![Connected Sources tab](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span></span>
2. <span data-ttu-id="794c8-155">**Windows Servers**를 클릭한 다음 사용하는 컴퓨터 프로세서 유형에 해당하는 **Windows 에이전트 다운로드**를 클릭하여 설치 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-155">Click **Windows Servers** and then click **Download Windows Agent** applicable to your computer processor type to download the setup file.</span></span>
3. <span data-ttu-id="794c8-156">**작업 영역 ID**오른쪽에서 복사 아이콘을 클릭하고 ID를 메모장에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-156">On the right of **Workspace ID**, click the copy icon and paste the ID into Notepad.</span></span>
4. <span data-ttu-id="794c8-157">**기본 키**오른쪽에서 복사 아이콘을 클릭하고 키를 메모장에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-157">On the right of **Primary Key**, click the copy icon and paste the key into Notepad.</span></span>     

## <a name="install-the-agent-using-setup"></a><span data-ttu-id="794c8-158">설치 프로그램을 사용하여 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="794c8-158">Install the agent using setup</span></span>
1. <span data-ttu-id="794c8-159">설치 프로그램을 실행하여 관리하려는 컴퓨터에 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-159">Run Setup to install the agent on a computer that you want to manage.</span></span>
2. <span data-ttu-id="794c8-160">Welcome 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-160">On the Welcome page, click **Next**.</span></span>
3. <span data-ttu-id="794c8-161">사용 조건 페이지에서 라이선스를 읽고 **동의함**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-161">On the License Terms page, read the license and then click **I Agree**.</span></span>
4. <span data-ttu-id="794c8-162">대상 폴더 페이지에서 기본 설치 폴더를 변경 또는 유지하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-162">On the Destination Folder page, change or keep the default installation folder and then click **Next**.</span></span>
5. <span data-ttu-id="794c8-163">에이전트 설치 옵션 페이지에서 에이전트를 Azure Log Analytics(OMS), Operations Manager에 연결하도록 선택하거나 에이전트를 나중에 구성하려는 경우 선택 항목을 비워둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-163">On the Agent Setup Options page, you can choose to connect the agent to Azure Log Analytics (OMS), Operations Manager, or you can leave the choices blank if you want to configure the agent later.</span></span> <span data-ttu-id="794c8-164">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-164">Click **Next**.</span></span>   
    - <span data-ttu-id="794c8-165">Azure Log Analytics(OMS)에 연결하려는 경우 이전 절차에서 메모장에 복사해 둔 **작업 영역 ID**와 **작업 영역 키(기본 키)**를 붙여 넣은 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-165">If you chose to connect to Azure Log Analytics (OMS), paste the **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in the previous procedure and then click **Next**.</span></span>  
        <span data-ttu-id="794c8-166">![작업 영역 ID 및 기본 키 붙여넣기](./media/log-analytics-windows-agents/connect-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="794c8-166">![paste Workspace ID and Primary Key](./media/log-analytics-windows-agents/connect-workspace.png)</span></span>
    - <span data-ttu-id="794c8-167">Operations Manager에 연결할 경우 **관리 그룹 이름**, **관리 서버** 이름, **관리 서버 포트**를 입력하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-167">If you chose to connect to Operations Manager, type the **Management Group Name**, **Management Server** name, and **Management Server Port**, and then click **Next**.</span></span> <span data-ttu-id="794c8-168">에이전트 작업 페이지에서 로컬 시스템 계정 또는 로컬 도메인 계정을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-168">On the Agent Action Account page, choose either the Local System account or a local domain account and then click **Next**.</span></span>  
        <span data-ttu-id="794c8-169">![관리 그룹 구성](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![에이전트 작업 계정](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span><span class="sxs-lookup"><span data-stu-id="794c8-169">![management group configuration](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![agent action account](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span></span>

6. <span data-ttu-id="794c8-170">설치 준비 페이지에서 선택 항목을 검토한 다음 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-170">On the Ready to Install page, review your choices and then click **Install**.</span></span>
7. <span data-ttu-id="794c8-171">구성 완료 페이지에서 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-171">On the Configuration completed successfully page, click **Finish**.</span></span>
8. <span data-ttu-id="794c8-172">완료되면 **제어판**에 **Microsoft Monitoring Agent**가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-172">When complete, the **Microsoft Monitoring Agent** appears in **Control Panel**.</span></span> <span data-ttu-id="794c8-173">여기에서 구성을 검토하고 에이전트가 Operational Insights(OMS)에 연결되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-173">You can review your configuration there and verify that the agent is connected to Operational Insights (OMS).</span></span> <span data-ttu-id="794c8-174">OMS에 연결되면 에이전트에 **Microsoft Monitoring Agent가 Microsoft Operations Management Suite 서비스에 성공적으로 연결되었습니다.**와 같은 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-174">When connected to OMS, the agent displays a message stating: **The Microsoft Monitoring Agent has successfully connected to the Microsoft Operations Management Suite service.**</span></span>

## <a name="configure-proxy-settings"></a><span data-ttu-id="794c8-175">프록시 설정 구성</span><span class="sxs-lookup"><span data-stu-id="794c8-175">Configure proxy settings</span></span>

<span data-ttu-id="794c8-176">제어판을 사용하여 Microsoft 모니터링 에이전트에 대한 프록시 설정을 구성하려면 다음 절차를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-176">You can use the following procedure to configure proxy settings for the Microsoft Monitoring Agent using Control Panel.</span></span> <span data-ttu-id="794c8-177">각 서버에 이 절차를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-177">You need to use this procedure for each server.</span></span> <span data-ttu-id="794c8-178">많은 서버를 구성해야 하는 경우, 스크립트를 사용하여 보다 쉽게 이 프로세스를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-178">If you have many servers that you need to configure, you might find it easier to use a script to automate this process.</span></span> <span data-ttu-id="794c8-179">그럴 경우 다음 절차 [스크립트를 사용하여 Microsoft 모니터링 에이전트에 대한 프록시 설정을 구성하려면](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="794c8-179">If so, see the next procedure [To configure proxy settings for the Microsoft Monitoring Agent using a script](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span></span>

### <a name="to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-control-panel"></a><span data-ttu-id="794c8-180">제어판을 사용하여 Microsoft Monitoring Agent에 대한 프록시 설정을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="794c8-180">To configure proxy settings for the Microsoft Monitoring Agent using Control Panel</span></span>
1. <span data-ttu-id="794c8-181">**제어판**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-181">Open **Control Panel**.</span></span>
2. <span data-ttu-id="794c8-182">**Microsoft Monitoring Agent**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-182">Open **Microsoft Monitoring Agent**.</span></span>
3. <span data-ttu-id="794c8-183">**프록시 설정** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-183">Click the **Proxy Settings** tab.</span></span>  
    <span data-ttu-id="794c8-184">![프록시 설정 탭](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span><span class="sxs-lookup"><span data-stu-id="794c8-184">![proxy settings tab](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span></span>
4. <span data-ttu-id="794c8-185">**프록시 서버 사용** 을 선택하고 URL과 포트 번호를 입력하고, 필요한 경우 표시된 예제와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-185">Select **Use a proxy server** and type the URL and port number, if one is needed, similar to the example shown.</span></span> <span data-ttu-id="794c8-186">프록시 서버에 인증이 필요한 경우 프록시 서버에 액세스 하려면 사용자 이름과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-186">If your proxy server requires authentication, type the username and password to access the proxy server.</span></span>


### <a name="verify-agent-connectivity-to-oms"></a><span data-ttu-id="794c8-187">OMS에 대한 에이전트 연결 확인</span><span class="sxs-lookup"><span data-stu-id="794c8-187">Verify agent connectivity to OMS</span></span>

<span data-ttu-id="794c8-188">에이전트가 다음 절차를 사용하여 OMS와 통신하고 있는지 여부를 쉽게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-188">You can easily verify whether your agents are communicating with OMS using the following procedure:</span></span>

1.  <span data-ttu-id="794c8-189">Windows 에이전트가 설치된 컴퓨터에서 제어판을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-189">On the computer with the Windows agent, open Control Panel.</span></span>
2.  <span data-ttu-id="794c8-190">Microsoft Monitoring Agent를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-190">Open Microsoft Monitoring Agent.</span></span>
3.  <span data-ttu-id="794c8-191">Azure Log Analytics(OMS) 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-191">Click the Azure Log Analytics (OMS) tab.</span></span>
4.  <span data-ttu-id="794c8-192">상태 열에는 Operations Management Suite 서비스에 성공적으로 연결된 에이전트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-192">In the Status column, you should see that the agent connected successfully to the Operations Management Suite service.</span></span>

![연결된 에이전트](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script"></a><span data-ttu-id="794c8-194">스크립트를 사용하여 Microsoft 모니터링 에이전트에 대한 프록시 설정을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="794c8-194">To configure proxy settings for the Microsoft Monitoring Agent using a script</span></span>
<span data-ttu-id="794c8-195">다음 샘플을 복사하여 사용자 환경에 특정한 정보로 업데이트하고 PS1 파일 이름 확장명으로 저장한 다음 OMS 서비스에 직접 연결되는 각 컴퓨터에서 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-195">Copy the following sample, update it with information specific to your environment, save it with a PS1 file name extension, and then run the script on each computer that connects directly to the OMS service.</span></span>

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get the Health Service configuration object.  We need to determine if we
    #have the right update rollup with the API we need.  If not, no need to run the rest of the script.
    $healthServiceSettings = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'

    $proxyMethod = $healthServiceSettings | Get-Member -Name 'SetProxyInfo'

    if (!$proxyMethod)
    {
         Write-Output 'Health Service proxy API not present, will not update settings.'
         return
    }

    Write-Output "Clearing proxy settings."
    $healthServiceSettings.SetProxyInfo('', '', '')

    $ProxyUserName = $cred.username

    Write-Output "Setting proxy to $ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-the-agent-using-the-command-line"></a><span data-ttu-id="794c8-196">명령줄을 사용하여 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="794c8-196">Install the agent using the command line</span></span>
- <span data-ttu-id="794c8-197">명령줄을 사용하여 에이전트를 설치하려면 다음 예제를 수정한 다음 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-197">Modify and then use the following example to install the agent using the command line.</span></span> <span data-ttu-id="794c8-198">예제에서는 완전 자동 설치를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-198">The example performs a fully silent installation.</span></span>

    >[!NOTE]
    <span data-ttu-id="794c8-199">에이전트를 업그레이드하려는 경우 Log Analytics 스크립팅 API를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-199">If you want to upgrade an agent, you need to use the Log Analytics scripting API.</span></span> <span data-ttu-id="794c8-200">에이전트를 업그레이드하려면 다음 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="794c8-200">See the next section to upgrade an agent.</span></span>

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

<span data-ttu-id="794c8-201">에이전트는 `/c`를 통해 IExpress를 자동 압축 풀기 프로그램으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-201">The agent uses IExpress as its self-extractor using the `/c` command.</span></span> <span data-ttu-id="794c8-202">[IExpress 소프트웨어 업데이트 패키지의 명령줄 스위치](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages)의 명령줄 스위치를 확인하고 필요에 맞게 예제를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-202">You can see the command-line switches at [Command-line switches for IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) and then update the example to suit your needs.</span></span>

|<span data-ttu-id="794c8-203">MMA 관련 옵션</span><span class="sxs-lookup"><span data-stu-id="794c8-203">MMA-specific options</span></span>                   |<span data-ttu-id="794c8-204">참고 사항</span><span class="sxs-lookup"><span data-stu-id="794c8-204">Notes</span></span>         |
|---------------------------------------|--------------|
|<span data-ttu-id="794c8-205">ADD_OPINSIGHTS_WORKSPACE</span><span class="sxs-lookup"><span data-stu-id="794c8-205">ADD_OPINSIGHTS_WORKSPACE</span></span>               | <span data-ttu-id="794c8-206">1 = 작업 영역에 보고하도록 에이전트 구성</span><span class="sxs-lookup"><span data-stu-id="794c8-206">1 = Configure the agent to report to a workspace</span></span>                |
|<span data-ttu-id="794c8-207">OPINSIGHTS_WORKSPACE_ID</span><span class="sxs-lookup"><span data-stu-id="794c8-207">OPINSIGHTS_WORKSPACE_ID</span></span>                | <span data-ttu-id="794c8-208">추가할 작업 영역의 작업 영역 ID(guid)</span><span class="sxs-lookup"><span data-stu-id="794c8-208">Workspace Id (guid) for the workspace to add</span></span>                    |
|<span data-ttu-id="794c8-209">OPINSIGHTS_WORKSPACE_KEY</span><span class="sxs-lookup"><span data-stu-id="794c8-209">OPINSIGHTS_WORKSPACE_KEY</span></span>               | <span data-ttu-id="794c8-210">작업 영역에서 처음 인증하는 데 사용되는 작업 영역 키</span><span class="sxs-lookup"><span data-stu-id="794c8-210">Workspace key used to initially authenticate with the workspace</span></span> |
|<span data-ttu-id="794c8-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span><span class="sxs-lookup"><span data-stu-id="794c8-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span></span>  | <span data-ttu-id="794c8-212">작업 영역이 있는 클라우드 환경 지정</span><span class="sxs-lookup"><span data-stu-id="794c8-212">Specify the cloud environment where the workspace is located</span></span> <br> <span data-ttu-id="794c8-213">0 = Azure 상용 클라우드(기본값)</span><span class="sxs-lookup"><span data-stu-id="794c8-213">0 = Azure commercial cloud (default)</span></span> <br> <span data-ttu-id="794c8-214">1 = Azure Government</span><span class="sxs-lookup"><span data-stu-id="794c8-214">1 = Azure Government</span></span> |
|<span data-ttu-id="794c8-215">OPINSIGHTS_PROXY_URL</span><span class="sxs-lookup"><span data-stu-id="794c8-215">OPINSIGHTS_PROXY_URL</span></span>               | <span data-ttu-id="794c8-216">사용할 프록시의 URI</span><span class="sxs-lookup"><span data-stu-id="794c8-216">URI for the proxy to use</span></span> |
|<span data-ttu-id="794c8-217">OPINSIGHTS_PROXY_USERNAME</span><span class="sxs-lookup"><span data-stu-id="794c8-217">OPINSIGHTS_PROXY_USERNAME</span></span>               | <span data-ttu-id="794c8-218">인증된 프록시에 액세스할 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="794c8-218">Username to access an authenticated proxy</span></span> |
|<span data-ttu-id="794c8-219">OPINSIGHTS_PROXY_PASSWORD</span><span class="sxs-lookup"><span data-stu-id="794c8-219">OPINSIGHTS_PROXY_PASSWORD</span></span>               | <span data-ttu-id="794c8-220">인증된 프록시에 액세스할 암호</span><span class="sxs-lookup"><span data-stu-id="794c8-220">Password to access an authenticated proxy</span></span> |

>[!NOTE]
<span data-ttu-id="794c8-221">IExpress의 명령줄 길이 제한에 도달하지 않으려면 작업 영역이 구성되지 않은 상태로 에이전트를 설치한 후 스크립트를 사용하여 작업 영역에 대한 구성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-221">To avoid hitting the command-line length limit of IExpress, install the agent with no workspace configured and then use a script to set configuration for the workspace.</span></span>

>[!NOTE]
<span data-ttu-id="794c8-222">`OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` 매개 변수를 사용할 때 `Command line option syntax error.`이 발생하는 경우 다음과 같은 해결 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-222">If you get a `Command line option syntax error.` when using the `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parameter, you can use the following workaround:</span></span>
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a><span data-ttu-id="794c8-223">스크립트를 사용하여 작업 영역 추가</span><span class="sxs-lookup"><span data-stu-id="794c8-223">Add a workspace using a script</span></span>
<span data-ttu-id="794c8-224">다음 예제처럼 Log Analytics 에이전트 스크립팅 API를 사용하여 작업 영역을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-224">Add a workspace using the Log Analytics agent scripting API with the following example:</span></span>

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

<span data-ttu-id="794c8-225">Azure에서 미국 정부에 대한 작업 영역을 추가하려면 다음 스크립트 샘플을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-225">To add a workspace in Azure for US Government, use the following script sample:</span></span>
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
<span data-ttu-id="794c8-226">이전에 명령줄 또는 스크립트를 사용하여 에이전트를 설치 또는 구성한 경우 `EnableAzureOperationalInsights`가 `AddCloudWorkspace`로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-226">If you've used the command line or script previously to install or configure the agent, `EnableAzureOperationalInsights` was replaced by `AddCloudWorkspace`.</span></span>

## <a name="install-the-agent-using-dsc-in-azure-automation"></a><span data-ttu-id="794c8-227">Azure 자동화에서 DSC를 사용하여 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="794c8-227">Install the agent using DSC in Azure Automation</span></span>

<span data-ttu-id="794c8-228">다음 스크립트 예제를 사용하여 Azure Automation에 DSC를 사용하여 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-228">You can use the following script example to install the agent using DSC in Azure Automation.</span></span> <span data-ttu-id="794c8-229">예제는 64비트 에이전트를 설치하고 `URI` 값으로 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-229">The example installs the 64-bit agent, identified by the `URI` value.</span></span> <span data-ttu-id="794c8-230">또한 URI 값을 바꿔 32비트 버전을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-230">You can also use the 32-bit version by replacing the URI value.</span></span> <span data-ttu-id="794c8-231">두 버전에 대한 URL</span><span class="sxs-lookup"><span data-stu-id="794c8-231">The URIs for both versions are:</span></span>

- <span data-ttu-id="794c8-232">Windows 64비트 에이전트 - https://go.microsoft.com/fwlink/?LinkId=828603</span><span class="sxs-lookup"><span data-stu-id="794c8-232">Windows 64-bit agent - https://go.microsoft.com/fwlink/?LinkId=828603</span></span>
- <span data-ttu-id="794c8-233">Windows 32비트 에이전트 - https://go.microsoft.com/fwlink/?LinkId=828604</span><span class="sxs-lookup"><span data-stu-id="794c8-233">Windows 32-bit agent - https://go.microsoft.com/fwlink/?LinkId=828604</span></span>


>[!NOTE]
<span data-ttu-id="794c8-234">이 절차 및 스크립트 예제는 기존 에이전트를 업그레이드하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-234">This procedure and script example will not upgrade an existing agent.</span></span>

1. <span data-ttu-id="794c8-235">[http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) 에서 Azure 자동화로 xPSDesiredStateConfiguration DSC 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-235">Import the xPSDesiredStateConfiguration DSC Module from [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) into Azure Automation.</span></span>  
2.  <span data-ttu-id="794c8-236">*OPSINSIGHTS_WS_ID* 및 *OPSINSIGHTS_WS_KEY*의 Azure Automation 변수 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-236">Create Azure Automation variable assets for *OPSINSIGHTS_WS_ID* and *OPSINSIGHTS_WS_KEY*.</span></span> <span data-ttu-id="794c8-237">*OPSINSIGHTS_WS_ID*를 OMS Log Analytics 작업 영역 ID에 설정하고 *OPSINSIGHTS_WS_KEY*를 작업 영역의 기본 키에 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-237">Set *OPSINSIGHTS_WS_ID* to your OMS Log Analytics workspace ID and set *OPSINSIGHTS_WS_KEY* to the primary key of your workspace.</span></span>
3.  <span data-ttu-id="794c8-238">다음 스크립트를 사용하고 MMAgent.ps1로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-238">Use the following script and save it as MMAgent.ps1</span></span>
4.  <span data-ttu-id="794c8-239">다음 예제를 수정 및 사용하여 Azure 자동화에 DSC를 사용하여 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-239">Modify and then use the following example to install the agent using DSC in Azure Automation.</span></span> <span data-ttu-id="794c8-240">Azure 자동화 인터페이스 또는 cmdlet을 사용하여 MMAgent.ps1을 Azure 자동화로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-240">Import MMAgent.ps1 into Azure Automation by using the Azure Automation interface or cmdlet.</span></span>
5.  <span data-ttu-id="794c8-241">구성에 노드를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-241">Assign a node to the configuration.</span></span> <span data-ttu-id="794c8-242">15분 이내에 노드가 구성을 점검하고 MMA가 노드로 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-242">Within 15 minutes, the node checks its configuration and the MMA is pushed to the node.</span></span>

```PowerShell
Configuration MMAgent
{
    $OIPackageLocalPath = "C:\MMASetup-AMD64.exe"
    $OPSINSIGHTS_WS_ID = Get-AutomationVariable -Name "OPSINSIGHTS_WS_ID"
    $OPSINSIGHTS_WS_KEY = Get-AutomationVariable -Name "OPSINSIGHTS_WS_KEY"


    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    Node OMSnode {
        Service OIService
        {
            Name = "HealthService"
            State = "Running"
            DependsOn = "[Package]OI"
        }

        xRemoteFile OIPackage {
            Uri = "https://go.microsoft.com/fwlink/?LinkId=828603"
            DestinationPath = $OIPackageLocalPath
        }

        Package OI {
            Ensure = "Present"
            Path  = $OIPackageLocalPath
            Name = "Microsoft Monitoring Agent"
            ProductId = "8A7F2C51-4C7D-4BFD-9014-91D11F24AAE2"
            Arguments = '/C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=' + $OPSINSIGHTS_WS_ID + ' OPINSIGHTS_WORKSPACE_KEY=' + $OPSINSIGHTS_WS_KEY + ' AcceptEndUserLicenseAgreement=1"'
            DependsOn = "[xRemoteFile]OIPackage"
        }
    }
}


```

### <a name="get-the-latest-productid-value"></a><span data-ttu-id="794c8-243">최신 ProductId 값 가져오기</span><span class="sxs-lookup"><span data-stu-id="794c8-243">Get the latest ProductId value</span></span>

<span data-ttu-id="794c8-244">MMAgent.ps1 스크립트에 있는 `ProductId value`은 각 에이전트 버전에 대해 고유합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-244">The `ProductId value` in the MMAgent.ps1 script is unique to each agent version.</span></span> <span data-ttu-id="794c8-245">각 에이전트의 업데이트된 버전이 게시되면, ProductId 값이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-245">When an updated version of each agent is published, the ProductId value changes.</span></span> <span data-ttu-id="794c8-246">따라서 나중에 ProductId가 변경되면 간단한 스크립트를 사용하여 에이전트 버전을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-246">So, when the ProductId changes in the future, you can find the agent version using a simple script.</span></span> <span data-ttu-id="794c8-247">테스트 서버에 최신 에이전트 버전을 설치한 후에 다음 스크립트를 사용하여 설치된 ProductId 값을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-247">After you have the latest agent version installed on a test server, you can use the following script to get the installed ProductId value.</span></span> <span data-ttu-id="794c8-248">최신 ProductId 값을 사용하면 MMAgent.ps1 스크립트에서 값을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-248">Using the latest ProductId value, you can update the value in the MMAgent.ps1 script.</span></span>

```PowerShell
$InstalledApplications  = Get-ChildItem hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall


foreach ($Application in $InstalledApplications)

{

     $Key = Get-ItemProperty $Application.PSPath

     if ($Key.DisplayName -eq "Microsoft Monitoring Agent")

     {

        $Key.DisplayName

        Write-Output ("Product ID is: " + $Key.PSChildName.Substring(1,$Key.PSChildName.Length -2))

     }

}  
```

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a><span data-ttu-id="794c8-249">에이전트를 수동으로 구성하거나 추가 작업 영역 추가</span><span class="sxs-lookup"><span data-stu-id="794c8-249">Configure an agent manually or add additional workspaces</span></span>
<span data-ttu-id="794c8-250">에이전트를 설치하고 구성하지 않은 경우 또는 에이전트가 여러 작업 영역에 보고하도록 하려는 경우 다음 정보를 참조하여 사용하도록 설정하거나 다시 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-250">If you've installed agents but did not configure them or if you want the agent to report to multiple workspaces, you can use the following information to enable an agent or reconfigure it.</span></span> <span data-ttu-id="794c8-251">에이전트를 구성한 후, 에이전트 서비스로 등록하고 필요한 구성 정보와 솔루션 정보를 포함하는 관리 팩을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-251">After you've configured the agent, it will register with the agent service and will get necessary configuration information and management packs that contain solution information.</span></span>

1. <span data-ttu-id="794c8-252">Microsoft Monitoring Agent를 설치한 다음 **제어판**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-252">After you've installed the Microsoft Monitoring Agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="794c8-253">**Microsoft Monitoring Agent**를 연 다음 **Azure Log Analytics(OMS)** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-253">Open **Microsoft Monitoring Agent** and then click the **Azure Log Analytics (OMS)** tab.</span></span>   
3. <span data-ttu-id="794c8-254">**추가**를 클릭하여 **Log Analytics 작업 영역 추가** 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-254">Click **Add** to open the **Add a Log Analytics Workspace** box.</span></span>
4. <span data-ttu-id="794c8-255">추가할 작업 영역에 대해 이전 절차에서 메모장에 복사해 둔 **작업 영역 ID**와 **작업 영역 키(기본 키)**를 붙여 넣은 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-255">Paste the **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in a previous procedure for the workspace that you want to add and then click **OK**.</span></span>  
    <span data-ttu-id="794c8-256">![Operational Insights 구성](./media/log-analytics-windows-agents/add-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="794c8-256">![configure Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span></span>

<span data-ttu-id="794c8-257">에이전트에서 모니터링하는 컴퓨터에서 데이터를 수집한 후, OMS에서 모니터링하는 컴퓨터의 수가 **설정**의 **연결된 원본** 탭에 **연결된 서버**로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-257">After data is collected from computers monitored by the agent, the number of computers monitored by OMS will appear in the OMS portal on the **Connected Sources** tab in **Settings** as **Servers Connected**.</span></span>


## <a name="to-disable-an-agent"></a><span data-ttu-id="794c8-258">에이전트를 사용하지 않도록 설정하려면</span><span class="sxs-lookup"><span data-stu-id="794c8-258">To disable an agent</span></span>
1. <span data-ttu-id="794c8-259">에이전트를 설치한 후 **제어판**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-259">After installing the agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="794c8-260">Microsoft Monitoring Agent를 연 다음 **Azure Log Analytics(OMS)** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-260">Open Microsoft Monitoring Agent and then click the **Azure Log Analytics (OMS)** tab.</span></span>
3. <span data-ttu-id="794c8-261">작업 영역을 선택하고 **제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-261">Select a workspace and then click **Remove**.</span></span> <span data-ttu-id="794c8-262">다른 모든 작업 영역에 대해 이 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-262">Repeat this step for all other workspaces.</span></span>


## <a name="optionally-configure-agents-to-report-to-an-operations-manager-management-group"></a><span data-ttu-id="794c8-263">또는 에이전트에서 Operations Manager 관리 그룹으로 보고하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-263">Optionally, configure agents to report to an Operations Manager management group</span></span>

<span data-ttu-id="794c8-264">IT 인프라에서 Operations Manager를 사용할 경우 Operations Manager 에이전트로 MMA 에이전트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-264">If you use Operations Manager in your IT infrastructure, you can also use the MMA agent as an Operations Manager agent.</span></span>

### <a name="to-configure-mma-agents-to-report-to-an-operations-manager-management-group"></a><span data-ttu-id="794c8-265">MMA 에이전트에서 Operations Manager 관리 그룹으로 보고하도록 구성하려면</span><span class="sxs-lookup"><span data-stu-id="794c8-265">To configure MMA agents to report to an Operations Manager management group</span></span>
1.  <span data-ttu-id="794c8-266">에이전트가 설치된 컴퓨터에서 **제어판**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-266">On the computer where the agent is installed, open **Control Panel**.</span></span>  
2.  <span data-ttu-id="794c8-267">**Microsoft Monitoring Agent**를 연 다음 **Operations Manager** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-267">Open **Microsoft Monitoring Agent** and then click the **Operations Manager** tab.</span></span>  
    <span data-ttu-id="794c8-268">![Microsoft Monitoring Agent Operations Manager 탭](./media/log-analytics-windows-agents/om-mg01.png)</span><span class="sxs-lookup"><span data-stu-id="794c8-268">![Microsoft Monitoring Agent Operations Manager tab](./media/log-analytics-windows-agents/om-mg01.png)</span></span>
3.  <span data-ttu-id="794c8-269">Operations Manager 서버가 Active Directory와 통합된 경우 **AD DS에서 관리 그룹 할당 자동 업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-269">If your Operations Manager servers have integration with Active Directory, click **Automatically update management group assignments from AD DS**.</span></span>
4.  <span data-ttu-id="794c8-270">**추가**를 클릭하여 **관리 그룹 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-270">Click **Add** to open the **Add a Management Group** dialog box.</span></span>  
    <span data-ttu-id="794c8-271">![Microsoft Monitoring Agent 관리 그룹 추가](./media/log-analytics-windows-agents/oms-mma-om02.png)</span><span class="sxs-lookup"><span data-stu-id="794c8-271">![Microsoft Monitoring Agent Add a Management Group](./media/log-analytics-windows-agents/oms-mma-om02.png)</span></span>
5.  <span data-ttu-id="794c8-272">**관리 그룹 이름** 상자에 관리 그룹의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-272">In **Management group name** box, type the name of your management group.</span></span>
6.  <span data-ttu-id="794c8-273">**기본 관리 서버** 상자에 기본 관리 서버의 컴퓨터 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-273">In the **Primary management server** box, type the computer name of the primary management server.</span></span>
7.  <span data-ttu-id="794c8-274">**관리 서버 포트** 상자에 TCP 포트 번호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-274">In the **Management server port** box, type the TCP port number.</span></span>
8.  <span data-ttu-id="794c8-275">**에이전트 작업 계정**에서 로컬 시스템 계정 또는 로컬 도메인 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-275">Under **Agent Action Account**, choose either the Local System account or a local domain account.</span></span>
9.  <span data-ttu-id="794c8-276">**확인**을 클릭하여 **관리 그룹 추가** 대화 상자를 닫은 다음 **확인**을 클릭하여 **Microsoft Monitoring Agent 속성** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-276">Click **OK** to close the **Add a Management Group** dialog box and then click **OK** to close the **Microsoft Monitoring Agent Properties** dialog box.</span></span>


## <a name="next-steps"></a><span data-ttu-id="794c8-277">다음 단계</span><span class="sxs-lookup"><span data-stu-id="794c8-277">Next steps</span></span>

- <span data-ttu-id="794c8-278">[솔루션 갤러리에서 Log Analytics 솔루션을 추가](log-analytics-add-solutions.md) 하여 기능을 추가하고 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="794c8-278">[Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md) to add functionality and gather data.</span></span>
