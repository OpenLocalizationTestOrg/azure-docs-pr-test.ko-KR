---
title: "aaaMicrosoft Azure 데이터--휴지 암호화 | Microsoft Docs"
description: "이 문서에서는 Microsoft Azure 데이터 암호화에 간략하게 설명에서 rest, 전반적인 기능 및 일반적인 고려 사항을 hello 합니다."
services: security
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: TomSh
ms.assetid: 9dcb190e-e534-4787-bf82-8ce73bf47dba
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: yurid
ms.openlocfilehash: d74d103e4fd7585543b4f039877af7d742a6b2e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-encryption-at-rest"></a>Azure 미사용 데이터 암호화
Tooyour 회사의 보안 및 규정 준수 요구 사항에 따라 Microsoft Azure toosafeguard 데이터 내에서 여러 도구가 있습니다. 이 문서는 데이터를 Microsoft Azure 전체에서 저장 된 상태의 보호, hello hello 데이터를 보호 하는 구현에 참여 하는 다양 한 구성 요소에 설명와 hello 다른 키 관리 보호 방법의 장점과 단점을 검토 하 방법을 중점을 둡니다. 

미사용 데이터 암호화는 일반적인 보안 요구 사항입니다. Microsoft Azure의 이점은 조직이 구현의 hello 비용 및 사용자 지정 키 관리 솔루션의 관리 및 hello 위험 필요 없이 미사용 데이터 암호화를 얻을 수입니다. 조직에는 Azure을 미사용 데이터 암호화를 완전히 관리할 수 있도록 hello 옵션이 제공 됩니다. 또한 조직에서는 암호화 또는 암호화 키를 관리 하는 다양 한 옵션 tooclosely가 있어야 합니다.

## <a name="what-is-encryption-at-rest"></a>미사용 데이터 암호화란?
휴지 암호화 toohello 암호화 (암호화) 데이터의 인코딩을 유지 될 때 참조 합니다. hello 암호화 Azure의 Rest 디자인에 tooencrypt 대칭 암호화를 사용 하 여 및 많은 양의 데이터를 신속 하 게 tooa 간단한 개념 모델에 따라 암호 해독:

- 대칭 암호화 키를 유지 될 때 사용 되는 tooencrypt 데이터는 
- 동일한 암호화 키를 hello 메모리에서 사용 하기 위해 준비 하는 것 처럼 사용 되는 toodecrypt 데이터는
- 데이터는 분할될 수 있고, 각 파티션마다 다른 키가 사용될 수 있다.
- 키는 액세스 toocertain id 및 로깅 키 사용을 제한 하는 액세스 제어 정책을 사용 하 여 안전한 위치에 저장 되어야 합니다. 데이터 암호화 키는 종종 암호로 암호화 된 비대칭 암호화 toofurther 액세스 제한 (hello에 설명 된 *키 계층*이 문서의 뒷부분에 나오는)

위의 hello 미사용 데이터 암호화의 hello 공통 상위 수준 요소를 설명합니다. 실제로 확장성과 가용성 보장뿐만 아니라 키 관리 및 제어 시나리오에는 추가 구성이 필요합니다. Microsoft Azure 미사용 데이터 암호화의 개념 및 구성 요소에 대해서는 아래에서 설명합니다.

## <a name="hello-purpose-of-encryption-at-rest"></a>휴지 암호화의 hello 용도
미사용 데이터 암호화가 나머지에서 데이터에 대 한 의도 한 tooprovide 데이터 보호 (위에 설명 된 대로.) Rest에서 데이터에 대 한 공격 시도 tooobtain 물리적으로 액세스 toohello 하드웨어는 hello에 데이터가 저장 되 등 손상 hello 데이터를 포함 합니다. 이러한 공격에 공격자가 tooremove hello 하드 드라이브는 유지 관리 하는 동안 서버의 하드 드라이브 신망을 수 있습니다. 이후 hello 공격자가 hello 하드 드라이브에서 제어 tooattempt tooaccess hello 데이터를 컴퓨터에 추가 됩니다. 

휴지 암호화 hello 디스크에 있는 경우 데이터는 암호화 되도록 하 여 hello 암호화 되지 않은 데이터에 액세스 하지 못하도록 설계 된 tooprevent hello 공격자가입니다. 공격자가 있는 경우 tooobtain 등 포함 된 하드 드라이브에 암호화 된 데이터 및 액세스 toohello 암호화 키, hello 공격자가 어려움을 겪고 없이 hello 데이터 손상 시 키 지 합니다. 이러한 시나리오는 것이 훨씬 더 복잡 한 암호화 된 데이터에 대 한 tooattempt 공격 및 암호화 되지 않은 하드 드라이브에 데이터를 액세스할 때 보다 리소스 소비 합니다. 이러한 이유로 미사용 데이터 암호화는 적극적으로 권장되며 많은 조직에서 우선 순위가 높은 요구 사항입니다. 

