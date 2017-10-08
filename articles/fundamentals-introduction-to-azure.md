---
title: aaaIntro tooMicrosoft Azure | Microsoft Docs
description: "새 tooMicrosoft Azure? Hello에 대 한 기본적인 개요 가져오기 서비스의 사용 되는 방법을 예제와 함께 제공 합니다."
services: " "
documentationcenter: .net
author: rboucher
manager: carolz
editor: 
ms.assetid: 6f47f711-2208-4c21-8c1d-826a54c05c29
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2015
ms.author: robb
ms.openlocfilehash: 6791506abe813e19ca7b04d78d35cb46352a9028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-microsoft-azure"></a>Microsoft Azure 소개
Microsoft Azure는 Microsoft의 응용 프로그램 플랫폼 hello 공용 클라우드입니다.  hello이 문서의 ´ ֲ toogive 클라우드 컴퓨팅에 대 한 정보가 있는 경우에 Azure의 hello 기초를 이해 하기 위한 토대 있습니다.

**어떻게 tooread이이 문서**

쉽게 tooget 오버 로드 된 것 이므로 azure hello 항상 커지고 있습니다.  이 문서에서 첫 번째로 나열 되 고 tooadditional 서비스에 이동 하 여는 hello 기본 서비스를 시작 합니다. 를 직접 방금 hello 추가 서비스를 사용할 수 없지만 hello 기본 서비스를 통해 Azure에서 실행 중인 응용 프로그램의 핵심을 hello 구성 아닙니다.

**사용자 의견 제공**

Microsoft는 사용자의 의견을 소중하게 생각합니다. 이 문서는 Azure의 개요를 효과적으로 제공하기 위해 작성되었습니다. 이미 있으면 직접 알려 주시기 hello hello 페이지 맨 아래에 hello 주석 섹션에서. 기능에 몇 가지 정보를 제공 toosee 및 방법을 tooimprove hello 문서를 예상 합니다.  

