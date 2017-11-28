---
title: "Hudson Continuous Integration과 함께 Azure 슬레이브 플러그인을 사용하는 방법 | Microsoft Docs"
description: "Hudson Continuous Integration과 함께 Azure 슬레이브 플러그인을 사용하는 방법에 대해 설명합니다."
services: virtual-machines-linux
documentationcenter: 
author: rmcmurray
manager: wpickett
editor: 
ms.assetid: b2083d1c-4de8-4a19-a615-ccc9d9b6e1d9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: c11b59f8ea432075b147a391de4b7bd3331e639e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-azure-slave-plug-in-with-hudson-continuous-integration"></a><span data-ttu-id="f9bce-103">Hudson Continuous Integration과 함께 Azure 슬레이브 플러그인을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="f9bce-103">How to use the Azure slave plug-in with Hudson Continuous Integration</span></span>
<span data-ttu-id="f9bce-104">Hudson용 Azure 슬레이브 플러그인을 사용하면 분산된 빌드를 실행할 때 슬레이브 노드를 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-104">The Azure slave plug-in for Hudson enables you to provision slave nodes on Azure when running distributed builds.</span></span>

## <a name="install-the-azure-slave-plug-in"></a><span data-ttu-id="f9bce-105">Azure 슬레이브 플러그인 설치</span><span class="sxs-lookup"><span data-stu-id="f9bce-105">Install the Azure Slave plug-in</span></span>
1. <span data-ttu-id="f9bce-106">Hudson 대시보드에서 **Manage Hudson**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-106">In the Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="f9bce-107">**Manage Hudson** 페이지에서 **Manage Plugins**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-107">In the **Manage Hudson** page, click on **Manage Plugins**.</span></span>
3. <span data-ttu-id="f9bce-108">**Available** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-108">Click the **Available** tab.</span></span>
4. <span data-ttu-id="f9bce-109">**검색**을 클릭하고 **Azure**를 입력하여 목록에 관련 플러그인만 표시되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-109">Click **Search** and type **Azure** to limit the list to relevant plug-ins.</span></span>
   
    <span data-ttu-id="f9bce-110">사용 가능한 플러그인 목록을 스크롤할 경우 **기타** 탭의 **클러스터 관리 및 분산 빌드** 섹션에서 Azure 슬레이브 플러그인이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-110">If you opt to scroll through the list of available plug-ins, you will find the Azure slave plug-in under the **Cluster Management and Distributed Build** section in the **Others** tab.</span></span>
5. <span data-ttu-id="f9bce-111">**Azure Slave Plugin**에 대한 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-111">Select the checkbox for **Azure Slave Plugin**.</span></span>
6. <span data-ttu-id="f9bce-112">**Install**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-112">Click **Install**.</span></span>
7. <span data-ttu-id="f9bce-113">Hudson을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-113">Restart Hudson.</span></span>

<span data-ttu-id="f9bce-114">이제 플러그인이 설치되었으므로 다음으로 Azure 구독 프로필로 플러그인을 구성하고 슬레이브 노드에 대한 VM을 만드는 데 사용할 템플릿을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-114">Now that the plug-in is installed, the next steps would be to configure the plug-in with your Azure subscription profile and to create a template that will be used in creating the VM for the slave node.</span></span>

## <a name="configure-the-azure-slave-plug-in-with-your-subscription-profile"></a><span data-ttu-id="f9bce-115">구독 프로필로 Azure 슬레이브 플러그인 구성</span><span class="sxs-lookup"><span data-stu-id="f9bce-115">Configure the Azure Slave plug-in with your subscription profile</span></span>
<span data-ttu-id="f9bce-116">게시 설정으로도 참조되는 구독 프로필은 보안 자격 증명 및 개발 환경에서 Azure로 작업할 때 필요한 일부 추가 정보를 포함하는 XML 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-116">A subscription profile, also referred to as publish settings, is an XML file that contains secure credentials and some additional information you'll need to work with Azure in your development environment.</span></span> <span data-ttu-id="f9bce-117">Azure 슬레이브 플러그인을 구성하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-117">To configure the Azure slave plug-in, you need:</span></span>

