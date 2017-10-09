1. <span data-ttu-id="e229b-101">열기 hello Android SDK Manager hello Android Studio의 hello 도구 모음 아이콘을 클릭 하 여 또는 클릭 하 여 **도구** -> **Android** -> **SDK Manager**hello 메뉴.</span><span class="sxs-lookup"><span data-stu-id="e229b-101">Open hello Android SDK Manager by clicking hello icon on hello toolbar of Android Studio or by clicking **Tools** -> **Android** -> **SDK Manager** on hello menu.</span></span> <span data-ttu-id="e229b-102">클릭 하 여 열를 프로젝트에 hello 대상 버전의 hello 사용 되는 Android SDK를 찾아 **패키지 세부 정보 표시**, 선택 **Google Api**아직 설치 되지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="e229b-102">Locate hello target version of hello Android SDK that is used in your project , open it by clicking **Show Package Details**, and choose **Google APIs**, if it is not already installed.</span></span>
2. <span data-ttu-id="e229b-103">Hello 클릭 **SDK 도구** 탭 합니다. Google Play Service를 아직 설치하지 않은 경우 아래와 같이 **Google Play Services** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e229b-103">Click hello **SDK Tools** tab. If you haven't already installed Google Play Service, click **Google Play Services** as shown below.</span></span> <span data-ttu-id="e229b-104">클릭 **적용** tooinstall 합니다.</span><span class="sxs-lookup"><span data-stu-id="e229b-104">Then click **Apply** tooinstall.</span></span> 
   
    <span data-ttu-id="e229b-105">참고 hello SDK 경로 이후 단계에서 사용 하기 위해입니다.</span><span class="sxs-lookup"><span data-stu-id="e229b-105">Note hello SDK path, for use in a later step.</span></span> 
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. <span data-ttu-id="e229b-106">열기 hello **의 build.gradle** hello 응용 프로그램 디렉터리의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e229b-106">Open hello **build.gradle** file in hello app directory.</span></span>
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. <span data-ttu-id="e229b-107">*종속성*아래에 이 줄 추가:</span><span class="sxs-lookup"><span data-stu-id="e229b-107">Add this line under *dependencies*:</span></span> 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. <span data-ttu-id="e229b-108">Hello 클릭 **Gradle 파일을 사용 하 여 동기화 프로젝트** hello 도구 모음에서 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="e229b-108">Click hello **Sync Project with Gradle Files** icon in hello tool bar.</span></span>
6. <span data-ttu-id="e229b-109">열기 **AndroidManifest.xml** 이 태그 toohello 추가 *응용 프로그램* 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="e229b-109">Open **AndroidManifest.xml** and add this tag toohello *application* tag.</span></span>
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

