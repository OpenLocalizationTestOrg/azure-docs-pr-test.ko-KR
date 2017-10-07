---
title: "Azure PowerShell을 사용한 Azure Redis Cache aaaManage | Microsoft Docs"
description: "자세한 내용은 방법 tooperform Azure PowerShell을 사용 하 여 Azure Redis 캐시에 대 한 관리 작업입니다."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1136efe5-1e33-4d91-bb49-c8e2a6dca475
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: sdanie
ms.openlocfilehash: 1d526ce65c4bc05345cd6c3ff370211ed562cab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-redis-cache-with-azure-powershell"></a>Azure PowerShell을 사용하여 Azure Redis Cache 관리
> [!div class="op_single_selector"]
> * [PowerShell](cache-howto-manage-redis-cache-powershell.md)
> * [Azure CLI](cache-manage-cli.md)
> 
> 

이 항목에서는 방식과 tooperform 공통 작업 만들기와 같은, 업데이트 및 사용자의 Azure Redis Cache 인스턴스가 어떻게 확장 tooregenerate 선택 키와 방법을 캐시에 대 한 tooview 정보입니다. Azure Redis Cache PowerShell cmdlet의 전체 목록은 [Azure Redis Cache cmdlet](https://msdn.microsoft.com/library/azure/mt634513.aspx)을 참조하세요.

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

Hello 클래식 배포 모델에 대 한 자세한 내용은 참조 [Azure 리소스 관리자 및 클래식 배포: 배포 모델을 이해 하 고 리소스 상태를 hello](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics)합니다.

## <a name="prerequisites"></a>필수 조건
Azure PowerShell을 이미 설치한 경우 Azure PowerShell 버전 1.0.0 이상이 있어야 합니다. Hello hello Azure PowerShell 명령 프롬프트에서이 명령을 사용 하 여 설치 된 Azure PowerShell 버전을 확인할 수 있습니다.

    Get-Module azure | format-table version


첫째, tooAzure이이 명령 사용 하 여 로그인 해야 합니다.

    Login-AzureRmAccount

Microsoft Azure 로그인 hello 대화 상자에서 Azure 계정 및 암호의 hello 전자 메일 주소를 지정 합니다.

다음으로, 여러 Azure 구독이 있는 경우 해야 tooset Azure 구독. 현재 구독 목록이 toosee이이 명령을 실행 합니다.

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

toospecify hello 구독을 hello 다음 명령을 실행 합니다. 다음 예제는 hello, hello 구독 이름은 `ContosoSubscription`합니다.

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

Azure 리소스 관리자와 Windows PowerShell을 사용할 수 있습니다, 전에 hello 다음을 해야 합니다.

* Windows PowerShell, 버전 3.0 또는 4.0. toofind hello 버전의 Windows PowerShell, 유형:`$PSVersionTable` 의 hello 값을 확인 하 고 `PSVersion` 3.0 또는 4.0가 있습니다. 호환 되는 버전 tooinstall 참조 [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) 또는 [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855)합니다.

tooget은 hello Get-help cmdlet 사용 하 여가이 자습서에 나와 있는 모든 cmdlet에 대 한 도움말을 자세히 설명 합니다.

    Get-Help <cmdlet-name> -Detailed

예를 들어 hello에 대 한 도움말을 tooget `New-AzureRmRedisCache` cmdlet, 유형:

    Get-Help New-AzureRmRedisCache -Detailed

### <a name="how-tooconnect-tooother-clouds"></a>어떻게 tooconnect tooother 클라우드
환경에는 기본 hello Azure로 `AzureCloud`이며 나타냅니다 hello 글로벌 Azure 클라우드 인스턴스. tooconnect tooa 다른 인스턴스를 사용 하 여 hello `Add-AzureRmAccount` hello로 명령을 `-Environment` 또는-`EnvironmentName` hello 원하는 환경 또는 환경 이름이 명령줄 스위치입니다.

toosee hello 목록이 hello를 실행 하는 사용 가능한 환경 `Get-AzureRmEnvironment` cmdlet.

### <a name="tooconnect-toohello-azure-government-cloud"></a>tooconnect toohello Azure Government 클라우드
tooconnect toohello Azure Government 클라우드 hello 다음 명령 중 하나를 사용 합니다.

    Add-AzureRMAccount -EnvironmentName AzureUSGovernment

또는

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureUSGovernment)

