### <a name="grant-mobile-engagement-access-to-your-gcm-api-key"></a><span data-ttu-id="d2519-101">Mobile Engagement에 GCM API 키에 대한 액세스 권한 부여</span><span class="sxs-lookup"><span data-stu-id="d2519-101">Grant Mobile Engagement access to your GCM API Key</span></span>
<span data-ttu-id="d2519-102">사용자를 대신하여 Mobile Engagement에서 푸시 알림을 보내도록 허용하려면 Mobile Engagement에 API 키에 대한 액세스 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2519-102">To allow Mobile Engagement to send push notifications on your behalf, you need to grant it access to your API Key.</span></span> <span data-ttu-id="d2519-103">키를 구성하고 Mobile Engagement 포털에 입력하여 이를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d2519-103">This is done by configuring and entering your key into the Mobile Engagement portal.</span></span>

1. <span data-ttu-id="d2519-104">Azure 클래식 포털에서 현재 이 프로젝트에 사용하고 있는 앱에 있는지 확인한 다음 아래쪽에서 **연결** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d2519-104">From your Azure Classic Portal, ensure you're in the app we're using for this project, and then click the **Engage** button at the bottom:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engage-button.png)
2. <span data-ttu-id="d2519-105">**설정** -> **네이티브 푸시** 섹션을 클릭하여 GCM 키를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d2519-105">Then click the **Settings** -> **Native Push** section to enter your GCM Key:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engagement-portal.png)
3. <span data-ttu-id="d2519-106">아래와 같이 **GCM 설정** 섹션의 **API 키** 앞에 있는 **편집** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d2519-106">Click the **Edit** icon in front of **API Key** in the **GCM Settings** section as shown below:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/native-push-settings.png)
4. <span data-ttu-id="d2519-107">팝업에서 전에 가져온 GCM 서버 키를 붙여넣은 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d2519-107">In the pop-up, paste the GCM Server Key you obtained before and then click **Ok**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/api-key.png)

## <span data-ttu-id="d2519-108"><a id="send"></a>앱에 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="d2519-108"><a id="send"></a>Send a notification to your app</span></span>
<span data-ttu-id="d2519-109">이제 앱에 푸시 알림을 보내는 간단한 푸시 알림 캠페인을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d2519-109">We will now create a simple push notification campaign that sends a push notification to our app.</span></span>

1. <span data-ttu-id="d2519-110">Mobile Engagement 포털에서 **도달률** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d2519-110">Navigate to the **REACH** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="d2519-111">**새 공지** 를 클릭하여 푸시 알림 캠페인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2519-111">Click **New announcement** to create your push notification campaign.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/new-announcement.png)
3. <span data-ttu-id="d2519-112">다음 단계를 수행하여 캠페인의 첫 번째 필드를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2519-112">Set up the first field of your campaign through the following steps:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-first-params.png)
   
    <span data-ttu-id="d2519-113">a.</span><span class="sxs-lookup"><span data-stu-id="d2519-113">a.</span></span> <span data-ttu-id="d2519-114">캠페인 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2519-114">Name your campaign.</span></span>
   
    <span data-ttu-id="d2519-115">b.</span><span class="sxs-lookup"><span data-stu-id="d2519-115">b.</span></span> <span data-ttu-id="d2519-116">**Delivery 형식**을 *시스템 알림 -> 심플*로 선택: 이 알림은 제목 및 몇 줄의 텍스트를 특징으로 하는 간단한 Android 푸시 알림 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="d2519-116">Select the **Delivery type** as *System notification -> Simple*: This is the simple Android push notification type that features a title and a small line of text.</span></span>
   
    <span data-ttu-id="d2519-117">c.</span><span class="sxs-lookup"><span data-stu-id="d2519-117">c.</span></span> <span data-ttu-id="d2519-118">앱 시작 여부와 관계없이 앱에서 알림을 받을 수 있도록 **배달 시간** 을 *항상* 으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2519-118">Select **Delivery time** as *Any time* to allow the app to receive a notification whether the app is started or not.</span></span>
   
    <span data-ttu-id="d2519-119">d.</span><span class="sxs-lookup"><span data-stu-id="d2519-119">d.</span></span> <span data-ttu-id="d2519-120">알림 텍스트에서 푸시에 굵게 표시할 **제목** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d2519-120">In the notification text type the **Title** which will be in bold in the push.</span></span>
   
    <span data-ttu-id="d2519-121">e.</span><span class="sxs-lookup"><span data-stu-id="d2519-121">e.</span></span> <span data-ttu-id="d2519-122">그런 다음 **메시지**</span><span class="sxs-lookup"><span data-stu-id="d2519-122">Then type your **Message**</span></span>
4. <span data-ttu-id="d2519-123">아래로 스크롤하여 **콘텐츠** 섹션에서 **알림만**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2519-123">Scroll down, and in the **Content** section, select **Notification only**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-content.png)
5. <span data-ttu-id="d2519-124">가능한 가장 기본적인 캠페인 설정을 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="d2519-124">You're done setting the most basic campaign possible.</span></span> <span data-ttu-id="d2519-125">이제 다시 아래로 스크롤하고 **만들기** 단추를 클릭하여 캠페인을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d2519-125">Now scroll down again and click the **Create** button to save your campaign.</span></span>
6. <span data-ttu-id="d2519-126">마지막 단계: **활성화** 를 클릭하여 푸시 알림을 보내기 위해 캠페인을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="d2519-126">Last step: click **Activate** to activate your campaign to send push notifications.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-activate.png)