* <span data-ttu-id="f9bce-118">구독 ID</span><span class="sxs-lookup"><span data-stu-id="f9bce-118">Your subscription id</span></span>
* <span data-ttu-id="f9bce-119">구독에 대한 관리 인증서</span><span class="sxs-lookup"><span data-stu-id="f9bce-119">A management certificate for your subscription</span></span>

<span data-ttu-id="f9bce-120">이러한 항목은 [구독 프로필]에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-120">These can be found in your [subscription profile].</span></span> <span data-ttu-id="f9bce-121">다음은 구독 프로필의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-121">Below is an example of a subscription profile.</span></span>

    <?xml version="1.0" encoding="utf-8"?>

        <PublishData>

          <PublishProfile SchemaVersion="2.0" PublishMethod="AzureServiceManagementAPI">

        <Subscription

              ServiceManagementUrl="https://management.core.windows.net"

              Id="<Subscription ID>"

              Name="Pay-As-You-Go"
            ManagementCertificate="<Management certificate value>" />

          </PublishProfile>

    </PublishData>

<span data-ttu-id="f9bce-122">구독 프로필이 있으면 다음 단계를 따라 Azure 슬레이브 플러그인을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-122">Once you have your subscription profile, follow these steps to configure the Azure slave plug-in.</span></span>

1. <span data-ttu-id="f9bce-123">Hudson 대시보드에서 **Manage Hudson**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-123">In the Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="f9bce-124">**Configure System**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-124">Click **Configure System**.</span></span>
3. <span data-ttu-id="f9bce-125">페이지를 아래로 스크롤해서 **Cloud** 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-125">Scroll down the page to find the **Cloud** section.</span></span>
4. <span data-ttu-id="f9bce-126">**Add new cloud > Microsoft Azure**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-126">Click **Add new cloud > Microsoft Azure**.</span></span>
   
    ![새 클라우드 추가][add new cloud]
   
    <span data-ttu-id="f9bce-128">그러면 구독 세부 정보를 입력해야 하는 필드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-128">This will show the fields where you need to enter your subscription details.</span></span>
   
    ![프로필 구성][configure profile]
5. <span data-ttu-id="f9bce-130">구독 프로필에서 구독 ID 및 관리 인증서를 복사하여 해당 필드에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-130">Copy the subscription id and management certificate from your subscription profile and paste them in the appropriate fields.</span></span>
   
    <span data-ttu-id="f9bce-131">구독 ID 및 관리 인증서를 복사할 때 값을 묶고 있는 따옴표는 포함하지 **마세요** .</span><span class="sxs-lookup"><span data-stu-id="f9bce-131">When copying the subscription id and management certificate, **do not** include the quotes that enclose the values.</span></span>
6. <span data-ttu-id="f9bce-132">**Verify configuration**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-132">Click on **Verify configuration**.</span></span>
7. <span data-ttu-id="f9bce-133">구성이 성공적으로 확인되면 **Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-133">When the configuration is verified successfully, click **Save**.</span></span>

## <a name="set-up-a-virtual-machine-template-for-the-azure-slave-plug-in"></a><span data-ttu-id="f9bce-134">Azure 슬레이브 플러그인용 가상 컴퓨터 템플릿 설정</span><span class="sxs-lookup"><span data-stu-id="f9bce-134">Set up a virtual machine template for the Azure Slave plug-in</span></span>
<span data-ttu-id="f9bce-135">가상 컴퓨터 템플릿은 플러그인이 Azure에 슬레이브 노드를 만들 때 사용할 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-135">A virtual machine template defines the parameters the plug-in will use to create a slave node on Azure.</span></span> <span data-ttu-id="f9bce-136">다음 단계에서는 Ubuntu VM용 템플릿을 만들 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-136">In the following steps we'll be creating template for an Ubuntu VM.</span></span>

