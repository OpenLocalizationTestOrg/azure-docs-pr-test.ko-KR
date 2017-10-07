---
title: "aaaProtect Azure API 관리에서 API | Microsoft Docs"
description: "자세한 내용은 방법 tooprotect 할당량 및 제한 (속도 제한) 정책을 사용 하 여 API입니다."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 450dc368-d005-401d-ae64-3e1a2229b12f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3113fd277d434da0c051b8b90fd629a102bf4867
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-api-with-rate-limits-using-azure-api-management"></a>Azure API Management를 사용하여 속도 제한으로 API 보호
이 가이드에서는 얼마나 쉬운지 백 엔드 API에 대 한 보호 tooadd Azure API 관리 속도 제한 및 할당량 정책을 구성 하 여 보여 줍니다.

이 자습서에서는 개발자가 사용할 수 있는 "무료 평가판" API 제품 만들어집니다 toomake tooa 최대 200 hello를 사용 하 여 주 tooyour API 호출을 분당 too10 호출 위쪽과 [구독 당 호출 속도 제한](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) 및 [ 구독 당 용 할당량 설정](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) 정책입니다. 그런 다음 hello API를 게시 하 고 hello 속도 제한 정책을 테스트 합니다.

좀 더 조정 hello를 사용 하는 시나리오를 고급 [키로 속도 제한](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) 및 [키로 할당량](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) 정책 참조 [제한 Azure API 관리 고급 요청](api-management-sample-flexible-throttling.md)합니다.

## <a name="create-product"></a>toocreate 제품
이 단계에서는 구독 승인을 요구하지 않는 무료 평가판 제품을 만듭니다.

> [!NOTE]
> 경우 이미 구성 된 제품 있고 toouse이이 자습서에 대 한 것을 이동할 수 있습니다 너무[구성 호출 속도 제한 및 할당량 정책을] [ Configure call rate limit and quota policies] 제품을 사용 하 여 여기에서 hello 자습서에 따라 및 대신 hello 무료 평가판 제품입니다.
> 
> 

시작 tooget 클릭 **게시자 포털** API 관리 서비스에 대 한 hello Azure 포털의에서.

![게시자 포털][api-management-management-console]

> API 관리 서비스 인스턴스를 아직 만들지 않은 경우 참조 [API 관리 서비스 인스턴스를 만들] [ Create an API Management service instance] hello에 [Azure API 관리에서 첫 번째 API 관리] [ Manage your first API in Azure API Management] 자습서입니다.
> 
> 

클릭 **제품** hello에 **API 관리** hello 왼쪽된 toodisplay hello에 메뉴 **제품** 페이지.

![제품 추가][api-management-add-product]

클릭 **추가 제품** toodisplay hello **추가 신제품** 대화 상자.

![새 제품 추가][api-management-new-product-window]

Hello에 **제목** 상자에서 입력 **무료 평가판**합니다.

Hello에 **설명** 상자, 텍스트 다음 형식 hello: **구독자를 200 호출/주 액세스가 거부 되었습니다 tooa 최대 호출 수 toorun 10 수/분이 됩니다.**

API Management의 제품은 보호되거나 개방될 수 있습니다. 보호 된 제품 구독된 toobefore 사용할 수 있어야 합니다. 개방된 제품은 구독하지 않고 사용할 수 있습니다. 되도록 **구독 필요** 은 선택한 toocreate 구독을 필요로 하는 보호 된 제품입니다. Hello 기본 설정입니다.

관리자 tooreview을 수락 하거나 거부 구독에서 toothis 제품 선택 **구독 승인이 필요한**합니다. Hello 확인란을 선택 하지 않으면 자동으로 승인 구독 시도 됩니다. 이 예제에서는 구독 승인 자동으로 되므로 hello 확인란을 선택 하지 마십시오.

tooallow 개발자 계정 toosubscribe 여러 번 toohello 신제품 선택 hello **여러 동시 구독을 허용할** 확인란 합니다. 이 자습서는 여러 동시 구독을 활용하지 않으므로 해당 항목을 선택하지 않습니다.

모든 값을 입력 한 후 클릭 **저장** toocreate hello 제품입니다.

![제품 추가됨][api-management-product-added]

기본적으로 새로운 제품은 hello에 표시 toousers **관리자** 그룹입니다. Tooadd hello 하겠습니다 **개발자** 그룹입니다. 클릭 **무료 평가판**, hello를 클릭 한 다음 **가시성** 탭 합니다.

