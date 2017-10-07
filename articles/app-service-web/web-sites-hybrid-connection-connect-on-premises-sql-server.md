---
title: "aaaConnect 하이브리드 연결을 사용 하 여 Azure 앱 서비스의 웹 앱에서 tooon 온-프레미스 SQL Server"
description: "Microsoft Azure에 웹 응용 프로그램을 만들고 tooan 온-프레미스 SQL Server 데이터베이스 연결"
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
ms.openlocfilehash: 2e8f8f7e0b9733cfb0433697615faba4358c6023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a><span data-ttu-id="c1a95-103">하이브리드 연결을 사용 하 여 Azure 앱 서비스의 웹 앱에서 tooon 온-프레미스 SQL Server 연결</span><span class="sxs-lookup"><span data-stu-id="c1a95-103">Connect tooon-premises SQL Server from a web app in Azure App Service using Hybrid Connections</span></span>
<span data-ttu-id="c1a95-104">하이브리드 연결은 연결 수 [Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714) 정적 TCP 포트를 사용 하는 웹 응용 프로그램 tooon 온-프레미스 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-104">Hybrid Connections can connect [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps tooon-premises resources that use a static TCP port.</span></span> <span data-ttu-id="c1a95-105">지원되는 리소스로는 Microsoft SQL Server, MySQL, HTTP 웹 API, App Service, 대부분의 사용자 지정 웹 서비스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-105">Supported resources include Microsoft SQL Server, MySQL, HTTP Web APIs, App Service, and most custom Web Services.</span></span>

