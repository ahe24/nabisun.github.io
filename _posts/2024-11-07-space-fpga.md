---
layout: post
title: 우주 방사선으로 인한 FPGA Soft Errors
date: 2024-11-07 07:51 +0900
description: 우주 방사선 영향 및 Precision Hi-rel
category: [EDA, Synthesis]
tags: [Precision, Hi-rel, FSM]
pin: false
math: true
mermaid: true
---

## :microscope: Space 환경에서 Radiation에 의한 Soft Errors

소프트 에러는 디자인 논리에서 값이 변하는 현상으로, 예를 들어 비트가 0에서 1로 또는 1에서 0으로 전환되는 경우를 말합니다. 이러한 에러는 "소프트"하다고 불리는데, 이는 영구적인 하드웨어 결함이 아닌 일시적인 현상이기 때문입니다. 이러한 에러는 소프트웨어나 중복된 하드웨어를 사용해 비트를 재설정하여 수정할 수 있습니다. 소프트 에러는 주로 아래의 세 가지 유형으로 구분됩니다.

### :ballot_box_with_check: 단일 이벤트 업셋 (Single Event Upset, SEU)

  단일 이벤트 업셋(SEU)은 저장 요소의 상태가 0에서 1로, 또는 1에서 0으로 바뀌는 현상입니다. 방사선 환경에서 자주 발생하며, 이를 완화하기 위해 많은 시간이 소요됩니다. SRAM 기반 장치에서는 SEU로 인해 FPGA 내부의 경로가 변경될 수 있으며, 이는 장치의 기능성을 효과적으로 변화시킬 수 있습니다. 그러나 SEU는 물리적인 손상을 일으키지는 않습니다.

### :ballot_box_with_check: 단일 이벤트 트랜지언트 (Single Event Transient, SET)

단일 이벤트 트랜지언트(SET)는 논리 게이트 내에서 전압이 변동하면서 일시적인 출력 변화가 발생하는 현상입니다. 이 일시적인 변화는 저장 요소에 유지될 수 있으며, 펄스의 빈도에 따라 오류가 저장될 가능성이 높아집니다. 즉, 간섭의 빈도가 높을수록 오류가 플립플롭에 기록될 가능성도 증가합니다.

### :ballot_box_with_check: 단일 이벤트 기능적 인터럽트 (Single Event Functional Interrupt, SEFI)

단일 이벤트 기능적 인터럽트(SEFI)는 장치가 예기치 않은 방식으로 동작하도록 만드는 에러입니다. 이로 인해 장치가 리셋되거나 잠길 수 있으며, 주로 제어 비트나 레지스터에서 발생합니다. SEFI는 장치의 정상적인 기능을 방해하며, 이 에러가 발생하면 시스템을 다시 껐다 켜야 정상 상태로 돌아올 수 있습니다.

## :microscope: 소프트 에러로부터의 보호

Precision Hi-Rel은 설계 과정에서 소프트 에러로부터 디자인을 보호하기 위해 합성 중에 에러 완화 회로를 자동으로 삽입하는 기능을 제공합니다. 이를 통해 얻을 수 있는 주요 장점은 다음과 같습니다.

설계자가 HDL에서 에러 완화 및 중복성을 수동으로 작성할 필요가 없어, 번거롭고 오류가 발생하기 쉬운 과정을 줄일 수 있습니다.
기존 검증 툴 흐름을 사용하여 이 방법을 쉽게 검증할 수 있습니다.
비방사선 강화 장치에서도 더 빠르고 자동화된 흐름을 통해 설계 옵션을 확장할 수 있습니다.
사용자는 복제할 부분을 선택하여 모듈별로 완화 회로를 제어할 수 있어, 설계 전체를 복제하지 않고 필요한 부분만 복제할 수 있습니다. 선택적 TMR(Triple Modular Redundancy) 적용을 통해 공간 절약이 가능합니다.
합성 중에 완화 회로를 삽입하면 사전/사후 처리 접근 방식에 비해 더 나은 공간 및 성능을 얻을 수 있습니다.

### :computer:  Precision Hi-Rel은 다음 두 가지 기능을 제공합니다

- 자동 멀티 모드 삼중 모듈 중복(TMR) 삽입
- Advanced Safe Finite State Machines
