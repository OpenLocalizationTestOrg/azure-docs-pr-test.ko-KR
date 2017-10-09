---
title: "aaaDeploy 프로그램 첫 번째 앱 tooCloud Microsoft Azure에서 대장간 | Microsoft Docs"
description: "응용 프로그램 tooCloud 대장간 Azure에서 배포"
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 8fa04a58-56ad-4e6c-bef4-d02c80d4b60f
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: seanmck
ms.openlocfilehash: 878da38f6eabe32a339f02aa0ead811d6e5af9a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-first-app-toocloud-foundry-on-microsoft-azure"></a><span data-ttu-id="b74dc-103">Microsoft Azure에서 대장간 첫 번째 앱 tooCloud 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="b74dc-103">Deploy your first app tooCloud Foundry on Microsoft Azure</span></span>

<span data-ttu-id="b74dc-104">[Cloud Foundry](http://cloudfoundry.org)는 Microsoft Azure에서 사용할 수 있는 인기 있는 오픈 소스 응용 프로그램 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-104">[Cloud Foundry](http://cloudfoundry.org) is a popular open-source application platform available on Microsoft Azure.</span></span> <span data-ttu-id="b74dc-105">이 문서에서는 보여줍니다 어떻게 toodeploy 및 Azure 환경에서 클라우드 대장간에서 응용 프로그램을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-105">In this article, we show how toodeploy and manage an application on Cloud Foundry in an Azure environment.</span></span>

## <a name="create-a-cloud-foundry-environment"></a><span data-ttu-id="b74dc-106">Cloud Foundry 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="b74dc-106">Create a Cloud Foundry environment</span></span>

<span data-ttu-id="b74dc-107">Azure에 Cloud Foundry 환경을 만들기 위한 여러 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-107">There are several options for creating a Cloud Foundry environment on Azure:</span></span>

- <span data-ttu-id="b74dc-108">사용 하 여 hello [중요 클라우드 대장간 제안] [ pcf-azuremarketplace] hello Azure 마켓플레이스 toocreate PCF Ops Manager 및 Service Broker Azure hello를 포함 하는 표준 환경에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-108">Use hello [Pivotal Cloud Foundry offer][pcf-azuremarketplace] in hello Azure Marketplace toocreate a standard environment that includes PCF Ops Manager and hello Azure Service Broker.</span></span> <span data-ttu-id="b74dc-109">찾을 수 있습니다 [지침을 완료] [ pcf-azuremarketplace-pivotaldocs] hello 마켓플레이스를 배포 하기 위한 hello 중요 설명서에에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-109">You can find [complete instructions][pcf-azuremarketplace-pivotaldocs] for deploying hello marketplace offer in hello Pivotal documentation.</span></span>
- <span data-ttu-id="b74dc-110">[Pivotal Cloud Foundry를 수동으로 배포][pcf-custom]하여 사용자 지정된 환경을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-110">Create a customized environment by [deploying Pivotal Cloud Foundry manually][pcf-custom].</span></span>
- <span data-ttu-id="b74dc-111">[Hello 오픈 소스 클라우드 대장간 패키지를 직접 배포] [ oss-cf-bosh] 를 설정 하 여 한 [BOSH](http://bosh.io) hello 클라우드 대장간 환경의 hello 배포를 조정 하는 VM 감독 합니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-111">[Deploy hello open-source Cloud Foundry packages directly][oss-cf-bosh] by setting up a [BOSH](http://bosh.io) director, a VM that coordinates hello deployment of hello Cloud Foundry environment.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="b74dc-112">Hello Azure Marketplace에서에서 PCF를 배포 하는 경우 hello SYSTEMDOMAINURL 메모 및 tooaccess hello hello 마켓플레이스 배포 가이드에 설명 되어 있는 중요 응용 프로그램 관리자 hello 관리자 자격 증명이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-112">If you are deploying PCF from hello Azure Marketplace, make a note of hello SYSTEMDOMAINURL and hello admin credentials required tooaccess hello Pivotal Apps Manager, both of which are described in hello marketplace deployment guide.</span></span> <span data-ttu-id="b74dc-113">이 자습서에서는 필요한 toocomplete 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-113">They are needed toocomplete this tutorial.</span></span> <span data-ttu-id="b74dc-114">마켓플레이스 배포 hello SYSTEMDOMAINURL hello 양식 https://system가 있습니다. *ip 주소*. cf.pcfazure.com 합니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-114">For marketplace deployments, hello SYSTEMDOMAINURL is in hello form https://system.*ip-address*.cf.pcfazure.com.</span></span>

## <a name="connect-toohello-cloud-controller"></a><span data-ttu-id="b74dc-115">Toohello 클라우드 컨트롤러를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-115">Connect toohello Cloud Controller</span></span>

<span data-ttu-id="b74dc-116">hello 클라우드 컨트롤러는 배포 하 고 응용 프로그램 관리에 대 한 hello 대 한 주 진입점 지점 tooa 클라우드 대장간 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-116">hello Cloud Controller is hello primary entry point tooa Cloud Foundry environment for deploying and managing applications.</span></span> <span data-ttu-id="b74dc-117">hello 코어 클라우드 컨트롤러 API (CCAPI)는 REST API, 이지만 다양 한 도구를 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-117">hello core Cloud Controller API (CCAPI) is a REST API, but it is accessible through various tools.</span></span> <span data-ttu-id="b74dc-118">Hello를 통해 상호 작용 우리는 경우 [클라우드 대장간 CLI][cf-cli]합니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-118">In this case, we interact with it through hello [Cloud Foundry CLI][cf-cli].</span></span> <span data-ttu-id="b74dc-119">Windows, Linux, MacOS 등 또는에 hello CLI를 설치할 수 있지만 것도 가능 하다 hello에 미리 설치 된 tooinstall 하지 않으려면 [Azure 클라우드 셸][cloudshell-docs]합니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-119">You can install hello CLI on Linux, MacOS, or Windows, but if you'd prefer not tooinstall it at all, it is available pre-installed in hello [Azure Cloud Shell][cloudshell-docs].</span></span>

<span data-ttu-id="b74dc-120">앞에 추가 되는, toolog `api` toohello hello 마켓플레이스 배포에서 얻은 SYSTEMDOMAINURL 합니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-120">toolog in, prepend `api` toohello SYSTEMDOMAINURL that you obtained from hello marketplace deployment.</span></span> <span data-ttu-id="b74dc-121">Hello도 포함 해야 hello 기본 배포는 자체 서명 된 인증서를 사용 하므로 `skip-ssl-validation` 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-121">Since hello default deployment uses a self-signed certificate, you should also include hello `skip-ssl-validation` switch.</span></span>

```bash
cf login -a https://api.SYSTEMDOMAINURL --skip-ssl-validation
```

<span data-ttu-id="b74dc-122">Toohello 클라우드 컨트롤러에에서 증명된 toolog 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-122">You are prompted toolog in toohello Cloud Controller.</span></span> <span data-ttu-id="b74dc-123">Hello 마켓플레이스 배포 단계에서 복사한 hello 관리자 계정 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-123">Use hello admin account credentials that you acquired from hello marketplace deployment steps.</span></span>

<span data-ttu-id="b74dc-124">클라우드 대장간 제공 *조직* 및 *공간* 네임 스페이스 tooisolate hello 팀과 공유 배포 내에서 환경으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-124">Cloud Foundry provides *orgs* and *spaces* as namespaces tooisolate hello teams and environments within a shared deployment.</span></span> <span data-ttu-id="b74dc-125">hello PCF 마켓플레이스 배포 포함 hello 기본 *시스템* org 및 공백 집합 toocontain 같은 hello 자동 크기 조정 서비스 및 hello Azure service broker의 hello 기본 구성 요소를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-125">hello PCF marketplace deployment includes hello default *system* org and a set of spaces created toocontain hello base components, like hello autoscaling service and hello Azure service broker.</span></span> <span data-ttu-id="b74dc-126">지금은 hello 선택 *시스템* 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-126">For now, choose hello *system* space.</span></span>


## <a name="create-an-org-and-space"></a><span data-ttu-id="b74dc-127">조직 및 공간 만들기</span><span class="sxs-lookup"><span data-stu-id="b74dc-127">Create an org and space</span></span>

<span data-ttu-id="b74dc-128">입력 하는 경우 `cf apps`, hello 시스템 조직 내에서 hello 시스템 공간에 배포 된 시스템 응용 프로그램 집합 표시</span><span class="sxs-lookup"><span data-stu-id="b74dc-128">If you type `cf apps`, you see a set of system applications that have been deployed in hello system space within hello system org.</span></span> 

<span data-ttu-id="b74dc-129">Hello를 유지 해야 *시스템* 시스템 응용 프로그램에 대 한 예약 org 만드세요 org 및 공간 toohouse 샘플 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-129">You should keep hello *system* org reserved for system applications, so create an org and space toohouse our sample application.</span></span>

```bash
cf create-org myorg
cf create-space dev -o myorg
```

<span data-ttu-id="b74dc-130">Hello 대상 명령 tooswitch toohello 새 조직 및 공간을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-130">Use hello target command tooswitch toohello new org and space:</span></span>

```bash
cf target -o testorg -s dev
```

<span data-ttu-id="b74dc-131">이제 응용 프로그램을 배포 하면 hello 새 조직 및 공간에서 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-131">Now, when you deploy an application, it is automatically created in hello new org and space.</span></span> <span data-ttu-id="b74dc-132">현재 tooconfirm hello 새 org/공간에 앱이 없습니다. 입력 `cf apps` 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-132">tooconfirm that there are currently no apps in hello new org/space, type `cf apps` again.</span></span>

> [!NOTE] 
> <span data-ttu-id="b74dc-133">조직 및 공백 및 역할 기반 액세스 제어 (RBAC)에 사용할 수 있습니다 어떻게 하는 방법에 대 한 자세한 내용은 참조 hello [클라우드 대장간 설명서][cf-orgs-spaces-docs]합니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-133">For more information about orgs and spaces and how they can be used for role-based access control (RBAC), see hello [Cloud Foundry documentation][cf-orgs-spaces-docs].</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="b74dc-134">응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="b74dc-134">Deploy an application</span></span>

<span data-ttu-id="b74dc-135">Java로 작성 되 고 hello에 따라 Hello ' 봄 ' 클라우드를 호출 하는 샘플 클라우드 대장간 응용 프로그램 사용 [Spring Framework](http://spring.io) 및 [스프링 부팅](http://projects.spring.io/spring-boot/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-135">Let's use a sample Cloud Foundry application called Hello Spring Cloud, which is written in Java and based on hello [Spring Framework](http://spring.io) and [Spring Boot](http://projects.spring.io/spring-boot/).</span></span>

### <a name="clone-hello-hello-spring-cloud-repository"></a><span data-ttu-id="b74dc-136">Hello Hello 스프링 클라우드 리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="b74dc-136">Clone hello Hello Spring Cloud repository</span></span>

<span data-ttu-id="b74dc-137">hello Hello 스프링 클라우드 샘플 응용 프로그램은 GitHub에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-137">hello Hello Spring Cloud sample application is available on GitHub.</span></span> <span data-ttu-id="b74dc-138">Tooyour 환경을 복제 하 고 hello 새 디렉터리로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-138">Clone it tooyour environment and change into hello new directory:</span></span>

```bash
git clone https://github.com/cloudfoundry-samples/hello-spring-cloud
cd hello-spring-cloud
```

### <a name="build-hello-application"></a><span data-ttu-id="b74dc-139">Hello 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="b74dc-139">Build hello application</span></span>

<span data-ttu-id="b74dc-140">사용 하 여 빌드 hello 앱 [Apache Maven](http://maven.apache.org)합니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-140">Build hello app using [Apache Maven](http://maven.apache.org).</span></span>

```bash
mvn clean package
```

### <a name="deploy-hello-application-with-cf-push"></a><span data-ttu-id="b74dc-141">Cf 푸시를 통한 hello 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="b74dc-141">Deploy hello application with cf push</span></span>

<span data-ttu-id="b74dc-142">대부분 응용 프로그램 tooCloud 대장간을 배포할 수 있습니다 hello를 사용 하 여 `push` 명령:</span><span class="sxs-lookup"><span data-stu-id="b74dc-142">You can deploy most applications tooCloud Foundry using hello `push` command:</span></span>

```bash
cf push
```

<span data-ttu-id="b74dc-143">때 있습니다 *푸시* 응용 프로그램을 클라우드 대장간 hello 유형의 응용 프로그램 (이 경우 Java 응용 프로그램에서)를 검색 하 고 해당 종속성 (이 경우 hello Spring framework)을에서 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-143">When you *push* an application, Cloud Foundry detects hello type of application (in this case, a Java app) and identifies its dependencies (in this case, hello Spring framework).</span></span> <span data-ttu-id="b74dc-144">다음 패키지 모든 toorun 코드 라고 하는 독립 실행형 컨테이너 이미지에 필요한는 *드롭릿*합니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-144">It then packages everything required toorun your code into a standalone container image, known as a *droplet*.</span></span> <span data-ttu-id="b74dc-145">마지막으로, 클라우드 대장간 일정 hello 사용자 환경에서 사용할 수 있는 컴퓨터 중 하나에서 응용 프로그램 hello 및 위치에 도달할 수, hello 명령의 hello 출력에서 제공 되는 URL을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-145">Finally, Cloud Foundry schedules hello application on one of hello available machines in your environment and creates a URL where you can reach it, which is available in hello output of hello command.</span></span>

![cf 밀어넣기 명령의 출력][cf-push-output]

<span data-ttu-id="b74dc-147">toosee hello hello 스프링 클라우드 응용 프로그램을 브라우저에서 제공 하는 개방형 hello URL:</span><span class="sxs-lookup"><span data-stu-id="b74dc-147">toosee hello hello-spring-cloud application, open hello provided URL in your browser:</span></span>

![Hello Spring Cloud용 기본 UI][hello-spring-cloud-basic]

> [!NOTE] 
> <span data-ttu-id="b74dc-149">toolearn 처리 과정에 대 한 자세한 `cf push`, 참조 [응용 프로그램 준비 된] [ cf-push-docs] hello 클라우드 대장간 설명서에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-149">toolearn more about what happens during `cf push`, see [How Applications Are Staged][cf-push-docs] in hello Cloud Foundry documentation.</span></span>

## <a name="view-application-logs"></a><span data-ttu-id="b74dc-150">응용 프로그램 로그 보기</span><span class="sxs-lookup"><span data-stu-id="b74dc-150">View application logs</span></span>

<span data-ttu-id="b74dc-151">이름을 사용 하 여 응용 프로그램에 대 한 hello 클라우드 대장간 CLI tooview 로그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-151">You can use hello Cloud Foundry CLI tooview logs for an application by its name:</span></span>

```bash
cf logs hello-spring-cloud
```

<span data-ttu-id="b74dc-152">기본적으로 hello 로깅합니다 명령을 사용 하 여 *꼬리*, 작성 된 대로 새 로그를 보여 주는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-152">By default, hello logs command uses *tail*, which shows new logs as they are written.</span></span> <span data-ttu-id="b74dc-153">toosee 새 로그 표시 hello 브라우저에서 hello hello 스프링 클라우드 앱을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-153">toosee new logs appear, refresh hello hello-spring-cloud app in hello browser.</span></span>

<span data-ttu-id="b74dc-154">이미 작성 tooview 로그 추가 hello `recent` 전환:</span><span class="sxs-lookup"><span data-stu-id="b74dc-154">tooview logs that have already been written, add hello `recent` switch:</span></span>

```bash
cf logs --recent hello-spring-cloud
```

## <a name="scale-hello-application"></a><span data-ttu-id="b74dc-155">배율 hello 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="b74dc-155">Scale hello application</span></span>

<span data-ttu-id="b74dc-156">기본적으로 `cf push`만 응용 프로그램의 단일 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-156">By default, `cf push` only creates a single instance of your application.</span></span> <span data-ttu-id="b74dc-157">tooensure 고가용성 및 높은 처리량을 위한 확장 가능 응용 프로그램의 인스턴스가 둘 이상 toorun 일반적으로 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-157">tooensure high availability and enable scale out for higher throughput, you generally want toorun more than one instance of your applications.</span></span> <span data-ttu-id="b74dc-158">Hello를 사용 하 여 이미 배포 된 응용 프로그램을 쉽게 확장할 수 있습니다 `scale` 명령:</span><span class="sxs-lookup"><span data-stu-id="b74dc-158">You can easily scale out already deployed applications using hello `scale` command:</span></span>

```bash
cf scale -i 2 hello-spring-cloud
```

<span data-ttu-id="b74dc-159">실행 중인 hello `cf app` 명령 hello 응용 프로그램에 클라우드 대장간은 hello 응용 프로그램의 다른 인스턴스를 만드는 것을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-159">Running hello `cf app` command on hello application shows that Cloud Foundry is creating another instance of hello application.</span></span> <span data-ttu-id="b74dc-160">Hello 응용 프로그램 시작 된 후 클라우드 대장간 부하 분산 트래픽 tooit를 자동으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b74dc-160">Once hello application has started, Cloud Foundry automatically starts load balancing traffic tooit.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b74dc-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b74dc-161">Next steps</span></span>

- <span data-ttu-id="b74dc-162">[읽기 hello 클라우드 대장간 설명서][cloudfoundry-docs]</span><span class="sxs-lookup"><span data-stu-id="b74dc-162">[Read hello Cloud Foundry documentation][cloudfoundry-docs]</span></span>
- <span data-ttu-id="b74dc-163">[클라우드 대장간에 대 한 hello Visual Studio Team Services 플러그 인을 설정 합니다.][vsts-plugin]</span><span class="sxs-lookup"><span data-stu-id="b74dc-163">[Set up hello Visual Studio Team Services plugin for Cloud Foundry][vsts-plugin]</span></span>
- <span data-ttu-id="b74dc-164">[클라우드 대장간에 대 한 로그 분석 노즐 Microsoft hello를 구성 합니다.][loganalytics-nozzle]</span><span class="sxs-lookup"><span data-stu-id="b74dc-164">[Configure hello Microsoft Log Analytics Nozzle for Cloud Foundry][loganalytics-nozzle]</span></span>

<!-- LINKS -->

[pcf-azuremarketplace]: https://azuremarketplace.microsoft.com/marketplace/apps/pivotal.pivotal-cloud-foundry
[pcf-custom]: https://docs.pivotal.io/pivotalcf/1-10/customizing/azure.html
[oss-cf-bosh]: https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/tree/master/docs
[pcf-azuremarketplace-pivotaldocs]: https://docs.pivotal.io/pivotalcf/customizing/pcf_azure.html
[cf-cli]: https://github.com/cloudfoundry/cli
[cloudshell-docs]: https://docs.microsoft.com/azure/cloud-shell/overview
[cf-orgs-spaces-docs]: https://docs.cloudfoundry.org/concepts/roles.html
[spring-boot]: https://projects.spring.io/spring-boot/
[spring-framework]: http://spring.io
[cf-push-docs]: https://docs.cloudfoundry.org/concepts/how-applications-are-staged.html
[cloudfoundry-docs]: https://docs.cloudfoundry.org
[vsts-plugin]: https://github.com/Microsoft/vsts-cloudfoundry
[loganalytics-nozzle]: https://github.com/Azure/oms-log-analytics-firehose-nozzle

<!-- IMAGES -->
[cf-push-output]: ./media/cloudfoundry-deploy-your-first-app/cf-push-output.png
[hello-spring-cloud-basic]: ./media/cloudfoundry-deploy-your-first-app/hello-spring-cloud-basic.png