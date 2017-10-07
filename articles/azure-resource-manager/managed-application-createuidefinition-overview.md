---
title: "Azure 관리 되는 응용 프로그램의 UI 정의 만드는 aaaUnderstand | Microsoft Docs"
description: "설명 방법을 Azure 관리 되는 응용 프로그램에 대 한 toocreate UI 정의"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/11/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: d53ddf438c24d5a6cb8dd53ca0b4694ab0462515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-createuidefinition"></a>CreateUiDefinition 시작
이 문서는 관리 되는 응용 프로그램을 만들기 위한 hello Azure 포털 toogenerate hello 사용자 인터페이스에서 사용 되는 한 CreateUiDefinition의 hello 핵심 개념을 소개 합니다.

```json
{
   "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
   "handler": "Microsoft.Compute.MultiVm",
   "version": "0.1.2-preview",
   "parameters": {
      "basics": [ ],
      "steps": [ ],
      "outputs": { }
   }
}
```

CreateUiDefinition에는 항상 다음 세 가지 속성이 포함됩니다. 

* 처리기
* 버전
* 매개 변수

관리 되는 응용 프로그램에 대 한 처리기는 항상 `Microsoft.Compute.MultiVm`, hello 지 원하는 최신 버전은 `0.1.2-preview`합니다.

hello 매개 변수 속성의 hello 스키마 hello hello 지정 된 처리기 및 버전 조합에 따라 달라 집니다. 관리 되는 응용 프로그램을 만들기 위해 지원 되는 hello 속성을 `basics`, `steps`, 및 `outputs`합니다. hello 기본 사항 및 단계 속성 포함 hello _요소_ 텍스트 상자 및 드롭다운 목록--같은 toobe에에서 표시 된 hello Azure 포털입니다. 속성의 사용 되는 toomap hello 출력 값은 hello 출력 hello hello Azure 리소스 관리자 배포 템플릿의 지정 된 요소 toohello 매개 변수입니다.

`$schema`를 포함하는 것이 좋지만 선택 사항입니다. 를 지정 하는 경우 hello에 대 한 값 `version` hello 내 hello 버전과 일치 해야 `$schema` URI입니다.

## <a name="basics"></a>기본 사항
hello 기본적인 단계는 항상 hello hello Azure 포털에는 CreateUiDefinition 구문 분석 하는 경우에 생성 하는 hello 마법사의 첫 번째 단계입니다. Toodisplaying hello 요소에 지정 된 또한 `basics`, hello 포털 사용자가 toochoose hello 구독, 리소스 그룹 및 hello 배포에 대 한 위치에 대 한 요소를 삽입 합니다. 일반적으로 클러스터 또는 관리자 자격 증명의 hello 이름 같은 배포 전체 매개 변수를 쿼리 하는 요소는이 단계에서는 이동 해야 합니다.

요소의 동작은 hello 사용자의 구독, 리소스 그룹 또는 위치에 따라, 해당 요소가 기본 사항에 사용할 수 없습니다. 예를 들어 **Microsoft.Compute.SizeSelector** hello 사용자의 구독 및 위치 toodetermine hello 목록이 사용 가능한 크기에 따라 달라 집니다. 따라서 **Microsoft.Compute.SizeSelector**는 steps에만 사용할 수 있습니다. 일반적으로 요소만 hello에 **Microsoft.Common** 기본 사항에 네임 스페이스를 사용할 수 있습니다. 하지만 다른 네임 스페이스의 일부 요소 (같은 **Microsoft.Compute.Credentials**) 하는 hello 사용자의 컨텍스트에 종속 되지 않은, 여전히 허용 됩니다.

## <a name="steps"></a>단계
hello 단계 속성 기본 기능을 각각 하나 이상의 요소를 포함 한 후 0 개 이상의 추가 단계 toodisplay를 포함할 수 있습니다. 역할 또는 배포 되는 hello 응용 프로그램의 계층 마다 단계를 추가 하는 것이 좋습니다. 예를 들어 클러스터에서 마스터 노드 hello에 대 한 입력에 대 한 단계와 hello 작업자 노드에 대 한 단계를 추가 합니다.

## <a name="outputs"></a>outputs
hello Azure 포털 사용 하 여 hello `outputs` 속성 toomap 요소에서 `basics` 및 `steps` hello Azure 리소스 관리자 배포 템플릿의 toohello 매개 변수입니다. 이 사전의 키 hello hello 형태의 hello 템플릿 매개 변수 및 hello 값이 참조 hello 요소에서 hello 출력 개체의 속성입니다.

## <a name="functions"></a>함수
비슷한 너무[템플릿 함수](resource-group-template-functions.md) Azure 리소스 관리자에서 (구문 및 기능 둘 다) CreateUiDefinition 요소의 입력 및 출력을 사용 하기 위한 함수도 제공으로 조건부와 같은 기능입니다.

## <a name="next-steps"></a>다음 단계
CreateUiDefinition 자체에는 간단한 스키마가 있습니다. hello 실제 깊이의 모든 지원 되는 hello 요소와 다음 문서는 hello 훌륭한 자세히 설명 하는 함수에서 나옵니다.

- [요소](managed-application-createuidefinition-elements.md)
- [함수](managed-application-createuidefinition-functions.md)

CreateUiDefinition에 대한 현재 JSON 스키마는 https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json에서 사용할 수 있습니다. 

이상 버전을 hello에 사용할 수 같은 위치입니다. Hello 대체 `0.1.2-preview` hello URL과 hello의 부분 `version` 값 하려는 toouse hello 버전 식별자를 사용 합니다. 현재 지원 되는 hello 버전 식별자는 `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, 및 `0.1.2-preview`합니다.