> API 관리 그룹은 제품 toodevelopers 사용 되는 toomanage hello 표시 합니다. 제품은 가시성 toogroups 부여 및 개발자가 보고 하 고는 속해 있는 표시 toohello 그룹 toohello 제품을 구독 합니다. 자세한 내용은 참조 [Azure API 관리에서 사용 하 여 toocreate 그룹화 하는 방법][How toocreate and use groups in Azure API Management]합니다.
> 
> 

![개발자 그룹 추가][api-management-add-developers-group]

선택 hello **개발자** 확인란을 선택한 다음 클릭 **저장**합니다.

## <a name="add-api"></a>tooadd API toohello 제품
Hello 자습서의이 단계에서는 hello 에코 API toohello 새로운 무료 평가판 제품을 추가 합니다.

> 각 API 관리 서비스 인스턴스를 사용 하는 tooexperiment 및 API 관리에 대 한 자세한 내용은 수 있는 에코 API로 미리 구성 되어 제공 됩니다. 자세한 내용은 [Azure API Management에서 첫 번째 API Management][Manage your first API in Azure API Management]를 참조하세요.
> 
> 

클릭 **제품** hello에서 **API 관리** 를 hello 왼쪽, 클릭 한 다음 메뉴 **무료 평가판** tooconfigure hello 제품입니다.

![제품 구성][api-management-configure-product]

클릭 **추가 API tooproduct**합니다.

![API tooproduct 추가][api-management-add-api]

**Echo API**를 선택하고 **저장**을 클릭합니다.

![Echo API 추가][api-management-add-echo-api]

## <a name="policies"></a>tooconfigure 호출 속도 제한 및 할당량 정책
속도 제한 및 할당량 hello 정책 편집기에서 구성 됩니다. 이 자습서에서는 추가할 예정 hello 두 정책을 hello [구독 당 호출 속도 제한](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) 및 [구독 당 용 할당량 설정](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) 정책입니다. 이러한 정책은 hello 제품 범위에서 적용 되어야 합니다.

클릭 **정책** hello에서 **API 관리** hello 왼쪽 메뉴. Hello에 **제품** 목록에서 클릭 **무료 평가판**합니다.

![제품 정책][api-management-product-policy]

클릭 **정책 추가** tooimport 정책 템플릿을 hello 및 hello 속도 제한 및 할당량 정책 만들기를 시작 합니다.

![정책 추가][api-management-add-policy]

속도 제한 및 할당량 정책은 인바운드 정책, 등 위치 hello 커서 hello 인바운드 요소에 사용 됩니다.

![정책 편집기][api-management-policy-editor-inbound]

정책 목록 hello 스크롤하여 이동 하며 hello 찾을 **구독 당 호출 속도 제한** 정책 항목입니다.

![정책 설명][api-management-limit-policies]

Hello에 커서가 놓입니다 hello 후 **인바운드** 정책 요소 옆에 있는 hello 화살표를 클릭 **구독 당 호출 속도 제한** tooinsert 정책 템플릿에 해당 합니다.

```xml
<rate-limit calls="number" renewal-period="seconds">
<api name="name" calls="number">
<operation name="name" calls="number" />
</api>
</rate-limit>
```

Hello 조각 알 수 있듯이 hello 정책 hello 제품의 Api 및 작업에 대 한 제한을 설정 있습니다. 이 자습서에서는 하지를 사용 하는 해당 기능 hello를 삭제 하므로 **api** 및 **작업** hello에서 요소를 **속도 제한** 만 외부 hello등요소**속도 제한** hello 다음 예제와 같이 요소가 유지 됩니다.

```xml
<rate-limit calls="number" renewal-period="seconds">
</rate-limit>
```

Hello 무료 평가판 제품 hello 허용 가능한 최대 호출 속도 분당 10 개의 호출이 구분 하므로 입력 **10** hello에 대 한 hello 값으로 **호출** 특성 및 **60** hello에대한**갱신 기간** 특성입니다.

```xml
<rate-limit calls="10" renewal-period="60">
</rate-limit>
```

tooconfigure hello **구독 당 용 할당량 설정** hello 바로 아래의 커서 새로 추가 정책, 위치 **속도 제한** hello 내의 요소 **인바운드** 요소를 다음를 hello toohello 왼쪽의 화살표를 클릭 **구독 당 용 할당량 설정**합니다.

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
<api name="name" calls="number" bandwidth="kilobytes">
<operation name="name" calls="number" bandwidth="kilobytes" />
</api>
</quota>
```

마찬가지로 toohello **구독 당 용 할당량 설정** 정책을 **구독 당 용 할당량 설정** 정책 hello 제품의 Api 및 작업에 대 한 caps를 설정할 수 있습니다. 이 자습서에서는 하지를 사용 하는 해당 기능 hello를 삭제 하므로 **api** 및 **작업** hello에서 요소를 **할당량** hello 다음 예제와 같이 요소입니다.

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
</quota>
```

