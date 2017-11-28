---
title: "VM에서 Java 응용 프로그램 aaaCompute를 많이 사용 | Microsoft Docs"
description: "다른 Java 응용 프로그램에서 계산 집약적인 Java 응용 프로그램을 실행 하는 Azure 가상 컴퓨터 toocreate 수 모니터링 하는 방법을 알아봅니다."
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
ms.openlocfilehash: 02a198802a8d78bd444cd5a9197a78cb94f48e3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-compute-intensive-task-in-java-on-a-virtual-machine"></a><span data-ttu-id="bf1ea-103">Toorun 계산 집약적인 java에서 가상 컴퓨터에서 작업 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bf1ea-103">How toorun a compute-intensive task in Java on a virtual machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="bf1ea-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="bf1ea-105">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="bf1ea-106">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="bf1ea-107">Azure 가상 컴퓨터 toohandle 계산 집약적인 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-107">With Azure, you can use a virtual machine toohandle compute-intensive tasks.</span></span> <span data-ttu-id="bf1ea-108">예를 들어 가상 컴퓨터 작업을 처리 하 고 결과 tooclient 컴퓨터 또는 모바일 응용 프로그램 배달 수입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-108">For example, a virtual machine can handle tasks and deliver results tooclient machines or mobile applications.</span></span> <span data-ttu-id="bf1ea-109">이 문서를 읽은 후 다른 Java 응용 프로그램에서 계산 집약적인 Java 응용 프로그램을 실행 하는 가상 컴퓨터 toocreate 수 모니터링 하는 방법을 이해를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-109">After reading this article, you will have an understanding of how toocreate a virtual machine that runs a compute-intensive Java application that can be monitored by another Java application.</span></span>

<span data-ttu-id="bf1ea-110">이 자습서에서는 toocreate Java 콘솔 응용 프로그램 라이브러리 tooyour Java 응용 프로그램을 가져올 수 및 Java 보관 파일 (JAR)를 생성할 수 있습니다 어떻게 알고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-110">This tutorial assumes you know how toocreate Java console applications, can import libraries tooyour Java application, and can generate a Java archive (JAR).</span></span> <span data-ttu-id="bf1ea-111">Microsoft Azure에 대한 지식은 없는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-111">No knowledge of Microsoft Azure is assumed.</span></span>

<span data-ttu-id="bf1ea-112">다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-112">You will learn:</span></span>

* <span data-ttu-id="bf1ea-113">어떻게 toocreate Java 개발 키트 (JDK)와 가상 컴퓨터를 이미 설치 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-113">How toocreate a virtual machine with a Java Development Kit (JDK) already installed.</span></span>
* <span data-ttu-id="bf1ea-114">어떻게 tooremotely tooyour 가상 컴퓨터에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-114">How tooremotely log in tooyour virtual machine.</span></span>
* <span data-ttu-id="bf1ea-115">어떻게 toocreate 서비스 버스 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-115">How toocreate a service bus namespace.</span></span>
* <span data-ttu-id="bf1ea-116">어떻게 toocreate 계산 집약적인 작업을 수행 하는 Java 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-116">How toocreate a Java application that performs a compute-intensive task.</span></span>
* <span data-ttu-id="bf1ea-117">어떻게 toocreate 모니터링 하는 Java 응용 프로그램 hello hello 계산 집약적인 작업의 진행 상황입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-117">How toocreate a Java application that monitors hello progress of hello compute-intensive task.</span></span>
* <span data-ttu-id="bf1ea-118">어떻게 toorun hello Java 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-118">How toorun hello Java applications.</span></span>
* <span data-ttu-id="bf1ea-119">어떻게 toostop hello Java 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-119">How toostop hello Java applications.</span></span>

<span data-ttu-id="bf1ea-120">이 자습서는 hello 계산 집약적인 작업에 대 한 hello 외판원 문제를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-120">This tutorial will use hello Traveling Salesman Problem for hello compute-intensive task.</span></span> <span data-ttu-id="bf1ea-121">hello 다음은 hello Java 응용 프로그램 실행 중인 hello 계산 집약적인 작업의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-121">hello following is an example of hello Java application running hello compute-intensive task.</span></span>

![순회 외판원 문제 해 찾기][solver_output]

