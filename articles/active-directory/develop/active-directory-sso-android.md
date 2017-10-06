---
title: "aaaHow tooenable에 ADAL을 사용 하 여 Android 응용 프로그램 간 SSO | Microsoft Docs"
description: "어떻게 toouse hello 기능을 응용 프로그램에서 Single Sign On ADAL SDK tooenable hello 합니다. "
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
ms.openlocfilehash: 3867e15030e5516464e4dbd92ba35894430daf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-cross-app-sso-on-android-using-adal"></a><span data-ttu-id="34e98-103">어떻게 tooenable ADAL을 사용 하 여 android 응용 프로그램 간 SSO</span><span class="sxs-lookup"><span data-stu-id="34e98-103">How tooenable cross-app SSO on Android using ADAL</span></span>
<span data-ttu-id="34e98-104">사용자가 tooenter 자격 증명을 한 번만 필요 하 고 응용 프로그램에서 자동으로 회사 자격 증명을 갖게 있도록 Single Sign-on (SSO)를 제공 하 이제에서 예상 하는 고객 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-104">Providing Single Sign-On (SSO) so that users only need tooenter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="34e98-105">hello 어려움 작은 화면에 종종 시간 전화 통화 또는 문자로 전송 코드와 같은 추가 요소 (2FA)와 함께 자신의 사용자 이름과 암호를 입력 하는 경우 사용자 빠른 불만에 결과 toodo이 제품에 대 한 번 이상 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-105">hello difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has toodo this more than one time for your product.</span></span>

<span data-ttu-id="34e98-106">또한 Microsoft 계정 또는 office 365에서 작업 계정과 같은 다른 응용 프로그램이 사용할 수 있는 id 플랫폼에 적용 하면 고객이 자신의 모든 응용 프로그램에서 이러한 자격 증명 toobe 사용 가능한 toouse hello 공급 업체 관계 없이 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials toobe available toouse across all their applications no matter hello vendor.</span></span>

<span data-ttu-id="34e98-107">hello 우리의 Microsoft Identity Sdk와 함께 Microsoft Id 플랫폼 모든이 하드 작업을 수행 하 고 기능 toodelight SSO 하거나 응용 프로그램 또는 사용자 고유의 도구 모음 내에서 사용 하는 고객을 hello 제공 브로커 기능 및 인증자 hello 전체 장치에서 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="34e98-107">hello Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you hello ability toodelight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across hello entire device.</span></span>

<span data-ttu-id="34e98-108">이 연습에서는 열에 표시 방법을 tooconfigure 우리의 SDK 응용 프로그램 tooprovide 내에서이 혜택 tooyour 고객 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-108">This walkthrough will tell you how tooconfigure our SDK within your application tooprovide this benefit tooyour customers.</span></span>

<span data-ttu-id="34e98-109">이 연습은 다음에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="34e98-110">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="34e98-110">Azure Active Directory</span></span>
* <span data-ttu-id="34e98-111">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="34e98-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="34e98-112">Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="34e98-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="34e98-113">Azure Active Directory 조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="34e98-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="34e98-114">위의 hello 문서 너무 방법을 알고 있는 것으로 가정[Azure Active Directory에 대 한 hello 레거시 포털에서 응용 프로그램을 프로 비전](active-directory-how-to-integrate.md) hello로 응용 프로그램 통합 및 [Microsoft Identity Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android) .</span><span class="sxs-lookup"><span data-stu-id="34e98-114">hello document preceding assumes you know how too[provision applications in hello legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with hello [Microsoft Identity Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android).</span></span>

