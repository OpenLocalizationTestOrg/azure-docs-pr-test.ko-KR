---
title: "여 aaaRun 백그라운드 작업"
description: "어떻게 toorun 백그라운드 작업 Azure에서 웹 앱에 알아봅니다."
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: af01771e-54eb-4aea-af5f-f883ff39572b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/27/2016
ms.author: glenga
ms.openlocfilehash: 96a3d977a806e7192207f0f4da79dfd248694336
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-background-tasks-with-webjobs"></a>WebJob으로 백그라운드 작업 실행
## <a name="overview"></a>개요
[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) 웹앱의 WebJobs에서 세 가지 방법, 즉 요청 시, 계속 실행 또는 일정에 따라 프로그램이나 스크립트를 실행할 수 있습니다. 추가 비용 toouse WebJobs 하지 않습니다.

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

이 문서에서는 방법을 사용 하 여 WebJobs toodeploy hello [Azure 포털](https://portal.azure.com)합니다. 방법에 대 한 정보에 대 한 Visual Studio 또는 지속적인 업데이트 프로세스를 사용 하 여 toodeploy 참조 [어떻게 tooDeploy Azure WebJobs tooWeb 앱](websites-dotnet-deploy-webjobs.md)합니다.

hello Azure WebJobs SDK는 많은 WebJobs 프로그래밍 작업을 간소화합니다. 자세한 내용은 참조 [hello WebJobs SDK 란](websites-dotnet-webjobs-sdk.md)합니다.

 또 다른 방법은 toorun 프로그램 및 스크립트는 서버가 없는 환경 또는 앱 서비스 앱에서 azure 함수를 제공 합니다. 자세한 내용은 [Azure Functions 개요](../azure-functions/functions-overview.md)를 참조하세요.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="acceptablefiles"></a>스크립트 또는 프로그램에 허용 가능한 파일 형식
hello 파일 유형만 허용 됩니다.

* .cmd, .bat, .exe(windows cmd 사용)
* .ps1(powershell 사용)
* .sh(bash 사용)
* .php(php 사용)
* .py(python 사용)
* .js(node 사용)
* .jar(java 사용)

## <a name="CreateOnDemand"></a>Hello 포털에서 주문형 WebJob 만들기
1. Hello에 **웹 앱** hello의 블레이드에서 [Azure 포털](https://portal.azure.com), 클릭 **모든 설정 > WebJobs** tooshow hello **WebJobs** 블레이드입니다.
   
    ![WebJob 블레이드](./media/web-sites-create-web-jobs/wjblade.png)
2. **추가**를 클릭합니다. hello **추가 WebJob** 대화 상자가 나타납니다.
   
    ![WebJob 블레이드 추가](./media/web-sites-create-web-jobs/addwjblade.png)
3. 아래 **이름**, WebJob hello에 대 한 이름을 제공 합니다. hello 이름은 문자 또는 숫자로 시작 해야 하며 이외의 특수 문자를 포함할 수 없습니다 "-" 및 "_"입니다.
4. Hello에 **어떻게 tooRun** 상자 **요청 시 실행**합니다.
5. Hello에 **파일 업로드** 상자 hello 폴더 아이콘을 클릭 하 고 스크립트가 포함 된 toohello zip 파일을 검색 합니다. hello zip 파일 필요한 toorun hello 프로그램 또는 스크립트 실행 파일 (.exe.cmd.bat.sh.php.py.js) 뿐만 아니라 모든 지원 파일 포함 해야 합니다.
6. 확인 **만들기** tooupload hello 스크립트 tooyour 웹 앱입니다. 
   
    hello WebJob hello에 대 한 지정 된 이름이 목록에 표시 hello hello **WebJobs** 블레이드입니다.
7. toorun hello WebJob을 클릭 하 고 hello 목록에서 해당 이름을 마우스 오른쪽 단추로 클릭 **실행**합니다.
   
    ![WebJob 실행](./media/web-sites-create-web-jobs/runondemand.png)

## <a name="CreateContinuous"></a>지속적으로 실행 중인 웹 작업 만들기
1. toocreate 지속적으로 실행 중인 WebJob hello를 한 번 실행 되는 WebJob을 만들에 있지만 hello에 동일한 단계에 따라 **어떻게 tooRun** 상자 **Continuous**합니다.
2. toostart 또는 중지 연속 WebJob hello 목록에서 WebJob hello 마우스 오른쪽 단추로 클릭 **시작** 또는 **중지**합니다.

> [!NOTE]
> 웹 앱이 둘 이상의 인스턴스에서 실행되는 경우 계속 실행되는 웹 작업은 모든 인스턴스에서 실행됩니다. 주문형 작업 및 예약형 작업은 Microsoft Azure의 부하 분산에 따라 선택된 단일 인스턴스에서 실행됩니다.
> 
> 연속 WebJobs에 대 한 toorun 안정적이 고 모든 인스턴스에 사용 Always On hello * 구성 설정을 앱에 대 한 hello 웹 그렇지 않으면 hello SCM 호스트 사이트 너무 오랫동안 유휴 되었을 때 실행을 중지할 수 있습니다.
> 
> 

## <a name="CreateScheduledCRON"></a>CRON 식을 사용하여 예정된 WebJob 만들기
이 기술은 기본, 표준 또는 프리미엄 모드에서 실행 되는 사용 가능한 tooWeb 앱으로 이루어지며 hello **Always On** toobe hello 앱에서 활성화를 설정 합니다.

단순히 tooturn 프로그램에서 요청 시 WebJob에 예약 된 WebJob 포함 한 `settings.job` WebJob zip 파일의 hello 루트에 파일입니다. 이 JSON 파일에는 아래 예제별로 [CRON 식](https://en.wikipedia.org/wiki/Cron)이 포함된 `schedule` 속성이 포함되어야 합니다.

hello CRON 식은 6 개의 필드 이루어져: `{second} {minute} {hour} {day} {month} {day of hello week}`합니다.

예를 들어 tootrigger WebJob 15 분 마다 프로그램 `settings.job` 갖기:

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

다른 CRON 일정 예:

* 매 시간 마다 (즉, 때마다 hello 수 시간 (분)은 0 임).`0 0 * * * *` 
* 매 시간 마다 too5 오전 9 시에서에서 오후:`0 0 9-17 * * *` 
* 매일 오전 9시 30분: `0 30 9 * * *`
* 평일 오전 9시 30분마다: `0 30 9 * * 1-5`

**참고**: Visual Studio에서 WebJob을 배포할 때는 있는지 toomark 확인 프로그램 `settings.job` '변경 된 내용만 복사'로 파일 속성입니다.

## <a name="CreateScheduled"></a>Hello Azure 스케줄러를 사용 하 여 예약 된 WebJob 만들기
다른 방법은 다음 hello에서는 hello Azure 스케줄러를 활용 합니다. 이 경우 WebJob hello 일정에 대 한 직접 정보는 없습니다. 대신, hello Azure 스케줄러를 가져옵니다 구성 된 tootrigger WebJob을 일정에 따라. 

해당 기능을 추가 하기 전에 hello를 사용 하 여 수행할 수 있습니다 하지만 hello Azure 포털에 아직 없는 hello 기능 toocreate 예약 된 WebJob [클래식 포털](http://manage.windowsazure.com)합니다.

1. Hello에 [클래식 포털](http://manage.windowsazure.com) toohello WebJob 페이지로 이동 하 고 클릭 **추가**합니다.
2. Hello에 **어떻게 tooRun** 상자 **일정에 따라 실행**합니다.
   
    ![새 예약형 작업][NewScheduledJob]
3. Hello 선택 **스케줄러 지역** 작업에 대 한 hello 대화 tooproceed toohello 다음 화면 오른쪽의 아래쪽 hello에 hello 화살표를 클릭 하 고 있습니다.
4. Hello에 **작업 만들기** 대화 상자에서 hello 유형의 선택 **되풀이** 원하는: **일회성 작업** 또는 **되풀이 작업**합니다.
   
    ![되풀이 예약][SchdRecurrence]
5. 또한 **지금** 또는 **특정 시간** 중에 **시작** 시간을 선택합니다.
   
    ![시작 시간 예약][SchdStart]
6. 특정 시간에 toostart를 원하는 경우 프로그램 시작 시간 값에서 선택 **시작에**합니다.
   
    ![특정 시간에 시작 예약][SchdStartOn]
7. Hello 있는 되풀이 작업을 선택한 경우 **되풀이 모든** 옵션 및 hello toospecify hello 주파수 **끝에** 옵션 toospecify 종료 시간입니다.
   
    ![되풀이 예약][SchdRecurEvery]
8. 선택 하면 **주**, hello를 선택할 수 있습니다 **에 특정 일정** 상자 고 hello 요일을 hello 원하는 작업 toorun hello를 지정 합니다.
   
    ![Hello 주 요일 일정][SchdWeeksOnParticular]
9. 선택 하면 **개월** 및 선택 hello **에 특정 일정** 상자 특정 번호가 매겨진에 hello 작업 toorun를 설정할 수 있습니다 **일** hello 달에 합니다. 
   
    ![Hello 월의에서 특정 날짜 예약][SchdMonthsOnPartDays]
10. 선택 하면 **요일이**에 작업 toorun hello 원하는 hello 달에는 하루 또는 며칠 분의 hello 주를 선택할 수 있습니다.
    
     ![한 달 중 특정 요일 예약][SchdMonthsOnPartWeekDays]
11. 마지막으로 hello를 사용 하 여 수도 있습니다 **발생** 옵션 toochoose hello 달의 주 (첫째, 둘째, 세 번째 등) hello 작업 toorun hello에 지정한 요일이 원하는 합니다.
    
    ![한 달 중 특정 주의 특정 요일 예약][SchdMonthsOnPartWeekDaysOccurences]
12. 하나 이상의 작업을 만든 후 해당 이름을 해당 상태, 일정 유형 및 기타 정보 hello WebJobs 탭에 표시 됩니다. 기록 정보 hello 마지막 30 개의 WebJobs에 대 한 유지 관리 됩니다.
    
    ![작업 목록][WebJobsListWithSeveralJobs]

### <a name="Scheduler"></a>예약된 작업 및 Azure 스케줄러
Hello의 hello Azure 스케줄러 페이지에 예약 된 작업을 추가로 구성할 수 있는 [클래식 포털](http://manage.windowsazure.com)합니다.

1. Hello WebJobs 페이지 클릭 hello 작업 **일정** 링크 toonavigate toohello Azure 스케줄러 포털 페이지입니다. 
   
   ![링크 tooAzure 스케줄러][LinkToScheduler]
2. Hello 스케줄러 페이지 hello 작업을 클릭 합니다.
   
    ![Hello 스케줄러 포털 페이지에서 작업][SchedulerPortal]
3. hello **작업 동작** 페이지가 열리면 hello 작업을 추가로 구성할 수 있습니다. 
   
    ![스케줄러의 작업 동작 페이지][JobActionPageInScheduler]

## <a name="ViewJobHistory"></a>Hello 작업 기록 보기
1. hello에서의 해당 링크를 클릭 하는 hello WebJobs SDK를 사용 하 여 만든 작업을 포함 하는 작업의 tooview hello 실행 기록을 **로그** hello WebJobs 블레이드의 열입니다. (사용할 수 있습니다 hello 로그 파일 페이지 toohello 클립보드의 hello 클립보드 아이콘 toocopy hello URL 하려는 경우.)
   
    ![로그 링크](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. 클릭 하 여 hello 링크 WebJob hello에 대 한 hello 세부 정보 페이지를 엽니다. 이 페이지를 표시 이름 hello 명령 실행의 hello 실행 된 마지막 시간 및 성공 또는 실패를 hello 합니다. 아래 **최근 작업 실행**, 시간 toosee 추가 세부 정보를 클릭 합니다.
   
    ![WebJob 세부 정보][WebJobDetails]
3. hello **WebJob 실행 세부 정보** 페이지가 나타납니다. 클릭 **토글 출력** toosee hello 텍스트 hello 로그 내용입니다. hello 출력 로그는 텍스트 형식입니다. 
   
    ![WebJob 실행 세부 작업][WebJobRunDetails]
4. 별도 브라우저 창에서 toosee hello 출력 텍스트 클릭 hello **다운로드** 링크 합니다. toodownload hello 텍스트 자체 hello 링크를 마우스 오른쪽 단추로 클릭 하 고 브라우저 옵션 toosave hello 파일 내용을 사용 합니다.
   
    ![로그 출력 다운로드][DownloadLogOutput]
5. hello **WebJobs** hello hello 페이지 맨 아래에 링크 hello 기록 대시보드에서 WebJobs의 편리한 방법을 tooget tooa 목록을 제공 합니다.
   
    ![링크 tooWebJobs 목록][WebJobsLinkToDashboardList]
   
    ![기록 대시보드의 작업 목록][WebJobsListInJobsDashboard]
   
    이러한 링크 중 하나를 클릭 하면 선택한 hello 작업에 대 한 WebJob 세부 정보 페이지 toohello 이동 합니다.

## <a name="WHPNotes"></a>참고 사항
* 무료 모드에서 웹 응용 프로그램 요청 toohello scm (배포) 사이트가 없는 있고 hello 웹 앱의 포털 Azure에서 열려 있지 않으면 20 분 후 시간 초과 될 수 있습니다. 요청 toohello 실제 사이트에이 다시 설정 되지 않습니다.
* 연속 작업에 대 한 코드는 무한 루프에서 toorun 작성 toobe가 필요 합니다.
* Hello 웹 앱 중일 때에 연속 작업이 계속 실행 됩니다.
* 기본 및 표준 모드 제공 hello 항상에 기능을 사용 하도록 설정 하면 웹 앱에서 유휴 상태가 되 수 없습니다.
* 계속 실행되는 웹 작업만을 디버깅할 수 있습니다. 예약된 또는 주문형 웹 작업 디버깅이 지원되지 않습니다.

## <a name="NextSteps"></a>다음 단계
자세한 내용은 [Azure WebJobs 권장 리소스][WebJobsRecommendedResources]를 참조하세요.

[PSonWebJobs]:http://blogs.msdn.com/b/nicktrog/archive/2014/01/22/running-powershell-web-jobs-on-azure-websites.aspx
[WebJobsRecommendedResources]:http://go.microsoft.com/fwlink/?LinkId=390226

[OnDemandWebJob]: ./media/web-sites-create-web-jobs/01aOnDemandWebJob.png
[WebJobsList]: ./media/web-sites-create-web-jobs/02aWebJobsList.png
[NewContinuousJob]: ./media/web-sites-create-web-jobs/03aNewContinuousJob.png
[NewScheduledJob]: ./media/web-sites-create-web-jobs/04aNewScheduledJob.png
[SchdRecurrence]: ./media/web-sites-create-web-jobs/05SchdRecurrence.png
[SchdStart]: ./media/web-sites-create-web-jobs/06SchdStart.png
[SchdStartOn]: ./media/web-sites-create-web-jobs/07SchdStartOn.png
[SchdRecurEvery]: ./media/web-sites-create-web-jobs/08SchdRecurEvery.png
[SchdWeeksOnParticular]: ./media/web-sites-create-web-jobs/09SchdWeeksOnParticular.png
[SchdMonthsOnPartDays]: ./media/web-sites-create-web-jobs/10SchdMonthsOnPartDays.png
[SchdMonthsOnPartWeekDays]: ./media/web-sites-create-web-jobs/11SchdMonthsOnPartWeekDays.png
[SchdMonthsOnPartWeekDaysOccurences]: ./media/web-sites-create-web-jobs/12SchdMonthsOnPartWeekDaysOccurences.png
[RunOnce]: ./media/web-sites-create-web-jobs/13RunOnce.png
[WebJobsListWithSeveralJobs]: ./media/web-sites-create-web-jobs/13WebJobsListWithSeveralJobs.png
[WebJobLogs]: ./media/web-sites-create-web-jobs/14WebJobLogs.png
[WebJobDetails]: ./media/web-sites-create-web-jobs/15WebJobDetails.png
[WebJobRunDetails]: ./media/web-sites-create-web-jobs/16WebJobRunDetails.png
[DownloadLogOutput]: ./media/web-sites-create-web-jobs/17DownloadLogOutput.png
[WebJobsLinkToDashboardList]: ./media/web-sites-create-web-jobs/18WebJobsLinkToDashboardList.png
[WebJobsListInJobsDashboard]: ./media/web-sites-create-web-jobs/19WebJobsListInJobsDashboard.png
[LinkToScheduler]: ./media/web-sites-create-web-jobs/31LinkToScheduler.png
[SchedulerPortal]: ./media/web-sites-create-web-jobs/32SchedulerPortal.png
[JobActionPageInScheduler]: ./media/web-sites-create-web-jobs/33JobActionPageInScheduler.png

