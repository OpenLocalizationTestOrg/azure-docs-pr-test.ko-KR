---
title: "로 Kafka-Azure HDInsight Spark 구조적 스트리밍을 aaaApache | Microsoft Docs"
description: "자세한 내용은 방법 toouse Apache Spark 스트리밍 (DStream) tooget 데이터 Apache Kafka 안팎으로 합니다. 이 예제에서는 HDInsight의 Spark에서 Jupyter Notebook을 사용하여 데이터를 스트리밍합니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/09/2017
ms.author: larryfr
ms.openlocfilehash: 0837e8fc5ea314e644daed029d596feeb2b02c68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a>HDInsight의 Kafka(미리 보기)에서 Spark 구조적 스트림 사용

자세한 내용은 방법 toouse Azure HDInsight의 Apache Kafka에서 Spark 구조적 스트리밍 tooread 데이터입니다.

Spark 구조적 스트림은 Spark SQL에서 작성된 스트림 처리 엔진입니다. 에 수 있습니다 hello tooexpress 스트리밍 계산 하면 일괄 처리 계산와 동일 정적 데이터입니다. 구조적 스트리밍에 대 한 자세한 내용은 참조 hello [구조적 스트리밍 프로그래밍 가이드 [알파]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) Apache.org에서 합니다.

> [!IMPORTANT]
> 이 예제에서는 HDInsight 3.6에서 Spark 2.1을 사용했습니다. 구조적 스트림은 Spark 2.1에서 __알파__로 간주합니다.
>
> 이 문서의 단계 hello HDInsight의 Spark와 HDInsight 클러스터에서 Kafka 모두 포함 된 Azure 리소스 그룹을 만듭니다. 이 클러스터는 Spark 클러스터 toodirectly hello를는 Azure 가상 네트워크 내에 위치한 둘 다 hello Kafka 클러스터와 통신 합니다.
>
> Hello이이 문서의 단계를 완료 하는 경우 toodelete hello 클러스터 tooavoid 초과 요금을 기억 합니다.

## <a name="create-hello-clusters"></a>Hello 클러스터를 만들려면

HDInsight의 Apache Kafka에서는 액세스 toohello Kafka 브로커를 통해 공용 인터넷 hello 합니다. 토론에 tooKafka 있어야 hello hello 노드로 동일한 Azure 가상 네트워크는 모든 작업이 hello Kafka 클러스터입니다. 예를 들어 hello Kafka 및 Spark 클러스터를 모두 Azure 가상 네트워크에 있는 합니다. hello 다음 그림에 hello 클러스터 간의 통신 흐름 방식을:

