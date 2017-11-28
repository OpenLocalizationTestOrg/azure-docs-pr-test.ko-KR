---
title: "hello Azure 포털에서에서 Azure BizTalk 서비스 aaaCreate | Microsoft Docs"
description: "자세한 내용은 방법 tooprovision hello; Azure 포털에서에서 Azure BizTalk 서비스를 만들거나 MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 3ad18876-a649-40d6-9aa0-1509c1d62c43
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 6781cadada8ac9c84e1fe045d2b0f995811f75b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-biztalk-services-using-hello-azure-portal"></a><span data-ttu-id="68d09-103">Hello Azure 포털을 사용 하 여 BizTalk 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="68d09-103">Create BizTalk Services using hello Azure portal</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]


> [!TIP]
> <span data-ttu-id="68d09-104">toohello Azure 포털에서에서 toosign, Azure 계정 및 Azure 구독 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-104">toosign in toohello Azure portal, you need an Azure account and Azure subscription.</span></span> <span data-ttu-id="68d09-105">계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-105">If you don't have an account, you can create a free trial account within a few minutes.</span></span> <span data-ttu-id="68d09-106">[Azure 무료 평가판](http://go.microsoft.com/fwlink/p/?LinkID=239738)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68d09-106">See [Azure Free Trial](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span></span>


## <span data-ttu-id="68d09-107"><a name="CreateService"></a>BizTalk 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="68d09-107"><a name="CreateService"></a>Create a BizTalk Service</span></span>
<span data-ttu-id="68d09-108">Hello 선택한 버전에 따라 BizTalk 서비스 설정의 일부만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-108">Depending on hello Edition you choose, not all BizTalk Service settings may be available.</span></span>

1. <span data-ttu-id="68d09-109">Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=213885)합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="68d09-110">Hello 아래쪽 탐색 창에서 선택 **새로**:</span><span class="sxs-lookup"><span data-stu-id="68d09-110">In hello bottom navigation pane, select **NEW**:</span></span>  
   <span data-ttu-id="68d09-111">![Hello 새로 만들기 단추를 선택 합니다.][NEWButton]</span><span class="sxs-lookup"><span data-stu-id="68d09-111">![Select hello New button][NEWButton]</span></span>
3. <span data-ttu-id="68d09-112">**APP SERVICES** > **BIZTALK SERVICE** > **사용자 지정 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-112">Select **APP SERVICES** > **BIZTALK SERVICE** > **CUSTOM CREATE**:</span></span>  
   <span data-ttu-id="68d09-113">![BizTalk 서비스 선택 및 사용자 지정 만들기 선택][NewBizTalkService]</span><span class="sxs-lookup"><span data-stu-id="68d09-113">![Select BizTalk Service and select Custom Create][NewBizTalkService]</span></span>
4. <span data-ttu-id="68d09-114">Hello BizTalk 서비스 설정을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-114">Enter hello BizTalk Service settings:</span></span>
   
    <table border="1">
    <tr>
    <td><span data-ttu-id="68d09-115"><strong>BizTalk 서비스 이름</strong></span><span class="sxs-lookup"><span data-stu-id="68d09-115"><strong>BizTalk service name</strong></span></span></td>
    <td><span data-ttu-id="68d09-116">아무 이름이나 입력할 수 있지만 구체적이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-116">You can enter any name but be specific.</span></span> <span data-ttu-id="68d09-117">일부 사례:</span><span class="sxs-lookup"><span data-stu-id="68d09-117">Some examples include:</span></span><br/><br/><span data-ttu-id="68d09-118">
    <em>mycompany</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="68d09-118">
    <em>mycompany</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="68d09-119">
    <em>mycompanymyapplication</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="68d09-119">
    <em>mycompanymyapplication</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="68d09-120">
    <em>myapplication</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="68d09-120">
    <em>myapplication</em>.biztalk.windows.net</span></span><br/><br/><span data-ttu-id="68d09-121">". biztalk.windows.net" 입력 하면 자동으로 추가 된 toohello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-121">".biztalk.windows.net" is automatically added toohello name you enter.</span></span> <span data-ttu-id="68d09-122">이렇게 하면 URL을 같은 BizTalk 서비스를 사용 하는 tooaccess 만들어집니다 <strong>https://<em>myapplication</em>. biztalk.windows.net</strong>합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-122">This creates a URL that is used tooaccess your BizTalk Service, like <strong>https://<em>myapplication</em>.biztalk.windows.net</strong>.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="68d09-123"><strong>에디션</strong></span><span class="sxs-lookup"><span data-stu-id="68d09-123"><strong>Edition</strong></span></span></td>
    <td><span data-ttu-id="68d09-124">Hello 테스트/개발 단계에 있는 경우 선택 <strong>개발자</strong>합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-124">If you are in hello testing/development phase, choose <strong>Developer</strong>.</span></span> <span data-ttu-id="68d09-125">Hello 프로덕션 단계에 있는 경우 사용 하 여 hello <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk 서비스: 버전 차트</a> toodetermine 경우 <strong>프리미엄</strong>, <strong>표준</strong>, 또는 <strong>Basic</strong>hello 비즈니스 시나리오에 대 한 올바른 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-125">If you are in hello production phase, use hello <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk Services: Editions Chart</a> toodetermine if <strong>Premium</strong>, <strong>Standard</strong>, or <strong>Basic</strong> is hello correct choice for your business scenario.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="68d09-126"><strong>지역</strong></span><span class="sxs-lookup"><span data-stu-id="68d09-126"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="68d09-127">지리적인 지역의 toohost hello BizTalk 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-127">Select hello geographic region toohost your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="68d09-128"><strong>도메인 URL</strong></span><span class="sxs-lookup"><span data-stu-id="68d09-128"><strong>Domain URL</strong></span></span></td>
    <td><span data-ttu-id="68d09-129"><strong>옵션</strong>.</span><span class="sxs-lookup"><span data-stu-id="68d09-129"><strong>Optional</strong>.</span></span> <span data-ttu-id="68d09-130">기본적으로 hello 도메인 URL은 <em>m e</em>. biztalk.windows.net 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-130">By default, hello domain URL is <em>YourBizTalkServiceName</em>.biztalk.windows.net.</span></span> <span data-ttu-id="68d09-131">사용자 지정 도메인을 입력할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-131">A custom domain can also be entered.</span></span> <span data-ttu-id="68d09-132">예를 들어 도메인이 <em>contoso</em>이면 다음과 같이 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-132">For example, if your domain is <em>contoso</em>, you can enter:</span></span> <br/><br/><span data-ttu-id="68d09-133">
    <em>MyCompany</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="68d09-133">
    <em>MyCompany</em>.contoso.com</span></span><br/><span data-ttu-id="68d09-134">
    <em>MyCompanyMyApplication</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="68d09-134">
    <em>MyCompanyMyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="68d09-135">
    <em>MyApplication</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="68d09-135">
    <em>MyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="68d09-136">
    <em>YourBizTalkServiceName</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="68d09-136">
    <em>YourBizTalkServiceName</em>.contoso.com</span></span><br/>
    </td>
    </tr>
    </table>
