---
title: "Azure 웹 앱에 대 한 사용자 지정 도메인 이름 aaaBuy"
description: "Azure 앱 서비스의 웹 앱과 toobuy 사용자 지정 도메인 이름을 하는 방법에 대해 알아봅니다."
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 70fb0e6e-8727-4cca-ba82-98a4d21586ff
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: 2ff61a3f27020516c917fe105ece99eb2a5754b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a>Azure Web Apps에 대한 사용자 지정 도메인 이름 구입

App Service 도메인(미리 보기)은 Azure에서 직접 관리되는 최상위 도메인입니다. 쉽게 toomanage 사용자 지정 도메인에 게 [Azure 웹 앱](app-service-web-overview.md)합니다. 이 자습서 toobuy 앱 서비스 도메인 및 DNS 할당 tooAzure 웹 응용 프로그램 이름을 지정 방법을 보여 줍니다.

이 문서는 Azure App Service(Web Apps, API Apps, Mobile Apps, Logic Apps)에 관한 내용입니다. Azure VM 또는 Azure 저장소에 대 한 참조 [할당 앱 서비스 도메인 tooAzure VM 또는 Azure 저장소](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/)합니다. Cloud Services의 경우 [Azure 클라우드 서비스에 대한 사용자 지정 도메인 이름 구성](../cloud-services/cloud-services-custom-domain-name-portal.md)을 참조하세요.

## <a name="prerequisites"></a>필수 조건

toocomplete이이 자습서:

* [App Service 앱을 만들거나](/azure/app-service/) 다른 자습서를 위해 만든 앱을 사용합니다.

## <a name="prepare-hello-app"></a>Hello 앱 준비

