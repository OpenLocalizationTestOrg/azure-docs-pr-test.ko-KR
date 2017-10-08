---
title: "웹 서비스 aaaHow toodeploy toomultiple 영역 | Microsoft Docs"
description: "단계 toodeploy (복사) 새 웹 서비스 tooother 영역입니다."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: cgronlun
ms.assetid: 36c60411-f2db-4ee2-9b66-b1f1d77a8f44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 21fcdb96f118c60ed98b60b1b2df833766c7c8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-web-service-toomultiple-regions"></a>어떻게 toodeploy 웹 서비스 toomultiple 영역
hello 새 Azure 웹 서비스를 사용 하면 tooeasily 여러 구독 또는 작업 영역 필요 없이 웹 서비스 toomultiple 영역을 배포 합니다. 

가격 책정은 지역별로 고유 하므로는 hello 웹 서비스를 배포할 각 지역에 대 한 청구 계획을 정의 해야 합니다.

## <a name="toocreate-a-plan-in-another-region"></a>toocreate 다른 지역에 계획
1. [Microsoft Azure 기계 학습 웹 서비스](https://services.azureml.net/)에 로그인합니다.
2. Hello 클릭 **계획** 메뉴 옵션입니다.
3. 보기 페이지를 덮어쓰며 hello 계획, 클릭 **새로**합니다.
4. Hello에서 **구독** 드롭다운에서 hello 새 계획 상주할 선택 hello 구독 합니다.
5. Hello에서 **지역** 드롭다운에서 hello 새 계획에 대 한 지역 선택 합니다. hello 선택한 영역에 대 한 계획 옵션 hello hello에 표시 됩니다 **계획 옵션** hello 페이지의 섹션입니다.
6. Hello에서 **리소스 그룹** 드롭다운을 선택 hello 계획에 대 한 리소스를 그룹화 합니다. 리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.
7. **계획 이름** hello 계획의 hello 이름 형식입니다.
8. 아래 **계획 옵션**, hello 새 계획에 대 한 hello 청구 수준을 클릭 합니다.
9. **만들기**를 클릭합니다.

## <a name="deploying-hello-web-service-tooanother-region"></a>Hello 웹 서비스 tooanother 영역 배포
1. Hello 클릭 **웹 서비스** 메뉴 옵션입니다.
2. Hello tooa 새 영역을 배포 하는 웹 서비스를 선택 합니다.
3. **복사**를 클릭합니다.
4. **웹 서비스 이름이**를 hello 웹 서비스에 대 한 새 이름을 입력 합니다.
5. **웹 서비스 기술**를 hello 웹 서비스에 대 한 설명을 입력 합니다.
6. Hello에서 **구독** 드롭다운을 새 웹 서비스는 hello에 상주할 선택 hello 구독 합니다.
7. Hello에서 **리소스 그룹** 드롭다운을 선택 hello 웹 서비스에 대 한 리소스를 그룹화 합니다. 리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.
8. Hello에서 **지역** 드롭다운에서 toodeploy hello 웹 서비스에서 선택 hello 영역입니다.
9. Hello에서 **저장소 계정** 드롭다운을 선택는 toostore hello에서 저장소 계정을 웹 서비스입니다.
10. Hello에서 **가격 계획** 드롭다운에서 8 단계에서 선택한 hello 지역에 대 한 계획을 선택 합니다.
11. **복사**를 클릭합니다.

