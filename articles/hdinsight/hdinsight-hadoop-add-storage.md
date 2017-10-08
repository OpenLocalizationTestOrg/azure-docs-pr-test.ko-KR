---
title: "aaaAdd 추가 Azure 저장소 계정 tooHDInsight | Microsoft Docs"
description: "어떻게 tooadd 추가 Azure 저장소 계정 tooan 기존 HDInsight 클러스터에 알아봅니다."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: ce5acfa4b61bf7e83b1fb374d64a1eaa3182fbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-additional-storage-accounts-toohdinsight"></a>추가 저장소 계정을 tooHDInsight 추가

Toouse 스크립트 작업 tooadd 추가 Azure 저장소 tooHDInsight를 계정 하는 방법에 대해 알아봅니다. hello이 문서의 단계는 저장소 계정 tooan 기존 Linux 기반 HDInsight 클러스터를 추가합니다.

> [!IMPORTANT]
> 만든 후에 추가 저장소 tooa 클러스터를 추가 하는 방법에 대 한이 문서의 hello 정보가입니다. 클러스터를 만드는 동안 저장소 계정을 추가하는 방법에 대한 자세한 내용은 [Hadoop, Spark, Kafka 등으로 HDInsight에서 클러스터를 설정](hdinsight-hadoop-provision-linux-clusters.md)을 참조하세요.

## <a name="how-it-works"></a>작동 방법

이 스크립트는 hello 매개 변수 뒤에 사용 됩니다.

* __Azure 저장소 계정 이름__: hello 저장소 계정 tooadd toohello HDInsight 클러스터의 hello 이름입니다. Hello 스크립트를 실행 한 후 HDInsight 읽고이 저장소 계정에 저장 된 데이터를 쓸 수 있습니다.

* __Azure 저장소 계정 키__: toohello 저장소 계정 액세스를 부여 하는 키입니다.

* __-p__ (선택 사항): 지정을 hello 키 암호화 되지 않은 하 고 일반 텍스트로 hello 코어 site.xml 파일에 저장 됩니다.

처리 하는 동안 hello 스크립트 hello 다음 작업을 수행 합니다.

* Hello 저장소 계정에 이미 있으면 hello 클러스터에 대 한 hello 코어 site.xml 구성 hello 스크립트가 종료 하 고 더 이상 매크로 수행 되도록 합니다.

* Hello 저장소 계정이 있고 hello 키를 사용 하 여 액세스할 수 있는지 확인 합니다.

* Hello 클러스터 자격 증명을 사용 하 여 hello 키를 암호화 합니다.

* Hello 저장소 계정 toohello site.xml 코어 파일을 추가합니다.

* 중지 하 고 hello Oozie, YARN, MapReduce2, 및 HDFS 서비스를 다시 시작 합니다. 이러한 서비스를 시작 및 중지 toouse hello 새로운 저장소 계정이 있습니다.

> [!WARNING]
> 저장소 계정을 사용 하 여 hello HDInsight 클러스터와 다른 위치에서 지원 되지 않습니다.

## <a name="hello-script"></a>hello 스크립트

__스크립트 위치__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)

__요구 사항__:

* hello에 hello 스크립트를 적용 해야 __헤드 노드__합니다.

## <a name="toouse-hello-script"></a>toouse hello 스크립트

이 스크립트는 Azure PowerShell hello Azure 포털에서에서 사용할 수 있습니다 또는 Azure CLI 1.0 hello 합니다. 자세한 내용은 참조 hello [스크립트 동작을 사용 하 여 사용자 지정 하는 Linux 기반 HDInsight 클러스터](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) 문서.

> [!IMPORTANT]
> Hello 사용자 지정 문서에서 제공 하는 hello 단계를 사용할 때 정보 tooapply 다음 hello이이 스크립트를 사용 합니다.
>
> * 이 스크립트 (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)에 대 한 hello URI가 있는 예제 스크립트 동작 URI를 대체 합니다.
> * Hello Azure 저장소 계정 이름과 키 hello 저장소 계정 toobe toohello 추가 된 클러스터의 모든 예에서는 매개 변수 대체 합니다. Azure 포털을 hello를 사용 하 여, 경우 이러한 매개 변수를 공백으로 구분 되어야 합니다.
> * 이 스크립트도 toomark를 불필요 __Persisted__hello 클러스터에 대 한 hello Ambari 구성을 직접 업데이트 될 때, 합니다.

## <a name="known-issues"></a>알려진 문제

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a>Azure Portal 또는 도구에 저장소 계정이 표시되지 않음

Hello Azure 포털에서에서 보기 hello HDInsight 클러스터를 선택을 선택 하면 hello __저장소 계정은__ 항목 __속성__ 이 스크립트 동작을 통해 추가 된 저장소 계정에 표시 되지 않습니다. Azure PowerShell 및 Azure CLI 표시 되지 않습니다 hello 추가 저장소 계정 중 하나입니다.

hello 저장소 정보 hello 스크립트 hello 클러스터에 대 한 hello 코어 site.xml 구성을 수정 하기 때문에 표시 되지 않습니다. 이 정보는 Azure 관리 Api를 사용 하 여 hello 클러스터 정보를 검색할 때 사용 되지 않습니다.

