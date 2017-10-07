---
title: "Azure AD Connect: 서비스 인스턴스 동기화 | Microsoft Docs"
description: "이 페이지에서는 Azure AD 인스턴스에 대한 특별한 고려 사항을 문서화합니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: f340ea11-8ff5-4ae6-b09d-e939c76355a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2a0d8a599cf84cd6530bdbb24951156510d2cf3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a>Azure AD Connect: 인스턴스에 대한 특별한 고려 사항
Azure AD의 전세계 인스턴스 hello와 azure AD Connect은 가장 많이 사용 및 Office 365 합니다. 그러나 다른 인스턴스도 있고 URL 및 기타 특별한 고려 사항에 대한 다른 요구 사항을 포함합니다.

## <a name="microsoft-cloud-germany"></a>Microsoft 클라우드 독일
hello [Microsoft 클라우드 독일](http://www.microsoft.de/cloud-deutschland) 독일어 데이터 트러스티 운영 되는 전체 클라우드입니다.

| 프록시 서버에서 Url tooopen |
| --- |
| \*.microsoftonline.de |
| \*.windows.net |
| +인증서 해지 목록 |

Tooyour Azure AD 테 넌 트에 로그인 할 때 hello onmicrosoft.de 도메인의 계정을 사용 해야 합니다.

Hello Microsoft 클라우드 독일에 현재 존재 하는 기능은:

* **Azure AD Connect Health**를 사용할 수 없습니다.
* **자동 업데이트**를 사용할 수 없습니다.
* **비밀번호 쓰기 저장**은 Azure AD Connect 버전 1.1.570.0 이상에서 미리 보기로 제공됩니다.
* 다른 Azure AD Premium 서비스를 사용할 수 없습니다.

## <a name="microsoft-azure-government-cloud"></a>Microsoft Azure Government 클라우드
hello [Microsoft Azure Government 클라우드](https://azure.microsoft.com/features/gov/) 미국 정부에 대 한 클라우드입니다.

이 클라우드는 DirSync의 이전 버전에서 지원되어 왔습니다. Azure AD Connect의 1.1.180 빌드에서 hello 차세대 hello 클라우드 사용할 수 있습니다. 이 세대 미국 전용 기반된 끝점을 사용 하는 있고 프록시 서버에서 다른 Url tooopen 목록이 있습니다.

| 프록시 서버에서 Url tooopen |
| --- |
| \*.microsoftonline.com |
| \*.microsoftonline.us |
| \*.gov.us.microsoftonline.com |
| +인증서 해지 목록 |

Azure AD Connect 수 없으면 tooautomatically 검색 된 Azure AD 테 넌 트 hello 정부 클라우드에 있어야 합니다. 대신 tootake hello Azure AD Connect를 설치할 때 작업을 수행 해야 합니다.

1. Hello Azure AD Connect 설치를 시작 합니다.
2. Hello 첫 번째 페이지 tooaccept hello EULA는 것을 표시 하는 경우 계속 하지 마십시오 두려면 hello 설치 마법사를 실행 합니다.
3. Regedit를 시작 하 고 hello 레지스트리 키 변경 `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello 값 `2`합니다.
4. 로 돌아가려면 toohello Azure AD Connect 설치 마법사, hello EULA에 동의 및 계속 합니다. 설치 하는 동안 확인 되었는지 toouse hello **사용자 지정 구성** 설치 경로 (및 Express 설치가 아닌). 그 hello 설치를 정상적으로 계속 합니다.

현재에 없는 hello Microsoft Azure Government 클라우드 기능:

* **Azure AD Connect Health**를 사용할 수 없습니다.
* **자동 업데이트**를 사용할 수 없습니다.
* **비밀번호 쓰기 저장**은 Azure AD Connect 버전 1.1.570.0 이상에서 미리 보기로 제공됩니다.
* 다른 Azure AD Premium 서비스를 사용할 수 없습니다.

## <a name="next-steps"></a>다음 단계
[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.
