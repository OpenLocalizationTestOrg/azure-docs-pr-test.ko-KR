---
title: "Memcache 프로토콜-Azure hello 통해 앱 서비스 웹 앱 tooRedis aaaConnect | Microsoft Docs"
description: "Azure 앱 서비스 tooRedis 캐시의에서 웹 앱을 연결 hello Memcache 프로토콜을 사용 하 여"
services: app-service\web
documentationcenter: php
author: SyntaxC4
manager: erikre
editor: riande
ms.assetid: 0fcdf9fa-2995-4839-ba4d-cfa389c4ba06
ms.service: app-service-web
ms.devlang: php
ms.topic: get-started-article
ms.tgt_pltfrm: windows
ms.workload: na
ms.date: 02/29/2016
ms.author: cfowler
ms.openlocfilehash: 48036d60fbbced59eb1e37584f507fffffff753d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# Hello Memcache 프로토콜을 통해 Azure 앱 서비스 tooRedis 캐시에서에서 웹 앱에 연결
이 문서에서는 알아봅니다 어떻게 tooconnect WordPress는 웹에서 응용 프로그램 [Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714) 너무[Azure Redis Cache] [ 12] hello를 사용 하 여 [Memcache] [ 13] 프로토콜입니다. 메모리 내 캐싱 Memcached 서버를 사용 하 여 기존 웹 앱이 있는 경우 앱 서비스 tooAzure 및 사용 하 여 hello 자사 캐싱 솔루션 Microsoft Azure에서 거의 또는 전혀 변경 tooyour 응용 프로그램 코드와 마이그레이션할 수 있습니다. 또한.NET, PHP, Node.js, Java, 및 Python 등의 널리 사용 되는 응용 프로그램 프레임 워크를 사용 하는 동안 메모리 내 캐시에 대 한 Azure Redis 캐시 Azure 앱 서비스에서 기존 Memcache 전문 지식을 toocreate 확장성이 높은, 분산 응용 프로그램을 사용할 수 있습니다.  

앱 서비스 웹 응용 프로그램 프록시 역할을 Memcache 호출 tooAzure Redis Cache 캐싱을 위한 하는 로컬 Memcached 서버 hello 웹 앱 Memcache shim 된이 응용 프로그램 시나리오를 수 있습니다. 이 통해 Redis 캐시와 hello Memcache 프로토콜 toocache 데이터를 사용 하 여 통신 하는 모든 앱. Memcache shim이 hello Memcache 프로토콜을 사용 하 여 통신 하는 것으로 응용 프로그램 또는 응용 프로그램 프레임 워크에서 사용할 수 없도록 hello 프로토콜 수준에서 작동 합니다.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## 필수 조건
웹 앱 Memcache 심 hello hello Memcache 프로토콜을 사용 하 여 통신 제공 응용 프로그램과 함께 사용할 수 있습니다. 이 예의 경우에 대 한 hello 참조 응용 프로그램은 hello Azure Marketplace에서에서 프로 비전 할 수 있는 확장 가능한 WordPress 사이트.

이 문서에서 설명 하는 hello 단계를 수행 합니다.

* [Hello Azure Redis 캐시 서비스의 인스턴스를 프로 비전][0]
* [Azure에서 확장 가능한 WordPress 사이트 배포][1]

Hello 확장 가능한 WordPress 사이트를 배포 및 프로 비전 Redis 캐시 인스턴스를 설정한 후 준비 tooproceed hello Memcache shim Azure 앱 서비스 웹 앱을 활성화할 수 있습니다.

