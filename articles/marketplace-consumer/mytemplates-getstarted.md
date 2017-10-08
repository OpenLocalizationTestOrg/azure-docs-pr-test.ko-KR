---
title: "aaaGet 개인 템플릿으로 시작 | Microsoft Docs"
description: "추가, 관리 및 hello Azure 포털, hello Azure CLI 또는 PowerShell을 사용 하 여 개인 서식 파일을 공유 합니다."
services: marketplace-customer
documentationcenter: 
author: VybavaRamadoss
manager: asimm
editor: 
tags: marketplace, azure-resource-manager
keywords: 
ms.assetid: 6ec20778-b578-4885-acb5-104b0e51ea1a
ms.service: marketplace
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: vybavar
ms.openlocfilehash: 1fe2c6422f62a98f7ae9ba5c61b9639d993f0bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-private-templates-on-hello-azure-portal"></a>Hello Azure 포털에 개인 템플릿으로 시작.
[Azure 리소스 관리자](../azure-resource-manager/resource-group-authoring-templates.md) 템플릿은 선언적 템플릿을 사용 하 여 배포 toodefine입니다. 솔루션에 대 한 리소스 toodeploy hello를 정의 하 고 매개 변수 및 변수를 사용 하면 다양 한 환경에 대 한 tooinput 값을 지정할 수 있습니다. hello 템플릿은 구성 JSON 및 사용할 수 있는 식의 배포에 대 한 tooconstruct 값입니다.

