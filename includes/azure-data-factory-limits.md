데이터 팩터리는는 다중 테 넌 트 서비스 위치 toomake 고객 구독와 다른 사용자의 작업에서 구성 설정은 있는지에 대 한 기본 제한을 따르는 hello에입니다. 다양 한 hello 제한 쉽게 여 늘릴 수 있습니다 toohello 최대 한도를 구독에 대 한 지원에 문의 합니다.

| **리소스** | **기본 제한** | **최대 제한** |
| --- | --- | --- |
| Azure 구독의 데이터 팩터리 |50 |[지원에 문의](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 데이터 팩터리 내의 파이프라인  |2500 |[지원에 문의](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 데이터 팩터리 내의 데이터 집합 |5000 |[지원에 문의](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 데이터 집합당 동시 조각 |10 |10 |
| 파이프라인 개체에 대한 개체당 바이트<sup>1</sup> |200KB |200KB |
| 데이터 집합 및 연결된 서비스 개체에 대한 개체당 바이트 <sup>1</sup> |100KB |2000KB |
| 구독 내부의 HDInsight 주문형 클러스터 코어<sup>2</sup> |60 |[지원에 문의](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 클라우드 데이터 이동 단위 <sup>3</sup> |32 |[지원에 문의](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 파이프라인 활동 실행에 대한 재시도 횟수 |1000 |MaxInt(32비트) |

<sup>1</sup>파이프라인, 데이터 집합 및 연결된 서비스 개체에서 작업의 논리적 그룹화를 나타냅니다. 이러한 개체에 대 한 제한을 tooamount 이동 하 고 hello Azure 데이터 팩터리 서비스와 함께 처리할 수 데이터와 관련 되지 않을 합니다. 데이터 팩터리 설계 된 tooscale toohandle 페타바이트 규모의 데이터입니다.

<sup>2</sup> 주문형 HDInsight 코어 hello 데이터 팩터리를 포함 하는 hello 구독에서 할당 됩니다. 결과적으로, 제한 초과 하는 hello는 hello Data Factory 주문형 HDInsight 코어 코어 제한을 적용 하 고 Azure 구독에 연결 된 hello 코어 제한 다릅니다.

<sup>3</sup> 클라우드 데이터 이동 단위(DMU)는 클라우드 간 복사 작업에 사용됩니다. 이 Data Factory에 단일 단위 hello 우위 (CPU, 메모리 및 네트워크 리소스 할당의 조합)를 나타내는 측정값입니다. 일부 시나리오의 경우 더 많은 DMU를 활용하여 더 높은 복사 처리량을 달성할 수 있습니다. 너무 참조[데이터 이동을 단위 클라우드](../articles/data-factory/data-factory-copy-activity-performance.md#cloud-data-movement-units) 세부 정보 섹션.

| **리소스** | **기본 하한값** | **최소 제한** |
| --- | --- | --- |
| 일정 간격 |15분 |15분 |
| 재시도 간의 간격 |1초 |1초 |
| 재시도 시간 제한 값 |1초 |1초 |

### <a name="web-service-call-limits"></a>웹 서비스 호출 제한
Azure Resource Manager에는 API 호출 제한이 있습니다. Hello 내 속도로 API 호출을 만들 수 있습니다 [Azure 리소스 관리자 API 제한](../articles/azure-subscription-service-limits.md#resource-group-limits)합니다.
