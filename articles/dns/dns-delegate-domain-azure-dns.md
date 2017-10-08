---
title: "aaaDelegate 사용자 도메인 tooAzure DNS | Microsoft Docs"
description: "이름을 어떻게 지정 toochange 도메인 위임 및 Azure DNS를 사용 하 여 서버 tooprovide 도메인 호스팅 이해 합니다."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 257da6ec-d6e2-4b6f-ad76-ee2dde4efbcc
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: gwallace
ms.openlocfilehash: f780bdaa416150e5e3afe6c6845dc75ba54b6203
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-a-domain-tooazure-dns"></a>도메인 tooAzure DNS 위임

Azure DNS toohost DNS 영역을 허용 하 고 Azure에서 도메인에 대 한 hello DNS 레코드를 관리 합니다. 도메인 tooreach Azure DNS에 대 한 DNS 쿼리에 대 한 순서로 hello 도메인에 toobe tooAzure DNS hello 부모 도메인에서 위임 합니다. Azure DNS에 유의 hello 도메인 등록 기관 않습니다. 이 문서에서는 설명 방법을 toodelegate 사용자 도메인 tooAzure DNS 합니다.

도메인 등록 기관에서 구매에 대 한 등록 자가 hello 옵션 tooset이 NS 레코드를 제공 합니다. 않아도 tooown 도메인 toocreate 해당 도메인 이름 사용 하 여 DNS 영역을 Azure DNS에 있습니다. 그러나 hello 등록 기관과 함께 hello 위임 tooAzure DNS tooown hello 도메인 tooset이 필요지 않습니다.

예를 들어 'contoso.net' hello 도메인을 구입 하 고 Azure DNS contoso.net' hello 이름'를 사용 하 여 영역을 만들어야 합니다. Hello 도메인의 hello 소유자로 등록 자가 옵션 tooconfigure hello 이름 서버 주소 (즉, hello NS 레코드) 도메인에 대 한 hello를 제공 합니다. hello 등록 자가이 경우 '.net' hello 부모 도메인의 이러한 NS 레코드를 저장합니다. 그런 다음 클라이언트 hello 전 세계는 'contoso.net'에서 DNS 레코드 tooresolve 하려고 할 때 Azure DNS 영역에서 tooyour 방향이 지정 된 도메인을 포함할 수 있습니다.

## <a name="create-a-dns-zone"></a>DNS 영역 만들기

1. Azure 포털 toohello에 로그인
1. Hello 허브 메뉴에서를 클릭 하 고 클릭 **새로 만들기 > 네트워킹 >** 클릭 하 고 **DNS 영역** tooopen hello 만들 DNS 영역 블레이드입니다.

    ![DNS 영역](./media/dns-domain-delegation/dns.png)

1. Hello에 **만들 DNS 영역** 블레이드 hello 다음 값을 입력 한 다음 클릭 **만들기**:

   | **설정** | **값** | **세부 정보** |
   |---|---|---|
   |**Name**|contoso.net|hello hello DNS 영역 이름|
   |**구독**|[구독 이름]|구독 toocreate hello 응용 프로그램 게이트웨이 선택 합니다.|
   |**리소스 그룹**|**새로 만들기:** contosoRG|리소스 그룹을 만듭니다. hello 리소스 그룹 이름은 선택한 hello 구독 내에서 고유 해야 합니다. 리소스 그룹을 읽기 hello에 대 한 자세한 toolearn [리소스 관리자](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) 개요 문서.|
   |**위치**:|미국 서부||

> [!NOTE]
> hello 리소스 그룹 hello 리소스 그룹의 toohello 위치 참조 되었으며 hello DNS 영역에 영향을 주지 않습니다. hello DNS 영역의 위치는 항상 "전역" 하 고 표시 되지 않습니다.

## <a name="retrieve-name-servers"></a>이름 서버 검색

DNS 영역 tooAzure DNS를 위임할 수 있습니다, 전에 먼저 해당 영역의 tooknow hello 이름 서버 이름을 해야 합니다. Azure DNS는 영역이 만들어질 때마다 풀에서 이름 서버를 할당합니다.

1. Hello Azure 포털에서에서 만든 hello DNS 영역과 **즐겨찾기** 창에서 클릭 **모든 리소스**합니다. Hello 클릭 **contoso.net** hello의 DNS 영역 **모든 리소스** 블레이드입니다. 이미 선택한 hello 구독에 여러 자원이 인 경우 입력 하면 **contoso.net** 이름별 필터 hello에... 상자 tooeasily 액세스 hello 응용 프로그램 게이트웨이 합니다. 

