---
title: "Mobile Engagement 사용자 인터페이스-aaaAzure 분석"
description: "자세한 내용은 방법 tooanalyze Azure Mobile Engagement 응용 프로그램에 대 한 기록 데이터"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6b2533ac-b8ec-4e35-872c-d563895bdc0c
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4a9df11226fed6710cfb1337ae84ece7596d482f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooanalyze-historical-data-about-your-application"></a><span data-ttu-id="67716-103">어떻게 tooanalyze 응용 프로그램에 대 한 기록 데이터</span><span class="sxs-lookup"><span data-stu-id="67716-103">How tooanalyze historical data about your application</span></span>
<span data-ttu-id="67716-104">이 문서에서는 hello 설명 **분석** hello 탭 **Mobile Engagement** 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="67716-104">This article describes hello **ANALYTICS** tab of hello **Mobile Engagement** portal.</span></span> <span data-ttu-id="67716-105">Hello를 사용 하 여 **Mobile Engagement** 포털 toomonitor 모바일 앱을 관리 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67716-105">You use hello **Mobile Engagement** portal toomonitor and manage your mobile apps.</span></span> <span data-ttu-id="67716-106">먼저 toocreate hello 포털을 사용 하 여 해당 toostart 참고는 **Azure Mobile Engagement** 계정.</span><span class="sxs-lookup"><span data-stu-id="67716-106">Note that toostart using hello portal you first need toocreate an **Azure Mobile Engagement** account.</span></span>

<span data-ttu-id="67716-107">hello hello UI의 분석 섹션 24 시간 마다 업데이트 되는 기록 데이터에 따라 응용 프로그램에 대 한 집계 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="67716-107">hello Analytics section of hello UI provides aggregated information about your application based on historic data that is updated every 24 hours.</span></span> <span data-ttu-id="67716-108">원형/선/가로 막대형 차트, 표, 및 맵을 구성 하는 다른 여러 대시보드에 hello 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67716-108">hello information is displayed on different dashboards composed of line/bar/pie charts, grids, and maps.</span></span> <span data-ttu-id="67716-109">hello 데이터를.csv 파일로 다운로드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67716-109">hello data can also be downloaded as .csv files.</span></span> <span data-ttu-id="67716-110">대부분의 동일한 정보 hello hello UI의 모니터 섹션에서에서 실시간으로 사용할 수 있으며 hello 분석 API에서에서 액세스할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67716-110">Most of this same information is available in real time in hello Monitor section of hello UI, and it can also be accessed from hello Analytics API.</span></span>

> [!NOTE]
> <span data-ttu-id="67716-111">섹션의 hello **Mobile Engagement** 포털 UI hello 포함 **도움말 표시** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="67716-111">Many sections of hello **Mobile Engagement** portal UI contain hello **SHOW HELP** button.</span></span> <span data-ttu-id="67716-112">이 단추 tooget 섹션에 대 한 자세한 컨텍스트 정보를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="67716-112">Press this button tooget more contextual information about a section.</span></span>

## <a name="standard-and-custom-analytics"></a><span data-ttu-id="67716-113">표준 분석 및 사용자 지정 분석</span><span class="sxs-lookup"><span data-stu-id="67716-113">Standard and Custom Analytics</span></span>
<span data-ttu-id="67716-114">Azure Mobile Engagement의 SDK hello로 앱을 통합 하는 즉시 그래프로 나타낼 수 있는 응용 프로그램에 대 한 기본, 표준 분석 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="67716-114">Azure Mobile Engagement provides a set of basic, standard analytic information about your applications that can be graphed as soon as you integrate your app with hello SDK.</span></span> <span data-ttu-id="67716-115">또한 azure Mobile Engagement hello 기능 toogather 추가 사용자 지정 분석 원하는 정보를 최종 사용자의 동작에 대 한를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="67716-115">Azure Mobile Engagement also provides hello ability toogather additional custom analytics information that you want about your end-users' behavior.</span></span> <span data-ttu-id="67716-116">이러한 정보를 수집하려면 Azure Mobile Engagement에서 해당 추가 데이터를 자동으로 수집할 수 있도록 사용자 지정 "태그(앱 정보)"를 사용하는 태그 계획을 **설정** 에서 작성하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67716-116">You can do this by creating a tag plan of custom "Tags (app info)", created from **Settings** so that Azure Mobile Engagement can collect this additional data for you.</span></span>

