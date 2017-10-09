---
title: "Azure Site Recovery와 aaaReplicate VMware Vm tooAzure | Microsoft Docs"
description: "VMware Vm tooAzure에서 실행 되는 작업을 복제 하기 위한 hello 단계의 개요를 제공 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 7104f67a3635b916048dcb61bca770c89f0c77fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-vms-tooazure-with-site-recovery"></a>사이트 복구와 VMware Vm tooAzure 복제

이 문서에서는 hello 단계 필요한 tooreplicate 온-프레미스 VMware 가상 컴퓨터 tooAzure, hello를 사용 하 여 간략하게 [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.


![배포 프로세스](./media/vmware-walkthrough-overview/vmware-to-azure-process.png)

**그림 1: 배포 프로세스 요약**

## <a name="step-1-review-architecture-and-prerequisites"></a>1단계: 아키텍처 및 필수 구성 요소 검토

배포를 시작 하기 전에 hello 시나리오 아키텍처를 검토 하 고 toodeploy 필요한 모든 hello 구성 요소 이해

너무 이동[1 단계: hello 아키텍처 검토](vmware-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>2단계: 필수 구성 요소 검토

Hello 필수 구성 요소에서 각 배포 구성 요소에 대 한 있습니까 있는지 확인 합니다.

- **Azure 필수 구성 요소**: Microsoft Azure 계정, Azure 네트워크 및 저장소 계정이 필요합니다.
- **온-프레미스 Site Recovery 구성 요소**: 컴퓨터가 온-프레미스 Site Recovery 구성 요소를 실행해야 합니다.
- **온-프레미스 VMware 필수 구성 요소**: 계정을 tooset 사이트 복구는 VMware 서버 및 Vm에 액세스할 수 있도록 해야 합니다.
- **Vm 복제**: Vm Azure 요구 사항에 tooreplicate 필요 toocomply을 hello 모바일 서비스 구성 요소가 설치 되어 있습니다.

너무 이동[2 단계: 필수 구성 요소 및 제한 사항 검토](vmware-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>3단계: 용량 계획

전체 배포를 수행 하는 경우 필요한 복제 리소스 아웃 toofigure를 해야 합니다. 두 도구 사용 가능한 toohelp의이 작업을 수행 합니다. TooStep 2를 이동 합니다. 빠른 tootest hello 환경을 설정 하 고이 단계를 건너뛸 수 있습니다.

너무 이동[3 단계: 용량 계획](vmware-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>4단계: 네트워킹 계획

Toodo 일부 네트워크 tooensure 있는지 Azure Vm 연결된 toonetworks 장애 조치가 발생 한 후와 hello 수 있는 올바른 IP 주소를 계획 해야 합니다.

너무 이동[4 단계: 네트워킹 계획](vmware-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>5단계: Azure 리소스 준비

시작하기 전에 Azure 네트워크 및 저장소를 설정합니다. 이 작업은 배포하는 동안에도 수행할 수 있지만 시작하기 전에 수행하는 것이 좋습니다.

너무 이동[5 단계: Azure 준비](vmware-walkthrough-prepare-azure.md)


## <a name="step-6-prepare-vmware"></a>6단계: VMware 준비

사이트 복구를 사용 하 여 계정을 tooset이 필요 합니다.

- 액세스 VMware 가상화 서버 tooautomatically Vm을 검색 합니다.
- Vm tooinstall hello 모바일 서비스에 액세스 합니다. Tooreplicate hello 모바일 서비스 에이전트가 하기 전에 설치 되어 있어야 합니다. 원하는 각 VM에 대 한 복제를 사용할 수 있습니다.

너무 이동[6 단계: VMware 준비](vmware-walkthrough-prepare-vmware.md)

## <a name="step-7-set-up-a-vault"></a>7단계: 자격 증명 모음 설정

복구 서비스 자격 증명 모음 tooorchestrate tooset 필요 하 고 복제를 관리 합니다. 수행할 hello 자격 증명 모음을 설정할 때 지정 tooreplicate, tooreplicate 원본 위치에 있습니다.

너무 이동[7 단계: 자격 증명 모음 설정](vmware-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>8단계: 원본 및 대상 설정 구성

Hello 원본 및 복제에 사용 되는 대상을 설정 합니다. 소스 설정 될 때까지 설정 통합 설치 tooinstall hello 온-프레미스 복구 사이트 구성 요소를 실행 작업이 포함 됩니다.

너무 이동[8 단계: hello 소스 및 대상 설정](vmware-walkthrough-source-target.md)

## <a name="step-9-set-up-a-replication-policy"></a>9단계: 복제 정책 설정

설정한 정책 toospecify 복제 설정을 VMware Vm에 대 한 hello 자격 증명 모음에 있습니다.

너무 이동[9 단계: 복제 정책 설정](vmware-walkthrough-replication.md)

## <a name="step-10-install-hello-mobility-service"></a>10 단계: hello 모바일 서비스를 설치 합니다.

hello 모바일 서비스를 설치 해야 원하는 tooreplicate 각 VM에 있습니다. 밀어넣기 또는 끌어오기 설치로 hello 서비스를 몇 가지 방법으로 tooset 가지가 있습니다.

너무 이동[10 단계: hello Mobility service 설치](vmware-walkthrough-install-mobility.md)

## <a name="step-11-enable-replication"></a>11단계: 복제 활성화

Hello 모바일 서비스의 VM에서 실행 되 고 복제를 활성화할 수 있습니다. 를 사용 하도록 설정한 후 hello VM의 초기 복제가 발생합니다.

너무 이동[11 단계: 복제 사용](vmware-walkthrough-enable-replication.md)

## <a name="step-12-run-a-test-failover"></a>12단계: 테스트 장애 조치(failover) 실행

초기 복제가 완료 된 후 델타 복제 실행 되 고 정상적으로 작동 하는지 테스트 장애 조치 toomake를 실행할 수 있습니다.

너무 이동[12 단계: 테스트 장애 조치 실행](vmware-walkthrough-test-failover.md)
