
hello Ls 시리즈 Cassandra, MongoDB, Cloudera를 포함 하는 NoSQL 데이터베이스와 같은 짧은 대기 시간 임시 저장소가 필요 하 고 Redis는 작업에 대해 최적화 되어 있습니다. hello Ls 시리즈 Vcpu too32 hello를 사용 하 여 최대 제공 [Intel® Xeon® E5 v3 제품군 프로세서가](http://www.intel.com/content/www/us/en/processors/xeon/xeon-e5-solutions.html)합니다. hello Ls 시리즈 gets G/GS 시리즈 hello 처럼 동일한 CPU 성능 hello 및 vCPU 당 메모리의 8 GiB와 함께 제공 합니다.  

## <a name="ls-series"></a>Ls 시리즈

ACU: 180-240
 
| 크기          | vCPU | 메모리: GiB | 임시 저장소(SSD) GiB | 최대 데이터 디스크 수 | 최대 캐시된 임시 저장소 처리량: IOPS/MBps(GiB 단위의 캐시 크기) | 최대 캐시되지 않은 디스크 처리량: IOPS/MBps | 최대 NIC 수 / 예상 네트워크 성능(Mbps) | 
|---------------|-----------|-------------|--------------------------|----------------|-------------------------------------------------------------|-------------------------------------------|------------------------------| 
| Standard_L4s  | 4    | 32   | 678   | 8              | 해당 없음/해당 없음(0)          | 5,000/125                               | 2 / 4000       | 
| Standard_L8s  | 8    | 64   | 1,388 | 16             | 해당 없음/해당 없음(0)          | 10,000/250                              | 4 / 8000  | 
| Standard_L16s | 16   | 128  | 2,807 | 32             | 해당 없음/해당 없음(0)          | 20,000/500                              | 8 / 6000 - 16000 &#8224; | 
| Standard_L32s* | 32 | 256  | 5,630 | 64             | 해당 없음/해당 없음(0)          | 40,000/1,000                            | 8 / 20000 | 
 

hello 최대 디스크 처리량 Ls 시리즈 Vm에 있을 수 있는 연결 된 디스크 hello 수, 크기 및 모든 스트라이프로 제한 합니다. 자세한 내용은 [Premium Storage: Azure 가상 컴퓨터 작업을 위한 고성능 저장소](../articles/storage/common/storage-premium-storage.md)를 참조하세요. 

* 인스턴스는 격리 된 toohardware 전용된 tooa 단일 고객입니다.

