---
title: "OMS 로그 분석에서 사용자 지정 JSON 데이터를 aaaCollecting | Microsoft Docs"
description: "Linux 용 OMS 에이전트 hello를 사용 하 여 로그 분석에 사용자 지정 JSON 데이터 소스를 수집할 수 있습니다.  이러한 사용자 지정 데이터 원본은 curl 또는 FluentD의 300+ 플러그 인의 하나와 같은 JSON을 반환하는 간단한 스크립트일 수 있습니다. 이 문서에서는이 데이터 컬렉션에 필요한 hello 구성을 설명 합니다."
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
ms.openlocfilehash: 97d401408a8c206d4a9ef2ec9b13ba1ca6b5e92b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="collecting-custom-json-data-sources-with-hello-oms-agent-for-linux-in-log-analytics"></a>로그 분석에 Linux 용 OMS 에이전트 hello로 수집 사용자 지정 JSON 데이터 소스
Linux 용 OMS 에이전트 hello를 사용 하 여 로그 분석에 사용자 지정 JSON 데이터 소스를 수집할 수 있습니다.  이러한 사용자 지정 데이터 원본은 [curl](https://curl.haxx.se/) 또는 [FluentD의 300+ 플러그 인](http://www.fluentd.org/plugins/all)의 하나와 같은 JSON을 반환하는 간단한 스크립트일 수 있습니다. 이 문서에서는이 데이터 컬렉션에 필요한 hello 구성을 설명 합니다.

> [!NOTE]
> 사용자 지정 JSON 데이터에 Linux용 OMS 에이전트 v1.1.0-217+가 필요합니다.

## <a name="configuration"></a>구성

### <a name="configure-input-plugin"></a>입력 플러그 인 구성

로그 분석에서 JSON 데이터 toocollect 추가 `oms.api.` 입력된 플러그인에서 FluentD 태그의 toohello 시작 합니다.

예를 들어 다음은 `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`에서 별도 구성 파일 `exec-json.conf`입니다.  Hello FluentD 플러그 인을 사용 하 여이 `exec` toorun curl 명령 30 초 마다.  이 명령의 출력 hello hello JSON 출력 플러그인에 의해 수집 됩니다.

```
<source>
  type exec
  command 'curl localhost/json.output'
  format json
  tag oms.api.httpresponse
  run_interval 30s
</source>

<match oms.api.httpresponse>
  type out_oms_api
  log_level info

  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms_api_httpresponse*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
```
hello 구성 파일에서 추가 `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` toohave 소유권이 다음 명령을 hello로 변경 해야 합니다.

`sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/exec-json.conf`

### <a name="configure-output-plugin"></a>출력 플러그 인 구성 
Hello 출력 플러그 인 구성 toohello 주요 구성에 따라 추가 `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` 또는 별도 구성 파일에 배치`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`

```
<match oms.api.**>
  type out_oms_api
  log_level info

  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms_api*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
```

### <a name="restart-oms-agent-for-linux"></a>Linux용 OMS 에이전트 다시 시작
다음 명령을 hello로 Linux 서비스에 대 한 hello OMS 에이전트를 다시 시작 합니다.

    sudo /opt/microsoft/omsagent/bin/service_control restart 

## <a name="output"></a>출력
hello 데이터를 수집할 로그 분석에서의 레코드 종류와 `<FLUENTD_TAG>_CL`합니다.

예를 들어, 사용자 정의 태그를 hello `tag oms.api.tomcat` 의 레코드 종류와 로그 분석에서 `tomcat_CL`합니다.  로그 검색을 수행 하는 hello로이 종류의 모든 레코드를 검색할 수 있습니다.

    Type=tomcat_CL

중첩된 JSON 데이터 원본이 지원되지만 부모 필드를 기반으로 인덱싱됩니다. Hello JSON 데이터를 다음으로 로그 분석 검색에서 반환 됩니다 예를 들어 `tag_s : "[{ "a":"1", "b":"2" }]`합니다.

```
{
    "tag": [{
        "a":"1",
        "b":"2"
    }]
}
```


## <a name="next-steps"></a>다음 단계
* 에 대 한 자세한 내용은 [검색 로그](log-analytics-log-searches.md) tooanalyze hello 데이터가 데이터 원본 및 솔루션에서 수집 합니다. 
 