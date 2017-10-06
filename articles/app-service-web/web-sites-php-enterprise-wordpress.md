---
title: "Azure에서 WordPress aaaEnterprise 클래스 | Microsoft Docs"
description: "Azure 앱 서비스에서 toohost 엔터프라이즈 수준의 WordPress 사이트 하는 방법에 대해 알아봅니다"
services: app-service\web
documentationcenter: 
author: sunbuild
manager: yochayk
editor: 
ms.assetid: 22d68588-2511-4600-8527-c518fede8978
ms.service: app-service-web
ms.devlang: php
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 10/24/2016
ms.author: sumuth
ms.openlocfilehash: 4347eddb31d622d1189dc5db4d81b0f3745d6e69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-class-wordpress-on-azure"></a>Azure의 엔터프라이즈급 WordPress
Azure App Service는 중요 업무용 대규모 [WordPress][wordpress] 사이트를 위한 안전하고 사용하기 쉬운 확장 가능 환경을 제공합니다. Hello와 같은 엔터프라이즈 수준의 사이트를 실행 하는 Microsoft 자체 [Office] [ officeblog] 및 [Bing] [ bingblog] 블로그. 이 문서 toouse hello tooestablish Microsoft Azure 앱 서비스의 웹 응용 프로그램 기능 하 고 엔터프라이즈 수준의 많은 양의 방문자를 처리할 수 있는 클라우드 기반 WordPress 사이트를 유지 관리 하는 방법을 보여 줍니다.

## <a name="architecture-and-planning"></a>아키텍처 및 계획
기본 WordPress 설치는 두 가지 요구 사항만 충족하면 됩니다.

