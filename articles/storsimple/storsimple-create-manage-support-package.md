---
title: "StorSimple 지원 패키지 만들기 | Microsoft Docs"
description: "StorSimple 장치용 지원 패키지를 만들고, 암호 해독 및 편집하는 방법을 알아봅니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: eac76f5f-5db1-4c92-af8c-54053b91e66c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 32d20e7a8adcfc646c592213fe7395b87a93c985
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-a-storsimple-support-package"></a><span data-ttu-id="1e2c0-103">StorSimple 지원 패키지 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="1e2c0-103">Create and manage a StorSimple support package</span></span>
## <a name="overview"></a><span data-ttu-id="1e2c0-104">개요</span><span class="sxs-lookup"><span data-stu-id="1e2c0-104">Overview</span></span>
<span data-ttu-id="1e2c0-105">StorSimple 지원 패키지는 StorSimple 장치 문제를 해결하는 데 있어서 Microsoft 지원을 지원하기 위해 모든 관련 로그를 수집하는 사용하기 쉬운 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs to assist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="1e2c0-106">수집된 로그는 암호화되고 압축됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-106">The collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="1e2c0-107">이 자습서는 지원 패키지를 만들고 관리하도록 단계별 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-107">This tutorial includes step-by-step instructions to create and manage the support package.</span></span>

## <a name="create-and-upload-a-support-package-in-the-azure-classic-portal"></a><span data-ttu-id="1e2c0-108">Azure 클래식 포털에서 지원 패키지 만들기 및 업로드</span><span class="sxs-lookup"><span data-stu-id="1e2c0-108">Create and upload a support package in the Azure classic portal</span></span>
<span data-ttu-id="1e2c0-109">Azure 클래식 포털에서 서비스의 **유지 관리** 페이지를 통해 Microsoft 지원 사이트에 지원 패키지를 만들고 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-109">You can create and upload a support package to the Microsoft Support site through the **Maintenance** page of the service in the Azure classic portal.</span></span>

> [!NOTE]
> <span data-ttu-id="1e2c0-110">업로드하려면 지원 암호가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-110">The upload requires a support passkey.</span></span> <span data-ttu-id="1e2c0-111">지원 엔지니어는 암호를 전자 메일로 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-111">Your support engineer should provide this to you in an email.</span></span>
> 
> 

<span data-ttu-id="1e2c0-112">암호화되고 압축된 지원 패키지(.cab 파일)를 만들고 지원 사이트에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-112">An encrypted and compressed support package (.cab file) is created and uploaded to the Support site.</span></span> <span data-ttu-id="1e2c0-113">그런 다음 지원 엔지니어는 문제를 해결하기 위한 지원 사이트에서 이 패키지를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-113">The support engineer can then retrieve this package from the Support site for troubleshooting the issue.</span></span>

<span data-ttu-id="1e2c0-114">지원 패키지를 만들려면 클래식 포털에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-114">Perform the following steps in the classic portal to create a support package.</span></span>

#### <a name="to-create-a-support-package-in-the-azure-classic-portal"></a><span data-ttu-id="1e2c0-115">Azure 클래식 포털에서 지원 패키지를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="1e2c0-115">To create a support package in the Azure classic portal</span></span>
1. <span data-ttu-id="1e2c0-116">**장치** > **유지 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-116">Select **Devices** > **Maintenance**.</span></span>
2. <span data-ttu-id="1e2c0-117">**지원 패키지** 섹션에서 **지원 패키지 만들기 및 업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-117">In the **Support package** section, select **Create and upload support package**.</span></span>
3. <span data-ttu-id="1e2c0-118">**지원 패키지 만들기 및 업로드** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-118">In the **Create and upload support package** dialog box, do the following:</span></span>
   
    ![지원 패키지 만들기](./media/storsimple-create-manage-support-package/IC740923.png)
   
   * <span data-ttu-id="1e2c0-120">**지원 암호** 텍스트 상자에 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-120">In the **Support Passkey** text box, enter the passkey.</span></span> <span data-ttu-id="1e2c0-121">Microsoft 지원 엔지니어가 전자 메일로 이 암호를 전송해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-121">Your Microsoft support engineer should send this passkey to you in email.</span></span>
   * <span data-ttu-id="1e2c0-122">동의를 제공하는 확인란을 선택하여 Microsoft 지원 사이트에 지원 패키지를 자동으로 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-122">Select the check box to provide consent to automatically upload the support package to the Microsoft Support site.</span></span>
   * <span data-ttu-id="1e2c0-123">확인 아이콘</span><span class="sxs-lookup"><span data-stu-id="1e2c0-123">Click the check icon</span></span> ![확인 아이콘](./media/storsimple-create-manage-support-package/IC740895.png)<span data-ttu-id="1e2c0-125">를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-125">.</span></span>

