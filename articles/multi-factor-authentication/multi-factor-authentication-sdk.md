---
title: "사용자 지정 앱에 대 한 소프트웨어 개발 키트 aaaMFA | Microsoft Docs"
description: "이 문서 toodownload 및 사용 하 여 사용자 지정 응용 프로그램을 위한 Azure MFA SDK tooenable 2 단계 인증을 hello 방법을 보여 줍니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1c152f67-be02-42a5-a0c7-246fb6b34377
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 10e02e844bf3928575bfca79dbc34717a31a08b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a><span data-ttu-id="dc0a2-103">Multi-Factor Authentication을 사용자 지정 앱(SDK)으로 빌드하기</span><span class="sxs-lookup"><span data-stu-id="dc0a2-103">Building Multi-Factor Authentication into Custom Apps (SDK)</span></span>

<span data-ttu-id="dc0a2-104">로그인 hello hello Azure Multi-factor Authentication 소프트웨어 개발 키트 (SDK)에 직접 2 단계 인증을 빌드할 수 있습니다 또는 Azure AD 테 넌 트에 응용 프로그램의 트랜잭션을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-104">hello Azure Multi-Factor Authentication Software Development Kit (SDK) lets you build two-step verification directly into hello sign-in or transaction processes of applications in your Azure AD tenant.</span></span>

<span data-ttu-id="dc0a2-105">C#, Visual Basic (.NET), Java, Perl, PHP, 및 Ruby 용 Multi-factor Authentication SDK hello ´ ù.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-105">hello Multi-Factor Authentication SDK is available for C#, Visual Basic (.NET), Java, Perl, PHP, and Ruby.</span></span> <span data-ttu-id="dc0a2-106">hello SDK 2 단계 인증에 대 한 씬 래퍼를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-106">hello SDK provides a thin wrapper around two-step verification.</span></span> <span data-ttu-id="dc0a2-107">필요한 모든 것 toowrite 주석 처리 된 소스 코드 파일, 예제 파일, 자세한 추가 정보 파일 등 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-107">It includes everything you need toowrite your code, including commented source code files, example files, and a detailed ReadMe file.</span></span> <span data-ttu-id="dc0a2-108">또한 각 SDK에는 인증서와 고유 tooyour Multi-factor Authentication 공급자가 트랜잭션을 암호화 하기 위한 개인 키 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-108">Each SDK also includes a certificate and private key for encrypting transactions that are unique tooyour Multi-Factor Authentication Provider.</span></span> <span data-ttu-id="dc0a2-109">공급자가 있으면으로 필요한 만큼 많은 언어와 형식에 hello SDK를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-109">As long as you have a provider, you can download hello SDK in as many languages and formats as you need.</span></span>

<span data-ttu-id="dc0a2-110">hello Multi-factor Authentication SDK의에서 Api hello의 hello 구조는 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-110">hello structure of hello APIs in hello Multi-Factor Authentication SDK is simple.</span></span> <span data-ttu-id="dc0a2-111">Hello 다단계 옵션 매개 변수 (예: 확인 모드) 및 사용자 데이터 (예: 전화 번호 toocall hello 또는 PIN 번호 toovalidate hello)를 사용 하 여 tooan API를 호출 하는 단일 함수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-111">Make a single function call tooan API with hello multi-factor option parameters (like verification mode) and user data (like hello telephone number toocall or hello PIN number toovalidate).</span></span> <span data-ttu-id="dc0a2-112">hello Api 번역 hello 함수 호출 웹 서비스 요청 toohello에 클라우드 기반 Azure Multi-factor Authentication 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-112">hello APIs translate hello function call into web services requests toohello cloud-based Azure Multi-Factor Authentication Service.</span></span> <span data-ttu-id="dc0a2-113">모든 호출은 모든 SDK에 포함 된 참조 toohello 개인 인증서를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-113">All calls must include a reference toohello private certificate that is included in every SDK.</span></span>