1. Hello DNS 영역 블레이드에서 hello 이름 서버를 검색 합니다. 이 예제에서는 hello 영역 'contoso.net' 할당 된 이름 서버에 ' n s 1-01.azure-dns.com', 'ns2 01.azure dns.net', ' ns3-01.azure-dns.org', 및 ' ns4-01.azure-dns.info':

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

Azure DNS hello 지정 된 이름 서버를 포함 하 여 영역에 권한 있는 NS 레코드를 자동으로 만듭니다.  Azure PowerShell 또는 Azure CLI를 통해 toosee hello 이름 서버 이름을 지정 하기만 하면 tooretrieve 이러한 레코드, 합니다.

hello 다음 예에서는 단계도 설명 hello tooretrieve hello 이름 서버에서 PowerShell 및 Azure CLI Azure DNS 영역에 대 한 합니다.

### <a name="powershell"></a>PowerShell

```powershell
# hello record name "@" is used toorefer toorecords at hello top of hello zone.
$zone = Get-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -Zone $zone
```

다음 예제는 hello hello 응답입니다.

```
Name              : @
ZoneName          : contoso.net
ResourceGroupName : contosorg
Ttl               : 172800
Etag              : 03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5
RecordType        : NS
Records           : {ns1-07.azure-dns.com., ns2-07.azure-dns.net., ns3-07.azure-dns.org.,
                    ns4-07.azure-dns.info.}
Metadata          :
```

### <a name="azure-cli"></a>Azure CLI

```azurecli
az network dns record-set show --resource-group contosoRG --zone-name contoso.net --type NS --name @
```

다음 예제는 hello hello 응답입니다.

```json
{
  "etag": "03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosoRG/providers/Microsoft.Network/dnszones/contoso.net/NS/@",
  "metadata": null,
  "name": "@",
  "nsRecords": [
    {
      "nsdname": "ns1-07.azure-dns.com."
    },
    {
      "nsdname": "ns2-07.azure-dns.net."
    },
    {
      "nsdname": "ns3-07.azure-dns.org."
    },
    {
      "nsdname": "ns4-07.azure-dns.info."
    }
  ],
  "resourceGroup": "contosoRG",
  "ttl": 172800,
  "type": "Microsoft.Network/dnszones/NS"
}
```

## <a name="delegate-hello-domain"></a>대리자 hello 도메인

Hello DNS 영역을 만들면이 고 hello 이름 서버에 hello 부모 도메인이 보았습니다 toobe를 hello Azure DNS 이름 서버를 업데이트 합니다. 각 등록자는 자신의 DNS 관리 도구 toochange hello 이름 서버 레코드를 도메인에 있습니다. Hello 등록자의 DNS 관리 페이지에서 hello NS 레코드를 편집 하 고 Azure DNS 만든 hello 것으로 hello NS 레코드를 바꿉니다.

도메인 tooAzure DNS를 위임할 때는 Azure DNS에서 제공 하는 hello 이름 서버 이름을 사용 해야 합니다. Toouse 모든 것이 좋습니다 4 hello 도메인 이름에 관계 없이 서버 이름, 이름을 지정 합니다. 도메인 위임 hello 이름 서버 이름 toouse 필요 하지 않습니다 hello 도메인와 같은 최상위 도메인입니다.

이러한 IP 주소는 나중에 변경 될 수 있습니다 때문 '연결 레코드가' toopoint toohello Azure DNS 이름 서버 IP 주소를 사용 해야 하지 않습니다. 고유한 영역에서 이름 서버 이름을 사용하는 위임('베니티 이름 서버'라고도 함)은 현재 Azure DNS에서 지원되지 않습니다.

## <a name="verify-name-resolution-is-working"></a>이름 확인이 작동하는지 확인

Hello 위임을 완료 한 후 프로그램 5d; 영역 (자동으로 만들어집니다 hello 영역을 만들 때)에 대 한 'nslookup' tooquery hello SOA 레코드와 같은 도구를 사용 하 여 이름 확인이 작동 하는지 확인할 수 있습니다.

Toospecify hello Azure DNS 이름 서버에 없는, hello 위임 올바르게 hello 일반 DNS 확인 프로세스를 설정한 경우 hello 이름 서버를 자동으로 찾습니다.

```
nslookup -type=SOA contoso.com
```

hello 다음은 hello 명령 앞의 예제 응답입니다.

```
Server: ns1-04.azure-dns.com
Address: 208.76.47.4

contoso.com
primary name server = ns1-04.azure-dns.com
responsible mail addr = msnhst.microsoft.com
serial = 1
refresh = 900 (15 mins)
retry = 300 (5 mins)
expire = 604800 (7 days)
default TTL = 300 (5 mins)
```

## <a name="delegate-sub-domains-in-azure-dns"></a>Azure DNS에서 하위 도메인 위임

