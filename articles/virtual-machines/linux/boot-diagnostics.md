---
title: "Azure에서 Linux 가상 컴퓨터에 대 한 진단 aaaBoot | Microsoft 문서"
description: "Azure에서 Linux 가상 컴퓨터에 대 한 hello 두 디버깅 기능 개요"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: Deland-Han
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: delhan
ms.openlocfilehash: d355d512de09d2f1d7a2718e3db3fb99c9dd9e24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-boot-diagnostics-tootroubleshoot-linux-virtual-machines-in-azure"></a><span data-ttu-id="37322-103">Toouse는 Azure에서 진단 tootroubleshoot Linux 가상 컴퓨터를 부팅 하는 방법</span><span class="sxs-lookup"><span data-stu-id="37322-103">How toouse boot diagnostics tootroubleshoot Linux virtual machines in Azure</span></span>

<span data-ttu-id="37322-104">이제 Azure에서 두 가지 디버깅 기능에 대한 지원이 제공됩니다. Azure Virtual Machines Resource Manager 배포 모델에 대한 콘솔 출력 및 스크린샷 지원.</span><span class="sxs-lookup"><span data-stu-id="37322-104">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="37322-105">설정할 때 사용자 고유의 이미지 tooAzure 이거나도 부팅 중 hello 플랫폼 이미지, 가상 컴퓨터를 부팅할 수 없는 상태로 가져옵니다 하는 이유는 여러 가지 이유가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37322-105">When bringing your own image tooAzure or even booting one of hello platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="37322-106">Tooeasily 있습니다를 진단 하 고 가상 컴퓨터 부팅 실패에서 복구 이러한 기능 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="37322-106">These features enable you tooeasily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="37322-107">Linux 가상 컴퓨터에 대 한 hello 출력 hello 포털에서에서 콘솔 로그를 쉽게 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37322-107">For Linux Virtual Machines, you can easily view hello output of your console log from hello Portal:</span></span>

![Azure portal](./media/boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="37322-109">그러나 Windows와 Linux 가상 컴퓨터에 대 한 Azure가 해줍니다 toosee를 hello 하이퍼바이저에서 hello VM의 스크린샷:</span><span class="sxs-lookup"><span data-stu-id="37322-109">However, for both Windows and Linux Virtual Machines, Azure also enables you toosee a screenshot of hello VM from hello hypervisor:</span></span>

![오류](./media/boot-diagnostics/screenshot2.png)

<span data-ttu-id="37322-111">이 두 가지 기능이 모든 지역의 Azure Virtual Machines에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="37322-111">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="37322-112">참고, 스크린샷 및 출력 저장소 계정에 분 tooappear too10 차지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37322-112">Note, screenshots, and output can take up too10 minutes tooappear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="37322-113">일반적인 부팅 오류</span><span class="sxs-lookup"><span data-stu-id="37322-113">Common boot errors</span></span>

- [<span data-ttu-id="37322-114">파일 시스템 문제</span><span class="sxs-lookup"><span data-stu-id="37322-114">File system issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/09/13/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes/)
- [<span data-ttu-id="37322-115">커널 문제</span><span class="sxs-lookup"><span data-stu-id="37322-115">Kernel Issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/10/09/linux-recovery-manually-fixing-non-boot-issues-related-to-kernel-problems/)
- [<span data-ttu-id="37322-116">FSTAB 오류</span><span class="sxs-lookup"><span data-stu-id="37322-116">FSTAB errors</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/ )

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="37322-117">새 가상 컴퓨터에서 진단 사용</span><span class="sxs-lookup"><span data-stu-id="37322-117">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="37322-118">Hello 미리 보기 포털에서에서 새 가상 컴퓨터를 만들 때 선택 hello **Azure 리소스 관리자** hello 배포 모델 드롭다운에서:</span><span class="sxs-lookup"><span data-stu-id="37322-118">When creating a new Virtual Machine from hello Preview Portal, select hello **Azure Resource Manager** from hello deployment model dropdown:</span></span>
 
    ![리소스 관리자](./media/boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="37322-120">이러한 진단 파일 hello 모니터링 옵션 tooselect hello 저장소 계정 tooplace 하려는 위치를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="37322-120">Configure hello Monitoring option tooselect hello storage account where you would like tooplace these diagnostic files.</span></span>
 
    ![VM 만들기](./media/boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="37322-122">Azure 리소스 관리자 템플릿을 배포 하는 경우 tooyour 가상 컴퓨터 리소스를 이동 하 고 hello 진단 프로필 섹션을 추가 하세요.</span><span class="sxs-lookup"><span data-stu-id="37322-122">If you are deploying from an Azure Resource Manager template, navigate tooyour Virtual Machine resource and append hello diagnostics profile section.</span></span> <span data-ttu-id="37322-123">Toouse hello "2015-06-15" API 버전 헤더를 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="37322-123">Remember toouse hello “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="37322-124">hello 진단 프로필 tooselect hello 저장소 계정을 저장할 tooput 이러한 로그 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37322-124">hello diagnostics profile enables you tooselect hello storage account where you want tooput these logs.</span></span>

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="37322-125">기존 가상 컴퓨터 업데이트</span><span class="sxs-lookup"><span data-stu-id="37322-125">Update an existing virtual machine</span></span>

<span data-ttu-id="37322-126">hello 포털을 통해 tooenable 부트 진단을 hello 포털을 통해 기존 가상 컴퓨터를 업데이트할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37322-126">tooenable boot diagnostics through hello portal, you can also update an existing virtual machine through hello portal.</span></span> <span data-ttu-id="37322-127">Hello 부트 진단이 저장 및 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="37322-127">Select hello Boot Diagnostics option and Save.</span></span> <span data-ttu-id="37322-128">Hello VM tootake 효과 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="37322-128">Restart hello VM tootake effect.</span></span>

![기본 VM 업데이트](./media/boot-diagnostics/screenshot5.png)