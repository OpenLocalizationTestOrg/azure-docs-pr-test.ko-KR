---
title: "aaaDeploy Node.js 응용 프로그램 tooLinux Azure의 가상 컴퓨터"
description: "자세한 방법을 toodeploy는 Node.js 응용 프로그램이 Azure에서 가상 컴퓨터를 tooLinux 합니다."
services: 
documentationcenter: nodejs
author: stepro
manager: dmitryr
editor: 
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: /azure
ms.assetid: 857a812d-c73e-4af7-a985-2d0baf8b6f71
ms.service: multiple
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2016
ms.author: stephpr
ms.openlocfilehash: e876c8170a06f102f7f32ec7cb930b876647a707
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-nodejs-application-toolinux-virtual-machines-in-azure"></a><span data-ttu-id="0c334-103">Node.js 응용 프로그램 tooLinux Azure의 가상 컴퓨터 배포</span><span class="sxs-lookup"><span data-stu-id="0c334-103">Deploy a Node.js application tooLinux Virtual Machines in Azure</span></span>
<span data-ttu-id="0c334-104">이 자습서에서는 어떻게 tootake Node.js 응용 프로그램을 Azure에서 실행 중인 tooLinux 가상 컴퓨터에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-104">This tutorial shows how tootake a Node.js application and deploy it tooLinux virtual machines running in Azure.</span></span> <span data-ttu-id="0c334-105">이 자습서의 지침에 hello Node.js를 실행할 수 있는 모든 운영 체제에서 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-105">hello instructions in this tutorial can be followed on any operating system that is capable of running Node.js.</span></span>

<span data-ttu-id="0c334-106">이 문서에서 배울 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-106">You'll learn how to:</span></span>

