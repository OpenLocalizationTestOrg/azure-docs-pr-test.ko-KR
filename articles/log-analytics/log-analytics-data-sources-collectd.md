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
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a>Log Analytics에서 Linux 에이전트의 CollectD에서 데이터 수집
[CollectD](https://collectd.org/)는 주기적으로 응용 프로그램의 성능 메트릭 및 시스템 수준 정보를 수집하는 오픈 소스 Linux 디먼입니다. 예제 응용 프로그램에는 가상 컴퓨터 JVM (Java) hello, MySQL Server 및 Nginx 포함 됩니다. 이 문서에서는 Log Analytics에서 CollectD의 성능 데이터 수집에 대한 정보를 제공합니다.

사용 가능한 플러그 인의 전체 목록은 [플러그 인의 테이블](https://collectd.org/wiki/index.php/Table_of_Plugins)에서 찾을 수 있습니다.

![CollectD 개요](media/log-analytics-data-sources-collectd/overview.png)

hello 다음 CollectD 구성에에서 포함 된 Linux tooroute CollectD 데이터 toohello OMS 에이전트에 대 한 OMS 에이전트 hello Linux.

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

또한 같은 구성이 대신 hello를 사용 하는 5.5 전에 collectD의 버전을 사용 하는 경우.

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

hello CollectD 구성은 hello 기본값을 사용 하 여`write_http` 포트 26000 tooOMS Linux 용 에이전트를 통해 플러그 인 toosend 성능 메트릭 데이터입니다. 

> [!NOTE]
> 필요한 경우이 포트에서 구성 된 tooa 정의 된 사용자 지정 포트를 수 있습니다.

Linux 용 OMS 에이전트 hello 26000 CollectD 메트릭에 대 한 포트에서 수신 및 다음 tooOMS 스키마 메트릭을 변환 합니다. hello 다음은 Linux 구성에 대 한 OMS 에이전트 hello `collectd.conf`합니다.

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a>지원되는 버전
- Log Analytics는 현재 CollectD 버전 4.8 이상을 지원합니다.
- CollectD 메트릭 수집에 Linux용 OMS 에이전트 v1.1.0-217 이상이 필요합니다.


## <a name="configuration"></a>구성
hello 다음은 로그 분석에 CollectD 데이터의 기본 단계 tooconfigure 컬렉션입니다.

1. Hello write_http 플러그 인을 사용 하 여 Linux 용 OMS 에이전트 CollectD toosend 데이터 toohello를 구성 합니다.  
2. Hello 적절 한 포트에 hello CollectD 데이터에 대 한 Linux toolisten에 대 한 hello OMS 에이전트를 구성 합니다.
3. CollectD 및 Linux용 OMS 에이전트를 다시 시작합니다.

### <a name="configure-collectd-tooforward-data"></a>CollectD tooforward 데이터 구성 

1. Linux 용 OMS 에이전트 tooroute CollectD 데이터 toohello `oms.conf` 요구 toobe tooCollectD의 구성 디렉터리를 추가 합니다. 이 파일의 hello 대상 컴퓨터의 Linux 배포판 hello에 따라 달라 집니다.

    CollectD config 디렉터리가 /etc/collectd.d/에 있는 경우:

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    CollectD config 디렉터리가 /etc/collectd/collectd.conf.d/에 있는 경우:

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    >5.5 이전 CollectD 버전에 대 한 toomodify hello 태그에 있을 `oms.conf` 위와 같이 합니다.
    >

2. Collectd.conf 원하는 toohello 작업 공간의 omsagent 구성 디렉터리를 복사 합니다.

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. OMS 에이전트 및 CollectD Linux에 대 한 명령을 수행 하는 hello로 다시 시작 합니다.

    sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart

## <a name="collectd-metrics-toolog-analytics-schema-conversion"></a>CollectD 메트릭 tooLog 분석 스키마 변환
toomaintain CollectD hello 스키마 매핑은 다음을 사용 하 여 Linux 및 hello 새 메트릭 용 OMS 에이전트에 의해 이미 수집 된 인프라 메트릭 간의 친숙 한 모델 수집:

| CollectD 메트릭 필드 | Log Analytics 필드 |
|:--|:--|
| host | 컴퓨터 |
| 플러그 인 | 없음 |
| plugin_instance | 인스턴스 이름<br>**plugin_instance**가 *null*인 경우 InstanceName="*_Total*" |
| type | ObjectName |
| type_instance | CounterName<br>**type_instance**가 *null*인 경우 CounterName=**비어 있음** |
| dsnames[] | CounterName |
| dstypes | 없음 |
| 값[] | CounterValue |

## <a name="next-steps"></a>다음 단계
* 에 대 한 자세한 내용은 [검색 로그](log-analytics-log-searches.md) tooanalyze hello 데이터가 데이터 원본 및 솔루션에서 수집 합니다. 
* 사용 하 여 [사용자 정의 필드](log-analytics-custom-fields.md) tooparse 레코드에서에서 데이터를 syslog 개별 계획을 선택 합니다.

