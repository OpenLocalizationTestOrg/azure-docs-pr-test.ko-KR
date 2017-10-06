---
title: "aaaHow toocreate 하 고 Azure API 관리에서 제품 게시"
description: "자세한 내용은 방법 toocreate 하 고 Azure API 관리에서 제품을 게시 합니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 31de55cb-9384-490b-a2f2-6dfcf83da764
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: f0a37f08b4e29ca68be9caec4c7604e3b4b6aaa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-publish-a-product-in-azure-api-management"></a>어떻게 toocreate 하 고 Azure API 관리에서 제품 게시
Azure API 관리에서 제품으로 하나 이상의 Api 사용 할당량 및 hello 사용 약관을 포함합니다. 제품이 게시 되 면 개발자 toohello 제품을 구독 하 고 toouse hello 제품의 Api를 시작할 수 있습니다. hello 항목 가이드 toocreating 제품에서 API를 추가 하 고 개발자를 위한 게시를 제공 합니다.

## <a name="create-product"> </a>제품 만들기
작업 추가 되 고 hello 게시자 포털에서 tooan API를 구성 합니다. tooaccess 게시자 포털을 클릭 하 여 hello **게시자 포털** API 관리 서비스에 대 한 hello Azure 포털의에서.

![게시자 포털][api-management-management-console]

> API 관리 서비스 인스턴스를 아직 만들지 않은 경우 참조 [API 관리 서비스 인스턴스를 만들] [ Create an API Management service instance] hello에 [Azure API 관리 시작] [ Get started with Azure API Management] 자습서입니다.
> 
> 

클릭 **제품** hello 메뉴 hello 왼쪽된 toodisplay hello에서 **제품** 페이지를 클릭 하 여 **제품 추가**합니다.

![제품][api-management-products]

![새 제품][api-management-add-new-product]

Hello에 hello 제품에 대 한 설명이 포함 된 이름을 입력 **이름** 필드와 hello 제품 hello에 대 한 설명 **설명** 필드입니다.

API Management에서 제품은 **개방형** 또는 **보호된** 제품일 수 있습니다. 보호 된 제품에 사용할 수 있습니다, 열려 있는 동안 구독된 toobefore 여야 합니다. 구독 없이 제품을 사용할 수 있습니다. 확인 **구독 필요** toocreate 구독 필요로 하는 보호 된 제품입니다. Hello 기본 설정입니다.

확인 **구독 승인이 필요한** 관리자 tooreview을 수락 하거나 거부 구독에서 toothis 제품입니다. Hello 상자 선택 하지 않으면 자동으로 승인 구독 시도 됩니다. 구독에 대 한 자세한 내용은 참조 하십시오. [구독자 tooa 제품][View subscribers tooa product]합니다.

tooallow 개발자 계정 toosubscribe 여러 번 toohello 제품 확인 hello **여러 구독을 허용할** 확인란 합니다. 이 확인란을 선택 하지 않으면 각 개발자 계정을 한 번 toohello 제품만를 구독할 수 있습니다.

![무제한의 여러 구독][api-management-unlimited-multiple-subscriptions]

여러 동시 구독 toolimit hello 수 확인 hello **동시에 대 한 구독 수를 제한** 확인란을 선택 하 고 hello 구독 제한을 입력 합니다. 다음 예제는 hello에서 동시 구독은 개발자 계정당 toofour를 제한 합니다.

![네 개의 여러 구독][api-management-four-multiple-subscriptions]

모든 새 제품 옵션이 구성 되 면 클릭 **저장** toocreate hello 새 제품입니다.

![제품][api-management-products-page]

> 기본적으로 새로운 제품은 게시, 아니며 표시만 toohello **관리자** 그룹입니다.
> 
> 

hello에 hello 제품 이름을 제품을 tooconfigure 클릭 **제품** 탭 합니다.

## <a name="add-apis"></a>Tooa 제품 Api 추가
hello **제품** 페이지에 구성에 대 한 링크를 4 개: **요약**, **설정**, **가시성**, 및  **구독자**합니다. hello **요약** 탭은 하거나 수 있는 Api를 추가 하 고 게시 제품 게시를 취소 합니다.

![요약][api-management-new-product-summary]

제품을 게시 하기 전에 필요한 tooadd 하나 이상의 Api입니다. toodo이를 클릭 하이 여 **추가 API tooproduct**합니다.

![API 추가][api-management-add-apis-to-product]

Select hello 필요한 Api 및 클릭 **저장**합니다.

## <a name="add-description"></a>추가 설명 정보 tooa 제품
hello **설정을** 탭에서는 tooprovide hello 제품의 용도, hello에 대 한 액세스를 제공 하는 Api 등 기타 유용한 정보에 대 한 정보를 자세히 설명 합니다. hello 콘텐츠는 hello API를 호출 하 고 일반 텍스트 또는 HTML 태그에 쓸 수 있는 hello 개발자를 대상 합니다.

