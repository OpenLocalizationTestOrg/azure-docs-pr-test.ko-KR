---
title: "Azure RemoteApp에 대 한 aaaChange hello 청구 | Microsoft Docs"
description: "자세한 내용은 toostop Azure RemoteApp에 대 한 요금이 청구 되는 방법입니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 8f94da9a-7848-4ddc-b7b7-d9c280ccf4d7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: mbaldwin
ms.openlocfilehash: fe3841a88978ec56829932621489e75d5dd7e673
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-azure-remoteapp-toomycloudit"></a>Azure RemoteApp tooMyCloudIT에서 마이그레이션 

**Microsoft Azure RemoteApp 현재 사용 합니까?** : MyCloudIT 빌드된 자동화 도구 toomigrate Azure RemoteApp (ARA) 커넥터가 컬렉션 toohello MyCloudIT 관리 플랫폼에 Microsoft Azure에서 toorun은 계속 합니다.

**Hello Azure 리소스 관리자 포털을 이용**: hello MyCloudIT 플랫폼으로 완료 된 마이그레이션 즉시 액세스 tooAzure 새 Azure 리소스 관리자 포털을 사용 하도록 설정 합니다. 이 포털에 모든 hello 새 기능이 포함 된 혁신 사항과 Microsoft Azure에서 제공 액세스 tooVirtual 컴퓨터 크기 tooensure 비롯 하 여 배포 빌드되는 toosupport hello 비즈니스 요구 사항을 합니다.

**병렬 tooensure hello에 적합 한 솔루션 요구 사항에서 테스트**: hello MyCloudIT 마이그레이션 도구 tooinitiate hello 마이그레이션 프로세스 및 병렬 동안에서 현재 ARA 사용자가 계속 toouse ARA 테스트 만들어집니다.  사용자는 마이그레이션 및 테스트가 완료될 때까지 ARA에서 유지됩니다.  hello 마이그레이션 도구 toohandle hello 일반적인 ARA 컬렉션을 만들어집니다.  문의 하십시오 고유한 비표준 시나리오 있는 생각 되 면 [ sales@conexlink.com ](mailto:sales@conexlink.com) 다르므로 마이그레이션이 맞춤형된 계획 tooassist를 제공할 수 있습니다.

**데스크톱-as a Service 기능**: MyCloudIT는 뿐만 아니라, 하는 데 익숙한 hello RemoteApp 기능을 제공 하지만 전체 데스크톱---서비스로 제공 사항에 유의 하세요 최소 사용자 없이도 월별 비용 동일 hello에 대 한 기능 요구 사항입니다.

## <a name="what-we-will-do-for-you"></a>사용자를 위한 기능

MyCloudIT은 hello 프로그램 구독 toohello 우리의 자동된 마이그레이션 도구의 구독의 Azure 리소스 관리자 포털의 Azure 클래식 포털에서 Azure RemoteApp 서식 파일의 hello 마이그레이션을 자동화합니다.  

> [!NOTE]
> 서식 파일에 남아 있어야 하는 Azure RemoteApp hello hello 원래 Azure RemoteApp 배포와 같은 Azure 지역입니다.  Hello 마이그레이션하는 동안 toochange Azure 지역 또는 Azure 구독을 필요한 경우에 문의해 주세요 추가 참고 자료 [ sales@conexlink.com ](mailto:sales@conexlink.com)합니다.

Hello에 대 한 자세한 정보에 대 한 아래 읽기 hello MyCloudIT 마이그레이션 도구의 마이그레이션 프로세스를 자동화 됨:

1. hello 마이그레이션 도구는 모든 기존 ARA 배포에 대 한 현재 구독을 검색합니다.  
2. 한 번에 하나의 ARA 컬렉션 toomigrate를 선택 합니다.  컬렉션이 여러 개 있는 경우 도구를 여러 번 실행합니다.
3. 레거시 데이터를 검색 하거나 수동으로 Upd toohello 새 배포를 매핑할 수 있도록 hello 옵션 toocopy hello 사용자 프로필 디스크 (UPD) tooyour 새 배포를 해야 합니다. Toocopy Upd 프로그램을 선택 하면 hello Upd를 저장 하 고 hello UPD 이름 tooeach 사용자 이름을 매핑하는 텍스트 파일을 포함 합니다.  Upd hello hello RDSMGMT 서버에 복사한 tooa 공유 됩니다 `F:\Shares\LegacyUPD` hello 공유를 통해 노출 될 및 `\\RDSmgmt\LegacyUPD`합니다. 
4. 마이그레이션에는 현재 ARA 배포에 대해 가동 중지 시간이 필요하지 않습니다.  그러나 모든 변경 내용을 toohello Upd (ARA)에서 hello 복사 후 hello Azure 리소스 관리자 포털에 저장 된 hello Upd에 이러한 변경 내용은 반영 되지 않습니다. 
5. 새 Azure 리소스 hello에 클래식 Azure 가상 네트워크의 파일 서버 VNet 기존 클래식 Azure 가상 네트워크 간의 피어 링 설정는 hello 새 가상 네트워크 생성을 도메인 컨트롤러와 같은 추가 Vm이 있는 경우 관리자 포털입니다.
6. 자동화 된 솔루션은 VNet 기존 클래식 Azure 가상 네트워크 간의 피어 링 설정 및 새 가상 네트워크를 기존 ARA 배포 하이브리드 배포; 인 경우 hello만 즉, 인증을 수행 하는 Windows Server Active Directory 도메인 컨트롤러에 hello 기존 클래식 가상 네트워크와 합니다. VNet 사용자 컬렉션에 대 한 피어 링 설정 하지 않으면 म VNet 피어 링 필요한 표시 되지만 문의해 주십시오으로 [ sales@conexlink.com ](mailto:sales@conexlink.com) 만족도 매우 tooconfigure 추가 비용 없이 VNet 피어 링 수 있습니다.
7. 자동화 된 솔루션 Azure DNS 구성을 업데이트 하는 방법을 사용 하면 새 가상 네트워크 설정 tooensure hello 새 배포 hello에 도메인 컨트롤러를 기존 tooyour 연결할 수 있습니다 클래식 VNet입니다.
8. 자동화 된 솔루션은 새로운이 가상 네트워크를 생성 하 고 배포에 기존 Windows Server Active Directory 서버 hello VNet 피어 링 설정할 때 IP 주소 충돌이 없습니다 되는지 확인 합니다.
9. 인증을 위해 Azure AD를 통해서만 경우 MyCloudIT 새 Windows Server Active Directory 도메인 만들고 hello 기존 Azure AD 인스턴스와 hello 만든 새 Windows Server Active Directory 도메인 간의 toosynchronize 사용자 Azure AD Connect를 사용 하 여 MyCloudIT 의해서 합니다에.
10. Windows Server Active Directory 도메인 tooauthenticate ARA 사용자가 사용 하는 자동화 된 솔루션에 새 MyCloudIT 배포 tooyour VNet 피어 링을 통해 Windows Server Active Directory 도메인 컨트롤러를 기존 연결 됩니다.
11. 인증에 Azure Active Directory Domain Services를 사용하는 경우 마이그레이션이 가능하지만 문의하여 사용자에게 맞는 사용자 지정 마이그레이션 계획을 작성하는 것이 좋습니다.  너무 전자 메일을 보내 주십시오[sales@conexlink.com](mailto:sales@conexlink.com)합니다. 
12. Hello 컬렉션 toobe 마이그레이션한은 지켜봅니다 및 자동화 된 솔루션 ARA 컬렉션 및 사용자 프로필 디스크 (선택 사항) toohello 새 구동 MyCloudIT 원격 응용 프로그램 솔루션을 마이그레이션하는 동안 완화를 확인 합니다.
13. 다시 발표 합니다 hello 배포 완료 되 면 hello ARA에 게시 된 동일한 응용 프로그램 및 배포 됩니다. 수 toopublish 추가 응용 프로그램을 게시 합니다.

