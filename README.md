# SVG

Scalable Vector Graphic

## 1. 무엇인가

- 확장 가능한 벡터 그래픽
- XML 기반의 2차원 그래픽(SVG코드 자체가 XML 기반 - 태그)
- 텍스트 기반의 이미지 포맷
- DOM의 일부로서 각 개체별로 HTML 엘리먼트가 추가됨
- 벡터기때문에 이미지의 크기에 상관 없이 선명하게 유지되고, 모양이 많이 복잡하지 않으면 파일 사이즈도 작음.
- CSS와 JS를 이용해서도 조작이 가능하다.
- 크기가 큰 이미지 표현에 유리
- IE 8이상의 모든 브라우저에서 지원

## 2. 렌더링이 어떻게 되나 

```html
<svg version="1.1"
     baseProfile="full"
     width="300" height="200"
     xmlns="http://www.w3.org/2000/svg">
  <rect width="100%" height="100%" fill="red" />
  <circle cx="150" cy="100" r="80" fill="green" />
  <text x="150" y="125" font-size="60" text-anchor="middle" fill="white">SVG</text>
</svg>
```

- SVG 루트 요소로부터 시작함, 네임스페이스 올바르게 바인딩해야함
- SVG 루트 요소의 width, height 속성 안에 들어오는 elem들만 정상적으로 렌더링된다. 잘리거나 그런거 없이..
- **태그 순서대로 위에서부터 그려진다** 그래서 z-index같은 개념이 없음. 먼저 그려진거 위에 나중에 그려진게 덮어진다. 아래에 위치할수록 더 잘보이게 된다.(참으로 직관적)
- HTML 소스에 직접 포함되거나, img태그나 iframe, object 등으로 포함시킬 수 있다.(.svg파일)

## 3. elem

드로잉 영역(SVG 태그 영역)의 좌측 상단이 (0,0)인 좌표 시스템을 따른다.

### circle(원)

```html
<!--원 -->
<circle cx="250" cy="25" r="25">

<!--타원 -->
<circle cx="250" cy="25" rx="100" ry="25">
```

- cx, cy: 원의 중심 좌표 지정
- r : 반지름
- rx, ry : 횡반지름, 종반지름(타원을 만들때 쓰인다)

### rect(사각형)

```html
<rect x="0" y="0" width="500" height="50">
```

- x,y: 시작좌표, 왼쪽 상단 꼭지점이 위치한다.
- width, height : 길이와 높이
- rx, ry: 사각형의 둥근 꼭지점

### line(선)

```html
<line x1="0" y1="0" x2="500" y2="50" stroke="black">
```

- (x1,y1)으로부터 (x2,y2)까지 선을 그린다.

### path(선+곡선)

```html
<path d="M10 10 H 90 V 90 H 10 L 10 10"/>
```

- 여러개의 직선과 곡선을 합쳐 복잡한 도형을 그릴 수 있게 해준다
- d: path의 모양을 정의, 단위가 붙지 않는다

### polyline(선잇기)

```html
<polyline points="60 110, 65 120, 70 115, 75 130, 80 125, 85 140, 90 135, 95 150, 100 145"/>
```

- points로 설정된 좌표들을 모두 이은 직선
- 연결된 직선들의 그룹. 목록은 꽤 길어질 수 있기 때문에 모든 포인트가 하나의 속성에 포함되는 꼴. 별모양이라던가,,

### text(텍스트)

```html
<text x='250' y='25'>svg꿀잼</text>
```

- 좌표랑 내용을 넘겨서 텍스트 렌더링한다.

### textPath(선을 따라가는 텍스트)

```html
<path id="my_path" d="M 20,20 C 80,60 100,40 120,20" fill="transparent" />
<text>
  <!--뭔가 선을 태깅해준다 -->
  <textPath xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#my_path">
    A curve.
  </textPath>
</text>
```

### g(그룹)

```html
<svg viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
  <!-- Using g to inherit presentation attributes -->
  <g fill="white" stroke="green" stroke-width="5">
    <circle cx="40" cy="40" r="25" />
    <circle cx="60" cy="60" r="25" />
  </g>
</svg>
```

- SVG elem들을 그룹화할때 사용하는 컨테이너다.
- 자식 elem들에 대해 속성을 한번에 지정해줄 수 있다.

## 4. property