## <a name="sso-concepts-in-hello-microsoft-identity-platform"></a><span data-ttu-id="34e98-115">Microsoft Id 플랫폼 hello에 대 한 SSO 개념</span><span class="sxs-lookup"><span data-stu-id="34e98-115">SSO Concepts in hello Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="34e98-116">Microsoft ID Broker</span><span class="sxs-lookup"><span data-stu-id="34e98-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="34e98-117">Microsoft hello 여러 공급 업체의 응용 프로그램 전체에서 자격 증명의 브리징에 대 한 허용 하는 모든 모바일 플랫폼에 대 한 응용 프로그램을 제공 하 고 어디에서 단일 안전한 곳을 필요로 하는 특별 한 향상 된 기능에 대 한 허용 toovalidate 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-117">Microsoft provides applications for every mobile platform that allow for hello bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where toovalidate credentials.</span></span> <span data-ttu-id="34e98-118">이를 **브로커**라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-118">We call these **brokers**.</span></span> <span data-ttu-id="34e98-119">IOS 및 Android에서 고객에 독립적으로 설치 하거나 해당 직원에 대 한 일부 또는 모두 hello 장치를 관리 하는 회사에서 장치 toohello 푸시할 수는 다운로드 가능한 응용 프로그램을 통해 제공 됩니다 이러한.</span><span class="sxs-lookup"><span data-stu-id="34e98-119">On iOS and Android these are provided through downloadable applications that customers either install independently or can be pushed toohello device by a company who manages some or all of hello device for their employee.</span></span> <span data-ttu-id="34e98-120">이러한 브로커 일부 응용 프로그램 및 IT 관리자의 필요에 따라 hello 전체 장치에 대 한 관리 보안을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-120">These brokers support managing security just for some applications or hello entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="34e98-121">Windows에서 기술적으로 웹 인증 브로커 hello 라고 toohello 운영 체제에서 기본적으로 제공 하는 계정 선택 하 여이 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-121">In Windows, this functionality is provided by an account chooser built in toohello operating system, known technically as hello Web Authentication Broker.</span></span>

<span data-ttu-id="34e98-122">방법에 대 한 자세한 내용은 이러한 브로커 및 방법을 고객에 게 표시 될 수 하 hello Microsoft Id 플랫폼에 대 한 읽기에 대 한 자신의 로그인 흐름에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-122">For more information on how we use these brokers and how your customers might see them in their login flow for hello Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="34e98-123">모바일 장치에 로그인하기 위한 패턴</span><span class="sxs-lookup"><span data-stu-id="34e98-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="34e98-124">장치에 대 한 액세스 toocredentials hello Microsoft Identity 플랫폼에 대 한 두 가지 기본 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-124">Access toocredentials on devices follow two basic patterns for hello Microsoft Identity platform:</span></span>

* <span data-ttu-id="34e98-125">비 브로커 지원 로그인</span><span class="sxs-lookup"><span data-stu-id="34e98-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="34e98-126">브로커 지원 로그인</span><span class="sxs-lookup"><span data-stu-id="34e98-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="34e98-127">비 브로커 지원 로그인</span><span class="sxs-lookup"><span data-stu-id="34e98-127">Non-broker assisted logins</span></span>
<span data-ttu-id="34e98-128">비 브로커 보조 로그인은 hello 응용 프로그램을 사용 하 여 인라인으로 발생 하지 않으며 해당 응용 프로그램에 대 한 hello 장치에서 hello 로컬 저장소를 사용 하는 로그인 환경을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-128">Non-broker assisted logins are login experiences that happen inline with hello application and use hello local storage on hello device for that application.</span></span> <span data-ttu-id="34e98-129">이 저장소는 응용 프로그램 간에 공유 될 수 있습니다 하지만 hello 자격 증명이 밀접 하 게 toohello 응용 프로그램 또는 제품군이 자격 증명을 사용 하는 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-129">This storage may be shared across applications but hello credentials are tightly bound toohello app or suite of apps using that credential.</span></span> <span data-ttu-id="34e98-130">경험해 본 있다면 대개이 많은 모바일 응용 프로그램에서 사용자 이름 및 hello 응용 프로그램 자체 내에 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-130">You've most likely experienced this in many mobile applications when you enter a username and password within hello application itself.</span></span>

<span data-ttu-id="34e98-131">이러한 로그인 hello 이점을 뒤에</span><span class="sxs-lookup"><span data-stu-id="34e98-131">These logins have hello following benefits:</span></span>

* <span data-ttu-id="34e98-132">Hello 응용 프로그램 내 사용자 환경이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-132">User experience exists entirely within hello application.</span></span>
* <span data-ttu-id="34e98-133">Hello로 서명 된 응용 프로그램에서 자격 증명을 공유할 수 동일한 인증서를 응용 프로그램 single sign on 환경을 tooyour 제품군을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-133">Credentials can be shared across applications that are signed by hello same certificate, providing a single sign-on experience tooyour suite of applications.</span></span>
* <span data-ttu-id="34e98-134">로깅 hello 환경 전체에 제어를 이전 및 이후 로그인 toohello 응용 프로그램에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-134">Control around hello experience of logging in is provided toohello application before and after sign-in.</span></span>

<span data-ttu-id="34e98-135">이러한 로그인 있어야 hello 다음 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-135">These logins have hello following drawbacks:</span></span>

