---
title: "aaaEnabling Eclipse에서 Azure 배포에 대 한 원격 액세스"
description: "Eclipse 용 Azure 도구 키트 hello를 사용 하 여 Azure 배포에 대 한 tooenable 원격 액세스 하는 방법을 알아봅니다."
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
ms.openlocfilehash: 00c2bf22c1f3ec792098f154f771c87506e87881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a><span data-ttu-id="41345-103">Eclipse에서 Azure 배포에 대한 원격 액세스를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="41345-103">Enabling Remote Access for Azure Deployments in Eclipse</span></span>
<span data-ttu-id="41345-104">toohelp 배포 문제 해결, 사용 하도록 설정 하 고 배포를 호스트 하는 원격 액세스 tooconnect toohello 가상 컴퓨터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41345-104">toohelp troubleshoot your deployments, you may enable and use Remote Access tooconnect toohello virtual machine hosting your deployment.</span></span> <span data-ttu-id="41345-105">원격 액세스 기능 hello hello 프로토콜 RDP (원격 데스크톱)에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="41345-105">hello Remote Access functionality relies on hello Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="41345-106">TooAzure를 게시 하기 전에 원격 액세스를 구성할 수 Eclipse와 Windows 운영 체제를 사용 하는 경우 또는 tooAzure, 게시 한 후 배포에 대 한 원격 액세스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41345-106">You can configure Remote Access for your deployment after you have published it tooAzure, or if you are using Eclipse with a Windows operating system, you can configure Remote Access before you publish tooAzure.</span></span> <span data-ttu-id="41345-107">참고가 Azure에서 순서 tooconnect tooyour 배포의 가상 컴퓨터의 운영 체제와 호환 되는 원격 데스크톱 클라이언트 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="41345-107">Note that you will need a remote desktop client that is compatible with your operating system in order tooconnect tooyour deployment's virtual machine in Azure.</span></span>

## <a name="how-tooenable-remote-access-before-you-deploy-tooazure"></a><span data-ttu-id="41345-108">원격 액세스 하기 전에 tooenable tooAzure를 배포 하는 방법</span><span class="sxs-lookup"><span data-stu-id="41345-108">How tooenable Remote Access before you deploy tooAzure</span></span>
> [!NOTE]
> <span data-ttu-id="41345-109">응용 프로그램 tooAzure를 배포 하기 전에 원격 액세스 tooenable toobe Windows에서 Eclipse를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41345-109">tooenable Remote Access before you deploy your application tooAzure, you need toobe running Eclipse on Windows.</span></span>
> 
> 

<span data-ttu-id="41345-110">hello 다음 그림에 나와 hello **원격 액세스** 속성 대화 상자 tooenable 원격 액세스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="41345-110">hello following image shows hello **Remote Access** properties dialog used tooenable remote access.</span></span>

![][ic719494]

<span data-ttu-id="41345-111">두 가지 방법으로 toodisplay hello **원격 액세스** 속성 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="41345-111">There are two ways toodisplay hello **Remote Access** properties dialog:</span></span>

* <span data-ttu-id="41345-112">Hello 클릭 **고급** hello에 대 한 링크 **원격 액세스** hello 섹션 **tooAzure 게시** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="41345-112">Click hello **Advanced** link in hello **Remote Access** section of hello **Publish tooAzure** dialog.</span></span>

* <span data-ttu-id="41345-113">열기 hello **속성** Azure 프로젝트의 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="41345-113">Open hello **Properties** dialog of your Azure project.</span></span>

