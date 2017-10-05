---
title: "Azure에서 Linux 및 오픈 소스 컴퓨팅 | Microsoft Docs"
description: "기본 Linux 사용, Azure에서 Linux 이미지 실행 또는 업로드에 대한 몇 가지 기본적인 개념, 기타 특정 기술 및 최적화에 대한 내용 등 Azure의 Linux 및 오픈 소스 컴퓨팅 문서 목록이 포함되어 있습니다."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: a7e608b5-26ea-41e0-b46b-1a483a257754
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/27/2016
ms.author: rasquill
ms.openlocfilehash: 1cdd0e68368d2dc376ee45df67bf5e75288d4ca3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="linux-and-open-source-computing-on-azure"></a><span data-ttu-id="4f564-103">Azure의 오픈 소스 컴퓨팅 및 Linux</span><span class="sxs-lookup"><span data-stu-id="4f564-103">Linux and open-source computing on Azure</span></span>
<span data-ttu-id="4f564-104">클래식 배포 모델에서 Linux 기반 가상 컴퓨터를 만들고 관리하는 데 필요한 모든 설명서를 찾아보세요.</span><span class="sxs-lookup"><span data-stu-id="4f564-104">Find all the documentation you need to create and manage Linux-based virtual machines in the classic deployment model.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="4f564-105">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f564-105">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4f564-106">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4f564-106">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="4f564-107">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4f564-107">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

