---
title: "Azure 네트워크 감시자 NSG 흐름 aaaVisualize 오픈 소스 도구를 사용 하 여 로그 | Microsoft Docs"
description: "이 페이지에서는 toouse 소스 도구 toovisualize NSG 흐름 로그 열기 하는 방법을 설명 합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e9b2dcad-4da4-4d6b-aee2-6d0afade0cb8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 47cb529d4a1e00e8c4c0fa6885cbf72aed3e74c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-azure-network-watcher-nsg-flow-logs-using-open-source-tools"></a>오픈 소스 도구를 사용하여 Azure Network Watcher NSG 흐름 로그 시각화

네트워크 보안 그룹 흐름 로그는 네트워크 보안 그룹의 송/수신 IP 트래픽을 이해하는 데 사용할 수 있는 정보를 제공합니다. 이러한 흐름 로그 아웃 바운드 나타나며 당 규칙 별로 인바운드 흐름 hello NIC hello 흐름 hello 흐름 (소스/대상 IP, 소스/대상 포트, 프로토콜) 및 hello 트래픽을 허용 또는 거부 된 경우에 대 한 5 튜플 정보에 적용 됩니다.

이러한 흐름 로그 어려운 toomanually 구문 분석 되며 로부터 이해를 넓힐 수 있습니다. 그러나 이 데이터를 시각화하는 데 도움이 되는 오픈 소스 도구가 몇 가지 있습니다. 이 문서 솔루션 toovisualize tooquickly 인덱스를 사용 하면 되며 프로그램 흐름 로그 Kibana 대시보드에서 시각화를 탄력적 스택 hello를 사용 하 여 이러한 로그를 제공 합니다.

## <a name="scenario"></a>시나리오

이 문서에서는 탄력적 스택 hello를 사용 하 여 toovisualize 네트워크 보안 그룹 흐름 로그 수 있는 솔루션을 설정 합니다.  Logstash 입력된 플러그 인 hello 흐름 로그가 들어 있는 대해 구성 된 hello 저장소 blob에서 직접 hello 흐름 로그를 가져옵니다. 탄력적 스택 hello를 사용 하 여 hello 흐름 로그 인덱싱됩니다 이동한 toocreate Kibana 대시보드 toovisualize hello 정보를 사용 합니다.

![시나리오][scenario]

## <a name="steps"></a>단계

### <a name="enable-network-security-group-flow-logging"></a>네트워크 보안 그룹 흐름 로그 사용
이 시나리오에서는 계정에 있는 하나 이상의 네트워크 보안 그룹에서 네트워크 보안 그룹 흐름 로깅을 사용하도록 설정해야 합니다. 네트워크 보안 흐름 로그 설정에 대 한 자세한 내용은 다음 문서 toohello 참조 [네트워크 보안 그룹에 대 한 소개 tooflow 로깅을](network-watcher-nsg-flow-logging-overview.md)합니다.


### <a name="set-up-hello-elastic-stack"></a>탄력적 스택 hello 설정
NSG를 연결 하 여 흐름 탄력적 스택 hello 사용 하 여 로그를 우리 수 Kibana 대시보드 toosearch 수 있습니다, 그래프, 분석, 만들고이 우리의 로그에서 정보를 파생 합니다.

#### <a name="install-elasticsearch"></a>Elasticsearch 설치

1. hello 탄력적 스택 버전 5.0 이상과 Java 8 필요합니다. Hello 명령을 실행 `java -version` toocheck 버전입니다. 설치에 toodocumentation를 참조 하세요 java 있는지 [Oracle의 웹 사이트](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)
1. 시스템에 대 한 hello 올바른 이진 패키지를 다운로드 합니다.

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    다른 설치 방법은 [Elasticsearch 설치](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)에서 확인할 수 있습니다.

1. Elasticsearch hello 명령을 사용 하 여 실행 되 고 있는지 확인 합니다.

    ```
    curl http://127.0.0.1:9200
    ```

    응답 비슷한 toothis를 나타나야 합니다.

    ```
    {
    "name" : "Angela Del Toro",
    "cluster_name" : "elasticsearch",
    "version" : {
        "number" : "5.2.0",
        "build_hash" : "8ff36d139e16f8720f2947ef62c8167a888992fe",
        "build_timestamp" : "2016-01-27T13:32:39Z",
        "build_snapshot" : false,
        "lucene_version" : "6.1.0"
    },
    "tagline" : "You Know, for Search"
    }
    ```

에 대 한 자세한 지침은 설치 탄력적 검색, toohello 페이지 참조 [설치](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)

### <a name="install-logstash"></a>Logstash 설치