Azure 웹 앱에서 웹 앱의 사용자 지정 도메인 toouse [앱 서비스 계획](https://azure.microsoft.com/pricing/details/app-service/) 유료 계층 이어야 합니다 (**Shared**, **기본**, **표준**, 또는 **프리미엄**). 이 단계에서는 있습니다 지원 되는지 확인 해당 hello 웹 앱 hello에 가격 책정 계층입니다.

### <a name="sign-in-tooazure"></a>TooAzure에 로그인

열기 hello [Azure 포털](https://portal.azure.com) Azure 계정으로 로그인 합니다.

### <a name="navigate-toohello-app-in-hello-azure-portal"></a>Hello Azure 포털에서에서 toohello 응용 프로그램 이동

Hello 왼쪽된 메뉴에서 선택 **응용 프로그램 서비스**, hello 응용 프로그램의 hello 이름을 선택 합니다.

![포털 탐색 tooAzure 응용 프로그램](./media/app-service-web-tutorial-custom-domain/select-app.png)

Hello 앱 서비스 앱의 관리 페이지가 hello 표시합니다.  

### <a name="check-hello-pricing-tier"></a>가격 책정 계층 hello를 확인 합니다.

왼쪽 탐색 hello 응용 프로그램 페이지의 hello, toohello 스크롤하여 **설정** 선택한 섹션 **(앱 서비스 계획) 수직**합니다.

![강화 메뉴](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

hello 응용 프로그램의 현재 계층에 파란색 테두리가 강조 표시 됩니다. Toomake hello 앱 hello 중이 아닌지 확인 **무료** 계층입니다. 사용자 지정 DNS hello에서 지원 되지 않습니다 **무료** 계층입니다. 

![가격 책정 계층 확인](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

Hello 앱 서비스 계획이 없는 경우 **무료**닫기, hello **가격 책정 계층 선택** 페이지 및 너무 건너뛸[구입 hello 도메인](#buy-the-domain)합니다.

### <a name="scale-up-hello-app-service-plan"></a>앱 서비스 계획 hello 수직 확장

Hello 이미 계층 중 하나를 선택 (**Shared**, **기본**, **표준**, 또는 **프리미엄**). 

**선택**을 클릭합니다.

![가격 책정 계층 확인](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

Hello 알림을 다음 표시 되 면 hello 크기 조정 작업이 완료 되었습니다.

![크기 조정 작업 확인](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-hello-domain"></a>Hello 도메인 구입

### <a name="sign-in-tooazure"></a>TooAzure에 로그인
열기 hello [Azure 포털](https://portal.azure.com/) Azure 계정으로 로그인 합니다.

### <a name="launch-buy-domains"></a>도메인 구입 시작
Hello에 **웹 앱** 탭을 선택 하면 웹 앱의 hello 이름을 클릭 **설정**를 선택한 후 **사용자 지정 도메인이**
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

Hello에 **사용자 지정 도메인** 페이지 **도메인을 구입**합니다.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

### <a name="configure-hello-domain-purchase"></a>Hello 도메인 구매를 구성 합니다.

Hello에 **응용 프로그램 서비스 도메인** 페이지 hello **도메인에 대 한 검색** 상자 toobuy 유형과 원하는 hello 도메인 이름을 입력 합니다 `Enter`합니다. hello 제안 된 사용 가능한 도메인 아래에 표시 됩니다 바로 hello 텍스트 상자입니다. Toobuy 원하는 하나 이상의 도메인을 선택 합니다. 
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

Hello 클릭 **연락처 정보** hello 도메인의 연락처 정보 양식을 작성 하 고 있습니다. 완료 되 면 클릭 **확인** tooreturn toohello 응용 프로그램 서비스 도메인 페이지.
   
모든 필수 필드를 가능한 한 정확하게 기입해야 합니다. 연락처 정보에 대 한 잘못 된 데이터는 오류 toopurchase 도메인에서 발생할 수 있습니다. 

그런 다음 도메인에 대 한 hello 원하는 옵션을 선택 합니다. 다음 표에서 설명 하는 hello를 참조 하십시오.

| 설정 | 제안 값 | 설명 |
|-|-|-|
|자동 갱신 | **사용** | 매년 App Service 도메인을 자동으로 갱신합니다. 신용 카드 청구 동일한 구매 가격의 갱신 hello 시 hello 합니다. |
|개인 정보 보호 | 사용 | 너무 옵트인 hello 구매 가격에 포함 된 "개인 정보 보호" _무료로_ (레지스트리가 개인 정보 보호와 같은 지원 하지 않습니다는 최상위 도메인을 제외한 _. co.in_, _합니다. co.uk_등). |
| 기본 호스트 이름 할당 | **www** 및 **@** | Select hello 원하는 경우 호스트 이름 바인딩을 원하는입니다. Hello 도메인 구매 작업이 완료 되 면 웹 앱 선택 hello 호스트 이름에 액세스할 수 있습니다. Hello 웹 응용 프로그램 뒤에 있는 경우 [Azure 트래픽 관리자](https://azure.microsoft.com/services/traffic-manager/), hello 옵션 tooassign hello 루트 도메인에 표시 되지 않으면 (@), 트래픽 관리자가 A 레코드를 지원 하지 않기 때문입니다. Hello 도메인 구매를 완료 후 toohello 호스트 이름을 할당 변경 내용을 만들 수 있습니다. |

### <a name="accept-terms-and-purchase"></a>조건에 동의하고 구매

클릭 **약관** tooreview hello 용어 및 hello 요금이 클릭 **구입**합니다.

> [!NOTE]
> Azure DNS toohost hello 도메인을 사용 하는 응용 프로그램 서비스 도메인. Toohello 도메인 등록 요금 뿐만 아니라 Azure DNS에 대 한 사용 요금이 부과 됩니다. 자세한 내용은 [Azure DNS 가격 책정](https://azure.microsoft.com/pricing/details/dns/)을 참조하세요.
>
>

Hello에 다시 **응용 프로그램 서비스 도메인** 페이지 **확인**합니다. Hello 작업이 진행 중에서 상태인 동안 다음 알림 hello를 표시 됩니다.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-hello-hostnames"></a>테스트 hello 호스트 이름

기본 호스트 이름을 tooyour 웹 앱에 할당 한 경우 선택한 각 호스트 이름에 대 한 성공 알림을 표시 합니다. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

Hello에 선택한 hello 호스트 이름이 표시 **사용자 지정 도메인** 페이지 hello **Hostnames** 섹션. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

tootest hello 호스트 이름, hello 브라우저에서 toohello 나열 된 호스트를 이동 합니다. Too_kontoso.net_를 이동해 보십시오 스크린 샷, 앞의 hello hello 예제 및 _www.kontoso.net_합니다.

## <a name="assign-hostnames-tooweb-app"></a>호스트 이름을 tooweb 응용 프로그램 할당

하나 tooassign 하지 않으려는 hello 동안 보다 많은 기본 호스트 이름 tooyour 웹 앱 프로세스를 구입 하거나 나열 되지 tooassign 호스트 이름을 사용 해야 할 경우, 언제 든 지 한 호스트 이름을 지정할 수 있습니다.

또한 응용 프로그램 서비스 도메인 tooany hello에에서 호스트 이름이 다른 웹 앱을 할당할 수 있습니다. hello 단계에 따라 응용 프로그램 서비스 도메인 hello 및 hello 웹 앱 toohello 속한 여부 동일한 구독 합니다.

- 다른 구독: hello 응용 프로그램 서비스 도메인 toohello 웹 응용 프로그램 외부에서 구매한 도메인에서 사용자 지정 DNS 레코드를 매핑합니다. 추가 사용자 지정 dns 정보 tooan 응용 프로그램 서비스 도메인 이름, 참조 [사용자 지정 DNS 레코드 관리](#custom)합니다. toomap 외부 구매한 도메인 tooa 웹 응용 프로그램 참조 [는 기존 사용자 지정 DNS 이름 tooAzure 웹 응용 프로그램을 매핑할](app-service-web-tutorial-custom-domain.md)합니다. 
- 동일한 구독: 사용 하 여 hello 단계를 수행 합니다.

### <a name="launch-add-hostname"></a>호스트 이름 추가 시작
Hello에 **응용 프로그램 서비스** 페이지, tooassign 호스트 이름, 선택 하려는 웹 앱 이름 선택 hello **설정**를 선택한 후 **사용자 지정 도메인**합니다.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

도메인을 구입한 hello에 나열 되어 있는지 확인 **응용 프로그램 서비스 도메인** 섹션 하지만 선택 하지 마십시오. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> 동일한 구독 hello 웹 앱에 표시 된 hello에서 모든 응용 프로그램 서비스 도메인 **사용자 지정 도메인** 페이지. 도메인은 hello 웹 앱 구독에 있지만 hello 웹 앱에서 볼 수 없는 경우 **사용자 지정 도메인** 페이지, hello를 다시 열어 보십시오 **사용자 지정 도메인** 페이지 또는 hello 웹 페이지를 새로 고칩니다. 또한, 진행률 또는 생성 실패에 대 한 hello 위쪽 hello Azure 포털의 알림 벨 hello를 확인 합니다.
>
>

**호스트 이름 추가**를 선택합니다.

### <a name="configure-hostname"></a>호스트 이름 구성
Hello에 **호스트 이름 추가** 대화 상자에서 응용 프로그램 서비스 도메인 또는 모든 하위 도메인의 형식 hello 정규화 된 도메인 이름입니다. 예:

- kontoso.net
- www.kontoso.net
- abc.kontoso.net

완료되면 **유효성 검사**를 선택합니다. hello hostname 레코드 종류 자동으로 선택 됩니다.

**호스트 이름 추가**를 선택합니다.

Hello 작업이 완료 되 면 호스트 이름을 할당 하는 hello에 대 한 성공 알림을 표시 합니다.  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a>호스트 이름 추가 닫기
Hello에 **호스트 이름 추가** 페이지에서 다른 호스트 이름 tooyour 웹 앱을 원하는 대로 지정 합니다. 완료 되 면 닫습니다 hello **호스트 이름 추가** 페이지.

이제 응용 프로그램에서 새로 할당 된 hello hostname(s) 표시 **사용자 지정 도메인** 페이지.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-hello-hostnames"></a>테스트 hello 호스트 이름

Hello 브라우저에서 toohello 나열 된 호스트를 이동 합니다. Hello 스크린 샷 앞에 hello 예에서 too_abc.kontoso.net_ 탐색 하십시오.

<a name="custom" />

## <a name="manage-custom-dns-records"></a>사용자 지정 DNS 레코드 관리

Azure에서 App Service 도메인에 대한 DNS 레코드는 [Azure DNS](https://azure.microsoft.com/services/dns/)를 사용하여 관리됩니다. 외부에서 구매한 도메인처럼 DNS 레코드를 추가, 제거 및 업데이트할 수 있습니다.

### <a name="open-app-service-domain"></a>App Service 도메인 열기

Hello hello 왼쪽된 메뉴에서 Azure 포털에서에서 선택 **더 서비스** > **응용 프로그램 서비스 도메인**합니다.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

Hello 도메인 toomanage를 선택 합니다. 

### <a name="access-dns-zone"></a>DNS 영역 액세스

Hello 도메인의 왼쪽된 메뉴에서 선택 **DNS 영역**합니다.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

Hello 열립니다 [DNS 영역](../dns/dns-zones-records.md) Azure DNS에서 서비스 응용 프로그램 도메인의 페이지입니다. 방법에 대 한 tooedit DNS 레코드 참조 [toomanage DNS 영역에 Azure 포털을 hello 어떻게](../dns/dns-operations-dnszones-portal.md)합니다.

## <a name="cancel-purchase-delete-domain"></a>구매 취소(도메인 삭제)

응용 프로그램 서비스 도메인 hello를 구입한 후 전체 환불에 대 한 구매 toocancel 5 일 수 있습니다. 5 일 후 응용 프로그램 서비스 도메인 hello를 삭제할 수 있지만 환불을 받을 수 없습니다.

### <a name="open-app-service-domain"></a>App Service 도메인 열기

Hello hello 왼쪽된 메뉴에서 Azure 포털에서에서 선택 **더 서비스** > **응용 프로그램 서비스 도메인**합니다.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

선택 hello 도메인 tooyou toocancel 하거나 삭제 합니다. 

### <a name="delete-hostname-bindings"></a>호스트 이름 바인딩 삭제

Hello 도메인의 왼쪽된 메뉴에서 선택 **호스트 이름 바인딩을**합니다. 모든 Azure 서비스에서 호스트 이름 바인딩은 hello 여기에 나열 됩니다.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

모든 호스트 이름 바인딩을 삭제 될 때까지 hello 응용 프로그램 서비스 도메인을 삭제할 수 없습니다.

**...** > **삭제**를 선택하여 각 호스트 이름 바인딩을 삭제합니다. 모든 hello 바인딩을 삭제 된 후 선택 **저장**합니다.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a>취소 또는 삭제

Hello 도메인의 왼쪽된 메뉴에서 선택 **개요**합니다. 

구입한 hello 도메인에 hello 취소 기간이 지나지 않은, 선택 **구입을 취소**합니다. 그렇지 않으면 **삭제** 단추가 대신 표시됩니다. 환불을 선택 하지 않고 toodelete hello 도메인 **삭제**합니다.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

선택 **확인** tooconfirm hello 작업 합니다. Tooproceed 않으려면 hello 확인 대화 상자 외부의 아무 곳 이나 클릭 합니다.

Hello 도메인은 구독에서 해제 한 후 모든 사용자에 사용할 수 있는 hello 작업이 완료 되 면 다시 toopurchase 합니다. 
