---
title: "VM을 AWS에서 Azure로 마이그레이션| Microsoft Docs"
description: "이 문서에서는 Azure Site Recovery를 사용하여 AWS(Amazon Web Services)를 실행하는 가상 컴퓨터를 Azure로 마이그레이션하는 방법을 설명합니다."
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
ms.openlocfilehash: b3c0727a279649f4f7dae30d41027129ce5b04ee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-to-azure-with-azure-site-recovery"></a><span data-ttu-id="9a3b9-103">Azure Site Recovery를 사용하여 AWS(Amazon Web Services)의 가상 컴퓨터를 Azure로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="9a3b9-103">Migrate virtual machines in Amazon Web Services (AWS) to Azure with Azure Site Recovery</span></span>

<span data-ttu-id="9a3b9-104">이 문서에서는 [Azure Site Recovery](site-recovery-overview.md) 서비스를 사용하여 AWS Windows 인스턴스를 Azure Virtual Machines로 마이그레이션하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9a3b9-104">This article describes how to migrate AWS Windows instances to Azure virtual machines with the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="9a3b9-105">마이그레이션은 AWS에서 Azure로 발생하는 효율적인 장애 조치입니다.</span><span class="sxs-lookup"><span data-stu-id="9a3b9-105">Migration is effectively a failover from AWS to Azure.</span></span> <span data-ttu-id="9a3b9-106">컴퓨터를 AWS로 장애 복구할 수 없고 진행 중인 복제도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9a3b9-106">You can't failback machines to AWS, and there's no ongoing replication.</span></span> <span data-ttu-id="9a3b9-107">이 문서에서는 Azure Portal에서 마이그레이션하기 위한 단계를 설명하고 [Azure에 물리적 컴퓨터를 복제](site-recovery-vmware-to-azure.md)하는 지침을 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a3b9-107">This article describes the steps for migration in the Azure portal, and are based on the instructions for [replicating a physical machine to Azure](site-recovery-vmware-to-azure.md).</span></span>

<span data-ttu-id="9a3b9-108">이 문서의 하단 또는 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="9a3b9-108">Post any comments or questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="9a3b9-109">지원되는 운영 체제</span><span class="sxs-lookup"><span data-stu-id="9a3b9-109">Supported operating systems</span></span>

<span data-ttu-id="9a3b9-110">Site Recovery는 다음 운영 체제 중 하나를 실행하는 EC2 인스턴스를 마이그레이션하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a3b9-110">Site Recovery can be used to migrate EC2 instances running any of the following operating systems:</span></span>

- <span data-ttu-id="9a3b9-111">Windows(64비트만 해당)</span><span class="sxs-lookup"><span data-stu-id="9a3b9-111">Windows(64 bit only)</span></span>
    - <span data-ttu-id="9a3b9-112">Windows Server 2008 R2 SP1+(Citrix PV 드라이버 또는 AWS PV 드라이버만 해당.</span><span class="sxs-lookup"><span data-stu-id="9a3b9-112">Windows Server 2008 R2 SP1+ (Citrix PV drivers or AWS PV drivers only.</span></span> <span data-ttu-id="9a3b9-113">**RedHat PV 드라이버를 실행하는 인스턴스가 지원되지 않습니다**)Windows Server 2012 Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="9a3b9-113">**Instances running RedHat PV drivers are not supported**) Windows Server 2012 Windows Server 2012 R2</span></span>
- <span data-ttu-id="9a3b9-114">Linux(64비트만 해당)</span><span class="sxs-lookup"><span data-stu-id="9a3b9-114">Linux (64 bit only)</span></span>
    - <span data-ttu-id="9a3b9-115">Red Hat Enterprise Linux 6.7(HVM 가상화된 인스턴스만 해당)</span><span class="sxs-lookup"><span data-stu-id="9a3b9-115">Red Hat Enterprise Linux 6.7 (HVM virtualized instances only)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a3b9-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9a3b9-116">Prerequisites</span></span>

<span data-ttu-id="9a3b9-117">이 배포에 대해 필요한 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9a3b9-117">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="9a3b9-118">**구성 서버**: 구성 서버 역할로 배포된 Windows Server 2012 R2를 실행 중인 Amazon EC2 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="9a3b9-118">**Configuration server**: An Amazon EC2 VM running Windows Server 2012 R2 is deployed as the configuration server.</span></span> <span data-ttu-id="9a3b9-119">기본적으로 다른 Azure Site Recovery 구성 요소(프로세스 서버와 마스터 대상 서버)는 구성 서버를 배포할 때 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a3b9-119">By default, the other Azure Site Recovery components (process server and master target server) are installed when you deploy the configuration server.</span></span> <span data-ttu-id="9a3b9-120">이 문서에서는 Azure Portal에서 마이그레이션하기 위한 단계를 설명하고 [자세한 정보](site-recovery-components.md)의 지침을 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a3b9-120">This article describes the steps for migration in the Azure portal, and are based on the instructions for  [Learn more](site-recovery-components.md)</span></span>

* <span data-ttu-id="9a3b9-121">**EC2 인스턴스**: 마이그레이션하려는 Amazon EC2 가상 컴퓨터 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="9a3b9-121">**EC2 instances**: The Amazon EC2 virtual machines instances that you want to migrate.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="9a3b9-122">배포 단계</span><span class="sxs-lookup"><span data-stu-id="9a3b9-122">Deployment steps</span></span>

