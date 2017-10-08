---
title: "aaaConnecting 보안 제품 toohello Operations Management Suite (OMS) 보안 및 감사 솔루션 | Microsoft Docs"
description: "이 문서는 관리 도구 모음 보안 및 감사 솔루션 일반적인 이벤트 형식을 사용 하 여 보안 제품 tooOperations tooconnect 있습니다를 수 있습니다."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 46eee484-e078-4bad-8c89-c88a3508f6aa
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 0f4b372d0379987c4e249628a3c8d52733be65c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-your-security-products-toohello-operations-management-suite-oms-security-and-audit-solution"></a><span data-ttu-id="57fc4-103">보안 제품 toohello Operations Management Suite (OMS) 보안 및 감사 솔루션에 연결</span><span class="sxs-lookup"><span data-stu-id="57fc4-103">Connecting your security products toohello Operations Management Suite (OMS) Security and Audit Solution</span></span> 
<span data-ttu-id="57fc4-104">이 문서를 사용 하면 보안 제품 hello OMS 보안 및 감사 솔루션에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57fc4-104">This document helps you connect your security products into hello OMS Security and Audit Solution.</span></span> <span data-ttu-id="57fc4-105">원본 hello 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57fc4-105">hello following sources are supported:</span></span>

- <span data-ttu-id="57fc4-106">CEF(일반 이벤트 형식) 이벤트</span><span class="sxs-lookup"><span data-stu-id="57fc4-106">Common Event Format (CEF) events</span></span>
- <span data-ttu-id="57fc4-107">Cisco ASA 이벤트</span><span class="sxs-lookup"><span data-stu-id="57fc4-107">Cisco ASA events</span></span>


## <a name="what-is-cef"></a><span data-ttu-id="57fc4-108">CEF란 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="57fc4-108">What is CEF?</span></span>
<span data-ttu-id="57fc4-109">공통 이벤트 형식 (CEF)는 많은 보안 공급 업체 tooallow 이벤트 간의 상호 운용성 서로 다른 플랫폼에서 사용 되는 Syslog 메시지를 기반으로 한 산업 표준 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="57fc4-109">Common Event Format (CEF) is an industry standard format on top of Syslog messages, used by many security vendors tooallow event interoperability among different platforms.</span></span> <span data-ttu-id="57fc4-110">OMS 보안 및 감사 솔루션 OMS 보안이 포함 된 보안 제품 CEF tooconnect 있습니다를 사용 하 여 데이터 수집을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="57fc4-110">OMS Security and Audit Solution support data ingestion using CEF, which enables you tooconnect your security products with OMS Security.</span></span> 

<span data-ttu-id="57fc4-111">데이터 원본 tooOMS를 연결 하 여이 플랫폼의 일부인 기능을 수행 하는 hello 수 tootake 활용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57fc4-111">By connecting your data source tooOMS, you are able tootake advantage of hello following capabilities that are part of this platform:</span></span>

- <span data-ttu-id="57fc4-112">검색 및 상관 관계</span><span class="sxs-lookup"><span data-stu-id="57fc4-112">Search & Correlation</span></span>
- <span data-ttu-id="57fc4-113">감사</span><span class="sxs-lookup"><span data-stu-id="57fc4-113">Auditing</span></span>
- <span data-ttu-id="57fc4-114">경고</span><span class="sxs-lookup"><span data-stu-id="57fc4-114">Alert</span></span>
- <span data-ttu-id="57fc4-115">위협 인텔리전스</span><span class="sxs-lookup"><span data-stu-id="57fc4-115">Threat Intelligence</span></span>
- <span data-ttu-id="57fc4-116">주목할 만한 문제</span><span class="sxs-lookup"><span data-stu-id="57fc4-116">Notable Issues</span></span>

## <a name="collection-of-security-solution-logs"></a><span data-ttu-id="57fc4-117">보안 솔루션 로그 수집</span><span class="sxs-lookup"><span data-stu-id="57fc4-117">Collection of security solution logs</span></span>