tooview 저장소 계정 정보는이 스크립트를 사용 하 여 hello Ambari REST API를 사용 하 여 toohello 클러스터를 추가 합니다. 클러스터에 대 한 hello 명령을 tooretrieve 다음이 정보를 사용 합니다.

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter hello cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> 설정 `$clusterName` hello HDInsight 클러스터의 toohello 이름입니다. 설정 `$storageAccountName` toohello hello 저장소 계정의 이름입니다. 메시지가 표시 되 면 hello 클러스터 로그인 (관리자)과 암호를 입력 합니다.

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> 설정 `$PASSWORD` toohello 클러스터 로그인 (관리자) 계정 암호입니다. 설정 `$CLUSTERNAME` hello HDInsight 클러스터의 toohello 이름입니다. 설정 `$STORAGEACCOUNTNAME` toohello hello 저장소 계정의 이름입니다.
>
> 이 예에서는 [curl (http://curl.haxx.se/)](http://curl.haxx.se/) 및 [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) JSON 데이터 tooretrieve 및 구문 분석 합니다.

이 명령을 사용 하는 경우 대체 __CLUSTERNAME__ hello HDInsight 클러스터의 hello 이름을 사용 합니다. 대체 __암호__ hello 클러스터에 대 한 HTTP hello 로그인 암호를 사용 합니다. 대체 __STORAGEACCOUNT__ 와 hello hello 저장소 계정의 이름으로 스크립트 동작을 사용 하 여 추가 합니다. 이 명령에서 반환 된 정보는 텍스트 다음 유사한 toohello 나타납니다.

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

이 텍스트에 사용 되는 암호화 된 키의 예는 tooaccess hello 저장소 계정입니다.

### <a name="unable-tooaccess-storage-after-changing-key"></a>없습니다 tooaccess 저장소 키를 변경한 후

저장소 계정에 대 한 hello 키를 변경 하면 HDInsight hello 저장소 계정을 더 이상 액세스할 수 없습니다. HDInsight은 hello 클러스터에 대 한 hello 코어 site.xml에서 키의 캐시 된 복사본을 사용합니다. 이 캐시 된 복사본에 업데이트 된 toomatch hello에 대 한 새 키 여야 합니다.

hello 스크립트 작업을 다시 실행 __하지__ hello 스크립트 hello 저장소 계정에 대 한 항목이 이미 있으면 toosee를 확인 하는 대로 hello 키를 업데이트 합니다. 항목이 존재하는 경우 변경하지 않습니다.

이 문제를 해결 toowork, hello 저장소 계정에 대 한 hello 기존 항목을 제거 해야 합니다. 다음 단계 tooremove hello 기존 항목 hello를 사용 합니다.

1. 웹 브라우저에서 HDInsight 클러스터에 대 한 hello Ambari 웹 UI를 엽니다. hello URI https://CLUSTERNAME.azurehdinsight.net입니다. 대체 __CLUSTERNAME__ 클러스터의 hello 이름을 사용 합니다.

    메시지가 표시 되 면 클러스터에 대 한 hello HTTP 로그인 사용자 및 암호를 입력 합니다.

2. Hello hello hello 페이지 왼쪽에 있는 서비스 목록에서 선택 __HDFS__합니다. 다음 hello 선택 __Configs__ hello 센터 hello 페이지의 탭 합니다.

3. Hello에 __필터...__  필드의 값을 입력 합니다. __fs.azure.account__합니다. Toohello 클러스터에 추가 된 모든 추가 저장소 계정에 대 한 항목을 반환 합니다. 항목에는 두 가지 유형, __keyprovider__와 __key__가 있습니다. 둘 다 hello 키 이름의 일부로 hello 저장소 계정의 hello 이름을 포함합니다.

    hello 다음은 라는 저장소 계정에 대 한 예제 항목 __mystorage__:

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. Tooremove 필요한 hello 저장소 계정에 대 한 hello 키를 식별 한 후 사용 하 여 hello 빨간색 '-' hello 항목 toodelete의 오른쪽 아이콘 toohello 것입니다. 다음 hello를 사용 하 여 __저장__ toosave 변경 내용을 단추입니다.

5. 변경 내용을 저장 한 후 hello 스크립트 작업 tooadd hello 저장소 계정 및 새 키 값 toohello 클러스터를 사용 합니다.

### <a name="poor-performance"></a>성능 저하

저장소 계정 hello hello HDInsight 클러스터와 다른 지역에 있으면 성능이 저하를 발생할 수 있습니다. 다른 지역 보냅니다 네트워크 트래픽이 hello 지역의 Azure 데이터 센터 외부와 across 데이터 액세스 hello 공용 인터넷을 지연이 발생할 수 있습니다.

> [!WARNING]
> Hello HDInsight 클러스터와 다른 지역에서 저장소 계정을 사용 하는 지원 되지 않습니다.

### <a name="additional-charges"></a>추가 요금

이면 hello 저장소 계정이 다른 지역에 HDInsight 클러스터를 hello 보다 사용자 Azure 청구에 추가 전송 요금을 확인할 수 있습니다. 데이터가 지역 데이터 센터를 떠날 때 송신 요금이 부과됩니다. 대금이 청구는 다른 지역에 있는 다른 Azure 데이터 센터에 대 한 hello 트래픽을 전송 하는 경우에 적용 됩니다.

> [!WARNING]
> Hello HDInsight 클러스터와 다른 지역에서 저장소 계정을 사용 하는 지원 되지 않습니다.

## <a name="next-steps"></a>다음 단계

추가 저장소 tooadd tooan 기존 HDInsight 클러스터를 계정 하는 방법을 배웠습니다. 스크립트 동작에 대한 자세한 내용은 [스크립트 동작을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)를 참조하세요.
