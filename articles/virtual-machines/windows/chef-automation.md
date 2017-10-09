---
title: "Chef와 가상 컴퓨터 배포 aaaAzure | Microsoft Docs"
description: "가상 컴퓨터 배포 및 구성 Microsoft Azure에서 Chef toodo toouse 자동화 하는 방법을 알아봅니다"
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
ms.openlocfilehash: c5ea98c673b2ee75dd4cedf27e50330af05230d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automating-azure-virtual-machine-deployment-with-chef"></a><span data-ttu-id="82dbb-103">Chef를 사용하여 Azure 가상 컴퓨터 배포 자동화</span><span class="sxs-lookup"><span data-stu-id="82dbb-103">Automating Azure virtual machine deployment with Chef</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="82dbb-104">Chef는 자동화 및 필요한 상태 구성을 제공하는 유용한 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-104">Chef is a great tool for delivering automation and desired state configurations.</span></span>

<span data-ttu-id="82dbb-105">최신 클라우드 api 릴리스 Azure과의 원활한 통합을 제공 하는 Chef, 기능 tooprovision hello 수 있도록 하며 단일 명령을 통해 구성 상태를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-105">With our latest cloud-api release, Chef provides seamless integration with Azure, giving you hello ability tooprovision and deploy configuration states through a single command.</span></span>

<span data-ttu-id="82dbb-106">이 문서에서는 알려드리겠습니다 방법을 tooset Chef 환경 tooprovision Azure 가상를 설치 하 고 정책 또는 "도움말"을 만들고이 cookbook tooan Azure 가상 컴퓨터를 배포 하는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-106">In this article, I’ll show you how tooset up your Chef environment tooprovision Azure virtual machines and walk you through creating a policy or “CookBook” and then deploying this cookbook tooan Azure virtual machine.</span></span>

<span data-ttu-id="82dbb-107">시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-107">Let’s begin!</span></span>

## <a name="chef-basics"></a><span data-ttu-id="82dbb-108">Chef 기본 사항</span><span class="sxs-lookup"><span data-stu-id="82dbb-108">Chef basics</span></span>
<span data-ttu-id="82dbb-109">시작 하기 전에 것이 좋습니다 hello Chef의 기본 개념을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-109">Before you begin, I suggest you review hello basic concepts of Chef.</span></span> <span data-ttu-id="82dbb-110">훌륭한 자료가 <a href="http://www.chef.io/chef" target="_blank">여기</a> 에 있으니 연습에 앞서 빠르게 읽어 보시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-110">There is great material <a href="http://www.chef.io/chef" target="_blank">here</a> and I recommend you have a quick read before you attempt this walkthrough.</span></span> <span data-ttu-id="82dbb-111">그러나 시작 하기 전에 hello 기본 사항을 요약해 보겠습니다는 I.</span><span class="sxs-lookup"><span data-stu-id="82dbb-111">I will however recap hello basics before we get started.</span></span>

<span data-ttu-id="82dbb-112">다음 다이어그램 hello hello 개략적인 Chef 아키텍처를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-112">hello following diagram depicts hello high-level Chef architecture.</span></span>

![][2]

<span data-ttu-id="82dbb-113">Chef에는 Chef 서버, Chef 클라이언트(노드) 및 Chef 워크스테이션 등의 세 가지 주요 아키텍처 구성 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-113">Chef has three main architectural components: Chef Server, Chef Client (node), and Chef Workstation.</span></span>

<span data-ttu-id="82dbb-114">hello Chef 서버는이 관리 지점 및 Chef 서버 hello에 대 한 두 가지가 있습니다: 호스팅된 솔루션이 나 온-프레미스 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-114">hello Chef Server is our management point and there are two options for hello Chef Server: a hosted solution or an on-premises solution.</span></span> <span data-ttu-id="82dbb-115">여기에서는 호스트 솔루션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-115">We will be using a hosted solution.</span></span>

