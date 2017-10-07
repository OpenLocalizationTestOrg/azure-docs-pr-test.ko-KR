---
title: "Azure에서 Directory Federation Services aaaActive | Microsoft Docs"
description: "이 문서에서는 살펴보겠습니다 어떻게 toodeploy 고가용성을 위해 Azure의 AD FS 합니다."
keywords: "azure의 AD FS를 배포, azure의 adfs, adfs azure, azure ad fs 배포, adfs 배포, ad fs를 azure의 ad fs를 배포, azure의 adfs 배포, AD FS를 배포 azure, azure ad fs, 소개 tooAD FS, Azure, azure에서 AD FS에서 iaas, ADFS, adfs tooazure를 이동"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 692a188c-badc-44aa-ba86-71c0e8074510
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: anandy; billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2c39271f7569b9ce395dce2f53f5ba5a4897b132
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-active-directory-federation-services-in-azure"></a>Azure에서 Active Directory Federation Services 배포
AD FS는 간편하고 안전한 ID 페더레이션 및 웹 Single Sign-on(SSO) 기능을 제공합니다. Azure AD와 페더레이션 하거나 O365 tooauthenticate 온-프레미스를 사용 하 여 자격 증명 및 클라우드의 모든 리소스에 액세스할 사용자가 선택을 취소 합니다. 결과적으로, 것이 중요 toohave 항상 사용 가능한 AD FS 인프라 tooensure tooresources 온-프레미스에 액세스 하 고 hello 클라우드에서 합니다. Azure의 AD FS 배포 필요한 최소한의 노력으로 hello 높은 가용성을 달성 하는 데 도움이 됩니다.
Azure에서 AD FS를 배포하는 여러 가지 이점의 일부는 다음과 같습니다.

* **고가용성** -항상 사용 가능한 인프라 되도록 있습니다 hello Azure 가용성 집합의 기능입니다.
* **쉬운 tooScale** – 더 많은 성능이 필요한? Azure에서 몇 번의 클릭으로 toomore 강력한 컴퓨터를 쉽게 마이그레이션합니다
* **지역 간 중복성** –와 Azure 지역 중복 hello 전세계 사용자 인프라는 항상 사용 가능한 보장할 수 있습니다
* **쉬운 tooManage** – Azure 포털에서 매우 간소화 된 관리 옵션이 있는 인프라를 관리은 매우 간단 하 고 깔끔한 

## <a name="design-principles"></a>디자인 원칙
![배포 설계](./media/active-directory-aadconnect-azure-adfs/deployment.png)

위의 hello 다이어그램 hello Azure의 AD FS 인프라를 배포 하는 기본 토폴로지 toostart 권장 보여 줍니다. hello 원리 hello hello 토폴로지의 다양 한 구성 요소는 다음과 같습니다.

* **DC/AD FS 서버**: 사용자가 1,000명보다 적은 경우 도메인 컨트롤러에 AD FS 역할을 설치할 수 있습니다. Hello 도메인 컨트롤러에 성능 영향을 받지 않도록 하려는 경우 나 1000 개 이상의 사용자가 사용 하는 경우에 다음 별도 서버에 AD FS를 배포 합니다.
* **WAP 서버** – 사용자가 AD FS 없는 시기 hello 회사 네트워크에도 hello에 연결할 수 있도록 필요한 toodeploy 웹 응용 프로그램 프록시 서버는 합니다.
* **DMZ**: hello 웹 응용 프로그램 프록시 서버 hello DMZ에에서 배치 됩니다 및 hello DMZ와 hello 내부 서브넷 간에 TCP/443만 액세스가 허용 됩니다.
* **부하 분산 장치**: AD FS 및 웹 응용 프로그램 프록시 서버의 고가용성을 tooensure을 권장 웹 응용 프로그램 프록시 서버에 대 한 AD FS 서버와 Azure 부하 분산 장치에 대 한 내부 부하 분산 장치를 사용 합니다.
* **가용성 집합**: tooprovide 중복 tooyour AD FS 배포 것이 좋습니다는 비슷한 작업에 대 한 가용성 집합에 두 개 이상의 가상 컴퓨터를 그룹화 합니다. 이 구성은 계획된 유지 관리 또는 계획되지 않은 유지 관리 이벤트 중에 적어도 하나의 가상 컴퓨터를 사용할 수 있습니다.
* **저장소 계정**: toohave 두 저장소 계정은 것이 좋습니다. 단일 저장소 계정의 toocreation의 단일 실패 지점이 될 수 있습니다 및 hello 배포 toobecome hello 저장소 계정 작동이 나 가능성이 시나리오에서 사용할 수 없게 될 수 있습니다. 두 개의 저장소 계정이 있으면 각 오류 줄에 하나의 저장소 계정을 연결할 수 있습니다.
* **네트워크 분리**: 웹 응용 프로그램 프록시 서버를 별도의 DMZ 네트워크에 배포해야 합니다. 서브넷인 하나의 가상 네트워크를 나눌 수 있으며 다음 격리 된 서브넷에 hello 웹 응용 프로그램 프록시 서버를 배포할 수 있습니다. 단순히 각 서브넷에 대 한 hello 네트워크 보안 그룹 설정을 구성할 수 있으며 hello 두 서브넷 간의 필요한 통신만을 허용. 자세한 내용은 아래 배포 시나리오 별로 지정됩니다.

