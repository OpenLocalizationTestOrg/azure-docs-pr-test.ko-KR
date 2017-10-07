---
title: "Azure API 관리에서 그룹을 사용 하 여 aaaManage 개발자 계정을 | Microsoft Docs"
description: "어떻게 toomanage 개발자 계정을 사용 하 여 자세한 내용은 Azure API 관리에서 그룹"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 33660b45-442f-44be-9a4a-1899d7f699b0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: c46e010e41d9705ae161dcd60d734a76d19c9e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-groups-toomanage-developer-accounts-in-azure-api-management"></a>Azure API 관리에서 사용 하 여 toocreate 그룹 toomanage 개발자 계정을 어떻게
API 관리 그룹은 제품 toodevelopers 사용 되는 toomanage hello 표시 합니다. 제품을 만들어 놓은 첫 번째 표시 toogroups 및 개발자가 해당 그룹에서 보고 하 고 hello 그룹과 연결 된 toohello 제품을 구독 합니다. 

API 관리 hello 변경할 수 없는 시스템 그룹 뒤에 있습니다.

* **관리자** - Azure 구독 관리자가 이 그룹의 구성원입니다. 관리자 API 관리 서비스 인스턴스, 관리 Api, 작업 및 개발자가 사용 하는 제품 hello 만들기.
* **개발자** - 인증된 개발자 포털 사용자가 이 그룹에 속합니다. 개발자는 Api를 사용 하 여 응용 프로그램을 구축 하는 hello 고객 있습니다. 개발자는 toohello 개발자 포털 액세스 권한이 부여 된 하 고 API의 hello 작업을 호출 하는 응용 프로그램을 빌드합니다.
* **게스트** -예:이 그룹에는 API 관리 인스턴스 년의 hello 개발자 포털을 방문 하는 잠재 고객의 개발자 포털 사용자가 인증 되지 않은 합니다. Hello 기능 tooview Api와 같은 특정 읽기 전용 액세스를 부여할 수 되지만 호출 하지 않습니다.

관리자 추가 toothese 시스템 그룹에 사용자 지정 그룹을 만들 수 있습니다 또는 [연결 된 Azure Active Directory 테 넌 트의 외부 그룹을 활용 하 여][leverage external groups in associated Azure Active Directory tenants]합니다. 사용자 지정 그룹과 외부 그룹 개발자 가시성 제공 시스템 그룹과 함께 사용할 수 있으며 tooAPI 제품에 액세스 합니다. 예를 들어 특정와 개발자가 파트너 조직 및의 액세스 허용 사용자 지정 그룹 하나 만들 수 있습니다 관련 Api만 포함 된 제품에서 Api toohello 합니다. 사용자는 두 그룹 이상의 구성원이 될 수 있습니다.

이 가이드에서는 API 관리 인스턴스의 관리자가 새 그룹을 추가하고 이 그룹과 새 제품 및 개발자를 연결하는 방법을 보여 줍니다.

