---
title: "하이브리드 연결을 사용하여 Azure 앱 서비스의 웹 앱에서 온-프레미스 SQL Server에 연결"
description: "Microsoft Azure에서 웹 앱을 만들어 온-프레미스 SQL Server 데이터베이스에 연결"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: 2b4e0539-1a0b-4aa1-8a69-b4b053c3b2e5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: cephalin
ms.openlocfilehash: 12456ef3e2aecfa7a03cca97de2ff6ffd9602357
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-on-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a><span data-ttu-id="81bea-103">하이브리드 연결을 사용하여 Azure 앱 서비스의 웹 앱에서 온-프레미스 SQL Server에 연결</span><span class="sxs-lookup"><span data-stu-id="81bea-103">Connect to on-premises SQL Server from a web app in Azure App Service using Hybrid Connections</span></span>
<span data-ttu-id="81bea-104">하이브리드 연결은 정적 TCP 포트를 사용하는 온-프레미스 리소스에 [Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714) 웹 앱을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-104">Hybrid Connections can connect [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps to on-premises resources that use a static TCP port.</span></span> <span data-ttu-id="81bea-105">지원되는 리소스로는 Microsoft SQL Server, MySQL, HTTP 웹 API, App Service, 대부분의 사용자 지정 웹 서비스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-105">Supported resources include Microsoft SQL Server, MySQL, HTTP Web APIs, App Service, and most custom Web Services.</span></span>

