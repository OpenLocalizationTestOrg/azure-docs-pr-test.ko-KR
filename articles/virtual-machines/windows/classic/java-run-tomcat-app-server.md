---
title: "클래식 Azure VM에서 aaaRun Java 응용 프로그램 서버 | Microsoft Docs"
description: "이 자습서에서는 어떻게 hello 클래식 배포 모델 및 표시를 사용 하 여 만든 리소스 toocreate Windows 가상 컴퓨터 및 toorun Apache Tomcat 응용 프로그램 서버를 구성 합니다."
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
ms.openlocfilehash: 2d9f586c9f628d3738522b320996b95b078d7454
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-java-application-server-on-a-virtual-machine-created-with-hello-classic-deployment-model"></a><span data-ttu-id="750b2-103">어떻게 toorun 가상 컴퓨터에서 Java 응용 프로그램 서버는 hello 클래식 배포 모델을 사용 하 여을 만든</span><span class="sxs-lookup"><span data-stu-id="750b2-103">How toorun a Java application server on a virtual machine created with hello classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="750b2-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="750b2-105">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="750b2-106">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="750b2-107">리소스 관리자 템플릿 toodeploy Tomcat 8 Java와 webapp 참조 [여기](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/)합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-107">For a Resource Manager template toodeploy a webapp with Java 8 and Tomcat, see [here](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).</span></span>

<span data-ttu-id="750b2-108">Azure 가상 컴퓨터 tooprovide 서버 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-108">With Azure, you can use a virtual machine tooprovide server capabilities.</span></span> <span data-ttu-id="750b2-109">예를 들어 Azure에서 실행 되는 가상 컴퓨터에 구성 된 toohost Apache Tomcat 같은 Java 응용 프로그램 서버 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-109">As an example, a virtual machine running on Azure can be configured toohost a Java application server, such as Apache Tomcat.</span></span>

<span data-ttu-id="750b2-110">이 가이드를 완료 한 후는 방법 이해 해야 합니다 toocreate 가상 컴퓨터를 Azure에서 실행 되 고 toorun Java 응용 프로그램 서버를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-110">After completing this guide, you will have an understanding of how toocreate a virtual machine running on Azure and configure it toorun a Java application server.</span></span> <span data-ttu-id="750b2-111">자세한 되며 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-111">You will learn and perform hello following tasks:</span></span>

* <span data-ttu-id="750b2-112">Java 개발 키트 (JDK) 이미 설치 되어에 어떻게 toocreate 가상 된 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-112">How toocreate a virtual machine that has a Java Development Kit (JDK) already installed.</span></span>
* <span data-ttu-id="750b2-113">어떻게 tooremotely tooyour 가상 컴퓨터에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-113">How tooremotely sign in tooyour virtual machine.</span></span>
* <span data-ttu-id="750b2-114">어떻게 tooinstall는 Java 응용 프로그램 서버--Apache Tomcat-가상 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-114">How tooinstall a Java application server--Apache Tomcat--on your virtual machine.</span></span>
* <span data-ttu-id="750b2-115">어떻게 toocreate 가상 컴퓨터에 대 한 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-115">How toocreate an endpoint for your virtual machine.</span></span>
* <span data-ttu-id="750b2-116">어떻게 tooopen 포트 hello에 응용 프로그램 서버에 대 한 방화벽입니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-116">How tooopen a port in hello firewall for your application server.</span></span>

<span data-ttu-id="750b2-117">hello 가상 컴퓨터에서 실행 되는 Tomcat에서 설치 결과 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-117">hello completed installation results in Tomcat running on a virtual machine.</span></span>

![Apache Tomcat을 실행하는 가상 컴퓨터][virtual_machine_tomcat]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a><span data-ttu-id="750b2-119">toocreate 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="750b2-119">toocreate a virtual machine</span></span>
1. <span data-ttu-id="750b2-120">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="750b2-121">클릭 **새로**, 클릭 **계산**, 클릭 **스크롤하게** hello에 **추천 앱**합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-121">Click **New**, click **Compute**, then click **See all** in hello **Featured apps**.</span></span>
3. <span data-ttu-id="750b2-122">클릭 **JDK**, 클릭 **JDK 8** hello에 **JDK** 창.</span><span class="sxs-lookup"><span data-stu-id="750b2-122">Click **JDK**, click **JDK 8** in hello **JDK** pane.</span></span>  
   <span data-ttu-id="750b2-123">가상 컴퓨터 이미지를 지 원하는 **JDK 6** 및 **JDK 7** JDK 8에서 준비 toorun 되지 않는 레거시 응용 프로그램의 경우에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-123">Virtual machine images that support **JDK 6** and **JDK 7** are available if you have legacy applications that are not ready toorun in JDK 8.</span></span>
4. <span data-ttu-id="750b2-124">JDK 8 hello 창에서 선택 **클래식**, 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-124">In hello JDK 8 pane, select **Classic**, then click **Create**.</span></span>
5. <span data-ttu-id="750b2-125">Hello에 **기본 사항** 블레이드:</span><span class="sxs-lookup"><span data-stu-id="750b2-125">In hello **Basics** blade:</span></span>
   1. <span data-ttu-id="750b2-126">Hello 가상 컴퓨터에 대 한 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-126">Specify a name for hello virtual machine.</span></span>
   2. <span data-ttu-id="750b2-127">Hello에 hello 관리자에 대 한 이름을 입력 **사용자 이름** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-127">Enter a name for hello administrator in hello **User Name** field.</span></span> <span data-ttu-id="750b2-128">이 이름은 기억 하 고 hello hello 다음 필드에 연결 된 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-128">Remember this name and hello associated password that follows in hello next field.</span></span> <span data-ttu-id="750b2-129">필요할 때 toohello 가상 컴퓨터를 원격으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-129">You need them when you remotely sign in toohello virtual machine.</span></span>
   3. <span data-ttu-id="750b2-130">Hello에 암호를 입력 **새 암호** hello에 다시 입력 하 고 필드 **암호 확인** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-130">Enter a password in hello **New password** field, and reenter it in hello **Confirm password** field.</span></span> <span data-ttu-id="750b2-131">이 암호는 hello 관리자 계정에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-131">This password is for hello Administrator account.</span></span>
   4. <span data-ttu-id="750b2-132">적절 한 선택 hello **구독**합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-132">Select hello appropriate **Subscription**.</span></span>
   5. <span data-ttu-id="750b2-133">Hello에 대 한 **리소스 그룹**, 클릭 **새로 만들기** 새 리소스 그룹의 hello 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-133">For hello **Resource group**, click **Create new** and enter hello name of a new resource group.</span></span> <span data-ttu-id="750b2-134">클릭 또는 **기존 항목 사용** hello 사용 가능한 리소스 그룹 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-134">Or, click **Use existing** and select one of hello available resource groups.</span></span>
   6. <span data-ttu-id="750b2-135">위치와 같은 hello 가상 컴퓨터가 있는 위치를 선택 **미국 중남부**합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-135">Select a location where hello virtual machine resides, such as **South Central US**.</span></span>
6. <span data-ttu-id="750b2-136">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-136">Click **Next**.</span></span>
7. <span data-ttu-id="750b2-137">Hello에 **가상 컴퓨터 이미지 크기** 블레이드를 **표준 A1** 또는 다른 적절 한 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-137">In hello **Virtual machine image size** blade, select **A1 Standard** or another appropriate image.</span></span>
8. <span data-ttu-id="750b2-138">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-138">Click **Select**.</span></span>

9. <span data-ttu-id="750b2-139">Hello에 **설정** 블레이드에서 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-139">In hello **Settings** blade, click **OK**.</span></span> <span data-ttu-id="750b2-140">Azure에서 제공 하는 hello 기본 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-140">You can use hello default values provided by Azure.</span></span>  
10. <span data-ttu-id="750b2-141">Hello에 **요약** 블레이드에서 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-141">In hello **Summary** blade, click **OK**.</span></span>

## <a name="tooremotely-sign-in-tooyour-virtual-machine"></a><span data-ttu-id="750b2-142">tooremotely 로그인 tooyour 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="750b2-142">tooremotely sign in tooyour virtual machine</span></span>
1. <span data-ttu-id="750b2-143">Toohello 로그온 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-143">Log on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="750b2-144">**가상 컴퓨터(클래식)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-144">Click **Virtual machines (classic)**.</span></span> <span data-ttu-id="750b2-145">필요한 경우 클릭 **더 많은 서비스** hello 왼쪽된 아래 모서리에 hello 서비스 범주에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-145">If needed, click **More services** at hello bottom left corner under hello service categories.</span></span> <span data-ttu-id="750b2-146">hello **가상 컴퓨터 (클래식)** hello에 항목이 나타납니다 **계산** 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-146">hello **Virtual machines (classic)** entry is listed in hello **Compute** group.</span></span>
3. <span data-ttu-id="750b2-147">Hello 하려는 toosign에 hello 가상 컴퓨터 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-147">Click hello name of hello virtual machine that you want toosign in to.</span></span>
4. <span data-ttu-id="750b2-148">Hello 가상 컴퓨터 시작 후 hello hello 창 위쪽에 메뉴 연결을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-148">After hello virtual machine has started, a menu at hello top of hello pane allows connections.</span></span>
5. <span data-ttu-id="750b2-149">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-149">Click **Connect**.</span></span>
6. <span data-ttu-id="750b2-150">필요한 tooconnect toohello 가상 컴퓨터로 toohello 표시 되는 메시지에 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-150">Respond toohello prompts as needed tooconnect toohello virtual machine.</span></span> <span data-ttu-id="750b2-151">일반적으로 저장 하거나 hello 연결 정보를 포함 하는 hello.rdp 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-151">Typically, you save or open hello .rdp file that contains hello connection details.</span></span> <span data-ttu-id="750b2-152">Hello hello hello.rdp 파일의 첫 번째 줄의 마지막 부분으로 toocopy hello url: 포트를 가질 수도 있으며 원격 로그인 응용 프로그램에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-152">You might have toocopy hello url:port as hello last part of hello first line of hello .rdp file and paste it in a remote sign-in application.</span></span>

## <a name="tooinstall-a-java-application-server-on-your-virtual-machine"></a><span data-ttu-id="750b2-153">tooinstall 가상 컴퓨터에서 Java 응용 프로그램 서버</span><span class="sxs-lookup"><span data-stu-id="750b2-153">tooinstall a Java application server on your virtual machine</span></span>
<span data-ttu-id="750b2-154">Java 응용 프로그램 서버 tooyour 가상 컴퓨터를 복사할 수 있습니다 또는 설치 관리자를 통해 Java 응용 프로그램 서버를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-154">You can copy a Java application server tooyour virtual machine, or you can install a Java application server through an installer.</span></span>

<span data-ttu-id="750b2-155">이 자습서는 hello Java 응용 프로그램 서버 tooinstall으로 Tomcat을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-155">This tutorial uses Tomcat as hello Java application server tooinstall.</span></span>