<span data-ttu-id="dc0a2-114">Hello Api에는 Azure Active Directory에 등록 하는 액세스 toousers 없으므로 파일이 나 데이터베이스에서 사용자 정보를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-114">Because hello APIs do not have access toousers registered in Azure Active Directory, you must provide user information in a file or database.</span></span> <span data-ttu-id="dc0a2-115">또한 hello Api 제공 하지 않습니다 등록 또는 사용자 관리 기능, toobuild 필요 하므로 이러한 프로세스를 응용 프로그램으로.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-115">Also, hello APIs do not provide enrollment or user management features, so you need toobuild these processes into your application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dc0a2-116">toodownload SDK hello Azure MFA, AAD Premium 또는 EMS 라이선스를 보유 하는 경우에 Azure Multi-factor Auth 공급자 toocreate 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-116">toodownload hello SDK, you need toocreate an Azure Multi-Factor Auth Provider even if you have Azure MFA, AAD Premium, or EMS licenses.</span></span> <span data-ttu-id="dc0a2-117">이 목적을 위해 Azure Multi-factor Auth 공급자를 만들 이미 라이선스를 보유 하는 경우 확인 hello로 있는지 toocreate hello 공급자 **활성화 된 사용자별** 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-117">If you create an Azure Multi-Factor Auth Provider for this purpose and already have licenses, make sure toocreate hello Provider with hello **Per Enabled User** model.</span></span> <span data-ttu-id="dc0a2-118">그런 다음 연결할 hello Azure MFA, Azure AD Premium 또는 EMS 라이선스를 포함 하는 hello 공급자 toohello 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-118">Then, link hello Provider toohello directory that contains hello Azure MFA, Azure AD Premium, or EMS licenses.</span></span> <span data-ttu-id="dc0a2-119">이 구성을 통해만 hello hello 소유한 라이선스 개수 보다 SDK를 사용 하 여 더 많은 고유 사용자가 있는 경우 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-119">This configuration ensures that you are only billed if you have more unique users using hello SDK than hello number of licenses you own.</span></span>


## <a name="download-hello-sdk"></a><span data-ttu-id="dc0a2-120">Hello SDK 다운로드</span><span class="sxs-lookup"><span data-stu-id="dc0a2-120">Download hello SDK</span></span>
<span data-ttu-id="dc0a2-121">Hello Azure Multi-factor SDK를 다운로드 하려면는 [Azure Multi-factor Auth 공급자](multi-factor-authentication-get-started-auth-provider.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-121">Downloading hello Azure Multi-Factor SDK requires an [Azure Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md).</span></span>  <span data-ttu-id="dc0a2-122">따라서 Azure MFA, Azure AD Premium 또는 Enterprise Mobility Suite 라이선스가 있는 경우에도 전체 Azure 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-122">This requires a full Azure subscription, even if Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses are owned.</span></span>  <span data-ttu-id="dc0a2-123">toodownload hello SDK, toohello Multi-factor 관리 포털을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-123">toodownload hello SDK, navigate toohello Multi-Factor Management Portal.</span></span> <span data-ttu-id="dc0a2-124">Hello 포털 hello Multi-factor Auth 공급자를 직접 관리 하거나 hello를 클릭 하 여 도달할 수 **"Go toohello 포털"** hello MFA 서비스 설정 페이지에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-124">You can reach hello portal either by managing hello Multi-Factor Auth Provider directly, or by clicking hello **"Go toohello portal"** link on hello MFA service settings page.</span></span>

### <a name="download-from-hello-azure-classic-portal"></a><span data-ttu-id="dc0a2-125">Hello Azure 클래식 포털에서 다운로드</span><span class="sxs-lookup"><span data-stu-id="dc0a2-125">Download from hello Azure classic portal</span></span>
1. <span data-ttu-id="dc0a2-126">Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com) 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-126">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="dc0a2-127">Hello 왼쪽에서 선택 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-127">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="dc0a2-128">Hello 상위 선택에 hello Active Directory 페이지 **Multi-factor Auth 공급자**</span><span class="sxs-lookup"><span data-stu-id="dc0a2-128">On hello Active Directory page, at hello top select **Multi-Factor Auth Providers**</span></span>
4. <span data-ttu-id="dc0a2-129">Hello 맨 아래에 선택 **관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-129">At hello bottom select **Manage**.</span></span> <span data-ttu-id="dc0a2-130">새 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-130">A new page opens.</span></span>
5. <span data-ttu-id="dc0a2-131">Hello 맨 아래에 남은 hello 클릭 **SDK**합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-131">On hello left, at hello bottom, click **SDK**.</span></span>
   <span data-ttu-id="dc0a2-132"><center>![다운로드](./media/multi-factor-authentication-sdk/download.png)</center></span><span class="sxs-lookup"><span data-stu-id="dc0a2-132"><center>![Download](./media/multi-factor-authentication-sdk/download.png)</center></span></span>
