---
title: "aaaMigrate 엔터프라이즈 웹 응용 프로그램 tooAzure 앱 서비스"
description: "Toouse 웹 응용 프로그램 마이그레이션 길잡이 tooquickly 기존 IIS 웹 사이트 tooAzure 앱 서비스 웹 앱을 마이그레이션할 하는 방법을 보여 줍니다."
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
ms.openlocfilehash: 7d66c5b799f0eefe85cbd9ba596ee0a05167f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-enterprise-web-app-tooazure-app-service"></a><span data-ttu-id="7b686-103">엔터프라이즈 웹 응용 프로그램 tooAzure 앱 서비스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="7b686-103">Migrate an enterprise web app tooAzure App Service</span></span>
<span data-ttu-id="7b686-104">인터넷 정보 서비스 (IIS)에서 6 이상을 실행 하는 기존 웹 사이트를 쉽게 마이그레이션할 수 있습니다 너무[앱 서비스 웹 앱](http://go.microsoft.com/fwlink/?LinkId=529714)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-104">You can easily migrate your existing websites that run on Internet Information Service (IIS) 6 or later too[App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="7b686-105">Windows Server 2003은 2015년 7월 14일에 지원이 종료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-105">Windows Server 2003 reached end of support on July 14th 2015.</span></span> <span data-ttu-id="7b686-106">Windows Server 2003 IIS 서버의 웹 사이트를 호스팅 중인는 웹 응용 프로그램 방법은 안전한, 낮은 비용 및 원활한 tookeep 온라인으로 웹 사이트 및 웹 응용 프로그램 마이그레이션 길잡이 도와 드립니다 hello 마이그레이션 프로세스를 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-106">If you are currently hosting your websites on an IIS server that is Windows Server 2003, Web Apps is a low-risk, low-cost, and low-friction way tookeep your websites online, and Web Apps Migration Assistant can help automate hello migration process for you.</span></span> 
> 
> 

<span data-ttu-id="7b686-107">[웹 앱 Migration Assistant](https://www.movemetothecloud.net/) IIS 서버 설치를 분석, 식별 사이트 수 마이그레이션된 tooApp 서비스 수를 마이그레이션할 수 없는 또는 hello 플랫폼에서 지원 하지 않는 모든 요소를 강조 표시 한 후 웹 사이트를 마이그레이션할 수 있습니다 및 연결 된 데이터베이스 tooAzure 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-107">[Web Apps Migration Assistant](https://www.movemetothecloud.net/) can analyze your IIS server installation, identify which sites can be migrated tooApp Service, highlight any elements that cannot be migrated or are unsupported on hello platform, and then migrate your websites and associated databases tooAzure.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="elements-verified-during-compatibility-analysis"></a><span data-ttu-id="7b686-108">호환성 분석 중 확인하는 요소</span><span class="sxs-lookup"><span data-stu-id="7b686-108">Elements Verified During Compatibility Analysis</span></span>
<span data-ttu-id="7b686-109">Migration Assistant hello 잠재적인 모든 문제 또는 온-프레미스 IIS tooAzure 앱 서비스 웹 앱에서에서 마이그레이션에 성공 하지 못할 수 있습니다는 차단 문제에 대 한 사용 하면 준비 보고서 tooidentify를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-109">hello Migration Assistant creates a readiness report tooidentify any potential causes for concern or blocking issues which may prevent a successful migration from on-premises IIS tooAzure App Service Web Apps.</span></span> <span data-ttu-id="7b686-110">일부 hello 주요 항목 toobe 인식 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-110">Some of hello key items toobe aware of are:</span></span>

* <span data-ttu-id="7b686-111">포트 바인딩 - 웹 앱은 HTTP 트래픽에는 포트 80, HTTPS 트래픽에는 포트 443만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-111">Port Bindings – Web Apps only supports Port 80 for HTTP and Port 443 for HTTPS traffic.</span></span> <span data-ttu-id="7b686-112">다른 포트 구성을 무시 되 고 트래픽이 라우팅된 too80 또는 443이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-112">Different port configurations will be ignored and traffic will be routed too80 or 443.</span></span> 
* <span data-ttu-id="7b686-113">인증 - 웹 앱은 익명 인증을 기본 지원하고 응용 프로그램에서 지정한 경우 폼 인증도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-113">Authentication – Web Apps supports Anonymous Authentication by default and Forms Authentication where specified by an application.</span></span> <span data-ttu-id="7b686-114">Windows 인증은 Azure Active Directory 및 ADFS와 통합해야만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-114">Windows Authentication can be used by integrating with Azure Active Directory and ADFS only.</span></span> <span data-ttu-id="7b686-115">예를 들어, 기본 인증과 같은 다른 인증 형식은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-115">All other forms of authentication - for example, Basic Authentication - are not currently supported.</span></span> 
* <span data-ttu-id="7b686-116">전역 어셈블리 캐시 (GAC) – hello GAC 웹 응용 프로그램에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-116">Global Assembly Cache (GAC) – hello GAC is not supported in Web Apps.</span></span> <span data-ttu-id="7b686-117">응용 프로그램 어셈블리를 참조 하는 경우는 toohello GAC를 일반적으로 배포에서는 웹 응용 프로그램에서 toodeploy toohello 응용 프로그램 bin 폴더를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-117">If your application references assemblies which you usually deploy toohello GAC, you will need toodeploy toohello application bin folder in Web Apps.</span></span> 
* <span data-ttu-id="7b686-118">IIS5 호환 모드 - 웹 앱에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-118">IIS5 Compatibility Mode – This is not supported in Web Apps.</span></span> 
* <span data-ttu-id="7b686-119">Hello에서 실행 하는 웹 응용 프로그램에서 응용 프로그램 풀 –, 각 사이트 및 해당 자식 응용 프로그램과 같은 응용 프로그램 풀.</span><span class="sxs-lookup"><span data-stu-id="7b686-119">Application Pools – In Web Apps, each site and its child applications run in hello same application pool.</span></span> <span data-ttu-id="7b686-120">사이트에 여러 응용 프로그램 풀을 사용 하 여 여러 자식 응용 프로그램을 같은 설정으로 단일 응용 프로그램 풀이 tooa를 통합 하거나 각 응용 프로그램 tooa 별도 웹 앱을 마이그레이션하십시오.</span><span class="sxs-lookup"><span data-stu-id="7b686-120">If your site has multiple child applications utilizing multiple application pools, consolidate them tooa single application pool with common settings or migrate each application tooa separate web app.</span></span>
* <span data-ttu-id="7b686-121">COM 구성 요소-웹 응용 프로그램의 COM 구성 요소 hello 플랫폼에서 hello 등록을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-121">COM Components – Web Apps does not allow hello registration of COM Components on hello platform.</span></span> <span data-ttu-id="7b686-122">웹 사이트 또는 응용 프로그램을 COM 구성 요소를 사용 하는 경우에 관리 코드에서 다시 작성 해야 하 고 hello 웹 사이트 또는 응용 프로그램에 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-122">If your websites or applications make use of any COM Components, you must rewrite them in managed code and deploy them with hello website or application.</span></span>
* <span data-ttu-id="7b686-123">ISAPI 확장-웹 응용 프로그램 ISAPI 확장의 hello 사용을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-123">ISAPI Extensions – Web Apps can support hello use of ISAPI Extensions.</span></span> <span data-ttu-id="7b686-124">Toodo hello 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-124">You need toodo hello following:</span></span>
  
  * <span data-ttu-id="7b686-125">웹 앱과 함께 hello Dll 배포</span><span class="sxs-lookup"><span data-stu-id="7b686-125">deploy hello DLLs with your web app</span></span> 
  * <span data-ttu-id="7b686-126">사용 하 여 hello Dll 등록 [Web.config](http://www.iis.net/configreference/system.webserver/isapifilters)</span><span class="sxs-lookup"><span data-stu-id="7b686-126">register hello DLLs using [Web.config](http://www.iis.net/configreference/system.webserver/isapifilters)</span></span>
  * <span data-ttu-id="7b686-127">"arbitrart ISAPI 확장 toobe 로드 하는 수"에 설명 된 hello 콘텐츠로 applicationHost.xdt 파일 hello 사이트 루트에 배치 [이 문서의 섹션](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples)</span><span class="sxs-lookup"><span data-stu-id="7b686-127">place an applicationHost.xdt file in hello site root with hello content outlined in "Allowing arbitrart ISAPI extensions toobe loaded" [section of this article](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples)</span></span> 
    
  
    
    <span data-ttu-id="7b686-128">방법의 자세한 예제와 웹 사이트, XML 문서 변환을 toouse 참조 [Microsoft Azure 웹 사이트를 변형](http://blogs.msdn.com/b/waws/archive/2014/06/17/transform-your-microsoft-azure-web-site.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-128">For more examples of how toouse XML Document Transformations with your website, see [Transform your Microsoft Azure Web Site](http://blogs.msdn.com/b/waws/archive/2014/06/17/transform-your-microsoft-azure-web-site.aspx).</span></span>
* <span data-ttu-id="7b686-129">SharePoint, FPSE(Front Page Server Extensions), FTP, SSL 인증서와 같은 다른 구성 요소는 마이그레이션되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-129">Other components like SharePoint, front page server extensions (FPSE), FTP, SSL certificates will not be migrated.</span></span>

## <a name="how-toouse-hello-web-apps-migration-assistant"></a><span data-ttu-id="7b686-130">어떻게 toouse hello 웹 응용 프로그램 마이그레이션 길잡이</span><span class="sxs-lookup"><span data-stu-id="7b686-130">How toouse hello Web Apps Migration Assistant</span></span>
<span data-ttu-id="7b686-131">이 섹션을 단계별로 예제 tootoomigrate 웹 사이트는 온-프레미스 Windows Server 2003 R2 (IIS 6.0) 컴퓨터에서 실행 하 고 사용 하는 SQL Server 데이터베이스:</span><span class="sxs-lookup"><span data-stu-id="7b686-131">This section steps through an example tootoomigrate a few websites that use a SQL Server database and running on an on-premises Windows Server 2003 R2 (IIS 6.0) machine:</span></span>

1. <span data-ttu-id="7b686-132">Hello IIS에서 서버 또는 클라이언트 컴퓨터를 탐색 너무[https://www.movemetothecloud.net/](https://www.movemetothecloud.net/)</span><span class="sxs-lookup"><span data-stu-id="7b686-132">On hello IIS server or your client machine navigate too[https://www.movemetothecloud.net/](https://www.movemetothecloud.net/)</span></span> 
   
   ![](./media/web-sites-migration-from-iis-server/migration-tool-homepage.png)
2. <span data-ttu-id="7b686-133">Hello를 클릭 하 여 웹 응용 프로그램 마이그레이션 길잡이 설치 **전용 IIS 서버** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-133">Install Web Apps Migration Assistant by clicking on hello **Dedicated IIS Server** button.</span></span> <span data-ttu-id="7b686-134">더 많은 옵션 옵션 hello 가까운 미래에에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-134">More options will be options in hello near future.</span></span> 
3. <span data-ttu-id="7b686-135">Hello 클릭 **도구 설치** 컴퓨터에 웹 응용 프로그램 마이그레이션 길잡이 tooinstall 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-135">Click hello **Install Tool** button tooinstall Web Apps Migration Assistant on your machine.</span></span>
   
   ![](./media/web-sites-migration-from-iis-server/install-page.png)
   
   > [!NOTE]
   > <span data-ttu-id="7b686-136">클릭할 수도 있습니다 **오프 라인 설치에 대 한 다운로드** toohello 연결 된 서버에서 설치에 대 한 toodownload ZIP 파일 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-136">You can also click **Download for offline install** toodownload a ZIP file for installing on servers not connected toohello internet.</span></span> <span data-ttu-id="7b686-137">클릭할 수 있는 또는 **기존 마이그레이션 준비 보고서 업로드**, 기존 마이그레이션 준비 상태 보고서를 이전에 생성 된 (나중에 설명)으로 고급 옵션 toowork은 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-137">Or, you can click **Upload an existing migration readiness report**, which is an advanced option toowork with an existing migration readiness report that you previously generated (explained later).</span></span>
   > 
   > 
4. <span data-ttu-id="7b686-138">Hello에 **응용 프로그램 설치** 화면 **설치** tooinstall 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-138">In hello **Application Install** screen, click **Install** tooinstall on your machine.</span></span> <span data-ttu-id="7b686-139">필요한 경우 웹 배포, DacFX, IIS와 같은 해당하는 종속성도 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-139">It will also install corresponding dependencies like Web Deploy, DacFX, and IIS, if needed.</span></span> 
   
   ![](./media/web-sites-migration-from-iis-server/install-progress.png)
   
   <span data-ttu-id="7b686-140">설치가 끝나면 Web App Migration Assistant가 자동으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-140">Once installed, Web Apps Migration Assistant automatically starts.</span></span>
5. <span data-ttu-id="7b686-141">선택 **원격 서버 tooAzure에서 사이트 및 데이터베이스를 마이그레이션할**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-141">Choose **Migrate sites and databases from a remote server tooAzure**.</span></span> <span data-ttu-id="7b686-142">원격 서버 hello에 대 한 hello 관리 자격 증명을 입력 하 고 클릭 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-142">Enter hello administrative credentials for hello remote server and click **Continue**.</span></span> 
   
   ![](./media/web-sites-migration-from-iis-server/migrate-from-remote.png)
   
   <span data-ttu-id="7b686-143">물론 hello 로컬 서버에서 toomigrate를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-143">You can of course choose toomigrate from hello local server.</span></span> <span data-ttu-id="7b686-144">hello 원격 옵션은 프로덕션 IIS 서버에서 toomigrate 웹 사이트를 원하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-144">hello remote option is useful when you want toomigrate websites from a production IIS server.</span></span>
   
   <span data-ttu-id="7b686-145">Hello 마이그레이션 도구는 조사 하는 시점에서 사이트, 응용 프로그램, 응용 프로그램 풀 및 종속성 tooidentify 후보 웹 사이트와 같이 마이그레이션에 대 한 IIS 서버의 구성을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-145">At this point hello migration tool will inspect hello your IIS server's configuration, such as Sites, Applications, Application Pools, and dependencies tooidentify candidate websites for migration.</span></span> 
6. <span data-ttu-id="7b686-146">hello 아래 스크린샷은 3 개 웹 사이트- **기본 웹 사이트**, **TimeTracker**, 및 **CommerceNet4**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-146">hello screenshot below shows three websites – **Default Web Site**, **TimeTracker**, and **CommerceNet4**.</span></span> <span data-ttu-id="7b686-147">했 toomigrate 한다고 하는 연결 된 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-147">All of them have an associated database that we want toomigrate.</span></span> <span data-ttu-id="7b686-148">모든 tooassess 선택한 다음 클릭 hello 사이트 선택 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-148">Select all of hello sites you would like tooassess and then click **Next**.</span></span>
   
   ![](./media/web-sites-migration-from-iis-server/select-migration-candidates.png)
7. <span data-ttu-id="7b686-149">클릭 **업로드** tooupload hello 준비 보고서입니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-149">Click **Upload** tooupload hello readiness report.</span></span> <span data-ttu-id="7b686-150">클릭 하면 **파일을 로컬로 저장**, 나중에 다시 hello 마이그레이션 도구를 실행할 수 있습니다 및 업로드 hello 설명한 것 처럼 준비 보고서를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-150">If you click **save file locally**, you can run hello migration tool again later and upload hello saved readiness report as noted earlier.</span></span>
   
   ![](./media/web-sites-migration-from-iis-server/upload-readiness-report.png)
   
   <span data-ttu-id="7b686-151">Hello 준비 보고서를 업로드 하면 Azure 준비 상태 분석 및 결과 hello 보여 줍니다. 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-151">Once you upload hello readiness report, Azure performs readiness analysis and shows you hello results.</span></span> <span data-ttu-id="7b686-152">각 웹 사이트에 대 한 hello 평가 정보를 읽고 이해할 수 있고 계속 진행 하기 전에 모든 문제를 해결 한 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-152">Read hello assessment details for each website and make sure that you understand or have addressed all issues before you proceed.</span></span> 
   
   ![](./media/web-sites-migration-from-iis-server/readiness-assessment.png)
8. <span data-ttu-id="7b686-153">클릭 **마이그레이션 시작** toostart hello 마이그레이션. 이제 사용자의 계정으로 리디렉션된 tooAzure toolog 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-153">Click **Begin Migration** toostart hello migration.You will now be redirected tooAzure toolog into your account.</span></span> <span data-ttu-id="7b686-154">활성 Azure 구독이 있는 계정으로 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-154">It is important that you log in with an account that has an active Azure Subscription.</span></span> <span data-ttu-id="7b686-155">Azure 계정이 없는 경우 [여기](https://azure.microsoft.com/pricing/free-trial/?WT.srch=1&WT.mc_ID=SEM_)에서 평가판에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-155">If you do not have an Azure account then you can sign up for a free trial [here](https://azure.microsoft.com/pricing/free-trial/?WT.srch=1&WT.mc_ID=SEM_).</span></span> 
9. <span data-ttu-id="7b686-156">Hello 테 넌 트 계정, Azure 구독 및 지역 toouse 마이그레이션된 Azure 웹 앱 및 데이터베이스를 선택한 다음 클릭 **마이그레이션 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-156">Select hello tenant account, Azure subscription and region toouse for your migrated Azure web apps and databases, and then click **Start Migration**.</span></span> <span data-ttu-id="7b686-157">나중에 웹 사이트 toomigrate hello를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-157">You can select hello websites toomigrate later.</span></span>
   
   ![](./media/web-sites-migration-from-iis-server/choose-tenant-account.png)
10. <span data-ttu-id="7b686-158">Hello 다음 화면에서 변경할 수 있습니다 toohello 기본 마이그레이션 설정 같은:</span><span class="sxs-lookup"><span data-stu-id="7b686-158">On hello next screen you can make changes toohello default migration settings, such as:</span></span>
    
    * <span data-ttu-id="7b686-159">기존 Azure SQL 데이터베이스를 사용하거나 새 Azure SQL 데이터베이스를 만들고 해당 자격 증명 구성</span><span class="sxs-lookup"><span data-stu-id="7b686-159">use an existing Azure SQL Database or create a new Azure SQL Database, and configure its credentials</span></span>
    * <span data-ttu-id="7b686-160">웹 사이트 toomigrate hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-160">select hello websites toomigrate</span></span>
    * <span data-ttu-id="7b686-161">hello Azure 웹 앱 및 연결 된 SQL 데이터베이스에 대 한 이름 정의</span><span class="sxs-lookup"><span data-stu-id="7b686-161">define names for hello Azure web apps and their linked SQL databases</span></span>
    * <span data-ttu-id="7b686-162">hello 전역 설정 및 사이트 수준 설정 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="7b686-162">customize hello global settings and site-level settings</span></span>
    
    <span data-ttu-id="7b686-163">아래의 스크린 샷은 hello hello 기본 설정 사용 하 여 마이그레이션을 위해 선택한 모든 hello 웹 사이트를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-163">hello screenshot below shows all hello websites selected for migration with hello default settings.</span></span>
    
    ![](./media/web-sites-migration-from-iis-server/migration-settings.png)
    
    > [!NOTE]
    > <span data-ttu-id="7b686-164">hello **Azure Active Directory를 사용 하도록 설정** hello Azure 웹 앱을 통합 하는 사용자 지정 설정에 대 한 확인란을 [Azure Active Directory](../active-directory/active-directory-whatis.md) (hello **기본 디렉터리**).</span><span class="sxs-lookup"><span data-stu-id="7b686-164">hello **Enable Azure Active Directory** checkbox in custom settings integrates hello Azure web app with [Azure Active Directory](../active-directory/active-directory-whatis.md) (hello **Default Directory**).</span></span> <span data-ttu-id="7b686-165">Azure Active Directory를 온-프레미스 Active Directory와 동기화하는 방법에 대한 자세한 내용은 [디렉터리 통합](http://msdn.microsoft.com/library/jj573653)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b686-165">For more information on syncing Azure Active Directory with your on-premises Active Directory, see [Directory integration](http://msdn.microsoft.com/library/jj573653).</span></span>
    > 
    > 
11. <span data-ttu-id="7b686-166">모든 필요한 hello을 변경한 후 클릭 **만들기** toostart hello 마이그레이션 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-166">Once you make all hello desired changes, click **Create** toostart hello migration process.</span></span> <span data-ttu-id="7b686-167">hello 마이그레이션 도구는 hello Azure SQL 데이터베이스 및 Azure 웹 앱을 만들고 hello 웹 사이트 콘텐츠 및 데이터베이스를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-167">hello migration tool will create hello Azure SQL Database and Azure web app, and then publish hello website content and databases.</span></span> <span data-ttu-id="7b686-168">hello 마이그레이션 진행률 hello 마이그레이션 도구에 명확 하 게 표시 되 고 요약 화면 hello 끝, 세부 정보 hello 사이트 마이그레이션, 성공 했는지 여부, 링크 toohello 새로 만든 Azure 웹 앱에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-168">hello migration progress is clearly shown in hello migration tool, and you will see a summary screen at hello end, which details hello sites migrated, whether they were successful, links toohello newly-created Azure web apps.</span></span> 
    
    <span data-ttu-id="7b686-169">모든 마이그레이션 도구는 명확 하 게 hello를 마이그레이션하는 동안 오류가 발생 하는 경우에 hello 실패 하 여 롤백된 hello 변경 내용을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-169">If any error occurs during migration, hello migration tool will clearly indicate hello failure and rollback hello changes.</span></span> <span data-ttu-id="7b686-170">Hello를 클릭 하 여 toohello 엔지니어링 팀에 직접 수 toosend hello 오류 보고서를 할당할 수도 있습니다 **오류 보고서 보내기** hello 캡처된 오류 호출 스택과 함께 단추 및 메시지 본문을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-170">You will also be able toosend hello error report directly toohello engineering team by clicking hello **Send Error Report** button, with hello captured failure call stack and build message body.</span></span> 
    
    ![](./media/web-sites-migration-from-iis-server/migration-error-report.png)
    
    <span data-ttu-id="7b686-171">하는 경우 마이그레이션에 성공 하면 오류 없이 클릭할 수도 있습니다 hello **의견 제공** 직접 tooprovide 피드백 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-171">If migrate succeeds without errors, you can also click hello **Give Feedback** button tooprovide any feedback directly.</span></span> 
12. <span data-ttu-id="7b686-172">Hello 링크 toohello Azure 웹 앱을 클릭 하 고 hello 마이그레이션에 성공 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-172">Click hello links toohello Azure web apps and verify that hello migration has succeeded.</span></span>
13. <span data-ttu-id="7b686-173">이제 관리할 수 있습니다 hello Azure 앱 서비스에서 웹 앱을 마이그레이션.</span><span class="sxs-lookup"><span data-stu-id="7b686-173">You can now manage hello migrated web apps in Azure App Service.</span></span> <span data-ttu-id="7b686-174">toodo hello에이 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-174">toodo this, log into hello [Azure Portal](https://portal.azure.com).</span></span>
14. <span data-ttu-id="7b686-175">Hello Azure 포털에서에서 열고 hello 웹 앱 블레이드 toosee 마이그레이션된 웹 사이트 (웹 앱으로 표시), 클릭 중 하나라도 toostart 연속 게시, 자동 크기 조정, 백업 만들기 및 사용 현황 모니터링을 구성 하는 등의 hello 웹 앱 관리 또는 성능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-175">In hello Azure Portal, open hello Web Apps blade toosee your migrated websites (shown as web apps), then click on any one of them toostart managing hello web app, such as configuring continuous publishing, creating backups, autoscaling, and monitoring usage or performance.</span></span>
    
    ![](./media/web-sites-migration-from-iis-server/TimeTrackerMigrated.png)

> [!NOTE]
> <span data-ttu-id="7b686-176">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-176">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="7b686-177">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b686-177">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="7b686-178">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="7b686-178">What's changed</span></span>
* <span data-ttu-id="7b686-179">웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="7b686-179">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

