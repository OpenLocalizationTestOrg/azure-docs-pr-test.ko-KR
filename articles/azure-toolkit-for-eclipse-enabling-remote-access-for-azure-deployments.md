---
title: "Eclipse에서 Azure 배포에 대한 원격 액세스를 사용하도록 설정"
description: "Eclipse용 Azure 도구 키트를 사용하여 Azure 배포에 대한 원격 액세스를 사용하도록 설정하는 방법에 알아봅니다."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: b6150006-9a7f-4d83-be18-d35ec780c7c5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 654d511bd5a62341f87569317e97360c94a6f26c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a><span data-ttu-id="fb210-103">Eclipse에서 Azure 배포에 대한 원격 액세스를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="fb210-103">Enabling Remote Access for Azure Deployments in Eclipse</span></span>
<span data-ttu-id="fb210-104">배포를 해결하기 위해 원격 액세스를 활성화하고 사용하여 배포를 호스팅하는 가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-104">To help troubleshoot your deployments, you may enable and use Remote Access to connect to the virtual machine hosting your deployment.</span></span> <span data-ttu-id="fb210-105">원격 액세스 기능은 원격 데스크톱 프로토콜(RDP)에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-105">The Remote Access functionality relies on the Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="fb210-106">Azure에 게시한 후 배포에 대한 원격 액세스를 구성할 수 있거나 Windows 운영 체제와 Eclipse를 사용하는 경우 Azure에 게시하기 전에 원격 액세스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-106">You can configure Remote Access for your deployment after you have published it to Azure, or if you are using Eclipse with a Windows operating system, you can configure Remote Access before you publish to Azure.</span></span> <span data-ttu-id="fb210-107">Azure에서 배포의 가상 컴퓨터에 연결하기 위해 운영 체제와 호환되는 원격 데스크톱 클라이언트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-107">Note that you will need a remote desktop client that is compatible with your operating system in order to connect to your deployment's virtual machine in Azure.</span></span>

## <a name="how-to-enable-remote-access-before-you-deploy-to-azure"></a><span data-ttu-id="fb210-108">Azure에 배포하기 전에 원격 액세스를 사용하도록 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="fb210-108">How to enable Remote Access before you deploy to Azure</span></span>
> [!NOTE]
> <span data-ttu-id="fb210-109">Azure에 응용 프로그램을 배포하기 전에 원격 액세스를 사용하도록 설정하려면 Windows에서 Eclipse를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-109">To enable Remote Access before you deploy your application to Azure, you need to be running Eclipse on Windows.</span></span>
> 
> 

<span data-ttu-id="fb210-110">다음 이미지는 원격 액세스를 활성화하는 데 사용되는 **원격 액세스** 속성 대화 상자를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-110">The following image shows the **Remote Access** properties dialog used to enable remote access.</span></span>

![][ic719494]

<span data-ttu-id="fb210-111">**원격 액세스** 속성 대화 상자를 표시하는 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-111">There are two ways to display the **Remote Access** properties dialog:</span></span>

* <span data-ttu-id="fb210-112">**Azure에 게시** 대화 상자의 **원격 액세스** 섹션에서 **고급** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-112">Click the **Advanced** link in the **Remote Access** section of the **Publish to Azure** dialog.</span></span>

* <span data-ttu-id="fb210-113">Azure 프로젝트의 **속성** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-113">Open the **Properties** dialog of your Azure project.</span></span>

