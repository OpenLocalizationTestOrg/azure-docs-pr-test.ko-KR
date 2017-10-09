---
title: "로그 분석 aaaConnect Windows 컴퓨터 tooAzure | Microsoft Docs"
description: "이 문서는 hello Microsoft Monitoring Agent (MMA)의 사용자 지정된 된 버전을 사용 하 여 온-프레미스 인프라 toohello 로그 분석 서비스의에서 hello 단계 tooconnect hello Windows 컴퓨터를 표시 합니다."
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
ms.openlocfilehash: 7e15f9eeb0440bd2f6557d7215df701526e4f9aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-windows-computers-toohello-log-analytics-service-in-azure"></a><span data-ttu-id="fd282-103">Azure에서 Windows 컴퓨터 toohello 로그 분석 서비스 연결</span><span class="sxs-lookup"><span data-stu-id="fd282-103">Connect Windows computers toohello Log Analytics service in Azure</span></span>

<span data-ttu-id="fd282-104">이 문서에서는 hello 단계 tooconnect Windows 컴퓨터 온-프레미스 인프라 tooOMS 작업 영역에서 사용자 지정된 된 버전의 Microsoft Monitoring Agent (MMA) hello 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-104">This article shows hello steps tooconnect Windows computers in your on-premises infrastructure tooOMS workspaces by using a customized version of hello Microsoft Monitoring Agent (MMA).</span></span> <span data-ttu-id="fd282-105">Tooinstall 필요 하 고 모든 toosend 데이터 toohello 로그 분석 서비스와 tooview 및 해당 데이터에서 작동 되도록 하려면에서 tooonboard hello 컴퓨터에 대 한 에이전트를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-105">You need tooinstall and connect agents for all of hello computers that you want tooonboard in order for them toosend data toohello Log Analytics service and tooview and act on that data.</span></span> <span data-ttu-id="fd282-106">각 에이전트 toomultiple 작업 영역을 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-106">Each agent can report toomultiple workspaces.</span></span>

<span data-ttu-id="fd282-107">Azure 자동화에서 설정, 명령줄 또는 DSC(필요한 상태 구성)를 사용하여 에이전트를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-107">You can install agents using Setup, command line, or with Desired State Configuration (DSC) in Azure Automation.</span></span>  

