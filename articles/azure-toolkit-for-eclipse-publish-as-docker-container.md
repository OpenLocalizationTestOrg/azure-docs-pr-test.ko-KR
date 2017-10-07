---
title: "사용 하 여 Docker 컨테이너 aaaPublish hello Azure Toolkit for Eclipse | Microsoft Docs"
description: "자세한 방법을 사용 하 여 Docker 컨테이너도 Azure는 웹 응용 프로그램 tooMicrosoft toopublish hello Azure Toolkit for Eclipse."
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
ms.openlocfilehash: 53ec3a7f7a171691024e03622fd48d6f1e257b50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="39932-103">Eclipse 용 Azure 도구 키트 hello를 사용 하 여 Docker 컨테이너와 웹 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="39932-103">Publish a web app as a Docker container by using hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="39932-104">Docker 컨테이너는 웹 응용 프로그램을 배포하는 데 널리 사용되는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="39932-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="39932-105">Docker 컨테이너를 사용 하 여 개발자는 모든 프로젝트 파일 및 종속성을 배포 tooa 서버에 대 한 단일 패키지를 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39932-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment tooa server.</span></span> <span data-ttu-id="39932-106">Azure Toolkit for Eclipse hello를 추가 하 여 Java 개발자를 위한이 프로세스를 간소화 *Docker 컨테이너로 게시* 배포 tooMicrosoft Azure에 대 한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="39932-106">hello Azure Toolkit for Eclipse simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment tooMicrosoft Azure.</span></span> <span data-ttu-id="39932-107">이 문서 안내 hello 단계 필요한 toopublish 응용 프로그램 tooAzure Docker 컨테이너.</span><span class="sxs-lookup"><span data-stu-id="39932-107">This article walks you through hello steps required toopublish your applications tooAzure as Docker containers.</span></span>

> [!NOTE]
> <span data-ttu-id="39932-108">Docker에 대 한 자세한 정보는 hello [Docker 웹 사이트]합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-108">More information about Docker is available on hello [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="39932-109">Docker 컨테이너를 사용 하 여 웹 응용 프로그램 tooAzure 게시</span><span class="sxs-lookup"><span data-stu-id="39932-109">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="39932-110">Eclipse의 웹앱 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="39932-110">Open your web app project in Eclipse.</span></span>

2. <span data-ttu-id="39932-111">toostart hello **Docker 컨테이너로 게시** 마법사 hello 다음 중 하나를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-111">toostart hello **Publish as Docker Container** wizard, do either of hello following:</span></span>

   * <span data-ttu-id="39932-112">Hello에 **탐색기** 볼 프로젝트를 마우스 오른쪽 단추로 클릭 하 여 **Azure**, 클릭 하 고 **Docker 컨테이너로 게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-112">In hello **Navigator** view, right-click your project, click **Azure**, and then click **Publish as Docker Container**.</span></span>

      ![탐색기 보기 Docker 컨테이너 명령으로 게시][PUB01]

   * <span data-ttu-id="39932-114">Hello Eclipse 도구 모음에서 hello **게시** 단추를 선택한 다음 클릭 **Docker 컨테이너로 게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-114">On hello Eclipse toolbar, click hello **Publish** button, and then click **Publish as Docker Container**.</span></span>

      ![Eclipse 도구 모음 Docker 컨테이너 명령으로 게시][PUB02]
      
    <span data-ttu-id="39932-116">hello **Azure에서 Docker 컨테이너 배포** 마법사가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="39932-116">hello **Deploy Docker Container on Azure** wizard opens.</span></span>

    ![hello Azure 마법사에서 Docker 컨테이너 배포][PUB03]

