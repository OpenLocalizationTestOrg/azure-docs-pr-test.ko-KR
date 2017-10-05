---
title: "Azure Monitor CLI 1.0 빠른 시작 샘플 | Microsoft Docs"
description: "Azure Monitor 기능에 대한 샘플 CLI 1.0 명령입니다. Azure Monitor는 Cloud Services, Virtual Machines 및 Web Apps의 크기를 자동으로 조정하고, 구성된 원격 분석 데이터 값을 기반으로 경고 알림을 보내거나 웹 URL을 호출할 수 있는 Microsoft Azure 서비스입니다."
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
ms.openlocfilehash: ec4512500dc3c77a40d2ebd1e6b460d5bb005811
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a><span data-ttu-id="d393c-105">Azure Monitor 플랫폼 간 CLI 1.0 빠른 시작 샘플</span><span class="sxs-lookup"><span data-stu-id="d393c-105">Azure Monitor  Cross-platform CLI 1.0 quick start samples</span></span>
<span data-ttu-id="d393c-106">이 문서에서는 Azure Monitor 기능에 액세스하는 데 유용한 샘플 CLI(명령줄 인터페이스) 명령을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d393c-106">This article shows you sample command-line interface (CLI) commands to help you access Azure Monitor features.</span></span> <span data-ttu-id="d393c-107">Azure Monitor를 통해 Cloud Services, Virtual Machines 및 Web Apps의 크기를 자동으로 조정하고, 구성된 원격 분석 데이터의 값을 기반으로 경고 알림을 보내거나 웹 URL을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d393c-107">Azure Monitor allows you to AutoScale Cloud Services, Virtual Machines, and Web Apps and to send alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="d393c-108">Azure Monitor는 2016년 9월 25일까지는 "Azure Insights"로 지칭했던 제품의 새로운 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d393c-108">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="d393c-109">하지만 네임스페이스와 아래 명령에서는 "insights"를 계속 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d393c-109">However, the namespaces and thus the commands below still contain the "insights".</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="d393c-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d393c-110">Prerequisites</span></span>
<span data-ttu-id="d393c-111">이미 Azure CLI를 설치하지 않은 경우 [Azure CLI 설치](../cli-install-nodejs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d393c-111">If you haven't already installed the Azure CLI, see [Install the Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="d393c-112">Azure CLI를 잘 모르는 경우 자세한 내용은 [Azure Resource Manager에서 Mac, Linux 및 Windows용 Azure CLI 사용](../xplat-cli-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d393c-112">If you're unfamiliar with Azure CLI, you can read more about it at [Use the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../xplat-cli-azure-resource-manager.md).</span></span>

<span data-ttu-id="d393c-113">Windows의 경우 [Node.js 웹 사이트](https://nodejs.org/)에서 npm을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d393c-113">In Windows, install npm from the [Node.js website](https://nodejs.org/).</span></span> <span data-ttu-id="d393c-114">설치를 완료한 후 관리자 권한으로 실행 권한으로 CMD.exe를 사용하여 npm이 설치된 폴더에서 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d393c-114">After you complete the installation, using CMD.exe with Run As Administrator privileges, execute the following from the folder where npm is installed:</span></span>

```console
npm install azure-cli --global
```

<span data-ttu-id="d393c-115">원하는 폴더/위치로 이동하여 명령줄에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d393c-115">Next, navigate to any folder/location you want and type at the command-line:</span></span>

```console
azure help
```

## <a name="log-in-to-azure"></a><span data-ttu-id="d393c-116">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="d393c-116">Log in to Azure</span></span>
<span data-ttu-id="d393c-117">첫 번째 단계에서는 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d393c-117">The first step is to login to your Azure account.</span></span>

```console
azure login
```

<span data-ttu-id="d393c-118">이 명령을 실행한 후 화면의 지시에 따라 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d393c-118">After running this command, you have to sign in via the instructions on the screen.</span></span> <span data-ttu-id="d393c-119">그러면 계정, 테넌트 ID 및 기본 구독 ID가 표시됩니다. 모든 명령은 기본 구독의 컨텍스트에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="d393c-119">Afterward, you see your Account, TenantId, and default Subscription Id. All commands work in the context of your default subscription.</span></span>

<span data-ttu-id="d393c-120">현재 구독에 대한 세부 정보를 나열하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d393c-120">To list the details of your current subscription, use the following command.</span></span>

```console
azure account show
```

<span data-ttu-id="d393c-121">작업 중인 컨텍스트를 다른 구독으로 변경하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d393c-121">To change working context to a different subscription, use the following command.</span></span>

```console
azure account set "subscription ID or subscription name"
```

<span data-ttu-id="d393c-122">Azure Resource Manager 및 Azure Monitor 명령을 사용하려면 Azure Resource Manager 모드에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d393c-122">To use Azure Resource Manager and Azure Monitor commands, you need to be in Azure Resource Manager mode.</span></span>

```console
azure config mode arm
```

<span data-ttu-id="d393c-123">지원되는 모든 Azure Monitor 명령 목록을 보려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d393c-123">To view a list of all supported Azure Monitor commands, perform the following.</span></span>

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a><span data-ttu-id="d393c-124">구독에 대한 활동 로그 보기</span><span class="sxs-lookup"><span data-stu-id="d393c-124">View activity log for a subscription</span></span>
<span data-ttu-id="d393c-125">활동 로그 이벤트 목록을 보려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d393c-125">To view a list of activity log events, perform the following.</span></span>

```console
azure insights logs list [options]
```

<span data-ttu-id="d393c-126">사용 가능한 모든 옵션을 보려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d393c-126">Try the following to view all available options.</span></span>

```console
azure insights logs list -help
```

<span data-ttu-id="d393c-127">다음은 resourceGroup별 로그를 나열하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="d393c-127">Here is an example to list logs by a resourceGroup</span></span>

```console
azure insights logs list --resourceGroup "myrg1"
```

<span data-ttu-id="d393c-128">호출자별 로그를 나열하는 예제</span><span class="sxs-lookup"><span data-stu-id="d393c-128">Example to list logs by caller</span></span>

```console
azure insights logs list --caller "myname@company.com"
```

<span data-ttu-id="d393c-129">시작 날짜 및 종료 날짜 내 리소스 유형에 대한 호출자별 로그를 나열하는 예제</span><span class="sxs-lookup"><span data-stu-id="d393c-129">Example to list logs by caller on a resource type, within a start and end date</span></span>

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a><span data-ttu-id="d393c-130">경고 작업</span><span class="sxs-lookup"><span data-stu-id="d393c-130">Work with alerts</span></span>
<span data-ttu-id="d393c-131">이 섹션의 정보를 사용하여 경고 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d393c-131">You can use the information in the section to work with alerts.</span></span>

### <a name="get-alert-rules-in-a-resource-group"></a><span data-ttu-id="d393c-132">리소스 그룹의 경고 규칙 가져오기</span><span class="sxs-lookup"><span data-stu-id="d393c-132">Get alert rules in a resource group</span></span>
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a><span data-ttu-id="d393c-133">메트릭 경고 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="d393c-133">Create a metric alert rule</span></span>
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a><span data-ttu-id="d393c-134">웹 테스트 경고 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="d393c-134">Create webtest alert rule</span></span>
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a><span data-ttu-id="d393c-135">경고 규칙 삭제</span><span class="sxs-lookup"><span data-stu-id="d393c-135">Delete an alert rule</span></span>
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a><span data-ttu-id="d393c-136">로그 프로필</span><span class="sxs-lookup"><span data-stu-id="d393c-136">Log profiles</span></span>
<span data-ttu-id="d393c-137">이 섹션의 정보를 사용하여 로그 프로필 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d393c-137">Use the information in this section to work with log profiles.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="d393c-138">로그 프로필 가져오기</span><span class="sxs-lookup"><span data-stu-id="d393c-138">Get a log profile</span></span>
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a><span data-ttu-id="d393c-139">보존하지 않는 로그 프로필 추가</span><span class="sxs-lookup"><span data-stu-id="d393c-139">Add a log profile without retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="d393c-140">로그 프로필 제거</span><span class="sxs-lookup"><span data-stu-id="d393c-140">Remove a log profile</span></span>
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a><span data-ttu-id="d393c-141">보존하는 로그 프로필 추가</span><span class="sxs-lookup"><span data-stu-id="d393c-141">Add a log profile with retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="d393c-142">보존하는 로그 프로필 및 이벤트 허브 추가</span><span class="sxs-lookup"><span data-stu-id="d393c-142">Add a log profile with retention and EventHub</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a><span data-ttu-id="d393c-143">진단</span><span class="sxs-lookup"><span data-stu-id="d393c-143">Diagnostics</span></span>
<span data-ttu-id="d393c-144">이 섹션의 정보를 사용하여 진단 설정 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d393c-144">Use the information in this section to work with diagnostic settings.</span></span>

### <a name="get-a-diagnostic-setting"></a><span data-ttu-id="d393c-145">진단 설정 가져오기</span><span class="sxs-lookup"><span data-stu-id="d393c-145">Get a diagnostic setting</span></span>
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a><span data-ttu-id="d393c-146">진단 설정 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="d393c-146">Disable a diagnostic setting</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a><span data-ttu-id="d393c-147">보존하지 않는 진단 설정 사용</span><span class="sxs-lookup"><span data-stu-id="d393c-147">Enable a diagnostic setting without retention</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a><span data-ttu-id="d393c-148">Autoscale</span><span class="sxs-lookup"><span data-stu-id="d393c-148">Autoscale</span></span>
<span data-ttu-id="d393c-149">이 섹션의 정보를 사용하여 자동 크기 조정 설정 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d393c-149">Use the information in this section to work with autoscale settings.</span></span> <span data-ttu-id="d393c-150">이러한 예제를 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d393c-150">You need to modify these examples.</span></span>

### <a name="get-autoscale-settings-for-a-resource-group"></a><span data-ttu-id="d393c-151">리소스 그룹에 대한 자동 크기 조정 설정 가져오기</span><span class="sxs-lookup"><span data-stu-id="d393c-151">Get autoscale settings for a resource group</span></span>
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a><span data-ttu-id="d393c-152">리소스 그룹의 이름으로 자동 크기 조정 설정 가져오기</span><span class="sxs-lookup"><span data-stu-id="d393c-152">Get autoscale settings by name in a resource group</span></span>
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a><span data-ttu-id="d393c-153">자동 크기 조정 설정 지정</span><span class="sxs-lookup"><span data-stu-id="d393c-153">Set auotoscale settings</span></span>
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```