<span data-ttu-id="c1a95-106">이 자습서에 설명 합니다 방법을 toocreate 앱 서비스 웹 앱 hello에 [Azure 포털](http://go.microsoft.com/fwlink/?LinkId=529715), hello 새 하이브리드 연결 기능을 사용 하 여 hello 웹 응용 프로그램 tooyour 로컬 온-프레미스 SQL Server 데이터베이스를 연결, 간단한 ASP.NET 만들기 hello 하이브리드 연결을 사용 하 고 hello 응용 프로그램 toohello 앱 서비스 웹 앱을 배포 하는 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-106">In this tutorial, you will learn how toocreate an App Service web app in hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), connect hello web app tooyour local on-premises SQL Server database using hello new Hybrid Connection feature, create a simple ASP.NET application that will use hello hybrid connection, and deploy hello application toohello App Service web app.</span></span> <span data-ttu-id="c1a95-107">Azure에서 웹 응용 프로그램을 완료 하는 hello 온 프레미스에 있는 멤버 자격 데이터베이스에 사용자 자격 증명을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-107">hello completed web app on Azure stores user credentials in a membership database that is on-premises.</span></span> <span data-ttu-id="c1a95-108">hello 자습서에서는 Azure 또는 ASP.NET을 사용 하 여 이전 본 경험이 없는 사용자 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-108">hello tutorial assumes no prior experience using Azure or ASP.NET.</span></span>

> [!NOTE]
> <span data-ttu-id="c1a95-109">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-109">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="c1a95-110">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-110">No credit cards required; no commitments.</span></span>
> 
> <span data-ttu-id="c1a95-111">hello 하이브리드 연결 기능은의 hello 웹 응용 프로그램 부분은 hello에만 사용할 수 있는 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-111">hello Web Apps portion of hello Hybrid Connections feature is available only in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="c1a95-112">BizTalk 서비스의 연결 toocreate 참조 [하이브리드 연결](http://go.microsoft.com/fwlink/p/?LinkID=397274)합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-112">toocreate a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span>  
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="c1a95-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c1a95-113">Prerequisites</span></span>
<span data-ttu-id="c1a95-114">toocomplete이이 자습서에서는 다음 제품 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-114">toocomplete this tutorial, you'll need hello following products.</span></span> <span data-ttu-id="c1a95-115">모두 무료 버전으로 사용 가능할 수 있으므로, Azure용 개발을 완전히 무료로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-115">All are available in free versions, so you can start developing for Azure entirely for free.</span></span>

* <span data-ttu-id="c1a95-116">**Azure 구독** - 무료 구독에 대해서는 [Azure 무료 평가](/pricing/free-trial/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c1a95-116">**Azure subscription** - For a free subscription, see [Azure Free Trial](/pricing/free-trial/).</span></span>
* <span data-ttu-id="c1a95-117">**Visual Studio 2013** -toodownload Visual Studio 2013의 무료 평가판 버전 참조 [Visual Studio 다운로드](http://www.visualstudio.com/downloads/download-visual-studio-vs)합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-117">**Visual Studio 2013** - toodownload a free trial version of Visual Studio 2013, see [Visual Studio Downloads](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span> <span data-ttu-id="c1a95-118">계속하기 전에 이 제품을 설치하세요.</span><span class="sxs-lookup"><span data-stu-id="c1a95-118">Install this before continuing.</span></span>
* <span data-ttu-id="c1a95-119">**Microsoft .NET Framework 3.5 서비스 팩 1** - 운영 체제가 Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 또는 Windows Server 2008 R2인 경우 제어판 > 프로그램 및 기능 > Windows 기능 사용/사용 안 함에서 이 제품을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-119">**Microsoft .NET Framework 3.5 Service Pack 1** - If your operating system is Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7, or Windows Server 2008 R2, you can enable this in Control Panel > Programs and Features > Turn Windows features on or off.</span></span> <span data-ttu-id="c1a95-120">그렇지 않으면 hello에서 다운로드할 수 [Microsoft 다운로드 센터](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22)합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-120">Otherwise, you can download it from hello [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span></span>
* <span data-ttu-id="c1a95-121">**SQL Server 2014 Express with Tools** -Microsoft SQL Server Express를 무료로 다운로드 hello에 [Microsoft 웹 플랫폼 데이터베이스 페이지](http://www.microsoft.com/web/platform/database.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-121">**SQL Server 2014 Express with Tools** - download Microsoft SQL Server Express for free at hello [Microsoft Web Platform Database page](http://www.microsoft.com/web/platform/database.aspx).</span></span> <span data-ttu-id="c1a95-122">Hello 선택 **Express** (LocalDB) 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-122">Choose hello **Express** (not LocalDB) version.</span></span> <span data-ttu-id="c1a95-123">hello **Express with Tools** 버전에 사용 하는이 자습서에서는 SQL Server Management Studio에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-123">hello **Express with Tools** version includes SQL Server Management Studio, which you will use in this tutorial.</span></span>
* <span data-ttu-id="c1a95-124">**SQL Server Management Studio Express** -이 앞에서 설명한 도구 다운로드와 함께 SQL Server 2014 Express hello에 포함 된 하지만 tooinstall 해야 할 경우 것을 별도로 다운로드 하 수 hello에서 설치 [SQL Server Express 다운로드 페이지](http://www.microsoft.com/web/platform/database.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-124">**SQL Server Management Studio Express** - This is included with hello SQL Server 2014 Express with Tools download mentioned above, but if you need tooinstall it separately, you can download and install it from hello [SQL Server Express download page](http://www.microsoft.com/web/platform/database.aspx).</span></span>

<span data-ttu-id="c1a95-125">hello 자습서는 Azure 구독을 Visual Studio 2013을 설치 해야 하 고 설치 하거나.NET Framework 3.5를 사용 하도록 설정 했으면 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-125">hello tutorial assumes that you have an Azure subscription, that you have installed Visual Studio 2013, and that you have installed or enabled .NET Framework 3.5.</span></span> <span data-ttu-id="c1a95-126">hello 자습서 hello Azure 하이브리드 연결에 사용할 수 있는 구성에서 SQL Server 2014 Express tooinstall (정적 TCP 포트를 기본 인스턴스)을 기능 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-126">hello tutorial shows you how tooinstall SQL Server 2014 Express in a configuration that works well with hello Azure Hybrid Connections feature (a default instance with a static TCP port).</span></span> <span data-ttu-id="c1a95-127">Hello 자습서를 시작 하기 전에 SQL Server가 설치 되지 않은 경우 위에서 언급 한 hello 위치에서 SQL Server 2014 Express with Tools를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-127">Before starting hello tutorial, download SQL Server 2014 Express with Tools from hello location mentioned above if you do not have SQL Server installed.</span></span>

### <a name="notes"></a><span data-ttu-id="c1a95-128">참고 사항</span><span class="sxs-lookup"><span data-stu-id="c1a95-128">Notes</span></span>
<span data-ttu-id="c1a95-129">toouse 온-프레미스 SQL Server 또는 SQL Server Express 데이터베이스 하이브리드 연결 된 TCP/IP toobe 고정 포트에서 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-129">toouse an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs toobe enabled on a static port.</span></span> <span data-ttu-id="c1a95-130">SQL Server의 기본 인스턴스에서는 고정 포트 1433을 사용하는 반면 명명된 인스턴스에서는 이 포트를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-130">Default instances on SQL Server use static port 1433, whereas named instances do not.</span></span>

<span data-ttu-id="c1a95-131">hello 온-프레미스 하이브리드 연결 관리자 에이전트를 설치 하는 hello 컴퓨터:</span><span class="sxs-lookup"><span data-stu-id="c1a95-131">hello computer on which you install hello on-premises Hybrid Connection Manager agent:</span></span>

* <span data-ttu-id="c1a95-132">통해 아웃 바운드 연결 tooAzure 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-132">Must have outbound connectivity tooAzure over:</span></span>

| <span data-ttu-id="c1a95-133">포트</span><span class="sxs-lookup"><span data-stu-id="c1a95-133">Port</span></span> | <span data-ttu-id="c1a95-134">이유</span><span class="sxs-lookup"><span data-stu-id="c1a95-134">Why</span></span> |
| --- | --- |
| <span data-ttu-id="c1a95-135">80</span><span class="sxs-lookup"><span data-stu-id="c1a95-135">80</span></span> |<span data-ttu-id="c1a95-136">**필요하며** 선택적으로 데이터 연결에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-136">**Required** for HTTP port for certificate validation and optionally for data connectivity.</span></span> |
| <span data-ttu-id="c1a95-137">443</span><span class="sxs-lookup"><span data-stu-id="c1a95-137">443</span></span> |<span data-ttu-id="c1a95-138">**선택사항** 입니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-138">**Optional** for data connectivity.</span></span> <span data-ttu-id="c1a95-139">아웃 바운드 연결 too443 사용할 수 없는 경우 TCP 포트 80이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-139">If outbound connectivity too443 is unavailable, TCP port 80 is used.</span></span> |
| <span data-ttu-id="c1a95-140">5671 및 9352</span><span class="sxs-lookup"><span data-stu-id="c1a95-140">5671 and 9352</span></span> |<span data-ttu-id="c1a95-141">**권장** 하지만 선택사항입니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-141">**Recommended** but Optional for data connectivity.</span></span> <span data-ttu-id="c1a95-142">이 모드를 사용하면 일반적으로 더 높은 처리량을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-142">Note this mode usually yields higher throughput.</span></span> <span data-ttu-id="c1a95-143">아웃 바운드 연결 toothese 포트를 사용할 수 없는 경우에 TCP 포트 443 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-143">If outbound connectivity toothese ports is unavailable, TCP port 443 is used.</span></span> |

* <span data-ttu-id="c1a95-144">수 tooreach hello 있어야 *hostname*:*portnumber* 온-프레미스 리소스의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-144">Must be able tooreach hello *hostname*:*portnumber* of your on-premises resource.</span></span>

<span data-ttu-id="c1a95-145">이 문서의 단계 hello hello 브라우저 hello 온-프레미스 하이브리드 연결 에이전트를 호스트 하는 hello 컴퓨터에서 사용 하는 것을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-145">hello steps in this article assume that you are using hello browser from hello computer that will host hello on-premises hybrid connection agent.</span></span>

<span data-ttu-id="c1a95-146">구성에서 하 고 위에서 설명한 hello 조건을 충족 하는 환경에서 설치 된 SQL Server를 이미 있는 경우에 바로 이동 하 고으로 시작할 수 있습니다 [온-프레미스 SQL Server 데이터베이스를 만들](#CreateSQLDB)합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-146">If you already have SQL Server installed in a configuration and in an environment that meets hello conditions described above, you can skip ahead and start with [Create a SQL Server database on-premises](#CreateSQLDB).</span></span>

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a><span data-ttu-id="c1a95-147">A.</span><span class="sxs-lookup"><span data-stu-id="c1a95-147">A.</span></span> <span data-ttu-id="c1a95-148">SQL Server Express 설치, TCP/IP 사용 및 SQL Server 데이터베이스 온-프레미스 만들기</span><span class="sxs-lookup"><span data-stu-id="c1a95-148">Install SQL Server Express, enable TCP/IP, and create a SQL Server database on-premises</span></span>
<span data-ttu-id="c1a95-149">이 섹션 tooinstall SQL Server Express에서 TCP/IP를 활성화 하 고 웹 응용 프로그램은 Azure 포털 hello로 작동할 수 있도록 데이터베이스를 만들 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-149">This section shows you how tooinstall SQL Server Express, enable TCP/IP, and create a database so that your web application will work with hello Azure Portal.</span></span>

### <a name="install-sql-server-express"></a><span data-ttu-id="c1a95-150">SQL Server Express 설치</span><span class="sxs-lookup"><span data-stu-id="c1a95-150">Install SQL Server Express</span></span>
1. <span data-ttu-id="c1a95-151">SQL Server Express tooinstall hello 실행 **SQLEXPRWT_x64_ENU.exe** 또는 **SQLEXPR_x86_ENU.exe** 다운로드 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-151">tooinstall SQL Server Express, run hello **SQLEXPRWT_x64_ENU.exe** or **SQLEXPR_x86_ENU.exe** file that you downloaded.</span></span> <span data-ttu-id="c1a95-152">hello SQL Server 설치 센터 마법사가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-152">hello SQL Server Installation Center wizard appears.</span></span>
   
    ![SQL Server 설치][SQLServerInstall]
2. <span data-ttu-id="c1a95-154">선택 **새 SQL Server 독립 실행형 설치 또는 추가 기능 tooan 기존 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-154">Choose **New SQL Server stand-alone installation or add features tooan existing installation**.</span></span> <span data-ttu-id="c1a95-155">Toohello에 도달할 때까지 hello 기본 선택 항목 및 설정을 적용 하는 hello 지침에 따라 **인스턴스 구성** 페이지.</span><span class="sxs-lookup"><span data-stu-id="c1a95-155">Follow hello instructions, accepting hello default choices and settings, until you get toohello **Instance Configuration** page.</span></span>
3. <span data-ttu-id="c1a95-156">Hello에 **인스턴스 구성** 페이지에서 선택 **기본 인스턴스**합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-156">On hello **Instance Configuration** page, choose **Default instance**.</span></span>
   
    ![기본 인스턴스 선택][ChooseDefaultInstance]
   
    <span data-ttu-id="c1a95-158">기본적으로 SQL Server의 기본 인스턴스 hello 하는 어떤 hello 하이브리드 연결 기능을 사용 하려면 정적 포트 1433에서 SQL Server 클라이언트의 요청에 대 한 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-158">By default, hello default instance of SQL Server listens for requests from SQL Server clients on static port 1433, which is what hello Hybrid Connections feature requires.</span></span> <span data-ttu-id="c1a95-159">명명된 인스턴스는 하이브리드 연결에서 지원하지 않는 동적 포트 및 UDP를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-159">Named instances use dynamic ports and UDP, which are not supported by Hybrid Connections.</span></span>
4. <span data-ttu-id="c1a95-160">Hello에 hello 기본값을 적용 **서버 구성** 페이지.</span><span class="sxs-lookup"><span data-stu-id="c1a95-160">Accept hello defaults on hello **Server Configuration** page.</span></span>
5. <span data-ttu-id="c1a95-161">Hello에 **데이터베이스 엔진 구성** 페이지의 **인증 모드**, 선택 **혼합 모드 (SQL Server 인증 및 Windows 인증)**, 제공 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-161">On hello **Database Engine Configuration** page, under **Authentication Mode**, choose **Mixed Mode (SQL Server authentication and Windows authentication)**, and provide a password.</span></span>
   
    ![혼합 모드 선택][ChooseMixedMode]
   
    <span data-ttu-id="c1a95-163">이 자습서에서는 SQL Server 인증을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-163">In this tutorial, you will be using SQL Server authentication.</span></span> <span data-ttu-id="c1a95-164">사용자가 제공한 있는지 tooremember hello 암호 때문일 나중에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-164">Be sure tooremember hello password that you provide, because you will need it later.</span></span>
6. <span data-ttu-id="c1a95-165">Hello 마법사 toocomplete hello 설치 hello 나머지 단계별로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-165">Step through hello rest of hello wizard toocomplete hello installation.</span></span>

### <a name="enable-tcpip"></a><span data-ttu-id="c1a95-166">TCP/IP 사용</span><span class="sxs-lookup"><span data-stu-id="c1a95-166">Enable TCP/IP</span></span>
<span data-ttu-id="c1a95-167">TCP/IP tooenable SQL Server Express를 설치할 때 설치 된 SQL Server 구성 관리자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-167">tooenable TCP/IP, you will use SQL Server Configuration Manager, which was installed when you installed SQL Server Express.</span></span> <span data-ttu-id="c1a95-168">Hello 단계에 따라 [SQL Server에 대 한 TCP/IP 네트워크 프로토콜을 사용 하도록 설정](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) 계속 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="c1a95-168">Follow hello steps in [Enable TCP/IP Network Protocol for SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) before continuing.</span></span>

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a><span data-ttu-id="c1a95-169">SQL Server 데이터베이스 온-프레미스</span><span class="sxs-lookup"><span data-stu-id="c1a95-169">Create a SQL Server database on-premises</span></span>
<span data-ttu-id="c1a95-170">Visual Studio 웹 응용 프로그램을 사용하려면 Azure에서 액세스할 수 있는 멤버 자격 데이터베이스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-170">Your Visual Studio web application requires a membership database that can be accessed by Azure.</span></span> <span data-ttu-id="c1a95-171">이렇게 하려면 SQL Server 또는 SQL Server Express 데이터베이스 (하지 hello LocalDB 데이터베이스 기본적으로 MVC 템플릿을 사용 하 여 hello)를 해야 하므로 다음 hello 멤버 자격 데이터베이스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-171">This requires a SQL Server or SQL Server Express database (not hello LocalDB database that hello MVC template uses by default), so you'll create hello membership database next.</span></span>

1. <span data-ttu-id="c1a95-172">SQL Server Management Studio에서 toohello 방금 설치 된 SQL Server를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-172">In SQL Server Management Studio, connect toohello SQL Server you just installed.</span></span> <span data-ttu-id="c1a95-173">(경우 hello **tooServer 연결** 너무 이동 대화 상자를 자동으로 나타나지 않으면**개체 탐색기** hello 왼쪽된 창에서 클릭 **연결**, 클릭하고**데이터베이스 엔진**.) ![TooServer 연결][SSMSConnectToServer]</span><span class="sxs-lookup"><span data-stu-id="c1a95-173">(If hello **Connect tooServer** dialog does not appear automatically, navigate too**Object Explorer** in hello left pane, click **Connect**, and then click **Database Engine**.) ![Connect tooServer][SSMSConnectToServer]</span></span>
   
    <span data-ttu-id="c1a95-174">**서버 유형**으로 **데이터베이스 엔진**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-174">For **Server type**, choose **Database Engine**.</span></span> <span data-ttu-id="c1a95-175">에 대 한 **서버 이름**를 사용할 수 있습니다 **localhost** hello의 또는 이름을 사용 하는 hello 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="c1a95-175">For **Server name**, you can use **localhost** or hello name of hello computer that you are using.</span></span> <span data-ttu-id="c1a95-176">선택 **SQL Server 인증**, 다음 hello sa 사용자 이름 및 이전에 만든 hello 암호를 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-176">Choose **SQL Server authentication**, and then log in with hello sa user name and hello password that you created earlier.</span></span>
2. <span data-ttu-id="c1a95-177">toocreate SQL Server Management Studio를 사용 하 여 새 데이터베이스를 마우스 오른쪽 단추로 클릭 **데이터베이스** 에 개체 탐색기, 마우스 클릭 **새 데이터베이스**합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-177">toocreate a new database by using SQL Server Management Studio, right-click **Databases** in Object Explorer, and then click **New Database**.</span></span>
   
    ![새 데이터베이스 만들기][SSMScreateNewDB]
3. <span data-ttu-id="c1a95-179">Hello에 **새 데이터베이스** 대화 상자에서 MembershipDB hello 데이터베이스 이름에 대 한 입력 한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-179">In hello **New Database** dialog, enter MembershipDB for hello database name, and then click **OK**.</span></span>
   
    ![데이터베이스 이름 입력][SSMSprovideDBname]
   
    <span data-ttu-id="c1a95-181">만들지 않으면 모든 변경 내용을 toohello 데이터베이스가 시점에서 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-181">Note that you do not make any changes toohello database at this point.</span></span> <span data-ttu-id="c1a95-182">hello 멤버 자격 정보 실행 하면 웹 응용 프로그램에 나중에 자동으로 추가할 수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-182">hello membership information will be added automatically later by your web application when you run it.</span></span>
4. <span data-ttu-id="c1a95-183">확장 하는 경우 개체 탐색기에서 **데이터베이스**, 해당 hello 멤버 자격 데이터베이스를 만든 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-183">In Object Explorer, if you expand **Databases**, you will see that hello membership database has been created.</span></span>
   
    ![MembershipDB 생성됨][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="c1a95-185">B.</span><span class="sxs-lookup"><span data-stu-id="c1a95-185">B.</span></span> <span data-ttu-id="c1a95-186">Hello Azure 포털에서에서 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="c1a95-186">Create a web app in hello Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="c1a95-187">이미 hello이이 자습서에 대 한 toouse 되도록 하는 Azure 포털에서 웹 응용 프로그램을 만들었으면 있습니다 건너뛰어 너무[하이브리드 연결을 만들고 BizTalk 서비스](#CreateHC) 하 고 여기에서 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-187">If you have already created a web app in hello Azure Portal that you want toouse for this tutorial, you can skip ahead too[Create a Hybrid Connection and a BizTalk Service](#CreateHC) and continue from there.</span></span>
> 
> 

1. <span data-ttu-id="c1a95-188">Hello에 [Azure 포털](https://portal.azure.com), 클릭 **새로** > **웹 + 모바일** > **웹 앱**합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-188">In hello [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web app**.</span></span>
   
    ![새 단추][New]
2. <span data-ttu-id="c1a95-190">웹 앱을 구성하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-190">Configure your web app, and then click **Create**.</span></span>
   
    ![웹 사이트 이름][WebsiteCreationBlade]
3. <span data-ttu-id="c1a95-192">몇 분 후 hello 웹 응용 프로그램이 만들어지고 해당 웹 앱 블레이드 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-192">After a few moments, hello web app is created and its web app blade appears.</span></span> <span data-ttu-id="c1a95-193">hello 블레이드는 웹 앱을 관리할 수 있는 수직으로 스크롤 가능한 한 대시보드입니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-193">hello blade is a vertically scrollable dashboard that lets you manage your web app.</span></span>
   
    ![실행 중인 웹 사이트][WebSiteRunningBlade]
   
    <span data-ttu-id="c1a95-195">tooverify hello 웹 앱이 라이브, hello를 클릭할 수 있는 **찾아보기** 아이콘 toodisplay hello 기본 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-195">tooverify hello web app is live, you can click hello **Browse** icon toodisplay hello default page.</span></span>

<span data-ttu-id="c1a95-196">다음으로 hello 웹 앱에 대 한 BizTalk 서비스 및 하이브리드 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-196">Next, you will create a hybrid connection and a BizTalk service for hello web app.</span></span>

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="c1a95-197">C.</span><span class="sxs-lookup"><span data-stu-id="c1a95-197">C.</span></span> <span data-ttu-id="c1a95-198">하이브리드 연결 및 BizTalk 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="c1a95-198">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="c1a95-199">다시 포털 hello에 toosettings 이동 하 고 클릭 **네트워킹** > **하이브리드 연결 끝점 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-199">Back in hello Portal, go toosettings and click **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![하이브리드 연결][CreateHCHCIcon]
2. <span data-ttu-id="c1a95-201">Hello 하이브리드 연결 블레이드에서 클릭 **추가** > **새 하이브리드 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-201">On hello Hybrid connections blade, click **Add** > **New hybrid connection**.</span></span>
3. <span data-ttu-id="c1a95-202">Hello에 **하이브리드 연결** 블레이드:</span><span class="sxs-lookup"><span data-stu-id="c1a95-202">On hello **Create hybrid connection** blade:</span></span>
   
   * <span data-ttu-id="c1a95-203">에 대 한 **이름**, hello 연결에 대 한 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-203">For **Name**, provide a name for hello connection.</span></span>
   * <span data-ttu-id="c1a95-204">에 대 한 **Hostname**, SQL Server 호스트 컴퓨터의 hello 컴퓨터 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-204">For **Hostname**, enter hello computer name of your SQL Server host computer.</span></span>
   * <span data-ttu-id="c1a95-205">에 대 한 **포트**, 1433 (SQL Server에 대 한 hello 기본 포트)을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-205">For **Port**, enter 1433 (hello default port for SQL Server).</span></span>
   * <span data-ttu-id="c1a95-206">클릭 **BizTalk 서비스** > **새 BizTalk 서비스** hello BizTalk 서비스에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-206">Click **BizTalk Service** > **New BizTalk Service** and enter a name for hello BizTalk service.</span></span>
     
     ![하이브리드 연결 만들기][TwinCreateHCBlades]
4. <span data-ttu-id="c1a95-208">**확인** 을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-208">Click **OK** twice.</span></span>
   
    <span data-ttu-id="c1a95-209">Hello 프로세스가 완료 되 면 hello **알림** 영역 녹색 깜박입니다 **성공** 및 hello **하이브리드 연결** 블레이드는 hello 새 하이브리드 연결을 표시 합니다. 상태를 hello **연결 되어 있지 않은**합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-209">When hello process completes, hello **Notifications** area will flash a green **SUCCESS** and hello **Hybrid connection** blade will show hello new hybrid connection with hello status as **Not connected**.</span></span>
   
    ![1개의 하이브리드 연결 생성됨][CreateHCOneConnectionCreated]

<span data-ttu-id="c1a95-211">이 시점에서 hello 클라우드 하이브리드 연결 인프라의 중요 한 부분을 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-211">At this point, you have completed an important part of hello cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="c1a95-212">이제 해당하는 온-프레미스 부분을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-212">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="d-install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a><span data-ttu-id="c1a95-213">D.</span><span class="sxs-lookup"><span data-stu-id="c1a95-213">D.</span></span> <span data-ttu-id="c1a95-214">Hello 온-프레미스 하이브리드 연결 관리자 toocomplete hello 연결 설치</span><span class="sxs-lookup"><span data-stu-id="c1a95-214">Install hello on-premises Hybrid Connection Manager toocomplete hello connection</span></span>
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

<span data-ttu-id="c1a95-215">Hello 하이브리드 연결 인프라에 완료 되 면 이제 웹 응용 프로그램을 사용 하 여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-215">Now that hello hybrid connection infrastructure is complete, you will create a web application that uses it.</span></span>

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-hello-database-connection-string-and-run-hello-project-locally"></a><span data-ttu-id="c1a95-216">E.</span><span class="sxs-lookup"><span data-stu-id="c1a95-216">E.</span></span> <span data-ttu-id="c1a95-217">기본 ASP.NET 웹 프로젝트를 만듭니다 hello 데이터베이스 연결 문자열을 편집 하 고 hello 프로젝트를 로컬로 실행</span><span class="sxs-lookup"><span data-stu-id="c1a95-217">Create a basic ASP.NET web project, edit hello database connection string, and run hello project locally</span></span>
### <a name="create-a-basic-aspnet-project"></a><span data-ttu-id="c1a95-218">기본 ASP.NET 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="c1a95-218">Create a basic ASP.NET project</span></span>
1. <span data-ttu-id="c1a95-219">Hello에 Visual Studio에서 **파일** 메뉴에서 새 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-219">In Visual Studio, on hello **File** menu, create a new Project:</span></span>
   
    ![새 Visual Studio 프로젝트][HCVSNewProject]
2. <span data-ttu-id="c1a95-221">Hello에 **템플릿** hello 섹션 **새 프로젝트** 대화 상자에서 **웹** 선택 **ASP.NET 웹 응용 프로그램**, 를클릭한다음 **정상**합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-221">In hello **Templates** section of hello **New Project** dialog, select **Web** and choose **ASP.NET Web Application**, and then click **OK**.</span></span>
   
    ![ASP.NET 웹 응용 프로그램 선택][HCVSChooseASPNET]
3. <span data-ttu-id="c1a95-223">Hello에 **새 ASP.NET 프로젝트** 대화 상자에서 선택 **MVC**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-223">In hello **New ASP.NET Project** dialog, choose **MVC**, and then click **OK**.</span></span>
   
    ![MVC 선택][HCVSChooseMVC]
4. <span data-ttu-id="c1a95-225">Hello 프로젝트를 만든 hello 응용 프로그램 추가 정보 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-225">When hello project has been created, hello application readme page appears.</span></span> <span data-ttu-id="c1a95-226">Hello 웹 프로젝트를 아직 실행 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="c1a95-226">Do not run hello web project yet.</span></span>
   
    ![추가 정보 페이지][HCVSReadmePage]

### <a name="edit-hello-database-connection-string-for-hello-application"></a><span data-ttu-id="c1a95-228">Hello 응용 프로그램에 대 한 hello 데이터베이스 연결 문자열 편집</span><span class="sxs-lookup"><span data-stu-id="c1a95-228">Edit hello database connection string for hello application</span></span>
<span data-ttu-id="c1a95-229">이 단계에서는 응용 프로그램에 알리는 hello 연결 문자열을 편집할 위치 toofind 로컬 SQL Server Express 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-229">In this step, you edit hello connection string that tells your application where toofind your local SQL Server Express database.</span></span> <span data-ttu-id="c1a95-230">hello 연결 문자열은 hello 응용 프로그램에 대 한 구성 정보를 포함 하는 hello 응용 프로그램의 Web.config 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-230">hello connection string is in hello application's Web.config file, which contains configuration information for hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="c1a95-231">응용 프로그램에서 SQL Server Express 및 하지 hello 하나 Visual Studio의 기본 LocalDB에서에서 만든 hello 데이터베이스를 사용 하는 tooensure는 프로젝트를 실행 하기 전에이 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-231">tooensure that your application uses hello database that you created in SQL Server Express, and not hello one in Visual Studio's default LocalDB, it is important that you complete this step before running your project.</span></span>
> 
> 

1. <span data-ttu-id="c1a95-232">솔루션 탐색기에서 hello Web.config 파일을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-232">In Solution Explorer, double-click hello Web.config file.</span></span>
   
    ![Web.config][HCVSChooseWebConfig]
2. <span data-ttu-id="c1a95-234">Hello 편집 **connectionStrings** 섹션 toopoint toohello SQL Server 데이터베이스에 다음 예제는 hello의 hello 구문 다음 로컬 컴퓨터에:</span><span class="sxs-lookup"><span data-stu-id="c1a95-234">Edit hello **connectionStrings** section toopoint toohello SQL Server database on your local machine, following hello syntax in hello following example:</span></span>
   
    ![연결 문자열][HCVSConnectionString]
   
    <span data-ttu-id="c1a95-236">Hello 연결 문자열을 작성할 때 염두 hello 다음에 유의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c1a95-236">When composing hello connection string, keep in mind hello following:</span></span>
   
   * <span data-ttu-id="c1a95-237">명명 된 인스턴스 (예를 들어 YourServer\SQLEXPRESS) 기본 인스턴스 대신 tooa을 연결 하는 경우에 SQL Server toouse 정적 포트를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-237">If you are connecting tooa named instance instead of a default instance (for example, YourServer\SQLEXPRESS), you must configure your SQL Server toouse static ports.</span></span> <span data-ttu-id="c1a95-238">정적 포트를 구성 하는 방법에 대 한 정보를 참조 하십시오. [어떻게 특정 포트에서 SQL Server toolisten tooconfigure](http://support.microsoft.com/kb/823938)합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-238">For information on configuring static ports, see [How tooconfigure SQL Server toolisten on a specific port](http://support.microsoft.com/kb/823938).</span></span> <span data-ttu-id="c1a95-239">기본적으로, 명명된 인스턴는 하이브리드 연결에서 지원되지 않는 UDP 및 동적 포트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-239">By default, named instances use UDP and dynamic ports, which are not supported by Hybrid Connections.</span></span>
   * <span data-ttu-id="c1a95-240">Hello를 지정 하는 것이 좋습니다. 로컬 SQL Server TCP 설정 개이고 hello 올바른 포트를 사용 하는 확인할 수 있도록 hello 연결 문자열에 포트 (1433 hello 예제에서와 같이 기본적으로).</span><span class="sxs-lookup"><span data-stu-id="c1a95-240">It is recommended that you specify hello port (1433 by default, as shown in hello example) on hello connection string so that you can be sure that your local SQL Server has TCP enabled and is using hello correct port.</span></span>
   * <span data-ttu-id="c1a95-241">Toouse SQL Server 인증 tooconnect, 연결 문자열에 hello 사용자 ID와 암호를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-241">Remember toouse SQL Server Authentication tooconnect, specifying hello user ID and password in your connection string.</span></span>
3. <span data-ttu-id="c1a95-242">클릭 **저장** Visual Studio toosave hello Web.config 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-242">Click **Save** in Visual Studio toosave hello Web.config file.</span></span>

### <a name="run-hello-project-locally-and-register-a-new-user"></a><span data-ttu-id="c1a95-243">Hello 프로젝트를 로컬로 실행 하 고 새 사용자 등록</span><span class="sxs-lookup"><span data-stu-id="c1a95-243">Run hello project locally and register a new user</span></span>
1. <span data-ttu-id="c1a95-244">디버그 아래의 hello 찾아보기 단추를 클릭 하 여 새 웹 프로젝트를 로컬로 실행 이제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-244">Now, run your new web project locally by clicking hello browse button under Debug.</span></span> <span data-ttu-id="c1a95-245">이 예에서는 Internet Explorer를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-245">This example uses Internet Explorer.</span></span>
   
    ![프로젝트 실행][HCVSRunProject]
2. <span data-ttu-id="c1a95-247">Hello hello 기본 웹 페이지의 오른쪽 위에, 선택 **등록** tooregister 새 계정:</span><span class="sxs-lookup"><span data-stu-id="c1a95-247">On hello upper right of hello default web page, choose **Register** tooregister a new account:</span></span>
   
    ![새 계정 등록][HCVSRegisterLocally]
3. <span data-ttu-id="c1a95-249">사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-249">Enter a user name and password:</span></span>
   
    ![사용자 이름 및 암호를 입력합니다.][HCVSCreateNewAccount]
   
    <span data-ttu-id="c1a95-251">이 응용 프로그램에 대 한 hello 멤버 자격 정보를 보유 하는 로컬 SQL Server에 데이터베이스를 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-251">This automatically creates a database on your local SQL Server that holds hello membership information for your application.</span></span> <span data-ttu-id="c1a95-252">Hello 테이블 중 하나 (**dbo입니다. AspNetUsers**) 보류 웹 hello 방금 입력 한 것 처럼 응용 프로그램 사용자 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-252">One of hello tables (**dbo.AspNetUsers**) holds web app user credentials like hello ones that you just entered.</span></span> <span data-ttu-id="c1a95-253">Hello 자습서의 뒷부분에서이 테이블에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-253">You will see this table later in hello tutorial.</span></span>
4. <span data-ttu-id="c1a95-254">Hello 기본 웹 페이지의 hello 브라우저 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-254">Close hello browser window of hello default web page.</span></span> <span data-ttu-id="c1a95-255">Visual Studio에서 hello 응용 프로그램을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-255">This stops hello application in Visual Studio.</span></span>

<span data-ttu-id="c1a95-256">Hello 다음 단계를 toopublish hello 응용 프로그램 tooAzure는 이제 하 고 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-256">You are now ready for hello next step, which is toopublish hello application tooAzure and test it.</span></span>

<a name="PubNTest"></a>

## <a name="f-publish-hello-web-application-tooazure-and-test-it"></a><span data-ttu-id="c1a95-257">F.</span><span class="sxs-lookup"><span data-stu-id="c1a95-257">F.</span></span> <span data-ttu-id="c1a95-258">웹 응용 프로그램 tooAzure hello를 게시 하 고 테스트</span><span class="sxs-lookup"><span data-stu-id="c1a95-258">Publish hello web application tooAzure and test it</span></span>
<span data-ttu-id="c1a95-259">프로그램 응용 프로그램 tooyour 앱 서비스 웹 앱을 게시 toosee hello 하이브리드 연결을 이전에 구성한는 방법을 테스트 하는 이제 tooconnect 사용 되는 로컬 컴퓨터에 웹 앱 toohello 데이터베이스 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-259">Now, you'll publish your application tooyour App Service web app and then test it toosee how hello hybrid connection you configured earlier is being used tooconnect your web app toohello database on your local machine.</span></span>

### <a name="publish-hello-web-application"></a><span data-ttu-id="c1a95-260">Hello 웹 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="c1a95-260">Publish hello web application</span></span>
1. <span data-ttu-id="c1a95-261">Hello hello Azure 포털의에서 앱 서비스 웹 앱에 대 한 게시 프로필을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-261">You can download your publishing profile for hello App Service web app in hello Azure Portal.</span></span> <span data-ttu-id="c1a95-262">웹 앱에 대 한 hello 블레이드에서 클릭 **Get 게시 프로필**, hello 파일 tooyour 컴퓨터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-262">On hello blade for your web app, click **Get publish profile**, and then save hello file tooyour computer.</span></span>
   
    ![게시 프로필 다운로드][PortalDownloadPublishProfile]
   
    <span data-ttu-id="c1a95-264">이제 이 파일을 Visual Studio 웹 응용 프로그램으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-264">Next, you will import this file into your Visual Studio web application.</span></span>
2. <span data-ttu-id="c1a95-265">Visual Studio에서 솔루션 탐색기에서 hello 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-265">In Visual Studio, right-click hello project name in Solution Explorer and select **Publish**.</span></span>
   
    ![게시 선택][HCVSRightClickProjectSelectPublish]
3. <span data-ttu-id="c1a95-267">Hello에 **웹 게시** 대화 상자의 hello에서 **프로필** 탭에서 선택 **가져오기**합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-267">In hello **Publish Web** dialog, on hello **Profile** tab, choose **Import**.</span></span>
   
    ![가져오기][HCVSPublishWebDialogImport]
4. <span data-ttu-id="c1a95-269">찾아보기 tooyour 게시 프로필 다운로드를 선택한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-269">Browse tooyour downloaded publishing profile, select it, and then click **OK**.</span></span>
   
    ![Tooprofile 찾아보기][HCVSBrowseToImportPubProfile]
5. <span data-ttu-id="c1a95-271">게시 정보를 가져와서 hello에 표시 **연결** hello 대화 상자의 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-271">Your publishing information is imported and displays on hello **Connection** tab of hello dialog.</span></span>
   
    ![게시 클릭][HCVSClickPublish]
   
    <span data-ttu-id="c1a95-273">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-273">Click **Publish**.</span></span>
   
    <span data-ttu-id="c1a95-274">게시 완료 되 면 브라우저를 시작 하 고 않는다는 점을 제외 하면 이제 hello Azure 클라우드 동시에 이제 친숙 한 ASP.NET 응용 프로그램-표시 됩니다!</span><span class="sxs-lookup"><span data-stu-id="c1a95-274">When publishing completes, your browser will launch and show your now familiar ASP.NET application -- except that now it is live in hello Azure cloud!</span></span>

<span data-ttu-id="c1a95-275">다음으로 라이브 웹 응용 프로그램 toosee 하이브리드 연결에서에서 사용할 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-275">Next, you will use your live web application toosee its Hybrid Connection in action.</span></span>

### <a name="test-hello-completed-web-application-on-azure"></a><span data-ttu-id="c1a95-276">테스트 hello Azure에서 웹 응용 프로그램을 완료</span><span class="sxs-lookup"><span data-stu-id="c1a95-276">Test hello completed web application on Azure</span></span>
1. <span data-ttu-id="c1a95-277">Hello 위에 Azure에서 웹 페이지의 오른쪽 선택 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-277">On hello top right of your web page on Azure, choose **Log in**.</span></span>
   
    ![로그인 테스트][HCTestLogIn]
2. <span data-ttu-id="c1a95-279">이제 웹 앱을 앱 서비스 tooyour 웹 응용 프로그램의 멤버 자격 데이터베이스를 로컬 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-279">Your App Service web app is now connected tooyour web application's membership database on your local machine.</span></span> <span data-ttu-id="c1a95-280">tooverify hello hello 로컬에 입력 한 동일한 자격 증명 이전 데이터베이스를 사용 하 여이 로그 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-280">tooverify this, log in with hello same credentials that you entered in hello local database earlier.</span></span>
   
    ![Hello 인사][HCTestHelloContoso]
3. <span data-ttu-id="c1a95-282">toofurther 새 하이브리드 연결을 테스트 하 고, 로그 오프 Azure 웹 응용 프로그램, 다른 사용자로 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-282">toofurther test your new hybrid connection, log off of your Azure web application and register as another user.</span></span> <span data-ttu-id="c1a95-283">새 사용자 이름 및 암호를 입력한 다음 **등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-283">Provide a new user name and password, and then click **Register**.</span></span>
   
    ![다른 사용자 테스트 등록][HCTestRegisterRelecloud]
4. <span data-ttu-id="c1a95-285">tooverify hello 새 사용자의 자격 증명 하이브리드 연결을 통해 로컬 데이터베이스에 저장 되어 있는 로컬 컴퓨터에 SQL Management Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-285">tooverify that hello new user's credentials have been stored in your local database through your hybrid connection, open SQL Management Studio on your local computer.</span></span> <span data-ttu-id="c1a95-286">개체 탐색기에서 확장 hello **MembershipDB** 데이터베이스를 선택한 다음 확장 **테이블**합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-286">In Object Explorer, expand hello **MembershipDB** database, and then expand **Tables**.</span></span> <span data-ttu-id="c1a95-287">마우스 오른쪽 단추로 클릭 hello **dbo입니다. AspNetUsers** 멤버 자격 테이블을 선택 **상위 1000 개 행 선택** tooview hello 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-287">Right-click hello **dbo.AspNetUsers** membership table and choose **Select Top 1000 Rows** tooview hello results.</span></span>
   
    ![Hello 결과 보기][HCTestSSMSTree]
5. <span data-ttu-id="c1a95-289">로컬 멤버 자격 테이블에는 이제 두 계정-로컬에서 만든 hello 및 hello hello Azure 클라우드에서에서 만든 하나 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-289">Your local membership table now shows both accounts - hello one that you created locally, and hello one that you created in hello Azure cloud.</span></span> <span data-ttu-id="c1a95-290">Azure의 하이브리드 연결 기능을 통해 온-프레미스 데이터베이스 tooyour hello 클라우드에서 만든 hello 저장 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-290">hello one that you created in hello cloud has been saved tooyour on-premises database through Azure's Hybrid Connection feature.</span></span>
   
    ![온-프레미스 데이터베이스에 등록된 사용자][HCTestShowMemberDb]

<span data-ttu-id="c1a95-292">이제 만들고 hello Azure 클라우드의에서 웹 앱 및 온-프레미스 SQL Server 데이터베이스 간의 하이브리드 연결을 사용 하 여 ASP.NET 웹 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-292">You have now created and deployed an ASP.NET web application that uses a hybrid connection between a web app in hello Azure cloud and an on-premises SQL Server database.</span></span> <span data-ttu-id="c1a95-293">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="c1a95-293">Congratulations!</span></span>

## <a name="see-also"></a><span data-ttu-id="c1a95-294">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c1a95-294">See Also</span></span>
[<span data-ttu-id="c1a95-295">하이브리드 연결 개요</span><span class="sxs-lookup"><span data-stu-id="c1a95-295">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="c1a95-296">Josh Twist가 소개하는 하이브리드 연결(채널 9 비디오)(영문)</span><span class="sxs-lookup"><span data-stu-id="c1a95-296">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="c1a95-297">하이브리드 연결 개요</span><span class="sxs-lookup"><span data-stu-id="c1a95-297">Hybrid Connections overview</span></span>](/services/biztalk-services/)

[<span data-ttu-id="c1a95-298">BizTalk 서비스: 대시보드, 모니터, 확장, 구성 및 하이브리드 연결 탭</span><span class="sxs-lookup"><span data-stu-id="c1a95-298">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="c1a95-299">원활한 응용 프로그램 이식성으로 실시간 하이브리드 연결 클라우드 구축(채널 9 비디오)(영문)</span><span class="sxs-lookup"><span data-stu-id="c1a95-299">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="c1a95-300">Azure App Service에서 하이브리드 연결을 사용하여 온-프레미스 리소스에 액세스</span><span class="sxs-lookup"><span data-stu-id="c1a95-300">Access on-premises resources using hybrid connections in Azure App Service</span></span>](web-sites-hybrid-connection-get-started.md)

[<span data-ttu-id="c1a95-301">ASP.NET ID 개요(영문)</span><span class="sxs-lookup"><span data-stu-id="c1a95-301">ASP.NET Identity Overview</span></span>](http://www.asp.net/identity)

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
