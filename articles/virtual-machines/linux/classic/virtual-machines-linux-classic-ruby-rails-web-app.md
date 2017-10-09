---
title: "Linux VM의 레일 웹 사이트에서 Ruby aaaHost | Microsoft Docs"
description: "Azure에서 Linux 가상 컴퓨터를 사용하여 Ruby on Rails 기반 웹 사이트를 설정 및 호스트하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: ruby
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: aad32685-3550-4bff-9c73-beb8d70b3291
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: ruby
ms.topic: article
ms.date: 06/27/2017
ms.author: robmcm
ms.openlocfilehash: c545c24fc6c89497854bbe55a6d0d1d0b072c386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="ruby-on-rails-web-application-on-an-azure-vm"></a><span data-ttu-id="ae7ee-103">Azure VM의 Ruby on Rails 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ae7ee-103">Ruby on Rails Web application on an Azure VM</span></span>
<span data-ttu-id="ae7ee-104">이 자습서에서는 어떻게 toohost Linux 가상 컴퓨터를 사용 하 여 Azure에서 레일 웹 사이트에 Ruby 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-104">This tutorial shows how toohost a Ruby on Rails website on Azure using a Linux virtual machine.</span></span>  

<span data-ttu-id="ae7ee-105">이 자습서의 내용은 Ubuntu Server 14.04 LTS를 사용하여 유효성이 검사되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-105">This tutorial was validated using Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="ae7ee-106">다른 Linux 배포판을 사용 하는 경우 해야 toomodify hello tooinstall 레일 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-106">If you use a different Linux distribution, you might need toomodify hello steps tooinstall Rails.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ae7ee-107">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="ae7ee-108">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="ae7ee-109">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
>
>

## <a name="create-an-azure-vm"></a><span data-ttu-id="ae7ee-110">Azure VM 만들기</span><span class="sxs-lookup"><span data-stu-id="ae7ee-110">Create an Azure VM</span></span>
<span data-ttu-id="ae7ee-111">Linux 이미지와 Azure VM을 만들어 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-111">Start by creating an Azure VM with a Linux image.</span></span>

<span data-ttu-id="ae7ee-112">toocreate VM hello, hello Azure 포털을 사용 하거나 Azure 명령줄 인터페이스 (CLI) hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-112">toocreate hello VM, you can use hello Azure portal or hello Azure Command-Line Interface (CLI).</span></span>

