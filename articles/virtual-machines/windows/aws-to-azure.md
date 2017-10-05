---
title: "Windows AWS VM을 Azure로 이동 | Microsoft Docs"
description: "Azure PowerShell을 사용하여 AWS(Amazon Web Services) EC2 Windows 인스턴스를 Azure Virtual Machines로 이동합니다."
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
ms.openlocfilehash: 7d2b498d3f84c4fd6cccf97c6d7781f293f5b395
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="move-a-windows-vm-from-amazon-web-services-aws-to-azure-using-powershell"></a><span data-ttu-id="913c0-103">PowerShell을 사용하여 AWS(Amazon Web Services)에서 Azure로 Windows VM 이동</span><span class="sxs-lookup"><span data-stu-id="913c0-103">Move a Windows VM from Amazon Web Services (AWS) to Azure using PowerShell</span></span>

<span data-ttu-id="913c0-104">워크로드를 호스팅하기 위해 Azure 가상 컴퓨터를 평가하는 경우 기존 AWS(Amazon Web Services) EC2 Windows VM 인스턴스를 내보낸 다음 VHD(가상 하드 디스크)를 Azure로 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="913c0-104">If you are evaluating Azure virtual machines for hosting your workloads, you can export an existing Amazon Web Services (AWS) EC2 Windows VM instance then upload the virtual hard disk (VHD) to Azure.</span></span> <span data-ttu-id="913c0-105">VHD를 업로드하면 VHD에서 Azure로 새 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="913c0-105">Once the VHD is uploaded, you can create a new VM in Azure from the VHD.</span></span> 

