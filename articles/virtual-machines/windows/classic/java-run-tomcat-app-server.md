---
title: "클래식 Azure VM에서 Java 응용 프로그램 서버 실행 | Microsoft Docs"
description: "이 자습서에서는 클래식 배포 모델을 사용하여 만든 리소스를 사용하며, Windows 가상 컴퓨터를 만들고 Apache Tomcat 응용 프로그램 서버를 실행하도록 구성하는 방법을 보여 줍니다."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d627aa09-f7d6-4239-8110-f8fc5111b939
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 03/16/2017
ms.author: robmcm
ms.openlocfilehash: 6e02f42613808bcb13c0057e9f8fcc1c02273e77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-run-a-java-application-server-on-a-virtual-machine-created-with-the-classic-deployment-model"></a><span data-ttu-id="39de0-103">클래식 배포 모델을 사용하여 만든 가상 컴퓨터에서 Java 응용 프로그램 서버를 실행하는 방법</span><span class="sxs-lookup"><span data-stu-id="39de0-103">How to run a Java application server on a virtual machine created with the classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="39de0-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="39de0-105">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="39de0-106">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="39de0-107">Java 8 및 Tomcat에서 웹앱을 배포하는 Resource Manager 템플릿은 [여기](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39de0-107">For a Resource Manager template to deploy a webapp with Java 8 and Tomcat, see [here](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).</span></span>

<span data-ttu-id="39de0-108">Azure에서 가상 컴퓨터를 사용하여 서버 기능을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-108">With Azure, you can use a virtual machine to provide server capabilities.</span></span> <span data-ttu-id="39de0-109">한 예로, Java 응용 프로그램 서버(예: Apache Tomcat)를 호스트하도록 Azure에서 실행되는 가상 컴퓨터를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-109">As an example, a virtual machine running on Azure can be configured to host a Java application server, such as Apache Tomcat.</span></span>

<span data-ttu-id="39de0-110">이 가이드를 완료하면 Azure에서 실행되는 가상 컴퓨터를 만들고 Java 응용 프로그램 서버에서 실행하도록 구성하는 방법을 이해할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-110">After completing this guide, you will have an understanding of how to create a virtual machine running on Azure and configure it to run a Java application server.</span></span> <span data-ttu-id="39de0-111">다음 작업을 배우고 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-111">You will learn and perform the following tasks:</span></span>

* <span data-ttu-id="39de0-112">Java 개발 키트(JDK)가 이미 설치된 가상 컴퓨터를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="39de0-112">How to create a virtual machine that has a Java Development Kit (JDK) already installed.</span></span>
* <span data-ttu-id="39de0-113">가상 컴퓨터에 원격으로 로그인하는 방법</span><span class="sxs-lookup"><span data-stu-id="39de0-113">How to remotely sign in to your virtual machine.</span></span>
* <span data-ttu-id="39de0-114">가상 컴퓨터에 Java 응용 프로그램 서버(Apache Tomcat)를 설치하는 방법</span><span class="sxs-lookup"><span data-stu-id="39de0-114">How to install a Java application server--Apache Tomcat--on your virtual machine.</span></span>
* <span data-ttu-id="39de0-115">가상 컴퓨터의 끝점을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="39de0-115">How to create an endpoint for your virtual machine.</span></span>
* <span data-ttu-id="39de0-116">방화벽에서 응용 프로그램 서버용 포트를 여는 방법</span><span class="sxs-lookup"><span data-stu-id="39de0-116">How to open a port in the firewall for your application server.</span></span>

<span data-ttu-id="39de0-117">설치를 완료하면 Tomcat이 가상 컴퓨터에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-117">The completed installation results in Tomcat running on a virtual machine.</span></span>

![Apache Tomcat을 실행하는 가상 컴퓨터][virtual_machine_tomcat]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="to-create-a-virtual-machine"></a><span data-ttu-id="39de0-119">가상 컴퓨터를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="39de0-119">To create a virtual machine</span></span>
1. <span data-ttu-id="39de0-120">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-120">Sign in to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="39de0-121">**새로 만들기**, **계산**을 차례로 클릭한 다음 **추천 앱**에서 **모두 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-121">Click **New**, click **Compute**, then click **See all** in the **Featured apps**.</span></span>
3. <span data-ttu-id="39de0-122">**JDK**를 클릭한 다음 **JDK** 창에서 **JDK 8**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-122">Click **JDK**, click **JDK 8** in the **JDK** pane.</span></span>  
   <span data-ttu-id="39de0-123">JDK 8에서 실행할 준비가 되지 않은 레거시 응용 프로그램이 있는 경우 **JDK 6** 및 **JDK 7**을 지원하는 가상 컴퓨터 이미지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-123">Virtual machine images that support **JDK 6** and **JDK 7** are available if you have legacy applications that are not ready to run in JDK 8.</span></span>
4. <span data-ttu-id="39de0-124">JDK 8 창에서 **클래식**을 선택한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-124">In the JDK 8 pane, select **Classic**, then click **Create**.</span></span>
5. <span data-ttu-id="39de0-125">**기본 사항** 블레이드에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-125">In the **Basics** blade:</span></span>
   1. <span data-ttu-id="39de0-126">가상 컴퓨터의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-126">Specify a name for the virtual machine.</span></span>
   2. <span data-ttu-id="39de0-127">**사용자 이름** 필드에 관리자의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-127">Enter a name for the administrator in the **User Name** field.</span></span> <span data-ttu-id="39de0-128">이 이름과 다음 필드에 있는 연결된 암호를 기억해 두세요.</span><span class="sxs-lookup"><span data-stu-id="39de0-128">Remember this name and the associated password that follows in the next field.</span></span> <span data-ttu-id="39de0-129">가상 컴퓨터에 원격으로 로그인할 때 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-129">You need them when you remotely sign in to the virtual machine.</span></span>
   3. <span data-ttu-id="39de0-130">**새 암호** 필드에 암호를 입력하고 **암호 확인** 필드에 다시 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-130">Enter a password in the **New password** field, and reenter it in the **Confirm password** field.</span></span> <span data-ttu-id="39de0-131">이 암호는 관리자 계정 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-131">This password is for the Administrator account.</span></span>
   4. <span data-ttu-id="39de0-132">적합한 **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-132">Select the appropriate **Subscription**.</span></span>
   5. <span data-ttu-id="39de0-133">**리소스 그룹**에 대해 **새로 만들기**를 클릭하고 새 리소스 그룹의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-133">For the **Resource group**, click **Create new** and enter the name of a new resource group.</span></span> <span data-ttu-id="39de0-134">또는 **기존 항목 사용**을 클릭하고 사용 가능한 리소스 그룹 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-134">Or, click **Use existing** and select one of the available resource groups.</span></span>
   6. <span data-ttu-id="39de0-135">가상 컴퓨터가 있는 위치(예: **미국 중남부**)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-135">Select a location where the virtual machine resides, such as **South Central US**.</span></span>
6. <span data-ttu-id="39de0-136">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-136">Click **Next**.</span></span>
7. <span data-ttu-id="39de0-137">**가상 컴퓨터 이미지 크기** 블레이드에서 **A1 표준** 또는 적절한 다른 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-137">In the **Virtual machine image size** blade, select **A1 Standard** or another appropriate image.</span></span>
8. <span data-ttu-id="39de0-138">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-138">Click **Select**.</span></span>

9. <span data-ttu-id="39de0-139">**설정** 블레이드에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-139">In the **Settings** blade, click **OK**.</span></span> <span data-ttu-id="39de0-140">Azure에서 제공하는 기본값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-140">You can use the default values provided by Azure.</span></span>  
10. <span data-ttu-id="39de0-141">**요약** 블레이드에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-141">In the **Summary** blade, click **OK**.</span></span>

## <a name="to-remotely-sign-in-to-your-virtual-machine"></a><span data-ttu-id="39de0-142">가상 컴퓨터에 원격으로 로그인하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-142">To remotely sign in to your virtual machine</span></span>
1. <span data-ttu-id="39de0-143">[Azure 포털](https://portal.azure.com)에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-143">Log on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="39de0-144">**가상 컴퓨터(클래식)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-144">Click **Virtual machines (classic)**.</span></span> <span data-ttu-id="39de0-145">필요한 경우 서비스 범주 아래의 왼쪽 하단에 있는 **추가 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-145">If needed, click **More services** at the bottom left corner under the service categories.</span></span> <span data-ttu-id="39de0-146">**가상 컴퓨터(클래식)** 항목이 **계산** 그룹에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-146">The **Virtual machines (classic)** entry is listed in the **Compute** group.</span></span>
3. <span data-ttu-id="39de0-147">로그인할 가상 컴퓨터의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-147">Click the name of the virtual machine that you want to sign in to.</span></span>
4. <span data-ttu-id="39de0-148">가상 컴퓨터가 시작되면 창 위쪽의 메뉴를 통해 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-148">After the virtual machine has started, a menu at the top of the pane allows connections.</span></span>
5. <span data-ttu-id="39de0-149">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-149">Click **Connect**.</span></span>
6. <span data-ttu-id="39de0-150">가상 컴퓨터에 연결해야 한다는 메시지에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-150">Respond to the prompts as needed to connect to the virtual machine.</span></span> <span data-ttu-id="39de0-151">일반적으로 연결 세부 정보가 포함된 .rdp 파일을 열거나 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-151">Typically, you save or open the .rdp file that contains the connection details.</span></span> <span data-ttu-id="39de0-152">.rdp 파일의 첫 줄 끝 부분으로 url:port를 복사한 다음 원격 로그인 응용 프로그램에 붙여 넣어야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-152">You might have to copy the url:port as the last part of the first line of the .rdp file and paste it in a remote sign-in application.</span></span>

## <a name="to-install-a-java-application-server-on-your-virtual-machine"></a><span data-ttu-id="39de0-153">가상 컴퓨터에 Java 응용 프로그램 서버를 설치하는 방법</span><span class="sxs-lookup"><span data-stu-id="39de0-153">To install a Java application server on your virtual machine</span></span>
<span data-ttu-id="39de0-154">Java 응용 프로그램 서버를 가상 컴퓨터로 복사하거나 설치 관리자를 통해 Java 응용 프로그램 서버를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-154">You can copy a Java application server to your virtual machine, or you can install a Java application server through an installer.</span></span>

<span data-ttu-id="39de0-155">이 자습서에서는 설치할 Java 응용 프로그램 서버로 Tomcat을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-155">This tutorial uses Tomcat as the Java application server to install.</span></span>

1. <span data-ttu-id="39de0-156">가상 컴퓨터에 로그인하는 경우 [Apache Tomcat](http://tomcat.apache.org/download-80.cgi)에 대한 브라우저 세션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-156">When you are signed in to your virtual machine, open a browser session to [Apache Tomcat](http://tomcat.apache.org/download-80.cgi).</span></span>
2. <span data-ttu-id="39de0-157">**32-bit/64-bit Windows Service Installer**링크를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-157">Double-click the link for **32-bit/64-bit Windows Service Installer**.</span></span> <span data-ttu-id="39de0-158">이 기술을 사용하면 Tomcat이 Windows 서비스로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-158">By using this technique, Tomcat installs as a Windows service.</span></span>
3. <span data-ttu-id="39de0-159">메시지가 표시되면 설치 관리자를 실행하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-159">When prompted, choose to run the installer.</span></span>
4. <span data-ttu-id="39de0-160">**Apache Tomcat Setup** 마법사에서 프롬프트에 따라 Tomcat을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-160">Within the **Apache Tomcat Setup** wizard, follow the prompts to install Tomcat.</span></span> <span data-ttu-id="39de0-161">이 자습서에서는 기본값을 그대로 사용해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-161">For the purposes of this tutorial, accepting the defaults is fine.</span></span> <span data-ttu-id="39de0-162">**Apache Tomcat 설정 마법사 완료** 대화 상자가 표시되면 옵션으로 제공되는 **Apache Tomcat 실행**을 선택하여 Tomcat을 바로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-162">When you reach the **Completing the Apache Tomcat Setup Wizard** dialog box, you can optionally check **Run Apache Tomcat** to have Tomcat start now.</span></span> <span data-ttu-id="39de0-163">**Finish** 를 클릭하여 Tomcat 설치 프로세스를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-163">Click **Finish** to complete the Tomcat setup process.</span></span>

## <a name="to-start-tomcat"></a><span data-ttu-id="39de0-164">Tomcat 시작 방법</span><span class="sxs-lookup"><span data-stu-id="39de0-164">To start Tomcat</span></span>

<span data-ttu-id="39de0-165">가상 컴퓨터에서 명령 프롬프트를 열고 **net&nbsp;start&nbsp;Tomcat8** 명령을 실행하여 Tomcat을 수동으로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-165">You can manually start Tomcat by opening a command prompt on your virtual machine and running the command **net&nbsp;start&nbsp;Tomcat8**.</span></span>

<span data-ttu-id="39de0-166">Tomcat이 실행되면 가상 컴퓨터의 브라우저에서 URL <http://localhost:8080/>을 입력하여 Tomcat에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-166">Once Tomcat is running, you can access Tomcat by entering the URL <http://localhost:8080> in the virtual machine's browser.</span></span>

<span data-ttu-id="39de0-167">Tomcat이 외부 컴퓨터에서 실행되는 것을 보려면 끝점을 만들고 포트를 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-167">To see Tomcat running from external machines, you need to create an endpoint and open a port.</span></span>

## <a name="to-create-an-endpoint-for-your-virtual-machine"></a><span data-ttu-id="39de0-168">가상 컴퓨터의 끝점을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="39de0-168">To create an endpoint for your virtual machine</span></span>
1. <span data-ttu-id="39de0-169">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-169">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="39de0-170">**가상 컴퓨터(클래식)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-170">Click **Virtual machines (classic)**.</span></span>
3. <span data-ttu-id="39de0-171">Java 응용 프로그램 서버를 실행하는 가상 컴퓨터의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-171">Click the name of the virtual machine that is running your Java application server.</span></span>
4. <span data-ttu-id="39de0-172">**끝점**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-172">Click **Endpoints**.</span></span>
5. <span data-ttu-id="39de0-173">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-173">Click **Add**.</span></span>
6. <span data-ttu-id="39de0-174">**끝점 추가** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-174">In the **Add endpoint** dialog box:</span></span>
   1. <span data-ttu-id="39de0-175">끝점의 이름(예: **HttpIn**)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-175">Specify a name for the endpoint; for example, **HttpIn**.</span></span>
   2. <span data-ttu-id="39de0-176">프로토콜에서 **TCP**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-176">Select **TCP** for the protocol.</span></span>
   3. <span data-ttu-id="39de0-177">공용 포트에서 **80** 을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-177">Specify **80** for the public port.</span></span>
   4. <span data-ttu-id="39de0-178">개인 포트에서 **8080** 을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-178">Specify **8080** for the private port.</span></span>
   5. <span data-ttu-id="39de0-179">부동 IP 주소에서 **사용 안 함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-179">Select **Disabled** for the floating IP address.</span></span>
   6. <span data-ttu-id="39de0-180">액세스 제어 목록을 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-180">Leave the access control list as is.</span></span>
   7. <span data-ttu-id="39de0-181">**확인** 단추를 클릭하여 대화 상자를 닫고 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-181">Click the **OK** button to close the dialog box and create the endpoint.</span></span>

## <a name="to-open-a-port-in-the-firewall-for-your-virtual-machine"></a><span data-ttu-id="39de0-182">가상 컴퓨터의 방화벽에서 포트를 여는 방법</span><span class="sxs-lookup"><span data-stu-id="39de0-182">To open a port in the firewall for your virtual machine</span></span>
1. <span data-ttu-id="39de0-183">가상 컴퓨터에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-183">Sign in to your virtual machine.</span></span>
2. <span data-ttu-id="39de0-184">**Windows 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-184">Click **Windows Start**.</span></span>
3. <span data-ttu-id="39de0-185">**제어판**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-185">Click **Control Panel**.</span></span>
4. <span data-ttu-id="39de0-186">**시스템 및 보안**, **Windows 방화벽**, **고급 설정**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-186">Click **System and Security**, click **Windows Firewall**, and then click **Advanced Settings**.</span></span>
5. <span data-ttu-id="39de0-187">**인바운드 규칙**을 선택하고 **새 규칙**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-187">Click **Inbound Rules**, and then click **New Rule**.</span></span>  
   <span data-ttu-id="39de0-188">![새 인바운드 규칙][NewIBRule]</span><span class="sxs-lookup"><span data-stu-id="39de0-188">![New inbound rule][NewIBRule]</span></span>
6. <span data-ttu-id="39de0-189">**규칙 유형**에 대해 **포트**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-189">For the **Rule Type**, select **Port**, and then click **Next**.</span></span>  
   <span data-ttu-id="39de0-190">![새 인바운드 규칙 포트][NewRulePort]</span><span class="sxs-lookup"><span data-stu-id="39de0-190">![New inbound rule port][NewRulePort]</span></span>
7. <span data-ttu-id="39de0-191">**프로토콜 및 포트** 화면에서 **TCP**를 선택하고 **8080**을 **특정 로컬 포트**로 지정한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-191">On the **Protocol and Ports** screen, select **TCP**, specify **8080** as the **Specific local port**, and then click **Next**.</span></span>  
  <span data-ttu-id="39de0-192">![새 인바운드 규칙][NewRuleProtocol]</span><span class="sxs-lookup"><span data-stu-id="39de0-192">![New inbound rule ][NewRuleProtocol]</span></span>
8. <span data-ttu-id="39de0-193">**작업** 화면에서 **연결 허용**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-193">On the **Action** screen, select **Allow the connection**, and then click **Next**.</span></span>
   <span data-ttu-id="39de0-194">![새 인바운드 규칙 동작][NewRuleAction]</span><span class="sxs-lookup"><span data-stu-id="39de0-194">![New inbound rule action][NewRuleAction]</span></span>
9. <span data-ttu-id="39de0-195">**프로필** 화면에서 **도메인**, **개인** 및 **공용**이 선택되었는지 확인하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-195">On the **Profile** screen, ensure that **Domain**, **Private**, and **Public** are selected, and then click **Next**.</span></span>
   <span data-ttu-id="39de0-196">![새 인바운드 규칙 프로필][NewRuleProfile]</span><span class="sxs-lookup"><span data-stu-id="39de0-196">![New inbound rule profile][NewRuleProfile]</span></span>
10. <span data-ttu-id="39de0-197">**이름** 화면에서 규칙 이름(예: **HttpIn**)(규칙 이름은 끝점 이름과 일치하지 않아도 됨)을 지정하고 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-197">On the **Name** screen, specify a name for the rule, such as **HttpIn** (the rule name is not required to match the endpoint name, however), and then click **Finish**.</span></span>  
    <span data-ttu-id="39de0-198">![새 인바운드 규칙 이름][NewRuleName]</span><span class="sxs-lookup"><span data-stu-id="39de0-198">![New inbound rule name][NewRuleName]</span></span>

<span data-ttu-id="39de0-199">이제 외부 브라우저에서 Tomcat 웹 사이트를 볼 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-199">At this point, your Tomcat website should be viewable from an external browser.</span></span> <span data-ttu-id="39de0-200">브라우저의 주소 창에서 폼의 URL을 입력  **http://*프로그램\_DNS\_이름*. cloudapp.net**, 여기서 ***프로그램\_DNS\_이름*** 가상 컴퓨터를 만들 때 지정 된 DNS 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-200">In the browser's address window, type a URL of the form **http://*your\_DNS\_name*.cloudapp.net**, where ***your\_DNS\_name*** is the DNS name you specified when you created the virtual machine.</span></span>

## <a name="application-lifecycle-considerations"></a><span data-ttu-id="39de0-201">응용 프로그램 수명 주기 고려 사항</span><span class="sxs-lookup"><span data-stu-id="39de0-201">Application lifecycle considerations</span></span>
* <span data-ttu-id="39de0-202">사용자 고유의 WAR(웹 응용 프로그램 보관)을 만들어 **webapps** 폴더에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-202">You could create your own web application archive (WAR) and add it to the **webapps** folder.</span></span> <span data-ttu-id="39de0-203">예를 들어 기본 JSP(Java 서비스 페이지) 동적 웹 프로젝트를 만들어 WAR 파일로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-203">For example, create a basic Java Service Page (JSP) dynamic web project and export it as a WAR file.</span></span> <span data-ttu-id="39de0-204">다음으로, 이 WAR을 가상 컴퓨터의 Apache Tomcat **webapps** 폴더에 복사한 후 브라우저에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-204">Next, copy the WAR to the Apache Tomcat **webapps** folder on the virtual machine, then run it in a browser.</span></span>
* <span data-ttu-id="39de0-205">기본적으로 Tomcat 서비스가 설치될 때 수동으로 시작되도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-205">By default when the Tomcat service is installed, it is set to start manually.</span></span> <span data-ttu-id="39de0-206">서비스 스냅인을 사용하여 자동으로 시작되도록 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-206">You can switch it to start automatically by using the Services snap-in.</span></span> <span data-ttu-id="39de0-207">**Windows 시작**, **관리 도구**, **서비스**를 차례로 클릭하여 서비스 스냅인을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-207">Start the Services snap-in by clicking **Windows Start**, **Administrative Tools**, and then **Services**.</span></span> <span data-ttu-id="39de0-208">**Apache Tomcat** 서비스를 두 번 클릭하고 **시작 유형**을 **자동**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-208">Double-click the **Apache Tomcat** service and set **Startup type** to **Automatic**.</span></span>

    ![서비스가 자동으로 시작되도록 설정][service_automatic_startup]

    <span data-ttu-id="39de0-210">Tomcat이 자동으로 시작되도록 설정할 경우의 이점은 가상 컴퓨터가 다시 부팅되면(예를 들어 재부팅이 필요한 소프트웨어 업데이트가 설치된 후) Tomcat이 실행되기 시작된다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-210">The benefit of having Tomcat start automatically is that it starts running when the virtual machine is rebooted (for example, after software updates that require a reboot are installed).</span></span>

## <a name="next-steps"></a><span data-ttu-id="39de0-211">다음 단계</span><span class="sxs-lookup"><span data-stu-id="39de0-211">Next steps</span></span>
<span data-ttu-id="39de0-212">Azure Storage, Service Bus, SQL Database 등 Java 응용 프로그램에 포함할 기타 서비스에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39de0-212">You can learn about other services (such as Azure Storage, service bus, and SQL Database) that you may want to include with your Java applications.</span></span> <span data-ttu-id="39de0-213">[Java 개발자 센터](https://azure.microsoft.com/develop/java/)에서 제공되는 정보를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="39de0-213">View the information available at the [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[virtual_machine_tomcat]:media/java-run-tomcat-app-server/WA_VirtualMachineRunningApacheTomcat.png

[service_automatic_startup]:media/java-run-tomcat-app-server/WA_TomcatServiceAutomaticStart.png









[NewIBRule]:media/java-run-tomcat-app-server/NewInboundRule.png
[NewRulePort]:media/java-run-tomcat-app-server/NewRulePort.png
[NewRuleProtocol]:media/java-run-tomcat-app-server/NewRuleProtocol.png
[NewRuleAction]:media/java-run-tomcat-app-server/NewRuleAction.png
[NewRuleName]:media/java-run-tomcat-app-server/NewRuleName.png
[NewRuleProfile]:media/java-run-tomcat-app-server/NewRuleProfile.png


<!-- Deleted from the "To create an ednpoint for your virtual mache" 3/17/2017,
     to use the new portal.
6. In the **Add endpoint** dialog box, ensure **Add standalone endpoint** is selected, and then click **Next**.
7. In the **New endpoint details** dialog box:
-->
