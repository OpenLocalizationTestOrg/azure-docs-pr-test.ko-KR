---
title: "자습서: Azure BizTalk 서비스를 사용하여 EDIFACT 송장 처리 | Microsoft Docs"
description: "Box 커넥터 또는 API 앱을 만들어서 구성하고 Azure 앱 서비스의 논리 앱에서 사용하는 방법"
services: biztalk-services
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
ms.assetid: 7e0b93fa-3e2b-4a9c-89ef-abf1d3aa8fa9
ms.service: biztalk-services
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/31/2016
ms.author: deonhe
ms.openlocfilehash: 4597ee28e4c3b797c0ab050b21a126a95d9e8191
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-process-edifact-invoices-using-azure-biztalk-services"></a><span data-ttu-id="0cf51-103">자습서: Azure BizTalk 서비스를 사용하여 EDIFACT 송장 처리</span><span class="sxs-lookup"><span data-stu-id="0cf51-103">Tutorial: Process EDIFACT invoices using Azure BizTalk Services</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="0cf51-104">BizTalk 서비스 포털을 사용하여 X12 및 EDIFACT 규약을 구성 및 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-104">You can use the BizTalk Services Portal to configure and deploy X12 and EDIFACT agreements.</span></span> <span data-ttu-id="0cf51-105">이 자습서에서는 거래 파트너 간에 송장 교환을 위해 EDIFACT 규약을 만드는 방법에 대해 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-105">In this tutorial, we look at how to create an EDIFACT agreement for exchanging invoices between trading partners.</span></span> <span data-ttu-id="0cf51-106">이 자습서는 EDIFACT 메시지를 교환하는 두 거래 업체 Northwind와 Contoso를 포함하는 종단 간 비즈니스 솔루션에 대해 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-106">This tutorial is written around an end-to-end business solution involving two trading partners, Northwind and Contoso that exchange EDIFACT messages.</span></span>  

