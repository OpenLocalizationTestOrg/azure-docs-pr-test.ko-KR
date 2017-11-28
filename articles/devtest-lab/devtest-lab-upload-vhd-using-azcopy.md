---
title: "VHD aaaUpload tooAzure DevTest Labs AzCopy를 사용 하 여 파일 | Microsoft Docs"
description: "AzCopy를 사용 하 여 VHD 파일 toolab 저장소 계정에 업로드"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 14f9e933b0bd27451f6bcb94841ecc381213e578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-azcopy"></a><span data-ttu-id="9abf4-103">AzCopy를 사용 하 여 VHD 파일 toolab 저장소 계정에 업로드</span><span class="sxs-lookup"><span data-stu-id="9abf4-103">Upload VHD file toolab's storage account using AzCopy</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="9abf4-104">Azure DevTest Labs, VHD 파일 tooprovision 사용 되는 가상 컴퓨터는 사용자 지정 이미지를 사용 하는 toocreate 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9abf4-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="9abf4-105">단계를 수행 하는 hello에 관한 AzCopy 명령줄 유틸리티 tooupload hello를 사용 하 여 VHD 파일 tooa lab의 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="9abf4-105">hello following steps walk you through using hello AzCopy command-line utility tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="9abf4-106">VHD 파일을 업로드 한 후 hello [다음 단계 섹션](#next-steps) toocreate hello에서 사용자 지정 이미지를 VHD 파일을 업로드 하는 방법을 보여 주는 몇 가지 기사를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="9abf4-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="9abf4-107">Azure의 디스크 및 VHD에 대한 자세한 내용은 [가상 컴퓨터용 디스크 및 VHD 정보](../virtual-machines/linux/about-disks-and-vhds.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9abf4-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

> [!NOTE] 
>  
> <span data-ttu-id="9abf4-108">AzCopy는 Windows 전용 명령줄 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="9abf4-108">AzCopy is a Windows-only command-line utility.</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="9abf4-109">단계별 지침</span><span class="sxs-lookup"><span data-stu-id="9abf4-109">Step-by-step instructions</span></span>

<span data-ttu-id="9abf4-110">다음 단계 워크 tooAzure DevTest Labs를 사용 하 여 파일을 VHD를 업로드 하는 과정를 hello [AzCopy](http://aka.ms/downloadazcopy)합니다.</span><span class="sxs-lookup"><span data-stu-id="9abf4-110">hello following steps walk you through uploading a VHD file tooAzure DevTest Labs using [AzCopy](http://aka.ms/downloadazcopy).</span></span> 

1. <span data-ttu-id="9abf4-111">Hello hello 랩 저장소 계정의 이름으로 hello Azure 포털을 사용 하 여 가져오기:</span><span class="sxs-lookup"><span data-stu-id="9abf4-111">Get hello name of hello lab's storage account using hello Azure portal:</span></span>

1. <span data-ttu-id="9abf4-112">Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.</span><span class="sxs-lookup"><span data-stu-id="9abf4-112">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="9abf4-113">선택 **더 많은 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9abf4-113">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="9abf4-114">랩의 hello 목록에서 원하는 랩 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9abf4-114">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="9abf4-115">Hello 랩 블레이드에서 선택 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="9abf4-115">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="9abf4-116">Hello 랩에 **구성** 블레이드를 **사용자 지정 이미지 (Vhd)**합니다.</span><span class="sxs-lookup"><span data-stu-id="9abf4-116">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="9abf4-117">Hello에 **사용자 지정 이미지** 블레이드에서 선택 **+ 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="9abf4-117">On hello **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="9abf4-118">Hello에 **사용자 지정 이미지** 블레이드를 **VHD**합니다.</span><span class="sxs-lookup"><span data-stu-id="9abf4-118">On hello **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="9abf4-119">Hello에 **VHD** 블레이드를 **PowerShell을 사용 하 여 VHD 업로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="9abf4-119">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![PowerShell을 사용하여 VHD 업로드](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. <span data-ttu-id="9abf4-121">hello **PowerShell을 사용 하 여 이미지를 업로드** 블레이드 표시 호출 toohello **Add-azurevhd** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9abf4-121">hello **Upload an image using PowerShell** blade displays a call toohello **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="9abf4-122">첫 번째 매개 변수를 hello (*대상*) blob 컨테이너에 대 한 hello URI가 포함 되어 (*업로드*) 형식에 따라 hello에:</span><span class="sxs-lookup"><span data-stu-id="9abf4-122">hello first parameter (*Destination*) contains hello URI for a blob container (*uploads*) in hello following format:</span></span>

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. <span data-ttu-id="9abf4-123">Hello 기록 이후 단계에서 사용 중 이므로 완전 한 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="9abf4-123">Make note of hello full URI as it is used in later steps.</span></span>

1. <span data-ttu-id="9abf4-124">AzCopy를 사용 하 여 hello VHD 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="9abf4-124">Upload hello VHD file using AzCopy:</span></span>
 
1. <span data-ttu-id="9abf4-125">[Hello AzCopy의 최신 버전 다운로드 및 설치](http://aka.ms/downloadazcopy)합니다.</span><span class="sxs-lookup"><span data-stu-id="9abf4-125">[Download and install hello latest version of AzCopy](http://aka.ms/downloadazcopy).</span></span>

1. <span data-ttu-id="9abf4-126">명령 창을 열고 toohello AzCopy 설치 디렉터리를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="9abf4-126">Open a command window and navigate toohello AzCopy installation directory.</span></span> <span data-ttu-id="9abf4-127">필요에 따라 hello AzCopy 설치 위치 tooyour 시스템 경로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9abf4-127">Optionally, you can add hello AzCopy installation location tooyour system path.</span></span> <span data-ttu-id="9abf4-128">기본적으로 AzCopy는 디렉터리를 다음 설치 된 toohello은:</span><span class="sxs-lookup"><span data-stu-id="9abf4-128">By default, AzCopy is installed toohello following directory:</span></span>

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. <span data-ttu-id="9abf4-129">Hello 저장소 계정 키와 blob 컨테이너 URI를 사용 하 여, hello 다음 hello 명령 프롬프트에서 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9abf4-129">Using hello storage account key and blob container URI, run hello following command at hello command prompt.</span></span> <span data-ttu-id="9abf4-130">hello *vhdFileName* 따옴표로 toobe 필요한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="9abf4-130">hello *vhdFileName* value needs toobe in quotes.</span></span> <span data-ttu-id="9abf4-131">VHD 파일을 업로드할 hello 프로세스 hello VHD 파일의 hello 크기 및 연결 속도 따라 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9abf4-131">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span>   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a><span data-ttu-id="9abf4-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9abf4-132">Next steps</span></span>

- [<span data-ttu-id="9abf4-133">Hello Azure 포털을 사용 하 여 VHD 파일에서 DevTest Labs를 Azure에서 사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="9abf4-133">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="9abf4-134">PowerShell을 사용하여 VHD 파일에서 Azure DevTest Labs에 사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="9abf4-134">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)