<span data-ttu-id="68d09-137">Hello 다음 화살표를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-137">Select hello NEXT arrow.</span></span>
<span data-ttu-id="68d09-138">5.</span><span class="sxs-lookup"><span data-stu-id="68d09-138">5.</span></span> <span data-ttu-id="68d09-139">Hello 저장소 및 데이터베이스 설정을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-139">Enter hello Storage and Database Settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="68d09-140"><strong>저장소 계정 모니터링/보관</strong></span><span class="sxs-lookup"><span data-stu-id="68d09-140"><strong>Monitoring/Archiving storage account</strong></span></span></td>
    <td><span data-ttu-id="68d09-141">기존 저장소 계정을 선택하거나 새 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-141">Select an existing storage account or create a new storage account.</span></span> <br/><br/><span data-ttu-id="68d09-142">새 저장소 계정을 만드는 경우 입력 hello <strong>저장소 계정 이름</strong>합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-142">If you create a new Storage account, enter hello <strong>Storage Account Name</strong>.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="68d09-143"><strong>데이터베이스 추적</strong></span><span class="sxs-lookup"><span data-stu-id="68d09-143"><strong>Tracking database</strong></span></span></td>
    <td><span data-ttu-id="68d09-144">기존 Azure SQL 데이터베이스를 사용하는 경우 다른 BizTalk 서비스에서는 이 데이터베이스를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-144">If you use an existing Azure SQL Database, it cannot be used by another BizTalk Service.</span></span> <span data-ttu-id="68d09-145">Hello 로그인 이름 및 Azure SQL 데이터베이스 서버를 만들 때 입력 한 암호가 필요.</span><span class="sxs-lookup"><span data-stu-id="68d09-145">You need hello login name and password entered when that Azure SQL Database Server was created.</span></span><br/><br/><span data-ttu-id="68d09-146"><strong>팁</strong> hello 추적 데이터베이스 만들기 및 모니터링/보관 저장소 계정에 동일한 지역으로 BizTalk 서비스 hello hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-146"><strong>TIP</strong> Create hello Tracking database and Monitoring/Archiving storage account in hello same region as hello BizTalk Service.</span></span></td>
    </tr>
    </table>
