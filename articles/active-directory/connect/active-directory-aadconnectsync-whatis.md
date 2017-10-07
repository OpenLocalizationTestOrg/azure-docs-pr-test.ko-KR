---
title: "Azure AD Connect 동기화: 동기화의 이해 및 사용자 지정 | Microsoft Docs"
description: "Azure AD Connect 동기화의 작동 방법 등에 대해 설명 toocustomize 합니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: ee4bf802-045b-4da0-986e-90aba2de58d6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/01/2016
ms.author: markvi
ms.openlocfilehash: 97e4bd9904b077f2628e5f8dcbaa6f1a76168a12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understand-and-customize-synchronization"></a>Azure AD Connect 동기화: 동기화의 이해 및 사용자 지정
hello Azure Active Directory Connect 동기화 서비스 (Azure AD Connect 동기화)는 Azure AD Connect의 주요 구성 요소입니다. 온-프레미스 환경 및 Azure AD 간의 관련된 toosynchronize id 데이터 중인 모든 hello 작업이 담당 합니다. Azure AD Connect 동기화는 DirSync, Azure AD Sync 및 Forefront Identity Manager의 Azure Active Directory Connector를 구성 하는 hello로 hello 후속입니다.

이 항목은 hello에 대 한 홈 **Azure AD Connect 동기화** (라고도 **동기화 엔진이**) 및 목록 링크 tooall 다른 항목 관련된 tooit 합니다. 링크 tooAzure AD에 연결. 참조 [Azure Active Directory와 온-프레미스 id 통합](active-directory-aadconnect.md)합니다.

hello 동기화 서비스 구성의 두 가지 구성 hello 온-프레미스 **Azure AD Connect 동기화** Azure AD에서 서비스 측 구성 요소와 hello 라는 **Azure AD Connect 동기화 서비스**합니다. hello 서비스는 일반적으로 DirSync, Azure AD 동기화 및 Azure AD Connect입니다.

