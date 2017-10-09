#### <a name="configure-hello-ios-project-in-xamarin-studio"></a><span data-ttu-id="80ff3-101">Xamarin Studio에서 hello iOS 프로젝트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ff3-101">Configure hello iOS project in Xamarin Studio</span></span>
1. <span data-ttu-id="80ff3-102">Xamarin.Studio를 열고 **Info.plist**, 및 업데이트 hello **번들 식별자** hello로 새 앱 ID를 사용 하 여 이전에 만든 ID 번들</span><span class="sxs-lookup"><span data-stu-id="80ff3-102">In Xamarin.Studio, open **Info.plist**, and update hello **Bundle Identifier** with hello bundle ID that you created earlier with your new app ID.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-21.png)
2. <span data-ttu-id="80ff3-103">너무 아래로 스크롤하여**백그라운드 모드**합니다.</span><span class="sxs-lookup"><span data-stu-id="80ff3-103">Scroll down too**Background Modes**.</span></span> <span data-ttu-id="80ff3-104">선택 hello **백그라운드 모드를 사용 하도록 설정** 상자와 hello **원격 알림** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="80ff3-104">Select hello **Enable Background Modes** box and hello **Remote notifications** box.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-22.png)
3. <span data-ttu-id="80ff3-105">Hello 솔루션 패널 tooopen에서 프로젝트를 두 번 클릭 **프로젝트 옵션**합니다.</span><span class="sxs-lookup"><span data-stu-id="80ff3-105">Double-click your project in hello Solution Panel tooopen **Project Options**.</span></span>
4. <span data-ttu-id="80ff3-106">아래 **빌드**, 선택 **iOS 번들 서명**, 선택 hello 해당 id 및 프로비저닝 프로필 방금 설정한이 프로젝트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ff3-106">Under **Build**, choose **iOS Bundle Signing**, and select hello corresponding identity and provisioning profile you just set up for this project.</span></span>

   ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-20.png)

   <span data-ttu-id="80ff3-107">이렇게 하면 해당 hello 프로젝트 코드 서명에 hello 새 프로필을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ff3-107">This ensures that hello project uses hello new profile for code signing.</span></span> <span data-ttu-id="80ff3-108">Hello Xamarin 장치 공식 설명서를 프로 비전에 대 한 참조 [Xamarin 장치 프로 비전]합니다.</span><span class="sxs-lookup"><span data-stu-id="80ff3-108">For hello official Xamarin device provisioning documentation, see [Xamarin Device Provisioning].</span></span>

#### <a name="configure-hello-ios-project-in-visual-studio"></a><span data-ttu-id="80ff3-109">Visual Studio에서 hello iOS 프로젝트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ff3-109">Configure hello iOS project in Visual Studio</span></span>
1. <span data-ttu-id="80ff3-110">Visual Studio에서 hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="80ff3-110">In Visual Studio, right-click hello project, and then click **Properties**.</span></span>
2. <span data-ttu-id="80ff3-111">Hello 속성 페이지에서 클릭 hello **iOS 응용 프로그램** 탭 및 업데이트 hello **식별자** 앞에서 만든 hello id입니다.</span><span class="sxs-lookup"><span data-stu-id="80ff3-111">In hello properties pages, click hello **iOS Application** tab, and update hello **Identifier** with hello ID that you created earlier.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-23.png)
3. <span data-ttu-id="80ff3-112">Hello에 **iOS 번들 서명** 탭을 선택 하는 hello 해당 id 및 프로비저닝 프로필 ड ि를이 프로젝트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ff3-112">In hello **iOS Bundle Signing** tab, select hello corresponding identity and provisioning profile you just set up for this project.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-24.png)

    <span data-ttu-id="80ff3-113">이렇게 하면 해당 hello 프로젝트 코드 서명에 hello 새 프로필을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ff3-113">This ensures that hello project uses hello new profile for code signing.</span></span> <span data-ttu-id="80ff3-114">Hello Xamarin 장치 공식 설명서를 프로 비전에 대 한 참조 [Xamarin 장치 프로 비전]합니다.</span><span class="sxs-lookup"><span data-stu-id="80ff3-114">For hello official Xamarin device provisioning documentation, see [Xamarin Device Provisioning].</span></span>
4. <span data-ttu-id="80ff3-115">Info.plist tooopen를 두 번 클릭 한 다음 사용 **RemoteNotifications** 아래 **백그라운드 모드**합니다.</span><span class="sxs-lookup"><span data-stu-id="80ff3-115">Double-click Info.plist tooopen it, and then enable **RemoteNotifications** under **Background Modes**.</span></span>

[Xamarin 장치 프로 비전]: http://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning/
