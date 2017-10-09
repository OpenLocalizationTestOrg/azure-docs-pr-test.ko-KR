
### <a name="update-manifest-file-tooenable-notifications"></a><span data-ttu-id="48e41-101">업데이트 매니페스트 파일 tooenable 알림</span><span class="sxs-lookup"><span data-stu-id="48e41-101">Update manifest file tooenable notifications</span></span>
<span data-ttu-id="48e41-102">프로그램 Manifest.xml hello 사이 아래 hello 앱에서 메시징 리소스 복사 `<application>` 및 `</application>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-102">Copy hello in-app messaging resources below into your Manifest.xml between hello `<application>` and `</application>` tags.</span></span>

        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/plain" />
              </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/html" />
            </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
                <category android:name="android.intent.category.DEFAULT"/>
            </intent-filter>
        </activity>
        <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver" android:exported="false">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
            </intent-filter>
        </receiver>
        <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
            <intent-filter>
                <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
            </intent-filter>
        </receiver>

### <a name="specify-an-icon-for-notifications"></a><span data-ttu-id="48e41-103">알림 아이콘 지정</span><span class="sxs-lookup"><span data-stu-id="48e41-103">Specify an icon for notifications</span></span>
<span data-ttu-id="48e41-104">Hello 간의 프로그램 Manifest.xml에서 XML 조각을 다음 붙여넣기 hello `<application>` 및 `</application>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-104">Paste hello following XML snippet in your Manifest.xml between hello `<application>` and `</application>` tags.</span></span>

        <meta-data android:name="engagement:reach:notification:icon" android:value="engagement_close"/>

<span data-ttu-id="48e41-105">앱 내 알림과 시스템에 표시 되는 hello 아이콘을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-105">This defines hello icon that is displayed both in system and in-app notifications.</span></span> <span data-ttu-id="48e41-106">이 아이콘은 앱 내 알림에는 옵션이지만 시스템 알림에는 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-106">It is optional for in-app notifications however mandatory for system notifications.</span></span> <span data-ttu-id="48e41-107">Android에서는 아이콘이 잘못된 시스템 알림을 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-107">Android will rejects system notifications with invalid icons.</span></span>

<span data-ttu-id="48e41-108">Hello 중 하나에 존재 하는 아이콘을 사용 하 고 있는지 확인 **그릴** 폴더 (같은 ``engagement_close.png``).</span><span class="sxs-lookup"><span data-stu-id="48e41-108">Make sure you are using an icon that exists in one of hello **drawable** folders (like ``engagement_close.png``).</span></span> <span data-ttu-id="48e41-109">**mipmap** 폴더는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-109">**mipmap** folder isn't supported.</span></span>

> [!NOTE]
> <span data-ttu-id="48e41-110">Hello를 사용 하지 않아야 **launcher** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-110">You should not use hello **launcher** icon.</span></span> <span data-ttu-id="48e41-111">다른 해결이 있으며 일반적으로 지원 되지 않습니다. hello mip 맵 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-111">It has a different resolution and is usually in hello mipmap folders, which we don't support.</span></span>
> 
> 

<span data-ttu-id="48e41-112">실제 앱의 경우 [Android 디자인 지침](http://developer.android.com/design/patterns/notifications.html)에 따라 알림에 적합한 아이콘을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-112">For real apps, you can use an icon that is suitable for notifications per [Android design guidelines](http://developer.android.com/design/patterns/notifications.html).</span></span>

> [!TIP]
> <span data-ttu-id="48e41-113">toobe 있는지 toouse 올바른 살펴보면 아이콘 해상도 [이러한 예제](https://www.google.com/design/icons)합니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-113">toobe sure toouse correct icon resolutions, you can look at [these examples](https://www.google.com/design/icons).</span></span>
> <span data-ttu-id="48e41-114">Toohello 아래로 스크롤하여 **알림** 섹션 아이콘을 클릭 하 고 클릭 `PNGS` toodownload hello 아이콘 그릴 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-114">Scroll down toohello **Notification** section, click an icon, and then click `PNGS` toodownload hello icon drawable set.</span></span> <span data-ttu-id="48e41-115">Hello 아이콘의 각 버전에는 해상도 toouse 사용 하 여 어떤 그릴 수 있는 폴더를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-115">You can see what drawable folders with which resolution toouse for each version of hello icon.</span></span>
> 
> 

### <a name="enable-your-app-tooreceive-gcm-push-notifications"></a><span data-ttu-id="48e41-116">응용 프로그램 tooreceive GCM 푸시 알림을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="48e41-116">Enable your app tooreceive GCM push notifications</span></span>
1. <span data-ttu-id="48e41-117">Hello 다음 프로그램 Manifest.xml hello 사이 붙여 `<application>` 및 `</application>` hello를 바꾼 후 태그 **보낸 사람 ID** Firebase 프로젝트 콘솔에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-117">Paste hello following into your Manifest.xml between hello `<application>` and `</application>` tags after replacing hello **Sender ID** obtained from your Firebase project console.</span></span> <span data-ttu-id="48e41-118">hello \n은 의도적으로 된 숫자 hello 프로젝트를 종료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-118">hello \n is intentional so make sure that you end hello project number with it.</span></span>
   
        <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
2. <span data-ttu-id="48e41-119">아래 hello 코드 프로그램 Manifest.xml hello 사이 붙여 넣습니다 `<application>` 및 `</application>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-119">Paste hello code below into your Manifest.xml between hello `<application>` and `</application>` tags.</span></span> <span data-ttu-id="48e41-120">Hello 패키지 이름 바꾸기 <Your package name>합니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-120">Replace hello package name <Your package name>.</span></span>
   
        <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
        android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver" android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<Your package name>" />
            </intent-filter>
        </receiver>
3. <span data-ttu-id="48e41-121">Hello 마지막 hello 하기 전에 표시 된 사용 권한 집합을 추가 `<application>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-121">Add hello last set of permissions that are highlighted before hello `<application>` tag.</span></span> <span data-ttu-id="48e41-122">대체 `<Your package name>` 응용 프로그램의 hello 실제 패키지 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="48e41-122">Replace `<Your package name>` by hello actual package name of your application.</span></span>
   
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="<Your package name>.permission.C2D_MESSAGE" />
        <permission android:name="<Your package name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