<span data-ttu-id="41345-114">새 Azure 배포 프로젝트를 만들면 hello 프로젝트는 기본적으로 사용 하는 원격 액세스 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41345-114">When you create a new Azure deployment project, hello project will not have Remote Access enabled by default.</span></span> <span data-ttu-id="41345-115">그러나 있습니다 사용 하 여 쉽게 원격 액세스 hello에 hello 사용자 이름 및 암호를 지정 하 여 **tooAzure 게시** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="41345-115">However, you can easily enable remote access by specifying hello user name and password in hello **Publish tooAzure** dialog.</span></span> <span data-ttu-id="41345-116">hello 원격 액세스 암호는 X.509 인증서를 사용 하 여 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41345-116">hello Remote Access password is encrypted using X.509 certificates.</span></span> <span data-ttu-id="41345-117">사용 하지 않는 경우, 사용자 고유의 인증서를 제공 hello 암호화는 hello Eclipse 용 Azure 플러그 인과 함께 제공 된 자체 서명 된 인증서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="41345-117">If you do not use provide your own certificate, hello encryption relies on a self-signed certificate shipped with hello Azure Plugin for Eclipse.</span></span> <span data-ttu-id="41345-118">Hello에이 자체 서명 된 인증서가 **cert** Azure 프로젝트의 폴더를 저장 된 공용 인증서 파일 (SampleRemoteAccessPublic.cer)로 모두 및 개인 정보 교환 (PFX)으로 인증서 파일 ( SampleRemoteAccessPrivate.pfx)입니다.</span><span class="sxs-lookup"><span data-stu-id="41345-118">This self-signed certificate is in hello **cert** folder of your Azure project, stored both as a public certificate file (SampleRemoteAccessPublic.cer) and as a Personal Information Exchange (PFX) certificate file (SampleRemoteAccessPrivate.pfx).</span></span> <span data-ttu-id="41345-119">후자의 hello hello hello 인증서에 대 한 개인 키가 포함 되어 있고 기본 암호 인 **Password1**합니다.</span><span class="sxs-lookup"><span data-stu-id="41345-119">hello latter contains hello private key for hello certificate, and it has a default password, **Password1**.</span></span> <span data-ttu-id="41345-120">그러나이 암호는 누구나 알 이후 학습 목적으로 프로덕션 배포에 대 한 하지에 대해서만 hello 기본 인증서를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41345-120">However, since this password is public knowledge, hello default certificate should be used only for learning purposes, not for a production deployment.</span></span> <span data-ttu-id="41345-121">따라서 이외의 학습 목적으로 배포를 위한 tooenabled 원격 세션을 원하는 경우 클릭 하 여 해야 hello **고급** hello에 대 한 링크 **tooAzure 게시** 대화 toospecify 직접 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="41345-121">So other than for learning purposes, when you want tooenabled remote sessions for your deployments, you should click hello **Advanced** link in hello **Publish tooAzure** dialog toospecify your own certificate.</span></span> <span data-ttu-id="41345-122">해당 Azure hello 사용자 암호를 해독할 수 있으므로 hello Azure 관리 포털 내에서 서비스를 호스트 하는 참고 hello 인증서 tooyour tooupload hello PFX 버전이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="41345-122">Note that you'll need tooupload hello PFX version of hello certificate tooyour hosted service within hello Azure Management Portal, so that Azure can decrypt hello user password.</span></span>

<span data-ttu-id="41345-123">hello 자습서의 나머지 부분에서는 hello tooenable 원격 사용 하지 않도록 설정 하는 원격 액세스를 사용 하 여 처음에 만든 Azure 배포 프로젝트에 대 한 액세스 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="41345-123">hello remainder of hello tutorial shows you how tooenable remote access for an Azure deployment project that was initially created with remote access disabled.</span></span> <span data-ttu-id="41345-124">이 자습서의 목적을 위해 새 자체 서명된 인증서를 만들 예정이며 해당 .pfx 파일은 사용자가 선택한 암호를 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41345-124">For purposes of this tutorial, we'll create a new self-signed certificate, and its .pfx file will have a password of your choice.</span></span> <span data-ttu-id="41345-125">인증 기관에서 발급 한 인증서를 사용 하 여 hello 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41345-125">You also have hello option of using a certificate issued by a certificate authority.</span></span>

## <a name="how-tooenable-remote-access-after-you-have-deployed-tooazure"></a><span data-ttu-id="41345-126">원격 액세스 한 후 tooenable tooAzure 구축 하는 방법을</span><span class="sxs-lookup"><span data-stu-id="41345-126">How tooenable Remote Access after you have deployed tooAzure</span></span>
<span data-ttu-id="41345-127">tooenable 원격 액세스 배포 tooAzure를 사용 하 여 hello 단계를 수행 하면:</span><span class="sxs-lookup"><span data-stu-id="41345-127">tooenable remote access after you have deployed tooAzure, use hello following steps:</span></span>

1. <span data-ttu-id="41345-128">Azure 계정을 사용 하 여 hello Azure 관리 포털에 로그인</span><span class="sxs-lookup"><span data-stu-id="41345-128">Log into hello Azure management portal using your Azure account</span></span>

2. <span data-ttu-id="41345-129">**클라우드 서비스**목록에서 배포된 클라우드 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="41345-129">In your list of **Cloud Services**, select your deployed cloud service</span></span>

