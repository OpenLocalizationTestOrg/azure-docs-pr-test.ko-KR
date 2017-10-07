---
title: "Android 용 Azure 모바일 앱 SDK aaaHow toouse hello | Microsoft Docs"
description: "Toouse는 Android 용 Azure 모바일 앱 SDK를 hello 하는 방법"
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
ms.openlocfilehash: 56eb73c4e1703d69877be499a09fc2130f1d68e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-sdk-for-android"></a>Toouse는 Android 용 Azure 모바일 앱 SDK를 hello 하는 방법

이 가이드에서는 어떻게 toouse hello 모바일 앱 tooimplement 일반적인 시나리오에 대 한 Android 클라이언트 SDK와 같은 보여 줍니다.

* 데이터 쿼리(삽입, 업데이트 및 삭제).
* 인증.
* 오류 처리.
* 클라이언트 hello에 사용자 지정합니다.

이 가이드는 hello 클라이언트 쪽 Android SDK에 중점을 둡니다.  모바일 앱에 대 한 서버 쪽 Sdk hello, 참조에 대해 더 알아봅니다 toolearn [.NET 백 엔드 SDK 작업할] [ 10] 또는 [어떻게 toouse hello Node.js 백 엔드 SDK] [ 11].

## <a name="reference-documentation"></a>참조 설명서

Hello를 찾을 수 있습니다 [Javadocs API 참조] [ 12] hello Android 클라이언트 라이브러리 GitHub에 대 한 합니다.

## <a name="supported-platforms"></a>지원되는 플랫폼

Android 용 Azure 모바일 앱 SDK hello 전화 및 태블릿 폼 팩터 용 API 수준 19-24 (Nougat 통해 KitKat)를 지원합니다.  특히, 인증는 일반적인 웹 프레임 워크 접근 방식을 toogather 자격 증명을 활용합니다.  서버 흐름 인증은 시계와 같은 소형 폼 팩터 장치에서는 작동하지 않습니다.

## <a name="setup-and-prerequisites"></a>설정 및 필수 조건

전체 hello [모바일 앱 빠른 시작](app-service-mobile-android-get-started.md) 자습서입니다.  자습서를 통해 Azure Mobile Apps를 개발하기 위한 모든 필수 구성 요소를 충족할 수 있습니다.  hello 퀵 스타트도를 사용 하면 계정을 구성 하 고 첫 번째 모바일 앱 백 엔드를 만듭니다.

Toocomplete hello 빠른 시작 자습서 하지 않으려면 hello 다음 작업을 완료 합니다.

