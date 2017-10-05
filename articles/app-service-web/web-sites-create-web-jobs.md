---
title: "WebJob으로 백그라운드 작업 실행"
description: "Azure 웹 앱에서 백그라운드 작업을 실행하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 3f8ae748e3d9c6b4e342536926a52b4e8f37ee51
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="run-background-tasks-with-webjobs"></a><span data-ttu-id="1f739-103">WebJob으로 백그라운드 작업 실행</span><span class="sxs-lookup"><span data-stu-id="1f739-103">Run Background tasks with WebJobs</span></span>
## <a name="overview"></a><span data-ttu-id="1f739-104">개요</span><span class="sxs-lookup"><span data-stu-id="1f739-104">Overview</span></span>
<span data-ttu-id="1f739-105">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) 웹앱의 WebJobs에서 세 가지 방법, 즉 요청 시, 계속 실행 또는 일정에 따라 프로그램이나 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-105">You can run programs or scripts in WebJobs in your [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web app in three ways: on demand, continuously, or on a schedule.</span></span> <span data-ttu-id="1f739-106">웹 작업을 사용하는 데 추가 비용은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-106">There is no additional cost to use WebJobs.</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="1f739-107">이 문서에서는 [Azure 포털](https://portal.azure.com)에서 웹 작업을 배포하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-107">This article shows how to deploy WebJobs by using the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="1f739-108">Visual Studio 또는 지속적인 전송 프로세스를 사용하여 배포하는 방법에 대한 자세한 내용은 [Azure 웹 작업을 웹 앱에 배포하는 방법](websites-dotnet-deploy-webjobs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f739-108">For information about how to deploy by using Visual Studio or a continuous delivery process, see [How to Deploy Azure WebJobs to Web Apps](websites-dotnet-deploy-webjobs.md).</span></span>

<span data-ttu-id="1f739-109">Azure WebJobs SDK는 많은 웹 작업 프로그래밍 작업을 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-109">The Azure WebJobs SDK simplifies many WebJobs programming tasks.</span></span> <span data-ttu-id="1f739-110">자세한 내용은 [WebJobs SDK 정의](websites-dotnet-webjobs-sdk.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f739-110">For more information, see [What is the WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

 <span data-ttu-id="1f739-111">Azure Functions는 서버가 없는 환경이나 App Service 앱에서 프로그램과 스크립트를 실행할 수 있는 또 다른 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-111">Azure Functions provides another way to run programs and scripts from either a serverless environment or from an App Service app.</span></span> <span data-ttu-id="1f739-112">자세한 내용은 [Azure Functions 개요](../azure-functions/functions-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f739-112">For more information, see [Azure Functions overview](../azure-functions/functions-overview.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="1f739-113"><a name="acceptablefiles"></a>스크립트 또는 프로그램에 허용 가능한 파일 형식</span><span class="sxs-lookup"><span data-stu-id="1f739-113"><a name="acceptablefiles"></a>Acceptable file types for scripts or programs</span></span>
<span data-ttu-id="1f739-114">다음 파일 형식이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-114">The following file types are accepted:</span></span>

* <span data-ttu-id="1f739-115">.cmd, .bat, .exe(windows cmd 사용)</span><span class="sxs-lookup"><span data-stu-id="1f739-115">.cmd, .bat, .exe (using windows cmd)</span></span>
* <span data-ttu-id="1f739-116">.ps1(powershell 사용)</span><span class="sxs-lookup"><span data-stu-id="1f739-116">.ps1 (using powershell)</span></span>
* <span data-ttu-id="1f739-117">.sh(bash 사용)</span><span class="sxs-lookup"><span data-stu-id="1f739-117">.sh (using bash)</span></span>
* <span data-ttu-id="1f739-118">.php(php 사용)</span><span class="sxs-lookup"><span data-stu-id="1f739-118">.php (using php)</span></span>
* <span data-ttu-id="1f739-119">.py(python 사용)</span><span class="sxs-lookup"><span data-stu-id="1f739-119">.py (using python)</span></span>
* <span data-ttu-id="1f739-120">.js(node 사용)</span><span class="sxs-lookup"><span data-stu-id="1f739-120">.js (using node)</span></span>
* <span data-ttu-id="1f739-121">.jar(java 사용)</span><span class="sxs-lookup"><span data-stu-id="1f739-121">.jar (using java)</span></span>

## <span data-ttu-id="1f739-122"><a name="CreateOnDemand"></a>포털에서 요청 시 웹 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="1f739-122"><a name="CreateOnDemand"></a>Create an on demand WebJob in the portal</span></span>
1. <span data-ttu-id="1f739-123">[Azure Portal](https://portal.azure.com)의 **웹앱** 블레이드에서 **모든 설정 > WebJobs**을 클릭하여 **WebJobs** 블레이드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-123">In the **Web App** blade of the [Azure Portal](https://portal.azure.com), click **All settings > WebJobs** to show the **WebJobs** blade.</span></span>
   
    ![WebJob 블레이드](./media/web-sites-create-web-jobs/wjblade.png)
2. <span data-ttu-id="1f739-125">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-125">Click **Add**.</span></span> <span data-ttu-id="1f739-126">**웹 작업 추가** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-126">The **Add WebJob** dialog appears.</span></span>
   
    ![WebJob 블레이드 추가](./media/web-sites-create-web-jobs/addwjblade.png)
3. <span data-ttu-id="1f739-128">**이름**에 웹 작업의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-128">Under **Name**, provide a name for the WebJob.</span></span> <span data-ttu-id="1f739-129">이름은 문자 또는 숫자로 시작해야 하며 "-" 및 "_"을 제외한 다른 특수 문자를 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-129">The name must start with a letter or a number and cannot contain any special characters other than "-" and "_".</span></span>
4. <span data-ttu-id="1f739-130">**실행 방법** 상자에서 **주문에 따라 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-130">In the **How to Run** box, choose **Run on Demand**.</span></span>
5. <span data-ttu-id="1f739-131">**파일 업로드** 상자에서 폴더 아이콘을 클릭하고 스크립트가 포함된 zip 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-131">In the **File Upload** box, click the folder icon and browse to the zip file that contains your script.</span></span> <span data-ttu-id="1f739-132">zip 파일에는 실행 파일(.exe .cmd .bat .sh .php .py .js)과 더불어 프로그램 또는 스크립트를 실행하는 데 필요한 지원 파일이 포함되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-132">The zip file should contain your executable (.exe .cmd .bat .sh .php .py .js) as well as any supporting files needed to run the program or script.</span></span>
6. <span data-ttu-id="1f739-133">**만들기** 를 선택하여 웹 앱에 스크립트를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-133">Check **Create** to upload the script to your web app.</span></span> 
   
    <span data-ttu-id="1f739-134">웹 작업에 지정된 이름은 **웹 작업** 블레이드의 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-134">The name you specified for the WebJob appears in the list on the **WebJobs** blade.</span></span>
7. <span data-ttu-id="1f739-135">웹 작업을 실행하려면 목록에서 해당 이름을 마우스 오른쪽 단추로 클릭하고 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-135">To run the WebJob, right-click its name in the list and click **Run**.</span></span>
   
    ![WebJob 실행](./media/web-sites-create-web-jobs/runondemand.png)

## <span data-ttu-id="1f739-137"><a name="CreateContinuous"></a>지속적으로 실행 중인 웹 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="1f739-137"><a name="CreateContinuous"></a>Create a continuously running WebJob</span></span>
1. <span data-ttu-id="1f739-138">지속적으로 실행하는 WebJob을 만들려면, 한 번 실행되는 WebJob을 만드는 단계를 그대로 따르고 **실행 방법** 상자에서 **연속**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-138">To create a continuously executing WebJob, follow the same steps for creating a WebJob that runs once, but in the **How to Run** box, choose **Continuous**.</span></span>
2. <span data-ttu-id="1f739-139">지속적인 WebJob을 시작하거나 중지하려면 목록에서 WebJob을 마우스 오른쪽 단추로 클릭하고 **시작** 또는 **중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-139">To start or stop a continuous WebJob, right-click the WebJob in the list and click **Start** or **Stop**.</span></span>

> [!NOTE]
> <span data-ttu-id="1f739-140">웹 앱이 둘 이상의 인스턴스에서 실행되는 경우 계속 실행되는 웹 작업은 모든 인스턴스에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-140">If your web app runs on more than one instance, a continuously running WebJob will run on all of your instances.</span></span> <span data-ttu-id="1f739-141">주문형 작업 및 예약형 작업은 Microsoft Azure의 부하 분산에 따라 선택된 단일 인스턴스에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-141">On-demand and scheduled WebJobs run on a single instance selected for load balancing by Microsoft Azure.</span></span>
> 
> <span data-ttu-id="1f739-142">연속하는 WebJob을 모든 인스턴스에서 안정적으로 실행하려면 웹앱에 대한 항상 위* 구성 설정을 사용하도록 설정합니다. 그렇지 않으면 SCM 호스트 사이트를 오래 동안 사용하지 않을 경우 실행이 중지될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-142">For Continuous WebJobs to run reliably and on all instances, enable the Always On* configuration setting for the web app otherwise they can stop running when the SCM host site has been idle for too long.</span></span>
> 
> 

## <span data-ttu-id="1f739-143"><a name="CreateScheduledCRON"></a>CRON 식을 사용하여 예정된 WebJob 만들기</span><span class="sxs-lookup"><span data-stu-id="1f739-143"><a name="CreateScheduledCRON"></a>Create a scheduled WebJob using a CRON expression</span></span>
<span data-ttu-id="1f739-144">이 기술은 기본, 표준 또는 프리미엄 모드에서 실행 중인 웹앱에 제공되며 앱에서 **Always On** 설정을 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-144">This technique is available to Web Apps running in Basic, Standard or Premium mode, and requires the **Always On** setting to be enabled on the app.</span></span>

<span data-ttu-id="1f739-145">주문형 WebJob을 예정된 WebJob으로 설정하려면 WebJob zip 파일의 루트에 `settings.job` 파일을 포함하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-145">To turn an On Demand WebJob into a scheduled WebJob, simply include a `settings.job` file at the root of your WebJob zip file.</span></span> <span data-ttu-id="1f739-146">이 JSON 파일에는 아래 예제별로 [CRON 식](https://en.wikipedia.org/wiki/Cron)이 포함된 `schedule` 속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-146">This JSON file should include a `schedule` property with a [CRON expression](https://en.wikipedia.org/wiki/Cron), per example below.</span></span>

<span data-ttu-id="1f739-147">CRON 식은 6개의 필드로 구성되어 있습니다. `{second} {minute} {hour} {day} {month} {day of the week}`.</span><span class="sxs-lookup"><span data-stu-id="1f739-147">The CRON expression is composed of 6 fields: `{second} {minute} {hour} {day} {month} {day of the week}`.</span></span>

<span data-ttu-id="1f739-148">예를 들어 15분마다 WebJob을 트리거하려면 `settings.job`에 다음 사항이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-148">For example, to trigger your WebJob every 15 minutes, your `settings.job` would have:</span></span>

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

<span data-ttu-id="1f739-149">다른 CRON 일정 예:</span><span class="sxs-lookup"><span data-stu-id="1f739-149">Other CRON schedule examples:</span></span>

* <span data-ttu-id="1f739-150">1시간마다(즉, 분을 나타내는 숫자가 0일 때마다): `0 0 * * * *`</span><span class="sxs-lookup"><span data-stu-id="1f739-150">Every hour (i.e. whenever the count of minutes is 0): `0 0 * * * *`</span></span> 
* <span data-ttu-id="1f739-151">오전 9시에서 오후 5시까지 1시간마다: `0 0 9-17 * * *`</span><span class="sxs-lookup"><span data-stu-id="1f739-151">Every hour from 9 AM to 5 PM: `0 0 9-17 * * *`</span></span> 
* <span data-ttu-id="1f739-152">매일 오전 9시 30분: `0 30 9 * * *`</span><span class="sxs-lookup"><span data-stu-id="1f739-152">At 9:30 AM every day: `0 30 9 * * *`</span></span>
* <span data-ttu-id="1f739-153">평일 오전 9시 30분마다: `0 30 9 * * 1-5`</span><span class="sxs-lookup"><span data-stu-id="1f739-153">At 9:30 AM every week day: `0 30 9 * * 1-5`</span></span>

<span data-ttu-id="1f739-154">**참고**: Visual Studio에서 WebJob을 배포하는 경우 `settings.job` 파일 속성이 '변경된 내용만 복사'로 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-154">**Note**: when deploying a WebJob from Visual Studio, make sure to mark your `settings.job` file properties as 'Copy if newer'.</span></span>

## <span data-ttu-id="1f739-155"><a name="CreateScheduled"></a>Azure 스케줄러를 사용하여 예정된 WebJob 만들기</span><span class="sxs-lookup"><span data-stu-id="1f739-155"><a name="CreateScheduled"></a>Create a scheduled WebJob using the Azure Scheduler</span></span>
<span data-ttu-id="1f739-156">다음 대체 기술은 Azure 스케줄러를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-156">The following alternate technique makes use of the Azure Scheduler.</span></span> <span data-ttu-id="1f739-157">이 경우 WebJob에 일정의 직접적인 정보가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-157">In this case, your WebJob does not have any direct knowledge of the schedule.</span></span> <span data-ttu-id="1f739-158">대신 Azure 스케줄러는 일정에서 WebJob을 트리거하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-158">Instead, the Azure Scheduler gets configured to trigger your WebJob on a schedule.</span></span> 

<span data-ttu-id="1f739-159">Azure 포털은 아직 예약된 웹 작업을 만들 수 없지만, [클래식 포털](http://manage.windowsazure.com)을 사용하여 기능이 추가될 때까지 예약된 웹 작업을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-159">The Azure Portal doesn't yet have the ability to create a scheduled WebJob, but until that feature is added you can do it by using the [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="1f739-160">[클래식 포털](http://manage.windowsazure.com) 에서 웹 작업 페이지로 이동하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-160">In the [classic portal](http://manage.windowsazure.com) go to the WebJob page and click **Add**.</span></span>
2. <span data-ttu-id="1f739-161">**실행 방법** 상자에서 **일정에 따라 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-161">In the **How to Run** box, choose **Run on a schedule**.</span></span>
   
    ![새 예약형 작업][NewScheduledJob]
3. <span data-ttu-id="1f739-163">작업에 대해 **Scheduler Region** 을 선택하고 대화 상자의 오른쪽 아래에 있는 화살표를 클릭하여 다음 화면으로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-163">Choose the **Scheduler Region** for your job, and then click the arrow on the bottom right of the dialog to proceed to the next screen.</span></span>
4. <span data-ttu-id="1f739-164">**작업 만들기** 대화 상자에서 **일회성 작업** 또는 **작업 되풀이** 중 원하는 **되풀이** 유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-164">In the **Create Job** dialog, choose the type of **Recurrence** you want: **One-time job** or **Recurring job**.</span></span>
   
    ![되풀이 예약][SchdRecurrence]
5. <span data-ttu-id="1f739-166">또한 **지금** 또는 **특정 시간** 중에 **시작** 시간을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-166">Also choose a **Starting** time: **Now** or **At a specific time**.</span></span>
   
    ![시작 시간 예약][SchdStart]
6. <span data-ttu-id="1f739-168">특정 시간에 시작하려면 **Starting On**에서 시작 시간 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-168">If you want to start at a specific time, choose your starting time values under **Starting On**.</span></span>
   
    ![특정 시간에 시작 예약][SchdStartOn]
7. <span data-ttu-id="1f739-170">되풀이 작업을 선택한 경우 발생 빈도를 지정하는 **되풀이 간격** 옵션과 종료 시간을 지정하는 **Ending On** 옵션이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-170">If you chose a recurring job, you have the **Recur Every** option to specify the frequency of occurrence and the **Ending On** option to specify an ending time.</span></span>
   
    ![되풀이 예약][SchdRecurEvery]
8. <span data-ttu-id="1f739-172">**주**를 선택하는 경우 **특정 일정에 따라** 상자를 선택하고 작업을 실행하려는 요일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-172">If you choose **Weeks**, you can select the **On a Particular Schedule** box and specify the days of the week that you want the job to run.</span></span>
   
    ![요일 예약][SchdWeeksOnParticular]
9. <span data-ttu-id="1f739-174">**월**을 선택하고 **특정 일정에 따라** 상자를 선택한 경우 한 달 중 특정 **일**에 실행하도록 작업을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-174">If you choose **Months** and select the **On a Particular Schedule** box, you can set the job to run on particular numbered **Days** in the month.</span></span> 
   
    ![한 달 중 특정 날짜 예약][SchdMonthsOnPartDays]
10. <span data-ttu-id="1f739-176">**Week Days**를 선택하면 작업을 실행하려는 해당 달의 요일을 하나 이상 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-176">If you choose **Week Days**, you can select which day or days of the week in the month you want the job to run on.</span></span>
    
     ![한 달 중 특정 요일 예약][SchdMonthsOnPartWeekDays]
11. <span data-ttu-id="1f739-178">마지막으로 **발생** 옵션을 사용하면 작업을 실행하도록 지정한 요일이 한 달 중 몇 번째 주(첫째, 둘째, 셋째 등)에 해당하는지를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-178">Finally, you can also use the **Occurrences** option to choose which week in the month (first, second, third etc.) you want the job to run on the week days you specified.</span></span>
    
    ![한 달 중 특정 주의 특정 요일 예약][SchdMonthsOnPartWeekDaysOccurences]
12. <span data-ttu-id="1f739-180">하나 이상의 작업을 만들면 WebJobs 탭에 작업의 상태, 일정 유형 및 기타 정보와 함께 이름이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-180">After you have created one or more jobs, their names will appear on the WebJobs tab with their status, schedule type, and other information.</span></span> <span data-ttu-id="1f739-181">최근 30개의 WebJobs 기록 정보가 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-181">Historical information for the last 30  WebJobs is maintained.</span></span>
    
    ![작업 목록][WebJobsListWithSeveralJobs]

### <span data-ttu-id="1f739-183"><a name="Scheduler"></a>예약된 작업 및 Azure 스케줄러</span><span class="sxs-lookup"><span data-stu-id="1f739-183"><a name="Scheduler"></a>Scheduled jobs and Azure Scheduler</span></span>
<span data-ttu-id="1f739-184">[클래식 포털](http://manage.windowsazure.com)의 Azure 스케줄러 페이지에서 예약된 작업을 추가로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-184">Scheduled jobs can be further configured in the Azure Scheduler pages of the [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="1f739-185">Azure 스케줄러 포털 페이지로 이동하려면 WebJobs 페이지에서 작업의 **일정** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-185">On the WebJobs page, click the job's **schedule** link to navigate to the Azure Scheduler portal page.</span></span> 
   
   ![Azure 스케줄러 링크][LinkToScheduler]
2. <span data-ttu-id="1f739-187">스케줄러 페이지에서 작업을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-187">On the Scheduler page, click the job.</span></span>
   
    ![스케줄러 포털 페이지의 작업][SchedulerPortal]
3. <span data-ttu-id="1f739-189">작업을 추가로 구성할 수 있는 **Job Action** 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-189">The **Job Action** page opens, where you can further configure the job.</span></span> 
   
    ![스케줄러의 작업 동작 페이지][JobActionPageInScheduler]

## <span data-ttu-id="1f739-191"><a name="ViewJobHistory"></a>작업 기록 보기</span><span class="sxs-lookup"><span data-stu-id="1f739-191"><a name="ViewJobHistory"></a>View the job history</span></span>
1. <span data-ttu-id="1f739-192">WebJobs SDK로 만든 작업을 포함하여 작업 실행 기록을 보려면 WebJobs 블레이드의 **로그** 열에서 해당 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-192">To view the execution history of a job, including jobs created with the WebJobs SDK, click  its corresponding link under the **Logs** column of the WebJobs blade.</span></span> <span data-ttu-id="1f739-193">원하는 경우 클립보드 아이콘을 사용하여 로그 파일 페이지의 URL을 클립보드로 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-193">(You can use the clipboard icon to copy the URL of the log file page to the clipboard if you wish.)</span></span>
   
    ![로그 링크](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. <span data-ttu-id="1f739-195">링크를 클릭하면 웹 작업에 대한 세부 정보 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-195">Clicking the link opens the details page for the WebJob.</span></span> <span data-ttu-id="1f739-196">이 페이지에는 명령 실행 이름, 마지막으로 실행한 시간 및 명령 성공/실패 여부가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-196">This page shows you the name of the command run, the last times it ran, and its success or failure.</span></span> <span data-ttu-id="1f739-197">**Recent job runs**에서 시간을 클릭하면 추가 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-197">Under **Recent job runs**, click a time to see further details.</span></span>
   
    ![WebJob 세부 정보][WebJobDetails]
3. <span data-ttu-id="1f739-199">**WebJob Run Details** 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-199">The **WebJob Run Details** page appears.</span></span> <span data-ttu-id="1f739-200">로그 내용의 텍스트를 보려면 **Toggle Output** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-200">Click **Toggle Output** to see the text of the log contents.</span></span> <span data-ttu-id="1f739-201">출력 로그는 텍스트 형식으로 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-201">The output log is in text format.</span></span> 
   
    ![WebJob 실행 세부 작업][WebJobRunDetails]
4. <span data-ttu-id="1f739-203">별도의 브라우저 창에서 출력 텍스트를 보려면 **다운로드** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-203">To see the output text in a separate browser window, click the **download** link.</span></span> <span data-ttu-id="1f739-204">텍스트 자체를 다운로드하려면 링크를 마우스 오른쪽 단추로 클릭하고 브라우저 옵션을 사용하여 파일 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-204">To download the text itself, right-click the link and use your browser options to save the file contents.</span></span>
   
    ![로그 출력 다운로드][DownloadLogOutput]
5. <span data-ttu-id="1f739-206">페이지 맨 위의 **웹 작업** 링크를 사용하면 기록 대시보드의 웹 작업 목록을 편리하게 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-206">The **WebJobs** link at the top of the page provides a convenient way to get to a list of WebJobs on the history dashboard.</span></span>
   
    ![WebJobs 목록 링크][WebJobsLinkToDashboardList]
   
    ![기록 대시보드의 작업 목록][WebJobsListInJobsDashboard]
   
    <span data-ttu-id="1f739-209">이러한 링크 중 하나를 클릭하면 선택한 작업의 WebJob Details 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-209">Clicking one of these links takes you to the WebJob Details page for the job you selected.</span></span>

## <span data-ttu-id="1f739-210"><a name="WHPNotes"></a>참고 사항</span><span class="sxs-lookup"><span data-stu-id="1f739-210"><a name="WHPNotes"></a>Notes</span></span>
* <span data-ttu-id="1f739-211">무료 모드의 웹앱은 SCM(배포) 사이트에 대한 요청이 없는 경우 20분 후 시간 초과되고 웹앱의 포털이 Azure에서 열리지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-211">Web apps in Free mode can time out after 20 minutes if there are no requests to the scm (deployment) site and the web app's portal is not open in Azure.</span></span> <span data-ttu-id="1f739-212">실제 사이트에 대한 요청이 있어도 이는 다시 설정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-212">Requests to the actual site will not reset this.</span></span>
* <span data-ttu-id="1f739-213">연속 작업을 위한 코드는 무한 반복으로 실행되도록 작성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-213">Code for a continuous job needs to be written to run in an endless loop.</span></span>
* <span data-ttu-id="1f739-214">연속 작업은 웹 앱이 실행되고 있는 경우에만 계속 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-214">Continuous jobs run continuously only when the web app is up.</span></span>
* <span data-ttu-id="1f739-215">기본 및 표준 모드에는 무중단 기능이 제공되며, 이 기능을 사용하도록 설정하면 웹 앱이 유휴 상태로 전환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-215">Basic and Standard modes offer the Always On feature which, when enabled, prevents web apps from becoming idle.</span></span>
* <span data-ttu-id="1f739-216">계속 실행되는 웹 작업만을 디버깅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-216">You can only debug continuously running WebJobs.</span></span> <span data-ttu-id="1f739-217">예약된 또는 주문형 웹 작업 디버깅이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f739-217">Debugging scheduled or on-demand WebJobs is not supported.</span></span>

## <span data-ttu-id="1f739-218"><a name="NextSteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="1f739-218"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="1f739-219">자세한 내용은 [Azure WebJobs 권장 리소스][WebJobsRecommendedResources]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f739-219">For more information, see [Azure WebJobs Recommended Resources][WebJobsRecommendedResources].</span></span>

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