<span data-ttu-id="bf1ea-123">hello 다음은 hello Java 응용 프로그램 모니터링 hello 계산 집약적인 작업의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-123">hello following is an example of hello Java application monitoring hello compute-intensive task.</span></span>

![순회 외판원 문제 클라이언트][client_output]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a><span data-ttu-id="bf1ea-125">toocreate 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="bf1ea-125">toocreate a virtual machine</span></span>
1. <span data-ttu-id="bf1ea-126">Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-126">Log in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="bf1ea-127">**새로 만들기**를 클릭하고 **계산**, **가상 컴퓨터**, **갤러리에서**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-127">Click **New**, click **Compute**, click **Virtual machine**, and then click **From Gallery**.</span></span>
3. <span data-ttu-id="bf1ea-128">Hello에 **가상 컴퓨터 이미지 선택** 대화 상자에서 **JDK 7 Windows Server 2012**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-128">In hello **Virtual machine image select** dialog box, select **JDK 7 Windows Server 2012**.</span></span>
   <span data-ttu-id="bf1ea-129">**JDK 6 Windows Server 2012** 는 아직 JDK 7에서 준비 toorun 없는 레거시 응용 프로그램이 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-129">Note that **JDK 6 Windows Server 2012** is available in case you have legacy applications that are not yet ready toorun in JDK 7.</span></span>
4. <span data-ttu-id="bf1ea-130">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-130">Click **Next**.</span></span>
5. <span data-ttu-id="bf1ea-131">Hello에 **가상 컴퓨터 구성** 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="bf1ea-131">In hello **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="bf1ea-132">Hello 가상 컴퓨터에 대 한 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-132">Specify a name for hello virtual machine.</span></span>
   2. <span data-ttu-id="bf1ea-133">Hello 크기 toouse hello 가상 컴퓨터를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-133">Specify hello size toouse for hello virtual machine.</span></span>
   3. <span data-ttu-id="bf1ea-134">Hello에 hello 관리자에 대 한 이름을 입력 **사용자 이름** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-134">Enter a name for hello administrator in hello **User Name** field.</span></span> <span data-ttu-id="bf1ea-135">이 암호 이름 및 hello 옆에 입력 하면, toohello 가상 컴퓨터에 원격으로 로그인 할 때 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-135">Remember this name and hello password you will enter next, you will use them when you remotely log in toohello virtual machine.</span></span>
   4. <span data-ttu-id="bf1ea-136">Hello에 암호를 입력 **새 암호** 필드를 다시 hello에 입력 **확인** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-136">Enter a password in hello **New password** field, and re-enter it in hello **Confirm** field.</span></span> <span data-ttu-id="bf1ea-137">이것이 hello 관리자 계정 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-137">This is hello Administrator account password.</span></span>
   5. <span data-ttu-id="bf1ea-138">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-138">Click **Next**.</span></span>
6. <span data-ttu-id="bf1ea-139">Hello에 다음 **가상 컴퓨터 구성** 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="bf1ea-139">In hello next **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="bf1ea-140">에 대 한 **클라우드 서비스**, hello 기본값을 사용 하 여 **새 클라우드 서비스를 만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-140">For **Cloud service**, use hello default **Create a new cloud service**.</span></span>
   2. <span data-ttu-id="bf1ea-141">값에 대 한 hello **클라우드 서비스 DNS 이름** cloudapp.net에서 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-141">hello value for **Cloud service DNS name** must be unique across cloudapp.net.</span></span> <span data-ttu-id="bf1ea-142">필요한 경우 Azure에서 고유한 이름이 되도록 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-142">If needed, modify this value so that Azure indicates it is unique.</span></span>
   3. <span data-ttu-id="bf1ea-143">지역, 선호도 그룹 또는 가상 네트워크를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-143">Specify a region, affinity group, or virtual network.</span></span> <span data-ttu-id="bf1ea-144">이 자습서에서는 지역(예: **미국 서부**)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-144">For purposes of this tutorial, specify a region such as **West US**.</span></span>
   4. <span data-ttu-id="bf1ea-145">**저장소 계정** 상자에서 **자동으로 생성된 저장소 계정 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-145">For **Storage Account**, select **Use an automatically generated storage account**.</span></span>
   5. <span data-ttu-id="bf1ea-146">**가용성 집합**에서 **(없음)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-146">For **Availability Set**, select **(None)**.</span></span>
   6. <span data-ttu-id="bf1ea-147">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-147">Click **Next**.</span></span>
