---
title: "Azure에 대 한 분류 aaaData | Microsoft Docs"
description: "이 문서는 데이터 분류에 대 한 기본적인 소개 toohello를 제공 하 고 특히 클라우드 컴퓨팅 및 Microsoft Azure를 사용 하 여 hello 컨텍스트에서 해당 값이 강조 표시"
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ROBOTS: NOINDEX
redirect_url: https://aka.ms/data-classification-cloud
ms.assetid: 91d4afed-b80f-4a26-b526-b52b9c858cfb
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/18/2017
ms.author: yurid
ms.openlocfilehash: 726da2482beab3bf7b0ac33510f2b523d5074df8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="data-classification-for-azure"></a>Azure에 대한 데이터 분류
이 문서는 데이터 분류에 대 한 기본적인 소개 toohello를 제공 하 고 특히 클라우드 컴퓨팅 및 Microsoft Azure를 사용 하 여 hello 컨텍스트에서 해당 값이 강조 표시 합니다. 

## <a name="data-classification-fundamentals"></a>데이터 분류 기본 사항
조직의 데이터를 성공적으로 분류하려면 조직의 필요를 폭 넓게 인식하고 데이터 자산이 상주하는 위치를 잘 이해하고 있어야 합니다.  

데이터는 세 가지 기본 상태 중 하나로 존재합니다. 

* 미사용 
* 진행 중 
* 전송 중 

세 가지 상태 데이터 분류에 대 한 고유한 기술 솔루션 필요 하지만 hello 적용 된 원칙 데이터 분류 해야 수 hello 동일 각각에 대해 합니다. 기밀로 분류 되는 데이터 필요 toostay 기밀 상태의 프로세스에서 및 전송에서 합니다. 

또한 데이터는 구조화될 수도 있고 구조화되지 않을 수도 있습니다. Hello에 대 한 일반적인 분류 프로세스는 데이터베이스에서 발견 되는 데이터 구조 및 스프레드시트는 문서, 소스 코드 및 전자 메일 같은 구조화 되지 않은 데이터에 대 한 보다 덜 복잡 하 고 시간이 많이 걸리는 toomanage 합니다. 

> [!TIP]
> Azure 기능 및 데이터 암호화 모범 사례에 관한 자세한 내용은 [Azure 데이터 암호화 모범 사례](azure-security-data-encryption-best-practices.md)를 참조하세요.
> 
> 

일반적으로 조직은 구조화된 데이터보다 구조화되지 않은 데이터를 더 많이 가지고 있습니다. 이 든 상관 없이 데이터 구조적 또는 비구조적, toomanage 데이터 민감도 중요 합니다. 제대로 구현 된 데이터 분류 자산 간주 되는 공용 또는 무료 toodistribute 데이터 자산 보다 큰 감독으로 관리 되는 중요 한 정보나 기밀 데이터 되도록 해줍니다. 

### <a name="controlling-access-toodata"></a>Toodata 액세스를 제어합니다.
인증 및 권한 부여는 종종 서로 혼동되고 역할은 오해됩니다. 실제로 않습니다 hello 다음 그림에에서 나와 있는 것 처럼 매우 다릅니다.  

![데이터 액세스 및 제어](./media/azure-security-data-classification/azure-security-data-classification-fig1.png)

### <a name="authentication"></a>인증
인증 일반적으로 두 개 이상의 부분으로 구성 됩니다: username 자격 증명 hello tooconfirm 암호와 같은 토큰에 대 한 사용자는 사용자 이름 또는 사용자 ID tooidentify 유효 합니다. hello 프로세스 hello 서비스; tooany 항목 액세스 또는 인증 된 사용자를 제공 하지 않습니다. hello 사용자가는 신원을 확인 합니다.   

> [!TIP]
> [Azure Active Directory](../active-directory/active-directory-whatis.md) tooauthenticate 수 있도록 사용자 권한을 부여 하는 클라우드 기반 id 서비스를 제공 합니다. 
> 
> 