<span data-ttu-id="57fc4-118">OMS 보안은 Syslogs 및 [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/) 로그에 CEF를 사용하는 로그의 컬렉션을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="57fc4-118">OMS Security supports collection of logs using CEF over Syslogs and [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/) logs.</span></span> <span data-ttu-id="57fc4-119">이 예제에서는 hello 소스 (hello 로그를 생성 하는 컴퓨터) ng syslog 디먼을 실행 하는 Linux 컴퓨터 이며 hello 대상이 OMS 보안.</span><span class="sxs-lookup"><span data-stu-id="57fc4-119">In this example, hello source (computer that generates hello logs) is a Linux computer running syslog-ng daemon and hello target is OMS Security.</span></span> <span data-ttu-id="57fc4-120">작업을 tooprepare hello Linux 컴퓨터 tooperform hello를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57fc4-120">tooprepare hello Linux computer you will need tooperform hello following tasks:</span></span>

- <span data-ttu-id="57fc4-121">이상 버전 1.2.0-25 Linux 용 OMS 에이전트 hello를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="57fc4-121">Download hello OMS Agent for Linux, version 1.2.0-25 or above.</span></span>
- <span data-ttu-id="57fc4-122">Hello 섹션에 따라 **빠른 설치 가이드** 에서 [이 여기서](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) tooinstall 및 온보드 hello 에이전트 tooyour 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="57fc4-122">Follow hello section **Quick Install Guide** from [this article](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) tooinstall and onboard hello agent tooyour workspace.</span></span>

<span data-ttu-id="57fc4-123">일반적으로 hello 에이전트 hello hello 로그에서 생성 되는 다른 컴퓨터에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57fc4-123">Typically, hello agent is installed on a different computer from hello one on which hello logs are generated.</span></span> <span data-ttu-id="57fc4-124">전달 hello 로그 toohello 에이전트 컴퓨터는 단계를 수행 하는 hello를 일반적으로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="57fc4-124">Forwarding hello logs toohello agent machine will usually require hello following steps:</span></span>

- <span data-ttu-id="57fc4-125">제품/컴퓨터 tooforward hello 필요한 이벤트 toohello syslog 디먼 (예: rsyslog 또는 syslog-ng) 로깅 hello hello 에이전트 컴퓨터에서 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="57fc4-125">Configure hello logging product/machine tooforward hello required events toohello syslog daemon (rsyslog or syslog-ng) on hello agent machine.</span></span>
- <span data-ttu-id="57fc4-126">원격 시스템에서 hello 에이전트 컴퓨터 tooreceive 메시지에 syslog 디먼 hello를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="57fc4-126">Enable hello syslog daemon on hello agent machine tooreceive messages from a remote system.</span></span>

<span data-ttu-id="57fc4-127">Hello 에이전트 컴퓨터에서 hello 이벤트 hello syslog 디먼 toolocal UDP 포트 25226에서에서 보낸 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="57fc4-127">On hello agent machine, hello events need toobe sent from hello syslog daemon toolocal UDP port 25226.</span></span> <span data-ttu-id="57fc4-128">hello 에이전트는이 포트에서 들어오는 이벤트에 대 한 수신 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="57fc4-128">hello agent is listening for incoming events on this port.</span></span> <span data-ttu-id="57fc4-129">hello 다음은 구성 (수정 가능 hello 구성 toofit 로컬 설정) 하는 hello 로컬 시스템 toohello 에이전트에서 모든 이벤트를 전송에 대 한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="57fc4-129">hello following is an example configuration for sending all events from hello local system toohello agent (you can modify hello configuration toofit your local settings):</span></span>