<span data-ttu-id="fb210-114">새 Azure 배포 프로젝트를 만드는 경우 프로젝트는 기본적으로 활성화된 원격 액세스가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-114">When you create a new Azure deployment project, the project will not have Remote Access enabled by default.</span></span> <span data-ttu-id="fb210-115">그러나 **Azure에 게시** 대화 상자에서 사용자 이름 및 암호를 지정하여 쉽게 원격 액세스를 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-115">However, you can easily enable remote access by specifying the user name and password in the **Publish to Azure** dialog.</span></span> <span data-ttu-id="fb210-116">원격 액세스 암호는 X.509 인증서를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-116">The Remote Access password is encrypted using X.509 certificates.</span></span> <span data-ttu-id="fb210-117">사용자 인증서를 제공하지 않는 경우 암호화는 Eclipse용 Azure 플러그 인과 함께 제공되는 자체 서명된 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-117">If you do not use provide your own certificate, the encryption relies on a self-signed certificate shipped with the Azure Plugin for Eclipse.</span></span> <span data-ttu-id="fb210-118">이 자체 서명된 인증서는 Azure 프로젝트의 **cert** 폴더에 있으며 공용 인증서 파일(SampleRemoteAccessPublic.cer) 및 개인 정보 교환(PFX) 인증서 파일(SampleRemoteAccessPrivate.pfx) 모두로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-118">This self-signed certificate is in the **cert** folder of your Azure project, stored both as a public certificate file (SampleRemoteAccessPublic.cer) and as a Personal Information Exchange (PFX) certificate file (SampleRemoteAccessPrivate.pfx).</span></span> <span data-ttu-id="fb210-119">후자는 인증서에 대한 개인 키를 포함하고 기본 암호, **Password1**을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-119">The latter contains the private key for the certificate, and it has a default password, **Password1**.</span></span> <span data-ttu-id="fb210-120">그러나 이 암호는 공공 정보이므로 기본 인증서는 프로덕션 배포용이 아닌 학습 용도로만 사용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-120">However, since this password is public knowledge, the default certificate should be used only for learning purposes, not for a production deployment.</span></span> <span data-ttu-id="fb210-121">따라서 학습 목적 이외로 배포를 위한 원격 세션을 사용하도록 설정하려는 경우 **Azure에 게시** 대화 상자에서 **고급** 링크를 클릭하여 고유 인증서를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-121">So other than for learning purposes, when you want to enabled remote sessions for your deployments, you should click the **Advanced** link in the **Publish to Azure** dialog to specify your own certificate.</span></span> <span data-ttu-id="fb210-122">Azure에서 사용자 암호를 해독할 수 있도록 Azure 관리 포털 내의 호스티드 서비스에 인증서의 PFX 버전을 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-122">Note that you'll need to upload the PFX version of the certificate to your hosted service within the Azure Management Portal, so that Azure can decrypt the user password.</span></span>

<span data-ttu-id="fb210-123">이 자습서의 나머지 부분에서는 사용하지 않도록 설정된 원격 액세스를 사용하여 처음에 만든 Azure 배포 프로젝트에 대한 원격 액세스를 사용하도록 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-123">The remainder of the tutorial shows you how to enable remote access for an Azure deployment project that was initially created with remote access disabled.</span></span> <span data-ttu-id="fb210-124">이 자습서의 목적을 위해 새 자체 서명된 인증서를 만들 예정이며 해당 .pfx 파일은 사용자가 선택한 암호를 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-124">For purposes of this tutorial, we'll create a new self-signed certificate, and its .pfx file will have a password of your choice.</span></span> <span data-ttu-id="fb210-125">인증 기관에서 발급한 인증서를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-125">You also have the option of using a certificate issued by a certificate authority.</span></span>

## <a name="how-to-enable-remote-access-after-you-have-deployed-to-azure"></a><span data-ttu-id="fb210-126">Azure에 배포한 후에 원격 액세스를 사용하도록 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="fb210-126">How to enable Remote Access after you have deployed to Azure</span></span>
<span data-ttu-id="fb210-127">Azure에 배포한 후 원격 액세스를 사용하도록 설정하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-127">To enable remote access after you have deployed to Azure, use the following steps:</span></span>

1. <span data-ttu-id="fb210-128">Azure 계정을 사용하여 Azure 관리 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-128">Log into the Azure management portal using your Azure account</span></span>

2. <span data-ttu-id="fb210-129">**클라우드 서비스**목록에서 배포된 클라우드 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-129">In your list of **Cloud Services**, select your deployed cloud service</span></span>

