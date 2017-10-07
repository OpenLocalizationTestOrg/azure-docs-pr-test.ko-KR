---
title: "Azure Active Directory-Azure API 관리를 사용 하 여 aaaAuthorize 개발자 계정을 | Microsoft Docs"
description: "자세한 내용은 방법 tooauthorize 사용자가 Azure Active Directory를 사용 하 여 API 관리에서 합니다."
services: api-management
documentationcenter: API Management
author: steved0x
manager: erikre
editor: 
ms.assetid: 33a69a83-94f2-4e4e-9cef-f2a5af3c9732
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ebf5447a509a47df35e4262138bfcf423cb1dd5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-azure-active-directory-in-azure-api-management"></a><span data-ttu-id="d5158-103">Tooauthorize 개발자 어떻게 사용 하 여 계정을 Azure Active Directory를 Azure API 관리에서</span><span class="sxs-lookup"><span data-stu-id="d5158-103">How tooauthorize developer accounts using Azure Active Directory in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="d5158-104">개요</span><span class="sxs-lookup"><span data-stu-id="d5158-104">Overview</span></span>
<span data-ttu-id="d5158-105">이 가이드에서는 tooenable Azure Active Directory에서 사용자에 대 한 toohello 개발자 포털에 액세스 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-105">This guide shows you how tooenable access toohello developer portal for users from Azure Active Directory.</span></span> <span data-ttu-id="d5158-106">이 가이드 또한 보면 방법을 포함 하는 외부 그룹을 추가 하 여 Azure Active Directory 사용자 그룹이 toomanage hello Azure Active Directory의 사용자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-106">This guide also shows you how toomanage groups of Azure Active Directory users by adding external groups that contain hello users of an Azure Active Directory.</span></span>

> <span data-ttu-id="d5158-107">이 가이드의 단계를 toocomplete hello 있어야 Azure Active Directory는 toocreate에 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-107">toocomplete hello steps in this guide you must first have an Azure Active Directory in which toocreate an application.</span></span>
> 
> 

## <a name="how-tooauthorize-developer-accounts-using-azure-active-directory"></a><span data-ttu-id="d5158-108">Tooauthorize 개발자 어떻게 사용 하 여 계정을 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d5158-108">How tooauthorize developer accounts using Azure Active Directory</span></span>
<span data-ttu-id="d5158-109">시작 tooget 클릭 **게시자 포털** hello API 관리 서비스에 대 한 Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="d5158-109">tooget started, click **Publisher portal** in hello Azure portal for your API Management service.</span></span> <span data-ttu-id="d5158-110">API 관리 게시자 포털 toohello 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-110">This takes you toohello API Management publisher portal.</span></span>

![게시자 포털][api-management-management-console]

> <span data-ttu-id="d5158-112">API 관리 서비스 인스턴스를 아직 만들지 않은 경우 참조 [API 관리 서비스 인스턴스를 만들] [ Create an API Management service instance] hello에 [Azure API 관리 시작] [ Get started with Azure API Management] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="d5158-113">클릭 **보안** hello에서 **API 관리** 메뉴를 클릭 한 hello 왼쪽 **외부 Id**합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-113">Click **Security** from hello **API Management** menu on hello left and click **External Identities**.</span></span>

![외부 ID][api-management-security-external-identities]

<span data-ttu-id="d5158-115">**Azure Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-115">Click **Azure Active Directory**.</span></span> <span data-ttu-id="d5158-116">Hello 메모 **리디렉션 URL** hello Azure 클래식 포털에서에서 Azure Active Directory tooyour 전환 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-116">Make a note of hello **Redirect URL** and switch over tooyour Azure Active Directory in hello Azure Classic Portal.</span></span>

![외부 ID][api-management-security-aad-new]

<span data-ttu-id="d5158-118">Hello 클릭 **추가** toocreate 새 Azure Active Directory 응용 프로그램 단추 선택한 **조직에서 개발 중인 응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-118">Click hello **Add** button toocreate a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![새 Azure Active Directory 응용 프로그램 추가][api-management-new-aad-application-menu]

