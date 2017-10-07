---
title: "AWS tooAzure에서 Vm aaaMigrate | Microsoft Docs"
description: "이 문서에서 설명 하는 방법을 toomigrate 가상 컴퓨터가 실행 중에 Azure Site Recovery를 사용 하 여 웹 서비스 AWS (Amazon) tooAzure 합니다."
services: site-recovery
documentationcenter: 
author: bsiva
manager: jwhit
editor: 
ms.assetid: ddb412fd-32a8-4afa-9e39-738b11b91118
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: c99b781ec9cca5b8f9a847d3fc48408062b120b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-tooazure-with-azure-site-recovery"></a><span data-ttu-id="59b66-103">웹 서비스 AWS (Amazon) tooAzure Azure 사이트 복구에서 가상 컴퓨터 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="59b66-103">Migrate virtual machines in Amazon Web Services (AWS) tooAzure with Azure Site Recovery</span></span>

<span data-ttu-id="59b66-104">이 문서에서는 toomigrate AWS Windows hello로 tooAzure 가상 컴퓨터 인스턴스 하는 방법을 설명 [Azure Site Recovery](site-recovery-overview.md) 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="59b66-104">This article describes how toomigrate AWS Windows instances tooAzure virtual machines with hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="59b66-105">마이그레이션은 장애 조치 AWS tooAzure에서 효과적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b66-105">Migration is effectively a failover from AWS tooAzure.</span></span> <span data-ttu-id="59b66-106">장애 복구 컴퓨터 tooAWS 없으며 지속적인 복제가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="59b66-106">You can't failback machines tooAWS, and there's no ongoing replication.</span></span> <span data-ttu-id="59b66-107">이 문서에서는 hello hello Azure 포털에서에서 마이그레이션 단계를 설명 하 고에 대 한 hello 지침에 따라 [물리적 컴퓨터 tooAzure 복제](site-recovery-vmware-to-azure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="59b66-107">This article describes hello steps for migration in hello Azure portal, and are based on hello instructions for [replicating a physical machine tooAzure](site-recovery-vmware-to-azure.md).</span></span>

<span data-ttu-id="59b66-108">Hello 또는이 문서의 hello 맨 아래에 설명 이나 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="59b66-108">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="59b66-109">지원되는 운영 체제</span><span class="sxs-lookup"><span data-stu-id="59b66-109">Supported operating systems</span></span>

<span data-ttu-id="59b66-110">사이트 복구에 사용 되는 toomigrate EC2 인스턴스 hello 다음 운영 체제 중 하나를 실행 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b66-110">Site Recovery can be used toomigrate EC2 instances running any of hello following operating systems:</span></span>

- <span data-ttu-id="59b66-111">Windows(64비트만 해당)</span><span class="sxs-lookup"><span data-stu-id="59b66-111">Windows(64 bit only)</span></span>
    - <span data-ttu-id="59b66-112">Windows Server 2008 R2 SP1+(Citrix PV 드라이버 또는 AWS PV 드라이버만 해당.</span><span class="sxs-lookup"><span data-stu-id="59b66-112">Windows Server 2008 R2 SP1+ (Citrix PV drivers or AWS PV drivers only.</span></span> <span data-ttu-id="59b66-113">**RedHat PV 드라이버를 실행하는 인스턴스가 지원되지 않습니다**)Windows Server 2012 Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="59b66-113">**Instances running RedHat PV drivers are not supported**) Windows Server 2012 Windows Server 2012 R2</span></span>
- <span data-ttu-id="59b66-114">Linux(64비트만 해당)</span><span class="sxs-lookup"><span data-stu-id="59b66-114">Linux (64 bit only)</span></span>
    - <span data-ttu-id="59b66-115">Red Hat Enterprise Linux 6.7(HVM 가상화된 인스턴스만 해당)</span><span class="sxs-lookup"><span data-stu-id="59b66-115">Red Hat Enterprise Linux 6.7 (HVM virtualized instances only)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59b66-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="59b66-116">Prerequisites</span></span>

<span data-ttu-id="59b66-117">이 배포에 대해 필요한 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="59b66-117">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="59b66-118">**구성 서버**: hello 구성 서버와 Windows Server 2012 r 2를 실행 하는 An Amazon EC2 VM을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b66-118">**Configuration server**: An Amazon EC2 VM running Windows Server 2012 R2 is deployed as hello configuration server.</span></span> <span data-ttu-id="59b66-119">기본적으로 hello 다른 Azure Site Recovery 구성 요소 (프로세스 서버 및 마스터 대상 서버) 설치 된 hello 구성 서버를 배포할 때.</span><span class="sxs-lookup"><span data-stu-id="59b66-119">By default, hello other Azure Site Recovery components (process server and master target server) are installed when you deploy hello configuration server.</span></span> <span data-ttu-id="59b66-120">이 문서에서는 hello hello Azure 포털에서에서 마이그레이션 단계를 설명 하 고에 대 한 hello 지침에 따라 [자세한 정보](site-recovery-components.md)</span><span class="sxs-lookup"><span data-stu-id="59b66-120">This article describes hello steps for migration in hello Azure portal, and are based on hello instructions for  [Learn more](site-recovery-components.md)</span></span>

* <span data-ttu-id="59b66-121">**EC2 인스턴스**: Amazon EC2 가상 컴퓨터 인스턴스를 원하는 toomigrate hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b66-121">**EC2 instances**: hello Amazon EC2 virtual machines instances that you want toomigrate.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="59b66-122">배포 단계</span><span class="sxs-lookup"><span data-stu-id="59b66-122">Deployment steps</span></span>

