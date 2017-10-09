---
title: "aaaAzure 계산-Linux 진단 확장 | Microsoft Docs"
description: "Tooconfigure는 Azure Linux 진단 확장 (했다) toocollect 메트릭 hello 방법과 Azure에서 실행 중인 Linux Vm에서 이벤트를 기록 합니다."
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 2b27ec00a876ded359a75170b407e28c40d8445d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-linux-diagnostic-extension-toomonitor-metrics-and-logs"></a>Linux 진단 확장 toomonitor 메트릭 및 로그를 사용 하 여

이 문서에서는 버전 3.0 이상 hello Linux 진단 확장을 설명 합니다.

> [!IMPORTANT]
> 2.3 이하 버전에 대한 내용은 [이 문서](./classic/diagnostic-extension-v2.md)를 참조하세요.

## <a name="introduction"></a>소개

Linux 진단 확장 hello Microsoft Azure에서 실행 되는 Linux VM의 사용자 모니터 hello 상태는 데 도움이 됩니다. 기능을 수행 하는 hello 다음과 같습니다.

* Hello VM에서에서 시스템 성능 메트릭을 수집 하 고 지정 된 저장소 계정에 특정 테이블에 저장 합니다.
* Syslog에서 이벤트 로그를 검색 하 고 저장소 계정을 지정 하는 hello의 특정 테이블에 저장 합니다.
* 수집 되 고 업로드 하는 사용자가 toocustomize hello 데이터 메트릭을 수 있습니다.
* 사용자가 toocustomize hello syslog 기능 및 수집 되 고 업로드 하는 이벤트의 심각도 수준이 있습니다.
* 사용자가 tooupload 지정 된 로그 파일 tooa 지정 된 저장소 테이블을 수 있습니다.
* 저장소 계정을 지정 하는 hello에 메트릭 및 로그 이벤트 tooarbitrary EventHub 끝점 및 JSON 형식의 blob를 전송 지원.

이 확장은 Azure 배포 모델 모두에서 작동합니다.

## <a name="installing-hello-extension-in-your-vm"></a>VM에서 hello 확장을 설치합니다.

Hello Azure PowerShell cmdlet, Azure CLI 스크립트 또는 Azure 배포 템플릿을 사용 하 여이 확장을 사용할 수 있습니다. 자세한 내용은 [확장 기능](./extensions-features.md)을 참조하세요.

hello Azure 포털은 했다 3.0 구성 하거나 사용된 tooenable 수 없습니다. 대신 버전 2.3을 설치하고 구성합니다. Azure 포털 그래프 및 경고 hello 확장의 두 버전의 데이터로 작동합니다.

이러한 설치 지침 및 [다운로드 가능한 샘플 구성](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json)은 다음을 수행할 수 있도록 LAD 3.0을 구성합니다.

* 캡처 및 저장소 했다 2.3;에서 제공 하는 대로 동일한 메트릭을 hello합니다
* 유용한 메트릭 집합을 파일 시스템, 새 tooLAD 3.0; 캡처
* 캡처 hello 기본 syslog 수집 했다 2.3;으로 사용 하도록 설정
* 차트 및 VM 메트릭에 대해 경고에 대 한 Azure 포털 환경 hello를 사용 하도록 설정 합니다.

다운로드 가능한 구성 hello은 예 시일 뿐입니다. toosuit 수정 필요 합니다.

### <a name="prerequisites"></a>필수 조건