## <a name="post-migration-benefits"></a>마이그레이션 후 이점

1. 원격 앱 배포 toomanage hello 전체 수명 수 있는 hello 관리 콘솔을 제공 합니다.
2. 포털에서 사용자의 가상 컴퓨터 수 toomanage 됩니다.  필요에 따라 개별 VM을 시작/중지 및 크기 조정합니다.
3. 기능 toocreate hello 및 사용자 관리 hello 관리 콘솔 제공 / 우리의 관리 포털에서 그룹입니다.
4. hello 관리 콘솔 동일한 로그온 환경 hello 기능 toosynchronize 사용자에 게 Office 365 toocreate 제공합니다.
5. hello 관리 콘솔 제공 hello 기능 toocreate 원격 응용 프로그램을 추가 및 중복 된 사용자 비용 또는 최소한의 사용자 요구 사항 없이 데스크톱 컬렉션입니다. 
6. 관리 콘솔 hello hello 기능 toopublish 새 원격 앱 응용 프로그램을 제공합니다.
7. hello 관리 콘솔은 hello 기능 tooschedule hello 시작 및 종료 원격 응용 프로그램 배포의 특정 시간 동안 솔루션만 필요한 경우 제공 합니다.
8. hello 관리 콘솔에는 고객 데이터에 대 한 문서 보존 기록을 제공 하는 hello Azure 백업 에이전트의 hello 기능 tooautomate hello 설치 및 구성을 제공 합니다.
9. hello 관리 콘솔은 배포의 tooperformance 메트릭에 액세스를 제공 합니다.  이렇게 하면 다른 성능 관리 도구를 설치 하지 않고 기능 tooidentify 잠재적인 성능 병목 현상을 hello 됩니다.
10. 여러 세션 호스트를 사용 하도록 설정한 경우 수 tooenable 자동 있도록 hello 세션 toobe 실행 해야 하는 호스트가 실행 되는 확장 됩니다.
11. MyCloudIT은 MyCloudIT 도메인 이름을 통해 액세스 toohello RDWeb 게이트웨이 서버를 제공합니다.  브랜딩 최종 사용자에 대 한 hello 기능 toore 맵 hello URL tooa 사용자 지정 URL도 제공 합니다.

## <a name="prerequisites-for-migration"></a>마이그레이션을 위한 필수 조건

1. 액세스 toohello 현재 Azure RemoteApp 솔루션을 호스팅하는 Azure 구독이 있어야 합니다.
2. 사용 권한을 통해 포털 구독 toomigrate 내에서 템플릿과 toocreate/새 MyCloudIT 배포를 수정 해야 합니다.
3. Azure Remoteapp에서 tooa 제한 인해 각 컬렉션만 마이그레이션할 수 있는지 세 번 note 하십시오.  Toomigrate 컬렉션을 네 번 이상 필요한 경우 티켓 tooAzure tooincrease 내보내기 개수, 발생 하거나 사용자 의견 및 hello ARA 요청 tooincrease hello 내보내기 수에 도움을 받을입니다.

## <a name="mycloudit-billing"></a>MyCloudIT 요금 청구

참조 하십시오 [MyCloudIT RemoteApp 솔루션에 대 한 가격 책정](https://mcitdocuments.blob.core.windows.net/terms/MyCloudIT_Pricing_Overview.pdf) (PDF) 방법에 대 한 toopredict 및 전반적인 Azure 비용을 관리 합니다.

질문이 여전히 있으면 문의해 주십시오 [ sales@conexlink.com ](mailto:sales@conexlink.com) hello 전체 데모 비디오를 시청 하거나 [Azure RemoteApp 마이그레이션 도구 MyCloudIT](https://www.youtube.com/watch?v=YQ_1F-JeeLM&t=482s)합니다. 

