---
title: "Azure에 대 한 aaaConfigure hello 역할 클라우드 Visual Studio와 함께 서비스 | Microsoft Docs"
description: "자세한 내용은 방법 tooset 및 Visual Studio를 사용 하 여 Azure 클라우드 서비스에 대 한 역할을 구성 합니다."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: d397ef87-64e5-401a-aad5-7f83f1022e16
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: d3c62eb57040ebe987787e73b17b468bb82122bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-cloud-service-roles-with-visual-studio"></a><span data-ttu-id="6dc02-103">Visual Studio를 사용하여 Azure 클라우드 서비스 역할 구성</span><span class="sxs-lookup"><span data-stu-id="6dc02-103">Configure Azure cloud service roles with Visual Studio</span></span>
<span data-ttu-id="6dc02-104">Azure 클라우드 서비스에는 하나 이상의 작업자 또는 웹 역할이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-104">An Azure cloud service can have one or more worker or web roles.</span></span> <span data-ttu-id="6dc02-105">각 역할에 대해 해당 역할 설정 방법 toodefine 필요한 고도 실행 방식을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-105">For each role, you need toodefine how that role is set up and also configure how that role runs.</span></span> <span data-ttu-id="6dc02-106">클라우드 서비스의 역할에 대해 자세히 toolearn hello 비디오를 참조 하세요. [소개 tooAzure 클라우드 서비스](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services)합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-106">toolearn more about roles in cloud services, see hello video [Introduction tooAzure Cloud Services](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services).</span></span> 

<span data-ttu-id="6dc02-107">클라우드 서비스에 대 한 hello 정보는 다음 파일이 hello에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-107">hello information for your cloud service is stored in hello following files:</span></span>

- <span data-ttu-id="6dc02-108">**ServiceDefinition.csdef** -hello 서비스 정의 파일은 필요한 역할을 포함 하 여 클라우드 서비스, 끝점 및 가상 컴퓨터 크기에 대 한 hello 런타임 설정을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-108">**ServiceDefinition.csdef** - hello service definition file defines hello runtime settings for your cloud service including what roles are required, endpoints, and virtual machine size.</span></span> <span data-ttu-id="6dc02-109">에 저장 된 hello 데이터 없음 `ServiceDefinition.csdef` 역할이 실행 되는 경우에 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-109">None of hello data stored in `ServiceDefinition.csdef` can be changed when your role is running.</span></span>
- <span data-ttu-id="6dc02-110">**ServiceConfiguration.cscfg** -hello 서비스 구성 파일 실행 되는 역할의 인스턴스 수를 구성 하 고 역할에 대해 정의 된 hello 설정의 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-110">**ServiceConfiguration.cscfg** - hello service configuration file configures how many instances of a role are run and hello values of hello settings defined for a role.</span></span> <span data-ttu-id="6dc02-111">에 저장 된 데이터를 hello `ServiceConfiguration.cscfg` 역할이 실행 되는 동안에 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-111">hello data stored in `ServiceConfiguration.cscfg` can be changed while your role is running.</span></span>

<span data-ttu-id="6dc02-112">역할 실행 되는 방식을 제어 하는 hello 설정에 대 한 다른 toostore 값, 여러 서비스 구성을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-112">toostore different values for hello settings that control how a role runs, you can define multiple service configurations.</span></span> <span data-ttu-id="6dc02-113">각 배포 환경에 대해 서로 다른 서비스 구성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-113">You can use a different service configuration for each deployment environment.</span></span> <span data-ttu-id="6dc02-114">예를 들어, 로컬 서비스 구성에서 저장소 계정 연결 문자열 toouse hello 로컬 Azure 저장소 에뮬레이터를 설정할 수 있으며 hello 클라우드에서 다른 서비스 구성 toouse Azure 저장소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-114">For example, you can set your storage account connection string toouse hello local Azure storage emulator in a local service configuration and create another service configuration toouse Azure storage in hello cloud.</span></span>

<span data-ttu-id="6dc02-115">Visual Studio에서 Azure 클라우드 서비스를 만들 때 두 개의 서비스 구성이 자동으로 만들어집니다 및 tooyour Azure 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-115">When you create an Azure cloud service in Visual Studio, two service configurations are automatically created and added tooyour Azure project:</span></span>

