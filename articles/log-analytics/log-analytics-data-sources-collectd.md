---
title: "OMS Log Analytics에서 CollectD의 데이터 수집 | Microsoft Docs"
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
ms.openlocfilehash: a63b15ca5126b45451f0694c9ee75d7b67b1ceaf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a><span data-ttu-id="b486a-104">Log Analytics에서 Linux 에이전트의 CollectD에서 데이터 수집</span><span class="sxs-lookup"><span data-stu-id="b486a-104">Collect data from CollectD on Linux agents in Log Analytics</span></span>
<span data-ttu-id="b486a-105">[CollectD](https://collectd.org/)는 주기적으로 응용 프로그램의 성능 메트릭 및 시스템 수준 정보를 수집하는 오픈 소스 Linux 디먼입니다.</span><span class="sxs-lookup"><span data-stu-id="b486a-105">[CollectD](https://collectd.org/) is an open source Linux daemon that periodically collects performance metrics from applications and system level information.</span></span> <span data-ttu-id="b486a-106">예제 응용 프로그램은 JVM(Java Virtual Machine), MySQL 서버 및 Nginx를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b486a-106">Example applications include the Java Virtual Machine (JVM), MySQL Server, and Nginx.</span></span> <span data-ttu-id="b486a-107">이 문서에서는 Log Analytics에서 CollectD의 성능 데이터 수집에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b486a-107">This article provides information on collecting performance data from CollectD in Log Analytics.</span></span>

<span data-ttu-id="b486a-108">사용 가능한 플러그 인의 전체 목록은 [플러그 인의 테이블](https://collectd.org/wiki/index.php/Table_of_Plugins)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b486a-108">A full list of available plugins can be found at [Table of Plugins](https://collectd.org/wiki/index.php/Table_of_Plugins).</span></span>

![CollectD 개요](media/log-analytics-data-sources-collectd/overview.png)

<span data-ttu-id="b486a-110">다음 CollectD 구성은 CollectD 데이터를 Linux 용 OMS 에이전트로 라우팅하도록 Linux용 OMS 에이전트에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b486a-110">The following CollectD configuration is included in the OMS Agent for Linux to route  CollectD data to the OMS Agent for Linux.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

<span data-ttu-id="b486a-111">또한 5.5 이전의 collectD 버전을 사용하는 경우 다음 구성을 대신 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b486a-111">Additionally, if using an versions of collectD before 5.5 use the following configuration instead.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

<span data-ttu-id="b486a-112">CollectD 구성은 기본값`write_http` 플러그 인을 사용하여 26000 포트를 통해 성능 메트릭 데이터를 Linux용 OMS 에이전트에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b486a-112">The CollectD configuration uses the default`write_http` plugin to send performance metric data over port 26000 to OMS Agent for Linux.</span></span> 

> [!NOTE]
> <span data-ttu-id="b486a-113">필요한 경우 이 포트는 사용자 지정 정의된 포트로 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b486a-113">This port can be configured to a custom-defined port if needed.</span></span>

<span data-ttu-id="b486a-114">또한 Linux용 OMS 에이전트는 CollectD 메트릭에 대해 26000 포트에서 수신한 다음 OMS 스키마 메트릭으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="b486a-114">The OMS Agent for Linux also listens on port 26000 for CollectD metrics and then converts them to OMS schema metrics.</span></span> <span data-ttu-id="b486a-115">다음은 Linux용 OMS 에이전트 구성 `collectd.conf`입니다.</span><span class="sxs-lookup"><span data-stu-id="b486a-115">The following is the OMS Agent for Linux configuration  `collectd.conf`.</span></span>

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a><span data-ttu-id="b486a-116">지원되는 버전</span><span class="sxs-lookup"><span data-stu-id="b486a-116">Versions supported</span></span>
- <span data-ttu-id="b486a-117">Log Analytics는 현재 CollectD 버전 4.8 이상을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b486a-117">Log Analytics currently supports CollectD version 4.8 and above.</span></span>
- <span data-ttu-id="b486a-118">CollectD 메트릭 수집에 Linux용 OMS 에이전트 v1.1.0-217 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b486a-118">OMS Agent for Linux v1.1.0-217 or above is required for CollectD metric collection.</span></span>


## <a name="configuration"></a><span data-ttu-id="b486a-119">구성</span><span class="sxs-lookup"><span data-stu-id="b486a-119">Configuration</span></span>
<span data-ttu-id="b486a-120">Log Analytics에서 CollectD 데이터의 컬렉션을 구성하는 기본 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b486a-120">The following are basic steps to configure collection of CollectD data in Log Analytics.</span></span>

1. <span data-ttu-id="b486a-121">write_http 플러그 인을 사용하여 Linux용 OMS 에이전트에 데이터를 보내도록 CollectD를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b486a-121">Configure CollectD to send data to the OMS Agent for Linux using the write_http plugin.</span></span>  
2. <span data-ttu-id="b486a-122">적절한 포트에서 CollectD 데이터에 대해 수신 대기하도록 Linux용 OMS 에이전트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b486a-122">Configure the OMS Agent for Linux to listen for the CollectD data on the appropriate port.</span></span>
3. <span data-ttu-id="b486a-123">CollectD 및 Linux용 OMS 에이전트를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b486a-123">Restart CollectD and OMS Agent for Linux.</span></span>

### <a name="configure-collectd-to-forward-data"></a><span data-ttu-id="b486a-124">데이터를 전달하도록 CollectD 구성</span><span class="sxs-lookup"><span data-stu-id="b486a-124">Configure CollectD to forward data</span></span> 

1. <span data-ttu-id="b486a-125">CollectD 데이터를 Linux용 OMS 에이전트로 라우팅하려면 `oms.conf`를 CollectD의 구성 디렉터리에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b486a-125">To route CollectD data to the OMS Agent for Linux, `oms.conf` needs to be added to CollectD's configuration directory.</span></span> <span data-ttu-id="b486a-126">이 파일의 대상은 컴퓨터의 Linux 배포판에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="b486a-126">The destination of this file depends on the Linux  distro of your machine.</span></span>

    <span data-ttu-id="b486a-127">CollectD config 디렉터리가 /etc/collectd.d/에 있는 경우:</span><span class="sxs-lookup"><span data-stu-id="b486a-127">If your CollectD config directory is located in /etc/collectd.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    <span data-ttu-id="b486a-128">CollectD config 디렉터리가 /etc/collectd/collectd.conf.d/에 있는 경우:</span><span class="sxs-lookup"><span data-stu-id="b486a-128">If your CollectD config directory is located in /etc/collectd/collectd.conf.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    ><span data-ttu-id="b486a-129">5.5 이전의 CollectD 버전의 경우 위와 같이 `oms.conf`에서 태그를 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b486a-129">For CollectD versions before 5.5 you will have to modify the tags in `oms.conf` as shown above.</span></span>
    >

2. <span data-ttu-id="b486a-130">collectd.conf를 원하는 작업 영역의 omsagent 구성 디렉터리에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b486a-130">Copy collectd.conf to the desired workspace's omsagent configuration directory.</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. <span data-ttu-id="b486a-131">다음 명령을 사용하여 CollectD 및 Linux 용 OMS 에이전트를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b486a-131">Restart CollectD and OMS Agent for Linux with the following commands.</span></span>

    <span data-ttu-id="b486a-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span><span class="sxs-lookup"><span data-stu-id="b486a-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span></span>

## <a name="collectd-metrics-to-log-analytics-schema-conversion"></a><span data-ttu-id="b486a-133">CollectD 메트릭을 Log Analytics 스키마로 변환</span><span class="sxs-lookup"><span data-stu-id="b486a-133">CollectD metrics to Log Analytics schema conversion</span></span>
<span data-ttu-id="b486a-134">Linux용 OMS 에이전트에서 이미 수집된 인프라 메트릭과 CollectD에서 수집된 새 메트릭 간에 친숙한 모델을 유지하기 위해 다음 스키마 매핑이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b486a-134">To maintain a familiar model between infrastructure metrics already collected by OMS Agent for Linux and the new metrics collected by CollectD the following schema mapping is used:</span></span>

| <span data-ttu-id="b486a-135">CollectD 메트릭 필드</span><span class="sxs-lookup"><span data-stu-id="b486a-135">CollectD Metric field</span></span> | <span data-ttu-id="b486a-136">Log Analytics 필드</span><span class="sxs-lookup"><span data-stu-id="b486a-136">Log Analytics field</span></span> |
|:--|:--|
| <span data-ttu-id="b486a-137">host</span><span class="sxs-lookup"><span data-stu-id="b486a-137">host</span></span> | <span data-ttu-id="b486a-138">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="b486a-138">Computer</span></span> |
| <span data-ttu-id="b486a-139">플러그 인</span><span class="sxs-lookup"><span data-stu-id="b486a-139">plugin</span></span> | <span data-ttu-id="b486a-140">없음</span><span class="sxs-lookup"><span data-stu-id="b486a-140">None</span></span> |
| <span data-ttu-id="b486a-141">plugin_instance</span><span class="sxs-lookup"><span data-stu-id="b486a-141">plugin_instance</span></span> | <span data-ttu-id="b486a-142">인스턴스 이름</span><span class="sxs-lookup"><span data-stu-id="b486a-142">Instance Name</span></span><br><span data-ttu-id="b486a-143">**plugin_instance**가 *null*인 경우 InstanceName="*_Total*"</span><span class="sxs-lookup"><span data-stu-id="b486a-143">If **plugin_instance** is *null* then InstanceName="*_Total*"</span></span> |
| <span data-ttu-id="b486a-144">type</span><span class="sxs-lookup"><span data-stu-id="b486a-144">type</span></span> | <span data-ttu-id="b486a-145">ObjectName</span><span class="sxs-lookup"><span data-stu-id="b486a-145">ObjectName</span></span> |
| <span data-ttu-id="b486a-146">type_instance</span><span class="sxs-lookup"><span data-stu-id="b486a-146">type_instance</span></span> | <span data-ttu-id="b486a-147">CounterName</span><span class="sxs-lookup"><span data-stu-id="b486a-147">CounterName</span></span><br><span data-ttu-id="b486a-148">**type_instance**가 *null*인 경우 CounterName=**비어 있음**</span><span class="sxs-lookup"><span data-stu-id="b486a-148">If **type_instance** is *null* then CounterName=**blank**</span></span> |
| <span data-ttu-id="b486a-149">dsnames[]</span><span class="sxs-lookup"><span data-stu-id="b486a-149">dsnames[]</span></span> | <span data-ttu-id="b486a-150">CounterName</span><span class="sxs-lookup"><span data-stu-id="b486a-150">CounterName</span></span> |
| <span data-ttu-id="b486a-151">dstypes</span><span class="sxs-lookup"><span data-stu-id="b486a-151">dstypes</span></span> | <span data-ttu-id="b486a-152">없음</span><span class="sxs-lookup"><span data-stu-id="b486a-152">None</span></span> |
| <span data-ttu-id="b486a-153">값[]</span><span class="sxs-lookup"><span data-stu-id="b486a-153">values[]</span></span> | <span data-ttu-id="b486a-154">CounterValue</span><span class="sxs-lookup"><span data-stu-id="b486a-154">CounterValue</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b486a-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b486a-155">Next steps</span></span>
* <span data-ttu-id="b486a-156">데이터 원본 및 솔루션에서 수집한 데이터를 분석하기 위해 [로그 검색](log-analytics-log-searches.md) 에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b486a-156">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
* <span data-ttu-id="b486a-157">[사용자 지정 필드](log-analytics-custom-fields.md) 를 사용하여 syslog 레코드의 데이터를 개별 필드로 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="b486a-157">Use [Custom Fields](log-analytics-custom-fields.md) to parse data from syslog records into individual fields.</span></span>

