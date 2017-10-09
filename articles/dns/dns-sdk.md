---
title: "aaaCreate DNS 영역 및 Azure DNS를 사용 하 여 레코드 집합 hello.NET SDK | Microsoft Docs"
description: "어떻게 toocreate DNS 영역과 레코드에에서 설정 Azure DNS hello.NET SDK를 사용 하 여 합니다."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: eed99b87-f4d4-4fbf-a926-263f7e30b884
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/19/2016
ms.author: jonatul
ms.openlocfilehash: e3bab98b13b787427219acb7ec55e53490512fe7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-zones-and-record-sets-using-hello-net-sdk"></a>DNS 영역 및 hello.NET SDK를 사용 하 여 레코드 집합 만들기

.NET DNS 관리 라이브러리와 함께 DNS SDK를 사용 하 여 toocreate, delete 또는 update DNS 영역을 레코드 집합 작업 및 레코드를 자동화할 수 있습니다. 전체 Visual Studio 프로젝트는 [여기](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)에서 사용할 수 있습니다.

## <a name="create-a-service-principal-account"></a>서비스 주체 계정 만들기

일반적으로 사용자 고유의 사용자 자격 증명 보다는 전용된 계정을 통해 tooAzure 리소스에 프로그래밍 방식으로 액세스 권한이 부여 됩니다. 이러한 전용 계정을 '서비스 주체' 계정이라고 합니다. toouse hello Azure DNS SDK 예제 프로젝트를 먼저 toocreate 서비스 주체 계정이 필요 하 고 hello 올바른 사용 권한을 할당 합니다.

