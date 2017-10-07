---
title: "aaaTroubleshoot Azure 클래식 포털에서 오류 백업 | Microsoft Docs"
description: "Azure 백업 및 복원 hello 클래식 포털에서 Azure 가상 컴퓨터의 문제를 해결 합니다."
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 117201fb-c0cd-4be4-b47f-abd88fe914cf
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/23/2017
ms.author: trinadhk;markgal;
ms.openlocfilehash: b9907f6fa57c631f5446c4d00f946a57c4efd72b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-virtual-machine-backup"></a>Azure 가상 컴퓨터 백업 문제 해결
> [!div class="op_single_selector"]
> * [복구 서비스 자격 증명 모음](backup-azure-vms-troubleshoot.md)
> * [백업 자격 증명 모음](backup-azure-vms-troubleshoot-classic.md)
>
>

Hello 테이블 아래에 나열 된 정보와 함께 Azure 백업을 사용 하는 동안 발생 한 오류를 해결할 수 있습니다.

## <a name="discovery"></a>검색
| 백업 작업 | 오류 세부 정보 | 해결 방법 |
| --- | --- | --- |
| 검색 |Toodiscover 새 항목이-하 고 내부 오류가 발생 하는 Microsoft Azure 백업에 실패 했습니다. 몇 분 정도 기다린 후 hello 작업을 다시 시도 하십시오. |Hello 검색 프로세스가 15 분 후 다시 시도 합니다. |
| 검색 |새 항목 toodiscover – 작업이 이미 진행 중입니다. 다른 검색에 실패 했습니다. Hello 현재 검색 작업이 완료 될 때까지 잠시 기다려 주십시오. |없음 |

