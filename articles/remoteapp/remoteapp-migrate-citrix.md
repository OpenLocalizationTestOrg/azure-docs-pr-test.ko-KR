---
title: "Azure RemoteApp tooCitrix XenApp Essentials에서에서 aaaMigrate | Microsoft Docs"
description: "어떻게 toomigrate Azure RemoteApp tooCitrix XenApp Essentials에서"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 695a8165-3454-4855-8e21-f2eb2c61201b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aa3ce28bc5a86d5b1dd3408196d51935395f55c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-azure-remoteapp-toocitrix-xenapp-essentials"></a>Azure RemoteApp tooCitrix XenApp Essentials에서 마이그레이션

Azure RemoteApp을 사용 중이 고 toomigrate tooCitrix XenApp Essentials, 많은 경우 몇 가지 필수 구성 요소 tookeep 유의 해야 합니다. 먼저 Citrix의 [Citrix XenApp Essentials의 단계별 기술 배포 가이드](https://docs.citrix.com/content/dam/docs/en-us/citrix-cloud/downloads/xenapp-essentials-deployment-guide.pdf) 및 해당 [ 온라인 기술 라이브러리](http://docs.citrix.com/en-us/citrix-cloud/xenapp-and-xendesktop-service/xenapp-essentials.html)를 참고하세요. 

## <a name="prerequisite-steps-for-migration"></a>마이그레이션을 위한 필수 구성 요소 단계

1. 새로운 가상 네트워크를 만들거나 Azure Resource Manager에서 Citrix XenApp Essentials에 배포할 Azure Virtual Network를 결정합니다. Azure 클래식 포털; hello를 사용 하는 azure RemoteApp Citrix XenApp Essentials만 Azure 리소스 관리자를 지원합니다.  
2. Citrix만 하이브리드 배포를 지원 하기 때문에 선택한 hello 가상 네트워크에 액세스 tooyour 도메인 컨트롤러, 네트워킹을 확인 합니다. Azure RemoteApp의 클라우드 배포를 사용 하는 경우 가상 네트워크에 액세스 tooan Active Directory 도메인 컨트롤러를 네트워크에 있는지 확인 합니다. Azure Active Directory Domain Services(Azure AD DS)를 사용할 수도 있습니다. 
3. DNS가 제대로 구성 되어 hello 가상 네트워크에 대 한 도메인 가입 하 여 첫 번째 시도에서 성공한 이므로 해당 hello를 확인 합니다. 선택한 hello 가상 네트워크의 가상 컴퓨터 (VM)를 만들 하 고 해당 hello DNS 수동 도메인 가입 tooverify를 수행할 수 있습니다 및 예상 대로 작동 하는 도메인 가입 합니다. 이렇게 하면는 성공적인 hello 처음 Citrix XenApp Essentials를 배포 합니다. 
4. 필요한 경우 Azure RemoteApp과 함께 사용하는 Azure 클래식 포털 가상 네트워크와 Azure Resource Manager 가상 네트워크간에 가상 네트워크 피어링을 만듭니다. 피어 링이 프로세스가 작동 하는 hello 두 네트워크에에서 들어 있는 경우 hello 동일 지역입니다. 그렇지 않으면 네트워킹에 대 한 사이트 간 VPN tooconnect hello 가상 네트워크를 사용 합니다. 
5. 필요에 따라 읽기 [방법 및 Azure RemoteApp 외부로 toomigrate 데이터](remoteapp-migrate.md)합니다. 
6. 업데이트 하면 기존 Azure RemoteApp 이미지 tooinclude hello Citrix VDA 구성 요소 (자세한 내용은 hello Citrix 설명서 참조). 
7. Azure 마켓플레이스 toohello 이동한 Citrix XenApp Essentials 배포를 시작 합니다.

## <a name="other-considerations"></a>기타 고려 사항

마이그레이션하는 경우 추가로 고려해 야 할 다음 hello 유의 해야 합니다.
- Citrix XenApp Essentials는 하이브리드 배포만 지원합니다. 즉, 순서 tooperform 도메인 가입의 네트워크 액세스 tooa 도메인 컨트롤러가 필요합니다. Azure RemoteApp의 클라우드 배포를 사용 하는 경우 Azure AD DS를 사용 하거나 가상 네트워크에 도메인 가입에 대 한 액세스 tooActive 디렉터리에 있는지 확인 하십시오. 
- toolearn toomove 사용자 데이터 tooCitrix XenApp Essentials 참조 [방법 및 Azure RemoteApp 외부로 toomigrate 데이터](remoteapp-migrate.md)합니다. 
- Citrix XenApp Essentials는 Active Directory 계정만을 지원합니다. Microsoft 계정(예 : outlook.com, msn.com 또는 hotmail.com)은 지원하지 않습니다. 

## <a name="citrix-xenapp-essentials-billing"></a>Citrix XenApp Essentials 청구

가격 책정에 자세한 내용은 참조 hello [FAQ](https://www.citrix.com/global-partners/microsoft/resources/xenapp-essentials-faq.html#tab-30699) 및 [Citrix 개요 문서](https://www.citrix.com/global-partners/microsoft/remote-app.html)합니다. TooCitrix XenApp Essentials는 세 개의 청구 구성 요소:

- hello Citrix 서비스 요금을는 매월 사용자 당 $12입니다. 모든 Azure 마켓플레이스 구매와 같은 Azure 구독에 연결 된 청구 toohello 지불 방법입니다. EA(기업 계약) 고객의 경우 Azure 금액 크레딧을 사용할 수 없습니다. 
- RDS(Remote Data Services) CAL(client access licenses) 현재는 $6.25에 대 한 hello Citrix XenApp Essentials 지불으로 제공 되는 원격 액세스 요금이 hello를 구입할 수 있습니다. EA 고객 인 경우이 대 한 Azure 금액 크레딧 toopay를 사용할 수 있습니다. 기존 RDS Cal toouse 하려는 경우에 게 문의 하세요. [ arainfo@microsoft.com ](mailto:arainfo@microsoft.com)이므로이 tooyour 청구서를 적용할 수 있습니다. 
- Azure 계산 및 저장소 이 hello Azure 저장소 비용 및 계산 소비 hello Vm에 대 한 사용 합니다. VM 크기와 사용자 밀도를 선택할 때 가격 책정에 주의하세요. EA 고객 인 경우이 대 한 Azure 금액 크레딧 toopay를 사용할 수 있습니다.

다른 질문이 있으면:
- [arainfo@microsoft.com](mailto:arainfo@microsoft.com)으로 메일을 보내세요.
- [Azure 지원에 문의하세요](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). 먼저 [Azure 지원 케이스를 열고](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) toohelp 필수 구성 요소와 1-5 단계. 6-7 단계에 대 한 hello Citrix 관리 포털 내에서 지원 티켓을 열어 Citrix에 게 문의 합니다. 
