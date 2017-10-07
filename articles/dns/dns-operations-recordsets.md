---
title: "Azure PowerShell을 사용 하 여 Azure DNS에 aaaManage DNS 기록 | Microsoft Docs"
description: "Azure DNS에서 도메인을 호스트하는 경우 Azure DNS에서 DNS 레코드 집합 및 레코드를 관리합니다. 레코드 집합 및 레코드 작업에 대한 모든 PowerShell 명령입니다."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 7136a373-0682-471c-9c28-9e00d2add9c2
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: bfdf116e174d06db0514abdc0ec3f4fc4ee0a079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-azure-powershell"></a>Azure PowerShell을 사용하여 Azure DNS에서 DNS 레코드 및 레코드 집합 관리

> [!div class="op_single_selector"]
> * [Azure 포털](dns-operations-recordsets-portal.md)
> * [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

이 문서에서는 Azure PowerShell을 사용 하 여 DNS toomanage DNS 영역에 대 한 기록 하는 방법을 설명 합니다. 플랫폼 간 hello를 사용 하 여 DNS 레코드를 관리할 수도 있습니다 [Azure CLI](dns-operations-recordsets-cli.md) 또는 hello [Azure 포털](dns-operations-recordsets-portal.md)합니다.

이 문서의 예제 hello 이미 있다고 가정 [로그인 되어 Azure PowerShell을 설치 하 고 DNS 영역을 만든](dns-operations-dnszones.md)합니다.

## <a name="introduction"></a>소개

Azure DNS에 DNS 레코드를 만들기 전에 먼저 toounderstand Azure DNS DNS 레코드 집합으로 DNS 레코드를 구성 하는 방법입니다.

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

Azure DNS의 DNS 레코드에 대한 자세한 내용은 [DNS 영역 및 레코드](dns-zones-records.md)를 참조하세요.


## <a name="create-a-new-dns-record"></a>새 DNS 레코드 만들기

너무 필요한 새 레코드는 동일한 이름을 지정 하 고 기존 레코드도 입력 hello,[toohello 기존 레코드 집합을 추가](#add-a-record-to-an-existing-record-set)합니다. 새 레코드에 있는 기존 레코드는 서로 다른 이름 및 형식을 tooall 경우 toocreate 새 레코드 집합을 해야 합니다. 

### <a name="create-a-records-in-a-new-record-set"></a>새 레코드 집합에서 ‘A’ 레코드 만들기

Hello를 사용 하 여 레코드 집합을 만들면 `New-AzureRmDnsRecordSet` cmdlet. 레코드 집합을 만들 때 toospecify hello 레코드 집합 이름, hello 영역, toolive (TTL), hello 레코드 종류 및 hello 레코드 toobe 생성 hello 시간이 필요 합니다.

레코드 tooa 레코드 집합을 추가 하기 위한 hello 매개 변수는 hello 레코드 집합의 hello 유형에 따라 다릅니다. 예를 들어 'A' 형식의 레코드 집합을 사용할 경우 toospecify hello IP 주소가 필요한 hello 매개 변수를 사용 하 여 `-IPv4Address`합니다. 다른 레코드 형식에 다른 매개 변수를 사용합니다. 자세한 내용은 [추가 레코드 형식 예제](#additional-record-type-examples)를 참조하세요.

hello 다음 예제에서는 hello 상대 이름에 DNS 영역 'contoso.com' hello ' w w w' 인 레코드 집합 hello 정규화 hello 레코드 집합의 이름은 'www.contoso.com '입니다. hello 레코드 유형이 'A'이 고 hello TTL 3600 초입니다. 레코드 집합 hello '1.2.3.4' IP 주소로 단일 레코드를 포함합니다.

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

toocreate hello '루트' 영역에서 설정 된 레코드 (이 경우 '만든 contoso.com'), 사용 하 여 hello 레코드 집합 이름 ' @' (따옴표 제외):

```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

Toocreate 레코드가 여러 개 포함 된 레코드를 설정 해야 할 경우 먼저 지역 배열을 만든 다음 너무 hello 배열을 전달 하 hello 레코드를 추가 하 고`New-AzureRmDnsRecordSet` 다음과 같습니다.

```powershell
$aRecords = @()
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4"
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "2.3.4.5"
New-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName MyResourceGroup -Ttl 3600 -RecordType A -DnsRecords $aRecords
```

[메타 데이터를 설정 하는 레코드](dns-zones-records.md#tags-and-metadata) 키-값 쌍으로 각 레코드 집합을 사용 하 여 사용 되는 tooassociate 응용 프로그램별 데이터 일 수 있습니다. hello 다음 예제에서는 설정 방법을 보여 줍니다 toocreate 레코드 두 개 메타 데이터 항목이 있는 ' dept finance =' 및 ' 환경을 프로덕션 ='.

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") -Metadata @{ dept="finance"; environment="production" } 
```

또한 azure DNS 역할을 할 수는 자리 표시자 tooreserve DNS 이름 DNS 레코드를 만들기 전에 '빈' 레코드 집합을 지원 합니다. 빈 레코드 집합 hello Azure DNS 제어 평면에 표시 되어 있지만 hello Azure DNS 이름 서버에 나타나지 않습니다. 다음 예제는 hello 빈 레코드 집합을 만듭니다.

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords @()
```

## <a name="create-records-of-other-types"></a>다른 형식의 레코드 만들기

것 볼 자세히 toocreate 'A' 레코드 방법, 다음 예제에서는 다른 toocreate 레코드 Azure DNS에서 지 원하는 형식을 기록 하는 방법을 보여 hello.

각 경우에서는 단일 레코드를 포함 하는 레코드 toocreate을 설정 하는 방법을 보여 줍니다. hello 'A'의 레코드에 대 한 이전 예제 조정된 toocreate 레코드 집합의 메타 데이터와 여러 레코드를 포함 하는 다른 유형 또는 수 toocreate 빈 레코드 집합.

에서는 제공 하지 않으므로 예제 toocreate SOA 레코드 집합 Soa 만들어지므로 및 각 DNS 영역 있을 경우 삭제 하 고 만들거나 수 개별적으로 삭제 합니다. 그러나 [SOA를 수정할 수는 뒷부분에 나오는 예제와 같이 hello](#to-modify-an-SOA-record)합니다.

### <a name="create-an-aaaa-record-set-with-a-single-record"></a>단일 레코드가 포함된 AAAA 레코드 집합 만들기

```powershell
New-AzureRmDnsRecordSet -Name "test-aaaa" -RecordType AAAA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ipv6Address "2607:f8b0:4009:1803::1005") 
```

### <a name="create-a-cname-record-set-with-a-single-record"></a>단일 레코드가 포함된 CNAME 레코드 집합 만들기

> [!NOTE]
> hello DNS 표준 hello 영역 루트에서 CNAME 레코드를 허용 하지 않습니다 (`-Name '@'`), 또는 둘 이상의 레코드를 포함 하는 레코드 집합 허용 하지 않습니다.
> 
> 자세한 내용은 [CNAME 레코드](dns-zones-records.md#cname-records)를 참조하세요.


```powershell
New-AzureRmDnsRecordSet -Name "test-cname" -RecordType CNAME -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Cname "www.contoso.com") 
```

### <a name="create-an-mx-record-set-with-a-single-record"></a>단일 레코드가 포함된 MX 레코드 집합 만들기

이 예제에서 사용 하 여 hello 레코드 집합 이름은 ' @' hello 영역 루트에서 toocreate는 MX 레코드 (이 경우 '만든 contoso.com').


```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType MX -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Exchange "mail.contoso.com" -Preference 5) 
```

### <a name="create-an-ns-record-set-with-a-single-record"></a>단일 레코드가 포함된 NS 레코드 집합 만들기

```powershell
New-AzureRmDnsRecordSet -Name "test-ns" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Nsdname "ns1.contoso.com") 
```

### <a name="create-a-ptr-record-set-with-a-single-record"></a>단일 레코드가 포함된 PTR 레코드 집합 만들기

이 경우 ' 내-arpa-zone.com' 나타냅니다 hello ARPA 역방향 조회 영역 IP 범위를 나타내는입니다. 이 IP 범위에 속하는 tooan IP 주소를 해당 하는 각 PTR 레코드를이 영역 집합입니다. hello 레코드 이름은 '10' hello 마지막 8 진수 단위 값이이 레코드를 나타내는이 IP 범위에 속하는 hello IP 주소입니다.

```powershell
New-AzureRmDnsRecordSet -Name 10 -RecordType PTR -ZoneName "my-arpa-zone.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "myservice.contoso.com") 
```

### <a name="create-an-srv-record-set-with-a-single-record"></a>단일 레코드가 포함된 SRV 레코드 집합 만들기

만들 때는 [SRV 레코드 집합](dns-zones-records.md#srv-records), hello 지정  *\_서비스* 및  *\_프로토콜* hello 레코드 집합입니다. 없는 필요 tooinclude는 ' @' hello 레코드 집합 hello 영역 루트에서 설정 SRV 레코드를 만들 때.

```powershell
New-AzureRmDnsRecordSet -Name "_sip._tls" -RecordType SRV -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Priority 0 -Weight 5 -Port 8080 -Target "sip.contoso.com") 
```


### <a name="create-a-txt-record-set-with-a-single-record"></a>단일 레코드가 포함된 TXT 레코드 집합 만들기

hello 다음 예제에서는 한 TXT toocreate 기록 하는 방법을 TXT 레코드에서 지원 되는 hello 최대 문자열 길이 대 한 자세한 내용은 참조 [TXT 레코드](dns-zones-records.md#txt-records)합니다.

```powershell
New-AzureRmDnsRecordSet -Name "test-txt" -RecordType TXT -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Value "This is a TXT record") 
```


## <a name="get-a-record-set"></a>레코드 집합 가져오기

tooretrieve 기존 레코드 집합을 사용 하 여 `Get-AzureRmDnsRecordSet`합니다. 이 cmdlet에는 Azure DNS에서 설정 하는 hello 레코드를 나타내는 로컬 개체를 반환 합니다.

와 마찬가지로 `New-AzureRmDnsRecordSet`, 지정 된 hello 레코드 집합 이름 이어야 합니다는 *상대* 이름, 즉 hello 영역 이름을 제외 해야 합니다. Toospecify hello 레코드 종류와 hello 레코드 집합을 포함 하는 hello 영역 필요 합니다.

hello 다음 예제에서는 설정 방법을 보여 줍니다 tooretrieve 레코드입니다. 이 예제에서는 hello 영역 지정 hello를 사용 하 여 `-ZoneName` 및 `-ResourceGroupName` 매개 변수입니다.

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

Hello를 사용 하 여 전달 되는 영역 개체를 사용 하 여 hello 영역도 지정할 수는 또는 `-Zone` 매개 변수입니다.

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

## <a name="list-record-sets"></a>레코드 집합 나열

사용할 수도 있습니다 `Get-AzureRmDnsZone` hello를 생략 하 여 영역에 있는 toolist 레코드 집합 `-Name` 및/또는 `-RecordType` 매개 변수입니다.

hello 다음 예제에서는 반환 hello 영역의 모든 레코드 집합:

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

hello 다음 예제에서는 모든 지정 된 형식의 집합을 기록 하는 방법을 집합 이름 hello 레코드를 생략 하는 동안 hello 레코드 종류를 지정 하 여 검색할 수 있습니다.

```powershell
$recordsets = Get-AzureRmDnsRecordSet -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