3. <span data-ttu-id="39932-118">Hello에 **이미지 이름을 입력 hello 아티팩트 경로 선택 하 고 사용 되는 Docker 호스트 toobe 확인** 창에서 다음 hello지 않습니다:</span><span class="sxs-lookup"><span data-stu-id="39932-118">In hello **Type an image name, select hello artifact's path and check a Docker host toobe used** window, do hello following:</span></span>

    <span data-ttu-id="39932-119">a.</span><span class="sxs-lookup"><span data-stu-id="39932-119">a.</span></span> <span data-ttu-id="39932-120">Hello에 **Docker 이미지 이름** 상자 Docker 호스트에 대 한 고유 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-120">In hello **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="39932-121">(hello를 이름으로 자동으로 만듭니다 있지만 수정할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="39932-121">(hello wizard automatically creates a name, but you can modify it.)</span></span>

    <span data-ttu-id="39932-122">b.</span><span class="sxs-lookup"><span data-stu-id="39932-122">b.</span></span> <span data-ttu-id="39932-123">hello **호스트** Docker 호스트를 이미 만든 영역에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39932-123">hello **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="39932-124">Hello 다음 중 하나를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-124">Do either of hello following:</span></span>

    * <span data-ttu-id="39932-125">기존 Docker 호스트를 사용 하도록 설정한 경우 웹 앱 tooit을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39932-125">If you have an existing Docker host, you can deploy your web app tooit.</span></span>
    * <span data-ttu-id="39932-126">새 Docker 호스트 toocreate 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-126">toocreate a new Docker host, click **Add**.</span></span>  
      
    <span data-ttu-id="39932-127">hello **Docker 호스트 만들기** 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="39932-127">hello **Create Docker Host** dialog box opens.</span></span>

    ![Azure에 Docker 컨테이너 배포 마법사][PUB04a]

4. <span data-ttu-id="39932-129">Hello에 **hello 새 가상 컴퓨터 구성** 창의 hello 다음 Docker 호스트에 대 한 옵션을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-129">In hello **Configure hello new virtual machine** window, specify hello following options for your Docker host.</span></span> <span data-ttu-id="39932-130">(hello 마법사, hello 옵션의 대부분을 자동으로 생성 하지만 그 중 하나를 수정할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="39932-130">(hello wizard automatically generates most of hello options for you, but you can modify any of them.)</span></span>

   <span data-ttu-id="39932-131">a.</span><span class="sxs-lookup"><span data-stu-id="39932-131">a.</span></span> <span data-ttu-id="39932-132">**이름**: hello Docker 호스트에 대 한 고유한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-132">**Name**: Enter a unique name for hello Docker host.</span></span> <span data-ttu-id="39932-133">(이 하지 hello hello Docker 이미지 이름을 이전에 지정한 것과 동일 합니다.)</span><span class="sxs-lookup"><span data-stu-id="39932-133">(It is not hello same as hello Docker image name that you specified earlier.)</span></span>

   <span data-ttu-id="39932-134">b.</span><span class="sxs-lookup"><span data-stu-id="39932-134">b.</span></span> <span data-ttu-id="39932-135">**구독**: hello 호스트에 사용 하는 Azure 구독을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-135">**Subscription**: Enter hello Azure subscription that you use for your host.</span></span>

   <span data-ttu-id="39932-136">c.</span><span class="sxs-lookup"><span data-stu-id="39932-136">c.</span></span> <span data-ttu-id="39932-137">**지역**: 호스트에 위치한 hello 지리적 지역을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-137">**Region**: Enter hello geographical region where your host is located.</span></span>

   <span data-ttu-id="39932-138">d.</span><span class="sxs-lookup"><span data-stu-id="39932-138">d.</span></span> <span data-ttu-id="39932-139">Hello에 **호스트 OS 및 크기** 탭:</span><span class="sxs-lookup"><span data-stu-id="39932-139">On hello **Host OS and Size** tab:</span></span>
     * <span data-ttu-id="39932-140">**호스트 OS**: 호스트에 포함 된 hello 가상 컴퓨터에 대 한 hello 운영 체제를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-140">**Host OS**: Enter hello operating system for hello virtual machine that contains your host.</span></span>
     * <span data-ttu-id="39932-141">**크기**: 호스트에 대 한 hello 가상 컴퓨터 크기를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-141">**Size**: Enter hello virtual-machine size for your host.</span></span>

   <span data-ttu-id="39932-142">e.</span><span class="sxs-lookup"><span data-stu-id="39932-142">e.</span></span> <span data-ttu-id="39932-143">Hello에 **리소스 그룹** 탭:</span><span class="sxs-lookup"><span data-stu-id="39932-143">On hello **Resource Group** tab:</span></span>
     * <span data-ttu-id="39932-144">**새 리소스 그룹**: 호스트에 사용할 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39932-144">**New resource group**: Create a new resource group for your host.</span></span>
     * <span data-ttu-id="39932-145">**기존 리소스 그룹**: Azure 계정에서 기존 리소스 그룹을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-145">**Existing resource group**: Enter an existing resource group from your Azure account.</span></span>

   <span data-ttu-id="39932-146">f.</span><span class="sxs-lookup"><span data-stu-id="39932-146">f.</span></span> <span data-ttu-id="39932-147">Hello에 **네트워크** 탭:</span><span class="sxs-lookup"><span data-stu-id="39932-147">On hello **Network** tab:</span></span>
     * <span data-ttu-id="39932-148">**새 가상 네트워크**: 호스트에 사용할 새 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39932-148">**New virtual network**: Create a new virtual network for your host.</span></span>
     * <span data-ttu-id="39932-149">**기존 가상 네트워크**: Azure 계정에서 기존 가상 네트워크를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-149">**Existing virtual network**: Enter an existing virtual network from your Azure account.</span></span>

   <span data-ttu-id="39932-150">g.</span><span class="sxs-lookup"><span data-stu-id="39932-150">g.</span></span> <span data-ttu-id="39932-151">Hello에 **저장소** 탭:</span><span class="sxs-lookup"><span data-stu-id="39932-151">On hello **Storage** tab:</span></span>
     * <span data-ttu-id="39932-152">**새 저장소 계정**: 호스트에 사용할 새 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39932-152">**New storage account**: Create a new storage account for your host.</span></span>
     * <span data-ttu-id="39932-153">**기존 저장소 계정**: Azure 계정에서 기존 저장소 계정을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-153">**Existing storage account**: Enter an existing storage account from your Azure account.</span></span>

