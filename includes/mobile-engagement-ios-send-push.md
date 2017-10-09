### <a name="grant-access-tooyour-push-certificate-toomobile-engagement"></a><span data-ttu-id="60530-101">권한 부여 액세스 tooyour 푸시 인증서 tooMobile Engagement</span><span class="sxs-lookup"><span data-stu-id="60530-101">Grant access tooyour Push Certificate tooMobile Engagement</span></span>
<span data-ttu-id="60530-102">사용자 대신 tooallow Mobile Engagement toosend 푸시 알림을, toogrant tooyour 인증서에 액세스 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60530-102">tooallow Mobile Engagement toosend Push Notifications on your behalf, you need toogrant it access tooyour certificate.</span></span> <span data-ttu-id="60530-103">이렇게 구성 하 고 hello Mobile Engagement 포털에 인증서를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="60530-103">This is done by configuring and entering your certificate into hello Mobile Engagement portal.</span></span> <span data-ttu-id="60530-104">[Apple 설명서](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="60530-104">Make sure you obtain your .p12 certificate as explained in [Apple's documentation](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

1. <span data-ttu-id="60530-105">Mobile engagement 연결 포털 tooyour 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="60530-105">Navigate tooyour Mobile Engagement portal.</span></span> <span data-ttu-id="60530-106">확인 올바른 hello에 있는 한 hello에서 클릭 한 다음 **사로잡는 구성** hello 아래쪽 단추:</span><span class="sxs-lookup"><span data-stu-id="60530-106">Ensure you're in hello correct and then click on hello **Engage** button at hello bottom:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engage-button.png)
2. <span data-ttu-id="60530-107">Hello 클릭 **설정을** engagement 연결 포털에서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="60530-107">Click on hello **Settings** page in your Engagement Portal.</span></span> <span data-ttu-id="60530-108">Hello 없어 클릭에서 **하 여 네이티브 푸시** tooupload p12 인증서 섹션:</span><span class="sxs-lookup"><span data-stu-id="60530-108">From there click on hello **Native Push** section tooupload your p12 certificate:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engagement-portal.png)
3. <span data-ttu-id="60530-109">다음과 같이 p12를 선택하여 업로드하고 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="60530-109">Select your p12, upload it and type your password:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/native-push-settings.png)

## <span data-ttu-id="60530-110"><a id="send"></a>보낼 알림 tooyour 앱</span><span class="sxs-lookup"><span data-stu-id="60530-110"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="60530-111">이제 푸시 tooour 앱 보낼 단순한 푸시 알림을 캠페인 사항을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="60530-111">We will now create a simple Push Notification campaign that will send a push tooour app:</span></span>

1. <span data-ttu-id="60530-112">Toohello 이동 **도달** Mobile engagement 연결 포털에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="60530-112">Navigate toohello **Reach** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="60530-113">클릭 **새 공지** toocreate 푸시 캠페인</span><span class="sxs-lookup"><span data-stu-id="60530-113">Click **New Announcement** toocreate your push campaign</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/new-announcement.png)
3. <span data-ttu-id="60530-114">캠페인의 첫 번째 필드 hello 설치:</span><span class="sxs-lookup"><span data-stu-id="60530-114">Setup hello first fields of your campaign:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-first-params.png)
   
   * <span data-ttu-id="60530-115">캠페인 **이름** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="60530-115">Provide a **Name** for your campaign</span></span> 
   * <span data-ttu-id="60530-116">선택 hello **배달 시간** 으로 **앱 외부만**: 일부 텍스트 옵션이 있는 hello 간단한 Apple 푸시 알림 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="60530-116">Select hello **Delivery time** as **Out of app only**: this is hello simple Apple push notification type that features some text.</span></span>
   * <span data-ttu-id="60530-117">Hello 알림 텍스트에서 첫 번째 hello 입력 **제목** 를 hello hello 푸시에서 첫 번째 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60530-117">In hello notification text, type first hello **Title** which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="60530-118">입력 한 다음 프로그램 **메시지** hello 두 번째 줄 됩니다</span><span class="sxs-lookup"><span data-stu-id="60530-118">Then type your **Message** which will be hello second line</span></span>
4. <span data-ttu-id="60530-119">Hello에서 콘텐츠 섹션을 선택 하 고 아래로 스크롤하여 **알림 전용**</span><span class="sxs-lookup"><span data-stu-id="60530-119">Scroll down, and in hello content section select **Notification only**</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-content.png)
5. <span data-ttu-id="60530-120">설정을 hello 가장 기본적인 캠페인을 완료 것입니다.</span><span class="sxs-lookup"><span data-stu-id="60530-120">You're done setting hello most basic campaign.</span></span> <span data-ttu-id="60530-121">이제 아래로 스크롤하여 클릭 **만들기** toosave 푸시 알림 캠페인 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="60530-121">Now scroll down and click on **Create** button toosave your push notification campaign.</span></span> 
6. <span data-ttu-id="60530-122">마지막으로-클릭 **Activate** toosend 푸시 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="60530-122">Finally - click on **Activate** toosend push notification.</span></span> 
   
    ![](./media/mobile-engagement-ios-send-push/campaign-activate.png)
7. <span data-ttu-id="60530-123">수 없게 됩니다. hello 다음과 같은 hello 알림 센터에 iOS 장치에서 hello 알림을 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="60530-123">You will be able receive hello notification on your iOS device in hello notification center like hello following:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/iphone-notification.png)
8. <span data-ttu-id="60530-124">이 iOS 장치를 함께 사용 하는 Apple Watch 있으면 hello 알림을 Apple Watch 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60530-124">If you have an Apple Watch paired with this iOS device then you will see hello notification on your Apple Watch:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/apple-watch.png)