1. tooinstall Logstash hello 다음 명령을 실행 합니다.

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. 다음 tooconfigure Logstash tooaccess 필요 하 고 hello 흐름 로그를 구문 분석 합니다. 다음을 사용하여 logstash.conf 파일을 만듭니다.

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. 다음 콘텐츠 toohello 파일 hello를 추가 합니다.

  ```
    input {
      azureblob
        {
            storage_account_name => "mystorageaccount"
            storage_access_key => "storageaccesskey"
            container => "nsgflowlogContainerName"
            codec => "json"
        }
      }

      filter {
        split { field => "[records]" }
        split { field => "[records][properties][flows]"}
        split { field => "[records][properties][flows][flows]"}
        split { field => "[records][properties][flows][flows][flowTuples]"}

     mutate{
      split => { "[records][resourceId]" => "/"}
      add_field => {"Subscription" => "%{[records][resourceId][2]}"
                    "ResourceGroup" => "%{[records][resourceId][4]}"
                    "NetworkSecurityGroup" => "%{[records][resourceId][8]}"}
      convert => {"Subscription" => "string"}
      convert => {"ResourceGroup" => "string"}
      convert => {"NetworkSecurityGroup" => "string"}
      split => { "[records][properties][flows][flows][flowTuples]" => ","}
      add_field => {
                  "unixtimestamp" => "%{[records][properties][flows][flows][flowTuples][0]}"
                  "srcIp" => "%{[records][properties][flows][flows][flowTuples][1]}"
                  "destIp" => "%{[records][properties][flows][flows][flowTuples][2]}"
                  "srcPort" => "%{[records][properties][flows][flows][flowTuples][3]}"
                  "destPort" => "%{[records][properties][flows][flows][flowTuples][4]}"
                  "protocol" => "%{[records][properties][flows][flows][flowTuples][5]}"
                  "trafficflow" => "%{[records][properties][flows][flows][flowTuples][6]}"
                  "traffic" => "%{[records][properties][flows][flows][flowTuples][7]}"
                   }
      convert => {"unixtimestamp" => "integer"}
      convert => {"srcPort" => "integer"}
      convert => {"destPort" => "integer"}        
     }

     date{
       match => ["unixtimestamp" , "UNIX"]
     }
    }

    output {
      stdout { codec => rubydebug }
      elasticsearch {
        hosts => "localhost"
        index => "nsg-flow-logs"
      }
    }  

  ```

Logstash를 설치 하는 방법에 자세한 내용은 참조 toohello [공식 설명서](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)

### <a name="install-hello-logstash-input-plugin-for-azure-blob-storage"></a>Azure blob 저장소에 대 한 hello Logstash 입력된 플러그인을 설치 합니다.

이 Logstash 플러그 인을 사용 하면 자신의 지정 된 저장소 계정에서 toodirectly 액세스 hello 흐름 로그 있습니다. tooinstall이 플러그이 인 (에서이 사례 /usr/share/logstash/bin) hello 기본 Logstash 설치 디렉터리에서 hello 명령을 실행 합니다.

```
logstash-plugin install logstash-input-azureblob
```

toostart Logstash hello 명령을 실행 합니다.

```
sudo /etc/init.d/logstash start
```

이 플러그 인에 대 한 자세한 내용은 참조 toodocumentation [여기](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)

### <a name="install-kibana"></a>Kibana 설치

1. 다음 명령을 tooinstall Kibana hello를 실행 합니다.

  ```
  curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
  tar xzvf kibana-5.2.0-linux-x86_64.tar.gz
  ```

1. toorun Kibana hello 명령을 사용 합니다.

  ```
  cd kibana-5.2.0-linux-x86_64/
  ./bin/kibana
  ```

1. tooview Kibana 웹 인터페이스를 너무 이동`http://localhost:5601`
1. 이 시나리오에 대 한 hello 인덱스 hello 흐름 로그에 사용 되는 방법은 "nsg 흐름 로그"입니다. Hello 인덱스 패턴 logstash.conf 파일의 hello "output" 섹션에 변경할 수 있습니다.

1. Tooview hello Kibana 대시보드를 원격으로 원하는 경우 만들 너무 액세스를 허용 하는 인바운드 NSG 규칙**5601 포트**합니다.

### <a name="create-a-kibana-dashboard"></a>Kibana 대시보드 만들기

이 문서에 대 한 있습니다 tooview 추세에 대 한 샘플 대시보드 및 경고의 세부 사항을 제공 합니다.

![그림 1][1]

