---
title: "Azure Logic Apps용 온-프레미스 데이터 원본에 액세스 | Microsoft Docs"
description: "논리 앱에서 온-프레미스 데이터 원본에 액세스할 수 있도록 온-프레미스 데이터 게이트웨이를 설정합니다."
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
ms.openlocfilehash: 24793b83ca284fe9510fe21bc2d13b0589209d36
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="access-data-sources-on-premises-from-logic-apps-with-the-on-premises-data-gateway"></a><span data-ttu-id="39758-104">온-프레미스 데이터 게이트웨이를 사용하여 논리 앱에서 온-프레미스 데이터 원본에 액세스</span><span class="sxs-lookup"><span data-stu-id="39758-104">Access data sources on premises from logic apps with the on-premises data gateway</span></span>

<span data-ttu-id="39758-105">논리 앱에서 온-프레미스 데이터 원본에 액세스하려면 지원되는 커넥터와 함께 논리 앱을 사용할 수 있는 온-프레미스 데이터 게이트웨이를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-105">To access data sources on premises from your logic apps, set up an on-premises data gateway that logic apps can use with supported connectors.</span></span> <span data-ttu-id="39758-106">게이트웨이는 온-프레미스 데이터 원본과 논리 앱 간에 빠른 데이터 전송 및 암호화를 제공하는 브리지 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-106">The gateway acts as a bridge that provides quick data transfer and encryption between data sources on premises and your logic apps.</span></span> <span data-ttu-id="39758-107">게이트웨이는 Azure Service Bus를 통해 암호화된 채널의 온-프레미스 원본에서 데이터를 릴레이합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-107">The gateway relays data from on-premises sources on encrypted channels through the Azure Service Bus.</span></span> <span data-ttu-id="39758-108">보안으로 시작하는 모든 트래픽은 게이트웨이 에이전트에서 트래픽을 아웃바운드합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-108">All traffic originates as secure outbound traffic from the gateway agent.</span></span> <span data-ttu-id="39758-109">[데이터 게이트웨이 작동 원리](logic-apps-gateway-install.md#gateway-cloud-service)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="39758-109">Learn more about [how the data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span> 

<span data-ttu-id="39758-110">게이트웨이는 다음과 같이 온-프레미스 데이터 원본에 대한 연결을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-110">The gateway supports connections to these data sources on premises:</span></span>

*   <span data-ttu-id="39758-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="39758-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="39758-112">DB2</span><span class="sxs-lookup"><span data-stu-id="39758-112">DB2</span></span>  
*   <span data-ttu-id="39758-113">파일 시스템</span><span class="sxs-lookup"><span data-stu-id="39758-113">File System</span></span>
*   <span data-ttu-id="39758-114">Informix</span><span class="sxs-lookup"><span data-stu-id="39758-114">Informix</span></span>
*   <span data-ttu-id="39758-115">MQ</span><span class="sxs-lookup"><span data-stu-id="39758-115">MQ</span></span>
*   <span data-ttu-id="39758-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="39758-116">MySQL</span></span>
*   <span data-ttu-id="39758-117">Oracle 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="39758-117">Oracle Database</span></span>
*   <span data-ttu-id="39758-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="39758-118">PostgreSQL</span></span>
*   <span data-ttu-id="39758-119">SAP 응용 프로그램 서버</span><span class="sxs-lookup"><span data-stu-id="39758-119">SAP Application Server</span></span> 
*   <span data-ttu-id="39758-120">SAP 메시지 서버</span><span class="sxs-lookup"><span data-stu-id="39758-120">SAP Message Server</span></span>
*   <span data-ttu-id="39758-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="39758-121">SharePoint</span></span>
*   <span data-ttu-id="39758-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="39758-122">SQL Server</span></span>
*   <span data-ttu-id="39758-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="39758-123">Teradata</span></span>

<span data-ttu-id="39758-124">이러한 단계에서는 논리 앱에서 작동하도록 온-프레미스 데이터 게이트웨이를 설정하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="39758-124">These steps show how to set up the on-premises data gateway to work with your logic apps.</span></span> <span data-ttu-id="39758-125">지원되는 커넥터에 대한 자세한 내용은 [Azure Logic Apps용 커넥터](../connectors/apis-list.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39758-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](../connectors/apis-list.md).</span></span> 

<span data-ttu-id="39758-126">다른 서비스에서 게이트웨이를 사용하는 방법에 대한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39758-126">For information about how to use the gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="39758-127">Microsoft Power BI 온-프레미스 데이터 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="39758-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="39758-128">Azure Analysis Services 온-프레미스 데이터 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="39758-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="39758-129">Microsoft Flow 온-프레미스 데이터 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="39758-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="39758-130">Microsoft PowerApps 온-프레미스 데이터 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="39758-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a><span data-ttu-id="39758-131">요구 사항</span><span class="sxs-lookup"><span data-stu-id="39758-131">Requirements</span></span>

* <span data-ttu-id="39758-132">[데이터 게이트웨이가 로컬 컴퓨터에 설치](logic-apps-gateway-install.md)되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-132">You must have already [installed the data gateway on a local computer](logic-apps-gateway-install.md).</span></span>

* <span data-ttu-id="39758-133">Azure Portal에 로그인할 때 [온-프레미스 데이터 게이트웨이를 설치](logic-apps-gateway-install.md#requirements)하는 데 사용된 것과 동일한 회사 또는 학교 계정을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-133">When you sign in to the Azure portal, you have to use the same work or school account that was used to [install the on-premises data gateway](logic-apps-gateway-install.md#requirements).</span></span> <span data-ttu-id="39758-134">또한 Azure Portal에서 게이트웨이 설치를 위해 게이트웨이 리소스를 만들 때 사용할 Azure 구독이 로그인 계정에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-134">Your sign-in account must also have an Azure subscription to use when you create a gateway resource in the Azure portal for your gateway installation.</span></span>

* <span data-ttu-id="39758-135">게이트웨이 설치는 Azure 게이트웨이 리소스에서 이미 요구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="39758-135">Your gateway installation can't already be claimed by an Azure gateway resource.</span></span> <span data-ttu-id="39758-136">하나의 게이트웨이 리소스에만 게이트웨이 설치를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39758-136">You can associate your gateway installation to only one Azure gateway resource.</span></span> <span data-ttu-id="39758-137">클레임은 게이트웨이 리소스를 만들 때 발생하므로 다른 리소스에서 설치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="39758-137">Claim happens when you create the gateway resource so that the installation is unavailable for other resources.</span></span>

## <a name="set-up-the-data-gateway-connection"></a><span data-ttu-id="39758-138">데이터 게이트웨이 연결 설정</span><span class="sxs-lookup"><span data-stu-id="39758-138">Set up the data gateway connection</span></span>

### <a name="1-install-the-on-premises-data-gateway"></a><span data-ttu-id="39758-139">1. 온-프레미스 데이터 게이트웨이 설치</span><span class="sxs-lookup"><span data-stu-id="39758-139">1. Install the on-premises data gateway</span></span>

<span data-ttu-id="39758-140">아직 수행하지 않은 경우 [온-프레미스 데이터 게이트웨이를 설치하는 단계](logic-apps-gateway-install.md)에 따르세요.</span><span class="sxs-lookup"><span data-stu-id="39758-140">If you haven't already, follow the [steps to install the on-premises data gateway](logic-apps-gateway-install.md).</span></span> <span data-ttu-id="39758-141">다른 단계를 계속하기 전에 로컬 컴퓨터에 데이터 게이트웨이를 설치했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-141">Before you continue with the other steps, make sure that you installed the data gateway on a local computer.</span></span>

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-the-on-premises-data-gateway"></a><span data-ttu-id="39758-142">2. 온-프레미스 데이터 게이트웨이에 Azure 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="39758-142">2. Create an Azure resource for the on-premises data gateway</span></span>

<span data-ttu-id="39758-143">로컬 컴퓨터에 게이트웨이를 설치한 후에 Azure에서 리소스인 데이터 게이트웨이를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-143">After you install the gateway on a local computer, you must create your data gateway as a resource in Azure.</span></span> <span data-ttu-id="39758-144">또한 이 단계는 Azure 구독과 게이트웨이 리소스를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-144">This step also associates your gateway resource with your Azure subscription.</span></span>

1. <span data-ttu-id="39758-145">[Azure Portal](https://portal.azure.com "Azure Portal")에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-145">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="39758-146">게이트웨이를 설치하는 데 동일한 Azure 회사 또는 학교 이메일 주소를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-146">Make sure to use the same Azure work or school email address used to install the gateway.</span></span>

2. <span data-ttu-id="39758-147">Azure의 왼쪽 메뉴에서 다음과 같이 **새로 만들기** > **엔터프라이즈 통합** > **온-프레미스 데이터 게이트웨이**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-147">On the left menu in Azure, choose **New** > **Enterprise Integration** > **On-premises data gateway** as shown here:</span></span>

   !["온-프레미스 데이터 게이트웨이" 찾기](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. <span data-ttu-id="39758-149">**연결 게이트웨이 만들기** 블레이드에서 데이터 게이트웨이 리소스를 만들기 위해 이러한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-149">On the **Create connection gateway** blade, provide these details to create your data gateway resource:</span></span>

    * <span data-ttu-id="39758-150">**이름**: 게이트웨이 리소스의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-150">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="39758-151">**구독**: 게이트웨이 리소스와 연결할 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-151">**Subscription**: Select the Azure subscription to associate with your gateway resource.</span></span> 
    <span data-ttu-id="39758-152">이 구독은 논리 앱과 동일한 구독이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-152">This subscription should be the same subscription as your logic app.</span></span>
   
      <span data-ttu-id="39758-153">기본 구독은 로그인하는 데 사용한 Azure 계정을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-153">The default subscription is based on the Azure account that you used to sign in.</span></span>

    * <span data-ttu-id="39758-154">**리소스 그룹**: 게이트웨이 리소스를 배포하기 위해 리소스 그룹을 만들거나 기존 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-154">**Resource group**: Create a resource group or select an existing resource group for deploying your gateway resource.</span></span> 
    <span data-ttu-id="39758-155">리소스 그룹을 통해 관련된 Azure 자산을 컬렉션으로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39758-155">Resource groups help you manage related Azure assets as a collection.</span></span>

    * <span data-ttu-id="39758-156">**위치**: Azure에서는 이 위치를 [게이트웨이 설치](logic-apps-gateway-install.md) 중에 게이트웨이 클라우드 서비스에 대해 선택한 동일한 지역으로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-156">**Location**: Azure restricts this location to the same region that was selected for the gateway cloud service during [gateway installation](logic-apps-gateway-install.md).</span></span> 

      > [!NOTE]
      > <span data-ttu-id="39758-157">게이트웨이 리소스 위치가 게이트웨이 클라우드 서비스 위치와 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-157">Make sure that the gateway resource location matches the gateway cloud service location.</span></span> <span data-ttu-id="39758-158">그렇지 않은 경우 게이트웨이 설치는 다음 단계에서 선택하도록 설치된 게이트웨이 목록에 나타나지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39758-158">Otherwise, your gateway installation might not appear in the installed gateways list for you to select in the next step.</span></span>
      > 
      > <span data-ttu-id="39758-159">게이트웨이 리소스 및 논리 앱에 서로 다른 지역을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39758-159">You can use different regions for your gateway resource and for your logic app.</span></span>

    * <span data-ttu-id="39758-160">**설치 이름**: 게이트웨이 설치가 선택되어 있지 않으면 이전에 설치한 게이트웨이를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-160">**Installation Name**: If your gateway installation isn't already selected, select the gateway that you previously installed.</span></span> 

    <span data-ttu-id="39758-161">게이트웨이 리소스를 Azure 대시보드에 추가하려면 **대시보드에 고정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-161">To add the gateway resource to your Azure dashboard, choose **Pin to dashboard**.</span></span> 
    <span data-ttu-id="39758-162">작업을 완료하면 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-162">When you're done, choose **Create**.</span></span>

    <span data-ttu-id="39758-163">예:</span><span class="sxs-lookup"><span data-stu-id="39758-163">For example:</span></span>

    ![온-프레미스 데이터 게이트웨이를 만들기 위해 세부 정보 제공](./media/logic-apps-gateway-connection/createblade.png)

    <span data-ttu-id="39758-165">기본 Azure 왼쪽 메뉴에서 언제든지 데이터 게이트웨이를 찾아 보려면 **추가 서비스** > **엔터프라이즈 통합** > **온-프레미스 데이터 게이트웨이**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-165">To find or view your data gateway at any time,  from the main Azure left menu, go to  **More Services** > **Enterprise Integration** > **On-premises Data Gateways**.</span></span>

    !["추가 서비스", "엔터프라이즈 통합", "온-프레미스 데이터 게이트웨이"로 이동](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-to-the-on-premises-data-gateway"></a><span data-ttu-id="39758-167">3. 온-프레미스 데이터 게이트웨이에 논리 앱 연결</span><span class="sxs-lookup"><span data-stu-id="39758-167">3. Connect your logic app to the on-premises data gateway</span></span>

<span data-ttu-id="39758-168">이제 데이터 게이트웨이 리소스를 만들고 해당 리소스와 Azure 구독을 연결했으므로 논리 앱과 데이터 게이트웨이 간을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-168">Now that you've created your data gateway resource and associated your Azure subscription with that resource, create a connection between your logic app and the data gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="39758-169">게이트웨이 연결 위치는 논리 앱과 동일한 지역에 있어야 하지만 다른 지역에 있는 데이터 게이트웨이를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39758-169">Your gateway connection location must exist in the same region as your logic app, but you can use a data gateway that exists in a different region.</span></span>

1. <span data-ttu-id="39758-170">Azure Portal의 논리 앱 디자이너에서 논리 앱을 만들거나 엽니다.</span><span class="sxs-lookup"><span data-stu-id="39758-170">In the Azure portal, create or open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="39758-171">온-프레미스 연결을 지원하는 SQL Server와 같은 커넥터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-171">Add a connector that supports on-premises connections, like SQL Server.</span></span>

3. <span data-ttu-id="39758-172">표시된 순서에 따라 **온-프레미스 데이터 게이트웨이를 통한 연결**을 선택하고 고유한 연결 이름 및 필수 정보를 제공하고 사용하려는 데이터 게이트웨이 리소스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-172">Following the order shown, select **Connect via on-premises data gateway**, provide a unique connection name and the required information, and select the data gateway resource that you want to use.</span></span> <span data-ttu-id="39758-173">작업을 완료하면 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-173">When you're done, choose **Create**.</span></span>

   > [!TIP]
   > <span data-ttu-id="39758-174">고유한 연결 이름을 통해 나중에, 특히 여러 연결을 만들 때 해당 연결을 쉽게 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39758-174">A unique connection name helps you easily identify that connection later, especially when you create multiple connections.</span></span> <span data-ttu-id="39758-175">해당하는 경우 사용자 이름의 정규화된 도메인도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="39758-175">If applicable, also include the qualified domain for your username.</span></span> 

   ![논리 앱과 데이터 게이트웨이 간에 연결 만들기](./media/logic-apps-gateway-connection/blankconnection.png)

<span data-ttu-id="39758-177">축하합니다. 게이트웨이 연결에 논리 앱을 사용할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="39758-177">Congratulations, your gateway connection is now ready for your logic app to use.</span></span>

## <a name="edit-your-gateway-connection-settings"></a><span data-ttu-id="39758-178">게이트웨이 연결 설정 편집</span><span class="sxs-lookup"><span data-stu-id="39758-178">Edit your gateway connection settings</span></span>

<span data-ttu-id="39758-179">논리 앱에 게이트웨이를 연결한 후에 나중에 해당 특정 연결에 대한 설정을 업데이트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="39758-179">After you create a gateway connection for your logic app, you might want to later update the settings for that specific connection.</span></span>

1. <span data-ttu-id="39758-180">게이트웨이 연결을 찾으려면:</span><span class="sxs-lookup"><span data-stu-id="39758-180">To find the gateway connection:</span></span>

   * <span data-ttu-id="39758-181">논리 앱 블레이드의 **개발 도구** 아래에서 **API 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-181">On the logic app blade, under **Development Tools**, select **API Connections**.</span></span> 
   
     <span data-ttu-id="39758-182">**API 연결** 창에서는 게이트웨이 연결을 포함하여 논리 앱과 관련된 모든 API 연결을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="39758-182">The **API Connections** pane shows all API connections associated with your logic app, including gateway connections.</span></span>

     ![논리 앱으로 이동, "API 연결" 선택](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * <span data-ttu-id="39758-184">또는 기본 Azure 왼쪽 메뉴에서 Azure 구독과 연결된 게이트웨이 연결을 비롯한 모든 API 연결에 대해 **추가 서비스** > **웹 및 Mobile Services** > **API 연결**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-184">Or, from the main Azure left menu, go to **More Services** > **Web & Mobile Services** > **API Connections** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span> 

   * <span data-ttu-id="39758-185">또는 기본 Azure 왼쪽 메뉴에서 Azure 구독과 연관된 게이트웨이 연결을 비롯한 모든 API 연결에 대해 **모든 리소스**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-185">Or, on the main Azure left menu, go to **All resources** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span>

2. <span data-ttu-id="39758-186">**API 연결 편집**을 보거나 편집 및 선택하려는 게이트웨이 연결을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-186">Select the gateway connection that you want to view or edit, and choose **Edit API connection**.</span></span>

   > [!TIP]
   > <span data-ttu-id="39758-187">업데이트가 적용되지 않더라도 [게이트웨이 Windows 서비스를 중지 및 다시 시작](./logic-apps-gateway-install.md#restart-gateway)합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-187">If your updates don't take effect, try [stopping and restarting the gateway Windows service](./logic-apps-gateway-install.md#restart-gateway).</span></span>

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a><span data-ttu-id="39758-188">온-프레미스 데이터 게이트웨이 리소스 전환 또는 삭제</span><span class="sxs-lookup"><span data-stu-id="39758-188">Switch or delete your on-premises data gateway resource</span></span>

<span data-ttu-id="39758-189">다른 게이트웨이 리소스를 만들거나 다른 리소스와 게이트웨이를 연결하거나 게이트웨이 리소스를 제거하려면 게이트웨이 설치에 영향을 주지 않고 게이트웨이 리소스를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39758-189">To create a different gateway resource, associate your gateway with a different resource, or remove the gateway resource, you can delete the gateway resource without affecting the gateway installation.</span></span> 

1. <span data-ttu-id="39758-190">기본 Azure 왼쪽 메뉴에서 **모든 리소스**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-190">From the main Azure left menu, go to **All resources**.</span></span> 
2. <span data-ttu-id="39758-191">데이터 게이트웨이 리소스를 찾아 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-191">Find and select your data gateway resource.</span></span>
3. <span data-ttu-id="39758-192">**온-프레미스 데이터 게이트웨이**를 선택하여 리소스 도구 모음에서 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39758-192">Choose **On-premises Data Gateway**, and on the resource toolbar, choose **Delete**.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="39758-193">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="39758-193">Frequently asked questions</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a><span data-ttu-id="39758-194">다음 단계</span><span class="sxs-lookup"><span data-stu-id="39758-194">Next steps</span></span>

* [<span data-ttu-id="39758-195">논리 앱 보안</span><span class="sxs-lookup"><span data-stu-id="39758-195">Secure your logic apps</span></span>](./logic-apps-securing-a-logic-app.md)
* [<span data-ttu-id="39758-196">논리 앱에 대한 일반적인 예제 및 시나리오</span><span class="sxs-lookup"><span data-stu-id="39758-196">Common examples and scenarios for logic apps</span></span>](./logic-apps-examples-and-scenarios.md)