hello Azure Government 클라우드에서에서 캐시 toocreate hello 다음 위치 중 하나를 사용 합니다.

* USGov 버지니아
* 미국 정부 아이오와

Hello Azure Government 클라우드에 대 한 자세한 내용은 참조 하십시오. [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) 및 [Microsoft Azure Government 개발자 가이드](../azure-government-developer-guide.md)합니다.

### <a name="tooconnect-toohello-azure-china-cloud"></a>tooconnect toohello Azure 중국 클라우드
tooconnect toohello Azure 중국 클라우드 hello 다음 명령 중 하나를 사용 합니다.

    Add-AzureRMAccount -EnvironmentName AzureChinaCloud

또는

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureChinaCloud)

hello Azure 중국 클라우드에서에서 캐시 toocreate hello 다음 위치 중 하나를 사용 합니다.

* 중국 동부
* 중국 북부

Hello Azure 중국 클라우드에 대 한 자세한 내용은 참조 하십시오. [중국의 21Vianet에서에서 운영 되는 Azure에 대 한 AzureChinaCloud](http://www.windowsazure.cn/)합니다.

### <a name="tooconnect-toomicrosoft-azure-germany"></a>tooconnect tooMicrosoft Azure 독일
tooconnect tooMicrosoft Azure 독일 hello 다음 명령 중 하나를 사용 합니다.

    Add-AzureRMAccount -EnvironmentName AzureGermanCloud


또는

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureGermanCloud)

Microsoft Azure 독일의 캐시 toocreate hello 다음 위치 중 하나를 사용 합니다.

* 독일 중부
* 독일 북동부