## <a name="analytics"></a><span data-ttu-id="67716-117">분석</span><span class="sxs-lookup"><span data-stu-id="67716-117">Analytics</span></span>
* <span data-ttu-id="67716-118">대시보드: 새 사용자와 활성 사용자 및 해당 추세에 대한 일반 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="67716-118">Dashboard: Shows general information about your new and actives users and their trends.</span></span>
* <span data-ttu-id="67716-119">사용자: 장치 식별자를 통해 사용자를 식별합니다. 이 식별자는 각 장치에서 고유합니다. 각각의 새 사용자는 새 장치 하나에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="67716-119">Users: Users are identified by their device identifier: this identifier is unique for each device (one new user is actually one new device).</span></span> <span data-ttu-id="67716-120">사용자는 지정된 시간 간격 동안 첫 번째 세션을 수행하는 경우 새 사용자로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="67716-120">A user is considered as new on a given time interval if he has performed his first session during this time interval.</span></span> <span data-ttu-id="67716-121">사용자는 hello 중 적어도 하나의 세션 지난 7 일 동안 수행한 경우 보존로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67716-121">A user is considered as retained if he has performed at least one session during hello last 7 days.</span></span> <span data-ttu-id="67716-122">활성 사용자는 지정된 기간 동안 세션을 하나 이상 만든 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="67716-122">Active Users are users that made at least one session during a given period.</span></span> <span data-ttu-id="67716-123">기간(월/주/일/시간)을 기준으로 정렬할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67716-123">You can sort by, monthly, weekly, daily, or hourly time periods.</span></span> <span data-ttu-id="67716-124">모든 hello 차트의와 유사 하지만 수 toofilter 고 응용 프로그램에 다음 toosort의 hello 버전과 같은 다양 한 기능으로 시간 동안.</span><span class="sxs-lookup"><span data-stu-id="67716-124">All of hello charts look similar but allow you toofilter by different features, such as hello version of your application, and then toosort by a period of time.</span></span> <span data-ttu-id="67716-125">hello hello SDK를 통합 하 여 수집한 정보를 표준 hello 다음과 같습니다: 활성 사용자, 새 사용자, 세션의 수, 길이 각 세션, hello 국가, 지역, 위치, 통신 회사 언어, 장치, 펌웨어에 대 한 기술 정보 네트워크 (WIFI) hello 앱 및 고객에 의해 사용 되는 SDK의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="67716-125">hello standard information gathered by integrating hello SDK includes hello following: Active users, new user, number of sessions, length of each session, technical information about hello country, locals, location, language carrier, devices, firmware, network (WIFI), versions of hello app and SDK, used by customers.</span></span> <span data-ttu-id="67716-126">이 정보는 hello 모니터 섹션에서 실시간으로에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67716-126">This information can be viewed in real time from hello monitor section.</span></span>

> [!NOTE]
> <span data-ttu-id="67716-127">hello 시간 동안은 기반 hello 사용자의 장치 설정에서 hello 날짜 하므로 해당 휴대폰 잘못 설정 하는 hello 날짜에 사용자 표시 될 수 hello에 잘못 된 시간 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="67716-127">hello time period is based on hello date from hello users' device settings, so a user whose phone has hello date incorrectly set could show up in hello wrong time period.</span></span>

