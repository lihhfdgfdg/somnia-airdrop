[somnia-airdrop-locked.html](https://github.com/user-attachments/files/22020407/somnia-airdrop-locked.html)
<!DOCTYPE html>
<html lang="zh">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Somnia Airdrop — 专属领取</title>
  <style>
    body { margin:0; font-family: Arial, sans-serif; background: linear-gradient(to bottom,#0f172a,#1e293b,#0f172a); color:white; }
    header { position:sticky;top:0;backdrop-filter:blur(10px);background:rgba(15,23,42,.7);border-bottom:1px solid rgba(255,255,255,0.1);padding:10px 20px;display:flex;justify-content:space-between;align-items:center; }
    button { padding:10px 16px;border:none;border-radius:9999px;cursor:pointer;font-weight:bold; }
    .primary { background:#6366f1;color:white; }
    .secondary { background:#475569;color:white; }
    .danger { background:#ef4444;color:white; }
    .card { background:rgba(30,41,59,.7);border:1px solid rgba(255,255,255,0.1);border-radius:16px;padding:20px;margin-top:20px; }
    input { padding:8px 12px;border-radius:8px;border:none;width:100%; }
    .muted { color:#94a3b8; }
    .footer { border-top:1px solid rgba(255,255,255,0.1);padding:20px;text-align:center;color:#94a3b8;font-size:14px; }
    .badge { display:inline-block;padding:2px 8px;border-radius:9999px;border:1px solid rgba(255,255,255,.2);font-size:12px; }
  </style>
</head>
<body>
  <header>
    <div>🌙 Somnia Airdrop • 专属领取</div>
    <span class="badge">演示站 · 离线页面</span>
  </header>
  <main style="max-width:900px;margin:0 auto;padding:20px;">
    <h1>本页面仅限<strong>预置地址</strong>领取</h1>
    <p class="muted">只有以下地址符合资格，额度固定为 100 颗。其他任意地址均不可领取。</p>

    <div class="card">
      <h3>允许领取的地址（唯一）</h3>
      <div style="word-break:break-all;background:rgba(2,6,23,.6);padding:10px;border-radius:8px;border:1px solid rgba(255,255,255,.08)">yiJSMGRZ6xgWJYpRfNStFDvVmeq24RNVP2rD8Jxwei3</div>
    </div>

    <div class="card">
      <h3>资格检测 & 领取</h3>
      <label class="muted">输入钱包地址（粘贴即可）：</label>
      <input id="walletInput" placeholder="在此粘贴地址"/>
      <div style="margin-top:10px;display:flex;gap:10px;flex-wrap:wrap;">
        <button class="primary" onclick="checkEligibility()">检测资格</button>
        <button id="claimBtn" class="secondary" onclick="claim()" disabled>领取 100 颗</button>
      </div>
      <div id="result" style="margin-top:15px;color:#cbd5e1"></div>
      <div id="note" class="muted" style="margin-top:8px;font-size:12px">提示：这是离线演示页面，不会发起链上交易，仅用于前端流程演示。</div>
    </div>
  </main>
  <div class="footer">© 2025 Somnia Airdrop Demo · 仅演示 · 不收集任何数据</div>

  <script>
    const WHITELIST = new Set(["yiJSMGRZ6xgWJYpRfNStFDvVmeq24RNVP2rD8Jxwei3"]);
    const ALLOCATION = 100;

    function normalize(s) {
      return (s || "").trim();
    }

    function eligible(addr) {
      return WHITELIST.has(addr);
    }

    function checkEligibility() {
      const input = document.getElementById("walletInput");
      const addr = normalize(input.value);
      const res = document.getElementById("result");
      const claimBtn = document.getElementById("claimBtn");

      if (!addr) {
        res.innerHTML = "<span style='color:#fca5a5'>请先粘贴地址</span>";
        claimBtn.disabled = true;
        return;
      }

      if (eligible(addr)) {
        res.innerHTML = `✅ 符合资格<br>地址：<b>${addr}</b><br>可领取：<b>${ALLOCATION}</b> 颗`;
        claimBtn.disabled = false;
        claimBtn.dataset.addr = addr;
      } else {
        res.innerHTML = `❌ 暂无资格<br>该页面仅限预置地址领取。`;
        claimBtn.disabled = true;
        claimBtn.dataset.addr = "";
      }
    }

    function claim() {
      const btn = document.getElementById("claimBtn");
      const addr = btn.dataset.addr || "";
      if (!addr || !eligible(addr)) return;

      // 仅做前端演示：本地记录已领取状态
      const key = "claimed::" + addr;
      if (localStorage.getItem(key)) {
        alert("该地址已标记为领取完成（本地记录）");
        return;
      }
      localStorage.setItem(key, "1");
      btn.disabled = true;
      btn.className = "primary";
      btn.innerText = "已领取（演示）";
      const res = document.getElementById("result");
      res.innerHTML = `🎉 领取成功（演示态）<br>地址：<b>${addr}</b> 已标记领取 <b>${ALLOCATION}</b> 颗`;
    }
  </script>
</body>
</index.html>