1. 에 따라 [이러한 지침](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate 서비스 사용자 계정 (hello Azure DNS SDK 샘플 프로젝트에는 암호 기반 인증 가정 합니다.)
2. 리소스 그룹을 만듭니다([방법은 여기에서 확인](../azure-resource-manager/resource-group-template-deploy-portal.md)).
3. 사용 하 여 Azure RBAC toogrant hello 서비스 보안 주체 ' DNS 영역 참가자 ' 권한 toohello 리소스 그룹 ([같습니다 어떻게](../active-directory/role-based-access-control-configure.md).)
4. Hello Azure DNS SDK 샘플 프로젝트를 사용 하는 경우 hello 'program.cs' 파일을 다음과 같이 편집 합니다.

   * Hello hello tenantId, clientId (계정 ID 라고도 함), 암호 (서비스 사용자 계정 암호) 및 1 단계에서 사용 되는 구독 Id에 대 한 올바른 값을 삽입 합니다.
   * 2 단계에서 선택한 hello 리소스 그룹 이름을 입력 합니다.
   * 선택한 DNS 영역 이름을 입력합니다.

## <a name="nuget-packages-and-namespace-declarations"></a>NuGet 패키지 및 네임스페이스 선언

tooinstall hello 해야 toouse hello Azure DNS.NET SDK **Azure DNS 관리 라이브러리** NuGet 패키지 및 기타 필요한 Azure 패키지 합니다.

1. **Visual Studio**에서 프로젝트 또는 새 프로젝트를 엽니다.
2. 너무 이동**도구**  **>**  **NuGet 패키지 관리자**  **>**  **에 대 한 NuGet 패키지 관리 솔루션 중...** .
3. 클릭 **찾아보기**, hello를 사용 하도록 설정 **Include 시험판** 확인란을 선택 및 형식 **Microsoft.Azure.Management.Dns** hello 검색 상자에 있습니다.
4. Hello 패키지를 선택 하 고 클릭 **설치** tooadd 것 tooyour Visual Studio 프로젝트입니다.
5. 패키지를 다음 tooalso 설치 hello 위에 hello 프로세스를 반복: **Microsoft.Rest.ClientRuntime.Azure.Authentication** 및 **Microsoft.Azure.Management.ResourceManager**합니다.

## <a name="add-namespace-declarations"></a>네임스페이스 선언 추가

Hello 다음 네임 스페이스 선언을 추가 합니다.

```cs
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
```

## <a name="initialize-hello-dns-management-client"></a>Hello DNS 관리 클라이언트를 초기화 합니다.

hello *DnsManagementClient* hello 메서드 및 DNS 영역 및 레코드 집합을 관리 하는 데 필요한 속성을 포함 합니다.  hello 다음 코드 toohello 서비스 사용자 계정에 로그인 하 고 DnsManagementClient 개체를 만듭니다.

```cs
// Build hello service credentials and DNS management client
var serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var dnsClient = new DnsManagementClient(serviceCreds);
dnsClient.SubscriptionId = subscriptionId;
```

## <a name="create-or-update-a-dns-zone"></a>DNS 영역 만들기 또는 업데이트

DNS 영역 toocreate 먼저는 "영역" 개체가 만들어진 toocontain hello DNS 영역 매개 변수입니다. Hello 위치가 too'global를 설정 하 고 DNS 영역은 연결 된 tooa 특정 지역 없기 때문에 '. 이 예제는 [Azure 리소스 관리자 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) toohello 영역도 추가 됩니다.

tooactually 만들거나 Azure DNS hello 영역 매개 변수를 포함 하는 hello 영역 개체에에서 hello 영역 업데이트 toohello 전달 *DnsManagementClient.Zones.CreateOrUpdateAsyc* 메서드.

> [!NOTE]
> DnsManagementClient 지원 작업의 세 가지 모드: 동기 ('CreateOrUpdate'), 비동기 ('CreateOrUpdateAsync'), 또는 액세스 toohello HTTP 응답 ('CreateOrUpdateWithHttpMessagesAsync')와 비동기입니다.  응용 프로그램 요구 사항에 따라 이러한 모드 중 하나를 선택할 수 있습니다.

Azure DNS는 [Etag](dns-getstarted-create-dnszone.md)라는 낙관적 동시성을 지원합니다. 이 예제에서는 지정 "*" hello ' None-If-match ' 헤더 지시 Azure DNS toocreate DNS 영역이 아직 없는 경우에 대 한 합니다.  hello 호출이 hello 지정 된 이름의 영역 hello 리소스 그룹에 이미 있는 경우 실패 합니다.

```cs
// Create zone parameters
var dnsZoneParams = new Zone("global"); // All DNS zones must have location = "global"

// Create a Azure Resource Manager 'tag'.  This is optional.  You can add multiple tags
dnsZoneParams.Tags = new Dictionary<string, string>();
dnsZoneParams.Tags.Add("dept", "finance");

// Create hello actual zone.
// Note: Uses 'If-None-Match *' ETAG check, so will fail if hello zone exists already.
// Note: For non-async usage, call dnsClient.Zones.CreateOrUpdate(resourceGroupName, zoneName, dnsZoneParams, null, "*")
// Note: For getting hello http response, call dnsClient.Zones.CreateOrUpdateWithHttpMessagesAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*")
var dnsZone = await dnsClient.Zones.CreateOrUpdateAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*");
```

## <a name="create-dns-record-sets-and-records"></a>DNS 레코드 집합 및 레코드 만들기

DNS 레코드는 레코드 집합으로 관리됩니다. 레코드 집합은 동일한 이름을 지정 하 고 기록 hello로 레코드 집합이 영역 내에서 형식입니다.  hello 레코드 집합 이름은 상대 toohello 영역 이름을 정규화 된 DNS 이름을 하지 hello 합니다.

레코드 집합이 toocreate 또는 업데이트, "레코드 집합" 매개 변수 개체가 만들어지고 너무 전달*DnsManagementClient.RecordSets.CreateOrUpdateAsync*합니다. 작업의 세 가지 모드도 DNS 영역: 동기 ('CreateOrUpdate'), 비동기 ('CreateOrUpdateAsync'), 또는 액세스 toohello HTTP 응답 ('CreateOrUpdateWithHttpMessagesAsync')와 비동기입니다.

DNS 영역의 경우 레코드 집합에 대한 작업에는 낙관적 동시성에 대한 지원이 포함되어 있습니다.  이 예제에서는 ' If-match '도 아니고 ' None-If-match ' 지정 hello 레코드 집합은 항상 만들어집니다.  이 호출은 동일한 이름을 지정 하 고 기록 hello를 사용 하 여 설정 하는 모든 기존 레코드를 덮어씁니다이 DNS 영역에 있는 형식입니다.

```cs
// Create record set parameters
var recordSetParams = new RecordSet();
recordSetParams.TTL = 3600;

// Add records toohello record set parameter object.  In this case, we'll add a record of type 'A'
recordSetParams.ARecords = new List<ARecord>();
recordSetParams.ARecords.Add(new ARecord("1.2.3.4"));

// Add metadata toohello record set.  Similar tooAzure Resource Manager tags, this is optional and you can add multiple metadata name/value pairs
recordSetParams.Metadata = new Dictionary<string, string>();
recordSetParams.Metadata.Add("user", "Mary");

// Create hello actual record set in Azure DNS
// Note: no ETAG checks specified, will overwrite existing record set if one exists
var recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSetParams);
```

## <a name="get-zones-and-record-sets"></a>영역 및 레코드 집합 가져오기

hello *DnsManagementClient.Zones.Get* 및 *DnsManagementClient.RecordSets.Get* 각각 메서드 검색 개별 영역 및 레코드 집합입니다. 레코드 집합의 유형, 이름 및 hello 영역 및 리소스 그룹에 있는으로 식별 됩니다. 영역에 있는 해당 이름 및 hello 리소스 그룹에 의해 식별 됩니다.

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);
```

## <a name="update-an-existing-record-set"></a>기존 레코드 집합 업데이트

tooupdate 기존 DNS 레코드 집합을 먼저 hello 레코드 업데이트 내용을 설정 되 면 hello 변경 제출 다음 hello 레코드 집합을 검색 합니다.  이 예제에서는 hello 'Etag' hello에서 검색할 레코드 hello ' If-match ' 매개 변수 집합을 지정 합니다. hello 호출이 동시 작업이 그 동안 hello에 설정 하는 hello 레코드를 수정 하는 경우 실패 합니다.

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);

// Add a new record toohello local object.  Note that records in a record set must be unique/distinct
recordSet.ARecords.Add(new ARecord("5.6.7.8"));

// Update hello record set in Azure DNS
// Note: ETAG check specified, update will be rejected if hello record set has changed in hello meantime
recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSet, recordSet.Etag);
```

