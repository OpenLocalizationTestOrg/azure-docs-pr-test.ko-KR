---
title: "서비스 패브릭 보안 검사 목록 aaaAzure | Microsoft Docs"
description: "이 문서에서는 Azure Fabric 보안에 대한 검사 목록을 제공합니다."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: 10ffaea9e7e4de6d758b0a57a79e269c87bfd14d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-checklist"></a>Azure Service Fabric 보안 검사 목록
이 문서에서는 Azure Service Fabric 환경을 보호하는 데 도움이 되는 사용하기 쉬운 검사 목록을 제공합니다.

## <a name="introduction"></a>소개
Azure 서비스 패브릭은 분산된 시스템 플랫폼으로 쉽게 toopackage를 사용 하면을 배포 하 고 확장성과 안정성이 뛰어난 microservices 관리 합니다. 또한 서비스 패브릭 hello를 개발 및 클라우드 응용 프로그램 관리에서 중요 한 문제를 해결 합니다. 개발자와 관리자가 복잡한 인프라 문제를 피하고 업무 수행에 필수적인 까다로운 워크로드를 확장 가능하고 신뢰할 수 있으며 관리가 가능하도록 구현하는 데 집중할 수 있습니다.

## <a name="checklist"></a>검사 목록
다음 검사 목록 toohelp 관리 및 보안 Azure 서비스 패브릭 솔루션의 구성에 관련 된 중요 문제를 간과 아직 있는지 확인 하는 hello를 사용 합니다.


|검사 목록 범주| 설명 |
| ------------ | -------- |
|[RBAC(역할 기반 액세스 제어)](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security-roles) | <ul><li>액세스 제어 작업을 허용 hello 클러스터 관리자 toolimit 액세스 toocertain 클러스터 hello 클러스터를 보안 하는 사용자의 다른 그룹에 대 한 합니다.</li><li>관리자에 대 한 모든 권한을 toomanagement 기능 (읽기/쓰기 기능만 포함)가 있습니다. </li><li>   사용자가 기본적으로 읽기 액세스 toomanagement 기능 (예: 쿼리 기능) 및 hello 기능 tooresolve 응용 프로그램 및 서비스입니다.</li></ul>|
|[X.509 인증서 및 Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security) | <ul><li>프로덕션 워크로드를 실행하는 클러스터에 사용되는 [인증서](https://docs.microsoft.com/en-us/dotnet/framework/wcf/feature-details/working-with-certificates)는 올바르게 구성된 Windows Server 인증서 서비스를 사용하여 만들어지거나 승인된 [CA(인증 기관)](https://en.wikipedia.org/wiki/Certificate_authority)에서 획득해야 합니다.</li><li>프로덕션 환경에서 [MakeCert.exe](https://msdn.microsoft.com/library/windows/desktop/aa386968.aspx)와 같은 도구를 사용하여 만든 [임시 또는 테스트 인증서](https://docs.microsoft.com/en-us/dotnet/framework/wcf/feature-details/how-to-create-temporary-certificates-for-use-during-development)를 사용하지 마세요. </li><li>[자체 서명된 인증서](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security)를 사용할 수 있지만 프로덕션이 아닌 테스트 클러스터에 대해서만 이러한 인증서를 사용해야 합니다.</li></ul>|
|[클러스터 보안](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security) | <ul><li>hello 클러스터 보안 시나리오 노드를 보안, 노드 클라이언트 보안 포함 [역할 기반 액세스 제어 (RBAC)](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security-roles)합니다.</li></ul>|
|[클러스터 인증](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) | <ul><li>클러스터 페더레이션에 대한 [노드 간 통신](https://github.com/MicrosoftDocs/azure-docs/blob/master/articles/service-fabric/service-fabric-cluster-security.md)을 인증합니다. </li></ul>|
|[서버 인증](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) | <ul><li>Hello 인증 [관리 끝점 클러스터](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-portal) tooa 관리 클라이언트입니다.</li></ul>|
|[응용 프로그램 보안](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm)| <ul><li>응용 프로그램 구성 값의 암호화 및 암호 해독</li><li> 복제 중에 노드 간 데이터 암호화</li></ul>|
|[클러스터 인증서](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security) | <ul><li>이 인증서는 hello 노드 클러스터 간의 필요한 toosecure hello 통신입니다.</li><li>  Hello hello hello 지문 섹션에서에서 기본 인증서의 지문과 hello의 hello ThumbprintSecondary 변수에 보조으로 설정 합니다.</li></ul>|
|[ServerCertificate](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security)| <ul><li>이 인증서는 tooconnect toothis 클러스터를 읽으려고 할 때 toohello 클라이언트를 표시 됩니다. 업그레이드에 두 개의 다른 서버 인증서, 기본 및 보조 인증서를 사용할 수 있습니다.</li></ul>|
|ClientCertificateThumbprints| <ul><li>Tooinstall hello 인증 클라이언트에서 인증서의 집합입니다. </li></ul>|
|ClientCertificateCommonNames| <ul><li>CertificateCommonName hello에 대 한 hello 첫 번째 클라이언트 인증서의 hello 일반 이름을 설정 합니다. hello CertificateIssuerThumbprint이이 인증서의 발급자 hello에 대 한 hello 지문입니다. </li></ul>|
|ReverseProxyCertificate| <ul><li>이것은 사용할 수 있는 선택적 인증서는 toosecure 하려는 경우 지정 된 프로그램 [역방향 프록시](https://docs.microsoft.com/en-in/azure/service-fabric/service-fabric-reverseproxy)합니다. </li></ul>|
|키 자격 증명 모음| <ul><li>Azure에서 서비스 패브릭 클러스터에 대 한 toomanage 인증서를 사용 합니다.  </li></ul>|


## <a name="next-steps"></a>다음 단계
- [서비스 패브릭 클러스터 업그레이드 프로세스 및 사용자 기대 수준](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-upgrade)
- [Visual Studio에서 서비스 패브릭 응용 프로그램 관리](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-manage-application-in-visual-studio).
- [Service Fabric 상태 모델 소개](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-health-introduction)
