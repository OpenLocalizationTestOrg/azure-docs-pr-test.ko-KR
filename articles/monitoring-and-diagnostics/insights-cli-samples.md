---
title: "빠른 시작 샘플 aaaAzure 모니터 CLI 1.0입니다. | Microsoft Docs"
description: "Azure Monitor 기능에 대한 샘플 CLI 1.0 명령입니다. Azure 모니터는 경고 알림 toosend 수 있는 Microsoft Azure 서비스, 구성 된 원격 분석 데이터 및 자동 크기 조정 클라우드 서비스, 가상 컴퓨터 및 웹 응용 프로그램의 값을 기반으로 하는 호출 웹 Url입니다."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 1653aa81-0ee6-4622-9c65-d4801ed9006f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 6cd9cd62b3a1977276563f5e43f5384ccca66247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a>Azure Monitor 플랫폼 간 CLI 1.0 빠른 시작 샘플
Azure 모니터 기능에 액세스 하는 CLI (명령줄 인터페이스) 명령 toohelp 샘플이 문서를 표시 합니다. Azure 모니터를 사용 하면 구성 된 원격 분석 데이터의 값을 기반으로 하는 호출 웹 Url 또는 tooAutoScale 클라우드 서비스, 가상 컴퓨터 및 웹 앱 및 toosend 경고 알림.

> [!NOTE]
> Azure 모니터는 2016 년 9 월 25 일 때까지 "Azure Insights" 라고 불렀습니다 기능에 대 한 새 이름을 hello는입니다. 그러나 hello 네임 스페이스 및 아래의 hello 명령 insights"hello" 여전히 포함 합니다.
> 
> 

## <a name="prerequisites"></a>필수 조건
Hello Azure CLI를 아직 설치 하지 않은 경우 참조 [설치 hello Azure CLI](../cli-install-nodejs.md)합니다. Azure CLI 모르는 경우 읽어볼 수 있는에서 항목에 대 한 [사용 하 여 hello Mac, Linux 및 Windows Azure 리소스 관리자에 대 한 Azure CLI](../xplat-cli-azure-resource-manager.md)합니다.

Windows에서 hello에서 npm 설치 [Node.js 웹 사이트](https://nodejs.org/)합니다. Hello 설치를 마친 후 관리자 권한으로 실행 권한으로 CMD.exe를 사용 하 여 다음 실행 하 hello npm 설치 되어 있는 hello 폴더에서:

```console
npm install azure-cli --global
```

다음으로 이동 tooany 폴더/원하는 위치 hello 명령줄에 입력 합니다.

```console
azure help
```

## <a name="log-in-tooazure"></a>TooAzure 로그인
hello 첫 번째 단계는 toologin tooyour Azure 계정입니다.

```console
azure login
```

이 명령을 실행 한 후가지고 toosign hello 화면에 대 한 hello 지침을 통해 합니다. 그러면 계정, 테넌트 ID 및 기본 구독 ID가 표시됩니다. 모든 명령이 기본 구독의 hello 컨텍스트에서 작동 합니다.

현재 구독 다음 명령을 사용 하 여 hello toolist hello 세부 정보입니다.

```console
azure account show
```

toochange 작업 컨텍스트 tooa 다른 구독, 다음 명령을 사용 하 여 hello 합니다.

```console
azure account set "subscription ID or subscription name"
```

toouse Azure 리소스 관리자 및 Azure 모니터의 명령을 toobe Azure 리소스 관리자 모드에서 필요 합니다.

```console
azure config mode arm
```

지원 되는 모든 Azure 모니터 명령 목록이 tooview hello 다음을 수행 합니다.

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a>구독에 대한 활동 로그 보기
활동 로그 이벤트 목록이 tooview hello 다음을 수행 합니다.

```console
azure insights logs list [options]
```

사용 가능한 옵션 모두 다음 tooview hello를 시도 하십시오.

```console
azure insights logs list -help
```

다음은 예제 toolist 로그는 리소스 그룹으로

```console
azure insights logs list --resourceGroup "myrg1"
```

호출자가 예제 toolist 로그

```console
azure insights logs list --caller "myname@company.com"
```

시작 및 종료 날짜 내에서 리소스 종류에는 호출자가 예제 toolist 로그

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a>경고 작업
경고 섹션 toowork hello에에서 hello 정보를 사용할 수 있습니다.

### <a name="get-alert-rules-in-a-resource-group"></a>리소스 그룹의 경고 규칙 가져오기
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a>메트릭 경고 규칙 만들기
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a>웹 테스트 경고 규칙 만들기
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a>경고 규칙 삭제
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a>로그 프로필
이 섹션 toowork 로그 프로필의 hello 정보를 사용 합니다.

### <a name="get-a-log-profile"></a>로그 프로필 가져오기
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a>보존하지 않는 로그 프로필 추가
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a>로그 프로필 제거
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a>보존하는 로그 프로필 추가
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a>보존하는 로그 프로필 및 이벤트 허브 추가
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a>진단
진단 설정 사용 하 여이 섹션 toowork의 hello 정보를 사용 합니다.

### <a name="get-a-diagnostic-setting"></a>진단 설정 가져오기
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a>진단 설정 사용 안 함
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a>보존하지 않는 진단 설정 사용
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a>Autoscale
자동 크기 조정 설정 사용 하 여이 섹션 toowork의 hello 정보를 사용 합니다. 이러한 예제 toomodify 필요합니다.

### <a name="get-autoscale-settings-for-a-resource-group"></a>리소스 그룹에 대한 자동 크기 조정 설정 가져오기
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a>리소스 그룹의 이름으로 자동 크기 조정 설정 가져오기
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a>자동 크기 조정 설정 지정
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```