## <a name="list-zones-and-record-sets"></a>영역 및 레코드 집합 나열

toolist 영역을 사용 하 여 hello *DnsManagementClient.Zones.List...*  나열 하 고 해당된 리소스 그룹의 모든 영역 또는 지정 된 Azure 구독 (전체 리소스 그룹입니다.) toolist 레코드 집합의 모든 영역을 지원 하는 메서드를 사용 하 여 *DnsManagementClient.RecordSets.List...*  메서드 목록에 추가 하거나 지정 된 영역의 모든 레코드 집합 또는 특정 종류의 해당 레코드 집합만 지원 합니다.

영역을 나열할 때 나오는 레코드 집합은 페이지를 매길 수 있습니다.  hello 방법을 예제와 다음 결과의 hello 페이지를 통해 tooiterate 합니다. (인위적으로 작은 페이지 크기는 '2'가 사용 되는 tooforce 페이징, 실제로이 매개 변수 생략 해야 하며 hello 사용 되는 기본 페이지 크기)

```cs
// Note: in this demo, we'll use a very small page size (2 record sets) toodemonstrate paging
// In practice, tooimprove performance you would use a large page size or just use hello system default
int recordSets = 0;
var page = await dnsClient.RecordSets.ListAllInResourceGroupAsync(resourceGroupName, zoneName, "2");
recordSets += page.Count();

while (page.NextPageLink != null)
{
    page = await dnsClient.RecordSets.ListAllInResourceGroupNextAsync(page.NextPageLink);
    recordSets += page.Count();
}
```

## <a name="next-steps"></a>다음 단계

Hello 다운로드 [DNS AZURE.NET SDK 샘플 프로젝트](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), 어떻게 toouse hello 다른 DNS 레코드 종류에 대 한 예제를 포함 하 여 Azure DNS.NET SDK의에 추가 예가 포함 합니다.
