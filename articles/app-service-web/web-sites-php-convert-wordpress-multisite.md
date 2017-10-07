---
title: "Azure 앱 서비스의 aaaConvert WordPress tooMultisite"
description: "Tootake 기존 WordPress 웹 앱이 Azure의 hello 갤러리를 통해 만들어진 하 고 tooWordPress 멀티 사이트를 변환 하는 방법을 알아봅니다"
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: fe52dbf4-179c-42f1-adf9-d6a9af920c39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 1153f0a8043de875f081704cd0a124776758878c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-wordpress-toomultisite-in-azure-app-service"></a>Azure 앱 서비스에서 WordPress tooMultisite 변환
## <a name="overview"></a>개요
*[Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*

이 자습서에서는 tootake WordPress는 기존 웹 응용 프로그램 만드는 방법은 Azure 및 WordPress 멀티 사이트에 설치 하는 변환에서 hello 갤러리를 통해 배웁니다. 또한 어떻게 tooassign hello의 사용자 지정 도메인 tooeach 하위 사이트 귀하의 설치에 설명 합니다.

여기서는 WordPress가 이미 설치되어 있다고 가정합니다. 이렇게 하지 않으면 하는 경우에 제공 된 hello 지침은 따르십시오 [Azure의 hello 갤러리에서 WordPress 웹 사이트를 만들][website-from-gallery]합니다.

기존 WordPress 변환 단일 사이트 설치 tooMultisite 일반적으로 매우 간단 하 고 hello에서 바로 hello 초기 단계 중 상당수 [A 네트워크 만들기] [ wordpress-codex-create-a-network] hello 페이지[WordPress Codex](http://codex.wordpress.org)합니다.

이제 시작하겠습니다.

## <a name="allow-multisite"></a>멀티 사이트 허용
먼저 hello 통해 멀티 사이트 tooenable `wp-config.php` hello로 파일 **WP\_허용\_멀티 사이트** 상수입니다. 없는 두 가지 방법 tooedit 웹 응용 프로그램 파일: hello FTP 및 Git 통해 hello를 통해 먼저가 있습니다. 방법을 잘 모를 경우 toosetup toohello 자습서 다음을 참조 하십시오 이러한 방법 중 하나:

* [MySQL 및 FTP를 사용하는 PHP 웹 사이트][website-w-mysql-and-ftp-ftp-setup]
* [MySQL 및 Git를 사용하는 PHP 웹 사이트][website-w-mysql-and-git-git-setup]

열기 hello `wp-config.php` 선택한 hello 편집기로 파일을 hello 위에 hello 다음과 같은 추가 `/* That's all, stop editing! Happy blogging. */` 선입니다.

    /* Multisite */

    define( 'WP_ALLOW_MULTISITE', true );

있는지 toosave hello 파일 이어야 하 고 뒤로 toohello 서버 업로드!

## <a name="network-setup"></a>네트워크 설정
Toohello 로그인 *wp 관리자* 웹 응용 프로그램의 영역 hello 아래에 새 항목을 참조 해야 **도구** 이라는 메뉴가 **네트워크 설정**합니다. 클릭 **네트워크 설정** 고 네트워크의 hello 세부 정보를 입력 합니다.

![네트워크 설정 화면][wordpress-network-setup]

이 자습서에서는 hello *하위 디렉터리* 항상 작동 해야 하 고 hello 자습서의 뒷부분에 나오는 각 하위 사이트에 대 한 사용자 지정 도메인을 설정 합니다 것 때문에 스키마를 사이트입니다. 그러나 hello 통해 도메인을 매핑하는 경우 하위 도메인을 설치 하는 가능한 toosetup 있어야 [Azure 포털](https://portal.azure.com) 및 와일드 카드 DNS를 올바르게 설정 합니다.

하위 도메인 vs 대 한 자세한 내용은 하위 디렉터리 설정을 참조 hello [멀티 사이트 네트워크 유형의] [ wordpress-codex-types-of-networks] hello WordPress Codex 문서입니다.

## <a name="enable-hello-network"></a>Hello 네트워크를 사용 하도록 설정
hello 네트워크 hello 데이터베이스에서 이제 구성 하지만 한 나머지 단계 tooenable hello 네트워크 기능. Hello 마무리 `wp-config.php` 설정을 확인 하 고 `web.config` 제대로 각 사이트를 라우팅합니다.

Hello를 클릭 한 후 **설치** hello 단추 *네트워크 설정* 페이지에서 WordPress는 tooupdate hello 시도 `wp-config.php` 및 `web.config` 파일입니다. 그러나 항상 확인 해야 hello 파일 tooensure hello 업데이트 성공 했습니다. 그렇지 않은 경우이 화면 hello 필요한 업데이트를 표시 합니다. 편집 하 고 hello 파일을 저장 합니다.

작업을 수행 하면 아웃 toolog 및 로그 필요 합니다. 이러한 업데이트 hello wp 관리 대시보드 스풀링됩니다.

있어야는 추가 메뉴 레이블이 지정 된 hello admin 모음의 **내 사이트**합니다. 이 메뉴 있습니다 toocontrol hello 통해 새로운 네트워크 **네트워크 관리자** 대시보드 합니다.

## <a name="adding-custom-domains"></a>사용자 지정 도메인 추가
hello [WordPress MU 도메인 매핑] [ wordpress-plugin-wordpress-mu-domain-mapping] 플러그 인을 사용 하면 쉽게 tooadd 사용자 지정 도메인 tooany 사이트 네트워크에 있습니다. 플러그 인 toooperate hello에 대 한 적절 하 게 해야 toodo hello 포털 뿐만 아니라 도메인 등록자에서 몇 가지 추가 설정이 있습니다.

## <a name="enable-domain-mapping-toohello-web-app"></a>도메인 매핑 toohello 웹 응용 프로그램을 사용 하도록 설정
hello **무료** [앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714) 계획 모드에서는 사용자 지정 도메인 tooWeb 앱을 추가할 수 없습니다. 해야 tooswitch 너무**Shared** 또는 **표준** 모드입니다. toodo이:

* Azure 포털 toohello를 로그인 하 고 웹 응용 프로그램을 찾습니다. 
* Hello 클릭 **수직** 탭에서 **설정을**합니다.
* **일반**에서 *공유* 또는 *표준*을 선택합니다.
* 페이지 맨 아래에 있는 **저장**

Tooverify hello 변경 하 라는 메시지가 나타날 수 고 웹 앱 수 이제 사용량에 따라 비용 하 고도 설정한 다른 구성이 hello를 승인할 수 있습니다.

몇 초 정도 tooprocess hello 새 설정을 걸리는 이제는 사용자 도메인을 좋은 시간 toostart 설정 합니다.

## <a name="verify-your-domain"></a>도메인 확인
Azure 웹 앱을 허용 하는 사용자 도메인 toohello 사이트 toomap 전에 먼저 hello 권한 부여 toomap hello 도메인 있는지 tooverify를 해야 합니다. toodo 따라서 새 CNAME 레코드 tooyour DNS 항목을 추가 해야 합니다.

* Tooyour 도메인의 DNS 관리자 로그인
* 새로운 CNAME *awverify*
* 지점 *awverify* 너무*awverify. YOUR_DOMAIN.azurewebsites.net*

단계를 수행 하는 hello 즉시 작동 하지 않을 경우 커피를 확인 한 다음 다시 시도 하 고 다시 시도 하십시오 이동 하는 하므로 하세요 전체 발효 DNS 변경 내용 toogo hello에 대 한 다소 시간이 걸릴 수 있습니다 것입니다.

## <a name="add-hello-domain-toohello-web-app"></a>Hello 도메인 toohello 웹 응용 프로그램 추가
Hello Azure 포털을 통해 반환 tooyour 웹 응용 프로그램 클릭 **설정**, 클릭 하 고 **사용자 지정 도메인 및 SSL**합니다.

Hello 때 *SSL 설정* 는 표시 나타납니다 hello 필드 tooassign tooyour 웹 응용 프로그램을 복원할 모든 hello 도메인을 입력 합니다. 도메인은 여기에 나열 되지 hello 도메인 DNS가 설치 하는 방법에 관계 없이 WordPress, 내부 매핑에 사용할 수 있는 되지 않습니다.

![사용자 지정 도메인 관리 대화 상자][wordpress-manage-domains]

Hello 텍스트 상자에 도메인을 입력 한 후 Azure hello 이전에 만든 CNAME 레코드를 확인 합니다. Hello DNS에 완전히 전파 되지, 빨간색 표시기가 표시 됩니다. 성공한 경우에는 녹색 확인 표시가 나타납니다. 

Hello hello hello 대화 상자 맨 아래에 나열 된 IP 주소를 기록해 둡니다. 도메인에 대 한이 toosetup hello 레코드가 필요 합니다.

## <a name="setup-hello-domain-a-record"></a>Hello 도메인 A 레코드를 설정 합니다.
Hello 다른 단계가 성공 했는지, 하는 경우 이제 hello DNS A 레코드를 통해 도메인 tooyour Azure 웹 앱을 할당할 수 있습니다. 

그러나 것이 중요 한 toonote 여기는 Azure 웹 앱에 동의 CNAME 및 A 레코드를 모두 있습니다 *해야* A 레코드 tooenable 적절 한 도메인 매핑을 사용 합니다. CNAME 전달할 수 없습니다 tooanother CNAME을 드립니다 YOUR_DOMAIN.azurewebsites.net를 사용 하 여 Azure에서 만든 작업은입니다.

Hello 이전 단계에서 hello IP 주소를 사용 하 여 tooyour DNS 관리자와 설치 hello 레코드 toopoint toothat IP 반환 합니다.

## <a name="install-and-setup-hello-plugin"></a>Hello 플러그 인을 설치 및 설정
WordPress 멀티 사이트가 현재 없는 기본 제공 메서드 toomap 사용자 지정 도메인입니다. 그러나 호출 플러그 인은 [WordPress MU 도메인 매핑] [ wordpress-plugin-wordpress-mu-domain-mapping] 드립니다 hello 기능을 추가 하는 합니다. 사이트의 네트워크 관리 부분 toohello에에서 로그인 하 고 hello 설치 **WordPress MU 도메인 매핑** 플러그 인 합니다.

설치 및 활성화 hello 플러그 인을 방문 후 **설정** > **도메인 매핑** tooconfigure hello 플러그 인 합니다. Hello 첫 번째 텍스트 상자에 *서버 IP 주소*, 입력된 hello toosetup 사용 된 IP 주소 hello hello 도메인에 대 한 레코드입니다. 필요한 설정을 *도메인 옵션* 원하는 (hello 기본값 만족 하는 종종)를 클릭 하 고 **저장**합니다.

## <a name="map-hello-domain"></a>Hello 도메인 매핑
Hello 방문 **대시보드** toomap hello 도메인을 원하는 hello 사이트에 대 한 합니다. 클릭 **도구** > **도메인 매핑** 및 형식 hello 새 도메인을 클릭 하 고 hello 텍스트 상자에 **추가**합니다.

기본적으로 hello 새 도메인에 자동으로 생성 된 사이트 도메인 toohello 다시 작성된 됩니다. 모든 트래픽을 전송 toohello 새 도메인 toohave을 원하는 경우 확인 hello *이 블로그에 대 한 주 도메인* 저장 하기 전에 상자입니다. 도메인 tooa 사이트의 무제한 추가할 수 있지만 하나만 주 수 있습니다.

## <a name="do-it-again"></a>다시 실행
Azure 웹 앱을 사용 하면 tooadd tooa 웹 응용 프로그램 도메인 개수는 제한이 있습니다. tooadd tooexecute hello 해야 하는 다른 도메인 **도메인 확인** 및 **hello 도메인 A 레코드를 설정** 각 도메인에 대 한 섹션.    

> [!NOTE]
> Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.
> 
> 

## <a name="whats-changed"></a>변경된 내용
* 웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)

[ben-lobaugh]: http://ben.lobaugh.net
[ms-open-tech]: http://msopentech.com
[website-from-gallery]: https://www.windowsazure.com/develop/php/tutorials/website-from-gallery/
[wordpress-codex-create-a-network]: http://codex.wordpress.org/Create_A_Network
[website-w-mysql-and-ftp-ftp-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-ftp/#header-0
[website-w-mysql-and-git-git-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-git/#header-1
[wordpress-network-setup]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-network-setup.png
[wordpress-codex-types-of-networks]: http://codex.wordpress.org/Before_You_Create_A_Network#Types_of_multisite_network
[wordpress-plugin-wordpress-mu-domain-mapping]: http://wordpress.org/extend/plugins/wordpress-mu-domain-mapping/

[wordpress-manage-domains]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-manage-domains.png


