---
title: "Azure AD 갤러리 응용 프로그램에 대해 사용자 프로비전을 구성하는 방법 | Microsoft Docs"
description: "Azure AD 응용 프로그램 갤러리에 이미 나열된 응용 프로그램에 대해 다양한 사용자 계정 프로비전 및 프로비전 해제를 빠르게 구성하는 방법"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 2e38fcb30ea7632339a3ba8815a536872cfcc69e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-user-provisioning-to-an-azure-ad-gallery-application"></a><span data-ttu-id="9f924-103">Azure AD 갤러리 응용 프로그램에 대해 사용자 프로비전을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="9f924-103">How to configure user provisioning to an Azure AD Gallery application</span></span>

<span data-ttu-id="9f924-104">*사용자 계정 프로비전*은 응용 프로그램의 로컬 사용자 프로필 저장소에 사용자 계정 레코드를 생성, 업데이트 및/또는 비활성화하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="9f924-104">*User account provisioning* is the act of creating, updating, and/or disabling user account records in an application’s local user profile store.</span></span> <span data-ttu-id="9f924-105">대부분의 클라우드 및 SaaS 응용 프로그램은 고유한 로컬 사용자 프로필 저장소에 사용자 역할 및 권한을 저장하고, 로컬 저장소의 그러한 사용자 레코드의 존재는 Single Sign-On 및 작업에 대한 액세스를 위해 *필요*합니다.</span><span class="sxs-lookup"><span data-stu-id="9f924-105">Most cloud and SaaS applications store the users role and permissions in their own local user profile store, and presence of such a user record in their local store is *required* for single sign-on and access to work.</span></span>

<span data-ttu-id="9f924-106">Azure Portal에서 엔터프라이즈 앱에 대한 왼쪽 탐색 창의 **프로비전** 탭에는 해당 앱에 대해 지원되는 프로비전 모드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f924-106">In the Azure portal, the **Provisioning** tab in the left navigation pane for an Enterprise App displays what provisioning modes are supported for that app.</span></span> <span data-ttu-id="9f924-107">다음 두 값 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f924-107">This can be one of two values:</span></span>

## <a name="configuring-an-application-for-manual-provisioning"></a><span data-ttu-id="9f924-108">수동 프로비전에 대한 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="9f924-108">Configuring an application for Manual Provisioning</span></span>

<span data-ttu-id="9f924-109">*수동* 프로비전이란 사용자 계정을 해당 앱에서 제공하는 방법을 사용하여 수동으로 만들어야 한다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="9f924-109">*Manual* provisioning means that user accounts must be created manually using the methods provided by that app.</span></span> <span data-ttu-id="9f924-110">해당 앱의 관리 포털에 로그인하고 웹 기반 사용자 인터페이스를 사용하여 사용자를 추가한다는 의미일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f924-110">This could mean logging into an administrative portal for that app and adding users using a web-based user interface.</span></span> <span data-ttu-id="9f924-111">또는 해당 응용 프로그램에서 제공하는 메커니즘을 사용하여 사용자 계정 세부 정보를 스프레드시트에 업로드한다는 의미일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f924-111">Or it could be uploading a spreadsheet with user account detail, using a mechanism provided by that application.</span></span> <span data-ttu-id="9f924-112">앱에서 제공한 설명서를 참조하거나 앱 개발자에게 문의하여 사용할 수 있는 메커니즘을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="9f924-112">Consult the documentation provided by the app, or contact the app developer to determine wat mechanisms are available.</span></span>

<span data-ttu-id="9f924-113">해당 응용 프로그램에 대해 수동 모드만 표시되는 경우 해당 앱에 대해 자동 Azure AD 프로비전 커넥터가 아직 생성되지 않았음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="9f924-113">If Manual is the only mode shown for a given application, it means that no automatic Azure AD provisioning connector has been created for the app yet.</span></span> <span data-ttu-id="9f924-114">또는 앱에서 자동화된 프로비전 커넥터를 빌드하는 필수 구성 요소 사용자 관리 API를 지원하지 않음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="9f924-114">Or it means the app does not support the pre-requisite user management API upon which to build an automated provisioning connector.</span></span>

<span data-ttu-id="9f924-115">해당 앱에 대해 자동 프로비전 지원을 요청하려면 <http://aka.ms/aadapprequest>에서 요청 양식을 작성하세요.</span><span class="sxs-lookup"><span data-stu-id="9f924-115">If you would like to request support for automatic provisioning for a given app, you can fill out a request at <http://aka.ms/aadapprequest>.</span></span>

## <a name="configuring-an-application-for-automatic-provisioning"></a><span data-ttu-id="9f924-116">자동 프로비전에 대한 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="9f924-116">Configuring an application for Automatic Provisioning</span></span>

<span data-ttu-id="9f924-117">*자동*이란 Azure AD 프로비전 커넥터가 이 응용 프로그램에 대해 개발되었음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="9f924-117">*Automatic* means that an Azure AD provisioning connector has been developed for this application.</span></span> <span data-ttu-id="9f924-118">Azure AD 프로비전 서비스 및 작동 방식에 대한 자세한 내용은 [Azure Active Directory를 사용하여 SaaS 응용 프로그램의 사용자를 자동으로 프로비전 및 프로비전 해제](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f924-118">For more information on the Azure AD provisioning service and how it works, see [Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).</span></span>

<span data-ttu-id="9f924-119">특정 사용자 및 그룹을 응용 프로그램에 프로비저닝하는 방법에 대한 자세한 내용은 [엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f924-119">For more information on how to provision specific users and groups to an application, see [Managing user account provisioning for enterprise apps](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).</span></span>

<span data-ttu-id="9f924-120">자동 프로비전을 사용하도록 설정하고 구성하는 데 필요한 실제 단계는 응용 프로그램에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="9f924-120">The actual steps required to enable and configure automatic provisioning vary depending on the application.</span></span>

>[!NOTE]
><span data-ttu-id="9f924-121">응용 프로그램의 프로비전 설정에 관한 설정 자습서를 찾아 해당 단계에 따라 앱 및 Azure AD를 구성하여 프로비전 연결을 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f924-121">You should start by finding the setup tutorial specific to setting up provisioning for your application, and following those steps to configure both the app and Azure AD to create the provisioning connection.</span></span> 
>
>

<span data-ttu-id="9f924-122">앱 자습서는 [Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f924-122">App tutorials can be found at [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).</span></span>

<span data-ttu-id="9f924-123">프로비전을 설정할 때 고려해야 할 중요한 사항은 Azure AD에서 응용 프로그램으로 이동하는 사용자(또는 그룹)를 정의하는 특성 매핑 및 워크플로를 검토하고 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9f924-123">An important thing to consider when setting up provisioning be to review and configure the attribute mappings and workflows that define which user (or group) properties flow from Azure AD to the application.</span></span> <span data-ttu-id="9f924-124">여기에는 두 시스템 간 사용자/그룹을 고유하게 식별하고 일치하는 데 사용되는 “일치하는 속성” 설정이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f924-124">This includes setting the “matching property” that be used to uniquely identify and match users/groups between the two systems.</span></span> <span data-ttu-id="9f924-125">이 중요한 프로세스에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="9f924-125">For more information on this important process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f924-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9f924-126">Next steps</span></span>
[<span data-ttu-id="9f924-127">Azure Active Directory에서 SaaS 응용 프로그램에 대한 사용자 프로비전 특성 매핑 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="9f924-127">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings)