<span data-ttu-id="68d09-147">Hello 다음 화살표를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-147">Select hello NEXT arrow.</span></span>
<span data-ttu-id="68d09-148">6.</span><span class="sxs-lookup"><span data-stu-id="68d09-148">6.</span></span> <span data-ttu-id="68d09-149">Hello 데이터베이스 설정을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-149">Enter hello Database settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="68d09-150"><strong>Name</strong></span><span class="sxs-lookup"><span data-stu-id="68d09-150"><strong>Name</strong></span></span></td>
    <td><span data-ttu-id="68d09-151">경우에 사용 가능한 <strong>새 SQL 데이터베이스 인스턴스를 만들고</strong> hello 이전 화면에서를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-151">Available when <strong>Create a new SQL Database instance</strong> is selected in hello previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="68d09-152">BizTalk 서비스에서 사용 하는 SQL 데이터베이스 이름 toobe를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-152">Enter a SQL Database name toobe used by your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="68d09-153"><strong>서버</strong></span><span class="sxs-lookup"><span data-stu-id="68d09-153"><strong>Server</strong></span></span></td>
    <td><span data-ttu-id="68d09-154">경우에 사용 가능한 <strong>새 SQL 데이터베이스 인스턴스를 만들고</strong> hello 이전 화면에서를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-154">Available when <strong>Create a new SQL Database instance</strong> is selected in hello previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="68d09-155">기존 SQL Database 서버를 선택하거나 새 SQL Database 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-155">Select an existing SQL Database Server or create a new SQL Database server.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="68d09-156"><strong>서버 로그인 이름</strong></span><span class="sxs-lookup"><span data-stu-id="68d09-156"><strong>Server login name</strong></span></span></td>
    <td><span data-ttu-id="68d09-157">Hello 로그인 사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-157">Enter hello login user name.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="68d09-158"><strong>서버 로그인 암호</strong></span><span class="sxs-lookup"><span data-stu-id="68d09-158"><strong>Server login password</strong></span></span></td>
    <td><span data-ttu-id="68d09-159">Hello 로그인 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-159">Enter hello login password.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="68d09-160"><strong>지역</strong></span><span class="sxs-lookup"><span data-stu-id="68d09-160"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="68d09-161"><strong>새 SQL Database 인스턴스 만들기</strong>를 선택한 경우에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-161">Available when <strong>Create a new SQL Database instance</strong> is selected.</span></span> <span data-ttu-id="68d09-162">지리적인 지역의 toohost hello SQL 데이터베이스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-162">Select hello geographic region toohost your SQL Database.</span></span></td>
    </tr>
    </table>

<span data-ttu-id="68d09-163">Hello 확인 표시가 toocomplete hello 마법사를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-163">Select hello check mark toocomplete hello wizard.</span></span> <span data-ttu-id="68d09-164">hello 진행률 아이콘이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-164">hello progress icon appears:</span></span>  
![완료 시 진행률 아이콘 표시][ProgressComplete]

<span data-ttu-id="68d09-166">완료 되 면 생성 되 고 응용 프로그램에 대 한 준비 hello Azure BizTalk 서비스는 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-166">When complete, hello Azure BizTalk Service is created and ready for your applications.</span></span> <span data-ttu-id="68d09-167">hello 기본 설정을 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-167">hello default settings are sufficient.</span></span> <span data-ttu-id="68d09-168">Toochange hello 기본 설정을 선택 **BIZTALK 서비스** 왼쪽된 탐색 창의 hello와 BizTalk 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-168">If you want toochange hello default settings, select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service.</span></span> <span data-ttu-id="68d09-169">추가 설정은 hello에 표시 됩니다 [대시보드, 모니터 및 배율 탭](biztalk-dashboard-monitor-scale-tabs.md) hello 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-169">Additional settings are displayed in hello [Dashboard, Monitor, and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md) at hello top.</span></span>

<span data-ttu-id="68d09-170">Hello hello BizTalk 서비스의 상태에 따라 완료할 수 없는 일부 작업은 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-170">Depending on hello state of hello BizTalk Service, there are some operations that cannot be completed.</span></span> <span data-ttu-id="68d09-171">이러한 작업의 목록에 대 한 이동 너무[BizTalk Services 상태 차트](biztalk-service-state-chart.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-171">For a list of these operations, go too[BizTalk Services State Chart](biztalk-service-state-chart.md).</span></span>