* **Azure Linux 에이전트 버전 2.2.0 이상**. 대부분의 Azure VM Linux 갤러리 이미지에는 2.2.7 이후 버전이 포함되어 있습니다. 실행 `/usr/sbin/waagent -version` tooconfirm hello 버전 hello VM에 설치 합니다. Hello VM은 이전 버전의 hello 게스트 에이전트를 실행 하는 경우에 따라 [이러한 지침](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate 것입니다.
* **Azure CLI**. [Hello Azure CLI 2.0 설정](https://docs.microsoft.com/cli/azure/install-azure-cli) 환경 컴퓨터에 있습니다.
* 아직 없는 경우 wget 명령 hello: 실행 `sudo apt-get install wget`합니다.
* 기존 Azure 구독 및 기존 저장소 계정 내 toostore hello 데이터입니다.

### <a name="sample-installation"></a>샘플 설치

처음 세 줄 hello hello에 올바른 매개 변수를 채웁니다 루트로이 스크립트를 실행 합니다.

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login tooAzure first before anything else
az login

# Select hello subscription containing hello storage account
az account set --subscription <your_azure_subscription_id>

# Download hello sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build hello VM resource ID. Replace storage account name and resource ID in hello public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build hello protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure tooinstall and enable hello extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

hello 샘플 구성에 대 한 hello URL 및 해당 콘텐츠를 주제 toochange 됩니다. Hello 포털 설정 JSON 파일의 복사본을 다운로드 하 고 필요에 따라 사용자 지정 합니다. 템플릿 또는 자동화를 생성할 때마다 해당 URL을 다운로드하는 대신 고유한 복사본을 사용해야 합니다.

### <a name="updating-hello-extension-settings"></a>Hello 확장 프로그램 설정 업데이트

Protected 또는 공용 설정을 변경한 후 배포할지 toohello VM을 실행 하 여 hello 동일한 명령입니다. Hello 설정에서 변경 된 사항이 업데이트 hello 설정은 toohello 확장을 전송 됩니다. Hello 구성 다시 로드 하 고 자체적으로 다시 시작 하는 야 합니다.

### <a name="migration-from-previous-versions-of-hello-extension"></a>Hello 확장의 이전 버전에서 마이그레이션

hello hello 확장의 최신 버전은 **3.0**합니다. **모든 이전 버전(2.x)은 사용되지 않으며 2018년 7월 31일부터는 게시되지 않을 수 있습니다**.

> [!IMPORTANT]
> 이 확장 프로그램에서는 hello 확장의 주요 변경 내용 toohello 구성을 소개합니다. 한 이러한 변경의 hello 확장; tooimprove hello 보안 결과적으로, 이전 버전과 호환성 2.x 하지 관리할 수 있게 합니다. 또한이 확장에 대 한 hello 확장 게시자는 hello 2.x 버전에 대 한 hello 게시자와 다릅니다.
>
> 2.x toothis 새 버전의 hello 확장 프로그램에서 toomigrate, (hello 이전 게시자 이름에서) 이전 확장명 hello 다음 버전 3 hello 확장의 설치 제거 해야 합니다.

권장 사항:

* 사용 하도록 설정 하는 자동으로 부 버전 업그레이드를 hello 확장을 설치 합니다.
  * 클래식 배포 모델 Vm에 Azure XPLAT CLI 또는 Powershell을 통해 hello 확장을 설치 하는 경우 '3.*' hello 버전으로 지정 합니다.
  * Azure 리소스 관리자 배포에서 Vm 모델을 포함 ' "autoUpgradeMinorVersion": true' hello VM 배포 템플릿에서 합니다.
* LAD 3.0에 대해 새 저장소 계정 또는 다른 저장소 계정을 사용합니다. LAD 2.3과 LAD 3.0 간에 다음과 같은 몇 가지 사소한 비호환성 문제가 있어 계정 공유에 문제가 발생합니다.
  * LAD 3.0은 syslog 이벤트를 이름이 다른 테이블에 저장합니다.
  * 에 대 한 문자열 hello counterSpecifier `builtin` 메트릭 했다 3.0에서 서로 다릅니다.

## <a name="protected-settings"></a>보호 설정

이 구성 정보 집합에는 공용 보기로부터 보호해야 하는 중요한 정보(예: 저장소 자격 증명)가 포함되어 있습니다. 이러한 설정은 전송 된 tooand hello 확장 암호화 된 형식에 의해 저장 됩니다.

```json
{
    "storageAccountName" : "hello storage account tooreceive data",
    "storageAccountEndPoint": "hello hostname suffix for hello cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

이름 | 값
---- | -----
storageAccountName | hello hello 저장소 계정의 이름으로 hello 확장에 의해 데이터가 쓰여집니다.
storageAccountEndPoint | (선택 사항) hello 끝점을 식별 하는 hello 저장소 계정이 존재 하는 hello 클라우드입니다. 했다 toohello Azure 공용 클라우드에서 기본적으로이 설정이 없으면 `https://core.windows.net`합니다. 독일 Azure, Azure Government 또는 Azure 중국에 저장소 계정을 toouse 그에 따라이 값을 설정합니다.
storageAccountSasToken | [계정 SAS 토큰](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) Blob 및 테이블 서비스에 대 한 (`ss='bt'`), 해당 toocontainers 및 개체 (`srt='co'`), 어떤 부여 추가, 생성, 목록, 업데이트 및 쓰기 권한이 (`sp='acluw'`). 수행 *하지* hello 앞에 오는 물음표 (?)를 포함 합니다.
mdsdHttpProxy | (선택 사항) HTTP 프록시는 데 필요한 정보 tooenable hello 확장 tooconnect toohello 저장소 계정 및 끝점을 지정 합니다.
sinksConfig | (선택 사항) 대체 대상 toowhich 메트릭 및 이벤트의 세부 정보를 전달할 수 있습니다. hello hello 확장이 지 원하는 각 데이터 싱크에 대 한 특정 세부 정보는 다음에 나오는 hello 섹션에 설명 되어 있습니다.

Hello Azure 포털을 통해 필요한 hello SAS 토큰을 쉽게 생성할 수 있습니다.

1. Hello 일반적인 용도의 스토리지 계정 toowhich hello 확장 toowrite 원하는 선택
1. "공유 액세스 서명" hello 왼쪽된 메뉴의 hello 설정 부분에서 선택 합니다.
1. 앞에서 설명한 대로 hello 적절 한 섹션을 확인 하십시오.
1. Hello "생성 SAS" 단추를 클릭 합니다.

![이미지](./media/diagnostic-extension/make_sas.png)

복사 hello hello storageAccountSasToken 필드로; SAS 생성 hello 앞에 오는 물음표를 제거 ("?").

### <a name="sinksconfig"></a>sinksConfig

```json
"sinksConfig": {
    "sink": [
        {
            "name": "sinkname",
            "type": "sinktype",
            ...
        },
        ...
    ]
},
```

이 선택적 섹션이 toowhich hello 확장 보냅니다 수집한 정보는 hello 기타 대상을 정의 합니다. hello "sink" 배열에 각각의 추가 데이터 싱크에 대 한 개체를 포함합니다. "type" 특성을 결정 하는 hello hello hello 개체의 다른 특성입니다.

요소 | 값
------- | -----
name | Hello 확장 구성의 다른 곳에서 toorefer toothis 싱크를 사용 하는 문자열입니다.
type | 정의 되 고 싱크의 hello 유형입니다. 이 형식의 인스턴스 (있는 경우) 다른 값을 hello을 결정 합니다.

Hello Linux 진단 확장의 버전 3.0에는 두 싱크 유형을 지원: EventHub, 및 JsonBlob 합니다.

#### <a name="hello-eventhub-sink"></a>hello EventHub 싱크

```json
"sink": [
    {
        "name": "sinkname",
        "type": "EventHub",
        "sasURL": "https SAS URL"
    },
    ...
]
```

hello "sasURL" 항목 포함 hello hello 이벤트 허브 toowhich 데이터에 대 한 SAS 토큰을 포함 한 전체 URL을 게시 해야 합니다. 했다는 hello 송신 클레임을 사용 하는 정책을 명명 SAS 필요 합니다. 예제:

* 호출된 Event Hubs 네임스페이스 만들기`contosohub`
* 호출 하는 hello 네임 스페이스에서 이벤트 허브를 만듭니다.`syslogmsgs`
* Hello 라는 이벤트 허브에서 공유 액세스 정책을 만들고 `writer` 하면 송신 클레임 hello는

만든 경우 SAS 좋은 2018, 년 1 월 1 UTC 자정까지 hello sasURL 값일 수 있습니다.

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

Event Hubs에 대한 SAS 토큰을 생성하는 방법에 대한 자세한 내용은 [이 웹 페이지](../../event-hubs/event-hubs-authentication-and-security-model-overview.md)를 참조하세요.

#### <a name="hello-jsonblob-sink"></a>hello JsonBlob 싱크

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

데이터 전송 tooa JsonBlob 싱크는 Azure 저장소의 blob에 저장 됩니다. 각 LAD 인스턴스는 매시간 각 싱크 이름에 대한 Blob을 만듭니다. 각 Blob에는 항상 구문상 유효한 JSON 배열의 개체가 포함되어 있습니다. 새 항목 toohello 배열을 추가 원자적으로 됩니다. Blob 이름이 hello 싱크 hello 사용 하 여 컨테이너에 저장 됩니다. blob 컨테이너 이름은 JsonBlob 싱크 toohello 이름에 대 한 Azure 저장소 규칙 hello: ASCII 소문자 영숫자와 또는 대시만 3에서 63 사이입니다.

## <a name="public-settings"></a>공용 설정

이 구조는 hello 확장에 의해 수집 된 hello 정보를 제어 하는 설정의 다양 한 요소를 포함 합니다. 각 설정은 선택 사항입니다. `ladCfg`를 지정할 경우 `StorageAccount`도 지정해야 합니다.

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "hello storage account tooreceive data",
    "mdsdHttpProxy" : ""
}
```

요소 | 값
------- | -----
StorageAccount | hello hello 저장소 계정의 이름으로 hello 확장에 의해 데이터가 쓰여집니다. 해야 hello에 지정 되어 이름과 같은 이름을 hello [보호 설정을](#protected-settings)합니다.
mdsdHttpProxy | (선택 사항) Hello와 같이 동일한 [보호 설정을](#protected-settings)합니다. hello 공개 값이 경우 hello 개인 값으로 재정의 설정 합니다. Hello에 암호와 같은 암호를 포함 하는 프록시 설정을 [보호 설정을](#protected-settings)합니다.

hello 나머지 요소는 hello 다음 섹션에서에서 자세히 설명 되어 있습니다.

### <a name="ladcfg"></a>ladCfg

```json
"ladCfg": {
    "diagnosticMonitorConfiguration": {
        "eventVolume": "Medium",
        "metrics": { ... },
        "performanceCounters": { ... },
        "syslogEvents": { ... }
    },
    "sampleRateInSeconds": 15
}
```

이 선택적 구조 컨트롤 hello 수집 메트릭 및 배달 toohello Azure 메트릭 서비스와 tooother 데이터에 대 한 로그 싱크 합니다. `performanceCounters`나 `syslogEvents` 또는 둘 다 지정해야 합니다. Hello를 지정 해야 `metrics` 구조입니다.

요소 | 값
------- | -----
eventVolume | (선택 사항) 컨트롤 hello hello 저장소 테이블 내에서 만든 파티션의 수입니다. `"Large"`, `"Medium"` 또는 `"Small"` 중 하나여야 합니다. Hello 기본값은 지정 하지 않으면 `"Medium"`합니다.
sampleRateInSeconds | (선택 사항) hello 기본 간격 (집계) 원시 메트릭 컬렉션입니다. 가장 작은 지원 hello 샘플링 주기 15 초입니다. Hello 기본값은 지정 하지 않으면 `15`합니다.

#### <a name="metrics"></a>메트릭

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

요소 | 값
------- | -----
resourceId | hello Azure 리소스 관리자 리소스 ID hello 가상 컴퓨터 크기 또는 hello VM의 VM 속한 toowhich hello를 설정 합니다. 이 설정은 해야도 JsonBlob 싱크 hello 구성에 사용 되는 경우를 지정 합니다.
scheduledTransferPeriod | 계산 하 고 tooAzure 메트릭, 8601는 시간 간격으로 표현 된 전송 하는 집계 메트릭을 toobe을는 hello 빈도. hello 가장 짧은 전송 기간은 60 초, 즉, PT1M를입니다. 하나 이상의 scheduledTransferPeriod를 지정해야 합니다.

샘플 hello 샘플링 주기 hello 카운터에 대해 명시적으로 정의 된 또는의 hello hello performanceCounters 섹션에 지정 된 메트릭 15 초 마다 수집 됩니다. 여러 scheduledTransferPeriod 주파수 예와 같이 hello 없으면 각 집계는 독립적으로 계산 합니다.

#### <a name="performancecounters"></a>performanceCounters

```json
"performanceCounters": {
    "sinks": "",
    "performanceCounterConfiguration": [
        {
            "type": "builtin",
            "class": "Processor",
            "counter": "PercentIdleTime",
            "counterSpecifier": "/builtin/Processor/PercentIdleTime",
            "condition": "IsAggregate=TRUE",
            "sampleRate": "PT15S",
            "unit": "Percent",
            "annotation": [
                {
                    "displayName" : "Aggregate CPU %idle time",
                    "locale" : "en-us"
                }
            ]
        }
    ]
}
```

이 선택적 섹션이 메트릭 hello 컬렉션을 제어합니다. 각각에 대해 집계 되는 원시 샘플 [scheduledTransferPeriod](#metrics) tooproduce 이러한 값:

* 평균
* minimum
* maximum
* 마지막으로 수집된 값
* 원시 샘플 수 toocompute hello 집계를 사용합니다.

요소 | 값
------- | -----
sinks | (선택 사항) 이름의 쉼표로 구분 된 목록을 싱크에서 toowhich 했다 집계 된 메트릭 결과 보냅니다. 모든 집계 된 메트릭 나열 하는 게시 된 tooeach 싱크 됩니다. [sinksConfig](#sinksconfig)를 참조하세요. 예: `"EHsink1, myjsonsink"`.
type | Hello hello 메트릭의 실제 공급자를 식별합니다.
class | "Counter"와 함께 hello 공급자의 네임 스페이스 내에서 특정 메트릭을 hello를 식별합니다.
counter | "Class"와 함께 hello 공급자의 네임 스페이스 내에서 특정 메트릭을 hello를 식별합니다.
counterSpecifier | Hello Azure 메트릭 네임 스페이스 내에서 특정 메트릭을 hello를 식별합니다.
condition | (선택 사항) 가 선택 되어 해당 개체의 모든 인스턴스에서 집계 hello 또는 선택 hello 개체 toowhich hello 메트릭의 특정 인스턴스에 적용 됩니다. 자세한 내용은 참조 hello [ `builtin` 메트릭 정의](#metrics-supported-by-builtin)합니다.
sampleRate | 이 메트릭은 대 한 원시 샘플에서 수집 하는 hello 속도 설정 하는 8601 간격이입니다. 을 설정 하지 경우 hello 컬렉션 간격이 hello 값으로 설정 되어 [sampleRateInSeconds](#ladcfg)합니다. 지원 되는 샘플링 주기를 가장 짧은 hello은 15 초 (PT15S).
단위 | 문자열 "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond", "Millisecond" 중 하나여야 합니다. Hello 메트릭에 대 한 hello 단위를 정의 합니다. 수집 된 hello 데이터 소비자에 수집 된 데이터 값 toomatch이이 단위 hello 있기만 하면 됩니다. LAD는 이 필드를 무시합니다.
displayName | hello 언어로 hello hello 관련된 로캘을 설정으로 지정 된 레이블 toobe Azure 메트릭에서 toothis 데이터를 연결 합니다. LAD는 이 필드를 무시합니다.

hello counterSpecifier는 파일과 연결 합니다. Azure 포털 차트 및 경고 기능을 hello 처럼 메트릭의 소비자 메트릭 또는 메트릭 인스턴스를 식별 하는 "키" hello로 counterSpecifier를 사용 합니다. `builtin` 메트릭의 경우 `/builtin/`으로 시작하는 counterSpecifier 값을 사용하는 것이 좋습니다. 특정 인스턴스 메트릭 수집 하는 경우 hello 인스턴스 toohello counterSpecifier 값의 hello 식별자를 연결 하는 것이 좋습니다. 일부 사례:

* `/builtin/Processor/PercentIdleTime` - 모든 코어의 평균 유휴 시간
* `/builtin/Disk/FreeSpace(/mnt)`-Hello /mnt 파일 시스템에 대 한 사용 가능한 공간
* `/builtin/Disk/FreeSpace` - 탑재된 모든 파일 시스템의 평균 사용 가능한 공간

했다 아니고 hello Azure 포털 hello counterSpecifier 값 toomatch 임의의 패턴이 필요합니다. 일관된 방법으로 counterSpecifier 값을 생성해야 합니다.

지정 하는 경우 `performanceCounters`, 했다 Azure 저장소에 항상 tooa 테이블 데이터를 씁니다. 있습니다 수 있는 hello 동일 tooJSON blob 및/또는 이벤트 허브에 기록 된 데이터는 있지만 저장 데이터 tooa 테이블을 비활성화할 수 없습니다. Hello 구성 된 진단 확장 toouse 함수의 모든 인스턴스의 동일한 저장소 계정 이름 및 끝점 추가 자신의 메트릭 및 로그 toohello hello 같은 테이블입니다. 너무 많은 Vm을 작성 하는 조절 하 여 동일한 테이블 파티션에 Azure toohello toothat 파티션을 기록 합니다. 1 (소량), (중간), 10 또는 100 (큼) 서로 다른 파티션을 분산 하는 hello eventVolume 원인을 항목 toobe를 설정 합니다. 일반적으로 "중간"는 충분 한 tooensure 트래픽이 조절 되 되지 않습니다. hello Azure 포털의 hello Azure 메트릭 기능은 hello 또는의 데이터를이 테이블 tooproduce 그래프 tootrigger 경고를 사용합니다. hello 테이블 이름은 이러한 문자열의 hello 연결입니다.

* `WADMetrics`
* hello "scheduledTransferPeriod" hello에 대 한 집계 hello 테이블에 저장 된 값
* `P10DV2S`
* Hello 형태로 "YYYYMMDD" 10 일 마다 변경 날짜

예에는 `WADMetricsPT1HP10DV2S20170410` 및 `WADMetricsPT1MP10DV2S20170609`가 포함됩니다.

#### <a name="syslogevents"></a>syslogEvents

```json
"syslogEvents": {
    "sinks": "",
    "syslogEventConfiguration": {
        "facilityName1": "minSeverity",
        "facilityName2": "minSeverity",
        ...
    }
}
```

이 선택적 섹션이 syslog에서 이벤트 로그의 hello 컬렉션을 제어합니다. Hello 섹션을 생략 하면 syslog 이벤트를 전혀 캡처되지 않습니다.

hello syslogEventConfiguration 컬렉션에 관심 있는 각 syslog 기능에 대 한 하나의 항목이 있습니다. MinSeverity는 특정 기능에 대 한 "NONE" 또는 해당 기능이 표시 되지 않으면 hello 요소에 전혀 해당 시설에서 이벤트가 캡처됩니다.

요소 | 값
------- | -----
sinks | 이름의 쉼표로 구분 된 목록을 싱크에서 toowhich 개별 로그에 이벤트 게시 됩니다. SyslogEventConfiguration의 hello 제한 일치 하는 모든 로그 이벤트는 나열 된 게시 된 tooeach 싱크입니다. 예: "EHforsyslog"
facilityName | syslog 기능 이름입니다(예: "LOG\_USER" 또는 "LOG\_LOCAL0"). Hello의 hello "기능" 섹션을 참조 [syslog 매뉴얼 페이지](http://man7.org/linux/man-pages/man3/syslog.3.html) hello 전체 목록에 대 한 합니다.
minSeverity | syslog 심각도 수준입니다(예: "LOG\_ERR" 또는 "LOG\_INFO"). Hello의 hello "수준" 섹션을 참조 [syslog 매뉴얼 페이지](http://man7.org/linux/man-pages/man3/syslog.3.html) hello 전체 목록에 대 한 합니다. hello 확장에 전송 되는 이벤트 toohello 시설 캡처하거나 hello 위에 수준을 지정 합니다.

지정 하는 경우 `syslogEvents`, 했다 Azure 저장소에 항상 tooa 테이블 데이터를 씁니다. 있습니다 수 있는 hello 동일 tooJSON blob 및/또는 이벤트 허브에 기록 된 데이터는 있지만 저장 데이터 tooa 테이블을 비활성화할 수 없습니다. 이 테이블에 대 한 동작을 분할 하는 hello에 대 한 설명 된 대로 동일한 hello은 `performanceCounters`합니다. hello 테이블 이름은 이러한 문자열의 hello 연결입니다.

* `LinuxSyslog`
* Hello 형태로 "YYYYMMDD" 10 일 마다 변경 날짜

예에는 `LinuxSyslog20170410` 및 `LinuxSyslog20170609`가 포함됩니다.

### <a name="perfcfg"></a>perfCfg

이 선택적 섹션은 임의의 [OMI](https://github.com/Microsoft/omi) 쿼리 실행을 제어합니다.

```json
"perfCfg": [
    {
        "namespace": "root/scx",
        "query": "SELECT PercentAvailableMemory, PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
        "table": "LinuxOldMemory",
        "frequency": 300,
        "sinks": ""
    }
]
```

요소 | 값
------- | -----
namespace | (선택 사항) hello OMI 네임 스페이스는 hello 내에서 쿼리 실행 합니다. 지정 하지 않으면 hello 기본값은 "루트/scx", hello 구현한 [System Center 플랫폼 공급자](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation)합니다.
쿼리 | hello OMI 쿼리 toobe를 실행 합니다.
테이블 | (선택 사항) hello Azure 저장소 테이블 저장소 계정을 지정 하는 hello (참조 [보호 설정을](#protected-settings)).
frequency | (선택 사항) hello 개수 hello 쿼리의 실행 간격 (초)입니다. 기본값은 300(5분)이고 최소값은 15초입니다.
sinks | (선택 사항) 추가 싱크 toowhich 원시 샘플 메트릭 결과의 이름의 쉼표로 구분 된 목록을 게시 되어야 합니다. Hello 확장명 또는 Azure 메트릭을 원시 이러한 샘플의 집계가 계산 됩니다.

"table"이나 "sinks" 또는 둘 다 지정해야 합니다.

### <a name="filelogs"></a>fileLogs

로그 파일의 컨트롤 hello를 캡처합니다. 했다는 텍스트 줄 바꿈을 toohello 파일에 작성 된 것 처럼 캡처하고 tootable 행 및/또는 모든 지정 된 싱크 (JsonBlob 또는 EventHub) 씁니다.

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

요소 | 값
------- | -----
file | 로그 파일 toobe hello의 전체 경로 이름을 hello 조사를 캡처한 합니다. hello pathname 단일 파일의 이름 이어야 합니다. 디렉터리의 이름을 두거나 와일드 카드를 포함할 수 없습니다.
테이블 | (선택 사항) hello Azure 저장소 테이블 hello 지정 된 저장소 계정 (지정 된 대로 보호 된 hello 구성에서), 새 줄에 hello 작성 된 "비상" hello 파일에서에서 합니다.
sinks | (선택 사항) 추가 싱크 toowhich 로그 선의 이름의 쉼표로 구분 된 목록을 전송 합니다.

"table"이나 "sinks" 또는 둘 다 지정해야 합니다.

## <a name="metrics-supported-by-hello-builtin-provider"></a>Hello 기본 제공 공급자가 지 원하는 메트릭

hello builtin 메트릭 공급자가 메트릭 가장 흥미로운 tooa 광범위 한 사용자 집합의 원본입니다. 이러한 메트릭은 다음과 같은 다섯 가지 광범위한 클래스에 속합니다.

* 프로세서
* 메모리
* 네트워크
* 파일 시스템
* 디스크

### <a name="builtin-metrics-for-hello-processor-class"></a>hello 프로세서 클래스에 대 한 기본 제공 된 메트릭

hello 프로세서 클래스 메트릭 VM hello 프로세서 사용에 대 한 정보를 제공합니다. 백분율을 집계 하는 경우에 hello 결과 모든 Cpu에서 hello 평균 합니다. 두 개의 코어 VM에서에서 한 코어 100% 사용 중 이며 다른 hello 100% 유휴 hello 보고 PercentIdleTime 50이 됩니다. 각 코어에 대 한 사용 중 50%가 hello 동일한 기간 hello 보고 결과 50도 될 수 있습니다. 4 코어 VM, 단일 코어 100% 사용 중 및 hello 유휴 상태, 다른 hello 보고 PercentIdleTime 75 됩니다.

counter | 의미
------- | -------
PercentIdleTime | Hello 집계 창 프로세서가 hello 커널 유휴 루프를 실행 하는 동안 있는 시간의 백분율
PercentProcessorTime | 비 유휴 스레드를 실행하는 시간의 백분율
PercentIOWaitTime | IO 작업 toocomplete에 대 한 대기 시간의 백분율
PercentInterruptTime | 하드웨어/소프트웨어 인터럽트 및 DPC(지연된 프로시저 호출)를 실행하는 시간의 백분율
PercentUserTime | Hello 집계 기간 동안 유휴 상태가 아닌 시간 보통 우선 순위로 보다 사용자에 소요 된 시간의 hello 백분율
PercentNiceTime | 비 유휴 시간의 낮아진된 (좋은) 우선 순위에 소요 된 hello 백분율
PercentPrivilegedTime | 비 유휴 시간의 권한 (커널) 모드에 소요 된 hello 백분율

hello 처음 네 개의 카운터 합계 too100%입니다. hello 마지막 세 개의 카운터를 합계 too100%; 이러한 세분화 PercentProcessorTime, PercentIOWaitTime, 및 PercentInterruptTime hello 합계입니다.

모든 프로세서에서 단일 메트릭을 집계 tooobtain 설정 `"condition": "IsAggregate=TRUE"`합니다. 특정 프로세서에 대 한 메트릭을 tooobtain hello 두 번째 논리 프로세서의 4 코어 VM을 같은 설정 `"condition": "Name=\\"1\\""`합니다. Hello 범위에 있는 논리 프로세서 번호 `[0..n-1]`합니다.

### <a name="builtin-metrics-for-hello-memory-class"></a>hello 메모리 클래스에 대 한 기본 제공 된 메트릭

hello 메트릭 메모리 클래스 메모리 사용률, 페이징 및 교환에 대 한 정보를 제공 합니다.

counter | 의미
------- | -------
AvailableMemory | 사용 가능한 실제 메모리(MiB)
PercentAvailableMemory | 총 메모리 중 사용 가능한 실제 메모리의 백분율
UsedMemory | 사용 중인 실제 메모리(MiB)
PercentUsedMemory | 총 메모리 중 사용 중인 실제 메모리의 백분율
PagesPerSec | 총 페이징(읽기/쓰기)
PagesReadPerSec | 백업 저장소(스왑 파일, 프로그램 파일, 매핑된 파일 등)에서 읽은 페이지
PagesWrittenPerSec | Toobacking 쓴 페이지 저장소 (스왑 파일, 매핑된 파일 등)
AvailableSwap | 사용하지 않는 스왑 공간(MiB)
PercentAvailableSwap | 총 스왑 중 사용하지 않은 스왑 공간의 백분율
UsedSwap | 사용 중인 스왑 공간(MiB)
PercentUsedSwap | 총 스왑 중 사용 중인 스왑 공간의 백분율

이 메트릭 클래스에는 인스턴스가 하나만 있습니다. hello "조건" 특성에 유용한 설정이 없는 및 생략 해야 합니다.

### <a name="builtin-metrics-for-hello-network-class"></a>hello 네트워크 클래스에 대 한 기본 제공 된 메트릭

hello 네트워크 클래스입니다. 메트릭 부팅 후 경과 개별 네트워크 인터페이스에 네트워크 작업에 대 한 정보를 제공합니다. LAD는 대역폭 메트릭을 노출하지 않으며 이는 호스트 메트릭에서 검색할 수 있습니다.

counter | 의미
------- | -------
BytesTransmitted | 부팅 이후 보낸 총 바이트
BytesReceived | 부팅 이후 받은 총 바이트
BytesTotal | 부팅 이후 보내거나 받은 총 바이트
PacketsTransmitted | 부팅 이후 보낸 총 패킷
PacketsReceived | 부팅 이후 받은 총 패킷
TotalRxErrors | 부팅 이후 수신 오류 수
TotalTxErrors | 부팅 이후 전송 오류 수
TotalCollisions | 부팅 후 경과 hello 네트워크 포트에서 보고 된 충돌 수

 이 클래스가 인스턴스화되더라도 LAD는 모든 네트워크 장치에서 집계되는 네트워크 메트릭을 캡처하지 않습니다. t h 0, 등의 특정 인터페이스에 대 한 tooobtain hello 메트릭을 설정 `"condition": "InstanceID=\\"eth0\\""`합니다.

### <a name="builtin-metrics-for-hello-filesystem-class"></a>파일 시스템 클래스 hello에 대 한 기본 제공 메트릭

hello 메트릭의 파일 시스템 클래스는 파일 시스템 사용에 대 한 정보를 제공합니다. Absolute 및 백분율 값 표시 tooan 일반 사용자 (루트)와 같이 보고 됩니다.

counter | 의미
------- | -------
FreeSpace | 사용 가능한 디스크 공간(바이트)
UsedSpace | 사용된 디스크 공간(바이트)
PercentFreeSpace | 사용 가능한 공간의 백분율
PercentUsedSpace | 사용된 공간의 백분율
PercentFreeInodes | 사용하지 않은 inode의 백분율
PercentUsedInodes | 모든 파일 시스템에서 합한 할당된(사용 중인) inode의 백분율
BytesReadPerSecond | 초당 읽은 바이트
BytesWrittenPerSecond | 초당 쓴 바이트
초당 바이트 수 | 초당 읽거나 쓴 바이트
ReadsPerSecond | 초당 읽기 작업
WritesPerSecond | 초당 쓰기 작업
TransfersPerSecond | 초당 읽기 또는 쓰기 작업

`"condition": "IsAggregate=True"`로 설정하면 모든 파일 시스템에서 집계된 값을 얻을 수 있습니다. `"condition": 'Name="/mnt"'`로 설정하면 특정 탑재된 파일 시스템(예: "/mnt")에 대한 값을 얻을 수 있습니다.

### <a name="builtin-metrics-for-hello-disk-class"></a>hello 디스크 클래스에 대 한 기본 제공 된 메트릭

hello 메트릭 디스크 클래스 디스크 장치 사용에 대 한 정보를 제공합니다. 이러한 통계는 toohello 전체 드라이브를 적용합니다. 장치에서 여러 파일 시스템이 있는 경우 해당 장치에 대 한 hello 카운터 인 효과적으로 모두에 걸쳐 집계 합니다.

counter | 의미
------- | -------
ReadsPerSecond | 초당 읽기 작업
WritesPerSecond | 초당 쓰기 작업
TransfersPerSecond | 초당 총 작업
AverageReadTime | 읽기 작업당 평균 시간(초)
AverageWriteTime | 쓰기 작업당 평균 시간(초)
AverageTransferTime | 작업당 평균 시간(초)
AverageDiskQueueLength | 대기 중인 디스크 작업의 평균 수
ReadBytesPerSecond | 초당 읽은 바이트 수
WriteBytesPerSecond | 초당 쓴 바이트 수
초당 바이트 수 | 초당 읽거나 쓴 바이트 수

`"condition": "IsAggregate=True"`로 설정하면 모든 디스크에서 집계된 값을 얻을 수 있습니다. tooget 정보 (예를 들어/개발/sdf1), 특정 장치에 대 한 설정 `"condition": "Name=\\"/dev/sdf1\\""`합니다.

## <a name="installing-and-configuring-lad-30-via-cli"></a>CLI를 통해 LAD 3.0 설치 및 구성

보호 된 설정을 PrivateConfig.json hello 파일에 있으며 PublicConfig.json에 공용 구성 정보는 라고 가정할 경우이 명령을 입력 합니다.

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

hello 명령은 hello Azure CLI의 hello Azure 리소스 관리 모드 (arm)를 사용 하는 것을 가정 합니다. 클래식 배포에 대 한 했다 tooconfigure (ASM) Vm 모델, 너무 전환 "asm" 모드 (`azure config mode asm`) hello 명령에 hello 리소스 그룹 이름은 생략 합니다. 자세한 내용은 참조 hello [CLI 설명서의 플랫폼 간](https://docs.microsoft.com/azure/xplat-cli-connect)합니다.

## <a name="an-example-lad-30-configuration"></a>LAD 3.0 구성 예제

Hello 앞에와 몇 가지 설명 했다 3.0 확장 샘플 구성이 정의 여기의 기반으로 합니다. tooapply이 샘플 tooyour 사례 EventHubs SAS 토큰 및 저장소 계정 이름을 사용 하 여, SAS 토큰을 계정 해야 합니다.

### <a name="privateconfigjson"></a>PrivateConfig.json

개인 설정은 다음을 구성합니다.

* 저장소 계정
* 일치하는 계정 SAS 토큰
* 여러 싱크(SAS 토큰이 있는 EventHubs 또는 JsonBlob)

```json
{
  "storageAccountName": "yourdiagstgacct",
  "storageAccountSasToken": "sv=xxxx-xx-xx&ss=bt&srt=co&sp=wlacu&st=yyyy-yy-yyT21%3A22%3A00Z&se=zzzz-zz-zzT21%3A22%3A00Z&sig=fake_signature",
  "sinksConfig": {
    "sink": [
      {
        "name": "SyslogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "FilelogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "MyJsonMetricsBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=fake_signature&se=1808096361&skn=yourehpolicy"
      },
      {
        "name": "MyMetricEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&skn=yourehpolicy"
      },
      {
        "name": "LoggingEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&se=1808096361&skn=yourehpolicy"
      }
    ]
  }
}
```

### <a name="publicconfigjson"></a>PublicConfig.json

공용 설정으로 LAD는 다음을 수행합니다.

* % 프로세서 시간 및 디스크 사용-공간 메트릭을 toohello 업로드 `WADMetrics*` 테이블
* 메시지에서 syslog 기능 "user" 및 심각도 "info" toohello 업로드 `LinuxSyslog*` 테이블
* 원시 OMI 쿼리 결과 (PercentProcessorTime 및 PercentIdleTime) toohello 라는 업로드 `LinuxCPU` 테이블
* 파일에서 추가 된 줄 업로드 `/var/log/myladtestlog` toohello `MyLadTestLog` 테이블

각각의 경우 데이터는 다음으로 업로드됩니다.

* Azure Blob 저장소 (컨테이너 이름은 hello JsonBlob 싱크에 정의 된 대로)
* EventHubs 끝점 (지정 된 대로 hello EventHubs 싱크에서)

```json
{
  "StorageAccount": "yourdiagstgacct",
  "sampleRateInSeconds": 15,
  "ladCfg": {
    "diagnosticMonitorConfiguration": {
      "performanceCounters": {
        "sinks": "MyMetricEventHub,MyJsonMetricsBlob",
        "performanceCounterConfiguration": [
          {
            "unit": "Percent",
            "type": "builtin",
            "counter": "PercentProcessorTime",
            "counterSpecifier": "/builtin/Processor/PercentProcessorTime",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Aggregate CPU %utilization"
              }
            ],
            "condition": "IsAggregate=TRUE",
            "class": "Processor"
          },
          {
            "unit": "Bytes",
            "type": "builtin",
            "counter": "UsedSpace",
            "counterSpecifier": "/builtin/FileSystem/UsedSpace",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Used disk space on /"
              }
            ],
            "condition": "Name=\"/\"",
            "class": "Filesystem"
          }
        ]
      },
      "metrics": {
        "metricAggregation": [
          {
            "scheduledTransferPeriod": "PT1H"
          },
          {
            "scheduledTransferPeriod": "PT1M"
          }
        ],
        "resourceId": "/subscriptions/your_azure_subscription_id/resourceGroups/your_resource_group_name/providers/Microsoft.Compute/virtualMachines/your_vm_name"
      },
      "eventVolume": "Large",
      "syslogEvents": {
        "sinks": "SyslogJsonBlob,LoggingEventHub",
        "syslogEventConfiguration": {
          "LOG_USER": "LOG_INFO"
        }
      }
    }
  },
  "perfCfg": [
    {
      "query": "SELECT PercentProcessorTime, PercentIdleTime FROM SCX_ProcessorStatisticalInformation WHERE Name='_TOTAL'",
      "table": "LinuxCpu",
      "frequency": 60,
      "sinks": "LinuxCpuJsonBlob,LinuxCpuEventHub"
    }
  ],
  "fileLogs": [
    {
      "file": "/var/log/myladtestlog",
      "table": "MyLadTestLog",
      "sinks": "FilelogJsonBlob,LoggingEventHub"
    }
  ]
}
```

hello `resourceId` hello에서 구성 설정의 hello VM 또는 hello 가상 컴퓨터 크기는 일치 해야 합니다.

* Azure 플랫폼 메트릭 차트 및 경고의 VM에서 작업 하는 hello hello resourceId를 알고 있습니다. Hello resourceId hello 조회 키를 사용 하 여 VM에 대 한 toofind hello 데이터를 필요로 합니다.
* Azure 자동 크기 조정을 사용 하는 경우 hello 자동 크기 조정 구성에 hello resourceId hello resourceId 했다에서 사용 하는 일치 해야 합니다.
* hello resourceId 했다 기록한 JsonBlobs의 hello 이름으로 만들어집니다.

## <a name="view-your-data"></a>데이터 보기

Hello Azure 포털 tooview 성능 데이터를 사용 하 여 또는 알림 설정:

![이미지](./media/diagnostic-extension/graph_metrics.png)

hello `performanceCounters` 데이터는 항상 Azure 저장소 테이블에 저장 됩니다. Azure Storage API는 다양한 언어 및 플랫폼에 사용할 수 있습니다.

데이터 전송 tooJsonBlob 싱크 hello에 명명 된 hello 저장소 계정에서 blob에 저장 됩니다 [보호 설정을](#protected-settings)합니다. 모든 Azure Blob 저장소 Api를 사용 하 여 hello blob 데이터를 사용할 수 있습니다.

또한 Azure 저장소에 이러한 UI 도구 tooaccess hello 데이터를 사용할 수 있습니다.

* Visual Studio 서버 탐색기.
* [Microsoft Azure Storage 탐색기](https://azurestorageexplorer.codeplex.com/ "Azure Storage 탐색기").

이 스냅숏을 Microsoft Azure 저장소 탐색기 세션의 테스트 VM에서 올바르게 구성 된 했다 3.0 확장 프로그램에서 Azure 저장소 테이블 및 컨테이너를 생성 하는 hello를 표시 합니다. hello 이미지 hello 정확히 일치 하지 않습니다. [샘플 했다 3.0 구성](#an-example-lad-30-configuration)합니다.

![이미지](./media/diagnostic-extension/stg_explorer.png)

Hello 관련 참조 [EventHubs 설명서](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn tooconsume 메시지 tooan EventHubs 끝점을 게시 하는 방법입니다.

## <a name="next-steps"></a>다음 단계

* 메트릭 경고를 만들 [Azure 모니터](../../monitoring-and-diagnostics/insights-alerts-portal.md) hello 메트릭 수집에 대 한 합니다.
* 메트릭에 대한 [모니터링 차트](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md)를 만듭니다.
* 너무 방법에 대해 알아봅니다[가상 컴퓨터 크기 집합을 만들](/azure/virtual-machines/linux/tutorial-create-vmss) 메트릭 toocontrol 자동 크기 조정을 사용 하 여 합니다.
