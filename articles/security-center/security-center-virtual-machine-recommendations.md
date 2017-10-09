---
title: "aaaProtecting Azure 보안 센터에서 가상 컴퓨터 | Microsoft Docs"
description: "이 문서에서는 가상 컴퓨터를 보호하고 보안 정책을 준수하는 데 도움이 되는 Azure 보안 센터의 권장 사항에 대해 설명합니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 47fa1f76-683d-4230-b4ed-d123fef9a3e8
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: terrylan
ms.openlocfilehash: 926c04974f61215b4a3e02646f23dafb87c793e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-virtual-machines-in-azure-security-center"></a>Azure 보안 센터에서 가상 컴퓨터 보호
Azure 보안 센터 리소스를 Azure의 hello 보안 상태를 분석합니다. 보안 센터 잠재적인 보안 문제를 식별 하는 경우 필요한 hello 컨트롤 구성 hello 과정을 안내 하는 권장 구성을 만듭니다.  권장 사항이 적용 tooAzure 리소스 종류: 가상 컴퓨터 (Vm), 네트워킹, SQL, 및 응용 프로그램입니다.

이 문서에서는 tooVMs 적용 되는 권장 합니다.  VM 권장 사항은 데이터 수집, 시스템 업데이트 적용, 맬웨어 방지 프로그램 프로비전, VM 디스크 암호화 등에 초점을 둡니다.  Hello 사용 가능한 VM 권장 사항 및 각은 적용 하는 경우 수행할 작업으로 참조 toohelp 아래 hello 테이블 사용 이해 합니다.

## <a name="available-vm-recommendations"></a>제공되는 VM 권장 사항
| 권장 사항 | 설명 |
| --- | --- |
| [구독에 대해 데이터 수집 활성화](security-center-enable-data-collection.md) |구독에서 각 구독 하 고 모든 가상 컴퓨터 (Vm)에 대 한 hello 보안 정책에서 데이터 컬렉션 켜기 하는 것이 좋습니다. |
| [Azure Storage 계정에 암호화 사용](security-center-enable-encryption-for-storage-account.md) | 미사용 데이터에 대한 Azure Storage 서비스 암호화를 사용하도록 권장합니다. 저장소 서비스 암호화 (SSE) tooAzure 저장소 작성 하 고 검색 하기 전에 암호를 해독 하는 경우 hello 데이터를 암호화 하 여 작동 합니다. SSE는 hello Azure Blob 서비스에 대 한 현재 사용할 수 및 블록 blob의 페이지 blob 사용할 수 있으며 추가 blob입니다. toolearn 더 참조 [미사용 데이터에 대 한 저장소 서비스 암호화](../storage/common/storage-service-encryption.md)합니다.</br>SSE는 Resource Manager 저장소 계정에만 지원됩니다. 클래식 저장소 계정은 현재 지원되지 않습니다. 클래식 toounderstand hello 및 리소스 관리자 배포 모델 참조 [Azure 배포 모델](../azure-classic-rm.md)합니다. |
| [OS 취약성 해결](security-center-remediate-os-vulnerabilities.md) |예를 들어 권장 구성 규칙 hello로 운영 체제 구성을 정렬 하는 권장 저장 암호 toobe를 허용 하지 않습니다. |
| [시스템 업데이트 적용](security-center-apply-system-updates.md) |누락 된 시스템 보안 및 중요 업데이트 tooVMs를 배포 하는 것이 좋습니다. |
| [Just-In-Time 네트워크 액세스 제어 적용](security-center-just-in-time.md) | Just-In-Time VM 액세스만 적용해야 합니다. 시간 기능에만 있는 hello 되며 미리 보기에서 hello 보안 센터의 표준 계층에 있습니다. 참조 [가격 책정](security-center-pricing.md) 보안 센터에 대해 자세히 toolearn 가격 책정 계층이 있습니다. |
| [시스템 업데이트 후 다시 부팅](security-center-apply-system-updates.md#reboot-after-system-updates) |시스템 업데이트를 적용 한 VM toocomplete hello 프로세스를 다시 부팅 하는 것이 좋습니다. |
| [Endpoint Protection 설치](security-center-install-endpoint-protection.md) |맬웨어 방지 프로그램 tooVMs (Windows Vm에만 해당)를 프로 비전 하는 것이 좋습니다. |
| [Endpoint Protection 상태 경고 해결](security-center-resolve-endpoint-protection-health-alerts.md) |끝점 보호 오류를 해결하는 것이 좋습니다. |
| [VM 에이전트 사용](security-center-enable-vm-agent.md) |하면 toosee Vm 해야 하는 hello VM 에이전트를 사용 합니다. VM 에이전트 hello 순서 tooprovision 패치 검사, 검색 기준 및 맬웨어 방지 프로그램에서에서 Vm에 설치 되어야 합니다. hello Azure Marketplace에서에서 배포 되는 Vm에 대 한 hello VM 에이전트는 기본적으로 설치 됩니다. hello 문서 [VM 에이전트 및 확장-2 부](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) tooinstall VM 에이전트를 hello 하는 방법에 대해 설명 합니다. |
| [디스크 암호화 적용](security-center-apply-disk-encryption.md) |Azure 디스크 암호화(Windows 및 Linux VM)를 사용하여 VM 디스크를 암호화하는 것이 좋습니다. Hello OS와 VM에 데이터 볼륨에 대 한 암호화를 사용 하는 것이 좋습니다. |
| [OS 버전 업데이트](security-center-update-os-version.md) |OS 제품군에 대 한 hello 운영 체제 (OS) 버전에 클라우드 서비스 toohello 사용 가능한 최신 버전에 대 한 업데이트 하는 것이 좋습니다.  클라우드 서비스에 대해 자세히 toolearn 참조 hello [클라우드 서비스 개요](../cloud-services/cloud-services-choose-me.md)합니다. |
| [취약점 평가 설치되지 않음](security-center-vulnerability-assessment-recommendations.md) |VM에 취약점 평가 솔루션을 설치하는 것이 좋습니다. |
| [취약점 해결](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |VM에 설치 하는 hello 취약점 평가 솔루션에 의해 검색 toosee 시스템 및 응용 프로그램 취약성이 있습니다. |

## <a name="see-also"></a>참고 항목
tooother Azure 리소스 유형에 적용 되는 권장 사항에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [Azure 보안 센터에서 응용 프로그램 보호](security-center-application-recommendations.md)
* [Azure 보안 센터에서 네트워크 보호](security-center-network-recommendations.md)
* [Azure 보안 센터에서 Azure SQL 서비스 보호](security-center-sql-service-recommendations.md)

보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -자세한 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.
* [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.
* [Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.