## <a name="manually-create-a-support-package"></a><span data-ttu-id="1e2c0-126">수동으로 지원 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="1e2c0-126">Manually create a support package</span></span>
<span data-ttu-id="1e2c0-127">경우에 따라 StorSimple 용 Windows PowerShell을 통해 지원 패키지를 수동으로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-127">In some cases, you'll need to manually create the support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="1e2c0-128">예:</span><span class="sxs-lookup"><span data-stu-id="1e2c0-128">For example:</span></span>

* <span data-ttu-id="1e2c0-129">Microsoft 지원과 공유하기 전에 로그 파일에서 중요한 정보를 제거해야 하는 경우</span><span class="sxs-lookup"><span data-stu-id="1e2c0-129">If you need to remove sensitive information from your log files prior to sharing with Microsoft Support.</span></span>
* <span data-ttu-id="1e2c0-130">연결 문제로 인해 패키지를 업로드하는 데 문제가 발생하는 경우</span><span class="sxs-lookup"><span data-stu-id="1e2c0-130">If you are having difficulty uploading the package due to connectivity issues.</span></span>

<span data-ttu-id="1e2c0-131">전자 메일을 통해 Microsoft 지원에 수동으로 생성된 지원 패키지를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-131">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="1e2c0-132">StorSimple용 Windows PowerShell에서 지원 패키지를 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-132">Perform the following steps to create a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="to-create-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="1e2c0-133">StorSimple용 Windows PowerShell에서 지원 패키지를 만들려면</span><span class="sxs-lookup"><span data-stu-id="1e2c0-133">To create a support package in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="1e2c0-134">StorSimple 장치에 연결하는데 사용된 원격 컴퓨터에서 관리자 권한으로 Windows PowerShell 세션을 시작하려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-134">To start a Windows PowerShell session as an administrator on the remote computer that's used to connect to your StorSimple device, enter the following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="1e2c0-135">Windows PowerShell 세션에서 장치의 SSAdmin 콘솔에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-135">In the Windows PowerShell session, connect to the SSAdmin Console of your device:</span></span>
   
   * <span data-ttu-id="1e2c0-136">명령 프롬프트에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-136">At the command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   * <span data-ttu-id="1e2c0-137">열린 대화 상자에서 장치 관리자 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-137">In the dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="1e2c0-138">기본 암호는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-138">The default password is:</span></span>
     
      `Password1`
     
      ![PowerShell 자격 증명 대화 상자](./media/storsimple-create-manage-support-package/IC740962.png)
   * <span data-ttu-id="1e2c0-140">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-140">Select **OK**.</span></span>
   * <span data-ttu-id="1e2c0-141">명령 프롬프트에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-141">At the command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="1e2c0-142">열린 세션에서 적절한 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-142">In the session that opens, enter the appropriate command.</span></span>
   
   * <span data-ttu-id="1e2c0-143">암호로 보호된 네트워크 공유에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-143">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="1e2c0-144">암호, 네트워크 공유 폴더의 경로 및 암호화 암호에 대해 묻는 메시지가 나타납니다.(지원 패키지가 암호화 되었기 때문)</span><span class="sxs-lookup"><span data-stu-id="1e2c0-144">You'll be prompted for a password, a path to the network shared folder, and an encryption passphrase (because the support package is encrypted).</span></span> <span data-ttu-id="1e2c0-145">그런 다음 지원 패키지는 지정된 폴더에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-145">A support package is then created in the specified folder.</span></span>
   * <span data-ttu-id="1e2c0-146">암호로 보호되지 않은 공유의 경우 `-Credential` 매개 변수가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-146">For shares that are not password protected, you do not need the `-Credential` parameter.</span></span> <span data-ttu-id="1e2c0-147">다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-147">Enter the following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="1e2c0-148">지정된 네트워크 공유 폴더에 두 컨트롤러를 위한 지원 패키지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-148">The support package is created for both controllers in the specified network shared folder.</span></span> <span data-ttu-id="1e2c0-149">문제해결을 위한 Microsoft 기술 지원 서비스에 보낼 수 있는 암호화되고 압축된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-149">It's an encrypted, compressed file that can be sent to Microsoft Support for troubleshooting.</span></span> <span data-ttu-id="1e2c0-150">자세한 내용은 [Microsoft 지원에 문의](storsimple-contact-microsoft-support.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-150">For more information, see [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

### <a name="the-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="1e2c0-151">Export-HcsSupportPackage cmdlet 매개 변수</span><span class="sxs-lookup"><span data-stu-id="1e2c0-151">The Export-HcsSupportPackage cmdlet parameters</span></span>
<span data-ttu-id="1e2c0-152">Export-HcsSupportPackage cmdlet으로 다음 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-152">You can use the following parameters with the Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="1e2c0-153">매개 변수</span><span class="sxs-lookup"><span data-stu-id="1e2c0-153">Parameter</span></span> | <span data-ttu-id="1e2c0-154">필수/선택</span><span class="sxs-lookup"><span data-stu-id="1e2c0-154">Required/Optional</span></span> | <span data-ttu-id="1e2c0-155">설명</span><span class="sxs-lookup"><span data-stu-id="1e2c0-155">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="1e2c0-156">필수</span><span class="sxs-lookup"><span data-stu-id="1e2c0-156">Required</span></span> |<span data-ttu-id="1e2c0-157">지원 패키지가 배치된 네트워크 공유 폴더의 위치를 제공하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-157">Use to provide the location of the network shared folder in which the support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="1e2c0-158">필수</span><span class="sxs-lookup"><span data-stu-id="1e2c0-158">Required</span></span> |<span data-ttu-id="1e2c0-159">지원 패키지를 암호화하기 위해 암호를 제공하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-159">Use to provide a passphrase to help encrypt the support package.</span></span> |
| `-Credential` |<span data-ttu-id="1e2c0-160">옵션</span><span class="sxs-lookup"><span data-stu-id="1e2c0-160">Optional</span></span> |<span data-ttu-id="1e2c0-161">네트워크 공유 폴더에 대한 액세스 자격 증명을 제공하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-161">Use to supply access credentials for the network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="1e2c0-162">옵션</span><span class="sxs-lookup"><span data-stu-id="1e2c0-162">Optional</span></span> |<span data-ttu-id="1e2c0-163">암호화 암호 확인 단계를 건너뛰는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-163">Use to skip the encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="1e2c0-164">옵션</span><span class="sxs-lookup"><span data-stu-id="1e2c0-164">Optional</span></span> |<span data-ttu-id="1e2c0-165">지원 패키지가 배치된 *경로* 의 디렉터리를 지정하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-165">Use to specify a directory under *Path* in which the support package is placed.</span></span> <span data-ttu-id="1e2c0-166">기본값은 [장치 이름]-[현재 날짜 및 시간: yyyy-MM-dd-HH-mm-ss]입니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-166">The default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="1e2c0-167">옵션</span><span class="sxs-lookup"><span data-stu-id="1e2c0-167">Optional</span></span> |<span data-ttu-id="1e2c0-168">**클러스터** (기본값)로 지정하여 두 컨트롤러에 대한 지원 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-168">Specify as **Cluster** (default) to create a support package for both controllers.</span></span> <span data-ttu-id="1e2c0-169">현재 컨트롤러에 대해서만 패키지를 만들려면 **컨트롤러**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-169">If you want to create a package only for the current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="1e2c0-170">지원 패키지 편집</span><span class="sxs-lookup"><span data-stu-id="1e2c0-170">Edit a support package</span></span>
<span data-ttu-id="1e2c0-171">지원 패키지를 생성한 후에 패키지를 편집하여 중요한 정보를 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-171">After you have generated a support package, you might need to edit the package to remove sensitive information.</span></span> <span data-ttu-id="1e2c0-172">볼륨 이름, 장치 IP 주소 및 로그 파일에서 백업 이름을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-172">This can include volume names, device IP addresses, and backup names from the log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1e2c0-173">StorSimple용 Windows PowerShell을 통해 생성된 지원 패키지를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-173">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="1e2c0-174">StorSimple Manager 서비스로 Azure 클래식 포털에서 생성한 패키지를 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-174">You can't edit a package created in the Azure classic portal with StorSimple Manager service.</span></span>
> 
> 

<span data-ttu-id="1e2c0-175">Microsoft 지원 사이트에 업로드하기 전에 지원 패키지를 편집하려면 먼저 지원 패키지의 암호를 해독하고 파일을 편집한 다음 다시 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-175">To edit a support package before uploading it on the Microsoft Support site, first decrypt the support package, edit the files, and then re-encrypt it.</span></span> <span data-ttu-id="1e2c0-176">다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-176">Perform the following steps.</span></span>