7. <span data-ttu-id="bf1ea-148">최종 hello에 **가상 컴퓨터 구성** 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="bf1ea-148">In hello final **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="bf1ea-149">Hello 기본 끝점 항목을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-149">Accept hello default endpoint entries.</span></span>
   2. <span data-ttu-id="bf1ea-150">페이지 맨 아래에 있는 **완료**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-150">Click **Complete**.</span></span>

## <a name="tooremotely-log-in-tooyour-virtual-machine"></a><span data-ttu-id="bf1ea-151">tooremotely 로그인 tooyour 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="bf1ea-151">tooremotely log in tooyour virtual machine</span></span>
1. <span data-ttu-id="bf1ea-152">Toohello 로그온 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-152">Log on toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="bf1ea-153">**가상 컴퓨터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-153">Click **Virtual machines**.</span></span>
3. <span data-ttu-id="bf1ea-154">Hello 하려는 toolog에 hello 가상 컴퓨터 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-154">Click hello name of hello virtual machine that you want toolog in to.</span></span>
4. <span data-ttu-id="bf1ea-155">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-155">Click **Connect**.</span></span>
5. <span data-ttu-id="bf1ea-156">필요한 tooconnect toohello 가상 컴퓨터로 toohello 표시 되는 메시지에 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-156">Respond toohello prompts as needed tooconnect toohello virtual machine.</span></span> <span data-ttu-id="bf1ea-157">Hello 관리자 이름 및 암호에 대 한 메시지가 표시 되 면 hello 가상 컴퓨터를 만들 때 제공한 hello 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-157">When prompted for hello administrator name and password, use hello values that you provided when you created hello virtual machine.</span></span>

<span data-ttu-id="bf1ea-158">해당 hello Azure 서비스 버스 기능 hello Baltimore CyberTrust 루트 인증서 toobe JRE의의 일부로 설치 해야 **cacerts** 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-158">Note that hello Azure Service Bus functionality requires hello Baltimore CyberTrust Root certificate toobe installed as part of your JRE's **cacerts** store.</span></span> <span data-ttu-id="bf1ea-159">이 인증서가 자동으로 환경 JRE (Java Runtime)이이 자습서에서 사용 하는 hello에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-159">This certificate is automatically included in hello Java Runtime Environment (JRE) used by this tutorial.</span></span> <span data-ttu-id="bf1ea-160">경우 않아도이 인증서에 프로그램 JRE **cacerts** 저장소를 참조 하십시오 [Java CA 인증서 저장소 인증서 toohello 추가] [ add_ca_cert] 추가에 대 한 내용은 (으로 에 대 한 정보, cacerts 저장소에 hello 인증서 보기)</span><span class="sxs-lookup"><span data-stu-id="bf1ea-160">If you do not have this certificate in your JRE **cacerts** store, see [Adding a Certificate toohello Java CA Certificate Store][add_ca_cert] for information on adding it (as well as information on viewing hello certificates in your cacerts store).</span></span>

## <a name="how-toocreate-a-service-bus-namespace"></a><span data-ttu-id="bf1ea-161">어떻게 toocreate 서비스 버스 네임 스페이스</span><span class="sxs-lookup"><span data-stu-id="bf1ea-161">How toocreate a service bus namespace</span></span>
<span data-ttu-id="bf1ea-162">Azure에서 서비스 버스를 사용 하 여 toobegin 큐, 서비스 네임 스페이스를 먼저 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-162">toobegin using Service Bus queues in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="bf1ea-163">서비스 네임스페이스는 응용 프로그램 내에서 서비스 버스 리소스의 주소를 지정하기 위한 범위 컨테이너를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-163">A service namespace provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="bf1ea-164">서비스 네임 스페이스 toocreate:</span><span class="sxs-lookup"><span data-stu-id="bf1ea-164">toocreate a service namespace:</span></span>

