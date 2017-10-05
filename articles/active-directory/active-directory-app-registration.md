---
title: "Azure Active Directory 앱 등록 | Microsoft Docs"
description: "이 문서에서는 Azure Portal을 사용하여 Azure Active Directory에 응용 프로그램을 등록하는 방법에 대해 설명합니다."
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 7dc7b89f-653f-405a-b5f4-2c1288720c15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: priyamo
ms.reviewer: elisol
ms.openlocfilehash: 2f2817688beb2028fd0bba8522827d87a0097f21
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="register-your-application-with-your-azure-active-directory-tenant"></a><span data-ttu-id="ecb95-103">Azure Active Directory 테넌트로 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="ecb95-103">Register your application with your Azure Active Directory tenant</span></span>

<span data-ttu-id="ecb95-104">Azure Portal을 사용하여 Azure AD(Azure Active Directory) 테넌트로 응용 프로그램을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-104">You can use the Azure portal to register your application with your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="ecb95-105">이렇게 하면 응용 프로그램의 응용 프로그램 ID가 만들어져 토큰을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-105">This creates an Application ID for the application, and enables it to receive tokens.</span></span>

1. <span data-ttu-id="ecb95-106">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-106">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ecb95-107">페이지의 오른쪽 위 모서리에서 계정을 선택하여 Azure AD 테넌트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-107">Choose your Azure AD tenant by selecting your account in the top right corner of the page.</span></span>
3. <span data-ttu-id="ecb95-108">왼쪽 탐색 창에서 **추가 서비스**를 선택하고 **앱 등록**을 클릭한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-108">In the left-hand navigation pane, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
4. <span data-ttu-id="ecb95-109">프롬프트에 따라 새 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-109">Follow the prompts and create a new application.</span></span> <span data-ttu-id="ecb95-110">웹 응용 프로그램 또는 네이티브 응용 프로그램에 대한 구체적인 예제를 원하는 경우 [빠른 시작](active-directory-developers-guide.md)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-110">If you'd like specific examples for web applications or native applications, check out our [quickstarts](active-directory-developers-guide.md).</span></span>
  * <span data-ttu-id="ecb95-111">웹 응용 프로그램의 경우 사용자가 로그인할 수 있는 앱의 기본 URL인 **로그인 URL**을 제공합니다(예: `http://localhost:12345`).</span><span class="sxs-lookup"><span data-stu-id="ecb95-111">For Web Applications, provide the **Sign-On URL**, which is the base URL of your app, where users can sign in e.g `http://localhost:12345`.</span></span>
<!--TODO: add once App ID URI is configurable: The **App ID URI** is a unique identifier for your application. The convention is to use `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * <span data-ttu-id="ecb95-112">네이티브 응용 프로그램의 경우 Azure AD에서 토큰 응답을 반환하는 데 사용하는 **리디렉션 URI**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-112">For Native Applications, provide a **Redirect URI**, which Azure AD uses to return token responses.</span></span> <span data-ttu-id="ecb95-113">응용 프로그램에 고유하게 해당되는 값을 입력합니다(예: `http://MyFirstAADApp`</span><span class="sxs-lookup"><span data-stu-id="ecb95-113">Enter a value specific to your application, .e.g `http://MyFirstAADApp`</span></span>
5. <span data-ttu-id="ecb95-114">등록을 완료하면 Azure AD에서 응용 프로그램에 고유한 클라이언트 식별자인 응용 프로그램 ID를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-114">Once you've completed registration, Azure AD assigns your application a unique client identifier, the Application ID.</span></span>

## <a name="update-application-settings-from-the-azure-portal"></a><span data-ttu-id="ecb95-115">Azure Portal에서 응용 프로그램 설정 업데이트</span><span class="sxs-lookup"><span data-stu-id="ecb95-115">Update application settings from the Azure portal</span></span>

<span data-ttu-id="ecb95-116">Azure Portal을 사용하여 기존 응용 프로그램 설정을 쉽게 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-116">You can easily modify an existing application's settings using the Azure portal.</span></span> <span data-ttu-id="ecb95-117">예를 들어 Azure AD에서 토큰 응답을 발급하는 회신 URL을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-117">For example, you may want to configure a reply URL, which is where Azure AD issues token responses.</span></span> <span data-ttu-id="ecb95-118">또한 응용 프로그램이 Microsoft Graph API에 액세스할 수 있도록 다른 응용 프로그램에 대한 권한을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-118">You may also want to configure permissions to other applications, for instance to allow your application to access the Microsoft Graph API.</span></span> <span data-ttu-id="ecb95-119">이러한 모든 작업은 응용 프로그램 설정 페이지에서 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-119">You can do all this through the application settings page.</span></span>

