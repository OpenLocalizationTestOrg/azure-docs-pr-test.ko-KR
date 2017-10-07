---
title: "Azure 서식 파일에 자식 리소스 aaaDefine | Microsoft Docs"
description: "리소스 종류 및 Azure 리소스 관리자 템플릿에 자식 리소스에 대 한 이름을 tooset hello 하는 방법을 보여 줍니다."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: tomfitz
ms.openlocfilehash: c502c589100d7ae864d7fb01b5ba10ddfaf92592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a>Resource Manager 템플릿에서 자식 리소스의 이름 및 유형 설정
서식 파일을 만들 때 자주 tooinclude 자식 리소스 관련된 tooa 부모 리소스에 필요 합니다. 예를 들어 템플릿에 SQL Server 및 데이터베이스가 포함될 수 있습니다. hello SQL 서버 hello 부모 리소스와 hello 데이터베이스가 hello 자식 리소스가 있습니다. 

hello hello 자식 리소스 종류의 형식은 다음과 같습니다.`{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`

hello hello 자식 리소스 이름의 형식은 다음과 같습니다.`{parent-resource-name}/{child-resource-name}`

그러나 hello 형식 및 서식 파일의 이름을 따라 다르게 hello 부모 리소스 내에 중첩 되어 있는지 여부 또는 자체적으로 hello 최상위 수준에서 지정 합니다. 이 항목에서는 두 toohandle 접근 하는 방법을 보여 줍니다.

정규화 된 참조 tooa 리소스를 생성할 때는 hello 순서 toocombine hello 형식에서 세그먼트 및 이름이 hello 2의 연결을 단순히 않습니다.  대신, hello 네임 스페이스 후의 시퀀스를 사용 하 여 *유형/이름이* 구체적인 toomost 특정 쌍:

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

예:

`Microsoft.Compute/virtualMachines/myVM/extensions/myExt`는 올바릅니다. `Microsoft.Compute/virtualMachines/extensions/myVM/myExt`는 올바르지 않습니다.

## <a name="nested-child-resource"></a>중첩된 자식 리소스
hello 가장 쉬운 방법은 toodefine 자식 리소스는 toonest hello 부모 리소스 내에서. hello 다음 예제에서는 SQL server에서 내에 중첩 된 SQL 데이터베이스

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  ...
  "resources": [
    {
      "name": "exampledatabase",
      "type": "databases",
      "apiVersion": "2014-04-01",
      ...
    }
  ]
}
```

Hello 자식 리소스에 대 한 hello 유형이 설정 되어 너무`databases` 하지만 해당 전체 리소스 형식이 `Microsoft.Sql/servers/databases`합니다. 그러지 않으면 `Microsoft.Sql/servers/` hello 부모 리소스 종류에서 가정 합니다. hello 자식 리소스 이름이 너무 설정`exampledatabase` hello 전체 이름 hello 부모 이름이 포함 됩니다. 그러지 않으면 `exampleserver` hello 부모 리소스에서 가정 합니다.

## <a name="top-level-child-resource"></a>최상위 자식 리소스
Hello 최상위 수준 hello 자식 리소스를 정의할 수 있습니다. Hello 부모 리소스 hello에 배포 되지 않은 경우이 방법을 사용할 수 있습니다 동일한 템플릿이나 toouse를 원하는 경우 `copy` toocreate 여러 자식 리소스입니다. 이 방법에서는 hello 전체 리소스 종류를 제공 하 고 hello 자식 리소스 이름에 hello 부모 리소스 이름을 포함 해야 합니다.

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  "resources": [ 
  ],
  ...
},
{
  "name": "exampleserver/exampledatabase",
  "type": "Microsoft.Sql/servers/databases",
  "apiVersion": "2014-04-01",
  ...
}
```

hello 데이터베이스는 hello hello 서식 파일에 동일한 수준에 정의 된 경우에 자식 리소스 toohello 서버.

## <a name="next-steps"></a>다음 단계
* 방법에 대 한 권장 사항에 대 한 toocreate 템플릿 참조 [Azure 리소스 관리자 템플릿 만들기에 대 한 유용한](resource-manager-template-best-practices.md)합니다.
* 여러 자식 리소스를 만드는 예제는 [Azure Resource Manager 템플릿에서 리소스의 여러 인스턴스 배포](resource-group-create-multiple.md)를 참조하세요.