5. <span data-ttu-id="39932-154">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="39932-154">Click **Next**.</span></span>

6. <span data-ttu-id="39932-155">Hello에 **자격 증명에 로그를 구성 및 포트 설정이** 창의 hello 다음 옵션 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-155">In hello **Configure log in credentials and port settings** window, select one of hello following options:</span></span>

    * <span data-ttu-id="39932-156">**Azure Key Vault에서 자격 증명 가져오기**: Azure 구독에 저장되어 있는 이전에 저장한 자격 증명 집합을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-156">**Import credentials from Azure Key Vault**: Specifies a previously saved set of credentials that are stored in your Azure subscription.</span></span>

      >[!NOTE]
      ><span data-ttu-id="39932-157">Azure 키 자격 증명 모음 특정 계정 또는 서비스 사용자를 사용 하 여 만든 다른 계정 또는 서비스 hello 구독을 공유 하는 사용자가 자동으로 액세스할 수 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-157">An Azure Key Vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares hello subscription.</span></span> <span data-ttu-id="39932-158">tooallow 다른 계정 또는 서비스 보안 주체 toouse 주요 자격 증명 모음 hello hello Azure 포털 tooadd hello 계정 또는 서비스 사용자를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-158">tooallow another account or service principal toouse hello Key Vault, you must use hello Azure portal tooadd hello account or service principal.</span></span>

    * <span data-ttu-id="39932-159">**새 로그인 자격 증명**: 새 로그인 자격 증명 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39932-159">**New log in credentials**: Creates a new set of login credentials.</span></span> <span data-ttu-id="39932-160">이 옵션을 선택 하는 경우 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="39932-160">If you select this option, do hello following:</span></span>
    
      * <span data-ttu-id="39932-161">Hello에 **VM 자격 증명** 탭에서 Docker 호스트의 가상 컴퓨터 로그인 자격 증명을 hello에 대 한 옵션 hello 다음 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-161">On hello **VM Credentials** tab, choose one of hello following options for hello virtual-machine login credentials of your Docker host:</span></span>

          * <span data-ttu-id="39932-162">**사용자 이름**: 가상 컴퓨터 로그인 자격 증명에 대 한 hello 사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-162">**Username**: Enter hello username for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="39932-163">**암호** 및 **Confirm**: 가상 컴퓨터 로그인 자격 증명에 대 한 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-163">**Password** and **Confirm**: Enter hello password for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="39932-164">**SSH**: Docker 호스트에 대 한 hello SSH (보안 셸) 설정을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-164">**SSH**: Enter hello Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="39932-165">Hello 다음 옵션에서에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39932-165">You can choose from hello following options:</span></span>
            * <span data-ttu-id="39932-166">**없음**: 가상 컴퓨터에서 SSH 연결을 허용하지 않게 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-166">**None**: Specifies that your virtual machine will not allow SSH connections.</span></span>
            * <span data-ttu-id="39932-167">**자동 생성**: SSH를 통해 연결 하기 위한 hello 필수 설정을 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39932-167">**Auto-generate**: Automatically creates hello requisite settings for connecting via SSH.</span></span>
            * <span data-ttu-id="39932-168">**디렉터리에서 가져오기**: 이전에 저장된 SSH 설정 집합을 포함하는 디렉터리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-168">**Import from directory**: Specifies a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="39932-169">hello 디렉터리 hello 다음 두 개의 파일이 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-169">hello directory must contain hello following two files:</span></span>
                * <span data-ttu-id="39932-170">*id_rsa*: 사용자에 대 한 hello RSA id를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-170">*id_rsa*: Contains hello RSA identification for a user.</span></span>
                * <span data-ttu-id="39932-171">*id_rsa.pub*: 인증에 사용 되는 hello RSA 공개 키를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-171">*id_rsa.pub*: Contains hello RSA public key that is used for authentication.</span></span>
        
        ![Docker 호스트 만들기][PUB05]

      * <span data-ttu-id="39932-173">Hello에 **Docker 디먼 자격 증명** 탭 hello 다음 옵션을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-173">On hello **Docker Daemon Credentials** tab, specify hello following options:</span></span>

          * <span data-ttu-id="39932-174">**Docker 데몬 포트**: Docker 호스트에 대 한 hello 고유 TCP 포트를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-174">**Docker Daemon port**: Enter hello unique TCP port for your Docker host.</span></span>
          * <span data-ttu-id="39932-175">**TLS 보안**: Docker 호스트에 대 한 hello 전송 계층 보안 설정을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-175">**TLS Security**: Enter hello Transport Layer Security settings for your Docker host.</span></span> <span data-ttu-id="39932-176">Hello 다음 옵션에서에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39932-176">You can choose from hello following options:</span></span>
            * <span data-ttu-id="39932-177">**없음**: 가상 컴퓨터에서 TLS 연결을 허용하지 않게 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-177">**None**: Specifies that your virtual machine will not allow TLS connections.</span></span>
            * <span data-ttu-id="39932-178">**자동 생성**: TLS를 통해 연결에 대 한 hello 필수 설정을 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39932-178">**Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.</span></span>
            * <span data-ttu-id="39932-179">**디렉터리에서 가져오기**: 이전에 저장된 TLS 설정 집합을 포함하는 디렉터리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-179">**Import from directory**: Specifies a directory that contains a set of previously saved TLS settings.</span></span> <span data-ttu-id="39932-180">보다 구체적으로, hello 디렉터리 hello 다음 6 개 파일이 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-180">More specifically, hello directory must contain hello following six files:</span></span>
                * <span data-ttu-id="39932-181">*ca.pem* 및 *ca key.pem*: hello 인증서 및 TLS 인증 기관 hello에 대 한 공개 키를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-181">*ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.</span></span>
                * <span data-ttu-id="39932-182">*cert.pem* 및 *key.pem*: hello 클라이언트 인증서 및 TLS 인증에 사용 되는 공개 키를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-182">*cert.pem* and *key.pem*: Contain hello client certificate and public key that is used for TLS authentication.</span></span>
                * <span data-ttu-id="39932-183">*server.pem* 및 *서버 key.pem*: hello 서버 인증서와 hello 호스트에 대 한 공개 키를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-183">*server.pem* and *server-key.pem*: Contain hello server certificate and public key for hello host.</span></span>

        ![Docker 호스트 만들기][PUB06]