* <span data-ttu-id="67716-128">재방문 주기: 지정된 시간 간격 동안 첫 번째 세션을 수행한 사용자는 재방문 사용자로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="67716-128">Retention: A user is considered as retained on a given time interval if he has performed his first session during this time interval.</span></span> <span data-ttu-id="67716-129">보존 된 사용자 (및 새 사용자)가 계산 되는 toohours, 일, 주 또는 월 hello 시간 간격을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67716-129">You can change hello time intervals during which retained users (and new users) are counted toohours, days, weeks, or months.</span></span> <span data-ttu-id="67716-130">hello 사용자 보존 분석 패 거리 들은 위에 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="67716-130">hello user retention analytics is built on top of cohorts.</span></span> <span data-ttu-id="67716-131">Cohort는 hello 집합 모든 hello 새 사용자 지정 된 기간 (즉,이 기간 동안 첫 번째 세션을 수행 하는 사용자 hello 집합)에 대 한 검색입니다.</span><span class="sxs-lookup"><span data-stu-id="67716-131">A cohort is hello set of all hello new users detected for a given period (i.e., hello set of users performing their first session during this period).</span></span> <span data-ttu-id="67716-132">Azure Mobile Engagement에서는 1일/2일/4일/7일/1개월에 해당하는 집단을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="67716-132">We use cohorts of 1-day, 2-day, 4-day, 7-day, or 1-month.</span></span> <span data-ttu-id="67716-133">집합이 지정 된 경우 모든 1 일, 2 일, 4 일, 7 일 또는 1 개월 코 호트 Azure Mobile Engagement에서는 hello 모든 사용자가 속할 toohello 코 호트 및가 여전히 활성 상태 (예: hello 기간 중 최소 하나의 세션에서 수행 하는 사용자 hello 집합).</span><span class="sxs-lookup"><span data-stu-id="67716-133">Given a cohort, every 1-day, 2-day, 4-day, 7-day, or 1-month, Azure Mobile Engagement computes hello set of all users who belong toohello cohort and are still active (i.e., hello set of users who performed at least one session during hello period).</span></span> <span data-ttu-id="67716-134">이 사용자 집합을 집단 버전이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="67716-134">This set of users is called a cohort version.</span></span> <span data-ttu-id="67716-135">(Azure Mobile Engagement 표시 될 수 있습니다 사용자의 수가 계속 사용 하는 응용 프로그램 있지만 유일한 hello 플랫폼 특정 저장소를 전달할 수 있습니다 수의 사용자 Windows 스토어 앱-예를 들어 GooglePlay iTunes 프로그램 제거 등.).</span><span class="sxs-lookup"><span data-stu-id="67716-135">(Azure Mobile Engagement can show you how many of your users are still using your app, but only hello platform specific store can tell you how many of your users uninstalled your app - for example, GooglePlay, iTunes, Windows Store, etc.).</span></span>
* <span data-ttu-id="67716-136">세션: hello 응용 프로그램 사용자가을 하나 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="67716-136">Sessions: One use of hello application by a user.</span></span> <span data-ttu-id="67716-137">세션 사용자가 수행한 작업의 hello 시퀀스에서 생성 됩니다 (활동은 일반적으로 연결된 toohello hello 응용 프로그램의 한 화면 사용 하지만 SDK가 hello 응용 프로그램에 통합 된 hello 방식으로 hello에 따라 달라질 수 있습니다).</span><span class="sxs-lookup"><span data-stu-id="67716-137">Sessions are generated from hello sequence of activities performed by users (an activity is usually associated toohello usage of one screen of hello application, but this can vary depending on hello way hello SDK has been integrated in hello application).</span></span> <span data-ttu-id="67716-138">사용자는 한 번에 하나의 활동만 수행할 수: hello 사용자 자신의 첫 번째 활동을 시작 하 고 그 그의 마지막 작업이 끝나면 중지 즉시 세션을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="67716-138">A user can only perform one activity at a time: a session starts as soon as hello user starts his first activity and stops when he finishes his last activity.</span></span> <span data-ttu-id="67716-139">사용자가 아무런 활동을 수행하지 않고 몇 초가 지나면 활동 시퀀스가 고유 세션 두 개로 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="67716-139">If a user stays more than a few seconds without performing any activity, then his sequence of activities is split into two distinct sessions.</span></span>
* <span data-ttu-id="67716-140">활동: hello 길이의 시간 사용자 및 응용 프로그램에서 각 화면 hello 이름은 각 화면에서 소비 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67716-140">Activities: hello names of each screen in your application and hello length of time users spend on each screen.</span></span> <span data-ttu-id="67716-141">활동은 toohello "앱 정보" 태그를 위해 자신의 앱에 대 한 설정에 해당 하는 사용자 지정 분석 옵션:</span><span class="sxs-lookup"><span data-stu-id="67716-141">Activities are a custom analytic option that will correspond toohello "app info" tags you have set up for your own app:</span></span>
* <span data-ttu-id="67716-142">사용자 경로: 사용자가 응용 프로그램 작업(화면)을 탐색하는 방식이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="67716-142">User Path:  Shows how your users navigate through your application's activities (screens).</span></span> <span data-ttu-id="67716-143">Hello 슬라이더 tooadjust hello 수준의 세부 정보를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67716-143">You can move hello slider tooadjust hello level of details.</span></span> <span data-ttu-id="67716-144">파란색 노드는 응용 프로그램의 활동을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="67716-144">Blue nodes represent your application's activities.</span></span> <span data-ttu-id="67716-145">크기는 비례에서 toohello 사용자가 보낸 합니다.</span><span class="sxs-lookup"><span data-stu-id="67716-145">Their size is proportional toohello time users spent in it.</span></span> <span data-ttu-id="67716-146">흰색 노드는 세션 시작 및 중지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="67716-146">White nodes represent session start and stop.</span></span> <span data-ttu-id="67716-147">빨간색 노드는 작동 중단을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="67716-147">Red nodes represent crashes.</span></span> <span data-ttu-id="67716-148">링크는 응용 프로그램 활동 간/활동과 작동 중단 간의 전환을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="67716-148">Links represent transitions between your application's activities (or between activities and crashes).</span></span> <span data-ttu-id="67716-149">데이터에 대 한 자세한 정보와 함께 도구 설명이 노드나 링크 toodisplay 클릭: hello 전환 수 및 hello 소스 활동 toohello 대상 활동에서 전환한 비율 hello는 특정 화면에서 소요 되는 hello 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="67716-149">Click on a node or a link toodisplay a tooltip with more information about your data: hello time spent in a particular screen, hello count of transitions, and hello percentage of transitions from hello source activity toohello destination activity.</span></span> <span data-ttu-id="67716-150">(한---60%---> B 의미 A가 hello 시간의 60% tooactivity B는 활동에 있는 사용자가 있습니다.) Tooclarify를 원하는 만큼 hello 그래프를 다시 구성할 수 있습니다. 위치가 변경 될 때마다 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67716-150">(A ---60% ---> B means that users being on activity A goes tooactivity B 60% of hello time.) You can reorganize hello graph as you want tooclarify it; its position is saved every time you make a change.</span></span> <span data-ttu-id="67716-151">표시 하거나 hello 충돌 toolighten hello 그래프를 숨길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67716-151">You can show or hide hello crashes toolighten hello graph.</span></span>
* <span data-ttu-id="67716-152">Hello 응용 프로그램의 사용자가 수행한 특정 작업을 이벤트: 합니다.</span><span class="sxs-lookup"><span data-stu-id="67716-152">Events: Specific actions taken by a user in hello application.</span></span> <span data-ttu-id="67716-153">이벤트의 hello 분포 hello 세션당 사용자 당 이벤트 수로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67716-153">hello distribution of events is shown as hello count of events per user per session.</span></span> <span data-ttu-id="67716-154">이벤트 알림 단추 또는 hello 수신 클릭 예를 들어 같은 즉각적인 작업을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="67716-154">An event represents an instant action, for example, a click on a button or hello reception of a notification.</span></span> <span data-ttu-id="67716-155">(이벤트의 hello 의미는 hello SDK가 hello 응용 프로그램에 통합 된 방식에 따라 다릅니다.) 이벤트는 세션이나 작업 중에 발생할 수도 있고 독립 실행형으로 발생할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67716-155">(hello meaning of events depends on how hello SDK has been integrated in hello application.) An event can occur during a session or a job or can be stand alone.</span></span>
* <span data-ttu-id="67716-156">작업:은 제외 하 고 유사한 tooevents hello 동작의 hello 길이에 집중합니다.</span><span class="sxs-lookup"><span data-stu-id="67716-156">Jobs: Similar tooevents except they focus on hello length of hello action.</span></span> <span data-ttu-id="67716-157">예를 들어 작업을 확인할 수 있습니다 시간 콘텐츠 tooload 또는 호출 tooweb 서비스에 대 한 기술 정보.</span><span class="sxs-lookup"><span data-stu-id="67716-157">For example, Jobs could tell you technical information about how long it takes content tooload or a call tooweb service.</span></span> <span data-ttu-id="67716-158">그 수 또한 양식에 사용자 toofill 데 걸리는 시간을 표시, 계정을 만들고 또는 제품을 구매 합니다.</span><span class="sxs-lookup"><span data-stu-id="67716-158">It could also show how long it takes a user toofill out a form, create an account, or make a purchase.</span></span> <span data-ttu-id="67716-159">작업을 작업의 hello 기간을 나타내는, 예제, 다운로드 작업 또는 hello hello 기간 시간 배너 hello 화면에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67716-159">A job represents hello duration of a task, for example, hello duration of a download task or hello time a banner is displayed on hello screen.</span></span> <span data-ttu-id="67716-160">(작업의 hello 의미는 hello SDK가 hello 응용 프로그램에 통합 된 방식에 따라 다릅니다.) 작업 (즉, 사용자 활동 없이)는 세션의 hello 범위 밖에 서 수행 하는 백그라운드 작업에 일반적으로 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67716-160">(hello meaning of Jobs depends on how hello SDK has been integrated in hello application.) Jobs are usually associated with background tasks that are performed outside of hello scope of a session (i.e., without any user activity).</span></span>
* <span data-ttu-id="67716-161">Technicals: 기술 hello 장치에 대 한 사용자의 정보 hello 추적할 수 있는, hello hello 사용자의 장치, 로캘, 통신 회사, 네트워크, 장치, 펌웨어 및 화면 크기 및 버전의 응용 프로그램 및 사용 되는 SDK 버전 hello hello와 같은 응용 프로그램에서 응용 프로그램의 합니다.</span><span class="sxs-lookup"><span data-stu-id="67716-161">Technicals: Technical information about hello devices of hello users of your app that you can track, such as hello Locale, Carrier, Network, Device, Firmware, and Screen size of hello users' devices, and hello Version of your App and hello SDK version used in your app.</span></span>
* <span data-ttu-id="67716-162">응용 프로그램 toocrash hello 발생 하지 않는 hello 응용 프로그램 내 기술 오류에 대 한 오류: 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="67716-162">Errors: Information about technical errors inside hello application that do not cause hello application toocrash.</span></span> <span data-ttu-id="67716-163">오류는 네트워크 문제, 잘못된 조작 등의 즉각적인 문제를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="67716-163">An error represents an instant issue, for example, a network failure or a bad manipulation.</span></span> <span data-ttu-id="67716-164">(이벤트의 hello 의미는 hello SDK가 hello 응용 프로그램에 통합 된 방식에 따라 다릅니다.) 오류는 세션이나 작업 중에 발생할 수도 있고 독립 실행형으로 발생할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67716-164">(hello meaning of events depends on how hello SDK has been integrated in hello application.) An error can occur during a session or a job or can be stand alone.</span></span>
* <span data-ttu-id="67716-165">응용 프로그램 toocrash는 오류에 대 한 충돌: 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="67716-165">Crashes: Information about errors that cause your application toocrash.</span></span> <span data-ttu-id="67716-166">충돌은 예기치 않은 상황이 여기서 hello 응용 프로그램의 예상 기능을 수행을 멈추고 중지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67716-166">A crash is an unexpected condition where hello application stops performing its expected functions and must be stopped.</span></span> <span data-ttu-id="67716-167">충돌은 일반적으로 hello 응용 프로그램의 tooa 버그 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="67716-167">A crash is usually due tooa bug in hello application.</span></span>

