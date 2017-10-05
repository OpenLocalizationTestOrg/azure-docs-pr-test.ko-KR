---
title: "오픈 소스 도구를 사용하여 Azure Network Watcher NSG 흐름 로그 시각화 | Microsoft Docs"
description: "이 페이지에서는 오픈 소스 도구를 사용하여 NSG 흐름 로그를 시각화하는 방법을 설명합니다."
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
ms.openlocfilehash: 20f60ccd9108a7473705c2368f28d3152d0dd614
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-azure-network-watcher-nsg-flow-logs-using-open-source-tools"></a><span data-ttu-id="a6e27-103">오픈 소스 도구를 사용하여 Azure Network Watcher NSG 흐름 로그 시각화</span><span class="sxs-lookup"><span data-stu-id="a6e27-103">Visualize Azure Network Watcher NSG flow logs using open source tools</span></span>

<span data-ttu-id="a6e27-104">네트워크 보안 그룹 흐름 로그는 네트워크 보안 그룹의 송/수신 IP 트래픽을 이해하는 데 사용할 수 있는 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-104">Network Security Group flow logs provide information that can be used understand ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="a6e27-105">이러한 흐름 로그는 트래픽이 허용되거나 거부된 경우 각 규칙을 기준으로 아웃바운드 및 인바운드 흐름, 흐름이 적용되는 NIC, 흐름에 대한 5개의 튜플 정보(원본/대상 IP, 원본/대상 포트, 프로토콜)를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-105">These flow logs show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5 tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

<span data-ttu-id="a6e27-106">이러한 흐름 로그는 수동으로 구문 분석하여 통찰력을 얻기 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-106">These flow logs can be difficult to manually parse and gain insights from.</span></span> <span data-ttu-id="a6e27-107">그러나 이 데이터를 시각화하는 데 도움이 되는 오픈 소스 도구가 몇 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-107">However, there are several open source tools that can help visualize this data.</span></span> <span data-ttu-id="a6e27-108">이 문서에서는 Kibana 대시보드에서 흐름 로그를 신속하게 인덱싱하고 시각화할 수 있는 탄력적인 스택을 사용하여 이러한 로그를 시각화하는 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-108">This article will provide a solution to visualize these logs using the Elastic Stack, which will allow you to quickly index and visualize your flow logs on a Kibana dashboard.</span></span>

## <a name="scenario"></a><span data-ttu-id="a6e27-109">시나리오</span><span class="sxs-lookup"><span data-stu-id="a6e27-109">Scenario</span></span>

<span data-ttu-id="a6e27-110">이 문서에서는 탄력적인 스택을 사용하여 네트워크 보안 그룹 흐름 로그를 시각화할 수 있는 솔루션을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-110">In this article, we will set up a solution that will allow you to visualize Network Security Group flow logs using the Elastic Stack.</span></span>  <span data-ttu-id="a6e27-111">Logstash 입력 플러그 인은 흐름 로그를 포함하기 위해 구성된 Blob Storage에서 직접 흐름 로그를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-111">A Logstash input plugin will obtain the flow logs directly from the storage blob configured for containing the flow logs.</span></span> <span data-ttu-id="a6e27-112">그런 다음 탄력적인 스택을 사용하여 흐름 로그가 인덱싱되고, 흐름 로그로 Kibana 대시보드를 만들어 정보를 시각화합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-112">Then, using the Elastic Stack, the flow logs will be indexed and used to create a Kibana dashboard to visualize the information.</span></span>

![시나리오][scenario]

## <a name="steps"></a><span data-ttu-id="a6e27-114">단계</span><span class="sxs-lookup"><span data-stu-id="a6e27-114">Steps</span></span>

