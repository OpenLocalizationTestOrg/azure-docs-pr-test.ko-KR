---
title: "사용 하 여 가상 컴퓨터 aaaManage IntelliJ에 대 한 Azure 탐색기 hello | Microsoft Docs"
description: "어떻게 toomanage Azure 가상 컴퓨터를 사용 하 여 hello Azure 탐색기에 대 한 자세한 내용은 IntelliJ 합니다."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: a73dd4f73b311dd3413f6712e3b76c36ee464de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-intellij"></a><span data-ttu-id="75b99-103">IntelliJ 용 hello Azure 탐색기를 사용 하 여 가상 컴퓨터를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-103">Manage virtual machines by using hello Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="75b99-104">hello hello IntelliJ 용 Azure 도구 키트의 일부인 Azure 탐색기의 Azure 계정과에서에서 가상 컴퓨터를 관리 하기 위한 사용 하기 쉬운 솔루션과 Java 개발자가 제공 hello IntelliJ 통합된 개발 환경 (IDE) 안에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-104">hello Azure Explorer, which is part of hello Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside hello IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a><span data-ttu-id="75b99-105">IntelliJ에서 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="75b99-105">Create a virtual machine in IntelliJ</span></span>

<span data-ttu-id="75b99-106">toocreate hello Azure 탐색기를 사용 하 여 가상 컴퓨터는 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-106">toocreate a virtual machine by using hello Azure Explorer, do hello following:</span></span> 

1. <span data-ttu-id="75b99-107">Hello hello 단계를 사용 하 여 tooyour Azure 계정에에서 로그인 [로그인에 대 한 지침 Azure 도구 키트 hello IntelliJ] 문서.</span><span class="sxs-lookup"><span data-stu-id="75b99-107">Sign in tooyour Azure account by using hello steps in hello [Sign-in instructions for hello Azure Toolkit for IntelliJ] article.</span></span>

2. <span data-ttu-id="75b99-108">Hello에 **Azure 탐색기** 보기, 확장 hello **Azure** 노드를 마우스 오른쪽 단추로 클릭 **가상 컴퓨터**, 클릭 하 고 **VM 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-108">In hello **Azure Explorer** view, expand hello **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span> 

   <span data-ttu-id="75b99-109">![hello VM 만들기 명령][CR01]</span><span class="sxs-lookup"><span data-stu-id="75b99-109">![hello Create VM command][CR01]</span></span>  
    <span data-ttu-id="75b99-110">hello **새 가상 컴퓨터 만들기** 마법사가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-110">hello **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="75b99-111">Hello에 **구독 선택** 창에서 구독을 선택한 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-111">In hello **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span> 

   ![hello 선택 구독 창][CR02]

