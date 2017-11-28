---
title: "OMS Log Analytics에서 Nagios 및 Zabbix 경고 수집 | Microsoft Docs"
description: "Nagios 및 Zabbix는 오픈 소스 모니터링 도구입니다. 다른 원본의 경고와 함께 분석하기 위해 이러한 도구에서 Log Analytics로 경고를 수집할 수 있습니다.  이 문서에서는 이러한 시스템에서 경고를 수집하도록 Linux용 OMS 에이전트를 구성하는 방법을 설명합니다."
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
ms.openlocfilehash: 0b64c32e1031e704d50aab0b38eaea41e27d134b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a><span data-ttu-id="ce053-105">Linux용 OMS 에이전트에서 Log Analytics에 Nagios 및 Zabbix의 경고 수집</span><span class="sxs-lookup"><span data-stu-id="ce053-105">Collect alerts from Nagios and Zabbix in Log Analytics from OMS Agent for Linux</span></span> 
<span data-ttu-id="ce053-106">[Nagios](https://www.nagios.org/) 및 [Zabbix](http://www.zabbix.com/)는 오픈 소스 모니터링 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-106">[Nagios](https://www.nagios.org/) and [Zabbix](http://www.zabbix.com/) are open source monitoring tools.</span></span>  <span data-ttu-id="ce053-107">[다른 원본의 경고](log-analytics-alerts.md)와 함께 분석하기 위해 이러한 도구에서 Log Analytics로 경고를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-107">You can collect alerts from these tools into Log Analytics in order to analyze them along with [alerts from other sources](log-analytics-alerts.md).</span></span>  <span data-ttu-id="ce053-108">이 문서에서는 이러한 시스템에서 경고를 수집하도록 Linux용 OMS 에이전트를 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-108">This article describes how to configure the OMS Agent for Linux to collect alerts from these systems.</span></span>
 
## <a name="configure-alert-collection"></a><span data-ttu-id="ce053-109">경고 수집 구성</span><span class="sxs-lookup"><span data-stu-id="ce053-109">Configure alert collection</span></span>

### <a name="configuring-nagios-alert-collection"></a><span data-ttu-id="ce053-110">Nagios 경고 수집 구성</span><span class="sxs-lookup"><span data-stu-id="ce053-110">Configuring Nagios alert collection</span></span>
<span data-ttu-id="ce053-111">Nagios 서버에서 다음 단계를 수행하여 경고를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-111">Perform the following steps on the Nagios server to collect alerts.</span></span>

1. <span data-ttu-id="ce053-112">**omsagent** 사용자에게 Nagios 로그 파일(예: `/var/log/nagios/nagios.log`)에 대한 읽기 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-112">Grant the user **omsagent** read access to the Nagios log file (i.e. `/var/log/nagios/nagios.log`).</span></span> <span data-ttu-id="ce053-113">nagios.log 파일이 `nagios` 그룹의 소유라는 가정 하에, **omsagent** 사용자를 **nagios** 그룹에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-113">Assuming the nagios.log file is owned by the group `nagios`, you can add the user **omsagent** to the **nagios** group.</span></span> 

    <span data-ttu-id="ce053-114">sudo usermod -a -G nagios omsagent</span><span class="sxs-lookup"><span data-stu-id="ce053-114">sudo usermod -a -G nagios omsagent</span></span>

2.  <span data-ttu-id="ce053-115">(`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`)에서 구성 파일을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-115">Modify the configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="ce053-116">다음 항목이 포함되고 주석 처리되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-116">Ensure the following entries are present and not commented out:</span></span>  

        <source>  
          type tail  
          #Update path to point to your nagios.log  
          path /var/log/nagios/nagios.log  
          format none  
          tag oms.nagios  
        </source>  
      
        <filter oms.nagios>  
          type filter_nagios_log  
        </filter>  

3. <span data-ttu-id="ce053-117">omsagent 디먼 다시 시작</span><span class="sxs-lookup"><span data-stu-id="ce053-117">Restart the omsagent daemon</span></span>

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a><span data-ttu-id="ce053-118">Zabbix 경고 수집 구성</span><span class="sxs-lookup"><span data-stu-id="ce053-118">Configuring Zabbix alert collection</span></span>
<span data-ttu-id="ce053-119">Zabbix 서버에서 경고를 수집하려면 *일반 텍스트*에서 사용자 및 암호를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-119">To collect alerts from a Zabbix server, you need to specify a user and password in *clear text*.</span></span> <span data-ttu-id="ce053-120">이상적인 방법이 아니지만 사용자를 생성하고 모니터링 권한만 부여하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-120">This is not ideal, but we recommend that you create the user and grant permissions to monitor onlu.</span></span>

<span data-ttu-id="ce053-121">Nagios 서버에서 다음 단계를 수행하여 경고를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-121">Perform the following steps on the Nagios server to collect alerts.</span></span>

1. <span data-ttu-id="ce053-122">(`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`)에서 구성 파일을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-122">Modify the configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="ce053-123">다음 항목이 포함되고 주석 처리되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-123">Ensure the following entries are present and not commented out.</span></span>  <span data-ttu-id="ce053-124">Zabbix 환경에 대한 값으로 사용자 이름 및 암호를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-124">Change the user name and password to values for your Zabbix environment.</span></span>

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. <span data-ttu-id="ce053-125">omsagent 디먼 다시 시작</span><span class="sxs-lookup"><span data-stu-id="ce053-125">Restart the omsagent daemon</span></span>

    <span data-ttu-id="ce053-126">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span><span class="sxs-lookup"><span data-stu-id="ce053-126">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span></span>


## <a name="alert-records"></a><span data-ttu-id="ce053-127">경고 레코드</span><span class="sxs-lookup"><span data-stu-id="ce053-127">Alert records</span></span>
<span data-ttu-id="ce053-128">Log Analytics에서 [로그 검색](log-analytics-log-searches.md)을 사용하여 Nagios 및 Zabbix에서 경고 레코드를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-128">You can retrieve alert records from Nagios and Zabbix using [log searches](log-analytics-log-searches.md) in Log Analytics.</span></span>

### <a name="nagios-alert-records"></a><span data-ttu-id="ce053-129">Nagios 경고 레코드</span><span class="sxs-lookup"><span data-stu-id="ce053-129">Nagios Alert records</span></span>

<span data-ttu-id="ce053-130">Nagios에서 수집된 경고는 **경고**의 **형식** 및 **Nagios**의 **SourceSystem**을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-130">Alert records collected by Nagios have a **Type** of **Alert** and a **SourceSystem** of **Nagios**.</span></span>  <span data-ttu-id="ce053-131">이들은 다음 표의 속성을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-131">They have the properties in the following table.</span></span>

| <span data-ttu-id="ce053-132">속성</span><span class="sxs-lookup"><span data-stu-id="ce053-132">Property</span></span> | <span data-ttu-id="ce053-133">설명</span><span class="sxs-lookup"><span data-stu-id="ce053-133">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ce053-134">형식</span><span class="sxs-lookup"><span data-stu-id="ce053-134">Type</span></span> |<span data-ttu-id="ce053-135">*경고*</span><span class="sxs-lookup"><span data-stu-id="ce053-135">*Alert*</span></span> |
| <span data-ttu-id="ce053-136">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="ce053-136">SourceSystem</span></span> |<span data-ttu-id="ce053-137">*Nagios*</span><span class="sxs-lookup"><span data-stu-id="ce053-137">*Nagios*</span></span> |
| <span data-ttu-id="ce053-138">AlertName</span><span class="sxs-lookup"><span data-stu-id="ce053-138">AlertName</span></span> |<span data-ttu-id="ce053-139">경고의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-139">Name of the alert.</span></span> |
| <span data-ttu-id="ce053-140">AlertDescription</span><span class="sxs-lookup"><span data-stu-id="ce053-140">AlertDescription</span></span> | <span data-ttu-id="ce053-141">경고에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-141">Description of the alert.</span></span> |
| <span data-ttu-id="ce053-142">AlertState</span><span class="sxs-lookup"><span data-stu-id="ce053-142">AlertState</span></span> | <span data-ttu-id="ce053-143">서비스 또는 호스트의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-143">Status of the service or host.</span></span><br><br><span data-ttu-id="ce053-144">확인</span><span class="sxs-lookup"><span data-stu-id="ce053-144">OK</span></span><br><span data-ttu-id="ce053-145">경고</span><span class="sxs-lookup"><span data-stu-id="ce053-145">WARNING</span></span><br><span data-ttu-id="ce053-146">위로</span><span class="sxs-lookup"><span data-stu-id="ce053-146">UP</span></span><br><span data-ttu-id="ce053-147">아래로</span><span class="sxs-lookup"><span data-stu-id="ce053-147">DOWN</span></span> |
| <span data-ttu-id="ce053-148">HostName</span><span class="sxs-lookup"><span data-stu-id="ce053-148">HostName</span></span> | <span data-ttu-id="ce053-149">경고를 생성한 호스트의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-149">Name of the host that created the alert.</span></span> |
| <span data-ttu-id="ce053-150">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="ce053-150">PriorityNumber</span></span> | <span data-ttu-id="ce053-151">경고의 우선 순위 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-151">Priority level of the alert.</span></span> |
| <span data-ttu-id="ce053-152">StateType</span><span class="sxs-lookup"><span data-stu-id="ce053-152">StateType</span></span> | <span data-ttu-id="ce053-153">경고 상태의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-153">The type of state of the alert.</span></span><br><br><span data-ttu-id="ce053-154">소프트 - 다시 확인되지 않은 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-154">SOFT - Issue that has not been rechecked.</span></span><br><span data-ttu-id="ce053-155">하드 - 특정 횟수를 다시 확인한 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-155">HARD - Issue that has been rechecked a specified number of times.</span></span>  |
| <span data-ttu-id="ce053-156">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="ce053-156">TimeGenerated</span></span> |<span data-ttu-id="ce053-157">경고가 만들어진 날짜 및 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-157">Date and time the alert was created.</span></span> |


### <a name="zabbix-alert-records"></a><span data-ttu-id="ce053-158">Zabbix 경고 레코드</span><span class="sxs-lookup"><span data-stu-id="ce053-158">Zabbix alert records</span></span>
<span data-ttu-id="ce053-159">Zabbix에서 수집된 경고는 **경고**의 **형식** 및 **Zabbix**의 **SourceSystem**을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-159">Alert records collected by Zabbix have a **Type** of **Alert** and a **SourceSystem** of **Zabbix**.</span></span>  <span data-ttu-id="ce053-160">이들은 다음 표의 속성을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-160">They have the properties in the following table.</span></span>

| <span data-ttu-id="ce053-161">속성</span><span class="sxs-lookup"><span data-stu-id="ce053-161">Property</span></span> | <span data-ttu-id="ce053-162">설명</span><span class="sxs-lookup"><span data-stu-id="ce053-162">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ce053-163">형식</span><span class="sxs-lookup"><span data-stu-id="ce053-163">Type</span></span> |<span data-ttu-id="ce053-164">*경고*</span><span class="sxs-lookup"><span data-stu-id="ce053-164">*Alert*</span></span> |
| <span data-ttu-id="ce053-165">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="ce053-165">SourceSystem</span></span> |<span data-ttu-id="ce053-166">*Zabbix*</span><span class="sxs-lookup"><span data-stu-id="ce053-166">*Zabbix*</span></span> |
| <span data-ttu-id="ce053-167">AlertName</span><span class="sxs-lookup"><span data-stu-id="ce053-167">AlertName</span></span> | <span data-ttu-id="ce053-168">경고의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-168">Name of the alert.</span></span> |
| <span data-ttu-id="ce053-169">AlertPriority</span><span class="sxs-lookup"><span data-stu-id="ce053-169">AlertPriority</span></span> | <span data-ttu-id="ce053-170">경고의 심각도입니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-170">Severity of the alert.</span></span><br><br><span data-ttu-id="ce053-171">분류되지 않음</span><span class="sxs-lookup"><span data-stu-id="ce053-171">not classified</span></span><br><span data-ttu-id="ce053-172">정보</span><span class="sxs-lookup"><span data-stu-id="ce053-172">information</span></span><br><span data-ttu-id="ce053-173">Warning</span><span class="sxs-lookup"><span data-stu-id="ce053-173">warning</span></span><br><span data-ttu-id="ce053-174">average</span><span class="sxs-lookup"><span data-stu-id="ce053-174">average</span></span><br><span data-ttu-id="ce053-175">높음</span><span class="sxs-lookup"><span data-stu-id="ce053-175">high</span></span><br><span data-ttu-id="ce053-176">심각</span><span class="sxs-lookup"><span data-stu-id="ce053-176">disaster</span></span>  |
| <span data-ttu-id="ce053-177">AlertState</span><span class="sxs-lookup"><span data-stu-id="ce053-177">AlertState</span></span> | <span data-ttu-id="ce053-178">경고의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-178">State of the alert.</span></span><br><br><span data-ttu-id="ce053-179">0 - 최신 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-179">0 - State is up to date.</span></span><br><span data-ttu-id="ce053-180">1 - 상태를 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-180">1 - State is unknown.</span></span>  |
| <span data-ttu-id="ce053-181">AlertTypeNumber</span><span class="sxs-lookup"><span data-stu-id="ce053-181">AlertTypeNumber</span></span> | <span data-ttu-id="ce053-182">경고가 여러 문제 이벤트를 생성할 수 있는지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-182">Specifies whether alert can generate multiple problem events.</span></span><br><br><span data-ttu-id="ce053-183">0 - 최신 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-183">0 - State is up to date.</span></span><br><span data-ttu-id="ce053-184">1 - 상태를 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-184">1 - State is unknown.</span></span>    |
| <span data-ttu-id="ce053-185">설명</span><span class="sxs-lookup"><span data-stu-id="ce053-185">Comments</span></span> | <span data-ttu-id="ce053-186">경고에 대한 추가 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-186">Additional comments for alert.</span></span> |
| <span data-ttu-id="ce053-187">HostName</span><span class="sxs-lookup"><span data-stu-id="ce053-187">HostName</span></span> | <span data-ttu-id="ce053-188">경고를 생성한 호스트의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-188">Name of the host that created the alert.</span></span> |
| <span data-ttu-id="ce053-189">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="ce053-189">PriorityNumber</span></span> | <span data-ttu-id="ce053-190">경고의 심각도를 나타내는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-190">Value indicating severity of the alert.</span></span><br><br><span data-ttu-id="ce053-191">0 - 분류되지 않음</span><span class="sxs-lookup"><span data-stu-id="ce053-191">0 - not classified</span></span><br><span data-ttu-id="ce053-192">1 - 정보</span><span class="sxs-lookup"><span data-stu-id="ce053-192">1 - information</span></span><br><span data-ttu-id="ce053-193">2 - 경고</span><span class="sxs-lookup"><span data-stu-id="ce053-193">2 - warning</span></span><br><span data-ttu-id="ce053-194">3 - 평균</span><span class="sxs-lookup"><span data-stu-id="ce053-194">3 - average</span></span><br><span data-ttu-id="ce053-195">4 - 높음</span><span class="sxs-lookup"><span data-stu-id="ce053-195">4 - high</span></span><br><span data-ttu-id="ce053-196">5 - 심각</span><span class="sxs-lookup"><span data-stu-id="ce053-196">5 - disaster</span></span> |
| <span data-ttu-id="ce053-197">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="ce053-197">TimeGenerated</span></span> |<span data-ttu-id="ce053-198">경고가 만들어진 날짜 및 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-198">Date and time the alert was created.</span></span> |
| <span data-ttu-id="ce053-199">TimeLastModified</span><span class="sxs-lookup"><span data-stu-id="ce053-199">TimeLastModified</span></span> |<span data-ttu-id="ce053-200">경고의 상태가 마지막 변경된 날짜 및 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-200">Date and time the state of the alert was last changed.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="ce053-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ce053-201">Next steps</span></span>
* <span data-ttu-id="ce053-202">Log Analytics에서 [경고](log-analytics-alerts.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-202">Learn about [alerts](log-analytics-alerts.md) in Log Analytics.</span></span>
* <span data-ttu-id="ce053-203">데이터 원본 및 솔루션에서 수집한 데이터를 분석하기 위해 [로그 검색](log-analytics-log-searches.md) 에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ce053-203">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
