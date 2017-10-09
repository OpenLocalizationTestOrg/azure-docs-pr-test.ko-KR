<span data-ttu-id="fa298-101">tooenable 세분화 된 암호 재설정 응용 프로그램에서 암호 재설정 정책을 toocreate가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa298-101">tooenable fine-grained password reset on your application, you will need toocreate a password reset policy.</span></span> <span data-ttu-id="fa298-102">해당 hello 테 넌 트 전체 암호 재설정 옵션을 지정 하는 참고 [여기](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa298-102">Note that hello tenant-wide password reset option specified [here](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span></span> <span data-ttu-id="fa298-103">이 정책은 성공적으로 완료 되는 hello 소비자를 통해 암호 재설정 하는 동안 되 고 응용 프로그램 hello 토큰의 hello 내용을 수신할 hello 환경을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa298-103">This policy describes hello experiences that hello consumers will go through during password reset and hello contents of tokens that hello application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="fa298-104">설정의 hello 정책 섹션에서 선택 **암호 재설정 정책** 클릭 **+ 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa298-104">In hello policies section of settings, select **Password reset policies** and click **+ Add**.</span></span>

![등록 또는 로그인 시 정책을 선택 하 고 hello 추가 단추를 클릭 합니다.](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-policy.png)

<span data-ttu-id="fa298-106">입력 정책 **이름** 응용 프로그램 tooreference에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa298-106">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="fa298-107">예를 들어 `SSPR`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fa298-107">For example, enter `SSPR`.</span></span>

<span data-ttu-id="fa298-108">**ID 공급자**를 클릭하고 **Reset password using email address**(전자 메일 주소를 사용하여 암호 재설정)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fa298-108">Select **Identity providers** and check **Reset password using email address**.</span></span> <span data-ttu-id="fa298-109">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fa298-109">Click **OK**.</span></span>

![암호 재설정 전자 메일 주소를 id 공급자로 사용 하 여 선택 하 고 hello 확인 단추를 클릭 합니다.](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-identity-providers.png)

<span data-ttu-id="fa298-111">**응용 프로그램 클레임**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fa298-111">Select **Application claims**.</span></span> <span data-ttu-id="fa298-112">성공적인 암호 재설정 환경 후 hello 권한 부여 토큰에 반환 된 원하는 클레임 전송 백 tooyour 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa298-112">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful password reset experience.</span></span> <span data-ttu-id="fa298-113">예를 들어 **사용자의 개체 ID**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fa298-113">For example, select **User's Object ID**.</span></span>

![일부 응용 프로그램 클레임을 선택하고 확인 단추를 클릭합니다.](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-application-claims.png)

<span data-ttu-id="fa298-115">클릭 **만들기** tooadd hello 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="fa298-115">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="fa298-116">hello 정책으로 표시 되 **B2C_1_SSPR**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa298-116">hello policy is listed as **B2C_1_SSPR**.</span></span> <span data-ttu-id="fa298-117">hello **B2C_1_** 접두사에 추가 된 toohello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="fa298-117">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="fa298-118">선택 하 여 hello 정책을 엽니다 **B2C_1_SSPR**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa298-118">Open hello policy by selecting **B2C_1_SSPR**.</span></span> <span data-ttu-id="fa298-119">Hello 테이블에 지정 된 hello 설정을 확인 한 후 클릭 **지금 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa298-119">Verify hello settings specified in hello table then click **Run now**.</span></span>

![정책을 선택하고 실행합니다.](media/active-directory-b2c-create-password-reset-policy/run-b2c-password-reset-policy.png)

| <span data-ttu-id="fa298-121">설정</span><span class="sxs-lookup"><span data-stu-id="fa298-121">Setting</span></span>      | <span data-ttu-id="fa298-122">값</span><span class="sxs-lookup"><span data-stu-id="fa298-122">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="fa298-123">**응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="fa298-123">**Applications**</span></span> | <span data-ttu-id="fa298-124">Contoso B2C 앱</span><span class="sxs-lookup"><span data-stu-id="fa298-124">Contoso B2C app</span></span> |
| <span data-ttu-id="fa298-125">**회신 URL 선택**</span><span class="sxs-lookup"><span data-stu-id="fa298-125">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="fa298-126">새 브라우저 탭이 열리고 hello 암호 재설정 응용 프로그램에서 소비자 경험을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa298-126">A new browser tab opens, and you can verify hello password reset consumer experience in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="fa298-127">정책 만들기에 대 일 분 차지 하 고 tootake 효과 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa298-127">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>
