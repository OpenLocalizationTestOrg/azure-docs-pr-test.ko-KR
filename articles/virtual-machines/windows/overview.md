---
title: "가상 컴퓨터 개요 aaaWindows | Microsoft Docs"
description: "Azure에서 Windows 가상 컴퓨터 만들기 및 관리에 대해 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: fbae9c8e-2341-4ed0-bb20-fd4debb2f9ca
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 8015b1aa4bcdaac2e721f25d85a5bc995a22f0f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-windows-virtual-machines-in-azure"></a>Azure에서의 Windows 가상 컴퓨터 개요

Azure Virtual Machines(VM)는 Azure에서 제공하는 여러 유형의 [확장성 있는 주문형 컴퓨팅 리소스](../../app-service-web/choose-web-site-cloud-service-vm.md) 중 하나입니다. 일반적으로 hello 다른 선택 항목이 제공 보다 hello 컴퓨팅 환경 보다 더 많은 제어 해야 하는 경우 VM 선택 합니다. 이 문서에서는 VM을 만들기 전에 고려해야 하는 요구 사항, 만드는 방법 및 관리하는 방법에 대해 설명합니다.

Azure VM을 제공 toobuy 않고도 가상화의 유연성을 hello hello 물리적 하드웨어를 유지 관리를 실행 합니다. 그러나 보내야 toomaintain hello VM 구성, 패치, 및를 실행 하는 hello 소프트웨어 설치 등의 작업을 수행 하 여 합니다.

Azure 가상 컴퓨터는 다양한 방식으로 사용할 수 있습니다. 일부 사례:

* **개발 및 테스트** – 빠른을 제공 하는 Azure Vm 및 특정 구성 사용 하 여 컴퓨터를 쉽게 toocreate toocode 필요한 응용 프로그램을 테스트 합니다.
* **Hello 클라우드에서 응용 프로그램** – 경제 의미 toorun를 수행할 수 있는 응용 프로그램에 대 한 수요가 변동 수 있으므로 Azure에서 VM에 있습니다. 필요할 경우 여분의 VM에 대해 비용을 지불하고, 그렇지 않은 경우에는 해당 VM을 종료합니다.
* **데이터 센터 확장** – Azure 가상 네트워크의 가상 컴퓨터는 연결 된 tooyour 조직 네트워크를 가능성이 높습니다.

hello 번호 응용 프로그램에서 사용 하는 Vm의 확장할 수 및 toowhatever 아웃가 필요한 toomeet 필요 합니다.

## <a name="what-do-i-need-toothink-about-before-creating-a-vm"></a>어떻게 해야 합니까 toothink에 대 한 VM을 만들기 전에?
Azure에서 응용 프로그램 인프라를 구축하는 경우에는 언제나 다양한 [디자인 고려 사항](/architecture/reference-architectures/virtual-machines-linux?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)이 있습니다. 통합 문서를 시작 하기 전에 VM의 이러한 측면에 대 한 중요 한 toothink은:

* 응용 프로그램 리소스의 hello 이름
* hello 리소스가 저장 되는 hello 위치
* hello VM의 hello 크기
* hello 만들 수 있는 Vm의 최대 수
* VM hello hello 운영 체제 실행
* hello 시작 된 후 VM의 hello 구성
* vm 해당 hello hello 관련 리소스

