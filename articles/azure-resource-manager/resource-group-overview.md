---
title: "리소스 관리자 개요 aaaAzure | Microsoft Docs"
description: "설명 방법을 toouse Azure 리소스 관리자 배포, 관리 및 Azure에서 리소스 액세스 제어에 대 한 합니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 76df7de1-1d3b-436e-9b44-e1b3766b3961
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: tomfitz
ms.openlocfilehash: a44fccd96d722c006224145d71cc44292255debf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-overview"></a>Azure Resource Manager 개요
일반적으로 많은 구성 요소가 – 미정 가상 컴퓨터, 저장소 계정 및 가상 네트워크 또는 웹 응용 프로그램, 데이터베이스, 데이터베이스 서버 및 타사 서비스의 응용 프로그램에 대 한 hello 인프라 구성 됩니다. 이러한 구성 요소를 별도 엔터티로 표시하지 않으면, 대신 관련된 단일 엔터티의 상호 종속적으로 부분으로 표시됩니다. Toodeploy, 관리, 한 그룹으로 보고 모니터링 합니다. Azure 리소스 관리자 그룹으로 toowork 솔루션에 hello 리소스를 사용 합니다. 배포 지정, 업데이트 또는 단일, 통합 작업에서 솔루션에 대 한 모든 hello 리소스를 삭제 합니다. 배포용 템플릿을 사용하고 이 템플릿을 테스트, 스테이징 및 프로덕션과 같은 여러 환경에서 사용할 수 있습니다. 리소스 관리자는 감사 보안을 제공 하 고 리소스 배포 된 후 관리 기능 toohelp 태그를 지정 합니다. 

## <a name="terminology"></a>용어
새 tooAzure 리소스 관리자 인 경우에 다음과 같은 익숙한 수 없는 몇 가지 용어입니다.