- `ServiceConfiguration.Cloud.cscfg`
- `ServiceConfiguration.Local.cscfg`

## <a name="configure-an-azure-cloud-service"></a><span data-ttu-id="6dc02-116">Azure 클라우드 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="6dc02-116">Configure an Azure cloud service</span></span>
<span data-ttu-id="6dc02-117">단계를 수행 하는 hello와 같이 Visual Studio에서 솔루션 탐색기에서 Azure 클라우드 서비스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-117">You can configure an Azure cloud service from Solution Explorer in Visual Studio, as shown in hello following steps:</span></span>

1. <span data-ttu-id="6dc02-118">Visual Studio에서 Azure 클라우드 서비스 프로젝트를 만들거나 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-118">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="6dc02-119">**솔루션 탐색기**, hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고, hello 상황에 맞는 메뉴에서 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-119">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>
   
    ![솔루션 탐색기 프로젝트 - 상황에 맞는 메뉴](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-project-context-menu.png)

1. <span data-ttu-id="6dc02-121">Hello 프로젝트의 속성 페이지에서 선택 hello **개발** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-121">In hello project's properties page, select hello **Development** tab.</span></span> 

    ![프로젝트 속성 페이지 - 개발 탭](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-development-tab.png)

1. <span data-ttu-id="6dc02-123">Hello에 **서비스 구성** 목록, 선택 hello tooedit 원하는 hello 서비스 구성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-123">In hello **Service Configuration** list, select hello name of hello service configuration that you want tooedit.</span></span> <span data-ttu-id="6dc02-124">(선택 toomake이이 역할에 대 한 tooall hello 서비스 구성을 변경 하려면 **모든 구성**.)</span><span class="sxs-lookup"><span data-stu-id="6dc02-124">(If you want toomake changes tooall hello service configurations for this role, select **All Configurations**.)</span></span>
   
    > [!IMPORTANT]
    > <span data-ttu-id="6dc02-125">특정 서비스 구성을 선택하면 일부 속성은 모든 구성에 대해서만 설정 가능하므로 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-125">If you choose a specific service configuration, some properties are disabled because they can only be set for all configurations.</span></span> <span data-ttu-id="6dc02-126">tooedit 선택 해야 이러한 속성을 **모든 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-126">tooedit these properties, you must select **All Configurations**.</span></span>
    > 
    > 
   
    ![Azure 클라우드 서비스에 대한 서비스 구성 목록](./media/vs-azure-tools-configure-roles-for-cloud-service/cloud-service-service-configuration-property.png)

## <a name="change-hello-number-of-role-instances"></a><span data-ttu-id="6dc02-128">Hello 역할 인스턴스 수 변경</span><span class="sxs-lookup"><span data-stu-id="6dc02-128">Change hello number of role instances</span></span>
<span data-ttu-id="6dc02-129">클라우드 서비스의 tooimprove hello 성능을 hello, 사용자 또는 특정 역할에 대해 예상 되는 hello 로드 hello 수에 따라 실행 중인 역할의 인스턴스 수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-129">tooimprove hello performance of your cloud service, you can change hello number of instances of a role that are running, based on hello number of users or hello load expected for a particular role.</span></span> <span data-ttu-id="6dc02-130">Hello 클라우드 서비스가 Azure에서 실행 될 때 별도 가상 컴퓨터 역할의 각 인스턴스에 대해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-130">A separate virtual machine is created for each instance of a role when hello cloud service runs in Azure.</span></span> <span data-ttu-id="6dc02-131">이 클라우드 서비스의 hello 배포에 대 한 hello 청구가 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-131">This affects hello billing for hello deployment of this cloud service.</span></span> <span data-ttu-id="6dc02-132">대금 청구에 대한 자세한 내용은 [Microsoft Azure 청구서 이해](billing/billing-understand-your-bill.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6dc02-132">For more information about billing, see [Understand your bill for Microsoft Azure](billing/billing-understand-your-bill.md).</span></span>

