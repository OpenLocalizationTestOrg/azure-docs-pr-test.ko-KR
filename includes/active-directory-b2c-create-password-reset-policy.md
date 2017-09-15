<span data-ttu-id="27cda-101">응용 프로그램에서 세분화된 암호 재설정을 사용하려면 암호 재설정 정책을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cda-101">To enable fine-grained password reset on your application, you will need to create a password reset policy.</span></span> <span data-ttu-id="27cda-102">[여기](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md)에 테넌트 범위의 암호 재설정 옵션이 지정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27cda-102">Note that the tenant-wide password reset option specified [here](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span></span> <span data-ttu-id="27cda-103">이 정책은 암호를 재설정하는 동안 소비자가 경험한 환경 및 응용 프로그램이 성공적인 완료를 수신하는 토큰의 콘텐츠를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="27cda-103">This policy describes the experiences that the consumers will go through during password reset and the contents of tokens that the application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="27cda-104">설정의 정책 섹션에서 **암호 재설정 정책**을 선택하고 **+ 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="27cda-104">In the policies section of settings, select **Password reset policies** and click **+ Add**.</span></span>

![등록 또는 로그인 정책을 선택하고 추가 단추를 클릭합니다.](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-policy.png)

<span data-ttu-id="27cda-106">참조할 응용 프로그램에 대한 정책 **이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="27cda-106">Enter a policy **Name** for your application to reference.</span></span> <span data-ttu-id="27cda-107">예를 들어 `SSPR`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="27cda-107">For example, enter `SSPR`.</span></span>

<span data-ttu-id="27cda-108">**ID 공급자**를 클릭하고 **Reset password using email address**(전자 메일 주소를 사용하여 암호 재설정)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="27cda-108">Select **Identity providers** and check **Reset password using email address**.</span></span> <span data-ttu-id="27cda-109">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27cda-109">Click **OK**.</span></span>

![ID 공급자로 전자 메일 주소를 사용하여 암호 재설정을 선택하고 확인 단추를 클릭합니다.](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-identity-providers.png)

<span data-ttu-id="27cda-111">**응용 프로그램 클레임**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="27cda-111">Select **Application claims**.</span></span> <span data-ttu-id="27cda-112">암호 재설정에 성공하면 응용 프로그램으로 다시 보낸 권한 부여 토큰에서 반환하려는 클레임을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="27cda-112">Choose claims you want returned in the authorization tokens sent back to your application after a successful password reset experience.</span></span> <span data-ttu-id="27cda-113">예를 들어 **사용자의 개체 ID**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="27cda-113">For example, select **User's Object ID**.</span></span>

![일부 응용 프로그램 클레임을 선택하고 확인 단추를 클릭합니다.](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-application-claims.png)

<span data-ttu-id="27cda-115">**만들기**를 클릭하여 정책을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="27cda-115">Click **Create** to add the policy.</span></span> <span data-ttu-id="27cda-116">정책이 **B2C_1_SSPR**로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="27cda-116">The policy is listed as **B2C_1_SSPR**.</span></span> <span data-ttu-id="27cda-117">**B2C_1_** 접두사가 이름에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="27cda-117">The **B2C_1_** prefix is appended to the name.</span></span>

<span data-ttu-id="27cda-118">**B2C_1_SSPR**을 선택하여 해당 정책을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="27cda-118">Open the policy by selecting **B2C_1_SSPR**.</span></span> <span data-ttu-id="27cda-119">표에 지정된 설정을 확인한 후 **지금 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27cda-119">Verify the settings specified in the table then click **Run now**.</span></span>

![정책을 선택하고 실행합니다.](media/active-directory-b2c-create-password-reset-policy/run-b2c-password-reset-policy.png)

| <span data-ttu-id="27cda-121">설정</span><span class="sxs-lookup"><span data-stu-id="27cda-121">Setting</span></span>      | <span data-ttu-id="27cda-122">값</span><span class="sxs-lookup"><span data-stu-id="27cda-122">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="27cda-123">**응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="27cda-123">**Applications**</span></span> | <span data-ttu-id="27cda-124">Contoso B2C 앱</span><span class="sxs-lookup"><span data-stu-id="27cda-124">Contoso B2C app</span></span> |
| <span data-ttu-id="27cda-125">**회신 URL 선택**</span><span class="sxs-lookup"><span data-stu-id="27cda-125">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="27cda-126">새 브라우저 탭이 열리고 응용 프로그램에서 암호 재설정 사용자 환경을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27cda-126">A new browser tab opens, and you can verify the password reset consumer experience in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="27cda-127">정책 만들기 및 업데이트가 적용되려면 최대 1분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="27cda-127">It takes up to a minute for policy creation and updates to take effect.</span></span>
>
