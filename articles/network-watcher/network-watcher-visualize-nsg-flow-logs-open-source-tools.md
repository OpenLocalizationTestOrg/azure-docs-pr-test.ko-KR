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
# <a name="visualize-azure-network-watcher-nsg-flow-logs-using-open-source-tools"></a><span data-ttu-id="55e61-103">오픈 소스 도구를 사용하여 Azure Network Watcher NSG 흐름 로그 시각화</span><span class="sxs-lookup"><span data-stu-id="55e61-103">Visualize Azure Network Watcher NSG flow logs using open source tools</span></span>

<span data-ttu-id="55e61-104">네트워크 보안 그룹 흐름 로그는 네트워크 보안 그룹의 송/수신 IP 트래픽을 이해하는 데 사용할 수 있는 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-104">Network Security Group flow logs provide information that can be used understand ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="55e61-105">이러한 흐름 로그 아웃 바운드 나타나며 당 규칙 별로 인바운드 흐름 hello NIC hello 흐름 hello 흐름 (소스/대상 IP, 소스/대상 포트, 프로토콜) 및 hello 트래픽을 허용 또는 거부 된 경우에 대 한 5 튜플 정보에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-105">These flow logs show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5 tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="55e61-106">이러한 흐름 로그 어려운 toomanually 구문 분석 되며 로부터 이해를 넓힐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-106">These flow logs can be difficult toomanually parse and gain insights from.</span></span> <span data-ttu-id="55e61-107">그러나 이 데이터를 시각화하는 데 도움이 되는 오픈 소스 도구가 몇 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-107">However, there are several open source tools that can help visualize this data.</span></span> <span data-ttu-id="55e61-108">이 문서 솔루션 toovisualize tooquickly 인덱스를 사용 하면 되며 프로그램 흐름 로그 Kibana 대시보드에서 시각화를 탄력적 스택 hello를 사용 하 여 이러한 로그를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-108">This article will provide a solution toovisualize these logs using hello Elastic Stack, which will allow you tooquickly index and visualize your flow logs on a Kibana dashboard.</span></span>

## <a name="scenario"></a><span data-ttu-id="55e61-109">시나리오</span><span class="sxs-lookup"><span data-stu-id="55e61-109">Scenario</span></span>

<span data-ttu-id="55e61-110">이 문서에서는 탄력적 스택 hello를 사용 하 여 toovisualize 네트워크 보안 그룹 흐름 로그 수 있는 솔루션을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-110">In this article, we will set up a solution that will allow you toovisualize Network Security Group flow logs using hello Elastic Stack.</span></span>  <span data-ttu-id="55e61-111">Logstash 입력된 플러그 인 hello 흐름 로그가 들어 있는 대해 구성 된 hello 저장소 blob에서 직접 hello 흐름 로그를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-111">A Logstash input plugin will obtain hello flow logs directly from hello storage blob configured for containing hello flow logs.</span></span> <span data-ttu-id="55e61-112">탄력적 스택 hello를 사용 하 여 hello 흐름 로그 인덱싱됩니다 이동한 toocreate Kibana 대시보드 toovisualize hello 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-112">Then, using hello Elastic Stack, hello flow logs will be indexed and used toocreate a Kibana dashboard toovisualize hello information.</span></span>

![시나리오][scenario]

## <a name="steps"></a><span data-ttu-id="55e61-114">단계</span><span class="sxs-lookup"><span data-stu-id="55e61-114">Steps</span></span>

