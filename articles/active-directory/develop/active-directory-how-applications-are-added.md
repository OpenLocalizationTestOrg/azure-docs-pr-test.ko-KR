---
title: "Azure Active Directory에 응용 프로그램을 추가하는 방법입니다."
description: "이 문서에서는 Azure Active Directory의 인스턴스에 응용 프로그램을 추가하는 방법을 설명합니다."
services: active-directory
documentationcenter: 
author: shoatman
manager: kbrint
editor: 
ms.assetid: 3321d130-f2a8-4e38-b35e-0959693f3576
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/09/2016
ms.author: shoatman
ms.custom: aaddev
ms.openlocfilehash: 6ffcfcb7ed071a12b0b3495ad534fd00f6d6ad99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-and-why-applications-are-added-to-azure-ad"></a><span data-ttu-id="04f9d-103">응용 프로그램을 Azure AD에 추가하는 방법 및 이유</span><span class="sxs-lookup"><span data-stu-id="04f9d-103">How and why applications are added to Azure AD</span></span>
<span data-ttu-id="04f9d-104">Azure Active Directory 인스턴스에서 응용 프로그램 목록을 확인할 때 처음에 어려운 것 중 하나는 응용 프로그램이 어디서 추가되었는지 및 그 이유를 이해하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-104">One of the initially puzzling things when viewing a list of applications in your instance of Azure Active Directory is understanding where the applications came from and why they are there.</span></span>  <span data-ttu-id="04f9d-105">이 문서에서는 응용 프로그램이 디렉터리에 표시되는 방식을 간략하게 설명하고 응용 프로그램이 디렉터리에 추가된 과정을 이해하는 데 도움이 되는 컨텍스트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-105">This article will provide a high level overview of how applications are represented in the directory and provide you with context that will assist you in understanding how an application came to be in your directory.</span></span>

## <a name="what-services-does-azure-ad-provide-to-applications"></a><span data-ttu-id="04f9d-106">응용 프로그램에 제공되는 Azure AD 서비스는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="04f9d-106">What services does Azure AD provide to applications?</span></span>
<span data-ttu-id="04f9d-107">Azure AD에서 제공하는 하나 이상의 서비스를 활용하기 위해 응용 프로그램이 Azure AD에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-107">Applications are added to Azure AD to leverage one or more of the services it provides.</span></span>  <span data-ttu-id="04f9d-108">서비스 포함 사항:</span><span class="sxs-lookup"><span data-stu-id="04f9d-108">Those services include:</span></span>

* <span data-ttu-id="04f9d-109">인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="04f9d-109">App authentication and authorization</span></span>
* <span data-ttu-id="04f9d-110">사용자 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="04f9d-110">User authentication & authorization</span></span>
* <span data-ttu-id="04f9d-111">페더레이션 또는 암호를 사용한 SSO(Single Sign-On)</span><span class="sxs-lookup"><span data-stu-id="04f9d-111">Single sign-on (SSO) using federation or password</span></span>
* <span data-ttu-id="04f9d-112">사용자 프로비전 및 동기화</span><span class="sxs-lookup"><span data-stu-id="04f9d-112">User provisioning & synchronization</span></span>
* <span data-ttu-id="04f9d-113">역할 기반 액세스 제어: 응용 프로그램 역할을 정의하는 디렉터리를 사용하여 응용 프로그램에서 역할 기반 권한 부여 확인을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-113">Role-based access control; Use the directory to define application roles to perform roles based authorization checks in an app.</span></span>
* <span data-ttu-id="04f9d-114">oAuth 인증 서비스(API/리소스에 대한 액세스 권한을 부여는 Microsoft 응용 프로그램 및 Office 365에서 사용하는 서비스)</span><span class="sxs-lookup"><span data-stu-id="04f9d-114">oAuth authorization services (used by Office 365 and other Microsoft apps to authorize access to APIs/resources.)</span></span>
* <span data-ttu-id="04f9d-115">응용 프로그램 게시 및 프록시: 개인 네트워크의 응용 프로그램을 인터넷에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-115">Application publishing & proxy; Publish an app from a private network to the internet</span></span>

