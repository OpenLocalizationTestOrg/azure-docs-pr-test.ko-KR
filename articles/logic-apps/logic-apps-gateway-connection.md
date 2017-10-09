---
title: "Azure 논리 앱에 대 한 온-프레미스에서 데이터 원본을 aaaAccess | Microsoft Docs"
description: "논리 앱에서 온-프레미스 데이터 원본에 액세스할 수 있도록 hello 온-프레미스 데이터 게이트웨이를 설정합니다"
keywords: "데이터에 액세스, 온-프레미스, 데이터 전송, 암호화, 데이터 원본"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 6cb4449d-e6b8-4c35-9862-15110ae73e6a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 1d3deaac5a095316ce78e224dab0c08559bc2ff2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="access-data-sources-on-premises-from-logic-apps-with-hello-on-premises-data-gateway"></a><span data-ttu-id="9c963-104">온-프레미스 hello 온-프레미스 데이터 게이트웨이 사용 하 여 논리 앱에서 데이터 원본 액세스</span><span class="sxs-lookup"><span data-stu-id="9c963-104">Access data sources on premises from logic apps with hello on-premises data gateway</span></span>

<span data-ttu-id="9c963-105">논리 앱에서 온-프레미스에서 데이터 원본을 tooaccess 논리 앱 지원 되는 커넥터와 함께 사용할 수 있는 온-프레미스 데이터 게이트웨이를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-105">tooaccess data sources on premises from your logic apps, set up an on-premises data gateway that logic apps can use with supported connectors.</span></span> <span data-ttu-id="9c963-106">hello 게이트웨이 빠른 데이터 전송 및 온-프레미스 데이터 원본과 논리 앱 간에 암호화를 제공 하는 브리지 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-106">hello gateway acts as a bridge that provides quick data transfer and encryption between data sources on premises and your logic apps.</span></span> <span data-ttu-id="9c963-107">hello 게이트웨이 hello Azure 서비스 버스를 통해 암호화 된 채널에 온-프레미스 원본에서 데이터를 릴레이합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-107">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="9c963-108">모든 트래픽이 hello 게이트웨이 에이전트의 보안 아웃 바운드 트래픽이으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-108">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="9c963-109">에 대 한 자세한 내용은 [hello 데이터 게이트웨이가 어떻게 작동](logic-apps-gateway-install.md#gateway-cloud-service)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-109">Learn more about [how hello data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span> 

<span data-ttu-id="9c963-110">hello 게이트웨이 온-프레미스 toothese 데이터 원본 연결을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-110">hello gateway supports connections toothese data sources on premises:</span></span>

*   <span data-ttu-id="9c963-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="9c963-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="9c963-112">DB2</span><span class="sxs-lookup"><span data-stu-id="9c963-112">DB2</span></span>  
*   <span data-ttu-id="9c963-113">파일 시스템</span><span class="sxs-lookup"><span data-stu-id="9c963-113">File System</span></span>
*   <span data-ttu-id="9c963-114">Informix</span><span class="sxs-lookup"><span data-stu-id="9c963-114">Informix</span></span>
*   <span data-ttu-id="9c963-115">MQ</span><span class="sxs-lookup"><span data-stu-id="9c963-115">MQ</span></span>
*   <span data-ttu-id="9c963-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="9c963-116">MySQL</span></span>
*   <span data-ttu-id="9c963-117">Oracle 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="9c963-117">Oracle Database</span></span>
*   <span data-ttu-id="9c963-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="9c963-118">PostgreSQL</span></span>
*   <span data-ttu-id="9c963-119">SAP 응용 프로그램 서버</span><span class="sxs-lookup"><span data-stu-id="9c963-119">SAP Application Server</span></span> 
*   <span data-ttu-id="9c963-120">SAP 메시지 서버</span><span class="sxs-lookup"><span data-stu-id="9c963-120">SAP Message Server</span></span>
*   <span data-ttu-id="9c963-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="9c963-121">SharePoint</span></span>
*   <span data-ttu-id="9c963-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="9c963-122">SQL Server</span></span>
*   <span data-ttu-id="9c963-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="9c963-123">Teradata</span></span>

<span data-ttu-id="9c963-124">이러한 단계는 어떻게 tooset hello 온-프레미스 데이터 게이트웨이 toowork 논리 앱을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-124">These steps show how tooset up hello on-premises data gateway toowork with your logic apps.</span></span> <span data-ttu-id="9c963-125">지원되는 커넥터에 대한 자세한 내용은 [Azure Logic Apps용 커넥터](../connectors/apis-list.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9c963-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](../connectors/apis-list.md).</span></span> 

<span data-ttu-id="9c963-126">Toouse 다른 서비스와 게이트웨이 hello 하는 방법에 대 한 내용은 다음이 문서를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-126">For information about how toouse hello gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="9c963-127">Microsoft Power BI 온-프레미스 데이터 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="9c963-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="9c963-128">Azure Analysis Services 온-프레미스 데이터 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="9c963-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="9c963-129">Microsoft Flow 온-프레미스 데이터 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="9c963-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="9c963-130">Microsoft PowerApps 온-프레미스 데이터 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="9c963-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a><span data-ttu-id="9c963-131">요구 사항</span><span class="sxs-lookup"><span data-stu-id="9c963-131">Requirements</span></span>

* <span data-ttu-id="9c963-132">이미 있어야 [hello 데이터 게이트웨이 로컬 컴퓨터에 설치](logic-apps-gateway-install.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-132">You must have already [installed hello data gateway on a local computer](logic-apps-gateway-install.md).</span></span>

* <span data-ttu-id="9c963-133">동일한 작업 hello 또는 학교 계정을 사용한 너무 toouse 있는 toohello Azure 포털에에서 로그인 할 때[hello 온-프레미스 데이터 게이트웨이 설치](logic-apps-gateway-install.md#requirements)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-133">When you sign in toohello Azure portal, you have toouse hello same work or school account that was used too[install hello on-premises data gateway](logic-apps-gateway-install.md#requirements).</span></span> <span data-ttu-id="9c963-134">사용자 로그인 계정에 게이트웨이 설치에 대 한 hello Azure 포털에서에서 게이트웨이 리소스를 만들 때 Azure 구독 toouse가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-134">Your sign-in account must also have an Azure subscription toouse when you create a gateway resource in hello Azure portal for your gateway installation.</span></span>

* <span data-ttu-id="9c963-135">게이트웨이 설치는 Azure 게이트웨이 리소스에서 이미 요구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-135">Your gateway installation can't already be claimed by an Azure gateway resource.</span></span> <span data-ttu-id="9c963-136">게이트웨이 설치 tooonly 하나의 Azure 게이트웨이 리소스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-136">You can associate your gateway installation tooonly one Azure gateway resource.</span></span> <span data-ttu-id="9c963-137">클레임은 hello 설치를 다른 리소스에 대 한 사용할 수 있도록 hello 게이트웨이 리소스를 만들 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-137">Claim happens when you create hello gateway resource so that hello installation is unavailable for other resources.</span></span>

## <a name="set-up-hello-data-gateway-connection"></a><span data-ttu-id="9c963-138">Hello 데이터 게이트웨이 연결을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-138">Set up hello data gateway connection</span></span>

### <a name="1-install-hello-on-premises-data-gateway"></a><span data-ttu-id="9c963-139">1. Hello 온-프레미스 데이터 게이트웨이 설치</span><span class="sxs-lookup"><span data-stu-id="9c963-139">1. Install hello on-premises data gateway</span></span>

<span data-ttu-id="9c963-140">아직 하지 않는 경우 따라 hello [단계 tooinstall hello 온-프레미스 데이터 게이트웨이](logic-apps-gateway-install.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-140">If you haven't already, follow hello [steps tooinstall hello on-premises data gateway](logic-apps-gateway-install.md).</span></span> <span data-ttu-id="9c963-141">Hello로 계속 하기 전에 다른 단계 hello 데이터 게이트웨이 로컬 컴퓨터에 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-141">Before you continue with hello other steps, make sure that you installed hello data gateway on a local computer.</span></span>

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-hello-on-premises-data-gateway"></a><span data-ttu-id="9c963-142">2. Hello 온-프레미스 데이터 게이트웨이에 대 한 Azure 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="9c963-142">2. Create an Azure resource for hello on-premises data gateway</span></span>

<span data-ttu-id="9c963-143">로컬 컴퓨터에 hello 게이트웨이 설치한 후 Azure에 리소스로 데이터 게이트웨이 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-143">After you install hello gateway on a local computer, you must create your data gateway as a resource in Azure.</span></span> <span data-ttu-id="9c963-144">또한 이 단계는 Azure 구독과 게이트웨이 리소스를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-144">This step also associates your gateway resource with your Azure subscription.</span></span>

1. <span data-ttu-id="9c963-145">Toohello 로그인 [Azure 포털](https://portal.azure.com "Azure 포털")합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-145">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="9c963-146">Toouse hello 동일한 Azure 회사 또는 학교 전자 메일 주소 사용 tooinstall hello 게이트웨이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-146">Make sure toouse hello same Azure work or school email address used tooinstall hello gateway.</span></span>

2. <span data-ttu-id="9c963-147">Azure의 hello 왼쪽된 메뉴에서 선택 **새로** > **엔터프라이즈 통합** > **온-프레미스 데이터 게이트웨이** 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-147">On hello left menu in Azure, choose **New** > **Enterprise Integration** > **On-premises data gateway** as shown here:</span></span>

   !["온-프레미스 데이터 게이트웨이" 찾기](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. <span data-ttu-id="9c963-149">Hello에 **연결 게이트웨이 만들기** 블레이드에서 이러한 세부 정보 toocreate 데이터 게이트웨이 리소스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-149">On hello **Create connection gateway** blade, provide these details toocreate your data gateway resource:</span></span>

    * <span data-ttu-id="9c963-150">**이름**: 게이트웨이 리소스의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-150">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="9c963-151">**구독**: 선택 hello 게이트웨이 리소스와 Azure 구독 tooassociate 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-151">**Subscription**: Select hello Azure subscription tooassociate with your gateway resource.</span></span> 
    <span data-ttu-id="9c963-152">이 구독 해야 hello 논리 앱과 동일한 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-152">This subscription should be hello same subscription as your logic app.</span></span>
   
      <span data-ttu-id="9c963-153">hello 기본 구독 hello toosign에 사용한 Azure 계정 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-153">hello default subscription is based on hello Azure account that you used toosign in.</span></span>

    * <span data-ttu-id="9c963-154">**리소스 그룹**: 게이트웨이 리소스를 배포하기 위해 리소스 그룹을 만들거나 기존 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-154">**Resource group**: Create a resource group or select an existing resource group for deploying your gateway resource.</span></span> 
    <span data-ttu-id="9c963-155">리소스 그룹을 통해 관련된 Azure 자산을 컬렉션으로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-155">Resource groups help you manage related Azure assets as a collection.</span></span>

    * <span data-ttu-id="9c963-156">**위치**: Azure 위치 toohello이를 제한 하는 동안 hello 게이트웨이 클라우드 서비스에 대해 선택 된 동일한 지역 [게이트웨이 설치](logic-apps-gateway-install.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-156">**Location**: Azure restricts this location toohello same region that was selected for hello gateway cloud service during [gateway installation](logic-apps-gateway-install.md).</span></span> 

      > [!NOTE]
      > <span data-ttu-id="9c963-157">Hello 게이트웨이 리소스 위치 hello 게이트웨이 클라우드 서비스 위치와 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-157">Make sure that hello gateway resource location matches hello gateway cloud service location.</span></span> <span data-ttu-id="9c963-158">그렇지 않은 경우 게이트웨이 설치 나타나지 않을 tooselect 있습니다 설치 하는 hello 게이트웨이 목록에 hello 다음 단계에서.</span><span class="sxs-lookup"><span data-stu-id="9c963-158">Otherwise, your gateway installation might not appear in hello installed gateways list for you tooselect in hello next step.</span></span>
      > 
      > <span data-ttu-id="9c963-159">게이트웨이 리소스 및 논리 앱에 서로 다른 지역을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-159">You can use different regions for your gateway resource and for your logic app.</span></span>

    * <span data-ttu-id="9c963-160">**설치 이름**: 게이트웨이 설치 선택 되어 있지 않으면 이전에 설치한 hello 게이트웨이 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-160">**Installation Name**: If your gateway installation isn't already selected, select hello gateway that you previously installed.</span></span> 

    <span data-ttu-id="9c963-161">tooadd hello 게이트웨이 리소스 tooyour Azure 대시보드를 선택 **Pin toodashboard**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-161">tooadd hello gateway resource tooyour Azure dashboard, choose **Pin toodashboard**.</span></span> 
    <span data-ttu-id="9c963-162">작업을 완료하면 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-162">When you're done, choose **Create**.</span></span>

    <span data-ttu-id="9c963-163">예:</span><span class="sxs-lookup"><span data-stu-id="9c963-163">For example:</span></span>

    ![온-프레미스 데이터 게이트웨이 toocreate 세부 정보를 제공 합니다.](./media/logic-apps-gateway-connection/createblade.png)

    <span data-ttu-id="9c963-165">hello 주요 Azure 왼쪽된 메뉴에서 언제 든 지 데이터 게이트웨이 너무 이동 toofind 또는 보기 **더 서비스** > **엔터프라이즈 통합** > **온-프레미스 데이터 게이트웨이**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-165">toofind or view your data gateway at any time,  from hello main Azure left menu, go too  **More Services** > **Enterprise Integration** > **On-premises Data Gateways**.</span></span>

    ![너무 이동 "더 많은 서비스", "엔터프라이즈 통합", "온-프레미스 데이터 게이트웨이"](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-toohello-on-premises-data-gateway"></a><span data-ttu-id="9c963-167">3. 논리 앱 toohello 온-프레미스 데이터 게이트웨이 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-167">3. Connect your logic app toohello on-premises data gateway</span></span>

<span data-ttu-id="9c963-168">데이터 게이트웨이 리소스를 생성 하 고 Azure 구독에 연결 된 해당 리소스 한 논리 앱 및 hello 데이터 게이트웨이 간의 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-168">Now that you've created your data gateway resource and associated your Azure subscription with that resource, create a connection between your logic app and hello data gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="9c963-169">게이트웨이 연결 위치에에서 존재 해야 hello 동일 지역 있지만 논리 앱으로 다른 지역에 존재 하는 데이터 게이트웨이 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-169">Your gateway connection location must exist in hello same region as your logic app, but you can use a data gateway that exists in a different region.</span></span>

1. <span data-ttu-id="9c963-170">Hello Azure 포털에서에서 만들거나 논리가 응용 프로그램 디자이너에서 논리 앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-170">In hello Azure portal, create or open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="9c963-171">온-프레미스 연결을 지원하는 SQL Server와 같은 커넥터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-171">Add a connector that supports on-premises connections, like SQL Server.</span></span>

3. <span data-ttu-id="9c963-172">선택 표시 된 hello 순서에 따라 **온-프레미스 데이터 게이트웨이 통해 연결**, 고유 연결 이름을 제공 하 고 필요한 정보를 hello 하 고 toouse 원하는 hello 데이터 게이트웨이 리소스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-172">Following hello order shown, select **Connect via on-premises data gateway**, provide a unique connection name and hello required information, and select hello data gateway resource that you want toouse.</span></span> <span data-ttu-id="9c963-173">작업을 완료하면 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-173">When you're done, choose **Create**.</span></span>

   > [!TIP]
   > <span data-ttu-id="9c963-174">고유한 연결 이름을 통해 나중에, 특히 여러 연결을 만들 때 해당 연결을 쉽게 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-174">A unique connection name helps you easily identify that connection later, especially when you create multiple connections.</span></span> <span data-ttu-id="9c963-175">해당 하는 경우 hello 정규화 된 도메인에서 사용자 이름을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-175">If applicable, also include hello qualified domain for your username.</span></span> 

   ![논리 앱과 데이터 게이트웨이 간에 연결 만들기](./media/logic-apps-gateway-connection/blankconnection.png)

<span data-ttu-id="9c963-177">축, 한 게이트웨이 연결 논리 앱 toouse 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-177">Congratulations, your gateway connection is now ready for your logic app toouse.</span></span>

## <a name="edit-your-gateway-connection-settings"></a><span data-ttu-id="9c963-178">게이트웨이 연결 설정 편집</span><span class="sxs-lookup"><span data-stu-id="9c963-178">Edit your gateway connection settings</span></span>

<span data-ttu-id="9c963-179">논리 앱에 대 한 게이트웨이 연결을 만든 후에 해당 특정 연결에 대 한 toolater 업데이트 hello 설정을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-179">After you create a gateway connection for your logic app, you might want toolater update hello settings for that specific connection.</span></span>

1. <span data-ttu-id="9c963-180">toofind hello 게이트웨이 연결:</span><span class="sxs-lookup"><span data-stu-id="9c963-180">toofind hello gateway connection:</span></span>

   * <span data-ttu-id="9c963-181">Hello 논리 앱 블레이드에서 아래 **개발 도구**선택, **API 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-181">On hello logic app blade, under **Development Tools**, select **API Connections**.</span></span> 
   
     <span data-ttu-id="9c963-182">hello **API 연결** 게이트웨이 연결을 포함 하 여 논리 앱과 연결 된 모든 API 연결 창에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-182">hello **API Connections** pane shows all API connections associated with your logic app, including gateway connections.</span></span>

     ![이동 tooyour 논리 앱을 "연결 API" 선택](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * <span data-ttu-id="9c963-184">Hello 주요 Azure 왼쪽된 메뉴에서 이동할 너무 또는 **더 서비스** > **웹 및 모바일 서비스** > **API 연결** 모든 API 연결에 대 한 Azure 구독과 연결 된 포함 하 여 게이트웨이 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-184">Or, from hello main Azure left menu, go too **More Services** > **Web & Mobile Services** > **API Connections** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span> 

   * <span data-ttu-id="9c963-185">Hello 주 Azure 왼쪽 메뉴에서 너무를 이동 또는**모든 리소스** 모든 API 연결에 대 한 Azure 구독과 연결 된 게이트웨이 연결을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-185">Or, on hello main Azure left menu, go too**All resources** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span>

2. <span data-ttu-id="9c963-186">Tooview 또는 편집을 선택 하는 hello 게이트웨이 연결을 선택 **편집 API 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-186">Select hello gateway connection that you want tooview or edit, and choose **Edit API connection**.</span></span>

   > [!TIP]
   > <span data-ttu-id="9c963-187">업데이트가 적용 되지 않습니다, 그래도 [hello 게이트웨이 Windows 서비스를 다시 시작 및 중지](./logic-apps-gateway-install.md#restart-gateway)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-187">If your updates don't take effect, try [stopping and restarting hello gateway Windows service](./logic-apps-gateway-install.md#restart-gateway).</span></span>

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a><span data-ttu-id="9c963-188">온-프레미스 데이터 게이트웨이 리소스 전환 또는 삭제</span><span class="sxs-lookup"><span data-stu-id="9c963-188">Switch or delete your on-premises data gateway resource</span></span>

<span data-ttu-id="9c963-189">toocreate 다른 게이트웨이 리소스를 다른 리소스와 게이트웨이 연결 하거나 hello 게이트웨이 리소스를 제거, hello 게이트웨이 설치에 영향을 주지 않고 hello 게이트웨이 리소스를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-189">toocreate a different gateway resource, associate your gateway with a different resource, or remove hello gateway resource, you can delete hello gateway resource without affecting hello gateway installation.</span></span> 

1. <span data-ttu-id="9c963-190">Hello 주요 Azure 왼쪽된 메뉴에서 이동할 너무**모든 리소스**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-190">From hello main Azure left menu, go too**All resources**.</span></span> 
2. <span data-ttu-id="9c963-191">데이터 게이트웨이 리소스를 찾아 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-191">Find and select your data gateway resource.</span></span>
3. <span data-ttu-id="9c963-192">선택 **온-프레미스 데이터 게이트웨이**, hello 리소스 도구 모음에서 선택 하 고 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c963-192">Choose **On-premises Data Gateway**, and on hello resource toolbar, choose **Delete**.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="9c963-193">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="9c963-193">Frequently asked questions</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a><span data-ttu-id="9c963-194">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9c963-194">Next steps</span></span>

* [<span data-ttu-id="9c963-195">논리 앱 보안</span><span class="sxs-lookup"><span data-stu-id="9c963-195">Secure your logic apps</span></span>](./logic-apps-securing-a-logic-app.md)
* [<span data-ttu-id="9c963-196">논리 앱에 대한 일반적인 예제 및 시나리오</span><span class="sxs-lookup"><span data-stu-id="9c963-196">Common examples and scenarios for logic apps</span></span>](./logic-apps-examples-and-scenarios.md)
