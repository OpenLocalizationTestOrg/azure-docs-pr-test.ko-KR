---
title: "Log Analytics의 VMware 모니터링 솔루션 | Microsoft Docs"
description: "VMware 모니터링 솔루션으로 로그를 관리하고 ESXi 호스트를 모니터링하는 방법을 알아봅니다."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 16516639-cc1e-465c-a22f-022f3be297f1
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.openlocfilehash: 17072c4b6e4fdf6e4dc2b7a6a4ded7fa9f9f6fde
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="vmware-monitoring-preview-solution-in-log-analytics"></a><span data-ttu-id="39613-103">Log Analytics의 VMware 모니터링(미리 보기) 솔루션</span><span class="sxs-lookup"><span data-stu-id="39613-103">VMware Monitoring (Preview) solution in Log Analytics</span></span>

![VMware 기호](./media/log-analytics-vmware/vmware-symbol.png)

<span data-ttu-id="39613-105">Log Analytics VMware 모니터링 솔루션은 대규모 VMware 로그에 적합한 중앙 집중식 로깅 및 모니터링 접근 방식을 만들 수 있는 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="39613-105">The VMware Monitoring solution in Log Analytics is a solution that helps you create a centralized logging and monitoring approach for large VMware logs.</span></span> <span data-ttu-id="39613-106">이 문서에서는 단일 위치에서 이 솔루션을 사용하여 ESXi 호스트의 문제를 해결, 캡처 및 관리하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-106">This article describes how you can troubleshoot, capture, and manage the ESXi hosts in a single location using the solution.</span></span> <span data-ttu-id="39613-107">솔루션을 사용하면 단일 위치에서 모든 ESXi 호스트에 대한 데이터를 자세히 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39613-107">With the solution, you can see detailed data for all your ESXi hosts in a single location.</span></span> <span data-ttu-id="39613-108">ESXi 호스트 로그를 통해 제공되는 상위 이벤트 수, 상태, VM 및 ESXi 호스트의 추세를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39613-108">You can see top event counts, status, and trends of VM and ESXi hosts provided through the ESXi host logs.</span></span> <span data-ttu-id="39613-109">중앙 집중식 ESXi 호스트 로그를 보고 검색하여 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39613-109">You can troubleshoot by viewing and searching centralized ESXi host logs.</span></span> <span data-ttu-id="39613-110">그리고 로그 검색 쿼리에 기반한 경고를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39613-110">And, you can create alerts based on log search queries.</span></span>

<span data-ttu-id="39613-111">이 솔루션은 ESXi 호스트의 기본 syslog 기능을 사용하여 OMS 에이전트가 있는 대상 VM에 데이터를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-111">The solution uses native syslog functionality of the ESXi host to push data to a target VM, which has OMS Agent.</span></span> <span data-ttu-id="39613-112">그러나 대상 VM 내의 syslog에 파일을 작성하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="39613-112">However, the solution doesn't write files into syslog within the target VM.</span></span> <span data-ttu-id="39613-113">OM 에이전트는 포트 1514를 열고 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-113">The OMS agent opens port 1514 and listens to this.</span></span> <span data-ttu-id="39613-114">데이터를 받으면 이를 OMS로 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-114">Once it receives the data, the OMS agent pushes the data into OMS.</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="39613-115">솔루션 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="39613-115">Installing and configuring the solution</span></span>
<span data-ttu-id="39613-116">다음 정보를 사용하여 솔루션을 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-116">Use the following information to install and configure the solution.</span></span>

* <span data-ttu-id="39613-117">[솔루션 갤러리에서 Log Analytics 솔루션 추가](log-analytics-add-solutions.md)에 설명된 절차를 통해 OMS 작업 영역에 VMware 모니터링 솔루션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-117">Add the VMware Monitoring solution to your OMS workspace using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>

#### <a name="supported-vmware-esxi-hosts"></a><span data-ttu-id="39613-118">지원되는 VMware ESXi 호스트</span><span class="sxs-lookup"><span data-stu-id="39613-118">Supported VMware ESXi hosts</span></span>
<span data-ttu-id="39613-119">vSphere ESXi 호스트 5.5 및 6.0</span><span class="sxs-lookup"><span data-stu-id="39613-119">vSphere ESXi Host 5.5 and 6.0</span></span>

#### <a name="prepare-a-linux-server"></a><span data-ttu-id="39613-120">Linux 서버 준비</span><span class="sxs-lookup"><span data-stu-id="39613-120">Prepare a Linux server</span></span>
<span data-ttu-id="39613-121">ESXi 호스트로부터 모든 syslog 데이터를 수신하는 Linux 운영 체제 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39613-121">Create a Linux operating system VM to receive all syslog data from the ESXi hosts.</span></span> <span data-ttu-id="39613-122">[OMS Linux 에이전트](log-analytics-linux-agents.md)는 모든 ESXi 호스트 syslog 데이터를 수집하는 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="39613-122">The [OMS Linux Agent](log-analytics-linux-agents.md) is the collection point for all ESXi host syslog data.</span></span> <span data-ttu-id="39613-123">아래 예에서 보여 주듯이 여러 ESXi 호스트에서 단일 Linux 서버로 로그를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39613-123">You can use multiple ESXi hosts to forward logs to a single Linux server, as in the following example.</span></span>  

   ![syslog 흐름](./media/log-analytics-vmware/diagram.png)

