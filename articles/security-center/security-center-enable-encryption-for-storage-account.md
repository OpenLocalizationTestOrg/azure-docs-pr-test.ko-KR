---
title: "Azure 보안 센터의 저장소 계정에 대 한 aaaEnable 암호화 | Microsoft Docs"
description: "이 문서에서는 어떻게 tooimplement hello Azure 보안 센터 권장 * * 암호화에 대 한 Azure 저장소 계정 * *를 사용 합니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/20/2016
ms.author: terrylan
ms.openlocfilehash: c5cbafbf3a8be86f213dcf1c0c0ddcc0222b3d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a>Azure Security Center에서 Azure Storage 계정에 암호화 사용
Azure Security Center에서는 미사용 데이터에 대한 Azure Storage 서비스 암호화를 사용하도록 권장합니다.

저장소 서비스 암호화 (SSE) 검색 하기 전에 hello 데이터 tooAzure 저장소 쓰일 때 hello 데이터를 암호화 및 해독 하 여 작동 합니다.  SSE는 hello Azure Blob 서비스에 대 한 현재 사용할 수 및 블록 blob의 페이지 blob 사용할 수 있으며 추가 blob입니다.  toolearn 더 참조 [미사용 데이터에 대 한 저장소 서비스 암호화](../storage/common/storage-service-encryption.md)합니다.


> [!Note]
> 암호화를 사용하도록 설정하면 새 데이터만 암호화됩니다. 저장소 계정의 모든 기존 blob은 암호화되지 않은 상태로 유지됩니다. tooencrypt 기존 blob 참조 hello [저장소 서비스 암호화 FAQ](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest)합니다.
>
>

Storage 서비스 암호화는 Resource Manager 저장소 계정에만 지원됩니다. 클래식 저장소 계정은 현재 지원되지 않습니다. 클래식 toounderstand hello 및 리소스 관리자 배포 모델 참조 [Azure 배포 모델](../azure-classic-rm.md)합니다.

> [!NOTE]
> 이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다.  이 문서는 단계별 가이드가 아닙니다.
>
>

## <a name="implement-hello-recommendation"></a>Hello 권장 구성 구현
1. Hello에 **권장 사항을** 블레이드를 **Azure 저장소 계정에 대 한 암호화를 사용 하도록 설정**합니다.
   ![저장소 계정에 암호화 사용][1]
2. hello **저장소 암호화 사용** 블레이드를 엽니다. 이 블레이드는 hello Azure 저장소 계정의 저장소 암호화를 해제 하는 위치를 나열 합니다. 이 예제에서는 **storageacct1**을 선택해 보겠습니다.
   ![저장소 암호화 사용][2]
3. hello **암호화** 블레이드 **storageacct1** 열립니다. **사용**을 선택합니다.
   ![암호화 블레이드][3]
4. **저장**을 선택합니다.

이제 **storageacct1**에 대한 저장소 암호화가 사용하도록 설정되었습니다.


## <a name="see-also"></a>참고 항목
이 문서에 설명 했습니다 어떻게 tooimplement hello 보안 센터 권장 사항 "Enable 암호화 Azure 저장소 계정에 대 한 합니다." Azure 저장소 서비스 암호화에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [휴지 상태의 데이터에 대한 Azure 저장소 서비스 암호화](../storage/common/storage-service-encryption.md)

보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -자세한 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.
* [Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.
* [Azure Security Center에서 보안 권장 사항 관리](security-center-recommendations.md) - 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.
* [Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) - Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png
