---
title: "VHD aaaUpload tooAzure DevTest Labs PowerShell을 사용 하 여 파일 | Microsoft Docs"
description: "PowerShell을 사용 하 여 VHD 파일 toolab 저장소 계정에 업로드"
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
ms.openlocfilehash: 9c3ee96e212457b0ef8203714b419350cb97f895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-powershell"></a><span data-ttu-id="299bc-103">PowerShell을 사용 하 여 VHD 파일 toolab 저장소 계정에 업로드</span><span class="sxs-lookup"><span data-stu-id="299bc-103">Upload VHD file toolab's storage account using PowerShell</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="299bc-104">Azure DevTest Labs, VHD 파일 tooprovision 사용 되는 가상 컴퓨터는 사용자 지정 이미지를 사용 하는 toocreate 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="299bc-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="299bc-105">hello 다음 단계에 관한 tooupload PowerShell을 사용 하 여 VHD 파일 tooa lab의 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="299bc-105">hello following steps walk you through using PowerShell tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="299bc-106">VHD 파일을 업로드 한 후 hello [다음 단계 섹션](#next-steps) toocreate hello에서 사용자 지정 이미지를 VHD 파일을 업로드 하는 방법을 보여 주는 몇 가지 기사를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="299bc-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="299bc-107">Azure의 디스크 및 VHD에 대한 자세한 내용은 [가상 컴퓨터용 디스크 및 VHD 정보](../virtual-machines/linux/about-disks-and-vhds.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="299bc-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="299bc-108">단계별 지침</span><span class="sxs-lookup"><span data-stu-id="299bc-108">Step-by-step instructions</span></span>

<span data-ttu-id="299bc-109">hello 다음 워크 tooAzure DevTest Labs PowerShell을 사용 하 여 파일을 VHD를 업로드 하는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="299bc-109">hello following steps walk you through uploading a VHD file tooAzure DevTest Labs using PowerShell.</span></span> 

1. <span data-ttu-id="299bc-110">Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.</span><span class="sxs-lookup"><span data-stu-id="299bc-110">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="299bc-111">선택 **더 많은 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="299bc-111">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="299bc-112">랩의 hello 목록에서 원하는 랩 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="299bc-112">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="299bc-113">Hello 랩 블레이드에서 선택 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="299bc-113">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="299bc-114">Hello 랩에 **구성** 블레이드를 **사용자 지정 이미지 (Vhd)**합니다.</span><span class="sxs-lookup"><span data-stu-id="299bc-114">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="299bc-115">Hello에 **사용자 지정 이미지** 블레이드에서 선택 **+ 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="299bc-115">On hello **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="299bc-116">Hello에 **사용자 지정 이미지** 블레이드를 **VHD**합니다.</span><span class="sxs-lookup"><span data-stu-id="299bc-116">On hello **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="299bc-117">Hello에 **VHD** 블레이드를 **PowerShell을 사용 하 여 VHD 업로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="299bc-117">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![PowerShell을 사용하여 VHD 업로드](./media/devtest-lab-upload-vhd-using-powershell/upload-image-using-psh.png)

1. <span data-ttu-id="299bc-119">Hello에 **PowerShell을 사용 하 여 이미지를 업로드** 복사 hello 생성 된 PowerShell 스크립트 tooa 텍스트 편집기, 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="299bc-119">On hello **Upload an image using PowerShell** blade, copy hello generated PowerShell script tooa text editor.</span></span>

1. <span data-ttu-id="299bc-120">Hello 수정 **LocalFilePath** hello의 매개 변수 **Add-azurevhd** hello tooupload VHD 파일의 cmdlet toopoint toohello 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="299bc-120">Modify hello **LocalFilePath** parameter of hello **Add-AzureVhd** cmdlet toopoint toohello location of hello VHD file you want tooupload.</span></span>

1. <span data-ttu-id="299bc-121">PowerShell 프롬프트에서 실행 hello **Add-azurevhd** cmdlet (수정 hello로 **LocalFilePath** 매개 변수).</span><span class="sxs-lookup"><span data-stu-id="299bc-121">At a PowerShell prompt, run hello **Add-AzureVhd** cmdlet (with hello modified **LocalFilePath** parameter).</span></span>

> [!WARNING] 
> 
> <span data-ttu-id="299bc-122">VHD 파일을 업로드할 hello 프로세스 hello VHD 파일의 hello 크기 및 연결 속도 따라 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="299bc-122">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="299bc-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="299bc-123">Next steps</span></span>

- [<span data-ttu-id="299bc-124">Hello Azure 포털을 사용 하 여 VHD 파일에서 DevTest Labs를 Azure에서 사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="299bc-124">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="299bc-125">PowerShell을 사용하여 VHD 파일에서 Azure DevTest Labs에 사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="299bc-125">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