## <a name="steps-toodeploy-ad-fs-in-azure"></a>단계 toodeploy Azure의 AD FS
이 섹션 개요 hello 가이드 toodeploy hello 아래에 언급 된 hello 단계에 사용 된 Azure의 AD FS 인프라입니다.

### <a name="1-deploying-hello-network"></a>1. Hello 네트워크 배포
위에서 설명한 대로 단일 가상 네트워크에 두 개의 서브넷을 만들거나 두 개의 완전히 다른 가상 네트워크(VNet)를 만들 수 있습니다. 이 문서는 단일 가상 네트워크를 배포하는 데 집중하고 해당 네트워크를 두 개의 서브넷으로 나눕니다. 현재 두 개의 별도 Vnet VNet tooVNet 게이트웨이 통신에 필요한 대로 보다 쉬운 접근입니다.

**1.1 가상 네트워크 만들기**

![가상 네트워크 만들기](./media/active-directory-aadconnect-azure-adfs/deploynetwork1.png)

Hello Azure 포털에서에서 가상 네트워크를 선택 하 고 hello 가상 네트워크 및 한 번의 클릭으로 즉시 서브넷 1 개 배포할 수 있습니다. INT 서브넷도 정의 되어과 이제 Vm toobe 추가 대 한 합니다.
hello 다음 단계는 tooadd 다른 서브넷 toohello 네트워크, 예: DMZ hello 서브넷입니다. toocreate는 DMZ 서브넷을 단순히 hello

* 새로 만든 hello 네트워크 선택
* Hello 속성에서 서브넷을 선택
* 패널 클릭 hello hello 서브넷에 단추 추가
* Hello 서브넷 이름 및 주소 공간 정보 toocreate hello 서브넷을 제공 합니다.

![서브넷](./media/active-directory-aadconnect-azure-adfs/deploynetwork2.png)

![서브넷 DMZ](./media/active-directory-aadconnect-azure-adfs/deploynetwork3.png)

**1.2. Hello 네트워크 보안 그룹 만들기**

네트워크 보안 그룹 NSG ()를 허용 하거나 거부 네트워크 트래픽을 가상 네트워크에서 VM 인스턴스 tooyour 액세스 제어 목록 (ACL) 규칙 목록이 포함 되어 있습니다. NSG는 서브넷 또는 서브넷 내의 개별 VM 인스턴스 중 하나와 연결될 수 있습니다. NSG를 서브넷과 연결 하는 경우 해당 서브넷에 tooall hello VM 인스턴스 hello ACL 규칙에 적용 됩니다.
이 가이드의 hello 용도로 두 Nsg 만듭니다: 마다 하나씩 내부 네트워크 및 DMZ에 대 한 합니다. 각각 NSG_INT 및 NSG_DMZ라는 레이블이 지정됩니다.

![NSG 만들기](./media/active-directory-aadconnect-azure-adfs/creatensg1.png)

NSG 만들어질 hello, 한 후 0 인바운드 및 0 아웃 바운드 규칙 수 있습니다. 일단 hello 역할 hello 해당 서버에 설치 되 면 다음 hello 인바운드 및 아웃 바운드 규칙 가능 따라 toohello 원하는 수준의 보안 합니다.

![NSG 초기화](./media/active-directory-aadconnect-azure-adfs/nsgint1.png)

Hello Nsg를 만든 후 서브넷과 NSG_INT 연결 INT 및 DMZ 서브넷과 NSG_DMZ 합니다. 예제 스크린샷은 다음과 같습니다.

![NSG 구성](./media/active-directory-aadconnect-azure-adfs/nsgconfigure1.png)