<span data-ttu-id="82dbb-116">hello Chef 클라이언트 (노드)는 관리 하는 hello 서버에 있는 hello 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-116">hello Chef Client (node) is hello agent that sits on hello servers you are managing.</span></span>

<span data-ttu-id="82dbb-117">hello Chef 워크스테이션은 우리의 관리자 워크스테이션 우리의 정책을 만들 म 및 우리의 관리 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-117">hello Chef Workstation is our admin workstation where we create our policies and execute our management commands.</span></span> <span data-ttu-id="82dbb-118">Hello 실행 **knife** 인프라에서 Chef 워크스테이션 toomanage hello 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-118">We run hello **knife** command from hello Chef Workstation toomanage our infrastructure.</span></span>

<span data-ttu-id="82dbb-119">"Cookbook" 및 "레시피" hello 개념 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-119">There is also hello concept of “Cookbooks” and “Recipes”.</span></span> <span data-ttu-id="82dbb-120">이들은 효율적으로 정의 하 고 적용 tooour 서버 hello 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-120">These are effectively hello policies we define and apply tooour servers.</span></span>

## <a name="preparing-hello-workstation"></a><span data-ttu-id="82dbb-121">Hello 워크스테이션 준비</span><span class="sxs-lookup"><span data-stu-id="82dbb-121">Preparing hello workstation</span></span>
<span data-ttu-id="82dbb-122">첫째, 준비 hello 워크스테이션을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-122">First, lets prep hello workstation.</span></span> <span data-ttu-id="82dbb-123">여기서는 표준 Windows 워크스테이션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-123">I’m using a standard Windows workstation.</span></span> <span data-ttu-id="82dbb-124">이러한 구성 파일과 cookbook toocreate 디렉터리 toostore 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-124">We need toocreate a directory toostore our config files and cookbooks.</span></span>

<span data-ttu-id="82dbb-125">먼저 C:\chef라는 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-125">First create a directory called C:\chef.</span></span>

<span data-ttu-id="82dbb-126">그런 다음 c:\chef\cookbooks라는 두 번째 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-126">Then create a second directory called c:\chef\cookbooks.</span></span>

<span data-ttu-id="82dbb-127">이제 필요 toodownload 쿼리하여 Azure 설정 파일 Chef 구독을 사용 하 여 통신할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-127">We now need toodownload our Azure settings file so Chef can communicate with our Azure subscription.</span></span>

