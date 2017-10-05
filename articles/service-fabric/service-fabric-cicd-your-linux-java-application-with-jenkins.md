---
title: "Jenkins를 사용하여 Azure Service Fabric Linux Java 응용 프로그램 연속 빌드 및 통합 | Microsoft Docs"
description: "Jenkins를 사용하여 Linux Java 응용 프로그램 연속 빌드 및 통합"
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: saysa
ms.openlocfilehash: d9372407540d903acca5b1639a2d9ceb0bf3c571
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-jenkins-to-build-and-deploy-your-linux-java-application"></a><span data-ttu-id="c0ad5-103">Jenkins를 사용하여 Linux Java 응용 프로그램 빌드 및 배포</span><span class="sxs-lookup"><span data-stu-id="c0ad5-103">Use Jenkins to build and deploy your Linux Java application</span></span>
<span data-ttu-id="c0ad5-104">Jenkins는 앱의 연속 통합 및 배포를 위한 인기 있는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-104">Jenkins is a popular tool for continuous integration and deployment of your apps.</span></span> <span data-ttu-id="c0ad5-105">Jenkins를 사용하여 Azure Service Fabric 응용 프로그램을 빌드하고 배포하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-105">Here's how to build and deploy your Azure Service Fabric application by using Jenkins.</span></span>

