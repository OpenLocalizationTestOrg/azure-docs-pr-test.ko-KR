---
title: "모바일 서비스 tooan 앱 서비스 모바일 앱에서 aaaMigrate"
description: "Tooeasily 모바일 서비스 응용 프로그램 tooan 앱 서비스 모바일 앱을 마이그레이션 방법에 대해 알아봅니다"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 07507ea2-690f-4f79-8776-3375e2adeb9e
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: glenga
ms.openlocfilehash: cd2e8d98595703389300b79da9bf51cdcefe7b40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="article-top"></a>마이그레이션에 기존 Azure 모바일 서비스 tooAzure 앱 서비스
Hello로 [Azure 앱 서비스의 일반적인 가용성], Azure 모바일 서비스 사이트를 쉽게 수 마이그레이션된 내부 tootake hello Azure 앱 서비스의 모든 기능을 활용 합니다.  이 문서에서는 Azure Mobile Services tooAzure 앱 서비스에서에서 사이트를 마이그레이션하는 경우 어떤 tooexpect를 설명 합니다.

## <a name="what-does-migration-do"></a>마이그레이션을 수행 하는 tooyour 사이트
Azure 모바일 서비스의 마이그레이션 설정에 모바일 서비스는 [Azure 앱 서비스] hello 코드에 영향을 주지 않고 응용 프로그램입니다.  Notification Hubs, SQL 데이터 연결, 인증 설정, 예약된 작업 및 도메인 이름은 변경되지 않습니다.  Azure 모바일 서비스를 사용 하 여 모바일 클라이언트 toooperate를 정상적으로 계속 합니다.  마이그레이션 전송된 tooAzure 앱 서비스 되 면 서비스를 다시 시작 합니다.

