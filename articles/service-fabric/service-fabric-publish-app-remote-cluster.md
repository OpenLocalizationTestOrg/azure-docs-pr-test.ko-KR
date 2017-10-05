---
title: "Visual Studio로 원격 클러스터에 앱 게시 | Microsoft Docs"
description: "Visual Studio를 사용하여 원격 서비스 패브릭 클러스터에 응용 프로그램을 게시하는 방법을 알아봅니다."
services: service-fabric
documentationcenter: na
author: cawams
manager: timlt
editor: 
ms.assetid: faecd892-eb54-4d9c-8023-c67442afb8e8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/29/2016
ms.author: cawa
ms.openlocfilehash: c440c520d84fc503ff9e705555449e92555d4721
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-remove-applications-using-visual-studio"></a><span data-ttu-id="13d5b-103">Visual Studio를 사용하여 응용 프로그램 배포 및 제거</span><span class="sxs-lookup"><span data-stu-id="13d5b-103">Deploy and remove applications using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="13d5b-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="13d5b-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="13d5b-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="13d5b-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="13d5b-106">FabricClient API</span><span class="sxs-lookup"><span data-stu-id="13d5b-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="13d5b-107">Visual Studio용 Azure 서비스 패브릭 확장은 서비스 패브릭 클러스터에 응용 프로그램을 게시하는 반복 및 스크립트 가능한 간편한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-107">The Azure Service Fabric extension for Visual Studio provides an easy, repeatable, and scriptable way to publish an application to a Service Fabric cluster.</span></span>

## <a name="the-artifacts-required-for-publishing"></a><span data-ttu-id="13d5b-108">게시에 필요한 아티팩트</span><span class="sxs-lookup"><span data-stu-id="13d5b-108">The artifacts required for publishing</span></span>
### <a name="deploy-fabricapplicationps1"></a><span data-ttu-id="13d5b-109">Deploy-FabricApplication.ps1</span><span class="sxs-lookup"><span data-stu-id="13d5b-109">Deploy-FabricApplication.ps1</span></span>
<span data-ttu-id="13d5b-110">서비스 패브릭 응용 프로그램 게시를 위한 매개 변수로 게시 프로필 경로를 사용하는 PowerShell 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-110">This is a PowerShell script that uses a publish profile path as a parameter for publishing Service Fabric applications.</span></span> <span data-ttu-id="13d5b-111">이 스크립트는 응용 프로그램의 일부이므로 응용 프로그램 맞게 필요에 따라 편하게 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-111">Since this script is part of your application, you are welcome to modify it as necessary for your application.</span></span>

### <a name="publish-profiles"></a><span data-ttu-id="13d5b-112">게시 프로필</span><span class="sxs-lookup"><span data-stu-id="13d5b-112">Publish profiles</span></span>
<span data-ttu-id="13d5b-113">이름이 **PublishProfiles**인 Service Fabric 응용 프로그램 프로젝트의 폴더에는 다음과 같이 응용 프로그램을 게시하기 위해 중요한 정보를 저장하는 XML 파일이 들어있습니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-113">A folder in the Service Fabric application project called **PublishProfiles** contains XML files that store essential information for publishing an application, such as:</span></span>

* <span data-ttu-id="13d5b-114">서비스 패브릭 클러스터 연결 매개 변수</span><span class="sxs-lookup"><span data-stu-id="13d5b-114">Service Fabric cluster connection parameters</span></span>
* <span data-ttu-id="13d5b-115">응용 프로그램 매개 변수 파일 경로</span><span class="sxs-lookup"><span data-stu-id="13d5b-115">Path to an application parameter file</span></span>
* <span data-ttu-id="13d5b-116">업그레이드 설정</span><span class="sxs-lookup"><span data-stu-id="13d5b-116">Upgrade settings</span></span>

<span data-ttu-id="13d5b-117">기본적으로 응용 프로그램은 Local.1Node.xml, Local.5Node.xml 및 Cloud.xml의 세 가지 게시 프로필을 포함하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-117">By default, your application will include three publish profiles: Local.1Node.xml, Local.5Node.xml, and Cloud.xml.</span></span> <span data-ttu-id="13d5b-118">기본 파일 중 하나를 복사 및 붙여넣기하여 프로필을 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-118">You can add more profiles by copying and pasting one of the default files.</span></span>