## <a name="get-started"></a><span data-ttu-id="4f564-108">시작</span><span class="sxs-lookup"><span data-stu-id="4f564-108">Get Started</span></span>
* [<span data-ttu-id="4f564-109">Azure의 Linux에 대한 소개</span><span class="sxs-lookup"><span data-stu-id="4f564-109">Introduction for Linux on Azure</span></span>](intro-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="4f564-110">클래식 배포 모델을 사용하여 만든 Azure 가상 컴퓨터에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="4f564-110">Frequently asked question about Azure Virtual Machines created with the classic deployment model</span></span>](classic/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4f564-111">가상 컴퓨터에 대한 이미지 정보</span><span class="sxs-lookup"><span data-stu-id="4f564-111">About images for virtual machines</span></span>](../windows/classic/about-images.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* <span data-ttu-id="4f564-112">[사용자 고유의 Distro 이미지 업로드](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)(및 [Azure 보증 배포판](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 사용 지침)</span><span class="sxs-lookup"><span data-stu-id="4f564-112">[Uploading your own Distro Image](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) (and also instructions using an [Azure-Endorsed Distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))</span></span>
* [<span data-ttu-id="4f564-113">Azure 클래식 포털을 사용하여 Linux VM에 로그온</span><span class="sxs-lookup"><span data-stu-id="4f564-113">Log on to a Linux VM Using the Azure classic portal</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="set-up"></a><span data-ttu-id="4f564-114">설정</span><span class="sxs-lookup"><span data-stu-id="4f564-114">Set up</span></span>
* [<span data-ttu-id="4f564-115">Azure 명령줄 인터페이스(Azure CLI) 설치</span><span class="sxs-lookup"><span data-stu-id="4f564-115">Install Azure Command-Line Interface (Azure CLI)</span></span>](../../cli-install-nodejs.md)

## <a name="tutorials"></a><span data-ttu-id="4f564-116">자습서</span><span class="sxs-lookup"><span data-stu-id="4f564-116">Tutorials</span></span>
* [<span data-ttu-id="4f564-117">Azure에서 Linux 가상 컴퓨터에 LAMP 스택 설치</span><span class="sxs-lookup"><span data-stu-id="4f564-117">Install the LAMP Stack on a Linux virtual machine in Azure</span></span>](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="4f564-118">Azure VM의 Ruby on Rails 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="4f564-118">Ruby on Rails Web application on an Azure VM</span></span>](classic/virtual-machines-linux-classic-ruby-rails-web-app.md)
* [<span data-ttu-id="4f564-119">방법: AMQP 및 서비스 버스용 Apache Qpid Proton-C 설치</span><span class="sxs-lookup"><span data-stu-id="4f564-119">How to: Install Apache Qpid Proton-C for AMQP and Service Bus</span></span>](../../service-bus-messaging/service-bus-amqp-apache.md)

### <a name="databases"></a><span data-ttu-id="4f564-120">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4f564-120">Databases</span></span>
* [<span data-ttu-id="4f564-121">Azure에서 MySQL 성능 최적화</span><span class="sxs-lookup"><span data-stu-id="4f564-121">Optimize Performance of MySQL on Azure</span></span>](classic/optimize-mysql.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4f564-122">MySQL 클러스터</span><span class="sxs-lookup"><span data-stu-id="4f564-122">MySQL Clusters</span></span>](classic/mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4f564-123">Azure에서 Linux 환경의 Cassandra 실행 및 Node.js에서 Cassandra에 액세스</span><span class="sxs-lookup"><span data-stu-id="4f564-123">Running Cassandra with Linux on Azure and Accessing it from Node.js</span></span>](classic/cassandra-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4f564-124">MariaDbs의 다중 마스터 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="4f564-124">Create a Multi-Master cluster of MariaDbs</span></span>](classic/mariadb-mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="hpc"></a><span data-ttu-id="4f564-125">HPC</span><span class="sxs-lookup"><span data-stu-id="4f564-125">HPC</span></span>
* [<span data-ttu-id="4f564-126">Azure에서 HPC Pack 클러스터의 Linux 계산 노드 시작</span><span class="sxs-lookup"><span data-stu-id="4f564-126">Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4f564-127">Azure의 Linux 계산 노드에서 Microsoft HPC 팩을 사용하여 NAMD 실행</span><span class="sxs-lookup"><span data-stu-id="4f564-127">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4f564-128">MPI 응용 프로그램을 실행하도록 Linux RDMA 클러스터 설정</span><span class="sxs-lookup"><span data-stu-id="4f564-128">Set up a Linux RDMA cluster to run MPI applications</span></span>](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="docker"></a><span data-ttu-id="4f564-129">Docker</span><span class="sxs-lookup"><span data-stu-id="4f564-129">Docker</span></span>
* [<span data-ttu-id="4f564-130">Azure 명령줄 인터페이스(Azure CLI)에서 Docker VM 확장 사용</span><span class="sxs-lookup"><span data-stu-id="4f564-130">Using the Docker VM Extension from the Azure Command-line Interface (Azure CLI)</span></span>](classic/cli-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4f564-131">Azure Portal에서 Docker VM 확장 사용</span><span class="sxs-lookup"><span data-stu-id="4f564-131">Using the Docker VM Extension from the Azure portal</span></span>](classic/portal-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4f564-132">Azure에서 docker-machine을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="4f564-132">How to use docker-machine on Azure</span></span>](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="ubuntu"></a><span data-ttu-id="4f564-133">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="4f564-133">Ubuntu</span></span>
* [<span data-ttu-id="4f564-134">방법: MySQL 클러스터</span><span class="sxs-lookup"><span data-stu-id="4f564-134">How to: MySQL Clusters</span></span>](classic/mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4f564-135">방법: Node.js 및 Cassandra</span><span class="sxs-lookup"><span data-stu-id="4f564-135">How to: Node.js and Cassandra</span></span>](classic/cassandra-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="opensuse"></a><span data-ttu-id="4f564-136">OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="4f564-136">OpenSUSE</span></span>
* [<span data-ttu-id="4f564-137">방법: MySQL 설치 및 실행</span><span class="sxs-lookup"><span data-stu-id="4f564-137">How to: Install and Run MySQL</span></span>](classic/mysql-on-opensuse.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="coreos"></a><span data-ttu-id="4f564-138">CoreOS</span><span class="sxs-lookup"><span data-stu-id="4f564-138">CoreOS</span></span>
* [<span data-ttu-id="4f564-139">방법: Azure에서 CoreOS를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="4f564-139">How to: Use CoreOS on Azure</span></span>](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="planning"></a><span data-ttu-id="4f564-140">계획</span><span class="sxs-lookup"><span data-stu-id="4f564-140">Planning</span></span>
* [<span data-ttu-id="4f564-141">Azure 인프라 서비스 구현 지침</span><span class="sxs-lookup"><span data-stu-id="4f564-141">Azure infrastructure services implementation guidelines</span></span>](../windows/infrastructure-subscription-accounts-guidelines.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="4f564-142">Linux 사용자 이름 선택</span><span class="sxs-lookup"><span data-stu-id="4f564-142">Selecting Linux Usernames</span></span>](usernames.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="4f564-143">클래식 배포 모델에서 가상 컴퓨터에 대한 가용성 집합을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="4f564-143">How to configure an availability set for virtual machines in the classic deployment model</span></span>](../windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4f564-144">Azure VM에 계획된 유지 관리 예약 방법</span><span class="sxs-lookup"><span data-stu-id="4f564-144">How to Schedule Planned Maintenance on Azure VMs</span></span>](classic/planned-maintenance-schedule.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4f564-145">가상 컴퓨터의 가용성 관리</span><span class="sxs-lookup"><span data-stu-id="4f564-145">Manage the availability of virtual machines</span></span>](../windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="4f564-146">Azure에서 Linux 가상 컴퓨터에 대한 계획된 유지 관리</span><span class="sxs-lookup"><span data-stu-id="4f564-146">Planned maintenance for Linux virtual machines in Azure</span></span>](planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="deployment"></a><span data-ttu-id="4f564-147">배포</span><span class="sxs-lookup"><span data-stu-id="4f564-147">Deployment</span></span>
* [<span data-ttu-id="4f564-148">Linux를 실행하는 사용자 지정 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="4f564-148">Create a custom virtual machine running Linux</span></span>](../windows/classic/createportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4f564-149">기본 사항: Linux VM을 캡처하여 템플릿 작성</span><span class="sxs-lookup"><span data-stu-id="4f564-149">The basics: Capturing a Linux VM to Make a Template</span></span>](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4f564-150">보증되지 않는 배포에 대한 정보</span><span class="sxs-lookup"><span data-stu-id="4f564-150">Information for Non-Endorsed Distributions</span></span>](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="management"></a><span data-ttu-id="4f564-151">관리</span><span class="sxs-lookup"><span data-stu-id="4f564-151">Management</span></span>
* [<span data-ttu-id="4f564-152">SSH</span><span class="sxs-lookup"><span data-stu-id="4f564-152">SSH</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="4f564-153">Linux에 대한 암호 또는 SSH 속성을 다시 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="4f564-153">How to Reset a Password or SSH Properties for Linux</span></span>](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4f564-154">루트 사용</span><span class="sxs-lookup"><span data-stu-id="4f564-154">Using Root</span></span>](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="azure-resources"></a><span data-ttu-id="4f564-155">Azure 리소스</span><span class="sxs-lookup"><span data-stu-id="4f564-155">Azure Resources</span></span>
* [<span data-ttu-id="4f564-156">Azure Linux 에이전트</span><span class="sxs-lookup"><span data-stu-id="4f564-156">The Azure Linux Agent</span></span>](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="4f564-157">Azure VM 확장 및 기능</span><span class="sxs-lookup"><span data-stu-id="4f564-157">Azure VM Extensions and Features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="4f564-158">Cloud-init에서 사용할 VM에 사용자 지정 데이터 주입</span><span class="sxs-lookup"><span data-stu-id="4f564-158">Injecting Custom Data into a VM to use with Cloud-init</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="storage"></a><span data-ttu-id="4f564-159">저장소</span><span class="sxs-lookup"><span data-stu-id="4f564-159">Storage</span></span>
* [<span data-ttu-id="4f564-160">Linux VM에 데이터 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="4f564-160">Attaching a Data Disk to a Linux VM</span></span>](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4f564-161">Linux VM에서 데이터 디스크 분리</span><span class="sxs-lookup"><span data-stu-id="4f564-161">Detaching a Data Disk from a Linux VM</span></span>](classic/detach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4f564-162">RAID</span><span class="sxs-lookup"><span data-stu-id="4f564-162">RAID</span></span>](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="networking"></a><span data-ttu-id="4f564-163">네트워킹</span><span class="sxs-lookup"><span data-stu-id="4f564-163">Networking</span></span>
* [<span data-ttu-id="4f564-164">Azure에서 클래식 가상 컴퓨터에 끝점을 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="4f564-164">How to set up endpoints on a classic virtual machine in Azure</span></span>](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="troubleshooting"></a><span data-ttu-id="4f564-165">문제 해결</span><span class="sxs-lookup"><span data-stu-id="4f564-165">Troubleshooting</span></span>
* [<span data-ttu-id="4f564-166">Linux 기반 Azure 가상 컴퓨터에 SSH(보안 셸) 연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="4f564-166">Troubleshoot Secure Shell (SSH) connections to a Linux-based Azure virtual machine</span></span>](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="4f564-167">Azure에서 새 Linux 가상 컴퓨터 생성 관련 클래식 배포 문제 해결</span><span class="sxs-lookup"><span data-stu-id="4f564-167">Troubleshoot classic deployment issues with creating a new Linux virtual machine in Azure</span></span>](classic/troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)  
* [<span data-ttu-id="4f564-168">Azure의 기존 Linux 가상 컴퓨터 재시작 또는 크기 조정 관련 클래식 배포 문제 해결</span><span class="sxs-lookup"><span data-stu-id="4f564-168">Troubleshoot classic deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure</span></span>](../windows/restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) 

## <a name="reference"></a><span data-ttu-id="4f564-169">참조</span><span class="sxs-lookup"><span data-stu-id="4f564-169">Reference</span></span>
* [<span data-ttu-id="4f564-170">ASM(Azure 서비스 관리) 모드의 Azure CLI 명령</span><span class="sxs-lookup"><span data-stu-id="4f564-170">Azure CLI commands in Azure Service Management (asm) mode</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="4f564-171">Azure 서비스 관리 REST API</span><span class="sxs-lookup"><span data-stu-id="4f564-171">Azure Service Management REST API</span></span>](https://msdn.microsoft.com/library/azure/ee460799.aspx)

## <a name="general-links"></a><span data-ttu-id="4f564-172">일반 링크</span><span class="sxs-lookup"><span data-stu-id="4f564-172">General Links</span></span>
<span data-ttu-id="4f564-173">다음 링크는 Microsoft 블로그, Technet 페이지 및 위의 Azure.com 설명서 외의 외부 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="4f564-173">The following links are for Microsoft blogs, Technet pages, and external sites rather than Azure.com documentation as above.</span></span> <span data-ttu-id="4f564-174">Azure와 오픈 소스 컴퓨팅 환경은 둘 다 빠르게 변화하고 있으므로 Microsoft에서 최신 항목을 지속해서 추가하고 오래된 항목을 제거하기 위해 최선을 다하고 *있음에도* 다음 링크는 분명히 오래된 버전일 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4f564-174">As both Azure and the open-source computing world are fast-moving targets, it is almost certain that the following links are out of date, *despite* the fact that we shall do our best to continually add newer topics and remove out-of-date ones.</span></span> <span data-ttu-id="4f564-175">누락된 사항이 있으면 설명을 통해 알려 주시거나 [Github 리포지토리](https://github.com/Azure/azure-content/)로 끌어오기 요청을 제출해 주세요.</span><span class="sxs-lookup"><span data-stu-id="4f564-175">If we've missed one, please let us know in the comments, or submit a pull request to our [GitHub repo](https://github.com/Azure/azure-content/).</span></span>

* [<span data-ttu-id="4f564-176">Docker 컨테이너를 사용하여 Linux에서 ASP.NET 5 실행</span><span class="sxs-lookup"><span data-stu-id="4f564-176">Running ASP.NET 5 on Linux using Docker Containers</span></span>](http://blogs.msdn.com/b/webdev/archive/2015/01/14/running-asp-net-5-applications-in-linux-containers-with-docker.aspx)
* [<span data-ttu-id="4f564-177">OpenLogic에서 CentOS VM 이미지를 배포하는 방법</span><span class="sxs-lookup"><span data-stu-id="4f564-177">How to Deploy a CentOS VM Image from OpenLogic</span></span>](https://azure.microsoft.com/blog/2013/01/11/deploying-openlogic-centos-images-on-windows-azure-virtual-machines/)
* [<span data-ttu-id="4f564-178">SUSE 업데이트 인프라</span><span class="sxs-lookup"><span data-stu-id="4f564-178">SUSE Update Infrastructure</span></span>](https://forums.suse.com/showthread.php?5622-New-Update-Infrastructure)
* [<span data-ttu-id="4f564-179">SAP Cloud Appliance Library용 SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="4f564-179">SUSE Linux Enterprise Server for SAP Cloud Appliance  Library</span></span>](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver11sp3forsapcloudappliance/)
* [<span data-ttu-id="4f564-180">Azure에서 고가용성 Linux를 빌드하는 12단계</span><span class="sxs-lookup"><span data-stu-id="4f564-180">Building Highly Available Linux on Azure in 12 Steps</span></span>](http://blogs.technet.com/b/keithmayer/archive/2014/10/03/quick-start-guide-building-highly-available-linux-servers-in-the-cloud-on-microsoft-azure.aspx)
* [<span data-ttu-id="4f564-181">Azure CLI, node.js 및 jhawk를 사용하여 Azure에서 Linux 프로비전 자동화</span><span class="sxs-lookup"><span data-stu-id="4f564-181">Automate Provisioning Linux on Azure with Azure CLI, node.js, jhawk</span></span>](http://blogs.technet.com/b/keithmayer/archive/2014/11/24/step-by-step-automated-provisioning-for-linux-in-the-cloud-with-microsoft-azure-xplat-cli-json-and-node-js-part-1.aspx)
* [<span data-ttu-id="4f564-182">Azure에서 GlusterFS</span><span class="sxs-lookup"><span data-stu-id="4f564-182">GlusterFS on Azure</span></span>](http://dastouri.azurewebsites.net/gluster-on-azure-part-1/)

### <a name="freebsd"></a><span data-ttu-id="4f564-183">FreeBSD</span><span class="sxs-lookup"><span data-stu-id="4f564-183">FreeBSD</span></span>
* [<span data-ttu-id="4f564-184">Azure에서 FreeBSD 실행</span><span class="sxs-lookup"><span data-stu-id="4f564-184">Running FreeBSD in Azure</span></span>](https://azure.microsoft.com/blog/2014/05/22/running-freebsd-in-azure/)
* [<span data-ttu-id="4f564-185">간편한 FreeBSD 배포</span><span class="sxs-lookup"><span data-stu-id="4f564-185">Easy Deploy FreeBSD</span></span>](http://msopentech.com/blog/2014/10/24/easy-deploy-freebsd-microsoft-azure-vm-depot/)
* [<span data-ttu-id="4f564-186">사용자 지정 FreeBSD 이미지 배포</span><span class="sxs-lookup"><span data-stu-id="4f564-186">Deploying a Customized FreeBSD Image</span></span>](http://msopentech.com/blog/2014/05/14/deploy-customize-freebsd-virtual-machine-image-microsoft-azure/)
* [<span data-ttu-id="4f564-187">Linux 파일 서버용 Kaspersky AV</span><span class="sxs-lookup"><span data-stu-id="4f564-187">Kaspersky AV for Linux File Server</span></span>](https://azure.microsoft.com/marketplace/partners/kaspersky-lab/kav-for-lfs-kav-for-lfs/)

### <a name="nosql"></a><span data-ttu-id="4f564-188">NoSQL</span><span class="sxs-lookup"><span data-stu-id="4f564-188">NoSQL</span></span>
* [<span data-ttu-id="4f564-189">8가지 Azure용 오픈 소스 NoSql 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4f564-189">8 Open-source NoSql Databases for Azure</span></span>](http://openness.microsoft.com/blog/2014/11/03/open-source-nosql-databases-microsoft-azure/)
* [<span data-ttu-id="4f564-190">Slideshare (MSOpenTech):Azure에서 CouchDb 경험</span><span class="sxs-lookup"><span data-stu-id="4f564-190">Slideshare (MSOpenTech): Experiences with CouchDb on Azure</span></span>](http://www.slideshare.net/brianbenz/experiences-using-couchdb-inside-microsofts-azure-team)
* [<span data-ttu-id="4f564-191">node.js, CORS 및 Grunt를 사용하여 CouchDB-as-a-Service 실행</span><span class="sxs-lookup"><span data-stu-id="4f564-191">Running CouchDB-as-a-Service with node.js, CORS, and Grunt</span></span>](http://msopentech.com/blog/2013/12/19/tutorial-building-multi-tier-windows-azure-web-application-use-cloudants-couchdb-service-node-js-cors-grunt-2/)
* [<span data-ttu-id="4f564-192">Azure Redis 캐시 서비스에서 Windows의 Redis</span><span class="sxs-lookup"><span data-stu-id="4f564-192">Redis on Windows in the Azure Redis Cache Service</span></span>](http://msopentech.com/blog/2014/05/12/redis-on-windows/)
* [<span data-ttu-id="4f564-193">Redis용 ASP.NET 세션 상태 공급자 미리 보기 릴리스 발표</span><span class="sxs-lookup"><span data-stu-id="4f564-193">Announcing ASP.NET Session State Provider for Redis Preview Release</span></span>](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx)
* [<span data-ttu-id="4f564-194">블로그: 이제 Azure 마켓플레이스에서 RavenHQ 사용 가능</span><span class="sxs-lookup"><span data-stu-id="4f564-194">Blog: RavenHQ Now Available in the Azure Marketplace</span></span>](https://azure.microsoft.com/blog/2014/08/12/ravenhq-now-available-in-the-azure-store/)

### <a name="big-data"></a><span data-ttu-id="4f564-195">빅 데이터</span><span class="sxs-lookup"><span data-stu-id="4f564-195">Big Data</span></span>
* [<span data-ttu-id="4f564-196">Azure Linux VM에 Hadoop 설치</span><span class="sxs-lookup"><span data-stu-id="4f564-196">Installing Hadoop on Azure Linux VMs</span></span>](http://blogs.msdn.com/b/benjguin/archive/2013/04/05/how-to-install-hadoop-on-windows-azure-linux-virtual-machines.aspx)
* [<span data-ttu-id="4f564-197">Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="4f564-197">Azure HDInsight</span></span>](https://azure.microsoft.com/documentation/learning-paths/hdinsight-self-guided-hadoop-training/)

### <a name="relational-database"></a><span data-ttu-id="4f564-198">관계형 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4f564-198">Relational database</span></span>
* [<span data-ttu-id="4f564-199">Microsoft Azure에서 MySQL 고가용성 아키텍처</span><span class="sxs-lookup"><span data-stu-id="4f564-199">MySQL High Availability Architecture in Microsoft Azure</span></span>](http://download.microsoft.com/download/6/1/C/61C0E37C-F252-4B33-9557-42B90BA3E472/MySQL_HADR_solution_in_Azure.pdf)
* [<span data-ttu-id="4f564-200">ILB를 사용하는 corosync, pg_bouncer를 통해 Postgres 설치</span><span class="sxs-lookup"><span data-stu-id="4f564-200">Installing Postgres with corosync, pg_bouncer using ILB</span></span>](https://github.com/chgeuer/postgres-azure)

### <a name="linux-high-performance-computing-hpc"></a><span data-ttu-id="4f564-201">Linux HPC(고성능 컴퓨팅)</span><span class="sxs-lookup"><span data-stu-id="4f564-201">Linux high performance computing (HPC)</span></span>
* <span data-ttu-id="4f564-202">[빠른 시작 템플릿: SLURM 클러스터 스핀업](https://github.com/Azure/azure-quickstart-templates/tree/master/slurm) (및 [블로그 게시물](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx))</span><span class="sxs-lookup"><span data-stu-id="4f564-202">[Quickstart template: Spin up a SLURM cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/slurm) (and [blog post](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx))</span></span>
* [<span data-ttu-id="4f564-203">빠른 시작 템플릿: Linux 계산 노드가 포함된 HPC 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="4f564-203">Quickstart template: Create an HPC cluster with Linux compute nodes</span></span>](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/)

### <a name="devops-management-and-optimization"></a><span data-ttu-id="4f564-204">개발, 관리 및 최적화</span><span class="sxs-lookup"><span data-stu-id="4f564-204">Devops, management, and optimization</span></span>
<span data-ttu-id="4f564-205">개발, 관리 및 최적화 환경은 매우 광범위하고 빠르게 변화하므로 아래 목록을 출발점으로 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f564-205">As the world of devops, management, and optimization is quite expansive and changing very quickly, you should consider the list below a starting point.</span></span>

* [<span data-ttu-id="4f564-206">비디오: Azure 가상 컴퓨터 : Chef, Puppet 및 Docker를 사용하여 Linux VM 관리</span><span class="sxs-lookup"><span data-stu-id="4f564-206">Video: Azure Virtual Machines : Using Chef, Puppet and Docker for managing Linux VMs</span></span>](https://azure.microsoft.com/blog/2014/12/15/azure-virtual-machines-using-chef-puppet-and-docker-for-managing-linux-vms/)
* [<span data-ttu-id="4f564-207">CoreOS 및 Weave로 자동화된 Kubernetes 클러스터에 대한 완벽한 가이드</span><span class="sxs-lookup"><span data-stu-id="4f564-207">Complete guide to automated Kubernetes cluster deployment with CoreOS and Weave</span></span>](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave)
* [<span data-ttu-id="4f564-208">Kubernetes Visualizer</span><span class="sxs-lookup"><span data-stu-id="4f564-208">Kubernetes Visualizer</span></span>](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/)
* [<span data-ttu-id="4f564-209">Azure용 Jenkins 슬레이브 플러그 인</span><span class="sxs-lookup"><span data-stu-id="4f564-209">Jenkins Slave Plug-in for Azure</span></span>](http://msopentech.com/blog/2014/09/23/announcing-jenkins-slave-plugin-azure/)
* [<span data-ttu-id="4f564-210">GitHub 리포지토리: Azure용 Jenkins 저장소 플러그인</span><span class="sxs-lookup"><span data-stu-id="4f564-210">GitHub repo: Jenkins Storage Plug-in for Azure</span></span>](https://github.com/jenkinsci/windows-azure-storage-plugin)
* [<span data-ttu-id="4f564-211">타사: Azure용 Hudson 슬레이브 플러그인</span><span class="sxs-lookup"><span data-stu-id="4f564-211">Third Party: Hudson Slave Plug-in for Azure</span></span>](http://wiki.hudson-ci.org/display/HUDSON/Azure+Slave+Plugin)
* [<span data-ttu-id="4f564-212">타사: Azure용 Hudson Storage 플러그인</span><span class="sxs-lookup"><span data-stu-id="4f564-212">Third Party: Hudson Storage Plug-in for Azure</span></span>](https://github.com/hudson3-plugins/windows-azure-storage-plugin)
* [<span data-ttu-id="4f564-213">비디오: Chef의 정의 및 작동 방식</span><span class="sxs-lookup"><span data-stu-id="4f564-213">Video: What is Chef and How does it Work?</span></span>](https://msopentech.com/blog/2014/03/31/using-chef-to-manage-azure-resources/)
* [<span data-ttu-id="4f564-214">비디오: Linux VM에서 Azure 자동화를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="4f564-214">Video: How to Use Azure Automation with Linux VMs</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Azure-Automation-104-managing-Linux-and-creating-Modules-with-Joe-Levy)
* [<span data-ttu-id="4f564-215">블로그: Linux용 Powershell DSC 작업 방법</span><span class="sxs-lookup"><span data-stu-id="4f564-215">Blog: How to do Powershell DSC for Linux</span></span>](http://blogs.technet.com/b/privatecloud/archive/2014/05/19/powershell-dsc-for-linux-step-by-step.aspx)
* [<span data-ttu-id="4f564-216">GitHub: Docker 클라이언트 DSC</span><span class="sxs-lookup"><span data-stu-id="4f564-216">GitHub: Docker Client DSC</span></span>](https://github.com/anweiss/DockerClientDSC)
* [<span data-ttu-id="4f564-217">Azure용 Packer 플러그인</span><span class="sxs-lookup"><span data-stu-id="4f564-217">Packer plugin for Azure</span></span>](https://github.com/msopentech/packer-azure)