지정 된 이름의 모든 레코드 집합 tooretrieve 레코드 유형에 필요한 tooretrieve 모든 레코드 집합 다음 필터 hello 결과:

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | where {$_.Name.Equals("www")}
```

위의 예제 모든 hello hello 영역 수 hello를 사용 하 여 지정 된 `-ZoneName` 및 `-ResourceGroupName`매개 변수 (표시 됨) 또는 영역 개체를 지정 하 여:

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$recordsets = Get-AzureRmDnsRecordSet -Zone $zone
```

## <a name="add-a-record-tooan-existing-record-set"></a>레코드 집합을 기존 레코드 tooan 추가

tooadd 레코드 tooan 기존 레코드를 설정 하려면이 세 단계를 수행 하는 hello를 수행 하십시오.

1. Hello 기존 레코드 집합 가져오기

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. Hello 새 레코드 toohello 로컬 레코드 집합을 추가 합니다. 이 작업은 오프라인 작업입니다.

    ```powershell
    Add-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. Hello 변경 백 toohello를 Azure DNS 서비스를 커밋하십시오. 

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $rs
    ```

사용 하 여 `Set-AzureRmDnsRecordSet` *대체* hello Azure DNS (및 포함 된 모든 레코드)의 지정 된 hello 레코드 집합으로 설정 하는 기존 레코드입니다. [Etag 검사](dns-zones-records.md#etags) 사용 tooensure 동시 변경 내용을 덮어쓰지 않습니다. Hello 옵션을 사용할 수 있습니다 `-Overwrite` toosuppress 이러한 검사를 전환 합니다.

이 작업 순서를 수도 있습니다 *파이프*를 매개 변수로 전달 하는 대신 hello 파이프를 사용 하 여 hello 레코드 집합 개체를 전달 하면 의미 합니다.

```powershell
Get-AzureRmDnsRecordSet -Name "www" –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Add-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

위의 예제에서는 hello 'A' 형식의 'A' 레코드 tooan 기존 레코드 tooadd 설정 하는 방법을 보여 줍니다. 작업의 유사한 시퀀스는 hello를 대체 하는 다른 형식에 사용 되는 tooadd 레코드 toorecord 집합 `-Ipv4Address` 의 매개 변수 `Add-AzureRmDnsRecordConfig` 다른 매개 변수 특정 tooeach 레코드 종류와 합니다. hello 각 레코드 종류에 대 한 매개 변수는 hello 동일 hello와 `New-AzureRmDnsRecordConfig` 에서 같이 cmdlet에 [추가 레코드 종류 예제](#additional-record-type-examples) 위에 있습니다.

'CNAME' 또는 'SOA' 형식의 레코드 집합은 둘 이상의 레코드를 포함할 수 없습니다. 이 제약 조건은 hello DNS 표준에서 발생합니다. Azure DNS의 제한 사항이 아닙니다.

## <a name="remove-a-record-from-an-existing-record-set"></a>기존 레코드 집합에서 레코드 제거

hello 프로세스 tooremove 레코드 집합에서 레코드는 기존 레코드 tooan 비슷한 toohello 프로세스 tooadd 집합을 기록 합니다.

1. Hello 기존 레코드 집합 가져오기

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. Hello 로컬 레코드 집합 개체에서 hello 레코드를 제거 합니다. 이 작업은 오프라인 작업입니다. hello 레코드가 제거 되는 모든 매개 변수는 기존 레코드와 정확 하 게 일치 해야 합니다.

    ```powershell
    Remove-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. Hello 변경 백 toohello를 Azure DNS 서비스를 커밋하십시오. 사용 하 여 hello 선택적 `-Overwrite` toosuppress 전환 [Etag 검사](dns-zones-records.md#etags) 동시 변경에 대 한 합니다.

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $Rs
    ```

시퀀스 tooremove hello 마지막 레코드를 레코드 집합 위에 hello를 사용 하 여 hello 레코드 집합을 삭제 하지 않습니다, 그리고 대신 빈 레코드 집합을 그대로 둡니다. 레코드 집합이 완전히 tooremove 참조 [레코드 집합 삭제](#delete-a-record-set)합니다.

Tooadding 레코드 tooa 레코드 집합이 마찬가지로 hello 일련의 작업 tooremove 레코드 집합 파이프 될 수 있습니다.

```powershell
Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Remove-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

다른 레코드 유형을 너무 hello 적절 한 형식 특정 매개 변수를 전달 하 여 사용할`Remove-AzureRmDnsRecordSet`합니다. hello 각 레코드 종류에 대 한 매개 변수는 hello 동일 hello와 `New-AzureRmDnsRecordConfig` 에서 같이 cmdlet에 [추가 레코드 종류 예제](#additional-record-type-examples) 위에 있습니다.


## <a name="modify-an-existing-record-set"></a>기존 레코드 집합 수정

기존 레코드 집합을 수정 하기 위한 hello 단계는 추가 하거나 레코드 집합에서 레코드를 제거할 때 수행 하는 비슷한 toohello 단계:

1. Hello 기존 레코드를 사용 하 여 설정 검색 `Get-AzureRmDnsRecordSet`합니다.
2. Hello 로컬 레코드 집합 개체를 수정 합니다.
    * 레코드 추가 또는 제거
    * 기존 레코드의 hello 매개 변수 변경
    * 메타 데이터 및 toolive TTL (time) 집합 hello 레코드를 변경 합니다.
3. Hello를 사용 하 여 변경 내용을 커밋하여 `Set-AzureRmDnsRecordSet` cmdlet. 이 *대체* hello Azure DNS에서 지정 된 hello 레코드 집합으로 설정 하는 기존 레코드입니다.

사용 하는 경우 `Set-AzureRmDnsRecordSet`, [Etag 검사](dns-zones-records.md#etags) 사용 tooensure 동시 변경 내용을 덮어쓰지 않습니다. Hello 옵션을 사용할 수 있습니다 `-Overwrite` toosuppress 이러한 검사를 전환 합니다.

### <a name="tooupdate-a-record-in-an-existing-record-set"></a>tooupdate 기존 레코드에서 레코드 집합

이 예제에서는 기존 '' 레코드의 hello IP 주소로 변경 합니다.

```powershell
$rs = Get-AzureRmDnsRecordSet -name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Ipv4Address = "9.8.7.6"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-an-soa-record"></a>toomodify SOA 레코드

추가 하거나 자동으로 설정 hello 영역 루트에 SOA 레코드를 생성 하는 hello에서 레코드를 제거할 수 없습니다 (`-Name "@"`, 인용 부호를 포함 하 여). 그러나 hello "호스트") (제외 SOA 레코드 내에 hello 매개 변수 중 하나를 수정 하 고 TTL을 설정 하는 hello 레코드.

hello 방법을 예제와 다음 toochange hello *전자 메일* hello SOA 레코드의 속성:

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType SOA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Email = "admin.contoso.com"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a>hello 영역 루트에 있는 toomodify NS 레코드

hello 영역 루트에서 설정 하는 hello NS 레코드는 각 DNS 영역과 자동으로 만들어집니다. Hello Azure DNS 이름 서버 할당된 toohello 영역의 hello 이름이 포함 되어 있습니다.

추가 이름 서버 toothis NS 레코드 집합을 공동 도메인 DNS 공급자를 둘 이상의 호스팅 toosupport를 추가할 수 있습니다. 또한 TTL hello 및이 레코드 집합에 대 한 메타 데이터를 수정할 수 있습니다. 그러나 제거 하거나 hello 미리 채워진된 Azure DNS 이름 서버를 수정할 수 없습니다.

Note이 적용 hello 영역 루트에서 레코드 집합 toohello NS만 됩니다. 제약 조건 없이 (사용 되는 toodelegate 하위 영역)으로 시간대에서 다른 NS 레코드 집합을 수정할 수 있습니다.

다음 예제는 hello 설정 방법을 보여 주는 tooadd 추가 이름 서버 toohello NS 레코드가 hello 영역 루트에서:

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Add-AzureRmDnsRecordConfig -RecordSet $rs -Nsdname ns1.myotherdnsprovider.com
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-record-set-metadata"></a>toomodify 레코드 메타 데이터 설정

[메타 데이터를 설정 하는 레코드](dns-zones-records.md#tags-and-metadata) 키-값 쌍으로 각 레코드 집합을 사용 하 여 사용 되는 tooassociate 응용 프로그램별 데이터 일 수 있습니다.

hello 다음 예제는 기존 레코드의 toomodify hello 메타 데이터 설정 하는 방법.

```powershell
# Get hello record set
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"

# Add 'dept=finance' name-value pair
$rs.Metadata.Add('dept', 'finance') 

# Remove metadata item named 'environment'
$rs.Metadata.Remove('environment')  

# Commit changes
Set-AzureRmDnsRecordSet -RecordSet $rs
```


## <a name="delete-a-record-set"></a>레코드 집합 삭제

Hello를 사용 하 여 레코드 집합을 삭제할 수 있습니다 `Remove-AzureRmDnsRecordSet` cmdlet. 레코드 집합을 삭제 하면 hello 레코드 집합 내의 모든 레코드가 삭제 합니다.

> [!NOTE]
> Hello NS 및 SOA 레코드 집합 hello 영역 루트에서 삭제할 수 없습니다 (`-Name '@'`).  Azure DNS 이러한 때 자동으로 생성 hello 영역을 만들었으며 hello 영역 삭제 될 때 자동으로 삭제 합니다.

hello 다음 예제에서는 설정 방법을 보여 줍니다 toodelete 레코드입니다. 이 예제에서는 hello 레코드 집합 이름, 형식 레코드 집합, 영역 이름 및 리소스 그룹은 각각 명시적으로 지정 합니다.

```powershell
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

또는 hello 레코드 집합 이름 및 유형로 지정할 수 있습니다 하 고 hello 영역 개체를 사용 하 여 지정 합니다.

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

세 번째 옵션으로 자체적으로 설정 하는 hello 레코드는 레코드 집합 개체를 사용 하 여 지정할 수 있습니다.

```powershell
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -RecordSet $rs
```

Hello 레코드 집합이 toobe 레코드 집합 개체를 사용 하 여 삭제를 지정 하는 경우 [Etag 검사](dns-zones-records.md#etags) 사용 tooensure 동시 변경 내용을 삭제 되지 않습니다. Hello 옵션을 사용할 수 있습니다 `-Overwrite` toosuppress 이러한 검사를 전환 합니다.

hello 레코드 집합 개체를 매개 변수로 전달 되는 대신도 파이프 될 수 있습니다.

```powershell
Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | Remove-AzureRmDnsRecordSet
```

## <a name="confirmation-prompts"></a>확인 메시지 표시

hello `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, 및 `Remove-AzureRmDnsRecordSet` cmdlet 모든 확인 메시지를 표시를 지원 합니다.

각 cmdlet 확인 메시지를 표시 하는 경우 hello `$ConfirmPreference` PowerShell 기본 설정 변수 값은 `Medium` 이하로 합니다. Hello 기본값에 대 한 이후 `$ConfirmPreference` 은 `High`, hello 기본 PowerShell 설정을 사용할 경우 이러한 프롬프트 제공 되지 않습니다.

Hello 현재 문자인 `$ConfirmPreference` hello를 사용 하 여 설정을 `-Confirm` 매개 변수입니다. 지정 하는 경우 `-Confirm` 또는 `-Confirm:$True` , hello cmdlet 확인 메시지가 표시 되기 전에 실행 합니다. 지정 하는 경우 `-Confirm:$False` , hello cmdlet 표시 하지 않습니다 확인 합니다. 

`-Confirm` 및 `$ConfirmPreference`에 대한 자세한 내용은 [기본 설정 변수 정보](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables)를 참조하세요.

## <a name="next-steps"></a>다음 단계

[Azure DNS의 영역 및 레코드](dns-zones-records.md)에 대해 자세히 알아봅니다.
<br>
너무 방법에 대해 알아봅니다[영역 및 레코드 보호](dns-protect-zones-recordsets.md) Azure DNS를 사용 하는 경우.
<br>
검토 hello [Azure DNS PowerShell 참조 설명서](/powershell/module/azurerm.dns)합니다.