### <a name="configure-syslog-collection"></a><span data-ttu-id="39613-125">Syslog 수집 구성</span><span class="sxs-lookup"><span data-stu-id="39613-125">Configure syslog collection</span></span>
1. <span data-ttu-id="39613-126">vSphere에 syslog를 전달하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-126">Set up syslog forwarding for VSphere.</span></span> <span data-ttu-id="39613-127">Syslog 전달을 설정하는 데 도움이 되는 자세한 내용은 [Configuring syslog on ESXi 5.x and 6.0 (2003322)](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2003322)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39613-127">For detailed information to help set up syslog forwarding, see [Configuring syslog on ESXi 5.x and 6.0 (2003322)](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2003322).</span></span> <span data-ttu-id="39613-128">**ESXi 호스트 구성** > **소프트웨어** > **고급 설정** > **Syslog**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-128">Go to **ESXi Host Configuration** > **Software** > **Advanced Settings** > **Syslog**.</span></span>
   <span data-ttu-id="39613-129">![vsphereconfig](./media/log-analytics-vmware/vsphere1.png)</span><span class="sxs-lookup"><span data-stu-id="39613-129">![vsphereconfig](./media/log-analytics-vmware/vsphere1.png)</span></span>  
2. <span data-ttu-id="39613-130">*Syslog.global.logHost* 필드에서 Linux 서버 및 *1514* 포트 번호를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-130">In the *Syslog.global.logHost* field, add your Linux server and the port number *1514*.</span></span> <span data-ttu-id="39613-131">예를 들어 `tcp://hostname:1514` 또는 `tcp://123.456.789.101:1514`와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="39613-131">For example, `tcp://hostname:1514` or `tcp://123.456.789.101:1514`</span></span>
3. <span data-ttu-id="39613-132">Syslog의 ESXi 호스트 방화벽을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="39613-132">Open the ESXi host firewall for syslog.</span></span> <span data-ttu-id="39613-133">**ESXi 호스트 구성** > **소프트웨어** > **보안 프로필** > **방화벽**으로 이동한 다음 **속성**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="39613-133">**ESXi Host Configuration** > **Software** > **Security Profile** > **Firewall** and open **Properties**.</span></span>  

    ![vspherefw](./media/log-analytics-vmware/vsphere2.png)  

    ![vspherefwproperties](./media/log-analytics-vmware/vsphere3.png)  
4. <span data-ttu-id="39613-136">vSphere 콘솔에서 해당 syslog가 제대로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-136">Check the vSphere Console to verify that that syslog is properly set up.</span></span> <span data-ttu-id="39613-137">ESXi 호스트에서 포트가 **1514**로 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-137">Confirm on the ESXI host that port **1514** is configured.</span></span>
5. <span data-ttu-id="39613-138">Linux용 OMS 에이전트를 다운로드하여 Linux 서버에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-138">Download and install the OMS Agent for Linux on the Linux server.</span></span> <span data-ttu-id="39613-139">자세한 내용은 [Linux용 OMS 에이전트 설명서](https://github.com/Microsoft/OMS-Agent-for-Linux)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39613-139">For more information, see the [Documentation for OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux).</span></span>
6. <span data-ttu-id="39613-140">Linux용 OMS 에이전트를 설치한 후 /etc/opt/microsoft/omsagent/sysconf/omsagent.d 디렉터리로 이동하고, vmware_esxi.conf 파일을  /etc/opt/microsoft/omsagent/conf/omsagent.d 디렉터리에 복사한 다음 해당 파일의 소유자/그룹 및 사용 권한을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-140">After the OMS Agent for Linux is installed, go to the  /etc/opt/microsoft/omsagent/sysconf/omsagent.d directory and copy the vmware_esxi.conf file to the /etc/opt/microsoft/omsagent/conf/omsagent.d directory and the change the owner/group and permissions of the file.</span></span> <span data-ttu-id="39613-141">예:</span><span class="sxs-lookup"><span data-stu-id="39613-141">For example:</span></span>

    ```
    sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/vmware_esxi.conf /etc/opt/microsoft/omsagent/conf/omsagent.d
   sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf
    ```
7. <span data-ttu-id="39613-142">`sudo /opt/microsoft/omsagent/bin/service_control restart`를 실행하여 Linux용 OMS 에이전트를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-142">Restart the OMS Agent for Linux by running `sudo /opt/microsoft/omsagent/bin/service_control restart`.</span></span>
8. <span data-ttu-id="39613-143">ESXi 호스트에서 `nc` 명령을 사용하여 Linux 서버와 ESXi 호스트 간의 연결을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-143">Test the connectivity between the Linux server and the ESXi host by using the `nc` command on the ESXi Host.</span></span> <span data-ttu-id="39613-144">예:</span><span class="sxs-lookup"><span data-stu-id="39613-144">For example:</span></span>

    ```
    [root@ESXiHost:~] nc -z 123.456.789.101 1514
    Connection to 123.456.789.101 1514 port [tcp/*] succeeded!
    ```