<span data-ttu-id="81bea-106">이 자습서에서 [Azure 포털](http://go.microsoft.com/fwlink/?LinkId=529715)에서 앱 서비스 웹앱을 만들고, 새 하이브리드 연결 기능을 사용하여 로컬 온-프레미스 SQL Server 데이터베이스에 웹앱을 연결하고, 하이브리드 연결을 사용하는 단순한 ASP.NET 응용 프로그램을 만들고, 앱 서비스 웹앱에 응용 프로그램을 배포하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-106">In this tutorial, you will learn how to create an App Service web app in the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), connect the web app to your local on-premises SQL Server database using the new Hybrid Connection feature, create a simple ASP.NET application that will use the hybrid connection, and deploy the application to the App Service web app.</span></span> <span data-ttu-id="81bea-107">Azure의 완전한 웹 앱은 온-프레미스인 멤버 자격 데이터베이스에서 사용자 자격 증명을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-107">The completed web app on Azure stores user credentials in a membership database that is on-premises.</span></span> <span data-ttu-id="81bea-108">이 자습서는 이전에 Azure 또는 ASP.NET을 사용해 본 경험이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-108">The tutorial assumes no prior experience using Azure or ASP.NET.</span></span>

> [!NOTE]
> <span data-ttu-id="81bea-109">Azure 계정을 등록하기 전에 Azure App Service를 시작하려면 [App Service 체험](https://azure.microsoft.com/try/app-service/)으로 이동합니다. App Service에서 단기 스타터 웹앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-109">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="81bea-110">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-110">No credit cards required; no commitments.</span></span>
> 
> <span data-ttu-id="81bea-111">하이브리드 연결 기능의 웹 앱 부분은 [Azure 포털](https://portal.azure.com)에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-111">The Web Apps portion of the Hybrid Connections feature is available only in the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="81bea-112">BizTalk 서비스에서 연결을 만들려면 [하이브리드 연결](http://go.microsoft.com/fwlink/p/?LinkID=397274)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81bea-112">To create a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span>  
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="81bea-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="81bea-113">Prerequisites</span></span>
<span data-ttu-id="81bea-114">이 자습서를 완료하려면 다음 제품이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-114">To complete this tutorial, you'll need the following products.</span></span> <span data-ttu-id="81bea-115">모두 무료 버전으로 사용 가능할 수 있으므로, Azure용 개발을 완전히 무료로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-115">All are available in free versions, so you can start developing for Azure entirely for free.</span></span>

* <span data-ttu-id="81bea-116">**Azure 구독** - 무료 구독에 대해서는 [Azure 무료 평가](/pricing/free-trial/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81bea-116">**Azure subscription** - For a free subscription, see [Azure Free Trial](/pricing/free-trial/).</span></span>
* <span data-ttu-id="81bea-117">**Visual Studio 2013** - Visual Studio 2013의 무료 평가판 버전을 다운로드하려면 [Visual Studio 다운로드](http://www.visualstudio.com/downloads/download-visual-studio-vs)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81bea-117">**Visual Studio 2013** - To download a free trial version of Visual Studio 2013, see [Visual Studio Downloads](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span> <span data-ttu-id="81bea-118">계속하기 전에 이 제품을 설치하세요.</span><span class="sxs-lookup"><span data-stu-id="81bea-118">Install this before continuing.</span></span>
* <span data-ttu-id="81bea-119">**Microsoft .NET Framework 3.5 서비스 팩 1** - 운영 체제가 Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 또는 Windows Server 2008 R2인 경우 제어판 > 프로그램 및 기능 > Windows 기능 사용/사용 안 함에서 이 제품을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-119">**Microsoft .NET Framework 3.5 Service Pack 1** - If your operating system is Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7, or Windows Server 2008 R2, you can enable this in Control Panel > Programs and Features > Turn Windows features on or off.</span></span> <span data-ttu-id="81bea-120">그렇지 않은 경우 [Microsoft 다운로드 센터](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-120">Otherwise, you can download it from the [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span></span>
* <span data-ttu-id="81bea-121">**SQL Server 2014 Express with Tools** - [Microsoft 웹 플랫폼 데이터베이스 페이지](http://www.microsoft.com/web/platform/database.aspx)에서 Microsoft SQL Server Express를 무료로 다운로드하세요.</span><span class="sxs-lookup"><span data-stu-id="81bea-121">**SQL Server 2014 Express with Tools** - download Microsoft SQL Server Express for free at the [Microsoft Web Platform Database page](http://www.microsoft.com/web/platform/database.aspx).</span></span> <span data-ttu-id="81bea-122">**Express** (LocalDB가 아닌) 버전을 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="81bea-122">Choose the **Express** (not LocalDB) version.</span></span> <span data-ttu-id="81bea-123">**Express with Tools** 버전에는 이 자습서에서 사용할 SQL Server Management Studio가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-123">The **Express with Tools** version includes SQL Server Management Studio, which you will use in this tutorial.</span></span>
* <span data-ttu-id="81bea-124">**SQL Server Management Studio Express** - 이 제품은 위에서 언급한 SQL Server 2014 Express with Tools 다운로드와 함께 포함되지만 별도로 설치해야 하는 경우 [SQL Server Express 다운로드 페이지](http://www.microsoft.com/web/platform/database.aspx)에서 이 제품을 다운로드하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-124">**SQL Server Management Studio Express** - This is included with the SQL Server 2014 Express with Tools download mentioned above, but if you need to install it separately, you can download and install it from the [SQL Server Express download page](http://www.microsoft.com/web/platform/database.aspx).</span></span>

<span data-ttu-id="81bea-125">이 자습서에서는 사용자가 Azure 구독을 사용하며, Visual Studio 2013을 설치했고, .NET Framework 3.5을 설치했거나 사용하도록 설정했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-125">The tutorial assumes that you have an Azure subscription, that you have installed Visual Studio 2013, and that you have installed or enabled .NET Framework 3.5.</span></span> <span data-ttu-id="81bea-126">이 자습서에서는 Azure 하이브리드 연결 기능(정적 TCP 포트를 사용하는 기본 인스턴스)에서 적절히 작동하는 구성에 SQL Server 2014 Express를 설치하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-126">The tutorial shows you how to install SQL Server 2014 Express in a configuration that works well with the Azure Hybrid Connections feature (a default instance with a static TCP port).</span></span> <span data-ttu-id="81bea-127">자습서를 시작하기 전에 SQL Server를 설치하지 않은 경우 위에서 언급한 SQL Server 2014 Express with Tools를 다운로드하세요.</span><span class="sxs-lookup"><span data-stu-id="81bea-127">Before starting the tutorial, download SQL Server 2014 Express with Tools from the location mentioned above if you do not have SQL Server installed.</span></span>

### <a name="notes"></a><span data-ttu-id="81bea-128">참고 사항</span><span class="sxs-lookup"><span data-stu-id="81bea-128">Notes</span></span>
<span data-ttu-id="81bea-129">하이브리드 연결을 사용하여 온-프레미스 SQL Server 또는 SQL Server Express 데이터베이스를 사용하려면 TCP/IP를 고정 포트에서 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-129">To use an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs to be enabled on a static port.</span></span> <span data-ttu-id="81bea-130">SQL Server의 기본 인스턴스에서는 고정 포트 1433을 사용하는 반면 명명된 인스턴스에서는 이 포트를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-130">Default instances on SQL Server use static port 1433, whereas named instances do not.</span></span>

<span data-ttu-id="81bea-131">온-프레미스 하이브리드 연결 관리자 에이전트를 설치하는 컴퓨터는 다음 조건을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-131">The computer on which you install the on-premises Hybrid Connection Manager agent:</span></span>

* <span data-ttu-id="81bea-132">다음 포트를 통해 Azure와의 아웃바운드 연결이 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-132">Must have outbound connectivity to Azure over:</span></span>

| <span data-ttu-id="81bea-133">포트</span><span class="sxs-lookup"><span data-stu-id="81bea-133">Port</span></span> | <span data-ttu-id="81bea-134">이유</span><span class="sxs-lookup"><span data-stu-id="81bea-134">Why</span></span> |
| --- | --- |
| <span data-ttu-id="81bea-135">80</span><span class="sxs-lookup"><span data-stu-id="81bea-135">80</span></span> |<span data-ttu-id="81bea-136">**필요하며** 선택적으로 데이터 연결에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-136">**Required** for HTTP port for certificate validation and optionally for data connectivity.</span></span> |
| <span data-ttu-id="81bea-137">443</span><span class="sxs-lookup"><span data-stu-id="81bea-137">443</span></span> |<span data-ttu-id="81bea-138">**선택사항** 입니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-138">**Optional** for data connectivity.</span></span> <span data-ttu-id="81bea-139">443에 대한 아웃바운드 연결을 사용할 수 없으면 TCP 포트 80이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-139">If outbound connectivity to 443 is unavailable, TCP port 80 is used.</span></span> |
| <span data-ttu-id="81bea-140">5671 및 9352</span><span class="sxs-lookup"><span data-stu-id="81bea-140">5671 and 9352</span></span> |<span data-ttu-id="81bea-141">**권장** 하지만 선택사항입니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-141">**Recommended** but Optional for data connectivity.</span></span> <span data-ttu-id="81bea-142">이 모드를 사용하면 일반적으로 더 높은 처리량을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-142">Note this mode usually yields higher throughput.</span></span> <span data-ttu-id="81bea-143">이러한 포트에 대한 아웃바운드 연결을 사용할 수 없으면 TCP 포트 443이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-143">If outbound connectivity to these ports is unavailable, TCP port 443 is used.</span></span> |

* <span data-ttu-id="81bea-144">온-프레미스 리소스의 *ostname*에서 다음을 수행합니다.*포트번호* 에 연결할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-144">Must be able to reach the *hostname*:*portnumber* of your on-premises resource.</span></span>

<span data-ttu-id="81bea-145">이 자습서의 단계에서는 온-프레미스 하이브리드 연결 에이전트를 호스트하는 컴퓨터에서 브라우저를 사용하고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-145">The steps in this article assume that you are using the browser from the computer that will host the on-premises hybrid connection agent.</span></span>

<span data-ttu-id="81bea-146">위에서 설명한 조건을 충족하는 구성 및 환경으로 SQL Server를 이미 설치한 경우 건너뛰어서 [SQL Server 데이터베이스 온-프레미스](#CreateSQLDB)를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-146">If you already have SQL Server installed in a configuration and in an environment that meets the conditions described above, you can skip ahead and start with [Create a SQL Server database on-premises](#CreateSQLDB).</span></span>

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a><span data-ttu-id="81bea-147">A.</span><span class="sxs-lookup"><span data-stu-id="81bea-147">A.</span></span> <span data-ttu-id="81bea-148">SQL Server Express 설치, TCP/IP 사용 및 SQL Server 데이터베이스 온-프레미스 만들기</span><span class="sxs-lookup"><span data-stu-id="81bea-148">Install SQL Server Express, enable TCP/IP, and create a SQL Server database on-premises</span></span>
<span data-ttu-id="81bea-149">이 섹션에서는 웹 응용 프로그램이 Azure 포털에서 작동하도록 SQL Server Express를 설치하고, TCP/IP를 사용하도록 설정하고, 데이터베이스를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-149">This section shows you how to install SQL Server Express, enable TCP/IP, and create a database so that your web application will work with the Azure Portal.</span></span>

### <a name="install-sql-server-express"></a><span data-ttu-id="81bea-150">SQL Server Express 설치</span><span class="sxs-lookup"><span data-stu-id="81bea-150">Install SQL Server Express</span></span>
1. <span data-ttu-id="81bea-151">SQL Server Express를 설치하기 위해 다운로드한 **SQLEXPRWT_x64_ENU.exe** 또는 **SQLEXPR_x86_ENU.exe** 파일을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-151">To install SQL Server Express, run the **SQLEXPRWT_x64_ENU.exe** or **SQLEXPR_x86_ENU.exe** file that you downloaded.</span></span> <span data-ttu-id="81bea-152">SQL Server 설치 센터 마법사가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-152">The SQL Server Installation Center wizard appears.</span></span>
   
    ![SQL Server 설치][SQLServerInstall]
2. <span data-ttu-id="81bea-154">**새 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-154">Choose **New SQL Server stand-alone installation or add features to an existing installation**.</span></span> <span data-ttu-id="81bea-155">**인스턴스 구성** 페이지가 나타날 때까지 지침을 따라, 기본 선택 사항 및 설정을 그대로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-155">Follow the instructions, accepting the default choices and settings, until you get to the **Instance Configuration** page.</span></span>
3. <span data-ttu-id="81bea-156">**인스턴스 구성** 페이지에서 **기본 인스턴스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-156">On the **Instance Configuration** page, choose **Default instance**.</span></span>
   
    ![기본 인스턴스 선택][ChooseDefaultInstance]
   
    <span data-ttu-id="81bea-158">기본적으로, SQL Server의 기본 인스턴스는 하이브리드 연결 기능이 요구하는 고정 포트 1433을 통해 SQL Server 클라이언트의 요청을 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-158">By default, the default instance of SQL Server listens for requests from SQL Server clients on static port 1433, which is what the Hybrid Connections feature requires.</span></span> <span data-ttu-id="81bea-159">명명된 인스턴스는 하이브리드 연결에서 지원하지 않는 동적 포트 및 UDP를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-159">Named instances use dynamic ports and UDP, which are not supported by Hybrid Connections.</span></span>
4. <span data-ttu-id="81bea-160">**서버 구성** 페이지에서 기본값을 그대로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-160">Accept the defaults on the **Server Configuration** page.</span></span>
5. <span data-ttu-id="81bea-161">**데이터베이스 엔진 구성** 페이지의 **인증 모드**에서 **혼합 모드(SQL Server 인증 및 Windows 인증)**를 선택하고 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-161">On the **Database Engine Configuration** page, under **Authentication Mode**, choose **Mixed Mode (SQL Server authentication and Windows authentication)**, and provide a password.</span></span>
   
    ![혼합 모드 선택][ChooseMixedMode]
   
    <span data-ttu-id="81bea-163">이 자습서에서는 SQL Server 인증을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-163">In this tutorial, you will be using SQL Server authentication.</span></span> <span data-ttu-id="81bea-164">나중에 필요하므로, 입력하는 암호는 기억해 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-164">Be sure to remember the password that you provide, because you will need it later.</span></span>
6. <span data-ttu-id="81bea-165">마법사의 나머지 단계를 진행하여 설치를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-165">Step through the rest of the wizard to complete the installation.</span></span>

### <a name="enable-tcpip"></a><span data-ttu-id="81bea-166">TCP/IP 사용</span><span class="sxs-lookup"><span data-stu-id="81bea-166">Enable TCP/IP</span></span>
<span data-ttu-id="81bea-167">TCP/IP를 사용하도록 설정하려면 SQL Server Express를 설치할 때 설치된 SQL Server 구성 관리자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-167">To enable TCP/IP, you will use SQL Server Configuration Manager, which was installed when you installed SQL Server Express.</span></span> <span data-ttu-id="81bea-168">계속하기 전에 [SQL Server에 대한 TCP/IP 네트워크 프로토콜 사용](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) 의 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="81bea-168">Follow the steps in [Enable TCP/IP Network Protocol for SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) before continuing.</span></span>

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a><span data-ttu-id="81bea-169">SQL Server 데이터베이스 온-프레미스</span><span class="sxs-lookup"><span data-stu-id="81bea-169">Create a SQL Server database on-premises</span></span>
<span data-ttu-id="81bea-170">Visual Studio 웹 응용 프로그램을 사용하려면 Azure에서 액세스할 수 있는 멤버 자격 데이터베이스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-170">Your Visual Studio web application requires a membership database that can be accessed by Azure.</span></span> <span data-ttu-id="81bea-171">여기에는 SQL Server 또는 SQL Server Express 데이터베이스(기본적으로 MVC 템플릿에서 사용하는 LocalDB 데이터베이스 아님)가 필요하므로, 이제 멤버 자격 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-171">This requires a SQL Server or SQL Server Express database (not the LocalDB database that the MVC template uses by default), so you'll create the membership database next.</span></span>

1. <span data-ttu-id="81bea-172">SQL Server Management Studio에서 방금 설치한 SQL Server에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-172">In SQL Server Management Studio, connect to the SQL Server you just installed.</span></span> <span data-ttu-id="81bea-173">(**서버에 연결** 대화 상자가 자동으로 나타나지 않으면 왼쪽 창의 **개체 탐색기**로 이동하여 **연결**을 클릭한 후 **데이터베이스 엔진**을 클릭합니다.) ![서버에 연결][SSMSConnectToServer]</span><span class="sxs-lookup"><span data-stu-id="81bea-173">(If the **Connect to Server** dialog does not appear automatically, navigate to **Object Explorer** in the left pane, click **Connect**, and then click **Database Engine**.) ![Connect to Server][SSMSConnectToServer]</span></span>
   
    <span data-ttu-id="81bea-174">**서버 유형**으로 **데이터베이스 엔진**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-174">For **Server type**, choose **Database Engine**.</span></span> <span data-ttu-id="81bea-175">**서버 이름**으로 **localhost** 또는 사용 중인 컴퓨터의 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-175">For **Server name**, you can use **localhost** or the name of the computer that you are using.</span></span> <span data-ttu-id="81bea-176">**SQL Server 인증**을 선택한 다음 앞서 만든 사용자 이름 및 암호로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-176">Choose **SQL Server authentication**, and then log in with the sa user name and the password that you created earlier.</span></span>
2. <span data-ttu-id="81bea-177">SQL Server Management Studio를 사용하여 새 데이터베이스를 만들려면 개체 탐색기에서 **데이터베이스**를 마우스 오른쪽 단추로 클릭한 다음 **새 데이터베이스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-177">To create a new database by using SQL Server Management Studio, right-click **Databases** in Object Explorer, and then click **New Database**.</span></span>
   
    ![새 데이터베이스 만들기][SSMScreateNewDB]
3. <span data-ttu-id="81bea-179">**새 데이터베이스** 대화 상자에 데이터베이스 이름으로 MembershipDB를 입력한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-179">In the **New Database** dialog, enter MembershipDB for the database name, and then click **OK**.</span></span>
   
    ![데이터베이스 이름 입력][SSMSprovideDBname]
   
    <span data-ttu-id="81bea-181">여기서는 데이터베이스를 변경하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-181">Note that you do not make any changes to the database at this point.</span></span> <span data-ttu-id="81bea-182">나중에 웹 응용 프로그램을 실행할 때 멤버 자격 정보가 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-182">The membership information will be added automatically later by your web application when you run it.</span></span>
4. <span data-ttu-id="81bea-183">개체 탐색기에서 **데이터베이스**를 확장하면 멤버 자격 데이터베이스가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-183">In Object Explorer, if you expand **Databases**, you will see that the membership database has been created.</span></span>
   
    ![MembershipDB 생성됨][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="81bea-185">B.</span><span class="sxs-lookup"><span data-stu-id="81bea-185">B.</span></span> <span data-ttu-id="81bea-186">Azure 포털에서 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="81bea-186">Create a web app in the Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="81bea-187">이 자습서에서 사용하고자 하는 Azure 포털에서 웹앱을 이미 만들었다면, [하이브리드 연결 및 BizTalk 서비스 만들기](#CreateHC) 를 건너뛰고 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-187">If you have already created a web app in the Azure Portal that you want to use for this tutorial, you can skip ahead to [Create a Hybrid Connection and a BizTalk Service](#CreateHC) and continue from there.</span></span>
> 
> 

1. <span data-ttu-id="81bea-188">[Azure Portal](https://portal.azure.com)에서 **새로 만들기** > **웹 + 모바일** > **웹앱**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-188">In the [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web app**.</span></span>
   
    ![새 단추][New]
2. <span data-ttu-id="81bea-190">웹 앱을 구성하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-190">Configure your web app, and then click **Create**.</span></span>
   
    ![웹 사이트 이름][WebsiteCreationBlade]
3. <span data-ttu-id="81bea-192">잠시 후 웹 앱이 생성되고 웹 앱 블레이드가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-192">After a few moments, the web app is created and its web app blade appears.</span></span> <span data-ttu-id="81bea-193">블레이드는 세로로 스크롤 가능한 대시보드이며 여기서 웹 앱을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-193">The blade is a vertically scrollable dashboard that lets you manage your web app.</span></span>
   
    ![실행 중인 웹 사이트][WebSiteRunningBlade]
   
    <span data-ttu-id="81bea-195">웹 앱이 라이브인지 확인하려면 **찾아보기** 아이콘을 클릭하여 기본 페이지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-195">To verify the web app is live, you can click the **Browse** icon to display the default page.</span></span>

<span data-ttu-id="81bea-196">이제 웹 앱용 하이브리드 연결 및 BizTalk 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-196">Next, you will create a hybrid connection and a BizTalk service for the web app.</span></span>

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="81bea-197">C.</span><span class="sxs-lookup"><span data-stu-id="81bea-197">C.</span></span> <span data-ttu-id="81bea-198">하이브리드 연결 및 BizTalk 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="81bea-198">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="81bea-199">포털로 돌아와서 설정으로 이동하고 **네트워킹** > **하이브리드 연결 끝점 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-199">Back in the Portal, go to settings and click **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![하이브리드 연결][CreateHCHCIcon]
2. <span data-ttu-id="81bea-201">하이브리드 연결 블레이드에서 **추가** > **새 하이브리드 연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-201">On the Hybrid connections blade, click **Add** > **New hybrid connection**.</span></span>
3. <span data-ttu-id="81bea-202">**하이브리드 연결 블레이드 만들기** 에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-202">On the **Create hybrid connection** blade:</span></span>
   
   * <span data-ttu-id="81bea-203">**이름**에서 연결 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-203">For **Name**, provide a name for the connection.</span></span>
   * <span data-ttu-id="81bea-204">**호스트 이름**에 SQL Server 호스트 컴퓨터의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-204">For **Hostname**, enter the computer name of your SQL Server host computer.</span></span>
   * <span data-ttu-id="81bea-205">**포트**에, 1433(SQL Server의 기본 포트)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-205">For **Port**, enter 1433 (the default port for SQL Server).</span></span>
   * <span data-ttu-id="81bea-206">**BizTalk 서비스** > **새 BizTalk 서비스**를 클릭하고 BizTalk 서비스의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-206">Click **BizTalk Service** > **New BizTalk Service** and enter a name for the BizTalk service.</span></span>
     
     ![하이브리드 연결 만들기][TwinCreateHCBlades]
4. <span data-ttu-id="81bea-208">**확인** 을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-208">Click **OK** twice.</span></span>
   
    <span data-ttu-id="81bea-209">프로세스가 완료되면 **알림** 영역은 녹색 **성공**으로 깜박이며 **하이브리드 연결** 블레이드는 **연결 되지 않음** 상태와 함께 새 하이브리드 연결을 표시합니다 .</span><span class="sxs-lookup"><span data-stu-id="81bea-209">When the process completes, the **Notifications** area will flash a green **SUCCESS** and the **Hybrid connection** blade will show the new hybrid connection with the status as **Not connected**.</span></span>
   
    ![1개의 하이브리드 연결 생성됨][CreateHCOneConnectionCreated]

<span data-ttu-id="81bea-211">여기서 클라우드 하이브리드 연결 인프라의 중요한 부분을 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-211">At this point, you have completed an important part of the cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="81bea-212">이제 해당하는 온-프레미스 부분을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-212">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="d-install-the-on-premises-hybrid-connection-manager-to-complete-the-connection"></a><span data-ttu-id="81bea-213">D.</span><span class="sxs-lookup"><span data-stu-id="81bea-213">D.</span></span> <span data-ttu-id="81bea-214">온-프레미스 하이브리드 연결 관리자를 설치하여 연결 완료</span><span class="sxs-lookup"><span data-stu-id="81bea-214">Install the on-premises Hybrid Connection Manager to complete the connection</span></span>
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

<span data-ttu-id="81bea-215">하이브리드 연결 인프라를 완성했으므로 이 인프라를 사용하는 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-215">Now that the hybrid connection infrastructure is complete, you will create a web application that uses it.</span></span>

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-the-database-connection-string-and-run-the-project-locally"></a><span data-ttu-id="81bea-216">E.</span><span class="sxs-lookup"><span data-stu-id="81bea-216">E.</span></span> <span data-ttu-id="81bea-217">기본 ASP.NET 웹 프로젝트 만들기, 데이터베이스 연결 문자열 편집 및 로컬로 프로젝트 실행</span><span class="sxs-lookup"><span data-stu-id="81bea-217">Create a basic ASP.NET web project, edit the database connection string, and run the project locally</span></span>
### <a name="create-a-basic-aspnet-project"></a><span data-ttu-id="81bea-218">기본 ASP.NET 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="81bea-218">Create a basic ASP.NET project</span></span>
1. <span data-ttu-id="81bea-219">Visual Studio의 **파일** 메뉴에서 새 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-219">In Visual Studio, on the **File** menu, create a new Project:</span></span>
   
    ![새 Visual Studio 프로젝트][HCVSNewProject]
2. <span data-ttu-id="81bea-221">**새 프로젝트** 대화 상자의 **템플릿** 섹션에서 **웹**을 선택하고 **ASP.NET 웹 응용 프로그램**을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-221">In the **Templates** section of the **New Project** dialog, select **Web** and choose **ASP.NET Web Application**, and then click **OK**.</span></span>
   
    ![ASP.NET 웹 응용 프로그램 선택][HCVSChooseASPNET]
3. <span data-ttu-id="81bea-223">**새 ASP.NET 프로젝트** 대화 상자에서 **MVC**를 선택한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-223">In the **New ASP.NET Project** dialog, choose **MVC**, and then click **OK**.</span></span>
   
    ![MVC 선택][HCVSChooseMVC]
4. <span data-ttu-id="81bea-225">프로젝트를 만들 때 응용 프로그램 추가 정보 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-225">When the project has been created, the application readme page appears.</span></span> <span data-ttu-id="81bea-226">아직 웹 프로젝트를 실행하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="81bea-226">Do not run the web project yet.</span></span>
   
    ![추가 정보 페이지][HCVSReadmePage]

### <a name="edit-the-database-connection-string-for-the-application"></a><span data-ttu-id="81bea-228">응용 프로그램의 데이터베이스 연결 문자열 편집</span><span class="sxs-lookup"><span data-stu-id="81bea-228">Edit the database connection string for the application</span></span>
<span data-ttu-id="81bea-229">이 단계에서, 응용 프로그램에 로컬 SQL Server Express 데이터베이스를 찾을 수 있는 위치를 알려 주는 연결 문자열을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-229">In this step, you edit the connection string that tells your application where to find your local SQL Server Express database.</span></span> <span data-ttu-id="81bea-230">연결 문자열은 응용 프로그램에 대한 구성 정보를 포함하는 응용 프로그램의 Web.config 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-230">The connection string is in the application's Web.config file, which contains configuration information for the application.</span></span>

> [!NOTE]
> <span data-ttu-id="81bea-231">응용 프로그램이 Visual Studio의 기본 LocalDB에 있는 데이터베이스가 아닌 SQL Server Express에서 만든 데이터베이스를 사용하도록 하려면 프로젝트를 실행하기 전에 이 단계를 완료하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-231">To ensure that your application uses the database that you created in SQL Server Express, and not the one in Visual Studio's default LocalDB, it is important that you complete this step before running your project.</span></span>
> 
> 

1. <span data-ttu-id="81bea-232">솔루션 탐색기에서 Web.config 파일을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-232">In Solution Explorer, double-click the Web.config file.</span></span>
   
    ![Web.config][HCVSChooseWebConfig]
2. <span data-ttu-id="81bea-234">다음 예의 다음 구문과 같이 로컬 컴퓨터에서 SQL Server 데이터베이스를 가리키도록 **connectionStrings** 섹션을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-234">Edit the **connectionStrings** section to point to the SQL Server database on your local machine, following the syntax in the following example:</span></span>
   
    ![연결 문자열][HCVSConnectionString]
   
    <span data-ttu-id="81bea-236">연결 문자열을 작성할 때 다음 사항을 기억하세요.</span><span class="sxs-lookup"><span data-stu-id="81bea-236">When composing the connection string, keep in mind the following:</span></span>
   
   * <span data-ttu-id="81bea-237">기본 인스턴스(예: YourServer\SQLEXPRESS)가 아닌 명명된 인스턴스에 연결하는 경우 정적 포트를 사용하도록 SQL Server를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-237">If you are connecting to a named instance instead of a default instance (for example, YourServer\SQLEXPRESS), you must configure your SQL Server to use static ports.</span></span> <span data-ttu-id="81bea-238">정적 포트를 구성하는 방법에 대한 자세한 내용은 [특정 포트에서 수신하도록 SQL Server를 구성하는 방법](http://support.microsoft.com/kb/823938)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81bea-238">For information on configuring static ports, see [How to configure SQL Server to listen on a specific port](http://support.microsoft.com/kb/823938).</span></span> <span data-ttu-id="81bea-239">기본적으로, 명명된 인스턴는 하이브리드 연결에서 지원되지 않는 UDP 및 동적 포트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-239">By default, named instances use UDP and dynamic ports, which are not supported by Hybrid Connections.</span></span>
   * <span data-ttu-id="81bea-240">로컬 SQL Server가 TCP를 사용하도록 설정하고 올바른 포트를 사용하고 있는지 확인할 수 있도록 연결 문자열에서 포트(예와 같이 기본적으로는 1433)를 지정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-240">It is recommended that you specify the port (1433 by default, as shown in the example) on the connection string so that you can be sure that your local SQL Server has TCP enabled and is using the correct port.</span></span>
   * <span data-ttu-id="81bea-241">연결 문자열에 사용자 ID 및 암호를 지정하면서 SQL Server 인증을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="81bea-241">Remember to use SQL Server Authentication to connect, specifying the user ID and password in your connection string.</span></span>
3. <span data-ttu-id="81bea-242">Visual Studio에서 **저장** 을 클릭하여 Web.config 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-242">Click **Save** in Visual Studio to save the Web.config file.</span></span>

### <a name="run-the-project-locally-and-register-a-new-user"></a><span data-ttu-id="81bea-243">로컬로 프로젝트 실행 및 새 사용자 등록</span><span class="sxs-lookup"><span data-stu-id="81bea-243">Run the project locally and register a new user</span></span>
1. <span data-ttu-id="81bea-244">이제, 디버그 아래에 있는 찾아보기 단추를 클릭하여 새 웹 프로젝트를 로컬로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-244">Now, run your new web project locally by clicking the browse button under Debug.</span></span> <span data-ttu-id="81bea-245">이 예에서는 Internet Explorer를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-245">This example uses Internet Explorer.</span></span>
   
    ![프로젝트 실행][HCVSRunProject]
2. <span data-ttu-id="81bea-247">기본 웹 페이지의 오른쪽 위에서 **등록** 을 선택하여 새 계정을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-247">On the upper right of the default web page, choose **Register** to register a new account:</span></span>
   
    ![새 계정 등록][HCVSRegisterLocally]
3. <span data-ttu-id="81bea-249">사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-249">Enter a user name and password:</span></span>
   
    ![사용자 이름 및 암호를 입력합니다.][HCVSCreateNewAccount]
   
    <span data-ttu-id="81bea-251">그러면 로컬 SQL Server에 응용 프로그램의 멤버 자격 정보를 저장하는 데이터베이스가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-251">This automatically creates a database on your local SQL Server that holds the membership information for your application.</span></span> <span data-ttu-id="81bea-252">테이블(**dbo.AspNetUsers**) 중 하나는 방금 입력한 것과 같은 웹앱 사용자 자격 증명을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-252">One of the tables (**dbo.AspNetUsers**) holds web app user credentials like the ones that you just entered.</span></span> <span data-ttu-id="81bea-253">이 테이블은 자습서의 뒷부분에 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-253">You will see this table later in the tutorial.</span></span>
4. <span data-ttu-id="81bea-254">기본 웹 페이지의 브라우저 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-254">Close the browser window of the default web page.</span></span> <span data-ttu-id="81bea-255">그러면 Visual Studio에서 응용 프로그램이 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-255">This stops the application in Visual Studio.</span></span>

<span data-ttu-id="81bea-256">이제 Azure에 응용 프로그램을 게시하고 테스트하는 다음 단계를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-256">You are now ready for the next step, which is to publish the application to Azure and test it.</span></span>

<a name="PubNTest"></a>

## <a name="f-publish-the-web-application-to-azure-and-test-it"></a><span data-ttu-id="81bea-257">F.</span><span class="sxs-lookup"><span data-stu-id="81bea-257">F.</span></span> <span data-ttu-id="81bea-258">웹 응용 프로그램을 Azure에 게시하고 테스트</span><span class="sxs-lookup"><span data-stu-id="81bea-258">Publish the web application to Azure and test it</span></span>
<span data-ttu-id="81bea-259">이제, 앱 서비스 웹 앱에 응용 프로그램을 게시한 다음 테스트하여 로컬 컴퓨터의 데이터베이스에 웹 앱을 연결하는 데 앞서 구성한 하이브리드 연결을 사용하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-259">Now, you'll publish your application to your App Service web app and then test it to see how the hybrid connection you configured earlier is being used to connect your web app to the database on your local machine.</span></span>

### <a name="publish-the-web-application"></a><span data-ttu-id="81bea-260">웹 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="81bea-260">Publish the web application</span></span>
1. <span data-ttu-id="81bea-261">Azure 포털에서 앱 서비스 웹앱에 대한 게시 프로필을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-261">You can download your publishing profile for the App Service web app in the Azure Portal.</span></span> <span data-ttu-id="81bea-262">웹 앱의 블레이드에서 **게시 프로필 얻기**를 선택한 다음, 컴퓨터에 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-262">On the blade for your web app, click **Get publish profile**, and then save the file to your computer.</span></span>
   
    ![게시 프로필 다운로드][PortalDownloadPublishProfile]
   
    <span data-ttu-id="81bea-264">이제 이 파일을 Visual Studio 웹 응용 프로그램으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-264">Next, you will import this file into your Visual Studio web application.</span></span>
2. <span data-ttu-id="81bea-265">Visual Studio의 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-265">In Visual Studio, right-click the project name in Solution Explorer and select **Publish**.</span></span>
   
    ![게시 선택][HCVSRightClickProjectSelectPublish]
3. <span data-ttu-id="81bea-267">**웹 게시** 대화 상자의 **프로필** 탭에서 **가져오기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-267">In the **Publish Web** dialog, on the **Profile** tab, choose **Import**.</span></span>
   
    ![가져오기][HCVSPublishWebDialogImport]
4. <span data-ttu-id="81bea-269">다운로드한 게시 프로필로 이동하여, 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-269">Browse to your downloaded publishing profile, select it, and then click **OK**.</span></span>
   
    ![프로필로 이동][HCVSBrowseToImportPubProfile]
5. <span data-ttu-id="81bea-271">게시 정보를 가져와 대화 상자의 **연결** 탭에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-271">Your publishing information is imported and displays on the **Connection** tab of the dialog.</span></span>
   
    ![게시 클릭][HCVSClickPublish]
   
    <span data-ttu-id="81bea-273">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-273">Click **Publish**.</span></span>
   
    <span data-ttu-id="81bea-274">게시가 완료되면 브라우저가 시작되고 현재 Azure 클라우드에서 라이브라는 점을 제외하고는 이제 친숙한 ASP.NET 응용 프로그램이 표시됩니다!</span><span class="sxs-lookup"><span data-stu-id="81bea-274">When publishing completes, your browser will launch and show your now familiar ASP.NET application -- except that now it is live in the Azure cloud!</span></span>

<span data-ttu-id="81bea-275">이제 라이브 웹 응용 프로그램을 사용하여 작동 중인 하이브리드 연결을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-275">Next, you will use your live web application to see its Hybrid Connection in action.</span></span>

### <a name="test-the-completed-web-application-on-azure"></a><span data-ttu-id="81bea-276">Azure에서 완료된 웹 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="81bea-276">Test the completed web application on Azure</span></span>
1. <span data-ttu-id="81bea-277">Azure 웹 페이지의 맨 위 오른쪽에서 **로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-277">On the top right of your web page on Azure, choose **Log in**.</span></span>
   
    ![로그인 테스트][HCTestLogIn]
2. <span data-ttu-id="81bea-279">이제 앱 서비스 웹 앱이 로컬 컴퓨터에 있는 웹 응용 프로그램의 멤버 자격 데이터베이스에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-279">Your App Service web app is now connected to your web application's membership database on your local machine.</span></span> <span data-ttu-id="81bea-280">이를 확인하기 위해 앞서 로컬 데이터베이스에 입력한 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-280">To verify this, log in with the same credentials that you entered in the local database earlier.</span></span>
   
    ![Hello 인사][HCTestHelloContoso]
3. <span data-ttu-id="81bea-282">새 하이브리드 연결을 더 테스트하려면 Azure 웹 응용 프로그램을 로그오프하고 다른 사용자로 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-282">To further test your new hybrid connection, log off of your Azure web application and register as another user.</span></span> <span data-ttu-id="81bea-283">새 사용자 이름 및 암호를 입력한 다음 **등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-283">Provide a new user name and password, and then click **Register**.</span></span>
   
    ![다른 사용자 테스트 등록][HCTestRegisterRelecloud]
4. <span data-ttu-id="81bea-285">하이브리드 연결을 통해 새 사용자의 자격 증명이 로컬 데이터베이스에 저장되었는지 확인하려면 로컬 컴퓨터에 SQL Management Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-285">To verify that the new user's credentials have been stored in your local database through your hybrid connection, open SQL Management Studio on your local computer.</span></span> <span data-ttu-id="81bea-286">개체 탐색기에서 **MembershipDB** 데이터베이스를 확장한 다음 **테이블**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-286">In Object Explorer, expand the **MembershipDB** database, and then expand **Tables**.</span></span> <span data-ttu-id="81bea-287">**dbo.AspNetUsers** 멤버 자격 테이블을 마우스 오른쪽 단추로 클릭하고 **상위 1000개의 행 선택**을 선택하여 결과를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-287">Right-click the **dbo.AspNetUsers** membership table and choose **Select Top 1000 Rows** to view the results.</span></span>
   
    ![결과 보기][HCTestSSMSTree]
5. <span data-ttu-id="81bea-289">이제 로컬 멤버 자격 테이블이 로컬로 만든 계정과 Azure 클라우드에서 만든 계정을 모두 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-289">Your local membership table now shows both accounts - the one that you created locally, and the one that you created in the Azure cloud.</span></span> <span data-ttu-id="81bea-290">클라우드에서 만든 계정이 Azure의 하이브리드 연결 기능을 통해 온-프레미스 데이터베이스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-290">The one that you created in the cloud has been saved to your on-premises database through Azure's Hybrid Connection feature.</span></span>
   
    ![온-프레미스 데이터베이스에 등록된 사용자][HCTestShowMemberDb]

<span data-ttu-id="81bea-292">이제 Azure 클라우드의 웹 앱과 온-프레미스 SQL Server 간의 하이브리드 연결을 사용하는 ASP.NET 웹 응용 프로그램을 만들어 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-292">You have now created and deployed an ASP.NET web application that uses a hybrid connection between a web app in the Azure cloud and an on-premises SQL Server database.</span></span> <span data-ttu-id="81bea-293">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="81bea-293">Congratulations!</span></span>

## <a name="see-also"></a><span data-ttu-id="81bea-294">참고 항목</span><span class="sxs-lookup"><span data-stu-id="81bea-294">See Also</span></span>
[<span data-ttu-id="81bea-295">하이브리드 연결 개요</span><span class="sxs-lookup"><span data-stu-id="81bea-295">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="81bea-296">Josh Twist가 소개하는 하이브리드 연결(채널 9 비디오)(영문)</span><span class="sxs-lookup"><span data-stu-id="81bea-296">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="81bea-297">하이브리드 연결 개요</span><span class="sxs-lookup"><span data-stu-id="81bea-297">Hybrid Connections overview</span></span>](/services/biztalk-services/)

[<span data-ttu-id="81bea-298">BizTalk 서비스: 대시보드, 모니터, 확장, 구성 및 하이브리드 연결 탭</span><span class="sxs-lookup"><span data-stu-id="81bea-298">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="81bea-299">원활한 응용 프로그램 이식성으로 실시간 하이브리드 연결 클라우드 구축(채널 9 비디오)(영문)</span><span class="sxs-lookup"><span data-stu-id="81bea-299">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="81bea-300">Azure App Service에서 하이브리드 연결을 사용하여 온-프레미스 리소스에 액세스</span><span class="sxs-lookup"><span data-stu-id="81bea-300">Access on-premises resources using hybrid connections in Azure App Service</span></span>](web-sites-hybrid-connection-get-started.md)

[<span data-ttu-id="81bea-301">ASP.NET ID 개요(영문)</span><span class="sxs-lookup"><span data-stu-id="81bea-301">ASP.NET Identity Overview</span></span>](http://www.asp.net/identity)

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- IMAGES -->
[SQLServerInstall]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A01SQLServerInstall.png
[ChooseDefaultInstance]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A02ChooseDefaultInstance.png
[ChooseMixedMode]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A03ChooseMixedMode.png
[SSMSConnectToServer]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A04SSMSConnectToServer.png
[SSMScreateNewDB]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A05SSMScreateNewDBlh.png
[SSMSprovideDBname]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A06SSMSprovideDBname.png
[SSMSMembershipDBCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A07SSMSMembershipDBCreated.png
[New]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D10HCStatusConnected.png
[HCVSNewProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E01HCVSNewProject.png
[HCVSChooseASPNET]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E02HCVSChooseASPNET.png
[HCVSChooseMVC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E03HCVSChooseMVC.png
[HCVSReadmePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E04HCVSReadmePage.png
[HCVSChooseWebConfig]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E05HCVSChooseWebConfig.png
[HCVSConnectionString]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSConnectionString.png
[HCVSRunProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSRunProject.png
[HCVSRegisterLocally]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E07HCVSRegisterLocally.png
[HCVSCreateNewAccount]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E08HCVSCreateNewAccount.png
[PortalDownloadPublishProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F01PortalDownloadPublishProfile.png
[HCVSPublishProfileInDownloadsFolder]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F02HCVSPublishProfileInDownloadsFolder.png
[HCVSRightClickProjectSelectPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F03HCVSRightClickProjectSelectPublish.png
[HCVSPublishWebDialogImport]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F04HCVSPublishWebDialogImport.png
[HCVSBrowseToImportPubProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F05HCVSBrowseToImportPubProfile.png
[HCVSClickPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F06HCVSClickPublish.png
[HCTestLogIn]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F07HCTestLogIn.png
[HCTestHelloContoso]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F08HCTestHelloContoso.png
[HCTestRegisterRelecloud]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F09HCTestRegisterRelecloud.png
[HCTestSSMSTree]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F10HCTestSSMSTree.png
[HCTestShowMemberDb]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F11HCTestShowMemberDb.png