>[!NOTE]
<span data-ttu-id="fd282-108">Azure에서 실행 중인 가상 컴퓨터에 대 한 hello를 사용 하 여 설치를 단순화할 수 [가상 컴퓨터 확장](log-analytics-azure-vm-extension.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-108">For virtual machines running in Azure, you can simplify installation by using hello [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="fd282-109">인터넷에 연결 된 컴퓨터에서 hello 에이전트 hello 연결 toohello 인터넷 toosend 데이터 tooOMS를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-109">On computers with Internet connectivity, hello agent uses hello connection toohello Internet toosend data tooOMS.</span></span> <span data-ttu-id="fd282-110">인터넷에 연결 되지 않은 컴퓨터를 사용할 수 있습니다는 프록시 또는 hello [OMS 게이트웨이](log-analytics-oms-gateway.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-110">For computers that do not have Internet connectivity, you can use a proxy or hello [OMS Gateway](log-analytics-oms-gateway.md).</span></span>

<span data-ttu-id="fd282-111">Windows 컴퓨터 tooOMS 연결 하는 것은 세 가지 간단한 단계를 사용 하 여 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-111">Connecting your Windows computers tooOMS is straightforward using three simple steps:</span></span>

1. <span data-ttu-id="fd282-112">Hello OMS 포털에서 hello 에이전트 설치 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="fd282-112">Download hello agent setup file from hello OMS portal</span></span>
2. <span data-ttu-id="fd282-113">선택한 hello 메서드를 사용 하 여 hello 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-113">Install hello agent using hello method you choose</span></span>
3. <span data-ttu-id="fd282-114">Hello 에이전트를 구성 하거나 필요한 경우 추가 작업 영역을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-114">Configure hello agent or add additional workspaces, if necessary</span></span>

<span data-ttu-id="fd282-115">hello 다음 다이어그램에서는 Windows 컴퓨터와 OMS 간의 hello 관계를 설치 하 고 에이전트를 구성한 후</span><span class="sxs-lookup"><span data-stu-id="fd282-115">hello following diagram shows hello relationship between your Windows computers and OMS after you’ve installed and configured agents.</span></span>

![oms-direct-agent-diagram](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

<span data-ttu-id="fd282-117">IT 보안 정책을 네트워크 tooconnect toohello 인터넷에서 컴퓨터를 허용 하지 않으므로, 컴퓨터 tooconnect toohello OMS 게이트웨이 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-117">If your IT security policies do not allow computers on your network tooconnect toohello Internet, you can configure your computers tooconnect toohello OMS Gateway.</span></span> <span data-ttu-id="fd282-118">자세한 내용 및 단계 tooconfigure OMS 게이트웨이 toohello OMS 서비스를 통해 서버 toocommunicate 프로그램 참조에 대 한 [hello OMS 게이트웨이 사용 하 여 컴퓨터 tooOMS 연결](log-analytics-oms-gateway.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-118">For more information and steps on how tooconfigure your servers toocommunicate through an OMS Gateway toohello OMS service, see [Connect computers tooOMS using hello OMS Gateway](log-analytics-oms-gateway.md).</span></span>

## <a name="system-requirements-and-required-configuration"></a><span data-ttu-id="fd282-119">시스템 요구 사항 및 필수 구성</span><span class="sxs-lookup"><span data-stu-id="fd282-119">System requirements and required configuration</span></span>
<span data-ttu-id="fd282-120">설치 하거나 에이전트를 배포 하기 전에 hello 요구 사항을 충족 하는 tooensure 검토 hello 다음에 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-120">Before you install or deploy agents, review hello following details tooensure you meet hello requirements.</span></span>

- <span data-ttu-id="fd282-121">Windows 7 SP1 또는 Windows Server 2008 SP 1 이후 버전을 실행 하는 컴퓨터에 OMS MMA hello를만 설치할 수 이상입니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-121">You can only install hello OMS MMA on computers running Windows Server 2008 SP 1 or later or Windows 7 SP1 or later.</span></span>
- <span data-ttu-id="fd282-122">Azure 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-122">You need an Azure subscription.</span></span>  <span data-ttu-id="fd282-123">자세한 내용은 [Log Analytics 시작](log-analytics-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fd282-123">For more information, see [Get started with Log Analytics](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="fd282-124">각 Windows 컴퓨터 수 tooconnect toohello 인터넷 있어야 합니다. HTTPS 또는 toohello OMS 게이트웨이 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-124">Each Windows computer must be able tooconnect toohello Internet using HTTPS or toohello OMS Gateway.</span></span> <span data-ttu-id="fd282-125">이 연결은 직접 hello OMS 게이트웨이 또는 프록시를 통해 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-125">This connection can be direct, via a proxy, or through hello OMS Gateway.</span></span>
- <span data-ttu-id="fd282-126">OMS MMA hello 독립 실행형 컴퓨터, 서버 및 가상 컴퓨터에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-126">You can install hello OMS MMA on stand-alone computers, servers, and virtual machines.</span></span> <span data-ttu-id="fd282-127">가상 컴퓨터 호스 티 드 Azure tooOMS tooconnect 참조 [연결 Azure 가상 컴퓨터 tooLog 분석](log-analytics-azure-vm-extension.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-127">If you want tooconnect Azure-hosted virtual machines tooOMS, see [Connect Azure virtual machines tooLog Analytics](log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="fd282-128">hello 에이전트는 다양 한 리소스에 대 한 toouse TCP 포트 443을 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-128">hello agent needs toouse TCP port 443 for various resources.</span></span>

### <a name="network"></a><span data-ttu-id="fd282-129">네트워크</span><span class="sxs-lookup"><span data-stu-id="fd282-129">Network</span></span>

<span data-ttu-id="fd282-130">Windows 에이전트 tooconnect tooand 레지스터 hello OMS 서비스에 대 한 hello 포트 번호 및 도메인 Url을 포함 하 여 toonetwork 리소스에 액세스 가져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-130">For Windows agents tooconnect tooand register with hello OMS service, they must have access toonetwork resources, including hello port numbers and domain URLs.</span></span>

- <span data-ttu-id="fd282-131">프록시 서버에 대 한 적절 한 프록시 서버를 에이전트 설정에 구성 된 리소스가 hello tooensure를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-131">For proxy servers, you need tooensure that hello appropriate proxy server resources are configured in agent settings.</span></span>
- <span data-ttu-id="fd282-132">인터넷 액세스 toohello 제한 하는 방화벽, 또는 네트워킹 엔지니어 필요 tooconfigure 사용자 방화벽 toopermit 액세스 tooOMS 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-132">For firewalls that restrict access toohello Internet, you or your networking engineers need tooconfigure your firewall toopermit access tooOMS.</span></span> <span data-ttu-id="fd282-133">에이전트 설정에서 아무 작업도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-133">No action is needed in agent settings.</span></span>

<span data-ttu-id="fd282-134">다음 표에서 hello 통신에 필요한 리소스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-134">hello following table shows resources needed for communication.</span></span>

>[!NOTE]
><span data-ttu-id="fd282-135">Hello 다음 리소스 중 일부 언급 Operational Insights 로그 분석에 대 한 이전 이름 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-135">Some of hello following resources mention Operational Insights, which was a previous name for Log Analytics.</span></span>

| <span data-ttu-id="fd282-136">에이전트 리소스</span><span class="sxs-lookup"><span data-stu-id="fd282-136">Agent Resource</span></span> | <span data-ttu-id="fd282-137">포트</span><span class="sxs-lookup"><span data-stu-id="fd282-137">Ports</span></span> | <span data-ttu-id="fd282-138">HTTPS 검사 무시</span><span class="sxs-lookup"><span data-stu-id="fd282-138">Bypass HTTPS inspection</span></span> |
|---|---|---|
| <span data-ttu-id="fd282-139">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="fd282-139">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="fd282-140">443</span><span class="sxs-lookup"><span data-stu-id="fd282-140">443</span></span> | <span data-ttu-id="fd282-141">예</span><span class="sxs-lookup"><span data-stu-id="fd282-141">Yes</span></span> |
| <span data-ttu-id="fd282-142">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="fd282-142">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="fd282-143">443</span><span class="sxs-lookup"><span data-stu-id="fd282-143">443</span></span> | <span data-ttu-id="fd282-144">예</span><span class="sxs-lookup"><span data-stu-id="fd282-144">Yes</span></span> |
| <span data-ttu-id="fd282-145">*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="fd282-145">*.blob.core.windows.net</span></span> | <span data-ttu-id="fd282-146">443</span><span class="sxs-lookup"><span data-stu-id="fd282-146">443</span></span> | <span data-ttu-id="fd282-147">예</span><span class="sxs-lookup"><span data-stu-id="fd282-147">Yes</span></span> |
| <span data-ttu-id="fd282-148">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="fd282-148">*.azure-automation.net</span></span> | <span data-ttu-id="fd282-149">443</span><span class="sxs-lookup"><span data-stu-id="fd282-149">443</span></span> | <span data-ttu-id="fd282-150">예</span><span class="sxs-lookup"><span data-stu-id="fd282-150">Yes</span></span> |



## <a name="download-hello-agent-setup-file-from-oms"></a><span data-ttu-id="fd282-151">OMS에서 hello 에이전트 설치 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="fd282-151">Download hello agent setup file from OMS</span></span>
1. <span data-ttu-id="fd282-152">Hello에 hello OMS 포털에서 **개요** 페이지에서 hello **설정** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-152">In hello OMS portal, on hello **Overview** page, click hello **Settings** tile.</span></span>  <span data-ttu-id="fd282-153">Hello 클릭 **연결 된 원본** hello 위쪽 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-153">Click hello **Connected Sources** tab at hello top.</span></span>  
    <span data-ttu-id="fd282-154">![연결된 원본 탭](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span><span class="sxs-lookup"><span data-stu-id="fd282-154">![Connected Sources tab](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span></span>
2. <span data-ttu-id="fd282-155">클릭 **Windows 서버** 클릭 하 고 **Windows 에이전트 다운로드** 적용 가능한 tooyour 컴퓨터 프로세서 종류 toodownload hello 설치 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-155">Click **Windows Servers** and then click **Download Windows Agent** applicable tooyour computer processor type toodownload hello setup file.</span></span>
3. <span data-ttu-id="fd282-156">Hello의 오른쪽에 **작업 영역 ID**hello 복사 아이콘을 클릭 하 고 hello ID를 메모장에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-156">On hello right of **Workspace ID**, click hello copy icon and paste hello ID into Notepad.</span></span>
4. <span data-ttu-id="fd282-157">Hello의 오른쪽에 **기본 키**hello 복사 아이콘을 클릭 하 고 hello 키를 메모장에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-157">On hello right of **Primary Key**, click hello copy icon and paste hello key into Notepad.</span></span>     

## <a name="install-hello-agent-using-setup"></a><span data-ttu-id="fd282-158">설치 프로그램을 사용 하 여 hello 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="fd282-158">Install hello agent using setup</span></span>
1. <span data-ttu-id="fd282-159">Toomanage 지정 하는 컴퓨터에서 설치 프로그램 tooinstall hello 에이전트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-159">Run Setup tooinstall hello agent on a computer that you want toomanage.</span></span>
2. <span data-ttu-id="fd282-160">Hello 시작 페이지에서 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-160">On hello Welcome page, click **Next**.</span></span>
3. <span data-ttu-id="fd282-161">Hello 사용 조건 페이지 hello 라이선스 읽고 클릭 **동의**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-161">On hello License Terms page, read hello license and then click **I Agree**.</span></span>
4. <span data-ttu-id="fd282-162">Hello 대상 폴더 페이지에서 변경 또는 hello 기본 설치 폴더를 유지 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-162">On hello Destination Folder page, change or keep hello default installation folder and then click **Next**.</span></span>
5. <span data-ttu-id="fd282-163">Hello 에이전트 설치 옵션 페이지에서 tooconnect hello 에이전트 tooAzure 로그 분석 (OMS) Operations Manager를 선택할 수 있습니다 하거나 있습니다 비워 둘 수 hello 선택 나중 tooconfigure hello 에이전트 사용 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="fd282-163">On hello Agent Setup Options page, you can choose tooconnect hello agent tooAzure Log Analytics (OMS), Operations Manager, or you can leave hello choices blank if you want tooconfigure hello agent later.</span></span> <span data-ttu-id="fd282-164">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-164">Click **Next**.</span></span>   
    - <span data-ttu-id="fd282-165">Tooconnect tooAzure 로그 분석 (OMS)을 선택한 경우 붙여 hello **작업 영역 ID** 및 **작업 영역 키 (기본 키)** hello 이전 절차에서 메모장에 복사 하 고 클릭  **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-165">If you chose tooconnect tooAzure Log Analytics (OMS), paste hello **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in hello previous procedure and then click **Next**.</span></span>  
        <span data-ttu-id="fd282-166">![작업 영역 ID 및 기본 키 붙여넣기](./media/log-analytics-windows-agents/connect-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="fd282-166">![paste Workspace ID and Primary Key](./media/log-analytics-windows-agents/connect-workspace.png)</span></span>
    - <span data-ttu-id="fd282-167">Tooconnect tooOperations 관리자를 선택한 경우 입력 hello **관리 그룹 이름**, **관리 서버** 이름 및 **관리 서버 포트**, 클릭하고**다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-167">If you chose tooconnect tooOperations Manager, type hello **Management Group Name**, **Management Server** name, and **Management Server Port**, and then click **Next**.</span></span> <span data-ttu-id="fd282-168">Hello 에이전트 작업 계정 페이지에서 hello 로컬 시스템 계정 또는 로컬 도메인 계정을 선택 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-168">On hello Agent Action Account page, choose either hello Local System account or a local domain account and then click **Next**.</span></span>  
        <span data-ttu-id="fd282-169">![관리 그룹 구성](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![에이전트 작업 계정](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span><span class="sxs-lookup"><span data-stu-id="fd282-169">![management group configuration](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![agent action account](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span></span>

6. <span data-ttu-id="fd282-170">Hello 준비 tooInstall 페이지에서 선택 사항을 확인 한 다음 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-170">On hello Ready tooInstall page, review your choices and then click **Install**.</span></span>
7. <span data-ttu-id="fd282-171">페이지에 구성이 성공적으로 완료 하는 hello **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-171">On hello Configuration completed successfully page, click **Finish**.</span></span>
8. <span data-ttu-id="fd282-172">완료 되 면 hello **Microsoft Monitoring Agent** 에 표시 **제어판**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-172">When complete, hello **Microsoft Monitoring Agent** appears in **Control Panel**.</span></span> <span data-ttu-id="fd282-173">구성에 검토 하 고 hello 에이전트에 연결 된 tooOperational Insights (OMS)은 확인 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-173">You can review your configuration there and verify that hello agent is connected tooOperational Insights (OMS).</span></span> <span data-ttu-id="fd282-174">연결 된 tooOMS hello 에이전트 라는 메시지 표시: **hello Microsoft Monitoring Agent toohello Microsoft Operations Management Suite 서비스를 성공적으로 연결 합니다.**</span><span class="sxs-lookup"><span data-stu-id="fd282-174">When connected tooOMS, hello agent displays a message stating: **hello Microsoft Monitoring Agent has successfully connected toohello Microsoft Operations Management Suite service.**</span></span>

## <a name="configure-proxy-settings"></a><span data-ttu-id="fd282-175">프록시 설정 구성</span><span class="sxs-lookup"><span data-stu-id="fd282-175">Configure proxy settings</span></span>

<span data-ttu-id="fd282-176">Microsoft Monitoring Agent 제어판을 사용 하 여 hello에 대 한 프로시저 tooconfigure 프록시 설정을 다음 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-176">You can use hello following procedure tooconfigure proxy settings for hello Microsoft Monitoring Agent using Control Panel.</span></span> <span data-ttu-id="fd282-177">각 서버 toouse이이 프로시저가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-177">You need toouse this procedure for each server.</span></span> <span data-ttu-id="fd282-178">Tooconfigure 해야 하는 많은 서버를 설정한 경우 알게 될 것 보다 쉽게 toouse 스크립트 tooautomate이이 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-178">If you have many servers that you need tooconfigure, you might find it easier toouse a script tooautomate this process.</span></span> <span data-ttu-id="fd282-179">이 경우 hello 다음 절차를 참조 하십시오. [hello 스크립트를 사용 하 여 Microsoft 모니터링 에이전트에 대 한 프록시 설정을 tooconfigure](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script)합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-179">If so, see hello next procedure [tooconfigure proxy settings for hello Microsoft Monitoring Agent using a script](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span></span>

### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-control-panel"></a><span data-ttu-id="fd282-180">Microsoft Monitoring Agent 제어판을 사용 하 여 hello에 대 한 프록시 설정을 tooconfigure</span><span class="sxs-lookup"><span data-stu-id="fd282-180">tooconfigure proxy settings for hello Microsoft Monitoring Agent using Control Panel</span></span>
1. <span data-ttu-id="fd282-181">**제어판**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-181">Open **Control Panel**.</span></span>
2. <span data-ttu-id="fd282-182">**Microsoft Monitoring Agent**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-182">Open **Microsoft Monitoring Agent**.</span></span>
3. <span data-ttu-id="fd282-183">Hello 클릭 **프록시 설정을** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-183">Click hello **Proxy Settings** tab.</span></span>  
    <span data-ttu-id="fd282-184">![프록시 설정 탭](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span><span class="sxs-lookup"><span data-stu-id="fd282-184">![proxy settings tab](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span></span>
4. <span data-ttu-id="fd282-185">선택 **프록시 서버를 사용 하 여** hello URL을 입력 하 고 필요한 마찬가지로 toohello 표시 된 예의 경우 포트 번호를 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-185">Select **Use a proxy server** and type hello URL and port number, if one is needed, similar toohello example shown.</span></span> <span data-ttu-id="fd282-186">프록시 서버에 인증이 필요한 경우 hello 사용자 이름 및 암호 tooaccess hello 프록시 서버를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-186">If your proxy server requires authentication, type hello username and password tooaccess hello proxy server.</span></span>


### <a name="verify-agent-connectivity-toooms"></a><span data-ttu-id="fd282-187">에이전트 연결 tooOMS 확인</span><span class="sxs-lookup"><span data-stu-id="fd282-187">Verify agent connectivity tooOMS</span></span>

<span data-ttu-id="fd282-188">에이전트 절차를 수행 하는 hello를 사용 하 여 OMS와 통신 하 고 있는지 여부를 쉽게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-188">You can easily verify whether your agents are communicating with OMS using hello following procedure:</span></span>

1.  <span data-ttu-id="fd282-189">Windows 에이전트 hello와 hello 컴퓨터에서 제어판을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-189">On hello computer with hello Windows agent, open Control Panel.</span></span>
2.  <span data-ttu-id="fd282-190">Microsoft Monitoring Agent를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-190">Open Microsoft Monitoring Agent.</span></span>
3.  <span data-ttu-id="fd282-191">Hello Azure 로그 분석 (OMS) 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-191">Click hello Azure Log Analytics (OMS) tab.</span></span>
4.  <span data-ttu-id="fd282-192">Hello 상태 열에 해당 hello 에이전트 연결 toohello Operations Management Suite 서비스 성공적으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-192">In hello Status column, you should see that hello agent connected successfully toohello Operations Management Suite service.</span></span>

![연결된 에이전트](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-a-script"></a><span data-ttu-id="fd282-194">Microsoft Monitoring Agent는 스크립트를 사용 하 여 hello에 대 한 프록시 설정을 tooconfigure</span><span class="sxs-lookup"><span data-stu-id="fd282-194">tooconfigure proxy settings for hello Microsoft Monitoring Agent using a script</span></span>
<span data-ttu-id="fd282-195">다음 샘플, 특정 tooyour 환경 정보로 업데이트 하 고, PS1 파일 이름 확장명으로 저장 및 toohello OMS 서비스에 직접 연결 하는 각 컴퓨터에이 hello 스크립트를 실행 하는 hello를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-195">Copy hello following sample, update it with information specific tooyour environment, save it with a PS1 file name extension, and then run hello script on each computer that connects directly toohello OMS service.</span></span>

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get hello Health Service configuration object.  We need toodetermine if we
    #have hello right update rollup with hello API we need.  If not, no need toorun hello rest of hello script.
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

    Write-Output "Setting proxy too$ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-hello-agent-using-hello-command-line"></a><span data-ttu-id="fd282-196">Hello 명령줄을 사용 하는 hello 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="fd282-196">Install hello agent using hello command line</span></span>
- <span data-ttu-id="fd282-197">수정 하 고 다음 명령줄 hello를 사용 하 여 예제 tooinstall hello 에이전트 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-197">Modify and then use hello following example tooinstall hello agent using hello command line.</span></span> <span data-ttu-id="fd282-198">hello 예제는 완전 자동 설치를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-198">hello example performs a fully silent installation.</span></span>

    >[!NOTE]
    <span data-ttu-id="fd282-199">에이전트 tooupgrade 원하는 해야 toouse hello 로그 분석 API를 스크립팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-199">If you want tooupgrade an agent, you need toouse hello Log Analytics scripting API.</span></span> <span data-ttu-id="fd282-200">Hello 다음 섹션 tooupgrade 에이전트를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="fd282-200">See hello next section tooupgrade an agent.</span></span>

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

<span data-ttu-id="fd282-201">hello 에이전트도의 자동 압축 풀기 IExpress를 사용 하 여 hello를 사용 하 여 `/c` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-201">hello agent uses IExpress as its self-extractor using hello `/c` command.</span></span> <span data-ttu-id="fd282-202">Hello 명령줄 스위치에서 볼 수 있습니다 [IExpress에 대 한 명령줄 스위치](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) 다음 업데이트 hello 예제 toosuit 필요 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-202">You can see hello command-line switches at [Command-line switches for IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) and then update hello example toosuit your needs.</span></span>

|<span data-ttu-id="fd282-203">MMA 관련 옵션</span><span class="sxs-lookup"><span data-stu-id="fd282-203">MMA-specific options</span></span>                   |<span data-ttu-id="fd282-204">참고 사항</span><span class="sxs-lookup"><span data-stu-id="fd282-204">Notes</span></span>         |
|---------------------------------------|--------------|
|<span data-ttu-id="fd282-205">ADD_OPINSIGHTS_WORKSPACE</span><span class="sxs-lookup"><span data-stu-id="fd282-205">ADD_OPINSIGHTS_WORKSPACE</span></span>               | <span data-ttu-id="fd282-206">1 = 구성 hello 에이전트 tooreport tooa 작업 영역</span><span class="sxs-lookup"><span data-stu-id="fd282-206">1 = Configure hello agent tooreport tooa workspace</span></span>                |
|<span data-ttu-id="fd282-207">OPINSIGHTS_WORKSPACE_ID</span><span class="sxs-lookup"><span data-stu-id="fd282-207">OPINSIGHTS_WORKSPACE_ID</span></span>                | <span data-ttu-id="fd282-208">작업 영역 tooadd hello에 대 한 작업 영역 Id (guid)</span><span class="sxs-lookup"><span data-stu-id="fd282-208">Workspace Id (guid) for hello workspace tooadd</span></span>                    |
|<span data-ttu-id="fd282-209">OPINSIGHTS_WORKSPACE_KEY</span><span class="sxs-lookup"><span data-stu-id="fd282-209">OPINSIGHTS_WORKSPACE_KEY</span></span>               | <span data-ttu-id="fd282-210">작업 영역 키 사용 되는 tooinitially hello 작업 영역을 사용 하 여 인증</span><span class="sxs-lookup"><span data-stu-id="fd282-210">Workspace key used tooinitially authenticate with hello workspace</span></span> |
|<span data-ttu-id="fd282-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span><span class="sxs-lookup"><span data-stu-id="fd282-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span></span>  | <span data-ttu-id="fd282-212">작업 영역 hello 위치한 hello 클라우드 환경 지정</span><span class="sxs-lookup"><span data-stu-id="fd282-212">Specify hello cloud environment where hello workspace is located</span></span> <br> <span data-ttu-id="fd282-213">0 = Azure 상용 클라우드(기본값)</span><span class="sxs-lookup"><span data-stu-id="fd282-213">0 = Azure commercial cloud (default)</span></span> <br> <span data-ttu-id="fd282-214">1 = Azure Government</span><span class="sxs-lookup"><span data-stu-id="fd282-214">1 = Azure Government</span></span> |
|<span data-ttu-id="fd282-215">OPINSIGHTS_PROXY_URL</span><span class="sxs-lookup"><span data-stu-id="fd282-215">OPINSIGHTS_PROXY_URL</span></span>               | <span data-ttu-id="fd282-216">프록시 toouse hello에 대 한 URI</span><span class="sxs-lookup"><span data-stu-id="fd282-216">URI for hello proxy toouse</span></span> |
|<span data-ttu-id="fd282-217">OPINSIGHTS_PROXY_USERNAME</span><span class="sxs-lookup"><span data-stu-id="fd282-217">OPINSIGHTS_PROXY_USERNAME</span></span>               | <span data-ttu-id="fd282-218">사용자 이름 tooaccess 인증 된 프록시</span><span class="sxs-lookup"><span data-stu-id="fd282-218">Username tooaccess an authenticated proxy</span></span> |
|<span data-ttu-id="fd282-219">OPINSIGHTS_PROXY_PASSWORD</span><span class="sxs-lookup"><span data-stu-id="fd282-219">OPINSIGHTS_PROXY_PASSWORD</span></span>               | <span data-ttu-id="fd282-220">암호 tooaccess 인증 된 프록시</span><span class="sxs-lookup"><span data-stu-id="fd282-220">Password tooaccess an authenticated proxy</span></span> |

>[!NOTE]
<span data-ttu-id="fd282-221">IExpress의 tooavoid 적중 hello 명령줄 길이 제한을 구성 하는 작업 영역이 없는 hello 에이전트를 설치 하 고 hello 작업 영역에 대 한 스크립트 tooset 구성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-221">tooavoid hitting hello command-line length limit of IExpress, install hello agent with no workspace configured and then use a script tooset configuration for hello workspace.</span></span>

>[!NOTE]
<span data-ttu-id="fd282-222">발생 하는 경우는 `Command line option syntax error.` hello를 사용 하는 경우 `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` 매개 변수를 hello 해결 방법은 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-222">If you get a `Command line option syntax error.` when using hello `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parameter, you can use hello following workaround:</span></span>
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a><span data-ttu-id="fd282-223">스크립트를 사용하여 작업 영역 추가</span><span class="sxs-lookup"><span data-stu-id="fd282-223">Add a workspace using a script</span></span>
<span data-ttu-id="fd282-224">다음 예제는 hello로 hello 로그 분석 에이전트 스크립팅 API를 사용 하 여 작업 영역을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-224">Add a workspace using hello Log Analytics agent scripting API with hello following example:</span></span>

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

<span data-ttu-id="fd282-225">tooadd 미국 정부, 사용 하 여 hello 다음 스크립트 샘플에 대 한 Azure에서 작업 영역:</span><span class="sxs-lookup"><span data-stu-id="fd282-225">tooadd a workspace in Azure for US Government, use hello following script sample:</span></span>
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
<span data-ttu-id="fd282-226">Hello 명령줄 사용한 또는 tooinstall 스크립트 이전에 hello 에이전트를 구성 하거나 경우 `EnableAzureOperationalInsights` 로 바뀌었습니다. `AddCloudWorkspace`합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-226">If you've used hello command line or script previously tooinstall or configure hello agent, `EnableAzureOperationalInsights` was replaced by `AddCloudWorkspace`.</span></span>

## <a name="install-hello-agent-using-dsc-in-azure-automation"></a><span data-ttu-id="fd282-227">Azure 자동화에 DSC를 사용 하 여 hello 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="fd282-227">Install hello agent using DSC in Azure Automation</span></span>

<span data-ttu-id="fd282-228">다음 스크립트 예제 tooinstall hello 에이전트 Azure 자동화에 DSC를 사용 하 여 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-228">You can use hello following script example tooinstall hello agent using DSC in Azure Automation.</span></span> <span data-ttu-id="fd282-229">hello 예제 설치 hello hello로 식별 되는 64 비트 에이전트 `URI` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-229">hello example installs hello 64-bit agent, identified by hello `URI` value.</span></span> <span data-ttu-id="fd282-230">Hello URI 값을 대체 하 여 hello 32 비트 버전을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-230">You can also use hello 32-bit version by replacing hello URI value.</span></span> <span data-ttu-id="fd282-231">두 버전 모두에 대 한 Uri hello가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-231">hello URIs for both versions are:</span></span>

- <span data-ttu-id="fd282-232">Windows 64비트 에이전트 - https://go.microsoft.com/fwlink/?LinkId=828603</span><span class="sxs-lookup"><span data-stu-id="fd282-232">Windows 64-bit agent - https://go.microsoft.com/fwlink/?LinkId=828603</span></span>
- <span data-ttu-id="fd282-233">Windows 32비트 에이전트 - https://go.microsoft.com/fwlink/?LinkId=828604</span><span class="sxs-lookup"><span data-stu-id="fd282-233">Windows 32-bit agent - https://go.microsoft.com/fwlink/?LinkId=828604</span></span>


>[!NOTE]
<span data-ttu-id="fd282-234">이 절차 및 스크립트 예제는 기존 에이전트를 업그레이드하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-234">This procedure and script example will not upgrade an existing agent.</span></span>

1. <span data-ttu-id="fd282-235">Hello xPSDesiredStateConfiguration DSC 모듈을 가져올에서 [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) Azure 자동화로 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-235">Import hello xPSDesiredStateConfiguration DSC Module from [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) into Azure Automation.</span></span>  
2.  <span data-ttu-id="fd282-236">*OPSINSIGHTS_WS_ID* 및 *OPSINSIGHTS_WS_KEY*의 Azure Automation 변수 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-236">Create Azure Automation variable assets for *OPSINSIGHTS_WS_ID* and *OPSINSIGHTS_WS_KEY*.</span></span> <span data-ttu-id="fd282-237">설정 *OPSINSIGHTS_WS_ID* tooyour OMS 로그 분석 작업 영역 ID 설정 및 *OPSINSIGHTS_WS_KEY* toohello 작업 영역의 기본 키입니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-237">Set *OPSINSIGHTS_WS_ID* tooyour OMS Log Analytics workspace ID and set *OPSINSIGHTS_WS_KEY* toohello primary key of your workspace.</span></span>
3.  <span data-ttu-id="fd282-238">다음 스크립트를 MMAgent.ps1로 저장 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="fd282-238">Use hello following script and save it as MMAgent.ps1</span></span>
4.  <span data-ttu-id="fd282-239">수정 하 고 다음 Azure 자동화에 DSC를 사용 하 여 예제 tooinstall hello 에이전트 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-239">Modify and then use hello following example tooinstall hello agent using DSC in Azure Automation.</span></span> <span data-ttu-id="fd282-240">Hello Azure 자동화 인터페이스 또는 cmdlet을 사용 하 여 Azure 자동화로 MMAgent.ps1를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-240">Import MMAgent.ps1 into Azure Automation by using hello Azure Automation interface or cmdlet.</span></span>
5.  <span data-ttu-id="fd282-241">노드 toohello 구성을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-241">Assign a node toohello configuration.</span></span> <span data-ttu-id="fd282-242">15 분 이내 hello 노드 구성을 확인 하 고 hello MMA toohello 노드 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-242">Within 15 minutes, hello node checks its configuration and hello MMA is pushed toohello node.</span></span>

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

### <a name="get-hello-latest-productid-value"></a><span data-ttu-id="fd282-243">Hello 최신 ProductId 값 가져오기</span><span class="sxs-lookup"><span data-stu-id="fd282-243">Get hello latest ProductId value</span></span>

<span data-ttu-id="fd282-244">hello `ProductId value` hello MMAgent.ps1 스크립트는 고유 tooeach 에이전트 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-244">hello `ProductId value` in hello MMAgent.ps1 script is unique tooeach agent version.</span></span> <span data-ttu-id="fd282-245">각 에이전트의 업데이트 된 버전이 게시 되 면 hello ProductId 값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-245">When an updated version of each agent is published, hello ProductId value changes.</span></span> <span data-ttu-id="fd282-246">따라서 hello ProductId hello 나중에 변경 되 면 간단한 스크립트를 사용 하 여 hello 에이전트 버전을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-246">So, when hello ProductId changes in hello future, you can find hello agent version using a simple script.</span></span> <span data-ttu-id="fd282-247">테스트 서버에 설치 된 hello 최신 에이전트 버전을 설정한 후 다음 스크립트 tooget 설치 hello ProductId 값 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-247">After you have hello latest agent version installed on a test server, you can use hello following script tooget hello installed ProductId value.</span></span> <span data-ttu-id="fd282-248">Hello 최신 ProductId 값을 사용 하 여 hello MMAgent.ps1 스크립트의에서 hello 값을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-248">Using hello latest ProductId value, you can update hello value in hello MMAgent.ps1 script.</span></span>

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

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a><span data-ttu-id="fd282-249">에이전트를 수동으로 구성하거나 추가 작업 영역 추가</span><span class="sxs-lookup"><span data-stu-id="fd282-249">Configure an agent manually or add additional workspaces</span></span>
<span data-ttu-id="fd282-250">에이전트를 설치 했으면 했지만 구성 하지 않은 경우 또는 hello 에이전트 tooreport toomultiple 작업 영역을 정보 tooenable 에이전트 다음 hello를 사용 하 여 또는 다시 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-250">If you've installed agents but did not configure them or if you want hello agent tooreport toomultiple workspaces, you can use hello following information tooenable an agent or reconfigure it.</span></span> <span data-ttu-id="fd282-251">Hello 에이전트를 구성 하 고 나면 hello 에이전트 서비스로 등록 하 고 필요한 구성 정보를 가져오고 솔루션 정보를 포함 하는 관리 팩.</span><span class="sxs-lookup"><span data-stu-id="fd282-251">After you've configured hello agent, it will register with hello agent service and will get necessary configuration information and management packs that contain solution information.</span></span>

1. <span data-ttu-id="fd282-252">Hello Microsoft Monitoring Agent를 설치한 후에 열 **제어판**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-252">After you've installed hello Microsoft Monitoring Agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="fd282-253">열기 **Microsoft Monitoring Agent** hello를 클릭 한 다음 **Azure 로그 분석 (OMS)** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-253">Open **Microsoft Monitoring Agent** and then click hello **Azure Log Analytics (OMS)** tab.</span></span>   
3. <span data-ttu-id="fd282-254">클릭 **추가** tooopen hello **로그 분석 작업 영역 추가** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-254">Click **Add** tooopen hello **Add a Log Analytics Workspace** box.</span></span>
4. <span data-ttu-id="fd282-255">붙여넣기 hello **작업 영역 ID** 및 **작업 영역 키 (기본 키)** tooadd 원하고 클릭 hello 작업 영역에 대 한 이전 절차에서 메모장에 복사한 **확인**.</span><span class="sxs-lookup"><span data-stu-id="fd282-255">Paste hello **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in a previous procedure for hello workspace that you want tooadd and then click **OK**.</span></span>  
    <span data-ttu-id="fd282-256">![Operational Insights 구성](./media/log-analytics-windows-agents/add-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="fd282-256">![configure Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span></span>

<span data-ttu-id="fd282-257">Hello 에이전트에서 모니터링 하는 컴퓨터에서 데이터를 수집 하는 hello OMS에서 모니터링 하는 컴퓨터 수가 hello에 hello OMS 포털에 표시 됩니다 **연결 된 원본** 탭에서 **설정** 으로  **연결 된 서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-257">After data is collected from computers monitored by hello agent, hello number of computers monitored by OMS will appear in hello OMS portal on hello **Connected Sources** tab in **Settings** as **Servers Connected**.</span></span>


## <a name="toodisable-an-agent"></a><span data-ttu-id="fd282-258">toodisable 에이전트</span><span class="sxs-lookup"><span data-stu-id="fd282-258">toodisable an agent</span></span>
1. <span data-ttu-id="fd282-259">Hello 에이전트를 설치한 후 열려면 **제어판**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-259">After installing hello agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="fd282-260">Microsoft Monitoring Agent를 열고 클릭 다음 hello **Azure 로그 분석 (OMS)** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-260">Open Microsoft Monitoring Agent and then click hello **Azure Log Analytics (OMS)** tab.</span></span>
3. <span data-ttu-id="fd282-261">작업 영역을 선택하고 **제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-261">Select a workspace and then click **Remove**.</span></span> <span data-ttu-id="fd282-262">다른 모든 작업 영역에 대해 이 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-262">Repeat this step for all other workspaces.</span></span>


## <a name="optionally-configure-agents-tooreport-tooan-operations-manager-management-group"></a><span data-ttu-id="fd282-263">필요에 따라 에이전트 tooreport tooan Operations Manager 관리 그룹 구성</span><span class="sxs-lookup"><span data-stu-id="fd282-263">Optionally, configure agents tooreport tooan Operations Manager management group</span></span>

<span data-ttu-id="fd282-264">IT 인프라에서 Operations Manager를 사용 하는 경우 Operations Manager 에이전트도 hello MMA 에이전트를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-264">If you use Operations Manager in your IT infrastructure, you can also use hello MMA agent as an Operations Manager agent.</span></span>

### <a name="tooconfigure-mma-agents-tooreport-tooan-operations-manager-management-group"></a><span data-ttu-id="fd282-265">tooconfigure MMA 에이전트 tooreport tooan Operations Manager 관리 그룹</span><span class="sxs-lookup"><span data-stu-id="fd282-265">tooconfigure MMA agents tooreport tooan Operations Manager management group</span></span>
1.  <span data-ttu-id="fd282-266">Hello hello 에이전트가 설치 된 컴퓨터에서 엽니다 **제어판**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-266">On hello computer where hello agent is installed, open **Control Panel**.</span></span>  
2.  <span data-ttu-id="fd282-267">열기 **Microsoft Monitoring Agent** hello를 클릭 한 다음 **Operations Manager** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-267">Open **Microsoft Monitoring Agent** and then click hello **Operations Manager** tab.</span></span>  
    <span data-ttu-id="fd282-268">![Microsoft Monitoring Agent Operations Manager 탭](./media/log-analytics-windows-agents/om-mg01.png)</span><span class="sxs-lookup"><span data-stu-id="fd282-268">![Microsoft Monitoring Agent Operations Manager tab](./media/log-analytics-windows-agents/om-mg01.png)</span></span>
3.  <span data-ttu-id="fd282-269">Operations Manager 서버가 Active Directory와 통합된 경우 **AD DS에서 관리 그룹 할당 자동 업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-269">If your Operations Manager servers have integration with Active Directory, click **Automatically update management group assignments from AD DS**.</span></span>
4.  <span data-ttu-id="fd282-270">클릭 **추가** tooopen hello **관리 그룹 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="fd282-270">Click **Add** tooopen hello **Add a Management Group** dialog box.</span></span>  
    <span data-ttu-id="fd282-271">![Microsoft Monitoring Agent 관리 그룹 추가](./media/log-analytics-windows-agents/oms-mma-om02.png)</span><span class="sxs-lookup"><span data-stu-id="fd282-271">![Microsoft Monitoring Agent Add a Management Group](./media/log-analytics-windows-agents/oms-mma-om02.png)</span></span>
5.  <span data-ttu-id="fd282-272">**관리 그룹 이름** 상자 관리 그룹의 hello 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-272">In **Management group name** box, type hello name of your management group.</span></span>
6.  <span data-ttu-id="fd282-273">Hello에 **기본 관리 서버** 상자 hello hello 기본 관리 서버의 컴퓨터 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-273">In hello **Primary management server** box, type hello computer name of hello primary management server.</span></span>
7.  <span data-ttu-id="fd282-274">Hello에 **관리 서버 포트** 상자의 형식 hello TCP 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-274">In hello **Management server port** box, type hello TCP port number.</span></span>
8.  <span data-ttu-id="fd282-275">아래 **에이전트 작업 계정**, hello 로컬 시스템 계정 또는 로컬 도메인 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-275">Under **Agent Action Account**, choose either hello Local System account or a local domain account.</span></span>
9.  <span data-ttu-id="fd282-276">클릭 **확인** tooclose hello **관리 그룹 추가** 대화 상자를 클릭 한 다음 **확인** tooclose hello **Microsoft Monitoring Agent 속성**대화 상자.</span><span class="sxs-lookup"><span data-stu-id="fd282-276">Click **OK** tooclose hello **Add a Management Group** dialog box and then click **OK** tooclose hello **Microsoft Monitoring Agent Properties** dialog box.</span></span>


## <a name="next-steps"></a><span data-ttu-id="fd282-277">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fd282-277">Next steps</span></span>

- <span data-ttu-id="fd282-278">[로그 분석 솔루션 hello 솔루션 갤러리에서에서 추가](log-analytics-add-solutions.md) tooadd 기능 및 수집 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="fd282-278">[Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md) tooadd functionality and gather data.</span></span>
