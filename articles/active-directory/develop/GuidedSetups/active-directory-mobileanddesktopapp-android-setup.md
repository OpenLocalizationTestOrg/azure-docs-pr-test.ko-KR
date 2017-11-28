---
title: "Azure AD v2 Android 시작 - 설정 | Microsoft Docs"
description: "Android 앱이 액세스 토큰을 얻고 Azure Active Directory v2 끝점에서 액세스 토큰이 필요한 Microsoft Graph API를 한 개 이상 호출할 수 있는 방법"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: a43d7e30a6f4176afba27f0de2c2c116df741080
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="2a5c4-103">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="2a5c4-103">Set up your project</span></span>

> <span data-ttu-id="2a5c4-104">이 샘플의 Android Studio 프로젝트를 다운로드하고 싶으세요?</span><span class="sxs-lookup"><span data-stu-id="2a5c4-104">Prefer to download this sample's Android Studio project instead?</span></span> <span data-ttu-id="2a5c4-105">[프로젝트를 다운로드](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip)하면 실행 전 코드 샘플을 구성하는 [구성 단계](#create-an-application-express)로 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a5c4-105">[Download a project](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) and skip to the [Configuration step](#create-an-application-express) to configure the code sample before executing    .</span></span>


### <a name="create-a-new-project"></a><span data-ttu-id="2a5c4-106">새 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="2a5c4-106">Create a new project</span></span> 
1.  <span data-ttu-id="2a5c4-107">Android Studio를 열고 `File` > `New` > `New Project`로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2a5c4-107">Open Android Studio, go to: `File` > `New` > `New Project`</span></span>
2.  <span data-ttu-id="2a5c4-108">응용 프로그램의 이름을 지정하고 `Next`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a5c4-108">Name your application and click `Next`</span></span>
3.  <span data-ttu-id="2a5c4-109">*API 21 이상(Android 5.0)*이 선택되어 있는지 확인하고 `Next`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a5c4-109">Make sure to select *API 21 or newer (Android 5.0)* and click `Next`</span></span>
4.  <span data-ttu-id="2a5c4-110">`Empty Activity`는 그대로 두고 `Next`을 클릭한 후 `Finish`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a5c4-110">Leave `Empty Activity`, click `Next`, then `Finish`</span></span>


### <a name="add-the-microsoft-authentication-library-msal-to-your-project"></a><span data-ttu-id="2a5c4-111">프로젝트에 MSAL(Microsoft 인증 라이브러리) 추가</span><span class="sxs-lookup"><span data-stu-id="2a5c4-111">Add the Microsoft Authentication Library (MSAL) to your project</span></span>
1.  <span data-ttu-id="2a5c4-112">Android Studio에서 `Gradle Scripts` > `build.gradle (Module: app)`으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2a5c4-112">In Android Studio, go to: `Gradle Scripts` > `build.gradle (Module: app)`</span></span>
2.  <span data-ttu-id="2a5c4-113">`Dependencies`아래에 다음 코드를 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2a5c4-113">Copy and paste the following code under `Dependencies`:</span></span>

```ruby  
compile ('com.microsoft.identity.client:msal:0.1.+') {
    exclude group: 'com.android.support', module: 'appcompat-v7'
}
compile 'com.android.volley:volley:1.0.0'
```

<!--start-collapse-->
### <a name="about-this-package"></a><span data-ttu-id="2a5c4-114">이 패키지 정보</span><span class="sxs-lookup"><span data-stu-id="2a5c4-114">About this package</span></span>

<span data-ttu-id="2a5c4-115">위의 패키지는 MSAL(Microsoft 인증 라이브러리)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2a5c4-115">The package above installs the Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="2a5c4-116">MSAL은 Azure Active Directory v2 끝점으로 보호되는 API에 액세스하는 데 사용되는 사용자 토큰의 획득, 캐싱 및 새로 고침을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="2a5c4-116">MSAL handles acquiring, caching and refreshing user tokens used to access APIs protected by Azure Active Directory v2 endpoint.</span></span>
<!--end-collapse-->

## <a name="create-your-applications-ui"></a><span data-ttu-id="2a5c4-117">응용 프로그램 UI 만들기</span><span class="sxs-lookup"><span data-stu-id="2a5c4-117">Create your application’s UI</span></span>

1.  <span data-ttu-id="2a5c4-118">`res` > `layout`에서 `activity_main.xml`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2a5c4-118">Open: `activity_main.xml` under `res` > `layout`</span></span>
2.  <span data-ttu-id="2a5c4-119">`android.support.constraint.ConstraintLayout` 등에서 `LinearLayout`으로 작업 레이아웃을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="2a5c4-119">Change the activity layout from `android.support.constraint.ConstraintLayout` or other to `LinearLayout`</span></span>
3.  <span data-ttu-id="2a5c4-120">`LinearLayout` 노드에 `android:orientation="vertical"` 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2a5c4-120">Add `android:orientation="vertical"` property to `LinearLayout` node</span></span>
4.  <span data-ttu-id="2a5c4-121">다음 코드를 복사하여 `LinearLayout` 노드에 붙여넣어 현재 내용을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2a5c4-121">Copy and paste the following code into the `LinearLayout` node, replacing the current content:</span></span>

```xml
<TextView
    android:text="Welcome, "
    android:textColor="#3f3f3f"
    android:textSize="50px"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_marginLeft="10dp"
    android:layout_marginTop="15dp"
    android:id="@+id/welcome"
    android:visibility="invisible"/>

<Button
    android:id="@+id/callGraph"
    android:text="Call Microsoft Graph"
    android:textColor="#FFFFFF"
    android:background="#00a1f1"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginTop="200dp"
    android:textAllCaps="false" />

<TextView
    android:text="Getting Graph Data..."
    android:textColor="#3f3f3f"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginLeft="5dp"
    android:id="@+id/graphData"
    android:visibility="invisible"/>

<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="0dip"
    android:layout_weight="1"
    android:gravity="center|bottom"
    android:orientation="vertical" >

    <Button
        android:text="Sign Out"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="15dp"
        android:textColor="#FFFFFF"
        android:background="#00a1f1"
        android:textAllCaps="false"
        android:id="@+id/clearCache"
        android:visibility="invisible" />
</LinearLayout>
```

