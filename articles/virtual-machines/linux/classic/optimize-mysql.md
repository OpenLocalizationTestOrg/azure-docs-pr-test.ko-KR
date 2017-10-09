---
title: "Linux에서 MySQL 성능 aaaOptimize | Microsoft Docs"
description: "자세한 내용은 방법 toooptimize MySQL Linux를 실행 중인 Azure 가상 컴퓨터 (VM)에서 실행 합니다."
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
ms.openlocfilehash: 9e6458723233721e06f30b9de33635d403eefcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-mysql-performance-on-azure-linux-vms"></a><span data-ttu-id="11f07-103">Azure Linux VM에서 MySQL 성능 최적화</span><span class="sxs-lookup"><span data-stu-id="11f07-103">Optimize MySQL Performance on Azure Linux VMs</span></span>
<span data-ttu-id="11f07-104">가상 하드웨어 선택과 소프트웨어 구성 모두에서 Azure의 MySQL 성능에 영향을 주는 많은 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-104">There are many factors that affect MySQL performance on Azure, both in virtual hardware selection and software configuration.</span></span> <span data-ttu-id="11f07-105">이 문서에서는 저장소, 시스템 및 데이터베이스 구성을 통해 성능을 최적화하는 방법에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-105">This article focuses on optimizing performance through storage, system, and database configurations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="11f07-106">Azure에는 리소스를 만들고 사용하기 위한 별도의 두 가지 배포 모델, 즉 [Azure Resource Manager](../../../resource-manager-deployment-model.md)와 클래식 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="11f07-107">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-107">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="11f07-108">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="11f07-109">리소스 관리자 모델 hello 사용 하 여 Linux VM 최적화에 대 한 정보를 참조 하십시오. [Azure에서 Linux VM 최적화](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-109">For information about Linux VM optimizations with hello Resource Manager model, see [Optimize your Linux VM on Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="utilize-raid-on-an-azure-virtual-machine"></a><span data-ttu-id="11f07-110">Azure 가상 컴퓨터에서 RAID 활용</span><span class="sxs-lookup"><span data-stu-id="11f07-110">Utilize RAID on an Azure virtual machine</span></span>
<span data-ttu-id="11f07-111">저장소는 클라우드 환경에서 데이터베이스 성능에 영향을 주는 hello 핵심 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-111">Storage is hello key factor that affects database performance in cloud environments.</span></span> <span data-ttu-id="11f07-112">비교 tooa 단일 디스크를 RAID 동시성을 통해 빠른 액세스를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-112">Compared tooa single disk, RAID can provide faster access via concurrency.</span></span> <span data-ttu-id="11f07-113">자세한 내용은 [표준 RAID 수준](http://en.wikipedia.org/wiki/Standard_RAID_levels)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11f07-113">For more information, see [Standard RAID levels](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span></span>   

<span data-ttu-id="11f07-114">Azure의 디스크 I/O 처리량 및 I/O 응답 시간은 RAID를 통해 향상될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-114">Disk I/O throughput and I/O response time in Azure can be improved through RAID.</span></span> <span data-ttu-id="11f07-115">이 테스트 랩 디스크 I/O 처리량을 두 개 수 및 I/O 응답 시간을 단축할 수 절반으로 평균 (두 개의 toofour, 4 개의 tooeight 등)에서 hello RAID 디스크 수가 두 배로 증가 하는 경우를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-115">Our lab tests show that disk I/O throughput can be doubled and I/O response time can be reduced by half on average when hello number of RAID disks is doubled (from two toofour, four tooeight, etc.).</span></span> <span data-ttu-id="11f07-116">자세한 내용은 [부록 A](#AppendixA) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11f07-116">See [Appendix A](#AppendixA) for details.</span></span>  

<span data-ttu-id="11f07-117">또한 toodisk I/O MySQL 성능이 향상 됩니다 hello RAID 수준을 높일 경우.</span><span class="sxs-lookup"><span data-stu-id="11f07-117">In addition toodisk I/O, MySQL performance improves when you increase hello RAID level.</span></span>  <span data-ttu-id="11f07-118">자세한 내용은 [부록 B](#AppendixB) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11f07-118">See [Appendix B](#AppendixB) for details.</span></span>  

<span data-ttu-id="11f07-119">Tooconsider hello 청크 크기를 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-119">You might also want tooconsider hello chunk size.</span></span> <span data-ttu-id="11f07-120">일반적으로 청크 크기가 크면 특히 대량 쓰기에서 오버헤드가 낮아집니다(특히 대량 쓰기의 경우).</span><span class="sxs-lookup"><span data-stu-id="11f07-120">In general, when you have a larger chunk size, you get lower overhead, especially for large writes.</span></span> <span data-ttu-id="11f07-121">그러나 hello 청크 크기가 너무 큰 경우 RAID 기능을 활용 하지 못하게 하는 추가 오버 헤드를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-121">However, when hello chunk size is too large, it might add additional overhead that prevents you from taking advantage of RAID.</span></span> <span data-ttu-id="11f07-122">hello 현재 기본 크기는 가장 일반적인 프로덕션 환경에 가장 적합 한 toobe이 확인 되는 512KB입니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-122">hello current default size is 512 KB, which is proven toobe optimal for most general production environments.</span></span> <span data-ttu-id="11f07-123">자세한 내용은 [부록 C](#AppendixC)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11f07-123">See [Appendix C](#AppendixC) for details.</span></span>   

<span data-ttu-id="11f07-124">여러 유형의 가상 컴퓨터에 추가할 수 있는 디스크 수에는 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-124">There are limits on how many disks you can add for different virtual machine types.</span></span> <span data-ttu-id="11f07-125">이러한 제한은 [Azure의 가상 컴퓨터 및 클라우드 서비스 크기](http://msdn.microsoft.com/library/azure/dn197896.aspx)에서 자세히 설명하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-125">These limits are detailed in [Virtual machine and cloud service sizes for Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span> <span data-ttu-id="11f07-126">더 적은 디스크와 tooset RAID 선택할 수는 있지만 4 개의 연결 된 데이터 디스크 toofollow hello RAID 예제에서는이 문서에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-126">You will need four attached data disks toofollow hello RAID example in this article, although you can choose tooset up RAID with fewer disks.</span></span>  

<span data-ttu-id="11f07-127">이 문서에서는 Linux 가상 컴퓨터를 이미 만들고 MYSQL을 설치 및 구성하는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-127">This article assumes you have already created a Linux virtual machine and have MYSQL installed and configured.</span></span> <span data-ttu-id="11f07-128">시작에 대 한 자세한 내용은 참조 하십시오. 어떻게 tooinstall Azure에서 MySQL.</span><span class="sxs-lookup"><span data-stu-id="11f07-128">For more information on getting started, see How tooinstall MySQL on Azure.</span></span>  

### <a name="set-up-raid-on-azure"></a><span data-ttu-id="11f07-129">Azure에서 RAID 설치</span><span class="sxs-lookup"><span data-stu-id="11f07-129">Set up RAID on Azure</span></span>
<span data-ttu-id="11f07-130">hello 다음 단계에서는 어떻게 toocreate RAID hello Azure 포털을 사용 하 여 Azure</span><span class="sxs-lookup"><span data-stu-id="11f07-130">hello following steps show how toocreate RAID on Azure by using hello Azure portal.</span></span> <span data-ttu-id="11f07-131">또한 Windows PowerShell 스크립트를 사용하여 RAID를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-131">You can also set up RAID by using Windows PowerShell scripts.</span></span>
<span data-ttu-id="11f07-132">이 예제에서는 디스크 4개를 사용하여 RAID 0을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-132">In this example, we will configure RAID 0 with four disks.</span></span>  

#### <a name="add-a-data-disk-tooyour-virtual-machine"></a><span data-ttu-id="11f07-133">데이터 디스크 tooyour 가상 컴퓨터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-133">Add a data disk tooyour virtual machine</span></span>
<span data-ttu-id="11f07-134">Hello Azure 포털에서에서 toohello 대시보드를 이동 하 고 hello 가상 컴퓨터 toowhich 원하는 tooadd 데이터 디스크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-134">In hello Azure portal, go toohello dashboard and select hello virtual machine toowhich you want tooadd a data disk.</span></span> <span data-ttu-id="11f07-135">이 예제에서는 hello 가상 컴퓨터가 mysqlnode1입니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-135">In this example, hello virtual machine is mysqlnode1.</span></span>  

<!--![Virtual machines][1]-->

<span data-ttu-id="11f07-136">**디스크**를 클릭한 다음 **새로 연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-136">Click **Disks** and then click **Attach New**.</span></span>

![가상 컴퓨터에서 디스크 추가](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-Disks-option.png)

<span data-ttu-id="11f07-138">새 500GB 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-138">Create a new 500 GB disk.</span></span> <span data-ttu-id="11f07-139">다음 사항을 확인 **호스트 캐시 기본 설정** 너무 설정**None**합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-139">Make sure that **Host Cache Preference** is set too**None**.</span></span>  <span data-ttu-id="11f07-140">작업을 완료하면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-140">When you're finished, click **OK**.</span></span>

![빈 디스크 연결](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-attach-empty-disk.png)


<span data-ttu-id="11f07-142">그러면 가상 컴퓨터에 빈 디스크 하나가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-142">This adds one empty disk into your virtual machine.</span></span> <span data-ttu-id="11f07-143">RAID의 데이터 디스크가 4개가 되도록 이 단계를 세 번 더 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-143">Repeat this step three more times so that you have four data disks for RAID.</span></span>  

<span data-ttu-id="11f07-144">추가 하는 hello를 볼 수 있습니다 hello 커널 메시지 로그를 확인 하 여 hello 가상 컴퓨터에서 구동 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-144">You can see hello added drives in hello virtual machine by looking at hello kernel message log.</span></span> <span data-ttu-id="11f07-145">예를 들어 toosee Ubuntu, 다음 명령을 사용 하 여 hello에 대 한:</span><span class="sxs-lookup"><span data-stu-id="11f07-145">For example, toosee this on Ubuntu, use hello following command:</span></span>  

    sudo grep SCSI /var/log/dmesg

#### <a name="create-raid-with-hello-additional-disks"></a><span data-ttu-id="11f07-146">추가 디스크 RAID hello로 만들기</span><span class="sxs-lookup"><span data-stu-id="11f07-146">Create RAID with hello additional disks</span></span>
<span data-ttu-id="11f07-147">hello 다음과 같은 단계로 진행 방법을 너무[소프트웨어 linux RAID 구성](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-147">hello following steps describe how too[configure software RAID on Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="11f07-148">Hello XFS 파일 시스템을 사용 하는 경우 hello RAID를 만든 후 다음 단계를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-148">If you are using hello XFS file system, execute hello following steps after you have created RAID.</span></span>
>
>

<span data-ttu-id="11f07-149">tooinstall XFS 다음 명령을 사용 하 여 hello Debian, Ubuntu, 또는 Linux Mint에서:</span><span class="sxs-lookup"><span data-stu-id="11f07-149">tooinstall XFS on Debian, Ubuntu, or Linux Mint, use hello following command:</span></span>  

    apt-get -y install xfsprogs  

<span data-ttu-id="11f07-150">tooinstall XFS 다음 명령을 사용 하 여 hello Fedora, CentOS, 또는 RHEL에:</span><span class="sxs-lookup"><span data-stu-id="11f07-150">tooinstall XFS on Fedora, CentOS, or RHEL, use hello following command:</span></span>  

    yum -y install xfsprogs  xfsdump


#### <a name="set-up-a-new-storage-path"></a><span data-ttu-id="11f07-151">새 저장소 경로 설정</span><span class="sxs-lookup"><span data-stu-id="11f07-151">Set up a new storage path</span></span>
<span data-ttu-id="11f07-152">다음 명령은 tooset 새 저장소 경로를 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="11f07-152">Use hello following command tooset up a new storage path:</span></span>  

    root@mysqlnode1:~# mkdir -p /RAID0/mysql

#### <a name="copy-hello-original-data-toohello-new-storage-path"></a><span data-ttu-id="11f07-153">원래 데이터 toohello hello 새 저장소 경로 복사</span><span class="sxs-lookup"><span data-stu-id="11f07-153">Copy hello original data toohello new storage path</span></span>
<span data-ttu-id="11f07-154">명령 toocopy 데이터 toohello 새 저장소 경로 따라 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-154">Use hello following command toocopy data toohello new storage path:</span></span>  

    root@mysqlnode1:~# cp -rp /var/lib/mysql/* /RAID0/mysql/

#### <a name="modify-permissions-so-mysql-can-access-read-and-write-hello-data-disk"></a><span data-ttu-id="11f07-155">(읽기 및 쓰기) MySQL에 액세스할 수 있도록 권한을 수정 hello 데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="11f07-155">Modify permissions so MySQL can access (read and write) hello data disk</span></span>
<span data-ttu-id="11f07-156">다음 명령은 toomodify 권한을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-156">Use hello following command toomodify permissions:</span></span>  

    root@mysqlnode1:~# chown -R mysql.mysql /RAID0/mysql && chmod -R 755 /RAID0/mysql


## <a name="adjust-hello-disk-io-scheduling-algorithm"></a><span data-ttu-id="11f07-157">알고리즘을 예약 하는 hello 디스크 I/O를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-157">Adjust hello disk I/O scheduling algorithm</span></span>
<span data-ttu-id="11f07-158">Linux에서는 다음 네 가지 유형의 I/O 일정 알고리즘을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-158">Linux implements four types of I/O scheduling algorithms:</span></span>  

* <span data-ttu-id="11f07-159">NOOP 알고리즘(작업 없음)</span><span class="sxs-lookup"><span data-stu-id="11f07-159">NOOP algorithm (No Operation)</span></span>
* <span data-ttu-id="11f07-160">Deadline 알고리즘(기한)</span><span class="sxs-lookup"><span data-stu-id="11f07-160">Deadline algorithm (Deadline)</span></span>
* <span data-ttu-id="11f07-161">Completely Fair Queuing 알고리즘(CFQ)</span><span class="sxs-lookup"><span data-stu-id="11f07-161">Completely fair queuing algorithm (CFQ)</span></span>
* <span data-ttu-id="11f07-162">Budget Period 알고리즘(예상)</span><span class="sxs-lookup"><span data-stu-id="11f07-162">Budget period algorithm (Anticipatory)</span></span>  

<span data-ttu-id="11f07-163">다양 한 시나리오 toooptimize 성능에서 다른 I/O 스케줄러를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-163">You can select different I/O schedulers under different scenarios toooptimize performance.</span></span> <span data-ttu-id="11f07-164">완전히 임의 액세스 환경에서 않습니다 CFQ hello 및 성능에 대 한 최종 기한에 도달한 알고리즘 간에 큰 차이.</span><span class="sxs-lookup"><span data-stu-id="11f07-164">In a completely random access environment, there is not a significant difference between hello CFQ and Deadline algorithms for performance.</span></span> <span data-ttu-id="11f07-165">안정성에 대 한 MySQL 데이터베이스 환경 tooDeadline hello를 설정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-165">We recommend that you set hello MySQL database environment tooDeadline for stability.</span></span> <span data-ttu-id="11f07-166">순차적 I/O가 많은 경우 CFQ로 인해 디스크 I/O 성능이 저하될 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-166">If there is a lot of sequential I/O, CFQ might reduce disk I/O performance.</span></span>   

<span data-ttu-id="11f07-167">SSD 및 다른 장비에 대 한 NOOP 또는 최종 기한에 도달한 hello 기본 스케줄러 보다 더 나은 성능을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-167">For SSD and other equipment, NOOP or Deadline can achieve better performance than hello default scheduler.</span></span>   

<span data-ttu-id="11f07-168">이전 toohello 커널 2.5, 알고리즘을 예약 하는 hello 기본 I/O 최종 기한입니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-168">Prior toohello kernel 2.5, hello default I/O scheduling algorithm is Deadline.</span></span> <span data-ttu-id="11f07-169">Hello 커널 2.6.18 부터는 CFQ hello 기본 I/O 예약 알고리즘 업체가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-169">Starting with hello kernel 2.6.18, CFQ became hello default I/O scheduling algorithm.</span></span>  <span data-ttu-id="11f07-170">커널 부팅 시이 설정을 지정할 수도 있고 hello 시스템에서 실행 중인 경우이 설정을 동적으로 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-170">You can specify this setting at kernel boot time or dynamically modify this setting when hello system is running.</span></span>  

<span data-ttu-id="11f07-171">다음 예제는 hello toocheck 집합과, 기본 스케줄러 toohello NOOP 알고리즘 hello Debian 배포 제품군의 hello 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-171">hello following example demonstrates how toocheck and set hello default scheduler toohello NOOP algorithm in hello Debian distribution family.</span></span>  

### <a name="view-hello-current-io-scheduler"></a><span data-ttu-id="11f07-172">보기 hello 현재 I/O 스케줄러</span><span class="sxs-lookup"><span data-stu-id="11f07-172">View hello current I/O scheduler</span></span>
<span data-ttu-id="11f07-173">tooview hello 스케줄러 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-173">tooview hello scheduler run hello following command:</span></span>  

    root@mysqlnode1:~# cat /sys/block/sda/queue/scheduler

<span data-ttu-id="11f07-174">Hello 현재 스케줄러를 나타내는 출력을 따라 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-174">You will see following output, which indicates hello current scheduler:</span></span>  

    noop [deadline] cfq


### <a name="change-hello-current-device-devsda-of-hello-io-scheduling-algorithm"></a><span data-ttu-id="11f07-175">Hello 현재 장치 (/ 개발/sda) hello I/O 예약 알고리즘의 변경</span><span class="sxs-lookup"><span data-stu-id="11f07-175">Change hello current device (/dev/sda) of hello I/O scheduling algorithm</span></span>
<span data-ttu-id="11f07-176">다음 명령을 toochange hello 현재 장치 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-176">Run hello following commands toochange hello current device:</span></span>  

    azureuser@mysqlnode1:~$ sudo su -
    root@mysqlnode1:~# echo "noop" >/sys/block/sda/queue/scheduler
    root@mysqlnode1:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
    root@mysqlnode1:~# update-grub

> [!NOTE]
> <span data-ttu-id="11f07-177">/dev/sda에 대해서만 이를 설정하는 것은 유용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-177">Setting this for /dev/sda alone is not useful.</span></span> <span data-ttu-id="11f07-178">Hello 데이터베이스가 있는 모든 데이터 디스크에 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-178">It must be set on all data disks where hello database resides.</span></span>  
>
>

<span data-ttu-id="11f07-179">다음 출력, grub.cfg 성공적으로 다시 작성 된 하 고 해당 hello 기본 스케줄러는 업데이트 된 tooNOOP 되었습니다 나타내는 hello를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-179">You should see hello following output, indicating that grub.cfg has been rebuilt successfully and that hello default scheduler has been updated tooNOOP:</span></span>  

    Generating grub configuration file ...
    Found linux image: /boot/vmlinuz-3.13.0-34-generic
    Found initrd image: /boot/initrd.img-3.13.0-34-generic
    Found linux image: /boot/vmlinuz-3.13.0-32-generic
    Found initrd image: /boot/initrd.img-3.13.0-32-generic
    Found memtest86+ image: /memtest86+.elf
    Found memtest86+ image: /memtest86+.bin
    done

<span data-ttu-id="11f07-180">Red Hat 배포 제품군 hello에 대 한만 다음 명령을 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="11f07-180">For hello Red Hat distribution family, you need only hello following command:</span></span>

    echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local

## <a name="configure-system-file-operations-settings"></a><span data-ttu-id="11f07-181">시스템 파일 작업 설정 구성</span><span class="sxs-lookup"><span data-stu-id="11f07-181">Configure system file operations settings</span></span>
<span data-ttu-id="11f07-182">최상의 방법 중 하나는 toodisable hello *하나만* hello 파일 시스템에 로깅 기능.</span><span class="sxs-lookup"><span data-stu-id="11f07-182">One best practice is toodisable hello *atime* logging feature on hello file system.</span></span> <span data-ttu-id="11f07-183">hello 마지막 파일 액세스 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-183">Atime is hello last file access time.</span></span> <span data-ttu-id="11f07-184">파일에 액세스할 때마다 hello 파일 시스템 레코드 hello hello 로그에 타임 스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-184">Whenever a file is accessed, hello file system records hello timestamp in hello log.</span></span> <span data-ttu-id="11f07-185">그러나 이 정보는 거의 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-185">However, this information is rarely used.</span></span> <span data-ttu-id="11f07-186">필요하지 않은 경우 사용하지 않도록 설정하여 전체 디스크 액세스 시간을 단축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-186">You can disable it if you don't need it, which will reduce overall disk access time.</span></span>  

<span data-ttu-id="11f07-187">toodisable 하나만 로깅, toomodify hello 파일 시스템 구성 파일 /etc/ fstab 필요한 추가 하는 hello **noatime** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-187">toodisable atime logging, you need toomodify hello file system configuration file /etc/ fstab and add hello **noatime** option.</span></span>  

<span data-ttu-id="11f07-188">예를 들어 hello 다음 예제와 같이 hello noatime 추가 hello vim /etc/fstab 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-188">For example, edit hello vim /etc/fstab file, adding hello noatime as shown in hello following sample:</span></span>  

    # CLOUD_IMG: This file was created/modified by hello Cloud Image build process
    UUID=3cc98c06-d649-432d-81df-6dcd2a584d41       /        ext4   defaults,discard        0 0
    #Add hello “noatime” option below toodisable atime logging
    UUID="431b1e78-8226-43ec-9460-514a9adf060e"     /RAID0   xfs   defaults,nobootwait, noatime 0 0
    /dev/sdb1       /mnt    auto    defaults,nobootwait,comment=cloudconfig 0       2

<span data-ttu-id="11f07-189">그런 다음 다음 명령을 hello로 hello 파일 시스템을 다시 탑재:</span><span class="sxs-lookup"><span data-stu-id="11f07-189">Then, remount hello file system with hello following command:</span></span>  

    mount -o remount /RAID0

<span data-ttu-id="11f07-190">테스트 hello 결과 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-190">Test hello modified result.</span></span> <span data-ttu-id="11f07-191">Hello 테스트 파일을 수정 하면 hello 액세스 시간이 업데이트 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-191">When you modify hello test file, hello access time is not updated.</span></span> <span data-ttu-id="11f07-192">다음 예제에서는 보여 수정 전후의 hello 코드 처럼 보이는 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-192">hello following examples show what hello code looks like before and after modification.</span></span>

<span data-ttu-id="11f07-193">이전:</span><span class="sxs-lookup"><span data-stu-id="11f07-193">Before:</span></span>        

![액세스 수정 이전 코드][5]

<span data-ttu-id="11f07-195">이후:</span><span class="sxs-lookup"><span data-stu-id="11f07-195">After:</span></span>

![액세스 수정 이후 코드][6]

## <a name="increase-hello-maximum-number-of-system-handles-for-high-concurrency"></a><span data-ttu-id="11f07-197">Hello 높은 동시성에 대 한 시스템 핸들의 최대 수 증가</span><span class="sxs-lookup"><span data-stu-id="11f07-197">Increase hello maximum number of system handles for high concurrency</span></span>
<span data-ttu-id="11f07-198">MySQL은 동시성이 뛰어난 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-198">MySQL is a high concurrency database.</span></span> <span data-ttu-id="11f07-199">hello 기본 동시 핸들 수는 Linux 용 1024 항상 충분 한지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-199">hello default number of concurrent handles is 1024 for Linux, which is not always sufficient.</span></span> <span data-ttu-id="11f07-200">다음 단계 tooincrease hello 최대 동시 핸들 hello 시스템 toosupport MySQL의 높은 동시성 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-200">Use hello following steps tooincrease hello maximum concurrent handles of hello system toosupport high concurrency of MySQL.</span></span>

### <a name="modify-hello-limitsconf-file"></a><span data-ttu-id="11f07-201">Hello limits.conf 파일 수정</span><span class="sxs-lookup"><span data-stu-id="11f07-201">Modify hello limits.conf file</span></span>
<span data-ttu-id="11f07-202">tooincrease hello 최대 동시 처리를 허용 하 고 hello hello /etc/security/limits.conf 파일에 있는 4 개의 줄을 다음 추가 하세요.</span><span class="sxs-lookup"><span data-stu-id="11f07-202">tooincrease hello maximum allowed concurrent handles, add hello following four lines in hello /etc/security/limits.conf file.</span></span> <span data-ttu-id="11f07-203">65536은 시스템 hello hello 최대 수를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-203">Note that 65536 is hello maximum number that hello system can support.</span></span>   

    * <span data-ttu-id="11f07-204">soft nofile 65536</span><span class="sxs-lookup"><span data-stu-id="11f07-204">soft nofile 65536</span></span>
    * <span data-ttu-id="11f07-205">hard nofile 65536</span><span class="sxs-lookup"><span data-stu-id="11f07-205">hard nofile 65536</span></span>
    * <span data-ttu-id="11f07-206">soft nproc 65536</span><span class="sxs-lookup"><span data-stu-id="11f07-206">soft nproc 65536</span></span>
    * <span data-ttu-id="11f07-207">hard nproc 65536</span><span class="sxs-lookup"><span data-stu-id="11f07-207">hard nproc 65536</span></span>

### <a name="update-hello-system-for-hello-new-limits"></a><span data-ttu-id="11f07-208">Hello 새로운 제한에 대 한 hello 시스템 업데이트</span><span class="sxs-lookup"><span data-stu-id="11f07-208">Update hello system for hello new limits</span></span>
<span data-ttu-id="11f07-209">다음 명령을 hello 실행 tooupdate hello 시스템:</span><span class="sxs-lookup"><span data-stu-id="11f07-209">tooupdate hello system, run hello following commands:</span></span>  

    ulimit -SHn 65536
    ulimit -SHu 65536

### <a name="ensure-that-hello-limits-are-updated-at-boot-time"></a><span data-ttu-id="11f07-210">부팅 시 hello 제한을 업데이트 합니다</span><span class="sxs-lookup"><span data-stu-id="11f07-210">Ensure that hello limits are updated at boot time</span></span>
<span data-ttu-id="11f07-211">이 적용 되도록 부팅 시 hello /etc/rc.local 파일에서 시작 명령을 수행 하는 hello를 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-211">Put hello following startup commands in hello /etc/rc.local file so it will take effect at boot time.</span></span>  

    echo “ulimit -SHn 65536” >>/etc/rc.local
    echo “ulimit -SHu 65536” >>/etc/rc.local

## <a name="mysql-database-optimization"></a><span data-ttu-id="11f07-212">MySQL 데이터베이스 최적화</span><span class="sxs-lookup"><span data-stu-id="11f07-212">MySQL database optimization</span></span>
<span data-ttu-id="11f07-213">Azure에서 MySQL tooconfigure에서는 온-프레미스 컴퓨터에서 사용 하 여 동일한 성능 조정 전략 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-213">tooconfigure MySQL on Azure, you can use hello same performance-tuning strategy you use on an on-premises machine.</span></span>  

<span data-ttu-id="11f07-214">hello 주 I/O 최적화 규칙은입니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-214">hello main I/O optimization rules are:</span></span>   

* <span data-ttu-id="11f07-215">Hello 캐시 크기를 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-215">Increase hello cache size.</span></span>
* <span data-ttu-id="11f07-216">I/O 응답 시간 감소</span><span class="sxs-lookup"><span data-stu-id="11f07-216">Reduce I/O response time.</span></span>  

<span data-ttu-id="11f07-217">MySQL 서버 설정을 toooptimize hello my.cnf 파일은 서버와 클라이언트 컴퓨터에 대 한 hello 기본 구성 파일을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-217">toooptimize MySQL server settings, you can update hello my.cnf file, which is hello default configuration file for both server and client computers.</span></span>  

<span data-ttu-id="11f07-218">hello 다음 구성 항목은 MySQL 성능에 영향을 주는 주요 요소를 hello:</span><span class="sxs-lookup"><span data-stu-id="11f07-218">hello following configuration items are hello main factors that affect MySQL performance:</span></span>  

* <span data-ttu-id="11f07-219">**innodb_buffer_pool_size**: 버퍼링 된 데이터 및 hello 인덱스 hello 버퍼 풀을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-219">**innodb_buffer_pool_size**: hello buffer pool contains buffered data and hello index.</span></span> <span data-ttu-id="11f07-220">일반적으로 실제 메모리의 too70 %를 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-220">This is usually set too70 percent of physical memory.</span></span>
* <span data-ttu-id="11f07-221">**innodb_log_file_size**: hello 다시 실행 로그 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-221">**innodb_log_file_size**: This is hello redo log size.</span></span> <span data-ttu-id="11f07-222">충돌이 발생 한 후 쓰기 작업은 안정적이 고 복구 가능한 빠른는 다시 실행 로그 tooensure를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-222">You use redo logs tooensure that write operations are fast, reliable, and recoverable after a crash.</span></span> <span data-ttu-id="11f07-223">이 제공 하의 공간이 충분 한 쓰기 작업의 로깅을 위한 too512 MB 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-223">This is set too512 MB, which will give you plenty of space for logging write operations.</span></span>
* <span data-ttu-id="11f07-224">**max_connections**: 일부 응용 프로그램은 연결을 제대로 닫지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-224">**max_connections**: Sometimes applications do not close connections properly.</span></span> <span data-ttu-id="11f07-225">더 큰 값을 더 많은 시간이 toorecycle 연결 유휴 상태인 hello 서버를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-225">A larger value will give hello server more time toorecycle idled connections.</span></span> <span data-ttu-id="11f07-226">hello 최대 연결 수는 10, 000 않으며 hello 권장 최대값은 5000입니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-226">hello maximum number of connections is 10,000, but hello recommended maximum is 5,000.</span></span>
* <span data-ttu-id="11f07-227">**Innodb_file_per_table**:이 설정을 사용 하거나 별도 파일에 InnoDB toostore 테이블의 hello 기능을 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-227">**Innodb_file_per_table**: This setting enables or disables hello ability of InnoDB toostore tables in separate files.</span></span> <span data-ttu-id="11f07-228">Hello 옵션 tooensure 몇 가지 세밀된 하 게 관리 작업 효율적으로 적용 될 수 있도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-228">Turn on hello option tooensure that several advanced administration operations can be applied efficiently.</span></span> <span data-ttu-id="11f07-229">성능 관점에서 수 hello 테이블 공간 전송 속도 고 hello 이물질이 관리 성능을 최적화 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-229">From a performance point of view, it can speed up hello table space transmission and optimize hello debris management performance.</span></span> <span data-ttu-id="11f07-230">hello가 ON이이 옵션에 대해 설정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-230">hello recommended setting for this option is ON.</span></span></br></br>
<span data-ttu-id="11f07-231">MySQL 5.6 hello 기본값은 ON 이므로 동작은 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-231">From MySQL 5.6, hello default setting is ON, so no action is required.</span></span> <span data-ttu-id="11f07-232">이전 버전에 대 한 hello 기본 설정은 OFF입니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-232">For earlier versions, hello default setting is OFF.</span></span> <span data-ttu-id="11f07-233">hello 설정은 새로 만든된 테이블에 영향을 주므로 데이터를 로드 하기 전에 변경 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-233">hello setting should be changed before data is loaded, because only newly created tables are affected.</span></span>
* <span data-ttu-id="11f07-234">**innodb_flush_log_at_trx_commit**: hello로 범위가 설정 too0, hello 기본값은 1 ~ 2입니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-234">**innodb_flush_log_at_trx_commit**: hello default value is 1, with hello scope set too0~2.</span></span> <span data-ttu-id="11f07-235">hello 기본값은 독립 실행형 MySQL DB에 대 한 hello 가장 적합 한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-235">hello default value is hello most suitable option for standalone MySQL DB.</span></span> <span data-ttu-id="11f07-236">2 사용의 hello 설정에는 대부분의 데이터 무결성 hello 이며 마스터 MySQL 클러스터에 대해 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-236">hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL Cluster.</span></span> <span data-ttu-id="11f07-237">hello 0 안정성 (일부 경우에 보다 나은 성능)에 영향을 줄 수 있으며 슬레이브 MySQL 클러스터에 대 한 적합 한 데이터 손실이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-237">hello setting of 0 allows data loss, which can affect reliability (in some cases with better performance), and is suitable for Slave in MySQL Cluster.</span></span>
* <span data-ttu-id="11f07-238">**Innodb_log_buffer_size**: hello 로그 버퍼 hello 트랜잭션 커밋 전에 tooflush hello 로그 toodisk 필요 없이 트랜잭션을 toorun 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-238">**Innodb_log_buffer_size**: hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit.</span></span> <span data-ttu-id="11f07-239">그러나 큰 이진 개체 또는 텍스트 필드가 있는 경우 hello 캐시를 신속 하 게 사용 됩니다 하 고 자주 디스크 I/O 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-239">However, if there is large binary object or text field, hello cache will be consumed quickly and frequent disk I/O will be triggered.</span></span> <span data-ttu-id="11f07-240">더 잘 Innodb_log_waits 상태 변수 없으면 hello 버퍼 크기를 늘릴는 0입니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-240">It is better increase hello buffer size if Innodb_log_waits state variable is not 0.</span></span>
* <span data-ttu-id="11f07-241">**query_cache_size**: hello 최선의 선택은 toodisable hello 처음에 옵니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-241">**query_cache_size**: hello best option is toodisable it from hello outset.</span></span> <span data-ttu-id="11f07-242">Query_cache_size too0 (이 MySQL 5.6 hello 기본 설정)를 설정 하 고 쿼리를 다른 메서드에 toospeed를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-242">Set query_cache_size too0 (this is hello default setting in MySQL 5.6) and use other methods toospeed up queries.</span></span>  

<span data-ttu-id="11f07-243">참조 [부록 D](#AppendixD) hello 최적화 전후의 성능 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-243">See [Appendix D](#AppendixD) for a comparison of performance before and after hello optimization.</span></span>

## <a name="turn-on-hello-mysql-slow-query-log-for-analyzing-hello-performance-bottleneck"></a><span data-ttu-id="11f07-244">Hello 성능 병목 상태를 분석 하기 위한 hello MySQL 느린 쿼리 로그 설정</span><span class="sxs-lookup"><span data-stu-id="11f07-244">Turn on hello MySQL slow query log for analyzing hello performance bottleneck</span></span>
<span data-ttu-id="11f07-245">hello MySQL 느린 쿼리 로그 MySQL에 대 한 hello 느린 쿼리를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-245">hello MySQL slow query log can help you identify hello slow queries for MySQL.</span></span> <span data-ttu-id="11f07-246">Hello MySQL 느린 쿼리 로그를 사용 하도록 설정한 후 같은 MySQL 도구를 사용할 수 있습니다 **mysqldumpslow** tooidentify hello 성능 병목 상태가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-246">After enabling hello MySQL slow query log, you can use MySQL tools like **mysqldumpslow** tooidentify hello performance bottleneck.</span></span>  

<span data-ttu-id="11f07-247">기본적으로 이 옵션은 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-247">By default, this is not enabled.</span></span> <span data-ttu-id="11f07-248">Hello 느린 쿼리 로그를 켜는 일부 CPU 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-248">Turning on hello slow query log might consume some CPU resources.</span></span> <span data-ttu-id="11f07-249">성능 병목 문제를 해결하기 위해 이 옵션을 일시적으로 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-249">We recommend that you enable this temporarily for troubleshooting performance bottlenecks.</span></span> <span data-ttu-id="11f07-250">hello 느린 쿼리 로그에 tooturn:</span><span class="sxs-lookup"><span data-stu-id="11f07-250">tooturn on hello slow query log:</span></span>

1. <span data-ttu-id="11f07-251">Hello toohello 끝 줄 다음에 추가 하 여 hello my.cnf 파일을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-251">Modify hello my.cnf file by adding hello following lines toohello end:</span></span>

        long_query_time = 2
        slow_query_log = 1
        slow_query_log_file = /RAID0/mysql/mysql-slow.log

2. <span data-ttu-id="11f07-252">Hello MySQL 서버를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-252">Restart hello MySQL server.</span></span>

        service  mysql  restart

3. <span data-ttu-id="11f07-253">여부 hello 설정을 적용 하 hello를 사용 하 여 확인 **표시** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-253">Check whether hello setting is taking effect by using hello **show** command.</span></span>

![Slow-query-log ON][7]   

![Slow-query-log results][8]

<span data-ttu-id="11f07-256">이 예제에서는 hello 느린 쿼리 기능을 켜 졌습니다 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-256">In this example, you can see that hello slow query feature has been turned on.</span></span> <span data-ttu-id="11f07-257">Hello를 사용 하 여 있습니다 **mysqldumpslow** toodetermine 성능 병목 현상을 도구 및 인덱스를 추가 하는 등의 성능을 최적화 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-257">You can then use hello **mysqldumpslow** tool toodetermine performance bottlenecks and optimize performance, such as adding indexes.</span></span>

## <a name="appendices"></a><span data-ttu-id="11f07-258">부록</span><span class="sxs-lookup"><span data-stu-id="11f07-258">Appendices</span></span>
<span data-ttu-id="11f07-259">hello 다음은 샘플 성능 테스트 데이터 대상으로 지정 된 랩 환경에서 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-259">hello following are sample performance test data produced in a targeted lab environment.</span></span> <span data-ttu-id="11f07-260">다양 한 성능 조정 방법으로 일반 배경 hello 성능 데이터 추세에 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-260">They provide general background on hello performance data trend with different performance tuning approaches.</span></span> <span data-ttu-id="11f07-261">hello 결과 서로 다른 환경 또는 제품 버전에서 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-261">hello results might vary under different environment or product versions.</span></span>

### <span data-ttu-id="11f07-262"><a name="AppendixA"></a>부록 A</span><span class="sxs-lookup"><span data-stu-id="11f07-262"><a name="AppendixA"></a>Appendix A</span></span>  
<span data-ttu-id="11f07-263">**RAID 수준별 디스크 성능(IOPS)**</span><span class="sxs-lookup"><span data-stu-id="11f07-263">**Disk performance (IOPS) with different RAID levels**</span></span>

![RAID 수준별 디스크 IOPS][9]

<span data-ttu-id="11f07-265">**테스트 명령**</span><span class="sxs-lookup"><span data-stu-id="11f07-265">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=5G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite

> [!NOTE]
> <span data-ttu-id="11f07-266">이 테스트의 작업 부하 hello tooreach hello의 상한값 RAID 시도 64 개 스레드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-266">hello workload of this test uses 64 threads, trying tooreach hello upper limit of RAID.</span></span>
>
>

### <span data-ttu-id="11f07-267"><a name="AppendixB"></a>부록 B</span><span class="sxs-lookup"><span data-stu-id="11f07-267"><a name="AppendixB"></a>Appendix B</span></span>  
<span data-ttu-id="11f07-268">**RAID 수준별 MySQL 성능(처리량) 비교** </span><span class="sxs-lookup"><span data-stu-id="11f07-268">**MySQL performance (throughput) comparison with different RAID levels** </span></span>  
<span data-ttu-id="11f07-269">(XFS 파일 시스템)</span><span class="sxs-lookup"><span data-stu-id="11f07-269">(XFS file system)</span></span>

![RAID 수준별 MySQL 성능 비교][10]  
![RAID 수준별 MySQL 성능 비교][11]

<span data-ttu-id="11f07-272">**테스트 명령**</span><span class="sxs-lookup"><span data-stu-id="11f07-272">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb

<span data-ttu-id="11f07-273">**RAID 수준별 MySQL 성능(OLTP) 비교**</span><span class="sxs-lookup"><span data-stu-id="11f07-273">**MySQL performance (OLTP) comparison with different RAID levels**</span></span>  
<span data-ttu-id="11f07-274">![RAID 수준별 MySQL 성능(OLTP) 비교][12]</span><span class="sxs-lookup"><span data-stu-id="11f07-274">![MySQL performance (OLTP) comparison with different RAID levels][12]</span></span>

<span data-ttu-id="11f07-275">**테스트 명령**</span><span class="sxs-lookup"><span data-stu-id="11f07-275">**Test commands**</span></span>

    time sysbench --test=oltp --db-driver=mysql --mysql-user=root --mysql-password=0ps.123  --mysql-table-engine=innodb --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-socket=/var/run/mysqld/mysqld.sock --mysql-db=test --oltp-table-size=1000000 prepare

### <span data-ttu-id="11f07-276"><a name="AppendixC"></a>부록 C</span><span class="sxs-lookup"><span data-stu-id="11f07-276"><a name="AppendixC"></a>Appendix C</span></span>   
<span data-ttu-id="11f07-277">**청크 크기별 디스크 성능(IOPS) 비교**</span><span class="sxs-lookup"><span data-stu-id="11f07-277">**Disk performance (IOPS) comparison for different chunk sizes**</span></span>  
<span data-ttu-id="11f07-278">(XFS 파일 시스템)</span><span class="sxs-lookup"><span data-stu-id="11f07-278">(XFS file system)</span></span>

![][13]

<span data-ttu-id="11f07-279">**테스트 명령**</span><span class="sxs-lookup"><span data-stu-id="11f07-279">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=30G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite
    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=1G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite  

<span data-ttu-id="11f07-280">이 테스트에 사용 되는 hello 파일 크기는 각각 된 30GB 및 1 g B, RAID 0 (4 개) XFS 파일 시스템과 합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-280">hello file sizes used for this testing are 30 GB and 1 GB, respectively, with RAID 0 (4 disks) XFS file system.</span></span>

### <span data-ttu-id="11f07-281"><a name="AppendixD"></a>부록 D</span><span class="sxs-lookup"><span data-stu-id="11f07-281"><a name="AppendixD"></a>Appendix D</span></span>  
<span data-ttu-id="11f07-282">**최적화 전후의 MySQL 성능(처리량) 비교**</span><span class="sxs-lookup"><span data-stu-id="11f07-282">**MySQL performance (throughput) comparison before and after optimization**</span></span>  
<span data-ttu-id="11f07-283">(XFS 파일 시스템)</span><span class="sxs-lookup"><span data-stu-id="11f07-283">(XFS File System)</span></span>

![최적화 전후의 MySQL 성능(처리량) 비교][14]

<span data-ttu-id="11f07-285">**테스트 명령**</span><span class="sxs-lookup"><span data-stu-id="11f07-285">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb,misam

<span data-ttu-id="11f07-286">**hello 구성 설정 기본 인스턴스 및 최적화는 다음과 같습니다.**</span><span class="sxs-lookup"><span data-stu-id="11f07-286">**hello configuration setting for default and optimization is as follows:**</span></span>

| <span data-ttu-id="11f07-287">매개 변수</span><span class="sxs-lookup"><span data-stu-id="11f07-287">Parameters</span></span> | <span data-ttu-id="11f07-288">기본값</span><span class="sxs-lookup"><span data-stu-id="11f07-288">Default</span></span> | <span data-ttu-id="11f07-289">최적화</span><span class="sxs-lookup"><span data-stu-id="11f07-289">Optimization</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11f07-290">**innodb_buffer_pool_size**</span><span class="sxs-lookup"><span data-stu-id="11f07-290">**innodb_buffer_pool_size**</span></span> |<span data-ttu-id="11f07-291">없음</span><span class="sxs-lookup"><span data-stu-id="11f07-291">None</span></span> |<span data-ttu-id="11f07-292">7 GB</span><span class="sxs-lookup"><span data-stu-id="11f07-292">7 GB</span></span> |
| <span data-ttu-id="11f07-293">**innodb_log_file_size**</span><span class="sxs-lookup"><span data-stu-id="11f07-293">**innodb_log_file_size**</span></span> |<span data-ttu-id="11f07-294">5MB</span><span class="sxs-lookup"><span data-stu-id="11f07-294">5 MB</span></span> |<span data-ttu-id="11f07-295">512MB</span><span class="sxs-lookup"><span data-stu-id="11f07-295">512 MB</span></span> |
| <span data-ttu-id="11f07-296">**max_connections**</span><span class="sxs-lookup"><span data-stu-id="11f07-296">**max_connections**</span></span> |<span data-ttu-id="11f07-297">100</span><span class="sxs-lookup"><span data-stu-id="11f07-297">100</span></span> |<span data-ttu-id="11f07-298">5000</span><span class="sxs-lookup"><span data-stu-id="11f07-298">5000</span></span> |
| <span data-ttu-id="11f07-299">**innodb_file_per_table**</span><span class="sxs-lookup"><span data-stu-id="11f07-299">**innodb_file_per_table**</span></span> |<span data-ttu-id="11f07-300">0</span><span class="sxs-lookup"><span data-stu-id="11f07-300">0</span></span> |<span data-ttu-id="11f07-301">1</span><span class="sxs-lookup"><span data-stu-id="11f07-301">1</span></span> |
| <span data-ttu-id="11f07-302">**innodb_flush_log_at_trx_commit**</span><span class="sxs-lookup"><span data-stu-id="11f07-302">**innodb_flush_log_at_trx_commit**</span></span> |<span data-ttu-id="11f07-303">1</span><span class="sxs-lookup"><span data-stu-id="11f07-303">1</span></span> |<span data-ttu-id="11f07-304">2</span><span class="sxs-lookup"><span data-stu-id="11f07-304">2</span></span> |
| <span data-ttu-id="11f07-305">**innodb_log_buffer_size**</span><span class="sxs-lookup"><span data-stu-id="11f07-305">**innodb_log_buffer_size**</span></span> |<span data-ttu-id="11f07-306">8MB</span><span class="sxs-lookup"><span data-stu-id="11f07-306">8 MB</span></span> |<span data-ttu-id="11f07-307">128MB</span><span class="sxs-lookup"><span data-stu-id="11f07-307">128 MB</span></span> |
| <span data-ttu-id="11f07-308">**query_cache_size**</span><span class="sxs-lookup"><span data-stu-id="11f07-308">**query_cache_size**</span></span> |<span data-ttu-id="11f07-309">16MB</span><span class="sxs-lookup"><span data-stu-id="11f07-309">16 MB</span></span> |<span data-ttu-id="11f07-310">0</span><span class="sxs-lookup"><span data-stu-id="11f07-310">0</span></span> |

<span data-ttu-id="11f07-311">에 대 한 더 자세한 [최적화 구성 매개 변수](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), toohello 참조 [MySQL 공식 지침](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method)합니다.</span><span class="sxs-lookup"><span data-stu-id="11f07-311">For more detailed [optimization configuration parameters](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), refer toohello [MySQL official instructions](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span></span>  

  <span data-ttu-id="11f07-312">**테스트 환경**</span><span class="sxs-lookup"><span data-stu-id="11f07-312">**Test environment**</span></span>  

| <span data-ttu-id="11f07-313">하드웨어</span><span class="sxs-lookup"><span data-stu-id="11f07-313">Hardware</span></span> | <span data-ttu-id="11f07-314">세부 정보</span><span class="sxs-lookup"><span data-stu-id="11f07-314">Details</span></span> |
| --- | --- |
| <span data-ttu-id="11f07-315">CPU</span><span class="sxs-lookup"><span data-stu-id="11f07-315">CPU</span></span> |<span data-ttu-id="11f07-316">AMD Opteron(tm) 프로세서 4171 HE/4 코어</span><span class="sxs-lookup"><span data-stu-id="11f07-316">AMD Opteron(tm) Processor 4171 HE/4 cores</span></span> |
| <span data-ttu-id="11f07-317">메모리</span><span class="sxs-lookup"><span data-stu-id="11f07-317">Memory</span></span> |<span data-ttu-id="11f07-318">14 GB</span><span class="sxs-lookup"><span data-stu-id="11f07-318">14 GB</span></span> |
| <span data-ttu-id="11f07-319">디스크</span><span class="sxs-lookup"><span data-stu-id="11f07-319">Disk</span></span> |<span data-ttu-id="11f07-320">10GB/디스크</span><span class="sxs-lookup"><span data-stu-id="11f07-320">10 GB/disk</span></span> |
| <span data-ttu-id="11f07-321">OS</span><span class="sxs-lookup"><span data-stu-id="11f07-321">OS</span></span> |<span data-ttu-id="11f07-322">Ubuntu 14.04.1 LTS</span><span class="sxs-lookup"><span data-stu-id="11f07-322">Ubuntu 14.04.1 LTS</span></span> |

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