경우에 따라 데이터 거버넌스 및 규정 준수 노력에 대한 조직의 요구 사항에 따라 미사용 데이터 암호화도 필요합니다. HIPAA, PCI 및 FedRAMP와 같은 산업 및 정부 규정 및 국제 규정 요구 사항은 데이터 보호 및 암호화 요구 사항과 관련된 프로세스 및 정책을 통해 특정 보호 기능을 배치하고 있습니다. 이러한 규정 중 대다수에는 미사용 데이터 암호화가 규정 준수 데이터 관리 및 보호에 필수적인 조치입니다. 

또한 toocompliance 및 규정 요구 사항 미사용 데이터 암호화는 심층적인 방어 플랫폼 기능으로 인식 해야 합니다. Microsoft 응용 프로그램, 서비스에 대 한 규정을 준수 하는 플랫폼을 제공 하 고 데이터 액세스 제어 및 감사 데이터, 포괄적인 시설 및 물리적 보안을 중요 한 tooprovide 추가 "겹치는" 보안 조치 hello 중 하나는 경우에는 다른 보안 실패를 측정합니다. 미사용 데이터 암호화는 이러한 추가적인 방어 메커니즘을 제공합니다.

Microsoft는 클라우드 서비스와의 암호화 키 및 암호화 키가 사용 될 때 표시 되는 액세스 toologs tooprovide 고객 적합 한 관리에서 나머지 옵션에서 커밋된 tooproviding 암호화 합니다. 또한 Microsoft는 모든 고객 데이터를 기본적으로 암호화 된 상태로 만드는 hello 목표 협력 합니다.

## <a name="azure-encryption-at-rest-components"></a>Azure 미사용 데이터 암호화의 구성 요소

앞에서 설명한 대로 hello 미사용 데이터 암호화의 ´ ֲ 디스크에 유지 되는 데이터는 암호화 키로 암호화 됩니다. tooachieve 그 목표에 해당 보안 키 생성, 저장소, 액세스 제어 및 관리 hello 암호화 키를 제공 해야 합니다. 세부 정보는 다를 수 있지만 Rest 구현에서 Azure 서비스 암호화는 다음 hello 다음 다이어그램에에서 나와 있는 개념 아래 hello 설명할 수 있습니다.

![구성 요소](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig1.png)

### <a name="azure-key-vault"></a>Azure 키 자격 증명 모음

hello 암호화 키 및 액세스 제어 toothose 키의 hello 저장소 위치는 rest 모델에서 중앙 tooan 암호화입니다. hello 키 toobe 지정 된 사용자와 사용 가능한 toospecific 서비스에서 관리할 수 있지만 높은 수준의 보안이 필요 합니다. Azure 서비스에 대 한 Azure 키 자격 증명 모음 이며 hello 권장 키 저장소 솔루션 서비스 전반에 걸쳐 공통적인 관리 환경을 제공 합니다. 키를 저장 및 키 자격 증명 모음에서 관리 및 toousers 또는 서비스 액세스 tooa 키 자격 증명 모음을 지정할 수 있습니다. Azure Key Vault는 고객이 관리하는 암호화 키 시나리오에서 사용할 고객 키 생성 또는 고객 키 가져오기를 지원합니다.

### <a name="azure-active-directory"></a>Azure Active Directory

사용 권한 toouse hello 키에 저장 된 Azure 키 자격 증명 모음의 toomanage 또는 tooaccess에 암호화에 대 한 Rest 암호화 및 암호 해독, tooAzure Active Directory 계정을 지정할 수 있습니다. 

### <a name="key-hierarchy"></a>키 계층 구조

일반적으로 하나 이상의 암호화 키가 미사용 데이터 암호화 구현에 사용됩니다. 비대칭 암호화는 hello 트러스트 및 키 액세스 및 관리에 필요한 인증을 설정 하는 데 유용 합니다. 대칭 암호화는 대량 암호화 및 암호 해독에 더 효율적이므로 더 강력한 암호화 및 더 나은 성능을 제공합니다. 또한 단일 암호화 키 감소 키 hello hello 위험이 손상 및 비용을 재 암호화 키를 교체 해야 하는 경우 hello hello 사용을 제한 합니다. 대칭 및 비대칭 암호화 및 hello 사용 제한의 tooleverage hello 이점 및 단일 키의 노출을 rest 모델에서 Azure 암호화 키 유형만 hello 구성 키 계층에서는 사용:

