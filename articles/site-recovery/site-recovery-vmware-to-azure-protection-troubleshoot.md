---
title: "aaaTroubleshoot 보호 실패/물리적 tooAzure | Microsoft Docs"
description: "이 문서에서는 hello 일반적인 VMware 컴퓨터 복제 오류를 설명 방법과 tootroubleshoot에"
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/26/2017
ms.author: asgang
ms.openlocfilehash: b821e9aa2610482ba1900645fb75e75744dc442f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-on-premises-vmwarephysical-server-replication-issues"></a><span data-ttu-id="1fac4-103">온-프레미스 VMware/물리적 서버 복제 문제 해결</span><span class="sxs-lookup"><span data-stu-id="1fac4-103">Troubleshoot on-premises VMware/Physical server replication issues</span></span>
<span data-ttu-id="1fac4-104">Azure Site Recovery를 사용하여 VMware 가상 컴퓨터 또는 물리적 서버를 보호하는 경우 특정 오류 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-104">You may receive a specific error message when protecting your VMware virtual machines or physical servers using Azure Site Recovery.</span></span> <span data-ttu-id="1fac4-105">이 문서 세부 정보 중 일부 hello 단계 tooresolve 문제 해결 발생 한 가지 일반적인 오류 메시지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-105">This article details some of hello more common error messages encountered, along with troubleshooting steps tooresolve them.</span></span>


## <a name="initial-replication-is-stuck-at-0"></a><span data-ttu-id="1fac4-106">초기 복제가 0%에 고정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-106">Initial replication is stuck at 0%</span></span>
<span data-ttu-id="1fac4-107">원본 프로세스 서버에 서버 또는 프로세스 Azure 서버 간의 tooconnectivity 문제 인해 소프트웨어는 대부분 지원에서 발생 하는 hello 초기 복제가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-107">Most of hello initial replication failures that we encounter at support are due tooconnectivity issues between source server-to-process server or process server-to-Azure.</span></span>
<span data-ttu-id="1fac4-108">대부분의 경우 할 수 있습니다 자체 아래에 나열 된 hello 단계에 따라 이러한 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-108">For most cases, you can self troubleshoot these issues by following hello steps listed below.</span></span>

###<a name="check-hello-following-on-source-machine"></a><span data-ttu-id="1fac4-109">원본 컴퓨터에서 hello 다음 확인</span><span class="sxs-lookup"><span data-stu-id="1fac4-109">Check hello following on SOURCE MACHINE</span></span>
* <span data-ttu-id="1fac4-110">원본 서버 컴퓨터 명령줄에서 네트워크 연결 문제 또는 방화벽 포트를 차단 문제 경우 toosee 아래 표시 된 대로 %https 포트 (기본값 9443)와 텔넷 tooping hello 프로세스 서버를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-110">From Source Server machine command line, use Telnet tooping hello Process Server with https port (default 9443) as shown below toosee if there are any network connectivity issues or firewall port blocking issues.</span></span>
     
    `telnet <PS IP address> <port>`