* <span data-ttu-id="34e98-136">사용자는 Microsoft ID를 사용하는 모든 앱이 아닌 응용 프로그램이 구성한 해당 Microsoft ID 간에서만 Single Sign-On을 경험할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="34e98-137">응용 프로그램을 사용 하 여 hello InTune 제품군 또는 조건부 액세스 등의 고급 비즈니스 기능으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-137">Your application cannot be used with more advanced business features such as Conditional Access or use hello InTune suite of products.</span></span>
* <span data-ttu-id="34e98-138">응용 프로그램은 비즈니스 사용자에 대한 인증서 기반 인증을 지원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="34e98-139">Microsoft Identity Sdk hello 프로그램 응용 프로그램 tooenable SSO의 hello 공유 저장소에서 작동 하는 방법에 대 한 표현을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-139">Here is a representation of how hello Microsoft Identity SDKs work with hello shared storage of your applications tooenable SSO:</span></span>

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

#### <a name="broker-assisted-logins"></a><span data-ttu-id="34e98-140">브로커 지원 로그인</span><span class="sxs-lookup"><span data-stu-id="34e98-140">Broker assisted logins</span></span>
<span data-ttu-id="34e98-141">Broker 기반 로그인에는 hello 저장 및 hello 브로커 tooshare 자격 증명의 보안을 사용 하 여 hello Microsoft Id 플랫폼을 적용 하는 hello 장치에서 모든 응용 프로그램 사이의 hello broker 응용 프로그램 내에서 발생 하는 로그인 환경이 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-141">Broker-assisted logins are login experiences that occur within hello broker application and use hello storage and security of hello broker tooshare credentials across all applications on hello device that apply hello Microsoft Identity platform.</span></span> <span data-ttu-id="34e98-142">이 응용 프로그램의 hello 브로커 toosign 사용자가 사용 한다는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-142">This means that your applications rely on hello broker toosign users in.</span></span> <span data-ttu-id="34e98-143">IOS 및 Android에서 이러한 브로커는 고객에 독립적으로 설치 하거나 해당 사용자에 대 한 hello 장치를 관리 하는 회사에서 장치 toohello 푸시할 수는 다운로드 가능한 응용 프로그램을 통해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed toohello device by a company who manages hello device for their user.</span></span> <span data-ttu-id="34e98-144">이러한 유형의 응용 프로그램의 예는 iOS에서 hello Microsoft Authenticator 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-144">An example of this type of application is hello Microsoft Authenticator application on iOS.</span></span> <span data-ttu-id="34e98-145">Windows 웹 인증 브로커 hello 라고 기술적으로 toohello 운영 체제에서 기본적으로 제공 하는 계정 선택 하 여이 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-145">In Windows this functionality is provided by an account chooser built in toohello operating system, known technically as hello Web Authentication Broker.</span></span>
<span data-ttu-id="34e98-146">hello 경험 플랫폼에 따라 다르며 하며 중단 toousers 수 되지 않은 경우 올바르게 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-146">hello experience varies by platform and can sometimes be disruptive toousers if not managed correctly.</span></span> <span data-ttu-id="34e98-147">익숙한 아마도 가장이 패턴 hello Facebook 응용 프로그램이 설치 된 다른 응용 프로그램에서 Facebook Connect를 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="34e98-147">You're probably most familiar with this pattern if you have hello Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="34e98-148">hello Microsoft Identity 플랫폼 사용 하 여 hello 같은 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-148">hello Microsoft Identity platform uses hello same pattern.</span></span>

<span data-ttu-id="34e98-149">IOS에 대 한이 인해 tooa "전환" 애니메이션 전송 대상에 응용 프로그램 toohello 백그라운드 hello Microsoft Authenticator 응용 프로그램 사용자 tooselect hello에 대 한 toohello 전경 제공 사용한 toosign 만족할 만한 계정.</span><span class="sxs-lookup"><span data-stu-id="34e98-149">For iOS this leads tooa "transition" animation where your application is sent toohello background while hello Microsoft Authenticator applications comes toohello foreground for hello user tooselect which account they would like toosign in with.</span></span>  

<span data-ttu-id="34e98-150">Android 및 Windows hello 계정에 대 한 선택은 덜 중단 toohello 사용자는 응용 프로그램 맨 위에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-150">For Android and Windows hello account chooser is displayed on top of your application which is less disruptive toohello user.</span></span>