1. <span data-ttu-id="bf1ea-165">Toohello 로그온 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-165">Log on toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="bf1ea-166">Hello hello Azure 클래식 포털의 왼쪽 아래 탐색 창에서 **서비스 버스, 액세스 제어 및 Caching**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-166">In hello lower-left navigation pane of hello Azure classic portal, click **Service Bus, Access Control & Caching**.</span></span>
3. <span data-ttu-id="bf1ea-167">Hello hello Azure 클래식 포털의 왼쪽 창에서 클릭 hello **서비스 버스** 노드를 hello를 클릭 한 다음 **새로** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-167">In hello upper-left pane of hello Azure classic portal, click hello **Service Bus** node, and then click hello **New** button.</span></span>  
   <span data-ttu-id="bf1ea-168">![서비스 버스 노드 스크린샷][svc_bus_node]</span><span class="sxs-lookup"><span data-stu-id="bf1ea-168">![Service Bus Node screenshot][svc_bus_node]</span></span>
4. <span data-ttu-id="bf1ea-169">Hello에 **새 서비스 Namespace를 만들** 대화 상자에 입력 한 **Namespace**, toomake를 고유한 지 클릭 하 고는 **가용성 확인** 단추 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-169">In hello **Create a new Service Namespace** dialog box, enter a **Namespace**, and then toomake sure that it is unique, click the **Check Availability** button.</span></span>  
   <span data-ttu-id="bf1ea-170">![새 네임스페이스 만들기 스크린샷][create_namespace]</span><span class="sxs-lookup"><span data-stu-id="bf1ea-170">![Create a New Namespace screenshot][create_namespace]</span></span>
5. <span data-ttu-id="bf1ea-171">된 hello 네임 스페이스 이름을 사용할 수 있는지 확인 한 후, 국가 또는 지역 하면 네임 스페이스를 호스팅해야 및 hello를 클릭 한 다음 선택 **만들 Namespace** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-171">After making sure hello namespace name is available, choose the country or region in which your namespace should be hosted, and then click hello **Create Namespace** button.</span></span>  
   
   <span data-ttu-id="bf1ea-172">hello 네임 스페이스를 만든 후 hello Azure 클래식 포털에에서 나타납니다 걸리고 순간 tooactivate 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-172">hello namespace you created will then appear in hello Azure classic portal and takes a moment tooactivate.</span></span> <span data-ttu-id="bf1ea-173">Hello 상태가 될 때까지 기다립니다 **활성** hello 다음 단계를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-173">Wait until hello status is **Active** before continuing with hello next step.</span></span>

## <a name="obtain-hello-default-management-credentials-for-hello-namespace"></a><span data-ttu-id="bf1ea-174">Hello 기본 관리 자격 증명을 가져올 hello 네임 스페이스에 대 한</span><span class="sxs-lookup"><span data-stu-id="bf1ea-174">Obtain hello Default Management Credentials for hello namespace</span></span>
<span data-ttu-id="bf1ea-175">Hello 새 네임 스페이스에 큐를 만들 때 처럼 순서 tooperform 관리 작업에는 네임 스페이스에 대 한 tooobtain hello 관리 자격 증명이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-175">In order tooperform management operations, such as creating a queue, on hello new namespace, you need tooobtain hello management credentials for the namespace.</span></span>

1. <span data-ttu-id="bf1ea-176">Hello 왼쪽된 탐색 창에서 클릭 hello **서비스 버스** 노드를 사용 가능한 네임 스페이스는 hello 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-176">In hello left navigation pane, click hello **Service Bus** node to display hello list of available namespaces.</span></span>
   <span data-ttu-id="bf1ea-177">![사용 가능한 네임스페이스 스크린샷][avail_namespaces]</span><span class="sxs-lookup"><span data-stu-id="bf1ea-177">![Available Namespaces screenshot][avail_namespaces]</span></span>
2. <span data-ttu-id="bf1ea-178">표시 된 hello 목록에서 방금 만든 hello 네임 스페이스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-178">Select hello namespace you just created from hello list shown.</span></span>
   <span data-ttu-id="bf1ea-179">![네임스페이스 목록 스크린샷][namespace_list]</span><span class="sxs-lookup"><span data-stu-id="bf1ea-179">![Namespace List screenshot][namespace_list]</span></span>
3. <span data-ttu-id="bf1ea-180">오른쪽 hello **속성** 창 새 네임 스페이스에 대 한 hello 속성을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-180">hello right-hand **Properties** pane lists hello properties for the new namespace.</span></span>
   <span data-ttu-id="bf1ea-181">![속성 창 스크린샷][properties_pane]</span><span class="sxs-lookup"><span data-stu-id="bf1ea-181">![Properties Pane screenshot][properties_pane]</span></span>
