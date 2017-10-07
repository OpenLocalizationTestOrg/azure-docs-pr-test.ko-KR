---
title: "aaaAdd 기능 tooyour 첫 번째 웹 응용 프로그램 | Microsoft Docs"
description: "잠시 후에 다양 한 기능 tooyour 첫 번째 웹 응용 프로그램을 추가 합니다."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 542671c2-22f0-4f20-8b4b-fa477264c492
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2016
ms.author: cephalin
ms.openlocfilehash: 46c9b118c2c188508cb0a369c691a79073b7d7b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-functionality-tooyour-first-web-app"></a>기능 tooyour 첫 번째 웹 응용 프로그램 추가
[5 분 후에 프로그램 첫 번째 웹 응용 프로그램 tooAzure 배포](app-service-web-get-started-dotnet.md), 샘플 웹 응용 프로그램을 배포한 [Azure 앱 서비스](../app-service/app-service-value-prop-what-is.md)합니다. 이 문서에서는 몇 가지 멋진 기능 배포 tooyour 웹 응용 프로그램을 신속 하 게 추가 합니다. 잠시 후에 다음을 수행합니다.

* 사용자에게 인증 적용
* 자동으로 앱 크기 조정
* 응용 프로그램의 성능 hello에서 경고를 수신

이전 문서 hello에에서 배포 되는 샘플 응용 프로그램을에 관계 없이 hello 자습서에서를 따라 따를 수 있습니다.

이 자습서에 몇 가지 예만 hello 앱 서비스 웹 앱 모드로 전환할 때 유용한 기능이 다음 세 가지 활동 hello 합니다. Hello에서 사용할 수 있는 다양 한 hello 기능 **무료** 계층 (첫 번째 웹 앱에서 실행 중인) 인 사용자 평가판 크레딧 tootry 높은 가격 책정 계층을 필요로 하는 기능을 사용할 수 있습니다. 웹 앱에 남아 있는 안심 **무료** 하면 명시적으로 변경 하지 않는 것 tooa 가격 책정 계층을 서로 다른 계층입니다.

