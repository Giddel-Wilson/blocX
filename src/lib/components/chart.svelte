<script lang="ts">
  import { onMount } from 'svelte';

  export let type: 'line' | 'area' | 'multi' = 'line';
  export let color: string = '#8b5cf6';
  
  let canvas: HTMLCanvasElement;
  
  onMount(() => {
    const ctx = canvas.getContext('2d');
    if (!ctx) return;

    // Set canvas size
    canvas.width = canvas.offsetWidth * 2;
    canvas.height = canvas.offsetHeight * 2;
    ctx.scale(2, 2);

    // Draw grid
    const gridColor = 'rgba(255, 255, 255, 0.1)';
    ctx.strokeStyle = gridColor;
    ctx.lineWidth = 0.5;

    // Horizontal grid lines
    for (let i = 0; i < canvas.offsetHeight; i += 20) {
      ctx.beginPath();
      ctx.moveTo(0, i);
      ctx.lineTo(canvas.offsetWidth, i);
      ctx.stroke();
    }

    // Vertical grid lines
    for (let i = 0; i < canvas.offsetWidth; i += 40) {
      ctx.beginPath();
      ctx.moveTo(i, 0);
      ctx.lineTo(i, canvas.offsetHeight);
      ctx.stroke();
    }

    if (type === 'multi') {
      // Draw multiple lines
      const colors = ['#8b5cf6', '#06b6d4', '#22c55e'];
      colors.forEach((color, index) => {
        drawLine(ctx, color, index);
      });
    } else {
      // Draw single line
      drawLine(ctx, color);
      
      if (type === 'area') {
        // Add gradient fill
        const gradient = ctx.createLinearGradient(0, 0, 0, canvas.offsetHeight);
        gradient.addColorStop(0, `${color}33`);
        gradient.addColorStop(1, `${color}00`);
        ctx.fillStyle = gradient;
        ctx.fill();
      }
    }
  });

  function drawLine(ctx: CanvasRenderingContext2D, color: string, offset = 0) {
    // Generate random data points with some smoothing
    const points: number[] = [];
    let prev = Math.random();
    for (let i = 0; i < 20; i++) {
      prev = prev * 0.7 + Math.random() * 0.3;
      points.push(prev);
    }
    
    ctx.beginPath();
    ctx.strokeStyle = color;
    ctx.lineWidth = 2;
    
    points.forEach((point, index) => {
      const x = (index / (points.length - 1)) * canvas.offsetWidth;
      const y = point * canvas.offsetHeight * 0.8 + (offset * 20);
      if (index === 0) {
        ctx.moveTo(x, y);
      } else {
        // Create smooth curve
        const xc = (x + (x - canvas.offsetWidth / points.length)) / 2;
        const yc = (y + points[index - 1] * canvas.offsetHeight * 0.8 + (offset * 20)) / 2;
        ctx.quadraticCurveTo(xc, yc, x, y);
      }
    });
    
    ctx.stroke();
  }
</script>

<canvas
  bind:this={canvas}
  class="w-full h-full"
></canvas>