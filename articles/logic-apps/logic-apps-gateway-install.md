---
title: "온-프레미스 데이터 게이트웨이 설치 - Azure Logic Apps | Microsoft Docs"
description: "온-프레미스 데이터 원본에 액세스하기 전에 빠른 데이터 전송 및 암호화를 위해 온-프레미스 데이터 원본과 논리 앱 간에 온-프레미스 데이터 게이트웨이를 설치합니다."
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
ms.openlocfilehash: 34e68ae7d35019848b35c785a2715ec458dc6e73
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="install-the-on-premises-data-gateway-for-azure-logic-apps"></a><span data-ttu-id="ac2dd-104">Azure Logic Apps에 온-프레미스 데이터 게이트웨이 설치</span><span class="sxs-lookup"><span data-stu-id="ac2dd-104">Install the on-premises data gateway for Azure Logic Apps</span></span>

<span data-ttu-id="ac2dd-105">논리 앱에서 온-프레미스 데이터 원본에 액세스하기 전에 온-프레미스 데이터 게이트웨이를 설치하고 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-105">Before your logic apps can access data sources on premises, you must install and set up the on-premises data gateway.</span></span> <span data-ttu-id="ac2dd-106">게이트웨이는 온-프레미스 시스템과 논리 앱 간에 빠른 데이터 전송 및 암호화를 제공하는 브리지 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-106">The gateway acts as a bridge that provides quick data transfer and encryption between on-premises systems and your logic apps.</span></span> <span data-ttu-id="ac2dd-107">게이트웨이는 Azure Service Bus를 통해 암호화된 채널의 온-프레미스 원본에서 데이터를 릴레이합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-107">The gateway relays data from on-premises sources on encrypted channels through the Azure Service Bus.</span></span> <span data-ttu-id="ac2dd-108">보안으로 시작하는 모든 트래픽은 게이트웨이 에이전트에서 트래픽을 아웃바운드합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-108">All traffic originates as secure outbound traffic from the gateway agent.</span></span> <span data-ttu-id="ac2dd-109">[데이터 게이트웨이 작동 원리](#gateway-cloud-service)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-109">Learn more about [how the data gateway works](#gateway-cloud-service).</span></span>

<span data-ttu-id="ac2dd-110">게이트웨이는 다음과 같이 온-프레미스 데이터 원본에 대한 연결을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-110">The gateway supports connections to these data sources on premises:</span></span>

*   <span data-ttu-id="ac2dd-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="ac2dd-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="ac2dd-112">DB2</span><span class="sxs-lookup"><span data-stu-id="ac2dd-112">DB2</span></span>  
*   <span data-ttu-id="ac2dd-113">파일 시스템</span><span class="sxs-lookup"><span data-stu-id="ac2dd-113">File System</span></span>
*   <span data-ttu-id="ac2dd-114">Informix</span><span class="sxs-lookup"><span data-stu-id="ac2dd-114">Informix</span></span>
*   <span data-ttu-id="ac2dd-115">MQ</span><span class="sxs-lookup"><span data-stu-id="ac2dd-115">MQ</span></span>
*   <span data-ttu-id="ac2dd-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="ac2dd-116">MySQL</span></span>
*   <span data-ttu-id="ac2dd-117">Oracle 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="ac2dd-117">Oracle Database</span></span>
*   <span data-ttu-id="ac2dd-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="ac2dd-118">PostgreSQL</span></span>
*   <span data-ttu-id="ac2dd-119">SAP 응용 프로그램 서버</span><span class="sxs-lookup"><span data-stu-id="ac2dd-119">SAP Application Server</span></span> 
*   <span data-ttu-id="ac2dd-120">SAP 메시지 서버</span><span class="sxs-lookup"><span data-stu-id="ac2dd-120">SAP Message Server</span></span>
*   <span data-ttu-id="ac2dd-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="ac2dd-121">SharePoint</span></span>
*   <span data-ttu-id="ac2dd-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="ac2dd-122">SQL Server</span></span>
*   <span data-ttu-id="ac2dd-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="ac2dd-123">Teradata</span></span>

<span data-ttu-id="ac2dd-124">다음 단계에서는 [게이트웨이와 논리 앱 간의 연결을 설정](./logic-apps-gateway-connection.md)하기 전에 먼저 온-프레미스 데이터 게이트웨이를 설치하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-124">These steps show how to first install the on-premises data gateway before you [set up a connection between the gateway and your logic apps](./logic-apps-gateway-connection.md).</span></span> <span data-ttu-id="ac2dd-125">지원되는 커넥터에 대한 자세한 내용은 [Azure Logic Apps용 커넥터](https://docs.microsoft.com/azure/connectors/apis-list)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span></span> 

<span data-ttu-id="ac2dd-126">다른 서비스에서 게이트웨이를 사용하는 방법에 대한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-126">For information about how to use the gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="ac2dd-127">Microsoft Power BI 온-프레미스 데이터 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="ac2dd-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="ac2dd-128">Azure Analysis Services 온-프레미스 데이터 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="ac2dd-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="ac2dd-129">Microsoft Flow 온-프레미스 데이터 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="ac2dd-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="ac2dd-130">Microsoft PowerApps 온-프레미스 데이터 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="ac2dd-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

<a name="requirements"></a>
## <a name="requirements"></a><span data-ttu-id="ac2dd-131">요구 사항</span><span class="sxs-lookup"><span data-stu-id="ac2dd-131">Requirements</span></span>

<span data-ttu-id="ac2dd-132">**최소**:</span><span class="sxs-lookup"><span data-stu-id="ac2dd-132">**Minimum**:</span></span>

* <span data-ttu-id="ac2dd-133">.NET 4.5 Framework</span><span class="sxs-lookup"><span data-stu-id="ac2dd-133">.NET 4.5 Framework</span></span>
* <span data-ttu-id="ac2dd-134">64비트 버전의 Windows 7 또는 Windows Server 2008 R2 이상</span><span class="sxs-lookup"><span data-stu-id="ac2dd-134">64-bit version of Windows 7 or Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="ac2dd-135">**권장**:</span><span class="sxs-lookup"><span data-stu-id="ac2dd-135">**Recommended**:</span></span>

* <span data-ttu-id="ac2dd-136">8 코어 CPU</span><span class="sxs-lookup"><span data-stu-id="ac2dd-136">8 Core CPU</span></span>
* <span data-ttu-id="ac2dd-137">8GB 메모리</span><span class="sxs-lookup"><span data-stu-id="ac2dd-137">8 GB Memory</span></span>
* <span data-ttu-id="ac2dd-138">64비트 버전의 Windows 2012 R2 이상</span><span class="sxs-lookup"><span data-stu-id="ac2dd-138">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="ac2dd-139">**중요 고려 사항**:</span><span class="sxs-lookup"><span data-stu-id="ac2dd-139">**Important considerations**:</span></span>

* <span data-ttu-id="ac2dd-140">온-프레미스 데이터 게이트웨이를 로컬 컴퓨터에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-140">Install the on-premises data gateway only on a local computer.</span></span>
<span data-ttu-id="ac2dd-141">도메인 컨트롤러에 게이트웨이를 설치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-141">You can't install the gateway on a domain controller.</span></span>

   > [!TIP]
   > <span data-ttu-id="ac2dd-142">데이터 원본과 동일한 컴퓨터에 게이트웨이를 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-142">You don't have to install the gateway on the same computer as your data source.</span></span> <span data-ttu-id="ac2dd-143">대기 시간을 최소화하려면 권한이 있다고 가정하여 가능하면 데이터 원본과 가깝게 또는 동일한 컴퓨터에 게이트웨이를 설치하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-143">To minimize latency, you can install the gateway as close as possible to your data source, or on the same computer, assuming that you have permissions.</span></span>

* <span data-ttu-id="ac2dd-144">게이트웨이가 이러한 상황에서 실행되지 않을 수 있기 때문에 꺼지거나, 절전 또는 인터넷에 연결되지 않은 컴퓨터에서 게이트웨이를 설치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-144">Don't install the gateway on a computer that turns off, goes to sleep, or doesn't connect to the Internet because the gateway can't run under those circumstances.</span></span> <span data-ttu-id="ac2dd-145">또한 무선 네트워크에서는 게이트웨이 성능이 저하될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-145">Also, gateway performance might suffer over a wireless network.</span></span>

* <span data-ttu-id="ac2dd-146">설치하는 동안 Microsoft 계정이 아니라 Azure Active Directory(Azure AD)에서 관리하는 [회사 또는 학교 계정](https://docs.microsoft.com/azure/active-directory/sign-up-organization)으로 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-146">During installation, you must sign in with a [work or school account](https://docs.microsoft.com/azure/active-directory/sign-up-organization) that's managed by Azure Active Directory (Azure AD), not a Microsoft account.</span></span> 

  <span data-ttu-id="ac2dd-147">나중에 Azure Portal에서 게이트웨이 설치를 통해 게이트웨이 리소스를 만들고 연결할 때 동일한 회사 또는 학교 계정을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-147">You have to use the same work or school account later in the Azure portal when you create and associate a gateway resource with your gateway installation.</span></span> <span data-ttu-id="ac2dd-148">그런 다음 논리 앱과 온-프레미스 데이터 원본 간의 연결을 만들 때 이 게이트웨이 리소스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-148">You then select this gateway resource when you create the connection between your logic app and the on-premises data source.</span></span> [<span data-ttu-id="ac2dd-149">Azure AD 회사 또는 학교 계정을 사용해야 하는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="ac2dd-149">Why must I use an Azure AD work or school account?</span></span>](#why-azure-work-school-account)

  > [!TIP]
  > <span data-ttu-id="ac2dd-150">Office 365 서비스에 등록하고 실제 회사 전자 메일을 제공하지 않은 경우 로그인 주소는 jeff@contoso.onmicrosoft.com과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-150">If you signed up for an Office 365 offering and didn't supply your actual work email, your sign-in address might look like jeff@contoso.onmicrosoft.com.</span></span> 

* <span data-ttu-id="ac2dd-151">기존 게이트웨이를 14.16.6317.4보다 이전 버전인 설치 관리자를 사용하여 설정한 경우 최신 설치 관리자를 실행하여 게이트웨이 위치를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-151">If you have an existing gateway that you set up with an installer that's earlier than version 14.16.6317.4, you can't change your gateway's location by running the latest installer.</span></span> <span data-ttu-id="ac2dd-152">그러나 최신 설치 관리자를 사용하여 새 게이트웨이를 원하는 위치로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-152">However, you can use the latest installer to set up a new gateway with the location that you want instead.</span></span>
  
  <span data-ttu-id="ac2dd-153">14.16.6317.4보다 이전 버전인 게이트웨이 설치 관리자가 있지만 게이트웨이를 아직 설치하지 않은 경우 최신 설치 관리자를 다운로드하여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-153">If you have a gateway installer that's earlier than version 14.16.6317.4, but you haven't installed your gateway yet, you can download and use the latest installer.</span></span>

<a name="install-gateway"></a>

## <a name="install-the-data-gateway"></a><span data-ttu-id="ac2dd-154">데이터 게이트웨이 설치</span><span class="sxs-lookup"><span data-stu-id="ac2dd-154">Install the data gateway</span></span>

1.  <span data-ttu-id="ac2dd-155">[로컬 컴퓨터에서 게이트웨이 설치 관리자를 다운로드하고 실행합니다](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="ac2dd-155">[Download and run the gateway installer on a local computer](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span></span>

2. <span data-ttu-id="ac2dd-156">개인정보처리방침 및 사용 약관을 검토하고 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-156">Review and accept the terms of use and privacy statement.</span></span>

3. <span data-ttu-id="ac2dd-157">게이트웨이를 설치하려는 로컬 컴퓨터의 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-157">Specify the path on your local computer where you want to install the gateway.</span></span>

4. <span data-ttu-id="ac2dd-158">메시지가 표시되면 Microsoft 계정이 아닌 Azure 회사 또는 학교 계정을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-158">When prompted, sign in with your Azure work or school account, not a Microsoft account.</span></span>

   ![Azure 회사 또는 학교 계정으로 로그인](./media/logic-apps-gateway-install/sign-in-gateway-install.png)

5. <span data-ttu-id="ac2dd-160">이제 설치된 게이트웨이를 [게이트웨이 클라우드 서비스](#gateway-cloud-service)에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-160">Now register your installed gateway with the [gateway cloud service](#gateway-cloud-service).</span></span> <span data-ttu-id="ac2dd-161">**이 컴퓨터에 새 게이트웨이 등록**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-161">Choose **Register a new gateway on this computer**.</span></span>

   <span data-ttu-id="ac2dd-162">게이트웨이 클라우드 서비스는 데이터 원본 자격 증명 및 게이트웨이 세부 정보를 암호화하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-162">The gateway cloud service encrypts and stores your data source credentials and gateway details.</span></span> 
   <span data-ttu-id="ac2dd-163">또한 서비스는 논리 앱, 온-프레미스 데이터 게이트웨이 및 온-프레미스 데이터 원본 간에 쿼리 및 해당 결과를 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-163">The service also routes queries and their results between your logic app, the on-premises data gateway, and your data source on premises.</span></span>

6. <span data-ttu-id="ac2dd-164">게이트웨이 설치에 대한 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-164">Provide a name for your gateway installation.</span></span> <span data-ttu-id="ac2dd-165">복구 키를 만든 다음 복구 키를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-165">Create a recovery key, then confirm your recovery key.</span></span> 

   > [!IMPORTANT] 
   > <span data-ttu-id="ac2dd-166">복구 키는 8자 이상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-166">Your recovery key must contain at least eight characters.</span></span> <span data-ttu-id="ac2dd-167">키를 안전한 장소에 저장하고 보관해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-167">Make sure that you save and keep the key in a safe place.</span></span> <span data-ttu-id="ac2dd-168">기존 게이트웨이를 마이그레이션, 복원 또는 사용하려는 경우에도 이 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-168">You also need this key when you want to migrate, restore, or take over an existing gateway.</span></span>

   1. <span data-ttu-id="ac2dd-169">게이트웨이 설치에서 사용하는 클라우드 서비스 게이트웨이 및 Azure Service Bus에 대한 기본 지역을 변경하려면 **지역 변경**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-169">To change the default region for the gateway cloud service and Azure Service Bus used by your gateway installation, choose **Change Region**.</span></span>

      ![지역 변경](./media/logic-apps-gateway-install/change-region-gateway-install.png)

      <span data-ttu-id="ac2dd-171">기본 지역은 Azure AD 테넌트와 연결된 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-171">The default region is the region associated with your Azure AD tenant.</span></span>

   2. <span data-ttu-id="ac2dd-172">다음 창에서 **지역 선택**을 열고 다른 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-172">On the next pane, open the **Select Region** to choose a different region.</span></span>

      ![다른 지역 선택](./media/logic-apps-gateway-install/select-region-gateway-install.png)

      <span data-ttu-id="ac2dd-174">예를 들어, 대기 시간을 줄일 수 있도록 논리 앱과 동일한 지역을 선택하거나 온-프레미스 데이터 원본에 가장 가까운 지역을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-174">For example, you might select the same region as your logic app, or select the region closest to your on-premises data source so you can reduce latency.</span></span> <span data-ttu-id="ac2dd-175">게이트웨이 리소스와 논리 앱은 서로 다른 위치에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-175">Your gateway resource and logic app can have different locations.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="ac2dd-176">설치 후에 이 지역을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-176">You can't change this region after installation.</span></span> <span data-ttu-id="ac2dd-177">또한 이 지역은 게이트웨이에 대한 Azure 리소스를 만들 수 있는 위치를 결정하고 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-177">This region also determines and restricts the location where you can create the Azure resource for your gateway.</span></span> <span data-ttu-id="ac2dd-178">따라서 Azure에서 게이트웨이 리소스를 만들 때 리소스 위치가 게이트웨이를 설치할 때 선택한 지역과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-178">So when you create your gateway resource in Azure, make sure that the resource location matches the region that you selected during gateway installation.</span></span>
      > 
      > <span data-ttu-id="ac2dd-179">나중에 게이트웨이에 다른 지역을 사용하려는 경우 새 게이트웨이를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-179">If you want to use a different region for your gateway later, you must set up a new gateway.</span></span>

   3. <span data-ttu-id="ac2dd-180">준비가 되면 **완료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-180">When you're ready, choose **Done**.</span></span>

7. <span data-ttu-id="ac2dd-181">이제 [게이트웨이에 대한 Azure 리소스를 만들](../logic-apps/logic-apps-gateway-connection.md) 수 있도록 Azure Portal에서 이러한 단계에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-181">Now follow these steps in the Azure portal so you can [create an Azure resource for your gateway](../logic-apps/logic-apps-gateway-connection.md).</span></span> 

<span data-ttu-id="ac2dd-182">[데이터 게이트웨이 작동 원리](#gateway-cloud-service)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-182">Learn more about [how the data gateway works](#gateway-cloud-service).</span></span>

## <a name="migrate-restore-or-take-over-an-existing-gateway"></a><span data-ttu-id="ac2dd-183">기존 게이트웨이 마이그레이션, 복원 또는 사용</span><span class="sxs-lookup"><span data-stu-id="ac2dd-183">Migrate, restore, or take over an existing gateway</span></span>

<span data-ttu-id="ac2dd-184">이러한 작업을 수행하려면 게이트웨이가 설치될 때 지정된 복구 키가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-184">To perform these tasks, you must have the recovery key that was specified when the gateway was installed.</span></span>

1. <span data-ttu-id="ac2dd-185">컴퓨터의 시작 메뉴에서 **온-프레미스 데이터 게이트웨이**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-185">From your computer's Start menu, choose **On-premises data gateway**.</span></span>

2. <span data-ttu-id="ac2dd-186">설치 관리자가 열리면 이전에 게이트웨이 설치에 사용한 것과 동일한 Azure 회사 또는 학교 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-186">After the installer opens, sign in with the same Azure work or school account that was previously used to install the gateway.</span></span>

3. <span data-ttu-id="ac2dd-187">**기존 게이트웨이 마이그레이션, 복원 또는 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-187">Choose **Migrate, restore, or take over an existing gateway**.</span></span>

4. <span data-ttu-id="ac2dd-188">마이그레이션, 복원 또는 사용하려는 게이트웨이에 대한 이름과 복구 키를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-188">Provide the name and recovery key for the gateway that you want to migrate, restore, or take over.</span></span>

<a name="restart-gateway"></a>
## <a name="restart-the-gateway"></a><span data-ttu-id="ac2dd-189">게이트웨이 다시 시작</span><span class="sxs-lookup"><span data-stu-id="ac2dd-189">Restart the gateway</span></span>

<span data-ttu-id="ac2dd-190">게이트웨이는 Windows 서비스로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-190">The gateway runs as a Windows service.</span></span> <span data-ttu-id="ac2dd-191">다른 Windows 서비스와 마찬가지로 여러 가지 방법으로 서비스를 시작하고 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-191">Like any other Windows service, you can start and stop the service in multiple ways.</span></span> <span data-ttu-id="ac2dd-192">예를 들어 게이트웨이가 실행 중인 컴퓨터에서 관리자 권한으로 명령 프롬프트를 열고 다음 명령 중 하나를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-192">For example, you can open a command prompt with elevated permissions on the computer where the gateway is running, and run either these commands:</span></span>

* <span data-ttu-id="ac2dd-193">서비스를 중지하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-193">To stop the service, run this command:</span></span>
  
    `net stop PBIEgwService`

* <span data-ttu-id="ac2dd-194">서비스를 시작하려면 이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-194">To start the service, run this command:</span></span>
  
    `net start PBIEgwService`

### <a name="windows-service-account"></a><span data-ttu-id="ac2dd-195">Windows 서비스 계정</span><span class="sxs-lookup"><span data-stu-id="ac2dd-195">Windows service account</span></span>

<span data-ttu-id="ac2dd-196">온-프레미스 데이터 게이트웨이는 Windows 서비스 로그인 자격 증명에 `NT SERVICE\PBIEgwService`를 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-196">The on-premises data gateway is set up to use `NT SERVICE\PBIEgwService` for the Windows service logon credentials.</span></span> <span data-ttu-id="ac2dd-197">게이트웨이는 기본적으로 게이트웨이를 설치한 컴퓨터에서 "서비스로 로그온(Log on as a service)"할 권한을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-197">By default, the gateway has the "Log on as a service" right for the machine where you install the gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="ac2dd-198">Windows 서비스 계정은 온-프레미스 데이터 원본에 연결하는 데 사용되는 동일한 계정 및 클라우드 서비스에 로그인하는 데 사용되는 Azure 회사 또는 학교 계정과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-198">The Windows service account differs from the account used for connecting to on-premises data sources, and from the Azure work or school account used to sign in to cloud services.</span></span>

## <a name="configure-a-firewall-or-proxy"></a><span data-ttu-id="ac2dd-199">방화벽 또는 프록시 구성</span><span class="sxs-lookup"><span data-stu-id="ac2dd-199">Configure a firewall or proxy</span></span>

<span data-ttu-id="ac2dd-200">게이트웨이는 [Azure Service Bus](https://azure.microsoft.com/services/service-bus/)에 대한 아웃바운드 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-200">The gateway creates an outbound connection to [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="ac2dd-201">게이트웨이에 대한 프록시 정보를 제공하려면 [프록시 설정 구성](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-201">To provide proxy information for your gateway, see [Configure proxy settings](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span></span>

<span data-ttu-id="ac2dd-202">방화벽 또는 프록시가 연결을 차단할 수 있는지를 확인하려면 컴퓨터가 인터넷 및 [Azure Service Bus](https://azure.microsoft.com/services/service-bus/)에 실제로 연결할 수 있는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-202">To check whether your firewall, or proxy, might block connections, confirm whether your machine can actually connect to the internet and the [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="ac2dd-203">PowerShell 창에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-203">From a PowerShell prompt, run this command:</span></span>

`Test-NetConnection -ComputerName watchdog.servicebus.windows.net -Port 9350`

> [!NOTE]
> <span data-ttu-id="ac2dd-204">이 명령은 Azure Service Bus에 대한 네트워크 연결 및 연결만을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-204">This command only tests network connectivity and connectivity to the Azure Service Bus.</span></span> <span data-ttu-id="ac2dd-205">따라서 이 명령은 게이트웨이 또는 게이트웨이 클라우드 서비스에서 자격 증명 및 게이트웨이 세부 정보를 암호화하고 저장하는 작업을 수행하는 것과 아무 관련이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-205">So the command doesn't have anything to do with the gateway or the gateway cloud service that encrypts and stores your credentials and gateway details.</span></span> 
>
> <span data-ttu-id="ac2dd-206">또한 이 명령은 Windows Server 2012 R2 이상 및 Windows 8.1 이상에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-206">Also, this command is only available on Windows Server 2012 R2 or later, and Windows 8.1 or later.</span></span> <span data-ttu-id="ac2dd-207">이전 OS 버전에서 연결을 테스트하는 데 텔넷을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-207">On earlier OS versions, you can use Telnet to test connectivity.</span></span> <span data-ttu-id="ac2dd-208">[Azure Service Bus 및 하이브리드 솔루션](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-208">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

<span data-ttu-id="ac2dd-209">결과는 다음 예제와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-209">Your results should look similar to this example:</span></span>

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

<span data-ttu-id="ac2dd-210">**TcpTestSucceeded**가 **True**로 설정되지 않으면 방화벽에 의해 차단될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-210">If **TcpTestSucceeded** is not set to **True**, you might be blocked by a firewall.</span></span> <span data-ttu-id="ac2dd-211">포괄적으로 설정하려면 **ComputerName** 및 **포트** 값을 이 항목의 [포트 구성](#configure-ports) 아래에 나열된 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-211">If you want to be comprehensive, substitute the **ComputerName** and **Port** values with the values listed under [Configure ports](#configure-ports) in this topic.</span></span>

<span data-ttu-id="ac2dd-212">또한 방화벽이 Azure Service Bus와 Azure 데이터 센터 간에 형성된 연결을 차단할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-212">The firewall might also block connections that the Azure Service Bus makes to the Azure datacenters.</span></span> <span data-ttu-id="ac2dd-213">이 시나리오를 실행할 경우 지역에서 해당 데이터 센터에 대한 모든 IP 주소를 승인(차단 해제)합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-213">If this scenario happens, approve (unblock) all the IP addresses for those datacenters in your region.</span></span> <span data-ttu-id="ac2dd-214">해당 IP 주소는 [여기에서 Azure IP 주소 목록을 가져옵니다](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="ac2dd-214">For those IP addresses, [get the Azure IP addresses list here](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

## <a name="configure-ports"></a><span data-ttu-id="ac2dd-215">포트 구성</span><span class="sxs-lookup"><span data-stu-id="ac2dd-215">Configure ports</span></span>

<span data-ttu-id="ac2dd-216">게이트웨이는 [Azure Service Bus](https://azure.microsoft.com/services/service-bus/)에 대한 아웃바운드 연결을 만들고 아웃바운드 포트인 TCP 443(기본값), 5671, 5672, 9350~9354에서 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-216">The gateway creates an outbound connection to [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) and communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span> <span data-ttu-id="ac2dd-217">게이트웨이에 인바운드 포트가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-217">The gateway doesn't require inbound ports.</span></span> <span data-ttu-id="ac2dd-218">[Azure Service Bus 및 하이브리드 솔루션](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-218">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

| <span data-ttu-id="ac2dd-219">도메인 이름</span><span class="sxs-lookup"><span data-stu-id="ac2dd-219">DOMAIN NAMES</span></span> | <span data-ttu-id="ac2dd-220">아웃바운드 포트</span><span class="sxs-lookup"><span data-stu-id="ac2dd-220">OUTBOUND PORTS</span></span> | <span data-ttu-id="ac2dd-221">설명</span><span class="sxs-lookup"><span data-stu-id="ac2dd-221">DESCRIPTION</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ac2dd-222">*.analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="ac2dd-222">*.analysis.windows.net</span></span> | <span data-ttu-id="ac2dd-223">443</span><span class="sxs-lookup"><span data-stu-id="ac2dd-223">443</span></span> | <span data-ttu-id="ac2dd-224">HTTPS</span><span class="sxs-lookup"><span data-stu-id="ac2dd-224">HTTPS</span></span> | 
| <span data-ttu-id="ac2dd-225">*.login.windows.net</span><span class="sxs-lookup"><span data-stu-id="ac2dd-225">*.login.windows.net</span></span> | <span data-ttu-id="ac2dd-226">443</span><span class="sxs-lookup"><span data-stu-id="ac2dd-226">443</span></span> | <span data-ttu-id="ac2dd-227">HTTPS</span><span class="sxs-lookup"><span data-stu-id="ac2dd-227">HTTPS</span></span> | 
| <span data-ttu-id="ac2dd-228">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="ac2dd-228">*.servicebus.windows.net</span></span> | <span data-ttu-id="ac2dd-229">5671-5672</span><span class="sxs-lookup"><span data-stu-id="ac2dd-229">5671-5672</span></span> | <span data-ttu-id="ac2dd-230">AMQP(고급 메시지 큐 프로토콜)</span><span class="sxs-lookup"><span data-stu-id="ac2dd-230">Advanced Message Queuing Protocol (AMQP)</span></span> | 
| <span data-ttu-id="ac2dd-231">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="ac2dd-231">*.servicebus.windows.net</span></span> | <span data-ttu-id="ac2dd-232">443, 9350-9354</span><span class="sxs-lookup"><span data-stu-id="ac2dd-232">443, 9350-9354</span></span> | <span data-ttu-id="ac2dd-233">TCP의 서비스 버스 릴레이에 대한 수신기(액세스 제어 토큰 획득에 443 필요)</span><span class="sxs-lookup"><span data-stu-id="ac2dd-233">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> | 
| <span data-ttu-id="ac2dd-234">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="ac2dd-234">*.frontend.clouddatahub.net</span></span> | <span data-ttu-id="ac2dd-235">443</span><span class="sxs-lookup"><span data-stu-id="ac2dd-235">443</span></span> | <span data-ttu-id="ac2dd-236">HTTPS</span><span class="sxs-lookup"><span data-stu-id="ac2dd-236">HTTPS</span></span> | 
| <span data-ttu-id="ac2dd-237">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="ac2dd-237">*.core.windows.net</span></span> | <span data-ttu-id="ac2dd-238">443</span><span class="sxs-lookup"><span data-stu-id="ac2dd-238">443</span></span> | <span data-ttu-id="ac2dd-239">HTTPS</span><span class="sxs-lookup"><span data-stu-id="ac2dd-239">HTTPS</span></span> | 
| <span data-ttu-id="ac2dd-240">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="ac2dd-240">login.microsoftonline.com</span></span> | <span data-ttu-id="ac2dd-241">443</span><span class="sxs-lookup"><span data-stu-id="ac2dd-241">443</span></span> | <span data-ttu-id="ac2dd-242">HTTPS</span><span class="sxs-lookup"><span data-stu-id="ac2dd-242">HTTPS</span></span> | 
| <span data-ttu-id="ac2dd-243">*.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="ac2dd-243">*.msftncsi.com</span></span> | <span data-ttu-id="ac2dd-244">443</span><span class="sxs-lookup"><span data-stu-id="ac2dd-244">443</span></span> | <span data-ttu-id="ac2dd-245">Power BI 서비스에서 게이트웨이에 연결할 수 없는 경우 인터넷 연결을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-245">Used to test internet connectivity when the gateway is unreachable by the Power BI service.</span></span> | 

<span data-ttu-id="ac2dd-246">도메인 대신 IP 주소를 승인해야 하는 경우 [Microsoft Azure 데이터 센터 IP 범위 목록](https://www.microsoft.com/download/details.aspx?id=41653)을 다운로드하여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-246">If you have to approve IP addresses instead of the domains, you can download and use the [Microsoft Azure Datacenter IP ranges list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="ac2dd-247">일부 경우에는 정규화된 도메인 이름이 아닌 IP 주소를 사용해서 Azure Service Bus를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-247">In some cases, the Azure Service Bus connections are made with IP Address rather than fully qualified domain names.</span></span>

<a name="gateway-cloud-service"></a>
## <a name="how-does-the-data-gateway-work"></a><span data-ttu-id="ac2dd-248">데이터 게이트웨이는 어떻게 작동하나요?</span><span class="sxs-lookup"><span data-stu-id="ac2dd-248">How does the data gateway work?</span></span>

<span data-ttu-id="ac2dd-249">데이터 게이트웨이는 논리 앱, 게이트웨이 클라우드 서비스 및 온-프레미스 데이터 원본 간의 빠르고 안전한 통신을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-249">The data gateway facilitates quick and secure communication between your logic app, the gateway cloud service, and your on-premises data source.</span></span> 

![diagram-for-on-premises-data-gateway-flow](./media/logic-apps-gateway-install/how-on-premises-data-gateway-works-flow-diagram.png)

<span data-ttu-id="ac2dd-251">따라서 클라우드의 사용자가 온-프레미스 데이터 원본에 연결된 요소와 상호 작용하는 경우:</span><span class="sxs-lookup"><span data-stu-id="ac2dd-251">So when the user in the cloud interacts with an element that's connected to your on-premises data source:</span></span>

1. <span data-ttu-id="ac2dd-252">게이트웨이 클라우드 서비스가 데이터 원본에 대해 암호화된 자격 증명과 함께 쿼리를 만들고, 게이트웨이가 처리할 수 있게 쿼리를 큐에 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-252">The gateway cloud service creates a query, along with the encrypted credentials for the data source, and sends the query to the queue for the gateway to process.</span></span>

2. <span data-ttu-id="ac2dd-253">게이트웨이 클라우드 서비스에서 쿼리를 분석하고 Azure Service Bus에 대한 요청을 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-253">The gateway cloud service analyzes the query and pushes the request to the Azure Service Bus.</span></span>

3. <span data-ttu-id="ac2dd-254">온-프레미스 데이터 게이트웨이가 보류 중인 요청을 위해 Azure 서비스 버스를 폴링합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-254">The on-premises data gateway polls the Azure Service Bus for pending requests.</span></span>

4. <span data-ttu-id="ac2dd-255">게이트웨이가 쿼리를 가져오고, 자격 증명의 암호를 해독하고, 해당 자격 증명으로 데이터 원본에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-255">The gateway gets the query, decrypts the credentials, and connects to the data source with those credentials.</span></span>

5. <span data-ttu-id="ac2dd-256">게이트웨이가 실행을 위해 데이터 원본에 쿼리를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-256">The gateway sends the query to the data source for execution.</span></span>

6. <span data-ttu-id="ac2dd-257">결과가 데이터 원본에서 게이트웨이로 다시 전송된 후 게이트웨이 클라우드 서비스로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-257">The results are sent from the data source, back to the gateway, and then to the gateway cloud service.</span></span> <span data-ttu-id="ac2dd-258">게이트웨이 클라우드 서비스에서 해당 결과를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-258">The gateway cloud service then uses the results.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="ac2dd-259">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="ac2dd-259">Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="ac2dd-260">일반</span><span class="sxs-lookup"><span data-stu-id="ac2dd-260">General</span></span>

<span data-ttu-id="ac2dd-261">**Q**: SQL Azure와 같은 클라우드에서 데이터 원본에 대한 게이트웨이가 필요하나요?</span><span class="sxs-lookup"><span data-stu-id="ac2dd-261">**Q**: Do I need a gateway for data sources in the cloud, such as SQL Azure?</span></span> <br/><span data-ttu-id="ac2dd-262">
**A**: 아니요.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-262">
**A**: No.</span></span> <span data-ttu-id="ac2dd-263">게이트웨이는 온-프레미스 데이터 원본에만 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-263">A gateway connects to on-premises data sources only.</span></span>

<span data-ttu-id="ac2dd-264">**Q**: 데이터 원본과 동일한 컴퓨터에 게이트웨이를 설치해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="ac2dd-264">**Q**: Does the gateway have to be installed on the same machine as the data source?</span></span> <br/><span data-ttu-id="ac2dd-265">
**A**: 아니요.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-265">
**A**: No.</span></span> <span data-ttu-id="ac2dd-266">게이트웨이는 제공된 연결 정보를 사용하여 데이터 원본에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-266">The gateway connects to the data source using the connection information that was provided.</span></span> <span data-ttu-id="ac2dd-267">이러한 의미에서 게이트웨이를 클라이언트 응용 프로그램이라고 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-267">Consider the gateway as a client application in this sense.</span></span> <span data-ttu-id="ac2dd-268">게이트웨이는 제공된 서버 이름에 연결할 수 있는 기능이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-268">The gateway just needs the capability to connect to the server name that was provided.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="ac2dd-269">**Q:**: Azure 회사 또는 학교 계정을 사용하여 로그인해야 하는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="ac2dd-269">**Q**: Why must I use an Azure work or school account to sign in?</span></span> <br/><span data-ttu-id="ac2dd-270">
**A**: 온-프레미스 데이터 게이트웨이를 설치할 때만 Azure 회사 또는 학교 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-270">
**A**: You can only use an Azure work or school account when you install the on-premises data gateway.</span></span> <span data-ttu-id="ac2dd-271">로그인 계정은 Azure AD(Azure Active Directory)에서 관리하는 테넌트에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-271">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="ac2dd-272">일반적으로 Azure AD 계정의 UPN(사용자 계정 이름)은 이메일 주소와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-272">Usually, your Azure AD account's user principal name (UPN) matches the email address.</span></span>

<span data-ttu-id="ac2dd-273">**Q**: 자격 증명은 어디에 저장되나요?</span><span class="sxs-lookup"><span data-stu-id="ac2dd-273">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="ac2dd-274">
**A**: 데이터 원본에 입력한 자격 증명은 게이트웨이 클라우드 서비스에 암호화되어 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-274">
**A**: The credentials that you enter for a data source are encrypted and stored in the gateway cloud service.</span></span> <span data-ttu-id="ac2dd-275">자격 증명은 온-프레미스 데이터 게이트웨이에서 해독됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-275">The credentials are decrypted at the on-premises data gateway.</span></span>

<span data-ttu-id="ac2dd-276">**Q**: 네트워크 대역폭에 대한 요구 사항이 있나요?</span><span class="sxs-lookup"><span data-stu-id="ac2dd-276">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="ac2dd-277">
**A**: 네트워크 연결의 처리량이 높은 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-277">
**A**: We recommend that your network connection has good throughput.</span></span> <span data-ttu-id="ac2dd-278">모든 환경은 다르며 전송되는 데이터의 양은 결과에 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-278">Every environment is different, and the amount of data being sent affects the results.</span></span> <span data-ttu-id="ac2dd-279">ExpressRoute를 사용하면 온-프레미스 및 Azure 데이터 센터 간의 처리량 수준을 보장하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-279">Using ExpressRoute could help to guarantee a level of throughput between on-premises and the Azure datacenters.</span></span>
<span data-ttu-id="ac2dd-280">타사 도구인 Azure Speed Test 앱을 사용하면 처리량을 측정하는 데 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-280">You can use the third-party tool Azure Speed Test app to help gauge your throughput.</span></span>

<span data-ttu-id="ac2dd-281">**Q**: 게이트웨이에서 데이터 원본으로의 쿼리를 실행할 때 나타나는 대기 시간은 얼마나 되나요?</span><span class="sxs-lookup"><span data-stu-id="ac2dd-281">**Q**: What is the latency for running queries to a data source from the gateway?</span></span> <span data-ttu-id="ac2dd-282">최선의 아키텍처는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="ac2dd-282">What is the best architecture?</span></span> <br/><span data-ttu-id="ac2dd-283">
**A**: 네트워크 대기 시간을 줄이려면 게이트웨이를 데이터 원본에 최대한 가깝게 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-283">
**A**: To reduce network latency, install the gateway as close to the data source as possible.</span></span> <span data-ttu-id="ac2dd-284">실제 데이터 원본에 게이트웨이를 설치할 수 있는 경우 이 근접성으로 인해 발생하는 대기 시간이 최소화됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-284">If you can install the gateway on the actual data source, this proximity minimizes the latency introduced.</span></span> <span data-ttu-id="ac2dd-285">데이터 센터도 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-285">Consider the datacenters too.</span></span> <span data-ttu-id="ac2dd-286">예를 들어 서비스에서 미국 서부 데이터 센터를 사용하고 Azure VM에서 SQL Server가 호스트되는 경우 Azure VM도 미국 서부에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-286">For example, if your service uses the West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in the West US too.</span></span> <span data-ttu-id="ac2dd-287">이 근접성으로 인해 대기 시간이 최소화되고 Azure VM에서 송신 요금이 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-287">This proximity minimizes latency and avoids egress charges on the Azure VM.</span></span>

<span data-ttu-id="ac2dd-288">**Q**: 결과가 클라우드로 어떻게 다시 전송되나요?</span><span class="sxs-lookup"><span data-stu-id="ac2dd-288">**Q**: How are results sent back to the cloud?</span></span> <br/><span data-ttu-id="ac2dd-289">
**A**: Azure Service Bus를 통해 결과가 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-289">
**A**: Results are sent through the Azure Service Bus.</span></span>

<span data-ttu-id="ac2dd-290">**Q**: 클라우드에서 게이트웨이로의 인바운드 연결이 있나요?</span><span class="sxs-lookup"><span data-stu-id="ac2dd-290">**Q**: Are there any inbound connections to the gateway from the cloud?</span></span> <br/><span data-ttu-id="ac2dd-291">
**A**: 아니요.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-291">
**A**: No.</span></span> <span data-ttu-id="ac2dd-292">게이트웨이는 Azure 서비스 버스에 대해 아웃바운드 연결을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-292">The gateway uses outbound connections to Azure Service Bus.</span></span>

<span data-ttu-id="ac2dd-293">**Q**: 아웃바운드 연결을 차단하면 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="ac2dd-293">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="ac2dd-294">이러한 연결을 열려면 무엇이 필요한가요?</span><span class="sxs-lookup"><span data-stu-id="ac2dd-294">What do I need to open?</span></span> <br/><span data-ttu-id="ac2dd-295">
**A**: 게이트웨이가 사용하는 포트 및 호스트를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-295">
**A**: See the ports and hosts that the gateway uses.</span></span>

<span data-ttu-id="ac2dd-296">**Q**: 실제 Windows 서비스를 어떻게 지칭하나요?</span><span class="sxs-lookup"><span data-stu-id="ac2dd-296">**Q**: What is the actual Windows service called?</span></span><br/><span data-ttu-id="ac2dd-297">
**A**: 서비스에서 게이트웨이를 Power BI 엔터프라이즈 게이트웨이 서비스라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-297">
**A**: In Services, the gateway is called Power BI Enterprise Gateway Service.</span></span>

<span data-ttu-id="ac2dd-298">**Q**: Azure Active Directory 계정으로 게이트웨이 Windows 서비스를 실행할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="ac2dd-298">**Q**: Can the gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="ac2dd-299">
**A**: 아니요.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-299">
**A**: No.</span></span> <span data-ttu-id="ac2dd-300">Windows 서비스에는 유효한 Windows 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-300">The Windows service must have a valid Windows account.</span></span> <span data-ttu-id="ac2dd-301">기본적으로 서비스는 서비스 SID, NT SERVICE\PBIEgwService를 사용하여 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-301">By default, the service runs with the Service SID, NT SERVICE\PBIEgwService.</span></span>

### <a name="high-availability-and-disaster-recovery"></a><span data-ttu-id="ac2dd-302">고가용성 및 재해 복구</span><span class="sxs-lookup"><span data-stu-id="ac2dd-302">High availability and disaster recovery</span></span>

<span data-ttu-id="ac2dd-303">**Q**: 재해 복구를 위해 어떤 옵션을 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="ac2dd-303">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="ac2dd-304">
**A**: 복구 키를 사용하여 게이트웨이를 복원하거나 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-304">
**A**: You can use the recovery key to restore or move a gateway.</span></span> <span data-ttu-id="ac2dd-305">게이트웨이를 설치할 때 복구 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-305">When you install the gateway, specify the recovery key.</span></span>

<span data-ttu-id="ac2dd-306">**Q**: 복구 키를 사용할 경우의 이점은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="ac2dd-306">**Q**: What is the benefit of the recovery key?</span></span> <br/><span data-ttu-id="ac2dd-307">
**A**: 복구 키는 재해 발생 후 게이트웨이 설정을 마이그레이션하거나 복구할 수 있는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-307">
**A**: The recovery key provides a way to migrate or recover your gateway settings after a disaster.</span></span>

<span data-ttu-id="ac2dd-308">**Q**: 게이트웨이에 고가용성 시나리오를 사용하기 위한 계획이 있나요?</span><span class="sxs-lookup"><span data-stu-id="ac2dd-308">**Q**: Are there any plans for enabling high availability scenarios with the gateway?</span></span> <br/><span data-ttu-id="ac2dd-309">
**A**: 이러한 시나리오는 로드맵에는 있지만 아직 일정은 나와 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-309">
**A**: These scenarios are on the roadmap, but we don't have a timeline yet.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ac2dd-310">문제 해결</span><span class="sxs-lookup"><span data-stu-id="ac2dd-310">Troubleshooting</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

<span data-ttu-id="ac2dd-311">**Q**: 온-프레미스 데이터 원본으로 어떤 쿼리가 전송되고 있는지를 어떻게 알 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="ac2dd-311">**Q**: How can I see what queries are being sent to the on-premises data source?</span></span> <br/><span data-ttu-id="ac2dd-312">
**A**: 전송 중인 쿼리를 포함하는 쿼리 추적을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-312">
**A**: You can enable query tracing, which includes the queries that are sent.</span></span> <span data-ttu-id="ac2dd-313">문제 해결이 끝나면 쿼리 추적을 원래 값으로 다시 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-313">Remember to change query tracing back to the original value when done troubleshooting.</span></span> <span data-ttu-id="ac2dd-314">쿼리 추적 기능을 그대로 두면 큰 로그가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-314">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="ac2dd-315">또한 추적 쿼리를 위해 데이터 원본이 포함하는 도구를 살펴볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-315">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="ac2dd-316">예를 들어 SQL Server 및 Analysis Services의 경우 확장 이벤트 또는 SQL 프로파일러를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-316">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="ac2dd-317">**Q**: 게이트웨이 로그는 어디에 있나요?</span><span class="sxs-lookup"><span data-stu-id="ac2dd-317">**Q**: Where are the gateway logs?</span></span> <br/><span data-ttu-id="ac2dd-318">
**A**: 이 항목 뒷부분에 나오는 도구를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-318">
**A**: See Tools later in this topic.</span></span>

### <a name="update-to-the-latest-version"></a><span data-ttu-id="ac2dd-319">최신 버전으로 업데이트</span><span class="sxs-lookup"><span data-stu-id="ac2dd-319">Update to the latest version</span></span>

<span data-ttu-id="ac2dd-320">게이트웨이 버전이 오래되면 여러 가지 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-320">Many issues can surface when the gateway version becomes outdated.</span></span> <span data-ttu-id="ac2dd-321">일반적으로는 최신 버전을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-321">As good general practice, make sure that you use the latest version.</span></span> <span data-ttu-id="ac2dd-322">한 달 동안 게이트웨이를 업데이트하지 않은 경우 최신 버전의 게이트웨이를 설치하고 문제가 재현되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-322">If you haven't updated the gateway for a month or longer, you might consider installing the latest version of the gateway, and see if you can reproduce the issue.</span></span>

### <a name="error-failed-to-add-user-to-group--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="ac2dd-323">오류: 그룹에 사용자를 추가하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-323">Error: Failed to add user to group.</span></span> <span data-ttu-id="ac2dd-324">(-2147463168 PBIEgwService 성능 로그 사용자)</span><span class="sxs-lookup"><span data-stu-id="ac2dd-324">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="ac2dd-325">지원되지 않는 도메인 컨트롤러에 게이트웨이 설치하려고 하면 이 오류가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-325">You might get this error if you try to install the gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="ac2dd-326">도메인 컨트롤러가 아닌 컴퓨터에 게이트웨이를 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-326">Make sure that you deploy the gateway on a machine that isn't a domain controller.</span></span>

## <a name="tools"></a><span data-ttu-id="ac2dd-327">도구</span><span class="sxs-lookup"><span data-stu-id="ac2dd-327">Tools</span></span>

### <a name="collect-logs-from-the-gateway-configurer"></a><span data-ttu-id="ac2dd-328">게이트웨이 구성기에서 로그 수집</span><span class="sxs-lookup"><span data-stu-id="ac2dd-328">Collect logs from the gateway configurer</span></span>

<span data-ttu-id="ac2dd-329">게이트웨이에 대한 여러 로그를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-329">You can collect several logs for the gateway.</span></span> <span data-ttu-id="ac2dd-330">항상 로그부터 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-330">Always start with the logs!</span></span>

#### <a name="installer-logs"></a><span data-ttu-id="ac2dd-331">설치 관리자 로그</span><span class="sxs-lookup"><span data-stu-id="ac2dd-331">Installer logs</span></span>

`%localappdata%\Temp\Power_BI_Gateway_–Enterprise.log`

#### <a name="configuration-logs"></a><span data-ttu-id="ac2dd-332">구성 로그</span><span class="sxs-lookup"><span data-stu-id="ac2dd-332">Configuration logs</span></span>

`%localappdata%\Microsoft\Power BI Enterprise Gateway\GatewayConfigurator.log`

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="ac2dd-333">엔터프라이즈 게이트웨이 서비스 로그</span><span class="sxs-lookup"><span data-stu-id="ac2dd-333">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\Power BI Enterprise Gateway\EnterpriseGateway.log`

#### <a name="event-logs"></a><span data-ttu-id="ac2dd-334">이벤트 로그</span><span class="sxs-lookup"><span data-stu-id="ac2dd-334">Event logs</span></span>

<span data-ttu-id="ac2dd-335">데이터 관리 게이트웨이 및 PowerBIGateway 로그를 **응용 프로그램 및 서비스 로그** 아래에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-335">You can find the Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>

### <a name="fiddler-trace"></a><span data-ttu-id="ac2dd-336">Fiddler 추적</span><span class="sxs-lookup"><span data-stu-id="ac2dd-336">Fiddler Trace</span></span>

<span data-ttu-id="ac2dd-337">[Fiddler](http://www.telerik.com/fiddler) 는 HTTP 트래픽을 모니터링하는 Telerik의 무료 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-337">[Fiddler](http://www.telerik.com/fiddler) is a free tool from Telerik that monitors HTTP traffic.</span></span> <span data-ttu-id="ac2dd-338">클라이언트 컴퓨터에서 Power BI를 사용하여 트래픽을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-338">You can see this traffic with the Power BI service from the client machine.</span></span> <span data-ttu-id="ac2dd-339">이 서비스는 오류 및 기타 관련된 정보를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2dd-339">This service might show errors and other related information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac2dd-340">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ac2dd-340">Next steps</span></span>
    
* [<span data-ttu-id="ac2dd-341">논리 앱에서 온-프레미스 데이터에 연결</span><span class="sxs-lookup"><span data-stu-id="ac2dd-341">Connect to on-premises data from logic apps</span></span>](../logic-apps/logic-apps-gateway-connection.md)
* [<span data-ttu-id="ac2dd-342">엔터프라이즈 통합 기능</span><span class="sxs-lookup"><span data-stu-id="ac2dd-342">Enterprise integration features</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="ac2dd-343">Azure Logic Apps용 커넥터</span><span class="sxs-lookup"><span data-stu-id="ac2dd-343">Connectors for Azure Logic Apps</span></span>](../connectors/apis-list.md)
