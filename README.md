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
