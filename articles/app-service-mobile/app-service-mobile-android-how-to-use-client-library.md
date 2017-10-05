---
title: "Android용 Azure Mobile Apps SDK를 사용하는 방법 | Microsoft Docs"
description: "Android용 Azure Mobile Apps SDK를 사용하는 방법"
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
ms.assetid: 5352d1e4-7685-4a11-aaf4-10bd2fa9f9fc
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: glenga
ms.openlocfilehash: 4b15d024ca6d5bbafe83d321a64021aecd78c4a8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-azure-mobile-apps-sdk-for-android"></a><span data-ttu-id="334e5-103">Android용 Azure Mobile Apps SDK를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="334e5-103">How to use the Azure Mobile Apps SDK for Android</span></span>

<span data-ttu-id="334e5-104">이 가이드에서는 모바일 앱용 Android 클라이언트 SDK를 사용하여 다음과 같은 일반적인 시나리오를 구현하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-104">This guide shows you how to use the Android client SDK for Mobile Apps to implement common scenarios, such as:</span></span>

* <span data-ttu-id="334e5-105">데이터 쿼리(삽입, 업데이트 및 삭제).</span><span class="sxs-lookup"><span data-stu-id="334e5-105">Querying for data (inserting, updating, and deleting).</span></span>
* <span data-ttu-id="334e5-106">인증.</span><span class="sxs-lookup"><span data-stu-id="334e5-106">Authentication.</span></span>
* <span data-ttu-id="334e5-107">오류 처리.</span><span class="sxs-lookup"><span data-stu-id="334e5-107">Handling errors.</span></span>
* <span data-ttu-id="334e5-108">클라이언트 사용자 지정.</span><span class="sxs-lookup"><span data-stu-id="334e5-108">Customizing the client.</span></span>

<span data-ttu-id="334e5-109">이 가이드는 클라이언트 쪽 Android SDK에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-109">This guide focuses on the client-side Android SDK.</span></span>  <span data-ttu-id="334e5-110">Mobile Apps용 서버 쪽 SDK에 대해 자세히 알아보려면 [.NET 백 엔드 SDK로 작업][10] 또는 [Node.js 백 엔드 SDK를 사용하는 방법][11]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="334e5-110">To learn more about the server-side SDKs for Mobile Apps, see [Work with .NET backend SDK][10] or [How to use the Node.js backend SDK][11].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="334e5-111">참조 설명서</span><span class="sxs-lookup"><span data-stu-id="334e5-111">Reference Documentation</span></span>

<span data-ttu-id="334e5-112">Android 클라이언트 라이브러리용 [Javadocs API 참조][12]는 GitHub에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-112">You can find the [Javadocs API reference][12] for the Android client library on GitHub.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="334e5-113">지원되는 플랫폼</span><span class="sxs-lookup"><span data-stu-id="334e5-113">Supported Platforms</span></span>

<span data-ttu-id="334e5-114">Android용 Azure Mobile Apps SDK는 휴대폰 및 태블릿 폼 팩터용 API 레벨 19 ~24(KitKat ~ Nougat)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-114">The Azure Mobile Apps SDK for Android supports API levels 19 through 24 (KitKat through Nougat) for phone and tablet form factors.</span></span>  <span data-ttu-id="334e5-115">특히 인증은 일반적인 웹 프레임워크 방식을 활용하여 자격 증명을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-115">Authentication, in particular, utilizes a common web framework approach to gather credentials.</span></span>  <span data-ttu-id="334e5-116">서버 흐름 인증은 시계와 같은 소형 폼 팩터 장치에서는 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-116">Server-flow authentication does not work with small form factor devices such as watches.</span></span>

## <a name="setup-and-prerequisites"></a><span data-ttu-id="334e5-117">설정 및 필수 조건</span><span class="sxs-lookup"><span data-stu-id="334e5-117">Setup and Prerequisites</span></span>

<span data-ttu-id="334e5-118">[Mobile Apps 빠른 시작](app-service-mobile-android-get-started.md) 자습서를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-118">Complete the [Mobile Apps quickstart](app-service-mobile-android-get-started.md) tutorial.</span></span>  <span data-ttu-id="334e5-119">자습서를 통해 Azure Mobile Apps를 개발하기 위한 모든 필수 구성 요소를 충족할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-119">This task ensures all pre-requisites for developing Azure Mobile Apps have been met.</span></span>  <span data-ttu-id="334e5-120">또한 빠른 시작 자습서를 참조하여 계정을 구성하고 첫 번째 모바일 앱 백 엔드를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-120">The Quickstart also helps you configure your account and create your first Mobile App backend.</span></span>

<span data-ttu-id="334e5-121">빠른 시작 자습서를 완료하지 않으려는 경우에는 다음 작업을 완료하세요.</span><span class="sxs-lookup"><span data-stu-id="334e5-121">If you decide not to complete the Quickstart tutorial, complete the following tasks:</span></span>

