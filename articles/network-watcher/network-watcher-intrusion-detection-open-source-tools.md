---
title: "Azure 네트워크 감시자 오픈 소스 도구와 aaaPerform 네트워크 침입 감지 | Microsoft Docs"
description: "이 문서에서는 Azure 네트워크 감시자 toouse 및 오픈 소스 도구 tooperform 네트워크 침입 감지에 어떻게 설명"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0f043f08-19e1-4125-98b0-3e335ba69681
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b5a909b827ab32ad6b2fd8e2911a944fd940249e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="perform-network-intrusion-detection-with-network-watcher-and-open-source-tools"></a>Network Watcher 및 오픈 소스 도구를 사용하여 네트워크 침입 검색 수행

패킷 캡처는 네트워크 IDS(침입 검색 시스템)를 구현하고 NSM(네트워크 보안 모니터링)을 수행하기 위한 핵심 구성 요소입니다. 패킷 캡처를 처리하고 가능한 네트워크 침입 및 악의적인 활동의 서명을 찾기 위한 여러 가지 오픈 소스 IDS 도구가 있습니다. 네트워크 감시자에서 제공 하는 hello 패킷 캡처를 사용 하 여 유해한 침입 또는 취약성에 대해 네트워크를 분석할 수 있습니다.

이러한 한 오픈 소스 도구 Suricata, ruleset toomonitor 네트워크 트래픽을 사용 하 고 의심 스러운 이벤트가 발생할 때마다 경고를 트리거합니다 하는 ID 엔진입니다. Suricata는 멀티스레드 엔진을 제공하므로 빨라진 속도 및 효율성으로 네트워크 트래픽 분석을 수행할 수 있습니다. Suricata 및 해당 기능에 대한 자세한 내용은 https://suricata-ids.org/ 웹 사이트를 참조하세요.

## <a name="scenario"></a>시나리오

환경 tooperform tooset 네트워크 네트워크 감시자를 Suricata를 사용 하 여 침입 검색 방법과 탄력적 스택 hello이 문서에 설명 합니다. 네트워크 감시자 사용 되는 tooperform 네트워크 침입 감지를 캡처하여 hello 패킷과 함께 있습니다를 제공 합니다. Suricata 프로세스 hello 패킷 캡처하고 트리거 경고 위협의 지정 된 규칙 집합을 일치 하는 패킷을 기반으로 합니다. 이러한 경고는 로컬 컴퓨터의 로그 파일에 저장됩니다. 탄력적 스택 hello를 사용 하 여 Suricata에서 생성 된 hello 로그 인덱싱할 수 및 toocreate hello 로그의 시각적 표현을는 수단 tooquickly 이득 insights toopotential 네트워크 취약점을 갖출 Kibana 대시보드를 사용 합니다.  

![간단한 웹 응용 프로그램 시나리오][1]

두 오픈 소스 도구를 설정할 수 있습니다는 Azure VM에서 tooperform 있도록 자신의 Azure 네트워크 환경 내에서 이러한 분석 합니다.

## <a name="steps"></a>단계

### <a name="install-suricata"></a>Suricata 설치

설치의 다른 모든 방법은 http://suricata.readthedocs.io/en/latest/install.html을 참조하세요.

1. VM의 hello 명령줄 터미널 hello 다음 명령을 실행 합니다.

    ```
    sudo add-apt-repository ppa:oisf/suricata-stable
    sudo apt-get update
    sudo sudo apt-get install suricata
    ```

1. tooverify hello 명령을 실행 하 여 설치 `suricata -h` toosee hello 전체 명령 목록을 합니다.

### <a name="download-hello-emerging-threats-ruleset"></a>Hello 위협 발생 하 고 규칙 집합 다운로드

이 단계에서는 없어 Suricata toorun에 대 한 모든 규칙. Toodetect, 원하는 특정 위협 tooyour 네트워크 또는 다양 한 발생 하 고 위협 또는 VRT 규칙 Snort에서 같은 공급자에서에서 사용 하 여 개발 된 규칙 집합을 수도 있습니다 하는 경우 사용자 고유의 규칙을 만들 수 있습니다. 여기 hello 자유롭게 액세스할 수 있는 위협 발생 하 고 규칙 집합에서 사용:

Hello 규칙 집합을 다운로드 하 여 hello 디렉터리에 복사 합니다.

