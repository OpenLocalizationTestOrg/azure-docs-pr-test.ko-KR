---
title: "Linux VM에서 Ruby on Rails 웹 사이트 호스트 | Microsoft Docs"
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
ms.openlocfilehash: 0518519da6c5e62a863a47d6743ab7b7c5923acf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="ruby-on-rails-web-application-on-an-azure-vm"></a><span data-ttu-id="78836-103">Azure VM의 Ruby on Rails 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="78836-103">Ruby on Rails Web application on an Azure VM</span></span>
<span data-ttu-id="78836-104">이 자습서에서는 Azure에서 Linux 가상 컴퓨터를 사용하여 Ruby on Rails 웹 사이트를 호스트하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="78836-104">This tutorial shows how to host a Ruby on Rails website on Azure using a Linux virtual machine.</span></span>  

<span data-ttu-id="78836-105">이 자습서의 내용은 Ubuntu Server 14.04 LTS를 사용하여 유효성이 검사되었습니다.</span><span class="sxs-lookup"><span data-stu-id="78836-105">This tutorial was validated using Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="78836-106">다른 Linux 배포를 사용하는 경우, Rails를 설치하는 단계를 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78836-106">If you use a different Linux distribution, you might need to modify the steps to install Rails.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="78836-107">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78836-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="78836-108">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="78836-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="78836-109">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="78836-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
>
>

## <a name="create-an-azure-vm"></a><span data-ttu-id="78836-110">Azure VM 만들기</span><span class="sxs-lookup"><span data-stu-id="78836-110">Create an Azure VM</span></span>
<span data-ttu-id="78836-111">Linux 이미지와 Azure VM을 만들어 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="78836-111">Start by creating an Azure VM with a Linux image.</span></span>

<span data-ttu-id="78836-112">VM을 만들려면 Azure Portal 또는 Azure CLI(명령줄 인터페이스)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78836-112">To create the VM, you can use the Azure portal or the Azure Command-Line Interface (CLI).</span></span>

