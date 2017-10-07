---
title: "CDN tooan Azure 앱 서비스 aaaAdd | Microsoft Docs"
description: "네트워크 CDN (콘텐츠 배달) tooan Azure 앱 서비스 toocache를 추가 하 고 hello 전 세계 닫기 tooyour 고객 서버에서 정적 파일을 제공 합니다."
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 88b7fd884517279064472b804a6d1dc2921cbd24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-content-delivery-network-cdn-tooan-azure-app-service"></a>추가 네트워크 CDN (콘텐츠 배달) tooan Azure 앱 서비스

[Azure 네트워크 CDN (콘텐츠 배달)](../cdn/cdn-overview.md) 전략적으로 배치 된 위치 tooprovide 최대 처리량 toousers 콘텐츠를 제공 하기 위한 정적 웹 콘텐츠를 캐시 합니다. hello CDN은 웹 응용 프로그램에 서버 부하를 줄어듭니다. 이 자습서에서는 어떻게 tooadd Azure CDN tooa [Azure 앱 서비스의 웹 앱](app-service-web-overview.md)합니다. 

Hello 사이트의 홈 페이지 hello 샘플 정적 HTML 사용 하는 다음과 같습니다.

![샘플 앱 홈 페이지](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

학습할 내용:

> [!div class="checklist"]
> * CDN 끝점 만들기
> * 캐시된 자산 새로 고침
> * 사용 하 여 쿼리 문자열 캐시 toocontrol 버전입니다.
> * Hello CDN 끝점에 대 한 사용자 지정 도메인을 사용 합니다.

## <a name="prerequisites"></a>필수 조건

toocomplete이이 자습서:

- [Git 설치](https://git-scm.com/)
- [Azure CLI 2.0 설치](https://docs.microsoft.com/cli/azure/install-azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-web-app"></a>Hello 웹 앱 만들기

사용 합니다, 따라 hello toocreate hello 웹 앱 [정적 HTML 퀵 스타트](app-service-web-get-started-html.md) hello를 통해 **찾아보기 toohello 앱** 단계입니다.

### <a name="have-a-custom-domain-ready"></a>사용자 지정 도메인 준비

toocomplete hello 사용자 지정 도메인 단계가이 자습서의 사용자 지정 도메인 tooown 필요 하 고이 도메인 공급자 (예: GoDaddy)에 대 한 액세스 tooyour DNS 레지스트리는 합니다. 에 대 한 DNS 항목 예를 들어 tooadd `contoso.com` 및 `www.contoso.com`, hello에 대 한 액세스 tooconfigure hello DNS 설정이 있어야 `contoso.com` 루트 도메인.

도메인 이름이 없는 경우 다음과 같은 hello [앱 서비스 도메인 자습서](custom-dns-web-site-buydomains-web-app.md) 사용 하 여 도메인 toopurchase hello Azure 포털입니다. 

## <a name="log-in-toohello-azure-portal"></a>Azure 포털 toohello에 로그인

브라우저를 열고 탐색 toohello [Azure 포털](https://portal.azure.com)합니다.

## <a name="create-a-cdn-profile-and-endpoint"></a>CDN 프로필 및 끝점 만들기

왼쪽 탐색 hello, 선택 **응용 프로그램 서비스**, 다음 hello에서 만든 hello 앱을 선택 하 고 [정적 HTML 퀵 스타트](app-service-web-get-started-html.md)합니다.

![Hello 포털에서 앱 서비스 앱 선택](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

Hello에 **앱 서비스** 페이지 hello에서 **설정** 섹션에서 **네트워킹 > 응용 프로그램에 대 한 Azure CDN 구성**합니다.

![Hello 포털에서 CDN을 선택 합니다.](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

Hello에 **Azure 콘텐츠 배달 네트워크** 페이지를 hello 제공 **새 끝점** hello 테이블에 지정 된 대로 설정 합니다.

![Hello 포털에서 프로필 및 끝점 만들기](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| 설정 | 제안 값 | 설명 |
| ------- | --------------- | ----------- |
| **CDN 프로필** | myCDNProfile | 선택 **새로 만들기** toocreate CDN 프로필입니다. CDN 프로필 hello로 CDN 끝점의 컬렉션은 같은 가격 책정 계층입니다. |
| **가격 책정 계층** | Standard Akamai | hello [가격 책정 계층](../cdn/cdn-overview.md#azure-cdn-features) hello 공급자 및 사용 가능한 기능을 지정 합니다. 이 자습서에서는 표준 Akamai를 사용합니다. |
| **CDN 끝점 이름** | Hello azureedge.net 도메인에서 고유한 이름 | Hello 도메인에서 캐시 된 리소스에 액세스 하면  *\<endpointname >. azureedge.net*합니다.

**만들기**를 선택합니다.

Azure는 hello 프로필 및 끝점을 만듭니다. hello에 새 끝점의 hello 표시 **끝점** 목록에서 같은 페이지 hello 그리고 hello 상태가 프로 비전 될 때 **실행**합니다.

![목록의 새 끝점](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-hello-cdn-endpoint"></a>테스트 hello CDN 끝점

Verizon 가격 책정 계층을 선택한 경우 끝점 전파를 위해 일반적으로 약 90분이 걸립니다. Akamai의 경우 전파하는 데 몇 분이 걸립니다.

hello 샘플 응용 프로그램에는 `index.html` 파일 및 *css*, *img*, 및 *js* 다른 정적 자산을 포함 하는 폴더입니다. 이 모든 파일에 대 한 경로 콘텐츠 hello hello CDN 끝점에서 동일한 hello 합니다. 예를 들어 hello 다음 Url의 액세스 hello *bootstrap.css* hello에 대 한 파일 *css* 폴더:

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

Url 브라우저 toohello를 이동 합니다.

```
http://<endpointname>.azureedge.net/index.html
```

![CDN에서 제공되는 샘플 앱 홈 페이지](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 Hello Azure 웹 앱의 앞부분에 나오는 실행 하는 동일한 페이지를 참조 합니다. Azure CDN이 hello 원본 웹 앱의 자산을 검색 하 고 hello CDN 끝점에서 제공 됩니다.

tooensure이이 페이지 hello CDN에서 새로 고침 hello 페이지에에서 캐시 됩니다. 두 개에 대 한 hello 같은 자산의 경우에 따라 필요한 hello CDN toocache hello 요청한 콘텐츠를 요청 합니다.

Azure CDN 프로필 및 끝점을 만드는 방법에 대한 자세한 내용은 [Azure CDN 시작](../cdn/cdn-create-new-endpoint.md)을 참조하세요.

## <a name="purge-hello-cdn"></a>CDN hello를 제거 합니다.

hello CDN에는 hello 활성 시간 (TTL) 구성에 따라 hello 원본 웹 앱에서 리소스를 주기적으로 새로 고쳐집니다. hello 기본 TTL은 7 일입니다.

때때로 hello-TTL 만료 전에 toorefresh hello CDN 예를 들어 때 필요한 업데이트 된 콘텐츠 toohello 웹 앱을 배포 합니다. 새로 고침 tootrigger hello CDN 리소스를 수동으로 제거할 수 있습니다. 

Hello 자습서의이 섹션에서는 변경 toohello 웹 앱을 배포 하 고 hello CDN tootrigger hello CDN toorefresh 해당 캐시를 제거 합니다.

### <a name="deploy-a-change-toohello-web-app"></a>변경 toohello 웹 응용 프로그램 배포

열기 hello `index.html` 파일을 추가 "-V2" hello 다음 예제와 같이 toohello H1 제목을: 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

변경 내용을 커밋하고 toohello 웹 앱을 배포 합니다.

```bash
git commit -am "version 2"
git push azure master
```

배포가 완료 되 면 찾아보기 toohello 웹 앱 URL을 변경 하는 hello를 표시 합니다.

```
http://<appname>.azurewebsites.net/index.html
```

![웹앱의 제목에서 V2](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

Hello 홈 페이지에 대 한 찾아보기 toohello CDN 끝점 URL hello CDN에에서 캐시 된 버전 hello 아직 만료 되지 않으므로 변경할 hello를 보이지 않습니다. 

```
http://<endpointname>.azureedge.net/index.html
```

![CDN의 제목에서 V2 없음](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-hello-cdn-in-hello-portal"></a>Hello CDN hello 포털에서 제거

tootrigger는 CDN tooupdate 캐시 된 버전의 hello를 CDN hello를 삭제 합니다.

Hello 포털 왼쪽된 탐색 영역에서 선택 **리소스 그룹**, 한 다음 웹 앱 (myResourceGroup)에 대해 만든 hello 리소스 그룹을 선택 합니다.

![리소스 그룹 선택](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

Hello 리소스 목록에서 CDN 끝점을 선택 합니다.

![끝점 선택](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

Hello의 hello 위쪽 **끝점** 페이지 **제거**합니다.

![제거 선택](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

원하는 toopurge hello 콘텐츠 경로 입력 합니다. 개별 파일 또는 경로 세그먼트 toopurge 전체 파일 경로 toopurge를 전달할 수 있으며 폴더의 모든 콘텐츠를 새로 고칠 수 있습니다. 변경한 이후 `index.html`, 인지 확인 하는 hello 경로 중 하나입니다.

Hello 페이지의 hello 맨 아래에 선택 **제거**합니다.

![페이지 제거](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-hello-cdn-is-updated"></a>해당 hello CDN은 업데이트를 확인 합니다.

Hello 삭제 요청은 몇 분 정도 일반적으로 처리를 완료할 때까지 기다립니다. toosee hello 현재 상태를 hello hello 페이지 위쪽에 선택 hello 종 모양 아이콘입니다. 

![제거 알림](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

Toohello CDN 끝점 URL에 대 한 찾아보기 `index.html`, 나타나고 이제 hello V2 toohello 제목 hello 홈 페이지에 추가 합니다. Hello CDN에 캐시를 새로 고칠를 표시 합니다.

```
http://<endpointname>.azureedge.net/index.html
```

![CDN의 제목에서 V2](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

자세한 내용은 [Azure CDN 끝점 제거](../cdn/cdn-purge-endpoint.md)를 참조하세요. 

## <a name="use-query-strings-tooversion-content"></a>쿼리 문자열 tooversion 콘텐츠 사용

Azure CDN hello hello 다음 캐싱 동작 옵션을 제공 합니다.

* 쿼리 문자열 무시
* 쿼리 문자열에 대한 캐싱 우회
* 모든 고유한 URL 캐시 

먼저 hello 이러한은 hello default, 자산 hello URL에 쿼리 문자열 hello에 관계 없이 캐시 된 버전을 하나만 있다는 것을 나타냅니다. 

Hello 자습서의이 섹션에서는 각 고유한 URL 동작 toocache 캐싱 hello를 변경할 수 있습니다.

### <a name="change-hello-cache-behavior"></a>Hello 캐시 동작 변경

Hello Azure 포털에서에서 **CDN 끝점** 페이지에서 **캐시**합니다.

선택 **각 고유한 URL 캐시** hello에서 **쿼리 문자열 캐싱 동작** 드롭 다운 목록입니다.

**저장**을 선택합니다.

![쿼리 문자열 캐싱 동작 선택](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a>고유 URL을 별도로 캐시했는지 확인

브라우저에서 hello CDN 끝점에 toohello 홈 페이지를 탐색 하는 쿼리 문자열을 포함. 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

CDN hello hello 현재 웹 응용 프로그램 콘텐츠를 hello 제목에 "V2"를 포함 하는 반환 합니다. 

tooensure이이 페이지 hello CDN에서 새로 고침 hello 페이지에에서 캐시 됩니다. 

열기 `index.html` 너무 "V2" 변경 "V3" hello 변경 내용 배포 및 합니다. 

```bash
git commit -am "version 3"
git push azure master
```

브라우저에서 새 쿼리 문자열로 toohello CDN 끝점 URL을와 같은 이동 `q=2`합니다. CDN hello hello 현재 가져옵니다 `index.html` 파일을 "V3"를 표시 합니다.  Hello로 toohello CDN 끝점을 이동 하는 경우 하지만 `q=1` 쿼리 문자열, "V2"를 참조 하십시오.

```
http://<endpointname>.azureedge.net/index.html?q=2
```

![CDN에서 제목에 V3, 쿼리 문자열 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

![CDN에서 제목에 V2, 쿼리 문자열 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

이 출력에서는 각 쿼리 문자열이 다르게 처리됨을 보여 줍니다.

* 이전에는 q=1이 사용되어 캐시된 내용(V2)을 반환합니다.
* q = 2 이므로 새로 만들었거나, hello 최신 웹 응용 프로그램 콘텐츠 검색 되 고 (V3)을 반환 합니다.

자세한 내용은 [쿼리 문자열을 사용하여 Azure CDN 캐싱 동작 제어](../cdn/cdn-query-string.md)를 참조하세요.

## <a name="map-a-custom-domain-tooa-cdn-endpoint"></a>사용자 지정 도메인 tooa CDN 끝점 매핑

CNAME 레코드를 만들어 사용자 지정 도메인 tooyour를 CDN 끝점 매핑합니다. CNAME 레코드는 원본 도메인 tooa 대상 도메인을 매핑하는 DNS 기능입니다. 예를 들어 매핑하는 `cdn.contoso.com` 또는 `static.contoso.com` 너무`contoso.azureedge.net`합니다.

사용자 지정 도메인이 없는 경우 다음과 같은 hello [앱 서비스 도메인 자습서](custom-dns-web-site-buydomains-web-app.md) 사용 하 여 도메인 toopurchase hello Azure 포털입니다. 

### <a name="find-hello-hostname-toouse-with-hello-cname"></a>CNAME hello로 hello hostname toouse 찾기

Hello Azure 포털에서에서 **끝점** 페이지에서 **개요** hello 탐색 및 선택 hello 왼쪽에서 선택 된 **+ 사용자 지정 도메인** hello hello 페이지 위쪽에 단추입니다.

![사용자 지정 도메인 추가 선택](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

Hello에 **사용자 지정 도메인 추가** 페이지에 CNAME 레코드를 만드는 hello 끝점 호스트 이름 toouse 표시 합니다. CDN 끝점 URL에서 파생 된 hello 호스트 이름:  **&lt;EndpointName >. azureedge.net**합니다. 

![도메인 페이지 추가](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-hello-cname-with-your-domain-registrar"></a>도메인 등록 기관과 함께 CNAME hello 구성

Tooyour 도메인 등록 기관의 웹 사이트를 탐색 하 고 DNS 레코드를 만들기 위한 hello 섹션을 찾습니다. **도메인 이름**, **DNS** 또는 **이름 서버 관리**와 같은 섹션에서 이를 찾을 수 있습니다.

CNAMEs를 관리 하기 위한 hello 섹션을 찾습니다. Toogo tooan 고급 설정 페이지를 가질 수 고 CNAME, 별칭 또는 하위 도메인 hello 단어를 검색할 수 있습니다.

선택된 된 하위 도메인을 매핑하는 CNAME 레코드를 만듭니다 (예를 들어 **정적** 또는 **cdn**) toohello **끝점 호스트 이름** hello 포털의 앞부분에 표시 합니다. 

### <a name="enter-hello-custom-domain-in-azure"></a>Azure의 hello 사용자 지정 도메인을 입력 합니다.

Toohello 반환 **사용자 지정 도메인 추가** 페이지 및 hello 하위 도메인을 포함 하 여 hello 대화 상자에서 사용자 지정 도메인을 입력 합니다. 예를 들어 `cdn.contoso.com`을 입력합니다.   
   
Azure는 입력 한 hello 도메인 이름에 대 한 hello CNAME 레코드가 있는지 확인 합니다. Hello CNAME이 올바르면 사용자 지정 도메인의 유효성이 검사 됩니다.

Hello 인터넷에서 CNAME 레코드 toopropagate tooname 서버 hello에 대 한 시간이 걸릴 수 있습니다. 도메인의 유효성이 바로 검사되지 않으면 몇 분 후에 다시 시도합니다.

### <a name="test-hello-custom-domain"></a>테스트 hello에 대 한 사용자 지정 도메인

브라우저에서 탐색 toohello `index.html` 사용자 지정 도메인을 사용 하 여 파일 (예를 들어 `cdn.contoso.com/index.html`) hello 결과 tooverify hello로 수행 하는 경우 직접 너무 동일`<endpointname>azureedge.net/index.html`합니다.

![사용자 지정 도메인 URL을 사용하는 샘플 앱 홈 페이지](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

자세한 내용은 참조 [맵 Azure CDN 콘텐츠 tooa 사용자 지정 도메인](../cdn/cdn-map-content-to-custom-domain.md)합니다.

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>다음 단계

학습한 내용은 다음과 같습니다.

> [!div class="checklist"]
> * CDN 끝점 만들기
> * 캐시된 자산 새로 고침
> * 사용 하 여 쿼리 문자열 캐시 toocontrol 버전입니다.
> * Hello CDN 끝점에 대 한 사용자 지정 도메인을 사용 합니다.

Toooptimize CDN 성능에 따라 hello 문서 방법에 대해 알아봅니다.

> [!div class="nextstepaction"]
> [Azure CDN에서 파일을 압축하여 성능 향상](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [Azure CDN 끝점에 자산 미리 로드](../cdn/cdn-preload-endpoint.md)