## <a name="register"></a>등록
| 백업 작업 | 오류 세부 정보 | 해결 방법 |
| --- | --- | --- |
| 등록 |데이터 디스크 개수 연결 toohello 초과 하는 가상 컴퓨터 지원 hello 제한-이 가상 컴퓨터와 재시도 hello 작업의 일부 데이터 디스크를 분리 하십시오. Azure 백업 지원 too16 데이터 디스크를 연결 tooan 백업에 대 한 Azure 가상 컴퓨터 |없음 |
| 등록 |Microsoft Azure 백업 몇 분 정도 기다렸다가 내부 오류가 발생 한 후 hello 작업을 다시 시도 하십시오. Hello 문제가 지속 되 면 Microsoft 지원에 문의 합니다. |프리미엄 LRS에서 VM의 지원 되지 않는 hello 뒤의 tooone 구성 때문에이 오류를 가져올 수 있습니다. <br> 복구 서비스 자격 증명 모음을 사용하여 프리미엄 저장소 VM을 백업할 수 있습니다. [자세한 정보](backup-introduction-to-azure-backup.md#using-premium-storage-vms-with-azure-backup) |
| 등록 |에이전트 설치 작업 시간 초과로 인해 등록하지 못했습니다. |Hello OS 버전의 hello 가상 컴퓨터를 지원 하는지 확인 합니다. |
| 등록 |명령을 실행하지 못했습니다. 이 항목에 대해 다른 작업이 진행 중입니다. Hello 이전 작업이 완료 될 때까지 기다려 주세요 |없음 |
| 등록 |프리미엄 저장소에 저장된 가상 하드 디스크에 있는 가상 컴퓨터는 백업을 지원하지 않습니다. |없음 |
| 등록 |가상 컴퓨터 에이전트가 hello 가상 컴퓨터에 없으면-hello 필요한 필수 소프트웨어를 VM 에이전트를 설치 하십시오 및 hello 작업을 다시 시작 합니다. |[자세한 내용은](#vm-agent) VM 에이전트를 설치 하 고 어떻게 toovalidate hello VM 에이전트를 설치 하는 방법에 대 한 합니다. |

## <a name="backup"></a>백업
| 백업 작업 | 오류 세부 정보 | 해결 방법 |
| --- | --- | --- |
| 백업 |스냅숏 상태에 대 한 hello VM 에이전트와 통신할 수 없습니다. 스냅숏 VM 하위 작업이 시간 초과 되었습니다. -Hello를 문제 해결 방법을 참조 하십시오 tooresolve이 있습니다. |이 오류는 hello VM 에이전트 문제가 있습니다 또는 네트워크 액세스 toohello Azure 인프라 어떤 방식으로든에서 차단 하는 경우에 throw 됩니다. [VM 스냅숏 문제 디버깅 문제](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md)에 대해 자세히 알아봅니다. <br> Hello VM 에이전트는 모든 문제를 유발 하지 않는지, hello VM에 다시 시작 합니다. 시간에 잘못 된 VM 상태가 문제를 일으킬 수 있습니다 및 hello VM을 다시 시작이 "잘못 된 상태"를 다시 설정 |
| 백업 |내부 오류로 인해 백업이 실패-hello 작업을 잠시 후에 다시 시도 하십시오. Hello 문제가 계속 되 면 Microsoft 지원에 문의 |VM 저장소에 액세스하는 데 일시적인 문제가 있는지 확인합니다. 확인 하십시오 [Azure 상태](https://azure.microsoft.com/en-us/status/) toosee 모든 진행 중인 실행 관련된 toocompute/저장/네트워크 hello 지역에 없는 경우. 하십시오 재시도 hello 백업 post 문제가 완화 됩니다. |
| 백업 |VM이 더 이상 존재 hello 작업을 수행할 수 없습니다. |백업 hello 백업에 대해 구성 된 VM 삭제 되었기 때문에 수행할 수 없습니다. TooProtected 항목 보기 이동 하 여 향후 백업을 중지, 보호 된 항목을 선택 하 고 보호 중지를 클릭 합니다. 백업 데이터 보존 옵션을 선택하여 데이터를 보존할 수 있습니다. 나중에 등록된 항목 보기에서 보호 구성을 클릭하여 이 가상 컴퓨터에 대한 보호를 다시 시작할 수 있습니다. |
| 백업 |실패 한 tooinstall hello hello 선택 항목-VM 에이전트에 Azure 복구 서비스 확장 Azure 복구 서비스 확장에 대 한 필수 조건입니다. Hello Azure VM 에이전트를 설치 하 고 hello 등록 작업을 다시 시작 하십시오 |<ol> <li>Hello VM 에이전트가 올바르게 설치 된 경우를 확인 합니다. <li>해당 hello 확인 플래그 hello VM config 올바르게 설정 되어 있습니다.</ol> [자세한 내용은](#validating-vm-agent-installation) VM 에이전트를 설치 하 고 어떻게 toovalidate hello VM 에이전트를 설치 하는 방법에 대 한 합니다. |
| 백업 |명령을 실행하지 못했습니다. 현재 이 항목에 대해 다른 작업이 진행 중입니다. 하십시오 hello 이전 작업이 완료 될 때까지 기다린 후 다시 시도 |Hello VM에 대 한 기존 백업 또는 복원 작업이 실행 되 고 hello 기존 작업을 실행 하는 동안 새 작업을 시작할 수 없습니다. |
| 백업 |"COM +가 없습니다 tootalk toohello Microsoft Distributed Transaction Coordinator hello 오류와 함께 확장 설치 실패 |Hello COM + 서비스가 실행 되지 않는 것을 의미 합니다. 이 문제 해결에 대한 도움은 Microsoft 지원에 문의하세요. |
| 백업 |스냅숏 작업이 실패 했으며 hello VSS 작업 오류로 "이이 드라이브는 BitLocker 드라이브 암호화로 잠겨 있음. 제어판에서 이 드라이브 잠금을 해제해야 합니다. |Hello VM에 있는 모든 드라이브에 대 한 BitLocker를 해제 하 고 hello VSS 문제가 해결 되는 경우 관찰 |
| 백업 |프리미엄 저장소에 저장된 가상 하드 디스크에 있는 가상 컴퓨터는 백업을 지원하지 않습니다. |없음 |
| 백업 |Azure 가상 컴퓨터를 찾을 수 없습니다. |이 오류는 hello 기본 VM을 삭제 하지만 hello 백업 정책을 계속 VM tooperform 백업용 toolook 때 발생 합니다. toofix이이 오류: <ol><li>Hello로 hello 가상 컴퓨터를 다시 만듭니다. 동일한 이름과 동일한 리소스 그룹 이름은 [클라우드 서비스 이름] <br>또는 <li> 후속 백업이 트리거되지 않도록 이 VM에 대한 보호를 해제합니다. </ol> |
| 백업 |가상 컴퓨터 에이전트가 hello 가상 컴퓨터에 없으면-hello 필요한 필수 소프트웨어를 VM 에이전트를 설치 하십시오 및 hello 작업을 다시 시작 합니다. |[자세한 내용은](#vm-agent) VM 에이전트를 설치 하 고 어떻게 toovalidate hello VM 에이전트를 설치 하는 방법에 대 한 합니다. |

## <a name="jobs"></a>작업
| 작업 | 오류 세부 정보 | 해결 방법 |
| --- | --- | --- |
| 작업 취소 |이 작업 유형에 대 한 취소를 사용할 수 없습니다-hello 작업이 완료 될 때까지 잠시 기다려 주십시오. |없음 |
| 작업 취소 |hello 작업이 취소 가능한 상태가 아니므로-hello 작업이 완료 될 때까지 잠시 기다려 주십시오. <br>또는<br> hello 선택한 작업을 취소할 수 있는 상태가 아니므로-hello 작업 toocomplete 잠시 기다려 주십시오. |모든 가능성에 hello 작업이 거의 완료 되었습니다. hello 작업이 완료 될 때까지 기다리십시오. |
| 작업 취소 |진행 중에-취소는 진행 중인 작업에만 지원 하므로 hello 작업을 취소할 수 없습니다. 진행 중인 작업에 대해 취소를 시도하세요. |이 tooa 일시적 상태로 인해 발생합니다. 잠시 기다렸다가 hello 취소 작업을 다시 시도 하십시오. |
| 작업 취소 |실패 한 toocancel hello 작업-작업 완료 될 때까지 기다리십시오. |없음 |

## <a name="restore"></a>복원
| 작업 | 오류 세부 정보 | 해결 방법 |
| --- | --- | --- |
| 복원 |클라우드 내부 오류로 인해 복원 실패 |<ol><li>클라우드 서비스 toowhich toorestore를 시도 하는 DNS 설정으로 구성 됩니다. 다음을 확인하면 알 수 있습니다. <br>$deployment = Get-AzureDeployment -ServiceName "ServiceName" -Slot "Production"     Get-AzureDns -DnsSettings $deployment.DnsSettings<br>구성된 주소가 있으면 DNS 설정이 구성되었다는 의미입니다.<br> <li>클라우드 서비스 toowhich tooyou 려 toorestore 예약 된 Ip로 구성 되어 있으며 기존 Vm 클라우드 서비스에서 중지 된 상태에서.<br>다음 powershell cmdlet을 사용하여 클라우드 서비스에 예약된 IP가 있는지 확인할 수 있습니다.<br>$deployment = Get-AzureDeployment -ServiceName "servicename" -Slot "Production" $dep.ReservedIPName <br><li>Toorestore toosame 클라우드 서비스에서 다음 특수 한 네트워크 구성 사용 하 여 가상 컴퓨터를 하려고 합니다. <br>- 부하 분산 장치 구성의 가상 컴퓨터(내부 및 외부)<br>- 여러 개의 예약된 IP를 사용하는 가상 컴퓨터<br>- 여러 NIC가 있는 가상 컴퓨터<br>Hello UI에서에서 새 클라우드 서비스를 선택 하십시오 또는 너무를 참조 하십시오[복원 고려 사항](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations) 특수 한 네트워크 구성 된 Vm에 대 한</ol> |
| 복원 |hello 선택한 DNS 이름이 이미 사용 중-하십시오 다른 DNS 이름을 지정 하 고 다시 시도 하십시오. |hello DNS 이름이 여기 참조 toohello 클라우드 서비스 이름 (일반적으로 끝나는. cloudapp.net에). 이 테스트 해야 toobe 고유 합니다. 이 오류가 발생 하면 복원 중 다른 VM 이름을 toochoose 필요. <br><br> 이 오류는 hello Azure 포털의 toousers만 표시 됩니다. hello PowerShell 통해 복원 작업 때문에 성공은 hello 디스크를 복원 하 고 VM hello를 만들지는 않습니다. hello 오류 hello 디스크 복원 작업 후 사용자가 VM hello를 명시적으로 만들 때 직면 하 게 될 됩니다. |
| 복원 |hello 지정 된 가상 네트워크 구성이 잘못 되었습니다-उ प क 다른 가상 네트워크 구성 하 고 다시 시도 하십시오. |없음 |
| 복원 |hello는 클라우드 서비스가 사용 하지 않는 hello hello 가상 컴퓨터 구성의 복원 되 고 일치-예약 된 IP를 사용 하지 않는 다른 클라우드 서비스를 지정 하거나 선택 하십시오에서 다른 복구 지점 toorestore는 예약된 된 IP를 지정 합니다. |없음 |
| 복원 |클라우드 서비스에는 다른 클라우드 서비스를 지정 하 여 또는 기존 끝점을 사용 하 여 다시 시도 hello 작업 입력된 끝점-의 수 제한에 도달 했습니다. |없음 |
| 복원 |백업 자격 증명 모음과 대상 저장소 계정이 서로 다른 두 지역에-hello 중인 복원 작업에 지정 된 hello 저장소 계정을 확인 hello 백업 자격 증명 모음과 동일한 Azure 지역입니다. |없음 |
| 복원 |지원 되는 hello 복원 작업이 않습니다으로 지정한 저장소 계정-만 기본/표준 저장소 계정을 로컬 중복 또는 지역 중복 복제 설정이 지원 됩니다. 지원되는 저장소 계정을 선택하세요. |없음 |
| 복원 |복원 작업에 대해 지정 된 저장소 계정의 유형이 온라인있지 않습니다.-복원 작업에 지정 된 hello 저장소 계정이 온라인 상태 인지 확인 |이 Azure 저장소에 또는 tooan 중단 인해 일시적인 오류로 인해 발생할 수 있습니다. 다른 저장소 계정을 선택하세요. |
| 복원 |리소스 그룹 할당량에 도달 했으므로-Azure 포털 또는 Azure 고객 지원으로 문의 tooincrease hello 제한에서 일부 리소스 그룹을 삭제 하십시오. |없음 |
| 복원 |선택한 서브넷이 존재하지 않습니다. 존재하는 서브넷을 선택하세요. |없음 |

## <a name="policy"></a>정책
| 작업 | 오류 세부 정보 | 해결 방법 |
| --- | --- | --- |
| 정책 만들기 |실패 한 toocreate hello 정책-정책 구성에 hello 보존 선택 항목 toocontinue를 줄이십시오. |없음 |

## <a name="vm-agent"></a>VM 에이전트
### <a name="setting-up-hello-vm-agent"></a>VM 에이전트 hello 설정
일반적으로 hello VM 에이전트는 hello Azure 갤러리에서에서 생성 된 Vm에 이미 있습니다. 그러나 온-프레미스 데이터 센터에서 마이그레이션된 가상 컴퓨터 hello VM 에이전트가 설치 되어 있어야 합니다. 이러한 Vm에 대 한 hello VM 에이전트 toobe 명시적으로 설치 해야 합니다. 에 대해 자세히 알아보세요 [hello VM에 에이전트를 설치 하는 기존 VM](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx)합니다.

Windows VM의 경우

* 다운로드 및 설치 hello [에이전트 MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)합니다. 관리자 권한 toocomplete hello 설치를 해야 합니다.
* [Hello VM 속성을 업데이트](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) 에이전트 hello tooindicate가 설치 되어 있습니다.

Linux VM의 경우

* github에서 최신 [Linux 에이전트](https://github.com/Azure/WALinuxAgent) 를 설치합니다.
* [Hello VM 속성을 업데이트](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) 에이전트 hello tooindicate가 설치 되어 있습니다.

### <a name="updating-hello-vm-agent"></a>Hello VM 에이전트를 업데이트합니다.
Windows VM의 경우

* 업데이트 hello VM 에이전트를 다시 설치 하는 hello [VM 에이전트 이진 파일](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)합니다. 그러나 hello VM 에이전트를 업데이트 하는 동안 실행 중인 백업 작업이 수행 되지 tooensure를 해야 합니다.

Linux VM의 경우

* Hello 지침에 따라 [Linux VM 에이전트 업데이트](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

### <a name="validating-vm-agent-installation"></a>VM 에이전트 설치의 유효성 검사
방법에 대 한 toocheck hello Windows Vm에서 VM 에이전트 버전:

1. Toohello Azure 가상 컴퓨터에 로그인 하 고 toohello 폴더 탐색 *C:\WindowsAzure\Packages*합니다. Hello WaAppAgent.exe 파일이 없는 찾아야 합니다.
2. Hello 파일을 마우스 오른쪽 단추로 클릭 한 다음 너무 이동 하십시오**속성**를 클릭 한 hello **세부 정보** 탭 hello 제품 버전 필드 2.6.1198.718 이루어져야 이상