- **데이터 암호화 키 (DEK)** – 파티션 또는 데이터 블록을 tooencrypt AES256 대칭 키에 사용 합니다.  단일 리소스에는 많은 파티션과 많은 데이터 암호화 키가 있을 수 있습니다. 서로 다른 키로 각 데이터 블록을 암호화하면 암호 분석 공격이 더욱 어려워집니다. 액세스 tooDEKs hello 리소스 공급자 또는 응용 프로그램 인스턴스에 의해 암호화 되 고 특정 블록을 암호 해독 필요 합니다. DEK를 새 키로 바뀔 때만 hello의 데이터는 연결 된 블록 이어야 합니다 hello 새 키로 다시 암호화 합니다.
- **암호화 키 KEK (키)** – 비대칭 암호화 키 tooencrypt hello 데이터 암호화 키를 사용 합니다. 키 암호화 키를 사용 하 여 hello toobe 암호화 되 고 제어 자체 데이터 암호화 키를 수 있습니다. hello 있는 엔터티를 액세스 toohello KEK hello DEK 필요한 hello 엔터티에 보다 달라질 수 있습니다. 이렇게 하면 한 엔터티 toobroker 액세스 toohello DEK hello 목적 각 DEK toospecific 파티션의 제한 된 액세스를 확인 합니다. Hello KEK 필요한 toodecrypt hello Dek 이므로 hello KEK는 사실상 기준인 Dek 효과적으로 삭제할 수 삭제 hello KEK의 단일 지점입니다.

hello 키 암호화 키로 암호화 된 hello 데이터 암호화 키를 별도로 저장 하 고 해당 키로만 액세스 toohello 키 암호화 키에서 모든 데이터 암호화 키를 얻을 수 있는 엔터티 암호화 키를 누릅니다. 다양한 키 저장소 모델이 지원됩니다. 각 모델에 hello 다음 섹션의 뒷부분에서 자세히 설명 합니다.

## <a name="data-encryption-models"></a>데이터 암호화 모델

이해 hello 다양 한 암호화 모델 및의 장단점 반드시 이해 Azure 구현 미사용 데이터 암호화에 다양 한 리소스 공급자를 어떻게 hello에 대 한 합니다. 이러한 정의 Azure tooensure 공용 언어 및 분류에 모든 리소스 공급자에서 공유 됩니다. 

서버 쪽 암호화에는 다음 세 가지 시나리오가 있습니다.

- 서비스 관리 키를 사용하여 서버 쪽 암호화
    - Hello 암호화 및 암호 해독 작업을 수행 하는 azure 리소스 공급자
    - Microsoft은 hello 키를 관리합니다.
    - 전체 클라우드 기능

- Azure Key Vault에서 고객 관리 키를 사용하여 서버 쪽 암호화
    - Hello 암호화 및 암호 해독 작업을 수행 하는 azure 리소스 공급자
    - 고객이 Azure Key Vault를 통해 키 제어
    - 전체 클라우드 기능

- 고객 제어 하드웨어에서 고객 관리 키를 사용하여 서버 쪽 암호화
    - Hello 암호화 및 암호 해독 작업을 수행 하는 azure 리소스 공급자
    - 고객이 고객 제어 하드웨어에서 키 제어
    - 전체 클라우드 기능

클라이언트 쪽 암호화 hello 다음을 고려해 보십시오.

- Azure 서비스에서 암호 해독된 데이터를 볼 수 없음
- 고객이 온-프레미스(또는 다른 보안 저장소)에서 키 관리 및 저장 - 키는은 사용할 수 있는 tooAzure 서비스 하지 않습니다.
- 제한된 클라우드 기능

두 기본 그룹으로 분할 하는 Azure에서 지원 되는 hello 암호화 모델: "클라이언트 암호화" 및 "서버 쪽 암호화"로 앞에서 언급 한 합니다. 즉, hello 암호화 rest 모델에 관계 없이 사용 되는, Azure 서비스 항상 권장 TLS 또는 HTTPS와 같은 보안 전송 사용 하 여 hello 참고 합니다. 따라서 전송에서 암호화 hello 전송 프로토콜에서 해결 해야 할 나머지 모델 toouse 어떤 암호화를 결정 하는 주요 요소가 아니어야 합니다.

### <a name="client-encryption-model"></a>클라이언트 쪽 암호화 모델

클라이언트 암호화 모델 tooencryption hello 서비스 또는 호출 응용 프로그램에서 hello 리소스 공급자 또는 Azure 외부에서 수행 하는 참조 합니다. Azure의 hello 서비스 응용 프로그램 또는 hello 고객 데이터 센터에서 실행 중인 응용 프로그램이 hello 암호화를 수행할 수 있습니다. 두 경우 모두이 암호화 모델을 활용 하는 경우, hello Azure 리소스 공급자 어떤 식으로든에서 hello 기능 toodecrypt hello 데이터 없이 데이터의 암호화 된 blob을 받거나 액세스 toohello 암호화 키가 있습니다. 이 모델에서는 hello 키 관리 서비스/응용 프로그램을 호출 하는 hello에서 수행 되 고은 완전히 불투명 toohello Azure 서비스입니다.