## <a name="how-are-applications-represented-in-the-directory"></a><span data-ttu-id="04f9d-116">응용 프로그램이 디렉터리에 어떻게 표시되나요?</span><span class="sxs-lookup"><span data-stu-id="04f9d-116">How are applications represented in the directory?</span></span>
<span data-ttu-id="04f9d-117">응용 프로그램은 Azure AD에서 응용 프로그램 개체와 서비스 주체 개체로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-117">Applications are represented in the Azure AD using 2 objects: an application object and a service principal object.</span></span>  <span data-ttu-id="04f9d-118">"home"/"owner" 또는 "publishing" 디렉터리에 등록된 하나의 응용 프로그램 개체와 응용 프로그램이 동작하는 모든 디렉터리의 응용 프로그램을 나타내는 하나 이상의 서비스 주체 개체가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-118">There is one application object, registered in a "home"/"owner" or "publishing" directory and one or more service principal objects representing the application in every directory in which it acts.</span></span>  

<span data-ttu-id="04f9d-119">응용 프로그램 개체는 Azure AD에 응용 프로그램을 설명하며(다중 테넌트 서비스) 다음을 포함할 수 있습니다(*참고*: 전체 목록은 아님).</span><span class="sxs-lookup"><span data-stu-id="04f9d-119">The application object describes the app to Azure AD (the multi-tenant service) and may include any of the following: (*Note*: This is not an exhaustive list.)</span></span>

* <span data-ttu-id="04f9d-120">이름, 로고, 게시자</span><span class="sxs-lookup"><span data-stu-id="04f9d-120">Name, Logo & Publisher</span></span>
* <span data-ttu-id="04f9d-121">비밀(응용 프로그램을 인증하는 데 사용되는 대칭 및/또는 비대칭 키)</span><span class="sxs-lookup"><span data-stu-id="04f9d-121">Secrets (symmetric and/or asymmetric keys used to authenticate the app)</span></span>
* <span data-ttu-id="04f9d-122">API 종속성(oAuth)</span><span class="sxs-lookup"><span data-stu-id="04f9d-122">API dependencies (oAuth)</span></span>
* <span data-ttu-id="04f9d-123">게시된 API/리소스/범위(oAuth)</span><span class="sxs-lookup"><span data-stu-id="04f9d-123">APIs/resources/scopes published (oAuth)</span></span>
* <span data-ttu-id="04f9d-124">응용 프로그램 역할(RBAC)</span><span class="sxs-lookup"><span data-stu-id="04f9d-124">App roles (RBAC)</span></span>
* <span data-ttu-id="04f9d-125">SSO 메타데이터 및 구성(SSO)</span><span class="sxs-lookup"><span data-stu-id="04f9d-125">SSO metadata and configuration (SSO)</span></span>
* <span data-ttu-id="04f9d-126">사용자 프로비전 메타데이터 및 구성</span><span class="sxs-lookup"><span data-stu-id="04f9d-126">User provisioning metadata and configuration</span></span>
* <span data-ttu-id="04f9d-127">프록시 메타데이터 및 구성</span><span class="sxs-lookup"><span data-stu-id="04f9d-127">Proxy metadata and configuration</span></span>

<span data-ttu-id="04f9d-128">서비스 주체는 홈 디렉터리를 포함하여 응용 프로그램이 동작하는 모든 디렉터리의 응용 프로그램 기록입니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-128">The service principal is a record of the application in every directory, where the application acts including its home directory.</span></span>  <span data-ttu-id="04f9d-129">서비스 주체가 수행하는 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-129">The service principal:</span></span>

