<span data-ttu-id="37e75-101">tooenable 프로필 응용 프로그램에서 편집 해야 toocreate 정책을 편집 하는 프로필입니다.</span><span class="sxs-lookup"><span data-stu-id="37e75-101">tooenable profile editing on your application, you will need toocreate a profile editing policy.</span></span> <span data-ttu-id="37e75-102">이 정책은 소비자를 성공적으로 완료 되 hello 응용 프로그램은 수신 하는 토큰의 프로필 편집 및 hello 내용을 중 통과 하는 hello 환경을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="37e75-102">This policy describes hello experiences that consumers will go through during profile editing and hello contents of tokens that hello application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="37e75-103">설정의 hello 정책 섹션에서 선택 **프로필 정책 편집** 클릭 **+ 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="37e75-103">In hello policies section of settings, select **Profile editing policies** and click **+ Add**.</span></span>

![정책을 편집 하는 프로필을 선택 하 고 hello 추가 단추를 클릭 합니다.](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

<span data-ttu-id="37e75-105">입력 정책 **이름** 응용 프로그램 tooreference에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="37e75-105">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="37e75-106">예를 들어 `SiPe`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="37e75-106">For example, enter `SiPe`.</span></span>

<span data-ttu-id="37e75-107">**ID 공급자**를 클릭하고 **로컬 계정 로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37e75-107">Select **Identity providers** and check **Local Account Signin**.</span></span> <span data-ttu-id="37e75-108">또한 필요에 따라 이미 구성되어 있는 소셜 ID 공급자를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37e75-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="37e75-109">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37e75-109">Click **OK**.</span></span>

![id 공급자로 로컬 계정 로그인을 선택 하 고 hello 확인 단추를 클릭 합니다.](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

<span data-ttu-id="37e75-111">**프로필 특성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37e75-111">Select **Profile attributes**.</span></span> <span data-ttu-id="37e75-112">특성 hello 소비자를 보고 하 고 자신의 프로필에 편집할 수를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="37e75-112">Choose attributes hello consumer can view and edit in their profile.</span></span> <span data-ttu-id="37e75-113">예를 들어 **국가/지역**, **표시 이름** 및 **우편 번호**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37e75-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="37e75-114">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37e75-114">Click **OK**.</span></span>

![일부 특성을 선택 하 고 hello 확인 단추를 클릭 합니다.](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

<span data-ttu-id="37e75-116">**응용 프로그램 클레임**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37e75-116">Select **Application claims**.</span></span> <span data-ttu-id="37e75-117">Hello 권한 부여 토큰에 반환 된 원하는 클레임 전송 성공적인 프로필 편집 환경은 후 뒤로 tooyour 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="37e75-117">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful profile editing experience.</span></span> <span data-ttu-id="37e75-118">예를 들어 **표시 이름**, **우편 번호**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37e75-118">For example, select **Display Name**, **Postal Code**.</span></span>

![일부 응용 프로그램 클레임을 선택하고 확인 단추를 클릭합니다.](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

<span data-ttu-id="37e75-120">클릭 **만들기** tooadd hello 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="37e75-120">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="37e75-121">hello 정책으로 표시 되 **B2C_1_SiPe**합니다.</span><span class="sxs-lookup"><span data-stu-id="37e75-121">hello policy is listed as **B2C_1_SiPe**.</span></span> <span data-ttu-id="37e75-122">hello **B2C_1_** 접두사에 추가 된 toohello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="37e75-122">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="37e75-123">선택 하 여 hello 정책을 엽니다 **B2C_1_SiPe**합니다.</span><span class="sxs-lookup"><span data-stu-id="37e75-123">Open hello policy by selecting **B2C_1_SiPe**.</span></span> <span data-ttu-id="37e75-124">Hello 테이블에 지정 된 hello 설정을 확인 한 후 클릭 **지금 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="37e75-124">Verify hello settings specified in hello table then click **Run now**.</span></span>

![정책을 선택하고 실행합니다.](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| <span data-ttu-id="37e75-126">설정</span><span class="sxs-lookup"><span data-stu-id="37e75-126">Setting</span></span>      | <span data-ttu-id="37e75-127">값</span><span class="sxs-lookup"><span data-stu-id="37e75-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="37e75-128">**응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="37e75-128">**Applications**</span></span> | <span data-ttu-id="37e75-129">Contoso B2C 앱</span><span class="sxs-lookup"><span data-stu-id="37e75-129">Contoso B2C app</span></span> |
| <span data-ttu-id="37e75-130">**회신 URL 선택**</span><span class="sxs-lookup"><span data-stu-id="37e75-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="37e75-131">새 브라우저 탭이 열리고 hello 프로필 편집 구성 된 대로 소비자 환경을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37e75-131">A new browser tab opens, and you can verify hello profile editing consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="37e75-132">정책 만들기에 대 일 분 차지 하 고 tootake 효과 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="37e75-132">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>