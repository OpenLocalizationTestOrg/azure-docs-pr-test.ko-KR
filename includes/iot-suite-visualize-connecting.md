## <a name="view-device-telemetry"></a>장치 원격 분석 보기

솔루션의 **장치** 페이지에서 장치에서 보낸 원격 분석을 볼 수 있습니다.

1. **장치** 페이지의 장치 목록에서 프로비전한 장치를 선택합니다. 패널은 장치 원격 분석의 그림을 포함한 장치에 대한 정보를 표시합니다.

    ![장치 세부 정보 보기](media/iot-suite-visualize-connecting/devicesdetail.png)

1. **압력**을 선택하여 원격 분석 표시를 변경합니다.

    ![압력 원격 분석 보기](media/iot-suite-visualize-connecting/devicespressure.png)

1. 장치에 대한 진단 정보를 보려면 **진단** 아래로 스크롤합니다.

    ![장치 진단 보기](media/iot-suite-visualize-connecting/devicesdiagnostics.png)

## <a name="act-on-your-device"></a>장치에서 작동

장치에서 메서드를 호출하려면 원격 모니터링 솔루션의 **장치** 페이지를 사용합니다. 예를 들어, 원격 모니터링 솔루션에서 **냉각기** 장치는 **Reboot** 메서드를 구현합니다.

1. **장치**를 선택하여 솔루션의 **장치** 페이지로 이동합니다.

1. **장치** 페이지의 장치 목록에서 프로비전한 장치를 선택합니다.

    ![물리적 장치 선택](media/iot-suite-visualize-connecting/devicesselect.png)

1. 장치에서 호출할 수 있는 메서드의 목록을 표시하려면 **일정**을 선택합니다. 메서드를 여러 장치에서 실행되도록 예약하기 위해 목록에서 여러 장치를 선택할 수 있습니다. **일정** 패널은 선택한 모든 장치에 공통적인 메서드의 유형을 표시합니다.

1. **Reboot**를 선택하고, 작업 이름을 **RebootPhysicalChiller**로 설정하고, **적용**을 선택합니다.

    ![다시 부팅 예약](media/iot-suite-visualize-connecting/deviceschedule.png)

1. 장치가 메서드를 처리하는 경우 장치 코드를 실행하는 콘솔에 메시지가 표시됩니다.

> [!NOTE]
> 솔루션에서 작업의 상태를 추적하려면 **보기**를 선택합니다.

## <a name="next-steps"></a>다음 단계

[미리 구성된 원격 모니터링 솔루션 사용자 지정](../articles/iot-suite/iot-suite-remote-monitoring-customize.md) 문서는 미리 구성된 솔루션을 사용자 지정하는 몇 가지 방법을 설명합니다.