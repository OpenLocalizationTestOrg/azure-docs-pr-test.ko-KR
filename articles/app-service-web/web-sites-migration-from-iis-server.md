---
title: "Azure 앱 서비스에서 엔터프라이즈 웹 앱 마이그레이션"
description: "Web App Migration Assistant를 사용하여 기존 IIS 웹 사이트를 Azure 앱 서비스 웹 앱으로 신속하게 마이그레이션하는 방법을 보여 줍니다."
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: 
ms.assetid: 2e846fc0-37cc-42e6-ac57-ff442ef16e85
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: 18d6a8da38b42dcf5c1500f7fc26638aea26a809
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-an-enterprise-web-app-to-azure-app-service"></a><span data-ttu-id="e2fa0-103">Azure 앱 서비스에서 엔터프라이즈 웹 앱 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="e2fa0-103">Migrate an enterprise web app to Azure App Service</span></span>
<span data-ttu-id="e2fa0-104">IIS(인터넷 정보 서비스) 6 이상을 실행하는 기존 웹 사이트를 [앱 서비스 웹 앱](http://go.microsoft.com/fwlink/?LinkId=529714)으로 쉽게 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-104">You can easily migrate your existing websites that run on Internet Information Service (IIS) 6 or later to [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="e2fa0-105">Windows Server 2003은 2015년 7월 14일에 지원이 종료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-105">Windows Server 2003 reached end of support on July 14th 2015.</span></span> <span data-ttu-id="e2fa0-106">현재 웹 사이트가 Windows Server 2003을 사용하는 IIS 서버에 있는 경우 웹 앱이 위험, 비용 및 충돌을 줄이면서 웹 사이트를 온라인으로 유지할 수 있는 방법이며, Web App Migration Assistant를 사용하면 마이그레이션 프로세스를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-106">If you are currently hosting your websites on an IIS server that is Windows Server 2003, Web Apps is a low-risk, low-cost, and low-friction way to keep your websites online, and Web Apps Migration Assistant can help automate the migration process for you.</span></span> 
> 
> 

<span data-ttu-id="e2fa0-107">[Web App Migration Assistant](https://www.movemetothecloud.net/) 는 IIS 서버 설치를 분석하고, 앱 서비스로 마이그레이션할 수 있는 사이트를 식별하고, 마이그레이션할 수 없거나 플랫폼에서 지원되지 않는 요소를 강조 표시한 후, 웹 사이트 및 관련 데이터베이스를 Azure로 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-107">[Web Apps Migration Assistant](https://www.movemetothecloud.net/) can analyze your IIS server installation, identify which sites can be migrated to App Service, highlight any elements that cannot be migrated or are unsupported on the platform, and then migrate your websites and associated databases to Azure.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="elements-verified-during-compatibility-analysis"></a><span data-ttu-id="e2fa0-108">호환성 분석 중 확인하는 요소</span><span class="sxs-lookup"><span data-stu-id="e2fa0-108">Elements Verified During Compatibility Analysis</span></span>
<span data-ttu-id="e2fa0-109">Migration Assistant에서는 온-프레미스 IIS에서 Azure 앱 서비스 웹 앱으로의 성공적인 마이그레이션을 방해할 수 있는 우려나 차단 문제의 잠재적인 원인을 식별하는 준비 보고서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-109">The Migration Assistant creates a readiness report to identify any potential causes for concern or blocking issues which may prevent a successful migration from on-premises IIS to Azure App Service Web Apps.</span></span> <span data-ttu-id="e2fa0-110">알고 있어야 하는 몇 가지 주요 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-110">Some of the key items to be aware of are:</span></span>

* <span data-ttu-id="e2fa0-111">포트 바인딩 - 웹 앱은 HTTP 트래픽에는 포트 80, HTTPS 트래픽에는 포트 443만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-111">Port Bindings – Web Apps only supports Port 80 for HTTP and Port 443 for HTTPS traffic.</span></span> <span data-ttu-id="e2fa0-112">다른 포트 구성은 무시되며 트래픽이 80 또는 443으로 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-112">Different port configurations will be ignored and traffic will be routed to 80 or 443.</span></span> 
* <span data-ttu-id="e2fa0-113">인증 - 웹 앱은 익명 인증을 기본 지원하고 응용 프로그램에서 지정한 경우 폼 인증도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-113">Authentication – Web Apps supports Anonymous Authentication by default and Forms Authentication where specified by an application.</span></span> <span data-ttu-id="e2fa0-114">Windows 인증은 Azure Active Directory 및 ADFS와 통합해야만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-114">Windows Authentication can be used by integrating with Azure Active Directory and ADFS only.</span></span> <span data-ttu-id="e2fa0-115">예를 들어, 기본 인증과 같은 다른 인증 형식은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-115">All other forms of authentication - for example, Basic Authentication - are not currently supported.</span></span> 
* <span data-ttu-id="e2fa0-116">GAC(전역 어셈블리 캐시) – GAC는 웹 앱에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-116">Global Assembly Cache (GAC) – The GAC is not supported in Web Apps.</span></span> <span data-ttu-id="e2fa0-117">응용 프로그램에서 일반적으로 GAC에 배포하는 어셈블리를 참조하는 경우 웹 앱의 응용 프로그램 bin 폴더에 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-117">If your application references assemblies which you usually deploy to the GAC, you will need to deploy to the application bin folder in Web Apps.</span></span> 
* <span data-ttu-id="e2fa0-118">IIS5 호환 모드 - 웹 앱에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-118">IIS5 Compatibility Mode – This is not supported in Web Apps.</span></span> 
* <span data-ttu-id="e2fa0-119">응용 프로그램 풀 – 웹 앱에서 각 사이트와 해당 자식 응용 프로그램은 동일한 응용 프로그램 풀에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-119">Application Pools – In Web Apps, each site and its child applications run in the same application pool.</span></span> <span data-ttu-id="e2fa0-120">사이트의 여러 자식 응용 프로그램이 여러 응용 프로그램 풀을 사용하는 경우에는 공통 설정을 사용해 응용 프로그램을 단일 응용 프로그램 풀로 통합하거나 각 응용 프로그램을 별도의 웹 앱으로 마이그레이션하세요.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-120">If your site has multiple child applications utilizing multiple application pools, consolidate them to a single application pool with common settings or migrate each application to a separate web app.</span></span>
* <span data-ttu-id="e2fa0-121">COM 구성 요소 – 웹 앱에서는 플랫폼에 COM 구성 요소를 등록할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-121">COM Components – Web Apps does not allow the registration of COM Components on the platform.</span></span> <span data-ttu-id="e2fa0-122">웹 사이트 또는 응용 프로그램에서 COM 구성 요소를 사용하는 경우에는 구성 요소를 관리 코드로 다시 작성하고 웹 사이트 또는 응용 프로그램을 함께 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-122">If your websites or applications make use of any COM Components, you must rewrite them in managed code and deploy them with the website or application.</span></span>
* <span data-ttu-id="e2fa0-123">ISAPI 확장 – 웹앱에서는 ISAPI 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-123">ISAPI Extensions – Web Apps can support the use of ISAPI Extensions.</span></span> <span data-ttu-id="e2fa0-124">다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-124">You need to do the following:</span></span>
  
  * <span data-ttu-id="e2fa0-125">웹 앱에 DLL 배포</span><span class="sxs-lookup"><span data-stu-id="e2fa0-125">deploy the DLLs with your web app</span></span> 
  * <span data-ttu-id="e2fa0-126">[Web.config](http://www.iis.net/configreference/system.webserver/isapifilters)</span><span class="sxs-lookup"><span data-stu-id="e2fa0-126">register the DLLs using [Web.config](http://www.iis.net/configreference/system.webserver/isapifilters)</span></span>
  * <span data-ttu-id="e2fa0-127">[이 문서의 섹션](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples), "임의 ISAPI 확장 로드 허용"에 설명된 내용에 따라 사이트 루트에 applicationHost.xdt 파일 배치</span><span class="sxs-lookup"><span data-stu-id="e2fa0-127">place an applicationHost.xdt file in the site root with the content outlined in "Allowing arbitrart ISAPI extensions to be loaded" [section of this article](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples)</span></span> 
    
  
    
    <span data-ttu-id="e2fa0-128">웹 사이트에서 XML 문서 변환을 사용하는 방법에 대한 예제는 [Microsoft Azure 웹 사이트 변환](http://blogs.msdn.com/b/waws/archive/2014/06/17/transform-your-microsoft-azure-web-site.aspx)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-128">For more examples of how to use XML Document Transformations with your website, see [Transform your Microsoft Azure Web Site](http://blogs.msdn.com/b/waws/archive/2014/06/17/transform-your-microsoft-azure-web-site.aspx).</span></span>
* <span data-ttu-id="e2fa0-129">SharePoint, FPSE(Front Page Server Extensions), FTP, SSL 인증서와 같은 다른 구성 요소는 마이그레이션되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-129">Other components like SharePoint, front page server extensions (FPSE), FTP, SSL certificates will not be migrated.</span></span>

## <a name="how-to-use-the-web-apps-migration-assistant"></a><span data-ttu-id="e2fa0-130">Web App Migration Assistant 사용 방법</span><span class="sxs-lookup"><span data-stu-id="e2fa0-130">How to use the Web Apps Migration Assistant</span></span>
<span data-ttu-id="e2fa0-131">이 섹션에서는 SQL Server 데이터베이스를 사용하고 온-프레미스 Windows Server 2003 R2(IIS 6.0) 컴퓨터에서 실행 중인 몇 개 웹 사이트를 마이그레이션하는 예제를 단계별로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-131">This section steps through an example to to migrate a few websites that use a SQL Server database and running on an on-premises Windows Server 2003 R2 (IIS 6.0) machine:</span></span>

1. <span data-ttu-id="e2fa0-132">IIS 서버 또는 클라이언트 컴퓨터에서 [https://www.movemetothecloud.net/](https://www.movemetothecloud.net/)</span><span class="sxs-lookup"><span data-stu-id="e2fa0-132">On the IIS server or your client machine navigate to [https://www.movemetothecloud.net/](https://www.movemetothecloud.net/)</span></span> 
   
   ![](./media/web-sites-migration-from-iis-server/migration-tool-homepage.png)
2. <span data-ttu-id="e2fa0-133">**Dedicated IIS Server** 단추를 클릭하여 Web App Migration Assistant를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-133">Install Web Apps Migration Assistant by clicking on the **Dedicated IIS Server** button.</span></span> <span data-ttu-id="e2fa0-134">향후 추가 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-134">More options will be options in the near future.</span></span> 
3. <span data-ttu-id="e2fa0-135">**Install Tool** 단추를 클릭하여 컴퓨터에 Web App Migration Assistant 를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-135">Click the **Install Tool** button to install Web Apps Migration Assistant on your machine.</span></span>
   
   ![](./media/web-sites-migration-from-iis-server/install-page.png)
   
   > [!NOTE]
   > <span data-ttu-id="e2fa0-136">**오프라인 설치를 위해 다운로드** 를 클릭하여 인터넷에 연결되지 않은 서버에 설치하기 위한 ZIP 파일을 다운로드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-136">You can also click **Download for offline install** to download a ZIP file for installing on servers not connected to the internet.</span></span> <span data-ttu-id="e2fa0-137">또는 **Upload an existing migration readiness report**를 클릭할 수 있으며, 이 고급 옵션을 선택하면 이전에 생성한 기존 마이그레이션 준비 보고서로 작업할 수 있습니다(나중에 설명).</span><span class="sxs-lookup"><span data-stu-id="e2fa0-137">Or, you can click **Upload an existing migration readiness report**, which is an advanced option to work with an existing migration readiness report that you previously generated (explained later).</span></span>
   > 
   > 
4. <span data-ttu-id="e2fa0-138">**응용 프로그램 설치** 화면에서 **설치**를 클릭하여 컴퓨터에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-138">In the **Application Install** screen, click **Install** to install on your machine.</span></span> <span data-ttu-id="e2fa0-139">필요한 경우 웹 배포, DacFX, IIS와 같은 해당하는 종속성도 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-139">It will also install corresponding dependencies like Web Deploy, DacFX, and IIS, if needed.</span></span> 
   
   ![](./media/web-sites-migration-from-iis-server/install-progress.png)
   
   <span data-ttu-id="e2fa0-140">설치가 끝나면 Web App Migration Assistant가 자동으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-140">Once installed, Web Apps Migration Assistant automatically starts.</span></span>
5. <span data-ttu-id="e2fa0-141">**Migrate sites and databases from a remote server to Azure**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-141">Choose **Migrate sites and databases from a remote server to Azure**.</span></span> <span data-ttu-id="e2fa0-142">원격 서버의 관리자 자격 증명을 입력하고 **Continue**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-142">Enter the administrative credentials for the remote server and click **Continue**.</span></span> 
   
   ![](./media/web-sites-migration-from-iis-server/migrate-from-remote.png)
   
   <span data-ttu-id="e2fa0-143">로컬 서버에서 마이그레이션할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-143">You can of course choose to migrate from the local server.</span></span> <span data-ttu-id="e2fa0-144">원격 옵션은 프로덕션 IIS 서버에서 웹 사이트를 마이그레이션할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-144">The remote option is useful when you want to migrate websites from a production IIS server.</span></span>
   
   <span data-ttu-id="e2fa0-145">이제 마이그레이션 도구에서는 사이트, 응용 프로그램, 응용 프로그램 풀 및 종속성과 같은 IIS 서버 구성을 검사하여 마이그레이션 후보 웹 사이트를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-145">At this point the migration tool will inspect the your IIS server's configuration, such as Sites, Applications, Application Pools, and dependencies to identify candidate websites for migration.</span></span> 
6. <span data-ttu-id="e2fa0-146">아래 스크린샷에는 **Default Web Site**, **TimeTracker** 및 **CommerceNet4**의 세 개 웹 사이트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-146">The screenshot below shows three websites – **Default Web Site**, **TimeTracker**, and **CommerceNet4**.</span></span> <span data-ttu-id="e2fa0-147">이들 사이트 모두는 여기서 마이그레이션할 데이터베이스와 연결되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-147">All of them have an associated database that we want to migrate.</span></span> <span data-ttu-id="e2fa0-148">평가할 사이트를 모두 선택한 후 **Next**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-148">Select all of the sites you would like to assess and then click **Next**.</span></span>
   
   ![](./media/web-sites-migration-from-iis-server/select-migration-candidates.png)
7. <span data-ttu-id="e2fa0-149">**Upload** 를 클릭하여 준비 보고서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-149">Click **Upload** to upload the readiness report.</span></span> <span data-ttu-id="e2fa0-150">**save file locally**를 클릭하면 나중에 마이그레이션 도구를 다시 실행하고 앞에서 설명한 대로 저장된 준비 보고서를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-150">If you click **save file locally**, you can run the migration tool again later and upload the saved readiness report as noted earlier.</span></span>
   
   ![](./media/web-sites-migration-from-iis-server/upload-readiness-report.png)
   
   <span data-ttu-id="e2fa0-151">준비 보고서를 업로드하면 Azure에서는 준비 분석을 수행하고 결과를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-151">Once you upload the readiness report, Azure performs readiness analysis and shows you the results.</span></span> <span data-ttu-id="e2fa0-152">각 웹 사이트에 대한 평가 세부 정보를 읽고 문제를 모두 파악하거나 해결한 후에 계속 진행하세요.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-152">Read the assessment details for each website and make sure that you understand or have addressed all issues before you proceed.</span></span> 
   
   ![](./media/web-sites-migration-from-iis-server/readiness-assessment.png)
8. <span data-ttu-id="e2fa0-153">**Begin Migration**을 클릭하여 마이그레이션을 시작합니다. 이제 계정으로 로그인하기 위해 Azure로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-153">Click **Begin Migration** to start the migration.You will now be redirected to Azure to log into your account.</span></span> <span data-ttu-id="e2fa0-154">활성 Azure 구독이 있는 계정으로 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-154">It is important that you log in with an account that has an active Azure Subscription.</span></span> <span data-ttu-id="e2fa0-155">Azure 계정이 없는 경우 [여기](https://azure.microsoft.com/pricing/free-trial/?WT.srch=1&WT.mc_ID=SEM_)에서 평가판에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-155">If you do not have an Azure account then you can sign up for a free trial [here](https://azure.microsoft.com/pricing/free-trial/?WT.srch=1&WT.mc_ID=SEM_).</span></span> 
9. <span data-ttu-id="e2fa0-156">마이그레이션한 Azure Web Apps 및 데이터베이스에 사용할 테넌트 계정, Azure 구독 및 지역을 선택한 다음 **마이그레이션 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-156">Select the tenant account, Azure subscription and region to use for your migrated Azure web apps and databases, and then click **Start Migration**.</span></span> <span data-ttu-id="e2fa0-157">나중에 마이그레이션할 웹 사이트를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-157">You can select the websites to migrate later.</span></span>
   
   ![](./media/web-sites-migration-from-iis-server/choose-tenant-account.png)
10. <span data-ttu-id="e2fa0-158">다음 화면에서 다음과 같이 기본 마이그레이션 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-158">On the next screen you can make changes to the default migration settings, such as:</span></span>
    
    * <span data-ttu-id="e2fa0-159">기존 Azure SQL 데이터베이스를 사용하거나 새 Azure SQL 데이터베이스를 만들고 해당 자격 증명 구성</span><span class="sxs-lookup"><span data-stu-id="e2fa0-159">use an existing Azure SQL Database or create a new Azure SQL Database, and configure its credentials</span></span>
    * <span data-ttu-id="e2fa0-160">마이그레이션할 웹 사이트 선택</span><span class="sxs-lookup"><span data-stu-id="e2fa0-160">select the websites to migrate</span></span>
    * <span data-ttu-id="e2fa0-161">Azure 웹 앱 및 이 사이트와 연결된 SQL 데이터베이스 정의</span><span class="sxs-lookup"><span data-stu-id="e2fa0-161">define names for the Azure web apps and their linked SQL databases</span></span>
    * <span data-ttu-id="e2fa0-162">전역 설정 및 사이트 수준 설정 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="e2fa0-162">customize the global settings and site-level settings</span></span>
    
    <span data-ttu-id="e2fa0-163">아래 스크린샷에는 기본 설정을 사용하여 마이그레이션하도록 선택한 웹 사이트가 모두 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-163">The screenshot below shows all the websites selected for migration with the default settings.</span></span>
    
    ![](./media/web-sites-migration-from-iis-server/migration-settings.png)
    
    > [!NOTE]
    > <span data-ttu-id="e2fa0-164">사용자 지정 설정에서 **Enable Azure Active Directory** 확인란을 선택하면 Azure 웹앱이 [Azure Active Directory](../active-directory/active-directory-whatis.md)(**기본 디렉터리**)와 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-164">the **Enable Azure Active Directory** checkbox in custom settings integrates the Azure web app with [Azure Active Directory](../active-directory/active-directory-whatis.md) (the **Default Directory**).</span></span> <span data-ttu-id="e2fa0-165">Azure Active Directory를 온-프레미스 Active Directory와 동기화하는 방법에 대한 자세한 내용은 [디렉터리 통합](http://msdn.microsoft.com/library/jj573653)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-165">For more information on syncing Azure Active Directory with your on-premises Active Directory, see [Directory integration](http://msdn.microsoft.com/library/jj573653).</span></span>
    > 
    > 
11. <span data-ttu-id="e2fa0-166">원하는 대로 모두 변경했으면 **Create** 를 클릭하여 마이그레이션 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-166">Once you make all the desired changes, click **Create** to start the migration process.</span></span> <span data-ttu-id="e2fa0-167">마이그레이션 도구에서는 Azure SQL 데이터베이스와 Azure 웹 앱을 만들고 웹 사이트 콘텐츠와 데이터베이스를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-167">The migration tool will create the Azure SQL Database and Azure web app, and then publish the website content and databases.</span></span> <span data-ttu-id="e2fa0-168">마이그레이션 진행률이 마이그레이션 도구에 명확히 표시되며 끝에 마이그레이션된 사이트, 마이그레이션 성공 여부, 새로 만든 Azure 웹 앱에 대한 링크를 자세히 설명하는 요약 화면이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-168">The migration progress is clearly shown in the migration tool, and you will see a summary screen at the end, which details the sites migrated, whether they were successful, links to the newly-created Azure web apps.</span></span> 
    
    <span data-ttu-id="e2fa0-169">마이그레이션 중 오류가 발생하는 경우 마이그레이션 도구에서는 오류를 명확히 표시하고 변경 내용을 롤백합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-169">If any error occurs during migration, the migration tool will clearly indicate the failure and rollback the changes.</span></span> <span data-ttu-id="e2fa0-170">**Send Error Report** 단추를 클릭하면 오류 보고서를 캡처된 오류 호출 스택 및 빌드 메시지 본문과 함께 엔지니어링 팀에 직접 보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-170">You will also be able to send the error report directly to the engineering team by clicking the **Send Error Report** button, with the captured failure call stack and build message body.</span></span> 
    
    ![](./media/web-sites-migration-from-iis-server/migration-error-report.png)
    
    <span data-ttu-id="e2fa0-171">마이그레이션이 오류 없이 완료되면 **Give Feedback** 단추를 클릭하여 사용자 의견을 직접 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-171">If migrate succeeds without errors, you can also click the **Give Feedback** button to provide any feedback directly.</span></span> 
12. <span data-ttu-id="e2fa0-172">Azure 웹 앱에 대한 링크를 클릭하고 마이그레이션이 성공했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-172">Click the links to the Azure web apps and verify that the migration has succeeded.</span></span>
13. <span data-ttu-id="e2fa0-173">이제 Azure 앱 서비스에서 마이그레이션된 웹 앱을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-173">You can now manage the migrated web apps in Azure App Service.</span></span> <span data-ttu-id="e2fa0-174">이를 위해서는 [Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-174">To do this, log into the [Azure Portal](https://portal.azure.com).</span></span>
14. <span data-ttu-id="e2fa0-175">Azure 포털에서 마이그레이션된 웹 사이트(웹 앱으로 표시)를 보려면, 웹 앱 블레이드를 연 다음 그 중 하나를 클릭하여 연속 게시 구성, 백업 만들기, 자동 크기 조정 및 사용 또는 성능 모니터링과 같은 웹 앱 관리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-175">In the Azure Portal, open the Web Apps blade to see your migrated websites (shown as web apps), then click on any one of them to start managing the web app, such as configuring continuous publishing, creating backups, autoscaling, and monitoring usage or performance.</span></span>
    
    ![](./media/web-sites-migration-from-iis-server/TimeTrackerMigrated.png)

> [!NOTE]
> <span data-ttu-id="e2fa0-176">Azure 계정을 등록하기 전에 Azure App Service를 시작하려면 [App Service 체험](https://azure.microsoft.com/try/app-service/)으로 이동합니다. App Service에서 단기 스타터 웹앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-176">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="e2fa0-177">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fa0-177">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="e2fa0-178">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="e2fa0-178">What's changed</span></span>
* <span data-ttu-id="e2fa0-179">웹 사이트에서 앱 서비스로의 변경에 대한 지침은 [Azure App Service와 이 서비스가 기존 Azure 서비스에 미치는 영향](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="e2fa0-179">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

