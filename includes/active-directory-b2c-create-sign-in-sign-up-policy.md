<span data-ttu-id="74740-101">tooenable 로그인, 응용 프로그램에 로그인 toocreate 정책 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74740-101">tooenable sign-in on your application, you will need toocreate a sign-in policy.</span></span> <span data-ttu-id="74740-102">이 정책은 성공적인 로그인에는 소비자를 통해 로그인 하는 동안 되 고 응용 프로그램 hello 토큰의 hello 내용을 수신할 hello 환경을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="74740-102">This policy describes hello experiences that consumers will go through during sign-in and hello contents of tokens that hello application will receive on successful sign-ins.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="74740-103">설정의 hello 정책 섹션에서 선택 **등록 또는 로그인 시 정책** 클릭 **+ 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="74740-103">In hello policies section of settings, select **Sign-up or sign-in policies** and click **+ Add**.</span></span>

![등록 또는 로그인 정책을 선택하고 추가 단추를 클릭합니다.](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-policy.png)

<span data-ttu-id="74740-105">입력 정책 **이름** 응용 프로그램 tooreference에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="74740-105">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="74740-106">예를 들어 `SiUpIn`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="74740-106">For example, enter `SiUpIn`.</span></span>

<span data-ttu-id="74740-107">**ID 공급자**를 선택한 다음 **전자 메일 등록**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74740-107">Select **Identity providers** and check **Email signup**.</span></span> <span data-ttu-id="74740-108">또한 필요에 따라 이미 구성되어 있는 소셜 ID 공급자를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74740-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="74740-109">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74740-109">Click **OK**.</span></span>

![id 공급자로 등록 전자 메일을 선택 하 고 hello 확인 단추를 클릭 합니다.](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-identity-providers.png)

<span data-ttu-id="74740-111">**등록 특성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74740-111">Select **Sign-up attributes**.</span></span> <span data-ttu-id="74740-112">특성 선택 toocollect hello 소비자에서 등록 하는 동안 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="74740-112">Choose attributes you want toocollect from hello consumer during sign-up.</span></span> <span data-ttu-id="74740-113">예를 들어 **국가/지역**, **표시 이름** 및 **우편 번호**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74740-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="74740-114">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74740-114">Click **OK**.</span></span>

![일부 특성을 선택 하 고 hello 확인 단추를 클릭 합니다.](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-sign-up-attributes.png)

<span data-ttu-id="74740-116">**응용 프로그램 클레임**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74740-116">Select **Application claims**.</span></span> <span data-ttu-id="74740-117">Hello 권한 부여 토큰에 반환 된 원하는 클레임 전송 성공적으로 등록 또는 로그인 경험 후 뒤로 tooyour 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="74740-117">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful sign-up or sign-in experience.</span></span> <span data-ttu-id="74740-118">예를 들어 **표시 이름**, **ID 공급자**, **우편 번호**, **새 사용자** 및 **사용자의 개체 ID**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74740-118">For example, select **Display Name**, **Identity Provider**, **Postal Code**, **User is new** and **User's Object ID**.</span></span>

![일부 응용 프로그램 클레임을 선택하고 확인 단추를 클릭합니다.](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-application-claims.png)

<span data-ttu-id="74740-120">클릭 **만들기** tooadd hello 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="74740-120">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="74740-121">hello 정책으로 표시 되 **B2C_1_SiUpIn**합니다.</span><span class="sxs-lookup"><span data-stu-id="74740-121">hello policy is listed as **B2C_1_SiUpIn**.</span></span> <span data-ttu-id="74740-122">hello **B2C_1_** 접두사에 추가 된 toohello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="74740-122">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="74740-123">선택 하 여 hello 정책을 엽니다 **B2C_1_SiUpIn**합니다.</span><span class="sxs-lookup"><span data-stu-id="74740-123">Open hello policy by selecting **B2C_1_SiUpIn**.</span></span> <span data-ttu-id="74740-124">Hello 테이블에 지정 된 hello 설정을 확인 한 후 클릭 **지금 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="74740-124">Verify hello settings specified in hello table then click **Run now**.</span></span>

![정책을 선택하고 실행합니다.](media/active-directory-b2c-create-sign-in-sign-up-policy/run-b2c-signup-signin-policy.png)

| <span data-ttu-id="74740-126">설정</span><span class="sxs-lookup"><span data-stu-id="74740-126">Setting</span></span>      | <span data-ttu-id="74740-127">값</span><span class="sxs-lookup"><span data-stu-id="74740-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="74740-128">**응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="74740-128">**Applications**</span></span> | <span data-ttu-id="74740-129">Contoso B2C 앱</span><span class="sxs-lookup"><span data-stu-id="74740-129">Contoso B2C app</span></span> |
| <span data-ttu-id="74740-130">**회신 URL 선택**</span><span class="sxs-lookup"><span data-stu-id="74740-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="74740-131">새 브라우저 탭이 열리고 구성 된 대로 hello 등록 또는 로그인 소비자 경험을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74740-131">A new browser tab opens, and you can verify hello sign-up or sign-in consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="74740-132">정책 만들기에 대 일 분 차지 하 고 tootake 효과 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="74740-132">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>