#### <a name="how-hello-broker-gets-invoked"></a><span data-ttu-id="34e98-151">Hello broker가 호출 하는 방법</span><span class="sxs-lookup"><span data-stu-id="34e98-151">How hello broker gets invoked</span></span>
<span data-ttu-id="34e98-152">호환 되는 broker hello Microsoft Authenticator 응용 프로그램, Microsoft Identity Sdk hello가 자동으로 같은 hello 장치가에 설치 된 경우에 사용자 toolog에서 모든 계정을 사용 하 여 만들려는 되었음을 나타낼 때 사용자에 대 한 hello 브로커 호출 작업 hello 수행 hello Microsoft Identity 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-152">If a compatible broker is installed on hello device, like hello Microsoft Authenticator application, hello Microsoft Identity SDKs will automatically do hello work of invoking hello broker for you when a user indicates they wish toolog in using any account from hello Microsoft Identity platform.</span></span> <span data-ttu-id="34e98-153">이 계정은 개인 Microsoft 계정, 회사 또는 학교 계정 또는 B2C 및 B2B 제품을 사용하여 Azure에 제공 및 호스트하는 계정일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 
 
 #### <a name="how-we-ensure-hello-application-is-valid"></a><span data-ttu-id="34e98-154">올바른지 hello 응용 프로그램 인지 확인 하는 방법</span><span class="sxs-lookup"><span data-stu-id="34e98-154">How we ensure hello application is valid</span></span>
 
 <span data-ttu-id="34e98-155">응용 프로그램 호출 hello 브로커 hello 필요 tooensure hello id가 중요 한 toohello 보안에서 지원 되는 broker 로그인을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-155">hello need tooensure hello identity of an application call hello broker is crucial toohello security we provide in broker assisted logins.</span></span> <span data-ttu-id="34e98-156">IOS 나 Android 악성 응용 프로그램이 "스푸핑"는 올바른 응용 프로그램의 식별자를 업데이트 하 고 hello 합법적인 응용 프로그램을 위한 hello 토큰을 수신할 수 있습니다 하므로 지정된 된 응용 프로그램에 대해서만 사용할 수 있는 고유 식별자를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive hello tokens meant for hello legitimate application.</span></span> <span data-ttu-id="34e98-157">런타임 시 hello 오른쪽 응용 프로그램과 알립니다 항상 tooensure, 반드시 hello 개발자 tooprovide 사용자 지정 redirectURI Microsoft와 응용 프로그램을 등록할 때 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-157">tooensure we are always communicating with hello right application at runtime, we ask hello developer tooprovide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="34e98-158">**개발자가 이 리디렉션 URI를 만드는 방법은 아래에 자세히 설명되어 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="34e98-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="34e98-159">이 사용자 지정 redirectURI hello 응용 프로그램의 hello 인증서 지문을 있어서 hello Google Play 스토어에 의해 toobe 고유 toohello 응용 프로그램을 보장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-159">This custom redirectURI contains hello certificate thumbprint of hello application and is ensured toobe unique toohello application by hello Google Play Store.</span></span> <span data-ttu-id="34e98-160">응용 프로그램 호출 hello 브로커 hello 브로커 hello Android 운영 체제 tooprovide 요청 hello와 인증서 지문을 해당 호출된 hello 브로커 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-160">When an application calls hello broker, hello broker asks hello Android operating system tooprovide it with hello certificate thumbprint that called hello broker.</span></span> <span data-ttu-id="34e98-161">hello broker hello 호출 tooour id 시스템에이 인증서 지문 tooMicrosoft를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-161">hello broker provides this certificate thumbprint tooMicrosoft in hello call tooour identity system.</span></span> <span data-ttu-id="34e98-162">Hello 응용 프로그램의 지문 hello 인증서 지문에 맞지 않는 hello 인증서를 제공 하면 hello 개발자가 toous 등록 하는 동안에서는 액세스를 거부할 toohello 토큰 hello 리소스 hello 응용 프로그램이 요청에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-162">If hello certificate thumbprint of hello application does not match hello certificate thumbprint provided toous by hello developer during registration, we will deny access toohello tokens for hello resource hello application is requesting.</span></span> <span data-ttu-id="34e98-163">이 검사는 hello 개발자가 등록 된 hello 응용 프로그램이 토큰 수신 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-163">This check ensures that only hello application registered by hello developer receives tokens.</span></span>