* 서브넷에 대 한 서브넷 tooopen hello 패널을 클릭
* Hello NSG 서브넷 tooassociate hello를 선택 합니다. 

구성을 마치면 서브넷에 대 한 hello 패널 다음과 같이 표시 됩니다.

![NSG 이후 서브넷](./media/active-directory-aadconnect-azure-adfs/nsgconfigure2.png)

**1.3. Tooon-프레미스 연결 만들기**

연결 tooon 온-프레미스에서 azure 순서 toodeploy hello 도메인 컨트롤러 (DC)에 필요 합니다. Azure는 다양 한 연결 옵션 tooconnect 온-프레미스 인프라 tooyour Azure 인프라를 제공합니다.

* 지점 및 사이트 간
* Virtual Network 사이트 간
* Express 경로

ExpressRoute toouse 것이 좋습니다. ExpressRoute를 사용하면 온-프레미스 또는 공동 배치 환경의 인프라와 Azure 데이터 센터 간에 개인 연결을 만들 수 있습니다. ExpressRoute 연결은 hello를 통해 이동 하지 않도록 공용 인터넷 합니다. 더 많은 안정성, 빨라진 속도, 낮은 대기 시간 및 일반 연결 보다 보안성이 높으며 hello 인터넷을 통해 제공합니다.
ExpressRoute toouse 것이 좋습니다 경우 조직에 가장 적합 한 모든 연결 방법을 선택할 수 있습니다. ExpressRoute 및 hello에 대 한 자세한 toolearn ExpressRoute를 사용 하 여 다양 한 연결 옵션 읽을 [express 경로 기술 개요](https://aka.ms/Azure/ExpressRoute)합니다.

### <a name="2-create-storage-accounts"></a>2. 저장소 계정 만들기
순서 toomaintain 고가용성에서 단일 저장소 계정에 대 한 종속성을 방지 하 고, 두 개의 저장소 계정을 만들 수 있습니다. 각 가용성 집합의 hello 컴퓨터 두 그룹으로 나누고 별도 저장소 계정을 각 그룹에 할당 합니다.

![저장소 계정 만들기](./media/active-directory-aadconnect-azure-adfs/storageaccount1.png)

### <a name="3-create-availability-sets"></a>3. 가용성 집합 만들기
각 역할 (DC/AD FS 및 WAP)에 대 한 최소 hello에서 2 컴퓨터에 있는 가용성 집합을 만듭니다. 각 역할이 높은 가용성을 달성하는 데 도움이 됩니다. 만드는 hello 가용성 설정 하는 동안 hello 다음에 필수 toodecide 됩니다.

* **오류 도메인**: 가상 컴퓨터에서 동일한 오류 도메인 공유 hello hello 동일한 전원 및 실제 네트워크 스위치입니다. 최소 2개의 장애 도메인을 사용하는 것이 좋습니다. hello 기본값은 3 이며이 배포의 hello 용도로 그대로 둘 수 있습니다.
* **업데이트 도메인**: 속하는 toohello 업데이트 하는 동안 동일한 업데이트 도메인은 함께 다시 시작 하는 컴퓨터입니다. Toohave 최소를 2 업데이트 도메인을 사용 하는 것이 좋습니다. hello 기본값은 5이 고이 배포의 hello 용도로 그대로 둘 수 있습니다.

![가용성 집합](./media/active-directory-aadconnect-azure-adfs/availabilityset1.png)

Hello 가용성 집합 만들기

| 가용성 집합 | 역할 | 장애 도메인 | 업데이트 도메인 |
|:---:|:---:|:---:|:--- |
| contosodcset |DC/ADFS |3 |5 |
| contosowapset |WAP |3 |5 |

### <a name="4-deploy-virtual-machines"></a>4. 가상 컴퓨터 배포
hello 다음 단계는 hello 인프라의 다른 역할을 호스트할 toodeploy 가상 컴퓨터. 각 가용성 집합에서 최소 두 대의 컴퓨터를 사용하는 것이 좋습니다. Hello 기본 배포에 대 한 4 개의 가상 컴퓨터를 만듭니다.

| 컴퓨터 | 역할 | 서브넷 | 가용성 집합 | Storage 계정 | IP 주소 |
|:---:|:---:|:---:|:---:|:---:|:---:|
| contosodc1 |DC/ADFS |INT |contosodcset |contososac1 |정적 |
| contosodc2 |DC/ADFS |INT |contosodcset |contososac2 |정적 |
| contosowap1 |WAP |DMZ |contosowapset |contososac1 |정적 |
| contosowap2 |WAP |DMZ |contosowapset |contososac2 |정적 |

보시는 것처럼 NSG가 지정되지 않았습니다. 즉, azure hello 서브넷 수준에서 NSG를 사용할 수 있습니다. 그런 다음 중 하나 hello 서브넷. 그렇지 않으면 hello NIC 개체와 관련 된 개별 NSG hello를 사용 하 여 컴퓨터 네트워크 트래픽을 제어할 수 있습니다. 자세한 내용은 [NSG(네트워크 보안 그룹)란](https://aka.ms/Azure/NSG)을 참고하세요.
Hello DNS을 관리 하는 경우에 고정 IP 주소는 것이 좋습니다. Azure DNS를 사용할 수 있으며 대신 hello 도메인에 대 한 DNS 레코드를 자신의 Azure Fqdn으로 새 컴퓨터 toohello 참조.
가상 컴퓨터 창의 hello 배포가 완료 된 후 다음과 같이 표시 됩니다.

![배포된 Virtual Machines](./media/active-directory-aadconnect-azure-adfs/virtualmachinesdeployed_noadfs.png)

### <a name="5-configuring-hello-domain-controller--ad-fs-servers"></a>5. 구성 hello 도메인 컨트롤러 / AD FS 서버
 순서 tooauthenticate에서 들어오는 모든 요청을 AD FS toocontact hello 도메인 컨트롤러를 해야 합니다. toosave hello 인증을 위해 Azure tooon 온-프레미스 DC에서 비용이 많이 드는 여행, 것이 좋습니다 toodeploy Azure의 hello 도메인 컨트롤러의 복제 합니다. 순서 tooattain 고가용성에 최소 2 도메인 컨트롤러의 한 가용성 집합 toocreate를 좋습니다.

| 도메인 컨트롤러 | 역할 | Storage 계정 |
|:---:|:---:|:---:|
| contosodc1 |복제본 |contososac1 |
| contosodc2 |복제본 |contososac2 |

* 두 서버 hello dns 복제본 도메인 컨트롤러로 승격
* Hello 서버 관리자를 사용 하 여 hello AD FS 역할을 설치 하 여 hello AD FS 서버를 구성 합니다.

### <a name="6-deploying-internal-load-balancer-ilb"></a>6. ILB(내부 부하 분산 장치) 배포
**6.1. ILB hello 만들기**

toodeploy 받는 ILB를 클릭 하 고 hello Azure 포털에서 선택 부하 분산 장치 (+)를 추가합니다.

> [!NOTE]
> 표시 되지 않으면 **부하 분산 장치** 메뉴를 클릭 **찾아보기** hello hello 포털의 왼쪽 아래에 표시 될 때까지 스크롤 **부하 분산 장치**합니다.  Hello 노란색 별표 tooadd 클릭 것 tooyour 메뉴. 이제 hello 새 부하 분산 장치 아이콘 tooopen hello 패널 toobegin 구성 hello 부하 분산 장치를 선택 합니다.
> 
> 

![부하 분산 장치 찾아보기](./media/active-directory-aadconnect-azure-adfs/browseloadbalancer.png)

* **이름**: 모든 적절 한 이름을 toohello 부하 분산 장치를 제공 합니다.
* **구성표**:이 부하 분산 장치 hello AD FS 서버 앞에 배치할 수 있고 내부 네트워크 연결 "내부"를 선택만 위한 것입니다
* **가상 네트워크**: AD FS를 배포 하는 hello 가상 네트워크를 선택 합니다.
* **서브넷**: hello 내부 서브넷 여기를 선택 합니다.
* **IP 주소 할당**: 정적

![내부 부하 분산 장치](./media/active-directory-aadconnect-azure-adfs/ilbdeployment1.png)

클릭 한 후 만들기 및 배포 된 hello ILB, 부하 분산 장치의 hello 목록에 표시 됩니다.

![ILB 이후 부하 분산 장치](./media/active-directory-aadconnect-azure-adfs/ilbdeployment2.png)

다음 단계는 tooconfigure hello 백 엔드 풀 및 hello 백 엔드 프로브 합니다.

**6.2. ILB 백 엔드 풀 구성**

새로 만든 ILB의 hello 부하 분산 장치 패널 선택 번호입니다. Hello 설정 패널을 열립니다. 

1. Hello 설정 패널에서 백 엔드 풀을 선택 합니다.
2. 가상 컴퓨터를 추가 하는 클릭, hello에서 백 엔드 풀 패널 추가
3. 가용성 집합을 선택할 수 있는 패널로 나타납니다.
4. AD FS hello 가용성 집합 선택

![ILB 백 엔드 풀 구성](./media/active-directory-aadconnect-azure-adfs/ilbdeployment3.png)

**6.3. 프로브 구성**

Hello ILB 설정 패널에서 프로브를 선택 합니다.

1. 추가를 클릭합니다.
2. 프로브에 대한 세부 정보를 제공합니다. a. **이름**: 이름을 검색합니다. b. **프로토콜**: TCP c. **포트**: 443(HTTPS) d. **간격**: 5 (기본값)-이 hello 간격 ILB는 hello 백 엔드 풀 e의에서 hello 컴퓨터를 검색 합니다. **비정상 임계값 제한**: 2 (기본 val ue) – 지나면 ILB는 컴퓨터에서에서 선언 hello 백 엔드 풀 속도 응답 하지 않는 송신 트래픽 tooit 연속 프로브 오류의 hello 임계값입니다.

![ILB 프로브 구성](./media/active-directory-aadconnect-azure-adfs/ilbdeployment4.png)

**6.4. 부하 분산 규칙 만들기**

순서 tooeffectively 균형 hello 트래픽이 부하 분산 규칙으로 hello ILB를 구성 해야 합니다. 순서 toocreate 부하 분산 규칙에 

1. 부하 분산 규칙 hello ILB의 hello 설정 패널에서 선택 합니다.
2. 부하 분산 규칙 패널 hello에서 추가 클릭
3. 부하 분산 규칙 패널 추가 hello에 한 합니다. **이름**: hello 규칙 b에 대 한 이름을 제공 합니다. **프로토콜**: TCP를 선택합니다. c. **포트**: 443 d. **백 엔드 포트**: 443 e. **백 엔드 풀**: hello AD FS 클러스터 이전 f에 대해 만든 hello 풀을 선택 합니다. **프로브**: 이전에 AD FS 서버에 대 한 만든 선택 hello 프로브

![ILB 분산 규칙 구성](./media/active-directory-aadconnect-azure-adfs/ilbdeployment5.png)

**6.5. ILB를 사용하여 DNS 업데이트**

DNS 서버 tooyour 이동한 다음 ILB hello에 대 한 CNAME을 만들어야 합니다. hello CNAME hello 페더레이션 서비스에 대 한 hello ILB의 toohello IP 주소를 가리키는 hello IP 주소를 사용 해야 합니다. 예를 들어 hello ILB DIP 주소가 10.3.0.8, 이며 hello 페더레이션 서비스가 설치 된 경우 fs.contoso.com, 그런 다음 fs.contoso.com too10.3.0.8 가리키는 CNAME을 만듭니다.
이렇게 하면 모든 hello ILB에서 fs.contoso.com 종료에 대 한 통신 및은 적절 하 게 라우팅되는지 합니다.

### <a name="7-configuring-hello-web-application-proxy-server"></a>7. Hello 웹 응용 프로그램 프록시 서버 구성
**7.1. Hello 웹 응용 프로그램 프록시 서버, tooreach AD FS 서버를 구성합니다.**

웹 응용 프로그램 프록시 서버는 주문 tooensure hello ILB 뒤에 수 tooreach hello AD FS 서버의 ILB hello에 대 한 hello %systemroot%\system32\drivers\etc\hosts에서 레코드를 만듭니다. 고유 이름 (DN) hello는 hello 페더레이션 서비스 이름, 예를 들어 fs.contoso.com 해야 합니다. 하며 hello IP 항목 hello ILB의 IP 주소 (10.3.0.8 hello 예제와 같이)에 해당 해야 합니다.

**7.2. Hello 웹 응용 프로그램 프록시 역할을 설치**

웹 응용 프로그램 프록시 서버 뒤에 ILB 수 tooreach hello AD FS 서버 인지 확인 한 후에 다음 hello 웹 응용 프로그램 프록시 서버를 설치할 수 있습니다. 웹 응용 프로그램 프록시 서버의 도메인에 가입된 toohello 되지는지 않습니다. Hello 원격 액세스 역할을 선택 하 여 두 명의 웹 응용 프로그램 프록시 서버 hello에 hello 웹 응용 프로그램 프록시 역할을 설치 합니다. hello 서버 관리자는 toocomplete hello WAP 설치를 안내 합니다.
Toodeploy WAP를 읽는 방법에 대 한 자세한 내용은 [설치 하 고 웹 응용 프로그램 프록시 서버 hello 구성](https://technet.microsoft.com/library/dn383662.aspx)합니다.

### <a name="8--deploying-hello-internet-facing-public-load-balancer"></a>8.  Hello 인터넷 연결 (공용) 부하 분산 장치 배포
**8.1.  인터넷 연결 (공용) 부하 분산 장치 만들기**

Hello Azure 포털에서에서 부하 분산 장치를 선택 하 고 추가 클릭 합니다. Hello 만들기 부하 분산 장치 패널에서 다음 정보는 hello를 입력 합니다.

1. **이름**: hello 부하 분산 장치에 대 한 이름
2. **구성표**: 공용 – 이 옵션에서는 이 부하 분산 장치에 공용 주소가 필요하다는 것을 Azure에 알립니다.
3. **IP 주소**: 새로운 IP 주소(동적) 만들기

![인터넷 연결 부하 분산 장치](./media/active-directory-aadconnect-azure-adfs/elbdeployment1.png)

배포 후 hello 부하 분산 장치는 hello 부하 분산 장치 목록에 표시 됩니다.

![부하 분산 장치 목록](./media/active-directory-aadconnect-azure-adfs/elbdeployment2.png)

**8.2. DNS 레이블 toohello 공용 IP 할당**

구성에 대 한 hello 패널을 부하 분산 장치 패널 toobring hello에에서 새로 만든 hello 부하 분산 장치 항목을 클릭 합니다. Hello 공용 IP에 대 한 단계 tooconfigure hello DNS 레이블 아래 따릅니다.

1. Hello 공용 IP 주소를 클릭 합니다. Hello 공용 IP에 대 한 hello 패널 및 해당 설정을 열립니다.
2. 구성을 클릭합니다.
3. DNS 레이블을 제공합니다. 이 예를 들어 contosofs.westus.cloudapp.azure.com 어디에서 나 액세스할 수 있는 hello 공용 DNS 레이블이 됩니다. 항목을 추가할 수 hello에 외부 DNS hello hello 외부의 toohello DNS 레이블을 확인 되는 (예: fs.contoso.com) 페더레이션 서비스에 대 한 부하 분산 장치 (contosofs.westus.cloudapp.azure.com).

![인터넷 연결 부하 분산 장치 구성](./media/active-directory-aadconnect-azure-adfs/elbdeployment3.png) 

![인터넷 연결 부하 분산 장치 구성(DNS)](./media/active-directory-aadconnect-azure-adfs/elbdeployment4.png)

**8.3. 인터넷 연결 (공용) 부하 분산 장치에 대한 백 엔드 풀 구성** 

Hello 내부 부하 분산 장치 만들기와 같이 동일한 단계를 따라 hello tooconfigure hello 백 엔드 풀 hello 가용성으로 부하 분산 장치 인터넷 (공용) 연결에 대 한 hello WAP 서버에 대 한 설정입니다. 예를 들어 contosowapset입니다.

![인터넷 연결 부하 분산 장치의 백 엔드 풀 구성](./media/active-directory-aadconnect-azure-adfs/elbdeployment5.png)

**8.4. 프로브 구성**

Hello hello 내부 부하 분산 장치 tooconfigure hello 프로브 WAP 서버 hello 백 엔드 풀에 대 한 구성에서 같이 동일한 단계를 따릅니다.

![인터넷 연결 부하 분산 장치의 프로브 구성](./media/active-directory-aadconnect-azure-adfs/elbdeployment6.png)

**8.5. 부하 분산 규칙 만들기**

Hello ILB tooconfigure hello 부하 분산와 같은 단계 TCP 443에 대 한 규칙을 따릅니다.

![인터넷 연결 부하 분산 장치의 분산 규칙 구성](./media/active-directory-aadconnect-azure-adfs/elbdeployment7.png)

### <a name="9-securing-hello-network"></a>9. Hello 네트워크 보안
**9.1. Hello 내부 서브넷 보안 설정**

Hello tooefficiently 순서에 따라 hello 아래와 같은 내부 서브넷 보안 규칙에 따라 필요한 전반적으로

| 규칙 | 설명 | 흐름 |
|:--- |:--- |:---:|
| AllowHTTPSFromDMZ |DMZ에서 hello HTTPS 통신을 허용 합니다. |인바운드 |
| DenyInternetOutbound |액세스 toointernet 없음 |아웃바운드 |

![INT 액세스 규칙(인바운드)](./media/active-directory-aadconnect-azure-adfs/nsg_int.png)

[주석]: <> (![INT 액세스 규칙(인바운드)](./media/active-directory-aadconnect-azure-adfs/nsgintinbound.png)) [주석]: <> (![INT 액세스 규칙(아웃바운드)](./media/active-directory-aadconnect-azure-adfs/nsgintoutbound.png))

**9.2. Hello DMZ 서브넷 보안 설정**

| 규칙 | 설명 | 흐름 |
|:--- |:--- |:---:|
| AllowHTTPSFromInternet |인터넷 toohello DMZ에서에서 HTTPS를 허용 합니다. |인바운드 |
| DenyInternetOutbound |차단 된 HTTPS toointernet 제외 하 고 |아웃바운드 |

![EXT 액세스 규칙(인바운드)](./media/active-directory-aadconnect-azure-adfs/nsg_dmz.png)

[주석]: <> (![EXT 액세스 규칙(인바운드)](./media/active-directory-aadconnect-azure-adfs/nsgdmzinbound.png)) [주석]: <> (![EXT 액세스 규칙(아웃바운드)](./media/active-directory-aadconnect-azure-adfs/nsgdmzoutbound.png))

> [!NOTE]
> 클라이언트 사용자 인증서 인증(X509 사용자 인증서를 사용하는 clientTLS 인증)이 필요한 경우 AD FS는 TCP 포트 49443를 인바운드 액세스에 사용하도록 설정해야 합니다.
> 
> 

### <a name="10-test-hello-ad-fs-sign-in"></a>10. 테스트 hello AD FS 로그인
hello 가장 쉬운 방법은 hello IdpInitiatedSignon.aspx 페이지를 사용 하 여 AD FS가 tootest입니다. 에 필요한 tooenable 순서 toobe 수 toodo IdpInitiatedSignOn hello AD FS 속성에 hello 합니다. AD FS 설치 tooverify 아래 hello 단계를 수행 합니다.

1. 실행 hello tooset PowerShell을 사용 하 여 hello AD FS 서버의 cmdlet 아래 것 tooenabled 합니다.
   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true 
2. 외부 컴퓨터에서 https://adfs.thecloudadvocate.com/adfs/ls/IdpInitiatedSignon.aspx에 액세스합니다.  
3. AD FS hello 페이지가 표시 되어야 다음과 유사한:

![테스트 로그인 페이지](./media/active-directory-aadconnect-azure-adfs/test1.png)

성공적으로 로그인하면 아래와 같은 성공 메시지가 표시됩니다.

![테스트 성공](./media/active-directory-aadconnect-azure-adfs/test2.png)

## <a name="template-for-deploying-ad-fs-in-azure"></a>Azure에서 AD FS를 배포하는 템플릿
hello 템플릿 2 각 도메인 컨트롤러, AD FS 및 WAP 6 컴퓨터 설치 프로그램을 배포합니다.

[Azure 배포 템플릿에서 AD FS](https://github.com/paulomarquesc/adfs-6vms-regular-template-based)

이 템플릿을 배포하는 동안 기존 가상 네트워크를 사용하거나 새 VNET을 만들 수 있습니다. hello hello 배포 사용자 지정에 사용할 수 있는 다양 한 매개 변수는 hello hello 배포 프로세스에 hello 매개 변수 사용에 대 한 설명에 다음과 같습니다. 

| 매개 변수 | 설명 |
|:--- |:--- |
| 위치 |지역 toodeploy hello 리소스 예: 미국 동부로 hello 하 고 있습니다. |
| StorageAccountType |hello 유형의 hello 만든 저장소 계정 |
| VirtualNetworkUsage |새 가상 네트워크를 만들지 아니면 기존 가상 네트워크를 사용할지를 나타냅니다. |
| VirtualNetworkName |기존 또는 새 가상 네트워크 사용량에 필수 hello 가상 네트워크 tooCreate의 hello 이름 |
| VirtualNetworkResourceGroupName |Hello hello 기존 가상 네트워크가 있는 hello 리소스 그룹 이름을 지정 합니다. 기존 가상 네트워크를 사용할 경우이 필수 매개 변수 hello 배포 hello 기존 가상 네트워크의 hello ID를 찾을 수 있도록 |
| VirtualNetworkAddressRange |hello의 주소 범위를 hello 새 VNET을 새 가상 네트워크를 만드는 경우 필수 |
| InternalSubnetName |두 가상 네트워크 사용 옵션 (새로운 또는 기존)에서 필수 hello 내부 서브넷의 hello 이름 |
| InternalSubnetAddressRange |hello 새 가상 네트워크를 만드는 경우 hello 도메인 컨트롤러 및 ADFS 서버를 필수를 포함 하는 hello 내부 서브넷의 주소 범위입니다. |
| DMZSubnetAddressRange |hello hello Windows 응용 프로그램 프록시 서버를 새 가상 네트워크를 만드는 경우에 필수를 포함 하는 hello dmz 서브넷의 주소 범위입니다. |
| DMZSubnetName |두 가상 네트워크 사용 옵션 (새로운 또는 기존)에서 필수 hello 내부 서브넷의 hello 이름입니다. |
| ADDC01NICIPAddress |내부 IP 주소 hello hello 첫 번째 도메인 컨트롤러,이 IP 주소 toohello DC 정적으로 할당 될 및 hello 내부 서브넷 내에서 유효한 ip 주소 여야 합니다. |
| ADDC02NICIPAddress |내부 IP 주소 hello hello 두 번째 도메인 컨트롤러,이 IP 주소 toohello DC 정적으로 할당 될 및 hello 내부 서브넷 내에서 유효한 ip 주소 여야 합니다. |
| ADFS01NICIPAddress |hello 내부 IP 주소 hello 첫 번째 ad FS 서버에서는이 IP 주소 toohello ADFS 서버 정적으로 할당 될 및 hello 내부 서브넷 내에서 유효한 ip 주소 여야 합니다. |
| ADFS02NICIPAddress |hello 내부 IP 주소 hello 두 번째 ADFS 서버에서는이 IP 주소 toohello ADFS 서버 정적으로 할당 될 및 hello 내부 서브넷 내에서 유효한 ip 주소 여야 합니다. |
| WAP01NICIPAddress |hello 내부 IP 주소 hello 첫 번째 WAP 서버에서는이 IP 주소 toohello WAP 서버 정적으로 할당 될 및 hello DMZ 서브넷 내에서 유효한 ip 주소 여야 합니다. |
| WAP02NICIPAddress |hello 내부 IP 주소 hello 두 번째 WAP 서버에서는이 IP 주소 toohello WAP 서버 정적으로 할당 될 및 hello DMZ 서브넷 내에서 유효한 ip 주소 여야 합니다. |
| ADFSLoadBalancerPrivateIPAddress |hello hello ADFS 내부 IP 주소를 부하 분산 장치,이 IP 주소 toohello 부하 분산 장치 정적으로 할당 될 및 hello 내부 서브넷 내에서 유효한 ip 주소 여야 합니다. |
| ADDCVMNamePrefix |도메인 컨트롤러의 가상 컴퓨터 이름 접두사입니다. |
| ADFSVMNamePrefix |ADFS 서버의 가상 컴퓨터 이름 접두사입니다. |
| WAPVMNamePrefix |WAP 서버의 가상 컴퓨터 이름 접두사입니다. |
| ADDCVMSize |hello 도메인 컨트롤러의 hello vm 크기 |
| ADFSVMSize |hello ADFS 서버 hello vm 크기 |
| WAPVMSize |hello WAP 서버 hello vm 크기 |
| AdminUserName |hello 이름 hello hello 가상 컴퓨터의 로컬 관리자 |
| AdminPassword |hello hello 가상 컴퓨터의 로컬 관리자 계정에 대 한 hello 암호 |

## <a name="additional-resources"></a>추가 리소스
* [가용성 집합](https://aka.ms/Azure/Availability) 
* [Azure 부하 분산 장치](https://aka.ms/Azure/ILB)
* [내부 부하 분산 장치](https://aka.ms/Azure/ILB/Internal)
* [인터넷 연결 부하 분산 장치](https://aka.ms/Azure/ILB/Internet)
* [Storage 계정](https://aka.ms/Azure/Storage)
* [Azure Virtual Networks](https://aka.ms/Azure/VNet)
* [AD FS 및 웹 응용 프로그램 프록시 링크](http://aka.ms/ADFSLinks) 

## <a name="next-steps"></a>다음 단계
* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)
* [Azure AD Connect를 사용하여 AD FS 구성 및 관리](active-directory-aadconnectfed-whatis.md)
* [Azure Traffic Manager를 사용하여 Azure에서 고가용성 교차 지리적 AD FS 배포](../active-directory-adfs-in-azure-with-azure-traffic-manager.md)

