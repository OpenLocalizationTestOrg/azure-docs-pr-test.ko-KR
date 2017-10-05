---
title: "ADAL을 사용하여 Android에서 앱 간 SSO를 사용하도록 설정하는 방법 | Microsoft Docs"
description: "ADAL SDK의 기능을 사용하여 응용 프로그램에서 Single Sign On을 활성화하는 방법입니다. "
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 40710225-05ab-40a3-9aec-8b4e96b6b5e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 04/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 9c7e959530a836fe5ddf74708363a636c39b3cc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-enable-cross-app-sso-on-android-using-adal"></a><span data-ttu-id="70b22-103">ADAL을 사용하여 Android에서 앱 간 SSO를 사용하도록 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="70b22-103">How to enable cross-app SSO on Android using ADAL</span></span>
<span data-ttu-id="70b22-104">사용자가 자격 증명을 한 번만 입력하고 응용 프로그램에서 자동으로 작동되도록 SSO(Single Sign-on)를 제공하는 것은 이제 고객에게 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-104">Providing Single Sign-On (SSO) so that users only need to enter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="70b22-105">종종 전화 통화 또는 문자로 전송하는 코드와 같은 추가 요소(2FA)로 결합된 작은 화면에서 자신의 사용자 이름 및 암호를 입력하는 어려움은 사용자가 제품에 대해 이를 한 번 이상 수행해야 하는 경우 빠른 불만족을 가져 옵니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-105">The difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has to do this more than one time for your product.</span></span>

<span data-ttu-id="70b22-106">또한 다른 응용 프로그램이 office365에서 Microsoft 계정 또는 회사 계정을 사용할 수 있는 ID 플랫폼을 적용하는 경우 고객은 공급 업체에 관계 없이 모든 응용 프로그램에서 자격 증명을 사용할 수 있기를 기대합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials to be available to use across all their applications no matter the vendor.</span></span>

<span data-ttu-id="70b22-107">Microsoft ID SDK와 함께 Microsoft ID 플랫폼은 이 모든 어려운 작업을 수행하며 자체 응용 프로그램 제품 내의 SSO 또는 전체 장치에서 브로커 기능 및 Authenticator 응용 프로그램으로 고객을 만족시키는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-107">The Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you the ability to delight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across the entire device.</span></span>

<span data-ttu-id="70b22-108">이 연습에서는 고객에게 이 혜택을 제공하도록 응용 프로그램 내에서 SDK를 구성하는 방법을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-108">This walkthrough will tell you how to configure our SDK within your application to provide this benefit to your customers.</span></span>

