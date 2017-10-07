---
title: "Azure dns-Azure CLI 2.0 aaaManage DNS 영역 | Microsoft Docs"
description: "Azure CLI 2.0을 사용하여 DNS 영역을 관리할 수 있습니다. 이 문서에서는 tooupdate, 삭제 하 고 dns를 Azure DNS 영역을 만드는 방법을 보여 줍니다."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: gwallace
ms.openlocfilehash: 3945a558b2db3490e50678d8395a47e55a85c8fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-20"></a>Azure DNS를 사용 하 여 DNS 영역 toomanage Azure CLI 2.0 hello 하는 방법

> [!div class="op_single_selector"]
> * [포털](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-dnszones-cli.md)


이 가이드에서는 어떻게 toomanage DNS 영역을 사용 가능한 Windows, Mac 및 Linux 용 플랫폼 간 Azure CLI hello를 사용 하 여 보여 줍니다. 사용 하 여 DNS 영역을 관리할 수 있습니다 [Azure PowerShell](dns-operations-dnszones.md) 또는 Azure 포털을 환영 합니다.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 버전 toocomplete hello 작업

Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.

* [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) -hello 클래식 및 리소스 관리 배포 모델에 대 한 우리의 CLI 합니다.
* [Azure CLI 2.0](dns-operations-dnszones-cli.md) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한 합니다.

## <a name="introduction"></a>소개

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a>Azure DNS용 Azure CLI 2.0 설정

### <a name="before-you-begin"></a>시작하기 전에

구성을 시작 하기 전에 다음 항목 hello 수 있는지 확인 하십시오.

* Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 활성화하거나 [무료 계정](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.

* Hello hello Azure CLI 2.0, Windows, Linux 또는 MAC.에 사용할 수 있는의 최신 버전 설치 자세한 내용은 [설치 hello Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)합니다.

### <a name="sign-in-tooyour-azure-account"></a>Azure 계정 tooyour에 로그인

콘솔 창을 열고 자격 증명을 사용하여 인증합니다. 자세한 내용은 로그를 참조 하십시오. hello Azure CLI에서에서 tooAzure에

```
az login
```

### <a name="select-hello-subscription"></a>Hello 구독 선택

Hello 계정에 대 한 hello 구독을 확인 합니다.

```
az account list
```

Azure 구독 toouse 선택 합니다.

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a>리소스 그룹 만들기

Azure 리소스 관리자를 사용하려면 모든 리소스 그룹이 위치를 지정해야 합니다. 이것은 해당 리소스 그룹의 리소스에 대 한 hello 기본 위치로 사용 됩니다. 그러나 모든 DNS 리소스가 하지 지역, 글로벌 되므로 hello 다양 한 리소스 그룹 위치에 어떠한 영향도 미치지 Azure DNS 합니다.

기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뛸 수 있습니다.

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a>도움말 보기

TooAzure DNS와 관련 된 모든 CLI 2.0 명령을 시작 `az network dns`합니다. Hello를 사용 하 여 각 명령에 대 한 도움말은 `--help` 옵션 (약식 `-h`).  예:

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a>DNS 영역 만들기

DNS 영역 hello를 사용 하 여 만들어집니다. `az network dns zone create` 명령입니다. 도움말을 보려면 `az network dns zone create -h`을 참조하세요.

hello 다음 예제에서는 호출 하는 DNS 영역 *contoso.com* 호출 hello 리소스 그룹에 *MyResourceGroup*:

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a>toocreate 태그와 DNS 영역

hello 다음 예제에서는 두 개의 toocreate DNS 영역 방법을 [Azure 리소스 관리자 태그](dns-zones-records.md#tags), *프로젝트 데모 =* 및 *env = 테스트*, hello를 사용 하 여 `--tags` 매개 변수 (약식 `-t`):

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a>DNS 영역 가져오기

tooretrieve DNS 영역을 사용 하 여 `az network dns zone show`합니다. 도움말을 보려면 `az network dns zone show --help`을 참조하세요.

hello 다음 예제에서는 반환 hello DNS 영역 *contoso.com* 및 리소스 그룹에서 관련된 데이터 *MyResourceGroup*합니다. 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

다음 예제는 hello hello 응답입니다.

```json
{
  "etag": "00000002-0000-0000-3d4d-64aa3689d201",
  "id": "/subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-04.azure-dns.com.",
    "ns2-04.azure-dns.net.",
    "ns3-04.azure-dns.org.",
    "ns4-04.azure-dns.info."
  ],
  "numberOfRecordSets": 4,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

DNS 레코드는 `az network dns zone show`에서 반환되지 않습니다. toolist DNS 레코드를 사용 하 여 `az network dns record-set list`합니다.


## <a name="list-dns-zones"></a>DNS 영역 나열

tooenumerate DNS 영역을 사용 하 여 `az network dns zone list`합니다. 도움말을 보려면 `az network dns zone list --help`을 참조하세요.

Hello 리소스 그룹을 지정 하 여 hello 리소스 그룹 내에서 해당 영역에만 나열합니다.

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

Hello 리소스 그룹을 생략 hello 구독의 모든 영역을 나열합니다.

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a>DNS 영역 업데이트

사용 하 여 DNS 영역 리소스를 제공할 수는 변경 내용 tooa `az network dns zone update`합니다. 도움말을 보려면 `az network dns zone update --help`을 참조하세요.

이 명령은 hello hello 영역 내에서 DNS 레코드 집합의 업데이트 되지 않는 (참조 [어떻게 tooManage DNS 레코드](dns-operations-recordsets-cli.md)). Hello 영역 리소스 자체의 속성을 사용 하는 유일한 tooupdate 것합니다. 이러한 속성은 현재 제한 toohello [Azure 리소스 관리자 '태그'](dns-zones-records.md#tags) hello 영역의 리소스에 대 한 합니다.

hello 다음 예제에서는 tooupdate hello DNS 영역에 태그를 삽입 방법 hello 기존 태그는 지정 된 hello 값으로 대체 됩니다.

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a>DNS 영역 삭제

`az network dns zone delete`를 사용하여 DNS 영역을 삭제할 수 있습니다. 도움말을 보려면 `az network dns zone delete --help`을 참조하세요.

> [!NOTE]
> DNS 영역을 삭제 하면 모든 DNS 레코드가 hello 영역 내에서 삭제 합니다. 이 작업은 취소할 수 없습니다. DNS 영역 hello를 사용 하는 경우 hello 영역이 삭제 되 면 hello 영역을 사용 하 여 서비스 실패 합니다.
>
>실수로 영역 삭제 tooprotect 참조 [tooprotect DNS 영역 및 기록 방법을](dns-protect-zones-recordsets.md)합니다.

이 명령은 확인 메시지를 표시합니다. 선택적 hello `--yes` 스위치가이 프롬프트를 표시 하지 않습니다.

hello 다음 예제에서는 어떻게 toodelete hello 영역 *contoso.com* 리소스 그룹에서 *MyResourceGroup*합니다.

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a>다음 단계

너무 방법에 대해 알아봅니다[레코드 집합 및 레코드 관리](dns-getstarted-create-recordset-cli.md) DNS 영역에 있습니다.

너무 방법에 대해 알아봅니다[사용자 도메인 tooAzure DNS 위임](dns-domain-delegation.md)합니다.

