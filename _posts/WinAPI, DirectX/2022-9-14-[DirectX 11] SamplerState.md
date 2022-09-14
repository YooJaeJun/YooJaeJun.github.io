---
title: "[DirectX 11] SamplerState"
categories:
    - WinAPIDirectX
tags:
    - WinAPIDirectX
---

<br>

# 개요

사각형 텍스쳐가 왼쪽상단 vertex 색은 빨강, 오른쪽상단 vertex 색은 초록이다.

이 사각형을 2배 확대했다.

중간 사이의 픽셀의 색은 어떻게 채울까?

<br>

# d3d11 SamplerState

유한 크기의 픽셀 배열인 텍스쳐에서 컬러를 추출해 uv 좌표에 대응하는 작업

SamplerState는 유한한 픽셀 크기를 가질 수 밖에 없는 텍스쳐의 각 픽셀 사이를 어떻게 처리할지 결정하는 State다.

<br>

# 표본 추출기(Sampler) 서술자 구조체 세팅

```cpp
    //기본 샘플러 값
    samplerDesc.Filter = D3D11_FILTER_MIN_MAG_POINT_MIP_LINEAR;
    samplerDesc.AddressU = D3D11_TEXTURE_ADDRESS_WRAP;
    samplerDesc.AddressV = D3D11_TEXTURE_ADDRESS_WRAP;
    samplerDesc.AddressW = D3D11_TEXTURE_ADDRESS_WRAP;
```

SamplerDesc 구조체 멤버 중 텍스쳐 Filter, AddressU의 타입에 대해 공부해보자.

우선 dx에서 텍스쳐를 의미하는 용어부터 보자.

<br>

# ShaderResourceView(SRV)

dx에서 텍스쳐를 말한다. 

dx에서 View는 서술자와 동의어다.

파일로부터 ID3D11ShaderResourceView를 생성해야 DirectX에게 텍스쳐를 그리라고 명령할 수 있게 된다.

<br>

# Filter

type: D3D11_FILTER

텍스쳐를 sampling 할 때 사용할 필터링 방법.

D3D11_FILTER_MIN_MAG_MIP_POINT, D3D11_FILTER_MIN_LINEAR_MAG_POINT_MIP_LINEAR 등 이름이 긴 타입들이 있다.

msdn에 있는 설명을 하나씩 요약해보면,

<br>

_POINT - 끊어지는 듯한 이미지

_LINEAR - 부드러운 이미지를 얻음 (선형 보간)

MIN - Minification 축소

MAG - Magnification 확대

MIP - Mip-mapping 밉맵
- 밉 레벨 샘플링
- 최적화된 이미지 시퀀스. 렌더링 할 때 시간과 처리 성능을 줄여주는 요소

<br>

예를 들어 D3D11_FILTER_MIN_MAG_MIP_POINT 는 확대, 축소, 밉맵 간 필터 처리 전부 POINT 방식이다.

하지만 내가 만든 게임 구현 시에는 어떤 타입을 써도 체감이 안 되어 연구가 더 필요하다.

<br>

# AddressU, V, W

type: D3D11_TEXTURE_ADDRESS_MODE

0~1 범위 밖에 있는 a v 텍스쳐 좌표를 해결하는 데 사용

D3D11_TEXTURE_ADDRESS_WRAP
- 모든 u, v 접합에서 텍스쳐가 반복된다.
- 0~1, 1~2 반복된 동일 텍스쳐

D3D11_TEXTURE_ADDRESS_MIRROR
- uv 좌표가 범위를 벗어나면 텍스쳐를 뒤집는다.
- 0~1은 정상, 1~2는 뒤집힌 이미지, 2~3은 정상, ...

D3D11_TEXTURE_ADDRESS_CLAMP
- uv 좌표가 범위를 벗어나면 끝 좌표의 픽셀이 반복된다.
- 0 미만 시 0,0 텍스쳐 색상, 1 초과 시 1,0 텍스쳐 색상

D3D11_TEXTURE_ADDRESS_BORDER
- uv 좌표가 범위를 벗어나면 D3D11_SAMPLER_DESC 혹은 HLSL 코드에 지정된 테두리 색상으로 설정된다.

D3D11_TEXTURE_ADDRESS_MIRROR_ONCE
- MIRROR + CLAMP
- 텍스쳐 좌표의 절대값을 취한 다음 최대값으로 고정함

<br>

# Texture.hlsl code

픽셀쉐이더 진입 함수

```cpp
float4 PS(PixelInput input) : SV_TARGET //SV_TARGET 은 타겟이될 색깔 
{
    float4 TextureColor =
    // 매핑된 좌표로 텍스쳐 로드
    Texture.Sample(Sampler, input.uv);
    // [생략]...
}
```

렌더링 파이프라인 PS 단계에서 Sample 코드를 끝으로 준비 완료

말로만 하고 글로만 쓰니 제대로 이해하기 힘들다.

직접 텍스쳐를 정해 uv를 점차 증감해보자.

<br>

# Example: Background Scrolling

<iframe width="1280" height="720" src="https://www.youtube.com/embed/lV-_4ipDNak" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>



<br>

# 참고

[MSDN](https://docs.microsoft.com/en-us/windows/win32/api/d3d11/ns-d3d11-d3d11_sampler_desc)

[Toymaker](http://keithditch.powweb.com/Games/html/sampler_states.html)