* <span data-ttu-id="04f9d-130">응용 프로그램 ID 속성을 통한 응용 프로그램 개체 다시 참조</span><span class="sxs-lookup"><span data-stu-id="04f9d-130">Refers back to an application object via the app id property</span></span>
* <span data-ttu-id="04f9d-131">로컬 사용자 및 그룹 응용 프로그램 역할 할당 기록</span><span class="sxs-lookup"><span data-stu-id="04f9d-131">Records local user and group app-role assignments</span></span>
* <span data-ttu-id="04f9d-132">응용 프로그램에 부여된 로컬 사용자 및 관리자 권한 기록</span><span class="sxs-lookup"><span data-stu-id="04f9d-132">Records local user and admin permissions granted to the app</span></span>
  * <span data-ttu-id="04f9d-133">예: 특정 사용자 메일에 액세스하기 위한 앱 권한</span><span class="sxs-lookup"><span data-stu-id="04f9d-133">For example: permission for the app to access a particular users email</span></span>
* <span data-ttu-id="04f9d-134">조건부 액세스 정책을 포함하여 로컬 정책 기록</span><span class="sxs-lookup"><span data-stu-id="04f9d-134">Records local policies including conditional access policy</span></span>
* <span data-ttu-id="04f9d-135">앱의 대체 로컬 설정 기록</span><span class="sxs-lookup"><span data-stu-id="04f9d-135">Records local alternate local settings for an app</span></span>
  * <span data-ttu-id="04f9d-136">클레임 변환 규칙</span><span class="sxs-lookup"><span data-stu-id="04f9d-136">Claims transformation rules</span></span>
  * <span data-ttu-id="04f9d-137">특성 매핑(사용자 프로비전)</span><span class="sxs-lookup"><span data-stu-id="04f9d-137">Attribute mappings (User provisioning)</span></span>
  * <span data-ttu-id="04f9d-138">테넌트 특정 응용 프로그램 역할(응용 프로그램이 사용자 지정 역할을 지원하는 경우)</span><span class="sxs-lookup"><span data-stu-id="04f9d-138">Tenant specific app roles (if the app supports custom roles)</span></span>
  * <span data-ttu-id="04f9d-139">이름/로고</span><span class="sxs-lookup"><span data-stu-id="04f9d-139">Name/Logo</span></span>

### <a name="a-diagram-of-application-objects-and-service-principals-across-directories"></a><span data-ttu-id="04f9d-140">응용 프로그램 개체 및 서비스 주체 액세스 디렉터리 다이어그램</span><span class="sxs-lookup"><span data-stu-id="04f9d-140">A diagram of application objects and service principals across directories</span></span>
![응용 프로그램 개체와 서비스 주체가 Azure AD 인스턴스와 같이 존재하는 방법을 보여 주는 다이어그램입니다.][apps_service_principals_directory]

<span data-ttu-id="04f9d-142">위의 다이어그램에서 볼 수 있듯이</span><span class="sxs-lookup"><span data-stu-id="04f9d-142">As you can see from the diagram above.</span></span>  <span data-ttu-id="04f9d-143">Microsoft는 두 개의 디렉터리를 내부적으로 유지하며(왼쪽 부분) 응용 프로그램을 게시하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-143">Microsoft maintains two directories internally (on the left) it uses to publish applications.</span></span>

* <span data-ttu-id="04f9d-144">Microsoft 응용 프로그램용 디렉터리(Microsoft 서비스 디렉터리)</span><span class="sxs-lookup"><span data-stu-id="04f9d-144">One for Microsoft Apps (Microsoft services directory)</span></span>
* <span data-ttu-id="04f9d-145">사전 통합된 타사 응용 프로그램용 디렉터리(응용 프로그램 갤러리 디렉터리)</span><span class="sxs-lookup"><span data-stu-id="04f9d-145">One for pre-integrated 3rd Party Apps (App Gallery directory)</span></span>

