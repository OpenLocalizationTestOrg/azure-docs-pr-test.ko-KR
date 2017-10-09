---
title: "지원 패키지 aaaCreate StorSimple 8000 시리즈 | Microsoft Docs"
description: "Toocreate, 암호를 해독 하면 및 StorSimple 8000 시리즈 장치에 대 한 지원 패키지 편집 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 857555b6ba31b1527f8f00d19818ebbec6005d0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-support-package-for-storsimple-8000-series"></a><span data-ttu-id="8908c-103">StorSimple 8000 시리즈용 지원 패키지 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="8908c-103">Create and manage a support package for StorSimple 8000 series</span></span>

## <a name="overview"></a><span data-ttu-id="8908c-104">개요</span><span class="sxs-lookup"><span data-stu-id="8908c-104">Overview</span></span>

<span data-ttu-id="8908c-105">StorSimple 지원 패키지는 StorSimple 장치 문제 해결에 모든 관련 로그 tooassist Microsoft 기술 지원 서비스를 수집 하는 사용 하기 쉬운 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs tooassist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="8908c-106">hello 수집 된 로그 암호화 되 고 압축 합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-106">hello collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="8908c-107">이 자습서는 toocreate 단계별 지침을 포함 하 고 StorSimple 8000 시리즈 장치에 대 한 hello 지원 패키지를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-107">This tutorial includes step-by-step instructions toocreate and manage hello support package for your StorSimple 8000 series device.</span></span> <span data-ttu-id="8908c-108">StorSimple 가상 배열을 사용 하는 경우 너무 이동[로그 패키지를 생성할](storsimple-ova-web-ui-admin.md#generate-a-log-package)합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-108">If you are working with a StorSimple Virtual Array, go too[generate a log package](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="create-a-support-package"></a><span data-ttu-id="8908c-109">지원 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="8908c-109">Create a support package</span></span>

<span data-ttu-id="8908c-110">경우에 따라 해야 toomanually StorSimple 용 Windows PowerShell을 통해 hello 지원 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-110">In some cases, you'll need toomanually create hello support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="8908c-111">예:</span><span class="sxs-lookup"><span data-stu-id="8908c-111">For example:</span></span>

* <span data-ttu-id="8908c-112">로그에서 tooremove 중요 한 정보가 필요한 경우 Microsoft 지원에 이전 toosharing 파일.</span><span class="sxs-lookup"><span data-stu-id="8908c-112">If you need tooremove sensitive information from your log files prior toosharing with Microsoft Support.</span></span>
* <span data-ttu-id="8908c-113">Tooconnectivity 문제 인해 hello 패키지를 업로드 하는 데 어려움이 발생 하는 경우 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-113">If you are having difficulty uploading hello package due tooconnectivity issues.</span></span>

<span data-ttu-id="8908c-114">전자 메일을 통해 Microsoft 지원에 수동으로 생성된 지원 패키지를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-114">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="8908c-115">Hello StorSimple 용 Windows PowerShell에서 지원 패키지 단계 toocreate 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-115">Perform hello following steps toocreate a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="toocreate-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="8908c-116">StorSimple 용 Windows PowerShell에서 지원 패키지 toocreate</span><span class="sxs-lookup"><span data-stu-id="8908c-116">toocreate a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="8908c-117">가 tooconnect tooyour StorSimple 장치를 사용 하는 hello 원격 컴퓨터에서 관리자 권한으로 Windows PowerShell 세션 toostart hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-117">toostart a Windows PowerShell session as an administrator on hello remote computer that's used tooconnect tooyour StorSimple device, enter hello following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="8908c-118">Hello Windows PowerShell 세션에서 장치의 SSAdmin 콘솔 toohello 연결:</span><span class="sxs-lookup"><span data-stu-id="8908c-118">In hello Windows PowerShell session, connect toohello SSAdmin Console of your device:</span></span>
   
   1. <span data-ttu-id="8908c-119">Hello 명령 프롬프트에서 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-119">At hello command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   2. <span data-ttu-id="8908c-120">Hello 대화 상자가 열리면 장치 관리자 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-120">In hello dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="8908c-121">hello 기본 암호는 _Password1_합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-121">hello default password is _Password1_.</span></span>
     
      ![PowerShell 자격 증명 대화 상자](./media/storsimple-8000-create-manage-support-package/IC740962.png)
   3. <span data-ttu-id="8908c-123">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-123">Select **OK**.</span></span>
   4. <span data-ttu-id="8908c-124">Hello 명령 프롬프트에서 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-124">At hello command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="8908c-125">열린 hello 세션 hello 적절 한 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-125">In hello session that opens, enter hello appropriate command.</span></span>
   
   * <span data-ttu-id="8908c-126">암호로 보호된 네트워크 공유에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-126">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="8908c-127">메시지가 표시 됩니다는 암호, 경로 toohello 네트워크 공유 폴더 및 암호화의 암호를 (hello 지원 패키지가 암호화 되기) 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-127">You'll be prompted for a password, a path toohello network shared folder, and an encryption passphrase (because hello support package is encrypted).</span></span> <span data-ttu-id="8908c-128">그런 다음 지원 패키지 hello 지정 된 폴더에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-128">A support package is then created in hello specified folder.</span></span>
   * <span data-ttu-id="8908c-129">암호로 보호 되지 않은 공유에 대 한 불필요 hello `-Credential` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-129">For shares that are not password protected, you do not need hello `-Credential` parameter.</span></span> <span data-ttu-id="8908c-130">Hello 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-130">Enter hello following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="8908c-131">hello 지정 된 네트워크 공유 폴더에 있는 두 컨트롤러에 대 한 hello 지원 패키지가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-131">hello support package is created for both controllers in hello specified network shared folder.</span></span> <span data-ttu-id="8908c-132">문제 해결에 대 한 지원 tooMicrosoft 보낼 수 있는 암호화, 압축 된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-132">It's an encrypted, compressed file that can be sent tooMicrosoft Support for troubleshooting.</span></span> <span data-ttu-id="8908c-133">자세한 내용은 [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8908c-133">For more information, see [Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

### <a name="hello-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="8908c-134">hello Export-hcssupportpackage cmdlet 매개 변수</span><span class="sxs-lookup"><span data-stu-id="8908c-134">hello Export-HcsSupportPackage cmdlet parameters</span></span>

<span data-ttu-id="8908c-135">Hello hello Export-hcssupportpackage cmdlet과 함께 매개 변수 뒤에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-135">You can use hello following parameters with hello Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="8908c-136">매개 변수</span><span class="sxs-lookup"><span data-stu-id="8908c-136">Parameter</span></span> | <span data-ttu-id="8908c-137">필수/선택</span><span class="sxs-lookup"><span data-stu-id="8908c-137">Required/Optional</span></span> | <span data-ttu-id="8908c-138">설명</span><span class="sxs-lookup"><span data-stu-id="8908c-138">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="8908c-139">필수</span><span class="sxs-lookup"><span data-stu-id="8908c-139">Required</span></span> |<span data-ttu-id="8908c-140">지원 패키지가 배치 되는 hello hello 네트워크 공유 폴더의 tooprovide hello 위치를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-140">Use tooprovide hello location of hello network shared folder in which hello support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="8908c-141">필수</span><span class="sxs-lookup"><span data-stu-id="8908c-141">Required</span></span> |<span data-ttu-id="8908c-142">사용 하 여 tooprovide 암호 toohelp hello 지원 패키지를 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-142">Use tooprovide a passphrase toohelp encrypt hello support package.</span></span> |
| `-Credential` |<span data-ttu-id="8908c-143">옵션</span><span class="sxs-lookup"><span data-stu-id="8908c-143">Optional</span></span> |<span data-ttu-id="8908c-144">Hello 네트워크 공유 폴더에 대 한 toosupply 액세스 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-144">Use toosupply access credentials for hello network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="8908c-145">옵션</span><span class="sxs-lookup"><span data-stu-id="8908c-145">Optional</span></span> |<span data-ttu-id="8908c-146">Tooskip hello 암호화 암호 확인 단계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-146">Use tooskip hello encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="8908c-147">옵션</span><span class="sxs-lookup"><span data-stu-id="8908c-147">Optional</span></span> |<span data-ttu-id="8908c-148">Toospecify에서 디렉터리를 사용 *경로* 는 hello 지원 패키지가 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-148">Use toospecify a directory under *Path* in which hello support package is placed.</span></span> <span data-ttu-id="8908c-149">hello 기본값은 [장치 이름]-[현재 날짜 및 시간: yyyy-mm-dd-hh-mm-ss].</span><span class="sxs-lookup"><span data-stu-id="8908c-149">hello default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="8908c-150">옵션</span><span class="sxs-lookup"><span data-stu-id="8908c-150">Optional</span></span> |<span data-ttu-id="8908c-151">으로 지정 **클러스터** (기본값) toocreate 두 컨트롤러 모두에 대 한 지원 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-151">Specify as **Cluster** (default) toocreate a support package for both controllers.</span></span> <span data-ttu-id="8908c-152">현재 컨트롤러 hello에 대 한 패키지 toocreate 하려는 지정 **컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-152">If you want toocreate a package only for hello current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="8908c-153">지원 패키지 편집</span><span class="sxs-lookup"><span data-stu-id="8908c-153">Edit a support package</span></span>

<span data-ttu-id="8908c-154">지원 패키지를 생성 한 후에 tooedit hello 패키지 tooremove 중요 한 정보가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-154">After you have generated a support package, you might need tooedit hello package tooremove sensitive information.</span></span> <span data-ttu-id="8908c-155">이 볼륨 이름, 장치 IP 주소 및 hello 로그 파일에서 백업 이름에 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-155">This can include volume names, device IP addresses, and backup names from hello log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8908c-156">StorSimple용 Windows PowerShell을 통해 생성된 지원 패키지를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-156">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="8908c-157">Hello StorSimple 장치 관리자 서비스와 Azure 포털에서에서 만든 패키지를 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-157">You can't edit a package created in hello Azure portal with StorSimple Device Manager service.</span></span>

<span data-ttu-id="8908c-158">tooedit 지원 패키지 hello Microsoft 지원 사이트에 업로드 하기 전에 먼저 hello 지원 패키지 암호를 해독 hello 파일을 편집한 다음 다시 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-158">tooedit a support package before uploading it on hello Microsoft Support site, first decrypt hello support package, edit hello files, and then re-encrypt it.</span></span> <span data-ttu-id="8908c-159">Hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-159">Perform hello following steps.</span></span>

#### <a name="tooedit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="8908c-160">StorSimple 용 Windows PowerShell에서 지원 패키지 tooedit</span><span class="sxs-lookup"><span data-stu-id="8908c-160">tooedit a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="8908c-161">에 이전에 설명 된 대로 지원 패키지 생성 [toocreate StorSimple 용 Windows PowerShell에서 지원 패키지](#to-create-a-support-package-in-windows-powershell-for-storsimple)합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-161">Generate a support package as described earlier, in [toocreate a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="8908c-162">[Hello 스크립트 다운로드](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) 클라이언트에서 로컬로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-162">[Download hello script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="8908c-163">Hello Windows PowerShell 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-163">Import hello Windows PowerShell module.</span></span> <span data-ttu-id="8908c-164">Hello 경로 toohello 로컬 폴더를 다운로드 한 hello 스크립트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-164">Specify hello path toohello local folder in which you downloaded hello script.</span></span> <span data-ttu-id="8908c-165">tooimport hello 모듈 입력:</span><span class="sxs-lookup"><span data-stu-id="8908c-165">tooimport hello module, enter:</span></span>
   
    `Import-module <Path toohello folder that contains hello Windows PowerShell script>`
4. <span data-ttu-id="8908c-166">모든 hello 파일이 *.aes* 압축 및 암호화 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-166">All hello files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="8908c-167">toodecompress 및 암호 해독 파일을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-167">toodecompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    <span data-ttu-id="8908c-168">Note hello 실제 파일 확장명 모든 hello 파일에 대해 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-168">Note that hello actual file extensions are now displayed for all hello files.</span></span>
   
    ![지원 패키지 편집](./media/storsimple-8000-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="8908c-170">Hello 암호화의 암호에 대 한 메시지가 면 hello 지원 패키지를 만들 때 사용한 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-170">When you're prompted for hello encryption passphrase, enter hello passphrase that you used when hello support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for hello following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="8908c-171">Hello 로그 파일이 있는 toohello 폴더를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-171">Browse toohello folder that contains hello log files.</span></span> <span data-ttu-id="8908c-172">Hello 로그 파일은 이제 압축을 풀 고 암호 해독 하기 때문에 이러한 원래 파일 확장명 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-172">Because hello log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="8908c-173">이러한 파일 tooremove 볼륨 이름, 장치 IP 주소 등의 모든 고객 관련 정보를 수정 하 고 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-173">Modify these files tooremove any customer-specific information, such as volume names and device IP addresses, and save hello files.</span></span>
7. <span data-ttu-id="8908c-174">닫기 hello 파일 toocompress gzip을 사용 하 여 AES 256으로 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-174">Close hello files toocompress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="8908c-175">이 네트워크를 통해 hello 지원 패키지를 전송에서 보안 성능 및 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-175">This is for speed and security in transferring hello support package over a network.</span></span> <span data-ttu-id="8908c-176">toocompress 파일을 암호화 하 고 hello 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-176">toocompress and encrypt files, enter hello following:</span></span>
   
    `Close-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    ![지원 패키지 편집](./media/storsimple-8000-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="8908c-178">메시지가 표시 되 면 hello 수정 된 지원 패키지에 대 한 암호화의 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-178">When prompted, provide an encryption passphrase for hello modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for hello following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="8908c-179">Microsoft 기술 지원 요청 될 때와 공유할 수 있도록 hello 새 암호를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-179">Write down hello new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="8908c-180">예: 암호로 보호된 공유에 대한 지원 패키지에서 파일 편집</span><span class="sxs-lookup"><span data-stu-id="8908c-180">Example: Editing files in a support package on a password-protected share</span></span>

<span data-ttu-id="8908c-181">다음 예제는 hello toodecrypt, 편집 하 고 다시 지원 패키지를 암호화 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-181">hello following example shows how toodecrypt, edit, and re-encrypt a support package.</span></span>

        PS C:\WINDOWS\system32> Import-module C:\Users\Default\StorSimple\SupportPackage\HCSSupportPackageTools.psm1

        PS C:\WINDOWS\system32> Open-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Open-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32> Close-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Close-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32>

## <a name="next-steps"></a><span data-ttu-id="8908c-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8908c-182">Next steps</span></span>

* <span data-ttu-id="8908c-183">Hello에 대 한 자세한 내용은 [hello 지원 패키지에서 수집 된 정보](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span><span class="sxs-lookup"><span data-stu-id="8908c-183">Learn about hello [information collected in hello Support package](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span></span>
* <span data-ttu-id="8908c-184">너무 방법에 대해 알아봅니다[사용 하 여 지원 패키지 및 장치 tootroubleshoot 장치 배포를 기록](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting)합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-184">Learn how too[use support packages and device logs tootroubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="8908c-185">너무 방법에 대해 알아봅니다[사용 하 여 StorSimple 장치를 StorSimple 장치 관리자 서비스 tooadminister hello](storsimple-8000-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8908c-185">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

