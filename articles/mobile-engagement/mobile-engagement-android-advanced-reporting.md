---
title: "Azure Mobile Engagement Android SDK에 대한 고급 보고 옵션"
description: "고급 보고를 실행하여 Azure Mobile Engagement Android SDK에 대한 분석을 캡처하는 방법을 설명합니다"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7da7abd5-19d6-4892-94d8-818e5424b2cd
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 2a1445afa2c2fca1a31ad9c012b9c8a917ebf65c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-reporting-with-engagement-on-android"></a><span data-ttu-id="7a730-103">Android에서 Engagement를 사용한 고급 보고</span><span class="sxs-lookup"><span data-stu-id="7a730-103">Advanced Reporting with Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7a730-104">유니버설 Windows</span><span class="sxs-lookup"><span data-stu-id="7a730-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="7a730-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="7a730-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="7a730-106">iOS</span><span class="sxs-lookup"><span data-stu-id="7a730-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="7a730-107">Android</span><span class="sxs-lookup"><span data-stu-id="7a730-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="7a730-108">이 항목에서는 Android 응용 프로그램에서 추가 보고 시나리오를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7a730-108">This topic describes additional reporting scenarios in your Android application.</span></span> <span data-ttu-id="7a730-109">이러한 옵션은 [시작](mobile-engagement-android-get-started.md) 자습서에서 만든 앱에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a730-109">You can apply these options to the app created in the [Getting Started](mobile-engagement-android-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a730-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7a730-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

<span data-ttu-id="7a730-111">완료한 자습서는 의도적으로 직접적이고 간소화했으나 선택할 수 있는 고급 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a730-111">The tutorial you completed was deliberately direct and simple, but there are advanced options you can choose.</span></span>

## <a name="modifying-your-activity-classes"></a><span data-ttu-id="7a730-112">`Activity` 클래스 수정</span><span class="sxs-lookup"><span data-stu-id="7a730-112">Modifying your `Activity` classes</span></span>
<span data-ttu-id="7a730-113">[시작 자습서](mobile-engagement-android-get-started.md)에서는 `*Activity` 하위 클래스가 해당 `Engagement*Activity` 클래스에서 상속하는 설정만 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="7a730-113">In the [Getting Started tutorial](mobile-engagement-android-get-started.md), all you had to do was to make your `*Activity` subclasses inherit from the corresponding `Engagement*Activity` classes.</span></span> <span data-ttu-id="7a730-114">예를 들어 레거시 작업이 `ListActivity`를 확장하는 경우 `EngagementListActivity`를 확장하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a730-114">For example, if your legacy activity extended `ListActivity`, you would make it extend `EngagementListActivity`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a730-115">`EngagementListActivity` 또는 `EngagementExpandableListActivity`를 사용할 경우 `super.onCreate(...);`를 호출하기 전에 `requestWindowFeature(...);`를 호출해야 합니다. 그렇지 않으면 충돌이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="7a730-115">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call to `requestWindowFeature(...);` is made before the call to `super.onCreate(...);`, otherwise a crash occurs.</span></span>
> 
> 

<span data-ttu-id="7a730-116">이러한 클래스는 `src` 폴더에서 찾을 수 있으며 프로젝트에 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a730-116">You can find these classes in the `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="7a730-117">또한 클래스는 **JavaDoc**에도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a730-117">The classes are also in the **JavaDoc**.</span></span>

## <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="7a730-118">대체 방법: `startActivity()` 및 `endActivity()` 수동 호출</span><span class="sxs-lookup"><span data-stu-id="7a730-118">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="7a730-119">`Activity` 클래스를 오버로드할 수 없거나 오버로드하지 않으려는 경우 `EngagementAgent`의 메서드를 직접 호출하여 작업을 시작하고 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a730-119">If you cannot or do not want to overload your `Activity` classes, you can instead start and end your activities by calling the `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a730-120">Android SDK는 응용 프로그램이 닫힐 때에도 `endActivity()` 메서드를 호출하지 않습니다(Android에서 응용 프로그램은 닫히지 않음).</span><span class="sxs-lookup"><span data-stu-id="7a730-120">The Android SDK never calls the `endActivity()` method, even when the application is closed (on Android, applications are never closed).</span></span> <span data-ttu-id="7a730-121">따라서 *모든* 작업의 `onResume` 콜백에서는 `startActivity()` 메서드를, *모든* 작업의 `onPause()` 콜백에서는 `endActivity()` 메서드를 호출하는 것이 *상당히* 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7a730-121">Thus, it is *HIGHLY* recommended to call the `startActivity()` method in the `onResume` callback of *ALL* your activities, and the `endActivity()` method in the `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="7a730-122">이것이 세션이 손실되지 않도록 하는 유일한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="7a730-122">This is the only way to be sure that sessions are not leaked.</span></span> <span data-ttu-id="7a730-123">세션이 손실되는 경우 세션이 보류 중인 한 서비스가 연결된 상태를 유지하므로 Engagement 서비스의 Engagement 백 엔드에 대한 연결이 끊기지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a730-123">If a session is leaked, the Engagement service never disconnects from the Engagement backend (since the service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="7a730-124">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="7a730-124">Here is an example:</span></span>

    public class MyActivity extends Some3rdPartyActivity
    {
      @Override
      protected void onResume()
      {
        super.onResume();
        String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at the end.
        EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
      }

      @Override
      protected void onPause()
      {
        super.onPause();
        EngagementAgent.getInstance(this).endActivity();
      }
    }

