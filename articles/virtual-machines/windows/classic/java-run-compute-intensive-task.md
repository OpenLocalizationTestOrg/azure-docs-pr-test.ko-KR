---
title: "VM의 계산 집약적인 Java 응용 프로그램 | Microsoft Docs"
description: "다른 Java 응용 프로그램에 의해 모니터링될 수 있는 계산 집약적인 Java 응용 프로그램을 실행하는 가상 컴퓨터를 만드는 방법에 대해 알아봅니다."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: ae6f2737-94c7-4569-9913-d871450c2827
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 8c51c0bb37e25ad61fe58a85dd641dabe0a1958c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-run-a-compute-intensive-task-in-java-on-a-virtual-machine"></a><span data-ttu-id="19f28-103">가상 컴퓨터에서 Java로 계산 집약적인 작업을 실행하는 방법</span><span class="sxs-lookup"><span data-stu-id="19f28-103">How to run a compute-intensive task in Java on a virtual machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="19f28-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="19f28-105">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="19f28-106">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="19f28-107">Azure에서 가상 컴퓨터를 사용하여 계산 집약적인 작업을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-107">With Azure, you can use a virtual machine to handle compute-intensive tasks.</span></span> <span data-ttu-id="19f28-108">예를 들어 가상 컴퓨터는 작업을 처리하고 그 결과를 클라이언트 컴퓨터 또는 모바일 응용 프로그램에 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-108">For example, a virtual machine can handle tasks and deliver results to client machines or mobile applications.</span></span> <span data-ttu-id="19f28-109">이 문서를 읽고 나면 다른 Java 응용 프로그램에 의해 모니터링될 수 있는 계산 집약적인 Java 응용 프로그램을 실행하는 가상 컴퓨터를 만드는 방법을 이해할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-109">After reading this article, you will have an understanding of how to create a virtual machine that runs a compute-intensive Java application that can be monitored by another Java application.</span></span>

<span data-ttu-id="19f28-110">이 자습서에서는 사용자가 Java 콘솔 응용 프로그램을 만드는 방법을  알고 있으며 라이브러리를 Java 응용 프로그램으로 가져오고 Java 아카이브(JAR)를 생성할 수 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-110">This tutorial assumes you know how to create Java console applications, can import libraries to your Java application, and can generate a Java archive (JAR).</span></span> <span data-ttu-id="19f28-111">Microsoft Azure에 대한 지식은 없는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-111">No knowledge of Microsoft Azure is assumed.</span></span>

<span data-ttu-id="19f28-112">다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-112">You will learn:</span></span>

* <span data-ttu-id="19f28-113">Java 개발 키트(JDK)가 이미 설치된 가상 컴퓨터를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="19f28-113">How to create a virtual machine with a Java Development Kit (JDK) already installed.</span></span>
* <span data-ttu-id="19f28-114">가상 컴퓨터에 원격으로 로그인하는 방법</span><span class="sxs-lookup"><span data-stu-id="19f28-114">How to remotely log in to your virtual machine.</span></span>
* <span data-ttu-id="19f28-115">서비스 버스 네임스페이스를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="19f28-115">How to create a service bus namespace.</span></span>
* <span data-ttu-id="19f28-116">계산 집약적인 작업을 수행하는 Java 응용 프로그램을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="19f28-116">How to create a Java application that performs a compute-intensive task.</span></span>
* <span data-ttu-id="19f28-117">계산 집약적인 작업의 진행 상황을 모니터링하는 Java 응용 프로그램을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="19f28-117">How to create a Java application that monitors the progress of the compute-intensive task.</span></span>
* <span data-ttu-id="19f28-118">Java 응용 프로그램을 실행하는 방법</span><span class="sxs-lookup"><span data-stu-id="19f28-118">How to run the Java applications.</span></span>
* <span data-ttu-id="19f28-119">Java 응용 프로그램을 중지하는 방법</span><span class="sxs-lookup"><span data-stu-id="19f28-119">How to stop the Java applications.</span></span>

<span data-ttu-id="19f28-120">이 자습서에서는 계산 집약적인 작업으로 순회 외판원 문제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-120">This tutorial will use the Traveling Salesman Problem for the compute-intensive task.</span></span> <span data-ttu-id="19f28-121">다음은 계산 집약적인 작업을 실행하는 Java 응용 프로그램의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-121">The following is an example of the Java application running the compute-intensive task.</span></span>

![순회 외판원 문제 해 찾기][solver_output]

<span data-ttu-id="19f28-123">다음은 계산 집약적인 작업을 모니터링하는 Java 응용 프로그램의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-123">The following is an example of the Java application monitoring the compute-intensive task.</span></span>

