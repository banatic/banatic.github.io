---
layout: default
title: 코너 특징점 검출
nav_order: 1
has_children: true
parent: 컴퓨터비전
---

# 코너 특징 검출

사람은 영상 속 내용을 판단할 때 주로 픽셀의 변화가 심한 곳에 중점적으로 관심을 둡니다. 그 중에서도 엣지와 엣지가 만나는 코너(corner)에 가장 큰 관심을 두게 됩니다.

코너를 검출하기 위한 방법으로 크리스 해리스의 논문에서 처음 소개된 해리스 코너 검출이 원조격입니다. 해리스 코너 검출은 소벨(sobel) 미부능로 엣지를 검출하면서 엣지의 경사도 변화량을 측정하여 변화량이 X축과 Y축 모든 방향으로 크게 변화하는 것을 코너로 판단합니다.

OpenCV는 해리스 코너 검출을 위해 아래와 같은 함수를 제공합니다.

- dst = cv.cornerHarris( src, blockSize, ksize, k[, dst, borderType])

    src : 입력 영상, 그레이 스케일

    blockSize : 이웃 픽셀 범위

    ksize : 소벨 미분 커널 크기

    k : 코너 검출 상수, 경험적 상수 (0.04~0.06)

    - dst : 코너 검출 결과

        src와 같은 크기의 1채널 배열, 변화량의 값, 지역 최대 값이 코너점을 의미

    borderType : 외곽 영역 보정 형식

시(Shi)와 토마시(Thomasi)는 논문을 통해 해리스 코너 검출을 개선한 알고리즘을 발표했는데, 이 방법으로 검출한 코너는 객체 추적에 좋은 특징이 된다고 해서 OpenCV는 cv2.goodFeaturesToTrack()이라는 이름의 함수를 제공합니다

- corners = cv2.goodFeaturesToTrack( img, maxCorners, qualityLevel, minDistance[, corners, mask, blockSize, useHarrisDetector, k])

    img : 입력 영상

    maxCorners : 얻고 싶은 코너 개수, 강한 것 순

    qualityLevel : 코너로 판단할 스레시홀드 값

    minDistance : 코너 간 최소 거리

    mask : 검출에 제외할 마스크

    blockSize = 3 : 코너 주변 영역의 크기

    - useHarrisDetector = False : 코너 검출 방법 선택

        True = 해리스 코너 검출 방법 

        False = 시와 토마스 검출 방법

    k : 해리스 코너 검출 방법에 사용할 k 계수

    corners : 코너 검출 좌표 결과, N x 1 x 2 크기의 배열 실수 값이므로 정수로 변환 필요