할당량은 hello 간격, 대역폭, 또는 둘 다 호출 수를 기반으로 수 있습니다. 이 자습서에서는 우리는 조정 안 함에 따라 대역폭, hello를 삭제 하므로 **대역폭** 특성입니다.

```xml
<quota calls="number" renewal-period="seconds">
</quota>
```

Hello 무료 평가판 제품 hello 할당량 주당 200 개의 호출을은입니다. 지정 **200** hello에 대 한 hello 값으로 **호출** 특성을 선택한 다음 지정 **604800** hello에 대 한 hello 값으로 **갱신 기간** 특성입니다.

```xml
<quota calls="200" renewal-period="604800">
</quota>
```

> 정책 간격은 초 단위로 지정합니다. 1 주일 toocalculate hello 간격을 hello hello 수가 hello 시간 (초) 1 분 (60)에 한 시간 (60)에 대 한 변경 hello 수 (24) 하루에서 시간 (7) 일 수를 곱하면 됩니다: 7 * 24 * 60 * 60 = 604800 합니다.
> 
> 

Hello 정책 구성 했으면 다음 예제는 hello와 일치 해야 합니다.

```xml
<policies>
    <inbound>
        <rate-limit calls="10" renewal-period="60">
        </rate-limit>
        <quota calls="200" renewal-period="604800">
        </quota>
        <base />

</inbound>
<outbound>

    <base />

    </outbound>
</policies>
```

Hello 정책이 구성 된 원하는 클릭 **저장**합니다.

![정책 저장][api-management-policy-save]

## <a name="publish-product"></a> toopublish hello 제품
Hello hello Api가 추가 하 고 구성 된 hello 정책, 했으므로 hello 제품 개발자가 사용할 수 있도록 게시 되어야 합니다. 클릭 **제품** hello에서 **API 관리** 를 hello 왼쪽, 클릭 한 다음 메뉴 **무료 평가판** tooconfigure hello 제품입니다.

![제품 구성][api-management-configure-product]

클릭 **게시**, 클릭 하 고 **예, 게시** tooconfirm 합니다.

![제품 게시][api-management-publish-product]

## <a name="subscribe-account"></a>toosubscribe 개발자 계정 toohello 제품
해당 hello 제품을 게시 하면 이제 구독 사용 가능한 toobe tooand 개발자가 사용 됩니다.

> API 관리 인스턴스 관리자는 자동으로 구독된 tooevery 제품입니다. 이 자습서 단계 hello 관리자가 아닌 개발자 계정 toohello 무료 평가판 제품 중 하 나와 겠습니다. 개발자 계정을 hello 관리자 역할의 일부 이면 다음 함께 수행할 수 있습니다이 단계를 이미 구독 하는 경우에 합니다.
> 
> 

클릭 **사용자** hello에 **API 관리** hello에 메뉴 왼쪽과 hello 개발자 계정 이름을 클릭 합니다. 이 예제에서 사용 하 여 hello **필터를 만들면 Gragg** 개발자 계정.

![개발자 구성][api-management-configure-developer]

**구독 추가**를 클릭합니다.

![구독 추가][api-management-add-subscription-menu]

**무료 평가판**을 선택한 다음, **구독**을 클릭합니다.

![구독 추가][api-management-add-subscription]

> [!NOTE]
> 이 자습서에서는 여러 동시 구독 hello 무료 평가판 제품에 대 한 사용 되지 않습니다. 큐브인 것 hello 다음 예제와 같이 증명된 tooname hello 구독 것입니다.
> 
> 

![구독 추가][api-management-add-subscription-multiple]

클릭 한 후 **Subscribe**, hello에 hello 제품 표시 **구독** hello 사용자에 대 한 목록입니다.

![구독 추가됨][api-management-subscription-added]

## <a name="test-rate-limit"></a>toocall 작업 및 테스트 hello 속도 제한
이제 hello 무료 평가판 제품 구성 되 고 게시, 우리 수 일부 작업을 호출을 hello 속도 제한 정책을 테스트 합니다.
클릭 하 여 스위치 toohello 개발자 포털 **개발자 포털** hello 오른쪽 위 메뉴에서 합니다.

![개발자 포털][api-management-developer-portal-menu]

클릭 **Api** 에 최상위 메뉴 hello 및 클릭 **에코 API**합니다.

