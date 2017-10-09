---
title: "Visual Studio에서 연결 된 서비스를 사용 하 여 Azure Active Directory aaaAdding | Microsoft Docs"
description: "Hello Visual Studio 연결 된 서비스 추가 대화 상자를 사용 하 여 Azure Active Directory 추가"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f599de6b-e369-436f-9cdc-48a0165684cb
ms.service: active-directory
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: kraigb
ms.openlocfilehash: 26c8f68edf9ec5f7bf65cbab34e4f9b4085ed18d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-an-azure-active-directory-by-using-connected-services-in-visual-studio"></a><span data-ttu-id="078cf-103">Visual Studio에서 연결된 서비스를 사용하여 Azure Active Directory 추가</span><span class="sxs-lookup"><span data-stu-id="078cf-103">Adding an Azure Active Directory by using Connected Services in Visual Studio</span></span>
<span data-ttu-id="078cf-104">Azure Active Directory(Azure AD)를 사용하여 ASP.NET MVC 웹 응용 프로그램 또는 웹 API 서비스에서 Active Directory 인증을 위한 SSO(Single Sign-on)을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="078cf-104">By using Azure Active Directory (Azure AD), you can support Single Sign-On (SSO) for ASP.NET MVC web applications, or Active Directory Authentication in Web API services.</span></span> <span data-ttu-id="078cf-105">Azure Active Directory 인증 사용자가 Azure Active Directory tooconnect tooyour 웹 응용 프로그램에서 자신의 계정을 사용 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="078cf-105">With Azure Active Directory Authentication, your users can use their accounts from Azure Active Directory tooconnect tooyour web applications.</span></span> <span data-ttu-id="078cf-106">hello 웹 API와 Azure Active Directory 인증의 이점 중 데이터 보안을 강화할된 웹 응용 프로그램에서 API를 노출 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="078cf-106">hello advantages of Azure Active Directory Authentication with Web API include enhanced data security when exposing an API from a web application.</span></span> <span data-ttu-id="078cf-107">Azure AD와 않아도 toomanage 자체 계정 및 사용자 관리를 사용 하는 별도 인증 시스템.</span><span class="sxs-lookup"><span data-stu-id="078cf-107">With Azure AD, you do not have toomanage a separate authentication system with its own account and user management.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="078cf-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="078cf-108">Prerequisites</span></span>
- <span data-ttu-id="078cf-109">Azure 계정 - Azure 계정이 없는 경우 [평가판을 등록](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)하거나 [Visual Studio 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="078cf-109">Azure account - If you don't have an Azure account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

### <a name="connect-tooazure-active-directory-using-hello-connected-services-dialog"></a><span data-ttu-id="078cf-110">TooAzure hello 연결 된 서비스를 사용 하 여 Active Directory 연결 대화 상자</span><span class="sxs-lookup"><span data-stu-id="078cf-110">Connect tooAzure Active Directory using hello Connected Services dialog</span></span>
1. <span data-ttu-id="078cf-111">Visual Studio에서 ASP.NET MVC 프로젝트 또는 ASP.NET Web API 프로젝트를 만들거나 엽니다.</span><span class="sxs-lookup"><span data-stu-id="078cf-111">In Visual Studio, create or open an ASP.NET MVC project, or an ASP.NET Web API project.</span></span>

1. <span data-ttu-id="078cf-112">Hello 솔루션 탐색기에서에서 마우스 오른쪽 단추로 클릭 hello **연결 된 서비스** 노드를 hello 상황에 맞는 메뉴에서 **연결 된 서비스 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="078cf-112">From hello Solution Explorer, right-click hello **Connected Services** node, and, from hello context menu, select **Add Connected Services**.</span></span>

1. <span data-ttu-id="078cf-113">Hello에 **연결 된 서비스** 페이지에서 **Azure Active directory 인증**합니다.</span><span class="sxs-lookup"><span data-stu-id="078cf-113">On hello **Connected Services** page, select **Authentication with Azure Active Directory**.</span></span>
   
    ![연결된 서비스 페이지](./media/vs-azure-tools-connected-services-add-active-directory/connected-services-add-active-directory.png)

1. <span data-ttu-id="078cf-115">Hello에 **소개** hello 페이지 **Azure AD 인증 구성** 선택 마법사 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="078cf-115">On hello **Introduction** page of hello **Configure Azure AD Authentication** wizard, select **Next**.</span></span>
   
    ![소개 페이지](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-1.png)

1. <span data-ttu-id="078cf-117">Hello에 **Single-sign On** hello 페이지 **Azure AD 인증 구성** hello에서 도메인을 선택 마법사 **도메인** 드롭 다운 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="078cf-117">On hello **Single-Sign On** page of hello **Configure Azure AD Authentication** wizard, select a domain from hello **Domain** drop-down list.</span></span> <span data-ttu-id="078cf-118">도메인 목록 hello hello 계정 설정 대화 상자에 나열 된 hello 계정으로 액세스할 수 있는 모든 도메인을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="078cf-118">hello list of domains contains all domains accessible by hello accounts listed in hello Account Settings dialog.</span></span> <span data-ttu-id="078cf-119">입력할 수 있는 도메인 이름을 찾을 수 없는 경우 hello 찾고와 같은 하나 `mydomain.onmicrosoft.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="078cf-119">As an alternative, you can enter a domain name if you don’t find hello one you’re looking for, such as `mydomain.onmicrosoft.com`.</span></span> <span data-ttu-id="078cf-120">기존 Azure Active Directory 응용 프로그램에서 hello 설정을 사용 하거나 hello 옵션 toocreate Azure Active Directory 응용 프로그램을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="078cf-120">You can choose hello option toocreate an Azure Active Directory app or use hello settings from an existing Azure Active Directory app.</span></span> <span data-ttu-id="078cf-121">완료되면 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="078cf-121">Select **Next** when done.</span></span>
   
    ![Single Sign-On 페이지](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-2.png)

1. <span data-ttu-id="078cf-123">Hello에 **디렉터리 액세스** hello 페이지 **Azure AD 인증 구성** 마법사에서 해당 hello 확인 **디렉터리 데이터 읽기** 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="078cf-123">On hello **Directory Access** page of hello **Configure Azure AD Authentication** wizard, ensure that hello **Read directory data** option is checked.</span></span> 
   
    ![디렉터리 액세스 페이지](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-3.png)

1. <span data-ttu-id="078cf-125">선택 **마침** tooadd hello 필요한 구성 코드 및 참조 tooenable Azure AD 인증을 위한 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="078cf-125">Select **Finish** tooadd hello necessary configuration code and references tooenable your project for Azure AD authentication.</span></span> <span data-ttu-id="078cf-126">Hello에서 hello Active Directory 도메인을 확인할 수 있습니다 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.</span><span class="sxs-lookup"><span data-stu-id="078cf-126">You can see hello Active Directory domain on hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="078cf-127">Visual Studio에 표시 됩니다는 [무슨 상황이 발생](#how-your-project-is-modified) 문서 tooshow 프로젝트의 수정 방법을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="078cf-127">Visual Studio will display a [What Happened](#how-your-project-is-modified) article tooshow you how your project was modified.</span></span> <span data-ttu-id="078cf-128">모두 제대로 작동 toocheck 하려는 경우 hello 수정한 구성 파일 중 하나가 열고 hello 문서에 언급 된 hello 설정이 있는 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="078cf-128">If you want toocheck that everything worked, open one of hello modified configuration files and verify that hello settings mentioned in hello article are there.</span></span> 

## <a name="how-your-project-is-modified"></a><span data-ttu-id="078cf-129">프로젝트를 수정하는 방법</span><span class="sxs-lookup"><span data-stu-id="078cf-129">How your project is modified</span></span>
<span data-ttu-id="078cf-130">Hello 마법사를 실행 하면 Visual Studio는 Azure Active Directory 및 연관 된 참조 tooyour 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="078cf-130">When you run hello wizard, Visual Studio adds Azure Active Directory and associated references tooyour project.</span></span> <span data-ttu-id="078cf-131">구성 파일 및 코드 프로젝트의 파일에에서 Azure AD에 대 한 수정 된 tooadd 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="078cf-131">Configuration files and code files in your project are also modified tooadd support for Azure AD.</span></span> <span data-ttu-id="078cf-132">Visual Studio에서는 hello 특정 수정 내용을 hello 프로젝트 형식에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="078cf-132">hello specific modifications that Visual Studio makes depend on hello project type.</span></span> <span data-ttu-id="078cf-133">ASP.NET MVC 프로젝트를 수정하는 방법에 대한 자세한 정보는 [변경된 내용 – MVC 프로젝트](http://go.microsoft.com/fwlink/p/?LinkID=513809)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="078cf-133">For detailed information about how ASP.NET MVC projects are modified, see [What happened– MVC Projects](http://go.microsoft.com/fwlink/p/?LinkID=513809).</span></span> <span data-ttu-id="078cf-134">웹 API 프로젝트는 [변경된 내용 - 웹 API 프로젝트](http://go.microsoft.com/fwlink/p/?LinkId=513810)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="078cf-134">For Web API projects, see [What happened – Web API Projects](http://go.microsoft.com/fwlink/p/?LinkId=513810).</span></span>

## <a name="next-steps"></a><span data-ttu-id="078cf-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="078cf-135">Next steps</span></span>
* [<span data-ttu-id="078cf-136">Azure Active Directory에 대한 MSDN 포럼</span><span class="sxs-lookup"><span data-stu-id="078cf-136">MSDN Forum for Azure Active Directory</span></span>](https://social.msdn.microsoft.com/forums/azure/home?forum=WindowsAzureAD)
* [<span data-ttu-id="078cf-137">Azure Active Directory 설명서</span><span class="sxs-lookup"><span data-stu-id="078cf-137">Azure Active Directory Documentation</span></span>](https://azure.microsoft.com/documentation/services/active-directory/)
* [<span data-ttu-id="078cf-138">블로그 게시물: 소개 tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="078cf-138">Blog Post: Intro tooAzure Active Directory</span></span>](http://blogs.msdn.com/b/brunoterkaly/archive/2014/03/03/introduction-to-windows-azure-active-directory.aspx)

