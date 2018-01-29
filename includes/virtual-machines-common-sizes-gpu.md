
GPU 최적화 VM 크기는 단일 또는 여러 NVIDIA GPU에서 사용 가능한 특수한 가상 머신입니다. 이러한 크기는 계산 집약적이며 그래픽 집약적인 시각화 워크로드용으로 설계되었습니다. 이 문서에서는 이 그룹화에서 각 크기에 대한 저장소 처리량 및 네트워크 대역폭뿐만 아니라 GPU, vCPU, 데이터 디스크 및 NIC의 수 및 형식에 대한 정보를 제공합니다. 

* **NC, NCv2 및 ND** 크기는 계산 집약적 및 네트워크 집약적 응용 프로그램, CUDA를 비롯한 알고리즘, OpenCL 기반 응용 프로그램 및 시뮬레이션, AI, 심층 학습에 좀 더 최적화되어 있습니다. 
* **NV** 크기는 OpenGL 및 DirectX와 같은 프레임 워크를 활용하는 원격 시각화, 스트리밍, 게임, 인코딩 및 VDI 시나리오에 맞게 최적화되고 설계되었습니다.  


## <a name="nc-instances"></a>NC 인스턴스

NC 인스턴스는 [NVIDIA Tesla K80](http://images.nvidia.com/content/pdf/kepler/Tesla-K80-BoardSpec-07317-001-v05.pdf) 카드에 의해 구동됩니다. 사용자는 에너지 탐색 응용 프로그램, 충돌 시뮬레이션, 광선 추적 렌더링, 심층 학습 등에 CUDA를 활용하여 데이터를 더 빠르게 처리할 수 있습니다. NC24r 구성은, 긴밀하게 결합된 병렬 컴퓨팅 워크로드용으로 최적화된 대기 시간이 짧고 처리량이 높은 네트워크 인터페이스를 제공합니다.


| 크기 | vCPU | 메모리: GiB | 임시 저장소(SSD) GiB | GPU | 최대 데이터 디스크 수 |
| --- | --- | --- | --- | --- | --- |
| Standard_NC6 |6 |56 | 380 | 1 | 24 |
| Standard_NC12 |12 |112 | 680 | 2 | 48 |
| Standard_NC24 |24 |224 | 1,440 | 4 | 64 |
| Standard_NC24r* |24 |224 | 1,440 | 4 | 64 |

1 GPU = K80 카드의 절반.

*RDMA 지원

## <a name="ncv2-instances"></a>NCv2 인스턴스

NCv2 인스턴스는 [NVIDIA Tesla P100](http://images.nvidia.com/content/tesla/pdf/nvidia-tesla-p100-datasheet.pdf) GPU에 의해 작동되는 차세대 NC 시리즈 컴퓨터입니다. 이러한 GPU는 현재 NC 시리즈보다 2배 이상 우수한 계산 성능을 제공할 수 있습니다. 고객은 저수지 모델링, DNA 배열, 단백질 분석, 몬테카를로 시뮬레이션 등 기존 HPC 워크로드에 이러한 업데이트된 GPU를 활용할 수 있습니다. NCv2 시리즈는 NC 시리즈처럼 긴밀하게 결합된 병렬 컴퓨팅 워크로드용으로 최적화된 대기 시간이 짧고 처리량이 높은 네트워크 인터페이스를 포함한 구성을 제공합니다.

> [!IMPORTANT]
> 이 크기 제품군의 경우 구독의 vCPU(코어) 할당량은 각 지역에서 처음에 0으로 설정됩니다. [사용 가능한 지역](https://azure.microsoft.com/regions/services/)에서 이 제품군에 대한 [vCPU 할당량 증가를 요청](../articles/azure-supportability/resource-manager-core-quotas-request.md)합니다.
>

| 크기 | vCPU | 메모리: GiB | 임시 저장소(SSD) GiB | GPU | 최대 데이터 디스크 수 |
| --- | --- | --- | --- | --- | --- |
| Standard_NC6_v2 |6 |112 | 336 | 1 | 12 |
| Standard_NC12_v2 |12 |224 | 672 | 2 | 24 |
| Standard_NC24_v2 |24 |448 | 1344 | 4 | 32 |
| Standard_NC24r_v2* |24 |1448 | 1344 | 4 | 32 |

한 개의 GPU = 한 개의 P100 카드

*RDMA 지원

## <a name="nd-instances"></a>ND 인스턴스

ND 시리즈 가상 머신은 AI 및 심층 학습 워크로드용으로 설계된 GPU 제품군에 새로 추가됩니다. 이 가상 머신은 교육 및 유추에 우수한 성능을 제공합니다. ND 인스턴스는 [NVIDIA Tesla P40](http://images.nvidia.com/content/pdf/tesla/184427-Tesla-P40-Datasheet-NV-Final-Letter-Web.pdf) GPU에 의해 구동됩니다. 이 인스턴스는 단정밀도 부동 소수점 작업, Microsoft Cognitive Toolkit, TensorFlow, Caffe 및 기타 프레임워크를 활용하는 AI 워크로드에 우수한 성능을 제공합니다. ND 시리즈는 훨씬 큰 GPU 메모리 크기(24GB)도 제공하므로 더 큰 규모의 신경망 모델에도 적합합니다. NC 시리즈와 마찬가지로 ND 시리즈는 RDMA를 통한 대기 시간이 낮고 처리량이 높은 보조 네트워크 및 InfiniBand 연결과 함께 구성할 수 있으므로 여러 GPU를 사용한 대규모 교육 작업을 실행할 수 있습니다.

> [!IMPORTANT]
> 이 크기 제품군의 경우 구독의 지역당 vCPU(코어) 할당량은 처음에 0으로 설정됩니다. [사용 가능한 지역](https://azure.microsoft.com/regions/services/)에서 이 제품군에 대한 [vCPU 할당량 증가를 요청](../articles/azure-supportability/resource-manager-core-quotas-request.md)합니다.
>

| 크기 | vCPU | 메모리: GiB | 임시 저장소(SSD) GiB | GPU | 최대 데이터 디스크 수 |
| --- | --- | --- | --- | --- | --- |
| Standard_ND6 |6 |112 | 336 | 1 | 12 |
| Standard_ND12 |12 |224 | 672 | 2 | 24 |
| Standard_ND24 |24 |448 | 1344 | 4 | 32 |
| Standard_ND24r* |24 |1448 | 1344 | 4 | 32 |

한 개의 GPU = 한 개의 P40 카드

*RDMA 지원

## <a name="nv-instances"></a>NV 인스턴스



NV 인스턴스는 고객이 해당 데이터 또는 시뮬레이션을 시각화할 수 있는 데스크톱 가속화 응용 프로그램 및 가상 데스크톱용 [NVIDIA Tesla M60 ](http://images.nvidia.com/content/tesla/pdf/188417-Tesla-M60-DS-A4-fnl-Web.pdf) GPU 및 NVIDIA GRID에 의해 지원됩니다. 사용자는 NV 인스턴스에서 그래픽 집약적인 워크플로를 시각화하여 뛰어난 그래픽 기능을 가져오고 인코딩 및 렌더링 등의 단정밀도 작업을 추가적으로 실행할 수 있습니다. 

| 크기 | vCPU | 메모리: GiB | 임시 저장소(SSD) GiB | GPU | 최대 데이터 디스크 수 |
| --- | --- | --- | --- | --- | --- |
| Standard_NV6 |6 |56 |380 | 1 | 24 |
| Standard_NV12 |12 |112 |680 | 2 | 48 |
| Standard_NV24 |24 |224 |1,440 | 4 | 64 |

1 GPU = M60 카드 절반.