1. Hello 대시보드 파일을 다운로드 [여기](https://aka.ms/networkwatchernsgflowlogdashboard), hello 시각화 파일 [여기](https://aka.ms/networkwatchernsgflowlogvisualizations), 및 저장 하는 hello 검색 파일 [여기](https://aka.ms/networkwatchernsgflowlogsearch)합니다.

1. Hello에서 **관리** 탭 Kibana의 이동 너무**개체 저장** 세 개 파일을 가져옵니다. Hello 다음 **대시보드** 열면 탭 및 부하 hello 샘플 대시보드 합니다.

사용자가 관심 있는 메트릭에 맞는 시각화 및 대시보드를 만들 수 있습니다. Kibana의 [공식적인 설명서](https://www.elastic.co/guide/en/kibana/current/visualize.html)에서 Kibana 시각화 만들기에 대해 자세히 알아보세요.

### <a name="visualize-nsg-flow-logs"></a>NSG 흐름 로그 시각화

hello 샘플 대시보드는 hello 흐름 로그의 몇 가지 시각화를 제공합니다.

1. 시간 시계열 그래프 기간 hello를 통해 흐름 hello 수를 표시 하 여 의사 결정/방향 시간에 따른-이동 합니다. 시간 단위 hello와 이러한 시각화 요소 범위를 편집할 수 있습니다. 의사 결정 hello 비율을 표시 하 여 흐름을 허용 하거나 인바운드 및 아웃 바운드 트래픽의 방향은 표시 hello 비율로 흐름 하는 동안 이루어진 결정을 거부 합니다. 이러한 시각 효과를 사용하면 시간에 따른 트래픽 추세를 검토할 수 있고 스파이크 또는 비정상 패턴을 찾을 수 있습니다.

  ![figure2][2]

1. 원형 차트의 흐름 hello 분석 tootheir 해당 포트를 보여 주는 – 대상/원본 포트에 의해 전달 됩니다. 이 보기를 사용하면 가장 자주 사용되는 포트를 볼 수 있습니다. Hello 원형 차트 내에서 특정 포트를 클릭 하면 해당 포트의 tooflows 아래로 hello 대시보드 hello 나머지 필터링 합니다.

  ![figure3][3]

1. 흐름 및 가장 빠른 로그 시간 – 흐름 hello 수를 기록 하 고 hello 가장 빠른 로그의 hello 날짜 캡처된를 표시 하는 메트릭 수입니다.

  ![figure4][4]

1. NSG 및 규칙 – 내 각 NSG에서 규칙의 hello 배포 뿐만 아니라 각 NSG 내에서 흐름의 hello 분포를 표시 하는 막대 그래프에서 흐름. 생성 된 규칙에는 대부분의 트래픽을 hello 및 여기에서 어떤 NSG를 확인할 수 있습니다.

  ![figure5][5]

1. 상위 10 개의 원본/대상 Ip-hello 상위 10 개의 원본 및 대상 Ip 보여 주는 가로 막대형 차트입니다. 이러한 차트 tooshow 보다 상위 Ip을 조정할 수 있습니다. 여기에서 있습니다 수 Ip 가장 일반적으로 발생 하는 hello로 볼 트래픽 의사 결정 hello (허용 또는 거부) 각 IP 방향으로 수행 합니다.

  ![figure6][6]

1. 흐름 튜플 – 다음이 표에 나와 있습니다 hello 각 흐름 튜플을 뿐만 아니라 해당 NGS 및 규칙에 포함 된 정보입니다.

  ![figure7][7]

쿼리 표시줄 hello를 사용 하 여 hello hello 대시보드 위쪽에, 구독 ID, 리소스 그룹, 규칙 또는 관심 있는 다른 모든 변수의 같은 hello 흐름의 모든 매개 변수에 따라 hello 대시보드를 필터링 할 수 있습니다. Kibana의 쿼리 및 필터에 대 한 자세한 참조 toohello [공식 설명서](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)

## <a name="conclusion"></a>결론

탄력적 스택 hello로 hello 네트워크 보안 그룹 흐름 로그를 결합 하 여 우리 발견 했을 강력 하 고 사용자 지정할 수 있는 방법 toovisualize와 우리의 네트워크 트래픽을 합니다. 이러한 대시보드 tooquickly 증가 허용 되어 아래로 필터 뿐만 네트워크 트래픽을 대 한 통찰력을 공유 하 고 비정상 모든 잠재적인 문제를 조사 합니다. Kibana를 사용 하 여 이러한 대시보드 조정 하 고 특정 시각화 toomeet의 모든 보안, 감사 및 준수 요구를 만들 수 있습니다.

## <a name="next-steps"></a>다음 단계

Toovisualize NSG 흐름 기록 하는 방법을 Power BI를 방문 하 여 자세한 [NSG 시각화할 Power BI를 사용 하 여 로그 전달](network-watcher-visualize-nsg-flow-logs-power-bi.md)


<!--Image references-->

[scenario]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/scenario.png
[1]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure7.png
