---
title: Windows AWS Vm tooAzure aaaMove | Microsoft Docs
description: "웹 서비스 AWS (Amazon) EC2 Windows 인스턴스 tooAzure Azure PowerShell을 사용 하 여 가상 컴퓨터를 이동 합니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: cynthn
ms.openlocfilehash: f912c28d3ffe585162c3add715a1318ac3cd4643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-from-amazon-web-services-aws-tooazure-using-powershell"></a><span data-ttu-id="50b1d-103">PowerShell을 사용 하 여 웹 서비스 AWS (Amazon) tooAzure에서 Windows VM 이동</span><span class="sxs-lookup"><span data-stu-id="50b1d-103">Move a Windows VM from Amazon Web Services (AWS) tooAzure using PowerShell</span></span>

<span data-ttu-id="50b1d-104">프로그램 워크 로드를 호스트에 대 한 Azure 가상 컴퓨터를 평가 하는 경우 기존 웹 서비스 AWS (Amazon) EC2 Windows VM 인스턴스를 내보내려면 다음 hello 가상 하드 디스크 (VHD) tooAzure 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50b1d-104">If you are evaluating Azure virtual machines for hosting your workloads, you can export an existing Amazon Web Services (AWS) EC2 Windows VM instance then upload hello virtual hard disk (VHD) tooAzure.</span></span> <span data-ttu-id="50b1d-105">한 번 hello VHD 업로드, 만들 수 있습니다는 새 VM Azure의 hello VHD에서.</span><span class="sxs-lookup"><span data-stu-id="50b1d-105">Once hello VHD is uploaded, you can create a new VM in Azure from hello VHD.</span></span> 