별도 자식 영역을 tooset 하려는 경우 Azure dns에서 하위 도메인을 위임할 수 있습니다. 예를 들어 있으면 설정 하 고 Azure dns에서 위임된 'contoso.net' tooset 별도 자식 영역을 선택 한다고 가정 'partners.contoso.net'.

1. Azure DNS partners.contoso.net을' hello 자식 영역' 만듭니다.
2. Hello Azure DNS에 hello 자식 영역을 호스팅하는 hello 자식 영역 tooobtain hello 이름 서버에 권한 있는 NS 레코드를 조회 합니다.
3. Toohello 자식 영역을 가리키는 hello 부모 영역에서 NS 레코드를 구성 하 여 hello 자식 영역을 위임 합니다.

### <a name="create-a-dns-zone"></a>DNS 영역 만들기

1. Azure 포털 toohello에 로그인
1. Hello 허브 메뉴에서를 클릭 하 고 클릭 **새로 만들기 > 네트워킹 >** 클릭 하 고 **DNS 영역** tooopen hello 만들 DNS 영역 블레이드입니다.

    ![DNS 영역](./media/dns-domain-delegation/dns.png)

1. Hello에 **만들 DNS 영역** 블레이드 hello 다음 값을 입력 한 다음 클릭 **만들기**:

   | **설정** | **값** | **세부 정보** |
   |---|---|---|
   |**Name**|partners.contoso.net|hello hello DNS 영역 이름|
   |**구독**|[구독 이름]|구독 toocreate hello 응용 프로그램 게이트웨이 선택 합니다.|
   |**리소스 그룹**|**기존 리소스 그룹 사용:** contosoRG|리소스 그룹을 만듭니다. hello 리소스 그룹 이름은 선택한 hello 구독 내에서 고유 해야 합니다. 리소스 그룹을 읽기 hello에 대 한 자세한 toolearn [리소스 관리자](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) 개요 문서.|
   |**위치**:|미국 서부||

> [!NOTE]
> hello 리소스 그룹 hello 리소스 그룹의 toohello 위치 참조 되었으며 hello DNS 영역에 영향을 주지 않습니다. hello DNS 영역의 위치는 항상 "전역" 하 고 표시 되지 않습니다.

### <a name="retrieve-name-servers"></a>이름 서버 검색

1. Hello Azure 포털에서에서 만든 hello DNS 영역과 **즐겨찾기** 창에서 클릭 **모든 리소스**합니다. Hello 클릭 **partners.contoso.net** hello의 DNS 영역 **모든 리소스** 블레이드입니다. 이미 선택한 hello 구독에 여러 자원이 인 경우 입력 하면 **partners.contoso.net** 이름별 필터 hello에... 상자 tooeasily 액세스 hello DNS 영역입니다.

1. Hello DNS 영역 블레이드에서 hello 이름 서버를 검색 합니다. 이 예제에서는 hello 영역 'contoso.net' 할당 된 이름 서버에 ' n s 1-01.azure-dns.com', 'ns2 01.azure dns.net', ' ns3-01.azure-dns.org', 및 ' ns4-01.azure-dns.info':

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

Azure DNS hello 지정 된 이름 서버를 포함 하 여 영역에 권한 있는 NS 레코드를 자동으로 만듭니다.  Azure PowerShell 또는 Azure CLI를 통해 toosee hello 이름 서버 이름을 지정 하기만 하면 tooretrieve 이러한 레코드, 합니다.

### <a name="create-name-server-record-in-parent-zone"></a>부모 영역에 이름 서버 레코드 만들기

1. Toohello 이동 **contoso.net** hello Azure 포털에서에서 DNS 영역입니다.
1. **+ 레코드 집합**을 클릭합니다.
1. Hello에 **레코드 집합을 추가** 블레이드에서 hello 다음 값을 입력 한 다음 클릭 **확인**:

   | **설정** | **값** | **세부 정보** |
   |---|---|---|
   |**Name**|파트너|hello hello 자식 DNS 영역 이름|
   |**형식**|NS|이름 서버 레코드에 NS를 사용합니다.|
   |**TTL**|1|Toolive 사용 되는 시간입니다.|
   |**TTL 단위**|시간|시간 단위 toolive toohours 설정|
   |**이름 서버**|{partners.contoso.net 영역의 이름 서버}|Partners.contoso.net 영역에서 모든 4 hello 이름 서버를 입력 합니다. |

   ![Dns-nameserver](./media/dns-domain-delegation/partnerzone.png)


### <a name="delegating-sub-domains-in-azure-dns-with-other-tools"></a>다른 도구를 사용하여 Azure DNS에서 하위 도메인 위임

