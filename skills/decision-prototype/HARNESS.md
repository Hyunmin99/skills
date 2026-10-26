# Prototype Harness

`decision-prototype`이 만드는 HTML의 공통 틀입니다. 아래 블록을 **그대로** 복사하고, 프레임 안(`.frame`)만 화면에 맞게 만듭니다.

## 페이지 구성 (순서 고정)

```
.page
├── section.ctl      컨트롤 바: 제목 + 한 줄 안내 + 토글 그룹(.grp > .seg) + [처음 상태로]
├── div.frame        운영 화면을 옮긴 프레임 (화면마다 다름)
├── section.cases    어떤 경우에 무엇이 나오나: 조건 표, 예시 데이터 결과 표
└── section.notes    보는 법: 예시 출처, 현재/제안 차이, 코드로 확인한 근거
.toast               조작 피드백 (프로토타입에서 동작하지 않는 버튼 안내 포함)
```

- 컨트롤 바 첫 토글은 항상 `화면: 현재 / 제안`.
- 추천안 버튼에는 `<span class="rec">추천</span>`.
- '어떤 경우에' 표의 안내 문구 칸은 `.l1`(첫째 줄) + `.l2`(둘째 줄), 나오지 않는 칸은 `td.none`에 "나오지 않음".

## CSS (그대로 복사)

토큰 블록은 세일즈맵 디자인 토큰입니다(salesmap.kr/design/token.md). 다른 제품이면 그 제품의 토큰으로 바꿉니다. 화면에 필요한 토큰만 추가하고, 있는 값은 바꾸지 않습니다.

```css
@font-face{font-family:"Pretendard Variable";font-weight:45 920;font-style:normal;font-display:swap;src:url(https://cdn.jsdelivr.net/npm/pretendard@1.3.9/dist/web/variable/woff2/PretendardVariable.woff2) format("woff2-variations")}
:root{
  --white:#FEFEFF; --black:#0D0E11;
  --gray-50:#F9F9FA; --gray-100:#F2F3F5; --gray-200:#E5E7EB; --gray-300:#D4D7DC; --gray-400:#C2C5CC; --gray-500:#A9ABB3;
  --gray-600:#8C8F96; --gray-700:#6A6D74; --gray-800:#50535C; --gray-900:#393A3F; --gray-950:#18191C;
  --main-50:#F0F4FF; --main-100:#EBF0FF; --main-600:#6366F1; --main-700:#554AE3; --main-800:#3E36C4;
  --orange-50:#FFF6F1; --orange-600:#F77B3A;
  --yellow-50:#FFFBED; --yellow-600:#F8CA22; --yellow-900:#D4A600;
  --dim-scrim:rgba(13,14,17,.40); --dim-hover:rgba(24,25,28,.05);
  --shadow-card:0 2px 12px rgba(106,109,116,.15);
  --shadow-md:0 0 20px rgba(13,14,17,.20),0 0 8px rgba(13,14,17,.08);
  --ease:cubic-bezier(.2,0,0,1);
  --font:"Pretendard Variable",Pretendard,-apple-system,BlinkMacSystemFont,"Apple SD Gothic Neo","Segoe UI",Roboto,sans-serif;
}
*{box-sizing:border-box}
html{font-family:var(--font);font-variant-numeric:tabular-nums;-webkit-font-smoothing:antialiased}
body{margin:0;background:var(--gray-100);color:var(--gray-950);font-size:14px;line-height:20px;padding-inline:16px;padding-block:24px 48px}
button,input{font:inherit;color:inherit}
:focus-visible{outline:2px solid var(--main-600);outline-offset:2px}
.page{max-width:1200px;margin:0 auto;display:flex;flex-direction:column;gap:16px}

/* prototype controls */
.ctl{background:var(--white);border-radius:12px;padding:16px 20px;display:flex;flex-wrap:wrap;gap:16px 32px;align-items:flex-end}
.ctl__title{width:100%;display:flex;flex-wrap:wrap;align-items:baseline;gap:8px}
.ctl__title b{font-size:18px;line-height:24px;font-weight:600}
.ctl__title span{color:var(--gray-700)}
.grp{display:flex;flex-direction:column;gap:8px}
.grp label{font-size:12px;line-height:16px;color:var(--gray-700);font-weight:500}
.seg{display:inline-flex;flex-wrap:wrap;background:var(--gray-100);border-radius:8px;padding:4px;gap:4px}
.seg button{border:0;background:none;height:28px;padding:0 12px;border-radius:6px;font-size:14px;font-weight:500;color:var(--gray-700);cursor:pointer;transition:background-color 150ms var(--ease)}
.seg button:hover{color:var(--gray-950)}
.seg button[aria-pressed="true"]{background:var(--white);color:var(--gray-950);box-shadow:0 1px 2px rgba(13,14,17,.08)}
.seg button:disabled{opacity:.4;cursor:default}
.rec{font-size:10px;line-height:16px;font-weight:600;color:var(--main-600);margin-left:4px}
.toast{position:fixed;left:50%;bottom:32px;transform:translate(-50%,8px);background:var(--gray-950);color:var(--white);padding:12px 16px;border-radius:8px;opacity:0;pointer-events:none;transition:opacity 200ms var(--ease),transform 200ms var(--ease);max-width:calc(100vw - 32px);z-index:10}
.toast.show{opacity:1;transform:translate(-50%,0)}

.notes{background:var(--white);border-radius:12px;padding:16px 20px;display:flex;flex-direction:column;gap:8px}
.notes b{font-weight:600}
.notes ul{margin:0;padding-left:20px;display:flex;flex-direction:column;gap:4px;color:var(--gray-800)}
.notes code{font-family:ui-monospace,Menlo,monospace;font-size:12px;background:var(--gray-100);padding:2px 4px;border-radius:4px}
/* case spec */
.cases{background:var(--white);border-radius:12px;padding:20px;display:flex;flex-direction:column;gap:24px}
.cases h3{margin:0;font-size:18px;line-height:24px;font-weight:600}
.cases h4{margin:0 0 4px;font-size:16px;line-height:24px;font-weight:600}
.cases__desc{margin:0 0 12px;color:var(--gray-700)}
.tbl-wrap{overflow-x:auto;border:1px solid var(--gray-200);border-radius:8px}
.tbl{width:100%;min-width:720px;border-collapse:collapse}
.tbl th,.tbl td{padding:10px 16px;text-align:left;vertical-align:top;border-bottom:1px solid var(--gray-200)}
.tbl th{background:var(--gray-100);color:var(--gray-700);font-weight:500;white-space:nowrap}
.tbl tbody tr:last-child td{border-bottom:0}
.tbl td.none{color:var(--gray-500)}
.tbl .l1{font-weight:500}
.tbl .l2{color:var(--gray-700);font-size:12px;line-height:16px;margin-top:2px}
.tbl em{font-style:normal;color:var(--main-600);font-weight:500}
```

## 마크업 (그대로 복사, 텍스트만 교체)

```html
<div class="page">
  <section class="ctl" aria-label="프로토타입 설정">
    <div class="ctl__title"><b>{티켓} {주제}</b><span>{무엇을 눌러 보면 되는지 한 줄}</span></div>
    <div class="grp"><label id="l-ver">화면</label>
      <div class="seg" role="group" aria-labelledby="l-ver" data-key="ver">
        <button type="button" data-v="asis">현재</button><button type="button" data-v="tobe">제안</button>
      </div></div>
    <div class="grp"><label id="l-data">{상태 데이터}</label>
      <div class="seg" role="group" aria-labelledby="l-data" data-key="data">
        <button type="button" data-v="some">{1명 이상}</button><button type="button" data-v="mixed">{여러 상태}</button><button type="button" data-v="none">{없음}</button>
      </div></div>
    <div class="grp"><label>&nbsp;</label>
      <div class="seg"><button type="button" data-act="reset">처음 상태로</button></div></div>
  </section>

  <div class="frame" id="frame"><!-- 운영 화면 --></div>

  <section class="cases" aria-labelledby="cases-t">
    <h3 id="cases-t">어떤 경우에 무엇이 나오나</h3>
    <div>
      <h4>{안내 이름}</h4>
      <p class="cases__desc">{어디에 어떻게 나오는지 한 문장}</p>
      <div class="tbl-wrap"><table class="tbl">
        <thead><tr><th>조건</th><th>{안내 이름}</th></tr></thead>
        <tbody>
          <tr><td>{조건}</td><td class="none">나오지 않음</td></tr>
          <tr><td>{조건}</td><td><div class="l1">{첫째 줄}</div><div class="l2">{둘째 줄}</div></td></tr>
        </tbody>
      </table></div>
    </div>
  </section>

  <section class="notes" aria-label="메모">
    <b>보는 법</b>
    <ul>
      <li>예시는 운영 {화면} '{실제 이름}'입니다.</li>
      <li>'현재'는 운영과 같습니다.</li>
    </ul>
  </section>
</div>
<div class="toast" id="toast" role="status" aria-live="polite"></div>
```

## 스크립트 패턴

- 상태는 객체 하나(`const S = {ver:'tobe', ...}`)에 둔다. 토글 그룹의 `data-key`가 `S`의 키, 버튼의 `data-v`가 값.
- `render()` 하나가 `S`와 편집 중인 데이터로 프레임 전체를 다시 그린다. 입력 중 다시 그릴 때는 포커스와 커서 위치를 복원한다.
- 이벤트는 `document`에 위임한다: `.seg[data-key] button`, `[data-act]`, `[data-toast]`.
- [처음 상태로]는 편집 데이터와 열린 패널·다이얼로그를 모두 초기화한다.

```js
let tt;
function toast(m){ const t = document.getElementById('toast'); t.textContent = m; t.classList.add('show'); clearTimeout(tt); tt = setTimeout(()=>t.classList.remove('show'), 1800); }

```
