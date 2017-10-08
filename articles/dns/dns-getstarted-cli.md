---
title: "Azure CLI 2.0을 사용 하 여 Azure DNS aaaGet 시작 | Microsoft Docs"
description: "자세한 내용은 방법 toocreate DNS 영역 및 Azure DNS에 레코드입니다. 단계별 가이드 toocreate 이며 첫 번째 DNS 영역 및 Azure CLI 2.0 hello를 사용 하 여 레코드를 관리 합니다."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 8a894941e9910d5cc35394a1be9dbca9792613f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-20"></a>Azure CLI 2.0을 사용하여 Azure DNS 시작

> [!div class="op_single_selector"]
> * [Azure 포털](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [Azure CLI 1.0](dns-getstarted-cli-nodejs.md)
> * [Azure CLI 2.0](dns-getstarted-cli.md)

이 문서를 안내해 hello 단계 toocreate 첫 번째 DNS 영역이 및은 Windows, Mac 및 Linux 가능한 플랫폼 간 Azure CLI 2.0 hello 사용 하 여 레코드 합니다. Hello Azure 포털 또는 Azure PowerShell을 사용 하 여 이러한 단계를 수행할 수 있습니다.

DNS 영역에는 특정 도메인에 대 한 사용 되는 toohost hello DNS 레코드입니다. Azure DNS에서 도메인 호스팅 toostart toocreate DNS 영역 해당 도메인 이름을 사용 해야 합니다. 그러면 이 DNS 영역 안에 도메인의 각 DNS 레코드가 생성됩니다. 마지막으로, toopublish DNS 영역 toohello 인터넷 tooconfigure hello 이름 서버 hello 도메인에 대 한 필요 합니다. 아래에서는 이러한 각 단계에 대해 설명합니다.

이러한 지침에는 이미 설치 및 CLI 2.0 tooAzure 로그인 했다고 가정 합니다. 에 대 한 도움말을 참조 하세요. [toomanage DNS 영역 Azure CLI 2.0을 사용 하는 방법을](dns-operations-dnszones-cli.md)합니다.

## <a name="create-hello-resource-group"></a>Hello 리소스 그룹 만들기

Hello DNS 영역을 만들기 전에 리소스 그룹 toocontain hello DNS 영역이 만들어집니다. hello 다음 hello 명령을 보여 줍니다.

```azurecli
az group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a>DNS 영역 만들기

DNS 영역 hello를 사용 하 여 만들어집니다. `az network dns zone create` 명령입니다. 이 명령에 대 한 도움말 toosee 입력 `az network dns zone create -h`합니다.

hello 다음 예제에서는 호출 하는 DNS 영역 *contoso.com* hello 리소스 그룹에 *MyResourceGroup*합니다. 사용자 고유의 대 한 hello 값으로 대체 hello 예제 toocreate DNS 영역을 사용 합니다.

```azurecli
az network dns zone create -g MyResourceGroup -n contoso.com
```


## <a name="create-a-dns-record"></a>DNS 레코드 만들기

toocreate DNS 레코드를 사용 하 여 hello `az network dns record-set [record type] add-record` 명령입니다. 도움말과 A 레코드에 대한 예제는 `azure network dns record-set A add-record -h`을 참조하세요.

hello 다음 예제에서는 레코드 hello 상대 이름이 "www" hello "MyResourceGroup" 리소스 그룹에 "contoso.com", DNS 영역에서 hello 정규화 hello 레코드 집합의 이름이 "www.contoso.com" 합니다. hello 레코드 종류는 "A", "1.2.3.4" IP 주소로 하 고 기본 TTL 3600 초 (1 시간)을 사용 됩니다.

```azurecli
az network dns record-set a add-record -g MyResourceGroup -z contoso.com -n www -a 1.2.3.4
```

다른 레코드 종류에 대 한 대체 TTL 값 및 toomodify 기존 레코드에 대 한 둘 이상의 레코드와 레코드 집합에 대 한 참조 [관리 DNS 레코드 및 레코드 집합을 사용 하 여 hello Azure CLI 2.0](dns-operations-recordsets-cli.md)합니다.


## <a name="view-records"></a>레코드 보기

영역에서 toolist hello DNS 레코드를 사용 합니다.

```azurecli
az network dns record-set list -g MyResourceGroup -z contoso.com
```


## <a name="update-name-servers"></a>이름 서버 업데이트

일단 시작 되 면 DNS 영역과 레코드는 올바르게 설정 되었는지, tooconfigure 필요한 충족 도메인 이름 toouse hello Azure DNS 이름 서버입니다. 이렇게 하면 다른 사용자 hello 인터넷 toofind에 DNS 레코드입니다.

영역에 대 한 hello 이름 서버 hello에 의해 제공 됩니다 `az network dns zone show` 명령입니다. toosee hello 이름 서버 이름, hello 다음 예제에에서 나와 있는 것 처럼 JSON 출력을 사용 합니다.

```azurecli
az network dns zone show -g MyResourceGroup -n contoso.com -o json

{
  "etag": "00000003-0000-0000-b40d-0996b97ed101",
  "id": "/subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-01.azure-dns.com.",
    "ns2-01.azure-dns.net.",
    "ns3-01.azure-dns.org.",
    "ns4-01.azure-dns.info."
  ],
  "numberOfRecordSets": 3,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

이러한 이름 서버 hello 도메인 이름 등록 기관 (여기서 구입한 hello 도메인 이름)으로 구성 해야 합니다. 등록자는 hello 옵션 tooset hello 도메인에 대 한 hello 이름 서버를 제공 합니다. 자세한 내용은 참조 [사용자 도메인 tooAzure DNS 위임](dns-domain-delegation.md)합니다.

## <a name="delete-all-resources"></a>모든 리소스 삭제
 
take hello 단계 다음에이 문서에서 만든 모든 리소스를 toodelete:

```azurecli
az group delete --name MyResourceGroup
```

## <a name="next-steps"></a>다음 단계

Azure DNS에 대해 자세히 toolearn 참조 [Azure DNS 개요](dns-overview.md)합니다.

Azure DNS에 DNS 영역 관리에 대 한 더 toolearn 참조 [Azure CLI 2.0을 사용 하 여 Azure DNS에서 관리 하는 DNS 영역](dns-operations-dnszones-cli.md)합니다.

Azure DNS에 DNS 레코드를 관리에 대해 자세히 toolearn 참조 [Azure CLI 2.0을 사용 하 여 Azure DNS에 관리 DNS 레코드와 레코드 집합](dns-operations-recordsets-cli.md)합니다.
