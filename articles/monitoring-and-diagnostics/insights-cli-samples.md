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
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a><span data-ttu-id="314d1-105">Azure Monitor 플랫폼 간 CLI 1.0 빠른 시작 샘플</span><span class="sxs-lookup"><span data-stu-id="314d1-105">Azure Monitor  Cross-platform CLI 1.0 quick start samples</span></span>
<span data-ttu-id="314d1-106">Azure 모니터 기능에 액세스 하는 CLI (명령줄 인터페이스) 명령 toohelp 샘플이 문서를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="314d1-106">This article shows you sample command-line interface (CLI) commands toohelp you access Azure Monitor features.</span></span> <span data-ttu-id="314d1-107">Azure 모니터를 사용 하면 구성 된 원격 분석 데이터의 값을 기반으로 하는 호출 웹 Url 또는 tooAutoScale 클라우드 서비스, 가상 컴퓨터 및 웹 앱 및 toosend 경고 알림.</span><span class="sxs-lookup"><span data-stu-id="314d1-107">Azure Monitor allows you tooAutoScale Cloud Services, Virtual Machines, and Web Apps and toosend alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="314d1-108">Azure 모니터는 2016 년 9 월 25 일 때까지 "Azure Insights" 라고 불렀습니다 기능에 대 한 새 이름을 hello는입니다.</span><span class="sxs-lookup"><span data-stu-id="314d1-108">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="314d1-109">그러나 hello 네임 스페이스 및 아래의 hello 명령 insights"hello" 여전히 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="314d1-109">However, hello namespaces and thus hello commands below still contain hello "insights".</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="314d1-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="314d1-110">Prerequisites</span></span>
<span data-ttu-id="314d1-111">Hello Azure CLI를 아직 설치 하지 않은 경우 참조 [설치 hello Azure CLI](../cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="314d1-111">If you haven't already installed hello Azure CLI, see [Install hello Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="314d1-112">Azure CLI 모르는 경우 읽어볼 수 있는에서 항목에 대 한 [사용 하 여 hello Mac, Linux 및 Windows Azure 리소스 관리자에 대 한 Azure CLI](../xplat-cli-azure-resource-manager.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="314d1-112">If you're unfamiliar with Azure CLI, you can read more about it at [Use hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../xplat-cli-azure-resource-manager.md).</span></span>

<span data-ttu-id="314d1-113">Windows에서 hello에서 npm 설치 [Node.js 웹 사이트](https://nodejs.org/)합니다.</span><span class="sxs-lookup"><span data-stu-id="314d1-113">In Windows, install npm from hello [Node.js website](https://nodejs.org/).</span></span> <span data-ttu-id="314d1-114">Hello 설치를 마친 후 관리자 권한으로 실행 권한으로 CMD.exe를 사용 하 여 다음 실행 하 hello npm 설치 되어 있는 hello 폴더에서:</span><span class="sxs-lookup"><span data-stu-id="314d1-114">After you complete hello installation, using CMD.exe with Run As Administrator privileges, execute hello following from hello folder where npm is installed:</span></span>

```console
npm install azure-cli --global
```

<span data-ttu-id="314d1-115">다음으로 이동 tooany 폴더/원하는 위치 hello 명령줄에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="314d1-115">Next, navigate tooany folder/location you want and type at hello command-line:</span></span>

```console
azure help
```

## <a name="log-in-tooazure"></a><span data-ttu-id="314d1-116">TooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="314d1-116">Log in tooAzure</span></span>
<span data-ttu-id="314d1-117">hello 첫 번째 단계는 toologin tooyour Azure 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="314d1-117">hello first step is toologin tooyour Azure account.</span></span>

```console
azure login
```

<span data-ttu-id="314d1-118">이 명령을 실행 한 후가지고 toosign hello 화면에 대 한 hello 지침을 통해 합니다.</span><span class="sxs-lookup"><span data-stu-id="314d1-118">After running this command, you have toosign in via hello instructions on hello screen.</span></span> <span data-ttu-id="314d1-119">그러면 계정, 테넌트 ID 및 기본 구독 ID가 표시됩니다. 모든 명령이 기본 구독의 hello 컨텍스트에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="314d1-119">Afterward, you see your Account, TenantId, and default Subscription Id. All commands work in hello context of your default subscription.</span></span>

<span data-ttu-id="314d1-120">현재 구독 다음 명령을 사용 하 여 hello toolist hello 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="314d1-120">toolist hello details of your current subscription, use hello following command.</span></span>

```console
azure account show
```

<span data-ttu-id="314d1-121">toochange 작업 컨텍스트 tooa 다른 구독, 다음 명령을 사용 하 여 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="314d1-121">toochange working context tooa different subscription, use hello following command.</span></span>

```console
azure account set "subscription ID or subscription name"
```

<span data-ttu-id="314d1-122">toouse Azure 리소스 관리자 및 Azure 모니터의 명령을 toobe Azure 리소스 관리자 모드에서 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="314d1-122">toouse Azure Resource Manager and Azure Monitor commands, you need toobe in Azure Resource Manager mode.</span></span>

```console
azure config mode arm
```

<span data-ttu-id="314d1-123">지원 되는 모든 Azure 모니터 명령 목록이 tooview hello 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="314d1-123">tooview a list of all supported Azure Monitor commands, perform hello following.</span></span>

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a><span data-ttu-id="314d1-124">구독에 대한 활동 로그 보기</span><span class="sxs-lookup"><span data-stu-id="314d1-124">View activity log for a subscription</span></span>
<span data-ttu-id="314d1-125">활동 로그 이벤트 목록이 tooview hello 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="314d1-125">tooview a list of activity log events, perform hello following.</span></span>

```console
azure insights logs list [options]
```

<span data-ttu-id="314d1-126">사용 가능한 옵션 모두 다음 tooview hello를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="314d1-126">Try hello following tooview all available options.</span></span>

```console
azure insights logs list -help
```

<span data-ttu-id="314d1-127">다음은 예제 toolist 로그는 리소스 그룹으로</span><span class="sxs-lookup"><span data-stu-id="314d1-127">Here is an example toolist logs by a resourceGroup</span></span>

```console
azure insights logs list --resourceGroup "myrg1"
```

<span data-ttu-id="314d1-128">호출자가 예제 toolist 로그</span><span class="sxs-lookup"><span data-stu-id="314d1-128">Example toolist logs by caller</span></span>

```console
azure insights logs list --caller "myname@company.com"
```

<span data-ttu-id="314d1-129">시작 및 종료 날짜 내에서 리소스 종류에는 호출자가 예제 toolist 로그</span><span class="sxs-lookup"><span data-stu-id="314d1-129">Example toolist logs by caller on a resource type, within a start and end date</span></span>

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a><span data-ttu-id="314d1-130">경고 작업</span><span class="sxs-lookup"><span data-stu-id="314d1-130">Work with alerts</span></span>
<span data-ttu-id="314d1-131">경고 섹션 toowork hello에에서 hello 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="314d1-131">You can use hello information in hello section toowork with alerts.</span></span>

### <a name="get-alert-rules-in-a-resource-group"></a><span data-ttu-id="314d1-132">리소스 그룹의 경고 규칙 가져오기</span><span class="sxs-lookup"><span data-stu-id="314d1-132">Get alert rules in a resource group</span></span>
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a><span data-ttu-id="314d1-133">메트릭 경고 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="314d1-133">Create a metric alert rule</span></span>
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a><span data-ttu-id="314d1-134">웹 테스트 경고 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="314d1-134">Create webtest alert rule</span></span>
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a><span data-ttu-id="314d1-135">경고 규칙 삭제</span><span class="sxs-lookup"><span data-stu-id="314d1-135">Delete an alert rule</span></span>
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a><span data-ttu-id="314d1-136">로그 프로필</span><span class="sxs-lookup"><span data-stu-id="314d1-136">Log profiles</span></span>
<span data-ttu-id="314d1-137">이 섹션 toowork 로그 프로필의 hello 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="314d1-137">Use hello information in this section toowork with log profiles.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="314d1-138">로그 프로필 가져오기</span><span class="sxs-lookup"><span data-stu-id="314d1-138">Get a log profile</span></span>
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a><span data-ttu-id="314d1-139">보존하지 않는 로그 프로필 추가</span><span class="sxs-lookup"><span data-stu-id="314d1-139">Add a log profile without retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="314d1-140">로그 프로필 제거</span><span class="sxs-lookup"><span data-stu-id="314d1-140">Remove a log profile</span></span>
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a><span data-ttu-id="314d1-141">보존하는 로그 프로필 추가</span><span class="sxs-lookup"><span data-stu-id="314d1-141">Add a log profile with retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="314d1-142">보존하는 로그 프로필 및 이벤트 허브 추가</span><span class="sxs-lookup"><span data-stu-id="314d1-142">Add a log profile with retention and EventHub</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a><span data-ttu-id="314d1-143">진단</span><span class="sxs-lookup"><span data-stu-id="314d1-143">Diagnostics</span></span>
<span data-ttu-id="314d1-144">진단 설정 사용 하 여이 섹션 toowork의 hello 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="314d1-144">Use hello information in this section toowork with diagnostic settings.</span></span>

### <a name="get-a-diagnostic-setting"></a><span data-ttu-id="314d1-145">진단 설정 가져오기</span><span class="sxs-lookup"><span data-stu-id="314d1-145">Get a diagnostic setting</span></span>
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a><span data-ttu-id="314d1-146">진단 설정 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="314d1-146">Disable a diagnostic setting</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a><span data-ttu-id="314d1-147">보존하지 않는 진단 설정 사용</span><span class="sxs-lookup"><span data-stu-id="314d1-147">Enable a diagnostic setting without retention</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a><span data-ttu-id="314d1-148">Autoscale</span><span class="sxs-lookup"><span data-stu-id="314d1-148">Autoscale</span></span>
<span data-ttu-id="314d1-149">자동 크기 조정 설정 사용 하 여이 섹션 toowork의 hello 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="314d1-149">Use hello information in this section toowork with autoscale settings.</span></span> <span data-ttu-id="314d1-150">이러한 예제 toomodify 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="314d1-150">You need toomodify these examples.</span></span>

### <a name="get-autoscale-settings-for-a-resource-group"></a><span data-ttu-id="314d1-151">리소스 그룹에 대한 자동 크기 조정 설정 가져오기</span><span class="sxs-lookup"><span data-stu-id="314d1-151">Get autoscale settings for a resource group</span></span>
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a><span data-ttu-id="314d1-152">리소스 그룹의 이름으로 자동 크기 조정 설정 가져오기</span><span class="sxs-lookup"><span data-stu-id="314d1-152">Get autoscale settings by name in a resource group</span></span>
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a><span data-ttu-id="314d1-153">자동 크기 조정 설정 지정</span><span class="sxs-lookup"><span data-stu-id="314d1-153">Set auotoscale settings</span></span>
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```
