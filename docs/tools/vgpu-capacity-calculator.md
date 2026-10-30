---
title: vGPU Capacity Calculator
hide:
  - toc
---

# NVIDIA L40S vGPU Capacity Calculator

Interactive Mixed-Size vGPU capacity planner for the Glasgow TRE **6× NVIDIA L40S (48 GB)** GPU cluster (`Min Profile = 4Q`).

<div style="margin: 0 -0.4rem;">
  <iframe
    id="vgpuCalcFrame"
    src="../../assets/vgpu-capacity-calculator.html"
    style="width: 100%; min-height: 760px; border: 1px solid rgba(148, 163, 184, 0.3); border-radius: 12px; background: transparent;"
    loading="lazy"
    title="Glasgow TRE Interactive NVIDIA L40S vGPU Capacity Calculator"
  ></iframe>
</div>

<script>
  window.addEventListener('message', function(e) {
    if (e.data && e.data.type === 'vgpu-calc-resize' && e.data.height) {
      var frame = document.getElementById('vgpuCalcFrame');
      if (frame) {
        frame.style.height = (e.data.height + 20) + 'px';
      }
    }
  });
</script>