1. <span data-ttu-id="750b2-156">Tooyour 가상 컴퓨터에 로그인 한 상태, 브라우저 세션을 너무 열[Apache Tomcat](http://tomcat.apache.org/download-80.cgi)합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-156">When you are signed in tooyour virtual machine, open a browser session too[Apache Tomcat](http://tomcat.apache.org/download-80.cgi).</span></span>
2. <span data-ttu-id="750b2-157">에 대 한 hello 링크를 두 번 클릭 **32 비트/64 비트 Windows 서비스 설치 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-157">Double-click hello link for **32-bit/64-bit Windows Service Installer**.</span></span> <span data-ttu-id="750b2-158">이 기술을 사용하면 Tomcat이 Windows 서비스로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-158">By using this technique, Tomcat installs as a Windows service.</span></span>
3. <span data-ttu-id="750b2-159">대화 상자가 나타나면 toorun hello 설치 관리자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-159">When prompted, choose toorun hello installer.</span></span>
4. <span data-ttu-id="750b2-160">Hello 내 **Apache Tomcat 설치** 마법사를 따라 hello tooinstall Tomcat 라는 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-160">Within hello **Apache Tomcat Setup** wizard, follow hello prompts tooinstall Tomcat.</span></span> <span data-ttu-id="750b2-161">이 자습서의 hello에서는 hello 기본값을 그대로 문제가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-161">For hello purposes of this tutorial, accepting hello defaults is fine.</span></span> <span data-ttu-id="750b2-162">Hello 나타나면 **Apache Tomcat 설치 마법사 완료 hello** 대화 상자에서 필요에 따라를 확인할 수 있습니다 **Apache Tomcat 실행** toohave 이제 Tomcat 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-162">When you reach hello **Completing hello Apache Tomcat Setup Wizard** dialog box, you can optionally check **Run Apache Tomcat** toohave Tomcat start now.</span></span> <span data-ttu-id="750b2-163">클릭 **마침** toocomplete hello Tomcat 설치 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-163">Click **Finish** toocomplete hello Tomcat setup process.</span></span>

## <a name="toostart-tomcat"></a><span data-ttu-id="750b2-164">Tomcat toostart</span><span class="sxs-lookup"><span data-stu-id="750b2-164">toostart Tomcat</span></span>

<span data-ttu-id="750b2-165">가상 컴퓨터와 실행 중인 hello 명령을 명령 프롬프트를 열어 Tomcat를 수동으로 시작할 수 있습니다 **net&nbsp;시작&nbsp;Tomcat8**합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-165">You can manually start Tomcat by opening a command prompt on your virtual machine and running hello command **net&nbsp;start&nbsp;Tomcat8**.</span></span>

<span data-ttu-id="750b2-166">Hello URL을 입력 하 여 Tomcat Tomcat 실행 되 면 액세스할 수 있습니다 <http://localhost:8080> hello 가상 컴퓨터의 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-166">Once Tomcat is running, you can access Tomcat by entering hello URL <http://localhost:8080> in hello virtual machine's browser.</span></span>

<span data-ttu-id="750b2-167">toosee 외부 컴퓨터에서 실행 되는 Tomcat toocreate 끝점 및 해야 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-167">toosee Tomcat running from external machines, you need toocreate an endpoint and open a port.</span></span>

## <a name="toocreate-an-endpoint-for-your-virtual-machine"></a><span data-ttu-id="750b2-168">가상 컴퓨터에 대 한 끝점 toocreate</span><span class="sxs-lookup"><span data-stu-id="750b2-168">toocreate an endpoint for your virtual machine</span></span>
1. <span data-ttu-id="750b2-169">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-169">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="750b2-170">**가상 컴퓨터(클래식)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-170">Click **Virtual machines (classic)**.</span></span>
3. <span data-ttu-id="750b2-171">Java 응용 프로그램 서버에서 실행 되는 hello 가상 컴퓨터의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-171">Click hello name of hello virtual machine that is running your Java application server.</span></span>
4. <span data-ttu-id="750b2-172">**Endpoints**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-172">Click **Endpoints**.</span></span>
5. <span data-ttu-id="750b2-173">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-173">Click **Add**.</span></span>
6. <span data-ttu-id="750b2-174">Hello에 **끝점 추가** 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="750b2-174">In hello **Add endpoint** dialog box:</span></span>
   1. <span data-ttu-id="750b2-175">Hello 끝점에 대 한 이름을 지정 합니다. 예를 들어 **HttpIn**합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-175">Specify a name for hello endpoint; for example, **HttpIn**.</span></span>
   2. <span data-ttu-id="750b2-176">선택 **TCP** hello 프로토콜에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-176">Select **TCP** for hello protocol.</span></span>
   3. <span data-ttu-id="750b2-177">지정 **80** hello 공용 포트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-177">Specify **80** for hello public port.</span></span>
   4. <span data-ttu-id="750b2-178">지정 **8080** hello 개인 포트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-178">Specify **8080** for hello private port.</span></span>
   5. <span data-ttu-id="750b2-179">선택 **비활성화** hello 부동 IP 주소에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-179">Select **Disabled** for hello floating IP address.</span></span>
   6. <span data-ttu-id="750b2-180">Hello 액세스 제어 목록을 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-180">Leave hello access control list as is.</span></span>
   7. <span data-ttu-id="750b2-181">Hello 클릭 **확인** tooclose hello 대화 상자 단추 및 hello 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-181">Click hello **OK** button tooclose hello dialog box and create hello endpoint.</span></span>

## <a name="tooopen-a-port-in-hello-firewall-for-your-virtual-machine"></a><span data-ttu-id="750b2-182">가상 컴퓨터에 대 한 hello 방화벽에서 포트 tooopen</span><span class="sxs-lookup"><span data-stu-id="750b2-182">tooopen a port in hello firewall for your virtual machine</span></span>
1. <span data-ttu-id="750b2-183">Tooyour 가상 컴퓨터에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-183">Sign in tooyour virtual machine.</span></span>
2. <span data-ttu-id="750b2-184">**Windows 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-184">Click **Windows Start**.</span></span>
3. <span data-ttu-id="750b2-185">**제어판**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-185">Click **Control Panel**.</span></span>
4. <span data-ttu-id="750b2-186">**시스템 및 보안**, **Windows 방화벽**, **고급 설정**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-186">Click **System and Security**, click **Windows Firewall**, and then click **Advanced Settings**.</span></span>
5. <span data-ttu-id="750b2-187">**인바운드 규칙**을 선택하고 **새 규칙**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-187">Click **Inbound Rules**, and then click **New Rule**.</span></span>  
   <span data-ttu-id="750b2-188">![새 인바운드 규칙][NewIBRule]</span><span class="sxs-lookup"><span data-stu-id="750b2-188">![New inbound rule][NewIBRule]</span></span>
6. <span data-ttu-id="750b2-189">Hello에 대 한 **규칙 유형**선택, **포트**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-189">For hello **Rule Type**, select **Port**, and then click **Next**.</span></span>  
   <span data-ttu-id="750b2-190">![새 인바운드 규칙 포트][NewRulePort]</span><span class="sxs-lookup"><span data-stu-id="750b2-190">![New inbound rule port][NewRulePort]</span></span>
7. <span data-ttu-id="750b2-191">Hello에 **프로토콜 및 포트** 화면에서 **TCP**, 지정 **8080** hello로 **특정 로컬 포트**, 클릭하고**다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-191">On hello **Protocol and Ports** screen, select **TCP**, specify **8080** as hello **Specific local port**, and then click **Next**.</span></span>  
  <span data-ttu-id="750b2-192">![새 인바운드 규칙][NewRuleProtocol]</span><span class="sxs-lookup"><span data-stu-id="750b2-192">![New inbound rule ][NewRuleProtocol]</span></span>
8. <span data-ttu-id="750b2-193">Hello에 **동작** 화면에서 **hello 연결 허용**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-193">On hello **Action** screen, select **Allow hello connection**, and then click **Next**.</span></span>
   <span data-ttu-id="750b2-194">![새 인바운드 규칙 동작][NewRuleAction]</span><span class="sxs-lookup"><span data-stu-id="750b2-194">![New inbound rule action][NewRuleAction]</span></span>
9. <span data-ttu-id="750b2-195">Hello에 **프로필** 화면에서 **도메인**, **개인**, 및 **공용** 를 선택한 다음 클릭 **다음** .</span><span class="sxs-lookup"><span data-stu-id="750b2-195">On hello **Profile** screen, ensure that **Domain**, **Private**, and **Public** are selected, and then click **Next**.</span></span>
   <span data-ttu-id="750b2-196">![새 인바운드 규칙 프로필][NewRuleProfile]</span><span class="sxs-lookup"><span data-stu-id="750b2-196">![New inbound rule profile][NewRuleProfile]</span></span>
10. <span data-ttu-id="750b2-197">그러나 Hello에 **이름** 화면에서 같이 hello 규칙에 대 한 이름을 지정 **HttpIn** (hello 규칙 이름이 하지 않으면 필요한 toomatch hello 끝점 이름을), 클릭 하 고 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-197">On hello **Name** screen, specify a name for hello rule, such as **HttpIn** (hello rule name is not required toomatch hello endpoint name, however), and then click **Finish**.</span></span>  
    <span data-ttu-id="750b2-198">![새 인바운드 규칙 이름][NewRuleName]</span><span class="sxs-lookup"><span data-stu-id="750b2-198">![New inbound rule name][NewRuleName]</span></span>

<span data-ttu-id="750b2-199">이제 외부 브라우저에서 Tomcat 웹 사이트를 볼 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-199">At this point, your Tomcat website should be viewable from an external browser.</span></span> <span data-ttu-id="750b2-200">Hello 브라우저의 주소 창에 hello 폼의 URL을 입력  **http://*프로그램\_DNS\_이름*. cloudapp.net**, 여기서 ***프로그램\_DNS\_이름*** hello 가상 컴퓨터를 만들 때 지정한 hello DNS 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-200">In hello browser's address window, type a URL of hello form **http://*your\_DNS\_name*.cloudapp.net**, where ***your\_DNS\_name*** is hello DNS name you specified when you created hello virtual machine.</span></span>

## <a name="application-lifecycle-considerations"></a><span data-ttu-id="750b2-201">응용 프로그램 수명 주기 고려 사항</span><span class="sxs-lookup"><span data-stu-id="750b2-201">Application lifecycle considerations</span></span>
* <span data-ttu-id="750b2-202">사용자 고유의 웹 응용 프로그램 보관 파일 (WAR)를 만들고 toohello 추가할 수 있습니다 **webapps** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-202">You could create your own web application archive (WAR) and add it toohello **webapps** folder.</span></span> <span data-ttu-id="750b2-203">예를 들어 기본 JSP(Java 서비스 페이지) 동적 웹 프로젝트를 만들어 WAR 파일로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-203">For example, create a basic Java Service Page (JSP) dynamic web project and export it as a WAR file.</span></span> <span data-ttu-id="750b2-204">이제 hello WAR toohello Apache Tomcat 복사 **webapps** 후 브라우저에서 실행 되는 hello 가상 컴퓨터의 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-204">Next, copy hello WAR toohello Apache Tomcat **webapps** folder on hello virtual machine, then run it in a browser.</span></span>
* <span data-ttu-id="750b2-205">기본적으로 hello Tomcat 서비스를 설치 하는 경우 설정은 toostart 수동으로입니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-205">By default when hello Tomcat service is installed, it is set toostart manually.</span></span> <span data-ttu-id="750b2-206">전환할 수도 있습니다 toostart 자동으로 hello 서비스 스냅인을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-206">You can switch it toostart automatically by using hello Services snap-in.</span></span> <span data-ttu-id="750b2-207">클릭 하 여 hello 서비스 스냅인 시작 **Windows 시작**, **관리 도구**, 차례로 **서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-207">Start hello Services snap-in by clicking **Windows Start**, **Administrative Tools**, and then **Services**.</span></span> <span data-ttu-id="750b2-208">Hello를 두 번 클릭 **Apache Tomcat** 서비스 설정 및 **시작 유형** 너무**자동**합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-208">Double-click hello **Apache Tomcat** service and set **Startup type** too**Automatic**.</span></span>

    ![서비스 toostart를 자동으로 설정][service_automatic_startup]

    <span data-ttu-id="750b2-210">hello 있으면 자동으로 시작 하는 Tomcat는 hello 가상 컴퓨터 (예를 들어 한 후 다시 부팅 해야 하는 소프트웨어 업데이트 설치 되어 있음)를 다시 부팅 될 때 실행 되 고 시작 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-210">hello benefit of having Tomcat start automatically is that it starts running when hello virtual machine is rebooted (for example, after software updates that require a reboot are installed).</span></span>

## <a name="next-steps"></a><span data-ttu-id="750b2-211">다음 단계</span><span class="sxs-lookup"><span data-stu-id="750b2-211">Next steps</span></span>
<span data-ttu-id="750b2-212">사용할 수 있는 다른 서비스 (예: Azure 저장소, 서비스 버스, SQL 데이터베이스)에 대 한 학습할 수 있는 Java 응용 프로그램과 함께 tooinclude 합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-212">You can learn about other services (such as Azure Storage, service bus, and SQL Database) that you may want tooinclude with your Java applications.</span></span> <span data-ttu-id="750b2-213">Hello에서 사용할 수 있는 hello 정보를 확인할 [Java 개발자 센터](https://azure.microsoft.com/develop/java/)합니다.</span><span class="sxs-lookup"><span data-stu-id="750b2-213">View hello information available at hello [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[virtual_machine_tomcat]:media/java-run-tomcat-app-server/WA_VirtualMachineRunningApacheTomcat.png

[service_automatic_startup]:media/java-run-tomcat-app-server/WA_TomcatServiceAutomaticStart.png









[NewIBRule]:media/java-run-tomcat-app-server/NewInboundRule.png
[NewRulePort]:media/java-run-tomcat-app-server/NewRulePort.png
[NewRuleProtocol]:media/java-run-tomcat-app-server/NewRuleProtocol.png
[NewRuleAction]:media/java-run-tomcat-app-server/NewRuleAction.png
[NewRuleName]:media/java-run-tomcat-app-server/NewRuleName.png
[NewRuleProfile]:media/java-run-tomcat-app-server/NewRuleProfile.png


<!-- Deleted from hello "toocreate an ednpoint for your virtual mache" 3/17/2017,
     toouse hello new portal.
6. In hello **Add endpoint** dialog box, ensure **Add standalone endpoint** is selected, and then click **Next**.
7. In hello **New endpoint details** dialog box:
-->