![Analytics2][11]

## <a name="accessing-hello-retention-overview"></a><span data-ttu-id="67716-169">Hello 고정 개요에 액세스</span><span class="sxs-lookup"><span data-stu-id="67716-169">Accessing hello Retention Overview</span></span>
![Analytics3][12]

<span data-ttu-id="67716-171">hello 고정 개요 여러 카드에 hello 가운데, 특정 보존 기간에 대 한 각 보여 주는 hello 개요에서 분리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67716-171">hello retention overview is broken down in hello middle into several cards, each showing hello overview for a certain retention period.</span></span> <span data-ttu-id="67716-172">hello 2 일의 보존 기간 hello 예제에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67716-172">hello 2-day retention period is seen in hello example.</span></span> <span data-ttu-id="67716-173">hello 다른 카드 표시 hello 4 및 7 일의 보존 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="67716-173">hello other cards show hello 4-day and 7-day retention periods.</span></span>

## <a name="understanding-hello-retention-overview-cards"></a><span data-ttu-id="67716-174">Hello 고정 개요 카드 이해</span><span class="sxs-lookup"><span data-stu-id="67716-174">Understanding hello Retention Overview cards</span></span>
![Analytics4][13]

### <a name="each-card-is-composed-of-3-main-parts"></a><span data-ttu-id="67716-176">각 카드는 3개의 주요 부분으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="67716-176">Each card is composed of 3 main parts:</span></span>
1. <span data-ttu-id="67716-177">1: hello 기간과 hello 코 호트 고려</span><span class="sxs-lookup"><span data-stu-id="67716-177">1: hello cohort and hello period considered</span></span>
2. <span data-ttu-id="67716-178">2-4: hello hello에 대 한 보존 현재 기간</span><span class="sxs-lookup"><span data-stu-id="67716-178">2-4: hello retention for hello current period</span></span>
3. <span data-ttu-id="67716-179">5: hello 기록의 스파크 라인</span><span class="sxs-lookup"><span data-stu-id="67716-179">5: A Sparkline of hello history</span></span>

