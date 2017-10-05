---
title: "게시자 계정 만들기 및 등록 | Microsoft Docs"
description: "Microsoft 개발자 계정을 만들고 승인 시 Azure 마켓플레이스에서 다양한 제품 유형을 판매할 수 있는 지침입니다."
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 5a2fe68d-2967-463f-8af6-42bed07e3eaa
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: hascipio
ms.openlocfilehash: 642e4a2d11ef5a92f5ab46bc4872414966b04c0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-microsoft-developer-account"></a><span data-ttu-id="535fa-103">Microsoft 개발자 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="535fa-103">Create a Microsoft Developer account</span></span>
<span data-ttu-id="535fa-104">이 문서에서는 Azure 마켓플레이스에서 승인된 Microsoft 개발자가 되기 위해 필요한 계정 만들기 및 등록 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-104">This article walks you through the necessary account creation and registration process to become an approved Microsoft Developer for the Azure Marketplace.</span></span>

## <a name="1-create-a-microsoft-account"></a><span data-ttu-id="535fa-105">1. Microsoft 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="535fa-105">1. Create a Microsoft account</span></span>
<span data-ttu-id="535fa-106">게시 프로세스를 시작하려면 Microsoft 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-106">To start the publishing process, you will need to create a Microsoft account.</span></span> <span data-ttu-id="535fa-107">이 계정은 **Microsoft 개발자 센터** 및 **Azure 게시 포털**에 등록하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-107">This account will be used to register in to both the **Microsoft Developer Center** and **Azure Publishing Portal**.</span></span> <span data-ttu-id="535fa-108">Azure 마켓플레이스 제품에 대해 Microsoft 계정이 하나만 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-108">You should have only one Microsoft account for your Azure Marketplace offerings.</span></span> <span data-ttu-id="535fa-109">서비스 또는 제품에 한정될 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-109">It should not be specific to services or offers.</span></span>

<span data-ttu-id="535fa-110">사용자 이름을 구성하는 주소는 귀사의 도메인에 속하고 귀사의 IT 팀에서 제어해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-110">The address that forms the user name should be on your domain and controlled by your IT team.</span></span> <span data-ttu-id="535fa-111">모든 게시 관련 작업은 이 계정을 통해 수행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-111">All the publishing related activities should be done through this account.</span></span>

> [!WARNING]
> <span data-ttu-id="535fa-112">**"Azure"** 및 **"Microsoft"**와 같은 단어는 Microsoft 계정 등록에 대해 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-112">Words like **"Azure"** and **"Microsoft"** are not supported for Microsoft account registration.</span></span> <span data-ttu-id="535fa-113">계정 만들기 및 등록 프로세스를 완료하려면 이러한 단어를 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="535fa-113">Avoid using these words to complete the account creation and registration process.</span></span>
>
>

### <a name="guidelines-for-company-accounts"></a><span data-ttu-id="535fa-114">회사 계정에 대한 지침</span><span class="sxs-lookup"><span data-stu-id="535fa-114">Guidelines for company accounts</span></span>
<span data-ttu-id="535fa-115">회사 계정을 만들 때 둘 이상의 사용자가 계정을 연 Microsoft 계정으로 로그인하여 계정에 액세스해야 하는 경우 다음 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-115">When creating a company account, follow these guidelines if more than one person will need to access the account by logging in with the Microsoft account that opened the account.</span></span>

> [!Important]
> <span data-ttu-id="535fa-116">중요 여러 사용자가 개발자 센터 계정에 액세스할 수 있게 하려면 Azure Active Directory를 사용하여 개인 Azure AD 자격 증명으로 로그인하여 계정에 액세스할 수 있는 개별 사용자에게 역할을 할당하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-116">Important To allow multiple users to access your Dev Center account, we recommend using Azure Active Directory to assign roles to individual users, who can access the account by signing in with their individual Azure AD credentials.</span></span> <span data-ttu-id="535fa-117">자세한 내용은 [계정 사용자 관리](https://msdn.microsoft.com/en-us/windows/uwp/publish/manage-account-users)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="535fa-117">For more info, see [Manage account users](https://msdn.microsoft.com/en-us/windows/uwp/publish/manage-account-users).</span></span>

