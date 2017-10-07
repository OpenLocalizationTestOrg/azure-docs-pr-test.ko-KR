---
title: "aaaAzure Linux Vm 및 Azure 저장소 | Microsoft Docs"
description: "Linux 가상 컴퓨터와 Azure Standard 및 Premium Storage와 Managed Disks 및 관리되지 않는 디스크를 설명합니다."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: d364c69e-0bd1-4f80-9838-bbc0a95af48c
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 2/7/2017
ms.author: rasquill
ms.openlocfilehash: d34441698a4e59721847685099e5fb3aa378c597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux-vm-storage"></a>Azure 및 Linux VM 저장소
Azure 저장소는 내구성, 가용성 및 고객의 확장성 toomeet hello 요구를 사용 하는 최신 응용 프로그램에 대 한 hello 클라우드 저장소 솔루션입니다.  또한 toomaking에 해당 개발자 toobuild 대규모 응용 프로그램 toosupport 새로운 시나리오에 대 한 가능한 경우 Azure 저장소도 hello 저장소 기반 제공 Azure 가상 컴퓨터에 대 한 합니다.

## <a name="managed-disks"></a>Managed Disks

Azure Vm은 지금 사용 하 여 [Azure 관리 되는 디스크](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json),이 통해 있습니다 toocreate Vm을 만들거나 모든 관리 하지 않고 [Azure 저장소 계정을](../../storage/common/storage-introduction.md) 직접 합니다. 프리미엄 원하는 표준 저장소와 달라진 hello 디스크 있어야 되며, Azure hello VM 디스크를 만듭니다 지정할 수 있습니다. Managed Disks가 있는 VM에는 다음을 포함한 여러 가지 중요한 기능이 있습니다.

- 자동 확장성 지원. Azure는 hello 디스크를 만들고, too10 기본 저장소 toosupport hello 구독 당 000 디스크를 관리 합니다.
- 가용성 집합으로 향상된 안정성. Azure는 가용성 집합 내에서 자동으로 VM 디스크를 서로 분리합니다.
- 향상된 액세스 제어. Managed Disks는 [Azure RBAC(역할 기반 액세스 제어)](../../active-directory/role-based-access-control-what-is.md)로 제어되는 다양한 작업을 노출합니다.

