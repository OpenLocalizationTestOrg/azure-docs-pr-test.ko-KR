---
title: "Azure 앱 서비스와 ClearDB MySql 데이터베이스에 대 한 aaaFAQ | Microsoft Docs"
description: "Azure 앱 서비스와 ClearDB MySQL 데이터베이스 사용에 대 한 toocommon 질문에 답변 합니다."
documentationcenter: php
services: 
author: sunbuild
manager: yochayk
editor: 
tags: mysql
ms.assetid: c2ed5e78-6d7d-4d0c-b7ee-a52ae41ceab8
ms.service: multiple
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/27/2016
ms.author: sumuth
ms.openlocfilehash: 3d9c9daca2b845ede8d3a1fdadefa7e668d62dee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="faq-for-cleardb-mysql-databases-with-azure-app-service"></a>Azure 앱 서비스를 사용하는 ClearDB MySQLl 데이터베이스에 대한 FAQ
이 FAQ는 Azure 웹앱용 ClearDB MySQL 데이터베이스의 사용 및 구매에 대한 일반적인 질문에 답변합니다.

## <a name="what-options-do-i-have-for-mysql-on-azure"></a>Azure에서 MySQL을 사용하려면 어떤 옵션이 필요한가요?
여러 옵션이 있습니다.

* [ClearDB 공유 MySQL 데이터베이스](/marketplace/partners/cleardb/databases/)
* [ClearDB MySQL 프리미엄 클러스터](/marketplace/partners/cleardb-clusters/cluster/)
* [Azure VM에서 실행되는 MySQL 클러스터](https://github.com/azure/azure-quickstart-templates/tree/master/mysql-replication)
* [Azure VM에서 실행되는 MySQL의 단일 인스턴스](virtual-machines/windows/classic/mysql-2008r2.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

ClearDB은 MySQL 서비스를 호스트 하는 및에서 hello MySQL 인프라를 관리 합니다. Azure 가상 컴퓨터에서 MySQL 클러스터 나 데이터베이스에 직접 실행 하면 tooset hello MySQL 서버를에 있고 지속적으로 업데이트 패치를 사용 합니다.

## <a name="do-i-need-a-credit-card-for-hello-web-app--mysql-template-in-hello-azure-marketplace"></a>신용 카드 hello 웹 응용 프로그램 + hello Azure Marketplace에서에서 MySQL 서식 파일에 대 한 필요 합니까?
이 구독에 사용 하는 hello 유형에 따라 다릅니다. 다음은 일반적으로 사용되는 구독 유형입니다.

* [종량제](/offers/ms-azr-0003p/): 신용 카드가 필요하며 유료 MySQL 데이터베이스를 구매하는 경우 신용 카드로 요금이 청구됩니다.
* [무료 평가판](https://azure.microsoft.com/pricing/free-trial/): Microsoft Azure 서비스에서 사용할 크레딧이 포함되어 있지만 타사 리소스의 구매에는 사용할 수 없습니다. toopurchase 제 3 자 서비스 또는 신용 카드 toouse 필요한 유료 MySQL 데이터베이스 구독을 사용할 수 있습니다. Web Apps의 경우 무료 ClearDB MySQL 데이터베이스를 만들 수 있습니다.
* [MSDN 구독이](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/) 및 **MSDN 개발 테스트 사용량 기준 과금 방식의**: 유사한 tooFree 평가판, MSDN 구독이 toohave 신용 카드 toopurchase ClearDB의 MySQL 솔루션 유료 필요 합니다.
* [EA(기업계약)](https://azure.microsoft.com/pricing/enterprise-agreement/): EA 고객은 Azure Marketplace(타사)에서 구매한 모든 제품에 대해 EA 분기별로 별도의 통합 청구서로 청구됩니다. 마켓플레이스 구매에 대 한 현금 약정 hello 외부 청구 됩니다. 유의 사항:,이 이번에, Azure 저장소를 사용할 수 있는 toocustomers 아제르바이잔, 크로아티아, 노르웨이 및 푸에르토리코에 등록 없습니다. 
* [DreamSpark](https://www.dreamspark.com/Product/Product.aspx?productid=99): 웹앱용 무료 ClearDB 데이터베이스만 만들 수 있습니다. Hello 다양 한 무료 ClearDB MySQL 데이터베이스를 만들 수 있습니다에 제한은 없습니다. 무료 데이터베이스 없는지 toobe 프로덕션 웹 앱에 사용 되는 평가판에 대 한이 서비스는 의도 한 대로 참고 합니다.

## <a name="why-was-i-charged-350-for-a-web-app--mysql-from-hello-azure-marketplace"></a>$3.50 웹 응용 프로그램 + MySQL에 대 한 hello Azure Marketplace에서에서 왜 요금이 청구 되었나요?
hello 기본 데이터베이스 옵션에는 $3.50 탄입니다. 데이터베이스를 만드는 동안 hello 비용을 표시 하지 않으려면 및 의도 하지 않았던 데이터베이스를 실수로 구입할 수 있습니다. Toofind 방식으로 tooimprove hello 경험 중 되지만 그때 까지는 클릭 하기 전에 모든 사용자 선택한 가격 책정 계층 웹 응용 프로그램 및 데이터베이스에 대 한 확인 해야 **만들기** hello 리소스의 hello 배포를 시작 합니다.

## <a name="i-am-running-mysql-on-my-own-azure-virtual-machine-can-i-connect-my-azure-web-app-toomy-database"></a>Azure 가상 컴퓨터에서 MySQL을 실행하고 있습니다. 내 Azure 웹 앱 toomy 데이터베이스를 연결할 수 있습니까?
예. Azure VM에 원격 액세스 tooyour 웹 응용 프로그램 지정으로 웹 앱 tooyour 데이터베이스를 연결할 수 있습니다. 자세한 내용은 [가상 컴퓨터에 MySQL 설치](virtual-machines/windows/classic/mysql-2008r2.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)를 참조하세요.

## <a name="in-which-countries-are-cleardb-premium-mysql-clusters-supported"></a>ClearDB 프리미엄 MySQL 클러스터가 지원되는 국가는 어디인가요?
[ClearDB 프리미엄 MySQL 클러스터](/marketplace/partners/cleardb-clusters/cluster/) 인도, 오스트레일리아, 브라질 남쪽 및 중국의 hello 예외와 함께 전 세계 모든 Azure 지역에서 사용할 수 있는 합니다.

## <a name="can-i-create-a-new-cluster-prior-toocreating-a-database-with-cleardb-premium-cluster-solution"></a>만들기는 새 클러스터 이전 toocreating 데이터베이스 ClearDB 프리미엄 클러스터 솔루션과
아니요, 빈 ClearDB 클러스터 만들기는 지원되지 않습니다. hello Azure 포털 있습니다 toocreate 데이터베이스 hello에서 새 클러스터를 만들 수 있는 클러스터에서 같은 시간입니다.

## <a name="will-i-be-warned-if-i-try-toodelete-a-cleardb-mysql-database-that-is-in-use-by-one-of-my-applications"></a>I 경고가 표시 됩니다 내 응용 프로그램 중 하나에 의해 toodelete ClearDB MySQL 데이터베이스 사용 중인 있나요?
아니요, 응용 프로그램이 사용하고 있는 마켓플레이스 구매 제품을 삭제할 경우 Azure는 경고를 표시하지 않습니다.

## <a name="which-regions-can-i-create-cleardb-databases-in"></a>어떤 지역에서 ClearDB 데이터베이스를 만들 수 있나요?
Azure 마켓플레이스를 사용할 수 있는 toocustomers 아제르바이잔, 크로아티아, 노르웨이 또는 푸에르토리코에 등록 없습니다. 이러한 지역에서는 ClearDB를 사용할 수 없습니다.

## <a name="what-pricing-tier-should-i-choose-for-a-production-web-app-and-database"></a>프로덕션 웹앱 및 데이터베이스에 대해 어떤 가격 책정 계층을 선택해야 하나요?
웹앱의 경우 기본이나 더 높은 가격 책정 계층을 사용합니다. ClearDB의 경우 Saturn 또는 Jupiter 플랜을 사용하는 것이 좋습니다. Hello 기능 및 모두에 대 한 각 가격 책정 계층의 제한 사항 검토 [웹 앱](https://azure.microsoft.com/pricing/details/app-service/) 및 [ClearDB MySQL 데이터베이스](/marketplace/partners/cleardb/databases/) toochoose hello 요구 사항에 맞는 합니다.

## <a name="how-do-i-upgrade-my-cleardb-database-from-one-plan-tooanother"></a>하나의 계획 tooanother에서 내 ClearDB 데이터베이스를 업그레이드 하려면 어떻게 합니까?
Hello에 [Azure 포털](https://portal.azure.com), ClearDB 공유 호스팅 데이터베이스를 확장할 수 있습니다. 이 내용을 읽고 [문서](https://blogs.msdn.microsoft.com/appserviceteam/2016/10/06/upgrade-your-cleardb-mysql-database-in-azure-portal/) toolearn 더 합니다. 현재 hello Azure 포털의에서 ClearDB 프리미엄 클러스터에 대 한 업그레이드가 지원 되지 않습니다.

## <a name="i-cant-see-my-cleardb-database-in-azure-portal"></a>Azure Portal에서 내 ClearDB 데이터베이스를 볼 수 없나요?
Azure 리소스 관리자를 사용 하 여 ClearDB 데이터베이스를 만들면 또는 [새 Azure 포털](https://portal.azure.com), hello에 표시 되지 것입니다 [이전 Azure 포털](https://manage.windowsazure.com)합니다. toowork-이 toolink 데이터베이스 수동으로 toohello 웹 앱입니다. 마찬가지로 경우 hello에 ClearDB 데이터베이스를 만들 [이전 포털](https://manage.windowsazure.com) 할 수 없는 수 toosee hello에서 데이터베이스 수 [새 Azure 포털](https://portal.azure.com)합니다. 없는 해결 hello 두 번째 시나리오에 있습니다.

## <a name="who-do-i-contact-for-support-when-my-database-is-down"></a>데이터베이스가 다운되었을 때 지원을 받으려면 누구에게 문의해야 하나요?
데이터베이스 관련 문제에 대해서는 [ClearDB 지원](https://www.cleardb.com/developers/help/support) 에 문의하세요. Tooprovide 준비 Azure 구독 정보를 사용 하 여 합니다.

## <a name="can-i-create-additional-users-for-my-cleardb-mysql-database-cluster-solution"></a>ClearDB MySQL 데이터베이스 클러스터 솔루션에 대한 추가 사용자를 만들 수 있나요?
아니요. 추가 사용자를 만들 수는 없지만 ClearDB 데이터베이스 클러스터에서 추가 데이터베이스를 만들 수 있습니다.  

## <a name="can-basicpro-series-databases-be-upgraded-in-place-similar-tooplanetary-plans-today-on-cleardb-portal"></a>Basic/Pro 시리즈 데이터베이스 업그레이드 된 전체 비슷한 tooPlanetary 계획 ClearDB 포털에 오늘 수 있습니까?
예, Basic 시리즈 데이터베이스는 전체 업그레이드(Basic 60 ~ Basic 500)할 수 있습니다. Pro 시리즈는 Pro 60을 제외하고 전체 업그레이드(Pro 125 ~ Pro 1000)할 수 있습니다. 현재 Pro 60 데이터베이스 업그레이드는 지원되지 않습니다. 

## <a name="when-i-migrate-my-resources-from-one-subscription-tooanother-does-my-cleardb-mysql-database-get-migrated-as-well"></a>하나의 구독 tooanother에서 내 리소스를 마이그레이션할 I 때 ClearDB MySQL 데이터베이스 마이그레이션되지는?
구독 간에 리소스 마이그레이션을 수행할 때 일부 [제한 사항](app-service-web/app-service-move-resources.md) 이 적용됩니다. ClearDB MySQL 데이터베이스는 타사 서비스이므로 Azure 구독 마이그레이션 중에 마이그레이션되지 않습니다. MySQL 사용자의 hello 마이그레이션을 관리 하지 않는 경우 이전 toomigrating Azure 데이터베이스 리소스에 프로그램 ClearDB MySQL 데이터베이스를 비활성화할 수 있습니다. 먼저 수동으로 데이터베이스를 마이그레이션한 다음 웹앱에 대한 Azure 구독 마이그레이션을 수행합니다. 

## <a name="i-hit-hello-spending-limit-on-my-subscription-i-removed-hello-limit-and-my-app-service-is-online-however-hello-database-is-not-accessible-how-do-i-re-enable-hello-cleardb-database"></a>I hello 내 구독에 지출 한도 도달 했습니다. Hello 제한 사라지고 내 응용 프로그램 서비스 이지만 온라인으로 hello 데이터베이스를 액세스할 수 없습니다. 다시 hello ClearDB 데이터베이스를 사용 하는 방법
연락처 [ClearDB 지원](https://www.cleardb.com/developers/help/support) toore 사용 hello 데이터베이스입니다. Azure 구독 정보와 데이터베이스 이름을 제공합니다.

## <a name="can-i-transfer-a-cleardb-database-from-a-credit-card-subscription-tooan-ea-subscription"></a>신용 카드 구독 tooan EA 구독에서 ClearDB 데이터베이스를 전송할 수 있습니까?
기존 ClearDB 데이터베이스 hello 기존 구독과 연결 된 hello 신용 카드를 사용 합니다. toouse toomigrate 데이터 tooa 새 데이터베이스를 두어야 하는 EA 구독:

* EA 구독으로 새 ClearDB 데이터베이스를 구매합니다.
* 데이터 tooyour 새 데이터베이스를 마이그레이션하십시오.
* 응용 프로그램 toouse hello 새 데이터베이스를 업데이트 합니다.
* 이전 ClearDB 데이터베이스를 삭제합니다.

MySQL (ClearDB)와 새 웹 앱을 만들거나 (ClearDB) MySQL 데이터베이스 만들기, 선택한 hello 구독 hello 서비스에 대 한 지불 방법을 결정 합니다. EA 구독과 म hello Azure 포털에서에서 ClearDB 같은 hello 공급 업체 서비스의 조달 hello 차단 하지 않습니다. EA 구독은 현금 약정 금액과 별도로 청구되며 분기별로 체납 청구됩니다. hello EA 고객 모든 공급 업체 마켓플레이스 서비스에 대 한 신용 카드 toopay 같은 지불 방법을를 tooset을 것입니다.

## <a name="where-can-i-see-hello-charges-for-cleardb-resources-in-an-ea-subscription"></a>EA 구독에서 ClearDB 리소스에 대 한 hello 요금 보기
직접 EA 고객에 대 한 Azure 마켓플레이스 요금 hello 엔터프라이즈 포털에 표시 됩니다. 마켓플레이스에서 구매한 모든 제품 및 사용량 과금은 현금 약정 금액과 별도로 청구되며 분기별로 체납 청구됩니다. EA 고객 toohello 타사 서비스 공급자 수 수행 하므로 해당 EA와 신용 카드와 같은 지불 방법을 사용 하 여 계정 및 직접 toopay를 해야 합니다.

간접 EA 고객 hello에서 자신의 Azure 마켓플레이스 구독을 찾을 수 **구독 관리** hello Enterprise Portal 하지만 가격 책정 페이지 숨겨집니다. 고객은 마켓플레이스 요금에 대한 내용을 LSP에 문의해야 합니다.

타사 서비스에 대 한 액세스 tooAzure 마켓플레이스 EA Azure 등록 관리자가 관리할 수 있습니다. 사용 하지 않도록 설정 하거나 다시 hello 계정 섹션 hello Enterprise Portal에서에서 관리 계정 및 구독에서 저장소 hello에서 액세스 too3rd 파티 구매를 활성화할 수 있습니다.

## <a name="who-do-i-contact-for-questions-about-my-bill-for-cleardb-services-in-my-ea-subscription"></a>EA 구독의 ClearDB 서비스의 요금에 대한 질문이 있는 경우 누구에게 문의해야 하나요?
연락처 [엔터프라이즈 고객 지원](http://aka.ms/AzureEntSupport) 관련해 서 toobilling 자신의 EA 등록에서 사용 합니다. hello EA 포털 지원 팀이 질문에 대답 되거나 문제를 해결 하는 데 도움이 됩니다.

## <a name="more-information"></a>자세한 정보
[Azure 마켓플레이스 FAQ](/marketplace/faq/)

