# 1
[codespace] (https://github.com/codespaces)

[무료 스프라이트 시트] ([https://itch.io](https://itch.io/game-assets/free/tag-sprites?utm_source=chatgpt.com))

[슬라임 코드] // slime.js

// 🔹 슬라임 이미지 로드
const slimeImg = new Image();
slimeImg.src = "images/slime/Slime2_Walk_with_shadow.png";

// 🔹 슬라임 프레임 설정
const SLIME_WIDTH = 64;
const SLIME_HEIGHT = 64;
const slimeFrameCount = 8;   // 가로 8프레임
let slimeFrame = 0;
let slimeFrameCounter = 0;

// 🔹 슬라임 위치
let slimeX = 200;
let slimeY = 400;
const slimeSpeed = 1.5;

// 🔹 슬라임 AI 상태
let slimeDirX = 0;
let slimeDirY = 0;
let slimeChangeDirTime = Date.now();

// 🔹 슬라임 업데이트
function updateSlime() {
  // 프레임 애니메이션
  slimeFrameCounter++;
  if (slimeFrameCounter % 8 === 0) { // 애니메이션 속도
    slimeFrame = (slimeFrame + 1) % slimeFrameCount;
  }

  // 방향 변경 (랜덤, 2~4초마다)
  const now = Date.now();
  if (now - slimeChangeDirTime > 2000 + Math.random() * 2000) {
    slimeChangeDirTime = now;

    // -1, 0, 1 중 랜덤 방향
    slimeDirX = Math.floor(Math.random() * 3) - 1;
    slimeDirY = Math.floor(Math.random() * 3) - 1;
  }

  // 위치 이동
  slimeX += slimeDirX * slimeSpeed;
  slimeY += slimeDirY * slimeSpeed;

  // 화면 밖으로 못 나가게 제한
  if (slimeX < 0) slimeX = 0;
  if (slimeX > 800 - SLIME_WIDTH * 2) slimeX = 800 - SLIME_WIDTH * 2;
  if (slimeY < 0) slimeY = 0;
  if (slimeY > 600 - SLIME_HEIGHT * 2) slimeY = 600 - SLIME_HEIGHT * 2;
}

// 🔹 슬라임 그리기
function drawSlime(ctx) {
  ctx.drawImage(
    slimeImg,
    slimeFrame * SLIME_WIDTH, // 애니메이션 프레임
    0,                        // 첫 줄만 사용
    SLIME_WIDTH, SLIME_HEIGHT,
    slimeX, slimeY,
    SLIME_WIDTH * 2, SLIME_HEIGHT * 2 // 2배 크기
  );
}