Managed Disks의 가격 책정은 관리되지 않는 디스크의 가격 책정과 다릅니다. 해당 정보는 [Managed Disks에 대한 가격 책정 및 요금 청구](../windows/managed-disks-overview.md#pricing-and-billing)를 참조하세요.

관리 되지 않는 디스크 toouse 관리 되는 디스크를 사용 하는 기존 Vm을 변환할 수 있습니다 [az vm 변환](/cli/azure/vm#convert)합니다. 자세한 내용은 참조 [어떻게 tooconvert Linux VM에서 관리 되지 않는 디스크 tooAzure 관리 하는 디스크](convert-unmanaged-to-managed-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다. Hello 관리 되지 않는 디스크가 경우, 또는 언제 든 지 되었습니다를 사용 하 여 암호화 하는 저장소 계정에 관리 되는 디스크에 관리 되지 않는 디스크를 변환할 수 없습니다 [Azure 저장소 서비스 암호화 SSE ()](../../storage/common/storage-service-encryption.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다. hello 다음 단계 tootooconvert 인 하거나 암호화 된 저장소 계정에 있었던 디스크를 관리 되지 않는 방법을 세부 정보:

- Hello 가상 하드 디스크 (VHD)를 사용 하 여 복사 [az 저장소 blob 복사 시작](/cli/azure/storage/blob/copy#start) tooa 저장소 계정을 Azure 저장소 서비스 암호화에 사용 되지 않습니다.
- 관리되는 디스크를 사용하는 VM을 만들고 [az vm create](/cli/azure/vm#create)로 생성되는 동안 해당 VHD 파일을 지정합니다. 또는
- 연결 hello 복사 된 VHD [az vm 디스크를 연결](/cli/azure/vm/disk#attach) 관리 디스크 tooa 사용 하 여 VM을 실행 합니다.


## <a name="azure-storage-standard-and-premium"></a>Azure Storage: Standard 및 Premium
Managed Disks 또는 관리되지 않는 디스크를 사용하는지 여부에 따라 Azure VM을 표준 저장소 디스크 또는 프리미엄 저장소 디스크에 빌드할 수 있습니다. VM 포털 toochoose hello를 사용 하는 경우 드롭다운 hello에 설정 해야 **기본 사항** 화면 tooview 표준 및 프리미엄 디스크. 때 고쳐져 tooSSD, 프리미엄 저장소만 사용 가능한 Vm가 표시 되지 SSD에서 지 원하는 모든 드라이브입니다.  경우 프리미엄 저장소 SSD에서 지 원하는 Vm 함께 고쳐져 tooHDD, 표준 저장소를 사용할 Vm 디스크 드라이브를 회전 뒷받침 되며 표시 됩니다.

Hello에서 VM을 만들 때 `azure-cli` 선택할 수 있는 표준 및 프리미엄 hello 통해 hello v M 크기를 선택할 때 `-z` 또는 `--vm-size` cli 플래그입니다.

## <a name="creating-a-vm-with-a-managed-disk"></a>Managed Disk를 사용하여 VM 만들기

hello 다음 예제를 실행 하려면 hello 수 있는 Azure CLI 2.0 [여기 설치](/cli/azure/install-azure-cli)합니다.

먼저 리소스 그룹 toomanage hello를 사용 하 여 리소스 만듭니다 [az 그룹 만들기](/cli/azure/group#create):

```azurecli
az group create --location westus --name myResourceGroup
```

이제 만들 VM hello [az vm 만들기](/cli/azure/vm#create)합니다. `mypublicdns`가 사용되었을 것이므로 고유한 `--public-ip-address-dns-name` 인수를 지정합니다.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --public-ip-address-dns-name mypublicdns
```

hello 이전 예제에서는 표준 저장소 계정에 관리 되는 디스크와 VM을 만듭니다. 프리미엄 저장소 계정 toouse 추가 hello `--storage-sku Premium_LRS` hello 다음 예제와 같이 인수:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --public-ip-address-dns-name mypublicdns \
    --storage-sku Premium_LRS
```

## <a name="standard-storage"></a>Standard Storage
표준 azure 저장소에는 저장소의 hello 기본 형식입니다.  Standard Storage는 영구적이면서 동시에 비용 효율적입니다.  

## <a name="premium-storage"></a>Premium Storage
Azure 프리미엄 저장소는 I/O 사용량이 많은 작업을 실행하는 가상 컴퓨터에서 대기 시간이 짧은 고성능 디스크 지원을 제공합니다. 프리미엄 저장소를 사용하는 가상 컴퓨터(VM) 디스크는 솔리드 스테이트 드라이브(SSD)에 데이터를 저장합니다. 응용 프로그램의 VM 디스크 tooAzure 프리미엄 저장소 tootake hello 속도의 장점과 성능 이러한 디스크를 마이그레이션할 수 있습니다.

Premium Storage 기능은 다음과 같습니다.

* 프리미엄 저장소 디스크: Azure 프리미엄 저장소 연결 된 tooDS, DSv2, 또는 GS 시리즈 Azure Vm 수 있는 VM 디스크를 지원 합니다.
* 프리미엄 페이지 Blob: 프리미엄 저장소는 사용 되는 toohold 영구 디스크 Azure 가상 컴퓨터 (Vm)에 대 한 Azure 페이지 Blob을 지원 합니다.
* 로컬 중복 저장소 프리미엄: 프리미엄 저장소 계정의 로컬 중복 저장소 (LRS) hello replication 옵션으로 및 지원 단일 지역 내 hello 데이터 복사본이 3 개 유지 합니다.
* [Premium Storage](../../storage/common/storage-premium-storage.md)

## <a name="premium-storage-supported-vms"></a>프리미엄 저장소 지원 VM
프리미엄 저장소는 DS 시리즈, DSv2 시리즈, GS 시리즈 및 Fs 시리즈 Azure VM(가상 컴퓨터)을 지원합니다. 프리미엄 저장소 지원 VM에서 표준 및 프리미엄 저장소 디스크를 모두 사용할 수 있습니다. 하지만 Premium Storage와 호환되지 않는 VM 시리즈에서는 Premium Storage 디스크를 사용할 수 없습니다.

프리미엄 저장소에서는 유효성을 검사 하는 hello Linux 배포는 다음과가 같습니다.

| 배포 | 버전 | 지원되는 커널 |
| --- | --- | --- |
| Ubuntu |12.04 |3.2.0-75.110+ |
| Ubuntu |14.04 |3.13.0-44.73+ |
| Debian |7.x, 8.x |3.16.7-ckt4-1+ |
| SLES |SLES 12 |3.12.36-38.1+ |
| SLES |SLES 11 SP4 |3.0.101-0.63.1+ |
| CoreOS |584.0.0+ |3.18.4+ |
| Centos |6.5, 6.6, 6.7, 7.0, 7.1 |3.10.0-229.1.2.el7+ |
| RHEL |6.8+, 7.2+ | |

## <a name="azure-file-storage"></a>Azure 파일 저장소
Azure 파일 저장소 hello 표준 SMB 프로토콜을 사용 하 여 hello 클라우드에서 파일 공유를 제공 합니다. Azure 파일을 통해 파일 서버 tooAzure에 의존 하는 엔터프라이즈 응용 프로그램을 마이그레이션할 수 있습니다. Azure에서 실행 중인 응용 프로그램은 Linux를 실행 중인 Azure 가상 컴퓨터에서 파일 공유를 쉽게 탑재할 수 있습니다. 및 파일 저장소의 최신 릴리스에서 hello 또한 탑재할 수 있습니다 파일 공유에서 SMB 3.0을 지원 하는 온-프레미스 응용 프로그램입니다.  파일 공유는 SMB 공유이므로 표준 파일 시스템 API를 통해 파일 공유에 액세스할 수 있습니다.

파일 저장 되므로 파일 저장소 제공 hello 가용성, 내구성, 확장성 및 지리적 중복 하는 Blob, 테이블 및 큐 저장소로 동일한 기술을 hello Azure 저장소 플랫폼에 기본 제공 되는 hello에 작성 됩니다. File Storage 성능 목표 및 제한에 대한 자세한 내용은 Azure Storage 확장성 및 성능 목표를 참조하세요.

* [어떻게 toouse Linux로 Azure 파일 저장소](../../storage/files/storage-how-to-use-files-linux.md)

## <a name="hot-storage"></a>핫 저장소
자주 액세스 되는 데이터를 저장 하기 위한 hello Azure 핫 저장소 계층 최적화 되어 있습니다.  핫 저장소는 blob 저장소에 대 한 hello 기본 저장소 유형입니다.

## <a name="cool-storage"></a>쿨 저장소
자주 액세스 되며 수명이 긴 데이터를 저장 하기 위한 hello Azure 쿨 저장소 계층 최적화 됩니다. 쿨 저장소에 대한 사용 사례 예제는 백업, 미디어 콘텐츠, 과학적 데이터, 규정 준수 및 보관 데이터를 포함합니다. 일반적으로 자주 액세스하지 않는 모든 데이터는 쿨 저장소에 적합합니다.

|  | 핫 저장소 계층 | 쿨 저장소 계층 |
|:--- |:---:|:---:|
| Availability |99.9% |99% |
| 가용성(RA-GRS 읽기) |99.99% |99.9% |
| 사용 요금 |저장소 비용 더 높음 |저장소 비용 더 낮음 |
| 낮은 액세스 |많은 액세스 | |
| 및 트랜잭션 비용 |및 트랜잭션 비용 | |

## <a name="redundancy"></a>중복
저장소 계정은 항상 Microsoft Azure의 hello 데이터 tooensure 내 구성과 고가용성을 일시적인 하드웨어 오류의 hello 면 에서도 hello Azure 저장소 SLA를 충족를 복제 합니다.

저장소 계정을 만들 때 hello 다음 복제 옵션 중 하나를 선택 해야 합니다.

* LRS(로컬 중복 저장소)
* ZRS(영역 중복 저장소)
* GRS(지역 중복 저장소)
* RA-GRS(읽기 액세스 지역 중복 저장소)

### <a name="locally-redundant-storage"></a>로컬 중복 저장소
로컬 중복 저장소 (LRS) 저장소 계정을 만든 hello 영역 내에 데이터를 복제 합니다. 저장소 계정 데이터에에서 대 한 모든 요청 toomaximize 내구성 3 번 복제 됩니다. 이러한 3개의 복제본은 각기 별도 오류 도메인 및 업그레이드 도메인에 상주합니다.  경과 했는데도 문제가 있다면 서 면된 tooall 세 개의 복제본에 한 번만 요청을 성공적으로 반환 합니다.

### <a name="zone-redundant-storage"></a>영역 중복 저장소
영역 중복 저장소 (ZRS)는 두 개의 toothree 시설에 걸쳐 단일 지역 내 또는 두 영역 간 LRS 보다 높은 지 속성을 제공 하 여 데이터를 복제 합니다. 저장소 계정 사용 ZRS 있으면 데이터가 hello 시설 중 하나에서 작업이 실패의 hello 경우에도 지속 됩니다.

### <a name="geo-redundant-storage"></a>지역 중복 저장소
지역 중복 저장소 (GRS) 수백 마일 떨어진 hello 기본 지역 데이터 tooa 보조 지역에 복제 합니다. GRS를 활성화 한 저장소 계정의 데이터가 전체 지역 가동 중단 또는 재해는 hello에 기본 지역을 복구할 수의 hello 경우에도 지속 됩니다.

### <a name="read-access-geo-redundant-storage"></a>읽기 액세스 지역 중복 저장소
읽기 액세스 지역 중복 저장소 (RA-GRS)는 두 영역 간 toohello 복제 GRS에서 제공 하는 또한 toohello 데이터 hello 보조 위치에 읽기 전용 액세스를 제공 하 여 저장소 계정의 가용성을 최대화 합니다. 데이터 hello 기본 지역에서 사용할 수 없게 되는 hello 이벤트에서 응용 프로그램 hello 보조 지역에서 데이터를 읽을 수 있습니다.

Azure Storage 중복에 대해 자세히 알아보려면 다음을 참조하세요.

* [Azure 저장소 복제](../../storage/common/storage-redundancy.md)

## <a name="scalability"></a>확장성
Azure 저장소 이므로 확장성이 뛰어난, 저장 하 고 수백 테라바이트 과학, 재무 분석 및 미디어 응용 프로그램에 필요한 데이터 toosupport hello 빅 데이터 시나리오를 처리할 수 있습니다. 또는 hello 적은 양의 소규모 기업 웹 사이트에 필요한 데이터를 저장할 수 있습니다. 가 나중에 맞게 때마다 저장 하는 hello 데이터에 대해서만 지불 합니다. Azure Storage는 현재 수십조에 달하는 고유한 고객 개체를 저장하고 초당 평균 수백만 건의 요청을 처리합니다.

Standard Storage 계정: Standard Storage 계정의 최대 총 요청 속도는 20,000IOPS입니다. hello 모든 표준 저장소 계정에 가상 컴퓨터 디스크에서 총 IOP 넘지 않아야이 한도 합니다.

Premium Storage 계정: Premium Storage 계정의 최대 총 처리량 속도는 50Gbps입니다. VM 디스크의 모든 hello 총 처리량이 한이도 넘지 않아야 합니다.

## <a name="availability"></a>Availability
적어도 99.99% (쿨 액세스 계층에 대해 99.9%) hello 시간, 우리 읽기 액세스 지역 중복 저장소 (RA-GRS) 계정에서 요청 tooread 데이터 처리는 성공적으로, 시도 tooread 데이터 hello 기본 지역에서 실패 하는 보장 hello 보조 지역에서 다시 시도 합니다.

해당 99.9% 이상의 (쿨 액세스 계층에 대 한 99%) hello 시간,에서는 더 성공적으로 보장 로컬 중복 저장소 (LRS), 영역 중복 저장소 (ZRS), 및 지역 중복 저장소 (GRS) 계정에서 tooread 데이터를 요청 하는 프로세스입니다.

해당 99.9% 이상의 (쿨 액세스 계층에 대 한 99%) hello 시간,에서는 더 성공적으로 보장 프로세스 요청 toowrite 데이터 tooLocally 중복 저장소 (LRS), 영역 중복 저장소 (ZRS), 및 지역 중복 저장소 (GRS) 계정 및 읽기 액세스 지역 중복 저장소 (RA-GRS) 계정입니다.

* [저장소에 대한 Azure SLA](https://azure.microsoft.com/support/legal/sla/storage/v1_1/)

## <a name="regions"></a>영역
Azure는 hello 세계 30 영역에서 일반적으로 사용할 수 및 4 추가 지역에 대 한 계획을 발표 했습니다. 지리적 확장 우리의 고객 tooachieve 더 높은 성능을 값과 요구 사항과 데이터 위치에 대 한 기본 설정을 지원 하기 때문에 Azure에 대 한 우선 순위는 합니다.  독일 azures 최신 지역 toolaunch가입니다.

Microsoft 클라우드 독일 hello 차별화 된 옵션 toohello 이미 사용할 수 있는 Microsoft 클라우드 서비스에서 제공 유럽, 증가 된 혁신 기회 및 되 파트너에 대 한 경제 성장 및 고객 독일, 만들기 EU (유럽 연합) hello 및 hello 유럽 자유 무역 연결 (EFTA).

Magdeburg 및 프랑크푸르트, 이러한 새 데이터 센터에서 고객 데이터는 데이터 트러스티, T 시스템 국제, 독립적인 독일어 회사 및 독일 통신 국의 자회사 hello 제어 관리 됩니다. 이러한 데이터 센터에서 Microsoft의 상업용 클라우드 서비스 tooGerman 데이터 처리 규정을 준수 하 고 고객의 데이터를 처리 하는 방법 및 위치 추가 선택 항목을 제공 합니다.

* [Azure 지역 맵](https://azure.microsoft.com/regions/)

## <a name="security"></a>보안
Azure 저장소는 다양 한 개발자를 함께 사용 하는 보안 기능 toobuild 보안 응용 프로그램을 제공 합니다. 역할 기반 액세스 제어 및 Azure Active Directory를 사용 하 여 hello 저장소 계정 자체를 보호할 수 있습니다. 클라이언트 쪽 암호화, HTTP 또는 SMB 3.0을 사용하여 응용 프로그램과 Azure 간에 전송 중인 데이터의 보안을 유지할 수 있습니다. 데이터 toobe 자동으로 암호화를 설정할 수 있습니다 때 tooAzure 저장소 서비스 암호화 SSE ()를 사용 하 여 저장소를 기록 합니다. 가상 컴퓨터에서 사용 되는 OS 및 데이터 디스크 toobe Azure 디스크 암호화를 사용 하 여 암호화를 설정할 수 있습니다. 공유 액세스 서명을 사용 하 여 Azure 저장소에 toohello 데이터 개체를 위임 된 액세스를 부여할 수 있습니다.

### <a name="management-plane-security"></a>관리 평면 보안
저장소 계정을 사용 하는 리소스 toomanage hello의 hello 관리 평면 구성 됩니다. 이 섹션에서는 hello Azure 리소스 관리자 배포 모델 및 역할 기반 액세스 제어 (RBAC) toocontrol toouse tooyour 저장소 계정 액세스 하는 방법에 대 한 알아보겠습니다. 저장소 계정 키를 관리 하는 방법에 대 한도 다룹니다 방법과 tooregenerate 해당 합니다.

### <a name="data-plane-security"></a>데이터 평면 보안
이 섹션에서는 살펴보게 저장소 계정의 blob, 파일, 큐 및 테이블을 같은 toohello 실제 데이터 개체 액세스할 수 있도록 공유 액세스 서명 및 저장 된 액세스 정책을 사용 하 여 합니다. 서비스 수준 SAS 및 계정 수준 SAS에 대한 설명이 제공됩니다. 것도 확인할 toolimit 액세스 방법을 tooa 특정 IP 주소 (또는 IP 주소 범위) 하 고 toolimit hello 프로토콜 tooHTTPS를 사용 하는 방법에 대 한 대기 하지 않고 공유 액세스 서명을 a toorevoke tooexpire 합니다.

## <a name="encryption-in-transit"></a>전송 중 암호화
이 섹션에서는 어떻게 toosecure 데이터 또는 Azure 저장소 외부로 전송 하는 경우. Azure 파일 공유에 대 한 SMB 3.0에서 사용 하는 HTTPS 및 hello 암호화 사용을 권장 하는 hello 방법에 대해 알아보겠습니다. 또한 사용할 수 있는 클라이언트 응용 프로그램에서 저장소에 전송 될 때까지 tooencrypt hello 데이터 및 toodecrypt hello 데이터 저장소에서 전송 된 후 클라이언트 쪽 암호화를 살펴보면 메뉴로 이동 합니다.

## <a name="encryption-at-rest"></a>휴지 상태의 암호화
저장소 서비스 암호화 (SSE) 및 저장소 계정에 대해 활성화 페이지 blob는 블록 blob에 tooAzure 저장소를 기록할 때 자동으로 암호화 되 고 blob을 추가 하는 방법에 대 한 설명 하겠습니다. Azure 디스크 암호화를 사용 하 여 hello는 기본적인 차이점 및 클라이언트 쪽 암호화 및 SSE 및 디스크 암호화의 사례를 탐색 하는 방법에 살펴보겠습니다. 미국 정부 컴퓨터의 FIPS 준수에 대해서도 간단히 살펴봅니다.

* [Azure Storage 보안 가이드](../../storage/common/storage-security-guide.md)

## <a name="temporary-disk"></a>임시 디스크
각 VM에는 임시 디스크가 포함되어 있습니다. hello 임시 디스크 응용 프로그램 및 프로세스에 대 한 단기 저장소를 제공 하며 페이지 또는 스왑 파일과 같은 데이터를 의도 한 tooonly 저장 합니다. Hello 임시 디스크에 데이터를 하는 동안 손실 될 수 있습니다는 [유지 관리 이벤트](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) 되거나 있습니다 [VM을 다시 배포](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다. Hello VM의 표준 다시 부팅 하는 동안 hello 데이터 hello 임시 드라이브에 유지 되어야 합니다.

Linux 가상 컴퓨터에서 hello 디스크는 일반적으로 **/개발/sdb** 서식이 지정 되 고 너무 탑재**/mnt** hello Azure Linux 에이전트에서 합니다. hello 임시 디스크의 hello 크기 hello 가상 컴퓨터의 hello 크기에 따라 달라 집니다. 자세한 내용은 [Linux 가상 컴퓨터의 크기](sizes.md)를 참조하세요.

Azure hello 임시 디스크를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [hello 임시 드라이브를 Microsoft Azure 가상 컴퓨터 이해](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="cost-savings"></a>비용 절감
* [저장소 비용](https://azure.microsoft.com/pricing/details/storage/)
* [저장소 비용 계산기](https://azure.microsoft.com/pricing/calculator/?service=storage)

## <a name="storage-limits"></a>저장소 제한
* [저장소 서비스 제한](../../azure-subscription-service-limits.md#storage-limits)