9. <span data-ttu-id="39613-145">OMS 포털에서 `Type=VMware_CL` 로그 검색을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-145">In the OMS Portal, perform a log search for `Type=VMware_CL`.</span></span> <span data-ttu-id="39613-146">OMS에서 syslog 데이터를 수집할 때는 syslog 형식을 그대로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-146">When OMS collects the syslog data, it retains the syslog format.</span></span> <span data-ttu-id="39613-147">포털에서는 *Hostname* 및 *ProcessName*과 같은 일부 특정 필드가 캡처됩니다.</span><span class="sxs-lookup"><span data-stu-id="39613-147">In the portal, some specific fields are captured, such as *Hostname* and *ProcessName*.</span></span>  

    ![type](./media/log-analytics-vmware/type.png)  

    <span data-ttu-id="39613-149">로그 검색 결과 보기가 위 이미지와 비슷한 경우 OMS VMware 모니터링 솔루션 대시보드를 사용하도록 설정된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="39613-149">If your view log search results are similar to the image above, you're set to use the OMS VMware Monitoring solution dashboard.</span></span>  

## <a name="vmware-data-collection-details"></a><span data-ttu-id="39613-150">VMware 데이터 수집 세부 정보</span><span class="sxs-lookup"><span data-stu-id="39613-150">VMware data collection details</span></span>
<span data-ttu-id="39613-151">VMware 모니터링 솔루션에서는 사용 설정된 Linux용 OMS 에이전트를 통해 ESXi 호스트로부터 다양한 성능 메트릭과 로그 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-151">The VMware Monitoring solution collects various performance metrics and log data from ESXi hosts using the OMS Agents for Linux that you have enabled.</span></span>

<span data-ttu-id="39613-152">다음 테이블은 데이터 수집 방법 및 데이터가 수집되는 방식에 대한 기타 세부 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="39613-152">The following table shows data collection methods and other details about how data is collected.</span></span>

| <span data-ttu-id="39613-153">플랫폼</span><span class="sxs-lookup"><span data-stu-id="39613-153">platform</span></span> | <span data-ttu-id="39613-154">Linux 용 OMS 에이전트</span><span class="sxs-lookup"><span data-stu-id="39613-154">OMS Agent for Linux</span></span> | <span data-ttu-id="39613-155">SCOM 에이전트</span><span class="sxs-lookup"><span data-stu-id="39613-155">SCOM agent</span></span> | <span data-ttu-id="39613-156">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="39613-156">Azure Storage</span></span> | <span data-ttu-id="39613-157">SCOM 필요?</span><span class="sxs-lookup"><span data-stu-id="39613-157">SCOM required?</span></span> | <span data-ttu-id="39613-158">관리 그룹을 통해 전송되는 SCOM 에이전트 데이터</span><span class="sxs-lookup"><span data-stu-id="39613-158">SCOM agent data sent via management group</span></span> | <span data-ttu-id="39613-159">수집 빈도</span><span class="sxs-lookup"><span data-stu-id="39613-159">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="39613-160">Linux</span><span class="sxs-lookup"><span data-stu-id="39613-160">Linux</span></span> |<span data-ttu-id="39613-161">&#8226;</span><span class="sxs-lookup"><span data-stu-id="39613-161">&#8226;</span></span> |  |  |  |  |<span data-ttu-id="39613-162">매 3분</span><span class="sxs-lookup"><span data-stu-id="39613-162">every 3 minutes</span></span> |

<span data-ttu-id="39613-163">다음 표에서는 VMware 모니터링 솔루션에서 수집한 데이터 형식의 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="39613-163">The following table show examples of data fields collected by the VMware Monitoring solution:</span></span>

