---
title: "Chef를 사용하여 Azure 가상 컴퓨터 배포 | Microsoft Docs"
description: "Chef를 사용하여 자동화된 가상 컴퓨터 배포 및 Microsoft Azure에서 구성하는 방법을 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: diegoviso
manager: timlt
tags: azure-service-management,azure-resource-manager
editor: 
ms.assetid: 0b82ca70-89ed-496d-bb49-c04ae59b4523
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: diviso
ms.openlocfilehash: b6db0fbb4e0de896994954974ddcc39daad9c125
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="automating-azure-virtual-machine-deployment-with-chef"></a><span data-ttu-id="729c3-103">Chef를 사용하여 Azure 가상 컴퓨터 배포 자동화</span><span class="sxs-lookup"><span data-stu-id="729c3-103">Automating Azure virtual machine deployment with Chef</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="729c3-104">Chef는 자동화 및 필요한 상태 구성을 제공하는 유용한 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-104">Chef is a great tool for delivering automation and desired state configurations.</span></span>

<span data-ttu-id="729c3-105">최신 cloud-api 릴리스에서 Chef는 Azure와의 원활한 통합을 통해 단일 명령으로 구성 상태를 프로비전 및 배포할 수 있는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-105">With our latest cloud-api release, Chef provides seamless integration with Azure, giving you the ability to provision and deploy configuration states through a single command.</span></span>

<span data-ttu-id="729c3-106">이 문서에서는 Chef 환경을 설정하여 Azure 가상 컴퓨터를 프로비전하는 방법을 보여 주고, 정책 또는 “CookBook”을 만든 다음 이 cookbook을 Azure 가상 컴퓨터에 배포하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-106">In this article, I’ll show you how to set up your Chef environment to provision Azure virtual machines and walk you through creating a policy or “CookBook” and then deploying this cookbook to an Azure virtual machine.</span></span>

<span data-ttu-id="729c3-107">시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-107">Let’s begin!</span></span>

## <a name="chef-basics"></a><span data-ttu-id="729c3-108">Chef 기본 사항</span><span class="sxs-lookup"><span data-stu-id="729c3-108">Chef basics</span></span>
<span data-ttu-id="729c3-109">시작하기 전에 Chef의 기본 개념을 검토해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-109">Before you begin, I suggest you review the basic concepts of Chef.</span></span> <span data-ttu-id="729c3-110">훌륭한 자료가 <a href="http://www.chef.io/chef" target="_blank">여기</a> 에 있으니 연습에 앞서 빠르게 읽어 보시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-110">There is great material <a href="http://www.chef.io/chef" target="_blank">here</a> and I recommend you have a quick read before you attempt this walkthrough.</span></span> <span data-ttu-id="729c3-111">하지만 시작하기 전에 기본 사항을 요약해 드릴 것입니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-111">I will however recap the basics before we get started.</span></span>

<span data-ttu-id="729c3-112">다음 다이어그램에 대략적인 Chef 아키텍처가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-112">The following diagram depicts the high-level Chef architecture.</span></span>

![][2]

<span data-ttu-id="729c3-113">Chef에는 Chef 서버, Chef 클라이언트(노드) 및 Chef 워크스테이션 등의 세 가지 주요 아키텍처 구성 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-113">Chef has three main architectural components: Chef Server, Chef Client (node), and Chef Workstation.</span></span>

<span data-ttu-id="729c3-114">Chef Server는 관리 지점이며, 호스트 솔루션과 온-프레미스 솔루션의 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-114">The Chef Server is our management point and there are two options for the Chef Server: a hosted solution or an on-premises solution.</span></span> <span data-ttu-id="729c3-115">여기에서는 호스트 솔루션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-115">We will be using a hosted solution.</span></span>

<span data-ttu-id="729c3-116">Chef Client(노드)는 관리 중인 서버에 있는 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-116">The Chef Client (node) is the agent that sits on the servers you are managing.</span></span>

<span data-ttu-id="729c3-117">Chef Workstation은 정책을 만들고 관리 명령을 실행하는 관리 워크스테이션입니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-117">The Chef Workstation is our admin workstation where we create our policies and execute our management commands.</span></span> <span data-ttu-id="729c3-118">Chef 워크스테이션에서 **knife** 명령을 실행하여 인프라를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-118">We run the **knife** command from the Chef Workstation to manage our infrastructure.</span></span>

<span data-ttu-id="729c3-119">“Cookbook” 및 “Recipe” 개념도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-119">There is also the concept of “Cookbooks” and “Recipes”.</span></span> <span data-ttu-id="729c3-120">이는 우리가 정의하고 서버에 적용하는 효과적인 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-120">These are effectively the policies we define and apply to our servers.</span></span>

