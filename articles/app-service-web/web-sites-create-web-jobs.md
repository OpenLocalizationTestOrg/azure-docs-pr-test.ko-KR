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
# <a name="run-background-tasks-with-webjobs"></a><span data-ttu-id="40391-103">WebJob으로 백그라운드 작업 실행</span><span class="sxs-lookup"><span data-stu-id="40391-103">Run Background tasks with WebJobs</span></span>
## <a name="overview"></a><span data-ttu-id="40391-104">개요</span><span class="sxs-lookup"><span data-stu-id="40391-104">Overview</span></span>
<span data-ttu-id="40391-105">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) 웹앱의 WebJobs에서 세 가지 방법, 즉 요청 시, 계속 실행 또는 일정에 따라 프로그램이나 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40391-105">You can run programs or scripts in WebJobs in your [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web app in three ways: on demand, continuously, or on a schedule.</span></span> <span data-ttu-id="40391-106">추가 비용 toouse WebJobs 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40391-106">There is no additional cost toouse WebJobs.</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="40391-107">이 문서에서는 방법을 사용 하 여 WebJobs toodeploy hello [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-107">This article shows how toodeploy WebJobs by using hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="40391-108">방법에 대 한 정보에 대 한 Visual Studio 또는 지속적인 업데이트 프로세스를 사용 하 여 toodeploy 참조 [어떻게 tooDeploy Azure WebJobs tooWeb 앱](websites-dotnet-deploy-webjobs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-108">For information about how toodeploy by using Visual Studio or a continuous delivery process, see [How tooDeploy Azure WebJobs tooWeb Apps](websites-dotnet-deploy-webjobs.md).</span></span>

<span data-ttu-id="40391-109">hello Azure WebJobs SDK는 많은 WebJobs 프로그래밍 작업을 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-109">hello Azure WebJobs SDK simplifies many WebJobs programming tasks.</span></span> <span data-ttu-id="40391-110">자세한 내용은 참조 [hello WebJobs SDK 란](websites-dotnet-webjobs-sdk.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-110">For more information, see [What is hello WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

 <span data-ttu-id="40391-111">또 다른 방법은 toorun 프로그램 및 스크립트는 서버가 없는 환경 또는 앱 서비스 앱에서 azure 함수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-111">Azure Functions provides another way toorun programs and scripts from either a serverless environment or from an App Service app.</span></span> <span data-ttu-id="40391-112">자세한 내용은 [Azure Functions 개요](../azure-functions/functions-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40391-112">For more information, see [Azure Functions overview](../azure-functions/functions-overview.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="40391-113"><a name="acceptablefiles"></a>스크립트 또는 프로그램에 허용 가능한 파일 형식</span><span class="sxs-lookup"><span data-stu-id="40391-113"><a name="acceptablefiles"></a>Acceptable file types for scripts or programs</span></span>
<span data-ttu-id="40391-114">hello 파일 유형만 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40391-114">hello following file types are accepted:</span></span>

* <span data-ttu-id="40391-115">.cmd, .bat, .exe(windows cmd 사용)</span><span class="sxs-lookup"><span data-stu-id="40391-115">.cmd, .bat, .exe (using windows cmd)</span></span>
* <span data-ttu-id="40391-116">.ps1(powershell 사용)</span><span class="sxs-lookup"><span data-stu-id="40391-116">.ps1 (using powershell)</span></span>
* <span data-ttu-id="40391-117">.sh(bash 사용)</span><span class="sxs-lookup"><span data-stu-id="40391-117">.sh (using bash)</span></span>
* <span data-ttu-id="40391-118">.php(php 사용)</span><span class="sxs-lookup"><span data-stu-id="40391-118">.php (using php)</span></span>
* <span data-ttu-id="40391-119">.py(python 사용)</span><span class="sxs-lookup"><span data-stu-id="40391-119">.py (using python)</span></span>
* <span data-ttu-id="40391-120">.js(node 사용)</span><span class="sxs-lookup"><span data-stu-id="40391-120">.js (using node)</span></span>
* <span data-ttu-id="40391-121">.jar(java 사용)</span><span class="sxs-lookup"><span data-stu-id="40391-121">.jar (using java)</span></span>

## <span data-ttu-id="40391-122"><a name="CreateOnDemand"></a>Hello 포털에서 주문형 WebJob 만들기</span><span class="sxs-lookup"><span data-stu-id="40391-122"><a name="CreateOnDemand"></a>Create an on demand WebJob in hello portal</span></span>
1. <span data-ttu-id="40391-123">Hello에 **웹 앱** hello의 블레이드에서 [Azure 포털](https://portal.azure.com), 클릭 **모든 설정 > WebJobs** tooshow hello **WebJobs** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="40391-123">In hello **Web App** blade of hello [Azure Portal](https://portal.azure.com), click **All settings > WebJobs** tooshow hello **WebJobs** blade.</span></span>
   
    ![WebJob 블레이드](./media/web-sites-create-web-jobs/wjblade.png)
2. <span data-ttu-id="40391-125">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-125">Click **Add**.</span></span> <span data-ttu-id="40391-126">hello **추가 WebJob** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="40391-126">hello **Add WebJob** dialog appears.</span></span>
   
    ![WebJob 블레이드 추가](./media/web-sites-create-web-jobs/addwjblade.png)
3. <span data-ttu-id="40391-128">아래 **이름**, WebJob hello에 대 한 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-128">Under **Name**, provide a name for hello WebJob.</span></span> <span data-ttu-id="40391-129">hello 이름은 문자 또는 숫자로 시작 해야 하며 이외의 특수 문자를 포함할 수 없습니다 "-" 및 "_"입니다.</span><span class="sxs-lookup"><span data-stu-id="40391-129">hello name must start with a letter or a number and cannot contain any special characters other than "-" and "_".</span></span>
4. <span data-ttu-id="40391-130">Hello에 **어떻게 tooRun** 상자 **요청 시 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-130">In hello **How tooRun** box, choose **Run on Demand**.</span></span>
5. <span data-ttu-id="40391-131">Hello에 **파일 업로드** 상자 hello 폴더 아이콘을 클릭 하 고 스크립트가 포함 된 toohello zip 파일을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-131">In hello **File Upload** box, click hello folder icon and browse toohello zip file that contains your script.</span></span> <span data-ttu-id="40391-132">hello zip 파일 필요한 toorun hello 프로그램 또는 스크립트 실행 파일 (.exe.cmd.bat.sh.php.py.js) 뿐만 아니라 모든 지원 파일 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-132">hello zip file should contain your executable (.exe .cmd .bat .sh .php .py .js) as well as any supporting files needed toorun hello program or script.</span></span>
6. <span data-ttu-id="40391-133">확인 **만들기** tooupload hello 스크립트 tooyour 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="40391-133">Check **Create** tooupload hello script tooyour web app.</span></span> 
   
    <span data-ttu-id="40391-134">hello WebJob hello에 대 한 지정 된 이름이 목록에 표시 hello hello **WebJobs** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="40391-134">hello name you specified for hello WebJob appears in hello list on hello **WebJobs** blade.</span></span>
7. <span data-ttu-id="40391-135">toorun hello WebJob을 클릭 하 고 hello 목록에서 해당 이름을 마우스 오른쪽 단추로 클릭 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-135">toorun hello WebJob, right-click its name in hello list and click **Run**.</span></span>
   
    ![WebJob 실행](./media/web-sites-create-web-jobs/runondemand.png)

## <span data-ttu-id="40391-137"><a name="CreateContinuous"></a>지속적으로 실행 중인 웹 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="40391-137"><a name="CreateContinuous"></a>Create a continuously running WebJob</span></span>
1. <span data-ttu-id="40391-138">toocreate 지속적으로 실행 중인 WebJob hello를 한 번 실행 되는 WebJob을 만들에 있지만 hello에 동일한 단계에 따라 **어떻게 tooRun** 상자 **Continuous**합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-138">toocreate a continuously executing WebJob, follow hello same steps for creating a WebJob that runs once, but in hello **How tooRun** box, choose **Continuous**.</span></span>
2. <span data-ttu-id="40391-139">toostart 또는 중지 연속 WebJob hello 목록에서 WebJob hello 마우스 오른쪽 단추로 클릭 **시작** 또는 **중지**합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-139">toostart or stop a continuous WebJob, right-click hello WebJob in hello list and click **Start** or **Stop**.</span></span>

> [!NOTE]
> <span data-ttu-id="40391-140">웹 앱이 둘 이상의 인스턴스에서 실행되는 경우 계속 실행되는 웹 작업은 모든 인스턴스에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="40391-140">If your web app runs on more than one instance, a continuously running WebJob will run on all of your instances.</span></span> <span data-ttu-id="40391-141">주문형 작업 및 예약형 작업은 Microsoft Azure의 부하 분산에 따라 선택된 단일 인스턴스에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="40391-141">On-demand and scheduled WebJobs run on a single instance selected for load balancing by Microsoft Azure.</span></span>
> 
> <span data-ttu-id="40391-142">연속 WebJobs에 대 한 toorun 안정적이 고 모든 인스턴스에 사용 Always On hello * 구성 설정을 앱에 대 한 hello 웹 그렇지 않으면 hello SCM 호스트 사이트 너무 오랫동안 유휴 되었을 때 실행을 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40391-142">For Continuous WebJobs toorun reliably and on all instances, enable hello Always On* configuration setting for hello web app otherwise they can stop running when hello SCM host site has been idle for too long.</span></span>
> 
> 

## <span data-ttu-id="40391-143"><a name="CreateScheduledCRON"></a>CRON 식을 사용하여 예정된 WebJob 만들기</span><span class="sxs-lookup"><span data-stu-id="40391-143"><a name="CreateScheduledCRON"></a>Create a scheduled WebJob using a CRON expression</span></span>
<span data-ttu-id="40391-144">이 기술은 기본, 표준 또는 프리미엄 모드에서 실행 되는 사용 가능한 tooWeb 앱으로 이루어지며 hello **Always On** toobe hello 앱에서 활성화를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-144">This technique is available tooWeb Apps running in Basic, Standard or Premium mode, and requires hello **Always On** setting toobe enabled on hello app.</span></span>

<span data-ttu-id="40391-145">단순히 tooturn 프로그램에서 요청 시 WebJob에 예약 된 WebJob 포함 한 `settings.job` WebJob zip 파일의 hello 루트에 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="40391-145">tooturn an On Demand WebJob into a scheduled WebJob, simply include a `settings.job` file at hello root of your WebJob zip file.</span></span> <span data-ttu-id="40391-146">이 JSON 파일에는 아래 예제별로 [CRON 식](https://en.wikipedia.org/wiki/Cron)이 포함된 `schedule` 속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-146">This JSON file should include a `schedule` property with a [CRON expression](https://en.wikipedia.org/wiki/Cron), per example below.</span></span>

<span data-ttu-id="40391-147">hello CRON 식은 6 개의 필드 이루어져: `{second} {minute} {hour} {day} {month} {day of hello week}`합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-147">hello CRON expression is composed of 6 fields: `{second} {minute} {hour} {day} {month} {day of hello week}`.</span></span>

<span data-ttu-id="40391-148">예를 들어 tootrigger WebJob 15 분 마다 프로그램 `settings.job` 갖기:</span><span class="sxs-lookup"><span data-stu-id="40391-148">For example, tootrigger your WebJob every 15 minutes, your `settings.job` would have:</span></span>

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

<span data-ttu-id="40391-149">다른 CRON 일정 예:</span><span class="sxs-lookup"><span data-stu-id="40391-149">Other CRON schedule examples:</span></span>

* <span data-ttu-id="40391-150">매 시간 마다 (즉, 때마다 hello 수 시간 (분)은 0 임).`0 0 * * * *`</span><span class="sxs-lookup"><span data-stu-id="40391-150">Every hour (i.e. whenever hello count of minutes is 0): `0 0 * * * *`</span></span> 
* <span data-ttu-id="40391-151">매 시간 마다 too5 오전 9 시에서에서 오후:`0 0 9-17 * * *`</span><span class="sxs-lookup"><span data-stu-id="40391-151">Every hour from 9 AM too5 PM: `0 0 9-17 * * *`</span></span> 
* <span data-ttu-id="40391-152">매일 오전 9시 30분: `0 30 9 * * *`</span><span class="sxs-lookup"><span data-stu-id="40391-152">At 9:30 AM every day: `0 30 9 * * *`</span></span>
* <span data-ttu-id="40391-153">평일 오전 9시 30분마다: `0 30 9 * * 1-5`</span><span class="sxs-lookup"><span data-stu-id="40391-153">At 9:30 AM every week day: `0 30 9 * * 1-5`</span></span>

<span data-ttu-id="40391-154">**참고**: Visual Studio에서 WebJob을 배포할 때는 있는지 toomark 확인 프로그램 `settings.job` '변경 된 내용만 복사'로 파일 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="40391-154">**Note**: when deploying a WebJob from Visual Studio, make sure toomark your `settings.job` file properties as 'Copy if newer'.</span></span>

## <span data-ttu-id="40391-155"><a name="CreateScheduled"></a>Hello Azure 스케줄러를 사용 하 여 예약 된 WebJob 만들기</span><span class="sxs-lookup"><span data-stu-id="40391-155"><a name="CreateScheduled"></a>Create a scheduled WebJob using hello Azure Scheduler</span></span>
<span data-ttu-id="40391-156">다른 방법은 다음 hello에서는 hello Azure 스케줄러를 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-156">hello following alternate technique makes use of hello Azure Scheduler.</span></span> <span data-ttu-id="40391-157">이 경우 WebJob hello 일정에 대 한 직접 정보는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="40391-157">In this case, your WebJob does not have any direct knowledge of hello schedule.</span></span> <span data-ttu-id="40391-158">대신, hello Azure 스케줄러를 가져옵니다 구성 된 tootrigger WebJob을 일정에 따라.</span><span class="sxs-lookup"><span data-stu-id="40391-158">Instead, hello Azure Scheduler gets configured tootrigger your WebJob on a schedule.</span></span> 

<span data-ttu-id="40391-159">해당 기능을 추가 하기 전에 hello를 사용 하 여 수행할 수 있습니다 하지만 hello Azure 포털에 아직 없는 hello 기능 toocreate 예약 된 WebJob [클래식 포털](http://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-159">hello Azure Portal doesn't yet have hello ability toocreate a scheduled WebJob, but until that feature is added you can do it by using hello [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="40391-160">Hello에 [클래식 포털](http://manage.windowsazure.com) toohello WebJob 페이지로 이동 하 고 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-160">In hello [classic portal](http://manage.windowsazure.com) go toohello WebJob page and click **Add**.</span></span>
2. <span data-ttu-id="40391-161">Hello에 **어떻게 tooRun** 상자 **일정에 따라 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-161">In hello **How tooRun** box, choose **Run on a schedule**.</span></span>
   
    ![새 예약형 작업][NewScheduledJob]
3. <span data-ttu-id="40391-163">Hello 선택 **스케줄러 지역** 작업에 대 한 hello 대화 tooproceed toohello 다음 화면 오른쪽의 아래쪽 hello에 hello 화살표를 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40391-163">Choose hello **Scheduler Region** for your job, and then click hello arrow on hello bottom right of hello dialog tooproceed toohello next screen.</span></span>
4. <span data-ttu-id="40391-164">Hello에 **작업 만들기** 대화 상자에서 hello 유형의 선택 **되풀이** 원하는: **일회성 작업** 또는 **되풀이 작업**합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-164">In hello **Create Job** dialog, choose hello type of **Recurrence** you want: **One-time job** or **Recurring job**.</span></span>
   
    ![되풀이 예약][SchdRecurrence]
5. <span data-ttu-id="40391-166">또한 **지금** 또는 **특정 시간** 중에 **시작** 시간을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-166">Also choose a **Starting** time: **Now** or **At a specific time**.</span></span>
   
    ![시작 시간 예약][SchdStart]
6. <span data-ttu-id="40391-168">특정 시간에 toostart를 원하는 경우 프로그램 시작 시간 값에서 선택 **시작에**합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-168">If you want toostart at a specific time, choose your starting time values under **Starting On**.</span></span>
   
    ![특정 시간에 시작 예약][SchdStartOn]
7. <span data-ttu-id="40391-170">Hello 있는 되풀이 작업을 선택한 경우 **되풀이 모든** 옵션 및 hello toospecify hello 주파수 **끝에** 옵션 toospecify 종료 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="40391-170">If you chose a recurring job, you have hello **Recur Every** option toospecify hello frequency of occurrence and hello **Ending On** option toospecify an ending time.</span></span>
   
    ![되풀이 예약][SchdRecurEvery]
8. <span data-ttu-id="40391-172">선택 하면 **주**, hello를 선택할 수 있습니다 **에 특정 일정** 상자 고 hello 요일을 hello 원하는 작업 toorun hello를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-172">If you choose **Weeks**, you can select hello **On a Particular Schedule** box and specify hello days of hello week that you want hello job toorun.</span></span>
   
    ![Hello 주 요일 일정][SchdWeeksOnParticular]
9. <span data-ttu-id="40391-174">선택 하면 **개월** 및 선택 hello **에 특정 일정** 상자 특정 번호가 매겨진에 hello 작업 toorun를 설정할 수 있습니다 **일** hello 달에 합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-174">If you choose **Months** and select hello **On a Particular Schedule** box, you can set hello job toorun on particular numbered **Days** in hello month.</span></span> 
   
    ![Hello 월의에서 특정 날짜 예약][SchdMonthsOnPartDays]
10. <span data-ttu-id="40391-176">선택 하면 **요일이**에 작업 toorun hello 원하는 hello 달에는 하루 또는 며칠 분의 hello 주를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40391-176">If you choose **Week Days**, you can select which day or days of hello week in hello month you want hello job toorun on.</span></span>
    
     ![한 달 중 특정 요일 예약][SchdMonthsOnPartWeekDays]
11. <span data-ttu-id="40391-178">마지막으로 hello를 사용 하 여 수도 있습니다 **발생** 옵션 toochoose hello 달의 주 (첫째, 둘째, 세 번째 등) hello 작업 toorun hello에 지정한 요일이 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-178">Finally, you can also use hello **Occurrences** option toochoose which week in hello month (first, second, third etc.) you want hello job toorun on hello week days you specified.</span></span>
    
    ![한 달 중 특정 주의 특정 요일 예약][SchdMonthsOnPartWeekDaysOccurences]
12. <span data-ttu-id="40391-180">하나 이상의 작업을 만든 후 해당 이름을 해당 상태, 일정 유형 및 기타 정보 hello WebJobs 탭에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40391-180">After you have created one or more jobs, their names will appear on hello WebJobs tab with their status, schedule type, and other information.</span></span> <span data-ttu-id="40391-181">기록 정보 hello 마지막 30 개의 WebJobs에 대 한 유지 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40391-181">Historical information for hello last 30  WebJobs is maintained.</span></span>
    
    ![작업 목록][WebJobsListWithSeveralJobs]

### <span data-ttu-id="40391-183"><a name="Scheduler"></a>예약된 작업 및 Azure 스케줄러</span><span class="sxs-lookup"><span data-stu-id="40391-183"><a name="Scheduler"></a>Scheduled jobs and Azure Scheduler</span></span>
<span data-ttu-id="40391-184">Hello의 hello Azure 스케줄러 페이지에 예약 된 작업을 추가로 구성할 수 있는 [클래식 포털](http://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-184">Scheduled jobs can be further configured in hello Azure Scheduler pages of hello [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="40391-185">Hello WebJobs 페이지 클릭 hello 작업 **일정** 링크 toonavigate toohello Azure 스케줄러 포털 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="40391-185">On hello WebJobs page, click hello job's **schedule** link toonavigate toohello Azure Scheduler portal page.</span></span> 
   
   ![링크 tooAzure 스케줄러][LinkToScheduler]
2. <span data-ttu-id="40391-187">Hello 스케줄러 페이지 hello 작업을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-187">On hello Scheduler page, click hello job.</span></span>
   
    ![Hello 스케줄러 포털 페이지에서 작업][SchedulerPortal]
3. <span data-ttu-id="40391-189">hello **작업 동작** 페이지가 열리면 hello 작업을 추가로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40391-189">hello **Job Action** page opens, where you can further configure hello job.</span></span> 
   
    ![스케줄러의 작업 동작 페이지][JobActionPageInScheduler]

## <span data-ttu-id="40391-191"><a name="ViewJobHistory"></a>Hello 작업 기록 보기</span><span class="sxs-lookup"><span data-stu-id="40391-191"><a name="ViewJobHistory"></a>View hello job history</span></span>
1. <span data-ttu-id="40391-192">hello에서의 해당 링크를 클릭 하는 hello WebJobs SDK를 사용 하 여 만든 작업을 포함 하는 작업의 tooview hello 실행 기록을 **로그** hello WebJobs 블레이드의 열입니다.</span><span class="sxs-lookup"><span data-stu-id="40391-192">tooview hello execution history of a job, including jobs created with hello WebJobs SDK, click  its corresponding link under hello **Logs** column of hello WebJobs blade.</span></span> <span data-ttu-id="40391-193">(사용할 수 있습니다 hello 로그 파일 페이지 toohello 클립보드의 hello 클립보드 아이콘 toocopy hello URL 하려는 경우.)</span><span class="sxs-lookup"><span data-stu-id="40391-193">(You can use hello clipboard icon toocopy hello URL of hello log file page toohello clipboard if you wish.)</span></span>
   
    ![로그 링크](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. <span data-ttu-id="40391-195">클릭 하 여 hello 링크 WebJob hello에 대 한 hello 세부 정보 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="40391-195">Clicking hello link opens hello details page for hello WebJob.</span></span> <span data-ttu-id="40391-196">이 페이지를 표시 이름 hello 명령 실행의 hello 실행 된 마지막 시간 및 성공 또는 실패를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-196">This page shows you hello name of hello command run, hello last times it ran, and its success or failure.</span></span> <span data-ttu-id="40391-197">아래 **최근 작업 실행**, 시간 toosee 추가 세부 정보를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-197">Under **Recent job runs**, click a time toosee further details.</span></span>
   
    ![WebJob 세부 정보][WebJobDetails]
3. <span data-ttu-id="40391-199">hello **WebJob 실행 세부 정보** 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="40391-199">hello **WebJob Run Details** page appears.</span></span> <span data-ttu-id="40391-200">클릭 **토글 출력** toosee hello 텍스트 hello 로그 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="40391-200">Click **Toggle Output** toosee hello text of hello log contents.</span></span> <span data-ttu-id="40391-201">hello 출력 로그는 텍스트 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="40391-201">hello output log is in text format.</span></span> 
   
    ![WebJob 실행 세부 작업][WebJobRunDetails]
4. <span data-ttu-id="40391-203">별도 브라우저 창에서 toosee hello 출력 텍스트 클릭 hello **다운로드** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-203">toosee hello output text in a separate browser window, click hello **download** link.</span></span> <span data-ttu-id="40391-204">toodownload hello 텍스트 자체 hello 링크를 마우스 오른쪽 단추로 클릭 하 고 브라우저 옵션 toosave hello 파일 내용을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-204">toodownload hello text itself, right-click hello link and use your browser options toosave hello file contents.</span></span>
   
    ![로그 출력 다운로드][DownloadLogOutput]
5. <span data-ttu-id="40391-206">hello **WebJobs** hello hello 페이지 맨 아래에 링크 hello 기록 대시보드에서 WebJobs의 편리한 방법을 tooget tooa 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-206">hello **WebJobs** link at hello top of hello page provides a convenient way tooget tooa list of WebJobs on hello history dashboard.</span></span>
   
    ![링크 tooWebJobs 목록][WebJobsLinkToDashboardList]
   
    ![기록 대시보드의 작업 목록][WebJobsListInJobsDashboard]
   
    <span data-ttu-id="40391-209">이러한 링크 중 하나를 클릭 하면 선택한 hello 작업에 대 한 WebJob 세부 정보 페이지 toohello 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-209">Clicking one of these links takes you toohello WebJob Details page for hello job you selected.</span></span>

## <span data-ttu-id="40391-210"><a name="WHPNotes"></a>참고 사항</span><span class="sxs-lookup"><span data-stu-id="40391-210"><a name="WHPNotes"></a>Notes</span></span>
* <span data-ttu-id="40391-211">무료 모드에서 웹 응용 프로그램 요청 toohello scm (배포) 사이트가 없는 있고 hello 웹 앱의 포털 Azure에서 열려 있지 않으면 20 분 후 시간 초과 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40391-211">Web apps in Free mode can time out after 20 minutes if there are no requests toohello scm (deployment) site and hello web app's portal is not open in Azure.</span></span> <span data-ttu-id="40391-212">요청 toohello 실제 사이트에이 다시 설정 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40391-212">Requests toohello actual site will not reset this.</span></span>
* <span data-ttu-id="40391-213">연속 작업에 대 한 코드는 무한 루프에서 toorun 작성 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="40391-213">Code for a continuous job needs toobe written toorun in an endless loop.</span></span>
* <span data-ttu-id="40391-214">Hello 웹 앱 중일 때에 연속 작업이 계속 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40391-214">Continuous jobs run continuously only when hello web app is up.</span></span>
* <span data-ttu-id="40391-215">기본 및 표준 모드 제공 hello 항상에 기능을 사용 하도록 설정 하면 웹 앱에서 유휴 상태가 되 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="40391-215">Basic and Standard modes offer hello Always On feature which, when enabled, prevents web apps from becoming idle.</span></span>
* <span data-ttu-id="40391-216">계속 실행되는 웹 작업만을 디버깅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40391-216">You can only debug continuously running WebJobs.</span></span> <span data-ttu-id="40391-217">예약된 또는 주문형 웹 작업 디버깅이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40391-217">Debugging scheduled or on-demand WebJobs is not supported.</span></span>

## <span data-ttu-id="40391-218"><a name="NextSteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="40391-218"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="40391-219">자세한 내용은 [Azure WebJobs 권장 리소스][WebJobsRecommendedResources]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40391-219">For more information, see [Azure WebJobs Recommended Resources][WebJobsRecommendedResources].</span></span>

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