| <span data-ttu-id="39613-164">필드 이름</span><span class="sxs-lookup"><span data-stu-id="39613-164">field name</span></span> | <span data-ttu-id="39613-165">설명</span><span class="sxs-lookup"><span data-stu-id="39613-165">description</span></span> |
| --- | --- |
| <span data-ttu-id="39613-166">Device_s</span><span class="sxs-lookup"><span data-stu-id="39613-166">Device_s</span></span> |<span data-ttu-id="39613-167">VMware 저장소 장치</span><span class="sxs-lookup"><span data-stu-id="39613-167">VMware storage devices</span></span> |
| <span data-ttu-id="39613-168">ESXIFailure_s</span><span class="sxs-lookup"><span data-stu-id="39613-168">ESXIFailure_s</span></span> |<span data-ttu-id="39613-169">오류 유형</span><span class="sxs-lookup"><span data-stu-id="39613-169">failure types</span></span> |
| <span data-ttu-id="39613-170">EventTime_t</span><span class="sxs-lookup"><span data-stu-id="39613-170">EventTime_t</span></span> |<span data-ttu-id="39613-171">이벤트가 발생한 시간</span><span class="sxs-lookup"><span data-stu-id="39613-171">time when event occurred</span></span> |
| <span data-ttu-id="39613-172">HostName_s</span><span class="sxs-lookup"><span data-stu-id="39613-172">HostName_s</span></span> |<span data-ttu-id="39613-173">ESXi 호스트 이름</span><span class="sxs-lookup"><span data-stu-id="39613-173">ESXi host name</span></span> |
| <span data-ttu-id="39613-174">Operation_s</span><span class="sxs-lookup"><span data-stu-id="39613-174">Operation_s</span></span> |<span data-ttu-id="39613-175">VM 만들기 또는 삭제</span><span class="sxs-lookup"><span data-stu-id="39613-175">create VM or delete VM</span></span> |
| <span data-ttu-id="39613-176">ProcessName_s</span><span class="sxs-lookup"><span data-stu-id="39613-176">ProcessName_s</span></span> |<span data-ttu-id="39613-177">이벤트 이름</span><span class="sxs-lookup"><span data-stu-id="39613-177">event name</span></span> |
| <span data-ttu-id="39613-178">ResourceId_s</span><span class="sxs-lookup"><span data-stu-id="39613-178">ResourceId_s</span></span> |<span data-ttu-id="39613-179">VMware 호스트 이름</span><span class="sxs-lookup"><span data-stu-id="39613-179">name of the VMware host</span></span> |
| <span data-ttu-id="39613-180">ResourceLocation_s</span><span class="sxs-lookup"><span data-stu-id="39613-180">ResourceLocation_s</span></span> |<span data-ttu-id="39613-181">VMware</span><span class="sxs-lookup"><span data-stu-id="39613-181">VMware</span></span> |
| <span data-ttu-id="39613-182">ResourceName_s</span><span class="sxs-lookup"><span data-stu-id="39613-182">ResourceName_s</span></span> |<span data-ttu-id="39613-183">VMware</span><span class="sxs-lookup"><span data-stu-id="39613-183">VMware</span></span> |
| <span data-ttu-id="39613-184">ResourceType_s</span><span class="sxs-lookup"><span data-stu-id="39613-184">ResourceType_s</span></span> |<span data-ttu-id="39613-185">Hyper-V</span><span class="sxs-lookup"><span data-stu-id="39613-185">Hyper-V</span></span> |
| <span data-ttu-id="39613-186">SCSIStatus_s</span><span class="sxs-lookup"><span data-stu-id="39613-186">SCSIStatus_s</span></span> |<span data-ttu-id="39613-187">VMware SCSI 상태</span><span class="sxs-lookup"><span data-stu-id="39613-187">VMware SCSI status</span></span> |
| <span data-ttu-id="39613-188">SyslogMessage_s</span><span class="sxs-lookup"><span data-stu-id="39613-188">SyslogMessage_s</span></span> |<span data-ttu-id="39613-189">Syslog 데이터</span><span class="sxs-lookup"><span data-stu-id="39613-189">Syslog data</span></span> |
| <span data-ttu-id="39613-190">UserName_s</span><span class="sxs-lookup"><span data-stu-id="39613-190">UserName_s</span></span> |<span data-ttu-id="39613-191">VM을 만들거나 삭제한 사용자</span><span class="sxs-lookup"><span data-stu-id="39613-191">user who created or deleted VM</span></span> |
| <span data-ttu-id="39613-192">VMName_s</span><span class="sxs-lookup"><span data-stu-id="39613-192">VMName_s</span></span> |<span data-ttu-id="39613-193">VM 이름</span><span class="sxs-lookup"><span data-stu-id="39613-193">VM name</span></span> |
| <span data-ttu-id="39613-194">Computer</span><span class="sxs-lookup"><span data-stu-id="39613-194">Computer</span></span> |<span data-ttu-id="39613-195">호스트 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="39613-195">host computer</span></span> |
| <span data-ttu-id="39613-196">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="39613-196">TimeGenerated</span></span> |<span data-ttu-id="39613-197">데이터가 생성된 시간</span><span class="sxs-lookup"><span data-stu-id="39613-197">time the data was generated</span></span> |
| <span data-ttu-id="39613-198">DataCenter_s</span><span class="sxs-lookup"><span data-stu-id="39613-198">DataCenter_s</span></span> |<span data-ttu-id="39613-199">VMware 데이터 센터</span><span class="sxs-lookup"><span data-stu-id="39613-199">VMware datacenter</span></span> |
| <span data-ttu-id="39613-200">StorageLatency_s</span><span class="sxs-lookup"><span data-stu-id="39613-200">StorageLatency_s</span></span> |<span data-ttu-id="39613-201">저장소 대기 시간(밀리초)</span><span class="sxs-lookup"><span data-stu-id="39613-201">storage latency (ms)</span></span> |

## <a name="vmware-monitoring-solution-overview"></a><span data-ttu-id="39613-202">VMware 모니터링 솔루션 개요</span><span class="sxs-lookup"><span data-stu-id="39613-202">VMware Monitoring solution overview</span></span>
<span data-ttu-id="39613-203">OMS 포털에 표시되는 VMware 타일에서는</span><span class="sxs-lookup"><span data-stu-id="39613-203">The VMware tile appears in the OMS portal.</span></span> <span data-ttu-id="39613-204">발생한 모든 오류에 대한 상위 수준 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-204">It provides a high-level view of any failures.</span></span> <span data-ttu-id="39613-205">타일을 클릭하면 대시보드 보기로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-205">When you click the tile, you go into a dashboard view.</span></span>

