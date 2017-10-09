---
title: "AD aaaAzure v2 Android 시작-설치 | Microsoft Docs"
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
ms.openlocfilehash: df2670d6d35b7a9a81158d4d7eb190540ca9c695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="950a5-103">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="950a5-103">Set up your project</span></span>

> <span data-ttu-id="950a5-104">Toodownload이이 샘플의 Android Studio 프로젝트를 대신 선호?</span><span class="sxs-lookup"><span data-stu-id="950a5-104">Prefer toodownload this sample's Android Studio project instead?</span></span> <span data-ttu-id="950a5-105">[프로젝트를 다운로드](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) toohello 건너뛸 [구성 단계](#create-an-application-express) tooconfigure hello 코드 샘플을 실행 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="950a5-105">[Download a project](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing    .</span></span>


### <a name="create-a-new-project"></a><span data-ttu-id="950a5-106">새 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="950a5-106">Create a new project</span></span> 
1.  <span data-ttu-id="950a5-107">Android Studio를 열고 `File` > `New` > `New Project`로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="950a5-107">Open Android Studio, go to: `File` > `New` > `New Project`</span></span>
2.  <span data-ttu-id="950a5-108">응용 프로그램의 이름을 지정하고 `Next`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="950a5-108">Name your application and click `Next`</span></span>
3.  <span data-ttu-id="950a5-109">있는지 tooselect 확인 *API 21 또는 최신 (Android 5.0)* 클릭`Next`</span><span class="sxs-lookup"><span data-stu-id="950a5-109">Make sure tooselect *API 21 or newer (Android 5.0)* and click `Next`</span></span>
4.  <span data-ttu-id="950a5-110">`Empty Activity`는 그대로 두고 `Next`을 클릭한 후 `Finish`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="950a5-110">Leave `Empty Activity`, click `Next`, then `Finish`</span></span>


### <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a><span data-ttu-id="950a5-111">Hello Microsoft 인증 라이브러리 (MSAL) tooyour 프로젝트 추가</span><span class="sxs-lookup"><span data-stu-id="950a5-111">Add hello Microsoft Authentication Library (MSAL) tooyour project</span></span>
1.  <span data-ttu-id="950a5-112">Android Studio에서 `Gradle Scripts` > `build.gradle (Module: app)`으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="950a5-112">In Android Studio, go to: `Gradle Scripts` > `build.gradle (Module: app)`</span></span>
2.  <span data-ttu-id="950a5-113">아래 코드를 복사 및 붙여넣기 hello 다음 `Dependencies`:</span><span class="sxs-lookup"><span data-stu-id="950a5-113">Copy and paste hello following code under `Dependencies`:</span></span>

```ruby  
compile ('com.microsoft.identity.client:msal:0.1.+') {
    exclude group: 'com.android.support', module: 'appcompat-v7'
}
compile 'com.android.volley:volley:1.0.0'
```

<!--start-collapse-->
### <a name="about-this-package"></a><span data-ttu-id="950a5-114">이 패키지 정보</span><span class="sxs-lookup"><span data-stu-id="950a5-114">About this package</span></span>

<span data-ttu-id="950a5-115">위의 hello 패키지는 hello Microsoft 인증 라이브러리 (MSAL)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="950a5-115">hello package above installs hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="950a5-116">MSAL 가져오는, 캐싱 및 사용자 토큰 tooaccess Azure Active Directory v2 끝점에 의해 보호 되는 Api를 새로 고침을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="950a5-116">MSAL handles acquiring, caching and refreshing user tokens used tooaccess APIs protected by Azure Active Directory v2 endpoint.</span></span>
<!--end-collapse-->

## <a name="create-your-applications-ui"></a><span data-ttu-id="950a5-117">응용 프로그램 UI 만들기</span><span class="sxs-lookup"><span data-stu-id="950a5-117">Create your application’s UI</span></span>

1.  <span data-ttu-id="950a5-118">`res` > `layout`에서 `activity_main.xml`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="950a5-118">Open: `activity_main.xml` under `res` > `layout`</span></span>
2.  <span data-ttu-id="950a5-119">사용 되는 hello 활동 레이아웃 변경 `android.support.constraint.ConstraintLayout` 또는 기타 너무`LinearLayout`</span><span class="sxs-lookup"><span data-stu-id="950a5-119">Change hello activity layout from `android.support.constraint.ConstraintLayout` or other too`LinearLayout`</span></span>
3.  <span data-ttu-id="950a5-120">추가 `android:orientation="vertical"` 속성 너무`LinearLayout` 노드</span><span class="sxs-lookup"><span data-stu-id="950a5-120">Add `android:orientation="vertical"` property too`LinearLayout` node</span></span>
4.  <span data-ttu-id="950a5-121">복사 및 붙여넣기 hello 다음 hello에 코딩할 `LinearLayout` 노드를 hello 현재 콘텐츠를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="950a5-121">Copy and paste hello following code into hello `LinearLayout` node, replacing hello current content:</span></span>

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