1. <span data-ttu-id="6dc02-133">Visual Studio에서 Azure 클라우드 서비스 프로젝트를 만들거나 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-133">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="6dc02-134">**솔루션 탐색기**, hello 프로젝트 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-134">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="6dc02-135">Hello에서 **역할** 노드, 마우스 오른쪽 단추로 클릭 hello 역할 tooupdate, 한, hello 상황에 맞는 메뉴에서 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-135">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![솔루션 탐색기 - Azure 역할의 상황에 맞는 메뉴](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="6dc02-137">선택 hello **구성** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-137">Select hello **Configuration** tab.</span></span>

    ![구성 탭](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page.png)

1. <span data-ttu-id="6dc02-139">Hello에 **서비스 구성** 목록, tooupdate 않겠다고 선택 hello 서비스 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-139">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>
   
    ![서비스 구성 목록](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-select-configuration.png)

1. <span data-ttu-id="6dc02-141">Hello에 **인스턴스 수를** 텍스트 상자에이 역할에 대 한 toostart 되도록 인스턴스의 hello 수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-141">In hello **Instance count** text box, enter hello number of instances that you want toostart for this role.</span></span> <span data-ttu-id="6dc02-142">Hello 클라우드 서비스 tooAzure 게시할 때 각 인스턴스는 별도 가상 컴퓨터에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-142">Each instance runs on a separate virtual machine when you publish hello cloud service tooAzure.</span></span>

    ![Hello 인스턴스 수를 업데이트합니다.](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-instance-count.png)