<span data-ttu-id="d5158-120">Hello 응용 프로그램에 대 한 이름을 입력 **웹 응용 프로그램 및/또는 Web API**, hello 다음 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-120">Enter a name for hello application, select **Web application and/or Web API**, and click hello next button.</span></span>

![새 Azure Active Directory 응용 프로그램][api-management-new-aad-application-1]

<span data-ttu-id="d5158-122">에 대 한 **로그온 URL**, 개발자 포털을 가리키도록의 hello 로그온 URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-122">For **Sign-on URL**, enter hello sign-on URL of your developer portal.</span></span> <span data-ttu-id="d5158-123">이 예제에서는 hello **로그온 URL** 은 `https://aad03.portal.current.int-azure-api.net/signin`합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-123">In this example, hello **Sign-on URL** is `https://aad03.portal.current.int-azure-api.net/signin`.</span></span> 

<span data-ttu-id="d5158-124">Hello에 대 한 **앱 ID URL**hello Azure Active Directory에 대 한 hello 기본 도메인 또는 사용자 지정 도메인을 입력 하 고 고유한 문자열 tooit를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-124">For hello **App ID URL**, enter either hello default domain or a custom domain for hello Azure Active Directory, and append a unique string tooit.</span></span> <span data-ttu-id="d5158-125">이 예제에서는 기본 도메인의 hello **https://contoso5api.onmicrosoft.com** 의 hello 접미사와 함께 사용 되 **/api** 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-125">In this example, hello default domain of **https://contoso5api.onmicrosoft.com** is used with hello suffix of **/api** specified.</span></span>

![새 Azure Active Directory 응용 프로그램 속성][api-management-new-aad-application-2]

<span data-ttu-id="d5158-127">Hello 확인 단추 toosave 클릭 하 고 hello 응용 프로그램을 만들어 toohello 전환 **구성** tooconfigure hello 새 응용 프로그램을 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-127">Click hello check button toosave and create hello application, and switch toohello **Configure** tab tooconfigure hello new application.</span></span>

![새 Azure Active Directory 응용 프로그램 만들어짐][api-management-new-aad-app-created]

<span data-ttu-id="d5158-129">여러 Azure Active 디렉터리 하는 경우이 응용 프로그램에 사용 되는 toobe 클릭 **예** 에 대 한 **응용 프로그램은 다중 테 넌 트**합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-129">If multiple Azure Active Directories are going toobe used for this application, click **Yes** for **Application is multi-tenant**.</span></span> <span data-ttu-id="d5158-130">hello 기본값은 **아니요**합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-130">hello default is **No**.</span></span>

![예][api-management-aad-app-multi-tenant]

<span data-ttu-id="d5158-132">복사 hello **리디렉션 URL** hello에서 **Azure Active Directory** hello 섹션 **외부 Id** 탭 hello 게시자 포털에서 하 고 hello 에붙여**회신 URL** 입력란.</span><span class="sxs-lookup"><span data-stu-id="d5158-132">Copy hello **Redirect URL** from hello **Azure Active Directory** section of hello **External Identities** tab in hello publisher portal and paste it into hello **Reply URL** text box.</span></span> 

![회신 URL][api-management-aad-reply-url]

<span data-ttu-id="d5158-134">스크롤 toohello 맨 hello 구성 탭을 선택 하는 hello **응용 프로그램 사용 권한** 드롭 다운 확인 **디렉터리 데이터 읽기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-134">Scroll toohello bottom of hello configure tab, select hello **Application Permissions** drop-down, and check **Read directory data**.</span></span>

![응용 프로그램 권한][api-management-aad-app-permissions]

<span data-ttu-id="d5158-136">선택 hello **권한 위임** 드롭 다운 확인 **로그온을 사용 하도록 설정 하 고 사용자의 프로필 읽기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-136">Select hello **Delegate Permissions** drop-down, and check **Enable sign-on and read users' profiles**.</span></span>

![위임된 권한][api-management-aad-delegated-permissions]