<span data-ttu-id="04f9d-146">Azure AD와 통합하는 응용 프로그램 게시자/공급업체에는 게시 디렉터리가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-146">Application publishers/vendors who integrate with Azure AD are required to have a publishing directory.</span></span>  <span data-ttu-id="04f9d-147">(일부 SAAS 디렉터리)</span><span class="sxs-lookup"><span data-stu-id="04f9d-147">(Some SAAS Directory).</span></span>

<span data-ttu-id="04f9d-148">직접 추가하는 응용 프로그램은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-148">Applications that you add yourself include:</span></span>

* <span data-ttu-id="04f9d-149">직접 개발한 응용 프로그램(AAD와 통합됨)</span><span class="sxs-lookup"><span data-stu-id="04f9d-149">Apps you developed (integrated with AAD)</span></span>
* <span data-ttu-id="04f9d-150">Single-Sign-On용으로 연결된 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="04f9d-150">Apps you connected for single-sign-on</span></span>
* <span data-ttu-id="04f9d-151">Azure AD 응용 프로그램 프록시를 사용하여 게시된 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="04f9d-151">Apps you published using the Azure AD application proxy.</span></span>

### <a name="a-couple-of-notes-and-exceptions"></a><span data-ttu-id="04f9d-152">일부 참고 및 예외 사항</span><span class="sxs-lookup"><span data-stu-id="04f9d-152">A couple of notes and exceptions</span></span>
* <span data-ttu-id="04f9d-153">일부 서비스 주체만 응용 프로그램 개체를 다시 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-153">Not all service principals point back to application objects.</span></span>  <span data-ttu-id="04f9d-154">그렇죠?</span><span class="sxs-lookup"><span data-stu-id="04f9d-154">Huh?</span></span> <span data-ttu-id="04f9d-155">Azure AD가 처음 빌드되었을 때 응용 프로그램에 제공된 서비스는 훨씬 제한적이었으며 서비스 주체로 충분히 응용 프로그램 ID를 설정할 수 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-155">When Azure AD was originally built the services provided to applications were much more limited and the service principal was sufficient for establishing an app identity.</span></span>  <span data-ttu-id="04f9d-156">원래 서비스 주체는 Windows Server Active Directory 서비스 계정의 형태에 더 가까웠습니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-156">The original service principal was closer in shape to the Windows Server Active Directory service account.</span></span>  <span data-ttu-id="04f9d-157">이러한 이유로 먼저 응용 프로그램 개체를 만들지 않고도 Azure AD PowerShell을 사용하여 서비스 주체를 만들 수 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-157">For this reason it's still possible to create service principals using the Azure AD PowerShell without first creating an application object.</span></span>  <span data-ttu-id="04f9d-158">Graph API는 응용 프로그램 개체가 있어야 서비스 주체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-158">The Graph API requires an app object before creating a service principal.</span></span>
* <span data-ttu-id="04f9d-159">위에서 설명한 정보 중 일부만 프로그래밍 방식으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-159">Not all of the information described above is currently exposed programmatically.</span></span>  <span data-ttu-id="04f9d-160">다음은 UI에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-160">The following are only available in the UI:</span></span>
  * <span data-ttu-id="04f9d-161">클레임 변환 규칙</span><span class="sxs-lookup"><span data-stu-id="04f9d-161">Claims transformation rules</span></span>
  * <span data-ttu-id="04f9d-162">특성 매핑(사용자 프로비전)</span><span class="sxs-lookup"><span data-stu-id="04f9d-162">Attribute mappings (User provisioning)</span></span>
