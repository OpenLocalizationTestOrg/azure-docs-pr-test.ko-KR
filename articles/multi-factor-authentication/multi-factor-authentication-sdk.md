---
title: "사용자 지정 앱에 대한 MFA 소프트웨어 개발 키트 | Microsoft Docs"
description: "이 문서에서는 Azure MFA SDK를 다운로드하고 사용하여 사용자 지정 앱에 대한 2단계 확인을 사용하는 방법을 보여 줍니다."
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
ms.openlocfilehash: 281f9c61a30a20027f69808600373aa272255ef6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a><span data-ttu-id="5fb04-103">Multi-Factor Authentication을 사용자 지정 앱(SDK)으로 빌드하기</span><span class="sxs-lookup"><span data-stu-id="5fb04-103">Building Multi-Factor Authentication into Custom Apps (SDK)</span></span>

<span data-ttu-id="5fb04-104">Azure Multi-Factor Authentication 소프트웨어 개발 키트(SDK)를 사용하면 Azure AD 테넌트에 응용 프로그램의 로그인 또는 트랜잭션 프로세스로 직접 2단계 검증을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-104">The Azure Multi-Factor Authentication Software Development Kit (SDK) lets you build two-step verification directly into the sign-in or transaction processes of applications in your Azure AD tenant.</span></span>

<span data-ttu-id="5fb04-105">Multi-Factor Authentication SDK는 C#, Visual Basic(.NET), Java, Perl, PHP 및 Ruby에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-105">The Multi-Factor Authentication SDK is available for C#, Visual Basic (.NET), Java, Perl, PHP, and Ruby.</span></span> <span data-ttu-id="5fb04-106">SDK는 2단계 검증에 대한 씬 래퍼를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-106">The SDK provides a thin wrapper around two-step verification.</span></span> <span data-ttu-id="5fb04-107">주석 처리된 소스 코드 파일, 예제 파일 및 자세한 추가 정보 파일을 포함하여 코드를 작성하는 데 필요한 모든 것이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-107">It includes everything you need to write your code, including commented source code files, example files, and a detailed ReadMe file.</span></span> <span data-ttu-id="5fb04-108">또한 각 SDK에는 Multi-Factor Authentication 공급자에 고유한 트랜잭션을 암호화하기 위한 인증서와 개인 키가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-108">Each SDK also includes a certificate and private key for encrypting transactions that are unique to your Multi-Factor Authentication Provider.</span></span> <span data-ttu-id="5fb04-109">공급자가 있으면 필요에 따라 많은 언어와 형식에서 SDK를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-109">As long as you have a provider, you can download the SDK in as many languages and formats as you need.</span></span>

<span data-ttu-id="5fb04-110">Multi-Factor Authentication SDK의 API 구조는 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-110">The structure of the APIs in the Multi-Factor Authentication SDK is simple.</span></span> <span data-ttu-id="5fb04-111">유효성을 검사할 PIN 번호나 전화번호와 같은 사용자 데이터 및 확인 모드와 같은 다단계 옵션 매개 변수를 사용하여 API에 단일 함수를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-111">Make a single function call to an API with the multi-factor option parameters (like verification mode) and user data (like the telephone number to call or the PIN number to validate).</span></span> <span data-ttu-id="5fb04-112">API는 클라우드 기반 Azure Multi-Factor Authentication 서비스에 대한 웹 서비스 요청으로 함수 호출을 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-112">The APIs translate the function call into web services requests to the cloud-based Azure Multi-Factor Authentication Service.</span></span> <span data-ttu-id="5fb04-113">모든 호출은 모든 SDK에 포함된 개인 인증서에 대한 참조를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-113">All calls must include a reference to the private certificate that is included in every SDK.</span></span>

