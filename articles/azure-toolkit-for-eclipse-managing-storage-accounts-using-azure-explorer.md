---
title: "Eclipse용 Azure Explorer를 사용하여 저장소 계정 관리 | Microsoft Docs"
description: "Eclipse용 Azure 탐색기를 사용하여 Azure Storage 계정을 관리하는 방법을 알아봅니다."
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
ms.openlocfilehash: 5b3014b5aca368be8ea46863c83665abde10fed5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-storage-accounts-by-using-the-azure-explorer-for-eclipse"></a><span data-ttu-id="383bf-103">Eclipse용 Azure Explorer를 사용하여 저장소 계정 관리</span><span class="sxs-lookup"><span data-stu-id="383bf-103">Manage storage accounts by using the Azure Explorer for Eclipse</span></span>

<span data-ttu-id="383bf-104">Eclipse용 Azure 도구 키트의 일부인 Azure Explorer는 Eclipse IDE(통합 개발 환경) 내에서 Azure 계정의 저장소 계정을 관리하기 위한 사용하기 쉬운 솔루션을 Java 개발자에게 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="383bf-104">The Azure Explorer, which is part of the Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside the Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-eclipse"></a><span data-ttu-id="383bf-105">Eclipse에서 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="383bf-105">Create a storage account in Eclipse</span></span>

<span data-ttu-id="383bf-106">Azure Explorer를 사용하여 저장소 계정을 만들려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="383bf-106">To create a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="383bf-107">[Eclipse용 Azure 도구 키트에 대한 로그인 지침]을 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="383bf-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for Eclipse].</span></span>

2. <span data-ttu-id="383bf-108">**Azure Explorer** 보기에서 **Azure** 노드를 확장하고 **저장소 계정**을 마우스 오른쪽 단추로 클릭한 후 **저장소 계정 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="383bf-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![저장소 계정 만들기 명령][CS01]

3. <span data-ttu-id="383bf-110">**저장소 계정 만들기** 대화 상자에서 다음 옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="383bf-110">In the **Create Storage Account** dialog box, specify the following options:</span></span>

   ![새 저장소 계정 만들기 대화 상자][CS02]

   * <span data-ttu-id="383bf-112">**이름**: 새 저장소 계정의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="383bf-112">**Name**: Specifies the name for the new storage account.</span></span>

   * <span data-ttu-id="383bf-113">**구독**: 새 저장소 계정에 사용할 Azure 구독을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="383bf-113">**Subscription**: Specifies the Azure subscription that you want to use for the new storage account.</span></span>

   * <span data-ttu-id="383bf-114">**리소스 그룹**: 가상 컴퓨터에 사용할 리소스 그룹을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="383bf-114">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="383bf-115">다음 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="383bf-115">Select one of the following options:</span></span>
      * <span data-ttu-id="383bf-116">**새로 만들기**: 새 리소스 그룹을 만들도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="383bf-116">**Create New**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="383bf-117">**기존 그룹 사용**: Azure 계정에 연결된 리소스 그룹 목록에서 선택하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="383bf-117">**Use Existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

   * <span data-ttu-id="383bf-118">**지역**: 저장소 계정을 만들 위치(예: “미국 서부”)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="383bf-118">**Region**: Specifies the location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="383bf-119">**계정 종류**: 만들려는 저장소 계정의 형식을 지정합니다(예: “Blob Storage”).</span><span class="sxs-lookup"><span data-stu-id="383bf-119">**Account kind**: Specifies the type of storage account to create (for example, "Blob storage").</span></span> <span data-ttu-id="383bf-120">자세한 내용은 [Azure 저장소 계정 정보]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="383bf-120">For more information, see [About Azure storage accounts].</span></span>

   * <span data-ttu-id="383bf-121">**성능**: 선택한 게시자에서 사용할 저장소 계정 제품을 지정합니다(예: “프리미엄”).</span><span class="sxs-lookup"><span data-stu-id="383bf-121">**Performance**: Specifies which storage account offering to use from the selected publisher (for example, "Premium").</span></span> <span data-ttu-id="383bf-122">자세한 내용은 [Azure Storage 확장성 및 성능 목표]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="383bf-122">For more information, see [Azure storage scalability and performance targets].</span></span>

   * <span data-ttu-id="383bf-123">**복제**: 저장소 계정에 대한 복제를 지정합니다(예: “영역 중복”).</span><span class="sxs-lookup"><span data-stu-id="383bf-123">**Replication**: Specifies the replication for the storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="383bf-124">자세한 내용은 [Azure Storage 복제]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="383bf-124">For more information, see [Azure storage replication].</span></span>

4. <span data-ttu-id="383bf-125">위의 옵션을 모두 지정했으면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="383bf-125">When you have specified all of the preceding options, click **Create**.</span></span>

## <a name="create-a-storage-container-in-eclipse"></a><span data-ttu-id="383bf-126">Eclipse에서 저장소 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="383bf-126">Create a storage container in Eclipse</span></span>

