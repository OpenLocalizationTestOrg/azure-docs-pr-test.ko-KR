---
title: "Azure aaaTag 논리 조직 위한 리소스 | Microsoft Docs"
description: "Tooapply tooorganize Azure 태그 하는 방법을 보여 줍니다. 대금 청구 및 관리에 대 한 리소스입니다."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 003a78e5-2ff8-4685-93b4-e94d6fb8ed5b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: AzurePortal
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tomfitz
ms.openlocfilehash: e07470463d160f8cefe5c80bc91e66a96af6ca45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-tags-tooorganize-your-azure-resources"></a>Azure 리소스 태그 tooorganize를 사용 하 여
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> Azure 리소스 관리자 작업을 지 원하는 유일한 tooresources 태그를 적용할 수 있습니다. 가상 컴퓨터, 가상 네트워크 또는 저장소 계정 (예: 통해 서 hello Azure 클래식 포털) hello 클래식 배포 모델을 만든 경우 태그 toothat 리소스를 적용할 수 없습니다. 태깅을 toosupport 리소스 관리자를 통해 이러한 리소스를 다시 배포 합니다. 다른 모든 리소스는 태그 지정을 지원합니다.
> 
> 

## <a name="policies-for-tag-consistency"></a>태그 일관성을 위한 정책

조직에 대 한 리소스 정책 toocreate 표준 규칙을 사용할 수 있습니다. 리소스 hello 적절 한 값으로 태그가 지정 되어 있는지 확인 하는 정책을 만들 수 있습니다. 자세한 내용은 [태그에 대한 리소스 정책 적용](resource-manager-policy-tags.md)을 참조하세요.

## <a name="powershell"></a>PowerShell
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a>Azure CLI

toosee hello에 대 한 기존 태그는 *리소스 그룹*를 사용 하 여:

```azurecli
az group show -n examplegroup --query tags
```

해당 스크립트에는 형식에 따라 hello 반환 합니다.

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

toosee hello에 대 한 기존 태그는 *를 지정 된 리소스 ID를 갖는 리소스*를 사용 하 여:

```azurecli
az resource show --id {resource-id} --query tags
```

또는 toosee hello에 대 한 기존 태그는 *지정된 된 이름, 유형 및 리소스 그룹에 있는 리소스*를 사용 하 여:

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

tooget 있는 리소스 그룹을 특정 태그를 사용 하 여 `az group list`:

```azurecli
az group list --tag Dept=IT
```

tooget 특정 태그 및 값을 가진 모든 hello 리소스 사용 `az resource list`:

```azurecli
az resource list --tag Dept=Finance
```

태그 tooa 리소스 또는 리소스 그룹을 적용할 때마다 해당 리소스 또는 리소스 그룹에 기존 태그 hello 덮어씁니다. 따라서 hello 리소스 또는 리소스 그룹에 기존 태그에 있는지 여부에 따라 다른 방법을 사용 해야 합니다. 

tooadd 태그 tooa *기존 태그 없이 리소스 그룹*를 사용 하 여:

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

tooadd 태그 tooa *기존 태그 없이 리소스*를 사용 하 여:

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

hello 기존 태그 가져오고 해당 값의 서식을 다시 지정 hello 기존 및 새 태그를 다시 적용 하는 태그를 이미가지고 있는 tooadd 태그 tooa 리소스: 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

tooapply 모든 리소스 그룹 tooits 리소스에서 태그를 삽입 하 고 *hello 리소스에 대 한 기존 태그를 유지 하지*, 다음 스크립트는 hello를 사용 하 여:

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    az resource tag --tags $t --id $resid
  done 
done
```

tooapply 모든 리소스 그룹 tooits 리소스에서 태그를 삽입 하 고 *리소스에 대 한 기존 태그 유지*, 다음 스크립트는 hello를 사용 하 여:

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    jsonrtag=$(az resource show --id $resid --query tags)
    rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
    az resource tag --tags $t$rt --id $resid
  done 
done
```


## <a name="templates"></a>템플릿

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a>포털
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a>REST API
hello Azure 포털 및 PowerShell 사용 하 여 hello [리소스 관리자 REST API](https://docs.microsoft.com/rest/api/resources/) hello 내부적입니다. Toointegrate 다른 환경으로 태그를 지정 해야 할 경우 사용 하 여 태그를 가져올 수 있습니다 **가져오기** 태그를 사용 하 여 hello 리소스 ID와 업데이트 hello 집합에는 **패치** 호출 합니다.

## <a name="tags-and-billing"></a>태그 및 청구
태그 toogroup 청구 데이터를 사용할 수 있습니다. 예를 들어 서로 다른 조직에 대 한 여러 Vm을 실행 하는 경우 hello 태그 toogroup 사용 비용 센터를 사용 합니다. Hello 프로덕션 환경에서 실행 중인 Vm에 대 한 hello 청구 사용량 등의 런타임 환경에 의해 태그 toocategorize 비용을 사용할 수도 있습니다.


Hello 통해 태그에 대 한 정보를 검색할 수 [Azure 리소스 사용량 및 RateCard Api](../billing/billing-usage-rate-card-overview.md) 또는 hello 사용 현황 쉼표로 구분 된 값 (CSV) 파일입니다. Hello에서 hello 사용량 파일을 다운로드 [Azure 계정 포털](https://account.windowsazure.com/) 또는 [EA 포털](https://ea.azure.com)합니다. 프로그래밍 방식 액세스 toobilling 정보에 대 한 자세한 내용은 참조 [Microsoft Azure 리소스 소비량에 대 한 이해력](../billing/billing-usage-rate-card-overview.md)합니다. REST API 작업에 대한 내용은 [Azure 청구 REST API 참조](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c)를 참조하세요.


Hello 태그는 hello에 나타나지 결제 태그를 지원 서비스에 대 한 hello 사용 CSV를 다운로드 하면 **태그** 열입니다. 자세한 내용은 [Microsoft Azure 청구서 이해](../billing/billing-understand-your-bill.md)를 참조하세요.

![요금 청구에 대한 태그를 참조하십시오.](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a>다음 단계
* 사용자 지정된 정책을 사용하여 구독 전체에 제한 사항 및 규칙을 적용할 수 있습니다. 정의한 정책을 사용하려면 모든 리소스에 특정 태그 값이 있어야 할 수도 있습니다. 자세한 내용은 참조 [정책 toomanage 리소스를 사용 하 고 액세스 제어](resource-manager-policy.md)합니다.
* 소개 toousing Azure PowerShell에 대 한 리소스를 배포 하는 경우 참조 [Azure PowerShell 사용 하 여 Azure 리소스 관리자와](powershell-azure-resource-manager.md)합니다.
* 소개 toousing hello Azure CLI에 대 한 리소스를 배포 하는 경우 참조 [Mac, Linux 및 Windows Azure 리소스 관리자에 대 한 Azure CLI를 사용 하 여 hello](xplat-cli-azure-resource-manager.md)합니다.
* 소개 toousing hello 포털에 대 한 참조 [사용 하 여 Azure 리소스를 Azure 포털 toomanage hello](resource-group-portal.md)합니다.  
* 기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.