<span data-ttu-id="34e98-164">**hello 개발자는 Microsoft Identity SDK hello hello 브로커를 호출 하거나 hello 비 브로커 보조 흐름을 사용 하는 경우 hello 선택을 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="34e98-164">**hello developer has hello choice of if hello Microsoft Identity SDK calls hello broker or uses hello non-broker assisted flow.**</span></span> <span data-ttu-id="34e98-165">그러나 하지 toouse hello 브로커 기반 흐름을 선택 하는 hello 개발자의 경우 이러한 hello의 이점을 잃게 SSO 자격 증명을 사용 하 여 해당 hello 사용자 hello 장치에 이미 추가한 수 없고을 Microsoft 비즈니스 기능과 함께 사용 하는 응용 프로그램 조건부 액세스, Intune 관리 기능 및 인증서 기반 인증 같은 고객을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-165">However if hello developer chooses not toouse hello broker-assisted flow they lose hello benefit of using SSO credentials that hello user may have already added on hello device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="34e98-166">이러한 로그인 hello 이점을 뒤에</span><span class="sxs-lookup"><span data-stu-id="34e98-166">These logins have hello following benefits:</span></span>

* <span data-ttu-id="34e98-167">Hello 공급 업체에 관계 없이 자신의 모든 응용 프로그램에 SSO를 경험 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-167">User experiences SSO across all their applications no matter hello vendor.</span></span>
* <span data-ttu-id="34e98-168">응용 프로그램 조건부 액세스 등의 고급 비즈니스 기능을 사용 하거나 제품 hello InTune 그룹을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-168">Your application can use more advanced business features such as Conditional Access or use hello InTune suite of products.</span></span>
* <span data-ttu-id="34e98-169">응용 프로그램은 비즈니스 사용자에 대한 인증서 기반 인증을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="34e98-170">훨씬 더 안전한 로그인 환경의 hello broker 응용 프로그램 추가 보안 알고리즘 및 암호화가 hello hello 응용 프로그램 및 hello 사용자 신원을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-170">Much more secure sign-in experience as hello identity of hello application and hello user are verified by hello broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="34e98-171">이러한 로그인 있어야 hello 다음 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-171">These logins have hello following drawbacks:</span></span>

* <span data-ttu-id="34e98-172">IOS에서 hello 사용자 자격 증명을 선택 하는 동안 응용 프로그램의 환경이 전환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-172">In iOS hello user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="34e98-173">응용 프로그램 내에서 고객에 대 한 hello 기능 toomanage hello 로그인의 손실 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-173">Loss of hello ability toomanage hello login experience for your customers within your application.</span></span>

<span data-ttu-id="34e98-174">Hello Microsoft Identity Sdk 작업 hello로 응용 프로그램 tooenable SSO broker 하는 방법에 대 한 표현을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-174">Here is a representation of how hello Microsoft Identity SDKs work with hello broker applications tooenable SSO:</span></span>

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

<span data-ttu-id="34e98-175">이 배경 정보를 갖춘 있어야 수 toobetter 이해 하 고 hello Microsoft Id 플랫폼 및 Sdk를 사용 하 여 응용 프로그램 내에서 SSO를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-175">Armed with this background information you should be able toobetter understand and implement SSO within your application using hello Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="34e98-176">ADAL을 사용하여 앱 간 SSO 활성화</span><span class="sxs-lookup"><span data-stu-id="34e98-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="34e98-177">Hello ADAL Android SDK 사용 하 여 여기에:</span><span class="sxs-lookup"><span data-stu-id="34e98-177">Here we use hello ADAL Android SDK to:</span></span>

* <span data-ttu-id="34e98-178">앱 제품군에 대한 비 브로커 지원 SSO 설정</span><span class="sxs-lookup"><span data-stu-id="34e98-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="34e98-179">브로커 지원 SSO에 대한 지원 설정</span><span class="sxs-lookup"><span data-stu-id="34e98-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="34e98-180">비 브로커 지원 SSO에 대한 SSO 설정</span><span class="sxs-lookup"><span data-stu-id="34e98-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="34e98-181">비 브로커 보조 SSO 응용 프로그램 전반에 대 한 Microsoft Identity Sdk hello SSO의 hello 복잡성 많이를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-181">For non-broker assisted SSO across applications hello Microsoft Identity SDKs manage much of hello complexity of SSO for you.</span></span> <span data-ttu-id="34e98-182">Hello 캐시에 hello 올바른 사용자를 찾아서 tooquery 있습니다에 대 한 로그인된 사용자의 목록을 유지 관리 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-182">This includes finding hello right user in hello cache and maintaining a list of logged in users for you tooquery.</span></span>

<span data-ttu-id="34e98-183">다음 toodo hello 필요를 소유 하는 응용 프로그램 전체에서 SSO tooenable:</span><span class="sxs-lookup"><span data-stu-id="34e98-183">tooenable SSO across applications you own you need toodo hello following:</span></span>