![타일](./media/log-analytics-vmware/tile.png)

#### <a name="navigate-the-dashboard-view"></a><span data-ttu-id="39613-207">대시보드 보기 탐색</span><span class="sxs-lookup"><span data-stu-id="39613-207">Navigate the dashboard view</span></span>
<span data-ttu-id="39613-208">**VMware** 대시보드 보기에 구성되는 블레이드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="39613-208">In the **VMware** dashboard view, blades are organized by:</span></span>

* <span data-ttu-id="39613-209">오류 상태 수</span><span class="sxs-lookup"><span data-stu-id="39613-209">Failure Status Count</span></span>
* <span data-ttu-id="39613-210">이벤트 수 기준 상위 호스트</span><span class="sxs-lookup"><span data-stu-id="39613-210">Top Host by Event Counts</span></span>
* <span data-ttu-id="39613-211">상위 이벤트 수</span><span class="sxs-lookup"><span data-stu-id="39613-211">Top Event Counts</span></span>
* <span data-ttu-id="39613-212">가상 컴퓨터 활동</span><span class="sxs-lookup"><span data-stu-id="39613-212">Virtual Machine Activities</span></span>
* <span data-ttu-id="39613-213">ESXi 호스트 디스크 이벤트</span><span class="sxs-lookup"><span data-stu-id="39613-213">ESXi Host Disk Events</span></span>

![solution1](./media/log-analytics-vmware/solutionview1-1.png)

![solution2](./media/log-analytics-vmware/solutionview1-2.png)

<span data-ttu-id="39613-216">블레이드를 클릭하면 해당 블레이드의 특정 세부 정보를 보여 주는 Log Analytics 검색 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="39613-216">Click any blade to open Log Analytics search pane that shows detailed information specific for the blade.</span></span>

<span data-ttu-id="39613-217">여기서는 특정 항목을 위해 검색 쿼리를 수정하도록 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39613-217">From here, you can edit the search query to modify it for something specific.</span></span> <span data-ttu-id="39613-218">OMS 검색에 대한 기본적인 내용은 [OMS 로그 검색 자습서](log-analytics-log-searches.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39613-218">For a tutorial on the basics of OMS search, check out the [OMS log search tutorial.](log-analytics-log-searches.md)</span></span>

#### <a name="find-esxi-host-events"></a><span data-ttu-id="39613-219">ESXi 호스트 이벤트 찾기</span><span class="sxs-lookup"><span data-stu-id="39613-219">Find ESXi host events</span></span>
<span data-ttu-id="39613-220">단일 ESXi 호스트에서는 프로세스에 따라 여러 로그를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-220">A single ESXi host generates multiple logs, based on their processes.</span></span> <span data-ttu-id="39613-221">VMware 모니터링 솔루션은 이러한 로그를 중앙 집중식으로 관리하고 이벤트 수를 요약 합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-221">The VMware Monitoring solution centralizes them and summarizes the event counts.</span></span> <span data-ttu-id="39613-222">이처럼 중앙 집중화된 보기를 사용하면 대량의 이벤트가 발생한 ESXi 호스트 및 사용자 환경에서 가장 빈번하게 발생한 이벤트를 손쉽게 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39613-222">This centralized view helps you understand which ESXi host has a high volume of events and what events occur most frequently in your environment.</span></span>

![event](./media/log-analytics-vmware/events.png)

<span data-ttu-id="39613-224">ESXi 호스트 또는 이벤트 유형을 클릭하면 관련 정보를 자세히 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39613-224">You can drill further by clicking an ESXi host or an event type.</span></span>

<span data-ttu-id="39613-225">ESXi 호스트 이름을 클릭하여 해당 ESXi 호스트의 정보를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="39613-225">When you click an ESXi host name, you view information from that ESXi host.</span></span> <span data-ttu-id="39613-226">이벤트 유형으로 한정된 결과를 원하는 경우 검색 쿼리에 `“ProcessName_s=EVENT TYPE”`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-226">If you want to narrow results with the event type, add `“ProcessName_s=EVENT TYPE”` in your search query.</span></span> <span data-ttu-id="39613-227">검색 필터에서 **ProcessName**을 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39613-227">You can select **ProcessName** in the search filter.</span></span> <span data-ttu-id="39613-228">그러면 사용자가 원하는 정보로 맞추어집니다.</span><span class="sxs-lookup"><span data-stu-id="39613-228">That narrows the information for you.</span></span>

![연습](./media/log-analytics-vmware/eventhostdrilldown.png)