* <span data-ttu-id="535fa-118">회사 도메인에 속하지만 단일 개인이 아닌 전자 메일 주소(예: windowsapps@fabrikam.com)를 사용하여 Microsoft 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-118">Create your Microsoft account using an email address that belongs to your company's domain, but not to a single individual—for example, windowsapps@fabrikam.com.</span></span>
* <span data-ttu-id="535fa-119">이 Microsoft 계정에 대한 액세스를 최대한 적은 수의 개발자로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-119">Limit access to this Microsoft account to the smallest possible number of developers.</span></span>
* <span data-ttu-id="535fa-120">개발자 계정에 액세스해야 하는 모든 사람을 포함하는 회사 전자 메일 배포 목록을 설정하고 보안 정보에 이 전자 메일 주소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-120">Set up a corporate email distribution list that includes everyone who needs to access the developer account, and add this email address to your security info.</span></span> <span data-ttu-id="535fa-121">이렇게 하면 목록에 있는 모든 직원이 필요할 때 보안 코드를 받고 Microsoft 계정의 보안 정보를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-121">This allows all of the employees on the list to receive security codes when needed and to manage your Microsoft account’s security info.</span></span> <span data-ttu-id="535fa-122">배포 목록을 설정할 수 없는 경우 개인 전자 메일 계정 소유자는 메시지가 표시되면(예: 새 보안 정보가 계정에 추가되거나 새 장치에서 액세스해야 하는 경우) 보안 코드에 액세스하여 공유할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-122">If setting up a distribution list is not feasible, the owner of the individual email account will need to be available to access and share the security code when prompted (such as when new security info is added to the account or when it must be accessed from a new device).</span></span>
* <span data-ttu-id="535fa-123">확장할 필요가 없고 핵심 팀 구성원에 액세스할 수 있는 회사 전화 번호를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-123">Add a company phone number that does not require an extension and is accessible to key team members.</span></span>
* <span data-ttu-id="535fa-124">일반적으로 개발자가 신뢰할 수 있는 장치를 사용하여 회사의 개발자 계정에 로그인하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-124">In general, have developers use trusted devices to log in to your company's developer account.</span></span> <span data-ttu-id="535fa-125">모든 핵심 팀 구성원은 이러한 신뢰할 수 있는 장치에 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-125">All key team members should have access to these trusted devices.</span></span> <span data-ttu-id="535fa-126">이렇게 하면 계정에 액세스할 때 보안 코드를 전송할 필요성이 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-126">This will reduce the need for security codes to be sent when accessing the account.</span></span>
* <span data-ttu-id="535fa-127">신뢰할 수 없는 PC에서 계정에 액세스할 수 있도록 해야 하는 경우 해당 액세스를 최대 5명의 개발자로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-127">If you need to allow access to the account from a non-trusted PC, limit that access to a maximum of five developers.</span></span> <span data-ttu-id="535fa-128">이상적으로는 이러한 개발자가 동일한 지리적 네트워크 위치를 공유하는 컴퓨터에서 계정에 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-128">Ideally, these developers should access the account from machines that share the same geographical and network location.</span></span>
* <span data-ttu-id="535fa-129">[https://account.live.com/proofs/Manage](https://account.live.com/proofs/Manage)에서 회사의 보안 정보를 자주 검토하여 모두 최신 정보인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-129">Frequently review your company’s security info at [https://account.live.com/proofs/Manage](https://account.live.com/proofs/Manage) to make sure it's all current.</span></span>

<span data-ttu-id="535fa-130">개발자 계정은 주로 신뢰할 수 있는 PC에서 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-130">Your developer account should be accessed primarily from trusted PCs.</span></span> <span data-ttu-id="535fa-131">이는 주당 계정별로 생성되는 코드 수에 제한이 있기 때문에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-131">This is critical because there is a limit to the number of codes generated per account, per week.</span></span> <span data-ttu-id="535fa-132">또한 가장 원활한 로그인 환경을 가능하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-132">It also enables the most seamless sign-in experience.</span></span>

<span data-ttu-id="535fa-133">추가 개발자 계정 지침 및 보안에 대한 자세한 내용을 보려면 [여기](https://msdn.microsoft.com/en-us/windows/uwp/publish/opening-a-developer-account#additional-guidelines-for-company-accounts)를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="535fa-133">For more information on additional developer account guidelines and security, click [here](https://msdn.microsoft.com/en-us/windows/uwp/publish/opening-a-developer-account#additional-guidelines-for-company-accounts).</span></span>

### <a name="instructions"></a><span data-ttu-id="535fa-134">지침</span><span class="sxs-lookup"><span data-stu-id="535fa-134">Instructions</span></span>
1. <span data-ttu-id="535fa-135">새 Chrome Incognito 또는 Internet Explorer InPrivate 브라우징 세션을 열어 기존 계정에 로그인되지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-135">Open a new Chrome Incognito or Internet Explorer InPrivate browsing session to ensure that you’re not signed in to an existing account.</span></span>
2. <span data-ttu-id="535fa-136">[https://signup.live.com/signup.aspx](https://signup.live.com/signup.aspx) 링크를 사용하여 전자 메일(예: 위의 지침에 따라 windowsapp@fabrikam.com)을 Microsoft 계정으로 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-136">Register the email (per the guidelines above e.g. windowsapp@fabrikam.com) as a Microsoft account by using the link [https://signup.live.com/signup.aspx](https://signup.live.com/signup.aspx).</span></span> <span data-ttu-id="535fa-137">아래의 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="535fa-137">Follow the instructions below.</span></span>

   1. <span data-ttu-id="535fa-138">계정을 Microsoft 계정으로 등록하는 동안 시스템에서 문자 메시지 또는 자동 응답 통화 형태로 계정 확인 코드를 보낼 올바른 전화번호를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-138">During registering your account as a Microsoft account, you need to provide a valid phone number for the system to send you an account verification code as a text message or an automated call.</span></span>
   2. <span data-ttu-id="535fa-139">계정을 Microsoft 계정으로 등록하는 동안 계정 확인을 위해 자동 전자 메일을 수신하기 위한 올바른 전자 메일 ID를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-139">During registering your account as a Microsoft account, you need to provide a valid email id for receiving an automated email for account verification.</span></span>
3. <span data-ttu-id="535fa-140">DL에 전송된 메일 주소를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-140">Verify the email address sent to the DL.</span></span>
4. <span data-ttu-id="535fa-141">이제 Microsoft 개발자 센터에서 새 Microsoft 계정을 사용할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-141">You’re now ready to use the new Microsoft account in the Microsoft Developer Center.</span></span>

## <a name="2-register-your-account-in-microsoft-developer-center"></a><span data-ttu-id="535fa-142">2. Microsoft 개발자 센터에서 계정 등록</span><span class="sxs-lookup"><span data-stu-id="535fa-142">2. Register your account in Microsoft Developer Center</span></span>
<span data-ttu-id="535fa-143">Microsoft 개발자 센터는 회사 정보를 등록하는 데 한 번 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-143">The Microsoft Developer Center is used to register the company information once.</span></span> <span data-ttu-id="535fa-144">등록자는 회사의 정식 담당자여야 하며 신원을 확인할 수 있는 개인 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-144">The registrant must be a valid representative of the company, and must provide their personal information as a way to validate their identity.</span></span> <span data-ttu-id="535fa-145">등록자는 회사에서 공유되는 Microsoft 계정을 사용해야 하며 **동일한 계정을 Azure 게시 포털에서도 사용해야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="535fa-145">The person registering must use a Microsoft account that is shared for the company, **and the same account must be used in the Azure Publishing Portal.**</span></span> <span data-ttu-id="535fa-146">계정 만들기를 시작하기 전에 회사에 Microsoft 개발자 센터 계정이 아직 없는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-146">You should check to make sure your company does not already have a Microsoft Developer Center account before you attempt to create one.</span></span> <span data-ttu-id="535fa-147">프로세스 중에 회사 주소 정보, 은행 계좌 정보 및 세금 정보를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-147">During the process, we will collect company address information, bank account information, and tax information.</span></span> <span data-ttu-id="535fa-148">이러한 정보는 일반적으로 재무 또는 업무 연락처에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-148">These are typically obtainable from finance or business contacts.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="535fa-149">제품 만들기 및 배포의 여러 단계를 진행하기 위해서는 다음 개발자 프로필 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-149">You must complete the following Developer profile components in order to progress through the various phases of offer creation and deployment.</span></span>
>
>

| <span data-ttu-id="535fa-150">개발자 프로필</span><span class="sxs-lookup"><span data-stu-id="535fa-150">Developer profile</span></span> | <span data-ttu-id="535fa-151">초안 시작</span><span class="sxs-lookup"><span data-stu-id="535fa-151">To start draft</span></span> | <span data-ttu-id="535fa-152">스테이징</span><span class="sxs-lookup"><span data-stu-id="535fa-152">Staging</span></span> | <span data-ttu-id="535fa-153">무료 게시 및 솔루션 템플릿</span><span class="sxs-lookup"><span data-stu-id="535fa-153">Publish free and solution template</span></span> | <span data-ttu-id="535fa-154">상업적 게시</span><span class="sxs-lookup"><span data-stu-id="535fa-154">Publish commercial</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="535fa-155">회사 등록</span><span class="sxs-lookup"><span data-stu-id="535fa-155">Company registration</span></span> |<span data-ttu-id="535fa-156">필수</span><span class="sxs-lookup"><span data-stu-id="535fa-156">Must have</span></span> |<span data-ttu-id="535fa-157">필수</span><span class="sxs-lookup"><span data-stu-id="535fa-157">Must have</span></span> |<span data-ttu-id="535fa-158">필수</span><span class="sxs-lookup"><span data-stu-id="535fa-158">Must have</span></span> |<span data-ttu-id="535fa-159">필수</span><span class="sxs-lookup"><span data-stu-id="535fa-159">Must have</span></span> |
| <span data-ttu-id="535fa-160">세금 프로필 ID</span><span class="sxs-lookup"><span data-stu-id="535fa-160">Tax profile ID</span></span> |<span data-ttu-id="535fa-161">옵션</span><span class="sxs-lookup"><span data-stu-id="535fa-161">Optional</span></span> |<span data-ttu-id="535fa-162">옵션</span><span class="sxs-lookup"><span data-stu-id="535fa-162">Optional</span></span> |<span data-ttu-id="535fa-163">옵션</span><span class="sxs-lookup"><span data-stu-id="535fa-163">Optional</span></span> |<span data-ttu-id="535fa-164">필수</span><span class="sxs-lookup"><span data-stu-id="535fa-164">Must have</span></span> |
| <span data-ttu-id="535fa-165">은행 계좌</span><span class="sxs-lookup"><span data-stu-id="535fa-165">Bank account</span></span> |<span data-ttu-id="535fa-166">옵션</span><span class="sxs-lookup"><span data-stu-id="535fa-166">Optional</span></span> |<span data-ttu-id="535fa-167">옵션</span><span class="sxs-lookup"><span data-stu-id="535fa-167">Optional</span></span> |<span data-ttu-id="535fa-168">옵션</span><span class="sxs-lookup"><span data-stu-id="535fa-168">Optional</span></span> |<span data-ttu-id="535fa-169">필수</span><span class="sxs-lookup"><span data-stu-id="535fa-169">Must have</span></span> |

> [!NOTE]
> <span data-ttu-id="535fa-170">BYOL(사용자 라이선스 필요)은 가상 컴퓨터에만 지원되며 **무료** 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-170">Bring Your Own License (BYOL) is supported only for virtual machines and is considered a **free** offering.</span></span>
>
>

### <a name="register-your-company-account"></a><span data-ttu-id="535fa-171">회사 계정 등록</span><span class="sxs-lookup"><span data-stu-id="535fa-171">Register your company account</span></span>
1. <span data-ttu-id="535fa-172">새 Chrome Incognito 또는 Internet Explorer InPrivate 브라우징 세션을 열어 개인 계정에 로그인되지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-172">Open a new  Internet Explorer InPrivate or Chrome Incognito browsing session to ensure that you’re not signed in to a personal account.</span></span>
2. <span data-ttu-id="535fa-173">[http://dev.windows.com/registration?accountprogram=azure](http://dev.windows.com/registration?accountprogram=azure) 로 이동하여 개발자 센터에서 본인을 판매자로 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-173">Go to [http://dev.windows.com/registration?accountprogram=azure](http://dev.windows.com/registration?accountprogram=azure) to register yourself as a seller in the Dev Center.</span></span> <span data-ttu-id="535fa-174">계속 진행하기 전에 다음 중요 정보를 읽어 보세요.</span><span class="sxs-lookup"><span data-stu-id="535fa-174">Please read the following important note before you proceed.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="535fa-175">개발자 센터에서 등록하는 데 사용할 전자 메일 ID 또는 메일 그룹(개인 종속성을 제거하려면 메일 그룹이 권장됨)을 Microsoft 계정으로 처음 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-175">Ensure that the email id or distribution list (a distribution list is recommended to remove dependency from individuals) which you will be using for registering in the Dev Center is at first registered as a Microsoft account.</span></span> <span data-ttu-id="535fa-176">그러지 않은 경우 이 [링크](https://signup.live.com/signup?uaid=e479342fe2824efeb0c3d92c8f961fd3&lic=1)를 사용하여 등록하세요.</span><span class="sxs-lookup"><span data-stu-id="535fa-176">If not, then please register using this [link](https://signup.live.com/signup?uaid=e479342fe2824efeb0c3d92c8f961fd3&lic=1).</span></span> <span data-ttu-id="535fa-177">또한 개발자 센터 등록을 위해서는 **Microsoft 회사 도메인의 전자 메일 ID(예: @microsoft.com)는 사용할 수 없습니다**.</span><span class="sxs-lookup"><span data-stu-id="535fa-177">Also, **any email id under the Microsoft company domain i.e. @microsoft.com cannot be used** for Dev Center registration.</span></span>
   >
   >

    ![drawing][img-signin]
3. <span data-ttu-id="535fa-179">"계정 보호 지원" 마법사를 완료하여 전화 번호 또는 메일 주소를 통해 신원을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-179">Complete the "Help us protect your account" wizard, which will verify your identity via phone number or email address.</span></span>

    ![그리기][img-verify]
4. <span data-ttu-id="535fa-181">"등록 계정 정보" 섹션에서 드롭다운 메뉴의 **계정 국가/지역** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-181">In the "Registration-Account Info" section, select your **Account country/region** from the dropdown menu.</span></span>

    ![그리기](media/marketplace-publishing-accounts-creation-registration/imgRegisterCo_04.png)

   > [!WARNING]
   > <span data-ttu-id="535fa-183">**"판매" 국가:** Azure 마켓플레이스에서 서비스를 판매하기 위해서는 등록된 법인이 승인된 위의 “판매” 국가 중 하나에 속해 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-183">**"Sell-from" Countries:** In order to sell your services on the Azure Marketplace, your registered entity needs to be from one of the approved “sell-from” countries above.</span></span> <span data-ttu-id="535fa-184">이 제한은 지급액 및 세금 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-184">This restriction is for payout and taxation reasons.</span></span> <span data-ttu-id="535fa-185">Microsoft는 가까운 장래에 이 국가 목록을 확장하기 위해 적극 노력하고 있으니 기대해 주세요.</span><span class="sxs-lookup"><span data-stu-id="535fa-185">We are actively looking to expand this list of countries in the near future, so stay tuned.</span></span> <span data-ttu-id="535fa-186">자세한 내용은 [마켓플레이스 참가 정책](http://go.microsoft.com/fwlink/?LinkID=526833)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="535fa-186">For more information, see the  [Marketplace participation policies](http://go.microsoft.com/fwlink/?LinkID=526833).</span></span>
   >
   >
5. <span data-ttu-id="535fa-187">"계정 형식"으로 **회사**를 선택하고 **다음** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-187">Select your "Account Type" as **Company** and then click the **Next** button.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="535fa-188">계정 형식에 대한 이해를 돕고 여러분을 위한 적합한 선택이 무엇인지 알려면 [계정 형식, 위치 및 수수료](https://msdn.microsoft.com/library/windows/apps/jj863494.aspx)</span><span class="sxs-lookup"><span data-stu-id="535fa-188">To better understand account types and which is best for you to choose, please view page [Account types, locations, and fees](https://msdn.microsoft.com/library/windows/apps/jj863494.aspx)</span></span>
   >
   >

    ![drawing](media/marketplace-publishing-accounts-creation-registration/imgRegisterCo_05.png)
6. <span data-ttu-id="535fa-190">**게시자 표시 이름**을 입력합니다. 이는 일반적으로 여러분의 회사 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-190">Enter the **Publisher display name**, typically the name of your company.</span></span>

   > [!TIP]
   > <span data-ttu-id="535fa-191">개발자 센터에 입력한 게시자 표시 이름은 제공 제품이 나열될 때 Azure 마켓플레이스에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-191">The publisher display name entered in the Dev Center is not displayed in the Azure Marketplace once your offer goes listed.</span></span> <span data-ttu-id="535fa-192">하지만 등록 프로세스를 완료하려면 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-192">But this must be filled to complete the registration process.</span></span>
   >
   >
7. <span data-ttu-id="535fa-193">계정 확인을 위한 **연락처 정보** 를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-193">Enter the **Contact info** for the account verification.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="535fa-194">개발자 센터에서 승인된 회사에 대한 확인 프로세스에 사용되므로 정확한 연락처 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-194">You must provide accurate contact information because it will be used in our verification process for your company to be approved in the Developer Center.</span></span>
   >
   >
8. <span data-ttu-id="535fa-195">**회사 승인자**의 연락처 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-195">Enter the contact information for the **Company Approver**.</span></span> <span data-ttu-id="535fa-196">회사 승인자는 조직을 대신하여 개발자 센터에서 계정을 만드는 권한이 있는 사람을 확인할 수 있는 사람입니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-196">Company approver is the person who can verify that you are authorized to create an account in the Dev Center on behalf of your organization.</span></span> <span data-ttu-id="535fa-197">작업을 마쳤으면 **다음**을 클릭하여 **"지급 섹션"**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-197">Click on **Next** to move to the **"Payment section"** once you are finished.</span></span>

    ![drawing](media/marketplace-publishing-accounts-creation-registration/imgRegisterCo_08.png)
9. <span data-ttu-id="535fa-199">결제 정보를 입력하여 해당 계정에 대한 비용을 지불합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-199">Enter your payment info to pay for your account.</span></span> <span data-ttu-id="535fa-200">등록 비용을 부담하는 프로모션 코드를 가지고 있는 경우 여기에 프로모션 코드를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-200">If you have a promo code that covers the cost of registration, you can enter that here.</span></span> <span data-ttu-id="535fa-201">그렇지 않은 경우 신용 카드 정보(또는 지원되는 시장에서 PayPal)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-201">Otherwise, provide your credit card info (or PayPal in supported markets).</span></span> <span data-ttu-id="535fa-202">작업을 마쳤으면 **다음**을 클릭하여 **"검토 화면"**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-202">When you are finished, click **Next** to move on to the **"Review screen"**.</span></span>

    ![drawing](media/marketplace-publishing-accounts-creation-registration/imgRegisterCo_09.png)
10. <span data-ttu-id="535fa-204">계정 정보를 검토하고 모든 정보가 올바른지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-204">Review your account info and confirm that everything is correct.</span></span> <span data-ttu-id="535fa-205">그런 다음 [Microsoft Azure 마켓플레이스 판매자 계약](http://go.microsoft.com/fwlink/?LinkID=699560)의 약관을 읽고 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-205">Then, read and accept the terms and conditions of the [Microsoft Azure Marketplace Publisher Agreement](http://go.microsoft.com/fwlink/?LinkID=699560).</span></span> <span data-ttu-id="535fa-206">확인란을 선택하여 이러한 약관을 읽고 동의했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-206">Check the box to indicate you have read and accepted these terms.</span></span>
11. <span data-ttu-id="535fa-207">**마침** 을 클릭하여 등록을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-207">Click **Finish** to confirm your registration.</span></span> <span data-ttu-id="535fa-208">메일 주소로 확인 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-208">We'll send a confirmation message to your email address.</span></span>
12. <span data-ttu-id="535fa-209">무료 제품만 게시할 계획인 경우 **Azure 마켓플레이스 게시 포털로 이동** 을 클릭하여 이 문서의 섹션 3, [게시 포털에서 계정 등록](#3-register-your-account-in-the-publishing-portal)을 건너뛰어도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-209">If you are planning to publish only free offers, click **Go to Azure Marketplace Publishing Portal** and you can skip to section 3 of this document, [Register your account in the publishing portal](#3-register-your-account-in-the-publishing-portal).</span></span>

<span data-ttu-id="535fa-210">상업용 제품(예: 시간별로 요금이 청구되는 가상 컴퓨터 제품)을 게시할 계획인 경우 개발자 센터 계정에서 세금 및 은행 정보를 완료해야 하는 **계정 정보 업데이트** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-210">If you are planning to publish commercial offers (e.g. Virtual Machine offers with hourly billing model), click **Update your account information** where you must fill in the tax and banking information in your Developer Center account.</span></span>

<span data-ttu-id="535fa-211">나중에 세금 및 은행 정보를 업데이트하려는 경우 다음 섹션(예: 이 문서의 섹션 3, [게시 포털에서 계정 등록](#3-register-your-account-in-the-publishing-portal))으로 이동했다가 Azure 게시 포털의 링크를 사용하여 나중에 다시 돌아올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-211">If you prefer to update your tax and bank information later, then you can move to the next section i.e. section 3 of this document, [Register your account in the publishing portal](#3-register-your-account-in-the-publishing-portal), and come back later by using links in the Azure Publishing Portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="535fa-212">상업용 제품의 경우 세금 및 은행 계좌 정보를 업데이트하지 않으면 제품을 프로덕션으로 푸시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-212">In case of commercial offers, you will not be able to push your offers to production without completing the tax and bank account information.</span></span>
>
>

<span data-ttu-id="535fa-213">나중에 세금 및 은행 정보를 업데이트하려는 경우 섹션 3, [게시 포털에서 계정 등록](#3-register-your-account-in-the-publishing-portal)으로 이동했다가 Azure 게시 포털의 링크를 사용하여 나중에 다시 돌아올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-213">If you prefer to update your tax and bank information later, you can go to section 3, [Register your account in the publishing portal](#3-register-your-account-in-the-publishing-portal), and come back later by using links in the Azure Publishing Portal.</span></span>

### <a name="add-tax-and-banking-information"></a><span data-ttu-id="535fa-214">세금 및 은행 정보 추가</span><span class="sxs-lookup"><span data-stu-id="535fa-214">Add tax and banking information</span></span>
 <span data-ttu-id="535fa-215">구매를 위한 상업용 제품을 게시하려는 경우 지급액 및 세금 정보를 추가하고 개발자 센터에서 확인을 위해 제출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-215">If you want to publish commercial offers for purchase, you also need to add payout and tax information and submit it for validation in the Developer Center.</span></span> <span data-ttu-id="535fa-216">무료 제품만(또는 BYOL 제품) 게시하는 경우 이 정보를 추가할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-216">If you will publish only free offers (or BYOL offers), then you do not need to add this information.</span></span> <span data-ttu-id="535fa-217">나중에 추가해도 되지만 세금 정보를 확인하는 데 시간이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-217">You can add it later, but it takes some time to validate the tax information.</span></span> <span data-ttu-id="535fa-218">구매를 위한 상업용 제품을 제공할 것을 알고 있다면 가능한 빨리 추가하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-218">If you know that you will offer commercial offers for purchase, we recommend that you add it as soon as possible.</span></span>

<span data-ttu-id="535fa-219">**은행 정보**</span><span class="sxs-lookup"><span data-stu-id="535fa-219">**Bank Information**</span></span>

1. <span data-ttu-id="535fa-220">Microsoft 계정을 사용하여 [Microsoft 개발자 센터](http://dev.windows.com/registration?accountprogram=azure) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-220">Sign in to the [Microsoft Developer Center](http://dev.windows.com/registration?accountprogram=azure) with your Microsoft account.</span></span>
2. <span data-ttu-id="535fa-221">왼쪽 메뉴에서 **지급 계좌**를 클릭하고 **지불 방법 선택** 아래에서 **은행 계좌** 또는 **PayPal**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-221">Click **Payout account** in the left menu, under **Choose payment method** click **Bank account** or **PayPal**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="535fa-222">마켓플레이스에서 고객이 구매하는 상업용 제품인 경우 이 계좌로 해당 구매에 대한 지급액을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-222">If you have commercial offers that customers purchase in the Marketplace, this is the account where you will receive payout for those purchases.</span></span>
   >
   >
3. <span data-ttu-id="535fa-223">결제 정보를 입력하고 만족할 경우 **저장** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-223">Enter the payment info, and click **Save** when you are satisfied.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="535fa-224">지급 계좌를 업데이트하거나 변경해야 하는 경우 위의 동일한 단계를 따라 현재 정보를 새 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-224">If you need to update or change your payout account, follow the same steps above, replacing the current info with the new info.</span></span> <span data-ttu-id="535fa-225">지급 계좌를 변경하면 한 번의 지불 주기까지 지불을 연기할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-225">Changing your payout account can delay your payments by up to one payment cycle.</span></span> <span data-ttu-id="535fa-226">이러한 지불 연기는 처음 지급 계좌를 설정할 때와 마찬가지로 계정 변경 내용을 확인해야 하기 때문에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-226">This delay occurs because we need to verify the account change, just as we did when you first set up the payout account.</span></span> <span data-ttu-id="535fa-227">계정 확인 작업이 끝난 후 여전히 전체 금액에 대해 비용을 지불해야 하는 경우 현재 지불 주기에 대한 모든 지불 대금이 다음 주기에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-227">You'll still get paid for the full amount after your account has been verified; any payments due for the current payment cycle will be added to the next one.</span></span>
   >
   >
4. <span data-ttu-id="535fa-228">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-228">Click **Next**.</span></span>

<span data-ttu-id="535fa-229">**세금 정보**</span><span class="sxs-lookup"><span data-stu-id="535fa-229">**Tax Information**</span></span>

1. <span data-ttu-id="535fa-230">Microsoft 계정을 사용하여(필요한 경우) [Microsoft 개발자 센터](http://dev.windows.com/registration?accountprogram=azure) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-230">Sign in to the [Microsoft Developer Center](http://dev.windows.com/registration?accountprogram=azure) with your Microsoft account (if needed).</span></span>
2. <span data-ttu-id="535fa-231">왼쪽 메뉴에서 **세금 프로필** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-231">Click **Tax profile** in the left menu.</span></span>
3. <span data-ttu-id="535fa-232">**세금 양식 작성** 페이지에서 영주권이 있는 국가 또는 지역을 선택한 후 주요 시민권을 보유한 국가 또는 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-232">On the **Set up your tax form** page, select the country or region where you have permanent residency, and then select the country or region where you hold primary citizenship.</span></span> <span data-ttu-id="535fa-233">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-233">Click **Next**.</span></span>
4. <span data-ttu-id="535fa-234">세금 세부 정보를 입력하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-234">Enter your tax details, and then click **Next**.</span></span>

> [!WARNING]
> <span data-ttu-id="535fa-235">Microsoft 개발자 센터 계정에서 세금 및 은행 계좌 정보를 완료하지 않으면 상업용 제품을 프로덕션으로 푸시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-235">You will not be able to push to production your commercial offers without completing the tax and bank account information in your Microsoft Developer Center account.</span></span>
>
>

<span data-ttu-id="535fa-236">개발자 센터 등록에 문제가 있으면 아래와 같이 지원 티켓을 기록하세요.</span><span class="sxs-lookup"><span data-stu-id="535fa-236">If you have issues with Developer Center registration, please log a support ticket as below</span></span>

1. <span data-ttu-id="535fa-237">지원 링크 [https://developer.microsoft.com/windows/support](https://developer.microsoft.com/windows/support)</span><span class="sxs-lookup"><span data-stu-id="535fa-237">Go to the support link [https://developer.microsoft.com/windows/support](https://developer.microsoft.com/windows/support)</span></span>
2. <span data-ttu-id="535fa-238">**문의처** 섹션 아래에서 **문제 제출** 버튼을 클릭합니다(아래 스크린샷 참조).</span><span class="sxs-lookup"><span data-stu-id="535fa-238">Under **Contact Us** section, click on the button **Submit an incident** (as shown in the screenshot below)</span></span>

    ![drawing](media/marketplace-publishing-accounts-creation-registration/imgAddTax_02.png)
3. <span data-ttu-id="535fa-240">**문제 형식**으로 "개발자 센터 도움말"을 선택하고 **범주**로 "앱 게시 및 관리"를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-240">Choose "Help with Dev Center" as **Problem type** and "Publish and manage apps" as **Category**.</span></span> <span data-ttu-id="535fa-241">그 다음에 "전자 메일 시작" 버튼을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-241">After that click on the button "Start email".</span></span>

    ![그리기](media/marketplace-publishing-accounts-creation-registration/imgAddTax_03.png)
4. <span data-ttu-id="535fa-243">로그인 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-243">You will be provided with a login page.</span></span> <span data-ttu-id="535fa-244">Microsoft 계정 로그인을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-244">Use any Microsoft account sign in.</span></span> <span data-ttu-id="535fa-245">Microsoft 계정이 없는 경우 이 [링크](https://signup.live.com/signup?uaid=0089f09ccae94043a0f07c2aaf928831&lic=1)를 사용하여 하나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-245">If you do not have a Microsoft account then create one using this [link](https://signup.live.com/signup?uaid=0089f09ccae94043a0f07c2aaf928831&lic=1).</span></span>
5. <span data-ttu-id="535fa-246">문제 세부 정보를 입력한 후 **제출** 버튼을 클릭하여 티켓을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-246">Fill in the details of the issue and subit the ticket by clicking on the **Submit** button.</span></span>

    ![drawing](media/marketplace-publishing-accounts-creation-registration/imgAddTax_05.png)

## <a name="3-register-your-account-in-the-publishing-portal"></a><span data-ttu-id="535fa-248">3. 게시 포털에서 계정 등록</span><span class="sxs-lookup"><span data-stu-id="535fa-248">3. Register your account in the publishing portal</span></span>
<span data-ttu-id="535fa-249">[게시 포털](http://publish.windowsazure.com) 은 제품을 게시하고 관리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-249">The [Publishing portal](http://publish.windowsazure.com) is used to publish and manage your offer(s).</span></span>

1. <span data-ttu-id="535fa-250">새 Chrome Incognito 또는 Internet Explorer InPrivate 검색 세션을 열어 개인 계정에 로그인되지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-250">Open a new Chrome Incognito or Internet Explorer InPrivate browsing session to ensure that you’re not signed in to a personal account.</span></span>
2. <span data-ttu-id="535fa-251">[http://publish.windowsazure.com](http://publish.windowsazure.com)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-251">Go to [http://publish.windowsazure.com](http://publish.windowsazure.com).</span></span>
3. <span data-ttu-id="535fa-252">새 사용자이며, 게시 포털에 처음으로 로그인하는 경우 개발자 센터 계정이 등록된 동일한 전자 메일 ID를 사용하여 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-252">If you are a new user and signing in to the Publishing portal for the first time, then you must sign in with the same email id with which your Dev Center account is registered.</span></span> <span data-ttu-id="535fa-253">이러한 방식으로 개발자 센터 계정 및 게시 포털 계정이 서로 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-253">In this way your Dev Center account and Publishing portal account will be linked with each other.</span></span> <span data-ttu-id="535fa-254">나중에 다음 단계를 수행하여 응용 프로그램에 대해 작업 중인 회사의 다른 멤버를 게시 포털에 공동 관리자로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-254">You can later add the other members of the company, who are working on the application, as a co-admin in the Publishing portal by following the steps below.</span></span>

<span data-ttu-id="535fa-255">게시 포털에서 공동 관리자로 추가되면 공동 관리자 계정을 사용하여 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-255">If you are added as a co-admin in the Publishing portal, then you can sign in with your co-admin account.</span></span>

> [!TIP]
> <span data-ttu-id="535fa-256">참가 정책은 [Azure 웹 사이트](https://azure.microsoft.com/support/legal/marketplace/participation-policies/)에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-256">The participation policies are described on the [Azure website](https://azure.microsoft.com/support/legal/marketplace/participation-policies/).</span></span>
>
>

## <a name="4-steps-to-add-a-co-admin-in-the-publishing-portal"></a><span data-ttu-id="535fa-257">4. 게시 포털에 공동 관리자를 추가하는 단계</span><span class="sxs-lookup"><span data-stu-id="535fa-257">4. Steps to add a co-admin in the Publishing portal</span></span>
<span data-ttu-id="535fa-258">**관리자인 경우** 아래에서 공동 관리자 추가 단계를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="535fa-258">**Assuming that you are the admin,** given below are the steps to add a co-admin.</span></span>

> [!NOTE]
> <span data-ttu-id="535fa-259">**새 사용자인 경우** 게시에 포털에 공동 관리자를 추가하기 전에 게시 포털에서 하나 이상의 응용 프로그램을 만들었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-259">**For the new users,** before you add a co-admin in the Publishing portal, ensure that you have created at least one application in the Publishing portal.</span></span> <span data-ttu-id="535fa-260">**게시자** 탭은 게시 포털에서 하나 이상의 응용 프로그램을 만든 이후에만 나타나기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-260">This is required as the **PUBLISHERS** tab appear only after creating at least one application in the Publishing portal.</span></span>
>
>

1. <span data-ttu-id="535fa-261">공동 관리자 전자 메일 ID가 MSA(Microsoft 계정)인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-261">Ensure that the co-admin email id is a Microsoft account(MSA).</span></span> <span data-ttu-id="535fa-262">그렇지 않은 경우 이 [링크](https://signup.live.com/signup?uaid=0089f09ccae94043a0f07c2aaf928831&lic=1)를 사용하여 MSA로 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-262">If not, register it as a MSA using this [link](https://signup.live.com/signup?uaid=0089f09ccae94043a0f07c2aaf928831&lic=1).</span></span>
2. <span data-ttu-id="535fa-263">공동 관리자를 추가하려고 하기 전에 관리자 계정 아래에 있는지 하나 이상의 응용 프로그램이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-263">Ensure that there is at least one application under the admin account before trying to add a co-admin.</span></span>
3. <span data-ttu-id="535fa-264">위 단계를 수행했으면 공동 관리자 전자 메일 ID를 사용하여 게시 포털에 로그인한 후 다시 로그아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-264">After the above steps are done, login to the Publishing portal with the co-admin email id and then log out.</span></span>
4. <span data-ttu-id="535fa-265">이제 관리자 전자 메일 ID를 사용하여 게시 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-265">Now login to the Publishing portal with the admin email id.</span></span>
5. <span data-ttu-id="535fa-266">게시자->계정 선택->관리자->공동 관리자 추가로 이동합니다(아래 스크린샷 참조).</span><span class="sxs-lookup"><span data-stu-id="535fa-266">Navigate to Publishers->select your account->Administrators->Add the co-admin (screenshot given below)</span></span>

   ![drawing](media/marketplace-publishing-accounts-creation-registration/imgAddAdmin_05.png)

## <a name="5-steps-to-delete-a-co-admin-in-the-publishing-portal"></a><span data-ttu-id="535fa-268">5. 게시 포털에서 공동 관리자를 삭제하는 단계</span><span class="sxs-lookup"><span data-stu-id="535fa-268">5. Steps to delete a co-admin in the Publishing portal</span></span>
<span data-ttu-id="535fa-269">**관리자인 경우** 아래에서 공동 관리자 삭제 단계를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="535fa-269">**Assuming that you are the admin,** given below are the steps to delete a co-admin.</span></span>

1. <span data-ttu-id="535fa-270">관리자 전자 메일 ID를 사용하여 게시 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-270">Login to the Publishing portal with the admin email id.</span></span>
2. <span data-ttu-id="535fa-271">**게시자**로 이동하여 계정을 선택하고 **관리자** -> **공동 관리자**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-271">Navigate to **Publishers** -> select your account -> **Administrators** -> **Co-Admins**.</span></span>
3. <span data-ttu-id="535fa-272">삭제하려는 공동 관리자 옆의 **X** 단추를 클릭합니다(아래에서 스크린샷 제공).</span><span class="sxs-lookup"><span data-stu-id="535fa-272">Click on the **X** button next to the co-admin you want tot delete (screenshot given below).</span></span>

    ![그리기](media/marketplace-publishing-accounts-creation-registration/imgDeleteAdmin_03.png)

## <a name="next-steps"></a><span data-ttu-id="535fa-274">다음 단계</span><span class="sxs-lookup"><span data-stu-id="535fa-274">Next steps</span></span>
<span data-ttu-id="535fa-275">계정을 만들고 등록했으므로 [비기술 필수 구성 요소](marketplace-publishing-pre-requisites.md)를 검토하여 제품을 게시하기 위한 모든 일반 필수 조건을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="535fa-275">Now that your account is created and registered, ensure you fulfill or meet all of the non-technical pre-requisites to publish your offer by reviewing [Non-technical pre-requisites](marketplace-publishing-pre-requisites.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="535fa-276">참고 항목</span><span class="sxs-lookup"><span data-stu-id="535fa-276">See also</span></span>
* [<span data-ttu-id="535fa-277">시작: Azure 마켓플레이스에 제품을 게시하는 방법</span><span class="sxs-lookup"><span data-stu-id="535fa-277">Getting started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

[img-msalive]:media/marketplace-publishing-accounts-creation-registration/creating-msa-account-msa-live.jpg
[img-email]:media/marketplace-publishing-accounts-creation-registration/creating-msa-account-msa-verifyemail.jpg
[img-sd-url]:media/marketplace-publishing-accounts-creation-registration/seller-dashboard-incognito.jpg
[img-signin]:media/marketplace-publishing-accounts-creation-registration/seller-dashboard-login.jpg
[img-verify]:media/marketplace-publishing-accounts-creation-registration/seller-dashboard-verify.jpg
[img-sd-top]:media/marketplace-publishing-accounts-creation-registration/seller-dashboard-personal-acc-details.jpg
[img-sd-info]:media/marketplace-publishing-accounts-creation-registration/seller-dashboard-personal.jpg
[img-sd-type]:media/marketplace-publishing-accounts-creation-registration/seller-dashboard-personal-acc-type.jpg
[img-sd-mktg1]:media/marketplace-publishing-accounts-creation-registration/seller-dashboard-personal-comp-det1.jpg
[img-sd-mktg2]:media/marketplace-publishing-accounts-creation-registration/seller-dashboard-personal-comp-det2.jpg
[img-sd-addr]:media/marketplace-publishing-accounts-creation-registration/seller-dashboard-personal-comp-add.jpg
[img-sd-legal]:media/marketplace-publishing-accounts-creation-registration/seller-dashboard-personal-cmp.jpg
[img-sd-submit]:media/marketplace-publishing-accounts-creation-registration/seller-dashboard-approval.jpg

[link-msdndoc]: https://msdn.microsoft.com/library/jj552460.aspx
[link-sellerdashboard]: http://sellerdashboard.microsoft.com/
[link-pubportal]: https://publish.windowsazure.com
[link-single-vm]:marketplace-publishing-vm-image-creation.md
[link-single-vm-prereq]:marketplace-publishing-vm-image-creation-prerequisites.md
[link-multi-vm]:marketplace-publishing-solution-template-creation.md
[link-multi-vm-prereq]:marketplace-publishing-solution-template-creation-prerequisites.md
[link-datasvc]:marketplace-publishing-data-service-creation.md
[link-datasvc-prereq]:marketplace-publishing-data-service-creation-prerequisites.md
[link-devsvc]:marketplace-publishing-dev-service-creation.md
[link-devsvc-prereq]:marketplace-publishing-dev-service-creation-prerequisites.md
[link-pushstaging]:marketplace-publishing-push-to-staging.md