![개발자 포털][api-management-developer-portal-api-menu]

**GET Resource**를 클릭한 다음 **사용해 보세요**를 클릭합니다.

![콘솔 시작][api-management-open-console]

Hello 기본 매개 변수 값을 유지 하 고 hello 무료 평가판 제품에 대 한 사용자 구독 키를 선택 합니다.

![구독 키][api-management-select-key]

> [!NOTE]
> 다중 구독인 경우 수에 대 한 있는지 tooselect hello 키 **무료 평가판**, 또는 hello 이전 단계에서 구성 된 다른 hello 정책 적용 되지 않습니다.
> 
> 

클릭 **보낼**, hello 응답을 확인 합니다. 참고 hello **응답 상태** 의 **200 확인**합니다.

![작업 결과][api-management-http-get-results]

클릭 **보낼** 분당 10 개의 호출 속도 제한 정책 hello 보다 큰 속도로 합니다. Hello 속도 제한 정책 초과 후의 응답 상태 **429 너무 많은 요청** 반환 됩니다.

![작업 결과][api-management-http-get-429]

hello **응답 콘텐츠** 간격 남아 있는 다시 시도가 성공적으로 수행 됩니다. 전에 hello를 나타냅니다.

분당 10 개의 호출이의 hello 속도 제한 정책 사용 되 고 hello에서 60 분이 지난 후 후속 호출은 실패 합니다 hello 속도 한도 초과 하기 전에 hello 10 성공한 호출 toohello 제품의 첫 번째입니다. 이 예제에서는 간격 남은 hello 54 초입니다.

## <a name="next-steps"> </a>다음 단계
* 데모 비디오를 따라 hello에서 속도 제한 및 할당량을 설정 합니다.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-product-with-rules/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-product-with-rules/api-management-add-product.png
[api-management-new-product-window]: ./media/api-management-howto-product-with-rules/api-management-new-product-window.png
[api-management-product-added]: ./media/api-management-howto-product-with-rules/api-management-product-added.png
[api-management-add-policy]: ./media/api-management-howto-product-with-rules/api-management-add-policy.png
[api-management-policy-editor-inbound]: ./media/api-management-howto-product-with-rules/api-management-policy-editor-inbound.png
[api-management-limit-policies]: ./media/api-management-howto-product-with-rules/api-management-limit-policies.png
[api-management-policy-save]: ./media/api-management-howto-product-with-rules/api-management-policy-save.png
[api-management-configure-product]: ./media/api-management-howto-product-with-rules/api-management-configure-product.png
[api-management-add-api]: ./media/api-management-howto-product-with-rules/api-management-add-api.png
[api-management-add-echo-api]: ./media/api-management-howto-product-with-rules/api-management-add-echo-api.png
[api-management-developer-portal-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-menu.png
[api-management-publish-product]: ./media/api-management-howto-product-with-rules/api-management-publish-product.png
[api-management-configure-developer]: ./media/api-management-howto-product-with-rules/api-management-configure-developer.png
[api-management-add-subscription-menu]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-menu.png
[api-management-add-subscription]: ./media/api-management-howto-product-with-rules/api-management-add-subscription.png
[api-management-developer-portal-api-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-api-menu.png
[api-management-open-console]: ./media/api-management-howto-product-with-rules/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-product-with-rules/api-management-http-get.png
[api-management-http-get-results]: ./media/api-management-howto-product-with-rules/api-management-http-get-results.png
[api-management-http-get-429]: ./media/api-management-howto-product-with-rules/api-management-http-get-429.png
[api-management-product-policy]: ./media/api-management-howto-product-with-rules/api-management-product-policy.png
[api-management-add-developers-group]: ./media/api-management-howto-product-with-rules/api-management-add-developers-group.png
[api-management-select-key]: ./media/api-management-howto-product-with-rules/api-management-select-key.png
[api-management-subscription-added]: ./media/api-management-howto-product-with-rules/api-management-subscription-added.png
[api-management-add-subscription-multiple]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-multiple.png

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Manage your first API in Azure API Management]: api-management-get-started.md
[How toocreate and use groups in Azure API Management]: api-management-howto-create-groups.md
[View subscribers tooa product]: api-management-howto-add-products.md#view-subscribers
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps

[Create a product]: #create-product
[Configure call rate limit and quota policies]: #policies
[Add an API toohello product]: #add-api
[Publish hello product]: #publish-product
[Subscribe a developer account toohello product]: #subscribe-account
[Call an operation and test hello rate limit]: #test-rate-limit

[Limit call rate]: https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate
[Set usage quota]: https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota
