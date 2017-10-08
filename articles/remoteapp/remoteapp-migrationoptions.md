---
title: "Azure RemoteApp에서 마이그레이션하기 위한 aaaOptions | Microsoft Docs"
description: "Azure RemoteApp에서 마이그레이션에 대 한 hello 옵션에 알아봅니다."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c4e0e5bc-5c13-4487-b1b6-ebf2a5edc1f0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 75324597881520d0c75939983b728ae9bbd7f436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="options-for-migrating-out-of-azure-remoteapp"></a>Azure RemoteApp에서 마이그레이션하기 위한 옵션
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.


Hello 때문에 Azure RemoteApp을 사용 하 여를 중지 한 경우 [중지를 알린](https://go.microsoft.com/fwlink/?linkid=821148) 또는 평가 마친 toomigrate Azure RemoteApp tooanother 앱 서비스에서 필요 합니다. 마이그레이션에는 두 가지 방식, 즉 자체 관리형 솔루션(종종 IaaS(Infrastructure as a Service)라고 함) 배포 또는 완전 관리형 제품(종종 PaaS(Platform as a Service)/SaaS(Software as a Service)라고 함)이 있습니다. 

자체 관리형 IaaS는 VM(가상 컴퓨터) 또는 실제 시스템에 직접 배포되어 사용자가 관리, 운영 및 소유하는 자체(DIY) 배포입니다. 다른 hello에서는 완전히 관리 되는 PaaS/SaaS 제공 Azure RemoteApp 것과 유사 합니다-작업을 처리 하는 원격 솔루션 기반으로 서비스 계층을 제공 하는 파트너를 종료 하 고 서비스를 제공 하는 동안, hello 고객으로 서 실행 일부 이미지 및 앱 관리.

[마이그레이션 옵션에 hello Azure RemoteApp 웹 세미나를 보려면](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp)에 대 한 자세한 정보 (hello 다른 호스팅 옵션의 예 포함)에 대 한 읽기 또는 합니다.

## <a name="self-managed-iaas-solutions"></a>자체 관리형 솔루션(IaaS)
### <a name="rds-on-iaas"></a>**IaaS의 RDS**
RemoteApp이나 온-프레미스 또는 호스팅된 환경에 속한 데스크톱(예: Azure VM)을 사용하면 네이티브 세션 기반 원격 데스크톱 서비스(Windows Server) 배포본을 배포할 수 있습니다. RDS 배포에 이미 익숙하고 기존 기술 전문 지식을 갖춘 고객에게는 IaaS에 대한 RDS 배포가 가장 적합합니다. 

> [!NOTE]
> 볼륨 라이선스 소프트웨어 보증 (SA)와 필요한 RDS 클라이언트 액세스 라이선스 toouse이 배포 옵션입니다.

Azure VM에 RDS를 배포하는 것은 템플릿을 배포/패치하는 것보다 쉽습니다([개요](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) 참조 및 [가져오기](https://aka.ms/rdautomation)). Hello를 사용 하 여 hello Azure RemoteApp 내에서 Azure 클래식 배포 모델 리소스 (Azure 리소스 모델 리소스가 아닌)와 동일한 탄력적인 크기 조정 기능을 가져올 수 있습니다 [자동 스크립트 확장](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76)더 많은 요소가 있지만, 사용자 지정 및 구성 합니다. 통해 기능은 지원 Azure Vm에서 RDS를 배포 하면 [Azure 지원](https://azure.microsoft.com/support/plans/), Azure RemoteApp과 함께 지원 하면 동일한 지원 전문가 hello 합니다. 에 연결 하 여 기존 사용량을 기준으로 예상 비용 얻을 수 있습니다 [Azure 지원](https://azure.microsoft.com/support/plans/), 또는 계산을 직접 수행할 수 있습니다를 사용 하 여는 곧 toobe 비용 계산기를 해제 합니다.  또한 N 시리즈 Vm (현재 비공개 미리 보기)에 추가할 수 있습니다 vGPU-vGPU를 추가 하는 방법에 대 한 및 방법에 대 한 더를 너무 들[Windows Server 2016의 RDS 향상 기능을 활용](https://myignite.microsoft.com/videos/2794) 우리의 Ignite 세션에서 합니다.   

에 대 한 단계별 배포 가이드를 했으므로 [Windows Server 2012 R2](http://aka.ms/rdsonazure) 및 [Windows Server 2016](http://aka.ms/rdsonazure2016) 배포와 tooassist 합니다. 체크 아웃 hello [원격 데스크톱 블로그](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) 최신 뉴스 hello에 대 한 합니다.

### <a name="citrix-on-iaas"></a>**IaaS의 Citrix**
세션 기반 XenApp 또는 XenDesktop의 네이티브 Citrix 배포본은 온-프레미스 또는 호스팅된 환경(예: Azure VM)에 배포할 수 있습니다. 

Hello 단계별 배포 가이드를 확인해 보세요 [Azure에서 Citrix XA 7.6](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), 자세한 정보에 대 한 합니다. 가격 계산기를 포함하여 [Azure에서 Citrix](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx)에 대해 자세히 알아보세요. 찾을 수 있습니다는 [Citrix 연락처](http://citrix.com/English/contact/index.asp) toodiscuss 사용 하 여 옵션입니다.

## <a name="fully-managed-paassaas-offerings"></a>완전 관리형 제품(PaaS/SaaS)

### <a name="citrix-xenapp-essentials-released-april-2017"></a>Citrix XenApp Essentials(2017년 4월 출시)
Hello에 지금 사용 가능 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials hello 새 응용 프로그램 가상화 서비스는 hello 전원 결합 및 유연성의 hello hello simple 규범적인와 Citrix 클라우드 플랫폼 및 Microsoft Azure RemoteApp의 사용 하기 쉬운 비전 합니다. 

기존 Azure RemoteApp 고객은 [평가판 등록](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/)이 가능합니다.  참고: Citrix 사용자 서비스 요금만 무료이며 Azure 계산 및 저장소 비용은 적용됩니다.

자세한 정보:
- [Azure RemoteApp tooCitrix XenApp Essentials에서 마이그레이션](remoteapp-migrate-citrix.md)
- [Citrix 및 Microsoft](https://www.citrix.com/global-partners/microsoft/remote-app.html)
- [Citrix XenApp Essentials 프레젠테이션](https://www.youtube.com/watch?v=91Z7CCfQ-9k)  

### <a name="citrix-cloud-xenapp-service-and-xendesktop-service"></a>Citrix 클라우드 XenApp 서비스 및 XenDesktop 서비스 

[Citrix 클라우드 XenApp 서비스와 XenDesktop 서비스](https://www.citrix.com/products/citrix-cloud/services.html) hello hello 배달 모두 응용 프로그램 및 데스크톱 및 고급 관리 및 모니터링 기능에 대 한 최상의 솔루션입니다. 

#### <a name="conexlink-platform-name-mycloudit"></a>Conexlink(플랫폼 이름: MyCloudIT)
[MyCloudIT](https://mycloudit.com) 은 원격 데스크톱 및 원격 응용 프로그램에서 인프라의 배달에는 Microsoft Azure 클라우드 hello 및 IT 회사 toosimplify에 대 한 자동화 플랫폼 최적화 하며 hello 마이그레이션의 크기를 조정 합니다. 

hello MyCloudIT 플랫폼 95%, 30% 비용 Azure 배포 시간이 단축 되 고 몇 가지 키 입력 하는 것에 hello 클라우드로 해당 클라이언트의 전체 IT 인프라를 이동 합니다. 파트너 하나의 전역 대시보드에서 이제 고객을 관리할 수, 서비스 최종 사용자에 게 hello 전 세계 이전과 전혀 광범위 한 Azure 트레이닝 또는 추가 오버 헤드를 추가 하지 않고 수익을 증가.  

> 기본 위치: 미국 텍사스주 댈러스
> 
> 작업 영역: 전 세계
> 
> 파트너 관계 상태: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)
> 
> Microsoft 클라우드 서비스 공급자: 예
> 
> 세션 기반 RemoteApp 및 데스크톱 솔루션 제공: 예, 둘 다
> 
> Azure RemoteApp 마이그레이션 솔루션: 예, [자세한 정보](https://mycloudit.com/remote-app-microsoft/)
> 
> Brian Garoutte, 비즈니스 개발 부사장
> 
> 전화 번호: 972-218-0741
>   
> 메일: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)

### <a name="frame"></a>프레임

IT 조직에서 엔터프라이즈 및 정부, 관리 되는 서비스 공급자, 선행 소프트웨어 공급 업체에서 toocreate 프레임을 선택 하 고 hello 클라우드에서 자신의 안전 하 고, 소프트웨어 정의 작업 영역을 관리 합니다. 작은 toolarge 조직 으로부터 프레임 사용 하면 사용자가 쉽게 toolet 모든 장치에서 모든 브라우저에 Windows 응용 프로그램에 액세스 합니다. hello 프레임 플랫폼 모든 포함 된 hello Azure 인프라 및 RDS 라이선스를 포함 하 여 hello 클라우드에서 관리 요구 toodeploy 응용 프로그램 (사용자 고유의 Azure 계정 및 라이선스는 선택 사항). 

[Azure의 프레임](https://www.fra.me/ara)에 대해 자세히 알아봅니다. 

> 기본 위치: 샌마티오, 캘리포니아, 미국
>
> 작업 영역: 전 세계
>
> Microsoft 파트너: 예
> 
> 전화 번호: 1-480-269-4668

### <a name="awingu"></a>Awingu
Awingu에서는 html5 브라우저에서 레거시 앱, SaaS 및 문서를 실행하는 간단한 온라인 작업 영역 솔루션을 제공합니다. 따라서 모든 종류의 장치에서 모든 응용 프로그램을 안전하게 사용할 수 있습니다. SaaS 서비스에 대해 광범위한 op Single Sign-On 옵션을 사용할 수 있습니다. 또한 다양한 파일 시스템(클라우드 포함)을 작업 영역에 통합할 수 있습니다. 다음 toofull 이동성 Awingu의 풍부한 온라인 작업 영역 세분화 된 컨트롤 (예: 다운로드/업로드), 감사, Multi-factor Authentication (예: Azure MFA), 세션 기록 등 전체 사용량 최적의 보안을 제공 합니다. 기본적으로 Awingu를 사용하면 문서 및 응용 프로그램 세션 공유에서 안전한 공동 작업을 최적화할 수 있습니다.
Awingu의 솔루션은 다중 테넌트, 다중 AD 및 오픈 API입니다. 중소기업 및 대기업, 클라우드 서비스 공급자 및 [ISV](http://www.isv2saas.com)에서 사용합니다. 이러한 고객은 특히 hello의 편리한, 유용한 쉽게 설치 하 고 낮은 TCO 합니다.

Awingu 내부에서 올인원은 [hello Azure Marketplace에서에서 사용할 수 있는](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) 2 기본 제공 동시 사용자와 합니다. 추가 라이선스는 [광범위한 배포자 및 판매점](http://www.awingu.com/reseller)을 통해 사용할 수 있습니다.

에 대 한 자세한 내용은 [대체 tooAzure RemoteApp으로에 Awingu](http://alternative-for-azure-remoteapp.awingu.com/)합니다.


> 기본 위치: 벨기에
> 
> 운영 지역: EMEA, 북미 및 브라질
> 
> 세션 기반 RemoteApp 및 데스크톱 솔루션 제공: 예, 둘 다 
> 
> **전역**:
> 
> Arnaud Marlière, CMO
> 
> 메일: [arnaud@awingu.com](mailto:arnaud@awingu.com)
> 
> 전화 번호: +1 646 583 3025
> 
> **벨기에 HQ**:
> 
> Ottergemsesteenweg-Zuid 808 B44
> 
> 9000 Gent
> 
> 메일: [info@awingu.com](mailto:info@awingu.com) 
> 
> 전화 번호: + 32 9 296 40 11
> 
> **USA**:
> 
> 7을 나타내며의 hello Americas, 1177 Ave
> 
> 뉴욕, NY 10036
> 
> 메일: [info.us@awingu.com](mailto:info.us@awingu.com)

### <a name="microsoft-hosted-service-provider"></a>Microsoft 호스티드 서비스 공급자
호스팅 파트너 완전히 관리 되는 호스팅된 Windows 데스크톱 및 Azure 리소스, 운영 체제, 응용 프로그램 관리를 포함할 수 있는 응용 프로그램 서비스 hello 및 기술 지원팀 파트너 hello를 사용 하 여 Microsoft와 계약을 라이선스의 일반적으로 제공 하 고 서비스 공급자 사용권 계약 tooallow 재판매 구독자 액세스 라이선스 (SAL) 되 고 함께 기타 소프트웨어 공급자입니다. hello 다음과 같은 정보가 세부 정보를 제공 hello 호스팅 서비스 공급자가 Azure RemoteApp 마이그레이션을 고객 지원에 특수화 하는 중 일부에 대 한 연락처 정보입니다. 체크 아웃 [호스팅 서비스 공급자의 현재 목록을 hello](http://aka.ms/rdsonazurecertified) hello 학습 경로 및 평가 하는 IaaS에서 RDS를 완료 합니다.  

### <a name="citrix-service-provider-program"></a>Citrix 서비스 공급자 프로그램
hello Citrix 서비스 공급자 프로그램 쉽게 tooSMBs 컴퓨팅, 쉬운, 종 량 제 모델에서 원하는 hello 서비스를 제공 하는 가상 클라우드 서비스 공급자 toodeliver hello 간소화 합니다. Citrix 서비스 공급자 Microsoft SPLA 비즈니스를 성장 및 RDS 플랫폼 투자를 확장 하 고 모든 장치, 원격 액세스, 광범위 한 응용 프로그램 지원, 풍부한 환경을, 추가 보안 및 향상 된 확장성 hello 합니다. 이에 따라 Citrix 서비스 공급자는 구독자를 더 많이 유치하며, 고객 만족도를 높이고, 운영 비용을 절감합니다. [자세한 정보](http://www.citrix.com/products/service-providers.html) 또는 [파트너 찾기](https://www.citrix.com/buy/partnerlocator.html)

#### <a name="acuutech"></a>Acuutech
[Acuutech](http://www.acuutech.com) 전체 데스크톱 및 ISV 응용 프로그램을 제공 하는 호스팅된 데스크톱 솔루션을 제공 하는 전문으로 Azure와 자체 데이터 센터에서 Microsoft 기술 tooa 전역 클라이언트 기반 기반 경험 합니다.

> 기본 위치: 영국 런던, 싱가포르, 미국 텍사스주 휴스턴
> 
> 작업 영역: 전 세계
> 
> 파트너 관계 상태: Gold
> 
> Microsoft 클라우드 서비스 공급자: 예
> 
> 세션 기반 RemoteApp 및 데스크톱 솔루션 제공: 예, 둘 다
> 
> Azure RemoteApp 마이그레이션 솔루션: 예, [자세한 정보](http://www.acuutech.com/ara-migration/)
> 
> **영국**:
>   
> 5/6 York House, Langston Road,
>   
> Loughton, Essex IG10 3TQ
>   
> 전화 번호: +44 (0) 20 8502 2155
> 
> **싱가포르**:
>   
> 100 Cecil Street, #09-02, 
>   
> hello 069532 구형, 싱가포르
> 
> 전화 번호: +65 6709 4933
>   
> **북아메리카**
>   
> 3601 S. Sandman St.
>   
> Suite 200, Houston, TX 77098
>   
> 전화 번호: +1 713 691 0800

#### <a name="aspex"></a>ASPEX
[ASPEX](http://www.aspex.be/en) 전문 toohello 클라우드 및 ISV 전환 하는 Isv에 ' 찾고 toooptimize 한 자신의 현재 클라우드 설정 합니다. ASPEX에서는 광범위한 관리, 개발 및 컨설팅 서비스를 제공합니다.  

> 기본 위치: 벨기에 앤트워프
> 
> 작업 영역: 서유럽
> 
> 파트너 관계 상태: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)
> 
> Microsoft 클라우드 서비스 공급자: 예
> 
> 세션 기반 RemoteApp 및 데스크톱 솔루션 제공: 예, 둘 다
> 
> Azure RemoteApp 마이그레이션 솔루션: 예, [자세한 정보](https://www.aspex.be/en/azure-remote-apps)
> 
> 전화 번호: +3232202198
> 
> 메일: [info@aspex.be](mailto:info@aspex.be)
> 
> 웹: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)

#### <a name="caasecom"></a>Caase.com
[Caase.com](http://www.caase.com/) 기업, 로컬 정부, 비 정부 기관이 및 Microsoft 클라우드 hello에서 작업 하는 더 효율적인 방법으로 빌어 의료 기관은 데 도움이 됩니다. 어떤 장치를 사용하더라도 낮은 IT 비용으로 어디서든 생산적이고 안전할 수 있습니다. Caase.com은 진정한 Microsoft Office365, Azure, Enterprise Mobility + Security 및 Windows 전문가입니다. 컨설팅, 마이그레이션 서비스, 채택 프로그램, 교육, 관리 및 지원 Caase.com은 고객사 직원, 파트너 및 공급 업체 모두를 위한 최적화되고 안전한 플랫폼을 만듭니다.
Caase.com은 hello Azure 원격 작업 영역 (모바일 환경) 및 디지털 작업 공간 (소셜 인트라넷) hello hello 거듭하면서입니다. 채택 –를 사용 하 여 수행 하는 두 솔루션-는 hello foundation hello 사용자가이 솔루션의 해당 경로 toohello Microsoft 클라우드에서에서 hello 가장, 성공 즐겁고 효과적인 경험을 갖도록 보장 합니다.
http://caase.com/over-ons/에서 네덜란드어 번역 및 관련 동영상을 참고할 수 있습니다.

> 운영 지역: 네덜란드 기반의 글로벌 환경
> 
> 파트너 관계 상태: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)
> 
> Microsoft 클라우드 서비스 공급자: 예
> 
> 세션 기반 RemoteApp 및 데스크톱 솔루션 제공: 예, 둘 다
> 
> Azure RemoteApp 마이그레이션 솔루션: 예, [자세한 정보](http://caase.com/diensten/microsoft-azure/)
> 
> 
> 네덜란드:
> 
> Rigtersbleek-Zandvoort 10(De Spinnerij)
> 
> 7521 BE, Enschede
> 
> 전화: +31 (0) 88 4320 000


#### <a name="nerdio"></a>Nerdio
[Azure에 대 한 Nerdio](http://getnerdio.com/nfa/) 는 Microsoft 클라우드 hello의 터무니 없이 단순 프로비저닝, 관리 및 최적화 전체 IT 환경에 배달 하는 IT 자동화 플랫폼입니다. 가상 데스크톱, 원격 응용 프로그램 및 서버를 한두 시간 내에 사용할 수 있습니다. 세 번의 클릭에서 hello 환경을 관리 이하의 Nerdio 관리자 포털을 사용 합니다. 지능형 자동 크기 조정을 사용 하 고 Azure IaaS 리소스에 40 too60 %를 저장 합니다.

> 기본 위치: 시카고, IL 운영 지역: 전세계 파트너 등급: [골드](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Microsoft 클라우드 서비스 공급자: 예
> 
> 세션 기반 RemoteApp 및 데스크톱 솔루션 제공: 예, 둘 다
> 
> Azure RemoteApp 마이그레이션 솔루션: 예
> 
> 
> 8001 Lincoln Ave
> 
> Suite 212
> 
> Skokie, IL 60077
> 
> 미국
> 
> (844) 4NERDIO ext. 6
> 
> [sayhello@getnerdio.com](mailto:sayhello@getnerdio.com)

#### <a name="saasplaza"></a>**SaaSplaza**
[SaaSplaza](http://www.saasplaza.com/)는 모든 Microsoft Dynamics 포트폴리오(NAV, AX, GP, SL, CRM) 개인 및 공용 클라우드(Azure)를 제공 합니다.

> 기본 위치: 네덜란드
> 
> 작업 영역: 전 세계
> 
> 파트너 관계 상태: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)
> 
> Microsoft 클라우드 서비스 공급자: 예
> 
> 세션 기반 RemoteApp 및 데스크톱 솔루션 제공: 예, 둘 다
> 
> **EMEA**
> 
> Prins Mauritslaan 29-35
> 
> 71 LP Badhoevedorp
> 
> 안녕 네덜란드
> 
> 전화 번호: +31 20 547 8060 
> 
>  **아메리카**
> 
> 171 Saxony Road, Suite 105
> 
> Encinitas, CA 92024
> 
> 샌디에이고
> 
> 미국
> 
> 전화 번호: +1 858 385 8900 
> 
> **APAC**:
> 
> 105 Cecil Street
>    
> \#11-08 hello 팔각형
> 
> Singapore 069534
> 
> 싱가포르
>   
> 전화 번호 - 싱가포르: + 65 6222 6591
> 
> 전화 번호 - 오스트레일리아: +61 2 8310 5568 
>    
> 전화 번호 - 뉴질랜드: +64 4 488 0321
> 
## <a name="need-more-help"></a>도움이 더 필요하세요?
여전히 도움이 필요하거나 추가 질문이 있나요? Hello tooget 도움말 메서드를 다음 중 하나를 사용 합니다. 

1. [arainfo@microsoft.com](mailto:arainfo@microsoft.com)으로 메일을 보내세요.
2. [Azure 지원](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)에 문의하세요. [Azure 지원 사례](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)를 열면서 시작합니다.
3. 전화로 문의하세요. [해당 지역 영업 담당자 전화번호 찾기](https://azure.microsoft.com/overview/sales-number/)