* [모바일 앱 백 엔드 만들기] [ 13] toouse Android 앱과 함께 합니다.
* Android Studio에서 [업데이트 hello Gradle 빌드 파일](#gradle-build)합니다.
* [인터넷 권한을 사용합니다](#enable-internet).

### <a name="gradle-build"></a>Hello Gradle 빌드 파일을 업데이트 합니다.

**build.gradle** 파일을 모두 변경합니다.

1. 이 코드 toohello 추가 *프로젝트* 수준 **의 build.gradle** hello 내 파일 *buildscript* 태그:

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. 이 코드 toohello 추가 *모듈 앱* 수준 **의 build.gradle** hello 내 파일 *종속성* 태그:

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    현재 hello 최신 버전은 3.3.0입니다. hello 지원 버전은 목록 [bintray에][14]합니다.

### <a name="enable-internet"></a>인터넷 권한 사용

Azure tooaccess 앱 hello 인터넷 사용 권한을 사용할 수 있어야 합니다. 사용 되지 않는 경우 다음 줄의 코드 tooyour hello 추가 **AndroidManifest.xml** 파일:

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a>클라이언트 연결 만들기

Azure 모바일 앱에서는 네 가지 기능 tooyour 모바일 응용 프로그램을 제공합니다.

* Azure Mobile Apps Service를 통한 데이터 액세스 및 오프라인 동기화.
* Hello Azure 모바일 앱 서버 SDK로 작성 된 사용자 지정 Api를 호출 합니다.
* Azure App Service 인증 및 권한 부여를 통한 인증.
* Notification Hubs를 통한 푸시 알림 등록.

이러한 각각의 함수는 먼저 `MobileServiceClient` 개체를 생성해야 합니다.  모바일 클라이언트 내에 하나의 `MobileServiceClient` 개체만 만들어야 합니다(즉 Singleton 패턴이어야 합니다).  toocreate는 `MobileServiceClient` 개체:

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with hello Site URL
    this);                  // Your application Context
```

hello `<MobileAppUrl>` 는 문자열 이거나 tooyour 모바일 백 엔드를 가리키는 URL 개체입니다.  Azure 앱 서비스 toohost 모바일 백 엔드를 사용할 경우의 보안 hello를 사용 하 여 확인 합니다 `https://` hello URL의 버전입니다.

클라이언트 hello 해야 작업 또는 상황에 맞는-액세스 toohello hello `this` hello 예제에서 매개 변수입니다.  MobileServiceClient 생성 hello hello 내에서 동작 `onCreate()` hello hello에서 참조 되는 활동의 메서드가 `AndroidManifest.xml` 파일입니다.

가장 좋은 방법은 서버 통신을 자체(singleton 패턴) 클래스로 추상화하는 것입니다.  이 경우 전달 해야 hello 생성자 tooappropriately 내에서 활동 hello hello 서비스를 구성 합니다.  예:

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

이제 호출할 수 있습니다 `AzureServiceAdapter.Initialize(this);` hello에 `onCreate()` 주 활동이 메서드.  Toohello 클라이언트 액세스를 필요로 하는 다른 모든 메서드를 사용 하 여 `AzureServiceAdapter.getInstance();` tooobtain 참조 toohello 서비스 어댑터입니다.

## <a name="data-operations"></a>데이터 작업

hello Azure 모바일 앱 SDK의 hello 핵심은 tooprovide 액세스 toodata hello 모바일 앱 백 엔드에 SQL Azure 내에 저장 합니다.  이러한 데이터는 강력한 형식의 클래스(권장됨) 또는 형식화되지 않은 쿼리(권장하지 않음)를 사용하여 액세스할 수 있습니다.  이 섹션의 hello 대량 강력한 형식의 클래스를 사용 하 여 처리 합니다.

### <a name="define-client-data-classes"></a>클라이언트 데이터 클래스 정의

tooaccess 테이블의에서 데이터를 SQL Azure toohello 테이블 hello 모바일 앱 백엔드에 해당 하는 클라이언트 데이터 클래스를 정의 합니다. 이 항목의 예제 가정 라는 테이블 **MyDataTable**, hello 열 뒤에 있는:

* id
* text
* complete

hello 해당 형식화 된 클라이언트 개체가 있는 라는 파일에 **MyDataTable.java**:

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

추가하는 각 필드에 getter 및 setter 메서드를 추가합니다.  SQL Azure 테이블에 더 많은 열이 있으면 hello 해당 필드 toothis 클래스를 추가 합니다.  예를 들어 경우 hello, DTO (데이터 전송 개체)가 정수 우선 순위 열 다음의 getter 및 setter 메서드와이 필드를 추가할 수 있습니다.

```java
private Integer priority;

/**
* Returns hello item priority
*/
public Integer getPriority() {
    return mPriority;
}

/**
* Sets hello item priority
*
* @param priority
*            priority tooset
*/
public final void setPriority(Integer priority) {
    mPriority = priority;
}
```

모바일 앱 백 엔드에 추가 테이블 toocreate 참조 toolearn [하는 방법: 테이블 컨트롤러 정의] [ 15] (.NET 백 엔드) 또는 [동적 스키마를 사용 하 여 정의 테이블] [ 16] (Node.js 백 엔드).

Azure 모바일 앱 백 엔드 테이블에는 4 개는 사용 가능한 tooclients 특수 필드 다섯 개가 정의 합니다.

* `String id`: hello hello 레코드에 대 한 전역적으로 고유 ID입니다.  모범 사례로,의 hello id hello 문자열 표현을 확인는 [UUID] [ 17] 개체입니다.
* `DateTimeOffset updatedAt`: hello의 hello 마지막 업데이트 날짜/시간입니다.  hello updatedAt 필드 hello 서버에 의해 설정 되 고 클라이언트 코드에서 설정할 수 없습니다.
* `DateTimeOffset createdAt`: hello 날짜/시간 hello 개체를 생성 합니다.  hello createdAt 필드 hello 서버에 의해 설정 되 고 클라이언트 코드에서 설정할 수 없습니다.
* `byte[] version`: 일반적으로 문자열로 표현, hello 버전도 설정 됩니다 hello 서버.
* `boolean deleted`: Hello 레코드 삭제 되었지만 아직 제거 되지 있는지 나타냅니다.  `deleted`를 클래스에서 속성으로 사용하지 마십시오.

hello `id` 필드는 필수입니다.  hello `updatedAt` 필드 및 `version` 필드 오프 라인 동기화에 사용 됩니다 (증분 동기화 및 충돌 해결을 위해 각각).  hello `createdAt` 필드가 참조 필드 이며 hello 클라이언트에서 사용 되지 않습니다.  hello 이름은 hello 속성의 이름을 "간에 실시간"를 조정할 수 있지만 되지 않습니다.  그러나 이름을 만들 수 있습니다 개체와 hello 간의 매핑을 "간에 실시간" hello를 사용 하 여 [gson] [ 3] 라이브러리입니다.  예:

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

### <a name="create-a-table-reference"></a>테이블 참조 만들기

tooaccess 테이블을 먼저 만듭니다는 [MobileServiceTable] [ 8] 호출 hello 개체 **getTable** 메서드 hello [MobileServiceClient][9].  이 메서드에는 두 가지 오버로드가 있습니다.

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

코드를 다음 hello에 **mClient** 은 참조 tooyour MobileServiceClient 개체입니다.  hello 첫 번째 오버 로드는 hello 클래스 이름 및 hello 테이블 이름이 있는 hello 동일 하며 hello 하나에 사용 됩니다 hello 빠른 시작 사용 됩니다.

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

hello 두 번째 오버 로드 될 때 사용 되 hello 테이블 이름이 hello 클래스 이름에서 다른: hello 첫 번째 매개 변수는 hello 테이블 이름입니다.

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <a name="query"></a> 엔드 테이블 쿼리

먼저 테이블 참조를 가져옵니다.  Hello 테이블 참조에 대해 쿼리를 실행 합니다.  쿼리는 다음의 조합입니다.

* `.where()` [필터 절](#filtering).
* `.orderBy()` [ordering 절](#sorting).
* `.select()` [필드 선택 절](#selection).
* [페이징 결과](#paging)에 대한 `.skip()` 및 `.top()`.

hello 절 앞에 순서 hello에 제공 해야 합니다.

### <a name="filter"></a> 결과 필터링

쿼리의 hello 일반 형식은 다음과 같습니다.

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts hello async into a sync result
```

hello 앞의 예제 모든 결과 반환 (위쪽 hello 서버에서 설정한 toohello 최대 페이지 크기).  hello `.execute()` 메서드 hello 백 엔드에서 hello 쿼리를 실행 합니다.  hello 쿼리는 변환 된 tooan [OData v3] [ 19] 전송 toohello 모바일 앱 백 엔드 전에 쿼리 합니다.  수신 했을 때 hello 모바일 앱 백 엔드는 hello 쿼리 hello SQL Azure 인스턴스에 대해 실행 하기 전에 SQL 문으로 변환 합니다.  네트워크 작업에 약간의 시간이 걸리므로 hello `.execute()` 메서드가 반환 되는 [ `ListenableFuture<E>` ] [ 18]합니다.

### <a name="filtering"></a>반환된 데이터 필터링

hello에서 모든 항목을 반환 하는 다음 쿼리를 실행 하는 hello **ToDoItem** 테이블 **완료** equals **false**합니다.

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

**mToDoTable** hello 참조 toohello 모바일 서비스 테이블 이전에 만든 것입니다.

Hello를 사용 하 여 필터를 정의 **여기서** hello 테이블 참조에 대해 메서드를 호출 합니다. hello **여기서** 메서드 뒤는 **필드** 메서드 뒤 hello 논리 조건자를 지정 하는 메서드입니다. 가능한 조건자 메서드에는 **eq**(같음), **ne**(같지 않음), **gt**(보다 큼), **ge**(보다 크거나 같음), **lt**(보다 작음), **le**(작거나 같음)가 포함됩니다. 이러한 메서드 번호를 비교 하 고 문자열 toospecific 값 필드입니다.

날짜를 기준으로 필터링할 수 있습니다. hello 다음 메서드를 통해 hello 날짜의 일부 또는 전체 hello 전체 날짜 필드를 비교할 수: **연도**, **월**, **일**, **시간**, **분**, 및 **두 번째**합니다. hello 다음 예제에서는 추가 항목에 대 한 필터 인 *기한* 2013 같음.

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

hello 다음 메서드 지원 복잡 한 필터 문자열 필드에: **startsWith**, **endsWith**, **concat**, **부분 문자열**, **indexOf**, **대체**, **toLower**, **toUpper**, **trim**, 및  **길이**합니다. 여기서 hello 테이블 행에 대 한 예에서는 필터를 다음 hello *텍스트* "PRI0"로 시작 열

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

hello 연산자 메서드를 다음 숫자 필드에 지원 됩니다: **추가**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, 및 **반올림**합니다. 여기서 hello 테이블 행에 대 한 예에서는 필터를 다음 hello **기간** 짝수입니다.

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

조건자를 **and**, **or**, **not** 등의 논리 메서드와 결합할 수 있습니다. 다음 예제는 hello hello 예 앞의 두 결합 합니다.

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

그룹 및 중첩 논리 연산자:

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

자세한 설명과 필터링의 예제를 참조 하세요. [hello Android 클라이언트 쿼리 모델의 hello 세부 탐색][20]합니다.

### <a name="sorting"></a>반환된 데이터 정렬

hello 다음 코드를 반환 모든 항목의 테이블에서 **ToDoItems** hello로 오름차순으로 정렬 *텍스트* 필드입니다. *mToDoTable* hello 참조 toohello 백 엔드 테이블 이전에 만든입니다.

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

hello의 첫 번째 매개 변수를 hello **orderBy** 방법은의 어떤 toosort hello 필드 문자열 같은 toohello 이름입니다. hello를 사용 하는 hello 두 번째 매개 변수 **QueryOrder** 열거형 toospecify 있는지 여부를 오름차순 또는 내림차순 toosort 합니다.  Hello를 사용 하 여 필터링 하는 경우 ***여기서*** 메서드, hello ***여기서*** hello 하기 전에 메서드를 호출 해야 ***orderBy*** 메서드.

### <a name="selection"></a>특정 열 선택

hello 다음 코드에서는 모든 tooreturn 목차에서 항목을 어떻게 **ToDoItems**만 hello를 표시 하지만 **완료** 및 **텍스트** 필드입니다. **mToDoTable** hello 참조 toohello 백 엔드 테이블 이전에 만든 것입니다.

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

hello 매개 변수 toohello 함수 선택은 hello 문자열 이름 tooreturn hello 테이블의 열입니다.  hello **선택** 메서드에 필요한 같은 toofollow 메서드 **여기서** 및 **orderBy**합니다. 그 뒤에 **skip** 및 **top**등의 메서드를 페이징하여 나올 수 있습니다.

### <a name="paging"></a>페이지에 데이터 반환

데이터는 **항상** 페이지에 반환됩니다.  반환 된 레코드의 최대 수 hello hello 서버에 의해 설정 됩니다.  Hello 클라이언트가 더 많은 레코드를 요청 하는 경우 hello 서버 hello 최대 레코드 수를 반환 합니다.  기본적으로 hello 서버의 hello 최대 페이지 크기는 50입니다.

첫 번째 예에서는 hello tooselect 테이블에서 상위 5 개 항목을 hello 하는 방법을 보여 줍니다. 목차에서 hello 항목을 반환 하는 hello 쿼리 **ToDoItems**합니다. **mToDoTable** hello 참조 toohello 백 엔드 테이블 이전에 만든입니다.

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

건너뜁니다 처음 5 개 항목 hello 및 반환의 다음 5 hello 다음 쿼리는 다음과 같습니다.

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

원할 경우 tooget 모든 레코드는 테이블의 모든 페이지를 통해 코드 tooiterate 구현.

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

이 메서드를 사용 하 여 모든 레코드에 대 한 요청에는 위의 두 요청 toohello 모바일 앱 백 엔드 최소를 만듭니다.

> [!TIP]
> 선택 hello 오른쪽 페이지 크기는 hello 요청이 수행 되는 동안 메모리 사용량, 대역폭 사용량 및 hello 데이터를 완전히 수신 지연 간의 균형입니다.  hello 기본값 (50 개의 레코드)은 모든 장치에 적합 합니다.  단독으로 더 큰 메모리 장치에서 운영 하는 경우 too500를 늘립니다.  결과 500 기록 초과 증가 hello 페이지 크기에 허용 되지 않는 지연 및 대용량 메모리 문제 발견 했습니다.

### <a name="chaining"></a>방법: 쿼리 메서드 연결

hello 메소드 백 엔드 테이블을 쿼리 하는 연결할 수 있습니다. 메서드를 정렬 하 고 페이징 하는 필터링 된 행의 tooselect 특정 열을 사용 하면 쿼리를 연결 합니다. 상당히 복잡한 논리 필터를 만들 수 있습니다.  각 쿼리 메서드는 쿼리 개체를 반환합니다. tooend hello 일련의 메서드 및 쿼리 실행된 실제로 hello 호출 hello **실행** 메서드. 예:

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

hello 연결 쿼리 메서드를 다음과 같이 정렬 되어야 합니다.

1. 필터링(**where**) 메서드.
2. 정렬(**orderBy**) 메서드.
3. 선택(**select**) 메서드.
4. 페이징(**skip** 및 **top**) 메서드.

## <a name="binding"></a>바인딩할 데이터 toohello 사용자 인터페이스

데이터 바인딩에는 세 가지 구성 요소가 필요합니다.

* hello 데이터 원본
* hello 화면 레이아웃
* hello 어댑터는 ties hello 두 함께입니다.

이 샘플 코드에서 hello 모바일 앱 SQL Azure 테이블에서 hello 데이터 반환 **ToDoItem** 를 배열에 있습니다. 이 활동은 데이터 응용 프로그램에서 매우 흔한 패턴입니다.  데이터베이스 쿼리는 종종 hello 가져옵니다 목록 또는 배열에서 행의 컬렉션을 반환 합니다. 이 샘플에서는 hello 배열이 hello 데이터 원본입니다.  hello 코드 hello 장치에 표시 되는 hello 데이터의 hello 뷰를 정의 하는 화면 레이아웃을 지정 합니다.  hello 두 바인딩된 hello의 확장은이 코드는 어댑터를 함께 **ArrayAdapter&lt;ToDoItem&gt;**  클래스입니다.

#### <a name="layout"></a>Hello 레이아웃을 정의 합니다.

hello 레이아웃 XML 코드의 여러 조각으로 정의 됩니다. 기존 레이아웃 들어 hello 코드 다음 나타내는 hello **ListView** 서버 마찬가지 toopopulate 주시기 바랍니다.

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

Hello 코드 앞에에서 hello *listitem* 특성 hello 목록에서 개별 행에 대 한 hello 레이아웃의 hello id를 지정 합니다. 이 코드는 확인란 및 해당 관련 된 텍스트를 지정 하 고 hello 목록의 각 항목에 대해 한 번씩 인스턴스화됩니다. 이 레이아웃 hello를 표시 하지 않습니다 **id** 필드를 사용 하 고 더 복잡 한 레이아웃은 hello 디스플레이에 추가 필드를 지정 합니다. 이 코드는 hello에 **row_list_to_do.xml** 파일입니다.

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

#### <a name="adapter"></a>Hello 어댑터 정의
이 뷰의 데이터 원본 hello 배열을 이므로 **ToDoItem**, 우리 하위 클래스에서 어댑터는 **ArrayAdapter&lt;ToDoItem&gt;**  클래스입니다. 이 하위 클래스에 대 한 뷰를 생성 합니다. 모든 **ToDoItem** hello를 사용 하 여 **row_list_to_do** 레이아웃 합니다.  이 코드의 hello 확장 클래스를 다음 hello 정의 **ArrayAdapter&lt;E&gt;**  클래스:

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

Hello 어댑터 재정의 **영역의 getView** 메서드. 예:

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

작업에서 다음과 같이 이 클래스의 인스턴스를 만듭니다.

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

hello 두 번째 매개 변수 toohello ToDoItemAdapter 생성자는 참조 toohello 레이아웃입니다. 에서는 이제 hello를 인스턴스화할 수 **ListView** hello 어댑터 toohello 할당 **ListView**합니다.

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <a name="use-adapter"></a>Hello 어댑터 tooBind toohello UI를 사용 하 여

데이터 바인딩 준비 toouse가 나타납니다. hello 다음 코드에서는 hello 테이블 및 채우기의 tooget 항목 로컬 어댑터 항목을 반환 하는 hello로 hello 하는 방법

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

Hello 어댑터 hello를 수정 하면 언제 든 지 호출 **ToDoItem** 테이블입니다. 수정은 레코드별로 이루어지기 때문에 사용자는 컬렉션이 아닌 단일 행을 다루게 됩니다. 항목을 삽입 하면 호출 hello **추가** 메서드 어댑터 hello 않으면 삭제 하는 경우 호출 hello **제거** 메서드.

전체 예제는 hello에서 찾을 수 [Android 퀵 스타트 프로젝트][21]합니다.

## <a name="inserting"></a>Hello 백 엔드에 데이터 삽입

Hello의 인스턴스를 인스턴스화하고 *ToDoItem* 클래스 및 해당 속성을 설정 합니다.

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

다음 사용 하 여 **했** tooinsert 개체:

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

반환 된 엔터티 일치 hello 백 엔드 테이블 포함된 hello ID와 다른 값을 삽입 하는 hello 데이터 hello (hello 같은 `createdAt`, `updatedAt`, 및 `version` 필드) hello 백 엔드에 설정 합니다.

Mobile Apps 테이블에는 **id**라고 하는 기본 키 열이 필요합니다. 이 열은 문자열이어야 합니다. hello ID 열의 기본값이 hello는 GUID입니다.  전자 메일 주소나 사용자 이름처럼 다른 고유한 값을 입력해도 됩니다. 삽입 된 레코드에 대 한 문자열 ID 값을 제공 하지는 hello 백 엔드 새 GUID를 생성 합니다.

Hello 장점 다음 제공 된 문자열 ID 값:

* 왕복 toohello 데이터베이스를 만들지 않고 Id는 생성할 수 있습니다.
* 레코드는 서로 다른 테이블 또는 데이터베이스에서 보다 쉽게 toomerge 합니다.
* 응용 프로그램의 논리를 통해 ID 값이 더 효율적으로 통합됩니다.

오프라인 동기화를 지원하려면 문자열 ID 값이 **필수** 입니다.  Hello 백 엔드 데이터베이스에 저장 되 면 Id를 변경할 수 없습니다.

## <a name="updating"></a>모바일 앱의 데이터 업데이트

테이블의 tooupdate 데이터 전달 hello 새 개체 toohello **update ()** 메서드.

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

이 예제에서는 *항목* hello에 참조 tooa 행이 *ToDoItem* 일부 변경 내용을 tooit 기능이 있는 테이블입니다.  동일한 hello로 hello 행 **id** 업데이트 됩니다.

## <a name="deleting"></a>모바일 앱의 데이터 삭제

코드 다음 hello toodelete 테이블의에서 데이터를 지정 하 여 데이터 개체를 hello 하는 방법을 보여 줍니다.

```java
mToDoTable
    .delete(item);
```

Hello를 지정 하 여 항목을 삭제할 수도 **id** hello 행 toodelete 필드입니다.

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <a name="lookup"></a>ID로 특정 항목 조회

특정 항목을 조회 **id** hello로 필드 **lookUp()** 메서드:

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <a name="untyped"></a>방법: 형식화되지 않은 데이터 작업

hello 형식화 되지 않은 프로그래밍 모델에는 JSON serialization 통해 정확 하 게 제어할 수 있습니다.  Toouse는 형식화 되지 않은 프로그래밍 모델을 사용할 수 있는 몇 가지 일반적인 시나리오가 있습니다. 예를 들어 백 엔드 테이블에 많은 열이 포함 되어 있고 tooreference hello 열의 하위 집합에 하기만 합니다.  hello 형식화 된 모델 toodefine hello 모바일 앱 백 엔드에서 데이터 클래스의 모든 hello 열은 정의 해야 합니다.  대부분의 데이터에 액세스 하기 위한 API를 호출 하는 hello 비슷합니다 toohello 프로그래밍 호출을 입력 합니다. hello 중요 한 차이점은 hello 형식화 되지 않은 모델에 hello에 대 한 메서드 호출 **MobileServiceJsonTable** hello 대신 개체 **MobileServiceTable** 개체입니다.

### <a name="json_instance"></a>형식화되지 않은 테이블 인스턴스 만들기

비슷한 toohello 입력 모델, 테이블 참조를 가져와서 시작 하 게 되지만 경우에 한 **MobileServicesJsonTable** 개체입니다. Hello를 호출 하 여 hello 참조를 가져올 **getTable** hello 클라이언트의 인스턴스 메서드:

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

Hello의 인스턴스를 만든 후 **MobileServiceJsonTable**, hello 형식화 된 프로그래밍 모델을 사용으로 사용할 수 있는 동일한 API를 hello 거의 했습니다. 일부 경우 hello 메서드는 형식화 된 매개 변수 대신는 형식화 되지 않은 매개 변수를 사용 합니다.

### <a name="json_insert"></a>형식화되지 않은 테이블에 삽입
코드에서 보여 주는 방법을 다음 hello toodo 삽입 합니다. hello 첫 번째 단계는 toocreate는 [JsonObject][1], hello에 포함 되어 있는 [gson] [ 3] 라이브러리입니다.

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

다음을 사용 하 여 **했** hello 테이블로 tooinsert hello 형식화 되지 않은 개체입니다.

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

Hello를 사용 하 여 hello 삽입 개체의 tooget hello ID 해야 할 경우 **getAsJsonPrimitive()** 메서드.

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <a name="json_delete"></a>형식화되지 않은 테이블에서 삭제
hello 다음 코드를 보여 줍니다 toodelete 인스턴스를 동일한 인스턴스를이 경우 hello 어떻게는 **JsonObject** hello 이전에 만들어진 *삽입* 예제입니다. hello 코드는 hello 경우 입력 한 hello와 같음 되었지만 hello 메서드를 다른 서명 참조 하므로 한 **JsonObject**합니다.

```java
mToDoTable
    .delete(insertedItem);
```

ID를 사용하여 직접 인스턴스를 삭제할 수도 있습니다.

```java
mToDoTable.delete(ID);
```

### <a name="json_get"></a>형식화되지 않은 테이블에서 모든 행 반환
코드에서 보여 주는 방법을 다음 hello tooretrieve 전체 테이블입니다. JSON 테이블을 사용 하는 후 선택적으로 hello 테이블의 열 중 일부만 검색할 수 있습니다.

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

hello 동일한 필터링, 필터링 및 페이징을 hello 형식화 된 모델에 사용할 수 있는 메서드는 hello 형식화 되지 않은 모델에 사용할 수 있습니다.

## <a name="offline-sync"></a>오프라인 동기화 구현

또한 Azure 모바일 앱 클라이언트 SDK hello SQLite 데이터베이스 toostore hello 서버 데이터의 복사본을 로컬에서 사용 하 여 데이터의 오프 라인 동기화를 구현 합니다.  오프 라인 테이블에서 수행 된 작업에는 모바일 연결 toowork가 필요 하지 않습니다.  복원 력 및 충돌 해결을 위해 더 복잡 한 논리의 hello 부담 성능에 오프 라인 동기화 유용 합니다.  Azure 모바일 앱 클라이언트 SDK hello hello 같은 기능을 구현 합니다.

* 증분 동기화: 업데이트된 레코드와 새 레코드 만 다운로드되기 때문에 대역폭과 메모리 사용량이 절약됩니다.
* 낙관적 동시성: 작업 toosucceed를 간주 됩니다.  충돌 해결 업데이트 hello 서버에서 수행 될 때까지 지연 됩니다.
* 충돌 해결 방법: tooalert hello 사용자를 연결 하는 hello SDK 충돌을 일으키는 변경이 hello 서버에서 내 렸 고 제공 하는 경우를 검색 합니다.
* 일시 삭제: 삭제 된 레코드를 삭제 하 여 오프 라인 캐시에 다른 장치 tooupdate 허용 표시 됩니다.

### <a name="initialize-offline-sync"></a>오프라인 동기화 초기화

오프 라인 각 테이블을 사용 하기 전에 hello 오프 라인 캐시에 정의 되어야 합니다.  일반적으로 테이블 정의의 hello 클라이언트 hello 만든 직후에 수행 됩니다.

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

                // Create a table definition.  As a best practice, store this with hello model definition and return it via
                // a static method
                Map<String, ColumnDataType> toDoItemDefinition = new HashMap<String, ColumnDataType>();
                toDoItemDefinition.put("id", ColumnDataType.String);
                toDoItemDefinition.put("complete", ColumnDataType.Boolean);
                toDoItemDefinition.put("text", ColumnDataType.String);
                toDoItemDefinition.put("version", ColumnDataType.String);
                toDoItemDefinition.put("updatedAt", ColumnDataType.DateTimeOffset);

                // Now define hello table in hello local store
                localStore.defineTable("ToDoItem", toDoItemDefinition);

                // Specify a sync handler for conflict resolution
                SimpleSyncHandler handler = new SimpleSyncHandler();

                // Initialize hello local store
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

### <a name="obtain-a-reference-toohello-offline-cache-table"></a>가져올 참조 toohello 오프 라인 캐시 테이블

온라인 테이블의 경우 `.getTable()`을 사용합니다.  오프라인 테이블의 경우 `.getSyncTable()`을 사용합니다.

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

온라인 테이블 (필터링, 정렬, 페이징, 데이터, 데이터 업데이트, 데이터 삽입 및 삭제 포함)는 동일 하 게 작동 하기 위해 사용할 수 있는 방법을 hello 모든 온라인 및 오프 라인 테이블에도 합니다.

### <a name="synchronize-hello-local-offline-cache"></a>로컬 오프 라인 캐시 hello 동기화

응용 프로그램의 hello 컨트롤 내에서 동기화는입니다.  다음은 동기화 메서드의 예입니다.

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

쿼리 이름을 toohello 제공 하면 `.pull(query, queryname)` 메서드를 증분 동기화는 만들었거나 마지막 성공적으로 완료 하는 hello 끌어오기 이후 변경 레코드만 tooreturn 사용된 합니다.

### <a name="handle-conflicts-during-offline-synchronization"></a>오프라인 동기화 중 충돌 처리

`.push()` 작업 중에 충돌이 발생하면 `MobileServiceConflictException`이 throw됩니다.   hello 서버에서 발급 한 항목 hello 예외에 포함 되어 있으며 여 검색할 수 `.getItem()` hello 예외에 있습니다.  다음 항목 hello MobileServiceSyncContext 개체에 대 한 호출 hello hello 푸시를 조정 합니다.

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

모든 충돌에는 원하는 것으로 표시 된, 일단 전화 `.push()` 다시 tooresolve 모든 hello 충돌 합니다.

## <a name="custom-api"></a>사용자 지정 API 호출

사용자 지정 API toodefine 사용자 지정 끝점을 서버 기능을 노출 하는 또는 하지 않는 매핑할 tooan 삽입, 업데이트, 삭제, 읽기 작업이 있습니다. 사용자 지정 API를 사용하면 HTTP 메시지 헤더 읽기와 설정 및 JSON 이외의 메시지 본문 형식 정의를 비롯하여 더 효율적으로 메시징을 제어할 수 있습니다.

Hello를 호출 하면 Android 클라이언트에서 **invokeApi** 메서드 toocall hello 사용자 지정 API 끝점. hello 다음 예제에서는 toocall API 끝점의 이름을 지정 방법 **completeAll**, 라는 컬렉션 클래스를 반환 하는 **MarkAllResult**합니다.

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

hello **invokeApi** hello 클라이언트 게시물 toohello 새 사용자 지정 API 요청을 전송 하는 메서드를 호출 합니다. hello 사용자 지정 API에서 반환 되는 hello 결과 오류 메시지 대화 상자에서에 표시 됩니다. 다른 버전의 **invokeApi** 필요에 따라 hello 요청 본문에는 개체를 보낼 hello HTTP 메서드를 지정 하 고 hello 요청과 함께 쿼리 매개 변수를 보낼 수 있도록 합니다. **invokeApi** 의 형식화되지 않은 버전도 제공됩니다.

## <a name="authentication"></a>인증 tooyour 앱 추가

자습서를 이미 자세히 설명 방법을 tooadd 이러한 기능입니다.

App Service는 Facebook, Google, Microsoft 계정, Twitter 및 Azure Active Directory와 같이 다양한 외부 ID 공급자를 사용하여 [앱 사용자의 인증](app-service-mobile-android-get-started-users.md) 을 지원합니다. 권한을 설정할 수 있습니다에 특정 작업에 대 한 테이블 toorestrict 액세스 tooonly 인증 된 사용자입니다. 또한 백 엔드에 인증 된 사용자 tooimplement 권한 부여 규칙의 hello id를 사용할 수 있습니다.

두 가지의 인증 흐름, 즉 **서버** 흐름과 **클라이언트** 흐름이 지원됩니다. hello 서버 흐름 hello id 공급자 웹 인터페이스를 사용 hello 가장 간단한 인증 경험을 제공 합니다.  추가 Sdk는 필요한 tooimplement 서버 흐름 인증 합니다. 서버 흐름 인증 hello 모바일 장치에 긴밀 한 통합을 제공 하지 않습니다 및 개념 증명 시나리오에만 권장 됩니다.

hello 클라이언트 흐름 Sdk hello id 공급자에서 제공 하므로 더 구체적인 통합 single sign on 같은 장치 관련 기능을 허용 합니다.  예를 들어 모바일 응용 프로그램에 hello Facebook SDK를 통합할 수 있습니다.  모바일 클라이언트 hello hello Facebook 응용 프로그램으로 교체 하 고 사용자 로그온 백 tooyour 모바일 응용 프로그램을 교체 하기 전에 확인 합니다.

4 단계는 응용 프로그램에서 필요한 tooenable 인증.

* ID 공급자로 인증할 수 있도록 앱을 등록합니다.
* App Service 백 엔드를 구성합니다.
* Hello 응용 프로그램 서비스 백 엔드에 대해서만 테이블 권한 tooauthenticated 사용자를 제한 합니다.
* 인증 코드 tooyour 응용 프로그램을 추가 합니다.

권한을 설정할 수 있습니다에 특정 작업에 대 한 테이블 toorestrict 액세스 tooonly 인증 된 사용자입니다. Hello 인증된 사용자 toomodify의 SID를 사용할 수도 있습니다 요청 합니다.  자세한 내용은 검토 [인증 시작] 및 hello 서버 SDK 방법 설명서입니다.

### <a name="caching"></a>인증: 서버 흐름

hello 다음 코드는 서버 흐름 로그인 프로세스를 시작 hello Google 공급자를 사용 하 여 합니다.  Hello Google 공급자에 대 한 hello 보안 요구 사항으로 인해 추가 구성이 필요 합니다.

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

또한 hello 메서드 toohello 기본 활동 클래스에 다음을 추가 합니다.

```java
// You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    // When request completes
    if (resultCode == RESULT_OK) {
        // Check hello request code matches hello one we send in hello login request
        if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
            MobileServiceActivityResult result = mClient.onActivityResult(data);
            if (result.isLoggedIn()) {
                // login succeeded
                createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                createTable();
            } else {
                // login failed, check hello error message
                String errorMessage = result.getErrorMessage();
                createAndShowDialog(errorMessage, "Error");
            }
        }
    }
}
```

hello `GOOGLE_LOGIN_REQUEST_CODE` 프로그램 main에 정의 된 hello에 대 한 작업은 사용 `login()` 메서드 및 hello 내 `onActivityResult()` 메서드.  Hello 같은 번호를 사용할 때 hello로 임의의 고유 번호를 선택할 수 있습니다 `login()` 메서드와 hello `onActivityResult()` 메서드.  (앞에서 보았듯이) 서비스 어댑터에 hello 클라이언트 코드를 추상화 하는 경우에 hello 서비스 어댑터에서 hello 적절 한 메서드를 호출 해야 합니다.

또한 customtabs에 대 한 tooconfigure hello 프로젝트가 필요 합니다.  먼저 리디렉션 URL을 지정합니다.  코드 조각 너무 다음 hello 추가`AndroidManifest.xml`:

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

Hello 추가 **redirectUriScheme** toohello `build.gradle` 응용 프로그램 파일:

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

마지막으로 추가 `com.android.support:customtabs:23.0.1` toohello 종속성 목록으로 hello `build.gradle` 파일:

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

hello에 로그인 한 사용자의 hello ID를 가져오기는 **MobileServiceUser** hello를 사용 하 여 **getUserId** 메서드. Toouse 미래 toocall 비동기 로그인 Api hello 하는 방법의 예제를 보려면 [인증 시작]합니다.

> [!WARNING]
> hello 언급 URL 체계는 대/소문자 구분 합니다.  `{url_scheme_of_you_app}`의 모든 경우가 대/소문자가 일치해야 합니다.

### <a name="caching"></a>인증 토큰 캐시

Toostore hello 사용자 ID와 인증 토큰 hello 장치에서 로컬로 필요 인증 토큰을 캐시 합니다. hello hello 앱이 시작 되 면 다음에 체크 hello 캐시 하 고 이러한 값이 더 있는 경우 절차에서 hello 로그를 건너뛰고이 데이터를 사용 하 여 hello 클라이언트 리하이드레이션 합니다. 그러나이 데이터는 / 소문자를 구분 하 고 hello 전화 가져옵니다 도난당 한 경우에 대비 안전을 위해 암호화 저장 되어야 합니다.  toocache 인증 토큰 방법의 전체 예제를 볼 수 [인증 토큰 섹션 캐시][7]합니다.

Toouse 만료 된 토큰을 시도할 때 수신 된 *401 권한이 없음* 응답 합니다. 필터를 사용하여 인증 오류를 처리할 수 있습니다.  필터 요청 toohello를 앱 서비스 백 엔드를 가로챕니다. hello 필터 코드 401에 대 한 hello 응답을 테스트 하 고 hello 로그인 프로세스를 트리거합니다 다음 hello 401을 생성 하는 hello 요청 다시 시작 합니다.

### <a name="refresh"></a>토큰 새로 고침 사용

Azure 앱 서비스 인증 및 권한 부여에서 반환 하는 hello 토큰에 1 시간까지 정의 된 수명이 있습니다.  이 기간이 지나면 hello 사용자를 다시 인증 해야 합니다.  있다면 흐름 클라이언트 인증을 통해 받은 다음 다시 인증 수는 수명이 긴 토큰을 사용 하 여 Azure 앱 서비스 인증 및 권한 부여를 사용 하 여 hello 동일한 토큰입니다.  또 다른 Azure App Service 토큰이 새로운 수명으로 생성됩니다.

또한 hello 공급자 toouse 새로 고침 토큰을 등록할 수 있습니다.  토큰 새로 고침을 항상 사용할 수는 없습니다.  추가 구성이 필요합니다.

* 에 대 한 **Azure Active Directory**, Azure Active Directory 앱 hello에 대 한 클라이언트 암호를 구성 합니다.  Azure Active Directory 인증을 구성할 때 hello Azure 앱 서비스에서에서 hello 클라이언트 암호를 지정 합니다.  `.login()`을 호출하면 `response_type=code id_token`을 매개 변수로 전달합니다.

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* 에 대 한 **Google**, hello 전달 `access_type=offline` 매개 변수로:

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* 에 대 한 **Microsoft 계정**선택, hello `wl.offline_access` 범위입니다.

호출 하는 토큰을 toorefresh `.refreshUser()`:

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

모범 사례로, hello 서버에서 401 응답을 검색 하 고 toorefresh hello 사용자 토큰을 시도 하는 필터를 만듭니다.

## <a name="log-in-with-client-flow-authentication"></a>클라이언트 흐름 인증으로 로그인

hello 흐름 클라이언트 인증으로 로그인 하기 위한 일반적인 프로세스는 다음과 같습니다.

* 서버 흐름 인증과 마찬가지로 Azure App Service 인증 및 권한 부여를 구성합니다.
* Hello tooproduce 인증 액세스 토큰에 대 한 인증 공급자 SDK를 통합 합니다.
* Hello 호출 `.login()` 메서드를 다음과 같이 합니다.

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

Hello 대체 `onSuccess()` 무엇이 든 코드를 사용 하 여 메서드는 성공적인 로그인 toouse 원하는 합니다.  hello `{provider}` 문자열은 유효한 공급자: **aad** (Azure Active Directory) **facebook**, **google**, **microsoftaccount**, 또는 **twitter**합니다.  사용자 지정 인증을 구현한 경우 hello 사용자 지정 인증 공급자 태그를 사용할 수 합니다.

### <a name="adal"></a>Active Directory 인증 라이브러리 (ADAL) hello로 사용자를 인증

Hello Active Directory 인증 라이브러리 (ADAL) toosign 사용자가 Azure Active Directory를 사용 하 여 응용 프로그램에 사용할 수 있습니다. 클라이언트 흐름 로그인을 사용 하는 것이 좋습니다 toousing hello 종종 `loginAsync()` 그대로 메서드 원래의 UX 느낌을 제공 하 고 추가 사용자 지정 허용 합니다.

1. 다음 hello 하 여 AAD 로그인에 대 한 모바일 앱 백 엔드 구성 [tooconfigure Active Directory 로그인에 대 한 서비스 응용 프로그램 방법] [ 22] 자습서입니다. 네이티브 클라이언트 응용 프로그램 등록 되었는지 toocomplete hello 선택적 단계를 확인 합니다.
2. 다음 정의 되는 프로그램의 build.gradle 파일 tooinclude hello를 수정 하 여 ADAL을 설치 합니다.

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

1. 다음 코드 tooyour 응용 프로그램을 교체를 수행 하는 hello hello를 추가 합니다.

* 대체 **INSERT-기관-여기** hello 테 넌 트 응용 프로그램을 프로 비전 하는 hello 이름의 합니다. hello 형식은 https://login.microsoftonline.com/contoso.onmicrosoft.com 여야 합니다.
* 대체 **리소스 ID 여기 삽입** 모바일 앱 백 엔드에 대 한 hello 클라이언트 ID로 합니다. Hello에서 hello 클라이언트 ID를 가져올 수 **고급** 탭의 **Azure Active Directory 설정** hello 포털에서입니다.
* 대체 **클라이언트 ID 여기 삽입** hello 네이티브 클라이언트 응용 프로그램에서 복사한 hello 클라이언트 ID로 합니다.
* 대체 **리디렉션 URI 여기 삽입** 웹 사이트와 */.auth/login/done* hello HTTPS 체계를 사용 하 여 끝점입니다. 이 값은 형태가 됩니다 너무*https://contoso.azurewebsites.net/.auth/login/done*합니다.

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

## <a name="filters"></a>클라이언트-서버 통신 hello 조정

클라이언트 연결 hello는 일반적으로 HTTP 라이브러리 hello Android SDK와 함께 제공 된 기본 hello를 사용 하 여 기본 HTTP 연결입니다.  Toochange를 이유는 다음과 같은 경우입니다.

* 대체는 HTTP 라이브러리 tooadjust 시간 제한을 toouse 백업본 있습니다.
* 진행률 표시줄 tooprovide 백업본 있습니다.
* 사용자 지정 헤더 toosupport API 관리 기능 tooadd 백업본 있습니다.
* 원하는 toointercept 실패 응답 재인증을 구현할 수 있도록 합니다.
* 원하는 toolog 백 엔드 요청 tooan 분석 서비스입니다.

### <a name="using-an-alternate-http-library"></a>대체 HTTP 라이브러리 사용

Hello 호출 `.setAndroidHttpClientFactory()` 클라이언트 참조를 만든 후 즉시 메서드.  예를 들어 tooset hello 연결 제한 시간 too60 초 (대신 hello 기본값 10 초):

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

### <a name="implement-a-progress-filter"></a>진행률 필터 구현

`ServiceFilter`를 구현하여 모든 요청에 대한 가로채기를 구현할 수 있습니다.  예를 들어 hello 다음 미리 만든된 진행률 표시줄을 업데이트합니다.

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

다음과 같이이 필터 toohello 클라이언트를 연결할 수 있습니다.

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a>요청 헤더 사용자 지정

Hello 다음을 사용 하 여 `ServiceFilter` hello 필터 hello에 연결 하 고 동일한 방식으로 hello `ProgressFilter`:

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

### <a name="conversions"></a>자동 직렬화 구성

Hello를 사용 하 여 tooevery 열을 적용 하는 변환 전략을 지정할 수 있습니다 [gson] [ 3] API입니다. hello Android 클라이언트 라이브러리를 사용 하 여 [gson] [ 3] hello 백그라운드 tooserialize Java 개체 tooJSON 데이터 hello 데이터 tooAzure 앱 서비스를 보내기 전에 합니다.  hello 다음 코드에서는 사용 hello **setFieldNamingStrategy()** 메서드 tooset hello 전략입니다. 이 예제에서는 hello 초기 문자 ("m"), 및 모든 필드 이름에 대 한 다음 소문자 hello 다음 문자를 삭제 합니다. 예를 들어 "mId"를 "id"로 변환합니다.  구현에 대 한 변환 전략 tooreduce hello 필요 `SerializedName()` 대부분의 필드에 대 한 주석입니다.

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

Hello를 사용 하 여 모바일 클라이언트 대 한 참조를 만들기 전에이 코드를 실행 해야 **MobileServiceClient**합니다.

<!-- URLs. -->
[Get started with Azure Mobile Apps]: app-service-mobile-android-get-started.md
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[Mobile Services SDK for Android]: http://go.microsoft.com/fwlink/p/?LinkID=717033
[Azure portal]: https://portal.azure.com
[인증 시작]: app-service-mobile-android-get-started-users.md
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