![Azure 가상 네트워크에 있는 Spark 및 Kafka 클러스터 다이어그램](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> hello Kafka 서비스는 hello 가상 네트워크 내에서 제한 된 toocommunication입니다. Hello 클러스터에 있는 다른 서비스 Ambar 및 SSH를 통해 액세스할 수와 같은 인터넷 hello 합니다. HDInsight와 사용할 수 있는 공용 포트 hello에 대 한 자세한 내용은 참조 하십시오. [포트 및 HDInsight에서 사용 하는 Uri](hdinsight-hadoop-port-settings-for-services.md)합니다.

수동으로 만들 수 있습니다는 Azure 가상 네트워크에서 Kafka, 및 Spark 클러스터를 보다 쉽게 Azure 리소스 관리자 템플릿 toouse는. 사용 하 여 hello 다음 단계는 Azure 가상 네트워크, Kafka toodeploy 및 Spark 클러스터 tooyour Azure 구독.

1. Hello tooAzure에서 단추 toosign 및 hello Azure 포털에서에서 열기 hello 서식 파일을 사용 합니다.
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    hello Azure 리소스 관리자 템플릿에 위치한 **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**합니다.

    이 템플릿은 hello 다음 리소스를 만듭니다.

    * HDInsight 3.5 클러스터의 Kafka
    * HDInsight 3.6 클러스터의 Spark
    * Azure 가상 네트워크를 hello HDInsight 클러스터를 포함 합니다.

    > [!IMPORTANT]
    > 이 예에서 사용 된 hello 구조적된 스트리밍 노트북 3.6 HDInsight의 Spark 필요 합니다. HDInsight의 Spark의 이전 버전을 사용 하는 경우 hello 노트북을 사용 하는 경우 오류가 발생 합니다.

2. 정보 toopopulate hello 항목에 나오는 hello에 사용 하 여 hello **사용자 지정 배포** 블레이드:
   
    ![HDInsight 사용자 지정 배포](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * **리소스 그룹**: 그룹을 만들거나 기존 그룹을 선택합니다. 이 그룹 hello HDInsight 클러스터를 포함합니다.

    * **위치**: 위치 지리적으로 닫기 tooyou를 선택 합니다.

    * **기본 클러스터 이름을**:이 값 hello hello Kafka 및 Spark 클러스터에 대 한 기본 이름으로 사용 됩니다. 예를 들어, **hdi**를 입력하면 spark-hdi__라는 Spark 클러스터와 **kafka-hdi**라는 Kafka 클러스터가 만들어집니다.

    * **클러스터 로그인 사용자 이름**: hello Kafka 및 Spark 클러스터에 대 한 hello 관리자 사용자 이름입니다.

    * **로그인 암호 클러스터**: hello Kafka 및 Spark 클러스터에 대 한 hello 관리자 사용자 암호입니다.

    * **SSH 사용자 이름이**: hello Kafka 및 Spark 클러스터에 대 한 SSH 사용자 toocreate hello 합니다.

    * **SSH 암호**: hello Kafka 및 Spark 클러스터에 대 한 SSH 사용자 hello에 대 한 hello 암호입니다.

3. 읽기 hello **약관**를 선택한 후 **toohello 약관 위에서 설명한 동의**합니다.

4. 마지막으로 확인 **Pin toodashboard** 선택한 후 **구매**합니다. Hello 클러스터 toocreate 약 20 분이 필요합니다.

Hello 리소스를 만든 리디렉션된 toohello 리소스 그룹 블레이드 됩니다.

![Hello vnet 및 클러스터 리소스 그룹 블레이드](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> Hello HDInsight 클러스터의 이름이 hello **spark BASENAME** 및 **kafka BASENAME**, 여기서 BASENAME는 hello 이름이 toohello 서식 파일을 제공 합니다. Toohello 클러스터를 연결 하는 경우 이후 단계에서 이러한 이름을 사용 합니다.

## <a name="get-hello-kafka-brokers"></a>Hello Kafka 브로커 가져오기

hello이 예제 코드에서는 연결 toohello Kafka broker hello Kafka 클러스터의에서 호스트입니다. toofind는 Kafka 브로커 호스트 hello, 다음 PowerShell 또는 Bash 예제 hello를 사용 하 여:

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
$clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$brokerHosts = $respObj.host_components.HostRoles.host_name
($brokerHosts -join ":9092,") + ":9092"
```

```bash
curl -u admin:$PASSWORD -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")'
```

> [!NOTE]
> 이 예에서는 `$PASSWORD` hello 클러스터 로그인에 대 한 toocontain hello 암호 및 `$CLUSTERNAME` toocontain hello 이름 hello Kafka 클러스터입니다.
>
> 이 예에서는 hello [jq](https://stedolan.github.io/jq/) hello JSON 문서에서 유틸리티 tooparse 데이터입니다.

hello는 텍스트 다음 비슷한 toohello 출력:

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

Hello 다음이 문서의 섹션에서에서 사용 중 이므로이 정보를 저장 합니다.

## <a name="get-hello-notebooks"></a>Hello 전자 필기장 가져오기

이 문서에서 설명 하는 hello 예제에 대 한 hello 코드에서 사용할 수는 [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming)합니다.

## <a name="upload-hello-notebooks"></a>Hello 전자 필기장 업로드

HDInsight 클러스터에서 단계 tooupload hello 전자 필기장 hello 프로젝트 tooyour Spark에서에서 다음 hello를 사용 합니다.

1. 웹 브라우저에서 toohello Jupyter 노트북 Spark 클러스터에 연결 합니다. Hello에서 url을 대체 `CLUSTERNAME` Kafka 클러스터의 hello 이름의:

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    메시지가 표시 되 면 hello 클러스터 로그인 (관리자)과 hello 클러스터를 만들 때 사용한 암호를 입력 합니다.

2. Hello의 오른쪽 상단 hello 페이지에서 hello를 사용 하 여 __업로드__ 단추 tooupload hello __스트림 트 윗 To_Kafka.ipynb__ 파일 toohello 클러스터입니다. 선택 __열려__ toostart hello 업로드 합니다.

    ![업로드 단추 tooselect hello를 사용 하 여 및 노트북 업로드](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![Hello KafkaStreaming.ipynb 파일 선택](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. Hello __스트림 트 윗 To_Kafka.ipynb__ hello 전자 필기장 및 선택 목록에 항목 __업로드__ 단추가 있습니다.

    ![사용 하 여 hello 업로드 단추 hello KafkaStreaming.ipynb 항목 tooupload 것 toohello 노트북 서버](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. 1-3 tooload hello 단계를 반복 __Spark-구성-스트리밍 액세스에서-Kafka.ipynb__ 노트북 합니다.

## <a name="load-tweets-into-kafka"></a>Kafka로 트윗 로드

Hello 파일 업로드 되었지만 되 면 선택 hello __스트림 트 윗 To_Kafka.ipynb__ 항목 tooopen hello 노트북 합니다. Kafka에 hello 노트북 tooload 트 윗의 hello 단계를 수행 합니다.

## <a name="process-tweets-using-spark-structured-streaming"></a>Spark 구조적 스트림을 사용하여 트윗 프로세스

Hello Jupyter 노트북 홈 페이지에서에서 선택 hello __Spark-구성-스트리밍 액세스에서-Kafka.ipynb__ 항목입니다. Spark 구조적 스트리밍을 사용 하 여 Kafka에서 hello 노트북 tooload 트 윗의 hello 단계를 수행 합니다.

## <a name="next-steps"></a>다음 단계

배웠습니다 했으므로 Spark 구조적 스트리밍 toouse hello Kafka Spark와 작업 하는 방법에 대 한 자세한 문서 toolearn 다음을 확인 하는 방법:

* [어떻게 toouse 멤버 Kafka와 스트리밍 (DStream)](hdinsight-apache-spark-with-kafka.md)합니다.
* [Jupyter Notebook 및 HDInsight의 Spark 시작](hdinsight-apache-spark-jupyter-spark-sql.md)