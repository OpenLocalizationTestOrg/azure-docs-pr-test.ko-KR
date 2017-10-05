---
title: "IntelliJ용 Azure Explorer를 사용하여 Virtual Machines 관리 | Microsoft Docs"
description: "IntelliJ용 Azure 탐색기를 사용하여 Azure Virtual Machines를 관리하는 방법을 알아봅니다."
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
ms.openlocfilehash: 9197580407b3509fbf9a842e1fee1e6348478c34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-intellij"></a><span data-ttu-id="6460d-103">IntelliJ용 Azure Explorer를 사용하여 Virtual Machines 관리</span><span class="sxs-lookup"><span data-stu-id="6460d-103">Manage virtual machines by using the Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="6460d-104">IntelliJ용 Azure 도구 키트의 일부인 Azure Explorer는 IntelliJ IDE(통합 개발 환경) 내에서 Azure 계정의 Virtual Machines를 관리하기 위한 사용하기 쉬운 솔루션을 Java 개발자에게 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-104">The Azure Explorer, which is part of the Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside the IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a><span data-ttu-id="6460d-105">IntelliJ에서 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="6460d-105">Create a virtual machine in IntelliJ</span></span>

<span data-ttu-id="6460d-106">Azure Explorer를 사용하여 가상 컴퓨터를 만들려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-106">To create a virtual machine by using the Azure Explorer, do the following:</span></span> 

1. <span data-ttu-id="6460d-107">[IntelliJ용 Azure 도구 키트에 대한 로그인 지침] 문서의 단계를 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-107">Sign in to your Azure account by using the steps in the [Sign-in instructions for the Azure Toolkit for IntelliJ] article.</span></span>

2. <span data-ttu-id="6460d-108">**Azure Explorer** 보기에서 **Azure** 노드를 확장하고 **Virtual Machines**를 마우스 오른쪽 단추로 클릭한 후 **VM 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span> 

   <span data-ttu-id="6460d-109">![VM 만들기 명령][CR01]</span><span class="sxs-lookup"><span data-stu-id="6460d-109">![The Create VM command][CR01]</span></span>  
    <span data-ttu-id="6460d-110">**새 가상 컴퓨터 만들기** 마법사가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-110">The **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="6460d-111">**구독 선택** 창에서 구독을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-111">In the **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span> 

   ![구독 선택 창][CR02]

