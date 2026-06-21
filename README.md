@import "tailwindcss";
@import "tw-animate-css";

@custom-variant dark (&:is(.dark *));

@theme inline {
  --radius-sm: calc(var(--radius) - 4px);
  --radius-md: calc(var(--radius) - 2px);
  --radius-lg: var(--radius);
  --radius-xl: calc(var(--radius) + 4px);
  --color-background: var(--background);
  --color-foreground: var(--foreground);
  --color-card: var(--card);
  --color-card-foreground: var(--card-foreground);
  --color-popover: var(--popover);
  --color-popover-foreground: var(--popover-foreground);
  --color-primary: var(--primary);
  --color-primary-foreground: var(--primary-foreground);
  --color-secondary: var(--secondary);
  --color-secondary-foreground: var(--secondary-foreground);
  --color-muted: var(--muted);
  --color-muted-foreground: var(--muted-foreground);
  --color-accent: var(--accent);
  --color-accent-foreground: var(--accent-foreground);
  --color-destructive: var(--destructive);
  --color-destructive-foreground: var(--destructive-foreground);
  --color-border: var(--border);
  --color-input: var(--input);
  --color-ring: var(--ring);
  --color-chart-1: var(--chart-1);
  --color-chart-2: var(--chart-2);
  --color-chart-3: var(--chart-3);
  --color-chart-4: var(--chart-4);
  --color-chart-5: var(--chart-5);
  --color-sidebar: var(--sidebar);
  --color-sidebar-foreground: var(--sidebar-foreground);
  --color-sidebar-primary: var(--sidebar-primary);
  --color-sidebar-primary-foreground: var(--sidebar-primary-foreground);
  --color-sidebar-accent: var(--sidebar-accent);
  --color-sidebar-accent-foreground: var(--sidebar-accent-foreground);
  --color-sidebar-border: var(--sidebar-border);
  --color-sidebar-ring: var(--sidebar-ring);
}

:root {
  --primary: #ADD8E6;
  --primary-foreground: #333;
  --sidebar-primary: #ADD8E6;
  --sidebar-primary-foreground: #333;
  --chart-1: #ADD8E6;
  --chart-2: #87CEEB;
  --chart-3: #5DADE2;
  --chart-4: #3498DB;
  --chart-5: #2E86C1;
  --radius: 0.5rem;
  --background: oklch(1 0 0);
  --foreground: oklch(0.2 0.01 0);
  --card: oklch(1 0 0);
  --card-foreground: oklch(0.2 0.01 0);
  --popover: oklch(1 0 0);
  --popover-foreground: oklch(0.2 0.01 0);
  --secondary: oklch(0.95 0.01 200);
  --secondary-foreground: oklch(0.3 0.01 0);
  --muted: oklch(0.9 0.01 200);
  --muted-foreground: oklch(0.5 0.01 0);
  --accent: #ADD8E6;
  --accent-foreground: #333;
  --destructive: oklch(0.577 0.245 27.325);
  --destructive-foreground: oklch(0.985 0 0);
  --border: oklch(0.92 0.004 286.32);
  --input: oklch(0.92 0.004 286.32);
  --ring: #ADD8E6;
  --sidebar: oklch(1 0 0);
  --sidebar-foreground: oklch(0.2 0.01 0);
  --sidebar-accent: #ADD8E6;
  --sidebar-accent-foreground: #333;
  --sidebar-border: oklch(0.92 0.004 286.32);
  --sidebar-ring: #ADD8E6;
}

.dark {
  --primary: #ADD8E6;
  --primary-foreground: #333;
  --sidebar-primary: #ADD8E6;
  --sidebar-primary-foreground: #333;
  --background: oklch(1 0 0);
  --foreground: oklch(0.2 0.01 0);
  --card: oklch(1 0 0);
  --card-foreground: oklch(0.2 0.01 0);
  --popover: oklch(1 0 0);
  --popover-foreground: oklch(0.2 0.01 0);
  --secondary: oklch(0.95 0.01 200);
  --secondary-foreground: oklch(0.3 0.01 0);
  --muted: oklch(0.9 0.01 200);
  --muted-foreground: oklch(0.5 0.01 0);
  --accent: #ADD8E6;
  --accent-foreground: #333;
  --destructive: oklch(0.704 0.191 22.216);
  --destructive-foreground: oklch(0.985 0 0);
  --border: oklch(1 0 0 / 10%);
  --input: oklch(1 0 0 / 15%);
  --ring: #ADD8E6;
  --chart-1: #ADD8E6;
  --chart-2: #87CEEB;
  --chart-3: #5DADE2;
  --chart-4: #3498DB;
  --chart-5: #2E86C1;
  --sidebar: oklch(1 0 0);
  --sidebar-foreground: oklch(0.2 0.01 0);
  --sidebar-accent: #ADD8E6;
  --sidebar-accent-foreground: #333;
  --sidebar-border: oklch(1 0 0 / 10%);
  --sidebar-ring: #ADD8E6;
}

@layer base {
  * {
    @apply border-border outline-ring/50;
  }
  body {
    @apply bg-background text-foreground;
  }
  button:not(:disabled),
  [role="button"]:not([aria-disabled="true"]),
  [type="button"]:not(:disabled),
  [type="submit"]:not(:disabled),
  [type="reset"]:not(:disabled),
  a[href],
  select:not(:disabled),
  input[type="checkbox"]:not(:disabled),
  input[type="radio"]:not(:disabled) {
    @apply cursor-pointer;
  }
}

@layer components {
  .container {
    width: 100%;
    margin-left: auto;
    margin-right: auto;
    padding-left: 1rem;
    padding-right: 1rem;
  }

  .flex {
    min-height: 0;
    min-width: 0;
  }

  @media (min-width: 640px) {
    .container {
      padding-left: 1.5rem;
      padding-right: 1.5rem;
    }
  }

  @media (min-width: 1024px) {
    .container {
      padding-left: 2rem;
      padding-right: 2rem;
      max-width: 1280px;
    }
  }

  /* Fade-in animation */
  .fade-in-up {
    opacity: 0;
    transform: translateY(30px);
  }

  .fade-in-up.visible {
    animation: fadeInUp 0.6s ease-out forwards;
  }

  @keyframes fadeInUp {
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
}