## <a name="preparing-the-workstation"></a><span data-ttu-id="729c3-121">워크스테이션 준비</span><span class="sxs-lookup"><span data-stu-id="729c3-121">Preparing the workstation</span></span>
<span data-ttu-id="729c3-122">먼저 워크스테이션을 준비하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-122">First, lets prep the workstation.</span></span> <span data-ttu-id="729c3-123">여기서는 표준 Windows 워크스테이션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-123">I’m using a standard Windows workstation.</span></span> <span data-ttu-id="729c3-124">구성 파일과 cookbook을 저장할 디렉터리를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-124">We need to create a directory to store our config files and cookbooks.</span></span>

<span data-ttu-id="729c3-125">먼저 C:\chef라는 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-125">First create a directory called C:\chef.</span></span>

<span data-ttu-id="729c3-126">그런 다음 c:\chef\cookbooks라는 두 번째 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-126">Then create a second directory called c:\chef\cookbooks.</span></span>

<span data-ttu-id="729c3-127">이제 Chef가 Azure 구독과 통신할 수 있도록 Azure 설정 파일을 다운로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-127">We now need to download our Azure settings file so Chef can communicate with our Azure subscription.</span></span>

<!--Download your publish settings from [here](https://manage.windowsazure.com/publishsettings/).-->
<span data-ttu-id="729c3-128">PowerShell Azure [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) 명령을 사용하여 게시 설정을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-128">Download your publish settings using the PowerShell Azure [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) command.</span></span> 

<span data-ttu-id="729c3-129">게시 설정 파일을 C:\chef에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-129">Save the publish settings file in C:\chef.</span></span>

## <a name="creating-a-managed-chef-account"></a><span data-ttu-id="729c3-130">관리되는 Chef 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="729c3-130">Creating a managed Chef account</span></span>
<span data-ttu-id="729c3-131">[여기](https://manage.chef.io/signup)에 호스트되는 Chef 계정에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-131">Sign up for a hosted Chef account [here](https://manage.chef.io/signup).</span></span>

<span data-ttu-id="729c3-132">등록 프로세스 중에 새 조직을 만들지 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-132">During the signup process, you will be asked to create a new organization.</span></span>

![][3]

<span data-ttu-id="729c3-133">조직을 만든 후 시작 키트를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-133">Once your organization is created, download the starter kit.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="729c3-134">키가 재설정된다는 경고 메시지가 나타나는 경우, 아직 구성된 기존 인프라가 없으므로 계속 진행해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-134">If you receive a prompt warning you that your keys will be reset, it’s ok to proceed as we have no existing infrastructure configured as yet.</span></span>
> 
> 

<span data-ttu-id="729c3-135">이 시작 키트 zip 파일에는 조직 구성 파일 및 키가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-135">This starter kit zip file contains your organization config files and keys.</span></span>

## <a name="configuring-the-chef-workstation"></a><span data-ttu-id="729c3-136">Chef 워크스테이션 구성</span><span class="sxs-lookup"><span data-stu-id="729c3-136">Configuring the Chef workstation</span></span>
<span data-ttu-id="729c3-137">chef-starter.zip 내용을 C:\chef에 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-137">Extract the content of the chef-starter.zip to C:\chef.</span></span>

<span data-ttu-id="729c3-138">chef-starter\chef-repo\.chef의 모든 파일을 c:\chef 디렉터리에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-138">Copy all files under chef-starter\chef-repo\.chef to your c:\chef directory.</span></span>

<span data-ttu-id="729c3-139">이제 디렉터리가 다음 예제와 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-139">Your directory should now look something like the following example.</span></span>

![][5]

<span data-ttu-id="729c3-140">이제 c:\chef 루트에 있는 Azure 게시 파일을 포함하여 네 개의 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-140">You should now have four files including the Azure publishing file in the root of c:\chef.</span></span>

<span data-ttu-id="729c3-141">PEM 파일에는 조직 및 관리자의 통신용 개인 키가 들어 있고, knife.rb 파일에는 knife 구성이 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-141">The PEM files contain your organization and admin private keys for communication while the knife.rb file contains your knife configuration.</span></span> <span data-ttu-id="729c3-142">knife.rb 파일을 편집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-142">We will need to edit the knife.rb file.</span></span>

<span data-ttu-id="729c3-143">원하는 편집기에서 파일을 열고 다음에 보듯이 표시되도록 경로에서 /../를 제거하여 “cookbook_path”를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-143">Open the file in your editor of choice and modify the “cookbook_path” by removing the /../ from the path so it appears as shown next.</span></span>

    cookbook_path  ["#{current_dir}/cookbooks"]

<span data-ttu-id="729c3-144">또한 Azure 게시 설정 파일의 이름을 나타내는 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-144">Also add the following line reflecting the name of your Azure publish settings file.</span></span>

    knife[:azure_publish_settings_file] = "yourfilename.publishsettings"

<span data-ttu-id="729c3-145">이제 knife.rb 파일이 다음 예제와 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-145">Your knife.rb file should now look similar to the following example.</span></span>

![][6]

<span data-ttu-id="729c3-146">이러한 줄은 Knife가 c:\chef\cookbooks 아래의 cookbooks 디렉터리에서 참조되고 Azure 작업 중 Azure 게시 설정 파일을 사용하도록 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-146">These lines will ensure that Knife references the cookbooks directory under c:\chef\cookbooks, and also uses our Azure Publish Settings file during Azure operations.</span></span>

## <a name="installing-the-chef-development-kit"></a><span data-ttu-id="729c3-147">Chef Development Kit 설치</span><span class="sxs-lookup"><span data-stu-id="729c3-147">Installing the Chef Development Kit</span></span>
<span data-ttu-id="729c3-148">이제 ChefDK(Chef Development Kit)를 [다운로드 및 설치](http://downloads.getchef.com/chef-dk/windows) 하여 Chef Workstation을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-148">Next [download and install](http://downloads.getchef.com/chef-dk/windows) the ChefDK (Chef Development Kit) to set up your Chef Workstation.</span></span>

![][7]

<span data-ttu-id="729c3-149">기본 위치인 c:\opscode에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-149">Install in the default location of c:\opscode.</span></span> <span data-ttu-id="729c3-150">설치하는 데 10분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-150">This install will take around 10 minutes.</span></span>

<span data-ttu-id="729c3-151">PATH 변수에 C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin에 대한 항목이 포함되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-151">Confirm your PATH variable contains entries for C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin</span></span>

<span data-ttu-id="729c3-152">그렇지 않으면 이러한 경로를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-152">If they are not there, make sure you add these paths!</span></span>

<span data-ttu-id="729c3-153">*경로 순서가 중요합니다!*</span><span class="sxs-lookup"><span data-stu-id="729c3-153">*NOTE THE ORDER OF THE PATH IS IMPORTANT!*</span></span> <span data-ttu-id="729c3-154">opscode 경로가 올바른 순서가 아니면 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-154">If your opscode paths are not in the correct order you will have issues.</span></span>

<span data-ttu-id="729c3-155">계속하기 전에 워크스테이션을 다시 부팅하세요.</span><span class="sxs-lookup"><span data-stu-id="729c3-155">Reboot your workstation before you continue.</span></span>

<span data-ttu-id="729c3-156">이제 Knife Azure 확장을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-156">Next, we will install the Knife Azure extension.</span></span> <span data-ttu-id="729c3-157">이는 “Azure 플러그 인”이 포함된 Knife를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-157">This provides Knife with the “Azure Plugin”.</span></span>

<span data-ttu-id="729c3-158">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-158">Run the following command.</span></span>

    chef gem install knife-azure ––pre

> [!NOTE]
> <span data-ttu-id="729c3-159">–pre 인수는 최신 API 집합에 대한 액세스를 제공하는 최신 RC 버전의 knife azure 플러그인을 받을 수 있도록 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-159">The –pre argument ensures you are receiving the latest RC version of the Knife Azure Plugin which provides access to the latest set of APIs.</span></span>
> 
> 

<span data-ttu-id="729c3-160">이와 동시에 여러 종속성도 설치될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-160">It’s likely that a number of dependencies will also be installed at the same time.</span></span>

![][8]

<span data-ttu-id="729c3-161">모든 것이 올바르게 구성되었는지 확인하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-161">To ensure everything is configured correctly, run the following command.</span></span>

    knife azure image list

<span data-ttu-id="729c3-162">모든 것이 올바르게 구성되었으면 사용 가능한 Azure 이미지 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-162">If everything is configured correctly, you will see a list of available Azure images scroll through.</span></span>

<span data-ttu-id="729c3-163">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-163">Congratulations.</span></span> <span data-ttu-id="729c3-164">워크스테이션이 설정되었습니다!</span><span class="sxs-lookup"><span data-stu-id="729c3-164">The workstation is set up!</span></span>

## <a name="creating-a-cookbook"></a><span data-ttu-id="729c3-165">Cookbook 만들기</span><span class="sxs-lookup"><span data-stu-id="729c3-165">Creating a Cookbook</span></span>
<span data-ttu-id="729c3-166">Cookbook은 Chef에서 관리되는 클라이언트를 실행할 명령 집합을 정의하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-166">A Cookbook is used by Chef to define a set of commands that you wish to execute on your managed client.</span></span> <span data-ttu-id="729c3-167">Cookbook 만들기는 간단하며, **chef generate cookbook** 명령을 사용하여 Cookbook 템플릿을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-167">Creating a Cookbook is straightforward and we use the **chef generate cookbook** command to generate our Cookbook template.</span></span> <span data-ttu-id="729c3-168">저는 IIS를 자동으로 배포하는 정책을 좋아하므로 저의 Cookbook 웹 서버를 호출해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-168">I will be calling my Cookbook web server as I would like a policy that automatically deploys IIS.</span></span>

<span data-ttu-id="729c3-169">C:\Chef 디렉터리에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-169">Under your C:\Chef directory run the following command.</span></span>

    chef generate cookbook webserver

<span data-ttu-id="729c3-170">C:\Chef\cookbooks\webserver 디렉터리 아래에 파일 집합이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-170">This will generate a set of files under the directory C:\Chef\cookbooks\webserver.</span></span> <span data-ttu-id="729c3-171">이제 관리되는 가상 컴퓨터에서 Chef 클라이언트를 실행할 명령 집합을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-171">We now need to define the set of commands we would like our Chef client to execute on our managed virtual machine.</span></span>

<span data-ttu-id="729c3-172">명령은 default.rb 파일에 저장되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-172">The commands are stored in the file default.rb.</span></span> <span data-ttu-id="729c3-173">이 파일에서 IIS를 설치하고, IIS를 시작하며, 템플릿 파일을 wwwroot 폴더에 복사하는 명령 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-173">In this file, I’ll be defining a set of commands that installs IIS, starts IIS and copies a template file to the wwwroot folder.</span></span>

<span data-ttu-id="729c3-174">C:\chef\cookbooks\webserver\recipes\default.rb를 수정하고 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-174">Modify the C:\chef\cookbooks\webserver\recipes\default.rb file and add the following lines.</span></span>

    powershell_script 'Install IIS' do
         action :run
         code 'add-windowsfeature Web-Server'
    end

    service 'w3svc' do
         action [ :enable, :start ]
    end

    template 'c:\inetpub\wwwroot\Default.htm' do
         source 'Default.htm.erb'
         rights :read, 'Everyone'
    end

<span data-ttu-id="729c3-175">작업이 완료되면 파일을 한 번 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-175">Save the file once you are done.</span></span>

## <a name="creating-a-template"></a><span data-ttu-id="729c3-176">템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="729c3-176">Creating a template</span></span>
<span data-ttu-id="729c3-177">앞서 설명한 바와 같이, default.html 페이지로 사용할 템플릿 파일을 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-177">As we mentioned previously, we need to generate a template file which will be used as our default.html page.</span></span>

<span data-ttu-id="729c3-178">다음 명령을 실행하여 템플릿을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-178">Run the following command to generate the template.</span></span>

    chef generate template webserver Default.htm

<span data-ttu-id="729c3-179">이제 C:\chef\cookbooks\webserver\templates\default\Default.htm.erb 파일로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-179">Now navigate to the C:\chef\cookbooks\webserver\templates\default\Default.htm.erb file.</span></span> <span data-ttu-id="729c3-180">간단한 “Hello World” HTML 코드를 추가하여 파일을 편집하고 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-180">Edit the file by adding some simple “Hello World” HTML code, and then save the file.</span></span>

## <a name="upload-the-cookbook-to-the-chef-server"></a><span data-ttu-id="729c3-181">Chef Server에 Cookbook 업로드</span><span class="sxs-lookup"><span data-stu-id="729c3-181">Upload the Cookbook to the Chef Server</span></span>
<span data-ttu-id="729c3-182">이 단계에서는 로컬 컴퓨터에서 만든 Cookbook을 복사하여 Chef Hosted Server에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-182">In this step, we are taking a copy of the Cookbook that we have created on our local machine and uploading it to the Chef Hosted Server.</span></span> <span data-ttu-id="729c3-183">업로드가 완료되면 **정책** 탭에 Cookbook이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-183">Once uploaded, the Cookbook will appear under the **Policy** tab.</span></span>

    knife cookbook upload webserver

![][9]

## <a name="deploy-a-virtual-machine-with-knife-azure"></a><span data-ttu-id="729c3-184">Knife Azure를 사용하여 가상 컴퓨터 배포</span><span class="sxs-lookup"><span data-stu-id="729c3-184">Deploy a virtual machine with Knife Azure</span></span>
<span data-ttu-id="729c3-185">이제 Azure 가상 컴퓨터를 배포하고 IIS 웹 서비스 및 기본 웹 페이지를 설치할 “Webserver” Cookbook을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-185">We will now deploy an Azure virtual machine and apply the “Webserver” Cookbook which will install our IIS web service and default web page.</span></span>

<span data-ttu-id="729c3-186">이 작업을 수행하려면 **knife azure server create** 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-186">In order to do this, use the **knife azure server create** command.</span></span>

<span data-ttu-id="729c3-187">명령의 예가 다음에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-187">Am example of the command appears next.</span></span>

    knife azure server create --azure-dns-name 'diegotest01' --azure-vm-name 'testserver01' --azure-vm-size 'Small' --azure-storage-account 'portalvhdsxxxx' --bootstrap-protocol 'cloud-api' --azure-source-image 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201411.01-en.us-127GB.vhd' --azure-service-location 'Southeast Asia' --winrm-user azureuser --winrm-password 'myPassword123' --tcp-endpoints 80,3389 --r 'recipe[webserver]'

<span data-ttu-id="729c3-188">매개 변수는 설명이 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-188">The parameters are self-explanatory.</span></span> <span data-ttu-id="729c3-189">특정 변수를 대체하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-189">Substitute your particular variables and run.</span></span>

> [!NOTE]
> <span data-ttu-id="729c3-190">명령줄에서 –tcp-endpoints 매개변수를 사용하여 끝점 네트워크 필터 규칙을 자동화해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-190">Through the the command line, I’m also automating my endpoint network filter rules by using the –tcp-endpoints parameter.</span></span> <span data-ttu-id="729c3-191">포트 80 및 3389를 열어 내 웹 페이지 및 RDP 세션에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-191">I’ve opened up ports 80 and 3389 to provide access to my web page and RDP session.</span></span>
> 
> 

<span data-ttu-id="729c3-192">명령을 실행하고 나면 Azure 포털로 이동하며 프로비전을 시작할 컴퓨터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-192">Once you run the command, go to the Azure portal and you will see your machine begin to provision.</span></span>

![][13]

<span data-ttu-id="729c3-193">명령 프롬프트가 다음에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-193">The command prompt appears next.</span></span>

![][10]

<span data-ttu-id="729c3-194">배포가 완료되면 포트 80을 통해 웹 서비스에 연결할 수 있어야 합니다. knife azure 명령으로 가상 컴퓨터를 프로비전할 때 이 포트를 이미 열었기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-194">Once the deployment is complete, we should be able to connect to the web service over port 80 as we had opened the port when we provisioned the virtual machine with the Knife Azure command.</span></span> <span data-ttu-id="729c3-195">이 가상 컴퓨터는 클라우드 서비스에 있는 유일한 가상 컴퓨터이므로 클라우드 서비스 url과 연결해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-195">As this virtual machine is the only virtual machine in my cloud service, I’ll connect it with the cloud service url.</span></span>

![][11]

<span data-ttu-id="729c3-196">보시는 바와 같이 HTML 코드를 독창적으로 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-196">As you can see, I got creative with my HTML code.</span></span>

<span data-ttu-id="729c3-197">포트 3389에서도 Azure Portal에서 RDP 세션을 통해 연결할 수 있다는 점을 기억하세요.</span><span class="sxs-lookup"><span data-stu-id="729c3-197">Don’t forget we can also connect through an RDP session from the Azure portal via port 3389.</span></span>

<span data-ttu-id="729c3-198">유익한 정보가 되셨기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="729c3-198">I hope this has been helpful!</span></span> <span data-ttu-id="729c3-199">이제 Azure의 Infrastructure as Code 과정을 시작해 보세요.</span><span class="sxs-lookup"><span data-stu-id="729c3-199">Go  and start your infrastructure as code journey with Azure today!</span></span>

<!--Image references-->
[2]: media/chef-automation/2.png
[3]: media/chef-automation/3.png
[4]: media/chef-automation/4.png
[5]: media/chef-automation/5.png
[6]: media/chef-automation/6.png
[7]: media/chef-automation/7.png
[8]: media/chef-automation/8.png
[9]: media/chef-automation/9.png
[10]: media/chef-automation/10.png
[11]: media/chef-automation/11.png
[13]: media/chef-automation/13.png


<!--Link references-->
