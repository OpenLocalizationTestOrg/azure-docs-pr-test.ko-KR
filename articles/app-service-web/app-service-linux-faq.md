---
title: "Linux의 Azure App Service Web App에 대한 FAQ | Microsoft Docs"
description: "Linux의 Azure App Service Web App에 대한 FAQ"
keywords: "Azure App Service, 웹앱, faq, linux, oss"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: 6122f28b35d143ec26a379ae9aa8aee9bdaaff9e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-app-service-web-app-on-linux-faq"></a><span data-ttu-id="f0768-104">Linux의 Azure App Service Web App에 대한 FAQ</span><span class="sxs-lookup"><span data-stu-id="f0768-104">Azure App Service Web App on Linux FAQ</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="f0768-105">Linux에 웹앱을 릴리스하면서 현재 플랫폼에 기능을 추가하고 플랫폼을 더욱 개선하기 위한 작업을 진행하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-105">With the release of Web App on Linux, we're working on adding features and making improvements to our platform.</span></span> <span data-ttu-id="f0768-106">다음은 최근 몇 달 동안 고객이 가장 자주 물어본 몇 가지 질문입니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-106">Here are some frequently asked questions (FAQ) that our customers have been asking us over the last months.</span></span>
<span data-ttu-id="f0768-107">질문이 있으면 문서에 남겨주세요. 최대한 신속하게 답변을 드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-107">If you have a question, comment on the article and we'll answer it as soon as possible.</span></span>

## <a name="built-in-images"></a><span data-ttu-id="f0768-108">기본 제공 이미지</span><span class="sxs-lookup"><span data-stu-id="f0768-108">Built-in images</span></span>

<span data-ttu-id="f0768-109">**Q:** 플랫폼에서 제공하는 기본 제공 Docker 컨테이너를 분기하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-109">**Q:** I want to fork the built-in Docker containers that the platform provides.</span></span> <span data-ttu-id="f0768-110">이러한 파일은 어디서 찾을 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="f0768-110">Where can I find those files?</span></span>

