 <html lang="es">  
<head>  
<meta charset="UTF-8">  
<meta name="viewport" content="width=device-width, initial-scale=1.0">  
<title>Calculadora de Incentivos - Choferes de Distribución</title>  
<style>  
* { margin: 0; padding: 0; box-sizing: border-box; }  
body {  
  background-color: #F0F4FF;  
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;  
  padding: 12px;  
  max-width: 600px;  
  margin: 0 auto;  
}  
.header {  
  background: linear-gradient(135deg, #003DA5, #0056D6);  
  padding: 16px 20px; border-radius: 16px; text-align: center;  
  margin: 6px 0 12px 0; box-shadow: 0 4px 12px rgba(0,61,165,0.3);  
}  
.header h1 { font-size: 1.3em; color: #FFD100; margin: 0; }  
.header p { color: white; font-size: 0.88em; margin: 4px 0 0 0; }  
.selector-container { margin-bottom: 12px; }  
.selector-container label { font-weight: bold; color: #003DA5; font-size: 0.95em; }  
.selector-container select {  
  width: 100%; padding: 10px 14px; border: 2px solid #003DA5;  
  border-radius: 12px; font-size: 1em; background: white; color: #333; margin-top: 4px;  
}  
.divider { border: none; border-top: 1.5px solid #003DA5; opacity: 0.2; margin: 8px 0; }  
.card {  
  background: white; border-radius: 12px; padding: 14px 16px;  
  margin-bottom: 10px; border-left: 5px solid #003DA5;  
  box-shadow: 0 2px 8px rgba(0,0,0,0.08);  
}  
.card-titulo { font-size: 1.02em; font-weight: bold; color: #003DA5; margin-bottom: 4px; }  
.input-group { margin-bottom: 10px; }  
.input-group label { font-size: 0.88em; color: #444; display: block; margin-bottom: 3px; font-weight: 500; }  
.input-group input {  
  width: 100%; padding: 9px 12px; border: 2px solid #003DA5;  
  border-radius: 10px; font-size: 1.05em; background: white; color: #333;  
}  
.input-group input:focus { outline: none; border-color: #FFD100; box-shadow: 0 0 0 3px rgba(255,209,0,0.3); }  
.input-group input::placeholder { color: #aaa; }  
.chip {  
  display: inline-block; padding: 3px 10px; border-radius: 20px;  
  font-size: 0.82em; margin: 3px 0;  
}  
.chip-verde { background-color: #D4EDDA; color: #155724; }  
.chip-rojo { background-color: #F8D7DA; color: #721C24; }  
.chip-amarillo { background-color: #FFF3CD; color: #856404; }  
.metricas-row { display: flex; gap: 6px; margin: 6px 0; flex-wrap: wrap; }  
.metrica {  
  background: #E8F0FF; border-radius: 12px; padding: 8px 10px;  
  text-align: center; flex: 1; min-width: 80px;  
}  
.metrica-valor { font-size: 1.2em; font-weight: bold; color: #003DA5; }  
.metrica-etiqueta { font-size: 0.72em; color: #555; }  
.resultado {  
  background: linear-gradient(135deg, #003DA5, #0056D6);  
  border-radius: 16px; padding: 20px; text-align: center;  
  color: white; margin-top: 12px; box-shadow: 0 6px 20px rgba(0,61,165,0.4);  
}  
.resultado-label { font-size: 0.95em; margin-bottom: 6px; }  
.resultado-total { font-size: 2.4em; font-weight: bold; color: #FFD100; }  
.resultado-desglose { font-size: 0.82em; color: #cce0ff; margin-top: 8px; line-height: 1.4; }  
.footer { text-align: center; color: #999; font-size: 0.75em; margin-top: 16px; padding-bottom: 20px; }  
.pilar-badge {  
  display: inline-block; background: #FFD100; color: #003DA5; font-weight: bold;  
  padding: 2px 10px; border-radius: 8px; font-size: 0.78em; margin-bottom: 4px;  
}  
.nota-info {  
  font-size: 0.75em; color: #856404; margin-top: 4px;  
}  
</style>  
</head>  
<body>  
  
<div class="header">  
  <h1>🚚 Incentivos Choferes</h1>  
  <p>Calculadora de distribución</p>  
</div>  
  
<div class="selector-container">  
  <label>📍 Tipo de Ruta</label>  
  <select id="tipo_ruta" onchange="calcularIncentivos()">  
    <option value="AAA" selected>AAA</option>  
    <option value="AA">AA</option>  
    <option value="A">A</option>  
    <option value="E">E</option>  
  </select>  
</div>  
  
<hr class="divider">  
  
<div class="card">  
  <span class="pilar-badge">INCENTIVO 1</span>  
  <div class="card-titulo">🗓️ Fecha Promesa</div>  
  <hr class="divider">  
  <div class="input-group">  
    <label>% Cumplimiento meta de Fecha Promesa</label>  
    <input type="text" id="input_fp" value="95.5" oninput="calcularIncentivos()">  
  </div>  
  <div id="chip_fp"></div>  
  <div id="metrica_fp" class="metricas-row"></div>  
</div>  
  
<div class="card">  
  <span class="pilar-badge">INCENTIVO 2</span>  
  <div class="card-titulo">📦 Artículos por Control</div>  
  <hr class="divider">  
  <div class="input-group">  
    <label>% Cumplimiento meta de Artículos por control</label>  
    <input type="text" id="input_ac" value="92.0" oninput="calcularIncentivos()">  
  </div>  
  <div id="chip_ac"></div>  
  <div id="metrica_ac" class="metricas-row"></div>  
</div>  
  
<div class="card">  
  <span class="pilar-badge">CANDADO</span>  
  <div class="card-titulo">⭐ NPS Trimestral</div>  
  <hr class="divider">  
  <p style="font-size:0.82em; color:#555; margin-bottom:8px;">  
    Sujeto a cumplir al menos el 91% de la meta del NPS Trimestral para poder multiplicar los incentivos.  
  </p>  
  <div class="input-group">  
    <label>% NPS Trimestral</label>  
    <input type="text" id="input_nps" value="94.5" oninput="calcularIncentivos()">  
  </div>  
  <div id="chip_nps"></div>  
  <div id="metrica_nps" class="metricas-row"></div>  
</div>  
  
<div id="resultado_total"></div>  
  
<div class="footer">Calculadora Interna • Choferes de Distribución</div>  
  
<script>  
function leerNum(id) {  
  var v = document.getElementById(id).value.replace(/,/g, '.').replace(/\$/g, '').replace(/ /g, '');  
  var n = parseFloat(v);  
  return isNaN(n) ? 0 : Math.max(0, n);  
}  
function fmt(n) { return '$' + n.toFixed(2).replace(/\B(?=(\d{3})+(?!\d))/g, ','); }  
function chipHTML(tipo, texto) {  
  return '<span class="chip chip-' + tipo + '">' + texto + '</span>';  
}  
function metricaHTML(etiqueta, valor) {  
  return '<div class="metrica"><div class="metrica-etiqueta">' + etiqueta + '</div><div class="metrica-valor">' + valor + '</div></div>';  
}  
function resultadoHTML(total, desglose) {  
  return '<div class="resultado"><div class="resultado-label">🏆 TU INCENTIVO TOTAL</div>'  
    + '<div class="resultado-total">' + fmt(total) + '</div>'  
    + '<div class="resultado-desglose">' + desglose + '</div></div>';  
}  
  
function calcularIncentivos() {  
  // 1. Fecha Promesa  
  var fp = leerNum('input_fp');  
  var base_fp = 0;  
  if (fp < 90) base_fp = 0;  
  else if (fp < 92) base_fp = 600;  
  else if (fp < 96) base_fp = 800;  
  else base_fp = 1000;  
  
  var chipFP = '';  
  if (fp < 90) chipFP = chipHTML('rojo', '❌ < 90.00% — $0');  
  else if (fp < 92) chipFP = chipHTML('amarillo', '⚠️ 90.00% - 91.99% — $600');  
  else if (fp < 96) chipFP = chipHTML('verde', '✅ 92.00% - 95.99% — $800');  
  else chipFP = chipHTML('verde', '🏆 96.00% - 100% — $1,000');  
   
  document.getElementById('chip_fp').innerHTML = chipFP;  
  document.getElementById('metrica_fp').innerHTML = metricaHTML('💰 Base Fecha Promesa', fmt(base_fp));  
  
  // 2. Artículos por Control  
  var ac = leerNum('input_ac');  
  var base_ac = 0;  
  if (ac < 90) base_ac = 0;  
  else if (ac < 92) base_ac = 600;  
  else if (ac < 96) base_ac = 800;  
  else base_ac = 1000;  
  
  var chipAC = '';  
  if (ac < 90) chipAC = chipHTML('rojo', '❌ < 90.00% — $0');  
  else if (ac < 92) chipAC = chipHTML('amarillo', '⚠️ 90.00% - 91.99% — $600');  
  else if (ac < 96) chipAC = chipHTML('verde', '✅ 92.00% - 95.99% — $800');  
  else chipAC = chipHTML('verde', '🏆 96.00% - 100% — $1,000');  
  
  document.getElementById('chip_ac').innerHTML = chipAC;  
  document.getElementById('metrica_ac').innerHTML = metricaHTML('💰 Base Art. por Control', fmt(base_ac));  
  
  // 3. NPS Trimestral (Candado/Multiplicador)  
  var nps = leerNum('input_nps');  
  var mult_nps = 0;  
  if (nps < 91) mult_nps = 0;  
  else if (nps < 92) mult_nps = 0.80;  
  else if (nps < 94) mult_nps = 1.00;  
  else mult_nps = 1.10;  
  
  var chipNPS = '';  
  if (nps < 91) chipNPS = chipHTML('rojo', '❌ Menor del 91% — Multiplicador 0%');  
  else if (nps < 92) chipNPS = chipHTML('amarillo', '⚠️ 91% al 91.9% — Multiplicador 80%');  
  else if (nps < 94) chipNPS = chipHTML('verde', '✅ 92% al 93.9% — Multiplicador 100%');  
  else chipNPS = chipHTML('verde', '🏆 94% al 100% — Multiplicador 110%');  
  
  document.getElementById('chip_nps').innerHTML = chipNPS;  
  document.getElementById('metrica_nps').innerHTML = metricaHTML('✖️ Multiplicador NPS', (mult_nps * 100).toFixed(0) + '%');  
  
  // Cálculo Total  
  var suma_bases = base_fp + base_ac;  
  var total = suma_bases * mult_nps;  
  
  var desglose = 'Base Fecha Promesa: ' + fmt(base_fp) + '<br>' +  
                 'Base Art. por Control: ' + fmt(base_ac) + '<br>' +  
                 'Suma de Bases: ' + fmt(suma_bases) + '<br>' +  
                 'Multiplicador NPS: ' + (mult_nps * 100).toFixed(0) + '%<br>' +  
                 '<strong>Cálculo: ' + fmt(suma_bases) + ' × ' + mult_nps.toFixed(2) + ' = ' + fmt(total) + '</strong>';  
  
  document.getElementById('resultado_total').innerHTML = resultadoHTML(total, desglose);  
}  
  
// Inicializar calculadora al cargar  
window.onload = function() {  
  calcularIncentivos();  
};  
</script>  
</body>  
</html>
