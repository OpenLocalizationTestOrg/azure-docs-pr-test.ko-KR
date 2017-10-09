---
title: "Apache Storm 및 HBase를 사용 하 여 aaaAnalyze 센서 데이터 | Microsoft Docs"
description: "자세한 내용은 가상 네트워크와 tooconnect tooApache 스톰 방법입니다. Storm를 사용 하 여 이벤트 허브에서 HBase tooprocess 센서 데이터를 사용 하 고 D3.js로 시각화 합니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a9a1ac8e-5708-4833-b965-e453815e671f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/09/2017
ms.author: larryfr
ms.openlocfilehash: e54fe9ffc720b0089f90e302b24a9438bd43999a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a>HDInsight(Hadoop)에서 Apache Storm, 이벤트 허브 및 HBase를 사용하여 센서 데이터 분석

자세한 내용은 Azure 이벤트 허브의 HDInsight tooprocess 센서 데이터에 대해 toouse Apache Storm 방법입니다. hello 데이터, HDInsight의 Apache HBase에 저장 됩니다 및 D3.js를 사용 하 여 시각화 됩니다.

이 문서에 사용 되는 hello Azure 리소스 관리자 템플릿을 보여 줍니다. 방법을 toocreate 리소스 그룹에 여러 Azure 리소스입니다. hello 템플릿은 Azure 가상 네트워크, 두 개의 HDInsight 클러스터 (스톰 및 HBase) 및 Azure 웹 앱을 만듭니다. 실시간 웹 대시보드를 구현 하는 node.js 웹 응용 프로그램 배포가 자동으로 toohello입니다.

> [!NOTE]
> 이 문서와이 문서에 대 한 예제에서 hello 정보 HDInsight 버전 3.6 필요 합니다.
>
> Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

## <a name="prerequisites"></a>필수 조건

