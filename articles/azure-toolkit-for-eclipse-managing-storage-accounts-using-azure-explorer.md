---
title: "사용 하 여 aaaManage 저장소 계정을 Eclipse 용 Azure 탐색기 hello | Microsoft Docs"
description: "어떻게 toomanage Azure 저장소는 Eclipse 용 Azure 탐색기 hello를 사용 하 여을 계정에 대해 알아봅니다."
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
ms.openlocfilehash: b7ec53e77e3c96d87754b9a658d31e6182121b22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-storage-accounts-by-using-hello-azure-explorer-for-eclipse"></a><span data-ttu-id="af2d9-103">Eclipse 용 Azure 탐색기 hello를 사용 하 여 저장소 계정 관리</span><span class="sxs-lookup"><span data-stu-id="af2d9-103">Manage storage accounts by using hello Azure Explorer for Eclipse</span></span>

<span data-ttu-id="af2d9-104">hello hello Eclipse 용 Azure 도구 키트의 일부인 Azure 탐색기에서 자신의 Azure 계정에 저장소 계정을 관리 하기 위한 사용 하기 쉬운 솔루션과 Java 개발자가 제공 hello Eclipse 통합된 개발 환경 (IDE) 안에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af2d9-104">hello Azure Explorer, which is part of hello Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside hello Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-eclipse"></a><span data-ttu-id="af2d9-105">Eclipse에서 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="af2d9-105">Create a storage account in Eclipse</span></span>

<span data-ttu-id="af2d9-106">toocreate hello Azure 탐색기를 사용 하 여 저장소 계정을 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="af2d9-106">toocreate a storage account by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="af2d9-107">Hello를 사용 하 여 Azure 계정 tooyour 로그인 [hello Eclipse 용 Azure 도구 키트에 대 한 로그인 지침]합니다.</span><span class="sxs-lookup"><span data-stu-id="af2d9-107">Sign in tooyour Azure account by using hello [Sign-in instructions for hello Azure Toolkit for Eclipse].</span></span>

2. <span data-ttu-id="af2d9-108">Hello에 **Azure 탐색기** 보기, hello 확장 **Azure** 노드를 마우스 오른쪽 단추로 클릭 **저장소 계정은**, 클릭 하 고 **저장소 계정 만들기**.</span><span class="sxs-lookup"><span data-stu-id="af2d9-108">In hello **Azure Explorer** view, expand hello **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![저장소 계정 만들기 명령][CS01]

3. <span data-ttu-id="af2d9-110">Hello에 **저장소 계정 만들기** 대화 상자를 hello 다음 옵션을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="af2d9-110">In hello **Create Storage Account** dialog box, specify hello following options:</span></span>

   ![새 저장소 계정 만들기 대화 상자][CS02]

   * <span data-ttu-id="af2d9-112">**이름**: hello 새 저장소 계정에 대 한 hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="af2d9-112">**Name**: Specifies hello name for hello new storage account.</span></span>

   * <span data-ttu-id="af2d9-113">**구독**: hello hello 새 저장소 계정에 대 한 toouse 되도록 Azure 구독을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="af2d9-113">**Subscription**: Specifies hello Azure subscription that you want toouse for hello new storage account.</span></span>

   * <span data-ttu-id="af2d9-114">**리소스 그룹**: 가상 컴퓨터에 대 한 hello 리소스 그룹을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="af2d9-114">**Resource Group**: Specifies hello resource group for your virtual machine.</span></span> <span data-ttu-id="af2d9-115">Hello 다음 옵션 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="af2d9-115">Select one of hello following options:</span></span>
      * <span data-ttu-id="af2d9-116">**새로 만들기**: toocreate 새 리소스 그룹 한다고 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="af2d9-116">**Create New**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="af2d9-117">**기존 그룹 사용**: Azure 계정에 연결된 리소스 그룹 목록에서 선택하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="af2d9-117">**Use Existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

   * <span data-ttu-id="af2d9-118">**지역**: hello 위치 (예: "West US") 저장소 계정을 만들 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="af2d9-118">**Region**: Specifies hello location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="af2d9-119">**Kind 계정**: 저장소 계정 toocreate (예: "Blob storage")의 hello 유형을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="af2d9-119">**Account kind**: Specifies hello type of storage account toocreate (for example, "Blob storage").</span></span> <span data-ttu-id="af2d9-120">자세한 내용은 [Azure 저장소 계정 정보]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af2d9-120">For more information, see [About Azure storage accounts].</span></span>

   * <span data-ttu-id="af2d9-121">**성능**: toouse (예: "프리미엄") hello 선택한 게시자에서 제공 하는 저장소 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="af2d9-121">**Performance**: Specifies which storage account offering toouse from hello selected publisher (for example, "Premium").</span></span> <span data-ttu-id="af2d9-122">자세한 내용은 [Azure Storage 확장성 및 성능 목표]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af2d9-122">For more information, see [Azure storage scalability and performance targets].</span></span>

   * <span data-ttu-id="af2d9-123">**복제**: hello 저장소 계정 (예를 들어 "영역 중복")에 대 한 hello 복제를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="af2d9-123">**Replication**: Specifies hello replication for hello storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="af2d9-124">자세한 내용은 [Azure Storage 복제]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af2d9-124">For more information, see [Azure storage replication].</span></span>