1. <span data-ttu-id="6dc02-144">Hello Visual Studio에서에서 도구 모음 선택 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-144">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="manage-connection-strings-for-storage-accounts"></a><span data-ttu-id="6dc02-145">저장소 계정에 대한 연결 문자열 관리</span><span class="sxs-lookup"><span data-stu-id="6dc02-145">Manage connection strings for storage accounts</span></span>
<span data-ttu-id="6dc02-146">서비스 구성에 대한 연결 문자열을 추가, 제거 또는 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-146">You can add, remove, or modify connection strings for your service configurations.</span></span> <span data-ttu-id="6dc02-147">예를 들어, `UseDevelopmentStorage=true`값이 있는 로컬 서비스 구성에 대해 로컬 연결 문자열이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-147">For example, you might want a local connection string for a local service configuration that has a value of `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="6dc02-148">Azure에서 저장소 계정을 사용 하는 클라우드 서비스 구성을 tooconfigure를 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-148">You might also want tooconfigure a cloud service configuration that uses a storage account in Azure.</span></span>

> [!WARNING]
> <span data-ttu-id="6dc02-149">저장소 계정 연결 문자열에 대 한 hello Azure 저장소 계정 키 정보를 입력 하면이 정보는 hello 서비스 구성 파일에 로컬로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-149">When you enter hello Azure storage account key information for a storage account connection string, this information is stored locally in hello service configuration file.</span></span> <span data-ttu-id="6dc02-150">그러나 현재는 이 정보가 암호화된 텍스트로 저장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-150">However, this information is currently not stored as encrypted text.</span></span>
> 
> 

<span data-ttu-id="6dc02-151">각 서비스 구성에 대 한 다른 값을 사용 하 여 클라우드 서비스에서 다른 연결 문자열은 toouse 개일 하 또는 클라우드 서비스 tooAzure 게시할 때 코드를 수정 하지 않는 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-151">By using a different value for each service configuration, you do not have toouse different connection strings in your cloud service or modify your code when you publish your cloud service tooAzure.</span></span> <span data-ttu-id="6dc02-152">Hello 코드와 hello 값에 hello 연결 문자열에 같은 이름을 클라우드 서비스를 빌드 또는 게시할 때 선택 하는 hello 서비스 구성에 따라 다를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-152">You can use hello same name for hello connection string in your code and hello value is different, based on hello service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="6dc02-153">Visual Studio에서 Azure 클라우드 서비스 프로젝트를 만들거나 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-153">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="6dc02-154">**솔루션 탐색기**, hello 프로젝트 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-154">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="6dc02-155">Hello에서 **역할** 노드, 마우스 오른쪽 단추로 클릭 hello 역할 tooupdate, 한, hello 상황에 맞는 메뉴에서 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-155">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![솔루션 탐색기 - Azure 역할의 상황에 맞는 메뉴](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="6dc02-157">선택 hello **설정을** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-157">Select hello **Settings** tab.</span></span>

    ![설정 탭](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="6dc02-159">Hello에 **서비스 구성** 목록, tooupdate 않겠다고 선택 hello 서비스 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-159">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>

    ![서비스 구성](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="6dc02-161">연결 문자열 tooadd 선택 **설정 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-161">tooadd a connection string, select **Add Setting**.</span></span>

    ![연결 문자열 추가](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="6dc02-163">Hello 새 설정이 toohello 목록 추가, hello 목록의 hello 행 hello 필요한 정보로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-163">Once hello new setting has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![새 연결 문자열](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="6dc02-165">**이름** -hello 연결 문자열에 대 한 toouse 되도록 hello 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-165">**Name** - Enter hello name that you want toouse for hello connection string.</span></span>
    - <span data-ttu-id="6dc02-166">**형식** -선택 **연결 문자열** hello 드롭 다운 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-166">**Type** - Select **Connection String** from hello drop-down list.</span></span>
    - <span data-ttu-id="6dc02-167">**값** -hello에 직접 hello 연결 문자열을 입력 하거나 **값** 셀 또는 hello에 줄임표 (...) toowork 선택 hello **저장소 연결 문자열 만들기** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="6dc02-167">**Value** - You can either enter hello connection string directly into hello **Value** cell, or select hello ellipsis (...) toowork in hello **Create Storage Connection String** dialog.</span></span>  

1. <span data-ttu-id="6dc02-168">Hello에 **저장소 연결 문자열 만들기** 대화 상자에서 옵션에 대 한 **사용 하 여 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-168">In hello **Create Storage Connection String** dialog, select an option for **Connect using**.</span></span> <span data-ttu-id="6dc02-169">선택한 hello 옵션에 대 한 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-169">Then follow hello instructions for hello option you select:</span></span>

    - <span data-ttu-id="6dc02-170">**Microsoft Azure 저장소 에뮬레이터** -이 옵션을 선택 하면 tooAzure만 적용 되므로 hello hello 대화 상자에서 나머지 설정이 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-170">**Microsoft Azure storage emulator** - If you select this option, hello remaining settings on hello dialog are disabled as they apply only tooAzure.</span></span> <span data-ttu-id="6dc02-171">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-171">Select **OK**.</span></span>
    - <span data-ttu-id="6dc02-172">**구독** -Microsoft 계정으로이 옵션을 사용 하 여 hello 드롭다운 목록 tooeither select 및 기호를 선택 하거나 Microsoft 계정을 추가 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="6dc02-172">**Your subscription** - If you select this option, use hello dropdown list tooeither select and sign into a Microsoft account, or add a Microsoft account.</span></span> <span data-ttu-id="6dc02-173">Azure 구독 및 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-173">Select an Azure subscription and storage account.</span></span> <span data-ttu-id="6dc02-174">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-174">Select **OK**.</span></span>
    - <span data-ttu-id="6dc02-175">**수동으로 입력 한 자격 증명** -hello 저장소 계정 이름을 입력 하 고 기본 키 또는 두 번째 키 hello 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-175">**Manually entered credentials** - Enter hello storage account name, and either hello primary or second key.</span></span> <span data-ttu-id="6dc02-176">**연결** 옵션을 선택합니다(대부분의 시나리오에 대해 HTTPS 권장). **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-176">Select an option for **Connection** (HTTPS is recommended for most scenarios.) Select **OK**.</span></span>

1. <span data-ttu-id="6dc02-177">연결 문자열 toodelete hello 연결 문자열을 선택한 다음 선택 **설정 제거**합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-177">toodelete a connection string, select hello connection string, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="6dc02-178">Hello Visual Studio에서에서 도구 모음 선택 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-178">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-connection-string"></a><span data-ttu-id="6dc02-179">프로그래밍 방식으로 연결 문자열 액세스</span><span class="sxs-lookup"><span data-stu-id="6dc02-179">Programmatically access a connection string</span></span>

<span data-ttu-id="6dc02-180">hello 다음 단계에서는 tooprogrammatically C#을 사용 하 여 연결 문자열을 액세스 하는 방법을</span><span class="sxs-lookup"><span data-stu-id="6dc02-180">hello following steps show how tooprogrammatically access a connection string using C#.</span></span>

1. <span data-ttu-id="6dc02-181">Hello 다음 추가 toouse hello 설정을 어디로 지시문 tooa C# 파일을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="6dc02-181">Add hello following using directives tooa C# file where you are going toouse hello setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="6dc02-182">hello 다음 코드에서는 방법의 예로 tooaccess 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-182">hello following code illustrates an example of how tooaccess a connection string.</span></span> <span data-ttu-id="6dc02-183">Hello 대체 &lt;ConnectionStringName > 자리 표시자 hello 적절 한 값으로.</span><span class="sxs-lookup"><span data-stu-id="6dc02-183">Replace hello &lt;ConnectionStringName> placeholder with hello appropriate value.</span></span> 

    ```csharp
    // Setup hello connection tooAzure Storage
    var storageAccount = CloudStorageAccount.Parse(RoleEnvironment.GetConfigurationSettingValue("<ConnectionStringName>"));
    ```

## <a name="add-custom-settings-toouse-in-your-azure-cloud-service"></a><span data-ttu-id="6dc02-184">Azure 클라우드 서비스에서 사용자 지정 설정을 toouse 추가</span><span class="sxs-lookup"><span data-stu-id="6dc02-184">Add custom settings toouse in your Azure cloud service</span></span>
<span data-ttu-id="6dc02-185">Hello 서비스 구성 파일에서 사용자 지정 설정 이름 및 특정 서비스 구성에 대 한 문자열에 대 한 값을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-185">Custom settings in hello service configuration file let you add a name and value for a string for a specific service configuration.</span></span> <span data-ttu-id="6dc02-186">이 설정은 tooconfigure hello 값을 참조 하 여 클라우드 서비스의 기능을 설정 하 고 코드에서이 값 toocontrol hello 논리를 사용 하 여 hello toouse를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-186">You might choose toouse this setting tooconfigure a feature in your cloud service by reading hello value of hello setting and using this value toocontrol hello logic in your code.</span></span> <span data-ttu-id="6dc02-187">서비스 패키지 toorebuild 필요 없이 또는 클라우드 서비스가 실행 되 고 이러한 서비스 구성 값을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-187">You can change these service configuration values without having toorebuild your service package or when your cloud service is running.</span></span> <span data-ttu-id="6dc02-188">설정이 변경될 때 코드에서 알림을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-188">Your code can check for notifications of when a setting changes.</span></span> <span data-ttu-id="6dc02-189">[RoleEnvironment.Changing 이벤트](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6dc02-189">See [RoleEnvironment.Changing Event](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).</span></span>

<span data-ttu-id="6dc02-190">서비스 구성에 대한 사용자 지정 설정을 추가, 제거 또는 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-190">You can add, remove, or modify custom settings for your service configurations.</span></span> <span data-ttu-id="6dc02-191">다양한 서비스 구성에 대해 이러한 문자열에 서로 다른 값이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-191">You might want different values for these strings for different service configurations.</span></span>

<span data-ttu-id="6dc02-192">각 서비스 구성에 대 한 다른 값을 사용 하 여 클라우드 서비스에서 다른 문자열은 toouse 개일 하 또는 클라우드 서비스 tooAzure 게시할 때 코드를 수정 하지 않는 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-192">By using a different value for each service configuration, you do not have toouse different strings in your cloud service or modify your code when you publish your cloud service tooAzure.</span></span> <span data-ttu-id="6dc02-193">Hello 코드와 hello 값에 hello 문자열에 같은 이름을 클라우드 서비스를 빌드 또는 게시할 때 선택 하는 hello 서비스 구성에 따라 다를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-193">You can use hello same name for hello string in your code and hello value is different, based on hello service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="6dc02-194">Visual Studio에서 Azure 클라우드 서비스 프로젝트를 만들거나 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-194">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="6dc02-195">**솔루션 탐색기**, hello 프로젝트 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-195">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="6dc02-196">Hello에서 **역할** 노드, 마우스 오른쪽 단추로 클릭 hello 역할 tooupdate, 한, hello 상황에 맞는 메뉴에서 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-196">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![솔루션 탐색기 - Azure 역할의 상황에 맞는 메뉴](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="6dc02-198">선택 hello **설정을** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-198">Select hello **Settings** tab.</span></span>

    ![설정 탭](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="6dc02-200">Hello에 **서비스 구성** 목록, tooupdate 않겠다고 선택 hello 서비스 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-200">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>

    ![서비스 구성 목록](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="6dc02-202">사용자 지정 설정을 tooadd 선택 **설정 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-202">tooadd a custom setting, select **Add Setting**.</span></span>

    ![사용자 지정 설정 추가](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="6dc02-204">Hello 새 설정이 toohello 목록 추가, hello 목록의 hello 행 hello 필요한 정보로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-204">Once hello new setting has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![새 사용자 지정 설정](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="6dc02-206">**이름** -hello 설정의 hello 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-206">**Name** - Enter hello name of hello setting.</span></span>
    - <span data-ttu-id="6dc02-207">**형식** -선택 **문자열** hello 드롭 다운 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-207">**Type** - Select **String** from hello drop-down list.</span></span>
    - <span data-ttu-id="6dc02-208">**값** -hello hello 설정 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-208">**Value** - Enter hello value of hello setting.</span></span> <span data-ttu-id="6dc02-209">Hello에 직접 hello 값을 입력 하거나 **값** 셀 또는 hello에 줄임표 (...) tooenter hello 값 선택 hello **문자열 편집** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="6dc02-209">You can either enter hello value directly into hello **Value** cell, or select hello ellipsis (...) tooenter hello value in hello **Edit String** dialog.</span></span>  

1. <span data-ttu-id="6dc02-210">사용자 지정 설정 toodelete hello 설정을 선택한 다음 선택 **설정 제거**합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-210">toodelete a custom setting, select hello setting, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="6dc02-211">Hello Visual Studio에서에서 도구 모음 선택 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-211">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-custom-settings-value"></a><span data-ttu-id="6dc02-212">프로그래밍 방식으로 사용자 지정 설정 값 액세스</span><span class="sxs-lookup"><span data-stu-id="6dc02-212">Programmatically access a custom setting's value</span></span>
 
<span data-ttu-id="6dc02-213">hello 다음 단계에서는 tooprogrammatically C#을 사용 하 여 사용자 지정 설정을 액세스 하는 방법</span><span class="sxs-lookup"><span data-stu-id="6dc02-213">hello following steps show how tooprogrammatically access a custom setting using C#.</span></span>

1. <span data-ttu-id="6dc02-214">Hello 다음 추가 toouse hello 설정을 어디로 지시문 tooa C# 파일을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="6dc02-214">Add hello following using directives tooa C# file where you are going toouse hello setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="6dc02-215">hello 다음 코드에서는 방법의 예로 사용자 지정 설정 tooaccess 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-215">hello following code illustrates an example of how tooaccess a custom setting.</span></span> <span data-ttu-id="6dc02-216">Hello 대체 &lt;SettingName > 자리 표시자 hello 적절 한 값으로.</span><span class="sxs-lookup"><span data-stu-id="6dc02-216">Replace hello &lt;SettingName> placeholder with hello appropriate value.</span></span> 
    
    ```csharp
    var settingValue = RoleEnvironment.GetConfigurationSettingValue("<SettingName>");
    ```

## <a name="manage-local-storage-for-each-role-instance"></a><span data-ttu-id="6dc02-217">각 역할 인스턴스에 대한 로컬 저장소 관리</span><span class="sxs-lookup"><span data-stu-id="6dc02-217">Manage local storage for each role instance</span></span>
<span data-ttu-id="6dc02-218">각 역할 인스턴스에 대한 로컬 파일 시스템 저장소를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-218">You can add local file system storage for each instance of a role.</span></span> <span data-ttu-id="6dc02-219">hello 데이터 저장소는 액세스할 수 있다는 점에서 hello에 대 한 데이터가 저장 되는 hello 역할의 다른 인스턴스 또는 다른 역할을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-219">hello data stored in that storage is not accessible by other instances of hello role for which hello data is stored, or by other roles.</span></span>  

1. <span data-ttu-id="6dc02-220">Visual Studio에서 Azure 클라우드 서비스 프로젝트를 만들거나 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-220">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="6dc02-221">**솔루션 탐색기**, hello 프로젝트 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-221">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="6dc02-222">Hello에서 **역할** 노드, 마우스 오른쪽 단추로 클릭 hello 역할 tooupdate, 한, hello 상황에 맞는 메뉴에서 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-222">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![솔루션 탐색기 - Azure 역할의 상황에 맞는 메뉴](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="6dc02-224">선택 hello **로컬 저장소** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-224">Select hello **Local Storage** tab.</span></span>

    ![로컬 저장소 탭](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab.png)

1. <span data-ttu-id="6dc02-226">Hello에 **서비스 구성** 나열 되어 있는지 확인 합니다. **모든 구성** hello 로컬 저장소 설정이 적용 tooall 서비스 구성을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-226">In hello **Service Configuration** list, ensure that **All Configurations** is selected as hello local storage settings apply tooall service configurations.</span></span> <span data-ttu-id="6dc02-227">사용할 수 없게 하는 hello 페이지의 모든 hello 입력된 필드에 다른 값이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-227">Any other value results in all hello input fields on hello page being disabled.</span></span> 

    ![서비스 구성 목록](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-service-configuration.png)

1. <span data-ttu-id="6dc02-229">로컬 저장소 항목 tooadd 선택 **로컬 저장소 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-229">tooadd a local storage entry, select **Add Local Storage**.</span></span>

    ![로컬 저장소 추가](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-add-local-storage.png)

1. <span data-ttu-id="6dc02-231">Hello 새 로컬 저장소 항목에 toohello 목록 추가 되 면 hello 목록의 hello 행 hello 필요한 정보로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-231">Once hello new local storage entry has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![새 로컬 저장소 항목](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-new-local-storage.png)

    - <span data-ttu-id="6dc02-233">**이름** -hello 새 로컬 저장소에 대 한 toouse 되도록 hello 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-233">**Name** - Enter hello name that you want toouse for hello new local storage.</span></span>
    - <span data-ttu-id="6dc02-234">**크기 (MB)** -hello 새 로컬 저장소에 필요한 mb hello 크기를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-234">**Size (MB)** - Enter hello size in MB that you need for hello new local storage.</span></span>
    - <span data-ttu-id="6dc02-235">**역할 재생에서 정리** -hello 가상 컴퓨터 역할 hello에 대 한 재활용 될 때이 옵션 tooremove hello 데이터 hello 새 로컬 저장소에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-235">**Clean on role recycle** - Select this option tooremove hello data in hello new local storage when hello virtual machine for hello role is recycled.</span></span>

1. <span data-ttu-id="6dc02-236">로컬 저장소 항목 toodelete hello 항목을 선택한 다음 선택 **로컬 저장소 제거**합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-236">toodelete a local storage entry, select hello entry, and then select **Remove Local Storage**.</span></span>

1. <span data-ttu-id="6dc02-237">Hello Visual Studio에서에서 도구 모음 선택 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-237">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-accessing-local-storage"></a><span data-ttu-id="6dc02-238">프로그래밍 방식으로 로컬 저장소 액세스</span><span class="sxs-lookup"><span data-stu-id="6dc02-238">Programmatically accessing local storage</span></span>

<span data-ttu-id="6dc02-239">이 섹션에서는 tooprogrammatically 로컬 저장소를 사용 하 여 C# 테스트 텍스트 파일을 작성 하 여 액세스 하는 방법을 보여 줍니다. `MyLocalStorageTest.txt`합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-239">This section illustrates how tooprogrammatically access local storage using C# by writing a test text file `MyLocalStorageTest.txt`.</span></span>  

### <a name="write-a-text-file-toolocal-storage"></a><span data-ttu-id="6dc02-240">텍스트 파일 toolocal 저장소 쓰기</span><span class="sxs-lookup"><span data-stu-id="6dc02-240">Write a text file toolocal storage</span></span>

<span data-ttu-id="6dc02-241">hello 코드 다음에 어떻게 toowrite는 텍스트 파일 toolocal 저장소의 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-241">hello following code shows an example of how toowrite a text file toolocal storage.</span></span> <span data-ttu-id="6dc02-242">Hello 대체 &lt;LocalStorageName > 자리 표시자 hello 적절 한 값으로.</span><span class="sxs-lookup"><span data-stu-id="6dc02-242">Replace hello &lt;LocalStorageName> placeholder with hello appropriate value.</span></span> 

    ```csharp
    // Retrieve an object that points toohello local storage resource
    LocalResource localResource = RoleEnvironment.GetLocalResource("<LocalStorageName>");
    
    //Define hello file name and path
    string[] paths = { localResource.RootPath, "MyLocalStorageTest.txt" };
    String filePath = Path.Combine(paths);
    
    using (FileStream writeStream = File.Create(filePath))
    {
        Byte[] textToWrite = new UTF8Encoding(true).GetBytes("Testing Web role storage");
        writeStream.Write(textToWrite, 0, textToWrite.Length);
    }

    ```

### <a name="find-a-file-written-toolocal-storage"></a><span data-ttu-id="6dc02-243">Toolocal 저장소 기록 파일 찾기</span><span class="sxs-lookup"><span data-stu-id="6dc02-243">Find a file written toolocal storage</span></span>

<span data-ttu-id="6dc02-244">다음이 단계를 수행 하는 hello 코드 hello 이전 섹션에서 만든 tooview hello 파일:</span><span class="sxs-lookup"><span data-stu-id="6dc02-244">tooview hello file created by hello code in hello previous section, follow these steps:</span></span>
    
1.  <span data-ttu-id="6dc02-245">Windows 알림 영역 hello hello Azure 아이콘을 마우스 오른쪽 단추로 클릭, hello 상황에 맞는 메뉴에서 선택 **계산 에뮬레이터 UI 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-245">In hello Windows notification area, right-click hello Azure icon, and, from hello context menu, select **Show Compute Emulator UI**.</span></span> 

    ![Azure 계산 에뮬레이터 표시](./media/vs-azure-tools-configure-roles-for-cloud-service/show-compute-emulator.png)

1. <span data-ttu-id="6dc02-247">Hello 웹 역할을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-247">Select hello web role.</span></span>

    ![Azure 계산 에뮬레이터](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator.png)

1. <span data-ttu-id="6dc02-249">Hello에 **Microsoft Azure 계산 에뮬레이터** 메뉴 선택 **도구** > **로컬 저장소 열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-249">On hello **Microsoft Azure Compute Emulator** menu, select **Tools** > **Open local store**.</span></span>

    ![로컬 저장소 메뉴 항목 열기](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator-open-local-store-menu.png)

1. <span data-ttu-id="6dc02-251">Hello Windows 탐색기 창이 열리면 입력 ' MyLocalStorageTest.txt ' hello에 **검색** 텍스트 상자와 선택 **Enter** toostart hello 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-251">When hello Windows Explorer window opens, enter `MyLocalStorageTest.txt`\` into hello **Search** text box, and select **Enter** toostart hello search.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6dc02-252">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6dc02-252">Next steps</span></span>
<span data-ttu-id="6dc02-253">[Azure 프로젝트 구성](vs-azure-tools-configuring-an-azure-project.md)을 읽고 Visual Studio에서 Azure 프로젝트에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-253">Learn more about Azure projects in Visual Studio by reading [Configuring an Azure Project](vs-azure-tools-configuring-an-azure-project.md).</span></span> <span data-ttu-id="6dc02-254">에 대 한 자세한 hello 클라우드 서비스 스키마를 읽어서 [스키마 참조](https://msdn.microsoft.com/library/azure/dd179398)합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc02-254">Learn more about hello cloud service schema by reading [Schema Reference](https://msdn.microsoft.com/library/azure/dd179398).</span></span>

