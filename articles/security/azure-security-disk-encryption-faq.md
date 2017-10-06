---
title: "aaaAzure 디스크 암호화 FAQ | Microsoft Docs"
description: "이 문서에서는 답변 toofrequently Windows 용 Microsoft Azure 디스크 암호화와 Linux IaaS Vm에 대 한 질문과 대답입니다."
services: security
documentationcenter: na
author: deventiwari
manager: avibm
editor: yuridio
ms.assetid: 7188da52-5540-421d-bf45-d124dee74979
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: devtiw
ms.openlocfilehash: 17f084628ba4ef22e9d37dd3052ef10f8eb2cd7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-frequently-asked-questions-faq"></a>Azure Disk Encryption FAQ(질문과 대답)

이 FAQ는 Windows 및 Linux IaaS VM용 Azure Disk Encryption에 대한 질문에 답변합니다. 이 서비스에 대한 자세한 내용은 [Windows 및 Linux IaaS VM용 Azure Disk Encryption](https://docs.microsoft.com/azure/security/azure-security-disk-encryption)을 참조하세요.

## <a name="general-questions"></a>일반적인 질문
**Q.** Azure Disk Encryption은 어느 지역의 GA에서 사용할 수 있나요?

**A:** Windows 및 Linux IaaS VM용 Azure Disk Encryption은 모든 Azure 공용 지역의 GA에서 사용할 수 있습니다.

**Q:** Azure Disk Encryption에서 사용할 수 있는 사용자 환경은 무엇인가요?

**A:** Azure Disk Encryption GA에서는 Azure Resource Manager 템플릿, Azure PowerShell, Azure CLI를 지원합니다. 이렇게 하면 IaaS VM에 대한 디스크 암호화를 사용하기 위한 세 가지 옵션이 있다는 점에서 많은 유연성을 제공합니다. Hello 사용자 환경 및 단계별 지침에 대 한 자세한 내용은 hello Azure 디스크 암호화 배포 시나리오 및 환경 제공 됩니다.

**Q:** Azure Disk Encryption 비용은 얼마인가요?

**A:** Azure Disk Encryption을 사용하여 VM 디스크를 암호화하는 데 요금이 부과되지 않습니다.

**Q:** Azure Disk Encryption을 사용할 수 있는 가상 컴퓨터 계층은 무엇인가요?

**A:** Azure Disk Encryption은 프리미엄 저장소가 있는 VM을 포함하여 [A, D, DS, G, GS, F](https://azure.microsoft.com/pricing/details/virtual-machines/) 등의 IaaS VM 시리즈를 포함한 표준 계층 VM에서만 사용할 수 있습니다. 기본 계층 VM에서는 사용할 수 없습니다.

**Q:** Azure Disk Encryption은 어떤 Linux 배포판을 지원하나요?

**A:** Azure 디스크 암호화는 hello 서버는 Linux 배포판 및 버전에서 지원 합니다.

| Linux 배포 | 버전 | 암호화에 지원되는 볼륨 유형|
| --- | --- |--- |
| Ubuntu | 16.04-DAILY-LTS | OS 및 데이터 디스크 |
| Ubuntu | 14.04.5-DAILY-LTS | OS 및 데이터 디스크 |
| RHEL | 7.3 | OS 및 데이터 디스크 |
| RHEL | 7.2 | OS 및 데이터 디스크 |
| RHEL | 6.8 | OS 및 데이터 디스크 |
| RHEL | 6.7 | 데이터 디스크  |
| CentOS | 7.3 | OS 및 데이터 디스크 |
| CentOS | 7.2n | OS 및 데이터 디스크 |
| CentOS | 6.8 | OS 및 데이터 디스크 |
| CentOS | 7.1 | 데이터 디스크  |
| CentOS | 7.0 | 데이터 디스크  |
| CentOS | 6.7 | 데이터 디스크  |
| CentOS | 6.6 | 데이터 디스크  |
| CentOS | 6.5 | 데이터 디스크  |
| openSUSE | 13.2 | 데이터 디스크  |
| SLES | 12 SP1 | 데이터 디스크  |
| SLES | 우선 순위: 12-SP1 | 데이터 디스크  |
| SLES | HPC 12 | 데이터 디스크  |
| SLES | 우선 순위: 11-SP4 | 데이터 디스크  |
| SLES | 11 SP4 | 데이터 디스크  |

**Q:** Azure Disk Encryption을 사용하기 시작하려면 어떻게 해야 하나요?

**A:** 어떻게 tooget에 의해 시작 읽기 hello Azure 디스크 암호화 백서 있는 고객에 배울 수 [여기](https://docs.microsoft.com/azure/security/azure-security-disk-encryption)

**Q:** Azure Disk Encryption을 사용하여 부팅 볼륨과 데이터 볼륨을 모두 암호화할 수 있나요?

**A:** 예, Windows 및 Linux IaaS VM용 부팅 볼륨과 데이터 볼륨을 암호화할 수 있습니다. Windows Vm에 대 한 첫 번째 encrpting hello OS 볼륨 없이 hello 데이터를 암호화할 수 없습니다. Linux vm의 경우 먼저 encryptinng hello OS 볼륨 없이 hello 데이터 볼륨을 암호화할 수 있습니다. Hello OS 볼륨 Liux에 대 한 암호화 되 면 Linux IaaS vm의 OS 볼륨 암호화를 해제 하면 지원 되지 않습니다.

**Q:** Azure Disk Encryption에서 "BYOK(Bring Your Own Key)" 기능을 사용하나요?

**A:** 네, 사용자 고유의 키 암호화 키를 제공할 수 있습니다. 이러한 키는 hello Azure 디스크 암호화에 대 한 키 저장소는 Azure 키 자격 증명 모음에 보호 됩니다. Hello 키 암호화 키에 대 한 자세한 내용은 시나리오를 지 원하는, hello Azure 디스크 암호화 배포 시나리오 및 환경 참조

**Q:** Azure에서 만든 키 암호화 키를 사용할 수 있나요?

**A:** 예, Azure 디스크 암호화 사용에 대 한 Azure 키 자격 증명 모음 toogenerate 키 암호화 키를 사용할 수 있습니다. 이러한 키는 hello Azure 디스크 암호화에 대 한 키 저장소는 Azure 키 자격 증명 모음에 보호 됩니다. Hello 키 암호화 키에 대 한 자세한 내용은 시나리오를 지 원하는, hello Azure 디스크 암호화 배포 시나리오 및 환경 참조

**Q:** 온-프레미스 키 관리 서비스/HSM toosafeguard hello 암호화 키 사용할 수 있습니까?

**A:** Azure 디스크 암호화 hello 온-프레미스 키 관리 서비스/HSM toosafeguard hello 암호화 키를 사용할 수 없습니다. Hello Azure 키 자격 증명 모음 서비스 toosafeguard hello 암호화 키만 사용할 수 있습니다. Hello 키 암호화 키에 대 한 자세한 내용은 시나리오를 지 원하는, hello Azure 디스크 암호화 배포 시나리오 및 환경 참조

**Q:** hello 필수 구성 요소 tooconfigure Azure 디스크 암호화 무엇 인가요?

**A:** hello Azure 디스크 암호화 필수 PowerShell 스크립트 toocreate AAD 응용 프로그램, 새로운 키 자격 증명 모음 만들기 또는 디스크는 암호화 액세스 tooenable 암호화 및 보호 방법을 암호 및 키에 대 한 기존 키 자격 증명 모음을 설정 합니다.  Hello 키 암호화 키에 대 한 자세한 내용은 시나리오를 지 원하는, hello Azure 디스크 암호화 필수 구성 요소 및 배포 시나리오 및 환경 참조

**Q:** 방법에 자세한 정보를 읽을 수는 있는 Azure 디스크 암호화를 구성 하기 위한 PowerShell toouse?

**A:** Azure Disk Encryption 기본 작업을 수행하는 방법과 고급 시나리오에 대한 몇 가지 훌륭한 문서가 있습니다. Hello 기본 작업에 대 한 체크 아웃 탐색 [Azure powershell-1 부의 Azure 디스크 암호화](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/16/explore-azure-disk-encryption-with-azure-powershell/)합니다. 고급 시나리오는 [Azure PowerShell를 사용하여 Azure Disk Encryption 탐색 - 2부(영문)](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2/)를 참조하세요.

**Q:** Azure Disk Encryption에서 지원하는 Azure PowerShell 버전은 무엇인가요?

**A:** 사용 hello 최신 버전의 Azure PowerShell SDK 버전 tooconfigure Azure 디스크 암호화 합니다. 최신 버전의 hello 다운로드 [Azure PowerShell](https://github.com/Azure/azure-powershell/releases)합니다. Azure SDK 버전 1.1.0에서는 Azure Disk Encryption을 지원하지 않습니다.

> [!NOTE]
> hello Linux Azure 디스크 암호화 미리 보기 확장을 사용 하는 사용 되지 않습니다. 자세한 내용은 참조 toodocumentation [여기](https://blogs.msdn.microsoft.com/azuresecurity/2017/07/12/deprecating-azure-disk-encryption-preview-extension-for-linux-iaas-vms/)

**Q:** 사용자 지정 Linux 이미지에 Azure Disk Encryption을 적용할 수 있나요?

**A:** 사용자 지정 Linux 이미지에는 Azure Disk Encryption을 적용할 수 없습니다. 유일한 hello 갤러리 Linux 이미지 위에 명시 된 지원 hello 배포판을 지원 합니다. 현재 사용자 지정 Linux 이미지는 지원하지 않습니다.

**Q:** 업데이트 tooa Red Hat Linux VM 적용할 수 Yum 업데이트를 사용 하 시겠습니까?

**A:** 예, [여기](https://blogs.msdn.microsoft.com/azuresecurity/2017/07/13/applying-updates-to-a-encrypted-azure-iaas-red-hat-vm-using-yum-update/)에서 설명하는 지침에 따라 Red Hat Linux VM을 업데이트하거나 패치할 수 있습니다.

**Q:** 여기서 tooask 질문을 이동 하거나 수 피드백 제공

**A:** 질문 hello Azure 디스크 암호화 포럼에 대 한 피드백을 요청을 제공할 수 있습니다 [여기](https://social.msdn.microsoft.com/Forums/home?forum=AzureDiskEncryption)

## <a name="see-also"></a>참고 항목
이 문서에서는 알아보았습니다 더 암호화에 대 한 hello 빈도가 가장 높은 질문 관련된 tooAzure 디스크,이 서비스 및 읽기 해당 기능에 대 한 자세한 내용은:

- [Azure Security Center에서 디스크 암호화 적용](https://docs.microsoft.com/azure/security-center/security-center-apply-disk-encryption)
- [Azure 가상 컴퓨터 암호화](https://docs.microsoft.com/azure/security-center/security-center-disk-encryption)
- [Azure 미사용 데이터 암호화](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest)
