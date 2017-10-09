---
title: "Linux 가상 컴퓨터에 Apache Tomcat을 aaaSet | Microsoft Docs"
description: "자세한 방법을 Linux를 실행 하는 Azure 가상 컴퓨터를 사용 하 여 Apache Tomcat7를 tooset 합니다."
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 45ecc89c-1cb0-4e80-8944-bd0d0bbedfdc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: ningk
ms.openlocfilehash: b837a73e91fcb25d5459d993a0e93ceef1a1fc8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-tomcat7-on-a-linux-virtual-machine-with-azure"></a><span data-ttu-id="91652-103">Azure를 사용하여 Linux 가상 컴퓨터에 Tomcat7 설치</span><span class="sxs-lookup"><span data-stu-id="91652-103">Set up Tomcat7 on a Linux virtual machine with Azure</span></span>
<span data-ttu-id="91652-104">Apache Tomcat (또는 단순히 Tomcat, 자카르타 Tomcat도 이전의)는 오픈 소스 웹 서버 및 servlet 컨테이너 hello Apache 소프트웨어 Foundation ASF ()에서 개발한,</span><span class="sxs-lookup"><span data-stu-id="91652-104">Apache Tomcat (or simply Tomcat, also formerly called Jakarta Tomcat) is an open source web server and servlet container developed by hello Apache Software Foundation (ASF).</span></span> <span data-ttu-id="91652-105">Tomcat 해 Java 서블릿에 hello 및 Sun Microsystems에서 hello JavaServer 페이지 (JSP) 사양을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-105">Tomcat implements hello Java Servlet and hello JavaServer Pages (JSP) specifications from Sun Microsystems.</span></span> <span data-ttu-id="91652-106">Tomcat 순수 Java HTTP 웹 서버 환경에서 어떤 toorun Java 코드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-106">Tomcat provides a pure Java HTTP web server environment in which toorun Java code.</span></span> <span data-ttu-id="91652-107">Hello 가장 단순한 구성 Tomcat는 단일 운영 체제 프로세스에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91652-107">In hello simplest configuration, Tomcat runs in a single operating system process.</span></span> <span data-ttu-id="91652-108">이 프로세스에서는 JVM(Java Virtual Machine)을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-108">This process runs a Java virtual machine (JVM).</span></span> <span data-ttu-id="91652-109">브라우저 tooTomcat의 모든 HTTP 요청을 별도 스레드에서 hello Tomcat 프로세스에서 변수로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91652-109">Every HTTP request from a browser tooTomcat is processed as a separate thread in hello Tomcat process.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="91652-110">Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델, 즉 [Azure Resource Manager 및 클래식](../../../resource-manager-deployment-model.md) 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-110">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="91652-111">이 문서에서는 toouse 클래식 배포 모델을 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-111">This article covers how toouse hello classic deployment model.</span></span> <span data-ttu-id="91652-112">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-112">We recommend that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="91652-113">리소스 관리자 템플릿 toodeploy Openjdk 및 Tomcat을 사용 하는 Ubuntu VM toouse 참조 [이 여기서](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/)합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-113">toouse a Resource Manager template toodeploy an Ubuntu VM with Open JDK and Tomcat, see [this article](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span></span>

<span data-ttu-id="91652-114">이 문서에서는 Tomcat7을 Linux 이미지에 설치하고 이를 Azure에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-114">In this article, you will install Tomcat7 on a Linux image and deploy it in Azure.</span></span>  

<span data-ttu-id="91652-115">다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="91652-115">You will learn:</span></span>  

* <span data-ttu-id="91652-116">어떻게 toocreate Azure의 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="91652-116">How toocreate a virtual machine in Azure.</span></span>
* <span data-ttu-id="91652-117">어떻게 tooprepare Tomcat7에 대 한 가상 컴퓨터를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-117">How tooprepare hello virtual machine for Tomcat7.</span></span>
* <span data-ttu-id="91652-118">어떻게 tooinstall Tomcat7 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-118">How tooinstall Tomcat7.</span></span>

