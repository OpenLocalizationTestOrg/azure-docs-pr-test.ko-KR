---
title: "도메인 간 Id 관리를 위한 시스템 aaaUsing 자동으로 프로 비전 tooapplications Azure Active Directory에서에서 사용자 및 그룹 | Microsoft Docs"
description: "Azure Active Directory 사용자 및 그룹 tooany 응용 프로그램 또는 id 저장소는 프런트 웹 서비스에 의해 hello SCIM 프로토콜 사양에에서 정의 된 hello 인터페이스와 자동으로 구축할 수 있습니다."
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
ms.openlocfilehash: 43045c97e68d0d22db598dcb5ec23481c4e97718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-system-for-cross-domain-identity-management-tooautomatically-provision-users-and-groups-from-azure-active-directory-tooapplications"></a><span data-ttu-id="e3202-103">도메인 간 Id 관리 tooautomatically 사용자 프로 비전 및 Azure Active Directory tooapplications에서 그룹에 대 한 시스템을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e3202-103">Using System for Cross-Domain Identity Management tooautomatically provision users and groups from Azure Active Directory tooapplications</span></span>

## <a name="overview"></a><span data-ttu-id="e3202-104">개요</span><span class="sxs-lookup"><span data-stu-id="e3202-104">Overview</span></span>
<span data-ttu-id="e3202-105">Azure Active Directory (Azure AD)에 사용자와 그룹 tooany 응용 프로그램 또는 id 저장소는 프런트 웹 서비스에 의해 hello에 정의 된 hello 인터페이스와 자동으로 구축할 수 [시스템 도메인 간 Identity Management (SCIM) 2.0 프로토콜 사양](https://tools.ietf.org/html/draft-ietf-scim-api-19)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-105">Azure Active Directory (Azure AD) can automatically provision users and groups tooany application or identity store that is fronted by a web service with hello interface defined in hello [System for Cross-Domain Identity Management (SCIM) 2.0 protocol specification](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span></span> <span data-ttu-id="e3202-106">Azure Active Directory toocreate 요청을 보낼 수 있습니다, 그리고 수정 또는 할당 된 사용자 및 그룹 toohello 웹 서비스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-106">Azure Active Directory can send requests toocreate, modify, or delete assigned users and groups toohello web service.</span></span> <span data-ttu-id="e3202-107">그런 다음 hello 웹 서비스 hello 대상 id 저장소에 대 한 작업으로 이러한 요청을 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-107">hello web service can then translate those requests into operations on hello target identity store.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="e3202-108">Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 



<span data-ttu-id="e3202-109">![][0]
*그림 1: 웹 서비스를 통해 Azure Active Directory tooan id 저장소에서 프로 비전*</span><span class="sxs-lookup"><span data-stu-id="e3202-109">![][0]
*Figure 1: Provisioning from Azure Active Directory tooan identity store via a web service*</span></span>

<span data-ttu-id="e3202-110">Azure AD tooenable single sign on 및 자동 사용자 프로 비전을 제공 하거나 SCIM 웹 서비스에 의해 프런트 되는 응용 프로그램에 hello "앱을 직접 bring" 기능을 함께에서이 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-110">This capability can be used in conjunction with hello “bring your own app” capability in Azure AD tooenable single sign-on and automatic user provisioning for applications that provide or are fronted by a SCIM web service.</span></span>

<span data-ttu-id="e3202-111">Azure Active Directory에서 SCIM을 사용하는 방법에 대한 두 가지 사용 사례가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-111">There are two use cases for using SCIM in Azure Active Directory:</span></span>

* <span data-ttu-id="e3202-112">**지 원하는 SCIM tooapplications 사용자 및 그룹을 프로 비전** SCIM 2.0을 지원 하 고 구성 없이 Azure AD와 작동 하는 인증에 대 한 OAuth 전달자 토큰을 사용 하는 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-112">**Provisioning users and groups tooapplications that support SCIM** Applications that support SCIM 2.0 and use OAuth bearer tokens for authentication works with Azure AD without configuration.</span></span>
* <span data-ttu-id="e3202-113">**다른 API 기반 프로 비전을 지원 되는 응용 프로그램에 대 한 프로 비전 솔루션을 빌드합니다** SCIM 아닌 응용 프로그램에 대 한 모든 API hello 응용 프로그램에서는 hello Azure AD SCIM 끝점 사이의 SCIM 끝점 tootranslate를 만들 수 있습니다 사용자 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-113">**Build your own provisioning solution for applications that support other API-based provisioning** For non-SCIM applications, you can create a SCIM endpoint tootranslate between hello Azure AD SCIM endpoint and any API hello application supports for user provisioning.</span></span> <span data-ttu-id="e3202-114">toohelp SCIM 끝점을 개발, toodo SCIM 끝점을 제공 하 고 SCIM 메시지를 변환 하는 방법을 보여 주는 코드 예제와 함께 공용 언어 인프라 (CLI) 라이브러리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-114">toohelp you develop a SCIM endpoint, we provide Common Language Infrastructure (CLI) libraries along with code samples that show you how toodo provide a SCIM endpoint and translate SCIM messages.</span></span>  

## <a name="provisioning-users-and-groups-tooapplications-that-support-scim"></a><span data-ttu-id="e3202-115">사용자 및 그룹 tooapplications SCIM 지 프로 비전</span><span class="sxs-lookup"><span data-stu-id="e3202-115">Provisioning users and groups tooapplications that support SCIM</span></span>
<span data-ttu-id="e3202-116">Azure AD 구성된 tooautomatically 프로 비전 할당 된 사용자 및 그룹 tooapplications 구현 하는 수는 [도메인 간 Id 관리 2 (SCIM)에 대 한 시스템](https://tools.ietf.org/html/draft-ietf-scim-api-19) 웹 서비스 및 인증에 대 한 OAuth 전달자 토큰을 수락 .</span><span class="sxs-lookup"><span data-stu-id="e3202-116">Azure AD can be configured tooautomatically provision assigned users and groups tooapplications that implement a [System for Cross-domain Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) web service and accept OAuth bearer tokens for authentication.</span></span> <span data-ttu-id="e3202-117">Hello SCIM 2.0 사양 내에서 응용 프로그램에는 이러한 요구 사항을 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-117">Within hello SCIM 2.0 specification, applications must meet these requirements:</span></span>

* <span data-ttu-id="e3202-118">사용자 및/또는 hello SCIM 프로토콜 섹션 3.3에 따라 그룹 만들기를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-118">Supports creating users and/or groups, as per section 3.3 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="e3202-119">사용자 및/또는 패치 요청 hello SCIM 프로토콜의 3.5.2 섹션에 따라 그룹 수정을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-119">Supports modifying users and/or groups with patch requests as per section 3.5.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="e3202-120">3.4.1 hello SCIM 프로토콜의 섹션에 따라 알려진된 리소스 검색을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-120">Supports retrieving a known resource as per section 3.4.1 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="e3202-121">사용자 및/또는 그룹의 hello SCIM 프로토콜 3.4.2 섹션에 따라 쿼리를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-121">Supports querying users and/or groups, as per section 3.4.2 of hello SCIM protocol.</span></span>  <span data-ttu-id="e3202-122">기본적으로 사용자는 externalId에서 쿼리되고 그룹은 displayName에서 쿼리됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-122">By default, users are queried by externalId and groups are queried by displayName.</span></span>  
* <span data-ttu-id="e3202-123">3.4.2 hello SCIM 프로토콜의 섹션에 따라 관리자가 사용자 ID로 쿼리를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-123">Supports querying user by ID and by manager as per section 3.4.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="e3202-124">그룹 및 섹션 3.4.2 hello SCIM 프로토콜에 따라 멤버 ID 별로 쿼리를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-124">Supports querying groups by ID and by member as per section 3.4.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="e3202-125">Hello SCIM 프로토콜의 섹션 2.1에 따라 권한 부여에 대 한 OAuth 전달자 토큰을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-125">Accepts OAuth bearer tokens for authorization as per section 2.1 of hello SCIM protocol.</span></span>

<span data-ttu-id="e3202-126">응용 프로그램 공급자 또는 응용 프로그램 공급자의 설명서를 통해 이러한 요구 사항과의 호환성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-126">Check with your application provider, or your application provider's documentation for statements of compatibility with these requirements.</span></span>

### <a name="getting-started"></a><span data-ttu-id="e3202-127">시작</span><span class="sxs-lookup"><span data-stu-id="e3202-127">Getting started</span></span>
<span data-ttu-id="e3202-128">이 문서에 설명 된 hello SCIM 프로필을 지 원하는 응용 프로그램에 연결 된 tooAzure Active Directory 수 hello Azure AD 응용 프로그램 갤러리에서 hello "갤러리 아닌 응용 프로그램" 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-128">Applications that support hello SCIM profile described in this article can be connected tooAzure Active Directory using hello "non-gallery application" feature in hello Azure AD application gallery.</span></span> <span data-ttu-id="e3202-129">연결 된, Azure AD에서 실행 되 면 동기화 프로세스에 대 한 hello 응용 프로그램의 SCIM 끝점을 쿼리하여 여기서 20 분 마다 사용자 및 그룹을 할당 하 고 만들거나 toohello 할당 세부 정보에 따라 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-129">Once connected, Azure AD runs a synchronization process every 20 minutes where it queries hello application's SCIM endpoint for assigned users and groups, and creates or modifies them according toohello assignment details.</span></span>

<span data-ttu-id="e3202-130">**tooconnect SCIM를 지 원하는 응용 프로그램:**</span><span class="sxs-lookup"><span data-stu-id="e3202-130">**tooconnect an application that supports SCIM:**</span></span>

1. <span data-ttu-id="e3202-131">역시 로그인[Azure 포털 hello](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-131">Sign in too[hello Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="e3202-132">너무 찾아보기 * * Azure Active Directory > 엔터프라이즈 응용 프로그램 및 선택 **새 응용 프로그램 > 모든 > 비 갤러리 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-132">Browse too**Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="e3202-133">응용 프로그램에 대 한 이름을 입력 하 고 클릭 **추가** 아이콘 toocreate 응용 프로그램 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-133">Enter a name for your application, and click **Add** icon toocreate an app object.</span></span>
    
  <span data-ttu-id="e3202-134">![][1]
  *그림 2: Azure AD 응용 프로그램 갤러리*</span><span class="sxs-lookup"><span data-stu-id="e3202-134">![][1]
*Figure 2: Azure AD application gallery*</span></span>
    
4. <span data-ttu-id="e3202-135">Hello 결과 화면에서 선택 hello **프로 비전** hello 왼쪽된 열에는 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-135">In hello resulting screen, select hello **Provisioning** tab in hello left column.</span></span>
5. <span data-ttu-id="e3202-136">Hello에 **프로 비전 모드** 메뉴 선택 **자동**합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-136">In hello **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="e3202-137">![][2]
  *그림 3: hello Azure 포털에서에서 프로 비전 구성*</span><span class="sxs-lookup"><span data-stu-id="e3202-137">![][2]
*Figure 3: Configuring provisioning in hello Azure portal*</span></span>
    
6. <span data-ttu-id="e3202-138">Hello에 **테 넌 트 URL** 필드 hello 응용 프로그램의 SCIM 끝점의 hello URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-138">In hello **Tenant URL** field, enter hello URL of hello application's SCIM endpoint.</span></span> <span data-ttu-id="e3202-139">예: https://api.contoso.com/scim/v2/</span><span class="sxs-lookup"><span data-stu-id="e3202-139">Example: https://api.contoso.com/scim/v2/</span></span>
7. <span data-ttu-id="e3202-140">Hello SCIM 끝점 Azure AD 이외의 발급자 로부터 OAuth 전달자 토큰에 필요한 경우 복사 hello 선택적 hello에 OAuth 전달자 토큰을 필요한 **암호 토큰** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-140">If hello SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy hello required OAuth bearer token into hello optional **Secret Token** field.</span></span> <span data-ttu-id="e3202-141">이 필드를 비워 두면 Azure AD에 각 요청에 따라 Azure AD에서 발급한 OAuth 전달자 토큰이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-141">If this field is left blank, then Azure AD included an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="e3202-142">ID 공급자로 Azure AD를 사용하는 앱은 Azure AD에서 발급한 토큰의 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-142">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="e3202-143">Hello 클릭 **연결 테스트** 단추 toohave Azure Active Directory 시도 tooconnect toohello SCIM 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-143">Click hello **Test Connection** button toohave Azure Active Directory attempt tooconnect toohello SCIM endpoint.</span></span> <span data-ttu-id="e3202-144">Hello 시도가 실패 한 경우 오류 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-144">If hello attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="e3202-145">Hello 시도 tooconnect toohello 응용 프로그램 성공 하는 경우 클릭 **저장** toosave hello에 대 한 관리자 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-145">If hello attempts tooconnect toohello application succeed, then click **Save** toosave hello admin credentials.</span></span>
10. <span data-ttu-id="e3202-146">Hello에 **매핑** 섹션에서 두 개의 선택할 수 있는 특성 매핑 집합이: 사용자 개체 및 그룹 개체에 대 한 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-146">In hello **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="e3202-147">Azure Active Directory tooyour 응용 프로그램에서 동기화 되는 각 하나의 tooreview hello 특성을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-147">Select each one tooreview hello attributes that are synchronized from Azure Active Directory tooyour app.</span></span> <span data-ttu-id="e3202-148">특성으로 선택 된 hello **일치** 속성은 업데이트 작업에 대 한 응용 프로그램에서 사용 되는 toomatch hello 사용자 및 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-148">hello attributes selected as **Matching** properties are used toomatch hello users and groups in your app for update operations.</span></span> <span data-ttu-id="e3202-149">변경 내용을 저장 단추 toocommit hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-149">Select hello Save button toocommit any changes.</span></span>

    >[!NOTE]
    ><span data-ttu-id="e3202-150">필요에 따라 hello "groups" 매핑을 해제 하 여 그룹 개체의 동기화를 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-150">You can optionally disable syncing of group objects by disabling hello "groups" mapping.</span></span> 

11. <span data-ttu-id="e3202-151">아래 **설정**, hello **범위** 사용자 및 그룹 동기화 되는 또는 필드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-151">Under **Settings**, hello **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="e3202-152">Hello에 할당 사용자 및 그룹에만 동기화 합니다 "동기화만 할당 된 사용자 및 그룹" (권장)을 선택 하면 **사용자 및 그룹** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-152">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in hello **Users and groups** tab.</span></span>
12. <span data-ttu-id="e3202-153">구성을 완료 되 면 변경 hello **프로 비전 상태** 너무**에**합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-153">Once your configuration is complete, change hello **Provisioning Status** too**On**.</span></span>
13. <span data-ttu-id="e3202-154">클릭 **저장** toostart hello Azure AD에 프로 비전 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-154">Click **Save** toostart hello Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="e3202-155">사용자 및 그룹 (권장) 할당만 동기화 하는 경우 수 있는지 tooselect hello **사용자 및 그룹** 탭 하 고 hello 사용자 및/또는 toosync 원하는 그룹을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-155">If syncing only assigned users and groups (recommended), be sure tooselect hello **Users and groups** tab and assign hello users and/or groups you wish toosync.</span></span>

<span data-ttu-id="e3202-156">Hello 초기 동기화가 시작 되 면 hello를 사용할 수 있습니다 **감사 로그** 응용 프로그램에서 서비스를 프로 비전 하는 hello 수행한 모든 작업을 보여 주는 toomonitor 진행 상황을 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-156">Once hello initial synchronization has started, you can use hello **Audit logs** tab toomonitor progress, which shows all actions performed by hello provisioning service on your app.</span></span> <span data-ttu-id="e3202-157">Hello Azure AD에 프로 비전 tooread 기록 하는 방법에 대 한 자세한 내용은 참조 하십시오. [자동 사용자 계정 프로 비전에 대 한 보고](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-157">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

>[!NOTE]
><span data-ttu-id="e3202-158">hello 초기 동기화는 hello 서비스가 실행 되 고으로 약 20 분 마다 발생 하는 후속 동기화 보다 더 긴 tooperform 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-158">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> 


## <a name="building-your-own-provisioning-solution-for-any-application"></a><span data-ttu-id="e3202-159">응용 프로그램에 대한 고유한 프로비전 솔루션 구축</span><span class="sxs-lookup"><span data-stu-id="e3202-159">Building your own provisioning solution for any application</span></span>
<span data-ttu-id="e3202-160">Azure Active Directory와 상호 작용하는 SCIM 웹 서비스를 만들어서 REST 또는 SOAP 사용자 프로비전 API를 제공하는 거의 모든 응용 프로그램에 대한 Single Sign-On 및 자동 사용자 프로비전을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-160">By creating a SCIM web service that interfaces with Azure Active Directory, you can enable single sign-on and automatic user provisioning for virtually any application that provides a REST or SOAP user provisioning API.</span></span>

<span data-ttu-id="e3202-161">방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-161">Here’s how it works:</span></span>

1. <span data-ttu-id="e3202-162">Azure AD는 [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/)로 명명된 공용 언어 인프라 라이브러리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-162">Azure AD provides a common language infrastructure library named [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span></span> <span data-ttu-id="e3202-163">시스템 통합 업체 및 개발자가이 라이브러리 toocreate를 사용할 수 있으며 Azure AD tooany 응용 프로그램의 id 저장소에 연결할 수 SCIM 기반 웹 서비스 끝점을 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-163">System integrators and developers can use this library toocreate and deploy a SCIM-based web service endpoint capable of connecting Azure AD tooany application’s identity store.</span></span>
2. <span data-ttu-id="e3202-164">매핑은 hello 웹 서비스 toomap hello 표준화 된 사용자 스키마 toohello 사용자 스키마와 hello 응용 프로그램에 필요한 프로토콜에서 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-164">Mappings are implemented in hello web service toomap hello standardized user schema toohello user schema and protocol required by hello application.</span></span>
3. <span data-ttu-id="e3202-165">hello 끝점 URL은 hello 응용 프로그램 갤러리에서 사용자 지정 응용 프로그램의 일부분으로 Azure AD에 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-165">hello endpoint URL is registered in Azure AD as part of a custom application in hello application gallery.</span></span>
4. <span data-ttu-id="e3202-166">사용자 및 그룹에는 Azure AD에서 응용 프로그램 toothis 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-166">Users and groups are assigned toothis application in Azure AD.</span></span> <span data-ttu-id="e3202-167">할당, 시 큐 동기화 toobe toohello 대상 응용 프로그램에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-167">Upon assignment, they are put into a queue toobe synchronized toohello target application.</span></span> <span data-ttu-id="e3202-168">hello 큐를 처리 하는 hello 동기화 프로세스에는 20 분 마다 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-168">hello synchronization process handling hello queue runs every 20 minutes.</span></span>

### <a name="code-samples"></a><span data-ttu-id="e3202-169">코드 샘플</span><span class="sxs-lookup"><span data-stu-id="e3202-169">Code Samples</span></span>
<span data-ttu-id="e3202-170">toomake이 프로세스는 더 쉽게 집합이 [코드 샘플](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) 제공 하는 SCIM 웹 서비스 끝점을 만드는 / 자동 프로 비전을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-170">toomake this process easier, a set of [code samples](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) are provided that create a SCIM web service endpoint and demonstrate automatic provisioning.</span></span> <span data-ttu-id="e3202-171">한 가지 샘플은 사용자 및 그룹을 나타내는 쉼표로 구분된 값의 행이 있는 파일을 유지 관리하는 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-171">One sample is of a provider that maintains a file with rows of comma-separated values representing users and groups.</span></span>  <span data-ttu-id="e3202-172">다른 hello hello Amazon 웹 서비스 Id 및 액세스 관리 서비스에 작동 하는 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-172">hello other is of a provider that operates on hello Amazon Web Services Identity and Access Management service.</span></span>  

<span data-ttu-id="e3202-173">**필수 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="e3202-173">**Prerequisites**</span></span>

* <span data-ttu-id="e3202-174">Visual Studio 2013 이상</span><span class="sxs-lookup"><span data-stu-id="e3202-174">Visual Studio 2013 or later</span></span>
* [<span data-ttu-id="e3202-175">Azure SDK for .NET</span><span class="sxs-lookup"><span data-stu-id="e3202-175">Azure SDK for .NET</span></span>](https://azure.microsoft.com/downloads/)
* <span data-ttu-id="e3202-176">Windows 컴퓨터를 지 원하는 hello ASP.NET 4.5 toobe SCIM 끝점 hello로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-176">Windows machine that supports hello ASP.NET framework 4.5 toobe used as hello SCIM endpoint.</span></span> <span data-ttu-id="e3202-177">이 컴퓨터는 hello 클라우드에서 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-177">This machine must be accessible from hello cloud</span></span>
* [<span data-ttu-id="e3202-178">Azure AD Premium의 평가판 또는 사용이 허가된 버전의 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="e3202-178">An Azure subscription with a trial or licensed version of Azure AD Premium</span></span>](https://azure.microsoft.com/services/active-directory/)
* <span data-ttu-id="e3202-179">hello AWS Amazon 샘플을 사용 하려면 hello에서 라이브러리 [Visual Studio 용 도구 키트에 AWS](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-179">hello Amazon AWS sample requires libraries from hello [AWS Toolkit for Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span></span> <span data-ttu-id="e3202-180">자세한 내용은 hello 추가 정보를 참조 하십시오. hello 샘플에 포함 된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-180">For more information, see hello README file included with hello sample.</span></span>

### <a name="getting-started"></a><span data-ttu-id="e3202-181">시작하기</span><span class="sxs-lookup"><span data-stu-id="e3202-181">Getting Started</span></span>
<span data-ttu-id="e3202-182">Azure AD에서 프로 비전을 허용할 수 있는 SCIM 끝점 요청 hello 가장 쉬운 방법은 tooimplement toobuild 이며 hello 프로 비전 된 사용자 tooa 쉼표로 구분 된 값 (CSV) 파일을 출력 하는 hello 코드 샘플을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-182">hello easiest way tooimplement a SCIM endpoint that can accept provisioning requests from Azure AD is toobuild and deploy hello code sample that outputs hello provisioned users tooa comma-separated value (CSV) file.</span></span>

<span data-ttu-id="e3202-183">**toocreate 샘플 SCIM 끝점:**</span><span class="sxs-lookup"><span data-stu-id="e3202-183">**toocreate a sample SCIM endpoint:**</span></span>

1. <span data-ttu-id="e3202-184">hello 코드 예제 패키지를 다운로드 [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span><span class="sxs-lookup"><span data-stu-id="e3202-184">Download hello code sample package at [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span></span>
2. <span data-ttu-id="e3202-185">Hello 패키지의 압축을 푸는 C:\AzureAD-BYOA-Provisioning-Samples\와 같은 위치에서 Windows 컴퓨터에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-185">Unzip hello package and place it on your Windows machine at a location such as C:\AzureAD-BYOA-Provisioning-Samples\.</span></span>
3. <span data-ttu-id="e3202-186">이 폴더에 Visual Studio에서 hello FileProvisioningAgent 솔루션을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-186">In this folder, launch hello FileProvisioningAgent solution in Visual Studio.</span></span>
4. <span data-ttu-id="e3202-187">선택 **도구 > 라이브러리 패키지 관리자 > 패키지 관리자 콘솔**, hello 다음 hello FileProvisioningAgent 프로젝트 tooresolve hello 솔루션 참조에 대 한 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-187">Select **Tools > Library Package Manager > Package Manager Console**, and execute hello following commands for hello FileProvisioningAgent project tooresolve hello solution references:</span></span>
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. <span data-ttu-id="e3202-188">Hello FileProvisioningAgent 프로젝트를 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="e3202-188">Build hello FileProvisioningAgent project.</span></span>
6. <span data-ttu-id="e3202-189">Hello 명령 프롬프트에서에서 응용 프로그램 Windows (Administrator)로 시작 하 고 hello를 사용 하 여 **cd** 명령 toochange hello 디렉터리 tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-189">Launch hello Command Prompt application in Windows (as an Administrator), and use hello **cd** command toochange hello directory tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** folder.</span></span>
7. <span data-ttu-id="e3202-190">Hello < ip 주소 > hello Windows 컴퓨터의 hello IP 주소 또는 도메인 이름으로 바뀔, 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-190">Run hello following command, replacing <ip-address> with hello IP address or domain name of hello Windows machine:</span></span>
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. <span data-ttu-id="e3202-191">창의에 **Windows 설정 > 네트워크 및 인터넷 설정을**선택, hello **Windows 방화벽 > 고급 설정**, 만들고는 **인바운드 규칙** 입니다 인바운드 액세스 tooport 9000을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-191">In Windows under **Windows Settings > Network & Internet Settings**, select hello **Windows Firewall > Advanced Settings**, and create an **Inbound Rule** that allows inbound access tooport 9000.</span></span>
9. <span data-ttu-id="e3202-192">Hello Windows 컴퓨터가 라우터 뒤에 있는 경우 라우터 요구 구성 toobe tooperform 네트워크 액세스 변환 해당 포트 9000 간의 노출된 toohello 있는 hello 인터넷 및 포트 9000 hello Windows 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-192">If hello Windows machine is behind a router, hello router needs toobe configured tooperform Network Access Translation between its port 9000 that is exposed toohello internet, and port 9000 on hello Windows machine.</span></span> <span data-ttu-id="e3202-193">이 Azure AD toobe 수 tooaccess 필요 hello 클라우드에서이 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-193">This is required for Azure AD toobe able tooaccess this endpoint in hello cloud.</span></span>

<span data-ttu-id="e3202-194">**hello 샘플 SCIM 끝점 Azure AD에서 tooregister 하 고:**</span><span class="sxs-lookup"><span data-stu-id="e3202-194">**tooregister hello sample SCIM endpoint in Azure AD:**</span></span>

1. <span data-ttu-id="e3202-195">역시 로그인[Azure 포털 hello](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-195">Sign in too[hello Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="e3202-196">너무 찾아보기 * * Azure Active Directory > 엔터프라이즈 응용 프로그램 및 선택 **새 응용 프로그램 > 모든 > 비 갤러리 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-196">Browse too**Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="e3202-197">응용 프로그램에 대 한 이름을 입력 하 고 클릭 **추가** 아이콘 toocreate 응용 프로그램 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-197">Enter a name for your application, and click **Add** icon toocreate an app object.</span></span> <span data-ttu-id="e3202-198">hello application 개체 생성은 의도 한 toorepresent hello 대상 앱 single sign-on, 및 뿐 아니라 hello SCIM 끝점 구현 tooand 프로비저닝 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-198">hello application object created is intended toorepresent hello target app you would be provisioning tooand implementing single sign-on for, and not just hello SCIM endpoint.</span></span>
4. <span data-ttu-id="e3202-199">Hello 결과 화면에서 선택 hello **프로 비전** hello 왼쪽된 열에는 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-199">In hello resulting screen, select hello **Provisioning** tab in hello left column.</span></span>
5. <span data-ttu-id="e3202-200">Hello에 **프로 비전 모드** 메뉴 선택 **자동**합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-200">In hello **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="e3202-201">![][2]
  *그림 4: hello Azure 포털에서에서 프로 비전 구성*</span><span class="sxs-lookup"><span data-stu-id="e3202-201">![][2]
*Figure 4: Configuring provisioning in hello Azure portal*</span></span>
    
6. <span data-ttu-id="e3202-202">Hello에 **테 넌 트 URL** 필드 hello 인터넷에 노출 된 URL과 SCIM 끝점의 포트를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-202">In hello **Tenant URL** field, enter hello internet-exposed URL and port of your SCIM endpoint.</span></span> <span data-ttu-id="e3202-203">것 것 처럼 http://testmachine.contoso.com:9000 나 < ip 주소 > 인터넷을 hello는 http://<ip-address>:9000/ 노출 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-203">This would be something like http://testmachine.contoso.com:9000 or http://<ip-address>:9000/, where <ip-address> is hello internet exposed IP address.</span></span>  
7. <span data-ttu-id="e3202-204">Hello SCIM 끝점 Azure AD 이외의 발급자 로부터 OAuth 전달자 토큰에 필요한 경우 복사 hello 선택적 hello에 OAuth 전달자 토큰을 필요한 **암호 토큰** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-204">If hello SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy hello required OAuth bearer token into hello optional **Secret Token** field.</span></span> <span data-ttu-id="e3202-205">이 필드를 비워 두면 Azure AD에 각 요청에 따라 Azure AD에서 발급한 OAuth 전달자 토큰이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-205">If this field is left blank, then Azure AD will include an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="e3202-206">ID 공급자로 Azure AD를 사용하는 앱은 Azure AD에서 발급한 토큰의 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-206">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="e3202-207">Hello 클릭 **연결 테스트** 단추 toohave Azure Active Directory 시도 tooconnect toohello SCIM 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-207">Click hello **Test Connection** button toohave Azure Active Directory attempt tooconnect toohello SCIM endpoint.</span></span> <span data-ttu-id="e3202-208">Hello 시도가 실패 한 경우 오류 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-208">If hello attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="e3202-209">Hello 시도 tooconnect toohello 응용 프로그램 성공 하는 경우 클릭 **저장** toosave hello에 대 한 관리자 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-209">If hello attempts tooconnect toohello application succeed, then click **Save** toosave hello admin credentials.</span></span>
10. <span data-ttu-id="e3202-210">Hello에 **매핑** 섹션에서 두 개의 선택할 수 있는 특성 매핑 집합이: 사용자 개체 및 그룹 개체에 대 한 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-210">In hello **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="e3202-211">Azure Active Directory tooyour 응용 프로그램에서 동기화 되는 각 하나의 tooreview hello 특성을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-211">Select each one tooreview hello attributes that are synchronized from Azure Active Directory tooyour app.</span></span> <span data-ttu-id="e3202-212">특성으로 선택 된 hello **일치** 속성은 업데이트 작업에 대 한 응용 프로그램에서 사용 되는 toomatch hello 사용자 및 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-212">hello attributes selected as **Matching** properties are used toomatch hello users and groups in your app for update operations.</span></span> <span data-ttu-id="e3202-213">변경 내용을 저장 단추 toocommit hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-213">Select hello Save button toocommit any changes.</span></span>
11. <span data-ttu-id="e3202-214">아래 **설정**, hello **범위** 사용자 및 그룹 동기화 되는 또는 필드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-214">Under **Settings**, hello **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="e3202-215">Hello에 할당 사용자 및 그룹에만 동기화 합니다 "동기화만 할당 된 사용자 및 그룹" (권장)을 선택 하면 **사용자 및 그룹** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-215">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in hello **Users and groups** tab.</span></span>
12. <span data-ttu-id="e3202-216">구성을 완료 되 면 변경 hello **프로 비전 상태** 너무**에**합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-216">Once your configuration is complete, change hello **Provisioning Status** too**On**.</span></span>
13. <span data-ttu-id="e3202-217">클릭 **저장** toostart hello Azure AD에 프로 비전 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-217">Click **Save** toostart hello Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="e3202-218">사용자 및 그룹 (권장) 할당만 동기화 하는 경우 수 있는지 tooselect hello **사용자 및 그룹** 탭 하 고 hello 사용자 및/또는 toosync 원하는 그룹을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-218">If syncing only assigned users and groups (recommended), be sure tooselect hello **Users and groups** tab and assign hello users and/or groups you wish toosync.</span></span>

<span data-ttu-id="e3202-219">Hello 초기 동기화가 시작 되 면 hello를 사용할 수 있습니다 **감사 로그** 응용 프로그램에서 서비스를 프로 비전 하는 hello 수행한 모든 작업을 보여 주는 toomonitor 진행 상황을 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-219">Once hello initial synchronization has started, you can use hello **Audit logs** tab toomonitor progress, which shows all actions performed by hello provisioning service on your app.</span></span> <span data-ttu-id="e3202-220">Hello Azure AD에 프로 비전 tooread 기록 하는 방법에 대 한 자세한 내용은 참조 하십시오. [자동 사용자 계정 프로 비전에 대 한 보고](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-220">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

<span data-ttu-id="e3202-221">hello 최종 단계는 hello 샘플을 확인 하는 tooopen hello hello \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug 폴더에 Windows 컴퓨터 TargetFile.csv 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-221">hello final step in verifying hello sample is tooopen hello TargetFile.csv file in hello \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug folder on your Windows machine.</span></span> <span data-ttu-id="e3202-222">Hello를 프로 비전 프로세스를 실행 한 후이 파일에 할당 하 고 사용자 및 그룹을 프로 비전 하는 모든 hello 세부적인 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-222">Once hello provisioning process is run, this file shows hello details of all assigned and provisioned users and groups.</span></span>

### <a name="development-libraries"></a><span data-ttu-id="e3202-223">개발 라이브러리</span><span class="sxs-lookup"><span data-stu-id="e3202-223">Development libraries</span></span>
<span data-ttu-id="e3202-224">toodevelop toohello SCIM 사양을 준수 하는 웹 서비스 먼저 숙지 hello toohelp microsoft hello 개발 프로세스를 가속화할 제공 라이브러리를 따라.</span><span class="sxs-lookup"><span data-stu-id="e3202-224">toodevelop your own web service that conforms toohello SCIM specification, first familiarize yourself with hello following libraries provided by Microsoft toohelp accelerate hello development process:</span></span> 

1. <span data-ttu-id="e3202-225">CLI(공용 언어 인프라) 라이브러리는 C#과 같은 해당 인프라에 따라 언어와 함께 사용하기 위해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-225">Common Language Infrastructure (CLI) libraries are offered for use with languages based on that infrastructure, such as C#.</span></span> <span data-ttu-id="e3202-226">이러한 라이브러리 중 하나 [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), 인터페이스 선언, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, hello 다음 그림에에서 표시 된: A hello 라이브러리를 사용 하는 개발자, 일반적으로 공급자 참조 될 수 있는 클래스와 해당 인터페이스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-226">One of those libraries, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declares an interface, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, shown in hello following illustration:  A developer using hello libraries would implement that interface with a class that may be referred to, generically, as a provider.</span></span> <span data-ttu-id="e3202-227">hello 라이브러리 hello 개발자 toodeploy toohello SCIM 사양을 준수 하는 웹 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-227">hello libraries enable hello developer toodeploy a web service that conforms toohello SCIM specification.</span></span> <span data-ttu-id="e3202-228">hello 웹 서비스는 인터넷 정보 서비스 또는 실행 가능한 모든 공용 언어 인프라 어셈블리 내에서 하거나 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-228">hello web service can be either hosted within Internet Information Services, or any executable Common Language Infrastructure assembly.</span></span> <span data-ttu-id="e3202-229">요청에 일부 id 저장소 hello 개발자 toooperate 하 여 프로그래밍할 수는 호출 toohello 공급자 메서드로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-229">Request is translated into calls toohello provider’s methods, which would be programmed by hello developer toooperate on some identity store.</span></span>
  
  ![][3]
  
2. <span data-ttu-id="e3202-230">[Express 경로 처리기](http://expressjs.com/guide/routing.html) 호출 (에 정의 된 대로 hello SCIM 사양), tooa node.js 웹 서비스를 나타내는 node.js 요청 개체를 구문 분석에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-230">[Express route handlers](http://expressjs.com/guide/routing.html) are available for parsing node.js request objects representing calls (as defined by hello SCIM specification), made tooa node.js web service.</span></span>   

### <a name="building-a-custom-scim-endpoint"></a><span data-ttu-id="e3202-231">사용자 지정 SCIM 끝점 빌드</span><span class="sxs-lookup"><span data-stu-id="e3202-231">Building a Custom SCIM Endpoint</span></span>
<span data-ttu-id="e3202-232">Hello CLI 라이브러리를 사용 하 여 해당 라이브러리를 사용 하는 개발자는 모든 실행 가능한 공용 언어 인프라 어셈블리 내에서 또는 인터넷 정보 서비스 내 서비스를 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-232">Using hello CLI libraries, developers using those libraries can host their services within any executable Common Language Infrastructure assembly, or within Internet Information Services.</span></span> <span data-ttu-id="e3202-233">Hello 주소 http://localhost:9000에서 있는 실행 가능한 어셈블리 내에서 서비스를 호스트에 대 한 샘플 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-233">Here is sample code for hosting a service within an executable assembly, at hello address http://localhost:9000:</span></span> 

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

<span data-ttu-id="e3202-234">이 서비스는 hello의 루트 인증 기관 hello 다음 중 하나는 HTTP 주소 및 서버 인증 인증서가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-234">This service must have an HTTP address and server authentication certificate of which hello root certification authority is one of hello following:</span></span> 

* <span data-ttu-id="e3202-235">CNNIC</span><span class="sxs-lookup"><span data-stu-id="e3202-235">CNNIC</span></span>
* <span data-ttu-id="e3202-236">Comodo</span><span class="sxs-lookup"><span data-stu-id="e3202-236">Comodo</span></span>
* <span data-ttu-id="e3202-237">CyberTrust</span><span class="sxs-lookup"><span data-stu-id="e3202-237">CyberTrust</span></span>
* <span data-ttu-id="e3202-238">DigiCert</span><span class="sxs-lookup"><span data-stu-id="e3202-238">DigiCert</span></span>
* <span data-ttu-id="e3202-239">GeoTrust</span><span class="sxs-lookup"><span data-stu-id="e3202-239">GeoTrust</span></span>
* <span data-ttu-id="e3202-240">GlobalSign</span><span class="sxs-lookup"><span data-stu-id="e3202-240">GlobalSign</span></span>
* <span data-ttu-id="e3202-241">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="e3202-241">Go Daddy</span></span>
* <span data-ttu-id="e3202-242">Verisign</span><span class="sxs-lookup"><span data-stu-id="e3202-242">Verisign</span></span>
* <span data-ttu-id="e3202-243">WoSign</span><span class="sxs-lookup"><span data-stu-id="e3202-243">WoSign</span></span>

<span data-ttu-id="e3202-244">서버 인증 인증서에 바인딩된 tooa 호스트의 포트에는 Windows hello 네트워크 셸 유틸리티를 사용 하 여 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-244">A server authentication certificate can be bound tooa port on a Windows host using hello network shell utility:</span></span> 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

<span data-ttu-id="e3202-245">여기서 hello hello certhash 인수에 제공 된 기간은 hello 인증서의 지문 안녕하세요 hello 값 hello appid 인수에 제공 되는 임의의 전역 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-245">Here, hello value provided for hello certhash argument is hello thumbprint of hello certificate, while hello value provided for hello appid argument is an arbitrary globally unique identifier.</span></span>  

<span data-ttu-id="e3202-246">인터넷 정보 서비스 내에서 toohost hello 서비스를 개발자 시작 hello 어셈블리의 hello 기본 네임 스페이스에 이름이 지정 된 클래스와 함께 CLA 코드 라이브러리 어셈블리를 빌드하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-246">toohost hello service within Internet Information Services, a developer would build a CLA code library assembly with a class named Startup in hello default namespace of hello assembly.</span></span>  <span data-ttu-id="e3202-247">이러한 클래스의 샘플은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-247">Here is a sample of such a class:</span></span> 

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

### <a name="handling-endpoint-authentication"></a><span data-ttu-id="e3202-248">끝점 인증 처리</span><span class="sxs-lookup"><span data-stu-id="e3202-248">Handling endpoint authentication</span></span>
<span data-ttu-id="e3202-249">Azure Active Directory에서 요청은 OAuth 2.0 전달자 토큰을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-249">Requests from Azure Active Directory include an OAuth 2.0 bearer token.</span></span>   <span data-ttu-id="e3202-250">모든 서비스 수신 hello 요청 hello 발급자 액세스 toohello Azure Active Directory Graph 웹 서비스에 대 한 예상 hello Azure Active Directory 테 넌을 대신 하 여 Azure Active Directory 것으로 인증 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-250">Any service receiving hello request should authenticate hello issuer as being Azure Active Directory on behalf of hello expected Azure Active Directory tenant, for access toohello Azure Active Directory Graph web service.</span></span>  <span data-ttu-id="e3202-251">Hello 토큰에서 발급자 hello "iss"와 같은 경우 iss 클레임으로 식별 됩니다: "https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/"입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-251">In hello token, hello issuer is identified by an iss claim, like, "iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span></span>  <span data-ttu-id="e3202-252">이 예제에서는 hello 클레임 값의 기본 주소 hello https://sts.windows.net, 발급자 hello 대로 Azure Active Directory를 식별, 동안 hello cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, 상대 주소 세그먼트의 고유 식별자 hello Azure Active 토큰이 발급 된 어떤 hello를 대신 하 여 디렉터리 테 넌 트.</span><span class="sxs-lookup"><span data-stu-id="e3202-252">In this example, hello base address of hello claim value, https://sts.windows.net, identifies Azure Active Directory as hello issuer, while hello relative address segment, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, is a unique identifier of hello Azure Active Directory tenant on behalf of which hello token was issued.</span></span>  <span data-ttu-id="e3202-253">Hello Azure Active Directory Graph 웹 서비스, 해당 서비스의 다음 hello 식별자에 액세스 하기 위한 hello 토큰이 발급 된 경우 00000002-0000-0000-c000-000000000000, 될 hello 토큰의 aud hello 값에서 무시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-253">If hello token was issued for accessing hello Azure Active Directory Graph web service, then hello identifier of that service, 00000002-0000-0000-c000-000000000000, should be in hello value of hello token’s aud claim.</span></span>  

<span data-ttu-id="e3202-254">SCIM 서비스를 빌드하기 위한 Microsoft에서 제공 하는 hello CLA 라이브러리를 사용 하는 개발자 Microsoft.Owin.Security.ActiveDirectory 패키지용 hello를 사용 하 여 다음이 단계를 수행 하 여 Azure Active Directory의 요청을 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-254">Developers using hello CLA libraries provided by Microsoft for building a SCIM service can authenticate requests from Azure Active Directory using hello Microsoft.Owin.Security.ActiveDirectory package by following these steps:</span></span> 

1. <span data-ttu-id="e3202-255">공급자에서 hello 서비스가 시작 될 때마다 호출 메서드 toobe를 반환 하 여 hello Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior 속성을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-255">In a provider, implement hello Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior property by having it return a method toobe called whenever hello service is started:</span></span> 

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

2. <span data-ttu-id="e3202-256">다음 코드 toothat 메서드 toohave hello bearing 액세스 toohello Azure AD 그래프 웹 서비스에 대 한 지정 된 테 넌을 대신 하 여 Azure Active Directory에서 발급 한 토큰으로 인증 하는 hello 서비스 끝점의 모든 요청 tooany를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-256">Add hello following code toothat method toohave any request tooany of hello service’s endpoints authenticated as bearing a token issued by Azure Active Directory on behalf of a specified tenant, for access toohello Azure AD Graph web service:</span></span> 

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
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute hello appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a><span data-ttu-id="e3202-257">사용자 및 그룹 스키마</span><span class="sxs-lookup"><span data-stu-id="e3202-257">User and group schema</span></span>
<span data-ttu-id="e3202-258">Azure Active Directory는 두 가지 유형의 리소스 tooSCIM 웹 서비스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-258">Azure Active Directory can provision two types of resources tooSCIM web services.</span></span>  <span data-ttu-id="e3202-259">이러한 형식의 리소스는 사용자 및 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-259">Those types of resources are users and groups.</span></span>  

<span data-ttu-id="e3202-260">사용자 리소스는이 프로토콜 사양에 포함 된 urn: ietf:params:scim:schemas:extension:enterprise:2.0:User hello 스키마 식별자로 식별 됩니다: http://tools.ietf.org/html/draft-ietf-scim-core-schema 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-260">User resources are identified by hello schema identifier, urn:ietf:params:scim:schemas:extension:enterprise:2.0:User, which is included in this protocol specification: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span></span>  <span data-ttu-id="e3202-261">아래 표에 1, urn: ietf:params:scim:schemas:extension:enterprise:2.0:User 리소스의 Azure Active Directory toohello 특성에 있는 사용자의 hello 특성의 hello 기본 매핑을 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-261">hello default mapping of hello attributes of users in Azure Active Directory toohello attributes of urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resources is provided in table 1, below.</span></span>  

<span data-ttu-id="e3202-262">리소스 그룹 hello 스키마 식별자로 식별 됩니다 http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-262">Group resources are identified by hello schema identifier, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  <span data-ttu-id="e3202-263">테이블 2, 아래 http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group 리소스의 Azure Active Directory toohello 특성에 있는 그룹의 hello 특성의 hello 기본 매핑 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-263">Table 2, below, shows hello default mapping of hello attributes of groups in Azure Active Directory toohello attributes of http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group resources.</span></span>  

### <a name="table-1-default-user-attribute-mapping"></a><span data-ttu-id="e3202-264">테이블 1: 기본 사용자 특성 매핑</span><span class="sxs-lookup"><span data-stu-id="e3202-264">Table 1: Default user attribute mapping</span></span>
| <span data-ttu-id="e3202-265">Azure Active Directory 사용자</span><span class="sxs-lookup"><span data-stu-id="e3202-265">Azure Active Directory user</span></span> | <span data-ttu-id="e3202-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span><span class="sxs-lookup"><span data-stu-id="e3202-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span></span> |
| --- | --- |
| <span data-ttu-id="e3202-267">IsSoftDeleted</span><span class="sxs-lookup"><span data-stu-id="e3202-267">IsSoftDeleted</span></span> |<span data-ttu-id="e3202-268">활성</span><span class="sxs-lookup"><span data-stu-id="e3202-268">active</span></span> |
| <span data-ttu-id="e3202-269">displayName</span><span class="sxs-lookup"><span data-stu-id="e3202-269">displayName</span></span> |<span data-ttu-id="e3202-270">displayName</span><span class="sxs-lookup"><span data-stu-id="e3202-270">displayName</span></span> |
| <span data-ttu-id="e3202-271">Facsimile-TelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="e3202-271">Facsimile-TelephoneNumber</span></span> |<span data-ttu-id="e3202-272">phoneNumbers[type eq "fax"].value</span><span class="sxs-lookup"><span data-stu-id="e3202-272">phoneNumbers[type eq "fax"].value</span></span> |
| <span data-ttu-id="e3202-273">givenName</span><span class="sxs-lookup"><span data-stu-id="e3202-273">givenName</span></span> |<span data-ttu-id="e3202-274">name.givenName</span><span class="sxs-lookup"><span data-stu-id="e3202-274">name.givenName</span></span> |
| <span data-ttu-id="e3202-275">jobTitle</span><span class="sxs-lookup"><span data-stu-id="e3202-275">jobTitle</span></span> |<span data-ttu-id="e3202-276">title</span><span class="sxs-lookup"><span data-stu-id="e3202-276">title</span></span> |
| <span data-ttu-id="e3202-277">mail</span><span class="sxs-lookup"><span data-stu-id="e3202-277">mail</span></span> |<span data-ttu-id="e3202-278">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="e3202-278">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="e3202-279">mailNickname</span><span class="sxs-lookup"><span data-stu-id="e3202-279">mailNickname</span></span> |<span data-ttu-id="e3202-280">externalId</span><span class="sxs-lookup"><span data-stu-id="e3202-280">externalId</span></span> |
| <span data-ttu-id="e3202-281">manager</span><span class="sxs-lookup"><span data-stu-id="e3202-281">manager</span></span> |<span data-ttu-id="e3202-282">manager</span><span class="sxs-lookup"><span data-stu-id="e3202-282">manager</span></span> |
| <span data-ttu-id="e3202-283">mobile</span><span class="sxs-lookup"><span data-stu-id="e3202-283">mobile</span></span> |<span data-ttu-id="e3202-284">phoneNumbers[type eq "mobile"].value</span><span class="sxs-lookup"><span data-stu-id="e3202-284">phoneNumbers[type eq "mobile"].value</span></span> |
| <span data-ttu-id="e3202-285">objectId</span><span class="sxs-lookup"><span data-stu-id="e3202-285">objectId</span></span> |<span data-ttu-id="e3202-286">id</span><span class="sxs-lookup"><span data-stu-id="e3202-286">id</span></span> |
| <span data-ttu-id="e3202-287">postalCode</span><span class="sxs-lookup"><span data-stu-id="e3202-287">postalCode</span></span> |<span data-ttu-id="e3202-288">addresses[type eq "work"].postalCode</span><span class="sxs-lookup"><span data-stu-id="e3202-288">addresses[type eq "work"].postalCode</span></span> |
| <span data-ttu-id="e3202-289">proxy-Addresses</span><span class="sxs-lookup"><span data-stu-id="e3202-289">proxy-Addresses</span></span> |<span data-ttu-id="e3202-290">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="e3202-290">emails[type eq "other"].Value</span></span> |
| <span data-ttu-id="e3202-291">physical-Delivery-OfficeName</span><span class="sxs-lookup"><span data-stu-id="e3202-291">physical-Delivery-OfficeName</span></span> |<span data-ttu-id="e3202-292">addresses[type eq "other"].Formatted</span><span class="sxs-lookup"><span data-stu-id="e3202-292">addresses[type eq "other"].Formatted</span></span> |
| <span data-ttu-id="e3202-293">streetAddress</span><span class="sxs-lookup"><span data-stu-id="e3202-293">streetAddress</span></span> |<span data-ttu-id="e3202-294">addresses[type eq "work"].streetAddress</span><span class="sxs-lookup"><span data-stu-id="e3202-294">addresses[type eq "work"].streetAddress</span></span> |
| <span data-ttu-id="e3202-295">surname</span><span class="sxs-lookup"><span data-stu-id="e3202-295">surname</span></span> |<span data-ttu-id="e3202-296">name.familyName</span><span class="sxs-lookup"><span data-stu-id="e3202-296">name.familyName</span></span> |
| <span data-ttu-id="e3202-297">telephone-Number</span><span class="sxs-lookup"><span data-stu-id="e3202-297">telephone-Number</span></span> |<span data-ttu-id="e3202-298">phoneNumbers[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="e3202-298">phoneNumbers[type eq "work"].value</span></span> |
| <span data-ttu-id="e3202-299">user-PrincipalName</span><span class="sxs-lookup"><span data-stu-id="e3202-299">user-PrincipalName</span></span> |<span data-ttu-id="e3202-300">userName</span><span class="sxs-lookup"><span data-stu-id="e3202-300">userName</span></span> |

### <a name="table-2-default-group-attribute-mapping"></a><span data-ttu-id="e3202-301">테이블 2: 기본 그룹 특성 매핑</span><span class="sxs-lookup"><span data-stu-id="e3202-301">Table 2: Default group attribute mapping</span></span>
| <span data-ttu-id="e3202-302">Azure Active Directory 그룹</span><span class="sxs-lookup"><span data-stu-id="e3202-302">Azure Active Directory group</span></span> | <span data-ttu-id="e3202-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span><span class="sxs-lookup"><span data-stu-id="e3202-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span></span> |
| --- | --- |
| <span data-ttu-id="e3202-304">displayName</span><span class="sxs-lookup"><span data-stu-id="e3202-304">displayName</span></span> |<span data-ttu-id="e3202-305">externalId</span><span class="sxs-lookup"><span data-stu-id="e3202-305">externalId</span></span> |
| <span data-ttu-id="e3202-306">mail</span><span class="sxs-lookup"><span data-stu-id="e3202-306">mail</span></span> |<span data-ttu-id="e3202-307">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="e3202-307">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="e3202-308">mailNickname</span><span class="sxs-lookup"><span data-stu-id="e3202-308">mailNickname</span></span> |<span data-ttu-id="e3202-309">displayName</span><span class="sxs-lookup"><span data-stu-id="e3202-309">displayName</span></span> |
| <span data-ttu-id="e3202-310">members</span><span class="sxs-lookup"><span data-stu-id="e3202-310">members</span></span> |<span data-ttu-id="e3202-311">members</span><span class="sxs-lookup"><span data-stu-id="e3202-311">members</span></span> |
| <span data-ttu-id="e3202-312">objectId</span><span class="sxs-lookup"><span data-stu-id="e3202-312">objectId</span></span> |<span data-ttu-id="e3202-313">id</span><span class="sxs-lookup"><span data-stu-id="e3202-313">id</span></span> |
| <span data-ttu-id="e3202-314">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="e3202-314">proxyAddresses</span></span> |<span data-ttu-id="e3202-315">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="e3202-315">emails[type eq "other"].Value</span></span> |

## <a name="user-provisioning-and-de-provisioning"></a><span data-ttu-id="e3202-316">사용자 프로비저닝 및 프로비전 해제</span><span class="sxs-lookup"><span data-stu-id="e3202-316">User provisioning and de-provisioning</span></span>
<span data-ttu-id="e3202-317">다음 그림에서는 hello 메시지를 Azure Active Directory 다른 id 저장소에 사용자의 tooa SCIM 서비스 toomanage hello 주기를 전송 하는 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-317">hello following illustration shows hello messages that Azure Active Directory sends tooa SCIM service toomanage hello lifecycle of a user in another identity store.</span></span> <span data-ttu-id="e3202-318">hello 다이어그램에는 어떻게는 SCIM hello CLI 라이브러리를 사용 하 여 구현 Microsoft에서 제공한 서비스 만들기에 대 한 공급자의 toohello 메서드를 호출에 해당 요청을 변환 하는 같은 서비스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-318">hello diagram also shows how a SCIM service implemented using hello CLI libraries provided by Microsoft for building such services translate those requests into calls toohello methods of a provider.</span></span>  

<span data-ttu-id="e3202-319">![][4]
*그림 5: 사용자 프로비저닝 및 시퀀스 프로비전 해제*</span><span class="sxs-lookup"><span data-stu-id="e3202-319">![][4]
*Figure 5: User provisioning and de-provisioning sequence*</span></span>

1. <span data-ttu-id="e3202-320">Azure Active Directory 쿼리 externalId 특성 값이 사용자의 hello mailNickname 특성 값을 일치 하는 Azure AD에서 사용자에 대 한 서비스를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-320">Azure Active Directory queries hello service for a user with an externalId attribute value matching hello mailNickname attribute value of a user in Azure AD.</span></span> <span data-ttu-id="e3202-321">hello 쿼리 jyoung은 Azure Active Directory에서 사용자의 mailNickname의 샘플에는이 예제에서는 같은 하이퍼텍스트 전송 프로토콜 (HTTP) 요청으로 표현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-321">hello query is expressed as a Hypertext Transfer Protocol (HTTP) request such as this example, wherein jyoung is a sample of a mailNickname of a user in Azure Active Directory:</span></span> 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="e3202-322">Hello 서비스가 SCIM 서비스 구현에 대 한 Microsoft에서 제공 하는 hello 공용 언어 인프라 라이브러리를 사용 하 여 작성 된 경우에 hello 요청 호출 toohello hello 서비스 공급자의 쿼리 방법으로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-322">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Query method of hello service’s provider.</span></span>  <span data-ttu-id="e3202-323">해당 메서드의 hello 서명을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-323">Here is hello signature of that method:</span></span> 
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
  <span data-ttu-id="e3202-324">Hello Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters 인터페이스의 hello 정의 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-324">Here is hello definition of hello Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters interface:</span></span> 
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
  <span data-ttu-id="e3202-325">다음 샘플 hello externalId 특성에 대 한 지정된 된 값으로 사용자에 대 한 쿼리의 hello, toohello 쿼리 메서드에 전달 하는 hello 인수 값은:</span><span class="sxs-lookup"><span data-stu-id="e3202-325">In hello following sample of a query for a user with a given value for hello externalId attribute, values of hello arguments passed toohello Query method are:</span></span> 
  * <span data-ttu-id="e3202-326">parameters.AlternateFilters.Count: 1</span><span class="sxs-lookup"><span data-stu-id="e3202-326">parameters.AlternateFilters.Count: 1</span></span>
  * <span data-ttu-id="e3202-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span><span class="sxs-lookup"><span data-stu-id="e3202-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span></span>
  * <span data-ttu-id="e3202-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="e3202-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="e3202-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span><span class="sxs-lookup"><span data-stu-id="e3202-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span></span>
  * <span data-ttu-id="e3202-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span><span class="sxs-lookup"><span data-stu-id="e3202-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span></span> 

2. <span data-ttu-id="e3202-331">Hello 응답 tooa 쿼리 toohello 웹 서비스 사용자는 사용자의 hello mailNickname 특성 값과 일치 하는 externalId 특성 값에 대 한 모든 사용자가 반환 하지 않는 경우 그런 다음 Azure Active Directory 요청 사용자 해당 hello 서비스 제공 해당 toohello 하나 Azure Active Directory에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-331">If hello response tooa query toohello web service for a user with an externalId attribute value that matches hello mailNickname attribute value of a user does not return any users, then Azure Active Directory requests that hello service provision a user corresponding toohello one in Azure Active Directory.</span></span>  <span data-ttu-id="e3202-332">다음은 그러한 요청의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-332">Here is an example of such a request:</span></span> 
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
  <span data-ttu-id="e3202-333">SCIM 서비스 구현에 대 한 Microsoft에서 제공 하는 hello 공용 언어 인프라 라이브러리는 호출 toohello hello 서비스 공급자의 Create 메서드를 해당 요청을 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-333">hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services would translate that request into a call toohello Create method of hello service’s provider.</span></span>  <span data-ttu-id="e3202-334">Create 메서드 hello이이 서명을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-334">hello Create method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="e3202-335">요청 tooprovision 사용자에서에서 hello 리소스에 대 한 인수의 값이 hello는 hello Microsoft.SystemForCrossDomainIdentityManagement의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-335">In a request tooprovision a user, hello value of hello resource argument is an instance of hello Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="e3202-336">Hello Microsoft.SystemForCrossDomainIdentityManagement.Schemas 라이브러리에 정의 된 Core2EnterpriseUser 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-336">Core2EnterpriseUser class, defined in hello Microsoft.SystemForCrossDomainIdentityManagement.Schemas library.</span></span>  <span data-ttu-id="e3202-337">Hello 요청 tooprovision hello 사용자에 성공 하면 다음 hello hello 메서드는 예상된 tooreturn hello Microsoft.SystemForCrossDomainIdentityManagement의 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="e3202-337">If hello request tooprovision hello user succeeds, then hello implementation of hello method is expected tooreturn an instance of hello Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="e3202-338">Hello 식별자 속성의 값이 hello Core2EnterpriseUser 클래스 toohello hello 새로 프로 비전 된 사용자의 고유 식별자를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-338">Core2EnterpriseUser class, with hello value of hello Identifier property set toohello unique identifier of hello newly provisioned user.</span></span>  

3. <span data-ttu-id="e3202-339">tooupdate tooexist id 저장소에 알려진 사용자는 SCIM hello 서비스에서와 같은 요청 hello 해당 사용자의 현재 상태를 요청 하 여 Azure Active Directory 계속 진행 하 여 프런트:</span><span class="sxs-lookup"><span data-stu-id="e3202-339">tooupdate a user known tooexist in an identity store fronted by an SCIM, Azure Active Directory proceeds by requesting hello current state of that user from hello service with a request such as:</span></span> 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="e3202-340">SCIM 서비스 구현에 대 한 Microsoft에서 제공 하는 hello 공용 언어 인프라 라이브러리를 사용 하 여 작성 하는 서비스에 hello 요청 호출 toohello hello 서비스 공급자의 검색 방법으로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-340">In a service built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, hello request is translated into a call toohello Retrieve method of hello service’s provider.</span></span>  <span data-ttu-id="e3202-341">Hello 서명의 hello 검색 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-341">Here is hello signature of hello Retrieve method:</span></span> 
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
  <span data-ttu-id="e3202-342">사용자의 요청 tooretrieve hello 현재 상태 hello 예에서 hello hello 매개 변수 인수 값으로 제공 하는 hello 개체의 hello 속성 hello 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-342">In hello example of a request tooretrieve hello current state of a user, hello values of hello properties of hello object provided as hello value of hello parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="e3202-343">식별자: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="e3202-343">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="e3202-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="e3202-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

4. <span data-ttu-id="e3202-345">참조 특성 toobe 업데이트 후 Azure Active Directory 쿼리 hello 서비스 toodetermine 여부 hello hello id 저장소의 hello 참조 특성의 현재 값 프런트 하 여 hello 서비스 이미 검색 hello 특성 값 Azure Active directory 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-345">If a reference attribute is toobe updated, then Azure Active Directory queries hello service toodetermine whether or not hello current value of hello reference attribute in hello identity store fronted by hello service already matches hello value of that attribute in Azure Active Directory.</span></span> <span data-ttu-id="e3202-346">사용자에 대 한 hello만는 hello의 현재 값이 방식으로 쿼리 됩니다 hello 관리자 특성이입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-346">For users, hello only attribute of which hello current value is queried in this way is hello manager attribute.</span></span> <span data-ttu-id="e3202-347">특정 사용자 개체의 hello 관리자 특성에는 현재 특정 값이 있는지 여부를 요청 toodetermine의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-347">Here is an example of a request toodetermine whether hello manager attribute of a particular user object currently has a certain value:</span></span> 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="e3202-348">값 hello hello 특성 쿼리 매개 변수의 id hello hello 필터 쿼리 매개 변수 값으로 제공 하는 hello 식을 만족 하는 사용자 개체가 있는 경우 다음 hello 서비스는 urn: ietf:params:scim:schemas와 예상된 toorespond을 나타냅니다. 코어: 2.0:User 또는 urn: ietf:params:scim:schemas:extension:enterprise:2.0:User 리소스, 해당 리소스의 id 특성의 hello 값만 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-348">hello value of hello attributes query parameter, id, signifies that if a user object exists that satisfies hello expression provided as hello value of hello filter query parameter, then hello service is expected toorespond with a urn:ietf:params:scim:schemas:core:2.0:User or urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resource, including only hello value of that resource’s id attribute.</span></span>  <span data-ttu-id="e3202-349">값의 hello hello **id** 특성 toohello 요청자 알려져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-349">hello value of hello **id** attribute is known toohello requestor.</span></span> <span data-ttu-id="e3202-350">쿼리 매개 변수를 필터 하는 hello; hello 값에 포함 되어 hello에 대 한 질문의 목적은 toorequest 존재 여부 등 모든 개체를 확인 하는 hello 필터 식을 만족 하는 리소스에 대 한 최소 표현을 실제로입니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-350">It is included in hello value of hello filter query parameter; hello purpose of asking for it is actually toorequest a minimal representation of a resource that satisfying hello filter expression as an indication of whether or not any such object exists.</span></span>   

  <span data-ttu-id="e3202-351">Hello 서비스가 SCIM 서비스 구현에 대 한 Microsoft에서 제공 하는 hello 공용 언어 인프라 라이브러리를 사용 하 여 작성 된 경우에 hello 요청 호출 toohello hello 서비스 공급자의 쿼리 방법으로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-351">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Query method of hello service’s provider.</span></span> <span data-ttu-id="e3202-352">hello 매개 변수 인수 hello 값으로 제공 하는 hello 개체의 hello 속성 hello 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-352">hello value of hello properties of hello object provided as hello value of hello parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="e3202-353">parameters.AlternateFilters.Count: 2</span><span class="sxs-lookup"><span data-stu-id="e3202-353">parameters.AlternateFilters.Count: 2</span></span>
  * <span data-ttu-id="e3202-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span><span class="sxs-lookup"><span data-stu-id="e3202-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span></span>
  * <span data-ttu-id="e3202-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="e3202-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="e3202-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="e3202-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="e3202-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="e3202-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span></span>
  * <span data-ttu-id="e3202-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="e3202-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="e3202-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span><span class="sxs-lookup"><span data-stu-id="e3202-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span></span>
  * <span data-ttu-id="e3202-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span><span class="sxs-lookup"><span data-stu-id="e3202-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span></span>
  * <span data-ttu-id="e3202-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="e3202-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

  <span data-ttu-id="e3202-362">여기에서 hello 인덱스 x의 hello 값 0 일 수 있습니다 및 hello hello 인덱스 y 값 수 1, 또는 x의 hello 값은 1 일 수 있으며 y의 hello 값 hello 필터에 대 한 쿼리 매개 변수는 hello 식의 hello 순서에 따라 0이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-362">Here, hello value of hello index x may be 0 and hello value of hello index y may be 1, or hello value of x may be 1 and hello value of y may be 0, depending on hello order of hello expressions of hello filter query parameter.</span></span>   

5. <span data-ttu-id="e3202-363">Azure Active Directory tooan SCIM 서비스 tooupdate 사용자를에서 요청의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-363">Here is an example of a request from Azure Active Directory tooan SCIM service tooupdate a user:</span></span> 
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
  <span data-ttu-id="e3202-364">SCIM 서비스를 구현 하기 위한 hello Microsoft 공용 언어 인프라 라이브러리는 hello 요청 호출 toohello hello 서비스 공급자의 Update 메서드를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-364">hello Microsoft Common Language Infrastructure libraries for implementing SCIM services would translate hello request into a call toohello Update method of hello service’s provider.</span></span> <span data-ttu-id="e3202-365">Hello 서명의 hello 큐브의 Update 메서드에 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-365">Here is hello signature of hello Update method:</span></span> 
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
    <span data-ttu-id="e3202-366">요청 tooupdate 사용자 hello 예제를 hello hello 패치 인수 값으로 제공 하는 hello 개체에는 이러한 속성 값에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-366">In hello example of a request tooupdate a user, hello object provided as hello value of hello patch argument has these property values:</span></span> 
  
  * <span data-ttu-id="e3202-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="e3202-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="e3202-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="e3202-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>
  * <span data-ttu-id="e3202-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span><span class="sxs-lookup"><span data-stu-id="e3202-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span></span>
  * <span data-ttu-id="e3202-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span><span class="sxs-lookup"><span data-stu-id="e3202-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span></span>
  * <span data-ttu-id="e3202-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="e3202-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span></span>
  * <span data-ttu-id="e3202-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span><span class="sxs-lookup"><span data-stu-id="e3202-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span></span>
  * <span data-ttu-id="e3202-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="e3202-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span></span>
  * <span data-ttu-id="e3202-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="e3202-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span></span>

6. <span data-ttu-id="e3202-375">SCIM service에 의해 프로 비전 toode id 저장소에서 사용자 프런트, Azure AD와 같은 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-375">toode-provision a user from an identity store fronted by an SCIM service, Azure AD sends a request such as:</span></span> 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="e3202-376">Hello 서비스가 SCIM 서비스 구현에 대 한 Microsoft에서 제공 하는 hello 공용 언어 인프라 라이브러리를 사용 하 여 작성 된 경우에 hello 요청 호출 toohello hello 서비스 공급자의 Delete 메서드로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-376">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Delete method of hello service’s provider.</span></span>   <span data-ttu-id="e3202-377">해당 메서드에는 다음 서명이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-377">That method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="e3202-378">hello hello resourceIdentifier 인수 값으로 제공 하는 hello 개체의 사용자 요청 toode-프로 비전이의 hello 예에 이러한 속성 값:</span><span class="sxs-lookup"><span data-stu-id="e3202-378">hello object provided as hello value of hello resourceIdentifier argument has these property values in hello example of a request toode-provision a user:</span></span> 
  
  * <span data-ttu-id="e3202-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="e3202-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="e3202-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="e3202-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

## <a name="group-provisioning-and-de-provisioning"></a><span data-ttu-id="e3202-381">그룹 프로비전 및 프로비전 해제</span><span class="sxs-lookup"><span data-stu-id="e3202-381">Group provisioning and de-provisioning</span></span>
<span data-ttu-id="e3202-382">hello 다음 그림에서는 hello 메시지 Azure AcD에 다른 id 저장소 그룹의 tooa SCIM 서비스 toomanage hello 주기를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-382">hello following illustration shows hello messages that Azure AcD sends tooa SCIM service toomanage hello lifecycle of a group in another identity store.</span></span>  <span data-ttu-id="e3202-383">이러한 메시지 toousers 세 가지 방법으로 관련 된 hello 메시지에서 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-383">Those messages differ from hello messages pertaining toousers in three ways:</span></span> 

* <span data-ttu-id="e3202-384">그룹 리소스의 hello 스키마 http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group으로 식별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-384">hello schema of a group resource is identified as http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  
* <span data-ttu-id="e3202-385">Tooretrieve 그룹 해당 hello 멤버 특성을 규정 하는 요청은 toobe 응답 toohello 요청에 제공 된 모든 리소스에서 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3202-385">Requests tooretrieve groups stipulate that hello members attribute is toobe excluded from any resource provided in response toohello request.</span></span>  
* <span data-ttu-id="e3202-386">요청 toodetermine hello 멤버 특성에 대 한 요청이 포함 됩니다는 참조 특성의 값을 특정 값에 있는지 여부.</span><span class="sxs-lookup"><span data-stu-id="e3202-386">Requests toodetermine whether a reference attribute has a certain value are requests about hello members attribute.</span></span>  

<span data-ttu-id="e3202-387">![][5]
*그림 6: 그룹 프로비전 및 시퀀스 프로비전 해제*</span><span class="sxs-lookup"><span data-stu-id="e3202-387">![][5]
*Figure 6: Group provisioning and de-provisioning sequence*</span></span>

## <a name="related-articles"></a><span data-ttu-id="e3202-388">관련 문서</span><span class="sxs-lookup"><span data-stu-id="e3202-388">Related articles</span></span>
* [<span data-ttu-id="e3202-389">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="e3202-389">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="e3202-390">사용자 프로 비전/프로 비전 해제 tooSaaS 응용 프로그램 자동화</span><span class="sxs-lookup"><span data-stu-id="e3202-390">Automate User Provisioning/Deprovisioning tooSaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="e3202-391">사용자 프로비저닝에 대한 특성 매핑 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="e3202-391">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="e3202-392">특성 매핑에 대한 식 작성</span><span class="sxs-lookup"><span data-stu-id="e3202-392">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="e3202-393">사용자 프로 비전에 대 한 필터 범위 지정</span><span class="sxs-lookup"><span data-stu-id="e3202-393">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="e3202-394">계정 프로비전 알림</span><span class="sxs-lookup"><span data-stu-id="e3202-394">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="e3202-395">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱</span><span class="sxs-lookup"><span data-stu-id="e3202-395">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG
