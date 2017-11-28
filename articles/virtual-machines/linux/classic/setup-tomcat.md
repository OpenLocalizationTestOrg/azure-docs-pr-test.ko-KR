---
title: "Linux 가상 컴퓨터에 Apache Tomcat 설치 | Microsoft Docs"
description: "Linux를 실행하는 Azure Virtual Machines를 사용하여 Apache Tomcat7을 설치하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: fa30c78a5a5d458ba8845c3c10b87538427786c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-tomcat7-on-a-linux-virtual-machine-with-azure"></a><span data-ttu-id="65f8b-103">Azure를 사용하여 Linux 가상 컴퓨터에 Tomcat7 설치</span><span class="sxs-lookup"><span data-stu-id="65f8b-103">Set up Tomcat7 on a Linux virtual machine with Azure</span></span>
<span data-ttu-id="65f8b-104">Apache Tomcat(또는 간단히 Tomcat, 이전에는 Jakarta Tomcat이라고도 함)은 ASF(Apache Software Foundation)에서 개발한 오픈 소스 웹 서버 및 서블릿 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-104">Apache Tomcat (or simply Tomcat, also formerly called Jakarta Tomcat) is an open source web server and servlet container developed by the Apache Software Foundation (ASF).</span></span> <span data-ttu-id="65f8b-105">Tomcat은 Sun Microsystems의 Java Servlet 및 JSP(JavaServer Pages) 사양을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-105">Tomcat implements the Java Servlet and the JavaServer Pages (JSP) specifications from Sun Microsystems.</span></span> <span data-ttu-id="65f8b-106">Tomcat은 Java 코드를 실행할 수 있는 순수한 Java HTTP 웹 서버 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-106">Tomcat provides a pure Java HTTP web server environment in which to run Java code.</span></span> <span data-ttu-id="65f8b-107">가장 단순한 구성의 경우 Tomcat은 단일 운영 체제 프로세스로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-107">In the simplest configuration, Tomcat runs in a single operating system process.</span></span> <span data-ttu-id="65f8b-108">이 프로세스에서는 JVM(Java Virtual Machine)을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-108">This process runs a Java virtual machine (JVM).</span></span> <span data-ttu-id="65f8b-109">브라우저에서 Tomcat으로 전송되는 모든 HTTP 요청은 Tomcat 프로세스에서 별도의 스레드로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-109">Every HTTP request from a browser to Tomcat is processed as a separate thread in the Tomcat process.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="65f8b-110">Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델, 즉 [Azure Resource Manager 및 클래식](../../../resource-manager-deployment-model.md) 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-110">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="65f8b-111">이 문서에서는 클래식 배포 모델을 사용하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-111">This article covers how to use the classic deployment model.</span></span> <span data-ttu-id="65f8b-112">대부분의 새로운 배포에서는 Azure Resource Manager 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-112">We recommend that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="65f8b-113">Resource Manager 템플릿을 사용하여 Open JDK 및 Tomcat이 있는 Ubuntu VM을 배포하려면 [이 문서 ](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="65f8b-113">To use a Resource Manager template to deploy an Ubuntu VM with Open JDK and Tomcat, see [this article](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span></span>

<span data-ttu-id="65f8b-114">이 문서에서는 Tomcat7을 Linux 이미지에 설치하고 이를 Azure에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-114">In this article, you will install Tomcat7 on a Linux image and deploy it in Azure.</span></span>  

<span data-ttu-id="65f8b-115">다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-115">You will learn:</span></span>  

* <span data-ttu-id="65f8b-116">Azure에서 가상 컴퓨터를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="65f8b-116">How to create a virtual machine in Azure.</span></span>
* <span data-ttu-id="65f8b-117">Tomcat7을 위한 가상 컴퓨터를 준비하는 방법</span><span class="sxs-lookup"><span data-stu-id="65f8b-117">How to prepare the virtual machine for Tomcat7.</span></span>
* <span data-ttu-id="65f8b-118">Tomcat7을 설치하는 방법</span><span class="sxs-lookup"><span data-stu-id="65f8b-118">How to install Tomcat7.</span></span>

