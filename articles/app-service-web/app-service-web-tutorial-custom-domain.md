---
title: "기존 사용자 지정 DNS aaaMap tooAzure 웹 앱 이름을 | Microsoft Docs"
description: "Tooadd 기존 사용자 지정 DNS 도메인 (베 니 티 도메인) tooa 웹 앱, 모바일 앱 백 엔드, 또는 Azure 앱 서비스에서 API 앱 이름 지정 방법을 알아봅니다."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2c4eea3c56c758ca11355554321ffa52dd2c6b9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="map-an-existing-custom-dns-name-tooazure-web-apps"></a>지도 기존 사용자 지정 DNS 이름 tooAzure 웹 응용 프로그램

[Azure Web Apps](app-service-web-overview.md)는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다. 이 자습서는 기존 사용자 지정 DNS toomap tooAzure 웹 응용 프로그램 이름 지정 방법을 보여 줍니다.

![포털 탐색 tooAzure 응용 프로그램](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * CNAME 레코드를 사용하여 하위 도메인(예: `www.contoso.com`) 매핑
> * A 레코드를 사용하여 루트 도메인(예: `contoso.com`) 매핑
> * CNAME 레코드를 사용하여 와일드카드 도메인(예: `*.contoso.com`) 매핑
> * 스크립트로 도메인 매핑 자동화

하나를 사용할 수는 **CNAME 레코드** 또는 **레코드** toomap 사용자 지정 DNS tooApp 서비스 이름을 지정 합니다. 

> [!NOTE]
> 루트 도메인(예: `contoso.com`)을 제외한 모든 사용자 지정 DNS 이름에 대해 CNAME을 사용하는 것이 좋습니다.

toomigrate 라이브 사이트 및 서비스의 DNS 도메인 이름 tooApp 참조 [활성 DNS 이름 tooAzure 앱 서비스를 마이그레이션할](app-service-custom-domain-name-migrate.md)합니다.

## <a name="prerequisites"></a>필수 조건

toocomplete이이 자습서:

* [App Service 앱을 만들거나](/azure/app-service/) 다른 자습서를 위해 만든 앱을 사용합니다.
* 도메인 이름을 구매 하 고 (예: GoDaddy) 도메인 공급자에 대 한 액세스 toohello DNS 레지스트리에 있는지 확인 합니다.

  에 대 한 DNS 항목 예를 들어 tooadd `contoso.com` 및 `www.contoso.com`, hello에 대 한 수 tooconfigure hello DNS 설정을 해야 `contoso.com` 루트 도메인.

  > [!NOTE]
  > 기존 도메인 이름 지정을 고려 하십시오. 없는 경우 [Azure 포털 hello를 사용 하 여 도메인을 구입](custom-dns-web-site-buydomains-web-app.md)합니다. 

## <a name="prepare-hello-app"></a>Hello 앱 준비

사용자 지정 DNS 이름 tooa 웹 앱의 경우 hello 웹 응용 프로그램의 toomap [앱 서비스 계획](https://azure.microsoft.com/pricing/details/app-service/) 유료 계층 이어야 합니다 (**Shared**, **기본**, **표준**, 또는  **프리미엄**). 이 단계에서는 수 있도록 해당 hello hello 앱이 앱 서비스 가격 책정 계층을 지원 합니다.

### <a name="sign-in-tooazure"></a>TooAzure에 로그인

열기 hello [Azure 포털](https://portal.azure.com) Azure 계정으로 로그인 합니다.

### <a name="navigate-toohello-app-in-hello-azure-portal"></a>Hello Azure 포털에서에서 toohello 응용 프로그램 이동

Hello 왼쪽된 메뉴에서 선택 **응용 프로그램 서비스**, hello 응용 프로그램의 hello 이름을 선택 합니다.

![포털 탐색 tooAzure 응용 프로그램](./media/app-service-web-tutorial-custom-domain/select-app.png)

Hello 앱 서비스 앱의 관리 페이지가 hello 표시합니다.  

<a name="checkpricing"></a>

### <a name="check-hello-pricing-tier"></a>가격 책정 계층 hello를 확인 합니다.

왼쪽 탐색 hello 응용 프로그램 페이지의 hello, toohello 스크롤하여 **설정** 선택한 섹션 **(앱 서비스 계획) 수직**합니다.

![강화 메뉴](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

hello 응용 프로그램의 현재 계층에 파란색 테두리가 강조 표시 됩니다. Toomake hello 앱 hello 중이 아닌지 확인 **무료** 계층입니다. 사용자 지정 DNS hello에서 지원 되지 않습니다 **무료** 계층입니다. 

![가격 책정 계층 확인](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

Hello 앱 서비스 계획이 없는 경우 **무료**닫기, hello **가격 책정 계층 선택** 페이지 및 너무 건너뛸[CNAME 레코드 매핑할](#cname)합니다.

<a name="scaleup"></a>

### <a name="scale-up-hello-app-service-plan"></a>앱 서비스 계획 hello 수직 확장

Hello 이미 계층 중 하나를 선택 (**Shared**, **기본**, **표준**, 또는 **프리미엄**). 

**선택**을 클릭합니다.

![가격 책정 계층 확인](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

Hello 알림을 다음 표시 되 면 hello 크기 조정 작업이 완료 되었습니다.

![크기 조정 작업 확인](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a>CNAME 레코드 매핑

Hello 자습서 예제에서는 hello에 대 한 CNAME 레코드를 추가 하면 `www` 하위 도메인 (예를 들어 `www.contoso.com`).

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a>Hello CNAME 레코드 만들기

CNAME 레코드 toomap 하위 도메인 toohello 앱의 기본 호스트 이름이 추가 (`<app_name>.azurewebsites.net`).

Hello에 대 한 `www.contoso.com` 도메인 예 hello 이름을 매핑하는 CNAME 레코드를 추가 `www` 너무`<app_name>.azurewebsites.net`합니다.

Hello CNAME을 추가한 후 다음 예제는 hello 같이 hello DNS 레코드 페이지 표시 됩니다.

![포털 탐색 tooAzure 응용 프로그램](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-hello-cname-record-mapping-in-azure"></a>Azure의 hello CNAME 레코드 매핑을 사용 합니다.

Hello hello Azure 포털의에서 왼쪽 hello 앱 페이지 탐색, 선택 **사용자 지정 도메인**합니다. 

![사용자 지정 도메인 메뉴](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

Hello에 **사용자 지정 도메인** 페이지 hello 응용 프로그램의 정규화 된 사용자 지정 DNS 이름 hello 추가 (`www.contoso.com`) toohello 목록입니다.

선택 hello  **+**  아이콘 다음 너무**호스트 이름 추가**합니다.

![호스트 이름 추가](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

형식 hello 정규화 된 도메인 이름에 대 한 CNAME 레코드를와 같은 추가 `www.contoso.com`합니다. 

**유효성 검사**를 선택합니다.

hello **호스트 이름 추가** 단추가 활성화 됩니다. 

다음 사항을 확인 **Hostname 레코드 종류** 너무 설정**CNAME (www.example.com 또는 모든 하위 도메인)**합니다.

**호스트 이름 추가**를 선택합니다.

![DNS 이름 toohello 앱 추가](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

Hello 새 호스트 이름 toobe hello 응용 프로그램에 반영 약간의 시간이 걸릴 수 있습니다 **사용자 지정 도메인** 페이지. Hello 브라우저 tooupdate hello 데이터를 새로 고쳐 보십시오.

![추가된 CNAME 레코드](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

단계를 수행 하지 하는 경우 또는 어딘가에 보시 겠어요 hello hello 페이지 맨 아래에 확인 오류 이전에 표시 합니다.

![확인 오류](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a>A 레코드 매핑

Hello 자습서 예제에서는 hello 루트 도메인에 대 한 A 레코드를 추가 하면 (예를 들어 `contoso.com`). 

<a name="info"></a>

### <a name="copy-hello-apps-ip-address"></a>Hello 응용 프로그램의 IP 주소를 복사 합니다.

toomap A 레코드를 hello 응용 프로그램의 외부 IP 주소를 해야합니다. Hello 앱에서이 IP 주소를 찾을 수 있습니다 **사용자 지정 도메인** hello Azure 포털에서에서 페이지입니다.

Hello hello Azure 포털의에서 왼쪽 hello 앱 페이지 탐색, 선택 **사용자 지정 도메인**합니다. 

![사용자 지정 도메인 메뉴](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

Hello에 **사용자 지정 도메인** 페이지, hello 응용 프로그램의 IP 주소를 복사 합니다.

![포털 탐색 tooAzure 응용 프로그램](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-a-record"></a>Hello A 레코드 만들기

앱 서비스에 필요한 toomap A 레코드 tooan 앱 **두** DNS 레코드:

- **A** toomap toohello 응용 프로그램의 IP 주소를 기록해 둡니다.
- A **TXT** toomap toohello 앱의 기본 호스트 이름이 기록 `<app_name>.azurewebsites.net`합니다. 응용 프로그램 서비스 구성 타임 tooverify hello 사용자 지정 도메인을 소유 하에이 레코드를 사용 합니다. App Service에서 사용자 지정 도메인의 유효성을 검사하고 해당 도메인을 구성한 후에는 이 TXT 레코드를 삭제할 수 있습니다. 

Hello에 대 한 `contoso.com` 도메인 예 toohello 표 다음에 따라 hello A와 TXT 레코드를 만듭니다 (`@` 일반적으로 나타내는 hello 루트 도메인). 

| 레코드 형식 | 호스트 | 값 |
| - | - | - |
| A | `@` | IP 주소를 [복사 hello 응용 프로그램의 IP 주소](#info) |
| TXT | `@` | `<app_name>.azurewebsites.net` |

Hello 레코드를 추가 하는 경우 다음 예제는 hello 같이 hello DNS 레코드 페이지 표시 됩니다.

![DNS 레코드 페이지](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-hello-a-record-mapping-in-hello-app"></a>Hello 응용 프로그램에서 레코드 매핑 hello를 사용 하도록 설정

Hello 앱에 다시 **사용자 지정 도메인** hello Azure 포털에서에서 페이지 hello 정규화 된 사용자 지정 DNS 이름을 추가 합니다 (예를 들어 `contoso.com`) toohello 목록입니다.

선택 hello  **+**  아이콘 다음 너무**호스트 이름 추가**합니다.

![호스트 이름 추가](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

형식 hello 정규화 된 도메인 이름에 대 한 hello A 레코드를와 같은 구성 `contoso.com`합니다.

**유효성 검사**를 선택합니다.

hello **호스트 이름 추가** 단추가 활성화 됩니다. 

다음 사항을 확인 **Hostname 레코드 종류** 너무 설정 되어**레코드 (example.com)**합니다.

**호스트 이름 추가**를 선택합니다.

![DNS 이름 toohello 앱 추가](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

Hello 새 호스트 이름 toobe hello 응용 프로그램에 반영 약간의 시간이 걸릴 수 있습니다 **사용자 지정 도메인** 페이지. Hello 브라우저 tooupdate hello 데이터를 새로 고쳐 보십시오.

![추가된 A 레코드](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

단계를 수행 하지 하는 경우 또는 어딘가에 보시 겠어요 hello hello 페이지 맨 아래에 확인 오류 이전에 표시 합니다.

![확인 오류](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a>와일드카드 도메인 매핑

매핑할 hello 자습서 예제에서는 [와일드 카드 DNS 이름이](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (예를 들어 `*.contoso.com`) toohello CNAME 레코드를 추가 하 여 앱 서비스 앱. 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a>Hello CNAME 레코드 만들기

CNAME 레코드 toomap 와일드 카드 이름 toohello 앱의 기본 호스트 이름이 추가 (`<app_name>.azurewebsites.net`).

Hello에 대 한 `*.contoso.com` 도메인 예 hello CNAME 레코드는 hello 이름 매핑됩니다 `*` 너무`<app_name>.azurewebsites.net`합니다.

Hello CNAME 추가 되 면 다음 예제는 hello 같이 hello DNS 레코드 페이지 표시 됩니다.

![포털 탐색 tooAzure 응용 프로그램](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-hello-cname-record-mapping-in-hello-app"></a>Hello 응용 프로그램에서 hello CNAME 레코드 매핑을 사용 합니다.

이제 hello 와일드 카드 이름 toohello 앱 일치 하는 모든 하위 도메인을 추가할 수 있습니다 (예를 들어 `sub1.contoso.com` 및 `sub2.contoso.com` 일치 `*.contoso.com`). 

Hello hello Azure 포털의에서 왼쪽 hello 앱 페이지 탐색, 선택 **사용자 지정 도메인**합니다. 

![사용자 지정 도메인 메뉴](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

선택 hello  **+**  아이콘 다음 너무**호스트 이름 추가**합니다.

![호스트 이름 추가](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

Hello 와일드 카드 도메인에 일치 하는 정규화 된 도메인 이름을 입력 (예를 들어 `sub1.contoso.com`)를 선택한 후 **유효성 검사**합니다.

hello **호스트 이름 추가** 단추가 활성화 됩니다. 

다음 사항을 확인 **Hostname 레코드 종류** 너무 설정**CNAME 레코드 (www.example.com 또는 모든 하위 도메인)**합니다.

**호스트 이름 추가**를 선택합니다.

![DNS 이름 toohello 앱 추가](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

Hello 새 호스트 이름 toobe hello 응용 프로그램에 반영 약간의 시간이 걸릴 수 있습니다 **사용자 지정 도메인** 페이지. Hello 브라우저 tooupdate hello 데이터를 새로 고쳐 보십시오.

선택 hello  **+**  아이콘 다시 tooadd hello 와일드 카드 도메인 일치 하는 다른 호스트 이름입니다. 예를 들어 `sub2.contoso.com`을 추가합니다.

![추가된 CNAME 레코드](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a>브라우저에서 테스트

찾아보기 이전에 구성 된 toohello DNS 이름 (예를 들어 `contoso.com`, `www.contoso.com`, `sub1.contoso.com`, 및 `sub2.contoso.com`).

![포털 탐색 tooAzure 응용 프로그램](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a>스크립트를 사용하여 자동화

Hello를 사용 하 여 스크립트를 사용 하는 사용자 지정 도메인의 관리를 자동화할 수 [Azure CLI](/cli/azure/install-azure-cli) 또는 [Azure PowerShell](/powershell/azure/overview)합니다. 

### <a name="azure-cli"></a>Azure CLI 

다음 명령을 hello는 구성 된 사용자 지정 DNS 이름 tooan 앱 서비스 앱을 추가 합니다. 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

자세한 내용은 참조 [tooa 웹 응용 프로그램 사용자 지정 도메인을 매핑할](scripts/app-service-cli-configure-custom-domain.md)합니다. 

### <a name="azure-powershell"></a>Azure PowerShell 

다음 명령을 hello는 구성 된 사용자 지정 DNS 이름 tooan 앱 서비스 앱을 추가 합니다. 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

자세한 내용은 참조 [tooa 웹 응용 프로그램 사용자 지정 도메인을 할당](scripts/app-service-powershell-configure-custom-domain.md)합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서 학습한 방법은 다음과 같습니다.

> [!div class="checklist"]
> * CNAME 레코드를 사용하여 하위 도메인 매핑
> * A 레코드를 사용하여 루트 도메인 매핑
> * CNAME 레코드를 사용하여 와일드카드 도메인 매핑
> * 스크립트로 도메인 매핑 자동화

다음 자습서 toolearn toohello 진행 방법을 toobind 사용자 지정 SSL 인증서 tooa 웹 앱입니다.

> [!div class="nextstepaction"]
> [기존 사용자 지정 SSL 인증서 tooAzure 웹 응용 프로그램 바인딩](app-service-web-tutorial-custom-ssl.md)
