---
layout: default
title: 캐스케이드 분류기
nav_order: 1
has_children: true
parent: 컴퓨터비전
---


# 캐스케이드 분류기

캐스케이드 분류기는 개발자가 직접 머신러닝 학습 알고리즘을 사용하지 않고도 객체를 검출할 수 있도록 opencv가 제공하는 대표적인 상위 레벨 API입니다

캐스케이드 분류기는 트리 기반 부스트된 거절 케스케이드 개념을 기초로 하며 얼굴 인식을 목적으로 했다가 이후 그 목적을 일반화해서 얼굴 말고도 대분의 물체(강체) 인식이 가능합니다

opencv에서 처음으로 구현할 때는 알프레드 하르가 처음 제안한 하르 웨이블릿이라는 피처만 지원하여 하르 케스케이드로 더 많이 알려져 있었지만, 이후 대각선 피처와 로컬 바이너리 패턴(LBP)을 추가 확장하여 이제는 다른 피처를 직접 작성해서 사용할 수 도 있습니다. 이를 위해 opencv_traincascade등의 번들 프로그램을 함께 제공하기도 합니다.

opencv는 케스케이드 분류기에 사용할 수 있는 훈련된 검출기를 xml 파일 형태로 제공합니다

opencv는 훈련된 검출기를 이용해서 객체를 검출하기 위한 캐스케이드 분류기 API를 아래와 같이 제공합니다

- classfier = cv2.CasscadeClassfier([filename]): 케스케이드 분류기 생성자

    filename : 검출기 저장 파일 경로

    classfier : 케스케이드 분류기 객체

- rect = classfier.detectMultiScale(img, scaleFactor, minNeighbors[,flags, minSize, maxSize)

    img : 입력 이미지

    scaleFactor : 이미지 확대 크기에 제한, 1.3~1.5(큰 값 : 인식 기회 증가, 속도 감소)

    minNeighbors : 요구되는 이웃 수 (큰 값 : 품질 증가, 검출 개수 감소

    flags : 구식 API를 위한 것, 지금은 사용 안함

    minSize, maxSize : 해당 사이즈 영역을 넘으면 검출 무시

    rect : 검출된 영역 좌표 (x, y, w, h)

cascading 검출기 작성 관련 블로그

                          

[OpenCV Haar/cascade training 튜토리얼](https://darkpgmr.tistory.com/70)