* **MySQL 데이터베이스**:이 요구 사항은 통해 사용할 수 있는 [hello Azure Marketplace에서에서 ClearDB][cdbnstore]합니다. 또는 [Windows][mysqlwindows] 또는 [Linux][mysqllinux] 중 하나를 사용하여 Azure Virtual Machines에서 고유한 MySQL 설치를 관리할 수 있습니다.

  > [!NOTE]
  > ClearDB에서는 여러 MySQL 구성을 제공합니다. 각 구성에는 다양한 성능 특징이 있습니다. Hello 참조 [Azure Store] [ cdbnstore] hello Azure 스토어를 통해 또는 hello에 표시 된 대로 직접 제공 되는 제품에 대 한 내용은 [ClearDB 웹 사이트](http://www.cleardb.com/pricing.view)합니다.
  >
  >
* **PHP 5.2.4 이상**: Azure App Service에서는 현재 [PHP 버전 5.4, 5.5 및 5.6][phpwebsite]을 제공합니다.

  > [!NOTE]
  > 하면 항상 실행된 hello 최신 버전의 PHP hello 최신 보안 픽스를 권장 합니다.
  >
  >

### <a name="basic-deployment"></a>기본 배포
방금 hello 기본 요구 사항을 사용 하는 경우에 Azure 지역 내에서 기본적인 솔루션을 만들 수 있습니다.

![단일 Azure 지역에 호스트된 Azure 웹앱 및 MySQL 데이터베이스][basic-diagram]

이렇게 하면 hello 사이트 tooscale 응용 프로그램의 여러 웹 응용 프로그램 인스턴스를 만들 수를 특정 지리적 지역에 hello 데이터 센터 내에서 호스트할는 모든 항목. 이 영역 외부에서 방문자가 hello 사이트를 사용 하는 경우 한 느린 응답 시간을 표시 합니다. 이 지역에서 hello 데이터 센터의 작동이 경우가 응용 프로그램.

### <a name="multi-region-deployment"></a>다중 지역 배포
Azure를 사용 하 여 [트래픽 관리자][trafficmanager], 여러 지리적 지역에 걸쳐 WordPress 사이트를 확장할 수 있으며 제공할 모든 방문자에 대해 동일한 URL hello 합니다. 모든 방문자 트래픽 관리자를 통해 제공 하 고 라우트된 tooa 지역을 기반으로 하는 hello 부하 분산 구성 합니다.

![지역에 걸쳐 라우터 tooroute tooMySQL CDBR 고가용성을 사용 하 여 여러 지역에서 호스팅되는 Azure 웹 앱][multi-region-diagram]

각 지역 내에서 여러 웹 응용 프로그램 인스턴스에서 hello WordPress 사이트 현재 확장할 수는 있지만이 확장은 특정 tooa 영역. 높은 트래픽 지역과 낮은 트래픽 지역이 다르게 확장될 수 있습니다.

사용할 수 있습니다 tooreplicate 및 경로 트래픽 toomultiple MySQL 데이터베이스 [ClearDB 가용 라우터에 (CDBRs)] [ cleardbscale] (왼쪽에 표시) 또는 [MySQL 클러스터 Carrier 등급 Edition (CGE)] [cge].

### <a name="multi-region-deployment-with-media-storage-and-caching"></a>미디어 저장소 및 캐싱을 사용한 다중 지역 배포
Hello 사이트에서 업로드 또는 호스트 미디어 파일을 허용 하는 경우 Azure Blob 저장소를 사용 합니다. 캐싱이 필요한 경우 [Redis cache][rediscache], [Memcache 클라우드](http://azure.microsoft.com/gallery/store/garantiadata/memcached/), [MemCachier](http://azure.microsoft.com/gallery/store/memcachier/memcachier/), 또는 기타 캐싱 hello 제공 되는 hello 중 하나 [Azure Store](http://azure.microsoft.com/gallery/store/)합니다.

![다중 지역에 호스트된 Azure 웹앱은 관리되는 캐시, Blob Storage 및 Content Delivery Network와 함께 MySQL용 CDBR 고가용성 라우터를 사용합니다.][performance-diagram]

Blob 저장소는 모든 사이트에서 파일을 복제 하는 방법에 대 한 tooworry 필요 없이 기본적으로 지역에 걸쳐 지리적으로 분산 합니다. 또한 Azure hello를 사용할 수 있습니다 [콘텐츠 배달 네트워크] [ cdn] 자세히 tooyour 방문자가 있는 파일 tooend 노드가 배포는 Blob 저장소에 대 한 합니다.

### <a name="planning"></a>계획
#### <a name="additional-requirements"></a>추가 요구 사항
| toodo이 중... | 사용 기능... |
| --- | --- |
| **대규모 파일 업로드 또는 저장** |[Blob Storage 사용을 위한 WordPress 플러그 인][storageplugin] |
| **메일 보내기** |[SendGrid] [ storesendgrid] 및 hello [SendGrid를 사용 하기 위한 WordPress 플러그 인][sendgridplugin] |
| **사용자 지정 도메인 이름** |[Azure App Service에서 사용자 지정 도메인 이름 구성][customdomain] |
| **HTTPS** |[Azure App Service에서 웹앱에 대한 HTTPS를 사용하도록 설정][httpscustomdomain] |
| **사전 프로덕션 유효성 검사** |[Azure App Service에서 웹앱에 대한 스테이징 환경 설정][staging] <p>웹 앱을 준비 tooproduction에서 이동 하면 hello WordPress 구성도 이동 합니다. 모든 설정이 지 프로덕션 응용 프로그램에 대 한 업데이트 된 toohello 요구 사항을 준비 하는 hello 앱 tooproduction 이동 하기 전에 있는지 확인 합니다.</p> |
| **모니터링 및 문제 해결** |[Azure App Service에서 웹앱에 대한 진단 로깅 사용하도록 설정][log] 및 [Azure App Service에서 Web Apps 모니터링][monitor] |
| **사이트 배포** |[Azure App Service에서 웹앱 배포][deploy] |

#### <a name="availability-and-disaster-recovery"></a>가용성 및 재해 복구
| toodo이 중... | 사용 기능... |
| --- | --- |
| **사이트 부하 분산** 또는 **사이트 지리적으로 분산** |[Azure Traffic Manager로 트래픽 라우팅][trafficmanager] |
| **백업 및 복원** |[Azure App Service에서 웹앱 백업][backup] 및 [Azure App Service에서 웹앱 복원][restore] |

#### <a name="performance"></a>성능
Hello 클라우드의 성능이 주로 캐싱 및 확장을 통해 이루어집니다. 그러나 hello 메모리, 대역폭 및 웹 응용 프로그램 호스트의 다른 특성 고려할 수 있습니다.

| toodo이 중... | 사용 기능... |
| --- | --- |
| **앱 서비스 인스턴스 기능 이해** |[App Service 계층의 기능을 비롯한 가격 책정 세부 정보][websitepricing] |
| **리소스 캐시** |[Redis 캐시][rediscache], [Memcache 클라우드](/gallery/store/garantiadata/memcached/), [MemCachier](/gallery/store/memcachier/memcachier/), 또는 중 하나 hello 캐싱 제공 되는 다른 hello [Azure 저장소](/gallery/store/) |
| **응용 프로그램 확장** |[Azure App Service에서 웹앱 크기 조정][websitescale] 및 [ClearDB 고가용성 라우팅][cleardbscale] Toohost를 선택 하 고 사용자 고유의 MySQL 설치를 관리 하는 경우 고려해 야 [MySQL 클러스터 CGE] [ cge] 확장에 대 한 합니다. |

#### <a name="migration"></a>마이그레이션
두 개의 메서드 toomigrate 기존 WordPress 사이트 tooAzure 앱 서비스

* **[WordPress 내보내기][export]**:이 메서드는 블로그의 hello 콘텐츠를 내보냅니다. Azure 앱 서비스에서 hello 콘텐츠 tooa 새 WordPress 사이트 hello를 사용 하 여 가져올 수 있습니다 [가져오기 WordPress 플러그 인][import]합니다.

  > [!NOTE]
  > 이 프로세스를 통해 콘텐츠를 마이그레이션할 수 있지만 플러그 인, 테마 또는 다른 사용자 지정 내용은 마이그레이션되지 않습니다. 이러한 구성 요소를 수동으로 다시 설치해야 합니다.
  >
  >
* **수동 마이그레이션**: [사이트를 백업] [ wordpressbackup] 및 [데이터베이스][wordpressdbbackup], 후 수동으로 복원 tooa 웹 응용 프로그램을 Azure에 앱 서비스 및 MySQL 데이터베이스를 연결된 합니다. 이 방법은 높은 수준으로 사용자는 유용한 toomigrate 사이트 hello 덜어 수동으로 플러그 인, 테마 및 기타 사용자 지정 설치를 방지 하기 때문에 합니다.

## <a name="step-by-step-instructions"></a>단계별 지침
### <a name="create-a-wordpress-site"></a>WordPress 사이트 만들기
1. 사용 하 여 hello [Azure 마켓플레이스] [ cdbnstore] toocreate hello에서 확인 된 hello 크기의 MySQL 데이터베이스 [아키텍처 및 계획](#planning) hello 영역 또는 영역 섹션 여기서 사이트 호스팅할 합니다.
2. Hello 단계에 따라 [Azure 앱 서비스에서 WordPress 웹 앱을 만들] [ createwordpress] toocreate WordPress 웹 응용 프로그램입니다. Hello 웹 응용 프로그램을 만들 때 선택 **기존 MySQL 데이터베이스를 사용 하 여**, 한 다음 1 단계에서 만든 hello 데이터베이스를 선택 합니다.

기존 WordPress 사이트를 마이그레이션하는 경우 참조 [기존 WordPress 사이트 tooAzure 마이그레이션할](#Migrate-an-existing-WordPress-site-to-Azure) 만들면 새 웹 앱입니다.

### <a name="migrate-an-existing-wordpress-site-tooazure"></a>기존 WordPress 사이트 tooAzure 마이그레이션
Hello에 설명 된 대로 [아키텍처 및 계획](#planning) 섹션에서 두 가지 방법으로 toomigrate WordPress 사이트는:

* **가져오기 및 내보내기를 사용 하 여** 많은 사용자 지정이 없는 또는 방금 toomove hello 콘텐츠를 원하는 사이트에 대 한 합니다.
* **사용 하 여 백업 및 복원** 저장할 toomove 모든 사용자 지정의 많은 사이트에 대 한 합니다.

사이트의 다음 섹션에서는 toomigrate hello 하나를 사용 합니다.

#### <a name="hello-export-and-import-method"></a>hello 내보내기 및 가져오기 방법을
1. 사용 하 여 [WordPress 내보내기] [ export] tooexport 기존 사이트입니다.
2. Hello hello 단계를 사용 하 여 웹 앱 만들기 [WordPress 사이트를 만들](#Create-a-new-WordPress-site) 섹션.
3. Hello에 tooyour WordPress 사이트에 로그인 [Azure 포털][mgmtportal], 클릭 하 고 **플러그 인** > **새로 추가**합니다. 검색 하 고 hello 설치 **WordPress 가져오기** 플러그 인 합니다.
4. Hello 가져오기 WordPress 플러그 인을 설치한 후 클릭 **도구** > **가져오기**, 클릭 하 고 **WordPress** toouse hello 가져오기 WordPress 플러그 인 합니다.
5. Hello에 **가져오기 WordPress** 페이지 **파일 선택**합니다. 기존 WordPress 사이트에서 내보낸 hello WXR 파일을 찾은 다음 클릭 **업로드 파일 및 가져오기**합니다.
6. **제출**을 클릭합니다. Hello 가져오기 작업이 성공 했다고 표시 됩니다.
7. 이러한 모든 단계를 완료 한 후 다시 시작에서 사이트의 **응용 프로그램 서비스** hello 블레이드 [Azure 포털][mgmtportal]합니다.

Hello 사이트를 가져온 후 tooperform hello hello 가져오기 파일에 포함 되지 않는 단계 tooenable 설정을 다음을 할 수 있습니다.

| 기존 설정... | 방법 |
| --- | --- |
| **Permalinks** |대시보드에서 hello WordPress hello 새 사이트의 클릭 **설정** > **고유 링크**, hello 고유 링크 구조를 업데이트 합니다. |
| **이미지/미디어 링크** |tooupdate 링크 toohello 새 위치, hello를 사용 하 여 [Velvet 파란색 업데이트 Url 플러그 인][velvet], 검색 및 바꾸기 도구를 선택 하거나 수동으로 데이터베이스의 hello 연결을 업데이트 합니다. |
| **테마** |너무 이동**모양** > **테마**, 한 다음 필요에 따라 hello 사이트 테마를 업데이트 합니다. |
| **메뉴** |테마에 메뉴를 지 원하는 경우 링크 tooyour 홈 페이지에는 hello 이전 하위 디렉터리에 있을 수 있습니다. 너무 이동**모양** > **메뉴**, 한 다음 적절히 업데이트 합니다. |

#### <a name="hello-backup-and-restore-method"></a>hello backup 및 restore 메서드
1. Hello에 있는 정보를 사용 하 여 사이트를 백업 하 여 기존 WordPress [WordPress 백업을][wordpressbackup]합니다.
2. Hello에 있는 정보를 사용 하 여 기존 데이터베이스를 백업 [데이터베이스 백업에][wordpressdbbackup]합니다.
3. 데이터베이스를 만들고 hello 백업을 복원 합니다.

   1. Hello에서 새 데이터베이스를 구입 [Azure 마켓플레이스][cdbnstore]에서 MySQL 데이터베이스를 설정 또는 [Windows] [ mysqlwindows] 또는 [Linux ] [ mysqllinux] 가상 컴퓨터.
   2. 와 마찬가지로 MySQL 클라이언트를 사용 하 여 [MySQL 워크 벤치] [ workbench] tooconnect toohello 새 데이터베이스를 선택한 WordPress 데이터베이스를 가져옵니다.
   3. Hello 데이터베이스 toochange hello 도메인 항목 tooyour 새 Azure 앱 서비스 도메인 예를 들어 mywordpress.azurewebsites.net를 업데이트 합니다. 사용 하 여 hello [찾기 및 바꾸기 WordPress 데이터베이스 스크립트에 대 한] [ searchandreplace] toosafely 모든 인스턴스를 변경 합니다.
4. Hello Azure 포털에서에서 웹 응용 프로그램을 만들고 hello WordPress 백업을 게시 합니다.

   1. hello에 데이터베이스를 사용 하는 웹 응용 프로그램이 toocreate [Azure 포털][mgmtportal], 클릭 **새로** > **웹 + 모바일**  >  **Azure 마켓플레이스** > **웹 앱** > **웹 응용 프로그램 + SQL** (또는 **웹 응용 프로그램 + MySQL**) > **만들**합니다. 모든 필요한 hello 설정을 toocreate 빈 웹 응용 프로그램을 구성 합니다.
   2. WordPress 백업에서 찾은 hello **wp config.php** 파일을 선택한 편집기에서 엽니다. 새 MySQL 데이터베이스에 대 한 hello 정보로 항목을 다음 hello를 바꿉니다.

      * **DB_NAME**: hello 데이터베이스의 hello 사용자 이름입니다.
      * **DB_USER**: hello 사용자 사용 되는 이름 tooaccess hello 데이터베이스입니다.
      * **DB_PASSWORD**: hello 사용자 암호입니다.

        이러한 항목을 변경한 후 저장 하 고 hello 닫습니다 **wp config.php** 파일입니다.
   3. 사용 하 여 hello [Azure 앱 서비스의 웹 앱을 배포] [ deploy] 정보 tooenable hello 배포 방법 toouse를 원하고 다음 Azure 앱 서비스에서 WordPress 백업 tooyour 웹 앱을 배포 합니다.
5. Hello WordPress 사이트를 배포한 후 있어야 수 tooaccess hello에 대 한 새 사이트 (앱 서비스 웹 응용 프로그램)으로 hello를 사용 하 여 *. azurewebsite.net hello 사이트 URL입니다.

### <a name="configure-your-site"></a>사이트 구성
Hello WordPress 사이트 생성 또는 마이그레이션된 된 후 정보 tooimprove 성능 다음 hello를 사용 하거나 추가 기능을 사용 하도록 설정 합니다.

| toodo이 중... | 사용 기능... |
| --- | --- |
| **앱 서비스 계획 모드, 크기 및 사용 크기 조정 설정** |[Azure App Service에서 웹앱 크기 조정][websitescale] |
| **영구 데이터베이스 연결 사용** |WordPress는 기본적으로 영구 데이터베이스 연결 후 다중 연결을 제한 하 여 연결 toohello 데이터베이스 toobecome를 일으킬 수 있는 사용 하지 않습니다. tooenable 영구 연결 설치 hello [영구 연결 어댑터 플러그 인](https://wordpress.org/plugins/persistent-database-connection-updater/installation/)합니다. |
| **성능 향상** |<ul><li><p><a href="https://azure.microsoft.com/en-us/blog/disabling-arrs-instance-affinity-in-windows-azure-web-sites/">Hello ARR 쿠키 사용 안 함</a>를 WordPress 여러 웹 응용 프로그램 인스턴스에서 실행 될 때 성능을 향상 시킬 수 있는 합니다.</p></li><li><p>캐싱을 사용하도록 설정합니다. 사용할 수 있습니다 <a href="http://msdn.microsoft.com/library/azure/dn690470.aspx">Redis 캐시</a> (미리 보기) hello로 <a href="https://wordpress.org/plugins/redis-object-cache/">Redis 캐시 WordPress 플러그 인 개체</a>, hello 중 hello에서 기타 캐싱 서비스를 사용할 수 있습니다 또는 <a href="/gallery/store/">Azure Store</a>합니다.</p></li><li><p>[Wincache로 WordPress 더 빠르게 만들기](https://wordpress.org/plugins/w3-total-cache/) Wincache는 기본적으로 웹앱에 대해 사용되도록 설정되어 있습니다. WinCache 및 동적 캐시를 함께 사용할 때 WinCache의 파일 캐시를 해제 하지만 hello 사용자 및 사용 하도록 설정 하는 세션 캐시를 유지 합니다. 파일 캐시는 시스템 수준.ini 파일에서 해제 tooturn hello 다음 값을 설정 합니다.<br/><code>wincache.fcenabled = 0</code></p></li><li><p>[Azure App Service에서 웹앱 크기를 조정][websitescale]하고 <a href="http://www.cleardb.com/developers/cdbr/introduction">ClearDB 고가용성 라우팅</a> 또는 <a href="http://www.mysql.com/products/cluster/">MySQL 클러스터 CGE</a>를 사용합니다.</p></li></ul> |
| **저장소에 Blob 사용** |<ol><li><p>[Azure Storage 계정 만들기](../storage/common/storage-create-storage-account.md)</p></li><li><p>너무 방법에 대해 알아봅니다[사용 하 여 hello 콘텐츠 배포 네트워크](../cdn/cdn-create-new-endpoint.md) toogeo-blob에 저장 된 데이터를 배포 합니다.</p></li><li><p>설치 및 구성 hello <a href="https://wordpress.org/plugins/windows-azure-storage/">WordPress 플러그 인에 대 한 Azure 저장소</a>합니다.</p><p>자세한 설정 및 hello 플러그 인에 대 한 구성 정보에 대 한 참조 hello <a href="http://plugins.svn.wordpress.org/windows-azure-storage/trunk/UserGuide.docx">사용자 가이드</a>합니다.</p> </li></ol> |
| **전자 메일 사용** |사용 하도록 설정 <a href="https://azure.microsoft.com/en-us/marketplace/partners/sendgrid/sendgrid-azure/">SendGrid</a> hello Azure 저장소를 사용 하 여 합니다. Hello 설치 <a href="http://wordpress.org/plugins/sendgrid-email-delivery-simplified">SendGrid 플러그 인</a> WordPress에 대 한 합니다. |
| **사용자 지정 도메인 이름 구성** |[Azure App Service에서 사용자 지정 도메인 이름 구성][customdomain] |
| **사용자 지정 도메인 이름에 HTTPS 사용** |[Azure App Service에서 웹앱에 대한 HTTPS를 사용하도록 설정][httpscustomdomain]. |
| **사이트 부하 분산 또는 지리적으로 분산** |[Azure Traffic Manager로 트래픽 라우팅][trafficmanager] 사용자 지정 도메인을 사용 하는 경우 참조 [Azure 앱 서비스에서 사용자 지정 도메인 이름을 구성] [ customdomain] 방법에 대 한 정보에 대 한 사용자 지정 도메인 이름이 트래픽 관리자 toouse 합니다. |
| **자동 백업 사용** |[Azure App Service에서 웹앱 백업][backup] |
| **진단 로깅 사용** |[Azure App Service에서 웹앱에 대한 진단 로깅 사용하도록 설정][log] |

## <a name="next-steps"></a>다음 단계
* [WordPress 최적화](http://codex.wordpress.org/WordPress_Optimization)
* [Azure 앱 서비스에서 WordPress toomultisite 변환](web-sites-php-convert-wordpress-multisite.md)
* [Azure용 ClearDB 업그레이드 마법사](http://www.cleardb.com/store/azure/upgrade)
* [Azure 앱 서비스에서 웹앱의 하위 폴더에 WordPress 호스팅](http://blogs.msdn.com/b/webapps/archive/2013/02/13/hosting-wordpress-in-a-subfolder-of-your-windows-azure-web-site.aspx)
* [단계별: Azure를 사용하여 WordPress 사이트 만들기](http://blogs.technet.com/b/blainbar/archive/2013/08/07/article-create-a-wordpress-site-using-windows-azure-read-on.aspx)
* [Azure에 기존 WordPress 블로그 호스트](http://blogs.msdn.com/b/msgulfcommunity/archive/2013/08/26/migrating-a-self-hosted-wordpress-blog-to-windows-azure.aspx)
* [WordPress에서 깔끔한 고정 링크 사용](http://www.iis.net/learn/extensions/url-rewrite-module/enabling-pretty-permalinks-in-wordpress)
* [어떻게 toomigrate Azure 앱 서비스에서 WordPress 블로그를 실행 합니다.](http://www.kefalidis.me/2012/06/how-to-migrate-and-run-your-wordpress-blog-on-windows-azure-websites/)
* [Toorun WordPress Azure 앱 서비스를 해제 하는 방법](http://architects.dzone.com/articles/how-run-wordpress-azure)
* [2분 이내의 Azure WordPress](http://www.sitepoint.com/wordpress-windows-azure-2-minutes-less/)
* [이동 WordPress 블로그 tooAzure-1 부: Azure에서 WordPress 블로그 만들기](http://www.davebost.com/2013/07/10/moving-a-wordpress-blog-to-windows-azure-part-1)
* [이동 WordPress 블로그 tooAzure-2 부: 콘텐츠를 전송 합니다.](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-transferring-your-content)
* [이동 WordPress 블로그 tooAzure-3 부: 사용자 지정 도메인 설정](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-3-setting-up-your-custom-domain)
* [WordPress 블로그 tooAzure-4 부 이동: 정말 고유 링크 및 URL 재작성 규칙](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-4-pretty-permalinks-and-url-rewrite-rules)
* [WordPress 블로그 tooAzure-5 부 이동: 하위 폴더 toohello 루트에서 이동](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-5-moving-from-a-subfolder-to-the-root)
* [어떻게는 WordPress tooset 웹 Azure 계정에는 앱](http://www.itexperience.net/2014/01/20/how-to-set-up-a-wordpress-website-in-your-windows-azure-account/)
* [Azure에서 WordPress 지원](http://www.johnpapa.net/wordpress-on-azure/)
* [Azure의 WordPress 관련 팁](http://www.johnpapa.net/azurecleardbmysql/)

> [!NOTE]
> Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다. 신용 카드는 필요하지 않으며 약정은 없습니다.
>
>

## <a name="whats-changed"></a>변경된 내용
가이드 toohello 변경 tooApp 웹 사이트 서비스에서에서 참조 [Azure 앱 서비스와 기존 Azure 서비스에 미치는 영향은](http://go.microsoft.com/fwlink/?LinkId=529714)합니다.

<!-- URL List -->

[performance-diagram]: ./media/web-sites-php-enterprise-wordpress/performance-diagram.png
[basic-diagram]: ./media/web-sites-php-enterprise-wordpress/basic-diagram.png
[multi-region-diagram]: ./media/web-sites-php-enterprise-wordpress/multi-region-diagram.png
[wordpress]: http://www.microsoft.com/web/wordpress
[officeblog]: http://blogs.office.com/
[bingblog]: http://blogs.bing.com/
[cdbnstore]: http://www.cleardb.com/store/azure
[storageplugin]: https://wordpress.org/plugins/windows-azure-storage/
[sendgridplugin]: http://wordpress.org/plugins/sendgrid-email-delivery-simplified/
[phpwebsite]: web-sites-php-configure.md
[customdomain]: app-service-web-tutorial-custom-domain.md
[trafficmanager]: ../traffic-manager/traffic-manager-overview.md
[backup]: web-sites-backup.md
[restore]: web-sites-restore.md
[rediscache]: https://azure.microsoft.com/documentation/services/redis-cache/
[managedcache]: http://msdn.microsoft.com/library/azure/dn386122.aspx
[websitescale]: web-sites-scale.md
[managedcachescale]: http://msdn.microsoft.com/library/azure/dn386113.aspx
[cleardbscale]: http://www.cleardb.com/developers/cdbr/introduction
[staging]: web-sites-staged-publishing.md
[monitor]: web-sites-monitor.md
[log]: web-sites-enable-diagnostic-log.md
[httpscustomdomain]: app-service-web-tutorial-custom-ssl.md
[mysqlwindows]:../virtual-machines/windows/classic/mysql-2008r2.md
[mysqllinux]:../virtual-machines/linux/classic/mysql-on-opensuse.md
[cge]: http://www.mysql.com/products/cluster/
[websitepricing]: /pricing/details/app-service/
[export]: http://en.support.wordpress.com/export/
[import]: http://wordpress.org/plugins/wordpress-importer/
[wordpressbackup]: http://wordpress.org/plugins/wordpress-importer/
[wordpressdbbackup]: http://codex.wordpress.org/Backing_Up_Your_Database
[createwordpress]: web-sites-php-web-site-gallery.md
[velvet]: https://wordpress.org/plugins/velvet-blues-update-urls/
[mgmtportal]: https://portal.azure.com/
[wordpressbackup]: http://codex.wordpress.org/WordPress_Backups
[wordpressdbbackup]: http://codex.wordpress.org/Backing_Up_Your_Database
[workbench]: http://www.mysql.com/products/workbench/
[searchandreplace]: http://interconnectit.com/124/search-and-replace-for-wordpress-databases/
[deploy]: web-sites-deploy.md
[posh]: /powershell/azureps-cmdlets-docs
[Azure CLI]:../cli-install-nodejs.md
[storesendgrid]: https://azure.microsoft.com/marketplace/partners/sendgrid/sendgrid-azure/
[cdn]: ../cdn/cdn-overview.md
