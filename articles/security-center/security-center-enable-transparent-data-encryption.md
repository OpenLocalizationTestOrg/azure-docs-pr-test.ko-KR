---
title: "Azure 보안 센터에서 투명 한 데이터 암호화 aaaEnable | Microsoft Docs"
description: "이 문서에서는 어떻게 tooimplement hello Azure 보안 센터 권장 * *를 사용 하도록 설정 투명 한 데이터 암호화 * *입니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e4be8a0e-2118-4ee9-a266-69e52d9f7f8e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 94c6e9a1feddaa48faac6c835d416c4d131cd5c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a>Azure 보안 센터에서 투명한 데이터 암호화 사용
아직 TDE(투명한 데이터 암호화)를 사용하도록 설정하지 않은 경우 SQL 데이터베이스에서 TDE를 사용하도록 설정하는 것이 좋습니다. TDE는에서는 데이터를 보호 하 고 변경 내용을 tooyour 응용 프로그램 필요 없이 데이터베이스, 연결 된 백업 및 트랜잭션 로그 파일에, 암호화 하 여 규정 준수 요구 사항을 충족할 수 있습니다. toolearn 더 참조 [Azure SQL 데이터베이스를 사용한 투명 한 데이터 암호화](https://msdn.microsoft.com/library/dn948096)합니다.

이 권장 사항은 적용 toohello Azure SQL 서비스에만 사용 합니다. 가상 컴퓨터에서 실행 되는 SQL 포함 되지 않습니다.

> [!NOTE]
> 이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다.  단계별 가이드는 아닙니다.
>
>

## <a name="implement-hello-recommendation"></a>Hello 권장 구성 구현
1. Hello에 **권장 사항을** 블레이드를 **투명 한 데이터 암호화**합니다.
   ![투명한 데이터 암호화 사용][1]
2. Hello 열립니다 **SQL 데이터베이스에서 투명 한 데이터 암호화를 사용 하도록 설정** 블레이드입니다. 에 SQL 데이터베이스 tooenable TDE를 선택 합니다.
   ![선택 하는 SQL DB tooenable TDE][2]
3. Hello에 **투명 한 데이터 암호화** 블레이드를 **ON** 데이터 암호화 및 선택에서 **저장** hello 블레이드의 hello 위쪽 리본 메뉴에 있습니다.
   ![TDE 켜기][3]

   TDE가 설정 되 면 hello 선택한 SQL 데이터베이스 hello **암호화 상태** 너무 바뀝니다**암호화**합니다.    

   ![암호화 상태][4]

## <a name="see-also"></a>참고 항목
이 문서에 설명 했습니다 어떻게 tooimplement hello 보안 센터 권장 "Enable 투명 한 데이터 암호화 합니다." SQL TDE에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [Azure SQL 데이터베이스를 사용한 투명한 데이터 암호화](https://msdn.microsoft.com/library/dn948096)
* [투명한 데이터 암호화(TDE) 시작](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -자세한 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.
* [Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.
* [Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.
* [Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -hello 최신 Azure 보안 뉴스 및 정보를 가져옵니다.

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png