<!--Download your publish settings from [here](https://manage.windowsazure.com/publishsettings/).-->
<span data-ttu-id="82dbb-128">다운로드 프로그램 hello Azure PowerShell을 사용 하 여 설정을 게시 [Get-azurepublishsettingsfile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-128">Download your publish settings using hello PowerShell Azure [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) command.</span></span> 

<span data-ttu-id="82dbb-129">Hello 저장 C:\chef에서 게시 설정 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-129">Save hello publish settings file in C:\chef.</span></span>

## <a name="creating-a-managed-chef-account"></a><span data-ttu-id="82dbb-130">관리되는 Chef 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="82dbb-130">Creating a managed Chef account</span></span>
<span data-ttu-id="82dbb-131">[여기](https://manage.chef.io/signup)에 호스트되는 Chef 계정에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-131">Sign up for a hosted Chef account [here](https://manage.chef.io/signup).</span></span>

<span data-ttu-id="82dbb-132">Hello 등록 프로세스 동안 됩니다 toocreate 새 조직을 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-132">During hello signup process, you will be asked toocreate a new organization.</span></span>

![][3]

<span data-ttu-id="82dbb-133">조직 만들어지면 hello 시작 키트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-133">Once your organization is created, download hello starter kit.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="82dbb-134">키 재설정 될 것 이라는 것을 경고 하는 메시지가 표시 되 면 아직 구성 된 기존 인프라가 없는 있으므로 확인 tooproceed 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-134">If you receive a prompt warning you that your keys will be reset, it’s ok tooproceed as we have no existing infrastructure configured as yet.</span></span>
> 
> 

<span data-ttu-id="82dbb-135">이 시작 키트 zip 파일에는 조직 구성 파일 및 키가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-135">This starter kit zip file contains your organization config files and keys.</span></span>

## <a name="configuring-hello-chef-workstation"></a><span data-ttu-id="82dbb-136">Hello Chef 워크스테이션 구성</span><span class="sxs-lookup"><span data-stu-id="82dbb-136">Configuring hello Chef workstation</span></span>
<span data-ttu-id="82dbb-137">Hello chef starter.zip tooC:\chef의 hello 콘텐츠를 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-137">Extract hello content of hello chef-starter.zip tooC:\chef.</span></span>

<span data-ttu-id="82dbb-138">Chef starter\chef repo 아래에 있는 모든 파일을 복사\.chef tooyour c:\chef 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-138">Copy all files under chef-starter\chef-repo\.chef tooyour c:\chef directory.</span></span>

<span data-ttu-id="82dbb-139">디렉터리는 이제 비슷합니다 다음 예제는 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-139">Your directory should now look something like hello following example.</span></span>

![][5]

<span data-ttu-id="82dbb-140">Hello Azure 게시 파일을 포함 하 여 c:\chef의 hello 루트에서 4 개의 파일을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-140">You should now have four files including hello Azure publishing file in hello root of c:\chef.</span></span>

<span data-ttu-id="82dbb-141">hello PEM 파일 hello knife.rb 파일 knife 구성을 포함 하는 동안 사용자의 조직 및 관리자 통신에 대 한 개인 키를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-141">hello PEM files contain your organization and admin private keys for communication while hello knife.rb file contains your knife configuration.</span></span> <span data-ttu-id="82dbb-142">Tooedit hello knife.rb 파일이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-142">We will need tooedit hello knife.rb file.</span></span>

<span data-ttu-id="82dbb-143">Hello 파일에서 원하는 편집기를 열고 cookbook_path"hello" hello를 제거 하 여 수정 /... / hello 경로 같이 다음에 표시 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-143">Open hello file in your editor of choice and modify hello “cookbook_path” by removing hello /../ from hello path so it appears as shown next.</span></span>

    cookbook_path  ["#{current_dir}/cookbooks"]

<span data-ttu-id="82dbb-144">추가적으로 hello 다음 줄에서는 Azure의 반사 hello 이름 게시 설정 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-144">Also add hello following line reflecting hello name of your Azure publish settings file.</span></span>

    knife[:azure_publish_settings_file] = "yourfilename.publishsettings"

<span data-ttu-id="82dbb-145">이제 knife.rb 파일에 다음 예제와 비슷한 toohello 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-145">Your knife.rb file should now look similar toohello following example.</span></span>

![][6]

<span data-ttu-id="82dbb-146">이 줄은 Knife hello cookbook 디렉터리 c:\chef\cookbooks, 아래에서 참조 하 고 또한 쿼리하여 Azure 게시 설정 파일을 사용 하 여 Azure 작업 중에 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-146">These lines will ensure that Knife references hello cookbooks directory under c:\chef\cookbooks, and also uses our Azure Publish Settings file during Azure operations.</span></span>

## <a name="installing-hello-chef-development-kit"></a><span data-ttu-id="82dbb-147">Hello Chef 개발 키트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-147">Installing hello Chef Development Kit</span></span>
<span data-ttu-id="82dbb-148">다음 [다운로드 및 설치](http://downloads.getchef.com/chef-dk/windows) Chef 워크스테이션을 ChefDK (Chef Development Kit) tooset hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-148">Next [download and install](http://downloads.getchef.com/chef-dk/windows) hello ChefDK (Chef Development Kit) tooset up your Chef Workstation.</span></span>

![][7]

<span data-ttu-id="82dbb-149">C:\opscode hello 기본 위치에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-149">Install in hello default location of c:\opscode.</span></span> <span data-ttu-id="82dbb-150">설치하는 데 10분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-150">This install will take around 10 minutes.</span></span>

<span data-ttu-id="82dbb-151">PATH 변수에 C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin에 대한 항목이 포함되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-151">Confirm your PATH variable contains entries for C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin</span></span>

<span data-ttu-id="82dbb-152">그렇지 않으면 이러한 경로를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-152">If they are not there, make sure you add these paths!</span></span>

<span data-ttu-id="82dbb-153">*참고 hello 순서의 hello 경로 중요!*</span><span class="sxs-lookup"><span data-stu-id="82dbb-153">*NOTE hello ORDER OF hello PATH IS IMPORTANT!*</span></span> <span data-ttu-id="82dbb-154">Opscode 경로 hello 올바른 순서에 없는 경우에 문제를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-154">If your opscode paths are not in hello correct order you will have issues.</span></span>

<span data-ttu-id="82dbb-155">계속하기 전에 워크스테이션을 다시 부팅하세요.</span><span class="sxs-lookup"><span data-stu-id="82dbb-155">Reboot your workstation before you continue.</span></span>

<span data-ttu-id="82dbb-156">다음으로 hello Knife Azure 확장을 설치 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-156">Next, we will install hello Knife Azure extension.</span></span> <span data-ttu-id="82dbb-157">"Azure 플러그 인" Knife hello로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-157">This provides Knife with hello “Azure Plugin”.</span></span>

<span data-ttu-id="82dbb-158">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-158">Run hello following command.</span></span>

    chef gem install knife-azure ––pre

> [!NOTE]
> <span data-ttu-id="82dbb-159">hello – pre 인수 hello 최신 RC 버전의 hello 액세스 toohello 최신 Api 집합을 제공 하는 Knife Azure 플러그 인을 받는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-159">hello –pre argument ensures you are receiving hello latest RC version of hello Knife Azure Plugin which provides access toohello latest set of APIs.</span></span>
> 
> 

<span data-ttu-id="82dbb-160">한 많은 종속성도 hello에 설치 될 가능성이 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-160">It’s likely that a number of dependencies will also be installed at hello same time.</span></span>

![][8]

<span data-ttu-id="82dbb-161">tooensure 모든 항목은 다음 명령이 실행된 hello 올바르게 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-161">tooensure everything is configured correctly, run hello following command.</span></span>

    knife azure image list

<span data-ttu-id="82dbb-162">모든 것이 올바르게 구성되었으면 사용 가능한 Azure 이미지 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-162">If everything is configured correctly, you will see a list of available Azure images scroll through.</span></span>

<span data-ttu-id="82dbb-163">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-163">Congratulations.</span></span> <span data-ttu-id="82dbb-164">hello 워크스테이션 설정 되었습니다!</span><span class="sxs-lookup"><span data-stu-id="82dbb-164">hello workstation is set up!</span></span>

## <a name="creating-a-cookbook"></a><span data-ttu-id="82dbb-165">Cookbook 만들기</span><span class="sxs-lookup"><span data-stu-id="82dbb-165">Creating a Cookbook</span></span>
<span data-ttu-id="82dbb-166">Cookbook Chef toodefine에서 사용 하는 관리 되는 클라이언트에서 tooexecute 한다고 명령 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-166">A Cookbook is used by Chef toodefine a set of commands that you wish tooexecute on your managed client.</span></span> <span data-ttu-id="82dbb-167">Cookbook을 만드는 것은 간단 하 고 사용 하 여 hello **cookbook을 생성 하는 chef** toogenerate 우리의 Cookbook 서식 파일을 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-167">Creating a Cookbook is straightforward and we use hello **chef generate cookbook** command toogenerate our Cookbook template.</span></span> <span data-ttu-id="82dbb-168">저는 IIS를 자동으로 배포하는 정책을 좋아하므로 저의 Cookbook 웹 서버를 호출해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-168">I will be calling my Cookbook web server as I would like a policy that automatically deploys IIS.</span></span>

<span data-ttu-id="82dbb-169">C:\Chef 디렉터리 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-169">Under your C:\Chef directory run hello following command.</span></span>

    chef generate cookbook webserver

<span data-ttu-id="82dbb-170">이 hello 디렉터리 C:\Chef\cookbooks\webserver 파일 집합이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-170">This will generate a set of files under hello directory C:\Chef\cookbooks\webserver.</span></span> <span data-ttu-id="82dbb-171">이제 우리 Chef 클라이언트 tooexecute 관리 되는 가상 컴퓨터에 같은 명령의 toodefine hello 집합이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-171">We now need toodefine hello set of commands we would like our Chef client tooexecute on our managed virtual machine.</span></span>

<span data-ttu-id="82dbb-172">hello 명령은 hello 파일 default.rb에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-172">hello commands are stored in hello file default.rb.</span></span> <span data-ttu-id="82dbb-173">이 파일에 I 합니다 정의할 명령 집합을 시작 하 여 IIS를 설치, IIS 템플릿 파일 toohello wwwroot 폴더를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-173">In this file, I’ll be defining a set of commands that installs IIS, starts IIS and copies a template file toohello wwwroot folder.</span></span>

<span data-ttu-id="82dbb-174">Hello C:\chef\cookbooks\webserver\recipes\default.rb 파일을 수정 하 고 hello 다음 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-174">Modify hello C:\chef\cookbooks\webserver\recipes\default.rb file and add hello following lines.</span></span>

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

<span data-ttu-id="82dbb-175">완료 되 면 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-175">Save hello file once you are done.</span></span>

## <a name="creating-a-template"></a><span data-ttu-id="82dbb-176">템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="82dbb-176">Creating a template</span></span>
<span data-ttu-id="82dbb-177">이전에 설명한 것 처럼 toogenerate 가격 default.html 페이지도 사용 되는 템플릿 파일 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-177">As we mentioned previously, we need toogenerate a template file which will be used as our default.html page.</span></span>

<span data-ttu-id="82dbb-178">다음 명령 toogenerate hello 템플릿이 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-178">Run hello following command toogenerate hello template.</span></span>

    chef generate template webserver Default.htm

<span data-ttu-id="82dbb-179">이제 toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb 파일을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-179">Now navigate toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb file.</span></span> <span data-ttu-id="82dbb-180">몇 가지 간단한 "Hello World" HTML 코드를 추가 하 여 hello 파일을 편집 하 고 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-180">Edit hello file by adding some simple “Hello World” HTML code, and then save hello file.</span></span>

## <a name="upload-hello-cookbook-toohello-chef-server"></a><span data-ttu-id="82dbb-181">Chef 서버 hello Cookbook toohello 업로드</span><span class="sxs-lookup"><span data-stu-id="82dbb-181">Upload hello Cookbook toohello Chef Server</span></span>
<span data-ttu-id="82dbb-182">이 단계에서는 로컬 컴퓨터에 만든 Cookbook hello의 복사본을 사용 하 고 toohello Chef 호스팅 서버를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-182">In this step, we are taking a copy of hello Cookbook that we have created on our local machine and uploading it toohello Chef Hosted Server.</span></span> <span data-ttu-id="82dbb-183">Hello Cookbook hello 아래에 표시 됩니다, 업로드 한 후 **정책** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-183">Once uploaded, hello Cookbook will appear under hello **Policy** tab.</span></span>

    knife cookbook upload webserver

![][9]

## <a name="deploy-a-virtual-machine-with-knife-azure"></a><span data-ttu-id="82dbb-184">Knife Azure를 사용하여 가상 컴퓨터 배포</span><span class="sxs-lookup"><span data-stu-id="82dbb-184">Deploy a virtual machine with Knife Azure</span></span>
<span data-ttu-id="82dbb-185">이제 Azure 가상 컴퓨터를 배포 하 고 hello 품질 IIS 웹 서비스와 기본 웹 페이지를 설치 하는 "웹 서버" Cookbook을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-185">We will now deploy an Azure virtual machine and apply hello “Webserver” Cookbook which will install our IIS web service and default web page.</span></span>

<span data-ttu-id="82dbb-186">이 toodo 주문 하 hello를 사용 하 여 **knife azure 서버 만들기** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-186">In order toodo this, use hello **knife azure server create** command.</span></span>

<span data-ttu-id="82dbb-187">독자 hello 명령의 한 예로 다음 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-187">Am example of hello command appears next.</span></span>

    knife azure server create --azure-dns-name 'diegotest01' --azure-vm-name 'testserver01' --azure-vm-size 'Small' --azure-storage-account 'portalvhdsxxxx' --bootstrap-protocol 'cloud-api' --azure-source-image 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201411.01-en.us-127GB.vhd' --azure-service-location 'Southeast Asia' --winrm-user azureuser --winrm-password 'myPassword123' --tcp-endpoints 80,3389 --r 'recipe[webserver]'

<span data-ttu-id="82dbb-188">hello 매개 변수는 자체 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-188">hello parameters are self-explanatory.</span></span> <span data-ttu-id="82dbb-189">특정 변수를 대체하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-189">Substitute your particular variables and run.</span></span>

> [!NOTE]
> <span data-ttu-id="82dbb-190">Hello hello 명령줄을 통해 hello – tcp 끝점 매개 변수를 사용 하 여 끝점 네트워크 필터 규칙을 자동화 I.</span><span class="sxs-lookup"><span data-stu-id="82dbb-190">Through hello hello command line, I’m also automating my endpoint network filter rules by using hello –tcp-endpoints parameter.</span></span> <span data-ttu-id="82dbb-191">포트 80 및 3389 tooprovide 액세스 toomy 웹 페이지 및 RDP 세션을 연 했습니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-191">I’ve opened up ports 80 and 3389 tooprovide access toomy web page and RDP session.</span></span>
> 
> 

<span data-ttu-id="82dbb-192">Hello 명령을 실행 하면 되 면 이동 toohello Azure 포털을 시작 tooprovision 컴퓨터에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-192">Once you run hello command, go toohello Azure portal and you will see your machine begin tooprovision.</span></span>

![][13]

<span data-ttu-id="82dbb-193">다음 hello 명령 프롬프트가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-193">hello command prompt appears next.</span></span>

![][10]

<span data-ttu-id="82dbb-194">Hello 배포 완료 되 면 우리 있어야 수 tooconnect toohello 웹 서비스 포트 80 통해 म म hello hello Knife Azure 명령 사용 하는 가상 컴퓨터를 프로비저닝할 때 hello 포트 연 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-194">Once hello deployment is complete, we should be able tooconnect toohello web service over port 80 as we had opened hello port when we provisioned hello virtual machine with hello Knife Azure command.</span></span> <span data-ttu-id="82dbb-195">이 가상 컴퓨터 클라우드 서비스 내에 가상 컴퓨터 hello 그대로 hello 클라우드 서비스 url과 연결 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-195">As this virtual machine is hello only virtual machine in my cloud service, I’ll connect it with hello cloud service url.</span></span>

![][11]

<span data-ttu-id="82dbb-196">보시는 바와 같이 HTML 코드를 독창적으로 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-196">As you can see, I got creative with my HTML code.</span></span>

<span data-ttu-id="82dbb-197">반드시 hello 포트 3389 통해 Azure 포털에서에서 RDP 세션을 통해 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-197">Don’t forget we can also connect through an RDP session from hello Azure portal via port 3389.</span></span>

<span data-ttu-id="82dbb-198">유익한 정보가 되셨기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="82dbb-198">I hope this has been helpful!</span></span> <span data-ttu-id="82dbb-199">이제 Azure의 Infrastructure as Code 과정을 시작해 보세요.</span><span class="sxs-lookup"><span data-stu-id="82dbb-199">Go  and start your infrastructure as code journey with Azure today!</span></span>

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