#### <a name="to-edit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="1e2c0-177">StorSimple용 Windows PowerShell에서 지원 패키지를 편집하려면</span><span class="sxs-lookup"><span data-stu-id="1e2c0-177">To edit a support package in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="1e2c0-178">이전에 [StorSimple용 Windows PowerShell에서 지원 패키지 만들기](#to-create-a-support-package-in-windows-powershell-for-storsimple)에서 설명한 대로 지원 패키지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-178">Generate a support package as described earlier, in [To create a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="1e2c0-179">[스크립트](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) 를 로컬로 클라이언트에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-179">[Download the script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="1e2c0-180">Windows PowerShell 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-180">Import the Windows PowerShell module.</span></span> <span data-ttu-id="1e2c0-181">스크립트를 다운로드한 로컬 폴더로 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-181">Specify the path to the local folder in which you downloaded the script.</span></span> <span data-ttu-id="1e2c0-182">모듈을 가져오려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-182">To import the module, enter:</span></span>
   
    `Import-module <Path to the folder that contains the Windows PowerShell script>`
4. <span data-ttu-id="1e2c0-183">모든 파일은 압축 및 암호화된 *.aes* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-183">All the files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="1e2c0-184">압축을 해제하고 파일의 암호를 해독하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-184">To decompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path to the folder that contains support package files>`
   
    <span data-ttu-id="1e2c0-185">실제 파일 확장명은 모든 파일에서 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-185">Note that the actual file extensions are now displayed for all the files.</span></span>
   
    ![지원 패키지 편집](./media/storsimple-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="1e2c0-187">암호화 암호에 대한 메시지가 표시 되는 경우 지원 패키지를 만들 때 사용한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-187">When you're prompted for the encryption passphrase, enter the passphrase that you used when the support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for the following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="1e2c0-188">로그 파일이 들어 있는 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-188">Browse to the folder that contains the log files.</span></span> <span data-ttu-id="1e2c0-189">이제 로그 파일의 압축을 해제하고 암호를 해독했기 때문에 원본 파일 확장명을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-189">Because the log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="1e2c0-190">이러한 파일을 수정하여 볼륨 이름 및 장치 IP 주소와 같은 고객 관련 정보를 제거하고 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-190">Modify these files to remove any customer-specific information, such as volume names and device IP addresses, and save the files.</span></span>
7. <span data-ttu-id="1e2c0-191">파일을 닫아서 Gzip으로 압축한 다음 AES-256으로 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-191">Close the files to compress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="1e2c0-192">네트워크를 통해 지원 패키지를 전송하는 경우 보안 및 속도를 위해서 이렇게 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-192">This is for speed and security in transferring the support package over a network.</span></span> <span data-ttu-id="1e2c0-193">파일을 압축하고 암호화하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-193">To compress and encrypt files, enter the following:</span></span>
   
    `Close-HcsSupportPackage <Path to the folder that contains support package files>`
   
    ![지원 패키지 편집](./media/storsimple-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="1e2c0-195">메시지가 표시되면 수정된 지원 패키지에 암호화 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-195">When prompted, provide an encryption passphrase for the modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for the following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="1e2c0-196">Microsoft 지원 요청 시 공유할 수 있도록 새 암호를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-196">Write down the new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="1e2c0-197">예: 암호로 보호된 공유에 대한 지원 패키지에서 파일 편집</span><span class="sxs-lookup"><span data-stu-id="1e2c0-197">Example: Editing files in a support package on a password-protected share</span></span>
<span data-ttu-id="1e2c0-198">다음 예제에서는 지원 패키지의 암호를 해독하고 편집 및 다시 암호화하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-198">The following example shows how to decrypt, edit, and re-encrypt a support package.</span></span>

        PS C:\WINDOWS\system32> Import-module C:\Users\Default\StorSimple\SupportPackage\HCSSupportPackageTools.psm1

        PS C:\WINDOWS\system32> Open-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Open-HcsSupportPackage at command pipeline position 1

        Supply values for the following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32> Close-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Close-HcsSupportPackage at command pipeline position 1

        Supply values for the following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32>

## <a name="next-steps"></a><span data-ttu-id="1e2c0-199">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1e2c0-199">Next steps</span></span>
* <span data-ttu-id="1e2c0-200">[지원 패키지 및 장치 로그를 사용하여 장치 배포 문제를 해결](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-200">Learn how to [use support packages and device logs to troubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="1e2c0-201">[StorSimple Manager 서비스를 사용하여 StorSimple 장치를 관리](storsimple-manager-service-administration.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1e2c0-201">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

