---
title: "aaaMigrate active DNS 이름을 tooAzure 앱 서비스 | Microsoft Docs"
description: "Toomigrate tooa 이미 할당 되어 있는 사용자 지정 DNS 도메인 이름을 사이트 tooAzure 앱 서비스 가동 중지 시간 없이 라이브 하는 방법에 대해 알아봅니다."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
tags: top-support-issue
ms.assetid: 10da5b8a-1823-41a3-a2ff-a0717c2b5c2d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: cephalin
ms.openlocfilehash: fbc4cc30dcb87efb2e867cb65c5404b667661e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-active-dns-name-tooazure-app-service"></a>마이그레이션 활성 DNS 이름 tooAzure 앱 서비스

이 문서에서는 어떻게 toomigrate active DNS 이름이 너무[Azure 앱 서비스](../app-service/app-service-value-prop-what-is.md) 가동 중지 시간 없이 합니다.

라이브 사이트 및 해당 DNS 도메인 이름 tooApp 서비스를 마이그레이션하는 경우 DNS 이름을 이미 제공 하는 중인 라이브 트래픽입니다. Hello 활성 DNS 이름 tooyour 앱 서비스 앱을 미리 바인딩하여 hello 마이그레이션하는 동안 DNS 확인에 가동 중지 시간을 피할 수 있습니다.

DNS 확인에 가동 중지 시간에 대 한 걱정 모르겠으면 참조 [는 기존 사용자 지정 DNS 이름 tooAzure 웹 응용 프로그램을 매핑할](app-service-web-tutorial-custom-domain.md)합니다.

## <a name="prerequisites"></a>필수 조건

이 방법 toocomplete:

- [App Service 앱이 무료 계층에 있지 않은지 확인합니다](app-service-web-tutorial-custom-domain.md#checkpricing).

## <a name="bind-hello-domain-name-preemptively"></a>여기서 hello 도메인 이름 바인딩

여기서 사용자 지정 도메인을 바인딩하는 경우 DNS 레코드를 변경 하기 전에 hello 다음 중 둘 다 수행 합니다.

- 도메인 소유권 확인
- 앱에 대 한 hello 도메인 이름을 사용 하도록 설정

Hello 이전 사이트 toohello 앱 서비스 앱에서에서 사용자 지정 DNS 이름을 마지막으로 마이그레이션하면 됩니다 가동 중지 시간 없이 DNS 확인에 있습니다.

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a>도메인 확인 레코드 만들기

tooverify 도메인 소유권을 TXT 추가 기록 합니다. hello TXT 레코드에서 매핑합니다 _awverify.&lt; 하위 도메인 >_ too_&lt;응용 프로그램 이름 >. azurewebsites.net_ 합니다. 

TXT 레코드 필요한 hello hello toomigrate DNS 레코드에 따라 달라 집니다. 예제를 보려면 다음 표는 hello (`@` 일반적으로 나타내는 hello 루트 도메인):  

| DNS 레코드 예제 | TXT 호스트 | TXT 값 |
| - | - | - |
| @(루트) | _awverify_ | _&lt;appname>.azurewebsites.net_ |
| www(하위) | _awverify.www_ | _&lt;appname>.azurewebsites.net_ |
| \*(와일드카드) | _awverify.\*_ | _&lt;appname>.azurewebsites.net_ |

DNS 레코드 페이지의 note hello 레코드 종류 hello toomigrate 원하는 DNS 이름입니다. App Service는 CNAME 및 A 레코드로부터의 매핑을 지원합니다.

### <a name="enable-hello-domain-for-your-app"></a>앱에 대 한 hello 도메인을 사용 하도록 설정

Hello에 [Azure 포털](https://portal.azure.com)hello hello 응용 프로그램 페이지의 왼쪽된 탐색에서 선택 **사용자 지정 도메인**합니다. 

![사용자 지정 도메인 메뉴](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

Hello에 **사용자 지정 도메인** 페이지, 선택 hello  **+**  아이콘 다음 너무**호스트 이름 추가**합니다.

![호스트 이름 추가](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

형식 hello 정규화 된 도메인 이름에 대 한 hello TXT 레코드를와 같은 추가 `www.contoso.com`합니다. 와일드 카드 도메인에 대 한 (같은 \*. contoso.com)을 hello 와일드 카드 도메인 일치 하는 모든 DNS 이름을 사용할 수 있습니다. 

**유효성 검사**를 선택합니다.

hello **호스트 이름 추가** 단추가 활성화 됩니다. 

다음 사항을 확인 **Hostname 레코드 종류** toohello DNS 레코드 종류 toomigrate 원하는 설정 됩니다.

**호스트 이름 추가**를 선택합니다.

![DNS 이름 toohello 앱 추가](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

Hello 새 호스트 이름 toobe hello 응용 프로그램에 반영 약간의 시간이 걸릴 수 있습니다 **사용자 지정 도메인** 페이지. Hello 브라우저 tooupdate hello 데이터를 새로 고쳐 보십시오.

![추가된 CNAME 레코드](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

이제 Azure 앱에서 사용자 지정 DNS 이름을 사용할 수 있도록 지정되었습니다. 

## <a name="remap-hello-active-dns-name"></a>Hello 활성 DNS 이름을 다시 매핑

hello 것만 왼쪽된 toodo은 다시 매핑에 활성 DNS 레코드 toopoint tooApp 서비스입니다. 오른쪽 이제 여전히 가리키도록 tooyour 이전 사이트입니다.

<a name="info"></a>

### <a name="copy-hello-apps-ip-address-a-record-only"></a>Hello 응용 프로그램의 IP 주소 (A 레코드만 해당)를 복사 합니다.

CNAME 레코드를 다시 매핑하는 경우 이 섹션을 건너뛰세요. 

hello에 표시 되어 hello 앱 서비스 앱의 외부 IP 주소가 필요한 tooremap A 레코드 **사용자 지정 도메인** 페이지.

닫기 hello **호스트 이름 추가** 페이지를 선택 하 여 **X** hello 오른쪽 위 모퉁이에 있습니다. 

Hello에 **사용자 지정 도메인** 페이지, hello 응용 프로그램의 IP 주소를 복사 합니다.

![포털 탐색 tooAzure 응용 프로그램](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-hello-dns-record"></a>Hello DNS 레코드 업데이트

도메인 공급자의 DNS 레코드 페이지 hello에 다시 hello DNS 레코드 tooremap를 선택 합니다.

Hello에 대 한 `contoso.com` 루트 도메인 예, 다음 표에 hello에 hello 예제와 같은 hello A 또는 CNAME 레코드를 다시 매핑해야 합니다. 

| FQDN 예 | 레코드 형식 | 호스트 | 값 |
| - | - | - | - |
| contoso.com(루트) | A | `@` | IP 주소를 [복사 hello 응용 프로그램의 IP 주소](#info) |
| www.contoso.com(하위) | CNAME | `www` | _&lt;appname>.azurewebsites.net_ |
| \*.contoso.com(와일드카드) | CNAME | _\*_ | _&lt;appname>.azurewebsites.net_ |

설정을 저장합니다.

DNS 쿼리 DNS 전파가 발생 직후 tooyour 앱 서비스 앱 확인을 시작 해야 합니다.

## <a name="next-steps"></a>다음 단계

사용자 지정 SSL toobind tooApp 서비스 인증서 하는 방법에 대해 알아봅니다.

> [!div class="nextstepaction"]
> [기존 사용자 지정 SSL 인증서 tooAzure 웹 응용 프로그램 바인딩](app-service-web-tutorial-custom-ssl.md)
