---
title: "aaaWhat은 Azure 키 자격 증명 모음 이란? | Microsoft Docs"
description: "Azure 키 자격 증명 모음은 클라우드 응용 프로그램 및 서비스에서 사용되는 암호화 키 및 비밀을 보호하는데 도움이 됩니다. Azure 키 자격 증명 모음을 사용하여, 고객은 키와 비밀(예: 인증 키, 저장소 계정 키, 데이터 암호화 키, PFX 파일 및 암호)을 암호화하여 하드웨어 보안 모듈(HSM)로 보호된 키를 사용합니다."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: e759df6f-0638-43b1-98ed-30b3913f9b82
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 296fcce03658b96b84afab299b73681bbe8ac9fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-key-vault"></a>Azure 키 자격 증명 모음이란?
Azure 키 자격 증명 모음은 대부분 지역에서 사용할 수 있습니다. 자세한 내용은 참조 hello [키 자격 증명 모음 가격 책정 페이지](https://azure.microsoft.com/pricing/details/key-vault/)합니다.

## <a name="introduction"></a>소개
Azure 키 자격 증명 모음은 클라우드 응용 프로그램 및 서비스에서 사용되는 암호화 키 및 비밀을 보호하는데 도움이 됩니다. Key Vault를 사용하여, 키와 비밀(예: 인증 키, 저장소 계정 키, 데이터 암호화 키, PFX 파일 및 암호)을 암호화에 하드웨어 보안 모듈(HSM)로 보호된 키를 사용합니다. 추가된 보증을 위해, HSM에서 키를 생성하거나 가져올 수 있습니다. Toodo이, Microsoft 프로세스를 선택 하는 경우 키 FIPS 140-2에서에서 수준 2 유효성이 검사 된 Hsm (하드웨어 및 펌웨어) 합니다.  

주요 자격 증명 모음은 hello 키 관리 프로세스를 간소화 하 고 액세스 하 고 데이터를 암호화 하는 키의 toomaintain 제어 있습니다. 개발자는 개발 및 테스트 (분)에 대 한 키를 만들 수 있으며 다음 원활 하 게 마이그레이션할 tooproduction 키. 보안 관리자 수 부여 (및 해지) 필요에 따라 권한 tookeys 합니다.

사용 하 여 hello 테이블 toobetter 다음 주요 자격 증명 모음 보안 관리자 및 개발자의 toomeet hello 요구 시키는 방법을 이해 합니다.

| 역할 | 문제 설명 | Azure 키 자격 증명 모음으로 해결됨 |
| --- | --- | --- |
| Azure 응용 프로그램용 개발자 |"Toowrite 응용 프로그램에서 서명 및 암호화를 위한 키를 사용 하는 Azure에 대 한 싶지만 원하는 이러한 키 toobe 외부 응용 프로그램에서 hello 솔루션은 지리적으로 분산 하는 응용 프로그램에 적합 합니다. <br/><br/>이러한 키와 암호 toobe toowrite hello 코드를 직접 필요 없이 보호 하려고 합니다. 또한 이러한 키와 암호 toobe 쉽게에 원하는 내게 toouse 최적의 성능으로 내 응용 프로그램에서. " |√ 키를 자격 증명 모음에 저장하고 필요할 때 URI로 호출합니다.<br/><br/> √ Azure에서는 업계 표준 알고리즘, 키 길이 및 HSM(하드웨어 보안 모듈)을 사용하여 키를 보호합니다.<br/><br/> √ 키 동일 hello에 상주 하는 Hsm에서 처리 되는 hello 응용 프로그램과 Azure 데이터 센터입니다. 안정성 및 hello 키 온-프레미스와 같은 별도 위치에 있는 경우 보다 대기 시간의 감소 제공 합니다. |
| SaaS(Software as a Service)에 대한 개발자  |"않으려고 hello 책임이 나 잠재적인 책임 내 고객의 테 넌 트 키 및 암호에 대 한 합니다. <br/><br/>Hello 고객 tooown 원하는 했으며 I 수행할 기껏해야 hello 핵심 소프트웨어 기능을 제공 하는 이러한 작업에 집중할 수 있도록 해당 키를 관리 합니다. " |√ 고객은 Azure에서 고유한 키를 가져오고 관리할 수 있습니다. SaaS 응용 프로그램의 해당 고객의 키를 사용 하 여 tooperform 암호화 작업 하면 주요 자격 증명 모음 hello 응용 프로그램을 대신 하 여 이러한 작업을 수행 합니다. hello 응용 프로그램 hello 고객의 키를 참조 하지 않습니다. |
| 수석 보안 책임자(CSO) |"Tooknow 응용 프로그램 보안 키 관리에 대 한 hsm은 FIPS 140-2 수준 2 준수 합니다. <br/><br/>내 조직 hello 키 수명 주기를 제어 인지 toomake를 원하고 키 사용을 모니터링할 수 있습니다. <br/><br/>및 원하는 Azure의 단일 위치에서 toomanage hello 키 여러 Azure 서비스 및 리소스를 사용 합니다. " |√ HSM은 FIPS 140-2 Level 2 검증되었습니다.<br/><br/>√ Key Vault는 Microsoft에서 키를 보거나 추출할 수 없게 설계되어 있습니다.<br/><br/>√ 키 사용을 거의 실시간으로 로깅합니다.<br/><br/>√ hello 자격 증명 모음 지원 및 응용 프로그램을 사용할 수 자격 증명 모음에에서 있는 Azure 지역 것에 관계 없이 단일 인터페이스를 제공 합니다. |

Azure를 구독하는 사용자는 주요 자격 증명 모음을 만들고 사용할 수 있습니다. 키 자격 증명 모음에는 개발자와 보안 관리자의 혜택이 있지만, 조직에 대한 다른 Azure 서비스를 관리하는 조직의 관리자가 구현하고 관리할 수 있습니다. 예를 들어이 관리자는 Azure 구독을 사용 하 여 로그인, hello 조직에 대 한 자격 증명 모음에서 어떤 toostore 키 만들고 후 운영 작업에 대 한 책임을 같은 수 있습니다:

* 키 또는 비밀 만들기 또는 가져오기
* 키 또는 비밀 취소 또는 삭제
* 사용자 권한을 부여 또는 응용 프로그램 tooaccess 다음 관리 하거나 해당 키와 암호를 사용할 수 있도록 키 자격 증명 모음을 환영
* 구성 키 용도(예: 서명 또는 암호화)
* 키 사용량 모니터링

이 관리자는 개발자가 응용 프로그램에서 Uri toocall에 게 제공 그리고 보안 관리자가 키 사용 현황 로깅 정보를 제공 합니다. 

   ![Azure 키 자격 증명 모음 개요][1]

개발자는 Api를 사용 하 여를 직접 hello 키를 관리할 수도 수 있습니다. 자세한 내용은 참조 [주요 자격 증명 모음 개발자 가이드 hello](key-vault-developers-guide.md)합니다.

## <a name="next-steps"></a>다음 단계
관리자에 대한 시작 자습서의 경우 [Azure 키 자격 증명 모음 시작](key-vault-get-started.md)을 참조하세요.

키 자격 증명 모음에 사용 현황 로깅에 대한 자세한 내용은 [Azure 키 자격 증명 모음 로깅](key-vault-logging.md)을 참조하세요.

Azure Key Vault로 키 및 암호를 사용하는 방법에 대한 자세한 내용은 [키, 암호 및 인증서 정보](https://msdn.microsoft.com/library/azure/dn903623\(v=azure.1\).aspx)를 참조하세요.

<!--Image references-->
[1]: ./media/key-vault-whatis/AzureKeyVault_overview.png
