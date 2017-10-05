---
title: "Azure Active Directory 응용 프로그램 및 서비스 주체 개체 | Microsoft Docs"
description: "Azure Active Directory의 응용 프로그램 및 서비스 주체 개체 간의 관계에 대한 설명"
documentationcenter: dev-center-name
author: dstrockis
manager: mbaldwin
services: active-directory
editor: 
ms.assetid: adfc0569-dc91-48fe-92c3-b5b4833703de
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4c75ade5f4e47ef64ccc0fe8af4b174c377dc7bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="application-and-service-principal-objects-in-azure-active-directory-azure-ad"></a><span data-ttu-id="c4987-103">Azure Active Directory(Azure AD)의 응용 프로그램 및 서비스 주체 개체</span><span class="sxs-lookup"><span data-stu-id="c4987-103">Application and service principal objects in Azure Active Directory (Azure AD)</span></span>
<span data-ttu-id="c4987-104">경우에 따라 “응용 프로그램”이 Azure AD의 문맥에서 사용될 때 용어의 의미를 잘못 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-104">Sometimes the meaning of the term "application" can be misunderstood when used in the context of Azure AD.</span></span> <span data-ttu-id="c4987-105">이 문서의 목표는 [다중 테넌트 응용 프로그램](active-directory-dev-glossary.md#multi-tenant-application)에 대한 등록 및 동의에 대한 그림을 통해 Azure AD 응용 프로그램 통합의 개념 및 구체적인 측면을 명확히 설명하여 보다 분명히 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-105">The goal of this article is to make it clearer, by clarifying conceptual and concrete aspects of Azure AD application integration, with an illustration of registration and consent for a [multi-tenant application](active-directory-dev-glossary.md#multi-tenant-application).</span></span>

## <a name="overview"></a><span data-ttu-id="c4987-106">개요</span><span class="sxs-lookup"><span data-stu-id="c4987-106">Overview</span></span>
<span data-ttu-id="c4987-107">Azure AD와 통합된 응용 프로그램은 소프트웨어 측면을 넘어서는 의미를 지닙니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-107">An application that has been integrated with Azure AD has implications that go beyond the software aspect.</span></span> <span data-ttu-id="c4987-108">“응용 프로그램”은 개념적 용어로 응용 프로그램 소프트웨어를 나타낼 뿐 아니라, 런타임 시 인증 및 권한 부여 “대화”에서 Azure AD 등록 및 역할을 나타내기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-108">"Application" is frequently used as a conceptual term, referring to not only the the application software, but also its Azure AD registration and role in authentication/authorization "conversations" at runtime.</span></span> <span data-ttu-id="c4987-109">기본적으로 응용 프로그램은 [클라이언트](active-directory-dev-glossary.md#client-application) 역할(리소스 사용)이나 [리소스 서버](active-directory-dev-glossary.md#resource-server) 역할(클라이언트에게 API 노출) 또는 두 역할 모두에서 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-109">By definition, an application can function in a [client](active-directory-dev-glossary.md#client-application) role (consuming a resource), a [resource server](active-directory-dev-glossary.md#resource-server) role (exposing APIs to clients), or even both.</span></span> <span data-ttu-id="c4987-110">대화 프로토콜은 클라이언트/리소스가 각기 리소스 데이터를 액세스/보호할 수 있도록 하려는 [OAuth 2.0 권한 부여 흐름](active-directory-dev-glossary.md#authorization-grant)에 의해 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-110">The conversation protocol is defined by an [OAuth 2.0 Authorization Grant flow](active-directory-dev-glossary.md#authorization-grant), allowing the client/resource to access/protect a resource's data respectively.</span></span> <span data-ttu-id="c4987-111">이제 한 단계 더 깊이 들어가, Azure AD 응용 프로그램 모델이 디자인 및 런타임 시 응용 프로그램을 내부적으로 나타내는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-111">Now let's go a level deeper, and see how the Azure AD application model represents an application at design-time and run-time.</span></span> 

## <a name="application-registration"></a><span data-ttu-id="c4987-112">응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="c4987-112">Application registration</span></span>
<span data-ttu-id="c4987-113">Azure AD 응용 프로그램을 [Azure Portal][AZURE-Portal]에 등록할 때, Azure AD 테넌트에 응용 프로그램 개체와 서비스 주체 개체라는 두 개체가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-113">When you register an Azure AD application in the [Azure portal][AZURE-Portal], two objects are created in your Azure AD tenant: an application object, and a service principal object.</span></span>

#### <a name="application-object"></a><span data-ttu-id="c4987-114">응용 프로그램 개체</span><span class="sxs-lookup"><span data-stu-id="c4987-114">Application object</span></span>
<span data-ttu-id="c4987-115">Azure AD 응용 프로그램은 응용 프로그램의 "홈" 테넌트라고도 알려진, 응용 프로그램이 등록된 Azure AD 테넌트에 상주하는 하나의 응용 프로그램 개체에 의해서만 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-115">An Azure AD application is defined by its one and only application object, which resides in the Azure AD tenant where the application was registered, known as the application's "home" tenant.</span></span> <span data-ttu-id="c4987-116">Azure AD Graph [응용 프로그램 엔터티][AAD-Graph-App-Entity]는 응용 프로그램 개체의 속성에 대한 스키마를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-116">The Azure AD Graph [Application entity][AAD-Graph-App-Entity] defines the schema for an application object's properties.</span></span> 

#### <a name="service-principal-object"></a><span data-ttu-id="c4987-117">서비스 주체 개체</span><span class="sxs-lookup"><span data-stu-id="c4987-117">Service principal object</span></span>
<span data-ttu-id="c4987-118">서비스 주체 개체는 런타임에 보안 주체가 응용 프로그램을 나타내는 기초를 제공하여 특정 테넌트에서 응용 프로그램 사용에 대한 정책 및 권한을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-118">The service principal object defines the policy and permissions for an application's use in a specific tenant, providing the basis for a security principal to represent the application at run-time.</span></span> <span data-ttu-id="c4987-119">Azure AD Graph [서비스 주체 엔터티][AAD-Graph-Sp-Entity]는 서비스 주체 개체의 속성에 대한 스키마를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-119">The Azure AD Graph [ServicePrincipal entity][AAD-Graph-Sp-Entity] defines the schema for a service principal object's properties.</span></span> 

#### <a name="application-and-service-principal-relationship"></a><span data-ttu-id="c4987-120">응용 프로그램 및 서비스 주체 관계</span><span class="sxs-lookup"><span data-stu-id="c4987-120">Application and service principal relationship</span></span>
<span data-ttu-id="c4987-121">응용 프로그램 개체는 모든 테넌트에서 사용하기 위한 응용 프로그램의 *글로벌* 표현으로 그리고 서비스 주체는 특정 테넌트에서 사용하기 위한 *로컬* 표현으로 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-121">Consider the application object as the *global* representation of your application for use across all tenants, and the service principal as the *local* representation for use in a specific tenant.</span></span> <span data-ttu-id="c4987-122">응용 프로그램 개체는 해당 서비스 주체 개체 만들기에 사용하기 위해 공통의 기본 속성이 *파생*되는 템플릿으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-122">The application object serves as the template from which common and default properties are *derived* for use in creating corresponding service principal objects.</span></span> <span data-ttu-id="c4987-123">따라서 응용 프로그램 개체는 소프트웨어 응용 프로그램과 1:1 관계가 있으며 해당 서비스 주체 개체와 1:다 관계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-123">An application object therefore has a 1:1 relationship with the software application, and a 1:many relationship with its corresponding service principal object(s).</span></span>

<span data-ttu-id="c4987-124">응용 프로그램이 사용될 각 테넌트에 서비스 주체를 만들어서 테넌트가 보호하는 리소스에 대한 로그인 및/또는 액세스를 위한 ID를 설정할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-124">A service principal must be created in each tenant where the application will be used, enabling it to establish an identity for sign-in and/or access to resources being secured by the tenant.</span></span> <span data-ttu-id="c4987-125">단일 테넌트 응용 프로그램에는 해당 홈 테넌트에 하나의 서비스 주체만 있으며 일반적으로 응용 프로그램 등록 중에 생성하고 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-125">A single-tenant application will have only one service principal (in its home tenant), usually created and consented for use during application registration.</span></span> <span data-ttu-id="c4987-126">다중 테넌트 웹 응용 프로그램/API에도 해당 테넌트의 사용자가 사용을 동의한 각 테넌트에 생성된 하나의 서비스 주체가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-126">A multi-tenant Web application/API will also have a service principal created in each tenant where a user from that tenant has consented to its use.</span></span>  

> [!NOTE]
> <span data-ttu-id="c4987-127">응용 프로그램 개체에 대해 이뤄진 모든 변경은 또한 응용 프로그램의 홈 테넌트(그것이 등록된 테넌트)에만 있는 해당 서비스 주체 개체에도 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-127">Any changes you make to your application object, are also reflected in its service principal object in the application's home tenant only (the tenant where it was registered).</span></span> <span data-ttu-id="c4987-128">다중 테넌트 응용 프로그램의 경우 [응용 프로그램 액세스 패널](https://myapps.microsoft.com)을 통해 액세스를 제거하고 다시 액세스 권한이 부여될 때까지 응용 프로그램 개체의 변경 내용은 모든 소비자 테넌트의 서비스 주체 개체에 반영되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-128">For multi-tenant applications, changes to the application object are not reflected in any consumer tenants' service principal objects, until the access is removed via the [Application Access Panel](https://myapps.microsoft.com) and granted again.</span></span>
><br>  
> <span data-ttu-id="c4987-129">또한 기본적으로 네이티브 응용 프로그램이 다중 테넌트로 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-129">Also note that native applications are registered as multi-tenant by default.</span></span>
> 
> 

## <a name="example"></a><span data-ttu-id="c4987-130">예제</span><span class="sxs-lookup"><span data-stu-id="c4987-130">Example</span></span>
<span data-ttu-id="c4987-131">다음 다이어그램은 **HR 앱**이라는 샘플 다중 테넌트 응용 프로그램의 컨텍스트에서 응용 프로그램의 응용 프로그램 개체와 해당 서비스 주체 개체를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-131">The following diagram illustrates the relationship between an application's application object and corresponding service principal objects, in the context of a sample multi-tenant application called **HR app**.</span></span> <span data-ttu-id="c4987-132">이 시나리오에는 세 가지 Azure AD 테넌트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-132">There are three Azure AD tenants in this scenario:</span></span> 

* <span data-ttu-id="c4987-133">**Adatum** - **HR 앱**을 개발한 회사에서 사용하는 테넌트</span><span class="sxs-lookup"><span data-stu-id="c4987-133">**Adatum** - the tenant used by the company that developed the **HR app**</span></span>
* <span data-ttu-id="c4987-134">**Contoso** - **HR 앱**의 소비자인 Contoso 조직에서 사용하는 테넌트</span><span class="sxs-lookup"><span data-stu-id="c4987-134">**Contoso** - the tenant used by the Contoso organization, which is a consumer of the **HR app**</span></span>
* <span data-ttu-id="c4987-135">**Fabrikam** - **HR 앱**의 또 다른 소비자인 Fabrikam 조직에서 사용하는 테넌트</span><span class="sxs-lookup"><span data-stu-id="c4987-135">**Fabrikam** - the tenant used by the Fabrikam organization, which also consumes the **HR app**</span></span>

![응용 프로그램 개체 및 서비스 주체 개체 간의 관계](./media/active-directory-application-objects/application-objects-relationship.png)

<span data-ttu-id="c4987-137">위 다이어그램에서 1단계는 응용 프로그램의 홈 테넌트에서 응용 프로그램 및 서비스 주체 개체를 만드는 과정입니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-137">In the previous diagram, Step 1 is the process of creating the application and service principal objects in the application's home tenant.</span></span>

<span data-ttu-id="c4987-138">2단계에서 Contoso 관리자와 Fabrikam 관리자가 전적으로 동의한 경우 서비스 주체 개체가 회사의 Azure AD 테넌트에 생성되고 관리자가 부여한 사용 권한이 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-138">In Step 2, when Contoso and Fabrikam administrators complete consent, a service principal object is created in their company's Azure AD tenant and assigned the permissions that the administrator granted.</span></span> <span data-ttu-id="c4987-139">또한 사용자가 개별 사용에 대한 동의를 할 수 있게 HR 앱이 구성/설계될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-139">Also note that the HR app could be configured/designed to allow consent by users for individual use.</span></span>

<span data-ttu-id="c4987-140">3단계에서는 HR 응용 프로그램의 각 소비자 테넌트(예: Contoso 및 Fabrikam)에 고유한 서비스 주체 개체가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-140">In Step 3, the consumer tenants of the HR application (Contoso and Fabrikam) each have their own service principal object.</span></span> <span data-ttu-id="c4987-141">각각은 런타임에 응용 프로그램 인스턴스의 사용을 나타내며, 이는 해당 관리자가 동의한 사용 권한으로 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-141">Each represents their use of an instance of the application at runtime, governed by the permissions consented by the respective administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4987-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c4987-142">Next steps</span></span>
<span data-ttu-id="c4987-143">응용 프로그램의 응용 프로그램 개체는 OData [응용 프로그램 엔터티][AAD-Graph-App-Entity]에 의해 표시된 대로 Azure AD Graph API, [Azure Portal의][AZURE-Portal] 응용 프로그램 매니페스트 편집기 또는 [Azure AD PowerShell cmdlet](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0)을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-143">An application's application object can be accessed via the Azure AD Graph API, the [Azure portal's][AZURE-Portal] application manifest editor, or [Azure AD PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0), as represented by its OData [Application entity][AAD-Graph-App-Entity].</span></span>

<span data-ttu-id="c4987-144">응용 프로그램의 서비스 주체 개체는 OData [서비스 주체 엔터티][AAD-Graph-Sp-Entity]에 의해 표시된 대로 Azure AD Graph API 또는 [Azure AD PowerShell cmdlet](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0)을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-144">An application's service principal object can be accessed via the Azure AD Graph API or [Azure AD PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0), as represented by its OData [ServicePrincipal entity][AAD-Graph-Sp-Entity].</span></span>

<span data-ttu-id="c4987-145">[Azure AD Graph Explorer](https://graphexplorer.azurewebsites.net/)는 응용 프로그램 및 서비스 주체 개체 둘 다를 쿼리하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4987-145">The [Azure AD Graph Explorer](https://graphexplorer.azurewebsites.net/) is useful for querying both the application and service principal objects.</span></span>

<!--Image references-->

<!--Reference style links -->
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AZURE-Portal]: https://portal.azure.com