4. <span data-ttu-id="6460d-113">**가상 컴퓨터 이미지 선택** 창에서 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-113">In the **Select a Virtual Machine Image** window, enter the following information:</span></span>

   * <span data-ttu-id="6460d-114">**위치**: 가상 컴퓨터를 만들 위치(예: *미국 서부*)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span> 

   * <span data-ttu-id="6460d-115">**권장 이미지**: 일반적으로 사용되는 이미지의 요약 목록에서 이미지를 선택하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-115">**Recommended image**: Specifies that you will choose an image from an abbreviated list of commonly used images.</span></span>

   * <span data-ttu-id="6460d-116">**사용자 지정 이미지**: 다음 정보를 제공하여 사용자 지정 이미지를 선택하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-116">**Custom image**: Specifies that you will choose a custom image by providing the following information:</span></span>

      * <span data-ttu-id="6460d-117">**게시자**: 가상 컴퓨터에 사용할 이미지를 만든 게시자를 지정합니다(예: *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="6460d-117">**Publisher**: Specifies the publisher that created the image that you will use for your virtual machine (for example, *Microsoft*).</span></span>

      * <span data-ttu-id="6460d-118">**제품**: 선택한 게시자에서 사용할 가상 컴퓨터 제품을 지정합니다(예: *JDK*).</span><span class="sxs-lookup"><span data-stu-id="6460d-118">**Offer**: Specifies the virtual machine offering to use from the selected publisher (for example, *JDK*).</span></span>

      * <span data-ttu-id="6460d-119">**SKU**: 선택한 제품에서 사용할 SKU(Stockkeeping Unit)를 지정합니다(예: *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="6460d-119">**Sku**: Specifies the stockkeeping unit (SKU) to use from the selected offering (for example, *JDK_8*).</span></span>

      * <span data-ttu-id="6460d-120">**버전 번호**: 선택한 SKU에서 사용할 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-120">**Version #**: Specifies which version of the selected SKU to use.</span></span>

   ![가상 컴퓨터 이미지 선택 창][CR03]

5. <span data-ttu-id="6460d-122">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-122">Click **Next**.</span></span> 

6. <span data-ttu-id="6460d-123">**가상 컴퓨터 기본 설정** 창에서 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-123">In the **Virtual Machine Basic Settings** window, enter the following information:</span></span>

   * <span data-ttu-id="6460d-124">**가상 컴퓨터 이름**: 새 가상 컴퓨터의 이름을 지정합니다. 이름은 문자로 시작하고 문자, 숫자 및 하이픈만 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-124">**Virtual machine name**: Specifies the name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="6460d-125">**크기**: 가상 컴퓨터용으로 할당할 코어 수 및 메모리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-125">**Size**: Specifies the number of cores and memory to allocate for your virtual machine.</span></span>

   * <span data-ttu-id="6460d-126">**사용자 이름**: 가상 컴퓨터를 관리하기 위해 만들 관리자 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-126">**User name**: Specifies the administrator account to create for managing your virtual machine.</span></span>

   * <span data-ttu-id="6460d-127">**암호** 및 **확인**: 관리자 계정의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-127">**Password** and **Confirm**: Specifies the password for your administrator account.</span></span>

   ![가상 컴퓨터 기본 설정 창][CR04]

7. <span data-ttu-id="6460d-129">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-129">Click **Next**.</span></span> 

8. <span data-ttu-id="6460d-130">**연결된 리소스** 창에서 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-130">In the **Associated Resources** window, enter the following information:</span></span>

   * <span data-ttu-id="6460d-131">**리소스 그룹**: 가상 컴퓨터에 사용할 리소스 그룹을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-131">**Resource group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="6460d-132">다음 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-132">Select one of the following options:</span></span>
      * <span data-ttu-id="6460d-133">**새로 만들기**: 새 리소스 그룹을 만들도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-133">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="6460d-134">**기존 그룹 사용**: Azure 계정에 연결된 리소스 그룹 목록에서 선택하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-134">**Use existing**: Specifies that you want to select from a list of resource groups that are associated with your Azure account.</span></span>

       ![연결된 리소스 창][CR07]

   * <span data-ttu-id="6460d-136">**저장소 계정**: 가상 컴퓨터를 저장하는 데 사용할 저장소 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-136">**Storage account**: Specifies the storage account to use for storing your virtual machine.</span></span> <span data-ttu-id="6460d-137">기존 저장소 계정을 사용하거나 새 저장소 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-137">You can choose an existing storage account or create a new account.</span></span> <span data-ttu-id="6460d-138">**새로 만들기**를 선택하면 다음 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-138">If you choose **Create New**, the following dialog box appears:</span></span>

      ![저장소 계정 만들기 대화 상자][CR05]

   * <span data-ttu-id="6460d-140">**가상 네트워크** 및 **서브넷**: 가상 컴퓨터가 연결될 가상 네트워크 및 서브넷을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-140">**Virtual Network** and **Subnet**: Specifies the virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="6460d-141">기존 네트워크 및 서브넷을 사용하거나 새 네트워크 및 서브넷을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-141">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="6460d-142">**새로 만들기**를 선택하는 경우 다음과 같은 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-142">If you select **Create new**, the following dialog box appears:</span></span>

      ![가상 네트워크 만들기 대화 상자][CR06]

   * <span data-ttu-id="6460d-144">**공용 IP 주소**: 가상 컴퓨터에 대한 외부 연결 IP 주소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-144">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="6460d-145">새 IP 주소를 만들도록 선택하거나, 가상 컴퓨터에 공용 IP 주소가 없는 경우 **(없음)**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-145">You can choose to create a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span> 

   * <span data-ttu-id="6460d-146">**네트워크 보안 그룹**: 가상 컴퓨터에 대한 선택적 네트워킹 방화벽을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-146">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="6460d-147">기존 방화벽을 선택하거나, 가상 컴퓨터에서 네트워크 방화벽을 사용하지 않을 경우 **(없음)**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-147">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span> 

   * <span data-ttu-id="6460d-148">**가용성 집합**: 가상 컴퓨터가 속할 선택적 가용성 집합을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-148">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="6460d-149">기존 가용성 집합을 선택하거나, 새 가용성 집합을 만들거나, 가상 컴퓨터가 가용성 집합에 속하지 않을 경우 **(없음)**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-149">You can select an existing availability set, create a new availability set or, if your virtual machine will not belong to an availability set, select **(None)**.</span></span>

9. <span data-ttu-id="6460d-150">**Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-150">Click **Finish**.</span></span>  
    <span data-ttu-id="6460d-151">새 가상 컴퓨터가 Azure Explorer 도구 창에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-151">Your new virtual machine appears in the Azure Explorer tool window.</span></span> 

   ![Azure Explorer 보기의 새 가상 컴퓨터][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a><span data-ttu-id="6460d-153">IntelliJ에서 가상 컴퓨터 다시 시작</span><span class="sxs-lookup"><span data-stu-id="6460d-153">Restart a virtual machine in IntelliJ</span></span>

<span data-ttu-id="6460d-154">IntelliJ에서 Azure Explorer를 사용하여 가상 컴퓨터를 다시 시작하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-154">To restart a virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="6460d-155">**Azure Explorer** 보기에서 가상 컴퓨터를 마우스 오른쪽 단추로 클릭하고 **다시 시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-155">In the **Azure Explorer** view, right-click the virtual machine, and then select **Restart**.</span></span>

   ![가상 컴퓨터 다시 시작 명령][RE01]

2. <span data-ttu-id="6460d-157">확인 창에서 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-157">In the confirmation window, click **Yes**.</span></span> 

   ![가상 컴퓨터 다시 시작 확인 창][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a><span data-ttu-id="6460d-159">IntelliJ에서 가상 컴퓨터 종료</span><span class="sxs-lookup"><span data-stu-id="6460d-159">Shut down a virtual machine in IntelliJ</span></span>

<span data-ttu-id="6460d-160">IntelliJ에서 Azure Explorer를 사용하여 가상 컴퓨터를 종료하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-160">To shut down a running virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="6460d-161">**Azure Explorer** 보기에서 가상 컴퓨터를 마우스 오른쪽 단추로 클릭하고 **종료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-161">In the **Azure Explorer** view, right-click the virtual machine, and then select **Shutdown**.</span></span>

   ![가상 컴퓨터 종료 명령][SH01]

2. <span data-ttu-id="6460d-163">확인 창에서 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-163">In the confirmation window, click **Yes**.</span></span> 

   ![가상 컴퓨터 종료 확인 창][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a><span data-ttu-id="6460d-165">IntelliJ에서 가상 컴퓨터 삭제</span><span class="sxs-lookup"><span data-stu-id="6460d-165">Delete a virtual machine in IntelliJ</span></span>

<span data-ttu-id="6460d-166">IntelliJ에서 Azure Explorer를 사용하여 가상 컴퓨터를 삭제하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-166">To delete a virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="6460d-167">**Azure Explorer** 보기에서 가상 컴퓨터를 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-167">In the **Azure Explorer** view, right-click the virtual machine, and then select **Delete**.</span></span>

   ![가상 컴퓨터 삭제 명령][DE01]

2. <span data-ttu-id="6460d-169">확인 창에서 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6460d-169">In the confirmation window, click **Yes**.</span></span> 

   ![가상 컴퓨터 삭제 확인 창][DE02]

## <a name="next-steps"></a><span data-ttu-id="6460d-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6460d-171">Next steps</span></span>
<span data-ttu-id="6460d-172">Azure 가상 컴퓨터 크기 및 가격 책정에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6460d-172">For more information about Azure virtual-machine sizes and pricing, see the following resources:</span></span>

* <span data-ttu-id="6460d-173">Azure Virtual Machines 크기</span><span class="sxs-lookup"><span data-stu-id="6460d-173">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="6460d-174">[Azure에서 Windows 가상 컴퓨터에 대한 크기]</span><span class="sxs-lookup"><span data-stu-id="6460d-174">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="6460d-175">[Azure에서 Linux 가상 컴퓨터에 대한 크기]</span><span class="sxs-lookup"><span data-stu-id="6460d-175">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="6460d-176">Azure Virtual Machines 가격 책정</span><span class="sxs-lookup"><span data-stu-id="6460d-176">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="6460d-177">[Windows 가상 컴퓨터 가격 책정]</span><span class="sxs-lookup"><span data-stu-id="6460d-177">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="6460d-178">[Linux 가상 컴퓨터 가격 책정]</span><span class="sxs-lookup"><span data-stu-id="6460d-178">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="6460d-179">Java IDE용 Azure 도구 키트에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6460d-179">For more information about the Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="6460d-180">[Eclipse용 Azure 도구 키트]</span><span class="sxs-lookup"><span data-stu-id="6460d-180">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="6460d-181">[Eclipse용 Azure 도구 키트의 새로운 기능]</span><span class="sxs-lookup"><span data-stu-id="6460d-181">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="6460d-182">[Eclipse용 Azure 도구 키트 설치]</span><span class="sxs-lookup"><span data-stu-id="6460d-182">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="6460d-183">[Eclipse용 Azure 도구 키트에 대한 로그인 지침]</span><span class="sxs-lookup"><span data-stu-id="6460d-183">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="6460d-184">[Eclipse에서 Azure용 Hello World 웹앱 만들기]</span><span class="sxs-lookup"><span data-stu-id="6460d-184">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="6460d-185">[IntelliJ용 Azure 도구 키트]</span><span class="sxs-lookup"><span data-stu-id="6460d-185">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="6460d-186">[IntelliJ용 Azure 도구 키트의 새로운 기능]</span><span class="sxs-lookup"><span data-stu-id="6460d-186">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="6460d-187">[IntelliJ용 Azure 도구 키트 설치]</span><span class="sxs-lookup"><span data-stu-id="6460d-187">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="6460d-188">[IntelliJ용 Azure 도구 키트에 대한 로그인 지침]</span><span class="sxs-lookup"><span data-stu-id="6460d-188">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="6460d-189">[IntelliJ에서 Azure용 Hello World 웹앱 만들기]</span><span class="sxs-lookup"><span data-stu-id="6460d-189">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="6460d-190">Java와 함께 Azure를 사용하는 것에 대한 자세한 내용은 [Azure Java 개발자 센터] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6460d-190">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="6460d-191">[Eclipse용 Azure 도구 키트]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="6460d-191">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="6460d-192">[IntelliJ용 Azure 도구 키트]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="6460d-192">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="6460d-193">[Eclipse에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="6460d-193">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="6460d-194">[IntelliJ에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="6460d-194">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="6460d-195">[Eclipse용 Azure 도구 키트 설치]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="6460d-195">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="6460d-196">[IntelliJ용 Azure 도구 키트 설치]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="6460d-196">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="6460d-197">[Eclipse용 Azure 도구 키트에 대한 로그인 지침]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="6460d-197">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="6460d-198">[IntelliJ용 Azure 도구 키트에 대한 로그인 지침]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="6460d-198">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="6460d-199">[Eclipse용 Azure 도구 키트의 새로운 기능]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="6460d-199">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="6460d-200">[IntelliJ용 Azure 도구 키트의 새로운 기능]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="6460d-200">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="6460d-201">[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="6460d-201">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="6460d-202">[Visual Studio Team Services용 Java 도구]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="6460d-202">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="6460d-203">[Azure에서 Windows 가상 컴퓨터에 대한 크기]: /azure/virtual-machines/virtual-machines-windows-sizes</span><span class="sxs-lookup"><span data-stu-id="6460d-203">[Sizes for Windows virtual machines in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span></span>
<span data-ttu-id="6460d-204">[Azure에서 Linux 가상 컴퓨터에 대한 크기]: /azure/virtual-machines/virtual-machines-linux-sizes</span><span class="sxs-lookup"><span data-stu-id="6460d-204">[Sizes for Linux virtual machines in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span></span>
<span data-ttu-id="6460d-205">[Windows 가상 컴퓨터 가격 책정]: /pricing/details/virtual-machines/windows/</span><span class="sxs-lookup"><span data-stu-id="6460d-205">[Windows virtual-machine pricing]: /pricing/details/virtual-machines/windows/</span></span>
<span data-ttu-id="6460d-206">[Linux 가상 컴퓨터 가격 책정]: /pricing/details/virtual-machines/linux/</span><span class="sxs-lookup"><span data-stu-id="6460d-206">[Linux virtual-machine pricing]: /pricing/details/virtual-machines/linux/</span></span>


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