<span data-ttu-id="383bf-127">Azure Explorer를 사용하여 저장소 컨테이너를 만들려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="383bf-127">To create a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="383bf-128">**Azure Explorer** 보기에서 컨테이너를 만들 저장소 계정을 마우스 오른쪽 단추로 클릭하고 **Blob 컨테이너 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="383bf-128">In the **Azure Explorer** view, right-click the storage account where you want to create a container, and then click **Create blob container**.</span></span>

   ![Blob 컨테이너 만들기 명령][CC01]

2. <span data-ttu-id="383bf-130">**Blob 컨테이너 만들기** 대화 상자에서 컨테이너의 이름을 지정하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="383bf-130">In the **Create blob container** dialog box, specify the name for your container, and then click **OK**.</span></span> <span data-ttu-id="383bf-131">저장소 컨테이너 이름 지정에 대한 자세한 내용은 [컨테이너, BLOB 및 메타데이터 이름 지정 및 참조]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="383bf-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![Blob 컨테이너 만들기 대화 상자][CC02]

## <a name="delete-a-storage-container-in-eclipse"></a><span data-ttu-id="383bf-133">Eclipse에서 저장소 컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="383bf-133">Delete a storage container in Eclipse</span></span>

<span data-ttu-id="383bf-134">Azure Explorer를 사용하여 저장소 컨테이너를 삭제하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="383bf-134">To delete a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="383bf-135">**Azure Explorer** 보기에서 저장소 컨테이너를 마우스 오른쪽 단추로 클릭하고 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="383bf-135">In the **Azure Explorer** view, right-click the storage container, and then click **Delete**.</span></span>

   ![저장소 컨테이너 삭제 명령][DC01]

2. <span data-ttu-id="383bf-137">확인 창에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="383bf-137">In the confirmation window, click **OK**.</span></span>

   ![저장소 컨테이너 삭제 확인 창][DC02]

## <a name="delete-a-storage-account-in-eclipse"></a><span data-ttu-id="383bf-139">Eclipse에서 저장소 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="383bf-139">Delete a storage account in Eclipse</span></span>

<span data-ttu-id="383bf-140">Azure Explorer를 사용하여 저장소 계정을 삭제하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="383bf-140">To delete a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="383bf-141">**Azure Explorer** 보기에서 저장소 계정을 마우스 오른쪽 단추로 클릭하고 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="383bf-141">In the **Azure Explorer** view, right-click the storage account, and then click **Delete**.</span></span>

   ![저장소 계정 삭제 명령][DS01]

2. <span data-ttu-id="383bf-143">확인 창에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="383bf-143">In the confirmation window, click **OK**.</span></span>

   ![저장소 계정 삭제 확인 창][DS02]

## <a name="next-steps"></a><span data-ttu-id="383bf-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="383bf-145">Next steps</span></span>
<span data-ttu-id="383bf-146">Azure Storage 계정, 크기 및 가격 책정에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="383bf-146">For more information about Azure storage accounts, sizes, and pricing, see the following resources:</span></span>

* <span data-ttu-id="383bf-147">[Microsoft Azure 저장소 소개]</span><span class="sxs-lookup"><span data-stu-id="383bf-147">[Introduction to Microsoft Azure Storage]</span></span>
* <span data-ttu-id="383bf-148">[Azure 저장소 계정 정보]</span><span class="sxs-lookup"><span data-stu-id="383bf-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="383bf-149">Azure Storage 계정 크기</span><span class="sxs-lookup"><span data-stu-id="383bf-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="383bf-150">[Azure의 Windows 저장소 계정 크기]</span><span class="sxs-lookup"><span data-stu-id="383bf-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="383bf-151">[Azure의 Linux 저장소 계정 크기]</span><span class="sxs-lookup"><span data-stu-id="383bf-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="383bf-152">Azure Storage 계정 가격 책정</span><span class="sxs-lookup"><span data-stu-id="383bf-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="383bf-153">[Windows 저장소 계정 가격 책정]</span><span class="sxs-lookup"><span data-stu-id="383bf-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="383bf-154">[Linux 저장소 계정 가격 책정]</span><span class="sxs-lookup"><span data-stu-id="383bf-154">[Linux storage-account pricing]</span></span>

