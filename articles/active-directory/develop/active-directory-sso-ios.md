---
title: "aaaHow tooenable ADAL을 사용 하 여 iOS에서 응용 프로그램 간 SSO | Microsoft Docs"
description: "어떻게 toouse hello 기능을 응용 프로그램에서 Single Sign On ADAL SDK tooenable hello 합니다. "
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: d042d6da-7503-4e20-bb55-06917de01fcd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 04/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: b7b4389a8dcd956211ffa1aaa431aaf21ded8961
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-cross-app-sso-on-ios-using-adal"></a><span data-ttu-id="26df9-103">어떻게 tooenable ADAL을 사용 하 여 iOS에서 응용 프로그램 간 SSO</span><span class="sxs-lookup"><span data-stu-id="26df9-103">How tooenable cross-app SSO on iOS using ADAL</span></span>
<span data-ttu-id="26df9-104">사용자가 tooenter 자격 증명을 한 번만 필요 하 고 응용 프로그램에서 자동으로 회사 자격 증명을 갖게 있도록 Single Sign-on (SSO)를 제공 하 이제에서 예상 하는 고객 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-104">Providing Single Sign-On (SSO) so that users only need tooenter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="26df9-105">hello 어려움 작은 화면에 종종 시간 전화 통화 또는 문자로 전송 코드와 같은 추가 요소 (2FA)와 함께 자신의 사용자 이름과 암호를 입력 하는 경우 사용자 빠른 불만에 결과 toodo이 제품에 대 한 번 이상 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-105">hello difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has toodo this more than one time for your product.</span></span>

<span data-ttu-id="26df9-106">또한 Microsoft 계정 또는 office 365에서 작업 계정과 같은 다른 응용 프로그램이 사용할 수 있는 id 플랫폼에 적용 하면 고객이 자신의 모든 응용 프로그램에서 이러한 자격 증명 toobe 사용 가능한 toouse hello 공급 업체 관계 없이 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials toobe available toouse across all their applications no matter hello vendor.</span></span>

<span data-ttu-id="26df9-107">hello 우리의 Microsoft Identity Sdk와 함께 Microsoft Id 플랫폼 모든이 하드 작업을 수행 하 고 기능 toodelight SSO 하거나 응용 프로그램 또는 사용자 고유의 도구 모음 내에서 사용 하는 고객을 hello 제공 브로커 기능 및 인증자 hello 전체 장치에서 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="26df9-107">hello Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you hello ability toodelight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across hello entire device.</span></span>

<span data-ttu-id="26df9-108">이 연습에서는 열에 표시 방법을 tooconfigure 우리의 SDK 응용 프로그램 tooprovide 내에서이 혜택 tooyour 고객 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-108">This walkthrough will tell you how tooconfigure our SDK within your application tooprovide this benefit tooyour customers.</span></span>