1. <span data-ttu-id="57fc4-130">터미널 창 열기 hello 및 이동 toohello 디렉터리 */etc/syslog-ng /*</span><span class="sxs-lookup"><span data-stu-id="57fc4-130">Open hello terminal window, and go toohello directory */etc/syslog-ng/*</span></span> 
2. <span data-ttu-id="57fc4-131">새 파일을 만들 *보안-구성-omsagent.conf* hello 다음 콘텐츠를 추가 하 고: OMS_facility local4 =</span><span class="sxs-lookup"><span data-stu-id="57fc4-131">Create a new file *security-config-omsagent.conf* and add hello following content:  OMS_facility = local4</span></span>
    
    <span data-ttu-id="57fc4-132">filter f_local4_oms { facility(local4); };</span><span class="sxs-lookup"><span data-stu-id="57fc4-132">filter f_local4_oms { facility(local4); };</span></span>

    <span data-ttu-id="57fc4-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span><span class="sxs-lookup"><span data-stu-id="57fc4-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span></span>

    <span data-ttu-id="57fc4-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span><span class="sxs-lookup"><span data-stu-id="57fc4-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span></span>
    
3. <span data-ttu-id="57fc4-135">Hello 파일을 다운로드 *security_events.conf* 에 배치 하 고 */etc/opt/microsoft/omsagent/conf/omsagent.d/* hello OMS 에이전트 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57fc4-135">Download hello file *security_events.conf* and place at */etc/opt/microsoft/omsagent/conf/omsagent.d/* in hello OMS Agent computer.</span></span>
4. <span data-ttu-id="57fc4-136">Toorestart hello syslog 디먼 아래 hello 명령을 입력: *syslog ng 실행에 대 한:*</span><span class="sxs-lookup"><span data-stu-id="57fc4-136">Type hello command below toorestart hello syslog daemon:  *For syslog-ng run:*</span></span>
    
    ```
    sudo service rsyslog restart
    ```

    <span data-ttu-id="57fc4-137">*rsyslog를 실행하기 위해*</span><span class="sxs-lookup"><span data-stu-id="57fc4-137">*For rsyslog run:*</span></span>
    
    ```
    /etc/init.d/syslog-ng restart
    ```
5. <span data-ttu-id="57fc4-138">OMS 에이전트 toorestart hello 아래 hello 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="57fc4-138">Type hello command below toorestart hello OMS Agent:</span></span>

    <span data-ttu-id="57fc4-139">*rsyslog-ng를 실행하기 위해*</span><span class="sxs-lookup"><span data-stu-id="57fc4-139">*For syslog-ng run:*</span></span>
    
    ```
    sudo service omsagent restart
    ```

    <span data-ttu-id="57fc4-140">*rsyslog를 실행하기 위해*</span><span class="sxs-lookup"><span data-stu-id="57fc4-140">*For rsyslog run:*</span></span>
    
    ```
    systemctl restart omsagent
    ```
6. <span data-ttu-id="57fc4-141">아래 hello 명령을 입력 하 고 hello 결과 tooconfirm hello OMS 에이전트 로그에 오류가 있는지 검토 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="57fc4-141">Type hello command below and review hello result tooconfirm that there are no errors in hello OMS Agent log:</span></span>

    ``` 
    tail /var/opt/microsoft/omsagent/log/omsagent.log
    ```

## <a name="reviewing-collected-security-events"></a><span data-ttu-id="57fc4-142">수집된 보안 이벤트 검토</span><span class="sxs-lookup"><span data-stu-id="57fc4-142">Reviewing collected security events</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

<span data-ttu-id="57fc4-143">Hello 구성 끝난 후, OMS 보안에 의해 수집 된 toobe hello 보안 이벤트에 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57fc4-143">After hello configuration is over, hello security event will start toobe ingested by OMS Security.</span></span> <span data-ttu-id="57fc4-144">toovisualize hello 명령을 입력 하는 이벤트만 열기 hello 로그 검색 *유형 = CommonSecurityLog* 에 검색 필드 hello 하 고 ENTER 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="57fc4-144">toovisualize those events, open hello Log Search, type hello command *Type=CommonSecurityLog* in hello search field and press ENTER.</span></span> <span data-ttu-id="57fc4-145">hello 다음 예제에서는 결과 보여 줍니다 hello이 명령의이 경우 OMS 보안 이미 수집 된 여러 공급 업체에서 보안 로그를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="57fc4-145">hello following example shows hello result of this command, notice that in this case OMS Security already ingested security logs from multiple vendors:</span></span>
   
![OMS 보안 및 감사 기준 평가](./media/oms-security-connect-products/oms-security-connect-products-fig1.png)

<span data-ttu-id="57fc4-147">단일 공급 업체, 예를 들어 온라인 Cisco 로그 toovisualize, 형식에 대 한이 검색을 구체화할 수 있습니다: *형식 CommonSecurityLog DeviceVendor = Cisco =*합니다.</span><span class="sxs-lookup"><span data-stu-id="57fc4-147">You can refine this search for one single vendor, for example, toovisualize online Cisco logs, type: *Type=CommonSecurityLog DeviceVendor=Cisco*.</span></span> <span data-ttu-id="57fc4-148">"CommonSecurityLog" hello에 미리 정의 된 필드에 다른 확장 하는 동안 hello 기본 extensios 여부 등 "사용자 지정 확장 프로그램" or not CEF 헤더 "AdditionalExtensions" 필드에 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57fc4-148">hello “CommonSecurityLog” has predefined fields for any CEF header including hello basic extensios, while any other extension whether it’s “Custom Extension” or not, will be inserted into "AdditionalExtensions" field.</span></span> <span data-ttu-id="57fc4-149">여기에서 hello 기능 tooget 전용 필드를 사용자 지정 필드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57fc4-149">You can use hello Custom Fields feature tooget dedicated fields from it.</span></span> 

### <a name="accessing-computers-missing-baseline-assessment"></a><span data-ttu-id="57fc4-150">기준 평가가 누락된 컴퓨터에 액세스</span><span class="sxs-lookup"><span data-stu-id="57fc4-150">Accessing computers missing baseline assessment</span></span>
<span data-ttu-id="57fc4-151">OMS는 tooWindows Server 2012 r 2를 Windows Server 2008 r 2에서 hello 도메인 구성원 기본 프로필을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="57fc4-151">OMS supports hello domain member baseline profile on Windows Server 2008 R2 up tooWindows Server 2012 R2.</span></span> <span data-ttu-id="57fc4-152">Windows Server 2016 기준은 계획은 아직 최종본이 아니며 게시되는 즉시 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="57fc4-152">Windows Server 2016 baseline isn’t final yet and will be added as soon as it is published.</span></span> <span data-ttu-id="57fc4-153">OMS 보안 및 감사 초기 평가 통해 검색 된 다른 모든 운영 체제 hello 아래에 표시 **초기 평가 누락 된 컴퓨터** 섹션.</span><span class="sxs-lookup"><span data-stu-id="57fc4-153">All other operating systems scanned via OMS Security and Audit baseline assessment appear under hello **Computers missing baseline assessment** section.</span></span>

## <a name="see-also"></a><span data-ttu-id="57fc4-154">참고 항목</span><span class="sxs-lookup"><span data-stu-id="57fc4-154">See also</span></span>
<span data-ttu-id="57fc4-155">이 문서에서는 방법에 대해 배웠습니다 tooconnect CEF 솔루션 tooOMS 합니다.</span><span class="sxs-lookup"><span data-stu-id="57fc4-155">In this document, you learned how tooconnect your CEF solution tooOMS.</span></span> <span data-ttu-id="57fc4-156">OMS 보안에 대해 자세히 toolearn hello 다음 문서 참조:</span><span class="sxs-lookup"><span data-stu-id="57fc4-156">toolearn more about OMS Security, see hello following articles:</span></span>

* [<span data-ttu-id="57fc4-157">OMS(Operations Management Suite) 개요</span><span class="sxs-lookup"><span data-stu-id="57fc4-157">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="57fc4-158">모니터링 및 Operations Management Suite 보안 및 감사 솔루션에 응답 중 tooSecurity 경고</span><span class="sxs-lookup"><span data-stu-id="57fc4-158">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="57fc4-159">Operations Management Suite 보안 및 감사 솔루션의 리소스 모니터링</span><span class="sxs-lookup"><span data-stu-id="57fc4-159">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