### <a name="azure-portal"></a><span data-ttu-id="78836-113">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="78836-113">Azure portal</span></span>
1. <span data-ttu-id="78836-114">[Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="78836-114">Sign into the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="78836-115">**새로 만들기**를 클릭한 다음 검색 상자에 "Ubuntu Server 14.04"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="78836-115">Click **New**, then type "Ubuntu Server 14.04" in the search box.</span></span> <span data-ttu-id="78836-116">검색에서 반환된 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78836-116">Click the entry returned by the search.</span></span> <span data-ttu-id="78836-117">배포 모델에서 **클래식**을 선택한 다음 "만들기"를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78836-117">For the deployment model, select **Classic**, then click "Create".</span></span>
3. <span data-ttu-id="78836-118">기본 블레이드에서 이름(VM), 사용자 이름, 인증 형식과 해당 자격 증명, Azure 구독, 리소스 그룹 및 위치와 같은 필수 필드에 대한 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="78836-118">In the Basics blade, supply values for the required fields: Name (for the VM), User name, Authentication type and the corresponding credentials, Azure subscription, Resource group, and Location.</span></span>

   ![새 Ubuntu 이미지 만들기](./media/virtual-machines-linux-classic-ruby-rails-web-app/createvm.png)

4. <span data-ttu-id="78836-120">VM을 프로비전한 후에 VM 이름을 클릭하고 **설정** 범주에서 **끝점**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78836-120">After the VM is provisioned, click on the VM name, and click **Endpoints** in the **Settings** category.</span></span> <span data-ttu-id="78836-121">**독립 실행형**에 나열된 SSH 끝점을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="78836-121">Find the SSH endpoint, listed under **Standalone**.</span></span>

   ![기본 끝점](./media/virtual-machines-linux-classic-ruby-rails-web-app/endpointsnewportal.png)

### <a name="azure-cli"></a><span data-ttu-id="78836-123">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="78836-123">Azure CLI</span></span>
<span data-ttu-id="78836-124">[Linux를 실행하는 가상 컴퓨터 만들기][vm-instructions]의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="78836-124">Follow the steps in [Create a Virtual Machine Running Linux][vm-instructions].</span></span>

<span data-ttu-id="78836-125">VM이 프로비전된 후, 다음 명령을 실행하여 SSH 끝점을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78836-125">After the VM is provisioned, you can get the SSH endpoint by running the following command:</span></span>

    azure vm endpoint list <vm-name>  

## <a name="install-ruby-on-rails"></a><span data-ttu-id="78836-126">Rails에 Ruby 설치</span><span class="sxs-lookup"><span data-stu-id="78836-126">Install Ruby on Rails</span></span>
1. <span data-ttu-id="78836-127">SSH를 사용하여 VM에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="78836-127">Use SSH to connect to the VM.</span></span>
2. <span data-ttu-id="78836-128">SSH 세션에서 다음 명령을 사용하여 VM에 Ruby를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="78836-128">From the SSH session, use the following commands to install Ruby on the VM:</span></span>

        sudo apt-get update -y
        sudo apt-get upgrade -y

        sudo apt-add-repository ppa:brightbox/ruby-ng
        sudo apt-get update
        sudo apt-get install ruby2.4

        > [!TIP]
        > The brightbox repository contains the current Ruby distribution.

    <span data-ttu-id="78836-129">설치는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78836-129">The installation may take a few minutes.</span></span> <span data-ttu-id="78836-130">완료되면 다음 명령을 사용하여 Ruby가 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="78836-130">When it completes, use the following command to verify that Ruby is installed:</span></span>

        ruby -v

3. <span data-ttu-id="78836-131">다음 명령을 사용하여 Rails를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="78836-131">Use the following command to install Rails:</span></span>

        sudo gem install rails --no-rdoc --no-ri -V

    <span data-ttu-id="78836-132">--no-rdoc 및 --no-ri 플래그를 사용하여 설명서 설치를 건너뜁니다. 이 방법이 더 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="78836-132">Use the --no-rdoc and --no-ri flags to skip installing the documentation, which is faster.</span></span>
    <span data-ttu-id="78836-133">이 명령을 실행하려면 시간이 오래 걸릴 수 있으니 –V를 추가하여 설치 프로세스에 대한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="78836-133">This command will likely take a long time to execute, so adding the -V will display information about the installation progress.</span></span>

## <a name="create-and-run-an-app"></a><span data-ttu-id="78836-134">앱 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="78836-134">Create and run an app</span></span>
<span data-ttu-id="78836-135">SSH를 통해 로그인한 경우.다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="78836-135">While still logged in via SSH, run the following commands:</span></span>

    rails new myapp
    cd myapp
    rails server -b 0.0.0.0 -p 3000

<span data-ttu-id="78836-136">[새](http://guides.rubyonrails.org/command_line.html#rails-new) 명령은 새 Rails 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="78836-136">The [new](http://guides.rubyonrails.org/command_line.html#rails-new) command creates a new Rails app.</span></span> <span data-ttu-id="78836-137">[서버](http://guides.rubyonrails.org/command_line.html#rails-server) 명령은 Rails와 함께 제공되는 WEBrick 웹 서버를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="78836-137">The [server](http://guides.rubyonrails.org/command_line.html#rails-server) command starts the WEBrick web server that comes with Rails.</span></span> <span data-ttu-id="78836-138">(프로덕션에서 사용하기 위해, 유니콘 또는 승객과 같은 다른 서버를 사용할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="78836-138">(For production use, you would probably want to use a different server, such as Unicorn or Passenger.)</span></span>

<span data-ttu-id="78836-139">다음과 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="78836-139">You should see output similar to the following.</span></span>

    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://0.0.0.0:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C to shutdown server
    [2015-06-09 23:34:23] INFO  WEBrick 1.3.1
    [2015-06-09 23:34:23] INFO  ruby 1.9.3 (2013-11-22) [x86_64-linux]
    [2015-06-09 23:34:23] INFO  WEBrick::HTTPServer#start: pid=27766 port=3000

## <a name="add-an-endpoint"></a><span data-ttu-id="78836-140">끝점 추가</span><span class="sxs-lookup"><span data-stu-id="78836-140">Add an endpoint</span></span>
1. <span data-ttu-id="78836-141">[Azure Portal] [https://portal.azure.com] 로 이동하고 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78836-141">Go to the [Azure portal][https://portal.azure.com] and select your VM.</span></span>

2. <span data-ttu-id="78836-142">페이지의 왼쪽 가장자리에 있는 **설정**에서 **끝점**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78836-142">Select **ENDPOINTS** in the **Settings** along the left edge the page.</span></span>

3. <span data-ttu-id="78836-143">페이지 위쪽에서 **ADD**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78836-143">Click **ADD** at the top of the page.</span></span>

4. <span data-ttu-id="78836-144">**끝점 추가** 대화 페이지에서 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="78836-144">In the **Add endpoint** dialog page, enter the following information:</span></span>

   * <span data-ttu-id="78836-145">**이름**: HTTP</span><span class="sxs-lookup"><span data-stu-id="78836-145">**Name**: HTTP</span></span>
   * <span data-ttu-id="78836-146">**프로토콜**: - TCP</span><span class="sxs-lookup"><span data-stu-id="78836-146">**Protocol**: TCP</span></span>
   * <span data-ttu-id="78836-147">**공용 포트**: 80</span><span class="sxs-lookup"><span data-stu-id="78836-147">**Public port**: 80</span></span>
   * <span data-ttu-id="78836-148">**개인 포트**: 3000</span><span class="sxs-lookup"><span data-stu-id="78836-148">**Private port**: 3000</span></span>
   * <span data-ttu-id="78836-149">**부동 PI 주소**: 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="78836-149">**Floating PI address**: Disabled</span></span>
   * <span data-ttu-id="78836-150">**액세스 제어 목록 - 순서**: 1001 또는 액세스 규칙의 우선 순위를 설정하는 다른 값</span><span class="sxs-lookup"><span data-stu-id="78836-150">**Access control list - Order**: 1001, or another value that sets the priority of this access rule.</span></span>
   * <span data-ttu-id="78836-151">**액세스 제어 목록 - 이름**: allowHTTP</span><span class="sxs-lookup"><span data-stu-id="78836-151">**Access control list - Name**: allowHTTP</span></span>
   * <span data-ttu-id="78836-152">**액세스 제어 목록 - 작업**: 허용</span><span class="sxs-lookup"><span data-stu-id="78836-152">**Access control list - Action**: permit</span></span>
   * <span data-ttu-id="78836-153">**액세스 제어 목록 - 원격 서브넷**: 1.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="78836-153">**Access control list - Remote subnet**: 1.0.0.0/16</span></span>

     <span data-ttu-id="78836-154">이 끝점에는 트래픽을 개인 포트 3000으로 라우팅하는 공용 포트 80이 있고 여기서 Rails 서버가 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="78836-154">This endpoint  has a public port of 80 that will route traffic to the private port of 3000, where the Rails server is listening.</span></span> <span data-ttu-id="78836-155">액세스 제어 목록 규칙은 포트 80에서 공용 트래픽을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="78836-155">The access control list rule allows public traffic on port 80.</span></span>

     ![new-endpoint](./media/virtual-machines-linux-classic-ruby-rails-web-app/createendpoint.png)

5. <span data-ttu-id="78836-157">확인을 클릭하여 끝점을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="78836-157">Click OK to save the endpoint.</span></span>

6. <span data-ttu-id="78836-158">메시지가 **가상 컴퓨터 끝점 저장**을 표시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78836-158">A message should appear that states **Saving virtual machine endpoint**.</span></span> <span data-ttu-id="78836-159">이 메시지가 사라지면 끝점이 활성 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="78836-159">Once this message disappears, the endpoint is active.</span></span> <span data-ttu-id="78836-160">이제 가상 컴퓨터의 DNS 이름으로 이동하여 응용 프로그램을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78836-160">You may now test your application by navigating to the DNS name of your virtual machine.</span></span> <span data-ttu-id="78836-161">웹 사이트는 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="78836-161">The website should appear similar to the following:</span></span>

    ![기본 Rails 페이지][default-rails-cloud]

## <a name="next-steps"></a><span data-ttu-id="78836-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="78836-163">Next steps</span></span>
<span data-ttu-id="78836-164">이 자습서에서는 수동으로 대부분의 단계를 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="78836-164">In this tutorial, you did most of the steps manually.</span></span> <span data-ttu-id="78836-165">프로덕션 환경의 개발 컴퓨터에 앱을 작성하고 Azure VM에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="78836-165">In a production environment, you would write your app on a development machine and deploy it to the Azure VM.</span></span> <span data-ttu-id="78836-166">또한 대부분의 프로덕션 환경은 Rails 응용 프로그램을 다른 서버 프로세스(예: Apache 또는 NginX)와 함께 호스트하며 이러한 서버 프로세스는 Rails 응용 프로그램의 여러 인스턴스로 라우팅하여 정적 리소스를 제공하는 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="78836-166">Also, most production environments host the Rails application in conjunction with another server process such as Apache or NginX, which handles request routing to multiple instances of the Rails application and serving static resources.</span></span> <span data-ttu-id="78836-167">자세한 내용은 http://rubyonrails.org/deploy/를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="78836-167">For more information, see http://rubyonrails.org/deploy/.</span></span>

<span data-ttu-id="78836-168">Ruby on Rails에 대해 자세히 알아보려면 [Ruby on Rails 가이드][rails-guides](영문)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="78836-168">To learn more about Ruby on Rails, visit the [Ruby on Rails Guides][rails-guides].</span></span>

<span data-ttu-id="78836-169">Ruby 응용 프로그램에서 Azure 서비스를 사용하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="78836-169">To use Azure services from your Ruby application, see:</span></span>

* <span data-ttu-id="78836-170">[BLOB을 사용하여 구조화되지 않은 데이터 저장][blobs]</span><span class="sxs-lookup"><span data-stu-id="78836-170">[Store unstructured data using blobs][blobs]</span></span>
* <span data-ttu-id="78836-171">[테이블을 사용하여 키/값 쌍 저장][tables]</span><span class="sxs-lookup"><span data-stu-id="78836-171">[Store key/value pairs using tables][tables]</span></span>
* <span data-ttu-id="78836-172">[Content Delivery Network로 높은 대역폭 콘텐츠 제공][cdn-howto]</span><span class="sxs-lookup"><span data-stu-id="78836-172">[Serve high bandwidth content with the Content Delivery Network][cdn-howto]</span></span>

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