![제품 설정][api-management-product-settings]

확인 **구독 필요** toocreate는 구독 toobe 사용 하거나 선택 취소를 해야 하는 보호 된 제품 hello 확인란 toocreate는 open 제품 구독 없이 호출 될 수입니다.

선택 **구독 승인이 필요한** toomanually 제품에서 제공 하는 모든 구독 요청을 승인 하려면. 기본적으로 모든 제품 구독은 자동으로 부여됩니다.

tooallow 개발자 계정 toosubscribe 여러 번 toohello 제품 확인 hello **여러 구독을 허용할** 확인란을 선택 하 고 필요에 따라 제한을 지정 합니다. 이 확인란을 선택 하지 않으면 각 개발자 계정을 한 번 toohello 제품만를 구독할 수 있습니다.

필요에 따라 hello 입력 **사용 약관** 구독자 순서 toouse hello 제품에 동의 해야 하는 hello 제품에 대 한 사용 조건 hello를 설명 하는 필드입니다.

## <a name="publish-product"> </a>제품 게시
제품에 Api hello을 호출 하기 전에 hello 제품 게시 되어야 합니다. Hello에 **요약** hello 제품에 대 한 탭을 클릭 **게시**, 클릭 하 고 **예, 게시** tooconfirm 합니다. 이전에 게시 된 제품 private toomake 클릭 **게시 취소**합니다.

![제품 게시][api-management-publish-product]

## <a name="make-visible"></a>제품 표시 toodevelopers 확인
hello **가시성** 탭에서는 toochoose 어떤 역할이 hello 개발자 포털에서 수 toosee hello 제품 및 toohello 제품을 구독할 수 있습니다.

![제품 표시][api-management-product-visiblity]

그룹에 hello 개발자를 위한 제품의 tooenable 또는 사용 안 함 표시 유형 확인 또는 hello hello 그룹 옆에 있는 확인란의 선택을 취소 및 클릭 **저장**합니다.

> 자세한 내용은 참조 [Azure API 관리에서 사용 하 여 toocreate 그룹 toomanage 개발자 계정을 어떻게][How toocreate and use groups toomanage developer accounts in Azure API Management]합니다.
> 
> 

## <a name="view-subscribers"></a>구독자 tooa 제품
hello **구독자** toohello 제품을 구독 하는 hello 개발자 탭에 나열 합니다. hello 세부 정보 및 각 개발자에 대 한 설정을 볼 수 있습니다 hello 개발자의 이름을 클릭 하 여 합니다. 이 예에서 없는 개발자 toohello 제품 아직 구독 합니다.

![개발자][api-management-developer-list]

## <a name="next-steps"> </a>다음 단계
한 번 hello 필요한 Api가 추가 하 고 hello 제품이 게시 개발자 수 toohello 제품 구독 toocall hello Api를 시작 합니다. 이러한 항목 및 고급 제품 구성을 설명하는 자습서에 대해서는 [AzureAPI Management에서 고급 제품 설정을 만들고 구성하는 방법][How create and configure advanced product settings in Azure API Management]을 참조하세요.

제품 사용에 대 한 자세한 내용은 hello 다음 비디오를 참조 하세요.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs tooa product]: #add-apis
[Add descriptive information tooa product]: #add-description
[Publish a product]: #publish-product
[Make a product visible toodevelopers]: #make-visible
[View subscribers tooa product]: #view-subscribers
[Next steps]: #next-steps

[api-management-management-console]: ./media/api-management-howto-add-products/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-add-products/api-management-add-product.png
[api-management-add-new-product]: ./media/api-management-howto-add-products/api-management-add-new-product.png
[api-management-unlimited-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-unlimited-multiple-subscriptions.png
[api-management-four-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-four-multiple-subscriptions.png
[api-management-products-page]: ./media/api-management-howto-add-products/api-management-products-page.png
[api-management-new-product-summary]: ./media/api-management-howto-add-products/api-management-new-product-summary.png
[api-management-add-apis-to-product]: ./media/api-management-howto-add-products/api-management-add-apis-to-product.png
[api-management-product-settings]: ./media/api-management-howto-add-products/api-management-product-settings.png
[api-management-publish-product]: ./media/api-management-howto-add-products/api-management-publish-product.png
[api-management-product-visiblity]: ./media/api-management-howto-add-products/api-management-product-visibility.png
[api-management-developer-list]: ./media/api-management-howto-add-products/api-management-developer-list.png



[api-management-products]: ./media/api-management-howto-add-products/api-management-products.png
[api-management-]: ./media/api-management-howto-add-products/
[api-management-]: ./media/api-management-howto-add-products/


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How toocreate and use groups toomanage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 
