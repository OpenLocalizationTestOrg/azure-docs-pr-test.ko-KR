---
title: "aaaAzure 인스턴스 메타 데이터 서비스 개요 | Microsoft Docs"
description: "VM의 계산, 네트워크 및 향후 유지 관리 이벤트에 대 한 rESTful 인터페이스 tooget 정보입니다."
services: virtual-machines-windows, virtual-machines-linux,virtual-machines-scale-sets, cloud-services
documentationcenter: virtual-machines
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 03/27/2017
ms.author: harijay
ms.openlocfilehash: e87cdf28f80b9ef8cc566b637549c48846862f0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-instance-metadata-service"></a>Azure Instance Metadata Service 


hello Azure 인스턴스 메타 데이터 서비스는 가상 컴퓨터를 구성 하 고 사용 하는 toomanage 수 있는 가상 컴퓨터 인스턴스를 실행 하는 방법에 대 한 정보를 제공 합니다.
여기에는 SKU, 네트워크 구성, 예정된 유지 관리 이벤트 등의 정보가 포함됩니다. 사용 가능한 정보 유형에 대한 자세한 내용은 [메타데이터 범주](#instance-metadata-data-categories)를 참조하세요.

Azure의 인스턴스 메타 데이터 서비스는 hello를 통해 액세스할 수 있는 tooall IaaS Vm 만든 REST 끝점 [Azure 리소스 관리자](https://docs.microsoft.com/rest/api/resources/)합니다. hello 끝점은 잘 알려진 라우팅할 수 없는 IP 주소에서 사용할 수 (`169.254.169.254`) hello VM 내 에서만 액세스할 수 있습니다.

### <a name="important-information"></a>중요 정보

이 서비스는 글로벌 Azure 지역에서 **일반 공급**됩니다. 정부, 중국 및 독일어 Azure 클라우드에 대한 공개 미리 보기로 제공됩니다. 정기적으로 가상 컴퓨터 인스턴스에 대 한 업데이트 tooexpose 새 정보를 받습니다. 이 페이지에는 최신 hello 반영 [데이터 범주](#instance-metadata-data-categories) 사용할 수 있습니다.

## <a name="service-availability"></a>서비스 가용성
hello 서비스를 사용할 수 있는 모든 전역 Azure 지역에서 사용할 수 있습니다. hello 서비스는 hello 정부, 중국, 또는 독일 지역에서 공개 미리 보기입니다.

영역                                        | 가용성
-----------------------------------------------|-----------------------------------------------
[일반 공급되는 모든 글로벌 Azure 지역](https://azure.microsoft.com/en-us/regions/)     | 일반 공급 
[Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)              | 미리 보기 
[Azure 중국](https://www.azure.cn/)                                                           | 미리 보기
[Azure 독일](https://azure.microsoft.com/en-us/overview/clouds/germany/)                    | 미리 보기

이 테이블의 다른 Azure 클라우드의 hello 서비스 사용할 수 있을 때 업데이트 됩니다.

tootry 아웃 hello 인스턴스 메타 데이터 서비스에서 VM을 만들 [Azure 리소스 관리자](https://docs.microsoft.com/rest/api/resources/) 또는 hello [Azure 포털](http://portal.azure.com) 영역 및 아래에 따라 hello 예제 위에 hello에 있습니다.

## <a name="usage"></a>사용

### <a name="versioning"></a>버전 관리
hello 인스턴스 메타 데이터 서비스 버전 관리입니다. 버전은 필수 이며 hello 현재 버전은 `2017-04-02`합니다.

> [!NOTE] 
> 이전 버전으로 hello api 버전 {최신 버전을 (를) 지원 되는 예약 된 이벤트의 미리 보기. 이 형식은 더 이상 지원 하며 hello 나중에 지원 되지 않습니다.

새로운 버전이 추가되더라도 스크립트가 특정 데이터 형식에 종속성이 있는 경우 이전 버전에 여전히 액세스할 수 있습니다. 그러나 해당 hello 현재 미리 보기 version(2017-03-01) 하지 못할 hello 서비스를 일반적으로 사용할 수 있는 note 합니다.

### <a name="using-headers"></a>헤더 사용
Hello 헤더를 제공 해야 hello 인스턴스 메타 데이터 서비스를 쿼리할 때 `Metadata: true` tooensure hello 요청이 실수로 리디렉션된 되지 않습니다.

### <a name="retrieving-metadata"></a>메타데이터 검색

인스턴스 메타데이터는 [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/)를 사용하여 생성/관리되는 VM을 실행하는 데 사용할 수 있습니다. 요청을 수행 하는 hello를 사용 하 여 가상 컴퓨터 인스턴스에 대 한 모든 데이터 범주에 액세스 합니다.

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> 모든 인스턴스 메타데이터 쿼리는 대/소문자를 구분합니다.

### <a name="data-output"></a>데이터 출력
기본적으로 인스턴스 메타 데이터 서비스 hello JSON 형식의 데이터를 반환 (`Content-Type: application/json`). 그러나 다른 API는 요청된 경우 다른 형식으로 데이터를 반환할 수 있습니다.
hello 다음 표는에 대 한 참조의 다른 데이터 형식의 Api 지원할 수 있습니다.

API | 기본 데이터 형식 | 다른 형식
--------|---------------------|--------------
/instance | json : | 텍스트
/scheduledevents | json : | 없음

tooaccess 기본이 아닌 응답 형식으로 hello 요청 쿼리 문자열 매개 변수로 hello 요청 된 형식을 지정 합니다. 예:

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a>보안
hello 인스턴스 메타 데이터 서비스 끝점을 라우팅할 수 없는 IP 주소를 가상 컴퓨터 인스턴스를 실행 하는 hello 내 에서만 액세스할 수 있습니다. 또한 모든 요청을 `X-Forwarded-For` 헤더 hello 서비스에 의해 거부 되었습니다.
또한 요청 toocontain 필요는 `Metadata: true` hello 실제 요청 헤더 tooensure 의도 대로 되었으며 직접 의도 하지 않은 리디렉션의 일부분이 아닙니다. 

### <a name="error"></a>오류
데이터 요소를 찾을 수 없음 또는 잘못 된 요청 있는 경우 hello 인스턴스 메타 데이터 서비스는 표준 HTTP 오류를 반환 합니다. 예:

HTTP 상태 코드 | 이유
----------------|-------
200 정상 |
400 잘못된 요청 | 누락된 `Metadata: true` 헤더
404 찾을 수 없음 | hello 요청 된 요소와 존재 
405 메서드를 사용할 수 없음 | `GET` 및 `POST` 요청만 지원됨
429 요청이 너무 많음 | hello API에는 현재 5 queries / sec의 최대 지원
500 서비스 오류     | 잠시 후 다시 시도하세요.

### <a name="examples"></a>예

> [!NOTE] 
> 모든 API 응답은 JSON 문자열입니다. 다음 예제 응답은 모두 가독성을 높이기 위해 적절히 인쇄되었습니다.

#### <a name="retrieving-network-information"></a>네트워크 정보 검색

**요청**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

**응답**

> [!NOTE] 
> hello 응답은 JSON 문자열입니다. 다음 예제 응답 hello 가독성을 높이기 위해 인쇄 된입니다.

```
{
  "interface": [
    {
      "ipv4": {
        "ipAddress": [
          {
            "privateIpAddress": "10.1.0.4",
            "publicIpAddress": "X.X.X.X"
          }
        ],
        "subnet": [
          {
            "address": "10.1.0.0",
            "prefix": "24"
          }
        ]
      },
      "ipv6": {
        "ipAddress": []
      },
      "macAddress": "000D3AF806EC"
    }
  ]
}

```

#### <a name="retrieving-public-ip-address"></a>공용 IP 주소 검색

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a>인스턴스에 대한 모든 메타데이터 검색

**요청**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

**응답**

> [!NOTE] 
> hello 응답은 JSON 문자열입니다. 다음 예제 응답 hello 가독성을 높이기 위해 인쇄 된입니다.

```
{
  "compute": {
    "location": "westcentralus",
    "name": "IMDSSample",
    "offer": "UbuntuServer",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "Canonical",
    "sku": "16.04.0-LTS",
    "version": "16.04.201610200",
    "vmId": "5d33a910-a7a0-4443-9f01-6a807801b29b",
    "vmSize": "Standard_A1"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.1.0.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.1.0.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": []
        },
        "macAddress": "000D3AF806EC"
      }
    ]
  }
}
```

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a>Windows 가상 컴퓨터에서 메타데이터 검색

**요청**

Hello PowerShell 유틸리티를 통해 Windows에서 인스턴스 메타 데이터를 검색할 수 있는 `curl`: 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

또는 hello 통해 `Invoke-RestMethod` cmdlet:
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

**응답**

> [!NOTE] 
> hello 응답은 JSON 문자열입니다. 다음 예제 응답 hello 가독성을 높이기 위해 인쇄 된입니다.

```
{
  "compute": {
    "location": "westus",
    "name": "SQLTest",
    "offer": "SQL2016SP1-WS2016",
    "osType": "Windows",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "MicrosoftSQLServer",
    "sku": "Enterprise",
    "version": "13.0.400110",
    "vmId": "453945c8-3923-4366-b2d3-ea4c80e9b70e",
    "vmSize": "Standard_DS2"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.0.1.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.0.1.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": [
            
          ]
        },
        "macAddress": "002248020E1E"
      }
    ]
  }
}
```

## <a name="instance-metadata-data-categories"></a>인스턴스 메타데이터 데이터 범주
다음 데이터 범주 hello hello 인스턴스 메타 데이터 서비스를 통해 사용할 수 있습니다.

Data | 설명
-----|------------
location | Azure 지역 hello VM에서 실행 되
name | Hello VM의 이름 
offer | Hello VM 이미지에 대 한 정보를 제공 합니다. 이 값은 Azure 이미지 갤러리에서 배포된 이미지에 대해서만 표시됩니다.
publisher | Hello VM 이미지의 게시자
sku | Hello VM 이미지에 대 한 특정 SKU  
버전 | Hello VM 이미지의 버전 
osType | Linux 또는or Windows 
platformUpdateDomain |  [업데이트 도메인](virtual-machines-windows-manage-availability.md) hello VM에서 실행 되 고
platformFaultDomain | [오류 도메인](virtual-machines-windows-manage-availability.md) hello VM에서 실행 되 고
vmId | [고유 식별자](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) hello VM에 대 한
vmSize | [VM 크기](virtual-machines-windows-sizes.md)
ipv4/privateIpAddress | Hello VM의 로컬 IPv4 주소 
ipv4/publicIpAddress | Hello VM의 공용 IPv4 주소
subnet/address | Hello VM의 서브넷 주소
subnet/prefix | 서브넷 접두사, 예:24
ipv6/ipaddress | Hello VM의 로컬 IPv6 주소
macAddress | VM MAC 주소 
scheduledevents | 현재 공개 미리 보기 [scheduledevents](virtual-machines-scheduled-events.md) 참조

## <a name="example-scenarios-for-usage"></a>사용법을 위한 예제 시나리오  

### <a name="tracking-vm-running-on-azure"></a>Azure에서 실행 중인 VM 추적

서비스 공급자로 서 소프트웨어를 실행 중인 Vm tootrack hello 수 필요할 수 있습니다 또는 hello VM이 tootrack 고유 해야 하는 에이전트가 있습니다. VM 사용 하 여 hello에 대 한 toobe 수 tooget 고유 ID `vmId` 인스턴스 메타 데이터 서비스에서 필드입니다.

**요청**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

**응답**

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a>장애/업데이트 도메인 기반 컨테이너, 데이터 파티션 배치 

특정 시나리오의 경우 다양한 데이터 복제본 배치가 매우 중요합니다. 예를 들어 [HDFS 복제본 배치](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) 또는 통해 컨테이너 위치는 [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) tooknow hello 필요할 수 있습니다 `platformFaultDomain` 및 `platformUpdateDomain` hello VM에서 실행 되 고 있습니다.
Hello 인스턴스 메타 데이터 서비스를 통해 직접이 데이터를 쿼리할 수 있습니다.

**요청**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

**응답**

```
0
```

### <a name="getting-more-information-about-hello-vm-during-support-case"></a>지원 사례 중 VM hello에 대 한 추가 정보 얻기 

서비스 공급자로 서 발생할 수 있습니다 지원 통화 넣을 tooknow hello VM에 대 한 자세한 정보. Hello 계산 메타 데이터 요청 hello 고객 tooshare Azure에서 VM의 hello 종류에 대 한 지원 전문가 tooknow hello에 대 한 기본 정보를 제공할 수 있습니다. 

**요청**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

**응답**

> [!NOTE] 
> hello 응답은 JSON 문자열입니다. 다음 예제 응답 hello 가독성을 높이기 위해 인쇄 된입니다.

```
{
  "compute": {
    "location": "CentralUS",
    "name": "IMDSCanary",
    "offer": "RHEL",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "RedHat",
    "sku": "7.2",
    "version": "7.2.20161026",
    "vmId": "5c08b38e-4d57-4c23-ac45-aca61037f084",
    "vmSize": "Standard_DS2"
  }
}
```

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-hello-vm"></a>Hello VM 내 서로 다른 언어를 사용 하 여 메타 데이터 서비스 호출의 예 

언어 | 예제 
---------|----------------
Ruby     | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb
Go Lan   | https://github.com/Microsoft/azureimds/blob/master/imdssample.go            
python   | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py
C++      | https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp
C#       | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs
JavaScript | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js
PowerShell | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1
Bash       | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh
    

## <a name="faq"></a>FAQ
1. Hello 오류가 발생 `400 Bad Request, Required metadata header not specified`합니다. 무슨 의미인가요?
   * hello 헤더를 요구 하는 hello 인스턴스 메타 데이터 서비스 `Metadata: true` toobe hello 요청에 전달 합니다. Hello REST 호출에이 헤더를 전달 하면 액세스 toohello 인스턴스 메타 데이터 서비스입니다. 
2. VM에 대한 계산 정보를 구할 수 없는 이유가 무엇인가요?
   * 현재 hello 인스턴스 메타 데이터 서비스는 Azure 리소스 관리자와 함께 만든 인스턴스에 지원 합니다. Hello 이후,에서는 클라우드 서비스 Vm에 대 한 지원을 추가 될 수 있습니다.
3. 잠시 전에 Azure Resource Manager를 통해 내 가상 컴퓨터를 만들었습니다. 계산 메타데이터 정보가 왜 표시되지 않나요?
   * 2016 년 9 월 이후 만들어진 모든 Vm을 추가 하는 [태그](../azure-resource-manager/resource-group-using-tags.md) toostart 보는 계산 메타 데이터입니다. 이전 Vm (2016 년 9 월 이전에 만든)을 위한 추가/제거 확장 또는 데이터 디스크 toohello VM toorefresh 메타 데이터가 없습니다.
4. 이유는 무엇입니까 hello 오류 `500 Internal Server Error`?
   * 지수 백오프 시스템을 기반으로 요청을 다시 시도하세요. Hello 문제가 계속 되 면 Azure 지원을 담당자에 게 문의 하십시오.
5. 추가 질문/의견은 어디에 공유하나요?
   * 의견은 http://feedback.azure.com에서 알려주세요.
7. 가상 컴퓨터 확장 집합 인스턴스에 작동하나요?
   * 예, 메타데이터 서비스는 확장 집합 인스턴스에 사용할 수 있습니다. 
6. Hello 서비스에 대 한 지원 받기
   * hello 서비스에 대 한 tooget 지원 hello 없는 수 tooget 메타 데이터 응답 긴 다시 시도한 후 VM에 대 한 Azure 포털에서 지원 문제를 만들려면 

   ![인스턴스 메타데이터 지원](./media/virtual-machines-instancemetadataservice-overview/InstanceMetadata-support.png)
    
## <a name="next-steps"></a>다음 단계

- Hello에 대 한 자세한 [scheduledevents](virtual-machines-scheduled-events.md) API **에서 공개 미리 보기** hello 인스턴스 메타 데이터 서비스에서 제공 합니다.