> <span data-ttu-id="d5158-138">응용 프로그램 및 권한이 위임된 하는 방법에 대 한 자세한 내용은 참조 [Graph API 액세스 hello][Accessing hello Graph API]합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-138">For more information about application and delegated permissions, see [Accessing hello Graph API][Accessing hello Graph API].</span></span>
> 
> 

<span data-ttu-id="d5158-139">복사 hello **클라이언트 Id** toohello 클립보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-139">Copy hello **Client Id** toohello clipboard.</span></span>

![클라이언트 ID][api-management-aad-app-client-id]

<span data-ttu-id="d5158-141">뒤로 toohello 게시자 포털을 전환 하 고 hello에 붙여 **클라이언트 Id** hello Azure Active Directory 응용 프로그램 구성에서 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-141">Switch back toohello publisher portal and paste in hello **Client Id** copied from hello Azure Active Directory application configuration.</span></span>

![클라이언트 ID][api-management-client-id]

<span data-ttu-id="d5158-143">뒤로 toohello Azure Active Directory 구성을 전환 하 고 hello 클릭 **기간 선택** 드롭 다운 hello **키** 섹션 고 간격을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-143">Switch back toohello Azure Active Directory configuration, and click hello **Select duration** drop-down in hello **Keys** section and specify an interval.</span></span> <span data-ttu-id="d5158-144">이 예제에서는 **1년**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-144">In this example, **1 year** is used.</span></span>

![키][api-management-aad-key-before-save]

<span data-ttu-id="d5158-146">클릭 **저장** toosave hello 구성 및 표시 hello 키입니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-146">Click **Save** toosave hello configuration and display hello key.</span></span> <span data-ttu-id="d5158-147">Hello 키 toohello 클립보드에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-147">Copy hello key toohello clipboard.</span></span>

> <span data-ttu-id="d5158-148">이 키를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-148">Make a note of this key.</span></span> <span data-ttu-id="d5158-149">Hello Azure Active Directory 구성 창을 닫으면 되 면 hello 키를 다시 표시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-149">Once you close hello Azure Active Directory configuration window, hello key cannot be displayed again.</span></span>
> 
> 

![키][api-management-aad-key-after-save]

<span data-ttu-id="d5158-151">스위치 백 toohello 게시자 포털 및 붙여넣기 hello 키 hello에 **클라이언트 암호** 입력란.</span><span class="sxs-lookup"><span data-stu-id="d5158-151">Switch back toohello publisher portal and paste hello key into hello **Client Secret** text box.</span></span>

![클라이언트 암호][api-management-client-secret]

<span data-ttu-id="d5158-153">**테 넌 트 허용** 하는 디렉터리 액세스 toohello hello API 관리 서비스 인스턴스에의 Api를 포함 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-153">**Allowed Tenants** specifies which directories have access toohello APIs of hello API Management service instance.</span></span> <span data-ttu-id="d5158-154">Hello toogrant에 액세스 하는 Azure Active Directory 인스턴스 toowhich의 hello 도메인을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-154">Specify hello domains of hello Azure Active Directory instances toowhich you want toogrant access.</span></span> <span data-ttu-id="d5158-155">줄바꿈, 공백 또는 쉼표로 여러 도메인을 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-155">You can separate multiple domains with newlines, spaces, or commas.</span></span>

![허용된 테넌트][api-management-client-allowed-tenants]


<span data-ttu-id="d5158-157">Hello 원하는 구성이 지정 되어 있는 경우 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-157">Once hello desired configuration is specified, click **Save**.</span></span>

![저장][api-management-client-allowed-tenants-save]

<span data-ttu-id="d5158-159">지정 된는 Azure Active Directory의 hello 단계를 수행 하 여 toohello 개발자 포털에 서명할 수 hello에 hello 사용자 hello 변경 내용이 저장 되 면 [Azure Active Directory 계정을 사용 하 여 toohello 개발자 포털에 로그인] [Log in toohello Developer portal using an Azure Active Directory account].</span><span class="sxs-lookup"><span data-stu-id="d5158-159">Once hello changes are saved, hello users in hello specified Azure Active Directory can sign in toohello Developer portal by following hello steps in [Log in toohello Developer portal using an Azure Active Directory account][Log in toohello Developer portal using an Azure Active Directory account].</span></span>