4. <span data-ttu-id="af2d9-125">Hello 앞에 옵션을 모두 지정한 경우 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="af2d9-125">When you have specified all of hello preceding options, click **Create**.</span></span>

## <a name="create-a-storage-container-in-eclipse"></a><span data-ttu-id="af2d9-126">Eclipse에서 저장소 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="af2d9-126">Create a storage container in Eclipse</span></span>

<span data-ttu-id="af2d9-127">hello Azure 탐색기를 사용 하 여 저장소 컨테이너 toocreate 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="af2d9-127">toocreate a storage container by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="af2d9-128">Hello에 **Azure 탐색기** 보기, toocreate 컨테이너를 선택 하 고 클릭 hello 저장소 계정을 마우스 오른쪽 단추로 **blob 컨테이너 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="af2d9-128">In hello **Azure Explorer** view, right-click hello storage account where you want toocreate a container, and then click **Create blob container**.</span></span>

   ![Blob 컨테이너 만들기 명령][CC01]

2. <span data-ttu-id="af2d9-130">Hello에 **blob 컨테이너 만들기** 대화 상자에서 사용자 컨테이너에 대 한 hello 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="af2d9-130">In hello **Create blob container** dialog box, specify hello name for your container, and then click **OK**.</span></span> <span data-ttu-id="af2d9-131">저장소 컨테이너 이름 지정에 대한 자세한 내용은 [컨테이너, BLOB, 메타데이터 이름 지정 및 참조]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af2d9-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![Blob 컨테이너 만들기 대화 상자][CC02]

## <a name="delete-a-storage-container-in-eclipse"></a><span data-ttu-id="af2d9-133">Eclipse에서 저장소 컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="af2d9-133">Delete a storage container in Eclipse</span></span>

<span data-ttu-id="af2d9-134">hello Azure 탐색기를 사용 하 여 저장소 컨테이너 toodelete 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="af2d9-134">toodelete a storage container by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="af2d9-135">Hello에 **Azure 탐색기** 볼 hello 저장소 컨테이너를 마우스 오른쪽 단추로 클릭 하 고 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="af2d9-135">In hello **Azure Explorer** view, right-click hello storage container, and then click **Delete**.</span></span>

   ![저장소 컨테이너 삭제 명령][DC01]

2. <span data-ttu-id="af2d9-137">Hello 확인 창에서 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="af2d9-137">In hello confirmation window, click **OK**.</span></span>

   ![저장소 컨테이너 삭제 확인 창][DC02]

## <a name="delete-a-storage-account-in-eclipse"></a><span data-ttu-id="af2d9-139">Eclipse에서 저장소 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="af2d9-139">Delete a storage account in Eclipse</span></span>

<span data-ttu-id="af2d9-140">toodelete hello Azure 탐색기를 사용 하 여 저장소 계정을 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="af2d9-140">toodelete a storage account by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="af2d9-141">Hello에 **Azure 탐색기** 볼 hello 저장소 계정을 마우스 오른쪽 단추로 클릭 하 고 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="af2d9-141">In hello **Azure Explorer** view, right-click hello storage account, and then click **Delete**.</span></span>

   ![저장소 계정 삭제 명령][DS01]

2. <span data-ttu-id="af2d9-143">Hello 확인 창에서 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="af2d9-143">In hello confirmation window, click **OK**.</span></span>

   ![저장소 계정 삭제 확인 창][DS02]

## <a name="next-steps"></a><span data-ttu-id="af2d9-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="af2d9-145">Next steps</span></span>
<span data-ttu-id="af2d9-146">Azure 저장소 계정, 크기 및 가격에 대 한 자세한 내용은 다음 리소스는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="af2d9-146">For more information about Azure storage accounts, sizes, and pricing, see hello following resources:</span></span>