### <a name="application-parameter-files"></a><span data-ttu-id="13d5b-119">응용 프로그램 매개 변수 파일</span><span class="sxs-lookup"><span data-stu-id="13d5b-119">Application parameter files</span></span>
<span data-ttu-id="13d5b-120">이름이 **ApplicationParameters**인 서비스 패브릭 응용 프로그램 프로젝트의 폴더에는 사용자 특정 응용 프로그램 매니페스트 매개 변수 값에 대한 XML 파일이 들어있습니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-120">A folder in the Service Fabric application project called **ApplicationParameters** contains XML files for user-specified application manifest parameter values.</span></span> <span data-ttu-id="13d5b-121">배포 설정에 다른 값을 사용할 수 잇게 응용 프로그램 매니페스트 파일을 매개 변수화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-121">Application manifest files can be parameterized so that you can use different values for deployment settings.</span></span> <span data-ttu-id="13d5b-122">응용 프로그램을 매개 변수화하는 방법에 대한 자세한 내용은 [서비스 패브릭에서 여러 환경 관리](service-fabric-manage-multiple-environment-app-configuration.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13d5b-122">To learn more about parameterizing your application, see [Manage multiple environments in Service Fabric](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

> [!NOTE]
> <span data-ttu-id="13d5b-123">행위자 서비스의 경우 편집기에서 또는 게시 대화 상자를 통해 파일 편집을 시도하기 전에 프로젝트를 먼저 빌드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-123">For actor services, you should build the project first before attempting to edit the file in an editor or through the publish dialog box.</span></span> <span data-ttu-id="13d5b-124">매니페스트 파일의 일부가 빌드 중에 생성되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-124">This is because part of the manifest files will be generated during the build.</span></span>

## <a name="to-publish-an-application-using-the-publish-service-fabric-application-dialog-box"></a><span data-ttu-id="13d5b-125">Service Fabric 응용 프로그램 게시 대화 상자를 사용하여 응용 프로그램을 게시하려면</span><span class="sxs-lookup"><span data-stu-id="13d5b-125">To publish an application using the Publish Service Fabric Application dialog box</span></span>
<span data-ttu-id="13d5b-126">다음 단계에서는 Visual Studio Service Fabric 도구에서 제공하는 **Service Fabric 응용 프로그램 게시** 대화 상자를 사용하여 응용 프로그램을 게시하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-126">The following steps demonstrate how to publish an application using the **Publish Service Fabric Application** dialog box provided by the Visual Studio Service Fabric Tools.</span></span>

1. <span data-ttu-id="13d5b-127">Service Fabric 응용 프로그램 프로젝트의 바로 가기 메뉴에서 **게시...**를 선택하여</span><span class="sxs-lookup"><span data-stu-id="13d5b-127">On the shortcut menu of the Service Fabric Application project, choose **Publish…**</span></span> <span data-ttu-id="13d5b-128">**Service Fabric 응용 프로그램 게시** 대화 상자를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-128">to view the **Publish Service Fabric Application** dialog box.</span></span>
   
    ![**Service Fabric 응용 프로그램 게시** 대화 상자][0]
   
    <span data-ttu-id="13d5b-130">**대상 프로필** 드롭다운 목록 상자에서 선택한 파일에 **매니페스트 버전**을 제외한 모든 설정이 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-130">The file selected in the **Target profile** dropdown list box is where all of the settings, except **Manifest versions**, are saved.</span></span> <span data-ttu-id="13d5b-131">기존 프로필을 재사용하거나 **대상 프로필** 드롭다운 목록 상자에서 **<프로필 관리…>**를 선택하여 새 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-131">You can either reuse an existing profile or create a new one by choosing **<Manage Profiles…>** in the **Target profile** dropdown list box.</span></span> <span data-ttu-id="13d5b-132">게시 프로필을 선택하면 그 내용이 대화 상자의 해당 필드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-132">When you choose a publish profile, its contents appear in the corresponding fields of the dialog box.</span></span> <span data-ttu-id="13d5b-133">언제든 변경 사항을 저장하려면 **프로필 저장** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-133">To save your changes at any time, choose the **Save Profile** link.</span></span>    
2. <span data-ttu-id="13d5b-134">**연결 끝점** 섹션에서 로컬 또는 원격 Service Fabric 클러스터의 게시 끝점을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-134">In the **Connection endpoint** section, specify a local or remote Service Fabric cluster’s publishing endpoint.</span></span> <span data-ttu-id="13d5b-135">연결 끝점을 추가 또는 변경하려면 **연결 끝점** 드롭다운 목록을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-135">To add or change the connection endpoint, click on the **Connection Endpoint** dropdown list.</span></span> <span data-ttu-id="13d5b-136">이 목록은 Azure 구독에 따라 게시할 수 있는 사용 가능한 Service Fabric 클러스터 연결 끝점을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-136">The list shows the available Service Fabric cluster connection endpoints to which you can publish based on your Azure subscription(s).</span></span> <span data-ttu-id="13d5b-137">Visual Studio에 아직 로그인하지 않은 경우 로그인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-137">Note that if you are not already logged in to Visual Studio, you will be prompted to do so.</span></span>
   
    <span data-ttu-id="13d5b-138">클러스터 선택 대화 상자를 사용하여 사용 가능한 구독 및 클러스터 집합 중에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-138">Use the cluster selection dialog box to choose from the set of available subscriptions and clusters.</span></span>
   
    ![**Service Fabric 클러스터 선택** 대화 상자][1]
   
   > [!NOTE]
   > <span data-ttu-id="13d5b-140">임의의 끝점(예: 당사 클러스터)에 게시하려는 경우 아래 **임의 클러스터 끝점에 게시** 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13d5b-140">If you would like to publish to an arbitrary endpoint (such as a party cluster), see the **Publishing to an arbitrary cluster endpoint** section below.</span></span>
   > 
   > 
   
    <span data-ttu-id="13d5b-141">끝점을 선택하면 Visual Studio가 선택한 서비스 패브릭 클러스터에 대해 연결 유효성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-141">Once you choose an endpoint, Visual Studio validates the connection to the selected Service Fabric cluster.</span></span> <span data-ttu-id="13d5b-142">클러스터에 보안이 없으면 Visual Studio가 즉시 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-142">If the cluster isn't secure, Visual Studio can connect to it immediately.</span></span> <span data-ttu-id="13d5b-143">그러나 클러스터가 보안 상태이면 계속하기 전에 로컬 컴퓨터에 인증서를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-143">However, if the cluster is secure, you'll need to install a certificate on your local computer before proceeding.</span></span> <span data-ttu-id="13d5b-144">자세한 내용은 [보안 연결을 구성하는 방법](service-fabric-visualstudio-configure-secure-connections.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13d5b-144">See [How to configure secure connections](service-fabric-visualstudio-configure-secure-connections.md) for more information.</span></span> <span data-ttu-id="13d5b-145">완료되면 **확인** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-145">When you're done, choose the **OK** button.</span></span> <span data-ttu-id="13d5b-146">선택한 클러스터가 **Service Fabric 응용 프로그램 게시** 대화 상자에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-146">The selected cluster appears in the **Publish Service Fabric Application** dialog box.</span></span>
3. <span data-ttu-id="13d5b-147">**응용 프로그램 매개 변수 파일** 드롭다운 목록에서 응용 프로그램 매개 변수 파일로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-147">In the **Application Parameter File** dropdown list box, navigate to an application parameter file.</span></span> <span data-ttu-id="13d5b-148">응용 프로그램 매개 변수 파일은 응용 프로그램 매니페스트 파일의 매개 변수에 대한 사용자 특정 값을 담고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-148">An application parameter file holds user-specified values for parameters in the application manifest file.</span></span> <span data-ttu-id="13d5b-149">매개 변수를 추가 또는 변경하려면 **편집** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-149">To add or change a parameter, choose the **Edit** button.</span></span> <span data-ttu-id="13d5b-150">**매개 변수** 표에서 매개 변수의 값을 입력하거나 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-150">Enter or change the parameter's value in the **Parameters** grid.</span></span> <span data-ttu-id="13d5b-151">완료되면 **저장** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-151">When you're done, choose the **Save** button.</span></span>
   
    ![**매개 변수 편집** 대화 상자][2]
4. <span data-ttu-id="13d5b-153">**응용 프로그램 업그레이드** 확인란을 사용하여 이 게시 작업이 업그레이드인지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-153">Use the **Upgrade the Application** checkbox to specify whether this publish action is an upgrade.</span></span> <span data-ttu-id="13d5b-154">업그레이드 게시 작업은 일반적인 게시 작업과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-154">Upgrade publish actions differ from normal publish actions.</span></span> <span data-ttu-id="13d5b-155">차이점 목록은 [서비스 패브릭 응용 프로그램 업그레이드](service-fabric-application-upgrade.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13d5b-155">See [Service Fabric Application Upgrade](service-fabric-application-upgrade.md) for a list of differences.</span></span> <span data-ttu-id="13d5b-156">업그레이드 설정을 구성하려면 **업그레이드 설정 구성** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-156">To configure upgrade settings, choose the **Configure Upgrade Settings** link.</span></span> <span data-ttu-id="13d5b-157">업그레이드 매개 변수 편집기가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-157">The upgrade parameter editor appears.</span></span> <span data-ttu-id="13d5b-158">업그레이드 매개 변수에 대한 자세한 내용은 [서비스 패브릭 응용 프로그램의 업그레이드 구성](service-fabric-visualstudio-configure-upgrade.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13d5b-158">See [Configure the upgrade of a Service Fabric application](service-fabric-visualstudio-configure-upgrade.md) to learn more about upgrade parameters.</span></span>
5. <span data-ttu-id="13d5b-159">**매니페스트 버전...** 버튼을</span><span class="sxs-lookup"><span data-stu-id="13d5b-159">Choose the **Manifest Versions…**</span></span> <span data-ttu-id="13d5b-160">선택하여 **버전 편집** 대화 상자를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-160">button to view the **Edit Versions** dialog box.</span></span> <span data-ttu-id="13d5b-161">업그레이드를 수행하려면 응용 프로그램 및 서비스 버전을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-161">You need to update application and service versions for an upgrade to take place.</span></span> <span data-ttu-id="13d5b-162">응용 프로그램과 서비스 매니페스트 버전이 업그레이드 프로세스에 어떻게 영향을 미치는지 확인하려면 [Service Fabric 응용 프로그램 업그레이드 자습서](service-fabric-application-upgrade-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13d5b-162">See [Service Fabric application upgrade tutorial](service-fabric-application-upgrade-tutorial.md) to learn how application and service manifest versions impact an upgrade process.</span></span>
   
    ![**버전 편집** 대화 상자][3]
   
    <span data-ttu-id="13d5b-164">응용 프로그램 및 서비스 버전이 1.0.0과 같은 의미 체계 버전 관리나 1.0.0.0 형식의 숫자 값을 사용할 경우 **응용 프로그램 및 서비스 버전을 자동으로 업데이트** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-164">If the application and service versions use semantic versioning such as 1.0.0 or numerical values in the format of 1.0.0.0, select the **Automatically update application and service versions** option.</span></span> <span data-ttu-id="13d5b-165">이 옵션을 선택하면 코드, 구성 또는 데이터 패키지 버전이 업데이트될 때마다 서비스 및 응용 프로그램 버전 번호가 자동으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-165">When you choose this option, the service and application version numbers are automatically updated whenever a code, config, or data package version is updated.</span></span> <span data-ttu-id="13d5b-166">버전을 수동으로 편집하려면 확인란의 선택을 취소하여 이 기능을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-166">If you prefer to edit the versions manually, clear the checkbox to disable this feature.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="13d5b-167">행위자 프로젝트에 대해 모든 패키지 항목을 표시하려면 먼저 서비스 매니페스트 파일에 항목을 생성하는 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-167">For all package entries to appear for an actor project, first build the project to generate the entries in the Service Manifest files.</span></span>
   > 
   > 
6. <span data-ttu-id="13d5b-168">모든 필요한 설정을 지정한 후에는 **게시** 단추를 선택하여 응용 프로그램을 선택한 서비스 패브릭 클러스터에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-168">When you're done specifying all of the necessary settings, choose the **Publish** button to publish your application to the selected Service Fabric cluster.</span></span> <span data-ttu-id="13d5b-169">지정한 설정이 게시 프로세스에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-169">The settings that you specified are applied to the publish process.</span></span>

## <a name="publish-to-an-arbitrary-cluster-endpoint-including-party-clusters"></a><span data-ttu-id="13d5b-170">임의 클러스터 끝점(당사 클러스터 포함)에 게시</span><span class="sxs-lookup"><span data-stu-id="13d5b-170">Publish to an arbitrary cluster endpoint (including party clusters)</span></span>
<span data-ttu-id="13d5b-171">Visual Studio 게시 환경은 Azure 구독 중 하나와 연결된 원격 클러스터에 게시하도록 최적화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-171">The Visual Studio publishing experience is optimized for publishing to remote clusters associated with one of your Azure subscriptions.</span></span> <span data-ttu-id="13d5b-172">그러나 게시 프로필 XML을 직접 편집하여 임의 끝점(예: 서비스 패브릭 당사 클러스터)에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-172">However, it is possible to publish to arbitrary endpoints (such as Service Fabric party clusters) by directly editing the publish profile XML.</span></span> <span data-ttu-id="13d5b-173">위에서 설명한 대로, 기본적으로 **Local.1Node.xml**, **Local.5Node.xml** 및 **Cloud.xml**이라는 세 게시 프로필이 제공되지만 다양한 환경에 맞는 추가 프로필을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-173">As described above, three publish profiles are provided by default--**Local.1Node.xml**, **Local.5Node.xml**, and **Cloud.xml**--but you are welcome to create additional profiles for different environments.</span></span> <span data-ttu-id="13d5b-174">예를 들어 **Party.xml**라는 당사 클러스터에 게시하기 위한 프로필을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-174">For instance, you might want to create a profile for publishing to party clusters, perhaps named **Party.xml**.</span></span>

<span data-ttu-id="13d5b-175">비보안 클러스터에 연결하는 경우 `partycluster1.eastus.cloudapp.azure.com:19000`과 같은 클러스터 연결 끝점만 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-175">If you are connecting to an unsecured cluster, all that's required is the cluster connection endpoint, such as `partycluster1.eastus.cloudapp.azure.com:19000`.</span></span> <span data-ttu-id="13d5b-176">이 경우 게시 프로필의 연결 끝점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-176">In that case, the connection endpoint in the publish profile would look something like this:</span></span>

```XML
<ClusterConnectionParameters ConnectionEndpoint="partycluster1.eastus.cloudapp.azure.com:19000" />
```

  <span data-ttu-id="13d5b-177">보안 클러스터에 연결하는 경우 로컬 저장소에서 인증에 사용할 클라이언트 인증서에 대한 세부 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-177">If you are connecting to a secured cluster, you will also need to provide the details of the client certificate from the local store to be used for authentication.</span></span> <span data-ttu-id="13d5b-178">자세한 내용은 [Service Fabric 클러스터에 대한 보안 연결 구성](service-fabric-visualstudio-configure-secure-connections.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13d5b-178">For more details, see [Configuring secure connections to a Service Fabric cluster](service-fabric-visualstudio-configure-secure-connections.md).</span></span>

  <span data-ttu-id="13d5b-179">게시 프로필을 설정하면 아래와 같이 게시 대화 상자에서 이를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-179">Once your publish profile is set up, you can reference it in the publish dialog box as shown below.</span></span>

  ![게시 대화 상자에서 새 게시 프로필][4]

  <span data-ttu-id="13d5b-181">이 경우 새 게시 프로필이 기본 응용 프로그램 매개 변수 파일 중 하나를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-181">Note that in this case, the new publish profile points to one of the default application parameter files.</span></span> <span data-ttu-id="13d5b-182">이것은 동일한 응용 프로그램 구성을 다양한 환경에 게시하려는 경우 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-182">This is appropriate if you want to publish the same application configuration to a number of environments.</span></span> <span data-ttu-id="13d5b-183">반면에 게시할 각 환경에 대해 서로 다른 구성을 포함하려는 경우 해당하는 응용 프로그램 매개 변수 파일을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="13d5b-183">By contrast, in cases where you want to have different configurations for each environment that you want to publish to, it would make sense to create a corresponding application parameter file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13d5b-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="13d5b-184">Next steps</span></span>
<span data-ttu-id="13d5b-185">연속 통합 환경에서 게시 프로세스를 자동화하는 방법은 [Service Fabric 연속 통합 설정](service-fabric-set-up-continuous-integration.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13d5b-185">To learn how to automate the publishing process in a continuous integration environment, see [Set up Service Fabric continuous integration](service-fabric-set-up-continuous-integration.md).</span></span>

[0]: ./media/service-fabric-publish-app-remote-cluster/PublishDialog.png
[1]: ./media/service-fabric-publish-app-remote-cluster/SelectCluster.png
[2]: ./media/service-fabric-publish-app-remote-cluster/EditParams.png
[3]: ./media/service-fabric-publish-app-remote-cluster/EditVersions.png
[4]: ./media/service-fabric-publish-app-remote-cluster/publish-to-party-cluster.png
