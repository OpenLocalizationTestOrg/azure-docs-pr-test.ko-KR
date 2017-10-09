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
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a>Linux용 OMS 에이전트에서 Log Analytics에 Nagios 및 Zabbix의 경고 수집 
[Nagios](https://www.nagios.org/) 및 [Zabbix](http://www.zabbix.com/)는 오픈 소스 모니터링 도구입니다.  있습니다 수 수집에서 경고를 이러한 도구의 로그 분석에 순서 tooanalyze와 함께 해당 [다른 소스에서 경고](log-analytics-alerts.md)합니다.  이 문서에서는 이러한 시스템에서 tooconfigure hello OMS 에이전트에 대 한 Linux toocollect 경고 하는 방법을 설명 합니다.
 
## <a name="configure-alert-collection"></a>경고 수집 구성

### <a name="configuring-nagios-alert-collection"></a>Nagios 경고 수집 구성
Hello hello Nagios 서버 toocollect 경고에 대해 다음 단계를 수행 합니다.

1. Grant hello 사용자 **omsagent** 읽기 권한을 toohello Nagios 로그 파일 (예: `/var/log/nagios/nagios.log`). Hello 그룹 hello nagios.log 파일을 소유 하는 것으로 가정 `nagios`, hello 사용자를 추가할 수 있습니다 **omsagent** toohello **nagios** 그룹입니다. 

    sudo usermod -a -G nagios omsagent

2.  Hello 구성 파일 수정 (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`). 충족 했는지 확인 hello 다음 항목이 있고 주석으로 하지 않습니다.  

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

3. Hello omsagent 디먼을 다시 시작

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a>Zabbix 경고 수집 구성
Zabbix 서버에서 경고 toocollect 해야 toospecify 사용자와 암호를 *일반 텍스트*합니다. 이 적절 하지만 hello 사용자를 만들고 toomonitor onlu 사용 권한을 부여 하는 것이 좋습니다.

Hello hello Nagios 서버 toocollect 경고에 대해 다음 단계를 수행 합니다.

1. Hello 구성 파일 수정 (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`). 항목을 다음 hello가 있고 하지 주석으로 처리를 확인 합니다.  Zabbix 환경에 대 한 hello 사용자 이름 및 암호 toovalues를 변경 합니다.

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. Hello omsagent 디먼을 다시 시작

    sudo sh /opt/microsoft/omsagent/bin/service_control restart


## <a name="alert-records"></a>경고 레코드
Log Analytics에서 [로그 검색](log-analytics-log-searches.md)을 사용하여 Nagios 및 Zabbix에서 경고 레코드를 검색할 수 있습니다.

### <a name="nagios-alert-records"></a>Nagios 경고 레코드

Nagios에서 수집된 경고는 **경고**의 **형식** 및 **Nagios**의 **SourceSystem**을 가집니다.  다음 표에 hello에 hello 속성을 갖게 됩니다.

| 속성 | 설명 |
|:--- |:--- |
| 형식 |*경고* |
| SourceSystem |*Nagios* |
| AlertName |Hello 경고의 이름입니다. |
| AlertDescription | Hello 경고의 설명입니다. |
| AlertState | Hello 서비스 또는 호스트의 상태입니다.<br><br>확인<br>경고<br>위로<br>아래로 |
| HostName | Hello 경고를 생성 하는 hello 호스트의 이름입니다. |
| PriorityNumber | Hello 경고의 우선 순위 수준입니다. |
| StateType | hello 형식 hello 경고의 상태입니다.<br><br>소프트 - 다시 확인되지 않은 문제입니다.<br>하드 - 특정 횟수를 다시 확인한 문제입니다.  |
| TimeGenerated |날짜 및 시간 hello 경고가 생성 되었습니다. |


### <a name="zabbix-alert-records"></a>Zabbix 경고 레코드
Zabbix에서 수집된 경고는 **경고**의 **형식** 및 **Zabbix**의 **SourceSystem**을 가집니다.  다음 표에 hello에 hello 속성을 갖게 됩니다.

| 속성 | 설명 |
|:--- |:--- |
| 형식 |*경고* |
| SourceSystem |*Zabbix* |
| AlertName | Hello 경고의 이름입니다. |
| AlertPriority | Hello 경고의 심각도입니다.<br><br>분류되지 않음<br>정보<br>Warning<br>average<br>높음<br>심각  |
| AlertState | Hello 경고의 상태입니다.<br><br>0-toodate를 상태가입니다.<br>1 - 상태를 알 수 없습니다.  |
| AlertTypeNumber | 경고가 여러 문제 이벤트를 생성할 수 있는지 여부를 지정합니다.<br><br>0-toodate를 상태가입니다.<br>1 - 상태를 알 수 없습니다.    |
| 설명 | 경고에 대한 추가 설명입니다. |
| HostName | Hello 경고를 생성 하는 hello 호스트의 이름입니다. |
| PriorityNumber | Hello 경고의 심각도 나타내는 값입니다.<br><br>0 - 분류되지 않음<br>1 - 정보<br>2 - 경고<br>3 - 평균<br>4 - 높음<br>5 - 심각 |
| TimeGenerated |날짜 및 시간 hello 경고가 생성 되었습니다. |
| TimeLastModified |Hello 경고의 날짜 및 시간 hello 상태 마지막 변경 되었습니다. |


## <a name="next-steps"></a>다음 단계
* Log Analytics에서 [경고](log-analytics-alerts.md)에 대해 알아봅니다.
* 에 대 한 자세한 내용은 [검색 로그](log-analytics-log-searches.md) tooanalyze hello 데이터가 데이터 원본 및 솔루션에서 수집 합니다. 