* <span data-ttu-id="334e5-122">Android 앱과 함께 사용할 [모바일 앱 백 엔드를 만듭니다][13].</span><span class="sxs-lookup"><span data-stu-id="334e5-122">[create a Mobile App backend][13] to use with your Android app.</span></span>
* <span data-ttu-id="334e5-123">Android Studio에서 [Gradle 빌드 파일을 업데이트](#gradle-build)합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-123">In Android Studio, [update the Gradle build files](#gradle-build).</span></span>
* <span data-ttu-id="334e5-124">[인터넷 권한을 사용합니다](#enable-internet).</span><span class="sxs-lookup"><span data-stu-id="334e5-124">[Enable internet permission](#enable-internet).</span></span>

### <span data-ttu-id="334e5-125"><a name="gradle-build"></a>Gradle 빌드 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="334e5-125"><a name="gradle-build"></a>Update the Gradle build file</span></span>

<span data-ttu-id="334e5-126">**build.gradle** 파일을 모두 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-126">Change both **build.gradle** files:</span></span>

1. <span data-ttu-id="334e5-127">*buildscript* 태그 내의 *프로젝트* 수준 **build.gradle** 파일에 이 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-127">Add this code to the *Project* level **build.gradle** file inside the *buildscript* tag:</span></span>

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. <span data-ttu-id="334e5-128">*dependencies* 태그 내의 *모듈 앱* 수준 **build.gradle** 파일에 이 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-128">Add this code to the *Module app* level **build.gradle** file inside the *dependencies* tag:</span></span>

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    <span data-ttu-id="334e5-129">현재 최신 버전은 3.3.0입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-129">Currently the latest version is 3.3.0.</span></span> <span data-ttu-id="334e5-130">지원되는 버전은 [bintray][14]에 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-130">The supported versions are listed [on bintray][14].</span></span>

### <span data-ttu-id="334e5-131"><a name="enable-internet"></a>인터넷 권한 사용</span><span class="sxs-lookup"><span data-stu-id="334e5-131"><a name="enable-internet"></a>Enable internet permission</span></span>

<span data-ttu-id="334e5-132">Azure에 액세스하려면 앱은 인터넷 사용 권한을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-132">To access Azure, your app must have the INTERNET permission enabled.</span></span> <span data-ttu-id="334e5-133">아직 사용하지 않는 경우 코드의 다음 줄을 **AndroidManifest.xml** 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-133">If it's not already enabled, add the following line of code to your **AndroidManifest.xml** file:</span></span>

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a><span data-ttu-id="334e5-134">클라이언트 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="334e5-134">Create a Client Connection</span></span>

<span data-ttu-id="334e5-135">Azure Mobile Apps는 모바일 응용 프로그램에 네 가지 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-135">Azure Mobile Apps provides four functions to your mobile application:</span></span>

* <span data-ttu-id="334e5-136">Azure Mobile Apps Service를 통한 데이터 액세스 및 오프라인 동기화.</span><span class="sxs-lookup"><span data-stu-id="334e5-136">Data Access and Offline Synchronization with an Azure Mobile Apps Service.</span></span>
* <span data-ttu-id="334e5-137">Azure Mobile Apps 서버 SDK로 작성된 사용자 지정 API 호출.</span><span class="sxs-lookup"><span data-stu-id="334e5-137">Call Custom APIs written with the Azure Mobile Apps Server SDK.</span></span>
* <span data-ttu-id="334e5-138">Azure App Service 인증 및 권한 부여를 통한 인증.</span><span class="sxs-lookup"><span data-stu-id="334e5-138">Authentication with Azure App Service Authentication and Authorization.</span></span>
* <span data-ttu-id="334e5-139">Notification Hubs를 통한 푸시 알림 등록.</span><span class="sxs-lookup"><span data-stu-id="334e5-139">Push Notification Registration with Notification Hubs.</span></span>

<span data-ttu-id="334e5-140">이러한 각각의 함수는 먼저 `MobileServiceClient` 개체를 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-140">Each of these functions first requires that you create a `MobileServiceClient` object.</span></span>  <span data-ttu-id="334e5-141">모바일 클라이언트 내에 하나의 `MobileServiceClient` 개체만 만들어야 합니다(즉 Singleton 패턴이어야 합니다).</span><span class="sxs-lookup"><span data-stu-id="334e5-141">Only one `MobileServiceClient` object should be created within your mobile client (that is, it should be a Singleton pattern).</span></span>  <span data-ttu-id="334e5-142">`MobileServiceClient` 개체를 만들려면:</span><span class="sxs-lookup"><span data-stu-id="334e5-142">To create a `MobileServiceClient` object:</span></span>

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with the Site URL
    this);                  // Your application Context
```

<span data-ttu-id="334e5-143">`<MobileAppUrl>`은 모바일 백 엔드를 가리키는 문자열 또는 URL 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-143">The `<MobileAppUrl>` is either a string or a URL object that points to your mobile backend.</span></span>  <span data-ttu-id="334e5-144">Azure App Service를 사용하여 모바일 백 엔드를 호스트하는 경우 보안 `https://` 버전의 URL을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-144">If you are using Azure App Service to host your mobile backend, then ensure you use the secure `https://` version of the URL.</span></span>

<span data-ttu-id="334e5-145">클라이언트는 활동 또는 컨텍스트(예제의 `this` 매개 변수)에 대한 액세스도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-145">The client also requires access to the Activity or Context - the `this` parameter in the example.</span></span>  <span data-ttu-id="334e5-146">MobileServiceClient 생성은 `AndroidManifest.xml` 파일에 언급된 활동의 `onCreate()` 메서드 내에서 수행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-146">The MobileServiceClient construction should happen within the `onCreate()` method of the Activity referenced in the `AndroidManifest.xml` file.</span></span>

<span data-ttu-id="334e5-147">가장 좋은 방법은 서버 통신을 자체(singleton 패턴) 클래스로 추상화하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-147">As a best practice, you should abstract server communication into its own (singleton-pattern) class.</span></span>  <span data-ttu-id="334e5-148">이런 경우 서비스를 적절히 구성하려면 활동을 생성자 내에서 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-148">In this case, you should pass the Activity within the constructor to appropriately configure the service.</span></span>  <span data-ttu-id="334e5-149">예:</span><span class="sxs-lookup"><span data-stu-id="334e5-149">For example:</span></span>

```java
package com.example.appname.services;

import android.content.Context;
import com.microsoft.windowsazure.mobileservices.*;

public AzureServiceAdapter {
    private String mMobileBackendUrl = "https://myappname.azurewebsites.net";
    private Context mContext;
    private MobileServiceClient mClient;
    private static AzureServiceAdapter mInstance = null;

    private AzureServiceAdapter(Context context) {
        mContext = context;
        mClient = new MobileServiceClient(mMobileBackendUrl, mContext);
    }

    public static void Initialize(Context context) {
        if (mInstance == null) {
            mInstance = new AzureServiceAdapter(context);
        } else {
            throw new IllegalStateException("AzureServiceAdapter is already initialized");
        }
    }

    public static AzureServiceAdapter getInstance() {
        if (mInstance == null) {
            throw new IllegalStateException("AzureServiceAdapter is not initialized");
        }
        return mInstance;
    }

    public MobileServiceClient getClient() {
        return mClient;
    }

    // Place any public methods that operate on mClient here.
}
```

<span data-ttu-id="334e5-150">이제 기본 활동의 `onCreate()` 메서드에서 `AzureServiceAdapter.Initialize(this);`를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-150">You can now call `AzureServiceAdapter.Initialize(this);` in the `onCreate()` method of your main activity.</span></span>  <span data-ttu-id="334e5-151">클라이언트에 대한 액세스가 필요한 다른 모든 메서드는 `AzureServiceAdapter.getInstance();`를 사용하여 서비스 어댑터에 대한 참조를 확보합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-151">Any other methods needing access to the client use `AzureServiceAdapter.getInstance();` to obtain a reference to the service adapter.</span></span>

## <a name="data-operations"></a><span data-ttu-id="334e5-152">데이터 작업</span><span class="sxs-lookup"><span data-stu-id="334e5-152">Data Operations</span></span>

<span data-ttu-id="334e5-153">Azure Mobile Apps SDK의 핵심은 Mobile App 백 엔드의 SQL Azure 내에 저장된 데이터에 대한 액세스를 제공하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-153">The core of the Azure Mobile Apps SDK is to provide access to data stored within SQL Azure on the Mobile App backend.</span></span>  <span data-ttu-id="334e5-154">이러한 데이터는 강력한 형식의 클래스(권장됨) 또는 형식화되지 않은 쿼리(권장하지 않음)를 사용하여 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-154">You can access this data using strongly typed classes (preferred) or untyped queries (not recommended).</span></span>  <span data-ttu-id="334e5-155">이 섹션의 대부분은 강력한 형식의 클래스 사용을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-155">The bulk of this section deals with using strongly typed classes.</span></span>

### <a name="define-client-data-classes"></a><span data-ttu-id="334e5-156">클라이언트 데이터 클래스 정의</span><span class="sxs-lookup"><span data-stu-id="334e5-156">Define client data classes</span></span>

<span data-ttu-id="334e5-157">SQL Azure 테이블의 데이터에 액세스하려면 모바일 앱 백 엔드에 있는 테이블에 해당하는 클라이언트 데이터 클래스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-157">To access data from SQL Azure tables, define client data classes that correspond to the tables in the Mobile App backend.</span></span> <span data-ttu-id="334e5-158">이 항목의 예에서는 이름이 **MyDataTable**이고 다음 열이 포함된 테이블을 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-158">Examples in this topic assume a table named **MyDataTable**, which has the following columns:</span></span>

* <span data-ttu-id="334e5-159">id</span><span class="sxs-lookup"><span data-stu-id="334e5-159">id</span></span>
* <span data-ttu-id="334e5-160">text</span><span class="sxs-lookup"><span data-stu-id="334e5-160">text</span></span>
* <span data-ttu-id="334e5-161">complete</span><span class="sxs-lookup"><span data-stu-id="334e5-161">complete</span></span>

<span data-ttu-id="334e5-162">해당하는 형식의 클라이언트 쪽 개체는 **MyDataTable.java**라는 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-162">The corresponding typed client-side object resides in a file called **MyDataTable.java**:</span></span>

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

<span data-ttu-id="334e5-163">추가하는 각 필드에 getter 및 setter 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-163">Add getter and setter methods for each field that you add.</span></span>  <span data-ttu-id="334e5-164">SQL Azure 테이블이 더 많은 열을 포함하는 경우 이 클래스에 해당하는 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-164">If your SQL Azure table contains more columns, you would add the corresponding fields to this class.</span></span>  <span data-ttu-id="334e5-165">예를 들어 DTO(데이터 전송 개체)에 정수 우선 순위 열이 있다면 getter 및 setter 메서드와 함께 이 필드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-165">For example, if the DTO (data transfer object) had an integer Priority column, then you might add this field, along with its getter and setter methods:</span></span>

```java
private Integer priority;

/**
* Returns the item priority
*/
public Integer getPriority() {
    return mPriority;
}

/**
* Sets the item priority
*
* @param priority
*            priority to set
*/
public final void setPriority(Integer priority) {
    mPriority = priority;
}
```

<span data-ttu-id="334e5-166">Mobile Apps 백 엔드에 추가 테이블을 작성하는 방법을 알아보려면 [방법: 테이블 컨트롤러 정의][15](.NET 백 엔드) 또는 [동적 스키마를 사용하여 테이블 정의][16](Node.js 백 엔드)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="334e5-166">To learn how to create additional tables in your Mobile Apps backend, see [How to: Define a table controller][15] (.NET backend) or [Define Tables using a Dynamic Schema][16] (Node.js backend).</span></span>

<span data-ttu-id="334e5-167">Azure Mobile Apps 백 엔드 테이블은 5개의 특수 필드를 정의하며 이 중 4개는 클라이언트에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-167">An Azure Mobile Apps backend table defines five special fields, four of which are available to clients:</span></span>

* <span data-ttu-id="334e5-168">`String id`: 레코드의 전역 고유 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-168">`String id`: The globally unique ID for the record.</span></span>  <span data-ttu-id="334e5-169">가장 좋은 방법은 ID를 [UUID][17] 개체의 문자열 표현으로 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-169">As a best practice, make the id the String representation of a [UUID][17] object.</span></span>
* <span data-ttu-id="334e5-170">`DateTimeOffset updatedAt`: 마지막 업데이트 날짜/시간입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-170">`DateTimeOffset updatedAt`: The date/time of the last update.</span></span>  <span data-ttu-id="334e5-171">updatedAt 필드는 서버에 의해 설정되며 클라이언트 코드로 설정하지 말아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-171">The updatedAt field is set by the server and should never be set by your client code.</span></span>
* <span data-ttu-id="334e5-172">`DateTimeOffset createdAt`: 개체가 만들어진 날짜/시간입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-172">`DateTimeOffset createdAt`: The date/time that the object was created.</span></span>  <span data-ttu-id="334e5-173">createdAt 필드는 서버에 의해 설정되며 클라이언트 코드로 설정하지 말아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-173">The createdAt field is set by the server and should never be set by your client code.</span></span>
* <span data-ttu-id="334e5-174">`byte[] version`: 일반적으로 문자열로 표시되며 버전도 서버에 의해 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-174">`byte[] version`: Normally represented as a string, the version is also set by the server.</span></span>
* <span data-ttu-id="334e5-175">`boolean deleted`: 레코드가 삭제되었지만 아직 제거되지 않았음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-175">`boolean deleted`: Indicates that the record has been deleted but not purged yet.</span></span>  <span data-ttu-id="334e5-176">`deleted`를 클래스에서 속성으로 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="334e5-176">Do not use `deleted` as a property in your class.</span></span>

<span data-ttu-id="334e5-177">`id` 필드는 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-177">The `id` field is required.</span></span>  <span data-ttu-id="334e5-178">`updatedAt` 필드 및 `version` 필드는 오프라인 동기화에(각각 증분 동기화 및 충돌 해결을 위해) 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-178">The `updatedAt` field and `version` field are used for offline synchronization (for incremental sync and conflict resolution respectively).</span></span>  <span data-ttu-id="334e5-179">`createdAt` 필드는 참조 필드이며 클라이언트에서 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-179">The `createdAt` field is a reference field and is not used by the client.</span></span>  <span data-ttu-id="334e5-180">이름은 속성의 "across-the-wire" 이름이며 조정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-180">The names are "across-the-wire" names of the properties and are not adjustable.</span></span>  <span data-ttu-id="334e5-181">하지만 [gson][3] 라이브러리를 사용하여 개체와 "across-the-wire" 이름 사이에 매핑을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-181">However, you can create a mapping between your object and the "across-the-wire" names using the [gson][3] library.</span></span>  <span data-ttu-id="334e5-182">예:</span><span class="sxs-lookup"><span data-stu-id="334e5-182">For example:</span></span>

```java
package com.example.zumoappname;

import com.microsoft.windowsazure.mobileservices.table.DateTimeOffset;

public class ToDoItem
{
    @com.google.gson.annotations.SerializedName("id")
    private String mId;
    public String getId() { return mId; }
    public final void setId(String id) { mId = id; }

    @com.google.gson.annotations.SerializedName("complete")
    private boolean mComplete;
    public boolean isComplete() { return mComplete; }
    public void setComplete(boolean complete) { mComplete = complete; }

    @com.google.gson.annotations.SerializedName("text")
    private String mText;
    public String getText() { return mText; }
    public final void setText(String text) { mText = text; }

    @com.google.gson.annotations.SerializedName("createdAt")
    private DateTimeOffset mCreatedAt;
    public DateTimeOffset getUpdatedAt() { return mCreatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset createdAt) { mCreatedAt = createdAt; }

    @com.google.gson.annotations.SerializedName("updatedAt")
    private DateTimeOffset mUpdatedAt;
    public DateTimeOffset getUpdatedAt() { return mUpdatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset updatedAt) { mUpdatedAt = updatedAt; }

    @com.google.gson.annotations.SerializedName("version")
    private String mVersion;
    public String getText() { return mVersion; }
    public final void setText(String version) { mVersion = version; }

    public ToDoItem() { }

    public ToDoItem(String id, String text) {
        this.setId(id);
        this.setText(text);
    }

    @Override
    public boolean equals(Object o) {
        return o instanceof ToDoItem && ((ToDoItem) o).mId == mId;
    }

    @Override
    public String toString() {
        return getText();
    }
}
```

### <a name="create-a-table-reference"></a><span data-ttu-id="334e5-183">테이블 참조 만들기</span><span class="sxs-lookup"><span data-stu-id="334e5-183">Create a Table Reference</span></span>

<span data-ttu-id="334e5-184">테이블에 액세스하려면 우선 [MobileServiceClient][9]에서 **getTable** 메서드를 호출하여 [MobileServiceTable][8] 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-184">To access a table, first create a [MobileServiceTable][8] object by calling the **getTable** method on the [MobileServiceClient][9].</span></span>  <span data-ttu-id="334e5-185">이 메서드에는 두 가지 오버로드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-185">This method has two overloads:</span></span>

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

<span data-ttu-id="334e5-186">다음 코드에서 **mClient** 는 MobileServiceClient 개체에 대한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-186">In the following code, **mClient** is a reference to your MobileServiceClient object.</span></span>  <span data-ttu-id="334e5-187">첫 번째 오버로드는 클래스 이름과 테이블 이름이 같을 때 사용하며 빠른 시작에서 사용되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-187">The first overload is used where the class name and the table name are the same, and is the one used in the Quickstart:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

<span data-ttu-id="334e5-188">두 번째 오버로드는 테이블 이름이 형식 이름과 다를 때 사용하고 첫 번째 매개 변수는 테이블 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-188">The second overload is used when the table name is different from the class name: the first parameter is the table name.</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <span data-ttu-id="334e5-189"><a name="query"></a> 엔드 테이블 쿼리</span><span class="sxs-lookup"><span data-stu-id="334e5-189"><a name="query"></a>Query a Backend Table</span></span>

<span data-ttu-id="334e5-190">먼저 테이블 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-190">First, obtain a table reference.</span></span>  <span data-ttu-id="334e5-191">그런 다음 테이블 참조에 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-191">Then execute a query on the table reference.</span></span>  <span data-ttu-id="334e5-192">쿼리는 다음의 조합입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-192">A query is any combination of:</span></span>

* <span data-ttu-id="334e5-193">`.where()` [필터 절](#filtering).</span><span class="sxs-lookup"><span data-stu-id="334e5-193">A `.where()` [filter clause](#filtering).</span></span>
* <span data-ttu-id="334e5-194">`.orderBy()` [ordering 절](#sorting).</span><span class="sxs-lookup"><span data-stu-id="334e5-194">An `.orderBy()` [ordering clause](#sorting).</span></span>
* <span data-ttu-id="334e5-195">`.select()` [필드 선택 절](#selection).</span><span class="sxs-lookup"><span data-stu-id="334e5-195">A `.select()` [field selection clause](#selection).</span></span>
* <span data-ttu-id="334e5-196">[페이징 결과](#paging)에 대한 `.skip()` 및 `.top()`.</span><span class="sxs-lookup"><span data-stu-id="334e5-196">A `.skip()` and `.top()` for [paged results](#paging).</span></span>

<span data-ttu-id="334e5-197">절은 선행 순으로 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-197">The clauses must be presented in the preceding order.</span></span>

### <span data-ttu-id="334e5-198"><a name="filter"></a> 결과 필터링</span><span class="sxs-lookup"><span data-stu-id="334e5-198"><a name="filter"></a> Filtering Results</span></span>

<span data-ttu-id="334e5-199">쿼리의 일반적인 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-199">The general form of a query is:</span></span>

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts the async into a sync result
```

<span data-ttu-id="334e5-200">앞의 예제는 모든 결과(서버가 설정한 최대 페이지 크기까지)를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-200">The preceding example returns all results (up to the maximum page size set by the server).</span></span>  <span data-ttu-id="334e5-201">`.execute()` 메서드는 백 엔드에서 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-201">The `.execute()` method executes the query on the backend.</span></span>  <span data-ttu-id="334e5-202">쿼리는 Mobile Apps 백 엔드로 전송되기 전에 [OData v3][19] 쿼리로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-202">The query is converted to an [OData v3][19] query before transmission to the Mobile Apps backend.</span></span>  <span data-ttu-id="334e5-203">수신되면 Mobile Apps 백 엔드는 SQL Azure 인스턴스에서 쿼리를 실행하기 전에 SQL 문으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-203">On receipt, the Mobile Apps backend converts the query into an SQL statement before executing it on the SQL Azure instance.</span></span>  <span data-ttu-id="334e5-204">네트워크 작업에 시간이 걸리므로 `.execute()` 메서드는 [`ListenableFuture<E>`][18]를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-204">Since network activity takes some time, The `.execute()` method returns a [`ListenableFuture<E>`][18].</span></span>

### <span data-ttu-id="334e5-205"><a name="filtering"></a>반환된 데이터 필터링</span><span class="sxs-lookup"><span data-stu-id="334e5-205"><a name="filtering"></a>Filter returned data</span></span>

<span data-ttu-id="334e5-206">다음 쿼리 실행은 **완료**가 **false**와 같은 **ToDoItem** 테이블에서 모든 항목을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-206">The following query execution returns all items from the **ToDoItem** table where **complete** equals **false**.</span></span>

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

<span data-ttu-id="334e5-207">**mToDoTable**은 이전에 만든 모바일 서비스 테이블에 대한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-207">**mToDoTable** is the reference to the mobile service table that we created previously.</span></span>

<span data-ttu-id="334e5-208">테이블 참조에 대한 **where** 메서드 호출을 사용하여 필터를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-208">Define a filter using the **where** method call on the table reference.</span></span> <span data-ttu-id="334e5-209">**where** 메서드 뒤에는 **field** 메서드를 사용하고 그 뒤에 논리 조건자를 지정하는 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-209">The **where** method is followed by a **field** method followed by a method that specifies the logical predicate.</span></span> <span data-ttu-id="334e5-210">가능한 조건자 메서드에는 **eq**(같음), **ne**(같지 않음), **gt**(보다 큼), **ge**(보다 크거나 같음), **lt**(보다 작음), **le**(작거나 같음)가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-210">Possible predicate methods include **eq** (equals), **ne** (not equal), **gt** (greater than), **ge** (greater than or equal to), **lt** (less than), **le** (less than or equal to).</span></span> <span data-ttu-id="334e5-211">이러한 메서드를 사용하면 숫자 및 문자열 필드를 특정 값과 비교할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-211">These methods let you compare number and string fields to specific values.</span></span>

<span data-ttu-id="334e5-212">날짜를 기준으로 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-212">You can filter on dates.</span></span> <span data-ttu-id="334e5-213">다음 메서드를 사용하면 전체 날짜 필드 또는 날짜의 부분을 비교할 수 있습니다. **년**, **월**, **일**, **시간**, **분** 및 **초**.</span><span class="sxs-lookup"><span data-stu-id="334e5-213">The following methods let you compare the entire date field or parts of the date: **year**, **month**, **day**, **hour**, **minute**, and **second**.</span></span> <span data-ttu-id="334e5-214">다음 예제는 *기한*이 2013과 같은 항목에 해당하는 필터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-214">The following example adds a filter for items whose *due date* equals 2013.</span></span>

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

<span data-ttu-id="334e5-215">**startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **replace**, **toLower**, **toUpper**, **trim**, **length**와 같은 메서드는 문자열 필드에 복합 필터를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-215">The following methods support complex filters on string fields: **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **replace**, **toLower**, **toUpper**, **trim**, and **length**.</span></span> <span data-ttu-id="334e5-216">다음 예제는 *텍스트* 열이 "PRI0"으로 시작되는 테이블 행을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-216">The following example filters for table rows where the *text* column starts with "PRI0."</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="334e5-217">연산자 메서드, **add**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling** 및 **round**는 숫자 필드에 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-217">The following operator methods are supported on number fields: **add**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, and **round**.</span></span> <span data-ttu-id="334e5-218">다음 예제는 **기간**이 짝수인 테이블 행을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-218">The following example filters for table rows where the **duration** is an even number.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

<span data-ttu-id="334e5-219">조건자를 **and**, **or**, **not** 등의 논리 메서드와 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-219">You can combine predicates with these logical methods: **and**, **or** and **not**.</span></span> <span data-ttu-id="334e5-220">다음 예제는 앞의 예 중 두 가지를 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-220">The following example combines two of the preceding examples.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="334e5-221">그룹 및 중첩 논리 연산자:</span><span class="sxs-lookup"><span data-stu-id="334e5-221">Group and nest logical operators:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013)
    .and(
        startsWith("text", "PRI0")
        .or()
        .field("duration").gt(10)
    )
    .execute().get();
```

<span data-ttu-id="334e5-222">필터링에 대한 자세한 내용과 예를 보려면 [Android 클라이언트 쿼리 모델의 다양한 기능 알아보기][20]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="334e5-222">For more detailed discussion and examples of filtering, see [Exploring the richness of the Android client query model][20].</span></span>

### <span data-ttu-id="334e5-223"><a name="sorting"></a>반환된 데이터 정렬</span><span class="sxs-lookup"><span data-stu-id="334e5-223"><a name="sorting"></a>Sort returned data</span></span>

<span data-ttu-id="334e5-224">다음 코드는 **ToDoItems** 테이블에서 *텍스트* 필드를 기준으로 오름차순 정렬된 모든 항목을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-224">The following code returns all items from a table of **ToDoItems** sorted ascending by the *text* field.</span></span> <span data-ttu-id="334e5-225">*mToDoTable* 은 이전에 만든 백 엔드 테이블에 대한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-225">*mToDoTable* is the reference to the backend table that you created previously:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

<span data-ttu-id="334e5-226">**orderBy** 메서드의 첫 번째 매개 변수는 정렬 기준이 되는 필드의 이름과 동일한 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-226">The first parameter of the **orderBy** method is a string equal to the name of the field on which to sort.</span></span> <span data-ttu-id="334e5-227">두 번째 매개 변수는 **QueryOrder** 열거형을 사용하여 오름차순이나 내림차순으로 정렬할지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-227">The second parameter uses the **QueryOrder** enumeration to specify whether to sort ascending or descending.</span></span>  <span data-ttu-id="334e5-228">***where*** 메서드를 사용하여 필터링하려는 경우 ***orderBy*** 메서드 이전에 ***where*** 메서드를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-228">If you are filtering using the ***where*** method, the ***where*** method must be invoked before the ***orderBy*** method.</span></span>

### <span data-ttu-id="334e5-229"><a name="selection"></a>특정 열 선택</span><span class="sxs-lookup"><span data-stu-id="334e5-229"><a name="selection"></a>Select specific columns</span></span>

<span data-ttu-id="334e5-230">다음 코드는 **ToDoItems** 테이블에서 모든 항목을 반환하지만 **완료** 및 **텍스트** 필드만 표시하는 방법을 보여 줍니다. </span><span class="sxs-lookup"><span data-stu-id="334e5-230">The following code illustrates how to return all items from a table of **ToDoItems**, but only displays the **complete** and **text** fields.</span></span> <span data-ttu-id="334e5-231">**mToDoTable** 은 이전에 만든 백 엔드 테이블에 대한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-231">**mToDoTable** is the reference to the backend table that we created previously.</span></span>

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

<span data-ttu-id="334e5-232">select 함수의 매개 변수는 반환하려는 테이블 열의 문자열 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-232">The parameters to the select function are the string names of the table's columns that you want to return.</span></span>  <span data-ttu-id="334e5-233">**select** 메서드는 **where**나 **orderBy** 같은 메서드의 뒤에 나와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-233">The **select** method needs to follow methods like **where** and **orderBy**.</span></span> <span data-ttu-id="334e5-234">그 뒤에 **skip** 및 **top**등의 메서드를 페이징하여 나올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-234">It can be followed by paging methods like **skip** and **top**.</span></span>

### <span data-ttu-id="334e5-235"><a name="paging"></a>페이지에 데이터 반환</span><span class="sxs-lookup"><span data-stu-id="334e5-235"><a name="paging"></a>Return data in pages</span></span>

<span data-ttu-id="334e5-236">데이터는 **항상** 페이지에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-236">Data is **ALWAYS** returned in pages.</span></span>  <span data-ttu-id="334e5-237">반환되는 레코드의 최대 수는 서버에 의해 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-237">The maximum number of records returned is set by the server.</span></span>  <span data-ttu-id="334e5-238">클라이언트가 더 많은 레코드를 요청하면 서버는 최대 레코드 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-238">If the client requests more records, then the server returns the maximum number of records.</span></span>  <span data-ttu-id="334e5-239">기본적으로 서버의 최대 페이지 크기는 50개 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-239">By default, the maximum page size on the server is 50 records.</span></span>

<span data-ttu-id="334e5-240">첫 번째 예는 테이블에서 상위 5개 항목을 선택하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-240">The first example shows how to select the top five items from a table.</span></span> <span data-ttu-id="334e5-241">쿼리는 **ToDoItems**테이블에서 항목을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-241">The query returns the items from a table of **ToDoItems**.</span></span> <span data-ttu-id="334e5-242">**mToDoTable** 은 이전에 만든 백 엔드 테이블에 대한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-242">**mToDoTable** is the reference to the backend table that you created previously:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

<span data-ttu-id="334e5-243">다음은 첫 5개 항목을 건너뛴 후 다음 5개를 반환하는 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-243">Here's a query that skips the first five items, and then returns the next five:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

<span data-ttu-id="334e5-244">하나의 테이블에 모든 레코드를 가져오려면 모든 페이지에서 반복하는 코드를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-244">If you wish to get all records in a table, implement code to iterate over all pages:</span></span>

```java
List<MyDataModel> results = new List<MyDataModel>();
int nResults;
do {
    int currentCount = results.size();
    List<MyDataModel> pagedResults = mDataTable
        .skip(currentCount).top(500)
        .execute().get();
    nResults = pagedResults.size();
    if (nResults > 0) {
        results.addAll(pagedResults);
    }
} while (nResults > 0);
```

<span data-ttu-id="334e5-245">이 메서드를 사용하여 모든 레코드를 요청하면 Mobile Apps 백 엔드에 대한 요청이 최소 두 개 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-245">A request for all records using this method creates a minimum of two requests to the Mobile Apps backend.</span></span>

> [!TIP]
> <span data-ttu-id="334e5-246">올바른 페이지 크기를 선택하면 요청이 발생하는 동안의 메모리 사용량과 데이터를 완전히 수신하는 데 걸리는 시간 및 대역폭 사용량 사이에 균형이 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-246">Choosing the right page size is a balance between memory usage while the request is happening, bandwidth usage and delay in receiving the data completely.</span></span>  <span data-ttu-id="334e5-247">기본값(레코드 50개)은 모든 장치에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-247">The default (50 records) is suitable for all devices.</span></span>  <span data-ttu-id="334e5-248">대형 메모리 장치에서 독점적으로 작동하는 경우 최대 500개까지 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-248">If you exclusively operate on larger memory devices, increase up to 500.</span></span>  <span data-ttu-id="334e5-249">페이지 크기를 레코드 500개를 초과하도록 늘리면 허용되지 않는 지연과 큰 메모리 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-249">We have found that increasing the page size beyond 500 records results in unacceptable delays and large memory issues.</span></span>

### <span data-ttu-id="334e5-250"><a name="chaining"></a>방법: 쿼리 메서드 연결</span><span class="sxs-lookup"><span data-stu-id="334e5-250"><a name="chaining"></a>How to: Concatenate query methods</span></span>

<span data-ttu-id="334e5-251">백 엔드 테이블을 쿼리하는 데 사용되는 메서드를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-251">The methods used in querying backend tables can be concatenated.</span></span> <span data-ttu-id="334e5-252">쿼리 메서드를 연결하면 정렬 및 페이징되는 필터링된 행의 특정 열을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-252">Chaining query methods allows you to select specific columns of filtered rows that are sorted and paged.</span></span> <span data-ttu-id="334e5-253">상당히 복잡한 논리 필터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-253">You can create complex logical filters.</span></span>  <span data-ttu-id="334e5-254">각 쿼리 메서드는 쿼리 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-254">Each query method returns a Query object.</span></span> <span data-ttu-id="334e5-255">일련의 메서드를 종료하고 실제로 쿼리를 실행하려면 **execute** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-255">To end the series of methods and actually run the query, call the **execute** method.</span></span> <span data-ttu-id="334e5-256">예:</span><span class="sxs-lookup"><span data-stu-id="334e5-256">For example:</span></span>

```java
List<ToDoItem> results = mToDoTable
        .where()
        .year("due").eq(2013)
        .and(
            startsWith("text", "PRI0").or().field("duration").gt(10)
        )
        .orderBy(duration, QueryOrder.Ascending)
        .select("id", "complete", "text", "duration")
        .skip(200).top(100)
        .execute()
        .get();
```

<span data-ttu-id="334e5-257">연결된 쿼리 메서드의 순서는 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-257">The chained query methods must be ordered as follows:</span></span>

1. <span data-ttu-id="334e5-258">필터링(**where**) 메서드.</span><span class="sxs-lookup"><span data-stu-id="334e5-258">Filtering (**where**) methods.</span></span>
2. <span data-ttu-id="334e5-259">정렬(**orderBy**) 메서드.</span><span class="sxs-lookup"><span data-stu-id="334e5-259">Sorting (**orderBy**) methods.</span></span>
3. <span data-ttu-id="334e5-260">선택(**select**) 메서드.</span><span class="sxs-lookup"><span data-stu-id="334e5-260">Selection (**select**) methods.</span></span>
4. <span data-ttu-id="334e5-261">페이징(**skip** 및 **top**) 메서드.</span><span class="sxs-lookup"><span data-stu-id="334e5-261">paging (**skip** and **top**) methods.</span></span>

## <span data-ttu-id="334e5-262"><a name="binding"></a>사용자 인터페이스에 데이터 바인딩</span><span class="sxs-lookup"><span data-stu-id="334e5-262"><a name="binding"></a>Bind data to the user interface</span></span>

<span data-ttu-id="334e5-263">데이터 바인딩에는 세 가지 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-263">Data binding involves three components:</span></span>

* <span data-ttu-id="334e5-264">데이터 원본</span><span class="sxs-lookup"><span data-stu-id="334e5-264">The data source</span></span>
* <span data-ttu-id="334e5-265">화면 레이아웃</span><span class="sxs-lookup"><span data-stu-id="334e5-265">The screen layout</span></span>
* <span data-ttu-id="334e5-266">두 요소를 연결하는 어댑터</span><span class="sxs-lookup"><span data-stu-id="334e5-266">The adapter that ties the two together.</span></span>

<span data-ttu-id="334e5-267">샘플 코드에서는 모바일 앱 SQL Azure 테이블 **ToDoItem** 의 데이터를 배열로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-267">In our sample code, we return the data from the Mobile Apps SQL Azure table **ToDoItem** into an array.</span></span> <span data-ttu-id="334e5-268">이 활동은 데이터 응용 프로그램에서 매우 흔한 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-268">This activity is a common pattern for data applications.</span></span>  <span data-ttu-id="334e5-269">데이터베이스 쿼리는 종종 클라이언트에서 목록 또는 배열로 가져오는 행 컬렉션을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-269">Database queries often return a collection of rows that the client gets in a list or array.</span></span> <span data-ttu-id="334e5-270">이 샘플에서 배열은 데이터 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-270">In this sample, the array is the data source.</span></span>  <span data-ttu-id="334e5-271">코드는 장치에 나타나는 데이터 뷰를 정의하는 화면 레이아웃을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-271">The code specifies a screen layout that defines the view of the data that appears on the device.</span></span>  <span data-ttu-id="334e5-272">이 두 요소는 어댑터(이 코드에서 **ArrayAdapter&lt;ToDoItem&gt;** 클래스의 확장)를 통해 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-272">The two are bound together with an adapter, which in this code is an extension of the **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span>

#### <span data-ttu-id="334e5-273"><a name="layout"></a>레이아웃 정의</span><span class="sxs-lookup"><span data-stu-id="334e5-273"><a name="layout"></a>Define the Layout</span></span>

<span data-ttu-id="334e5-274">레이아웃은 다수의 XML 코드 조각으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-274">The layout is defined by several snippets of XML code.</span></span> <span data-ttu-id="334e5-275">기존 레이아웃을 고려할 때 다음 코드는 서버 데이터로 채울 **ListView**를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-275">Given an existing layout, the following code represents the **ListView** we want to populate with our server data.</span></span>

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

<span data-ttu-id="334e5-276">위의 코드에서 *listitem* 특성은 목록의 개별 행에 대한 레이아웃의 ID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-276">In the preceding code, the *listitem* attribute specifies the id of the layout for an individual row in the list.</span></span> <span data-ttu-id="334e5-277">이 코드는 확인란 및 관련된 텍스트를 지정하고 목록의 각 항목에 대해 한 번씩 인스턴스화됩니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-277">This code specifies a check box and its associated text and gets instantiated once for each item in the list.</span></span> <span data-ttu-id="334e5-278">이 레이아웃은 **ID** 필드를 표시하지 않고 더 복잡한 레이아웃은 디스플레이에서 추가 필드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-278">This layout does not display the **id** field, and a more complex layout would specify additional fields in the display.</span></span> <span data-ttu-id="334e5-279">이 코드는 **row_list_to_do.xml** 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-279">This code is in the **row_list_to_do.xml** file.</span></span>

```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal">
    <CheckBox
        android:id="@+id/checkToDoItem"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/checkbox_text" />
</LinearLayout>
```

#### <span data-ttu-id="334e5-280"><a name="adapter"></a>어댑터 정의</span><span class="sxs-lookup"><span data-stu-id="334e5-280"><a name="adapter"></a>Define the adapter</span></span>
<span data-ttu-id="334e5-281">이 뷰의 데이터 원본은 **ToDoItem**의 배열이기 때문에, **ArrayAdapter&lt;ToDoItem&gt;** 클래스에서 어댑터의 서브클래스를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-281">Since the data source of our view is an array of **ToDoItem**, we subclass our adapter from an **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span> <span data-ttu-id="334e5-282">이 서브클래스는 **row_list_to_do** 레이아웃을 사용하는 모든 **ToDoItem**의 뷰를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-282">This subclass produces a View for every **ToDoItem** using the **row_list_to_do** layout.</span></span>  <span data-ttu-id="334e5-283">코드에는 **ArrayAdapter&lt;E&gt;** 클래스의 확장인 다음 클래스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-283">In our code, we define the following class that is an extension of the **ArrayAdapter&lt;E&gt;** class:</span></span>

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

<span data-ttu-id="334e5-284">어댑터의 **getView** 메서드를 다시 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-284">Override the adapters **getView** method.</span></span> <span data-ttu-id="334e5-285">예:</span><span class="sxs-lookup"><span data-stu-id="334e5-285">For example:</span></span>

```
    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        View row = convertView;

        final ToDoItem currentItem = getItem(position);

        if (row == null) {
            LayoutInflater inflater = ((Activity) mContext).getLayoutInflater();
            row = inflater.inflate(R.layout.row_list_to_do, parent, false);
        }
        row.setTag(currentItem);

        final CheckBox checkBox = (CheckBox) row.findViewById(R.id.checkToDoItem);
        checkBox.setText(currentItem.getText());
        checkBox.setChecked(false);
        checkBox.setEnabled(true);

        checkBox.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View arg0) {
                if (checkBox.isChecked()) {
                    checkBox.setEnabled(false);
                    if (mContext instanceof ToDoActivity) {
                        ToDoActivity activity = (ToDoActivity) mContext;
                        activity.checkItem(currentItem);
                    }
                }
            }
        });
        return row;
    }
```

<span data-ttu-id="334e5-286">작업에서 다음과 같이 이 클래스의 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-286">We create an instance of this class in our Activity as follows:</span></span>

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

<span data-ttu-id="334e5-287">ToDoItemAdapter 생성자의 두 번째 매개 변수는 레이아웃에 대한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-287">The second parameter to the ToDoItemAdapter constructor is a reference to the layout.</span></span> <span data-ttu-id="334e5-288">이제 **ListView**를 인스턴스화하고 **ListView**에 어댑터를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-288">We can now instantiate the **ListView** and assign the adapter to the **ListView**.</span></span>

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <span data-ttu-id="334e5-289"><a name="use-adapter"></a>어댑터를 사용하여 UI에 바인딩</span><span class="sxs-lookup"><span data-stu-id="334e5-289"><a name="use-adapter"></a>Use the Adapter to Bind to the UI</span></span>

<span data-ttu-id="334e5-290">이제 데이터 바인딩을 사용할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-290">You are now ready to use data binding.</span></span> <span data-ttu-id="334e5-291">다음 코드는 테이블의 항목을 가져오고 로컬 어댑터를 반환된 항목으로 채우는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-291">The following code shows how to get items in the table and fills the local adapter with the returned items.</span></span>

```java
    public void showAll(View view) {
        AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
            @Override
            protected Void doInBackground(Void... params) {
                try {
                    final List<ToDoItem> results = mToDoTable.execute().get();
                    runOnUiThread(new Runnable() {

                        @Override
                        public void run() {
                            mAdapter.clear();
                            for (ToDoItem item : results) {
                                mAdapter.add(item);
                            }
                        }
                    });
                } catch (Exception exception) {
                    createAndShowDialog(exception, "Error");
                }
                return null;
            }
        };
        runAsyncTask(task);
    }
```

<span data-ttu-id="334e5-292">**ToDoItem** 테이블을 수정할 때 언제든지 어댑터를 호출하세요.</span><span class="sxs-lookup"><span data-stu-id="334e5-292">Call the adapter any time you modify the **ToDoItem** table.</span></span> <span data-ttu-id="334e5-293">수정은 레코드별로 이루어지기 때문에 사용자는 컬렉션이 아닌 단일 행을 다루게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-293">Since modifications are done on a record by record basis, you handle a single row instead of a collection.</span></span> <span data-ttu-id="334e5-294">항목을 삽입할 때는 어댑터에 대해 **add** 메서드를 호출하고, 삭제할 때는 **remove** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-294">When you insert an item, call the **add** method on the adapter; when deleting, call the **remove** method.</span></span>

<span data-ttu-id="334e5-295">전체 예제는 [Android 빠른 시작 프로젝트][21]에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-295">You can find a complete example in the [Android Quickstart Project][21].</span></span>

## <span data-ttu-id="334e5-296"><a name="inserting"></a>백 엔드에 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="334e5-296"><a name="inserting"></a>Insert data into the backend</span></span>

<span data-ttu-id="334e5-297">*ToDoItem* 클래스 인스턴스를 인스턴스화하고 해당 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-297">Instantiate an instance of the *ToDoItem* class and set its properties.</span></span>

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

<span data-ttu-id="334e5-298">그런 다음 **insert()** 를 사용하여 개체를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-298">Then use **insert()** to insert an object:</span></span>

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="334e5-299">반환된 엔터티는 백 엔드 테이블에 삽입된 데이터와 일치하며 이는 ID 및 백 엔드에 설정된 다른 값(예: `createdAt`, `updatedAt` 및 `version` 필드)을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-299">The returned entity matches the data inserted into the backend table, included the ID and any other values (such as the `createdAt`, `updatedAt`, and `version` fields) set on the backend.</span></span>

<span data-ttu-id="334e5-300">Mobile Apps 테이블에는 **id**라고 하는 기본 키 열이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-300">Mobile Apps tables require a primary key column named **id**.</span></span> <span data-ttu-id="334e5-301">이 열은 문자열이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-301">This column must be a string.</span></span> <span data-ttu-id="334e5-302">ID 열의 기본값은 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-302">The default value of the ID column is a GUID.</span></span>  <span data-ttu-id="334e5-303">전자 메일 주소나 사용자 이름처럼 다른 고유한 값을 입력해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-303">You can provide other unique values, such as email addresses or usernames.</span></span> <span data-ttu-id="334e5-304">삽입된 레코드에 대한 문자열 ID 값을 입력하지 않으면 백 엔드에서 새 GUID를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-304">When a string ID value is not provided for an inserted record, the backend generates a new GUID.</span></span>

<span data-ttu-id="334e5-305">문자열 ID 값은 다음과 같은 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-305">String ID values provide the following advantages:</span></span>

* <span data-ttu-id="334e5-306">데이터베이스에 대한 왕복 없이도 ID를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-306">IDs can be generated without making a round trip to the database.</span></span>
* <span data-ttu-id="334e5-307">여러 테이블 또는 데이터베이스의 레코드를 병합하기가 더 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-307">Records are easier to merge from different tables or databases.</span></span>
* <span data-ttu-id="334e5-308">응용 프로그램의 논리를 통해 ID 값이 더 효율적으로 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-308">ID values integrate better with an application's logic.</span></span>

<span data-ttu-id="334e5-309">오프라인 동기화를 지원하려면 문자열 ID 값이 **필수** 입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-309">String ID values are **REQUIRED** for offline sync support.</span></span>  <span data-ttu-id="334e5-310">ID가 백 엔드 데이터베이스에 저장되고 나면 ID를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-310">You cannot change an Id once it is stored in the backend database.</span></span>

## <span data-ttu-id="334e5-311"><a name="updating"></a>모바일 앱의 데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="334e5-311"><a name="updating"></a>Update data in a mobile app</span></span>

<span data-ttu-id="334e5-312">테이블의 데이터를 업데이트하려면 새 개체를 **update()** 메서드에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-312">To update data in a table, pass the new object to the **update()** method.</span></span>

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="334e5-313">이 예제에서 *item*은 일부 변경된 *ToDoItem* 테이블의 행에 대한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-313">In this example, *item* is a reference to a row in the *ToDoItem* table, which has had some changes made to it.</span></span>  <span data-ttu-id="334e5-314">**id** 가 같은 행이 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-314">The row with the same **id** is updated.</span></span>

## <span data-ttu-id="334e5-315"><a name="deleting"></a>모바일 앱의 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="334e5-315"><a name="deleting"></a>Delete data in a mobile app</span></span>

<span data-ttu-id="334e5-316">다음 코드는 데이터 개체를 지정하여 테이블에서 데이터를 삭제하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-316">The following code shows how to delete data from a table by specifying the data object.</span></span>

```java
mToDoTable
    .delete(item);
```

<span data-ttu-id="334e5-317">또한 삭제할 행의 **ID** 필드를 지정하여 항목을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-317">You can also delete an item by specifying the **id** field of the row to delete.</span></span>

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <span data-ttu-id="334e5-318"><a name="lookup"></a>ID로 특정 항목 조회</span><span class="sxs-lookup"><span data-stu-id="334e5-318"><a name="lookup"></a>Look up a specific item by Id</span></span>

<span data-ttu-id="334e5-319">**lookUp()** 메서드를 사용하여 특정 **id** 필드 값을 가진 항목을 조회합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-319">Look up an item with a specific **id** field with the **lookUp()** method:</span></span>

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <span data-ttu-id="334e5-320"><a name="untyped"></a>방법: 형식화되지 않은 데이터 작업</span><span class="sxs-lookup"><span data-stu-id="334e5-320"><a name="untyped"></a>How to: Work with untyped data</span></span>

<span data-ttu-id="334e5-321">형식화되지 않은 프로그래밍 모델은 JSON 직렬화를 정확하게 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-321">The untyped programming model gives you exact control over JSON serialization.</span></span>  <span data-ttu-id="334e5-322">형식화되지 않은 프로그래밍 모델을 사용하는 것이 좋은 몇 가지 일반적인 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-322">There are some common scenarios where you may wish to use an untyped programming model.</span></span> <span data-ttu-id="334e5-323">백 엔드 테이블에 여러 열이 있는데 그 중 일부만 참조해야 하는 경우를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-323">For example, if your backend table contains many columns and you only need to reference a subset of the columns.</span></span>  <span data-ttu-id="334e5-324">형식화된 모델을 사용하려면 데이터 클래스의 Mobile Apps 백 엔드에 정의된 모든 열을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-324">The typed model requires you to define all the columns defined in the Mobile Apps backend in your data class.</span></span>  <span data-ttu-id="334e5-325">데이터에 액세스하는 대부분의 API 호출은 형식화된 프로그래밍 호출과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-325">Most of the API calls for accessing data are similar to the typed programming calls.</span></span> <span data-ttu-id="334e5-326">주요 차이점은 형식화되지 않은 모델에서는 **MobileServiceTable** 개체 대신 **MobileServiceJsonTable** 개체에 대해 메서드를 호출한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-326">The main difference is that in the untyped model you invoke methods on the **MobileServiceJsonTable** object, instead of the **MobileServiceTable** object.</span></span>

### <span data-ttu-id="334e5-327"><a name="json_instance"></a>형식화되지 않은 테이블 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="334e5-327"><a name="json_instance"></a>Create an instance of an untyped table</span></span>

<span data-ttu-id="334e5-328">형식화된 모델과 유사하게 테이블 참조를 가져와서 시작합니다. 하지만 이 경우에는 이 참조가 **MobileServicesJsonTable** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-328">Similar to the typed model, you start by getting a table reference, but in this case it's a **MobileServicesJsonTable** object.</span></span> <span data-ttu-id="334e5-329">클라이언트의 인스턴스에 대해 **getTable** 메서드를 호출하여 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-329">Obtain the reference by calling the **getTable** method on an instance of the client:</span></span>

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

<span data-ttu-id="334e5-330">**MobileServiceJsonTable**의 인스턴스를 만들면 형식화된 프로그래밍 모델을 사용할 때와 거의 동일한 API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-330">Once you have created an instance of the **MobileServiceJsonTable**, it has virtually the same API available as with the typed programming model.</span></span> <span data-ttu-id="334e5-331">경우에 따라 메서드가 형식화된 매개 변수 대신 형식화되지 않은 매개 변수를 가져오기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-331">In some cases, the methods take an untyped parameter instead of a typed parameter.</span></span>

### <span data-ttu-id="334e5-332"><a name="json_insert"></a>형식화되지 않은 테이블에 삽입</span><span class="sxs-lookup"><span data-stu-id="334e5-332"><a name="json_insert"></a>Insert into an untyped table</span></span>
<span data-ttu-id="334e5-333">다음 코드는 삽입하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-333">The following code shows how to do an insert.</span></span> <span data-ttu-id="334e5-334">첫 번째 단계는 [gson][3] 라이브러리의 일부인 [JsonObject][1]를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-334">The first step is to create a [JsonObject][1], which is part of the [gson][3] library.</span></span>

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

<span data-ttu-id="334e5-335">그런 다음 **insert()** 를 사용하여 형식화되지 않은 개체를 테이블에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-335">Then, Use **insert()** to insert the untyped object into the table.</span></span>

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

<span data-ttu-id="334e5-336">삽입된 개체의 ID를 가져와야 하는 경우 **getAsJsonPrimitive()** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-336">If you need to get the ID of the inserted object, use the **getAsJsonPrimitive()** method.</span></span>

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <span data-ttu-id="334e5-337"><a name="json_delete"></a>형식화되지 않은 테이블에서 삭제</span><span class="sxs-lookup"><span data-stu-id="334e5-337"><a name="json_delete"></a>Delete from an untyped table</span></span>
<span data-ttu-id="334e5-338">다음 코드는 인스턴스를 삭제하는 방법을 보여 줍니다. 이 경우에는 앞의 **insert** 예에서 만들어진 것과 동일한 *JsonObject* 인스턴스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-338">The following code shows how to delete an instance, in this case, the same instance of a **JsonObject** that was created in the prior *insert* example.</span></span> <span data-ttu-id="334e5-339">코드는 형식화된 경우와 같지만 메서드가 **JsonObject**를 참조하기 때문에 메서드의 서명이 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-339">The code is the same as with the typed case, but the method has a different signature since it references an **JsonObject**.</span></span>

```java
mToDoTable
    .delete(insertedItem);
```

<span data-ttu-id="334e5-340">ID를 사용하여 직접 인스턴스를 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-340">You can also delete an instance directly by using its ID:</span></span>

```java
mToDoTable.delete(ID);
```

### <span data-ttu-id="334e5-341"><a name="json_get"></a>형식화되지 않은 테이블에서 모든 행 반환</span><span class="sxs-lookup"><span data-stu-id="334e5-341"><a name="json_get"></a>Return all rows from an untyped table</span></span>
<span data-ttu-id="334e5-342">다음 코드는 전체 테이블을 검색하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-342">The following code shows how to retrieve an entire table.</span></span> <span data-ttu-id="334e5-343">Json 테이블을 사용하기 때문에 테이블 열의 일부만 선택적으로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-343">Since you are using a JSON Table, you can selectively retrieve only some of the table's columns.</span></span>

```java
public void showAllUntyped(View view) {
    new AsyncTask<Void, Void, Void>() {
        @Override
        protected Void doInBackground(Void... params) {
            try {
                final JsonElement result = mJsonToDoTable.execute().get();
                final JsonArray results = result.getAsJsonArray();
                runOnUiThread(new Runnable() {

                    @Override
                    public void run() {
                        mAdapter.clear();
                        for (JsonElement item : results) {
                            String ID = item.getAsJsonObject().getAsJsonPrimitive("id").getAsString();
                            String mText = item.getAsJsonObject().getAsJsonPrimitive("text").getAsString();
                            Boolean mComplete = item.getAsJsonObject().getAsJsonPrimitive("complete").getAsBoolean();
                            ToDoItem mToDoItem = new ToDoItem();
                            mToDoItem.setId(ID);
                            mToDoItem.setText(mText);
                            mToDoItem.setComplete(mComplete);
                            mAdapter.add(mToDoItem);
                        }
                    }
                });
            } catch (Exception exception) {
                createAndShowDialog(exception, "Error");
            }
            return null;
        }
    }.execute();
}
```

<span data-ttu-id="334e5-344">형식화된 모델에 제공되는 것과 동일한 필터링 및 페이징 메서드가 형식화되지 않은 모델에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-344">The same set of filtering, filtering and paging methods that are available for the typed model are available for the untyped model.</span></span>

## <span data-ttu-id="334e5-345"><a name="offline-sync"></a>오프라인 동기화 구현</span><span class="sxs-lookup"><span data-stu-id="334e5-345"><a name="offline-sync"></a>Implement Offline Sync</span></span>

<span data-ttu-id="334e5-346">Azure Mobile Apps 클라이언트 SDK는 SQLite 데이터베이스를 사용하여 서버 데이터의 복사본을 로컬에 저장하여 데이터의 오프라인 동기화를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-346">The Azure Mobile Apps Client SDK also implements offline synchronization of data by using a SQLite database to store a copy of the server data locally.</span></span>  <span data-ttu-id="334e5-347">오프라인 테이블에 수행되는 작업에는 모바일 연결이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-347">Operations performed on an offline table do not require mobile connectivity to work.</span></span>  <span data-ttu-id="334e5-348">오프라인 동기화는 충돌 해결을 위해보다 복잡한 논리를 사용하는 대신 복원력과 성능을 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-348">Offline sync aids in resilience and performance at the expense of more complex logic for conflict resolution.</span></span>  <span data-ttu-id="334e5-349">Azure Mobile Apps 클라이언트 SDK는 다음 기능을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-349">The Azure Mobile Apps Client SDK implements the following features:</span></span>

* <span data-ttu-id="334e5-350">증분 동기화: 업데이트된 레코드와 새 레코드 만 다운로드되기 때문에 대역폭과 메모리 사용량이 절약됩니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-350">Incremental Sync: Only updated and new records are downloaded, saving bandwidth and memory consumption.</span></span>
* <span data-ttu-id="334e5-351">낙관적 동시성: 작업이 성공한 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-351">Optimistic Concurrency: Operations are assumed to succeed.</span></span>  <span data-ttu-id="334e5-352">충돌 해결은 서버에서 업데이트가 수행될 때까지 지연됩니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-352">Conflict Resolution is deferred until updates are performed on the server.</span></span>
* <span data-ttu-id="334e5-353">충돌 해결: SDK는 서버에서 충돌하는 변경이 발생하면 이를 감지하고 사용자에게 경고하기 위해 후크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-353">Conflict Resolution: The SDK detects when a conflicting change has been made at the server and provides hooks to alert the user.</span></span>
* <span data-ttu-id="334e5-354">일시 삭제: 삭제된 레코드가 삭제된 것으로 표시되기 때문에 다른 장치가 오프라인 캐시를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-354">Soft Delete: Deleted records are marked deleted, allowing other devices to update their offline cache.</span></span>

### <a name="initialize-offline-sync"></a><span data-ttu-id="334e5-355">오프라인 동기화 초기화</span><span class="sxs-lookup"><span data-stu-id="334e5-355">Initialize Offline Sync</span></span>

<span data-ttu-id="334e5-356">각 오프라인 테이블은 사용 전에 오프라인 캐시에 정의되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-356">Each offline table must be defined in the offline cache before use.</span></span>  <span data-ttu-id="334e5-357">일반적으로 테이블 정의는 클라이언트 생성 직후에 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-357">Normally, table definition is done immediately after the creation of the client:</span></span>

```java
AsyncTask<Void, Void, Void> initializeStore(MobileServiceClient mClient)
    throws MobileServiceLocalStoreException, ExecutionException, InterruptedException
{
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>() {
        @Override
        protected void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                if (syncContext.isInitialized()) {
                    return null;
                }
                SQLiteLocalStore localStore = new SQLiteLocalStore(mClient.getContext(), "offlineStore", null, 1);

                // Create a table definition.  As a best practice, store this with the model definition and return it via
                // a static method
                Map<String, ColumnDataType> toDoItemDefinition = new HashMap<String, ColumnDataType>();
                toDoItemDefinition.put("id", ColumnDataType.String);
                toDoItemDefinition.put("complete", ColumnDataType.Boolean);
                toDoItemDefinition.put("text", ColumnDataType.String);
                toDoItemDefinition.put("version", ColumnDataType.String);
                toDoItemDefinition.put("updatedAt", ColumnDataType.DateTimeOffset);

                // Now define the table in the local store
                localStore.defineTable("ToDoItem", toDoItemDefinition);

                // Specify a sync handler for conflict resolution
                SimpleSyncHandler handler = new SimpleSyncHandler();

                // Initialize the local store
                syncContext.initialize(localStore, handler).get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

### <a name="obtain-a-reference-to-the-offline-cache-table"></a><span data-ttu-id="334e5-358">오프라인 캐시 테이블에 대한 참조 얻기</span><span class="sxs-lookup"><span data-stu-id="334e5-358">Obtain a reference to the Offline Cache Table</span></span>

<span data-ttu-id="334e5-359">온라인 테이블의 경우 `.getTable()`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-359">For an online table, you use `.getTable()`.</span></span>  <span data-ttu-id="334e5-360">오프라인 테이블의 경우 `.getSyncTable()`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-360">For an offline table, use `.getSyncTable()`:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

<span data-ttu-id="334e5-361">온라인 테이블에서 사용할 수 있는 모든 메서드(필터링, 정렬, 페이징, 데이터 삽입, 데이터 업데이트 및 데이터 삭제 포함)는 온라인 및 오프라인 테이블에서 동일하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-361">All the methods that are available for online tables (including filtering, sorting, paging, inserting data, updating data, and deleting data) work equally well on online and offline tables.</span></span>

### <a name="synchronize-the-local-offline-cache"></a><span data-ttu-id="334e5-362">로컬 오프라인 캐시 동기화</span><span class="sxs-lookup"><span data-stu-id="334e5-362">Synchronize the Local Offline Cache</span></span>

<span data-ttu-id="334e5-363">동기화는 앱의 제어 범위 내에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-363">Synchronization is within the control of your app.</span></span>  <span data-ttu-id="334e5-364">다음은 동기화 메서드의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-364">Here is an example synchronization method:</span></span>

```java
private AsyncTask<Void, Void, Void> sync(MobileServiceClient mClient) {
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
        @Override
        protected Void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                syncContext.push().get();
                mToDoTable.pull(null, "todoitem").get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

<span data-ttu-id="334e5-365">쿼리 이름이 `.pull(query, queryname)` 메서드에 제공되면 증분 동기화를 사용하여 마지막으로 완료된 끌어오기 이후에 생성되거나 변경된 레코드만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-365">If a query name is provided to the `.pull(query, queryname)` method, then incremental sync is used to return only records that have been created or changed since the last successfully completed pull.</span></span>

### <a name="handle-conflicts-during-offline-synchronization"></a><span data-ttu-id="334e5-366">오프라인 동기화 중 충돌 처리</span><span class="sxs-lookup"><span data-stu-id="334e5-366">Handle Conflicts during Offline Synchronization</span></span>

<span data-ttu-id="334e5-367">`.push()` 작업 중에 충돌이 발생하면 `MobileServiceConflictException`이 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-367">If a conflict happens during a `.push()` operation, a `MobileServiceConflictException` is thrown.</span></span>   <span data-ttu-id="334e5-368">서버에서 발급한 항목은 예외에 포함되며 예외에서 `.getItem()`으로 검색될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-368">The server-issued item is embedded in the exception and can be retrieved by `.getItem()` on the exception.</span></span>  <span data-ttu-id="334e5-369">MobileServiceSyncContext 개체에서 다음 항목을 호출하여 푸시를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-369">Adjust the push by calling the following items on the MobileServiceSyncContext object:</span></span>

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

<span data-ttu-id="334e5-370">모든 충돌이 원하는 대로 표시되면 `.push()`를 다시 호출하여 모든 충돌을 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-370">Once all conflicts are marked as you wish, call `.push()` again to resolve all the conflicts.</span></span>

## <span data-ttu-id="334e5-371"><a name="custom-api"></a>사용자 지정 API 호출</span><span class="sxs-lookup"><span data-stu-id="334e5-371"><a name="custom-api"></a>Call a custom API</span></span>

<span data-ttu-id="334e5-372">사용자 지정 API는 삽입, 업데이트, 삭제 또는 읽기 작업에 매핑되지 않는 서버 기능을 노출하는 사용자 지정 끝점을 정의할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-372">A custom API enables you to define custom endpoints that expose server functionality that does not map to an insert, update, delete, or read operation.</span></span> <span data-ttu-id="334e5-373">사용자 지정 API를 사용하면 HTTP 메시지 헤더 읽기와 설정 및 JSON 이외의 메시지 본문 형식 정의를 비롯하여 더 효율적으로 메시징을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-373">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="334e5-374">Android 클라이언트에서 **invokeApi** 메서드를 호출하여 사용자 지정 API 끝점을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-374">From an Android client, you call the **invokeApi** method to call the custom API endpoint.</span></span> <span data-ttu-id="334e5-375">다음 예제에서는 **completeAll**이라는 API 끝점을 호출하는 방법을 보여주며 이는 **MarkAllResult**라는 컬렉션 클래스를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-375">The following example shows how to call an API endpoint named **completeAll**, which returns a collection class named **MarkAllResult**.</span></span>

```java
public void completeItem(View view) {
    ListenableFuture<MarkAllResult> result = mClient.invokeApi("completeAll", MarkAllResult.class);
    Futures.addCallback(result, new FutureCallback<MarkAllResult>() {
        @Override
        public void onFailure(Throwable exc) {
            createAndShowDialog((Exception) exc, "Error");
        }

        @Override
        public void onSuccess(MarkAllResult result) {
            createAndShowDialog(result.getCount() + " item(s) marked as complete.", "Completed Items");
            refreshItemsFromTable();
        }
    });
}
```

<span data-ttu-id="334e5-376">**invokeApi** 메서드가 클라이언트에서 호출되어 POST 요청을 새 사용자 지정 API로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-376">The **invokeApi** method is called on the client, which sends a POST request to the new custom API.</span></span> <span data-ttu-id="334e5-377">사용자 지정 API에서 반환하는 결과는 오류와 마찬가지로 메시지 대화 상자에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-377">The result returned by the custom API is displayed in a message dialog, as are any errors.</span></span> <span data-ttu-id="334e5-378">다른 버전의 **invokeApi** 를 사용하면 필요에 따라 요청 본문에 개체를 보내고 HTTP 메서드를 지정하며 요청으로 쿼리 매개 변수를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-378">Other versions of **invokeApi** let you optionally send an object in the request body, specify the HTTP method, and send query parameters with the request.</span></span> <span data-ttu-id="334e5-379">**invokeApi** 의 형식화되지 않은 버전도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-379">Untyped versions of **invokeApi** are provided as well.</span></span>

## <span data-ttu-id="334e5-380"><a name="authentication"></a>앱에 인증 추가</span><span class="sxs-lookup"><span data-stu-id="334e5-380"><a name="authentication"></a>Add authentication to your app</span></span>

<span data-ttu-id="334e5-381">자습서는 이러한 기능을 추가하는 방법을 이미 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-381">Tutorials already describe in detail how to add these features.</span></span>

<span data-ttu-id="334e5-382">App Service는 Facebook, Google, Microsoft 계정, Twitter 및 Azure Active Directory와 같이 다양한 외부 ID 공급자를 사용하여 [앱 사용자의 인증](app-service-mobile-android-get-started-users.md) 을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-382">App Service supports [authenticating app users](app-service-mobile-android-get-started-users.md) using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="334e5-383">테이블에 대해 사용 권한을 설정하여 특정 작업을 위한 액세스를 인증된 사용자로만 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-383">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="334e5-384">인증된 사용자의 ID를 사용하여 서버 스크립트에 인증 규칙을 구현할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-384">You can also use the identity of authenticated users to implement authorization rules in your backend.</span></span>

<span data-ttu-id="334e5-385">두 가지의 인증 흐름, 즉 **서버** 흐름과 **클라이언트** 흐름이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-385">Two authentication flows are supported: a **server** flow and a **client** flow.</span></span> <span data-ttu-id="334e5-386">서버 흐름의 경우 ID 공급자의 웹 인터페이스를 사용하므로 인증 경험이 가장 단순합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-386">The server flow provides the simplest authentication experience, as it relies on the identity providers web interface.</span></span>  <span data-ttu-id="334e5-387">서버 흐름 인증을 구현하기 위해 추가 SDK가 필요하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-387">No additional SDKs are required to implement server flow authentication.</span></span> <span data-ttu-id="334e5-388">서버 흐름 인증은 모바일 장치와 긴밀하게 통합되지 않으므로 개념 증명 시나리오에만 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-388">Server flow authentication does not provide a deep integration into the mobile device and is only recommended for proof of concept scenarios.</span></span>

<span data-ttu-id="334e5-389">클라이언트 흐름의 경우 ID 공급자가 제공한 SDK를 사용하므로 Single Sign-On 같은 장치별 기능과 심도 깊은 통합이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-389">The client flow allows for deeper integration with device-specific capabilities such as single sign-on as it relies on SDKs provided by the identity provider.</span></span>  <span data-ttu-id="334e5-390">예를 들어 Facebook SDK를 모바일 응용 프로그램에 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-390">For example, you can integrate the Facebook SDK into your mobile application.</span></span>  <span data-ttu-id="334e5-391">모바일 클라이언트는 Facebook 앱으로 전환한 후 다시 모바일 앱으로 전환하기 전에 사용자의 로그온을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-391">The mobile client swaps into the Facebook app and confirms your sign-on before swapping back to your mobile app.</span></span>

<span data-ttu-id="334e5-392">앱에서 인증을 사용하도록 설정하려면 다음 네 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-392">Four steps are required to enable authentication in your app:</span></span>

* <span data-ttu-id="334e5-393">ID 공급자로 인증할 수 있도록 앱을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-393">Register your app for authentication with an identity provider.</span></span>
* <span data-ttu-id="334e5-394">App Service 백 엔드를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-394">Configure your App Service backend.</span></span>
* <span data-ttu-id="334e5-395">App Service 백 엔드에서 테이블 사용 권한을 인증된 사용자로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-395">Restrict table permissions to authenticated users only on the App Service backend.</span></span>
* <span data-ttu-id="334e5-396">앱에 인증 코드 추가</span><span class="sxs-lookup"><span data-stu-id="334e5-396">Add authentication code to your app.</span></span>

<span data-ttu-id="334e5-397">테이블에 대해 사용 권한을 설정하여 특정 작업을 위한 액세스를 인증된 사용자로만 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-397">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="334e5-398">인증된 사용자의 SID를 사용하여 요청을 수정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-398">You can also use the SID of an authenticated user to modify requests.</span></span>  <span data-ttu-id="334e5-399">자세한 내용은 [인증 시작] 및 서버 SDK 사용 방법 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="334e5-399">For more information, review [Get started with authentication] and the Server SDK HOWTO documentation.</span></span>

### <span data-ttu-id="334e5-400"><a name="caching"></a>인증: 서버 흐름</span><span class="sxs-lookup"><span data-stu-id="334e5-400"><a name="caching"></a>Authentication: Server Flow</span></span>

<span data-ttu-id="334e5-401">다음 코드는 Google 공급자를 사용하여 서버 흐름 로그인 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-401">The following code starts a server flow login process using the Google provider.</span></span>  <span data-ttu-id="334e5-402">Google 공급자에 대한 보안 요구 사항으로 인해 추가 구성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-402">Additional configuration is required because of the security requirements for the Google provider:</span></span>

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

<span data-ttu-id="334e5-403">또한 기본 활동 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-403">In addition, add the following method to the main Activity class:</span></span>

```java
// You can choose any unique number here to differentiate auth providers from each other. Note this is the same code at login() and onActivityResult().
public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    // When request completes
    if (resultCode == RESULT_OK) {
        // Check the request code matches the one we send in the login request
        if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
            MobileServiceActivityResult result = mClient.onActivityResult(data);
            if (result.isLoggedIn()) {
                // login succeeded
                createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                createTable();
            } else {
                // login failed, check the error message
                String errorMessage = result.getErrorMessage();
                createAndShowDialog(errorMessage, "Error");
            }
        }
    }
}
```

<span data-ttu-id="334e5-404">기본 활동에 정의된 `GOOGLE_LOGIN_REQUEST_CODE`는 `login()` 메서드와 `onActivityResult()` 메서드에 내에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-404">The `GOOGLE_LOGIN_REQUEST_CODE` defined in your main Activity is used for the `login()` method and within the `onActivityResult()` method.</span></span>  <span data-ttu-id="334e5-405">`login()` 메서드와 `onActivityResult()` 메서드에 동일한 번호가 사용되는 한 고유 번호를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-405">You can choose any unique number, as long as the same number is used within the `login()` method and the `onActivityResult()` method.</span></span>  <span data-ttu-id="334e5-406">클라이언트 코드를 서비스 어댑터로 추상화하는 경우(앞서 설명한 것처럼) 서비스 어댑터에서 적절한 메서드를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-406">If you abstract the client code into a service adapter (as shown earlier), you should call the appropriate methods on the service adapter.</span></span>

<span data-ttu-id="334e5-407">또한 customtab을 위해 프로젝트를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-407">You also need to configure the project for customtabs.</span></span>  <span data-ttu-id="334e5-408">먼저 리디렉션 URL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-408">First specify a redirect-URL.</span></span>  <span data-ttu-id="334e5-409">다음 조각을 `AndroidManifest.xml`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-409">Add the following snippet to `AndroidManifest.xml`:</span></span>

```xml
<activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback"/>
    </intent-filter>
</activity>
```

<span data-ttu-id="334e5-410">**redirectUriScheme**을 응용 프로그램의 `build.gradle` 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-410">Add the **redirectUriScheme** to the `build.gradle` file for your application:</span></span>

```text
android {
    buildTypes {
        release {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
        debug {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
    }
}
```

<span data-ttu-id="334e5-411">마지막으로 `com.android.support:customtabs:23.0.1`을 `build.gradle` 파일의 종속성 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-411">Finally, add `com.android.support:customtabs:23.0.1` to the dependencies list in the `build.gradle` file:</span></span>

```text
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.google.code.gson:gson:2.3'
    compile 'com.google.guava:guava:18.0'
    compile 'com.android.support:customtabs:23.0.1'
    compile 'com.squareup.okhttp:okhttp:2.5.0'
    compile 'com.microsoft.azure:azure-mobile-android:3.2.0@aar'
    compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@jar'
}
```

<span data-ttu-id="334e5-412">**getUserId** 메서드를 사용하여 **MobileServiceUser**에서 로그인한 사용자의 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-412">Obtain the ID of the logged-in user from a **MobileServiceUser** using the **getUserId** method.</span></span> <span data-ttu-id="334e5-413">미래를 사용하여 비동기 로그인 API를 호출하는 방법의 예제는 [인증 시작]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="334e5-413">For an example of how to use Futures to call the asynchronous login APIs, see [Get started with authentication].</span></span>

> [!WARNING]
> <span data-ttu-id="334e5-414">언급한 URL 구성표는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-414">The URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="334e5-415">`{url_scheme_of_you_app}`의 모든 경우가 대/소문자가 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-415">Ensure that all occurrences of `{url_scheme_of_you_app}` match case.</span></span>

### <span data-ttu-id="334e5-416"><a name="caching"></a>인증 토큰 캐시</span><span class="sxs-lookup"><span data-stu-id="334e5-416"><a name="caching"></a>Cache authentication tokens</span></span>

<span data-ttu-id="334e5-417">인증 토큰을 캐시하려면 사용자 ID 및 인증 토큰을 장치에 로컬로 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-417">Caching authentication tokens requires you to store the User ID and authentication token locally on the device.</span></span> <span data-ttu-id="334e5-418">다음에 앱이 시작될 때 캐시를 확인하여 이 값이 있는 경우 로그인 절차를 건너뛰고 이 데이터로 클라이언트를 리하이드레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-418">The next time the app starts, you check the cache, and if these values are present, you can skip the log in procedure and rehydrate the client with this data.</span></span> <span data-ttu-id="334e5-419">하지만 이 데이터는 중요하므로 휴대폰을 분실하는 경우 안전을 위해 암호화하여 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-419">However this data is sensitive, and it should be stored encrypted for safety in case the phone gets stolen.</span></span>  <span data-ttu-id="334e5-420">인증 토큰을 캐시하는 방법의 전체 예제는 [캐시 인증 토큰 섹션][7]에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-420">You can see a complete example of how to cache authentication tokens in [Cache authentication tokens section][7].</span></span>

<span data-ttu-id="334e5-421">만료된 토큰을 사용하려고 하면 *401 권한 없음* 응답을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-421">When you try to use an expired token, you receive a *401 unauthorized* response.</span></span> <span data-ttu-id="334e5-422">필터를 사용하여 인증 오류를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-422">You can handle authentication errors using filters.</span></span>  <span data-ttu-id="334e5-423">필터가 App Service 백 엔드에 대한 요청을 가로챕니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-423">Filters intercept requests to the App Service backend.</span></span> <span data-ttu-id="334e5-424">필터 코드가 401에 대한 응답을 테스트하고, 로그인 프로세스를 트리거한 후 401을 생성한 요청을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-424">The filter code tests the response for a 401, triggers the sign-in process, and then resumes the request that generated the 401.</span></span>

### <span data-ttu-id="334e5-425"><a name="refresh"></a>토큰 새로 고침 사용</span><span class="sxs-lookup"><span data-stu-id="334e5-425"><a name="refresh"></a>Use Refresh Tokens</span></span>

<span data-ttu-id="334e5-426">Azure App Service 인증 및 권한 부여에서 반환된 토큰에는 정의된 수명이 1시간 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-426">The token returned by Azure App Service Authentication and Authorization has a defined life time of one hour.</span></span>  <span data-ttu-id="334e5-427">이 기간이 지나면 사용자를 다시 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-427">After this period, you must reauthenticate the user.</span></span>  <span data-ttu-id="334e5-428">클라이언트 흐름 인증을 통해 수신한 수명이 긴 토큰을 사용하는 경우 동일한 토큰을 사용하여 Azure App Service 인증 및 권한 부여로 다시 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-428">If you are using a long-lived token that you have received via client-flow authentication, then you can reauthenticate with Azure App Service Authentication and Authorization using the same token.</span></span>  <span data-ttu-id="334e5-429">또 다른 Azure App Service 토큰이 새로운 수명으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-429">Another Azure App Service token is generated with a new lifetime.</span></span>

<span data-ttu-id="334e5-430">토큰 새로 고침을 사용하도록 공급자를 등록할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-430">You can also register the provider to use Refresh Tokens.</span></span>  <span data-ttu-id="334e5-431">토큰 새로 고침을 항상 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-431">A Refresh Token is not always available.</span></span>  <span data-ttu-id="334e5-432">추가 구성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-432">Additional configuration is required:</span></span>

* <span data-ttu-id="334e5-433">**Azure Active Directory**의 경우 Azure Active Directory 앱에 대한 클라이언트 비밀을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-433">For **Azure Active Directory**, configure a client secret for the Azure Active Directory App.</span></span>  <span data-ttu-id="334e5-434">Azure Active Directory 인증을 구성할 때 Azure App Service에 클라이언트 비밀을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-434">Specify the client secret in the Azure App Service when configuring Azure Active Directory Authentication.</span></span>  <span data-ttu-id="334e5-435">`.login()`을 호출하면 `response_type=code id_token`을 매개 변수로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-435">When calling `.login()`, pass `response_type=code id_token` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="334e5-436">**Google**의 경우 `access_type=offline`을 매개 변수로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-436">For **Google**, pass the `access_type=offline` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="334e5-437">**Microsoft 계정**은 `wl.offline_access` 범위를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-437">For **Microsoft Account**, select the `wl.offline_access` scope.</span></span>

<span data-ttu-id="334e5-438">토큰을 새로 고치려면 `.refreshUser()`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-438">To refresh a token, call `.refreshUser()`:</span></span>

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

<span data-ttu-id="334e5-439">가장 좋은 방법은 서버에서 401 응답을 감지하고 사용자 토큰을 새로 고치려고 시도하는 필터를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-439">As a best practice, create a filter that detects a 401 response from the server and tries to refresh the user token.</span></span>

## <a name="log-in-with-client-flow-authentication"></a><span data-ttu-id="334e5-440">클라이언트 흐름 인증으로 로그인</span><span class="sxs-lookup"><span data-stu-id="334e5-440">Log in with Client-flow Authentication</span></span>

<span data-ttu-id="334e5-441">클라이언트 흐름 인증을 사용한 일반적인 로그인 프로세스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-441">The general process for logging in with client-flow authentication is as follows:</span></span>

* <span data-ttu-id="334e5-442">서버 흐름 인증과 마찬가지로 Azure App Service 인증 및 권한 부여를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-442">Configure Azure App Service Authentication and Authorization as you would server-flow authentication.</span></span>
* <span data-ttu-id="334e5-443">인증을 위해 인증 공급자 SDK를 통합하여 액세스 토큰을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-443">Integrate the authentication provider SDK for authentication to produce an access token.</span></span>
* <span data-ttu-id="334e5-444">다음과 같이 `.login()` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-444">Call the `.login()` method as follows:</span></span>

    ```java
    JSONObject payload = new JSONObject();
    payload.put("access_token", result.getAccessToken());
    ListenableFuture<MobileServiceUser> mLogin = mClient.login("{provider}", payload.toString());
    Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
        @Override
        public void onFailure(Throwable exc) {
            exc.printStackTrace();
        }
        @Override
        public void onSuccess(MobileServiceUser user) {
            Log.d(TAG, "Login Complete");
        }
    });
    ```

<span data-ttu-id="334e5-445">`onSuccess()` 메서드를 성공적인 로그인에 사용할 코드로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-445">Replace the `onSuccess()` method with whatever code you wish to use on a successful login.</span></span>  <span data-ttu-id="334e5-446">`{provider}` 문자열은 유효한 공급자 즉 **aad**(Azure Active Directory), **facebook**, **google**, **microsoftaccount** 또는 **twitter**입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-446">The `{provider}` string is a valid provider: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, or **twitter**.</span></span>  <span data-ttu-id="334e5-447">사용자 지정 인증을 구현하면 사용자 지정 인증 공급자 태그를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-447">If you have implemented custom authentication, then you can also use the custom authentication provider tag.</span></span>

### <span data-ttu-id="334e5-448"><a name="adal"></a>Active Directory 인증 라이브러리(ADAL)를 사용하여 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="334e5-448"><a name="adal"></a>Authenticate users with the Active Directory Authentication Library (ADAL)</span></span>

<span data-ttu-id="334e5-449">Azure Active Directory를 사용하여 응용 프로그램에 사용자가 로그인하려면 Active Directory 인증 라이브러리(ADAL)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-449">You can use the Active Directory Authentication Library (ADAL) to sign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="334e5-450">클라이언트 흐름 로그인은 UX 느낌을 그대로 제공하고 추가 사용자 지정이 가능하기 때문에 `loginAsync()` 메서드보다 선호도가 높습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-450">Using a client flow login is often preferable to using the `loginAsync()` methods as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="334e5-451">[Active Directory 로그인에 App Service를 구성하는 방법][22] 자습서를 수행하여 AAD 로그인에 모바일 앱 백 엔드를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-451">Configure your mobile app backend for AAD sign-in by following the [How to configure App Service for Active Directory login][22] tutorial.</span></span> <span data-ttu-id="334e5-452">네이티브 클라이언트 응용 프로그램을 등록하는 선택적 단계를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-452">Make sure to complete the optional step of registering a native client application.</span></span>
2. <span data-ttu-id="334e5-453">다음 정의를 포함하도록 build.gradle 파일을 수정하여 ADAL을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-453">Install ADAL by modifying your build.gradle file to include the following definitions:</span></span>

```
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
packagingOptions {
    exclude 'META-INF/MSFTSIG.RSA'
    exclude 'META-INF/MSFTSIG.SF'
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
    compile 'com.android.support:support-v4:23.0.0'
}
```

1. <span data-ttu-id="334e5-454">응용 프로그램에 아래 코드를 추가하여 다음과 같이 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-454">Add the following code to your application, making the following replacements:</span></span>

* <span data-ttu-id="334e5-455">**INSERT-AUTHORITY-HERE** 를 응용 프로그램이 프로비전된 테넌트의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-455">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span></span> <span data-ttu-id="334e5-456">형식은 https://login.microsoftonline.com/contoso.onmicrosoft.com이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-456">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span>
* <span data-ttu-id="334e5-457">**INSERT-RESOURCE-ID-HERE** 를 모바일 앱 백 엔드에 대한 클라이언트 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-457">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span></span> <span data-ttu-id="334e5-458">포털의 Azure **Active Directory 설정**에 있는 **고급** 탭에서 클라이언트 ID를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-458">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span></span>
* <span data-ttu-id="334e5-459">**INSERT-CLIENT-ID-HERE** 를 네이티브 클라이언트 응용 프로그램에서 복사한 클라이언트 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-459">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span></span>
* <span data-ttu-id="334e5-460">HTTPS 체계를 사용하여 **INSERT-REDIRECT-URI-HERE** 를 사이트의 */.auth/login/done* 끝점으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-460">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="334e5-461">이 값은 *https://contoso.azurewebsites.net/.auth/login/done*과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-461">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

```java
private AuthenticationContext mContext;

private void authenticate() {
    String authority = "INSERT-AUTHORITY-HERE";
    String resourceId = "INSERT-RESOURCE-ID-HERE";
    String clientId = "INSERT-CLIENT-ID-HERE";
    String redirectUri = "INSERT-REDIRECT-URI-HERE";
    try {
        mContext = new AuthenticationContext(this, authority, true);
        mContext.acquireToken(this, resourceId, clientId, redirectUri, PromptBehavior.Auto, "", callback);
    } catch (Exception exc) {
        exc.printStackTrace();
    }
}

private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {
    @Override
    public void onError(Exception exc) {
        if (exc instanceof AuthenticationException) {
            Log.d(TAG, "Cancelled");
        } else {
            Log.d(TAG, "Authentication error:" + exc.getMessage());
        }
    }

    @Override
    public void onSuccess(AuthenticationResult result) {
        if (result == null || result.getAccessToken() == null
                || result.getAccessToken().isEmpty()) {
            Log.d(TAG, "Token is empty");
        } else {
            try {
                JSONObject payload = new JSONObject();
                payload.put("access_token", result.getAccessToken());
                ListenableFuture<MobileServiceUser> mLogin = mClient.login("aad", payload.toString());
                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        exc.printStackTrace();
                    }
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        Log.d(TAG, "Login Complete");
                    }
                });
            }
            catch (Exception exc){
                Log.d(TAG, "Authentication error:" + exc.getMessage());
            }
        }
    }
};

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (mContext != null) {
        mContext.onActivityResult(requestCode, resultCode, data);
    }
}
```

## <span data-ttu-id="334e5-462"><a name="filters"></a>클라이언트-서버 통신 조정</span><span class="sxs-lookup"><span data-stu-id="334e5-462"><a name="filters"></a>Adjust the Client-Server Communication</span></span>

<span data-ttu-id="334e5-463">클라이언트 연결은 일반적으로 Android SDK와 함께 제공되는 기본 HTTP 라이브러리를 사용하는 기본 HTTP 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-463">The Client connection is normally a basic HTTP connection using the underlying HTTP library supplied with the Android SDK.</span></span>  <span data-ttu-id="334e5-464">변경하려는 이유는 여러 가지입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-464">There are several reasons why you would want to change that:</span></span>

* <span data-ttu-id="334e5-465">시간 제한을 조정하기 위해 대체 HTTP 라이브러리를 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-465">You wish to use an alternate HTTP library to adjust timeouts.</span></span>
* <span data-ttu-id="334e5-466">진행률 표시줄을 제공하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-466">You wish to provide a progress bar.</span></span>
* <span data-ttu-id="334e5-467">API 관리 기능을 지원하기 위해 사용자 지정 헤더를 추가하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-467">You wish to add a custom header to support API management functionality.</span></span>
* <span data-ttu-id="334e5-468">다시 인증을 구현할 수 있도록 실패한 응답을 가로채려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-468">You wish to intercept a failed response so that you can implement reauthentication.</span></span>
* <span data-ttu-id="334e5-469">분석 서비스에 백엔드 요청을 기록하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-469">You wish to log backend requests to an analytics service.</span></span>

### <a name="using-an-alternate-http-library"></a><span data-ttu-id="334e5-470">대체 HTTP 라이브러리 사용</span><span class="sxs-lookup"><span data-stu-id="334e5-470">Using an alternate HTTP Library</span></span>

<span data-ttu-id="334e5-471">클라이언트 참조를 만든 직후 `.setAndroidHttpClientFactory()` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-471">Call the `.setAndroidHttpClientFactory()` method immediately after creating your client reference.</span></span>  <span data-ttu-id="334e5-472">예를 들어 연결 시간 제한을 60초(기본값 10초 대신)로 설정하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-472">For example, to set the connection timeout to 60 seconds (instead of the default 10 seconds):</span></span>

```java
mClient = new MobileServiceClient("https://myappname.azurewebsites.net");
mClient.setAndroidHttpClientFactory(new OkHttpClientFactory() {
    @Override
    public OkHttpClient createOkHttpClient() {
        OkHttpClient client = new OkHttpClinet();
        client.setReadTimeout(60, TimeUnit.SECONDS);
        client.setWriteTimeout(60, TimeUnit.SECONDS);
        return client;
    }
});
```

### <a name="implement-a-progress-filter"></a><span data-ttu-id="334e5-473">진행률 필터 구현</span><span class="sxs-lookup"><span data-stu-id="334e5-473">Implement a Progress Filter</span></span>

<span data-ttu-id="334e5-474">`ServiceFilter`를 구현하여 모든 요청에 대한 가로채기를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-474">You can implement an intercept of every request by implementing a `ServiceFilter`.</span></span>  <span data-ttu-id="334e5-475">예를 들어, 다음은 미리 만든 진행률 표시줄을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-475">For example, the following updates a pre-created progress bar:</span></span>

```java
private class ProgressFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        final SettableFuture<ServiceFilterResponse> resultFuture = SettableFuture.create();
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                if (mProgressBar != null) mProgressBar.setVisibility(ProgressBar.VISIBLE);
            }
        });

        ListenableFuture<ServiceFilterResponse> future = next.onNext(request);
        Futures.addCallback(future, new FutureCallback<ServiceFilterResponse>() {
            @Override
            public void onFailure(Throwable e) {
                resultFuture.setException(e);
            }
            @Override
            public void onSuccess(ServiceFilterResponse response) {
                runOnUiThread(new Runnable() {
                    @Override
                    pubic void run() {
                        if (mProgressBar != null)
                            mProgressBar.setVisibility(ProgressBar.GONE);
                    }
                });
                resultFuture.set(response);
            }
        });
        return resultFuture;
    }
}
```

<span data-ttu-id="334e5-476">다음과 같이 이 필터를 클라이언트에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-476">You can attach this filter to the client as follows:</span></span>

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a><span data-ttu-id="334e5-477">요청 헤더 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="334e5-477">Customize Request Headers</span></span>

<span data-ttu-id="334e5-478">다음 `ServiceFilter`를 사용하고 `ProgressFilter`와 같은 방식으로 필터를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-478">Use the following `ServiceFilter` and attach the filter in the same way as the `ProgressFilter`:</span></span>

```java
private class CustomHeaderFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                request.addHeader("X-APIM-Router", "mobileBackend");
            }
        });
        SettableFuture<ServiceFilterResponse> result = SettableFuture.create();
        try {
            ServiceFilterResponse response = next.onNext(request).get();
            result.set(response);
        } catch (Exception exc) {
            result.setException(exc);
        }
    }
}
```

### <span data-ttu-id="334e5-479"><a name="conversions"></a>자동 직렬화 구성</span><span class="sxs-lookup"><span data-stu-id="334e5-479"><a name="conversions"></a>Configure Automatic Serialization</span></span>

<span data-ttu-id="334e5-480">[gson][3] API를 사용하여 모든 열에 적용되는 변환 전략을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-480">You can specify a conversion strategy that applies to every column by using the [gson][3] API.</span></span> <span data-ttu-id="334e5-481">Android 클라이언트 라이브러리는 배후에서 [gson][3]을 사용하여 Java 개체를 JSON 데이터로 직렬화한 후 Azure App Service로 데이터를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-481">The Android client library uses [gson][3] behind the scenes to serialize Java objects to JSON data before the data is sent to Azure App Service.</span></span>  <span data-ttu-id="334e5-482">다음은 **setFieldNamingStrategy()** 메서드를 사용하여 전략을 설정하는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-482">The following code uses the **setFieldNamingStrategy()** method to set the strategy.</span></span> <span data-ttu-id="334e5-483">이 예에서는 시작 문자("m")를 삭제한 후 각 필드 이름에 대해 다음 문자를 소문자로 처리하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-483">This example will delete the initial character (an "m"), and then lower-case the next character, for every field name.</span></span> <span data-ttu-id="334e5-484">예를 들어 "mId"를 "id"로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-484">For example, it would turn "mId" into "id."</span></span>  <span data-ttu-id="334e5-485">대부분의 필드에서 `SerializedName()` 주석의 필요성을 줄이려면 변환 전략을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-485">Implement a conversion strategy to reduce the need for `SerializedName()` annotations on most fields.</span></span>

```java
FieldNamingStrategy namingStrategy = new FieldNamingStrategy() {
    public String translateName(File field) {
        String name = field.getName();
        return Character.toLowerCase(name.charAt(1)) + name.substring(2);
    }
}

client.setGsonBuilder(
    MobileServiceClient
        .createMobileServiceGsonBuilder()
        .setFieldNamingStrategy(namingStategy)
);
```

<span data-ttu-id="334e5-486">**MobileServiceClient**를 사용하여 모바일 클라이언트 참조를 만들기 전에 이 코드를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="334e5-486">This code must be executed before creating a mobile client reference using the **MobileServiceClient**.</span></span>

<!-- URLs. -->
[Get started with Azure Mobile Apps]: app-service-mobile-android-get-started.md
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[Mobile Services SDK for Android]: http://go.microsoft.com/fwlink/p/?LinkID=717033
[Azure portal]: https://portal.azure.com
<span data-ttu-id="334e5-487">[인증 시작]: app-service-mobile-android-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="334e5-487">[Get started with authentication]: app-service-mobile-android-get-started-users.md</span></span>
[1]: http://google-gson.googlecode.com/svn/trunk/gson/docs/javadocs/com/google/gson/JsonObject.html
[2]: http://hashtagfail.com/post/44606137082/mobile-services-android-serialization-gson
[3]: http://go.microsoft.com/fwlink/p/?LinkId=290801
[4]: http://go.microsoft.com/fwlink/p/?LinkId=296840
[5]: app-service-mobile-android-get-started-push.md
[6]: ../notification-hubs/notification-hubs-push-notification-overview.md#integration-with-app-service-mobile-apps
[7]: app-service-mobile-android-get-started-users.md#cache-tokens
[8]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/table/MobileServiceTable.html
[9]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/MobileServiceClient.html
[10]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[11]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[12]: http://azure.github.io/azure-mobile-apps-android-client/
[13]: app-service-mobile-android-get-started.md#create-a-new-azure-mobile-app-backend
[14]: http://go.microsoft.com/fwlink/p/?LinkID=717034
[15]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[17]: https://developer.android.com/reference/java/util/UUID.html
[18]: https://github.com/google/guava/wiki/ListenableFutureExplained
[19]: http://www.odata.org/documentation/odata-version-3-0/
[20]: http://hashtagfail.com/post/46493261719/mobile-services-android-querying
[21]: https://github.com/Azure-Samples/azure-mobile-apps-android-quickstart
[22]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Future]: http://developer.android.com/reference/java/util/concurrent/Future.html
[AsyncTask]: http://developer.android.com/reference/android/os/AsyncTask.html