```
wget http://rules.emergingthreats.net/open/suricata/emerging.rules.tar.gz
tar zxf emerging.rules.tar.gz
sudo cp -r rules /etc/suricata/
```

### <a name="process-packet-captures-with-suricata"></a>Suricata로 패킷 캡처 처리

tooprocess 패킷 hello 다음 명령을 실행 Suricata를 사용 하 여 캡처합니다.

```
sudo suricata -c /etc/suricata/suricata.yaml -r <location_of_pcapfile>
```
hello fast.log 파일을 읽을 toocheck hello 결과 알림:
```
tail -f /var/log/suricata/fast.log
```

### <a name="set-up-hello-elastic-stack"></a>탄력적 스택 hello 설정

Hello 로그 Suricata 생성 하는 네트워크에서 발생 한 상황에 대 한 중요 한 정보를 포함, 이러한 로그 파일 hello 쉬운 tooread 되지 하 고 이해 합니다. Suricata 탄력적 스택 hello를 연결 하 여 우리 수 Kibana 대시보드 toosearch 수 있습니다, 그리고 그래프, 분석, 만들고 insights는 로그에서 파생 합니다.

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
1. 그런 다음 tooconfigure Logstash tooread eve.json 파일의 hello 출력에서 필요합니다. 다음을 사용하여 logstash.conf 파일을 만듭니다.

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. 다음 콘텐츠 toohello 파일 hello 추가 (hello 경로 toohello eve.json 파일이 올바른지 확인):

    ```ruby
    input {
    file {
        path => ["/var/log/suricata/eve.json"]
        codec =>  "json"
        type => "SuricataIDPS"
    }

    }

    filter {
    if [type] == "SuricataIDPS" {
        date {
        match => [ "timestamp", "ISO8601" ]
        }
        ruby {
        code => "
            if event.get('[event_type]') == 'fileinfo'
            event.set('[fileinfo][type]', event.get('[fileinfo][magic]').to_s.split(',')[0])
            end
        "
        }

        ruby{
        code => "
            if event.get('[event_type]') == 'alert'
            sp = event.get('[alert][signature]').to_s.split(' group ')
            if (sp.length == 2) and /\A\d+\z/.match(sp[1])
                event.set('[alert][signature]', sp[0])
            end
            end
            "
        }
    }

    if [src_ip]  {
        geoip {
        source => "src_ip"
        target => "geoip"
        #database => "/opt/logstash/vendor/geoip/GeoLiteCity.dat"
        add_field => [ "[geoip][coordinates]", "%{[geoip][longitude]}" ]
        add_field => [ "[geoip][coordinates]", "%{[geoip][latitude]}"  ]
        }
        mutate {
        convert => [ "[geoip][coordinates]", "float" ]
        }
        if ![geoip.ip] {
        if [dest_ip]  {
            geoip {
            source => "dest_ip"
            target => "geoip"
            #database => "/opt/logstash/vendor/geoip/GeoLiteCity.dat"
            add_field => [ "[geoip][coordinates]", "%{[geoip][longitude]}" ]
            add_field => [ "[geoip][coordinates]", "%{[geoip][latitude]}"  ]
            }
            mutate {
            convert => [ "[geoip][coordinates]", "float" ]
            }
        }
        }
    }
    }

    output {
    elasticsearch {
        hosts => "localhost"
    }
    }
    ```

1. Logstash hello 파일을 수집할 수 있도록 있는지 toogive hello 올바른 사용 권한이 toohello eve.json 파일을 확인 합니다.
    
    ```
    sudo chmod 775 /var/log/suricata/eve.json
    ```

1. toostart Logstash hello 명령을 실행 합니다.

    ```
    sudo /etc/init.d/logstash start
    ```

Logstash를 설치 하는 방법에 자세한 내용은 참조 toohello [공식 설명서](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)

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
1. 이 시나리오에 대 한 hello Suricata 로그에 사용 되는 hello 인덱스 패턴은 "logstash-*"

1. Tooview hello Kibana 대시보드를 원격으로 원하는 경우 만들 너무 액세스를 허용 하는 인바운드 NSG 규칙**5601 포트**합니다.

### <a name="create-a-kibana-dashboard"></a>Kibana 대시보드 만들기

이 문서에 대 한 있습니다 tooview 추세에 대 한 샘플 대시보드 및 경고의 세부 사항을 제공 합니다.