* <span data-ttu-id="af2d9-147">[Azure 저장소 소개 tooMicrosoft]</span><span class="sxs-lookup"><span data-stu-id="af2d9-147">[Introduction tooMicrosoft Azure Storage]</span></span>
* <span data-ttu-id="af2d9-148">[Azure 저장소 계정 정보]</span><span class="sxs-lookup"><span data-stu-id="af2d9-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="af2d9-149">Azure Storage 계정 크기</span><span class="sxs-lookup"><span data-stu-id="af2d9-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="af2d9-150">[Azure의 Windows 저장소 계정 크기]</span><span class="sxs-lookup"><span data-stu-id="af2d9-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="af2d9-151">[Azure의 Linux 저장소 계정 크기]</span><span class="sxs-lookup"><span data-stu-id="af2d9-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="af2d9-152">Azure Storage 계정 가격 책정</span><span class="sxs-lookup"><span data-stu-id="af2d9-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="af2d9-153">[Windows 저장소 계정 가격 책정]</span><span class="sxs-lookup"><span data-stu-id="af2d9-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="af2d9-154">[Linux 저장소 계정 가격 책정]</span><span class="sxs-lookup"><span data-stu-id="af2d9-154">[Linux storage-account pricing]</span></span>

<span data-ttu-id="af2d9-155">Java Ide에 대 한 Azure 도구 키트에 대 한 자세한 내용은 hello 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="af2d9-155">For more information about Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="af2d9-156">[Eclipse용 Azure 도구 키트]</span><span class="sxs-lookup"><span data-stu-id="af2d9-156">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="af2d9-157">[Hello Eclipse 용 Azure 도구 키트의에서 새로운 기능]</span><span class="sxs-lookup"><span data-stu-id="af2d9-157">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="af2d9-158">[Hello Eclipse 용 Azure 도구 키트 설치]</span><span class="sxs-lookup"><span data-stu-id="af2d9-158">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="af2d9-159">[hello Eclipse 용 Azure 도구 키트에 대 한 로그인 지침]</span><span class="sxs-lookup"><span data-stu-id="af2d9-159">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="af2d9-160">[Eclipse에서 Azure용 Hello World 웹앱 만들기]</span><span class="sxs-lookup"><span data-stu-id="af2d9-160">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="af2d9-161">[IntelliJ용 Azure 도구 키트]</span><span class="sxs-lookup"><span data-stu-id="af2d9-161">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="af2d9-162">[Hello IntelliJ 용 Azure 도구 키트의에서 새로운 기능]</span><span class="sxs-lookup"><span data-stu-id="af2d9-162">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="af2d9-163">[IntelliJ 용 hello Azure 도구 키트 설치]</span><span class="sxs-lookup"><span data-stu-id="af2d9-163">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="af2d9-164">[로그인에 대 한 지침 Azure 도구 키트 hello IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="af2d9-164">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="af2d9-165">[IntelliJ에서 Azure용 Hello World 웹앱 만들기]</span><span class="sxs-lookup"><span data-stu-id="af2d9-165">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="af2d9-166">Java와 함께 Azure를 사용하는 것에 대한 자세한 내용은 [Azure Java 개발자 센터] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af2d9-166">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Eclipse용 Azure 도구 키트]: ./azure-toolkit-for-eclipse.md
[IntelliJ용 Azure 도구 키트]: ./azure-toolkit-for-intellij.md
[Eclipse에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[IntelliJ에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Hello Eclipse 용 Azure 도구 키트 설치]: ./azure-toolkit-for-eclipse-installation.md
[IntelliJ 용 hello Azure 도구 키트 설치]: ./azure-toolkit-for-intellij-installation.md
[hello Eclipse 용 Azure 도구 키트에 대 한 로그인 지침]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[로그인에 대 한 지침 Azure 도구 키트 hello IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Hello Eclipse 용 Azure 도구 키트의에서 새로운 기능]: ./azure-toolkit-for-eclipse-whats-new.md
[Hello IntelliJ 용 Azure 도구 키트의에서 새로운 기능]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/
[Visual Studio Team Services용 Java 도구]: https://java.visualstudio.com/

[Azure 저장소 소개 tooMicrosoft]: /azure/storage/storage-introduction
[Azure 저장소 계정 정보]: /azure/storage/storage-create-storage-account
[Azure Storage 복제]: /azure/storage/storage-redundancy
[Azure Storage 확장성 및 성능 목표]: /azure/storage/storage-scalability-targets
[컨테이너, BLOB, 메타데이터 이름 지정 및 참조]: http://go.microsoft.com/fwlink/?LinkId=255555

[Azure의 Windows 저장소 계정 크기]: /azure/virtual-machines/virtual-machines-windows-sizes
[Azure의 Linux 저장소 계정 크기]: /azure/virtual-machines/virtual-machines-linux-sizes
[Windows 저장소 계정 가격 책정]: /pricing/details/virtual-machines/windows/
[Linux 저장소 계정 가격 책정]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC02.png
