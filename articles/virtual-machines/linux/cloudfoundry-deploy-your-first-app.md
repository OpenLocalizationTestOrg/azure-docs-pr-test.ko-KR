---
title: "Microsoft Azure의 Cloud Foundry에 첫 번째 앱 배포 | Microsoft Docs"
description: "Azure의 Cloud Foundry에 응용 프로그램 배포"
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
ms.openlocfilehash: b617127fc0a3f8dcae293e356ea669edcfa5deff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-your-first-app-to-cloud-foundry-on-microsoft-azure"></a><span data-ttu-id="beda8-103">Microsoft Azure의 Cloud Foundry에 첫 번째 앱 배포</span><span class="sxs-lookup"><span data-stu-id="beda8-103">Deploy your first app to Cloud Foundry on Microsoft Azure</span></span>

<span data-ttu-id="beda8-104">[Cloud Foundry](http://cloudfoundry.org)는 Microsoft Azure에서 사용할 수 있는 인기 있는 오픈 소스 응용 프로그램 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-104">[Cloud Foundry](http://cloudfoundry.org) is a popular open-source application platform available on Microsoft Azure.</span></span> <span data-ttu-id="beda8-105">이 문서에서는 Azure 환경에서 Cloud Foundry의 응용 프로그램을 배포 및 관리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-105">In this article, we show how to deploy and manage an application on Cloud Foundry in an Azure environment.</span></span>

## <a name="create-a-cloud-foundry-environment"></a><span data-ttu-id="beda8-106">Cloud Foundry 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="beda8-106">Create a Cloud Foundry environment</span></span>

<span data-ttu-id="beda8-107">Azure에 Cloud Foundry 환경을 만들기 위한 여러 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-107">There are several options for creating a Cloud Foundry environment on Azure:</span></span>

- <span data-ttu-id="beda8-108">Azure Marketplace에서 [Pivotal Cloud Foundry 제품][pcf-azuremarketplace]을 사용하여 PCF Ops Manager 및 Azure Service Broker를 포함하는 표준 환경을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-108">Use the [Pivotal Cloud Foundry offer][pcf-azuremarketplace] in the Azure Marketplace to create a standard environment that includes PCF Ops Manager and the Azure Service Broker.</span></span> <span data-ttu-id="beda8-109">Pivotal 설명서에서 마켓플레이스 제품을 배포하기 위한 [전체 지침][pcf-azuremarketplace-pivotaldocs]을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-109">You can find [complete instructions][pcf-azuremarketplace-pivotaldocs] for deploying the marketplace offer in the Pivotal documentation.</span></span>
- <span data-ttu-id="beda8-110">[Pivotal Cloud Foundry를 수동으로 배포][pcf-custom]하여 사용자 지정된 환경을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-110">Create a customized environment by [deploying Pivotal Cloud Foundry manually][pcf-custom].</span></span>
- <span data-ttu-id="beda8-111">[BOSH](http://bosh.io) 디렉터, Cloud Foundry 환경의 배포를 조정하는 VM을 설정하여 [오픈 소스 Cloud Foundry 패키지를 직접 배포][oss-cf-bosh]합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-111">[Deploy the open-source Cloud Foundry packages directly][oss-cf-bosh] by setting up a [BOSH](http://bosh.io) director, a VM that coordinates the deployment of the Cloud Foundry environment.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="beda8-112">Azure Marketplace에서 PCF를 배포하는 경우 Pivotal 앱 관리자에 액세스하는 데 필요한 SYSTEMDOMAINURL 및 관리자 자격 증명을 적어 둡니다. 둘은 마켓플레이스 배포 가이드에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-112">If you are deploying PCF from the Azure Marketplace, make a note of the SYSTEMDOMAINURL and the admin credentials required to access the Pivotal Apps Manager, both of which are described in the marketplace deployment guide.</span></span> <span data-ttu-id="beda8-113">이 자습서를 완료하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-113">They are needed to complete this tutorial.</span></span> <span data-ttu-id="beda8-114">마켓플레이스 배포의 경우 SYSTEMDOMAINURL은 https://system.*ip-address*.cf.pcfazure.com 양식입니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-114">For marketplace deployments, the SYSTEMDOMAINURL is in the form https://system.*ip-address*.cf.pcfazure.com.</span></span>

## <a name="connect-to-the-cloud-controller"></a><span data-ttu-id="beda8-115">Cloud Controller에 연결</span><span class="sxs-lookup"><span data-stu-id="beda8-115">Connect to the Cloud Controller</span></span>

<span data-ttu-id="beda8-116">Cloud Controller는 응용 프로그램 배포 및 관리를 위한 Cloud Foundry 환경에 대한 기본 진입점입니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-116">The Cloud Controller is the primary entry point to a Cloud Foundry environment for deploying and managing applications.</span></span> <span data-ttu-id="beda8-117">핵심 CCAPI(Cloud Controller API)는 REST API이지만 다양한 도구를 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-117">The core Cloud Controller API (CCAPI) is a REST API, but it is accessible through various tools.</span></span> <span data-ttu-id="beda8-118">이 경우 [Cloud Foundry CLI][cf-cli]를 통해 상호 작용합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-118">In this case, we interact with it through the [Cloud Foundry CLI][cf-cli].</span></span> <span data-ttu-id="beda8-119">Linux, MacOS 또는 Windows에 CLI를 설치할 수 있지만 전혀 설치하지 않으려는 경우 [Azure Cloud Shell][cloudshell-docs]에 사전 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-119">You can install the CLI on Linux, MacOS, or Windows, but if you'd prefer not to install it at all, it is available pre-installed in the [Azure Cloud Shell][cloudshell-docs].</span></span>

<span data-ttu-id="beda8-120">로그인하려면 마켓플레이스 배포에서 가져온 SYSTEMDOMAINURL 앞에 `api`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-120">To log in, prepend `api` to the SYSTEMDOMAINURL that you obtained from the marketplace deployment.</span></span> <span data-ttu-id="beda8-121">기본 배포는 자체 서명된 인증서를 사용하므로 `skip-ssl-validation` 스위치를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-121">Since the default deployment uses a self-signed certificate, you should also include the `skip-ssl-validation` switch.</span></span>

```bash
cf login -a https://api.SYSTEMDOMAINURL --skip-ssl-validation
```

<span data-ttu-id="beda8-122">Cloud Controller에 로그인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-122">You are prompted to log in to the Cloud Controller.</span></span> <span data-ttu-id="beda8-123">마켓플레이스 배포 단계에서 얻은 관리자 계정 자격 증명을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-123">Use the admin account credentials that you acquired from the marketplace deployment steps.</span></span>

<span data-ttu-id="beda8-124">Cloud Foundry는 네임스페이스로 *조직* 및 *공간*을 제공하여 공유 배포 내에서 팀과 환경을 격리합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-124">Cloud Foundry provides *orgs* and *spaces* as namespaces to isolate the teams and environments within a shared deployment.</span></span> <span data-ttu-id="beda8-125">PCF 마켓플레이스 배포는 기본 *시스템* 조직 및 자동 크기 조정 서비스 및 Azure Service Broker와 같은 기본 구성 요소를 포함하도록 만들어진 공간 집합을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-125">The PCF marketplace deployment includes the default *system* org and a set of spaces created to contain the base components, like the autoscaling service and the Azure service broker.</span></span> <span data-ttu-id="beda8-126">현재로는 *시스템* 공간을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-126">For now, choose the *system* space.</span></span>


## <a name="create-an-org-and-space"></a><span data-ttu-id="beda8-127">조직 및 공간 만들기</span><span class="sxs-lookup"><span data-stu-id="beda8-127">Create an org and space</span></span>

<span data-ttu-id="beda8-128">`cf apps`를 입력하는 경우 시스템 조직 내에서 시스템 공간에 배포된 시스템 응용 프로그램 집합이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-128">If you type `cf apps`, you see a set of system applications that have been deployed in the system space within the system org.</span></span> 

<span data-ttu-id="beda8-129">조직 및 공간을 만들어 샘플 응용 프로그램을 저장하도록 시스템 응용 프로그램에 대해 예약된 *시스템* 조직을 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-129">You should keep the *system* org reserved for system applications, so create an org and space to house our sample application.</span></span>

```bash
cf create-org myorg
cf create-space dev -o myorg
```

<span data-ttu-id="beda8-130">대상 명령을 사용하여 새 조직 및 공간으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-130">Use the target command to switch to the new org and space:</span></span>

```bash
cf target -o testorg -s dev
```

<span data-ttu-id="beda8-131">이제 응용 프로그램을 배포할 때 새 조직 및 공간에 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-131">Now, when you deploy an application, it is automatically created in the new org and space.</span></span> <span data-ttu-id="beda8-132">현재 새 조직/공간에 앱이 없는지 확인하려면 `cf apps`를 다시 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-132">To confirm that there are currently no apps in the new org/space, type `cf apps` again.</span></span>

> [!NOTE] 
> <span data-ttu-id="beda8-133">조직과 공간 및 RBAC(역할 기반 액세스 제어)에 사용할 수 있는 방법에 대한 자세한 내용 [Cloud Foundry 설명서][cf-orgs-spaces-docs]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="beda8-133">For more information about orgs and spaces and how they can be used for role-based access control (RBAC), see the [Cloud Foundry documentation][cf-orgs-spaces-docs].</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="beda8-134">응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="beda8-134">Deploy an application</span></span>

<span data-ttu-id="beda8-135">Java로 작성되며 [Spring Framework](http://spring.io) 및 [Spring Boot](http://projects.spring.io/spring-boot/)를 기반으로 하는 Hello Spring Cloud라는 샘플 Cloud Foundry 응용 프로그램을 사용해 봅시다.</span><span class="sxs-lookup"><span data-stu-id="beda8-135">Let's use a sample Cloud Foundry application called Hello Spring Cloud, which is written in Java and based on the [Spring Framework](http://spring.io) and [Spring Boot](http://projects.spring.io/spring-boot/).</span></span>

### <a name="clone-the-hello-spring-cloud-repository"></a><span data-ttu-id="beda8-136">Hello Spring Cloud 리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="beda8-136">Clone the Hello Spring Cloud repository</span></span>

<span data-ttu-id="beda8-137">Hello Spring Cloud 샘플 응용 프로그램은 GitHub에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-137">The Hello Spring Cloud sample application is available on GitHub.</span></span> <span data-ttu-id="beda8-138">사용자 환경에 복제하고 새 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-138">Clone it to your environment and change into the new directory:</span></span>

```bash
git clone https://github.com/cloudfoundry-samples/hello-spring-cloud
cd hello-spring-cloud
```

### <a name="build-the-application"></a><span data-ttu-id="beda8-139">응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="beda8-139">Build the application</span></span>

<span data-ttu-id="beda8-140">[Apache Maven](http://maven.apache.org)을 사용하여 앱을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-140">Build the app using [Apache Maven](http://maven.apache.org).</span></span>

```bash
mvn clean package
```

### <a name="deploy-the-application-with-cf-push"></a><span data-ttu-id="beda8-141">cf 밀어넣기로 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="beda8-141">Deploy the application with cf push</span></span>

<span data-ttu-id="beda8-142">`push` 명령을 사용하여 대부분의 응용 프로그램을 Cloud Foundry에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-142">You can deploy most applications to Cloud Foundry using the `push` command:</span></span>

```bash
cf push
```

<span data-ttu-id="beda8-143">응용 프로그램을 *밀어넣는* 경우 Cloud Foundry는 응용 프로그램의 유형을 검색하고(이 경우 Java 앱) 해당 종속성을 식별합니다(이 경우 Spring framework).</span><span class="sxs-lookup"><span data-stu-id="beda8-143">When you *push* an application, Cloud Foundry detects the type of application (in this case, a Java app) and identifies its dependencies (in this case, the Spring framework).</span></span> <span data-ttu-id="beda8-144">그런 다음 코드를 *드롭릿*으로 알려진 독립 실행형 컨테이너 이미지로 실행하는 데 필요한 모든 요소를 패키지합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-144">It then packages everything required to run your code into a standalone container image, known as a *droplet*.</span></span> <span data-ttu-id="beda8-145">마지막으로 Cloud Foundry는 사용자 환경에서 사용할 수 있는 컴퓨터 중 하나에서 응용 프로그램을 예약하고 접근할 수 있는 URL을 만듭니다. 이는 명령의 출력에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-145">Finally, Cloud Foundry schedules the application on one of the available machines in your environment and creates a URL where you can reach it, which is available in the output of the command.</span></span>

![cf 밀어넣기 명령의 출력][cf-push-output]

<span data-ttu-id="beda8-147">hello-spring-cloud 응용 프로그램을 보려면 브라우저에서 제공된 URL을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-147">To see the hello-spring-cloud application, open the provided URL in your browser:</span></span>

![Hello Spring Cloud용 기본 UI][hello-spring-cloud-basic]

> [!NOTE] 
> <span data-ttu-id="beda8-149">`cf push` 처리 과정에 대한 자세한 내용을 보려면 Cloud Foundry 설명서에서 [응용 프로그램 준비 방법][cf-push-docs]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="beda8-149">To learn more about what happens during `cf push`, see [How Applications Are Staged][cf-push-docs] in the Cloud Foundry documentation.</span></span>

## <a name="view-application-logs"></a><span data-ttu-id="beda8-150">응용 프로그램 로그 보기</span><span class="sxs-lookup"><span data-stu-id="beda8-150">View application logs</span></span>

<span data-ttu-id="beda8-151">Cloud Foundry CLI를 사용하여 해당 이름으로 응용 프로그램에 대한 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-151">You can use the Cloud Foundry CLI to view logs for an application by its name:</span></span>

```bash
cf logs hello-spring-cloud
```

<span data-ttu-id="beda8-152">기본적으로 로그 명령은 작성된 대로 새 로그를 보여 주는 *비상 로그*를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-152">By default, the logs command uses *tail*, which shows new logs as they are written.</span></span> <span data-ttu-id="beda8-153">표시되는 새 로그를 보려면 브라우저에서 hello-spring-cloud 앱을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-153">To see new logs appear, refresh the hello-spring-cloud app in the browser.</span></span>

<span data-ttu-id="beda8-154">이미 작성된 로그를 보려면 `recent` 스위치를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-154">To view logs that have already been written, add the `recent` switch:</span></span>

```bash
cf logs --recent hello-spring-cloud
```

## <a name="scale-the-application"></a><span data-ttu-id="beda8-155">응용 프로그램 크기 조정</span><span class="sxs-lookup"><span data-stu-id="beda8-155">Scale the application</span></span>

<span data-ttu-id="beda8-156">기본적으로 `cf push`만 응용 프로그램의 단일 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-156">By default, `cf push` only creates a single instance of your application.</span></span> <span data-ttu-id="beda8-157">고가용성을 보장하고 높은 처리량을 위해 규모 확장을 활성화하려면 일반적으로 응용 프로그램의 둘 이상의 인스턴스를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-157">To ensure high availability and enable scale out for higher throughput, you generally want to run more than one instance of your applications.</span></span> <span data-ttu-id="beda8-158">`scale` 명령을 사용하여 이미 배포된 응용 프로그램을 쉽게 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-158">You can easily scale out already deployed applications using the `scale` command:</span></span>

```bash
cf scale -i 2 hello-spring-cloud
```

<span data-ttu-id="beda8-159">응용 프로그램에서 `cf app` 명령을 실행하면 Cloud Foundry가 응용 프로그램의 다른 인스턴스를 만들고 있음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-159">Running the `cf app` command on the application shows that Cloud Foundry is creating another instance of the application.</span></span> <span data-ttu-id="beda8-160">응용 프로그램이 시작된 후 Cloud Foundry는 트래픽 부하 분산을 자동으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-160">Once the application has started, Cloud Foundry automatically starts load balancing traffic to it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="beda8-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="beda8-161">Next steps</span></span>

- <span data-ttu-id="beda8-162">[Cloud Foundry 설명서 읽기][cloudfoundry-docs]</span><span class="sxs-lookup"><span data-stu-id="beda8-162">[Read the Cloud Foundry documentation][cloudfoundry-docs]</span></span>
- <span data-ttu-id="beda8-163">[Cloud Foundry용 Visual Studio Team Services 플러그인 설정][vsts-plugin]</span><span class="sxs-lookup"><span data-stu-id="beda8-163">[Set up the Visual Studio Team Services plugin for Cloud Foundry][vsts-plugin]</span></span>
- <span data-ttu-id="beda8-164">[Cloud Foundry용 Microsoft Log Analytics 노즐 구성][loganalytics-nozzle]</span><span class="sxs-lookup"><span data-stu-id="beda8-164">[Configure the Microsoft Log Analytics Nozzle for Cloud Foundry][loganalytics-nozzle]</span></span>

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