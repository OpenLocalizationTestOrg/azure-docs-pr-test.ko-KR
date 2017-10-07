---
title: "aaaBatch 및 hello 클라우드-Azure의에서 HPC 솔루션 | Microsoft Docs"
description: "Azure의 배치 및 고성능 컴퓨팅(HPC 및 Big Compute) 시나리오와 솔루션 옵션에 대해 알아보기"
services: batch, virtual-machines, cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: aab5401d-2baf-4cf2-bf20-ad224de33888
ms.service: batch
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c5a3c8859d1f95040bcdad15942a815d71eb4486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="batch-and-hpc-solutions-for-large-scale-computing-workloads"></a>대규모 컴퓨팅 워크로드를 위한 Batch 및 HPC 솔루션

Azure는 효율적이고 확장성 있는 *Big Compute*로도 불리는 배치 및 HPC(고성능 컴퓨팅)용 클라우드 솔루션을 소개합니다. 배운 Azure의 서비스 toosupport 및 큰 계산 작업, 또는 너무 직접 이동할[솔루션 시나리오](#scenarios) 이 문서의 뒷부분에 나오는 합니다. 이 문서에서는 기술 의사 결정자, IT 관리자 및 독립 소프트웨어 공급 업체에 대해 주로 하지만 다른 IT 전문가 개발자가 사용할 수 it toofamiliarize 자체 이러한 솔루션.

조직에는 엔지니어링 디자인 및 분석, 이미지 렌더링, 복잡한 모델링, Monte Carlo 시뮬레이션, 재무 위험 계산 및 기타 대규모 컴퓨팅 문제가 있습니다. Azure는 hello 리소스, 규모 및 필요한 일정에 따라 이러한 문제를 해결 하는 조직은 수 있습니다. Azure를 활용하여 조직에서는 다음을 수행할 수 있습니다.

* 하이브리드 솔루션을 확장 하는 온-프레미스 HPC 클러스터 toooffload 최고 작업 toohello 클라우드가 만들으십시오
* Azure에서 전체 HPC 클러스터 도구 및 워크로드 실행
* 와 같은 관리 되 고 확장 가능한 Azure 서비스를 사용 하 여 [일괄 처리](https://azure.microsoft.com/documentation/services/batch/) toodeploy 필요 없이 계산 집약적인 작업 toorun 계산 인프라 및 관리

이 문서의 hello 범위를 초과 하지만 Azure 개발자와 파트너에 전체 집합도 제공 기능, 아키텍처 및 개발 도구 toobuild 대규모, 사용자 지정 큰 계산 워크플로 합니다. 이며 증가 파트너 에코 시스템 준비 toohelp 여 큰 계산 작업 hello Azure 클라우드에서에서 생산성을 확인 합니다.

## <a name="batch-and-hpc-applications"></a>배치 및 HPC 응용 프로그램
웹 응용 프로그램 및 많은 기간 업무 응용 프로그램과 달리 배치 및 HPC 응용 프로그램에는 정의 된 시작과 끝이 있으며 때때로 몇 시간 이상 일정이 또는 요청에 따라 실행할 수 있습니다. 대부분 두 가지 주요 범주로 분류: *기본적으로 병렬* ("병렬 난해한" hello 문제를 해결 하기 위해 여러 컴퓨터 또는 프로세서에서 병렬로 toorunning을 활용 하기 때문에) 및 *밀접 하 게 결합 된*합니다. Hello 이러한 응용 프로그램 종류에 대 한 자세한 내용은 다음 표를 참조 하십시오. 일부 Azure 솔루션에서는 한 형식이 나 다른 hello에 대 한 더 잘 작동 합니다.

> [!NOTE]
> 배치 및 HPC 솔루션에서 응용 프로그램의 실행 중인 인스턴스는 일반적으로 *작업*이라고 하며 각 작업은 *태스크*로 나눌 수 있습니다. Hello hello 응용 프로그램에 대 한 클러스터형된 계산 리소스 통칭 되 고 *계산 노드*합니다.
> 
> 

| 형식 | 특성 | 예 |
| --- | --- | --- |
| **본질적 병렬**<br/><br/>![본질적 병렬][parallel] |• 개별 컴퓨터는 응용 프로그램 논리를 독립적으로 실행<br/><br/> • 추가 컴퓨터 하면 hello 응용 프로그램 tooscale 늘어나고 감소 계산 시간<br/><br/>• 응용 프로그램은 별도 실행 파일로 구성되거나 클라이언트에서 호출하는 서비스의 그룹으로 구분됨(서비스 지향 아키텍처, 또는 SOA, 응용 프로그램)  |• 재무 위험 모델링<br/><br/>• 이미지 렌더링 및 이미지 처리<br/><br/>• 미디어 인코딩 및 코드 변환<br/><br/>• Monte Carlo 시뮬레이션<br/><br/>• 소프트웨어 테스트 |
| **Tightly coupled**<br/><br/>![Tightly coupled][coupled] |• 응용 프로그램에 계산 노드 toointeract 또는 exchange 중간 결과 필요<br/><br/>계산 노드를 사용 하 여 통신할 수 • hello 인터페이스 MPI (Message Passing), 병렬 컴퓨팅을 위한 일반 통신 프로토콜인<br/><br/>• hello 응용 프로그램은 중요 한 toonetwork 대기 시간 및 대역폭<br/><br/>• 응용 프로그램의 성능은 InfiniBand 및 원격 직접 메모리 액세스(RDMA)와 같은 고속 네트워킹 기술을 사용하여 향상시킬 수 있음. |• 석유 및 가스 저장소 모델링<br/><br/>• 컴퓨팅 유체 역학 같은 엔지니어링 디자인 및 분석<br/><br/>• 자동차 충돌, 핵 반응 같은 물리적 시뮬레이션<br/><br/>• 날씨 예측 |

### <a name="considerations-for-running-batch-and-hpc-applications-in-hello-cloud"></a>Hello 클라우드에서 일괄 처리 및 HPC 응용 프로그램을 실행 하기 위한 고려 사항
온-프레미스 HPC 클러스터 tooAzure 또는 tooa (크로스-프레미스) 하이브리드 환경에서 디자인 된 toorun 되는 많은 응용 프로그램을 쉽게 마이그레이션할 수 있습니다. 그러나 다음 사항 등 일부 제한사항 또는 고려사항이 있을 수 있습니다.

* **클라우드 리소스의 가용성** -hello 사용할 클라우드 계산 리소스의 유형에 따라 수 없는 지속적으로 컴퓨터 수 toorely은 작업이 실행 되는 동안 합니다. 상태 처리 및 진행률 클라우드 리소스를 사용 하는 경우 일반적인 기술 toohandle 가능한 일시적인 오류 및 자세한 필요를 가리키는지 확인 합니다.
* **데이터 액세스** -NFS와 같은 엔터프라이즈 클러스터에서 일반적으로 사용할 수 있는 데이터 액세스 기술은 hello 클라우드에서 특별 한 구성이 필요할 수 있습니다. 또는 hello 클라우드에 대 한 tooadopt 서로 다른 데이터 액세스 방법 및 패턴을 할 수 있습니다.
* **데이터 이동** -프로세스 많은 양의 데이터를 전략은 클라우드 저장소, toocompute 리소스에 필요한 toomove hello 데이터는 응용 프로그램에 대 한 합니다. [Azure ExpressRoute](https://azure.microsoft.com/services/expressroute/)와 같은 고속 크로스-프레미스 네트워킹이 필요할 수도 있습니다. 또한 해당 데이터를 저장하거나 액세스하기 위해 법, 규정 또는 정책 제한 사항 고려합니다.
* **라이선스** -라이선스에 대 한 상용 응용 프로그램의 공급 업체에 hello 또는에서 실행 하기 위한 기타 제한 사항 클라우드를 환영 합니다. 일부 공급 업체는 종량제 라이선스를 제공합니다. 솔루션에 대 한 hello 클라우드에서 라이선스 서버에 대 한 tooplan를 필요 하거나 tooan 온-프레미스 라이선스 서버에 연결 될 수 있습니다.

### <a name="big-compute-or-big-data"></a>큰 계산 또는 빅 데이터?
빅 데이터 및 큰 계산 응용 프로그램 간의 구분선 hello 명확 항상 없고 일부 응용 프로그램에는 두 가지의 특성 있을 수 있습니다. 두 가지 모두 컴퓨터의 클러스터에서 일반적으로 대규모 계산을 실행할 것을 포함합니다. 하지만 hello 솔루션 접근 방식 및 지원 도구 다를 수 있습니다.

• **큰 계산** tooinvolve 의존는 응용 프로그램 CPU 성능과 메모리 같은 엔지니어링 시뮬레이션, 재무 위험 모델링 및 디지털 렌더링과 하는 경향이 있습니다. 큰 계산 솔루션에 대 한 hello 인프라 특수 멀티 코어 프로세서 tooperform 원시 계산을 사용 하는 컴퓨터 및 특수 한 고속 네트워킹 하드웨어 tooconnect hello 컴퓨터 포함 될 수 있습니다.

• **빅 데이터** 는 단일 컴퓨터 또는 데이터베이스 관리 시스템에 의해 관리될 수 없는 다량의 데이터를 포함하는 데이터 분석 문제를 해결합니다. 예로는 대량의 웹 로그 또는 기타 비즈니스 인텔리전스 데이터가 있습니다. 빅 데이터 toorely 디스크 용량 및 cpu 보다 I/O 성능에 더 많은 경향이 있습니다. Apache Hadoop toomanage hello 클러스터 및 파티션 hello 데이터와 같은 특수 한 빅 데이터 도구가 있습니다. (Azure HDInsight 및 다른 Azure Hadoop 솔루션에 대한 정보는 [Hadoop](https://azure.microsoft.com/solutions/hadoop/)을 참조하십시오.)

## <a name="compute-management-and-job-scheduling"></a>계산 관리 및 작업 예약
종종 실행 중인 일괄 처리 및 HPC 응용 프로그램에 포함 되어는 *클러스터 관리자* 및 *작업 스케줄러* toohelp 클러스터형된 계산 리소스를 관리 하 고 hello 작업을 실행 하는 toohello 응용 프로그램을 할당 합니다. 이러한 함수는 별도 도구나 통합된 도구 또는 서비스로 수행할 수 있습니다.

* **클러스터 관리자** - 계산 리소스 (또는 계산 노드)를 프로비전하고 릴리스하고 관리합니다. 클러스터 관리자에서 운영 체제 이미지의 설치를 자동화할 수 및 계산 노드에서 응용 프로그램 toodemands에 따라 계산 리소스를 확장 하 고 hello 노드의 hello 성능을 모니터링 합니다.
* **작업 스케줄러** -hello 리소스 지정 (예: 프로세서 또는 메모리) 응용 프로그램 요구 및 hello 경우 중 실행 됩니다. 작업 스케줄러 작업의 큐를 유지 관리 하 고 할당된 된 우선 순위나 기타 특성에 따라 리소스 toothem를 할당 합니다.

클러스터링 및 작업 예약 도구 Windows 기반 및 Linux 기반 클러스터용 잘 tooAzure 마이그레이션할 수 있습니다. 예를 들어 [Microsoft HPC 팩](https://technet.microsoft.com/library/cc514029)인 Windows 및 Linux HPC 워크로드용 Microsoft의 무료 계산 클러스터 솔루션은 Azure에서 실행하기 위한 여러 옵션을 제공합니다. 토크 및 SLURM와 같은 오픈 소스 도구 toorun Linux 클러스터를 빌드할 수도 있습니다. 표시할 수도 있습니다 상용 그리드 솔루션 tooAzure 같은 [TIBCO DataSynapse GridServer](https://azure.microsoft.com/blog/tibco-datasynapse-comes-to-the-azure-marketplace/), [IBM 스펙트럼 Symphony 및 Symphony LSF](https://azure.microsoft.com/blog/ibm-and-microsoft-azure-support-spectrum-symphony-and-spectrum-lsf/), 및 [Univa 그리드 엔진](http://www.univa.com/products/grid-engine)합니다.

Hello 다음 섹션에에서 나와 있는 것 처럼 Azure 서비스 toomanage 계산 리소스를 사용할 수 있으며 작업 없이 (또는 외에) 기존의 클러스터 관리 도구를 예약 해야 합니다.

## <a name="scenarios"></a>시나리오
다음은 세 가지 일반 시나리오 toorun 큰 계산 작업 Azure에서 기존 HPC 클러스터 솔루션, Azure 서비스 또는 hello 둘의 조합을 사용 하 여입니다. 각 시나리오를 선택하기 위한 주요 고려 사항이 나열되지만 전체 목록은 아닙니다. 더 솔루션에서 사용할 수 있습니다 hello 사용 가능한 Azure 서비스에 대 한는 hello 문서의 뒷부분에 나오는 합니다.

| 시나리오 | 선택한 이유는 무엇인가요? |
| --- | --- | --- |
| **HPC 클러스터 tooAzure 버스트**<br/><br/>[![클러스터 버스트][burst_cluster]](./media/batch-hpc-solutions/burst_cluster.png) <br/><br/> 자세한 정보:<br/>• [Burst HPC Pack을 사용한 tooAzure 작업자 인스턴스](https://technet.microsoft.com/library/gg481749.aspx)<br/><br/>• [HPC Pack을 사용하여 하이브리드 계산 클러스터 설정](../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)<br/><br/>• [TooAzure HPC Pack을 사용한 일괄 처리를 전환 합니다.](https://technet.microsoft.com/library/mt612877.aspx)<br/><br/> |• [Microsoft HPC 팩](https://technet.microsoft.com/library/cc514029) 또는 다른 온-프레미스 클러스터와 추가 Azure 리소스를 하이브리드 솔루션에 결합<br/><br/>•는 서비스 (PaaS) 가상 컴퓨터 인스턴스 (현재 Windows Server만 해당)으로 플랫폼에서 큰 계산 작업 toorun를 확장 합니다.<br/><br/>• 선택적 Azure 가상 네트워크를 사용하여 온-프레미스 라이선스 서버 또는 데이터 저장소에 액세스 |
| **Azure에서 완전한 HPC 클러스터 만들기**<br/><br/>[![IaaS의 클러스터][iaas_cluster]](./media/batch-hpc-solutions/iaas_cluster.png)<br/><br/>자세한 정보:<br/>• [Azure의 HPC 클러스터 솔루션](big-compute-resources.md)<br/><br/> |• 표준 또는 사용자 지정 Windows 또는 Linux IaaS(infrastructure as a service) 가상 컴퓨터에 빠르고 일관되게 응용 프로그램 및 클러스터 도구 배포.<br/><br/>•는 Hello 작업 솔루션 선택한 일정을 사용 하 여 다양 한 큰 계산 작업을 실행 합니다.<br/><br/>•는 네트워킹 및 저장소 toocreate 전체 클라우드 기반 솔루션을 비롯 한 추가 Azure 서비스를 사용 합니다. |
| **병렬 응용 프로그램 tooAzure 확장**<br/><br/>[![Azure 배치][batch_proc]](./media/batch-hpc-solutions/batch_proc.png)<br/><br/>자세한 정보:<br/>• [Azure 배치의 기본 사항](batch-technical-overview.md)<br/><br/>• [.NET 용 hello Azure 배치 라이브러리 시작](batch-dotnet-get-started.md) |• 사용 하 여 개발 [Azure 배치](https://azure.microsoft.com/documentation/services/batch/) tooscale Windows 또는 Linux 가상 컴퓨터의 풀에 있는 다양 한 큰 계산 작업 toorun 아웃 합니다.<br/><br/>• Azure 플랫폼 서비스 toomanage 배포 및 가상 컴퓨터, 작업 예약, 재해 복구, 데이터 이동, 종속성 관리 및 응용 프로그램 배포의 자동 크기 조정을 사용 합니다. |

## <a name="azure-services-for-big-compute"></a>큰 계산에 대한 azure 서비스
Hello 계산, 데이터, 네트워킹 및 큰 계산 솔루션 및 워크플로를 결합할 수는 관련된 서비스에 대 한 자세한 다음과 같습니다. Azure 서비스에 대 한 자세한 지침 참조에 대 한 Azure 서비스 hello [설명서](https://azure.microsoft.com/documentation/)합니다. hello [시나리오](#scenarios) 이 문서의 앞부분에서 이러한 서비스를 사용 하 여 몇 가지 방법을 보여 줍니다.

> [!NOTE]
> Azure는 정기적으로 시나리오에 유용할 수 있는 새로운 서비스를 도입합니다. 질문이 있는 경우 [Azure 파트너](https://pinpoint.microsoft.com/en-US/search?keyword=azure) 또는 전자 메일 *bigcompute@microsoft.com*에 문의하세요.
> 
> 

### <a name="compute-services"></a>Compute services
Azure 계산 서비스는 큰 계산 솔루션 및 다양 한 시나리오에 대 한 hello 다른 계산 서비스 제공 장점과의 hello 핵심입니다. 기본적인 수준에서 이러한 서비스는 Windows Server Hyper-v 기술을 사용 하 여 Azure에서 제공 하는 가상 컴퓨터 기반 계산 인스턴스에서 toorun 응용 프로그램에 대 한 서로 다른 모드를 제공 합니다. 이러한 인스턴스는 표준 및 사용자 지정 Linux 및 Windows 운영 체제와 도구를 실행할 수 있습니다. Azure는 CPU 코어, 메모리, 디스크 용량 및 기타 특성의 서로 다른 구성을 가진 [인스턴스 크기](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 를 선택하도록 합니다. 필요에 따라 코어 hello 인스턴스 toothousands 확장할 수 있으며 더 적은 리소스가 필요한 경우 다음 확장 수 있습니다.

> [!NOTE]
> Azure hello 활용 [H 시리즈 hello와 같은 계산 집약적인 인스턴스](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooimprove hello HPC 워크 로드의 성능 및 확장성. 또한 이러한 인스턴스는 대기 시간이 짧고 처리량이 많은 응용 프로그램 네트워크를 필요로 하는 병렬 MPI 응용 프로그램을 지원합니다. 사용할 수는 또한 [N 시리즈](../virtual-machines/windows/sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) NVIDIA Gpu tooexpand hello Azure의 컴퓨팅 요구 및 시각화 시나리오 범위를 가진 Vm입니다.  
> 
> 

| 부여 | 설명 |
| --- | --- |
| **[가상 컴퓨터](https://azure.microsoft.com/documentation/services/virtual-machines/)**<br/><br/> |• Microsoft Hyper-V 기술을 사용하여 서비스(IaaS)로서 계산 인프라를 제공<br/><br/>• Tooflexibly 프로 비전을 사용 하 고 hello에서 표준 Windows Server 또는 Linux 이미지에서 영구적 클라우드 컴퓨터를 관리할 [Azure 마켓플레이스](https://azure.microsoft.com/marketplace/), 또는 제공한 이미지 및 데이터 디스크<br/><br/>• 배포 하 고으로 관리할 수 [VM 크기 집합이](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/) toobuild 대규모 동일한 가상 컴퓨터에서 사용 하 여 서비스 자동 크기 조정 tooincrease 또는 감소 용량 자동으로<br/><br/>• 실행 온-프레미스 계산 클러스터 도구 및 hello 클라우드에서 전적으로 응용 프로그램<br/><br/> |
| **[클라우드 서비스](https://azure.microsoft.com/documentation/services/cloud-services/)**<br/><br/> |• Windows Server를 실행 중인 가상 컴퓨터에 있으며 Azure에서 완전히 관리되는 작업자 역할 인스턴스에서 큰 계산 응용 프로그램을 실행할 수 있음<br/><br/>• 관리 오버헤드가 적고, 확장 가능하고 안정적이며, PaaS(Platform as a Service) 모델로 실행되는 애플리케이션 지원<br/><br/>추가 도구 또는 온-프레미스 HPC 클러스터 솔루션과 개발 toointegrate • 필요할 수 있습니다. |
| **[배치](https://azure.microsoft.com/documentation/services/batch/)**<br/><br/> |• 완전히 관리되는 서비스에서 대규모 병렬 및 배치 워크로드를 실행<br/><br/>• 가상 컴퓨터의 관리되는 풀을 작업 예약하고 자동으로 크기를 조정하는 기능 제공<br/><br/>• 개발자가 있도록 toobuild 및 실행 응용 프로그램 서비스 또는 클라우드 사용 기존 응용 프로그램<br/> |

### <a name="storage-services"></a>저장소 서비스
일반적으로 큰 계산 솔루션은 입력된 데이터 집합에 대해 작동하며 그 결과 대한 데이터를 생성합니다. 큰 계산 솔루션에서 사용 되는 hello Azure 저장소 서비스에 포함 됩니다.

* [Blob, 테이블 및 큐 저장소](https://azure.microsoft.com/documentation/services/storage/) - 대량의 구조화되지 않은 데이터, NoSQL 데이터 및 워크플로와 통신에 대한 메시지를 각각 관리합니다. 예를 들어 기술 하는 큰 데이터 집합 또는 입력된 이미지 hello에 대 한 blob 저장소를 사용할 수 있습니다 또는 미디어 파일을 응용 프로그램 프로세스입니다. 솔루션에서 비동기 통신을 위한 큐를 사용할 수 있습니다. 참조 [Azure 저장소 소개 tooMicrosoft](../storage/common/storage-introduction.md)합니다.
* [Azure 파일 저장소](https://azure.microsoft.com/services/storage/files/) -공용 파일 공유 및 사용 하 여 Azure에 데이터 hello 일부 HPC 클러스터 솔루션에 필요한 표준 SMB 프로토콜입니다.
* [데이터 레이크 저장소](https://azure.microsoft.com/services/data-lake-store/) -실시간으로 일괄 처리에 대 한 유용한 hello 클라우드 및 대화형 분석에 대 한 대규모 Apache Hadoop 분산 파일 시스템을 제공 합니다.

### <a name="data-and-analysis-services"></a>데이터 및 분석 서비스
일부 큰 계산 시나리오는 대규모 데이터 흐름이 포함하0거나 추가 처리 또는 분석에 필요한 데이터를 생성합니다. Azure는 다음과 같은 몇 가지 데이터 및 분석 서비스를 제공합니다.

* [데이터 팩터리](https://azure.microsoft.com/documentation/services/data-factory/) - 온-프레미스, 클라우드 기반 및 인터넷 데이터 저장소에서 데이터를 결합, 집계 및 변환하는 데이터 기반 워크플로(파이프라인)를 구축합니다.
* [SQL 데이터베이스](https://azure.microsoft.com/documentation/services/sql-database/) -hello에서 관리 되는 서비스는 Microsoft SQL Server 관계형 데이터베이스 관리 시스템의 주요 기능을 제공 합니다.
* [HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/) -를 배포 하 고 프로 비전 hello에서 Windows Server 또는 Linux 기반 Apache Hadoop 클러스터 toomanage 클라우드, 분석 및 빅 데이터를 보고 합니다.
* [기계 학습](https://azure.microsoft.com/documentation/services/machine-learning/) - 사용자가 완전히 관리되는 서비스의 예측 분석 솔루션을 만들고, 테스트, 운영, 관리할 수 있도록 돕습니다.

### <a name="additional-services"></a>서비스
큰 계산 솔루션에서 다른 Azure 서비스 tooconnect tooresources 온-프레미스를 할 수 또는 다른 환경에서 합니다. 예를 들면 다음과 같습니다.

* [가상 네트워크](https://azure.microsoft.com/documentation/services/virtual-network/) -Azure tooconnect Azure 리소스 tooeach 다른 또는 tooyour 온-프레미스 데이터 센터에서 논리적으로 분리 된 섹션을 만듭니다. 크로스-프레미스 가상 네트워크를 통해 Big Compute 응용 프로그램은 온-프레미스 데이터, Active Directory 서비스 및 라이선스 서버에 액세스할 수 있습니다.
* [ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/) - 온-프레미스 또는 공동 배치 환경에 있는 Microsoft 데이터 센터와 인프라 간에 개인 연결을 만들 수 있습니다. ExpressRoute는 hello 인터넷을 통해 보다 높은 수준의 보안, 더 많은 안정성, 빨라진 속도 및 일반 연결 보다 더 낮은 대기 시간을 제공합니다.
* [서비스 버스](https://azure.microsoft.com/documentation/services/service-bus/) -Azure에 있는 다른 클라우드 플랫폼 또는 데이터 센터에 있는지 여부를 응용 프로그램에 대 한 몇 가지 메커니즘 toocommunicate 또는 exchange 데이터를 제공 합니다.

## <a name="next-steps"></a>다음 단계
* 참조 [HPC 및 일괄 처리에 대 한 기술 리소스](big-compute-resources.md) toofind 기술 지침 toobuild 솔루션입니다.
* Cycle Computing, Rescale 및 UberCloud를 포함하여 파트너와 Azure 옵션을 살펴봅니다.
* [Towers Watson](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222), [Altair](https://azure.microsoft.com/blog/availability-of-altair-radioss-rdma-on-microsoft-azure/), [ANSYS](https://azure.microsoft.com/blog/ansys-cfd-and-microsoft-azure-perform-the-best-hpc-scalability-in-the-cloud/) 및 [d3VIEW](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088)에서 제공하는 Azure 빅 컴퓨팅 솔루션에 대해 읽습니다.
* 에 대 한 hello 최신 알림을 참조 hello [Microsoft HPC 및 일괄 처리 팀 블로그](http://blogs.technet.com/b/windowshpc/) 및 hello [Azure 블로그](https://azure.microsoft.com/blog/tag/hpc/)합니다.

<!--Image references-->
[parallel]: ./media/batch-hpc-solutions/parallel.png
[coupled]: ./media/batch-hpc-solutions/coupled.png
[iaas_cluster]: ./media/batch-hpc-solutions/iaas_cluster.png
[burst_cluster]: ./media/batch-hpc-solutions/burst_cluster.png
[batch_proc]: ./media/batch-hpc-solutions/batch_proc.png
