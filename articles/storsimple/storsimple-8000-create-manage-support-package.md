---
title: "StorSimple 8000 시리즈 지원 패키지 만들기 | Microsoft Docs"
description: "StorSimple 8000 시리즈 장치용 지원 패키지를 만들고, 암호 해독 및 편집하는 방법을 알아봅니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 92abbb96b2117e10800de61b5c405a784453265b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-a-support-package-for-storsimple-8000-series"></a><span data-ttu-id="52535-103">StorSimple 8000 시리즈용 지원 패키지 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="52535-103">Create and manage a support package for StorSimple 8000 series</span></span>

## <a name="overview"></a><span data-ttu-id="52535-104">개요</span><span class="sxs-lookup"><span data-stu-id="52535-104">Overview</span></span>

<span data-ttu-id="52535-105">StorSimple 지원 패키지는 StorSimple 장치 문제를 해결하는 데 있어서 Microsoft 지원을 지원하기 위해 모든 관련 로그를 수집하는 사용하기 쉬운 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="52535-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs to assist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="52535-106">수집된 로그는 암호화되고 압축됩니다.</span><span class="sxs-lookup"><span data-stu-id="52535-106">The collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="52535-107">이 자습서는 StorSimple 8000 시리즈 장치에 대한 지원 패키지를 만들고 관리하도록 단계별 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-107">This tutorial includes step-by-step instructions to create and manage the support package for your StorSimple 8000 series device.</span></span> <span data-ttu-id="52535-108">StorSimple 가상 배열을 사용하는 경우 [로그 패키지 생성](storsimple-ova-web-ui-admin.md#generate-a-log-package)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-108">If you are working with a StorSimple Virtual Array, go to [generate a log package](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="create-a-support-package"></a><span data-ttu-id="52535-109">지원 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="52535-109">Create a support package</span></span>

<span data-ttu-id="52535-110">경우에 따라 StorSimple 용 Windows PowerShell을 통해 지원 패키지를 수동으로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-110">In some cases, you'll need to manually create the support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="52535-111">예:</span><span class="sxs-lookup"><span data-stu-id="52535-111">For example:</span></span>

* <span data-ttu-id="52535-112">Microsoft 지원과 공유하기 전에 로그 파일에서 중요한 정보를 제거해야 하는 경우</span><span class="sxs-lookup"><span data-stu-id="52535-112">If you need to remove sensitive information from your log files prior to sharing with Microsoft Support.</span></span>
* <span data-ttu-id="52535-113">연결 문제로 인해 패키지를 업로드하는 데 문제가 발생하는 경우</span><span class="sxs-lookup"><span data-stu-id="52535-113">If you are having difficulty uploading the package due to connectivity issues.</span></span>

<span data-ttu-id="52535-114">전자 메일을 통해 Microsoft 지원에 수동으로 생성된 지원 패키지를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52535-114">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="52535-115">StorSimple용 Windows PowerShell에서 지원 패키지를 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-115">Perform the following steps to create a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="to-create-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="52535-116">StorSimple용 Windows PowerShell에서 지원 패키지를 만들려면</span><span class="sxs-lookup"><span data-stu-id="52535-116">To create a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="52535-117">StorSimple 장치에 연결하는데 사용된 원격 컴퓨터에서 관리자 권한으로 Windows PowerShell 세션을 시작하려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-117">To start a Windows PowerShell session as an administrator on the remote computer that's used to connect to your StorSimple device, enter the following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="52535-118">Windows PowerShell 세션에서 장치의 SSAdmin 콘솔에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-118">In the Windows PowerShell session, connect to the SSAdmin Console of your device:</span></span>
   
   1. <span data-ttu-id="52535-119">명령 프롬프트에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-119">At the command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   2. <span data-ttu-id="52535-120">열린 대화 상자에서 장치 관리자 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-120">In the dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="52535-121">기본 암호는 _Password1_입니다.</span><span class="sxs-lookup"><span data-stu-id="52535-121">The default password is _Password1_.</span></span>
     
      ![PowerShell 자격 증명 대화 상자](./media/storsimple-8000-create-manage-support-package/IC740962.png)
   3. <span data-ttu-id="52535-123">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-123">Select **OK**.</span></span>
   4. <span data-ttu-id="52535-124">명령 프롬프트에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-124">At the command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="52535-125">열린 세션에서 적절한 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-125">In the session that opens, enter the appropriate command.</span></span>
   
   * <span data-ttu-id="52535-126">암호로 보호된 네트워크 공유에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-126">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="52535-127">암호, 네트워크 공유 폴더의 경로 및 암호화 암호에 대해 묻는 메시지가 나타납니다.(지원 패키지가 암호화 되었기 때문)</span><span class="sxs-lookup"><span data-stu-id="52535-127">You'll be prompted for a password, a path to the network shared folder, and an encryption passphrase (because the support package is encrypted).</span></span> <span data-ttu-id="52535-128">그런 다음 지원 패키지는 지정된 폴더에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="52535-128">A support package is then created in the specified folder.</span></span>
   * <span data-ttu-id="52535-129">암호로 보호되지 않은 공유의 경우 `-Credential` 매개 변수가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="52535-129">For shares that are not password protected, you do not need the `-Credential` parameter.</span></span> <span data-ttu-id="52535-130">다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-130">Enter the following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="52535-131">지정된 네트워크 공유 폴더에 두 컨트롤러를 위한 지원 패키지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52535-131">The support package is created for both controllers in the specified network shared folder.</span></span> <span data-ttu-id="52535-132">문제해결을 위한 Microsoft 기술 지원 서비스에 보낼 수 있는 암호화되고 압축된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="52535-132">It's an encrypted, compressed file that can be sent to Microsoft Support for troubleshooting.</span></span> <span data-ttu-id="52535-133">자세한 내용은 [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="52535-133">For more information, see [Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

### <a name="the-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="52535-134">Export-HcsSupportPackage cmdlet 매개 변수</span><span class="sxs-lookup"><span data-stu-id="52535-134">The Export-HcsSupportPackage cmdlet parameters</span></span>

<span data-ttu-id="52535-135">Export-HcsSupportPackage cmdlet으로 다음 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52535-135">You can use the following parameters with the Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="52535-136">매개 변수</span><span class="sxs-lookup"><span data-stu-id="52535-136">Parameter</span></span> | <span data-ttu-id="52535-137">필수/선택</span><span class="sxs-lookup"><span data-stu-id="52535-137">Required/Optional</span></span> | <span data-ttu-id="52535-138">설명</span><span class="sxs-lookup"><span data-stu-id="52535-138">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="52535-139">필수</span><span class="sxs-lookup"><span data-stu-id="52535-139">Required</span></span> |<span data-ttu-id="52535-140">지원 패키지가 배치된 네트워크 공유 폴더의 위치를 제공하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-140">Use to provide the location of the network shared folder in which the support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="52535-141">필수</span><span class="sxs-lookup"><span data-stu-id="52535-141">Required</span></span> |<span data-ttu-id="52535-142">지원 패키지를 암호화하기 위해 암호를 제공하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-142">Use to provide a passphrase to help encrypt the support package.</span></span> |
| `-Credential` |<span data-ttu-id="52535-143">옵션</span><span class="sxs-lookup"><span data-stu-id="52535-143">Optional</span></span> |<span data-ttu-id="52535-144">네트워크 공유 폴더에 대한 액세스 자격 증명을 제공하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-144">Use to supply access credentials for the network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="52535-145">옵션</span><span class="sxs-lookup"><span data-stu-id="52535-145">Optional</span></span> |<span data-ttu-id="52535-146">암호화 암호 확인 단계를 건너뛰는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-146">Use to skip the encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="52535-147">옵션</span><span class="sxs-lookup"><span data-stu-id="52535-147">Optional</span></span> |<span data-ttu-id="52535-148">지원 패키지가 배치된 *경로* 의 디렉터리를 지정하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-148">Use to specify a directory under *Path* in which the support package is placed.</span></span> <span data-ttu-id="52535-149">기본값은 [장치 이름]-[현재 날짜 및 시간: yyyy-MM-dd-HH-mm-ss]입니다.</span><span class="sxs-lookup"><span data-stu-id="52535-149">The default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="52535-150">옵션</span><span class="sxs-lookup"><span data-stu-id="52535-150">Optional</span></span> |<span data-ttu-id="52535-151">**클러스터** (기본값)로 지정하여 두 컨트롤러에 대한 지원 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52535-151">Specify as **Cluster** (default) to create a support package for both controllers.</span></span> <span data-ttu-id="52535-152">현재 컨트롤러에 대해서만 패키지를 만들려면 **컨트롤러**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-152">If you want to create a package only for the current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="52535-153">지원 패키지 편집</span><span class="sxs-lookup"><span data-stu-id="52535-153">Edit a support package</span></span>

<span data-ttu-id="52535-154">지원 패키지를 생성한 후에 패키지를 편집하여 중요한 정보를 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-154">After you have generated a support package, you might need to edit the package to remove sensitive information.</span></span> <span data-ttu-id="52535-155">볼륨 이름, 장치 IP 주소 및 로그 파일에서 백업 이름을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52535-155">This can include volume names, device IP addresses, and backup names from the log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="52535-156">StorSimple용 Windows PowerShell을 통해 생성된 지원 패키지를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52535-156">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="52535-157">StorSimple 장치 관리자 서비스로 Azure Portal에서 생성한 패키지를 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="52535-157">You can't edit a package created in the Azure portal with StorSimple Device Manager service.</span></span>

<span data-ttu-id="52535-158">Microsoft 지원 사이트에 업로드하기 전에 지원 패키지를 편집하려면 먼저 지원 패키지의 암호를 해독하고 파일을 편집한 다음 다시 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-158">To edit a support package before uploading it on the Microsoft Support site, first decrypt the support package, edit the files, and then re-encrypt it.</span></span> <span data-ttu-id="52535-159">다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-159">Perform the following steps.</span></span>

#### <a name="to-edit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="52535-160">StorSimple용 Windows PowerShell에서 지원 패키지를 편집하려면</span><span class="sxs-lookup"><span data-stu-id="52535-160">To edit a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="52535-161">이전에 [StorSimple용 Windows PowerShell에서 지원 패키지 만들기](#to-create-a-support-package-in-windows-powershell-for-storsimple)에서 설명한 대로 지원 패키지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-161">Generate a support package as described earlier, in [To create a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="52535-162">[스크립트](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) 를 로컬로 클라이언트에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-162">[Download the script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="52535-163">Windows PowerShell 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="52535-163">Import the Windows PowerShell module.</span></span> <span data-ttu-id="52535-164">스크립트를 다운로드한 로컬 폴더로 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-164">Specify the path to the local folder in which you downloaded the script.</span></span> <span data-ttu-id="52535-165">모듈을 가져오려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-165">To import the module, enter:</span></span>
   
    `Import-module <Path to the folder that contains the Windows PowerShell script>`
4. <span data-ttu-id="52535-166">모든 파일은 압축 및 암호화된 *.aes* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="52535-166">All the files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="52535-167">압축을 해제하고 파일의 암호를 해독하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-167">To decompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path to the folder that contains support package files>`
   
    <span data-ttu-id="52535-168">실제 파일 확장명은 모든 파일에서 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="52535-168">Note that the actual file extensions are now displayed for all the files.</span></span>
   
    ![지원 패키지 편집](./media/storsimple-8000-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="52535-170">암호화 암호에 대한 메시지가 표시 되는 경우 지원 패키지를 만들 때 사용한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-170">When you're prompted for the encryption passphrase, enter the passphrase that you used when the support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for the following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="52535-171">로그 파일이 들어 있는 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-171">Browse to the folder that contains the log files.</span></span> <span data-ttu-id="52535-172">이제 로그 파일의 압축을 해제하고 암호를 해독했기 때문에 원본 파일 확장명을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52535-172">Because the log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="52535-173">이러한 파일을 수정하여 볼륨 이름 및 장치 IP 주소와 같은 고객 관련 정보를 제거하고 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-173">Modify these files to remove any customer-specific information, such as volume names and device IP addresses, and save the files.</span></span>
7. <span data-ttu-id="52535-174">파일을 닫아서 Gzip으로 압축한 다음 AES-256으로 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-174">Close the files to compress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="52535-175">네트워크를 통해 지원 패키지를 전송하는 경우 보안 및 속도를 위해서 이렇게 합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-175">This is for speed and security in transferring the support package over a network.</span></span> <span data-ttu-id="52535-176">파일을 압축하고 암호화하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-176">To compress and encrypt files, enter the following:</span></span>
   
    `Close-HcsSupportPackage <Path to the folder that contains support package files>`
   
    ![지원 패키지 편집](./media/storsimple-8000-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="52535-178">메시지가 표시되면 수정된 지원 패키지에 암호화 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="52535-178">When prompted, provide an encryption passphrase for the modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for the following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="52535-179">Microsoft 지원 요청 시 공유할 수 있도록 새 암호를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="52535-179">Write down the new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="52535-180">예: 암호로 보호된 공유에 대한 지원 패키지에서 파일 편집</span><span class="sxs-lookup"><span data-stu-id="52535-180">Example: Editing files in a support package on a password-protected share</span></span>

<span data-ttu-id="52535-181">다음 예제에서는 지원 패키지의 암호를 해독하고 편집 및 다시 암호화하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="52535-181">The following example shows how to decrypt, edit, and re-encrypt a support package.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="52535-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="52535-182">Next steps</span></span>

* <span data-ttu-id="52535-183">[지원 패키지에서 수집된 정보](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="52535-183">Learn about the [information collected in the Support package](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span></span>
* <span data-ttu-id="52535-184">[지원 패키지 및 장치 로그를 사용하여 장치 배포 문제를 해결](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="52535-184">Learn how to [use support packages and device logs to troubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="52535-185">[StorSimple 장치 관리자 서비스를 사용하여 StorSimple 장치를 관리](storsimple-8000-manager-service-administration.md)하는 방법에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="52535-185">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