#### <a name="find-high-vm-activities"></a><span data-ttu-id="39613-230">빈번한 VM 활동 찾기</span><span class="sxs-lookup"><span data-stu-id="39613-230">Find high VM activities</span></span>
<span data-ttu-id="39613-231">ESXi 호스트마다 가상 컴퓨터를 만들고 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39613-231">A virtual machine can be created and deleted on any ESXi host.</span></span> <span data-ttu-id="39613-232">이렇게 하면 관리자가 ESXi 호스트에서 만드는 VM 수를 식별하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39613-232">It's helpful for an administrator to identify how many VMs an ESXi host creates.</span></span> <span data-ttu-id="39613-233">또한 성능과 용량 계획을 파악하는 데에도 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39613-233">That in-turn, helps to understand performance and capacity planning.</span></span> <span data-ttu-id="39613-234">사용자 환경을 관리할 때는 VM 활동 이벤트를 추적하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-234">Keeping track of VM activity events is crucial when managing your environment.</span></span>

![연습](./media/log-analytics-vmware/vmactivities1.png)

<span data-ttu-id="39613-236">또한 ESXi 호스트 VM 생성 데이터도 확인하려는 경우에는 ESXi 호스트 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-236">If you want to see additional ESXi host VM creation data, click an ESXi host name.</span></span>

![연습](./media/log-analytics-vmware/createvm.png)

#### <a name="common-search-queries"></a><span data-ttu-id="39613-238">일반적 검색 쿼리</span><span class="sxs-lookup"><span data-stu-id="39613-238">Common search queries</span></span>
<span data-ttu-id="39613-239">솔루션에는 대규모 저장소 공간, 저장소 대기 시간, 경로 오류 등 ESXi 호스트를 관리하는 데 유용한 쿼리들이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39613-239">The solution includes other useful queries that can help you manage your ESXi hosts, such as high storage space, storage latency, and path failure.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![쿼리](./media/log-analytics-vmware/queries.png)


#### <a name="save-queries"></a><span data-ttu-id="39613-241">쿼리 저장</span><span class="sxs-lookup"><span data-stu-id="39613-241">Save queries</span></span>
<span data-ttu-id="39613-242">OMS 표준 기능인 검색 쿼리 저장은 유용한 것으로 확인된 쿼리를 유지하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39613-242">Saving search queries is a standard feature in OMS and can help you keep any queries that you’ve found useful.</span></span> <span data-ttu-id="39613-243">만든 쿼리가 유용하다고 생각되면 **즐겨찾기**를 클릭하여 해당 쿼리를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-243">After you create a query that you find useful, save it by clicking the **Favorites**.</span></span> <span data-ttu-id="39613-244">저장된 쿼리를 사용하면 나중에 사용자 지정 대시보드를 만들 수 있는 [내 대시보드](log-analytics-dashboards.md) 페이지에서 해당 쿼리를 손쉽게 다시 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39613-244">A saved query lets you easily reuse it later from the [My Dashboard](log-analytics-dashboards.md) page where you can create your own custom dashboards.</span></span>

![DockerDashboardView](./media/log-analytics-vmware/dockerdashboardview.png)

