---
title: "OMS 로그 분석에서 CollectD aaaCollect 데이터로 | Microsoft Docs"
description: "CollectD는 주기적으로 응용 프로그램의 데이터 및 시스템 수준 정보를 수집하는 오픈 소스 Linux 디먼입니다.  이 문서에서는 Log Analytics에서 CollectD의 데이터 수집에 대한 정보를 제공합니다."
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
ms.date: 05/02/2017
ms.author: magoedte
ms.openlocfilehash: 7ad82c9c67a664aabd44f08bef2253d84cd2dfba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a><span data-ttu-id="4a504-104">Log Analytics에서 Linux 에이전트의 CollectD에서 데이터 수집</span><span class="sxs-lookup"><span data-stu-id="4a504-104">Collect data from CollectD on Linux agents in Log Analytics</span></span>
<span data-ttu-id="4a504-105">[CollectD](https://collectd.org/)는 주기적으로 응용 프로그램의 성능 메트릭 및 시스템 수준 정보를 수집하는 오픈 소스 Linux 디먼입니다.</span><span class="sxs-lookup"><span data-stu-id="4a504-105">[CollectD](https://collectd.org/) is an open source Linux daemon that periodically collects performance metrics from applications and system level information.</span></span> <span data-ttu-id="4a504-106">예제 응용 프로그램에는 가상 컴퓨터 JVM (Java) hello, MySQL Server 및 Nginx 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a504-106">Example applications include hello Java Virtual Machine (JVM), MySQL Server, and Nginx.</span></span> <span data-ttu-id="4a504-107">이 문서에서는 Log Analytics에서 CollectD의 성능 데이터 수집에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4a504-107">This article provides information on collecting performance data from CollectD in Log Analytics.</span></span>

<span data-ttu-id="4a504-108">사용 가능한 플러그 인의 전체 목록은 [플러그 인의 테이블](https://collectd.org/wiki/index.php/Table_of_Plugins)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a504-108">A full list of available plugins can be found at [Table of Plugins](https://collectd.org/wiki/index.php/Table_of_Plugins).</span></span>

![CollectD 개요](media/log-analytics-data-sources-collectd/overview.png)

<span data-ttu-id="4a504-110">hello 다음 CollectD 구성에에서 포함 된 Linux tooroute CollectD 데이터 toohello OMS 에이전트에 대 한 OMS 에이전트 hello Linux.</span><span class="sxs-lookup"><span data-stu-id="4a504-110">hello following CollectD configuration is included in hello OMS Agent for Linux tooroute  CollectD data toohello OMS Agent for Linux.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

<span data-ttu-id="4a504-111">또한 같은 구성이 대신 hello를 사용 하는 5.5 전에 collectD의 버전을 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="4a504-111">Additionally, if using an versions of collectD before 5.5 use hello following configuration instead.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

<span data-ttu-id="4a504-112">hello CollectD 구성은 hello 기본값을 사용 하 여`write_http` 포트 26000 tooOMS Linux 용 에이전트를 통해 플러그 인 toosend 성능 메트릭 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="4a504-112">hello CollectD configuration uses hello default`write_http` plugin toosend performance metric data over port 26000 tooOMS Agent for Linux.</span></span> 

> [!NOTE]
> <span data-ttu-id="4a504-113">필요한 경우이 포트에서 구성 된 tooa 정의 된 사용자 지정 포트를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a504-113">This port can be configured tooa custom-defined port if needed.</span></span>

<span data-ttu-id="4a504-114">Linux 용 OMS 에이전트 hello 26000 CollectD 메트릭에 대 한 포트에서 수신 및 다음 tooOMS 스키마 메트릭을 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a504-114">hello OMS Agent for Linux also listens on port 26000 for CollectD metrics and then converts them tooOMS schema metrics.</span></span> <span data-ttu-id="4a504-115">hello 다음은 Linux 구성에 대 한 OMS 에이전트 hello `collectd.conf`합니다.</span><span class="sxs-lookup"><span data-stu-id="4a504-115">hello following is hello OMS Agent for Linux configuration  `collectd.conf`.</span></span>

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a><span data-ttu-id="4a504-116">지원되는 버전</span><span class="sxs-lookup"><span data-stu-id="4a504-116">Versions supported</span></span>
- <span data-ttu-id="4a504-117">Log Analytics는 현재 CollectD 버전 4.8 이상을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4a504-117">Log Analytics currently supports CollectD version 4.8 and above.</span></span>
- <span data-ttu-id="4a504-118">CollectD 메트릭 수집에 Linux용 OMS 에이전트 v1.1.0-217 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4a504-118">OMS Agent for Linux v1.1.0-217 or above is required for CollectD metric collection.</span></span>


## <a name="configuration"></a><span data-ttu-id="4a504-119">구성</span><span class="sxs-lookup"><span data-stu-id="4a504-119">Configuration</span></span>
<span data-ttu-id="4a504-120">hello 다음은 로그 분석에 CollectD 데이터의 기본 단계 tooconfigure 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="4a504-120">hello following are basic steps tooconfigure collection of CollectD data in Log Analytics.</span></span>

1. <span data-ttu-id="4a504-121">Hello write_http 플러그 인을 사용 하 여 Linux 용 OMS 에이전트 CollectD toosend 데이터 toohello를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a504-121">Configure CollectD toosend data toohello OMS Agent for Linux using hello write_http plugin.</span></span>  
2. <span data-ttu-id="4a504-122">Hello 적절 한 포트에 hello CollectD 데이터에 대 한 Linux toolisten에 대 한 hello OMS 에이전트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a504-122">Configure hello OMS Agent for Linux toolisten for hello CollectD data on hello appropriate port.</span></span>
3. <span data-ttu-id="4a504-123">CollectD 및 Linux용 OMS 에이전트를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4a504-123">Restart CollectD and OMS Agent for Linux.</span></span>

### <a name="configure-collectd-tooforward-data"></a><span data-ttu-id="4a504-124">CollectD tooforward 데이터 구성</span><span class="sxs-lookup"><span data-stu-id="4a504-124">Configure CollectD tooforward data</span></span> 

1. <span data-ttu-id="4a504-125">Linux 용 OMS 에이전트 tooroute CollectD 데이터 toohello `oms.conf` 요구 toobe tooCollectD의 구성 디렉터리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a504-125">tooroute CollectD data toohello OMS Agent for Linux, `oms.conf` needs toobe added tooCollectD's configuration directory.</span></span> <span data-ttu-id="4a504-126">이 파일의 hello 대상 컴퓨터의 Linux 배포판 hello에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="4a504-126">hello destination of this file depends on hello Linux  distro of your machine.</span></span>

    <span data-ttu-id="4a504-127">CollectD config 디렉터리가 /etc/collectd.d/에 있는 경우:</span><span class="sxs-lookup"><span data-stu-id="4a504-127">If your CollectD config directory is located in /etc/collectd.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    <span data-ttu-id="4a504-128">CollectD config 디렉터리가 /etc/collectd/collectd.conf.d/에 있는 경우:</span><span class="sxs-lookup"><span data-stu-id="4a504-128">If your CollectD config directory is located in /etc/collectd/collectd.conf.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    ><span data-ttu-id="4a504-129">5.5 이전 CollectD 버전에 대 한 toomodify hello 태그에 있을 `oms.conf` 위와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a504-129">For CollectD versions before 5.5 you will have toomodify hello tags in `oms.conf` as shown above.</span></span>
    >

2. <span data-ttu-id="4a504-130">Collectd.conf 원하는 toohello 작업 공간의 omsagent 구성 디렉터리를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a504-130">Copy collectd.conf toohello desired workspace's omsagent configuration directory.</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. <span data-ttu-id="4a504-131">OMS 에이전트 및 CollectD Linux에 대 한 명령을 수행 하는 hello로 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a504-131">Restart CollectD and OMS Agent for Linux with hello following commands.</span></span>

    <span data-ttu-id="4a504-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span><span class="sxs-lookup"><span data-stu-id="4a504-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span></span>

## <a name="collectd-metrics-toolog-analytics-schema-conversion"></a><span data-ttu-id="4a504-133">CollectD 메트릭 tooLog 분석 스키마 변환</span><span class="sxs-lookup"><span data-stu-id="4a504-133">CollectD metrics tooLog Analytics schema conversion</span></span>
<span data-ttu-id="4a504-134">toomaintain CollectD hello 스키마 매핑은 다음을 사용 하 여 Linux 및 hello 새 메트릭 용 OMS 에이전트에 의해 이미 수집 된 인프라 메트릭 간의 친숙 한 모델 수집:</span><span class="sxs-lookup"><span data-stu-id="4a504-134">toomaintain a familiar model between infrastructure metrics already collected by OMS Agent for Linux and hello new metrics collected by CollectD hello following schema mapping is used:</span></span>

| <span data-ttu-id="4a504-135">CollectD 메트릭 필드</span><span class="sxs-lookup"><span data-stu-id="4a504-135">CollectD Metric field</span></span> | <span data-ttu-id="4a504-136">Log Analytics 필드</span><span class="sxs-lookup"><span data-stu-id="4a504-136">Log Analytics field</span></span> |
|:--|:--|
| <span data-ttu-id="4a504-137">host</span><span class="sxs-lookup"><span data-stu-id="4a504-137">host</span></span> | <span data-ttu-id="4a504-138">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="4a504-138">Computer</span></span> |
| <span data-ttu-id="4a504-139">플러그 인</span><span class="sxs-lookup"><span data-stu-id="4a504-139">plugin</span></span> | <span data-ttu-id="4a504-140">없음</span><span class="sxs-lookup"><span data-stu-id="4a504-140">None</span></span> |
| <span data-ttu-id="4a504-141">plugin_instance</span><span class="sxs-lookup"><span data-stu-id="4a504-141">plugin_instance</span></span> | <span data-ttu-id="4a504-142">인스턴스 이름</span><span class="sxs-lookup"><span data-stu-id="4a504-142">Instance Name</span></span><br><span data-ttu-id="4a504-143">**plugin_instance**가 *null*인 경우 InstanceName="*_Total*"</span><span class="sxs-lookup"><span data-stu-id="4a504-143">If **plugin_instance** is *null* then InstanceName="*_Total*"</span></span> |
| <span data-ttu-id="4a504-144">type</span><span class="sxs-lookup"><span data-stu-id="4a504-144">type</span></span> | <span data-ttu-id="4a504-145">ObjectName</span><span class="sxs-lookup"><span data-stu-id="4a504-145">ObjectName</span></span> |
| <span data-ttu-id="4a504-146">type_instance</span><span class="sxs-lookup"><span data-stu-id="4a504-146">type_instance</span></span> | <span data-ttu-id="4a504-147">CounterName</span><span class="sxs-lookup"><span data-stu-id="4a504-147">CounterName</span></span><br><span data-ttu-id="4a504-148">**type_instance**가 *null*인 경우 CounterName=**비어 있음**</span><span class="sxs-lookup"><span data-stu-id="4a504-148">If **type_instance** is *null* then CounterName=**blank**</span></span> |
| <span data-ttu-id="4a504-149">dsnames[]</span><span class="sxs-lookup"><span data-stu-id="4a504-149">dsnames[]</span></span> | <span data-ttu-id="4a504-150">CounterName</span><span class="sxs-lookup"><span data-stu-id="4a504-150">CounterName</span></span> |
| <span data-ttu-id="4a504-151">dstypes</span><span class="sxs-lookup"><span data-stu-id="4a504-151">dstypes</span></span> | <span data-ttu-id="4a504-152">없음</span><span class="sxs-lookup"><span data-stu-id="4a504-152">None</span></span> |
| <span data-ttu-id="4a504-153">값[]</span><span class="sxs-lookup"><span data-stu-id="4a504-153">values[]</span></span> | <span data-ttu-id="4a504-154">CounterValue</span><span class="sxs-lookup"><span data-stu-id="4a504-154">CounterValue</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4a504-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4a504-155">Next steps</span></span>
* <span data-ttu-id="4a504-156">에 대 한 자세한 내용은 [검색 로그](log-analytics-log-searches.md) tooanalyze hello 데이터가 데이터 원본 및 솔루션에서 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a504-156">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
* <span data-ttu-id="4a504-157">사용 하 여 [사용자 정의 필드](log-analytics-custom-fields.md) tooparse 레코드에서에서 데이터를 syslog 개별 계획을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a504-157">Use [Custom Fields](log-analytics-custom-fields.md) tooparse data from syslog records into individual fields.</span></span>