> [!NOTE]
    > <span data-ttu-id="1fac4-111">텔넷을 사용 하 여, PING tootest 연결 기능을 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="1fac4-111">Use Telnet, don’t use PING tootest connectivity.</span></span>  <span data-ttu-id="1fac4-112">텔넷이 설치 되지 않은 경우 hello 단계 목록에 따라 [여기](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="1fac4-112">If Telnet is not installed, follow hello steps list [here](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span></span>

<span data-ttu-id="1fac4-113">없습니다 tooconnect hello 프로세스 서버에서 인바운드 포트 9443 허용 하 고 경우 hello를 확인 하는 경우 문제가 여전히 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-113">If unable tooconnect, allow inbound port 9443 on hello Process Server and check if hello problem still exits.</span></span> <span data-ttu-id="1fac4-114">프로세스 서버가 DMZ 뒤에 있어서 이 문제를 일으켰던 경우도 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-114">There has been some cases where process server was behind DMZ, which was causing this problem.</span></span>

* <span data-ttu-id="1fac4-115">서비스의 hello 상태 확인 `InMage Scout VX Agent – Sentinel/OutpostStart` 없는 경우 실행 및 검사 hello 문제가 여전히 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-115">Check hello status of service `InMage Scout VX Agent – Sentinel/OutpostStart` if it is not running and check if hello problem still exists.</span></span>   
 
###<a name="check-hello-following-on-process-server"></a><span data-ttu-id="1fac4-116">프로세스 서버에서 다음 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-116">Check hello following on PROCESS SERVER</span></span>

* <span data-ttu-id="1fac4-117">**프로세스 서버 데이터 tooAzure 푸시합니다 적극적으로 하는 경우 확인**</span><span class="sxs-lookup"><span data-stu-id="1fac4-117">**Check if process server is actively pushing data tooAzure**</span></span> 

<span data-ttu-id="1fac4-118">프로세스 서버 컴퓨터에서 작업 관리자 (Ctrl-Shift-Esc 키를 눌러) hello를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-118">From Process Server machine, open hello Task Manager (press Ctrl-Shift-Esc ).</span></span> <span data-ttu-id="1fac4-119">Toohello 성능 탭으로 이동 하 고 ' 열기 리소스 모니터 ' 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-119">Go toohello Performance tab and click ‘Open Resource Monitor’ link.</span></span> <span data-ttu-id="1fac4-120">리소스 관리자에서 tooNetwork 탭으로 이동 합니다. '네트워크 작업을 사용하여 프로세스'의 cbengine.exe가 적극적으로 대량의(단위: Mb) 데이터를 보내는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-120">From Resource Manager, go tooNetwork tab. Check if cbengine.exe in ‘Processes with Network Activity’ is actively sending large volume (in Mbs) of data.</span></span>

![복제 활성화](./media/site-recovery-protection-common-errors/cbengine.png)

<span data-ttu-id="1fac4-122">그렇지 않으면 아래에 나열 된 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-122">If not follow hello steps listed below:</span></span>

* <span data-ttu-id="1fac4-123">**프로세스 서버 수 tooconnect Azure Blob 인지 확인**: 선택 하 고 있는지 확인 하십시오. cbengine.exe tooview hello ' TCP 연결 ' toosee 프로세스 서버 tooAzure 저장소 blob URL 연결 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-123">**Check if Process server is able tooconnect Azure Blob**: Select and check cbengine.exe tooview hello ‘TCP Connections’ toosee if there is connectivity from Process server tooAzure Storage blob URL.</span></span>

![복제 활성화](./media/site-recovery-protection-common-errors/rmonitor.png)

<span data-ttu-id="1fac4-125">다음 tooControl 패널을 이동 하지 않은 경우 > 서비스, 다음 서비스는 hello 실행 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-125">If not then go tooControl Panel > Services, check if hello following services are up and running:</span></span>

     * cxprocessserver
     * InMage Scout VX Agent – Sentinel/Outpost
     * Microsoft Azure Recovery Services Agent
     * Microsoft Azure Site Recovery Service
     * tmansvc
     * 
<span data-ttu-id="1fac4-126">(다시) 실행 중인 모든 서비스를 시작 하 고 hello 문제가 아직 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-126">(Re)Start any service which is not running and check if hello problem still exists.</span></span>

* <span data-ttu-id="1fac4-127">**프로세스 서버 포트 443을 사용 하 여 수 tooconnect tooAzure 공용 IP 주소 인지 확인**</span><span class="sxs-lookup"><span data-stu-id="1fac4-127">**Check if Process server is able tooconnect tooAzure Public IP address using port 443**</span></span>

<span data-ttu-id="1fac4-128">열기에서 최신 CBEngineCurr.errlog hello `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` 검색: 443 및 연결 시도가 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-128">Open hello latest CBEngineCurr.errlog from `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` and search for :443  and connection attempt failed.</span></span>

![복제 활성화](./media/site-recovery-protection-common-errors/logdetails1.png)

<span data-ttu-id="1fac4-130">문제가 있는 경우 다음 명령줄 프로세스 서버에서에서 사용 하 여 텔넷 tooping Azure 공용 IP 주소 (이미지 위에 마스크 된) hello CBEngineCurr.currLog에 포트 443을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-130">If there are issues, then from Process Server command line, use telnet tooping your Azure Public IP address (masked in above image) found in hello CBEngineCurr.currLog using port 443.</span></span>

      telnet <your Azure Public IP address as seen in CBEngineCurr.errlog>  443
<span data-ttu-id="1fac4-131">없습니다 tooconnect 인 경우 다음 단계에 설명 된 대로 프록시 toofirewall 기한 hello 액세스 문제가 발생 한 경우를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-131">If you are unable tooconnect, then check if hello access issue is due toofirewall or Proxy as described in next step.</span></span>


* <span data-ttu-id="1fac4-132">**프로세스 서버에서 IP 주소를 기준으로 방화벽 액세스를 차단 하지는 경우 확인**: hello 서버의 IP 주소를 기준으로 방화벽 규칙을 사용 하는 경우 다음 Microsoft Azure 데이터 센터 IP 범위에서 전체 목록은 hello 다운로드 [여기 ](https://www.microsoft.com/download/details.aspx?id=41653) 추가할 tooyour 방화벽 구성 tooensure 통신 tooAzure (및 HTTPS (443) 포트 hello)를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-132">**Check if IP address-based firewall on Process server are not blocking access**: If you are using an IP address-based firewall rules on hello server, then download hello complete list of Microsoft Azure Datacenter IP Ranges from [here](https://www.microsoft.com/download/details.aspx?id=41653) and add them tooyour firewall configuration tooensure they allow communication tooAzure (and hello HTTPS (443) port).</span></span>  <span data-ttu-id="1fac4-133">West US (액세스 제어 및 Id 관리에 사용) 및 hello 구독의 Azure 지역에 대 한 IP 주소 범위를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-133">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

* <span data-ttu-id="1fac4-134">**URL 기반 방화벽 프로세스 서버에서 액세스 하는 경우 차단 하지 않는지 확인**: hello 서버의 URL 기반 방화벽 규칙을 사용 하는 경우 다음 Url hello에 toofirewall 구성 추가 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-134">**Check if URL-based firewall on Process server is not blocking access**:  If you are using a URL based firewall rules on hello server, ensure hello following URLs are added toofirewall configuration.</span></span> 
     
  <span data-ttu-id="1fac4-135">`*.accesscontrol.windows.net:` - Access Control 및 Identity Management에 사용됨</span><span class="sxs-lookup"><span data-stu-id="1fac4-135">`*.accesscontrol.windows.net:` Used for access control and identity management</span></span>

  <span data-ttu-id="1fac4-136">`*.backup.windowsazure.com:` - 복제 데이터 전송 및 오케스트레이션에 사용됨</span><span class="sxs-lookup"><span data-stu-id="1fac4-136">`*.backup.windowsazure.com:` Used for replication data transfer and orchestration</span></span>

  <span data-ttu-id="1fac4-137">`*.blob.core.windows.net:`액세스 toohello에 사용 되는 저장소 계정을 저장 하는 복제 된 데이터</span><span class="sxs-lookup"><span data-stu-id="1fac4-137">`*.blob.core.windows.net:` Used for access toohello storage account that stores replicated data</span></span>

  <span data-ttu-id="1fac4-138">`*.hypervrecoverymanager.windowsazure.com:` - 복제 관리 작업 및 오케스트레이션에 사용됨</span><span class="sxs-lookup"><span data-stu-id="1fac4-138">`*.hypervrecoverymanager.windowsazure.com:` Used for replication management operations and orchestration</span></span>

  <span data-ttu-id="1fac4-139">`time.nist.gov`및 `time.windows.com`: 시스템 및 전역 시간 간의 toocheck 시간 동기화를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-139">`time.nist.gov` and `time.windows.com`: Used toocheck time synchronization between system and global time.</span></span>

<span data-ttu-id="1fac4-140">**Azure Government 클라우드**의 URL:</span><span class="sxs-lookup"><span data-stu-id="1fac4-140">URLs for **Azure Government Cloud**:</span></span>

`* .ugv.hypervrecoverymanager.windowsazure.us`

`* .ugv.backup.windowsazure.us`

`* .ugi.hypervrecoverymanager.windowsazure.us`

`* .ugi.backup.windowsazure.us` 

* <span data-ttu-id="1fac4-141">**프로세스 서버의 프록시 설정이 액세스를 차단하지 않는지 확인합니다**.</span><span class="sxs-lookup"><span data-stu-id="1fac4-141">**Check if Proxy Settings on Process server are not blocking access**.</span></span>  <span data-ttu-id="1fac4-142">프록시 서버를 사용 하는 경우 hello DNS 서버 확인 하는 hello 프록시 서버 이름을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-142">If you are using a Proxy Server, ensure hello proxy server name is resolving by hello DNS server.</span></span>
<span data-ttu-id="1fac4-143">toocheck hello 구성 서버 설치 시 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-143">toocheck what you have provided at hello time of Configuration Server setup.</span></span> <span data-ttu-id="1fac4-144">Go tooregistry 키</span><span class="sxs-lookup"><span data-stu-id="1fac4-144">Go tooregistry key</span></span>

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure Site Recovery\ProxySettings`

<span data-ttu-id="1fac4-145">이제 Azure Site Recovery 에이전트 toosend 데이터에서 동일한 설정을 사용 하는 해당 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-145">Now ensure that hello same settings are being used by Azure Site Recovery agent toosend data.</span></span>
<span data-ttu-id="1fac4-146">Microsoft Azure Backup 검색</span><span class="sxs-lookup"><span data-stu-id="1fac4-146">Search Microsoft Azure  Backup</span></span> 

![복제 활성화](./media/site-recovery-protection-common-errors/mab.png)

<span data-ttu-id="1fac4-148">해당 항목을 열고 작업 > 속성 변경을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-148">Open it and click on Action > Change Properties.</span></span> <span data-ttu-id="1fac4-149">프록시 구성 탭에서 hello 레지스트리 설정에 의해 표시 된 것 처럼 동일 해야 하는 hello 프록시 주소를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-149">Under Proxy Configuration tab, you should see hello proxy address, which should be same as shown by hello registry settings.</span></span> <span data-ttu-id="1fac4-150">그렇지 않은 경우 암호를 변경 하십시오 toohello 동일한 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-150">If not, please change it toohello same address.</span></span>

![복제 활성화](./media/site-recovery-protection-common-errors/mabproxy.png)

* <span data-ttu-id="1fac4-152">**스로틀 대역폭이 프로세스 서버에서 제한 되지 않은 확인**: hello 대역폭을 늘린 hello 문제가 여전히 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-152">**Check if Throttle bandwidth is not constrained on Process server**:  Increase hello bandwidth  and check if hello problem still exists.</span></span>

##<a name="next-steps"></a><span data-ttu-id="1fac4-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1fac4-153">Next steps</span></span>
<span data-ttu-id="1fac4-154">도움이 필요한 경우 그런 다음 게시할 쿼리 너무[ASR 포럼](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-154">If you need more help, then post your query too[ASR forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span></span> <span data-ttu-id="1fac4-155">커뮤니티 있고 수 tooassist 됩니다 엔지니어가 중 하나가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fac4-155">We have an active community and one of our engineers will be able tooassist you.</span></span>
