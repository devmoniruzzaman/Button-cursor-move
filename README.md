document.addEventListener('DOMContentLoaded', function () {
  const section = document.querySelector('.video-section');
  const btn = document.querySelector('.play-btn');

  if (!section || !btn) return;

  if (getComputedStyle(section).position === 'static') {
    section.style.position = 'relative';
  }

  let mouseInside = false;

  section.addEventListener('mouseenter', function () {
    mouseInside = true;
  });

  section.addEventListener('mousemove', function (e) {
    if (!mouseInside) return;

    const rect = section.getBoundingClientRect();
    const btnRect = btn.getBoundingClientRect();
    const btnW = btnRect.width;
    const btnH = btnRect.height;

    // Get raw mouse position relative to section
    let x = e.clientX - rect.left;
    let y = e.clientY - rect.top;

    // Clamp X and Y so button always stays within section
    const minX = btnW / 2;
    const maxX = rect.width - btnW / 2;
    const minY = btnH / 2;
    const maxY = rect.height - btnH / 2;

    x = Math.max(minX, Math.min(x, maxX));
    y = Math.max(minY, Math.min(y, maxY));

    btn.style.left = x + 'px';
    btn.style.top = y + 'px';
    btn.style.transform = 'translate(-50%, -50%) scale(1.1)';
  });

  section.addEventListener('mouseleave', function () {
    mouseInside = false;
    btn.style.transform = 'translate(-50%, -50%) scale(1)';
  });
});