### <a name="azure-portal"></a><span data-ttu-id="ae7ee-113">Azure portal</span><span class="sxs-lookup"><span data-stu-id="ae7ee-113">Azure portal</span></span>
1. <span data-ttu-id="ae7ee-114">Hello에 로그인 [Azure 포털](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="ae7ee-114">Sign into hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="ae7ee-115">클릭 **새로**, hello 검색 상자에 "Ubuntu Server 14.04"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-115">Click **New**, then type "Ubuntu Server 14.04" in hello search box.</span></span> <span data-ttu-id="ae7ee-116">Hello 검색에서 반환 된 hello 항목을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-116">Click hello entry returned by hello search.</span></span> <span data-ttu-id="ae7ee-117">Hello 배포 모델에 대 한 선택 **클래식**, 다음 "만들기"를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-117">For hello deployment model, select **Classic**, then click "Create".</span></span>
3. <span data-ttu-id="ae7ee-118">Hello 기본 사항 블레이드에서 필수 hello 필드에 대 한 값을 제공 합니다: (hello VM)에 대 한 이름, 사용자 이름, 인증 유형 및 hello 해당 자격 증명, Azure 구독, 리소스 그룹 및 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-118">In hello Basics blade, supply values for hello required fields: Name (for hello VM), User name, Authentication type and hello corresponding credentials, Azure subscription, Resource group, and Location.</span></span>

   ![새 Ubuntu 이미지 만들기](./media/virtual-machines-linux-classic-ruby-rails-web-app/createvm.png)

4. <span data-ttu-id="ae7ee-120">Hello VM 프로 비전 되 면 hello VM 이름을 클릭 하 고 클릭 **끝점** hello에 **설정을** 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-120">After hello VM is provisioned, click on hello VM name, and click **Endpoints** in hello **Settings** category.</span></span> <span data-ttu-id="ae7ee-121">아래에 나열 되는 hello SSH 끝점을 찾을 **독립 실행형**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-121">Find hello SSH endpoint, listed under **Standalone**.</span></span>

   ![기본 끝점](./media/virtual-machines-linux-classic-ruby-rails-web-app/endpointsnewportal.png)

### <a name="azure-cli"></a><span data-ttu-id="ae7ee-123">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ae7ee-123">Azure CLI</span></span>
<span data-ttu-id="ae7ee-124">Hello 단계에 따라 [는 Linux 가상 컴퓨터 실행을 만들][vm-instructions]합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-124">Follow hello steps in [Create a Virtual Machine Running Linux][vm-instructions].</span></span>

<span data-ttu-id="ae7ee-125">Hello VM 프로 비전 되 면 hello 다음 명령을 실행 하 여 hello SSH 끝점을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-125">After hello VM is provisioned, you can get hello SSH endpoint by running hello following command:</span></span>

    azure vm endpoint list <vm-name>  

## <a name="install-ruby-on-rails"></a><span data-ttu-id="ae7ee-126">Rails에 Ruby 설치</span><span class="sxs-lookup"><span data-stu-id="ae7ee-126">Install Ruby on Rails</span></span>
1. <span data-ttu-id="ae7ee-127">SSH tooconnect toohello VM을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-127">Use SSH tooconnect toohello VM.</span></span>
2. <span data-ttu-id="ae7ee-128">Hello SSH 세션에서 명령을 tooinstall Ruby에 나오는 hello VM에 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-128">From hello SSH session, use hello following commands tooinstall Ruby on hello VM:</span></span>

        sudo apt-get update -y
        sudo apt-get upgrade -y

        sudo apt-add-repository ppa:brightbox/ruby-ng
        sudo apt-get update
        sudo apt-get install ruby2.4

        > [!TIP]
        > hello brightbox repository contains hello current Ruby distribution.

    <span data-ttu-id="ae7ee-129">hello 설치는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-129">hello installation may take a few minutes.</span></span> <span data-ttu-id="ae7ee-130">작업이 완료 될 때 사용 하 여 hello 다음 명령 tooverify Ruby가 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-130">When it completes, use hello following command tooverify that Ruby is installed:</span></span>

        ruby -v

3. <span data-ttu-id="ae7ee-131">사용 하 여 hello 다음 명령 tooinstall 레일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-131">Use hello following command tooinstall Rails:</span></span>

        sudo gem install rails --no-rdoc --no-ri -V

    <span data-ttu-id="ae7ee-132">Hello-no rdoc 및--no ri 플래그 tooskip 더 빠른 hello 설명서 설치를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-132">Use hello --no-rdoc and --no-ri flags tooskip installing hello documentation, which is faster.</span></span>
    <span data-ttu-id="ae7ee-133">이 명령은 tooexecute,-V hello 추가 되므로 설치 진행률 hello에 대 한 정보를 표시 됩니다는 오랜 시간이 걸립니다 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-133">This command will likely take a long time tooexecute, so adding hello -V will display information about hello installation progress.</span></span>

## <a name="create-and-run-an-app"></a><span data-ttu-id="ae7ee-134">앱 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="ae7ee-134">Create and run an app</span></span>
<span data-ttu-id="ae7ee-135">에 계속 로그인 한 SSH를 통해, hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-135">While still logged in via SSH, run hello following commands:</span></span>

    rails new myapp
    cd myapp
    rails server -b 0.0.0.0 -p 3000

<span data-ttu-id="ae7ee-136">hello [새](http://guides.rubyonrails.org/command_line.html#rails-new) 명령은 새 레일 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-136">hello [new](http://guides.rubyonrails.org/command_line.html#rails-new) command creates a new Rails app.</span></span> <span data-ttu-id="ae7ee-137">hello [서버](http://guides.rubyonrails.org/command_line.html#rails-server) 시작 hello WEBrick 웹 서버 레일와 함께 제공 되는 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-137">hello [server](http://guides.rubyonrails.org/command_line.html#rails-server) command starts hello WEBrick web server that comes with Rails.</span></span> <span data-ttu-id="ae7ee-138">(프로덕션 용도로 싶을 toouse 유니콘, 승객 등의 다른 서버입니다.)</span><span class="sxs-lookup"><span data-stu-id="ae7ee-138">(For production use, you would probably want toouse a different server, such as Unicorn or Passenger.)</span></span>

<span data-ttu-id="ae7ee-139">유사한 toohello 다음 출력이 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-139">You should see output similar toohello following.</span></span>

    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://0.0.0.0:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C tooshutdown server
    [2015-06-09 23:34:23] INFO  WEBrick 1.3.1
    [2015-06-09 23:34:23] INFO  ruby 1.9.3 (2013-11-22) [x86_64-linux]
    [2015-06-09 23:34:23] INFO  WEBrick::HTTPServer#start: pid=27766 port=3000

## <a name="add-an-endpoint"></a><span data-ttu-id="ae7ee-140">끝점 추가</span><span class="sxs-lookup"><span data-stu-id="ae7ee-140">Add an endpoint</span></span>
1. <span data-ttu-id="ae7ee-141">[Azure 포털] toohello 이동 [https://portal.azure.com] VM을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-141">Go toohello [Azure portal][https://portal.azure.com] and select your VM.</span></span>

2. <span data-ttu-id="ae7ee-142">선택 **끝점** hello에 **설정을** hello 왼쪽된 가장자리 hello 페이지와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-142">Select **ENDPOINTS** in hello **Settings** along hello left edge hello page.</span></span>

3. <span data-ttu-id="ae7ee-143">클릭 **추가** hello hello 페이지 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-143">Click **ADD** at hello top of hello page.</span></span>

4. <span data-ttu-id="ae7ee-144">Hello에 **끝점 추가** 대화 상자 페이지에서 다음 정보는 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-144">In hello **Add endpoint** dialog page, enter hello following information:</span></span>

   * <span data-ttu-id="ae7ee-145">**이름**: HTTP</span><span class="sxs-lookup"><span data-stu-id="ae7ee-145">**Name**: HTTP</span></span>
   * <span data-ttu-id="ae7ee-146">**프로토콜**: - TCP</span><span class="sxs-lookup"><span data-stu-id="ae7ee-146">**Protocol**: TCP</span></span>
   * <span data-ttu-id="ae7ee-147">**공용 포트**: 80</span><span class="sxs-lookup"><span data-stu-id="ae7ee-147">**Public port**: 80</span></span>
   * <span data-ttu-id="ae7ee-148">**개인 포트**: 3000</span><span class="sxs-lookup"><span data-stu-id="ae7ee-148">**Private port**: 3000</span></span>
   * <span data-ttu-id="ae7ee-149">**부동 PI 주소**: 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="ae7ee-149">**Floating PI address**: Disabled</span></span>
   * <span data-ttu-id="ae7ee-150">**액세스 제어 목록-순서**: 1001, 또는 다른 값이 액세스 규칙의 우선 순위 hello 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-150">**Access control list - Order**: 1001, or another value that sets hello priority of this access rule.</span></span>
   * <span data-ttu-id="ae7ee-151">**액세스 제어 목록 - 이름**: allowHTTP</span><span class="sxs-lookup"><span data-stu-id="ae7ee-151">**Access control list - Name**: allowHTTP</span></span>
   * <span data-ttu-id="ae7ee-152">**액세스 제어 목록 - 작업**: 허용</span><span class="sxs-lookup"><span data-stu-id="ae7ee-152">**Access control list - Action**: permit</span></span>
   * <span data-ttu-id="ae7ee-153">**액세스 제어 목록 - 원격 서브넷**: 1.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="ae7ee-153">**Access control list - Remote subnet**: 1.0.0.0/16</span></span>

     <span data-ttu-id="ae7ee-154">이 끝점에 트래픽을 toohello 개인 포트 3000, hello 레일 서버 수신 대기 라우팅합니다. 80 공용 포트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-154">This endpoint  has a public port of 80 that will route traffic toohello private port of 3000, where hello Rails server is listening.</span></span> <span data-ttu-id="ae7ee-155">hello 액세스 제어 목록 규칙에는 포트 80에서 공용 트래픽을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-155">hello access control list rule allows public traffic on port 80.</span></span>

     ![new-endpoint](./media/virtual-machines-linux-classic-ruby-rails-web-app/createendpoint.png)

5. <span data-ttu-id="ae7ee-157">확인 toosave hello 끝점을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-157">Click OK toosave hello endpoint.</span></span>

6. <span data-ttu-id="ae7ee-158">메시지가 **가상 컴퓨터 끝점 저장**을 표시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-158">A message should appear that states **Saving virtual machine endpoint**.</span></span> <span data-ttu-id="ae7ee-159">이 메시지가 사라집니다 되 면 hello 끝점이 활성 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-159">Once this message disappears, hello endpoint is active.</span></span> <span data-ttu-id="ae7ee-160">이제 가상 컴퓨터의 DNS 이름을 toohello 이동 하 여 응용 프로그램을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-160">You may now test your application by navigating toohello DNS name of your virtual machine.</span></span> <span data-ttu-id="ae7ee-161">hello 웹 사이트에는 비슷한 toohello 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-161">hello website should appear similar toohello following:</span></span>

    ![기본 Rails 페이지][default-rails-cloud]

## <a name="next-steps"></a><span data-ttu-id="ae7ee-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ae7ee-163">Next steps</span></span>
<span data-ttu-id="ae7ee-164">이 자습서에서는 수행한 hello 단계 중 대부분 수동으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-164">In this tutorial, you did most of hello steps manually.</span></span> <span data-ttu-id="ae7ee-165">프로덕션 환경에서 개발 컴퓨터에서 앱을 작성 하는 toohello Azure VM을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-165">In a production environment, you would write your app on a development machine and deploy it toohello Azure VM.</span></span> <span data-ttu-id="ae7ee-166">또한 대부분의 프로덕션 환경 Apache 또는 처리 하는 정적 리소스 이며 hello 레일 응용 프로그램의 라우팅 toomultiple 인스턴스 요청 NginX 같은 다른 서버 프로세스와 함께에서 hello 레일 응용 프로그램을 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-166">Also, most production environments host hello Rails application in conjunction with another server process such as Apache or NginX, which handles request routing toomultiple instances of hello Rails application and serving static resources.</span></span> <span data-ttu-id="ae7ee-167">자세한 내용은 http://rubyonrails.org/deploy/를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-167">For more information, see http://rubyonrails.org/deploy/.</span></span>

<span data-ttu-id="ae7ee-168">Ruby 레일에에 대 한 자세한 정보는 toolearn 방문 hello [레일 가이드에 Ruby][rails-guides]합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-168">toolearn more about Ruby on Rails, visit hello [Ruby on Rails Guides][rails-guides].</span></span>

<span data-ttu-id="ae7ee-169">Ruby 응용 프로그램에서 toouse Azure 서비스를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ae7ee-169">toouse Azure services from your Ruby application, see:</span></span>

* <span data-ttu-id="ae7ee-170">[BLOB을 사용하여 구조화되지 않은 데이터 저장][blobs]</span><span class="sxs-lookup"><span data-stu-id="ae7ee-170">[Store unstructured data using blobs][blobs]</span></span>
* <span data-ttu-id="ae7ee-171">[테이블을 사용하여 키/값 쌍 저장][tables]</span><span class="sxs-lookup"><span data-stu-id="ae7ee-171">[Store key/value pairs using tables][tables]</span></span>
* <span data-ttu-id="ae7ee-172">[콘텐츠 배달 네트워크 hello로 고대역폭 콘텐츠를 제공 합니다.][cdn-howto]</span><span class="sxs-lookup"><span data-stu-id="ae7ee-172">[Serve high bandwidth content with hello Content Delivery Network][cdn-howto]</span></span>

<!-- WA.com links -->
[blobs]:../../../storage/blobs/storage-ruby-how-to-use-blob-storage.md
[cdn-howto]:https://azure.microsoft.com/develop/ruby/app-services/
[tables]:../../../cosmos-db/table-storage-how-to-use-ruby.md
[vm-instructions]:createportal.md

<!-- External Links -->
[rails-guides]:http://guides.rubyonrails.org/
[sqlite3]:http://www.sqlite.org/

<!-- Images -->

[default-rails-cloud]:./media/virtual-machines-linux-classic-ruby-rails-web-app/basicrailscloud.png
[vmlist]:./media/virtual-machines-linux-classic-ruby-rails-web-app/vmlist.png
[endpoints]:./media/virtual-machines-linux-classic-ruby-rails-web-app/endpoints.png
[new-endpoint]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint.png
[new-endpoint1]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint1.png