<span data-ttu-id="70b22-109">이 연습은 다음에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="70b22-110">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="70b22-110">Azure Active Directory</span></span>
* <span data-ttu-id="70b22-111">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="70b22-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="70b22-112">Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="70b22-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="70b22-113">Azure Active Directory 조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="70b22-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="70b22-114">이전 문서는 [Azure Active Directory에 대한 레거시 포털에서 응용 프로그램을 프로비전](active-directory-how-to-integrate.md)하는 방법을 알고 있으며 응용 프로그램을 [Microsoft ID Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android)와 통합했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-114">The document preceding assumes you know how to [provision applications in the legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with the [Microsoft Identity Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android).</span></span>

## <a name="sso-concepts-in-the-microsoft-identity-platform"></a><span data-ttu-id="70b22-115">Microsoft ID 플랫폼의 SSO 개념</span><span class="sxs-lookup"><span data-stu-id="70b22-115">SSO Concepts in the Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="70b22-116">Microsoft ID Broker</span><span class="sxs-lookup"><span data-stu-id="70b22-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="70b22-117">Microsoft는 다른 공급 업체의 응용 프로그램에서 자격 증명의 브리징을 허용하고 자격 증명을 확인하는 위치에서 단일 보안 위치가 필요한 특수한 향상된 기능을 허용하는 모든 모바일 플랫폼에 대한 응용 프로그램을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-117">Microsoft provides applications for every mobile platform that allow for the bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where to validate credentials.</span></span> <span data-ttu-id="70b22-118">이를 **브로커**라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-118">We call these **brokers**.</span></span> <span data-ttu-id="70b22-119">iOS 및 Android에서 고객이 독립적으로 설치하거나 해당 직원에 대한 일부 또는 모든 장치를 관리하는 회사에서 장치에 푸시할 수 있는 다운로드 가능한 응용 프로그램을 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-119">On iOS and Android these are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages some or all of the device for their employee.</span></span> <span data-ttu-id="70b22-120">이러한 브로커는 일부 응용 프로그램 또는 IT 관리자가 원하는 기능에 따라 전체 장치에 대해서만 보안 관리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-120">These brokers support managing security just for some applications or the entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="70b22-121">Windows에서 이 기능은 기술적으로 웹 인증 브로커로 알려진 운영 체제에 기본적으로 제공된 계정 선택기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-121">In Windows, this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>

<span data-ttu-id="70b22-122">이러한 브로커를 사용하는 방법 및 고객이 Microsoft ID 플랫폼에 대한 로그인 흐름에서 이를 보는 방법을 이해하려면 자세한 내용을 읽어 보세요.</span><span class="sxs-lookup"><span data-stu-id="70b22-122">For more information on how we use these brokers and how your customers might see them in their login flow for the Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="70b22-123">모바일 장치에 로그인하기 위한 패턴</span><span class="sxs-lookup"><span data-stu-id="70b22-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="70b22-124">장치에서 자격 증명에 대한 액세스는 Microsoft ID 플랫폼에 대해 두 가지 기본 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-124">Access to credentials on devices follow two basic patterns for the Microsoft Identity platform:</span></span>

* <span data-ttu-id="70b22-125">비 브로커 지원 로그인</span><span class="sxs-lookup"><span data-stu-id="70b22-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="70b22-126">브로커 지원 로그인</span><span class="sxs-lookup"><span data-stu-id="70b22-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="70b22-127">비 브로커 지원 로그인</span><span class="sxs-lookup"><span data-stu-id="70b22-127">Non-broker assisted logins</span></span>
<span data-ttu-id="70b22-128">비 브로커 지원 로그인은 응용 프로그램과 함께 인라인을 발생하고 해당 응용 프로그램에 대한 장치에서 로컬 저장소를 사용하는 로그인 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-128">Non-broker assisted logins are login experiences that happen inline with the application and use the local storage on the device for that application.</span></span> <span data-ttu-id="70b22-129">이 저장소는 응용 프로그램 간에 공유될 수 있지만 자격 증명은 해당 자격 증명을 사용하는 앱 또는 앱의 제품군에 밀접하게 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-129">This storage may be shared across applications but the credentials are tightly bound to the app or suite of apps using that credential.</span></span> <span data-ttu-id="70b22-130">응용 프로그램 자체 내에서 사용자 이름 및 암호를 입력하는 경우 많은 모바일 응용 프로그램에서 이를 경험할 가능성이 가장 큽니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-130">You've most likely experienced this in many mobile applications when you enter a username and password within the application itself.</span></span>

<span data-ttu-id="70b22-131">이러한 로그인은 다음과 같은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-131">These logins have the following benefits:</span></span>

* <span data-ttu-id="70b22-132">사용자 환경은 응용 프로그램 내에 완전히 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-132">User experience exists entirely within the application.</span></span>
* <span data-ttu-id="70b22-133">응용 프로그램 제품군에 Single Sign-On 환경을 제공하여 동일한 인증서로 서명하는 응용 프로그램에서 자격 증명을 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-133">Credentials can be shared across applications that are signed by the same certificate, providing a single sign-on experience to your suite of applications.</span></span>
* <span data-ttu-id="70b22-134">로그인 환경 주위의 제어는 로그인 이전 및 이후에 응용 프로그램에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-134">Control around the experience of logging in is provided to the application before and after sign-in.</span></span>

<span data-ttu-id="70b22-135">이러한 로그인은 다음과 같은 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-135">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="70b22-136">사용자는 Microsoft ID를 사용하는 모든 앱이 아닌 응용 프로그램이 구성한 해당 Microsoft ID 간에서만 Single Sign-On을 경험할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="70b22-137">조건부 액세스와 같은 고급 비즈니스 기능과 함께 응용 프로그램을 사용하거나 InTune 제품군을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-137">Your application cannot be used with more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="70b22-138">응용 프로그램은 비즈니스 사용자에 대한 인증서 기반 인증을 지원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="70b22-139">Microsoft ID SDK가 응용 프로그램의 공유 저장소와 작업하여 SSO를 활성화하는 방법에 대한 표현은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-139">Here is a representation of how the Microsoft Identity SDKs work with the shared storage of your applications to enable SSO:</span></span>

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| Azure SDK  | | Azure SDK  |  | Azure SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a><span data-ttu-id="70b22-140">브로커 지원 로그인</span><span class="sxs-lookup"><span data-stu-id="70b22-140">Broker assisted logins</span></span>
<span data-ttu-id="70b22-141">브로커 지원 로그인은 브로커 응용 프로그램 내에서 발생하고 Microsoft ID 플랫폼을 적용하는 장치의 모든 응용 프로그램에서 자격 증명을 공유하도록 브로커의 저장소와 보안을 사용하는 로그인 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-141">Broker-assisted logins are login experiences that occur within the broker application and use the storage and security of the broker to share credentials across all applications on the device that apply the Microsoft Identity platform.</span></span> <span data-ttu-id="70b22-142">즉, 응용 프로그램은 사용자가 로그인하도록 브로커를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-142">This means that your applications rely on the broker to sign users in.</span></span> <span data-ttu-id="70b22-143">iOS 및 Android에서 해당 브로커는 고객이 독립적으로 설치하거나 사용자에 대한 장치를 관리하는 회사에서 장치에 푸시할 수 있는 다운로드 가능한 응용 프로그램을 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages the device for their user.</span></span> <span data-ttu-id="70b22-144">이 응용 프로그램 유형의 예는 iOS에서 Microsoft Authenticator 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-144">An example of this type of application is the Microsoft Authenticator application on iOS.</span></span> <span data-ttu-id="70b22-145">Windows에서 이 기능은 기술적으로 웹 인증 브로커로 알려진 운영 체제에 기본적으로 제공된 계정 선택기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-145">In Windows this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>
<span data-ttu-id="70b22-146">환경은 플랫폼별로 다르며 올바르게 관리되지 않는 경우 사용자에게 작업 중단이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-146">The experience varies by platform and can sometimes be disruptive to users if not managed correctly.</span></span> <span data-ttu-id="70b22-147">Facebook 응용 프로그램을 설치하고 다른 응용 프로그램에서 Facebook Connect를 사용하는 경우 아마도 이 패턴과 가장 친숙할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-147">You're probably most familiar with this pattern if you have the Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="70b22-148">Microsoft ID 플랫폼은 동일한 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-148">The Microsoft Identity platform uses the same pattern.</span></span>

<span data-ttu-id="70b22-149">iOS의 경우 이는 Microsoft Authenticator 응용 프로그램이 사용자가 로그인하려는 계정을 선택하도록 포그라운드로 오는 동안 응용 프로그램이 백그라운드로 전송되는 "전환" 애니메이션이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-149">For iOS this leads to a "transition" animation where your application is sent to the background while the Microsoft Authenticator applications comes to the foreground for the user to select which account they would like to sign in with.</span></span>  

<span data-ttu-id="70b22-150">Android 및 Windows의 경우 계정 선택기가 사용자에게 덜 방해가 되는 응용 프로그램 맨 위에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-150">For Android and Windows the account chooser is displayed on top of your application which is less disruptive to the user.</span></span>

#### <a name="how-the-broker-gets-invoked"></a><span data-ttu-id="70b22-151">브로커를 호출하는 방법</span><span class="sxs-lookup"><span data-stu-id="70b22-151">How the broker gets invoked</span></span>
<span data-ttu-id="70b22-152">호환되는 브로커가 Microsoft Authenticator 응용 프로그램과 마찬가지로 장치에 설치된 경우 Microsoft ID SDK는 사용자가 Microsoft ID 플랫폼에서 계정을 사용하여 로그인하려는 것을 나타내는 경우 브로커 호출 작업을 자동으로 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-152">If a compatible broker is installed on the device, like the Microsoft Authenticator application, the Microsoft Identity SDKs will automatically do the work of invoking the broker for you when a user indicates they wish to log in using any account from the Microsoft Identity platform.</span></span> <span data-ttu-id="70b22-153">이 계정은 개인 Microsoft 계정, 회사 또는 학교 계정 또는 B2C 및 B2B 제품을 사용하여 Azure에 제공 및 호스트하는 계정일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 
 
 #### <a name="how-we-ensure-the-application-is-valid"></a><span data-ttu-id="70b22-154">응용 프로그램이 유효한지 확인하는 방법</span><span class="sxs-lookup"><span data-stu-id="70b22-154">How we ensure the application is valid</span></span>
 
 <span data-ttu-id="70b22-155">브로커를 호출하는 응용 프로그램의 ID를 확인하는 것은 브로커 지원 로그인에 제공하는 보안에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-155">The need to ensure the identity of an application call the broker is crucial to the security we provide in broker assisted logins.</span></span> <span data-ttu-id="70b22-156">iOS와 Android 모두 제공된 응용 프로그램에만 유효한 고유한 식별자를 적용하지 않으므로 악의적 응용 프로그램은 합법적인 응용 프로그램의 ID를 “스푸핑"하고 합법적인 응용 프로그램을 의미하는 토큰을 받을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive the tokens meant for the legitimate application.</span></span> <span data-ttu-id="70b22-157">런타임 시 적절한 응용 프로그램으로 항상 통신하고 있음을 확인하기 위해 Microsoft에 해당 응용 프로그램을 등록할 때 개발자에게 사용자 지정 redirectURI를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-157">To ensure we are always communicating with the right application at runtime, we ask the developer to provide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="70b22-158">**개발자가 이 리디렉션 URI를 만드는 방법은 아래에 자세히 설명되어 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="70b22-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="70b22-159">이 사용자 지정 redirectURI는 응용 프로그램의 인증서 지문을 포함하고 Google Play 스토어에서 응용 프로그램에 고유하도록 보장됩니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-159">This custom redirectURI contains the certificate thumbprint of the application and is ensured to be unique to the application by the Google Play Store.</span></span> <span data-ttu-id="70b22-160">응용 프로그램이 브로커를 호출하면 브로커는 Android 운영 체제에 브로커를 호출한 인증서 지문을 제공하도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-160">When an application calls the broker, the broker asks the Android operating system to provide it with the certificate thumbprint that called the broker.</span></span> <span data-ttu-id="70b22-161">브로커는 ID 시스템에 대한 호출에서 Microsoft에 이 인증서 지문을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-161">The broker provides this certificate thumbprint to Microsoft in the call to our identity system.</span></span> <span data-ttu-id="70b22-162">응용 프로그램의 인증서 지문이 등록하는 동안 개발자가 제공한 인증서 지문과 일치하지 않는 경우 응용 프로그램이 요청하는 리소스를 위한 토큰에 대한 액세스를 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-162">If the certificate thumbprint of the application does not match the certificate thumbprint provided to us by the developer during registration, we will deny access to the tokens for the resource the application is requesting.</span></span> <span data-ttu-id="70b22-163">이러한 확인을 통해 개발자가 등록한 응용 프로그램만 토큰을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-163">This check ensures that only the application registered by the developer receives tokens.</span></span>

<span data-ttu-id="70b22-164">**개발자는 Microsoft ID SDK가 브로커를 호출할지 비 브로커 지원 흐름을 사용할지를 선택할 수 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="70b22-164">**The developer has the choice of if the Microsoft Identity SDK calls the broker or uses the non-broker assisted flow.**</span></span> <span data-ttu-id="70b22-165">그러나 개발자가 브로커 지원 흐름을 사용하지 않도록 선택하는 경우 사용자가 장치에 이미 추가했으며 조건부 액세스, Intune 관리 기능 및 인증서 기반 인증과 같은 Microsoft가 고객에게 제공하는 비즈니스 기능으로 응용 프로그램이 사용되는 것을 예방하는 SSO 자격 증명 사용의 이점을 잃게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-165">However if the developer chooses not to use the broker-assisted flow they lose the benefit of using SSO credentials that the user may have already added on the device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="70b22-166">이러한 로그인은 다음과 같은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-166">These logins have the following benefits:</span></span>

* <span data-ttu-id="70b22-167">사용자는 공급 업체에 관계 없이 모든 응용 프로그램에서 SSO를 경험합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-167">User experiences SSO across all their applications no matter the vendor.</span></span>
* <span data-ttu-id="70b22-168">응용 프로그램은 조건부 액세스와 같은 고급 비즈니스 기능을 사용하거나 InTune 제품군을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-168">Your application can use more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="70b22-169">응용 프로그램은 비즈니스 사용자에 대한 인증서 기반 인증을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="70b22-170">응용 프로그램 및 사용자의 ID로서 더 안전한 로그인 환경은 추가 보안 알고리즘 및 암호화로 브로커 응용 프로그램에 의해 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-170">Much more secure sign-in experience as the identity of the application and the user are verified by the broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="70b22-171">이러한 로그인은 다음과 같은 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-171">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="70b22-172">iOS에서 사용자는 자격 증명을 선택하는 동안 응용 프로그램의 환경 밖으로 전환됩니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-172">In iOS the user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="70b22-173">응용 프로그램 내에서 고객에 대한 로그인 환경을 관리하는 기능이 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-173">Loss of the ability to manage the login experience for your customers within your application.</span></span>

<span data-ttu-id="70b22-174">Microsoft ID SDK가 브로커 응용 프로그램과 작업하여 SSO를 활성화하는 방법에 대한 표현은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-174">Here is a representation of how the Microsoft Identity SDKs work with the broker applications to enable SSO:</span></span>

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
|  ADAL SDK  | |  ADAL SDK  |   |  ADAL SDK   |
+-----+------+-+-----+------+-  +-------+-----+
      |              |                  |
      |       +------v------+           |
      |       |             |           |
      |       | Microsoft   |           |
      +-------> Broker      |^----------+
              | Application
              |             |
              +-------------+
              |             |
              |   Broker    |
              |   Storage   |
              |             |
              +-------------+

```

<span data-ttu-id="70b22-175">이 배경 정보를 사용하여 Microsoft ID 플랫폼 및 SDK를 사용하여 응용 프로그램 내에서 SSO를 더 잘 이해하고 구현할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-175">Armed with this background information you should be able to better understand and implement SSO within your application using the Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="70b22-176">ADAL을 사용하여 앱 간 SSO 활성화</span><span class="sxs-lookup"><span data-stu-id="70b22-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="70b22-177">여기에서 ADAL Android SDK를 사용하여 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-177">Here we use the ADAL Android SDK to:</span></span>

* <span data-ttu-id="70b22-178">앱 제품군에 대한 비 브로커 지원 SSO 설정</span><span class="sxs-lookup"><span data-stu-id="70b22-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="70b22-179">브로커 지원 SSO에 대한 지원 설정</span><span class="sxs-lookup"><span data-stu-id="70b22-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="70b22-180">비 브로커 지원 SSO에 대한 SSO 설정</span><span class="sxs-lookup"><span data-stu-id="70b22-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="70b22-181">응용 프로그램에서 비 브로커 지원 SSO의 경우 Microsoft ID SDK는 SSO의 복잡성을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-181">For non-broker assisted SSO across applications the Microsoft Identity SDKs manage much of the complexity of SSO for you.</span></span> <span data-ttu-id="70b22-182">캐시에서 올바른 사용자를 찾고 쿼리할 로그인된 사용자의 목록을 유지 관리하는 것을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-182">This includes finding the right user in the cache and maintaining a list of logged in users for you to query.</span></span>

<span data-ttu-id="70b22-183">소유하고 있는 응용 프로그램에서 SSO를 활성화하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-183">To enable SSO across applications you own you need to do the following:</span></span>

1. <span data-ttu-id="70b22-184">모든 응용 프로그램 사용자가 동일한 클라이언트 ID 또는 응용 프로그램 ID인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-184">Ensure all your applications user the same Client ID or Application ID.</span></span>
2. <span data-ttu-id="70b22-185">모든 응용 프로그램이 동일한 SharedUserID 집합을 포함하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-185">Ensure all your applications have the same SharedUserID set.</span></span>
3. <span data-ttu-id="70b22-186">모든 응용 프로그램이 저장소를 공유할 수 있도록 Google Play 스토어에서 동일한 서명 인증서를 공유하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-186">Ensure that all of your applications share the same signing certificate from the Google Play store so that you can share storage.</span></span>

#### <a name="step-1-using-the-same-client-id--application-id-for-all-the-applications-in-your-suite-of-apps"></a><span data-ttu-id="70b22-187">1단계: 앱 제품군에서 모든 응용 프로그램에 대한 동일한 클라이언트 ID / 응용 프로그램 ID 사용</span><span class="sxs-lookup"><span data-stu-id="70b22-187">Step 1: Using the same Client ID / Application ID for all the applications in your suite of apps</span></span>
<span data-ttu-id="70b22-188">Microsoft ID 플랫폼이 응용 프로그램에서 토큰을 공유하도록 허용하는지 알려면 각 응용 프로그램은 동일한 클라이언트 ID 또는 응용 프로그램 ID를 공유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-188">In order for the Microsoft Identity platform to know that it's allowed to share tokens across your applications, each of your applications will need to share the same Client ID or Application ID.</span></span> <span data-ttu-id="70b22-189">포털에 첫 번째 응용 프로그램을 등록했던 경우에 제공된 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-189">This is the unique identifier that was provided to you when you registered your first application in the portal.</span></span>

<span data-ttu-id="70b22-190">동일한 응용 프로그램 ID를 사용하는 경우 다른 앱을 Microsoft ID 서비스에 식별하는 방법을 궁금해 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-190">You may be wondering how you will identify different apps to the Microsoft Identity service if it uses the same Application ID.</span></span> <span data-ttu-id="70b22-191">**리디렉션 URI**를 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-191">The answer is with the **Redirect URIs**.</span></span> <span data-ttu-id="70b22-192">각 응용 프로그램에는 등록 포털에 등록한 여러 개의 리디렉션 URI가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-192">Each application can have multiple Redirect URIs registered in the onboarding portal.</span></span> <span data-ttu-id="70b22-193">제품의 각 앱은 다른 리디렉션 URI를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-193">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="70b22-194">표시되는 모양의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-194">An example of how this looks is below:</span></span>

<span data-ttu-id="70b22-195">App1 리디렉션 URI: `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span><span class="sxs-lookup"><span data-stu-id="70b22-195">App1 Redirect URI: `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span></span>

<span data-ttu-id="70b22-196">App2 리디렉션 URI: `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span><span class="sxs-lookup"><span data-stu-id="70b22-196">App2 Redirect URI: `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span></span>

<span data-ttu-id="70b22-197">App3 리디렉션 URI: `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span><span class="sxs-lookup"><span data-stu-id="70b22-197">App3 Redirect URI: `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span></span>

<span data-ttu-id="70b22-198">....</span><span class="sxs-lookup"><span data-stu-id="70b22-198">....</span></span>

<span data-ttu-id="70b22-199">이는 동일한 클라이언트 ID / 응용 프로그램 ID 아래에 중첩되며 SDK 구성에서 우리에게 반환하는 리디렉션 URI에 따라 조회됩니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-199">These are nested under the same client ID / application ID and looked up based on the redirect URI you return to us in your SDK configuration.</span></span>

```
+-------------------+
|                   |
|  Client ID        |
+---------+---------+
          |
          |           +-----------------------------------+
          |           |  App 1 Redirect URI               |
          +----------^+                                   |
          |           +-----------------------------------+
          |
          |           +-----------------------------------+
          +----------^+  App 2 Redirect URI               |
          |           |                                   |
          |           +-----------------------------------+
          |
          +----------^+-----------------------------------+
                      |  App 3 Redirect URI               |
                      |                                   |
                      +-----------------------------------+

```


<span data-ttu-id="70b22-200">*이러한 리디렉션 URI의 형식은 아래에 설명되어 있습니다. 브로커를 지원하려고 하는 한 모든 리디렉션 URI를 사용할 수 있습니다. 이 경우 위와 같이 표시되어야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="70b22-200">*Note that the format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish to support the broker, in which case they must look something like the above*</span></span>

#### <a name="step-2-configuring-shared-storage-in-android"></a><span data-ttu-id="70b22-201">2단계: Android에서 공유 저장소 구성</span><span class="sxs-lookup"><span data-stu-id="70b22-201">Step 2: Configuring shared storage in Android</span></span>
<span data-ttu-id="70b22-202">`SharedUserID` 설정은 이 문서의 범위를 벗어나지만 [매니페스트](http://developer.android.com/guide/topics/manifest/manifest-element.html)의 Google Android 설명서를 참조하여 학습할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-202">Setting the `SharedUserID` is beyond the scope of this document but can be learned by reading the Google Android documentation on the [Manifest](http://developer.android.com/guide/topics/manifest/manifest-element.html).</span></span> <span data-ttu-id="70b22-203">중요한 것은 사용자가 sharedUserID가 불리는 이름을 결정하는 것과 모든 응용 프로그램에서 이를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-203">What is important is that you decide what you want your sharedUserID will be called and use that across all your applications.</span></span>

<span data-ttu-id="70b22-204">모든 응용 프로그램에 `SharedUserID` 가 있으면 SSO를 사용할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-204">Once you have the `SharedUserID` in all your applications you are ready to use SSO.</span></span>

> [!WARNING]
> <span data-ttu-id="70b22-205">응용 프로그램에서 저장소를 공유하는 경우 모든 응용 프로그램은 사용자를 삭제하거나 더 심한 경우 응용 프로그램에서 모든 토큰을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-205">When you share storage across your applications any application can delete users, or worse delete all the tokens across your application.</span></span> <span data-ttu-id="70b22-206">백그라운드 작업을 하기 위해 토큰을 사용하는 응용 프로그램이 있는 경우에 특히 미치는 영향이 커집니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-206">This is particularly disastrous if you have applications that rely on the tokens to do background work.</span></span> <span data-ttu-id="70b22-207">저장소를 공유하면 Microsoft ID SDK를 통한 모든 제거 작업에 특히 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-207">Sharing storage means that you must be very careful in any and all remove operations through the Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="70b22-208">이것으로 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-208">That's it!</span></span> <span data-ttu-id="70b22-209">이제 Microsoft ID SDK는 모든 응용 프로그램에서 자격 증명을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-209">The Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="70b22-210">사용자 목록도 응용 프로그램 인스턴스 간에 공유됩니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-210">The user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="70b22-211">브로커 지원 SSO에 대한 SSO 설정</span><span class="sxs-lookup"><span data-stu-id="70b22-211">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="70b22-212">장치에 설치되어 있는 모든 브로커를 사용하는 응용 프로그램에 대한 기능은 **기본적으로 해제되어**있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-212">The ability for an application to use any broker that is installed on the device is **turned off by default**.</span></span> <span data-ttu-id="70b22-213">브로커와 함께 응용 프로그램을 사용하려면 몇 가지 추가 구성을 수행하고 응용 프로그램에 코드를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-213">In order to use your application with the broker you must do some additional configuration and add some code to your application.</span></span>

<span data-ttu-id="70b22-214">수행할 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-214">The steps to follow are:</span></span>

1. <span data-ttu-id="70b22-215">MS SDK에 대한 응용 프로그램 코드의 호출에서 브로커 모드 활성화</span><span class="sxs-lookup"><span data-stu-id="70b22-215">Enable broker mode in your application code's call to the MS SDK</span></span>
2. <span data-ttu-id="70b22-216">새 리디렉션 URI 설정 및 앱과 앱 등록에 이를 제공</span><span class="sxs-lookup"><span data-stu-id="70b22-216">Establish a new redirect URI and provide that to both the app and your app registration</span></span>
3. <span data-ttu-id="70b22-217">Android 매니페스트에서 올바른 사용 권한 설정</span><span class="sxs-lookup"><span data-stu-id="70b22-217">Setting up the correct permissions in the Android manifest</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="70b22-218">1단계: 응용 프로그램에서 브로커 모드 활성화</span><span class="sxs-lookup"><span data-stu-id="70b22-218">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="70b22-219">"설정" 또는 인증 인스턴스의 초기 설정을 만들 때 브로커를 사용하는 응용 프로그램에 대한 기능은 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-219">The ability for your application to use the broker is turned on when you create the "settings" or initial setup of your Authentication instance.</span></span> <span data-ttu-id="70b22-220">코드에서 ApplicationSettings 형식을 설정하여 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-220">You do this by setting your ApplicationSettings type in your code:</span></span>

```
AuthenticationSettings.Instance.setUseBroker(true);
```


#### <a name="step-2-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="70b22-221">2단계: URL 구성표와 함께 새 리디렉션 URI 설정</span><span class="sxs-lookup"><span data-stu-id="70b22-221">Step 2: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="70b22-222">올바른 응용 프로그램에 자격 증명 토큰을 항상 반환하는지 확인하려면 Android 운영 체제에서 확인할 수 있는 방식으로 응용 프로그램에 다시 호출하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-222">In order to ensure that we always return the credential tokens to the correct application, we need to make sure we call back to your application in a way that the Android operating system can verify.</span></span> <span data-ttu-id="70b22-223">Android 운영 체제는 Google Play 스토어에서 인증서의 해시를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-223">The Android operating system uses the hash of the certificate in the Google Play store.</span></span> <span data-ttu-id="70b22-224">불량 응용 프로그램에서 이를 스푸핑할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-224">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="70b22-225">따라서 토큰이 올바른 응용 프로그램에 반환되는지 확인하도록 브로커 응용 프로그램의 URI와 함께 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-225">Therefore, we leverage this along with the URI of our broker application to ensure that the tokens are returned to the correct application.</span></span> <span data-ttu-id="70b22-226">이 고유한 리디렉션 URI를 응용 프로그램 및 개발자 포털에서 리디렉션 URI로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-226">We require you to establish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="70b22-227">리디렉션 URI는 다음의 적절한 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-227">Your redirect URI must be in the proper form of:</span></span>

`msauth://packagename/Base64UrlencodedSignature`

<span data-ttu-id="70b22-228">예: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span><span class="sxs-lookup"><span data-stu-id="70b22-228">ex: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span></span>

<span data-ttu-id="70b22-229">[Azure Portal](https://portal.azure.com/)을 사용하여 앱 등록에 이 리디렉션 URI를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-229">This Redirect URI needs to be specified in your app registration using the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="70b22-230">Azure AD 앱 등록에 대한 자세한 내용은 [Azure Active Directory와 통합](active-directory-how-to-integrate.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70b22-230">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

#### <a name="step-3-set-up-the-correct-permissions-in-your-application"></a><span data-ttu-id="70b22-231">3단계: 응용 프로그램에 올바른 사용 권한 설정</span><span class="sxs-lookup"><span data-stu-id="70b22-231">Step 3: Set up the correct permissions in your application</span></span>
<span data-ttu-id="70b22-232">Android에서 브로커 응용 프로그램은 Android OS의 계정 관리자 기능을 사용하여 응용 프로그램 간에 자격 증명을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-232">Our broker application in Android uses the Accounts Manager feature of the Android OS to manage credentials across applications.</span></span> <span data-ttu-id="70b22-233">Android에서 브로커를 사용하려면 앱 매니페스트에 AccountManager 계정을 사용할 수 있는 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-233">In order to use the broker in Android your app manifest must have permissions to use AccountManager accounts.</span></span> <span data-ttu-id="70b22-234">이 부분은 [여기의 계정 관리자에 대한 Google 설명서](http://developer.android.com/reference/android/accounts/AccountManager.html)</span><span class="sxs-lookup"><span data-stu-id="70b22-234">This is discussed in detail in the [Google documentation for Account Manager here](http://developer.android.com/reference/android/accounts/AccountManager.html)</span></span>

<span data-ttu-id="70b22-235">특히 이러한 사용 권한은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-235">In particular, these permissions are:</span></span>

```
GET_ACCOUNTS
USE_CREDENTIALS
MANAGE_ACCOUNTS
```

### <a name="youve-configured-sso"></a><span data-ttu-id="70b22-236">SSO를 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-236">You've configured SSO!</span></span>
<span data-ttu-id="70b22-237">이제 Microsoft ID SDK는 자동으로 응용 프로그램에서 자격 증명을 공유하고 장치에 있는 경우 브로커를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="70b22-237">Now the Microsoft Identity SDK will automatically both share credentials across your applications and invoke the broker if it's present on their device.</span></span>