![클라이언트](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig2.png)

### <a name="server-side-encryption-model"></a>서버 쪽 암호화 모델

서버 쪽 암호화 모델 tooencryption hello Azure 서비스에서 수행 하는 참조 하십시오. 해당 모델에서 리소스 공급자 hello 수행 hello 암호화 및 해독 작업 합니다. 예를 들어 Azure 저장소는 일반 텍스트 작업에 데이터를 받을 수 있습니다 및 수행될지 hello 암호화 및 암호 해독 내부적으로 합니다. hello 리소스 공급자 구성을 제공 하는 hello에 따라 hello 고객 또는 Microsoft에서 관리 되는 암호화 키를 사용할 수 있습니다. 

![서버](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig3.png)

### <a name="server-side-encryption-key-management-models"></a>서버 쪽 암호화 키 관리 모델

각 rest 모델 hello 서버 쪽 암호화 키 관리의 고유한 특성을 의미합니다. 이 포함 됩니다 하 고 암호화 키 생성, 되 고 저장 하는 방법으로 hello 액세스 모델 및 키 회전 프로시저 hello 합니다. 

#### <a name="server-side-encryption-using-service-managed-keys"></a>서비스 관리 키를 사용하여 서버 쪽 암호화

많은 고객에 대 한 hello 필수 요구는 데이터 hello tooensure는 않든 때마다 암호화 됩니다. 서비스 관리 키를 사용 하 여 서버 쪽 암호화 암호화에 대 한 고객 toomark hello 특정 리소스 (저장소 계정, SQL DB, 등)를 허용 하 고 키 발급, 회전 및 백업 등의 모든 키 관리 측면을 그대로 두고 여이 모델이 가능 tooMicrosoft 합니다. 대부분의 Azure 서비스는 일반적으로 미사용 데이터 암호화를 지 원하는 hello 관리 hello 암호화 키 tooAzure의 오프 로드의이 모델을 지원 합니다. hello Azure 리소스 공급자 hello 키를 만들고 하 고, 보안 저장소에 배치, 필요할 때 검색 합니다. Hello 서비스에 대 한 모든 권한을 toohello 키 및 hello 서비스는 hello 자격 증명 수명 주기 관리에 대 한 모든 권한을 의미 합니다.

![관리](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig4.png)

따라서 신속 하 게 관리 서비스 키를 사용 하는 서버 쪽 암호화 hello 필요 toohave 미사용 데이터 암호화 낮은 오버 헤드 toohello 고객을 해결 합니다. 사용 가능한 경우 고객 일반적으로 hello hello 대상 구독 및 리소스 공급자에 대 한 Azure 포털 열리고 암호화 hello 데이터 toobe 만족할 만한 나타내는 상자를 확인 합니다. 일부 리소스 관리자에서는 기본적으로 서비스 관리 키를 사용하는 서버 쪽 암호화가 설정되어 있습니다. 

Microsoft 관리 키를 사용 하 여 서버 쪽 암호화 hello 서비스에 대 한 모든 권한을 toostore 키 및 관리 hello 의미는 않습니다. 강화 된 보안을 방지할 수 우려 때문에 일부 고객 toomanage hello 키를 사용할 수 있습니다, 동안 hello 비용 및 사용자 지정 키 저장소 솔루션과 관련 된 위험 때 고려해 야이 모델을 평가 합니다. 대부분의 경우에는 조직 리소스 제약 조건 또는 온-프레미스 솔루션의 위험 hello 나머지 키 암호화의 클라우드 관리 hello 위험 보다 큰 수를 결정할 수 있습니다.  그러나이 모델 요구 사항 toocontrol hello 만들기를 적용 하는 조직에 대 한 충분 한 수 없거나 (예: hello 서비스를 관리 하는 것 보다는 서비스의 암호화 키를 관리 하는 hello 암호화 키 또는 toohave 다른 사용자의 수명 주기 키 관리 hello에서의 분리 hello 서비스에 대 한 전반적인 관리 모델).

##### <a name="key-access"></a>키 액세스

서비스 관리 키가 있는 서버 쪽 암호화를 사용 하는 경우 키 생성 hello hello 서비스에서 관리 저장소 및 서비스 액세스 됩니다. 일반적으로 hello 기본 Azure 리소스 공급자 toohello 데이터를 닫고 신속 하 게 사용 가능 하 고 hello 키 암호화 키 하는 동안 액세스할 수 있는 보안는 내부 저장소에 저장 되어 있는 저장소에 hello 데이터 암호화 키를 저장 합니다.

**장점**

- 간단한 설정
- Microsoft에서 키 회전, 백업 및 중복성을 관리합니다.
- 고객에 없는 사용자 지정 키 관리 구성표의 위험 구현 또는 hello와 관련 된 비용을 hello 합니다.

**단점**

- 고객을 제어할 hello 암호화 키 (키 사양, 수명 주기, 해지 등)
- Hello 서비스에 대 한 전반적인 관리 모델에서 없음 기능 toosegregate 키 관리

#### <a name="server-side-encryption-using-customer-managed-keys-in-azure-key-vault"></a>Azure Key Vault에서 고객 관리 키를 사용하여 서버 쪽 암호화 

경우에 hello 요구 사항은 저장 된 상태의 tooencrypt hello 데이터 제어 hello 암호화 키 고객 고객 관리 키를 사용 하 여 주요 자격 증명 모음에 서버 쪽 암호화를 사용할 수 있습니다. 일부 서비스의 Azure 키 자격 증명 모음에만 hello 루트 키 암호화 키를 저장할 수 있습니다 및 저장소 hello 내부 위치 가까이 toohello 데이터에서 데이터 암호화 키를 암호화 합니다. 에 시나리오 고객의 직접 가져올 수 tooKey (BYOK – Bring Your 고유 키), 자격 증명 모음 키 또는 새 키를 생성 하 고 tooencrypt hello 필요한 리소스를 사용 합니다. 리소스 공급자 hello hello 암호화 및 암호 해독 작업을 수행 하는 동안 모든 암호화 작업에 대 한 hello 루트 키로 구성 된 hello 키를 사용 합니다. 

##### <a name="key-access"></a>키 액세스

hello Azure 키 자격 증명 모음에서 고객이 관리 키를 사용 하 여 서버 쪽 암호화 모델에서는 hello 서비스 액세스 방법 hello 키 tooencrypt 및 필요에 따라 암호를 해독 합니다. 나머지 키 암호화에는 해당 서비스 id 액세스 tooreceive hello 키 부여의 액세스 제어 정책을 통해 액세스할 수 있는 tooa 서비스를 수행 됩니다. 연결된 구독을 대신하여 실행되는 Azure 서비스는 해당 구독 내에서 해당 서비스에 대한 ID로 구성할 수 있습니다. hello 서비스는 Azure Active Directory 인증을 수행 하 고 해당 서비스를 대신 하 여 hello 구독으로 자신을 식별 하는 인증 토큰을 받을 수 있습니다. 발표 된 tooKey 자격 증명 모음 키를 tooobtain 될 것에 부여 된에 대 한 액세스 토큰 수 수. 있습니다

암호화 키를 사용 하 여 작업을 위해 서비스 id를 얻을 수의 작업을 수행 하는 hello 액세스 tooany: 암호 해독, 암호화, unwrapKey, wrapKey, 확인, 서명, 가져오기, 목록, 업데이트, 만들기, 가져오기, 삭제, 백업 및 복원 합니다.

tooobtain 암호화 또는 해당 hello (tooget hello 키 암호 해독을 위해) UnwrapKey, WrapKey (tooinsert 주요 자격 증명 모음 새 키를 만들 때에 키)를가지고 있어야 서비스 인스턴스를 실행 하는 리소스 관리자 rest hello 서비스 id에서 데이터를 암호 해독에 사용할 키입니다.


>[!NOTE] 
>주요 자격 증명 모음에 대 한 세부 권한 부여 참조 hello에서 주요 자격 증명 모음 페이지 secure hello [Azure 키 자격 증명 모음 설명서](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault)합니다. 

**장점**

- Hello 키에 대 한 모든 권한을 사용 – 암호화 키도 hello 고객의 제어 hello 고객의 주요 자격 증명 모음에서 관리 됩니다.
- 기능 tooencrypt 여러 서비스 tooone 마스터
- Hello 서비스에 대 한 전반적인 관리 모델에서 키 관리를 분리할 수 있습니다.
- 지역 간 서비스 및 키 위치를 정의할 수 있습니다.

**단점**

- 키 액세스 관리에 대한 책임이 전적으로 고객에게 있습니다.
- 키 수명 주기 관리에 대한 책임이 전적으로 고객에게 있습니다.
- 추가 설치 및 구성 오버헤드

#### <a name="server-side-encryption-using-service-managed-keys-in-customer-controlled-hardware"></a>고객 제어 하드웨어에서 서비스 관리 키를 사용하여 서버 쪽 암호화

