---
title: "aaaAzure 관리 응용 프로그램 마켓플레이스 hello에 | Microsoft Docs"
description: "Azure에 설명 hello 마켓플레이스를 통해 사용할 수 있는 응용 프로그램을 관리 합니다."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b3cdf3f1fccdd47db699e4892ae8bce35118bfd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-in-hello-marketplace"></a>Azure는 마켓플레이스 hello에 대 한 응용 프로그램 관리

 Msp, Isv 및 시스템 통합자 (SIs) צ ְ ײ Azure 응용 프로그램 toooffer 솔루션 tooall Azure 마켓플레이스 고객을 관리 합니다. 이러한 솔루션 hello 유지 관리 및 서비스 고객에 대 한 오버 헤드가 줄입니다. 인프라 및 hello 마켓플레이스를 통해 소프트웨어 게시자 판매할 수 있습니다. 서비스 및 운영 지원 toomanaged 응용 프로그램에 연결할 수 있습니다. 자세한 내용은 [관리되는 응용 프로그램 개요](managed-application-overview.md)를 참조하세요.

MSP, ISV, 또는 SI 수는 응용 프로그램 toohello 마켓플레이스에 게시 방법과 toocustomers 광범위 하 게 사용할 수 있도록이 문서에 설명 합니다.

## <a name="prerequisites-for-publishing-a-managed-application"></a>관리되는 응용 프로그램을 게시하기 위한 필수 조건

마켓플레이스 hello에 toolisting 필수 구성 요소:

