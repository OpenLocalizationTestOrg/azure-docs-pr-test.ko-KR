### <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a><span data-ttu-id="1723c-101">Grant Mobile Engagement 액세스 tooyour GCM API 키</span><span class="sxs-lookup"><span data-stu-id="1723c-101">Grant Mobile Engagement access tooyour GCM API Key</span></span>
<span data-ttu-id="1723c-102">Mobile Engagement toosend 푸시 알림을 사용자 대신 tooallow 하 고, toogrant tooyour API 키에 액세스 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1723c-102">tooallow Mobile Engagement toosend push notifications on your behalf, you need toogrant it access tooyour API Key.</span></span> <span data-ttu-id="1723c-103">이렇게 구성 하 고 hello Mobile Engagement 포털에 키를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1723c-103">This is done by configuring and entering your key into hello Mobile Engagement portal.</span></span>

1. <span data-ttu-id="1723c-104">Azure 클래식 포털에서 hello 앱에서는이 프로젝트에 대 한 사용 중이 고 hello를 클릭 한 다음에 있는 확인 **사로잡는 구성** hello 아래쪽 단추:</span><span class="sxs-lookup"><span data-stu-id="1723c-104">From your Azure Classic Portal, ensure you're in hello app we're using for this project, and then click hello **Engage** button at hello bottom:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engage-button.png)
2. <span data-ttu-id="1723c-105">Hello 클릭 **설정** -> **하 여 네이티브 푸시** tooenter GCM 키 섹션:</span><span class="sxs-lookup"><span data-stu-id="1723c-105">Then click hello **Settings** -> **Native Push** section tooenter your GCM Key:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engagement-portal.png)
3. <span data-ttu-id="1723c-106">Hello 클릭 **편집** 아이콘의 앞 **API 키** hello에 **GCM 설정** 아래와 같이 섹션:</span><span class="sxs-lookup"><span data-stu-id="1723c-106">Click hello **Edit** icon in front of **API Key** in hello **GCM Settings** section as shown below:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/native-push-settings.png)
4. <span data-ttu-id="1723c-107">Hello 팝업에 hello 하기 전에 가져온 GCM 서버 키를 붙여 넣고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="1723c-107">In hello pop-up, paste hello GCM Server Key you obtained before and then click **Ok**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/api-key.png)

## <span data-ttu-id="1723c-108"><a id="send"></a>보낼 알림 tooyour 앱</span><span class="sxs-lookup"><span data-stu-id="1723c-108"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="1723c-109">이제 푸시 알림 tooour 응용 프로그램에서 전송 하는 간단한 푸시 알림 캠페인 사항을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1723c-109">We will now create a simple push notification campaign that sends a push notification tooour app.</span></span>

1. <span data-ttu-id="1723c-110">Toohello 이동 **도달** Mobile engagement 연결 포털에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1723c-110">Navigate toohello **REACH** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="1723c-111">클릭 **새 공지** toocreate 푸시 알림 캠페인입니다.</span><span class="sxs-lookup"><span data-stu-id="1723c-111">Click **New announcement** toocreate your push notification campaign.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/new-announcement.png)
3. <span data-ttu-id="1723c-112">단계를 수행 하는 hello 통해 캠페인의 hello 첫 번째 필드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1723c-112">Set up hello first field of your campaign through hello following steps:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-first-params.png)
   
    <span data-ttu-id="1723c-113">a.</span><span class="sxs-lookup"><span data-stu-id="1723c-113">a.</span></span> <span data-ttu-id="1723c-114">캠페인 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1723c-114">Name your campaign.</span></span>
   
    <span data-ttu-id="1723c-115">b.</span><span class="sxs-lookup"><span data-stu-id="1723c-115">b.</span></span> <span data-ttu-id="1723c-116">선택 hello **배달 유형** 으로 *시스템 알림 단순->*: hello 간단한 Android 푸시 알림 형식 제목 및 텍스트 줄 작은 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="1723c-116">Select hello **Delivery type** as *System notification -> Simple*: This is hello simple Android push notification type that features a title and a small line of text.</span></span>
   
    <span data-ttu-id="1723c-117">c.</span><span class="sxs-lookup"><span data-stu-id="1723c-117">c.</span></span> <span data-ttu-id="1723c-118">선택 **배달 시간** 으로 *언제 든 지* tooallow hello 앱 tooreceive 알림을 여부 또는 not hello 응용 프로그램이 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1723c-118">Select **Delivery time** as *Any time* tooallow hello app tooreceive a notification whether hello app is started or not.</span></span>
   
    <span data-ttu-id="1723c-119">d.</span><span class="sxs-lookup"><span data-stu-id="1723c-119">d.</span></span> <span data-ttu-id="1723c-120">Hello 알림 텍스트 형식 hello에 **제목** 에 될 hello 푸시에서 굵게 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1723c-120">In hello notification text type hello **Title** which will be in bold in hello push.</span></span>
   
    <span data-ttu-id="1723c-121">e.</span><span class="sxs-lookup"><span data-stu-id="1723c-121">e.</span></span> <span data-ttu-id="1723c-122">그런 다음 **메시지**</span><span class="sxs-lookup"><span data-stu-id="1723c-122">Then type your **Message**</span></span>
4. <span data-ttu-id="1723c-123">아래로 스크롤하고 hello에 **콘텐츠** 섹션에서 **알림 전용**합니다.</span><span class="sxs-lookup"><span data-stu-id="1723c-123">Scroll down, and in hello **Content** section, select **Notification only**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-content.png)
5. <span data-ttu-id="1723c-124">설정을 hello 가장 기본적인 캠페인 가능한 작업이 끝났습니다.</span><span class="sxs-lookup"><span data-stu-id="1723c-124">You're done setting hello most basic campaign possible.</span></span> <span data-ttu-id="1723c-125">이제 다시 아래로 스크롤하여 하 고 hello 클릭 **만들기** toosave 캠페인 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1723c-125">Now scroll down again and click hello **Create** button toosave your campaign.</span></span>
6. <span data-ttu-id="1723c-126">마지막 단계: 클릭 **Activate** tooactivate 캠페인 toosend 푸시 알림에 합니다.</span><span class="sxs-lookup"><span data-stu-id="1723c-126">Last step: click **Activate** tooactivate your campaign toosend push notifications.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-activate.png)