3. <span data-ttu-id="41345-130">Hello 클라우드 서비스 웹 페이지에서 클릭 hello **구성** 링크</span><span class="sxs-lookup"><span data-stu-id="41345-130">In hello cloud service web page, click hello **Configure** link</span></span>

4. <span data-ttu-id="41345-131">Hello 구성 페이지의 아래쪽 hello 클릭 hello **원격** 링크</span><span class="sxs-lookup"><span data-stu-id="41345-131">On hello bottom of hello configuration page, click hello **Remote** link</span></span>

5. <span data-ttu-id="41345-132">Hello 팝업 대화 상자가 나타나는 경우:</span><span class="sxs-lookup"><span data-stu-id="41345-132">When hello pop-up dialog box appears:</span></span>
   
   * <span data-ttu-id="41345-133">Hello 역할을 지정 하면 tooenable 원격 액세스 하려는</span><span class="sxs-lookup"><span data-stu-id="41345-133">Specify hello Role you for which you want tooenable remote access</span></span>

   * <span data-ttu-id="41345-134">Tooselect hello 클릭 **원격 데스크톱 사용** 확인란</span><span class="sxs-lookup"><span data-stu-id="41345-134">Click tooselect hello **Enable Remote Desktop** checkbox</span></span>
   
   * <span data-ttu-id="41345-135">사용자 이름 및 원격 액세스를 위한 toouse 원하는 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41345-135">Specify a user name and password you want toouse for remote access</span></span>
   
   * <span data-ttu-id="41345-136">Hello 인증서 toouse 선택</span><span class="sxs-lookup"><span data-stu-id="41345-136">Select hello certificate toouse</span></span>

6. <span data-ttu-id="41345-137">**확인**</span><span class="sxs-lookup"><span data-stu-id="41345-137">Click **OK**</span></span> 

<span data-ttu-id="41345-138">구성 변경 진행 중 몇 분 toocomplete 소요 될 수 있는 않다는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41345-138">You will see a message stating that your configuration change is in progress, which may take a few minutes toocomplete.</span></span> <span data-ttu-id="41345-139">Hello 구성 변경이 완료 되 면에서 다음과 같이 hello hello **toolog에 원격으로** 이 문서의 뒷부분에 나오는 섹션.</span><span class="sxs-lookup"><span data-stu-id="41345-139">After hello configuration change has completed, follow hello steps in hello **toolog in remotely** section later in this article.</span></span>

## <a name="how-tooenable-remote-access-in-your-package"></a><span data-ttu-id="41345-140">Tooenable 원격 패키지에 액세스 하는 방법</span><span class="sxs-lookup"><span data-stu-id="41345-140">How tooenable Remote Access in your package</span></span>
1. <span data-ttu-id="41345-141">Eclipse의 Project Explorer 창에서 Azure 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Properties**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41345-141">Within Eclipse's Project Explorer pane, right-click your Azure project and click **Properties**.</span></span>

2. <span data-ttu-id="41345-142">Hello에 **속성** 대화 상자를 확장 하 고 **Azure** hello 왼쪽 창에서 **원격 액세스**합니다.</span><span class="sxs-lookup"><span data-stu-id="41345-142">In hello **Properties** dialog, expand **Azure** in hello left-hand pane and click **Remote Access**.</span></span>

3. <span data-ttu-id="41345-143">Hello에 **원격 액세스** 대화 상자에서 확인 **이 로그인 자격 증명으로 모든 역할 tooaccept 원격 데스크톱 연결을 사용 하도록 설정** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="41345-143">In hello **Remote Access** dialog, ensure **Enable all roles tooaccept Remote Desktop Connections with these login credentials** is checked.</span></span>

4. <span data-ttu-id="41345-144">Hello 원격 데스크톱 연결에 대 한 사용자 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41345-144">Specify a user name for hello Remote Desktop connection.</span></span>

5. <span data-ttu-id="41345-145">지정 하 고 hello 사용자에 대 한 hello 암호를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="41345-145">Specify and confirm hello password for hello user.</span></span> <span data-ttu-id="41345-146">hello 사용자 이름 및 암호 설정 된 값이 대화이 상자에 원격 데스크톱 연결을 설정할 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41345-146">hello user name and password values set in this dialog will be used when you make a Remote Desktop connection.</span></span> <span data-ttu-id="41345-147">(이것은 PFX 암호와 다른 별도 암호입니다.)</span><span class="sxs-lookup"><span data-stu-id="41345-147">(Note that this is a separate password from your PFX password.)</span></span>

6. <span data-ttu-id="41345-148">Hello 사용자 계정에 대 한 hello 만료 날짜를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41345-148">Specify hello expiration date for hello user account.</span></span>