* 기술

    *  Hello 기본 구조 및 Azure 리소스 관리자 템플릿 구문에 대 한 정보를 참조 하십시오. [Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다.
    *  tooview 전체 서식 파일 솔루션 비교 참조 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/en-us/documentation/templates/) 또는 hello [퀵 스타트 템플릿 리포지토리](https://github.com/azure/azure-quickstart-templates)합니다.
    *  Toocreate hello 마켓플레이스를 통해 응용 프로그램을 배포 하는 고객에 대 한 인터페이스를 hello 하는 방법에 대 한 정보를 참조 하십시오. [사용자 인터페이스 정의 파일을 만들](managed-application-createuidefinition-overview.md)합니다.

* 비기술(비즈니스 요구 사항)

    *   회사 또는 해당 대리점 판매 hello Marketplace에서 지원 되는 위치는 국가에 있어야 합니다.
    *   Hello Marketplace에서 지 원하는 청구 모델에 호환 되는 방식으로 제품을 받아야 합니다.
    *   본인이 기술 지원을 사용할 수 있는 toocustomers 상업적으로 적절 한 방식으로 확인 해야 합니다. hello 지원 될 무료 이며 유료, 하거나 커뮤니티를 통해 지원 합니다.
    *   소프트웨어 및 타사 소프트웨어 종속성에 대해 사용 허가를 받을 책임이 있습니다.
    *   제품 toobe에 대 한 기준에 맞는 콘텐츠 및에 표시 된 hello 마켓플레이스 hello에 Azure 포털을 제공 해야 합니다.
    *   Toohello hello Azure 마켓플레이스 참여 정책 및 게시자 계약 약관을 동의 해야 합니다.
    *   Microsoft Azure 인증 프로그램 계약, hello 사용 약관 및 Microsoft 개인정보취급방침 toocomply를 동의 해야 합니다.

## <a name="create-a-new-azure-application-offer"></a>새 Azure 응용 프로그램 제품 만들기

준비 toocreate 후 hello 필수 구성 요소를 충족 하는 관리 되는 응용 프로그램 제공 합니다. 제품 및 SKU를 간략히 살펴보겠습니다.

### <a name="offer"></a>제안

관리 되는 응용 프로그램에 대 한 hello 제공 tooa 클래스는 게시자에서 제공 하는 제품의 해당 합니다. 새로운 유형의 솔루션/응용 프로그램 원하는 toomake hello 시장에서에서 사용할 수 있는 경우 새 제안을으로 설정할 수 있습니다. 제품은 SKU의 컬렉션입니다. 모든 제안 hello Marketplace의에서 고유 엔터티로 표시 됩니다.

### <a name="sku"></a>SKU

SKU는 hello 가장 작은 있는 구입 가능한 단위 제안의입니다. Hello 내 SKU를 사용할 수 있습니다 간에 동일한 제품 클래스 (제안) toodifferentiate:

* 제공되는 다양한 기능.
* Hello 제공 관리 또는 관리 되지 않는 여부
* 지원되는 요금 청구 모델.

SKU는 hello Marketplace에서에서 hello 부모 제공 아래에 나타납니다. Hello Azure 포털에에서 있는 구입 가능한 자체 엔터티로 표시 됩니다.

### <a name="set-up-an-offer"></a>제품 설정

1. Toohello 로그인 [클라우드 파트너 포털](https://cloudpartner.azure.com/)합니다.

2. Hello hello 왼쪽의 탐색 창에서 선택 **+ 새 제안을** > **Azure 응용 프로그램**합니다.

    ![새 제품](./media/managed-application-author-marketplace/newOffer.png)

3. Hello에 남아 있는 hello에 나타나는 hello 양식을 작성 **편집기** 보기. 필수 필드는 빨간색 별표(*)로 표시됩니다.

    ![제품 설정](./media/managed-application-author-marketplace/newOffer_OfferSettings.png)

    4 개의 주 폼은 관리 되는 응용 프로그램을 사용 하는 toocreate 합니다.

    a. 제품 설정

    b. SKU

    c. 마켓플레이스

    d. 지원

이러한 폼 hello 다음 섹션에서에서 자세히 설명 되어 있습니다.

## <a name="offer-settings-form"></a>제품 설정 양식
이 기본 형식은 toospecify hello 제안 설정을 사용 합니다.

1. Hello 입력 **설정을 제공** 폼입니다. hello 다른 필드는 같습니다.

    a. **제안 ID**:이 고유 식별자 게시자 프로필 내에서 hello 제품을 식별 합니다. 이 ID는 제품 URL, Resource Manager 템플릿 및 청구 보고서에서 볼 수 있습니다. 소문자 영숫자 문자 또는 대시(-)로만 구성할 수 있습니다. hello ID에 대시 끝날 수 없습니다. 최대 50 자로 제한 tooa 것합니다. 제품이 라이브 상태가 되면 이 필드는 잠깁니다.

    b. **게시자 ID**: toopublish 아래에서이 서비스를 원하는이 드롭다운 목록에서 toochoose hello 게시자 프로필을 사용 합니다. 제품이 라이브 상태가 되면 이 필드는 잠깁니다.

    c. **이름**: hello 포털 및 hello Marketplace에에서 자신의 구독에 대 한이 표시 이름을 표시 합니다. 최대 50문자를 포함할 수 있습니다. 제품의 인식 가능한 브랜드 이름을 포함합니다. 회사 이름을 포함하는 것이 마케팅 전략인 경우를 제외하고 여기에 회사 이름을 포함하지 마세요. 자신의 웹 사이트에이 서비스를 마케팅 하는 경우 hello 이름이 확인 정확 하 게 웹 사이트에 표시 되는 방식입니다.

2. 선택 **저장** toosave 진행 합니다. 

## <a name="skus-form"></a>SKU 양식
hello 다음 단계에 대 한 제안 tooadd Sku입니다.

1. **SKU** > **새 SKU**를 선택합니다. 

    ![새 SKU 선택](./media/managed-application-author-marketplace/newOffer_skus.png)

2. **SKU ID**를 입력합니다. SKU ID는 제공 하는 서비스 내에서 SKU hello에 대 한 고유 식별자입니다. 이 ID는 제품 URL, Resource Manager 템플릿 및 청구 보고서에서 볼 수 있습니다. 소문자 영숫자 문자 또는 대시(-)로만 구성할 수 있습니다. hello ID에 대시를 끝나서는 안 되며 최대 50 자로 제한 tooa 있습니다. 제품이 라이브 상태가 되면 이 필드는 잠깁니다. 제품 내에 여러 SKU를 포함할 수 있습니다. 필요한 SKU toopublish 각 이미지에 대 한 계획입니다.

3. Hello 채울 **SKU 세부 정보** hello 다음 양식에서 섹션:

    ![새 SKU 제공](./media/managed-application-author-marketplace/newOffer_newsku.png)

    Hello 다음 필드를 입력 합니다.
    
    a. **제목**: 이 SKU의 제목을 입력합니다. 이 항목에 대 한 hello 갤러리에서이 제목이 표시 됩니다.

    b. **요약**: 이 SKU에 대한 간단한 요약을 입력합니다. 이 텍스트 hello 제목 아래에 나타납니다.

    c. **설명**: hello SKU에 대 한 자세한 설명을 입력 합니다.

    d. **SKU 유형의**: hello 가능한 값은 **관리 응용 프로그램** 및 **솔루션 템플릿을**합니다. 이 경우 **관리되는 응용 프로그램**을 선택합니다.

4. Hello 채울 **패키지 세부 정보** hello 다음 양식에서 섹션:

    ![패키지](./media/managed-application-author-marketplace/newOffer_newsku_package.png)

    Hello 다음 필드를 입력 합니다.

    a. **현재 버전**: hello 패키지 업로드에 대 한 버전을 입력 합니다. Hello 형태로 표시 것 `{number}.{number}.{number}{number}`합니다.

    b. **패키지 파일을 선택**: hello.zip 파일로 압축 된 파일을 다음이 패키지에 포함 되어 있습니다.
    * **applianceMainTemplate.json**: toodeploy hello 솔루션/응용 프로그램을 사용 하는 hello 배포 템플릿 파일입니다. 방법에 대 한 내용은 toocreate 배포 템플릿 파일을 참조 하세요. [첫 번째 Azure 리소스 관리자 서식 파일 만들기](resource-manager-create-first-template.md)합니다.
    * **appliancecreateUIDefinition.json**:이 파일은 tooprovision이 솔루션/응용 프로그램 사용 hello Azure 포털 toogenerate hello 사용자 인터페이스에서 사용 합니다. 자세한 내용은 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)을 참조하세요.
    * **mainTemplate.json**:이 템플릿 파일 hello Microsoft.Solution/appliances 리소스만 포함 합니다. hello mainTemplate 파일 hello를 다음 속성이 포함 되어 있습니다.

        *  **종류**: 사용 **마켓플레이스** hello Marketplace에서에서 관리 되는 응용 프로그램에 대 한 합니다.
        *  **ManagedResourceGroupId**: hello 고객의 구독에서이 리소스 그룹은 applianceMainTemplate.json에 정의 된 모든 hello 리소스 배포 됩니다.
        *  **PublisherPackageId**:이 문자열 hello 패키지를 고유 하 게 식별 합니다. Hello 형태로 표시의 hello 값을 제공 `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`합니다.

Hello 가져올 **ID 제공** 및 **게시자 ID** hello 다음 이미지와 같이 포털을 게시 하는 hello에서:

![제품 ID](./media/managed-application-author-marketplace/UniqueString_pubid_offerid.png)
        
Hello 가져올 **SKU ID**hello 다음 이미지에에서 나타난 것 처럼:

![SKU ID](./media/managed-application-author-marketplace/UniqueString_skuid.png)
        
Hello 패키지를 다운로드 **버전**hello 다음 이미지에에서 나타난 것 처럼:

![패키지 버전](./media/managed-application-author-marketplace/UniqueString_packageversion.png)
    
  값을 hello 앞 예제는 hello에 따라, **PublisherPackageId** 은 `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`합니다.

  샘플 mainTemplate.json:

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "storageAccountNamePrefix": {
        "type": "string",
        "metadata": {
          "description": "Specify hello name of hello storage account"
        }
      },
      "storageAccountType": {
        "type": "string"
      }
    },
    "variables": {
      "managedResourceGroup": "[concat(resourceGroup().id,uniquestring(resourceGroup().id))]"
    },
    "resources": [{
      "type": "Microsoft.Solutions/appliances",
      "apiVersion": "2016-09-01-preview",
      "name": "[concat(parameters('storageAccountNamePrefix'), '-', 'managed')]",
      "location": "[resourceGroup().location]",
      "kind": "marketplace",
      "properties": {
        "managedResourceGroupId": "[variables('managedResourceGroup')]",
        "PublisherPackageId":"azureappliancetest.ravmanagedapptest.ravpreviewmanagedsku.1.0.0",
        "parameters": {
          "storageAccountName": {
            "value": "[parameters('storageAccountNamePrefix')]"
          },
          "storageAccountType": {
            "value": "[parameters('storageAccountType')]"
          }
        }
      }
    }],
    "outputs": {

    }
  }
  ```

이 패키지는 다른 중첩 된 템플릿에 있어야 하거나 필요한 toosuccessfully 되는 스크립트를이 응용 프로그램을 제공 합니다. hello mainTemplate.json, applianceMainTemplate.json, 및 applianceCreateUIDefinition.json 파일이 있어야 hello 루트 폴더에 있습니다.

* **권한 부여**:이 속성은 액세스 및 hello 수준의 액세스를 가져옵니다는 고객의 구독에서 toohello 리소스를 정의 합니다. hello 게시자 toomanage hello 응용 프로그램 hello 고객을 대신 하 여 사용할 수 있습니다.
* **PrincipalId**:이 속성은 사용자, 사용자 그룹 또는 응용 프로그램 hello 고객의 구독에서 hello 리소스에 대 한 특정 권한 부여의 hello Azure Active Directory (Azure AD) 식별자입니다. 역할 정의 hello hello 권한을 설명합니다. 
* **역할 정의**:이 속성은 역할의 목록을 모든 hello 기본 제공 역할 기반 액세스 제어 (RBAC) Azure AD에서 제공 합니다. Hello 고객을 대신 하 여 가장 적합 한 toouse toomanage hello 리소스는 hello 역할을 선택할 수 있습니다.

여러 권한 부여를 추가할 수 있습니다. AD 사용자 그룹을 만들고 **PrincipalId**에서 해당 ID를 지정하는 것이 좋습니다. 이러한 방식으로 hello 필요 tooupdate hello SKU 없이 더 많은 사용자가 toohello 사용자 그룹을 추가할 수 있습니다.

RBAC에 대 한 자세한 내용은 참조 [hello Azure 포털에에서 RBAC 시작](../active-directory/role-based-access-control-what-is.md)합니다.

## <a name="marketplace-form"></a>Marketplace 양식

마켓플레이스 폼 hello hello에 표시 되는 필드에 대 한 요청 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com) hello에 [Azure 포털](https://portal.azure.com/)합니다.

### <a name="preview-subscription-ids"></a>미리 보기 구독 ID

Azure 구독 Id가 게시 된 후 hello 제안에 액세스할 수 있는 목록을 입력 합니다. 수행 하기 전에 이러한 구독 허용 목록을 tootest hello 미리 본 제품을 사용할 수 있습니다 라이브 합니다. Hello 파트너 포털에서 too100 구독을의 허용 목록을 컴파일할 수 있습니다.

### <a name="suggested-categories"></a>권장 범주

제안을 가장 된 연결 될 수 있는 hello 목록에서 toofive 범주를 선택 합니다. 이러한 범주는 사용 되는 toomap hello에서 사용할 수 있는 사용자 제공 toohello 제품 범주 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com) 및 hello [Azure 포털](https://portal.azure.com/)합니다.

#### <a name="azure-marketplace"></a>Azure 마켓플레이스

관리 되는 응용 프로그램의 hello 요약 hello를 다음 필드를 표시 합니다.

![Marketplace 요약](./media/managed-application-author-marketplace/publishvm10.png)

hello **개요** 탭에 관리 되는 응용 프로그램에 필드 다음 hello 표시 됩니다.

![마켓플레이스 개요](./media/managed-application-author-marketplace/publishvm11.png)

hello **계획 + 가격 책정** 탭에 관리 되는 응용 프로그램에 필드 다음 hello 표시 됩니다.

![Marketplace 계획](./media/managed-application-author-marketplace/publishvm15.png)

#### <a name="azure-portal"></a>Azure portal

관리 되는 응용 프로그램의 hello 요약 hello를 다음 필드를 표시 합니다.

![포털 요약](./media/managed-application-author-marketplace/publishvm12.png)

관리 되는 응용 프로그램에 대 한 hello 개요 hello를 다음 필드를 표시 합니다.

![포털 개요](./media/managed-application-author-marketplace/publishvm13.png)

#### <a name="logo-guidelines"></a>로고 지침

Hello 클라우드 파트너 포털에 업로드 하는 모든 로고에 대 한 이러한 지침을 따릅니다.

*   hello Azure 디자인 간단한 색상표를 있습니다. Hello 수가 기본과 보조 색 로고에 제한 합니다.
*   hello 포털의 hello 테마 색 흰색은 검정입니다. 로고에 대 한 hello 배경색으로 이러한 색을 사용 하지 마십시오. Hello 포털에서 관련성이 로고 하는 색을 사용 합니다. 간단한 기본 색을 사용하는 것이 좋습니다. *투명 한 배경을 사용 하는 경우 hello 로고와 텍스트 흰색이 아닌 있는지 확인 검정, 또는 파란색입니다.*
*   그라데이션 배경이 hello 로고에 사용 하지 마십시오.
*   Hello 로고, 하더라도 회사 또는 브랜드 이름에 텍스트를 배치 하지 마십시오. 로고의 hello 모양과 느낌 플랫와 기울기를 방지 합니다.
*   Hello 로고 확대 되지 있는지 확인 합니다.

#### <a name="hero-logo"></a>대표 로고

hello hero 로고 선택 사항입니다. hello 게시자 하지 tooupload hero 로고를 선택할 수 있습니다. Hello hero 아이콘을 업로드 한 후에 삭제할 수 없습니다. 그 당시 hello 파트너 hero 아이콘에 대 한 hello 마켓플레이스 지침을 따라야 합니다.

Hello hero 로고 아이콘에 대 한 이러한 지침을 따릅니다.

*   hello 게시자 표시 이름, hello 계획 제목 및 긴 요약 hello 제공 흰색으로 표시 됩니다. 따라서 사용 하지 마십시오 밝은 색 hello hero 아이콘의 hello 배경색입니다. 대표 아이콘에는 검은색, 흰색 또는 투명한 배경이 허용되지 않습니다.
*   Hello 제안을 나열 됩니다 hello 게시자 표시 이름, hello 계획 제목, 긴 요약 hello 제안 및 hello **만들기** 단추 hello hero 로고에 프로그래밍 방식으로 포함 합니다. 따라서 하지 hello hero 로고를 디자인 하는 동안 텍스트를 입력 합니다. 빈 공간 hello에 오른쪽 것 이므로 유지 hello 텍스트가 해당 공간에에서 프로그래밍 방식으로 포함 됩니다. hello 텍스트에 대 한 hello 빈 공간 hello 오른쪽에 415 x 100 픽셀 이어야 합니다. Hello 왼쪽에서 370 픽셀로 오프셋 됩니다.

    ![대표 로고 예제](./media/managed-application-author-marketplace/publishvm14.png)

## <a name="support-form"></a>지원 양식

Hello 채울 **지원** 회사에서 지 원하는 폼에 연결 합니다. 이 정보는 엔지니어링 연락처와 고객 지원 연락처일 수 있습니다.

## <a name="publish-an-offer"></a>제품 게시

모든 hello 섹션을 입력 한 후 선택 **게시** 제안을 사용할 수 있는 toocustomers 하는 toostart hello 프로세스가 있습니다.

## <a name="next-steps"></a>다음 단계

* 소개 toomanaged 응용 프로그램에 대 한 참조 [관리 되는 응용 프로그램 개요](managed-application-overview.md)합니다.
* Hello 시장에서에서 관리 되는 응용 프로그램을 사용 하는 방법에 대 한 정보를 참조 하십시오. [사용할 Azure 관리 응용 프로그램 마켓플레이스 hello에](managed-application-consume-marketplace.md)합니다.
* 서비스 카탈로그 관리되는 응용 프로그램을 게시하는 방법에 대한 자세한 내용은 [서비스 카탈로그 관리되는 응용 프로그램 만들기 및 게시](managed-application-publishing.md)를 참조하세요.
* 서비스 카탈로그 관리되는 응용 프로그램을 사용하는 방법에 대한 자세한 내용은 [서비스 카탈로그 관리되는 응용 프로그램 사용](managed-application-consumption.md)을 참조하세요.