<span data-ttu-id="26df9-109">이 연습은 다음에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="26df9-110">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="26df9-110">Azure Active Directory</span></span>
* <span data-ttu-id="26df9-111">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="26df9-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="26df9-112">Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="26df9-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="26df9-113">Azure Active Directory 조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="26df9-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="26df9-114">위의 hello 문서 너무 방법을 알고 있는 것으로 가정[Azure Active Directory에 대 한 hello 레거시 포털에서 응용 프로그램을 프로 비전](active-directory-how-to-integrate.md) hello로 응용 프로그램 통합 및 [Microsoft Identity iOS SDK](https://github.com/AzureAD/azure-activedirectory-library-for-objc)합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-114">hello document preceding assumes you know how too[provision applications in hello legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with hello [Microsoft Identity iOS SDK](https://github.com/AzureAD/azure-activedirectory-library-for-objc).</span></span>

## <a name="sso-concepts-in-hello-microsoft-identity-platform"></a><span data-ttu-id="26df9-115">Microsoft Id 플랫폼 hello에 대 한 SSO 개념</span><span class="sxs-lookup"><span data-stu-id="26df9-115">SSO Concepts in hello Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="26df9-116">Microsoft ID Broker</span><span class="sxs-lookup"><span data-stu-id="26df9-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="26df9-117">Microsoft hello 여러 공급 업체의 응용 프로그램 전체에서 자격 증명의 브리징에 대 한 허용 하는 모든 모바일 플랫폼에 대 한 응용 프로그램을 제공 하 고 어디에서 단일 안전한 곳을 필요로 하는 특별 한 향상 된 기능에 대 한 허용 toovalidate 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-117">Microsoft provides applications for every mobile platform that allow for hello bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where toovalidate credentials.</span></span> <span data-ttu-id="26df9-118">이를 **브로커**라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-118">We call these **brokers**.</span></span> <span data-ttu-id="26df9-119">IOS 및 Android에서 이러한 브로커는 고객에 독립적으로 설치 하거나 해당 직원에 대 한 일부 또는 모두 hello 장치를 관리 하는 회사에서 장치 toohello 푸시할 수는 다운로드 가능한 응용 프로그램을 통해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-119">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed toohello device by a company who manages some or all of hello device for their employee.</span></span> <span data-ttu-id="26df9-120">이러한 브로커 일부 응용 프로그램 및 IT 관리자의 필요에 따라 hello 전체 장치에 대 한 관리 보안을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-120">These brokers support managing security just for some applications or hello entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="26df9-121">Windows에서 기술적으로 웹 인증 브로커 hello 라고 toohello 운영 체제에서 기본적으로 제공 하는 계정 선택 하 여이 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-121">In Windows, this functionality is provided by an account chooser built in toohello operating system, known technically as hello Web Authentication Broker.</span></span>

<span data-ttu-id="26df9-122">방법에 대 한 자세한 내용은 이러한 브로커 및 방법을 고객에 게 표시 될 수 하 hello Microsoft Id 플랫폼에 대 한 읽기에 대 한 자신의 로그인 흐름에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-122">For more information on how we use these brokers and how your customers might see them in their login flow for hello Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="26df9-123">모바일 장치에 로그인하기 위한 패턴</span><span class="sxs-lookup"><span data-stu-id="26df9-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="26df9-124">장치에 대 한 액세스 toocredentials hello Microsoft Identity 플랫폼에 대 한 두 가지 기본 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-124">Access toocredentials on devices follow two basic patterns for hello Microsoft Identity platform:</span></span>

* <span data-ttu-id="26df9-125">비 브로커 지원 로그인</span><span class="sxs-lookup"><span data-stu-id="26df9-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="26df9-126">브로커 지원 로그인</span><span class="sxs-lookup"><span data-stu-id="26df9-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="26df9-127">비 브로커 지원 로그인</span><span class="sxs-lookup"><span data-stu-id="26df9-127">Non-broker assisted logins</span></span>
<span data-ttu-id="26df9-128">비 브로커 보조 로그인은 hello 응용 프로그램을 사용 하 여 인라인으로 발생 하지 않으며 해당 응용 프로그램에 대 한 hello 장치에서 hello 로컬 저장소를 사용 하는 로그인 환경을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-128">Non-broker assisted logins are login experiences that happen inline with hello application and use hello local storage on hello device for that application.</span></span> <span data-ttu-id="26df9-129">이 저장소는 응용 프로그램 간에 공유 될 수 있습니다 하지만 hello 자격 증명이 밀접 하 게 toohello 응용 프로그램 또는 제품군이 자격 증명을 사용 하는 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-129">This storage may be shared across applications but hello credentials are tightly bound toohello app or suite of apps using that credential.</span></span> <span data-ttu-id="26df9-130">경험해 본 있다면 대개이 많은 모바일 응용 프로그램에서 사용자 이름 및 hello 응용 프로그램 자체 내에 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-130">You've most likely experienced this in many mobile applications when you enter a username and password within hello application itself.</span></span>

<span data-ttu-id="26df9-131">이러한 로그인 hello 이점을 뒤에</span><span class="sxs-lookup"><span data-stu-id="26df9-131">These logins have hello following benefits:</span></span>

* <span data-ttu-id="26df9-132">Hello 응용 프로그램 내 사용자 환경이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-132">User experience exists entirely within hello application.</span></span>
* <span data-ttu-id="26df9-133">Hello로 서명 된 응용 프로그램에서 자격 증명을 공유할 수 동일한 인증서를 응용 프로그램 single sign on 환경을 tooyour 제품군을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-133">Credentials can be shared across applications that are signed by hello same certificate, providing a single sign-on experience tooyour suite of applications.</span></span>
* <span data-ttu-id="26df9-134">로깅 hello 환경 전체에 제어를 이전 및 이후 로그인 toohello 응용 프로그램에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-134">Control around hello experience of logging in is provided toohello application before and after sign-in.</span></span>

<span data-ttu-id="26df9-135">이러한 로그인 있어야 hello 다음 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-135">These logins have hello following drawbacks:</span></span>

* <span data-ttu-id="26df9-136">사용자는 Microsoft ID를 사용하는 모든 앱이 아닌 응용 프로그램이 구성한 해당 Microsoft ID 간에서만 Single Sign-On을 경험할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="26df9-137">응용 프로그램을 사용 하 여 hello InTune 제품군 또는 조건부 액세스 등의 고급 비즈니스 기능으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-137">Your application cannot be used with more advanced business features such as Conditional Access or use hello InTune suite of products.</span></span>
* <span data-ttu-id="26df9-138">응용 프로그램은 비즈니스 사용자에 대한 인증서 기반 인증을 지원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="26df9-139">Microsoft Identity Sdk hello 프로그램 응용 프로그램 tooenable SSO의 hello 공유 저장소에서 작동 하는 방법에 대 한 표현을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-139">Here is a representation of how hello Microsoft Identity SDKs work with hello shared storage of your applications tooenable SSO:</span></span>

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| ADAL SDK  |  |  ADAL SDK  |  |  ADAK SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a><span data-ttu-id="26df9-140">브로커 지원 로그인</span><span class="sxs-lookup"><span data-stu-id="26df9-140">Broker assisted logins</span></span>
<span data-ttu-id="26df9-141">Broker 기반 로그인에는 hello 저장 및 hello 브로커 tooshare 자격 증명의 보안을 사용 하 여 hello Microsoft Id 플랫폼을 적용 하는 hello 장치에서 모든 응용 프로그램 사이의 hello broker 응용 프로그램 내에서 발생 하는 로그인 환경이 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-141">Broker-assisted logins are login experiences that occur within hello broker application and use hello storage and security of hello broker tooshare credentials across all applications on hello device that apply hello Microsoft Identity platform.</span></span> <span data-ttu-id="26df9-142">이 응용 프로그램의 hello 브로커 toosign 사용자가 사용 한다는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-142">This means that your applications rely on hello broker toosign users in.</span></span> <span data-ttu-id="26df9-143">IOS 및 Android에서 이러한 브로커는 고객에 독립적으로 설치 하거나 해당 사용자에 대 한 hello 장치를 관리 하는 회사에서 장치 toohello 푸시할 수는 다운로드 가능한 응용 프로그램을 통해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed toohello device by a company who manages hello device for their user.</span></span> <span data-ttu-id="26df9-144">이러한 유형의 응용 프로그램의 예는 iOS에서 hello Microsoft Authenticator 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-144">An example of this type of application is hello Microsoft Authenticator application on iOS.</span></span> <span data-ttu-id="26df9-145">Windows 웹 인증 브로커 hello 라고 기술적으로 toohello 운영 체제에서 기본적으로 제공 하는 계정 선택 하 여이 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-145">In Windows this functionality is provided by an account chooser built in toohello operating system, known technically as hello Web Authentication Broker.</span></span>
<span data-ttu-id="26df9-146">hello 경험 플랫폼에 따라 다르며 하며 중단 toousers 수 되지 않은 경우 올바르게 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-146">hello experience varies by platform and can sometimes be disruptive toousers if not managed correctly.</span></span> <span data-ttu-id="26df9-147">익숙한 아마도 가장이 패턴 hello Facebook 응용 프로그램이 설치 된 다른 응용 프로그램에서 Facebook Connect를 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="26df9-147">You're probably most familiar with this pattern if you have hello Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="26df9-148">hello Microsoft Identity 플랫폼 사용 하 여 hello 같은 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-148">hello Microsoft Identity platform uses hello same pattern.</span></span>

<span data-ttu-id="26df9-149">IOS에 대 한이 인해 tooa "전환" 애니메이션 전송 대상에 응용 프로그램 toohello 백그라운드 hello Microsoft Authenticator 응용 프로그램 사용자 tooselect hello에 대 한 toohello 전경 제공 사용한 toosign 만족할 만한 계정.</span><span class="sxs-lookup"><span data-stu-id="26df9-149">For iOS this leads tooa "transition" animation where your application is sent toohello background while hello Microsoft Authenticator applications comes toohello foreground for hello user tooselect which account they would like toosign in with.</span></span>  

<span data-ttu-id="26df9-150">Android 및 Windows hello 계정에 대 한 선택은 덜 중단 toohello 사용자는 응용 프로그램 맨 위에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-150">For Android and Windows hello account chooser is displayed on top of your application which is less disruptive toohello user.</span></span>

#### <a name="how-hello-broker-gets-invoked"></a><span data-ttu-id="26df9-151">Hello broker가 호출 하는 방법</span><span class="sxs-lookup"><span data-stu-id="26df9-151">How hello broker gets invoked</span></span>
<span data-ttu-id="26df9-152">호환 되는 broker hello Microsoft Authenticator 응용 프로그램, Microsoft Identity Sdk hello가 자동으로 같은 hello 장치가에 설치 된 경우에 사용자 toolog에서 모든 계정을 사용 하 여 만들려는 되었음을 나타낼 때 사용자에 대 한 hello 브로커 호출 작업 hello 수행 hello Microsoft Identity 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-152">If a compatible broker is installed on hello device, like hello Microsoft Authenticator application, hello Microsoft Identity SDKs will automatically do hello work of invoking hello broker for you when a user indicates they wish toolog in using any account from hello Microsoft Identity platform.</span></span> <span data-ttu-id="26df9-153">이 계정은 개인 Microsoft 계정, 회사 또는 학교 계정 또는 B2C 및 B2B 제품을 사용하여 Azure에 제공 및 호스트하는 계정일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 

 #### <a name="how-we-ensure-hello-application-is-valid"></a><span data-ttu-id="26df9-154">올바른지 hello 응용 프로그램 인지 확인 하는 방법</span><span class="sxs-lookup"><span data-stu-id="26df9-154">How we ensure hello application is valid</span></span>
 
 <span data-ttu-id="26df9-155">응용 프로그램 호출 hello 브로커 hello 필요 tooensure hello id가 중요 한 toohello 보안에서 지원 되는 broker 로그인을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-155">hello need tooensure hello identity of an application call hello broker is crucial toohello security we provide in broker assisted logins.</span></span> <span data-ttu-id="26df9-156">IOS 나 Android 악성 응용 프로그램이 "스푸핑"는 올바른 응용 프로그램의 식별자를 업데이트 하 고 hello 합법적인 응용 프로그램을 위한 hello 토큰을 수신할 수 있습니다 하므로 지정된 된 응용 프로그램에 대해서만 사용할 수 있는 고유 식별자를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive hello tokens meant for hello legitimate application.</span></span> <span data-ttu-id="26df9-157">런타임 시 hello 오른쪽 응용 프로그램과 알립니다 항상 tooensure, 반드시 hello 개발자 tooprovide 사용자 지정 redirectURI Microsoft와 응용 프로그램을 등록할 때 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-157">tooensure we are always communicating with hello right application at runtime, we ask hello developer tooprovide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="26df9-158">**개발자가 이 리디렉션 URI를 만드는 방법은 아래에 자세히 설명되어 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="26df9-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="26df9-159">이 사용자 지정 redirectURI hello hello 응용 프로그램의 번들 ID가 포함 되어 및 hello Apple 앱 스토어에 의해 toobe 고유 toohello 응용 프로그램을 보장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-159">This custom redirectURI contains hello Bundle ID of hello application and is ensured toobe unique toohello application by hello Apple App Store.</span></span> <span data-ttu-id="26df9-160">응용 프로그램 호출 hello 브로커 hello 브로커 hello iOS를 요청할 때 사용 하 여 번들 ID를 호출한 hello 브로커를 hello 시스템 tooprovide 운영 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-160">When an application calls hello broker, hello broker asks hello iOS operating system tooprovide it with hello Bundle ID that called hello broker.</span></span> <span data-ttu-id="26df9-161">이 번들 ID tooMicrosoft hello 호출 tooour id 시스템에서 제공 하는 hello broker 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-161">hello broker provides this Bundle ID tooMicrosoft in hello call tooour identity system.</span></span> <span data-ttu-id="26df9-162">Hello hello 응용 프로그램의 번들 ID에 등록 하는 동안 번들 ID가 toous hello 개발자가 제공 하는 hello와 일치 하지 않으면, 우리에서 액세스를 거부할 toohello 토큰 hello 리소스 hello 응용 프로그램이 요청에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-162">If hello Bundle ID of hello application does not match hello Bundle ID provided toous by hello developer during registration, we will deny access toohello tokens for hello resource hello application is requesting.</span></span> <span data-ttu-id="26df9-163">이 검사는 hello 개발자가 등록 된 hello 응용 프로그램이 토큰 수신 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-163">This check ensures that only hello application registered by hello developer receives tokens.</span></span>

<span data-ttu-id="26df9-164">**hello 개발자는 Microsoft Identity SDK hello hello 브로커를 호출 하거나 hello 비 브로커 보조 흐름을 사용 하는 경우 hello 선택을 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="26df9-164">**hello developer has hello choice of if hello Microsoft Identity SDK calls hello broker or uses hello non-broker assisted flow.**</span></span> <span data-ttu-id="26df9-165">그러나 하지 toouse hello 브로커 기반 흐름을 선택 하는 hello 개발자의 경우 이러한 hello의 이점을 잃게 SSO 자격 증명을 사용 하 여 해당 hello 사용자 hello 장치에 이미 추가한 수 없고을 Microsoft 비즈니스 기능과 함께 사용 하는 응용 프로그램 조건부 액세스, Intune 관리 기능 및 인증서 기반 인증 같은 고객을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-165">However if hello developer chooses not toouse hello broker-assisted flow they lose hello benefit of using SSO credentials that hello user may have already added on hello device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="26df9-166">이러한 로그인 hello 이점을 뒤에</span><span class="sxs-lookup"><span data-stu-id="26df9-166">These logins have hello following benefits:</span></span>

* <span data-ttu-id="26df9-167">Hello 공급 업체에 관계 없이 자신의 모든 응용 프로그램에 SSO를 경험 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-167">User experiences SSO across all their applications no matter hello vendor.</span></span>
* <span data-ttu-id="26df9-168">응용 프로그램 조건부 액세스 등의 고급 비즈니스 기능을 사용 하거나 제품 hello InTune 그룹을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-168">Your application can use more advanced business features such as Conditional Access or use hello InTune suite of products.</span></span>
* <span data-ttu-id="26df9-169">응용 프로그램은 비즈니스 사용자에 대한 인증서 기반 인증을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="26df9-170">훨씬 더 안전한 로그인 환경의 hello broker 응용 프로그램 추가 보안 알고리즘 및 암호화가 hello hello 응용 프로그램 및 hello 사용자 신원을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-170">Much more secure sign-in experience as hello identity of hello application and hello user are verified by hello broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="26df9-171">이러한 로그인 있어야 hello 다음 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-171">These logins have hello following drawbacks:</span></span>

* <span data-ttu-id="26df9-172">IOS에서 hello 사용자 자격 증명을 선택 하는 동안 응용 프로그램의 환경이 전환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-172">In iOS hello user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="26df9-173">응용 프로그램 내에서 고객에 대 한 hello 기능 toomanage hello 로그인의 손실 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-173">Loss of hello ability toomanage hello login experience for your customers within your application.</span></span>

<span data-ttu-id="26df9-174">Hello Microsoft Identity Sdk 작업 hello로 응용 프로그램 tooenable SSO broker 하는 방법에 대 한 표현을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-174">Here is a representation of how hello Microsoft Identity SDKs work with hello broker applications tooenable SSO:</span></span>

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
| Azure SDK  | | Azure SDK  |   | Azure SDK   |
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

<span data-ttu-id="26df9-175">이 배경 정보를 갖춘 있어야 수 toobetter 이해 하 고 hello Microsoft Id 플랫폼 및 Sdk를 사용 하 여 응용 프로그램 내에서 SSO를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-175">Armed with this background information you should be able toobetter understand and implement SSO within your application using hello Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="26df9-176">ADAL을 사용하여 앱 간 SSO 활성화</span><span class="sxs-lookup"><span data-stu-id="26df9-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="26df9-177">Hello ADAL iOS SDK 사용 여기에:</span><span class="sxs-lookup"><span data-stu-id="26df9-177">Here we use hello ADAL iOS SDK to:</span></span>

* <span data-ttu-id="26df9-178">앱 제품군에 대한 비 브로커 지원 SSO 설정</span><span class="sxs-lookup"><span data-stu-id="26df9-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="26df9-179">브로커 지원 SSO에 대한 지원 설정</span><span class="sxs-lookup"><span data-stu-id="26df9-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="26df9-180">비 브로커 지원 SSO에 대한 SSO 설정</span><span class="sxs-lookup"><span data-stu-id="26df9-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="26df9-181">비 브로커 보조 SSO 응용 프로그램 전반에 대 한 Microsoft Identity Sdk hello SSO의 hello 복잡성 많이를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-181">For non-broker assisted SSO across applications hello Microsoft Identity SDKs manage much of hello complexity of SSO for you.</span></span> <span data-ttu-id="26df9-182">Hello 캐시에 hello 올바른 사용자를 찾아서 tooquery 있습니다에 대 한 로그인된 사용자의 목록을 유지 관리 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-182">This includes finding hello right user in hello cache and maintaining a list of logged in users for you tooquery.</span></span>

<span data-ttu-id="26df9-183">다음 toodo hello 필요를 소유 하는 응용 프로그램 전체에서 SSO tooenable:</span><span class="sxs-lookup"><span data-stu-id="26df9-183">tooenable SSO across applications you own you need toodo hello following:</span></span>

1. <span data-ttu-id="26df9-184">모든 사용자 응용 프로그램 사용자 hello 같은 클라이언트 ID 또는 id입니다. 응용 프로그램 확인</span><span class="sxs-lookup"><span data-stu-id="26df9-184">Ensure all your applications user hello same Client ID or Application ID.</span></span>
2. <span data-ttu-id="26df9-185">모든 키 집합을 공유할 수 있도록 Apple에서 인증서 같은 서명 하 여 응용 프로그램 공유 hello 확인</span><span class="sxs-lookup"><span data-stu-id="26df9-185">Ensure that all of your applications share hello same signing certificate from Apple so that you can share keychains</span></span>
3. <span data-ttu-id="26df9-186">요청 각 응용 프로그램에 대 한 동일한 키 집합 자격 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-186">Request hello same keychain entitlement for each of your applications.</span></span>
4. <span data-ttu-id="26df9-187">Microsoft Identity Sdk hello에 대 한 hello 공유 키 집합 toouse 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-187">Tell hello Microsoft Identity SDKs about hello shared keychain you want us toouse.</span></span>

#### <a name="using-hello-same-client-id--application-id-for-all-hello-applications-in-your-suite-of-apps"></a><span data-ttu-id="26df9-188">동일한 클라이언트 ID를 hello를 사용 하 여 / 응용 프로그램의 응용 프로그램 도구 모음에 모든 hello에 대 한 응용 프로그램 ID</span><span class="sxs-lookup"><span data-stu-id="26df9-188">Using hello same Client ID / Application ID for all hello applications in your suite of apps</span></span>
<span data-ttu-id="26df9-189">Microsoft Identity 플랫폼 tooknow hello에 대 한 응용 프로그램에서 tooshare 토큰 수 있는지, 각 응용 프로그램이 있어야 tooshare hello 같은 클라이언트 ID 또는 응용 프로그램 id입니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-189">In order for hello Microsoft Identity platform tooknow that it's allowed tooshare tokens across your applications, each of your applications will need tooshare hello same Client ID or Application ID.</span></span> <span data-ttu-id="26df9-190">Hello 포털에서 첫 번째 응용 프로그램을 등록할 때 tooyou 제공한 hello 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-190">This is hello unique identifier that was provided tooyou when you registered your first application in hello portal.</span></span>

<span data-ttu-id="26df9-191">다양 한 앱 식별 하는 방법 할까요 toohello Microsoft Id 서비스를 사용 하는 경우 hello 동일한 응용 프로그램 id입니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-191">You may be wondering how you will identify different apps toohello Microsoft Identity service if it uses hello same Application ID.</span></span> <span data-ttu-id="26df9-192">hello 대답이 hello로 **리디렉션 Uri**합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-192">hello answer is with hello **Redirect URIs**.</span></span> <span data-ttu-id="26df9-193">각 응용 프로그램에는 hello 등록 포털에 등록 한 리디렉션 Uri 여러 개 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-193">Each application can have multiple Redirect URIs registered in hello onboarding portal.</span></span> <span data-ttu-id="26df9-194">제품의 각 앱은 다른 리디렉션 URI를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-194">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="26df9-195">표시되는 모양의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-195">An example of how this looks is below:</span></span>

<span data-ttu-id="26df9-196">App1 리디렉션 URI: `x-msauth-mytestiosapp://com.myapp.mytestapp`</span><span class="sxs-lookup"><span data-stu-id="26df9-196">App1 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp`</span></span>

<span data-ttu-id="26df9-197">App2 리디렉션 URI: `x-msauth-mytestiosapp://com.myapp.mytestapp2`</span><span class="sxs-lookup"><span data-stu-id="26df9-197">App2 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp2`</span></span>

<span data-ttu-id="26df9-198">App3 리디렉션 URI: `x-msauth-mytestiosapp://com.myapp.mytestapp3`</span><span class="sxs-lookup"><span data-stu-id="26df9-198">App3 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp3`</span></span>

<span data-ttu-id="26df9-199">....</span><span class="sxs-lookup"><span data-stu-id="26df9-199">....</span></span>

<span data-ttu-id="26df9-200">아래에 중첩 된 이러한 동일한 클라이언트 ID를 hello / 응용 프로그램 ID 및 조회에 따라 hello에 대 한 리디렉션 URI SDK 구성에서 toous을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-200">These are nested under hello same client ID / application ID and looked up based on hello redirect URI you return toous in your SDK configuration.</span></span>

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


<span data-ttu-id="26df9-201">*이러한 리디렉션 Uri의 형식은 hello는 아래 설명 되어 있습니다. 이 경우 이러한 해야 다음과 같은 hello 위의 toosupport hello broker 싶지 않다면 모든 리디렉션 URI를 사용할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="26df9-201">*Note that hello format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish toosupport hello broker, in which case they must look something like hello above*</span></span>

#### <a name="create-keychain-sharing-between-applications"></a><span data-ttu-id="26df9-202">응용 프로그램 간에 공유되는 키 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="26df9-202">Create keychain sharing between applications</span></span>
<span data-ttu-id="26df9-203">이 문서의 hello 범위를 벗어납니다 키 집합 공유를 사용 하 고 Apple에서 해당 문서에 포함 [기능 추가](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-203">Enabling keychain sharing is beyond hello scope of this document and covered by Apple in their document [Adding Capabilities](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html).</span></span> <span data-ttu-id="26df9-204">중요 한 것은 호출 하 여 키 집합 toobe 원하는 결정 하 고 모든 응용 프로그램에서 해당 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-204">What is important is that you decide what you want your keychain toobe called and add that capability across all your applications.</span></span>

<span data-ttu-id="26df9-205">설정 제대로 권리가 부여 받은 프로젝트 디렉터리에 파일 나타나야 않은 경우 `entitlements.plist` hello 다음 처럼 보이는 항목을 포함 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-205">When you do have entitlements set up correctly you should see a file in your project directory entitled `entitlements.plist` that contains something that looks like hello following:</span></span>

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>keychain-access-groups</key>
    <array>
        <string>$(AppIdentifierPrefix)com.myapp.mytestapp</string>
        <string>$(AppIdentifierPrefix)com.myapp.mycache</string>
    </array>
</dict>
</plist>
```

<span data-ttu-id="26df9-206">각 응용 프로그램에서 사용 하도록 설정 하는 hello 키 집합 자격 있고 준비 toouse SSO는 후 Microsoft Identity SDK hello에 대 한 키 체인 설정에 따라 hello를 사용 하 여 프로그램 `ADAuthenticationSettings` 설정은 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="26df9-206">Once you have hello keychain entitlement enabled in each of your applications, and you are ready toouse SSO, tell hello Microsoft Identity SDK about your keychain by using hello following setting in your `ADAuthenticationSettings` with hello following setting:</span></span>

```
defaultKeychainSharingGroup=@"com.myapp.mycache";
```

> [!WARNING]
> <span data-ttu-id="26df9-207">응용 프로그램에서 키 집합을 공유 하는 경우 모든 응용 프로그램 사용자를 삭제 하거나 나빠지는 지 응용 프로그램에서 모든 hello 토큰을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-207">When you share a keychain across your applications any application can delete users or worse delete all hello tokens across your application.</span></span> <span data-ttu-id="26df9-208">이 hello 토큰 toodo 백그라운드 작업을 사용 하는 응용 프로그램의 경우에 특히 재해로입니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-208">This is particularly disastrous if you have applications that rely on hello tokens toodo background work.</span></span> <span data-ttu-id="26df9-209">모든에 특히 주의 이어야 한다는 의미는 키 집합 공유 hello Microsoft Identity Sdk를 통해 작업을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-209">Sharing a keychain means that you must be very careful in any and all remove operations through hello Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="26df9-210">이것으로 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-210">That's it!</span></span> <span data-ttu-id="26df9-211">이제 Microsoft Identity SDK hello 응용 프로그램에서 자격 증명을 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-211">hello Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="26df9-212">hello 사용자 목록도 응용 프로그램 인스턴스 간에 공유 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-212">hello user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="26df9-213">브로커 지원 SSO에 대한 SSO 설정</span><span class="sxs-lookup"><span data-stu-id="26df9-213">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="26df9-214">응용 프로그램 toouse hello 장치에 설치 되어 있는 모든 broker에 대 한 기능 hello **기본적으로 해제 되어**합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-214">hello ability for an application toouse any broker that is installed on hello device is **turned off by default**.</span></span> <span data-ttu-id="26df9-215">순서로 toouse 응용 프로그램 hello 브로커와 몇 가지 추가 구성을 변경 하 고 일부 코드 tooyour 응용 프로그램을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-215">In order toouse your application with hello broker you must do some additional configuration and add some code tooyour application.</span></span>

<span data-ttu-id="26df9-216">hello 단계 toofollow가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-216">hello steps toofollow are:</span></span>

1. <span data-ttu-id="26df9-217">응용 프로그램 코드의 호출 toohello MS SDK에서에서 broker 모드를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-217">Enable broker mode in your application code's call toohello MS SDK.</span></span>
2. <span data-ttu-id="26df9-218">새 리디렉션 URI를 해당 tooboth hello 앱 및 앱 등록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-218">Establish a new redirect URI and provide that tooboth hello app and your app registration.</span></span>
3. <span data-ttu-id="26df9-219">URL 구성표 등록.</span><span class="sxs-lookup"><span data-stu-id="26df9-219">Registering a URL Scheme.</span></span>
4. <span data-ttu-id="26df9-220">iOS9 지원: 권한 tooyour info.plist 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-220">iOS9 Support: Add a permission tooyour info.plist file.</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="26df9-221">1단계: 응용 프로그램에서 브로커 모드 활성화</span><span class="sxs-lookup"><span data-stu-id="26df9-221">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="26df9-222">"hello"컨텍스트 또는 인증 개체의 초기 설정을 만들 때 응용 프로그램 toouse hello broker 프로그램에 대 한 hello 기능이 켜 집니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-222">hello ability for your application toouse hello broker is turned on when you create hello "context" or initial setup of your Authentication object.</span></span> <span data-ttu-id="26df9-223">코드에서 자격 증명 형식을 설정하여 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-223">You do this by setting your credentials type in your code:</span></span>

```
/*! See hello ADCredentialsType enumeration definition for details */
@propertyADCredentialsType credentialsType;
```
<span data-ttu-id="26df9-224">hello `AD_CREDENTIALS_AUTO` 설정을 사용 하면 toohello 브로커 아웃 hello Microsoft Identity SDK tootry toocall `AD_CREDENTIALS_EMBEDDED` hello Microsoft Identity SDK에서 toohello 브로커 호출 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-224">hello `AD_CREDENTIALS_AUTO` setting will allow hello Microsoft Identity SDK tootry toocall out toohello broker, `AD_CREDENTIALS_EMBEDDED` will prevent hello Microsoft Identity SDK from calling toohello broker.</span></span>

#### <a name="step-2-registering-a-url-scheme"></a><span data-ttu-id="26df9-225">2단계: URL 구성표 등록</span><span class="sxs-lookup"><span data-stu-id="26df9-225">Step 2: Registering a URL Scheme</span></span>
<span data-ttu-id="26df9-226">hello Microsoft Identity 플랫폼 Url tooinvoke hello 브로커와 다음 반환 컨트롤 뒤로 tooyour 응용 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-226">hello Microsoft Identity platform uses URLs tooinvoke hello broker and then return control back tooyour application.</span></span> <span data-ttu-id="26df9-227">toofinish URL 체계 해야 해당 왕복 등록 응용 프로그램에 대 한 해당 hello Microsoft Identity 플랫폼에 대 한 알게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-227">toofinish that round trip you need a URL scheme registered for your application that hello Microsoft Identity platform will know about.</span></span> <span data-ttu-id="26df9-228">이 수 또한 tooany 기타 응용 프로그램 스키마의 응용 프로그램에 이전에 등록 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-228">This can be in addition tooany other app schemes you may have previously registered with your application.</span></span>

> [!WARNING]
> <span data-ttu-id="26df9-229">Hello hello를 사용 하 여 다른 앱의 URL 구성표 상당히 고유 toominimize hello 가능성을 만드는 것이 좋습니다 동일한 URL 구성표입니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-229">We recommend making hello URL scheme fairly unique toominimize hello chances of another app using hello same URL scheme.</span></span> <span data-ttu-id="26df9-230">Apple는 hello 앱 스토어에 등록 된 URL 스키마의 hello 고유성을 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-230">Apple does not enforce hello uniqueness of URL schemes that are registered in hello app store.</span></span>
> 
> 

<span data-ttu-id="26df9-231">다음은 프로젝트 구성에 나타나는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-231">Below is an example of how this appears in your project configuration.</span></span> <span data-ttu-id="26df9-232">또한 XCode에서도 이를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-232">You may also do this in XCode as well:</span></span>

```
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>com.myapp.mytestapp</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>x-msauth-mytestiosapp</string>
        </array>
    </dict>
</array>
```

#### <a name="step-3-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="26df9-233">3단계: URL 구성표와 함께 새 리디렉션 URI 설정</span><span class="sxs-lookup"><span data-stu-id="26df9-233">Step 3: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="26df9-234">에 항상 반환 hello 자격 증명 토큰 toohello 올바른 응용 프로그램 순서 tooensure, toomake म 콜백할 tooyour 응용 프로그램 iOS 운영 체제 hello 하는 방식으로 확인할 수 있는지 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-234">In order tooensure that we always return hello credential tokens toohello correct application, we need toomake sure we call back tooyour application in a way that hello iOS operating system can verify.</span></span> <span data-ttu-id="26df9-235">hello iOS 운영 체제 보고서 toohello Microsoft broker 응용 프로그램 hello 메서드를 호출 하는 hello 응용 프로그램의 번들 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-235">hello iOS operating system reports toohello Microsoft broker applications hello Bundle ID of hello application calling it.</span></span> <span data-ttu-id="26df9-236">불량 응용 프로그램에서 이를 스푸핑할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-236">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="26df9-237">따라서 활용 하 여이 hello hello 토큰 toohello 올바른 응용 프로그램으로 반환 됨 우리의 broker 응용 프로그램 tooensure의 URI와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-237">Therefore, we leverage this along with hello URI of our broker application tooensure that hello tokens are returned toohello correct application.</span></span> <span data-ttu-id="26df9-238">필요 하면 tooestablish이 고유 리디렉션 URI를 모두 설정 하 여 응용 프로그램에서 리디렉션 URI로 우리의 개발자 포털에서.</span><span class="sxs-lookup"><span data-stu-id="26df9-238">We require you tooestablish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="26df9-239">Hello 적절 한 형태의 사용자 리디렉션 URI 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-239">Your redirect URI must be in hello proper form of:</span></span>

`<app-scheme>://<your.bundle.id>`

<span data-ttu-id="26df9-240">예: *x-msauth-mytestiosapp://com.myapp.mytestapp*</span><span class="sxs-lookup"><span data-stu-id="26df9-240">ex: *x-msauth-mytestiosapp://com.myapp.mytestapp*</span></span>

<span data-ttu-id="26df9-241">이 리디렉션 URI toobe hello를 사용 하 여 응용 프로그램 등록에 지정 된 필요한 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-241">This Redirect URI needs toobe specified in your app registration using hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="26df9-242">Azure AD 앱 등록에 대한 자세한 내용은 [Azure Active Directory와 통합](active-directory-how-to-integrate.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26df9-242">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

##### <a name="step-3a-add-a-redirect-uri-in-your-app-and-dev-portal-toosupport-certificate-based-authentication"></a><span data-ttu-id="26df9-243">3a 단계: 응용 프로그램 및 개발자 포털 toosupport 인증서 기반 인증의 리디렉션 URI 추가</span><span class="sxs-lookup"><span data-stu-id="26df9-243">Step 3a: Add a redirect URI in your app and dev portal toosupport certificate based authentication</span></span>
<span data-ttu-id="26df9-244">두 번째 "msauth" toosupport 인증서 기반 인증에 응용 프로그램 및 hello 등록 toobe 필요 [Azure 포털](https://portal.azure.com/) tooadd 원할 경우 toohandle 인증서 인증을 지 원하는 응용 프로그램에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-244">toosupport cert based authentication a second "msauth"  needs toobe registered in your application and hello [Azure portal](https://portal.azure.com/) toohandle certificate authentication if you wish tooadd that support in your application.</span></span>

`msauth://code/<broker-redirect-uri-in-url-encoded-form>`

<span data-ttu-id="26df9-245">예: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span><span class="sxs-lookup"><span data-stu-id="26df9-245">ex: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span></span>

#### <a name="step-4-ios9-add-a-configuration-parameter-tooyour-app"></a><span data-ttu-id="26df9-246">4 단계: iOS9: 구성 매개 변수 tooyour 앱 추가</span><span class="sxs-lookup"><span data-stu-id="26df9-246">Step 4: iOS9: Add a configuration parameter tooyour app</span></span>
<span data-ttu-id="26df9-247">ADAL 사용 – canOpenURL: toocheck hello 브로커 hello 장치에 설치 된 경우.</span><span class="sxs-lookup"><span data-stu-id="26df9-247">ADAL uses –canOpenURL: toocheck if hello broker is installed on hello device.</span></span> <span data-ttu-id="26df9-248">iOS 9에서 Apple은 응용 프로그램에서 쿼리할 수 있는 구성표를 잠궜습니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-248">In iOS 9 Apple locked down what schemes an application can query for.</span></span> <span data-ttu-id="26df9-249">tooadd "msauth" toohello LSApplicationQueriesSchemes 섹션 해야 프로그램 `info.plist file`합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-249">You will need tooadd “msauth” toohello LSApplicationQueriesSchemes section of your `info.plist file`.</span></span>

<span data-ttu-id="26df9-250"><key>LSApplicationQueriesSchemes</key></span><span class="sxs-lookup"><span data-stu-id="26df9-250"><key>LSApplicationQueriesSchemes</key></span></span>

<span data-ttu-id="26df9-251"><array><string>msauth</string>
</array></span><span class="sxs-lookup"><span data-stu-id="26df9-251"><array> <string>msauth</string>
</array></span></span>

### <a name="youve-configured-sso"></a><span data-ttu-id="26df9-252">SSO를 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-252">You've configured SSO!</span></span>
<span data-ttu-id="26df9-253">이제 Microsoft Identity SDK hello에서는 자동으로 응용 프로그램에서 자격 증명을 공유를 자신의 장치에 표시 되지 않으면 hello 브로커를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="26df9-253">Now hello Microsoft Identity SDK will automatically both share credentials across your applications and invoke hello broker if it's present on their device.</span></span>

