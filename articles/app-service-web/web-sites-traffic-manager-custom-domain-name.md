---
title: "Azure 앱 서비스 부하 분산에 대 한 트래픽 관리자를 사용 하는 웹 앱에 대 한 사용자 지정 도메인 이름 aaaConfigure 합니다."
description: "부하 분산을 위해 트래픽 관리자를 포함하는 Azure 앱 서비스의 웹 앱에 대한 사용자 지정 도메인 이름을 사용합니다."
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 0f96c0e7-0901-489b-a95a-e3b66ca0a1c2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: dfde5fc6b445b30b10e03dcb03e8d072130d9377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-a-web-app-in-azure-app-service-using-traffic-manager"></a>트래픽 관리자를 사용하는 Azure 앱 서비스의 웹 앱에 대한 사용자 지정 도메인 이름 구성
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro-traffic-manager.md)]

이 문서에서는 부하 분산을 위해 트래픽 관리자를 사용하는 Azure 앱 서비스에서 사용자 지정 도메인 이름을 사용하는 일반 지침을 제공합니다.

[!INCLUDE [tmwebsitefooter](../../includes/custom-dns-web-site-traffic-manager-notes.md)]

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a>DNS 레코드 이해
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-traffic-manager.md)]

<a name="bkmk_configsharedmode"></a>

## <a name="configure-your-web-apps-for-standard-mode"></a>표준 모드에 대해 웹 앱 구성
[!INCLUDE [modes](../../includes/custom-dns-web-site-modes-traffic-manager.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a>사용자 지정 도메인에 대한 DNS 레코드 추가
> [!NOTE]
> Azure 앱 서비스 웹 앱을 통해 도메인을 구입한 한 후 다음 단계를 건너뛰고 있습니다 toohello의 마지막 단계를 참조 하는 경우 [는 웹 응용 프로그램 도메인을 구입](custom-dns-web-site-buydomains-web-app.md) 문서.
> 
> 

tooassociate Azure 앱 서비스의 웹 앱과 사용자 지정 도메인을 추가 해야 새 항목 hello DNS 테이블의 사용자 지정 도메인에 대 한 hello 도메인 등록자에서 도메인 이름을 구매한에서 제공 하는 도구를 사용 하 여 합니다. 다음 단계 toolocate hello를 사용 하 여 및 hello DNS 도구를 사용 합니다.

1. 도메인 등록자에 tooyour 계정에 로그인 하 고 DNS 레코드를 관리 하기 위한 페이지를 확인 합니다. 링크 검색 또는 hello 사이트의 영역으로 표시 **도메인 이름**, **DNS**, 또는 **이름 서버 관리**합니다. 링크 toothis 페이지를 찾을 수 있습니다 수 계정 정보를 보고 하 고 다음 링크를와 같은 찾고 종종 **내 도메인**합니다.
2. 도메인 이름에 대 한 hello 관리 페이지를 발견 하면 tooedit hello DNS 레코드를 허용 하는 링크를 찾아보십시오. 이 링크는 **영역 파일**, **DNS 레코드** 또는 **고급** 구성 링크로 나열될 수 있습니다.
   
   * hello 페이지의 레코드를 연결 하는 항목 등 이미 만든는 것 '**@**'또는'\*' '도메인 주차' 페이지를 사용 합니다. 또한 **www**와 같은 일반 하위 도메인에 대한 레코드가 포함될 수 있습니다.
   * hello 페이지 언급 **CNAME 레코드**, 드롭 다운 tooselect 레코드 종류를 제공 합니다. **A records** 및 **MX 레코드**와 같은 다른 레코드를 나타낼 수도 있습니다. 어떤 경우에는 CNAME 레코드를 **별칭 레코드**와 같은 다른 이름으로 부릅니다.
   * hello 페이지에는 너무 사용 하는 필드**지도** 에서 **호스트 이름** 또는 **도메인 이름** tooanother 도메인 이름입니다.
3. 각 등록자의 hello 세부 사항 다 일반적 상태에 매핑해야 *에서* 사용자 지정 도메인 이름 (같은 **contoso.com**,) *를* hello 트래픽 관리자 도메인 이름 (**contoso.trafficmanager.net**) 웹 앱에 사용 되는 합니다.
   
   > [!NOTE]
   > 또는 앱 tooit 바인딩할 toopreemptively를 해야 하는 레코드는 이미 사용 중인 경우는 추가 CNAME 레코드를 만들 수 있습니다. 예를 들어 toopreemptively 바인딩 **www.contoso.com** tooyour 웹 응용 프로그램에서 CNAME 레코드를 만들 **awverify.www** 너무**contoso.trafficmanager.net**합니다. 그런 다음 hello "www" CNAME 레코드를 변경 하지 않고 "www.contoso.com" tooyour 웹 앱을 추가할 수 있습니다. 자세한 내용은 [사용자 지정 도메인에서 웹앱에 대한 DNS 레코드 만들기][CREATEDNS]를 참조하세요.
   > 
   > 
4. 등록자에서 DNS 레코드를 수정 또는 추가 완료 되 면 hello 변경 내용을 저장 합니다.

<a name="enabledomain"></a>

## <a name="enable-traffic-manager"></a>트래픽 관리자 사용
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-traffic-manager.md)]

## <a name="next-steps"></a>다음 단계
자세한 내용은 참조 hello [Node.js 개발자 센터](/develop/nodejs/)합니다.

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[CREATEDNS]: ../dns/dns-web-sites-custom-domain.md