6. <span data-ttu-id="dc0a2-133">하나의 hello 관련 된 다운로드 링크를 클릭 hello 언어를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-133">Select hello language you want and click one hello associated download links.</span></span>
7. <span data-ttu-id="dc0a2-134">Hello 다운로드를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-134">Save hello download.</span></span>

### <a name="download-from-hello-service-settings"></a><span data-ttu-id="dc0a2-135">Hello 서비스 설정에서 다운로드</span><span class="sxs-lookup"><span data-stu-id="dc0a2-135">Download from hello service settings</span></span>
1. <span data-ttu-id="dc0a2-136">Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com) 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-136">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="dc0a2-137">Hello 왼쪽에서 선택 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-137">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="dc0a2-138">Azure AD 인스턴스를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-138">Double-click your instance of Azure AD.</span></span>
4. <span data-ttu-id="dc0a2-139">Hello 상위 클릭에서 **구성**</span><span class="sxs-lookup"><span data-stu-id="dc0a2-139">At hello top click **Configure**</span></span>
5. <span data-ttu-id="dc0a2-140">Multi-Factor Authentication 아래에서 **서비스 설정 관리**
   ![다운로드](./media/multi-factor-authentication-sdk/download2.png)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-140">Under multi-factor authentication, select **Manage service settings**
![Download](./media/multi-factor-authentication-sdk/download2.png)</span></span>
6. <span data-ttu-id="dc0a2-141">Hello 서비스 설정 페이지에서 클릭에 hello hello 화면 맨 아래에 **Go toohello 포털**합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-141">On hello services settings page, at hello bottom of hello screen click **Go toohello portal**.</span></span> <span data-ttu-id="dc0a2-142">새 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-142">A new page opens.</span></span>
   <span data-ttu-id="dc0a2-143">![다운로드](./media/multi-factor-authentication-sdk/download3a.png)</span><span class="sxs-lookup"><span data-stu-id="dc0a2-143">![Download](./media/multi-factor-authentication-sdk/download3a.png)</span></span>
7. <span data-ttu-id="dc0a2-144">Hello 맨 아래에 남은 hello 클릭 **SDK**합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-144">On hello left, at hello bottom, click **SDK**.</span></span>
8. <span data-ttu-id="dc0a2-145">하나의 hello 관련 된 다운로드 링크를 클릭 hello 언어를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-145">Select hello language you want and click one hello associated download links.</span></span>
9. <span data-ttu-id="dc0a2-146">Hello 다운로드를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-146">Save hello download.</span></span>

## <a name="whats-in-hello-sdk"></a><span data-ttu-id="dc0a2-147">Hello에 포함 된 내용 SDK</span><span class="sxs-lookup"><span data-stu-id="dc0a2-147">What's in hello SDK</span></span>
<span data-ttu-id="dc0a2-148">hello를 SDK hello를 다음 항목 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-148">hello SDK includes hello following items:</span></span>