### <a name="authorization"></a>권한 부여
권한 부여는 hello 프로세스 응용 프로그램, 데이터 집합, 데이터 파일 또는 다른 개체에는 인증 된 사용자 hello 기능 tooaccess를 제공 하는 중입니다. 인증 된 사용자가 hello 권한 toouse 할당 수정 하거나 액세스할 수 있는 삭제 항목 toodata 분류 주의가 필요 합니다. 

성공적인 권한 부여 구현의 메커니즘 toovalidate 개별 사용자의 필요 tooaccess 파일 및 역할, 보안 정책 및 정책 고려 사항 위험의 조합에 따라 정보 필요 합니다. 예를 들어 특정 기간 업무 (LOB) 응용 프로그램의 데이터는 모든 직원이 액세스 하는 toobe 필요 하지 않을 수도 및 직원의 작은 하위 집합만 가능성이 필요한 액세스 toohuman hr () 파일입니다. 하지만 조직 toocontrol 고, 방법, 사용자를 인증 하기 위한 효과적인 시스템 준비 해야으로 데이터를 액세스할 수 있는 사용자. 

> [!TIP]
> Microsoft Azure에서 사용자에 게 필요 업무 tooperform는 있는지 tooleverage 신속히 알아봅니다 액세스 제어 (RBAC) toogrant만 hello 제한 된 액세스를 확인 합니다. 읽기 [역할 할당 toomanage tooyour Azure Active Directory 리소스 액세스를 사용 하 여](../active-directory/role-based-access-control-configure.md) 자세한 정보에 대 한 합니다. 
> 
> 

### <a name="roles-and-responsibilities-in-cloud-computing"></a>클라우드 컴퓨팅에서 역할 및 책임
클라우드 공급자 위험을 관리 하는의 고객이 원하는 tooensure 해당 데이터 분류 관리 및 적용 올바르게 구현 하지만 tooprovide hello 적절 한 수준의 데이터 관리 서비스입니다.  

Hello 다음 그림에에서 나와 있는 것 처럼에 배치 되는 클라우드 서비스 모델에 따라 책임 달라 집니다 데이터 분류 합니다. hello 세 가지 기본 클라우드 서비스 모델은 서비스 (IaaS), 서비스 (PaaS) 플랫폼 및 서비스로 SaaS ()는 소프트웨어 인프라입니다. 또한 데이터 분류 메커니즘의 구현에 대 한 의존도 hello 및 hello 클라우드 공급자의 요구 사항에 따라 달라 집니다. 

![역할](./media/azure-security-data-classification/azure-security-data-classification-fig2.png)

데이터 분류 수행 하는 있지만 클라우드 공급자 어떻게 보호 하 고 hello 고객 데이터의 클라우드 내에 저장 된 hello 개인 정보를 유지 하는 방법에 대 한 기록된 행을 확인 해야 합니다.  

* **IaaS 공급자** 요구 사항이 제한 된 가상 환경 hello tooensuring 데이터 분류 기능이 및 고객의 규정 준수 요구 사항을 수용할 수 있습니다. 고객 데이터 규정 준수 요구 사항을 해결 하는지 tooensure만 필요 하기 때문에 기본적으로 데이터 분류에 더 작은 역할을 보유 하는 IaaS 공급자. 그러나 공급자 해야 여전히 가상 환경 해결 확인 더하기 toosecuring에서 데이터 분류 요구 사항의 데이터 센터입니다.
* **PaaS 공급자** hello 플랫폼 분류 도구에 대 한 계층적된 접근 tooprovide 보안에 사용 될 수 있으므로 책임 혼합 될 수 있습니다. PaaS 공급자 인증 및 일부 권한 부여 규칙을 수 있는 담당자 및 보안 및 데이터 분류 기능이 tootheir 응용 프로그램 계층을 제공 해야 합니다. 훨씬 IaaS 공급자와 같은 PaaS 공급자 필요 자사의 플랫폼 준수 tooensure 모든 관련 데이터 분류 요구 사항과 합니다.
* **SaaS 공급자** 는 권한 부여 체인의 일부분으로 간주 자주는 고 됩니다 필요 hello SaaS 응용 프로그램에 저장 된 데이터를 hello tooensure 제어할 수 유형별로 분류 합니다. LOB 응용 프로그램에 대해 SaaS 응용 프로그램을 사용할 수 있으며 앞으로 tooprovide 의미 tooauthenticate hello 사용 되 고 저장 하는 데이터에 권한을 부여 합니다. 

