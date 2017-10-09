---
title: "Azure에서 Linux Vm의 aaaOverview | Microsoft Docs"
description: "Linux 가상 컴퓨터를 사용하여 Azure 계산, 저장소 및 네트워킹 서비스를 설명합니다."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: rickstercdn
manager: timlt
editor: 
ms.assetid: 7965a80f-ea24-4cc2-bc43-60b574101902
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 09/14/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 958e219d53026d787a7a41f2fd13c29c739a9238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux"></a>Azure 및 Linux
Microsoft Azure는 솔루션을 호스팅하는 데 적합한 분석, Virtual Machines, 데이터베이스, 모바일, 네트워킹, 저장소 및 웹을 비롯한 나날이 다양해지는 통합 공용 클라우드 서비스입니다.  Microsoft Azure는 용도, 원할 때-tooinvest에서 온-프레미스 하드웨어가 필요 없이 대 한 사용량 기준 과금 tooonly 수 있는 확장 가능한 컴퓨팅 플랫폼을 제공 합니다.  Azure는 때 tooscale를 솔루션의 클라이언트 tooservice hello 요구 필요한 toowhatever 스케일 아웃 준비 합니다.

익숙한는 hello Amazon의의 다양 한 기능 검사할 수 AWS, Azure vs AWS hello [정의 매핑 문서](https://azure.microsoft.com/campaigns/azure-vs-aws/mapping/)합니다.

## <a name="regions"></a>영역
Microsoft Azure 리소스 hello 전 세계 여러 지리적 지역에 걸쳐 분산 됩니다.  "지역"은 동일한 지리적 지역에서 여러 데이터 센터를 나타냅니다.  일반적으로 사용 가능한 34 지역이 발표 하는 추가 4 지역 hello 전 세계 해야 합니다. Tooexpand 우리의 글로벌 검사-계속 하기 때문에 기존 및 새로 업데이트 된 목록을 발표 영역을 유지 합니다.

* [Azure 지역](https://azure.microsoft.com/regions/)

## <a name="availability"></a>Availability
업계 선두 단일 인스턴스 가상 컴퓨터를 서비스 수준 계약 99.9%의 모든 디스크에 대 한 프리미엄 저장소가 hello VM을 배포한 제공를 발표 했습니다.  표준 99.95%에 배포 tooqualify 되려면에서 VM 서비스 수준 계약에 여전히 필요 하면 toodeploy 가용성 집합 내에서 워크 로드를 실행 하는 두 개 이상의 Vm입니다. 이렇게 하면 VM이 데이터 센터에서 여러 오류 도메인 간에 분산될 뿐만 아니라 다양한 유지 관리 창이 있는 호스트에 배포됩니다. 전체 hello [Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/) 설명 hello 전체적으로 Azure의 가용성을 보장 합니다.

## <a name="managed-disks"></a>Managed Disks

관리 디스크 핸들 Azure 저장소 계정 만들기 및 사용자에 대 한 hello 백그라운드에서 관리 및의 hello 저장소 계정 확장성 제한 hello에 대 한 tooworry 있는지를 확인 합니다. Hello 디스크 크기와 hello 성능 계층 (Standard 또는 Premium) 단순히 지정 하 고 Azure 위해 만들고 관리 hello 디스크 있습니다. 디스크를 더하거나 hello VM 확장 및 축소가 서 되더라도 tooworry hello 저장소 사용량에 대 한 필요는 없습니다. 새 Vm을 만드는 경우 [hello Azure CLI 2.0을 사용 하 여](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 관리 되는 OS 및 데이터 디스크와 Azure 포털 toocreate Vm을 환영 합니다. 관리 되지 않는 디스크가 있는 Vm를 설정한 경우 다음을 할 수 있습니다 [관리 하는 디스크를 통해 지원 하 여 Vm toobe 변환](convert-unmanaged-to-managed-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

또한 Azure 지역 마다 하나의 저장소 계정에 사용자 지정 이미지를 관리 하 고 hello에 Vm의 toocreate 수백 사용 수 동일한 구독 합니다. 관리 되는 디스크에 대 한 자세한 내용은 hello를 참조 하십시오 [디스크 관리 개요](../windows/managed-disks-overview.md)합니다.

## <a name="azure-virtual-machines--instances"></a>Azure Virtual Machines 및 인스턴스
Microsoft Azure는 많은 파트너가 제공하고 유지 관리하는 다양하고 인기 있는 Linux 배포를 지원합니다.  Red Hat Enterprise, CentOS, Debian, Ubuntu, CoreOS, RancherOS, FreeBSD 및 더 hello Azure Marketplace에서에서 같은 배포판을 찾을 수 있습니다. 적극적으로 협력 다양 한 Linux 커뮤니티 tooadd 더 많은 버전 toohello [Azure 보증 Linux 배포판](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 목록입니다.

선택한 사용자 기본 설정된 Linux 배포판 현재 hello 갤러리에 있는 경우 가져올 수 있습니다"고유한 Linux"로 VM [만들기 및 Azure에서 Linux VHD 업로드](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

Azure 가상 컴퓨터를 사용 하면 다양 한 컴퓨팅 agile 방법으로 솔루션 toodeploy 있습니다. 거의 모든 운영 체제(Windows, Linux 또는 증가하는 파트너 목록 중 하나에서 사용자 지정으로 만든 운영 체제)에서 거의 모든 워크로드 및 언어를 배포할 수 있습니다. 그래도 원하는 내용이 표시되지 않나요?  걱정하지 마세요. 온-프레미스에서 고유한 이미지를 가져올 수 있습니다.

## <a name="vm-sizes"></a>VM 크기
Azure에서 VM을 배포 하면 tooselect 우리의 일련의 크기에 적합 한 tooyour 작업 중 하나에서 v M 크기 하려고 합니다. hello 크기 hello를 처리 성능, 메모리 및 hello 가상 컴퓨터의 저장 용량에도 영향을 줍니다. VM을 실행 하 고 할당된 된 리소스를 사용해 시간 hello hello 금액에 따라 청구 됩니다. [Virtual Machine 크기](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)의 전체 목록입니다.

다음은 시리즈(A, D, DS, G 및 GS) 중 하나에서 VM 크기를 선택하기 위한 몇 가지 기본 지침입니다.
* A 시리즈 VM은 간단한 워크로드 및 개발/테스트 시나리오에 대한 초급 수준의 VM 가격을 책정한 값입니다. 모든 지역에서 광범위 하 게 사용할 수 있는 하 고 연결 및 모든 표준 리소스 사용 가능한 toovirtual 컴퓨터를 사용 합니다.
* A 시리즈 크기(A8-A11)는 고성능 계산 클러스터 응용 프로그램에 적합한 특수한 계산 집약적 구성입니다.
* D 시리즈 Vm은 더 뛰어난 계산 기능과 임시 디스크 성능이 요구 하는 디자인 된 toorun 응용 프로그램. D 시리즈 Vm hello 임시 디스크에 대 한 빠른 프로세서, 더 높은 메모리 대 코어 비율, 및는 SSD (반도체 드라이브)를 제공합니다.
* Dv2 시리즈, D 시리즈의 hello 최신 버전을 더 강력한 CPU 기능. hello Dv2 시리즈 CPU은 약 35 %hello 보다 더 빠르게 D 시리즈 CPU입니다. 에 기반 하는 hello 최신 세대 2.4 g h z Intel Xeon® E5-2673 v3 (Haskell) 프로세서 및 Intel 터보 증폭 기술 2.0 hello로 too3.2 g h z 위로 이동할 수 있습니다. hello Dv2 시리즈에 D 시리즈 hello으로 같은 메모리 및 디스크 구성 hello 합니다.
* G 시리즈 Vm hello 가장 많은 메모리를 제공 하 고 Intel Xeon E5 V3 제품군 프로세서가 있는 호스트에 실행 합니다.

참고: DS 시리즈 및 GS 시리즈 Vm은 저장소 액세스 tooPremium-우리의 SSD I/O가 많은 작업에 대 한 고성능의 대기 시간이 짧은 저장소를 백업 합니다. Premium Storage는 특정 지역에서만 사용할 수 있습니다. 자세한 내용은 다음을 참조하세요.

* [Premium Storage: Azure 가상 컴퓨터 작업을 위한 고성능 저장소](../../storage/common/storage-premium-storage.md)

## <a name="automation"></a>Automation
tooachieve 적절 한 DevOps culture 모든 인프라 코드 여야 합니다.  인프라를 hello 모든 생활에서 코드를 쉽게 수 (피닉스 서버)를 다시 생성 합니다.  Azure는 hello 주요 자동화 모든 Ansible, Chef, SaltStack, puppet과 같은 도구와 함께 작동 합니다.  또한 Azure는 자체 자동화 도구도 제공합니다.

* [Azure 템플릿](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Azure는 Azure를 지원하는 대부분의 Linux 배포판에서 [cloud-init](http://cloud-init.io/)에 대한 지원을 롤아웃하고 있습니다.  현재 Canonical의 Ubuntu VM은 기본적으로 사용하도록 설정된 cloud-init와 함께 배포됩니다.  그러나 빨간색 Hats RHEL, CentOS 및 클라우드 init 지원, Azure hello Fedora RedHat에서 유지 관리 하는 이미지 클라우드 init 설치할 필요가 없습니다.  toouse 클라우드 초기화 RedHat 제품군 운영 체제에서 클라우드 init 설치로 사용자 지정 이미지를 만들 해야 있습니다.

* [Azure Linux VM에서 cloud-init 사용](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quotas"></a>할당량
각 Azure 구독 기본 할당량 한도 프로젝트에 대 한 Vm의 다 수의 hello 배포에 영향을 줄 수 있는 위치에 있습니다. hello 현재 구독 별로 제한은 / 지역당 20 대의 Vm입니다.  제한 증가를 요구하는 지원 티켓을 제출하면 할당량 제한을 빠르고 쉽게 늘릴 수 있습니다.  할당량 제한에 대한 자세한 내용은 다음을 참조하세요.

* [Azure 구독 서비스 제한](../../azure-subscription-service-limits.md)

## <a name="partners"></a>파트너
Microsoft는 사용 가능한 tooensure hello 이미지 업데이트 되 고 Azure 런타임에 대 한 액세스에 최적화 된 파트너와 밀접 하 게 작동 합니다.  파트너에 대한 자세한 내용은 아래의 해당 마켓플레이스 페이지를 확인하세요.

* Azure의 Linux - [보증 배포판](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* SUSE- [Azure Marketplace - SUSE Linux Enterprise Server](https://azuremarketplace.microsoft.com/en-us/marketplace/apps?search=%27SUSE%27)
* Redhat - [Azure Marketplace - RedHat Enterprise Linux 7.2](https://azure.microsoft.com/marketplace/partners/redhat/redhatenterpriselinux72/)
* Canonical - [Azure Marketplace - Ubuntu Server 16.04 LTS](https://azure.microsoft.com/marketplace/partners/canonical/ubuntuserver1604lts/)
* Debian - [Azure Marketplace - Debian 8 "Jessie"](https://azure.microsoft.com/marketplace/partners/credativ/debian8/)
* FreeBSD - [Azure Marketplace - FreeBSD 10.3](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
* CoreOS - [Azure Marketplace - CoreOS(Stable)](https://azure.microsoft.com/marketplace/partners/coreos/coreosstable/)
* RancherOS - [Azure Marketplace - RancherOS](https://azure.microsoft.com/marketplace/partners/rancher/rancheros/)
* Bitnami - [Bitnami Library for Azure](https://azure.bitnami.com/)
* Mesosphere - [Azure Marketplace - Mesosphere DC/OS on Azure](https://azure.microsoft.com/marketplace/partners/mesosphere/dcosdcos/)
* Docker - [Azure Marketplace - Azure Container Service with Docker Swarm](https://azure.microsoft.com/marketplace/partners/microsoft/acsswarms/)
* Jenkins - [Azure Marketplace - CloudBees Jenkins Platform](https://azure.microsoft.com/marketplace/partners/cloudbees/jenkins-platformjenkins-platform/)

## <a name="getting-started-with-linux-on-azure"></a>Azure에서 Linux 시작
Azure 계정, Azure CLI 설치 hello 및 SSH 공개 및 개인 키 쌍 필요한 Azure를 사용 하 여 toobegin 합니다.

### <a name="sign-up-for-an-account"></a>계정 등록
Azure 클라우드 hello를 사용 하 여 hello 첫 번째 단계에는 Azure 계정에 대해 toosign입니다.  Toohello 이동 [Azure 계정 등록](https://azure.microsoft.com/pricing/free-trial/) tooget 시작 페이지입니다.

### <a name="install-hello-cli"></a>Hello CLI를 설치 합니다.
새 Azure 계정으로 시작할 수 있는 hello 웹 기반 관리 패널은 Azure 포털을 사용 하 여 즉시 합니다.  hello 설치 toomanage hello hello 명령줄을 통해 Azure 클라우드, `azure-cli`합니다.  Hello 설치 [Azure CLI 2.0](/cli/azure/install-azure-cli) Mac 또는 Linux 워크스테이션에 설치 합니다.

### <a name="create-an-ssh-key-pair"></a>SSH 키 쌍 만들기
이제는 Azure 계정, hello Azure 웹 포털 및 Azure CLI hello 있어야 합니다.  hello 다음 단계는 toocreate 암호를 사용 하지 않고 Linux에 사용 되는 tooSSH 있는 SSH 키 쌍입니다.  [Linux 및 Mac에서 SSH 키 만들기](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooenable 암호 없는 로그인 되 고 보안이 강화 됩니다.

### <a name="create-a-vm-using-hello-cli"></a>Hello CLI를 사용 하 여 VM 만들기
Linux VM을 만드는 빠른 방법을 toodeploy 없이 종료 hello 터미널에서 작업 하는 VM은 hello CLI를 사용 하 여입니다.  명령줄 플래그 또는 스위치를 통해 사용할 수 있는 모두 hello 웹 포털에서 지정할 수 있습니다.  

* [Hello CLI를 사용 하 여 Linux VM 만들기](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="create-a-vm-in-hello-portal"></a>Hello 포털에서 VM 만들기
Hello Azure 웹 포털에서 Linux VM을 만드는 방법은 tooeasily 지점과 클릭 광고 hello 다양 한 옵션 tooget tooa 배포 합니다.  명령줄 플래그 또는 스위치를 사용 하는 대신 수 tooview 멋진 웹 레이아웃의 다양 한 옵션 및 설정 됩니다.  Hello 명령줄 인터페이스를 통해 사용 가능한 모든 hello 포털에서 사용할 수도 있습니다.

* [Hello 포털을 사용 하 여 Linux VM 만들기](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="login-using-ssh-without-a-password"></a>SSH를 사용하여 암호 없이 로그인
hello VM은 Azure에서 실행 되며에서 준비 toolog 합니다.  SSH 통해에서 암호 toolog를 사용 하는 것은 안전 하지 않은 고 시간이 많이 소요입니다.  SSH 키를 사용 하 여 가장 안전한 방법 및 hello 가장 빠른 방법은 toologin hello 됩니다.  사용자가 만든 Linux VM hello 포털 또는 hello CLI 통해 때 두 가지 인증 선택 합니다.  SSH에 대 한 암호를 선택 하는 경우 Azure hello VM tooallow 로그인 암호를 통해 구성 됩니다.  Azure VM hello 구성 toouse SSH 공개 키를 선택한 경우 tooonly SSH 통해 로그인을 허용할 키 및 암호 로그인을 사용 하지 않도록 설정 합니다. 만 하 여 Linux VM을 사용 하 여 SSH 키 로그인 허용 toosecure hello hello CLI 또는 hello 포털에서 VM 만들기 중 SSH 공개 키 옵션입니다.

## <a name="related-azure-components"></a>관련 Azure 구성 요소
## <a name="storage"></a>저장소
* [Azure 저장소 소개 tooMicrosoft](../../storage/common/storage-introduction.md)
* [디스크 tooa hello azure cli를 사용 하 여 Linux VM 추가](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Tooattach 데이터 hello Azure 포털에서에서 Linux VM tooa 디스크 하는 방법](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="networking"></a>네트워킹
* [Virtual Network 개요](../../virtual-network/virtual-networks-overview.md)
* [Azure의 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)
* [Azure에서 Linux VM 포트 tooa 열기](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Hello Azure 포털에서에서 정규화 된 도메인 이름 만들기](portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="containers"></a>컨테이너
* [Azure Virtual Machines 및 컨테이너](containers.md)
* [Azure 컨테이너 서비스 소개](../../container-service/container-service-intro.md)
* [Azure 컨테이너 서비스 클러스터 배포](../../container-service/dcos-swarm/container-service-deployment.md)

## <a name="next-steps"></a>다음 단계
이제 Azure의 Linux를 대략적으로 이해하게 되었을 것입니다.  hello 다음 단계에 toodive 이며 몇 가지 Vm 만들기.

* [Azure CLI를 통해 일반 작업을 위한 샘플 스크립트 확장 목록 탐색](cli-samples.md)