* <span data-ttu-id="dc0a2-149">**README**.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-149">**README**.</span></span> <span data-ttu-id="dc0a2-150">기존 또는 새 응용 프로그램에서 toouse Multi-factor Authentication Api hello 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-150">Explains how toouse hello Multi-Factor Authentication APIs in a new or existing application.</span></span>
* <span data-ttu-id="dc0a2-151">Multi-Factor Authentication의 **소스 파일**</span><span class="sxs-lookup"><span data-stu-id="dc0a2-151">**Source files** for Multi-Factor Authentication</span></span>
* <span data-ttu-id="dc0a2-152">**클라이언트 인증서** toocommunicate 사용 하 여 Multi-factor Authentication 서비스 hello로</span><span class="sxs-lookup"><span data-stu-id="dc0a2-152">**Client certificate** that you use toocommunicate with hello Multi-Factor Authentication service</span></span>
* <span data-ttu-id="dc0a2-153">**개인 키** hello 인증서에 대 한</span><span class="sxs-lookup"><span data-stu-id="dc0a2-153">**Private key** for hello certificate</span></span>
* <span data-ttu-id="dc0a2-154">**결과를 호출합니다.**</span><span class="sxs-lookup"><span data-stu-id="dc0a2-154">**Call results.**</span></span> <span data-ttu-id="dc0a2-155">호출 결과 코드의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-155">A list of call result codes.</span></span> <span data-ttu-id="dc0a2-156">tooopen이이 파일을 사용 하 여 텍스트 워드 패드와 같은 서식에 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-156">tooopen this file, use an application with text formatting, such as WordPad.</span></span> <span data-ttu-id="dc0a2-157">사용 하 여 hello 호출 결과 코드 tootest 및 응용 프로그램에 Multi-factor Authentication의 hello 구현 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-157">Use hello call result codes tootest and troubleshoot hello implementation of Multi-Factor Authentication in your application.</span></span> <span data-ttu-id="dc0a2-158">상태 코드를 인증하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-158">They are not authentication status codes.</span></span>
* <span data-ttu-id="dc0a2-159">**예제.**</span><span class="sxs-lookup"><span data-stu-id="dc0a2-159">**Examples.**</span></span> <span data-ttu-id="dc0a2-160">Multi-Factor Authentication의 기본 작업 구현에 대한 샘플 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-160">Sample code for a basic working implementation of Multi-Factor Authentication.</span></span>

> [!WARNING]
> <span data-ttu-id="dc0a2-161">hello 클라이언트 인증서가 사용자를 위해 특별히 생성 된 고유한 개인 인증서.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-161">hello client certificate is a unique private certificate that was generated especially for you.</span></span> <span data-ttu-id="dc0a2-162">이 파일을 손실하거나 공유하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-162">Do not share or lose this file.</span></span> <span data-ttu-id="dc0a2-163">Hello Multi-factor Authentication 서비스와의 통신 키 tooensuring hello 보안은</span><span class="sxs-lookup"><span data-stu-id="dc0a2-163">It’s your key tooensuring hello security of your communications with hello Multi-Factor Authentication service.</span></span>

## <a name="code-sample"></a><span data-ttu-id="dc0a2-164">코드 샘플</span><span class="sxs-lookup"><span data-stu-id="dc0a2-164">Code sample</span></span>
<span data-ttu-id="dc0a2-165">이 코드 예제에서는 hello Azure Multi-factor Authentication SDK tooadd 표준 모드 음성에에서 대 한 Api toouse hello 확인 tooyour 응용 프로그램을 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-165">This code sample shows you how toouse hello APIs in hello Azure Multi-Factor Authentication SDK tooadd standard mode voice call verification tooyour application.</span></span> <span data-ttu-id="dc0a2-166">표준 모드는 사용자 응답 tooby hello # 키를 눌러 hello 전화 통화입니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-166">Standard mode is a telephone call that hello user responds tooby pressing hello # key.</span></span>