7. <span data-ttu-id="41345-149">클릭 **새로** toocreate 새 자체 서명 된 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="41345-149">Click **New** toocreate a new self-signed certificate.</span></span> <span data-ttu-id="41345-150">(또는 hello 통해 작업 영역이 나 파일 시스템에서 인증서를 선택할 수 **작업 영역** 또는 **FileSystem** 각각 하지만이 자습서에서는 새 만듭니다 단추 인증서입니다.)</span><span class="sxs-lookup"><span data-stu-id="41345-150">(Alternatively, you could select a certificate from your workspace or file system through hello **Workspace** or **FileSystem** buttons, respectively, but for purposes of this tutorial we'll create a new certificate.)</span></span>

   * <span data-ttu-id="41345-151">Hello에 **새 인증서** 대화 상자에서 지정 하 고 PFX 파일을 사용 하는 hello 암호를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="41345-151">In hello **New Certificate** dialog, specify and confirm hello password you'll use for your PFX file.</span></span>

   * <span data-ttu-id="41345-152">에 대해 제공 된 값과 hello 허용 **이름 (CN)**, 하거나 사용자 지정 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="41345-152">Accept hello value provided for **Name (CN)**, or use a custom name.</span></span>

   * <span data-ttu-id="41345-153">Hello 새 인증서를.cer 형식으로 저장 될 hello 경로 파일 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41345-153">Specify hello path and file name where hello new certificate, in .cer form, will be saved.</span></span> <span data-ttu-id="41345-154">이 단계와 hello 다음 단계에 대 한 hello를 사용할 수 있습니다 **cert** 수 있지만 Azure 프로젝트의 폴더는 무료 toochoose 다른 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="41345-154">For this step and hello next step, you could use hello **cert** folder of your Azure project, but you're free toochoose another location.</span></span> <span data-ttu-id="41345-155">이 자습서의 목적을 위해 **c:\mycert\mycert.cer**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41345-155">For purposes of this tutorial, we'll use **c:\mycert\mycert.cer**.</span></span> <span data-ttu-id="41345-156">(Hello 만들 **c:\mycert** 폴더 이전 tooproceeding 또는 원하는 경우 기존 폴더를 사용 합니다.)</span><span class="sxs-lookup"><span data-stu-id="41345-156">(Create hello **c:\mycert** folder prior tooproceeding, or use an existing folder if desired.)</span></span>

   * <span data-ttu-id="41345-157">Hello 새 인증서와 개인 키를.pfx 형식으로 저장할 수 hello 경로 파일 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41345-157">Specify hello path and file name where hello new certificate and its private key, in .pfx form, will be saved.</span></span> <span data-ttu-id="41345-158">이 자습서의 목적을 위해 **c:\mycert\mycert.pfx**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41345-158">For purposes of this tutorial, we'll use **c:\mycert\mycert.pfx**.</span></span> <span data-ttu-id="41345-159">프로그램 **새 인증서** 대화 비슷한 toohello 다음과 같아야 합니다. (사용 하지 않은 경우 hello 폴더 경로 업데이트 **c:\mycert**):</span><span class="sxs-lookup"><span data-stu-id="41345-159">Your **New Certificate** dialog should look similar toohello following (update hello folder paths if you did not use **c:\mycert**):</span></span>
     
      ![][ic712275]

   * <span data-ttu-id="41345-160">클릭 **확인** tooclose hello **새 인증서** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="41345-160">Click **OK** tooclose hello **New Certificate** dialog.</span></span>

8. <span data-ttu-id="41345-161">프로그램 **원격 액세스** 대화 비슷한 toohello 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41345-161">Your **Remote Access** dialog should look similar toohello following:</span></span></p>
   
   ![][ic719495]

9. <span data-ttu-id="41345-162">클릭 **확인** tooclose hello **원격 액세스** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="41345-162">Click **OK** tooclose hello **Remote Access** dialog.</span></span>

<span data-ttu-id="41345-163">응용 프로그램을 다시 작성, hello로 toocloud 배포에 대 한 집합을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="41345-163">Rebuild your application, with hello build set for deployment toocloud.</span></span>

## <a name="toolog-in-remotely"></a><span data-ttu-id="41345-164">toolog에 원격으로</span><span class="sxs-lookup"><span data-stu-id="41345-164">toolog in remotely</span></span>
<span data-ttu-id="41345-165">역할 인스턴스가 준비 되 면 원격 응용 프로그램을 호스팅하는 toohello 가상 컴퓨터에 로그온 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41345-165">Once your role instance is ready, you can remotely log in toohello virtual machine that is hosting your application.</span></span>

* <span data-ttu-id="41345-166">Windows 및 선택한 hello에서 Eclipse를 사용 하는 경우 **배포 시 원격 데스크톱 시작** 옵션 중에 배포 tooAzure 나타납니다 원격 데스크톱 연결 로그온 화면이 배포를 시작할 때입니다.</span><span class="sxs-lookup"><span data-stu-id="41345-166">If are using Eclipse on Windows and you selected hello **Start remote desktop on deploy** option during your deployment tooAzure, you will be presented with a Remote Desktop Connection logon screen when your deployment starts.</span></span> <span data-ttu-id="41345-167">Hello 사용자 이름 및 암호를 묻는 메시지가 나타나면 hello 원격 사용자에 대해 지정한 hello 값을 입력 하 고에 수 toolog 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41345-167">When you are prompted for hello user name and password, enter hello values that you specified for hello remote user and will be able toolog in.</span></span>

* <span data-ttu-id="41345-168">또 다른 방법은 toolog hello를 통해 원격으로 <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure 관리 포털</a>:</span><span class="sxs-lookup"><span data-stu-id="41345-168">Another way toolog in remotely is through hello <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:</span></span>
  
  * <span data-ttu-id="41345-169">Hello 내 **클라우드 서비스** hello Azure 관리 포털의 보기 클라우드 서비스를 클릭 하 고 **인스턴스**, 특정 인스턴스를 클릭 하 고 클릭 다음 hello **연결**단추입니다.</span><span class="sxs-lookup"><span data-stu-id="41345-169">Within hello **Cloud Services** view of hello Azure Management portal, click your cloud service, click **Instances**, click a specific instance, and then click hello **Connect** button.</span></span> <span data-ttu-id="41345-170">hello **연결** 단추가 hello 명령 모음에서 hello 다음과 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="41345-170">hello **Connect** button appears as hello following in hello command bar:</span></span>
    
      ![][ic659273]

  * <span data-ttu-id="41345-171">Hello를 클릭 한 후 **연결** 단추를 증명된 tooopen RDP 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41345-171">After clicking hello **Connect** button, you will be prompted tooopen an RDP file.</span></span> <span data-ttu-id="41345-172">Hello 파일을 열고 hello 프롬프트를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="41345-172">Open hello file and follow hello prompts.</span></span> <span data-ttu-id="41345-173">(있습니다 수이 파일 tooyour 로컬 컴퓨터를 저장할 수도 한 다음 hello 파일 두 번 클릭 하 여 tooremote 로그에서에서 실행 tooyour toofirst 필요 없이 가상 컴퓨터 이동 hello 관리 포털.)</span><span class="sxs-lookup"><span data-stu-id="41345-173">(You could also save this file tooyour local computer, and then run hello file by double-clicking it tooremote log in tooyour virtual machine without needing toofirst go hello management portal.)</span></span>

  * <span data-ttu-id="41345-174">Hello 사용자 이름 및 암호를 묻는 메시지가 나타나면 hello 원격 사용자에 대해 지정한 hello 값을 입력 하 고에 수 toolog 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41345-174">When you are prompted for hello user name and password, enter hello values that you specified for hello remote user and will be able toolog in.</span></span>

> [!NOTE]
> <span data-ttu-id="41345-175">Windows 이외의 운영 체제에 있는 toouse 운영 체제와 호환 되는 원격 데스크톱 클라이언트를 해야 hello 단계 tooconfigure hello 다운로드 한 RDP 파일의 hello 설정 사용 하 여 해당 클라이언트를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="41345-175">If you are on a non-Windows operating system, you need toouse a Remote Desktop client that is compatible with your operating system and follow hello steps tooconfigure that client with hello settings in hello RDP file that you downloaded.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="41345-176">참고 항목</span><span class="sxs-lookup"><span data-stu-id="41345-176">See Also</span></span>
<span data-ttu-id="41345-177">[Eclipse용 Azure 도구 키트][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="41345-177">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="41345-178">[Eclipse에서 Azure용 Hello World 응용 프로그램 만들기][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="41345-178">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="41345-179">[Hello Eclipse 용 Azure 도구 키트 설치][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="41345-179">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="41345-180">Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터][Azure Java Developer Center]합니다.</span><span class="sxs-lookup"><span data-stu-id="41345-180">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