1. <span data-ttu-id="9a3b9-123">Recovery Services 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9a3b9-123">Create a Recovery Services vault.</span></span>
2. <span data-ttu-id="9a3b9-124">EC2 인스턴스의 보안 그룹에는 마이그레이션하려는 EC2 인스턴스와 구성 서버를 배포하려는 인스턴스 간의 통신을 허용하도록 구성된 규칙이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a3b9-124">The Security Group of your EC2 instances should have rules configured to allow communication between the EC2 instance that you want to migrate, and the instance on which you plan to deploy the Configuration Server.</span></span>

3. <span data-ttu-id="9a3b9-125">EC2 인스턴스와 동일한 Amazon 가상 사설 클라우드에서 ASR 구성 서버를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="9a3b9-125">On the same Amazon Virtual Private Cloud as your EC2 instances, deploy an ASR configuration server.</span></span> <span data-ttu-id="9a3b9-126">구성 서버 배포 요구 사항은 VMware/Physical to Azure 필수 구성 요소를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a3b9-126">Refer the VMware / Physical to Azure prerequisites for configuration server deployment requirements.</span></span>

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  <span data-ttu-id="9a3b9-128">구성 서버가 AWS에 배포되고 Recovery Services 자격 증명 모음으로 등록되면 아래와 같이 Site Recovery 인프라 아래에서 구성 서버 및 프로세스 서버가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a3b9-128">Once your configuration server is deployed in AWS and registered with your Recovery Services vault, you should see the configuration server and process server under Site Recovery infrastructure as shown below:</span></span>

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. <span data-ttu-id="9a3b9-130">구성 서버를 배포(표시되는 데 최대 15분이 걸릴 수 있음)한 후에 마이그레이션할 VM과 통신할 수 있는지 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="9a3b9-130">After you've deployed the configuration server (it might take up to 15 minustes for it to appear), validate that it can communicate with the VMs that you want to migrate.</span></span>

6. <span data-ttu-id="9a3b9-131">[복제 설정을 지정합니다](site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="9a3b9-131">[Set up replication settings](site-recovery-setup-replication-settings-vmware.md).</span></span>

7. <span data-ttu-id="9a3b9-132">복제 사용: 마이그레이션할 VM에 대해 복제를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a3b9-132">Enable replication: Enable replication for the VMs you want to migrate.</span></span> <span data-ttu-id="9a3b9-133">EC2 콘솔에서 얻을 수 있는 개인 IP 주소를 사용하여 EC2 인스턴스를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a3b9-133">You can discover the EC2 instances using the private IP addresses, which you can get from the EC2 console.</span></span>

    ![SelectVM](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. <span data-ttu-id="9a3b9-135">EC2 인스턴스가 보호되고 Azure에 복제가 완료되면 [테스트 장애 조치를 실행](site-recovery-test-failover-to-azure.md)하여 Azure에서 응용 프로그램의 성능을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="9a3b9-135">Once the EC2 instances have been protected and the replication to Azure is complete, [run a Test Failover](site-recovery-test-failover-to-azure.md) to validate your application's performance in Azure.</span></span>

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. <span data-ttu-id="9a3b9-137">각 VM에 대해 AWS에서 Azure로 장애 조치를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9a3b9-137">Run a Failover from AWS to Azure for each VM.</span></span> <span data-ttu-id="9a3b9-138">선택적으로 복구 계획을 만들고 장애 조치를 실행하여 AWS에서 Azure에 여러 가상 컴퓨터를 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a3b9-138">Optionally, you can create a recovery plan and run a Failover, to migrate multiple virtual machines from AWS to Azure.</span></span> <span data-ttu-id="9a3b9-139">[자세히 알아봅니다](site-recovery-create-recovery-plans.md) .</span><span class="sxs-lookup"><span data-stu-id="9a3b9-139">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

10. <span data-ttu-id="9a3b9-140">마이그레이션의 경우 장애 조치를 커밋할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9a3b9-140">For migration, you don't need to commit a failover.</span></span> <span data-ttu-id="9a3b9-141">대신 마이그레이션할 각 컴퓨터에 대해 마이그레이션 완료 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a3b9-141">Instead, you select the Complete Migration option for each machine you want to migrate.</span></span> <span data-ttu-id="9a3b9-142">마이그레이션 완료 작업은 마이그레이션 프로세스를 마치고 가상 컴퓨터에 대한 복제를 제거하며 컴퓨터에 대한 Site Recovery 청구를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="9a3b9-142">The Complete Migration action finishes up the migration process, removes replication for the machine, and stops Site Recovery billing for the machine.</span></span>

    ![마이그레이션](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a><span data-ttu-id="9a3b9-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9a3b9-144">Next steps</span></span>

- <span data-ttu-id="9a3b9-145">재해 복구 수요에 맞게 다른 지역으로 [복제할 수 있도록 마이그레이션된 컴퓨터를 준비](site-recovery-azure-to-azure-after-migration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9a3b9-145">[Prepare migrated machines to enable replication](site-recovery-azure-to-azure-after-migration.md) to another region for disaster recovery needs.</span></span>
- <span data-ttu-id="9a3b9-146">[Azure Virtual Machines를 복제](site-recovery-azure-to-azure.md)하여 워크로드 보호를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9a3b9-146">Start protecting your workloads by [replicating Azure virtual machines.](site-recovery-azure-to-azure.md)</span></span>