## <a name="azure-ad-connect-sync-topics"></a>Azure AD Connect 동기화 항목
| 항목 | 포함 및 시기 tooread |
| --- | --- |
| **Azure AD Connect 동기화 기본 사항** | |
| [Hello 아키텍처 이해](active-directory-aadconnectsync-understanding-architecture.md) |그룹 정책에 대 한 새로운 toohello 동기화 엔진은 사람과 toolearn hello 아키텍처 및 사용 되는 hello 용어에 대 한 원하는 합니다. |
| [기술 개념](active-directory-aadconnectsync-technical-concepts.md) |Hello 아키텍처 항목 및 간단 하 게 짧은 버전 설명 hello 사용 되는 용어입니다. |
| [Azure AD Connect에 대한 토폴로지](active-directory-aadconnect-topologies.md) |Hello 다른 토폴 리 지 및 시나리오 hello 동기화 엔진 지원에 설명합니다. |
| **사용자 지정 구성** | |
| [실행 중인 hello 설치 마법사를 다시](active-directory-aadconnectsync-installation-wizard.md) |옵션을 설명 hello Azure AD Connect 설치 마법사를 다시 실행할 때 사용할 수 있어야 합니다. |
| [선언적 프로비전 이해](active-directory-aadconnectsync-understanding-declarative-provisioning.md) |선언적 프로비저닝 이라고 하는 hello 구성 모델에 설명 합니다. |
| [선언적 프로비전 식 이해](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) |선언적 프로비저닝이에 사용 된 hello 식 언어에 대 한 hello 구문을 설명 합니다. |
| [Hello 기본 구성 이해](active-directory-aadconnectsync-understanding-default-configuration.md) |기본적으로 규칙 hello 및 hello 기본 구성에 설명합니다. 또한 hello 규칙 함께 기본적으로 시나리오 toowork hello에 대 한 작동 방법을 설명 합니다. |
| [사용자 및 연락처 이해](active-directory-aadconnectsync-understanding-users-and-contacts.md) |Hello 이전 항목에서 계속 하 고 사용자 및 연락처에 대 한 hello 구성을 작동 방식, 특히 다중 포리스트 환경에서 설명 합니다. |
| [어떻게 변경 toohello toomake 기본 구성](active-directory-aadconnectsync-change-the-configuration.md) |일반적인 구성 변경 tooattribute toomake 흐르는 방식을 보여 줍니다. |
| [Hello 기본 구성 변경에 대 한 모범 사례](active-directory-aadconnectsync-best-practices-changing-default-configuration.md) |지원 제한 사항 및 변경 toohello 기본적으로 구성 하기 위한 합니다. |
| [필터링 구성](active-directory-aadconnectsync-configure-filtering.md) |Hello 단계별 방법과 AD tooAzure toolimit 되는 개체를 동기화 하는 방법에 대 한 다른 옵션에 설명 tooconfigure 이러한 옵션입니다. |
| **기능 및 시나리오** | |
| [실수로 인한 삭제 방지](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) |Hello 설명 *실수로 삭제 금지* 기능 및 방법을 tooconfigure 것입니다. |
| [스케줄러](active-directory-aadconnectsync-feature-scheduler.md) |, 동기화, 데이터 가져오기 및 내보내기는 hello 기본 제공 스케줄러에 설명 합니다. |
| [암호 동기화 구현](active-directory-aadconnectsync-implement-password-synchronization.md) |암호 동기화의 작동 방법을 설명 어떻게 tooimplement, 방법과 toooperate 고 문제를 해결 합니다. |
| [장치 쓰기 저장](active-directory-aadconnect-feature-device-writeback.md) |Azure AD Connect에서 장치 쓰기 저장이 작동하는 방식에 대해 설명합니다. |
| [디렉터리 확장](active-directory-aadconnectsync-feature-directory-extensions.md) |Tooextend Azure AD 스키마와 사용자 지정 특성을 hello 하는 방법을 설명 합니다. |
| **동기화 서비스** | |
| [Azure AD Connect 동기화 서비스 기능](active-directory-aadconnectsyncservice-features.md) |동기화 서비스 쪽 hello 및 Azure AD에서 toochange 설정을 동기화 하는 방법을 설명 합니다. |
| [중복 특성 복원력](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) |설명 방법을 tooenable 사용 하 여 **userPrincipalName** 및 **proxyAddresses** 중복 된 특성 값 복구 합니다. |
| **작업 및 UI** | |
| [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md) |동기화 서비스 관리자 UI를 포함 하 여 hello 설명 [작업](active-directory-aadconnectsync-service-manager-ui-operations.md), [커넥터](active-directory-aadconnectsync-service-manager-ui-connectors.md), [메타 버스 디자이너](active-directory-aadconnectsync-service-manager-ui-mvdesigner.md), 및 [메타버스검색](active-directory-aadconnectsync-service-manager-ui-mvsearch.md) 탭 합니다. |
| [운영 작업 및 고려 사항](active-directory-aadconnectsync-operations.md) |재해 복구와 같은 운영 문제에 대해 설명합니다. |
| **방법...** | |
| [Hello Azure AD 계정 다시 설정](active-directory-aadconnectsync-howto-azureadaccount.md) |Hello 서비스 계정의 tooreset hello 자격 증명 tooconnect Azure AD Connect 동기화 tooAzure AD에서에서 사용 하는 방법입니다. |
| **자세한 내용 및 참조** | |
| [포트](active-directory-aadconnect-ports.md) |메일 그룹 포트가 있는 hello 동기화 엔진 및 온-프레미스 디렉터리와 Azure AD 간의 tooopen이 필요 합니다. |
| [특성이 tooAzure Active Directory 동기화](active-directory-aadconnectsync-attributes-synchronized.md) |온-프레미스 AD와 Azure AD 간에 동기화되는 모든 특성을 나열합니다. |
| [함수 참조](active-directory-aadconnectsync-functions-reference.md) |선언적 프로비전에 사용할 수 있는 모든 함수를 나열합니다. |

## <a name="additional-resources"></a>추가 리소스
* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)