## <a name="post-provisioning-steps"></a><span data-ttu-id="68d09-172">프로비전 후 단계</span><span class="sxs-lookup"><span data-stu-id="68d09-172">Post-provisioning steps</span></span>
* [<span data-ttu-id="68d09-173">로컬 컴퓨터에 hello 인증서 설치</span><span class="sxs-lookup"><span data-stu-id="68d09-173">Install hello certificate on a local computer</span></span>](#InstallCert)
* [<span data-ttu-id="68d09-174">프로덕션이 준비된 인증서 추가</span><span class="sxs-lookup"><span data-stu-id="68d09-174">Add a production-ready certificate</span></span>](#AddCert)
* [<span data-ttu-id="68d09-175">Hello 액세스 제어 네임 스페이스 가져오기</span><span class="sxs-lookup"><span data-stu-id="68d09-175">Get hello Access Control namespace</span></span>](#ACS)

#### <span data-ttu-id="68d09-176"><a name="InstallCert"></a>로컬 컴퓨터에 hello 인증서 설치</span><span class="sxs-lookup"><span data-stu-id="68d09-176"><a name="InstallCert"></a>Install hello certificate on a local computer</span></span>
<span data-ttu-id="68d09-177">BizTalk 서비스 프로비전의 일부로 자체 서명된 인증서가 만들어지고 BizTalk 서비스 구독에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-177">As part of BizTalk Service provisioning, a self-signed certificate is created and associated with your BizTalk Service subscription.</span></span> <span data-ttu-id="68d09-178">이 인증서를 다운로드 하 여 BizTalk 서비스 응용 프로그램을 배포 하거나 송신 메시지 tooa BizTalk 서비스 끝점에서 컴퓨터에 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-178">You must download this certificate and install it on computers from where you either deploy BizTalk Service applications or send messages tooa BizTalk Service endpoint.</span></span>

1. <span data-ttu-id="68d09-179">Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=213885)합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-179">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="68d09-180">선택 **BIZTALK 서비스** 왼쪽된 탐색 창의 hello와 BizTalk 서비스 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-180">Select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service subscription.</span></span>
3. <span data-ttu-id="68d09-181">선택 hello **대시보드** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-181">Select hello **Dashboard** tab.</span></span>
4. <span data-ttu-id="68d09-182">**SSL 인증서 다운로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-182">Select **Download SSL Certificate**:</span></span>  
   <span data-ttu-id="68d09-183">![SSL 인증서 수정][QuickGlance]</span><span class="sxs-lookup"><span data-stu-id="68d09-183">![Modify SSL Certificate][QuickGlance]</span></span>
5. <span data-ttu-id="68d09-184">Hello 인증서를 두 번 클릭 하 고 hello 마법사 tooinstall hello 인증서를 통해 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-184">Double-click hello certificate and run through hello wizard tooinstall hello certificate.</span></span> <span data-ttu-id="68d09-185">Hello 아래의 hello 인증서가 설치 되었는지 확인 **신뢰할 수 있는 루트 인증 기관** 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-185">Make sure you install hello certificate under hello **Trusted Root Certificate Authorities** store.</span></span>

#### <span data-ttu-id="68d09-186"><a name="AddCert"></a>프로덕션이 준비된 인증서 추가</span><span class="sxs-lookup"><span data-stu-id="68d09-186"><a name="AddCert"></a>Add a production-ready certificate</span></span>
<span data-ttu-id="68d09-187">hello 자체 서명 된 인증서를 개발 환경 에서만 사용 하기 위한 BizTalk 서비스를 만들 때 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-187">hello self-signed certificate that is automatically created when creating BizTalk Services is intended for use in development environments only.</span></span> <span data-ttu-id="68d09-188">프로덕션 시나리오의 경우 이 인증서를 프로덕션이 준비된 인증서로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-188">For production scenarios, replace it with a production-ready certificate.</span></span>

1. <span data-ttu-id="68d09-189">Hello에 **대시보드** 탭에서 **업데이트 SSL 인증서**합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-189">On hello **Dashboard** tab, select **Update SSL Certificate**.</span></span>
2. <span data-ttu-id="68d09-190">SSL 인증서를 개인 tooyour 찾아보기 (*CertificateName*.pfx) BizTalk 서비스 이름을 포함 하, hello 암호를 입력 한 다음 hello 확인 표시를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-190">Browse tooyour private SSL certificate (*CertificateName*.pfx) that includes your BizTalk Service name, enter hello password, and then click hello check mark.</span></span>

#### <span data-ttu-id="68d09-191"><a name="ACS"></a>Hello 액세스 제어 네임 스페이스 가져오기</span><span class="sxs-lookup"><span data-stu-id="68d09-191"><a name="ACS"></a>Get hello Access Control namespace</span></span>
1. <span data-ttu-id="68d09-192">Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=213885)합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-192">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="68d09-193">선택 **BIZTALK 서비스** 왼쪽된 탐색 창의 hello와 BizTalk 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-193">Select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service.</span></span>
3. <span data-ttu-id="68d09-194">Hello 작업 표시줄에서 선택 **연결 정보**:</span><span class="sxs-lookup"><span data-stu-id="68d09-194">In hello task bar, select **Connection Information**:</span></span>  
   <span data-ttu-id="68d09-195">![연결 정보 선택][ACSConnectInfo]</span><span class="sxs-lookup"><span data-stu-id="68d09-195">![Select Connection Information][ACSConnectInfo]</span></span>
4. <span data-ttu-id="68d09-196">Hello 액세스 제어 값을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-196">Copy hello Access Control values.</span></span>

<span data-ttu-id="68d09-197">Visual Studio에서 BizTalk 서비스를 배포할 때 이 액세스 제어 네임스페이스를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-197">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="68d09-198">BizTalk 서비스에 대 한 액세스 제어 네임 스페이스 hello 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-198">hello Access Control namespace is automatically created for your BizTalk Service.</span></span>

<span data-ttu-id="68d09-199">hello 액세스 제어 값 응용 프로그램과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-199">hello Access Control values can be used with any application.</span></span> <span data-ttu-id="68d09-200">Azure BizTalk 서비스를 만들면이 액세스 제어 네임 스페이스는 BizTalk 서비스 배포와 hello 인증을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-200">When Azure BizTalk Services is created, this Access Control namespace controls hello authentication with your BizTalk Service deployment.</span></span> <span data-ttu-id="68d09-201">Toochange hello 구독 hello 네임 스페이스를 관리할 경우 선택 **ACTIVE DIRECTORY** 왼쪽된 탐색 창의 hello와 네임 스페이스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-201">If you want toochange hello subscription or manage hello namespace, select **ACTIVE DIRECTORY** in hello left navigation pane and then select your namespace.</span></span> <span data-ttu-id="68d09-202">작업 표시줄 hello 옵션을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-202">hello task bar lists your options.</span></span>

<span data-ttu-id="68d09-203">클릭 하면 **관리** 열립니다 hello 액세스 제어 관리 포털.</span><span class="sxs-lookup"><span data-stu-id="68d09-203">Clicking **Manage** opens hello Access Control Management Portal.</span></span> <span data-ttu-id="68d09-204">Hello 액세스 제어 관리 포털에서에서 BizTalk 서비스 사용 하 여 hello **서비스 id**:</span><span class="sxs-lookup"><span data-stu-id="68d09-204">In hello Access Control Management Portal, hello BizTalk Service uses **Service identities**:</span></span>  
<span data-ttu-id="68d09-205">![Hello 액세스 제어 관리 포털의에서 ACS 서비스 Id][ACSServiceIdentities]</span><span class="sxs-lookup"><span data-stu-id="68d09-205">![ACS Service Identities in hello Access Control Management Portal][ACSServiceIdentities]</span></span>

<span data-ttu-id="68d09-206">hello 액세스 제어 서비스 id는 토큰을 수신 하 고 응용 프로그램이 나 클라이언트 tooauthenticate 액세스 제어와 함께 직접 사용할 수 있는 자격 증명의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-206">hello Access Control service identity is a set of credentials that allow applications or clients tooauthenticate directly with Access Control and receive a token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="68d09-207">hello BizTalk 서비스는 **소유자** hello 기본 서비스 id 및 hello에 대 한 **암호** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-207">hello BizTalk Service uses **Owner** for hello default service identity and hello **Password** value.</span></span> <span data-ttu-id="68d09-208">Hello 암호 값 대신 hello 대칭 키 값을 사용 하는 경우 hello 다음과 같은 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-208">If you use hello Symmetric Key value instead of hello Password value, hello following error may occur.</span></span><br/><br/><span data-ttu-id="68d09-209">*지정 된 hello로 toohello 액세스 제어 관리 서비스 계정을 연결할 수 없습니다. 자격 증명*</span><span class="sxs-lookup"><span data-stu-id="68d09-209">*Could not connect toohello Access Control Management Service account with hello specified credentials*</span></span>
> 
> 

<span data-ttu-id="68d09-210">[ACS 네임스페이스 관리](https://msdn.microsoft.com/library/azure/hh674478.aspx) 에는 일부 지침 및 권장 사항이 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-210">[Managing Your ACS Namespace](https://msdn.microsoft.com/library/azure/hh674478.aspx) lists some guidelines and recommendations.</span></span>

## <a name="requirements-explained"></a><span data-ttu-id="68d09-211">요구 사항 설명</span><span class="sxs-lookup"><span data-stu-id="68d09-211">Requirements explained</span></span>
<span data-ttu-id="68d09-212">이러한 요구 사항을 toohello 적용 되지 않는 무료 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-212">These requirements do not apply toohello Free Edition.</span></span>

<table border="1">
<tr bgcolor="FAF9F9">
        <td><span data-ttu-id="68d09-213"><strong>필요한 항목</strong></span><span class="sxs-lookup"><span data-stu-id="68d09-213"><strong>What you need</strong></span></span></td>
        <td><span data-ttu-id="68d09-214"><strong>필요한 이유</strong></span><span class="sxs-lookup"><span data-stu-id="68d09-214"><strong>Why you need it</strong></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="68d09-215">Azure 구독</span><span class="sxs-lookup"><span data-stu-id="68d09-215">Azure subscription</span></span></td>
<td><span data-ttu-id="68d09-216">hello 구독 toohello Azure 포털에에서 로그인 하려면 사용자를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-216">hello subscription determines who can sign in toohello Azure portal.</span></span> <span data-ttu-id="68d09-217">hello 계정 보유자에 hello 구독을 만듭니다 <a HREF="https://account.windowsazure.com/Subscriptions"> Azure 구독</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-217">hello Account holder creates hello subscription at <a HREF="https://account.windowsazure.com/Subscriptions"> Azure Subscriptions</a>.</span></span>
<br/><br/>
<span data-ttu-id="68d09-218">hello Azure 계정 구독이 여러 개 있을 수 있습니다 및 허용 되는 사용자가 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-218">hello Azure account can have multiple subscriptions and can be managed by anyone who is permitted.</span></span> <span data-ttu-id="68d09-219">예를 들어 Azure 계정 소유자 이라는 구독을 만들고 <em>BizTalkServiceSubscription</em> 제공 회사 내에서 BizTalk 관리자 hello 및 (예를 들어 ContosoBTSAdmins@live.com) toothis 구독에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-219">For example, your Azure account holder creates a subscription named <em>BizTalkServiceSubscription</em> and gives hello BizTalk Administrators within your company (for example, ContosoBTSAdmins@live.com) access toothis subscription.</span></span> <span data-ttu-id="68d09-220">이 시나리오에서는 hello BizTalk 관리자 toohello Azure 포털에에서 로그인 한 전체 관리자 권한 tooall hello 호스팅된 서비스의 Azure BizTalk 서비스를 포함 하 여 hello 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-220">In this scenario, hello BizTalk Administrators sign in toohello Azure portal and have full Administrator rights tooall hello hosted services in hello subscription, including Azure BizTalk Services.</span></span> <span data-ttu-id="68d09-221">hello BizTalk 관리자 hello Azure 계정 소유자에 게 없는 tooany 청구 정보에 액세스할 했으므로 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-221">hello BizTalk Administrators are not hello Azure account holders and therefore don't have access tooany billing information.</span></span>
<br/><br/><span data-ttu-id="68d09-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577">Hello Azure 포털에서에서 구독 및 저장소 계정 관리</a> 자세한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577"> Manage Subscriptions and Storage Accounts in hello Azure portal</a> provides more information.</span></span>
</td>
</tr>
<tr>
<td><span data-ttu-id="68d09-223">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="68d09-223">Azure SQL Database</span></span></td>
<td><span data-ttu-id="68d09-224">Hello 테이블, 뷰 및 hello hello 추적 데이터를 포함 하는 BizTalk 서비스에서 사용 하는 저장된 프로시저를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-224">Stores hello tables, views, and stored procedures used by hello BizTalk Service, including hello Tracking data.</span></span>
<br/><br/>
<span data-ttu-id="68d09-225">BizTalk 서비스를 만들 때 기존 Azure SQL Server, Azure SQL 데이터베이스를 사용하거나 새로운 서버 또는 데이터베이스를 자동으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-225">When you create a BizTalk Service, you can use an existing Azure SQL Server, Azure SQL Database, or automatically create a new Server or Database.</span></span>
<br/><br/>
<span data-ttu-id="68d09-226">SQL 데이터베이스의 크기 조정 hello 자동으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-226">hello SQL Database scale is automatically configured.</span></span> <span data-ttu-id="68d09-227">일반적으로 hello 기본 소수 자릿수는 BizTalk 서비스에 대 한 충분 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-227">Typically, hello default scale is sufficient for a BizTalk Service.</span></span> <span data-ttu-id="68d09-228">변경 hello 눈금 가격에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-228">Changing hello scale impacts pricing.</span></span> <span data-ttu-id="68d09-229"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930">Azure SQL Database의 계정 및 대금 청구</a>
 참조</span><span class="sxs-lookup"><span data-stu-id="68d09-229">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930"> Accounts and Billing in Azure SQL Database</a>
</span></span><br/><br/><span data-ttu-id="68d09-230">
<strong>참고</strong>
</span><span class="sxs-lookup"><span data-stu-id="68d09-230">
<strong>Notes</strong>
</span></span><br/>
<ul>
<li> <span data-ttu-id="68d09-231">새 Azure SQL Server 및 데이터베이스를 만들면 Azure 서비스가 자동으로 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-231">When you create a new Azure SQL Server and Database, Azure Services is automatically enabled.</span></span> <span data-ttu-id="68d09-232">Azure 서비스를 필요로 하는 hello BizTalk 서비스가 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-232">hello BizTalk Service requires Azure Services be enabled.</span></span></li>
<li><span data-ttu-id="68d09-233">기존 Azure SQL Server에 새 Azure SQL 데이터베이스를 만들면 hello 방화벽 규칙의 hello 서버 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-233">If you create a new Azure SQL Database on an existing Azure SQL Server, hello firewall rules of hello Server are not changed.</span></span> <span data-ttu-id="68d09-234">결과적으로, 있기 다른 Azure 서비스 액세스 toohello 서버 데이터베이스를 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-234">As a result, it's possible other Azure Services are not allowed access toohello Server's databases.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="68d09-235">Azure 액세스 제어 네임스페이스</span><span class="sxs-lookup"><span data-stu-id="68d09-235">Azure Access Control namespace</span></span></td>
<td><span data-ttu-id="68d09-236">Azure BizTalk 서비스로 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-236">Authenticates with Azure BizTalk Services.</span></span> <span data-ttu-id="68d09-237">Visual Studio에서 BizTalk 서비스를 배포할 때 이 액세스 제어 네임스페이스를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-237">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="68d09-238">BizTalk 서비스를 만들면 hello Access Control 네임 스페이스 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-238">When you create a BizTalk Service, hello Access Control namespace is automatically created.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="68d09-239">Azure Storage 계정</span><span class="sxs-lookup"><span data-stu-id="68d09-239">Azure Storage account</span></span></td>
<td><span data-ttu-id="68d09-240">제공은 tootables, blob 및 큐에 BizTalk 서비스 toosave hello 다음에서 사용 하 여 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-240">Gives access tootables, blobs, and queues used by your BizTalk Service toosave hello following:</span></span>

<ul>
<li><span data-ttu-id="68d09-241">로그 파일을 해당 모니터 hello BizTalk 서비스 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-241">Log files that monitor hello BizTalk Service.</span></span> <span data-ttu-id="68d09-242">출력을 모니터링 하는 hello hello에도 표시 됩니다 **모니터링** hello Azure 포털에서에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-242">hello monitoring output is also displayed in hello **Monitoring** tab in hello Azure portal.</span></span></li>
<li><span data-ttu-id="68d09-243">X12 또는 파트너 간에 AS2 규약을 만들 때 hello 보관 기능 toostore 메시지 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-243">When creating an X12 or AS2 agreement between partners, you can enable hello Archiving feature toostore message properties.</span></span> <span data-ttu-id="68d09-244">이 데이터는 hello 저장소 계정에에서 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-244">This data is saved in hello Storage account.</span></span></li>
</ul>
<br/>
<span data-ttu-id="68d09-245">BizTalk 서비스를 만들 때 기존 저장소 계정을 사용하거나 새 저장소 계정을 자동으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-245">When you create a BizTalk Service, you can use an existing Storage account or automatically create a new Storage account.</span></span>
<br/><br/>
<span data-ttu-id="68d09-246">BizTalk 서비스에 대 한 hello 기본 저장소 설정이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-246">hello default Storage settings are sufficient for a BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="68d09-247">저장소 계정을 만들면 기본 키와 보조 키가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-247">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="68d09-248">이러한 키는 저장소 계정 액세스 tooyour를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-248">These Keys control access tooyour Storage account.</span></span> <span data-ttu-id="68d09-249">hello BizTalk 서비스는 hello 기본 키를 자동으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-249">hello BizTalk Service automatically uses hello Primary Key.</span></span>
<br/><br/>
<span data-ttu-id="68d09-250">자세한 내용은 <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671">저장소</a>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68d09-250">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671"> Storage</a> for more information.</span></span>
</td>
</tr>

<tr>
<td><span data-ttu-id="68d09-251">SSL 개인 인증서</span><span class="sxs-lookup"><span data-stu-id="68d09-251">SSL private certificate</span></span></td>
<td>
<span data-ttu-id="68d09-252">Azure BizTalk 서비스가 만들어지면 BizTalk 서비스 이름이 포함된 HTTPS URL도 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-252">When an Azure BizTalk Service is created, an HTTPS URL that includes your BizTalk Service name is also created.</span></span> <span data-ttu-id="68d09-253">이 URL은 자동으로 구성 된 toouse 자체 서명 된 개발 전용 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-253">This URL is automatically configured toouse a self-signed development-only certificate.</span></span> <span data-ttu-id="68d09-254">프로덕션의 경우 개인 SSL 인증서가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-254">For production, you need a private SSL certificate.</span></span>
<br/><br/><span data-ttu-id="68d09-255">
<strong>중요 SSL 인증서 정보</strong>

</span><span class="sxs-lookup"><span data-stu-id="68d09-255">
<strong>Important SSL Certificate Information</strong>

</span></span><ul>
<li><span data-ttu-id="68d09-256">hello 인증서 만료 날짜가 5 년 미만인 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-256">hello certificate expiration date must be less than 5 years.</span></span></li>
<li><span data-ttu-id="68d09-257">모든 개인 인증서에는 암호가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-257">All private certificates require a password.</span></span> <span data-ttu-id="68d09-258">이 암호를 확인하고 관리자와 공유하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-258">Know this password and as a best practice, share this password with your administrators.</span></span></li>
<li><span data-ttu-id="68d09-259">자체 서명된 인증서는 테스트/개발 환경에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-259">Self-signed certificates are used in a test/development environment.</span></span> <span data-ttu-id="68d09-260">자체 서명 된 인증서를 사용할 때 hello 인증서 tooyour 개인 인증서 저장소를 가져오고 hello 신뢰할 수 있는 루트 인증 기관 인증서 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-260">When using self-signed certificates, import hello certificate tooyour Personal certificate store and hello Trusted Root Certification Authorities certificate store.</span></span></li>
</ul>
<br/><span data-ttu-id="68d09-261">Hello 프로덕션 인증서 요청 tooyour 인증 기관을 보낼 때 다음과 같은 인증서 속성 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-261">When sending hello production certificate request tooyour certification authority, give hello following certificate properties:</span></span>
<br/>

<ul>
<li><span data-ttu-id="68d09-262"><strong>확장된 키 사용</strong>: Azure BizTalk Services는 최소한 서버 인증이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-262"><strong>Enhanced Key Usage</strong>: At a minimum, Azure BizTalk Services requires Server Authentication.</span></span></li>
<li><span data-ttu-id="68d09-263"><strong>일반 이름</strong>: hello 정규화 된 도메인 이름 (FQDN) Azure BizTalk 서비스 URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-263"><strong>Common Name</strong>: Enter hello fully qualified domain name (FQDN) of your Azure BizTalk Service URL.</span></span> <span data-ttu-id="68d09-264">이 문서의 <a HREF="#CreateService">BizTalk 서비스 만들기</a>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68d09-264">See <a HREF="#CreateService">Create a BizTalk Service</a> in this article.</span></span></li>
</ul>
<br/>
<span data-ttu-id="68d09-265">Hello BizTalk 서비스가 만들어지면 새롭거나 다른 인증서를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-265">A new or different certificate can be added after hello BizTalk Service is created.</span></span>
</td>
</tr>
</table>
<!---Loc Comment: Please, check link [Create a BizTalk Service] since it is not redirecting tooany location.--->



## <a name="hybrid-connections"></a><span data-ttu-id="68d09-266">하이브리드 연결</span><span class="sxs-lookup"><span data-stu-id="68d09-266">Hybrid Connections</span></span>
<span data-ttu-id="68d09-267">Azure BizTalk 서비스를 만들 때 hello **하이브리드 연결** 탭을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-267">When you create an Azure BizTalk Service, hello **Hybrid Connections** tab is available:</span></span>

![하이브리드 연결 탭][HybridConnectionTab]

<span data-ttu-id="68d09-269">하이브리드 연결을 사용 하는 tooconnect Azure 웹 포털 또는 Azure 모바일 서비스 tooany 온-프레미스 SQL Server, MySQL, HTTP 웹 Api, 모바일 서비스 및 대부분의 사용자 지정 웹 서비스와 같은 정적 TCP 포트를 사용 하는 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-269">Hybrid Connections are used tooconnect an Azure website or Azure mobile service tooany on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, Mobile Services, and most custom Web Services.</span></span>  <span data-ttu-id="68d09-270">하이브리드 연결와 hello BizTalk 어댑터 서비스는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-270">Hybrid Connections and hello BizTalk Adapter Service are different.</span></span> <span data-ttu-id="68d09-271">hello BizTalk 어댑터 서비스는 사용 되는 tooconnect Azure BizTalk 서비스 tooan 온-프레미스 업무 (LOB) 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-271">hello BizTalk Adapter Service is used tooconnect Azure BizTalk Services tooan on-premises Line of Business (LOB) system.</span></span>

 <span data-ttu-id="68d09-272">참조 [하이브리드 연결](integration-hybrid-connection-overview.md) toolearn 더 만들기 및 관리 하이브리드 연결을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-272">See [Hybrid Connections](integration-hybrid-connection-overview.md) toolearn more, including creating and managing Hybrid Connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68d09-273">다음 단계</span><span class="sxs-lookup"><span data-stu-id="68d09-273">Next steps</span></span>
<span data-ttu-id="68d09-274">BizTalk 서비스를 만들면 했으므로 숙지 다른 hello [BizTalk 서비스: 대시보드, 모니터 및 배율 탭](biztalk-dashboard-monitor-scale-tabs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-274">Now that a BizTalk Service is created, familiarize yourself with hello different [BizTalk Services: Dashboard, Monitor and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md).</span></span> <span data-ttu-id="68d09-275">응용 프로그램에 BizTalk 서비스를 사용할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-275">Your BizTalk Service is ready for your applications.</span></span> <span data-ttu-id="68d09-276">응용 프로그램을 이동 너무 만들 toostart[Azure BizTalk 서비스](http://go.microsoft.com/fwlink/p/?LinkID=235197)합니다.</span><span class="sxs-lookup"><span data-stu-id="68d09-276">toostart creating applications, go too[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="68d09-277">참고 항목</span><span class="sxs-lookup"><span data-stu-id="68d09-277">See also</span></span>
* [<span data-ttu-id="68d09-278">BizTalk 서비스: Editions 차트</span><span class="sxs-lookup"><span data-stu-id="68d09-278">BizTalk Services: Editions Chart</span></span>](biztalk-editions-feature-chart.md)<br/>
* [<span data-ttu-id="68d09-279">BizTalk Services: 상태 차트</span><span class="sxs-lookup"><span data-stu-id="68d09-279">BizTalk Services: State Chart</span></span>](biztalk-service-state-chart.md)<br/>
* [<span data-ttu-id="68d09-280">BizTalk 서비스: 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="68d09-280">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)<br/>
* [<span data-ttu-id="68d09-281">BizTalk 서비스: 제한</span><span class="sxs-lookup"><span data-stu-id="68d09-281">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)<br/>
* [<span data-ttu-id="68d09-282">BizTalk 서비스: 발급자 이름 및 발급자 키</span><span class="sxs-lookup"><span data-stu-id="68d09-282">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)<br/>
* [<span data-ttu-id="68d09-283">Azure BizTalk 서비스 SDK를 hello 어떻게 사용 하 여 시작 합니까</span><span class="sxs-lookup"><span data-stu-id="68d09-283">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="68d09-284">VNet</span><span class="sxs-lookup"><span data-stu-id="68d09-284">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)

[NewBizTalkService]: ./media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: ./media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: ./media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: ./media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: ./media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: ./media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: ./media/biztalk-provision-services/WABS_HybridConnectionTab.png