> [!NOTE]
> Azure CLI를 사용 하 여 만든 hello 웹 앱이 실행 **무료** 공유 하는 하나의 VM 인스턴스 리소스 할당량에 허용 되는 계층입니다. **무료** 계층을 사용하여 이용할 수 있는 항목에 대한 자세한 내용은 [앱 서비스 제한](../azure-subscription-service-limits.md#app-service-limits)을 참조하세요.
> 
> 

## <a name="authenticate-your-users"></a>사용자 인증
이제 얼마나 쉬운지 tooadd 인증 tooyour 앱을 확인해 보겠습니다 (에서 추가 읽기 [응용 프로그램 서비스 인증/권한 부여](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)).

1. 앱에 대 한 포털 블레이드에서 hello 방금 있는 열을 클릭 **설정** > **인증 / 권한 부여**합니다.  
    ![인증 - 설정 블레이드](./media/app-service-web-get-started/aad-login-settings.png)
2. 클릭 **에** tooturn 인증 합니다.  
3. **인증 공급자**에서 **Azure Active Directory**를 클릭합니다.  
    ![인증 - Azure AD 선택](./media/app-service-web-get-started/aad-login-config.png)
4. Hello에 **Azure Active Directory 설정** 블레이드에서 클릭 **Express**, 클릭 **확인**합니다. hello 기본 설정을 만들 새 Azure AD 응용 프로그램 기본 디렉터리에 있습니다.  
    ![인증 - express 구성](./media/app-service-web-get-started/aad-login-express.png)
5. **저장**을 클릭합니다.  
    ![인증 - 구성 저장](./media/app-service-web-get-started/aad-login-save.png)
   
    Hello 변경이 완료 되 면 hello 알림 벨 친숙 한 메시지와 함께 녹색으로 바뀌도록 표시 됩니다.
6. 응용 프로그램의 포털 블레이드에서 hello에 다시 hello 클릭 **URL** 링크 (또는 **찾아보기** hello 메뉴 모음에서). hello 연결이 HTTP 주소입니다.  
    ![인증-tooURL 찾아보기](./media/app-service-web-get-started/aad-login-browse-click.png)  
    하지만 새 탭에서 hello 앱을 열었을 상자 리디렉션되는 URL을 여러 번 hello 하 고 HTTPS 주소와 응용 프로그램에 완료 합니다. 어떤 표시 되는 tooyour Azure 구독에에서이 이미 인 기록 되 고 hello 응용 프로그램에서 자동으로 인증 하는 합니다.  
    ![인증 - 로그인](./media/app-service-web-get-started/aad-login-browse-http-postclick.png)  
    이제 다른 브라우저에서 인증 되지 않은 세션을 열 경우 toohello를 탐색할 때 로그인 화면을 볼 수 있습니다 동일한 URL입니다.  
    <!-- ![Authenticate - login page](./media/app-service-web-get-started/aad-login-browse.png)  -->
    Azure Active Directory를 사용하여 작업을 완료하지 못한 경우 기본 디렉터리에는 Azure AD 사용자가 없을 수 있습니다. 이 경우 아마도 거기에 hello 유일한 계정은 hello Microsoft 계정과 Azure 구독. 에 toohello 응용 프로그램에서 자동으로 로그인 하는 이유 hello 동일한 이전 브라우저.
    이 로그인 페이지에 동일한 Microsoft 계정 toolog를 사용할 수 있습니다.

축, 모든 트래픽을 tooyour 웹 앱을 인증 하는.

Hello에 알 수 있습니다 **인증 / 권한 부여** 와 같은 더 많은 할 수 있는 블레이드:

* 소셜 로그인 활성화
* 여러 로그인 옵션 활성화
* 사람들은 처음 tooyour 응용 프로그램을 이동 하는 경우 hello 기본 동작을 변경 합니다.

앱 서비스는 hello 일반적인 인증 중 일부에 대해 턴키 솔루션 필요할 tooprovide hello 인증 논리를 직접 필요 하지를 제공 합니다.
자세한 내용은 참조 [앱 서비스 인증/권한 부여](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)를 참조하세요.

## <a name="scale-your-app-automatically-based-on-demand"></a>필요에 따라 자동으로 앱 크기 조정
다음 보겠습니다 자동 크기 조정 하는 자동으로 조정 하기 toorespond toouser 필요 시 용량 하므로 응용 프로그램 (에서 추가 읽기 [Azure에서 응용 프로그램을 수직](web-sites-scale.md) 및 [수동 또는 자동으로 인스턴스 수를 크기 조정](../monitoring-and-diagnostics/insights-how-to-scale.md)).

간단히 말하면 다음과 같은 두 가지 방법으로 웹앱의 크기를 조정할 수 있습니다.

* [강화](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): 더 많은 CPU, 메모리, 디스크 공간 및 추가 기능(전용 VM, 사용자 지정 도메인 및 인증서, 스테이징 슬롯, 자동 크기 조정 등)을 사용할 수 있습니다. 가격 책정 계층 응용 프로그램에 속한 앱 서비스 계획의 hello를 변경 하 여 확장 합니다.
* [확장할](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): hello 응용 프로그램을 실행 하는 VM 인스턴스 수를 증가 합니다.
  수평 확장할 수 있습니다 tooas 50 개의 인스턴스도 많은 가격 책정 계층에 따라 합니다.

각설하고, 자동 크기 조정을 설정해 보겠습니다.

1. 첫째, tooenable 자동 크기 조정 수직 확장 해 보겠습니다. 응용 프로그램의 포털 블레이드에서 hello 클릭 **설정** > **배율 (앱 서비스 계획)을**합니다.  
    ![강화 - 설정 블레이드](./media/app-service-web-get-started/scale-up-settings.png)
2. Scroll 및 선택 hello **S1 표준** 계층, 자동 크기 조정 (스크린 샷에 원)를 지 원하는 가장 낮은 계층 hello을 차례로 클릭 **선택**합니다.  
    ![강화 - 계층 선택](./media/app-service-web-get-started/scale-up-select.png)
   
    강화가 완료되었습니다.
   
   > [!IMPORTANT]
   > 이 계층은 무료 평가판 크레딧을 소비합니다. 기본 사용 사용량 기준 과금 계정이 있는 경우 tooyour 계정 요금이 부과 됩니다.
   > 
   > 
3. 다음으로, 자동 크기 조정을 구성해 보겠습니다. 응용 프로그램의 포털 블레이드에서 hello 클릭 **설정** > **배율 (앱 서비스 계획) Out**합니다.  
    ![규모 확장 - 설정 블레이드](./media/app-service-web-get-started/scale-out-settings.png)
4. 변경 **하 여 확장할** 너무**CPU 비율**합니다. hello 드롭다운 아래 hello 슬라이더를 적절 하 게 업데이트 합니다. 그런 다음 **인스턴스** 범위를 **1** ~ **2**로, **대상 범위**를 **40** ~ **80**으로 정의합니다. Hello 상자에 입력 하거나 hello 슬라이더를 이동 하 여 그렇게 합니다.  
    ![규모 확장 - 자동 크기 조정 구성](./media/app-service-web-get-started/scale-out-configure.png)
   
    이 구성에 따라 CPU 사용률이 80%를 초과하면 자동으로 규모 확장되고 CPU 사용률이 40% 미만으로 떨어지면 자동으로 규모 축소됩니다.
5. 클릭 **저장** hello 메뉴 모음에서 합니다.

축하합니다. 앱 자동 크기 조정이 설정되었습니다.

Hello에 알 수 있습니다 **크기 조정 설정을** 와 같은 더 많은 할 수 있는 블레이드:

* 인스턴스의 tooa 특정 수의 크기를 수동으로 조정
* 메모리 비율 또는 디스크 큐와 같은 기타 성능 메트릭에 따라 크기 조정
* 성능 규칙이 트리거되면 크기 조정 동작을 사용자 지정
* 일정에 따라 자동 크기 조정
* 향후 이벤트에 대해 자동 크기 조정 동작 설정

앱 강화에 대한 자세한 내용은 [Azure에서 앱 크기 확장](web-sites-scale.md)을 참조하세요. 규모 확장에 대한 자세한 내용은 [수동 또는 자동으로 인스턴스 개수 조정](../monitoring-and-diagnostics/insights-how-to-scale.md)을 참조하세요.

## <a name="receive-alerts-for-your-app"></a>앱에 대한 경고 받기
앱이 hello 최대 인스턴스 수 (2)에 도달 하면 어떤 일이 생기 자동 크기 조정 하 고 원하는 사용률이 (80%) 보다 높은 CPU가?
경고를 설정할 수 있습니다 (에서 추가 읽기 [경고 알림의 받을](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)) tooinform 수익과 수 있도록 이러한 상황의 크기를 조정 등록/앱, 예를 들어 있습니다. 이 시나리오에 대한 경고를 간단하게 설정해 보겠습니다.

1. 응용 프로그램의 포털 블레이드에서 hello 클릭 **도구** > **경고**합니다.  
    ![경고 - 설정 블레이드](./media/app-service-web-get-started/alert-settings.png)
2. **경고 추가**를 클릭합니다. 그런 다음, hello **리소스** 상자의로 끝나는 선택 hello 리소스 **(serverfarm)**합니다. 그 리소스가 앱 서비스 계획입니다.  
    ![경고 - App Service 계획에 대한 경고 추가](./media/app-service-web-get-started/alert-add.png)
3. **이름**을 `CPU Maxed`로, **메트릭**을 **CPU 비율**로, **임계값**을 `90`으로 지정한 다음 **전자 메일 소유자, 참여자 및 독자**를 선택하고 **확인**을 클릭합니다.   
    ![경고 - 경고 구성](./media/app-service-web-get-started/alert-configure.png)
   
    Azure hello 경고 만들기 완료 되 면 hello에 표시 됩니다 **경고** 블레이드입니다.  
    ![경고 - 완료된 보기](./media/app-service-web-get-started/alert-done.png)

축하합니다. 이제 경고가 생겼습니다.

이 경고 설정은 5분마다 CPU 사용률을 확인합니다. 사용률이 90%를 초과하면 권한이 있는 사용자와 함께 전자 메일 경고를 받게 됩니다. toosee 모든 사용자는 권한 있는 tooreceive hello 경고를 찾아 응용 프로그램의 toohello 포털 블레이드를 다시 클릭 hello **액세스** 단추입니다.  
![경고를 받는 사람 확인](./media/app-service-web-get-started/alert-rbac.png)

확인할 **구독 관리자** hello는 이미 **소유자** hello 응용 프로그램의 합니다. 이 그룹은 Azure 구독 (예: 평가판 구독이) hello 계정 관리자 인 경우 포함 됩니다. Azure 역할 기반 액세스 제어에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)를 참조하세요.