* **리소스** - Azure를 통해 사용할 수 있는 관리 가능한 항목입니다. 몇 가지 일반적인 리소스는 가상 컴퓨터, 저장소 계정, 웹앱, 데이터베이스 및 가상 네트워크이지만 더 많은 종류가 있습니다.
* **리소스 그룹** - Azure 솔루션에 관련된 리소스를 보유하는 컨테이너입니다. 리소스 그룹 hello hello 솔루션에 대 한 모든 hello 리소스 또는 그룹으로 toomanage 되도록 하는 리소스에만 포함할 수 있습니다. 원하는 tooallocate 리소스를 결정 하는 요소 hello 조직에 가장 적합 한 기반으로 tooresource 그룹입니다. [리소스 그룹](#resource-groups)을 참조하세요.
* **리소스 공급자** -hello 리소스를 제공 하는 서비스 배포 및 관리할 수 리소스 관리자를 통해 합니다. 각 리소스 공급자는 배포 된 hello 리소스를 사용 하기 위한 작업을 제공 합니다. 몇 가지 일반 리소스 공급자는 Microsoft.Compute hello 가상 컴퓨터 리소스를 제공 하는, Microsoft.Storage hello 저장소 계정 리소스를 제공 하는 및 Microsoft.Web이 관련된 tooweb 앱 리소스를 제공 합니다. [리소스 공급자](#resource-providers)를 참조하세요.
* **리소스 관리자 템플릿** -하나 이상의 리소스 toodeploy tooa 리소스 그룹을 정의 하는 개체 JSON (JavaScript Notation) 파일입니다. 또한 배포 된 hello 리소스 간의 종속성 hello를 정의합니다. hello 템플릿을 일관 되 고 반복 해 서 사용 되는 toodeploy hello 리소스 수 있습니다. [템플릿 배포](#template-deployment)를 참조하세요.
* **선언적 구문** -수 있는 구문 상태 "같습니다. 의도 I toocreate" toowrite hello 일련의 명령을 toocreate 프로그래밍 하지 않고도 것입니다. hello 리소스 관리자 템플릿은 선언문의 예입니다. Hello 파일 인프라 toodeploy tooAzure hello에 대 한 hello 속성을 정의합니다. 

## <a name="hello-benefits-of-using-resource-manager"></a>리소스 관리자를 사용 하 여 hello 이점
리소스 관리자는 다음과 같은 여러 이점이 있습니다.

* 배포, 관리 하 고 이러한 리소스를 개별적으로 처리 하지 않고 그룹에서 솔루션에 대 한 모든 hello 리소스를 모니터링할 수 있습니다.
* 반복 해 서 hello 개발 수명 주기 전체에서 솔루션을 배포할 수 있으며 것을 확신할 리소스 일관 된 상태로 배포 됩니다.
* 스크립트가 아닌 선언적 템플릿을 통해 인프라를 관리할 수 있습니다.
* Hello 올바른 순서로 배포 되므로 리소스 간의 종속성을 hello를 정의할 수 있습니다.
* 역할 기반 액세스 제어 (RBAC) hello 관리 플랫폼에 고유 하 게 통합 되어 있으므로 리소스 그룹에 대 한 액세스 제어 tooall 서비스를 적용할 수 있습니다.
* 태그를 적용할 수 tooresources toologically 구독에서 모든 hello 리소스를 구성 합니다.
* 리소스 그룹에 대 한 비용을 확인 하 여 조직의 요금 청구를 명확 하 게 같은 태그를 hello 공유 합니다.  

리소스 관리자는 새로운 방식으로 toodeploy 제공 하 고 솔루션을 관리 합니다. 사용 하는 경우 이전 버전의 배포 모델을 hello 및 toolearn hello 변경에 대 한 원하는, 참조 [이해 리소스 관리자 배포 및 클래식 배포](resource-manager-deployment-model.md)합니다.

## <a name="consistent-management-layer"></a>일관적인 관리 계층
리소스 관리자는 Azure PowerShell, Azure CLI, Azure 포털, REST API 및 개발 도구를 통해 수행 하는 hello 작업에 대 한 일관 된 관리 계층을 제공 합니다. Hello 도구는 모두 작업의 공통 집합을 사용합니다. 가장 잘 작동 하 고 활용할 수 같은 의미로 혼동 하지 않고 있는 hello 도구를 사용 합니다. 

hello 다음 이미지와 모든 hello 도구와 상호 작용 하는 방법 hello 같은 Azure 리소스 관리자 API입니다. hello API toohello 리소스 관리자 서비스 인증 및 hello 요청 권한 부여 요청을 전달 합니다. 리소스 관리자는 다음 hello 요청 toohello 적절 한 리소스 공급자를 라우팅합니다.

![리소스 관리자 요청 모델](./media/resource-group-overview/consistent-management-layer.png)

## <a name="guidance"></a>지침
hello 다음 제안 사항을 쉽게 활용할 리소스 관리자의 솔루션을 작업할 때.

1. 정의 하 고 대신 명령적 명령을 통해 hello 선언적 구문에서 리소스 관리자 템플릿을 통해 인프라를 배포 합니다.
2. Hello 서식 파일의 모든 배포 및 구성 단계를 정의 합니다. 솔루션을 설정하기 위해 수동 단계가 없어야 합니다.
3. 명령적 명령을 toomanage toostart 같은 사용자 리소스를 실행 하거나 응용 프로그램 또는 컴퓨터를 중지 합니다.
4. Hello로 리소스를 정렬 된 리소스 그룹에에서 동일한 주기 합니다. 리소스의 모든 다른 구성에 태그를 사용합니다.

템플릿에 대한 권장 사항은 [Azure Resource Manager 템플릿 생성 모범 사례](resource-manager-template-best-practices.md)를 참조하세요.

기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.

## <a name="resource-groups"></a>리소스 그룹
리소스 그룹을 정의할 때 몇 가지 중요 한 요소 tooconsider가 있습니다.

1. 그룹의 모든 hello 리소스를 공유 해야 같은 수명 주기 hello 합니다. 리소스를 함께 배포, 업데이트, 삭제합니다. 데이터베이스 서버와 같은 하나의 리소스, 다양 한 배포 주기 중에 tooexist이 필요한 다른 리소스 그룹에 있어야 합니다.
2. 각 리소스는 하나의 리소스 그룹에만 있을 수 있습니다.
3. 추가 하거나 언제 든 지 리소스 tooa 리소스 그룹을 제거할 수 있습니다.
4. 특정 리소스 그룹 tooanother 그룹에서 리소스를 이동할 수 있습니다. 자세한 내용은 참조 [리소스 toonew 리소스 그룹이 나 구독 이동](resource-group-move-resources.md)합니다.
5. 리소스 그룹을 다른 지역에 상주하는 리소스를 포함할 수 있습니다.
6. 리소스 그룹 수 있습니다. 관리 작업을 위한 tooscope 액세스 제어를 사용 합니다.
7. 리소스는 다른 리소스 그룹의 리소스와 상호 작용할 수 있습니다. Hello 두 리소스 관련 되어 있지만 공유 하지 않는 경우이 상호 작용은 일반적인 hello 같은 수명 주기 (예를 들어, 웹 앱 tooa 데이터베이스 연결).

리소스 그룹을 만들 때 해당 리소스 그룹 위치 tooprovide가 필요 합니다. 리소스 그룹에 위치가 필요한 이유는 무엇인지 궁금할 수 있습니다. And hello 리소스 hello 리소스 그룹 보다 서로 다른 위치에 넣을 수 있는 경우 이유 hello 리소스 그룹 위치는 상관이 전혀 "? 리소스 그룹 hello hello 리소스에 대 한 메타 데이터를 저장합니다. 따라서 hello 리소스 그룹에 대 한 위치를 지정 하면 지정 하는 메타 데이터가 저장 됩니다. 규정 준수 상의 이유로 tooensure 할 수 있습니다는 데이터가 저장 되는 특정 지역에 있습니다.

## <a name="resource-providers"></a>리소스 공급자
각 리소스 공급자는 Azure 서비스를 사용하는 일련의 리소스 및 작업을 제공합니다. 예를 들어 toostore 키와 암호를 원할 경우 사용 하 여 작업할 hello **Microsoft.KeyVault** 리소스 공급자입니다. 이 리소스 공급자 라는 리소스 형식을 제공 **자격 증명 모음** hello 주요 자격 증명 모음을 만들기 위한 합니다. 

리소스 종류의 hello 이름은 hello 형식을: **{리소스 공급자} / {리소스 유형의}**합니다. 예를 들어 hello 주요 자격 증명 모음 형식이 **Microsoft.KeyVault/vaults**합니다.

리소스 배포을 시작 하기 전에 hello 사용 가능한 리소스 공급자의 이해할 해야 있습니다. 리소스의 hello 이름을 리소스를 정의 하는 공급자 및 리소스 수를 알 toodeploy tooAzure 원하는 합니다. 또한 tooknow hello에 대 한 유효한 위치가 및 API 버전에 필요한 각 리소스 유형에 합니다. 자세한 내용은 [리소스 공급자 및 형식](resource-manager-supported-services.md)을 참조하세요.

## <a name="template-deployment"></a>템플릿 배포
리소스 관리자와 hello 인프라 및 Azure 솔루션의 구성을 정의 하는 JSON 형식으로 서식 파일을 만들 수 있습니다. 템플릿을 사용하여 수명 주기 내내 솔루션을 반복적으로 배포하고 안심하고 일관된 상태로 리소스를 배포할 수 있습니다. Hello 포털에서 솔루션을 만들 때 hello 솔루션 배포 템플릿을 자동으로 포함 됩니다. 없는 toocreate 프로그램 템플릿을 처음부터 솔루션에 대 한 hello 템플릿으로 시작 하 고 toomeet 사용자 지정할 수 있으므로 필요 합니다. Hello hello 리소스 그룹의 현재 상태 내보내기 하거나 특정 배포에 사용 되는 hello 템플릿을 검토 하 여 기존 리소스 그룹에 대 한 서식 파일을 검색할 수 있습니다. Hello 보기 [서식 파일을 내보낸](resource-manager-export-template.md) hello 템플릿 구문에 대 한 유용한 방법은 toolearn 됩니다.

toolearn hello 템플릿과 작성 하는 방법의 hello 형식에 대 한 참조 [첫 번째 Azure 리소스 관리자 서식 파일 만들기](resource-manager-create-first-template.md)합니다. tooview hello 리소스 형식에 대 한 JSON 구문을 참조 [Azure 리소스 관리자 템플릿을에 리소스를 정의](/azure/templates/)합니다.

Hello 템플릿 예: 다른 요청을 처리 하는 리소스 관리자 (hello 이미지에 대 한 참조 [일관적인 관리 계층](#consistent-management-layer)). Hello 템플릿을 구문 분석 하 고 hello 적절 한 리소스 공급자에 대 한 REST API 작업에 해당 구문으로 변환 합니다. 예를 들어 때 리소스 관리자 템플릿을 리소스 정의 다음 hello로 수신 합니다.

```json
"resources": [
  {
    "apiVersion": "2016-01-01",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "mystorageaccount",
    "location": "westus",
    "sku": {
      "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {
    }
  }
]
```

Hello 정의 toohello 전송 toohello Microsoft.Storage 리소스 공급자 REST API 작업으로 변환 합니다.

```HTTP
PUT
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/mystorageaccount?api-version=2016-01-01
REQUEST BODY
{
  "location": "westus",
  "properties": {
  }
  "sku": {
    "name": "Standard_LRS"
  },   
  "kind": "Storage"
}
```

서식 파일 및 리소스 그룹을 정의 하는 방법을 tooyou 및 원하는 toomanage를 완전히 솔루션입니다. 예를 들어 단일 템플릿 tooa 단일 리소스 그룹을 통해 3 계층 응용 프로그램을 배포할 수 있습니다.

![3계층 템플릿](./media/resource-group-overview/3-tier-template.png)

그러나 없는 toodefine 전체 인프라 단일 템플릿의. 종종, 이렇게 하면 의미 toodivide 배포 요구 사항을 대상으로 하는 목적에 따른 템플릿 집합에 있습니다. 서로 다른 솔루션에 이러한 템플릿을 쉽게 다시 사용할 수 있습니다. 특정 솔루션 toodeploy 모든 필요한 hello 서식 파일을 연결 하는 마스터 템플릿을 만듭니다. hello 다음 이미지 중첩 방법을 보여 줍니다 toodeploy 3 개를 포함 하는 부모 템플릿을 통해 세 가지 계층 솔루션 템플릿을 합니다.

![중첩된 계층 템플릿](./media/resource-group-overview/nested-tiers-template.png)

별도 수명 주기에 있는 사용자 계층을 계획 하는 경우 3 개 계층 tooseparate 리소스 그룹에 배포할 수 있습니다. 공지 hello 리소스가 다른 리소스 그룹에 연결 된 tooresources 될 수 있습니다.

![계층 템플릿](./media/resource-group-overview/tier-templates.png)

템플릿 설계에 대한 더 많은 제안은 [Azure Resource Manager 템플릿 설계의 패턴](best-practices-resource-manager-design-templates.md)을 참조하세요. 중첩된 템플릿에 대한 자세한 내용은 [Azure Resource Manager에서 연결된 템플릿 사용](resource-group-linked-templates.md)을 참조하세요.

Azure 리소스 관리자는 hello 올바른 순서로 tooensure 리소스가 생성 되는 종속성을 분석 합니다. 한 리소스가 다른 리소스(예: 디스크에 대한 저장소 계정을 필요로 하는 가상 컴퓨터)의 값에 의존하는 경우 종속성을 설정합니다. 자세한 정보는 [Azure 리소스 관리자 템플릿에서 종속성 정의](resource-group-define-dependencies.md)를 참조하세요.

또한 업데이트 toohello 인프라에 대 한 hello 서식 파일을 사용할 수 있습니다. 예를 들어 리소스 tooyour 솔루션을 추가한 이미 배포 된 hello 리소스에 대 한 구성 규칙을 추가 합니다. Hello 템플릿 지정 리소스가 이미 존재 하지만 해당 리소스를 만드는 Azure 리소스 관리자 새 자산을 만드는 대신 한 업데이트를 수행 합니다. Azure 리소스 관리자 업데이트 hello 기존 자산 toohello 동일 하므로 상태 새 것입니다.  

리소스 관리자는 hello 설치에 포함 되지 않은 특정 소프트웨어를 설치 하는 등 추가 작업이 필요한 경우 시나리오에 대 한 확장을 제공 합니다. DSC, Chef 또는 Puppet와 같은 구성 관리 서비스를 이미 사용 중인 경우 확장을 사용하여 해당 서비스로 작업을 계속할 수 있습니다. 가상 컴퓨터 확장에 대한 자세한 내용은 [가상 컴퓨터 확장 및 기능 정보](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요. 

마지막으로, hello 서식 파일에는 앱에 대 한 hello 소스 코드의 일부가 됩니다. Tooyour 소스 코드 리포지토리에 확인 하 고 앱이 변화 함에 따라이 업데이트할 수 있습니다. Visual Studio를 통해 hello 서식 파일을 편집할 수 있습니다.

서식 파일을 정의한 후 준비 toodeploy hello 리소스 tooAzure 됩니다. Hello 명령 toodeploy hello 리소스에 대 한 참조.

* [Resource Manager 템플릿과 Azure PowerShell로 리소스 배포](resource-group-template-deploy.md)
* [Resource Manager 템플릿과 Azure CLI로 리소스 배포](resource-group-template-deploy-cli.md)
* [Resource Manager 템플릿과 Azure Portal로 리소스 배포](resource-group-template-deploy-portal.md)
* [Resource Manager 템플릿과 Resource Manager REST API로 리소스 배포](resource-group-template-deploy-rest.md)

## <a name="tags"></a>태그들
리소스 관리자는 toocategorize 리소스 관리 또는 청구에 대 한 tooyour 요구 사항에 따라 태그를 지정할 수 있는 기능을 제공 합니다. 태그를 사용 하 여 리소스 그룹 및 리소스의 복잡 한 컬렉션 하는 경우 대부분 의미 tooyou hello에 수행 하는 hello 방식으로 이러한 자산 toovisualize 필요 합니다. 조직에서 비슷한 역할을 제공 하거나 toohello 속해 있는 리소스 태그 수는 예를 들어 같은 동일 부서입니다. 태그를 조직의 사용자가 만들 수 없는 toolater 어려울 수 있는 여러 리소스를 식별 하 고 관리 합니다. 예를 들어 특정 프로젝트에 대 한 모든 hello 리소스 toodelete를 지정할 수 있습니다. 이러한 리소스는 hello 프로젝트에 대 한 태그가 지정 되지를 하는 경우 toomanually 찾을 수 있습니다. 태그를 지정 하면 구독에 tooreduce 불필요 한 비용에 대 한는 가장 좋은 방법은 수 있습니다. 

리소스 hello에 tooreside 불필요 동일한 리소스 그룹 tooshare 태그입니다. 사용자 고유의 태그 분류 tooensure 조직의 모든 사용자가 대신 사용 하도록 일반 태그 약간 다른 태그 (예: "dept" 대신 "department")가 실수로 적용 하는 사용자가 만들 수 있습니다.

다음 예제는 hello 태그가 적용 tooa 가상 컴퓨터를 보여 줍니다.

```json
"resources": [    
  {
    "type": "Microsoft.Compute/virtualMachines",
    "apiVersion": "2015-06-15",
    "name": "SimpleWindowsVM",
    "location": "[resourceGroup().location]",
    "tags": {
        "costCenter": "Finance"
    },
    ...
  }
]
```

tooretrieve 모든 hello 리소스 태그 값으로 사용 하 여 PowerShell cmdlet을 다음 hello:

```powershell
Find-AzureRmResource -TagName costCenter -TagValue Finance
```

또는 다음 Azure CLI 2.0 명령을 hello:

```azurecli
az resource list --tag costCenter=Finance
```

Hello Azure 포털을 통해 태그가 지정 된 리소스를 볼 수 있습니다.

hello [사용 현황 보고서](../billing/billing-understand-your-bill.md) 구독에 포함 되어 태그 이름 및 값을 나타냄 toobreak 비용으로 사용할 수 있는 대 한 합니다. 태그에 대 한 자세한 내용은 참조 [를 사용 하 여 Azure 리소스를 tooorganize 태그](resource-group-using-tags.md)합니다.

## <a name="access-control"></a>Access Control
리소스 관리자 사용 하면 조직에 대 한 액세스 toospecific 동작을 가진 toocontrol 있습니다. 기본적으로 역할 기반 액세스 제어 (RBAC) hello 관리 플랫폼으로 통합 하 고 해당 액세스 제어 tooall 서비스 리소스 그룹에 적용 됩니다. 

역할 기반 액세스 제어를 사용한 작업 시에 두 가지 주요 개념과 toounderstand:

* 역할 정의 - 사용 권한 집합을 설명하고 여러 할당에 사용할 수 있습니다.
* 역할 할당 - 특정 범위(구독, 리소스 그룹 또는 리소스)에 대한 ID(사용자 또는 그룹)로 정의를 연결합니다. hello 정의 더 낮은 범위도 상속 됩니다.

사용자가 toopre 정의 플랫폼 및 리소스 관련 역할을 추가할 수 있습니다. 예를 들어 사용자가 tooview 리소스를 허용 하는 판독기를 호출 하는 hello 미리 정의 된 역할을 활용할 수 있지만 변경 하지 합니다. 이 유형의 액세스 toohello 읽기 역할을 해야 하는 조직에서 사용자를 추가 하 고 hello 역할 toohello 구독, 리소스 그룹 또는 리소스를 적용 합니다.

Azure hello를 다음 4 개의 플랫폼 역할을 제공 합니다.

1. 소유자는 액세스를 제외한 모든 것을 관리할 수 있음
2. 참여자는 액세스를 제외한 모든 것을 관리할 수 있음
3. 읽기 권한자는 모든 항목을 볼 수 있지만 변경할 수 없음
4. 사용자 액세스 관리자-tooAzure 리소스를 액세스 하는 사용자를 관리할 수 있습니다.

Azure는 몇 가지 리소스 특정 역할도 제공합니다. 몇 가지 일반적인 경우는 다음과 같습니다.

1. 가상 컴퓨터 참가자-가상 컴퓨터를 관리할 수 있지만 부여 하지 toothem, 액세스 하 고 hello 가상 네트워크 또는 저장소 계정 toowhich 연결 되어 있는 관리할 수 없습니다.
2. 네트워크 참가자-모든 네트워크 리소스를 관리할 수 있지만 toothem 액세스 권한을 부여 하지
3. 저장소 계정 참가자-저장소 계정을 관리할 수 있지만 toothem 액세스 권한을 부여 하지
4. SQL Server 참여자는 해당 보안 관련 정책을 제외한 SQL 서버 및 데이터베이스를 관리할 수 있음
5. 웹 사이트 참가자-웹 사이트를 관리할 수 있지만 연결 되어 있는 웹 계획 toowhich 하지 hello

역할 및 허용 되는 작업의 전체 목록을 hello에 대 한 참조 [RBAC: 역할에 기본 제공](../active-directory/role-based-access-built-in-roles.md)합니다. 역할 기반 Access Control에 대한 자세한 내용은 [Azure 역할 기반 Access Control](../active-directory/role-based-access-control-configure.md)를 참조하세요. 

경우에 따라 toorun 코드 또는 리소스에 액세스 하는 스크립트 싶지만 toorun 하지 않을 사용자의 자격 증명에서 합니다. 대신, toocreate hello 응용 프로그램에 대 한 사용자는 서비스 라는 id 한 hello hello 서비스 사용자에 대 한 적절 한 역할을 할당 합니다. 리소스 관리자 hello 응용 프로그램에 대 한 자격 증명 toocreate 있으며 프로그래밍 방식으로 hello 응용 프로그램을 인증 합니다. 서비스 사용자를 만드는 방법에 대해 toolearn 다음 항목 중 하나를 참조 합니다.

* [Azure PowerShell toocreate 서비스 보안 주체 tooaccess 리소스 사용](resource-group-authenticate-service-principal.md)
* [Azure CLI toocreate 서비스 보안 주체 tooaccess 리소스 사용](resource-group-authenticate-service-principal-cli.md)
* [포털 toocreate Azure Active Directory 응용 프로그램 및 서비스 사용자 리소스에 액세스할 수 있는 사용](resource-group-create-service-principal-portal.md)

명시적으로 삭제 또는 수정 하에서 중요 한 리소스 tooprevent 사용자가 잠글 수 있습니다. 자세한 내용은 [Azure 리소스 관리자를 사용하여 리소스 잠그기](resource-group-lock-resources.md)를 참조하세요.

## <a name="activity-logs"></a>활동 로그
Resource Manager는 리소스를 만들거나 수정 또는 삭제하는 모든 작업을 기록합니다. Hello 활동 로그 toofind 문제를 해결할 때 오류 또는 toomonitor 사용할 수 있습니다 조직 내에서 사용자 리소스를 수정 하는 방법입니다. toosee hello 로그 선택 **활동 로그** hello에 **설정을** 블레이드 리소스 그룹에 대 한 합니다. 사용자가 시작한 hello 작업을 포함 하 여 여러 다른 값으로 hello 로그를 필터링 할 수 있습니다. 작업 활동 로그 hello에 대 한 정보를 참조 하십시오. [활동 보기 로그 toomanage Azure 리소스](resource-group-audit.md)합니다.

## <a name="customized-policies"></a>사용자 지정된 정책
리소스 관리자 리소스 관리를 위한 사용자 지정 toocreate 정책이 있습니다. hello 유형의 만들면 정책 다양 한 시나리오를 포함할 수 있습니다. 리소스에 대한 명명 규칙을 적용하거나 배포할 수 있는 리소스의 형식 및 인스턴스를 제한하거나 리소스 종류를 호스트할 수 있는 지역을 제한할 수 있습니다. 부서에서 리소스 tooorganize 청구에 태그 값을 요구할 수 있습니다. 정책을 만들 toohelp 비용 절감 하 고 구독에서 일관성을 유지 합니다. 

JSON을 사용하여 정책을 정의하고 구독 전체 또는 리소스 그룹 내에서 해당 정책을 적용합니다. 정책 적용된 tooresource 형식이 역할 기반 액세스 제어와 다릅니다.

다음 예제는 hello에는 모든 리소스 costCenter 태그를 포함 하는 지정 하 여 태그 일관성을 보장 하는 정책을 보여 줍니다.

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

더 다양한 유형의 정책을 만들 수 있습니다. 자세한 내용은 참조 [toomanage 리소스 사용 정책 및 액세스 제어](resource-manager-policy.md)합니다.

## <a name="sdks"></a>SDK
Azure SDK는 여러 언어 및 플랫폼에 사용할 수 있습니다. 이러한 언어 구현은 각각 해당 에코 시스템 패키지 관리자 및 GitHub를 통해 사용할 수 있습니다.

다음은 오픈 소스 SDK 리포지토리입니다. 피드백, 문제 및 끌어오기 요청을 환영합니다.

* [Azure SDK for .NET](https://github.com/Azure/azure-sdk-for-net)
* [Java용 Azure 관리 라이브러리](https://github.com/Azure/azure-sdk-for-java)
* [Node.js용 Azure SDK](https://github.com/Azure/azure-sdk-for-node)
* [PHP용 Azure SDK](https://github.com/Azure/azure-sdk-for-php)
* [Python용 Azure SDK](https://github.com/Azure/azure-sdk-for-python)
* [Ruby용 Azure SDK](https://github.com/Azure/azure-sdk-for-ruby)

사용자 리소스에서 이러한 언어를 사용하는 방법에 대한 정보는 다음을 확인합니다.

* [.NET 개발자용 Azure](/dotnet/azure/?view=azure-dotnet)
* [Java 개발자용 Azure](/java/azure/)
* [Node.js 개발자용 Azure](/nodejs/azure/)
* [Python 개발자용 Azure](/python/azure/)

> [!NOTE]
> Hello SDK hello 필요한 기능을 제공 하지 않는 toohello 호출할 수도 있습니다 [Azure REST API](https://docs.microsoft.com/rest/api/resources/) 직접 합니다.
> 
> 

## <a name="next-steps"></a>다음 단계
* 템플릿으로 간단한 소개 tooworking, 참조 [기존 리소스에서 Azure 리소스 관리자 템플릿 내보내기](resource-manager-export-template.md)합니다.
* 템플릿을 만드는 자세한 연습은 [첫 번째 Azure Resource Manager 템플릿 만들기](resource-manager-create-first-template.md)를 참조하세요.
* 템플릿에서 사용 가능한 toounderstand hello 함수 참조 [템플릿 함수](resource-group-template-functions.md)
* Resource Manager로 Visual Studio를 사용하는 방법에 대한 정보는 [Visual Studio를 통해 Azure 리소스 그룹 생성 및 배포](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)를 참조하세요.

이 개요에 대한 비디오 데모는 다음과 같습니다.

>[!VIDEO https://channel9.msdn.com/Blogs/Azure-Documentation-Shorts/Azure-Resource-Manager-Overview/player]


[powershellref]: https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.2.0/azurerm.resources