* <span data-ttu-id="0c334-107">간단한 TODO 응용 프로그램을 포함하는 GitHub 리포지토리 분기 및 복제.</span><span class="sxs-lookup"><span data-stu-id="0c334-107">Fork and clone a GitHub repository containing a simple TODO application;</span></span>
* <span data-ttu-id="0c334-108">만들기 및 Azure toorun hello 응용 프로그램의 두 Linux 가상 컴퓨터 구성</span><span class="sxs-lookup"><span data-stu-id="0c334-108">Create and configure two Linux virtual machines in Azure toorun hello application;</span></span>
* <span data-ttu-id="0c334-109">업데이트 toohello 웹 프런트 엔드 가상 컴퓨터에 푸시하여 hello 응용 프로그램을 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-109">Iterate on hello application by pushing updates toohello web frontend virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="0c334-110">toocomplete이이 자습서에서는 hello는 개발 컴퓨터에서 기능 toouse Git 및 GitHub 계정 및 Microsoft Azure 계정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-110">toocomplete this tutorial, you need a GitHub account and a Microsoft Azure account, and hello ability toouse Git from a development machine.</span></span>
> 
> <span data-ttu-id="0c334-111">현재 GitHub 계정이 없는 경우 [여기서](https://github.com/join)등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-111">If you don't have a GitHub account, you can sign up [here](https://github.com/join).</span></span>
> 
> <span data-ttu-id="0c334-112">[Microsoft Azure](https://azure.microsoft.com/) 계정이 없으면 [여기서](https://azure.microsoft.com/pricing/free-trial/) 무료 평가판에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-112">If you don't have a [Microsoft Azure](https://azure.microsoft.com/) account, you can sign up for a FREE trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="0c334-113">이 또한 단계별로 안내 합니다 hello 등록에 대 한 프로세스는 [Microsoft 계정](http://account.microsoft.com) 하면 아직 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="0c334-113">This will also lead you through hello sign up process for a [Microsoft Account](http://account.microsoft.com) if you do not already have one.</span></span> <span data-ttu-id="0c334-114">또는 Visual Studio 구독자인 경우 [MSDN 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-114">Alternatively, if you are a Visual Studio subscriber, you can [activate your MSDN benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="0c334-115">개발 컴퓨터에 Git가 없으며 Macintosh 또는 Windows 컴퓨터를 사용하는 경우 Git를 [여기](http://www.git-scm.com)에서 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-115">If you do not have git on your development machine, then if you are using a Macintosh or Windows machine, install git from [here](http://www.git-scm.com).</span></span> <span data-ttu-id="0c334-116">Linux를 사용 하는 경우 설치와 같은,에 가장 적합 한 hello 메커니즘을 사용 하 여 git `sudo apt-get install git`합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-116">If you are using Linux, install git using hello mechanism most appropriate for you, such as `sudo apt-get install git`.</span></span>
> 
> 

## <a name="forking-and-cloning-hello-todo-application"></a><span data-ttu-id="0c334-117">분기 및 복제 hello TODO 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="0c334-117">Forking and Cloning hello TODO Application</span></span>
<span data-ttu-id="0c334-118">이 자습서에서 사용 하는 할 일 응용 프로그램 hello 할 일 목록 추적 하는 MongoDB 인스턴스에 대해 간단한 웹 프런트 엔드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-118">hello TODO application used by this tutorial implements a simple web frontend over a MongoDB instance that keeps track of a TODO list.</span></span> <span data-ttu-id="0c334-119">TooGitHub 로그인 한 후 이동 [여기](https://github.com/stepro/node-todo) toofind hello 응용 프로그램 및 hello 링크를 사용 하 여 오른쪽 위를 hello에 분기 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-119">After signing in tooGitHub, go [here](https://github.com/stepro/node-todo) toofind hello application and fork it using hello link in hello top right.</span></span> <span data-ttu-id="0c334-120">*accountname*/node-todo로 명명된 계정에 리포지토리를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-120">This should create a repository in your account named *accountname*/node-todo.</span></span>

<span data-ttu-id="0c334-121">이제 개발 컴퓨터에서 이 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-121">Now on your development machine, clone this repository:</span></span>

    git clone https://github.com/accountname/node-todo.git

<span data-ttu-id="0c334-122">에서는 hello 저장소의 로컬 복제본이 약간 나중 toohello 소스 코드 변경 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="0c334-122">We'll use this local clone of hello repository a little later when making changes toohello source code.</span></span>

## <a name="creating-and-configuring-hello-linux-virtual-machines"></a><span data-ttu-id="0c334-123">만들기 및 hello Linux 가상 컴퓨터를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-123">Creating and Configuring hello Linux Virtual Machines</span></span>
<span data-ttu-id="0c334-124">Azure는 Linux 가상 컴퓨터를 사용하는 원시 계산을 훌륭히 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-124">Azure has great support for raw compute using Linux virtual machines.</span></span> <span data-ttu-id="0c334-125">이 부분의 hello 자습서에서는 쉽게 두 Linux 가상 컴퓨터를 실행 하는 방법을 hello TODO 응용 프로그램 toothem, 실행 중인 hello 웹 프런트 엔드에 1과 hello MongoDB 인스턴스 다른 hello에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-125">This part of hello tutorial shows how you can easily spin up two Linux virtual machines and deploy hello TODO application toothem, running hello web frontend on one and hello MongoDB instance on hello other.</span></span>

### <a name="creating-virtual-machines"></a><span data-ttu-id="0c334-126">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="0c334-126">Creating Virtual Machines</span></span>
<span data-ttu-id="0c334-127">hello 가장 쉬운 방법은 toocreate Azure에서 새 가상 컴퓨터는 toouse hello Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-127">hello easiest way toocreate a new virtual machine in Azure is toouse hello Azure Portal.</span></span> <span data-ttu-id="0c334-128">클릭 [여기](https://portal.azure.com) 웹 브라우저에서에 hello Azure 포털에서 toosign을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-128">Click [here](https://portal.azure.com) toosign in and launch hello Azure Portal in your web browser.</span></span> <span data-ttu-id="0c334-129">Azure 포털 hello 로드 되 면 hello 다음 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-129">Once hello Azure Portal has loaded, complete hello following steps:</span></span>

* <span data-ttu-id="0c334-130">안녕하세요 "+ 새로 만들기"를 클릭 합니다. 연결;</span><span class="sxs-lookup"><span data-stu-id="0c334-130">Click hello "+ New" link;</span></span>
* <span data-ttu-id="0c334-131">Hello "을 계산" 범주를 선택 하 고 "Ubuntu Server 14.04 LTS";를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-131">Pick hello "Compute" category and choose "Ubuntu Server 14.04 LTS";</span></span>
* <span data-ttu-id="0c334-132">Hello "리소스 관리자" 배포 모델을 선택 하 고 "만들기";</span><span class="sxs-lookup"><span data-stu-id="0c334-132">Select hello "Resource Manager" deployment model and click "Create";</span></span>
* <span data-ttu-id="0c334-133">다음 지침에 따라 hello 기본 사항을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-133">Fill in hello basics following these guidelines:</span></span>
  * <span data-ttu-id="0c334-134">나중에 쉽게 식별할 수 있는 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-134">Specify a name you can easily identify later;</span></span>
  * <span data-ttu-id="0c334-135">이 자습서에서는 암호 인증을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-135">For this tutorial, choose Password authentication;</span></span>
  * <span data-ttu-id="0c334-136">식별할 수 있는 이름으로 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-136">Create a new resource group with an identifiable name.</span></span>
* <span data-ttu-id="0c334-137">Hello 가상 컴퓨터 크기에 대 한 "A1 표준" 되는 것이 좋습니다가이 자습서에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-137">For hello Virtual Machine size, "A1 Standard" is a reasonable choice for this tutorial.</span></span>
* <span data-ttu-id="0c334-138">추가 설정에 대 한 "Standard" hello 디스크 유형을 확인 하 고 나머지 항목을 기본값으로 hello 모든 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-138">For additional settings, ensure hello disk type is "Standard" and accept all hello remaining defaults.</span></span>
* <span data-ttu-id="0c334-139">Hello 요약 페이지에 hello 만들기를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-139">Kick off hello creation on hello summary page.</span></span>

<span data-ttu-id="0c334-140">위의 hello 수행 hello 웹 프런트 엔드 및 hello MongoDB 인스턴스에 대 한 두 toocreate Linux 가상 컴퓨터에 두 번 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-140">Perform hello above process twice toocreate two Linux virtual machines, one for hello web frontend and one for hello MongoDB instance.</span></span> <span data-ttu-id="0c334-141">Hello 가상 컴퓨터 만들기에는 5-10 분 정도 소요 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-141">Creation of hello virtual machines will take about 5-10 minutes.</span></span>

### <a name="assigning-a-dns-entry-for-virtual-machines"></a><span data-ttu-id="0c334-142">가상 컴퓨터에 DNS 항목 할당</span><span class="sxs-lookup"><span data-stu-id="0c334-142">Assigning a DNS entry for Virtual Machines</span></span>
<span data-ttu-id="0c334-143">Azure에서 만든 가상 컴퓨터는 기본적으로 1.2.3.4와 같은 공용 IP 주소를 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-143">Virtual machines created in Azure are by default only accessible through a public IP address like 1.2.3.4.</span></span> <span data-ttu-id="0c334-144">보겠습니다 hello 컴퓨터 보다 쉽게 식별할 수 있도록 DNS 항목을 지정 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-144">Let's make hello machines more easily identifiable by assigning them DNS entries.</span></span>

<span data-ttu-id="0c334-145">Hello 포털 hello 가상 컴퓨터를 만들었다고에 표시 되 면 hello 왼쪽된 탐색 모음에서 hello "가상 컴퓨터" 링크를 클릭 하 고 컴퓨터를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-145">Once hello portal indicates that hello virtual machines have been created, click on hello "Virtual machines" link in hello left navbar and locate your machines.</span></span> <span data-ttu-id="0c334-146">각 컴퓨터에 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-146">For each machine:</span></span>

* <span data-ttu-id="0c334-147">Hello Essentials 탭을 찾아서 hello 공용 IP 주소; 클릭</span><span class="sxs-lookup"><span data-stu-id="0c334-147">Locate hello Essentials tab and click on hello Public IP Address;</span></span>
* <span data-ttu-id="0c334-148">Hello 공용 IP 주소 구성에서 DNS 이름 레이블을 할당 하 고 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-148">In hello public IP address configuration, assign a DNS name label and save.</span></span>

<span data-ttu-id="0c334-149">hello 포털은 해당 hello 이름을 지정 하는 사용할 수 있는 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-149">hello portal will ensure that hello name you specify is available.</span></span> <span data-ttu-id="0c334-150">Hello 구성에서 저장 한 후 가상 컴퓨터 이름을 갖게 됩니다. 호스트와 유사한 너무`machinename.region.cloudapp.azure.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-150">After saving hello configuration, your virtual machines will have host names similar too`machinename.region.cloudapp.azure.com`.</span></span>

### <a name="connecting-toohello-virtual-machines"></a><span data-ttu-id="0c334-151">Toohello 가상 컴퓨터를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-151">Connecting toohello Virtual Machines</span></span>
<span data-ttu-id="0c334-152">가상 컴퓨터를 프로 비전 된 경우 SSH를 통해 미리 구성 된 tooallow 원격 연결 된입니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-152">When your virtual machines were provisioned, they were pre-configured tooallow remote connections over SSH.</span></span> <span data-ttu-id="0c334-153">이 hello 메커니즘 tooconfigure hello 가상 컴퓨터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-153">This is hello mechanism we will use tooconfigure hello virtual machines.</span></span> <span data-ttu-id="0c334-154">개발 작업을 위한 기간을 사용 하는 경우 이미 않아도 하나 경우 tooget SSH 클라이언트를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-154">If you are using Windows for your development, you will need tooget an SSH client if you do not already have one.</span></span> <span data-ttu-id="0c334-155">여기서 일반적인 선택은 PuTTY이며 [여기](http://www.chiark.greenend.org.uk/~sgtatham/putty/)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-155">A common choice here is PuTTY, which can be downloaded from [here](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span></span> <span data-ttu-id="0c334-156">Macintosh 및 Linux OS는 미리 설치된 SSH 버전으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-156">Macintosh and Linux OSes come with a version of SSH pre-installed.</span></span>

### <a name="configuring-hello-web-frontend-virtual-machine"></a><span data-ttu-id="0c334-157">Hello 웹 프런트 엔드 가상 컴퓨터를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-157">Configuring hello Web Frontend Virtual Machine</span></span>
<span data-ttu-id="0c334-158">SSH toohello 웹 프런트 엔드 컴퓨터를 사용 하 여 PuTTY, ssh 명령줄 또는 다른 임의의 SSH 도구 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-158">SSH toohello web frontend machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="0c334-159">명령 프롬프트에서 다음 환영 메시지가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-159">You should see a welcome message followed by a command prompt.</span></span>

<span data-ttu-id="0c334-160">우선 Git 및 노드가 모두 설치되었는지 확인해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-160">First, let's make sure that git and node are both installed:</span></span>

    sudo apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs

<span data-ttu-id="0c334-161">Hello 응용 프로그램의 웹 프런트 엔드 일부 네이티브 Node.js 모듈을 기반 tooinstall hello는 일련의 기본 빌드 도구도 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-161">Since hello application's web frontend relies on some native Node.js modules, we also need tooinstall hello essential set of build tools:</span></span>

    sudo apt-get install -y build-essential

<span data-ttu-id="0c334-162">마지막으로, 보겠습니다 라는 Node.js 응용 프로그램을 설치 *영원히*, toorun Node.js 서버 응용 프로그램 수:</span><span class="sxs-lookup"><span data-stu-id="0c334-162">Finally, let's install a Node.js application called *forever*, which helps toorun Node.js server applications:</span></span>

    sudo npm install -g forever

<span data-ttu-id="0c334-163">이이 가상 컴퓨터 toobe 수 toorun hello 응용 프로그램의 웹 프런트 엔드에 필요한 모든 hello 종속성을 실행 하는 설정 하겠습니다 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-163">These are all hello dependencies needed on this virtual machine toobe able toorun hello application's web frontend, so let's get that running.</span></span> <span data-ttu-id="0c334-164">toodo이를 먼저 만듭니다 hello GitHub 리포지토리 (다루게 될 것이 업데이트 시나리오 나중) 업데이트 toohello 가상 컴퓨터를 쉽게 게시할 하 고 다음 hello bare 복제 tooprovide를 복제할 수 있도록 이전에 분기의 복제본을 완전 한 버전의 hello 실제로 실행 될 수 있는 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-164">toodo this, we will first create a bare clone of hello GitHub repository you previously forked so that you can easily publish updates toohello virtual machine (we'll cover this update scenario later), and then clone hello bare clone tooprovide a version of hello repository that can actually be executed.</span></span>

<span data-ttu-id="0c334-165">Hello 다음 명령을 실행 hello 홈 (~) 디렉터리에서 시작 합니다 (교체 *accountname* 을 GitHub 사용자 계정 이름):</span><span class="sxs-lookup"><span data-stu-id="0c334-165">Starting from hello home (~) directory, run hello following commands (replacing *accountname* with your GitHub user account name):</span></span>

    git clone --bare https://github.com/accountname/node-todo.git
    git clone node-todo.git

<span data-ttu-id="0c334-166">이제 hello 노드 todo 디렉터리를 입력 하 고이 명령을 실행.</span><span class="sxs-lookup"><span data-stu-id="0c334-166">Now enter hello node-todo directory and run these commands:</span></span>

    npm install
    forever start server.js

<span data-ttu-id="0c334-167">그러나 hello 웹 프런트 엔드 응용 프로그램의 실행 되, 즉 하나의 단계가 더 웹 브라우저에서 hello 응용 프로그램에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-167">hello application's web frontend is now running, however there is one more step before you can access hello application from a web browser.</span></span> <span data-ttu-id="0c334-168">hello 만든 가상 컴퓨터 보호 되는 Azure 리소스를 호출 하 여 한 *네트워크 보안 그룹*, 만든 가상 컴퓨터를 프로 비전 할 때 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-168">hello virtual machine you created is protected by an Azure resource called a *network security group*, which was created for you when you provisioned hello virtual machine.</span></span> <span data-ttu-id="0c334-169">현재이 리소스는 외부 요청 tooport 라우팅된 22 toobe toohello 있는 가상 컴퓨터 hello 컴퓨터 하지만 다른와 SSH 통신만 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-169">Currently, this resource only allows external requests tooport 22 toobe routed toohello virtual machine, which enables SSH communication with hello machine but nothing else.</span></span> <span data-ttu-id="0c334-170">따라서 순서 tooview hello 포트 8080에서 구성 된 toorun 되 TODO 응용 프로그램에서에서이 포트도 필요 열렸습니다 toobe 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-170">So in order tooview hello TODO application, which is configured toorun on port 8080, this port also needs toobe opened up.</span></span>

<span data-ttu-id="0c334-171">Toohello Azure 포털을 반환 하 고 hello 다음 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-171">Return toohello Azure Portal and complete hello following steps:</span></span>

* <span data-ttu-id="0c334-172">"리소스 그룹" hello 왼쪽된 탐색 모음; 클릭</span><span class="sxs-lookup"><span data-stu-id="0c334-172">Click on "Resource groups" in hello left navbar;</span></span>
* <span data-ttu-id="0c334-173">가상 컴퓨터를 포함 하는 hello 리소스 그룹 선택</span><span class="sxs-lookup"><span data-stu-id="0c334-173">Select hello resource group that contains your virtual machine;</span></span>
* <span data-ttu-id="0c334-174">리소스의 hello 결과 목록에서 hello 네트워크 보안 그룹 (hello 하나 방패 아이콘으로);를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-174">In hello resulting list of resources, select hello network security group (hello one with a shield icon);</span></span>
* <span data-ttu-id="0c334-175">Hello 속성에서 "인바운드 보안 규칙";를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-175">In hello properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="0c334-176">Hello 도구 모음에서 "추가"를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-176">In hello toolbar, click "Add";</span></span>
* <span data-ttu-id="0c334-177">"default-allow-todo"와 같은 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-177">Provide a name like "default-allow-todo";</span></span>
* <span data-ttu-id="0c334-178">너무 hello 프로토콜 설정 "TCP";</span><span class="sxs-lookup"><span data-stu-id="0c334-178">Set hello protocol too"TCP";</span></span>
* <span data-ttu-id="0c334-179">대상 포트 범위를 hello 설정 너무 "8080";</span><span class="sxs-lookup"><span data-stu-id="0c334-179">Set hello destination port range too"8080";</span></span>
* <span data-ttu-id="0c334-180">확인을 클릭 하 고 hello 보안 규칙 toobe 생성 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-180">Click OK and wait for hello security rule toobe created.</span></span>

<span data-ttu-id="0c334-181">이 보안 규칙을 만든 후 hello TODO 응용 프로그램에 공개적으로 표시 되는 인터넷 hello 및 URL을와 같은 사용 하는 예를 들어 tooit를 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-181">After creating this security rule, hello TODO application is publically visible on hello internet and you can browse tooit, for instance using a URL such as:</span></span>

    http://machinename.region.cloudapp.azure.com:8080

<span data-ttu-id="0c334-182">에서는 아직 구성 하지 않은 hello MongoDB 가상 컴퓨터, 경우에 hello TODO 응용 프로그램 기능 매우 toobe이 표시 되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-182">You will notice that even though we have not yet configured hello MongoDB virtual machine, hello TODO application appears toobe quite functional.</span></span> <span data-ttu-id="0c334-183">Hello 소스 리포지토리는 하드 코드 된 toouse 미리 배포 MongoDB 인스턴스 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-183">This is because hello source repository is hardcoded toouse a pre-deployed MongoDB instance.</span></span> <span data-ttu-id="0c334-184">Hello MongoDB 가상 컴퓨터를 구성한 후 뒤로 이동 하 고 대신 hello 소스 코드 tooutilize 개인 MongoDB 인스턴스를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-184">Once we have configured hello MongoDB virtual machine, we will go back and change hello source code tooutilize our private MongoDB instance instead.</span></span>

### <a name="configuring-hello-mongodb-virtual-machine"></a><span data-ttu-id="0c334-185">Hello MongoDB 가상 컴퓨터를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-185">Configuring hello MongoDB Virtual Machine</span></span>
<span data-ttu-id="0c334-186">SSH toohello 두 번째 컴퓨터를 사용 하 여 PuTTY, ssh 명령줄 또는 다른 임의의 SSH 도구 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-186">SSH toohello second machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="0c334-187">Hello 환영 메시지 및 명령 프롬프트를 확인 한 후 MongoDB 설치 (이 지침에서 수행 된 [여기](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span><span class="sxs-lookup"><span data-stu-id="0c334-187">After seeing hello welcome message and command prompt, install MongoDB (these instructions were taken from [here](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span></span>

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
    sudo apt-get update
    sudo apt-get install -y mongodb-org

<span data-ttu-id="0c334-188">기본적으로 MongoDB는 로컬로 액세스할 수 있도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-188">By default, MongoDB is configured so it can only be accessed locally.</span></span> <span data-ttu-id="0c334-189">이 자습서에서는 hello 응용 프로그램의 가상 컴퓨터에서 액세스할 수 있도록 MongoDB 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-189">For this tutorial, we will configure MongoDB so it can be accessed from hello application's virtual machine.</span></span> <span data-ttu-id="0c334-190">Sudo 컨텍스트에서 hello /etc/mongod.conf 파일을 열고 hello 찾을 `# network interfaces` 섹션.</span><span class="sxs-lookup"><span data-stu-id="0c334-190">In a sudo context, open hello /etc/mongod.conf file and locate hello `# network interfaces` section.</span></span> <span data-ttu-id="0c334-191">변경 hello `net.bindIp` 구성 값 너무`0.0.0.0`합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-191">Change hello `net.bindIp` configuration value too`0.0.0.0`.</span></span>

> [!NOTE]
> <span data-ttu-id="0c334-192">이 구성은이 자습서에만 hello 목적입니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-192">This configuration is for hello purposes of this tutorial only.</span></span> <span data-ttu-id="0c334-193">권장되는 보안 사례가 **아니고** 프로덕션 환경에서는 사용되면 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-193">It is **NOT** a recommended security practice and should not be used in production environments.</span></span>
> 
> 

<span data-ttu-id="0c334-194">이제 hello MongoDB 서비스가 시작 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-194">Now ensure hello MongoDB service has been started:</span></span>

    sudo service mongod restart

<span data-ttu-id="0c334-195">MongoDB는 기본적으로 포트 27017에 대해 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-195">MongoDB operates over port 27017 by default.</span></span> <span data-ttu-id="0c334-196">Hello에 동일한 방식으로 tooopen 했습니다: 포트 8080 hello 웹 프런트 엔드 가상 컴퓨터에 있으므로 tooopen 포트 27017 hello MongoDB 가상 컴퓨터에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-196">So, in hello same way that we needed tooopen port 8080 on hello web frontend virtual machine, we need tooopen port 27017 on hello MongoDB virtual machine.</span></span>

<span data-ttu-id="0c334-197">Toohello Azure 포털을 반환 하 고 hello 다음 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-197">Return toohello Azure Portal and complete hello following steps:</span></span>

* <span data-ttu-id="0c334-198">"리소스 그룹" hello 왼쪽된 탐색 모음; 클릭</span><span class="sxs-lookup"><span data-stu-id="0c334-198">Click on "Resource groups" in hello left navbar;</span></span>
* <span data-ttu-id="0c334-199">Hello MongoDB 가상 컴퓨터를 포함 하는 hello 리소스 그룹 선택</span><span class="sxs-lookup"><span data-stu-id="0c334-199">Select hello resource group that contains hello MongoDB virtual machine;</span></span>
* <span data-ttu-id="0c334-200">리소스의 hello 결과 목록에서 toohello MongoDB 가상 컴퓨터를 지정한 이름과 같은 이름을 hello로 hello 네트워크 보안 그룹 (hello 하나 방패 아이콘으로)을 선택</span><span class="sxs-lookup"><span data-stu-id="0c334-200">In hello resulting list of resources, select hello network security group (hello one with a shield icon) with hello same name that you gave toohello MongoDB virtual machine;</span></span>
* <span data-ttu-id="0c334-201">Hello 속성에서 "인바운드 보안 규칙";를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-201">In hello properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="0c334-202">Hello 도구 모음에서 "추가"를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-202">In hello toolbar, click "Add";</span></span>
* <span data-ttu-id="0c334-203">"default-allow-mongo"와 같은 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-203">Provide a name like "default-allow-mongo";</span></span>
* <span data-ttu-id="0c334-204">너무 hello 프로토콜 설정 "TCP";</span><span class="sxs-lookup"><span data-stu-id="0c334-204">Set hello protocol too"TCP";</span></span>
* <span data-ttu-id="0c334-205">대상 포트 범위를 hello 설정 너무 "27017";</span><span class="sxs-lookup"><span data-stu-id="0c334-205">Set hello destination port range too"27017";</span></span>
* <span data-ttu-id="0c334-206">확인을 클릭 하 고 hello 보안 규칙 toobe 생성 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-206">Click OK and wait for hello security rule toobe created.</span></span>

## <a name="iterating-on-hello-todo-application"></a><span data-ttu-id="0c334-207">Hello TODO 응용 프로그램에서 반복</span><span class="sxs-lookup"><span data-stu-id="0c334-207">Iterating on hello TODO application</span></span>
<span data-ttu-id="0c334-208">지금까지 것을 프로 비전 Linux 가상 컴퓨터 2: MongoDB 인스턴스 하나를 실행 하는 hello 응용 프로그램의 웹 프런트 엔드 및 하나를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-208">So far, we have provisioned two Linux virtual machines: one that is running hello application's web frontend and one that is running a MongoDB instance.</span></span> <span data-ttu-id="0c334-209">하지만 문제가-hello 웹 프런트 엔드 사용자를 프로 비전 하는 hello MongoDB 인스턴스를 아직 사용 실제로 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-209">But there is a problem - hello web frontend isn't actually using hello provisioned MongoDB instance yet.</span></span> <span data-ttu-id="0c334-210">문제를 해결 하겠습니다 hello 웹 프런트 엔드 코드 toouse를 업데이트 하 여 하드 코드 된 인스턴스 대신 환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-210">Let's fix that by updating hello web frontend code toouse an environment variable instead of a hard-coded instance.</span></span>

### <a name="changing-hello-todo-application"></a><span data-ttu-id="0c334-211">Hello TODO 응용 프로그램 변경</span><span class="sxs-lookup"><span data-stu-id="0c334-211">Changing hello TODO application</span></span>
<span data-ttu-id="0c334-212">먼저 hello 노드 todo 리포지토리를 복제 하려면 개발 컴퓨터에 hello 열고 `node-todo/config/database.js` 선호 하는 편집기에서 파일을 hello url 값과 같은 hello 하드 코드 된 값에서 변경 `mongodb://...` 너무`process.env.MONGODB`합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-212">On your development machine where you first cloned hello node-todo repository, open hello `node-todo/config/database.js` file in your favorite editor and change hello url value from hello hard-coded value like `mongodb://...` too`process.env.MONGODB`.</span></span>

<span data-ttu-id="0c334-213">변경 내용을 커밋하고 toohello GitHub 마스터 푸시하십시오.</span><span class="sxs-lookup"><span data-stu-id="0c334-213">Commit your changes and push toohello GitHub master:</span></span>

    git commit -am "Get MongoDB instance from env"
    git push origin master

<span data-ttu-id="0c334-214">그러나이 hello 변경 toohello 웹 프런트 엔드 가상 컴퓨터를 게시 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-214">Unfortunately, this doesn't publish hello change toohello web frontend virtual machine.</span></span> <span data-ttu-id="0c334-215">이제 몇 가지 더 많은 변경 내용을 toothat 가상 컴퓨터 tooenable hello hello 실제 환경에서 hello 변경 효과 신속 하 게 살펴볼 수 있도록 업데이트를 게시 하기 위한 단순 하지만 효율적인 메커니즘을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-215">Let's make a few more changes toothat virtual machine tooenable a simple but effective mechanism for publishing updates so you can quickly observe hello effect of hello changes in hello live environment.</span></span>

### <a name="configuring-hello-web-frontend-virtual-machine"></a><span data-ttu-id="0c334-216">Hello 웹 프런트 엔드 가상 컴퓨터를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-216">Configuring hello Web Frontend Virtual Machine</span></span>
<span data-ttu-id="0c334-217">이전에 만들었다고 hello 노드 todo 저장소의 복제본을 bare hello 웹 프런트 엔드 가상 컴퓨터에서 다시 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-217">Recall that we previously created a bare clone of hello node-todo repository on hello web frontend virtual machine.</span></span> <span data-ttu-id="0c334-218">밝혀졌습니다이 작업을 원격 toowhich 변경 내용을 푸시 될 수 있는 새 Git 만들었음을 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-218">It turns out that this action created a new Git remote toowhich changes can be pushed.</span></span> <span data-ttu-id="0c334-219">그러나 단순히 toothis 원격 푸시하여 매우 코드에서 작업할 때 개발자가 찾고 hello 신속 하 게 반복 모델을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-219">However, simply pushing toothis remote doesn't quite give hello rapid iteration model that developers are looking for when working on their code.</span></span>

<span data-ttu-id="0c334-220">어떤 것을 toobe 수 toodo는 hello 가상 컴퓨터에 밀어넣기 toohello 원격 리포지토리 발생할 때 TODO 응용 프로그램을 실행 하는 hello는 자동으로 업데이트 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-220">What we would like toobe able toodo is ensure that when a push toohello remote repository on hello virtual machine occurs, hello running TODO application is automatically updated.</span></span> <span data-ttu-id="0c334-221">다행히이 작업은 쉽게 tooachieve git 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-221">Fortunately, this is easy tooachieve with git.</span></span>

<span data-ttu-id="0c334-222">Git 후크 hello 저장소에서 수행 된 특정 시간 tooreact tooactions에 호출 되는 수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-222">Git exposes a number of hooks that are called at particular times tooreact tooactions taken on hello repository.</span></span> <span data-ttu-id="0c334-223">셸 스크립트를 사용 하 여 hello 저장소에 지정 된 이러한 `hooks` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-223">These are specified using shell scripts in hello repository's `hooks` folder.</span></span> <span data-ttu-id="0c334-224">속성은 hello 자동 업데이트 시나리오에 가장 적합 hello 후크는 hello `post-update` 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-224">hello hook that is most applicable for hello auto-update scenario is hello `post-update` event.</span></span>

<span data-ttu-id="0c334-225">SSH 세션 toohello 웹 프런트 엔드를 가상 컴퓨터에서 변경 toohello `~/node-todo.git/hooks` 디렉터리 hello 다음 라는 tooa 콘텐츠 파일을 추가 하 고 `post-update` (교체 `machinename` 및 `region` MongoDB 가상 컴퓨터 정보로):</span><span class="sxs-lookup"><span data-stu-id="0c334-225">In a SSH session toohello web frontend virtual machine, change toohello `~/node-todo.git/hooks` directory and add hello following content tooa file named `post-update` (replacing `machinename` and `region` with your MongoDB virtual machine information):</span></span>

    #!/bin/bash

    forever stopall
    unset 'GIT_DIR'
    export MONGODB="mongodb://machinename.region.cloudapp.azure.com:27017/tododb"
    cd ~/node-todo && git fetch origin && git pull origin master && npm install && forever start ~/node-todo/server.js
    exec git update-server-info

<span data-ttu-id="0c334-226">Hello 다음 명령을 실행 하 여이 파일은 실행 파일을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-226">Ensure this file is executable by running hello following command:</span></span>

    chmod 755 post-update

<span data-ttu-id="0c334-227">이 스크립트를 사용 하면 현재 hello 서버 응용 프로그램이 중지 되, hello 복제 된 저장소의 hello 코드를 업데이트 된 toohello 최신, 업데이트 된 종속성을 만족 hello 서버를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-227">This script ensures that hello current server application is stopped, hello code in hello cloned repository is updated toohello latest, any updated dependencies are satisfied, and hello server is restarted.</span></span> <span data-ttu-id="0c334-228">또한 해당 hello 환경 수행 하도록 구성 되는 환경 변수에서 첫 번째 응용 프로그램 업데이트 tooget hello MongoDB 인스턴스를 수신 하기 위해 준비 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-228">It also ensures that hello environment has been configured in preparation for receiving our first application update tooget hello MongoDB instance from an environment variable.</span></span>

### <a name="configuring-your-development-machine"></a><span data-ttu-id="0c334-229">개발 컴퓨터 구성</span><span class="sxs-lookup"><span data-stu-id="0c334-229">Configuring your Development Machine</span></span>
<span data-ttu-id="0c334-230">이제 개발 컴퓨터 toohello 웹 프런트 엔드 가상 컴퓨터를 연결 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-230">Now let's get your development machine hooked up toohello web frontend virtual machine.</span></span> <span data-ttu-id="0c334-231">이 hello 완전 저장소는 원격 hello 가상 컴퓨터에 추가 하는 것과 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-231">This is as simple as adding hello bare repository on hello virtual machine as a remote.</span></span> <span data-ttu-id="0c334-232">이 스크립트 명령 toodo 다음 hello를 실행 (교체 *사용자* 을 웹 프런트 엔드 가상 컴퓨터 로그인 이름 및 *machinename* 및 *지역* 적절 하 게):</span><span class="sxs-lookup"><span data-stu-id="0c334-232">Run hello following command toodo this (replacing *user* with your web frontend virtual machine login name and *machinename* and *region* as appropriate):</span></span>

    git remote add azure user@machinename.region.cloudapp.azure.com:node-todo.git

<span data-ttu-id="0c334-233">이 필요한 tooenable 밀어넣거나 게시 적용, toohello 웹 프런트 엔드 가상 컴퓨터를 변경 하는 all입니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-233">This is all that is needed tooenable pushing, or in effect publishing, changes toohello web frontend virtual machine.</span></span>

### <a name="publishing-updates"></a><span data-ttu-id="0c334-234">업데이트 게시</span><span class="sxs-lookup"><span data-stu-id="0c334-234">Publishing Updates</span></span>
<span data-ttu-id="0c334-235">Hello 응용 프로그램에서 고유한 MongoDB 인스턴스를 사용할 수 있도록 지금까지 설정한 hello 하나의 변경을 게시 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-235">Let's publish hello one change that has been made so far so that hello application will use our own MongoDB instance:</span></span>

    git push azure master

<span data-ttu-id="0c334-236">출력 유사한 toothis를 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-236">You should see output similar toothis:</span></span>

    Counting objects: 4, done.
    Delta compression using up too4 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (4/4), 406 bytes | 0 bytes/s, done.
    Total 4 (delta 1), reused 0 (delta 0)
    remote: info:    Forever stopped processes:
    remote: data:        uid  command         script    forever pid  id logfile                         uptime
    remote: data:    [0] 0Lyh /usr/bin/nodejs server.js 9064    9301    /home/username/.forever/0Lyh.log 0:0:3:17.487
    remote: From /home/username/node-todo
    remote:    5f31fd7..5bc7be5  master     -> origin/master
    remote: From /home/username/node-todo
    remote:  * branch            master     -> FETCH_HEAD
    remote: Updating 5f31fd7..5bc7be5
    remote: Fast-forward
    remote:  config/database.js | 2 +-
    remote:  1 file changed, 1 insertion(+), 1 deletion(-)
    remote: npm WARN package.json node-todo@0.0.0 No repository field.
    remote: npm WARN package.json node-todo@0.0.0 No license field.
    remote: warn:    --minUptime not set. Defaulting to: 1000ms
    remote: warn:    --spinSleepTime not set. Your script will exit if it does not stay up for at least 1000ms
    remote: info:    Forever processing file: /home/username/node-todo/server.js
    toousername@machinename.region.cloudapp.azure.com:node-todo.git
    5f31fd7..5bc7be5  master -> master

<span data-ttu-id="0c334-237">이 명령이 완료 된 후에 웹 브라우저에서 hello 응용 프로그램을 새로 고쳐 보십시오.</span><span class="sxs-lookup"><span data-stu-id="0c334-237">After this command completes, try refreshing hello application in a web browser.</span></span> <span data-ttu-id="0c334-238">여기에 제시 된 hello 할 일 목록은 비어 있으며 공유 동률된 toohello MongoDB 인스턴스를 배포 하는 더 이상 수 toosee 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-238">You should be able toosee that hello TODO list presented here is empty and no longer tied toohello shared deployed MongoDB instance.</span></span>

<span data-ttu-id="0c334-239">toocomplete hello 자습서 다른, 더 많은 보이는 변경을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-239">toocomplete hello tutorial, let's make another, more visible change.</span></span> <span data-ttu-id="0c334-240">개발 컴퓨터에서 선호 하는 편집기를 사용 하 여 hello node-todo/public/index.html 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-240">On your development machine, open hello node-todo/public/index.html file using your favorite editor.</span></span> <span data-ttu-id="0c334-241">Hello jumbotron 헤더를 찾아서 "저는 Todo-aholic"에서 너무 "I am Azure에서 Todo aholic!" hello 제목을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-241">Locate hello jumbotron header and change  hello title from "I'm a Todo-aholic" too"I'm a Todo-aholic on Azure!".</span></span>

<span data-ttu-id="0c334-242">이제 커밋하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-242">Now let's commit:</span></span>

    git commit -am "Azurify hello title"

<span data-ttu-id="0c334-243">이 시간, tooback toohello GitHub 리포지토리를 푸시하기 전에 hello 변경 tooAzure를 게시 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-243">This time, let's publish hello change tooAzure before pushing it tooback toohello GitHub repo:</span></span>

    git push azure master

<span data-ttu-id="0c334-244">이 명령이 완료 되 면 hello 웹 페이지를 새로 고 hello 변경 내용이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-244">Once this command completes, refresh hello web page and you will see hello changes.</span></span> <span data-ttu-id="0c334-245">자신을 이후 hello 변경 백 toohello 원본 원격 강제:</span><span class="sxs-lookup"><span data-stu-id="0c334-245">Since they look good, push hello change back toohello origin remote:</span></span> 

    git push origin master

## <a name="next-steps"></a><span data-ttu-id="0c334-246">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0c334-246">Next Steps</span></span>
<span data-ttu-id="0c334-247">방법을 보여 주었습니다.이 문서 tootake Node.js 응용 프로그램을 Azure에서 실행 중인 tooLinux 가상 컴퓨터에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-247">This article showed how tootake a Node.js application and deploy it tooLinux virtual machines running in Azure.</span></span> <span data-ttu-id="0c334-248">Azure에서 Linux 가상 컴퓨터에 대해 자세히 toolearn 참조 [Azure에서 소개 tooLinux](/documentation/articles/virtual-machines-linux-introduction/)합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-248">toolearn more about Linux virtual machines in Azure, see [Introduction tooLinux on Azure](/documentation/articles/virtual-machines-linux-introduction/).</span></span>

<span data-ttu-id="0c334-249">방법에 대 한 자세한 내용은 Azure에서 Node.js 응용 프로그램 toodevelop 참조 hello [Node.js 개발자 센터](/develop/nodejs/)합니다.</span><span class="sxs-lookup"><span data-stu-id="0c334-249">For more information about how toodevelop Node.js applications on Azure, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