<span data-ttu-id="5fb04-114">Azure Active Directory에 등록된 사용자에 대한 액세스 권한이 API에 없기 때문에 사용자 정보를 파일이나 데이터베이스에 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-114">Because the APIs do not have access to users registered in Azure Active Directory, you must provide user information in a file or database.</span></span> <span data-ttu-id="5fb04-115">또한 API는 등록 또는 사용자 관리 기능을 제공하지 않으므로, 응용 프로그램으로 이 프로세스를 빌드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-115">Also, the APIs do not provide enrollment or user management features, so you need to build these processes into your application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5fb04-116">SDK를 다운로드하려면 Azure MFA, AAD Premium 또는 EMS 라이선스가 있더라도 Azure Multi-Factor Auth 공급자를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-116">To download the SDK, you need to create an Azure Multi-Factor Auth Provider even if you have Azure MFA, AAD Premium, or EMS licenses.</span></span> <span data-ttu-id="5fb04-117">이를 위해 Azure Multi-Factor Auth 공급자를 만들고 이미 라이선스를 보유한 경우 공급자는 반드시 **활성화된 사용자당** 모델을 사용하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-117">If you create an Azure Multi-Factor Auth Provider for this purpose and already have licenses, make sure to create the Provider with the **Per Enabled User** model.</span></span> <span data-ttu-id="5fb04-118">그런 다음 Azure MFA, Azure AD Premium 또는 EMS 라이선스를 포함하는 디렉터리에 공급자를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-118">Then, link the Provider to the directory that contains the Azure MFA, Azure AD Premium, or EMS licenses.</span></span> <span data-ttu-id="5fb04-119">이 구성을 사용하면 사용자가 소유한 라이선스 수보다 SDK를 사용하는 고유 사용자가 더 많은 경우에만 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-119">This configuration ensures that you are only billed if you have more unique users using the SDK than the number of licenses you own.</span></span>


## <a name="download-the-sdk"></a><span data-ttu-id="5fb04-120">SDK 다운로드</span><span class="sxs-lookup"><span data-stu-id="5fb04-120">Download the SDK</span></span>
<span data-ttu-id="5fb04-121">Azure Multi-Factor SDK를 다운로드하려면 [Azure Multi-Factor Auth 공급자](multi-factor-authentication-get-started-auth-provider.md)가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-121">Downloading the Azure Multi-Factor SDK requires an [Azure Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md).</span></span>  <span data-ttu-id="5fb04-122">따라서 Azure MFA, Azure AD Premium 또는 Enterprise Mobility Suite 라이선스가 있는 경우에도 전체 Azure 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-122">This requires a full Azure subscription, even if Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses are owned.</span></span>  <span data-ttu-id="5fb04-123">SDK를 다운로드하려면 다단계 관리 포털로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-123">To download the SDK, navigate to the Multi-Factor Management Portal.</span></span> <span data-ttu-id="5fb04-124">Multi-Factor Auth 공급자를 직접 관리하거나 MFA 서비스 설정 페이지에서 **"포털로 이동"** 링크를 클릭하여 포털로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-124">You can reach the portal either by managing the Multi-Factor Auth Provider directly, or by clicking the **"Go to the portal"** link on the MFA service settings page.</span></span>

