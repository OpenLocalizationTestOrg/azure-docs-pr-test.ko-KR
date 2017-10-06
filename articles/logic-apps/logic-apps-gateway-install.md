---
title: "Azure 논리 앱-aaaInstall 온-프레미스 데이터 게이트웨이 | Microsoft Docs"
description: "온-프레미스 데이터 원본에 액세스 하기 전에 빠른 데이터 전송 및 온-프레미스 데이터 원본과 논리 앱 간에 암호화를 위한 hello 온-프레미스 데이터 게이트웨이 설치"
keywords: "데이터에 액세스, 온-프레미스, 데이터 전송, 암호화, 데이터 원본"
services: logic-apps
documentationcenter: 
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 47e3024e-88a0-4017-8484-8f392faec89d
ms.service: logic-apps
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 01386a904d856ff545f2eca8eb1b008dcdc08574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-on-premises-data-gateway-for-azure-logic-apps"></a><span data-ttu-id="dc81e-104">Azure 논리 앱에 대 한 hello 온-프레미스 데이터 게이트웨이 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-104">Install hello on-premises data gateway for Azure Logic Apps</span></span>

<span data-ttu-id="dc81e-105">논리 앱에서 온-프레미스 데이터 원본에 액세스 하기 전에 설치 하 고 hello 온-프레미스 데이터 게이트웨이 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-105">Before your logic apps can access data sources on premises, you must install and set up hello on-premises data gateway.</span></span> <span data-ttu-id="dc81e-106">hello 게이트웨이 빠른 데이터 전송 및 온-프레미스 시스템과 논리 앱 간에 암호화를 제공 하는 브리지 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-106">hello gateway acts as a bridge that provides quick data transfer and encryption between on-premises systems and your logic apps.</span></span> <span data-ttu-id="dc81e-107">hello 게이트웨이 hello Azure 서비스 버스를 통해 암호화 된 채널에 온-프레미스 원본에서 데이터를 릴레이합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-107">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="dc81e-108">모든 트래픽이 hello 게이트웨이 에이전트의 보안 아웃 바운드 트래픽이으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-108">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="dc81e-109">에 대 한 자세한 내용은 [hello 데이터 게이트웨이가 어떻게 작동](#gateway-cloud-service)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-109">Learn more about [how hello data gateway works](#gateway-cloud-service).</span></span>

<span data-ttu-id="dc81e-110">hello 게이트웨이 온-프레미스 toothese 데이터 원본 연결을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-110">hello gateway supports connections toothese data sources on premises:</span></span>

*   <span data-ttu-id="dc81e-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="dc81e-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="dc81e-112">DB2</span><span class="sxs-lookup"><span data-stu-id="dc81e-112">DB2</span></span>  
*   <span data-ttu-id="dc81e-113">파일 시스템</span><span class="sxs-lookup"><span data-stu-id="dc81e-113">File System</span></span>
*   <span data-ttu-id="dc81e-114">Informix</span><span class="sxs-lookup"><span data-stu-id="dc81e-114">Informix</span></span>
*   <span data-ttu-id="dc81e-115">MQ</span><span class="sxs-lookup"><span data-stu-id="dc81e-115">MQ</span></span>
*   <span data-ttu-id="dc81e-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="dc81e-116">MySQL</span></span>
*   <span data-ttu-id="dc81e-117">Oracle 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="dc81e-117">Oracle Database</span></span>
*   <span data-ttu-id="dc81e-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="dc81e-118">PostgreSQL</span></span>
*   <span data-ttu-id="dc81e-119">SAP 응용 프로그램 서버</span><span class="sxs-lookup"><span data-stu-id="dc81e-119">SAP Application Server</span></span> 
*   <span data-ttu-id="dc81e-120">SAP 메시지 서버</span><span class="sxs-lookup"><span data-stu-id="dc81e-120">SAP Message Server</span></span>
*   <span data-ttu-id="dc81e-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="dc81e-121">SharePoint</span></span>
*   <span data-ttu-id="dc81e-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="dc81e-122">SQL Server</span></span>
*   <span data-ttu-id="dc81e-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="dc81e-123">Teradata</span></span>

<span data-ttu-id="dc81e-124">다음이 단계 표시 방법을 toofirst 설치 hello 온-프레미스 데이터 게이트웨이 하기 전에 [hello 게이트웨이와 논리 앱 간의 연결을 설정](./logic-apps-gateway-connection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-124">These steps show how toofirst install hello on-premises data gateway before you [set up a connection between hello gateway and your logic apps](./logic-apps-gateway-connection.md).</span></span> <span data-ttu-id="dc81e-125">지원되는 커넥터에 대한 자세한 내용은 [Azure Logic Apps용 커넥터](https://docs.microsoft.com/azure/connectors/apis-list)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dc81e-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span></span> 

<span data-ttu-id="dc81e-126">Toouse 다른 서비스와 게이트웨이 hello 하는 방법에 대 한 내용은 다음이 문서를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-126">For information about how toouse hello gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="dc81e-127">Microsoft Power BI 온-프레미스 데이터 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="dc81e-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="dc81e-128">Azure Analysis Services 온-프레미스 데이터 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="dc81e-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="dc81e-129">Microsoft Flow 온-프레미스 데이터 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="dc81e-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="dc81e-130">Microsoft PowerApps 온-프레미스 데이터 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="dc81e-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

<a name="requirements"></a>
## <a name="requirements"></a><span data-ttu-id="dc81e-131">요구 사항</span><span class="sxs-lookup"><span data-stu-id="dc81e-131">Requirements</span></span>

<span data-ttu-id="dc81e-132">**최소**:</span><span class="sxs-lookup"><span data-stu-id="dc81e-132">**Minimum**:</span></span>

* <span data-ttu-id="dc81e-133">.NET 4.5 Framework</span><span class="sxs-lookup"><span data-stu-id="dc81e-133">.NET 4.5 Framework</span></span>
* <span data-ttu-id="dc81e-134">64비트 버전의 Windows 7 또는 Windows Server 2008 R2 이상</span><span class="sxs-lookup"><span data-stu-id="dc81e-134">64-bit version of Windows 7 or Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="dc81e-135">**권장**:</span><span class="sxs-lookup"><span data-stu-id="dc81e-135">**Recommended**:</span></span>

* <span data-ttu-id="dc81e-136">8 코어 CPU</span><span class="sxs-lookup"><span data-stu-id="dc81e-136">8 Core CPU</span></span>
* <span data-ttu-id="dc81e-137">8GB 메모리</span><span class="sxs-lookup"><span data-stu-id="dc81e-137">8 GB Memory</span></span>
* <span data-ttu-id="dc81e-138">64비트 버전의 Windows 2012 R2 이상</span><span class="sxs-lookup"><span data-stu-id="dc81e-138">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="dc81e-139">**중요 고려 사항**:</span><span class="sxs-lookup"><span data-stu-id="dc81e-139">**Important considerations**:</span></span>

* <span data-ttu-id="dc81e-140">로컬 컴퓨터에만 hello 온-프레미스 데이터 게이트웨이 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-140">Install hello on-premises data gateway only on a local computer.</span></span>
<span data-ttu-id="dc81e-141">도메인 컨트롤러에 hello 게이트웨이 설치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-141">You can't install hello gateway on a domain controller.</span></span>

   > [!TIP]
   > <span data-ttu-id="dc81e-142">Hello에 tooinstall hello 게이트웨이 없는 데이터 소스와 같은 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="dc81e-142">You don't have tooinstall hello gateway on hello same computer as your data source.</span></span> <span data-ttu-id="dc81e-143">toominimize 대기 시간 hello 또는 가능한 tooyour 데이터 소스로 동일 가까운 hello 게이트웨이 설치할 수 있습니다 컴퓨터 권한이 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-143">toominimize latency, you can install hello gateway as close as possible tooyour data source, or on hello same computer, assuming that you have permissions.</span></span>

* <span data-ttu-id="dc81e-144">Hello 게이트웨이 해제, toosleep, 이동 또는 hello 게이트웨이 이러한 상황에서 실행할 수 없기 때문에 toohello 인터넷에 연결 하지 않는 컴퓨터에 설치 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="dc81e-144">Don't install hello gateway on a computer that turns off, goes toosleep, or doesn't connect toohello Internet because hello gateway can't run under those circumstances.</span></span> <span data-ttu-id="dc81e-145">또한 무선 네트워크에서는 게이트웨이 성능이 저하될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-145">Also, gateway performance might suffer over a wireless network.</span></span>

* <span data-ttu-id="dc81e-146">설치하는 동안 Microsoft 계정이 아니라 Azure Active Directory(Azure AD)에서 관리하는 [회사 또는 학교 계정](https://docs.microsoft.com/azure/active-directory/sign-up-organization)으로 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-146">During installation, you must sign in with a [work or school account](https://docs.microsoft.com/azure/active-directory/sign-up-organization) that's managed by Azure Active Directory (Azure AD), not a Microsoft account.</span></span> 

  <span data-ttu-id="dc81e-147">동일한 작업 hello 또는 학교 계정을 나중에 hello Azure toouse 있는 포털 만들고 게이트웨이 설치와 게이트웨이 리소스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-147">You have toouse hello same work or school account later in hello Azure portal when you create and associate a gateway resource with your gateway installation.</span></span> <span data-ttu-id="dc81e-148">그런 다음 프로그램 논리 앱 및 hello 온-프레미스 데이터 소스 간 hello 연결을 만들 때이 게이트웨이 리소스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-148">You then select this gateway resource when you create hello connection between your logic app and hello on-premises data source.</span></span> [<span data-ttu-id="dc81e-149">Azure AD 회사 또는 학교 계정을 사용해야 하는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="dc81e-149">Why must I use an Azure AD work or school account?</span></span>](#why-azure-work-school-account)

  > [!TIP]
  > <span data-ttu-id="dc81e-150">Office 365 서비스에 등록하고 실제 회사 전자 메일을 제공하지 않은 경우 로그인 주소는 jeff@contoso.onmicrosoft.com과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-150">If you signed up for an Office 365 offering and didn't supply your actual work email, your sign-in address might look like jeff@contoso.onmicrosoft.com.</span></span> 

* <span data-ttu-id="dc81e-151">14.16.6317.4 버전 보다 이전 하는 설치 관리자를 설정 하는 기존 게이트웨이 사용 하도록 설정한 경우 실행 중인 hello 최신 설치 관리자에서 게이트웨이 위치를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-151">If you have an existing gateway that you set up with an installer that's earlier than version 14.16.6317.4, you can't change your gateway's location by running hello latest installer.</span></span> <span data-ttu-id="dc81e-152">그러나 새 게이트웨이를 최신 설치 관리자 tooset hello 대신 원하는 hello 위치와 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-152">However, you can use hello latest installer tooset up a new gateway with hello location that you want instead.</span></span>
  
  <span data-ttu-id="dc81e-153">하지만 이전 버전 14.16.6317.4, 게이트웨이 설치 관리자 있는 게이트웨이 설치 하지 않은 경우 아직 다운로드 하 고 수 hello 최신 설치 관리자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-153">If you have a gateway installer that's earlier than version 14.16.6317.4, but you haven't installed your gateway yet, you can download and use hello latest installer.</span></span>

<a name="install-gateway"></a>

## <a name="install-hello-data-gateway"></a><span data-ttu-id="dc81e-154">Hello 데이터 게이트웨이 설치</span><span class="sxs-lookup"><span data-stu-id="dc81e-154">Install hello data gateway</span></span>

1.  <span data-ttu-id="dc81e-155">[다운로드 하 고 hello 게이트웨이 설치 관리자는 로컬 컴퓨터에서 실행](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-155">[Download and run hello gateway installer on a local computer](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span></span>

2. <span data-ttu-id="dc81e-156">검토 하 고 hello 개인정보취급방침 및 사용 약관에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-156">Review and accept hello terms of use and privacy statement.</span></span>

3. <span data-ttu-id="dc81e-157">Tooinstall hello 게이트웨이 저장할 로컬 컴퓨터의 hello 경로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-157">Specify hello path on your local computer where you want tooinstall hello gateway.</span></span>

4. <span data-ttu-id="dc81e-158">메시지가 표시되면 Microsoft 계정이 아닌 Azure 회사 또는 학교 계정을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-158">When prompted, sign in with your Azure work or school account, not a Microsoft account.</span></span>

   ![Azure 회사 또는 학교 계정으로 로그인](./media/logic-apps-gateway-install/sign-in-gateway-install.png)

5. <span data-ttu-id="dc81e-160">이제 hello로 설치 된 게이트웨이 등록 [게이트웨이 클라우드 서비스](#gateway-cloud-service)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-160">Now register your installed gateway with hello [gateway cloud service](#gateway-cloud-service).</span></span> <span data-ttu-id="dc81e-161">**이 컴퓨터에 새 게이트웨이 등록**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-161">Choose **Register a new gateway on this computer**.</span></span>

   <span data-ttu-id="dc81e-162">hello 게이트웨이 클라우드 서비스를 암호화 하 고 데이터 원본 자격 증명 및 게이트웨이 세부 정보를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-162">hello gateway cloud service encrypts and stores your data source credentials and gateway details.</span></span> 
   <span data-ttu-id="dc81e-163">또한 hello 서비스 온-프레미스 쿼리 및 논리 앱, hello 온-프레미스 데이터 게이트웨이 및 데이터 원본 간의 그 결과 라우트합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-163">hello service also routes queries and their results between your logic app, hello on-premises data gateway, and your data source on premises.</span></span>

6. <span data-ttu-id="dc81e-164">게이트웨이 설치에 대한 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-164">Provide a name for your gateway installation.</span></span> <span data-ttu-id="dc81e-165">복구 키를 만든 다음 복구 키를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-165">Create a recovery key, then confirm your recovery key.</span></span> 

   > [!IMPORTANT] 
   > <span data-ttu-id="dc81e-166">복구 키는 8자 이상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-166">Your recovery key must contain at least eight characters.</span></span> <span data-ttu-id="dc81e-167">저장 하 고 안전한 장소에 hello 키를 보관 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-167">Make sure that you save and keep hello key in a safe place.</span></span> <span data-ttu-id="dc81e-168">Toomigrate, 원하는 때이 키도 필요 복원 또는 기존 게이트웨이를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-168">You also need this key when you want toomigrate, restore, or take over an existing gateway.</span></span>

   1. <span data-ttu-id="dc81e-169">toochange hello 기본 지역 hello 게이트웨이 클라우드 서비스 및 Azure 서비스 버스 게이트웨이 설치 프로그램에서 사용 하는 선택 **변경 지역**합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-169">toochange hello default region for hello gateway cloud service and Azure Service Bus used by your gateway installation, choose **Change Region**.</span></span>

      ![지역 변경](./media/logic-apps-gateway-install/change-region-gateway-install.png)

      <span data-ttu-id="dc81e-171">hello 기본 영역이 Azure AD 테 넌 트와 연결 된 hello 영역이입니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-171">hello default region is hello region associated with your Azure AD tenant.</span></span>

   2. <span data-ttu-id="dc81e-172">Hello 다음 창에서 엽니다 hello **선택 영역** 너무 다른 지역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-172">On hello next pane, open hello **Select Region** too choose a different region.</span></span>

      ![다른 지역 선택](./media/logic-apps-gateway-install/select-region-gateway-install.png)

      <span data-ttu-id="dc81e-174">예를 들어 있습니다 수 선택 hello 논리 앱와 동일한 지역 또는 select hello 지역 가장 가까운 tooyour 온-프레미스 데이터 원본 대기 시간을 줄일 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-174">For example, you might select hello same region as your logic app, or select hello region closest tooyour on-premises data source so you can reduce latency.</span></span> <span data-ttu-id="dc81e-175">게이트웨이 리소스와 논리 앱은 서로 다른 위치에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-175">Your gateway resource and logic app can have different locations.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="dc81e-176">설치 후에 이 지역을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-176">You can't change this region after installation.</span></span> <span data-ttu-id="dc81e-177">또한이 지역 결정 하 고 게이트웨이 hello Azure 리소스를 만들 수 있는 hello 위치를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-177">This region also determines and restricts hello location where you can create hello Azure resource for your gateway.</span></span> <span data-ttu-id="dc81e-178">따라서 Azure에서 게이트웨이 리소스를 만들 때 hello 리소스 위치 게이트웨이 설치 중에 선택한 hello 영역 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-178">So when you create your gateway resource in Azure, make sure that hello resource location matches hello region that you selected during gateway installation.</span></span>
      > 
      > <span data-ttu-id="dc81e-179">원할 경우 다른 지역의 toouse 게이트웨이 나중에 새 게이트웨이 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-179">If you want toouse a different region for your gateway later, you must set up a new gateway.</span></span>

   3. <span data-ttu-id="dc81e-180">준비가 되면 **완료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-180">When you're ready, choose **Done**.</span></span>

7. <span data-ttu-id="dc81e-181">할 수 있도록 hello Azure 포털에서에서이 단계에 따라 [게이트웨이에 대 한 Azure 리소스 만들기](../logic-apps/logic-apps-gateway-connection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-181">Now follow these steps in hello Azure portal so you can [create an Azure resource for your gateway](../logic-apps/logic-apps-gateway-connection.md).</span></span> 

<span data-ttu-id="dc81e-182">에 대 한 자세한 내용은 [hello 데이터 게이트웨이가 어떻게 작동](#gateway-cloud-service)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-182">Learn more about [how hello data gateway works](#gateway-cloud-service).</span></span>

## <a name="migrate-restore-or-take-over-an-existing-gateway"></a><span data-ttu-id="dc81e-183">기존 게이트웨이 마이그레이션, 복원 또는 사용</span><span class="sxs-lookup"><span data-stu-id="dc81e-183">Migrate, restore, or take over an existing gateway</span></span>

<span data-ttu-id="dc81e-184">이러한 작업 tooperform, hello 게이트웨이 설치할 때 지정 된 hello 복구 키를 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-184">tooperform these tasks, you must have hello recovery key that was specified when hello gateway was installed.</span></span>

1. <span data-ttu-id="dc81e-185">컴퓨터의 시작 메뉴에서 **온-프레미스 데이터 게이트웨이**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-185">From your computer's Start menu, choose **On-premises data gateway**.</span></span>

2. <span data-ttu-id="dc81e-186">Hello 설치 관리자가 열립니다. 그러면 로그인에 사용한 후 hello 동일한 Azure 회사 또는 tooinstall hello 게이트웨이 사용 하는 이전 학교 계정.</span><span class="sxs-lookup"><span data-stu-id="dc81e-186">After hello installer opens, sign in with hello same Azure work or school account that was previously used tooinstall hello gateway.</span></span>

3. <span data-ttu-id="dc81e-187">**기존 게이트웨이 마이그레이션, 복원 또는 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-187">Choose **Migrate, restore, or take over an existing gateway**.</span></span>

4. <span data-ttu-id="dc81e-188">Toomigrate, 복원 또는 인수를 통해 하려는 hello 게이트웨이에 대 한 hello 이름 및 복구 키를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-188">Provide hello name and recovery key for hello gateway that you want toomigrate, restore, or take over.</span></span>

<a name="restart-gateway"></a>
## <a name="restart-hello-gateway"></a><span data-ttu-id="dc81e-189">Hello 게이트웨이 다시 시작</span><span class="sxs-lookup"><span data-stu-id="dc81e-189">Restart hello gateway</span></span>

<span data-ttu-id="dc81e-190">hello 게이트웨이 Windows 서비스로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-190">hello gateway runs as a Windows service.</span></span> <span data-ttu-id="dc81e-191">다른 Windows 서비스와 마찬가지로 시작 하 고 여러 가지 방법으로 hello 서비스를 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-191">Like any other Windows service, you can start and stop hello service in multiple ways.</span></span> <span data-ttu-id="dc81e-192">예를 들어 hello 게이트웨이 실행 하는 hello 컴퓨터에서 승격 된 권한으로 명령 프롬프트를 열고 하 고 이러한 명령 중 하나를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-192">For example, you can open a command prompt with elevated permissions on hello computer where hello gateway is running, and run either these commands:</span></span>

* <span data-ttu-id="dc81e-193">이 명령을 실행 toostop hello 서비스:</span><span class="sxs-lookup"><span data-stu-id="dc81e-193">toostop hello service, run this command:</span></span>
  
    `net stop PBIEgwService`

* <span data-ttu-id="dc81e-194">이 명령을 실행 toostart hello 서비스:</span><span class="sxs-lookup"><span data-stu-id="dc81e-194">toostart hello service, run this command:</span></span>
  
    `net start PBIEgwService`

### <a name="windows-service-account"></a><span data-ttu-id="dc81e-195">Windows 서비스 계정</span><span class="sxs-lookup"><span data-stu-id="dc81e-195">Windows service account</span></span>

<span data-ttu-id="dc81e-196">hello 온-프레미스 데이터 게이트웨이 toouse 설정 `NT SERVICE\PBIEgwService` Windows hello에 대 한 서비스 로그온 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-196">hello on-premises data gateway is set up toouse `NT SERVICE\PBIEgwService` for hello Windows service logon credentials.</span></span> <span data-ttu-id="dc81e-197">기본적으로 hello 게이트웨이 hello 컴퓨터에 대 한 "서비스로 로그온" 권한을 hello에 hello 게이트웨이 설치 하는 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-197">By default, hello gateway has hello "Log on as a service" right for hello machine where you install hello gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="dc81e-198">tooon 온-프레미스 데이터 원본에 연결 하는 데 사용 되는 hello 계정 및 Azure 작업 hello hello Windows 서비스 계정을 다른 또는 학교 계정 toocloud 서비스에서 toosign를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-198">hello Windows service account differs from hello account used for connecting tooon-premises data sources, and from hello Azure work or school account used toosign in toocloud services.</span></span>

## <a name="configure-a-firewall-or-proxy"></a><span data-ttu-id="dc81e-199">방화벽 또는 프록시 구성</span><span class="sxs-lookup"><span data-stu-id="dc81e-199">Configure a firewall or proxy</span></span>

<span data-ttu-id="dc81e-200">hello 게이트웨이 아웃 바운드 연결을 너무 만듭니다 [Azure 서비스 버스](https://azure.microsoft.com/services/service-bus/)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-200">hello gateway creates an outbound connection too [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="dc81e-201">사용자 게이트웨이에 대 한 프록시 정보 tooprovide 참조 [프록시 설정 구성](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-201">tooprovide proxy information for your gateway, see [Configure proxy settings](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span></span>

<span data-ttu-id="dc81e-202">toocheck 방화벽 또는 프록시 연결을 차단할 수 있는지 여부를 확인 컴퓨터 실제로 toohello를 연결할 수 있는지 여부를 인터넷 및 hello [Azure 서비스 버스](https://azure.microsoft.com/services/service-bus/)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-202">toocheck whether your firewall, or proxy, might block connections, confirm whether your machine can actually connect toohello internet and hello [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="dc81e-203">PowerShell 창에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-203">From a PowerShell prompt, run this command:</span></span>

`Test-NetConnection -ComputerName watchdog.servicebus.windows.net -Port 9350`

> [!NOTE]
> <span data-ttu-id="dc81e-204">이 명령은 네트워크 연결 및 연결 toohello Azure 서비스 버스에만 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-204">This command only tests network connectivity and connectivity toohello Azure Service Bus.</span></span> <span data-ttu-id="dc81e-205">Hello 명령 할당 되지 않은 하므로 toodo hello 게이트웨이 또는 hello 게이트웨이 클라우드 서비스를 암호화 하 고 자격 증명 및 게이트웨이 세부 정보를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-205">So hello command doesn't have anything toodo with hello gateway or hello gateway cloud service that encrypts and stores your credentials and gateway details.</span></span> 
>
> <span data-ttu-id="dc81e-206">또한 이 명령은 Windows Server 2012 R2 이상 및 Windows 8.1 이상에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-206">Also, this command is only available on Windows Server 2012 R2 or later, and Windows 8.1 or later.</span></span> <span data-ttu-id="dc81e-207">텔넷 이전 운영 체제 버전에서 사용할 수 있습니다 너무 연결을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-207">On earlier OS versions, you can use Telnet too test connectivity.</span></span> <span data-ttu-id="dc81e-208">[Azure Service Bus 및 하이브리드 솔루션](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-208">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

<span data-ttu-id="dc81e-209">결과는 비슷한 예는 toothis 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-209">Your results should look similar toothis example:</span></span>

```text
ComputerName           : watchdog.servicebus.windows.net
RemoteAddress          : 70.37.104.240
RemotePort             : 5672
InterfaceAlias         : vEthernet (Broadcom NetXtreme Gigabit Ethernet - Virtual Switch)
SourceAddress          : 10.120.60.105
PingSucceeded          : False
PingReplyDetails (RTT) : 0 ms
TcpTestSucceeded       : True
```

<span data-ttu-id="dc81e-210">경우 **TcpTestSucceeded** 너무 설정 하지 않으면**True**, 방화벽으로 차단 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-210">If **TcpTestSucceeded** is not set too**True**, you might be blocked by a firewall.</span></span> <span data-ttu-id="dc81e-211">Toobe를 포괄적인 원하는 경우 대체 hello **ComputerName** 및 **포트** 아래 나열 된 값과 hello 값 [포트 구성](#configure-ports) 이 항목의 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-211">If you want toobe comprehensive, substitute hello **ComputerName** and **Port** values with hello values listed under [Configure ports](#configure-ports) in this topic.</span></span>

<span data-ttu-id="dc81e-212">hello 방화벽 연결 Azure 서비스 버스 toohello Azure 데이터 센터를 사용 하면 해당 hello를 차단도 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-212">hello firewall might also block connections that hello Azure Service Bus makes toohello Azure datacenters.</span></span> <span data-ttu-id="dc81e-213">이 시나리오에서 상황이 발생 하는 경우 승인 (차단 해제) 모든 hello 해당 지역에서 해당 데이터 센터에 대 한 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-213">If this scenario happens, approve (unblock) all hello IP addresses for those datacenters in your region.</span></span> <span data-ttu-id="dc81e-214">이러한 IP 주소에 대 한 [get hello Azure IP 주소 목록 여기](https://www.microsoft.com/download/details.aspx?id=41653)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-214">For those IP addresses, [get hello Azure IP addresses list here](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

## <a name="configure-ports"></a><span data-ttu-id="dc81e-215">포트 구성</span><span class="sxs-lookup"><span data-stu-id="dc81e-215">Configure ports</span></span>

<span data-ttu-id="dc81e-216">hello 게이트웨이 아웃 바운드 연결을 너무 만듭니다[Azure 서비스 버스](https://azure.microsoft.com/services/service-bus/) 아웃 바운드 포트는 통신: TCP 443 (기본값), 5671, 5672, 9350 9354 통해.</span><span class="sxs-lookup"><span data-stu-id="dc81e-216">hello gateway creates an outbound connection too[Azure Service Bus](https://azure.microsoft.com/services/service-bus/) and communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span> <span data-ttu-id="dc81e-217">hello 게이트웨이 인바운드 포트가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-217">hello gateway doesn't require inbound ports.</span></span> <span data-ttu-id="dc81e-218">[Azure Service Bus 및 하이브리드 솔루션](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-218">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

| <span data-ttu-id="dc81e-219">도메인 이름</span><span class="sxs-lookup"><span data-stu-id="dc81e-219">DOMAIN NAMES</span></span> | <span data-ttu-id="dc81e-220">아웃바운드 포트</span><span class="sxs-lookup"><span data-stu-id="dc81e-220">OUTBOUND PORTS</span></span> | <span data-ttu-id="dc81e-221">설명</span><span class="sxs-lookup"><span data-stu-id="dc81e-221">DESCRIPTION</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dc81e-222">*.analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="dc81e-222">*.analysis.windows.net</span></span> | <span data-ttu-id="dc81e-223">443</span><span class="sxs-lookup"><span data-stu-id="dc81e-223">443</span></span> | <span data-ttu-id="dc81e-224">HTTPS</span><span class="sxs-lookup"><span data-stu-id="dc81e-224">HTTPS</span></span> | 
| <span data-ttu-id="dc81e-225">*.login.windows.net</span><span class="sxs-lookup"><span data-stu-id="dc81e-225">*.login.windows.net</span></span> | <span data-ttu-id="dc81e-226">443</span><span class="sxs-lookup"><span data-stu-id="dc81e-226">443</span></span> | <span data-ttu-id="dc81e-227">HTTPS</span><span class="sxs-lookup"><span data-stu-id="dc81e-227">HTTPS</span></span> | 
| <span data-ttu-id="dc81e-228">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="dc81e-228">*.servicebus.windows.net</span></span> | <span data-ttu-id="dc81e-229">5671-5672</span><span class="sxs-lookup"><span data-stu-id="dc81e-229">5671-5672</span></span> | <span data-ttu-id="dc81e-230">AMQP(고급 메시지 큐 프로토콜)</span><span class="sxs-lookup"><span data-stu-id="dc81e-230">Advanced Message Queuing Protocol (AMQP)</span></span> | 
| <span data-ttu-id="dc81e-231">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="dc81e-231">*.servicebus.windows.net</span></span> | <span data-ttu-id="dc81e-232">443, 9350-9354</span><span class="sxs-lookup"><span data-stu-id="dc81e-232">443, 9350-9354</span></span> | <span data-ttu-id="dc81e-233">TCP의 서비스 버스 릴레이에 대한 수신기(액세스 제어 토큰 획득에 443 필요)</span><span class="sxs-lookup"><span data-stu-id="dc81e-233">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> | 
| <span data-ttu-id="dc81e-234">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="dc81e-234">*.frontend.clouddatahub.net</span></span> | <span data-ttu-id="dc81e-235">443</span><span class="sxs-lookup"><span data-stu-id="dc81e-235">443</span></span> | <span data-ttu-id="dc81e-236">HTTPS</span><span class="sxs-lookup"><span data-stu-id="dc81e-236">HTTPS</span></span> | 
| <span data-ttu-id="dc81e-237">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="dc81e-237">*.core.windows.net</span></span> | <span data-ttu-id="dc81e-238">443</span><span class="sxs-lookup"><span data-stu-id="dc81e-238">443</span></span> | <span data-ttu-id="dc81e-239">HTTPS</span><span class="sxs-lookup"><span data-stu-id="dc81e-239">HTTPS</span></span> | 
| <span data-ttu-id="dc81e-240">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="dc81e-240">login.microsoftonline.com</span></span> | <span data-ttu-id="dc81e-241">443</span><span class="sxs-lookup"><span data-stu-id="dc81e-241">443</span></span> | <span data-ttu-id="dc81e-242">HTTPS</span><span class="sxs-lookup"><span data-stu-id="dc81e-242">HTTPS</span></span> | 
| <span data-ttu-id="dc81e-243">*.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="dc81e-243">*.msftncsi.com</span></span> | <span data-ttu-id="dc81e-244">443</span><span class="sxs-lookup"><span data-stu-id="dc81e-244">443</span></span> | <span data-ttu-id="dc81e-245">Hello 게이트웨이 hello Power BI 서비스에 연결할 수 없는 경우 tootest 인터넷 연결을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-245">Used tootest internet connectivity when hello gateway is unreachable by hello Power BI service.</span></span> | 

<span data-ttu-id="dc81e-246">다운로드 하 고 hello를 사용 하 여 수 hello 도메인 대신 tooapprove IP 주소를 설정한 경우 [Microsoft Azure 데이터 센터 IP 범위 목록을](https://www.microsoft.com/download/details.aspx?id=41653)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-246">If you have tooapprove IP addresses instead of hello domains, you can download and use hello [Microsoft Azure Datacenter IP ranges list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="dc81e-247">경우에 따라 hello Azure 서비스 버스 연결은 정규화 된 도메인 이름이 아닌 IP 주소와 함께 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-247">In some cases, hello Azure Service Bus connections are made with IP Address rather than fully qualified domain names.</span></span>

<a name="gateway-cloud-service"></a>
## <a name="how-does-hello-data-gateway-work"></a><span data-ttu-id="dc81e-248">Hello 데이터 게이트웨이 어떻게 작동 합니까?</span><span class="sxs-lookup"><span data-stu-id="dc81e-248">How does hello data gateway work?</span></span>

<span data-ttu-id="dc81e-249">hello 데이터 게이트웨이 논리 앱, hello 게이트웨이 클라우드 서비스 및 온-프레미스 데이터 원본 간의 신속 하 고 보안 통신을 용이 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-249">hello data gateway facilitates quick and secure communication between your logic app, hello gateway cloud service, and your on-premises data source.</span></span> 

![diagram-for-on-premises-data-gateway-flow](./media/logic-apps-gateway-install/how-on-premises-data-gateway-works-flow-diagram.png)

<span data-ttu-id="dc81e-251">따라서 hello 클라우드에서 hello 사용자 tooyour 연결 된 요소와 상호 작용 하는 경우 온-프레미스 데이터 원본:</span><span class="sxs-lookup"><span data-stu-id="dc81e-251">So when hello user in hello cloud interacts with an element that's connected tooyour on-premises data source:</span></span>

1. <span data-ttu-id="dc81e-252">hello 게이트웨이 클라우드 서비스 hello 데이터 원본에 대 한 암호화 hello 자격 증명과 함께 쿼리를 만들고 게이트웨이 tooprocess hello에 대 한 hello 쿼리 toohello 큐를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-252">hello gateway cloud service creates a query, along with hello encrypted credentials for hello data source, and sends hello query toohello queue for hello gateway tooprocess.</span></span>

2. <span data-ttu-id="dc81e-253">hello 게이트웨이 클라우드 서비스 hello 쿼리를 분석 하 고 hello 요청 toohello Azure 서비스 버스를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-253">hello gateway cloud service analyzes hello query and pushes hello request toohello Azure Service Bus.</span></span>

3. <span data-ttu-id="dc81e-254">hello 온-프레미스 데이터 게이트웨이 보류 중인 요청 hello에 대 한 Azure 서비스 버스를 폴링합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-254">hello on-premises data gateway polls hello Azure Service Bus for pending requests.</span></span>

4. <span data-ttu-id="dc81e-255">hello 쿼리 가져오고 hello 자격 증명의 암호를 해독 toohello 데이터 원본 자격 증명으로 연결 하는 hello 게이트웨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-255">hello gateway gets hello query, decrypts hello credentials, and connects toohello data source with those credentials.</span></span>

5. <span data-ttu-id="dc81e-256">hello 게이트웨이 hello 쿼리 toohello 실행할 데이터 소스에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-256">hello gateway sends hello query toohello data source for execution.</span></span>

6. <span data-ttu-id="dc81e-257">hello 결과 hello 데이터 원본, 백 toohello 게이트웨이 및 toohello 게이트웨이 클라우드 서비스에서 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-257">hello results are sent from hello data source, back toohello gateway, and then toohello gateway cloud service.</span></span> <span data-ttu-id="dc81e-258">hello 게이트웨이 클라우드 서비스 사용 하 여 hello 결과.</span><span class="sxs-lookup"><span data-stu-id="dc81e-258">hello gateway cloud service then uses hello results.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="dc81e-259">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="dc81e-259">Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="dc81e-260">일반</span><span class="sxs-lookup"><span data-stu-id="dc81e-260">General</span></span>

<span data-ttu-id="dc81e-261">**Q:**: hello 클라우드에서 SQL Azure와 같은 데이터 원본에는 게이트웨이 필요 한가요?</span><span class="sxs-lookup"><span data-stu-id="dc81e-261">**Q**: Do I need a gateway for data sources in hello cloud, such as SQL Azure?</span></span> <br/><span data-ttu-id="dc81e-262">
**A**: 아니요.</span><span class="sxs-lookup"><span data-stu-id="dc81e-262">
**A**: No.</span></span> <span data-ttu-id="dc81e-263">게이트웨이는 tooon 온-프레미스 데이터 원본만 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-263">A gateway connects tooon-premises data sources only.</span></span>

<span data-ttu-id="dc81e-264">**Q:**: hello 게이트웨이 toobe hello hello 데이터 원본으로 동일한 컴퓨터에 설치 되어 있습니까?</span><span class="sxs-lookup"><span data-stu-id="dc81e-264">**Q**: Does hello gateway have toobe installed on hello same machine as hello data source?</span></span> <br/><span data-ttu-id="dc81e-265">
**A**: 아니요.</span><span class="sxs-lookup"><span data-stu-id="dc81e-265">
**A**: No.</span></span> <span data-ttu-id="dc81e-266">hello 게이트웨이 제공 된 hello 연결 정보를 사용 하 여 toohello 데이터 소스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-266">hello gateway connects toohello data source using hello connection information that was provided.</span></span> <span data-ttu-id="dc81e-267">이런이 의미에서 클라이언트 응용 프로그램으로 hello 게이트웨이 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-267">Consider hello gateway as a client application in this sense.</span></span> <span data-ttu-id="dc81e-268">hello 게이트웨이 hello 기능 tooconnect toohello 서버 이름을 제공 하는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-268">hello gateway just needs hello capability tooconnect toohello server name that was provided.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="dc81e-269">**Q:**: 이유 해야 합니까는 Azure 회사 또는 학교 사용에 대 한 계정 toosign?</span><span class="sxs-lookup"><span data-stu-id="dc81e-269">**Q**: Why must I use an Azure work or school account toosign in?</span></span> <br/><span data-ttu-id="dc81e-270">
**A**: Azure 작업을 사용 하 여 또는 학교 계정을 hello 온-프레미스 데이터 게이트웨이 설치할 때만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-270">
**A**: You can only use an Azure work or school account when you install hello on-premises data gateway.</span></span> <span data-ttu-id="dc81e-271">로그인 계정은 Azure AD(Azure Active Directory)에서 관리하는 테넌트에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-271">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="dc81e-272">일반적으로 Azure AD 계정의 사용자 계정 이름 (UPN)는 hello 전자 메일 주소와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-272">Usually, your Azure AD account's user principal name (UPN) matches hello email address.</span></span>

<span data-ttu-id="dc81e-273">**Q**: 자격 증명은 어디에 저장되나요?</span><span class="sxs-lookup"><span data-stu-id="dc81e-273">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="dc81e-274">
**A**: hello 입력 한 자격 증명이 데이터 원본에 대 한 암호화 및 hello 게이트웨이 클라우드 서비스에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-274">
**A**: hello credentials that you enter for a data source are encrypted and stored in hello gateway cloud service.</span></span> <span data-ttu-id="dc81e-275">hello 온-프레미스 데이터 게이트웨이에 hello 자격 증명의 암호가 해독 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-275">hello credentials are decrypted at hello on-premises data gateway.</span></span>

<span data-ttu-id="dc81e-276">**Q**: 네트워크 대역폭에 대한 요구 사항이 있나요?</span><span class="sxs-lookup"><span data-stu-id="dc81e-276">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="dc81e-277">
**A**: 네트워크 연결의 처리량이 높은 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-277">
**A**: We recommend that your network connection has good throughput.</span></span> <span data-ttu-id="dc81e-278">모든 환경은 다름와 전송 중인 데이터 양을 hello hello 결과 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-278">Every environment is different, and hello amount of data being sent affects hello results.</span></span> <span data-ttu-id="dc81e-279">ExpressRoute를 사용 하 여 온-프레미스 및 hello Azure 데이터 센터 간 처리량의 수준을 tooguarantee를 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-279">Using ExpressRoute could help tooguarantee a level of throughput between on-premises and hello Azure datacenters.</span></span>
<span data-ttu-id="dc81e-280">처리량 hello 타사 도구 Azure 속도 테스트 앱 toohelp 계기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-280">You can use hello third-party tool Azure Speed Test app toohelp gauge your throughput.</span></span>

<span data-ttu-id="dc81e-281">**Q:**: hello 게이트웨이에서 실행 중인 쿼리 tooa 데이터 원본에 대 한 hello 대기 시간 이란?</span><span class="sxs-lookup"><span data-stu-id="dc81e-281">**Q**: What is hello latency for running queries tooa data source from hello gateway?</span></span> <span data-ttu-id="dc81e-282">Hello 최상의 아키텍처는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="dc81e-282">What is hello best architecture?</span></span> <br/><span data-ttu-id="dc81e-283">
**A**: tooreduce 네트워크 대기 시간, 가능한 데이터 원본 닫기 toohello로 hello 게이트웨이 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-283">
**A**: tooreduce network latency, install hello gateway as close toohello data source as possible.</span></span> <span data-ttu-id="dc81e-284">Hello 실제 데이터 원본에 hello 게이트웨이 설치할 수 있습니다,이 근접 단어는 발생 하는 hello 대기 시간을 최소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-284">If you can install hello gateway on hello actual data source, this proximity minimizes hello latency introduced.</span></span> <span data-ttu-id="dc81e-285">너무 hello 데이터 센터를 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-285">Consider hello datacenters too.</span></span> <span data-ttu-id="dc81e-286">예를 들어 해당 서비스는 hello 미국 서 부 데이터 센터를 사용 하는 경우 Azure VM에서 호스팅되는 SQL Server 있으면 Azure VM에에서 있어야 hello West US 너무 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-286">For example, if your service uses hello West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in hello West US too.</span></span> <span data-ttu-id="dc81e-287">이 근접 대기 시간을 최소화 하 고 hello Azure VM에서 송신 요금을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-287">This proximity minimizes latency and avoids egress charges on hello Azure VM.</span></span>

<span data-ttu-id="dc81e-288">**Q:**: 보낸 결과 백 toohello 클라우드 인가요?</span><span class="sxs-lookup"><span data-stu-id="dc81e-288">**Q**: How are results sent back toohello cloud?</span></span> <br/><span data-ttu-id="dc81e-289">
**A**: 결과 hello Azure 서비스 버스를 통해 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-289">
**A**: Results are sent through hello Azure Service Bus.</span></span>

<span data-ttu-id="dc81e-290">**Q:**: hello 클라우드에서 한 인바운드 연결 toohello 게이트웨이가 있습니까?</span><span class="sxs-lookup"><span data-stu-id="dc81e-290">**Q**: Are there any inbound connections toohello gateway from hello cloud?</span></span> <br/><span data-ttu-id="dc81e-291">
**A**: 아니요.</span><span class="sxs-lookup"><span data-stu-id="dc81e-291">
**A**: No.</span></span> <span data-ttu-id="dc81e-292">hello 게이트웨이 아웃 바운드 연결 tooAzure 서비스 버스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-292">hello gateway uses outbound connections tooAzure Service Bus.</span></span>

<span data-ttu-id="dc81e-293">**Q**: 아웃바운드 연결을 차단하면 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="dc81e-293">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="dc81e-294">수행할 작업 tooopen 필요 합니까?</span><span class="sxs-lookup"><span data-stu-id="dc81e-294">What do I need tooopen?</span></span> <br/><span data-ttu-id="dc81e-295">
**A**: hello 포트 및 호스트 게이트웨이 사용 하 여 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="dc81e-295">
**A**: See hello ports and hosts that hello gateway uses.</span></span>

<span data-ttu-id="dc81e-296">**Q:**: hello 실제 Windows 서비스 섞어?</span><span class="sxs-lookup"><span data-stu-id="dc81e-296">**Q**: What is hello actual Windows service called?</span></span><br/><span data-ttu-id="dc81e-297">
**A**: hello 게이트웨이 서비스에서 Power BI 엔터프라이즈 게이트웨이 서비스를 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-297">
**A**: In Services, hello gateway is called Power BI Enterprise Gateway Service.</span></span>

<span data-ttu-id="dc81e-298">**Q:**: Azure Active Directory 계정으로 실행 하는 게이트웨이 Windows 서비스 hello 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="dc81e-298">**Q**: Can hello gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="dc81e-299">
**A**: 아니요.</span><span class="sxs-lookup"><span data-stu-id="dc81e-299">
**A**: No.</span></span> <span data-ttu-id="dc81e-300">hello Windows 서비스에는 유효한 Windows 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-300">hello Windows service must have a valid Windows account.</span></span> <span data-ttu-id="dc81e-301">기본적으로 hello 서비스는 NT SERVICE\PBIEgwService hello 서비스 SID로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-301">By default, hello service runs with hello Service SID, NT SERVICE\PBIEgwService.</span></span>

### <a name="high-availability-and-disaster-recovery"></a><span data-ttu-id="dc81e-302">고가용성 및 재해 복구</span><span class="sxs-lookup"><span data-stu-id="dc81e-302">High availability and disaster recovery</span></span>

<span data-ttu-id="dc81e-303">**Q**: 재해 복구를 위해 어떤 옵션을 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="dc81e-303">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="dc81e-304">
**A**: hello 복구 키 toorestore 사용 하거나 게이트웨이 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-304">
**A**: You can use hello recovery key toorestore or move a gateway.</span></span> <span data-ttu-id="dc81e-305">Hello 게이트웨이 설치할 때 hello 복구 키를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-305">When you install hello gateway, specify hello recovery key.</span></span>

<span data-ttu-id="dc81e-306">**Q:**: hello 복구 키의 hello 이점은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="dc81e-306">**Q**: What is hello benefit of hello recovery key?</span></span> <br/><span data-ttu-id="dc81e-307">
**A**: hello 복구 키 방식으로 toomigrate 제공 하거나 재해가 발생 한 후 게이트웨이 설정을 복구 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-307">
**A**: hello recovery key provides a way toomigrate or recover your gateway settings after a disaster.</span></span>

<span data-ttu-id="dc81e-308">**Q:**: hello 게이트웨이와 함께 고가용성 시나리오를 사용 하기 위한 계획이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="dc81e-308">**Q**: Are there any plans for enabling high availability scenarios with hello gateway?</span></span> <br/><span data-ttu-id="dc81e-309">
**A**: hello 로드맵에 이러한 시나리오는 했지만 아직 시간대가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-309">
**A**: These scenarios are on hello roadmap, but we don't have a timeline yet.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="dc81e-310">문제 해결</span><span class="sxs-lookup"><span data-stu-id="dc81e-310">Troubleshooting</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

<span data-ttu-id="dc81e-311">**Q:**: 어떻게 하는 쿼리를 보내는 toohello 온-프레미스 데이터 원본을 볼 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="dc81e-311">**Q**: How can I see what queries are being sent toohello on-premises data source?</span></span> <br/><span data-ttu-id="dc81e-312">
**A**: hello 전송 된 쿼리를 포함 하는 쿼리 추적을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-312">
**A**: You can enable query tracing, which includes hello queries that are sent.</span></span> <span data-ttu-id="dc81e-313">Toochange 쿼리 문제 해결를 수행할 때 toohello 원래 값을 추적 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-313">Remember toochange query tracing back toohello original value when done troubleshooting.</span></span> <span data-ttu-id="dc81e-314">쿼리 추적 기능을 그대로 두면 큰 로그가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-314">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="dc81e-315">또한 추적 쿼리를 위해 데이터 원본이 포함하는 도구를 살펴볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-315">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="dc81e-316">예를 들어 SQL Server 및 Analysis Services의 경우 확장 이벤트 또는 SQL 프로파일러를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-316">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="dc81e-317">**Q:**: hello 게이트웨이 로그는 어디에 있습니까?</span><span class="sxs-lookup"><span data-stu-id="dc81e-317">**Q**: Where are hello gateway logs?</span></span> <br/><span data-ttu-id="dc81e-318">
**A**: 이 항목 뒷부분에 나오는 도구를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dc81e-318">
**A**: See Tools later in this topic.</span></span>

### <a name="update-toohello-latest-version"></a><span data-ttu-id="dc81e-319">Toohello 최신 버전을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-319">Update toohello latest version</span></span>

<span data-ttu-id="dc81e-320">Hello 게이트웨이 버전이 오래 되 면 많은 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-320">Many issues can surface when hello gateway version becomes outdated.</span></span> <span data-ttu-id="dc81e-321">좋은 일반 사례로 hello 최신 버전을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-321">As good general practice, make sure that you use hello latest version.</span></span> <span data-ttu-id="dc81e-322">한 달 이상 hello 게이트웨이 업데이트 하지 않은 경우 hello 최신 버전의 hello 게이트웨이 설치 하는 것이 좋습니다. 수도 있으며 hello 문제를 재현할 수 있는지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-322">If you haven't updated hello gateway for a month or longer, you might consider installing hello latest version of hello gateway, and see if you can reproduce hello issue.</span></span>

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="dc81e-323">오류: tooadd 사용자 toogroup을 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-323">Error: Failed tooadd user toogroup.</span></span> <span data-ttu-id="dc81e-324">(-2147463168 PBIEgwService 성능 로그 사용자)</span><span class="sxs-lookup"><span data-stu-id="dc81e-324">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="dc81e-325">지원 되지 않는 도메인 컨트롤러에 tooinstall hello 게이트웨이 시도 하면이 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-325">You might get this error if you try tooinstall hello gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="dc81e-326">도메인 컨트롤러가 아닌 컴퓨터에 hello 게이트웨이 배포 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-326">Make sure that you deploy hello gateway on a machine that isn't a domain controller.</span></span>

## <a name="tools"></a><span data-ttu-id="dc81e-327">도구</span><span class="sxs-lookup"><span data-stu-id="dc81e-327">Tools</span></span>

### <a name="collect-logs-from-hello-gateway-configurer"></a><span data-ttu-id="dc81e-328">Hello 게이트웨이 configurer에서 로그를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-328">Collect logs from hello gateway configurer</span></span>

<span data-ttu-id="dc81e-329">Hello 게이트웨이에 대 한 여러 로그를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-329">You can collect several logs for hello gateway.</span></span> <span data-ttu-id="dc81e-330">항상 hello 로그를 시작!</span><span class="sxs-lookup"><span data-stu-id="dc81e-330">Always start with hello logs!</span></span>

#### <a name="installer-logs"></a><span data-ttu-id="dc81e-331">설치 관리자 로그</span><span class="sxs-lookup"><span data-stu-id="dc81e-331">Installer logs</span></span>

`%localappdata%\Temp\Power_BI_Gateway_–Enterprise.log`

#### <a name="configuration-logs"></a><span data-ttu-id="dc81e-332">구성 로그</span><span class="sxs-lookup"><span data-stu-id="dc81e-332">Configuration logs</span></span>

`%localappdata%\Microsoft\Power BI Enterprise Gateway\GatewayConfigurator.log`

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="dc81e-333">엔터프라이즈 게이트웨이 서비스 로그</span><span class="sxs-lookup"><span data-stu-id="dc81e-333">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\Power BI Enterprise Gateway\EnterpriseGateway.log`

#### <a name="event-logs"></a><span data-ttu-id="dc81e-334">이벤트 로그</span><span class="sxs-lookup"><span data-stu-id="dc81e-334">Event logs</span></span>

<span data-ttu-id="dc81e-335">데이터 관리 게이트웨이 및 PowerBIGateway 로그 hello를 찾을 수 있습니다 **응용 프로그램 및 서비스 로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-335">You can find hello Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>

### <a name="fiddler-trace"></a><span data-ttu-id="dc81e-336">Fiddler 추적</span><span class="sxs-lookup"><span data-stu-id="dc81e-336">Fiddler Trace</span></span>

<span data-ttu-id="dc81e-337">[Fiddler](http://www.telerik.com/fiddler) 는 HTTP 트래픽을 모니터링하는 Telerik의 무료 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-337">[Fiddler](http://www.telerik.com/fiddler) is a free tool from Telerik that monitors HTTP traffic.</span></span> <span data-ttu-id="dc81e-338">Hello hello 클라이언트 컴퓨터에서 Power BI 서비스를 사용 하 여이 트래픽을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-338">You can see this traffic with hello Power BI service from hello client machine.</span></span> <span data-ttu-id="dc81e-339">이 서비스는 오류 및 기타 관련된 정보를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc81e-339">This service might show errors and other related information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc81e-340">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dc81e-340">Next steps</span></span>
    
* [<span data-ttu-id="dc81e-341">논리 앱에서 tooon 온-프레미스 데이터 연결</span><span class="sxs-lookup"><span data-stu-id="dc81e-341">Connect tooon-premises data from logic apps</span></span>](../logic-apps/logic-apps-gateway-connection.md)
* [<span data-ttu-id="dc81e-342">엔터프라이즈 통합 기능</span><span class="sxs-lookup"><span data-stu-id="dc81e-342">Enterprise integration features</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="dc81e-343">Azure Logic Apps용 커넥터</span><span class="sxs-lookup"><span data-stu-id="dc81e-343">Connectors for Azure Logic Apps</span></span>](../connectors/apis-list.md)