Hello를 새 사용할 수 있습니다 **템플릿** hello에서 기능 [Azure 포털](https://portal.azure.com) hello 함께 **Microsoft.Gallery** hello의 확장으로 리소스 공급자 [ Azure 마켓플레이스](https://azure.microsoft.com/marketplace/) tooenable 사용자 toocreate 관리 하 고 개인 라이브러리 개인 템플릿을 배포 합니다.

이 문서에서는 추가, 관리 하 고 개인 공유 **템플릿** Azure 포털 hello를 사용 하 여 합니다.

## <a name="guidance"></a>지침
hello 다음 제안 사항을 할 완전히 활용 **템플릿** 솔루션을 작업할 때:

* **템플릿** 은 Resource Manager 템플릿 및 추가 메타데이터를 포함하는 캡슐화된 리소스입니다. Hello Marketplace에서에서 tooan 항목 매우 비슷하게 작동합니다. 주요 차이점 hello 것과 반대로 toohello 공용 마켓플레이스 항목으로 비공개 항목 된다는 점입니다.
* hello **템플릿** 라이브러리 배포 toocustomize 해야 하는 사용자에 적합 합니다.
* **템플릿** 은 Azure 내에서 간단한 리포지토리가 필요한 사용자에 대해 제대로 작동합니다.
* 기존 Resource Manager 템플릿으로 시작합니다. [github](https://github.com/Azure/azure-quickstart-templates)에서 템플릿을 찾거나 기존 리소스 그룹에서 [템플릿을 내보냅니다](../azure-resource-manager/resource-manager-export-template.md).
* **템플릿** 동률된 toohello 사용자에 게 게시 됩니다. hello 게시자 이름이 tooit 읽기 권한을 가진 tooeveryone 표시 됩니다.
* **템플릿** 은 Resource Manager 리소스이며 게시된 후에는 이름을 바꿀 수 없습니다.

## <a name="add-a-template-resource"></a>템플릿 리소스 추가
두 가지 방법으로 toocreate는 **템플릿** hello Azure 포털에서에서 리소스입니다.

### <a name="method-1--create-a-new-template-resource-from-a-running-resource-group"></a>방법 1: 실행 중인 리소스 그룹에서 새 템플릿 리소스 만들기
1. Tooan hello Azure 포털에서 기존 리소스 그룹을 이동 합니다. **설정**에서 **템플릿 내보내기**를 선택합니다.
2. Hello를 사용 하 여 hello 리소스 관리자 템플릿을 내보낸 후 **템플릿 저장** 단추 toosave 것 toohello **템플릿** 저장소입니다. 템플릿 내보내기에 대한 전체 세부 정보는 [여기](../azure-resource-manager/resource-manager-export-template.md)에서 확인하세요.
   <br /><br />
   ![리소스 그룹 내보내기](media/rg-export-portal1.PNG)  <br />
3. 선택 hello **tooTemplate 저장** 명령 단추입니다.
   <br /><br />
4. Hello 다음 정보를 입력 합니다.
   
   * 이름-hello 템플릿 개체의 이름 (참고: Azure 리소스 관리자 기반 이름입니다. 모든 명명 제한 사항을 적용하고 만든 후에는 변경할 수 없습니다).
   * 설명 – hello 서식 파일에 대 한 요약입니다.
     
     ![템플릿 저장](media/save-template-portal1.PNG)  <br />
5. **Save**를 클릭합니다.
   
   > [!NOTE]
   > hello 내보내기 템플릿 블레이드 알림을 표시 hello 리소스 관리자에서 내보낸된 템플릿에 오류가 있지만 수 toosave은 여전히이 리소스 관리자 템플릿 toohello 템플릿. 확인 하 고 재배포 hello 리소스 관리자 템플릿 내보내기 전에 모든 리소스 관리자 템플릿 문제 해결을 확인 합니다.
   > 
   > 

### <a name="method-2--add-a-new-template-resource-from-browse"></a>방법 2: 찾아보기에서 새 템플릿 리소스 추가
새 추가할 수 **템플릿** 안녕하세요 + 추가 명령 단추를 사용 하 여 처음부터 **찾아보기 > 템플릿**합니다. 이름, 설명 및 리소스 관리자 템플릿 JSON hello tooprovide 필요 합니다.

![템플릿 추가](media/add-template-portal1.PNG)  <br />

> [!NOTE]
> Microsoft.Gallery는 테넌트 기반 Azure 리소스 공급자입니다. hello 템플릿 리소스는 동 점된 toohello 사용자 만든 사람입니다. 동 점된 tooany 특정 구독 하지 않습니다. 구독 toobe 서식 파일을 배포 하는 경우에 선택 해야 합니다.
> 
> 

## <a name="view-template-resources"></a>템플릿 리소스 보기
모든 **템플릿** 에서 사용할 수 있는 tooyou를 볼 수 있습니다 **찾아보기 > 템플릿**합니다. 여기에는 만든 **템플릿** 과 다양한 수준의 권한으로 공유한 템플릿이 포함됩니다. Hello에 대 한 자세한 내용은 [액세스 제어](#access-control-for-a-tenant-resource-provider) 아래 섹션.

![템플릿 보기](media/view-template-portal1.PNG)  <br />

hello 세부 정보를 볼 수는 **템플릿** hello 목록에서 항목을 클릭 하 여 합니다.

![템플릿 보기](media/view-template-portal2c.png)  <br />

## <a name="edit-a-template-resource"></a>템플릿 리소스 편집
에 대 한 hello 편집 흐름을 시작할 수는 **템플릿** hello 항목 hello 브라우즈 목록에서 마우스 오른쪽 단추로 클릭 하 여 또는 hello 편집 명령 단추를 선택 하 여 합니다.

![템플릿 편집](media/edit-template-portal1a.PNG)  <br />

Hello 설명 또는 리소스 관리자 템플릿 텍스트를 편집할 수 있습니다. 리소스 관리자 리소스 이름 이므로 이름 hello를 편집할 수 없습니다. JSON hello 리소스 관리자 템플릿을 편집할 때 tooensure 것은 유효한 JSON을 확인 합니다. 선택 **확인** 차례로 **저장** toosave 서식 파일에 업데이트 합니다.

![템플릿 편집](media/edit-template-portal2a.PNG)  <br />

한 번 hello **템플릿** 저장 된 알림이 표시 됩니다.

![템플릿 편집](media/edit-template-portal3b.png)  <br />

## <a name="deploy-a-template-resource"></a>템플릿 리소스 배포
**읽기** 권한이 있는 **템플릿**을 배포할 수 있습니다. hello 배포 흐름 hello 표준 Azure 템플릿 배포 블레이드를 시작합니다. Hello 배포와 함께 리소스 관리자 템플릿 매개 변수 tooproceed hello에 대 한 hello 값을 입력 합니다.

![템플릿 배포](media/deploy-template-portal1b.png)  <br />

## <a name="share-a-template-resource"></a>템플릿 리소스 공유
**템플릿** 리소스를 동료와 공유할 수 있습니다. 공유 비슷하게 너무[Azure에서 모든 리소스에 대 한 역할 할당](../active-directory/role-based-access-control-configure.md)합니다. hello **템플릿** 소유자 권한을 tooother 사용자에 게 제공 상호 작용할 수 있는 템플릿 리소스입니다. hello 개인 또는 그룹 hello 공유 하는 사람의 **템플릿** 됩니다 수 toosee hello 리소스 관리자 템플릿 및 해당 갤러리 속성입니다.

### <a name="access-control-for-hello-microsoftgallery-resources"></a>Hello Microsoft.Gallery 리소스에 대 한 액세스 제어
| 역할 | 권한 |
| --- | --- |
| 소유자 |공유를 포함 하 여 hello 템플릿 리소스에 대 한 모든 권한을 허용합니다 |
| 읽기 권한자 |Hello 템플릿 리소스에서 읽기 및 Execute(Deploy) 허용 |
| 참여자 |Hello 템플릿 리소스에 대 한 권한을 편집 및 삭제를 허용합니다. 사용자는 다른 사용자와 hello 서식 파일을 공유할 수 없습니다. |

선택 **공유** 마우스 오른쪽 단추로 클릭 하 여 또는 특정 항목의 hello 보기 블레이드에서 hello 찾아보기 항목에 있습니다. 그러면 공유 환경이 시작됩니다.

![템플릿 공유](media/share-template-portal1a.png)  <br />

 이제 역할과 사용자 또는 그룹 tooprovide 액세스 tooa 특정를 선택할 수 있습니다 **템플릿**합니다. hello 사용 가능한 역할 소유자, 독자 및 참가자 됩니다. Hello에 대 한 자세한 내용은 [액세스 제어](#access-control-for-a-tenant-resource-provider) 위의 섹션.

![템플릿 공유](media/share-template-portal2b.png)  <br />

![템플릿 공유](media/share-template-portal3b.png)  <br />

**선택** 및 **확인**을 클릭합니다. Hello 사용자 또는 그룹 표시 toohello 리소스를 추가 합니다.

![템플릿 공유](media/share-template-portal4b.png)  <br />

> [!NOTE]
> 서식 파일만 공유할 수는 사용자 및 그룹 hello 동일한 Azure Active Directory 테 넌 트입니다. 테 넌 트에 있지 않은 전자 메일 주소가 있는 서식 파일을 공유 하는 경우 요청 hello 사용자 toojoin hello 테 넌 트에 게스트로 초대 전송 됩니다.
> 
> 

## <a name="next-steps"></a>다음 단계
* 리소스 관리자 템플릿을 만드는 방법에 대해 toolearn 참조 [템플릿 작성](../azure-resource-manager/resource-group-authoring-templates.md)
* 리소스 관리자 서식 파일에서 사용 가능한 toounderstand hello 함수 참조 [템플릿 함수](../azure-resource-manager/resource-group-template-functions.md)
* 템플릿 설계에 대한 지침은 [Azure 리소스 관리자 템플릿 설계의 모범 사례](../azure-resource-manager/best-practices-resource-manager-design-templates.md)

