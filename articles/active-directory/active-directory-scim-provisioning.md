---
title: "System for Cross-Domain Identity Management를 사용하여 사용자 및 그룹을 Azure Active Directory에서 응용 프로그램으로 자동 프로비전 | Microsoft Docs"
description: "Azure Active Directory는 SCIM 프로토콜 사양에 정의된 인터페이스를 가진 웹 서비스가 향하는 응용 프로그램 또는 ID 저장소에 사용자 및 그룹을 자동으로 프로비전할 수 있습니다."
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 4d86f3dc-e2d3-4bde-81a3-4a0e092551c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.custom: aaddev;it-pro;oldportal
ms.openlocfilehash: 91978cee88d55c99bcb63c63cdaf01581ae84668
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="using-system-for-cross-domain-identity-management-to-automatically-provision-users-and-groups-from-azure-active-directory-to-applications"></a><span data-ttu-id="3e3a9-103">도메인 간 ID 관리용 시스템을 사용하여 사용자 및 그룹을 Azure Active Directory에서 응용 프로그램으로 자동 프로비전</span><span class="sxs-lookup"><span data-stu-id="3e3a9-103">Using System for Cross-Domain Identity Management to automatically provision users and groups from Azure Active Directory to applications</span></span>

## <a name="overview"></a><span data-ttu-id="3e3a9-104">개요</span><span class="sxs-lookup"><span data-stu-id="3e3a9-104">Overview</span></span>
<span data-ttu-id="3e3a9-105">Azure AD(Active Directory)는 [SCIM(System for Cross-Domain Identity Management) 2.0 프로토콜 사양](https://tools.ietf.org/html/draft-ietf-scim-api-19)에 정의된 인터페이스를 가진 웹 서비스가 향하는 응용 프로그램 또는 ID 저장소에 사용자 및 그룹을 자동으로 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-105">Azure Active Directory (Azure AD) can automatically provision users and groups to any application or identity store that is fronted by a web service with the interface defined in the [System for Cross-Domain Identity Management (SCIM) 2.0 protocol specification](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span></span> <span data-ttu-id="3e3a9-106">Azure Active Directory는 웹 서비스에 할당된 사용자 및 그룹을 만들고 수정하고 삭제하는 요청을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-106">Azure Active Directory can send requests to create, modify, or delete assigned users and groups to the web service.</span></span> <span data-ttu-id="3e3a9-107">그러면 웹 서비스에서 이러한 요청을 대상 ID 저장소의 작업으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-107">The web service can then translate those requests into operations on the target identity store.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="3e3a9-108">이 문서에서 참조되는 Azure 클래식 포털을 사용하는 대신 Azure Portal에서 [Azure AD 관리 센터](https://aad.portal.azure.com)를 사용하여 Azure AD를 관리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-108">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> 



<span data-ttu-id="3e3a9-109">![][0]
*그림 1: 웹 서비스를 통해 Azure Active Directory에서 ID 저장소에 프로비전*</span><span class="sxs-lookup"><span data-stu-id="3e3a9-109">![][0]
*Figure 1: Provisioning from Azure Active Directory to an identity store via a web service*</span></span>

<span data-ttu-id="3e3a9-110">이 기능은 Azure AD에서 “고유한 앱 가져오기” 기능과 함께 사용하여 제공하거나 SCIM 웹 서비스가 앞서는 응용 프로그램에 대해 Single Sign-On 및 자동 사용자 프로비저닝을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-110">This capability can be used in conjunction with the “bring your own app” capability in Azure AD to enable single sign-on and automatic user provisioning for applications that provide or are fronted by a SCIM web service.</span></span>

<span data-ttu-id="3e3a9-111">Azure Active Directory에서 SCIM을 사용하는 방법에 대한 두 가지 사용 사례가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-111">There are two use cases for using SCIM in Azure Active Directory:</span></span>

* <span data-ttu-id="3e3a9-112">**SCIM을 지원하는 응용 프로그램에 사용자 및 그룹 프로비전** SCIM 2.0을 지원하며 인증에 OAuth 전달자 토큰을 사용하는 응용 프로그램은 별도의 구성 없이 Azure AD에서 바로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-112">**Provisioning users and groups to applications that support SCIM** Applications that support SCIM 2.0 and use OAuth bearer tokens for authentication works with Azure AD without configuration.</span></span>
* <span data-ttu-id="3e3a9-113">**다른 API 기반 프로비전을 지원하는 응용 프로그램에 대한 프로비전 솔루션 빌드** 비 SCIM 응용 프로그램의 경우 Azure AD SCIM 끝점과 응용 프로그램이 사용자 프로비저닝에 대해 지원하는 API 간에 변환하는 SCIM 끝점을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-113">**Build your own provisioning solution for applications that support other API-based provisioning** For non-SCIM applications, you can create a SCIM endpoint to translate between the Azure AD SCIM endpoint and any API the application supports for user provisioning.</span></span> <span data-ttu-id="3e3a9-114">SCIM 끝점 개발을 지원하기 위해 SCIM 끝점을 제공하고 SCIM 메시지를 변환하는 방법을 보여주는 코드 샘플과 함께 CLI(공용 언어 인프라) 라이브러리가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-114">To help you develop a SCIM endpoint, we provide Common Language Infrastructure (CLI) libraries along with code samples that show you how to do provide a SCIM endpoint and translate SCIM messages.</span></span>  

## <a name="provisioning-users-and-groups-to-applications-that-support-scim"></a><span data-ttu-id="3e3a9-115">SCIM을 지원하는 응용 프로그램에 사용자 및 그룹 프로비전</span><span class="sxs-lookup"><span data-stu-id="3e3a9-115">Provisioning users and groups to applications that support SCIM</span></span>
<span data-ttu-id="3e3a9-116">Azure AD는 [SCIM(System for Cross-domain Identity Management) 2](https://tools.ietf.org/html/draft-ietf-scim-api-19) 웹 서비스를 구현하고 인증에 대한 OAuth 전달자 토큰을 수락하는 응용 프로그램에 자동으로 할당된 사용자 및 그룹을 프로비전하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-116">Azure AD can be configured to automatically provision assigned users and groups to applications that implement a [System for Cross-domain Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) web service and accept OAuth bearer tokens for authentication.</span></span> <span data-ttu-id="3e3a9-117">SCIM 2.0 사양 내에서 응용 프로그램은 다음의 요구 사항을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-117">Within the SCIM 2.0 specification, applications must meet these requirements:</span></span>

* <span data-ttu-id="3e3a9-118">SCIM 프로토콜의 섹션 3.3에 따라 사용자 및/또는 그룹 만들기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-118">Supports creating users and/or groups, as per section 3.3 of the SCIM protocol.</span></span>  
* <span data-ttu-id="3e3a9-119">SCIM 프로토콜의 섹션 3.5.2에 따라 패치를 사용하여 사용자 및/또는 그룹 수정을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-119">Supports modifying users and/or groups with patch requests as per section 3.5.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="3e3a9-120">SCIM 프로토콜의 섹션 3.4.1에 따라 알려진 리소스 검색을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-120">Supports retrieving a known resource as per section 3.4.1 of the SCIM protocol.</span></span>  
* <span data-ttu-id="3e3a9-121">SCIM 프로토콜의 섹션 3.4.2에 따라 사용자 및/또는 그룹 쿼리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-121">Supports querying users and/or groups, as per section 3.4.2 of the SCIM protocol.</span></span>  <span data-ttu-id="3e3a9-122">기본적으로 사용자는 externalId에서 쿼리되고 그룹은 displayName에서 쿼리됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-122">By default, users are queried by externalId and groups are queried by displayName.</span></span>  
* <span data-ttu-id="3e3a9-123">SCIM 프로토콜의 섹션 3.4.2에 따라 ID 및 관리자에 의한 사용자 쿼리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-123">Supports querying user by ID and by manager as per section 3.4.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="3e3a9-124">SCIM 프로토콜의 섹션 3.4.2에 따라 ID 및 멤버에 의한 그룹 쿼리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-124">Supports querying groups by ID and by member as per section 3.4.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="3e3a9-125">SCIM 프로토콜의 섹션 2.1에 따라 권한 부여에 대한 OAuth 전달자 토큰을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-125">Accepts OAuth bearer tokens for authorization as per section 2.1 of the SCIM protocol.</span></span>

<span data-ttu-id="3e3a9-126">응용 프로그램 공급자 또는 응용 프로그램 공급자의 설명서를 통해 이러한 요구 사항과의 호환성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-126">Check with your application provider, or your application provider's documentation for statements of compatibility with these requirements.</span></span>

### <a name="getting-started"></a><span data-ttu-id="3e3a9-127">시작</span><span class="sxs-lookup"><span data-stu-id="3e3a9-127">Getting started</span></span>
<span data-ttu-id="3e3a9-128">Azure AD 응용 프로그램 갤러리에 있는 "비-갤러리 응용 프로그램" 기능을 사용하여 이 문서에서 설명한 SCIM 프로필을 지원하는 응용 프로그램을 Azure Active Directory에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-128">Applications that support the SCIM profile described in this article can be connected to Azure Active Directory using the "non-gallery application" feature in the Azure AD application gallery.</span></span> <span data-ttu-id="3e3a9-129">연결되면 Azure AD는 할당된 사용자 및 그룹에 응용 프로그램의 SCIM 끝점을 쿼리하고 할당 정보에 따라 사용자 및 그룹을 만들거나 수정하는 동기화 프로세스를 20분마다 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-129">Once connected, Azure AD runs a synchronization process every 20 minutes where it queries the application's SCIM endpoint for assigned users and groups, and creates or modifies them according to the assignment details.</span></span>

<span data-ttu-id="3e3a9-130">**SCIM을 지원하는 응용 프로그램을 연결하려면:**</span><span class="sxs-lookup"><span data-stu-id="3e3a9-130">**To connect an application that supports SCIM:**</span></span>

1. <span data-ttu-id="3e3a9-131">[Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-131">Sign in to [the Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="3e3a9-132">**Azure Active Directory > Enterprise 응용 프로그램을 찾아서 **새 응용 프로그램 > 모두 > 비-갤러리 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-132">Browse to **Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="3e3a9-133">응용 프로그램의 이름을 입력하고 **추가** 아이콘을 클릭하여 앱 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-133">Enter a name for your application, and click **Add** icon to create an app object.</span></span>
    
  <span data-ttu-id="3e3a9-134">![][1]
  *그림 2: Azure AD 응용 프로그램 갤러리*</span><span class="sxs-lookup"><span data-stu-id="3e3a9-134">![][1]
*Figure 2: Azure AD application gallery*</span></span>
    
4. <span data-ttu-id="3e3a9-135">결과 화면에서 왼쪽 열의 **프로비전** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-135">In the resulting screen, select the **Provisioning** tab in the left column.</span></span>
5. <span data-ttu-id="3e3a9-136">**프로비전 모드** 메뉴에서 **자동**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-136">In the **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="3e3a9-137">![][2]
  *그림 3: Azure Portal에서 프로비전 구성*</span><span class="sxs-lookup"><span data-stu-id="3e3a9-137">![][2]
*Figure 3: Configuring provisioning in the Azure portal*</span></span>
    
6. <span data-ttu-id="3e3a9-138">**테넌트 URL** 필드에 응용 프로그램의 SCIM 끝점 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-138">In the **Tenant URL** field, enter the URL of the application's SCIM endpoint.</span></span> <span data-ttu-id="3e3a9-139">예: https://api.contoso.com/scim/v2/</span><span class="sxs-lookup"><span data-stu-id="3e3a9-139">Example: https://api.contoso.com/scim/v2/</span></span>
7. <span data-ttu-id="3e3a9-140">SCIM 끝점에 Azure AD가 아닌 다른 발급자의 OAuth 전달자 토큰이 필요한 경우 필요한 OAuth 전달자 토큰을 **비밀 토큰** 필드(선택 사항)에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-140">If the SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy the required OAuth bearer token into the optional **Secret Token** field.</span></span> <span data-ttu-id="3e3a9-141">이 필드를 비워 두면 Azure AD에 각 요청에 따라 Azure AD에서 발급한 OAuth 전달자 토큰이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-141">If this field is left blank, then Azure AD included an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="3e3a9-142">ID 공급자로 Azure AD를 사용하는 앱은 Azure AD에서 발급한 토큰의 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-142">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="3e3a9-143">**연결 테스트** 단추를 클릭하여 Azure Active Directory에서 SCIM 끝점에 연결을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-143">Click the **Test Connection** button to have Azure Active Directory attempt to connect to the SCIM endpoint.</span></span> <span data-ttu-id="3e3a9-144">시도가 실패하면 오류 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-144">If the attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="3e3a9-145">응용 프로그램에 연결 시도가 성공하면 **저장**을 클릭하여 관리자 자격 증명을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-145">If the attempts to connect to the application succeed, then click **Save** to save the admin credentials.</span></span>
10. <span data-ttu-id="3e3a9-146">**매핑** 섹션에는 선택 가능한 특성 매핑 집합이 두 개 있는데, 하나는 사용자 개체용이고 다른 하나는 그룹 개체용입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-146">In the **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="3e3a9-147">각 특성 매핑을 선택하여 Azure Active Directory에서 앱으로 동기화되는 특성을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-147">Select each one to review the attributes that are synchronized from Azure Active Directory to your app.</span></span> <span data-ttu-id="3e3a9-148">**일치** 속성으로 선택한 특성은 업데이트 작업 시 앱의 사용자와 그룹을 일치시키는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-148">The attributes selected as **Matching** properties are used to match the users and groups in your app for update operations.</span></span> <span data-ttu-id="3e3a9-149">저장 단추를 선택하여 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-149">Select the Save button to commit any changes.</span></span>

    >[!NOTE]
    ><span data-ttu-id="3e3a9-150">필요에 따라 "그룹" 매핑을 사용하지 않도록 설정하여 그룹 개체의 동기화를 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-150">You can optionally disable syncing of group objects by disabling the "groups" mapping.</span></span> 

11. <span data-ttu-id="3e3a9-151">**설정** 아래의 **범위** 필드는 동기화되는 사용자 및 그룹을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-151">Under **Settings**, the **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="3e3a9-152">"할당된 사용자 및 그룹만 동기화"(권장)를 선택하면 **사용자 및 그룹** 탭에서 할당된 사용자 및 그룹만 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-152">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in the **Users and groups** tab.</span></span>
12. <span data-ttu-id="3e3a9-153">구성이 완료되면 **프로비전 상태**를 **켜기**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-153">Once your configuration is complete, change the **Provisioning Status** to **On**.</span></span>
13. <span data-ttu-id="3e3a9-154">**저장**을 클릭하여 Azure AD 프로비전 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-154">Click **Save** to start the Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="3e3a9-155">할당된 사용자 및 그룹만 동기화하는 경우(권장) **사용자 및 그룹** 탭을 선택하고 동기화하려는 사용자 및/또는 그룹을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-155">If syncing only assigned users and groups (recommended), be sure to select the **Users and groups** tab and assign the users and/or groups you wish to sync.</span></span>

<span data-ttu-id="3e3a9-156">초기 동기화가 시작되면 **감사 로그** 탭을 사용하여 진행 상황을 모니터링할 수 있습니다. 이 탭에는 앱의 프로비전 서비스에서 수행하는 모든 작업이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-156">Once the initial synchronization has started, you can use the **Audit logs** tab to monitor progress, which shows all actions performed by the provisioning service on your app.</span></span> <span data-ttu-id="3e3a9-157">Azure AD 프로비저닝 로그를 읽는 방법에 대한 자세한 내용은 [자동 사용자 계정 프로비저닝에 대한 보고](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-157">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

>[!NOTE]
><span data-ttu-id="3e3a9-158">초기 동기화는 서비스가 실행되는 동안 약 20분마다 발생하는 차후 동기화보다 더 많은 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-158">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> 


## <a name="building-your-own-provisioning-solution-for-any-application"></a><span data-ttu-id="3e3a9-159">응용 프로그램에 대한 고유한 프로비전 솔루션 구축</span><span class="sxs-lookup"><span data-stu-id="3e3a9-159">Building your own provisioning solution for any application</span></span>
<span data-ttu-id="3e3a9-160">Azure Active Directory와 상호 작용하는 SCIM 웹 서비스를 만들어서 REST 또는 SOAP 사용자 프로비전 API를 제공하는 거의 모든 응용 프로그램에 대한 Single Sign-On 및 자동 사용자 프로비전을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-160">By creating a SCIM web service that interfaces with Azure Active Directory, you can enable single sign-on and automatic user provisioning for virtually any application that provides a REST or SOAP user provisioning API.</span></span>

<span data-ttu-id="3e3a9-161">방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-161">Here’s how it works:</span></span>

1. <span data-ttu-id="3e3a9-162">Azure AD는 [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/)로 명명된 공용 언어 인프라 라이브러리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-162">Azure AD provides a common language infrastructure library named [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span></span> <span data-ttu-id="3e3a9-163">시스템 통합 업체 및 개발자는 이 라이브러리를 사용하여 응용 프로그램 ID 저장소에 Azure AD를 연결할 수 있는 SCIM 기반 웹 서비스 끝점을 만들고 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-163">System integrators and developers can use this library to create and deploy a SCIM-based web service endpoint capable of connecting Azure AD to any application’s identity store.</span></span>
2. <span data-ttu-id="3e3a9-164">매핑은 웹 서비스에서 구현되어 스키마에 응용 프로그램에서 필요한 사용자 스키마 및 프로토콜에 표준화된 사용자 스키마를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-164">Mappings are implemented in the web service to map the standardized user schema to the user schema and protocol required by the application.</span></span>
3. <span data-ttu-id="3e3a9-165">끝점 URL은 응용 프로그램 갤러리에서 사용자 지정 응용 프로그램의 일부로 Azure AD에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-165">The endpoint URL is registered in Azure AD as part of a custom application in the application gallery.</span></span>
4. <span data-ttu-id="3e3a9-166">사용자 및 그룹은 Azure AD에서 이 응용 프로그램에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-166">Users and groups are assigned to this application in Azure AD.</span></span> <span data-ttu-id="3e3a9-167">할당 시 큐에 저장하여 대상 응용 프로그램에 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-167">Upon assignment, they are put into a queue to be synchronized to the target application.</span></span> <span data-ttu-id="3e3a9-168">큐를 처리하는 동기화 프로세스는 20분마다 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-168">The synchronization process handling the queue runs every 20 minutes.</span></span>

### <a name="code-samples"></a><span data-ttu-id="3e3a9-169">코드 샘플</span><span class="sxs-lookup"><span data-stu-id="3e3a9-169">Code Samples</span></span>
<span data-ttu-id="3e3a9-170">이 과정을 보다 쉽게 하려면 [코드 샘플](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) 의 집합이 SCIM 웹 서비스 끝점을 만들고 자동 프로비전을 보여주도록 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-170">To make this process easier, a set of [code samples](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) are provided that create a SCIM web service endpoint and demonstrate automatic provisioning.</span></span> <span data-ttu-id="3e3a9-171">한 가지 샘플은 사용자 및 그룹을 나타내는 쉼표로 구분된 값의 행이 있는 파일을 유지 관리하는 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-171">One sample is of a provider that maintains a file with rows of comma-separated values representing users and groups.</span></span>  <span data-ttu-id="3e3a9-172">다른 샘플은 Amazon 웹 서비스 ID 및 액세스 관리 서비스에서 작동하는 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-172">The other is of a provider that operates on the Amazon Web Services Identity and Access Management service.</span></span>  

<span data-ttu-id="3e3a9-173">**필수 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="3e3a9-173">**Prerequisites**</span></span>

* <span data-ttu-id="3e3a9-174">Visual Studio 2013 이상</span><span class="sxs-lookup"><span data-stu-id="3e3a9-174">Visual Studio 2013 or later</span></span>
* [<span data-ttu-id="3e3a9-175">Azure SDK for .NET</span><span class="sxs-lookup"><span data-stu-id="3e3a9-175">Azure SDK for .NET</span></span>](https://azure.microsoft.com/downloads/)
* <span data-ttu-id="3e3a9-176">ASP.NET framework 4.5를 SCIM 끝점으로 사용하도록 지원하는 Windows 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-176">Windows machine that supports the ASP.NET framework 4.5 to be used as the SCIM endpoint.</span></span> <span data-ttu-id="3e3a9-177">이 컴퓨터는 클라우드에서 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-177">This machine must be accessible from the cloud</span></span>
* [<span data-ttu-id="3e3a9-178">Azure AD Premium의 평가판 또는 사용이 허가된 버전의 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="3e3a9-178">An Azure subscription with a trial or licensed version of Azure AD Premium</span></span>](https://azure.microsoft.com/services/active-directory/)
* <span data-ttu-id="3e3a9-179">Amazon AWS 샘플에는 [Visual Studio용 AWS Toolkit](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html)의 라이브러리가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-179">The Amazon AWS sample requires libraries from the [AWS Toolkit for Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span></span> <span data-ttu-id="3e3a9-180">자세한 내용은 샘플에 포함된 README 파일을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-180">For more information, see the README file included with the sample.</span></span>

### <a name="getting-started"></a><span data-ttu-id="3e3a9-181">시작하기</span><span class="sxs-lookup"><span data-stu-id="3e3a9-181">Getting Started</span></span>
<span data-ttu-id="3e3a9-182">Azure AD에서 프로비전 요청을 수락할 수 있는 SCIM 끝점을 구현하는 가장 쉬운 방법은 쉼표로 구분된 값(CSV) 파일에 프로비전된 사용자를 출력하는 코드 샘플을 빌드하고 배포하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-182">The easiest way to implement a SCIM endpoint that can accept provisioning requests from Azure AD is to build and deploy the code sample that outputs the provisioned users to a comma-separated value (CSV) file.</span></span>

<span data-ttu-id="3e3a9-183">**샘플 SCIM 끝점을 만들려면:**</span><span class="sxs-lookup"><span data-stu-id="3e3a9-183">**To create a sample SCIM endpoint:**</span></span>

1. <span data-ttu-id="3e3a9-184">[https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span><span class="sxs-lookup"><span data-stu-id="3e3a9-184">Download the code sample package at [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span></span>
2. <span data-ttu-id="3e3a9-185">패키지의 압축을 풀고 C:\AzureAD-BYOA-Provisioning-Samples와 같은 위치에서 Windows 컴퓨터에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-185">Unzip the package and place it on your Windows machine at a location such as C:\AzureAD-BYOA-Provisioning-Samples\.</span></span>
3. <span data-ttu-id="3e3a9-186">이 폴더에 Visual Studio에 있는 FileProvisioningAgent 솔루션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-186">In this folder, launch the FileProvisioningAgent solution in Visual Studio.</span></span>
4. <span data-ttu-id="3e3a9-187">**도구 > 라이브러리 패키지 관리자 > 패키지 관리자 콘솔**을 선택하고, FileProvisioningAgent 프로젝트에 대해 다음 명령을 실행하여 솔루션 참조를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-187">Select **Tools > Library Package Manager > Package Manager Console**, and execute the following commands for the FileProvisioningAgent project to resolve the solution references:</span></span>
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. <span data-ttu-id="3e3a9-188">FileProvisioningAgent 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-188">Build the FileProvisioningAgent project.</span></span>
6. <span data-ttu-id="3e3a9-189">관리자 권한으로 Windows에서 명령 프롬프트 응용 프로그램을 시작하고 **cd** 명령을 사용하여 디렉터리를 **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-189">Launch the Command Prompt application in Windows (as an Administrator), and use the **cd** command to change the directory to your **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** folder.</span></span>
7. <span data-ttu-id="3e3a9-190">다음 명령을 실행하고, <ip-address>를 Windows 컴퓨터의 IP 주소 또는 도메인 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-190">Run the following command, replacing <ip-address> with the IP address or domain name of the Windows machine:</span></span>
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. <span data-ttu-id="3e3a9-191">Windows의 **Windows 설정 > 네트워크 및 인터넷 설정**에서 **Windows 방화벽 > 고급 설정**을 선택하고 포트 9000에 인바운드 액세스를 허용하는 **인바운드 규칙**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-191">In Windows under **Windows Settings > Network & Internet Settings**, select the **Windows Firewall > Advanced Settings**, and create an **Inbound Rule** that allows inbound access to port 9000.</span></span>
9. <span data-ttu-id="3e3a9-192">Windows 컴퓨터가 라우터 뒤에 있는 경우 라우터는 인터넷에 노출되는 포트 9000과 Windows 컴퓨터에 있는 포트 9000 사이의 네트워크 액세스 변환을 수행하도록 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-192">If the Windows machine is behind a router, the router needs to be configured to perform Network Access Translation between its port 9000 that is exposed to the internet, and port 9000 on the Windows machine.</span></span> <span data-ttu-id="3e3a9-193">Azure AD의 경우 클라우드에서 이 끝점에 액세스할 수 있으려면 이것이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-193">This is required for Azure AD to be able to access this endpoint in the cloud.</span></span>

<span data-ttu-id="3e3a9-194">**Azure AD에서 샘플 SCIM 끝점을 등록하려면:**</span><span class="sxs-lookup"><span data-stu-id="3e3a9-194">**To register the sample SCIM endpoint in Azure AD:**</span></span>

1. <span data-ttu-id="3e3a9-195">[Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-195">Sign in to [the Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="3e3a9-196">**Azure Active Directory > Enterprise 응용 프로그램을 찾아서 **새 응용 프로그램 > 모두 > 비-갤러리 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-196">Browse to **Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="3e3a9-197">응용 프로그램의 이름을 입력하고 **추가** 아이콘을 클릭하여 앱 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-197">Enter a name for your application, and click **Add** icon to create an app object.</span></span> <span data-ttu-id="3e3a9-198">만든 응용 프로그램 개체는 SCIM 끝점뿐 아니라 Single Sign-On을 프로비전하고 구현하려는 대상 앱을 나타내는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-198">The application object created is intended to represent the target app you would be provisioning to and implementing single sign-on for, and not just the SCIM endpoint.</span></span>
4. <span data-ttu-id="3e3a9-199">결과 화면에서 왼쪽 열의 **프로비전** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-199">In the resulting screen, select the **Provisioning** tab in the left column.</span></span>
5. <span data-ttu-id="3e3a9-200">**프로비전 모드** 메뉴에서 **자동**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-200">In the **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="3e3a9-201">![][2]
  *그림 4: Azure Portal에서 프로비전 구성*</span><span class="sxs-lookup"><span data-stu-id="3e3a9-201">![][2]
*Figure 4: Configuring provisioning in the Azure portal*</span></span>
    
6. <span data-ttu-id="3e3a9-202">**테넌트 URL** 필드에 인터넷에 노출된 URL 및 SCIM 끝점의 포트를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-202">In the **Tenant URL** field, enter the internet-exposed URL and port of your SCIM endpoint.</span></span> <span data-ttu-id="3e3a9-203"><ip-address>가 인터넷 노출된 IP 주소인 경우 http://testmachine.contoso.com:9000 또는 http://<ip-address>:9000/과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-203">This would be something like http://testmachine.contoso.com:9000 or http://<ip-address>:9000/, where <ip-address> is the internet exposed IP address.</span></span>  
7. <span data-ttu-id="3e3a9-204">SCIM 끝점에 Azure AD가 아닌 다른 발급자의 OAuth 전달자 토큰이 필요한 경우 필요한 OAuth 전달자 토큰을 **비밀 토큰** 필드(선택 사항)에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-204">If the SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy the required OAuth bearer token into the optional **Secret Token** field.</span></span> <span data-ttu-id="3e3a9-205">이 필드를 비워 두면 Azure AD에 각 요청에 따라 Azure AD에서 발급한 OAuth 전달자 토큰이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-205">If this field is left blank, then Azure AD will include an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="3e3a9-206">ID 공급자로 Azure AD를 사용하는 앱은 Azure AD에서 발급한 토큰의 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-206">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="3e3a9-207">**연결 테스트** 단추를 클릭하여 Azure Active Directory에서 SCIM 끝점에 연결을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-207">Click the **Test Connection** button to have Azure Active Directory attempt to connect to the SCIM endpoint.</span></span> <span data-ttu-id="3e3a9-208">시도가 실패하면 오류 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-208">If the attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="3e3a9-209">응용 프로그램에 연결 시도가 성공하면 **저장**을 클릭하여 관리자 자격 증명을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-209">If the attempts to connect to the application succeed, then click **Save** to save the admin credentials.</span></span>
10. <span data-ttu-id="3e3a9-210">**매핑** 섹션에는 선택 가능한 특성 매핑 집합이 두 개 있는데, 하나는 사용자 개체용이고 다른 하나는 그룹 개체용입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-210">In the **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="3e3a9-211">각 특성 매핑을 선택하여 Azure Active Directory에서 앱으로 동기화되는 특성을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-211">Select each one to review the attributes that are synchronized from Azure Active Directory to your app.</span></span> <span data-ttu-id="3e3a9-212">**일치** 속성으로 선택한 특성은 업데이트 작업 시 앱의 사용자와 그룹을 일치시키는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-212">The attributes selected as **Matching** properties are used to match the users and groups in your app for update operations.</span></span> <span data-ttu-id="3e3a9-213">저장 단추를 선택하여 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-213">Select the Save button to commit any changes.</span></span>
11. <span data-ttu-id="3e3a9-214">**설정** 아래의 **범위** 필드는 동기화되는 사용자 및 그룹을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-214">Under **Settings**, the **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="3e3a9-215">"할당된 사용자 및 그룹만 동기화"(권장)를 선택하면 **사용자 및 그룹** 탭에서 할당된 사용자 및 그룹만 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-215">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in the **Users and groups** tab.</span></span>
12. <span data-ttu-id="3e3a9-216">구성이 완료되면 **프로비전 상태**를 **켜기**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-216">Once your configuration is complete, change the **Provisioning Status** to **On**.</span></span>
13. <span data-ttu-id="3e3a9-217">**저장**을 클릭하여 Azure AD 프로비전 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-217">Click **Save** to start the Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="3e3a9-218">할당된 사용자 및 그룹만 동기화하는 경우(권장) **사용자 및 그룹** 탭을 선택하고 동기화하려는 사용자 및/또는 그룹을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-218">If syncing only assigned users and groups (recommended), be sure to select the **Users and groups** tab and assign the users and/or groups you wish to sync.</span></span>

<span data-ttu-id="3e3a9-219">초기 동기화가 시작되면 **감사 로그** 탭을 사용하여 진행 상황을 모니터링할 수 있습니다. 이 탭에는 앱의 프로비전 서비스에서 수행하는 모든 작업이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-219">Once the initial synchronization has started, you can use the **Audit logs** tab to monitor progress, which shows all actions performed by the provisioning service on your app.</span></span> <span data-ttu-id="3e3a9-220">Azure AD 프로비저닝 로그를 읽는 방법에 대한 자세한 내용은 [자동 사용자 계정 프로비저닝에 대한 보고](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-220">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

<span data-ttu-id="3e3a9-221">이 샘플을 확인하는 마지막 단계는 Windows 컴퓨터에서 \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug 폴더에 TargetFile.csv 파일을 여는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-221">The final step in verifying the sample is to open the TargetFile.csv file in the \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug folder on your Windows machine.</span></span> <span data-ttu-id="3e3a9-222">프로비전 프로세스가 실행되면 이 파일은 할당되고 프로비전된 모든 사용자 및 그룹의 세부 사항을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-222">Once the provisioning process is run, this file shows the details of all assigned and provisioned users and groups.</span></span>

### <a name="development-libraries"></a><span data-ttu-id="3e3a9-223">개발 라이브러리</span><span class="sxs-lookup"><span data-stu-id="3e3a9-223">Development libraries</span></span>
<span data-ttu-id="3e3a9-224">SCIM 사양을 준수하는 웹 서비스를 개발하려면 먼저 개발 프로세스를 가속화하기 위해 Microsoft에서 제공하는 다음 라이브러리를 숙지합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-224">To develop your own web service that conforms to the SCIM specification, first familiarize yourself with the following libraries provided by Microsoft to help accelerate the development process:</span></span> 

1. <span data-ttu-id="3e3a9-225">CLI(공용 언어 인프라) 라이브러리는 C#과 같은 해당 인프라에 따라 언어와 함께 사용하기 위해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-225">Common Language Infrastructure (CLI) libraries are offered for use with languages based on that infrastructure, such as C#.</span></span> <span data-ttu-id="3e3a9-226">이러한 라이브러리 중 하나인 [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/)는 다음 일러스트레이션에 표시된 것처럼 Microsoft.SystemForCrossDomainIdentityManagement.IProvider 인터페이스를 선언합니다. 이 라이브러리를 사용하는 개발자는 일반적으로 공급자로 참조되는 클래스를 사용하여 해당 인터페이스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-226">One of those libraries, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declares an interface, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, shown in the following illustration:  A developer using the libraries would implement that interface with a class that may be referred to, generically, as a provider.</span></span> <span data-ttu-id="3e3a9-227">이 라이브러리를 사용하면 개발자는 SCIM 사양을 준수하는 웹 서비스를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-227">The libraries enable the developer to deploy a web service that conforms to the SCIM specification.</span></span> <span data-ttu-id="3e3a9-228">웹 서비스는 인터넷 정보 서비스 또는 실행 가능한 모든 공용 언어 인프라 어셈블리 내에 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-228">The web service can be either hosted within Internet Information Services, or any executable Common Language Infrastructure assembly.</span></span> <span data-ttu-id="3e3a9-229">요청은 공급자의 메서드에 대한 호출로 변환되며, 개발자에 의해 일부 ID 저장소에서 작동하도록 프로그래밍됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-229">Request is translated into calls to the provider’s methods, which would be programmed by the developer to operate on some identity store.</span></span>
  
  ![][3]
  
2. <span data-ttu-id="3e3a9-230">[기본 경로 처리기](http://expressjs.com/guide/routing.html)는 node.js 웹 서비스에 수행된(SCIM 사양에 정의된 대로) 호출을 나타내는 node.js 요청 개체를 구문 분석하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-230">[Express route handlers](http://expressjs.com/guide/routing.html) are available for parsing node.js request objects representing calls (as defined by the SCIM specification), made to a node.js web service.</span></span>   

### <a name="building-a-custom-scim-endpoint"></a><span data-ttu-id="3e3a9-231">사용자 지정 SCIM 끝점 빌드</span><span class="sxs-lookup"><span data-stu-id="3e3a9-231">Building a Custom SCIM Endpoint</span></span>
<span data-ttu-id="3e3a9-232">CLI 라이브러리를 사용하는 개발자는 실행 가능한 공용 언어 인프라 어셈블리 또는 인터넷 정보 서비스 내에서 해당 서비스를 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-232">Using the CLI libraries, developers using those libraries can host their services within any executable Common Language Infrastructure assembly, or within Internet Information Services.</span></span> <span data-ttu-id="3e3a9-233">다음은 http://localhost:9000 주소에 있는 실행 가능한 어셈블리 내에서 서비스를 호스트하기 위한 샘플 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-233">Here is sample code for hosting a service within an executable assembly, at the address http://localhost:9000:</span></span> 

    private static void Main(string[] arguments)
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IProvider and 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
      new DevelopersMonitor();
    Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
      new DevelopersProvider(arguments[1]);
    Microsoft.SystemForCrossDomainIdentityManagement.Service webService = null;
    try
    {
        webService = new WebService(monitor, provider);
        webService.Start("http://localhost:9000");

        Console.ReadKey(true);
    }
    finally
    {
        if (webService != null)
        {
            webService.Dispose();
            webService = null;
        }
    }
    }

    public class WebService : Microsoft.SystemForCrossDomainIdentityManagement.Service
    {
    private Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor;
    private Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider;

    public WebService(
      Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitoringBehavior, 
      Microsoft.SystemForCrossDomainIdentityManagement.IProvider providerBehavior)
    {
        this.monitor = monitoringBehavior;
        this.provider = providerBehavior;
    }

    public override IMonitor MonitoringBehavior
    {
        get
        {
            return this.monitor;
        }

        set
        {
            this.monitor = value;
        }
    }

    public override IProvider ProviderBehavior
    {
        get
        {
            return this.provider;
        }

        set
        {
            this.provider = value;
        }
    }
    }

<span data-ttu-id="3e3a9-234">이 서비스는 다음 루트 인증 기관 중 하나에 속한 HTTP 주소 및 서버 인증 인증서를 가지고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-234">This service must have an HTTP address and server authentication certificate of which the root certification authority is one of the following:</span></span> 

* <span data-ttu-id="3e3a9-235">CNNIC</span><span class="sxs-lookup"><span data-stu-id="3e3a9-235">CNNIC</span></span>
* <span data-ttu-id="3e3a9-236">Comodo</span><span class="sxs-lookup"><span data-stu-id="3e3a9-236">Comodo</span></span>
* <span data-ttu-id="3e3a9-237">CyberTrust</span><span class="sxs-lookup"><span data-stu-id="3e3a9-237">CyberTrust</span></span>
* <span data-ttu-id="3e3a9-238">DigiCert</span><span class="sxs-lookup"><span data-stu-id="3e3a9-238">DigiCert</span></span>
* <span data-ttu-id="3e3a9-239">GeoTrust</span><span class="sxs-lookup"><span data-stu-id="3e3a9-239">GeoTrust</span></span>
* <span data-ttu-id="3e3a9-240">GlobalSign</span><span class="sxs-lookup"><span data-stu-id="3e3a9-240">GlobalSign</span></span>
* <span data-ttu-id="3e3a9-241">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="3e3a9-241">Go Daddy</span></span>
* <span data-ttu-id="3e3a9-242">Verisign</span><span class="sxs-lookup"><span data-stu-id="3e3a9-242">Verisign</span></span>
* <span data-ttu-id="3e3a9-243">WoSign</span><span class="sxs-lookup"><span data-stu-id="3e3a9-243">WoSign</span></span>

<span data-ttu-id="3e3a9-244">서버 인증 인증서는 네트워크 셸 유틸리티를 사용하여 다음과 같이 Windows 호스트의 포트에 바인딩될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-244">A server authentication certificate can be bound to a port on a Windows host using the network shell utility:</span></span> 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

<span data-ttu-id="3e3a9-245">여기서 appid 인수에 제공된 값은 임의의 GUID(Globally Unique Identifier)인 반면 certhash 인수에 제공된 값은 인증서의 지문입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-245">Here, the value provided for the certhash argument is the thumbprint of the certificate, while the value provided for the appid argument is an arbitrary globally unique identifier.</span></span>  

<span data-ttu-id="3e3a9-246">인터넷 정보 서비스 내에서 서비스를 호스트하려면 개발자는 어셈블리의 기본 네임스페이스에 있는 Startup이라는 클래스를 사용하여 CLA 코드 라이브러리 어셈블리를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-246">To host the service within Internet Information Services, a developer would build a CLA code library assembly with a class named Startup in the default namespace of the assembly.</span></span>  <span data-ttu-id="3e3a9-247">이러한 클래스의 샘플은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-247">Here is a sample of such a class:</span></span> 

    public class Startup
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor and  
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter starter;

    public Startup()
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
          new DevelopersMonitor();
        Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
          new DevelopersProvider();
        this.starter = 
          new Microsoft.SystemForCrossDomainIdentityManagement.WebApplicationStarter(
            provider, 
            monitor);
    }

    public void Configuration(
      Owin.IAppBuilder builder) // Defined in in Owin.dll.  
    {
        this.starter.ConfigureApplication(builder);
    }
    }

### <a name="handling-endpoint-authentication"></a><span data-ttu-id="3e3a9-248">끝점 인증 처리</span><span class="sxs-lookup"><span data-stu-id="3e3a9-248">Handling endpoint authentication</span></span>
<span data-ttu-id="3e3a9-249">Azure Active Directory에서 요청은 OAuth 2.0 전달자 토큰을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-249">Requests from Azure Active Directory include an OAuth 2.0 bearer token.</span></span>   <span data-ttu-id="3e3a9-250">요청을 받는 모든 서비스는 예상된 Azure Active Directory 테넌트 대신 Azure Active Directory의 Graph 웹 서비스에 액세스하는 데 대해 발급자를 Azure Active Directory로 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-250">Any service receiving the request should authenticate the issuer as being Azure Active Directory on behalf of the expected Azure Active Directory tenant, for access to the Azure Active Directory Graph web service.</span></span>  <span data-ttu-id="3e3a9-251">토큰에서 발급자는 "iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/"와 같은 iss 클레임으로 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-251">In the token, the issuer is identified by an iss claim, like, "iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span></span>  <span data-ttu-id="3e3a9-252">이 예제에서 상대 주소 세그먼트인 cbb1a5ac-f33b-45fa-9bf5-f37db0fed422가 토큰이 발급된 대신 Azure Active Directory 테넌트의 고유한 발급자인 반면 클레임 값의 기본 주소인 https://sts.windows.net은 Azure Active Directory를 발급자로 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-252">In this example, the base address of the claim value, https://sts.windows.net, identifies Azure Active Directory as the issuer, while the relative address segment, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, is a unique identifier of the Azure Active Directory tenant on behalf of which the token was issued.</span></span>  <span data-ttu-id="3e3a9-253">토큰이 Azure Active Directory Graph 웹 서비스에 액세스하기 위해 발급되었다면 해당 서비스의 식별자인 00000002-0000-0000-c000-000000000000는 토큰의 aud 클레임의 값에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-253">If the token was issued for accessing the Azure Active Directory Graph web service, then the identifier of that service, 00000002-0000-0000-c000-000000000000, should be in the value of the token’s aud claim.</span></span>  

<span data-ttu-id="3e3a9-254">SCIM 서비스 구축을 위해 Microsoft에서 제공하는 CLA 라이브러리를 사용하는 개발자는 Microsoft.Owin.Security.ActiveDirectory 패키지로 다음 단계를 수행하여 Azure Active Directory에서 요청을 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-254">Developers using the CLA libraries provided by Microsoft for building a SCIM service can authenticate requests from Azure Active Directory using the Microsoft.Owin.Security.ActiveDirectory package by following these steps:</span></span> 

1. <span data-ttu-id="3e3a9-255">공급자에서 서비스가 시작할 때 마다 호출되는 메서드를 반환함으로써 Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior 속성을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-255">In a provider, implement the Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior property by having it return a method to be called whenever the service is started:</span></span> 

  ````
    public override Action\<Owin.IAppBuilder, System.Web.Http.HttpConfiguration.HttpConfiguration\> StartupBehavior
    {
      get
      {
        return this.OnServiceStartup;
      }
    }

    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder,  // Defined in Owin.dll.  
      System.Web.Http.HttpConfiguration configuration)  // Defined in System.Web.Http.dll.  
    {
    }
  ````

2. <span data-ttu-id="3e3a9-256">해당 메서드에 다음 코드를 추가하여 지정된 테넌트 대신 인증된 서비스의 끝점 중 하나가 Azure AD Graph 웹 서비스에 액세스하는 데 대해 Azure Active Directory에서 발급한 토큰을 갖도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-256">Add the following code to that method to have any request to any of the service’s endpoints authenticated as bearing a token issued by Azure Active Directory on behalf of a specified tenant, for access to the Azure AD Graph web service:</span></span> 

  ````
    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder IAppBuilder applicationBuilder, 
      System.Web.Http.HttpConfiguration HttpConfiguration configuration)
    {
      // IFilter is defined in System.Web.Http.dll.  
      System.Web.Http.Filters.IFilter authorizationFilter = 
        new System.Web.Http.AuthorizeAttribute(); // Defined in System.Web.Http.dll.configuration.Filters.Add(authorizationFilter);

      // SystemIdentityModel.Tokens.TokenValidationParameters is defined in    
      // System.IdentityModel.Token.Jwt.dll.
      SystemIdentityModel.Tokens.TokenValidationParameters tokenValidationParameters =     
        new TokenValidationParameters()
        {
          ValidAudience = "00000002-0000-0000-c000-000000000000"
        };

      // WindowsAzureActiveDirectoryBearerAuthenticationOptions is defined in 
      // Microsoft.Owin.Security.ActiveDirectory.dll
      Microsoft.Owin.Security.ActiveDirectory.
      WindowsAzureActiveDirectoryBearerAuthenticationOptions authenticationOptions =
        new WindowsAzureActiveDirectoryBearerAuthenticationOptions()    {
        TokenValidationParameters = tokenValidationParameters,
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute the appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a><span data-ttu-id="3e3a9-257">사용자 및 그룹 스키마</span><span class="sxs-lookup"><span data-stu-id="3e3a9-257">User and group schema</span></span>
<span data-ttu-id="3e3a9-258">Azure Active Directory는 두 형식의 리소스를 SCIM 웹 서비스에 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-258">Azure Active Directory can provision two types of resources to SCIM web services.</span></span>  <span data-ttu-id="3e3a9-259">이러한 형식의 리소스는 사용자 및 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-259">Those types of resources are users and groups.</span></span>  

<span data-ttu-id="3e3a9-260">사용자 리소스는 http://tools.ietf.org/html/draft-ietf-scim-core-schema 프로토콜 사양에 포함된 스키마 식별자 urn: ietf:params:scim:schemas:extension:enterprise:2.0:User로 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-260">User resources are identified by the schema identifier, urn:ietf:params:scim:schemas:extension:enterprise:2.0:User, which is included in this protocol specification: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span></span>  <span data-ttu-id="3e3a9-261">urn: ietf:params:scim:schemas:extension:enterprise:2.0:User 리소스의 특성에 Azure Active Directory에서 사용자의 특성을 기본 매핑한 작업은 아래 테이블 1에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-261">The default mapping of the attributes of users in Azure Active Directory to the attributes of urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resources is provided in table 1, below.</span></span>  

<span data-ttu-id="3e3a9-262">그룹 리소스는 스키마 식별자 http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group으로 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-262">Group resources are identified by the schema identifier, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  <span data-ttu-id="3e3a9-263">아래 표 2에서는 Azure Active Directory의 그룹 특성과 http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group resources 리소스 특성 간의 기본 매핑을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-263">Table 2, below, shows the default mapping of the attributes of groups in Azure Active Directory to the attributes of http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group resources.</span></span>  

### <a name="table-1-default-user-attribute-mapping"></a><span data-ttu-id="3e3a9-264">테이블 1: 기본 사용자 특성 매핑</span><span class="sxs-lookup"><span data-stu-id="3e3a9-264">Table 1: Default user attribute mapping</span></span>
| <span data-ttu-id="3e3a9-265">Azure Active Directory 사용자</span><span class="sxs-lookup"><span data-stu-id="3e3a9-265">Azure Active Directory user</span></span> | <span data-ttu-id="3e3a9-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span><span class="sxs-lookup"><span data-stu-id="3e3a9-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span></span> |
| --- | --- |
| <span data-ttu-id="3e3a9-267">IsSoftDeleted</span><span class="sxs-lookup"><span data-stu-id="3e3a9-267">IsSoftDeleted</span></span> |<span data-ttu-id="3e3a9-268">활성</span><span class="sxs-lookup"><span data-stu-id="3e3a9-268">active</span></span> |
| <span data-ttu-id="3e3a9-269">displayName</span><span class="sxs-lookup"><span data-stu-id="3e3a9-269">displayName</span></span> |<span data-ttu-id="3e3a9-270">displayName</span><span class="sxs-lookup"><span data-stu-id="3e3a9-270">displayName</span></span> |
| <span data-ttu-id="3e3a9-271">Facsimile-TelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="3e3a9-271">Facsimile-TelephoneNumber</span></span> |<span data-ttu-id="3e3a9-272">phoneNumbers[type eq "fax"].value</span><span class="sxs-lookup"><span data-stu-id="3e3a9-272">phoneNumbers[type eq "fax"].value</span></span> |
| <span data-ttu-id="3e3a9-273">givenName</span><span class="sxs-lookup"><span data-stu-id="3e3a9-273">givenName</span></span> |<span data-ttu-id="3e3a9-274">name.givenName</span><span class="sxs-lookup"><span data-stu-id="3e3a9-274">name.givenName</span></span> |
| <span data-ttu-id="3e3a9-275">jobTitle</span><span class="sxs-lookup"><span data-stu-id="3e3a9-275">jobTitle</span></span> |<span data-ttu-id="3e3a9-276">title</span><span class="sxs-lookup"><span data-stu-id="3e3a9-276">title</span></span> |
| <span data-ttu-id="3e3a9-277">mail</span><span class="sxs-lookup"><span data-stu-id="3e3a9-277">mail</span></span> |<span data-ttu-id="3e3a9-278">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="3e3a9-278">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="3e3a9-279">mailNickname</span><span class="sxs-lookup"><span data-stu-id="3e3a9-279">mailNickname</span></span> |<span data-ttu-id="3e3a9-280">externalId</span><span class="sxs-lookup"><span data-stu-id="3e3a9-280">externalId</span></span> |
| <span data-ttu-id="3e3a9-281">manager</span><span class="sxs-lookup"><span data-stu-id="3e3a9-281">manager</span></span> |<span data-ttu-id="3e3a9-282">manager</span><span class="sxs-lookup"><span data-stu-id="3e3a9-282">manager</span></span> |
| <span data-ttu-id="3e3a9-283">mobile</span><span class="sxs-lookup"><span data-stu-id="3e3a9-283">mobile</span></span> |<span data-ttu-id="3e3a9-284">phoneNumbers[type eq "mobile"].value</span><span class="sxs-lookup"><span data-stu-id="3e3a9-284">phoneNumbers[type eq "mobile"].value</span></span> |
| <span data-ttu-id="3e3a9-285">objectId</span><span class="sxs-lookup"><span data-stu-id="3e3a9-285">objectId</span></span> |<span data-ttu-id="3e3a9-286">id</span><span class="sxs-lookup"><span data-stu-id="3e3a9-286">id</span></span> |
| <span data-ttu-id="3e3a9-287">postalCode</span><span class="sxs-lookup"><span data-stu-id="3e3a9-287">postalCode</span></span> |<span data-ttu-id="3e3a9-288">addresses[type eq "work"].postalCode</span><span class="sxs-lookup"><span data-stu-id="3e3a9-288">addresses[type eq "work"].postalCode</span></span> |
| <span data-ttu-id="3e3a9-289">proxy-Addresses</span><span class="sxs-lookup"><span data-stu-id="3e3a9-289">proxy-Addresses</span></span> |<span data-ttu-id="3e3a9-290">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="3e3a9-290">emails[type eq "other"].Value</span></span> |
| <span data-ttu-id="3e3a9-291">physical-Delivery-OfficeName</span><span class="sxs-lookup"><span data-stu-id="3e3a9-291">physical-Delivery-OfficeName</span></span> |<span data-ttu-id="3e3a9-292">addresses[type eq "other"].Formatted</span><span class="sxs-lookup"><span data-stu-id="3e3a9-292">addresses[type eq "other"].Formatted</span></span> |
| <span data-ttu-id="3e3a9-293">streetAddress</span><span class="sxs-lookup"><span data-stu-id="3e3a9-293">streetAddress</span></span> |<span data-ttu-id="3e3a9-294">addresses[type eq "work"].streetAddress</span><span class="sxs-lookup"><span data-stu-id="3e3a9-294">addresses[type eq "work"].streetAddress</span></span> |
| <span data-ttu-id="3e3a9-295">surname</span><span class="sxs-lookup"><span data-stu-id="3e3a9-295">surname</span></span> |<span data-ttu-id="3e3a9-296">name.familyName</span><span class="sxs-lookup"><span data-stu-id="3e3a9-296">name.familyName</span></span> |
| <span data-ttu-id="3e3a9-297">telephone-Number</span><span class="sxs-lookup"><span data-stu-id="3e3a9-297">telephone-Number</span></span> |<span data-ttu-id="3e3a9-298">phoneNumbers[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="3e3a9-298">phoneNumbers[type eq "work"].value</span></span> |
| <span data-ttu-id="3e3a9-299">user-PrincipalName</span><span class="sxs-lookup"><span data-stu-id="3e3a9-299">user-PrincipalName</span></span> |<span data-ttu-id="3e3a9-300">userName</span><span class="sxs-lookup"><span data-stu-id="3e3a9-300">userName</span></span> |

### <a name="table-2-default-group-attribute-mapping"></a><span data-ttu-id="3e3a9-301">테이블 2: 기본 그룹 특성 매핑</span><span class="sxs-lookup"><span data-stu-id="3e3a9-301">Table 2: Default group attribute mapping</span></span>
| <span data-ttu-id="3e3a9-302">Azure Active Directory 그룹</span><span class="sxs-lookup"><span data-stu-id="3e3a9-302">Azure Active Directory group</span></span> | <span data-ttu-id="3e3a9-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span><span class="sxs-lookup"><span data-stu-id="3e3a9-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span></span> |
| --- | --- |
| <span data-ttu-id="3e3a9-304">displayName</span><span class="sxs-lookup"><span data-stu-id="3e3a9-304">displayName</span></span> |<span data-ttu-id="3e3a9-305">externalId</span><span class="sxs-lookup"><span data-stu-id="3e3a9-305">externalId</span></span> |
| <span data-ttu-id="3e3a9-306">mail</span><span class="sxs-lookup"><span data-stu-id="3e3a9-306">mail</span></span> |<span data-ttu-id="3e3a9-307">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="3e3a9-307">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="3e3a9-308">mailNickname</span><span class="sxs-lookup"><span data-stu-id="3e3a9-308">mailNickname</span></span> |<span data-ttu-id="3e3a9-309">displayName</span><span class="sxs-lookup"><span data-stu-id="3e3a9-309">displayName</span></span> |
| <span data-ttu-id="3e3a9-310">members</span><span class="sxs-lookup"><span data-stu-id="3e3a9-310">members</span></span> |<span data-ttu-id="3e3a9-311">members</span><span class="sxs-lookup"><span data-stu-id="3e3a9-311">members</span></span> |
| <span data-ttu-id="3e3a9-312">objectId</span><span class="sxs-lookup"><span data-stu-id="3e3a9-312">objectId</span></span> |<span data-ttu-id="3e3a9-313">id</span><span class="sxs-lookup"><span data-stu-id="3e3a9-313">id</span></span> |
| <span data-ttu-id="3e3a9-314">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="3e3a9-314">proxyAddresses</span></span> |<span data-ttu-id="3e3a9-315">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="3e3a9-315">emails[type eq "other"].Value</span></span> |

## <a name="user-provisioning-and-de-provisioning"></a><span data-ttu-id="3e3a9-316">사용자 프로비저닝 및 프로비전 해제</span><span class="sxs-lookup"><span data-stu-id="3e3a9-316">User provisioning and de-provisioning</span></span>
<span data-ttu-id="3e3a9-317">다음 일러스트레이션은 다른 ID 저장소에 사용자의 수명 주기를 관리하도록 Azure Active Directory가 SCIM 서비스를 보낸다는 메시지를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-317">The following illustration shows the messages that Azure Active Directory sends to a SCIM service to manage the lifecycle of a user in another identity store.</span></span> <span data-ttu-id="3e3a9-318">또한 다이어그램은 이러한 서비스 구축을 위해 Microsoft에서 제공하는 CLI 라이브러리를 사용하여 구현된 SCIM 서비스가 이러한 요청을 어떻게 공급자의 메서드에 호출로 번역하는지를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-318">The diagram also shows how a SCIM service implemented using the CLI libraries provided by Microsoft for building such services translate those requests into calls to the methods of a provider.</span></span>  

<span data-ttu-id="3e3a9-319">![][4]
*그림 5: 사용자 프로비저닝 및 시퀀스 프로비전 해제*</span><span class="sxs-lookup"><span data-stu-id="3e3a9-319">![][4]
*Figure 5: User provisioning and de-provisioning sequence*</span></span>

1. <span data-ttu-id="3e3a9-320">Azure Active Directory는 externalId 특성 값이 Azure AD의 사용자 mailNickname 특성 값과 일치하는 사용자를 서비스에 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-320">Azure Active Directory queries the service for a user with an externalId attribute value matching the mailNickname attribute value of a user in Azure AD.</span></span> <span data-ttu-id="3e3a9-321">쿼리는 이 예제처럼 HTTP(Hypertext Transfer Protocol) 요청으로 표현되며, 여기서 jyoung은 Azure Active Directory에서 사용자의 mailNickname 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-321">The query is expressed as a Hypertext Transfer Protocol (HTTP) request such as this example, wherein jyoung is a sample of a mailNickname of a user in Azure Active Directory:</span></span> 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="3e3a9-322">서비스가 SCIM 서비스 구현에 대해 Microsoft에서 제공하는 공용 언어 인프라 라이브러리를 사용하여 작성되면 요청이 서비스 공급자의 쿼리 메서드 호출로 번역됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-322">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Query method of the service’s provider.</span></span>  <span data-ttu-id="3e3a9-323">해당 메서드의 서명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-323">Here is the signature of that method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Protocol.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource[]> Query(
      Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters parameters, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="3e3a9-324">Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters 인터페이스의 정의는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-324">Here is the definition of the Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters interface:</span></span> 
  ````
    public interface IQueryParameters: 
      Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
        System.Collections.Generic.IReadOnlyCollection <Microsoft.SystemForCrossDomainIdentityManagement.IFilter> AlternateFilters 
        { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
      system.Collections.Generic.IReadOnlyCollection<string> ExcludedAttributePaths 
      { get; }
      System.Collections.Generic.IReadOnlyCollection<string> RequestedAttributePaths 
      { get; }
      string SchemaIdentifier 
      { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IFilter
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IFilter AdditionalFilter 
          { get; set; }
        string AttributePath 
          { get; } 
        Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator FilterOperator 
          { get; }
        string ComparisonValue 
          { get; }
    }

    public enum Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator
    {
        Equals
    }
  ````
  <span data-ttu-id="3e3a9-325">externalId 특성의 값이 지정된 사용자에 대한 다음 쿼리 샘플에서 쿼리 메서드에 전달된 인수의 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-325">In the following sample of a query for a user with a given value for the externalId attribute, values of the arguments passed to the Query method are:</span></span> 
  * <span data-ttu-id="3e3a9-326">parameters.AlternateFilters.Count: 1</span><span class="sxs-lookup"><span data-stu-id="3e3a9-326">parameters.AlternateFilters.Count: 1</span></span>
  * <span data-ttu-id="3e3a9-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span><span class="sxs-lookup"><span data-stu-id="3e3a9-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span></span>
  * <span data-ttu-id="3e3a9-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="3e3a9-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="3e3a9-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span><span class="sxs-lookup"><span data-stu-id="3e3a9-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span></span>
  * <span data-ttu-id="3e3a9-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span><span class="sxs-lookup"><span data-stu-id="3e3a9-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span></span> 

2. <span data-ttu-id="3e3a9-331">externalId 특성 값이 사용자의 mailNickname 특성 값과 일치하는 사용자를 웹 서비스에 쿼리할 때 응답으로 사용자가 반환되지 않는 경우 Azure Active Directory는 서비스가 Azure Active Directory의 사용자에 해당하는 사용자를 프로비전하도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-331">If the response to a query to the web service for a user with an externalId attribute value that matches the mailNickname attribute value of a user does not return any users, then Azure Active Directory requests that the service provision a user corresponding to the one in Azure Active Directory.</span></span>  <span data-ttu-id="3e3a9-332">다음은 그러한 요청의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-332">Here is an example of such a request:</span></span> 
  ````
    POST https://.../scim/Users HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas":
      [
        "urn:ietf:params:scim:schemas:core:2.0:User",
        "urn:ietf:params:scim:schemas:extension:enterprise:2.0User"],
      "externalId":"jyoung",
      "userName":"jyoung",
      "active":true,
      "addresses":null,
      "displayName":"Joy Young",
      "emails": [
        {
          "type":"work",
          "value":"jyoung@Contoso.com",
          "primary":true}],
      "meta": {
        "resourceType":"User"},
       "name":{
        "familyName":"Young",
        "givenName":"Joy"},
      "phoneNumbers":null,
      "preferredLanguage":null,
      "title":null,
      "department":null,
      "manager":null}
  ````
  <span data-ttu-id="3e3a9-333">SCIM 서비스 구현에 대해 Microsoft에서 제공하는 공용 언어 인프라 라이브러리는 요청이 서비스 공급자의 만들기 메서드에 호출을 요청하도록 번역됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-333">The Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services would translate that request into a call to the Create method of the service’s provider.</span></span>  <span data-ttu-id="3e3a9-334">만들기 메서드에는 다음 서명이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-334">The Create method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="3e3a9-335">사용자를 프로비전하는 요청에서 리소스 인수의 값은 Microsoft.SystemForCrossDomainIdentityManagement의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-335">In a request to provision a user, the value of the resource argument is an instance of the Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="3e3a9-336">Microsoft.SystemForCrossDomainIdentityManagement.Schemas 라이브러리에 정의된 Core2EnterpriseUser 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-336">Core2EnterpriseUser class, defined in the Microsoft.SystemForCrossDomainIdentityManagement.Schemas library.</span></span>  <span data-ttu-id="3e3a9-337">사용자를 프로비전하는 요청이 성공하는 경우 메서드의 구현은 Microsoft.SystemForCrossDomainIdentityManagement의 인스턴스를 반환할 것으로 예상됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-337">If the request to provision the user succeeds, then the implementation of the method is expected to return an instance of the Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="3e3a9-338">새로 프로비전된 사용자의 고유 식별자에 설정된 식별자 속성의 값을 가진 Core2EnterpriseUser 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-338">Core2EnterpriseUser class, with the value of the Identifier property set to the unique identifier of the newly provisioned user.</span></span>  

3. <span data-ttu-id="3e3a9-339">SCIM에 의해 제어되는 ID 저장소에 있는 것으로 알려진 사용자를 업데이트하기 위해 Azure Active Directory는 다음과 같은 요청으로 서비스에서 해당 사용자의 현재 상태를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-339">To update a user known to exist in an identity store fronted by an SCIM, Azure Active Directory proceeds by requesting the current state of that user from the service with a request such as:</span></span> 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="3e3a9-340">SCIM 서비스 구현에 대해 Microsoft에서 제공하는 공용 언어 인프라 라이브러리를 사용하여 작성된 서비스에서 요청은 서비스 공급자의 검색 메서드에 호출하도록 번역됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-340">In a service built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, the request is translated into a call to the Retrieve method of the service’s provider.</span></span>  <span data-ttu-id="3e3a9-341">해당 검색 메서드의 서명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-341">Here is the signature of the Retrieve method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource and 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
    // are defined in Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> 
       Retrieve(
         Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
           parameters, 
           string correlationIdentifier);

    public interface 
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters:   
        IRetrievalParameters
        {
          Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
            ResourceIdentifier 
              { get; }
    }
    public interface Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier
    {
        string Identifier 
          { get; set; }
        string Microsoft.SystemForCrossDomainIdentityManagement.SchemaIdentifier 
          { get; set; }
    }
  ````
  <span data-ttu-id="3e3a9-342">사용자의 현재 상태를 검색하는 요청 예제에서 매개 변수 인수 값으로 제공되는 개체의 속성 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-342">In the example of a request to retrieve the current state of a user, the values of the properties of the object provided as the value of the parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="3e3a9-343">식별자: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="3e3a9-343">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="3e3a9-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="3e3a9-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

4. <span data-ttu-id="3e3a9-345">참조 특성을 업데이트해야 하는 경우 Azure Active Directory는 서비스를 쿼리하여 서비스에 의해 제어되는 ID 저장소에 있는 참조 특성의 현재 값이 Azure Active Directory의 해당 특성 값과 이미 일치하는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-345">If a reference attribute is to be updated, then Azure Active Directory queries the service to determine whether or not the current value of the reference attribute in the identity store fronted by the service already matches the value of that attribute in Azure Active Directory.</span></span> <span data-ttu-id="3e3a9-346">사용자의 경우 현재 값이 이 방식으로 쿼리된 유일한 특성은 관리자 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-346">For users, the only attribute of which the current value is queried in this way is the manager attribute.</span></span> <span data-ttu-id="3e3a9-347">특정 사용자 개체의 관리자 특성 값에 현재 특정 값이 있는지 여부를 결정하는 요청의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-347">Here is an example of a request to determine whether the manager attribute of a particular user object currently has a certain value:</span></span> 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="3e3a9-348">특성 쿼리 매개 변수인 ID의 값은 필터 쿼리 매개 변수의 값으로 제공되는 식을 만족하는 사용자 개체가 있다는 것을 의미하고 서비스는 해당 리소스 ID 특성의 값을 포함하는 urn:ietf:params:scim:schemas:core:2.0:User or urn:ietf:params:scim:schemas:extension:enterprise:2.0:User 리소스를 사용하여 응답할 것으로 예상됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-348">The value of the attributes query parameter, id, signifies that if a user object exists that satisfies the expression provided as the value of the filter query parameter, then the service is expected to respond with a urn:ietf:params:scim:schemas:core:2.0:User or urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resource, including only the value of that resource’s id attribute.</span></span>  <span data-ttu-id="3e3a9-349">**id** 특성 값은 요청자에게 알려집니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-349">The value of the **id** attribute is known to the requestor.</span></span> <span data-ttu-id="3e3a9-350">이 값은 필터 쿼리 매개 변수의 값에 포함되며, 이 값을 묻는 목적은 실제로 이러한 개체의 존재 여부를 확인하는 필터 식을 만족하는 리소스의 최소 표현을 요청하기 위함입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-350">It is included in the value of the filter query parameter; the purpose of asking for it is actually to request a minimal representation of a resource that satisfying the filter expression as an indication of whether or not any such object exists.</span></span>   

  <span data-ttu-id="3e3a9-351">서비스가 SCIM 서비스 구현에 대해 Microsoft에서 제공하는 공용 언어 인프라 라이브러리를 사용하여 작성되면 요청이 서비스 공급자의 쿼리 메서드 호출로 번역됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-351">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Query method of the service’s provider.</span></span> <span data-ttu-id="3e3a9-352">매개 변수 인수의 값으로 제공되는 개체의 속성 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-352">The value of the properties of the object provided as the value of the parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="3e3a9-353">parameters.AlternateFilters.Count: 2</span><span class="sxs-lookup"><span data-stu-id="3e3a9-353">parameters.AlternateFilters.Count: 2</span></span>
  * <span data-ttu-id="3e3a9-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span><span class="sxs-lookup"><span data-stu-id="3e3a9-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span></span>
  * <span data-ttu-id="3e3a9-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="3e3a9-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="3e3a9-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="3e3a9-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="3e3a9-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="3e3a9-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span></span>
  * <span data-ttu-id="3e3a9-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="3e3a9-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="3e3a9-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span><span class="sxs-lookup"><span data-stu-id="3e3a9-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span></span>
  * <span data-ttu-id="3e3a9-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span><span class="sxs-lookup"><span data-stu-id="3e3a9-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span></span>
  * <span data-ttu-id="3e3a9-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="3e3a9-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

  <span data-ttu-id="3e3a9-362">여기에서 필터 쿼리 매개 변수 식의 순서에 따라 인덱스 x의 값은 0이고 인덱스 y의 값은 1일 수 있습니다. 또는 x 값이 1이고 y 값이 0일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-362">Here, the value of the index x may be 0 and the value of the index y may be 1, or the value of x may be 1 and the value of y may be 0, depending on the order of the expressions of the filter query parameter.</span></span>   

5. <span data-ttu-id="3e3a9-363">다음은 Azure Active Directory에서 SCIM 서비스로 사용자를 업데이트하는 요청의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-363">Here is an example of a request from Azure Active Directory to an SCIM service to update a user:</span></span> 
  ````
    PATCH ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas": 
      [
        "urn:ietf:params:scim:api:messages:2.0:PatchOp"],
      "Operations":
      [
        {
          "op":"Add",
          "path":"manager",
          "value":
            [
              {
                "$ref":"http://.../scim/Users/2819c223-7f76-453a-919d-413861904646",
                "value":"2819c223-7f76-453a-919d-413861904646"}]}]}
  ````
  <span data-ttu-id="3e3a9-364">SCIM 서비스 구현에 대한 Microsoft 공용 언어 인프라 라이브러리는 요청이 서비스 공급자의 업데이트 메서드에 호출을 요청하도록 번역됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-364">The Microsoft Common Language Infrastructure libraries for implementing SCIM services would translate the request into a call to the Update method of the service’s provider.</span></span> <span data-ttu-id="3e3a9-365">Update 메서드의 서명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-365">Here is the signature of the Update method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks and 
    // System.Collections.Generic.IReadOnlyCollection<T>
    // are defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IPatch, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation, 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationName, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IPath and 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationValue 
    // are all defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 

    System.Threading.Tasks.Task Update(
      Microsoft.SystemForCrossDomainIdentityManagement.IPatch patch, 
      string correlationIdentifier);

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IPatch
    {
    Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase 
      PatchRequest 
        { get; set; }
    Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
      ResourceIdentifier 
        { get; set; }        
    }

    public class PatchRequest2: 
      Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase
    {
    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation> 
        Operations
        { get;}

    public void AddOperation(
      Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation operation);
    }

    public class PatchOperation
    {
    public Microsoft.SystemForCrossDomainIdentityManagement.OperationName 
      Name
      { get; set; }

    public Microsoft.SystemForCrossDomainIdentityManagement.IPath 
      Path
      { get; set; }

    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.OperationValue> Value
      { get; }

    public void AddValue(
      Microsoft.SystemForCrossDomainIdentityManagement.OperationValue value);
    }

    public enum OperationName
    {
      Add,
      Remove,
      Replace
    }

    public interface IPath
    {
      string AttributePath { get; }
      System.Collections.Generic.IReadOnlyCollection<IFilter> SubAttributes { get; }
      Microsoft.SystemForCrossDomainIdentityManagement.IPath ValuePath { get; }
    }

    public class OperationValue
    {
      public string Reference
      { get; set; }

      public string Value
      { get; set; }
    }
  ````
    <span data-ttu-id="3e3a9-366">사용자를 업데이트하는 요청의 예에서 패치 인수의 값으로 제공되는 개체는 다음과 같은 속성 값이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-366">In the example of a request to update a user, the object provided as the value of the patch argument has these property values:</span></span> 
  
  * <span data-ttu-id="3e3a9-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="3e3a9-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="3e3a9-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="3e3a9-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>
  * <span data-ttu-id="3e3a9-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span><span class="sxs-lookup"><span data-stu-id="3e3a9-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span></span>
  * <span data-ttu-id="3e3a9-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span><span class="sxs-lookup"><span data-stu-id="3e3a9-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span></span>
  * <span data-ttu-id="3e3a9-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="3e3a9-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span></span>
  * <span data-ttu-id="3e3a9-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span><span class="sxs-lookup"><span data-stu-id="3e3a9-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span></span>
  * <span data-ttu-id="3e3a9-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="3e3a9-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span></span>
  * <span data-ttu-id="3e3a9-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="3e3a9-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span></span>

6. <span data-ttu-id="3e3a9-375">SCIM 서비스에 의해 제어되는 ID 저장소에서 사용자의 프로비전을 해제하기 위해 Azure AD에서 다음과 같은 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-375">To de-provision a user from an identity store fronted by an SCIM service, Azure AD sends a request such as:</span></span> 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="3e3a9-376">서비스가 SCIM 서비스 구현에 대해 Microsoft에서 제공하는 공용 언어 인프라 라이브러리를 사용하여 작성되면 요청이 서비스 공급자의 삭제 메서드 호출로 번역됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-376">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Delete method of the service’s provider.</span></span>   <span data-ttu-id="3e3a9-377">해당 메서드에는 다음 서명이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-377">That method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="3e3a9-378">사용자의 프로비전을 해제하는 요청의 예에서 resourceIdentifier 인수의 값으로 제공되는 개체는 다음과 같은 속성 값이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-378">The object provided as the value of the resourceIdentifier argument has these property values in the example of a request to de-provision a user:</span></span> 
  
  * <span data-ttu-id="3e3a9-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="3e3a9-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="3e3a9-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="3e3a9-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

## <a name="group-provisioning-and-de-provisioning"></a><span data-ttu-id="3e3a9-381">그룹 프로비전 및 프로비전 해제</span><span class="sxs-lookup"><span data-stu-id="3e3a9-381">Group provisioning and de-provisioning</span></span>
<span data-ttu-id="3e3a9-382">다음 일러스트레이션은 다른 ID 저장소에 그룹의 수명 주기를 관리하도록 Azure AD가 SCIM 서비스를 보낸다는 메시지를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-382">The following illustration shows the messages that Azure AcD sends to a SCIM service to manage the lifecycle of a group in another identity store.</span></span>  <span data-ttu-id="3e3a9-383">이러한 메시지는 세 가지 부분에서 사용자에 관련된 메시지가 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-383">Those messages differ from the messages pertaining to users in three ways:</span></span> 

* <span data-ttu-id="3e3a9-384">그룹 리소스의 스키마는 http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group으로 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-384">The schema of a group resource is identified as http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  
* <span data-ttu-id="3e3a9-385">그룹을 검색하는 요청은 멤버 특성이 요청에 대한 응답에서 제공된 리소스로부터 제외된다고 규정합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-385">Requests to retrieve groups stipulate that the members attribute is to be excluded from any resource provided in response to the request.</span></span>  
* <span data-ttu-id="3e3a9-386">참조 특성에 특정 값이 있는지를 확인하는 요청은 멤버 특성에 대한 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3a9-386">Requests to determine whether a reference attribute has a certain value are requests about the members attribute.</span></span>  

<span data-ttu-id="3e3a9-387">![][5]
*그림 6: 그룹 프로비전 및 시퀀스 프로비전 해제*</span><span class="sxs-lookup"><span data-stu-id="3e3a9-387">![][5]
*Figure 6: Group provisioning and de-provisioning sequence*</span></span>

## <a name="related-articles"></a><span data-ttu-id="3e3a9-388">관련 문서</span><span class="sxs-lookup"><span data-stu-id="3e3a9-388">Related articles</span></span>
* [<span data-ttu-id="3e3a9-389">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="3e3a9-389">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="3e3a9-390">SaaS 앱에 자동화된 사용자 프로비전/프로비전 해제</span><span class="sxs-lookup"><span data-stu-id="3e3a9-390">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="3e3a9-391">사용자 프로비저닝에 대한 특성 매핑 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="3e3a9-391">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="3e3a9-392">특성 매핑에 대한 식 작성</span><span class="sxs-lookup"><span data-stu-id="3e3a9-392">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="3e3a9-393">사용자 프로 비전에 대 한 필터 범위 지정</span><span class="sxs-lookup"><span data-stu-id="3e3a9-393">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="3e3a9-394">계정 프로비전 알림</span><span class="sxs-lookup"><span data-stu-id="3e3a9-394">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="3e3a9-395">SaaS App을 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="3e3a9-395">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG
