# study-vuetify

아이콘 : https://material.io/resources/icons/?style=baseline
mdi-icon : http://code.meta-platform.com/assets/mdi/preview.html

##뷰티파이 BreakPoints

```
xs = 핸드폰 , sm = 아이패드, md = 노트북, lg = 컴퓨터, xl = 4k 모니터
```

참고 : https://vuetifyjs.com/ko/customization/breakpoints

##뷰티파이 색상

```
{이름 : 사용방법,색상}
{ primary : 중요,주로 짙은 파랑 },
{ info : 정보자료,주로 하늘색 },
{ success : 성공,주로 초록},
{ warning : 경고, 주로 오렌지},
{ error : 위험, 주로 빨강},
옵션 : lighten-(1~5) : 연해짐, darken-(1~4) : 짙어짐, accent(1~4) : 밝은?

```

색상 참고 : https://vuetifyjs.com/ko/styles/colors

##뷰티파이 css

```
Display : [
    d-{value}
    여기서 value = ['inline', 'inline-block', 'blcok', 'table',
                'table-cell', 'table-row', 'flex', 'inline-flex']
    사용방법 : <div class="d-inline">
    참고 : https://vuetifyjs.com/en/styles/display/
],
Spacing : [
    m = margin, p = padding
    사용방법 : <div class="pt-3">
    EX) pt = padding-top, pa = padding-all,
    참고 : https://vuetifyjs.com/en/styles/spacing/
]
```

##뷰티파이 GRID

```
Vuetify는 12구획으로 나누어진 그리드 시스템을 지원함.
v-container > v-layout > v-flex
1.v-container : 페이지 중심에 적용됨 , 만약 전체 너비를 이용하고자 하면 'fluid'를 사용.
2.v-layout : 컴포넌트는 각 섹션을 분리하는데 사용됨, v-flex 필수적으로 사용해야함.
```