### <a name="enable-network-security-group-flow-logging"></a><span data-ttu-id="a6e27-115">네트워크 보안 그룹 흐름 로그 사용</span><span class="sxs-lookup"><span data-stu-id="a6e27-115">Enable Network Security Group flow logging</span></span>
<span data-ttu-id="a6e27-116">이 시나리오에서는 계정에 있는 하나 이상의 네트워크 보안 그룹에서 네트워크 보안 그룹 흐름 로깅을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-116">For this scenario, you must have Network Security Group Flow Logging enabled on at least one Network Security Group in your account.</span></span> <span data-ttu-id="a6e27-117">네트워크 보안 흐름 로그를 사용하도록 설정하는 방법에 대한 지침은 [네트워크 보안 그룹에 대한 흐름 로깅 소개](network-watcher-nsg-flow-logging-overview.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6e27-117">For instructions on enabling Network Security Flow Logs, refer to the following article [Introduction to flow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>


### <a name="set-up-the-elastic-stack"></a><span data-ttu-id="a6e27-118">탄력적 스택 설정</span><span class="sxs-lookup"><span data-stu-id="a6e27-118">Set up the Elastic Stack</span></span>
<span data-ttu-id="a6e27-119">NSG 흐름 로그를 탄력적 스택과 연결하여 로그에서 정보를 검색하고, 그래프화하며 분석하고 정보를 끌어낼 수 있는 Kibana 대시보드를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-119">By connecting NSG flow logs with the Elastic Stack, we can create a Kibana dashboard what allows us to search, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="a6e27-120">Elasticsearch 설치</span><span class="sxs-lookup"><span data-stu-id="a6e27-120">Install Elasticsearch</span></span>

1. <span data-ttu-id="a6e27-121">이번 5.0 이상의 탄력적 스택에는 Java 8이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-121">The Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="a6e27-122">`java -version` 명령을 실행하여 버전을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-122">Run the command `java -version` to check your version.</span></span> <span data-ttu-id="a6e27-123">java가 설치되지 않은 경우 [Oracle의 웹 사이트](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)에서 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6e27-123">If you do not have java install, refer to documentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="a6e27-124">시스템에 맞는 이진 패키지를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-124">Download the correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="a6e27-125">다른 설치 방법은 [Elasticsearch 설치](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-125">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="a6e27-126">명령으로 Elasticsearch가 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-126">Verify that Elasticsearch is running with the command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="a6e27-127">다음과 유사한 응답이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-127">You should see a response similar to this:</span></span>

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

<span data-ttu-id="a6e27-128">탄력적 검색 설치에 대한 추가 정보는 [설치](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6e27-128">For further instructions on installing Elastic search, refer to the page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="a6e27-129">Logstash 설치</span><span class="sxs-lookup"><span data-stu-id="a6e27-129">Install Logstash</span></span>

1. <span data-ttu-id="a6e27-130">Logstash를 설치하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-130">To install Logstash run the following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="a6e27-131">다음에는 흐름 로그를 액세스하고 구문 분석하도록 Logstash를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-131">Next we need to configure Logstash to access and parse the flow logs.</span></span> <span data-ttu-id="a6e27-132">다음을 사용하여 logstash.conf 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-132">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="a6e27-133">파일에 다음 내용을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-133">Add the following content to the file:</span></span>

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

<span data-ttu-id="a6e27-134">Logstash 설치에 대한 추가 정보는 [공식 설명서](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6e27-134">For further instructions on installing Logstash, refer to the [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-the-logstash-input-plugin-for-azure-blob-storage"></a><span data-ttu-id="a6e27-135">Azure Blob Storage를 위한 Logstash 입력 플러그 인 설치</span><span class="sxs-lookup"><span data-stu-id="a6e27-135">Install the Logstash input plugin for Azure blob storage</span></span>

<span data-ttu-id="a6e27-136">이 Logstash 플러그 인을 사용하면 지정된 저장소 계정에서 흐름 로그에 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-136">This Logstash plugin will allow you to directly access the flow logs from their designated storage account.</span></span> <span data-ttu-id="a6e27-137">이 플러그 인을 설치하려면 기본 Logstash 설치 디렉터리(이 경우 /usr/share/logstash/bin)에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-137">To install this plugin, from the default Logstash installation directory (in this case /usr/share/logstash/bin) run the command:</span></span>

```
logstash-plugin install logstash-input-azureblob
```

<span data-ttu-id="a6e27-138">Logstash를 시작하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-138">To start Logstash run the command:</span></span>

```
sudo /etc/init.d/logstash start
```

<span data-ttu-id="a6e27-139">이 플러그 인에 대한 자세한 내용을 보려면 [여기](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)에서 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6e27-139">For more information about this plugin, refer to documentation [here](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="a6e27-140">Kibana 설치</span><span class="sxs-lookup"><span data-stu-id="a6e27-140">Install Kibana</span></span>

1. <span data-ttu-id="a6e27-141">다음 명령을 실행하여 Kibana를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-141">Run the following commands to install Kibana:</span></span>

  ```
  curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
  tar xzvf kibana-5.2.0-linux-x86_64.tar.gz
  ```

1. <span data-ttu-id="a6e27-142">Kibana를 실행하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-142">To run Kibana use the commands:</span></span>

  ```
  cd kibana-5.2.0-linux-x86_64/
  ./bin/kibana
  ```

1. <span data-ttu-id="a6e27-143">Kibana 웹 인터페이스를 보려면 `http://localhost:5601`로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-143">To view your Kibana web interface, navigate to `http://localhost:5601`</span></span>
1. <span data-ttu-id="a6e27-144">이 시나리오에서 흐름 로그에 사용된 인덱스 패턴은 "nsg-flow-logs"입니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-144">For this scenario, the index pattern used for the flow logs is "nsg-flow-logs".</span></span> <span data-ttu-id="a6e27-145">logstash.conf 파일의 "output" 섹션에서 인덱스 패턴을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-145">You may change the index pattern in the "output" section of your logstash.conf file.</span></span>

1. <span data-ttu-id="a6e27-146">Kibana 대시보드를 원격으로 보려면 **포트 5601**에 대해 액세스를 허용하는 인바운드 NSG 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-146">If you want to view the Kibana dashboard remotely, create an inbound NSG rule allowing access to **port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="a6e27-147">Kibana 대시보드 만들기</span><span class="sxs-lookup"><span data-stu-id="a6e27-147">Create a Kibana dashboard</span></span>

<span data-ttu-id="a6e27-148">이 문서에서는 경고에 대한 추세 및 세부 정보를 볼 수 있는 샘플 대시보드를 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-148">For this article, we have provided a sample dashboard for you to view trends and details in your alerts.</span></span>

![그림 1][1]

1. <span data-ttu-id="a6e27-150">대시보드 파일은 [여기](https://aka.ms/networkwatchernsgflowlogdashboard)에서, 시각화 파일은 [여기](https://aka.ms/networkwatchernsgflowlogvisualizations)에서, 저장된 검색 파일은 [여기](https://aka.ms/networkwatchernsgflowlogsearch)에서 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-150">Download the dashboard file [here](https://aka.ms/networkwatchernsgflowlogdashboard), the visualization file [here](https://aka.ms/networkwatchernsgflowlogvisualizations), and the saved search file [here](https://aka.ms/networkwatchernsgflowlogsearch).</span></span>

1. <span data-ttu-id="a6e27-151">Kibana의 **관리** 탭 아래에서 **저장된 개체**로 이동하고 세 개 파일을 모두 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-151">Under the **Management** tab of Kibana, navigate to **Saved Objects** and import all three files.</span></span> <span data-ttu-id="a6e27-152">그런 다음 **대시보드** 탭에서 샘플 대시보드를 열고 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-152">Then from the **Dashboard** tab you can open and load the sample dashboard.</span></span>

<span data-ttu-id="a6e27-153">사용자가 관심 있는 메트릭에 맞는 시각화 및 대시보드를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-153">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="a6e27-154">Kibana의 [공식적인 설명서](https://www.elastic.co/guide/en/kibana/current/visualize.html)에서 Kibana 시각화 만들기에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="a6e27-154">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

### <a name="visualize-nsg-flow-logs"></a><span data-ttu-id="a6e27-155">NSG 흐름 로그 시각화</span><span class="sxs-lookup"><span data-stu-id="a6e27-155">Visualize NSG flow logs</span></span>

<span data-ttu-id="a6e27-156">샘플 대시보드는 흐름 로그에 대한 다양한 시각화를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-156">The sample dashboard provides several visualizations of the flow logs:</span></span>

1. <span data-ttu-id="a6e27-157">Flows by Decision/Direction Over Time - 기간별 흐름 수를 보여주는 시계열 그래프입니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-157">Flows by Decision/Direction Over Time - time series graphs showing the number of flows over the time period.</span></span> <span data-ttu-id="a6e27-158">이러한 시각화 요소의 시간 단위와 범위를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-158">You can edit the unit of time and span of both these visualizations.</span></span> <span data-ttu-id="a6e27-159">Flows by Decision은 허용 또는 거부 결정의 비율을 보여주고, Flows by Direction은 인바운드 및 아웃바운드 트래픽의 비율을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-159">Flows by Decision shows the proportion of allow or deny decisions made, while Flows by Direction shows the proportion of inbound and outbound traffic.</span></span> <span data-ttu-id="a6e27-160">이러한 시각 효과를 사용하면 시간에 따른 트래픽 추세를 검토할 수 있고 스파이크 또는 비정상 패턴을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-160">With these visuals you can examine traffic trends over time and look for any spikes or unusual patterns.</span></span>

  ![figure2][2]

1. <span data-ttu-id="a6e27-162">Flows by Destination/Source Port - 각 해당 포트에 대한 흐름의 분석 결과를 보여 주는 원형 차트입니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-162">Flows by Destination/Source Port – pie charts showing the breakdown of flows to their respective ports.</span></span> <span data-ttu-id="a6e27-163">이 보기를 사용하면 가장 자주 사용되는 포트를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-163">With this view you can see your most commonly used ports.</span></span> <span data-ttu-id="a6e27-164">원형 차트 내에서 특정 포트를 클릭하면 대시보드의 나머지 부분이 해당 포트의 흐름으로 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-164">If you click on a specific port within the pie chart, the rest of the dashboard will filter down to flows of that port.</span></span>

  ![figure3][3]

1. <span data-ttu-id="a6e27-166">Number of Flows 및 Earliest Log Time – 기록된 흐름 수 및 가장 빨리 캡처된 로그의 날짜를 보여주는 메트릭입니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-166">Number of Flows and Earliest Log Time – metrics showing you the number of flows recorded and the date of the earliest log captured.</span></span>

  ![figure4][4]

1. <span data-ttu-id="a6e27-168">Flows by NSG and Rule – 각 NSG 내 흐름 분포와 각 NSG 내 규칙 분포를 보여주는 막대 그래프입니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-168">Flows by NSG and Rule – a bar graph showing you the distribution of flows within each NSG, as well as the distribution of rules within each NSG.</span></span> <span data-ttu-id="a6e27-169">여기에서 어떤 NSG와 규칙이 가장 많은 트래픽을 생성했는지 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-169">From here you can see which NSG and rules generated the most traffic.</span></span>

  ![figure5][5]

1. <span data-ttu-id="a6e27-171">Top 10 Source/Destination IPs - 상위 10개의 원본 및 대상 IP를 보여주는 막대형 차트입니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-171">Top 10 Source/Destination IPs – bar charts showing the top 10 source and destination IPs.</span></span> <span data-ttu-id="a6e27-172">이러한 차트를 조정하여 표시되는 상위 IP를 늘리거나 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-172">You can adjust these charts to show more or less top IPs.</span></span> <span data-ttu-id="a6e27-173">여기에서 가장 자주 발생하는 IP와 각 IP에 대해 수행되는 트래픽 의사 결정(허용 또는 거부)을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-173">From here you can see the most commonly occurring IPs as well as the traffic decision (allow or deny) being made towards each IP.</span></span>

  ![figure6][6]

1. <span data-ttu-id="a6e27-175">Flow Tuples - 이 표에서는 각 흐름 튜플 내에 포함된 정보와 해당하는 NGS 및 규칙을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-175">Flow Tuples – this table shows you the information contained within each flow tuple, as well as its corresponding NGS and rule.</span></span>

  ![figure7][7]

<span data-ttu-id="a6e27-177">대시보드 맨 위에 있는 쿼리 표시줄을 사용하여 구독 ID, 리소스 그룹, 규칙 또는 원하는 다른 변수 같은 흐름의 모든 매개 변수를 기준으로 대시보드를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-177">Using the query bar at the top of the dashboard, you can filter down the dashboard based on any parameter of the flows, such as subscription ID, resource groups, rule, or any other variable of interest.</span></span> <span data-ttu-id="a6e27-178">Kibana의 쿼리 및 필터에 대한 자세한 내용을 보려면 [공식 설명서](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6e27-178">For more about Kibana's queries and filters, refer to the [official documentation](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span></span>

## <a name="conclusion"></a><span data-ttu-id="a6e27-179">결론</span><span class="sxs-lookup"><span data-stu-id="a6e27-179">Conclusion</span></span>

<span data-ttu-id="a6e27-180">탄력적인 스택과 네트워크 보안 그룹 흐름 로그를 결합하여 네트워크 트래픽을 가시화하는 강력하고 사용자 지정 가능한 방법을 개발했습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-180">By combining the Network Security Group flow logs with the Elastic Stack, we have come up with powerful and customizable way to visualize our network traffic.</span></span> <span data-ttu-id="a6e27-181">이러한 대시보드를 사용하면 네트워크 트래픽에 대한 통찰력을 신속하게 얻고 공유할 뿐만 모든 잠재적인 이상 요소를 필터링하고 조사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-181">These dashboards allow you to quickly gain and share insights about your network traffic, as well as filter down and investigate on any potential anomalies.</span></span> <span data-ttu-id="a6e27-182">Kibana를 사용하면 이러한 대시보드를 조정하고 모든 보안, 감사 및 규정 준수 요구 사항에 맞는 특정 시각화 요소를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e27-182">Using Kibana, you can tailor these dashboards and create specific visualizations to meet any security, audit, and compliance needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6e27-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a6e27-183">Next steps</span></span>

<span data-ttu-id="a6e27-184">[PowerBI에서 NSG 흐름 로그 시각화](network-watcher-visualize-nsg-flow-logs-power-bi.md)에서 Power BI로 NSG 흐름 로그를 시각화하는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="a6e27-184">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


<!--Image references-->

[scenario]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/scenario.png
[1]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure7.png
