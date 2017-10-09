---
title: "파일 수준에서 Azure 백업의 HANA aaaSAP | Microsoft Docs"
description: "Azure 가상 컴퓨터에는 SAP HANA에 대한 두 가지 주요 백업 방법이 있습니다. 이 문서에서는 파일 수준의 SAP HANA Azure 백업에 대해 설명합니다"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ums.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 3/13/2017
ms.author: rclaus
ms.openlocfilehash: d5a55de5634ac7724e7fd0fa3760c6c408c3db74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-azure-backup-on-file-level"></a>파일 수준의 SAP HANA Azure 백업

## <a name="introduction"></a>소개

이 문서는 3부로 구성된 SAP HANA 백업 관련 문서 시리즈의 일부입니다. [Azure 가상 컴퓨터에서 SAP HANA에 대 한 백업 가이드](./sap-hana-backup-guide.md) 시작, 대 한 개요 및 정보를 제공 하 고 [SAP HANA 백업 스냅숏을 기반으로 저장소](./sap-hana-backup-storage-snapshots.md) 표지 hello 저장소 스냅숏 기반 백업 옵션입니다.

Hello Azure VM 크기 보고, 하나는 GS5 64 개의 연결 된 데이터 디스크를 허용 하는지 확인할 수 있습니다. 대용량 SAP HANA 시스템의 경우 데이터와 로그 파일을 유지하는 데 많은 수의 디스크를 이미 사용하고 있으므로 소프트웨어 RAID와 결합하여 디스크 IO 처리량을 최적화할 수도 있습니다. hello 문제 다음 toostore SAP HANA 가득 hello 연결 된 데이터 디스크 시간이 지남에 따라 있는 파일을 백업 하는 위치는입니다. 참조 [Azure에서 Linux 가상 컴퓨터에 대 한 크기](../../linux/sizes.md) hello Azure VM 크기 테이블에 대 한 합니다.

