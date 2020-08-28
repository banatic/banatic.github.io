---
layout: default
title: 옵티컬플로우
nav_order: 2
has_children: true
parent: 컴퓨터비전
---


# 옵티컬 플로우(optical flow)

옵티컬 플로우는 이전 장면과 다음 장면 사이의 픽셀이 이동한 방향과 거리에 대한 분포입니다. 이것은 영상 속 물체가 어느 방향으로 얼마만큼 움직였는지를 알 수 있으므로 움직임 자체에 대한 인식은 물론 여기에 추가적인 연산을 가하면 움직임을 예측할 수도 있습니다.

옵티컬 플로는 계산하는 방식에 따라 크게 두 가지로 나뉩니다. 일부 픽셀만을 계산하는 희소 옵티컬플로와 영상 전체 픽셀을 모두 계산하는 밀집 옵티컬 플로 입니다.

(필요한 건 희소 옵티컬 플로인것 같아서 희소 옵티컬 플로만 작성합니다)

희소 방식의 루카스-카나테 알고리즘을 구현한 cv2.calcOpticalFlowPyrLK() 함수를 알아봅시다

- nextPts,  status, err, = cv2.calcOpticalFlowPyrLK( prevImg, nextImg, prevPts, nextPts [, status, err, winSize, maxLevel, criteria, flags, minEigThreshold])

    prevImg : 이전 프레임 영상

    nextImg :  다음 프레임 영상

    prevPts : 이전 프레임의 코너 특징점, cv2.goodFeaturesToTrack()으로 검출

    nextPts : 다음 프레임에서 이동한 코너의 특징점

    status : 결과 상태 벡터, nextPts와 같은 길이, 대응점이 있으면 1, 없으면 0

    err : 결과 에러 벡터, 대응점 간의 오차

    winSize=(21,22) :  각 이미지 피라미드의 검색 윈도 크기

    maxLevel = 3 : 이미지 피라미드 계층 수

    - criteria = (COUNT+EPS, 30, 0.01) : 반복 탐색 중지 요건

        아래와 같은 type이 있음

        cv2.TERM_CRITERIA_EPS : 정확도가 epsilon보다 작으면

        cv2.TERM_CRITERIA_MAX_ITER : 횟수를 채우면

        cv2.TERM_CRITERIA_COUNT : MAX_ITER와 동일

    max_iter : 최대 반복 횟수

    epsilon : 최소 정확도

    - flags = 0 : 연산 모드

        0 : prevPts를 nextPts의 초기 값으로 사용

        cv2.OPTFLOW_USE_INITIAL_FLOW : nextPts의 값을 초기 값으로 사용

        cv2.OPTFLOW_LK_GET_MIN_EIGENVALS : 오차를 최소 고유 값으로 계산

    minEighThreshold=le-4 : 대응점 계산에 사용할 최소 임계 고유값

cv2.calcOpticalFlowPyrLK() 함수는 픽셀 전체를 계산하지 않고 cv2.goodFeatureToTrack() 함수로 얻은 코너 특징점만 가지고 계산합니다. prevImg와 nextImg에 각각 이전 이후 프레임을 전달하고 prePts에  이전 프레임에서 검출한 코너 특징점을 전달하면 그 코너점이 이후 프레임의 어디로 이동했는지 찾아서 nextPts로 변환합니다. 이때 두 코너 점이 서로 대응하는지 여부를 status에 1과 0으로 표시해서 함께 반환합니다. 이 함수는 작은 윈도를 사용하므로 큰 움직임을 계산하지 못하는 문제가 있는데, 이를 보완하기 위해서 이미지 피라미드를 사용합니다 maxLevel에 0을 지정하면 이미지 피라미드를 사용하지 않습니다