3. <span data-ttu-id="fb210-130">클라우드 서비스 웹 페이지에서 **구성** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-130">In the cloud service web page, click the **Configure** link</span></span>

4. <span data-ttu-id="fb210-131">구성 페이지의 맨 아래에서 **원격** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-131">On the bottom of the configuration page, click the **Remote** link</span></span>

5. <span data-ttu-id="fb210-132">팝업 대화 상자가 나타나는 경우:</span><span class="sxs-lookup"><span data-stu-id="fb210-132">When the pop-up dialog box appears:</span></span>
   
   * <span data-ttu-id="fb210-133">원격 액세스를 사용하도록 설정하려는 역할을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-133">Specify the Role you for which you want to enable remote access</span></span>

   * <span data-ttu-id="fb210-134">클릭하여 **원격 데스크톱 사용** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-134">Click to select the **Enable Remote Desktop** checkbox</span></span>
   
   * <span data-ttu-id="fb210-135">원격 액세스에 대해 사용하려는 사용자 이름 및 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-135">Specify a user name and password you want to use for remote access</span></span>
   
   * <span data-ttu-id="fb210-136">사용할 인증서를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-136">Select the certificate to use</span></span>

6. <span data-ttu-id="fb210-137">**확인**</span><span class="sxs-lookup"><span data-stu-id="fb210-137">Click **OK**</span></span> 

<span data-ttu-id="fb210-138">구성 변경이 진행 중임을 나타내는 메시지가 표시되며 완료하려면 몇 분 정도 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-138">You will see a message stating that your configuration change is in progress, which may take a few minutes to complete.</span></span> <span data-ttu-id="fb210-139">구성 변경이 완료된 후 이 문서의 뒷부분에 나오는 **원격으로 로그인하려면** 섹션의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-139">After the configuration change has completed, follow the steps in the **To log in remotely** section later in this article.</span></span>

## <a name="how-to-enable-remote-access-in-your-package"></a><span data-ttu-id="fb210-140">패키지에서 원격 액세스를 사용하도록 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="fb210-140">How to enable Remote Access in your package</span></span>
1. <span data-ttu-id="fb210-141">Eclipse의 Project Explorer 창에서 Azure 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Properties**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-141">Within Eclipse's Project Explorer pane, right-click your Azure project and click **Properties**.</span></span>

2. <span data-ttu-id="fb210-142">**속성** 대화 상자에서 왼쪽 창의 **Azure**를 확장하고 **원격 액세스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-142">In the **Properties** dialog, expand **Azure** in the left-hand pane and click **Remote Access**.</span></span>

3. <span data-ttu-id="fb210-143">**원격 액세스** 대화 상자에서 **모든 역할이 다음 로그인 자격 증명을 사용하는 원격 데스크톱 연결을 수락하도록 허용**이 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-143">In the **Remote Access** dialog, ensure **Enable all roles to accept Remote Desktop Connections with these login credentials** is checked.</span></span>

4. <span data-ttu-id="fb210-144">원격 데스크톱 연결에 대한 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-144">Specify a user name for the Remote Desktop connection.</span></span>

5. <span data-ttu-id="fb210-145">사용자에 대한 암호를 지정하고 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-145">Specify and confirm the password for the user.</span></span> <span data-ttu-id="fb210-146">이 대화 상자에 설정된 사용자 이름 및 암호 값은 원격 데스크톱 연결을 설정할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-146">The user name and password values set in this dialog will be used when you make a Remote Desktop connection.</span></span> <span data-ttu-id="fb210-147">(이것은 PFX 암호와 다른 별도 암호입니다.)</span><span class="sxs-lookup"><span data-stu-id="fb210-147">(Note that this is a separate password from your PFX password.)</span></span>

6. <span data-ttu-id="fb210-148">사용자 계정에 대한 만료 날짜를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-148">Specify the expiration date for the user account.</span></span>

7. <span data-ttu-id="fb210-149">**New** 를 클릭하여 자체 서명된 새로운 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-149">Click **New** to create a new self-signed certificate.</span></span> <span data-ttu-id="fb210-150">(또는 **작업 영역** 또는 **파일 시스템** 단추를 통해 각각 작업 영역이나 파일 시스템에서 인증서를 선택할 수 있지만 이 자습서의 목적을 위해 새 인증서를 만듭니다.)</span><span class="sxs-lookup"><span data-stu-id="fb210-150">(Alternatively, you could select a certificate from your workspace or file system through the **Workspace** or **FileSystem** buttons, respectively, but for purposes of this tutorial we'll create a new certificate.)</span></span>

   * <span data-ttu-id="fb210-151">**New Certificate** 대화 상자에서 PFX 파일에서 사용할 암호를 지정하고 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-151">In the **New Certificate** dialog, specify and confirm the password you'll use for your PFX file.</span></span>

   * <span data-ttu-id="fb210-152">**Name (CN)**에서 제공된 값을 사용하거나 사용자 지정 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-152">Accept the value provided for **Name (CN)**, or use a custom name.</span></span>

   * <span data-ttu-id="fb210-153">.cer 형식으로 새 인증서가 저장될 경로 및 파일 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-153">Specify the path and file name where the new certificate, in .cer form, will be saved.</span></span> <span data-ttu-id="fb210-154">이 단계와 다음 단계의 경우 Azure 프로젝트의 **cert** 폴더를 사용할 수 있지만 다른 위치를 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-154">For this step and the next step, you could use the **cert** folder of your Azure project, but you're free to choose another location.</span></span> <span data-ttu-id="fb210-155">이 자습서의 목적을 위해 **c:\mycert\mycert.cer**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-155">For purposes of this tutorial, we'll use **c:\mycert\mycert.cer**.</span></span> <span data-ttu-id="fb210-156">(계속하기 전에 **c:\mycert** 폴더를 만들거나 원하는 경우 기존 폴더를 사용합니다.)</span><span class="sxs-lookup"><span data-stu-id="fb210-156">(Create the **c:\mycert** folder prior to proceeding, or use an existing folder if desired.)</span></span>

   * <span data-ttu-id="fb210-157">.cer 형식으로 새 인증서 및 해당 개인 키가 저장될 경로 및 파일 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-157">Specify the path and file name where the new certificate and its private key, in .pfx form, will be saved.</span></span> <span data-ttu-id="fb210-158">이 자습서의 목적을 위해 **c:\mycert\mycert.pfx**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-158">For purposes of this tutorial, we'll use **c:\mycert\mycert.pfx**.</span></span> <span data-ttu-id="fb210-159">**새 인증서** 대화 상자는 다음과 유사합니다(**c:\mycert**를 사용하지 않은 경우 폴더 경로 업데이트).</span><span class="sxs-lookup"><span data-stu-id="fb210-159">Your **New Certificate** dialog should look similar to the following (update the folder paths if you did not use **c:\mycert**):</span></span>
     
      ![][ic712275]

   * <span data-ttu-id="fb210-160">**확인**을 클릭하여 **새 인증서** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-160">Click **OK** to close the **New Certificate** dialog.</span></span>

8. <span data-ttu-id="fb210-161">**원격 액세스** 대화 상자는 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-161">Your **Remote Access** dialog should look similar to the following:</span></span></p>
   
   ![][ic719495]

9. <span data-ttu-id="fb210-162">**확인**을 클릭하여 **원격 액세스** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-162">Click **OK** to close the **Remote Access** dialog.</span></span>

<span data-ttu-id="fb210-163">클라우드 배포용으로 설정된 빌드로 응용 프로그램을 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-163">Rebuild your application, with the build set for deployment to cloud.</span></span>