> [!NOTE]
> 또한 toocreating hello 게시자 포털에서 그룹 관리을 있습니다 수 만들고 hello API 관리 REST API를 사용 하 여 그룹 관리 [그룹](https://msdn.microsoft.com/library/azure/dn776329.aspx) 엔터티.
> 
> 

## <a name="create-group"> </a>그룹 만들기
새 그룹을 toocreate 클릭 **게시자 포털** API 관리 서비스에 대 한 hello Azure 포털의에서. API 관리 게시자 포털 toohello 이동합니다.

![게시자 포털][api-management-management-console]

> API 관리 서비스 인스턴스를 아직 만들지 않은 경우 참조 [API 관리 서비스 인스턴스를 만들] [ Create an API Management service instance] hello에 [Azure API 관리 시작] [ Get started with Azure API Management] 자습서입니다.
> 
> 

클릭 **그룹** hello에서 **API 관리** 를 hello 왼쪽, 클릭 한 다음 메뉴 **그룹 추가**합니다.

![새 그룹 추가][api-management-add-group]

Hello 그룹 및 선택적 설명을 대 한 고유한 이름을 입력 하 고 클릭 **저장**합니다.

![새 그룹 추가][api-management-add-group-window]

hello 그룹 탭 tooedit hello hello 새 그룹이 표시 됩니다 **이름** 또는 **설명** hello 그룹의 hello 목록의 hello 그룹의 hello 이름을 클릭 합니다. toodelete hello 그룹에서 클릭 **삭제**합니다.

![그룹 추가됨][api-management-new-group]

Hello 그룹을 만든 했으므로 제품 및 개발자와 연결할 수 있습니다.

## <a name="associate-group-product"> </a>그룹과 제품 연결
제품을 가진 그룹이 tooassociate 클릭 **제품** hello에서 **API 관리** hello에 메뉴 왼쪽과 hello 원하는 제품의 hello 이름을 클릭 합니다.

![표시 여부 설정][api-management-add-group-to-product]

선택 hello **가시성** tooadd 탭 및 그룹 및 tooview hello hello 제품에 대 한 현재 그룹을 제거 합니다. tooadd / 제거 그룹을 확인 하거나 hello 원하는 그룹 및 클릭에 대 한 hello 확인란의 선택을 취소 **저장**합니다.

![표시 여부 설정][api-management-add-group-to-product-visibility]

> [!NOTE]
> tooadd Azure Active Directory 그룹 참조 [tooauthorize 개발자 방법을 사용 하 여 계정을 Azure Active Directory를 Azure API 관리에서](api-management-howto-aad.md)합니다.
> 
> hello tooconfigure 그룹 **가시성** 제품에 대 한 탭을 클릭 **그룹 관리**합니다.
> 
> 

제품 그룹에 연결 되 고 나면 개발자가 해당 그룹에서 볼 수 있으며 toohello 제품 구독.

## <a name="associate-group-developer"> </a>그룹과 개발자 연결
개발자 tooassociate 그룹 클릭 **사용자** hello에서 **API 관리** 왼쪽, hello 및 hello 개발자 옆의 확인란 hello에 메뉴 tooassociate 사용 하 여 원하는 그룹입니다.

![개발자 toogroup 추가][api-management-add-group-to-developer]

Hello 원하는 개발자가 확인 되 면 클릭 hello에서 원하는 그룹 hello **tooGroup 추가** 드롭 다운 합니다. 개발자가 hello를 사용 하 여 그룹에서 제거할 수 **그룹에서 제거** 드롭 다운 합니다. 

![개발자][api-management-add-group-to-developer-saved]

Hello 개발자 및 hello 그룹 간의 hello 연결이 추가 되 면 hello에서 볼 수 있습니다 **사용자** 탭 합니다.

## <a name="next-steps"> </a>다음 단계
* 개발자 tooa 그룹에 추가 되 면 확인 하 고 해당 그룹에 연결 된 toohello 제품을 구독 합니다. 자세한 내용은 [Azure API Management에서 제품을 만들고 게시하는 방법][How create and publish a product in Azure API Management]을 참조하세요.
* 또한 toocreating hello 게시자 포털에서 그룹 관리을 있습니다 수 만들고 hello API 관리 REST API를 사용 하 여 그룹 관리 [그룹](https://msdn.microsoft.com/library/azure/dn776329.aspx) 엔터티.

[api-management-management-console]: ./media/api-management-howto-create-groups/api-management-management-console.png
[api-management-add-group]: ./media/api-management-howto-create-groups/api-management-add-group.png
[api-management-add-group-window]: ./media/api-management-howto-create-groups/api-management-add-group-window.png
[api-management-new-group]: ./media/api-management-howto-create-groups/api-management-new-group.png
[api-management-add-group-to-product]: ./media/api-management-howto-create-groups/api-management-add-group-to-product.png
[api-management-add-group-to-product-visibility]: ./media/api-management-howto-create-groups/api-management-add-group-to-product-visibility.png
[api-management-add-group-to-developer]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer.png
[api-management-add-group-to-developer-saved]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer-saved.png

[api-management-]: ./media/api-management-howto-create-groups/api-management-.png

[Create a group]: #create-group
[Associate a group with a product]: #associate-group-product
[Associate groups with developers]: #associate-group-developer
[Next steps]: #next-steps

[How create and publish a product in Azure API Management]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[leverage external groups in associated Azure Active Directory tenants]: api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group
