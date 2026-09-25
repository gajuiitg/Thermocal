<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-TND589HSEC"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-TND589HSEC');
</script>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, shrink-to-fit=yes">
<title>PR-EOS Density &amp; Cp Calculator | C1-C3 Light Hydrocarbons</title>
<style>
  :root{
    --bg: #f3f6f8;
    --panel: #ffffff;
    --panel2: #f0f4f7;
    --border: #d8e1e7;
    --text: #1b2a33;
    --text-dim: #556872;
    --accent: #1f8fa8;
    --accent2: #d97706;
    --vapor: #1f5fa8;
    --liquid: #0f8f73;
    --mono: 'IBM Plex Mono', 'Consolas', monospace;
    --sans: 'IBM Plex Sans', 'Segoe UI', Arial, sans-serif;
  }
  *{box-sizing:border-box;}
  body{
    margin:0; background:var(--bg); color:var(--text);
    font-family:var(--sans); font-size:14px; line-height:1.5;
  }
  header{
    padding:20px 28px 16px; border-bottom:1px solid var(--border);
    display:flex; justify-content:space-between; align-items:baseline; flex-wrap:wrap; gap:8px;
  }
  header h1{
    font-family:var(--mono); font-size:17px; font-weight:600; margin:0; letter-spacing:0.5px;
    color:var(--text);
  }
  header h1 span{color:var(--accent);}
  header .sub{font-size:12px; color:var(--text-dim); font-family:var(--mono);}
  main{max-width:1180px; margin:0 auto; padding:24px 20px 60px;}
  .grid{display:grid; grid-template-columns: 380px 1fr; gap:20px;}
  @media (max-width:880px){.grid{grid-template-columns:1fr;}}

  .panel{background:var(--panel); border:1px solid var(--border); border-radius:6px; padding:18px 20px;}
  .panel + .panel{margin-top:16px;}
  .panel h2{
    font-family:var(--mono); font-size:12px; text-transform:uppercase; letter-spacing:1px;
    color:var(--text-dim); margin:0 0 14px; padding-bottom:8px; border-bottom:1px solid var(--border);
  }

  label{display:block; font-size:12px; color:var(--text-dim); margin-bottom:4px; margin-top:12px;}
  label:first-of-type{margin-top:0;}
  input[type=number], select{
    width:100%; background:var(--panel2); border:1px solid var(--border); border-radius:4px;
    color:var(--text); padding:8px 10px; font-family:var(--mono); font-size:13px;
  }
  input[type=number]:focus, select:focus{outline:none; border-color:var(--accent);}
  .row2{display:grid; grid-template-columns:1fr 1fr; gap:10px;}

  .phase-toggle{display:flex; border:1px solid var(--border); border-radius:4px; overflow:hidden; margin-top:12px;}
  .phase-toggle button{
    flex:1; background:var(--panel2); border:none; color:var(--text-dim); padding:9px 0;
    font-family:var(--mono); font-size:12px; cursor:pointer; transition:.15s;
  }
  .phase-toggle button.active{background:var(--accent); color:#08110f; font-weight:600;}

  .comp-table{width:100%; border-collapse:collapse; margin-top:6px;}
  .comp-table th{
    text-align:left; font-size:10px; color:var(--text-dim); font-weight:500; padding:4px 6px;
    text-transform:uppercase; letter-spacing:0.5px;
  }
  .comp-table td{padding:3px 6px;}
  .comp-table input[type=number]{padding:5px 8px; font-size:12px;}
  .comp-table input[type=number]:disabled{opacity:0.3; cursor:not-allowed;}
  .comp-table td.name-col{font-family:var(--mono); font-size:12px; white-space:normal;}
  .comp-table td.chk-col{width:22px; text-align:center; padding:3px 2px;}
  .comp-table input[type=checkbox]{width:14px; height:14px; cursor:pointer; accent-color:var(--accent);}
  .comp-table td.group-hdr{
    padding:9px 6px 3px; font-size:10px; color:var(--accent2); text-transform:uppercase;
    letter-spacing:0.6px; font-weight:600; border-bottom:1px solid var(--border);
  }
  .comp-sum{font-family:var(--mono); font-size:11px; color:var(--text-dim); margin-top:8px; text-align:right;}
  .comp-sum.err{color:#e06c5c;}

  button.calc{
    width:100%; margin-top:16px; background:var(--accent); color:#08110f; border:none;
    border-radius:4px; padding:11px 0; font-family:var(--mono); font-size:13px; font-weight:700;
    letter-spacing:0.5px; cursor:pointer; text-transform:uppercase;
  }
  button.calc:hover{background:#63c2b8;}

  .results-grid{display:grid; grid-template-columns:1fr 1fr; gap:14px;}
  .result-card{
    background:var(--panel2); border:1px solid var(--border); border-radius:5px; padding:14px 16px;
  }
  .result-card .label{font-size:11px; color:var(--text-dim); text-transform:uppercase; letter-spacing:0.5px;}
  .result-card .value{font-family:var(--mono); font-size:24px; font-weight:600; margin-top:4px;}
  .result-card .unit{font-size:12px; color:var(--text-dim); margin-left:4px;}
  .result-card.vapor .value{color:var(--vapor);}
  .result-card.liquid .value{color:var(--liquid);}

  .detail-table{width:100%; border-collapse:collapse; margin-top:16px; font-family:var(--mono); font-size:12px;}
  .detail-table td{padding:6px 10px; border-bottom:1px solid var(--border);}
  .detail-table td:first-child{color:var(--text-dim); width:55%;}
  .detail-table td:last-child{text-align:right;}

  .warn{
    background:#2a1f14; border:1px solid #5c4423; color:#e8a23d; border-radius:4px;
    padding:10px 12px; font-size:12px; margin-top:12px; display:none;
  }
  .warn.show{display:block;}

  .footer-note{margin-top:20px; font-size:11px; color:var(--text-dim); line-height:1.6;}
  .footer-note code{background:var(--panel2); padding:1px 5px; border-radius:3px;}

  .placeholder{color:var(--text-dim); font-size:13px; text-align:center; padding:60px 20px;}

  .mode-toggle{display:flex; gap:8px; margin-bottom:20px;}
  .mode-toggle button{
    background:var(--panel); border:1px solid var(--border); color:var(--text-dim);
    padding:10px 20px; border-radius:6px; font-family:var(--mono); font-size:12px;
    letter-spacing:0.5px; cursor:pointer; font-weight:600;
  }
  .mode-toggle button.active{background:var(--accent); color:#08110f; border-color:var(--accent);}

  .flash-table{width:100%; border-collapse:collapse; margin-top:10px; font-family:var(--mono); font-size:12px;}
  .flash-table th{
    text-align:right; font-size:10px; color:var(--text-dim); font-weight:500; padding:6px 8px;
    text-transform:uppercase; letter-spacing:0.5px; border-bottom:1px solid var(--border);
  }
  .flash-table th:first-child{text-align:left;}
  .flash-table td{padding:6px 8px; text-align:right; border-bottom:1px solid var(--border);}
  .flash-table td:first-child{text-align:left; color:var(--text);}
  .flash-table .kcol{color:var(--accent2);}

  .beta-bar-wrap{margin:16px 0; background:var(--panel2); border-radius:5px; overflow:hidden; height:34px; position:relative; border:1px solid var(--border);}
  .beta-bar-liquid{position:absolute; left:0; top:0; bottom:0; background:var(--liquid); display:flex; align-items:center; justify-content:center; font-family:var(--mono); font-size:11px; color:#08110f; font-weight:700;}
  .beta-bar-vapor{position:absolute; right:0; top:0; bottom:0; background:var(--vapor); display:flex; align-items:center; justify-content:center; font-family:var(--mono); font-size:11px; color:#08110f; font-weight:700;}

  .export-toolbar{display:flex; gap:8px; margin-top:16px; padding-top:14px; border-top:1px solid var(--border);}
  .export-toolbar button{
    flex:1; background:var(--panel2); border:1px solid var(--border); color:var(--text);
    padding:9px 10px; border-radius:5px; font-family:var(--mono); font-size:11px;
    letter-spacing:0.3px; cursor:pointer; font-weight:600;
  }
  .export-toolbar button:hover{border-color:var(--accent); color:var(--accent);}

  #printMeta{display:none;}

  @media print {
    body{background:#fff; color:#000;}
    header, .mode-toggle, .grid > div:first-child, .footer-note, .export-toolbar, .warn{
      display:none !important;
    }
    .grid{display:block;}
    .panel{border:none; background:#fff; padding:0;}
    .result-card{border:1px solid #999; background:#fff;}
    .result-card .value, .result-card .label{color:#000;}
    .detail-table td, .flash-table td, .flash-table th{color:#000; border-color:#ccc;}
    #printMeta{
      display:block; font-family:var(--sans); font-size:11px; color:#333;
      margin-bottom:14px; padding-bottom:10px; border-bottom:2px solid #333;
    }
    main{max-width:100%; padding:0;}
  }
</style>
</head>
<body>

<header>
  <h1>PR-EOS <span>DENSITY, Cp, FLASH &amp; JT</span> CALCULATOR</h1>
  <div class="sub">Peng-Robinson (1978) &middot; C1/C2/C2=/C3/C3= &middot; Pure &amp; Mixture</div>
</header>

<main>
  <div id="printMeta"></div>

  <div class="mode-toggle">
    <button id="modeDensity" class="active" onclick="setMode('density')">DENSITY &amp; Cp</button>
    <button id="modeJT" onclick="setMode('jt')">ISENTHALPIC (JT)</button>
    <button id="modeCV" onclick="setMode('cv')">CALORIFIC VALUE</button>
    <button id="modeMix" onclick="setMode('mix')">MIXING (2 STREAMS)</button>
  </div>

  <div id="densityMode">
  <div class="grid">
    <!-- LEFT: INPUTS -->
    <div>
      <div class="panel">
        <h2>Conditions</h2>
        <div class="row2">
          <div>
            <label>Temperature</label>
            <input type="number" id="tempVal" value="25" step="any">
          </div>
          <div>
            <label>Unit</label>
            <select id="tempUnit">
              <option value="C">&deg;C</option>
              <option value="K">K</option>
              <option value="F">&deg;F</option>
            </select>
          </div>
        </div>
        <div class="row2">
          <div>
            <label>Pressure</label>
            <input type="number" id="presVal" value="1" step="any">
          </div>
          <div>
            <label>Unit</label>
            <select id="presUnit">
              <option value="atm">atm</option>
              <option value="bar" selected>bar</option>
              <option value="barg">barg</option>
              <option value="kPa">kPa</option>
              <option value="kgcm2g">kg/cm&sup2;g</option>
              <option value="psi">psia</option>
            </select>
          </div>
        </div>
        <label>Phase (which cubic root to report)</label>
        <div class="phase-toggle">
          <button id="btnVapor" class="active" onclick="setPhase('vapor')">VAPOR</button>
          <button id="btnLiquid" onclick="setPhase('liquid')">LIQUID</button>
        </div>
      </div>

      <div class="panel">
        <h2>Composition</h2>
        <div class="phase-toggle">
          <button id="dBasisMol" class="active" onclick="setBasis('d','mol')">MOL %</button>
          <button id="dBasisWt" onclick="setBasis('d','wt')">WT %</button>
        </div>
        <table class="comp-table" id="compTable">
          <thead><tr><th></th><th>Component</th><th id="dCompColHdr">z<sub>i</sub></th></tr></thead>
          <tbody></tbody>
        </table>
        <div class="comp-sum" id="compSum">Sum: 1.0000</div>
        <div class="footer-note" style="margin-top:6px;">Tick a component to include it in the mixture. Newly ticked components start at 0 &mdash; enter a value.</div>
      </div>

      <button class="calc" onclick="runCalc()">CALCULATE</button>
      <div class="warn" id="warnBox"></div>
    </div>

    <!-- RIGHT: RESULTS -->
    <div>
      <div class="panel" id="resultsPanel">
        <h2>Results</h2>
        <div class="placeholder">Enter conditions and composition, then click Calculate.</div>
      </div>
    </div>
  </div>

  <div class="footer-note">
    Model: Peng-Robinson (1978) cubic EOS, van der Waals one-fluid mixing rules, literature/simulator-default
    binary interaction parameters (k<sub>ij</sub>) for light hydrocarbon pairs. Ideal-gas Cp from Reid/Prausnitz/Poling
    polynomials (<code>Cp&deg; = A + BT + CT&sup2; + DT&sup3;</code>); real-gas Cp includes PR departure function.
    Liquid-phase density from PR EOS without volume translation — expect ~2&ndash;5% deviation from measured
    saturated-liquid density; cross-check against plant data or a process simulator for custody-transfer /
    fiscal use. Not a substitute for validated process simulation for safety-critical design.
    <br><br>
    <strong>IBP / FBP</strong> (mixtures only): bubble-point and dew-point temperature at the input pressure,
    found via the PR-EOS flash engine. <strong>Flash Point</strong> is a theoretical estimate using Antoine
    vapor pressures and the Le Chatelier lower-flammability-limit (LFL) mixing rule at 1&nbsp;atm, approximating
    liquid composition &asymp; feed composition — it is <em>not</em> a substitute for a laboratory-measured
    flash point (ASTM D56/D93/D3278) and should not be used as the sole basis for fire-safety classification
    or regulatory compliance.
    <br><br>
    <strong>Extended component set</strong> (1,3-butadiene, n-butane, C5H10/1-pentene, benzene, toluene,
    n-hexane, methanol, VCM, EDC, HCl, chlorine, EO, EG): critical properties (T<sub>c</sub>, P<sub>c</sub>,
    &omega;) are literature-typical values, and untabulated binary pairs default to k<sub>ij</sub>=0
    (ideal mixing) &mdash; verify against DIPPR/NIST/a process simulator before design or safety use.
    Saturation-temperature (Antoine) and Flash Point estimates are not yet available for these components
    (density, Cp, and JT/enthalpy calculations are unaffected).
     <footer class="no-print">
      <h3>Developer Information</h3>
      <p><strong>Gajanand Yadav</strong></p>
      <p>Chemical Engineer</p>
      <p>Email: <a href="mailto:gajanandiitg@gmail.com">gajanandiitg@gmail.com</a>
      <p><a href="https://www.linkedin.com/in/gajanand-yadav-512624a5/" target="_blank">LinkedIn</a></p>
      Mobile: <a href="tel:+918369354472">+91-8369354472</a></p>
      <p>For Back to Profile </p> 
      <a href="https://gajuiitg.github.io/Profile/">Clickable here</a>
      </footer>
  </div>
  </div><!-- /densityMode -->

  <div id="jtMode" style="display:none;">
    <div class="grid">
      <!-- LEFT: INPUTS -->
      <div>
        <div class="panel">
          <h2>Inlet / Outlet Conditions</h2>
          <div class="row2">
            <div>
              <label>Inlet Temperature, T1</label>
              <input type="number" id="jT1Val" value="25" step="any">
            </div>
            <div>
              <label>Unit</label>
              <select id="jT1Unit">
                <option value="C" selected>&deg;C</option>
                <option value="K">K</option>
                <option value="F">&deg;F</option>
              </select>
            </div>
          </div>
          <div class="row2">
            <div>
              <label>Inlet Pressure, P1</label>
              <input type="number" id="jP1Val" value="20" step="any">
            </div>
            <div>
              <label>Unit</label>
              <select id="jP1Unit">
                <option value="atm">atm</option>
                <option value="bar" selected>bar</option>
                <option value="barg">barg</option>
                <option value="kPa">kPa</option>
                <option value="kgcm2g">kg/cm&sup2;g</option>
                <option value="psi">psia</option>
              </select>
            </div>
          </div>
          <div class="row2">
            <div>
              <label>Outlet Pressure, P2</label>
              <input type="number" id="jP2Val" value="5" step="any">
            </div>
            <div>
              <label>Unit</label>
              <select id="jP2Unit">
                <option value="atm">atm</option>
                <option value="bar" selected>bar</option>
                <option value="barg">barg</option>
                <option value="kPa">kPa</option>
                <option value="kgcm2g">kg/cm&sup2;g</option>
                <option value="psi">psia</option>
              </select>
            </div>
          </div>
          <div class="footer-note" style="margin-top:14px;">
            Adiabatic, isenthalpic (H<sub>1</sub>=H<sub>2</sub>) pressure reduction — e.g. across a control
            valve or PRV. P2 must be less than P1. Solves for outlet T2 such that real-gas enthalpy
            (PR EOS departure + ideal-gas Cp integral) is conserved.
          </div>
        </div>

        <div class="panel">
          <h2>Feed Composition</h2>
          <div class="phase-toggle">
            <button id="jBasisMol" class="active" onclick="setBasis('j','mol')">MOL %</button>
            <button id="jBasisWt" onclick="setBasis('j','wt')">WT %</button>
          </div>
          <table class="comp-table" id="jCompTable">
            <thead><tr><th></th><th>Component</th><th id="jCompColHdr">z<sub>i</sub></th></tr></thead>
            <tbody></tbody>
          </table>
          <div class="comp-sum" id="jCompSum">Sum: 1.0000</div>
          <div class="footer-note" style="margin-top:6px;">Tick a component to include it in the feed. Newly ticked components start at 0 &mdash; enter a value.</div>
        </div>

        <button class="calc" onclick="runJT()">CALCULATE T2</button>
        <div class="warn" id="jWarnBox"></div>
      </div>

      <!-- RIGHT: RESULTS -->
      <div>
        <div class="panel" id="jResultsPanel">
          <h2>Results</h2>
          <div class="placeholder">Enter conditions and feed composition, then click Calculate T2.</div>
        </div>
      </div>
    </div>

    <div class="footer-note">
      <strong>Method:</strong> (1) Flash the feed at (T1,P1) via PR-EOS fugacities to get inlet molar
      enthalpy H1 = ideal-gas Cp integral + phase-fraction-weighted PR departure function. (2) Search T2 at
      P2 by bisection until H(T2,P2) = H1. For a <strong>pure component</strong>, phase change at fixed P
      happens at a single saturation temperature (a true latent-heat jump in H, not a smooth kink) — so if
      H1 falls between the saturated-liquid and saturated-vapor enthalpies at T<sub>sat</sub>(P2), the
      outlet is exactly at T<sub>sat</sub>(P2) with vapor fraction from an enthalpy lever-rule balance,
      rather than from a naive continuous T-search (which would straddle the discontinuity incorrectly).
      For a <strong>mixture</strong>, the two-phase region spans a continuous range of T at fixed P, so
      direct bisection on T finds the two-phase solution directly.
      <br><br>
      For extended-set pure components without a loaded Antoine correlation, the saturation-temperature
      clamp at T<sub>sat</sub>(P2) is skipped and the solver goes straight to bisection on T &mdash; this
      is fine away from a phase change, but can be less precise exactly at one.
       <footer class="no-print">
      <h3>Developer Information</h3>
      <p><strong>Gajanand Yadav</strong></p>
      <p>Chemical Engineer</p>
      <p>Email: <a href="mailto:gajanandiitg@gmail.com">gajanandiitg@gmail.com</a>
      <p><a href="https://www.linkedin.com/in/gajanand-yadav-512624a5/" target="_blank">LinkedIn</a></p>
      Mobile: <a href="tel:+918369354472">+91-8369354472</a></p>
      <p>For Back to Profile </p> 
      <a href="https://gajuiitg.github.io/Profile/">Clickable here</a>
      </footer>
    </div>
  </div><!-- /jtMode -->

  <div id="cvMode" style="display:none;">
    <div class="grid">
      <!-- LEFT: INPUTS -->
      <div>
        <div class="panel">
          <h2>Reference Conditions (volumetric basis)</h2>
          <label>Reference Temperature</label>
          <select id="cvTref">
            <option value="0">0 &deg;C (Nm&sup3;, normal conditions)</option>
            <option value="15" selected>15 &deg;C (Sm&sup3;, GPA/typical standard)</option>
            <option value="15.56">15.56 &deg;C (60 &deg;F)</option>
            <option value="20">20 &deg;C</option>
            <option value="25">25 &deg;C</option>
          </select>
          <div class="footer-note" style="margin-top:14px;">
            Molar and mass-basis calorific values don't depend on this choice. Reference pressure fixed at
            1 atm (101.325 kPa). Volumetric conversion uses the ideal-gas law — a simplified version of the
            real-gas compressibility (summation-factor) correction in full ISO 6976 / GPA 2172; adequate for
            typical fuel-gas heating value estimates but not for custody-transfer-grade certification.
          </div>
        </div>

        <div class="panel">
          <h2>Composition</h2>
          <div class="phase-toggle">
            <button id="cvBasisMol" class="active" onclick="setBasis('cv','mol')">MOL %</button>
            <button id="cvBasisWt" onclick="setBasis('cv','wt')">WT %</button>
          </div>
          <table class="comp-table" id="cvCompTable">
            <thead><tr><th></th><th>Component</th><th id="cvCompColHdr">z<sub>i</sub></th></tr></thead>
            <tbody></tbody>
          </table>
          <div class="comp-sum" id="cvCompSum">Sum: 1.0000</div>
          <div class="footer-note" style="margin-top:6px;">Tick a component to include it in the mixture. Newly ticked components start at 0 &mdash; enter a value.</div>
        </div>

        <button class="calc" onclick="runCV()">CALCULATE</button>
        <div class="warn" id="cvWarnBox"></div>
      </div>

      <!-- RIGHT: RESULTS -->
      <div>
        <div class="panel" id="cvResultsPanel">
          <h2>Results</h2>
          <div class="placeholder">Enter composition, then click Calculate.</div>
        </div>
      </div>
    </div>

    <div class="footer-note">
      <strong>Method:</strong> Molar GCV/NCV = &Sigma; z<sub>i</sub>&middot;(GCV or NCV)<sub>i</sub>, using
      standard ideal-gas heats of combustion at 25&deg;C (GPA 2145 / ISO 6976-consistent values; product
      water liquid for GCV/gross/HHV, vapor for NCV/net/LHV). Mass basis divides by mixture MW. Volumetric
      basis divides by the ideal-gas molar volume at the selected reference conditions. Specific gravity is
      mixture MW over dry-air MW (28.9647 g/mol); Wobbe Index = volumetric CV / &radic;(specific gravity).
      Oxygen, Nitrogen, and Water are treated as inert (zero heating value) — they dilute the mixture but
      don't consume heat in this convention.
      <br><br>
      Extended-set heats of combustion (butadiene, butane, C5H10, benzene, toluene, hexane, methanol, VCM,
      EDC, EO, EG) are approximate literature values; HCl and Chlorine are treated as inert (zero heating
      value) since they don't combust. Chlorinated species form HCl on combustion rather than only CO2/H2O,
      so treat their listed values as indicative only &mdash; verify before fiscal/custody use.
       <footer class="no-print">
      <h3>Developer Information</h3>
      <p><strong>Gajanand Yadav</strong></p>
      <p>Chemical Engineer</p>
      <p>Email: <a href="mailto:gajanandiitg@gmail.com">gajanandiitg@gmail.com</a>
      <p><a href="https://www.linkedin.com/in/gajanand-yadav-512624a5/" target="_blank">LinkedIn</a></p>
      Mobile: <a href="tel:+918369354472">+91-8369354472</a></p>
      <p>For Back to Profile </p> 
      <a href="https://gajuiitg.github.io/Profile/">Clickable here</a>
      </footer>
    </div>
  </div><!-- /cvMode -->

  <div id="mixMode" style="display:none;">
  <div class="grid">
    <!-- LEFT: INPUTS -->
    <div>
      <div class="panel">
        <h2>Stream 1 &mdash; Conditions</h2>
        <div class="row2">
          <div>
            <label>Temperature</label>
            <input type="number" id="mix1TempVal" value="40" step="any">
          </div>
          <div>
            <label>Unit</label>
            <select id="mix1TempUnit">
              <option value="C" selected>&deg;C</option>
              <option value="K">K</option>
              <option value="F">&deg;F</option>
            </select>
          </div>
        </div>
        <div class="row2">
          <div>
            <label>Pressure</label>
            <input type="number" id="mix1PresVal" value="20" step="any">
          </div>
          <div>
            <label>Unit</label>
            <select id="mix1PresUnit">
              <option value="atm">atm</option>
              <option value="bar" selected>bar</option>
              <option value="barg">barg</option>
              <option value="kPa">kPa</option>
              <option value="kgcm2g">kg/cm&sup2;g</option>
              <option value="psi">psia</option>
            </select>
          </div>
        </div>
        <label>Phase (declared inlet state)</label>
        <div class="phase-toggle">
          <button id="mix1PhaseVapor" class="active" onclick="setStreamPhase(1,'vapor')">VAPOR</button>
          <button id="mix1PhaseLiquid" onclick="setStreamPhase(1,'liquid')">LIQUID</button>
        </div>
        <div class="row2">
          <div>
            <label>Flow rate</label>
            <input type="number" id="mix1FlowVal" value="100" step="any" min="0">
          </div>
          <div>
            <label>Unit</label>
            <select id="mix1FlowUnit">
              <option value="kmolh" selected>kmol/h</option>
              <option value="kgh">kg/h</option>
            </select>
          </div>
        </div>
      </div>

      <div class="panel">
        <h2>Stream 1 &mdash; Composition</h2>
        <div class="phase-toggle">
          <button id="mix1BasisMol" class="active" onclick="setBasis('mix1','mol')">MOL %</button>
          <button id="mix1BasisWt" onclick="setBasis('mix1','wt')">WT %</button>
        </div>
        <table class="comp-table" id="mix1CompTable">
          <thead><tr><th></th><th>Component</th><th id="mix1CompColHdr">z<sub>i</sub></th></tr></thead>
          <tbody></tbody>
        </table>
        <div class="comp-sum" id="mix1CompSum">Sum: 1.0000</div>
        <div class="footer-note" style="margin-top:6px;">Tick a component to include it in Stream 1.</div>
      </div>

      <div class="panel">
        <h2>Stream 2 &mdash; Conditions</h2>
        <div class="row2">
          <div>
            <label>Temperature</label>
            <input type="number" id="mix2TempVal" value="25" step="any">
          </div>
          <div>
            <label>Unit</label>
            <select id="mix2TempUnit">
              <option value="C" selected>&deg;C</option>
              <option value="K">K</option>
              <option value="F">&deg;F</option>
            </select>
          </div>
        </div>
        <div class="row2">
          <div>
            <label>Pressure</label>
            <input type="number" id="mix2PresVal" value="20" step="any">
          </div>
          <div>
            <label>Unit</label>
            <select id="mix2PresUnit">
              <option value="atm">atm</option>
              <option value="bar" selected>bar</option>
              <option value="barg">barg</option>
              <option value="kPa">kPa</option>
              <option value="kgcm2g">kg/cm&sup2;g</option>
              <option value="psi">psia</option>
            </select>
          </div>
        </div>
        <label>Phase (declared inlet state)</label>
        <div class="phase-toggle">
          <button id="mix2PhaseVapor" onclick="setStreamPhase(2,'vapor')">VAPOR</button>
          <button id="mix2PhaseLiquid" class="active" onclick="setStreamPhase(2,'liquid')">LIQUID</button>
        </div>
        <div class="row2">
          <div>
            <label>Flow rate</label>
            <input type="number" id="mix2FlowVal" value="20" step="any" min="0">
          </div>
          <div>
            <label>Unit</label>
            <select id="mix2FlowUnit">
              <option value="kmolh" selected>kmol/h</option>
              <option value="kgh">kg/h</option>
            </select>
          </div>
        </div>
      </div>

      <div class="panel">
        <h2>Stream 2 &mdash; Composition</h2>
        <div class="phase-toggle">
          <button id="mix2BasisMol" class="active" onclick="setBasis('mix2','mol')">MOL %</button>
          <button id="mix2BasisWt" onclick="setBasis('mix2','wt')">WT %</button>
        </div>
        <table class="comp-table" id="mix2CompTable">
          <thead><tr><th></th><th>Component</th><th id="mix2CompColHdr">z<sub>i</sub></th></tr></thead>
          <tbody></tbody>
        </table>
        <div class="comp-sum" id="mix2CompSum">Sum: 1.0000</div>
        <div class="footer-note" style="margin-top:6px;">Tick a component to include it in Stream 2.</div>
      </div>

      <div class="panel">
        <h2>Mixed Outlet &mdash; Pressure</h2>
        <div class="row2">
          <div>
            <label>Final (mixed) pressure</label>
            <input type="number" id="mixPfVal" value="17.5" step="any">
          </div>
          <div>
            <label>Unit</label>
            <select id="mixPfUnit">
              <option value="atm">atm</option>
              <option value="bar">bar</option>
              <option value="barg">barg</option>
              <option value="kPa">kPa</option>
              <option value="kgcm2g" selected>kg/cm&sup2;g</option>
              <option value="psi">psia</option>
            </select>
          </div>
        </div>
        <div class="footer-note" style="margin-top:6px;">
          Outlet temperature is solved from an adiabatic, steady-state energy balance
          (F<sub>1</sub>H<sub>1</sub>+F<sub>2</sub>H<sub>2</sub>=F<sub>total</sub>H<sub>mix</sub>) at this pressure &mdash;
          it is not an input.
        </div>
      </div>

      <button class="calc" onclick="runMix()">CALCULATE MIX</button>
      <div class="warn" id="mixWarnBox"></div>
    </div>

    <!-- RIGHT: RESULTS -->
    <div>
      <div class="panel" id="mixResultsPanel">
        <h2>Results</h2>
        <div class="placeholder">Enter both streams' conditions and composition, then click Calculate Mix.</div>
      </div>
    </div>
  </div>

  <div class="footer-note">
    <strong>Method:</strong> each inlet stream's molar enthalpy is evaluated at its own T, P, and
    <em>declared</em> phase (ideal-gas Cp&deg; integral + PR-EOS departure, same convention as the
    Density &amp; Cp tab). The two streams are combined on a molar basis into a single feed composition,
    and the outlet temperature at the specified final pressure is found by solving the steady-state,
    adiabatic energy balance F<sub>1</sub>H<sub>1</sub> + F<sub>2</sub>H<sub>2</sub> = F<sub>total</sub>&middot;H<sub>mix</sub>(T,P<sub>f</sub>).
    No heat loss, no shaft work, and no pressure-drop-induced flashing beyond what the energy balance itself
    predicts are assumed (a real tee/header may lose heat to ambient or have a different pressure profile).
    <br><br>
    The outlet phase (vapor / liquid / two-phase) is <em>not</em> assumed &mdash; it is determined
    rigorously from a PT flash (Rachford-Rice + PR fugacity coefficients) on the combined composition
    at the solved temperature and specified pressure, exactly as in the Isenthalpic (JT) tab. If the
    result is two-phase, vapor and liquid density/Cp are reported separately in addition to the
    flow-weighted apparent values.
     <footer class="no-print">
      <h3>Developer Information</h3>
      <p><strong>Gajanand Yadav</strong></p>
      <p>Chemical Engineer</p>
      <p>Email: <a href="mailto:gajanandiitg@gmail.com">gajanandiitg@gmail.com</a>
      <p><a href="https://www.linkedin.com/in/gajanand-yadav-512624a5/" target="_blank">LinkedIn</a></p>
      Mobile: <a href="tel:+918369354472">+91-8369354472</a></p>
      <p>For Back to Profile </p> 
      <a href="https://gajuiitg.github.io/Profile/">Clickable here</a>
      </footer>
  </div>
  </div><!-- /mixMode -->
</main>

<script>
// ============================================================
// Peng-Robinson EOS engine (mirrors pr_core.py logic)
// ============================================================
const R = 8.314462618; // J/mol.K

const COMPONENTS = {
  Methane:   {Tc:190.56, Pc:4599000, omega:0.0115, MW:16.043},
  Ethane:    {Tc:305.32, Pc:4872000, omega:0.0995, MW:30.070},
  Ethylene:  {Tc:282.34, Pc:5041000, omega:0.0866, MW:28.054},
  Propane:   {Tc:369.83, Pc:4248000, omega:0.1523, MW:44.097},
  Propylene: {Tc:364.85, Pc:4600000, omega:0.1424, MW:42.081},
  Oxygen:    {Tc:154.581, Pc:5043000, omega:0.0222, MW:31.999},
  Nitrogen:  {Tc:126.192, Pc:3395800, omega:0.0372, MW:28.013},
  Hydrogen:  {Tc:33.145, Pc:1296400, omega:-0.2190, MW:2.016},
  Water:     {Tc:647.096, Pc:22064000, omega:0.3443, MW:18.015},
  "Carbon Dioxide (CO2)":      {Tc:304.13, Pc:7377000, omega:0.2239, MW:44.010},
  // --- Extended set (literature-typical critical properties; verify against
  // DIPPR/NIST/simulator databank before safety-critical or custody use) ---
  "1,3-Butadiene":              {Tc:425.0,  Pc:4330000, omega:0.195, MW:54.092},
  "n-Butane":                   {Tc:425.12, Pc:3796000, omega:0.200, MW:58.122},
  "C5H10 (1-Pentene)":          {Tc:464.7,  Pc:3529000, omega:0.245, MW:70.135},
  "Benzene":                    {Tc:562.05, Pc:4895000, omega:0.212, MW:78.114},
  "Toluene":                    {Tc:591.75, Pc:4108000, omega:0.264, MW:92.141},
  "Vinyl Chloride (VCM)":       {Tc:432.0,  Pc:5600000, omega:0.122, MW:62.499},
  "1,2-Dichloroethane (EDC)":   {Tc:561.6,  Pc:5400000, omega:0.269, MW:98.959},
  "Hydrogen Chloride (HCl)":    {Tc:324.65, Pc:8310000, omega:0.132, MW:36.461},
  "Chlorine":                   {Tc:417.15, Pc:7710000, omega:0.069, MW:70.906},
  "Ethylene Oxide (EO)":        {Tc:469.15, Pc:7190000, omega:0.202, MW:44.053},
  "Ethylene Glycol (EG)":       {Tc:719.7,  Pc:7700000, omega:0.500, MW:62.068},
  "n-Hexane":                   {Tc:507.6,  Pc:3025000, omega:0.301, MW:86.178},
  "Methanol":                   {Tc:512.6,  Pc:8084000, omega:0.565, MW:32.042}
};

const CP0 = {
  Methane:   {A:19.251, B:5.213e-2,  C:1.197e-5,  D:-1.132e-8},
  Ethane:    {A:5.409,  B:1.781e-1,  C:-6.938e-5, D:8.713e-9},
  Ethylene:  {A:3.806,  B:1.566e-1,  C:-8.348e-5, D:1.755e-8},
  Propane:   {A:-4.224, B:3.063e-1,  C:-1.586e-4, D:3.215e-8},
  Propylene: {A:3.710,  B:2.345e-1,  C:-1.160e-4, D:2.205e-8},
  Oxygen:    {A:29.6213, B:-8.120003e-03, C:3.058886e-05,  D:-1.737182e-08},
  Nitrogen:  {A:30.0153, B:-7.765822e-03, C:1.744816e-05,  D:-6.961427e-09},
  Hydrogen:  {A:18.3001, B:6.847923e-02,  C:-1.393455e-04, D:9.250750e-08},
  Water:     {A:33.6739, B:-6.446044e-03, C:2.402575e-05,  D:-1.004486e-08},
  "Carbon Dioxide (CO2)": {A:19.795, B:7.343e-02, C:-5.602e-05, D:1.715e-08},
  // --- Extended set: simple 2-parameter (linear) fits to literature ideal-gas
  // Cp at ~298K/600K (C=D=0). Adequate for typical process-range estimates;
  // verify against DIPPR/NIST for precision work outside ~250-600 K. ---
  "1,3-Butadiene":            {A:12.9, B:0.2235, C:0, D:0},
  "n-Butane":                 {A:26.0, B:0.2400, C:0, D:0},
  "C5H10 (1-Pentene)":        {A:36.1, B:0.2815, C:0, D:0},
  "Benzene":                  {A:3.8,  B:0.2636, C:0, D:0},
  "Toluene":                  {A:15.4, B:0.2960, C:0, D:0},
  "Vinyl Chloride (VCM)":     {A:30.3, B:0.0762, C:0, D:0},
  "1,2-Dichloroethane (EDC)": {A:48.4, B:0.0993, C:0, D:0},
  "Hydrogen Chloride (HCl)":  {A:28.6, B:0.00166,C:0, D:0},
  "Chlorine":                 {A:31.2, B:0.00894,C:0, D:0},
  "Ethylene Oxide (EO)":      {A:11.5, B:0.1225, C:0, D:0},
  "Ethylene Glycol (EG)":     {A:31.0, B:0.2483, C:0, D:0},
  "n-Hexane":                 {A:35.3, B:0.3645, C:0, D:0},
  "Methanol":                 {A:12.6, B:0.1056, C:0, D:0}
};

const COMP_GROUPS = [
  {label:"Light Gases (C1\u2013C3)", items:["Methane","Ethane","Ethylene","Propane","Propylene"]},
  {label:"Inerts / Utility Gases",   items:["Oxygen","Nitrogen","Hydrogen","Water","Carbon Dioxide (CO2)"]},
  {label:"C4\u2013C6 Hydrocarbons",  items:["1,3-Butadiene","n-Butane","C5H10 (1-Pentene)","n-Hexane"]},
  {label:"Aromatics",                items:["Benzene","Toluene"]},
  {label:"Oxygenates",               items:["Methanol","Ethylene Oxide (EO)","Ethylene Glycol (EG)"]},
  {label:"Chlorinated / Acid Gas",   items:["Vinyl Chloride (VCM)","1,2-Dichloroethane (EDC)","Hydrogen Chloride (HCl)","Chlorine"]}
];
const ORDER = COMP_GROUPS.flatMap(g=>g.items);
const ORIGINAL_NINE = ["Methane","Ethane","Ethylene","Propane","Propylene","Oxygen","Nitrogen","Hydrogen","Water"];

const KIJ = {
  "Methane|Ethane": -0.0026, "Methane|Ethylene": 0.0100, "Methane|Propane": 0.0140,
  "Methane|Propylene": 0.0090, "Ethane|Ethylene": 0.0030, "Ethane|Propane": 0.0011,
  "Ethane|Propylene": 0.0080, "Ethylene|Propane": 0.0080, "Ethylene|Propylene": 0.0020,
  "Propane|Propylene": 0.0030,
  "Nitrogen|Methane": 0.0311, "Nitrogen|Ethane": 0.0515, "Nitrogen|Ethylene": 0.0800,
  "Nitrogen|Propane": 0.0852, "Nitrogen|Propylene": 0.0800,
  "Oxygen|Methane": 0.0311, "Oxygen|Ethane": 0.0515, "Oxygen|Ethylene": 0.0800,
  "Oxygen|Propane": 0.0852, "Oxygen|Propylene": 0.0800,
  "Hydrogen|Methane": 0.0263, "Hydrogen|Ethane": 0.0463, "Hydrogen|Ethylene": 0.0500,
  "Hydrogen|Propane": 0.0533, "Hydrogen|Propylene": 0.0500,
  "Water|Methane": 0.4900, "Water|Ethane": 0.4800, "Water|Ethylene": 0.4800,
  "Water|Propane": 0.5000, "Water|Propylene": 0.4800,
  "Nitrogen|Oxygen": -0.0119, "Nitrogen|Hydrogen": 0.1030, "Nitrogen|Water": 0.3200,
  "Oxygen|Hydrogen": 0.1030, "Oxygen|Water": 0.3000, "Hydrogen|Water": -0.2000
};

function getKij(i,j){
  if(i===j) return 0;
  return (KIJ[i+"|"+j] !== undefined) ? KIJ[i+"|"+j] : (KIJ[j+"|"+i] !== undefined ? KIJ[j+"|"+i] : 0);
}

function prParams(comp){
  const d = COMPONENTS[comp];
  const ac = 0.45724 * R*R * d.Tc*d.Tc / d.Pc;
  const b = 0.07780 * R * d.Tc / d.Pc;
  let kappa;
  if(d.omega <= 0.491){
    kappa = 0.37464 + 1.54226*d.omega - 0.26992*d.omega*d.omega;
  } else {
    kappa = 0.379642 + 1.48503*d.omega - 0.164423*d.omega**2 + 0.016666*d.omega**3;
  }
  return {ac, b, kappa, Tc:d.Tc};
}

function aOfT(comp, T){
  const p = prParams(comp);
  const alpha = Math.pow(1 + p.kappa*(1 - Math.sqrt(T/p.Tc)), 2);
  return {a: p.ac*alpha, b: p.b};
}

function mixtureAmBm(comps, z, T){
  const n = comps.length;
  const a_i = [], b_i = [];
  for(let i=0;i<n;i++){
    const r = aOfT(comps[i], T);
    a_i.push(r.a); b_i.push(r.b);
  }
  let bm = 0;
  for(let i=0;i<n;i++) bm += z[i]*b_i[i];
  let am = 0;
  for(let i=0;i<n;i++){
    for(let j=0;j<n;j++){
      const k = getKij(comps[i], comps[j]);
      const aij = Math.sqrt(a_i[i]*a_i[j])*(1-k);
      am += z[i]*z[j]*aij;
    }
  }
  return {am, bm, a_i, b_i};
}

// Solve cubic Z^3 + c2 Z^2 + c1 Z + c0 = 0 via Cardano/trig method
function solveCubic(c2, c1, c0){
  const a = c2, b = c1, c = c0;
  const p = b - a*a/3;
  const q = 2*a*a*a/27 - a*b/3 + c;
  const roots = [];
  const disc = (q*q)/4 + (p*p*p)/27;
  if(disc > 0){
    const sq = Math.sqrt(disc);
    const u = Math.cbrt(-q/2 + sq);
    const v = Math.cbrt(-q/2 - sq);
    roots.push(u + v - a/3);
  } else {
    const r = Math.sqrt(-p*p*p/27);
    const phi = Math.acos(Math.max(-1,Math.min(1, -q/(2*r))));
    const m = 2*Math.sqrt(-p/3);
    roots.push(m*Math.cos(phi/3) - a/3);
    roots.push(m*Math.cos((phi+2*Math.PI)/3) - a/3);
    roots.push(m*Math.cos((phi+4*Math.PI)/3) - a/3);
  }
  return roots;
}

function densityAndZ(comps, z, T, P, phase){
  const {am, bm} = mixtureAmBm(comps, z, T);
  const A = am*P/(R*T)**2;
  const B = bm*P/(R*T);
  const c2 = -(1-B);
  const c1 = A - 3*B*B - 2*B;
  const c0 = -(A*B - B*B - B*B*B);
  let roots = solveCubic(c2, c1, c0).filter(r => r > B && isFinite(r));
  roots.sort((a,b)=>a-b);
  if(roots.length === 0) throw new Error("No valid real root — check conditions (may be supercritical / out of range).");
  const Z = (phase === "vapor") ? roots[roots.length-1] : roots[0];
  const V = Z*R*T/P; // m3/mol
  let MW = 0;
  for(let i=0;i<comps.length;i++) MW += z[i]*COMPONENTS[comps[i]].MW;
  const rho = (MW/1000)/V;
  return {Z, V, rho, MW, roots, am, bm};
}

function cpIdealMix(comps, z, T){
  let cp0 = 0;
  for(let i=0;i<comps.length;i++){
    const d = CP0[comps[i]];
    cp0 += z[i]*(d.A + d.B*T + d.C*T*T + d.D*T*T*T);
  }
  return cp0;
}

function cpDeparture(comps, z, T, P, phase){
  const sqrt2 = Math.SQRT2;
  const res = densityAndZ(comps, z, T, P, phase);
  const V = res.V, bm = res.bm;
  const dT = 0.1;
  const am0 = mixtureAmBm(comps, z, T).am;
  const amP = mixtureAmBm(comps, z, T+dT).am;
  const amM = mixtureAmBm(comps, z, T-dT).am;
  const damdT = (amP - amM)/(2*dT);
  const d2amdT2 = (amP - 2*am0 + amM)/(dT*dT);

  const b = bm;
  const lnTerm = Math.log((V + (1+sqrt2)*b)/(V + (1-sqrt2)*b));
  const CvRes = (T*d2amdT2)/(2*sqrt2*b) * lnTerm;

  const dPdT_V = R/(V-b) - damdT/(V*V + 2*b*V - b*b);
  const dPdV_T = -R*T/((V-b)*(V-b)) + am0*(2*V+2*b)/Math.pow(V*V+2*b*V-b*b, 2);

  const CpRes = CvRes - R + (T*dPdT_V*dPdT_V)/(-dPdV_T);
  const Cp0 = cpIdealMix(comps, z, T);
  const Cp_real = Cp0 + CpRes;
  const Cv_real = (Cp0 - R) + CvRes; // Cv0 = Cp0 - R for an ideal gas, plus the real-gas Cv departure
  const k = Cp_real / Cv_real; // heat capacity ratio, k = Cp/Cv
  return {Cp_ideal: Cp0, Cp_departure: CpRes, Cp_real, Cv_real, k, res};
}

// ============================================================
// UI wiring
// ============================================================
let currentPhase = "vapor";
const basisState = {d: "mol", j: "mol", cv: "mol", mix1: "mol", mix2: "mol"};
const mixPhaseState = {1: "vapor", 2: "liquid"};

function setStreamPhase(n, p){
  mixPhaseState[n] = p;
  document.getElementById("mix"+n+"PhaseVapor").classList.toggle("active", p==="vapor");
  document.getElementById("mix"+n+"PhaseLiquid").classList.toggle("active", p==="liquid");
}

function setBasis(tab, basis){
  basisState[tab] = basis;
  const molBtn = document.getElementById(tab+"BasisMol");
  const wtBtn = document.getElementById(tab+"BasisWt");
  molBtn.classList.toggle("active", basis==="mol");
  wtBtn.classList.toggle("active", basis==="wt");
  const hdr = document.getElementById(tab+"CompColHdr");
  hdr.innerHTML = (basis==="mol") ? "z<sub>i</sub>" : "w<sub>i</sub>";
}

function wtToMol(comps, wtFractions){
  // Convert weight fractions to mole fractions: mol_i proportional to w_i/MW_i, then normalize.
  const raw = comps.map((c,i)=> wtFractions[i]/COMPONENTS[c].MW);
  const sum = raw.reduce((a,b)=>a+b,0);
  return raw.map(v=>v/sum);
}

// ============================================================
// Shared toggle-aware composition table builder (density/JT/CV tabs)
// ============================================================
function buildToggleCompTable(tableId, defaults, sumFnName){
  const tbody = document.querySelector("#"+tableId+" tbody");
  tbody.innerHTML = "";
  COMP_GROUPS.forEach(g=>{
    const trh = document.createElement("tr");
    trh.innerHTML = `<td class="group-hdr" colspan="3">${g.label}</td>`;
    tbody.appendChild(trh);
    g.items.forEach(name=>{
      const checked = ORIGINAL_NINE.includes(name);
      const val = defaults[name] !== undefined ? defaults[name] : 0;
      const tr = document.createElement("tr");
      tr.innerHTML =
        `<td class="chk-col"><input type="checkbox" class="comp-check" data-comp="${name}" ${checked?'checked':''} onchange="onCompToggle(this,'${sumFnName}')"></td>` +
        `<td class="name-col">${name}</td>` +
        `<td><input type="number" step="0.0001" min="0" max="1" value="${val}" data-comp="${name}" oninput="${sumFnName}()" ${checked?'':'disabled'}></td>`;
      tbody.appendChild(tr);
    });
  });
  window[sumFnName]();
}

function onCompToggle(cb, sumFnName){
  const tr = cb.closest("tr");
  const numInput = tr.querySelector("input[type=number]");
  numInput.disabled = !cb.checked;
  window[sumFnName]();
}

function sumToggleTable(tableId, sumElId){
  let sum = 0;
  document.querySelectorAll("#"+tableId+" tbody tr").forEach(tr=>{
    const cb = tr.querySelector("input[type=checkbox]");
    if(!cb || !cb.checked) return;
    sum += parseFloat(tr.querySelector("input[type=number]").value)||0;
  });
  const el = document.getElementById(sumElId);
  el.textContent = "Sum: " + sum.toFixed(4);
  el.className = "comp-sum" + (Math.abs(sum-1)>0.0005 ? " err" : "");
  return sum;
}

function collectActiveComps(tableId){
  const comps = [], z = [];
  let sum = 0;
  document.querySelectorAll("#"+tableId+" tbody tr").forEach(tr=>{
    const cb = tr.querySelector("input[type=checkbox]");
    if(!cb || !cb.checked) return;
    const inp = tr.querySelector("input[type=number]");
    const v = parseFloat(inp.value)||0;
    sum += v;
    if(v > 0){ comps.push(inp.dataset.comp); z.push(v); }
  });
  return {comps, z, sum};
}

function buildCompTable(){
  const defaults = {Methane:0.20, Ethane:0.20, Ethylene:0.20, Propane:0.20, Propylene:0.20};
  buildToggleCompTable("compTable", defaults, "updateSum");
}

function updateSum(){
  return sumToggleTable("compTable", "compSum");
}

function setPhase(p){
  currentPhase = p;
  document.getElementById("btnVapor").classList.toggle("active", p==="vapor");
  document.getElementById("btnLiquid").classList.toggle("active", p==="liquid");
}

function toKelvin(val, unit){
  if(unit==="K") return val;
  if(unit==="C") return val+273.15;
  if(unit==="F") return (val-32)*5/9+273.15;
}
function toPascal(val, unit){
  if(unit==="atm") return val*101325;
  if(unit==="bar") return val*100000;
  if(unit==="barg") return (val+1.01325)*100000;
  if(unit==="kPa") return val*1000;
  if(unit==="kgcm2g") return (val*98066.5)+101325;
  if(unit==="psi") return val*6894.757;
}

function runCalc(){
  const warnBox = document.getElementById("warnBox");
  warnBox.className = "warn"; warnBox.textContent = "";
  try{
    const tVal = parseFloat(document.getElementById("tempVal").value);
    const tUnit = document.getElementById("tempUnit").value;
    const pVal = parseFloat(document.getElementById("presVal").value);
    const pUnit = document.getElementById("presUnit").value;
    const T = toKelvin(tVal, tUnit);
    const P = toPascal(pVal, pUnit);

    if(T <= 0 || P <= 0) throw new Error("Temperature and pressure must be positive (absolute).");

    let {comps, z, sum} = collectActiveComps("compTable");
    if(comps.length===0) throw new Error("Tick at least one component and enter a non-zero mole fraction.");
    if(Math.abs(sum-1) > 0.0005){
      // normalize but warn
      z = z.map(v=>v/sum);
      warnBox.textContent = `Note: composition summed to ${sum.toFixed(4)}, auto-normalized to 1.0000.`;
      warnBox.classList.add("show");
    }
    if(basisState.d === "wt"){
      z = wtToMol(comps, z);
      warnBox.textContent += (warnBox.textContent? " " : "") + "Note: input interpreted as wt% and converted to mole fractions for calculation.";
      warnBox.classList.add("show");
    }

    const dz = densityAndZ(comps, z, T, P, currentPhase);
    const cp = cpDeparture(comps, z, T, P, currentPhase);

    // Saturation temperature at input P (pure component only, via Antoine equation)
    let tsatInfo = null;
    if(comps.length === 1){
      const tsatK = tsatPure(comps[0], P);
      tsatInfo = (tsatK !== null) ? tsatK : "range";
    }

    // IBP/FBP for mixtures (bubble/dew point at input P)
    let ibpFbpInfo = null;
    if(comps.length >= 2){
      const ibp = bubblePointT(comps, z, P);
      const fbp = dewPointT(comps, z, P);
      ibpFbpInfo = {ibp, fbp};
    }

    // Flash point estimate (fire safety) - applies to both pure and mixture
    const fpInfo = flashPointEstimate(comps, z);

    // Reduced conditions warning (rough EOS validity check)
    let TcMix = 0; // simple mole-fraction average as rough guide only
    for(let i=0;i<comps.length;i++) TcMix += z[i]*COMPONENTS[comps[i]].Tc;
    if(T > 1.3*TcMix){
      warnBox.textContent += (warnBox.textContent? " " : "") + "Note: T is well above mixture pseudo-critical Tc — supercritical region, liquid root may not exist physically.";
      warnBox.classList.add("show");
    }

    renderResults(dz, cp, comps, z, T, P, tsatInfo, ibpFbpInfo, fpInfo);
  } catch(e){
    warnBox.textContent = "Error: " + e.message;
    warnBox.classList.add("show");
    document.getElementById("resultsPanel").innerHTML = '<h2>Results</h2><div class="placeholder">Calculation failed — see message above.</div>';
  }
}

function renderResults(dz, cp, comps, z, T, P, tsatInfo, ibpFbpInfo, fpInfo){
  const phaseLabel = currentPhase === "vapor" ? "Vapor" : "Liquid";
  const phaseClass = currentPhase;
  const compList = comps.map((c,i)=> `${c} (${(z[i]*100).toFixed(2)}%)`).join(", ");

  let tsatRow;
  if(tsatInfo === null){
    tsatRow = "";
  } else if(tsatInfo === "range"){
    tsatRow = `<tr><td>Saturation temperature at input P</td><td>N/A (outside Antoine correlation range, or no vapor-pressure correlation loaded yet for this component)</td></tr>`;
  } else {
    tsatRow = `<tr><td>Saturation temperature at input P (Antoine)</td><td>${(tsatInfo-273.15).toFixed(3)} &deg;C (${tsatInfo.toFixed(3)} K)</td></tr>`;
  }

  let ibpFbpRows = "";
  if(ibpFbpInfo !== null){
    const ibpStr = (ibpFbpInfo.ibp !== null) ? `${(ibpFbpInfo.ibp-273.15).toFixed(3)} &deg;C` : "N/A (no convergence in searched range)";
    const fbpStr = (ibpFbpInfo.fbp !== null) ? `${(ibpFbpInfo.fbp-273.15).toFixed(3)} &deg;C` : "N/A (no convergence in searched range)";
    ibpFbpRows = `
      <tr><td>Initial Boiling Point, IBP (bubble T @ input P)</td><td>${ibpStr}</td></tr>
      <tr><td>Final Boiling Point, FBP (dew T @ input P)</td><td>${fbpStr}</td></tr>`;
  }

  let fpRow = "";
  if(fpInfo.T_fp !== null){
    fpRow = `<tr><td>Flash Point (estimated, 1 atm)</td><td>${(fpInfo.T_fp-273.15).toFixed(2)} &deg;C</td></tr>`;
  } else {
    fpRow = `<tr><td>Flash Point (estimated, 1 atm)</td><td>N/A &mdash; ${fpInfo.status}</td></tr>`;
  }

  const html = `
    <h2>Results &mdash; ${phaseLabel} Phase</h2>
    <div class="results-grid">
      <div class="result-card ${phaseClass}">
        <div class="label">Density</div>
        <div class="value">${dz.rho.toFixed(3)}<span class="unit">kg/m&sup3;</span></div>
      </div>
      <div class="result-card ${phaseClass}">
        <div class="label">Real-Gas Cp</div>
        <div class="value">${cp.Cp_real.toFixed(3)}<span class="unit">J/mol&middot;K</span></div>
      </div>
      <div class="result-card ${phaseClass}">
        <div class="label">k = Cp/Cv</div>
        <div class="value">${cp.k.toFixed(4)}</div>
      </div>
    </div>
    <table class="detail-table">
      <tr><td>Compressibility factor, Z</td><td>${dz.Z.toFixed(6)}</td></tr>
      <tr><td>Molar volume</td><td>${(dz.V*1000).toFixed(4)} L/mol</td></tr>
      <tr><td>Mixture molecular weight</td><td>${dz.MW.toFixed(3)} g/mol</td></tr>
      <tr><td>Density (mass basis)</td><td>${dz.rho.toFixed(4)} kg/m&sup3;</td></tr>
      <tr><td>Density (molar basis)</td><td>${(1/dz.V).toFixed(3)} mol/m&sup3; &times; 10&sup3;... (${(1/dz.V/1000).toFixed(4)} kmol/m&sup3;)</td></tr>
      <tr><td>Ideal-gas Cp&deg;</td><td>${cp.Cp_ideal.toFixed(4)} J/mol&middot;K</td></tr>
      <tr><td>Cp departure (real &minus; ideal)</td><td>${cp.Cp_departure.toFixed(4)} J/mol&middot;K</td></tr>
      <tr><td>Real-gas Cp</td><td>${cp.Cp_real.toFixed(4)} J/mol&middot;K</td></tr>
      <tr><td>Specific Cp (mass basis)</td><td>${(cp.Cp_real/(dz.MW/1000)).toFixed(3)} J/kg&middot;K</td></tr>
      <tr><td>Real-gas Cv</td><td>${cp.Cv_real.toFixed(4)} J/mol&middot;K</td></tr>
      <tr><td>Specific Cv (mass basis)</td><td>${(cp.Cv_real/(dz.MW/1000)).toFixed(3)} J/kg&middot;K</td></tr>
      <tr><td>Heat capacity ratio, k = Cp/Cv</td><td>${cp.k.toFixed(4)}</td></tr>
      ${tsatRow}
      ${ibpFbpRows}
      ${fpRow}
      <tr><td>Temperature</td><td>${T.toFixed(2)} K (${(T-273.15).toFixed(2)} &deg;C)</td></tr>
      <tr><td>Pressure</td><td>${(P/100000).toFixed(4)} bar (${(P/101325).toFixed(4)} atm)</td></tr>
      <tr><td>Composition (mole basis)</td><td style="text-align:left; max-width:260px;">${compList}</td></tr>
      <tr><td>Real roots of cubic (Z)</td><td>${dz.roots.map(r=>r.toFixed(5)).join(" / ")}</td></tr>
    </table>
    ${exportToolbarHTML('resultsPanel','Density_Cp_Results')}
  `;
  document.getElementById("resultsPanel").innerHTML = html;
}

// ============================================================
// PT FLASH engine (Rachford-Rice + PR fugacity coefficients)
// ============================================================
function mixtureAmBmFull(comps, z, T){
  const n = comps.length;
  const a_i = [], b_i = [];
  for(let i=0;i<n;i++){ const r = aOfT(comps[i], T); a_i.push(r.a); b_i.push(r.b); }
  let bm = 0;
  for(let i=0;i<n;i++) bm += z[i]*b_i[i];
  let am = 0;
  const a_ij = [];
  for(let i=0;i<n;i++){
    a_ij.push([]);
    for(let j=0;j<n;j++){
      const k = getKij(comps[i], comps[j]);
      const aij = Math.sqrt(a_i[i]*a_i[j])*(1-k);
      a_ij[i].push(aij);
      am += z[i]*z[j]*aij;
    }
  }
  return {am, bm, a_i, b_i, a_ij};
}

function solveCubicZFull(A, B){
  const c2 = -(1-B), c1 = A - 3*B*B - 2*B, c0 = -(A*B - B*B - B*B*B);
  let roots = solveCubic(c2,c1,c0).filter(r => r > B && isFinite(r));
  roots.sort((a,b)=>a-b);
  return roots;
}

function fugacityCoeffs(comps, w, T, P, phase){
  const n = comps.length;
  const {am, bm, a_i, b_i, a_ij} = mixtureAmBmFull(comps, w, T);
  const A = am*P/(R*T)**2;
  const B = bm*P/(R*T);
  const roots = solveCubicZFull(A,B);
  if(roots.length===0) throw new Error("No real root — conditions out of valid EOS range.");
  const Z = (phase==="vapor") ? roots[roots.length-1] : roots[0];
  const sqrt2 = Math.SQRT2;
  const lnphi = [];
  for(let i=0;i<n;i++){
    let sumTerm = 0;
    for(let j=0;j<n;j++) sumTerm += w[j]*a_ij[i][j];
    const term1 = (b_i[i]/bm)*(Z-1);
    const term2 = -Math.log(Z-B);
    const term3 = -(A/(2*sqrt2*B))*(2*sumTerm/am - b_i[i]/bm);
    const term4 = Math.log((Z+(1+sqrt2)*B)/(Z+(1-sqrt2)*B));
    lnphi.push(term1+term2+term3*term4);
  }
  return {phi: lnphi.map(Math.exp), Z, A, B};
}

function wilsonK(comps, T, P){
  return comps.map(c=>{
    const d = COMPONENTS[c];
    return (d.Pc/P)*Math.exp(5.373*(1+d.omega)*(1-d.Tc/T));
  });
}

function rachfordRice(z, K, beta){
  let s=0;
  for(let i=0;i<z.length;i++) s += z[i]*(K[i]-1)/(1+beta*(K[i]-1));
  return s;
}

function solveRR(z, K){
  let lo=1e-10, hi=1-1e-10;
  let fLo = rachfordRice(z,K,lo), fHi = rachfordRice(z,K,hi);
  if(fLo<=0) return lo;
  if(fHi>=0) return hi;
  for(let it=0; it<200; it++){
    const mid = 0.5*(lo+hi);
    const fm = rachfordRice(z,K,mid);
    if(Math.abs(fm)<1e-12) return mid;
    if(fLo*fm<0){ hi=mid; } else { lo=mid; fLo=fm; }
  }
  return 0.5*(lo+hi);
}

function ptFlash(comps, zIn, T, P, maxIter=200, tol=1e-10){
  const sum = zIn.reduce((a,b)=>a+b,0);
  const z = zIn.map(v=>v/sum);
  let K = wilsonK(comps, T, P);
  let beta=0.5, x, y, Zl, Zv;
  let it;
  for(it=0; it<maxIter; it++){
    beta = solveRR(z, K);
    x = z.map((zi,i)=> zi/(1+beta*(K[i]-1)));
    const xsum = x.reduce((a,b)=>a+b,0);
    x = x.map(v=>v/xsum);
    y = x.map((xi,i)=> K[i]*xi);
    const ysum = y.reduce((a,b)=>a+b,0);
    y = y.map(v=>v/ysum);

    const rL = fugacityCoeffs(comps, x, T, P, "liquid");
    const rV = fugacityCoeffs(comps, y, T, P, "vapor");
    Zl = rL.Z; Zv = rV.Z;
    const Knew = rL.phi.map((pl,i)=> pl/rV.phi[i]);
    let err=0;
    for(let i=0;i<K.length;i++) err += (Knew[i]/K[i]-1)**2;
    K = Knew;
    if(err < tol){
      const sp = beta<1e-6 ? "liquid" : (beta>1-1e-6 ? "vapor" : null);
      return {beta, x, y, K, converged:true, iters:it+1, Zl, Zv, singlePhase:sp};
    }
  }
  const sp = beta<1e-6 ? "liquid" : (beta>1-1e-6 ? "vapor" : null);
  return {beta, x, y, K, converged:false, iters:maxIter, Zl, Zv, singlePhase:sp};
}

// ============================================================
// Flash UI wiring
// ============================================================
// ============================================================
// Print PDF / Save Results export utilities
// ============================================================
function printResults(panelId, titleText){
  // Populate the hidden #printMeta block with a title + timestamp, then trigger
  // the browser's print dialog. Print CSS hides everything except the currently
  // visible results panel, so "Save as PDF" in the print dialog gives a clean PDF.
  const meta = document.getElementById("printMeta");
  const now = new Date();
  meta.innerHTML = `<strong>${titleText}</strong><br>Generated ${now.toLocaleString()} &middot; Peng-Robinson EOS Calculator`;
  window.print();
}

function saveResultsAsText(panelId, titleText){
  const panel = document.getElementById(panelId);
  if(!panel) return;
  const now = new Date();
  let lines = [];
  lines.push(titleText);
  lines.push(`Generated ${now.toLocaleString()} - Peng-Robinson EOS Calculator`);
  lines.push("=".repeat(60));
  lines.push("");

  // Walk the panel's headings, result cards, and table rows in document order.
  const walker = panel.querySelectorAll("h2, .result-card, tr");
  const seen = new Set();
  panel.childNodes.forEach(node => collectText(node, lines));

  function collectText(node, out){
    if(node.nodeType !== 1) return;
    if(node.tagName === "H2"){
      out.push("");
      out.push(node.textContent.trim());
      out.push("-".repeat(node.textContent.trim().length));
    } else if(node.classList && node.classList.contains("results-grid")){
      node.querySelectorAll(".result-card").forEach(card=>{
        const label = card.querySelector(".label")?.textContent.trim() || "";
        const value = card.querySelector(".value")?.textContent.trim().replace(/\s+/g," ") || "";
        out.push(`${label}: ${value}`);
      });
    } else if(node.tagName === "TABLE"){
      node.querySelectorAll("tr").forEach(tr=>{
        const cells = Array.from(tr.children).map(td=>td.textContent.trim());
        if(cells.length >= 2) out.push(`${cells[0]}: ${cells.slice(1).join("  ")}`);
        else if(cells.length===1) out.push(cells[0]);
      });
    } else if(node.tagName === "DIV" || node.tagName === "P"){
      const txt = node.textContent.trim();
      if(txt && !node.querySelector("table, h2, .results-grid")) out.push(txt);
      node.childNodes.forEach(child => collectText(child, out));
    }
  }

  const blob = new Blob([lines.join("\n")], {type:"text/plain"});
  const url = URL.createObjectURL(blob);
  const a = document.createElement("a");
  const fname = titleText.toLowerCase().replace(/[^a-z0-9]+/g,"_").replace(/^_|_$/g,"") + "_" + now.toISOString().slice(0,19).replace(/[:T]/g,"-") + ".txt";
  a.href = url;
  a.download = fname;
  document.body.appendChild(a);
  a.click();
  document.body.removeChild(a);
  URL.revokeObjectURL(url);
}

function exportToolbarHTML(panelId, titleText){
  return `
    <div class="export-toolbar">
      <button onclick="printResults('${panelId}','${titleText}')">&#128438; PRINT / SAVE PDF</button>
      <button onclick="saveResultsAsText('${panelId}','${titleText}')">&#128190; SAVE RESULTS (.TXT)</button>
    </div>`;
}

function setMode(m){
  document.getElementById("modeDensity").classList.toggle("active", m==="density");
  document.getElementById("modeJT").classList.toggle("active", m==="jt");
  document.getElementById("modeCV").classList.toggle("active", m==="cv");
  document.getElementById("modeMix").classList.toggle("active", m==="mix");
  document.getElementById("densityMode").style.display = (m==="density") ? "" : "none";
  document.getElementById("jtMode").style.display = (m==="jt") ? "" : "none";
  document.getElementById("cvMode").style.display = (m==="cv") ? "" : "none";
  document.getElementById("mixMode").style.display = (m==="mix") ? "" : "none";
}

// ============================================================
// ISENTHALPIC (JT) engine
// ============================================================
const TREF = 298.15;

function hIdealMix(comps, z, T){
  let H = 0;
  for(let i=0;i<comps.length;i++){
    const d = CP0[comps[i]];
    const dT = T - TREF;
    const integral = d.A*dT + d.B/2*(T*T-TREF*TREF) + d.C/3*(T**3-TREF**3) + d.D/4*(T**4-TREF**4);
    H += z[i]*integral;
  }
  return H;
}
function daDtMixture(comps, w, T, dT=0.05){
  const amP = mixtureAmBmFull(comps, w, T+dT).am;
  const amM = mixtureAmBmFull(comps, w, T-dT).am;
  return (amP-amM)/(2*dT);
}
function hDeparture(comps, w, T, P, phase){
  const {am, bm} = mixtureAmBmFull(comps, w, T);
  const A = am*P/(R*T)**2;
  const B = bm*P/(R*T);
  const roots = solveCubicZFull(A,B);
  if(roots.length===0) throw new Error("No real root in enthalpy departure — conditions out of valid EOS range.");
  const Z = (phase==="vapor") ? roots[roots.length-1] : roots[0];
  const damdT = daDtMixture(comps, w, T);
  const b = bm;
  const sqrt2 = Math.SQRT2;
  const lnTerm = Math.log((Z+(1+sqrt2)*B)/(Z+(1-sqrt2)*B));
  const Hdep = R*T*(Z-1) + (T*damdT - am)/(2*sqrt2*b)*lnTerm;
  return {Hdep, Z};
}
function totalEnthalpy(comps, z, T, P){
  const flash = ptFlash(comps, z, T, P);
  const beta = flash.beta;
  const x = flash.x, y = flash.y;
  const Hig = hIdealMix(comps, z, T);
  if(beta <= 1e-9){
    const {Hdep:HdepL, Z:Zl} = hDeparture(comps, x, T, P, "liquid");
    return {H:Hig+HdepL, beta:0, x, y, Zl, Zv:null};
  } else if(beta >= 1-1e-9){
    const {Hdep:HdepV, Z:Zv} = hDeparture(comps, y, T, P, "vapor");
    return {H:Hig+HdepV, beta:1, x, y, Zl:null, Zv};
  } else {
    const {Hdep:HdepL, Z:Zl} = hDeparture(comps, x, T, P, "liquid");
    const {Hdep:HdepV, Z:Zv} = hDeparture(comps, y, T, P, "vapor");
    const H = Hig + beta*HdepV + (1-beta)*HdepL;
    return {H, beta, x, y, Zl, Zv};
  }
}
// ============================================================
// Antoine equation coefficients: log10(P[bar]) = A - B/(T[K]+C)
// NIST-literature values where available, extended with fits against a
// high-accuracy reference EOS (max error <1.4%, mostly <0.3%) to cover the
// full range up to ~0.999*Tc where NIST's published range doesn't reach.
// ============================================================
const ANTOINE = {
  Methane: [
    [90.99, 189.99, 3.9895, 443.028, -0.49],
  ],
  Ethane: [
    [91.33, 144.13, 4.50706, 791.300, -6.422],
    [135.74, 199.91, 3.93835, 659.739, -16.719],
    [199.91, 250.00, 4.08994, 718.8578, -8.4463],
    [250.00, 305.00, 4.83219, 1131.9743, 54.5205],
  ],
  Ethylene: [
    [149.37, 188.57, 3.87261, 584.146, -18.307],
    [188.57, 235.00, 4.08960, 661.4056, -7.2420],
    [235.00, 282.00, 4.85734, 1065.1391, 55.1620],
  ],
  Propane: [
    [166.02, 231.41, 4.01158, 834.26, -22.763],
    [230.60, 320.70, 3.98292, 819.296, -24.417],
    [277.60, 360.80, 4.53678, 1149.36, 24.906],
  ],
  Propylene: [
    [165.81, 225.98, 3.97488, 795.819, -24.884],
    [225.98, 295.00, 4.04904, 830.8327, -20.0289],
    [295.00, 364.00, 4.80776, 1311.7049, 52.1063],
  ],
  Oxygen: [
    [60.00, 100.00, 3.80864, 318.2813, -6.4929],
    [100.00, 130.00, 4.03722, 363.7605, 0.1546],
    [130.00, 154.40, 4.84170, 605.6726, 38.3166],
  ],
  Nitrogen: [
    [65.00, 95.00, 3.69813, 265.9835, -5.3218],
    [95.00, 115.00, 4.10067, 342.2127, 6.6190],
    [115.00, 126.05, 5.34584, 712.2617, 60.4972],
  ],
  Hydrogen: [
    [14.00, 24.00, 2.98026, 68.8939, 2.8010],
    [24.00, 33.00, 3.78095, 117.7903, 10.9710],
  ],
  Water: [
    [275.00, 370.00, 5.20793, 1737.6641, -39.0485],
    [370.00, 470.00, 5.05134, 1642.7191, -47.5493],
    [470.00, 570.00, 5.29346, 1858.3410, -20.0729],
    [570.00, 646.40, 6.60398, 3600.2886, 197.8151],
  ],
};

function tsatPure(comp, P){
  // Direct closed-form Antoine solve: log10(P[bar]) = A - B/(T+C) => T = B/(A-log10P) - C
  // More accurate than a PR-EOS fugacity-equality search (Antoine is fit to real
  // experimental vapor-pressure data). Returns null if P is outside the
  // correlation's validity range for this component.
  if(!ANTOINE[comp]) return null;
  const Pbar = P / 1e5;
  if(Pbar <= 0) return null;
  const log10P = Math.log10(Pbar);
  for(const [TrLo, TrHi, A, B, C] of ANTOINE[comp]){
    const T = B/(A - log10P) - C;
    if(T >= TrLo - 2 && T <= TrHi + 2) return T;
  }
  return null;
}

// ============================================================
// IBP (bubble point) / FBP (dew point) for mixtures
// ============================================================
function bubblePointT(comps, xIn, P, tol=1e-6, maxIter=100){
  const sum = xIn.reduce((a,b)=>a+b,0);
  const x = xIn.map(v=>v/sum);
  const n = comps.length;
  if(n===1) return tsatPure(comps[0], P);

  function betaAt(T){ return ptFlash(comps, x, T, P).beta; }
  let Tguess = 0;
  for(let i=0;i<n;i++) Tguess += x[i]*COMPONENTS[comps[i]].Tc;
  Tguess *= 0.65;

  const b0 = betaAt(Tguess);
  let lo, hi;
  const step = 10.0;
  if(b0 <= 1e-9){
    lo = Tguess; hi = Tguess;
    let found = false;
    for(let k=0;k<60;k++){ hi += step; if(betaAt(hi) > 1e-9){ found = true; break; } }
    if(!found) return null;
  } else {
    hi = Tguess; lo = Tguess;
    let found = false;
    for(let k=0;k<60;k++){ lo -= step; if(lo <= 0) return null; if(betaAt(lo) <= 1e-9){ found = true; break; } }
    if(!found) return null;
  }
  for(let it=0; it<maxIter; it++){
    const mid = 0.5*(lo+hi);
    const b = betaAt(mid);
    if(Math.abs(hi-lo) < tol) return mid;
    if(b > 1e-9) hi = mid; else lo = mid;
  }
  return 0.5*(lo+hi);
}

function dewPointT(comps, yIn, P, tol=1e-6, maxIter=100){
  const sum = yIn.reduce((a,b)=>a+b,0);
  const y = yIn.map(v=>v/sum);
  const n = comps.length;
  if(n===1) return tsatPure(comps[0], P);

  function betaAt(T){ return ptFlash(comps, y, T, P).beta; }
  let Tguess = 0;
  for(let i=0;i<n;i++) Tguess += y[i]*COMPONENTS[comps[i]].Tc;
  Tguess *= 0.75;

  const b0 = betaAt(Tguess);
  let lo, hi;
  const step = 10.0;
  if(b0 >= 1-1e-9){
    lo = Tguess; hi = Tguess;
    let found = false;
    for(let k=0;k<60;k++){ lo -= step; if(lo <= 0) return null; if(betaAt(lo) < 1-1e-9){ found = true; break; } }
    if(!found) return null;
  } else {
    lo = Tguess; hi = Tguess;
    let found = false;
    for(let k=0;k<60;k++){ hi += step; if(betaAt(hi) >= 1-1e-9){ found = true; break; } }
    if(!found) return null;
  }
  for(let it=0; it<maxIter; it++){
    const mid = 0.5*(lo+hi);
    const b = betaAt(mid);
    if(Math.abs(hi-lo) < tol) return mid;
    if(b >= 1-1e-9) hi = mid; else lo = mid;
  }
  return 0.5*(lo+hi);
}

// ============================================================
// Flash Point estimation (fire safety) via Antoine + Le Chatelier LFL rule
// ============================================================
const LFL = {
  Methane: 5.0, Ethane: 3.0, Ethylene: 2.7, Propane: 2.1, Propylene: 2.0, Hydrogen: 4.0,
  Oxygen: null, Nitrogen: null, Water: null,
  // Extended set: Antoine vapor-pressure correlations aren't available yet for
  // these, so they're excluded from the flash-point (LFL mixing rule) estimate
  // rather than risk an unvalidated result. Density/Cp/JT calcs are unaffected.
  "1,3-Butadiene": null, "n-Butane": null, "C5H10 (1-Pentene)": null,
  "Benzene": null, "Toluene": null, "Vinyl Chloride (VCM)": null,
  "1,2-Dichloroethane (EDC)": null, "Hydrogen Chloride (HCl)": null,
  "Chlorine": null, "Ethylene Oxide (EO)": null, "Ethylene Glycol (EG)": null,
  "n-Hexane": null, "Methanol": null, "Carbon Dioxide (CO2)": null
};

function psatAntoine(comp, T){
  if(!ANTOINE[comp]) return null;
  for(const [TrLo, TrHi, A, B, C] of ANTOINE[comp]){
    if(T >= TrLo-2 && T <= TrHi+2){
      const log10P = A - B/(T+C);
      return Math.pow(10, log10P) * 1e5;
    }
  }
  return null;
}

function flashPointEstimate(comps, zIn, maxIter=200){
  const sum = zIn.reduce((a,b)=>a+b,0);
  const z = zIn.map(v=>v/sum);
  const Patm = 101325.0;

  const combIdx = [];
  for(let i=0;i<comps.length;i++){ if(LFL[comps[i]] !== null && z[i] > 1e-9) combIdx.push(i); }
  if(combIdx.length === 0) return {T_fp:null, LFL_mix:null, status:"No combustible components present (or zero concentration) - flash point not applicable."};

  let zCombSum = 0;
  combIdx.forEach(i => zCombSum += z[i]);
  let sumRatio = 0;
  combIdx.forEach(i => sumRatio += (z[i]/zCombSum) / LFL[comps[i]]);
  const LFLmix = 1.0 / sumRatio;

  function vfrac(T){
    let total = 0, anyValid = false;
    for(const i of combIdx){
      const p = psatAntoine(comps[i], T);
      if(p !== null){ total += z[i]*p/Patm; anyValid = true; }
    }
    return [total, anyValid];
  }

  let TloB = Infinity, ThiB = -Infinity;
  combIdx.forEach(i => {
    const c = comps[i];
    const lo = Math.min(...ANTOINE[c].map(r=>r[0]));
    const hi = Math.max(...ANTOINE[c].map(r=>r[1]));
    TloB = Math.min(TloB, lo); ThiB = Math.max(ThiB, hi);
  });
  const Tlo = TloB - 2, Thi = ThiB + 2;
  const [fLo, validLo] = vfrac(Tlo);
  const [fHi, validHi] = vfrac(Thi);
  const target = LFLmix / 100;

  if(!validLo || !validHi) return {T_fp:null, LFL_mix:LFLmix, status:"Antoine data range insufficient to bracket flash point for this composition."};
  if(fLo >= target) return {T_fp:Tlo, LFL_mix:LFLmix, status:`Flash point at or below the lowest Antoine-valid temperature (${Tlo.toFixed(1)} K) - mixture is flammable across its entire representable liquid range.`};
  if(fHi < target) return {T_fp:null, LFL_mix:LFLmix, status:"Vapor pressure never reaches the LFL threshold within the Antoine-valid range (mixture too dilute in combustibles for this simplified estimate)."};

  let lo = Tlo, hi = Thi;
  for(let it=0; it<maxIter; it++){
    const mid = 0.5*(lo+hi);
    const [fMid, validMid] = vfrac(mid);
    if(!validMid) break;
    if(Math.abs(fMid-target) < 1e-6) return {T_fp:mid, LFL_mix:LFLmix, status:"Converged."};
    if(fMid < target) lo = mid; else hi = mid;
  }
  return {T_fp: 0.5*(lo+hi), LFL_mix:LFLmix, status:"Converged (bisection limit)."};
}

function totalEnthalpyPure(comp, T, P){
  const {am, bm} = mixtureAmBmFull([comp],[1.0],T);
  const A = am*P/(R*T)**2, B = bm*P/(R*T);
  const roots = solveCubicZFull(A,B);
  const Hig = hIdealMix([comp],[1.0],T);
  if(roots.length===1){
    const Z = roots[0];
    const phase = Z>0.5 ? "vapor" : "liquid";
    const {Hdep} = hDeparture([comp],[1.0],T,P,phase);
    return {H:Hig+Hdep, phase, Z, beta: phase==="vapor"?1:0};
  }
  const rv = fugacityCoeffs([comp],[1.0],T,P,"vapor");
  const rl = fugacityCoeffs([comp],[1.0],T,P,"liquid");
  if(rv.phi[0] <= rl.phi[0]){
    const {Hdep,Z} = hDeparture([comp],[1.0],T,P,"vapor");
    return {H:Hig+Hdep, phase:"vapor", Z, beta:1};
  } else {
    const {Hdep,Z} = hDeparture([comp],[1.0],T,P,"liquid");
    return {H:Hig+Hdep, phase:"liquid", Z, beta:0};
  }
}
function isenthalpicFlashPure(comp, T1, P1, P2, tol=1e-3, maxIter=100){
  const r1 = totalEnthalpyPure(comp, T1, P1);
  const H1 = r1.H;
  const Tsat = tsatPure(comp, P2);
  if(Tsat !== null){
    const {Hdep:HdepL, Z:Zl} = hDeparture([comp],[1.0],Tsat,P2,"liquid");
    const {Hdep:HdepV, Z:Zv} = hDeparture([comp],[1.0],Tsat,P2,"vapor");
    const HigSat = hIdealMix([comp],[1.0],Tsat);
    const HliqSat = HigSat+HdepL, HvapSat = HigSat+HdepV;
    if(H1 >= HliqSat && H1 <= HvapSat){
      const beta = HvapSat>HliqSat ? (H1-HliqSat)/(HvapSat-HliqSat) : 0;
      return {T2:Tsat, H1, H2:H1, iters:1, converged:true,
              resultAtT2:{H:H1, phase:"Two-phase (at Tsat)", Z:null, beta, Zl, Zv},
              inletResult:r1, Tsat};
    }
  }
  function f(T){ const r = totalEnthalpyPure(comp, T, P2); return [r.H - H1, r]; }
  let Tstart = T1;
  let [fStart, rStart] = f(Tstart);
  if(Math.abs(fStart) < tol){
    return {T2:Tstart, H1, H2:fStart+H1, iters:1, converged:true, resultAtT2:rStart, inletResult:r1, Tsat};
  }
  let step=5.0, Tlo,flo,Thi,fHi;
  if(fStart>0){
    Thi=Tstart; fHi=fStart;
    Tlo = Tstart-step;
    [flo] = f(Tlo);
    let ei=0;
    while(flo>0 && ei<40){ step*=1.7; Thi=Tlo; fHi=flo; Tlo-=step; [flo]=f(Tlo); ei++; }
  } else {
    Tlo=Tstart; flo=fStart;
    Thi=Tstart+step;
    [fHi]=f(Thi);
    let ei=0;
    while(fHi<0 && ei<40){ step*=1.7; Tlo=Thi; flo=fHi; Thi+=step; [fHi]=f(Thi); ei++; }
  }
  let converged=false, Tmid=Tlo, fmid=flo, rmid=rStart, it;
  for(it=0; it<maxIter; it++){
    Tmid = 0.5*(Tlo+Thi);
    [fmid, rmid] = f(Tmid);
    if(Math.abs(fmid)<tol){ converged=true; break; }
    if((flo<0) === (fmid<0)){ Tlo=Tmid; flo=fmid; } else { Thi=Tmid; fHi=fmid; }
  }
  return {T2:Tmid, H1, H2:fmid+H1, iters:it+1, converged, resultAtT2:rmid, inletResult:r1, Tsat};
}
function isenthalpicFlash(comps, z, T1, P1, P2, tol=1e-3, maxIter=100){
  if(comps.length===1) return isenthalpicFlashPure(comps[0], T1, P1, P2, tol, maxIter);
  const r1 = totalEnthalpy(comps, z, T1, P1);
  const H1 = r1.H;
  function f(T){ const r = totalEnthalpy(comps, z, T, P2); return [r.H - H1, r]; }
  let Tstart = T1;
  let [fStart, rStart] = f(Tstart);
  if(Math.abs(fStart) < tol){
    return {T2:Tstart, H1, H2:fStart+H1, iters:1, converged:true, resultAtT2:rStart, inletResult:r1};
  }
  let step=5.0, Tlo,flo,Thi,fHi;
  if(fStart>0){
    Thi=Tstart; fHi=fStart;
    Tlo = Tstart-step;
    [flo] = f(Tlo);
    let ei=0;
    while(flo>0 && ei<40){ step*=1.7; Thi=Tlo; fHi=flo; Tlo-=step; [flo]=f(Tlo); ei++; }
  } else {
    Tlo=Tstart; flo=fStart;
    Thi=Tstart+step;
    [fHi]=f(Thi);
    let ei=0;
    while(fHi<0 && ei<40){ step*=1.7; Tlo=Thi; flo=fHi; Thi+=step; [fHi]=f(Thi); ei++; }
  }
  let converged=false, Tmid=Tlo, fmid=flo, rmid=rStart, it;
  for(it=0; it<maxIter; it++){
    Tmid = 0.5*(Tlo+Thi);
    [fmid, rmid] = f(Tmid);
    if(Math.abs(fmid)<tol){ converged=true; break; }
    if((flo<0) === (fmid<0)){ Tlo=Tmid; flo=fmid; } else { Thi=Tmid; fHi=fmid; }
  }
  return {T2:Tmid, H1, H2:fmid+H1, iters:it+1, converged, resultAtT2:rmid, inletResult:r1};
}

// ============================================================
// TWO-STREAM MIXING engine
// ============================================================
function streamMolarEnthalpy(comps, z, T, P, phase){
  const Hig = hIdealMix(comps, z, T);
  const {Hdep} = hDeparture(comps, z, T, P, phase);
  return Hig + Hdep;
}

function combineStreams(comps1, z1, F1, comps2, z2, F2){
  const map = {};
  comps1.forEach((c,i)=>{ map[c] = (map[c]||0) + z1[i]*F1; });
  comps2.forEach((c,i)=>{ map[c] = (map[c]||0) + z2[i]*F2; });
  const Ftotal = F1 + F2;
  const comps = Object.keys(map);
  const z = comps.map(c => map[c]/Ftotal);
  return {comps, z, Ftotal};
}

function solveTForH(getHFn, Htarget, Tguess, tol=1e-3, maxIter=150){
  function f(T){ return getHFn(T) - Htarget; }
  let Tstart = Tguess;
  let fStart = f(Tstart);
  if(Math.abs(fStart) < tol) return {T:Tstart, converged:true, iters:1};
  let step=5.0, Tlo,flo,Thi,fHi;
  if(fStart>0){
    Thi=Tstart; fHi=fStart;
    Tlo = Tstart-step;
    flo = f(Tlo);
    let ei=0;
    while(flo>0 && ei<50){ step*=1.7; Thi=Tlo; fHi=flo; Tlo-=step; flo=f(Tlo); ei++; }
  } else {
    Tlo=Tstart; flo=fStart;
    Thi=Tstart+step;
    fHi=f(Thi);
    let ei=0;
    while(fHi<0 && ei<50){ step*=1.7; Tlo=Thi; flo=fHi; Thi+=step; fHi=f(Thi); ei++; }
  }
  let converged=false, Tmid=Tlo, fmid=flo, it;
  for(it=0; it<maxIter; it++){
    Tmid = 0.5*(Tlo+Thi);
    fmid = f(Tmid);
    if(Math.abs(fmid)<tol){ converged=true; break; }
    if((flo<0) === (fmid<0)){ Tlo=Tmid; flo=fmid; } else { Thi=Tmid; fHi=fmid; }
  }
  return {T:Tmid, converged, iters:it+1};
}

// Solves for the rigorous outlet state (T, phase split) of the combined stream at Pf
// given the target molar enthalpy Havg. Always returns {beta, Zl, Zv, x, y} so the
// renderer can treat pure and multi-component outlets identically.
function solveOutletState(combComps, combZ, Havg, Pf, Tguess){
  if(combComps.length === 1){
    const comp = combComps[0];
    const Tsat = tsatPure(comp, Pf);
    if(Tsat !== null){
      const HigSat = hIdealMix([comp],[1.0],Tsat);
      const {Hdep:HdepL, Z:Zl} = hDeparture([comp],[1.0],Tsat,Pf,"liquid");
      const {Hdep:HdepV, Z:Zv} = hDeparture([comp],[1.0],Tsat,Pf,"vapor");
      const HliqSat = HigSat+HdepL, HvapSat = HigSat+HdepV;
      if(Havg >= HliqSat && Havg <= HvapSat){
        const beta = HvapSat>HliqSat ? (Havg-HliqSat)/(HvapSat-HliqSat) : 0;
        return {T:Tsat, converged:true, iters:1, state:{beta, Zl, Zv, x:[1.0], y:[1.0]}};
      }
    }
    const getH = (T)=>totalEnthalpyPure(comp, T, Pf).H;
    const sol = solveTForH(getH, Havg, Tguess);
    const st = totalEnthalpyPure(comp, sol.T, Pf);
    return {T: sol.T, converged: sol.converged, iters: sol.iters,
            state:{ beta: st.beta,
                    Zl: st.phase==="liquid" ? st.Z : null,
                    Zv: st.phase==="vapor" ? st.Z : null,
                    x:[1.0], y:[1.0] }};
  } else {
    const getH = (T)=>totalEnthalpy(combComps, combZ, T, Pf).H;
    const sol = solveTForH(getH, Havg, Tguess);
    const st = totalEnthalpy(combComps, combZ, sol.T, Pf);
    return {T: sol.T, converged: sol.converged, iters: sol.iters, state: st};
  }
}

// ============================================================
// JT UI wiring
// ============================================================
function buildJTCompTable(){
  const defaults = {Propane:1};
  buildToggleCompTable("jCompTable", defaults, "updateJTSum");
}
function updateJTSum(){
  return sumToggleTable("jCompTable", "jCompSum");
}

function runJT(){
  const warnBox = document.getElementById("jWarnBox");
  warnBox.className = "warn"; warnBox.textContent = "";
  try{
    const t1Val = parseFloat(document.getElementById("jT1Val").value);
    const t1Unit = document.getElementById("jT1Unit").value;
    const p1Val = parseFloat(document.getElementById("jP1Val").value);
    const p1Unit = document.getElementById("jP1Unit").value;
    const p2Val = parseFloat(document.getElementById("jP2Val").value);
    const p2Unit = document.getElementById("jP2Unit").value;

    const T1 = toKelvin(t1Val, t1Unit);
    const P1 = toPascal(p1Val, p1Unit);
    const P2 = toPascal(p2Val, p2Unit);

    if(T1 <= 0 || P1 <= 0 || P2 <= 0) throw new Error("Temperature and pressures must be positive (absolute).");
    if(P2 >= P1) throw new Error("Outlet pressure P2 must be less than inlet pressure P1 (this is a pressure REDUCTION).");

    let {comps, z, sum} = collectActiveComps("jCompTable");
    if(comps.length===0) throw new Error("Tick at least one component and enter a non-zero mole fraction.");
    if(Math.abs(sum-1) > 0.0005){
      z = z.map(v=>v/sum);
      warnBox.textContent = `Note: composition summed to ${sum.toFixed(4)}, auto-normalized to 1.0000.`;
      warnBox.classList.add("show");
    }
    if(basisState.j === "wt"){
      z = wtToMol(comps, z);
      warnBox.textContent += (warnBox.textContent? " " : "") + "Note: input interpreted as wt% and converted to mole fractions for calculation.";
      warnBox.classList.add("show");
    }

    const r = isenthalpicFlash(comps, z, T1, P1, P2);

    if(!r.converged){
      warnBox.textContent += (warnBox.textContent? " " : "") + `Note: did not fully converge within iteration limit — result shown is the best estimate after ${r.iters} iterations.`;
      warnBox.classList.add("show");
    }

    renderJTResults(r, comps, z, T1, P1, P2);
  } catch(e){
    warnBox.textContent = "Error: " + e.message;
    warnBox.classList.add("show");
    document.getElementById("jResultsPanel").innerHTML = '<h2>Results</h2><div class="placeholder">Calculation failed — see message above.</div>';
  }
}

function renderJTResults(r, comps, z, T1, P1, P2){
  const T2C = r.T2 - 273.15;
  const T1C = T1 - 273.15;
  const dT = T2C - T1C;
  const beta2 = r.resultAtT2.beta;
  const phase2 = r.resultAtT2.phase || (beta2 < 1e-6 ? "All LIQUID" : (beta2 > 1-1e-6 ? "All VAPOR" : "Two-phase (VLE)"));

  let compRows = "";
  const isPure = comps.length === 1;
  if(!isPure && r.resultAtT2.x && beta2 > 1e-6 && beta2 < 1-1e-6){
    comps.forEach((c,i)=>{
      compRows += `<tr><td>${c}</td><td>${z[i].toFixed(4)}</td><td>${r.resultAtT2.x[i].toFixed(4)}</td><td>${r.resultAtT2.y[i].toFixed(4)}</td></tr>`;
    });
  }

  const html = `
    <h2>Isenthalpic Flash Results</h2>
    <div class="results-grid">
      <div class="result-card ${dT<0?'liquid':'vapor'}">
        <div class="label">Outlet Temperature, T2</div>
        <div class="value">${T2C.toFixed(2)}<span class="unit">&deg;C</span></div>
      </div>
      <div class="result-card ${phase2.includes('VAPOR')||phase2==='vapor' ? 'vapor':'liquid'}">
        <div class="label">Outlet Vapor Fraction</div>
        <div class="value">${(beta2*100).toFixed(2)}<span class="unit">%</span></div>
      </div>
    </div>
    <table class="detail-table">
      <tr><td>Temperature change, T2 &minus; T1</td><td>${dT>=0?'+':''}${dT.toFixed(3)} &deg;C</td></tr>
      <tr><td>Inlet temperature, T1</td><td>${T1C.toFixed(2)} &deg;C (${T1.toFixed(2)} K)</td></tr>
      <tr><td>Outlet temperature, T2</td><td>${T2C.toFixed(2)} &deg;C (${r.T2.toFixed(2)} K)</td></tr>
      <tr><td>Inlet pressure, P1</td><td>${(P1/1e5).toFixed(3)} bar</td></tr>
      <tr><td>Outlet pressure, P2</td><td>${(P2/1e5).toFixed(3)} bar</td></tr>
      <tr><td>Outlet phase</td><td>${phase2}</td></tr>
      <tr><td>Outlet vapor fraction, &beta;2</td><td>${beta2.toFixed(6)}</td></tr>
      <tr><td>Outlet liquid fraction, 1&minus;&beta;2</td><td>${(1-beta2).toFixed(6)}</td></tr>
      <tr><td>H1 (inlet molar enthalpy, ref-relative)</td><td>${r.H1.toFixed(2)} J/mol</td></tr>
      <tr><td>H2 (outlet molar enthalpy, ref-relative)</td><td>${r.H2.toFixed(2)} J/mol</td></tr>
      <tr><td>Enthalpy residual (should be ~0)</td><td>${(r.H2-r.H1).toExponential(3)} J/mol</td></tr>
      <tr><td>Iterations</td><td>${r.iters} ${r.converged ? "(converged)" : "(NOT fully converged)"}</td></tr>
      ${isPure && r.Tsat ? `<tr><td>Saturation temp. of pure fluid at P2</td><td>${(r.Tsat-273.15).toFixed(2)} &deg;C</td></tr>` : ""}
    </table>
    ${compRows ? `
    <h2 style="margin-top:18px;">Outlet Phase Compositions</h2>
    <table class="flash-table">
      <tr><th>Component</th><th>Feed z<sub>i</sub></th><th>Liquid x<sub>i</sub></th><th>Vapor y<sub>i</sub></th></tr>
      ${compRows}
    </table>` : ""}
    ${exportToolbarHTML('jResultsPanel','Isenthalpic_JT_Results')}
  `;
  document.getElementById("jResultsPanel").innerHTML = html;
}

// ============================================================
// CALORIFIC VALUE engine
// ============================================================
const CALORIFIC = {
  Methane:   {GCV:891.56,  NCV:802.62},
  Ethane:    {GCV:1560.69, NCV:1428.83},
  Ethylene:  {GCV:1411.18, NCV:1323.18},
  Propane:   {GCV:2219.17, NCV:2043.11},
  Propylene: {GCV:2058.50, NCV:1925.97},
  Hydrogen:  {GCV:285.83,  NCV:241.82},
  Oxygen:    {GCV:0.0,     NCV:0.0},
  Nitrogen:  {GCV:0.0,     NCV:0.0},
  Water:     {GCV:0.0,     NCV:0.0},
  "Carbon Dioxide (CO2)": {GCV:0.0, NCV:0.0},
  // --- Extended set: approximate literature heats of combustion (ideal-gas
  // basis, kJ/mol, 25°C). Chlorinated species (VCM, EDC) form HCl rather than
  // only H2O/CO2 on combustion; HCl and Chlorine themselves don't combust and
  // are treated as inert (zero heating value), same convention as O2/N2/H2O.
  // Verify all of these against GPA 2145/ISO 6976 or plant lab data before
  // custody-transfer or fiscal use. ---
  "1,3-Butadiene":            {GCV:2541.5, NCV:2409.5},
  "n-Butane":                 {GCV:2877.6, NCV:2657.6},
  "C5H10 (1-Pentene)":        {GCV:3138.3, NCV:2918.3},
  "Benzene":                  {GCV:3301.5, NCV:3169.5},
  "Toluene":                  {GCV:3948.3, NCV:3772.3},
  "Methanol":                 {GCV:763.5,  NCV:675.5},
  "n-Hexane":                 {GCV:4194.7, NCV:3886.7},
  "Vinyl Chloride (VCM)":     {GCV:719.6,  NCV:675.6},
  "1,2-Dichloroethane (EDC)": {GCV:1050.0, NCV:1006.0},
  "Ethylene Oxide (EO)":      {GCV:1305.6, NCV:1217.6},
  "Ethylene Glycol (EG)":     {GCV:1242.2, NCV:1110.2},
  "Hydrogen Chloride (HCl)":  {GCV:0.0,    NCV:0.0},
  "Chlorine":                 {GCV:0.0,    NCV:0.0}
};
const MW_AIR = 28.9647;

function calorificValue(comps, zIn, TrefC){
  const sum = zIn.reduce((a,b)=>a+b,0);
  const z = zIn.map(v=>v/sum);
  let MWmix = 0, GCVmolar = 0, NCVmolar = 0;
  for(let i=0;i<comps.length;i++){
    MWmix += z[i]*COMPONENTS[comps[i]].MW;
    GCVmolar += z[i]*CALORIFIC[comps[i]].GCV;
    NCVmolar += z[i]*CALORIFIC[comps[i]].NCV;
  }
  const GCVmass = GCVmolar/MWmix;   // MJ/kg
  const NCVmass = NCVmolar/MWmix;   // MJ/kg

  const TrefK = TrefC + 273.15;
  const Pref = 101325;
  const Vm = R*TrefK/Pref;          // m3/mol ideal gas
  const GCVvol = (GCVmolar/Vm)/1000; // MJ/m3
  const NCVvol = (NCVmolar/Vm)/1000; // MJ/m3

  const SG = MWmix/MW_AIR;
  const wobbeGross = SG>0 ? GCVvol/Math.sqrt(SG) : 0;
  const wobbeNet = SG>0 ? NCVvol/Math.sqrt(SG) : 0;

  return {MWmix, GCVmolar, NCVmolar, GCVmass, NCVmass, GCVvol, NCVvol, SG, wobbeGross, wobbeNet, TrefC};
}

// ============================================================
// CV UI wiring
// ============================================================
function buildCVCompTable(){
  const defaults = {Methane:0.90, Ethane:0.05, Propane:0.02, Nitrogen:0.03};
  buildToggleCompTable("cvCompTable", defaults, "updateCVSum");
}

function updateCVSum(){
  return sumToggleTable("cvCompTable", "cvCompSum");
}

// ============================================================
// MIXING tab: two-stream composition tables (reuse shared toggle builder)
// ============================================================
function buildMix1CompTable(){
  const defaults = {Methane:0.20, Ethane:0.20, Ethylene:0.20, Propane:0.20, Propylene:0.20};
  buildToggleCompTable("mix1CompTable", defaults, "updateMix1Sum");
}
function updateMix1Sum(){
  return sumToggleTable("mix1CompTable", "mix1CompSum");
}
function buildMix2CompTable(){
  const defaults = {Propane:1.0};
  buildToggleCompTable("mix2CompTable", defaults, "updateMix2Sum");
}
function updateMix2Sum(){
  return sumToggleTable("mix2CompTable", "mix2CompSum");
}

function runCV(){
  const warnBox = document.getElementById("cvWarnBox");
  warnBox.className = "warn"; warnBox.textContent = "";
  try{
    const TrefC = parseFloat(document.getElementById("cvTref").value);

    let {comps, z, sum} = collectActiveComps("cvCompTable");
    if(comps.length===0) throw new Error("Tick at least one component and enter a non-zero mole fraction.");
    if(Math.abs(sum-1) > 0.0005){
      z = z.map(v=>v/sum);
      warnBox.textContent = `Note: composition summed to ${sum.toFixed(4)}, auto-normalized to 1.0000.`;
      warnBox.classList.add("show");
    }
    if(basisState.cv === "wt"){
      z = wtToMol(comps, z);
      warnBox.textContent += (warnBox.textContent? " " : "") + "Note: input interpreted as wt% and converted to mole fractions for calculation.";
      warnBox.classList.add("show");
    }

    const r = calorificValue(comps, z, TrefC);
    renderCVResults(r, comps, z);
  } catch(e){
    warnBox.textContent = "Error: " + e.message;
    warnBox.classList.add("show");
    document.getElementById("cvResultsPanel").innerHTML = '<h2>Results</h2><div class="placeholder">Calculation failed — see message above.</div>';
  }
}

function renderCVResults(r, comps, z){
  const compList = comps.map((c,i)=> `${c} (${(z[i]*100).toFixed(2)}%)`).join(", ");
  const refLabel = r.TrefC + "&deg;C, 1 atm";

  const html = `
    <h2>Calorific Value Results</h2>
    <div class="results-grid">
      <div class="result-card vapor">
        <div class="label">Gross CV (GCV / HHV)</div>
        <div class="value">${r.GCVvol.toFixed(3)}<span class="unit">MJ/m&sup3;</span></div>
      </div>
      <div class="result-card liquid">
        <div class="label">Net CV (NCV / LHV)</div>
        <div class="value">${r.NCVvol.toFixed(3)}<span class="unit">MJ/m&sup3;</span></div>
      </div>
    </div>
    <table class="detail-table">
      <tr><td>Mixture molecular weight</td><td>${r.MWmix.toFixed(3)} g/mol</td></tr>
      <tr><td>Specific gravity (vs air)</td><td>${r.SG.toFixed(4)}</td></tr>
      <tr><td>Reference conditions (volumetric)</td><td>${refLabel}</td></tr>
      <tr><td>GCV (molar)</td><td>${r.GCVmolar.toFixed(3)} kJ/mol</td></tr>
      <tr><td>NCV (molar)</td><td>${r.NCVmolar.toFixed(3)} kJ/mol</td></tr>
      <tr><td>GCV (mass basis)</td><td>${r.GCVmass.toFixed(4)} MJ/kg</td></tr>
      <tr><td>NCV (mass basis)</td><td>${r.NCVmass.toFixed(4)} MJ/kg</td></tr>
      <tr><td>GCV (volumetric)</td><td>${r.GCVvol.toFixed(4)} MJ/m&sup3;</td></tr>
      <tr><td>NCV (volumetric)</td><td>${r.NCVvol.toFixed(4)} MJ/m&sup3;</td></tr>
      <tr><td>Wobbe Index (gross)</td><td>${r.wobbeGross.toFixed(3)} MJ/m&sup3;</td></tr>
      <tr><td>Wobbe Index (net)</td><td>${r.wobbeNet.toFixed(3)} MJ/m&sup3;</td></tr>
      <tr><td>Composition (mole basis)</td><td style="text-align:left; max-width:260px;">${compList}</td></tr>
    </table>
    ${exportToolbarHTML('cvResultsPanel','Calorific_Value_Results')}
  `;
  document.getElementById("cvResultsPanel").innerHTML = html;
}

// ============================================================
// MIXING tab UI wiring
// ============================================================
function runMix(){
  const warnBox = document.getElementById("mixWarnBox");
  warnBox.className = "warn"; warnBox.textContent = "";
  const warnMsgs = [];
  try{
    // --- Stream 1 ---
    const t1Val = parseFloat(document.getElementById("mix1TempVal").value);
    const t1Unit = document.getElementById("mix1TempUnit").value;
    const p1Val = parseFloat(document.getElementById("mix1PresVal").value);
    const p1Unit = document.getElementById("mix1PresUnit").value;
    const T1 = toKelvin(t1Val, t1Unit);
    const P1 = toPascal(p1Val, p1Unit);
    const phase1 = mixPhaseState[1];
    const flow1Val = parseFloat(document.getElementById("mix1FlowVal").value);
    const flow1Unit = document.getElementById("mix1FlowUnit").value;

    let {comps: comps1, z: z1, sum: sum1} = collectActiveComps("mix1CompTable");
    if(comps1.length===0) throw new Error("Stream 1: tick at least one component and enter a non-zero mole fraction.");
    if(Math.abs(sum1-1) > 0.0005){
      z1 = z1.map(v=>v/sum1);
      warnMsgs.push(`Stream 1 composition summed to ${sum1.toFixed(4)}, auto-normalized to 1.0000.`);
    }
    if(basisState.mix1 === "wt"){
      z1 = wtToMol(comps1, z1);
      warnMsgs.push("Stream 1 input interpreted as wt% and converted to mole fractions.");
    }

    // --- Stream 2 ---
    const t2Val = parseFloat(document.getElementById("mix2TempVal").value);
    const t2Unit = document.getElementById("mix2TempUnit").value;
    const p2Val = parseFloat(document.getElementById("mix2PresVal").value);
    const p2Unit = document.getElementById("mix2PresUnit").value;
    const T2 = toKelvin(t2Val, t2Unit);
    const P2 = toPascal(p2Val, p2Unit);
    const phase2 = mixPhaseState[2];
    const flow2Val = parseFloat(document.getElementById("mix2FlowVal").value);
    const flow2Unit = document.getElementById("mix2FlowUnit").value;

    let {comps: comps2, z: z2, sum: sum2} = collectActiveComps("mix2CompTable");
    if(comps2.length===0) throw new Error("Stream 2: tick at least one component and enter a non-zero mole fraction.");
    if(Math.abs(sum2-1) > 0.0005){
      z2 = z2.map(v=>v/sum2);
      warnMsgs.push(`Stream 2 composition summed to ${sum2.toFixed(4)}, auto-normalized to 1.0000.`);
    }
    if(basisState.mix2 === "wt"){
      z2 = wtToMol(comps2, z2);
      warnMsgs.push("Stream 2 input interpreted as wt% and converted to mole fractions.");
    }

    if(T1<=0 || P1<=0 || T2<=0 || P2<=0) throw new Error("Temperatures and pressures must be positive (absolute).");
    if(!(flow1Val > 0) || !(flow2Val > 0)) throw new Error("Enter a positive flow rate for both streams.");

    const MW1 = comps1.reduce((s,c,i)=>s+z1[i]*COMPONENTS[c].MW, 0);
    const MW2 = comps2.reduce((s,c,i)=>s+z2[i]*COMPONENTS[c].MW, 0);
    const F1 = (flow1Unit === "kgh") ? flow1Val/MW1 : flow1Val; // kmol/h
    const F2 = (flow2Unit === "kgh") ? flow2Val/MW2 : flow2Val; // kmol/h

    const pfVal = parseFloat(document.getElementById("mixPfVal").value);
    const pfUnit = document.getElementById("mixPfUnit").value;
    const Pf = toPascal(pfVal, pfUnit);
    if(Pf <= 0) throw new Error("Final mixed pressure must be positive (absolute).");
    if(Pf > Math.min(P1,P2) + 1){
      warnMsgs.push("Note: final mixed pressure exceeds one or both inlet pressures — confirm this is physically intended (e.g. a pump/compressor downstream), not a passive tee/header.");
    }

    const H1 = streamMolarEnthalpy(comps1, z1, T1, P1, phase1);
    const H2 = streamMolarEnthalpy(comps2, z2, T2, P2, phase2);

    const {comps: combComps, z: combZ, Ftotal} = combineStreams(comps1, z1, F1, comps2, z2, F2);
    const Havg = (F1*H1 + F2*H2) / Ftotal;
    const Tguess = (F1*T1 + F2*T2) / Ftotal;

    const outletSol = solveOutletState(combComps, combZ, Havg, Pf, Tguess);
    if(!outletSol.converged){
      warnMsgs.push(`Note: energy balance did not fully converge within the iteration limit — result is the best estimate after ${outletSol.iters} iterations.`);
    }

    if(warnMsgs.length){
      warnBox.textContent = warnMsgs.join(" ");
      warnBox.classList.add("show");
    }

    renderMixResults({
      comps1, z1, T1, P1, phase1, F1, MW1, H1,
      comps2, z2, T2, P2, phase2, F2, MW2, H2,
      combComps, combZ, Ftotal, Pf, Havg, outletSol
    });
  } catch(e){
    warnBox.textContent = "Error: " + e.message;
    warnBox.classList.add("show");
    document.getElementById("mixResultsPanel").innerHTML = '<h2>Results</h2><div class="placeholder">Calculation failed — see message above.</div>';
  }
}

function renderMixResults(r){
  const {comps1,z1,T1,P1,phase1,F1,MW1,H1,
         comps2,z2,T2,P2,phase2,F2,MW2,H2,
         combComps,combZ,Ftotal,Pf,Havg,outletSol} = r;

  const Tf = outletSol.T;
  const st = outletSol.state;
  const beta = st.beta;
  const isTwoPhase = beta > 1e-6 && beta < 1-1e-6;
  const phaseLabel = isTwoPhase ? "Two-Phase (VLE)" : (beta >= 1-1e-6 ? "Vapor" : "Liquid");
  const phaseClass = isTwoPhase ? "vapor" : (beta >= 1-1e-6 ? "vapor" : "liquid");

  const MWmix = combComps.reduce((s,c,i)=>s+combZ[i]*COMPONENTS[c].MW, 0);

  let rhoOut, CpOut, kOut, VOut, extraRows = "";
  if(!isTwoPhase){
    const activePhase = (beta >= 1-1e-6) ? "vapor" : "liquid";
    const Zout = (activePhase === "vapor") ? st.Zv : st.Zl;
    VOut = Zout*R*Tf/Pf; // m3/mol
    rhoOut = (MWmix/1000)/VOut; // kg/m3
    const cpr = cpDeparture(combComps, combZ, Tf, Pf, activePhase);
    CpOut = cpr.Cp_real;
    kOut = cpr.k;
  } else {
    const Vv = st.Zv*R*Tf/Pf, Vl = st.Zl*R*Tf/Pf;
    VOut = beta*Vv + (1-beta)*Vl; // apparent molar volume, additive-volume mixing rule
    rhoOut = (MWmix/1000)/VOut;
    const rhoV = (MWmix/1000)/Vv, rhoL = (MWmix/1000)/Vl;
    const cprV = cpDeparture(combComps, st.y, Tf, Pf, "vapor");
    const cprL = cpDeparture(combComps, st.x, Tf, Pf, "liquid");
    const cpV = cprV.Cp_real, cpL = cprL.Cp_real;
    CpOut = beta*cpV + (1-beta)*cpL; // flow-weighted average, informational only
    kOut = cprV.k; // k is reported for the vapor phase (the phase it's normally used for — relief/compressible flow)
    extraRows = `
      <tr><td>Vapor-phase density</td><td>${rhoV.toFixed(4)} kg/m&sup3;</td></tr>
      <tr><td>Liquid-phase density</td><td>${rhoL.toFixed(4)} kg/m&sup3;</td></tr>
      <tr><td>Vapor-phase Cp</td><td>${cpV.toFixed(4)} J/mol&middot;K</td></tr>
      <tr><td>Liquid-phase Cp</td><td>${cpL.toFixed(4)} J/mol&middot;K</td></tr>
      <tr><td>Vapor-phase k = Cp/Cv</td><td>${cprV.k.toFixed(4)}</td></tr>
      <tr><td>Liquid-phase k = Cp/Cv</td><td>${cprL.k.toFixed(4)}</td></tr>`;
  }

  const compList = combComps.map((c,i)=> `${c} (${(combZ[i]*100).toFixed(2)}%)`).join(", ");

  let vleRows = "";
  if(isTwoPhase){
    combComps.forEach((c,i)=>{
      vleRows += `<tr><td>${c}</td><td>${combZ[i].toFixed(4)}</td><td>${st.x[i].toFixed(4)}</td><td>${st.y[i].toFixed(4)}</td></tr>`;
    });
  }

  const html = `
    <h2>Mixed Outlet Properties</h2>
    <div class="results-grid">
      <div class="result-card ${phaseClass}">
        <div class="label">Outlet Temperature</div>
        <div class="value">${(Tf-273.15).toFixed(2)}<span class="unit">&deg;C</span></div>
      </div>
      <div class="result-card ${phaseClass}">
        <div class="label">Outlet Density</div>
        <div class="value">${rhoOut.toFixed(3)}<span class="unit">kg/m&sup3;</span></div>
      </div>
      <div class="result-card ${phaseClass}">
        <div class="label">k = Cp/Cv${isTwoPhase?' (vapor)':''}</div>
        <div class="value">${kOut.toFixed(4)}</div>
      </div>
    </div>
    <table class="detail-table">
      <tr><td>Outlet phase</td><td>${phaseLabel}</td></tr>
      <tr><td>Outlet vapor fraction, &beta;</td><td>${beta.toFixed(6)}</td></tr>
      <tr><td>Outlet temperature</td><td>${(Tf-273.15).toFixed(3)} &deg;C (${Tf.toFixed(2)} K)</td></tr>
      <tr><td>Outlet (mixed) pressure</td><td>${((Pf-101325)/98066.5).toFixed(4)} kg/cm&sup2;g (${(Pf/1e5).toFixed(4)} bar-a)</td></tr>
      <tr><td>Outlet Cp/Cv ratio, k${isTwoPhase?' (vapor phase)':''}</td><td>${kOut.toFixed(4)}</td></tr>
      <tr><td>Outlet density</td><td>${rhoOut.toFixed(4)} kg/m&sup3;</td></tr>
      <tr><td>Outlet Cp (real gas${isTwoPhase?', flow-weighted avg of both phases':''})</td><td>${CpOut.toFixed(4)} J/mol&middot;K</td></tr>
      <tr><td>Outlet molar volume (apparent)</td><td>${(VOut*1000).toFixed(4)} L/mol</td></tr>
      <tr><td>Outlet mixture molecular weight</td><td>${MWmix.toFixed(3)} g/mol</td></tr>
      ${extraRows}
      <tr><td>Total outlet molar flow</td><td>${Ftotal.toFixed(4)} kmol/h</td></tr>
      <tr><td>Total outlet mass flow</td><td>${(Ftotal*MWmix).toFixed(2)} kg/h</td></tr>
      <tr><td>Combined composition (mole basis)</td><td style="text-align:left; max-width:260px;">${compList}</td></tr>
      <tr><td>Energy balance</td><td>solved in ${outletSol.iters} iteration(s), ${outletSol.converged?"converged":"NOT fully converged"}</td></tr>
    </table>
    ${vleRows ? `
    <h2 style="margin-top:18px;">Outlet Phase Compositions (VLE)</h2>
    <table class="flash-table">
      <tr><th>Component</th><th>Mixed Feed z<sub>i</sub></th><th>Liquid x<sub>i</sub></th><th>Vapor y<sub>i</sub></th></tr>
      ${vleRows}
    </table>` : ""}
    <h2 style="margin-top:18px;">Inlet Stream Summary</h2>
    <table class="flash-table">
      <tr><th>Property</th><th>Stream 1</th><th>Stream 2</th></tr>
      <tr><td>Temperature</td><td>${(T1-273.15).toFixed(2)} &deg;C</td><td>${(T2-273.15).toFixed(2)} &deg;C</td></tr>
      <tr><td>Pressure</td><td>${(P1/1e5).toFixed(3)} bar</td><td>${(P2/1e5).toFixed(3)} bar</td></tr>
      <tr><td>Declared phase</td><td>${phase1}</td><td>${phase2}</td></tr>
      <tr><td>Molar flow</td><td>${F1.toFixed(4)} kmol/h</td><td>${F2.toFixed(4)} kmol/h</td></tr>
      <tr><td>Mass flow</td><td>${(F1*MW1).toFixed(2)} kg/h</td><td>${(F2*MW2).toFixed(2)} kg/h</td></tr>
      <tr><td>Molecular weight</td><td>${MW1.toFixed(3)} g/mol</td><td>${MW2.toFixed(3)} g/mol</td></tr>
      <tr><td>Molar enthalpy (ref-relative)</td><td>${H1.toFixed(2)} J/mol</td><td>${H2.toFixed(2)} J/mol</td></tr>
      <tr><td>Composition (mole basis)</td>
        <td style="text-align:left;">${comps1.map((c,i)=>`${c} (${(z1[i]*100).toFixed(1)}%)`).join(", ")}</td>
        <td style="text-align:left;">${comps2.map((c,i)=>`${c} (${(z2[i]*100).toFixed(1)}%)`).join(", ")}</td></tr>
    </table>
    ${exportToolbarHTML('mixResultsPanel','Two_Stream_Mixing_Results')}
  `;
  document.getElementById("mixResultsPanel").innerHTML = html;
}

buildCompTable();
buildJTCompTable();
buildCVCompTable();
buildMix1CompTable();
buildMix2CompTable();
</script>
</body>
</html>