* Azure 구독.
* [Node.js](http://nodejs.org/): 개발 환경에서 로컬로 사용 되는 toopreview hello 웹 대시보드 합니다.
* [Java 및 hello JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): toodevelop hello 스톰 토폴로지를 사용 합니다.
* [Maven](http://maven.apache.org/what-is-maven.html): toobuild 및 컴파일 hello 프로젝트를 사용된 합니다.
* [Git](http://git-scm.com/): GitHub에서 사용 되는 toodownload hello 프로젝트.
* **SSH** 클라이언트: tooconnect toohello Linux 기반 HDInsight 클러스터를 사용 합니다. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.


> [!IMPORTANT]
> 기존 HDInsight 클러스터가 필요하지 않습니다. 이 문서의 단계 hello hello 다음 리소스를 만듭니다.
> 
> * Azure 가상 네트워크
> * HDInsight 클러스터의 Storm(Linux 기반, 작업자 노드 2개)
> * HDInsight 클러스터의 HBase(Linux 기반, 작업자 노드 2개)
> * Hello 웹 대시보드를 호스팅하는 Azure 웹 앱

## <a name="architecture"></a>아키텍처

![아키텍처 다이어그램](./media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

이 예제에서는 다음과 같은 구성 요소가 hello 이루어져 있습니다.

* **Azure 이벤트 허브**: 센서에서 수집된 데이터를 포함합니다.
* **HDInsight의 Storm**: 이벤트 허브의 데이터를 실시간으로 처리합니다.
* **HDInsight의 HBase**: Storm에서 처리된 후에 데이터에 대한 영구 NoSQL 데이터 저장소를 제공합니다.
* **Azure 가상 네트워크 서비스**: HDInsight 클러스터에서 HDInsight의 Storm hello 및 HBase 간의 보안 통신을 사용 하도록 설정 합니다.
  
  > [!NOTE]
  > 가상 네트워크는 hello HBase Java 클라이언트 API를 사용 하는 경우에 필요 합니다. HBase 클러스터에 대 한 hello 공용 게이트웨이 통해 노출 되지 않습니다. 동일한 가상 네트워크를 허용 하는 hello로 설치 HBase 및 Storm 클러스터 hello Storm 클러스터 (또는 hello 가상 네트워크에서 다른 시스템) toodirectly 클라이언트 API를 사용 하 여 HBase에 액세스 합니다.

* **대시보드 웹 사이트**: 실시간으로 데이터 차트를 작성하는 예제 대시보드입니다.
  
  * hello 웹 사이트는 Node.js에서 구현 됩니다.
  * [Socket.io](http://socket.io/) hello 웹 사이트와 hello 스톰 토폴로지 실시간 통신에 사용 됩니다.
    
    > [!NOTE]
    > 통신에 Socket.io를 사용하는 것은 구현 세부 정보입니다. 원시 WebSocket 또는 SignalR과 같은 모든 통신 프레임워크를 사용할 수 있습니다.

  * [D3.js](http://d3js.org/) toohello 웹 사이트에 전송 된 사용 되는 toograph hello 데이터입니다.

> [!IMPORTANT]
> 지원 되는 방법을 toocreate 하나 HDInsight 클러스터가 없습니다 스톰와 HBase 없기 때문에 두 개의 클러스터가 필요 합니다.

hello 토폴로지 데이터 이벤트 허브에서 사용 하 여 읽고 hello [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) 집합과 hello를 사용 하 여 HBase에 데이터 쓰기 [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) 클래스입니다. Hello 웹 사이트와 통신을 사용 하 여 수행 됩니다 [socket.io client.java](https://github.com/nkzawa/socket.io-client.java)합니다.

다음 다이어그램 hello hello 토폴로지의 hello 레이아웃을 설명 합니다.

![토폴로지 다이어그램](./media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> 이 다이어그램은 토폴로지 hello의 단순화 된 보기입니다. Event Hub의 각 파티션에 대해 각 구성 요소의 인스턴스가 만들어집니다. 이러한 인스턴스는 hello hello 클러스터 노드를 통해 배포 되 고 다음과 같이 데이터 간에 전달 되:
> 
> * Hello 배출구 toohello 파서 데이터는 부하 분산 합니다.
> * 장치 ID hello 파서 toohello 대시보드 및 HBase에서 데이터가 그룹화 되어, 메시지를 동일한 장치를 항상 hello 있도록 흐름 toohello 동일한 구성 요소입니다.

### <a name="topology-components"></a>토폴로지 구성 요소

* **이벤트 허브 Spout**: hello 배출구 0.10.0 Apache Storm 버전의 일부로 제공 되며 높은 합니다.
  
  > [!NOTE]
  > 이 예에서 사용 된 hello 이벤트 허브 배출구 HDInsight 클러스터 버전이 3.5 또는 3.6에서 Storm이 필요 합니다.

* **ParserBolt.java**: hello 배출구에서 내보내는 hello 데이터 원시 JSON 이며 한 번에 하나 이상의 경우에 따라 이벤트를 내보냅니다. 이 볼트 읽고 hello에서 내보내는 hello 데이터 spout hello JSON 메시지를 구문 분석 합니다. hello 볼트 다음 여러 필드를 포함 하는 튜플로 서 hello 데이터를 내보냅니다.
* **DashboardBolt.java**:이 구성 요소 toouse toohello 웹 대시보드에 실시간으로 Java toosend 데이터에 대 한 클라이언트 라이브러리 Socket.io hello 하는 방법을 보여 줍니다.
* **아니요 hbase.yaml**: hello 로컬 모드에서 실행할 때 사용 되는 토폴로지 정의 합니다. HBase 구성 요소를 사용하지 않습니다.
* **hbase.yaml와**: hello hello 토폴로지 hello 클러스터에서 실행할 때 사용 되는 토폴로지 정의 합니다. HBase 구성 요소를 사용합니다.
* **dev.properties**: hello hello 이벤트 허브 배출구, HBase 볼트 및 대시보드 구성 요소에 대 한 구성 정보입니다.

## <a name="prepare-your-environment"></a>환경 준비

이 예제를 사용 하기 전에 hello 스톰 토폴로지에서 읽고 Azure 이벤트 허브를 만들어야 합니다.

### <a name="configure-event-hub"></a>이벤트 허브 구성

이벤트 허브는이 예제에 대 한 hello 데이터 원본. 다음 단계 toocreate 이벤트 허브 hello를 사용 합니다.

1. Hello에서 [Azure 포털](https://portal.azure.com)선택, **+ 새로 만들기** -> **사물 인터넷** -> **이벤트 허브**합니다.
2. Hello에 **만들 Namespace** 섹션를 hello 다음 작업을 수행 합니다.
   
   1. 입력 한 **이름** hello 네임 스페이스에 대 한 합니다.
   2. 가격 책정 계층을 선택합니다. **기본** 이면 충분합니다.
   3. 선택 hello Azure **구독** toouse 합니다.
   4. 기존 리소스 그룹을 선택하거나 새 리소스 그룹을 만듭니다.
   5. 선택 hello **위치** hello 이벤트 허브에 대 한 합니다.
   6. 선택 **Pin toodashboard**, 클릭 하 고 **만들기**합니다.

3. Hello 생성 프로세스가 완료 되 면 hello 네임 스페이스에 대 한 이벤트 허브 정보 표시 됩니다. 여기에서 **+ Event Hub 추가**를 선택합니다. Hello에 **이벤트 허브 만들기** 섹션의 이름을 입력 합니다. **sensordata**를 선택한 후 **만들기**합니다. 나머지 필드는 hello 기본값 hello를 둡니다.
4. Hello 이벤트 허브에서 하 여 네임 스페이스 선택에 대 한 보기 **이벤트 허브**합니다. 선택 hello **sensordata** 항목입니다.
5. Hello sensordata 이벤트 허브에서에서 선택 **공유 액세스 정책을**합니다. 사용 하 여 hello **+ 추가** 다음 정책 링크 tooadd hello:

    | 정책 이름 | 클레임 |
    | ----- | ----- |
    | devices | 보내기 |
    | storm | 수신 대기 |

1. 두 정책을 모두 선택 하 고 hello 메모 **기본 키** 값입니다. Hello 값 이후 단계에서 두 정책을 모두 필요합니다.

## <a name="download-and-configure-hello-project"></a>다운로드 하 고 hello 프로젝트 구성

Hello toodownload hello 프로젝트 GitHub에서 다음을 사용 합니다.

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

Hello 명령이 완료 된 후에 디렉터리 구조를 다음 hello

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains hello topology
            resources/
                log4j2.xml - set logging toominimal.
                no-hbase.yaml - topology definition without hbase components.
                with-hbase.yaml - topology definition with hbase components.
            src/main/java/com/microsoft/examples/bolts/
                ParserBolt.java - parses JSON data into tuples
                DashboardBolt.java - sends data over Socket.IO toohello web dashboard.
        dashboard/nodejs/ - this is hello node.js web dashboard.
        SendEvents/ - utilities toosend fake sensor data.

> [!NOTE]
> 이 문서는이 예제에 포함 된 hello 코드의 toofull 세부 정보에는 설명 하지 않습니다. 그러나 hello 코드 주석 완벽 하 게 됩니다.

이벤트 허브를 열고 hello에서 tooconfigure hello 프로젝트 tooread `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` 파일 및 줄을 다음에 이벤트 허브 정보 toohello 추가:

```bash
eventhub.read.policy.name: your_read_policy_name
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: your_event_hub_name
eventhub.partitions: 2
```

## <a name="compile-and-test-locally"></a>로컬로 컴파일 및 테스트

> [!IMPORTANT]
> 로컬로 hello 토폴로지를 사용 하 여 작업 스톰 개발 환경 필요 합니다. 자세한 내용은 Apache.org에서 [Storm 개발 환경 설정](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html)을 참조하세요.

> [!WARNING]
> Windows 개발 환경의 사용 하는 경우 발생할 수 있습니다는 `java.io.IOException` 때 hello 토폴로지를 로컬로 실행 합니다. 이 경우 HDInsight의 toorunning hello 토폴로지 이동 합니다.

를 테스트 하기 전에 hello 토폴로지의 hello 대시보드 tooview hello 출력을 시작 하 고 이벤트 허브에 데이터 toostore를 생성 합니다.

> [!IMPORTANT]
> 이 토폴로지의 hello HBase 구성 요소가 로컬로 테스트할 때에 활성 아닙니다. Java API hello hello HBase 클러스터에 대 한 외부 hello hello 클러스터 포함 된 Azure 가상 네트워크에서에서 액세스할 수 없습니다.

### <a name="start-hello-web-application"></a>Hello 웹 응용 프로그램 시작

1. 명령 프롬프트를 열고 디렉터리를 너무 변경`hdinsight-eventhub-example/dashboard`합니다. 명령 tooinstall hello 종속성 hello 웹 응용 프로그램에 필요한 다음 hello를 사용 합니다.
   
    ```bash
    npm install
    ```

2. 사용 하 여 hello 다음 명령 toostart hello 웹 응용 프로그램을 사용할 수 있습니다.
   
    ```bash
    node server.js
    ```
   
    텍스트 다음 메시지와 비슷한 toohello를 표시 됩니다.
   
        Server listening at port 3000

3. 웹 브라우저를 열고 다음을 입력 `http://localhost:3000/` hello 주소로 합니다. 다음 이미지는 페이지와 유사한 toohello 표시 됩니다.
   
    ![웹 대시보드](./media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    이 명령 프롬프트는 계속 열어 두세요. 테스트를 마친 후 Ctrl + C toostop hello 웹 서버를 사용 합니다.

### <a name="generate-data"></a>데이터 생성

> [!NOTE]
> hello이 섹션의 단계에 사용 하 여 Node.js 모든 플랫폼에서 사용할 수 있도록 합니다. 다른 언어 예제를 보려면 hello `SendEvents` 디렉터리입니다.

1. 새 프롬프트, 셸 또는 터미널을 열고 디렉터리를 너무 변경`hdinsight-eventhub-example/SendEvents/nodejs`합니다. 다음 명령을 사용 하 여 hello hello 응용 프로그램에 필요한 tooinstall hello 종속성:

    ```bash
    npm install
    ```

2. 열기 hello `app.js` 텍스트 편집기에서 파일을 hello 이전에 가져온 이벤트 허브 정보를 추가 합니다.
   
    ```javascript
    // ServiceBus Namespace
    var namespace = 'YourNamespace';
    // Event Hub Name
    var hubname ='sensordata';
    // Shared access Policy name and key (from Event Hub configuration)
    var my_key_name = 'devices';
    var my_key = 'YourKey';
    ```
   
   > [!NOTE]
   > 이 예에서는 사용 했다고 가정 `sensordata` 이벤트 허브의 hello 이름으로 합니다. 해당 `devices` hello 정책에의 hello 이름으로는 `Send` 클레임입니다.

3. 이벤트 허브에서 명령 tooinsert 새 항목을 다음 hello를 사용 합니다.
   
    ```bash
    node app.js
    ```
   
    출력의 hello 데이터를 포함 하는 여러 줄 tooEvent 허브 전송 하는 것이 표시 됩니다.
   
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"0","Temperature":7}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"1","Temperature":39}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"2","Temperature":86}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"3","Temperature":29}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"4","Temperature":30}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"5","Temperature":5}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"6","Temperature":24}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"7","Temperature":40}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"8","Temperature":43}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"9","Temperature":84}