1. Hello 대시보드 파일을 다운로드 [여기](https://aka.ms/networkwatchersuricatadashboard), hello 시각화 파일 [여기](https://aka.ms/networkwatchersuricatavisualization), 및 저장 하는 hello 검색 파일 [여기](https://aka.ms/networkwatchersuricatasavedsearch)합니다.

1. Hello에서 **관리** 탭 Kibana의 이동 너무**개체 저장** 세 개 파일을 가져옵니다. Hello 다음 **대시보드** 열면 탭 및 부하 hello 샘플 대시보드 합니다.

사용자가 관심 있는 메트릭에 맞는 시각화 및 대시보드를 만들 수 있습니다. Kibana의 [공식적인 설명서](https://www.elastic.co/guide/en/kibana/current/visualize.html)에서 Kibana 시각화 만들기에 대해 자세히 알아보세요.

![Kibana 대시보드][2]

### <a name="visualize-ids-alert-logs"></a>IDS 경고 로그 시각화

hello 샘플 대시보드는 hello Suricata 경고 로그의 몇 가지 시각화를 제공합니다.

1. GeoIP – 원본 (결정에 따라 IP)는 지리적 위치에 따라 해당 국가 hello 분포를 보여 주는 지도 별 경고

    ![지역 ip][3]

1. 상위 10 개의 경고 – hello 10 가장 자주 트리거되 경고의 요약이 그 설명을 보고 합니다. 개별 경고를 클릭 하면 toothat 특정 경고와 관련 된 hello 대시보드 toohello 정보를 필터링 합니다.

    ![이미지 4][4]

1. 경고-수 hello hello 규칙 집합에 의해 트리거되는 경고의 총 수

    ![이미지 5][5]

1. 상위 20 소스/대상 Ip/포트-을 보여 주는 원형 차트는 상위 Ip 20 개 hello 및 경고 하는 포트에서 트리거 되었습니다. 개수와 특정 Ip/포트 toosee 아래로 필터링 할 수 있습니다 알림의 종류 트리거되는 중입니다.

    ![이미지 6][6]

1. 경고 요약 – 각 개별 경고의 구체적인 세부 정보를 요약하여 보여주는 표입니다. 이 테이블 tooshow 각 경고에 대 한 관심 있는 다른 매개 변수를 지정할 수 있습니다.

    ![이미지 7][7]

사용자 지정 시각화 및 대시보드 만들기에 대한 자세한 내용은 [Kibana의 공식적인 설명서](https://www.elastic.co/guide/en/kibana/current/introduction.html)를 참조하세요.

## <a name="conclusion"></a>결론

Network Watcher에서 제공하는 패킷 캡처와 Suricata와 같은 오픈 소스 IDS 도구를 결합하여 광범위한 위협에 대해 네트워크 침입 검색을 수행할 수 있습니다. 이러한 대시보드 있습니다 tooquickly 동향 및 비정상 네트워크 내도 살펴보고 hello 데이터 toodiscover 근본 원인 악의적인 사용자 에이전트 또는 취약 포트 같은 알림 메시지를 허용 합니다. 이 추출 된 데이터로 tooreact tooand 모든 유해한 침입 시도로 네트워크를 보호 하는 방법에 대 한 합리적 결정 하 고 규칙 tooprevent 이후 침입 tooyour 네트워크를 만들 수 있습니다.

## <a name="next-steps"></a>다음 단계

Tootrigger 패킷에 따라 경고 방문 하 여 캡처 하는 방법에 대해 알아봅니다 [패킷 캡처 toodo 사전 네트워크 모니터링 Azure 함수와 함께 사용 하 여](network-watcher-alert-triggered-packet-capture.md)

Toovisualize NSG 흐름 기록 하는 방법을 Power BI를 방문 하 여 자세한 [NSG 시각화할 Power BI를 사용 하 여 로그 전달](network-watcher-visualize-nsg-flow-logs-power-bi.md)



<!-- images -->
[1]: ./media/network-watcher-intrusion-detection-open-source-tools/figure1.png
[2]: ./media/network-watcher-intrusion-detection-open-source-tools/figure2.png
[3]: ./media/network-watcher-intrusion-detection-open-source-tools/figure3.png
[4]: ./media/network-watcher-intrusion-detection-open-source-tools/figure4.png
[5]: ./media/network-watcher-intrusion-detection-open-source-tools/figure5.png
[6]: ./media/network-watcher-intrusion-detection-open-source-tools/figure6.png
[7]: ./media/network-watcher-intrusion-detection-open-source-tools/figure7.png
