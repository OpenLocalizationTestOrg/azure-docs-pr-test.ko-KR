<!-- A-series - compute-intensive instances, H-series -->

hello A8 A11 및 H 시리즈 크기 라고 *계산 집약적인 인스턴스*합니다. 이러한 크기를 실행 하는 hello 하드웨어를 디자인 하 고 계산 집약적인에 맞게 최적화 및 네트워크 집약적 응용 프로그램, 고성능 컴퓨팅 HPC ()를 포함 하 여 클러스터 응용 프로그램, 모델링 및 시뮬레이션 합니다. hello A8 A11 시리즈 Intel Xeon E5-2670 @ 2.6 g h Z를 사용 하 고 hello H 시리즈 3.2 g h z @ Intel Xeon E5-2667 v3를 사용 합니다. 

Azure H 시리즈 가상 컴퓨터는 hello 다음 세대 고성능 컴퓨팅 Vm 분자 모델링 및 계산 유체 역학와 같은 고급 계산 요구를 목표로 합니다. 이러한 8에서 16 vCPU Vm DDR4 메모리를 갖춘 Intel Haswell E5 2667 V3 hello 프로세서 기술에 빌드되고 SSD 기반 임시 저장 합니다. 

또한 toohello 상당한 CPU 전원, hello H 시리즈는 FDR InfiniBand 및 몇 가지 메모리 구성 toosupport 메모리 집약적 계산 요구 사항을 사용 하 여 대기 시간이 짧은 RDMA 네트워킹에 대 한 다양 한 옵션을 제공 합니다.



## <a name="h-series"></a>H 시리즈

ACU: 290-300

| 크기 | vCPU | 메모리: GiB | 임시 저장소(SSD) GiB | 최대 데이터 디스크 수 | 최대 디스크 처리량: IOPS | 최대 NIC 수 |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_H8 |8 |56 |1000 |16 |16 x 500 |2  |
| Standard_H16 |16 |112 |2000 |32 |32 x 500 |4 |
| Standard_H8m |8 |112 |1000 |16 |16 x 500 |2  |
| Standard_H16m |16 |224 |2000 |32 |32 x 500 |4  |
| Standard_H16r* |16 |112 |2000 |32 |32 x 500 |4  |
| Standard_H16mr* |16 |224 |2000 |32 |32 x 500 |4 |

*MPI 응용 프로그램의 경우 초단기 대기 시간 및 고 대역폭을 제공하는 FDR InfiniBand 네트워크를 통해 전용 RDMA 백 엔드 네트워크를 사용할 수 있습니다.

<br>



## <a name="a-series---compute-intensive-instances"></a>A-시리즈 - 계산 집약적 인스턴스

ACU: 225

| 크기 | vCPU | 메모리: GiB | 임시 저장소(HDD) GiB | 최대 데이터 디스크 수 | 최대 데이터 디스크 처리량: IOPS | 최대 NIC 수|
| --- | --- | --- | --- | --- | --- | --- |
| Standard_A8* |8 |56 |382 |16 |16x500 |2 |
| Standard_A9* |16 |112 |382 |16 |16x500 |4 |
| Standard_A10 |8 |56 |382 |16 |16x500 |2  |
| Standard_A11 |16 |112 |382 |16 |16x500 |4 |

*MPI 응용 프로그램의 경우 초단기 대기 시간 및 고 대역폭을 제공하는 FDR InfiniBand 네트워크를 통해 전용 RDMA 백 엔드 네트워크를 사용할 수 있습니다.

<br>