7. <span data-ttu-id="39932-185">모든 hello 앞에 정보를 입력 한 후 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-185">After you have entered all of hello preceding information, click **Finish**.</span></span>

8. <span data-ttu-id="39932-186">Hello에 **Azure에서 Docker 컨테이너 배포** 마법사를 클릭 하 여 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-186">In hello **Deploy Docker Container on Azure** wizard, click **Next**.</span></span>

   ![hello Azure 마법사에서 Docker 컨테이너 배포][PUB07]

9. <span data-ttu-id="39932-188">Hello에 **hello Docker 컨테이너 toobe 만든 구성** 창에서 다음 hello지 않습니다:</span><span class="sxs-lookup"><span data-stu-id="39932-188">In hello **Configure hello Docker container toobe created** window, do hello following:</span></span>

   <span data-ttu-id="39932-189">a.</span><span class="sxs-lookup"><span data-stu-id="39932-189">a.</span></span> <span data-ttu-id="39932-190">Hello에 **Docker 컨테이너 이름을** 상자 Docker 컨테이너에 대 한 고유 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-190">In hello **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="39932-191">b.</span><span class="sxs-lookup"><span data-stu-id="39932-191">b.</span></span> <span data-ttu-id="39932-192">Hello Docker 이미지를 다음 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-192">Choose one of hello following Docker images:</span></span>
     * <span data-ttu-id="39932-193">**미리 정의된 Docker 이미지**: Azure에서 기존 Docker 이미지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-193">**Predefined Docker image**: Specifies a pre-existing Docker image from Azure.</span></span>

       >[!NOTE]
       ><span data-ttu-id="39932-194">이 상자에서 Docker 이미지 hello 목록은 여러 그림으로 구성 된 Azure 도구 키트는 hello 구성 toopatch 프로그램 아티팩트가 자동으로 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39932-194">hello list of Docker images in this box consists of several images that hello Azure Toolkit has been configured toopatch so that your artifact is deployed automatically.</span></span>

     * <span data-ttu-id="39932-195">**사용자 지정 Dockerfile**: 로컬 컴퓨터에서 이전에 저장된 Dockerfile을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-195">**Custom Dockerfile**: Specifies a previously saved Dockerfile from your local computer.</span></span>

       >[!NOTE]
       ><span data-ttu-id="39932-196">이 기능은 toodeploy 자신의 Dockerfile 알아보려는 개발자를 위한 보다 고급입니다.</span><span class="sxs-lookup"><span data-stu-id="39932-196">This is a more advanced feature for developers who want toodeploy their own Dockerfile.</span></span> <span data-ttu-id="39932-197">그러나 toodevelopers 자신의 Dockerfile 제대로 빌드는이 옵션 tooensure를 사용 하는 중일으로 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-197">However, it is up toodevelopers who use this option tooensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="39932-198">hello Azure 도구 키트 하므로 hello Dockerfile에 문제가 hello 배포가 실패할 수 있습니다 hello 콘텐츠 사용자 지정 Dockerfile의 유효성을 검사 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="39932-198">hello Azure Toolkit does not validate hello content in a custom Dockerfile, so hello deployment might fail if hello Dockerfile has issues.</span></span> <span data-ttu-id="39932-199">또한 Azure 도구 키트 hello hello 사용자 지정 Dockerfile toocontain 웹 응용 프로그램 아티팩트를 요구 하 고 tooopen HTTP 연결을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-199">In addition, hello Azure Toolkit expects hello custom Dockerfile toocontain a web app artifact, and it will attempt tooopen an HTTP connection.</span></span> <span data-ttu-id="39932-200">개발자가 다른 아티팩트 형식을 게시하는 경우 배포 후에 무해한 오류가 표시될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39932-200">If developers publish a different type of artifact, they may receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="39932-201">c.</span><span class="sxs-lookup"><span data-stu-id="39932-201">c.</span></span> <span data-ttu-id="39932-202">**포트 설정을**: hello 고유 TCP 포트 바인딩을 Docker 컨테이너에 대 한 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-202">**Port settings**: Enter hello unique TCP port binding for your Docker container.</span></span>

     ![hello 구성 hello Docker 컨테이너 toobe 만든 창][PUB08]

