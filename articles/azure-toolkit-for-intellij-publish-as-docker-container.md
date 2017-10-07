---
title: "사용 하 여 Docker 컨테이너 aaaPublish IntelliJ에 대 한 Azure 도구 키트 hello | Microsoft Docs"
description: "자세한 내용은 toopublish 웹 앱 tooMicrosoft Docker 컨테이너를 사용 하 여 Azure IntelliJ에 대 한 Azure 도구 키트를 hello 하는 방법입니다."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: bee94cb269ea707ae7ad55232e23e915aec48c34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="01f14-103">IntelliJ에 대 한 hello Azure 도구 키트를 사용 하 여 Docker 컨테이너와 웹 응용 프로그램을 게시</span><span class="sxs-lookup"><span data-stu-id="01f14-103">Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="01f14-104">Docker 컨테이너는 웹 응용 프로그램을 배포하는 데 널리 사용되는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="01f14-105">Docker 컨테이너를 사용 하 여 개발자는 모든 프로젝트 파일 및 종속성을 배포 tooa 서버에 대 한 단일 패키지를 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment tooa server.</span></span> <span data-ttu-id="01f14-106">hello IntelliJ 용 Azure 도구 키트를 추가 하 여 Java 개발자를 위한이 프로세스를 간소화 *Docker 컨테이너로 게시* 배포 tooMicrosoft Azure에 대 한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-106">hello Azure Toolkit for IntelliJ simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment tooMicrosoft Azure.</span></span> <span data-ttu-id="01f14-107">이 문서 안내 hello 단계 필요한 toopublish 응용 프로그램 tooAzure Docker 컨테이너.</span><span class="sxs-lookup"><span data-stu-id="01f14-107">This article walks you through hello steps required toopublish your applications tooAzure as Docker containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="01f14-108">Docker에 대 한 자세한 정보는 hello [Docker 웹 사이트]합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-108">More information about Docker is available on hello [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="01f14-109">Docker 컨테이너를 사용 하 여 웹 응용 프로그램 tooAzure 게시</span><span class="sxs-lookup"><span data-stu-id="01f14-109">Publish your web app tooAzure by using a Docker container</span></span>

> [!NOTE]
> * <span data-ttu-id="01f14-110">toopublish 웹 앱 배포 준비 아티팩트를 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-110">toopublish your web app, you must create a deployment-ready artifact.</span></span> <span data-ttu-id="01f14-111">toolearn hello을 더 참조 [아티팩트 만들기에 대 한 자세한 내용은](#artifacts) 섹션.</span><span class="sxs-lookup"><span data-stu-id="01f14-111">toolearn more, see hello [Additional information about creating artifacts](#artifacts) section.</span></span>
>
> * <span data-ttu-id="01f14-112">Hello 배포 마법사를 한 번 이상 완료 한 후 hello 마법사를 다시 실행 하는 경우 대부분의 사용자 설정이 기본값으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-112">After you have completed hello deployment wizard at least once, most of your settings are used as defaults when you run hello wizard again.</span></span>
>

1. <span data-ttu-id="01f14-113">IntelliJ의 웹앱 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-113">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="01f14-114">toostart hello **Docker 컨테이너로 게시** 마법사 hello 다음 중 하나를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-114">toostart hello **Publish as Docker Container** wizard, do either of hello following:</span></span>

   * <span data-ttu-id="01f14-115">Hello에 **프로젝트** 도구 창 프로젝트를 마우스 오른쪽 단추로 클릭 하 여 **Azure**, 클릭 하 고 **Docker 컨테이너로 게시**:</span><span class="sxs-lookup"><span data-stu-id="01f14-115">In hello **Project** tool window, right-click your project, click **Azure**, and then click **Publish as Docker Container**:</span></span>

      ![hello Docker 컨테이너 명령으로 게시][PUB01]

   * <span data-ttu-id="01f14-117">도구 모음의 hello IntelliJ 클릭 hello **게시 그룹** 단추를 선택한 다음 클릭 **Docker 컨테이너로 게시**:</span><span class="sxs-lookup"><span data-stu-id="01f14-117">On hello IntelliJ toolbar, click hello **Publish Group** button, and then click **Publish as Docker Container**:</span></span>

      <span data-ttu-id="01f14-118">![hello Docker 컨테이너 명령으로 게시][PUB02]</span><span class="sxs-lookup"><span data-stu-id="01f14-118">![hello Publish as Docker Container command][PUB02]</span></span>  
    <span data-ttu-id="01f14-119">hello **Azure에서 Docker 컨테이너 배포** 마법사가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-119">hello **Deploy Docker Container on Azure** wizard opens.</span></span>

   ![hello Azure 마법사에서 Docker 컨테이너 배포][PUB03]

3. <span data-ttu-id="01f14-121">Hello에 **이미지 이름을 입력 hello 아티팩트 경로 선택 하 고 사용 되는 Docker 호스트 toobe 확인** 창에서 다음 hello지 않습니다:</span><span class="sxs-lookup"><span data-stu-id="01f14-121">In hello **Type an image name, select hello artifact's path and check a Docker host toobe used** window, do hello following:</span></span> 

   <span data-ttu-id="01f14-122">a.</span><span class="sxs-lookup"><span data-stu-id="01f14-122">a.</span></span> <span data-ttu-id="01f14-123">Hello에 **Docker 이미지 이름** 상자 Docker 호스트에 대 한 고유 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-123">In hello **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="01f14-124">(hello를 이름으로 자동으로 만듭니다 있지만 수정할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="01f14-124">(hello wizard automatically creates a name, but you can modify it.)</span></span> 

   <span data-ttu-id="01f14-125">b.</span><span class="sxs-lookup"><span data-stu-id="01f14-125">b.</span></span> <span data-ttu-id="01f14-126">hello **호스트** Docker 호스트를 이미 만든 영역에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-126">hello **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="01f14-127">Hello 다음 중 하나를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-127">Do either of hello following:</span></span> 
      * <span data-ttu-id="01f14-128">기존 Docker 호스트를 사용 하도록 설정한 경우 웹 앱 tooit을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-128">If you have an existing Docker host, you can deploy your web app tooit.</span></span>
      * <span data-ttu-id="01f14-129">Docker 호스트 toocreate hello 녹색 더하기 기호를 클릭 합니다. (**+**).</span><span class="sxs-lookup"><span data-stu-id="01f14-129">toocreate a Docker host, click hello green plus sign (**+**).</span></span>  
       <span data-ttu-id="01f14-130">hello **Docker 호스트 만들기** 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-130">hello **Create Docker Host** dialog box opens.</span></span> 

      ![Azure에 Docker 컨테이너 배포 마법사][PUB04a]

4. <span data-ttu-id="01f14-132">Hello에 **hello 새 가상 컴퓨터 구성** 창의 hello 다음 Docker 호스트에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-132">In hello **Configure hello new virtual machine** window, provide hello following information about your Docker host.</span></span> <span data-ttu-id="01f14-133">(대부분의 사용자에 대 한 hello 정보를 자동으로 생성 하는 hello 마법사 있지만 그 중 하나를 수정할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="01f14-133">(hello wizard automatically generates most of hello information for you, but you can modify any of them.)</span></span> 

   <span data-ttu-id="01f14-134">a.</span><span class="sxs-lookup"><span data-stu-id="01f14-134">a.</span></span> <span data-ttu-id="01f14-135">Hello에 **이름** 상자 hello Docker 호스트에 대 한 고유 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-135">In hello **Name** box, enter a unique name for hello Docker host.</span></span> <span data-ttu-id="01f14-136">(이 하지 hello hello Docker 이미지 이름을 이전에 지정한 것과 동일 합니다.)</span><span class="sxs-lookup"><span data-stu-id="01f14-136">(It is not hello same as hello Docker image name that you specified earlier.)</span></span> 
    
   <span data-ttu-id="01f14-137">b.</span><span class="sxs-lookup"><span data-stu-id="01f14-137">b.</span></span> <span data-ttu-id="01f14-138">Hello에 **구독** 상자 hello 호스트에 사용 하는 Azure 구독을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-138">In hello **Subscription** box, enter hello Azure subscription that you use for your host.</span></span> 
      
   <span data-ttu-id="01f14-139">c.</span><span class="sxs-lookup"><span data-stu-id="01f14-139">c.</span></span> <span data-ttu-id="01f14-140">Hello에 **지역** 상자에 호스트에 위치한 hello 지리적 위치 영역을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-140">In hello **Region** box, enter hello geographical region where your host is located.</span></span>
      
   <span data-ttu-id="01f14-141">d.</span><span class="sxs-lookup"><span data-stu-id="01f14-141">d.</span></span> <span data-ttu-id="01f14-142">Hello에 **OS 및 크기** 탭에서 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-142">On hello **OS and Size** tab, do hello following:</span></span>      
      * <span data-ttu-id="01f14-143">**호스트 OS**: 호스트에 포함 된 hello 가상 컴퓨터에 대 한 hello 운영 체제를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-143">**Host OS**: Enter hello operating system for hello virtual machine that contains your host.</span></span> 
      * <span data-ttu-id="01f14-144">**크기**: 호스트에 대 한 hello 가상 컴퓨터 크기를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-144">**Size**: Enter hello virtual-machine size for your host.</span></span>   
       
   <span data-ttu-id="01f14-145">e.</span><span class="sxs-lookup"><span data-stu-id="01f14-145">e.</span></span> <span data-ttu-id="01f14-146">Hello에 **리소스 그룹** 탭 hello 다음 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-146">On hello **Resource Group** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="01f14-147">**새 리소스 그룹**: 호스트에 사용할 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-147">**New resource group**: Create a resource group for your host.</span></span>
      * <span data-ttu-id="01f14-148">**기존 리소스 그룹**: Azure 계정에서 기존 리소스 그룹을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-148">**Existing resource group**: Specify an existing resource group from your Azure account.</span></span> 
       
   <span data-ttu-id="01f14-149">f.</span><span class="sxs-lookup"><span data-stu-id="01f14-149">f.</span></span> <span data-ttu-id="01f14-150">Hello에 **네트워크** 탭 hello 다음 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-150">On hello **Network** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="01f14-151">**새 가상 네트워크**: 호스트에 사용할 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-151">**New virtual network**: Create a virtual network for your host.</span></span>
      * <span data-ttu-id="01f14-152">**기존 가상 네트워크**: Azure 계정에서 기존 가상 네트워크를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-152">**Existing virtual network**: Specify an existing virtual network from your Azure account.</span></span> 
       
   <span data-ttu-id="01f14-153">g.</span><span class="sxs-lookup"><span data-stu-id="01f14-153">g.</span></span> <span data-ttu-id="01f14-154">Hello에 **저장소** 탭 hello 다음 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-154">On hello **Storage** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="01f14-155">**새 저장소 계정**: 호스트에 사용할 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-155">**New storage account**: Create a storage account for your host.</span></span>
      * <span data-ttu-id="01f14-156">**기존 저장소 계정**: Azure 계정에서 기존 저장소 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-156">**Existing storage account**: Specify an existing storage account from your Azure account.</span></span>
       
5. <span data-ttu-id="01f14-157">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-157">Click **Next**.</span></span>  
     <span data-ttu-id="01f14-158">hello **자격 증명에 로그를 구성 및 포트 설정이** 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-158">hello **Configure log in credentials and port settings** window opens.</span></span>

      ![자격 증명 및 포트 설정 창에서 hello 구성 로그][PUB05]

6. <span data-ttu-id="01f14-160">Hello 다음 옵션 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-160">Select one of hello following options:</span></span>

      * <span data-ttu-id="01f14-161">**Azure Key Vault에서 자격 증명 가져오기**: Azure 구독에 저장되어 있는 이전에 저장한 자격 증명 집합을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-161">**Import credentials from Azure Key Vault**: Specify a previously saved set of credentials that are stored in your Azure subscription.</span></span>

          > [!NOTE]
          > <span data-ttu-id="01f14-162">특정 계정 또는 서비스 사용자를 사용 하 여 만든는 Azure 키 자격 증명 모음에 다른 계정 또는 서비스 사용자 hello 구독을 공유 하 여 자동으로 액세스할 수 없는 경우</span><span class="sxs-lookup"><span data-stu-id="01f14-162">An Azure key vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares hello subscription.</span></span> <span data-ttu-id="01f14-163">다른 계정 또는 서비스 보안 주체 toouse hello 키 자격 증명 모음 tooallow hello Azure 포털 tooadd hello 계정 또는 서비스 사용자를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-163">tooallow another account or service principal toouse hello key vault, you must use hello Azure portal tooadd hello account or service principal.</span></span>

      * <span data-ttu-id="01f14-164">**새 로그인 자격 증명**: 새 로그인 자격 증명 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-164">**New log in credentials**: Create a new set of login credentials.</span></span> <span data-ttu-id="01f14-165">이 옵션을 선택 하는 경우 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-165">If you select this option, do hello following:</span></span>

        <span data-ttu-id="01f14-166">a.</span><span class="sxs-lookup"><span data-stu-id="01f14-166">a.</span></span> <span data-ttu-id="01f14-167">Hello에 **VM 자격 증명** 탭 hello 다음 Docker 호스트의 가상 컴퓨터 로그인 자격 증명 hello에 대 한 정보를 제공 합니다: * **Username**: 가상 컴퓨터 로그인에 대 한 hello 사용자 이름 입력 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-167">On hello **VM Credentials** tab, provide hello following information for hello virtual-machine login credentials of your Docker host: * **Username**: Enter hello username for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="01f14-168">* **암호** 및 **Confirm**: 가상 컴퓨터 로그인 자격 증명에 대 한 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-168">* **Password** and **Confirm**: Enter hello password for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="01f14-169">* **SSH**: Docker 호스트에 대 한 hello SSH (보안 셸) 설정을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-169">* **SSH**: Enter hello Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="01f14-170">Hello 다음 옵션 중 하나를 선택할 수 있습니다: * **None**: 가상 컴퓨터에 SSH 연결을 허용 하지 않는 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-170">You can select one of hello following options: * **None**: Specifies that your virtual machine does not allow SSH connections.</span></span>
                <span data-ttu-id="01f14-171">* **자동 생성**: SSH를 통해 연결 하기 위한 hello 필수 설정을 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-171">* **Auto-generate**: Automatically creates hello requisite settings for connecting via SSH.</span></span>
                <span data-ttu-id="01f14-172">* **디렉터리에서 가져오기**: 이전에 저장 된 SSH 설정 집합이 포함 된 디렉터리 toospecify 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-172">* **Import from directory**: Allows you toospecify a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="01f14-173">hello 디렉터리 hello 다음 두 개의 파일이 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-173">hello directory must contain hello following two files:</span></span>
                
                  * *id_rsa*: Contains hello RSA identification for a user.
                  * *id_rsa.pub*: Contains hello RSA public key that is used for authentication.
            
        <span data-ttu-id="01f14-174">b.</span><span class="sxs-lookup"><span data-stu-id="01f14-174">b.</span></span> <span data-ttu-id="01f14-175">Hello에 **Docker 디먼 액세스** 탭 hello 다음 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-175">On hello **Docker Daemon Access** tab, provide hello following information:</span></span>

          ![Docker 호스트 만들기][PUB06]
    
             * **Docker Daemon port**: Enter hello unique TCP port for your Docker host.
             * **TLS Security**: Enter hello Transport Layer Security settings for your Docker host. You can choose from hello following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. hello directory must contain hello following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain hello client certificate and public key that is used for TLS authentication.

7. <span data-ttu-id="01f14-177">Hello 필요한 정보를 입력 한 후 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-177">After you have entered hello required information, click **Finish**.</span></span>  
    <span data-ttu-id="01f14-178">hello **Azure에서 Docker 컨테이너 배포** 마법사가 다시 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-178">hello **Deploy Docker Container on Azure** wizard reappears.</span></span>

   ![Azure에 Docker 컨테이너 배포 마법사][PUB07]

8. <span data-ttu-id="01f14-180">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-180">Click **Next**.</span></span>  
    <span data-ttu-id="01f14-181">hello **hello Docker 컨테이너 toobe 만든 구성** 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-181">hello **Configure hello Docker container toobe created** window opens.</span></span>

   ![hello 구성 hello Docker 컨테이너 toobe 만든 창][PUB08]

9. <span data-ttu-id="01f14-183">Hello에 **hello Docker 컨테이너 toobe 만든 구성** 창 hello 다음 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-183">In hello **Configure hello Docker container toobe created** window, provide hello following information:</span></span> 

   <span data-ttu-id="01f14-184">a.</span><span class="sxs-lookup"><span data-stu-id="01f14-184">a.</span></span> <span data-ttu-id="01f14-185">Hello에 **Docker 컨테이너 이름을** 상자 Docker 컨테이너에 대 한 고유 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-185">In hello **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="01f14-186">b.</span><span class="sxs-lookup"><span data-stu-id="01f14-186">b.</span></span> <span data-ttu-id="01f14-187">Hello Docker 이미지를 다음 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-187">Choose one of hello following Docker images:</span></span> 

      * <span data-ttu-id="01f14-188">**미리 정의된 Docker 이미지**: Azure에서 기존 Docker 이미지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-188">**Predefined Docker image**: Specify a pre-existing Docker image from Azure.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="01f14-189">이 상자에서 Docker 이미지 hello 목록은 여러 그림으로 구성 된 Azure 도구 키트는 hello 구성 toopatch 프로그램 아티팩트가 자동으로 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-189">hello list of Docker images in this box consists of several images that hello Azure Toolkit has been configured toopatch so that your artifact is deployed automatically.</span></span> 

      * <span data-ttu-id="01f14-190">**사용자 지정 Dockerfile**: 로컬 컴퓨터에서 이전에 저장된 Dockerfile을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-190">**Custom Dockerfile**: Specify a previously saved Dockerfile from your local computer.</span></span>

        > [!NOTE]
        > <span data-ttu-id="01f14-191">이 기능은 toodeploy 자신의 Dockerfile 알아보려는 개발자를 위한 보다 고급입니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-191">This is a more advanced feature for developers who want toodeploy their own Dockerfile.</span></span> <span data-ttu-id="01f14-192">그러나 toodevelopers 자신의 Dockerfile 제대로 빌드는이 옵션 tooensure를 사용 하는 중일으로 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-192">However, it is up toodevelopers who use this option tooensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="01f14-193">Hello Azure 도구 키트는 사용자 지정 Dockerfile의 hello 콘텐츠 유효성을 검사 하지 않습니다, hello Dockerfile에 문제가 hello 배포가 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-193">Because hello Azure Toolkit does not validate hello content in a custom Dockerfile, hello deployment might fail if hello Dockerfile has issues.</span></span> <span data-ttu-id="01f14-194">또한 hello Azure 도구 키트에서 Dockerfile toocontain를 사용자 지정 하는 hello. 웹 응용 프로그램 아티팩트를 기대 하기 때문에 tooopen HTTP 연결 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-194">In addition, because hello Azure Toolkit expects hello custom Dockerfile toocontain a web app artifact, it attempts tooopen an HTTP connection.</span></span> <span data-ttu-id="01f14-195">개발자가 다른 아티팩트 형식을 게시하는 경우 배포 후에 무해한 오류가 표시될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-195">If developers publish a different type of artifact, they might receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="01f14-196">c.</span><span class="sxs-lookup"><span data-stu-id="01f14-196">c.</span></span> <span data-ttu-id="01f14-197">Hello에 **포트 설정을** 상자 Docker 컨테이너에 대 한 hello 고유 TCP 포트 바인딩을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-197">In hello **Port settings** box, enter hello unique TCP port binding for your Docker container.</span></span> 

10. <span data-ttu-id="01f14-198">Hello 이전 단계를 완료 한 후 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-198">After you have completed hello preceding steps, click **Finish**.</span></span> 

<span data-ttu-id="01f14-199">hello Azure 도구 키트는 Docker 컨테이너에 웹 앱 tooAzure 프로그램 배포를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-199">hello Azure Toolkit begins deploying your web app tooAzure in a Docker container.</span></span> <span data-ttu-id="01f14-200">IntelliJ toobe hello 백그라운드에서 배포를 구성 하지 않으면는 **tooAzure 배포** 진행률 표시줄이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-200">Unless you have configured IntelliJ toobe deployed in hello background, a **Deploying tooAzure** progress bar appears.</span></span> 

![hello 배포 진행률 표시줄][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a><span data-ttu-id="01f14-202">아티팩트 가져오기에 대한 추가 정보</span><span class="sxs-lookup"><span data-stu-id="01f14-202">Additional information about creating artifacts</span></span>

<span data-ttu-id="01f14-203">배포 준비 아티팩트 toocreate 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-203">toocreate a deployment-ready artifact, do hello following:</span></span>

1. <span data-ttu-id="01f14-204">IntelliJ의 웹앱 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-204">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="01f14-205">**파일**을 클릭한 다음 **프로젝트 구조**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-205">Click **File**, and then click **Project Structure**.</span></span>

   ![hello 프로젝트 구조 명령][ART01]

3. <span data-ttu-id="01f14-207">아티팩트를 프로그램 tooadd hello 녹색 더하기 기호를 클릭 합니다. (**+**)를 클릭 하 고 **웹 응용 프로그램: 보관**합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-207">tooadd an artifact, click hello green plus sign (**+**), and then click **Web Application: Archive**.</span></span>

   ![hello "웹 응용 프로그램:: 보관" 명령][ART02]

4. <span data-ttu-id="01f14-209">Hello에 **이름** 상자 프로그램 아티팩트에 대 한 이름을 입력 합니다 (hello를 넣지 마십시오 *.war* 확장)를 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-209">In hello **Name** box, enter a name for your artifact (do not include hello *.war* extension), and then click **OK**.</span></span>

   ![hello 아티팩트 이름 상자][ART03]

<span data-ttu-id="01f14-211">IntelliJ에서 아티팩트를 만드는 방법에 대 한 자세한 내용은 참조 [아티팩트 구성] hello JetBrains 웹 사이트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-211">For more information about creating artifacts in IntelliJ, see [Configuring artifacts] on hello JetBrains website.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01f14-212">다음 단계</span><span class="sxs-lookup"><span data-stu-id="01f14-212">Next steps</span></span>
<span data-ttu-id="01f14-213">Java Ide에 대 한 hello Azure 도구 키트에 대 한 자세한 내용은 hello 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="01f14-213">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="01f14-214">[Eclipse용 Azure 도구 키트]</span><span class="sxs-lookup"><span data-stu-id="01f14-214">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="01f14-215">[Hello Eclipse 용 Azure 도구 키트의에서 새로운 기능]</span><span class="sxs-lookup"><span data-stu-id="01f14-215">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="01f14-216">[Hello Eclipse 용 Azure 도구 키트 설치]</span><span class="sxs-lookup"><span data-stu-id="01f14-216">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="01f14-217">[Eclipse 용 Azure 도구 키트 hello에 대 한 로그인 지침]</span><span class="sxs-lookup"><span data-stu-id="01f14-217">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="01f14-218">[Eclipse에서 Azure용 Hello World 웹앱 만들기]</span><span class="sxs-lookup"><span data-stu-id="01f14-218">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="01f14-219">[IntelliJ용 Azure 도구 키트]</span><span class="sxs-lookup"><span data-stu-id="01f14-219">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="01f14-220">[Hello IntelliJ 용 Azure 도구 키트의에서 새로운 기능]</span><span class="sxs-lookup"><span data-stu-id="01f14-220">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="01f14-221">[IntelliJ 용 hello Azure 도구 키트 설치]</span><span class="sxs-lookup"><span data-stu-id="01f14-221">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="01f14-222">[로그인에 대 한 지침 Azure 도구 키트 hello IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="01f14-222">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="01f14-223">[IntelliJ에서 Azure용 Hello World 웹앱 만들기]</span><span class="sxs-lookup"><span data-stu-id="01f14-223">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="01f14-224">Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터] 및 hello [Visual Studio Team Services에 대 한 Java 도구]합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-224">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="01f14-225">Docker에 대 한 추가 리소스에 대 한 참조 hello 공식 [Docker 웹 사이트]합니다.</span><span class="sxs-lookup"><span data-stu-id="01f14-225">For additional resources for Docker, see hello official [Docker website].</span></span>

<!-- URL List -->

[Eclipse용 Azure 도구 키트]: ./azure-toolkit-for-eclipse.md
[IntelliJ용 Azure 도구 키트]: ./azure-toolkit-for-intellij.md
[Eclipse에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[IntelliJ에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Hello Eclipse 용 Azure 도구 키트 설치]: ./azure-toolkit-for-eclipse-installation.md
[IntelliJ 용 hello Azure 도구 키트 설치]: ./azure-toolkit-for-intellij-installation.md
[Eclipse 용 Azure 도구 키트 hello에 대 한 로그인 지침]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[로그인에 대 한 지침 Azure 도구 키트 hello IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Hello Eclipse 용 Azure 도구 키트의에서 새로운 기능]: ./azure-toolkit-for-eclipse-whats-new.md
[Hello IntelliJ 용 Azure 도구 키트의에서 새로운 기능]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/
[Visual Studio Team Services에 대 한 Java 도구]: https://java.visualstudio.com/

[Docker 웹 사이트]: https://www.docker.com/
[아티팩트 구성]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB08.png
[PUB09]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB09.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART03.png