<span data-ttu-id="383bf-155">Java IDE용 Azure 도구 키트에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="383bf-155">For more information about Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="383bf-156">[Eclipse용 Azure 도구 키트]</span><span class="sxs-lookup"><span data-stu-id="383bf-156">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="383bf-157">[Eclipse용 Azure 도구 키트의 새로운 기능]</span><span class="sxs-lookup"><span data-stu-id="383bf-157">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="383bf-158">[Eclipse용 Azure 도구 키트 설치]</span><span class="sxs-lookup"><span data-stu-id="383bf-158">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="383bf-159">[Eclipse용 Azure 도구 키트에 대한 로그인 지침]</span><span class="sxs-lookup"><span data-stu-id="383bf-159">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="383bf-160">[Eclipse에서 Azure용 Hello World 웹앱 만들기]</span><span class="sxs-lookup"><span data-stu-id="383bf-160">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="383bf-161">[IntelliJ용 Azure 도구 키트]</span><span class="sxs-lookup"><span data-stu-id="383bf-161">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="383bf-162">[IntelliJ용 Azure 도구 키트의 새로운 기능]</span><span class="sxs-lookup"><span data-stu-id="383bf-162">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="383bf-163">[IntelliJ용 Azure 도구 키트 설치]</span><span class="sxs-lookup"><span data-stu-id="383bf-163">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="383bf-164">[IntelliJ용 Azure 도구 키트에 대한 로그인 지침]</span><span class="sxs-lookup"><span data-stu-id="383bf-164">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="383bf-165">[IntelliJ에서 Azure용 Hello World 웹앱 만들기]</span><span class="sxs-lookup"><span data-stu-id="383bf-165">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="383bf-166">Java와 함께 Azure를 사용하는 것에 대한 자세한 내용은 [Azure Java 개발자 센터] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="383bf-166">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="383bf-167">[Eclipse용 Azure 도구 키트]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="383bf-167">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="383bf-168">[IntelliJ용 Azure 도구 키트]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="383bf-168">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="383bf-169">[Eclipse에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="383bf-169">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="383bf-170">[IntelliJ에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="383bf-170">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="383bf-171">[Eclipse용 Azure 도구 키트 설치]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="383bf-171">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="383bf-172">[IntelliJ용 Azure 도구 키트 설치]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="383bf-172">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="383bf-173">[Eclipse용 Azure 도구 키트에 대한 로그인 지침]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="383bf-173">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="383bf-174">[IntelliJ용 Azure 도구 키트에 대한 로그인 지침]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="383bf-174">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="383bf-175">[Eclipse용 Azure 도구 키트의 새로운 기능]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="383bf-175">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="383bf-176">[IntelliJ용 Azure 도구 키트의 새로운 기능]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="383bf-176">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="383bf-177">[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="383bf-177">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="383bf-178">[Visual Studio Team Services용 Java 도구]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="383bf-178">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="383bf-179">[Microsoft Azure 저장소 소개]: /azure/storage/storage-introduction</span><span class="sxs-lookup"><span data-stu-id="383bf-179">[Introduction to Microsoft Azure Storage]: /azure/storage/storage-introduction</span></span>
<span data-ttu-id="383bf-180">[Azure 저장소 계정 정보]: /azure/storage/storage-create-storage-account</span><span class="sxs-lookup"><span data-stu-id="383bf-180">[About Azure storage accounts]: /azure/storage/storage-create-storage-account</span></span>
<span data-ttu-id="383bf-181">[Azure Storage 복제]: /azure/storage/storage-redundancy</span><span class="sxs-lookup"><span data-stu-id="383bf-181">[Azure storage replication]: /azure/storage/storage-redundancy</span></span>
<span data-ttu-id="383bf-182">[Azure Storage 확장성 및 성능 목표]: /azure/storage/storage-scalability-targets</span><span class="sxs-lookup"><span data-stu-id="383bf-182">[Azure storage scalability and Performance Targets]: /azure/storage/storage-scalability-targets</span></span>
<span data-ttu-id="383bf-183">[컨테이너, BLOB 및 메타데이터 이름 지정 및 참조]: http://go.microsoft.com/fwlink/?LinkId=255555</span><span class="sxs-lookup"><span data-stu-id="383bf-183">[Naming and referencing containers, blobs, and metadata]: http://go.microsoft.com/fwlink/?LinkId=255555</span></span>

<span data-ttu-id="383bf-184">[Azure의 Windows 저장소 계정 크기]: /azure/virtual-machines/virtual-machines-windows-sizes</span><span class="sxs-lookup"><span data-stu-id="383bf-184">[Sizes for Windows storage accounts in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span></span>
<span data-ttu-id="383bf-185">[Azure의 Linux 저장소 계정 크기]: /azure/virtual-machines/virtual-machines-linux-sizes</span><span class="sxs-lookup"><span data-stu-id="383bf-185">[Sizes for Linux storage accounts in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span></span>
<span data-ttu-id="383bf-186">[Windows 저장소 계정 가격 책정]: /pricing/details/virtual-machines/windows/</span><span class="sxs-lookup"><span data-stu-id="383bf-186">[Windows storage-account pricing]: /pricing/details/virtual-machines/windows/</span></span>
<span data-ttu-id="383bf-187">[Linux 저장소 계정 가격 책정]: /pricing/details/virtual-machines/linux/</span><span class="sxs-lookup"><span data-stu-id="383bf-187">[Linux storage-account pricing]: /pricing/details/virtual-machines/linux/</span></span>

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC02.png
