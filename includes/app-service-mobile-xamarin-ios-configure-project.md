#### <a name="configure-the-ios-project-in-xamarin-studio"></a><span data-ttu-id="7aa85-101">Xamarin Studio에서 iOS 프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="7aa85-101">Configure the iOS project in Xamarin Studio</span></span>
1. <span data-ttu-id="7aa85-102">Xamarin.Studio에서 **Info.plist**를 열고 앞에서 새 앱 ID로 만든 번들 ID를 사용하여 **Bundle 식별자**를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa85-102">In Xamarin.Studio, open **Info.plist**, and update the **Bundle Identifier** with the bundle ID that you created earlier with your new app ID.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-21.png)
2. <span data-ttu-id="7aa85-103">아래의 **Background Modes**로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa85-103">Scroll down to **Background Modes**.</span></span> <span data-ttu-id="7aa85-104">**Enable Background Modes** 상자와 **Remote notifications** 상자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa85-104">Select the **Enable Background Modes** box and the **Remote notifications** box.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-22.png)
3. <span data-ttu-id="7aa85-105">Solution Panel에서 프로젝트를 두 번 클릭하여 **Project Options**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7aa85-105">Double-click your project in the Solution Panel to open **Project Options**.</span></span>
4. <span data-ttu-id="7aa85-106">**Build**에서 **iOS Bundle Signing**을 선택하고 방금 이 프로젝트에 대해 설정한 해당 ID 및 프로비전 프로필을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa85-106">Under **Build**, choose **iOS Bundle Signing**, and select the corresponding identity and provisioning profile you just set up for this project.</span></span>

   ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-20.png)

   <span data-ttu-id="7aa85-107">이제 프로젝트에서 코드 서명에 새 프로필을 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aa85-107">This ensures that the project uses the new profile for code signing.</span></span> <span data-ttu-id="7aa85-108">공식 Xamarin 장치 프로비저닝 설명서를 보려면 [Xamarin 장치 프로비저닝]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7aa85-108">For the official Xamarin device provisioning documentation, see [Xamarin Device Provisioning].</span></span>

#### <a name="configure-the-ios-project-in-visual-studio"></a><span data-ttu-id="7aa85-109">Visual Studio에서 iOS 프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="7aa85-109">Configure the iOS project in Visual Studio</span></span>
1. <span data-ttu-id="7aa85-110">Visual Studio에서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa85-110">In Visual Studio, right-click the project, and then click **Properties**.</span></span>
2. <span data-ttu-id="7aa85-111">속성 페이지에서 **iOS 응용 프로그램** 탭을 클릭하고 앞에서 만든 ID를 사용하여 **식별자**를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa85-111">In the properties pages, click the **iOS Application** tab, and update the **Identifier** with the ID that you created earlier.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-23.png)
3. <span data-ttu-id="7aa85-112">**iOS Bundle Signing** 탭에서 방금 이 프로젝트에 대해 설정한 해당 ID 및 프로비전 프로필을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa85-112">In the **iOS Bundle Signing** tab, select the corresponding identity and provisioning profile you just set up for this project.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-24.png)

    <span data-ttu-id="7aa85-113">이제 프로젝트에서 코드 서명에 새 프로필을 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aa85-113">This ensures that the project uses the new profile for code signing.</span></span> <span data-ttu-id="7aa85-114">공식 Xamarin 장치 프로비저닝 설명서를 보려면 [Xamarin 장치 프로비저닝]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7aa85-114">For the official Xamarin device provisioning documentation, see [Xamarin Device Provisioning].</span></span>
4. <span data-ttu-id="7aa85-115">Info.plist를 두 번 클릭하여 연 다음 **Background Modes**에서 **RemoteNotifications**를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7aa85-115">Double-click Info.plist to open it, and then enable **RemoteNotifications** under **Background Modes**.</span></span>

<span data-ttu-id="7aa85-116">[Xamarin 장치 프로비저닝]: http://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning/</span><span class="sxs-lookup"><span data-stu-id="7aa85-116">[Xamarin Device Provisioning]: http://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning/</span></span>