![순회 외판원 문제 클라이언트][client_output]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="to-create-a-virtual-machine"></a><span data-ttu-id="19f28-125">가상 컴퓨터를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="19f28-125">To create a virtual machine</span></span>
1. <span data-ttu-id="19f28-126">[Azure 클래식 포털](https://manage.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-126">Log in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="19f28-127">**새로 만들기**를 클릭하고 **계산**, **가상 컴퓨터**, **갤러리에서**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-127">Click **New**, click **Compute**, click **Virtual machine**, and then click **From Gallery**.</span></span>
3. <span data-ttu-id="19f28-128">**가상 컴퓨터 이미지 선택** 대화 상자에서 **JDK 7 Windows Server 2012**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-128">In the **Virtual machine image select** dialog box, select **JDK 7 Windows Server 2012**.</span></span>
   <span data-ttu-id="19f28-129">**JDK 6 Windows Server 2012** 는 아직 JDK 7에서 실행할 준비가 되지 않은 레거시 응용 프로그램이 있는 경우에 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-129">Note that **JDK 6 Windows Server 2012** is available in case you have legacy applications that are not yet ready to run in JDK 7.</span></span>
4. <span data-ttu-id="19f28-130">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-130">Click **Next**.</span></span>
5. <span data-ttu-id="19f28-131">**가상 컴퓨터 구성** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-131">In the **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="19f28-132">가상 컴퓨터의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-132">Specify a name for the virtual machine.</span></span>
   2. <span data-ttu-id="19f28-133">가상 컴퓨터에 사용할 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-133">Specify the size to use for the virtual machine.</span></span>
   3. <span data-ttu-id="19f28-134">**사용자 이름** 필드에 관리자의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-134">Enter a name for the administrator in the **User Name** field.</span></span> <span data-ttu-id="19f28-135">입력하는 이름 및 암호는 나중에 가상 컴퓨터에 원격으로 로그인할 때 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-135">Remember this name and the password you will enter next, you will use them when you remotely log in to the virtual machine.</span></span>
   4. <span data-ttu-id="19f28-136">**새 암호** 필드에 암호를 입력하고 **확인** 필드에 다시 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-136">Enter a password in the **New password** field, and re-enter it in the **Confirm** field.</span></span> <span data-ttu-id="19f28-137">이 암호는 관리자 계정 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-137">This is the Administrator account password.</span></span>
   5. <span data-ttu-id="19f28-138">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-138">Click **Next**.</span></span>
6. <span data-ttu-id="19f28-139">다음 **가상 컴퓨터 구성** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-139">In the next **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="19f28-140">**클라우드 서비스**의 경우 기본값인 **새 클라우드 서비스 만들기**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-140">For **Cloud service**, use the default **Create a new cloud service**.</span></span>
   2. <span data-ttu-id="19f28-141">**클라우드 서비스 DNS 이름** 값은 cloudapp.net에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-141">The value for **Cloud service DNS name** must be unique across cloudapp.net.</span></span> <span data-ttu-id="19f28-142">필요한 경우 Azure에서 고유한 이름이 되도록 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-142">If needed, modify this value so that Azure indicates it is unique.</span></span>
   3. <span data-ttu-id="19f28-143">지역, 선호도 그룹 또는 가상 네트워크를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-143">Specify a region, affinity group, or virtual network.</span></span> <span data-ttu-id="19f28-144">이 자습서에서는 지역(예: **미국 서부**)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-144">For purposes of this tutorial, specify a region such as **West US**.</span></span>
   4. <span data-ttu-id="19f28-145">**저장소 계정** 상자에서 **자동으로 생성된 저장소 계정 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-145">For **Storage Account**, select **Use an automatically generated storage account**.</span></span>
   5. <span data-ttu-id="19f28-146">**가용성 집합**에서 **(없음)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-146">For **Availability Set**, select **(None)**.</span></span>
   6. <span data-ttu-id="19f28-147">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-147">Click **Next**.</span></span>
7. <span data-ttu-id="19f28-148">마지막 **가상 컴퓨터 구성** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-148">In the final **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="19f28-149">기본 끝점 항목을 그대로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-149">Accept the default endpoint entries.</span></span>
   2. <span data-ttu-id="19f28-150">**완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-150">Click **Complete**.</span></span>

## <a name="to-remotely-log-in-to-your-virtual-machine"></a><span data-ttu-id="19f28-151">가상 컴퓨터에 원격으로 로그인하는 방법</span><span class="sxs-lookup"><span data-stu-id="19f28-151">To remotely log in to your virtual machine</span></span>
1. <span data-ttu-id="19f28-152">[Azure 클래식 포털](https://manage.windowsazure.com)에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-152">Log on to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="19f28-153">**가상 컴퓨터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-153">Click **Virtual machines**.</span></span>
3. <span data-ttu-id="19f28-154">로그인할 가상 컴퓨터의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-154">Click the name of the virtual machine that you want to log in to.</span></span>
4. <span data-ttu-id="19f28-155">**연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-155">Click **Connect**.</span></span>
5. <span data-ttu-id="19f28-156">가상 컴퓨터에 연결해야 한다는 메시지에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-156">Respond to the prompts as needed to connect to the virtual machine.</span></span> <span data-ttu-id="19f28-157">관리자 이름 및 암호를 묻는 메시지가 표시되면 가상 컴퓨터를 만들 때 제공한 값을 사용하십시오.</span><span class="sxs-lookup"><span data-stu-id="19f28-157">When prompted for the administrator name and password, use the values that you provided when you created the virtual machine.</span></span>

<span data-ttu-id="19f28-158">Azure 서비스 버스 기능을 사용하려면 Baltimore CyberTrust 루트 인증서가 JRE의 **cacerts** 저장소의 일부로 설치되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-158">Note that the Azure Service Bus functionality requires the Baltimore CyberTrust Root certificate to be installed as part of your JRE's **cacerts** store.</span></span> <span data-ttu-id="19f28-159">이 인증서는 본 자습서에서 사용하는 JRE(Java Runtime Environment)에 자동으로 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-159">This certificate is automatically included in the Java Runtime Environment (JRE) used by this tutorial.</span></span> <span data-ttu-id="19f28-160">이 인증서가 JRE **cacerts** 저장소에 없는 경우, [Java CA 인증서 저장소에 인증서 추가][add_ca_cert]에서 인증서 추가에 대한 내용 및 cacerts 저장소의 인증서 보기에 대한 정보를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="19f28-160">If you do not have this certificate in your JRE **cacerts** store, see [Adding a Certificate to the Java CA Certificate Store][add_ca_cert] for information on adding it (as well as information on viewing the certificates in your cacerts store).</span></span>

## <a name="how-to-create-a-service-bus-namespace"></a><span data-ttu-id="19f28-161">서비스 버스 네임스페이스를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="19f28-161">How to create a service bus namespace</span></span>
<span data-ttu-id="19f28-162">Azure에서 서비스 버스 큐 사용을 시작하려면 먼저 서비스 네임스페이스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-162">To begin using Service Bus queues in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="19f28-163">서비스 네임스페이스는 응용 프로그램 내에서 서비스 버스 리소스의 주소를 지정하기 위한 범위 컨테이너를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-163">A service namespace provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="19f28-164">서비스 네임스페이스를 만들려면</span><span class="sxs-lookup"><span data-stu-id="19f28-164">To create a service namespace:</span></span>

1. <span data-ttu-id="19f28-165">[Azure 클래식 포털](https://manage.windowsazure.com)에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-165">Log on to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="19f28-166">Azure 클래식 포털의 왼쪽 하단 탐색 창에서 **Service Bus, 액세스 제어 및 캐시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-166">In the lower-left navigation pane of the Azure classic portal, click **Service Bus, Access Control & Caching**.</span></span>
3. <span data-ttu-id="19f28-167">Azure 클래식 포털의 왼쪽 상단 창에서 **Service Bus** 노드 및 **새로 만들기** 버튼을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-167">In the upper-left pane of the Azure classic portal, click the **Service Bus** node, and then click the **New** button.</span></span>  
   <span data-ttu-id="19f28-168">![서비스 버스 노드 스크린샷][svc_bus_node]</span><span class="sxs-lookup"><span data-stu-id="19f28-168">![Service Bus Node screenshot][svc_bus_node]</span></span>
4. <span data-ttu-id="19f28-169">**새 서비스 네임스페이스 만들기** 대화 상자에서 **네임스페이스**를 입력한 후 네임스페이스가 중복되지 않는지 확인하기 위해 **중복 확인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-169">In the **Create a new Service Namespace** dialog box, enter a **Namespace**, and then to make sure that it is unique, click the **Check Availability** button.</span></span>  
   <span data-ttu-id="19f28-170">![새 네임스페이스 만들기 스크린샷][create_namespace]</span><span class="sxs-lookup"><span data-stu-id="19f28-170">![Create a New Namespace screenshot][create_namespace]</span></span>
5. <span data-ttu-id="19f28-171">네임스페이스 이름이 사용 가능한지 확인한 후 해당 네임스페이스를 호스트할 국가 또는 지역을 선택한 다음, **Create Namespace** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-171">After making sure the namespace name is available, choose the country or region in which your namespace should be hosted, and then click the **Create Namespace** button.</span></span>  
   
   <span data-ttu-id="19f28-172">생성된 네임스페이스는 Azure 클래식 포털에 나타나며, 잠시후에 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-172">The namespace you created will then appear in the Azure classic portal and takes a moment to activate.</span></span> <span data-ttu-id="19f28-173">다음 단계를 계속하기 전에 **활성** 상태가 될 때까지 기다리십시오.</span><span class="sxs-lookup"><span data-stu-id="19f28-173">Wait until the status is **Active** before continuing with the next step.</span></span>

## <a name="obtain-the-default-management-credentials-for-the-namespace"></a><span data-ttu-id="19f28-174">네임스페이스에 대한 기본 관리 자격 증명 얻기</span><span class="sxs-lookup"><span data-stu-id="19f28-174">Obtain the Default Management Credentials for the namespace</span></span>
<span data-ttu-id="19f28-175">새 네임스페이스에 대해 큐 만들기 등의 관리 작업을 수행하려면 네임스페이스에 대한 관리 자격 증명을 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-175">In order to perform management operations, such as creating a queue, on the new namespace, you need to obtain the management credentials for the namespace.</span></span>

1. <span data-ttu-id="19f28-176">왼쪽 탐색 창에서 **서비스 버스** 노드를 클릭하여 사용 가능한 네임스페이스 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-176">In the left navigation pane, click the **Service Bus** node to display the list of available namespaces.</span></span>
   <span data-ttu-id="19f28-177">![사용 가능한 네임스페이스 스크린샷][avail_namespaces]</span><span class="sxs-lookup"><span data-stu-id="19f28-177">![Available Namespaces screenshot][avail_namespaces]</span></span>
2. <span data-ttu-id="19f28-178">표시된 목록에서 방금 만든 네임스페이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-178">Select the namespace you just created from the list shown.</span></span>
   <span data-ttu-id="19f28-179">![네임스페이스 목록 스크린샷][namespace_list]</span><span class="sxs-lookup"><span data-stu-id="19f28-179">![Namespace List screenshot][namespace_list]</span></span>
3. <span data-ttu-id="19f28-180">오른쪽 **속성** 창에 새 네임스페이스의 속성이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-180">The right-hand **Properties** pane lists the properties for the new namespace.</span></span>
   <span data-ttu-id="19f28-181">![속성 창 스크린샷][properties_pane]</span><span class="sxs-lookup"><span data-stu-id="19f28-181">![Properties Pane screenshot][properties_pane]</span></span>
4. <span data-ttu-id="19f28-182">**기본 키** 가 숨겨져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-182">The **Default Key** is hidden.</span></span> <span data-ttu-id="19f28-183">**보기** 단추를 클릭하여 보안 자격 증명을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-183">Click the **View** button to display the security credentials.</span></span>
   <span data-ttu-id="19f28-184">![기본 키 스크린샷][default_key]</span><span class="sxs-lookup"><span data-stu-id="19f28-184">![Default Key screenshot][default_key]</span></span>
5. <span data-ttu-id="19f28-185">**기본 발급자** 및 **기본 키**를 기록해 둡니다. 이 정보는 아래에서 네임스페이스 관련 작업을 수행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-185">Make a note of the **Default Issuer** and the **Default Key** as you will use this information below to perform operations with the namespace.</span></span>

## <a name="how-to-create-a-java-application-that-performs-a-compute-intensive-task"></a><span data-ttu-id="19f28-186">계산 집약적인 작업을 수행하는 Java 응용 프로그램을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="19f28-186">How to create a Java application that performs a compute-intensive task</span></span>
1. <span data-ttu-id="19f28-187">개발 컴퓨터(직접 생성한 가상 컴퓨터일 필요는 없음)에서 [Java용 Azure SDK](https://azure.microsoft.com/develop/java/)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-187">On your development machine (which does not have to be the virtual machine that you created), download the [Azure SDK for Java](https://azure.microsoft.com/develop/java/).</span></span>
2. <span data-ttu-id="19f28-188">이 섹션의 끝부분에 있는 예제 코드를 사용하여 Java 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-188">Create a Java console application using the example code at the end of this section.</span></span> <span data-ttu-id="19f28-189">이 자습서에서는 Java 파일 이름으로 **TSPSolver.java** 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-189">In this tutorial, we'll use **TSPSolver.java** as the Java file name.</span></span> <span data-ttu-id="19f28-190">**your\_service\_bus\_namespace**, **your\_service\_bus\_owner** 및 **your\_service\_bus\_key** 자리 표시자를 각각 Service Bus **네임스페이스**, **기본 발급자** 및 **기본 키** 값을 사용하도록 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-190">Modify the **your\_service\_bus\_namespace**, **your\_service\_bus\_owner**, and **your\_service\_bus\_key** placeholders to use your service bus **namespace**, **Default Issuer** and **Default Key** values, respectively.</span></span>
3. <span data-ttu-id="19f28-191">코딩 후에 응용 프로그램을 실행 가능한 Java 아카이브(JAR)로 내보내고 필요한 라이브러리를 생성된 JAR 안에 패키징합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-191">After coding, export the application to a runnable Java archive (JAR), and package the required libraries into the generated JAR.</span></span> <span data-ttu-id="19f28-192">이 자습서에서는 생성된 JAR 이름으로 **TSPSolver.jar** 을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-192">In this tutorial, we'll use **TSPSolver.jar** as the generated JAR name.</span></span>

<p/>

    // TSPSolver.java

    import com.microsoft.windowsazure.services.core.Configuration;
    import com.microsoft.windowsazure.services.core.ServiceException;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import java.io.*;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import java.util.ArrayList;
    import java.util.Date;
    import java.util.List;

    public class TSPSolver {

        //  Value specifying how often to provide an update to the console.
        private static long loopCheck = 100000000;  

        private static long nTimes = 0, nLoops=0;

        private static double[][] distances;
        private static String[] cityNames;
        private static int[] bestOrder;
        private static double minDistance;
        private static ServiceBusContract service;

        private static void buildDistances(String fileLocation, int numCities) throws Exception{
            try{
                BufferedReader file = new BufferedReader(new InputStreamReader(new DataInputStream(new FileInputStream(new File(fileLocation)))));
                double[][] cityLocs = new double[numCities][2];
                for (int i = 0; i<numCities; i++){
                    String[] line = file.readLine().split(", ");
                    cityNames[i] = line[0];
                    cityLocs[i][0] = Double.parseDouble(line[1]);
                    cityLocs[i][1] = Double.parseDouble(line[2]);
                }
                for (int i = 0; i<numCities; i++){
                    for (int j = i; j<numCities; j++){
                        distances[i][j] = Math.hypot(Math.abs(cityLocs[i][0] - cityLocs[j][0]), Math.abs(cityLocs[i][1] - cityLocs[j][1]));
                        distances[j][i] = distances[i][j];
                    }
                }
            } catch (Exception e){
                throw e;
            }
        }

        private static void permutation(List<Integer> startCities, double distSoFar, List<Integer> restCities) throws Exception {

            try
            {
                nTimes++;
                if (nTimes == loopCheck)
                {
                    nLoops++;
                    nTimes = 0;
                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.print("Current time is " + dateFormat.format(date) + ". ");
                    System.out.println(  "Completed " + nLoops + " iterations of size of " + loopCheck + ".");
                }

                if ((restCities.size() == 1) && ((minDistance == -1) || (distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-1)] < minDistance))){
                    startCities.add(restCities.get(0));
                    newBestDistance(startCities, distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-2)]);
                    startCities.remove(startCities.size()-1);
                }
                else{
                    for (int i=0; i<restCities.size(); i++){
                        startCities.add(restCities.get(0));
                        restCities.remove(0);
                        permutation(startCities, distSoFar + distances[startCities.get(startCities.size()-1)][startCities.get(startCities.size()-2)],restCities);
                        restCities.add(startCities.get(startCities.size()-1));
                        startCities.remove(startCities.size()-1);
                    }
                }
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        private static void newBestDistance(List<Integer> cities, double distance) throws ServiceException, Exception {
            try
            {
                minDistance = distance;
                String cityList = "Shortest distance is "+minDistance+", with route: ";
                for (int i = 0; i<bestOrder.length; i++){
                    bestOrder[i] = cities.get(i);
                    cityList += cityNames[bestOrder[i]];
                    if (i != bestOrder.length -1)
                        cityList += ", ";
                }
                System.out.println(cityList);
                service.sendQueueMessage("TSPQueue", new BrokeredMessage(cityList));
            }
            catch (ServiceException se)
            {
                throw se;
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        public static void main(String args[]){

            try {

                Configuration config = ServiceBusConfiguration.configureWithWrapAuthentication(
                        "your_service_bus_namespace", "your_service_bus_owner",
                        "your_service_bus_key",
                        ".servicebus.windows.net",
                        "-sb.accesscontrol.windows.net/WRAPv0.9");

                service = ServiceBusService.create(config);

                int numCities = 10;  // Use as the default, if no value is specified at command line.
                if (args.length != 0)
                {
                    if (args[0].toLowerCase().compareTo("createqueue")==0)
                    {
                        // No processing to occur other than creating the queue.
                        QueueInfo queueInfo = new QueueInfo("TSPQueue");

                        service.createQueue(queueInfo);

                        System.out.println("Queue named TSPQueue was created.");

                        System.exit(0);
                    }

                    if (args[0].toLowerCase().compareTo("deletequeue")==0)
                    {
                        // No processing to occur other than deleting the queue.
                        service.deleteQueue("TSPQueue");

                        System.out.println("Queue named TSPQueue was deleted.");

                        System.exit(0);
                    }

                    // Neither creating or deleting a queue.
                    // Assume the value passed in is the number of cities to solve.
                    numCities = Integer.valueOf(args[0]);  
                }

                System.out.println("Running for " + numCities + " cities.");

                List<Integer> startCities = new ArrayList<Integer>();
                List<Integer> restCities = new ArrayList<Integer>();
                startCities.add(0);
                for(int i = 1; i<numCities; i++)
                    restCities.add(i);
                distances = new double[numCities][numCities];
                cityNames = new String[numCities];
                buildDistances("c:\\TSP\\cities.txt", numCities);
                minDistance = -1;
                bestOrder = new int[numCities];
                permutation(startCities, 0, restCities);
                System.out.println("Final solution found!");
                service.sendQueueMessage("TSPQueue", new BrokeredMessage("Complete"));
            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }
        }

    }



## <a name="how-to-create-a-java-application-that-monitors-the-progress-of-the-compute-intensive-task"></a><span data-ttu-id="19f28-193">계산 집약적인 작업의 진행 상황을 모니터링하는 Java 응용 프로그램을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="19f28-193">How to create a Java application that monitors the progress of the compute-intensive task</span></span>
1. <span data-ttu-id="19f28-194">개발 컴퓨터에서 이 섹션의 끝부분에 있는 예제 코드를 사용하여 Java 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-194">On your development machine, create a Java console application using the example code at the end of this section.</span></span> <span data-ttu-id="19f28-195">이 자습서에서는 Java 파일 이름으로 **TSPClient.java** 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-195">In this tutorial, we'll use **TSPClient.java** as the Java file name.</span></span> <span data-ttu-id="19f28-196">**your\_service\_bus\_namespace**, **your\_service\_bus\_owner** 및 **your\_service\_bus\_key** 자리 표시자를 각각 Service Bus **네임스페이스**, **기본 발급자** 및 **기본 키** 값을 사용하도록 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-196">As shown earlier, modify the **your\_service\_bus\_namespace**, **your\_service\_bus\_owner**, and **your\_service\_bus\_key** placeholders to use your service bus **namespace**, **Default Issuer** and **Default Key** values, respectively.</span></span>
2. <span data-ttu-id="19f28-197">응용 프로그램을 실행 가능한 JAR로 내보내고 필요한 라이브러리를 생성된 JAR 안에 패키징합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-197">Export the application to a runnable JAR, and package the required libraries into the generated JAR.</span></span> <span data-ttu-id="19f28-198">이 자습서에서는 생성된 JAR 이름으로 **TSPClient.jar** 을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-198">In this tutorial, we'll use **TSPClient.jar** as the generated JAR name.</span></span>

<p/>

    // TSPClient.java

    import java.util.Date;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import com.microsoft.windowsazure.services.core.*;

    public class TSPClient
    {

        public static void main(String[] args)
        {
                try
                {

                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.println("Starting at " + dateFormat.format(date) + ".");

                    String namespace = "your_service_bus_namespace";
                    String issuer = "your_service_bus_owner";
                    String key = "your_service_bus_key";

                    Configuration config;
                    config = ServiceBusConfiguration.configureWithWrapAuthentication(
                            namespace, issuer, key,
                            ".servicebus.windows.net",
                            "-sb.accesscontrol.windows.net/WRAPv0.9");

                    ServiceBusContract service = ServiceBusService.create(config);

                    BrokeredMessage message;

                    int waitMinutes = 3;  // Use as the default, if no value is specified at command line.
                    if (args.length != 0)
                    {
                        waitMinutes = Integer.valueOf(args[0]);  
                    }

                    String waitString;

                    waitString = (waitMinutes == 1) ? "minute." : waitMinutes + " minutes.";

                    // This queue must have previously been created.
                    service.getQueue("TSPQueue");

                    int numRead;

                    String s = null;

                    while (true)
                    {

                        ReceiveQueueMessageResult resultQM = service.receiveQueueMessage("TSPQueue");
                        message = resultQM.getValue();

                        if (null != message && null != message.getMessageId())
                        {

                            // Display the queue message.
                            byte[] b = new byte[200];

                            System.out.print("From queue: ");

                            s = null;
                            numRead = message.getBody().read(b);
                            while (-1 != numRead)
                            {
                                s = new String(b);
                                s = s.trim();
                                System.out.print(s);
                                numRead = message.getBody().read(b);
                            }
                            System.out.println();
                            if (s.compareTo("Complete") == 0)
                            {
                                // No more processing to occur.
                                date = new Date();
                                System.out.println("Finished at " + dateFormat.format(date) + ".");
                                break;
                            }
                        }
                        else
                        {
                            // The queue is empty.
                            System.out.println("Queue is empty. Sleeping for another " + waitString);
                            Thread.sleep(60000 * waitMinutes);
                        }
                    }

            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }

        }

    }

## <a name="how-to-run-the-java-applications"></a><span data-ttu-id="19f28-199">Java 응용 프로그램을 실행하는 방법</span><span class="sxs-lookup"><span data-stu-id="19f28-199">How to run the Java applications</span></span>
<span data-ttu-id="19f28-200">계산 집약적인 응용 프로그램을 실행하여 먼저 큐를 만든 후에 순회 외판원 문제를 해결합니다. 그러면 현 시점에서의 최상의 경로가 서비스 버스 큐에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-200">Run the compute-intensive application, first to create the queue, then to solve the Traveling Saleseman Problem, which will add the current best route to the service bus queue.</span></span> <span data-ttu-id="19f28-201">계산 집약적인 응용 프로그램이 실행 중인 동안 또는 실행된 이후에 클라이언트를 실행하여 서비스 버스 큐에서 가져온 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-201">While the compute-intensive application is running (or afterwards), run the client to display results from the service bus queue.</span></span>

### <a name="to-run-the-compute-intensive-application"></a><span data-ttu-id="19f28-202">계산 집약적인 응용 프로그램을 실행하려면</span><span class="sxs-lookup"><span data-stu-id="19f28-202">To run the compute-intensive application</span></span>
1. <span data-ttu-id="19f28-203">가상 컴퓨터에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-203">Log on to your virtual machine.</span></span>
2. <span data-ttu-id="19f28-204">응용 프로그램을 실행할 폴더(예:</span><span class="sxs-lookup"><span data-stu-id="19f28-204">Create a folder where you will run your application.</span></span> <span data-ttu-id="19f28-205">**c:\TSP**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-205">For example, **c:\TSP**.</span></span>
3. <span data-ttu-id="19f28-206">**TSPSolver.jar**를 **c:\TSP**에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-206">Copy **TSPSolver.jar** to **c:\TSP**,</span></span>
4. <span data-ttu-id="19f28-207">다음과 같은 콘텐츠가 포함된 **c:\TSP\cities.txt** 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-207">Create a file named **c:\TSP\cities.txt** with the following contents.</span></span>
   
        City_1, 1002.81, -1841.35
        City_2, -953.55, -229.6
        City_3, -1363.11, -1027.72
        City_4, -1884.47, -1616.16
        City_5, 1603.08, -1030.03
        City_6, -1555.58, 218.58
        City_7, 578.8, -12.87
        City_8, 1350.76, 77.79
        City_9, 293.36, -1820.01
        City_10, 1883.14, 1637.28
        City_11, -1271.41, -1670.5
        City_12, 1475.99, 225.35
        City_13, 1250.78, 379.98
        City_14, 1305.77, 569.75
        City_15, 230.77, 231.58
        City_16, -822.63, -544.68
        City_17, -817.54, -81.92
        City_18, 303.99, -1823.43
        City_19, 239.95, 1007.91
        City_20, -1302.92, 150.39
        City_21, -116.11, 1933.01
        City_22, 382.64, 835.09
        City_23, -580.28, 1040.04
        City_24, 205.55, -264.23
        City_25, -238.81, -576.48
        City_26, -1722.9, -909.65
        City_27, 445.22, 1427.28
        City_28, 513.17, 1828.72
        City_29, 1750.68, -1668.1
        City_30, 1705.09, -309.35
        City_31, -167.34, 1003.76
        City_32, -1162.85, -1674.33
        City_33, 1490.32, 821.04
        City_34, 1208.32, 1523.3
        City_35, 18.04, 1857.11
        City_36, 1852.46, 1647.75
        City_37, -167.44, -336.39
        City_38, 115.4, 0.2
        City_39, -66.96, 917.73
        City_40, 915.96, 474.1
        City_41, 140.03, 725.22
        City_42, -1582.68, 1608.88
        City_43, -567.51, 1253.83
        City_44, 1956.36, 830.92
        City_45, -233.38, 909.93
        City_46, -1750.45, 1940.76
        City_47, 405.81, 421.84
        City_48, 363.68, 768.21
        City_49, -120.3, -463.13
        City_50, 588.51, 679.33
5. <span data-ttu-id="19f28-208">명령 프롬프트에서 디렉터리를 c:\TSP로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-208">At a command prompt, change directories to c:\TSP.</span></span>
6. <span data-ttu-id="19f28-209">JRE의 bin 폴더가 PATH 환경 변수에 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-209">Ensure the JRE's bin folder is in the PATH environment variable.</span></span>
7. <span data-ttu-id="19f28-210">TSP 해 찾기 순열을 실행하기 전에 서비스 버스 큐를 먼저 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-210">You'll need to create the service bus queue before you run the TSP solver permutations.</span></span> <span data-ttu-id="19f28-211">다음 명령을 실행하여 서비스 버스 큐를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-211">Run the following command to create the service bus queue.</span></span>
   
        java -jar TSPSolver.jar createqueue
8. <span data-ttu-id="19f28-212">큐가 만들어졌으므로 이제 TSP 해 찾기 순열을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-212">Now that the queue is created, you can run the TSP solver permutations.</span></span> <span data-ttu-id="19f28-213">예를 들어 다음 명령을 실행하여 8개 도시에 대해 해 찾기를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-213">For example, run the following command to run the solver for 8 cities.</span></span>
   
        java -jar TSPSolver.jar 8
   
   <span data-ttu-id="19f28-214">숫자를 지정하지 않으면 10개 도시에 대해 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-214">If you don't specify a number, it will run for 10 cities.</span></span> <span data-ttu-id="19f28-215">해 찾기에서 현재의 최단 경로를 찾으면 해당 경로가 큐에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-215">As the solver finds current shortest routes, it will add them to the queue.</span></span>

> [!NOTE]
> <span data-ttu-id="19f28-216">지정한 숫자가 클수록 해 찾기 실행 시간이 길어집니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-216">The larger the number that you specify, the longer the solver will run.</span></span> <span data-ttu-id="19f28-217">예를 들어 14개 도시에 대해 실행하면 몇 분이 걸릴 수 있고, 15개 도시에 대해 실행하면 몇 시간이 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-217">For example, running for 14 cities could take several minutes, and running for 15 cities could take several hours.</span></span> <span data-ttu-id="19f28-218">도시를 16개 이상으로 늘리면 며칠 동안 더 나아가 수주, 수개월, 수년에 걸쳐 실행될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-218">Increasing to 16 or more cities could result in days of runtime (eventually weeks, months, and years).</span></span> <span data-ttu-id="19f28-219">이는 도시의 수가 증가함에 따라 해 찾기에 의해 평가되는 순열의 수가 급증하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-219">This is due to the rapid increase in the number of permutations evaluated by the solver as the number of cities increases.</span></span>
> 
> 

### <a name="how-to-run-the-monitoring-client-application"></a><span data-ttu-id="19f28-220">모니터링하는 클라이언트 응용 프로그램을 실행하는 방법</span><span class="sxs-lookup"><span data-stu-id="19f28-220">How to run the monitoring client application</span></span>
1. <span data-ttu-id="19f28-221">클라이언트 응용 프로그램을 실행할 컴퓨터에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-221">Log on to your machine where you will run the client application.</span></span> <span data-ttu-id="19f28-222">이 컴퓨터가 **TSPSolver** 응용 프로그램을 실행하는 컴퓨터와 같을 수도 있지만 반드시 같아야 하는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-222">This does not need to be the same machine running the **TSPSolver** application, although it can be.</span></span>
2. <span data-ttu-id="19f28-223">응용 프로그램을 실행할 폴더(예:</span><span class="sxs-lookup"><span data-stu-id="19f28-223">Create a folder where you will run your application.</span></span> <span data-ttu-id="19f28-224">**c:\TSP**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-224">For example, **c:\TSP**.</span></span>
3. <span data-ttu-id="19f28-225">**TSPClient.jar**를 **c:\TSP**에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-225">Copy **TSPClient.jar** to **c:\TSP**,</span></span>
4. <span data-ttu-id="19f28-226">JRE의 bin 폴더가 PATH 환경 변수에 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-226">Ensure the JRE's bin folder is in the PATH environment variable.</span></span>
5. <span data-ttu-id="19f28-227">명령 프롬프트에서 디렉터리를 c:\TSP로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-227">At a command prompt, change directories to c:\TSP.</span></span>
6. <span data-ttu-id="19f28-228">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-228">Run the following command.</span></span>
   
        java -jar TSPClient.jar
   
    <span data-ttu-id="19f28-229">큐를 점검하는 시점 사이의 대기 시간(분)을 명령줄 인수로 전달하여 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-229">Optionally, specify the number of minutes to sleep in between checking the queue, by passing in a command-line argument.</span></span> <span data-ttu-id="19f28-230">큐 점검을 위한 기본 대기 기간은 3분이며, **TSPClient**로 명령줄 인수가 전달되지 않을 경우 이 값이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-230">The default sleep period for checking the queue is 3 minutes, which is used if no command-line argument is passed to **TSPClient**.</span></span> <span data-ttu-id="19f28-231">대기 간격으로 다른 값(예: 1분)을 사용하고 싶으면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-231">If you want to use a different value for the sleep interval, for example, one minute, run the following command.</span></span>
   
        java -jar TSPClient.jar 1
   
    <span data-ttu-id="19f28-232">클라이언트는 "완료"라는 큐 메시지가 확인될 때까지 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-232">The client will run until it sees a queue message of "Complete".</span></span> <span data-ttu-id="19f28-233">클라이언트를 실행하지 않은 상태로 해 찾기를 여러 번 실행하는 경우, 큐를 완전히 비우기 위해 클라이언트를 여러 번 실행해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-233">Note that if you run multiple occurrences of the solver without running the client, you may need to run the client multiple times to completely empty the queue.</span></span> <span data-ttu-id="19f28-234">또는 큐를 삭제한 후 큐를 다시 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-234">Alternatively, you can delete the queue and then create it again.</span></span> <span data-ttu-id="19f28-235">큐를 삭제하려면 다음 **TSPSolver**(**TSPClient** 아님) 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-235">To delete the queue, run the following **TSPSolver** (not **TSPClient**)  command.</span></span>
   
        java -jar TSPSolver.jar deletequeue
   
    <span data-ttu-id="19f28-236">모든 경로에 대한 조사를 마칠 때까지 해 찾기가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-236">The solver will run until it finishes examining all routes.</span></span>

## <a name="how-to-stop-the-java-applications"></a><span data-ttu-id="19f28-237">Java 응용 프로그램을 중지하는 방법</span><span class="sxs-lookup"><span data-stu-id="19f28-237">How to stop the Java applications</span></span>
<span data-ttu-id="19f28-238">해 찾기 및 클라이언트 응용 프로그램을 정상적인 완료 이전에 종료하고 싶으면 **Ctrl+C** 를 누르면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19f28-238">For both the solver and client applications, you can press **Ctrl+C** to exit if you want to end prior to normal completion.</span></span>

[solver_output]:media/java-run-compute-intensive-task/WA_JavaTSPSolver.png
[client_output]:media/java-run-compute-intensive-task/WA_JavaTSPClient.png
[svc_bus_node]:media/java-run-compute-intensive-task/SvcBusQueues_02_SvcBusNode.jpg
[create_namespace]:media/java-run-compute-intensive-task/SvcBusQueues_03_CreateNewSvcNamespace.jpg
[avail_namespaces]:media/java-run-compute-intensive-task/SvcBusQueues_04_SvcBusNode_AvailNamespaces.jpg
[namespace_list]:media/java-run-compute-intensive-task/SvcBusQueues_05_NamespaceList.jpg
[properties_pane]:media/java-run-compute-intensive-task/SvcBusQueues_06_PropertiesPane.jpg
[default_key]:media/java-run-compute-intensive-task/SvcBusQueues_07_DefaultKey.jpg
[add_ca_cert]: ../../../java-add-certificate-ca-store.md
