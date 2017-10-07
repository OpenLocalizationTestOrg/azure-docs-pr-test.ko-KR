---
title: "리소스 정책에 대 한 aaaAzure 포털 | Microsoft Docs"
description: "설명 방법을 toouse 포털 toocreate Azure 리소스 관리자 정책 및 관리 합니다. Hello 구독 또는 리소스 그룹에 정책은 적용할 수 있습니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: tomfitz
ms.openlocfilehash: ce6413386317e532b63761a24458b85c996af4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-tooassign-and-manage-resource-policies"></a>Azure 포털 tooassign를 사용 하 고 리소스 정책 관리
Azure 포털 hello 있습니다 tooassign 리소스 tooresource 그룹 정책 및 구독을 사용합니다. hello 사용자 인터페이스를 사용 하면 쉽게 tooselect hello 정책 tooassign, 원하고 해당 정책 toocustomize hello 정책 설정에 대 한 매개 변수 값을 지정 합니다. 

tooassign hello 포털을 통해 정책으로는 hello 정책 정의 구독에 이미 있어야 합니다. 사용자 구독에는 몇 가지 기본 제공 정책 정의 하면 tooassign tooresource 그룹 또는 구독에 대해 준비 합니다. 이러한 기본 제공 정책 및 hello 포털 tooassign 정책을 사용 하 여 때 정의한 사용자 지정 정책은 표시 됩니다. 소개 toopolicies 및 toodefine 사용자 정책을 지정 하는 방법에 대 한 참조 [리소스 정책 개요](resource-manager-policy.md)합니다.

정책은 모든 자식 리소스에 의해 상속됩니다. 따라서 정책이 적용 된 tooa 리소스 그룹와 된 경우 해당 리소스 그룹에서 적용 가능한 tooall hello 리소스입니다. 이 문서에서는 hello 용어 **범위** toohello 리소스 그룹이 나 hello 정책 할당 된 구독을 참조 합니다. 

리소스(PUT 및 PATCH 작업)를 만들고 업데이트할 때 정책이 평가됩니다.

## <a name="assign-a-policy"></a>정책 할당

1. tooassign 정책 tooeither 리소스 그룹이 나 구독을 해당 리소스 그룹 또는 구독을 선택 합니다. Hello 설정에서 선택 **정책**합니다.

   ![정책 선택](./media/resource-manager-policy-portal/select-policies.png)

2. 이 범위에 대 한 정책 할당 toocreate 선택 **할당 추가**합니다.

   ![할당 추가](./media/resource-manager-policy-portal/add-assignment.png)

3. Tooassign hello 정책을 선택 합니다. 모든 정책 정의 tooyour 구독을 추가 하지 않은 경우에 할당에 사용할 수 있는 hello 기본 제공 정책을 참조 합니다. 이러한 기본 제공 정책은 여러 일반적인 시나리오에 사용할 수 있습니다.

   ![정의 선택](./media/resource-manager-policy-portal/select-definition.png)

4. 정책을 선택한 후 hello 정책에 대 한 설명 및 해당 정책에 대 한 매개 변수를 참조 합니다. 예를 들어 hello 다음 이미지에서는 hello **위치 허용** hello 사용 가능한 위치를 제한 하는 hello 정책에 필요한 매개 변수입니다.

   ![매개 변수 표시](./media/resource-manager-policy-portal/show-parameters.png)

5. Hello 사용자 인터페이스를 통해 hello 정책 매개 변수 (예: 배포에 사용할 수 있는 hello 위치)에 대 한 값 toospecify hello를 선택 합니다.

   ![매개 변수 값 선택](./media/resource-manager-policy-portal/select-parameters.png)

6. 다른 매개 변수 hello에 대 한 값을 제공 합니다. hello 범위 hello 블레이드 hello 정책 할당을 시작할 때 선택에 따라 자동으로 할당 됩니다. 완료되면 **확인** 을 선택합니다.

   ![매개 변수 정의](./media/resource-manager-policy-portal/define-parameters.png)

  Hello 정책 할당 toohello 범위를 지정 합니다.

## <a name="view-policy-assignments"></a>정책 할당 보기

정책을 할당 한 후에 표시 해당 범위에 대 한 정책 hello 목록입니다. hello **세부 정보** 탭 hello 정책 할당의 요약 정보를 표시 합니다.

![세부 정보 표시](./media/resource-manager-policy-portal/show-details.png)

hello **할당 규칙** 탭 hello 정책 정의 대 한 JSON hello를 표시 합니다.

![할당 규칙 표시](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a>기존 정책 할당 변경

클라이언트는 정책을 toochange 선택 **할당을 편집** 또는 **삭제**

![할당 편집 또는 삭제](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a>사용자 지정 정책 할당

구독에 사용자 지정 정책을 정의한 경우 해당 정책을 hello 포털을 통해 할당 수 있습니다. 이러한 정책은 앞에 **[Custom]**이 표시됩니다.

![사용자 지정 정책](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a>다음 단계
* toolearn 정책을 정의 하기 위한 hello JSON 구문에 대 한 참조 [리소스 정책 개요](resource-manager-policy.md)합니다.
* 기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.
* 에 hello 정책 스키마를 게시 [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json)합니다. 