<span data-ttu-id="f0768-111">**A:** [GitHub](https://github.com/azure-app-service)에서 모든 Docker 파일을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-111">**A:** You can find all Docker files on [GitHub](https://github.com/azure-app-service).</span></span> <span data-ttu-id="f0768-112">[Docker Hub](https://hub.docker.com/u/appsvc/)에서 모든 Docker 컨테이너를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-112">You can find all Docker containers on [Docker Hub](https://hub.docker.com/u/appsvc/).</span></span>

<span data-ttu-id="f0768-113">**Q:** 런타임 스택을 구성할 때 시작 파일 섹션에 대해 예상되는 값은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="f0768-113">**Q:** What are the expected values for the Startup File section when I configure the runtime stack?</span></span>

<span data-ttu-id="f0768-114">**A:** Node.Js의 경우 PM2 구성 파일 또는 스크립트 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-114">**A:** For Node.Js, you specify the PM2 configuration file or your script file.</span></span> <span data-ttu-id="f0768-115">.Net Core의 경우 컴파일된 DLL 이름을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-115">For .NET Core, specify your compiled DLL name.</span></span> <span data-ttu-id="f0768-116">Ruby의 경우 앱을 초기화하려면 Ruby 스크립트를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-116">For Ruby, you can specify the Ruby script that you want to initialize your app with.</span></span>

## <a name="management"></a><span data-ttu-id="f0768-117">관리</span><span class="sxs-lookup"><span data-stu-id="f0768-117">Management</span></span>

<span data-ttu-id="f0768-118">**Q:** Azure Portal에서 다시 시작 단추를 누르면 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="f0768-118">**Q:** What happens when I press the restart button in the Azure portal?</span></span>

<span data-ttu-id="f0768-119">**A:** Docker를 다시 시작하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-119">**A:** This is the equivalent of Docker restart.</span></span>

<span data-ttu-id="f0768-120">**Q:** 앱 컨테이너 가상 컴퓨터(VM)에 연결하기 위해 Secure Shell(SSH)을 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="f0768-120">**Q:** Can I use Secure Shell (SSH) to connect to the app container virtual machine (VM)?</span></span>

<span data-ttu-id="f0768-121">**A:** 예, SCM 사이트를 통해 이 작업을 수행할 수 있습니다. 자세한 내용은 [Linux의 웹앱에 대한 SSH 지원](./app-service-linux-ssh-support.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0768-121">**A:** Yes, you can do that through the SCM site, check the following article for more information [SSH support for Web App on Linux](./app-service-linux-ssh-support.md)</span></span>

<span data-ttu-id="f0768-122">**Q:** SDK 또는 ARM 템플릿을 통해 Linux App Service 계획을 만들려고 합니다. 어떻게 할 수 있을까요?</span><span class="sxs-lookup"><span data-stu-id="f0768-122">**Q:** I want to create a Linux App Service plane through SDK or an ARM template, how can I achieve this?</span></span>

<span data-ttu-id="f0768-123">**A:** App Service의 `reserved` 필드를 `true`로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-123">**A:** You need to set the `reserved` field of the app service to `true`.</span></span>

## <a name="continuous-integrationdeployment"></a><span data-ttu-id="f0768-124">지속적인 통합/배포</span><span class="sxs-lookup"><span data-stu-id="f0768-124">Continuous integration/deployment</span></span>

<span data-ttu-id="f0768-125">**Q:** Docker Hub에서 이미지를 업데이트한 후에도 웹앱에서 여전히 기존 Docker 컨테이너 이미지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-125">**Q:** My web app still uses an old Docker container image after I've updated the image on Docker Hub.</span></span> <span data-ttu-id="f0768-126">사용자 지정 컨테이너의 지속적인 통합/배포를 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="f0768-126">Do you support continuous integration/deployment of custom containers?</span></span>

<span data-ttu-id="f0768-127">**A:** Azure Container Registry 또는 DockerHub 이미지에 대한 지속적인 통합/배포를 설정하려면 [Linux에서 Azure 웹앱을 사용하여 연속 배포](./app-service-linux-ci-cd.md) 문서를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="f0768-127">**A:** To set up continuous integration/deployment for Azure Container Registry or DockerHub images by check the following article [Continuous Deployment with Azure Web App on Linux](./app-service-linux-ci-cd.md).</span></span> <span data-ttu-id="f0768-128">개인 레지스트리의 경우 웹앱을 중지했다가 다시 시작하여 컨테이너를 새로 고칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-128">For private registries, you can refresh the container by stopping and then starting your web app.</span></span> <span data-ttu-id="f0768-129">또는 컨테이너를 강제로 새로 고침하도록 더미 응용 프로그램을 변경 또는 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-129">Or you can change or add a dummy application setting to force a refresh of your container.</span></span>

<span data-ttu-id="f0768-130">**Q:** 스테이징 환경이 지원되나요?</span><span class="sxs-lookup"><span data-stu-id="f0768-130">**Q:** Do you support staging environments?</span></span>

<span data-ttu-id="f0768-131">**A:** 예.</span><span class="sxs-lookup"><span data-stu-id="f0768-131">**A:** Yes.</span></span>

<span data-ttu-id="f0768-132">**Q:** **웹 배포**를 사용하여 내 웹앱을 설정할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="f0768-132">**Q:** Can I use **web deploy** to deploy my web app?</span></span>

<span data-ttu-id="f0768-133">**A:** 예. `WEBSITE_WEBDEPLOY_USE_SCM`이라는 앱 설정을 `false`로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-133">**A:** Yes, you need to set an app setting called `WEBSITE_WEBDEPLOY_USE_SCM` to `false`.</span></span>

## <a name="language-support"></a><span data-ttu-id="f0768-134">언어 지원</span><span class="sxs-lookup"><span data-stu-id="f0768-134">Language support</span></span>

<span data-ttu-id="f0768-135">**Q:** 컴파일되지 않은 .NET Core 앱을 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="f0768-135">**Q:** Do you support uncompiled .NET Core apps?</span></span>

<span data-ttu-id="f0768-136">**A:** 예.</span><span class="sxs-lookup"><span data-stu-id="f0768-136">**A:** Yes.</span></span>

<span data-ttu-id="f0768-137">**Q:** 작성기를 PHP 앱의 종속성 관리자로 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="f0768-137">**Q:** Do you support Composer as a dependency manager for PHP apps?</span></span>

<span data-ttu-id="f0768-138">**A:** 예.</span><span class="sxs-lookup"><span data-stu-id="f0768-138">**A:** Yes.</span></span> <span data-ttu-id="f0768-139">Git 배포 중에 Kudu는 사용자가 PHP 응용 프로그램을 배포하고 있음을 감지하고(composer.json 파일의 존재 덕분) 자동으로 작성기 설치를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-139">During a Git deployment, Kudu should detect that you are deploying a PHP application (thanks to the presence of a composer.json file) and will trigger a composer install for you.</span></span>

## <a name="custom-containers"></a><span data-ttu-id="f0768-140">사용자 지정 컨테이너</span><span class="sxs-lookup"><span data-stu-id="f0768-140">Custom containers</span></span>

<span data-ttu-id="f0768-141">**Q:** 나만의 사용자 지정 컨테이너를 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-141">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="f0768-142">앱이 `\home\` 디렉터리에 상주하는데 [SCM 사이트](https://github.com/projectkudu/kudu) 또는 FTP 클라이언트를 사용하여 콘텐츠를 찾아볼 때 파일을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-142">My app resides in the `\home\` directory, but I can't find my files when I browse the content by using the [SCM site](https://github.com/projectkudu/kudu) or an FTP client.</span></span> <span data-ttu-id="f0768-143">내 파일은 어디에 있나요?</span><span class="sxs-lookup"><span data-stu-id="f0768-143">Where are my files?</span></span>

<span data-ttu-id="f0768-144">**A:** `\home\` 디렉터리에 SMB 공유를 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-144">**A:** We mount an SMB share to the `\home\` directory.</span></span> <span data-ttu-id="f0768-145">포함된 모든 콘텐츠를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-145">This will override any content that's there.</span></span>

<span data-ttu-id="f0768-146">**Q:** 나만의 사용자 지정 컨테이너를 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-146">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="f0768-147">플랫폼에서 `\home\`에 SMB 공유를 탑재하지 않으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-147">I don't want the platform to mount an SMB share to the `\home\`.</span></span>

<span data-ttu-id="f0768-148">**A:** `WEBSITES_ENABLE_APP_SERVICE_STORAGE` 앱 설정을 `false`로 설정하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-148">**A:** You can do that by setting the `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting to `false`.</span></span>

<span data-ttu-id="f0768-149">**Q:** 내 사용자 지정 컨테이너는 시작하는 데 시간이 오래 걸리고 플랫폼이 시작을 마무리하기 전에 컨테이너를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-149">**Q:** My custom container takes a long time to start, and the platform restart the container before it finishes starting up.</span></span>

<span data-ttu-id="f0768-150">**A:** 컨테이너를 다시 시작하기 전에 플랫폼이 대기할 시간을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-150">**A:** You can configure the time the platform will wait before restarting your container.</span></span> <span data-ttu-id="f0768-151">`WEBSITES_CONTAINER_START_TIME_LIMIT` 앱 설정을 원하는 값(초)으로 설정하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-151">This can be done by setting the `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting to the desired value in seconds.</span></span> <span data-ttu-id="f0768-152">기본값은 230초이고 최대값은 600초입니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-152">The default is 230 seconds, and the max is 600 seconds.</span></span>

<span data-ttu-id="f0768-153">**Q:** 개인 레지스트리 서버 URL의 형식은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="f0768-153">**Q:** What is the format for private registry server url?</span></span>

<span data-ttu-id="f0768-154">**A:** `http://` 또는 `https://`를 포함하여 전체 레지스트리 URL을 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-154">**A:** You need to provide the full registry url including `http://` or `https://`.</span></span>

<span data-ttu-id="f0768-155">**Q:** 개인 레지스트리 옵션에서 이미지 이름의 형식은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="f0768-155">**Q:** What is the format for the image name in private registry option?</span></span>

<span data-ttu-id="f0768-156">**A:** 개인 레지스트리 URL을 포함하여 전체 이미지 이름을 추가해야 합니다(예:</span><span class="sxs-lookup"><span data-stu-id="f0768-156">**A:** You need to add the full image name including the private registry url (eg.</span></span> <span data-ttu-id="f0768-157">myacr.azurecr.io/dotnet:latest).</span><span class="sxs-lookup"><span data-stu-id="f0768-157">myacr.azurecr.io/dotnet:latest)</span></span>

<span data-ttu-id="f0768-158">**Q:** 사용자 지정 컨테이너 이미지에 포트를 두 개 이상 표시하려 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-158">**Q:** I want to expose more than one port on my custom container image.</span></span> <span data-ttu-id="f0768-159">가능할까요?</span><span class="sxs-lookup"><span data-stu-id="f0768-159">Is that possible?</span></span>

<span data-ttu-id="f0768-160">**A:** 현재는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-160">**A:** Currently, that isn't supported.</span></span>

<span data-ttu-id="f0768-161">**Q:** 사용자 고유의 저장소를 가져올 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="f0768-161">**Q:** Can I bring my own storage?</span></span>

<span data-ttu-id="f0768-162">**A:** 현재는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-162">**A:** Currently that isn't supported.</span></span>

<span data-ttu-id="f0768-163">**Q:** 내 사용자 지정 컨테이너의 파일 시스템 또는 실행 중인 프로세스를 SCM 사이트에서 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-163">**Q:** I can't browse my custom container's file system or running processes from the SCM site.</span></span> <span data-ttu-id="f0768-164">그 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="f0768-164">Why is that?</span></span>

<span data-ttu-id="f0768-165">**A:** SCM 사이트는 별도의 컨테이너에서 실행되기 때문에</span><span class="sxs-lookup"><span data-stu-id="f0768-165">**A:** The SCM site runs in a separate container.</span></span> <span data-ttu-id="f0768-166">사용자가 앱 컨테이너의 파일 시스템 또는 실행 중인 프로세스를 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-166">You can't check the file system or running processes of the app container.</span></span>

<span data-ttu-id="f0768-167">**Q:** 내 사용자 지정 컨테이너가 포트 80 이외의 포트를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-167">**Q:** My custom container listens to a port other than port 80.</span></span> <span data-ttu-id="f0768-168">해당 포트로 요청을 라우팅하도록 내 앱을 구성하려면 어떻게 합니까?</span><span class="sxs-lookup"><span data-stu-id="f0768-168">How can I configure my app to route the requests to that port?</span></span>

<span data-ttu-id="f0768-169">**A:** 자동 포트 검색 기능이 있으며 **WEBSITES_PORT**라는 응용 프로그램 설정을 지정하고 예상되는 포트 번호 값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-169">**A:** We have auto port detection, also you can specify an application setting called **WEBSITES_PORT**, and give it the value of the expected port number.</span></span> <span data-ttu-id="f0768-170">이전에 플랫폼은 `PORT` 앱 설정을 사용했으며 이 앱 설정 사용을 사용되지 않도록 하고 `WEBSITES_PORT`를 단독으로 사용하도록 이동할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-170">Previously the platform was using `PORT` app setting, we are planning to deprecate the use this app setting and move to using `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="f0768-171">**Q:** 사용자 지정 컨테이너에서 HTTPS를 구현해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="f0768-171">**Q:** Do I need to implement HTTPS in my custom container.</span></span>

<span data-ttu-id="f0768-172">**A:** 아니요. 플랫폼에서는 공유 프런트 엔드에서 HTTPS 종료를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-172">**A:** No, the platform handles HTTPS termination at the shared frontends.</span></span>

## <a name="pricing-and-sla"></a><span data-ttu-id="f0768-173">가격 및 SLA</span><span class="sxs-lookup"><span data-stu-id="f0768-173">Pricing and SLA</span></span>

<span data-ttu-id="f0768-174">**Q:** 공개 미리 보기를 사용 하는 동안 가격은 얼마입니까?</span><span class="sxs-lookup"><span data-stu-id="f0768-174">**Q:** What's the pricing while you're using the public preview?</span></span>

<span data-ttu-id="f0768-175">**A:** 일반 Azure App Service 가격으로 앱이 실행되는 시간의 절반이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-175">**A:** You are charged half the number of hours that your app runs, with the normal Azure App Service pricing.</span></span> <span data-ttu-id="f0768-176">즉, 이 일반 Azure App Service 가격에서 50% 할인이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-176">This means that you get a 50 percent discount on normal Azure App Service pricing.</span></span>

## <a name="other"></a><span data-ttu-id="f0768-177">기타</span><span class="sxs-lookup"><span data-stu-id="f0768-177">Other</span></span>

<span data-ttu-id="f0768-178">**Q:** 응용 프로그램 설정 이름에 지원되는 문자는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="f0768-178">**Q:** What are the supported characters in application settings names?</span></span>

<span data-ttu-id="f0768-179">**A:** 응용 프로그램 설정에는 A-Z, a-z, 0-9 및 밑줄만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-179">**A:** You can only use A-Z, a-z, 0-9, and the underscore for application settings.</span></span>

<span data-ttu-id="f0768-180">**Q:** 어디서 새 기능을 요청할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="f0768-180">**Q:** Where can I request new features?</span></span>

<span data-ttu-id="f0768-181">**A:** [Web Apps 사용자 의견 포럼](https://aka.ms/webapps-uservoice)에서 사용자의 아이디어를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0768-181">**A:** You can submit your idea at the [Web Apps feedback forum](https://aka.ms/webapps-uservoice).</span></span> <span data-ttu-id="f0768-182">아이디어 제목에 "[Linux]"를 붙여 주세요.</span><span class="sxs-lookup"><span data-stu-id="f0768-182">Add "[Linux]" to the title of your idea.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0768-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f0768-183">Next steps</span></span>
* [<span data-ttu-id="f0768-184">Linux에서 Azure Web App이란?</span><span class="sxs-lookup"><span data-stu-id="f0768-184">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="f0768-185">Linux의 Azure Web App에 대한 SSH 지원</span><span class="sxs-lookup"><span data-stu-id="f0768-185">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="f0768-186">Azure App Service에서 스테이징 환경 설정</span><span class="sxs-lookup"><span data-stu-id="f0768-186">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="f0768-187">Linux에서 Azure 웹앱을 사용한 연속 배포</span><span class="sxs-lookup"><span data-stu-id="f0768-187">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