### <a name="here-is-detailed-information-about-each-element"></a><span data-ttu-id="67716-180">아래에서 각 요소에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="67716-180">Here is detailed information about each element:</span></span>
1. <span data-ttu-id="67716-181">코 호트 및 기간:이 헤드라인 hello 유형의 코 호트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="67716-181">Cohort and period: This headline gives hello type of cohort.</span></span> <span data-ttu-id="67716-182">여기 "2 일 기간"을 살펴 사용자의 hello 동작 2 일 동안, hello 2 일로 블록 뒤의 연결 여부와 일, 2의 기간 동안 도착 하는 사용자가 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="67716-182">Here "2-day period" means that we will look at hello behavior of users over 2 days, Users that arrived over a period of 2 days, and whether they connect in hello following blocks of 2 days.</span></span> <span data-ttu-id="67716-183">위의 hello 예제 고려 hello 사이 사용자의 활동을 hello 21 및 11 월 22.</span><span class="sxs-lookup"><span data-stu-id="67716-183">hello example above considers hello activity of users between hello 21st and 22nd of November.</span></span>
2. <span data-ttu-id="67716-184">이 hello 보존 속도 19, 20 11 월에 도착 하는 hello 사용자에 대 한 hello 21-11 월 22를 통해 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="67716-184">This gives hello retention rate over hello 21 and 22 of November for hello users arriving in 19 and 20 of November.</span></span> <span data-ttu-id="67716-185">활성 사용자 1 사이의 21st 및 22nd hello, hello 3 사이 새 사용자를 통해 몇 여기 19th 및 20 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="67716-185">Here we had 1 active user between hello 21st and 22nd, over hello 3 that were new users between hello 19th and 20th.</span></span>
3. <span data-ttu-id="67716-186">위의 동일한 정보를 그래픽으로 나타낼이 시각적 표시기 제공 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="67716-186">This visual indicator gives hello same information as above represented graphically.</span></span> <span data-ttu-id="67716-187">(세 번째 hello의 hello 원이 hello 33% 정도 번호에서입니다.) 추가 정보를 제공 하는 hello 색: 녹색 hello 이전 계산에서 증가 하 고이 숫자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="67716-187">(hello third of hello circle is from hello 33% number.) hello color gives additional information: Green indicates this number is growing from hello previous calculation.</span></span> <span data-ttu-id="67716-188">노란색은 값이 이전과 동일하며 빨간색은 값이 감소했다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="67716-188">Yellow means stable, and red means decreasing.</span></span>
4. <span data-ttu-id="67716-189">이 hello 계산에 사용 되는 hello 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="67716-189">This indicates hello values used for hello calculation.</span></span>
5. <span data-ttu-id="67716-190">이 hello 보존 값의 hello 기록의 스파크 라인입니다.</span><span class="sxs-lookup"><span data-stu-id="67716-190">This is a Sparkline of hello history of hello retention values.</span></span> <span data-ttu-id="67716-191">값을 허용 하면 toosee hello에 hello toohave 지난 광범위 한 수준의 어떻게 발전 했습니다.</span><span class="sxs-lookup"><span data-stu-id="67716-191">It allows you toosee hello values in hello past toohave a broad view of how it evolved.</span></span>

## <a name="see-also"></a><span data-ttu-id="67716-192">참고 항목</span><span class="sxs-lookup"><span data-stu-id="67716-192">See also</span></span>
* <span data-ttu-id="67716-193">[개념][Link 6]</span><span class="sxs-lookup"><span data-stu-id="67716-193">[Concepts][Link 6]</span></span>
* <span data-ttu-id="67716-194">[문제 해결 가이드 서비스][Link 24]</span><span class="sxs-lookup"><span data-stu-id="67716-194">[Troubleshooting Guide Service][Link 24]</span></span>

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md