## <a name="to-log-in-remotely"></a><span data-ttu-id="fb210-164">원격으로 로그인하려면</span><span class="sxs-lookup"><span data-stu-id="fb210-164">To log in remotely</span></span>
<span data-ttu-id="fb210-165">역할 인스턴스가 준비되면 응용 프로그램을 호스팅하는 가상 컴퓨터에 원격으로 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-165">Once your role instance is ready, you can remotely log in to the virtual machine that is hosting your application.</span></span>

* <span data-ttu-id="fb210-166">Azure에 배포하는 동안 Windows에서 Eclipse를 사용하고 **Start remote desktop on deploy** 옵션을 선택한 경우 배포를 시작할 때 원격 데스크톱 연결 로그온 화면이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-166">If are using Eclipse on Windows and you selected the **Start remote desktop on deploy** option during your deployment to Azure, you will be presented with a Remote Desktop Connection logon screen when your deployment starts.</span></span> <span data-ttu-id="fb210-167">사용자 이름 및 암호를 묻는 메시지가 나타나면 원격 사용자에 대해 지정한 값을 입력하고 로그인할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-167">When you are prompted for the user name and password, enter the values that you specified for the remote user and will be able to log in.</span></span>

* <span data-ttu-id="fb210-168">원격으로 로그인하는 또 다른 방법은 <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure 관리 포털</a>을 통해서 입니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-168">Another way to log in remotely is through the <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:</span></span>
  
  * <span data-ttu-id="fb210-169">Azure 관리 포털의 **클라우드 서비스** 보기 내에서 **인스턴스**를 클릭하고 특정 인스턴스를 클릭한 다음 **연결** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-169">Within the **Cloud Services** view of the Azure Management portal, click your cloud service, click **Instances**, click a specific instance, and then click the **Connect** button.</span></span> <span data-ttu-id="fb210-170">**연결** 단추가 명령 모음에서 다음과 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-170">The **Connect** button appears as the following in the command bar:</span></span>
    
      ![][ic659273]

  * <span data-ttu-id="fb210-171">**연결** 단추를 클릭한 후 RDP 파일을 열라는 메시지가 나타납니다</span><span class="sxs-lookup"><span data-stu-id="fb210-171">After clicking the **Connect** button, you will be prompted to open an RDP file.</span></span> <span data-ttu-id="fb210-172">파일을 열고 프롬프트를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-172">Open the file and follow the prompts.</span></span> <span data-ttu-id="fb210-173">(이 파일을 로컬 컴퓨터에 저장한 다음 두 번 클릭하여 파일을 실행하여 관리 포털로 먼저 이동하지 않고도 가상 컴퓨터에 원격으로 로그인할 수도 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="fb210-173">(You could also save this file to your local computer, and then run the file by double-clicking it to remote log in to your virtual machine without needing to first go the management portal.)</span></span>

  * <span data-ttu-id="fb210-174">사용자 이름 및 암호를 묻는 메시지가 나타나면 원격 사용자에 대해 지정한 값을 입력하고 로그인할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-174">When you are prompted for the user name and password, enter the values that you specified for the remote user and will be able to log in.</span></span>

> [!NOTE]
> <span data-ttu-id="fb210-175">비 Windows 운영 체제에 있는 경우 운영 체제와 호환되는 원격 데스크톱 클라이언트를 사용하고 다운로드한 RDP 파일의 설정을 사용하여 해당 클라이언트를 구성하는 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb210-175">If you are on a non-Windows operating system, you need to use a Remote Desktop client that is compatible with your operating system and follow the steps to configure that client with the settings in the RDP file that you downloaded.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="fb210-176">참고 항목</span><span class="sxs-lookup"><span data-stu-id="fb210-176">See Also</span></span>
<span data-ttu-id="fb210-177">[Eclipse용 Azure 도구 키트][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="fb210-177">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="fb210-178">[Eclipse에서 Azure용 Hello World 응용 프로그램 만들기][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="fb210-178">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="fb210-179">[Eclipse용 Azure 도구 키트 설치][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="fb210-179">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="fb210-180">Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Azure Java 개발자 센터][Azure Java Developer Center]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb210-180">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
