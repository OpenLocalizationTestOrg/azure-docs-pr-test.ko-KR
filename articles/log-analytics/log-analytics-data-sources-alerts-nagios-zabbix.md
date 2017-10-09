---
title: "OMS 로그 분석에서 aaaCollect Nagios 및 Zabbix 경고 | Microsoft Docs"
description: "Nagios 및 Zabbix는 오픈 소스 모니터링 도구입니다. 있습니다 수 수집 경고 이러한 도구에서 순서 tooanalyze의 로그 분석에 이러한 다른 소스에서 경고와 함께 합니다.  이 문서에서는 이러한 시스템에서 tooconfigure hello OMS 에이전트에 대 한 Linux toocollect 경고 하는 방법을 설명 합니다."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 23e2252e4fed8bc87baec063694a8472ca84220d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a><span data-ttu-id="6ed39-105">Linux용 OMS 에이전트에서 Log Analytics에 Nagios 및 Zabbix의 경고 수집</span><span class="sxs-lookup"><span data-stu-id="6ed39-105">Collect alerts from Nagios and Zabbix in Log Analytics from OMS Agent for Linux</span></span> 
<span data-ttu-id="6ed39-106">[Nagios](https://www.nagios.org/) 및 [Zabbix](http://www.zabbix.com/)는 오픈 소스 모니터링 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-106">[Nagios](https://www.nagios.org/) and [Zabbix](http://www.zabbix.com/) are open source monitoring tools.</span></span>  <span data-ttu-id="6ed39-107">있습니다 수 수집에서 경고를 이러한 도구의 로그 분석에 순서 tooanalyze와 함께 해당 [다른 소스에서 경고](log-analytics-alerts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-107">You can collect alerts from these tools into Log Analytics in order tooanalyze them along with [alerts from other sources](log-analytics-alerts.md).</span></span>  <span data-ttu-id="6ed39-108">이 문서에서는 이러한 시스템에서 tooconfigure hello OMS 에이전트에 대 한 Linux toocollect 경고 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-108">This article describes how tooconfigure hello OMS Agent for Linux toocollect alerts from these systems.</span></span>
 
## <a name="configure-alert-collection"></a><span data-ttu-id="6ed39-109">경고 수집 구성</span><span class="sxs-lookup"><span data-stu-id="6ed39-109">Configure alert collection</span></span>

### <a name="configuring-nagios-alert-collection"></a><span data-ttu-id="6ed39-110">Nagios 경고 수집 구성</span><span class="sxs-lookup"><span data-stu-id="6ed39-110">Configuring Nagios alert collection</span></span>
<span data-ttu-id="6ed39-111">Hello hello Nagios 서버 toocollect 경고에 대해 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-111">Perform hello following steps on hello Nagios server toocollect alerts.</span></span>

1. <span data-ttu-id="6ed39-112">Grant hello 사용자 **omsagent** 읽기 권한을 toohello Nagios 로그 파일 (예: `/var/log/nagios/nagios.log`).</span><span class="sxs-lookup"><span data-stu-id="6ed39-112">Grant hello user **omsagent** read access toohello Nagios log file (i.e. `/var/log/nagios/nagios.log`).</span></span> <span data-ttu-id="6ed39-113">Hello 그룹 hello nagios.log 파일을 소유 하는 것으로 가정 `nagios`, hello 사용자를 추가할 수 있습니다 **omsagent** toohello **nagios** 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-113">Assuming hello nagios.log file is owned by hello group `nagios`, you can add hello user **omsagent** toohello **nagios** group.</span></span> 

    <span data-ttu-id="6ed39-114">sudo usermod -a -G nagios omsagent</span><span class="sxs-lookup"><span data-stu-id="6ed39-114">sudo usermod -a -G nagios omsagent</span></span>

2.  <span data-ttu-id="6ed39-115">Hello 구성 파일 수정 (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="6ed39-115">Modify hello configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="6ed39-116">충족 했는지 확인 hello 다음 항목이 있고 주석으로 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-116">Ensure hello following entries are present and not commented out:</span></span>  

        <source>  
          type tail  
          #Update path toopoint tooyour nagios.log  
          path /var/log/nagios/nagios.log  
          format none  
          tag oms.nagios  
        </source>  
      
        <filter oms.nagios>  
          type filter_nagios_log  
        </filter>  

3. <span data-ttu-id="6ed39-117">Hello omsagent 디먼을 다시 시작</span><span class="sxs-lookup"><span data-stu-id="6ed39-117">Restart hello omsagent daemon</span></span>

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a><span data-ttu-id="6ed39-118">Zabbix 경고 수집 구성</span><span class="sxs-lookup"><span data-stu-id="6ed39-118">Configuring Zabbix alert collection</span></span>
<span data-ttu-id="6ed39-119">Zabbix 서버에서 경고 toocollect 해야 toospecify 사용자와 암호를 *일반 텍스트*합니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-119">toocollect alerts from a Zabbix server, you need toospecify a user and password in *clear text*.</span></span> <span data-ttu-id="6ed39-120">이 적절 하지만 hello 사용자를 만들고 toomonitor onlu 사용 권한을 부여 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-120">This is not ideal, but we recommend that you create hello user and grant permissions toomonitor onlu.</span></span>

<span data-ttu-id="6ed39-121">Hello hello Nagios 서버 toocollect 경고에 대해 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-121">Perform hello following steps on hello Nagios server toocollect alerts.</span></span>

1. <span data-ttu-id="6ed39-122">Hello 구성 파일 수정 (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="6ed39-122">Modify hello configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="6ed39-123">항목을 다음 hello가 있고 하지 주석으로 처리를 확인 합니다.  Zabbix 환경에 대 한 hello 사용자 이름 및 암호 toovalues를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-123">Ensure hello following entries are present and not commented out.  Change hello user name and password toovalues for your Zabbix environment.</span></span>

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. <span data-ttu-id="6ed39-124">Hello omsagent 디먼을 다시 시작</span><span class="sxs-lookup"><span data-stu-id="6ed39-124">Restart hello omsagent daemon</span></span>

    <span data-ttu-id="6ed39-125">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span><span class="sxs-lookup"><span data-stu-id="6ed39-125">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span></span>


## <a name="alert-records"></a><span data-ttu-id="6ed39-126">경고 레코드</span><span class="sxs-lookup"><span data-stu-id="6ed39-126">Alert records</span></span>
<span data-ttu-id="6ed39-127">Log Analytics에서 [로그 검색](log-analytics-log-searches.md)을 사용하여 Nagios 및 Zabbix에서 경고 레코드를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-127">You can retrieve alert records from Nagios and Zabbix using [log searches](log-analytics-log-searches.md) in Log Analytics.</span></span>

### <a name="nagios-alert-records"></a><span data-ttu-id="6ed39-128">Nagios 경고 레코드</span><span class="sxs-lookup"><span data-stu-id="6ed39-128">Nagios Alert records</span></span>

<span data-ttu-id="6ed39-129">Nagios에서 수집된 경고는 **경고**의 **형식** 및 **Nagios**의 **SourceSystem**을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-129">Alert records collected by Nagios have a **Type** of **Alert** and a **SourceSystem** of **Nagios**.</span></span>  <span data-ttu-id="6ed39-130">다음 표에 hello에 hello 속성을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-130">They have hello properties in hello following table.</span></span>

| <span data-ttu-id="6ed39-131">속성</span><span class="sxs-lookup"><span data-stu-id="6ed39-131">Property</span></span> | <span data-ttu-id="6ed39-132">설명</span><span class="sxs-lookup"><span data-stu-id="6ed39-132">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="6ed39-133">형식</span><span class="sxs-lookup"><span data-stu-id="6ed39-133">Type</span></span> |<span data-ttu-id="6ed39-134">*경고*</span><span class="sxs-lookup"><span data-stu-id="6ed39-134">*Alert*</span></span> |
| <span data-ttu-id="6ed39-135">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="6ed39-135">SourceSystem</span></span> |<span data-ttu-id="6ed39-136">*Nagios*</span><span class="sxs-lookup"><span data-stu-id="6ed39-136">*Nagios*</span></span> |
| <span data-ttu-id="6ed39-137">AlertName</span><span class="sxs-lookup"><span data-stu-id="6ed39-137">AlertName</span></span> |<span data-ttu-id="6ed39-138">Hello 경고의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-138">Name of hello alert.</span></span> |
| <span data-ttu-id="6ed39-139">AlertDescription</span><span class="sxs-lookup"><span data-stu-id="6ed39-139">AlertDescription</span></span> | <span data-ttu-id="6ed39-140">Hello 경고의 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-140">Description of hello alert.</span></span> |
| <span data-ttu-id="6ed39-141">AlertState</span><span class="sxs-lookup"><span data-stu-id="6ed39-141">AlertState</span></span> | <span data-ttu-id="6ed39-142">Hello 서비스 또는 호스트의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-142">Status of hello service or host.</span></span><br><br><span data-ttu-id="6ed39-143">확인</span><span class="sxs-lookup"><span data-stu-id="6ed39-143">OK</span></span><br><span data-ttu-id="6ed39-144">경고</span><span class="sxs-lookup"><span data-stu-id="6ed39-144">WARNING</span></span><br><span data-ttu-id="6ed39-145">위로</span><span class="sxs-lookup"><span data-stu-id="6ed39-145">UP</span></span><br><span data-ttu-id="6ed39-146">아래로</span><span class="sxs-lookup"><span data-stu-id="6ed39-146">DOWN</span></span> |
| <span data-ttu-id="6ed39-147">HostName</span><span class="sxs-lookup"><span data-stu-id="6ed39-147">HostName</span></span> | <span data-ttu-id="6ed39-148">Hello 경고를 생성 하는 hello 호스트의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-148">Name of hello host that created hello alert.</span></span> |
| <span data-ttu-id="6ed39-149">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="6ed39-149">PriorityNumber</span></span> | <span data-ttu-id="6ed39-150">Hello 경고의 우선 순위 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-150">Priority level of hello alert.</span></span> |
| <span data-ttu-id="6ed39-151">StateType</span><span class="sxs-lookup"><span data-stu-id="6ed39-151">StateType</span></span> | <span data-ttu-id="6ed39-152">hello 형식 hello 경고의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-152">hello type of state of hello alert.</span></span><br><br><span data-ttu-id="6ed39-153">소프트 - 다시 확인되지 않은 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-153">SOFT - Issue that has not been rechecked.</span></span><br><span data-ttu-id="6ed39-154">하드 - 특정 횟수를 다시 확인한 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-154">HARD - Issue that has been rechecked a specified number of times.</span></span>  |
| <span data-ttu-id="6ed39-155">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="6ed39-155">TimeGenerated</span></span> |<span data-ttu-id="6ed39-156">날짜 및 시간 hello 경고가 생성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-156">Date and time hello alert was created.</span></span> |


### <a name="zabbix-alert-records"></a><span data-ttu-id="6ed39-157">Zabbix 경고 레코드</span><span class="sxs-lookup"><span data-stu-id="6ed39-157">Zabbix alert records</span></span>
<span data-ttu-id="6ed39-158">Zabbix에서 수집된 경고는 **경고**의 **형식** 및 **Zabbix**의 **SourceSystem**을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-158">Alert records collected by Zabbix have a **Type** of **Alert** and a **SourceSystem** of **Zabbix**.</span></span>  <span data-ttu-id="6ed39-159">다음 표에 hello에 hello 속성을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-159">They have hello properties in hello following table.</span></span>

| <span data-ttu-id="6ed39-160">속성</span><span class="sxs-lookup"><span data-stu-id="6ed39-160">Property</span></span> | <span data-ttu-id="6ed39-161">설명</span><span class="sxs-lookup"><span data-stu-id="6ed39-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="6ed39-162">형식</span><span class="sxs-lookup"><span data-stu-id="6ed39-162">Type</span></span> |<span data-ttu-id="6ed39-163">*경고*</span><span class="sxs-lookup"><span data-stu-id="6ed39-163">*Alert*</span></span> |
| <span data-ttu-id="6ed39-164">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="6ed39-164">SourceSystem</span></span> |<span data-ttu-id="6ed39-165">*Zabbix*</span><span class="sxs-lookup"><span data-stu-id="6ed39-165">*Zabbix*</span></span> |
| <span data-ttu-id="6ed39-166">AlertName</span><span class="sxs-lookup"><span data-stu-id="6ed39-166">AlertName</span></span> | <span data-ttu-id="6ed39-167">Hello 경고의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-167">Name of hello alert.</span></span> |
| <span data-ttu-id="6ed39-168">AlertPriority</span><span class="sxs-lookup"><span data-stu-id="6ed39-168">AlertPriority</span></span> | <span data-ttu-id="6ed39-169">Hello 경고의 심각도입니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-169">Severity of hello alert.</span></span><br><br><span data-ttu-id="6ed39-170">분류되지 않음</span><span class="sxs-lookup"><span data-stu-id="6ed39-170">not classified</span></span><br><span data-ttu-id="6ed39-171">정보</span><span class="sxs-lookup"><span data-stu-id="6ed39-171">information</span></span><br><span data-ttu-id="6ed39-172">Warning</span><span class="sxs-lookup"><span data-stu-id="6ed39-172">warning</span></span><br><span data-ttu-id="6ed39-173">average</span><span class="sxs-lookup"><span data-stu-id="6ed39-173">average</span></span><br><span data-ttu-id="6ed39-174">높음</span><span class="sxs-lookup"><span data-stu-id="6ed39-174">high</span></span><br><span data-ttu-id="6ed39-175">심각</span><span class="sxs-lookup"><span data-stu-id="6ed39-175">disaster</span></span>  |
| <span data-ttu-id="6ed39-176">AlertState</span><span class="sxs-lookup"><span data-stu-id="6ed39-176">AlertState</span></span> | <span data-ttu-id="6ed39-177">Hello 경고의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-177">State of hello alert.</span></span><br><br><span data-ttu-id="6ed39-178">0-toodate를 상태가입니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-178">0 - State is up toodate.</span></span><br><span data-ttu-id="6ed39-179">1 - 상태를 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-179">1 - State is unknown.</span></span>  |
| <span data-ttu-id="6ed39-180">AlertTypeNumber</span><span class="sxs-lookup"><span data-stu-id="6ed39-180">AlertTypeNumber</span></span> | <span data-ttu-id="6ed39-181">경고가 여러 문제 이벤트를 생성할 수 있는지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-181">Specifies whether alert can generate multiple problem events.</span></span><br><br><span data-ttu-id="6ed39-182">0-toodate를 상태가입니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-182">0 - State is up toodate.</span></span><br><span data-ttu-id="6ed39-183">1 - 상태를 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-183">1 - State is unknown.</span></span>    |
| <span data-ttu-id="6ed39-184">설명</span><span class="sxs-lookup"><span data-stu-id="6ed39-184">Comments</span></span> | <span data-ttu-id="6ed39-185">경고에 대한 추가 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-185">Additional comments for alert.</span></span> |
| <span data-ttu-id="6ed39-186">HostName</span><span class="sxs-lookup"><span data-stu-id="6ed39-186">HostName</span></span> | <span data-ttu-id="6ed39-187">Hello 경고를 생성 하는 hello 호스트의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-187">Name of hello host that created hello alert.</span></span> |
| <span data-ttu-id="6ed39-188">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="6ed39-188">PriorityNumber</span></span> | <span data-ttu-id="6ed39-189">Hello 경고의 심각도 나타내는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-189">Value indicating severity of hello alert.</span></span><br><br><span data-ttu-id="6ed39-190">0 - 분류되지 않음</span><span class="sxs-lookup"><span data-stu-id="6ed39-190">0 - not classified</span></span><br><span data-ttu-id="6ed39-191">1 - 정보</span><span class="sxs-lookup"><span data-stu-id="6ed39-191">1 - information</span></span><br><span data-ttu-id="6ed39-192">2 - 경고</span><span class="sxs-lookup"><span data-stu-id="6ed39-192">2 - warning</span></span><br><span data-ttu-id="6ed39-193">3 - 평균</span><span class="sxs-lookup"><span data-stu-id="6ed39-193">3 - average</span></span><br><span data-ttu-id="6ed39-194">4 - 높음</span><span class="sxs-lookup"><span data-stu-id="6ed39-194">4 - high</span></span><br><span data-ttu-id="6ed39-195">5 - 심각</span><span class="sxs-lookup"><span data-stu-id="6ed39-195">5 - disaster</span></span> |
| <span data-ttu-id="6ed39-196">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="6ed39-196">TimeGenerated</span></span> |<span data-ttu-id="6ed39-197">날짜 및 시간 hello 경고가 생성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-197">Date and time hello alert was created.</span></span> |
| <span data-ttu-id="6ed39-198">TimeLastModified</span><span class="sxs-lookup"><span data-stu-id="6ed39-198">TimeLastModified</span></span> |<span data-ttu-id="6ed39-199">Hello 경고의 날짜 및 시간 hello 상태 마지막 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-199">Date and time hello state of hello alert was last changed.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="6ed39-200">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6ed39-200">Next steps</span></span>
* <span data-ttu-id="6ed39-201">Log Analytics에서 [경고](log-analytics-alerts.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-201">Learn about [alerts](log-analytics-alerts.md) in Log Analytics.</span></span>
* <span data-ttu-id="6ed39-202">에 대 한 자세한 내용은 [검색 로그](log-analytics-log-searches.md) tooanalyze hello 데이터가 데이터 원본 및 솔루션에서 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ed39-202">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