## <a name="hello-components-of-azure"></a>hello Azure 구성 요소
Azure 관리 포털 hello 등과 hello와 같은 다양 한 시각적 보조 범주로 서비스를 그룹화 [Azure 인포 그래픽 이란](https://azure.microsoft.com/documentation/infographics/azure/) 합니다. 관리 포털 hello 사용 하는 것은 Azure에서 서비스 대부분 (모두는 아니지만) toomanage 합니다.

이 문서 ´ ֲ는 **다른 조직** tootalk 서비스에 대 한 유사한 함수와 toocall 더 큰 데이터베이스의 일부인 중요 한 하위 서비스에 기반 합니다.  

![Azure 구성 요소](./media/fundamentals-introduction-to-azure/AzureComponentsIntroNew780.png)   
 *그림: Azure는 Azure 데이터 센터에서 실행되는 인터넷 액세스가 가능한 응용 프로그램 서비스를 제공합니다.*

## <a name="management-portal"></a>관리 포털
Azure의 hello를 호출 하는 웹 인터페이스 [관리 포털](http://manage.windowsazure.com) 관리자 수 있도록 해 주는 tooaccess 및 모든 Azure 아니지만 대부분의 기능을 관리 합니다.  일반적으로 Microsoft는 이전에 사용 중지 전에 hello 최신 UI 포털 베타의를 해제 합니다. hello 최신 라고 hello ["Azure 미리 보기 포털"](https://portal.azure.com/)합니다.

두 포털이 모두 활성 상태이면 보통 오랜 기간 동안 겹침 현상이 발생합니다. 핵심 서비스는 두 포털 모두에 표시되지만, 일부 기능은 두 포털 모두에서 사용할 수 없을 수 있습니다. 최신 서비스 hello 최신 포털 첫 번째 및 이전 서비스에 표시 될 수 있습니다 및 기능 hello 이전 하나에에서만 존재할 수 있습니다.  여기에 hello 메시지는 hello 이전 포털에서 뭔가 찾지 못한 경우 확인 최신 hello와 반대로입니다.

## <a name="compute"></a>계산
클라우드 플랫폼에서 hello 가장 기본적인 항목 중 하나는 응용 프로그램을 실행할입니다. Hello Azure 계산 모델의 각 역할 tooplay 자체에 있습니다.

이러한 기술을 별도로 사용 하거나 응용 프로그램에 대 한 필요한 toocreate hello 오른쪽 foundation 결합 수 있습니다. hello 방법을 따라 선택 하는 어떤 문제에 toosolve 중 어느 것입니다.

### <a name="azure-virtual-machines"></a>Azure 가상 컴퓨터
![Azure 가상 컴퓨터 ROBBCSIART_TEST](./media/fundamentals-introduction-to-azure/mscsiart_VirtualMachinesIntroNew_12345.png)   
*그림: Azure 가상 컴퓨터 제공 hello 클라우드에서 가상 컴퓨터 인스턴스에 대 한 모든 권한을 합니다.*

hello 기능 toocreate 필요에 따라 가상 컴퓨터 간에 또는 독립 실행형 이미지에서 사용자가 제공한 여부 매우 유용할 수 있습니다. Azure 가상 컴퓨터에서는 일반적으로 IaaS(Infrastructure as a Service)로 알려진 이 방법을 제공합니다. 그림 2 하 고 가상 컴퓨터 (VM)를 실행 하는 방법의 조합을 보여 줍니다 VHD에서 toocreate 하나 있습니다.  

VM toocreate는 VHD toouse 및 hello VM의 크기를 지정 합니다.  그런 다음 지불 hello 시간에 대 한 VM 실행 되 고 해당 hello 합니다. Hello 사용할 수 있는 VHD를 유지 하는 데 최소한의 저장소 비용이 청구는 hello 분 단위 및이 서비스를 실행 하는 동안에 지불 합니다. Azure는 주식 ("이미지" 이라고 함) 포함 하는 Vhd에서 부팅 가능한 운영 체제 toostart 갤러리를 제공 합니다. 여기에는 Windows Server, Linux, SQL Server, Oracle 등 Microsoft와 파트너 옵션이 포함됩니다. 무료 toocreate Vhd와 이미지를 하 고 사용자가 직접 업로드 합니다. 데이터만 포함하는 VHD를 업로드한 다음 실행 중인 VM에서 액세스할 수도 있습니다.

Hello VHD에서에 도달할 때마다 VM 실행 하는 동안 수행 된 변경 내용을 영구적으로 저장할 수 있습니다. hello 다음 해당 VHD에서 VM을 만들 때 작업을 선택의 나머지 부분은 합니다. 가상 컴퓨터를 다시 hello Vhd hello에 대해 논의할 나중에 Azure 저장소 blob에 저장 됩니다.  즉, 중복 tooensure Vm toohardware 및 디스크 오류 인해 사라질지 않습니다를 얻게 됩니다. 도 가능한 toocopy hello 로컬로 실행 하는 Azure에서 VHD를 변경 합니다.

응용 프로그램 실행 하기 전에 만든 방식과 toocreate 결정에 따라 하나 이상의 가상 컴퓨터 내에서 처음부터 이제 합니다.

Tooaddress 사용 되는 여러 가지 문제 수 컴퓨팅이 매우 일반적인 방법 toocloud 합니다.

**가상 컴퓨터 시나리오**

1. **개발/테스트** -toocreate 사용을 마쳤으면 종료할 수 있는 저렴 한 개발 및 테스트 플랫폼 사용할 수 있습니다. 또한 어떤 언어나 라이브러리를 사용해서도 응용 프로그램을 만들고 실행할 수 있습니다. 해당 응용 프로그램이 Azure에서 제공 하는 hello 데이터 관리 옵션 중 하나를 사용할 수 및 SQL Server 또는 하나 이상의 가상 컴퓨터에서에서 실행 하는 다른 DBMS toouse 선택할 수도 있습니다.
2. **응용 프로그램 tooAzure (리프트 시프트) 이동** -"리프트 시프트" 참조 toomoving 응용 프로그램 훨씬 지게차 toomove 큰 개체를 사용할 때와 합니다.  "이동" 것 tooAzure 및 실행할 로컬 데이터 센터에서 VHD를 hello "리프트" 있습니다.  일반적으로 나면 toodo 몇 가지 작업 tooremove 종속성 다른 시스템에 있습니다. 종속성이 너무 많은 경우 옵션 3을 선택할 수도 있습니다.  
3. **데이터 센터 확장** - SharePoint 또는 기타 응용 프로그램을 실행하는 온-프레미스 데이터 센터의 확장으로 Azure VM을 사용하는 것입니다. toosupport이 hello 클라우드에서 가능한 toocreate Windows 도메인 Active Directory를 Azure Vm에서 실행 하 여는 것입니다. 함께 사용할 수 있습니다 (뒷부분에서 설명)는 Azure 가상 네트워크 tootie 로컬 네트워크 및 네트워크 Azure에서.

### <a name="web-apps"></a>웹앱
![Azure Web Apps ROBBCSIART_TEST](./media/fundamentals-introduction-to-azure/mscsiart_AzureWebsitesIntroNew_12345.png)   
 *그림: 웹 응용 프로그램을 Azure 웹 사이트 응용 프로그램에서에서 실행 hello 클라우드 toomanage hello 기본 웹 서버 필요 없이 됩니다.*

Hello 가장 일반적인 것 중 접할 hello 클라우드에서 하나는 웹 사이트 및 웹 응용 프로그램 실행 됩니다. Azure 가상 컴퓨터에는이 권한이 하지만 여전히 hello 과제 하나 이상의 Vm 및 hello 기본 운영 체제를 관리 하면 남습니다. 클라우드 서비스 웹 역할이 이 작업을 수행할 수 있지만 이 역할을 배포하여 관리하는 것도 관리 작업입니다.  어떻게 만들려는 경우 웹 사이트를 다른 사람에 게 hello 관리 작업을 담당?

바로 이것이 웹앱이 제공하는 정확한 기능입니다. 이 계산 모델 Api와 hello Azure 관리 포털을 사용 하 여 관리 되는 웹 환경을 제공 합니다. 웹 앱을 변경 하지 않은 기존 웹 사이트 응용 프로그램을 이동할 수 있습니다 또는 hello 클라우드에서 직접 새 인증서를 만들 수 있습니다. 웹 사이트를 실행 하 고 수 더하거나 빼는 인스턴스가 동적으로 간에 Azure 웹 앱 tooload 분산 요청에 의존 합니다. Azure 응용 프로그램 웹 사이트가 다른 사이트와 가상 컴퓨터에서 실행 하는 공유 옵션 및 사이트 toorun 자체 VM에서 허용 하는 표준 옵션을 모두 제공 합니다. hello 표준 옵션에서는 사용자 인스턴스가 필요한 경우의 (컴퓨팅) hello 크기를 늘릴 수도 있습니다.

개발을 위해서 Azure 웹앱은 관계형 저장소용 SQL 데이터베이스와 MySQL(Microsoft 파트너의 경우 ClearDB)과 함께 .NET, PHP, Node.js, Java, Python 등을 지원합니다. 또한 WordPress, Joomla, Drupal 등의 여러 인기 있는 응용 프로그램을 기본적으로 지원합니다. hello 목표 tooprovide는 저렴 한 비용, 확장 가능 하 고 hello 공용 클라우드에서 웹 사이트 및 웹 응용 프로그램을 만들기 위한 광범위 하 게 유용한 플랫폼입니다.

**웹앱 시나리오**

웹 앱은 의도 한 toobe 기업, 개발자 및 웹 디자인 기관에 유용 합니다. 기업에 상태 확인 웹 사이트를 위한 손쉬운 관리, 확장 가능성, 높은 보안, 고도의 가용성 등을 제공하는 솔루션입니다. 웹 사이트를 tooset 필요할 때 Azure 웹 앱과 최상의 toostart 이며 사용할 수 있는 기능을 사용 해야 하는 후 tooCloud 서비스를 계속 합니다. Hello 끝날을 hello 옵션 중 적합 한 toochoose 수 있는 더 많은 링크에 대 한 hello "컴퓨팅" 섹션을 참조 하십시오.

### <a name="cloud-services"></a>클라우드 서비스
![Azure Cloud Service](./media/fundamentals-introduction-to-azure/CloudServicesIntroNew.png)   
*그림: Azure 클라우드 서비스 위치 toorun 확장성이 뛰어난 사용자 지정 코드 플랫폼에서 제공 된 서비스 (PaaS) 환경으로*

Toobuild 많은 동시 사용자를 지원할 수 있는, 많은 관리 하지 않아도 고 이동 하지 않는 클라우드 응용 프로그램을 한다고 가정 합니다. 설정 된 소프트웨어 공급 업체 등 결정된 tooembrace Saas ()는 버전의 hello 클라우드에서 응용 프로그램 중 하나를 구축 하 여 소프트웨어를 수 있습니다. 빠른 성장을 바라보는 스타트업이라면 소비자 응용 프로그램을 만들 수도 있습니다. Azure에 구축하는 경우 어떤 실행 모델을 사용해야 할까요?

Azure 웹앱을 사용하면 웹 응용 프로그램을 만들 수 있지만 약간의 제약 조건이 따릅니다. 관리자 액세스 권한이 없는 경우 소프트웨어를 임의로 설치할 수 없다는 점이 대표적인 예입니다. Azure 가상 컴퓨터를 사용 하면 다양 한 관리 액세스를 포함 하 여 유연성 및 확실히 수 toobuild는 확장성이 크지 응용 프로그램 수 있지만 toohandle 신뢰성 및 관리의 다양 한 확인하실 수 있습니다. 원하는 기능을 제공 하는 옵션 hello 필요 하지만 또한 대부분의 안정성 및 관리에 필요한 hello 작업을 처리 하는 컨트롤입니다.

Azure 클라우드 서비스가 정답입니다. 이 기술은 toosupport 확장성이 뛰어나고 안정적 및 관리자가 낮은 응용 프로그램을 명시적으로 설계 되었으며 것은 예제 서비스 (PaaS) 플랫폼 이라는 일반적으로 것입니다. toouse C#, Java, PHP, Python, Node.js 또는 다른 작업 등 선택한 hello 기술을 사용 하 여 응용 프로그램 만들기, 합니다. 코드는 다음 버전의 Windows Server를 실행 중인 가상 컴퓨터 (참조 tooas 인스턴스)에서 실행 합니다.

하지만 이러한 Vm은 hello Azure 가상 컴퓨터를 만드는 것과 다릅니다. 예를 들면 Azure가 운영 체제 패치를 설치하고 자동으로 새로 패치된 이미지를 사용하는 등 해당 VM을 직접 관리한다는 차이점을 들 수 있습니다. 이 인해 응용 프로그램 해서는 안 웹 또는 작업자 역할 인스턴스;의 상태를 유지 관리 대신 hello 다음 섹션에서 설명 하는 hello Azure 데이터 관리 옵션 중 하나에 유지 합니다. Azure는 또한 VM을 모니터링하여 오류가 발생하면 VM을 다시 시작합니다. 클라우드를 설정할 수 있습니다 서비스 tooautomatically 응답 toodemand에 더 많거나 적은 인스턴스를 만듭니다. 이 있습니다 증가 toohandle 사용량 및 눈금 다시 돌리거나 있으면 더 적은 사용량 만큼 지불 되지 않습니다.

인스턴스를 만들 때 두 개의 역할 toochoose을 Windows Server에 기반한 둘 다. 웹 역할의 인스턴스는 작업자 역할의 인스턴스는 손실 IIS를 실행 하는 하는 hello 주요 차이점이 두 hello 합니다. 그러나 관리 되는 둘 다 hello에 동일한 방법으로 하며의 일반적으로 응용 프로그램 toouse 모두 합니다. 예를 들어 웹 역할 인스턴스를, 사용자에 게 요청을 수락 후 처리를 위해 tooa 작업자 역할 인스턴스를 전달 될 수 있습니다. tooscale 위나 아래로 이동 하면 응용 프로그램을 Azure의 역할 중 하나 이상의 인스턴스가 만들거나 기존 인스턴스를 종료할 요청할 수 있습니다. 하며 비슷한 tooAzure 가상 컴퓨터를 하는 요금이 청구 hello 시간에 대해서만 각 웹 또는 작업자 역할 인스턴스가 실행 되 고 있습니다.

**클라우드 서비스 시나리오**

클라우드 서비스는 이상적인 toosupport 대규모 스케일 아웃는 Azure 웹 앱에서 제공 하는 보다 hello 플랫폼을 통해 보다 자세히 제어 해야 하지만 hello 기본 운영 체제에 대 한 제어를 필요 하지 않습니다.

#### <a name="choosing-a-compute-model"></a>계산 모델 선택
hello 페이지 [Azure 웹 앱, 클라우드 서비스 및 가상 컴퓨터 비교](app-service-web/choose-web-site-cloud-service-vm.md) 방법에 대 한 상세 정보가 제공 toochoose 계산 모델입니다.

## <a name="data-management"></a>데이터 관리
응용 프로그램에는 데이터가 필요하고, 서로 다른 종류의 응용 프로그램에는 서로 다른 종류의 데이터가 필요합니다. 이 때문에 Azure는 여러 가지 방법으로 toostore 제공 하 고 데이터를 관리 합니다. Azure는 많은 저장소 옵션을 제공하지만 모두 영구 저장소를 위해 설계되었습니다.  이러한 옵션 중 하나로 Azure 데이터 센터-Azure toouse 지리적 중복 tooback tooanother 데이터 센터 이상 300 거리에 있는를 허용 하는 경우 6 동기화 유지할 데이터의 복사본을 3 개 항상 됩니다.     

### <a name="in-virtual-machines"></a>가상 컴퓨터에서
hello 기능 toorun SQL Server 또는 Azure 가상 컴퓨터를 만든 VM에서 다른 DBMS 언급 이미 했습니다. 이 옵션 제한 toorelational 시스템; 없음을 실현 합니다. 사용자는 또한 MongoDB Cassandra 등의 무료 toorun NoSQL 기술 합니다. We're it 간단 하 게 복제는 데이터베이스 시스템을 직접 실행 tooin 자체 데이터 센터를 사용-방법 이지만 해당 DBMS의 hello 관리 처리 필요 합니다.  다른 옵션을 자세히 또는 모든 사용자에 대 한 hello 관리 Azure 처리합니다.

다시 hello 가상 컴퓨터의 hello 상태 및 모든 추가 데이터 디스크를 만들거나 업로드 하는 blob 저장소에 저장 (에 대해 논의할 나중에)에 의해 지원 됩니다.  

### <a name="azure-sql-database"></a>Azure SQL Database
![Azure 저장소 SQL 데이터베이스](./media/fundamentals-introduction-to-azure/StorageAzureSQLDatabaseIntroNew.png)   

*그림: Azure SQL 데이터베이스는 hello 클라우드에서 관리 되는 관계형 데이터베이스 서비스를 제공합니다.*

관계형 저장소에 대 한 Azure SQL 데이터베이스 hello 기능을 제공합니다. 주저 하지 마시기 바랍니다 hello 주의 이름을 지정 합니다. 이 데이터베이스는 Windows Server에서 실행되는 SQL Server에서 제공하는 일반 SQL 데이터베이스와 다릅니다.  

SQL Azure 라고 부르던, Azure SQL 데이터베이스의 모든 제공 hello 관계형 데이터베이스 관리 시스템, 원자성 트랜잭션을 포함 하 여 데이터 무결성, ANSI SQL 쿼리와 친숙 한 프로그래밍에 여러 사용자가 동시 데이터 액세스의 주요 기능 모델입니다. SQL Server와 같이 Entity Framework, ADO.NET, JDBC, 기타 친숙한 데이터 액세스 기술 등을 사용하여 SQL 데이터베이스에 액세스할 수 있습니다. 또한 hello SQL Server Management Studio와 같은 SQL Server 도구와 함께 T-SQL 언어의 대부분을 지원합니다. SQL Server(또는 다른 관계형 데이터베이스)에 친숙한 사람은 SQL 데이터베이스를 쉽게 사용할 수 있을 것입니다.

하지만 SQL 데이터베이스 아닙니다 DBMS 방금 hello에서 클라우드 it의 PaaS 서비스입니다. 데이터를 액세스할 수 있는 사용자와 계속 제어할 하지만 SQL 데이터베이스 hello 하드웨어 인프라를 관리 하 고 toodate hello 데이터베이스 및 운영 체제 소프트웨어를 자동으로 유지 하는 등의 hello 관리 grunt 작업을 담당 합니다. 또한 SQL 데이터베이스는 고가용성, 자동 백업, 지정 시간 복원 기능을 제공하며, 여러 지역에 걸쳐 복사본을 복제할 수도 있습니다.  

**SQL 데이터베이스에 대한 시나리오**

Azure 하는 응용 프로그램 (hello 계산 모델을 사용) 관계형 저장소를 만드는 경우 SQL 데이터베이스 좋을 수 있습니다. 외부 hello 클라우드를 실행 중인 응용 프로그램을 사용할 수도이 서비스 하지만 다른 시나리오는 여러 가지 하므로. 예를 들어, 다양한 클라이언트 시스템(데스크 톱, 노트북, 태블릿, 휴대폰 등)에서 SQL 데이터베이스에 저장된 데이터를 액세스할 수 있습니다. 또한 복제를 통해 기본 제공 고가용성을 제공하기 때문에 SQL 데이터베이스를 사용하면 가동 중지 시간을 최소화할 수 있습니다.

### <a name="tables"></a>테이블
![Azure 저장소 테이블](./media/fundamentals-introduction-to-azure/StorageTablesIntroNew.png)  

*그림: Azure 테이블 플랫 NoSQL 방법을 toostore 데이터를 제공 합니다.*

이 기능은 "Azure 저장소"라고 하는 대규모 기능의 일부이기 때문에 때때로 다른 용어로 부르기도 합니다. "Tables", "Azure 테이블" 또는 "저장소 테이블"을 참조 하는 경우는 모든 hello 다릅니다.  

Hello 이름을 혼동 하지 마십시오 하 고:이 기술은 관계형 저장소를 제공 하지 않습니다. 사실 키/값 저장소라고 부르는 NoSQL 방식의 하나입니다. Azure 테이블을 사용하면 응용 프로그램을 통해 문자열, 정수, 날짜 등의 다양한 유형 속성을 저장할 수 있습니다. 그런 다음 응용 프로그램에서 해당 그룹의 고유키를 제공하여 속성 그룹을 검색할 수 있습니다. 복잡 한 작업 동안 테이블에 대 한 빠른 액세스 tootyped 데이터 제공 처럼 조인은 지원 되지 않습니다. 때도 단일 테이블 수 toohold와 매우 확장 가능한 데이터 테라바이트 만큼 합니다. 및 그 단순 함으로 일치의 경우 테이블은 SQL 데이터베이스의 관계형 저장소 보다 일반적으로 보다 저렴 toouse 합니다.

**테이블에 대한 시나리오**

Toocreate 한다고 가정 fast 하는 Azure 응용 프로그램을 많이 미정 tootyped 데이터에 액세스 하지만이 데이터에 대 한 복잡 한 SQL 쿼리 tooperform 필요 하지 않습니다. 예를 들어, 각 사용자에 대 한 toostore 고객 프로필 정보를 필요로 하는 소비자 응용 프로그램을 만들려는 한다고 가정 합니다. 앱 하려고 toobe 매우 인기 있는 tooallow 대량의 데이터를 사용 해야 하지만 있습니다 수행 하지 않습니다을 저장 하 고 초과 하 여이 데이터와 별 다음 간단한 방법으로 검색 합니다. Azure 테이블 타당 한 시나리오의 정확히 hello 종류입니다.

### <a name="blobs"></a>Blob
![Azure Storage Blobs](./media/fundamentals-introduction-to-azure/StorageBlobsIntroNew.png)    
*그림: Azure Blob은 비구조적 이진 데이터를 제공합니다.*  

Azure Blob (다시 "Blob Storage" 및 "저장소 Blob"는 hello 동일한 작업)은 설계 된 toostore 비구조적된 이진 데이터입니다. 테이블 서비스처럼 Blob은 단일 Blob이 최대 1TB(테라바이트)까지 지원되는 저렴한 저장소를 제공합니다. 또한 Azure 응용 프로그램에서 Blob을 통해 Azure 인스턴스에 탑재된 Windows 파일 시스템용 영구적 저장소를 제공하는 Azure 드라이브를 사용할 수도 있습니다. hello 응용 프로그램에는 일반적인 Windows 파일을 표시 하지만 hello 내용은 실제로 blob에 저장 됩니다.

Blob 저장소는 다른 많은 Azure 기능(가상 컴퓨터 포함)에 사용되므로 특히 사용자의 작업 부담을 줄여 줍니다.

**Blob에 대한 시나리오**

예를 들어 비디오, 광범위한 파일, 기타 이진 정보 등을 저장하는 응용 프로그램에서 간단하고 저렴한 저장소인 Blob을 사용할 수 있습니다. 또한 Blob은 일반적으로 CDN(콘텐츠 배달 네트워크) 등 나중에 다룰 다른 서비스와 함께 사용됩니다.  

### <a name="import--export"></a>가져오기/내보내기
![Azure 가져오기 내보내기 서비스](./media/fundamentals-introduction-to-azure/ImportExportIntroNew.png)  

*그림: Azure 가져오기 / 내보내기 빠르고 저렴 한 비용 대량 데이터 가져오기 또는 내보내기에 대 한 Azure에서 실제 하드 드라이브 tooor hello 기능 tooship를 제공 합니다.*  

Azure에 많은 데이터 toomove가 필요한 경우도 있습니다. 며칠 정도 긴 시간이 걸리며 상당한 대역폭을 사용하게 됩니다. 이러한 경우에는 Azure 가져오기/내보내기, 있습니다 있습니다 tooship Bitlocker로 암호화 된 3.5 인치 SATA 하드 드라이브를 직접 tooAzure 데이터 센터, 여기서 Microsoft hello 데이터 전송 blob 저장소에 있습니다 사용할 수 있습니다.  Hello 업로드가 완료 되 면 Microsoft는 hello 드라이브 백 tooyou를 제공 됩니다.  Blob 저장소에서 데이터의 양이 많은 하드 드라이브에 내보낸 후 메일을 통해 뒤로 tooyou 전송를 요청할 수 있습니다.

**가져오기/내보내기에 대한 시나리오**

* **큰 데이터 마이그레이션을** 많은 양의 데이터 (테라바이트) 필요한 경우 언제-tooupload tooAzure 원하는, hello 가져오기/내보내기 서비스는 종종 매우 빠르고 아마도 hello를 통해 전송 하는 보다 저렴 한 비용 인터넷 합니다. Blob의 hello 데이터를 테이블 저장소 또는 SQL 데이터베이스와 같은 다른 형태로 처리할 수 있습니다.
* **데이터 복구 보관** -가져오기/내보내기 toohave Microsoft 전송 많은 양의 tooa 저장 장치 보낼 경우 해당 장치를 원하는 백 tooa 위치를 전달 하는 Azure Blob 저장소에 저장 된 데이터를 사용할 수 있습니다. 어느 정도 시간이 걸리기 때문에 재해 복구에는 적절한 옵션이 아닙니다. 그러나 빠르게 액세스하지 않아도 되는 보관된 데이터에는 최상의 옵션입니다.

### <a name="file-service"></a>파일 서비스
![Azure File Service](./media/fundamentals-introduction-to-azure/FileServiceIntroNew.png)    
*그림: Azure 파일 서비스 제공 SMB \\ \\hello 클라우드에서 실행 중인 응용 프로그램에 대 한 서버 경로입니다.*

온-프레미스, 것이 일반적인 toohave 많은 양의 파일 저장소를 사용 하 여 hello 서버 메시지 블록 (SMB) 프로토콜을 통해 액세스할 수는 \\ \\Server\share 형식입니다. Azure 이제는 toouse 수 있는 서비스가이 프로토콜 hello 클라우드에서 합니다. Azure에서 실행 중인 응용 프로그램 tooshare 파일을 친숙 한 파일 시스템 ReadFile 및 WriteFile와 같은 Api를 사용 하 여 Vm 간에 사용할 수 있습니다. 또한 hello 파일 액세스할 수도 hello에도 가상 네트워크를 설정 하는 경우 온-프레미스에서 tooaccess hello 공유 수 있는 REST 인터페이스를 통해 동시 합니다. Azure 파일 hello blob 서비스 위에 빌드됩니다. 따라서, 상속 되므로 hello 가용성의 동일한 내구성, 확장성 및 지리적 중복 Azure 저장소에 기본 제공 합니다.

**Azure 파일에 대한 시나리오**

* **기존 앱 toohello 클라우드 마이그레이션** -hello 응용 프로그램의 부분 간에 tooshare 데이터를 공유 하는 그 보다 쉽게 toomigrate 온-프레미스 응용 프로그램 toohello 클라우드 파일을 사용 하 합니다. Toohello 파일 공유를 연결 하는 각 VM 및 읽고 그 온-프레미스 파일에 대해 공유 하는 것 처럼 파일을 쓸 수 다음 합니다.
* **공유 응용 프로그램 설정** -분산된 응용 프로그램에 대 한 일반적인 패턴은 여러 가상 컴퓨터에서 액세스할 수 있는 중앙된 위치에 toohave 구성 파일입니다. 이러한 구성 파일을 Azure 파일 공유에 저장하면 모든 응용 프로그램 인스턴스에서 읽을 수 있습니다. hello REST 인터페이스를 통해 전 세계 액세스 toohello 구성 파일을 통해 hello 설정은 관리할 수도 있습니다.
* **진단 공유** - 로그, 메트릭, 크래시 덤프 등과 같은 진단 파일을 저장하고 공유할 수 있습니다. 이러한 파일을 SMB hello와 REST 인터페이스를 통해 사용할 수 있으면 처리 하 고 hello 진단 데이터를 분석 하기 위한 분석 도구의 다양 한을 응용 프로그램 toouse 있습니다.
* **개발/테스트/Debug** 개발자 또는 관리자가 hello 클라우드의 가상 컴퓨터에서 작업할 때-도구 또는 유틸리티 집합이 필요한 경우가 많습니다. 각 가상 컴퓨터에서 이러한 유틸리티를 설치 및 분산하는 작업은 시간이 많이 걸립니다. Azure 파일을 개발자 또는 관리자 선호 하는 도구 파일 공유에 저장 하 고 toothem 모든 가상 컴퓨터에서 연결 수입니다.

## <a name="networking"></a>네트워킹
Hello world에 분산 하는 많은 데이터 센터에서 azure 오늘 실행 됩니다. 응용 프로그램을 실행 하거나 데이터를 저장할 때 이러한 데이터 센터 toouse 중 하나 이상을 선택할 수 있습니다. 아래 hello 서비스를 사용 하 여 다양 한 방법으로 toothese 데이터 센터를 연결할 수 있습니다.

### <a name="virtual-network"></a>가상 네트워크
![VirtualNetwork](./media/fundamentals-introduction-to-azure/VirtualNetworkIntroNew.png)   

*그림: 가상 네트워크 hello 클라우드에서 개인 네트워크 서로 다른 서비스 tooeach 대화를 나눌 수 있으므로, 또는 제공 tooon 온-프레미스 리소스 VPN 크로스-프레미스 연결을 설정 합니다.*  

하나의 유용한 방법은 toouse 공용 클라우드에서 tootreat 자체 데이터 센터의 확장으로 합니다.

주문형으로 VM을 만들 수 있기 때문에 더 이상 필요하지 않을 때 제거와 동시에 결제를 중단하여 원할 때만 컴퓨팅 기능을 갖출 수 있습니다. 및 Azure 가상 컴퓨터를 사용 하면 SharePoint, Active Directory 및 기타 친숙 한 온-프레미스 소프트웨어를 실행 하는 Vm을 만들 수 있습니다, 때문에이 방법은 이미 hello 응용 프로그램 작업할 수 있습니다.

toomake이 실제로 유용 하지만 사용자를 포함 해야 toobe 수 tootreat 이러한 응용 프로그램 자체 데이터 센터에서 실행 하는 것 처럼 경우. Azure 가상 네트워크가 바로 그러한 서비스를 제공합니다. VPN 게이트웨이 장치를 사용 하 여 관리자가 설정할 수 가상 사설망 (VPN)을 로컬 네트워크 사이의 tooa 배포 된 Azure 가상 네트워크에에서 있는 Vm에 합니다. 사용자의 IP v4 주소 toohello 클라우드 Vm에 할당 하기 때문에 사용자의 네트워크에서 toobe 나타납니다. 조직의 사용자가 응용 프로그램 hello 해당 Vm에 액세스할 수 로컬로 실행 중인 하는 경우를 포함 합니다.

사용자에게 적합한 가상 네트워크를 계획 및 생성에 대한 자세한 내용은 [가상 네트워크](virtual-network/virtual-networks-overview.md)를 참조하세요.

### <a name="express-route"></a>Express 경로
![Express 경로](./media/fundamentals-introduction-to-azure/ExpressRouteIntroNew.png)   

*그림: ExpressRoute를 통해 Azure 가상 네트워크, 하지만 경로 대신 줄을 더 빠르게 전용을 사용 하 여 공용 인터넷 hello 합니다.*  

Azure 가상 네트워크 연결에서 제공할 수 있는 것보다 더 많은 대역폭 또는 보안이 필요한 경우 Express 경로를 살펴볼 수 있습니다. 일부 경우에는 Express 경로를 통해 비용을 절감할 수도 있습니다. Azure에서 가상 네트워크 필요 하지만 hello를 통해 전달 되지 않는 전용된 연결을 사용 하 여 사이트와 Azure 간의 hello 링크 공용 인터넷 합니다. toouse이이 서비스를 요청, 네트워크 서비스 공급자 또는 exchange 공급자를 사용 하 여 규약 toohave 필요 합니다.

더 많은 시간이 필요 ExpressRoute 연결을 설정 및 계획, 하므로 toostart 해도 사이트 간 vpn을 다음로 마이그레이션해야 tooan ExpressRoute 연결 합니다.

Express 경로에 대한 자세한 내용은 [Express 경로 기술 개요](expressroute/expressroute-introduction.md)를 참조하세요.

### <a name="traffic-manager"></a>트래픽 관리자
![TrafficManager](./media/fundamentals-introduction-to-azure/TrafficManagerIntroNew.png)   

*그림: Azure 트래픽 관리자 있습니다 tooroute 글로벌 트래픽 tooyour 서비스를 지능형 규칙에 따라 수 있습니다.*

Azure 응용 프로그램을 여러 데이터 센터에서 실행 중인 경우 hello 응용 프로그램의 인스턴스를 통해 사용자의 Azure 트래픽 관리자 tooroute 요청을 지능적으로 사용할 수 있습니다. 트래픽을 라우팅할 수 있습니다에서 액세스할 수으로 Azure에서 실행 중이지 tooservices hello 인터넷 합니다.  

Hello world의 일부 단일 사용자와 Azure 응용 프로그램 하나만 Azure 데이터 센터에서 실행 될 수 있습니다. 그러나 사용자와 응용 프로그램 hello world 주위에 흩어져 있는는 여러 데이터 센터의 가능성이 더 toorun 미정도 모두입니다. 문제가 직면 하는이 두 번째 상황에서는: 어떻게 수행 하면 지능적으로 전달할 사용자 tooapplication 인스턴스? 대부분의 hello 싶을 각 사용자 tooaccess hello 데이터 센터와 가장 가까운 tooher, 그녀의 hello 최적의 응답 시간이 가능성이 생깁니다 때문입니다. 하지만 hello 응용 프로그램의 해당 인스턴스에 오버 로드 된 되었거나 사용할 수 없는 경우에 어떻게? 이 경우 좋은 toodirect 그녀의 요청을 자동으로 상태가 tooanother 데이터 센터입니다. 이것이 바로 Azure 트래픽 관리자의 역할입니다.

응용 프로그램의 hello 소유자는 이러한 규칙으로 트래픽 관리자 toocarry에 의존 합니다 사용자 로부터의 요청 directed toodatacenters 여야 방법을 지정 하는 규칙을 정의 합니다. 예를 들어 사용자가 정상적으로 directed toohello 가장 가까운 Azure 데이터 센터, 있지만 hello 응답 시간이 해당 기본 데이터 센터에서 다른 데이터 센터에서 hello 응답 시간을 초과 하는 경우 하나 tooanother 전송 합니다. 여러 사용자가 있는 세계적으로 분산 된 응용 프로그램의 경우 이와 같은 기본 제공 서비스 toohandle 문제가 유용 합니다.

디렉터리 서비스 (DNS 이름) tooroute 사용자 tooservice 끝점을 사용 하 여 트래픽 관리자 되지만 추가 트래픽을 시작 하지 못할 트래픽 관리자를 통해 해당 연결 되 면 합니다. 그래서 트래픽 관리자에서 서비스 통신을 느리게 만들 수 있는 병목 현상이 발생하지 않도록 합니다.

## <a name="developer-services"></a>개발자 서비스
Azure는 다양 한 도구 toohelp 개발자 및 IT 전문가 만들고 hello 클라우드에서 응용 프로그램을 유지 관리 합니다.  

### <a name="azure-sdk"></a>Azure SDK
2008 년에 다시 hello 첫 번째 시험판 버전의 Azure 지원만.NET 개발. 하지만 이제 Azure 응용 프로그램을 대부분의 언어로 작성할 수 있습니다. 현재 Microsoft는 .NET, Java, PHP, Node.js, Ruby, Python 등의 언어별 SDK를 제공합니다. 또한 C++ 등 모든 언어를 기본적으로 지원하는 일반적인 Azure SDK도 있습니다.  

이러한 SDK는 Azure 응용 프로그램의 구축, 배포, 관리 등을 돕습니다. SDK는 [www.microsoftazure.com](https://azure.microsoft.com/downloads/) 또는 GitHub에 있으며, Visual Studio 및 Eclipse와 함께 사용할 수 있습니다. 또한 azure Linux 및 Macintosh 시스템에서 tooAzure 응용 프로그램 배포 도구를 포함 하는 편집기 또는 개발 환경으로 개발자가 사용할 수 있는 명령줄 도구를 제공 합니다.

Azure 응용 프로그램 빌드를 돕는 것 외에도, 이 SDK는 Azure 서비스를 사용하는 소프트웨어 작성을 돕는 클라이언트 라이브러리를 제공합니다. 예를 들어 Azure blob을 읽고 하는 응용 프로그램을 작성 하거나 hello Azure 관리 인터페이스를 통해 Azure 응용 프로그램을 배포 하는 도구를 만들 수 있습니다.

### <a name="visual-studio-team-services"></a>Visual Studio Team Services
Visual Studio Team Services에는 hello Azure에에서 응용 프로그램 toodevelop는 데 도움이 되는 숫자 서비스를 포함 하는 마케팅 이름입니다.

tooavoid 혼동-호스트 또는 웹 기반 버전의 Visual Studio 제공 하지 않습니다. 따라서 Visual Studio의 로컬 실행 사본이 여전히 필요합니다. 그러나 매우 유용한 다른 많은 도구를 제공합니다.

이 서비스에는 버전 제어 및 작업 항목 추적 기능을 제공하는 Team Foundation Service라고 하는 호스티드 소스 제어 시스템을 포함합니다.  원하는 경우 버전 제어에 Git을 사용할 수 있습니다. 있으며 프로젝트에서 사용 하 여 hello 소스 제어 시스템을 변경할 수 있습니다. 하면 무제한 개인 팀 프로젝트에서 액세스할 수 있는 위치에 만들 수는 hello world.  

Visual Studio Team Services는 부하 테스팅 서비스를 제공합니다. Vm 클라우드 hello에서에서 Visual Studio에서 만든 부하 테스트를 실행할 수 있습니다. Hello, tooload 테스트 하는 사용자의 총 수를 지정 하 고 Visual Studio Team Services는 자동으로 개수 에이전트가 필요한 지 결정, 시작 hello 필요한 가상 컴퓨터를 하 고 부하 테스트를 실행 합니다. MSDN 구독자인 경우 매달 부하 테스팅을 할 수 있는 상당한 무료 사용 시간을 받게 됩니다.

또한 Visual Studio Team Services는 연속 통합 빌드, Kanban 보드, 가상 팀 회의실과 같은 기능을 통해 민첩한 개발도 지원합니다.

**Visual Studio Team Services 시나리오**

Visual Studio Team Services에는 회사 toocollaborate 전 세계 필요 하 고 이미 hello 인프라에에서 없는 위치 toodo 하므로 대 한 적합 한 옵션입니다. 몇 분 안에 설정하고, 소스 제어 시스템을 선택하고 하루 만에 코드 작성과 빌드를 시작할 수 있습니다.  hello 팀 도구를 조정 하기 위해 장소를 제공 및 hello 분석 필요 tootest 제공 공동 작업 및 hello 추가 도구 및 응용 프로그램을 신속 하 게 조정 합니다.

하지만 온-프레미스 시스템에 이미 있는 조직에서는 보다 효율적인 경우 Visual Studio Team Services toosee에서 새 프로젝트를 테스트할 수 있습니다.   

### <a name="application-insights"></a>Application Insights
![Application Insights](./media/fundamentals-introduction-to-azure/ApplicationInsights.png)  

*그림: Application Insights는 라이브 웹 또는 장치 앱의 성능 및 사용 현황을 모니터링합니다.*

모바일 장치, 데스크톱 또는 웹 브라우저에서 실행되는 앱을 게시한 경우 Application Insights는 앱의 작동 방식 및 사용자가 해당 앱으로 수행하는 작업을 알려줍니다. 충돌 및 느린 응답 수를 유지 합니다, 그리고 문제를 진단 hello 그림에서는 허용 되지 않는 임계값을 교차 하는 데 도움이 및 여부 경고 합니다.

새로운 기능을 개발할 때 toomeasure 사용자와 성공 여부를 계획 합니다. 사용 패턴을 분석하여 고객에게 최적으로 작동하는 기능을 이해하고 모든 개발 주기에서 앱을 향상시킵니다.

Azure에 호스트되지만 Application Insights는 Azure 내부 및 외부의 광범위한 앱에 작동합니다. iOS, Android, OSX 및 Windows 응용 프로그램은 물론, J2EE 및 ASP.NET 웹앱을 모두 포괄합니다. 원격 분석 toobe 분석 하 고 Azure에서 Application Insights 서비스 hello에 표시 된 hello 앱을 사용 하 여 빌드한 SDK에서 전송 됩니다.

더 특수 한 분석 하려는 경우 hello 원격 분석 스트림 tooa 데이터베이스 또는 tooPower BI 또는 다른 도구를 내보냅니다.

**Application Insights 시나리오**

앱을 개발 중입니다. 웹앱이나 장치 앱일 수도 있고, 웹 백 엔드가 있는 장치 앱일 수도 있습니다.

* 게시 된 후 응용 프로그램의 hello 성능을 튜닝 또는 되는 동안 부하를 테스트 합니다.  Application Insights는 모든 설치 된 hello 인스턴스에서 원격 분석을 집계 하 고 응답 시간, 요청 및 예외 수가, 종속성 응답 시간 및 기타 성능 지표에 대 한 차트를 제공 합니다. 이를 통해 앱 성능을 쉽게 조정할 수 있습니다. 코드 tooreport를 삽입 하면 데이터가 필요할 때 더 합니다.
* 라이브 앱에서 문제를 검색하고 진단합니다. 성과 표시기가 허용 가능한 임계값을 초과하거나 못미칠 경우 전자 메일로 경고할 수 있습니다. 예를 들어 toosee hello 요청 예외를 발생 시킨 특정 사용자 세션을 조사할 수 있습니다.
* 각 새로운 기능의 사용 현황 tooassess hello 성공 여부를 추적 합니다. 새 사용자 스토리를 디자인할 때 얼마나를 사용 하는 사용자가 예상된 목표를 달성 하는지 여부 및 toomeasure를 계획 합니다. Application Insights를 통해 웹 페이지 보기와 같은 기본 사용 현황 데이터 고 보다 자세히 코드 tootrack hello 사용자 경험을 삽입할 수 있습니다.

### <a name="automation"></a>Automation
Hello를 수행 하는 toowaste 시간을 배치할 수 아무도 같은 수동 반복 처리 합니다. Azure 자동화 하는 방법을 제공 하면 toocreate에 대 한 모니터링, 관리 및 Azure 환경에서 리소스를 배포 합니다.  

자동화는 hello에서는 "runbook" Windows PowerShell 워크플로 (vs. 단순히 일반 PowerShell)을 사용 하 여이 사용 합니다. Runbook toobe 사용자 개입 없이 실행 되어야 합니다. PowerShell 워크플로 허용 hello 따라 검사점에서 저장 된 스크립트 toobe의 hello 상태 방법입니다. 다음 오류가 발생할 경우 없는 toostart hello 처음부터 스크립트입니다. Hello 마지막 검사점에서 다시 시작할 수 있습니다. 많은 작업 시도 toomake hello 스크립트 핸들 가능한 모든 오류를 줄일 수 있습니다.

**자동화 시나리오**

Azure 자동화에 적합 한 선택 tooautomate hello 수동, 장기-실행 중 이며, 오류가 발생할 Azure에서 자주 반복 되는 작업입니다.

### <a name="api-management"></a>API 관리
만들기 및 hello에 게시 하는 응용 프로그램 프로그래머 Api (인터페이스) 인터넷은 일반적인 방식으로 tooprovide 서비스 tooapplications입니다. 조직 제 3 자의 허용할 수 있습니다 이러한 서비스 (예: 날씨 데이터) resellable 인 요금에 대 한 서비스 동일한 tooaccess 합니다. Toomore 파트너 크기를 조정 일반적으로 toooptimize 필요 하 액세스를 제어 합니다.  일부 파트너 hello 데이터를 다른 형식에도 필요 않을 수 있습니다.

Azure API 관리 쉽게 조직 toopublish Api toopartners, 직원 및 공급 업체 개발자에 대 한 안전 하 고 규모에 있습니다. 다른 API 끝점을 제공 하 고 역할 프록시 toocall 캐싱, 변환와 같은 서비스를 제공 하는 동안 실제 끝점 hello으로 제한, 액세스 제어 및 분석 집계 합니다.

**API 관리 시나리오**

회사에 일련의 장치 예를 들어 hello 근무자 트럭 모든 장치에는 운송 회사 toocall 백 tooa 중앙 서비스 tooget 데이터와 필요한 모든 경우를 가정해 봅니다.  Hello 회사 tooset 확실히 합니다 시스템 tootrack 위로 이므로 직접 트럭 안정적으로 예측 및 배달 시간을 업데이트할 수 있습니다. 그렇게 하면 보유한 트럭 수를 파악하여 적절히 계획할 수 있기 때문입니다.  각 트럭의 위치 지정 및 속도 데이터를 더와 tooa 중앙 위치를 다시 호출 하는 장치가 필요 합니다.

Hello 운송 회사의 고객은 아마도 위치 지정이 데이터를 가져오는에서 얻을 수 있습니다.  hello 고객 수 정도 제품에는 tootravel, 여기서은 의문 사항이 얼마나 있습니다 (어떤 것 유료 tooship 함께) 하는 경우 특정 경로 따라 지불 tooknow를 사용 합니다. 회사를 전달 하는 hello는 이미이 데이터를 집계, 많은 고객 수에 대 한 비용을 지불 합니다.  하지만 다음 회사를 전달 하는 hello tooprovide toogive 고객 데이터 hello 하 게 합니다. 액세스 toocustomers, 제공 되 면 얼마나 자주 hello 데이터를 쿼리 하는 작업을 제어할이 없을 수 있습니다. 데이터에 액세스할 수 있는 사용자에 대 한 tooprovide 규칙을 갖게 됩니다. 이러한 모든 규칙 toobe가 외부 API에 기본 제공 되는 것입니다. 여기가 바로 API 관리가 도울 수 있는 지점입니다.  

## <a name="identity-and-access"></a>ID 및 액세스
대부분의 응용 프로그램에는 ID와 관련된 작업이 포함됩니다. 사용자를 식별하면 응용 프로그램에서 해당 사용자와 상호 작용하는 방식을 결정할 수 있습니다. Azure는 서비스 toohelp 추적 id와 함께 제공 이미 사용 하는 id 저장소와 통합 합니다.

### <a name="active-directory"></a>Active Directory
대부분의 디렉터리 서비스와 같은 Azure Active Directory 사용자 및 자신이 속한 hello 조직에 대 한 정보를 저장 합니다. 사용자가 로그인 하는 서버 수 있도록 다음 제공 토큰으로 제공할 수 있는 tooapplications tooprove id입니다. 또한 로컬 네트워크에 있는 온-프레미스에서 실행되는 Windows Server Active Directory와 사용자 정보를 동기화할 수 있습니다. Hello 메커니즘 및 Azure Active Directory에서 사용 되는 데이터 형식으로 Windows Server Active Directory에서 사용 되는 같지 동안 hello 기능을 수행 하므로 매우 비슷합니다.

중요 한 toounderstand 클라우드 응용 프로그램에서 Azure Active Directory는 용도로 주로 설계 합니다. 예를 들어 Azure나 다른 클라우드 플랫폼에서 실행하는 응용 프로그램에서 사용할 수 있습니다. 또한 Office 365와 같은 Microsoft 자체 클라우드 응용 프로그램에서도 Azure Active Directory를 사용합니다. 그러나 Azure 가상 컴퓨터와 Azure 가상 네트워크를 사용 하 여 hello 클라우드로 데이터 센터 tooextend 않으려면 Azure Active Directory은 hello 것이 좋습니다. 대신, 가상 컴퓨터에서 Windows Server Active Directory toorun을 해도 됩니다.

toolet 응용 프로그램에 포함 된 hello 정보 액세스, Azure Active Directory는 Azure Active Directory Graph를 호출 하는 RESTful API를 제공 합니다. 이 API를 사용 하면 모든 디렉터리 개체를 액세스 하는 플랫폼 및 간의 hello 관계에서 실행 되는 응용 프로그램입니다.  예를 들어 승인 된 응용 프로그램 사용자가 속한 hello 그룹, 기타 정보에 대 한 API toolearn이를 사용할 수 있습니다. 응용 프로그램 사용자가 해당 사회 사람들 hello 연결과 보다 체계적으로 작동 하 게 그래프 줍니다 간의 관계를 참고할 수 있습니다.

이 서비스를 Azure Active Directory 액세스 제어의 다른 기능 쉽게 응용 프로그램 tooaccept id 정보에 대 한 Facebook, Google, Windows Live ID 및 기타 인기 있는 id 공급자에서 있습니다. Hello 응용 프로그램 toounderstand hello 다양 한 데이터 형식 및 이러한 각 공급자에서 사용 하는 프로토콜 않아도, 액세스 제어로 변환 모두 단일 공통 형식으로 합니다. 또한 응용 프로그램에서 하나 이상의 Active Directory 도메인에서의 로그인을 허용할 수 있도록 해줍니다. 예를 들어 고객 single sign on toohello 응용 프로그램의 각 SaaS 응용 프로그램을 제공 하는 공급 업체 toogive 사용자가 Azure Active Directory 액세스 제어를 사용할 수 있습니다.

디렉터리 서비스는 온-프레미스 컴퓨팅의 핵심 토대인 만큼 놀라운 것도 중요 한 hello 클라우드에서 되지 않아야 합니다.

### <a name="multi-factor-authentication"></a>Multi-Factor Authentication
![Azure Multi-Factor Authentication](./media/fundamentals-introduction-to-azure/MFAIntroNew.png)   

*그림: Multi-factor Authentication 기능을 제공 hello에 대 한 응용 프로그램 tooverify 둘 이상의 형식의 id*

보안은 언제나 중요한 사항입니다. MFA(Multi-factor authentication)는 사용자 본인만 자신의 계정에 액세스하도록 보장하는 데 유용합니다. MFA(2단계 인증 또는 "2FA"라고도 함)를 사용하려면 사용자가 로그인 및 트랜잭션을 위해 다음 3가지 ID 검증 방법 중 2가지를 제공해야 합니다.

* 사용자가 알고 있는 정보(일반적으로 암호)
* 사용자가 보유한 장치(예: 휴대폰과 같이 쉽게 복제되지 않는 신뢰할 수 있는 장치)
* 사용자의 신원 정보(생체 인식)

요구할 수 있는 사용자가 로그인 하면 되므로 tooalso 모바일 앱, 전화 통화 또는 문자 메시지를 암호와 함께에서 해당 id를 확인 합니다. 기본적으로 Azure Active Directory 사용자 로그인에 대 한 유일한 인증 방법으로 암호만 hello 사용을 지원합니다. Azure AD와 함께 또는 사용자 지정 응용 프로그램과 함께 MFA를 사용할 수 있으며, 디렉터리를 사용 하 여 hello MFA SDK입니다. 또한 Multi-Factor Authentication 서버를 통해 온-프레미스 응용 프로그램과 함께 사용할 수도 있습니다.

**MFA 시나리오**

무단 진입 시 재정적 또는 지적 재산권의 측면에서 높은 비용을 초래할 수 있는 은행 로그인 및 소스 코드 액세스와 같은 중요 계정에 대한 로그인 보호   

## <a name="mobile"></a>모바일
모바일 장치에 대 한 앱을 만드는 경우 Azure는 hello 클라우드에서 데이터를 저장, 사용자를 인증 및 다양 한 사용자 지정 코드 toowrite 필요 없이 푸시 알림을 보낼 수 있습니다.

가상 컴퓨터, 클라우드 서비스 또는 웹 응용 프로그램을 사용 하 여 모바일 앱에 대 한 백 엔드 hello 확실히 빌드할 수 하는 동안 Azure의 서비스를 사용 하 여 서비스 구성 요소를 기본 훨씬 더 적은 시간 쓰기 hello 소요 단축할 수 있습니다.

### <a name="mobile-apps"></a>Mobile Apps
![모바일 앱](./media/fundamentals-introduction-to-azure/MobileServicesIntroNew.png)

*그림: 모바일 앱은 모바일 장치와 상호 작용하는 응용 프로그램에 일반적으로 필요한 기능을 제공합니다.*

Azure 모바일 앱은 모바일 응용 프로그램용 백엔드를 빌드할 때 시간을 절약할 수 있는 유용한 기능을 많이 제공합니다. Toodo 간단한 프로 비전 및 SQL 데이터베이스에 저장 된 데이터를 관리할 수 있습니다. 서버 쪽 코드를 사용하면 Blob 저장소나 MongoDB와 같은 추가 데이터 저장소 옵션을 쉽게 사용할 수 있습니다. Mobile Apps는 알림을 지원합니다. 물론 특정한 경우에는 다음에 설명하는 알림 허브를 사용할 수도 있습니다.  hello 서비스 REST API에 모바일 응용 프로그램 수행 tooget 작업을 호출할 수 있습니다. 또한 모바일 앱 Microsoft와 Active Directory를 통해 tooauthenticate 사용자 뿐 아니라 Facebook, Twitter, Google 등 기타 잘 알려진 id 공급자 hello 기능을 제공 합니다.   

서비스 버스 및 작업자 역할을 같은 다른 Azure 서비스를 사용 하 고 tooon 온-프레미스 시스템을 연결할 수 있습니다. Hello tooprovide 추가 기능 (예: 전자 메일에 대 한 SendGrid) Azure 저장소에서에서 타사 애드온도 사용할 수 있습니다.

Native client 라이브러리 Android, iOS, HTML/JavaScript, Windows Phone 및 Windows 스토어에 대 한 모든 주요 모바일 플랫폼에서 앱에 대 한 보다 쉽게 toodevelop 지정. REST API toouse 모바일 서비스 데이터 및 서로 다른 플랫폼에서 앱과 인증 기능을 사용합니다. 단일 모바일 서비스를 사용하여 복수의 클라이언트 앱을 지원할 수 있으며 장치 간에 일관적인 사용자 경험을 제공할 수 있습니다.

Azure에서 대규모를 이미 지원 하므로 앱이 더 인기가 hello 트래픽을 처리할 수 있습니다.  모니터링 및 로깅을 지 원하는 toohelp 문제를 해결 하 고 성능을 관리 합니다.

### <a name="notification-hubs"></a>알림 허브
![NotificationHubs](./media/fundamentals-introduction-to-azure/NotificationHubsIntroNew.png)  

*그림: 알림 허브는 모바일 장치와 상호 작용하는 응용 프로그램에 일반적으로 필요한 기능을 제공합니다.*

Azure 모바일 앱에 알림을 toodo 코드를 작성할 수 있지만, 알림 허브는 최적화 된 toobroadcast 수백만 개의 항상 개인 설정 된 푸시 알림 분 이내입니다.  Tooworry 모바일 통신 회사 또는 장치 제조업체와 같은 세부 정보에 대 한 필요는 없습니다. 단일 API 호출로 개인 또는 수백만 명의 사용자를 대상으로 할 수 있습니다.

알림 허브는 원하는 백 엔드도 설계 된 toowork입니다. Azure 모바일 앱, hello 클라우드의 모든 공급자에서 실행 되는 사용자 지정 백 엔드 또는 온-프레미스 백엔드를 사용할 수 있습니다.

**알림 허브 시나리오** toonotify 플레이어 2를 할 수 있는 플레이어 걸린 turns 모바일 게임을 작성 하는 경우 해당 플레이어 1 그녀의 설정 완료 합니다. Toodo 하기만 하면 되는 경우에 모바일 앱을 사용할 수 있습니다. 10만 명의 사용자를 갖는 경우 하지만 게임을 재생 하 고 중요 한 무료 제공 tooeveryone, 알림 허브는 hello 적합 한 번 toosend 설정할 수 있습니다.

짧은 대기 시간으로 이벤트 및 사용자의 제품 알림 알림 toomillions 스포츠 주요 뉴스를 보낼 수 있습니다. 기업에서는 직원 전자 메일 또는 다른 응용 프로그램 toostay 정보를 확인 하는 tooconstantly 없는 새 시간이 중요 한 같은 통신 판매 정보에 대 한 직원에 게 알릴 수입니다. 또한 Multi-Factor Authentication에 필요한 1회용 암호도 전송할 수 있습니다.

## <a name="back-up"></a>백업
모든 enterprise 데이터 toobackup 및 복원 해야합니다. Azure toobackup 사용 및 hello 클라우드 또는 온-프레미스에서 응용 프로그램을 복원할 수 있습니다. Azure 백업의 hello 유형에 따라 toohelp 다양 한 옵션을 제공합니다.

### <a name="site-recovery"></a>사이트 복구
Azure 사이트 복구 (이전의 Hyper-v 복구 관리자)는 사이트에 걸쳐 hello 복제 및 복구를 조정 하 여 중요 한 응용 프로그램을 보호 하는 데 유용 합니다. 사이트 복구 기능 tooprotect 응용 프로그램 hyper-v, VMWare 또는 SAN tooyour 자체 보조 사이트, tooa 호스터의 사이트 또는 tooAzure 기반 및 hello 비용 및 복잡 한 빌드 및 보조 위치를 직접 관리를 방지를 제공 합니다. Azure 데이터를 암호화 하 고 통신 하 고 옵션이 hello 너무 rest에서 데이터에 대 한 암호화를 사용 하도록 설정 합니다.

서비스의 hello 상태를 지속적으로 모니터링 하 고 hello hello hello 기본 데이터 센터에 사이트 중단 이벤트에서 서비스의 순차적 복구 자동화 합니다. 가상 컴퓨터 수 가져와 오케스트레이션된으로 toohelp 복원 서비스에 신속 하 게 복잡 한 다중 계층 작업에 대해서도 합니다.

사이트 복구는 Hyper-V 복제본, System Center, SQL Server Always On 등의 기존 기술에서도 작동합니다. 자세한 내용은 [Azure 사이트 복구 개요](site-recovery/site-recovery-overview.md) 를 확인합니다.

### <a name="azure-backup"></a>Azure 백업
![Azure Backup](./media/fundamentals-introduction-to-azure/AzureBackupIntroNew.png)  

*그림: Azure 백업에서에서 데이터를 백업 온-프레미스 Windows 서버 hello 클라우드로 합니다.*  

Azure 백업은 hello 클라우드로 Windows Server를 실행 하는 온-프레미스 서버에서 데이터를 백업 합니다. Windows Server 2012, Windows Server 2012 Essentials 또는 System Center 2012-Data Protection Manager의 백업 도구 hello에서 직접 백업을 관리할 수 있습니다. 또는 전문 백업 에이전트를 사용할 수 있습니다.

전송 전에 백업이 암호화되며 Azure에 암호화된 상태로 저장되고 사용자가 업로드한 인증서로 보호되므로 데이터가 더 안전합니다. hello 서비스는 hello Azure 저장소에 있는 동일한 중복 및 항상 사용 가능한 데이터 보호를 사용 합니다.  전체 백업 또는 증분 백업을 실행하여 파일 및 폴더를 정기적으로 또는 즉시 백업할 수 있습니다. 데이터를 toohello 클라우드 백업 후 권한이 있는 사용자가 백업을 tooany 서버를 쉽게 복구할 수 있습니다. 또한 구성 가능한 데이터 보존 정책, 데이터 압축 및 데이터 전송 제한 hello 비용 toostore 및 전송 데이터를 관리할 수 있도록 제공 합니다.

**Azure 백업에 대한 시나리오**

Windows Server 또는 System Center를 이미 사용하는 경우 Azure 백업은 서버 파일 시스템, 가상 컴퓨터 및 SQL Server 데이터베이스를 백업하는 데 사용할 수 있는 자연스러운 솔루션입니다.  이 솔루션은 암호화된, 스파스 및 압축 파일에 대해 작업합니다. 있으므로 몇 가지 제한 사항이 [hello Azure 백업에 대 한 필수 조건 확인](http://technet.microsoft.com/library/dn296608.aspx) 첫 번째입니다.

## <a name="messaging-and-integration"></a>메시징 및 통합
무엇이에 관계 없이 코드는 다른 코드와 함께 toointeract 자주 필요 합니다.  상황에 따라서는 기본 대기 중인 메시징이 가장 필요해질 수 있으며, 다른 경우에는 좀 더 복잡한 상호 작용이 필요할 수 있습니다. Azure는 이러한 문제는 몇 가지 방법으로 toosolve를 제공합니다. 그림 5 hello 선택 항목을 보여 줍니다.

### <a name="queues"></a>큐
![Azure 서비스 버스 릴레이](./media/fundamentals-introduction-to-azure/QueuesIntroNew.png)

*그림: 큐는 응용 프로그램 내의 부분 간 연결을 느슨하게 하여 크기 조정을 용이하게 해줍니다.*  

큐는 간단한 아이디어입니다. 응용 프로그램이 어떤 메시지를 큐에 보내면 다른 응용 프로그램이 그 메시지를 읽습니다. 응용 프로그램 뿐이 간단 하 게 서비스에 필요한 hello 적합 하 고 Azure 큐 수 있습니다.

Hello 방식으로 hello 증가 하 여 Azure, 때문에 Azure 저장소 큐 및 서비스 버스 큐는 비슷한 큐 서비스를 제공 합니다. hello 상당히 기술 문서에서 그는 이유 toouse 하나 hello 통해 다른 hello 이유가 설명 되어 [Azure 큐 및 서비스 버스 큐-비교 및 대조](http://msdn.microsoft.com/library/azure/hh767287.aspx)합니다.  많은 시나리오에서 두 가지 서비스가 모두 작동합니다.

**큐 시나리오**

동일한 클라우드 서비스 응용 프로그램을 hello 중요 한 한 큐의 일반적인 용도 오늘 toolet 웹 역할 인스턴스 내에서 작업자 역할 인스턴스를와 통신 합니다.

예를 들어 비디오를 공유하는 Azure 응용 프로그램을 작성한다고 가정합시다. hello 응용 프로그램의 PHP 실행 되는 코드 업로드 하면 사용자가 업로드 하 고 변환 하는 C#에서 구현 되는 작업자 역할 함께 비디오를 시청 하는 웹 역할에서 비디오를 다양 한 형식으로 구성 됩니다.

웹 역할 인스턴스에서 사용자 로부터 새 비디오 가져오면 hello 비디오는 blob에 저장 하 다음 알려 큐를 통해 메시지 tooa 작업자 역할을 보낼 수 있는 새로운 toofind 비디오입니다. 작업자 역할 인스턴스 it hello 큐에서 읽기 그러면 하나에서 hello 메시지는 중요 하 고 필요한 hello 비디오 번역 hello 백그라운드에서 수행 하지 않습니다.

비동기 처리를 사용 하면 이러한 방식으로 응용 프로그램을 구성 하 고 hello 웹 역할 인스턴스 수 및 작업자 역할 인스턴스를 독립적으로 변경 될 수 있으므로 응용 프로그램 보다 쉽게 tooscale hello 수도 있습니다. 작업자 역할을 위아래로 트리거 tooscale hello 수로 hello 큐 크기를 사용할 수도 있습니다. 값이 높아질수록 더 많은 역할을 추가할 수 있습니다. 더 낮은 가져오면 toosave money 역할을 실행 중인 hello 수를 줄일 수 있습니다.  

웹 또는 작업자 역할을 사용하지 않더라도 응용 프로그램 내의 많은 다른 부분들 간에 이러한 동일한 패턴을 사용할 수 있습니다.  요청을 위아래로 hello 큐의 어느 쪽에 tooscale hello 부분 허용 및 처리 시간이 필요 합니다.

### <a name="service-bus"></a>서비스 버스
모바일 장치 또는 다른 곳에서 해당 데이터 센터에서 hello 클라우드 실행할지 toointeract 응용 프로그램에 필요 합니다. Azure 서비스 버스의 hello 목표는 데이터를 교환 하는 거의 모든 위치를 실행 중인 toolet 응용 프로그램입니다.

또한 toohello 큐 (일대일) 앞에서 설명한 서비스 버스 tooother를 통신 방법도 제공 합니다.

#### <a name="service-bus-relay"></a>서비스 버스 릴레이
![Azure 서비스 버스 릴레이](./media/fundamentals-introduction-to-azure/ServiceBusRelayIntroNew.png)

*그림: 서비스 버스 릴레이는 방화벽의 다른 쪽에 있는 응용 프로그램 간에 통신을 허용합니다.*

서비스 버스 방화벽을 통해 안전 하 게 toointeract 제공 하는 릴레이 서비스를 통해 직접 통신을 허용 합니다. 서비스 버스 릴레이 hello 클라우드에서 보다는 로컬에서 호스팅되는 끝점을 통해 메시지를 교환 하 여 응용 프로그램 toocommunicate를 사용 합니다.

**서비스 버스 릴레이 시나리오**

서비스 버스를 통해 통신하는 응용 프로그램은 Azure 응용 프로그램 또는 다른 클라우드 플랫폼에서 실행되는 소프트웨어일 수 있습니다. 그러나 hello 클라우드 외부에서 실행 되는 응용 프로그램 수도 있습니다. 예를 들어 자체 데이터 센터 내부의 컴퓨터에서 예약 서비스를 구현하는 항공사를 생각해 보겠습니다. hello airline tooexpose 공항, 예약 에이전트 터미널, 및 이전에 고객의 휴대폰에 체크 인 키오스크 등의 이러한 서비스 toomany 클라이언트를 필요 합니다. 사용할 수 있습니다 서비스 버스 toodo hello 간의 느슨하게 결합 된 상호 작용 다양 한 응용 프로그램을 만드는이 있습니다.

#### <a name="service-bus-topics-and-subscriptions"></a>서비스 버스 토픽 및 구독
![Azure Service Bus Topics](./media/fundamentals-introduction-to-azure/ServiceBusTopicsSubsIntroNew.png)   
 *그림: 여러 앱 toopost 메시지 및 특정 조건을 충족 하는 다른 응용 프로그램 toosubscribe tooreceive 메시지가 서비스 버스 항목 허용 합니다.*

서비스 버스는 토픽 및 구독이라고 하는 게시-구독 메커니즘을 제공합니다. 기업을, 다른 응용 프로그램 구독 toothis 항목을 만들 수 있지만 응용 프로그램 tooa 부분 메시지를 보낼 수 있습니다. 이 hello 동일한 메시지가 여러 수신자가 읽게 될 수 있도록 응용 프로그램 집합 간의 일 대 다 통신을 허용 합니다.

**서비스 버스 토픽 및 구독 시나리오**

설정 하는 있는 모든 중요 한 많은 메시지가 하지만 다양 한 다운스트림 시스템 이러한 통신의 toolisten toodiffering 하위 집합을 언제 든 지 서비스 버스 항목 및 구독은 좋은 방법입니다.

### <a name="biztalk-services"></a>BizTalk 서비스
![BizTalk 서비스](./media/fundamentals-introduction-to-azure/BizTalkServicesIntroNew.png)   
 *그림: BizTalk 서비스는 hello 클라우드에서 hello 기능 tootransform XML 메시지 형식을 제공 합니다.*

때로 서로 다른 메시징 형식을 사용하여 통신하는 시스템을 연결해야 하는 경우가 있습니다. 것 비즈니스 toohave 다른 데이터베이스 스키마 및 XML는 공통 표준인 사용할 수 있는 경우에 형식, 메시징에 대 한 합니다. 많은 사용자 지정 코드를 작성 하지 않고에 BizTalk Server 온-프레미스 toointegrate 다양 한 시스템으로 사용할 수 있습니다.  Azure BizTalk 서비스는 hello 제공을 서비스의 하지만 hello 클라우드에서 동일한 형식입니다. 만 사용 하 여 및 작업 걱정할 필요가 배율 tooon 온-프레미스 할 것 처럼 결제할 수 있습니다.

**BizTalk 서비스 시나리오**

B2B(Business-to-Business) 상호 작용에는 보통 이 유형의 변환이 필요합니다.  예를 들어 회사에서 tooorder 파트 비행기 요구를 빌드 다양 한 부분 공급자입니다. 협력 부품 공급자는 많아질 예정입니다.  해당 주문을 hello 공급 업체 시스템에 hello 비행기 빌더 시스템에서 직접 자동화 된 toogo 이어야 합니다.  두 비즈니스가 toochange 코어 시스템과 메시지 형식 및은 해당 형식의 동일 hello은 희박 합니다. BizTalk 서비스 메시지 걸리고 hello 새 형식 양방향 사이 변환 수 있습니다. 어느 hello 비행기 공급 업체 작업 tootranslate hello 수행 하거나 다양 한 공급 업체 hello 필요한 번역의 더 많은 제어 및 hello 양 싶은 사람이 누가 따라 수 있습니다.     

## <a name="compute-assistance"></a>계산 지원
Azure는 toorun hello 항상 필요 하지 않는 서비스에 대 한 지원을 제공 합니다.  

### <a name="scheduler"></a>스케줄러
![Azure Scheduler](./media/fundamentals-introduction-to-azure/SchedulerIntroNew.png)   
*그림: Azure 스케줄러 제공 방법을 tooschedule 작업이 특정 기간에 대 한 특정 시간에 합니다.*

응용 프로그램 하나만 필요한 경우가 toorun 특정 시간에. Azure에서이 유형의 응용 프로그램은 응용 프로그램을 방금 연중 무휴 tooprocess 데이터에 대 한 대기를 계속 실행 하는 대신 비용을 절약할 수 있습니다. Azure 스케줄러가 있습니다 tooschedule를 간격을 시간 또는 일정에 따라 응용 프로그램 실행 해야 하는 경우. 이렇게 하면 안정적이며 네트워크, 컴퓨터 및 데이터 센터 오류가 발생할 경우에도 프로세스가 실행되는지 확인할 수 있습니다. 이러한 작업 스케줄러 REST API toomanage hello를 사용합니다.

예약 된 경보가 발생 스케줄러 HTTP 또는 HTTPS 메시지 tooa 특정 끝점 보내거나 저장소 큐에 메시지를 넣을 수 있습니다.  Toohave 필요는 응용 프로그램에 액세스할 수 있는 끝점이 또는 저장소 큐를 모니터링 하 게 합니다. 그런 다음 hello 메시지, 되 면를 프로그래밍 하는 모든 작업을 수행할 수 것입니다.

**스케줄러 시나리오**

* 응용 프로그램 작업의 되풀이: 예를 들어, 서비스 수 있습니다 주기적으로 twitter에서 데이터를 가져올와 정기 피드에 hello 데이터를 수집 합니다.
* 일일 유지 관리: 로그 처리 또는 잘라내기, 백업 및 기타 일시적인 예약 작업
* 밤에 실행되는 작업
* 일별 로그 잘라내기, 백업 수행, 기타 유지 관리 작업 등의 웹 응용 프로그램 작업. 관리자가 선택할 수 있습니다 toobackup 그녀의 데이터베이스 hello에 대 한 매일 오전 1 시에 다음 9 개월 동안 예.

스케줄러 API hello 있습니다 toocreate, 업데이트, 삭제, 보기 및 작업 컬렉션 및 예약 된 작업을 프로그래밍 방식으로 관리 합니다.

## <a name="performance"></a>성능
성능은 항상 응용 프로그램에 중요합니다. 응용 프로그램은 tooaccess hello 동일한 데이터를 반복 합니다. 한 가지 방법은 tooimprove 성능은 tookeep 해당 데이터 자세히 toohello 응용 프로그램의 복사본, 최소화 hello 시간이 필요 tooretrieve 것입니다. Azure는 이를 위해 다양한 서비스를 제공합니다.

### <a name="azure-caching"></a>Azure 캐싱
![Azure Caching](./media/fundamentals-introduction-to-azure/AzureCacheIntroNew.png)   
 **그림: Azure 응용 프로그램은 메모리에 데이터를 캐시하고 많은 작업 역할에 걸쳐 분할할 수도 있습니다.**

Azure의 데이터 관리 서비스(SQL 데이터베이스, 테이블, Blob 등)에 저장된 데이터에는 비교적 빠르게 액세스할 수 있습니다. 하지만 메모리 내에 저장된 데이터에 액세스하면 속도가 더 빨라집니다. 자주 액세스하는 데이터의 메모리 내 복사본을 보관할 때 응용 프로그램의 성능이 향상되는 이유가 여기에 있습니다. Azure의 메모리 내 캐싱 toodo에이 사용할 수 있습니다.

클라우드 서비스 응용 프로그램은이 캐시에 데이터를 저장한 다음 tooaccess 영구 저장소 없이 직접 검색할 수 있습니다. 응용 프로그램의 Vm 또는 Vm에서 제공 하는 내부 전용 전적으로 toocaching hello 캐시를 유지할 수 있습니다. 두 경우 모두 hello 캐시를 배포할 수 있습니다, 그리고 hello 데이터와 Azure 데이터 센터에서 여러 Vm 간에 확산 포함 합니다.

Azure에는 시간에 따라 전환된 다양한 캐시 기술이 많이 있습니다. 에 도입 된 hello 순서는 공유 된 역할에서 관리 하 고 Redis 캐시 합니다. hello 공유 캐싱 이전 기술 이며 새로운 구현 된 만들지 마십시오. hello 관리 되는 캐시에 hello hello 역할의 동일한 기능, 캐시 하지만 외부의 관리 되는 서비스로 hello Azure 관리 포털. hello Redis 캐시 미리 보기입니다. hello Redis 구현 기능의 hello 가장 큰 수 있으며 새 캐싱 코드를 작성 하는 경우에 권장 됩니다.

**Azure 캐시 시나리오**

제품 카탈로그를 반복적으로 읽는 응용 프로그램을 이러한 종류의 캐시를 사용 하 여 이점을 얻을 수, 예를 들어 hello 데이터 이후에 해야 사용할 수 있습니다 더 신속 하 게 합니다. hello 기술 잠금, 읽기 전용 데이터 뿐만 아니라 읽기/쓰기와 함께 사용할이 값도 지원 합니다. 및 ASP.NET 응용 프로그램만 구성 변경으로 hello 서비스 toostore 세션 데이터를 사용할 수 있습니다.

### <a name="content-delivery-network"></a>Content Delivery Network
![Azure CDN](./media/fundamentals-introduction-to-azure/CDNIntroNew.png)   
 **그림: hello 전 세계 사이트에서 blob의 복사본을 캐시할 수 있습니다.**

Hello 전 세계 사용자가 액세스할 수 있는 toostore blob 데이터 사용 한다고 가정 합니다. 어쩌면 hello 최신 World Cup 일치 하는 예를 들어, 드라이버 업데이트 또는 인기 있는 전자책 비디오를입니다. 여러 Azure 데이터 센터에 hello 데이터의 복사본을 저장는 도움이 되지만, 이지만 사용자가 많은 경우 하지 않을 충분 합니다. 더 나은 성능을 위해 hello Azure CDN을 사용할 수 있습니다.

CDN hello 전 세계 hello, 각각 Azure blob의 복사본을 저장할 수 있는 다양 한 사이트에 있습니다. hello hello world의 특정 부분에 사용자가 특정 blob에 액세스 하는 처음으로 포함 된 hello 정보에 복사 됩니다 Azure 데이터 센터에서 해당 지리적 위치에서 로컬 CDN 저장소. Hello world 부분에 대 한 액세스는 hello CDN에에서 캐시 된 hello blob 복사본을 사용 하는 데 이후 부터는-Azure 데이터 센터에 가장 가까운 모든 hello 방식으로 toohello toogo 필요한 하지 않습니다. hello 결과 hello world의 아무 곳 이나 사용자가 데이터에 빠르게 액세스 toofrequently 액세스입니다.

**CDN 시나리오**

것이 일반적인 toouse CDN을 전 세계 미디어 서비스 toodeliver 비디오를 포함 합니다. 동영상은 일반적으로 대용량이며 상당한 대역폭을 요구합니다.  미디어 서비스는 이 페이지의 다른 부분에서 다룹니다.

## <a name="big-data-and-big-compute"></a>빅데이터 및 빅컴퓨팅
### <a name="hdinsight-hadoop"></a>HDInsight(Hadoop)
![HDInsight](./media/fundamentals-introduction-to-azure/HDInsightIntroNew.png)   
 **그림: HDInsight hello 대량 처리 엄청난 양의 데이터와 함께 사용 하면**

수 년에 대 한 관계형 DBMS를 사용 하 여 작성 하는 데이터 웨어하우스에 저장 된 관계형 데이터에 hello 대량의 데이터 분석을 수행 하지 않았습니다. 이러한 종류의 비즈니스 분석은 여전히 중요 하 고 오랜 시간이 toocome에 대 한 됩니다. 하지만 경우에 어떻게 tooanalyze hello 데이터는 관계형 데이터베이스만 처리할 수 없는 것 크기가 매우 커서? 고 hello 데이터가 아닌 관계형 가정 하 시겠습니까? 데이터 센터에 있는 서버 로그, 센서로부터 제공되는 기록 이벤트 데이터 등이 그 예입니다. 이것이 바로 빅데이터의 문제이며 여기에는 새로운 방식이 필요합니다.

빅 데이터 분석을 위해 오늘 주요 기술 hello Hadoop입니다. 오픈 소스 프로젝트는 Apache,이 기술을 hello Hadoop 분산 파일 시스템 (HDFS)를 사용 하 여 데이터를 저장 한 후 개발자는 MapReduce 작업 tooanalyze 해당 데이터를 만들 수 있습니다. HDFS 각각 hello 빅 데이터 하기 때문에 hello MapReduce 작업의 실행 청크 동시에 처리 한 다음 여러 서버에서 데이터를 확산 됩니다.

HDInsight는 hello 이름 hello Azure의 Apache Hadoop 기반 서비스입니다. HDInsight HDFS를 hello 클러스터에서 데이터를 저장 하 고 여러 Vm에 분산할 수 있습니다. 또한 해당 Vm에서 MapReduce 작업의 hello 논리를 분산 합니다. 와 마찬가지로 온-프레미스 Hadoop 데이터는 처리 된 로컬로-hello 논리에서 작동 하는 hello 데이터는 동일한 VM hello-병렬 성능 향상을 위해 합니다. HDInsight는 또한 Blob을 사용하는 ASV(Azure Storage Vault)에 데이터를 저장합니다.  사용 ASV 하면 toosave money 중이 아닌 경우 사용 하 여 HDInsight 클러스터를 삭제할 수 있지만 여전히 hello 클라우드에서 데이터를 유지 하기 때문에 있습니다.

HDinsight은 Hive 및 Pig를 포함 하 여 hello Hadoop 생태계도의 다른 구성 요소를 지원 합니다. Microsoft는 또한 좀 더 쉽게 toowork HDInsight에서 생성 된 데이터와 hello HiveODBC 어댑터 및 Excel을 사용 하는 데이터 탐색기와 같은 기존 BI 도구를 사용 하 여 구성 요소를 만들었습니다.

### <a name="high-performance-computing-big-compute"></a>HPC(고성능 컴퓨팅)(빅컴퓨팅)
Hello 가장 유용한 방법으로 toouse 클라우드 플랫폼 중 하나는 toorun 고성능 컴퓨팅 (HPC) 및 기타 "큰 계산" 응용 프로그램입니다. 예로 특수 한 엔지니어링 빌드된 응용 프로그램을 toouse hello 소위 병렬 응용 프로그램의 경우 이러한 재무 위험 모델 뿐 아니라 업계 표준 인터페이스 MPI (Message Passing).

큰 계산의 hello 핵심 hello에서 많은 컴퓨터에서 코드를 실행 중인 동시 합니다. Azure에서 즉 여러 가상 컴퓨터를 동시에 실행에 문제가 병렬 toosolve에서 작업 하는 모든. 이 인스턴스 간에 몇 가지 방식으로 tooresources 및 tooschedule 응용 프로그램을 toodistribute 즉, 해당 작업을 필요이 작업을 수행 합니다. Microsoft의 무료 HPC Pack와 다른 계산 클러스터 솔루션, 활용 Azure 계산 및 인프라 서비스 tooadd 용량 주문형 tooan 온-프레미스 계산 클러스터 또는 hello에서 전적으로 큰 계산 응용 프로그램 실행에 수행할 수 있습니다. 클라우드입니다.

Azure VM의 범위와 CPU 코어, 메모리, 디스크 용량 및 다른 응용 프로그램의 다른 특징 toomeet hello 요구의 구성이 각기 다른 인스턴스 크기를 제공합니다. hello을 최근에 도입 된 A8 및 A9 인스턴스 작업에 많은 계산 집약적인 작업 및 병렬 MPI 응용 프로그램 특히 고속의 멀티 코어 Cpu 및 많은 양의 메모리를 갖기 때문입니다. 특정 구성에서 hello 인스턴스 낮은 대기 시간 및 처리량이 높은 응용 프로그램 네트워크에서에서 활용 병렬 MPI 응용 프로그램의 최대 효율성을 위해 원격 직접 메모리 액세스 (RDMA) 기술을 포함 하는 hello 클라우드입니다.

또한 Azure는 빅컴퓨팅 응용 프로그램 개발자 및 파트너에게 계산 기능, 서비스, 아키텍처 선택 사항 및 개발 도구의 완전한 집합을 제공합니다. Azure는 특수 한 데이터 워크플로와 관련 된 사용자 지정 큰 계산 워크플로 지원 하 고 작업 및 태스크 예약 패턴이의 toothousands 확장할 수 있는 코어를 계산 합니다.

## <a name="media"></a>미디어
![Azure Media Services](./media/fundamentals-introduction-to-azure/MediaServicesIntroNew.png)   
 **그림: 미디어 서비스는 비디오 및 기타 미디어 tooclients hello 전 세계 제공 하는 응용 프로그램에 대 한 플랫폼.**

오늘날 비디오는 인터넷 트래픽의 큰 부분을 차지하고 있고 그 비율은 앞으로 더 늘어날 것입니다. 아직 hello 웹에서 비디오를 제공 하 쉽지 않습니다. 변수를 많은, hello 같은 인코딩 알고리즘 및 hello hello 사용자의 화면 해상도 표시 됩니다. 합니다. 비디오에는 많은 사용자 toowatch 온라인 동영상 만족할 만한 결정할 때 토요일 밤 스파이크 같은 수요가 toohave 급증은 경향이 있습니다.

인기도를 고려할 때 수많은 새 응용 프로그램이 비디오 기능을 포함하는 것은 안전한 투자로 볼 수 있을 것입니다. 이러한 모든 일부 toosolve 필요 하지만 hello의 동일한 문제 및 해당 문제를 자체적으로 해결 하나씩 만드는 의미가 없습니다. 더 나은 방법은 toocreate 많은 응용 프로그램 toouse에 대 한 일반적인 솔루션 제공 하는 플랫폼입니다. 및이 플랫폼 hello 클라우드에서 구축 몇 가지 장점이 선택을 취소 합니다. 종 량 제 기준 광범위 하 게 사용할 수 있습니다 및 hello 가변성에서 비디오 응용 프로그램에 종종 맞서게 요구를 처리할 수도 있습니다.

Azure 미디어 서비스가 이 문제를 해결해 줍니다. Azure 미디어 서비스는 비디오나 다른 미디어를 사용하여 응용 프로그램을 작성하고 실행하는 사람들의 편의를 위해 클라우드 구성 요소 집합을 제공합니다.

Hello 그림에서 볼 수 있듯이 미디어 서비스는 비디오 및 기타 미디어를 사용 하는 응용 프로그램에 대 한 구성 요소 집합을 제공 합니다. 예를 들어 미디어 포함 됩니다 (저장 된 Azure Blob에) 미디어 서비스, 인코딩 구성 요소가 지 원하는 다양 한 비디오 및 오디오 형식, 디지털 권한 관리를 제공 하는 콘텐츠 보호 구성에 구성 요소 tooupload 비디오 수집 비디오 스트림, 스트리밍에 대 한 구성 요소에 광고를 삽입 하기 위한 구성 요소입니다. Microsoft 파트너 hello 플랫폼에 대 한 구성 요소를 제공 합니다. 다음 이러한 구성 요소를 배포 하 고 대신 요금을 청구할 microsoft 수도 있습니다.

이 플랫폼을 사용하는 응용 프로그램은 Azure나 다른 서비스에서 실행할 수 있습니다. 예를 들어 데스크톱 응용 프로그램 비디오 프로덕션 집 비디오 tooMedia 서비스 업로드에서 사용자에 게 할당할 수도 있습니다에 대 한 다음 처리 다양 한 방법으로. 또는 Azure에서 실행 되는 콘텐츠 관리 클라우드 기반 서비스 tooprocess 미디어 서비스에 의존 하 고 비디오를 배포할 수 있습니다. 각 응용 프로그램 구성 요소를 선택 실행 아무 곳에 나 되며 그렇게 무엇이 든, toouse, RESTful 인터페이스를 통한 액세스 필요 합니다.

toodistribute 생성 기능, 응용 프로그램이 다른 CDN hello Azure CDN을 사용할 수 또는 정당한 송신에서는 직접 비트 toousers 합니다. 어떤 방법으로든 배포된 후에는 미디어 서비스를 사용하여 작성된 비디오를 다양한 클라이언트 시스템(Windows, Macintosh, HTML 5, iOS, Android, Windows Phone, Flash, Silverlight 등)에서 사용할 수 있습니다. hello ´ ֲ toomake 것 보다 쉽게 toocreate 최신 미디어 응용 프로그램입니다.

**참조**

미디어 서비스의 작동 방식을 보다 시각적 보기에 대 한 다운로드 hello [Azure 미디어 서비스 포스터][Azure Media Services Poster]합니다.

## <a name="commerce"></a>상거래
응용 프로그램 작성 방법 서비스로 소프트웨어의 hello 등장 변형 것입니다. 이는 응용 프로그램을 판매하는 방법도 달라진다는 의미입니다. SaaS 응용 프로그램 hello 클라우드에 거주 하 고, 이후는 잠재 고객의 온라인 솔루션 찾아야 하는 것이 좋습니다. 이러한 변경으로 toodata tooapplications 적용 합니다. 서는 안 사람 보이는 이유 toohello 클라우드 상업적으로 사용할 수 있는 데이터 집합에 대 한? Microsoft의 hello로 이러한 문제를 모두 해결 [Azure 마켓플레이스](https://azure.microsoft.com/marketplace/)합니다.

![Azure Commerce](./media/fundamentals-introduction-to-azure/CommerceIntroNew.png)   
 **그림: Azure Marketplace 및 Azure Store어를 통해 Azure 응용 프로그램 및 상용 데이터 집합을 찾아서 구매하고 Azure 응용 프로그램의 일부로 사용할 수 있습니다.**

hello hello 2 간의 차이 hello Azure 관리 포털 외부에서 마켓플레이스 이지만 hello 저장소에서 액세스할 수 hello 포털 내부 합니다. 잠재 고객 toofind Azure를 검색할 수 요구 사항을 충족 하는 응용 프로그램입니다. 고객은 인구 통계 데이터, 경제 데이터, 지리적 데이터 등뿐만 아니 상거래 데이터 집합을 검색할 수 있습니다. 원하는 항목을 찾을 경우 수 액세스할 hello 공급 업체에서 마켓플레이스 hello 또는 저장소 웹 위치를 통해 직접 또는 hello 관리 포털에서에서 일부 경우에 합니다. 응용 프로그램 hello Bing 검색 API hello 웹 검색의 toohello 결과 액세스 부여 마켓플레이스를 통해 사용할 수도 있습니다.

**상거래 시나리오**

SendGrid는 hello toosend 전자 메일 수 있는 Azure 저장소에서에서 응용 프로그램입니다. 이 응용 프로그램은 안정적인 배달 및 통계와 같은 추가 기능을 제공합니다.  이 응용 프로그램 및 관련된 서비스를 구입 하지 않고 수 있습니다 이러한 인프라 toobuild 직접 보십시오.  

## <a name="getting-started"></a>시작하기
Hello 큰 그림 hello 다음 단계를가지고 toowrite 첫 번째 Azure 응용 프로그램은 합니다. 언어를 선택 [가져오기 적절 한 SDK hello](/downloads/), 계속 해 서 및 합니다. 클라우드 컴퓨팅은 hello 새 기본값-지금 시작 합니다.

[Azure Media Services Poster]: http://azure.microsoft.com/documentation/infographics/media-services/