1. <span data-ttu-id="34e98-184">모든 사용자 응용 프로그램 사용자 hello 같은 클라이언트 ID 또는 id입니다. 응용 프로그램 확인</span><span class="sxs-lookup"><span data-stu-id="34e98-184">Ensure all your applications user hello same Client ID or Application ID.</span></span>
2. <span data-ttu-id="34e98-185">모든 응용 프로그램이 동일한 SharedUserID 설정 hello 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="34e98-185">Ensure all your applications have hello same SharedUserID set.</span></span>
3. <span data-ttu-id="34e98-186">모든 저장소를 공유할 수 있도록 hello Google Play에서에서 동일한 서명 인증서를 저장 하면 응용 프로그램 공유 hello 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-186">Ensure that all of your applications share hello same signing certificate from hello Google Play store so that you can share storage.</span></span>

#### <a name="step-1-using-hello-same-client-id--application-id-for-all-hello-applications-in-your-suite-of-apps"></a><span data-ttu-id="34e98-187">1 단계: 동일한 클라이언트 ID를 hello를 사용 하 여 / 응용 프로그램의 응용 프로그램 도구 모음에 모든 hello에 대 한 응용 프로그램 ID</span><span class="sxs-lookup"><span data-stu-id="34e98-187">Step 1: Using hello same Client ID / Application ID for all hello applications in your suite of apps</span></span>
<span data-ttu-id="34e98-188">Microsoft Identity 플랫폼 tooknow hello에 대 한 응용 프로그램에서 tooshare 토큰 수 있는지, 각 응용 프로그램이 있어야 tooshare hello 같은 클라이언트 ID 또는 응용 프로그램 id입니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-188">In order for hello Microsoft Identity platform tooknow that it's allowed tooshare tokens across your applications, each of your applications will need tooshare hello same Client ID or Application ID.</span></span> <span data-ttu-id="34e98-189">Hello 포털에서 첫 번째 응용 프로그램을 등록할 때 tooyou 제공한 hello 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-189">This is hello unique identifier that was provided tooyou when you registered your first application in hello portal.</span></span>

<span data-ttu-id="34e98-190">다양 한 앱 식별 하는 방법 할까요 toohello Microsoft Id 서비스를 사용 하는 경우 hello 동일한 응용 프로그램 id입니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-190">You may be wondering how you will identify different apps toohello Microsoft Identity service if it uses hello same Application ID.</span></span> <span data-ttu-id="34e98-191">hello 대답이 hello로 **리디렉션 Uri**합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-191">hello answer is with hello **Redirect URIs**.</span></span> <span data-ttu-id="34e98-192">각 응용 프로그램에는 hello 등록 포털에 등록 한 리디렉션 Uri 여러 개 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-192">Each application can have multiple Redirect URIs registered in hello onboarding portal.</span></span> <span data-ttu-id="34e98-193">제품의 각 앱은 다른 리디렉션 URI를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-193">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="34e98-194">표시되는 모양의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-194">An example of how this looks is below:</span></span>

<span data-ttu-id="34e98-195">App1 리디렉션 URI: `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span><span class="sxs-lookup"><span data-stu-id="34e98-195">App1 Redirect URI: `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span></span>

<span data-ttu-id="34e98-196">App2 리디렉션 URI: `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span><span class="sxs-lookup"><span data-stu-id="34e98-196">App2 Redirect URI: `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span></span>

<span data-ttu-id="34e98-197">App3 리디렉션 URI: `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span><span class="sxs-lookup"><span data-stu-id="34e98-197">App3 Redirect URI: `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span></span>

<span data-ttu-id="34e98-198">....</span><span class="sxs-lookup"><span data-stu-id="34e98-198">....</span></span>

<span data-ttu-id="34e98-199">아래에 중첩 된 이러한 동일한 클라이언트 ID를 hello / 응용 프로그램 ID 및 조회에 따라 hello에 대 한 리디렉션 URI SDK 구성에서 toous을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-199">These are nested under hello same client ID / application ID and looked up based on hello redirect URI you return toous in your SDK configuration.</span></span>

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


<span data-ttu-id="34e98-200">*이러한 리디렉션 Uri의 형식은 hello는 아래 설명 되어 있습니다. 이 경우 이러한 해야 다음과 같은 hello 위의 toosupport hello broker 싶지 않다면 모든 리디렉션 URI를 사용할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="34e98-200">*Note that hello format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish toosupport hello broker, in which case they must look something like hello above*</span></span>

