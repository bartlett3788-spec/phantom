[phantom.html](https://github.com/user-attachments/files/28342943/phantom.html)
# phantom<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Phantom</title>
  <meta name="apple-mobile-web-app-capable" content="yes" />
  <meta name="apple-mobile-web-app-title" content="Phantom" />
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@latest/tabler-icons.min.css" />
  <style>
    :root{--color-text-primary:#1a1a1a;--color-text-secondary:#6b7280;--color-text-tertiary:#9ca3af;--color-background-primary:#ffffff;--color-background-secondary:#f3f4f6;--color-border-primary:#1a1a1a;--color-border-secondary:#d1d5db;--color-border-tertiary:#e5e7eb;--color-text-danger:#991b1b;--color-border-danger:#fca5a5;--border-radius-md:8px;--border-radius-lg:12px;--font-sans:-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif;}
    @media(prefers-color-scheme:dark){:root{--color-text-primary:#f9fafb;--color-text-secondary:#9ca3af;--color-text-tertiary:#6b7280;--color-background-primary:#111827;--color-background-secondary:#1f2937;--color-border-primary:#f9fafb;--color-border-secondary:#374151;--color-border-tertiary:#1f2937;--color-text-danger:#fca5a5;--color-border-danger:#991b1b;}}
    *{box-sizing:border-box;margin:0;padding:0}
    body{font-family:var(--font-sans);background:var(--color-background-primary);color:var(--color-text-primary);max-width:680px;margin:0 auto;padding:0 16px;min-height:100vh}
    .nav-bar{display:flex;align-items:center;border-bottom:0.5px solid var(--color-border-tertiary);margin-bottom:1.5rem;padding-top:12px}
    .nav-logo{display:flex;align-items:center;gap:8px;margin-right:auto;padding-bottom:12px}
    .nav-logo-mark{width:30px;height:30px;background:#1a1a1a;border-radius:8px;display:flex;align-items:center;justify-content:center;color:#fff;font-weight:500;font-size:14px}
    .nav-logo-name{font-size:16px;font-weight:500;color:var(--color-text-primary)}
    .nav-links{display:flex}
    .nav-link{padding:10px 12px;font-size:13px;color:var(--color-text-secondary);cursor:pointer;border-bottom:2px solid transparent;white-space:nowrap}
    .nav-link.active{color:var(--color-text-primary);font-weight:500;border-bottom-color:#1a1a1a}
    .bottom-nav{display:flex;border-top:0.5px solid var(--color-border-tertiary);padding:.5rem 0 .25rem;margin-top:2rem;position:sticky;bottom:0;background:var(--color-background-primary)}
    .bn-item{flex:1;display:flex;flex-direction:column;align-items:center;gap:3px;cursor:pointer;padding:.5rem}
    .bn-icon{font-size:20px;color:var(--color-text-secondary)}
    .bn-label{font-size:10px;color:var(--color-text-secondary)}
    .bn-item.active .bn-icon,.bn-item.active .bn-label{color:var(--color-text-primary);font-weight:500}
    .screen{display:none}.screen.visible{display:block}
    .app-tab{display:none;padding-bottom:80px}
    .chip{display:inline-flex;align-items:center;gap:6px;padding:7px 14px;border-radius:20px;border:0.5px solid var(--color-border-secondary);font-size:13px;color:var(--color-text-primary);background:var(--color-background-primary);cursor:pointer;user-select:none;transition:all .15s}
    .chip:hover{background:var(--color-background-secondary)}
    .chip.active{background:#1a1a1a;color:#fff;border-color:#1a1a1a}
    .chip.warn.active{background:#993C1D;color:#fff;border-color:#993C1D}
    .chip-tk{font-size:11px;display:none}
    .chip.active .chip-tk{display:inline}
    .days-grid{display:grid;grid-template-columns:repeat(7,1fr);gap:6px;margin-bottom:1.25rem}
    .day-chip{padding:10px 4px 5px;border-radius:var(--border-radius-md);border:0.5px solid var(--color-border-secondary);font-size:13px;text-align:center;cursor:pointer;color:var(--color-text-primary);background:var(--color-background-primary);user-select:none;transition:all .15s}
    .day-chip.active{background:#1a1a1a;color:#fff;border-color:#1a1a1a}
    .day-tk{display:none;font-size:9px;margin-top:3px}
    .day-chip.active .day-tk{display:block}
    .struct-card{border:0.5px solid var(--color-border-secondary);border-radius:var(--border-radius-md);padding:.875rem 1rem;cursor:pointer;transition:all .15s;margin-bottom:8px;display:flex;align-items:flex-start;gap:10px}
    .struct-card:hover{background:var(--color-background-secondary)}
    .struct-card.sel{border:1.5px solid #1a1a1a;background:var(--color-background-secondary)}
    .struct-icon{width:22px;height:22px;border-radius:50%;border:1.5px solid var(--color-border-secondary);display:flex;align-items:center;justify-content:center;flex-shrink:0;margin-top:1px;transition:all .15s;font-size:11px;color:transparent}
    .struct-card.sel .struct-icon{background:#1a1a1a;border-color:#1a1a1a;color:#fff}
    .struct-title{font-size:13px;font-weight:500;color:var(--color-text-primary)}
    .struct-desc{font-size:12px;color:var(--color-text-secondary);margin-top:2px}
    .day-strip{display:flex;gap:5px;margin-bottom:1.25rem;overflow-x:auto;-webkit-overflow-scrolling:touch}
    .ds-btn{min-width:42px;padding:8px 6px;border-radius:var(--border-radius-md);border:0.5px solid var(--color-border-secondary);font-size:12px;text-align:center;cursor:pointer;color:var(--color-text-secondary);background:var(--color-background-primary);transition:all .15s;user-select:none;flex-shrink:0}
    .ds-btn.viewing{background:#1a1a1a;color:#fff;border-color:#1a1a1a}
    .ds-btn.rest-day{border-style:dashed}
    .ds-btn.today-dot::after{content:'';display:block;width:4px;height:4px;border-radius:50%;background:currentColor;margin:2px auto 0}
    .card{background:var(--color-background-primary);borde