### <a name="download-from-the-azure-classic-portal"></a><span data-ttu-id="5fb04-125">Azure 클래식 포털에서 다운로드</span><span class="sxs-lookup"><span data-stu-id="5fb04-125">Download from the Azure classic portal</span></span>
1. <span data-ttu-id="5fb04-126">관리자 권한으로 [Azure 클래식 포털](https://manage.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-126">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="5fb04-127">왼쪽 창에서 **Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-127">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="5fb04-128">Active Directory 페이지의 위쪽에서 **Multi-Factor Auth 공급자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-128">On the Active Directory page, at the top select **Multi-Factor Auth Providers**</span></span>
4. <span data-ttu-id="5fb04-129">아래쪽에서 **관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-129">At the bottom select **Manage**.</span></span> <span data-ttu-id="5fb04-130">새 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-130">A new page opens.</span></span>
5. <span data-ttu-id="5fb04-131">왼쪽 아래에서 **SDK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-131">On the left, at the bottom, click **SDK**.</span></span>
   <span data-ttu-id="5fb04-132"><center>![다운로드](./media/multi-factor-authentication-sdk/download.png)</center></span><span class="sxs-lookup"><span data-stu-id="5fb04-132"><center>![Download](./media/multi-factor-authentication-sdk/download.png)</center></span></span>
6. <span data-ttu-id="5fb04-133">원하는 언어를 누르고 관련된 다운로드 링크를 하나 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-133">Select the language you want and click one the associated download links.</span></span>
7. <span data-ttu-id="5fb04-134">다운로드 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-134">Save the download.</span></span>

### <a name="download-from-the-service-settings"></a><span data-ttu-id="5fb04-135">서비스 설정에서 다운로드</span><span class="sxs-lookup"><span data-stu-id="5fb04-135">Download from the service settings</span></span>
1. <span data-ttu-id="5fb04-136">관리자 권한으로 [Azure 클래식 포털](https://manage.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-136">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="5fb04-137">왼쪽 창에서 **Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-137">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="5fb04-138">Azure AD 인스턴스를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-138">Double-click your instance of Azure AD.</span></span>
4. <span data-ttu-id="5fb04-139">위쪽에서 **구성**</span><span class="sxs-lookup"><span data-stu-id="5fb04-139">At the top click **Configure**</span></span>
5. <span data-ttu-id="5fb04-140">Multi-Factor Authentication 아래에서 **서비스 설정 관리**
   ![다운로드](./media/multi-factor-authentication-sdk/download2.png)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-140">Under multi-factor authentication, select **Manage service settings**
![Download](./media/multi-factor-authentication-sdk/download2.png)</span></span>
6. <span data-ttu-id="5fb04-141">서비스 설정 페이지의 화면 아래쪽에서 **포털로 이동**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-141">On the services settings page, at the bottom of the screen click **Go to the portal**.</span></span> <span data-ttu-id="5fb04-142">새 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-142">A new page opens.</span></span>
   <span data-ttu-id="5fb04-143">![다운로드](./media/multi-factor-authentication-sdk/download3a.png)</span><span class="sxs-lookup"><span data-stu-id="5fb04-143">![Download](./media/multi-factor-authentication-sdk/download3a.png)</span></span>
7. <span data-ttu-id="5fb04-144">왼쪽 아래에서 **SDK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-144">On the left, at the bottom, click **SDK**.</span></span>
8. <span data-ttu-id="5fb04-145">원하는 언어를 누르고 관련된 다운로드 링크를 하나 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-145">Select the language you want and click one the associated download links.</span></span>
9. <span data-ttu-id="5fb04-146">다운로드 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-146">Save the download.</span></span>

## <a name="whats-in-the-sdk"></a><span data-ttu-id="5fb04-147">SDK의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="5fb04-147">What's in the SDK</span></span>
<span data-ttu-id="5fb04-148">SDK에는 다음 항목이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-148">The SDK includes the following items:</span></span>

* <span data-ttu-id="5fb04-149">**README**.</span><span class="sxs-lookup"><span data-stu-id="5fb04-149">**README**.</span></span> <span data-ttu-id="5fb04-150">기존 또는 새 응용 프로그램에서 Multi-Factor Authentication API를 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-150">Explains how to use the Multi-Factor Authentication APIs in a new or existing application.</span></span>
* <span data-ttu-id="5fb04-151">Multi-Factor Authentication의 **소스 파일**</span><span class="sxs-lookup"><span data-stu-id="5fb04-151">**Source files** for Multi-Factor Authentication</span></span>
* <span data-ttu-id="5fb04-152">**클라이언트 인증서** </span><span class="sxs-lookup"><span data-stu-id="5fb04-152">**Client certificate** that you use to communicate with the Multi-Factor Authentication service</span></span>
* <span data-ttu-id="5fb04-153">**개인 키** </span><span class="sxs-lookup"><span data-stu-id="5fb04-153">**Private key** for the certificate</span></span>
* <span data-ttu-id="5fb04-154">**결과를 호출합니다.**</span><span class="sxs-lookup"><span data-stu-id="5fb04-154">**Call results.**</span></span> <span data-ttu-id="5fb04-155">호출 결과 코드의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-155">A list of call result codes.</span></span> <span data-ttu-id="5fb04-156">이 파일을 열려면 텍스트 워드패드와 같은 서식에 응용 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-156">To open this file, use an application with text formatting, such as WordPad.</span></span> <span data-ttu-id="5fb04-157">호출 결과 코드를 사용하여 응용 프로그램의 Multi-Factor Authentication 구현을 테스트하고 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-157">Use the call result codes to test and troubleshoot the implementation of Multi-Factor Authentication in your application.</span></span> <span data-ttu-id="5fb04-158">상태 코드를 인증하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-158">They are not authentication status codes.</span></span>
* <span data-ttu-id="5fb04-159">**예제.**</span><span class="sxs-lookup"><span data-stu-id="5fb04-159">**Examples.**</span></span> <span data-ttu-id="5fb04-160">Multi-Factor Authentication의 기본 작업 구현에 대한 샘플 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-160">Sample code for a basic working implementation of Multi-Factor Authentication.</span></span>

> [!WARNING]
> <span data-ttu-id="5fb04-161">클라이언트 인증서는 특히 사용자에 대해 생성된 고유한 개인 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-161">The client certificate is a unique private certificate that was generated especially for you.</span></span> <span data-ttu-id="5fb04-162">이 파일을 손실하거나 공유하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="5fb04-162">Do not share or lose this file.</span></span> <span data-ttu-id="5fb04-163">Multi-Factor Authentication 서비스와의 통신 보안을 유지할 키입니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-163">It’s your key to ensuring the security of your communications with the Multi-Factor Authentication service.</span></span>

## <a name="code-sample"></a><span data-ttu-id="5fb04-164">코드 샘플</span><span class="sxs-lookup"><span data-stu-id="5fb04-164">Code sample</span></span>
<span data-ttu-id="5fb04-165">이 코드 예제에서는 Azure Multi-Factor Authentication SDK의 API를 사용하여 표준 모드 음성 통화 확인을 응용 프로그램에 추가하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-165">This code sample shows you how to use the APIs in the Azure Multi-Factor Authentication SDK to add standard mode voice call verification to your application.</span></span> <span data-ttu-id="5fb04-166">표준 모드는 사용자가 # 키를 눌러 응답하는 전화 통화입니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-166">Standard mode is a telephone call that the user responds to by pressing the # key.</span></span>

<span data-ttu-id="5fb04-167">이 예에서는 C# 서버측 논리를 사용하는 기본 ASP.NET 응용 프로그램에서 C# .NET 2.0 Multi-Factor Authentication SDK를 사용하지만 프로세스는 다른 언어에서 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-167">This example uses the C# .NET 2.0 Multi-Factor Authentication SDK in a basic ASP.NET application with C# server-side logic, but the process is similar in other languages.</span></span> <span data-ttu-id="5fb04-168">SDK에는 실행 파일이 아닌 소스 파일이 포함되어 있으므로 파일을 빌드하고 참조하거나 응용 프로그램에 직접 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-168">Because the SDK includes source files, not executable files, you can build the files and reference them or include them directly in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="5fb04-169">Multi-Factor Authentication을 구현하는 경우 기본 인증 방법(사용자 이름 및 암호)을 보완하기 위해 보조 또는 3차 확인으로 추가 방법(전화 통화 또는 텍스트 메시지)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-169">When implementing Multi-Factor Authentication, use the additional methods (phone call or text message) as secondary or tertiary verification to supplement your primary authentication method (username and password).</span></span> <span data-ttu-id="5fb04-170">이러한 메서드는 기본 인증 방법으로 만들지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-170">These methods are not designed as primary authentication methods.</span></span>

### <a name="code-sample-overview"></a><span data-ttu-id="5fb04-171">코드 샘플 개요</span><span class="sxs-lookup"><span data-stu-id="5fb04-171">Code Sample Overview</span></span>
<span data-ttu-id="5fb04-172">간단한 웹 데모 응용 프로그램에 대한 이 샘플 코드는 # 키 응답으로 전화 통화를 사용하여 사용자의 인증을 검증합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-172">This sample code for a simple web demo application uses a telephone call with a # key response to verify the user's authentication.</span></span> <span data-ttu-id="5fb04-173">이 전화 통화 단계는 Multi-Factor Authentication에서 표준 모드라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-173">This telephone call factor is known in Multi-Factor Authentication as standard mode.</span></span>

<span data-ttu-id="5fb04-174">클라이언트측 코드는 Multi-Factor Authentication 관련 요소를 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-174">The client-side code does not include any Multi-Factor Authentication-specific elements.</span></span> <span data-ttu-id="5fb04-175">추가 인증 단계는 기본 인증과 독립적이기 때문에 기존의 로그온 인터페이스를 변경하지 않고 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-175">Because the additional authentication factors are independent of the primary authentication, you can add them without changing the existing sign-on interface.</span></span> <span data-ttu-id="5fb04-176">다단계 SDK의 API를 통해 사용자 환경을 사용자 지정할 수 있지만 전혀 변경할 필요가 없을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-176">The APIs in the Multi-Factor SDK let you customize the user experience, but you might not need to change anything at all.</span></span>

<span data-ttu-id="5fb04-177">서버쪽 코드는 2 단계에서 표준 모드 인증을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-177">The server-side code adds standard-mode authentication in Step 2.</span></span> <span data-ttu-id="5fb04-178">표준 모드 확인에 필요한 매개 변수로 PfAuthParams 개체를 만듭니다. 사용자 이름, 전화 번호, 모드 및 클라이언트 인증서(CertFilePath)에 대한 경로가 각 호출에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-178">It creates a PfAuthParams object with the parameters that are required for standard-mode verification: username, telephone number, and mode, and the path to the client certificate (CertFilePath), which is required in each call.</span></span> <span data-ttu-id="5fb04-179">PfAuthParams의 모든 매개 변수의 데모를 보려면 SDK의 예제 파일을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5fb04-179">For a demonstration of all parameters in PfAuthParams, see the Example file in the SDK.</span></span>

<span data-ttu-id="5fb04-180">다음으로, 코드는 PfAuthParams 개체를 pf_authenticate() 함수에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-180">Next, the code passes the PfAuthParams object to the pf_authenticate() function.</span></span> <span data-ttu-id="5fb04-181">반환 값은 인증의 성공 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-181">The return value indicates the success or failure of the authentication.</span></span> <span data-ttu-id="5fb04-182">out 매개 변수, callStatus 및 errorID는 추가 호출 결과 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-182">The out parameters, callStatus, and errorID, contain additional call result information.</span></span> <span data-ttu-id="5fb04-183">호출 결과 코드는 SDK의 호출 결과 파일에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-183">The call result codes are documented in the call results file in the SDK.</span></span>

<span data-ttu-id="5fb04-184">이 최소 구현은 몇 줄로 작성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-184">This minimal implementation can be written in a few lines.</span></span> <span data-ttu-id="5fb04-185">그러나 프로덕션 코드에서는 보다 복잡 한 오류 처리, 추가 데이터베이스 코드 및 고급 사용자 환경을 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-185">However, in production code, you would include more sophisticated error handling, additional database code, and an enhanced user experience.</span></span>

### <a name="web-client-code"></a><span data-ttu-id="5fb04-186">웹 클라이언트 코드</span><span class="sxs-lookup"><span data-stu-id="5fb04-186">Web Client Code</span></span>
<span data-ttu-id="5fb04-187">다음은 데모 페이지에 대한 웹 클라이언트 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-187">The following is web client code for a demo page.</span></span>

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


### <a name="server-side-code"></a><span data-ttu-id="5fb04-188">서버 쪽 코드</span><span class="sxs-lookup"><span data-stu-id="5fb04-188">Server-Side Code</span></span>
<span data-ttu-id="5fb04-189">다음 서버쪽 코드에서 Multi-Factor Authentication이 구성되고 2 단계에서 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-189">In the following server-side code, Multi-Factor Authentication is configured and run in Step 2.</span></span> <span data-ttu-id="5fb04-190">표준 모드(MODE_STANDARD)는 사용자가 # 키를 눌러 응답하는 전화 통화입니다.</span><span class="sxs-lookup"><span data-stu-id="5fb04-190">Standard mode (MODE_STANDARD) is a telephone call to which the user responds by pressing the # key.</span></span>

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
            // Step 1: Validate the username and password
            if (username.Text != "Contoso" || password.Text != "password")
            {
                lblResult.ForeColor = System.Drawing.Color.Red;
                lblResult.Text = "Username or password incorrect.";
            }
            else
            {
                // Step 2: Perform multi-factor authentication

                // Add call details from the user database.
                PfAuthParams pfAuthParams = new PfAuthParams();
                pfAuthParams.Username = username.Text;
                pfAuthParams.Phone = "5555555555";
                pfAuthParams.Mode = pf_auth.MODE_STANDARD;

                // Specify a client certificate
                // NOTE: This file contains the private key for the client
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