경우에 hello 요구 되지 않는 tooencrypt hello 데이터는 Microsoft의 제어를 벗어나야 소유 리포지토리에 hello 키 관리, 일부 Azure 서비스가 hello 호스트 사용자 고유의 키 HYOK () 키 관리 모델을 사용 합니다. 이 모델에서는 hello 서비스 외부 사이트에서 hello 키를 검색 해야 하 고 따라서 성능과 가용성을 보장이 영향을 받음, 구성이 더 복잡 하다. 또한 hello 서비스는 hello 암호화 하는 동안 액세스 toohello DEK가 해독 작업이이 모델의 전반적인 보안 보증 hello 및 키는 Azure 키 자격 증명 모음에서 고객이 관리 하는 비슷한 toowhen hello은입니다.  따라서 특정 키 관리 요구 사항이 필요하지 않는 한 대부분의 조직에는 이 모델이 적합하지 않습니다. Toothese 제한 인해 대부분의 Azure 서비스 서버 관리 키를 사용 하 여 제어 하는 고객 하드웨어에서 서버 쪽 암호화를 지원 하지 않습니다.

##### <a name="key-access"></a>키 액세스

관리 서비스 키를 사용 하 여 제어 하는 고객 하드웨어에서 서버 쪽 암호화를 사용 하는 경우 hello 키 hello 고객으로 구성 된 시스템에 유지 됩니다. 이 모델을 지 원하는 azure 서비스 보안 연결 tooa 고객을 설정 하는 방법을 제공 키 저장소를 제공 합니다.

**장점**

- Hello 루트 키에 대 한 모든 권한을 사용 – 암호화 키를 제공 하는 고객 저장소에서 관리
- 기능 tooencrypt 여러 서비스 tooone 마스터
- Hello 서비스에 대 한 전반적인 관리 모델에서 키 관리를 분리할 수 있습니다.
- 지역 간 서비스 및 키 위치를 정의할 수 있습니다.

**단점**

- 키 저장소, 보안, 성능 및 가용성에 대한 전적인 책임
- 키 액세스 관리에 대한 전적인 책임
- 키 수명 주기 관리에 대한 전적인 책임
- 중요한 설정, 구성 및 지속적인 유지 관리 비용
- Hello 고객 데이터 센터와 Azure 데이터 센터 간의 네트워크 가용성 증가 의존 합니다.

## <a name="encryption-at-rest-in-microsoft-cloud-services"></a>Microsoft Cloud 서비스 내 미사용 데이터 암호화

Microsoft Cloud 서비스는 세 가지 클라우드 모델, 즉 IaaS, PaaS, SaaS에서 모두 사용됩니다. 각 모델에서 작동하는 방식에 대한 예는 다음과 같습니다.

- 참조 된 서버 또는 Office 365와 같은 hello 클라우드에서 제공 하는 응용 프로그램을 포함 하는 SaaS 소프트웨어 tooas 소프트웨어 서비스입니다.
- 고객 활용 하 여 해당 응용 프로그램에서는 hello 클라우드 hello 클라우드를 사용 하 여 작업을 위한 플랫폼 서비스 같은 저장소, 분석 및 서비스 버스 기능입니다.
- 인프라 서비스 또는 운영 체제 및 hello에서 호스트 되는 응용 프로그램 배포에 고객 서비스 (IaaS) 인프라를 클라우드 및 수 있는 다른를 활용 하 여 클라우드 서비스입니다.

### <a name="encryption-at-rest-for-saas-customers"></a>SaaS 고객에 대한 미사용 데이터 암호화

SaaS(Software as a Service) 고객은 일반적으로 각 서비스에서 미사용 데이터 암호화를 사용하도록 설정하거나 사용할 수 있습니다. Office 365 서비스에 저장 된 상태의 고객 tooverify 또는 사용이 암호화에 대 한 몇 가지 옵션이 있습니다. Office 365 서비스에 대한 자세한 내용은 Office 365용 데이터 암호화 기술을 참조하세요.

### <a name="encryption-at-rest-for-paas-customers"></a>PaaS 고객에 대한 미사용 데이터 암호화

플랫폼 서비스 (PaaS) 고객의 데이터로 일반적으로 응용 프로그램 실행 환경을에 있으며 모든 Azure 리소스 공급자 toostore 고객 데이터를 사용 합니다. 나머지 옵션 사용 가능한 tooyou toosee hello 암호화 있습니다를 사용 하는 hello 저장소 및 응용 프로그램 플랫폼에 대 한 아래의 hello 테이블을 검사 합니다. 지원 링크 tooinstructions 미사용 데이터 암호화를 사용 하도록 설정 하면 각 리소스 공급자에 제공 됩니다. 

### <a name="encryption-at-rest-for-iaas-customers"></a>IaaS 고객에 대한 미사용 데이터 암호화

IaaS(Infrastructure as a Service) 고객은 다양한 서비스와 응용 프로그램을 사용할 수 있습니다. IaaS 서비스를 사용하면 Azure Disk Encryption을 사용하여 Azure 호스팅 가상 컴퓨터 및 VHD에서 미사용 데이터 암호화를 사용할 수 있습니다. 

#### <a name="encrypted-storage"></a>암호화된 저장소