<span data-ttu-id="dc0a2-167">이 예제에서는 C# 서버 쪽 논리를 사용 하 여 기본 ASP.NET 응용 프로그램에 C#.NET 2.0 Multi-factor Authentication SDK hello를 사용 하지만 hello 프로세스는 다른 언어에서와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-167">This example uses hello C# .NET 2.0 Multi-Factor Authentication SDK in a basic ASP.NET application with C# server-side logic, but hello process is similar in other languages.</span></span> <span data-ttu-id="dc0a2-168">Hello SDK 실행 파일이 아닌 소스 파일에 포함 되어 있으므로 hello 파일을 작성 하 및 참고할 또는 응용 프로그램에 직접 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-168">Because hello SDK includes source files, not executable files, you can build hello files and reference them or include them directly in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="dc0a2-169">Multi-factor Authentication을 구현할 때 사용 하 여 hello 추가 방법 (전화 통화 또는 문자 메시지) 보조 또는 3 차 확인 toosupplement으로 기본 인증 방법 (사용자 이름 및 암호).</span><span class="sxs-lookup"><span data-stu-id="dc0a2-169">When implementing Multi-Factor Authentication, use hello additional methods (phone call or text message) as secondary or tertiary verification toosupplement your primary authentication method (username and password).</span></span> <span data-ttu-id="dc0a2-170">이러한 메서드는 기본 인증 방법으로 만들지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-170">These methods are not designed as primary authentication methods.</span></span>

### <a name="code-sample-overview"></a><span data-ttu-id="dc0a2-171">코드 샘플 개요</span><span class="sxs-lookup"><span data-stu-id="dc0a2-171">Code Sample Overview</span></span>
<span data-ttu-id="dc0a2-172">이 샘플 코드는 간단한 웹 데모 응용 프로그램에 대 한 # 키 응답 tooverify hello 사용자의 인증 전화 통화를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-172">This sample code for a simple web demo application uses a telephone call with a # key response tooverify hello user's authentication.</span></span> <span data-ttu-id="dc0a2-173">이 전화 통화 단계는 Multi-Factor Authentication에서 표준 모드라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-173">This telephone call factor is known in Multi-Factor Authentication as standard mode.</span></span>

<span data-ttu-id="dc0a2-174">hello 클라이언트 쪽 코드는 Multi-factor Authentication 관련 요소가 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-174">hello client-side code does not include any Multi-Factor Authentication-specific elements.</span></span> <span data-ttu-id="dc0a2-175">Hello 추가 인증 단계는 독립적 이므로 hello 기본 인증, hello 기존의 로그온 인터페이스를 변경 하지 않고도 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-175">Because hello additional authentication factors are independent of hello primary authentication, you can add them without changing hello existing sign-on interface.</span></span> <span data-ttu-id="dc0a2-176">hello Multi-factor SDK의에서 Api hello hello 사용자 환경을 사용자 지정할 수 있지만 않아도 toochange 아무 것도 전혀 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-176">hello APIs in hello Multi-Factor SDK let you customize hello user experience, but you might not need toochange anything at all.</span></span>

<span data-ttu-id="dc0a2-177">hello 서버 쪽 코드는 2 단계에서에서 표준 모드 인증을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-177">hello server-side code adds standard-mode authentication in Step 2.</span></span> <span data-ttu-id="dc0a2-178">표준 모드 확인에 필요한 hello 매개 변수가 있는 PfAuthParams 개체를 만듭니다: 사용자 이름, 전화 번호 및 모드 및 hello 경로 toohello 않는 클라이언트 인증서 (p a t h) 각 호출에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-178">It creates a PfAuthParams object with hello parameters that are required for standard-mode verification: username, telephone number, and mode, and hello path toohello client certificate (CertFilePath), which is required in each call.</span></span> <span data-ttu-id="dc0a2-179">PfAuthParams에서 모든 매개 변수의 데모를 보려면 참조 hello SDK에서에서 hello 예제 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-179">For a demonstration of all parameters in PfAuthParams, see hello Example file in hello SDK.</span></span>

<span data-ttu-id="dc0a2-180">다음으로 hello 코드 hello PfAuthParams 개체 toohello pf_authenticate() 함수를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-180">Next, hello code passes hello PfAuthParams object toohello pf_authenticate() function.</span></span> <span data-ttu-id="dc0a2-181">hello 반환 값의 hello 인증 hello 성공 또는 실패를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-181">hello return value indicates hello success or failure of hello authentication.</span></span> <span data-ttu-id="dc0a2-182">매개 변수, callStatus, 및 errorID hello, 추가 호출 결과 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-182">hello out parameters, callStatus, and errorID, contain additional call result information.</span></span> <span data-ttu-id="dc0a2-183">hello 통화 결과 코드는 hello SDK hello 호출 결과 파일에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-183">hello call result codes are documented in hello call results file in hello SDK.</span></span>