4. <span data-ttu-id="75b99-113">Hello에 **가상 컴퓨터 이미지 선택** 창의 hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-113">In hello **Select a Virtual Machine Image** window, enter hello following information:</span></span>

   * <span data-ttu-id="75b99-114">**위치**: 가상 컴퓨터를 만들 위치(예: *미국 서부*)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span> 

   * <span data-ttu-id="75b99-115">**권장 이미지**: 일반적으로 사용되는 이미지의 요약 목록에서 이미지를 선택하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-115">**Recommended image**: Specifies that you will choose an image from an abbreviated list of commonly used images.</span></span>

   * <span data-ttu-id="75b99-116">**사용자 지정 이미지**: 지정 hello 다음 정보를 제공 하 여 사용자 지정 이미지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-116">**Custom image**: Specifies that you will choose a custom image by providing hello following information:</span></span>

      * <span data-ttu-id="75b99-117">**게시자**: 가상 컴퓨터에 사용할 hello 이미지를 만든 hello 게시자를 지정 합니다 (예를 들어 *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="75b99-117">**Publisher**: Specifies hello publisher that created hello image that you will use for your virtual machine (for example, *Microsoft*).</span></span>

      * <span data-ttu-id="75b99-118">**제공**: toouse hello 선택한 게시자에서 제공 하는 hello 가상 컴퓨터를 지정 합니다 (예를 들어 *JDK*).</span><span class="sxs-lookup"><span data-stu-id="75b99-118">**Offer**: Specifies hello virtual machine offering toouse from hello selected publisher (for example, *JDK*).</span></span>

      * <span data-ttu-id="75b99-119">**Sku**: hello stockkeeping 단위 (SKU) toouse hello 선택한를 지정 합니다 (예를 들어 *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="75b99-119">**Sku**: Specifies hello stockkeeping unit (SKU) toouse from hello selected offering (for example, *JDK_8*).</span></span>

      * <span data-ttu-id="75b99-120">**버전 #**: 버전을 선택 하는 hello 지정 SKU toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-120">**Version #**: Specifies which version of hello selected SKU toouse.</span></span>

   ![가상 컴퓨터 이미지 기간을 선택 하는 hello][CR03]

5. <span data-ttu-id="75b99-122">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-122">Click **Next**.</span></span> 

6. <span data-ttu-id="75b99-123">Hello에 **가상 컴퓨터 기본 설정** 창의 hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-123">In hello **Virtual Machine Basic Settings** window, enter hello following information:</span></span>

   * <span data-ttu-id="75b99-124">**가상 컴퓨터 이름**: 문자로 시작 하 고 문자, 숫자 및 하이픈만 포함 해야 하는 새 가상 컴퓨터에 대 한 hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-124">**Virtual machine name**: Specifies hello name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="75b99-125">**크기**: 코어와 메모리 tooallocate 가상 컴퓨터에 대 한 hello 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-125">**Size**: Specifies hello number of cores and memory tooallocate for your virtual machine.</span></span>

   * <span data-ttu-id="75b99-126">**사용자 이름**: 가상 컴퓨터를 관리 하기 위한 관리자 계정 toocreate hello를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-126">**User name**: Specifies hello administrator account toocreate for managing your virtual machine.</span></span>

   * <span data-ttu-id="75b99-127">**암호** 및 **Confirm**: hello 프로그램 관리자 계정의 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-127">**Password** and **Confirm**: Specifies hello password for your administrator account.</span></span>

   ![hello 가상 컴퓨터 기본 설정 창][CR04]

7. <span data-ttu-id="75b99-129">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-129">Click **Next**.</span></span> 

8. <span data-ttu-id="75b99-130">Hello에 **연결 된 리소스** 창 hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-130">In hello **Associated Resources** window, enter hello following information:</span></span>

   * <span data-ttu-id="75b99-131">**리소스 그룹**: 가상 컴퓨터에 대 한 hello 리소스 그룹을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-131">**Resource group**: Specifies hello resource group for your virtual machine.</span></span> <span data-ttu-id="75b99-132">Hello 다음 옵션 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-132">Select one of hello following options:</span></span>
      * <span data-ttu-id="75b99-133">**새로 만들기**: toocreate 새 리소스 그룹 한다고 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-133">**Create new**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="75b99-134">**기존 항목 사용**: Azure 계정에 연관 된 리소스 그룹의 목록에서 tooselect 한다고 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-134">**Use existing**: Specifies that you want tooselect from a list of resource groups that are associated with your Azure account.</span></span>

       ![hello 연결 된 리소스 창][CR07]

   * <span data-ttu-id="75b99-136">**저장소 계정**: 가상 컴퓨터를 저장 하기 위한 저장소 계정 toouse hello를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-136">**Storage account**: Specifies hello storage account toouse for storing your virtual machine.</span></span> <span data-ttu-id="75b99-137">기존 저장소 계정을 사용하거나 새 저장소 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-137">You can choose an existing storage account or create a new account.</span></span> <span data-ttu-id="75b99-138">선택 하면 **새로 만들기**, hello 다음 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-138">If you choose **Create New**, hello following dialog box appears:</span></span>

      ![hello 저장소 계정 만들기 대화 상자][CR05]

   * <span data-ttu-id="75b99-140">**가상 네트워크** 및 **서브넷**: hello 가상 네트워크 및 가상 컴퓨터에 연결 하는 서브넷을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-140">**Virtual Network** and **Subnet**: Specifies hello virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="75b99-141">기존 네트워크 및 서브넷을 사용하거나 새 네트워크 및 서브넷을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-141">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="75b99-142">선택 하는 경우 **새로 만들기**, hello 다음 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-142">If you select **Create new**, hello following dialog box appears:</span></span>

      ![hello 가상 네트워크 만들기 대화 상자][CR06]

   * <span data-ttu-id="75b99-144">**공용 IP 주소**: 가상 컴퓨터에 대한 외부 연결 IP 주소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-144">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="75b99-145">Toocreate 새 IP 주소를 선택할 수 있습니다 또는 선택할 수 가상 컴퓨터에는 공용 IP 주소를 없으면 **(없음)**합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-145">You can choose toocreate a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span> 

   * <span data-ttu-id="75b99-146">**네트워크 보안 그룹**: 가상 컴퓨터에 대한 선택적 네트워킹 방화벽을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-146">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="75b99-147">기존 방화벽을 선택하거나, 가상 컴퓨터에서 네트워크 방화벽을 사용하지 않을 경우 **(없음)**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-147">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span> 

   * <span data-ttu-id="75b99-148">**가용성 집합**: 가상 컴퓨터가 속할 선택적 가용성 집합을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-148">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="75b99-149">수 기존 가용성 집합, 새 가용성 집합 만들기를 선택 하거나 가상 컴퓨터 tooan 가용성 집합에 속하지 것입니다 선택 **(없음)**합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-149">You can select an existing availability set, create a new availability set or, if your virtual machine will not belong tooan availability set, select **(None)**.</span></span>

9. <span data-ttu-id="75b99-150">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-150">Click **Finish**.</span></span>  
    <span data-ttu-id="75b99-151">새 가상 컴퓨터에 hello Azure 탐색기 도구 창에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-151">Your new virtual machine appears in hello Azure Explorer tool window.</span></span> 

   ![Hello Azure 탐색기 보기에서에서 새 가상 컴퓨터][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a><span data-ttu-id="75b99-153">IntelliJ에서 가상 컴퓨터 다시 시작</span><span class="sxs-lookup"><span data-stu-id="75b99-153">Restart a virtual machine in IntelliJ</span></span>

<span data-ttu-id="75b99-154">toorestart IntelliJ의 hello Azure 탐색기를 사용 하 여 가상 컴퓨터는 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-154">toorestart a virtual machine by using hello Azure Explorer in IntelliJ, do hello following:</span></span>

1. <span data-ttu-id="75b99-155">Hello에 **Azure 탐색기** 확인, hello 가상 컴퓨터를 마우스 오른쪽 단추로 클릭 한 다음 선택 **다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-155">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Restart**.</span></span>

   ![가상 컴퓨터 다시 시작 명령을 hello합니다][RE01]

2. <span data-ttu-id="75b99-157">Hello 확인 창에서 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-157">In hello confirmation window, click **Yes**.</span></span> 

   ![hello 확인 창 가상 컴퓨터를 다시 시작][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a><span data-ttu-id="75b99-159">IntelliJ에서 가상 컴퓨터 종료</span><span class="sxs-lookup"><span data-stu-id="75b99-159">Shut down a virtual machine in IntelliJ</span></span>

<span data-ttu-id="75b99-160">IntelliJ의 hello Azure 탐색기를 사용 하 여 실행 중인 가상 컴퓨터를 tooshut 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-160">tooshut down a running virtual machine by using hello Azure Explorer in IntelliJ, do hello following:</span></span>

1. <span data-ttu-id="75b99-161">Hello에 **Azure 탐색기** 확인, hello 가상 컴퓨터를 마우스 오른쪽 단추로 클릭 한 다음 선택 **종료**합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-161">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Shutdown**.</span></span>

   ![가상 컴퓨터 종료 명령은 hello][SH01]

2. <span data-ttu-id="75b99-163">Hello 확인 창에서 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-163">In hello confirmation window, click **Yes**.</span></span> 

   ![확인 창 가상 컴퓨터를 종료 하는 hello][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a><span data-ttu-id="75b99-165">IntelliJ에서 가상 컴퓨터 삭제</span><span class="sxs-lookup"><span data-stu-id="75b99-165">Delete a virtual machine in IntelliJ</span></span>

<span data-ttu-id="75b99-166">toodelete IntelliJ의 hello Azure 탐색기를 사용 하 여 가상 컴퓨터는 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-166">toodelete a virtual machine by using hello Azure Explorer in IntelliJ, do hello following:</span></span>

1. <span data-ttu-id="75b99-167">Hello에 **Azure 탐색기** 확인, hello 가상 컴퓨터를 마우스 오른쪽 단추로 클릭 한 다음 선택 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-167">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Delete**.</span></span>

   ![hello 가상 컴퓨터 삭제 명령][DE01]

2. <span data-ttu-id="75b99-169">Hello 확인 창에서 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="75b99-169">In hello confirmation window, click **Yes**.</span></span> 

   ![hello 확인 창 가상 컴퓨터를 삭제 합니다.][DE02]

## <a name="next-steps"></a><span data-ttu-id="75b99-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="75b99-171">Next steps</span></span>
<span data-ttu-id="75b99-172">Azure 가상 컴퓨터 크기 및 가격에 대 한 자세한 내용은 다음 리소스는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="75b99-172">For more information about Azure virtual-machine sizes and pricing, see hello following resources:</span></span>

* <span data-ttu-id="75b99-173">Azure Virtual Machines 크기</span><span class="sxs-lookup"><span data-stu-id="75b99-173">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="75b99-174">[Azure에서 Windows 가상 컴퓨터에 대한 크기]</span><span class="sxs-lookup"><span data-stu-id="75b99-174">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="75b99-175">[Azure에서 Linux 가상 컴퓨터에 대한 크기]</span><span class="sxs-lookup"><span data-stu-id="75b99-175">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="75b99-176">Azure Virtual Machines 가격 책정</span><span class="sxs-lookup"><span data-stu-id="75b99-176">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="75b99-177">[Windows 가상 컴퓨터 가격 책정]</span><span class="sxs-lookup"><span data-stu-id="75b99-177">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="75b99-178">[Linux 가상 컴퓨터 가격 책정]</span><span class="sxs-lookup"><span data-stu-id="75b99-178">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="75b99-179">Java Ide에 대 한 hello Azure 도구 키트에 대 한 자세한 내용은 hello 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="75b99-179">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="75b99-180">[Eclipse용 Azure 도구 키트]</span><span class="sxs-lookup"><span data-stu-id="75b99-180">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="75b99-181">[Hello Eclipse 용 Azure 도구 키트의에서 새로운 기능]</span><span class="sxs-lookup"><span data-stu-id="75b99-181">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="75b99-182">[Hello Eclipse 용 Azure 도구 키트 설치]</span><span class="sxs-lookup"><span data-stu-id="75b99-182">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="75b99-183">[Eclipse 용 Azure 도구 키트 hello에 대 한 로그인 지침]</span><span class="sxs-lookup"><span data-stu-id="75b99-183">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="75b99-184">[Eclipse에서 Azure용 Hello World 웹앱 만들기]</span><span class="sxs-lookup"><span data-stu-id="75b99-184">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="75b99-185">[IntelliJ용 Azure 도구 키트]</span><span class="sxs-lookup"><span data-stu-id="75b99-185">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="75b99-186">[Hello IntelliJ 용 Azure 도구 키트의에서 새로운 기능]</span><span class="sxs-lookup"><span data-stu-id="75b99-186">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="75b99-187">[IntelliJ 용 hello Azure 도구 키트 설치]</span><span class="sxs-lookup"><span data-stu-id="75b99-187">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="75b99-188">[로그인에 대 한 지침 Azure 도구 키트 hello IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="75b99-188">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="75b99-189">[IntelliJ에서 Azure용 Hello World 웹앱 만들기]</span><span class="sxs-lookup"><span data-stu-id="75b99-189">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="75b99-190">Java와 함께 Azure를 사용하는 것에 대한 자세한 내용은 [Azure Java 개발자 센터] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75b99-190">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Eclipse용 Azure 도구 키트]: ./azure-toolkit-for-eclipse.md
[IntelliJ용 Azure 도구 키트]: ./azure-toolkit-for-intellij.md
[Eclipse에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[IntelliJ에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Hello Eclipse 용 Azure 도구 키트 설치]: ./azure-toolkit-for-eclipse-installation.md
[IntelliJ 용 hello Azure 도구 키트 설치]: ./azure-toolkit-for-intellij-installation.md
[Eclipse 용 Azure 도구 키트 hello에 대 한 로그인 지침]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[로그인에 대 한 지침 Azure 도구 키트 hello IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Hello Eclipse 용 Azure 도구 키트의에서 새로운 기능]: ./azure-toolkit-for-eclipse-whats-new.md
[Hello IntelliJ 용 Azure 도구 키트의에서 새로운 기능]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/
[Visual Studio Team Services용 Java 도구]: https://java.visualstudio.com/

[Azure에서 Windows 가상 컴퓨터에 대한 크기]: /azure/virtual-machines/virtual-machines-windows-sizes
[Azure에서 Linux 가상 컴퓨터에 대한 크기]: /azure/virtual-machines/virtual-machines-linux-sizes
[Windows 가상 컴퓨터 가격 책정]: /pricing/details/virtual-machines/windows/
[Linux 가상 컴퓨터 가격 책정]: /pricing/details/virtual-machines/linux/


<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR08.png