1. <span data-ttu-id="f9bce-137">Hudson 대시보드에서 **Manage Hudson**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-137">In the Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="f9bce-138">**Configure System**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-138">Click on **Configure System**.</span></span>
3. <span data-ttu-id="f9bce-139">페이지를 아래로 스크롤해서 **Cloud** 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-139">Scroll down the page to find the **Cloud** section.</span></span>
4. <span data-ttu-id="f9bce-140">**Cloud** 섹션 내에서 **Add Azure Virtual Machine Template**를 찾은 후 **Add** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-140">Within the **Cloud** section, find **Add Azure Virtual Machine Template** and click the **Add** button.</span></span>
   
    ![VM 템플릿 추가][add vm template]
5. <span data-ttu-id="f9bce-142">**Name** 필드에서 클라우드 서비스 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-142">Specify a cloud service name in the **Name** field.</span></span> <span data-ttu-id="f9bce-143">지정한 이름이 기존 클라우드 서비스를 참조하는 경우, VM은 해당 서비스를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-143">If the name you specify refers to an existing cloud service, the VM will be provisioned in that service.</span></span> <span data-ttu-id="f9bce-144">그렇지 않은 경우 Azure는 새로운 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-144">Otherwise, Azure will create a new one.</span></span>
6. <span data-ttu-id="f9bce-145">**Description** 필드에 만드는 템플릿을 설명하는 텍스트를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-145">In the **Description** field, enter text that describes the template you are creating.</span></span> <span data-ttu-id="f9bce-146">이 정보는 설명 목적이며 VM 프로비저닝에는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-146">This information is only for documentary purposes and is not used in provisioning a VM.</span></span>
7. <span data-ttu-id="f9bce-147">**Labels** 필드에 **linux**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-147">In the **Labels** field, enter **linux**.</span></span> <span data-ttu-id="f9bce-148">이 레이블은 만드는 템플릿을 식별하는 데 사용되며, 추후 Hudson 작업을 만들 때 참조에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-148">This label is used to identify the template you are creating and is subsequently used to reference the template when creating a Hudson job.</span></span>
8. <span data-ttu-id="f9bce-149">VM을 만들 하위 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-149">Select a region where the VM will be created.</span></span>
9. <span data-ttu-id="f9bce-150">적절한 VM 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-150">Select the appropriate VM size.</span></span>
10. <span data-ttu-id="f9bce-151">VM을 만들 저장소 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-151">Specify a storage account where the VM will be created.</span></span> <span data-ttu-id="f9bce-152">사용할 클라우드 서비스와 동일한 하위 지역에 있는지 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="f9bce-152">Make sure that it is in the same region as the cloud service you'll be using.</span></span> <span data-ttu-id="f9bce-153">이후 만들어질 새 저장소를 사용하려는 경우 이 필드는 비워두어도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-153">If you want new storage to be created, you can leave this field blank.</span></span>
11. <span data-ttu-id="f9bce-154">보존 시간은 Hudson이 유휴 슬레이브를 삭제하기까지의 시간을 분 단위로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-154">Retention time specifies the number of minutes before Hudson deletes an idle slave.</span></span> <span data-ttu-id="f9bce-155">기본값인 60으로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-155">Leave this at the default value of 60.</span></span>
12. <span data-ttu-id="f9bce-156">**Usage**에서 슬레이브 노드가 사용되는 경우에 적절한 조건을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-156">In **Usage**, select the appropriate condition when this slave node will be used.</span></span> <span data-ttu-id="f9bce-157">지금은 **Utilize this node as much as possible**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-157">For now, select **Utilize this node as much as possible**.</span></span>
    
     <span data-ttu-id="f9bce-158">이때 다음과 유사한 형식으로 표시되게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-158">At this point, your form would look somewhat similar to this:</span></span>
    
     ![템플릿 구성][template config]