* <span data-ttu-id="04f9d-163">서비스 주체 및 응용 프로그램 개체에 대한 자세한 내용은 Azure AD Graph REST API 참조 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04f9d-163">For more detailed information on the service principal and application objects please refer to the Azure AD Graph REST API reference documentation.</span></span>  <span data-ttu-id="04f9d-164">*힌트*: The Azure AD Graph API 설명서는 현재 사용할 수 있는 Azure AD의 스키마 참조에 가깝습니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-164">*Hint*: The Azure AD Graph API documentation is the closest thing to a schema reference for Azure AD that's currently available.</span></span>  
  * [<span data-ttu-id="04f9d-165">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="04f9d-165">Application</span></span>](https://msdn.microsoft.com/library/azure/dn151677.aspx)
  * [<span data-ttu-id="04f9d-166">서비스 주체</span><span class="sxs-lookup"><span data-stu-id="04f9d-166">Service Principal</span></span>](https://msdn.microsoft.com/library/azure/dn194452.aspx)

## <a name="how-are-apps-added-to-my-azure-ad-instance"></a><span data-ttu-id="04f9d-167">응용 프로그램이 Azure AD 인스턴스에 어떻게 추가되나요?</span><span class="sxs-lookup"><span data-stu-id="04f9d-167">How are apps added to my Azure AD instance?</span></span>
<span data-ttu-id="04f9d-168">다음과 같은 여러 가지 방법으로 응용 프로그램을 Azure AD에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-168">There are many ways an app can be added to Azure AD:</span></span>

* <span data-ttu-id="04f9d-169">[Azure Active Directory 응용 프로그램 갤러리](https://azure.microsoft.com/updates/azure-active-directory-over-1000-apps/)</span><span class="sxs-lookup"><span data-stu-id="04f9d-169">Add an app from the [Azure Active Directory App Gallery](https://azure.microsoft.com/updates/azure-active-directory-over-1000-apps/)</span></span>
* <span data-ttu-id="04f9d-170">Azure Active Directory와 통합된 타사 응용 프로그램에 등록/로그인(예: [Smartsheet](https://app.smartsheet.com/b/home) 또는 [DocuSign](https://www.docusign.net/member/MemberLogin.aspx))</span><span class="sxs-lookup"><span data-stu-id="04f9d-170">Sign up/into a 3rd Party App integrated with Azure Active Directory (For example: [Smartsheet](https://app.smartsheet.com/b/home) or [DocuSign](https://www.docusign.net/member/MemberLogin.aspx))</span></span>
  * <span data-ttu-id="04f9d-171">등록/로그인하는 동안 해당 프로필 및 다른 사용 권한에 액세스하도록 앱에 권한을 부여하라는 메시지가 사용자에게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-171">During sign up/in users are asked to give permission to the app to access their profile and other permissions.</span></span>  <span data-ttu-id="04f9d-172">처음으로 동의하는 사람이 응용 프로그램을 나타내는 서비스 주체를 디렉터리에 추가하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-172">The first person to give consent causes a service principal representing the app to be added to the directory.</span></span>
* <span data-ttu-id="04f9d-173">[Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="04f9d-173">Sign up/into Microsoft online services like [Office 365](http://products.office.com/)</span></span>
  * <span data-ttu-id="04f9d-174">Office 365를 구독하거나 평가판을 시작하면 Office 365와 관련된 모든 기능을 전달하는 데 사용되는 다양한 서비스를 나타내는 디렉터리에 하나 이상의 서비스 주체가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-174">When you subscribe to Office 365 or begin a trial one or more service principals are created in the directory representing the various services that are used to deliver all of the functionality associated with Office 365.</span></span>
  * <span data-ttu-id="04f9d-175">SharePoint와 같은 일부 Office 365 서비스는 워크플로 등 구성 요소 간의 보안 통신을 허용하도록 지속적으로 서비스 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-175">Some Office 365 services like SharePoint create service principals on an on-going basis to allow secure communication between components including workflows.</span></span>
* <span data-ttu-id="04f9d-176">Azure 관리 포털에서 개발 중인 응용 프로그램 추가. 참조: https://msdn.microsoft.com/library/azure/dn132599.aspx</span><span class="sxs-lookup"><span data-stu-id="04f9d-176">Add an app you're developing in the Azure Management Portal see: https://msdn.microsoft.com/library/azure/dn132599.aspx</span></span>
* <span data-ttu-id="04f9d-177">Visual Studio를 사용하여 개발 중인 응용 프로그램 추가. 참조:</span><span class="sxs-lookup"><span data-stu-id="04f9d-177">Add an app you're developing using Visual Studio see:</span></span>
  * [<span data-ttu-id="04f9d-178">ASP.Net 인증 방법</span><span class="sxs-lookup"><span data-stu-id="04f9d-178">ASP.Net Authentication Methods</span></span>](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions)
  * [<span data-ttu-id="04f9d-179">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="04f9d-179">Connected Services</span></span>](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx)
* <span data-ttu-id="04f9d-180">[Azure AD 응용 프로그램 프록시](https://msdn.microsoft.com/library/azure/dn768219.aspx)</span><span class="sxs-lookup"><span data-stu-id="04f9d-180">Add an app to use to use the [Azure AD Application Proxy](https://msdn.microsoft.com/library/azure/dn768219.aspx)</span></span>
* <span data-ttu-id="04f9d-181">SAML 또는 암호 SSO를 사용하여 Single-Sign-On용 응용 프로그램 연결</span><span class="sxs-lookup"><span data-stu-id="04f9d-181">Connect an app for single sign on using SAML or Password SSO</span></span>
* <span data-ttu-id="04f9d-182">Azure의 다양한 개발자 환경 및 개발자 센터의 API 탐색기 환경을 포함한 기타 여러 가지 방법</span><span class="sxs-lookup"><span data-stu-id="04f9d-182">Many others including various developer experiences in Azure and/in API explorer experiences across developer centers</span></span>

## <a name="who-has-permission-to-add-applications-to-my-azure-ad-instance"></a><span data-ttu-id="04f9d-183">응용 프로그램을 Azure AD 인스턴스에 추가할 권한이 있는 사용자는?</span><span class="sxs-lookup"><span data-stu-id="04f9d-183">Who has permission to add applications to my Azure AD instance?</span></span>
<span data-ttu-id="04f9d-184">다음 작업은 전역 관리자만 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-184">Only global administrators can:</span></span>

* <span data-ttu-id="04f9d-185">Azure AD 응용 프로그램 갤러리(사전 통합된 타사 응용 프로그램)에서 앱 추가</span><span class="sxs-lookup"><span data-stu-id="04f9d-185">Add apps from the Azure AD app gallery (pre-integrated 3rd Party Apps)</span></span>
* <span data-ttu-id="04f9d-186">Azure AD 응용 프로그램 프록시를 사용하여 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="04f9d-186">Publish an app using the Azure AD Application Proxy</span></span>

<span data-ttu-id="04f9d-187">디렉터리의 모든 사용자는 개발 중인 응용 프로그램을 추가할 권한 및 조직 데이터를 공유하거나 액세스 권한을 부여할 응용 프로그램을 결정할 권한을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-187">All users in your directory have rights to add applications that they are developing and discretion over which applications they share/give access to their organizational data.</span></span>  <span data-ttu-id="04f9d-188">*사용자가 앱을 등록 및 로그인하고 권한을 부여하면 서비스 주체가 만들어질 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="04f9d-188">*Remember user sign up/in to an app and granting permissions may result in a service principal being created.*</span></span>

<span data-ttu-id="04f9d-189">처음에는 염려스러울 수 있으나 다음을 기억하세요.</span><span class="sxs-lookup"><span data-stu-id="04f9d-189">This might initially sound concerning, but keep the following in mind:</span></span>

* <span data-ttu-id="04f9d-190">응용 프로그램을 디렉터리에 등록/기록하지 않고도 응용 프로그램은 수년간 사용자 인증에 Windows Server Active Directory를 활용해왔습니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-190">Apps have been able to leverage Windows Server Active Directory for user authentication for many years without requiring the application to be registered/recorded in the directory.</span></span>  <span data-ttu-id="04f9d-191">이제 조직에서 디렉터리를 사용하는 응용 프로그램 수 및 용도를 정확하게 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-191">Now the organization will have improved visibility to exactly how many apps are using the directory and what for.</span></span>
* <span data-ttu-id="04f9d-192">관리자 중심 응용 프로그램 게시/등록 프로세스가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-192">No need for admin driven app publishing/registration process.</span></span>  <span data-ttu-id="04f9d-193">Active Directory Federation Services를 사용할 경우 신뢰 당사자로 개발자가 아닌 관리자가 앱을 추가해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-193">With Active Directory Federation Services it was likely that an admin had to add an app as a relying party on behalf of developers.</span></span>  <span data-ttu-id="04f9d-194">이제 개발자가 직접 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-194">Now developers can self-service.</span></span>
* <span data-ttu-id="04f9d-195">비즈니스 목적의 경우 사용자는 조직 계정을 사용하여 응용 프로그램에 로그인/등록하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-195">Users signing in/up to apps using their organization accounts for business purposes is a good thing.</span></span>  <span data-ttu-id="04f9d-196">이후에 사용자가 조직을 떠날 경우 사용하던 응용 프로그램에서 자신의 계정에 액세스할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-196">If they subsequently leave the organization they will lose access to their account in the application they were using.</span></span>
* <span data-ttu-id="04f9d-197">어떤 데이터를 어떤 응용 프로그램과 공유했는지 기록하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-197">Having a record of what data was shared with which application is a good thing.</span></span>  <span data-ttu-id="04f9d-198">데이터는 더욱 전송하기 쉬워졌으며 어떤 데이터를 어떤 응용 프로그램으로 누구와 공유했는지 기록해놓는 것이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-198">Data is more transportable than ever and having a clear record of who shared what data with which applications is useful.</span></span>
* <span data-ttu-id="04f9d-199">oAuth용 Azure AD를 사용하는 응용 프로그램은 사용자가 응용 프로그램에 부여할 수 있는 권한 및 관리자가 동의하는 데 필요한 권한을 정확하게 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-199">Apps who use Azure AD for oAuth decide exactly what permissions that users are able to grant to applications and which permissions require an admin to agree to.</span></span>  <span data-ttu-id="04f9d-200">더 큰 범위 및 보다 중요한 사용 권한에 대해서는 관리자만 동의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-200">It should go without saying that only admins can consent to larger scopes and more significant permissions.</span></span>
* <span data-ttu-id="04f9d-201">사용자가 응용 프로그램을 추가하고 응용 프로그램이 데이터에 액세스하도록 허용하는 것은 감사된 이벤트이므로 Azure 관리 포털 내의 감사 보고서를 보고 디렉터리에 응용 프로그램을 추가하는 방법을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-201">Users adding and allowing apps to access their data are audited events so you can view the Audit Reports within the Azure Managment portal to determine how an app was added to the directory.</span></span>

<span data-ttu-id="04f9d-202">**참고:** *Microsoft는 수개월 동안 기본 구성을 사용하여 운영해오고 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="04f9d-202">**Note:** *Microsoft itself has been operating using the default configuration for many months now.*</span></span>

<span data-ttu-id="04f9d-203">요약하자면 Azure 관리 포털에서 디렉터리 구성을 수정하여 디렉터리의 사용자가 응용 프로그램을 추가하거나 응용 프로그램과 공유할 정보를 결정하지 못하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-203">With all of that said it is possible to prevent users in your directory from adding applications and from exercising discretion over what information they share with applications by modifying Directory configuration in the Azure Management portal.</span></span>  <span data-ttu-id="04f9d-204">다음 구성은 Azure 관리 포털 내의 디렉터리의 "구성" 탭에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04f9d-204">The following configuration can be accessed within the Azure Management portal on your Directory's "Configure" tab.</span></span>

![통합된 응용 프로그램 설정을 구성하기 위한 UI의 스크린샷][app_settings]

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="04f9d-206">다음 단계</span><span class="sxs-lookup"><span data-stu-id="04f9d-206">Next steps</span></span>
<span data-ttu-id="04f9d-207">응용 프로그램을 Azure AD에 추가하는 방법 및 응용 프로그램에 맞게 서비스를 구성하는 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="04f9d-207">Learn more about how to add applications to Azure AD and how to configure services for apps.</span></span>

* <span data-ttu-id="04f9d-208">개발자: [응용 프로그램을 AAD와 통합하는 방법에 대해 알아보기](https://msdn.microsoft.com/library/azure/dn151122.aspx)</span><span class="sxs-lookup"><span data-stu-id="04f9d-208">Developers: [Learn how to integrate an application with AAD](https://msdn.microsoft.com/library/azure/dn151122.aspx)</span></span>
* <span data-ttu-id="04f9d-209">개발자: [GitHub에서 Azure Active Directory와 통합된 앱의 샘플 코드 검토하기](https://github.com/AzureADSamples)</span><span class="sxs-lookup"><span data-stu-id="04f9d-209">Developers: [Review sample code for apps integrated with Azure Active Directory on GitHub](https://github.com/AzureADSamples)</span></span>
* <span data-ttu-id="04f9d-210">개발자 및 IT 전문가: [Azure Active Directory Graph API용 REST API 설명서 검토하기](https://msdn.microsoft.com/library/azure/hh974478.aspx)</span><span class="sxs-lookup"><span data-stu-id="04f9d-210">Developers and IT Pros: [Review the REST API documentation for the Azure Active Directory Graph API](https://msdn.microsoft.com/library/azure/hh974478.aspx)</span></span>
* <span data-ttu-id="04f9d-211">IT 전문가: [응용 프로그램 갤러리에서 Azure Active Directory 사전 통합된 응용 프로그램을 사용하는 방법에 대해 알아보기](https://msdn.microsoft.com/library/azure/dn308590.aspx)</span><span class="sxs-lookup"><span data-stu-id="04f9d-211">IT Pros: [Learn how to use Azure Active Directory pre-integrated applications from the App Gallery](https://msdn.microsoft.com/library/azure/dn308590.aspx)</span></span>
* <span data-ttu-id="04f9d-212">IT 전문가: [사전 통합된 특정 응용 프로그램 구성에 대한 자습서 찾기](https://msdn.microsoft.com/library/azure/dn893637.aspx)</span><span class="sxs-lookup"><span data-stu-id="04f9d-212">IT Pros: [Find tutorials for configuring specific pre-integrated apps](https://msdn.microsoft.com/library/azure/dn893637.aspx)</span></span>
* <span data-ttu-id="04f9d-213">IT 전문가: [Azure Active Directory 응용 프로그램 프록시를 사용하여 응용 프로그램을 게시하는 방법에 대해 알아보기](https://msdn.microsoft.com/library/azure/dn768219.aspx)</span><span class="sxs-lookup"><span data-stu-id="04f9d-213">IT Pros: [Learn how to publish an app using the Azure Active Directory Application Proxy](https://msdn.microsoft.com/library/azure/dn768219.aspx)</span></span>

## <a name="see-also"></a><span data-ttu-id="04f9d-214">참고 항목</span><span class="sxs-lookup"><span data-stu-id="04f9d-214">See also</span></span>
* [<span data-ttu-id="04f9d-215">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="04f9d-215">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)

<!--Image references-->
[apps_service_principals_directory]:../media/active-directory-how-applications-are-added/HowAppsAreAddedToAAD.jpg
[app_settings]:../media/active-directory-how-applications-are-added/IntegratedAppSettings.jpg