<span data-ttu-id="913c0-106">이 항목에서는 단일 VM을 AWS에서 Azure로 이동하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="913c0-106">This topic covers moving a single VM from AWS to Azure.</span></span> <span data-ttu-id="913c0-107">VM을 AWS에서 Azure로 대규모로 이동하려면 [Azure Site Recovery를 사용하여 AWS(Amazon Web Services)의 가상 컴퓨터를 Azure로 마이그레이션](../../site-recovery/site-recovery-migrate-aws-to-azure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="913c0-107">If you want to move VMs from AWS to Azure at scale, see [Migrate virtual machines in Amazon Web Services (AWS) to Azure with Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span></span>

## <a name="prepare-the-vm"></a><span data-ttu-id="913c0-108">VM 준비</span><span class="sxs-lookup"><span data-stu-id="913c0-108">Prepare the VM</span></span> 
 
<span data-ttu-id="913c0-109">일반화된 VHD 및 특수한 VHD 모두를 Azure에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="913c0-109">You can upload both generalized and specialized VHDs to Azure.</span></span> <span data-ttu-id="913c0-110">각 유형은 AWS에서 내보내기 전에 VM을 준비해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="913c0-110">Each type requires that you prepare the VM before exporting from AWS.</span></span> 

- <span data-ttu-id="913c0-111">**일반화된 VHD** - 일반화된 VHD에는 Sysprep을 사용하여 제거된 모든 개인 계정 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="913c0-111">**Generalized VHD** - a generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="913c0-112">새 VM을 만드는 이미지로 VHD를 사용하려는 경우 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="913c0-112">If you intend to use the VHD as an image to create new VMs from, you should:</span></span> 
 
    * <span data-ttu-id="913c0-113">[Windows VM을 준비합니다](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="913c0-113">[Prepare a Windows VM](prepare-for-upload-vhd-image.md).</span></span>  
    * <span data-ttu-id="913c0-114">Sysprep을 사용하여 가상 컴퓨터를 일반화합니다.</span><span class="sxs-lookup"><span data-stu-id="913c0-114">Generalize the virtual machine using Sysprep.</span></span>  

 
- <span data-ttu-id="913c0-115">**특수한 VHD** - 특수한 VHD는 사용자 계정, 응용 프로그램 및 원본 VM의 다른 상태 데이터를 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="913c0-115">**Specialized VHD** - a specialized VHD maintains the user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="913c0-116">새 VM을 만드는데 VHD를 그대로 사용하려는 경우 다음 단계가 완료되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="913c0-116">If you intend to use the VHD as-is to create a new VM, ensure the following steps are completed.</span></span>  
    * <span data-ttu-id="913c0-117">[Azure에 업로드할 Windows VHD를 준비합니다](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="913c0-117">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md).</span></span> <span data-ttu-id="913c0-118">Sysprep을 사용하여 VM을 일반화하지 **마십시오**.</span><span class="sxs-lookup"><span data-stu-id="913c0-118">**Do not** generalize the VM using Sysprep.</span></span> 
    * <span data-ttu-id="913c0-119">모든 게스트 가상화 도구 및 VM에 설치된 에이전트를 제거합니다(예: VMware 도구).</span><span class="sxs-lookup"><span data-stu-id="913c0-119">Remove any guest virtualization tools and agents that are installed on the VM (i.e. VMware tools).</span></span> 
    * <span data-ttu-id="913c0-120">VM이 DHCP를 통해 해당 IP 주소 및 DNS 설정을 가져오도록 구성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="913c0-120">Ensure the VM is configured to pull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="913c0-121">이렇게 하면 서버를 시작할 때 VNet 내의 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="913c0-121">This ensures that the server obtains an IP address within the VNet when it starts up.</span></span>  


## <a name="export-and-download-the-vhd"></a><span data-ttu-id="913c0-122">VHD 내보내기 및 다운로드</span><span class="sxs-lookup"><span data-stu-id="913c0-122">Export and download the VHD</span></span> 

<span data-ttu-id="913c0-123">EC2 인스턴스를 Amazon S3 버킷의 VHD로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="913c0-123">Export the EC2 instance to a VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="913c0-124">Amazon 설명서의 [VM 가져오기/내보내기를 사용하여 인스턴스를 VM으로 내보내기](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html)(영문) 항목에서 설명하는 단계를 수행하고, [create-instance-export-task](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) 명령을 실행하여 EC2 인스턴스를 VHD 파일로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="913c0-124">Follow the steps described in the Amazon documentation topic [Exporting an Instance as a VM Using VM Import/Export](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) and run the [create-instance-export-task](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) command to export the EC2 instance to a VHD file.</span></span> 

<span data-ttu-id="913c0-125">내보낸 VHD 파일은 지정한 Amazon S3 버킷에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="913c0-125">The exported VHD file is saved in the Amazon S3 bucket you specify.</span></span> <span data-ttu-id="913c0-126">VHD를 내보내기 위한 기본 구문은 다음과 같으며, 여기서 <brackets>의 자리 표시자 텍스트를 사용자의 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="913c0-126">The basic syntax for exporting the VHD is below, just replace the placeholder text in <brackets> with your information.</span></span>

```
aws ec2 create-instance-export-task --instance-id <instanceID> --target-environment Microsoft \
  --export-to-s3-task DiskImageFormat=VHD,ContainerFormat=ova,S3Bucket=<bucket>,S3Prefix=<prefix>
```

<span data-ttu-id="913c0-127">VHD를 내보냈으면 [S3 버킷에서 개체를 다운로드하려면 어떻게 해야 합니까?(영문)](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html)의 지침에 따라 S3 버킷에서 VHD 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="913c0-127">Once the VHD has been exported, follow the instructions in [How Do I Download an Object from an S3 Bucket?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) to download the VHD file from the S3 bucket.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="913c0-128">AWS에서는 VHD 다운로드에 대한 데이터 전송 요금을 청구합니다.</span><span class="sxs-lookup"><span data-stu-id="913c0-128">AWS charges data transfer fees for downloading the VHD.</span></span> <span data-ttu-id="913c0-129">자세한 내용은 [Amazon S3 요금](https://aws.amazon.com/s3/pricing/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="913c0-129">See [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/) for more information.</span></span>


## <a name="next-steps"></a><span data-ttu-id="913c0-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="913c0-130">Next steps</span></span>

<span data-ttu-id="913c0-131">이제 VHD를 Azure에 업로드하고 새 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="913c0-131">Now you can upload the VHD to Azure and create a new VM.</span></span> 

- <span data-ttu-id="913c0-132">내보내기 전에 **일반화**하도록 원본에서 Sysprep을 실행한 경우 [일반화된 VHD 업로드 및 이 디스크를 사용하여 Azure에서 새 VM 만들기](upload-generalized-managed.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="913c0-132">If you ran Sysprep on your source to **generalize** it before exporting, see [Upload a generalized VHD and use it to create a new VMs in Azure](upload-generalized-managed.md)</span></span>
- <span data-ttu-id="913c0-133">내보내기 전에 Sysprep을 실행하지 않은 경우 VHD는 **특수한 디스크**로 간주됩니다. [Azure에 특수한 VHD 업로드 및 새 VM 만들기](create-vm-specialized.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="913c0-133">If you did not run Sysprep before exporting, the VHD is considered **specialized**, see [Upload a specialized VHD to Azure and create a new VM](create-vm-specialized.md)</span></span>

 