<span data-ttu-id="91652-119">이미 Azure 구독이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-119">It is assumed that you already have an Azure subscription.</span></span>  <span data-ttu-id="91652-120">무료 평가판에 등록할 수는 그렇지 않은 경우 [Azure 웹 사이트를 hello](https://azure.microsoft.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-120">If not, you can sign up for a free trial at [hello Azure website](https://azure.microsoft.com/).</span></span> <span data-ttu-id="91652-121">MSDN 구독이 있는 경우 [Microsoft Azure 특별 가격: MSDN, MPN 및 BizSpark 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91652-121">If you have an MSDN subscription, see [Microsoft Azure Special Pricing: MSDN, MPN, and BizSpark Benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span></span> <span data-ttu-id="91652-122">Azure에 대 한 자세한 정보는 toolearn 참조 [Azure 란?](https://azure.microsoft.com/overview/what-is-azure/)합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-122">toolearn more about Azure, see [What is Azure?](https://azure.microsoft.com/overview/what-is-azure/).</span></span>

<span data-ttu-id="91652-123">이 문서에서는 사용자가 Tomcat 및 Linux에 대한 기본적인 실무 지식을 갖추고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-123">This article assumes that you have a basic working knowledge of Tomcat and Linux.</span></span>  

## <a name="phase-1-create-an-image"></a><span data-ttu-id="91652-124">1단계: 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="91652-124">Phase 1: Create an image</span></span>
<span data-ttu-id="91652-125">이 단계에서는 Azure에서 Linux 이미지를 사용하여 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="91652-125">In this phase, you will create a virtual machine by using a Linux image in Azure.</span></span>  

### <a name="step-1-generate-an-ssh-authentication-key"></a><span data-ttu-id="91652-126">1단계: SSH 인증 키 생성</span><span class="sxs-lookup"><span data-stu-id="91652-126">Step 1: Generate an SSH authentication key</span></span>
<span data-ttu-id="91652-127">SSH는 시스템 관리자에게 중요한 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="91652-127">SSH is an important tool for system administrators.</span></span> <span data-ttu-id="91652-128">그러나 사람이 식별할 수 있는 암호를 기반으로 하여 액세스 보안을 구성하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-128">However, configuring access security based on a human-determined password is not recommended.</span></span> <span data-ttu-id="91652-129">악의적인 사용자는 사용자 이름 및 취약한 암호를 기반으로 하는 시스템에 침입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-129">Malicious users can break into your system based on a username and a weak password.</span></span>

<span data-ttu-id="91652-130">hello 좋은 소식 tooleave 원격 액세스를 열고 암호에 대해서는 걱정 하지 하 게 된다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="91652-130">hello good news is that there is a way tooleave remote access open and not worry about passwords.</span></span> <span data-ttu-id="91652-131">이 방법은 비대칭 암호화를 사용하는 인증으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="91652-131">This method consists of authentication with asymmetric cryptography.</span></span> <span data-ttu-id="91652-132">hello 사용자의 개인 키는 hello hello 인증 권한을 부여 하는 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="91652-132">hello user’s private key is hello one that grants hello authentication.</span></span> <span data-ttu-id="91652-133">Hello 사용자 계정 잠금도 수 toonot 암호 인증을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-133">You can even lock hello user’s account toonot allow password authentication.</span></span>

<span data-ttu-id="91652-134">이 메서드의 또 다른 이점은 toodifferent 서버에서 다른 암호 toosign 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-134">Another advantage of this method is that you do not need different passwords toosign in toodifferent servers.</span></span> <span data-ttu-id="91652-135">Tooremember 여러 암호를 사용 하면 모든 서버에 개인 키를 개인 hello을 사용 하 여 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-135">You can authenticate by using hello personal private key on all servers, which prevents you from having tooremember several passwords.</span></span>



<span data-ttu-id="91652-136">이러한 단계 toogenerate hello SSH 인증 키를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="91652-136">Follow these steps toogenerate hello SSH authentication key.</span></span>

1. <span data-ttu-id="91652-137">에서 다운로드 및 설치 PuTTYgen hello 수정할 수 있는 위치: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span><span class="sxs-lookup"><span data-stu-id="91652-137">Download and install PuTTYgen from hello following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
2. <span data-ttu-id="91652-138">Puttygen.exe를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-138">Run Puttygen.exe.</span></span>
3. <span data-ttu-id="91652-139">클릭 **생성** toogenerate hello 키입니다.</span><span class="sxs-lookup"><span data-stu-id="91652-139">Click **Generate** toogenerate hello keys.</span></span> <span data-ttu-id="91652-140">Hello 프로세스에서 hello hello 창에서 빈 영역을 통해 임의성 hello 마우스를 이동 하 여 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-140">In hello process, you can increase randomness by moving hello mouse over hello blank area in hello window.</span></span>  
   <span data-ttu-id="91652-141">![새 키 단추를 생성 하는 hello를 보여 주는 puTTY 키 생성기 스크린 샷][1]</span><span class="sxs-lookup"><span data-stu-id="91652-141">![PuTTY Key Generator screenshot that shows hello generate new key button][1]</span></span>
4. <span data-ttu-id="91652-142">프로세스를 생성 하는 hello Puttygen.exe는 새 공개 키를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-142">After hello generate process, Puttygen.exe will show your new public key.</span></span>  
   ![Hello 새 공개 키와 개인 키 단추 저장 hello를 보여 주는 puTTY 키 생성기 스크린 샷][2]
5. <span data-ttu-id="91652-144">선택 하 고 hello 공개 키를 복사 하 고 publicKey.pem 라는 파일에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-144">Select and copy hello public key, and save it in a file named publicKey.pem.</span></span> <span data-ttu-id="91652-145">클릭 하지 마십시오 **저장 공개 키**저장 된 공개 키 파일 형식과 hello은 원하는 hello 공개 키와 다르기 때문에, 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-145">Don’t click **Save public key**, because hello saved public key’s file format is different from hello public key we want.</span></span>
6. <span data-ttu-id="91652-146">**개인 키 저장**을 클릭하고 privateKey.ppk 파일에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-146">Click **Save private key**, and save it in a file named privateKey.ppk.</span></span>

### <a name="step-2-create-hello-image-in-hello-azure-portal"></a><span data-ttu-id="91652-147">2 단계: hello Azure 포털에서에서 hello 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="91652-147">Step 2: Create hello image in hello Azure portal</span></span>
1. <span data-ttu-id="91652-148">Hello에 [포털](https://portal.azure.com/), 클릭 **새로** hello에서 작업 표시줄 toocreate 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="91652-148">In hello [portal](https://portal.azure.com/), click **New** in hello task bar toocreate an image.</span></span> <span data-ttu-id="91652-149">필요에 따라 hello Linux 이미지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-149">Then choose hello Linux image that is based on your needs.</span></span> <span data-ttu-id="91652-150">hello 다음 예제에서는 hello Ubuntu 14.04 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="91652-150">hello following example uses hello Ubuntu 14.04 image.</span></span>
<span data-ttu-id="91652-151">![Hello 새로 만들기 단추를 보여 주는 hello 포털의 스크린샷][3]</span><span class="sxs-lookup"><span data-stu-id="91652-151">![Screenshot of hello portal that shows hello New button][3]</span></span>

2. <span data-ttu-id="91652-152">에 대 한 **호스트 이름**, 있는지와 인터넷 클라이언트는 tooaccess이 가상 컴퓨터를 사용 하는 hello URL에 대 한 hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-152">For **Host Name**, specify hello name for hello URL that you and Internet clients will use tooaccess this virtual machine.</span></span> <span data-ttu-id="91652-153">예를 들어 tomcatdemo hello DNS 이름의 hello 마지막 부분을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-153">Define hello last part of hello DNS name, for example, tomcatdemo.</span></span> <span data-ttu-id="91652-154">Azure는 tomcatdemo.cloudapp.net으로 hello URL을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-154">Azure will then generate hello URL as tomcatdemo.cloudapp.net.</span></span>  

3. <span data-ttu-id="91652-155">에 대 한 **SSH 인증 키**, PuTTYgen가 생성 하는 hello 공개 키가 포함 된 hello publicKey.pem 파일에서 hello 키 값을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-155">For **SSH Authentication Key**, copy hello key value from hello publicKey.pem file, which contains hello public key generated by PuTTYgen.</span></span>  
<span data-ttu-id="91652-156">![SSH 인증 키 상자 hello 포털에][4]</span><span class="sxs-lookup"><span data-stu-id="91652-156">![SSH Authentication Key box in hello portal][4]</span></span>

4. <span data-ttu-id="91652-157">필요에 따라 다른 설정을 구성한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-157">Configure other settings as needed, and then click **Create**.</span></span>  

## <a name="phase-2-prepare-your-virtual-machine-for-tomcat7"></a><span data-ttu-id="91652-158">2단계: Tomcat7에 대해 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="91652-158">Phase 2: Prepare your virtual machine for Tomcat7</span></span>
<span data-ttu-id="91652-159">이 단계 Tomcat 트래픽에 대 한 끝점을 구성 하 고 tooyour 새 가상 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-159">In this phase, you will configure an endpoint for Tomcat traffic, and then connect tooyour new virtual machine.</span></span>

### <a name="step-1-open-hello-http-port-tooallow-web-access"></a><span data-ttu-id="91652-160">1 단계: hello HTTP 포트 tooallow web access를 열으십시오</span><span class="sxs-lookup"><span data-stu-id="91652-160">Step 1: Open hello HTTP port tooallow web access</span></span>
<span data-ttu-id="91652-161">Azure의 끝점은 공용 및 개인 포트와 함께 TCP 또는 UDP 프로토콜로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="91652-161">Endpoints in Azure consist of a TCP or UDP protocol, along with a public and private port.</span></span> <span data-ttu-id="91652-162">hello 개인 포트는 hello 서비스는 tooon hello 가상 컴퓨터를 수신 대기 하는 hello 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="91652-162">hello private port is hello port that hello service is listening tooon hello virtual machine.</span></span> <span data-ttu-id="91652-163">hello 공용 포트는 hello Azure 클라우드 서비스는 hello 포트 tooexternally, 인터넷 기반 들어오는 트래픽에 대 한 수신 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-163">hello public port is hello port that hello Azure cloud service listens tooexternally for incoming, Internet-based traffic.</span></span>  

<span data-ttu-id="91652-164">TCP 포트 8080에는 Tomcat toolisten를 사용 하는 hello 기본 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="91652-164">TCP port 8080 is hello default port number that Tomcat uses toolisten.</span></span> <span data-ttu-id="91652-165">Azure 끝점에서 이 포트를 열면 사용자와 다른 인터넷 클라이언트가 Tomcat 페이지에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-165">If this port is opened with an Azure endpoint, you and other Internet clients can access Tomcat pages.</span></span>  

1. <span data-ttu-id="91652-166">Hello 포털에서 클릭 **찾아보기** > **가상 컴퓨터**, 다음 만든 hello 가상 컴퓨터를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-166">In hello portal, click **Browse** > **Virtual machines**, and then click hello virtual machine that you created.</span></span>  
   <span data-ttu-id="91652-167">![Hello 가상 컴퓨터 디렉터리의 스크린샷][5]</span><span class="sxs-lookup"><span data-stu-id="91652-167">![Screenshot of hello Virtual machines directory][5]</span></span>
2. <span data-ttu-id="91652-168">tooadd 끝점 tooyour 가상 컴퓨터를 클릭 하 여 hello **끝점** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="91652-168">tooadd an endpoint tooyour virtual machine, click hello **Endpoints** box.</span></span>
   <span data-ttu-id="91652-169">![Hello 끝점 상자를 보여 주는 스크린샷][6]</span><span class="sxs-lookup"><span data-stu-id="91652-169">![Screenshot that shows hello Endpoints box][6]</span></span>
3. <span data-ttu-id="91652-170">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-170">Click **Add**.</span></span>  

   1. <span data-ttu-id="91652-171">Hello 끝점에 대 한 hello 끝점에 대 한 이름을 입력 **끝점**, 다음에 80을 입력 하 고 **공용 포트**합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-171">For hello endpoint, enter a name for hello endpoint in **Endpoint**, and then enter 80 in **Public Port**.</span></span>  

      <span data-ttu-id="91652-172">값을 설정 하면 too80 tooinclude hello 포트 번호가 사용 되는 tooaccess Tomcat hello URL에 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-172">If you set it too80, you don’t need tooinclude hello port number in hello URL that is used tooaccess Tomcat.</span></span> <span data-ttu-id="91652-173">예를 들면 http://tomcatdemo.cloudapp.net과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-173">For example, http://tomcatdemo.cloudapp.net.</span></span>    

      <span data-ttu-id="91652-174">81, 같은 tooanother 값을 설정 하면 tooadd hello 포트 번호 toohello URL tooaccess Tomcat 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-174">If you set it tooanother value, such as 81, you need tooadd hello port number toohello URL tooaccess Tomcat.</span></span> <span data-ttu-id="91652-175">예를 들면 http://tomcatdemo.cloudapp.net:81/과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-175">For example,  http://tomcatdemo.cloudapp.net:81/.</span></span>
   2. <span data-ttu-id="91652-176">**개인 포트**에 8080을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-176">Enter 8080 in **Private Port**.</span></span> <span data-ttu-id="91652-177">기본적으로 Tomcat은 8080 TCP 포트에서 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-177">By default, Tomcat listens on TCP port 8080.</span></span> <span data-ttu-id="91652-178">Tomcat의 hello 기본 수신 대기 포트를 변경 하는 경우 업데이트 해야 **개인 포트** toobe hello Tomcat 수신 대기 포트 hello와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-178">If you changed hello default listen port of Tomcat, you should update **Private Port** toobe hello same as hello Tomcat listen port.</span></span>  
      <span data-ttu-id="91652-179">![추가 명령, 공용 포트 및 개인 포트를 보여 주는 UI 스크린샷][7]</span><span class="sxs-lookup"><span data-stu-id="91652-179">![Screenshot of UI that shows Add command, Public Port, and Private Port][7]</span></span>
4. <span data-ttu-id="91652-180">클릭 **확인** tooadd hello 끝점 tooyour 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="91652-180">Click **OK** tooadd hello endpoint tooyour virtual machine.</span></span>

### <a name="step-2-connect-toohello-image-you-created"></a><span data-ttu-id="91652-181">2 단계: 만든 toohello 이미지 연결</span><span class="sxs-lookup"><span data-stu-id="91652-181">Step 2: Connect toohello image you created</span></span>
<span data-ttu-id="91652-182">SSH 도구 tooconnect tooyour 가상 컴퓨터를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-182">You can choose any SSH tool tooconnect tooyour virtual machine.</span></span> <span data-ttu-id="91652-183">이 예제에서는 PuTTY를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-183">In this example, we use PuTTY.</span></span>  

1. <span data-ttu-id="91652-184">Hello 포털에서 가상 컴퓨터의 DNS 이름을 hello를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="91652-184">Get hello DNS name of your virtual machine from hello portal.</span></span>
    1. <span data-ttu-id="91652-185">**찾아보기** > **가상 컴퓨터**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-185">Click **Browse** > **Virtual machines**.</span></span>
    2. <span data-ttu-id="91652-186">가상 컴퓨터의 hello 이름을 선택한 다음 클릭 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-186">Select hello name of your virtual machine, and then click **Properties**.</span></span>
    3. <span data-ttu-id="91652-187">Hello에 **속성** 타일, 찾는 위치 hello **도메인 이름** 상자 tooget hello DNS 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="91652-187">In hello **Properties** tile, look in hello **Domain Name** box tooget hello DNS name.</span></span>  

2. <span data-ttu-id="91652-188">Hello에서 SSH 연결에 대 한 hello 포트 번호를 가져오려면 **SSH** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="91652-188">Get hello port number for SSH connections from hello **SSH** box.</span></span>  
<span data-ttu-id="91652-189">![Hello SSH 연결 포트 번호를 보여 주는 스크린샷][8]</span><span class="sxs-lookup"><span data-stu-id="91652-189">![Screenshot that shows hello SSH connection port number][8]</span></span>

3. <span data-ttu-id="91652-190">[PuTTY](http://www.putty.org/)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-190">Download [PuTTY](http://www.putty.org/).</span></span>  

4. <span data-ttu-id="91652-191">다운로드 한 후 Putty.exe hello 실행 파일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-191">After downloading, click hello executable file Putty.exe.</span></span> <span data-ttu-id="91652-192">PuTTY 구성에서 hello 호스트 이름의 hello 기본 옵션을 구성 하 고 포트 번호를 가상 컴퓨터의 hello 속성에서 가져온 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="91652-192">In PuTTY configuration, configure hello basic options with hello host name and port number that is obtained from hello properties of your virtual machine.</span></span>   
![Hello PuTTY 구성 호스트 이름과 포트 옵션을 보여 주는 스크린샷][9]

5. <span data-ttu-id="91652-194">Hello 왼쪽된 창에서 클릭 **연결** > **SSH** > **Auth**, 클릭 하 고 **찾아보기** toospecify hello privateKey.ppk 파일의 hello 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="91652-194">In hello left pane, click **Connection** > **SSH** > **Auth**, and then click **Browse** toospecify hello location of hello privateKey.ppk file.</span></span> <span data-ttu-id="91652-195">hello privateKey.ppk 파일 hello hello의 앞부분에 나오는 PuTTYgen에서 생성 되는 개인 키가 들어 "1 단계: 이미지 만들기"이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="91652-195">hello privateKey.ppk file contains hello private key that is generated by PuTTYgen earlier in hello "Phase 1: Create an image" section of this article.</span></span>  
<span data-ttu-id="91652-196">![Hello 연결 디렉터리 계층 구조 및 찾아보기 단추를 보여 주는 스크린샷][10]</span><span class="sxs-lookup"><span data-stu-id="91652-196">![Screenshot that shows hello Connection directory hierarchy and Browse button][10]</span></span>

6. <span data-ttu-id="91652-197">**열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-197">Click **Open**.</span></span> <span data-ttu-id="91652-198">메시지 상자에 경고 메시지가 표시될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-198">You might be alerted by a message box.</span></span> <span data-ttu-id="91652-199">Hello DNS 이름을 구성 하 고 포트 번호를 올바르게 클릭 하 여 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-199">If you have configured hello DNS name and port number correctly, click **Yes**.</span></span>
<span data-ttu-id="91652-200">![Hello 알림을 보여 주는 스크린샷][11]</span><span class="sxs-lookup"><span data-stu-id="91652-200">![Screenshot that shows hello notification][11]</span></span>

7. <span data-ttu-id="91652-201">사용자는 증명된 tooenter 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="91652-201">You are prompted tooenter your username.</span></span>  
![위치를 보여 주는 스크린 샷 tooenter 사용자 이름][12]

8. <span data-ttu-id="91652-203">Hello에 toocreate hello 가상 컴퓨터를 사용 하는 hello 사용자 이름을 입력 "1 단계: 이미지 만들기"이이 문서의 앞부분에 나오는 섹션.</span><span class="sxs-lookup"><span data-stu-id="91652-203">Enter hello username that you used toocreate hello virtual machine in hello "Phase 1: Create an image" section earlier in this article.</span></span> <span data-ttu-id="91652-204">Hello 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91652-204">You will see something like hello following:</span></span>  
![Hello 인증 확인을 보여 주는 스크린샷][13]

## <a name="phase-3-install-software"></a><span data-ttu-id="91652-206">3단계: 소프트웨어 설치</span><span class="sxs-lookup"><span data-stu-id="91652-206">Phase 3: Install software</span></span>
<span data-ttu-id="91652-207">이 단계에서는 hello Java 런타임 환경, Tomcat7, 및 기타 Tomcat7 구성 요소를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-207">In this phase, you install hello Java runtime environment, Tomcat7, and other Tomcat7 components.</span></span>  

### <a name="java-runtime-environment"></a><span data-ttu-id="91652-208">Java Runtime Environment</span><span class="sxs-lookup"><span data-stu-id="91652-208">Java runtime environment</span></span>
<span data-ttu-id="91652-209">Tomcat은 Java로 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-209">Tomcat is written in Java.</span></span> <span data-ttu-id="91652-210">JDK(Java Development Kit)에는 두 가지 종류의 JDK, 즉 OpenJDK와 Oracle JDK가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-210">There are two kinds of Java Development Kits (JDKs), OpenJDK and Oracle JDK.</span></span> <span data-ttu-id="91652-211">원하는 hello를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-211">You can choose hello one you want.</span></span>  

> [!NOTE]
> <span data-ttu-id="91652-212">모두 Jdk hello 클래스 hello Java API에에서 대 한 코드 hello 거의 했지만 hello 가상 컴퓨터에 대 한 hello 코드는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="91652-212">Both JDKs have almost hello same code for hello classes in hello Java API, but hello code for hello virtual machine is different.</span></span> <span data-ttu-id="91652-213">OpenJDK 경향이 toouse 오픈 라이브러리, toouse 닫힌 스토리 동안 Oracle JDK는 경향이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-213">OpenJDK tends toouse open libraries, while Oracle JDK tends toouse closed ones.</span></span> <span data-ttu-id="91652-214">Oracle JDK는 더 많은 클래스와 일부 수정된 버그를 포함하고 있지만 OpenJDK보다 더 안정적입니다.</span><span class="sxs-lookup"><span data-stu-id="91652-214">Oracle JDK has more classes and some fixed bugs, and Oracle JDK is more stable than OpenJDK.</span></span>

#### <a name="install-openjdk"></a><span data-ttu-id="91652-215">OpenJDK 설치</span><span class="sxs-lookup"><span data-stu-id="91652-215">Install OpenJDK</span></span>  

<span data-ttu-id="91652-216">다음 명령은 toodownload OpenJDK hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-216">Use hello following command toodownload OpenJDK.</span></span>   

    sudo apt-get update  
    sudo apt-get install openjdk-7-jre  


* <span data-ttu-id="91652-217">디렉터리 toocontain toocreate hello JDK 파일:</span><span class="sxs-lookup"><span data-stu-id="91652-217">toocreate a directory toocontain hello JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="91652-218">tooextract hello JDK hello/usr/lib/jvm/디렉터리에 파일:</span><span class="sxs-lookup"><span data-stu-id="91652-218">tooextract hello JDK files into hello /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/

#### <a name="install-oracle-jdk"></a><span data-ttu-id="91652-219">Oracle JDK 설치</span><span class="sxs-lookup"><span data-stu-id="91652-219">Install Oracle JDK</span></span>


<span data-ttu-id="91652-220">Hello 명령 toodownload Oracle JDK hello Oracle 웹 사이트에서 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-220">Use hello following command toodownload Oracle JDK from hello Oracle website.</span></span>  

     wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz  
* <span data-ttu-id="91652-221">디렉터리 toocontain toocreate hello JDK 파일:</span><span class="sxs-lookup"><span data-stu-id="91652-221">toocreate a directory toocontain hello JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="91652-222">tooextract hello JDK hello/usr/lib/jvm/디렉터리에 파일:</span><span class="sxs-lookup"><span data-stu-id="91652-222">tooextract hello JDK files into hello /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/  
* <span data-ttu-id="91652-223">Oracle JDK 기본 Java 가상 컴퓨터를 hello 대로 tooset:</span><span class="sxs-lookup"><span data-stu-id="91652-223">tooset Oracle JDK as hello default Java virtual machine:</span></span>  

        sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_05/bin/java 100  

        sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_05/bin/javac 100  

#### <a name="confirm-that-java-installation-is-successful"></a><span data-ttu-id="91652-224">Java 설치가 성공적인지 확인</span><span class="sxs-lookup"><span data-stu-id="91652-224">Confirm that Java installation is successful</span></span>
<span data-ttu-id="91652-225">같은 hello tootest hello Java 런타임 환경이 올바르게 설치 하는 경우 다음 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-225">You can use a command like hello following tootest if hello Java runtime environment is installed correctly:</span></span>  

    java -version  

<span data-ttu-id="91652-226">OpenJDK를 설치한 경우 hello 다음과 같은 메시지가 나타납니다: ![성공 OpenJDK 설치 메시지][14]</span><span class="sxs-lookup"><span data-stu-id="91652-226">If you installed OpenJDK, you should see a message like hello following: ![Successful OpenJDK installation message][14]</span></span>

<span data-ttu-id="91652-227">Oracle JDK를 설치한 경우 hello 다음과 같은 메시지가 나타납니다: ![성공 Oracle JDK 설치 메시지][15]</span><span class="sxs-lookup"><span data-stu-id="91652-227">If you installed Oracle JDK, you should see a message like hello following: ![Successful Oracle JDK installation message][15]</span></span>

### <a name="install-tomcat7"></a><span data-ttu-id="91652-228">Tomcat7 설치</span><span class="sxs-lookup"><span data-stu-id="91652-228">Install Tomcat7</span></span>
<span data-ttu-id="91652-229">다음 명령은 tooinstall Tomcat7 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-229">Use hello following command tooinstall Tomcat7.</span></span>  

    sudo apt-get install tomcat7  

<span data-ttu-id="91652-230">Tomcat7를 사용 하지 않는 경우이 명령은의 적절 한 변형 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-230">If you are not using Tomcat7, use hello appropriate variation of this command.</span></span>  

#### <a name="confirm-that-tomcat7-installation-is-successful"></a><span data-ttu-id="91652-231">Tomcat7 설치가 성공적인지 확인</span><span class="sxs-lookup"><span data-stu-id="91652-231">Confirm that Tomcat7 installation is successful</span></span>
<span data-ttu-id="91652-232">Tomcat7이 성공적으로 설치 toocheck 찾아보기 tooyour Tomcat 서버 DNS 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="91652-232">toocheck if Tomcat7 is successfully installed, browse tooyour Tomcat server’s DNS name.</span></span> <span data-ttu-id="91652-233">이 문서에서는 hello 예를 들어 URL http://tomcatexample.cloudapp.net/ 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91652-233">In this article, hello example URL is http://tomcatexample.cloudapp.net/.</span></span> <span data-ttu-id="91652-234">Hello 다음과 같은 메시지가 나타나면 Tomcat7 제대로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91652-234">If you see a message like hello following, Tomcat7 is installed correctly.</span></span>
<span data-ttu-id="91652-235">![Tomcat7 설치 성공 메시지][16]</span><span class="sxs-lookup"><span data-stu-id="91652-235">![Successful Tomcat7 installation message][16]</span></span>

### <a name="install-other-tomcat7-components"></a><span data-ttu-id="91652-236">기타 Tomcat7 구성 요소 설치</span><span class="sxs-lookup"><span data-stu-id="91652-236">Install other Tomcat7 components</span></span>
<span data-ttu-id="91652-237">설치할 수 있는 다른 선택적 Tomcat 구성 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-237">There are other optional Tomcat components that you can install.</span></span>  

<span data-ttu-id="91652-238">사용 하 여 hello **sudo apt 캐시 검색 tomcat7** 명령 toosee 모든 hello 사용 가능한 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="91652-238">Use hello **sudo apt-cache search tomcat7** command toosee all of hello available components.</span></span> <span data-ttu-id="91652-239">다음 명령을 tooinstall hello 데 유용한 몇 가지 구성 요소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-239">Use hello following commands tooinstall some useful components.</span></span>  

    sudo apt-get install tomcat7-admin      #admin web applications

    sudo apt-get install tomcat7-user         #tools toocreate user instances  

## <a name="phase-4-configure-tomcat7"></a><span data-ttu-id="91652-240">4단계: Tomcat7 구성</span><span class="sxs-lookup"><span data-stu-id="91652-240">Phase 4: Configure Tomcat7</span></span>
<span data-ttu-id="91652-241">이 단계에서는 Tomcat을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-241">In this phase, you administer Tomcat.</span></span>

### <a name="start-and-stop-tomcat7"></a><span data-ttu-id="91652-242">Tomcat7 시작 및 중지</span><span class="sxs-lookup"><span data-stu-id="91652-242">Start and stop Tomcat7</span></span>
<span data-ttu-id="91652-243">hello Tomcat7 서버는 설치할 때 자동으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-243">hello Tomcat7 server automatically starts when you install it.</span></span> <span data-ttu-id="91652-244">다음 명령을 hello로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-244">You can also start it with hello following command:</span></span>   

    sudo /etc/init.d/tomcat7 start

<span data-ttu-id="91652-245">toostop Tomcat7:</span><span class="sxs-lookup"><span data-stu-id="91652-245">toostop Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 stop

<span data-ttu-id="91652-246">Tomcat7 tooview hello 상태:</span><span class="sxs-lookup"><span data-stu-id="91652-246">tooview hello status of Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 status

<span data-ttu-id="91652-247">toorestart Tomcat 서비스:</span><span class="sxs-lookup"><span data-stu-id="91652-247">toorestart Tomcat services:</span></span> 

    sudo /etc/init.d/tomcat7 restart

### <a name="tomcat7-administration"></a><span data-ttu-id="91652-248">Tomcat7 관리</span><span class="sxs-lookup"><span data-stu-id="91652-248">Tomcat7 administration</span></span>
<span data-ttu-id="91652-249">Hello Tomcat 사용자 구성 파일 tooset 관리자 자격 증명을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-249">You can edit hello Tomcat user configuration file tooset up your admin credentials.</span></span> <span data-ttu-id="91652-250">다음 명령을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="91652-250">Use hello following command:</span></span>  

    sudo vi  /etc/tomcat7/tomcat-users.xml   

<span data-ttu-id="91652-251">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="91652-251">Here is an example:</span></span>  
![Hello sudo vi 명령 출력을 보여 주는 스크린샷][17]  

> [!NOTE]
> <span data-ttu-id="91652-253">Hello 관리자 사용자 이름에 대 한 강력한 암호를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="91652-253">Create a strong password for hello admin username.</span></span>  

<span data-ttu-id="91652-254">이 파일을 편집한 후 Tomcat7 서비스를 다시 시작 해야 hello 변경 내용이 적용 되는 명령 tooensure 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="91652-254">After editing this file, you should restart Tomcat7 services with hello following command tooensure that hello changes take effect:</span></span>  

    sudo /etc/init.d/tomcat7 restart  

<span data-ttu-id="91652-255">브라우저를 열고 다음을 입력 **http://<your tomcat server DNS name>/관리자/html** URL hello으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-255">Open your browser, and enter **http://<your tomcat server DNS name>/manager/html** as hello URL.</span></span> <span data-ttu-id="91652-256">이 문서에 대 한 hello 등 hello URL은 http://tomcatexample.cloudapp.net/manager/html입니다.</span><span class="sxs-lookup"><span data-stu-id="91652-256">For hello example in this article, hello URL is http://tomcatexample.cloudapp.net/manager/html.</span></span>  

<span data-ttu-id="91652-257">에 연결 하면 다음과 유사한 toohello 다음을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-257">After connecting, you should see something similar toohello following:</span></span>  
![Hello Tomcat 웹 응용 프로그램 관리자의 스크린샷][18]

## <a name="common-issues"></a><span data-ttu-id="91652-259">일반적인 문제</span><span class="sxs-lookup"><span data-stu-id="91652-259">Common issues</span></span>
### <a name="cant-access-hello-virtual-machine-with-tomcat-and-moodle-from-hello-internet"></a><span data-ttu-id="91652-260">Hello 인터넷에서에서 Tomcat 및 Moodle hello 가상 컴퓨터를 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-260">Can't access hello virtual machine with Tomcat and Moodle from hello Internet</span></span>
#### <a name="symptom"></a><span data-ttu-id="91652-261">증상</span><span class="sxs-lookup"><span data-stu-id="91652-261">Symptom</span></span>  
  <span data-ttu-id="91652-262">Tomcat 실행 중이지만 브라우저와 hello Tomcat 기본 페이지를 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-262">Tomcat is running but you can’t see hello Tomcat default page with your browser.</span></span>
#### <a name="possible-root-cause"></a><span data-ttu-id="91652-263">가능한 근본 원인</span><span class="sxs-lookup"><span data-stu-id="91652-263">Possible root cause</span></span>   

  * <span data-ttu-id="91652-264">hello Tomcat 수신 대기 포트를 hello Tomcat 트래픽에 대 한 가상 컴퓨터의 끝점의 개인 포트와 동일한 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91652-264">hello Tomcat listen port is not hello same as hello private port of your virtual machine's endpoint for Tomcat traffic.</span></span>  

     <span data-ttu-id="91652-265">포트를 수신 하는 공용 포트 및 개인 포트 끝점 설정 하 고 hello 개인 포트는 Tomcat hello와 동일 hello가 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-265">Check your public port and private port endpoint settings and make sure hello private port is hello same as hello Tomcat listen port.</span></span> <span data-ttu-id="91652-266">가상 컴퓨터의 끝점 구성에 대한 지침은 이 문서의 "1단계: 이미지 만들기" 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91652-266">See "Phase 1: Create an image" section of this article for instructions on configuring endpoints for your virtual machine.</span></span>  

     <span data-ttu-id="91652-267">toodetermine hello Tomcat 수신 대기 포트, /etc/httpd/conf/httpd.conf (Red Hat 릴리스) 또는 /etc/tomcat7/server.xml (Debian 릴리스)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="91652-267">toodetermine hello Tomcat listen port, open /etc/httpd/conf/httpd.conf (Red Hat release), or /etc/tomcat7/server.xml (Debian release).</span></span> <span data-ttu-id="91652-268">기본적으로 hello Tomcat 수신 대기 포트는 8080입니다.</span><span class="sxs-lookup"><span data-stu-id="91652-268">By default, hello Tomcat listen port is 8080.</span></span> <span data-ttu-id="91652-269">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="91652-269">Here is an example:</span></span>  

        <Connector port="8080" protocol="HTTP/1.1"  connectionTimeout="20000"   URIEncoding="UTF-8"            redirectPort="8443" />  

     <span data-ttu-id="91652-270">Debian 및 Ubuntu 원하는 toochange hello 기본 포트의 Tomcat 수신 (예: 8081)와 같은 가상 컴퓨터를 사용 하는, 하는 경우 hello 운영 체제에 대 한 hello 포트를 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-270">If you are using a virtual machine like Debian or Ubuntu and you want toochange hello default port of Tomcat Listen (for example 8081), you should also open hello port for hello operating system.</span></span> <span data-ttu-id="91652-271">첫째, hello 프로필을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="91652-271">First, open hello profile:</span></span>  

        sudo vi /etc/default/tomcat7  

     <span data-ttu-id="91652-272">그런 다음 hello 마지막 줄의 주석 처리 제거 하 고 변경 "no" 너무 "yes"입니다.</span><span class="sxs-lookup"><span data-stu-id="91652-272">Then uncomment hello last line and change “no” too“yes”.</span></span>  

        AUTHBIND=yes
  2. <span data-ttu-id="91652-273">hello 방화벽 Tomcat의 hello 수신 대기 포트를 비활성화 했습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-273">hello firewall has disabled hello listen port of Tomcat.</span></span>

     <span data-ttu-id="91652-274">Hello Tomcat 기본 페이지 hello 로컬 호스트에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-274">You can only see hello Tomcat default page from hello local host.</span></span> <span data-ttu-id="91652-275">hello 문제는 주로 기대 tooby Tomcat hello 포트 hello 방화벽에 의해 차단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91652-275">hello problem is most likely that hello port, which is listened tooby Tomcat, is blocked by hello firewall.</span></span> <span data-ttu-id="91652-276">Hello w3m 도구 toobrowse hello 웹 페이지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-276">You can use hello w3m tool toobrowse hello webpage.</span></span> <span data-ttu-id="91652-277">hello 다음 명령을 설치 w3m 및 toohello Tomcat 기본 페이지를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-277">hello following commands install w3m and browse toohello Tomcat default page:</span></span>  


        <span data-ttu-id="91652-278">sudo yum  install w3m w3m-img</span><span class="sxs-lookup"><span data-stu-id="91652-278">sudo yum  install w3m w3m-img</span></span>


        <span data-ttu-id="91652-279">w3m http://localhost:8080</span><span class="sxs-lookup"><span data-stu-id="91652-279">w3m http://localhost:8080</span></span>  
#### <a name="solution"></a><span data-ttu-id="91652-280">해결 방법</span><span class="sxs-lookup"><span data-stu-id="91652-280">Solution</span></span>

  * <span data-ttu-id="91652-281">Hello Tomcat 수신 대기 포트 트래픽 toohello 가상 컴퓨터에 대 한 hello 끝점의 hello 개인 포트로 hello 동일은, hello 개인 포트를 변경할 필요 있습니다 toobe hello Tomcat 수신 대기 포트 hello와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-281">If hello Tomcat listen port is not hello same as hello private port of hello endpoint for traffic toohello virtual machine, you need change hello private port toobe hello same as hello Tomcat listen port.</span></span>   
  2. <span data-ttu-id="91652-282">방화벽/iptables 하 여 hello 문제가 발생 하는 경우 다음 줄 너무/등/sysconfig/iptables hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-282">If hello issue is caused by firewall/iptables, add hello following lines too/etc/sysconfig/iptables.</span></span> <span data-ttu-id="91652-283">https 트래픽에 대 한 hello 두 번째 줄만 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-283">hello second line is only needed for https traffic:</span></span>  

      <span data-ttu-id="91652-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span><span class="sxs-lookup"><span data-stu-id="91652-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span></span>

      <span data-ttu-id="91652-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span><span class="sxs-lookup"><span data-stu-id="91652-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span></span>  

     > [!IMPORTANT]
     > <span data-ttu-id="91652-286">Hello 이전 줄은 전역적으로 hello 다음과 같은 액세스를 제한 하 고 모든 줄 위에 배치 됩니다 있는지 확인:-A 입력-j 거부-거부-와 icmp 호스트 금지</span><span class="sxs-lookup"><span data-stu-id="91652-286">Make sure hello previous lines are positioned above any lines that would globally restrict access, such as hello following: -A INPUT -j REJECT --reject-with icmp-host-prohibited</span></span>



<span data-ttu-id="91652-287">tooreload hello iptables, hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-287">tooreload hello iptables, run hello following command:</span></span>

    service iptables restart

<span data-ttu-id="91652-288">CentOS 6.3에서 테스트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-288">This has been tested on CentOS 6.3.</span></span>

### <a name="permission-denied-when-you-upload-project-files-toovarlibtomcat7webapps"></a><span data-ttu-id="91652-289">사용 권한이 거부 프로젝트 업로드 하면 파일 너무/var/lib/tomcat7/webapps /</span><span class="sxs-lookup"><span data-stu-id="91652-289">Permission denied when you upload project files too/var/lib/tomcat7/webapps/</span></span>
#### <a name="symptom"></a><span data-ttu-id="91652-290">증상</span><span class="sxs-lookup"><span data-stu-id="91652-290">Symptom</span></span>
  <span data-ttu-id="91652-291">SFTP 클라이언트 (예: FileZilla) tooconnect tooyour 가상 컴퓨터를 사용 하 고 너무/var/lib/tomcat7/webapps 이동/toopublish 오류 메시지와 비슷한 toohello 다음 가져올 사이트:</span><span class="sxs-lookup"><span data-stu-id="91652-291">When you use an SFTP client (such as FileZilla) tooconnect tooyour virtual machine and navigate too/var/lib/tomcat7/webapps/ toopublish your site, you get an error message similar toohello following:</span></span>  

     status:    Listing directory /var/lib/tomcat7/webapps
     Command:    put "C:\Users\liang\Desktop\info.jsp" "info.jsp"
     Error:    /var/lib/tomcat7/webapps/info.jsp: open for write: permission denied
     Error:    File transfer failed
#### <a name="possible-root-cause"></a><span data-ttu-id="91652-292">가능한 근본 원인</span><span class="sxs-lookup"><span data-stu-id="91652-292">Possible root cause</span></span>
  <span data-ttu-id="91652-293">해야 권한을 tooaccess hello /var/lib/tomcat7/webapps 폴더가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-293">You have no permissions tooaccess hello /var/lib/tomcat7/webapps folder.</span></span>  
#### <a name="solution"></a><span data-ttu-id="91652-294">해결 방법</span><span class="sxs-lookup"><span data-stu-id="91652-294">Solution</span></span>  
  <span data-ttu-id="91652-295">Hello 루트 계정에서 tooget 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-295">You need tooget permission from hello root account.</span></span> <span data-ttu-id="91652-296">루트 toohello hello 컴퓨터를 프로 비전 할 때 사용한 사용자 이름에서 해당 폴더의 hello 소유권을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-296">You can change hello ownership of that folder from root toohello username you used when you provisioned hello machine.</span></span> <span data-ttu-id="91652-297">Hello azureuser 계정 이름의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-297">Here is an example with hello azureuser account name:</span></span>  

     sudo chown azureuser -R /var/lib/tomcat7/webapps

  <span data-ttu-id="91652-298">너무 디렉터리 내의 모든 파일에 대 한 hello-R 옵션 tooapply hello 사용 권한을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-298">Use hello -R option tooapply hello permissions for all files inside of a directory too.</span></span>  

  <span data-ttu-id="91652-299">이 명령은 디렉터리에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-299">This command also works for directories.</span></span> <span data-ttu-id="91652-300">hello-R 옵션 변경 내용은 모든 파일 및 디렉터리 hello 디렉터리 내에 대 한 권한을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-300">hello -R option changes hello permissions for all files and directories inside hello directory.</span></span> <span data-ttu-id="91652-301">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="91652-301">Here is an example:</span></span>  

     sudo chown -R username:group directory  

  <span data-ttu-id="91652-302">이 명령은 모든 파일 및 hello 디렉터리 내에 있는 디렉터리에 대 한 소유권 (사용자 및 그룹)를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-302">This command changes ownership (both user and group) for all files and directories that are inside hello directory.</span></span>  

  <span data-ttu-id="91652-303">hello 다음 명령은 변경 hello 폴더 디렉터리의 hello 허가 합니다.</span><span class="sxs-lookup"><span data-stu-id="91652-303">hello following command only changes hello permission of hello folder directory.</span></span> <span data-ttu-id="91652-304">hello 파일 및 폴더 hello 디렉터리 내의 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91652-304">hello files and folders inside hello directory are not changed.</span></span>  

     sudo chown username:group directory

[1]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-01.png
[2]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-02.png
[3]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-03.png
[4]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-04.png
[5]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-05.png
[6]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-06.png
[7]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-07.png
[8]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-08.png
[9]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-09.png
[10]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-10.png
[11]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-11.png
[12]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-12.png
[13]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-13.png
[14]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-14.png
[15]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-15.png
[16]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-16.png
[17]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-17.png
[18]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-18.png
