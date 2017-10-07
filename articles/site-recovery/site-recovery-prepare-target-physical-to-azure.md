---
title: "대상 (실제 tooAzure) 준비 | Microsoft Docs"
description: "이 문서에서는 설명 방법을 tooprepare tooAzure Windows 또는 Linux를 실행 하는 물리적 서버를 복제 하 여 Azure 환경 toostart 합니다."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhemraj
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 5/31/2017
ms.author: bsiva
ms.openlocfilehash: 126fb86133e1a00f5669410943565c4cd78e4369
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-target-vmware-tooazure"></a>대상 (VMware tooAzure) 준비
> [!div class="op_single_selector"]
> * [VMware tooAzure](./site-recovery-prepare-target-vmware-to-azure.md)
> * [물리적 tooAzure](./site-recovery-prepare-target-physical-to-azure.md)

이 문서에서는 설명 방법을 tooprepare 복제 하는 물리적 서버 (x64)를 Azure로 Windows 또는 Linux를 실행 하 여 Azure 환경 toostart 합니다.

## <a name="prerequisites"></a>필수 조건

hello 문서 hello 다음을 가정합니다.
- 복구 서비스 자격 증명 모음 tooprotect을 실제 서버 만들었습니다. Hello에서 복구 서비스 자격 증명 모음을 만들 수 있습니다 [Azure 포털](http://portal.azure.com "Azure 포털")합니다.
- 있는 [온-프레미스 환경을 설정](./site-recovery-set-up-physical-to-azure.md) tooreplicate 물리적 서버 tooAzure 합니다.

## <a name="prepare-target"></a>대상 준비

Hello를 완료 한 후 **단계 1:Select 보호 목표** 및 **2 단계: 준비 소스**, 너무 취해집니다**3 단계: 대상**

![대상 준비](./media/site-recovery-prepare-target-physical-to-azure/prepare-target-physical-to-azure.png)

1. **구독:** hello에서 드롭 다운 메뉴에서 선택 hello tooreplicate 구독 실제 서버를 합니다.
2. **배포 모델:** 선택 hello 배포 모델 (Classic 또는 리소스 관리자)

배포 모델을 선택 하는 hello에 따라, 유효성 검사를 해야 하는 하나 이상의 호환 되는 저장소 계정 및 대상 구독 tooreplicate hello 및 장애 조치의 가상 네트워크를 실제 서버 tooensure는 실행 됩니다.

Hello 유효성 검사를 성공적으로 완료 되 면 확인 toogo toohello 다음 단계를 클릭 합니다.

더 많은 tooadd ु 없거나 호환 리소스 관리자 저장소 계정 또는 가상 네트워크 않은 후 그렇게 hello를 클릭 하 여 **저장소 계정 추가** 또는 **+ 네트워크** hello hello 위쪽에 단추 블레이드입니다.

## <a name="next-steps"></a>다음 단계
[복제 설정 구성](./site-recovery-setup-replication-settings-vmware.md)
