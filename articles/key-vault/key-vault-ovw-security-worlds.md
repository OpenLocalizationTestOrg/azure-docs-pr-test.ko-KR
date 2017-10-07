---
ms.assetid: 
title: "주요 자격 증명 모음 보안 권역 aaaAzure | Microsoft Docs"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/03/2017
ms.openlocfilehash: 1995119c9e9886829d6c50af921f275d10e382f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a>Azure Key Vault 보안 권역 및 지리적 경계

Azure Key Vault는 다중 테넌트 서비스이며, 각 Azure 위치의 HSM(하드웨어 보안 모듈) 풀을 사용합니다. 

모든 Hsm hello의 Azure 위치에 동일한 지리적 지역 공유 hello 동일한 암호화 경계 (Thales 보안 권역). 예를 들어 미국 동부 및 공유 미국 서 부 hello 동일한 보안 권역 toohello 미국 지리적 위치에 속하기 때문에 있습니다. 마찬가지로, 일본 공유의 모든 Azure 위치 오스트레일리아, 인도의 모든 Azure 위치와 동일한 보안 권역 hello 등에입니다. 

## <a name="backup-and-restore-behavior"></a>백업 및 복원 동작

이러한 조건에 모두으로 다른 Azure 위치에 tooa에 키 자격 증명 모음. 복원 하는 Azure 위치 일 수 있습니다 하나에 키 자격 증명 모음에서 키의 백업:

- 모두 hello Azure 위치 toohello 속한 동일한 지리적 위치
- Toohello 속한 hello 키 자격 증명 모음을 모두 동일한 Azure 구독

예를 들어, 서인도에서 주요 자격 증명 모음에 있는 키의 지정 된 구독에 의해 발생 한 백업만 수 hello에 복원 된 tooanother에 키 자격 증명 모음. 동일한 구독과 지리적 위치입니다. 인도 서 부, 중앙 인도 또는 남 인도 있습니다.

## <a name="regions-and-products"></a>지역 및 제품

- [Azure 지역](https://azure.microsoft.com/regions/)
- [지역별 Microsoft 제품](https://azure.microsoft.com/regions/services/)

지역에 매핑된 toosecurity 세계, 주요 hello 테이블 제목으로 표시 되는

예를 들어 hello 지역 문서에서 제품 hello에서는 **Americas** 탭 영역이 EAST US, 미국 중남부, 미국 서 부 모든 매핑 toohello Americas 합니다. 

>[!NOTE]
>예외로, 미국 국방부 동부 및 미국 국방부 중부에는 자체 보안 권역이 있습니다. 

마찬가지로 hello에서 **유럽** 탭, 유럽 북부 및 서 부 유럽 모두 매핑할 toohello Europe 지역입니다. hello도 마찬가지입니다 hello에 **아시아 태평양** 탭 합니다.