1. <span data-ttu-id="ecb95-120">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-120">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ecb95-121">페이지의 오른쪽 위 모서리에서 계정을 선택하여 Azure AD 테넌트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-121">Choose your Azure AD tenant by selecting your account in the top right corner of the page.</span></span>
3. <span data-ttu-id="ecb95-122">왼쪽 탐색 창에서 **추가 서비스**를 선택하고 **앱 등록**을 클릭한 다음 목록에서 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-122">In the left-hand navigation pane, choose **More Services**, click **App Registrations**, and choose your application from the list.</span></span>
4. <span data-ttu-id="ecb95-123">**설정**을 클릭하여 응용 프로그램의 설정 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-123">Click **Settings** to open up the settings page for the application.</span></span>
  * <span data-ttu-id="ecb95-124">**속성** 페이지에서 응용 프로그램의 일반 정보를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-124">The **Properties** page lets you modify the general information for the application.</span></span> <span data-ttu-id="ecb95-125">여기에는 응용 프로그램 이름, 로그인 URL 및 로그아웃 URL이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-125">This includes the application name, the sign-on URL, and the logout URL.</span></span>
  * <span data-ttu-id="ecb95-126">**회신 URL** 페이지에서 Azure AD가 토큰 응답을 보내는 회신 URL을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-126">The **Reply URLs** page allows you to add a reply URL, which is where Azure AD sends token responses.</span></span>
  * <span data-ttu-id="ecb95-127">**소유자** 페이지에서 응용 프로그램 소유자를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-127">The **Owners** page allows you to add application owners.</span></span>
  * <span data-ttu-id="ecb95-128">**권한** 페이지에서 앱에 대한 권한을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-128">The **Permissions** page allows you to configure permissions for the app.</span></span> <span data-ttu-id="ecb95-129">예를 들어 Microsoft Graph API에 액세스하려면 API 선택기에서 **추가**를 클릭하고 **Microsoft Graph**를 선택한 다음 필요한 권한을 선택합니다(예: **디렉터리 데이터 읽기**).</span><span class="sxs-lookup"><span data-stu-id="ecb95-129">For example, to access the Microsoft Graph API, click **Add** and select **Microsoft Graph** in the API selector, then choose the permission required, for example **Read Directory Data**.</span></span>
  * <span data-ttu-id="ecb95-130">**키** 페이지에서 응용 프로그램 비밀을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-130">The **Keys** page allows you to add application secrets.</span></span> <span data-ttu-id="ecb95-131">비밀은 만든 직후에 한 번만 표시되므로 나중에 사용하기 위해 복사해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-131">The secret will only be displayed once immediately after creation, so make sure to copy it for further use.</span></span>

## <a name="use-the-inline-manifest-editor"></a><span data-ttu-id="ecb95-132">인라인 매니페스트 편집기 사용</span><span class="sxs-lookup"><span data-stu-id="ecb95-132">Use the inline manifest editor</span></span>

<span data-ttu-id="ecb95-133">인라인 매니페스트 편집기를 사용하여 Azure Portal에서 직접 공개되지 않는 특정 응용 프로그램의 속성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-133">You can use the inline manifest editor to modify certain application properties that are not exposed directly in the Azure portal.</span></span> <span data-ttu-id="ecb95-134">예를 들어 이 편집기에서 응용 프로그램의 앱 ID URI를 수정하거나 기본 권한 부여 코드 흐름 대신 OAuth2.0 암시적 흐름을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-134">For example, you can use it to modify the application's App ID URI or to enable the OAuth2.0 implicit flow instead of the default authorization grant code flow.</span></span>

1. <span data-ttu-id="ecb95-135">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-135">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ecb95-136">페이지의 오른쪽 위 모서리에서 계정을 선택하여 Azure AD 테넌트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-136">Choose your Azure AD tenant by selecting your account in the top right corner of the page.</span></span>
3. <span data-ttu-id="ecb95-137">왼쪽 탐색 창에서 **추가 서비스**를 선택하고 **앱 등록**을 클릭한 다음 목록에서 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-137">In the left-hand navigation pane, choose **More Services**, click **App Registrations**, and choose your application from the list.</span></span>
4. <span data-ttu-id="ecb95-138">응용 프로그램 페이지에서 **매니페스트**를 클릭하여 인라인 매니페스트 편집기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-138">Click **Manifest** from the application page to open the inline manifest editor.</span></span>
5. <span data-ttu-id="ecb95-139">매니페스트를 직접 변경하고 준비가 되면 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-139">You can directly make changes to the manifest and save it when you're ready.</span></span> <span data-ttu-id="ecb95-140">또는 매니페스트를 다운로드하여 선호하는 편집기에서 열고 업데이트된 매니페스트를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-140">Alternatively, you can download the manifest to open it in your favorite editor and upload the updated manifest.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ecb95-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ecb95-141">Next Steps</span></span>

1. <span data-ttu-id="ecb95-142">Azure AD를 사용하여 인증을 수행하는 응용 프로그램에 대한 자세한 연습에 대해 [빠른 시작](active-directory-developers-guide.md)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-142">Check out the [Quickstarts](active-directory-developers-guide.md) for detailed walkthroughs of applications performing authentication using Azure AD.</span></span>
2. <span data-ttu-id="ecb95-143">[GitHub](https://github.com/azure-samples)에서 코드 샘플에 대한 전체 목록을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb95-143">Check out our full list of code samples in [GitHub](https://github.com/azure-samples).</span></span>