## <a name="sample-based-on-this-tutorial"></a><span data-ttu-id="0cf51-107">이 자습서를 기반으로 하는 샘플</span><span class="sxs-lookup"><span data-stu-id="0cf51-107">Sample based on this tutorial</span></span>
<span data-ttu-id="0cf51-108">이 자습서는 **MSDN 코드 갤러리**에서 다운로드 가능한 샘플 [BizTalk 서비스를 사용하여 EDIFACT 송장 전송](http://go.microsoft.com/fwlink/?LinkId=401005)에 대해 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-108">This tutorial is written around a sample, **Sending EDIFACT Invoices Using BizTalk Services**, which is available to download from the [MSDN Code Gallery](http://go.microsoft.com/fwlink/?LinkId=401005).</span></span> <span data-ttu-id="0cf51-109">샘플을 사용하고 이 자습서를 진행하여 샘플이 빌드된 방식을 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-109">You could use the sample and go through this tutorial to understand how the sample was built.</span></span> <span data-ttu-id="0cf51-110">또는 이 자습서를 사용하여 사용자 고유의 솔루션 처음부터 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-110">Or, you could use this tutorial to create your own solution ground-up.</span></span> <span data-ttu-id="0cf51-111">이 자습서는 이 솔루션이 빌드된 방식을 이해할 수 있도록 두 번째 접근 방식을 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-111">This tutorial is targeted towards the second approach so that you understand how this solution was built.</span></span> <span data-ttu-id="0cf51-112">또한 가능한 만큼 자습서는 샘플과 일치하고 샘플에 사용된 것과 동일한 아티팩트에 대한 이름(예: 스키마, 변환)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-112">Also, as much as possible, the tutorial is consistent with the sample and uses the same names for artifacts (for example, schemas, transforms) as used in the sample.</span></span>  

> [!NOTE]
> <span data-ttu-id="0cf51-113">이 솔루션은 EAI 브리지에서 EDI 브리지로 메시지 전송을 포함하므로 [BizTalk 서비스 브리지 연결 샘플](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104) 샘플을 다시 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-113">Because this solution involves sending a message from an EAI bridge to an EDI bridge, it reuses the [BizTalk Services Bridge chaining sample](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104) sample.</span></span>  
> 
> 

## <a name="what-does-the-solution-do"></a><span data-ttu-id="0cf51-114">솔루션의 기능은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="0cf51-114">What does the solution do?</span></span>
<span data-ttu-id="0cf51-115">이 솔루션에서 Northwind는 Contoso에서 EDIFACT 송장을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-115">In this solution, Northwind receives EDIFACT invoices from Contoso.</span></span> <span data-ttu-id="0cf51-116">이 송장은 표준 EDI 형식이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-116">These invoices are not in a standard EDI format.</span></span> <span data-ttu-id="0cf51-117">따라서 Northwind로 송장을 보내기 전에 EDIFACT 송장(INVOIC이라고도 함) 문서로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-117">So, before sending the invoice to Northwind, it must be transformed to an EDIFACT invoice (also called INVOIC) document.</span></span> <span data-ttu-id="0cf51-118">수신 시 Northwind는 EDIFACT 송장을 처리하고 Contoso에 제어 메시지(CONTRL이라고도 함)를 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-118">On receipt, Northwind must process the EDIFACT invoice, and return a control message (also called CONTRL) to Contoso.</span></span>

![][1]  

<span data-ttu-id="0cf51-119">이 비즈니스 시나리오를 획득하기 위해 Contoso는 Microsoft Azure BizTalk 서비스와 함께 제공되는 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-119">To achieve this business scenario, Contoso uses the features provided with Microsoft Azure BizTalk Services.</span></span>

* <span data-ttu-id="0cf51-120">Contoso는 EAI 브리지를 사용하여 원래 송장을 EDIFACT INVOIC으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-120">Contoso uses EAI bridges to transform the original invoice to EDIFACT INVOIC.</span></span>
* <span data-ttu-id="0cf51-121">그런 다음 EAI 브리지는 BizTalk 서비스 포털에서 구성된 규약의 일부분으로 배포된 EDI 송신 브리지에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-121">The EAI bridge then sends the message to an EDI send bridge deployed as part of an agreement configured in the BizTalk Services Portal.</span></span>
* <span data-ttu-id="0cf51-122">EDI 송신 브리지는 EDIFACT INVOIC을 처리하고 Northwind로 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-122">The EDI send bridge processes the EDIFACT INVOIC and routes it to Northwind.</span></span>
* <span data-ttu-id="0cf51-123">송장을 받은 후 Northwind는 규약의 일부로 배포된 EDI 수신 브리지에 CONTRL 메시지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-123">After receiving the invoice, Northwind returns a CONTRL message to the EDI receive bridge deployed as part of the agreement.</span></span>  

> [!NOTE]
> <span data-ttu-id="0cf51-124">필요에 따라 이 솔루션은 일괄 처리를 사용하여 각 송장을 별도로 보내지 않고 일괄 처리로 송장을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-124">Optionally, this solution also demonstrates how to use batching to send the invoices in batches, instead of sending each invoice separately.</span></span>  
> 
> 

<span data-ttu-id="0cf51-125">시나리오를 완료하려면 서비스 버스 큐를 사용하여 Contoso에서 Northwind로 송장을 보내거나 Northwind로부터 승인을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-125">To complete the scenario, we use Service Bus queues to send invoice from Contoso to Northwind or receive acknowledgement from Northwind.</span></span> <span data-ttu-id="0cf51-126">이러한 큐는 다운로드로 제공되며 이 자습서의 일부로 사용 가능한 샘플 패키지에 포함된 클라이언트 응용 프로그램을 사용하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-126">These queues can be created using a client application, which is available as a download and is included in the sample package that is available as part of this tutorial.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="0cf51-127">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0cf51-127">Prerequisites</span></span>
* <span data-ttu-id="0cf51-128">서비스 버스 네임스페이스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-128">You must have a Service Bus namespace.</span></span> <span data-ttu-id="0cf51-129">네임스페이스를 만드는 방법에 대한 지침은 [방법: 서비스 버스 서비스 네임스페이스 만들기 또는 수정](https://msdn.microsoft.com/library/azure/hh674478.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cf51-129">For instructions on creating a namespace, see [How To: Create or Modify a Service Bus Service Namespace](https://msdn.microsoft.com/library/azure/hh674478.aspx).</span></span> <span data-ttu-id="0cf51-130">**edifactbts**라는 프로비전된 서비스 버스 네임스페이스가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-130">Let us assume that you already have a Service Bus namespace provisioned, called **edifactbts**.</span></span>
* <span data-ttu-id="0cf51-131">BizTalk 서비스 구독이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-131">You must have a BizTalk Services subscription.</span></span> <span data-ttu-id="0cf51-132">자세한 내용은 [Azure 클래식 포털을 사용하여 BizTalk 서비스 만들기](http://go.microsoft.com/fwlink/?LinkID=302280)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cf51-132">For instructions, see [Create a BizTalk Service using Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=302280).</span></span> <span data-ttu-id="0cf51-133">이 자습서의 경우 **contosowabs**라는 BizTalk 서비스 구독을 보유했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-133">For this tutorial, let us assume you have a BizTalk Services subscription, called **contosowabs**.</span></span>
* <span data-ttu-id="0cf51-134">BizTalk 서비스 포털에서 BizTalk 서비스 구독을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-134">Register your BizTalk Services subscription on the BizTalk Services Portal.</span></span> <span data-ttu-id="0cf51-135">자세한 내용은 [BizTalk 서비스 포털에서 BizTalk 서비스 배포 등록](https://msdn.microsoft.com/library/hh689837.aspx)</span><span class="sxs-lookup"><span data-stu-id="0cf51-135">For instructions, see [Registering a BizTalk Service Deployment on the BizTalk Services Portal](https://msdn.microsoft.com/library/hh689837.aspx)</span></span>
* <span data-ttu-id="0cf51-136">Visual Studio가 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-136">You must have Visual Studio installed.</span></span>
* <span data-ttu-id="0cf51-137">BizTalk 서비스 SDK가 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-137">You must have BizTalk Services SDK installed.</span></span> <span data-ttu-id="0cf51-138">[http://go.microsoft.com/fwlink/?LinkId=235057](http://go.microsoft.com/fwlink/?LinkId=235057)</span><span class="sxs-lookup"><span data-stu-id="0cf51-138">You can download the SDK from [http://go.microsoft.com/fwlink/?LinkId=235057](http://go.microsoft.com/fwlink/?LinkId=235057)</span></span>  

## <a name="step-1-create-the-service-bus-queues"></a><span data-ttu-id="0cf51-139">1단계: 서비스 버스 큐 만들기</span><span class="sxs-lookup"><span data-stu-id="0cf51-139">Step 1: Create the Service Bus queues</span></span>
<span data-ttu-id="0cf51-140">이 솔루션에서는 서비스 버스 큐를 사용하여 거래 업체 간에 메시지를 교환합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-140">This solution uses Service Bus queues to exchange messages between trading partners.</span></span> <span data-ttu-id="0cf51-141">Contoso와 Northwind는 EAI 및/또는 EDI 브리지를 사용할 위치에서 큐에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-141">Contoso and Northwind send messages to the queues from where the EAI and/or EDI bridges consume them.</span></span> <span data-ttu-id="0cf51-142">이 솔루션에서는 세 개의 서비스 버스 큐가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-142">For this solution, you need three Service Bus queues:</span></span>

* <span data-ttu-id="0cf51-143">**northwindreceive** – Northwind는 이 큐를 통해 Contoso에서 송장을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-143">**northwindreceive** – Northwind receives the invoice from Contoso over this queue.</span></span>
* <span data-ttu-id="0cf51-144">**contosoreceive** – Contoso는 이 큐를 통해 Northwind로부터 승인을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-144">**contosoreceive** – Contoso receives the acknowledgement from Northwind over this queue.</span></span>
* <span data-ttu-id="0cf51-145">**일시 중단** – 모든 일시 중단된 메시지가 이 큐에 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-145">**suspended** – All suspended messages are routed to this queue.</span></span> <span data-ttu-id="0cf51-146">처리 중 실패하는 경우 메시지는 일시 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-146">Messages are suspended if they fail during processing.</span></span>

<span data-ttu-id="0cf51-147">샘플 패키지에 포함된 클라이언트 응용 프로그램을 사용하여 이러한 서비스 버스 큐를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-147">You can create these Service Bus queues by using a client application included in the sample package.</span></span>  

1. <span data-ttu-id="0cf51-148">샘플을 다운로드한 위치에서 **자습서: BizTalk 서비스 EDI Bridges.sln을 사용하여 송장 전송**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-148">From the location where you downloaded the sample, open **Tutorial Sending Invoices Using BizTalk Services EDI Bridges.sln**.</span></span>
2. <span data-ttu-id="0cf51-149">**F5** 키를 눌러 빌드하고 **자습서 클라이언트** 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-149">Press **F5** to build and start the **Tutorial Client** application.</span></span>
3. <span data-ttu-id="0cf51-150">화면에서 서비스 버스 ACS 네임스페이스, 발급자 이름 및 발급자 키를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-150">In the screen, enter the Service Bus ACS namespace, issuer name, and issuer key.</span></span>
   
   ![][2]  
4. <span data-ttu-id="0cf51-151">서비스 버스 네임스페이스에서 세 개의 큐가 만들어진다는 메시지 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-151">A message box prompts that three queues will be created in your Service Bus namespace.</span></span> <span data-ttu-id="0cf51-152">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-152">Click **OK**.</span></span>
5. <span data-ttu-id="0cf51-153">자습서 클라이언트를 실행 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-153">Leave the Tutorial Client running.</span></span> <span data-ttu-id="0cf51-154">열고 **서비스 버스** > ***서비스 버스 네임스페이스*** > **큐**를 클릭하고 세 개의 큐가 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-154">Open the , click **Service Bus** > ***your Service Bus namespace*** > **Queues**, and verify that the three queues are created.</span></span>  

## <a name="step-2-create-and-deploy-trading-partner-agreement"></a><span data-ttu-id="0cf51-155">2단계: 거래 업체 규약 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="0cf51-155">Step 2: Create and deploy trading partner agreement</span></span>
<span data-ttu-id="0cf51-156">Contoso와 Northwind 간의 거래 업체 규약을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-156">Create a trading partner agreement between Contoso and Northwind.</span></span> <span data-ttu-id="0cf51-157">거래 업체 규약은 사용할 메시지 스키마, 사용할 메시징 프로토콜 등과 같은 두 비즈니스 파트너 간의 거래 규약을 정의합니다. 거래 업체 규약은 거래 업체에 메시지를 보내는 브리지(**EDI 송신 브리지**)와 거래 업체로부터 메시지를 수신하는 브리지(**EDI 수신 브리지**)의 두 개의 EDI 브리지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-157">A trading partner agreement defines a trade contract between the two business partners, such as which message schema to use, which messaging protocol to use, etc. A trading partner agreement includes two EDI bridges, one to send messages to trading partners (called the **EDI Send bridge**) and one to receive messages from trading partners (called the **EDI Receive bridge**).</span></span>

<span data-ttu-id="0cf51-158">이 솔루션의 컨텍스트에서 규약의 송신 측에 해당하는 EDI 송신 브리지는 Contoso에서 Northwind로 EDIFACT 송장을 보내는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-158">In the context of this solution, the EDI send bridge corresponds to the send-side of the agreement and is used to send the EDIFACT invoice from Contoso to Northwind.</span></span> <span data-ttu-id="0cf51-159">마찬가지로 규약의 수신 측에 해당하는 EDI 수신 브리지는 Northwind로부터 승인을 받는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-159">Similarly, the EDI receive bridge corresponds to the receive-side of the agreement and is used to receive acknowledgements from Northwind.</span></span>  

### <a name="create-the-trading-partners"></a><span data-ttu-id="0cf51-160">거래 업체 만들기</span><span class="sxs-lookup"><span data-stu-id="0cf51-160">Create the trading partners</span></span>
<span data-ttu-id="0cf51-161">먼저 Contoso와 Northwind에 대한 거래 업체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-161">To start with, create trading partners for Contoso and Northwind.</span></span>  

1. <span data-ttu-id="0cf51-162">BizTalk 서비스 포털의 **파트너** 탭에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-162">In the BizTalk Services Portal, on the **Partners** tab, click **Add**.</span></span>
2. <span data-ttu-id="0cf51-163">새 파트너 페이지에서 파트너 이름으로 **Contoso**를 입력한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-163">In the New partner page, enter **Contoso** as a partner name, and then click **Save**.</span></span>
3. <span data-ttu-id="0cf51-164">두 번째 파트너, **Northwind**를 만드는 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-164">Repeat the step to create the second partner, **Northwind**.</span></span>  

### <a name="create-the-agreement"></a><span data-ttu-id="0cf51-165">규약 만들기</span><span class="sxs-lookup"><span data-stu-id="0cf51-165">Create the agreement</span></span>
<span data-ttu-id="0cf51-166">거래 업체 규약은 거래 업체의 비즈니스 프로필 간에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-166">Trading partner agreements are created between business profiles of trading partners.</span></span> <span data-ttu-id="0cf51-167">이 솔루션에서는 파트너를 만들 때 자동으로 만들어지는 기본 파트너 프로필을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-167">This solution uses the default partner profiles that are automatically created when we created the partners.</span></span>  

1. <span data-ttu-id="0cf51-168">BizTalk 서비스 포털에서 **규약** > **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-168">In the BizTalk Services Portal, click **Agreements** > **Add**.</span></span>
2. <span data-ttu-id="0cf51-169">새 규약의 **일반 설정** 페이지에서 아래 이미지에 표시된 값을 지정한 다음 **계속**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-169">In the new agreement’s **General Settings** page, specify the values as shown in the image below, and then click **Continue**.</span></span>
   
   ![][3]  
   
   <span data-ttu-id="0cf51-170">**계속**을 클릭하면 두 개의 탭 **수신 설정** 및 **송신 설정**을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-170">After you click **Continue**, two tabs, **Receive Settings** and **Send Settings** become available.</span></span>
3. <span data-ttu-id="0cf51-171">Contoso와 Northwind 간의 규약을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-171">Create the send agreement between Contoso and Northwind.</span></span> <span data-ttu-id="0cf51-172">이 규약은 Contoso에서 Northwind로 EDIFACT 송장을 보내는 방법을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-172">This agreement governs how Contoso sends the EDIFACT invoice to Northwind.</span></span>
   
   1. <span data-ttu-id="0cf51-173">**송신 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-173">Click **Send Settings**.</span></span>
   2. <span data-ttu-id="0cf51-174">**인바운드 URL**, **변환** 및 **일괄 처리** 탭의 기본값을 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-174">Retain the default values on the **Inbound URL**, **Transform**, and **Batching** tabs.</span></span>
   3. <span data-ttu-id="0cf51-175">**스키마** 섹션 아래의 **프로토콜** 탭에서 **EFACT_D93A_INVOIC.xsd** 스키마를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-175">On the **Protocol** tab, under the **Schemas** section, upload the **EFACT_D93A_INVOIC.xsd** schema.</span></span> <span data-ttu-id="0cf51-176">이 스키마는 샘플 패키지와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-176">This schema is available with the sample package.</span></span>
      
      ![][4]  
   4. <span data-ttu-id="0cf51-177">**전송** 탭에서 서비스 버스 큐에 대한 세부 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-177">On the **Transport** tab, specify the details for the Service Bus queues.</span></span> <span data-ttu-id="0cf51-178">송신 측 규약의 경우 **northwindreceive** 큐를 사용하여 Northwind에 EDIFACT 송장을 보내고 **일시 중단** 큐를 사용하여 처리하는 동안 실패 및 일시 중단된 모든 메시지를 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-178">For the send-side agreement, we use the **northwindreceive** queue to send the EDIFACT invoice to Northwind, and the **suspended** queue to route any messages that fail during processing and are suspended.</span></span> <span data-ttu-id="0cf51-179">이 항목의 **1단계: 서비스 버스 큐 만들기** 에서 해당 큐를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-179">You created these queues in **Step 1: Create the Service Bus queues** (in this topic).</span></span>
      
      ![][5]  
      
      <span data-ttu-id="0cf51-180">**전송 설정 > 전송 유형** 및 **메시지 일시 중지 설정 > 전송 유형** 아래에서 Azure 서비스 버스를 선택하고 이미지에 표시된 대로 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-180">Under **Transport Settings > Transport type** and **Message Suspension Settings > Transport type**, select Azure Service Bus and provide the values as shown in the image.</span></span>
4. <span data-ttu-id="0cf51-181">Contoso와 Northwind 간의 수신 규약을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-181">Create the receive agreement between Contoso and Northwind.</span></span> <span data-ttu-id="0cf51-182">이 규약은 Contoso가 Northwind로부터 승인을 받는 방법을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-182">This agreement governs how Contoso receives the acknowledgement from Northwind.</span></span>
   
   1. <span data-ttu-id="0cf51-183">**수신 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-183">Click **Receive Settings**.</span></span>
   2. <span data-ttu-id="0cf51-184">**전송** 및 **변환** 탭의 기본값을 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-184">Retain the default values on the **Transport** and **Transform** tabs.</span></span>
   3. <span data-ttu-id="0cf51-185">**스키마** 섹션 아래의 **프로토콜** 탭에서 **EFACT_4.1_CONTRL.xsd** 스키마를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-185">On the **Protocol** tab, under the **Schemas** section, upload the **EFACT_4.1_CONTRL.xsd** schema.</span></span> <span data-ttu-id="0cf51-186">이 스키마는 샘플 패키지와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-186">This schema is available with the sample package.</span></span>
   4. <span data-ttu-id="0cf51-187">**경로** 탭에서 northwind에서의 승인만 Contoso로 라우팅되도록 하는 필터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-187">On the **Route** tab, create a filter to ensure that only acknowledgements from Northwind are routed to Contoso.</span></span> <span data-ttu-id="0cf51-188">**경로 설정** 아래에서 **추가**를 클릭하여 라우팅 필터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-188">Under **Route Settings**, click **Add** to create the routing filter.</span></span>
      
      ![][6]  
      
      1. <span data-ttu-id="0cf51-189">이미지와 같이 **규칙 이름**, **경로 규칙** 및 **경로 대상**에 대한 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-189">Provide values for **Rule Name**, **Route rule**, and **Route destination** as shown in the image.</span></span>
      2. <span data-ttu-id="0cf51-190">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-190">Click **Save**.</span></span>
   5. <span data-ttu-id="0cf51-191">**경로** 탭에서 일시 중단된 승인(처리 중 실패한 승인)이 라우팅될 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-191">On the **Route** tab again, specify where suspended acknowledgements (acknowledgements that fail during processing) are routed to.</span></span> <span data-ttu-id="0cf51-192">Azure 서비스 버스에 대한 전송 방식, **큐**에 대한 라우팅 대상 유형, **공유 액세스 서명**(SAS)에 대한 인증 유형을 설정하고 서비스 버스 네임스페이스에 대한 SAS 연결 문자열을 제공한 다음 **일시 중단됨**으로 큐 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-192">Set the transport type to Azure Service Bus, route destination type to **Queue**, authentication type to **Shared Access Signature** (SAS), provide the SAS connection string for the Service Bus namespace, and then enter the queue name as **suspended**.</span></span>
5. <span data-ttu-id="0cf51-193">마지막으로 **배포** 를 클릭하여 규약을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-193">Finally, click **Deploy** to deploy the agreement.</span></span> <span data-ttu-id="0cf51-194">송신 및 수신 규약이 배포되는 끝점을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-194">Note the endpoints where the send and receive agreements get deployed.</span></span>
   
   * <span data-ttu-id="0cf51-195">**인바운드 URL** 아래의 **송신 설정** 탭에서 끝점을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="0cf51-195">On the **Send Settings** tab, under **Inbound URL**, note the endpoint.</span></span> <span data-ttu-id="0cf51-196">EDI 송신 브리지를 사용하여 Contoso에서 Northwind로 메시지를 보내려면 이 끝점에 메시지를 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-196">To send a message from Contoso to Northwind using the EDI send bridge, you must send a message to this endpoint.</span></span>
   * <span data-ttu-id="0cf51-197">**전송** 아래의 **수신 설정** 탭에서 끝점을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="0cf51-197">On the **Receive Settings** tab, under **Transport**, note the endpoint.</span></span> <span data-ttu-id="0cf51-198">EDI 수신 브리지를 사용하여 Northwind에서 Contoso로 메시지를 보내려면 이 끝점에 메시지를 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-198">To send a message from Northwind to Contoso using the EDI receive bridge, you must send a message to this endpoint.</span></span>  

## <a name="step-3-create-and-deploy-the-biztalk-services-project"></a><span data-ttu-id="0cf51-199">3단계: BizTalk 서비스 프로젝트 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="0cf51-199">Step 3: Create and deploy the BizTalk Services project</span></span>
<span data-ttu-id="0cf51-200">이전 단계에서 EDIFACT 송장 및 승인을 처리하도록 EDI 송신 및 수신 규약을 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-200">In the previous step, you deployed the EDI send and receive agreements to process EDIFACT invoices and acknowledgements.</span></span> <span data-ttu-id="0cf51-201">이러한 규약은 표준 EDIFACT 메시지 스키마를 준수하는 메시지만을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-201">These agreements can only process messages that conform to the standard EDIFACT message schema.</span></span> <span data-ttu-id="0cf51-202">그러나 이 솔루션에 대한 시나리오마다 Contoso는 내부 소유 스키마로 Northwind에 송장을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-202">However, per the scenario for this solution, Contoso sends an invoice to Northwind in an in-house proprietary schema.</span></span> <span data-ttu-id="0cf51-203">따라서 메시지가 EDI 송신 브리지에 전송되기 전에 내부 스키마에서 표준 EDIFACT 송장 스키마로 변환되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-203">So, before the message is sent to the EDI send bridge, it must be transformed from the in-house schema to the standard EDIFACT invoice schema.</span></span> <span data-ttu-id="0cf51-204">BizTalk 서비스 EAI 프로젝트는 그렇게 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-204">The BizTalk Services EAI project does that.</span></span>

<span data-ttu-id="0cf51-205">메시지를 변환하는 BizTalk 서비스 프로젝트, **InvoiceProcessingBridge**는 다운로드한 샘플의 일부로 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-205">The BizTalk Services project, **InvoiceProcessingBridge**, that transforms the message is also included as part of the sample you downloaded.</span></span> <span data-ttu-id="0cf51-206">프로젝트는 다음 아티팩트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-206">The project includes the following artifacts:</span></span>

* <span data-ttu-id="0cf51-207">**INHOUSEINVOICE.XSD** – Northwind로 전송되는 내부 송장 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-207">**INHOUSEINVOICE.XSD** – Schema of the in-house invoice that is sent to Northwind.</span></span>
* <span data-ttu-id="0cf51-208">**EFACT_D93A_INVOIC.XSD** – 표준 EDIFACT 송장 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-208">**EFACT_D93A_INVOIC.XSD** – Schema of the standard EDIFACT invoice.</span></span>
* <span data-ttu-id="0cf51-209">**EFACT_4.1_CONTRL.XSD** – Northwind가 Contoso에 보내는 EDIFACT 승인 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-209">**EFACT_4.1_CONTRL.XSD** – Schema of the EDIFACT acknowledgement that Northwind sends to Contoso.</span></span>
* <span data-ttu-id="0cf51-210">**INHOUSEINVOICE_to_D93AINVOIC.TRFM** – 내부 송장 스키마를 표준 EDIFACT 송장 스키마에 매핑하는 변환입니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-210">**INHOUSEINVOICE_to_D93AINVOIC.TRFM** – The transform that maps the in-house invoice schema to the standard EDIFACT invoice schema.</span></span>  

### <a name="create-the-biztalk-services-project"></a><span data-ttu-id="0cf51-211">BizTalk 서비스 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="0cf51-211">Create the BizTalk Services project</span></span>
1. <span data-ttu-id="0cf51-212">Visual Studio 솔루션에서 InvoiceProcessingBridge 프로젝트를 확장한 다음 **MessageFlowItinerary.bcs** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-212">In the Visual Studio solution, expand the InvoiceProcessingBridge project, and then open the **MessageFlowItinerary.bcs** file.</span></span>
2. <span data-ttu-id="0cf51-213">캔버스에서 아무 곳이나 클릭하고 속성 상자에서 **BizTalk 서비스 URL** 을 설정하여 BizTalk 서비스 구독 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-213">Click anywhere on the canvas and set the **BizTalk Service URL** in the property box to specify your BizTalk Services subscription name.</span></span> <span data-ttu-id="0cf51-214">예: `https://contosowabs.biztalk.windows.net`</span><span class="sxs-lookup"><span data-stu-id="0cf51-214">For example, `https://contosowabs.biztalk.windows.net`.</span></span>
   
   ![][7]  
3. <span data-ttu-id="0cf51-215">도구 상자에서 **Xml 단방향 브리지** 를 캔버스로 끌어서 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-215">From the toolbox, drag an **Xml One-Way Bridge** to the canvas.</span></span> <span data-ttu-id="0cf51-216">브리지의 **엔터티 이름** 및 **상대 주소** 속성을 **ProcessInvoiceBridge**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-216">Set the **Entity Name** and **Relative Address** properties of the bridge to **ProcessInvoiceBridge**.</span></span> <span data-ttu-id="0cf51-217">**ProcessInvoiceBridge** 를 두 번 클릭하여 브리지 구성 화면을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-217">Double-click **ProcessInvoiceBridge** to open the bridge configuration surface.</span></span>
4. <span data-ttu-id="0cf51-218">**메시지 유형** 상자 내에서 더하기(**+**) 단추를 클릭하여 들어오는 메시지의 스키마를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-218">Within the **Message Types** box, click the plus (**+**) button to specify the schema of the incoming message.</span></span> <span data-ttu-id="0cf51-219">EAI 브리지에 대해 들어오는 메시지는 항상 내부 송장이므로 **INHOUSEINVOICE**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-219">Because the incoming message for the EAI bridge is always the in-house invoice, set this to **INHOUSEINVOICE**.</span></span>
   
   ![][8]  
5. <span data-ttu-id="0cf51-220">**Xml 변환** 셰이프를 클릭하고 속성 상자에서 **맵** 속성에 대해 줄임표(**...**) 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-220">Click the **Xml Transform** shape, and in the property box, for the **Maps** property, click the ellipsis (**...**) button.</span></span> <span data-ttu-id="0cf51-221">**맵 선택** 대화 상자에서 **INHOUSEINVOICE_to_D93AINVOIC** 변환 파일을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-221">In the **Maps Selection** dialog box, select the **INHOUSEINVOICE_to_D93AINVOIC** transform file, and then click **OK**.</span></span>
   
   ![][9]  
6. <span data-ttu-id="0cf51-222">**MessageFlowItinerary.bcs**로 돌아가고 도구 상자에서 **양방향 외부 서비스 끝점**을 **ProcessInvoiceBridge**의 오른쪽으로 끌어서 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-222">Go back to **MessageFlowItinerary.bcs**, and from the toolbox, drag a **Two-Way External Service Endpoint** to the right of the **ProcessInvoiceBridge**.</span></span> <span data-ttu-id="0cf51-223">해당 **엔터티 이름** 속성을 **EDIBridge**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-223">Set its **Entity Name** property to **EDIBridge**.</span></span>
7. <span data-ttu-id="0cf51-224">솔루션 탐색기에서 **MessageFlowItinerary.bcs**를 확장하고 **EDIBridge.config** 파일을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-224">In the Solution Explorer, expand the **MessageFlowItinerary.bcs** and double-click the **EDIBridge.config** file.</span></span> <span data-ttu-id="0cf51-225">**EDIBridge.config** 의 내용을 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-225">Replace the content of the **EDIBridge.config** with the following.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0cf51-226">.config 파일을 편집해야 하는 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="0cf51-226">Why do I need to edit the .config file?</span></span> <span data-ttu-id="0cf51-227">브리지 디자이너 캔버스에 추가한 외부 서비스 끝점은 이전에 배포한 EDI 브리지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-227">The external service endpoint that we added to the bridge designer canvas represents the EDI bridges that we deployed earlier.</span></span> <span data-ttu-id="0cf51-228">EDI 브리지는 양방향 브리지이며 송신 측과 수신 측이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-228">EDI bridges are two-way bridges, with a send and receive side.</span></span> <span data-ttu-id="0cf51-229">그러나 브리지 디자이너에 추가한 EAI 브리지는 단방향 브리지입니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-229">However, the EAI bridge that we added to the bridge designer is a one-way bridge.</span></span> <span data-ttu-id="0cf51-230">그러므로 두 브리지의 서로 다른 메시지 교환 패턴을 처리하기 위해 .config 파일에 해당 구성을 포함하여 사용자 지정 브리지 동작을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-230">So, to handle the different message exchange patterns of the two bridges, we use a custom bridge behavior by including its configuration in the .config file.</span></span> <span data-ttu-id="0cf51-231">또한 사용자 지정 동작은 또한 EDI 송신 브리지 끝점에 대한 인증을 처리합니다. 이 사용자 지정 동작은 [BizTalk 서비스 브리지 연결 샘플 - EAI에서 EDI로](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104)에 별도 샘플로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-231">Additionally, the custom behavior also handles the authentication to the EDI send bridge endpoint.This custom behavior is available as a separate sample at [BizTalk Services Bridge chaining sample - EAI to EDI](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104).</span></span> <span data-ttu-id="0cf51-232">이 솔루션은 샘플을 다시 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-232">This solution reuses the sample.</span></span>  
   > 
   > 
   
   ```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
     <system.serviceModel>
       <extensions>
         <behaviorExtensions>
           <add name="BridgeAuthentication" 
                 type="Microsoft.BizTalk.Bridge.Behaviour.BridgeBehaviorElement, Microsoft.BizTalk.Bridge.Behaviour, Version=1.0.0.0, Culture=neutral, PublicKeyToken=ae58f69b69495c05" />
         </behaviorExtensions>
       </extensions>
       <behaviors>
         <endpointBehaviors>
           <behavior name="BridgeAuthenticationConfiguration">
             <!-- Enter the ACS namespace, issuer name and issuer secret of the BizTalk Services deployment -->
             <BridgeAuthentication acsnamespace="[YOUR ACS NAMESPACE]" 
                                   issuername="owner" 
                                   issuersecret="[YOUR ACS SECRET]" />
             <webHttp />
           </behavior>
         </endpointBehaviors>
       </behaviors>
       <bindings>
         <webHttpBinding>
           <binding name="BridgeBindingConfiguration">
             <security mode="Transport" />
           </binding>
         </webHttpBinding>
       </bindings>
       <client>
         <clear />
         <!--
           Go BizTalk Portal > Agreement > Send Settings > Inbound URL
           Copy the Endpoint URL and paste it in the below address field
         -->
         <endpoint name="TwoWayExternalServiceEndpointReference1" 
                   address="[YOUR EDI BRIDGE SEND URI]" 
                   behaviorConfiguration="BridgeAuthenticationConfiguration" 
                   binding="webHttpBinding" 
                   bindingConfiguration="BridgeBindingConfiguration" 
                   contract="System.ServiceModel.Routing.IRequestReplyRouter" />
       </client>
     </system.serviceModel>
   </configuration>
   
   ```
8. <span data-ttu-id="0cf51-233">구성 세부 정보를 포함하도록 EDIBridge.config 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="0cf51-233">Update the EDIBridge.config file to include configuration details</span></span>
   
   * <span data-ttu-id="0cf51-234">*<behaviors>* 아래에서 BizTalk 서비스 구독에 연결된 ACS 네임스페이스 및 키를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-234">Under *<behaviors>*, provide the ACS namespace and key associated with the BizTalk Services subscription.</span></span>
   * <span data-ttu-id="0cf51-235">*<client>* 아래에서 EDI 송신 규약이 배포되는 끝점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-235">Under *<client>*, provide the endpoint where the EDI send agreement is deployed.</span></span>
   
   <span data-ttu-id="0cf51-236">변경 내용을 저장하고 구성 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-236">Save changes and close the configuration file.</span></span>
9. <span data-ttu-id="0cf51-237">도구 상자에서 **커넥터**를 클릭하고 **ProcessInvoiceBridge**와 **EDIBridge** 구성 요소를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-237">From the Toolbox, click the **Connector** and join the **ProcessInvoiceBridge** and **EDIBridge** components.</span></span> <span data-ttu-id="0cf51-238">커넥터를 선택하고 속성 상자에서 **필터 조건**을 **모두 일치**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-238">Select the connector, and in Properties box, set **Filter Condition** to **Match All**.</span></span> <span data-ttu-id="0cf51-239">이렇게 하면 EAI 브리지에서 처리된 모든 메시지가 EDI 브리지에 라우팅될 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-239">This ensures that all messages processed by the EAI bridge are routed to the EDI bridge.</span></span>
   
   ![][10]  
10. <span data-ttu-id="0cf51-240">솔루션에 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-240">Save changes to the solution.</span></span>  

### <a name="deploy-the-project"></a><span data-ttu-id="0cf51-241">프로젝트 배포</span><span class="sxs-lookup"><span data-stu-id="0cf51-241">Deploy the project</span></span>
1. <span data-ttu-id="0cf51-242">BizTalk 서비스 프로젝트를 만든 컴퓨터에서 BizTalk 서비스 구독에 대한 SSL 인증서를 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-242">On the computer where you created the BizTalk Services project, download and install the SSL certificate for your BizTalk Services subscription.</span></span> <span data-ttu-id="0cf51-243">BizTalk 서비스에서 **대시보드**를 클릭한 다음 **SSL 인증서 다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-243">From , under BizTalk Services, click **Dashboard**, and then click **Download SSL Certificate**.</span></span> <span data-ttu-id="0cf51-244">인증서를 두 번 클릭하고 설치를 완료하라는 프롬프트를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-244">Double-click the certificate and follow the prompt to complete the installation.</span></span> <span data-ttu-id="0cf51-245">**신뢰할 수 있는 루트 인증 기관** 인증서 저장소에 인증서를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-245">Make sure you install the certificate under **Trusted Root Certification Authorities** certificate store.</span></span>
2. <span data-ttu-id="0cf51-246">Visual Studio 솔루션 탐색기에서 **InvoiceProcessingBridge** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-246">In Visual Studio Solution Explorer, right-click the **InvoiceProcessingBridge** project, and then click **Deploy**.</span></span>
3. <span data-ttu-id="0cf51-247">이미지에 표시된 대로 값을 입력한 다음 **배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-247">Provide the values as shown in the image, and then click **Deploy**.</span></span> <span data-ttu-id="0cf51-248">BizTalk 서비스 대시보드에서 **연결 정보** 를 클릭하여 BizTalk 서비스에 대한 ACS 자격 증명을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-248">You can get the ACS credentials for BizTalk Services by clicking **Connection Information** from the BizTalk Services dashboard.</span></span>
   
   ![][11]  
   
   <span data-ttu-id="0cf51-249">출력 창에서 EAI 브리지가 배포되는 끝점(예: `https://contosowabs.biztalk.windows.net/default/ProcessInvoiceBridge`)을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-249">From the output pane, copy the endpoint where the EAI bridge is deployed, for example, `https://contosowabs.biztalk.windows.net/default/ProcessInvoiceBridge`.</span></span> <span data-ttu-id="0cf51-250">이 끝점 URL은 나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-250">You will need this endpoint URL later.</span></span>  

## <a name="step-4-test-the-solution"></a><span data-ttu-id="0cf51-251">4단계: 솔루션 테스트</span><span class="sxs-lookup"><span data-stu-id="0cf51-251">Step 4: Test the solution</span></span>
<span data-ttu-id="0cf51-252">이 항목에서는 샘플의 일부로 제공되는 **자습서 클라이언트** 응용 프로그램을 사용하여 솔루션을 테스트하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-252">In this topic, we look at how to test the solution by using the **Tutorial Client** application provided as part of the sample.</span></span>  

1. <span data-ttu-id="0cf51-253">Visual Studio에서 F5 키를 눌러 **자습서 클라이언트**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-253">In Visual Studio, press F5 to start the **Tutorial Client**.</span></span>
2. <span data-ttu-id="0cf51-254">화면은 서비스 버스 큐를 만든 단계의 미리 채워진 값을 가져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-254">The screen must have the values prepopulated from the step where we created the Service Bus queues.</span></span> <span data-ttu-id="0cf51-255">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-255">Click **Next**.</span></span>
3. <span data-ttu-id="0cf51-256">다음 창에서 BizTalk 서비스 구독에 대한 ACS 자격 증명 및 EAI 및 EDI(수신) 브리지가 배포되는 끝점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-256">In the next window, provide ACS credentials for BizTalk Services subscription, and the endpoints where EAI and EDI (receive) bridges are deployed.</span></span>
   
   <span data-ttu-id="0cf51-257">이전 단계에서 EAI 브리지 끝점을 복사했습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-257">You had copied the EAI bridge endpoint in the previous step.</span></span> <span data-ttu-id="0cf51-258">EDI 수신 브리지 끝점의 경우 BizTalk 서비스 포털에서 규약 > 수신 설정 > 전송 > 끝점으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-258">For EDI receive bridge endpoint, in the BizTalk Services Portal, go to the agreement > Receive Settings > Transport > Endpoint.</span></span>
   
   ![][12]  
4. <span data-ttu-id="0cf51-259">다음 창의 Contoso 아래에서 **내부 송장 보내기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-259">In the next window, under Contoso, click the **Send In-house Invoice** button.</span></span> <span data-ttu-id="0cf51-260">파일 열기 대화 상자에서 INHOUSEINVOICE.txt 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-260">In the File open dialog box, open the INHOUSEINVOICE.txt file.</span></span> <span data-ttu-id="0cf51-261">파일의 내용을 확인한 다음 **확인** 을 클릭하여 송장을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-261">Examine the content of the file and then click **OK** to send the invoice.</span></span>
   
   ![][13]  
5. <span data-ttu-id="0cf51-262">몇 초 후에 Northwind에서 송장을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-262">In a few seconds the invoice is received at Northwind.</span></span> <span data-ttu-id="0cf51-263">**메시지 보기** 링크를 클릭하여 Northwind가 받은 송장을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-263">Click the **View Message** link to see the invoice received by Northwind.</span></span> <span data-ttu-id="0cf51-264">Northwind가 송장을 받은 방식은 표준 EDIFACT 스키마이며 Contoso가 보낸 방식은 내부 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-264">Notice how the invoice received by Northwind is in standard EDIFACT schema while the one sent by Contoso was an in-house schema.</span></span>
   
   ![][14]  
6. <span data-ttu-id="0cf51-265">송장을 선택한 다음 **승인 보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-265">Select the invoice and then click **Send Acknowledgement**.</span></span> <span data-ttu-id="0cf51-266">표시되는 대화 상자에서 교환 ID가 받은 송장과 보낸 승인에서 동일한지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-266">In the dialog box that pops up, notice that the interchange ID is same in the received invoice and the acknowledgement being sent.</span></span> <span data-ttu-id="0cf51-267">**승인 보내기** 대화 상자에서 확인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-267">Click OK in the **Send Acknowledgement** dialog box.</span></span>
   
   ![][15]  
7. <span data-ttu-id="0cf51-268">몇 초 후에 Contoso에서 승인이 성공적으로 수신됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-268">In a few seconds, the acknowledgement is successfully received at Contoso.</span></span>
   
   ![][16]  

## <a name="step-5-optional-send-edifact-invoice-in-batches"></a><span data-ttu-id="0cf51-269">5단계(선택): 일괄 처리로 EDIFACT 송장 보내기</span><span class="sxs-lookup"><span data-stu-id="0cf51-269">Step 5 (optional): Send EDIFACT invoice in batches</span></span>
<span data-ttu-id="0cf51-270">BizTalk 서비스 EDI 브리지는 나가는 메시지의 일괄 처리도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-270">BizTalk Services EDI bridges also supports batching of outgoing messages.</span></span> <span data-ttu-id="0cf51-271">이 기능은 개별 메시지 대신 일괄 처리 메시지(특정 조건 충족) 수신을 선호하는 수신 파트너에게 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-271">This feature is useful for receiving partners that prefer to receive a batch of messages (meeting certain criterion) instead of individual messages.</span></span>

<span data-ttu-id="0cf51-272">일괄 처리로 작업할 때 가장 중요한 부분은 릴리스 조건이라고도 하는 실제 일괄 처리 릴리스입니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-272">The most important aspect when working with batches is the actual release of the batch, also called the release criteria.</span></span> <span data-ttu-id="0cf51-273">릴리스 조건은 수신 파트너가 원하는 메시지를 받는 방식에 따라 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-273">The release criteria can be based on how the receiving partner wants to receive messages.</span></span> <span data-ttu-id="0cf51-274">일괄 처리가 활성화되는 경우 EDI 브리지는 릴리스 조건이 충족될 때까지 수신 파트너에게 나가는 메시지를 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-274">If batching is enabled, the EDI bridge does not send the outgoing message to the receiving partner until the release criteria is fulfilled.</span></span> <span data-ttu-id="0cf51-275">예를 들어 메시지 크기에 따른 일괄 처리 기준은 'n' 메시지가 일괄 처리된 경우에만 일괄 처리를 디스패치합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-275">For example, a batching criteria based on message size dispatches a batch only when ‘n’ messages are batched.</span></span> <span data-ttu-id="0cf51-276">일괄 처리가 매일 정해진 시간에 전송되도록 일괄 처리 조건은 시간 기반이 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-276">A batch criteria can also be time-based, such that a batch is sent at a fixed time every day.</span></span> <span data-ttu-id="0cf51-277">이 솔루션에서는 조건에 따라 메시지 크기를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-277">In this solution, we try the message-size based criteria.</span></span>

1. <span data-ttu-id="0cf51-278">BizTalk 서비스 포털에서 이전에 만든 규약을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-278">In the BizTalk Services Portal, click the agreement you created earlier.</span></span> <span data-ttu-id="0cf51-279">송신 설정 > 일괄 처리 > 일괄 처리 추가를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-279">Click Send Settings > Batching > Add Batch.</span></span>
2. <span data-ttu-id="0cf51-280">일괄 처리 이름으로 **InvoiceBatch**를 입력하고 설명을 제공한 다음 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-280">For batch name, enter **InvoiceBatch**, provide a description, and then click **Next**.</span></span>
3. <span data-ttu-id="0cf51-281">일괄 처리해야 하는 메시지를 정의하는 일괄 처리 조건을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-281">Specify a batch criteria, that defines which messages must be batched.</span></span> <span data-ttu-id="0cf51-282">이 솔루션에서는 모든 메시지를 일괄 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-282">In this solution, we batch all messages.</span></span> <span data-ttu-id="0cf51-283">따라서 고급 정의 사용 옵션을 선택하고 **1 = 1**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-283">So, select the Use advanced definitions option, and enter **1 = 1**.</span></span> <span data-ttu-id="0cf51-284">이는 항상 true가 되는 조건이므로 모든 메시지가 일괄 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-284">This is a condition which will always be true, and hence all messages will be batched.</span></span> <span data-ttu-id="0cf51-285">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-285">Click **Next**.</span></span>
   
   ![][17]  
4. <span data-ttu-id="0cf51-286">일괄 처리 릴리스 조건을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-286">Specify a batch release criteria.</span></span> <span data-ttu-id="0cf51-287">드롭다운 상자에서 **MessageCountBased**를 선택하고 **수**에 대해 **3**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-287">From the drop-box, select **MessageCountBased**, and for **Count**, specify **3**.</span></span> <span data-ttu-id="0cf51-288">세 개의 메시지 일괄 처리가 Northwind로 전송됨을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-288">This means that a batch of three messages will be sent to Northwind.</span></span> <span data-ttu-id="0cf51-289">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-289">Click **Next**.</span></span>
   
   ![][18]  
5. <span data-ttu-id="0cf51-290">요약을 검토한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-290">Review the summary and then click **Save**.</span></span> <span data-ttu-id="0cf51-291">**배포** 를 클릭하여 규약을 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-291">Click **Deploy** to redeploy the agreement.</span></span>
6. <span data-ttu-id="0cf51-292">**자습서 클라이언트**로 돌아가 **내부 송장 보내기**를 클릭하고 송장을 보내도록 프롬프트를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-292">Go back to the **Tutorial Client**, click **Send In-house Invoice**, and follow the prompts to send the invoice.</span></span> <span data-ttu-id="0cf51-293">일괄 처리 크기가 맞지 않기 때문에 Northwind에서 받는 송장이 없음을 확인하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-293">You will notice that no invoice is received at Northwind because the batch size is not met.</span></span> <span data-ttu-id="0cf51-294">Northwind로 전송되는 세 개의 송장 메시지를 갖도록 이 단계를 두 번 더 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-294">Repeat this step two more times, so that you have three invoice messages sent to Northwind.</span></span> <span data-ttu-id="0cf51-295">이는 3개의 메시지 일괄 처리 릴리스 조준을 충족하고 이제 Northwind에서 송장을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cf51-295">This satisfies the batch release criteria of 3 messages and you should now see an invoice at Northwind.</span></span>

<!--Image references-->
[1]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-1.PNG  
[2]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-2.PNG  
[3]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-3.PNG
[4]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-4.PNG  
[5]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-5.PNG  
[6]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-6.PNG  
[7]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-7.PNG  
[8]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-8.PNG
[9]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-9.PNG  
[10]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-10.PNG  
[11]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-11.PNG  
[12]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-12.PNG  
[13]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-13.PNG
[14]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-14.PNG  
[15]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-15.PNG  
[16]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-16.PNG  
[17]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-17.PNG  
[18]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-18.PNG

