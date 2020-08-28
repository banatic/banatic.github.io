---
layout: default
title: 트랙커 API
nav_order: 4
has_children: true
parent: 컴퓨터비전
---

# 트랙킹 API (tracking API)

OpenCV 3.x 버전 부터는 엑스트라(contrib) 모듈에 여러 가지 머신 러닝 알고리즘으로 구현한 트래킹 API가 추가 되었습니다. 이 API를 이용하면 복잡한 이론적인 알고리즘을 전혀 알고 있지 못해도 추적할 객체의 초기 위치만 전달하면 손쉽게 객체 추적을 할 수 있습니다.

API 관련 문서

[https://docs.opencv.org/3.4.1/d0/d0a/classcv_1_1Tracker.html](https://docs.opencv.org/3.4.1/d0/d0a/classcv_1_1Tracker.html)

총 8가지의 트랙커를 제공하는데, cv2.Tracker 추상 클래스로 인터페이스를 통일해서 구현 클래스의 객체 생성함수만 다르고 사용하는 방법은 모두 같습니다

- retval = cv2.Tracker.init( image, boundingBox) : 트랙커 초기화

    image : 입력 영상

    boundingBox : 추적 대상 객체가 있는 좌표 (x, y, w, h)

- retval, boundingBox = cv2.Tracker.update(image) : 새로운 프레임에서 추적 객체 위치 찾기

    image : 새로운 프레임 영상

    retval : 추적 성공여부

    boundingBox : 새로운 프레임에서의 추적 대상 객체의 새로운 위치 (x, y, w, h)

cv2.Tracker는 init() 함수로 트랙커에 초기 추적 대상 객체의 위치를 알려주고 update()함수에 다음 프레임을 전달하면 객체가 이동한 위치를 반환합니다. 이를 지원하는 클래스의 생성자는 다음과 같습니다.

tracker = cv2.TrackerBoosting_creator() : AdaBoot 알고리즘 기반

tracker = cv2.TrackerMIL_create() : MIL(Multiple Instance Learning) 알고리즘 기반

tracker = cv2.TrackerTLD_create() : TLD(Tracking, Learning and Detection) 알고리즘 기반

tracker = cv2.TrackerKCF_create() : KCF(Kernelized Correlation Fileters) 알고리즘 기반

tracker = cv2.TrackerGOTURN_create() : 객체의 전방향/역방향을 추적해서 불일치성 측정

tracker = cv2.TrackerCSRT_create()  : CNN 기반 (openCV3.4 버전에서는 버그로 동작안됨)

tracker = cv2.TrackerMOSSE_create() : 내부적으로 그레이 스케일 사용