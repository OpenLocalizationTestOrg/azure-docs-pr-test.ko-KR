---
title: "aaaCommunity 도구-이동 클래식 리소스 tooAzure 리소스 관리자 | Microsoft Docs"
description: "Hello 커뮤니티 toohelp에서 제공 하는이 문서 카탈로그 hello 도구 클래식 toohello Azure 리소스 관리자 배포 모델에서 IaaS 리소스를 마이그레이션합니다."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 228b697b-3950-49f5-84bb-283bb56621b1
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 67d5624a14d12a2d9eb46eb12aef461b706d4589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="community-tools-toomigrate-iaas-resources-from-classic-tooazure-resource-manager"></a>커뮤니티 도구 toomigrate 클래식 tooAzure 리소스 관리자에서에서 처리 되는 IaaS 리소스
클래식 toohello Azure 리소스 관리자 배포 모델에서 IaaS 리소스에 대 한 마이그레이션을 사용 하 여 hello 커뮤니티 tooassist에서 제공 된이 문서 카탈로그 hello 도구입니다.

> [!NOTE]
> 이러한 도구는 Microsoft 지원을 통해 공식적으로 지원되지는 않습니다. 따라서 열려 있는 GitHub에 원본이 고 we're 수정 또는 추가 시나리오에 대 한 만족도 매우 tooaccept Pr 합니다. 문제가 tooreport hello GitHub 문제점 기능을 사용 합니다.
> 
> 이러한 도구를 사용하여 마이그레이션을 수행하면 클래식 Virtual Machine의 가동이 중지됩니다. 플랫폼에서 지원하는 마이그레이션 방법은 다음 페이지를 참조하세요. 
> 
>   * [플랫폼이는 클래식 tooAzure 리소스 관리자 스택에서 IaaS 리소스의 마이그레이션 지원](migration-classic-resource-manager-overview.md)
>   * [플랫폼에 대 한 기술 고찰 클래식 tooAzure 리소스 관리자에서에서의 마이그레이션 지원](migration-classic-resource-manager-deep-dive.md)
>   * [IaaS 리소스 클래식 tooAzure Azure PowerShell을 사용 하 여 리소스 관리자에서 마이그레이션](migration-classic-resource-manager-ps.md)
> 
> 

## <a name="asmmetadataparser"></a>AsmMetadataParser
Azure 서비스 관리 tooAzure 리소스 관리자에서에서 엔터프라이즈 마이그레이션의 일부로 만들어진 도우미 도구의 컬렉션입니다. 이 도구는 tooreplicate hello 마이그레이션 프로덕션 구독에 대해 실행 하기 전에 강철 있는 문제 및 마이그레이션 테스트에 사용할 수 있는 다른 구독으로 인프라입니다.

[링크 toohello 도구 설명서](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

## <a name="migaz"></a>migAz
migAz는 옵션이 추가로 toomigrate 클래식 IaaS 리소스 tooAzure 리소스 관리자 IaaS 리소스의 전체 집합입니다. hello 마이그레이션 내에서 발생할 수 hello 동일 구독 간이나 서로 다른 구독 및 구독 유형 (예: CSP 구독).

[링크 toohello 도구 설명서](https://github.com/Azure/migAz)

## <a name="next-steps"></a>다음 단계

* [클래식 tooAzure 리소스 관리자에서에서 리소스를 IaaS 플랫폼에서 지 원하는 마이그레이션 개요](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [클래식 tooAzure 리소스 관리자에서에서 마이그레이션 플랫폼 지원에 기술 심층 분석](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [클래식 tooAzure 리소스 관리자에서에서 IaaS 리소스의 마이그레이션 계획](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [클래식 tooAzure 리소스 관리자에서에서 PowerShell toomigrate IaaS 리소스를 사용 하 여](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [CLI toomigrate IaaS 리소스 클래식 tooAzure 리소스 관리자를에서 사용 하 여](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [가장 일반적인 마이그레이션 오류 검토](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [클래식 tooAzure 리소스 관리자에서에서 마이그레이션 IaaS 리소스에 대 한 가장 자주 묻는 질문 검토 hello](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