> [!NOTE]
> 경고 규칙은 Azure 기능입니다. 자세한 내용은 [경고 알림 받기](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)를 참조하세요.
> 
> 

## <a name="next-steps"></a>다음 단계
방식으로 tooconfigure hello에서 경고를 알 수 있습니다는 풍부한 hello에 대 한 도구 집합이 **도구** 블레이드입니다. 여기에서 문제를 해결할 수 문제, 성능 모니터링 취약점에 대 한 테스트, 리소스 관리, hello VM 콘솔을 사용 및 유용한 확장을 추가 합니다. 이러한 도구의 toodiscover hello 간단 하면서도 강력한 도구 서 성장할 중 하나에 각 tooclick을 초대 합니다.

방법을 알아보려면 toodo 배포 된 앱과 함께 더 많은 합니다. 다음은 일부 목록입니다.

* [사용자 지정 도메인 이름 구입 및 구성](custom-dns-web-site-buydomains-web-app.md) - *.azurewebsites.net 도메인 대신 웹앱에 대한 매력적인 도메인을 구입합니다. 또는 이미 있는 도메인을 사용합니다.
* [스테이징 환경 설정](web-sites-staged-publishing.md) -프로덕션 환경으로 전환 하기 전에 URL을 준비 하 여 응용 프로그램 tooa를 배포 합니다. 안심하고 라이브 웹앱을 업데이트합니다. 다중 배포 슬롯으로 정교한 DevOps 솔루션을 설정합니다.
* [연속 배포 설정](app-service-continuous-deployment.md) - 원본 제어 시스템에 앱 배포를 통합합니다. 모든 커밋을 사용하여 Azure에 배포합니다.
* [온-프레미스 리소스에 액세스](web-sites-hybrid-connection-get-started.md) - 기존 온-프레미스 데이터베이스 또는 CRM 시스템에 액세스합니다.
* [앱 백업](web-sites-backup.md) - 백업을 설정하고 웹앱에 복원합니다. 예기치 않은 오류에 준비하고 해당 오류에서 복구합니다.
* [진단 로그를 사용 하도록 설정](web-sites-enable-diagnostic-log.md) -Azure 또는 응용 프로그램 추적에서 읽기 hello IIS 로그입니다. 스트림에서 읽고 다운로드하거나 턴키 분석을 위해 [Application Insights](../application-insights/app-insights-overview.md) 로 가져옵니다.
* [취약성에 대한 앱 스캔](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/) -
  [Tinfoil Security](https://www.tinfoilsecurity.com/)에서 제공하는 서비스를 사용하여 최신 위협에 대해 웹앱을 스캔합니다.
* [백그라운드 작업 실행](../azure-functions/functions-overview.md) - 데이터 처리, 보고 등의 작업을 실행합니다.
* [앱 서비스 작동 방법 알아보기](../app-service/app-service-how-works-readme.md)