<span data-ttu-id="dc0a2-184">이 최소 구현은 몇 줄로 작성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-184">This minimal implementation can be written in a few lines.</span></span> <span data-ttu-id="dc0a2-185">그러나 프로덕션 코드에서는 보다 복잡 한 오류 처리, 추가 데이터베이스 코드 및 고급 사용자 환경을 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-185">However, in production code, you would include more sophisticated error handling, additional database code, and an enhanced user experience.</span></span>

### <a name="web-client-code"></a><span data-ttu-id="dc0a2-186">웹 클라이언트 코드</span><span class="sxs-lookup"><span data-stu-id="dc0a2-186">Web Client Code</span></span>
<span data-ttu-id="dc0a2-187">hello 다음은 웹 클라이언트 코드는 데모 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-187">hello following is web client code for a demo page.</span></span>

    <%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="\_Default" %>

    <!DOCTYPE html>

    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
    <title>Multi-Factor Authentication Demo</title>
    </head>
    <body>
    <h1>Azure Multi-Factor Authentication Demo</h1>
    <form id="form1" runat="server">

    <div style="width:auto; float:left">
    Username:&nbsp;<br />
    Password:&nbsp;<br />
    </div>

    <div">
    <asp:TextBox id="username" runat="server" width="100px"/><br />
    <asp:Textbox id="password" runat="server" width="100px" TextMode="password" /><br />
    </div>

    <asp:Button id="btnSubmit" runat="server" Text="Log in" onClick="btnSubmit_Click"/>

    <p><asp:Label ID="lblResult" runat="server"></asp:Label></p>

    </form>
    </body>
    </html>


### <a name="server-side-code"></a><span data-ttu-id="dc0a2-188">서버 쪽 코드</span><span class="sxs-lookup"><span data-stu-id="dc0a2-188">Server-Side Code</span></span>
<span data-ttu-id="dc0a2-189">서버 쪽 코드 다음 hello, Multi-factor Authentication가 구성 되 고 2 단계에서에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-189">In hello following server-side code, Multi-Factor Authentication is configured and run in Step 2.</span></span> <span data-ttu-id="dc0a2-190">표준 모드 (MODE_STANDARD)는 전화 통화 toowhich hello 사용자 hello # 키를 눌러 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc0a2-190">Standard mode (MODE_STANDARD) is a telephone call toowhich hello user responds by pressing hello # key.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.UI;
    using System.Web.UI.WebControls;

    public partial class \_Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void btnSubmit_Click(object sender, EventArgs e)
        {
            // Step 1: Validate hello username and password
            if (username.Text != "Contoso" || password.Text != "password")
            {
                lblResult.ForeColor = System.Drawing.Color.Red;
                lblResult.Text = "Username or password incorrect.";
            }
            else
            {
                // Step 2: Perform multi-factor authentication

                // Add call details from hello user database.
                PfAuthParams pfAuthParams = new PfAuthParams();
                pfAuthParams.Username = username.Text;
                pfAuthParams.Phone = "5555555555";
                pfAuthParams.Mode = pf_auth.MODE_STANDARD;

                // Specify a client certificate
                // NOTE: This file contains hello private key for hello client
                // certificate. It must be stored with appropriate file
                // permissions.
                pfAuthParams.CertFilePath = "c:\\cert_key.p12";

                // Perform phone-based authentication
                int callStatus;
                int errorId;

                if(pf_auth.pf_authenticate(pfAuthParams, out callStatus, out errorId))
                {
                    lblResult.ForeColor = System.Drawing.Color.Green;
                    lblResult.Text = "Multi-Factor Authentication succeeded.";
                }
                else
                {
                    lblResult.ForeColor = System.Drawing.Color.Red;
                    lblResult.Text = "Multi-Factor Authentication failed.";
                }
            }

        }
    }