### <a name="build-and-start-hello-topology"></a>빌드하고 hello 토폴로지를 시작 합니다.

1. 새 명령 프롬프트를 열고 디렉터리를 너무 변경`hdinsight-eventhub-example/TemperatureMonitor`합니다. 토폴로지 hello toobuild 및 패키지 다음 명령을 hello를 사용 합니다. 

    ```bash
    mvn clean package
    ```

2. 로컬 모드에서는 다음 명령을 사용 하 여 hello toostart hello 토폴로지:

    ```bash
    storm jar target/TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local --filter dev.properties resources/no-hbase.yaml
    ```

    * `--local`로컬 모드에서 hello 토폴로지를 시작합니다.
    * `--filter`사용 하 여 hello `dev.properties` hello 토폴로지 정의에서 파일 toopopulate 매개 변수입니다.
    * `resources/no-hbase.yaml`사용 하 여 hello `no-hbase.yaml` 토폴로지 정의 합니다.
 
   시작 되 면 hello 토폴로지 이벤트 허브에서 항목을 읽고 하 고 로컬 컴퓨터에서 실행 중인 toohello 대시보드 보냅니다. 다음 이미지와 비슷한 toohello hello 웹 대시보드에 표시 되는 줄이 표시 되어야 합니다.
   
    ![데이터가 표시된 대시보드](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. Hello 대시보드를 실행 하는 동안 사용 하 여 hello `node app.js` 이전 hello에서 명령을 단계 toosend 새 데이터 tooEvent 허브입니다. Hello 온도 값을 임의로 생성 하기 때문에 hello 그래프 tooshow 크게 변경 온도 업데이트 해야 합니다.
   
   > [!NOTE]
   > Hello에 있어야 **hdinsight-eventhub-예/SendEvents/Nodejs** hello를 사용 하는 경우 디렉터리 `node app.js` 명령입니다.

3. Ctrl + C를 사용 하 여 중지 hello 토폴로지 hello 대시보드 해당 업데이트를 확인 한 후 합니다. 또한 Ctrl + C toostop hello 로컬 웹 서버를 사용할 수 있습니다.

## <a name="create-a-storm-and-hbase-cluster"></a>Storm 및 HBase 클러스터 만들기

이 섹션 사용의 단계를 hello는 [Azure 리소스 관리자 템플릿](../azure-resource-manager/resource-group-template-deploy.md) toocreate hello 가상 네트워크에는 Azure 가상 네트워크 및 스톰 및 HBase 클러스터입니다. hello 템플릿 Azure 웹 앱도 만들고에 hello 대시보드의 복사본을 배포 합니다.

> [!NOTE]
> 가상 네트워크는 hello Storm 클러스터에서 실행 되는 hello 토폴로지 hello HBase Java API를 사용 하 여 hello HBase 클러스터와 직접 통신할 수 있도록 사용 됩니다.

이 문서에 사용 되는 hello 리소스 관리자 템플릿을 공용 blob 컨테이너에에 위치한 **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**합니다.

1. Hello tooAzure에서 단추 toosign와 hello Azure 포털에서에서 열기 hello 리소스 관리자 템플릿을 다음를 클릭 합니다.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.6.json" target="_blank"><img src="./media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. Hello에서 **사용자 지정 배포** 섹션에서 다음 값에는 hello를 입력 합니다.
   
    ![HDInsight 매개 변수](./media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * **기본 클러스터 이름을**:이 값 hello hello 스톰 및 HBase 클러스터에 대 한 기본 이름으로 사용 됩니다. 예를 들어 **abc**를 입력하면 **storm-abc**라는 Storm 클러스터와 **hbase-abc**라는 HBase 클러스터가 생성됩니다.
   * **클러스터 로그인 사용자 이름**: hello 스톰 및 HBase 클러스터에 대 한 hello 관리자 사용자 이름입니다.
   * **로그인 암호 클러스터**: hello 스톰 및 HBase 클러스터에 대 한 hello 관리자 사용자 암호입니다.
   * **SSH 사용자 이름이**: hello 스톰 및 HBase 클러스터에 대 한 SSH 사용자 toocreate hello 합니다.
   * **SSH 암호**: hello 스톰 및 HBase 클러스터에 대 한 SSH 사용자 hello에 대 한 hello 암호입니다.
   * **위치**: hello 클러스터에 생성 되는 hello 영역입니다.
     
     클릭 **확인** toosave hello 매개 변수입니다.

3. 사용 하 여 hello **기본 사항** toocreate 리소스 그룹 섹션 또는 기존 템플릿을 선택 합니다.
4. Hello에 **리소스 그룹 위치** hello에 대 한 선택 드롭다운 메뉴에서 선택 hello 동일한 위치 **위치** hello에 대 한 매개 변수 **설정을** 섹션.
5. Hello 사용 약관을 읽고 다음 선택 **toohello 약관 위에서 설명한 동의**합니다.
6. 마지막으로 확인 **Pin toodashboard** 선택한 후 **구매**합니다. Hello 클러스터 toocreate 약 20 분이 필요합니다.

Hello 리소스를 만든 후 hello 리소스 그룹에 대 한 정보가 표시 됩니다.

![Hello vnet 및 클러스터 리소스 그룹](./media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> Hello HDInsight 클러스터의 이름이 hello **스톰 BASENAME** 및 **hbase BASENAME**, 여기서 BASENAME는 hello 이름이 toohello 서식 파일을 제공 합니다. Toohello 클러스터를 연결 하는 경우 이후 단계에서 이러한 이름을 사용 합니다. 또한 hello hello 대시보드 사이트의 이름 메모는 **basename 대시보드**합니다. 이 값은 이 문서의 뒷부분에서 사용됩니다.

## <a name="configure-hello-dashboard-bolt"></a>Hello 대시보드 볼트 구성

toosend 데이터 toohello 대시보드 웹 앱으로 배포를 hello 다음 hello에 줄을 수정 해야 `dev.properties`파일:

```yaml
dashboard.uri: http://localhost:3000
```

변경 `http://localhost:3000` 너무`http://BASENAME-dashboard.azurewebsites.net` hello 파일을 저장 합니다. 대체 **BASENAME** hello 이전 단계에서 제공한 hello 기본 이름을 사용 합니다. 또한 tooselect hello 대시보드 및 보기 hello URL 이전에 만든 hello 리소스 그룹을 사용할 수 있습니다.

## <a name="create-hello-hbase-table"></a>Hello HBase 테이블 만들기

HBase의 데이터를 toostore, 테이블을 먼저 작성 해야 했습니다. 미리 스톰 toowrite를 필요로 하는 리소스를 만들기, toocreate 동일한 리소스 hello 여러 인스턴스 스톰 토폴로지 내에서 toocreate 리소스는 동안 발생할 수 있습니다. Hello 토폴로지 외부 hello 리소스를 만들고 읽기/쓰기 및 분석에 대 한 스톰을 사용 합니다.

1. SSH 사용자 hello 및 클러스터를 만드는 동안 toohello 서식 파일을 입력 한 암호를 사용 하 여 SSH tooconnect toohello HBase 클러스터를 사용 합니다. 예를 들어 hello를 사용 하 여 연결 `ssh` 명령 구문 다음 hello를 사용 합니다.
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```
   
    대체 `sshuser` hello 클러스터를 만들 때 제공한 hello SSH 사용자 이름이 사용 됩니다. 대체 `clustername` hello HBase 클러스터 이름을 사용 합니다.

2. Hello SSH 세션에서 hello HBase 셸을 시작 합니다.
   
    ```bash
    hbase shell
    ```
   
    Hello 셸 로드 되 면 참조는 `hbase(main):001:0>` 프롬프트입니다.

3. HBase 셸 hello에서 hello 명령 toocreate 테이블 toostore hello 센서 데이터를 다음을 입력 합니다.
   
    ```hbase
    create 'SensorData', 'cf'
    ```

4. 다음 명령을 hello를 사용 하 여 해당 hello 테이블 생성 되었는지 확인 합니다.
   
    ```hbase
    scan 'SensorData'
    ```
   
    다음 예에서는, hello 테이블에 행이 0 개 나타내는 비슷한 toohello 정보를 반환 합니다.
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. 입력 `exit` tooexit hello HBase 셸:

## <a name="configure-hello-hbase-bolt"></a>Hello HBase 볼트 구성

hello Storm 클러스터에서 toowrite tooHBase, hello HBase 볼트 HBase 클러스터의 hello 구성 세부 정보를 제공 해야 합니다.

1. Hello HBase 클러스터에 대 한 예제 tooretrieve hello 사육 쿼럼 다음 중 하나를 사용 합니다.

    ```bash
    CLUSTERNAME='your_HDInsight_cluster_name'
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HBASE/components/HBASE_MASTER" | jq '.metrics.hbase.master.ZookeeperQuorum'
    ```

    > [!NOTE]
    > 대체 `your_HDInsight_cluster_name` HDInsight 클러스터의 hello 이름의 합니다. Hello를 설치 하는 방법에 대 한 자세한 내용은 `jq` 유틸리티 참조 [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/)합니다.
    >
    > 메시지가 표시 되 면 hello HDInsight 관리자 로그인에 대 한 hello 암호를 입력 합니다.

    ```powershell
    $clusterName = 'your_HDInsight_cluster_name`
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HBASE/components/HBASE_MASTER" -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.metrics.hbase.master.ZookeeperQuorum
    ```

    > [!NOTE]
    > 대체 ' HDInsight 클러스터의 hello 이름의 your_HDInsight_cluster_name 합니다. 메시지가 표시 되 면 hello HDInsight 관리자 로그인에 대 한 hello 암호를 입력 합니다.
    >
    > 이 예제에서는 Azure PowerShell이 필요합니다. Azure PowerShell 사용에 대한 자세한 내용은 [Azure PowerShell 시작](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)을 참조하세요.

    이러한 예제에서 반환 하는 hello 정보는 텍스트 다음 유사한 toohello:

    `zk2-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk0-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk3-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181`

    이 정보는 스톰 toocommunicate hello HBase 클러스터에서 사용 됩니다.

2. Hello 수정 `dev.properties` 파일을 hello 사육 쿼럼 정보 toohello 다음 줄 추가:

    ```yaml
    hbase.zookeeper.quorum: your_hbase_quorum
    ```

## <a name="build-package-and-deploy-hello-solution-toohdinsight"></a>패키지를 빌드 및 hello 솔루션 tooHDInsight 배포

개발 환경에서 다음 단계 toodeploy hello Storm 토폴로지 toohello storm 클러스터 hello를 사용 합니다.

1. Hello에서 `TemperatureMonitor` 디렉터리 사용 하 여 hello 다음 tooperform 새 빌드 명령 및 프로젝트에서 JAR 패키지 만들기:
   
        mvn clean package
   
    이 명령은 프로젝트의 대상 디렉터리에 `TemperatureMonitor-1.0-SNAPSHOT.jar in hello `라는 파일을 만듭니다.

2. 사용 하 여 scp tooupload hello `TemperatureMonitor-1.0-SNAPSHOT.jar` 및 `dev.properties` 파일 tooyour Storm 클러스터입니다. Hello에서 다음 예제에서는 대체 `sshuser` hello 클러스터를 만들 때 제공한 hello SSH 사용자와 및 `clustername` Storm 클러스터의 hello 이름으로 합니다. 메시지가 표시 되 면 hello SSH 사용자에 대 한 hello 암호를 입력 합니다.
   
    ```bash
    scp target/TemperatureMonitor-1.0-SNAPSHOT.jar dev.properties sshuser@clustername-ssh.azurehdinsight.net:
    ```

   > [!NOTE]
   > Tooupload hello 파일 몇 분 정도 걸릴 수 있습니다.

    Hello를 사용 하 여 대 한 자세한 내용은 `scp` 및 `ssh` HDInsight 사용 하 여 명령을 참조 [SSH HDInsight를 사용](./hdinsight-hadoop-linux-use-ssh-unix.md)

3. Hello 파일에 업로드 되 면 SSH를 사용 하 여 toohello Storm 클러스터를 연결 합니다.
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    대체 `sshuser` hello SSH 사용자 이름이 사용 됩니다. 대체 `clustername` hello Storm 클러스터 이름을 사용 합니다.

4. toostart는 토폴로지 hello, hello 다음 hello SSH 세션에서 명령을 사용 하 여:
   
    ```bash
    storm jar TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote --filter dev.properties -R /with-hbase.yaml
    ```

    * `--remote`hello 토폴로지 toohello hello 클러스터의 toohello 감독자 노드를 배포 하는 Nimbus 서비스에 전송 합니다.
    * `--filter`사용 하 여 hello `dev.properties` hello 토폴로지 정의에서 파일 toopopulate 매개 변수입니다.
    * `-R /with-hbase.yaml`사용 하 여 hello `with-hbase.yaml` 토폴로지 hello 패키지에 포함 합니다.

5. Hello 토폴로지 시작 된 후에 다음 사용 하 여 hello Azure에 게시 된 브라우저 toohello 웹 사이트 열기 `node app.js` 명령 toosend 데이터 tooEvent 허브입니다. Hello 웹 대시보드 업데이트 toodisplay hello 정보를 표시 되어야 합니다.
   
    ![dashboard](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a>HBase 데이터 보기

다음 단계 tooconnect tooHBase hello를 사용 하 여 하 고 있는지 hello에 데이터가 기록 된 toohello 테이블을 확인 합니다.

1. SSH tooconnect toohello HBase 클러스터를 사용 합니다.
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    대체 `sshuser` hello SSH 사용자 이름이 사용 됩니다. 대체 `clustername` hello HBase 클러스터 이름을 사용 합니다.

2. Hello SSH 세션에서 hello HBase 셸을 시작 합니다.
   
    ```bash
    hbase shell
    ```
   
    Hello 셸 로드 되 면 참조는 `hbase(main):001:0>` 프롬프트입니다.

3. Hello 테이블에서 행을 보기:
   
    ```hbase
    scan 'SensorData'
    ```
   
    이 명령은 텍스트 다음, hello 테이블에 데이터를 나타내는 비슷한 toohello 정보를 반환 합니다.
   
        hbase(main):002:0> scan 'SensorData'
        ROW                             COLUMN+CELL
        \x00\x00\x00\x00               column=cf:temperature, timestamp=1467290788277, value=\x00\x00\x00\x04
        \x00\x00\x00\x00               column=cf:timestamp, timestamp=1467290788277, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x01               column=cf:temperature, timestamp=1467290788348, value=\x00\x00\x00M
        \x00\x00\x00\x01               column=cf:timestamp, timestamp=1467290788348, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x02               column=cf:temperature, timestamp=1467290788268, value=\x00\x00\x00R
        \x00\x00\x00\x02               column=cf:timestamp, timestamp=1467290788268, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x03               column=cf:temperature, timestamp=1467290788269, value=\x00\x00\x00#
        \x00\x00\x00\x03               column=cf:timestamp, timestamp=1467290788269, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x04               column=cf:temperature, timestamp=1467290788356, value=\x00\x00\x00>
        \x00\x00\x00\x04               column=cf:timestamp, timestamp=1467290788356, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x05               column=cf:temperature, timestamp=1467290788326, value=\x00\x00\x00\x0D
        \x00\x00\x00\x05               column=cf:timestamp, timestamp=1467290788326, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x06               column=cf:temperature, timestamp=1467290788253, value=\x00\x00\x009
        \x00\x00\x00\x06               column=cf:timestamp, timestamp=1467290788253, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x07               column=cf:temperature, timestamp=1467290788229, value=\x00\x00\x00\x12
        \x00\x00\x00\x07               column=cf:timestamp, timestamp=1467290788229, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x08               column=cf:temperature, timestamp=1467290788336, value=\x00\x00\x00\x16
        \x00\x00\x00\x08               column=cf:timestamp, timestamp=1467290788336, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x09               column=cf:temperature, timestamp=1467290788246, value=\x00\x00\x001
        \x00\x00\x00\x09               column=cf:timestamp, timestamp=1467290788246, value=2015-02-10T14:43.05.00320Z
        10 row(s) in 0.1800 seconds
   
   > [!NOTE]
   > 이 검색 작업 hello 테이블에서 최대 10 개의 행을 반환합니다.

## <a name="delete-your-clusters"></a>클러스터 삭제

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

toodelete hello 클러스터, 저장소 및 웹 응용 프로그램을 포함 하는 hello 리소스 그룹을 삭제 한 번에 합니다.

## <a name="next-steps"></a>다음 단계

HDInsight의 Storm 토폴로지에 대한 자세한 내용은 [HDInsight의 Storm에 대한 예제 토폴로지](hdinsight-storm-example-topology.md)를 참조하세요.

Apache Storm에 대 한 자세한 내용은 참조 hello [Apache Storm](https://storm.incubator.apache.org/) 사이트입니다.

HDInsight에서 HBase에 대 한 자세한 내용은 참조 hello [개요를 HDInsight HBase](hdinsight-hbase-overview.md)합니다.

Socket.io에 대 한 자세한 내용은 참조 hello [socket.io](http://socket.io/) 사이트입니다.

D3.js에 대한 자세한 내용은 [D3.js - 데이터 기반 문서](http://d3js.org/)를 참조하세요.

Java에서 토폴로지를 만들기에 대한 자세한 내용은 [HDInsight의 Apache Storm용 Java 토폴로지 개발](hdinsight-storm-develop-java-topology.md)을 참조하세요.

.NET에서 토폴로지를 만들기에 대한 자세한 내용은 [Visual Studio를 사용하여 HDInsight의 Apache Storm용 C# 토폴로지 개발](hdinsight-storm-develop-csharp-visual-studio-topology.md)을 참조하세요.

[azure-portal]: https://portal.azure.com