PaaS와 마찬가지로 IaaS 솔루션은 암호화된 미사용 데이터를 저장하는 다른 Azure 서비스를 활용할 수 있습니다. 이러한 경우에 각 사용 되는 Azure 서비스에서 제공 하는 대로 Rest 지원에서 hello 암호화를 사용할 수 있습니다. 다음 표에서 hello hello 주요 저장소, 서비스 및 응용 프로그램 플랫폼 및 지원 되는 미사용 데이터 암호화의 hello 모델을 열거 합니다. 지원 링크가 tooinstructions 미사용 데이터 암호화를 사용 하도록 설정 하면 제공 됩니다. 

#### <a name="encrypted-compute"></a>암호화된 계산

나머지 솔루션에서 전체 암호화는 데이터가 암호화 되지 않은 형태로 저장할 수 없는 해당 hello가 필요 합니다. 사용 중인 hello Windows 페이지 파일, 크래시 덤프, 모든 로깅 hello 등 다양 한 방법으로 데이터를 메모리에 데이터를 로컬로 유지 서버 로드 hello에 응용 프로그램 수행할 수 있습니다. 이 데이터는 암호화 tooensure 미사용 IaaS 응용 프로그램 암호화 사용 하 여 Azure 디스크는 Azure IaaS 가상 컴퓨터 (Windows 또는 Linux) 및 가상 디스크입니다. 

#### <a name="custom-encryption-at-rest"></a>사용자 지정 미사용 데이터 암호화

가능할 때마다 사용된 모든 Azure 서비스에서 제공하는 Azure Disk Encryption 및 미사용 데이터 암호화 옵션을 IaaS 응용 프로그램에서 활용하는 것이 좋습니다. 경우에 따라 불규칙 한 암호화 요구 사항 또는 비 Azure 기반된 저장소, IaaS 응용 프로그램의 개발자 tooimplement 암호화 해야 할 수와 같은 자체 놓습니다. IaaS 솔루션 개발자는 특정 Azure 구성 요소를 활용하여 Azure 관리 및 고객 기대와 더 잘 통합될 수 있습니다. 특히, 개발자는 hello 서비스 tooprovide 키 저장소를 보안으로 대부분의 Azure 플랫폼 서비스와 일관 된 키 관리 옵션에 고객에 게 제공 Azure 키 자격 증명 모음을 사용 해야 합니다. 또한 사용자 지정 솔루션은 Azure 관리 서비스 Id tooenable 서비스 계정 tooaccess 암호화 키를 사용 해야 합니다. Azure Key Vault 및 Managed Service Identities에 대한 개발자 정보는 해당 SDK를 참조하세요.

## <a name="azure-resource-providers-encryption-model-support"></a>Azure 리소스 공급자 암호화 모델 지원

Microsoft Azure 서비스는 각각 hello 암호화 rest 모델 중 하나 이상을 지원합니다. 그러나 일부 서비스에 대 한 hello 암호화 모델 중 하나 이상이 아니어야 적용 합니다. 또한 서비스가 서로 다른 일정으로 이러한 시나리오에 대한 지원을 해제할 수 있습니다. Hello 암호화 각 hello 주요 Azure 데이터 저장소 서비스에 대 한이 문서 작성 hello 시 rest 지원에 설명합니다.

### <a name="azure-disk-encryption"></a>Azure Disk Encryption