4. <span data-ttu-id="bf1ea-182">hello **기본 키** 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-182">hello **Default Key** is hidden.</span></span> <span data-ttu-id="bf1ea-183">Hello 클릭 **보기** toodisplay hello에 대 한 보안 자격 증명을 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-183">Click hello **View** button toodisplay hello security credentials.</span></span>
   <span data-ttu-id="bf1ea-184">![기본 키 스크린샷][default_key]</span><span class="sxs-lookup"><span data-stu-id="bf1ea-184">![Default Key screenshot][default_key]</span></span>
5. <span data-ttu-id="bf1ea-185">Hello 메모 **기본 발급자** 및 hello **기본 키** tooperform 작업 아래에이 정보를 사용 하 여 네임 스페이스와 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-185">Make a note of hello **Default Issuer** and hello **Default Key** as you will use this information below tooperform operations with the namespace.</span></span>

## <a name="how-toocreate-a-java-application-that-performs-a-compute-intensive-task"></a><span data-ttu-id="bf1ea-186">어떻게 toocreate 계산 집약적인 작업을 수행 하는 Java 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="bf1ea-186">How toocreate a Java application that performs a compute-intensive task</span></span>
1. <span data-ttu-id="bf1ea-187">개발 컴퓨터에서 (없는 만든 toobe hello 가상 컴퓨터)을 다운로드 hello [Azure SDK for Java](https://azure.microsoft.com/develop/java/)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-187">On your development machine (which does not have toobe hello virtual machine that you created), download hello [Azure SDK for Java](https://azure.microsoft.com/develop/java/).</span></span>
2. <span data-ttu-id="bf1ea-188">이 섹션의 hello 끝에 hello 예제 코드를 사용 하 여 Java 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-188">Create a Java console application using hello example code at hello end of this section.</span></span> <span data-ttu-id="bf1ea-189">이 자습서에서는 **TSPSolver.java** hello Java 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-189">In this tutorial, we'll use **TSPSolver.java** as hello Java file name.</span></span> <span data-ttu-id="bf1ea-190">Hello 수정 **프로그램\_서비스\_버스\_네임 스페이스**, **프로그램\_서비스\_버스\_소유자**, 및 **프로그램\_서비스\_버스\_키** 자리 표시자 toouse 서비스 버스 **네임 스페이스**, **기본 발급자** 및  **기본 키** 값을 각각.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-190">Modify hello **your\_service\_bus\_namespace**, **your\_service\_bus\_owner**, and **your\_service\_bus\_key** placeholders toouse your service bus **namespace**, **Default Issuer** and **Default Key** values, respectively.</span></span>
3. <span data-ttu-id="bf1ea-191">후 코딩, 내보내기 hello 응용 프로그램 tooa runnable Java 보관 파일 (JAR) 및 패키지 hello 필요 hello에 라이브러리 JAR을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-191">After coding, export hello application tooa runnable Java archive (JAR), and package hello required libraries into hello generated JAR.</span></span> <span data-ttu-id="bf1ea-192">이 자습서에서는 **TSPSolver.jar** 생성 hello JAR 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-192">In this tutorial, we'll use **TSPSolver.jar** as hello generated JAR name.</span></span>

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

        //  Value specifying how often tooprovide an update toohello console.
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

                int numCities = 10;  // Use as hello default, if no value is specified at command line.
                if (args.length != 0)
                {
                    if (args[0].toLowerCase().compareTo("createqueue")==0)
                    {
                        // No processing toooccur other than creating hello queue.
                        QueueInfo queueInfo = new QueueInfo("TSPQueue");

                        service.createQueue(queueInfo);

                        System.out.println("Queue named TSPQueue was created.");

                        System.exit(0);
                    }

                    if (args[0].toLowerCase().compareTo("deletequeue")==0)
                    {
                        // No processing toooccur other than deleting hello queue.
                        service.deleteQueue("TSPQueue");

                        System.out.println("Queue named TSPQueue was deleted.");

                        System.exit(0);
                    }

                    // Neither creating or deleting a queue.
                    // Assume hello value passed in is hello number of cities toosolve.
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



## <a name="how-toocreate-a-java-application-that-monitors-hello-progress-of-hello-compute-intensive-task"></a><span data-ttu-id="bf1ea-193">어떻게 toocreate 모니터링 하는 Java 응용 프로그램 hello hello 계산 집약적인 작업의 진행 상황</span><span class="sxs-lookup"><span data-stu-id="bf1ea-193">How toocreate a Java application that monitors hello progress of hello compute-intensive task</span></span>
1. <span data-ttu-id="bf1ea-194">개발 컴퓨터에서이 섹션의 hello 끝에 hello 예제 코드를 사용 하 여 Java 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-194">On your development machine, create a Java console application using hello example code at hello end of this section.</span></span> <span data-ttu-id="bf1ea-195">이 자습서에서는 **TSPClient.java** hello Java 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-195">In this tutorial, we'll use **TSPClient.java** as hello Java file name.</span></span> <span data-ttu-id="bf1ea-196">에서 설명한 것 처럼 수정 hello **프로그램\_서비스\_버스\_네임 스페이스**, **프로그램\_서비스\_버스\_소유자**, 및 **프로그램\_서비스\_버스\_키** 자리 표시자 toouse 서비스 버스 **네임 스페이스**, **기본 발급자**및 **기본 키** 값을 각각.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-196">As shown earlier, modify hello **your\_service\_bus\_namespace**, **your\_service\_bus\_owner**, and **your\_service\_bus\_key** placeholders toouse your service bus **namespace**, **Default Issuer** and **Default Key** values, respectively.</span></span>
2. <span data-ttu-id="bf1ea-197">Hello 응용 프로그램 tooa 내보내기 실행 가능한 JAR 및 패키지 hello hello에 라이브러리 생성 JAR 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-197">Export hello application tooa runnable JAR, and package hello required libraries into hello generated JAR.</span></span> <span data-ttu-id="bf1ea-198">이 자습서에서는 **TSPClient.jar** 생성 hello JAR 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-198">In this tutorial, we'll use **TSPClient.jar** as hello generated JAR name.</span></span>

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

                    int waitMinutes = 3;  // Use as hello default, if no value is specified at command line.
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

                            // Display hello queue message.
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
                                // No more processing toooccur.
                                date = new Date();
                                System.out.println("Finished at " + dateFormat.format(date) + ".");
                                break;
                            }
                        }
                        else
                        {
                            // hello queue is empty.
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

## <a name="how-toorun-hello-java-applications"></a><span data-ttu-id="bf1ea-199">어떻게 toorun hello Java 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="bf1ea-199">How toorun hello Java applications</span></span>
<span data-ttu-id="bf1ea-200">첫 번째 toocreate hello 큐 다음 toosolve hello 현재 최상의 경로 toohello 서비스 버스 큐를 추가 하는 여행 Saleseman 문제 hello hello 계산 집약적인 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-200">Run hello compute-intensive application, first toocreate hello queue, then toosolve hello Traveling Saleseman Problem, which will add hello current best route toohello service bus queue.</span></span> <span data-ttu-id="bf1ea-201">Hello 하는 동안 계산 집약적인 응용 프로그램은 실행 (또는 나중에) hello 서비스 버스 큐에서 실행된 hello 클라이언트 toodisplay 결과.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-201">While hello compute-intensive application is running (or afterwards), run hello client toodisplay results from hello service bus queue.</span></span>

### <a name="toorun-hello-compute-intensive-application"></a><span data-ttu-id="bf1ea-202">toorun hello 계산 집약적인 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="bf1ea-202">toorun hello compute-intensive application</span></span>
1. <span data-ttu-id="bf1ea-203">Tooyour 가상 컴퓨터에 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-203">Log on tooyour virtual machine.</span></span>
2. <span data-ttu-id="bf1ea-204">응용 프로그램을 실행할 폴더(예:</span><span class="sxs-lookup"><span data-stu-id="bf1ea-204">Create a folder where you will run your application.</span></span> <span data-ttu-id="bf1ea-205">**c:\TSP**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-205">For example, **c:\TSP**.</span></span>
3. <span data-ttu-id="bf1ea-206">복사 **TSPSolver.jar** 너무**c:\TSP**,</span><span class="sxs-lookup"><span data-stu-id="bf1ea-206">Copy **TSPSolver.jar** too**c:\TSP**,</span></span>
4. <span data-ttu-id="bf1ea-207">라는 파일을 만들어 **c:\TSP\cities.txt** 내용을 따라 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-207">Create a file named **c:\TSP\cities.txt** with hello following contents.</span></span>
   
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
5. <span data-ttu-id="bf1ea-208">명령 프롬프트에서 디렉터리 tooc:\TSP를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-208">At a command prompt, change directories tooc:\TSP.</span></span>
6. <span data-ttu-id="bf1ea-209">Hello JRE bin 폴더는 hello PATH 환경 변수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-209">Ensure hello JRE's bin folder is in hello PATH environment variable.</span></span>
7. <span data-ttu-id="bf1ea-210">Hello TSP solver 순열을 실행 하기 전에 toocreate hello 서비스 버스 큐를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-210">You'll need toocreate hello service bus queue before you run hello TSP solver permutations.</span></span> <span data-ttu-id="bf1ea-211">다음 명령 toocreate hello 서비스 버스 큐 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-211">Run hello following command toocreate hello service bus queue.</span></span>
   
        java -jar TSPSolver.jar createqueue
8. <span data-ttu-id="bf1ea-212">Hello 큐를 만든 했으므로 hello TSP solver 순열을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-212">Now that hello queue is created, you can run hello TSP solver permutations.</span></span> <span data-ttu-id="bf1ea-213">예를 들어 hello 명령 toorun hello solver 8 도시에 대 한 다음를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-213">For example, run hello following command toorun hello solver for 8 cities.</span></span>
   
        java -jar TSPSolver.jar 8
   
   <span data-ttu-id="bf1ea-214">숫자를 지정하지 않으면 10개 도시에 대해 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-214">If you don't specify a number, it will run for 10 cities.</span></span> <span data-ttu-id="bf1ea-215">Hello solver 현재 가장 짧은 경로 발견 하는 대로 추가 됩니다에 toohello 큐.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-215">As hello solver finds current shortest routes, it will add them toohello queue.</span></span>

> [!NOTE]
> <span data-ttu-id="bf1ea-216">더 큰 hello hello 번호 지정 하는, 긴 hello solver hello 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-216">hello larger hello number that you specify, hello longer hello solver will run.</span></span> <span data-ttu-id="bf1ea-217">예를 들어 14개 도시에 대해 실행하면 몇 분이 걸릴 수 있고, 15개 도시에 대해 실행하면 몇 시간이 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-217">For example, running for 14 cities could take several minutes, and running for 15 cities could take several hours.</span></span> <span data-ttu-id="bf1ea-218">런타임 (최종적 몇 주, 월 및 연도) 일 too16 또는 도시를 더 증가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-218">Increasing too16 or more cities could result in days of runtime (eventually weeks, months, and years).</span></span> <span data-ttu-id="bf1ea-219">Toohello 급증 hello 수 도시 증가로 해 hello 찾기 평가 순열의 hello 수 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-219">This is due toohello rapid increase in hello number of permutations evaluated by hello solver as hello number of cities increases.</span></span>
> 
> 

### <a name="how-toorun-hello-monitoring-client-application"></a><span data-ttu-id="bf1ea-220">어떻게 toorun hello 모니터링 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="bf1ea-220">How toorun hello monitoring client application</span></span>
1. <span data-ttu-id="bf1ea-221">Hello 클라이언트 응용 프로그램을 실행할 tooyour 컴퓨터에 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-221">Log on tooyour machine where you will run hello client application.</span></span> <span data-ttu-id="bf1ea-222">필요 하지 않습니다 toobe hello hello를 실행 하는 동일한 컴퓨터 **TSPSolver** 울 수 있지만 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-222">This does not need toobe hello same machine running hello **TSPSolver** application, although it can be.</span></span>
2. <span data-ttu-id="bf1ea-223">응용 프로그램을 실행할 폴더(예:</span><span class="sxs-lookup"><span data-stu-id="bf1ea-223">Create a folder where you will run your application.</span></span> <span data-ttu-id="bf1ea-224">**c:\TSP**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-224">For example, **c:\TSP**.</span></span>
3. <span data-ttu-id="bf1ea-225">복사 **TSPClient.jar** 너무**c:\TSP**,</span><span class="sxs-lookup"><span data-stu-id="bf1ea-225">Copy **TSPClient.jar** too**c:\TSP**,</span></span>
4. <span data-ttu-id="bf1ea-226">Hello JRE bin 폴더는 hello PATH 환경 변수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-226">Ensure hello JRE's bin folder is in hello PATH environment variable.</span></span>
5. <span data-ttu-id="bf1ea-227">명령 프롬프트에서 디렉터리 tooc:\TSP를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-227">At a command prompt, change directories tooc:\TSP.</span></span>
6. <span data-ttu-id="bf1ea-228">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-228">Run hello following command.</span></span>
   
        java -jar TSPClient.jar
   
    <span data-ttu-id="bf1ea-229">필요에 따라 명령줄 인수를 전달 하 여 hello 큐를 확인 하는 중 사이의 분 toosleep hello 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-229">Optionally, specify hello number of minutes toosleep in between checking hello queue, by passing in a command-line argument.</span></span> <span data-ttu-id="bf1ea-230">hello hello 큐를 확인 하기 위한 기본 절전 모드 시간은 3 분, 명령줄 인수를 전달 하지 너무 경우 사용 되는**TSPClient**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-230">hello default sleep period for checking hello queue is 3 minutes, which is used if no command-line argument is passed too**TSPClient**.</span></span> <span data-ttu-id="bf1ea-231">예를 들어 hello 대기 간격에 대 한 원하는 toouse 다른 값을 1 분 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-231">If you want toouse a different value for hello sleep interval, for example, one minute, run hello following command.</span></span>
   
        java -jar TSPClient.jar 1
   
    <span data-ttu-id="bf1ea-232">클라이언트 hello "완료"의 큐 메시지를 발견할 때까지 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-232">hello client will run until it sees a queue message of "Complete".</span></span> <span data-ttu-id="bf1ea-233">참고 hello 클라이언트를 실행 하지 않고 hello solver 여러 번을 실행 하면 toorun hello 클라이언트 여러 번 toocompletely 빈 hello 큐를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-233">Note that if you run multiple occurrences of hello solver without running hello client, you may need toorun hello client multiple times toocompletely empty hello queue.</span></span> <span data-ttu-id="bf1ea-234">또는 hello 큐를 삭제 한 후 다시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-234">Alternatively, you can delete hello queue and then create it again.</span></span> <span data-ttu-id="bf1ea-235">hello 다음 실행 toodelete hello 큐 **TSPSolver** (하지 **TSPClient**) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-235">toodelete hello queue, run hello following **TSPSolver** (not **TSPClient**)  command.</span></span>
   
        java -jar TSPSolver.jar deletequeue
   
    <span data-ttu-id="bf1ea-236">hello solver 모든 경로 검사를 완료 될 때까지 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-236">hello solver will run until it finishes examining all routes.</span></span>

## <a name="how-toostop-hello-java-applications"></a><span data-ttu-id="bf1ea-237">어떻게 toostop hello Java 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="bf1ea-237">How toostop hello Java applications</span></span>
<span data-ttu-id="bf1ea-238">Hello solver와 클라이언트 응용 프로그램에 대 한 누르면 **Ctrl + C** tooexit tooend 이전 toonormal 완료 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="bf1ea-238">For both hello solver and client applications, you can press **Ctrl+C** tooexit if you want tooend prior toonormal completion.</span></span>

[solver_output]:media/java-run-compute-intensive-task/WA_JavaTSPSolver.png
[client_output]:media/java-run-compute-intensive-task/WA_JavaTSPClient.png
[svc_bus_node]:media/java-run-compute-intensive-task/SvcBusQueues_02_SvcBusNode.jpg
[create_namespace]:media/java-run-compute-intensive-task/SvcBusQueues_03_CreateNewSvcNamespace.jpg
[avail_namespaces]:media/java-run-compute-intensive-task/SvcBusQueues_04_SvcBusNode_AvailNamespaces.jpg
[namespace_list]:media/java-run-compute-intensive-task/SvcBusQueues_05_NamespaceList.jpg
[properties_pane]:media/java-run-compute-intensive-task/SvcBusQueues_06_PropertiesPane.jpg
[default_key]:media/java-run-compute-intensive-task/SvcBusQueues_07_DefaultKey.jpg
[add_ca_cert]: ../../../java-add-certificate-ca-store.md