<span data-ttu-id="65f8b-119">이미 Azure 구독이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-119">It is assumed that you already have an Azure subscription.</span></span>  <span data-ttu-id="65f8b-120">그렇지 않으면 [Azure 웹 사이트](https://azure.microsoft.com/)에서 무료 평가판을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-120">If not, you can sign up for a free trial at [the Azure website](https://azure.microsoft.com/).</span></span> <span data-ttu-id="65f8b-121">MSDN 구독이 있는 경우 [Microsoft Azure 특별 가격: MSDN, MPN 및 BizSpark 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="65f8b-121">If you have an MSDN subscription, see [Microsoft Azure Special Pricing: MSDN, MPN, and BizSpark Benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span></span> <span data-ttu-id="65f8b-122">Azure에 대한 자세한 내용은 [Azure 정의](https://azure.microsoft.com/overview/what-is-azure/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="65f8b-122">To learn more about Azure, see [What is Azure?](https://azure.microsoft.com/overview/what-is-azure/).</span></span>

<span data-ttu-id="65f8b-123">이 문서에서는 사용자가 Tomcat 및 Linux에 대한 기본적인 실무 지식을 갖추고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-123">This article assumes that you have a basic working knowledge of Tomcat and Linux.</span></span>  

## <a name="phase-1-create-an-image"></a><span data-ttu-id="65f8b-124">1단계: 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="65f8b-124">Phase 1: Create an image</span></span>
<span data-ttu-id="65f8b-125">이 단계에서는 Azure에서 Linux 이미지를 사용하여 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-125">In this phase, you will create a virtual machine by using a Linux image in Azure.</span></span>  

### <a name="step-1-generate-an-ssh-authentication-key"></a><span data-ttu-id="65f8b-126">1단계: SSH 인증 키 생성</span><span class="sxs-lookup"><span data-stu-id="65f8b-126">Step 1: Generate an SSH authentication key</span></span>
<span data-ttu-id="65f8b-127">SSH는 시스템 관리자에게 중요한 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-127">SSH is an important tool for system administrators.</span></span> <span data-ttu-id="65f8b-128">그러나 사람이 식별할 수 있는 암호를 기반으로 하여 액세스 보안을 구성하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-128">However, configuring access security based on a human-determined password is not recommended.</span></span> <span data-ttu-id="65f8b-129">악의적인 사용자는 사용자 이름 및 취약한 암호를 기반으로 하는 시스템에 침입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-129">Malicious users can break into your system based on a username and a weak password.</span></span>

<span data-ttu-id="65f8b-130">하지만 암호를 걱정하지 않고 원격 액세스를 허용하는 좋은 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-130">The good news is that there is a way to leave remote access open and not worry about passwords.</span></span> <span data-ttu-id="65f8b-131">이 방법은 비대칭 암호화를 사용하는 인증으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-131">This method consists of authentication with asymmetric cryptography.</span></span> <span data-ttu-id="65f8b-132">사용자의 개인 키가 인증을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-132">The user’s private key is the one that grants the authentication.</span></span> <span data-ttu-id="65f8b-133">사용자 계정을 잠그면 암호 인증을 허용하지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-133">You can even lock the user’s account to not allow password authentication.</span></span>

<span data-ttu-id="65f8b-134">이 방법의 또 다른 이점은 서버마다 다른 암호를 사용하여 로그인할 필요가 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-134">Another advantage of this method is that you do not need different passwords to sign in to different servers.</span></span> <span data-ttu-id="65f8b-135">모든 서버에서 개인 키를 사용하여 인증할 수 있으므로 여러 암호를 기억할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-135">You can authenticate by using the personal private key on all servers, which prevents you from having to remember several passwords.</span></span>



<span data-ttu-id="65f8b-136">SSH 인증 키를 생성하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-136">Follow these steps to generate the SSH authentication key.</span></span>

1. <span data-ttu-id="65f8b-137">PuTTYgen을 다운로드하고 설치합니다(다운로드 위치: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)).</span><span class="sxs-lookup"><span data-stu-id="65f8b-137">Download and install PuTTYgen from the following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
2. <span data-ttu-id="65f8b-138">Puttygen.exe를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-138">Run Puttygen.exe.</span></span>
3. <span data-ttu-id="65f8b-139">**생성** 을 클릭하여 키를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-139">Click **Generate** to generate the keys.</span></span> <span data-ttu-id="65f8b-140">이 과정에서 창의 빈 영역 위로 마우스를 이동하여 임의성을 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-140">In the process, you can increase randomness by moving the mouse over the blank area in the window.</span></span>  
   <span data-ttu-id="65f8b-141">![새 키 생성 단추를 보여 주는 PuTTY 키 생성기 스크린샷][1]</span><span class="sxs-lookup"><span data-stu-id="65f8b-141">![PuTTY Key Generator screenshot that shows the generate new key button][1]</span></span>
4. <span data-ttu-id="65f8b-142">생성 프로세스가 끝나면 Puttygen.exe에서 새 공개 키를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-142">After the generate process, Puttygen.exe will show your new public key.</span></span>  
   ![새 공개 키와 개인 키 저장 단추를 보여 주는 PuTTY 키 생성기 스크린샷][2]
5. <span data-ttu-id="65f8b-144">공개 키를 선택하여 복사하고 publicKey.pem 파일에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-144">Select and copy the public key, and save it in a file named publicKey.pem.</span></span> <span data-ttu-id="65f8b-145">저장된 공개 키의 파일 형식은 원하는 공개 키와 다르므로 **공개 키 저장**을 클릭하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="65f8b-145">Don’t click **Save public key**, because the saved public key’s file format is different from the public key we want.</span></span>
6. <span data-ttu-id="65f8b-146">**개인 키 저장**을 클릭하고 privateKey.ppk 파일에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-146">Click **Save private key**, and save it in a file named privateKey.ppk.</span></span>

