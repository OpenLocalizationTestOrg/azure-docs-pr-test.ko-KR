
<br>

> [!NOTE]
> <span data-ttu-id="a9939-101">관리자가 사용자 이름과 암호를 제공한 경우, 회사 또는 학교 ID( *조직 ID*라고도 부름)가 이미 있을 가능성이 큽니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-101">If you were given a user name and password by an administrator, there's a good chance that you already have a work or school ID (also sometimes called an *organizational ID*).</span></span> <span data-ttu-id="a9939-102">이런 경우, 계정이 필요한 Azure 리소스에 Azure 계정을 사용하여 즉시 액세스를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-102">If so, you can immediately begin to use your Azure account to access Azure resources that require one.</span></span> <span data-ttu-id="a9939-103">해당 리소스를 사용할 수 없는 경우는 이 문서의 도움말을 다시 참조해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-103">If you find that you cannot use those resources, you may need to return to this article for help.</span></span> <span data-ttu-id="a9939-104">자세한 내용은 [로그인에 사용할 수 있는 계정](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) 및 [Azure 구독과 Azure AD의 연관 관계](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9939-104">For more information, see [Accounts that you can use for sign in](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) and [How an Azure subscription is related to Azure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span></span>
> 
> 

<span data-ttu-id="a9939-105">절차는 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-105">The steps are simple.</span></span> <span data-ttu-id="a9939-106">Azure 클래식 포털에서 로그인한 ID를 찾은 후 기본 Azure Active Directory 도메인을 검색하고 Azure 공동 관리자로 새 사용자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-106">You need to locate your signed on identity in the Azure classic portal, discover your default Azure Active Directory domain, and add a new user to it as an Azure co-administrator.</span></span>

## <a name="locate-your-default-directory-in-the-azure-classic-portal"></a><span data-ttu-id="a9939-107">Azure 클래식 포털에서 기본 디렉터리 찾기</span><span class="sxs-lookup"><span data-stu-id="a9939-107">Locate your default directory in the Azure classic portal</span></span>
<span data-ttu-id="a9939-108">먼저 개인 Microsoft 계정 ID를 사용하여 [Azure 클래식 포털](https://manage.windowsazure.com) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-108">Start by logging in to the [Azure classic portal](https://manage.windowsazure.com) with your personal Microsoft account identity.</span></span> <span data-ttu-id="a9939-109">로그인하고 나서 왼쪽의 파란색 패널을 아래로 스크롤하여 **ACTIVE DIRECTORY**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-109">After you are logged in, scroll down the blue panel on the left side and click **ACTIVE DIRECTORY**.</span></span>

![Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

<span data-ttu-id="a9939-111">Azure에서 사용자 ID에 대한 정보를 검색하여 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-111">Let's start by finding some information about your identity in Azure.</span></span> <span data-ttu-id="a9939-112">주 창에 다음과 같이 기본 디렉터리 하나가 있다는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-112">You should see something like the following in the main pane, showing that you have one default directory.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

<span data-ttu-id="a9939-113">정보를 좀더 찾아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-113">Let's find out some more information about it.</span></span> <span data-ttu-id="a9939-114">기본 디렉터리 행을 클릭하여 기본 디렉터리 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-114">Click the default directory row, which brings you into the default directory properties.</span></span>  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

<span data-ttu-id="a9939-115">기본 도메인 이름을 보려면 **도메인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-115">To view the default domain name, click **DOMAINS**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

<span data-ttu-id="a9939-116">여기서, Azure 계정을 이미 만든 경우 Azure Active Directory가 onmicrosoft.com의 하위 도메인으로 사용되는 개인 ID의 해시 값(텍스트 문자열에서 생성된 숫자)이 도메인을 만들었음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-116">Here you should be able to see that when the Azure account was created, Azure Active Directory created a personal default domain that is a hash value (a number generated from a string of text) of your personal ID used as a subdomain of onmicrosoft.com.</span></span> <span data-ttu-id="a9939-117">이 도메인이 지금 새 사용자를 추가할 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-117">That's the domain to which you will now add a new user.</span></span>

## <a name="creating-a-new-user-in-the-default-domain"></a><span data-ttu-id="a9939-118">기본 도메인에서 새 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a9939-118">Creating a new user in the default domain</span></span>
<span data-ttu-id="a9939-119">**사용자** 를 클릭하여 단일 개인 계정을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-119">Click **USERS** and look for your single personal account.</span></span> <span data-ttu-id="a9939-120">**원본 위치** 열에 **Microsoft 계정**으로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-120">You should see in the **SOURCED FROM** column that it is a **Microsoft account**.</span></span> <span data-ttu-id="a9939-121">기본 .onmicrosoft.com Azure Active Directory 도메인에 사용자를 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-121">We want to create a user in your default .onmicrosoft.com Azure Active Directory domain.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

<span data-ttu-id="a9939-122">다음 몇 단계에서는 [이러한 지침](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) 을 따르지만 특정 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-122">We're going to follow [these instructions](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) in the next few steps, but use a specific example.</span></span>

<span data-ttu-id="a9939-123">페이지 맨 아래에서 **+사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-123">At the bottom of the page, click **+ADD USER**.</span></span> <span data-ttu-id="a9939-124">표시되는 페이지에서 새 사용자 이름을 입력하고 **사용자 유형**을 **조직 내 새 사용자**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-124">In the page that appears, type the new user name, and make the **Type of User** a **New user in your organization**.</span></span> <span data-ttu-id="a9939-125">이 예제에서 새 사용자 이름은 `ahmet`입니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-125">In this example, the new user name is `ahmet`.</span></span> <span data-ttu-id="a9939-126">이전에서 검색한 기본 도메인을 ahmet의 전자 메일 주소에 대한 도메인으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-126">Select the default domain that you discovered previously as the domain for ahmet's email address.</span></span> <span data-ttu-id="a9939-127">끝나면 다음 화살표를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-127">Click the next arrow when finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

<span data-ttu-id="a9939-128">Ahmet에 대한 세부 정보를 추가하되 적절한 **역할** 값을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-128">Add more details for Ahmet, but make sure to select the appropriate **ROLE** value.</span></span> <span data-ttu-id="a9939-129">작업을 제대로 수행하려면 **전역 관리자** 를 사용하는 것이 간편하지만 권한이 더 적은 역할을 사용할 수 있는 경우는 그 역할을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-129">It's easy to use **Global Admin** to make sure things are working, but if you can use a lesser role, that's a good idea.</span></span> <span data-ttu-id="a9939-130">이 예제에서는 **사용자** 역할을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-130">This example uses the **User** role.</span></span> <span data-ttu-id="a9939-131">(자세한 내용은 [역할별 관리자 권한](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1)을 참조하세요.) 작업에서 각 로그에 대해 Multi-Factor Authentication을 사용하려는 경우가 아니면 Multi-Factor Authentication을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-131">(Find out more at [Administrator permissions by role](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Do not enable multi-factor authentication unless you want to use multifactor authentication for each log in operation.</span></span> <span data-ttu-id="a9939-132">끝나면 다음 화살표를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-132">Click the next arrow when you're finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

<span data-ttu-id="a9939-133">**만들기** 단추를 클릭하여 Ahmet에 대한 임시 암호를 생성하고 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-133">Click the **create** button to generate and display a temporary password for Ahmet.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

<span data-ttu-id="a9939-134">사용자 이름 메일 주소를 복사하거나 **암호를 메일로 보내기**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-134">Copy the user name email address, or use **SEND PASSWORD IN EMAIL**.</span></span> <span data-ttu-id="a9939-135">로그온하기 위해 이 정보가 곧 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-135">You'll need the information to log on shortly.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

<span data-ttu-id="a9939-136">이제 Azure Active Directory에서 소싱된 새로운 사용자인 **개발자 Ahmet**가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-136">Now you should see the new user, **Ahmet the Developer**, sourced from Azure Active Directory.</span></span> <span data-ttu-id="a9939-137">Azure Active Directory를 사용하여 새로운 회사 또는 학교 ID를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-137">You've created the new work or school identity with Azure Active Directory.</span></span> <span data-ttu-id="a9939-138">그러나 이 ID에는 아직 Azure 리소스를 사용할 수 있는 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-138">However, this identity does not yet have permissions to use Azure resources.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

<span data-ttu-id="a9939-139">**암호를 메일로 보내기**를 사용하는 경우 다음과 같은 종류의 메일이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-139">If you use **SEND PASSWORD IN EMAIL**, the following kind of email is sent.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a><span data-ttu-id="a9939-140">구독에 대한 Azure 공동 관리자 권한 추가</span><span class="sxs-lookup"><span data-stu-id="a9939-140">Adding Azure co-administrator rights for subscriptions</span></span>
<span data-ttu-id="a9939-141">이제 새 사용자가 관리 포털에 로그인할 수 있도록 새 사용자를 구독의 공동 관리자로 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-141">Now you need to add the new user as a co-administrator of your subscription so the new user can sign in to the Management Portal.</span></span> <span data-ttu-id="a9939-142">이 작업을 수행하려면 왼쪽 패널에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-142">To do this, in the lower-left panel click **Settings**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

<span data-ttu-id="a9939-143">기본 설정 영역에서 상단의 **관리자** 를 클릭하며, 여기에는 개인 Microsoft 계정 ID만 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-143">In the main settings area, click **ADMINISTRATORS** at the top and you should see only your personal Microsoft account identity.</span></span> <span data-ttu-id="a9939-144">페이지의 아래쪽에서 **+추가** 를 클릭하여 공동 관리자를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-144">At the bottom of the page, click **+ADD** to specify a co-administrator.</span></span> <span data-ttu-id="a9939-145">여기에 기본 도메인을 포함하여, 이미 만들어둔 새 사용자의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-145">Here, enter the email address of the new user you had created, including your default domain.</span></span> <span data-ttu-id="a9939-146">다음 스크린샷에 표시 된 것과 같이 기본 디렉터리에 대한 사용자 옆에 녹색 확인 표시가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-146">As shown in the next screenshot, a green check mark appears next to the user for the default directory.</span></span> <span data-ttu-id="a9939-147">이 사용자를 관리자로 지정하려는 모든 구독을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-147">Remember to select all of the subscriptions that you would like this user to be able to administer.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

<span data-ttu-id="a9939-148">작업이 완료되면 새로운 공동 관리자 ID를 포함하여 두 명의 사용자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-148">When you are done, you should now see two users, including your new co-administrator identity.</span></span> <span data-ttu-id="a9939-149">포털에서 로그아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-149">Log out of the portal.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-the-new-users-password"></a><span data-ttu-id="a9939-150">로그인 및 새 사용자의 암호 변경</span><span class="sxs-lookup"><span data-stu-id="a9939-150">Logging in and changing the new user's password</span></span>
<span data-ttu-id="a9939-151">만든 새 사용자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-151">Log in as the new user you created.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

<span data-ttu-id="a9939-152">즉시 새 암호를 만들도록 요청하는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-152">You will immediately be prompted to create a new password.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

<span data-ttu-id="a9939-153">다음과 같이 성공에 대한 보상이 주어집니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-153">You should be rewarded with success that looks like the following.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a><span data-ttu-id="a9939-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a9939-154">Next steps</span></span>
<span data-ttu-id="a9939-155">이제 새 Azure Active Directory ID를 통해 [Azure 리소스 그룹 템플릿](../articles/xplat-cli-azure-resource-manager.md)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9939-155">You can now use your new Azure Active Directory identity to use [Azure resource group templates](../articles/xplat-cli-azure-resource-manager.md).</span></span>

    azure login
    info:    Executing command login
    warn:    Please note that currently you can login only via Microsoft organizational account or service principal. For instructions on how to set them up, please read http://aka.ms/Dhf67j.
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