### <a name="naming"></a>이름 지정
가상 컴퓨터에는 [이름](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 하며 할당 된 tooit hello 운영 체제의 일부분으로 구성 된 컴퓨터 이름이 있습니다. VM의 hello 이름 too15 문자를 수 있습니다.

Azure toocreate hello 운영 체제 디스크를 hello 컴퓨터 이름을 사용 하 고 hello 가상 컴퓨터 이름에는 hello 동일 합니다. 경우 있습니다 [업로드 하 고 사용자 고유의 이미지 사용](upload-generalized-managed.md) hello 이름은 다를 수 있습니다, 이전에 구성 된 운영 체제를 포함 하 고 toocreate 가상 컴퓨터를 사용 합니다. 사용자 고유의 이미지 파일을 업로드 하는 hello 운영 체제에서 컴퓨터 이름을 hello 및 hello 가상 컴퓨터 이름이 동일 hello 하는 것이 좋습니다.

### <a name="locations"></a>위치
Azure에서 만든 모든 리소스를 여러 배포 [지리적 영역](https://azure.microsoft.com/regions/) hello 전 세계 합니다. Hello 영역 이라고 일반적으로 **위치** VM을 만들 때. Hello 위치는 VM에 대 한 hello 가상 하드 디스크가 저장 되는 위치를 지정 합니다.

이 표에서 hello 방법을 사용할 수 있는 위치의 목록을 가져올 수 있습니다.

| 메서드 | 설명 |
| --- | --- |
| Azure portal |VM을 만들 때 hello 목록에서 위치를 선택 합니다. |
| Azure PowerShell |사용 하 여 hello [Get AzureRmLocation](/powershell/module/azurerm.resources/get-azurermlocation) 명령입니다. |
| REST API |사용 하 여 hello [지점](https://docs.microsoft.com/rest/api/resources/subscriptions#Subscriptions_ListLocations) 작업 합니다. |

### <a name="vm-size"></a>VM 크기
hello [크기](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 의 hello 사용 하는 VM에 의해 결정 됩니다 hello 작업 toorun 되도록 합니다. 사용자가 선택한 hello 크기는 다음 성능, 메모리 및 저장소 용량을 처리 하는 등의 요소를 결정 합니다. Azure는 다양 한 유형의 사용 하 여 다양 한 크기 toosupport 제공합니다.

Azure 청구는 [시간당 가격](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) hello VM의 크기와 운영 체제에 따라 합니다. 부분 시간의 경우 Azure는 사용 하는 hello 분에 대해서만 요금. 저장소는 가격이 책정되며 개별적으로 청구됩니다.

### <a name="vm-limits"></a>VM 제한
사용자 구독에는 기본 [할당량 한도](../../azure-subscription-service-limits.md) 프로젝트에 대 한 많은 Vm의 hello 배포에 영향을 줄 수 있는 위치에 있습니다. hello 현재 구독 별로 제한은 / 지역당 20 대의 Vm입니다. 증가를 요구하는 지원 티켓을 제출하면 제한 량이 늘어날 수 있습니다.

### <a name="operating-system-disks-and-images"></a>운영 체제 디스크 및 이미지
가상 컴퓨터를 사용 하 여 [가상 하드 디스크 (Vhd)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toostore 운영 체제 (OS) 및 데이터입니다. Vhd는 tooinstall OS에서에서 선택할 수 있습니다 hello 이미지에도 사용 됩니다. 

Azure에서 제공 많은 [마켓플레이스 이미지](https://azure.microsoft.com/marketplace/virtual-machines/) toouse 다양 한 버전 및 Windows Server 운영 체제의 종류입니다. 마켓플레이스 이미지는 이미지 게시자, 제안, SKU 및 버전(대개 최신으로 지정된 버전)으로 식별됩니다. 

이 표에서 이미지에 대 한 hello 정보를 찾을 수 있는 몇 가지 방법에 설명 합니다.

| 메서드 | 설명 |
| --- | --- |
| Azure portal |hello 값은 이미지 toouse를 선택 하면 드립니다 자동으로 지정 됩니다. |
| Azure PowerShell |[Get-AzureRMVMImagePublisher](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/get-azurermvmimagepublisher) -Location "location"<BR>[Get-AzureRMVMImageOffer](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/get-azurermvmimageoffer) -Location "location" -Publisher "publisherName"<BR>[Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) -Location "location" -Publisher "publisherName" -Offer "offerName" |
| REST API |[이미지 게시자 나열](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publishers)<BR>[이미지 제안 나열](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publisher-offers)<BR>[이미지 SKU 나열](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publisher-offer-skus) |

너무 선택할 수 있습니다[업로드 하 고 사용자 고유의 이미지 사용](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account) hello 게시자 이름, 제안 및 sku 이렇게 하면 사용 되지 않습니다.

### <a name="extensions"></a>확장
VM [확장](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)은 배포 후 구성 및 자동화 작업을 통해 VM 추가 기능을 제공합니다.

다음과 같은 일반 작업은 확장을 사용하여 수행할 수 있습니다.

* **사용자 지정 스크립트를 실행** – hello [사용자 지정 스크립트 확장](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello VM 프로 비전 될 때 스크립트를 실행 하 여 hello VM에서 작업을 구성 하도록 도와줍니다.
* **배포 및 구성 관리** – hello [PowerShell 필요한 상태 구성 (DSC) 확장](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 쉽게 DSC VM toomanage에 설정할 수 구성 / 환경입니다.
* **진단 데이터 수집** – hello [Azure 진단 확장](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toomonitor 사용된 될 수 있는 hello VM toocollect 진단 데이터를 구성 하면 hello 응용 프로그램의 상태입니다.

### <a name="related-resources"></a>관련 리소스
hello이이 테이블의 hello VM에서 사용 및 tooexist 필요 리소스나 VM hello를 만들 때 만들 수 있습니다.

| 리소스 | 필수 | 설명 |
| --- | --- | --- |
| [리소스 그룹](../../azure-resource-manager/resource-group-overview.md) |예 |hello VM 리소스 그룹에 포함 되어야 합니다. |
| [저장소 계정](../../storage/common/storage-create-storage-account.md) |예 |hello VM 해당 가상 하드 디스크를 저장소 계정 toostore hello 필요합니다. |
| [가상 네트워크](../../virtual-network/virtual-networks-overview.md) |예 |hello VM 가상 네트워크의 구성원 이어야 합니다. |
| [공용 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) |아니요 |hello VM에 액세스 하는 공용 IP 주소 할당 tooit tooremotely가 있을 수 있습니다. |
| [네트워크 인터페이스](../../virtual-network/virtual-network-network-interface.md) |예 |hello VM hello 네트워크에서 네트워크 인터페이스 toocommunicate hello 필요합니다. |
| [데이터 디스크](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |아니요 |hello VM 데이터 디스크가 tooexpand 저장소 기능을 포함할 수 있습니다. |

## <a name="how-do-i-create-my-first-vm"></a>첫 번째 VM을 만드는 방법
VM을 만들기 위한 몇 가지 옵션이 있습니다. hello 선택한 사항이 있는 hello 환경에 따라 달라 집니다. 

이 표에서 정보 tooget VM 만들기를 시작 합니다.

| 메서드 | 문서 |
| --- | --- |
| Azure portal |[Hello 포털을 사용 하 여 Windows를 실행 하는 가상 컴퓨터 만들기](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| 템플릿 |[리소스 관리자 템플릿을 사용하여 Windows 가상 컴퓨터 만들기](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Azure PowerShell |[PowerShell을 사용하여 Windows VM 만들기](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| 클라이언트 SDK |[C#를 사용하여 Azure 리소스 배포](csharp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| REST API |[VM 만들기 또는 업데이트](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-create-or-update) |

문제가 결코 발생하지 않기를 바라지만 때로는 몇몇 문제가 발생하기도 합니다. 이러한 상황은 tooyou 발생 하는 경우에 hello 정보를 볼 [문제를 해결 하는 리소스 관리자 배포 문제 Azure에서 Windows 가상 컴퓨터 만들기에](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

## <a name="how-do-i-manage-hello-vm-that-i-created"></a>Hello 만든 VM을 관리 하려면 어떻게 해야 합니까?
VM은 스크립팅 지원을 통해 브라우저 기반 포털, 명령줄 도구로 관리하거나 REST API를 통해 직접 관리할 수 있습니다. 수행할 수 있는 몇 가지 일반적인 관리 작업에는 VM에 대 한 정보를 가져오기는 tooa VM 가용성, 관리 하 고 백업에 대 한 로깅을 합니다.

### <a name="get-information-about-a-vm"></a>VM 관련 정보 가져오기
이 표에 하면 VM에 대 한 정보를 얻을 수 있는 hello 방식 중 몇 있습니다.

| 메서드 | 설명 |
| --- | --- |
| Azure portal |Hello 허브 메뉴에서 클릭 **가상 컴퓨터** hello 목록에서 hello VM을 선택 합니다. Hello VM에 대 한 hello 블레이드에서에 toooverview 정보에 액세스, 값 설정 및 모니터링 메트릭에서 있는 있습니다. |
| Azure PowerShell |PowerShell toomanage Vm 사용 하는 방법에 대 한 정보를 참조 하십시오. [만들기 hello Azure PowerShell 모듈을 사용 하 여 Windows Vm을 관리 하 고](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. |
| REST API |사용 하 여 hello [VM 가져오기 정보](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get) VM에 대 한 작업 tooget 정보입니다. |
| 클라이언트 SDK |C# toomanage Vm 사용 하는 방법에 대 한 정보를 참조 하십시오. [Azure 리소스 관리자 및 C#을 사용 하 여 관리 Azure 가상 컴퓨터](csharp-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. |

### <a name="log-on-toohello-vm"></a>Toohello VM에 로그온
단추를 사용 하면 hello 연결 hello Azure 포털에서에서 너무[RDP (원격 데스크톱) 세션을 시작](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. 발생할 수 있는 경우에 따라 잘못 된 toouse 원격 연결을 시도할 때. 이 경우 tooyou 경우 체크 아웃의 hello 도움말 정보 [문제를 해결 하는 원격 데스크톱 연결 tooan Azure Windows를 실행 하는 가상 컴퓨터](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

### <a name="manage-availability"></a>가용성 관리
가 위해서는 toounderstand 있습니다 어떻게 너무[고가용성을 보장](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 응용 프로그램에 대 한 합니다. 이 구성을 하나 이상 실행 하는 여러 Vm tooensure을 만들어야 합니다.

프로그램 배포 tooqualify 우리의 99.95 VM 서비스 수준 계약에 대 한, 해야 toodeploy 내 작업을 실행 하는 두 개 이상의 Vm는 [가용성 집합](tutorial-availability-sets.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. 이렇게 구성하면 VM이 여러 오류 도메인 간에 분산되고, 다양한 유지 관리 창을 사용하는 호스트에 배포됩니다. 전체 hello [Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/) 설명 hello 전체적으로 Azure의 가용성을 보장 합니다.

### <a name="back-up-hello-vm"></a>Hello VM 백업
A [복구 서비스 자격 증명 모음](../../backup/backup-introduction-to-azure-backup.md) 는 tooprotect 사용 되는 데이터 및 자산을 모두 Azure 백업 및 Azure 사이트 복구 서비스입니다. 복구 서비스 자격 증명 모음에도 사용할 수 있습니다[배포 및 PowerShell을 사용 하 여 리소스 관리자를 통해 배포 된 Vm에 대 한 백업 관리](../../backup/backup-azure-vms-automation.md)합니다. 

## <a name="next-steps"></a>다음 단계
* 확인 하려는 toowork Linux Vm이 있는 경우 [Azure와 Linux](../linux/overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.
* Hello에서 인프라를 설정 하는 주변 hello 지침에 대 한 자세한 [예제에서는 Azure 인프라 연습](infrastructure-example.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