현재 Azure Backup 서비스에서 사용할 수 있는 SAP HANA 백업 통합은 없습니다. SAP HANA Studio 또는 SAP HANA SQL 문을 통해 파일 기반 백업으로 hello 파일 수준에서 백업/복원 toomanage는 hello 표준 방법입니다. 자세한 내용은 [SAP HANA SQL 및 시스템 보기 참조](https://help.sap.com/hana/SAP_HANA_SQL_and_System_Views_Reference_en.pdf)(영문)를 참조하세요.

![이 그림에서는 SAP HANA Studio에서 hello 백업 메뉴 항목의 hello 대화 상자를 보여 줍니다.](media/sap-hana-backup-file-level/image022.png)

이 그림에서 SAP HANA Studio hello 백업 메뉴 항목의 hello 대화 상자를 보여 줍니다. 형식을 선택할 때 &quot;파일인&quot; 하나에 toospecify 경로 hello 파일 시스템 SAP HANA hello 백업 파일을 기록 하는 위치에 있습니다. 복원 하는 hello 동일한 방식으로 합니다.

간단하고 직관적인 선택으로 보이지만 몇 가지 고려 사항이 있습니다. 앞에서 설명한 대로 Azure VM에 연결할 수 있는 데이터 디스크의 수는 제한됩니다. 용량 toostore SAP HANA의 hello 데이터베이스 및 디스크 처리량 요구 사항, 소프트웨어를 수행할 수도 있습니다의 hello 크기에 따라 VM hello hello 파일 시스템에 백업 파일 수 없는 경우 여러 데이터 디스크 스트라이프를 사용 하 여 RAID 합니다. 테라바이트 단위의 데이터를 처리할 때 이러한 백업 파일을 이동하고 파일 크기 제한과 성능을 관리하기 위한 다양한 옵션이 이 문서의 뒷부분에 나와 있습니다.

전체 용량과 관련하여 더 많은 유연성을 제공하는 또 다른 옵션은 Azure Blob 저장소입니다. 단일 blob 제한 too1 TB도 이지만, 현재 500TB hello 단일 blob 컨테이너의 총 용량이입니다. 또한 제공 고객 hello choice tooselect 소위 &quot;쿨&quot; blob 저장소 비용 이점이 있습니다. 멋진 Blob 저장소에 대한 자세한 내용은 [Azure Blob Storage: 핫 및 쿨 저장소 계층](../../../storage/blobs/storage-blob-storage-tiers.md)을 참조하세요.

추가 보안을 위해 지리적 복제 된 저장소 계정 toostore hello SAP HANA 백업을 사용 합니다. 저장소 계정 복제에 대한 자세한 내용은 [Azure Storage 복제](../../../storage/common/storage-redundancy.md)를 참조하세요.

지리적 복제된 전용 백업 저장소 계정에 SAP HANA 백업 전용 VHD를 배치할 수 있습니다. 그렇지 않으면 tooa 지리적 복제 된 저장소 계정 hello SAP HANA 백업을 유지 하는 hello Vhd 또는 다른 지역에 있는 tooa 저장소 계정을 복사 하나.

## <a name="azure-backup-agent"></a>Azure Backup 에이전트

Azure 백업 제안의 hello 옵션 toonot toobe hello 게스트 OS에 설치 되어 있는 hello 백업 에이전트를 통해 전체 Vm 하지만 또한 파일 및 디렉터리를만 백업 합니다. 하지만 2016 년 12 월을 기준으로이 에이전트는 Windows에서 지원만 (참조 [hello 리소스 관리자 배포 모델을 사용 하 여 Windows 서버 또는 클라이언트 tooAzure 백업](../../../backup/backup-configure-vault.md)).

해결 방법 toofirst 복사본이 예를 들어 (SAMBA 공유)를 통해 SAP HANA 백업 파일 tooa Azure에서 Windows VM 하 고 여기에서 hello Azure 백업 에이전트를 사용 합니다. 기술적으로 가능 하지만 것를 복잡성이 증가할 및 hello 백업 속도가 저하 하거나 복원 프로세스 hello Linux와 Windows VM hello 간의 toohello 복사 인해 크게 줄었습니다. 없으면 toofollow이이 방법을 권장 합니다.

## <a name="azure-blobxfer-utility-details"></a>Azure blobxfer 유틸리티 정보

CLI 또는 PowerShell을 사용할 수 toostore 디렉터리와 Azure 저장소에 파일 hello 중 하나를 사용 하 여 도구를 개발 하거나 [Azure Sdk](https://azure.microsoft.com/downloads/)합니다. 데이터 tooAzure 저장소를 복사 하는 데 즉시 사용할 유틸리티, AzCopy를도 이지만 Windows만 되 고 (참조 [hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송](../../../storage/common/storage-use-azcopy.md)).

따라서 blobxfer 유틸리티가 SAP HANA 백업 파일을 복사하는 데 사용되었습니다. 이 유틸리티는 프로덕션 환경에서 많은 고객이 사용하는 오픈 소스이며 [GitHub](https://github.com/Azure/blobxfer)에서 사용할 수 있습니다. 이 도구는 tooeither Azure blob 저장소 또는 Azure 파일 공유 직접 하나의 toocopy 데이터를 사용 합니다. 또한 여러 파일이 있는 디렉터리를 복사하는 경우 md5 해시 또는 자동 병렬 처리와 같은 유용한 기능을 다양하게 제공합니다.

## <a name="sap-hana-backup-performance"></a>SAP HANA 백업 성능

![SAP HANA Studio hello SAP HANA 백업 콘솔의는이 스크린 샷](media/sap-hana-backup-file-level/image023.png)

이 스크린 샷 hello SAP HANA Studio에서 SAP HANA 백업 콘솔입니다. 약 42 분 toodo hello 백업 걸리는 toohello HANA VM을 연결 된 단일 Azure 표준 저장소 디스크에는 230 g B의 hello XFS 파일 시스템을 사용 합니다.

![이 스크린 샷 YaST hello SAP HANA 테스트 VM에는](media/sap-hana-backup-file-level/image024.png)

이 스크린 샷 hello SAP HANA 테스트 VM에 YaST입니다. 앞에서 설명한 것 처럼 SAP HANA 백업에 대 한 hello 1TB 단일 디스크를 볼 수 하나. 약 42 분 toobackup 걸리는 230 GB입니다. 또한 5개의 200GB 디스크가 연결되었고, 소프트웨어 RAID md0이 만들어졌으며, 이러한 5개의 Azure 데이터 디스크에 스트라이핑이 사용되었습니다.

![연결 된 표준 저장소를 Azure 데이터 디스크를 동일한 백업 소프트웨어 RAID에 스트라이프가 있는 5 간에 hello 반복](media/sap-hana-backup-file-level/image025.png)

반복 hello 동일한 소프트웨어 RAID에 사용 하 여 백업을 스트라이프 5에서 too10 분 아래로 42 분에서 표준 저장소를 Azure 데이터 디스크 상태가 hello 백업 시간을 연결 합니다. hello 디스크가 toohello VM을 캐시 하지 않고도 연결 된입니다. 따라서 것이 얼마나 중요 한지 디스크 쓰기 처리량이 확실 한 hello 백업 시간입니다. 하나에 다음 스위치 tooAzure 프리미엄 저장소 toofurther 최적의 성능을 위해 hello 프로세스를 가속화할 수 있습니다. 일반적으로 프로덕션 시스템에는 Azure 프리미엄 저장소를 사용해야 합니다.

## <a name="copy-sap-hana-backup-files-tooazure-blob-storage"></a>SAP HANA 백업 파일 tooAzure blob 저장소를 복사 합니다.

2016 년 12 월의 hello 가장 처럼 옵션 tooquickly SAP HANA 백업 파일을 저장 Azure blob 저장소입니다. 단일 blob 컨테이너 하나에 500tb를 Azure에 충분 한 SAP HANA 백업 tookeep GS5 VM에서 실행 중인 대부분의 SAP HANA 시스템에 충분 한 제한이 있습니다. 고객의 여지가 hello 간의 &quot;핫&quot; 및 &quot;콜드&quot; blob 저장소 (참조 [Azure Blob 저장소: 핫 및 저장소 계층 냉각용](../../../storage/blobs/storage-blob-storage-tiers.md)).

Hello blobxfer 도구 tooAzure blob 저장소에 직접 쉽게 toocopy hello SAP HANA에 대 한 백업 파일은 있습니다.

![여기서는 전체 SAP HANA 파일 백업의 hello 파일을 볼 수 하나](media/sap-hana-backup-file-level/image026.png)

여기서는 전체 SAP HANA 파일 백업의 hello 파일을 볼 수 하나. 4 개의 파일 및 hello 가장 큰 옵션에 230 GB 약 합니다.

![3000 초 대략 toocopy hello 230 GB tooan 표준 Azure 저장소 계정 blob 컨테이너를 걸리는](media/sap-hana-backup-file-level/image027.png)

Hello 초기 테스트의 md5 해시를 사용 하지, 걸린 3000 초 대략 toocopy hello 230 GB tooan 표준 Azure 저장소 계정 blob 컨테이너입니다.

![이 스크린 샷에 하나 수 모양을 확인할 hello Azure 포털에서](media/sap-hana-backup-file-level/image028.png)

이 스크린 샷에 hello Azure 포털에 나타나는 하나이 보입니다. 라는 blob 컨테이너 &quot;sap-hana-백업을&quot; 만들어졌으며 hello SAP HANA 백업 파일을 나타내는 4 hello blob을 포함 합니다. 그 중 하나는 약 230GB 크기입니다.

hello HANA Studio 백업 콘솔 HANA 백업 파일의 한 toorestrict hello 최대 파일 크기를 허용 합니다. Hello 샘플 환경에서 하나의 큰 230 GB 파일 대신 작은 여러 백업 파일을 가능한 toohave 함으로써 성능이 향상 됩니다.

![Hello HANA 쪽 대상이 &#39; hello 백업 파일 크기 제한을 설정 t hello 백업 시간 개선](media/sap-hana-backup-file-level/image029.png)

Hello HANA 쪽 대상이 &#39; hello 백업 파일 크기 제한을 설정 hello 파일은 다음이 그림에 표시 된 대로 순차적으로 기록 되기 때문에 t hello 백업 시간을 단축 합니다. hello 파일 크기 제한 때문에 hello 백업 hello 230 GB 대신 4 개의 큰 데이터 파일을 단일 파일 생성 too60 GB 설정 되었습니다.

![hello blobxfer 도구의 tootest 병렬 처리 수준, HANA 백업에 대 한 최대 파일 크기 hello 다음 설정한 too15 GB](media/sap-hana-backup-file-level/image030.png)

hello blobxfer 도구의 tootest 병렬 처리 수준, HANA 백업에 대 한 최대 파일 크기 hello too15 GB 19 백업 파일은 다음 설정 되었습니다. 이 구성은 too875 초 아래로 3000 초에서 blobxfer toocopy hello 230 GB tooAzure blob 저장소에 대 한 hello 시간으로 전환 합니다.

이 결과 Azure blob를 작성 하기 위한 60MB/sec의 toohello 제한 때문입니다. 여러 blob 통해 병렬 처리 수준 hello 병목 상태가 해결 되지만 한 가지 단점이 있습니다: 많이 있는 새로운 hello blobxfer 도구 toocopy의 이러한 모든 HANA 백업 파일 tooAzure blob 저장소에서는 부하를 HANA VM hello와 hello 네트워크입니다. HANA 시스템의 작업에 영향을 미칩니다.

## <a name="blob-copy-of-dedicated-azure-data-disks-in-backup-software-raid"></a>백업 소프트웨어 RAID에서 전용 Azure 데이터 디스크의 Blob 복사

Hello 수동 VM 데이터 디스크 백업 달리 하나이 접근 방식에서 VM toosave hello 전체 SAP 설치에서 HANA 데이터를 비롯 한 모든 hello 데이터 디스크를 백업 HANA 로깅하지 않습니다 파일 및 config 파일. 대신, hello 개념은 전용 toohave 소프트웨어 RAID 스트라이프가 있는 여러 Azure 데이터 Vhd에 걸쳐 전체 SAP HANA 파일 백업을 저장 하기 위한입니다. 하나에 이러한 디스크를 hello SAP HANA 백업을 복사 합니다. 전용 tooa 연결 또는 전용된 HANA 백업 저장소 계정에 유지할 수 쉽게은 &quot;VM 관리 백업&quot; 추가 처리를 위해 합니다.

![관련 된 모든 Vhd hello를 사용 하 여 복사 된 * * 시작-azurestorageblobcopy * * PowerShell 명령](media/sap-hana-backup-file-level/image031.png)

관련 된 모든 Vhd hello를 사용 하 여 복사 된 hello 백업 toohello 로컬 소프트웨어 RAID 완료 된 후 **시작 azurestorageblobcopy** PowerShell 명령 (참조 [시작 AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy)). Hello 백업 파일을 유지 하는 데 전용 hello 파일 시스템에만 영향을 미칩니다를 hello 디스크에 SAP HANA 데이터 또는 로그 파일 일관성에 대 한 문제 없이 있습니다. 이 명령의 이점은 hello VM 온라인 유지 되는 동안 작동 한다는 점입니다. 특정 프로세스가 toohello 백업 스트라이프 세트를 씁니다 toobe 수 있는지 toounmount hello 하기 전에 blob 복사 하 고 나중에 다시 탑재 합니다. 사용할 수 있는 적절 한 너무 또는&quot;고정&quot; hello 파일 시스템입니다. 예를 들어 xfs 통해\_hello XFS 파일 시스템에 대 한 고정 합니다.

![이 스크린샷은 hello Azure 포털에 hello vhd 컨테이너의 blob 목록을 hello를 보여 줍니다.](media/sap-hana-backup-file-level/image032.png)

이 스크린샷은 hello의 hello blob 목록을 보여 줍니다. &quot;vhd&quot; hello Azure 포털에 대 한 컨테이너입니다. hello 스크린샷은 hello 5 개의 Vhd hello 소프트웨어 RAID tookeep SAP HANA 백업 파일 toohello SAP HANA 서버 VM tooserve를 연결 된입니다. Hello hello blob 복사 명령을 통해 수행 된 복사본이 5 또한 보여줍니다.

![테스트를 위해 hello SAP HANA 백업 소프트웨어 RAID 디스크의 hello 복사본 된 연결 된 toohello 응용 프로그램 서버 VM](media/sap-hana-backup-file-level/image033.png)

테스트를 위해 hello SAP HANA 백업 소프트웨어 RAID 디스크의 hello 복사본에 연결 된 toohello 응용 프로그램 서버 VM 했습니다.

![tooattach hello 디스크 복사본 hello 응용 프로그램 서버 VM 종료](media/sap-hana-backup-file-level/image034.png)

hello 응용 프로그램 서버 VM tooattach hello 디스크 복사본 종료 되었습니다. VM hello를 시작한 후 hello 개이며, 그 hello RAID 제대로 검색 되었습니다 (UUID을 통해 탑재). 탑재 지점에만 hello hello YaST 파티 셔 너를 통해 만들어진, 누락 되었습니다. 나중에 SAP HANA 백업 파일 복사본을 hello 있게 OS 수준에 표시 되었습니다.

## <a name="copy-sap-hana-backup-files-toonfs-share"></a>SAP HANA tooNFS 공유는 백업 파일을 복사

hello SAP HANA NFS 공유에 백업 파일을 저장 하는 방법을 고려할 수 toolessen hello에 영향을 줄 hello 성능 또는 디스크 공간 관점에서 SAP HANA 시스템을 하나. 작동 기술적으로 하지만 두 번째 Azure VM을 사용 하 여 NFS 공유 hello의 hello 호스트로 것을 의미 합니다. VM 네트워크 대역폭을 toohello 인해 작은 VM 크기, 되지 않아야 합니다. 의미 다음이 다운 tooshut 하기가 &quot;VM 백업&quot; 만 hello SAP HANA 백업 실행에 대해 상태로 전환 합니다. 공유 하면 hello 네트워크에 부하를 추가 및 영향 hello SAP HANA 시스템 하지만 hello에 나중에 백업 파일을 hello 단순히 관리 NFS 대 &quot;VM 백업&quot; 것에 영향을 주지 hello SAP HANA 시스템 전혀 합니다.

![Azure VM에서 NFS 공유 된 탑재 된 toohello SAP HANA 서버 VM](media/sap-hana-backup-file-level/image035.png)

tooverify hello NFS 대/소문자를 사용 하 여, Azure VM에서 NFS 공유에 탑재 된 toohello SAP HANA 서버 VM 인지 합니다. 특별한 NFS 튜닝을 적용하지 않았습니다.

![직접 toodo hello 백업 1 시간 46 분 소요](media/sap-hana-backup-file-level/image036.png)

hello NFS 공유 hello SAP HANA 서버에 하나 hello와 같은 빠른 스트라이프 세트를 했습니다. 그럼에도 불구 하 고 걸린 1 시간 및 46 분 toodo hello 10 분이 아닌 hello NFS 공유에 직접 백업 tooa 로컬 스트라이프 세트를 작성할 때입니다.

![hello 대안 1 시간 43 분에서 속도가 훨씬 빨라집니다 되지 않았습니다.](media/sap-hana-backup-file-level/image037.png)

운영 체제 수준에서 백업 tooa 로컬 스트라이프 세트를 수행 하 고 toohello 복사 hello 다른 방법도 NFS 공유 (단순 **cp avr** 명령) 속도가 훨씬 빨라집니다 되지 않았습니다. 1시간 43분이 걸렸습니다.

따라서 작동 되지만 성능 hello 230 GB 백업 테스트에 대 한 좋은 되지 않았습니다. 다중 테라바이트 크기로 작업할 경우에는 더욱 나쁠 것입니다.

## <a name="copy-sap-hana-backup-files-tooazure-file-service"></a>SAP HANA 백업 파일 tooAzure 파일 서비스를 복사 합니다.

Azure 파일을 Azure Linux VM 내부 공유 가능 toomount 이며 hello 문서 [어떻게 toouse Azure 파일 저장소와 Linux](../../../storage/files/storage-how-to-use-files-linux.md) 방법에 자세히 설명 toodo 것입니다. 현재 Azure 파일 공유당 5TB의 할당량 제한이 있으며, 파일당 파일 크기 제한은 1TB입니다. 저장소 제한에 대한 내용은 [Azure Storage 확장성 및 성능 목표](../../../storage/common/storage-scalability-targets.md)를 참조하세요.

그러나 테스트한 결과 SAP HANA 백업이 현재 이러한 종류의 CIFS 탑재와 직접 작동하지 않습니다. 또한 [SAP Note 1820529](https://launchpad.support.sap.com/#/notes/1820529)에서도 CIFS를 권장하지 않는다고 명시하고 있습니다.

![이 그림에서 SAP HANA Studio hello 백업 대화 상자에서 오류를 보여 줍니다.](media/sap-hana-backup-file-level/image038.png)

이 그림 tooback 직접 tooa CIFS 탑재 Azure 파일 공유를 시도할 때 hello 백업 대화 상자에서 SAP HANA Studio에서 오류를 보여 줍니다. 하나에 toodo VM 파일 시스템에는 표준 SAP HANA 백업이 첫째, 고 없어 tooAzure에서 복사 hello 백업 파일을 다음 파일 서비스입니다.

![이 그림은 929 초 toocopy 19 SAP HANA 백업 파일에 대 한 걸리는 보여 줍니다.](media/sap-hana-backup-file-level/image039.png)

이 그림 걸린다는 929 초 toocopy에 대 한 대략 230 GB toohello Azure 파일 공유의 총 크기가 19 SAP HANA 백업 파일입니다.

![SAP HANA VM hello에서 hello 소스 디렉터리 구조를 복사한 toohello Azure 파일 공유](media/sap-hana-backup-file-level/image040.png)

이 스크린 샷에 하나 볼 수는 hello SAP HANA VM에서 hello 소스 디렉터리 구조가 복사한 toohello Azure 파일 공유: 디렉터리 (hana\_백업\_fsl\_15gb) 및 19 개별 백업 파일입니다.

SAP HANA Azure 파일에 백업 파일을 저장 SAP HANA 파일 백업을 지 원하는 경우 직접 hello 향후에 흥미로운 옵션 수 있습니다. 또는 가능 하 게 될 때 toomount NFS를 통해 파일을 Azure hello 최대 할당량 한도 5TB 보다 훨씬 높습니다.

## <a name="next-steps"></a>다음 단계
* [Azure Virtual Machines의 SAP HANA 백업 가이드](sap-hana-backup-guide.md) - 시작에 대한 개요 및 정보를 제공합니다.
* [SAP HANA 백업 스냅숏을 기반으로 저장소](sap-hana-backup-storage-snapshots.md) hello 저장소 스냅숏 기반 백업 옵션에 설명 합니다.
* tooestablish 고가용성 및 (대형 인스턴스) Azure에서 SAP HANA의 재해 복구 계획의 참조 toolearn [SAP HANA (대형 인스턴스) 고가용성 및 재해 복구 Azure에서](hana-overview-high-availability-disaster-recovery.md)합니다.
