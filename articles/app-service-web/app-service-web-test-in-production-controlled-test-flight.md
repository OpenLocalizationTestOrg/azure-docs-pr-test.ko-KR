---
title: "aaaFlighting 배포 (베타)에서 테스트 Azure 앱 서비스"
description: "응용 프로그램 또는 베타의 새로운 기능 tooflight이 종단 간 자습서에서 업데이트를 테스트 하는 방법을 알아봅니다. 연속 게시, 슬롯, 트래픽 라우팅 및 Application Insights 통합과 같은 앱 서비스 기능을 함께 소개합니다."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 17953c51-38f8-442d-bb0b-f69c1542f0e9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cephalin
ms.openlocfilehash: e83477b1fe46be09e5baa7bc2bd239b840b05cf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="flighting-deployment-beta-testing-in-azure-app-service"></a>Azure 앱 서비스에서 Flighting 배포(베타 테스트)
이 자습서에서는 어떻게 toodo *플 라이팅 배포* 통합 하 여 hello의 다양 한 기능 [Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714) 및 [Azure Application Insights](/services/application-insights/)합니다.

*Flighting* 은 제한된 수의 실제 고객으로 새로운 기능 또는 변경의 유효성을 검사하는 배포 프로세스이며 프로덕션 시나리오의 주요 테스트입니다. 김 윤 식 toobeta는 테스트 및 "처리 중 통제 된 테스트" 라고도 합니다. 웹 서비스를 제공하는 많은 대기업이 이 방법을 사용하여 [민첩한 개발](https://en.wikipedia.org/wiki/Agile_software_development)이라는 해당 연습에서 앱 업데이트의 초기 유효성 검사를 가져옵니다. Azure 앱 서비스 하면 지속적인 게시로 프로덕션에서 toointegrate 테스트 하 고 Application Insights tooimplement hello 동일한 DevOps 시나리오. 이 방법의 이점은 다음과 같습니다.

* **실제 피드백을 얻을 *전에* 업데이트가 릴리스된 tooproduction** -hello 놓으면으로 피드백을 얻는 것 피드백 해제 하기 전에 취소만 합니다. 초기 hello 제품 수명 주기에서 사용자가 원하는 실제 사용자 트래픽 및 동작을 사용 하 여 업데이트를 테스트할 수 있습니다.
* **[연속 테스트 기반 개발(CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development) 향상** - Application Insights를 사용하여 연속 통합 및 계측으로 프로덕션에서 테스트를 통합하여 사용자 유효성 검사가 제품 수명 주기에서 초기에 자동으로 발생합니다. 수동 테스트 실행에 시간 투자를 줄일 수 있습니다.
* **테스트 워크플로 최적화** -연속 모니터링 계측으로 프로덕션에서 테스트를 자동화 하 여 수행할 수 있습니다 잠재적으로 단일 프로세스에서 테스트의 다양 한 종류의 hello 목표와 같은 [통합](https://en.wikipedia.org/wiki/Integration_testing), [회귀](https://en.wikipedia.org/wiki/Regression_testing), [유용성](https://en.wikipedia.org/wiki/Usability_testing), 내게 필요한 옵션, 지역화, [성능](https://en.wikipedia.org/wiki/Software_performance_testing), [보안](https://en.wikipedia.org/wiki/Security_testing), 및 [ 승인](https://en.wikipedia.org/wiki/Acceptance_testing)합니다.

Flighting 배포는 라이브 트래픽의 라우팅에 국한되지 않습니다. 이러한 배포는 예기치 않은 버그, 성능 저하, 사용자 환경 문제 인지 여부를 최대한 빨리 toogain 통찰력을 합니다. 실제 고객을 상대한다는 점을 기억하십시오. 따라서 toodo 것 바로, 있어야를 설정한 후에 플 라이팅 배포 toogather 하면 필요한 순서 toomake 결정을 내릴된 다음 단계에 대 한 모든 hello 데이터입니다. 이 자습서에서는 New Relic 또는 시나리오에 적합 한 기타 기술 있지만 Application Insights를 사용 하 여 toocollect 데이터 사용 방법입니다.

## <a name="what-you-will-do"></a>수행할 사항
이 자습서에서는 살펴보겠습니다 어떻게 toobring 프로덕션에서 응용 프로그램 서비스 응용 프로그램 시나리오 함께 tootest 다음 hello:

* [프로덕션 트래픽을 라우팅할](app-service-web-test-in-production-get-start.md) tooyour 베타 응용 프로그램
* [응용 프로그램을 계측할](../application-insights/app-insights-web-track-usage.md) tooobtain 유용한 메트릭
* 연속 베타 앱 배포 및 라이브 앱 메트릭 추적
* Hello 프로덕션 앱 및 코드 어떻게 변경 되는지 hello 베타 앱 toosee 간의 비교 메트릭 tooresults 변환

## <a name="what-you-will-need"></a>필요한 사항
* Azure 계정.
* [GitHub](https://github.com/) 계정
* Visual Studio 2015-hello를 다운로드할 수 있습니다 [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx)합니다.
* Git 셸 (설치 된 [Windows 용 GitHub](https://windows.github.com/))-이 통해 있습니다 toorun hello 두 hello Git 및 PowerShell 명령 동일한 세션
* 최신 [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) 비트
* 기본적으로 hello 다음 이해:
  * [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) 템플릿 배포([Azure에서 예측 가능하도록 복잡한 응용 프로그램 배포](app-service-deploy-complex-application-predictably.md) 참조)
  * [Git](http://git-scm.com/documentation)
  * [PowerShell](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> 이 자습서는 Azure 계정 toocomplete 필요합니다.
>
> * 할 수 있습니다 [무료로 Azure 계정을 개설](https://azure.microsoft.com/pricing/free-trial/) -크레딧을 얻게 Azure 서비스를 유료 아웃 tootry 사용할 수 있으며 모두 사용 하는 후에 hello 계정 등에 사용 가능한 웹 응용 프로그램 등의 Azure 서비스입니다.
> * [Visual Studio 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) 할 수 있음: Visual Studio 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공합니다.
>
> Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.
>
>

## <a name="set-up-your-production-web-app"></a>프로덕션 웹앱 설치
> [!NOTE]
> 이 자습서에 사용 된 hello 스크립트 GitHub 리포지토리에서 지속적인 게시를 자동으로 구성 됩니다. 이렇게 하려면 GitHub 자격 증명 Azure에 이미 저장 되어, hello 웹 앱에 대 한 소스 제어 설정 tooconfigure 시도할 때 스크립팅된 hello 배포 그렇지 않으면 실패 합니다.
>
> azure에서 자격 증명에 GitHub toostore hello에 웹 앱 만들기 [Azure 포털](https://portal.azure.com/) 및 [GitHub 배포 구성](app-service-continuous-deployment.md)합니다. 하기만 하면 toodo 한 번이 됩니다.
>
>

일반적인 DevOps 시나리오에서는 Azure에서 동시에 실행 하는 응용 프로그램 하 고 지속적인 게시를 통해 변경 내용을 tooit toomake 하려는 있습니다. 이 시나리오에서는 tooproduction가 개발 하 고 테스트 하는 서식 파일을 배포 합니다.

1. 사용자 고유의 분기의 hello 만들기 [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) 저장소입니다. 분기를 만드는 방법에 대한 자세한 내용은 [리포지토리 분기](https://help.github.com/articles/fork-a-repo/)를 참조하세요. 사용자의 포크를 생성하면, 브라우저에서 볼 수 있습니다.

   ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. Git 셸 세션을 엽니다. Git 셸이 없는 경우 [Windows용 GitHub](https://windows.github.com/) 를 설치합니다.
3. Hello 다음 명령을 실행 하 여 포크의 로컬 복제본을 만듭니다.

     git clone https://github.com/<your_fork>/ToDoApp.git
4. 로컬 복제본을 사용 하는 후 너무 이동*&lt;repository_root >*\ARMTemplates, 및 실행된 hello deploy.ps1 같이 고유한 접미사와 함께 아래 스크립트:

     .\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git -ResourceGroupSuffix <your_suffix>
5. 대화 상자가 나타나면 원하는 hello 사용자 이름 및 데이터베이스 액세스에 대 한 암호에 입력 합니다. Toospecify 필요 하므로 데이터베이스 자격 증명 기억 다시 때 업데이트 hello 리소스 그룹에 해당 합니다.

   다양 한 Azure 리소스의 진행 상태를 프로 비전 하는 hello를 표시 되어야 합니다. 배포가 완료 되 면 hello 스크립트 hello 브라우저에서 응용 프로그램 hello 실행과 친숙 한 경고음을 제공 합니다.
   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.1-app-in-browser.png)
6. Git 셸 세션으로 돌아가서 다음을 실행합니다.

     .\swap –Name ToDoApp<your_suffix>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.2-swap-to-production.png)
7. Hello 스크립트 작업을 마치면 toobrowse toohello 프런트 엔드의 주소 돌아가서 (http://ToDoApp*&lt;your_suffix >*.azurewebsites.net/) toosee hello 응용 프로그램을 프로덕션 환경에서 실행 합니다.
8. Hello에 로그인 [Azure 포털](https://portal.azure.com/) 무엇이 확인 하 고 있습니다.

   Hello에 수 toosee 두 웹 응용 프로그램 수 같은 리소스 그룹, hello 사용 하 여 `Api` hello 이름에서 접미사입니다. Hello 리소스 그룹 보기를 보면 하는 경우 hello SQL 데이터베이스 및 서버, 앱 서비스 계획 hello 및 hello 웹 앱에 대 한 스테이징 슬롯 hello도 표시 됩니다. Hello 다양 한 리소스를 탐색 하 고 비교를 사용 하 여  *&lt;repository_root >*\ARMTemplates\ProdAndStage.json toosee hello 서식 파일에 구성 된 방법입니다.

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.3-resource-group-view.png)

Hello 프로덕션 응용 프로그램을 설정 했습니다.  이제 유용성 hello 앱에 대 한 나쁘지 피드백 나타나는 가정해 보겠습니다. 따라서 tooinvestigate를 결정합니다. 거 tooinstrument 앱 toogive 피드백 있습니다.

## <a name="investigate-instrument-your-client-app-for-monitoringmetrics"></a>조사: 모니터링/메트릭에 대한 클라이언트 앱 계측
1. Visual Studio에서 *&lt;repository_root>*\src\MultiChannelToDo.sln을 엽니다.
2. 솔루션 > **솔루션에 대한 NuGet 패키지 관리** > **복원**을 마우스 오른쪽 단추로 클릭하여 모든 NuGet 패키지를 복원합니다.
3. 마우스 오른쪽 단추로 클릭 **MultiChannelToDo.Web** > **Application Insights 원격 분석 추가** > **설정 구성** > 리소스 그룹 변경 tooToDoApp*&lt;your_suffix >* > **Application Insights 추가 tooProject**합니다.
4. Hello Azure 포털에서에서 hello에 대 한 hello 블레이드를 엽니다 **MultiChannelToDo.Web** Application Insight 리소스입니다. Hello 그런 다음 **응용 프로그램 상태** 부, 클릭 **toocollect 브라우저 페이지에서 데이터를 로드 하는 방법에 대해 알아봅니다** > 코드를 복사 합니다.
5. Hello JS 계측 코드를 너무 복사 추가*&lt;repository_root >*hello 닫는 직전 \src\MultiChannelToDo.Web\app\Index.cshtml `<heading>` 태그입니다. Application Insight 리소스의 hello 고유 계측 키를 포함 해야 합니다.

        <script type="text/javascript">
        var appInsights=window.appInsights||function(config){
            function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
        }({
            instrumentationKey:"<your_unique_instrumentation_key>"
        });

        window.appInsights=appInsights;
        appInsights.trackPageView();
        </script>
6. Hello 본문의 코드 toohello 맨 아래에 다음을 추가 하 여 사용자 지정 이벤트 tooApplication Insights 마우스 클릭에 대 한 보내기:

       <script>
           $(document.body).find("*").click(function(event) {

               appInsights.trackEvent(event.target.tagName + ": " + event.target.className);
           });
       </script>

   이 JavaScript 코드 조각을 hello 웹 응용 프로그램에서 사용자가 클릭할 때마다 사용자 지정 이벤트 tooApplication 통찰력을 보냅니다.
7. Git 셸에서 커밋하고 GitHub에서 변경 내용을 tooyour 포크 푸시하십시오. 다음 클라이언트 toorefresh 브라우저에 대 한 대기 합니다.

       git add -A :/
       git commit -m "add AI configuration for client app"
       git push origin master
8. 배포 된 hello 앱 변경 내용 tooproduction를 바꿉니다.

     .\swap –Name ToDoApp<your_suffix>
9. 사용자가 구성한 toohello Application Insights 리소스를 찾아봅니다. 사용자 지정 이벤트를 클릭합니다.

   ![](./media/app-service-web-test-in-production-controlled-test-flight/01-custom-events.png)

   사용자 지정 이벤트에 대한 메트릭이 보이지 않으면 몇 분 기다렸다가 **새로 고침**을 클릭합니다.

아래와 같은 차트를 본다고 가정합니다.

![](./media/app-service-web-test-in-production-controlled-test-flight/02-custom-events-chart-view.png)

및 그 아래의 이벤트 표 형태 hello:

![](./media/app-service-web-test-in-production-controlled-test-flight/03-custom-event-grid-view.png)

Hello tooyour ToDoApp 응용 프로그램 코드에 따라, **단추** toohello 전송 단추와 hello 이벤트는 해당 **입력** 이벤트 해당 toohello 텍스트 상자에 붙여넣습니다. 지금까지는 합리적입니다. 그러나 것 같습니다.는 충분 한 크기가 클릭 및 매우 몇 번의 클릭 hello 할 일 항목에는 (hello **LI** 이벤트).

이 하면 폼 hello의 어느 부분이 UI는 클릭 가능한 아니며 hello 목록 항목 및 해당 아이콘에 가져가면 hello 커서 텍스트 선택에 대 한 스타일 지정 하기 때문에 일부 사용자가 프로그램 가설 혼동 기반으로 합니다.

![](./media/app-service-web-test-in-production-controlled-test-flight/04-to-do-list-item-ui.png)

부자연스러운 예제일 수 있습니다. 그럼에도 불구 하 고 진행 중인 toomake 개선 tooyour 응용 프로그램 하 고 라이브 고객 으로부터 플 라이팅 배포 tooget 유용성 피드백을 수행 합니다.

### <a name="instrument-your-server-app-for-monitoringmetrics"></a>모니터링/메트릭에 대한 서버 앱 계측
이 자습서에서 설명 하는 hello 시나리오 hello 클라이언트 앱만 처리 하므로 탄젠트입니다. 그러나 완결성에 대 한 hello 서버 쪽 앱을 설정 합니다.

1. 마우스 오른쪽 단추로 클릭 **MultiChannelToDo** > **Application Insights 원격 분석 추가** > **설정 구성** > 리소스 그룹 변경 tooToDoApp*&lt;your_suffix >* > **Application Insights 추가 tooProject**합니다.
2. Git 셸에서 커밋하고 GitHub에서 변경 내용을 tooyour 포크 푸시하십시오. 다음 클라이언트 toorefresh 브라우저에 대 한 대기 합니다.

       git add -A :/
       git commit -m "add AI configuration for server app"
       git push origin master
3. 배포 된 hello 앱 변경 내용 tooproduction를 바꿉니다.

     .\swap –Name ToDoApp<your_suffix>

이것으로 끝입니다.

## <a name="investigate-add-slot-specific-tags-tooyour-client-app-metrics"></a>슬롯 관련 태그 tooyour 클라이언트 응용 프로그램 메트릭을 추가 조사 하십시오:
이 섹션에서는 구성한 hello 다양 한 배포 슬롯 toosend 슬롯 관련 원격 분석 toohello 같은 Application Insights 리소스입니다. 이러한 방식으로 원격 분석을 비교할 수 있습니다 다른 슬롯 (배포 환경) tooeasily 트래픽만 간에 데이터 앱 변경 내용 hello 효과 확인 합니다. At hello 동일한 시간을 계속할 수 있도록 toomonitor 프로덕션 응용 프로그램 필요에 따라 hello 나머지에서 hello 프로덕션 트래픽을 구분할 수 있습니다.

클라이언트 동작에 데이터를 수집 하는 이후 [원격 분석 이니셜라이저 tooyour JavaScript 코드를 추가](../application-insights/app-insights-api-filtering-sampling.md) index.cshtml에 있습니다. 서버 쪽 성능 tootest 하려는 경우 예를 들어 할 수 있는 마찬가지로 서버 코드에서 (참조 [사용자 지정 이벤트 및 메트릭을 대 한 Application Insights API](../application-insights/app-insights-api-custom-events-metrics.md)합니다.

1. 먼저 추가 하는 hello 코드 있게 되었습니다 hello 두 `//` 아래에 메모 hello JavaScript 블록 toohello를 추가한 `<heading>` 이전 태그를 지정 합니다.

        window.appInsights = appInsights;

        // Begin new code
        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["Environment"] = "@System.Configuration.ConfigurationManager.AppSettings["environment"]";
            });
        });
        // End new code

        appInsights.trackPageView();

    이 이니셜라이저 코드는 hello `appInsights` 개체 tooadd hello 라는 사용자 지정 속성 `Environment` tooevery 부분의 원격 분석을 보냅니다.
2. 다음으로 Azure에서 웹앱에 대해 이 사용자 지정 속성을 [슬롯 설정](web-sites-staged-publishing.md#AboutConfiguration) 에 추가합니다. toodo 명령을 Git 셸 세션에서 다음 실행된이, hello 합니다.

        $app = Get-AzureWebsite -Name todoapp<your_suffix> -Slot production
        $app.AppSettings.Add("environment", "Production")
        $app.SlotStickyAppSettingNames.Add("environment")
        $app | Set-AzureWebsite -Name todoapp<your_suffix> -Slot production

    프로젝트의 Web.config hello 이미 정의 되어 hello `environment` 앱 설정 합니다. 이 설정을 사용 하 여 hello 응용 프로그램을 로컬로 테스트할 때 하면 메트릭이 태그로 지정 될 `VS Debugger`합니다. 그러나 변경 내용을 tooAzure 푸시할 때 Azure는 고 hello를 사용 하 여 `environment` 사항과 대신 hello 웹 앱의 구성에서 설정 하는 응용 프로그램으로 태그 처리 될 `Production`합니다.
3. 커밋 및 GitHub에서 코드 변경 내용을 tooyour 포크 강제 하 고 사용자가 toouse hello 새 앱 (toorefresh hello 브라우저 필요) 될 때까지 기다립니다. Application Insights에서 새 속성 tooshow hello에 대 한 약 15 분을 차지 `MultiChannelToDo.Web` 리소스입니다.

        git add -A :/
        git commit -m "add environment property tooAI events for client app"
        git push origin master
4. 이제 toohello 이동 **사용자 지정 이벤트** 블레이드를 다시 및 필터에 메트릭 hello `Environment=Production`합니다. 이 필터와 hello 새 사용자 지정 이벤트를 모두 hello 프로덕션에서 슬롯 수 toosee 수 있어야 합니다.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/05-filter-on-production-environment.png)
5. Hello 클릭 **즐겨찾기** 단추 toosave hello 현재 메트릭 탐색기 설정을 toosomething 같은 **사용자 지정 이벤트: 프로덕션**합니다. 나중에 이 뷰 및 배포 슬롯 뷰를 쉽게 전환할 수 있습니다.

   > [!TIP]
   > 더욱 강력한 분석의 경우 [Power BI로 Application Insights 리소스 통합](../application-insights/app-insights-export-power-bi.md)을 고려합니다.
   >
   >

### <a name="add-slot-specific-tags-tooyour-server-app-metrics"></a>슬롯 관련 태그 tooyour 서버 응용 프로그램 메트릭 추가
다시 완결성에 대 한 hello 서버 쪽 앱을 설정 합니다. JavaScript 계측는 hello 클라이언트 앱에서는 달리 hello 서버 응용 프로그램에 대 한 슬롯 관련 태그.NET 코드를 계측 합니다.

1. *&lt;repository_root>*\src\MultiChannelToDo\Global.asax.cs를 엽니다. 닫는 중괄호 네임 스페이스 hello 직전 아래 hello 코드 블록을 추가 합니다.

        namespace MultiChannelToDo
        {
                ...

                // Begin new code
            public class ConfigInitializer
            : ITelemetryInitializer
            {
                void ITelemetryInitializer.Initialize(ITelemetry telemetry)
                {
                    telemetry.Context.Properties["Environment"] = System.Configuration.ConfigurationManager.AppSettings["environment"];
                }
            }
                // End new code
        }
2. Hello를 추가 하 여 hello 이름 확인 오류를 해결 `using` hello 파일의 시작 부분 toohello 아래 문:

        using Microsoft.ApplicationInsights.Channel;
        using Microsoft.ApplicationInsights.Extensibility;
3. Hello hello toohello 맨 아래에 코드 추가 `Application_Start()` 메서드:

        TelemetryConfiguration.Active.TelemetryInitializers.Add(new ConfigInitializer());
4. 커밋 및 GitHub에서 코드 변경 내용을 tooyour 포크 강제 하 고 사용자가 toouse hello 새 앱 (toorefresh hello 브라우저 필요) 될 때까지 기다립니다. Application Insights에서 새 속성 tooshow hello에 대 한 약 15 분을 차지 `MultiChannelToDo` 리소스입니다.

        git add -A :/
        git commit -m "add environment property tooAI events for server app"
        git push origin master

## <a name="update-set-up-your-beta-branch"></a>업데이트: 베타 분기 설정
1. 열기  *&lt;repository_root >*\ARMTemplates\ProdAndStagetest.json 및 찾기 hello `appsettings` 리소스 (검색할 `"name": "appsettings"`). 각 슬롯에 하나 씩 4개가 있습니다.
2. 각 `appsettings` 리소스에 추가 `"environment": "[parameters('slotName')]"` 앱 toohello 끝 설정 hello `properties` 배열입니다. 쉼표 tooend hello 이전 줄 것을 잊지 마십시오.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/06-arm-app-setting-with-slot-name.png)

    Hello 방금 추가한 `environment` hello 템플릿에서 tooall hello 슬롯을 설정 하는 응용 프로그램입니다.
3. 동일한 파일 hello 하 hello `slotconfignames` 리소스 (검색할 `"name": "slotconfignames"`). 각 앱에 하나 씩 2개가 있습니다.
4. 각 `slotconfignames` 리소스를 추가 `"environment"` hello toohello 끝 `appSettingNames` 배열입니다. 쉼표 tooend hello 이전 줄 것을 잊지 마십시오.

    Hello 방금 변경한 `environment` 두 앱에 대 한 응용 프로그램 설정 스틱 tooits 제품의 배포 슬롯입니다.  
5. Git 셸 세션에서 다음 실행된 hello로 명령을 hello 동일한 리소스 그룹 접미사 이전에 사용 합니다.

        git checkout -b beta
        git push origin beta
        .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch beta
6. 메시지가 지정 이전과 같은 SQL 데이터베이스 자격 증명 hello 합니다. 그런 다음 tooupdate hello 리소스 그룹으로 형식 때 요청 `Y`, 다음 `ENTER`합니다.

    Hello 스크립트 완료, hello 원본 리소스 그룹에 모든 리소스는 유지 되지만 "beta" 라는 새 슬롯은 내에 만든 hello로 동일 되 면 hello 시작 부분에서 만든 hello "스테이징" 슬롯으로 구성 합니다.

   > [!NOTE]
   > 이 방법으로 서로 다른 배포 환경에서 hello 메서드 간에 차이가 있는 [Azure 앱 서비스와 Agile 소프트웨어 개발](app-service-agile-software-development.md)합니다. 여기에서 배포 슬롯을 사용하여 배포 환경을 만든 반면 저기서는 리소스 그룹을 사용하여 배포 환경을 만듭니다. 배포 환경 리소스 그룹으로 관리 하면 tookeep hello 프로덕션 환경 off-limits toodevelopers, 아니라 슬롯을 쉽게 수행할 수 있는 프로덕션 환경에서 테스트 하는 쉬운 toodo 않습니다.
   >
   >

또한 원하는 경우 실행하여 알파 앱을 만들 수 있습니다.

    git checkout -b alpha
    git push origin alpha
    .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch alpha

이 자습서에서는 베타 앱을 계속 사용합니다.

## <a name="update-push-your-updates-toohello-beta-app"></a>업데이트: 업데이트 toohello 베타 앱 푸시
원하는 tooimprove tooyour 응용 프로그램을 백업 합니다.

1. 베타 분기에서 지금 여러분이 있는지 확인합니다.

        git checkout beta
2.  *&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml, 찾기 hello `<li>` 태그를 지정 하 고 hello 추가 `style="cursor:pointer"` 특성을 다음과 같이 합니다.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/07-change-cursor-style-on-li.png)
3. 커밋하고 tooAzure 푸시하십시오.
4. Hello 변경 이제에 반영 되도록 hello 베타 슬롯 toohttp://todoapp 이동 하 여 확인*&lt;your_suffix >*-beta.azurewebsites.net/ 합니다. Hello 변경 아직 브라우저 tooget hello 새 javascript 코드를 새로 고치려면 표시 되지 않으면 합니다.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/08-verify-change-in-beta-site.png)

Hello 베타 슬롯에서 실행 되는 변경 내용을가지고 준비 tooperform 플 라이팅 배포 됩니다.

## <a name="validate-route-traffic-toohello-beta-app"></a>유효성 검사: 경로 트래픽 toohello 베타 응용 프로그램
이 섹션에서는 트래픽 toohello 베타 응용 프로그램을 라우팅합니다. 데모의 명확성을 위해 tooroute hello 사용자 트래픽 tooit의 상당 부분이 겠 군요. 실제로 hello 소통량 원하는 tooroute 상황에 따라 달라 집니다. 예를 들어, microsoft.com의 hello 규모에 사이트가 있는 경우 순서 toogain 유용한 데이터의 총 트래픽의 1% 보다 작은 할 수 있습니다.

1. Git 셸 세션에서 실행 명령을 tooroute 다음 hello hello 프로덕션 트래픽 toohello 베타 슬롯의 절반 합니다.

        $siteName = "ToDoApp<your suffix>"
        $rule = New-Object Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.RampUpRule
        $rule.ActionHostName = "$siteName-beta.azurewebsites.net"
        $rule.ReroutePercentage = 50
        $rule.Name = "beta"
        Set-AzureWebsite $siteName -Slot Production -RoutingRules $rule

   hello `ReroutePercentage=50` 속성 지정 hello 프로덕션 트래픽의 50% 라우트된 toohello 베타 앱의 URL (hello로 지정 된 `ActionHostName` 속성).
2. 이제 toohttp://ToDoApp 이동*&lt;your_suffix >*. azurewebsites.net 합니다. hello 트래픽의 50%를 리디렉션된 toohello 베타 슬롯 수 있습니다.
3. Application Insights 리소스에서 hello 메트릭을 기준으로 필터링 환경 = "beta"입니다.

   > [!NOTE]
   > 다른 즐겨찾기로이 필터링 된 보기를 저장 하는 경우 프로덕션 및 베타 뷰 간의 hello 메트릭 탐색기 보기 쉽게 전환할 수 합니다.
   >
   >

다음과 유사한 toohello 다음을 참조 하는 Application Insights에 있다고 가정 합니다.

![](./media/app-service-web-test-in-production-controlled-test-flight/09-test-beta-site-in-production.png)

뿐만 아니라이 표시 hello에 대 한 많은 자세한 클릭 된다고 `<li>` 태그 toobe의 클릭 급증 하기 때문에 결과적으로 하지만 `<li>` 태그입니다. 다음 사용자를 새 hello 가져 왔어 있는지을 완료할 수 있습니다 `<li>` 태그 클릭할 수 및는 이제 hello 응용 프로그램의 모든 이전에 완료 된 작업의 선택을 취소 합니다.

플 라이팅 배포의 hello 데이터에 따라 새 UI를 프로덕션에 대 한 준비가 되었는지 결정 합니다.

## <a name="go-live-move-your-new-code-into-production"></a>바로 사용: 새 코드를 프로덕션으로 이동
사용자는 이제 준비 toomove 업데이트 tooproduction 합니다. 유용은 이제는 업데이트의 유효성을 이미 알고 있는 *전에* tooproduction 푸시됩니다. 이제 안심하고 배포할 수 있습니다. 클라이언트 응용 프로그램 업데이트 toohello AngularJS를 보낸 후 hello 클라이언트 쪽 코드만 유효 합니다. Toomake 변경 toohello 백 엔드 웹 API 앱 인 경우 쉽고 마찬가지로 변경 내용을 확인할 수 있습니다.

1. Git 셸에서 hello 다음 명령을 실행 하 여 hello 트래픽 라우팅 규칙을 제거 합니다.

        Set-AzureWebsite $siteName -Slot Production -RoutingRules @()
2. Hello Git 명령을 실행 합니다.

        git checkout master
        git pull origin master
        git merge beta
        git push origin master
3. 몇 분 정도 hello에 대 한 새로운 배포 toobe toohello 슬롯을 코딩 한 다음 시작 http://ToDoApp 기다리세요*&lt;your_suffix >*-hello 스테이징에서 새 업데이트 hello staging.azurewebsites.net tooverify 준비 슬롯입니다. 분기의 마스터 분기는 해당 hello 연결 toohello 준비 기억 응용 프로그램의 슬롯입니다.
4. 이제 프로덕션 환경으로 슬롯을 준비 하는 hello를 교체

        cd <ROOT>\ToDoApp\ARMTemplates
        .\swap.ps1 -Name todoapp<your_suffix>

## <a name="summary"></a>요약
Azure 앱 서비스 쉽게 소규모 toomedium 기업 tootest에 대 한 고객 지향 앱 프로덕션 환경에서 어떤 큰 기업에서 일반적으로 수행 되 있습니다. 다행히이 자습서가 제공한 hello toobring 함께 응용 프로그램 서비스 및 Application Insights toomake 가능한 플 라이팅 배포 및 기타 테스트 프로덕션 시나리오 DevOps 세계에 필요한 기술입니다.

## <a name="more-resources"></a>추가 리소스
* [Azure 앱 서비스를 사용하여 Agile 소프트웨어 개발](app-service-agile-software-development.md)
* [Azure 앱 서비스에서 웹 앱에 대한 스테이징 환경 설정](web-sites-staged-publishing.md)
* [Azure에서 예측 가능하도록 복잡한 응용 프로그램을 배포](app-service-deploy-complex-application-predictably.md)
* [Azure 리소스 관리자 템플릿 작성](../azure-resource-manager/resource-group-authoring-templates.md)
* [JSONLint-hello JSON 유효성 검사기](http://jsonlint.com/)
* [Git 분기-기본 분기 및 병합](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [Azure PowerShell](/powershell/azure/overview)
* [프로젝트 Kudu Wiki](https://github.com/projectkudu/kudu/wiki)
