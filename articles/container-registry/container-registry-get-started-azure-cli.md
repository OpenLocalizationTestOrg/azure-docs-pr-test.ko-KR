---
title: "aaaCreate 개인 Docker 컨테이너 레지스트리-Azure CLI | Microsoft Docs"
description: "만들기 및 관리 사설 Docker 컨테이너 레지스트리 Azure CLI 2.0 hello로 시작."
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0d876a70b71a5e1bd564fbc9198f693dfe8a347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-cli-20"></a>Hello Azure CLI 2.0을 사용 하 여 개인 Docker 컨테이너 등록 만들기
명령을 사용 하 여 hello에 [Azure CLI 2.0](https://github.com/Azure/azure-cli) toocreate 컨테이너 레지스트리 및 Windows, Linux 또는 Mac 컴퓨터에서 해당 설정을 관리 합니다. 또한 생성 하 고 컨테이너 레지스트리에 hello를 사용 하 여 관리 수 [Azure 포털](container-registry-get-started-portal.md) 또는 프로그래밍 방식으로 컨테이너 레지스트리 hello [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376)합니다.


* 배경 및 개념에 대 한 참조 [hello 개요](container-registry-intro.md)
* 컨테이너 레지스트리 CLI 명령에 대 한 도움말 (`az acr` 명령)을 hello 전달 `-h` tooany 명령 매개 변수입니다.


## <a name="prerequisites"></a>필수 조건
* **Azure CLI 2.0**: tooinstall CLI 2.0 hello로 시작 하 고 hello를 참조 하십시오 [설치 지침](/cli/azure/install-azure-cli)합니다. 실행 하 여 Azure 구독 tooyour 로그인 `az login`합니다. 자세한 내용은 참조 [hello CLI 2.0 시작](/cli/azure/get-started-with-azure-cli)합니다.
* **리소스 그룹**: 컨테이너 레지스트리를 만들기 전에 [리소스 그룹](../azure-resource-manager/resource-group-overview.md#resource-groups)을 만들거나 기존 리소스 그룹을 사용합니다. 컨테이너 레지스트리 서비스가 hello는 위치에는 hello 리소스 그룹이 있는지 확인 [사용 가능한](https://azure.microsoft.com/regions/services/)합니다. 사용 하 여 리소스 그룹 toocreate CLI 2.0 hello 참조 [hello CLI 2.0 참조](/cli/azure/group)합니다.
* **저장소 계정** (선택 사항): 표준 Azure 만들기 [저장소 계정](../storage/common/storage-introduction.md) tooback hello 컨테이너 레지스트리 hello에서 동일한 위치입니다. 사용 하 여 레지스트리를 만들 때 저장소 계정을 지정 하지 않으면 `az acr create`, 솔루션이 hello 명령을 생성 합니다. 사용 하 여 저장소 계정을 toocreate CLI 2.0 hello를 참조 하십시오. [hello CLI 2.0 참조](/cli/azure/storage/account)합니다. Premium Storage는 현재 지원되지 않습니다.
* **서비스 사용자** (선택 사항): hello CLI로 레지스트리를 만들 때 기본적으로이 속성은 설정 하지 액세스용 합니다. 필요에 따라 기존 Azure Active Directory 서비스 보안 주체 tooa 레지스트리의 할당할 수 있습니다 (또는 새 할당)을 만들고 hello 레지스트리 관리자 사용자 계정 사용 또는 사용 합니다. 이 문서의 뒷부분에 나오는 hello 섹션을 참조 하십시오. 레지스트리 액세스 하는 방법에 대 한 자세한 내용은 참조 [hello 컨테이너 레지스트리로 인증](container-registry-authentication.md)합니다.

## <a name="create-a-container-registry"></a>컨테이너 레지스트리 만들기
Hello 실행 `az acr create` 명령 toocreate 컨테이너 레지스트리 합니다.

> [!TIP]
> 레지스트리를 만들 때 전역적으로 고유한 최상위 도메인 이름(문자 및 숫자만 포함)을 지정합니다. hello 예에서 hello 레지스트리 이름이 `myRegistry1`, 되지만 대신 사용자 고유의의 고유 이름입니다.
>
>

다음 명령을 사용 하 여 최소한의 매개 변수 toocreate 컨테이너 레지스트리 hello hello `myRegistry1` hello 리소스 그룹에 `myResourceGroup`, hello를 사용 하 여 및 *기본* sku:

```azurecli
az acr create --name myRegistry1 --resource-group myResourceGroup --sku Basic
```

* `--storage-account-name` 는 선택 사항입니다. 하지 않은 경우, 지정 된 저장소 계정을 hello 레지스트리 이름으로 된 이름을 만들어지고 타임 스탬프 hello에서 리소스 그룹을 지정 합니다.

Hello 레지스트리를 만들면 hello 출력은 유사한 toohello 다음.

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T18:36:29.124842+00:00",
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry
/registries/myRegistry1",
  "location": "southcentralus",
  "loginServer": "myregistry1.azurecr.io",
  "name": "myRegistry1",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "myregistry123456789"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}

```


특별 고려 사항:

* `id`-Hello 레지스트리에 tooassign 서비스 사용자를 원하는 경우 필요 하면 구독에 대 한 식별자입니다.
* `loginServer`-hello 정규화 된 이름을 너무 지정[toohello 레지스트리 로그인](container-registry-authentication.md)합니다. 이 예제에서는 hello 이름이 `myregistry1.exp.azurecr.io` (모두 소문자).

## <a name="assign-a-service-principal"></a>서비스 주체 할당
CLI 2.0 명령을 tooassign Azure Active Directory 서비스 보안 주체 tooa 레지스트리를 사용 합니다. hello 이러한 예에서 서비스 사용자는 할당 hello 소유자 역할 되지만 할당할 수 있습니다 [다른 역할](../active-directory/role-based-access-control-configure.md) 들어 있습니다.

### <a name="create-a-service-principal-and-assign-access-toohello-registry"></a>서비스 사용자를 만들고 액세스 toohello 레지스트리를 할당 합니다.
다음 명령을 hello에서 새 서비스 사용자 식별자가 할당 된 소유자 역할 액세스 toohello 레지스트리 hello와 함께 전달 `--scopes` 매개 변수입니다. Hello로 강력한 암호를 지정 `--password` 매개 변수입니다.

```azurecli
az ad sp create-for-rbac --scopes /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --password myPassword
```



### <a name="assign-an-existing-service-principal"></a>기존 서비스 주체 할당
이미 서비스 사용자를 갖고 있으며 tooassign 원하는 경우 해당 소유자 역할 액세스 toohello 레지스트리, 다음 예제 명령은 비슷한 toohello를 실행 합니다. Hello를 사용 하 여 hello 서비스 주 응용 프로그램 ID를 전달 하면 `--assignee` 매개 변수:

```azurecli
az role assignment create --scope /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --assignee myAppId
```



## <a name="manage-admin-credentials"></a>관리자 자격 증명 관리
관리자 계정은 각 컨테이너 레지스트리에 대해 자동으로 생성되며 기본적으로 비활성화됩니다. 다음 예제에서는 보여 hello `az acr` CLI toomanage hello 관리자 자격 증명 컨테이너 레지스트리에 대 한 명령입니다.

### <a name="obtain-admin-user-credentials"></a>관리자 사용자 자격 증명 가져오기
```azurecli
az acr credential show -n myRegistry1
```

### <a name="enable-admin-user-for-an-existing-registry"></a>기존 레지스트리에 대한 관리자 사용자 활성화
```azurecli
az acr update -n myRegistry1 --admin-enabled true
```

### <a name="disable-admin-user-for-an-existing-registry"></a>기존 레지스트리에 대한 관리자 사용자 비활성화
```azurecli
az acr update -n myRegistry1 --admin-enabled false
```

## <a name="list-images-and-tags"></a>이미지 및 태그 나열
사용 하 여 hello `az acr` CLI 명령을 tooquery hello 이미지와 저장소의 태그입니다.

> [!NOTE]
> 현재 컨테이너 레지스트리 hello 지원 하지 않는 `docker search` 이미지 및 태그에 대 한 명령 tooquery 합니다.


### <a name="list-repositories"></a>리포지토리 나열
hello 다음 예에서는 나열 JSON (JavaScript Object Notation) 형식의 레지스트리에 hello 저장소:

```azurecli
az acr repository list -n myRegistry1 -o json
```

### <a name="list-tags"></a>태그 나열
hello 다음 예에서는 나열 hello hello 태그 **샘플/nginx** JSON 형식의 저장소:

```azurecli
az acr repository show-tags -n myRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a>다음 단계
* [Hello Docker CLI를 사용 하 여 첫 번째 이미지 강제](container-registry-get-started-docker-cli.md)