## <a name="general-prerequisites"></a><span data-ttu-id="c0ad5-106">일반 필수 조건</span><span class="sxs-lookup"><span data-stu-id="c0ad5-106">General prerequisites</span></span>
- <span data-ttu-id="c0ad5-107">로컬로 설치된 Git가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-107">Have Git installed locally.</span></span> <span data-ttu-id="c0ad5-108">운영 체제에 따라 [Git 다운로드 페이지](https://git-scm.com/downloads)에서 적절한 Git 버전을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-108">You can install the appropriate Git version from [the Git downloads page](https://git-scm.com/downloads), based on your operating system.</span></span> <span data-ttu-id="c0ad5-109">Git을 처음 접하는 경우 [Git 설명서](https://git-scm.com/docs)에서 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-109">If you are new to Git, learn more about it from the [Git documentation](https://git-scm.com/docs).</span></span>
- <span data-ttu-id="c0ad5-110">유용한 Service Fabric Jenkins 플러그 인이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-110">Have the Service Fabric Jenkins plug-in handy.</span></span> <span data-ttu-id="c0ad5-111">[Service Fabric 다운로드](https://servicefabricdownloads.blob.core.windows.net/jenkins/serviceFabric.hpi)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-111">You can download it from [Service Fabric downloads](https://servicefabricdownloads.blob.core.windows.net/jenkins/serviceFabric.hpi).</span></span>

## <a name="set-up-jenkins-inside-a-service-fabric-cluster"></a><span data-ttu-id="c0ad5-112">Service Fabric 클러스터 내에서 Jenkins 설정</span><span class="sxs-lookup"><span data-stu-id="c0ad5-112">Set up Jenkins inside a Service Fabric cluster</span></span>

<span data-ttu-id="c0ad5-113">Service Fabric 클러스터 내부 또는 외부에서 Jenkins를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-113">You can set up Jenkins either inside or outside a Service Fabric cluster.</span></span> <span data-ttu-id="c0ad5-114">다음 섹션에서는 Azure Storage 계정을 사용하여 컨테이너 인스턴스 상태를 저장하면서 클러스터 내에서 이를 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-114">The following sections show how to set it up inside a cluster while using an Azure storage account to save the state of the container instance.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c0ad5-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c0ad5-115">Prerequisites</span></span>
1. <span data-ttu-id="c0ad5-116">Service Fabric Linux 클러스터를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-116">Have a Service Fabric Linux cluster ready.</span></span> <span data-ttu-id="c0ad5-117">Azure Portal에서 만든 Service Fabric 클러스터에는 Docker가 이미 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-117">A Service Fabric cluster created from the Azure portal already has Docker installed.</span></span> <span data-ttu-id="c0ad5-118">클러스터를 로컬로 실행하는 경우 ``docker info`` 명령을 사용하여 Docker가 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-118">If you are running the cluster locally, check if Docker is installed by using the command ``docker info``.</span></span> <span data-ttu-id="c0ad5-119">설치되어 있지 않으면 다음 명령을 사용하여 적절하게 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-119">If it is not installed, install it accordingly by using the following commands:</span></span>

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```
2. <span data-ttu-id="c0ad5-120">다음 단계를 사용하여 Service Fabric 컨테이너 응용 프로그램을 클러스터에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-120">Have the Service Fabric container application deployed on the cluster, by using the following steps:</span></span>

  ```sh
git clone https://github.com/Azure-Samples/service-fabric-java-getting-started.git
cd service-fabric-java-getting-started/Services/JenkinsDocker/
```

3. <span data-ttu-id="c0ad5-121">Jenkins 컨테이너 인스턴스의 상태를 유지하려는 Azure Storage 파일 공유의 연결 옵션 세부 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-121">You need the connect option details of the Azure storage file-share, where you want to persist the state of the Jenkins container instance.</span></span> <span data-ttu-id="c0ad5-122">동일한 용도로 Microsoft Azure Portal을 사용하는 경우 ``sfjenkinsstorage1``이라는 Azure Storage 계정을 만드는 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-122">If you are using the Microsoft Azure portal for the same, please follow the steps - Create an Azure storage account, say ``sfjenkinsstorage1``.</span></span> <span data-ttu-id="c0ad5-123">``sfjenkins``라는 저장소 계정 아래 **파일 공유**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-123">Create a **File Share** under that storage account, say ``sfjenkins``.</span></span> <span data-ttu-id="c0ad5-124">파일 공유에 대해 **연결**을 클릭하고 다음과 유사하게 **Linux에서 연결** 아래 표시되는 값을 메모해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-124">Click on **Connect** for the file-share and note the values it displays under **Connecting from Linux**, say this would look like as follows -</span></span>
```sh
sudo mount -t cifs //sfjenkinsstorage1.file.core.windows.net/sfjenkins [mount point] -o vers=3.0,username=sfjenkinsstorage1,password=<storage_key>,dir_mode=0777,file_mode=0777
```

4. <span data-ttu-id="c0ad5-125">```setupentrypoint.sh``` 스크립트에서 자리 표시자 값을 해당 azure 저장소 세부 정보로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-125">Update the placeholder values in the ```setupentrypoint.sh``` script with corresponding azure-storage details.</span></span>
```sh
vi JenkinsSF/JenkinsOnSF/Code/setupentrypoint.sh
```
<span data-ttu-id="c0ad5-126">``[REMOTE_FILE_SHARE_LOCATION]``을 위의 포인트 3 연결 출력의 ``//sfjenkinsstorage1.file.core.windows.net/sfjenkins`` 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-126">Replace ``[REMOTE_FILE_SHARE_LOCATION]`` with the value ``//sfjenkinsstorage1.file.core.windows.net/sfjenkins`` from the output of the connect in point 3 above.</span></span>
<span data-ttu-id="c0ad5-127">``[FILE_SHARE_CONNECT_OPTIONS_STRING]``을 위의 포인트 3에서 ``vers=3.0,username=sfjenkinsstorage1,password=GB2NPUCQY9LDGeG9Bci5dJV91T6SrA7OxrYBUsFHyueR62viMrC6NIzyQLCKNz0o7pepGfGY+vTa9gxzEtfZHw==,dir_mode=0777,file_mode=0777`` 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-127">Replace ``[FILE_SHARE_CONNECT_OPTIONS_STRING]`` with the value ``vers=3.0,username=sfjenkinsstorage1,password=GB2NPUCQY9LDGeG9Bci5dJV91T6SrA7OxrYBUsFHyueR62viMrC6NIzyQLCKNz0o7pepGfGY+vTa9gxzEtfZHw==,dir_mode=0777,file_mode=0777`` from point 3 above.</span></span>

5. <span data-ttu-id="c0ad5-128">클러스터에 연결하고 컨테이너 응용 프로그램을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-128">Connect to the cluster and install the container application.</span></span>
```azurecli
sfctl cluster select --endpoint http://PublicIPorFQDN:19080   # cluster connect command
bash Scripts/install.sh
```
<span data-ttu-id="c0ad5-129">그러면 클러스터에 Jenkins 컨테이너를 설치하고 Service Fabric Explorer를 사용하여 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-129">This installs a Jenkins container on the cluster, and can be monitored by using the Service Fabric Explorer.</span></span>

### <a name="steps"></a><span data-ttu-id="c0ad5-130">단계</span><span class="sxs-lookup"><span data-stu-id="c0ad5-130">Steps</span></span>
1. <span data-ttu-id="c0ad5-131">브라우저에서 ``http://PublicIPorFQDN:8081``으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-131">From your browser, go to ``http://PublicIPorFQDN:8081``.</span></span> <span data-ttu-id="c0ad5-132">로그인하는 데 필요한 초기 관리자 암호의 경로가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-132">It provides the path of the initial admin password required to sign in.</span></span> <span data-ttu-id="c0ad5-133">관리 사용자 권한으로 Jenkins를 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-133">You can continue to use Jenkins as an admin user.</span></span> <span data-ttu-id="c0ad5-134">또는 초기 관리자 계정으로 로그인한 후에 사용자를 만들고 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-134">Or you can create and change the user, after you sign in with the initial admin account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c0ad5-135">클러스터를 만드는 동안 8081 포트를 응용 프로그램 끝점 포트로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-135">Ensure that the 8081 port is specified as the application endpoint port while you are creating the cluster.</span></span>
   >

2. <span data-ttu-id="c0ad5-136">``docker ps -a``를 사용하여 컨테이너 인스턴스 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-136">Get the container instance ID by using ``docker ps -a``.</span></span>
3. <span data-ttu-id="c0ad5-137">컨테이너에 SSH(Secure Shell) 로그인을 수행하고 Jenkins 포털에서 표시된 경로를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-137">Secure Shell (SSH) sign in to the container, and paste the path you were shown on the Jenkins portal.</span></span> <span data-ttu-id="c0ad5-138">예를 들어 포털에서 경로 `PATH_TO_INITIAL_ADMIN_PASSWORD`가 표시된 경우 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-138">For example, if in the portal it shows the path `PATH_TO_INITIAL_ADMIN_PASSWORD`, run the following:</span></span>

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash   # This takes you inside Docker shell
  cat PATH_TO_INITIAL_ADMIN_PASSWORD
  ```

4. <span data-ttu-id="c0ad5-139">[새 SSH 키 생성 및 SSH 에이전트에 추가](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)에서 설명한 단계를 사용하여 Jenkins를 사용하도록 GitHub을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-139">Set up GitHub to work with Jenkins, by using the steps mentioned in [Generating a new SSH key and adding it to the SSH agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).</span></span>
    * <span data-ttu-id="c0ad5-140">GitHub에서 제공되는 지침을 사용하여 SSH 키를 생성하고 SSH 키를 리포지토리를 호스팅하는 GitHub 계정에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-140">Use the instructions provided by GitHub to generate the SSH key, and to add the SSH key to the GitHub account that is hosting your repository.</span></span>
    * <span data-ttu-id="c0ad5-141">(호스트가 아닌) Jenkins Docker 셸에서 이전 링크에 언급된 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-141">Run the commands mentioned in the preceding link in the Jenkins Docker shell (and not on your host).</span></span>
    * <span data-ttu-id="c0ad5-142">호스트에서 Jenkins 셸에 로그인하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-142">To sign in to the Jenkins shell from your host, use the following command:</span></span>

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
  ```

## <a name="set-up-jenkins-outside-a-service-fabric-cluster"></a><span data-ttu-id="c0ad5-143">Service Fabric 클러스터 외부에서 Jenkins 설정</span><span class="sxs-lookup"><span data-stu-id="c0ad5-143">Set up Jenkins outside a Service Fabric cluster</span></span>

<span data-ttu-id="c0ad5-144">Service Fabric 클러스터 내부 또는 외부에서 Jenkins를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-144">You can set up Jenkins either inside or outside of a Service Fabric cluster.</span></span> <span data-ttu-id="c0ad5-145">다음 섹션에서는 클러스터 외부에서 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-145">The following sections show how to set it up outside a cluster.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c0ad5-146">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c0ad5-146">Prerequisites</span></span>
<span data-ttu-id="c0ad5-147">Docker를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-147">You need to have Docker installed.</span></span> <span data-ttu-id="c0ad5-148">다음 명령을 사용하여 터미널에서 Docker를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-148">The following commands can be used to install Docker from the terminal:</span></span>

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```

<span data-ttu-id="c0ad5-149">이렇게 하면 터미널에서 ``docker info``를 실행할 때 출력에서 Docker 서비스가 실행되는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-149">Now when you run ``docker info`` in the terminal, you should see in the output that the Docker service is running.</span></span>

### <a name="steps"></a><span data-ttu-id="c0ad5-150">단계</span><span class="sxs-lookup"><span data-stu-id="c0ad5-150">Steps</span></span>
  1. <span data-ttu-id="c0ad5-151">Service Fabric Jenkins 컨테이너 이미지를 끌어옵니다. ``docker pull raunakpandya/jenkins:v1``</span><span class="sxs-lookup"><span data-stu-id="c0ad5-151">Pull the Service Fabric Jenkins container image: ``docker pull raunakpandya/jenkins:v1``</span></span>
  2. <span data-ttu-id="c0ad5-152">다음 컨테이너 이미지를 실행합니다. ``docker run -itd -p 8080:8080 raunakpandya/jenkins:v1``</span><span class="sxs-lookup"><span data-stu-id="c0ad5-152">Run the container image: ``docker run -itd -p 8080:8080 raunakpandya/jenkins:v1``</span></span>
  3. <span data-ttu-id="c0ad5-153">컨테이너 이미지 인스턴스 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-153">Get the ID of the container image instance.</span></span> <span data-ttu-id="c0ad5-154">명령 ``docker ps –a``를 사용하여 모든 Docker 컨테이너를 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-154">You can list all the Docker containers with the command ``docker ps –a``</span></span>
  4. <span data-ttu-id="c0ad5-155">다음 단계에 따라 Jenkins 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-155">Sign in to the Jenkins portal by using the following steps:</span></span>

    * ```sh
    docker exec [first-four-digits-of-container-ID] cat /var/jenkins_home/secrets/initialAdminPassword
    ```
    <span data-ttu-id="c0ad5-156">컨테이너 ID가 2d24a73b5964이면 2d24를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-156">If container ID is 2d24a73b5964, use 2d24.</span></span>
    * <span data-ttu-id="c0ad5-157">이 암호는 ``http://<HOST-IP>:8080``인 포털에서 Jenkins 대시보드에 로그인하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-157">This password is required for signing in to the Jenkins dashboard from portal, which is ``http://<HOST-IP>:8080``</span></span>
    * <span data-ttu-id="c0ad5-158">처음으로 로그인한 후에 사용자 고유의 사용자 계정을 만들어 향후 목적을 위해 사용하거나 관리자 계정을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-158">After you sign in for the first time, you can create your own user account and use that for future purposes, or you can continue to use the administrator account.</span></span> <span data-ttu-id="c0ad5-159">사용자를 만들면 해당 계정으로 계속 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-159">After you create a user, you need to continue with that.</span></span>
  5. <span data-ttu-id="c0ad5-160">[새 SSH 키 생성 및 SSH 에이전트에 추가](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)에서 설명한 단계를 사용하여 Jenkins를 사용하도록 GitHub을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-160">Set up GitHub to work with Jenkins, by using the steps mentioned in [Generating a new SSH key and adding it to the SSH agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).</span></span>
        * <span data-ttu-id="c0ad5-161">GitHub에서 제공되는 지침을 사용하여 SSH 키를 생성하고 SSH 키를 리포지토리를 호스팅하는 GitHub 계정에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-161">Use the instructions provided by GitHub to generate the SSH key, and to add the SSH key to the GitHub account that is hosting the repository.</span></span>
        * <span data-ttu-id="c0ad5-162">(호스트가 아닌) Jenkins Docker 셸에서 이전 링크에 언급된 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-162">Run the commands mentioned in the preceding link in the Jenkins Docker shell (and not on your host).</span></span>
      * <span data-ttu-id="c0ad5-163">호스트에서 Jenkins 셸에 로그인하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-163">To sign in to the Jenkins shell from your host, use the following commands:</span></span>

      ```sh
      docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
      ```

<span data-ttu-id="c0ad5-164">Jenkins 컨테이너 이미지가 호스팅되는 클러스터 또는 컴퓨터에 공용 연결 IP가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-164">Ensure that the cluster or machine where the Jenkins container image is hosted has a public-facing IP.</span></span> <span data-ttu-id="c0ad5-165">그러면 Jenkins 인스턴스가 GitHub에서 알림을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-165">This enables the Jenkins instance to receive notifications from GitHub.</span></span>

## <a name="install-the-service-fabric-jenkins-plug-in-from-the-portal"></a><span data-ttu-id="c0ad5-166">포털에서 Service Fabric Jenkins 플러그 인 설치</span><span class="sxs-lookup"><span data-stu-id="c0ad5-166">Install the Service Fabric Jenkins plug-in from the portal</span></span>

1. <span data-ttu-id="c0ad5-167">``http://PublicIPorFQDN:8081``으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-167">Go to ``http://PublicIPorFQDN:8081``</span></span>
2. <span data-ttu-id="c0ad5-168">Jenkins 대시보드에서 **Jenkins 관리** > **플러그 인 관리** > **고급**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-168">From the Jenkins dashboard, select **Manage Jenkins** > **Manage Plugins** > **Advanced**.</span></span>
<span data-ttu-id="c0ad5-169">여기에서는 플러그 인을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-169">Here, you can upload a plug-in.</span></span> <span data-ttu-id="c0ad5-170">**파일 선택**을 선택한 다음 필수 구성 요소에서 다운로드한 **serviceFabric.hpi** 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-170">Select **Choose file**, and then select the **serviceFabric.hpi** file, which you downloaded under prerequisites.</span></span> <span data-ttu-id="c0ad5-171">**업로드**를 선택하면 Jenkins에서 플러그 인을 자동으로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-171">When you select **Upload**, Jenkins automatically installs the plug-in.</span></span> <span data-ttu-id="c0ad5-172">요청된 경우 다시 시작을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-172">Allow a restart if requested.</span></span>

## <a name="create-and-configure-a-jenkins-job"></a><span data-ttu-id="c0ad5-173">Jenkins 작업 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="c0ad5-173">Create and configure a Jenkins job</span></span>

1. <span data-ttu-id="c0ad5-174">대시보드에서 **새 항목**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-174">Create a **new item** from dashboard.</span></span>
2. <span data-ttu-id="c0ad5-175">항목 이름을 입력합니다(예: **MyJob**).</span><span class="sxs-lookup"><span data-stu-id="c0ad5-175">Enter an item name (for example, **MyJob**).</span></span> <span data-ttu-id="c0ad5-176">**자유로운 프로젝트**를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-176">Select **free-style project**, and click **OK**.</span></span>
3. <span data-ttu-id="c0ad5-177">작업 페이지로 이동하여 **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-177">Go the job page, and click **Configure**.</span></span>

   <span data-ttu-id="c0ad5-178">a.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-178">a.</span></span> <span data-ttu-id="c0ad5-179">일반 섹션의 **GitHub 프로젝트** 아래에서 GitHub 프로젝트 URL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-179">In the general section, under **GitHub project**, specify your GitHub project URL.</span></span> <span data-ttu-id="c0ad5-180">이 URL은 Jenkins CI/CD(연속 통합, 연속 배포) 흐름과 통합하려는 Service Fabric Java 응용 프로그램을 호스트합니다(예: ``https://github.com/sayantancs/SFJenkins``).</span><span class="sxs-lookup"><span data-stu-id="c0ad5-180">This URL hosts the Service Fabric Java application that you want to integrate with the Jenkins continuous integration, continuous deployment (CI/CD) flow (for example, ``https://github.com/sayantancs/SFJenkins``).</span></span>

   <span data-ttu-id="c0ad5-181">b.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-181">b.</span></span> <span data-ttu-id="c0ad5-182">**소스 코드 관리** 섹션 아래에서 **Git**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-182">Under the **Source Code Management** section, select **Git**.</span></span> <span data-ttu-id="c0ad5-183">Jenkins CI/CD 흐름과 통합하려는 Service Fabric Java 응용 프로그램을 호스트하는 리포지토리 URL을 지정합니다(예: ``https://github.com/sayantancs/SFJenkins.git``).</span><span class="sxs-lookup"><span data-stu-id="c0ad5-183">Specify the repository URL that hosts the Service Fabric Java application that you want to integrate with the Jenkins CI/CD flow (for example, ``https://github.com/sayantancs/SFJenkins.git``).</span></span> <span data-ttu-id="c0ad5-184">또한 여기에서 빌드할 분기를 지정할 수 있습니다(예: **/master**).</span><span class="sxs-lookup"><span data-stu-id="c0ad5-184">Also, you can specify here which branch to build (for example, **/master**).</span></span>
4. <span data-ttu-id="c0ad5-185">Jenkins와 통신할 수 있도록 리포지토리를 호스팅하는 *GitHub*을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-185">Configure your *GitHub* (which is hosting the repository) so that it is able to talk to Jenkins.</span></span> <span data-ttu-id="c0ad5-186">다음 단계를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-186">Use the following steps:</span></span>

   <span data-ttu-id="c0ad5-187">a.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-187">a.</span></span> <span data-ttu-id="c0ad5-188">GitHub 리포지토리 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-188">Go to your GitHub repository page.</span></span> <span data-ttu-id="c0ad5-189">**설정** > **통합 및 서비스**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-189">Go to **Settings** > **Integrations and Services**.</span></span>

   <span data-ttu-id="c0ad5-190">b.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-190">b.</span></span> <span data-ttu-id="c0ad5-191">**서비스 추가**를 선택하고 **Jenkins**를 입력하고 **Jenkins-GitHub 플러그 인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-191">Select **Add Service**, type **Jenkins**, and select the **Jenkins-GitHub plugin**.</span></span>

   <span data-ttu-id="c0ad5-192">c.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-192">c.</span></span> <span data-ttu-id="c0ad5-193">Jenkins Webhook URL을 입력합니다(기본적으로 ``http://<PublicIPorFQDN>:8081/github-webhook/``이여야 함).</span><span class="sxs-lookup"><span data-stu-id="c0ad5-193">Enter your Jenkins webhook URL (by default, it should be ``http://<PublicIPorFQDN>:8081/github-webhook/``).</span></span> <span data-ttu-id="c0ad5-194">**서비스 추가/업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-194">Click **add/update service**.</span></span>

   <span data-ttu-id="c0ad5-195">d.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-195">d.</span></span> <span data-ttu-id="c0ad5-196">테스트 이벤트가 사용자의 Jenkins 인스턴스로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-196">A test event is sent to your Jenkins instance.</span></span> <span data-ttu-id="c0ad5-197">GitHub의 웹후크에서 녹색 확인 표시가 나타나고 프로젝트가 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-197">You should see a green check by the webhook in GitHub, and your project will build.</span></span>

   <span data-ttu-id="c0ad5-198">e.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-198">e.</span></span> <span data-ttu-id="c0ad5-199">**트리거 빌드** 섹션 아래에서 원하는 빌드 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-199">Under the **Build Triggers** section, select which build option you want.</span></span> <span data-ttu-id="c0ad5-200">이 예에서는 리포지토리에 일부 푸시가 발생할 때마다 빌드를 트리거하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-200">For this example, you want to trigger a build whenever some push to the repository happens.</span></span> <span data-ttu-id="c0ad5-201">따라서 **GITScm 폴링에 대한 GitHub 후크 트리거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-201">So you select **GitHub hook trigger for GITScm polling**.</span></span> <span data-ttu-id="c0ad5-202">(이전에는 이 옵션을 **변경 내용이 GitHub에 푸시될 경우에 빌드**라고 했습니다.)</span><span class="sxs-lookup"><span data-stu-id="c0ad5-202">(Previously, this option was called **Build when a change is pushed to GitHub**.)</span></span>

   <span data-ttu-id="c0ad5-203">f.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-203">f.</span></span> <span data-ttu-id="c0ad5-204">**빌드 섹션** 아래 **빌드 단계 추가** 드롭다운에서 **Gradle 스크립트 호출** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-204">Under the **Build section**, from the drop-down **Add build step**, select the option **Invoke Gradle Script**.</span></span> <span data-ttu-id="c0ad5-205">제공된 위젯에서 사용자의 응용 프로그램에 대한 경로를 **루트 빌드 스크립트**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-205">In the widget that comes, specify the path to **Root build script** for your application.</span></span> <span data-ttu-id="c0ad5-206">그러면 지정된 경로에서 build.gradle을 선택하고 적절하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-206">It picks up build.gradle from the path specified, and works accordingly.</span></span> <span data-ttu-id="c0ad5-207">Eclipse 플러그 인 또는 Yeoman 생성기를 사용하여 ``MyActor``이라는 프로젝트를 만든 경우 루트 빌드 스크립트는 ``${WORKSPACE}/MyActor``를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-207">If you create a project named ``MyActor`` (using the Eclipse plug-in or Yeoman generator), the root build script should contain ``${WORKSPACE}/MyActor``.</span></span> <span data-ttu-id="c0ad5-208">이 기능을 표시한 예제는 다음 스크린샷을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-208">See the following screenshot for an example of what this looks like:</span></span>

    ![Service Fabric Jenkins 빌드 작업][build-step]

   <span data-ttu-id="c0ad5-210">g.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-210">g.</span></span> <span data-ttu-id="c0ad5-211">**빌드 후 작업** 드롭다운에서 **Service Fabric 프로젝트 배포**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-211">From the **Post-Build Actions** drop-down, select **Deploy Service Fabric Project**.</span></span> <span data-ttu-id="c0ad5-212">여기에서 Jenkins가 컴파일한 Service Fabric 응용 프로그램을 배포한 클러스터 세부 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-212">Here you need to provide cluster details where the Jenkins compiled Service Fabric application would be deployed.</span></span> <span data-ttu-id="c0ad5-213">또한 응용 프로그램을 배포하는 데 사용된 추가 응용 프로그램 세부 정보를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-213">You can also provide additional application details used to deploy the application.</span></span> <span data-ttu-id="c0ad5-214">이 기능을 표시한 예제는 다음 스크린샷을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-214">See the following screenshot for an example of what this looks like:</span></span>

    ![Service Fabric Jenkins 빌드 작업][post-build-step]

   > [!NOTE]
   > <span data-ttu-id="c0ad5-216">이 클러스터는 Service Fabric을 사용하여 Jenkins 컨테이너 이미지를 배포하는 경우에 Jenkins 컨테이너 응용 프로그램을 호스팅하는 것과 동일할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-216">The cluster here could be same as the one hosting the Jenkins container application, in case you are using Service Fabric to deploy the Jenkins container image.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="c0ad5-217">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c0ad5-217">Next steps</span></span>
<span data-ttu-id="c0ad5-218">이제 GitHub 및 Jenkins가 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-218">GitHub and Jenkins are now configured.</span></span> <span data-ttu-id="c0ad5-219">리포지토리 예제의 ``MyActor`` 프로젝트에서 일부 샘플을 변경하는 것을 고려합니다. https://github.com/sayantancs/SFJenkins</span><span class="sxs-lookup"><span data-stu-id="c0ad5-219">Consider making some sample change in your ``MyActor`` project in the repository example, https://github.com/sayantancs/SFJenkins.</span></span> <span data-ttu-id="c0ad5-220">원격 ``master`` 분기(또는 사용하도록 구성된 분기)에 변경 내용을 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-220">Push your changes to a remote ``master`` branch (or any branch that you have configured to work with).</span></span> <span data-ttu-id="c0ad5-221">사용자가 구성한 Jenkins 작업 ``MyJob``이 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-221">This triggers the Jenkins job, ``MyJob``, that you configured.</span></span> <span data-ttu-id="c0ad5-222">그러면 GitHub에서 변경 내용을 가져오고, 해당 내용을 빌드하고, 빌드 후 작업에서 지정한 클러스터 끝점으로 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="c0ad5-222">It fetches the changes from GitHub, builds them, and deploys the application to the cluster endpoint you specified in post-build actions.</span></span>  

  <!-- Images -->
  [build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/build-step.png
  [post-build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/post-build-step.png