13. <span data-ttu-id="f9bce-160">**Image Family or Id** 에서 VM에 설치할 시스템 이미지를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-160">In **Image Family or Id** you have to specify what system image will be installed on your VM.</span></span> <span data-ttu-id="f9bce-161">이미지 제품군 목록에서 선택하거나 사용자 지정 이미지를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-161">You can either select from a list of image families or specify a custom image.</span></span>
    
     <span data-ttu-id="f9bce-162">이미지 제품군 목록에서 선택하려는 경우, 이미지 제품군 이름의 첫 글자(대/소문자 구분)를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-162">If you want to select from a list of image families, enter the first character (case-sensitive) of the image family name.</span></span> <span data-ttu-id="f9bce-163">예를 들어 **U** 를 입력하면 Ubuntu Server 제품군 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-163">For instance, typing **U** will bring up a list of Ubuntu Server families.</span></span> <span data-ttu-id="f9bce-164">목록에서 선택하면 VM을 프로비저닝할 때 Jenkins가 해당 제품군에서 시스템 이미지의 최신 버전을 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-164">Once you select from the list, Jenkins will use the latest version of that system image from that family when provisioning your VM.</span></span>
    
     ![OS 제품군 목록][OS family list]
    
     <span data-ttu-id="f9bce-166">이미지 제품군 목록에서 선택하는 대신 사용하고자 하는 사용자 지정 이미지가 있는 경우, 해당 사용자 지정 이미지의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-166">If you have a custom image that you want to use instead, enter the name of that custom image.</span></span> <span data-ttu-id="f9bce-167">사용자 지정 이미지 이름은 목록에 표시되지 않으므로 이름을 올바르게 입력했는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-167">Custom image names are not shown in a list so you have to ensure that the name is entered correctly.</span></span>    
    
     <span data-ttu-id="f9bce-168">이 자습서에서는 **U**를 입력하여 Ubuntu 이미지 목록을 표시하고 **Ubuntu Server 14.04 LTS**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-168">For this tutorial, type **U** to bring up a list of Ubuntu images and select **Ubuntu Server 14.04 LTS**.</span></span>
14. <span data-ttu-id="f9bce-169">**Launch method**에 대해서는 **SSH**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-169">For **Launch method**, select **SSH**.</span></span>
15. <span data-ttu-id="f9bce-170">다음 스크립트를 복사하여 **Init script** 필드에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-170">Copy the script below and paste in the **Init script** field.</span></span>
    
         # Install Java
    
         sudo apt-get -y update
    
         sudo apt-get install -y openjdk-7-jdk
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y openjdk-7-jdk
    
         # Install git
    
         sudo apt-get install -y git
    
         #Install ant
    
         sudo apt-get install -y ant
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y ant
    
     <span data-ttu-id="f9bce-171">**Init script** 는 VM이 만들어진 다음에 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-171">The **Init script** will be executed after the VM is created.</span></span> <span data-ttu-id="f9bce-172">이 예에서는 이 스크립트가 Java, git 및 ant를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-172">In this example, the script installs Java, git, and ant.</span></span>
16. <span data-ttu-id="f9bce-173">**Username** 및 **Password** 필드에는 VM에 만들어질 관리자 계정에 대한 기본 설정 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-173">In the **Username** and **Password** fields, enter your preferred values for the administrator account that will be created on your VM.</span></span>
17. <span data-ttu-id="f9bce-174">**Verify Template** 을 클릭하여 지정한 매개 변수가 유효한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-174">Click on **Verify Template** to check if the parameters you specified are valid.</span></span>
18. <span data-ttu-id="f9bce-175">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-175">Click on **Save**.</span></span>