### <a name="step-2-create-the-image-in-the-azure-portal"></a><span data-ttu-id="65f8b-147">2단계: Azure Portal에서 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="65f8b-147">Step 2: Create the image in the Azure portal</span></span>
1. <span data-ttu-id="65f8b-148">[포털](https://portal.azure.com/)에서 작업 표시줄에서 **새로 만들기**를 클릭하여 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-148">In the [portal](https://portal.azure.com/), click **New** in the task bar to create an image.</span></span> <span data-ttu-id="65f8b-149">그런 다음 필요에 따라 Linux 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-149">Then choose the Linux image that is based on your needs.</span></span> <span data-ttu-id="65f8b-150">다음 예제에서는 Ubuntu 14.04 이미지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-150">The following example uses the Ubuntu 14.04 image.</span></span>
<span data-ttu-id="65f8b-151">![새로 만들기 단추를 보여 주는 포털의 스크린샷][3]</span><span class="sxs-lookup"><span data-stu-id="65f8b-151">![Screenshot of the portal that shows the New button][3]</span></span>

2. <span data-ttu-id="65f8b-152">**호스트 이름**에서 사용자와 인터넷 클라이언트가 이 가상 컴퓨터에 액세스하는 데 사용할 URL의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-152">For **Host Name**, specify the name for the URL that you and Internet clients will use to access this virtual machine.</span></span> <span data-ttu-id="65f8b-153">DNS 이름의 마지막 부분을 정의합니다(예: tomcatdemo).</span><span class="sxs-lookup"><span data-stu-id="65f8b-153">Define the last part of the DNS name, for example, tomcatdemo.</span></span> <span data-ttu-id="65f8b-154">그러면 Azure에서 tomcatdemo.cloudapp.net과 같은 URL을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-154">Azure will then generate the URL as tomcatdemo.cloudapp.net.</span></span>  

3. <span data-ttu-id="65f8b-155">**SSH 인증 키**에서 PuTTYgen으로 생성한 공개 키가 포함된 publicKey.pem 파일의 키 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-155">For **SSH Authentication Key**, copy the key value from the publicKey.pem file, which contains the public key generated by PuTTYgen.</span></span>  
<span data-ttu-id="65f8b-156">![포털의 SSH 인증 키 상자][4]</span><span class="sxs-lookup"><span data-stu-id="65f8b-156">![SSH Authentication Key box in the portal][4]</span></span>

4. <span data-ttu-id="65f8b-157">필요에 따라 다른 설정을 구성한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-157">Configure other settings as needed, and then click **Create**.</span></span>  

## <a name="phase-2-prepare-your-virtual-machine-for-tomcat7"></a><span data-ttu-id="65f8b-158">2단계: Tomcat7에 대해 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="65f8b-158">Phase 2: Prepare your virtual machine for Tomcat7</span></span>
<span data-ttu-id="65f8b-159">이 단계에서는 Tomcat 트래픽에 대한 끝점을 구성한 다음 새 가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-159">In this phase, you will configure an endpoint for Tomcat traffic, and then connect to your new virtual machine.</span></span>

### <a name="step-1-open-the-http-port-to-allow-web-access"></a><span data-ttu-id="65f8b-160">1단계: 웹 액세스를 허용하도록 HTTP 포트 열기</span><span class="sxs-lookup"><span data-stu-id="65f8b-160">Step 1: Open the HTTP port to allow web access</span></span>
<span data-ttu-id="65f8b-161">Azure의 끝점은 공용 및 개인 포트와 함께 TCP 또는 UDP 프로토콜로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-161">Endpoints in Azure consist of a TCP or UDP protocol, along with a public and private port.</span></span> <span data-ttu-id="65f8b-162">개인 포트는 가상 컴퓨터에서 서비스가 수신 대기하는 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-162">The private port is the port that the service is listening to on the virtual machine.</span></span> <span data-ttu-id="65f8b-163">공용 포트는 외부에서 Azure 클라우드 서비스가 들어오는 인터넷 기반 수신 트래픽을 수신 대기하는 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-163">The public port is the port that the Azure cloud service listens to externally for incoming, Internet-based traffic.</span></span>  

<span data-ttu-id="65f8b-164">8080 TCP 포트는 Tomcat에서 수신 대기하는 데 사용하는 기본 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-164">TCP port 8080 is the default port number that Tomcat uses to listen.</span></span> <span data-ttu-id="65f8b-165">Azure 끝점에서 이 포트를 열면 사용자와 다른 인터넷 클라이언트가 Tomcat 페이지에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-165">If this port is opened with an Azure endpoint, you and other Internet clients can access Tomcat pages.</span></span>  

1. <span data-ttu-id="65f8b-166">포털에서 **찾아보기** > **가상 컴퓨터**를 차례로 클릭한 다음 만든 가상 컴퓨터를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-166">In the portal, click **Browse** > **Virtual machines**, and then click the virtual machine that you created.</span></span>  
   <span data-ttu-id="65f8b-167">![가상 컴퓨터 디렉터리의 스크린샷][5]</span><span class="sxs-lookup"><span data-stu-id="65f8b-167">![Screenshot of the Virtual machines directory][5]</span></span>
2. <span data-ttu-id="65f8b-168">가상 컴퓨터에 끝점을 추가하려면 **끝점** 확인란을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-168">To add an endpoint to your virtual machine, click the **Endpoints** box.</span></span>
   <span data-ttu-id="65f8b-169">![끝점 확인란을 보여 주는 스크린샷][6]</span><span class="sxs-lookup"><span data-stu-id="65f8b-169">![Screenshot that shows the Endpoints box][6]</span></span>
3. <span data-ttu-id="65f8b-170">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-170">Click **Add**.</span></span>  

   1. <span data-ttu-id="65f8b-171">끝점의 경우 **끝점**에 끝점 이름을 입력한 다음 **공용 포트**에 80을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-171">For the endpoint, enter a name for the endpoint in **Endpoint**, and then enter 80 in **Public Port**.</span></span>  

      <span data-ttu-id="65f8b-172">80으로 설정하면 Tomcat에 액세스하는 데 사용되는 URL에 포트 번호를 포함할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-172">If you set it to 80, you don’t need to include the port number in the URL that is used to access Tomcat.</span></span> <span data-ttu-id="65f8b-173">예를 들면 http://tomcatdemo.cloudapp.net과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-173">For example, http://tomcatdemo.cloudapp.net.</span></span>    

      <span data-ttu-id="65f8b-174">다른 값(예: 81)으로 설정하면 Tomcat에 액세스할 수 있도록 URL에 포트 번호를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-174">If you set it to another value, such as 81, you need to add the port number to the URL to access Tomcat.</span></span> <span data-ttu-id="65f8b-175">예를 들면 http://tomcatdemo.cloudapp.net:81/과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-175">For example,  http://tomcatdemo.cloudapp.net:81/.</span></span>
   2. <span data-ttu-id="65f8b-176">**개인 포트**에 8080을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-176">Enter 8080 in **Private Port**.</span></span> <span data-ttu-id="65f8b-177">기본적으로 Tomcat은 8080 TCP 포트에서 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-177">By default, Tomcat listens on TCP port 8080.</span></span> <span data-ttu-id="65f8b-178">Tomcat의 기본 수신 대기 포트를 변경한 경우 **개인 포트**를 Tomcat 수신 대기 포트와 같도록 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-178">If you changed the default listen port of Tomcat, you should update **Private Port** to be the same as the Tomcat listen port.</span></span>  
      <span data-ttu-id="65f8b-179">![추가 명령, 공용 포트 및 개인 포트를 보여 주는 UI 스크린샷][7]</span><span class="sxs-lookup"><span data-stu-id="65f8b-179">![Screenshot of UI that shows Add command, Public Port, and Private Port][7]</span></span>
4. <span data-ttu-id="65f8b-180">**확인** 을 클릭하여 가상 컴퓨터에 끝점을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-180">Click **OK** to add the endpoint to your virtual machine.</span></span>

### <a name="step-2-connect-to-the-image-you-created"></a><span data-ttu-id="65f8b-181">2단계: 만든 이미지에 연결</span><span class="sxs-lookup"><span data-stu-id="65f8b-181">Step 2: Connect to the image you created</span></span>
<span data-ttu-id="65f8b-182">가상 컴퓨터에 연결하기 위한 SSH 도구를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-182">You can choose any SSH tool to connect to your virtual machine.</span></span> <span data-ttu-id="65f8b-183">이 예제에서는 PuTTY를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-183">In this example, we use PuTTY.</span></span>  

1. <span data-ttu-id="65f8b-184">포털에서 가상 컴퓨터의 DNS 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-184">Get the DNS name of your virtual machine from the portal.</span></span>
    1. <span data-ttu-id="65f8b-185">**찾아보기** > **가상 컴퓨터**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-185">Click **Browse** > **Virtual machines**.</span></span>
    2. <span data-ttu-id="65f8b-186">가상 컴퓨터의 이름을 선택한 다음 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-186">Select the name of your virtual machine, and then click **Properties**.</span></span>
    3. <span data-ttu-id="65f8b-187">**속성** 타일에서 **도메인 이름** 상자를 보고 DNS 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-187">In the **Properties** tile, look in the **Domain Name** box to get the DNS name.</span></span>  

2. <span data-ttu-id="65f8b-188">**SSH** 상자에서 SSH 연결의 포트 번호를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-188">Get the port number for SSH connections from the **SSH** box.</span></span>  
<span data-ttu-id="65f8b-189">![SSH 연결 포트 번호를 보여 주는 스크린샷][8]</span><span class="sxs-lookup"><span data-stu-id="65f8b-189">![Screenshot that shows the SSH connection port number][8]</span></span>

3. <span data-ttu-id="65f8b-190">[PuTTY](http://www.putty.org/)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-190">Download [PuTTY](http://www.putty.org/).</span></span>  

4. <span data-ttu-id="65f8b-191">다운로드한 후 Putty.exe 실행 파일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-191">After downloading, click the executable file Putty.exe.</span></span> <span data-ttu-id="65f8b-192">PuTTY 구성에서 가상 컴퓨터의 속성에서 가져온 호스트 이름과 포트 번호로 기본 옵션을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-192">In PuTTY configuration, configure the basic options with the host name and port number that is obtained from the properties of your virtual machine.</span></span>   
![PuTTY 구성 호스트 이름 및 포트 옵션을 보여 주는 스크린샷][9]

5. <span data-ttu-id="65f8b-194">왼쪽 창에서 **연결** > **SSH** > **인증**을 차례로 클릭한 다음 **찾아보기**를 클릭하여 privateKey.ppk 파일의 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-194">In the left pane, click **Connection** > **SSH** > **Auth**, and then click **Browse** to specify the location of the privateKey.ppk file.</span></span> <span data-ttu-id="65f8b-195">privateKey.ppk 파일에는 이미 이 문서의 "1단계: 이미지 만들기" 섹션의 PuTTYgen에서 생성한 개인 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-195">The privateKey.ppk file contains the private key that is generated by PuTTYgen earlier in the "Phase 1: Create an image" section of this article.</span></span>  
<span data-ttu-id="65f8b-196">![연결 디렉터리 계층 구조와 찾아보기 단추를 보여 주는 스크린샷][10]</span><span class="sxs-lookup"><span data-stu-id="65f8b-196">![Screenshot that shows the Connection directory hierarchy and Browse button][10]</span></span>

6. <span data-ttu-id="65f8b-197">**열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-197">Click **Open**.</span></span> <span data-ttu-id="65f8b-198">메시지 상자에 경고 메시지가 표시될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-198">You might be alerted by a message box.</span></span> <span data-ttu-id="65f8b-199">DNS 이름과 포트 번호를 올바르게 구성한 경우 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-199">If you have configured the DNS name and port number correctly, click **Yes**.</span></span>
<span data-ttu-id="65f8b-200">![알림을 보여 주는 스크린샷][11]</span><span class="sxs-lookup"><span data-stu-id="65f8b-200">![Screenshot that shows the notification][11]</span></span>

7. <span data-ttu-id="65f8b-201">사용자 이름을 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-201">You are prompted to enter your username.</span></span>  
![사용자 이름을 입력하는 위치를 보여 주는 스크린샷][12]

8. <span data-ttu-id="65f8b-203">이 문서 앞부분의 "1단계: 이미지 만들기" 섹션에서 가상 컴퓨터를 만드는 데 사용한 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-203">Enter the username that you used to create the virtual machine in the "Phase 1: Create an image" section earlier in this article.</span></span> <span data-ttu-id="65f8b-204">다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-204">You will see something like the following:</span></span>  
![인증 확인을 보여 주는 스크린샷][13]

## <a name="phase-3-install-software"></a><span data-ttu-id="65f8b-206">3단계: 소프트웨어 설치</span><span class="sxs-lookup"><span data-stu-id="65f8b-206">Phase 3: Install software</span></span>
<span data-ttu-id="65f8b-207">이 단계에서는 Java Runtime Environment, Tomcat7 및 기타 Tomcat7 구성 요소를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-207">In this phase, you install the Java runtime environment, Tomcat7, and other Tomcat7 components.</span></span>  

### <a name="java-runtime-environment"></a><span data-ttu-id="65f8b-208">Java Runtime Environment</span><span class="sxs-lookup"><span data-stu-id="65f8b-208">Java runtime environment</span></span>
<span data-ttu-id="65f8b-209">Tomcat은 Java로 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-209">Tomcat is written in Java.</span></span> <span data-ttu-id="65f8b-210">JDK(Java Development Kit)에는 두 가지 종류의 JDK, 즉 OpenJDK와 Oracle JDK가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-210">There are two kinds of Java Development Kits (JDKs), OpenJDK and Oracle JDK.</span></span> <span data-ttu-id="65f8b-211">원하는 JDK를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-211">You can choose the one you want.</span></span>  

> [!NOTE]
> <span data-ttu-id="65f8b-212">두 JDK는 Java API의 클래스와 거의 동일한 코드를 갖추고 있지만 가상 시스템의 코드와는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-212">Both JDKs have almost the same code for the classes in the Java API, but the code for the virtual machine is different.</span></span> <span data-ttu-id="65f8b-213">OpenJDK는 개방형 라이브러리를 사용하는 반면 Oracle JDK는 폐쇄형 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-213">OpenJDK tends to use open libraries, while Oracle JDK tends to use closed ones.</span></span> <span data-ttu-id="65f8b-214">Oracle JDK는 더 많은 클래스와 일부 수정된 버그를 포함하고 있지만 OpenJDK보다 더 안정적입니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-214">Oracle JDK has more classes and some fixed bugs, and Oracle JDK is more stable than OpenJDK.</span></span>

#### <a name="install-openjdk"></a><span data-ttu-id="65f8b-215">OpenJDK 설치</span><span class="sxs-lookup"><span data-stu-id="65f8b-215">Install OpenJDK</span></span>  

<span data-ttu-id="65f8b-216">다음 명령을 사용하여 OpenJDK를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-216">Use the following command to download OpenJDK.</span></span>   

    sudo apt-get update  
    sudo apt-get install openjdk-7-jre  


* <span data-ttu-id="65f8b-217">JDK 파일을 포함할 디렉터리를 만들려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-217">To create a directory to contain the JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="65f8b-218">JDK 파일을 /usr/lib/jvm/ 디렉터리에 추출하려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-218">To extract the JDK files into the /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/

#### <a name="install-oracle-jdk"></a><span data-ttu-id="65f8b-219">Oracle JDK 설치</span><span class="sxs-lookup"><span data-stu-id="65f8b-219">Install Oracle JDK</span></span>


<span data-ttu-id="65f8b-220">다음 명령을 사용하여 Oracle 웹 사이트에서 Oracle JDK를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-220">Use the following command to download Oracle JDK from the Oracle website.</span></span>  

     wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz  
* <span data-ttu-id="65f8b-221">JDK 파일을 포함할 디렉터리를 만들려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-221">To create a directory to contain the JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="65f8b-222">JDK 파일을 /usr/lib/jvm/ 디렉터리에 추출하려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-222">To extract the JDK files into the /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/  
* <span data-ttu-id="65f8b-223">Oracle JDK를 기본 Java 가상 컴퓨터로 설정하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-223">To set Oracle JDK as the default Java virtual machine:</span></span>  

        sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_05/bin/java 100  

        sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_05/bin/javac 100  

#### <a name="confirm-that-java-installation-is-successful"></a><span data-ttu-id="65f8b-224">Java 설치가 성공적인지 확인</span><span class="sxs-lookup"><span data-stu-id="65f8b-224">Confirm that Java installation is successful</span></span>
<span data-ttu-id="65f8b-225">다음과 같은 명령을 사용하여 Java Runtime Environment가 올바르게 설치되었는지 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-225">You can use a command like the following to test if the Java runtime environment is installed correctly:</span></span>  

    java -version  

<span data-ttu-id="65f8b-226">OpenJDK를 설치한 경우 다음과 같은 메시지가 표시됩니다. ![OpenJDK 설치 성공 메시지][14]</span><span class="sxs-lookup"><span data-stu-id="65f8b-226">If you installed OpenJDK, you should see a message like the following: ![Successful OpenJDK installation message][14]</span></span>

<span data-ttu-id="65f8b-227">Oracle JDK를 설치한 경우 다음과 같은 메시지가 표시됩니다. ![Oracle JDK 설치 성공 메시지][15]</span><span class="sxs-lookup"><span data-stu-id="65f8b-227">If you installed Oracle JDK, you should see a message like the following: ![Successful Oracle JDK installation message][15]</span></span>

### <a name="install-tomcat7"></a><span data-ttu-id="65f8b-228">Tomcat7 설치</span><span class="sxs-lookup"><span data-stu-id="65f8b-228">Install Tomcat7</span></span>
<span data-ttu-id="65f8b-229">다음 명령을 사용하여 Tomcat7을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-229">Use the following command to install Tomcat7.</span></span>  

    sudo apt-get install tomcat7  

<span data-ttu-id="65f8b-230">Tomcat7을 사용하지 않는 경우 이 명령의 적절한 변형을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-230">If you are not using Tomcat7, use the appropriate variation of this command.</span></span>  

#### <a name="confirm-that-tomcat7-installation-is-successful"></a><span data-ttu-id="65f8b-231">Tomcat7 설치가 성공적인지 확인</span><span class="sxs-lookup"><span data-stu-id="65f8b-231">Confirm that Tomcat7 installation is successful</span></span>
<span data-ttu-id="65f8b-232">Tomcat7이 성공적으로 설치되었는지 확인하려면 Tomcat 서버의 DNS 이름을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-232">To check if Tomcat7 is successfully installed, browse to your Tomcat server’s DNS name.</span></span> <span data-ttu-id="65f8b-233">이 문서의 예제 URL은 http://tomcatexample.cloudapp.net/입니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-233">In this article, the example URL is http://tomcatexample.cloudapp.net/.</span></span> <span data-ttu-id="65f8b-234">다음과 같은 메시지가 표시되면 Tomcat7이 제대로 설치된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-234">If you see a message like the following, Tomcat7 is installed correctly.</span></span>
<span data-ttu-id="65f8b-235">![Tomcat7 설치 성공 메시지][16]</span><span class="sxs-lookup"><span data-stu-id="65f8b-235">![Successful Tomcat7 installation message][16]</span></span>

### <a name="install-other-tomcat7-components"></a><span data-ttu-id="65f8b-236">기타 Tomcat7 구성 요소 설치</span><span class="sxs-lookup"><span data-stu-id="65f8b-236">Install other Tomcat7 components</span></span>
<span data-ttu-id="65f8b-237">설치할 수 있는 다른 선택적 Tomcat 구성 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-237">There are other optional Tomcat components that you can install.</span></span>  

<span data-ttu-id="65f8b-238">**sudo apt-cache search tomcat7** 명령을 사용하여 사용할 수 있는 모든 구성 요소를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-238">Use the **sudo apt-cache search tomcat7** command to see all of the available components.</span></span> <span data-ttu-id="65f8b-239">다음 명령을 사용하여 몇 가지 유용한 구성 요소를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-239">Use the following commands to install some useful components.</span></span>  

    sudo apt-get install tomcat7-admin      #admin web applications

    sudo apt-get install tomcat7-user         #tools to create user instances  

## <a name="phase-4-configure-tomcat7"></a><span data-ttu-id="65f8b-240">4단계: Tomcat7 구성</span><span class="sxs-lookup"><span data-stu-id="65f8b-240">Phase 4: Configure Tomcat7</span></span>
<span data-ttu-id="65f8b-241">이 단계에서는 Tomcat을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-241">In this phase, you administer Tomcat.</span></span>

### <a name="start-and-stop-tomcat7"></a><span data-ttu-id="65f8b-242">Tomcat7 시작 및 중지</span><span class="sxs-lookup"><span data-stu-id="65f8b-242">Start and stop Tomcat7</span></span>
<span data-ttu-id="65f8b-243">Tomcat7 서버를 설치하면 자동으로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-243">The Tomcat7 server automatically starts when you install it.</span></span> <span data-ttu-id="65f8b-244">또한 다음 명령을 사용하여 시작할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-244">You can also start it with the following command:</span></span>   

    sudo /etc/init.d/tomcat7 start

<span data-ttu-id="65f8b-245">Tomcat7을 중지하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-245">To stop Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 stop

<span data-ttu-id="65f8b-246">Tomcat7의 상태를 보려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-246">To view the status of Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 status

<span data-ttu-id="65f8b-247">Tomcat 서비스를 다시 시작하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-247">To restart Tomcat services:</span></span> 

    sudo /etc/init.d/tomcat7 restart

### <a name="tomcat7-administration"></a><span data-ttu-id="65f8b-248">Tomcat7 관리</span><span class="sxs-lookup"><span data-stu-id="65f8b-248">Tomcat7 administration</span></span>
<span data-ttu-id="65f8b-249">Tomcat 사용자 구성 파일을 편집하여 관리자 자격 증명을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-249">You can edit the Tomcat user configuration file to set up your admin credentials.</span></span> <span data-ttu-id="65f8b-250">다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-250">Use the following command:</span></span>  

    sudo vi  /etc/tomcat7/tomcat-users.xml   

<span data-ttu-id="65f8b-251">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-251">Here is an example:</span></span>  
![sudo vi 명령 출력을 보여 주는 스크린샷][17]  

> [!NOTE]
> <span data-ttu-id="65f8b-253">관리자 사용자 이름에 대한 강력한 암호를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-253">Create a strong password for the admin username.</span></span>  

<span data-ttu-id="65f8b-254">이 파일을 편집한 후 다음 명령으로 Tomcat7 서비스를 다시 시작해야 변경 내용이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-254">After editing this file, you should restart Tomcat7 services with the following command to ensure that the changes take effect:</span></span>  

    sudo /etc/init.d/tomcat7 restart  

<span data-ttu-id="65f8b-255">브라우저를 열고 URL로 **http://<your tomcat server DNS name>/manager/html**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-255">Open your browser, and enter **http://<your tomcat server DNS name>/manager/html** as the URL.</span></span> <span data-ttu-id="65f8b-256">이 문서의 예제에 나와 있는 URL은 http://tomcatexample.cloudapp.net/manager/html입니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-256">For the example in this article, the URL is http://tomcatexample.cloudapp.net/manager/html.</span></span>  

<span data-ttu-id="65f8b-257">연결되면 다음과 유사한 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-257">After connecting, you should see something similar to the following:</span></span>  
![Tomcat 웹 응용 프로그램 관리자의 스크린샷][18]

## <a name="common-issues"></a><span data-ttu-id="65f8b-259">일반적인 문제</span><span class="sxs-lookup"><span data-stu-id="65f8b-259">Common issues</span></span>
### <a name="cant-access-the-virtual-machine-with-tomcat-and-moodle-from-the-internet"></a><span data-ttu-id="65f8b-260">인터넷에서 Tomcat 및 Moodle이 있는 가상 컴퓨터에 액세스할 수 없음</span><span class="sxs-lookup"><span data-stu-id="65f8b-260">Can't access the virtual machine with Tomcat and Moodle from the Internet</span></span>
#### <a name="symptom"></a><span data-ttu-id="65f8b-261">증상</span><span class="sxs-lookup"><span data-stu-id="65f8b-261">Symptom</span></span>  
  <span data-ttu-id="65f8b-262">Tomcat이 실행되고 있지만 브라우저에서 Tomcat 기본 페이지를 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-262">Tomcat is running but you can’t see the Tomcat default page with your browser.</span></span>
#### <a name="possible-root-cause"></a><span data-ttu-id="65f8b-263">가능한 근본 원인</span><span class="sxs-lookup"><span data-stu-id="65f8b-263">Possible root cause</span></span>   

  * <span data-ttu-id="65f8b-264">Tomcat 수신 대기 포트는 Tomcat 트래픽에 대한 가상 컴퓨터 끝점의 개인 포트와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-264">The Tomcat listen port is not the same as the private port of your virtual machine's endpoint for Tomcat traffic.</span></span>  

     <span data-ttu-id="65f8b-265">공용 포트 및 개인 포트 끝점 설정을 확인하고, 개인 포트가 Tomcat 수신 대기 포트와 같은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-265">Check your public port and private port endpoint settings and make sure the private port is the same as the Tomcat listen port.</span></span> <span data-ttu-id="65f8b-266">가상 컴퓨터의 끝점 구성에 대한 지침은 이 문서의 "1단계: 이미지 만들기" 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="65f8b-266">See "Phase 1: Create an image" section of this article for instructions on configuring endpoints for your virtual machine.</span></span>  

     <span data-ttu-id="65f8b-267">Tomcat 수신 대기 포트를 확인하려면 /etc/httpd/conf/httpd.conf(Red Hat 릴리스) 또는 /etc/tomcat7/server.xml(Debian 릴리스)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-267">To determine the Tomcat listen port, open /etc/httpd/conf/httpd.conf (Red Hat release), or /etc/tomcat7/server.xml (Debian release).</span></span> <span data-ttu-id="65f8b-268">기본적으로 Tomcat 수신 대기 포트는 8080입니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-268">By default, the Tomcat listen port is 8080.</span></span> <span data-ttu-id="65f8b-269">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-269">Here is an example:</span></span>  

        <Connector port="8080" protocol="HTTP/1.1"  connectionTimeout="20000"   URIEncoding="UTF-8"            redirectPort="8443" />  

     <span data-ttu-id="65f8b-270">Debian 또는 Ubuntu와 같은 가상 컴퓨터를 사용하는 경우 Tomcat 수신 대기 기본 포트(예: 8081)를 변경하려면 해당 운영 체제의 포트도 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-270">If you are using a virtual machine like Debian or Ubuntu and you want to change the default port of Tomcat Listen (for example 8081), you should also open the port for the operating system.</span></span> <span data-ttu-id="65f8b-271">먼저 프로필을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-271">First, open the profile:</span></span>  

        sudo vi /etc/default/tomcat7  

     <span data-ttu-id="65f8b-272">그런 다음 마지막 줄에 주석 처리를 제거하고 "아니요"를 "예"로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-272">Then uncomment the last line and change “no” to “yes”.</span></span>  

        AUTHBIND=yes
  2. <span data-ttu-id="65f8b-273">방화벽에서 Tomcat 수신 대기 포트를 사용하지 않도록 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-273">The firewall has disabled the listen port of Tomcat.</span></span>

     <span data-ttu-id="65f8b-274">로컬 호스트에서만 Tomcat 기본 페이지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-274">You can only see the Tomcat default page from the local host.</span></span> <span data-ttu-id="65f8b-275">문제는 주로 Tomcat에서 수신 대기하는 포트가 방화벽으로 차단되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-275">The problem is most likely that the port, which is listened to by Tomcat, is blocked by the firewall.</span></span> <span data-ttu-id="65f8b-276">w3m 도구를 사용하여 웹 페이지를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-276">You can use the w3m tool to browse the webpage.</span></span> <span data-ttu-id="65f8b-277">다음 명령은 w3m을 설치하고 Tomcat 기본 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-277">The following commands install w3m and browse to the Tomcat default page:</span></span>  


        <span data-ttu-id="65f8b-278">sudo yum  install w3m w3m-img</span><span class="sxs-lookup"><span data-stu-id="65f8b-278">sudo yum  install w3m w3m-img</span></span>


        <span data-ttu-id="65f8b-279">w3m http://localhost:8080</span><span class="sxs-lookup"><span data-stu-id="65f8b-279">w3m http://localhost:8080</span></span>  
#### <a name="solution"></a><span data-ttu-id="65f8b-280">해결 방법</span><span class="sxs-lookup"><span data-stu-id="65f8b-280">Solution</span></span>

  * <span data-ttu-id="65f8b-281">Tomcat 수신 대기 포트가 가상 컴퓨터의 트래픽에 대한 끝점의 개인 포트와 다른 경우 개인 포트를 Tomcat 수신 대기 포트와 동일하게 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-281">If the Tomcat listen port is not the same as the private port of the endpoint for traffic to the virtual machine, you need change the private port to be the same as the Tomcat listen port.</span></span>   
  2. <span data-ttu-id="65f8b-282">방화벽/iptables로 인해 문제가 발생하면 /etc/sysconfig/iptables에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-282">If the issue is caused by firewall/iptables, add the following lines to /etc/sysconfig/iptables.</span></span> <span data-ttu-id="65f8b-283">두 번째 줄은 https 트래픽에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-283">The second line is only needed for https traffic:</span></span>  

      <span data-ttu-id="65f8b-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span><span class="sxs-lookup"><span data-stu-id="65f8b-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span></span>

      <span data-ttu-id="65f8b-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span><span class="sxs-lookup"><span data-stu-id="65f8b-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span></span>  

     > [!IMPORTANT]
     > <span data-ttu-id="65f8b-286">위의 줄은 -A INPUT -j REJECT --reject-with icmp-host-prohibited와 같이 액세스를 전역적으로 제한하는 줄 위에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-286">Make sure the previous lines are positioned above any lines that would globally restrict access, such as the following: -A INPUT -j REJECT --reject-with icmp-host-prohibited</span></span>



<span data-ttu-id="65f8b-287">iptables를 다시 로드하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-287">To reload the iptables, run the following command:</span></span>

    service iptables restart

<span data-ttu-id="65f8b-288">CentOS 6.3에서 테스트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-288">This has been tested on CentOS 6.3.</span></span>

### <a name="permission-denied-when-you-upload-project-files-to-varlibtomcat7webapps"></a><span data-ttu-id="65f8b-289">/var/lib/tomcat7/webapps/에 프로젝트 파일을 업로드할 때 권한이 거부됨</span><span class="sxs-lookup"><span data-stu-id="65f8b-289">Permission denied when you upload project files to /var/lib/tomcat7/webapps/</span></span>
#### <a name="symptom"></a><span data-ttu-id="65f8b-290">증상</span><span class="sxs-lookup"><span data-stu-id="65f8b-290">Symptom</span></span>
  <span data-ttu-id="65f8b-291">SFTP 클라이언트(예: FileZilla)를 사용하여 가상 컴퓨터에 연결하고 /var/lib/tomcat7/webapps/로 이동하여 사이트를 게시하면 다음과 비슷한 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-291">When you use an SFTP client (such as FileZilla) to connect to your virtual machine and navigate to /var/lib/tomcat7/webapps/ to publish your site, you get an error message similar to the following:</span></span>  

     status:    Listing directory /var/lib/tomcat7/webapps
     Command:    put "C:\Users\liang\Desktop\info.jsp" "info.jsp"
     Error:    /var/lib/tomcat7/webapps/info.jsp: open for write: permission denied
     Error:    File transfer failed
#### <a name="possible-root-cause"></a><span data-ttu-id="65f8b-292">가능한 근본 원인</span><span class="sxs-lookup"><span data-stu-id="65f8b-292">Possible root cause</span></span>
  <span data-ttu-id="65f8b-293">/var/lib/tomcat7/webapps 폴더에 액세스할 수 있는 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-293">You have no permissions to access the /var/lib/tomcat7/webapps folder.</span></span>  
#### <a name="solution"></a><span data-ttu-id="65f8b-294">해결 방법</span><span class="sxs-lookup"><span data-stu-id="65f8b-294">Solution</span></span>  
  <span data-ttu-id="65f8b-295">루트 계정에서 권한을 부여받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-295">You need to get permission from the root account.</span></span> <span data-ttu-id="65f8b-296">해당 폴더의 소유권을 루트에서 컴퓨터를 프로비전할 때 사용한 사용자 이름으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-296">You can change the ownership of that folder from root to the username you used when you provisioned the machine.</span></span> <span data-ttu-id="65f8b-297">다음은 azureuser 계정 이름을 사용한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-297">Here is an example with the azureuser account name:</span></span>  

     sudo chown azureuser -R /var/lib/tomcat7/webapps

  <span data-ttu-id="65f8b-298">-R 옵션을 사용하여 디렉터리 내의 모든 파일에 대해서도 권한을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-298">Use the -R option to apply the permissions for all files inside of a directory too.</span></span>  

  <span data-ttu-id="65f8b-299">이 명령은 디렉터리에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-299">This command also works for directories.</span></span> <span data-ttu-id="65f8b-300">-R 옵션은 디렉터리 내의 모든 파일과 디렉터리에 대한 권한을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-300">The -R option changes the permissions for all files and directories inside the directory.</span></span> <span data-ttu-id="65f8b-301">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-301">Here is an example:</span></span>  

     sudo chown -R username:group directory  

  <span data-ttu-id="65f8b-302">이 명령은 디렉터리 내에 있는 모든 파일과 디렉터리에 대한 소유권(사용자 및 그룹 둘 다)을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-302">This command changes ownership (both user and group) for all files and directories that are inside the directory.</span></span>  

  <span data-ttu-id="65f8b-303">다음 명령은 폴더 디렉터리의 권한만 변경하며,</span><span class="sxs-lookup"><span data-stu-id="65f8b-303">The following command only changes the permission of the folder directory.</span></span> <span data-ttu-id="65f8b-304">디렉터리 내의 파일과 폴더는 변경하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="65f8b-304">The files and folders inside the directory are not changed.</span></span>  

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
