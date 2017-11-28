---
title: "Linux에서 MySQL 성능 최적화 | Microsoft Docs"
description: "Linux를 실행하는 Azure VM(가상 컴퓨터)에서 실행 중인 MySQL을 최적화하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0c1c7fc5-a528-4d84-b65d-2df225f2233f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: ningk
ms.openlocfilehash: 8f2ec884fa98e989448ac11675e71f39aa21fa7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="optimize-mysql-performance-on-azure-linux-vms"></a><span data-ttu-id="05dcb-103">Azure Linux VM에서 MySQL 성능 최적화</span><span class="sxs-lookup"><span data-stu-id="05dcb-103">Optimize MySQL Performance on Azure Linux VMs</span></span>
<span data-ttu-id="05dcb-104">가상 하드웨어 선택과 소프트웨어 구성 모두에서 Azure의 MySQL 성능에 영향을 주는 많은 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-104">There are many factors that affect MySQL performance on Azure, both in virtual hardware selection and software configuration.</span></span> <span data-ttu-id="05dcb-105">이 문서에서는 저장소, 시스템 및 데이터베이스 구성을 통해 성능을 최적화하는 방법에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-105">This article focuses on optimizing performance through storage, system, and database configurations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="05dcb-106">Azure에는 리소스를 만들고 사용하기 위한 별도의 두 가지 배포 모델, 즉 [Azure Resource Manager](../../../resource-manager-deployment-model.md)와 클래식 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="05dcb-107">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-107">This article covers using the classic deployment model.</span></span> <span data-ttu-id="05dcb-108">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="05dcb-109">Resource Manager 모델을 사용한 Linux VM 최적화에 대한 내용은 [Azure에서 Linux VM 최적화](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05dcb-109">For information about Linux VM optimizations with the Resource Manager model, see [Optimize your Linux VM on Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="utilize-raid-on-an-azure-virtual-machine"></a><span data-ttu-id="05dcb-110">Azure 가상 컴퓨터에서 RAID 활용</span><span class="sxs-lookup"><span data-stu-id="05dcb-110">Utilize RAID on an Azure virtual machine</span></span>
<span data-ttu-id="05dcb-111">저장소는 클라우드 환경에서 데이터베이스 성능에 영향을 주는 핵심 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-111">Storage is the key factor that affects database performance in cloud environments.</span></span> <span data-ttu-id="05dcb-112">단일 디스크에 비해 RAID는 동시 연결을 통해 더욱 빠른 액세스를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-112">Compared to a single disk, RAID can provide faster access via concurrency.</span></span> <span data-ttu-id="05dcb-113">자세한 내용은 [표준 RAID 수준](http://en.wikipedia.org/wiki/Standard_RAID_levels)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05dcb-113">For more information, see [Standard RAID levels](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span></span>   

<span data-ttu-id="05dcb-114">Azure의 디스크 I/O 처리량 및 I/O 응답 시간은 RAID를 통해 향상될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-114">Disk I/O throughput and I/O response time in Azure can be improved through RAID.</span></span> <span data-ttu-id="05dcb-115">Microsoft의 랩 테스트에서는 RAID 디스크 수를 두 배로 늘리면(예: 2개에서 4개, 4개에서 8개 등으로) 평균적으로 디스크 I/O 처리량이 두 배로 늘어나고 I/O 응답 시간이 절반으로 줄어들 수 있음을 보여 주었습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-115">Our lab tests show that disk I/O throughput can be doubled and I/O response time can be reduced by half on average when the number of RAID disks is doubled (from two to four, four to eight, etc.).</span></span> <span data-ttu-id="05dcb-116">자세한 내용은 [부록 A](#AppendixA) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05dcb-116">See [Appendix A](#AppendixA) for details.</span></span>  

<span data-ttu-id="05dcb-117">디스크 I/O 외에도 RAID 수준을 높일 경우 MySQL 성능이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-117">In addition to disk I/O, MySQL performance improves when you increase the RAID level.</span></span>  <span data-ttu-id="05dcb-118">자세한 내용은 [부록 B](#AppendixB) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05dcb-118">See [Appendix B](#AppendixB) for details.</span></span>  

<span data-ttu-id="05dcb-119">또한 청크 크기를 고려할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-119">You might also want to consider the chunk size.</span></span> <span data-ttu-id="05dcb-120">일반적으로 청크 크기가 크면 특히 대량 쓰기에서 오버헤드가 낮아집니다(특히 대량 쓰기의 경우).</span><span class="sxs-lookup"><span data-stu-id="05dcb-120">In general, when you have a larger chunk size, you get lower overhead, especially for large writes.</span></span> <span data-ttu-id="05dcb-121">그러나 청크 크기가 너무 크면 추가 오버헤드가 발생할 수 있으므로 RAID를 활용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-121">However, when the chunk size is too large, it might add additional overhead that prevents you from taking advantage of RAID.</span></span> <span data-ttu-id="05dcb-122">현재 기본 크기는 512KB이며, 대부분의 일반 프로덕션 환경에 가장 적합한 것으로 증명되었습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-122">The current default size is 512 KB, which is proven to be optimal for most general production environments.</span></span> <span data-ttu-id="05dcb-123">자세한 내용은 [부록 C](#AppendixC)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05dcb-123">See [Appendix C](#AppendixC) for details.</span></span>   

<span data-ttu-id="05dcb-124">여러 유형의 가상 컴퓨터에 추가할 수 있는 디스크 수에는 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-124">There are limits on how many disks you can add for different virtual machine types.</span></span> <span data-ttu-id="05dcb-125">이러한 제한은 [Azure의 가상 컴퓨터 및 클라우드 서비스 크기](http://msdn.microsoft.com/library/azure/dn197896.aspx)에서 자세히 설명하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-125">These limits are detailed in [Virtual machine and cloud service sizes for Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span> <span data-ttu-id="05dcb-126">더 적은 수의 디스크로 RAID를 설정하도록 선택할 수 있지만 이 문서의 RAID 예제를 따르려면 연결된 데이터 디스크 4개가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-126">You will need four attached data disks to follow the RAID example in this article, although you can choose to set up RAID with fewer disks.</span></span>  

<span data-ttu-id="05dcb-127">이 문서에서는 Linux 가상 컴퓨터를 이미 만들고 MYSQL을 설치 및 구성하는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-127">This article assumes you have already created a Linux virtual machine and have MYSQL installed and configured.</span></span> <span data-ttu-id="05dcb-128">시작하는 방법에 대한 자세한 내용은 Azure에서 MySQL을 설치하는 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05dcb-128">For more information on getting started, see How to install MySQL on Azure.</span></span>  

### <a name="set-up-raid-on-azure"></a><span data-ttu-id="05dcb-129">Azure에서 RAID 설치</span><span class="sxs-lookup"><span data-stu-id="05dcb-129">Set up RAID on Azure</span></span>
<span data-ttu-id="05dcb-130">다음 단계에서는 Azure Portal을 사용하여 Azure에서 RAID를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-130">The following steps show how to create RAID on Azure by using the Azure portal.</span></span> <span data-ttu-id="05dcb-131">또한 Windows PowerShell 스크립트를 사용하여 RAID를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-131">You can also set up RAID by using Windows PowerShell scripts.</span></span>
<span data-ttu-id="05dcb-132">이 예제에서는 디스크 4개를 사용하여 RAID 0을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-132">In this example, we will configure RAID 0 with four disks.</span></span>  

#### <a name="add-a-data-disk-to-your-virtual-machine"></a><span data-ttu-id="05dcb-133">가상 컴퓨터에 데이터 디스크 추가</span><span class="sxs-lookup"><span data-stu-id="05dcb-133">Add a data disk to your virtual machine</span></span>
<span data-ttu-id="05dcb-134">Azure Portal에서 대시보드로 이동하고 데이터 디스크를 추가할 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-134">In the Azure portal, go to the dashboard and select the virtual machine to which you want to add a data disk.</span></span> <span data-ttu-id="05dcb-135">이 예제의 가상 컴퓨터는 mysqlnode1입니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-135">In this example, the virtual machine is mysqlnode1.</span></span>  

<!--![Virtual machines][1]-->

<span data-ttu-id="05dcb-136">**디스크**를 클릭한 다음 **새로 연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-136">Click **Disks** and then click **Attach New**.</span></span>

![가상 컴퓨터에서 디스크 추가](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-Disks-option.png)

<span data-ttu-id="05dcb-138">새 500GB 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-138">Create a new 500 GB disk.</span></span> <span data-ttu-id="05dcb-139">**호스트 캐시 기본 설정**이 **None**으로 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-139">Make sure that **Host Cache Preference** is set to **None**.</span></span>  <span data-ttu-id="05dcb-140">작업을 완료하면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-140">When you're finished, click **OK**.</span></span>

![빈 디스크 연결](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-attach-empty-disk.png)


<span data-ttu-id="05dcb-142">그러면 가상 컴퓨터에 빈 디스크 하나가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-142">This adds one empty disk into your virtual machine.</span></span> <span data-ttu-id="05dcb-143">RAID의 데이터 디스크가 4개가 되도록 이 단계를 세 번 더 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-143">Repeat this step three more times so that you have four data disks for RAID.</span></span>  

<span data-ttu-id="05dcb-144">커널 메시지 로그에서 가상 컴퓨터에 추가된 드라이브를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-144">You can see the added drives in the virtual machine by looking at the kernel message log.</span></span> <span data-ttu-id="05dcb-145">예를 들어 Ubuntu에서 이를 보려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-145">For example, to see this on Ubuntu, use the following command:</span></span>  

    sudo grep SCSI /var/log/dmesg

#### <a name="create-raid-with-the-additional-disks"></a><span data-ttu-id="05dcb-146">추가 디스크를 사용하여 RAID 만들기</span><span class="sxs-lookup"><span data-stu-id="05dcb-146">Create RAID with the additional disks</span></span>
<span data-ttu-id="05dcb-147">다음 단계에서는 [Linux에서 소프트웨어 RAID를 구성](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-147">The following steps describe how to [configure software RAID on Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="05dcb-148">XFS 파일 시스템을 사용하는 경우 RAID를 만든 후에 다음 단계를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-148">If you are using the XFS file system, execute the following steps after you have created RAID.</span></span>
>
>

<span data-ttu-id="05dcb-149">Debian, Ubuntu 또는 Linux Mint에서 XFS를 설치하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-149">To install XFS on Debian, Ubuntu, or Linux Mint, use the following command:</span></span>  

    apt-get -y install xfsprogs  

<span data-ttu-id="05dcb-150">Fedora, CentOS 또는 RHEL에서 XFS를 설치하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-150">To install XFS on Fedora, CentOS, or RHEL, use the following command:</span></span>  

    yum -y install xfsprogs  xfsdump


#### <a name="set-up-a-new-storage-path"></a><span data-ttu-id="05dcb-151">새 저장소 경로 설정</span><span class="sxs-lookup"><span data-stu-id="05dcb-151">Set up a new storage path</span></span>
<span data-ttu-id="05dcb-152">다음 명령을 사용하여 새 저장소 경로를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-152">Use the following command to set up a new storage path:</span></span>  

    root@mysqlnode1:~# mkdir -p /RAID0/mysql

#### <a name="copy-the-original-data-to-the-new-storage-path"></a><span data-ttu-id="05dcb-153">새 저장소 경로에 원본 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="05dcb-153">Copy the original data to the new storage path</span></span>
<span data-ttu-id="05dcb-154">다음 명령을 사용하여 새 저장소 경로에 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-154">Use the following command to copy data to the new storage path:</span></span>  

    root@mysqlnode1:~# cp -rp /var/lib/mysql/* /RAID0/mysql/

#### <a name="modify-permissions-so-mysql-can-access-read-and-write-the-data-disk"></a><span data-ttu-id="05dcb-155">MySQL에서 데이터 디스크에 액세스(읽기/쓰기)할 수 있도록 사용 권한 수정</span><span class="sxs-lookup"><span data-stu-id="05dcb-155">Modify permissions so MySQL can access (read and write) the data disk</span></span>
<span data-ttu-id="05dcb-156">다음 명령을 사용하여 권한을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-156">Use the following command to modify permissions:</span></span>  

    root@mysqlnode1:~# chown -R mysql.mysql /RAID0/mysql && chmod -R 755 /RAID0/mysql


## <a name="adjust-the-disk-io-scheduling-algorithm"></a><span data-ttu-id="05dcb-157">디스크 I/O 일정 알고리즘 조정</span><span class="sxs-lookup"><span data-stu-id="05dcb-157">Adjust the disk I/O scheduling algorithm</span></span>
<span data-ttu-id="05dcb-158">Linux에서는 다음 네 가지 유형의 I/O 일정 알고리즘을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-158">Linux implements four types of I/O scheduling algorithms:</span></span>  

* <span data-ttu-id="05dcb-159">NOOP 알고리즘(작업 없음)</span><span class="sxs-lookup"><span data-stu-id="05dcb-159">NOOP algorithm (No Operation)</span></span>
* <span data-ttu-id="05dcb-160">Deadline 알고리즘(기한)</span><span class="sxs-lookup"><span data-stu-id="05dcb-160">Deadline algorithm (Deadline)</span></span>
* <span data-ttu-id="05dcb-161">Completely Fair Queuing 알고리즘(CFQ)</span><span class="sxs-lookup"><span data-stu-id="05dcb-161">Completely fair queuing algorithm (CFQ)</span></span>
* <span data-ttu-id="05dcb-162">Budget Period 알고리즘(예상)</span><span class="sxs-lookup"><span data-stu-id="05dcb-162">Budget period algorithm (Anticipatory)</span></span>  

<span data-ttu-id="05dcb-163">상황에 따라 다른 I/O 스케줄러를 선택하여 성능을 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-163">You can select different I/O schedulers under different scenarios to optimize performance.</span></span> <span data-ttu-id="05dcb-164">완전한 임의 액세스 환경에서는 CFQ 알고리즘과 Deadline 알고리즘 간에 성능 면에서 큰 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-164">In a completely random access environment, there is not a significant difference between the CFQ and Deadline algorithms for performance.</span></span> <span data-ttu-id="05dcb-165">MySQL 데이터베이스 환경은 안정성을 위해 Deadline으로 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-165">We recommend that you set the MySQL database environment to Deadline for stability.</span></span> <span data-ttu-id="05dcb-166">순차적 I/O가 많은 경우 CFQ로 인해 디스크 I/O 성능이 저하될 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-166">If there is a lot of sequential I/O, CFQ might reduce disk I/O performance.</span></span>   

<span data-ttu-id="05dcb-167">SSD 및 기타 장비의 경우 NOOP 또는 Deadline을 사용하면 기본 스케줄러보다 성능이 더 향상될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-167">For SSD and other equipment, NOOP or Deadline can achieve better performance than the default scheduler.</span></span>   

<span data-ttu-id="05dcb-168">커널 2.5 이전에는 Deadline이었지만,</span><span class="sxs-lookup"><span data-stu-id="05dcb-168">Prior to the kernel 2.5, the default I/O scheduling algorithm is Deadline.</span></span> <span data-ttu-id="05dcb-169">커널 2.6.18부터 CFQ가 기본 I/O 스케줄링 알고리즘이 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-169">Starting with the kernel 2.6.18, CFQ became the default I/O scheduling algorithm.</span></span>  <span data-ttu-id="05dcb-170">커널 부팅 시 이 설정을 지정하거나 시스템이 실행 중일 때 이 설정을 동적으로 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-170">You can specify this setting at kernel boot time or dynamically modify this setting when the system is running.</span></span>  

<span data-ttu-id="05dcb-171">다음 예제에서는 기본 스케줄러를 확인하여 Debian 배포판 제품군의 NOOP 알고리즘으로 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-171">The following example demonstrates how to check and set the default scheduler to the NOOP algorithm in the Debian distribution family.</span></span>  

### <a name="view-the-current-io-scheduler"></a><span data-ttu-id="05dcb-172">현재 I/O 스케줄러 보기</span><span class="sxs-lookup"><span data-stu-id="05dcb-172">View the current I/O scheduler</span></span>
<span data-ttu-id="05dcb-173">스케줄러를 보려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-173">To view the scheduler run the following command:</span></span>  

    root@mysqlnode1:~# cat /sys/block/sda/queue/scheduler

<span data-ttu-id="05dcb-174">현재 스케줄러를 나타내는 다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-174">You will see following output, which indicates the current scheduler:</span></span>  

    noop [deadline] cfq


### <a name="change-the-current-device-devsda-of-the-io-scheduling-algorithm"></a><span data-ttu-id="05dcb-175">I/O 스케줄링 알고리즘의 현재 장치(/dev/sda) 변경</span><span class="sxs-lookup"><span data-stu-id="05dcb-175">Change the current device (/dev/sda) of the I/O scheduling algorithm</span></span>
<span data-ttu-id="05dcb-176">다음 명령을 실행하여 현재 디렉터리를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-176">Run the following commands to change the current device:</span></span>  

    azureuser@mysqlnode1:~$ sudo su -
    root@mysqlnode1:~# echo "noop" >/sys/block/sda/queue/scheduler
    root@mysqlnode1:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
    root@mysqlnode1:~# update-grub

> [!NOTE]
> <span data-ttu-id="05dcb-177">/dev/sda에 대해서만 이를 설정하는 것은 유용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-177">Setting this for /dev/sda alone is not useful.</span></span> <span data-ttu-id="05dcb-178">데이터베이스가 있는 모든 데이터 디스크에 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-178">It must be set on all data disks where the database resides.</span></span>  
>
>

<span data-ttu-id="05dcb-179">grub.cfg가 성공적으로 다시 빌드되었으며 기본 스케줄러가 NOOP로 업데이트되었음을 나타내는 다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-179">You should see the following output, indicating that grub.cfg has been rebuilt successfully and that the default scheduler has been updated to NOOP:</span></span>  

    Generating grub configuration file ...
    Found linux image: /boot/vmlinuz-3.13.0-34-generic
    Found initrd image: /boot/initrd.img-3.13.0-34-generic
    Found linux image: /boot/vmlinuz-3.13.0-32-generic
    Found initrd image: /boot/initrd.img-3.13.0-32-generic
    Found memtest86+ image: /memtest86+.elf
    Found memtest86+ image: /memtest86+.bin
    done

<span data-ttu-id="05dcb-180">Red Hat 배포판 제품군의 경우 다음 명령만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-180">For the Red Hat distribution family, you need only the following command:</span></span>

    echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local

## <a name="configure-system-file-operations-settings"></a><span data-ttu-id="05dcb-181">시스템 파일 작업 설정 구성</span><span class="sxs-lookup"><span data-stu-id="05dcb-181">Configure system file operations settings</span></span>
<span data-ttu-id="05dcb-182">파일 시스템에서 *atime* 로깅 기능을 사용하지 않도록 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-182">One best practice is to disable the *atime* logging feature on the file system.</span></span> <span data-ttu-id="05dcb-183">Atime은 마지막 파일 액세스 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-183">Atime is the last file access time.</span></span> <span data-ttu-id="05dcb-184">파일에 액세스할 때마다 파일 시스템에서 로그에 타임스탬프를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-184">Whenever a file is accessed, the file system records the timestamp in the log.</span></span> <span data-ttu-id="05dcb-185">그러나 이 정보는 거의 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-185">However, this information is rarely used.</span></span> <span data-ttu-id="05dcb-186">필요하지 않은 경우 사용하지 않도록 설정하여 전체 디스크 액세스 시간을 단축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-186">You can disable it if you don't need it, which will reduce overall disk access time.</span></span>  

<span data-ttu-id="05dcb-187">atime 로깅을 사용하지 않도록 설정하려면 파일 시스템 구성 파일 /etc/ fstab을 수정하고 **noatime** 옵션을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-187">To disable atime logging, you need to modify the file system configuration file /etc/ fstab and add the **noatime** option.</span></span>  

<span data-ttu-id="05dcb-188">예를 들어 vim/etc/fstab 파일을 편집하여 다음 샘플과 같이 noatime을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-188">For example, edit the vim /etc/fstab file, adding the noatime as shown in the following sample:</span></span>  

    # CLOUD_IMG: This file was created/modified by the Cloud Image build process
    UUID=3cc98c06-d649-432d-81df-6dcd2a584d41       /        ext4   defaults,discard        0 0
    #Add the “noatime” option below to disable atime logging
    UUID="431b1e78-8226-43ec-9460-514a9adf060e"     /RAID0   xfs   defaults,nobootwait, noatime 0 0
    /dev/sdb1       /mnt    auto    defaults,nobootwait,comment=cloudconfig 0       2

<span data-ttu-id="05dcb-189">그런 후 다음 명령으로 파일 시스템을 다시 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-189">Then, remount the file system with the following command:</span></span>  

    mount -o remount /RAID0

<span data-ttu-id="05dcb-190">수정된 결과를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-190">Test the modified result.</span></span> <span data-ttu-id="05dcb-191">테스트 파일을 수정하면 액세스 시간이 업데이트되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-191">When you modify the test file, the access time is not updated.</span></span> <span data-ttu-id="05dcb-192">다음 예제에서는 수정 전후의 코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-192">The following examples show what the code looks like before and after modification.</span></span>

<span data-ttu-id="05dcb-193">이전:</span><span class="sxs-lookup"><span data-stu-id="05dcb-193">Before:</span></span>        

![액세스 수정 이전 코드][5]

<span data-ttu-id="05dcb-195">이후:</span><span class="sxs-lookup"><span data-stu-id="05dcb-195">After:</span></span>

![액세스 수정 이후 코드][6]

## <a name="increase-the-maximum-number-of-system-handles-for-high-concurrency"></a><span data-ttu-id="05dcb-197">동시성 향상을 위한 최대 시스템 핸들 수 증가</span><span class="sxs-lookup"><span data-stu-id="05dcb-197">Increase the maximum number of system handles for high concurrency</span></span>
<span data-ttu-id="05dcb-198">MySQL은 동시성이 뛰어난 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-198">MySQL is a high concurrency database.</span></span> <span data-ttu-id="05dcb-199">기본 동시 핸들 수는 Linux의 경우 1024개이며, 이것으로 부족한 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-199">The default number of concurrent handles is 1024 for Linux, which is not always sufficient.</span></span> <span data-ttu-id="05dcb-200">다음 단계를 사용하여 MySQL의 뛰어난 동시성을 지원하도록 시스템의 최대 동시 핸들 수를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-200">Use the following steps to increase the maximum concurrent handles of the system to support high concurrency of MySQL.</span></span>

### <a name="modify-the-limitsconf-file"></a><span data-ttu-id="05dcb-201">limits.conf 파일 수정</span><span class="sxs-lookup"><span data-stu-id="05dcb-201">Modify the limits.conf file</span></span>
<span data-ttu-id="05dcb-202">허용되는 최대 동시 처리량을 늘리려면 /etc/security/limits.conf 파일에 다음 네 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-202">To increase the maximum allowed concurrent handles, add the following four lines in the /etc/security/limits.conf file.</span></span> <span data-ttu-id="05dcb-203">65536은 시스템에서 지원할 수 있는 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-203">Note that 65536 is the maximum number that the system can support.</span></span>   

    * <span data-ttu-id="05dcb-204">soft nofile 65536</span><span class="sxs-lookup"><span data-stu-id="05dcb-204">soft nofile 65536</span></span>
    * <span data-ttu-id="05dcb-205">hard nofile 65536</span><span class="sxs-lookup"><span data-stu-id="05dcb-205">hard nofile 65536</span></span>
    * <span data-ttu-id="05dcb-206">soft nproc 65536</span><span class="sxs-lookup"><span data-stu-id="05dcb-206">soft nproc 65536</span></span>
    * <span data-ttu-id="05dcb-207">hard nproc 65536</span><span class="sxs-lookup"><span data-stu-id="05dcb-207">hard nproc 65536</span></span>

### <a name="update-the-system-for-the-new-limits"></a><span data-ttu-id="05dcb-208">새 제한에 대해 시스템 업데이트</span><span class="sxs-lookup"><span data-stu-id="05dcb-208">Update the system for the new limits</span></span>
<span data-ttu-id="05dcb-209">시스템을 업데이트하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-209">To update the system, run the following commands:</span></span>  

    ulimit -SHn 65536
    ulimit -SHu 65536

### <a name="ensure-that-the-limits-are-updated-at-boot-time"></a><span data-ttu-id="05dcb-210">부팅 시 제한이 업데이트되도록 설정</span><span class="sxs-lookup"><span data-stu-id="05dcb-210">Ensure that the limits are updated at boot time</span></span>
<span data-ttu-id="05dcb-211">부팅 시 적용되도록 /etc/rc.local 파일에 다음 시작 명령을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-211">Put the following startup commands in the /etc/rc.local file so it will take effect at boot time.</span></span>  

    echo “ulimit -SHn 65536” >>/etc/rc.local
    echo “ulimit -SHu 65536” >>/etc/rc.local

## <a name="mysql-database-optimization"></a><span data-ttu-id="05dcb-212">MySQL 데이터베이스 최적화</span><span class="sxs-lookup"><span data-stu-id="05dcb-212">MySQL database optimization</span></span>
<span data-ttu-id="05dcb-213">Azure에서 MySQL을 구성하려면 온-프레미스 시스템에서 사용하는 것과 동일한 성능 조정 전략을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-213">To configure MySQL on Azure, you can use the same performance-tuning strategy you use on an on-premises machine.</span></span>  

<span data-ttu-id="05dcb-214">기본 I/O 최적화 규칙은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-214">The main I/O optimization rules are:</span></span>   

* <span data-ttu-id="05dcb-215">캐시 크기 증가.</span><span class="sxs-lookup"><span data-stu-id="05dcb-215">Increase the cache size.</span></span>
* <span data-ttu-id="05dcb-216">I/O 응답 시간 감소</span><span class="sxs-lookup"><span data-stu-id="05dcb-216">Reduce I/O response time.</span></span>  

<span data-ttu-id="05dcb-217">MySQL 서버 설정을 최적화하려면 서버 컴퓨터와 클라이언트 컴퓨터 모두의 기본 구성 파일인 my.cnf 파일을 업데이트하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-217">To optimize MySQL server settings, you can update the my.cnf file, which is the default configuration file for both server and client computers.</span></span>  

<span data-ttu-id="05dcb-218">다음 구성 항목은 MySQL 성능에 영향을 주요 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-218">The following configuration items are the main factors that affect MySQL performance:</span></span>  

* <span data-ttu-id="05dcb-219">**innodb_buffer_pool_size**: 버퍼 풀에는 버퍼된 데이터와 인덱스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-219">**innodb_buffer_pool_size**: The buffer pool contains buffered data and the index.</span></span> <span data-ttu-id="05dcb-220">이 옵션은 일반적으로 실제 메모리의 70%로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-220">This is usually set to 70 percent of physical memory.</span></span>
* <span data-ttu-id="05dcb-221">**innodb_log_file_size**: 다시 실행 로그 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-221">**innodb_log_file_size**: This is the redo log size.</span></span> <span data-ttu-id="05dcb-222">다시 실행 로그를 사용하면 쓰기 작업이 빠르고 안정적이며 크래시 후 복구할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-222">You use redo logs to ensure that write operations are fast, reliable, and recoverable after a crash.</span></span> <span data-ttu-id="05dcb-223">이 옵션은 512MB로 설정되어 있으며, 쓰기 작업을 로깅하는 데 충분한 공간을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-223">This is set to 512 MB, which will give you plenty of space for logging write operations.</span></span>
* <span data-ttu-id="05dcb-224">**max_connections**: 일부 응용 프로그램은 연결을 제대로 닫지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-224">**max_connections**: Sometimes applications do not close connections properly.</span></span> <span data-ttu-id="05dcb-225">이 값이 클수록 서버에 유휴 상태의 연결을 재순환할 수 있는 시간이 더 많이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-225">A larger value will give the server more time to recycle idled connections.</span></span> <span data-ttu-id="05dcb-226">최대 연결 수는 10,000개이지만 권장되는 최대값은 5,000개입니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-226">The maximum number of connections is 10,000, but the recommended maximum is 5,000.</span></span>
* <span data-ttu-id="05dcb-227">**Innodb_file_per_table**: 이 설정은 InnoDB에서 테이블을 별도의 파일에 저장할 수 있는 기능을 사용하거나 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-227">**Innodb_file_per_table**: This setting enables or disables the ability of InnoDB to store tables in separate files.</span></span> <span data-ttu-id="05dcb-228">이 옵션을 설정하면 여러 고급 관리 작업을 효율적으로 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-228">Turn on the option to ensure that several advanced administration operations can be applied efficiently.</span></span> <span data-ttu-id="05dcb-229">성능 면에서 테이블 공간 전송 속도를 높이고 잔류물 관리 성능을 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-229">From a performance point of view, it can speed up the table space transmission and optimize the debris management performance.</span></span> <span data-ttu-id="05dcb-230">이 옵션의 권장 설정은 ON입니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-230">The recommended setting for this option is ON.</span></span></br></br>
<span data-ttu-id="05dcb-231">MySQL 5.6부터 기본 설정이 ON이므로 어떤 조치도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-231">From MySQL 5.6, the default setting is ON, so no action is required.</span></span> <span data-ttu-id="05dcb-232">이전 버전의 경우 기본 설정은 OFF입니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-232">For earlier versions, the default setting is OFF.</span></span> <span data-ttu-id="05dcb-233">새로 만든 테이블만 영향을 받으므로 데이터가 로드되기 전에 설정을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-233">The setting should be changed before data is loaded, because only newly created tables are affected.</span></span>
* <span data-ttu-id="05dcb-234">**innodb_flush_log_at_trx_commit**: 기본값은 1이며 범위는 0~2로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-234">**innodb_flush_log_at_trx_commit**: The default value is 1, with the scope set to 0~2.</span></span> <span data-ttu-id="05dcb-235">기본값은 독립 실행형 MySQL DB에 가장 적합한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-235">The default value is the most suitable option for standalone MySQL DB.</span></span> <span data-ttu-id="05dcb-236">2로 설정하면 데이터 무결성이 가장 많이 높아지며 MySQL 클러스터의 마스터에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-236">The setting of 2 enables the most data integrity and is suitable for Master in MySQL Cluster.</span></span> <span data-ttu-id="05dcb-237">0으로 설정하면 데이터 손실이 발생하여 안정성에 영향을 줄 수 있으며(경우에 따라 성능이 향상될 수 있음) MySQL 클러스터의 슬레이브에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-237">The setting of 0 allows data loss, which can affect reliability (in some cases with better performance), and is suitable for Slave in MySQL Cluster.</span></span>
* <span data-ttu-id="05dcb-238">**Innodb_log_buffer_size**: 로그 버퍼는 트랜잭션이 커밋되기 전에 로그를 디스크에 플러시하지 않고도 트랜잭션이 실행되도록 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-238">**Innodb_log_buffer_size**: The log buffer allows transactions to run without having to flush the log to disk before the transactions commit.</span></span> <span data-ttu-id="05dcb-239">그러나 큰 이진 개체 또는 텍스트 필드가 있으면 캐시가 빠르게 소비되고 디스크 I/O가 자주 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-239">However, if there is large binary object or text field, the cache will be consumed quickly and frequent disk I/O will be triggered.</span></span> <span data-ttu-id="05dcb-240">Innodb_log_waits 상태 변수가 0이 아닌 경우 버퍼 크기를 늘리는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-240">It is better increase the buffer size if Innodb_log_waits state variable is not 0.</span></span>
* <span data-ttu-id="05dcb-241">**query_cache_size**: 처음부터 사용하지 않도록 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-241">**query_cache_size**: The best option is to disable it from the outset.</span></span> <span data-ttu-id="05dcb-242">query_cache_size를 0(MySQL 5.6의 기본 설정)으로 설정하고 다른 방법을 사용하여 쿼리 속도를 높입니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-242">Set query_cache_size to 0 (this is the default setting in MySQL 5.6) and use other methods to speed up queries.</span></span>  

<span data-ttu-id="05dcb-243">최적화 전후의 성능 비교는 [부록 D](#AppendixD)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05dcb-243">See [Appendix D](#AppendixD) for a comparison of performance before and after the optimization.</span></span>

## <a name="turn-on-the-mysql-slow-query-log-for-analyzing-the-performance-bottleneck"></a><span data-ttu-id="05dcb-244">MySQL 느린 쿼리 로그를 설정하여 성능 병목 현상 분석</span><span class="sxs-lookup"><span data-stu-id="05dcb-244">Turn on the MySQL slow query log for analyzing the performance bottleneck</span></span>
<span data-ttu-id="05dcb-245">MySQL 느린 쿼리 로그를 사용하면 MySQL에 대한 느린 쿼리를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-245">The MySQL slow query log can help you identify the slow queries for MySQL.</span></span> <span data-ttu-id="05dcb-246">MySQL 느린 쿼리 로그를 사용하도록 설정한 후 **mysqldumpslow** 와 같은 MySQL 도구를 사용하여 성능 병목 현상을 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-246">After enabling the MySQL slow query log, you can use MySQL tools like **mysqldumpslow** to identify the performance bottleneck.</span></span>  

<span data-ttu-id="05dcb-247">기본적으로 이 옵션은 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-247">By default, this is not enabled.</span></span> <span data-ttu-id="05dcb-248">느린 쿼리 로그를 설정하면 일부 CPU 리소스가 소모될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-248">Turning on the slow query log might consume some CPU resources.</span></span> <span data-ttu-id="05dcb-249">성능 병목 문제를 해결하기 위해 이 옵션을 일시적으로 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-249">We recommend that you enable this temporarily for troubleshooting performance bottlenecks.</span></span> <span data-ttu-id="05dcb-250">느린 쿼리 로그를 설정하려면 다음과 같이 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-250">To turn on the slow query log:</span></span>

1. <span data-ttu-id="05dcb-251">다음 줄을 끝에 추가하여 my.cnf 파일을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-251">Modify the my.cnf file by adding the following lines to the end:</span></span>

        long_query_time = 2
        slow_query_log = 1
        slow_query_log_file = /RAID0/mysql/mysql-slow.log

2. <span data-ttu-id="05dcb-252">MySQL 서버를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-252">Restart the MySQL server.</span></span>

        service  mysql  restart

3. <span data-ttu-id="05dcb-253">**show** 명령을 사용하여 설정이 적용되고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-253">Check whether the setting is taking effect by using the **show** command.</span></span>

![Slow-query-log ON][7]   

![Slow-query-log results][8]

<span data-ttu-id="05dcb-256">이 예제에서는 느린 쿼리 기능이 설정된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-256">In this example, you can see that the slow query feature has been turned on.</span></span> <span data-ttu-id="05dcb-257">**mysqldumpslow** 도구를 사용하여 성능 병목 현상을 확인하고 인덱스 추가와 같은 성능을 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-257">You can then use the **mysqldumpslow** tool to determine performance bottlenecks and optimize performance, such as adding indexes.</span></span>

## <a name="appendices"></a><span data-ttu-id="05dcb-258">부록</span><span class="sxs-lookup"><span data-stu-id="05dcb-258">Appendices</span></span>
<span data-ttu-id="05dcb-259">다음은 대상 랩 환경에서 생성된 샘플 성능 테스트 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-259">The following are sample performance test data produced in a targeted lab environment.</span></span> <span data-ttu-id="05dcb-260">여기서는 서로 다른 성능 조정 방법을 사용하여 성능 데이터 추세에 대한 일반적인 배경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-260">They provide general background on the performance data trend with different performance tuning approaches.</span></span> <span data-ttu-id="05dcb-261">환경이나 제품 버전에 따라 결과가 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-261">The results might vary under different environment or product versions.</span></span>

### <span data-ttu-id="05dcb-262"><a name="AppendixA"></a>부록 A</span><span class="sxs-lookup"><span data-stu-id="05dcb-262"><a name="AppendixA"></a>Appendix A</span></span>  
<span data-ttu-id="05dcb-263">**RAID 수준별 디스크 성능(IOPS)**</span><span class="sxs-lookup"><span data-stu-id="05dcb-263">**Disk performance (IOPS) with different RAID levels**</span></span>

![RAID 수준별 디스크 IOPS][9]

<span data-ttu-id="05dcb-265">**테스트 명령**</span><span class="sxs-lookup"><span data-stu-id="05dcb-265">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=5G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite

> [!NOTE]
> <span data-ttu-id="05dcb-266">이 테스트의 작업에서는 RAID 상한에 도달하기 위해 64개의 스레드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-266">The workload of this test uses 64 threads, trying to reach the upper limit of RAID.</span></span>
>
>

### <span data-ttu-id="05dcb-267"><a name="AppendixB"></a>부록 B</span><span class="sxs-lookup"><span data-stu-id="05dcb-267"><a name="AppendixB"></a>Appendix B</span></span>  
<span data-ttu-id="05dcb-268">**RAID 수준별 MySQL 성능(처리량) 비교** </span><span class="sxs-lookup"><span data-stu-id="05dcb-268">**MySQL performance (throughput) comparison with different RAID levels** </span></span>  
<span data-ttu-id="05dcb-269">(XFS 파일 시스템)</span><span class="sxs-lookup"><span data-stu-id="05dcb-269">(XFS file system)</span></span>

![RAID 수준별 MySQL 성능 비교][10]  
![RAID 수준별 MySQL 성능 비교][11]

<span data-ttu-id="05dcb-272">**테스트 명령**</span><span class="sxs-lookup"><span data-stu-id="05dcb-272">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb

<span data-ttu-id="05dcb-273">**RAID 수준별 MySQL 성능(OLTP) 비교**</span><span class="sxs-lookup"><span data-stu-id="05dcb-273">**MySQL performance (OLTP) comparison with different RAID levels**</span></span>  
<span data-ttu-id="05dcb-274">![RAID 수준별 MySQL 성능(OLTP) 비교][12]</span><span class="sxs-lookup"><span data-stu-id="05dcb-274">![MySQL performance (OLTP) comparison with different RAID levels][12]</span></span>

<span data-ttu-id="05dcb-275">**테스트 명령**</span><span class="sxs-lookup"><span data-stu-id="05dcb-275">**Test commands**</span></span>

    time sysbench --test=oltp --db-driver=mysql --mysql-user=root --mysql-password=0ps.123  --mysql-table-engine=innodb --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-socket=/var/run/mysqld/mysqld.sock --mysql-db=test --oltp-table-size=1000000 prepare

### <span data-ttu-id="05dcb-276"><a name="AppendixC"></a>부록 C</span><span class="sxs-lookup"><span data-stu-id="05dcb-276"><a name="AppendixC"></a>Appendix C</span></span>   
<span data-ttu-id="05dcb-277">**청크 크기별 디스크 성능(IOPS) 비교**</span><span class="sxs-lookup"><span data-stu-id="05dcb-277">**Disk performance (IOPS) comparison for different chunk sizes**</span></span>  
<span data-ttu-id="05dcb-278">(XFS 파일 시스템)</span><span class="sxs-lookup"><span data-stu-id="05dcb-278">(XFS file system)</span></span>

![][13]

<span data-ttu-id="05dcb-279">**테스트 명령**</span><span class="sxs-lookup"><span data-stu-id="05dcb-279">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=30G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite
    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=1G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite  

<span data-ttu-id="05dcb-280">이 테스트에 사용된 파일 크기는 각각 RAID 0(4개 디스크) XFS 파일 시스템이 있는 30GB 및 1GB입니다.</span><span class="sxs-lookup"><span data-stu-id="05dcb-280">The file sizes used for this testing are 30 GB and 1 GB, respectively, with RAID 0 (4 disks) XFS file system.</span></span>

### <span data-ttu-id="05dcb-281"><a name="AppendixD"></a>부록 D</span><span class="sxs-lookup"><span data-stu-id="05dcb-281"><a name="AppendixD"></a>Appendix D</span></span>  
<span data-ttu-id="05dcb-282">**최적화 전후의 MySQL 성능(처리량) 비교**</span><span class="sxs-lookup"><span data-stu-id="05dcb-282">**MySQL performance (throughput) comparison before and after optimization**</span></span>  
<span data-ttu-id="05dcb-283">(XFS 파일 시스템)</span><span class="sxs-lookup"><span data-stu-id="05dcb-283">(XFS File System)</span></span>

![최적화 전후의 MySQL 성능(처리량) 비교][14]

<span data-ttu-id="05dcb-285">**테스트 명령**</span><span class="sxs-lookup"><span data-stu-id="05dcb-285">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb,misam

<span data-ttu-id="05dcb-286">**기본 및 최적화에 대한 구성 설정은 다음과 같습니다.**</span><span class="sxs-lookup"><span data-stu-id="05dcb-286">**The configuration setting for default and optimization is as follows:**</span></span>

| <span data-ttu-id="05dcb-287">매개 변수</span><span class="sxs-lookup"><span data-stu-id="05dcb-287">Parameters</span></span> | <span data-ttu-id="05dcb-288">기본값</span><span class="sxs-lookup"><span data-stu-id="05dcb-288">Default</span></span> | <span data-ttu-id="05dcb-289">최적화</span><span class="sxs-lookup"><span data-stu-id="05dcb-289">Optimization</span></span> |
| --- | --- | --- |
| <span data-ttu-id="05dcb-290">**innodb_buffer_pool_size**</span><span class="sxs-lookup"><span data-stu-id="05dcb-290">**innodb_buffer_pool_size**</span></span> |<span data-ttu-id="05dcb-291">없음</span><span class="sxs-lookup"><span data-stu-id="05dcb-291">None</span></span> |<span data-ttu-id="05dcb-292">7 GB</span><span class="sxs-lookup"><span data-stu-id="05dcb-292">7 GB</span></span> |
| <span data-ttu-id="05dcb-293">**innodb_log_file_size**</span><span class="sxs-lookup"><span data-stu-id="05dcb-293">**innodb_log_file_size**</span></span> |<span data-ttu-id="05dcb-294">5MB</span><span class="sxs-lookup"><span data-stu-id="05dcb-294">5 MB</span></span> |<span data-ttu-id="05dcb-295">512MB</span><span class="sxs-lookup"><span data-stu-id="05dcb-295">512 MB</span></span> |
| <span data-ttu-id="05dcb-296">**max_connections**</span><span class="sxs-lookup"><span data-stu-id="05dcb-296">**max_connections**</span></span> |<span data-ttu-id="05dcb-297">100</span><span class="sxs-lookup"><span data-stu-id="05dcb-297">100</span></span> |<span data-ttu-id="05dcb-298">5000</span><span class="sxs-lookup"><span data-stu-id="05dcb-298">5000</span></span> |
| <span data-ttu-id="05dcb-299">**innodb_file_per_table**</span><span class="sxs-lookup"><span data-stu-id="05dcb-299">**innodb_file_per_table**</span></span> |<span data-ttu-id="05dcb-300">0</span><span class="sxs-lookup"><span data-stu-id="05dcb-300">0</span></span> |<span data-ttu-id="05dcb-301">1</span><span class="sxs-lookup"><span data-stu-id="05dcb-301">1</span></span> |
| <span data-ttu-id="05dcb-302">**innodb_flush_log_at_trx_commit**</span><span class="sxs-lookup"><span data-stu-id="05dcb-302">**innodb_flush_log_at_trx_commit**</span></span> |<span data-ttu-id="05dcb-303">1</span><span class="sxs-lookup"><span data-stu-id="05dcb-303">1</span></span> |<span data-ttu-id="05dcb-304">2</span><span class="sxs-lookup"><span data-stu-id="05dcb-304">2</span></span> |
| <span data-ttu-id="05dcb-305">**innodb_log_buffer_size**</span><span class="sxs-lookup"><span data-stu-id="05dcb-305">**innodb_log_buffer_size**</span></span> |<span data-ttu-id="05dcb-306">8MB</span><span class="sxs-lookup"><span data-stu-id="05dcb-306">8 MB</span></span> |<span data-ttu-id="05dcb-307">128MB</span><span class="sxs-lookup"><span data-stu-id="05dcb-307">128 MB</span></span> |
| <span data-ttu-id="05dcb-308">**query_cache_size**</span><span class="sxs-lookup"><span data-stu-id="05dcb-308">**query_cache_size**</span></span> |<span data-ttu-id="05dcb-309">16MB</span><span class="sxs-lookup"><span data-stu-id="05dcb-309">16 MB</span></span> |<span data-ttu-id="05dcb-310">0</span><span class="sxs-lookup"><span data-stu-id="05dcb-310">0</span></span> |

<span data-ttu-id="05dcb-311">[최적화 구성 매개 변수](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html)(영문)에 대한 자세한 내용은 [MySQL 공식 지침](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05dcb-311">For more detailed [optimization configuration parameters](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), refer to the [MySQL official instructions](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span></span>  

  <span data-ttu-id="05dcb-312">**테스트 환경**</span><span class="sxs-lookup"><span data-stu-id="05dcb-312">**Test environment**</span></span>  

| <span data-ttu-id="05dcb-313">하드웨어</span><span class="sxs-lookup"><span data-stu-id="05dcb-313">Hardware</span></span> | <span data-ttu-id="05dcb-314">세부 정보</span><span class="sxs-lookup"><span data-stu-id="05dcb-314">Details</span></span> |
| --- | --- |
| <span data-ttu-id="05dcb-315">CPU</span><span class="sxs-lookup"><span data-stu-id="05dcb-315">CPU</span></span> |<span data-ttu-id="05dcb-316">AMD Opteron(tm) 프로세서 4171 HE/4 코어</span><span class="sxs-lookup"><span data-stu-id="05dcb-316">AMD Opteron(tm) Processor 4171 HE/4 cores</span></span> |
| <span data-ttu-id="05dcb-317">메모리</span><span class="sxs-lookup"><span data-stu-id="05dcb-317">Memory</span></span> |<span data-ttu-id="05dcb-318">14 GB</span><span class="sxs-lookup"><span data-stu-id="05dcb-318">14 GB</span></span> |
| <span data-ttu-id="05dcb-319">디스크</span><span class="sxs-lookup"><span data-stu-id="05dcb-319">Disk</span></span> |<span data-ttu-id="05dcb-320">10GB/디스크</span><span class="sxs-lookup"><span data-stu-id="05dcb-320">10 GB/disk</span></span> |
| <span data-ttu-id="05dcb-321">OS</span><span class="sxs-lookup"><span data-stu-id="05dcb-321">OS</span></span> |<span data-ttu-id="05dcb-322">Ubuntu 14.04.1 LTS</span><span class="sxs-lookup"><span data-stu-id="05dcb-322">Ubuntu 14.04.1 LTS</span></span> |

[1]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-01.png
[2]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-02.png
[3]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-03.png
[4]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-04.png
[5]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-05.png
[6]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-06.png
[7]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-07.png
[8]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-08.png
[9]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-09.png
[10]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-10.png
[11]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-11.png
[12]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-12.png
[13]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-13.png
[14]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-14.png