### <a name="enable-network-security-group-flow-logging"></a><span data-ttu-id="55e61-115">네트워크 보안 그룹 흐름 로그 사용</span><span class="sxs-lookup"><span data-stu-id="55e61-115">Enable Network Security Group flow logging</span></span>
<span data-ttu-id="55e61-116">이 시나리오에서는 계정에 있는 하나 이상의 네트워크 보안 그룹에서 네트워크 보안 그룹 흐름 로깅을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-116">For this scenario, you must have Network Security Group Flow Logging enabled on at least one Network Security Group in your account.</span></span> <span data-ttu-id="55e61-117">네트워크 보안 흐름 로그 설정에 대 한 자세한 내용은 다음 문서 toohello 참조 [네트워크 보안 그룹에 대 한 소개 tooflow 로깅을](network-watcher-nsg-flow-logging-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-117">For instructions on enabling Network Security Flow Logs, refer toohello following article [Introduction tooflow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>


### <a name="set-up-hello-elastic-stack"></a><span data-ttu-id="55e61-118">탄력적 스택 hello 설정</span><span class="sxs-lookup"><span data-stu-id="55e61-118">Set up hello Elastic Stack</span></span>
<span data-ttu-id="55e61-119">NSG를 연결 하 여 흐름 탄력적 스택 hello 사용 하 여 로그를 우리 수 Kibana 대시보드 toosearch 수 있습니다, 그래프, 분석, 만들고이 우리의 로그에서 정보를 파생 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-119">By connecting NSG flow logs with hello Elastic Stack, we can create a Kibana dashboard what allows us toosearch, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="55e61-120">Elasticsearch 설치</span><span class="sxs-lookup"><span data-stu-id="55e61-120">Install Elasticsearch</span></span>

1. <span data-ttu-id="55e61-121">hello 탄력적 스택 버전 5.0 이상과 Java 8 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-121">hello Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="55e61-122">Hello 명령을 실행 `java -version` toocheck 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-122">Run hello command `java -version` toocheck your version.</span></span> <span data-ttu-id="55e61-123">설치에 toodocumentation를 참조 하세요 java 있는지 [Oracle의 웹 사이트](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span><span class="sxs-lookup"><span data-stu-id="55e61-123">If you do not have java install, refer toodocumentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="55e61-124">시스템에 대 한 hello 올바른 이진 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-124">Download hello correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="55e61-125">다른 설치 방법은 [Elasticsearch 설치](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-125">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="55e61-126">Elasticsearch hello 명령을 사용 하 여 실행 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-126">Verify that Elasticsearch is running with hello command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="55e61-127">응답 비슷한 toothis를 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-127">You should see a response similar toothis:</span></span>

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

<span data-ttu-id="55e61-128">에 대 한 자세한 지침은 설치 탄력적 검색, toohello 페이지 참조 [설치](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span><span class="sxs-lookup"><span data-stu-id="55e61-128">For further instructions on installing Elastic search, refer toohello page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="55e61-129">Logstash 설치</span><span class="sxs-lookup"><span data-stu-id="55e61-129">Install Logstash</span></span>

1. <span data-ttu-id="55e61-130">tooinstall Logstash hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-130">tooinstall Logstash run hello following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="55e61-131">다음 tooconfigure Logstash tooaccess 필요 하 고 hello 흐름 로그를 구문 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-131">Next we need tooconfigure Logstash tooaccess and parse hello flow logs.</span></span> <span data-ttu-id="55e61-132">다음을 사용하여 logstash.conf 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-132">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="55e61-133">다음 콘텐츠 toohello 파일 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-133">Add hello following content toohello file:</span></span>

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

<span data-ttu-id="55e61-134">Logstash를 설치 하는 방법에 자세한 내용은 참조 toohello [공식 설명서](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span><span class="sxs-lookup"><span data-stu-id="55e61-134">For further instructions on installing Logstash, refer toohello [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-hello-logstash-input-plugin-for-azure-blob-storage"></a><span data-ttu-id="55e61-135">Azure blob 저장소에 대 한 hello Logstash 입력된 플러그인을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-135">Install hello Logstash input plugin for Azure blob storage</span></span>

<span data-ttu-id="55e61-136">이 Logstash 플러그 인을 사용 하면 자신의 지정 된 저장소 계정에서 toodirectly 액세스 hello 흐름 로그 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-136">This Logstash plugin will allow you toodirectly access hello flow logs from their designated storage account.</span></span> <span data-ttu-id="55e61-137">tooinstall이 플러그이 인 (에서이 사례 /usr/share/logstash/bin) hello 기본 Logstash 설치 디렉터리에서 hello 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-137">tooinstall this plugin, from hello default Logstash installation directory (in this case /usr/share/logstash/bin) run hello command:</span></span>

```
logstash-plugin install logstash-input-azureblob
```

<span data-ttu-id="55e61-138">toostart Logstash hello 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-138">toostart Logstash run hello command:</span></span>

```
sudo /etc/init.d/logstash start
```

<span data-ttu-id="55e61-139">이 플러그 인에 대 한 자세한 내용은 참조 toodocumentation [여기](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span><span class="sxs-lookup"><span data-stu-id="55e61-139">For more information about this plugin, refer toodocumentation [here](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="55e61-140">Kibana 설치</span><span class="sxs-lookup"><span data-stu-id="55e61-140">Install Kibana</span></span>

1. <span data-ttu-id="55e61-141">다음 명령을 tooinstall Kibana hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-141">Run hello following commands tooinstall Kibana:</span></span>

  ```
  curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
  tar xzvf kibana-5.2.0-linux-x86_64.tar.gz
  ```

1. <span data-ttu-id="55e61-142">toorun Kibana hello 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-142">toorun Kibana use hello commands:</span></span>

  ```
  cd kibana-5.2.0-linux-x86_64/
  ./bin/kibana
  ```

1. <span data-ttu-id="55e61-143">tooview Kibana 웹 인터페이스를 너무 이동`http://localhost:5601`</span><span class="sxs-lookup"><span data-stu-id="55e61-143">tooview your Kibana web interface, navigate too`http://localhost:5601`</span></span>
1. <span data-ttu-id="55e61-144">이 시나리오에 대 한 hello 인덱스 hello 흐름 로그에 사용 되는 방법은 "nsg 흐름 로그"입니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-144">For this scenario, hello index pattern used for hello flow logs is "nsg-flow-logs".</span></span> <span data-ttu-id="55e61-145">Hello 인덱스 패턴 logstash.conf 파일의 hello "output" 섹션에 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-145">You may change hello index pattern in hello "output" section of your logstash.conf file.</span></span>

1. <span data-ttu-id="55e61-146">Tooview hello Kibana 대시보드를 원격으로 원하는 경우 만들 너무 액세스를 허용 하는 인바운드 NSG 규칙**5601 포트**합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-146">If you want tooview hello Kibana dashboard remotely, create an inbound NSG rule allowing access too**port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="55e61-147">Kibana 대시보드 만들기</span><span class="sxs-lookup"><span data-stu-id="55e61-147">Create a Kibana dashboard</span></span>

<span data-ttu-id="55e61-148">이 문서에 대 한 있습니다 tooview 추세에 대 한 샘플 대시보드 및 경고의 세부 사항을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-148">For this article, we have provided a sample dashboard for you tooview trends and details in your alerts.</span></span>

![그림 1][1]

1. <span data-ttu-id="55e61-150">Hello 대시보드 파일을 다운로드 [여기](https://aka.ms/networkwatchernsgflowlogdashboard), hello 시각화 파일 [여기](https://aka.ms/networkwatchernsgflowlogvisualizations), 및 저장 하는 hello 검색 파일 [여기](https://aka.ms/networkwatchernsgflowlogsearch)합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-150">Download hello dashboard file [here](https://aka.ms/networkwatchernsgflowlogdashboard), hello visualization file [here](https://aka.ms/networkwatchernsgflowlogvisualizations), and hello saved search file [here](https://aka.ms/networkwatchernsgflowlogsearch).</span></span>

1. <span data-ttu-id="55e61-151">Hello에서 **관리** 탭 Kibana의 이동 너무**개체 저장** 세 개 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-151">Under hello **Management** tab of Kibana, navigate too**Saved Objects** and import all three files.</span></span> <span data-ttu-id="55e61-152">Hello 다음 **대시보드** 열면 탭 및 부하 hello 샘플 대시보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-152">Then from hello **Dashboard** tab you can open and load hello sample dashboard.</span></span>

<span data-ttu-id="55e61-153">사용자가 관심 있는 메트릭에 맞는 시각화 및 대시보드를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-153">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="55e61-154">Kibana의 [공식적인 설명서](https://www.elastic.co/guide/en/kibana/current/visualize.html)에서 Kibana 시각화 만들기에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="55e61-154">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

### <a name="visualize-nsg-flow-logs"></a><span data-ttu-id="55e61-155">NSG 흐름 로그 시각화</span><span class="sxs-lookup"><span data-stu-id="55e61-155">Visualize NSG flow logs</span></span>

<span data-ttu-id="55e61-156">hello 샘플 대시보드는 hello 흐름 로그의 몇 가지 시각화를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-156">hello sample dashboard provides several visualizations of hello flow logs:</span></span>

1. <span data-ttu-id="55e61-157">시간 시계열 그래프 기간 hello를 통해 흐름 hello 수를 표시 하 여 의사 결정/방향 시간에 따른-이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-157">Flows by Decision/Direction Over Time - time series graphs showing hello number of flows over hello time period.</span></span> <span data-ttu-id="55e61-158">시간 단위 hello와 이러한 시각화 요소 범위를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-158">You can edit hello unit of time and span of both these visualizations.</span></span> <span data-ttu-id="55e61-159">의사 결정 hello 비율을 표시 하 여 흐름을 허용 하거나 인바운드 및 아웃 바운드 트래픽의 방향은 표시 hello 비율로 흐름 하는 동안 이루어진 결정을 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-159">Flows by Decision shows hello proportion of allow or deny decisions made, while Flows by Direction shows hello proportion of inbound and outbound traffic.</span></span> <span data-ttu-id="55e61-160">이러한 시각 효과를 사용하면 시간에 따른 트래픽 추세를 검토할 수 있고 스파이크 또는 비정상 패턴을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-160">With these visuals you can examine traffic trends over time and look for any spikes or unusual patterns.</span></span>

  ![figure2][2]

1. <span data-ttu-id="55e61-162">원형 차트의 흐름 hello 분석 tootheir 해당 포트를 보여 주는 – 대상/원본 포트에 의해 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-162">Flows by Destination/Source Port – pie charts showing hello breakdown of flows tootheir respective ports.</span></span> <span data-ttu-id="55e61-163">이 보기를 사용하면 가장 자주 사용되는 포트를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-163">With this view you can see your most commonly used ports.</span></span> <span data-ttu-id="55e61-164">Hello 원형 차트 내에서 특정 포트를 클릭 하면 해당 포트의 tooflows 아래로 hello 대시보드 hello 나머지 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-164">If you click on a specific port within hello pie chart, hello rest of hello dashboard will filter down tooflows of that port.</span></span>

  ![figure3][3]

1. <span data-ttu-id="55e61-166">흐름 및 가장 빠른 로그 시간 – 흐름 hello 수를 기록 하 고 hello 가장 빠른 로그의 hello 날짜 캡처된를 표시 하는 메트릭 수입니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-166">Number of Flows and Earliest Log Time – metrics showing you hello number of flows recorded and hello date of hello earliest log captured.</span></span>

  ![figure4][4]

1. <span data-ttu-id="55e61-168">NSG 및 규칙 – 내 각 NSG에서 규칙의 hello 배포 뿐만 아니라 각 NSG 내에서 흐름의 hello 분포를 표시 하는 막대 그래프에서 흐름.</span><span class="sxs-lookup"><span data-stu-id="55e61-168">Flows by NSG and Rule – a bar graph showing you hello distribution of flows within each NSG, as well as hello distribution of rules within each NSG.</span></span> <span data-ttu-id="55e61-169">생성 된 규칙에는 대부분의 트래픽을 hello 및 여기에서 어떤 NSG를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-169">From here you can see which NSG and rules generated hello most traffic.</span></span>

  ![figure5][5]

1. <span data-ttu-id="55e61-171">상위 10 개의 원본/대상 Ip-hello 상위 10 개의 원본 및 대상 Ip 보여 주는 가로 막대형 차트입니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-171">Top 10 Source/Destination IPs – bar charts showing hello top 10 source and destination IPs.</span></span> <span data-ttu-id="55e61-172">이러한 차트 tooshow 보다 상위 Ip을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-172">You can adjust these charts tooshow more or less top IPs.</span></span> <span data-ttu-id="55e61-173">여기에서 있습니다 수 Ip 가장 일반적으로 발생 하는 hello로 볼 트래픽 의사 결정 hello (허용 또는 거부) 각 IP 방향으로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-173">From here you can see hello most commonly occurring IPs as well as hello traffic decision (allow or deny) being made towards each IP.</span></span>

  ![figure6][6]

1. <span data-ttu-id="55e61-175">흐름 튜플 – 다음이 표에 나와 있습니다 hello 각 흐름 튜플을 뿐만 아니라 해당 NGS 및 규칙에 포함 된 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-175">Flow Tuples – this table shows you hello information contained within each flow tuple, as well as its corresponding NGS and rule.</span></span>

  ![figure7][7]

<span data-ttu-id="55e61-177">쿼리 표시줄 hello를 사용 하 여 hello hello 대시보드 위쪽에, 구독 ID, 리소스 그룹, 규칙 또는 관심 있는 다른 모든 변수의 같은 hello 흐름의 모든 매개 변수에 따라 hello 대시보드를 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-177">Using hello query bar at hello top of hello dashboard, you can filter down hello dashboard based on any parameter of hello flows, such as subscription ID, resource groups, rule, or any other variable of interest.</span></span> <span data-ttu-id="55e61-178">Kibana의 쿼리 및 필터에 대 한 자세한 참조 toohello [공식 설명서](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span><span class="sxs-lookup"><span data-stu-id="55e61-178">For more about Kibana's queries and filters, refer toohello [official documentation](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span></span>

## <a name="conclusion"></a><span data-ttu-id="55e61-179">결론</span><span class="sxs-lookup"><span data-stu-id="55e61-179">Conclusion</span></span>

<span data-ttu-id="55e61-180">탄력적 스택 hello로 hello 네트워크 보안 그룹 흐름 로그를 결합 하 여 우리 발견 했을 강력 하 고 사용자 지정할 수 있는 방법 toovisualize와 우리의 네트워크 트래픽을 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-180">By combining hello Network Security Group flow logs with hello Elastic Stack, we have come up with powerful and customizable way toovisualize our network traffic.</span></span> <span data-ttu-id="55e61-181">이러한 대시보드 tooquickly 증가 허용 되어 아래로 필터 뿐만 네트워크 트래픽을 대 한 통찰력을 공유 하 고 비정상 모든 잠재적인 문제를 조사 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-181">These dashboards allow you tooquickly gain and share insights about your network traffic, as well as filter down and investigate on any potential anomalies.</span></span> <span data-ttu-id="55e61-182">Kibana를 사용 하 여 이러한 대시보드 조정 하 고 특정 시각화 toomeet의 모든 보안, 감사 및 준수 요구를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e61-182">Using Kibana, you can tailor these dashboards and create specific visualizations toomeet any security, audit, and compliance needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55e61-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="55e61-183">Next steps</span></span>

<span data-ttu-id="55e61-184">Toovisualize NSG 흐름 기록 하는 방법을 Power BI를 방문 하 여 자세한 [NSG 시각화할 Power BI를 사용 하 여 로그 전달](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="55e61-184">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


<!--Image references-->

[scenario]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/scenario.png
[1]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure7.png