#### <a name="create-alerts-from-queries"></a><span data-ttu-id="39613-246">쿼리에서 경고 만들기</span><span class="sxs-lookup"><span data-stu-id="39613-246">Create alerts from queries</span></span>
<span data-ttu-id="39613-247">쿼리를 만든 후에는 특정 이벤트가 발생할 때 경고하도록 이 쿼리를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="39613-247">After you’ve created your queries, you might want to use the queries to alert you when specific events occur.</span></span> <span data-ttu-id="39613-248">경고를 생성하는 방법에 대한 내용은 [Log Analytics의 경고](log-analytics-alerts.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39613-248">See [Alerts in Log Analytics](log-analytics-alerts.md) for information about how to create alerts.</span></span> <span data-ttu-id="39613-249">경고 쿼리 및 기타 쿼리의 예제에 대해서는 [Monitor VMware using OMS Log Analytics](https://blogs.technet.microsoft.com/msoms/2016/06/15/monitor-vmware-using-oms-log-analytics)(영문) 블로그 게시물을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39613-249">For examples of alerting queries and other query examples, see the [Monitor VMware using OMS Log Analytics](https://blogs.technet.microsoft.com/msoms/2016/06/15/monitor-vmware-using-oms-log-analytics) blog post.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="39613-250">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="39613-250">Frequently asked questions</span></span>
### <a name="what-do-i-need-to-do-on-the-esxi-host-setting-what-impact-will-it-have-on-my-current-environment"></a><span data-ttu-id="39613-251">ESXi 호스트 설정에서 수행해야 하는 작업은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="39613-251">What do I need to do on the ESXi host setting?</span></span> <span data-ttu-id="39613-252">현재 환경에 미치는 영향은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="39613-252">What impact will it have on my current environment?</span></span>
<span data-ttu-id="39613-253">이 솔루션은 기본 ESXi 호스트 Syslog 전달 메커니즘을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-253">The solution uses the native ESXi Host Syslog forwarding mechanism.</span></span> <span data-ttu-id="39613-254">ESXi 호스트에 추가 Microsoft 소프트웨어가 없어도 로그를 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39613-254">You don't need any additional Microsoft software on the ESXi Host to capture the logs.</span></span> <span data-ttu-id="39613-255">기존 환경에 미치는 영향이 적습니다.</span><span class="sxs-lookup"><span data-stu-id="39613-255">It should have a low impact to your existing environment.</span></span> <span data-ttu-id="39613-256">그러나 ESXI 기능인 syslog 전달을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-256">However, you do need to set syslog forwarding, which is ESXI functionality.</span></span>

### <a name="do-i-need-to-restart-my-esxi-host"></a><span data-ttu-id="39613-257">ESXi 호스트를 다시 시작해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="39613-257">Do I need to restart my ESXi host?</span></span>
<span data-ttu-id="39613-258">아니요.</span><span class="sxs-lookup"><span data-stu-id="39613-258">No.</span></span> <span data-ttu-id="39613-259">이 프로세스는 호스트를 다시 시작하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39613-259">This process does not require a restart.</span></span> <span data-ttu-id="39613-260">vSphere에서 syslog을 제대로 업데이트하지 못하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39613-260">Sometimes, vSphere does not properly update the syslog.</span></span> <span data-ttu-id="39613-261">이 경우 ESXi 호스트에 로그온하여 syslog를 다시 로드하세요.</span><span class="sxs-lookup"><span data-stu-id="39613-261">In such a case, log on to the ESXi host and reload the syslog.</span></span> <span data-ttu-id="39613-262">호스트를 다시 시작할 필요가 없으므로 이 프로세스는 사용자 환경에 방해가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="39613-262">Again, you don't have to restart the host, so this process isn't disruptive to your environment.</span></span>

### <a name="can-i-increase-or-decrease-the-volume-of-log-data-sent-to-oms"></a><span data-ttu-id="39613-263">OMS로 전송되는 로그 데이터의 양을 늘리거나 줄일 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="39613-263">Can I increase or decrease the volume of log data sent to OMS?</span></span>
<span data-ttu-id="39613-264">예.</span><span class="sxs-lookup"><span data-stu-id="39613-264">Yes you can.</span></span> <span data-ttu-id="39613-265">vsphere에서 ESXi 호스트 로그 수준 설정을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39613-265">You can use the ESXi Host Log Level settings in vSphere.</span></span> <span data-ttu-id="39613-266">로그 수집은 *정보* 수준을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-266">Log collection is based on the *info* level.</span></span> <span data-ttu-id="39613-267">따라서 VM 만들기 또는 삭제를 감사하려면 호스트에서 *정보* 수준을 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-267">So, if you want to audit VM creation or deletion, you need to keep the *info* level on Hostd.</span></span> <span data-ttu-id="39613-268">자세한 내용은 [VMware 기술 자료](https://kb.vmware.com/selfservice/microsites/search.do?&cmd=displayKC&externalId=1017658)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39613-268">For more information, see the [VMware Knowledge Base](https://kb.vmware.com/selfservice/microsites/search.do?&cmd=displayKC&externalId=1017658).</span></span>

### <a name="why-is-hostd-not-providing-data-to-oms-my-log-setting-is-set-to-info"></a><span data-ttu-id="39613-269">호스트에서 OMS에 데이터를 제공하지 않는 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="39613-269">Why is Hostd not providing data to OMS?</span></span> <span data-ttu-id="39613-270">로그는 정보로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39613-270">My log setting is set to info.</span></span>
<span data-ttu-id="39613-271">Syslog 타임스탬프에 대한 ESXi 호스트 버그가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="39613-271">There was an ESXi host bug for the syslog timestamp.</span></span> <span data-ttu-id="39613-272">자세한 내용은 [VMware 기술 자료](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2111202)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39613-272">For more information, see the [VMware Knowledge Base](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2111202).</span></span> <span data-ttu-id="39613-273">해결 방법을 적용하면 호스트가 정상적으로 작동할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="39613-273">After you apply the workaround, Hostd should function normally.</span></span>

### <a name="can-i-have-multiple-esxi-hosts-forwarding-syslog-data-to-a-single-vm-with-omsagent"></a><span data-ttu-id="39613-274">여러 ESXi 호스트에서 omsagent를 실행하는 단일 VM에 syslog 데이터를 전달하도록 할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="39613-274">Can I have multiple ESXi hosts forwarding syslog data to a single VM with omsagent?</span></span>
<span data-ttu-id="39613-275">예.</span><span class="sxs-lookup"><span data-stu-id="39613-275">Yes.</span></span> <span data-ttu-id="39613-276">여러 ESXi 호스트에서 omsagent를 실행하는 단일 VM에 전달하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39613-276">You can have multiple ESXi hosts forwarding to a single VM with omsagent.</span></span>

### <a name="why-dont-i-see-data-flowing-into-oms"></a><span data-ttu-id="39613-277">OMS로 이동하는 데이터가 보이지 않는 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="39613-277">Why don't I see data flowing into OMS?</span></span>
<span data-ttu-id="39613-278">여러 가지 이유가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39613-278">There can be multiple reasons:</span></span>

* <span data-ttu-id="39613-279">ESXi 호스트가 omsagent를 실행하는 VM에 데이터를 올바르게 푸시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="39613-279">The ESXi host is not correctly pushing data to the VM running omsagent.</span></span> <span data-ttu-id="39613-280">테스트하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-280">To test, perform the following steps:</span></span>

  1. <span data-ttu-id="39613-281">확인하려면 ssh를 사용하여 ESXi 호스트에 로그인하고 다음 명령을 실행합니다. `nc -z ipaddressofVM 1514`</span><span class="sxs-lookup"><span data-stu-id="39613-281">To confirm, log on to the ESXi host using ssh and run the following command: `nc -z ipaddressofVM 1514`</span></span>

      <span data-ttu-id="39613-282">실행에 실패한 경우 고급 구성의 vSphere 설정이 올바르지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39613-282">If this is not successful, vSphere settings in the Advanced Configuration are likely not correct.</span></span> <span data-ttu-id="39613-283">syslog 전달을 위해 ESXi 호스트를 설정하는 방법에 대한 자세한 내용은 [syslog 수집 구성](#configure-syslog-collection)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39613-283">See [Configure syslog collection](#configure-syslog-collection) for information about how to set up the ESXi host for syslog forwarding.</span></span>
  2. <span data-ttu-id="39613-284">Syslog 포트 연결에 성공했지만 여전히 데이터가 보이지 않는 경우 ssh를 통해 다음 명령을 실행하여 ESXi 호스트에서 syslog를 다시 로드하세요. ` esxcli system syslog reload`</span><span class="sxs-lookup"><span data-stu-id="39613-284">If syslog port connectivity is successful, but you don't still see any data, then reload the syslog on the ESXi host by using ssh to run the following command: ` esxcli system syslog reload`</span></span>
* <span data-ttu-id="39613-285">OMS 에이전트가 설치된 VM이 올바르게 설정되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="39613-285">The VM with OMS Agent is not set correctly.</span></span> <span data-ttu-id="39613-286">이를 테스트하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-286">To test this, perform the following steps:</span></span>

  1. <span data-ttu-id="39613-287">OMS는 포트 1514를 수신 대기하고 OMS에 데이터를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-287">OMS listens to the port 1514 and pushes data into OMS.</span></span> <span data-ttu-id="39613-288">이 포트가 열려 있는지 확인하려면 다음 명령을 실행합니다. `netstat -a | grep 1514`</span><span class="sxs-lookup"><span data-stu-id="39613-288">To verify that it is open, run the following command: `netstat -a | grep 1514`</span></span>
  2. <span data-ttu-id="39613-289">포트 `1514/tcp`가 열려 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-289">You should see port `1514/tcp` open.</span></span> <span data-ttu-id="39613-290">그렇지 않으면 omsagent가 제대로 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-290">If you do not, verify that the omsagent is installed correctly.</span></span> <span data-ttu-id="39613-291">포트 정보가 보이지 않으면 syslog 포트가 VM에서 열려 있지 않은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="39613-291">If you do not see the port information, then the syslog port is not open on the VM.</span></span>

     1. <span data-ttu-id="39613-292">`ps -ef | grep oms`를 사용하여 OM 에이전트가 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-292">Verify that the OMS Agent is running by using `ps -ef | grep oms`.</span></span> <span data-ttu-id="39613-293">실행되고 있지 않은 경우 ` sudo /opt/microsoft/omsagent/bin/service_control start` 명령을 실행하여 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-293">If it is not running, start the process by running the command ` sudo /opt/microsoft/omsagent/bin/service_control start`</span></span>
     2. <span data-ttu-id="39613-294">`/etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="39613-294">Open the `/etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf` file.</span></span>

         <span data-ttu-id="39613-295">적절한 사용자 및 그룹 설정이 유효한지 확인합니다(`-rw-r--r-- 1 omsagent omiusers 677 Sep 20 16:46 vmware_esxi.conf`와 유사함).</span><span class="sxs-lookup"><span data-stu-id="39613-295">Verify that the proper user and group setting is valid, similar to: `-rw-r--r-- 1 omsagent omiusers 677 Sep 20 16:46 vmware_esxi.conf`</span></span>

         <span data-ttu-id="39613-296">파일이 없거나 사용자 및 그룹 정책 설정이 잘못된 경우 [Linux 서버를 준비](#prepare-a-linux-server)하여 정정 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="39613-296">If the file does not exist or the user and group setting is wrong, take corrective action by [Preparing a Linux server](#prepare-a-linux-server).</span></span>

## <a name="next-steps"></a><span data-ttu-id="39613-297">다음 단계</span><span class="sxs-lookup"><span data-stu-id="39613-297">Next steps</span></span>
* <span data-ttu-id="39613-298">Log Analytics의 [로그 검색](log-analytics-log-searches.md)을 통한 자세한 VMware 호스트 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="39613-298">Use [Log Searches](log-analytics-log-searches.md) in Log Analytics to view detailed VMware host data.</span></span>
* <span data-ttu-id="39613-299">VMware 호스트 데이터를 보여 주는 [사용자 고유의 대시보드 만들기](log-analytics-dashboards.md)</span><span class="sxs-lookup"><span data-stu-id="39613-299">[Create your own dashboards](log-analytics-dashboards.md) showing VMware host data.</span></span>
* <span data-ttu-id="39613-300">특정 VMware 호스트 이벤트가 발생하는 경우의 [경고 만들기](log-analytics-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="39613-300">[Create alerts](log-analytics-alerts.md) when specific VMware host events occur.</span></span>