hello 다음 예제에서는 제공 hello 단계 toodelegate PowerShell 및 CLI Azure DNS에 하위 도메인:

#### <a name="powershell"></a>PowerShell

다음 PowerShell 예에서는 hello이 작동 방식을 보여 줍니다. hello hello Azure 포털을 통해 실행할 수 있습니다 또는 hello 플랫폼 간 Azure CLI를 통해 동일한 단계를 포함 합니다.

```powershell
# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
$parent = New-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
$child = New-AzureRmDnsZone -Name partners.contoso.net -ResourceGroupName contosoRG

# Retrieve hello authoritative NS records from hello child zone as shown in hello next example. This contains hello name servers assigned toohello child zone.
$child_ns_recordset = Get-AzureRmDnsRecordSet -Zone $child -Name "@" -RecordType NS

# Create hello corresponding NS record set in hello parent zone toocomplete hello delegation. hello record set name in hello parent zone matches hello child zone name, in this case "partners".
$parent_ns_recordset = New-AzureRmDnsRecordSet -Zone $parent -Name "partners" -RecordType NS -Ttl 3600
$parent_ns_recordset.Records = $child_ns_recordset.Records
Set-AzureRmDnsRecordSet -RecordSet $parent_ns_recordset
```

사용 하 여 `nslookup` 모든 항목이 올바르게 설정 되어 hello hello 자식 영역 SOA 레코드를 조회 하 여 tooverify 합니다.

```
nslookup -type=SOA partners.contoso.com
```

```
Server: ns1-08.azure-dns.com
Address: 208.76.47.8

partners.contoso.com
    primary name server = ns1-08.azure-dns.com
    responsible mail addr = msnhst.microsoft.com
    serial = 1
    refresh = 900 (15 mins)
    retry = 300 (5 mins)
    expire = 604800 (7 days)
    default TTL = 300 (5 mins)
```

#### <a name="azure-cli"></a>Azure CLI

```azurecli
#!/bin/bash

# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
az network dns zone create -g contosoRG -n contoso.net
az network dns zone create -g contosoRG -n partners.contoso.net
```

Hello 이름 서버 hello에 대 한 검색 `partners.contoso.net` hello 출력에서 영역입니다.

```
{
  "etag": "00000003-0000-0000-418f-250de2b2d201",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosorg/providers/Microsoft.Network/dnszones/partners.contoso.net",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "partners.contoso.net",
  "nameServers": [
    "ns1-09.azure-dns.com.",
    "ns2-09.azure-dns.net.",
    "ns3-09.azure-dns.org.",
    "ns4-09.azure-dns.info."
  ],
  "numberOfRecordSets": 2,
  "resourceGroup": "contosorg",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

레코드 집합 hello와 각 이름 서버에 대 한 NS 레코드를 만듭니다.

```azurecli
#!/bin/bash

# Create hello record set
az network dns record-set ns create --resource-group contosorg --zone-name contoso.net --name partners

# Create a ns record for each name server.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns1-09.azure-dns.com.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns2-09.azure-dns.net.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns3-09.azure-dns.org.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns4-09.azure-dns.info.
```

## <a name="delete-all-resources"></a>모든 리소스 삭제

이 문서에서는 다음 단계 완료 hello에서에서 만든 모든 리소스를 toodelete:

1. Hello Azure 포털에서에서 **즐겨찾기** 창에서 클릭 **모든 리소스**합니다. Hello 클릭 **contosorg** 리소스 그룹 hello에서 모든 리소스 블레이드입니다. 이미 선택한 hello 구독에 여러 자원이 인 경우 입력 하면 **contosorg** hello에 **이름별으로 필터링...** 상자 tooeasily 액세스 hello 리소스 그룹입니다.
1. Hello에 **contosorg** 블레이드에서 hello 클릭 **삭제** 단추입니다.
1. hello 포털 해야 tootype hello 이름의 hello 리소스 그룹 tooconfirm toodelete 원하는 것입니다. 형식 *contosorg* hello 리소스 그룹 이름에 대 한 클릭 **삭제**합니다. 리소스 그룹을 삭제 hello 리소스 그룹 내에서 모든 리소스에 있으므로 항상 있는지 tooconfirm 리소스 그룹의 hello 내용을 삭제 하기 전에 합니다. hello 포털 hello 리소스 그룹 내에 포함 된 모든 리소스를 삭제 한 다음 자체 hello 리소스 그룹을 삭제 합니다. 이 프로세스는 몇 분 정도 걸립니다.

## <a name="next-steps"></a>다음 단계

[DNS 영역 관리](dns-operations-dnszones.md)

[DNS 레코드 관리](dns-operations-recordsets.md)