<span data-ttu-id="50b1d-106">이 항목에서 AWS tooAzure 단일 VM 이동에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="50b1d-106">This topic covers moving a single VM from AWS tooAzure.</span></span> <span data-ttu-id="50b1d-107">최대 규모로 AWS tooAzure toomove Vm 참조 [서비스 AWS (Amazon Web) tooAzure Azure 사이트 복구에서 가상 컴퓨터를 마이그레이션할](../../site-recovery/site-recovery-migrate-aws-to-azure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="50b1d-107">If you want toomove VMs from AWS tooAzure at scale, see [Migrate virtual machines in Amazon Web Services (AWS) tooAzure with Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span></span>

## <a name="prepare-hello-vm"></a><span data-ttu-id="50b1d-108">Hello VM 준비</span><span class="sxs-lookup"><span data-stu-id="50b1d-108">Prepare hello VM</span></span> 
 
<span data-ttu-id="50b1d-109">일반화 된 만들고 특수화할 Vhd tooAzure 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50b1d-109">You can upload both generalized and specialized VHDs tooAzure.</span></span> <span data-ttu-id="50b1d-110">각 유형에 AWS에서 내보내기 전에 hello VM을 준비 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="50b1d-110">Each type requires that you prepare hello VM before exporting from AWS.</span></span> 

- <span data-ttu-id="50b1d-111">**일반화된 VHD** - 일반화된 VHD에는 Sysprep을 사용하여 제거된 모든 개인 계정 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50b1d-111">**Generalized VHD** - a generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="50b1d-112">Toouse hello VHD 이미지 toocreate로 가져오려는 경우에서 새 Vm을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="50b1d-112">If you intend toouse hello VHD as an image toocreate new VMs from, you should:</span></span> 
 
    * <span data-ttu-id="50b1d-113">[Windows VM을 준비합니다](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="50b1d-113">[Prepare a Windows VM](prepare-for-upload-vhd-image.md).</span></span>  
    * <span data-ttu-id="50b1d-114">Sysprep를 사용 하 여 hello 가상 컴퓨터를 일반화 합니다.</span><span class="sxs-lookup"><span data-stu-id="50b1d-114">Generalize hello virtual machine using Sysprep.</span></span>  

 
- <span data-ttu-id="50b1d-115">**VHD를 특수화할** -특수 VHD hello 사용자 계정, 응용 프로그램 및 원래 VM에서 다른 상태 데이터를 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="50b1d-115">**Specialized VHD** - a specialized VHD maintains hello user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="50b1d-116">Toouse를 가져오려는 경우 VHD로 hello-toocreate 새 VM은 hello 다음 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="50b1d-116">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span>  
    * <span data-ttu-id="50b1d-117">[Windows VHD tooupload tooAzure 준비](prepare-for-upload-vhd-image.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="50b1d-117">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md).</span></span> <span data-ttu-id="50b1d-118">**없는** 일반화 Sysprep를 사용 하 여 VM hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="50b1d-118">**Do not** generalize hello VM using Sysprep.</span></span> 
    * <span data-ttu-id="50b1d-119">모든 게스트 가상화 도구와 hello (즉, VMware 도구)를 VM에 설치 된 에이전트를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="50b1d-119">Remove any guest virtualization tools and agents that are installed on hello VM (i.e. VMware tools).</span></span> 
    * <span data-ttu-id="50b1d-120">Hello VM 확인 해당 IP 주소 및 DNS 설정이 DHCP 통해 구성 된 toopull 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50b1d-120">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="50b1d-121">이렇게 하면 해당 hello 서버를 시작할 때 hello VNet 내에서 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="50b1d-121">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span>  


## <a name="export-and-download-hello-vhd"></a><span data-ttu-id="50b1d-122">내보내기 및 hello VHD를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="50b1d-122">Export and download hello VHD</span></span> 

<span data-ttu-id="50b1d-123">Hello EC2 인스턴스 tooa Amazon S3 버킷에서 VHD를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="50b1d-123">Export hello EC2 instance tooa VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="50b1d-124">Hello Amazon 설명서 항목에 설명 된 hello 단계에 따라 [인스턴스도는 VM 사용 하 여 VM 가져오기/내보내기 내보내기](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) 및 실행된 hello [-인스턴스-내보내기-작업 만들기](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) 명령 tooexport hello EC2 인스턴스 tooa VHD 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="50b1d-124">Follow hello steps described in hello Amazon documentation topic [Exporting an Instance as a VM Using VM Import/Export](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) and run hello [create-instance-export-task](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) command tooexport hello EC2 instance tooa VHD file.</span></span> 

<span data-ttu-id="50b1d-125">hello 내보낸된 VHD 파일에에서 저장 됩니다 hello Amazon S3 버킷을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="50b1d-125">hello exported VHD file is saved in hello Amazon S3 bucket you specify.</span></span> <span data-ttu-id="50b1d-126">hello 기본 구문 미만인 내보내는 hello VHD에 대 한 바꾸면 hello 자리 표시자 텍스트에 <brackets> 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="50b1d-126">hello basic syntax for exporting hello VHD is below, just replace hello placeholder text in <brackets> with your information.</span></span>

```
aws ec2 create-instance-export-task --instance-id <instanceID> --target-environment Microsoft \
  --export-to-s3-task DiskImageFormat=VHD,ContainerFormat=ova,S3Bucket=<bucket>,S3Prefix=<prefix>
```

<span data-ttu-id="50b1d-127">Hello VHD를 내보낸 후 hello 지침에 따라 [다운로드 하는 방법 개체 S3 버킷을에서?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) hello S3 버킷을에서 toodownload hello VHD 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="50b1d-127">Once hello VHD has been exported, follow hello instructions in [How Do I Download an Object from an S3 Bucket?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) toodownload hello VHD file from hello S3 bucket.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="50b1d-128">AWS는 hello VHD를 다운로드 하기 위한 데이터 전송 요금이 청구 합니다.</span><span class="sxs-lookup"><span data-stu-id="50b1d-128">AWS charges data transfer fees for downloading hello VHD.</span></span> <span data-ttu-id="50b1d-129">자세한 내용은 [Amazon S3 요금](https://aws.amazon.com/s3/pricing/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="50b1d-129">See [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/) for more information.</span></span>


## <a name="next-steps"></a><span data-ttu-id="50b1d-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="50b1d-130">Next steps</span></span>

<span data-ttu-id="50b1d-131">이제 hello VHD tooAzure 업로드 하 고 새 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50b1d-131">Now you can upload hello VHD tooAzure and create a new VM.</span></span> 

- <span data-ttu-id="50b1d-132">너무 소스에서 Sysprep을 실행 한 경우**일반화** 참조 내보내기 전에 [일반화 된 VHD를 업로드 하 고 Azure에서 새 Vm toocreate 사용](upload-generalized-managed.md)</span><span class="sxs-lookup"><span data-stu-id="50b1d-132">If you ran Sysprep on your source too**generalize** it before exporting, see [Upload a generalized VHD and use it toocreate a new VMs in Azure](upload-generalized-managed.md)</span></span>
- <span data-ttu-id="50b1d-133">내보내기 전에 Sysprep를 실행 하지 않은 경우 hello VHD 것으로 간주 됩니다 **특수**, 참조 [특수 VHD tooAzure 업로드 하 고 새 VM 만들기](create-vm-specialized.md)</span><span class="sxs-lookup"><span data-stu-id="50b1d-133">If you did not run Sysprep before exporting, hello VHD is considered **specialized**, see [Upload a specialized VHD tooAzure and create a new VM](create-vm-specialized.md)</span></span>

 