#### <a name="step-2-configuring-shared-storage-in-android"></a><span data-ttu-id="34e98-201">2단계: Android에서 공유 저장소 구성</span><span class="sxs-lookup"><span data-stu-id="34e98-201">Step 2: Configuring shared storage in Android</span></span>
<span data-ttu-id="34e98-202">설정 hello `SharedUserID` hello hello에 Google Android 설명서를 참조 하 여 피어에서 확인 될 수 있지만이 설명서의 hello 범위를 벗어납니다 [매니페스트](http://developer.android.com/guide/topics/manifest/manifest-element.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-202">Setting hello `SharedUserID` is beyond hello scope of this document but can be learned by reading hello Google Android documentation on hello [Manifest](http://developer.android.com/guide/topics/manifest/manifest-element.html).</span></span> <span data-ttu-id="34e98-203">중요한 것은 사용자가 sharedUserID가 불리는 이름을 결정하는 것과 모든 응용 프로그램에서 이를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-203">What is important is that you decide what you want your sharedUserID will be called and use that across all your applications.</span></span>

<span data-ttu-id="34e98-204">Hello 있으면 `SharedUserID` 준비 toouse SSO는 응용 프로그램에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-204">Once you have hello `SharedUserID` in all your applications you are ready toouse SSO.</span></span>

> [!WARNING]
> <span data-ttu-id="34e98-205">응용 프로그램에서 저장소를 공유 하는 경우 모든 응용 프로그램 사용자를 삭제 하거나 나빠지는 지 응용 프로그램에서 모든 hello 토큰을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-205">When you share storage across your applications any application can delete users, or worse delete all hello tokens across your application.</span></span> <span data-ttu-id="34e98-206">이 hello 토큰 toodo 백그라운드 작업을 사용 하는 응용 프로그램의 경우에 특히 재해로입니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-206">This is particularly disastrous if you have applications that rely on hello tokens toodo background work.</span></span> <span data-ttu-id="34e98-207">저장소를 공유 hello Microsoft Identity Sdk를 통해 모든 제거 작업에 특히 주의 이어야 한다는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-207">Sharing storage means that you must be very careful in any and all remove operations through hello Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="34e98-208">이것으로 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-208">That's it!</span></span> <span data-ttu-id="34e98-209">이제 Microsoft Identity SDK hello 응용 프로그램에서 자격 증명을 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-209">hello Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="34e98-210">hello 사용자 목록도 응용 프로그램 인스턴스 간에 공유 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-210">hello user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="34e98-211">브로커 지원 SSO에 대한 SSO 설정</span><span class="sxs-lookup"><span data-stu-id="34e98-211">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="34e98-212">응용 프로그램 toouse hello 장치에 설치 되어 있는 모든 broker에 대 한 기능 hello **기본적으로 해제 되어**합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-212">hello ability for an application toouse any broker that is installed on hello device is **turned off by default**.</span></span> <span data-ttu-id="34e98-213">순서로 toouse 응용 프로그램 hello 브로커와 몇 가지 추가 구성을 변경 하 고 일부 코드 tooyour 응용 프로그램을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-213">In order toouse your application with hello broker you must do some additional configuration and add some code tooyour application.</span></span>

<span data-ttu-id="34e98-214">hello 단계 toofollow가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-214">hello steps toofollow are:</span></span>

1. <span data-ttu-id="34e98-215">응용 프로그램 코드의 호출 toohello MS SDK에서에서 broker 모드를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="34e98-215">Enable broker mode in your application code's call toohello MS SDK</span></span>
2. <span data-ttu-id="34e98-216">새 리디렉션 URI를 설정 하 고 해당 tooboth hello 앱 및 앱 등록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-216">Establish a new redirect URI and provide that tooboth hello app and your app registration</span></span>
3. <span data-ttu-id="34e98-217">올바른 권한을 hello Android 매니페스트에서 hello 설정</span><span class="sxs-lookup"><span data-stu-id="34e98-217">Setting up hello correct permissions in hello Android manifest</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="34e98-218">1단계: 응용 프로그램에서 브로커 모드 활성화</span><span class="sxs-lookup"><span data-stu-id="34e98-218">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="34e98-219">"hello"설정 또는 인증 인스턴스의 초기 설정을 만들 때 응용 프로그램 toouse hello broker 프로그램에 대 한 hello 기능이 켜 집니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-219">hello ability for your application toouse hello broker is turned on when you create hello "settings" or initial setup of your Authentication instance.</span></span> <span data-ttu-id="34e98-220">코드에서 ApplicationSettings 형식을 설정하여 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-220">You do this by setting your ApplicationSettings type in your code:</span></span>

```
AuthenticationSettings.Instance.setUseBroker(true);
```


#### <a name="step-2-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="34e98-221">2단계: URL 구성표와 함께 새 리디렉션 URI 설정</span><span class="sxs-lookup"><span data-stu-id="34e98-221">Step 2: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="34e98-222">에 항상 반환 hello 자격 증명 토큰 toohello 올바른 응용 프로그램 순서 tooensure, toomake म 콜백할 hello Android 운영 체제가 설치 하는 방식으로 tooyour 응용 프로그램을 확인할 수 있는지 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-222">In order tooensure that we always return hello credential tokens toohello correct application, we need toomake sure we call back tooyour application in a way that hello Android operating system can verify.</span></span> <span data-ttu-id="34e98-223">hello Android 운영 체제 hello Google Play 스토어에에서 hello 인증서의 hello 해시를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-223">hello Android operating system uses hello hash of hello certificate in hello Google Play store.</span></span> <span data-ttu-id="34e98-224">불량 응용 프로그램에서 이를 스푸핑할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-224">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="34e98-225">따라서 활용 하 여이 hello hello 토큰 toohello 올바른 응용 프로그램으로 반환 됨 우리의 broker 응용 프로그램 tooensure의 URI와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-225">Therefore, we leverage this along with hello URI of our broker application tooensure that hello tokens are returned toohello correct application.</span></span> <span data-ttu-id="34e98-226">필요 하면 tooestablish이 고유 리디렉션 URI를 모두 설정 하 여 응용 프로그램에서 리디렉션 URI로 우리의 개발자 포털에서.</span><span class="sxs-lookup"><span data-stu-id="34e98-226">We require you tooestablish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="34e98-227">Hello 적절 한 형태의 사용자 리디렉션 URI 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-227">Your redirect URI must be in hello proper form of:</span></span>

`msauth://packagename/Base64UrlencodedSignature`

<span data-ttu-id="34e98-228">예: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span><span class="sxs-lookup"><span data-stu-id="34e98-228">ex: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span></span>

<span data-ttu-id="34e98-229">이 리디렉션 URI toobe hello를 사용 하 여 응용 프로그램 등록에 지정 된 필요한 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-229">This Redirect URI needs toobe specified in your app registration using hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="34e98-230">Azure AD 앱 등록에 대한 자세한 내용은 [Azure Active Directory와 통합](active-directory-how-to-integrate.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="34e98-230">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

#### <a name="step-3-set-up-hello-correct-permissions-in-your-application"></a><span data-ttu-id="34e98-231">3 단계: 응용 프로그램에서 올바른 권한을 hello 설정</span><span class="sxs-lookup"><span data-stu-id="34e98-231">Step 3: Set up hello correct permissions in your application</span></span>
<span data-ttu-id="34e98-232">응용 프로그램 간에 hello Android OS toomanage 자격 증명의 hello 계정 관리자 기능을 사용 하는 Android에서 해당 broker 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-232">Our broker application in Android uses hello Accounts Manager feature of hello Android OS toomanage credentials across applications.</span></span> <span data-ttu-id="34e98-233">Android에서 주문 toouse hello 브로커에서 응용 프로그램 매니페스트에 권한을 toouse AccountManager 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-233">In order toouse hello broker in Android your app manifest must have permissions toouse AccountManager accounts.</span></span> <span data-ttu-id="34e98-234">Hello에 자세히 설명 되어 있음 [Google 계정 관리자에 대 한 설명서 센터의 설명서](http://developer.android.com/reference/android/accounts/AccountManager.html)</span><span class="sxs-lookup"><span data-stu-id="34e98-234">This is discussed in detail in hello [Google documentation for Account Manager here](http://developer.android.com/reference/android/accounts/AccountManager.html)</span></span>

<span data-ttu-id="34e98-235">특히 이러한 사용 권한은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-235">In particular, these permissions are:</span></span>

```
GET_ACCOUNTS
USE_CREDENTIALS
MANAGE_ACCOUNTS
```

### <a name="youve-configured-sso"></a><span data-ttu-id="34e98-236">SSO를 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-236">You've configured SSO!</span></span>
<span data-ttu-id="34e98-237">이제 Microsoft Identity SDK hello에서는 자동으로 응용 프로그램에서 자격 증명을 공유를 자신의 장치에 표시 되지 않으면 hello 브로커를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="34e98-237">Now hello Microsoft Identity SDK will automatically both share credentials across your applications and invoke hello broker if it's present on their device.</span></span>