Microsoft Azure Germany에 대한 자세한 내용은 [Microsoft Azure Germany](https://azure.microsoft.com/overview/clouds/germany/)를 참조하세요.

### <a name="properties-used-for-azure-redis-cache-powershell"></a>Azure Redis Cache PowerShell에 사용되는 속성
다음 표에 hello 속성과 자주 사용 되는 매개 변수를 만들고 Azure PowerShell을 사용 하 여 Azure Redis 캐시 인스턴스를 관리 하는 경우에 대 한 설명을 포함 합니다.

| 매개 변수 | 설명 | 기본값 |
| --- | --- | --- |
| 이름 |Hello 캐시의 이름 | |
| 위치 |Hello 캐시의 위치 | |
| ResourceGroupName |어떤 toocreate hello 캐시에 리소스 그룹 이름 | |
| 크기 |hello hello 캐시 크기입니다. 유효한 값: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB |1GB |
| ShardCount |클러스터링을 사용 프리미엄 캐시를 만들 때 분할 영역 toocreate hello 수입니다. 유효한 값: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 | |
| SKU |Hello hello 캐시의 SKU를 지정합니다. 유효한 값: 기본, 표준, 프리미엄 |표준 |
| RedisConfiguration |Redis 구성 설정을 지정합니다. 각 설정에 대 한 자세한 내용은 hello 다음을 참조 하십시오. [RedisConfiguration 속성](#redisconfiguration-properties) 테이블입니다. | |
| EnableNonSslPort |Hello 비 SSL 포트를 사용 하는지 여부를 나타냅니다. |False |
| MaxMemoryPolicy |이 매개 변수는 더 이상 사용되지 않으며 대신 RedisConfiguration을 사용합니다. | |
| StaticIP |VNET에서 캐시를 호스팅하는 경우 hello 캐시에 대 한 hello 서브넷에 고유한 IP 주소를 지정 합니다. 을 지정 하지 않으면 하나는 선택 됩니다 hello 서브넷에서. | |
| 서브넷 |VNET에서 캐시를 호스팅하는 경우 어떤 toodeploy hello 캐시 hello hello 서브넷 이름을 지정 합니다. | |
| VirtualNetwork |hello 리소스 ID를 지정 하는 VNET에서 캐시를 호스팅하는 경우에 어떤 toodeploy hello 캐시에는 VNET hello 합니다. | |
| KeyType |액세스 키를 지정 합니다. 액세스 키를 갱신할 때 tooregenerate 합니다. 유효한 값: 주, 보조 | |

### <a name="redisconfiguration-properties"></a>RedisConfiguration 속성
| 속성 | 설명 | 가격 책정 계층 |
| --- | --- | --- |
| rdb-backup-enabled |[Redis 데이터 지속성](cache-how-to-premium-persistence.md) 사용 여부 |프리미엄 전용 |
| rdb-storage-connection-string |연결 문자열 toohello 저장소 계정에 대 한 hello [Redis 데이터 지 속성](cache-how-to-premium-persistence.md) |프리미엄 전용 |
| rdb-backup-frequency |백업 빈도 대 한 hello [Redis 데이터 지 속성](cache-how-to-premium-persistence.md) |프리미엄 전용 |
| maxmemory-reserved |Hello 구성 [예약 되는 메모리](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) 캐시 되지 않은 프로세스에 대 한 |표준 및 프리미엄 |
| maxmemory-policy |Hello 구성 [의 제거 정책](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) hello 캐시에 대 한 |모든 가격 책정 계층 |
| notify-keyspace-events |[Keyspace 알림](cache-configure.md#keyspace-notifications-advanced-settings) |표준 및 프리미엄 |
| hash-max-ziplist-entries |작은 집계 데이터 형식에 대한 [메모리 최적화](http://redis.io/topics/memory-optimization) 구성 |표준 및 프리미엄 |
| hash-max-ziplist-value |작은 집계 데이터 형식에 대한 [메모리 최적화](http://redis.io/topics/memory-optimization) 구성 |표준 및 프리미엄 |
| set-max-intset-entries |작은 집계 데이터 형식에 대한 [메모리 최적화](http://redis.io/topics/memory-optimization) 구성 |표준 및 프리미엄 |
| zset-max-ziplist-entries |작은 집계 데이터 형식에 대한 [메모리 최적화](http://redis.io/topics/memory-optimization) 구성 |표준 및 프리미엄 |
| zset-max-ziplist-value |작은 집계 데이터 형식에 대한 [메모리 최적화](http://redis.io/topics/memory-optimization) 구성 |표준 및 프리미엄 |
| 데이터베이스 |Hello 데이터베이스 수를 구성합니다. 이 속성은 캐시 만들기에서만 구성할 수 있습니다. |표준 및 프리미엄 |

## <a name="toocreate-a-redis-cache"></a>toocreate Redis 캐시
Hello를 사용 하 여 새 Azure Redis Cache 인스턴스가 만들어지지 [새로 AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.

> [!IMPORTANT]
> hello 처음 hello Azure 포털을 사용 하 여 구독에서 Redis cache를 만들 때 hello 포털 등록 hello `Microsoft.Cache` 해당 구독에 대 한 네임 스페이스입니다. 사용 하려는 경우 toocreate hello PowerShell을 사용 하 여 구독에서 캐시를 먼저 Redis, 다음 명령을; hello를 사용 하 여 해당 네임 스페이스를 먼저 등록 해야 합니다. 그렇지 않으면 cmdlet과 같은 `New-AzureRmRedisCache` 및 `Get-AzureRmRedisCache` 실패 합니다.
> 
> `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Cache"`
> 
> 

사용 가능한 매개 변수 목록과 해당 설명을 보려면에 대 한 toosee `New-AzureRmRedisCache`실행 hello 다음 명령을 합니다.

    PS C:\> Get-Help New-AzureRmRedisCache -detailed

    NAME
        New-AzureRmRedisCache

    SYNOPSIS
        Creates a new redis cache.


    SYNTAX
        New-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Location <String> [-RedisVersion <String>]
        [-Size <String>] [-Sku <String>] [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort
        <Boolean>] [-ShardCount <Integer>] [-VirtualNetwork <String>] [-Subnet <String>] [-StaticIP <String>]
        [<CommonParameters>]


    DESCRIPTION
        hello New-AzureRmRedisCache cmdlet creates a new redis cache.


    PARAMETERS
        -Name <String>
            Name of hello redis cache toocreate.

        -ResourceGroupName <String>
            Name of resource group in which toocreate hello redis cache.

        -Location <String>
            Location in which toocreate hello redis cache.

        -RedisVersion <String>
            RedisVersion is deprecated and will be removed in future release.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value, databases.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. If no value is provided, hello default value is false and the
            non-SSL port will be disabled. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        -VirtualNetwork <String>
            hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{
            subid}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicNetwork/VirtualNetworks/{vnetName}

        -Subnet <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        -StaticIP <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

toocreate hello 다음 명령을 실행 합니다. 기본 매개 변수가 있는 캐시 합니다.

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US"

`ResourceGroupName``Name`, 및 `Location` 필수 매개 변수가 있지만 hello 나머지는 선택 사항이 며 기본값이 지정 합니다. Hello 지정 된 이름, 위치 및 크기와 사용 하지 않도록 설정 하는 hello 비 SSL 포트에에서 1GB 있는 리소스 그룹으로 표준 SKU Azure Redis 캐시 인스턴스를 만듭니다 hello 이전 명령을 실행 합니다.

P1 (6GB-60GB), P2 (13 GB-130 기가바이트)의 크기를 지정 하는 프리미엄 캐시 toocreate P3 (26GB-260 기가바이트) 또는 P4 (53GB 530 10GB). hello를 사용 하 여 분할 영역 수를 지정 하는 클러스터링, tooenable `ShardCount` 매개 변수입니다. hello 다음 만드는 예제 P1 프리미엄 캐시 3 분할 된 데이터베이스입니다. P1 프리미엄 캐시의 크기를 6GB는 하며 세 가지 분할 영역 hello 전체 크기를 지정 했기 때문 18 GB (3 x 6 GB)

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P1 -ShardCount 3

hello에 대 한 toospecify 값 `RedisConfiguration` 매개 변수를 내부 hello 값 묶습니다 `{}` 으로 키/값 쌍 같은 `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`합니다. hello 다음 예제에서는 캐시를 만든 표준 1GB와 `allkeys-random` 구성 된 최대 메모리 정책 및 키 스페이스 알림 `KEA`합니다. 자세한 내용은 [Keyspace 알림(고급 설정)](cache-configure.md#keyspace-notifications-advanced-settings) 및 [메모리 정책](cache-configure.md#memory-policies)을 참조하세요.

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}

<a name="databases"></a>

## <a name="tooconfigure-hello-databases-setting-during-cache-creation"></a>캐시 만들기 중에 설정 tooconfigure hello 데이터베이스
hello `databases` 캐시 만들기 중에 설정을 구성할 수 있습니다. hello 다음 예제에서는 프리미엄 P3 hello를 사용 하 여 48 데이터베이스와 함께 (26GB) 캐시 [새로 AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P3 -RedisConfiguration @{"databases" = "48"}

Hello에 대 한 자세한 내용은 `databases` 속성 참조 [기본 Azure Redis Cache 서버 구성](cache-configure.md#default-redis-server-configuration)합니다. Hello를 사용 하 여 캐시를 만드는 방법에 대 한 자세한 내용은 [새로 AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet hello 이전 참조 [toocreate Redis Cache](#to-create-a-redis-cache) 섹션.

## <a name="tooupdate-a-redis-cache"></a>tooupdate Redis 캐시
Azure Redis 캐시 인스턴스가 hello를 사용 하 여 업데이트 됩니다 [집합 AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet.

사용 가능한 매개 변수 목록과 해당 설명을 보려면에 대 한 toosee `Set-AzureRmRedisCache`실행 hello 다음 명령을 합니다.

    PS C:\> Get-Help Set-AzureRmRedisCache -detailed

    NAME
        Set-AzureRmRedisCache

    SYNOPSIS
        Set redis cache updatable parameters.

    SYNTAX
        Set-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Size <String>] [-Sku <String>]
        [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort <Boolean>] [-ShardCount
        <Integer>] [<CommonParameters>]

    DESCRIPTION
        hello Set-AzureRmRedisCache cmdlet sets redis cache parameters.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooupdate.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. hello default value is null and no change will be made toothe
            currently configured value. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

hello `Set-AzureRmRedisCache` cmdlet과 같은 사용된 tooupdate 속성 수 `Size`, `Sku`, `EnableNonSslPort`, 및 hello `RedisConfiguration` 값입니다. 

hello 업데이트 hello에 대 한 hello Redis 캐시 maxmemory 정책 다음 명령은 이름이 myCache입니다.

    Set-AzureRmRedisCache -ResourceGroupName "myGroup" -Name "myCache" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random"}

<a name="scale"></a>

## <a name="tooscale-a-redis-cache"></a>tooscale Redis 캐시
`Set-AzureRmRedisCache`사용 되는 tooscale 때 hello Azure Redis 캐시 인스턴스 수 `Size`, `Sku`, 또는 `ShardCount` 속성이 수정 됩니다. 

> [!NOTE]
> PowerShell을 사용 하 여 캐시 크기 조정 주체 toohello 동일한 제한을 이며 캐시에서 크기 조정 지침 hello Azure 포털. Tooa 다른 제한 사항에 따라 hello로 가격 책정 계층을 확장할 수 있습니다.
> 
> * 더 높은 가격 책정 계층 tooa 더 낮은 가격 책정 계층에서에서 확장할 수는 없습니다.
> * 업그레이드할 수 없는 **프리미엄** tooa 아래로 캐시 **표준** 또는 **기본** 캐시 합니다.
> * 업그레이드할 수 없는 **표준** tooa 아래로 캐시 **기본** 캐시 합니다.
> * 확장할 수는 **기본** tooa 캐시 **표준** 캐시 있지만 hello hello 크기를 변경할 수 없습니다 동시 합니다. 크기를 다르게 해야 할 경우에 크기 조정 작업의 후속 toohello 원하는 크기를 수행할 수 있습니다.
> * 업그레이드할 수 없는 **기본** 캐시 직접 tooa **프리미엄** 캐시 합니다. 확장 해야 **기본** 너무**표준** 한 크기 조정 작업에서 **표준** 너무**프리미엄** 후속 배율 작업입니다.
> * toohello 아래로 더 큰 크기를 확장할 수 없으며 **C0 (250MB)** 크기입니다.
> 
> 자세한 내용은 참조 [어떻게 tooScale Azure Redis 캐시](cache-how-to-scale.md)합니다.
> 
> 

hello 다음 예제에서는 어떻게 tooscale 캐시 라는 `myCache` tooa 2.5 g B 캐시 합니다. 이 명령은 기본 또는 표준 캐시 둘 다에 적용할 수 있습니다.

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

이 명령이 실행 된 후에 hello 캐시의 hello 상태가 반환 됩니다 (유사한 toocalling `Get-AzureRmRedisCache`). 해당 hello 참고 `ProvisioningState` 은 `Scaling`합니다.

    PS C:\> Set-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup -Size 2.5GB


    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/mygroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Scaling
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 150], [notify-keyspace-events, KEA],
                         [maxmemory-delta, 150]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : mygroup
    PrimaryKey         : ....
    SecondaryKey       : ....
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

Hello 크기 조정 작업이 완료 되 면 hello `ProvisioningState` 쪽 변경`Succeeded`합니다. Toomake 후속 있는 크기 조정 작업에서 기본 tooStandard 변경 등 다음 hello 크기를 변경 해야 할 경우 hello 이전 작업이 완료 되거나 오류 유사한 toohello 다음 수신 될 때까지 기다려야 합니다.

    Set-AzureRmRedisCache : Conflict: hello resource '...' is not in a stable state, and is currently unable tooaccept hello update request.

## <a name="tooget-information-about-a-redis-cache"></a>Redis 캐시에 대 한 tooget 정보
Hello를 사용 하 여 캐시에 대 한 정보를 검색할 수 [Get AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet.

사용 가능한 매개 변수 목록과 해당 설명을 보려면에 대 한 toosee `Get-AzureRmRedisCache`실행 hello 다음 명령을 합니다.

    PS C:\> Get-Help Get-AzureRmRedisCache -detailed

    NAME
        Get-AzureRmRedisCache

    SYNOPSIS
        Gets details about a single cache or all caches in hello specified resource group or all caches in hello current
        subscription.

    SYNTAX
        Get-AzureRmRedisCache [-Name <String>] [-ResourceGroupName <String>] [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCache cmdlet gets hello details about a cache or caches depending on input parameters. If both
        ResourceGroupName and Name parameters are provided then Get-AzureRmRedisCache will return details about the
        specific cache name provided.

        If only ResourceGroupName is provided than it will return details about all caches in hello specified resource group.

        If no parameters are given than it will return details about all caches hello current subscription.

    PARAMETERS
        -Name <String>
            hello name of hello cache. When this parameter is provided along with ResourceGroupName, Get-AzureRmRedisCache
            returns hello details for hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache or caches. If ResourceGroupName is provided with Name
            then Get-AzureRmRedisCache returns hello details of hello cache specified by Name. If only hello ResourceGroup
            parameter is provided, then details for all caches in hello resource group are returned.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

hello 현재 구독에서 모든 캐시에 대 한 정보 tooreturn 실행 `Get-AzureRmRedisCache` 매개 변수 없이 합니다.

    Get-AzureRmRedisCache

특정 리소스 그룹의 모든 캐시에 대 한 정보 tooreturn 실행 `Get-AzureRmRedisCache` hello로 `ResourceGroupName` 매개 변수입니다.

    Get-AzureRmRedisCache -ResourceGroupName myGroup

특정 캐시에 대 한 정보 tooreturn 실행 `Get-AzureRmRedisCache` hello로 `Name` hello 캐시 및 hello의 hello 이름을 포함 하는 매개 변수 `ResourceGroupName` 해당 캐시를 포함 하는 hello 리소스 그룹과 매개 변수입니다.

    PS C:\> Get-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/myGroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Succeeded
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 62], [notify-keyspace-events, KEA],
                         [maxclients, 1000]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : myGroup
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

## <a name="tooretrieve-hello-access-keys-for-a-redis-cache"></a>Redis cache에 대해 tooretrieve hello 선택 키
캐시에 대 한 hello 선택 키 tooretrieve hello를 사용할 수 있습니다 [Get AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet.

사용 가능한 매개 변수 목록과 해당 설명을 보려면에 대 한 toosee `Get-AzureRmRedisCacheKey`실행 hello 다음 명령을 합니다.

    PS C:\> Get-Help Get-AzureRmRedisCacheKey -detailed

    NAME
        Get-AzureRmRedisCacheKey

    SYNOPSIS
        Gets hello accesskeys for hello specified redis cache.


    SYNTAX
        Get-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCacheKey cmdlet gets hello access keys for hello specified cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

캐시에 호출 hello에 대 한 키 tooretrieve hello `Get-AzureRmRedisCacheKey` cmdlet 및 캐시의 hello 이름에는 통과 hello hello 캐시를 포함 하는 hello 리소스 그룹의 이름입니다.

    PS C:\> Get-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup

    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : ABhfB757JgjIgt785JgKH9865eifmekfnn649303JKL=

## <a name="tooregenerate-access-keys-for-your-redis-cache"></a>Redis 캐시에 대 한 tooregenerate 선택 키
캐시에 대 한 hello 선택 키 tooregenerate hello를 사용할 수 있습니다 [새로 AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet.

사용 가능한 매개 변수 목록과 해당 설명을 보려면에 대 한 toosee `New-AzureRmRedisCacheKey`실행 hello 다음 명령을 합니다.

    PS C:\> Get-Help New-AzureRmRedisCacheKey -detailed

    NAME
        New-AzureRmRedisCacheKey

    SYNOPSIS
        Regenerates hello access key of a redis cache.

    SYNTAX
        New-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> -KeyType <String> [-Force] [<CommonParameters>]

    DESCRIPTION
        hello New-AzureRmRedisCacheKey cmdlet regenerate hello access key of a redis cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -KeyType <String>
            Specifies whether tooregenerate hello primary or secondary access key. Possible values are Primary or Secondary.

        -Force
            When hello Force parameter is provided, hello specified access key is regenerated without any confirmation prompts.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

캐시에서 호출 hello tooregenerate hello 기본 또는 보조 키 `New-AzureRmRedisCacheKey` cmdlet 및 hello 전달 리소스 그룹 이름을 지정 하 고 지정 `Primary` 또는 `Secondary` hello에 대 한 `KeyType` 매개 변수입니다. 다음 예제는 hello에 캐시에 대 한 hello 보조 액세스 키 다시 생성 됩니다.

    PS C:\> New-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup -KeyType Secondary

    Confirm
    Are you sure you want tooregenerate Secondary key for redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : c53hj3kh4jhHjPJk8l0jji785JgKH9865eifmekfnn6=

## <a name="toodelete-a-redis-cache"></a>toodelete Redis 캐시
Redis cache toodelete hello를 사용 하 여 [제거 AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet.

사용 가능한 매개 변수 목록과 해당 설명을 보려면에 대 한 toosee `Remove-AzureRmRedisCache`실행 hello 다음 명령을 합니다.

    PS C:\> Get-Help Remove-AzureRmRedisCache -detailed

    NAME
        Remove-AzureRmRedisCache

    SYNOPSIS
        Remove redis cache if exists.

    SYNTAX
        Remove-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Force] [-PassThru] [<CommonParameters>

    DESCRIPTION
        hello Remove-AzureRmRedisCache cmdlet removes a redis cache if it exists.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooremove.

        -ResourceGroupName <String>
            Name of hello resource group of hello cache tooremove.

        -Force
            When hello Force parameter is provided, hello cache is removed without any confirmation prompts.

        -PassThru
            By default Remove-AzureRmRedisCache removes hello cache and does not return any value. If hello PassThru par
            is provided then Remove-AzureRmRedisCache returns a boolean value indicating hello success of hello operatio

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

다음 예제는 hello에서 명명 된 캐시 hello `myCache` 제거 됩니다.

    PS C:\> Remove-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Confirm
    Are you sure you want tooremove redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


## <a name="tooimport-a-redis-cache"></a>tooimport Redis 캐시
Hello를 사용 하 여 Azure Redis Cache 인스턴스로 데이터를 가져올 수 있습니다 `Import-AzureRmRedisCache` cmdlet.

> [!IMPORTANT]
> 가져오기/내보내기는 [프리미엄 계층](cache-premium-tier-intro.md) 캐시에만 제공됩니다. 가져오기/내보내기에 대한 자세한 내용은 [Azure Redis Cache에서 데이터 가져오기 및 내보내기](cache-how-to-import-export-data.md)를 참조하세요.
> 
> 

사용 가능한 매개 변수 목록과 해당 설명을 보려면에 대 한 toosee `Import-AzureRmRedisCache`실행 hello 다음 명령을 합니다.

    PS C:\> Get-Help Import-AzureRmRedisCache -detailed

    NAME
        Import-AzureRmRedisCache

    SYNOPSIS
        Import data from blobs tooAzure Redis Cache.


    SYNTAX
        Import-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Files <String[]> [-Format <String>] [-Force]
        [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Import-AzureRmRedisCache cmdlet imports data from hello specified blobs into Azure Redis Cache.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Files <String[]>
            SAS urls of blobs whose content should be imported into hello cache.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -Force
            When hello Force parameter is provided, import will be performed without any confirmation prompts.

        -PassThru
            By default Import-AzureRmRedisCache imports data in cache and does not return any value. If hello PassThru
            parameter is provided then Import-AzureRmRedisCache returns a boolean value indicating hello success of the
            operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


hello 다음 명령에서에서 데이터를 가져옵니다 Azure Redis 캐시로 hello SAS uri로 지정 된 hello blob입니다.

    PS C:\>Import-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Files @("https://mystorageaccount.blob.core.windows.net/mycontainername/blobname?sv=2015-04-05&sr=b&sig=caIwutG2uDa0NZ8mjdNJdgOY8%2F8mhwRuGNdICU%2B0pI4%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwd") -Force

## <a name="tooexport-a-redis-cache"></a>tooexport Redis 캐시
Azure Redis Cache 인스턴스에서 hello를 사용 하 여 데이터를 내보낼 수 `Export-AzureRmRedisCache` cmdlet.

> [!IMPORTANT]
> 가져오기/내보내기는 [프리미엄 계층](cache-premium-tier-intro.md) 캐시에만 제공됩니다. 가져오기/내보내기에 대한 자세한 내용은 [Azure Redis Cache에서 데이터 가져오기 및 내보내기](cache-how-to-import-export-data.md)를 참조하세요.
> 
> 

사용 가능한 매개 변수 목록과 해당 설명을 보려면에 대 한 toosee `Export-AzureRmRedisCache`실행 hello 다음 명령을 합니다.

    PS C:\> Get-Help Export-AzureRmRedisCache -detailed

    NAME
        Export-AzureRmRedisCache

    SYNOPSIS
        Exports data from Azure Redis Cache tooa specified container.


    SYNTAX
        Export-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Prefix <String> -Container <String> [-Format
        <String>] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Export-AzureRmRedisCache cmdlet exports data from Azure Redis Cache tooa specified container.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Prefix <String>
            Prefix toouse for blob names.

        -Container <String>
            SAS url of container where data should be exported.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -PassThru
            By default Export-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Export-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


hello 다음 명령은 데이터에서에서 내보냅니다 hello SAS uri로 지정 된 hello 컨테이너로 Azure Redis Cache 인스턴스.

        PS C:\>Export-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Prefix "blobprefix"
        -Container "https://mystorageaccount.blob.core.windows.net/mycontainer?sv=2015-04-05&sr=c&sig=HezZtBZ3DURmEGDduauE7
        pvETY4kqlPI8JCNa8ATmaw%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwdl"

## <a name="tooreboot-a-redis-cache"></a>tooreboot Redis 캐시
Azure Redis 캐시 인스턴스의 hello를 사용 하 여 다시 부팅할 수 `Reset-AzureRmRedisCache` cmdlet.

> [!IMPORTANT]
> 재부팅은 [프리미엄 계층](cache-premium-tier-intro.md) 캐시에만 사용할 수 있습니다. 캐시를 재부팅하는 방법에 대한 자세한 내용은 [캐시 관리 - 재부팅](cache-administration.md#reboot)을 참조하세요.
> 
> 

사용 가능한 매개 변수 목록과 해당 설명을 보려면에 대 한 toosee `Reset-AzureRmRedisCache`실행 hello 다음 명령을 합니다.

    PS C:\> Get-Help Reset-AzureRmRedisCache -detailed

    NAME
        Reset-AzureRmRedisCache

    SYNOPSIS
        Reboot specified node(s) of an Azure Redis Cache instance.


    SYNTAX
        Reset-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -RebootType <String> [-ShardId <Integer>]
        [-Force] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Reset-AzureRmRedisCache cmdlet reboots hello specified node(s) of an Azure Redis Cache instance.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -RebootType <String>
            Which node tooreboot. Possible values are "PrimaryNode", "SecondaryNode", "AllNodes".

        -ShardId <Integer>
            Which shard tooreboot when rebooting a premium cache with clustering enabled.

        -Force
            When hello Force parameter is provided, reset will be performed without any confirmation prompts.

        -PassThru
            By default Reset-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Reset-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


hello 다음 명령을 다시 부팅 지정 hello의 두 노드 모두 캐시 합니다.

        PS C:\>Reset-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -RebootType "AllNodes"
        -Force


## <a name="next-steps"></a>다음 단계
Azure를 통해 Windows PowerShell 사용에 대 한 더 toolearn hello 다음 리소스를 참조 하십시오.

* [MSDN에 있는 Azure Redis Cache cmdlet 설명서](https://msdn.microsoft.com/library/azure/mt634513.aspx)
* [Azure 리소스 관리자 Cmdlet](http://go.microsoft.com/fwlink/?LinkID=394765): hello Azure 리소스 관리자 모듈의 toouse hello cmdlet에 알아봅니다.
* [Toomanage Azure 리소스 그룹 리소스를 사용 하 여](../azure-resource-manager/resource-group-template-deploy-portal.md): 자세한 방법을 toocreate hello Azure 포털에서에서 리소스 그룹 및 관리 합니다.
* [Azure 블로그](http://blogs.msdn.com/windowsazure): Azure의 새로운 기능에 대해 알아봅니다.
* [Windows PowerShell 블로그](http://blogs.msdn.com/powershell): Windows PowerShell의 새로운 기능에 대해 알아봅니다.
* ["Hey, Scripting Guy!" 블로그](http://blogs.technet.com/b/heyscriptingguy/): hello Windows PowerShell 커뮤니티에서에서 실제 팁과 요령을 가져옵니다.