10. <span data-ttu-id="39932-204">모든 hello 이전 단계를 완료 한 후 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-204">After you have completed all of hello preceding steps, click **Finish**.</span></span>

<span data-ttu-id="39932-205">hello Azure 도구 키트는 Docker 컨테이너에 웹 앱 tooAzure 프로그램 배포를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-205">hello Azure Toolkit begins deploying your web app tooAzure in a Docker container.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="39932-206">다음 단계</span><span class="sxs-lookup"><span data-stu-id="39932-206">Next steps</span></span>
<span data-ttu-id="39932-207">Java Ide에 대 한 hello Azure 도구 키트에 대 한 자세한 내용은 hello 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="39932-207">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="39932-208">[Eclipse용 Azure 도구 키트]</span><span class="sxs-lookup"><span data-stu-id="39932-208">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="39932-209">[Hello Eclipse 용 Azure 도구 키트의에서 새로운 기능]</span><span class="sxs-lookup"><span data-stu-id="39932-209">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="39932-210">[Hello Eclipse 용 Azure 도구 키트 설치]</span><span class="sxs-lookup"><span data-stu-id="39932-210">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="39932-211">[Eclipse 용 Azure 도구 키트 hello에 대 한 로그인 지침]</span><span class="sxs-lookup"><span data-stu-id="39932-211">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="39932-212">[Eclipse에서 Azure용 Hello World 웹앱 만들기]</span><span class="sxs-lookup"><span data-stu-id="39932-212">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="39932-213">[IntelliJ용 Azure 도구 키트]</span><span class="sxs-lookup"><span data-stu-id="39932-213">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="39932-214">[Hello IntelliJ 용 Azure 도구 키트의에서 새로운 기능]</span><span class="sxs-lookup"><span data-stu-id="39932-214">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="39932-215">[IntelliJ 용 hello Azure 도구 키트 설치]</span><span class="sxs-lookup"><span data-stu-id="39932-215">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="39932-216">[로그인에 대 한 지침 Azure 도구 키트 hello IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="39932-216">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="39932-217">[IntelliJ에서 Azure용 Hello World 웹앱 만들기]</span><span class="sxs-lookup"><span data-stu-id="39932-217">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="39932-218">Java와 함께 Azure를 사용하는 것에 대한 자세한 내용은 [Azure Java 개발자 센터] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39932-218">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="39932-219">Docker에 대 한 추가 리소스에 대 한 참조 hello 공식 [Docker 웹 사이트]합니다.</span><span class="sxs-lookup"><span data-stu-id="39932-219">For additional resources for Docker, see hello official [Docker website].</span></span>

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
[Visual Studio Team Services용 Java 도구]: https://java.visualstudio.com/

[Docker 웹 사이트]: https://www.docker.com/

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB08.png