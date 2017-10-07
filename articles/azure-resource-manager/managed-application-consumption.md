---
title: "Azure aaaConsume 관리 응용 프로그램 | Microsoft Docs"
description: "고객이 게시된 파일에서 Azure 관리되는 응용 프로그램을 만드는 방법에 대해 설명합니다."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b8510086eb05304c0e351a391b7e0cf34a467568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-internal-managed-application"></a>내부 관리되는 응용 프로그램 사용

조직의 구성원을 위한 Azure [관리 응용 프로그램](managed-application-overview.md)을 사용할 수 있습니다. 예를 들어 조직 표준을 준수하도록 하는 IT 부서에서 관리되는 응용 프로그램을 선택할 수 있습니다. 이러한 관리 되는 응용 프로그램은 hello 하지 hello Azure 마켓플레이스 서비스 카탈로그를 통해 사용할 수 있습니다.

이 문서의 계속 하기 전에 구독에 대 한 관리 되는 응용 프로그램 hello 서비스 카탈로그에서 사용할 수 있어야 합니다. 조직의 다른 사용자가 관리되는 응용 프로그램을 가지고 있지 않은 경우 [내부 사용을 위한 관리되는 응용 프로그램 게시](managed-application-publishing.md)를 참조하세요.

현재 Azure CLI 또는 hello Azure 포털 tooconsume 관리 되는 응용 프로그램 중 하나를 사용할 수 있습니다.

## <a name="create-hello-managed-application-by-using-hello-portal"></a>Hello 포털을 사용 하 여 hello 관리 되는 응용 프로그램 만들기

다음이 단계를 수행 하는 toodeploy hello 포털을 통해 관리 되는 응용 프로그램:

1. Azure 포털 toohello를 이동 합니다. **서비스 카탈로그 관리되는 응용 프로그램**을 검색합니다.

   ![서비스 카탈로그 관리되는 응용 프로그램](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. Select hello toocreate 사용 가능한 솔루션 hello 목록에서 원하는 응용 프로그램을 관리 합니다. **만들기**를 선택합니다.

   ![관리되는 응용 프로그램 선택](./media/managed-application-consumption/select-offer.png)

1. Hello 매개 변수를 필요한 tooprovision hello 리소스에 대 한 값을 제공 합니다. 위치에 **미국 중서부**를 선택합니다. **확인**을 선택합니다.

   ![관리되는 응용 프로그램 매개 변수](./media/managed-application-consumption/input-parameters.png)

1. hello 템플릿 제공한 hello 값의 유효성을 검사 합니다. 유효성 검사는 성공 하는 경우 선택 **확인** toostart hello 배포 합니다.

   ![관리되는 응용 프로그램 유효성 검사](./media/managed-application-consumption/validation.png)

Hello 배포 완료 되 면 hello 서식 파일에 정의 된 hello 적절 한 리소스는 사용자가 제공한 hello 관리 되는 리소스 그룹에 프로 비전 됩니다.

## <a name="create-hello-managed-application-by-using-azure-cli"></a>Azure CLI를 사용 하 여 hello 관리 되는 응용 프로그램 만들기

두 가지 방법으로 toocreate 관리 되는 응용 프로그램을 Azure CLI를 사용 하 여

* 관리 되는 응용 프로그램을 만들기 위한 hello 명령을 사용 합니다.
* Hello 일반 템플릿 배포 명령을 사용 합니다.

### <a name="use-hello-template-deployment-command"></a>Hello 템플릿 배포 명령을 사용 하 여

만든 공급 업체 hello hello applianceMainTemplate.json 파일을 배포 합니다.

그런 다음 두 개의 리소스 그룹을 만듭니다. hello 첫 번째 리소스 그룹은 hello 관리 되는 응용 프로그램 리소스를 만들 위치: Microsoft.Solutions/appliances 합니다. 두 번째 리소스 그룹 hello mainTemplate.json에 정의 된 hello 리소스를 모두 포함 되어 있습니다. 이 리소스 그룹은 hello ISV에 의해 관리 됩니다.

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> 사용 하 여 `westcentralus` hello 리소스 그룹의 hello 위치로 합니다.
>

mainResourceGroup, 다음 명령을 사용 하 여 hello에에서 toodeploy applianceMainTemplate.json:

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

Hello 템플릿 실행 앞, 뒤 묻는 hello hello 서식 파일에 정의 된 hello 매개 변수 값에 대 한 합니다. 또한 toohello 매개 변수를 필요한 tooprovision 리소스 서식 파일에, 두 가지 주요 매개 변수 값이 필요 하면:

- **managedResourceGroupId**: hello hello 리소스 그룹 포함 hello에에서 정의 된 리소스 applianceMainTemplate.json의 ID입니다. hello 폼의 hello ID가 `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`합니다. hello ID의 예에서는 앞에 오는 hello에서 `managedResourceGroup`합니다.
- **applianceDefinitionId**: 관리 되는 응용 프로그램 정의 리소스의 hello hello ID입니다. 이 값은 hello ISV가 제공 됩니다.

> [!NOTE]
> hello 게시자 hello 관리 되는 응용 프로그램 정의 포함 하는 액세스 toohello 리소스 그룹에 부여 해야 합니다. hello 정의 리소스가 hello 게시자 구독에 생성 됩니다. 따라서, 사용자, 사용자 그룹 또는 응용 프로그램 hello 고객 테 넌 트에 대 한 읽기 액세스 toothis 리소스가 필요합니다.

관리 되는 hello 참조 hello 배포 성공적으로 완료 되 면 mainResourceGroup 응용 프로그램을 만듭니다. hello storageAccount 리소스 managedResourceGroup에 만들어집니다.

### <a name="use-hello-create-command"></a>사용 하 여 hello 명령 만들기

Hello를 사용할 수 있습니다 `az managedapp create` 명령 toocreate hello에서 관리 되는 응용 프로그램 관리 응용 프로그램 정의 합니다.

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* **어플라이언스 정의 Id**: hello의 리소스 ID hello hello 앞 단계에서에서 만든 응용 프로그램 정의 관리 합니다. tooobtain hello 다음 명령을 실행 하는이 ID에:

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  이 명령은 관리 되는 hello 응용 프로그램 정의 반환합니다. Hello hello ID 속성 값이 필요합니다.

* **관리-rg-id**: hello 리소스 그룹 포함 hello에에서 정의 된 리소스 applianceMainTemplate.json의 hello 이름입니다. 이 리소스 그룹은 hello 관리 되는 리소스 그룹입니다. Hello 게시자가이 기능을 관리 합니다. 리소스 그룹이 없는 경우 현재 사용자에 대해 만들어집니다.
* **리소스 그룹**: hello 응용 프로그램 리소스 관리는 hello 리소스 그룹이 만들어집니다. hello Microsoft.Solutions/appliance 리소스가이 리소스 그룹에서 실행 됩니다.
* **매개 변수**: hello applianceMainTemplate.json에 정의 된 hello 리소스에 필요한 매개 변수입니다.

## <a name="known-issues"></a>알려진 문제

이 미리 보기 릴리스에서 될 hello를 포함 되어 있습니다.

* 500 내부 서버 오류 hello 관리 되는 응용 프로그램의 hello 생성 중에 나타납니다. 이 문제를 실행 하면 가능성이 toobe 간헐적으로 발생 됩니다. Hello 작업을 다시 시도 합니다.
* Hello 관리 되는 리소스 그룹에 대 한 새 리소스 그룹이 필요 합니다. 기존 리소스 그룹을 사용 하 여 hello 배포가 실패 합니다.
* hello hello Microsoft.Solutions/appliances 리소스가 포함 된 리소스 그룹에에서 만들어야 hello **westcentralus** 위치 합니다.

## <a name="next-steps"></a>다음 단계

* 소개 toomanaged 응용 프로그램에 대 한 참조 [관리 되는 응용 프로그램 개요](managed-application-overview.md)합니다.
* 서비스 카탈로그 관리되는 응용 프로그램을 게시하는 방법에 대한 자세한 내용은 [서비스 카탈로그 관리되는 응용 프로그램 만들기 및 게시](managed-application-publishing.md)를 참조하세요.
* 게시는 관리 되는 응용 프로그램 toohello Azure Marketplace에 대 한 정보를 참조 하십시오. [Azure 마켓플레이스 hello에 대 한 응용 프로그램 관리](managed-application-author-marketplace.md)합니다.
* Hello 시장에서에서 관리 되는 응용 프로그램을 사용 하는 방법에 대 한 정보를 참조 하십시오. [사용할 Azure 관리 응용 프로그램 마켓플레이스 hello에](managed-application-consume-marketplace.md)합니다.