## 웹 앱 Memcache 심 hello를 사용 하도록 설정
순서 tooconfigure Memcache 심에서 세 가지 응용 프로그램 설정을 만들어야 합니다. 이렇게 다양 한 hello를 비롯 하 여 메서드를 사용 하 여 [Azure 포털](http://go.microsoft.com/fwlink/?LinkId=529715), hello [클래식 포털][3], hello [Azure PowerShell Cmdlet] [ 5] 또는 hello [Azure 명령줄 인터페이스][5]합니다. 이 게시물의 hello 위해서 댓 toouse hello [Azure 포털] [ 4] tooset hello 앱 설정 합니다. hello 다음 값을 검색할 수에서 **설정을** Redis 캐시 인스턴스의 블레이드 합니다.

![Azure Redis 캐시 설정 블레이드](./media/web-sites-connect-to-redis-using-memcache-protocol/1-azure-redis-cache-settings.png)

### REDIS_HOST 앱 설정 추가
필요한 첫 번째 응용 프로그램 설정을 hello toocreate는 hello **REDIS\_호스트** 앱 설정 합니다. 이 설정은 hello 대상 toowhich hello shim 전달 hello 캐시 정보를 설정합니다. hello에서 hello REDIS_HOST 응용 프로그램 설정을 검색할 수에 대 한 필수 값 hello **속성** Redis 캐시 인스턴스의 블레이드 합니다.

![Azure Redis 캐시 호스트 이름](./media/web-sites-connect-to-redis-using-memcache-protocol/2-azure-redis-cache-hostname.png)

Hello 응용 프로그램을 설정할 때의 너무 hello 키 설정**REDIS\_호스트** hello 응용 프로그램 설정 toohello의 hello 값과 **hostname** hello Redis 캐시 인스턴스의 합니다.

![웹앱 AppSetting REDIS_HOST](./media/web-sites-connect-to-redis-using-memcache-protocol/3-azure-website-appsettings-redis-host.png)

### REDIS_KEY 앱 설정 추가
필요한 두 번째 응용 프로그램 설정을 hello toocreate는 hello **REDIS\_키** 앱 설정 합니다. 이 설정은 hello 인증 토큰 필요한 toosecurely 액세스 hello Redis 캐시 인스턴스를 제공합니다. Hello에서 hello REDIS_KEY 응용 프로그램 설정에 대 한 필수 hello 값을 검색할 수 있습니다 **선택키가** hello Redis 캐시 인스턴스의 블레이드 합니다.

![Azure Redis 캐시 기본 키](./media/web-sites-connect-to-redis-using-memcache-protocol/4-azure-redis-cache-primarykey.png)

Hello 응용 프로그램을 설정할 때의 너무 hello 키 설정**REDIS\_키** hello 응용 프로그램 설정 toohello의 hello 값과 **기본 키** hello Redis 캐시 인스턴스의 합니다.

![Azure 웹 사이트 AppSetting REDIS_KEY](./media/web-sites-connect-to-redis-using-memcache-protocol/5-azure-website-appsettings-redis-primarykey.png)

### MEMCACHESHIM_REDIS_ENABLE 앱 설정 추가
마지막 응용 프로그램 설정이 hello는 사용 되는 tooenable hello Memcache 심을 사용 하 여 hello REDIS_HOST 및 REDIS_KEY tooconnect toohello Azure Redis Cache 및 앞으로 hello 캐시 호출, 웹 응용 프로그램에서입니다. Hello 응용 프로그램을 설정할 때의 너무 hello 키 설정**MEMCACHESHIM\_REDIS\_사용** 값을 너무 hello 및**true**합니다.

![웹앱 AppSetting MEMCACHESHIM_REDIS_ENABLE](./media/web-sites-connect-to-redis-using-memcache-protocol/6-azure-website-appsettings-enable-shim.png)

Hello 3 (3) 응용 프로그램 설정 추가 완료 하면 클릭 **저장**합니다.

## PHP에 Memcache 확장 사용
Hello 응용 프로그램 toospeak hello Memcache 프로토콜을 위해에서 필요한 tooinstall hello Memcache 확장 tooPHP-WordPress 사이트에 대 한 hello 언어 프레임 워크입니다.

### Hello php_memcache 확장 다운로드
너무 찾아보기[PECL][6]합니다. Hello 범주 캐싱, 아래에서 클릭 [memcache][7]합니다. Hello 다운로드 열 아래에서 hello DLL 링크를 클릭 합니다.

![PHP PECL 웹 사이트](./media/web-sites-connect-to-redis-using-memcache-protocol/7-php-pecl-website.png)

웹 응용 프로그램에서 사용 하도록 설정 하는 PHP 버전 hello에 대 한 hello 비 스레드로부터 안전 하 게 보호 (NTS) x86 링크를 다운로드 합니다. (기본은 PHP 5.4입니다.)

![PHP PECL 웹 사이트 Memcache 패키지](./media/web-sites-connect-to-redis-using-memcache-protocol/8-php-pecl-memcache-package.png)

### Hello php_memcache 확장 사용 하도록 설정
Hello 파일을 다운로드 한 후 압축 해제 하 고 hello 업로드 **php\_memcache.dll** hello에 **d:\\홈\\사이트\\wwwroot\\bin\\ext\\**  디렉터리입니다. Hello php_memcache.dll hello 웹 앱에 업로드 되 면 tooenable hello 확장 toohello PHP 런타임에 필요 합니다. tooenable hello hello open hello Azure 포털에서에서 Memcache 확장 **응용 프로그램 설정** 블레이드 hello 웹 앱에 대 한의 hello 키를 가진 새 응용 프로그램 설정을 추가 **PHP\_확장** 및 hello 값 **bin\\ext\\php_memcache.dll**합니다.

> [!NOTE]
> Hello 웹 응용 프로그램은 tooload 여러 PHP 확장을 필요한 경우 PHP_EXTENSIONS hello 값 tooDLL 파일 상대 경로 쉼표로 구분 된 목록 이어야 합니다.
> 
> 

![웹앱 AppSetting PHP_EXTENSIONS](./media/web-sites-connect-to-redis-using-memcache-protocol/9-azure-website-appsettings-php-extensions.png)

완료되면 **저장**을 클릭합니다.

## Memcache WordPress 플러그인 설치
> [!NOTE]
> Hello를 다운로드할 수도 있습니다 [Memcached 개체 캐시 플러그 인](https://wordpress.org/plugins/memcached/) WordPress.org에서 합니다.
> 
> 

Hello WordPress 플러그 인 페이지에서 클릭 **새로 추가**합니다.

![WordPress 플러그인 페이지](./media/web-sites-connect-to-redis-using-memcache-protocol/10-wordpress-plugin.png)

Hello 검색 상자에 입력 **memcached** 누릅니다 **Enter**합니다.

![WordPress 새 플러그인 추가](./media/web-sites-connect-to-redis-using-memcache-protocol/11-wordpress-add-new-plugin.png)

찾을 **Memcached 개체 캐시** hello 목록에서 클릭 **지금 설치**합니다.

![Memcache WordPress 플러그인 설치](./media/web-sites-connect-to-redis-using-memcache-protocol/12-wordpress-install-memcache-plugin.png)

### Hello Memcache WordPress 플러그 인을 사용 하도록 설정
> [!NOTE]
> 이 블로그의 hello 지침에 따라 [어떻게 tooenable 웹 응용 프로그램에서 사이트 확장] [ 8] tooinstall Visual Studio Team Services.
> 
> 

Hello에 `wp-config.php` 파일, hello 코드 위의 hello 중지 편집 설명 hello hello 파일 끝에 다음을 추가 합니다.

```php
$memcached_servers = array(
    'default' => array('localhost:' . getenv("MEMCACHESHIM_PORT"))
);
```

이 코드를 붙여 넣은 후 monaco hello 문서를 자동으로 저장 됩니다.

hello 다음 단계 tooenable hello 개체 캐시 플러그 인입니다. 끌어서 놓기를 통해 이렇게 **개체 cache.php** 에서 **wp-콘텐츠/플러그 인/memcached** 폴더 toohello **wp 콘텐츠** 폴더 tooenable hello Memcache 개체 캐시 기능입니다.

![Hello memcache 개체 cache.php 플러그 인을 찾기](./media/web-sites-connect-to-redis-using-memcache-protocol/13-locate-memcache-object-cache-plugin.png)

이제 해당 hello **개체 cache.php** 파일이 hello에 **wp 콘텐츠** hello Memcached 개체 캐시는 이제 사용할 수 있습니다. 폴더입니다.

![Hello memcache 개체 cache.php 플러그 인을 사용 하도록 설정](./media/web-sites-connect-to-redis-using-memcache-protocol/14-enable-memcache-object-cache-plugin.png)

## Hello 플러그 인이 작동 하는 Memcache 개체 캐시를 확인 합니다.
Hello 단계 tooenable hello 웹 앱 Memcache 심 일부만 완료 됩니다. hello만 왼쪽 tooverify hello 데이터 Redis 캐시 인스턴스를 채우는입니다.

### Azure Redis Cache에서 hello 비 SSL 포트 지원을 사용 하도록 설정
> [!NOTE]
> 이 문서 작성의 hello 시 hello Redis CLI SSL 연결을 지원 하지 않습니다, 그리고 따라서 hello 다음 단계는 필요 합니다.
> 
> 

Hello Azure 포털에서에서이 웹 앱에 대해 만든 toohello Redis 캐시 인스턴스를 찾습니다. Hello 캐시 블레이드를 연 후 클릭 hello **설정을** 아이콘입니다.

![Azure Redis Cache 설정 단추](./media/web-sites-connect-to-redis-using-memcache-protocol/15-azure-redis-cache-settings-button.png)

선택 **액세스 포트** hello 목록에서 합니다.

![Azure Redis Cache 액세스 포트](./media/web-sites-connect-to-redis-using-memcache-protocol/16-azure-redis-cache-access-port.png)

**SSL을 통해서만 액세스 허용**에 대해 **아니요**를 클릭합니다.

![Azure Redis Cache 액세스 포트 SSL만](./media/web-sites-connect-to-redis-using-memcache-protocol/17-azure-redis-cache-access-port-ssl-only.png)

이제 hello 비 SSL 포트 설정 되어 있는지 표시 됩니다. **Save**를 클릭합니다.

![Azure Redis Cache Redis SSL이 아닌 포털에 액세스](./media/web-sites-connect-to-redis-using-memcache-protocol/18-azure-redis-cache-access-port-non-ssl.png)

### Redis Cache tooAzure redis cli에서 연결
> [!NOTE]
> 이 단계에서는 redis가 개발 컴퓨터에 로컬로 설치된 것으로 간주합니다. [다음 지침을 사용하여 Redis를 로컬로 설치합니다][9].
> 
> 

다음 명령을 선택 및 형식 hello의 명령줄 콘솔을 엽니다.

```shell
redis-cli –h <hostname-for-redis-cache> –a <primary-key-for-redis-cache> –p 6379
```

Hello 대체  **&lt;호스트 이름에 대 한 redis 캐시&gt;**  hello 실제 xxxxx.redis.cache.windows.net 호스트 이름 및 hello  **&lt;기본 키-에-redis-캐시&gt;**  hello hello 캐시에 대 한 액세스 키를 눌러 다음 **Enter**합니다. 연결 되 면 hello CLI가 toohello Redis 캐시 인스턴스의 모든 redis 명령을 실행 합니다. Hello 스크린 아래 toolist hello 키를 선택 했습니다.

![Redis Cache tooAzure 터미널에 CLI Redis에서 연결](./media/web-sites-connect-to-redis-using-memcache-protocol/19-redis-cli-terminal.png)

hello 호출 toolist hello 키 값을 반환 해야 합니다. 파일이 없으면 toohello 웹 응용 프로그램을 탐색 하 고 다시 시도 합니다.

## 결론
축하합니다. hello WordPress 응용 프로그램 처리량이 증가 중앙된 메모리에 캐시 tooaid가 되었습니다. 기억 hello 웹 앱 Memcache Shim 프로그래밍 언어 또는 응용 프로그램 프레임 워크에 관계 없이 Memcache 클라이언트와 함께 사용할 수 있습니다. hello 웹 앱 Memcache shim에 대 한 의견이 나 tooask 질문 tooprovide 너무 게시[MSDN 포럼] [ 10] 또는 [Stackoverflow][11]합니다.

> [!NOTE]
> Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.
> 
> 

## 변경된 내용
* 웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [Azure 앱 서비스와 기존 Azure 서비스에 미치는 영향](http://go.microsoft.com/fwlink/?LinkId=529714)

[0]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache
[1]: http://bit.ly/1t0KxBQ
[2]: http://manage.windowsazure.com
[3]: http://portal.azure.com
[4]: /powershell/azureps-cmdlets-docs
[5]: /downloads
[6]: http://pecl.php.net
[7]: http://pecl.php.net/package/memcache
[8]: http://blog.syntaxc4.net/post/2015/02/05/how-to-enable-a-site-extension-in-azure-websites.aspx
[9]: http://redis.io/download#installation
[10]: https://social.msdn.microsoft.com/Forums/home?forum=windowsazurewebsitespreview
[11]: http://stackoverflow.com/questions/tagged/azure-web-sites
[12]: /services/cache/
[13]: http://memcached.org
