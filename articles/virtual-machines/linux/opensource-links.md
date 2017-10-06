---
title: "aaaLinux 및 오픈 소스 azure 컴퓨팅 | Microsoft Docs"
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
ms.openlocfilehash: 3ce0dcc65f28d0dddb29f654409f6dae56213bc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="linux-and-open-source-computing-on-azure"></a>Azure의 오픈 소스 컴퓨팅 및 Linux
Hello 클래식 배포 모델에서 Linux 기반 가상 컴퓨터를 관리 및 toocreate 해야 모든 hello 설명서를 찾습니다.

> [!IMPORTANT] 
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.

## <a name="get-started"></a>시작
* [Azure의 Linux에 대한 소개](intro-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [자주 묻는 질문에 대 한 Azure 가상 컴퓨터 hello 클래식 배포 모델을 사용 하 여 만든](classic/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [가상 컴퓨터에 대한 이미지 정보](../windows/classic/about-images.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [사용자 고유의 Distro 이미지 업로드](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)(및 [Azure 보증 배포판](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 사용 지침)
* [Azure 클래식 포털을 사용 하 여 Linux VM hello tooa에 로그온](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="set-up"></a>설정
* [Azure 명령줄 인터페이스(Azure CLI) 설치](../../cli-install-nodejs.md)

## <a name="tutorials"></a>자습서
* [LAMP 스택 hello Azure에서 Linux 가상 컴퓨터에 설치](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure VM의 Ruby on Rails 웹 응용 프로그램](classic/virtual-machines-linux-classic-ruby-rails-web-app.md)
* [방법: AMQP 및 서비스 버스용 Apache Qpid Proton-C 설치](../../service-bus-messaging/service-bus-amqp-apache.md)

### <a name="databases"></a>데이터베이스
* [Azure에서 MySQL 성능 최적화](classic/optimize-mysql.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [MySQL 클러스터](classic/mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Azure에서 Linux 환경의 Cassandra 실행 및 Node.js에서 Cassandra에 액세스](classic/cassandra-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [MariaDbs의 다중 마스터 클러스터 만들기](classic/mariadb-mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="hpc"></a>HPC
* [Azure에서 HPC Pack 클러스터의 Linux 계산 노드 시작](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Azure의 Linux 계산 노드에서 Microsoft HPC 팩을 사용하여 NAMD 실행](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Linux RDMA 클러스터 toorun MPI 응용 프로그램 설정](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="docker"></a>Docker
* [Hello Azure CLI (명령줄 인터페이스 Azure)에서 Docker VM 확장 hello를 사용 하 여](classic/cli-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Hello Azure 포털에서에서 Docker VM 확장 hello를 사용 하 여](classic/portal-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [어떻게 toouse docker-Azure에서 컴퓨터](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="ubuntu"></a>Ubuntu
* [방법: MySQL 클러스터](classic/mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [방법: Node.js 및 Cassandra](classic/cassandra-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="opensuse"></a>OpenSUSE
* [방법: MySQL 설치 및 실행](classic/mysql-on-opensuse.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="coreos"></a>CoreOS
* [방법: Azure에서 CoreOS를 사용하는 방법](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="planning"></a>계획
* [Azure 인프라 서비스 구현 지침](../windows/infrastructure-subscription-accounts-guidelines.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Linux 사용자 이름 선택](usernames.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Tooconfigure 가용성에 대해 어떻게 설정 hello 클래식 배포 모델의 가상 컴퓨터](../windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [어떻게 tooSchedule Azure Vm에서 계획 된 유지 관리](classic/planned-maintenance-schedule.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [가상 컴퓨터의 hello 가용성 관리](../windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure에서 Linux 가상 컴퓨터에 대한 계획된 유지 관리](planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="deployment"></a>배포
* [Linux를 실행하는 사용자 지정 가상 컴퓨터 만들기](../windows/classic/createportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [기본 사항 hello: Linux VM tooMake 서식 파일을 캡처](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [보증되지 않는 배포에 대한 정보](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="management"></a>관리
* [SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [어떻게 tooReset 암호나 Linux에 대 한 SSH 속성](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [루트 사용](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="azure-resources"></a>Azure 리소스
* [hello Azure Linux 에이전트](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure VM 확장 및 기능](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [클라우드 init로 VM toouse에 사용자 지정 데이터 삽입](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="storage"></a>저장소
* [데이터 디스크 tooa Linux VM 연결](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Linux VM에서 데이터 디스크 분리](classic/detach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="networking"></a>네트워킹
* [어떻게 tooset azure에서 클래식 가상 컴퓨터에 끝점을](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="troubleshooting"></a>문제 해결
* [SSH (보안 셸) 연결 tooa Linux 기반 Azure 가상 컴퓨터 문제 해결](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure에서 새 Linux 가상 컴퓨터 생성 관련 클래식 배포 문제 해결](classic/troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)  
* [Azure의 기존 Linux 가상 컴퓨터 재시작 또는 크기 조정 관련 클래식 배포 문제 해결](../windows/restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) 

## <a name="reference"></a>참조
* [ASM(Azure 서비스 관리) 모드의 Azure CLI 명령](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [Azure 서비스 관리 REST API](https://msdn.microsoft.com/library/azure/ee460799.aspx)

## <a name="general-links"></a>일반 링크
Microsoft 블로그 Technet 페이지 및 외부 사이트 대신, 위와 같은 Azure.com 설명서 링크를 따라 hello가 됩니다. Azure와 hello 오픈 소스 컴퓨팅 환경으로 고속-이동 하는 대상에는 원래 거의 링크 다음 hello 특정 구식이 *불구 하 고* 우리의 최상의 toocontinually 수행 해야 하는 hello 팩트 최신 항목을 추가 및 제거 오래 된 것입니다. 하나 벗어나 म 경우 알려 주세요 hello 주석에서 알고 오거나 끌어오기 요청 tooour 제출 [GitHub 리포지토리](https://github.com/Azure/azure-content/)합니다.

* [Docker 컨테이너를 사용하여 Linux에서 ASP.NET 5 실행](http://blogs.msdn.com/b/webdev/archive/2015/01/14/running-asp-net-5-applications-in-linux-containers-with-docker.aspx)
* [어떻게 tooDeploy OpenLogic의 CentOS VM 이미지](https://azure.microsoft.com/blog/2013/01/11/deploying-openlogic-centos-images-on-windows-azure-virtual-machines/)
* [SUSE 업데이트 인프라](https://forums.suse.com/showthread.php?5622-New-Update-Infrastructure)
* [SAP Cloud Appliance Library용 SUSE Linux Enterprise Server](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver11sp3forsapcloudappliance/)
* [Azure에서 고가용성 Linux를 빌드하는 12단계](http://blogs.technet.com/b/keithmayer/archive/2014/10/03/quick-start-guide-building-highly-available-linux-servers-in-the-cloud-on-microsoft-azure.aspx)
* [Azure CLI, node.js 및 jhawk를 사용하여 Azure에서 Linux 프로비전 자동화](http://blogs.technet.com/b/keithmayer/archive/2014/11/24/step-by-step-automated-provisioning-for-linux-in-the-cloud-with-microsoft-azure-xplat-cli-json-and-node-js-part-1.aspx)
* [Azure에서 GlusterFS](http://dastouri.azurewebsites.net/gluster-on-azure-part-1/)

### <a name="freebsd"></a>FreeBSD
* [Azure에서 FreeBSD 실행](https://azure.microsoft.com/blog/2014/05/22/running-freebsd-in-azure/)
* [간편한 FreeBSD 배포](http://msopentech.com/blog/2014/10/24/easy-deploy-freebsd-microsoft-azure-vm-depot/)
* [사용자 지정 FreeBSD 이미지 배포](http://msopentech.com/blog/2014/05/14/deploy-customize-freebsd-virtual-machine-image-microsoft-azure/)
* [Linux 파일 서버용 Kaspersky AV](https://azure.microsoft.com/marketplace/partners/kaspersky-lab/kav-for-lfs-kav-for-lfs/)

### <a name="nosql"></a>NoSQL
* [8가지 Azure용 오픈 소스 NoSql 데이터베이스](http://openness.microsoft.com/blog/2014/11/03/open-source-nosql-databases-microsoft-azure/)
* [Slideshare (MSOpenTech):Azure에서 CouchDb 경험](http://www.slideshare.net/brianbenz/experiences-using-couchdb-inside-microsofts-azure-team)
* [node.js, CORS 및 Grunt를 사용하여 CouchDB-as-a-Service 실행](http://msopentech.com/blog/2013/12/19/tutorial-building-multi-tier-windows-azure-web-application-use-cloudants-couchdb-service-node-js-cors-grunt-2/)
* [Hello Azure Redis 캐시 서비스의에서 Windows에서 redis](http://msopentech.com/blog/2014/05/12/redis-on-windows/)
* [Redis용 ASP.NET 세션 상태 공급자 미리 보기 릴리스 발표](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx)
* [블로그: RavenHQ 이제에서 사용할 수 있는 hello Azure 마켓플레이스](https://azure.microsoft.com/blog/2014/08/12/ravenhq-now-available-in-the-azure-store/)

### <a name="big-data"></a>빅 데이터
* [Azure Linux VM에 Hadoop 설치](http://blogs.msdn.com/b/benjguin/archive/2013/04/05/how-to-install-hadoop-on-windows-azure-linux-virtual-machines.aspx)
* [Azure HDInsight](https://azure.microsoft.com/documentation/learning-paths/hdinsight-self-guided-hadoop-training/)

### <a name="relational-database"></a>관계형 데이터베이스
* [Microsoft Azure에서 MySQL 고가용성 아키텍처](http://download.microsoft.com/download/6/1/C/61C0E37C-F252-4B33-9557-42B90BA3E472/MySQL_HADR_solution_in_Azure.pdf)
* [ILB를 사용하는 corosync, pg_bouncer를 통해 Postgres 설치](https://github.com/chgeuer/postgres-azure)

### <a name="linux-high-performance-computing-hpc"></a>Linux HPC(고성능 컴퓨팅)
* [빠른 시작 템플릿: SLURM 클러스터 스핀업](https://github.com/Azure/azure-quickstart-templates/tree/master/slurm) (및 [블로그 게시물](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx))
* [빠른 시작 템플릿: Linux 계산 노드가 포함된 HPC 클러스터 만들기](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/)

### <a name="devops-management-and-optimization"></a>개발, 관리 및 최적화
Devops, 관리 및 최적화의 world hello로 매우 과다가 매우 신속 하 게 변경, 시작 지점 아래 hello 목록을 고려해 야 합니다.

* [비디오: Azure 가상 컴퓨터 : Chef, Puppet 및 Docker를 사용하여 Linux VM 관리](https://azure.microsoft.com/blog/2014/12/15/azure-virtual-machines-using-chef-puppet-and-docker-for-managing-linux-vms/)
* [CoreOS 및 직물 tooautomated Kubernetes 클러스터 배포 가이드를 완료 합니다.](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave)
* [Kubernetes Visualizer](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/)
* [Azure용 Jenkins 슬레이브 플러그 인](http://msopentech.com/blog/2014/09/23/announcing-jenkins-slave-plugin-azure/)
* [GitHub 리포지토리: Azure용 Jenkins 저장소 플러그인](https://github.com/jenkinsci/windows-azure-storage-plugin)
* [타사: Azure용 Hudson 슬레이브 플러그인](http://wiki.hudson-ci.org/display/HUDSON/Azure+Slave+Plugin)
* [타사: Azure용 Hudson Storage 플러그인](https://github.com/hudson3-plugins/windows-azure-storage-plugin)
* [비디오: Chef의 정의 및 작동 방식](https://msopentech.com/blog/2014/03/31/using-chef-to-manage-azure-resources/)
* [비디오: 어떻게 tooUse Linux Vm과 Azure 자동화](http://channel9.msdn.com/Shows/Azure-Friday/Azure-Automation-104-managing-Linux-and-creating-Modules-with-Joe-Levy)
* [블로그: 어떻게 toodo Linux 용 Powershell DSC](http://blogs.technet.com/b/privatecloud/archive/2014/05/19/powershell-dsc-for-linux-step-by-step.aspx)
* [GitHub: Docker 클라이언트 DSC](https://github.com/anweiss/DockerClientDSC)
* [Azure용 Packer 플러그인](https://github.com/msopentech/packer-azure)