1. <span data-ttu-id="59b66-123">Recovery Services 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="59b66-123">Create a Recovery Services vault.</span></span>
2. <span data-ttu-id="59b66-124">hello EC2 인스턴스의 보안 그룹 구성 된 규칙 tooallow 통신 toodeploy hello 구성 서버 하려는 hello 인스턴스와 toomigrate, 원하는 hello EC2 인스턴스 사이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b66-124">hello Security Group of your EC2 instances should have rules configured tooallow communication between hello EC2 instance that you want toomigrate, and hello instance on which you plan toodeploy hello Configuration Server.</span></span>

3. <span data-ttu-id="59b66-125">Hello에 동일한 Amazon 가상 사설 클라우드 EC2 인스턴스로 ASR 구성 서버를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b66-125">On hello same Amazon Virtual Private Cloud as your EC2 instances, deploy an ASR configuration server.</span></span> <span data-ttu-id="59b66-126">Hello VMware 참조 실제 / 구성 서버 배포 요구 사항에 대 한 tooAzure 필수 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="59b66-126">Refer hello VMware / Physical tooAzure prerequisites for configuration server deployment requirements.</span></span>

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  <span data-ttu-id="59b66-128">구성 서버에는 AWS에 배포 하 고 복구 서비스 자격 증명 모음에 등록 되 면 아래와 같이 hello 구성 서버 및 사이트 복구 인프라 프로세스 서버 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59b66-128">Once your configuration server is deployed in AWS and registered with your Recovery Services vault, you should see hello configuration server and process server under Site Recovery infrastructure as shown below:</span></span>

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. <span data-ttu-id="59b66-130">Hello 구성 서버를 배포한 후 (것에 대 한 too15 minustes 걸릴 수도 있습니다 tooappear), toomigrate 원하는 hello Vm과 통신할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b66-130">After you've deployed hello configuration server (it might take up too15 minustes for it tooappear), validate that it can communicate with hello VMs that you want toomigrate.</span></span>

6. <span data-ttu-id="59b66-131">[복제 설정을 지정합니다](site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="59b66-131">[Set up replication settings](site-recovery-setup-replication-settings-vmware.md).</span></span>

7. <span data-ttu-id="59b66-132">복제를 사용 하도록 설정: hello toomigrate 원하는 Vm에 대 한 복제를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b66-132">Enable replication: Enable replication for hello VMs you want toomigrate.</span></span> <span data-ttu-id="59b66-133">Hello EC2 콘솔에서 가져올 수 hello 개인 IP 주소를 사용 하 여 hello EC2 인스턴스를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b66-133">You can discover hello EC2 instances using hello private IP addresses, which you can get from hello EC2 console.</span></span>

    ![SelectVM](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. <span data-ttu-id="59b66-135">Hello EC2 인스턴스를 보호 하 고 hello 복제 tooAzure 완료 되 면 [테스트 장애 조치 실행](site-recovery-test-failover-to-azure.md) toovalidate Azure에서 응용 프로그램의 성능입니다.</span><span class="sxs-lookup"><span data-stu-id="59b66-135">Once hello EC2 instances have been protected and hello replication tooAzure is complete, [run a Test Failover](site-recovery-test-failover-to-azure.md) toovalidate your application's performance in Azure.</span></span>

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. <span data-ttu-id="59b66-137">AWS tooAzure에서 각 VM에 대 한 장애 조치를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b66-137">Run a Failover from AWS tooAzure for each VM.</span></span> <span data-ttu-id="59b66-138">필요에 따라 복구 계획을 만드는 하 고 AWS tooAzure에서 장애 조치 toomigrate 여러 가상 컴퓨터를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b66-138">Optionally, you can create a recovery plan and run a Failover, toomigrate multiple virtual machines from AWS tooAzure.</span></span> <span data-ttu-id="59b66-139">[자세히 알아봅니다](site-recovery-create-recovery-plans.md) .</span><span class="sxs-lookup"><span data-stu-id="59b66-139">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

10. <span data-ttu-id="59b66-140">마이그레이션에 대 한 장애 조치 toocommit이 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="59b66-140">For migration, you don't need toocommit a failover.</span></span> <span data-ttu-id="59b66-141">Hello 마이그레이션을 완료 옵션을 선택 하는 대신, 원하는 toomigrate 각 컴퓨터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b66-141">Instead, you select hello Complete Migration option for each machine you want toomigrate.</span></span> <span data-ttu-id="59b66-142">hello 마이그레이션을 완료 동작 hello 마이그레이션 프로세스를 완료 하 고, hello 컴퓨터에 대 한 복제를 제거, hello 컴퓨터에 대 한 청구 하는 사이트 복구를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b66-142">hello Complete Migration action finishes up hello migration process, removes replication for hello machine, and stops Site Recovery billing for hello machine.</span></span>

    ![마이그레이션](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a><span data-ttu-id="59b66-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="59b66-144">Next steps</span></span>

- <span data-ttu-id="59b66-145">[마이그레이션된 컴퓨터 tooenable 복제 준비](site-recovery-azure-to-azure-after-migration.md) 재해 복구 요구에 따라 tooanother 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="59b66-145">[Prepare migrated machines tooenable replication](site-recovery-azure-to-azure-after-migration.md) tooanother region for disaster recovery needs.</span></span>
- <span data-ttu-id="59b66-146">[Azure Virtual Machines를 복제](site-recovery-azure-to-azure.md)하여 워크로드 보호를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="59b66-146">Start protecting your workloads by [replicating Azure virtual machines.](site-recovery-azure-to-azure.md)</span></span>