<span data-ttu-id="d5158-160">여러 도메인 hello에 지정할 수 있습니다 **허용 테 넌 트** 섹션.</span><span class="sxs-lookup"><span data-stu-id="d5158-160">Multiple domains can be specified in hello **Allowed Tenants** section.</span></span> <span data-ttu-id="d5158-161">모든 사용자는 hello 원래 도메인 hello 응용 프로그램 등록 된 다른 도메인에서 로그인 할 수, 전에 hello 서로 다른 도메인의 글로벌 관리자 권한을 부여 해야 응용 프로그램 tooaccess hello에 대 한 디렉터리 데이터.</span><span class="sxs-lookup"><span data-stu-id="d5158-161">Before any user can log in from a different domain than hello original domain where hello application was registered, a global administrator of hello different domain must grant permission for hello application tooaccess directory data.</span></span> <span data-ttu-id="d5158-162">toogrant 권한, 전역 관리자에 게 너무 이동 해야`https://<URL of your developer portal>/aadadminconsent` (예를 들어 https://contoso.portal.azure-api.net/aadadminconsent) hello toogive 액세스 tooand 원하는 Active Directory 테 넌 트의 hello 도메인 이름 입력 제출을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-162">toogrant permission, hello global administrator should go too`https://<URL of your developer portal>/aadadminconsent` (for example, https://contoso.portal.azure-api.net/aadadminconsent), type in hello domain name of hello Active Directory tenant they want toogive access tooand click Submit.</span></span> <span data-ttu-id="d5158-163">Hello 다음의 예를 들어의 전역 관리자 `miaoaad.onmicrosoft.com` toogive 권한 toothis 특정 개발자 포털에서이 하려고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-163">In hello following example, a global administrator from `miaoaad.onmicrosoft.com` is trying toogive permission toothis particular developer portal.</span></span> 

![권한][api-management-aad-consent]

<span data-ttu-id="d5158-165">Hello 다음 화면에서 전역 관리자에 게 증명된 tooconfirm hello 권한을 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-165">In hello next screen, hello global administrator will be prompted tooconfirm giving hello permission.</span></span> 

![권한][api-management-permissions-form]

> <span data-ttu-id="d5158-167">비전역 관리자가 권한 전에 toolog에 전역 관리자가 부여, hello 로그인 시도 실패 및 오류 화면이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-167">If a non-global administrator tries toolog in before permissions are granted by a global administrator, hello login attempt fails and an error screen is displayed.</span></span>
> 
> 

## <a name="how-tooadd-an-external-azure-active-directory-group"></a><span data-ttu-id="d5158-168">어떻게 tooadd 외부 Azure Active Directory 그룹</span><span class="sxs-lookup"><span data-stu-id="d5158-168">How tooadd an external Azure Active Directory Group</span></span>
<span data-ttu-id="d5158-169">Azure Active Directory의 사용자에 대 한 액세스를 설정한 후 쉽게 관리할 수 원하는 hello 제품 hello 그룹에서 hello 개발자의 hello 연결 API 관리 toomore에 Azure Active Directory 그룹을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-169">After enabling access for users in an Azure Active Directory, you can add Azure Active Directory groups into API Management toomore easily manage hello association of hello developers in hello group with hello desired products.</span></span>

> <span data-ttu-id="d5158-170">먼저 외부 Azure Active Directory 그룹에서 Azure Active Directory hello tooconfigure hello hello 이전 섹션 절차에에서 따라 hello Identities 탭에서 구성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-170">tooconfigure an external Azure Active Directory group, hello Azure Active Directory must first be configured in hello Identities tab by following hello procedure in hello previous section.</span></span> 
> 
> 

<span data-ttu-id="d5158-171">외부 Azure Active Directory 그룹 hello에서 추가 된 **가시성** toogrant 액세스 toohello 그룹 원하는 hello 제품의 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-171">External Azure Active Directory groups are added from hello **Visibility** tab of hello product for which you wish toogrant access toohello group.</span></span> <span data-ttu-id="d5158-172">클릭 **제품**, hello 원하는 제품의 hello 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-172">Click **Products**, and then click hello name of hello desired product.</span></span>

![제품 구성][api-management-configure-product]

<span data-ttu-id="d5158-174">Toohello 전환 **가시성** 탭을 클릭 **Azure Active Directory에서 그룹 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-174">Switch toohello **Visibility** tab, and click **Add Groups from Azure Active Directory**.</span></span>

![그룹 추가][api-management-add-groups]

<span data-ttu-id="d5158-176">선택 hello **Azure Active Directory 테 넌 트** hello 드롭 다운 목록 및 hello hello에서 원하는 그룹의 다음 유형 hello 이름에서 **그룹** toobe 입력란을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-176">Select hello **Azure Active Directory Tenant** from hello drop-down list, and then type hello name of hello desired group in hello **Groups** toobe added text box.</span></span>

![그룹 선택][api-management-select-group]

<span data-ttu-id="d5158-178">이 그룹 이름은 hello에 있습니다 **그룹** hello 다음 예제에에서 표시 된 대로 Azure Active Directory에 대 한 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-178">This group name can be found in hello **Groups** list for your Azure Active Directory, as shown in hello following example.</span></span>

![Azure Active Directory 그룹 목록][api-management-aad-groups-list]

<span data-ttu-id="d5158-180">클릭 **추가** toovalidate hello 그룹 이름 및 hello 그룹을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-180">Click **Add** toovalidate hello group name and add hello group.</span></span> <span data-ttu-id="d5158-181">이 예제에서는 hello **Contoso 5 개발자** 외부 그룹이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-181">In this example, hello **Contoso 5 Developers** external group is added.</span></span> 

![그룹 추가됨][api-management-aad-group-added]

<span data-ttu-id="d5158-183">클릭 **저장** toosave hello 새 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-183">Click **Save** toosave hello new group selection.</span></span>

<span data-ttu-id="d5158-184">제품 중 하나에서 Azure Active Directory 그룹에 구성 된 사용 가능한 toobe hello에 확인 표시가 되어 **가시성** 탭에 대 한 hello API 관리 서비스 인스턴스의 다른 제품 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-184">Once an Azure Active Directory group has been configured from one product, it is available toobe checked on hello **Visibility** tab for hello other products in hello API Management service instance.</span></span>

<span data-ttu-id="d5158-185">tooreview hello 속성 hello hello 그룹의 hello 이름을 클릭 하는 추가 되 면 외부 그룹을 구성 하 고 **그룹** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-185">tooreview and configure hello properties for external groups once they have been added, click hello name of hello group from hello **Groups** tab.</span></span>

![그룹 관리][api-management-groups]

<span data-ttu-id="d5158-187">여기에서 hello를 편집할 수 있습니다 **이름** 및 hello **설명** hello 그룹의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-187">From here you can edit hello **Name** and hello **Description** of hello group.</span></span>

![그룹 편집][api-management-edit-group]

<span data-ttu-id="d5158-189">사용자 hello에서 구성 된 Azure Active Directory 수 뷰와 toohello 개발자 포털에 로그인 및 hello 지침 hello 섹션 다음에 따라 표시 여부를 가지는 tooany 그룹을 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-189">Users from hello configured Azure Active Directory can sign in toohello Developer portal and view and subscribe tooany groups for which they have visibility by following hello instructions in hello following section.</span></span>

## <a name="how-toolog-in-toohello-developer-portal-using-an-azure-active-directory-account"></a><span data-ttu-id="d5158-190">어떻게 toolog Azure Active Directory 계정을 사용 하 여 toohello 개발자 포털에서</span><span class="sxs-lookup"><span data-stu-id="d5158-190">How toolog in toohello Developer portal using an Azure Active Directory account</span></span>
<span data-ttu-id="d5158-191">hello 이전 섹션에 구성 된 Azure Active Directory 계정을 사용 하는 hello 개발자 포털에 toolog hello를 사용 하 여 새 브라우저 창을 열고 **로그온 URL** hello Active Directory 응용 프로그램 구성 및 클릭 **Azure Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-191">toolog into hello Developer portal using an Azure Active Directory account configured in hello previous sections, open a new browser window using hello **Sign-on URL** from hello Active Directory application configuration, and click **Azure Active Directory**.</span></span>

![개발자 포털][api-management-dev-portal-signin]

<span data-ttu-id="d5158-193">Azure Active Directory에 hello 사용자 중 하나의 hello 자격 증명을 입력 하 고 클릭 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-193">Enter hello credentials of one of hello users in your Azure Active Directory, and click **Sign in**.</span></span>

![로그인][api-management-aad-signin]

<span data-ttu-id="d5158-195">추가 정보가 필요한 경우 등록 양식과 함께 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-195">You may be prompted with a registration form if any additional information is required.</span></span> <span data-ttu-id="d5158-196">Hello 등록 양식을 완성 하 고 클릭 **등록**합니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-196">Complete hello registration form and click **Sign up**.</span></span>

![등록][api-management-complete-registration]

<span data-ttu-id="d5158-198">사용자는 이제 API 관리 서비스 인스턴스에 대 한 hello 개발자 포털에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5158-198">Your user is now logged into hello developer portal for your API Management service instance.</span></span>

![등록 완료][api-management-registration-complete]

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-security-external-identities.png
[api-management-security-aad-new]: ./media/api-management-howto-aad/api-management-security-aad-new.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-aad/api-management-new-aad-application-menu.png
[api-management-new-aad-application-1]: ./media/api-management-howto-aad/api-management-new-aad-application-1.png
[api-management-new-aad-application-2]: ./media/api-management-howto-aad/api-management-new-aad-application-2.png
[api-management-new-aad-app-created]: ./media/api-management-howto-aad/api-management-new-aad-app-created.png
[api-management-aad-app-permissions]: ./media/api-management-howto-aad/api-management-aad-app-permissions.png
[api-management-aad-app-client-id]: ./media/api-management-howto-aad/api-management-aad-app-client-id.png
[api-management-client-id]: ./media/api-management-howto-aad/api-management-client-id.png
[api-management-aad-key-before-save]: ./media/api-management-howto-aad/api-management-aad-key-before-save.png
[api-management-aad-key-after-save]: ./media/api-management-howto-aad/api-management-aad-key-after-save.png
[api-management-client-secret]: ./media/api-management-howto-aad/api-management-client-secret.png
[api-management-client-allowed-tenants]: ./media/api-management-howto-aad/api-management-client-allowed-tenants.png
[api-management-client-allowed-tenants-save]: ./media/api-management-howto-aad/api-management-client-allowed-tenants-save.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-aad/api-management-aad-delegated-permissions.png
[api-management-dev-portal-signin]: ./media/api-management-howto-aad/api-management-dev-portal-signin.png
[api-management-aad-signin]: ./media/api-management-howto-aad/api-management-aad-signin.png
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.png
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-aad-consent]: ./media/api-management-howto-aad/api-management-aad-consent.png
[api-management-permissions-form]: ./media/api-management-howto-aad/api-management-permissions-form.png
[api-management-configure-product]: ./media/api-management-howto-aad/api-management-configure-product.png
[api-management-add-groups]: ./media/api-management-howto-aad/api-management-add-groups.png
[api-management-select-group]: ./media/api-management-howto-aad/api-management-select-group.png
[api-management-aad-groups-list]: ./media/api-management-howto-aad/api-management-aad-groups-list.png
[api-management-aad-group-added]: ./media/api-management-howto-aad/api-management-aad-group-added.png
[api-management-groups]: ./media/api-management-howto-aad/api-management-groups.png
[api-management-edit-group]: ./media/api-management-howto-aad/api-management-edit-group.png

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing hello Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account

