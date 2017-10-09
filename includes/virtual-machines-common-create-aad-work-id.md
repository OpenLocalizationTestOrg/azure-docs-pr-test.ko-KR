
<br>

> [!NOTE]
> <span data-ttu-id="cae7c-101">관리자가 사용자 이름과 암호를 제공한 경우, 회사 또는 학교 ID( *조직 ID*라고도 부름)가 이미 있을 가능성이 큽니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-101">If you were given a user name and password by an administrator, there's a good chance that you already have a work or school ID (also sometimes called an *organizational ID*).</span></span> <span data-ttu-id="cae7c-102">그렇다면 toouse를 요구 하는 Azure 리소스에 Azure 계정 tooaccess 즉시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-102">If so, you can immediately begin toouse your Azure account tooaccess Azure resources that require one.</span></span> <span data-ttu-id="cae7c-103">이러한 리소스를 사용할 수 없다는 찾을 경우 tooreturn toothis 문서에 대 한 도움말 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-103">If you find that you cannot use those resources, you may need tooreturn toothis article for help.</span></span> <span data-ttu-id="cae7c-104">자세한 내용은 참조 [에 사용할 수 있는 계정에 로그인](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) 및 [어떻게 Azure 구독을 관련된 tooAzure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir)합니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-104">For more information, see [Accounts that you can use for sign in](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) and [How an Azure subscription is related tooAzure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span></span>
> 
> 

<span data-ttu-id="cae7c-105">hello 단계는 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-105">hello steps are simple.</span></span> <span data-ttu-id="cae7c-106">필요한 toolocate 로그인 된 hello Azure 클래식 포털의에서 id에 대 여 기본 Azure Active Directory 도메인을 검색 하 고 새 사용자 tooit를 Azure 공동 관리자로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-106">You need toolocate your signed on identity in hello Azure classic portal, discover your default Azure Active Directory domain, and add a new user tooit as an Azure co-administrator.</span></span>

## <a name="locate-your-default-directory-in-hello-azure-classic-portal"></a><span data-ttu-id="cae7c-107">기본 디렉터리 hello Azure 클래식 포털에서 찾을</span><span class="sxs-lookup"><span data-stu-id="cae7c-107">Locate your default directory in hello Azure classic portal</span></span>
<span data-ttu-id="cae7c-108">Toohello에 로그인 하 여 시작 [Azure 클래식 포털](https://manage.windowsazure.com) 개인 Microsoft 계정 id와 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-108">Start by logging in toohello [Azure classic portal](https://manage.windowsazure.com) with your personal Microsoft account identity.</span></span> <span data-ttu-id="cae7c-109">로그인 할 hello 왼쪽의 파란색 hello 패널 아래로 스크롤하여을 클릭 하면 **ACTIVE DIRECTORY**합니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-109">After you are logged in, scroll down hello blue panel on hello left side and click **ACTIVE DIRECTORY**.</span></span>

![Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

<span data-ttu-id="cae7c-111">Azure에서 사용자 ID에 대한 정보를 검색하여 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-111">Let's start by finding some information about your identity in Azure.</span></span> <span data-ttu-id="cae7c-112">Hello hello 기본 창에서 다음, 하나의 기본 디렉터리가 있는지를 보여 주는 같은 내용이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-112">You should see something like hello following in hello main pane, showing that you have one default directory.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

<span data-ttu-id="cae7c-113">정보를 좀더 찾아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-113">Let's find out some more information about it.</span></span> <span data-ttu-id="cae7c-114">Hello 기본 디렉터리 속성으로 제공 하는 hello 기본 디렉터리 행을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-114">Click hello default directory row, which brings you into hello default directory properties.</span></span>  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

<span data-ttu-id="cae7c-115">tooview hello 기본 도메인 이름을 클릭 하 여 **도메인**합니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-115">tooview hello default domain name, click **DOMAINS**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

<span data-ttu-id="cae7c-116">여기 Azure 계정이 hello를 만들 때 Azure Active Directory 만든 해시 값 (텍스트 문자열에서 생성 된 번호)에 해당 개인 기본 도메인 수 toosee 있어야 onmicrosoft.com의 하위 도메인으로 사용 되는 개인 ID의 합니다. 그건 hello 도메인 toowhich 이제 새 사용자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-116">Here you should be able toosee that when hello Azure account was created, Azure Active Directory created a personal default domain that is a hash value (a number generated from a string of text) of your personal ID used as a subdomain of onmicrosoft.com. That's hello domain toowhich you will now add a new user.</span></span>

## <a name="creating-a-new-user-in-hello-default-domain"></a><span data-ttu-id="cae7c-117">Hello 기본 도메인에 새 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="cae7c-117">Creating a new user in hello default domain</span></span>
<span data-ttu-id="cae7c-118">**사용자** 를 클릭하여 단일 개인 계정을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-118">Click **USERS** and look for your single personal account.</span></span> <span data-ttu-id="cae7c-119">Hello에 표시 되어야 **원본 위치** 는 열 한 **Microsoft 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-119">You should see in hello **SOURCED FROM** column that it is a **Microsoft account**.</span></span> <span data-ttu-id="cae7c-120">기본 사용자 toocreate 주시기 바랍니다. onmicrosoft.com Azure Active Directory 도메인.</span><span class="sxs-lookup"><span data-stu-id="cae7c-120">We want toocreate a user in your default .onmicrosoft.com Azure Active Directory domain.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

<span data-ttu-id="cae7c-121">Toofollow 여기 [이러한 지침](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) 에 다음 몇 단계 hello 하지만 특정 예제를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-121">We're going toofollow [these instructions](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) in hello next few steps, but use a specific example.</span></span>

<span data-ttu-id="cae7c-122">Hello hello 페이지의 아래쪽에 있는 클릭 **+ 사용자 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-122">At hello bottom of hello page, click **+ADD USER**.</span></span> <span data-ttu-id="cae7c-123">나타나는 hello 페이지에서 새 사용자 이름 hello를 입력 하 고 hello 확인 **사용자 유형** 는 **조직 내에서 새 사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-123">In hello page that appears, type hello new user name, and make hello **Type of User** a **New user in your organization**.</span></span> <span data-ttu-id="cae7c-124">이 예에서 새 사용자 이름 hello는 `ahmet`합니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-124">In this example, hello new user name is `ahmet`.</span></span> <span data-ttu-id="cae7c-125">이전에 ahmet의 전자 메일 주소에 대 한 hello 도메인으로 검색 하는 hello 기본 도메인을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-125">Select hello default domain that you discovered previously as hello domain for ahmet's email address.</span></span> <span data-ttu-id="cae7c-126">완료 되 면 hello 다음 화살표를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-126">Click hello next arrow when finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

<span data-ttu-id="cae7c-127">Ahmet에 대 한 자세한 정보를 추가 하지만 있는지 tooselect hello를 적절 한 확인 **역할** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-127">Add more details for Ahmet, but make sure tooselect hello appropriate **ROLE** value.</span></span> <span data-ttu-id="cae7c-128">쉽게 toouse는 **전역 관리자** toomake 것으로 작업 하는 있지만 더 낮은 역할을 사용 하려면 경우 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-128">It's easy toouse **Global Admin** toomake sure things are working, but if you can use a lesser role, that's a good idea.</span></span> <span data-ttu-id="cae7c-129">이 예에서는 hello **사용자** 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-129">This example uses hello **User** role.</span></span> <span data-ttu-id="cae7c-130">(자세한 내용은 [역할별 관리자 권한](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1)을 참조하세요.) 각 로그 작업에 대해 다단계 인증 toouse 사용 하려는 경우가 아니면 다단계 인증을 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="cae7c-130">(Find out more at [Administrator permissions by role](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Do not enable multi-factor authentication unless you want toouse multifactor authentication for each log in operation.</span></span> <span data-ttu-id="cae7c-131">완료 되 면 hello 다음 화살표를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-131">Click hello next arrow when you're finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

<span data-ttu-id="cae7c-132">Hello 클릭 **만들** toogenerate 단추 및 Ahmet에 대 한 임시 암호를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-132">Click hello **create** button toogenerate and display a temporary password for Ahmet.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

<span data-ttu-id="cae7c-133">Hello 사용자 이름은 전자 메일 주소를 복사 하거나 사용 하 여 **암호에 전자 메일 보내기**합니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-133">Copy hello user name email address, or use **SEND PASSWORD IN EMAIL**.</span></span> <span data-ttu-id="cae7c-134">곧 hello 정보 toolog에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-134">You'll need hello information toolog on shortly.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

<span data-ttu-id="cae7c-135">이제 hello 새 사용자를 표시 해야 **Ahmet hello 개발자**, Azure Active Directory에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-135">Now you should see hello new user, **Ahmet hello Developer**, sourced from Azure Active Directory.</span></span> <span data-ttu-id="cae7c-136">Azure Active Directory와 hello 새 회사 또는 학교 identity 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-136">You've created hello new work or school identity with Azure Active Directory.</span></span> <span data-ttu-id="cae7c-137">그러나이 id를 포함 하지 않은 사용 권한을 toouse Azure 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-137">However, this identity does not yet have permissions toouse Azure resources.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

<span data-ttu-id="cae7c-138">사용 하는 경우 **암호에 전자 메일 보내기**, hello 전자 메일의 종류에 따라 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-138">If you use **SEND PASSWORD IN EMAIL**, hello following kind of email is sent.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a><span data-ttu-id="cae7c-139">구독에 대한 Azure 공동 관리자 권한 추가</span><span class="sxs-lookup"><span data-stu-id="cae7c-139">Adding Azure co-administrator rights for subscriptions</span></span>
<span data-ttu-id="cae7c-140">이제 사용자가 필요 tooadd hello 새 구독의 공동 관리자로 hello 새 사용자가 toohello 관리 포털에에서 로그인 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-140">Now you need tooadd hello new user as a co-administrator of your subscription so hello new user can sign in toohello Management Portal.</span></span> <span data-ttu-id="cae7c-141">이 hello 왼쪽 패널에서 클릭 toodo **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-141">toodo this, in hello lower-left panel click **Settings**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

<span data-ttu-id="cae7c-142">Hello 메인 설정 영역에서 클릭 **관리자** hello에 top 해야 표시만 사용자 개인 Microsoft 계정 id입니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-142">In hello main settings area, click **ADMINISTRATORS** at hello top and you should see only your personal Microsoft account identity.</span></span> <span data-ttu-id="cae7c-143">Hello hello 페이지의 아래쪽에 있는 클릭 **+ 추가** toospecify 공동 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-143">At hello bottom of hello page, click **+ADD** toospecify a co-administrator.</span></span> <span data-ttu-id="cae7c-144">여기에서 hello 새 사용자를 만들 때, 기본 도메인을 포함 하 여 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-144">Here, enter hello email address of hello new user you had created, including your default domain.</span></span> <span data-ttu-id="cae7c-145">Hello 다음 스크린샷에 나와 있는 것 처럼 녹색 확인 표시가 hello 기본 디렉터리에 대 한 다음 toohello 사용자 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-145">As shown in hello next screenshot, a green check mark appears next toohello user for hello default directory.</span></span> <span data-ttu-id="cae7c-146">Tooselect 기억 모든 싶다는 의사를이 사용자 toobe 수 tooadminister hello 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-146">Remember tooselect all of hello subscriptions that you would like this user toobe able tooadminister.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

<span data-ttu-id="cae7c-147">작업이 완료되면 새로운 공동 관리자 ID를 포함하여 두 명의 사용자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-147">When you are done, you should now see two users, including your new co-administrator identity.</span></span> <span data-ttu-id="cae7c-148">로그 아웃 hello 포털.</span><span class="sxs-lookup"><span data-stu-id="cae7c-148">Log out of hello portal.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-hello-new-users-password"></a><span data-ttu-id="cae7c-149">로그인 및 hello 새 사용자의 암호를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-149">Logging in and changing hello new user's password</span></span>
<span data-ttu-id="cae7c-150">만든 hello 새 사용자로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-150">Log in as hello new user you created.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

<span data-ttu-id="cae7c-151">입력 정보 요청된 toocreate 새 암호를 즉시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-151">You will immediately be prompted toocreate a new password.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

<span data-ttu-id="cae7c-152">다음과 같은 hello 성공적으로 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-152">You should be rewarded with success that looks like hello following.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a><span data-ttu-id="cae7c-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cae7c-153">Next steps</span></span>
<span data-ttu-id="cae7c-154">이제 새 Azure Active Directory identity toouse 프로그램을 사용할 수 있습니다 [Azure 리소스 그룹 템플릿](../articles/xplat-cli-azure-resource-manager.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cae7c-154">You can now use your new Azure Active Directory identity toouse [Azure resource group templates](../articles/xplat-cli-azure-resource-manager.md).</span></span>

    azure login
    info:    Executing command login
    warn:    Please note that currently you can login only via Microsoft organizational account or service principal. For instructions on how tooset them up, please read http://aka.ms/Dhf67j.
    Username: ahmet@aztrainpassxxxxxoutlook.onmicrosoft.com
    Password: *********
    /info:    Added subscription Azure Pass
    info:    Setting subscription Azure Pass as default
    +
    info:    login command OK
    ralph@local:~$ azure config mode arm
    info:    New mode is arm
    ralph@local:~$ azure group list
    info:    Executing command group list
    + Listing resource groups
    info:    No matched resource groups were found
    info:    group list command OK
    ralph@local:~$ azure group create newgroup westus
    info:    Executing command group create
    + Getting resource group newgroup
    + Creating resource group newgroup
    info:    Created resource group newgroup
    data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/newgroup
    data:    Name:                newgroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags:
    data:
    info:    group create command OK