Azure IaaS(Infrastructure as a Service) 기능을 사용하는 모든 고객은 Azure Disk Encryption을 통해 IaaS VM 및 디스크에 대한 미사용 데이터 암호화를 달성할 수 있습니다. Azure 디스크에 대 한 자세한 내용은 암호화 참조 hello [Azure 디스크 암호화 설명서](https://docs.microsoft.com/azure/security/azure-security-disk-encryption)합니다.

#### <a name="azure-storage"></a>Azure 저장소

Azure Blob 및 File 저장소는 서버 쪽 암호화 시나리오 및 고객 암호화 데이터(클라이언트 쪽 암호화)에 대한 미사용 데이터 암호화를 지원합니다.

- 서버 쪽: Azure Blob 저장소를 사용하는 고객은 각 Azure 저장소 리소스 계정에서 미사용 데이터 암호화를 사용할 수 있습니다. 한 번만 사용할 수 있는 서버 쪽 암호화 toohello 응용 프로그램 투명 하 게 수행 됩니다. 자세한 내용은 [미사용 데이터에 대한 Azure Storage 서비스 암호화](https://docs.microsoft.com/azure/storage/storage-service-encryption)를 참조하세요.
- 클라이언트 쪽: Azure Blobs의 클라이언트 쪽 암호화가 지원됩니다. 고객을 암호화 하는 클라이언트 쪽 암호화를 사용 하는 경우 데이터 hello 및 hello 데이터 암호화 된 blob로 업로드 합니다. 키 관리는 hello 고객에 의해 수행 됩니다. 자세한 내용은 [Microsoft Azure Storage용 클라이언트 쪽 암호화 및 Azure Key Vault](https://docs.microsoft.com/azure/storage/storage-client-side-encryption)를 참조하세요.


#### <a name="sql-azure"></a>SQL Azure

SQL Azure는 현재 Microsoft 관리 서비스 쪽 및 클라이언트 쪽 암호화 시나리오에 대한 미사용 데이터 암호화를 지원합니다.

에 대 한 지원 서버 암호화를 현재 투명 한 데이터 암호화를 라는 hello SQL 기능을 통해 제공 됩니다. SQL Azure 고객이 TDE 키를 사용하도록 설정하면 해당 키가 자동으로 만들어지고 관리됩니다. Hello 데이터베이스 및 서버 수준에서 휴지 암호화를 사용할 수 있습니다. 2017년 6월 현재 [TDE(투명한 데이터 암호화)](https://msdn.microsoft.com/library/bb934049.aspx)는 새로 만든 데이터베이스에서 기본적으로 사용하도록 설정됩니다.

Hello를 통해 SQL Azure 데이터의 클라이언트 쪽 암호화는 지원 [항상 암호화](https://msdn.microsoft.com/library/mt163865.aspx) 기능입니다. 항상 암호화 된 hello 클라이언트에서 만들고 저장 하는 키를 사용 합니다. Windows 인증서 저장소, Azure 주요 자격 증명 또는 로컬 하드웨어 보안 모듈에서 고객 hello 마스터 키를 저장할 수 있습니다. SQL Server Management Studio를 사용 하 여 SQL 사용자 항목 선택 키 만족할 만한 toouse tooencrypt 되는 열입니다.

|                                  |                |                     | **암호화 모델**             |                              |        |
|----------------------------------|----------------|---------------------|------------------------------|------------------------------|--------|
|                                  |                |                     |                              |                              | **클라이언트** |
|                                  | **키 관리** | **서비스 관리 키** | **Key Vault에서 관리되는 고객** | **온-프레미스에서 관리되는 고객** |        |
| **저장소 및 데이터베이스**            |                |                     |                              |                              |        |
| 디스크(IaaS)                      |                | -                   | 예                          | 예*                         | -      |
| SQL Server(IaaS)                |                | 예                 | 예                          | 예                          | 예    |
| SQL Azure(PaaS)                 |                | 예                 | 미리 보기                      | -                            | 예    |
| Azure Storage(블록/페이지 Blob) |                | 예                 | 미리 보기                      | -                            | 예    |
| Azure Storage(파일)            |                | 예                 | -                            | -                            | -      |
| Azure Storage(테이블, 큐)   |                | -                   | -                            | -                            | 예    |
| Cosmos DB(Document DB)          |                | 예                 | -                            | -                            | -      |
| StorSimple                       |                | 예                 | -                            | -                            | 예    |
| Backup                           |                | -                   | -                            | -                            | 예    |
| **인텔리전스 및 분석**       |                |                     |                              |                              |        |
| Azure 데이터 팩터리               |                | 예                 | -                            | -                            | -      |
| Azure 기계 학습           |                | -                   | 미리 보기                      | -                            | -      |
| Azure Stream Analytics           |                | 예                 | -                            | -                            | -      |
| HDInsights(Azure Blob Storage)  |                | 예                 | -                            | -                            | -      |
| HDInsights(Data Lake Storage)   |                | 예                 | -                            | -                            | -      |
| Azure Data Lake Store            |                | 예                 | 예                          | -                            | -      |
| Azure Data Catalog               |                | 예                 | -                            | -                            | -      |
| Power BI                         |                | 예                 | -                            | -                            | -      |
| **IoT 서비스**                     |                |                     |                              |                              |        |
| IoT 허브                          |                | -                   | -                            | -                            | 예    |
| Service Bus                      |                | -              | -                            | -                            | 예    |
| Event Hubs                       |                | -             | -                            | -                            | -      |


## <a name="conclusion"></a>결론

Azure 서비스에 저장 된 고객 데이터의 보호 다양화 tooMicrosoft입니다. 모든 Azure 호스 티 드 서비스는 Rest 옵션에서 커밋된 tooproviding 암호화 합니다. Azure Storage, SQL Azure 및 주요 분석 및 인텔리전스 서비스와 같은 기본 서비스에서는 이미 미사용 데이터 암호화 옵션을 제공하고 있습니다. 이러한 서비스 중 일부는 고객 관리 키와 클라이언트 쪽 암호화뿐만 아니라 서비스 관리 키와 암호화도 지원하고 있습니다. Microsoft Azure 서비스 대폭 개선 하는 암호화 Rest 공급 시 및 hello 예정 된 월에서 미리 보기 및 일반 가용성에 대 한 새 옵션 예정인 합니다.