[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

## <a name="why-migrate"></a>사이트를 마이그레이션해야 하는 이유
Microsoft는 포함 하 여 Azure 앱 서비스의 hello 기능에 Azure 모바일 서비스 tootake 활용 마이그레이션하는 권장:

* [WebJobs] 및 [사용자 지정 도메인 이름]을 포함하는 새로운 호스트 기능.
* 연결 tooyour 온-프레미스 리소스를 사용 하 여 [VNet] 또한 너무[하이브리드 연결]합니다.
* New Relic 또는 [Application Insights]를 통한 모니터링 및 문제 해결.
* [스테이징 슬롯], 롤백 및 프로덕션 내 테스트를 포함하는 기본 제공 DevOps 도구.
* [자동 크기 조정], 부하 분산 및 [성능 모니터링].

Azure 앱 서비스의 hello 이점에 자세한 내용은 참조 hello [모바일 서비스 vs. App Service] 항목을 참조하세요.

## <a name="before-you-begin"></a>시작하기 전에
사이트에서 주요 작업을 시작하기 전에 모바일 서비스 스크립트와 SQL Database를 백업해야 합니다.

## <a name="migrating-site"></a>사이트 마이그레이션
hello 마이그레이션 프로세스는 단일 Azure 지역에 있는 모든 사이트를 마이그레이션합니다.

toomigrate 사이트:

1. Toohello 로그인 [Azure 클래식 포털]합니다.
2. 모바일 서비스를 선택 하 시겠습니까 toomigrate hello 지역에 있습니다.
3. Hello 클릭 **tooApp 서비스 마이그레이션** 단추입니다.

   ![hello 마이그레이션 단추][0]
4. Hello 마이그레이션 tooApp 서비스 대화 상자를 읽습니다.
5. 제공 된 hello 상자에 모바일 서비스의 hello 이름을 입력 합니다.  예를 들어 도메인 이름이 contoso.azure mobile.net 이면 다음를 입력 *contoso* hello 상자를 제공 합니다.
6. Hello 눈금 단추를 클릭 합니다.

Hello hello 작업 모니터에서 hello 마이그레이션 상태를 모니터링 합니다. 사이트가로 나열 되어 *마이그레이션* hello Azure 클래식 포털의에서.

  ![마이그레이션 작업 모니터링][1]

각 마이그레이션에서 마이그레이션 중인 모바일 서비스 당 3 too15 분 걸릴 수 있습니다.  Hello 마이그레이션하는 동안 사이트에 계속 사용할 수 있습니다.
사이트는 hello hello 마이그레이션 프로세스가 끝날 때 다시 시작 됩니다.  몇 초 정도 지속 되는 hello 다시 시작 프로세스 중에 hello 사이트를 사용할 수 없습니다.

## <a name="finalizing-migration"></a>Hello 마이그레이션을 완료 하는 중
Tootest hello 마이그레이션 프로세스의 hello 결론에 모바일 클라이언트에서 사이트를 계획 합니다.  Toohello 모바일 클라이언트 변경 하지 않고 모든 일반적인 클라이언트 작업을 수행할 수 있는지 확인 합니다.  

### <a name="update-app-service-tier"></a>적절한 앱 서비스 가격 책정 계층 선택
가격 tooAzure 앱 서비스를 마이그레이션한 후에 더 많은 유연성이 있습니다.

1. Toohello 로그인 [Azure 포털]합니다.
2. 선택 **모든 리소스** 또는 **응용 프로그램 서비스** 마이그레이션된 모바일 서비스의 hello 이름을 클릭 합니다.
3. 기본적으로 hello 설정 블레이드에서가 열립니다.
4. 클릭 **앱 서비스 계획** hello 설정 메뉴에서 합니다.
5. Hello 클릭 **가격 책정 계층** 바둑판식으로 배열입니다.
6. Hello 타일 적절 한 tooyour 요구 사항를 클릭 한 다음 클릭 **선택**합니다.  TooClick 할 수 있습니다 **모든 보기** toosee hello 가격 책정 계층을 사용할 수 있습니다.

시작 지점으로 계층을 따라 hello를 것이 좋습니다.

| 모바일 서비스 가격 책정 계층 | 앱 서비스 가격 책정 계층 |
|:--- |:--- |
| 무료 |F1 무료 |
| Basic |B1 기본 |
| 표준 |S1 표준 |

Hello 오른쪽 가격대 키를 눌러 응용 프로그램에 대 한 중요 한 선택 유연성이 있습니다.  너무 참조[앱 서비스 가격 책정] hello 새 앱 서비스 가격 정보.

> [!TIP]
> hello 표준으로 서비스 응용 프로그램 계층 기능이 포함 되어 액세스 toomany toouse, 경우가 포함 하 여 [스테이징 슬롯], 자동 백업 되 고, 자동 크기 조정 합니다.  발생 된 hello 새로운 기능을 확인해 보십시오.
>
>

### <a name="review-migration-scheduler-jobs"></a>Hello 마이그레이션된 스케줄러 작업을 검토
스케줄러 작업은 마이그레이션 후에 약 30분까지 표시되지 않습니다.  Toorun hello 백그라운드에서 계속 하는 예약 된 작업입니다.
tooview 다시 표시 되 후 예약 된 작업:

1. Toohello 로그인 [Azure 포털]합니다.
2. 선택 **찾아보기 >**, 입력 **일정** hello에 *필터* 상자를 선택한 다음 선택 **스케줄러 컬렉션**합니다.

마이그레이션 후에 사용 가능한 무료 스케줄러 작업의 수가 제한됩니다.  사용 및 hello 검토 [Azure 스케줄러 계획]합니다.

### <a name="configure-cors"></a>필요한 경우 CORS 구성
크로스-원본 자원 공유 기법 tooallow 웹 사이트 tooaccess 다른 도메인의 웹 API입니다.  연결 된 웹 사이트와 Azure 모바일 서비스를 사용 하는 hello 마이그레이션의 일부로 CORS tooconfigure를 할 수 있습니다.  모바일 장치에서 단독으로 Azure 모바일 서비스를 액세스 하면 다음 CORS 드문 경우에서를 제외 하 고 구성 toobe를 필요 하지 않습니다.

마이그레이션된 CORS 설정에는 hello로 사용할 수 **MS_CrossDomainWhitelist** 앱 설정 합니다.  toomigrate 프로그램 사이트 toohello 앱 서비스의 CORS 기능:

1. Toohello 로그인 [Azure 포털]합니다.
2. 선택 **모든 리소스** 또는 **응용 프로그램 서비스** 마이그레이션된 모바일 서비스의 hello 이름을 클릭 합니다.
3. 기본적으로 hello 설정 블레이드에서가 열립니다.
4. 클릭 **CORS** hello API 메뉴에 있습니다.
5. 한 다음 Enter 키를 제공 된 hello 상자에 허용 된 원본을 입력 하십시오.
6. Origin 허용 목록이 잘못 되 면 hello 저장 단추를 클릭 합니다.

> [!TIP]
> Hello에 웹 사이트와 모바일 서비스를 실행할 수는 Azure 응용 프로그램 서비스를 사용 하 여 hello 이점 중 하나는 사이트입니다.  자세한 내용은 참조 hello [다음 단계](#next-steps) 섹션.
>
>

### <a name="download-publish-profile"></a>새 게시 프로필 다운로드
사이트의 게시 프로필 hello tooAzure 앱 서비스를 마이그레이션할 때 변경 됩니다.  Visual Studio에서 사이트를 toopublish을 가져오려는 경우 새 게시 프로필을 해야 합니다.  toodownload hello 새 게시 프로필:

1. Toohello 로그인 [Azure 포털]합니다.
2. 선택 **모든 리소스** 또는 **응용 프로그램 서비스** 마이그레이션된 모바일 서비스의 hello 이름을 클릭 합니다.
3. **게시 프로필 가져오기**를 클릭합니다.

hello PublishSettings 파일은 다운로드 한 tooyour 컴퓨터입니다.  일반적으로 파일 이름은 *sitename*.PublishSettings입니다.  가져오기 hello 게시 하 여 기존 프로젝트에는 설정:

1. Visual Studio 및 Azure 모바일 서비스 프로젝트를 엽니다.
2. Hello에서 프로젝트를 마우스 오른쪽 단추로 클릭 **솔루션 탐색기** 선택 **게시...**
3. **가져오기**를 클릭합니다.
4. **찾아보기**를 클릭하고 다운로드한 게시 설정 파일을 선택합니다.  **확인**
5. 클릭 **연결 유효성 검사** tooensure hello 설정 작업을 게시 합니다.
6. 클릭 **게시** toopublish 사이트입니다.

## <a name="working-with-your-site"></a>마이그레이션 후에 사이트로 작업
Hello에 새 앱 서비스에서 작업 시작 [Azure 포털] 마이그레이션 후 합니다.  hello는 다음과 같은 hello에 tooperform를 사용 하는 특정 작업에 대 한 몇 가지 메모 [Azure 클래식 포털]앱 서비스 동등한 함께 합니다.

### <a name="publishing-your-site"></a>마이그레이션된 사이트 다운로드 및 게시
사이트는 git 또는 ftp를 통해 사용될 수 있고 WebDeploy, TFS, Mercurial, GitHub, FTP 등 다양한 메커니즘을 사용하여 다시 게시될 수 있습니다.  배포 자격 증명 hello hello 나머지 사이트도 마이그레이션됩니다.  배포 자격 증명을 설정하지 않거나 기억하지 못하는 경우 다시 설정할 수 있습니다.

1. Toohello 로그인 [Azure 포털]합니다.
2. 선택 **모든 리소스** 또는 **응용 프로그램 서비스** 마이그레이션된 모바일 서비스의 hello 이름을 클릭 합니다.
3. 기본적으로 hello 설정 블레이드에서가 열립니다.
4. 클릭 **배포 자격 증명** hello 게시 메뉴에에서 있습니다.
5. Hello 새 배포 자격 증명도 제공 하는 hello 상자에 입력 한 다음 hello 저장 단추를 클릭 합니다.

Git와 함께 이러한 자격 증명 tooclone hello 사이트를 사용 하거나 GitHub, TFS 또는 Mercurial에서 자동화 된 배포를 설정할 수 있습니다.  자세한 내용은 참조 hello [Azure 앱 서비스 배포 설명서]합니다.

### <a name="appsettings"></a>응용 프로그램 설정
마이그레이션된 모바일 서비스에 대한 설정은 대부분 앱 설정을 통해 사용할 수 있습니다.  Hello에서 hello 응용 프로그램 설정 목록이 가져올 수 있습니다 [Azure 포털]합니다.
tooview 응용 프로그램 설정을 변경 합니다.

1. Toohello 로그인 [Azure 포털]합니다.
2. 선택 **모든 리소스** 또는 **응용 프로그램 서비스** 마이그레이션된 모바일 서비스의 hello 이름을 클릭 합니다.
3. 기본적으로 hello 설정 블레이드에서가 열립니다.
4. 클릭 **응용 프로그램 설정** hello 일반 메뉴에 있습니다.
5. 응용 프로그램 설정 섹션 toohello 스크롤하여 응용 프로그램 설정의 찾을 합니다.
6. Hello 앱 설정 tooedit hello 값의 hello 값을 클릭 합니다.  클릭 **저장** toosave hello 값입니다.

Hello에서 여러 앱 설정을 업데이트할 수 있습니다 동시 합니다.

> [!TIP]
> 두 가지 응용 프로그램 설정을 hello로 동일한 값입니다.  예를 들어 *ApplicationKey* 및 *MS\_ApplicationKey*를 확인할 수 있습니다.  Hello에 두 응용 프로그램 설정을 업데이트 같은 시간입니다.
>
>

### <a name="authentication"></a>인증
모든 인증 설정은 마이그레이션된 사이트에서 앱 설정으로 사용할 수 있습니다.  tooupdate 인증 설정에 적절 한 응용 프로그램 설정을 변경 해야 합니다.  hello 아래 표에 나와 인증 공급자에 대 한 hello 적절 한 응용 프로그램 설정.

| 공급자 | 클라이언트 ID | 클라이언트 암호 | 기타 설정 |
|:--- |:--- |:--- |:--- |
| Microsoft 계정 |**MS\_MicrosoftClientID** |**MS\_MicrosoftClientSecret** |**MS\_MicrosoftPackageSID** |
| Facebook |**MS\_FacebookAppID** |**MS\_FacebookAppSecret** | |
| Twitter |**MS\_TwitterConsumerKey** |**MS\_TwitterConsumerSecret** | |
| Google |**MS\_GoogleClientID** |**MS\_GoogleClientSecret** | |
| Azure AD |**MS\_AadClientID** | |**MS\_AadTenants** |

참고: **MS\_AadTenants** 테 넌 트 도메인 (hello hello 모바일 서비스 포털에서 필드 "허용 테 넌 트")의 쉼표로 구분 된 목록으로 저장 됩니다.

> [!WARNING]
> **Hello 설정 메뉴에서 hello 인증 메커니즘을 사용 하지 않습니다**
>
> Azure 앱 서비스는 hello에서 별도 "코드 없음" 인증 및 권한 부여 시스템 제공 *인증 / 권한 부여* 설정 메뉴 및 (사용 되지 않음) hello *모바일 인증* hello 설정 메뉴에서 옵션입니다.  이러한 옵션은 마이그레이션된 Azure 모바일 서비스와 호환되지 않습니다.  할 수 있습니다 [사이트 업그레이드](app-service-mobile-net-upgrading-from-mobile-services.md) hello Azure 앱 서비스 인증 tootake 활용 합니다.
>
>

### <a name="easytables"></a>데이터
hello *데이터* 모바일 서비스에서 탭으로 대체 되었습니다 *쉽게 테이블* hello Azure 포털 내에서.  tooaccess 쉽게 테이블:

1. Toohello 로그인 [Azure 포털]합니다.
2. 선택 **모든 리소스** 또는 **응용 프로그램 서비스** 마이그레이션된 모바일 서비스의 hello 이름을 클릭 합니다.
3. 기본적으로 hello 설정 블레이드에서가 열립니다.
4. 클릭 **쉽게 테이블** hello 모바일 메뉴에 있습니다.

Hello를 클릭 하 여 테이블을 추가할 수 있습니다 **추가** 단추 또는 테이블 이름을 클릭 하 여 기존 테이블에 액세스 합니다.  다음을 비롯하여 이 블레이드에서 할 수 있는 다양한 작업이 있습니다.

* 테이블 사용 권한 변경
* Hello 작업 스크립트를 편집합니다.
* Hello 테이블 스키마 관리
* Hello 테이블 삭제
* Hello 테이블 내용 지우기
* Hello 테이블의 특정 행 삭제

### <a name="easyapis"></a>API
hello *API* 모바일 서비스에서 탭으로 대체 되었습니다 *쉽게 Api* hello Azure 포털 내에서.  tooaccess 쉽게 Api:

1. Toohello 로그인 [Azure 포털]합니다.
2. 선택 **모든 리소스** 또는 **응용 프로그램 서비스** 마이그레이션된 모바일 서비스의 hello 이름을 클릭 합니다.
3. 기본적으로 hello 설정 블레이드에서가 열립니다.
4. 클릭 **쉽게 Api** hello 모바일 메뉴에 있습니다.

마이그레이션된 Api는 이미 hello 블레이드에 나열 됩니다.  또한 이 블레이드에서 API를 추가할 수 있습니다.  특정 API toomanage hello API를 클릭 합니다.
Hello 새 블레이드에서 hello 사용 권한 조정 하 고 hello API에 대 한 hello 스크립트를 편집할 수 있습니다.

### <a name="on-demand-jobs"></a>스케줄러 작업
모든 스케줄러 작업은 스케줄러 작업 컬렉션 섹션 hello를 통해 사용할 수 있습니다.  tooaccess 스케줄러 작업:

1. Toohello 로그인 [Azure 포털]합니다.
2. 선택 **찾아보기 >**, 입력 **일정** hello에 *필터* 상자를 선택한 다음 선택 **스케줄러 컬렉션**합니다.
3. 사이트에 대 한 hello 작업 컬렉션을 선택 합니다.  *sitename*-Jobs로 이름이 지정됩니다.
4. **설정**을 클릭합니다.
5. 관리 아래에 있는 **스케줄러 작업**을 클릭합니다.

마이그레이션을 시작 하기 전에 지정한 hello 빈도로 예약 된 작업이 표시 됩니다.  주문형 작업은 사용할 수 없게 설정 됩니다.  toorun 주문형 작업:

1. Toorun hello 작업을 선택 합니다.
2. 필요한 경우 클릭 **사용** tooenable hello 작업 합니다.
3. **설정**을 클릭한 다음 **일정**을 클릭합니다.
4. **한 번** 되풀이를 선택한 다음 **저장**을 클릭합니다.

요청 시 작업은 `App_Data/config/scripts/scheduler post-migration`에 위치합니다.  모든 주문형 작업은 너무 변환 하는 것이 좋습니다[WebJobs] 또는 [Functions]합니다.  [WebJobs] 또는 [Functions]로 새 스케줄러 작업을 작성합니다.

### <a name="notification-hubs"></a>알림 허브
모바일 서비스는 푸시 알림에 알림 허브를 사용합니다.  앱 설정에 따라 hello 마이그레이션 후 사용 되는 toolink hello 알림 허브 tooyour 모바일 서비스에는:

| 응용 프로그램 설정 | 설명 |
|:--- |:--- |
| **MS\_PushEntityNamespace** |알림 허브 Namespace hello |
| **MS\_NotificationHubName** |hello 알림 허브 이름 |
| **MS\_NotificationHubConnectionString** |hello 알림 허브 연결 문자열 |
| **MS\_NamespaceName** |MS_PushEntityNamespace에 대한 별칭 |

알림 허브는 hello을 통해 관리 [Azure 포털]합니다.  Hello 알림 허브 이름 (이 찾을 수 있습니다 hello 응용 프로그램 설정을 사용 하 여) note:

1. Toohello 로그인 [Azure 포털]합니다.
2. **찾아보기**>를 선택한 다음 **Notification Hubs**를 선택합니다.
3. Hello 모바일 서비스와 연결 된 hello 알림 허브 이름을 클릭 합니다.

> [!NOTE]
> Notification Hubs가 "혼합" 형식이면 표시되지 않습니다.  "혼합" 형식 알림 허브는 알림 허브 및 레거시 서비스 버스 기능을 모두 활용합니다.  계속하기 전에 [혼합 네임스페이스를 변환]합니다.  Hello 변환이 완료 되 면 알림 허브 hello가 표시 [Azure 포털]합니다.
>
>

자세한 내용을 보려면 검토 hello [알림 허브] 설명서입니다.

> [!TIP]
> Hello에 알림 허브 관리 기능 [Azure 포털] 미리 보기에서 계속 됩니다.  hello [Azure 클래식 포털] 모든 알림 허브를 관리 하기 위한 사용 가능한 상태로 유지 합니다.
>
>

### <a name="legacy-push"></a>레거시 푸시 설정
사용 하는 알림 허브에 hello 소개 하기 전에 모바일 서비스에 푸시를 구성한 경우 *기존 푸시*합니다.  사용 중인 푸시 구성에 Notification Hubs가 표시되지 않으면 *레거시 푸시*가 사용되는 것입니다.  이 기능은 다른 기능과 함께 마이그레이션됩니다.  그러나 hello 마이그레이션이 완료 된 후에 곧 tooNotification 허브를 업그레이드 하는 것이 좋습니다.

중간 hello, 모든 hello 기존 푸시 설정 (주목할 만한 예외 hello APNS 인증서의 hello)에서 사용할 수 있습니다 앱 설정 합니다.  Hello hello 파일 시스템에 적합 한 파일을 대체 하 여 hello APNS 인증서를 업데이트 합니다.

### <a name="app-settings"></a>기타 앱 설정
추가 응용 프로그램 설정은 다음 hello은 모바일 서비스에서 마이그레이션된 및에서 사용할 수 있는 *설정* > *앱 설정*:

| 응용 프로그램 설정 | 설명 |
|:--- |:--- |
| **MS\_MobileServiceName** |앱의 hello 이름 |
| **MS\_MobileServiceDomainSuffix** |hello 도메인 접두사입니다. 예: azure-mobile.net |
| **MS\_ApplicationKey** |응용 프로그램 키 |
| **MS\_MasterKey** |앱 마스터 키 |

hello 응용 프로그램 키와 마스터 키에는 원래 모바일 서비스에서 동일한 toohello 응용 프로그램 키가 있습니다.  특히, 응용 프로그램 키 hello hello 모바일 API의 사용을 toovalidate 모바일 클라이언트에서 전송 됩니다.

### <a name="cliequivalents"></a>해당하는 명령줄
Hello를 더 이상 사용할 수 *azure 모바일* toomanage Azure 모바일 서비스 사이트 명령입니다.  다양 한 함수 hello로 대체 되었습니다 대신 *azure 사이트* 명령입니다.  다음 테이블 toofind 해당 하는 일반적인 명령에 대 한 hello를 사용 합니다.

| *Azure 모바일* 명령 | 해당하는 *Azure 사이트* 명령 |
|:--- |:--- |
| 모바일 위치 |사이트 위치 목록 |
| 모바일 목록 |사이트 목록 |
| mobile show *name* |site show *name* |
| mobile restart *name* |site restart *name* |
| mobile redeploy *name* |site deployment redeploy *commitId* *name* |
| mobile key set *name* *type* *value* |site appsetting delete *key* *name* <br/> site appsetting add *key*=*value* *name* |
| mobile config list *name* |site appsetting list *name* |
| mobile config get *name* *key* |site appsetting show *key* *name* |
| mobile config set *name* *key* |site appsetting delete *key* *name* <br/> site appsetting add *key*=*value* *name* |
| mobile domain list *name* |site domain list *name* |
| mobile domain add *name* *domain* |site domain add *domain* *name* |
| mobile domain delete *name* |site domain delete *domain* *name* |
| mobile scale show *name* |site show *name* |
| mobile scale change *name* |site scale mode *mode* *name* <br /> site scale instances *instances* *name* |
| mobile appsetting list *name* |site appsetting list *name* |
| mobile appsetting add *name* *key* *value* |site appsetting add *key*=*value* *name* |
| mobile appsetting delete *name* *key* |site appsetting delete *key* *name* |
| mobile appsetting show *name* *key* |site appsetting delete *key* *name* |

인증 또는 푸시 알림 설정을 업데이트 하 여 적절 한 응용 프로그램 설정 hello를 업데이트 합니다.
ftp 또는 git를 통해 파일을 편집하고 사이트를 게시합니다.

### <a name="diagnostics"></a>진단 및 로깅
Azure 앱 서비스에서 정상적으로 진단 로깅을 사용합니다.  tooenable 진단 로깅:

1. Toohello 로그인 [Azure 포털]합니다.
2. 선택 **모든 리소스** 또는 **응용 프로그램 서비스** 마이그레이션된 모바일 서비스의 hello 이름을 클릭 합니다.
3. 기본적으로 hello 설정 블레이드에서가 열립니다.
4. 선택 **진단 로그** hello 기능 메뉴.
5. 클릭 **ON** hello 다음 로그에 대 한: **응용 프로그램 로깅 (파일 시스템)**, **자세한 오류 메시지**, 및 **실패 한 요청 추적**
6. 웹 서버 로깅에서 **파일 시스템** 을 클릭합니다.
7. 페이지 맨 아래에 있는 **저장**

tooview hello 로그:

1. Toohello 로그인 [Azure 포털]합니다.
2. 선택 **모든 리소스** 또는 **응용 프로그램 서비스** 마이그레이션된 모바일 서비스의 hello 이름을 클릭 합니다.
3. Hello 클릭 **도구** 단추
4. 선택 **로그 스트림** hello 관찰 메뉴.

로그는 생성 될 때 hello 창에 표시 됩니다.  배포 자격 증명을 사용 하 여 나중에 분석에 대 한 hello 로그를 다운로드할 수 있습니다. 자세한 내용은 참조 hello [로깅] 설명서입니다.

## <a name="known-issues"></a>알려진 문제
### <a name="deleting-a-migrated-mobile-app-clone-causes-a-site-outage"></a>마이그레이션된 모바일 앱 복제를 삭제하면 사이트 중단이 발생함
Azure PowerShell delete hello 복제를 사용 하 여 마이그레이션된 모바일 서비스를 복제 하면 hello 프로덕션 서비스에 대 한 DNS 항목이 제거 됩니다.  사이트는 hello 인터넷에서에서 액세스할 수 없습니다.  

해결 방법: 사이트 tooclone을 원할 경우 그렇게 hello 포털을 통해.

### <a name="changing-webconfig-does-not-work"></a>Web.config를 변경할 수 없습니다.
ASP.NET 사이트를 사용 하는 경우 변경 toohello `Web.config` 파일 적용 되지 않습니다.  Azure 앱 서비스 hello 적절 한 빌드 `Web.config` 시작 toosupport hello 모바일 서비스 런타임에 파일입니다.  XML 변환 파일을 사용하여 특정 설정(예: 사용자 지정 헤더)를 재정의할 수 있습니다.  파일 만들기에 호출 `applicationHost.xdt` -hello에이 파일 끝나야 `D:\home\site` 디렉터리 hello Azure 서비스에 있습니다.  사용자 지정 배포 스크립트를 통하거나 Kudu를 사용하여 `applicationHost.xdt` 파일을 업로드합니다.  hello 다음 예제에서는 문서를 보여 줍니다.

```
<?xml version="1.0" encoding="utf-8"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.webServer>
    <httpProtocol>
      <customHeaders>
        <add name="X-Frame-Options" value="DENY" xdt:Transform="Replace" />
        <remove name="X-Powered-By" xdt:Transform="Insert" />
      </customHeaders>
    </httpProtocol>
    <security>
      <requestFiltering removeServerHeader="true" xdt:Transform="SetAttributes(removeServerHeader)" />
    </security>
  </system.webServer>
</configuration>
```

자세한 내용은 참조 hello [XDT 변환 샘플] GitHub에 대 한 설명서입니다.

### <a name="migrated-mobile-services-cannot-be-added-tootraffic-manager"></a>마이그레이션된 모바일 서비스 tooTraffic 관리자를 추가할 수 없습니다.
트래픽 관리자 프로필을 만들 때 마이그레이션된 모바일 서비스 toohello 프로필을 직접 선택할 수 없습니다.  "외부 끝점"을 사용합니다.  PowerShell을 통해서만 외부 끝점을 추가할 수 있습니다.  자세한 내용은 [Traffic Manager 자습서](https://azure.microsoft.com/blog/azure-traffic-manager-external-endpoints-and-weighted-round-robin-via-powershell/)를 참조합니다.

## <a name="next-steps"></a>다음 단계
이제 응용 프로그램 마이그레이션된 tooApp 서비스, 했으므로 더 많은 기능을 사용할 수 있습니다.

* 배포 [스테이징 슬롯] toostage 변경 tooyour 사이트를 허용 하 고 수행 A / B 테스트 합니다.
* [WebJobs] 은 요청 시 예약된 작업을 대체합니다.
* 있습니다 수 [지속적으로 배포] 사이트 tooGitHub, TFS 또는 Mercurial 연결 하 여 사이트입니다.
* 사용할 수 있습니다 [Application Insights] toomonitor 사이트입니다.
* 웹 사이트는 서버와 모바일 API에서 동일한 코드를 hello 합니다.

### <a name="upgrading-your-site"></a>모바일 서비스 사이트 tooAzure 모바일 앱 SDK를 업그레이드합니다.
* Node.js 기반 서버 프로젝트에 대 한 hello 새로운 [모바일 앱 Node.js SDK] 몇 가지 새로운 기능을 제공 합니다. 예를 들어 이제 로컬 개발 및 디버깅을 수행하고 0.10 이후의 모든 Node.js 버전을 사용할 수 있으며 원하는 Express.js 미들웨어로 사용자 지정할 수 있습니다.
* 에 대 한 .NET 기반 서버 프로젝트를 새로운 hello [모바일 앱 SDK NuGet 패키지](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) NuGet 종속성에 더 많은 유연성이 있어야 합니다.  이러한 패키지는 hello 새 앱 서비스 인증을 지원 하 고 ASP.NET 프로젝트 작성. 업그레이드에 대 한 자세한 참조 [업그레이드 하면 기존.NET 모바일 서비스 tooApp 서비스](app-service-mobile-net-upgrading-from-mobile-services.md)합니다.

<!-- Images -->
[0]: ./media/app-service-mobile-migrating-from-mobile-services/migrate-to-app-service-button.PNG
[1]: ./media/app-service-mobile-migrating-from-mobile-services/migration-activity-monitor.png
[2]: ./media/app-service-mobile-migrating-from-mobile-services/triggering-job-with-postman.png

<!-- Links -->
[앱 서비스 가격]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[Application Insights]: ../application-insights/app-insights-overview.md
[자동 크기 조정]: ../app-service-web/web-sites-scale.md
[Azure 앱 서비스]: ../app-service/app-service-value-prop-what-is.md
[Azure 앱 서비스 배포 설명서]: ../app-service-web/web-sites-deploy.md
[Azure 클래식 포털]: https://manage.windowsazure.com
[Azure 포털]: https://portal.azure.com
[Azure Region]: https://azure.microsoft.com/en-us/regions/
[Azure 스케줄러 계획]: ../scheduler/scheduler-plans-billing.md
[지속적으로 배포]: ../app-service-web/app-service-continuous-deployment.md
[혼합 네임스페이스를 변환]: https://azure.microsoft.com/en-us/blog/updates-from-notification-hubs-independent-nuget-installation-model-pmt-and-more/
[curl]: http://curl.haxx.se/
[사용자 지정 도메인 이름]: ../app-service-web/web-sites-custom-domain-name.md
[Fiddler]: http://www.telerik.com/fiddler
[Azure 앱 서비스의 일반적인 가용성]: https://azure.microsoft.com/blog/announcing-general-availability-of-app-service-mobile-apps/
[하이브리드 연결]: ../app-service-web/web-sites-hybrid-connection-get-started.md
[로깅]: ../app-service-web/web-sites-enable-diagnostic-log.md
[모바일 앱 Node.js SDK]: https://github.com/azure/azure-mobile-apps-node
[모바일 서비스 vs. App Service]: app-service-mobile-value-prop-migration-from-mobile-services.md
[알림 허브]: ../notification-hubs/notification-hubs-push-notification-overview.md
[성능 모니터링]: ../app-service-web/web-sites-monitor.md
[Postman]: http://www.getpostman.com/
[스테이징 슬롯]: ../app-service-web/web-sites-staged-publishing.md
[VNet]: ../app-service-web/web-sites-integrate-with-vnet.md
[WebJobs]: ../app-service-web/websites-webjobs-resources.md
[XDT 변환 샘플]: https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples
[Functions]: ../azure-functions/functions-overview.md