<span data-ttu-id="7a730-125">이 예제는 `EngagementActivity` 클래스 및 해당 변형과 비슷합니다. 해당 소스 코드는 `src` 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a730-125">This example is similar to the `EngagementActivity` class and its variants, whose source code is provided in the `src` folder.</span></span>

## <a name="using-applicationoncreate"></a><span data-ttu-id="7a730-126">Application.onCreate() 사용</span><span class="sxs-lookup"><span data-stu-id="7a730-126">Using Application.onCreate()</span></span>
<span data-ttu-id="7a730-127">`Application.onCreate()` 및 기타 응용 프로그램 콜백에 배치하는 코드는 Engagement 서비스를 비롯하여 모든 응용 프로그램 프로세스에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a730-127">Any code you place in `Application.onCreate()` and in other application callbacks is run for all your application's processes, including the Engagement service.</span></span> <span data-ttu-id="7a730-128">이로 인해 Engagement 프로세스, 중복 브로드캐스트 수신기 또는 서비스에서의 불필요한 메모리 할당 및 스레드와 같은 원치 않는 부작용이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a730-128">It may have unwanted side effects, like unneeded memory allocations and threads in the Engagement's process, or duplicate broadcast receivers or services.</span></span>

<span data-ttu-id="7a730-129">`Application.onCreate()`를 재정의하는 경우 `Application.onCreate()` 함수의 시작 부분에 다음 코드 조각을 추가하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7a730-129">If you override `Application.onCreate()`, we recommend adding the following code snippet at the beginning of your `Application.onCreate()` function:</span></span>

     public void onCreate()
     {
       if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
         return;

       ... Your code...
     }

<span data-ttu-id="7a730-130">그리고 `Application.onTerminate()`, `Application.onLowMemory()` 및 `Application.onConfigurationChanged(...)`에 대해 동일한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a730-130">You can do the same thing for `Application.onTerminate()`, `Application.onLowMemory()`, and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="7a730-131">또한 `Application`을(를) 확장하는 대신 `EngagementApplication`을(를) 확장할 수도 있습니다. 콜백 `Application.onCreate()`은(는) 프로세스 검사를 수행하고 현재 프로세스가 Engagement 서비스를 호스트하는 프로세스가 아닌 경우에만 `Application.onApplicationProcessCreate()`을(를) 호출합니다. 그리고 다른 콜백에 대해서도 동일한 규칙이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a730-131">You can also extend `EngagementApplication` instead of extending `Application`: the callback `Application.onCreate()` does the process check and calls `Application.onApplicationProcessCreate()` only if the current process is not the one hosting the Engagement service, the same rules apply for the other callbacks.</span></span>

## <a name="tags-in-the-androidmanifestxml-file"></a><span data-ttu-id="7a730-132">AndroidManifest.xml 파일에 태그 지정</span><span class="sxs-lookup"><span data-stu-id="7a730-132">Tags in the AndroidManifest.xml file</span></span>
<span data-ttu-id="7a730-133">AndroidManifest.xml 파일의 서비스 태그에서 `android:label` 특성을 사용하면 휴대폰의 "서비스 실행 중" 화면에서 최종 사용자에게 표시될 Engagement 서비스의 이름을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a730-133">In the service tag in the AndroidManifest.xml file, the `android:label` attribute allows you to choose the name of the Engagement service as it appears to end users in the "Running services" screen of their phone.</span></span> <span data-ttu-id="7a730-134">이 특성을 `"<Your application name>Service"`로 설정하는 것이 좋습니다(예: `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="7a730-134">We recommended setting this attribute to `"<Your application name>Service"` (for example, `"AcmeFunGameService"`).</span></span>

<span data-ttu-id="7a730-135">또한 `android:process` 특성을 지정하면 Engagement 서비스가 자체 프로세스에서 실행됩니다. 그리고 응용 프로그램과 동일한 프로세스에서 Engagement를 실행하면 주/UI 스레드의 응답성이 떨어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a730-135">Specifying the `android:process` attribute ensures that the Engagement service runs in its own process (running Engagement in the same process as your application makes your main/UI thread potentially less responsive).</span></span>

## <a name="building-with-proguard"></a><span data-ttu-id="7a730-136">ProGuard를 사용하여 빌드</span><span class="sxs-lookup"><span data-stu-id="7a730-136">Building with ProGuard</span></span>
<span data-ttu-id="7a730-137">ProGuard로 응용 프로그램 패키지를 빌드하는 경우 일부 클래스를 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a730-137">If you build your application package with ProGuard, you need to keep some classes.</span></span> <span data-ttu-id="7a730-138">다음 구성 코드 조각을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a730-138">You can use the following configuration snippet:</span></span>

    -keep public class * extends android.os.IInterface
    -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
    <methods>;
     }