## <a name="create-a-hudson-job-that-runs-on-a-slave-node-on-azure"></a><span data-ttu-id="f9bce-176">Azure의 슬레이브 노드에서 실행되는 Hudson 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="f9bce-176">Create a Hudson job that runs on a slave node on Azure</span></span>
<span data-ttu-id="f9bce-177">이 섹션에서는 Azure의 슬레이브 노드에서 실행할 Hudson 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-177">In this section, you'll be creating a Hudson task that will run on a slave node on Azure.</span></span>

1. <span data-ttu-id="f9bce-178">Hudson 대시보드에서 **New Job**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-178">In the Hudson dashboard, click **New Job**.</span></span>
2. <span data-ttu-id="f9bce-179">만들 작업에 대한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-179">Enter a name for the job you are creating.</span></span>
3. <span data-ttu-id="f9bce-180">작업 유형에 대해서는 **Build a free-style software job**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-180">For the job type, select **Build a free-style software job**.</span></span>
4. <span data-ttu-id="f9bce-181">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-181">Click **OK**.</span></span>
5. <span data-ttu-id="f9bce-182">작업 구성 페이지에서 **Restrict where this project can be run**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-182">In the job configuration page, select **Restrict where this project can be run**.</span></span>
6. <span data-ttu-id="f9bce-183">**Node and label menu**를 선택하고 **linux**를 선택합니다(이전 섹션에서 가상 컴퓨터 템플릿을 만들 때 이 레이블을 지정했습니다).</span><span class="sxs-lookup"><span data-stu-id="f9bce-183">Select **Node and label menu** and select **linux** (we specified this label when creating the virtual machine template in the previous section).</span></span>
7. <span data-ttu-id="f9bce-184">**빌드** 섹션에서 **빌드 단계 추가**를 클릭하고 **셸 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-184">In the **Build** section, click **Add build step** and select **Execute shell**.</span></span>
8. <span data-ttu-id="f9bce-185">다음 스크립트를 편집하여 **{github 계정 이름}**, **{프로젝트 이름}** 및 **{프로젝트 디렉터리}**를 적절한 값으로 대체하고, 편집한 스크립트를 표시되는 텍스트 영역에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-185">Edit the following script, replacing **{your github account name}**, **{your project name}**, and **{your project directory}** with appropriate values, and paste the edited script in the text area that appears.</span></span>
   
        # Clone from git repo
   
        currentDir="$PWD"
   
        if [ -e {your project directory} ]; then
   
              cd {your project directory}
   
              git pull origin master
   
        else
   
              git clone https://github.com/{your github account name}/{your project name}.git
   
        fi
   
        # change directory to project
   
        cd $currentDir/{your project directory}
   
        #Execute build task
   
        ant
9. <span data-ttu-id="f9bce-186">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-186">Click on **Save**.</span></span>
10. <span data-ttu-id="f9bce-187">Hudson 대시보드에서 방금 만든 작업을 찾아서 **Schedule a build** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-187">In the Hudson dashboard, find the job you just created and click on the **Schedule a build** icon.</span></span>

<span data-ttu-id="f9bce-188">그러면 Hudson은 이전 섹션에서 만든 템플릿을 사용하여 슬레이브 노드를 만들고 이 작업에 대한 빌드 단계에서 지정한 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bce-188">Hudson will then create a slave node using the template created in the previous section and execute the script you specified in the build step for this task.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9bce-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f9bce-189">Next Steps</span></span>
<span data-ttu-id="f9bce-190">Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Azure Java 개발자 센터]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9bce-190">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<!-- URL List -->

<span data-ttu-id="f9bce-191">[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="f9bce-191">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="f9bce-192">[구독 프로필]: http://go.microsoft.com/fwlink/?LinkID=396395</span><span class="sxs-lookup"><span data-stu-id="f9bce-192">[subscription profile]: http://go.microsoft.com/fwlink/?LinkID=396395</span></span>

<!-- IMG List -->

[add new cloud]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addcloud.png
[configure profile]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-configureprofile.png
[add vm template]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addnewvmtemplate.png
[template config]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-templateconfig1-withdata.png
[OS family list]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-oslist.png