## <a name="classification-process"></a>분류 프로세스
Hello를 이해 하는 대부분의 조직 데이터 분류를 위해 필요 하 고 기본 질문에 맞서게 tooimplement 원하는: 여기서 toobegin?

효율적이 고 간단한 단방향 tooimplement 데이터 분류는 toouse hello 계획을 위해서는에서 검사, ACT 모델 [MOF](https://technet.microsoft.com/solutionaccelerators/dd320379.aspx)합니다. hello 다음 hello 작업을이 모델에 필요한 toosuccessfully 구현 데이터 분류를 차트 그림입니다.  

1. **계획**. 데이터 보유 하 고 toodeploy hello 분류 프로그램, 데이터 자산을 식별 하 고 보호 프로필을 개발 합니다. 
2. **실행**. 데이터 분류 정책이 동의한 후 hello 프로그램을 배포 하 고 기밀 데이터에 대 한 필요에 따라 적용 기술을 구현 합니다.  
3. **확인**. 확인 하 고 hello 도구와 방법을 사용 하 고 효과적으로 주소 지정 tooensure hello 분류 정책은 보고서를 확인 합니다. 
4. **작업**. 데이터 액세스의 hello 상태를 검토 하 고 파일 및는 재분류 및 수정 버전이 방법론 tooadopt 변경과 tooaddress 새로운 위험을 사용 하 여 수정 해야 하는 데이터를 검토 합니다.  

![계획, 수행, 확인, 작업](./media/azure-security-data-classification/azure-security-data-classification-fig3.png)

### <a name="select-a-terminology-model-that-addresses-your-needs"></a>요구 사항을 처리하는 용어 모델 선택
수동 프로세스를 사용자 또는 시스템의 위치, 데이터베이스 관련 분류와 같은 응용 프로그램 기반 프로세스를 기반으로 하며 자동화 된 데이터를 분류 하는 위치 기반 프로세스를 포함 한 데이터를 분류 하기 위한 몇 가지 유형의 프로세스 존재 이 문서의 뒷부분에 나오는 hello "기밀 데이터를 보호" 섹션에 설명 되어 다음과 같은 다양 한 기술을 사용 하는 프로세스입니다.  

이 문서에서는 널리 사용되고 업계에서 인정 받는 모델을 기반으로 하는 일반화된 용어 모델 두 가지를 소개합니다. 이러한 용어 모델을 세 가지 수준의 분류 민감도 제공 하는 다음 표에 hello에 표시 됩니다.  

> [!NOTE]
> 파일이 나 hello 최고 수준의 분류에 있는 서로 다른 수준에서 일반적으로 분류할 수 있는 데이터를 설정 해야 하는 결합 hello 전반적인 분류 하는 리소스 분류할 때입니다. 예를 들어 중요하고 제한된 데이터를 포함하고 있는 파일은 제한으로 분류해야 합니다.  
> 
> 

| **민감도** | **용어 모델 1** | **용어 모델 2** |
| --- | --- | --- |
| 높음 |기밀 |제한 |
| 중간 |내부 전용 |중요 |
| 낮음 |공용 |제한 없음 |

#### <a name="confidential-restricted"></a>기밀(제한됨)
기밀 또는 제한 된으로 분류 된 정보를 치명적인 tooone 또는 개인 및/또는 더 조직 손상 되거나 손실 될 수 있는 데이터를 포함 합니다. 이러한 정보는 자주에 "필요 tooknow"으로 제공 및 포함 될 수 있습니다. 

* 사회 보장 번호 또는 국적 식별 번호, 여권 번호, 신용 카드 번호, 운전 면허증 번호, 의료 기록 및 건강 보험 상품 ID 번호 등과 같은 개인 식별이 가능한 정보를 비롯한 개인 데이터.  
* 수표 또는 투자 계좌 번호 등과 같은 금융 계좌 번호를 비롯한 금융 기록. 
* 고유하거나 특정적인 지적 재산인 문서 또는 데이터와 같은 비즈니스 자료.  
* 잠재적 변호인 특권 자료를 비롯한 법적 데이터. 
* 개인 암호화 키, 사용자 이름 암호 쌍 또는 개인 생체 인식 키 파일과 같은 기타 식별 순서를 비롯한 인증 데이터. 

많은 경우 기밀로 분류되는 데이터에는 데이터 처리에 대한 규정 및 준수 요구 사항이 적용됩니다. 

#### <a name="for-internal-use-only-sensitive"></a>내부 전용(중요)
보통 민감도로 분류되는 정보는 손실되거나 파괴되더라도 개인 및/또는 조직에 심각한 영향을 주지 않는 파일 및 데이터를 포함합니다. 이러한 정보는 다음과 같습니다. 

* 전자 메일, 되는 대부분의 삭제 또는 (개별 hello 기밀 분류에서 식별 된 사용자 로부터 사서함 또는 메일 제외)은 위기 상황을 발생 하지 않고 분산 될 수 있습니다.  
* 기밀 데이터를 포함하고 있지 않은 문서 및 파일.

일반적으로 이 분류는 기밀이 아닌 모든 내용을 포함합니다. 관리되거나 매일 사용되는 대부분의 파일은 중요로 분류될 수 있으므로 이 분류는 대부분의 비즈니스 데이터를 포함할 수 있습니다. 공용으로 설정 되거나 기밀 데이터에 hello 예외로 기본적으로 비즈니스 조직 내의 모든 데이터 중요 한 것으로 분류할 수 있습니다. 

#### <a name="public-unrestricted"></a>공용(제한 없음)
공용으로 분류 된 정보를 데이터와 중요 한 toobusiness 요구 사항이 나 작업 되지 않은 파일을 포함 합니다. 이 분류는 의도적으로 릴리스된 toohello 마케팅 자료 또는 키를 눌러 공지 사항 등의 사용을 위해 공개 된 데이터를 포함할 수도 있습니다. 또한 이 분류는 전자 메일 서비스에 의해 저장된 스팸 메일 메시지와 같은 데이터를 포함할 수 있습니다. 

### <a name="define-data-ownership"></a>데이터 소유권 정의
것이 중요 한 tooestablish 모든 데이터 자산에 대 한 소유권 체인 custodial 선택을 취소 합니다. hello 다음 표에 다양 한 데이터 소유권 역할 데이터 분류 노력 및 해당 권한에 관계에 있습니다.  

| **역할** | **만들기** | **수정/삭제** | **대리자** | **읽기** | **보관/복원** |
| --- | --- | --- | --- | --- | --- |
| 소유자 |X |X |X |X |X |
| 보유자 | | |X | | |
| 관리자 | | | | |X |
| 사용자\* | |X | |X | |

**사용자에게 보유자에 의한 편집 및 삭제와 같은 추가 권한을 부여할 수 있음* 

> [!NOTE]
> 이 표는 역할 및 권한의 자세한 목록을 제공하지 않으며 단지 대표적인 샘플일 뿐입니다. 
> 
> 

hello **데이터 자산 소유자** hello 보유 하 고 할당 하 고 소유권을 위임할 수 있는 hello 데이터의 원래 작성자가 있습니다. 파일을 만들 때 의미 하는 책임 toounderstand toobe 기밀로 분류 되는 사항 조직의 정책에 따라 분류 수 tooassign hello 소유자 여야 합니다. 모든 데이터 자산 소유자의 데이터는 해당 소유자가 기밀(제한) 데이터 유형을 소유하거나 만들 책임이 있지 않은 한 내부 전용(중요)으로 자동 분류될 수 있습니다. 대부분의 경우 hello 소유자 역할 hello 데이터 분류 한 후 변경 됩니다. 예를 들어 hello 소유자 분류 된 정보 데이터베이스를 만들고 해당 권한 toohello 데이터 보유 하 고 포기 될 수 있습니다.  

> [!NOTE]
> 데이터 자산 소유자는 다양 한 서비스, 장치 및 미디어, 일부는 개인 및 toohello 조직 속할 중 일부는 주로 사용 합니다. 명확한 조직 정책은 노트북 및 스마트 장치와 같은 장치의 사용이 데이터 분류 지침을 따르도록 하는 데 도움이 될 수 있습니다.  
> 
> 

hello **데이터 자산 보유 하 고** 에 의해 할당 된 hello 자산 소유자 (또는 해당 대리자) toomanage hello 자산 따라 tooagreements hello 자산 소유자 또는 해당 되는 정책 요구 사항에 따라 합니다. 이상적으로 자동화 된 시스템에서 hello 보유 하 고 역할을 구현할 수 있습니다. 자산 보유자 필요한 액세스 제어 제공 되 고 관리 및 위임 된 tootheir 주의 자산을 보호 되도록 합니다. hello 자산 보유자의 hello 책임을 들 수 있습니다.  

* Hello 자산 hello 자산 소유자의 방향에 따라 또는 hello 자산 소유자  보호 
* 분류 정책이 준수되는지 확인 
* Tooagreed 변경의 자산 소유자에 게 알리지-컨트롤 및/또는 보호 프로시저 이전 toothose 변경 내용이 적용 시 
* Hello 자산 보유자 책임의 변경 내용 tooor 제거에 대 한 보고 toohello 자산 소유자 
* **관리자**는 무결성을 유지해야 할 책임이 있는 사용자이지만, 데이터 자산 소유자, 보유자 또는 사용자는 아닙니다. 실제로 여러 관리자 역할 toohello 데이터에 액세스 하지 않고도 데이터 컨테이너 관리 서비스를 제공 합니다. 선택 가져오고 작동 hello 장치와 저장소 해당 집 hello 자산 및 hello 관리자 역할에는 hello 자산의 레코드를 유지 관리 하는 hello 데이터의 백업 및 복원을 포함 됩니다. 
* hello 자산 사용자 액세스 toodata 또는 파일 부여 받은 모든 사용자를 포함 합니다. 액세스 할당 하 여 hello 소유자 toohello 자산 보유 하 고 종종 위임 됩니다.  

### <a name="implementation"></a>구현
관리 고려 사항 tooall 분류 방법론을 적용 합니다. 이러한 고려 사항은 필요 tooinclude 세부 정보를 사용자에 대 한 내용, 위치, 시점과 이유는 데이터 자산 것 수 사용, 액세스, 변경 또는 삭제 합니다. 모든 자산 관리 조직의 위험을 표시 하는 방법을 이해 해야 하지만 hello 데이터 분류 프로세스에 정의 된 대로 간단한 방법론을 적용할 수 있습니다. 데이터 분류에 대 한 추가 고려 사항 hello 소개 새 응용 프로그램 및 도구 및 분류 방법 구현 된 후 변경 내용 관리를 포함 합니다.  

### <a name="reclassification"></a>재분류
데이터 자산의 hello 분류 상태를 변경 하거나 다시 분류 toobe 해당 hello 데이터 자산 중요도 결정 하는 사용자 또는 시스템 또는 위험 프로필이 변경 된 경우 필요 합니다. 이 위해가 하 고 hello 분류 상태 toobe 현재 계속 되도록 보장 하는 데 중요 합니다. 수동으로 분류되지 않은 대부분의 콘텐츠는 자동으로 또는 데이터 보유자 또는 데이터 소유자의 사용에 따라 분류될 수 있습니다. 

### <a name="manual-data-reclassification"></a>수동 데이터 재분류
이상적으로이 위해 변경 내용의 세부 hello 캡처되고 감사를 확인 합니다. 수동 재분류에 대 한 hello 가능성이 가장 높은 이유는 용지 형식이 나 된 원래 마이닝에서 잘못 분류 되는 요구 사항 tooreview 데이터에 유지 하는 레코드 또는 구분에 속하는 이유로 것입니다. 이 문서에서 데이터 분류 및 이동 데이터 toohello 클라우드에서는 있다고 간주 수동 재분류 노력 상황별으로에 주의 해야 합니다. 한 위험 관리 검토 이상적인 tooaddress 분류 요구 사항. 일반적으로 이러한 시키기는 hello 조직의 정책을 분류 toobe는 사항에 대 한 고려를 hello 기본 분류 상태 (모든 데이터 및 중요 한 하지만 하지 기밀 중인 파일) 하 고 위험 수준이 높은 데이터에 대 한 예외입니다. 

### <a name="automatic-data-reclassification"></a>자동 데이터 재분류
자동 데이터 재분류 수동 분류로 hello 같은 일반 규칙을 사용 합니다. hello 예외 규칙 뒤 하 고 필요에 따라 적용 되는 자동화 된 솔루션을 유지 하는 수입니다. 데이터 분류는 권한 부여 기술을 사용하여 데이터가 저장, 사용 중 및 전송 중일 때 적용할 수 있는 데이터 분류 적용 정책의 일부로 수행될 수 있습니다.

* 응용 프로그램 기반. 특정 응용 프로그램을 사용하면 기본적으로 분류 수준이 설정됩니다. 예를 들어 고객 관계 관리(CRM) 소프트웨어, HR 및 건강 기록 관리 도구에서 나온 데이터는 기본적으로 기밀입니다. 
* 위치 기반. 데이터 위치는 데이터 민감도를 식별하는 데 도움이 될 수 있습니다. 예를 들어, 시간 또는 재무 부서에서 저장 된 데이터를 본질적으로 기밀 가능성이 toobe입니다.  

### <a name="data-retention-recovery-and-disposal"></a>데이터 보존, 복구 및 삭제
데이터 복구 및 삭제는 데이터 재분류와 마찬가지로 데이터 자산 관리의 필수적인 부분입니다. hello 데이터 복구 및 삭제에 대 한 데이터 보존 정책에 의해 정의 됩니다 원칙과 동일 hello에 강제로 방식으로 데이터 재분류; 이러한 위해 공동 작업으로 hello 보유 하 고 및 관리자 역할에 의해 수행 됩니다.  

오류 toohave 데이터 보존 정책을 규정 및 법적 검색 요구 사항과 데이터 손실 또는 실패 toocomply를 의미할 수 있습니다. 명확 하 게 정의 된 데이터 보존 정책이 없는 대부분의 조직에서는 기본 "모든 것 이" 보존 정책을 toouse는 경향이 있습니다. 그러나 그러한 보존 정책은 클라우드 서비스 시나리오에서 추가적인 위험이 있습니다. 

예를 들어 클라우드 서비스 공급자에 대 한 데이터 보존 정책은 (으로 hello 서비스는 hello 데이터 보관에 대 한 지불 됩니다) "hello hello 구독 기간"의 경우와 간주할 수 있습니다. 그러한 유료 보존 계약은 회사 또는 규정 보존 정책을 다루지 않을 수 있습니다. 기밀 데이터에 대한 정책을 정의하면 모범 사례에 따라 확실히 데이터가 저장되고 제거되도록 할 수 있습니다. 또한 보관 정책을 만들 수 있습니다 데이터에 대 한 이해를 삭제 해야 tooformalize 및 시기. 

데이터 보존 정책에 필요한 hello 다뤄야 합니다. 규정 및 규정 준수 요구 사항으로 요구 되는 회사 법적 보존 합니다. 분류된 데이터는 공급자를 통해 저장한 데이터에 대한 보존 기간과 예외에 관한 질문을 유발할 수 있으며, 정확하게 분류되지 않은 데이터의 경우 그러한 질문이 제기될 가능성이 더 높습니다. 

> [!TIP]
> hello를 참조 하 여 Azure 데이터 보존 정책 등에 대 한 자세한 정보 [Microsoft 온라인 정기 가입 계약](https://azure.microsoft.com/support/legal/subscription-agreement/)
> 
> 

## <a name="protecting-confidential-data"></a>기밀 데이터 보호
데이터 분류 한 후 찾기 및 구현 방법으로 tooprotect 기밀 데이터는 모든 데이터 보호 배포 전략의 핵심 됩니다. 기밀 데이터를 보호 하려면 추가로 주의 받지 toohow 데이터가 저장 되 고 전송 hello 클라우드 에서처럼도 기존 아키텍처에 필요 합니다. 

이 섹션에서는 toohelp 기밀로 분류 않은 데이터를 보호 적용 작업을 자동화할 수 있는 일부 기술에 대 한 기본 정보를 제공 합니다. 

다음 그림에서는 hello,으로 이러한 기술은으로 배포할 수 있습니다 온-프레미스 또는 클라우드 기반 솔루션-또는 해당 온-프레미스 배포의 일부 있고 나머지 일부 hello 클라우드에서 하이브리드 방식입니다. (암호화 및 권한 관리와 같은 일부 기술은 확장할 수도 toouser 장치.)  

![기술](./media/azure-security-data-classification/azure-security-data-classification-fig4.png)

### <a name="rights-management-software"></a>권한 관리 소프트웨어
데이터 손실을 방지하기 위한 한 가지 솔루션은 권한 관리 소프트웨어입니다. 조직에서 종료 시점의 정보의 toointerrupt hello 흐름을 시도 하는 방법과, 달리 권한 관리 소프트웨어 심층 데이터 저장소 기술 수준에서 작동 합니다. 문서는 암호화되며 암호를 해독할 수 있는 사람에 대한 제어에서는 디렉터리 서비스와 같은 인증 제어 솔루션에 정의된 액세스 제어를 사용합니다.  

> [!TIP]
> 데이터로 hello 정보 보호 솔루션 tooprotect 다양 한 시나리오에서 Azure 권한 관리 (Azure RMS)를 사용할 수 있습니다. 이 Azure 솔루션에 대한 자세한 내용은 [Azure Rights Management란?](https://docs.microsoft.com/rights-management/understand-explore/what-is-azure-rms)을 참조하세요.
> 
> 

권한 관리 소프트웨어의 hello 이점 중 일부는 다음과 같습니다. 

* 중요 정보를 보호합니다. 사용자가 권한 관리 지원 응용 프로그램을 사용하여 자신의 데이터를 직접 보호할 수 있습니다. 추가 단계가 필요하지 않습니다. 즉, 문서 작성, 전자 메일 보내기 및 데이터 게시는 일관성 있는 데이터 보호 환경을 제공합니다. 
* 보호는 hello 데이터와 함께 이동 됩니다. 고객의 hello 클라우드를 기존 IT 인프라 또는 hello 사용자 데스크톱에서 누가 tootheir 데이터에 액세스 제어에 남아 있습니다. 조직에서는 tooencrypt 자신의 데이터를 선택할 수 있으며 tootheir 비즈니스 요구 사항에 따라 액세스를 제한 됩니다. 
* 기본 정보 보호 정책입니다. 관리자 및 사용자는 "회사 기밀–읽기 전용" 및 "전달하지 말 것" 등 많은 일반적인 비즈니스 시나리오에 대한 표준 정책을 사용할 수 있습니다. 읽기, 복사, 저장, 편집, 인쇄 및 전달 tooallow 유연 하 게 정의할 사용자 지정 사용 권한 등 다양 한 사용 권한 사용할 수 있습니다. 

> [!TIP]
> 미사용 데이터에 대해서는 [Azure 저장소 서비스 암호화](../storage/storage-service-encryption.md)를 사용하여 Azure 저장소의 데이터를 보호할 수 있습니다. 사용할 수도 있습니다 [Azure 디스크 암호화](azure-security-disk-encryption.md) toohelp Azure 가상 컴퓨터에 대 한 사용 되는 가상 디스크에 포함 된 데이터를 보호 합니다.
> 
> 

### <a name="encryption-gateways"></a>암호화 게이트웨이
모든 액세스 toocloud 기반 데이터 경로 재정의 하 여 암호화 게이트웨이 자체 레이어 tooprovide 암호화 서비스에서 작동 합니다. 이 방법을 VPN(가상 사설망)의 방법과 혼동하지 않아야 합니다. 암호화 게이트웨이 투명 한 설계 된 tooprovide 레이어 toocloud 기반 솔루션입니다.   

암호화 게이트웨이 수단 toomanage 및 전송 중에 hello 데이터와 저장 된 상태의 데이터를 암호화 하 여 기밀로 분류 되었습니다 되는 데이터 보호를 제공할 수 있습니다.  

암호화 게이트웨이 사용자 장치 사이의 hello 데이터 흐름에 있고 응용 프로그램 데이터 센터는 tooprovide 암호화/암호 해독 서비스 합니다. 이러한 솔루션은 VPN과 마찬가지로 대부분 온-프레미스 솔루션입니다. 이들은 디자인 된 tooprovide hello 데이터와 키 관리 공급자를 배치 hello 위험을 절감 하 고 암호화 키를 제어할 수 있는 타사입니다. 이러한 솔루션은 디자인, 암호화, toowork 매우 유사 하 게 원활 하 게 및 투명 하 게 사용자 hello 서비스 사이입니다. 

> [!TIP]
> 사용할 수 있습니다 Azure ExpressRoute tooextend 온-프레미스 네트워크에 hello Microsoft 클라우드 전용된 개인 연결을 통해. 이 기능에 대한 자세한 내용은 [Express 경로 기술 개요](../expressroute/expressroute-introduction.md)를 참조하세요. 온-프레미스 네트워크와 Azure 간의 프레미스 간 연결을 위한 또 다른 옵션은 [사이트 간 VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)입니다.
> 
> 

### <a name="data-loss-prevention"></a>데이터 손실 방지
데이터 손실 (경우에 따라 참조 tooas 데이터 유출)는 중요 한 고려 사항 이며 hello 악성 또는 실수로 참가자를 통해 외부 데이터 손실 방지 대부분의 조직에 대 한 가장 중요 합니다.  

데이터 손실 방지(DLP) 기술은 전자 메일 서비스와 같은 솔루션이 기밀로 분류된 데이터를 전송하지 않도록 하는 데 도움이 될 수 있습니다. 조직 이용할 수 toohelp DLP 기능에서 기존 제품의 데이터 손실을 방지할 수 있습니다. 이러한 기능에는 처음부터 새로 또는 hello 소프트웨어 공급 업체에서 제공 하는 템플릿을 사용 하 여 쉽게 만들 수 있는 정책을 사용 합니다.  

DLP 기술을 통해 키워드 일치, 사전 일치, 정규식 평가, 및 기타 콘텐츠 검사 toodetect 콘텐츠 조직 DLP 정책을 위반 하는 심도 깊은 콘텐츠 분석을 수행할 수 있습니다. 예를 들어 DLP 손실을 방지할 수 있습니다 hello의 데이터 형식에 따라 hello: 

* 사회 보장 번호 및 국적 식별 번호 
* 은행 정보 
* 신용 카드 번호  
* IP 주소 

또한 일부 DLP 기술 (예를 들어 경우 조직 tootransmit 사회 보장 번호 정보 tooa 급여 프로세서 필요) hello 기능 toooverride hello DLP 구성을 제공 합니다. 또한도 전송 되지 않게 toosend 중요 한 정보를 끄려고 전에 사용자가 알림을 받을 수 있도록 가능한 tooconfigure DLP 됩니다. 

> [!TIP]
> Office 365 DLP 기능 tooprotect 문서를 사용할 수 있습니다. 자세한 내용은 [Office 365 준수 제어: 데이터 손실 방지](https://blogs.office.com/2013/10/28/office-365-compliance-controls-data-loss-prevention/)를 참조하세요.
> 
> 

## <a name="see-also"></a>참고 항목
* [Azure 데이터 암호화 모범 사례](azure-security-data-encryption-best-practices.md)
* [Azure Identity Management 및 액세스 제어 보안 모범 사례](azure-security-identity-management-best-practices.md)
* [Azure 보안 팀 블로그](http://blogs.msdn.com/b/azuresecurity/)
* [Microsoft 보안 대응 센터](https://technet.microsoft.com/library/dn440717.aspx)

