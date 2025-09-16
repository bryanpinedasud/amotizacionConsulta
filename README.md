<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Tabla de Amortización</title>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@600;700&family=Poppins:wght@400;600;700&family=Roboto+Mono&display=swap" rel="stylesheet">
  <style>
    /* Reset */
    * { margin: 0; padding: 0; box-sizing: border-box; }

    body {
      font-family: 'Poppins', sans-serif;
      background: #f4f6f9;
      color: #2c3e50;
      padding: 20px;
    }

    h1 {
      text-align: center;
      font-size: 30px;
      font-weight: 700;
      color: #2c3e50;
      margin-bottom: 25px;
      font-family: 'Poppins', sans-serif;
    }

    /* Layout principal */
    .contenedor {
      display: grid;
      grid-template-columns: 2fr 1fr;
      gap: 30px;
      max-width: 1300px;
      margin: auto;
    }

    /* Panel izquierdo */
    .izquierda {
      background: #fff;
      padding: 25px;
      border-radius: 16px;
      box-shadow: 0 6px 16px rgba(0,0,0,0.08);
    }

    /* Formulario */
    .formulario label {
      display: block;
      margin-top: 15px;
      font-weight: 600;
      color: #34495e;
      font-family: 'Poppins', sans-serif;
    }

    .formulario input, .formulario select {
      width: 100%;
      padding: 12px;
      margin-top: 6px;
      border-radius: 10px;
      border: 1px solid #dce1e6;
      font-size: 15px;
      transition: all 0.3s;
      font-family: 'Montserrat', sans-serif;
    }

    .formulario input:focus, .formulario select:focus {
      outline: none;
      border-color: #3498db;
      box-shadow: 0 0 0 3px rgba(52,152,219,0.2);
    }

    /* Botón */
    .formulario button {
      width: 100%;
      padding: 14px;
      border-radius: 10px;
      font-size: 16px;
      font-weight: 600;
      margin-top: 18px;
      border: none;
      cursor: pointer;
      transition: all 0.3s;
      background: linear-gradient(135deg, #3498db, #2980b9);
      color: white;
      font-family: 'Poppins', sans-serif;
    }

    .formulario button:hover {
      background: linear-gradient(135deg, #2980b9, #1c6ea4);
    }

    /* Tabla */
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 25px;
      background: #fff;
      border-radius: 12px;
      overflow: hidden;
      box-shadow: 0 6px 16px rgba(0,0,0,0.08);
      font-family: 'Roboto Mono', monospace;
    }

    th {
      background: #3498db;
      color: white;
      padding: 14px;
      font-weight: 600;
      text-transform: uppercase;
      font-size: 14px;
      position: sticky;
      top: 0;
    }

    td {
      padding: 14px;
      text-align: center;
      font-size: 14px;
      color: #2c3e50;
    }

    tr:nth-child(even) { background: #f9fbfd; }
    tr:hover { background: #eef6fc; }

    /* Panel derecho */
    .derecha {
      display: flex;
      flex-direction: column;
      gap: 25px;
    }

    /* Tarjeta principal (Cuota Mensual) */
    .card-principal {
      background: linear-gradient(135deg, #27ae60, #219150);
      color: white;
      padding: 35px 25px;
      border-radius: 16px;
      border: 4px solid #1e8449; /* borde agregado */
      text-align: center;
      box-shadow: 0 8px 18px rgba(0,0,0,0.15);
    }

    .card-principal h2 {
      font-size: 24px;
      margin-bottom: 15px;
      font-weight: 600;
      font-family: 'Poppins', sans-serif;
    }

    .card-principal p {
      font-size: 46px;
      font-weight: 700;
      font-family: 'Montserrat', sans-serif;
    }

    /* Otras tarjetas */
    .card {
      background: #fff;
      padding: 25px;
      border-radius: 16px;
      box-shadow: 0 6px 16px rgba(0,0,0,0.08);
      text-align: center;
    }

    .card h2 {
      margin-bottom: 8px;
      color: #7f8c8d;
      font-size: 16px;
      font-weight: 600;
      font-family: 'Poppins', sans-serif;
    }

    .card p {
      font-size: 22px;
      font-weight: 700;
      color: #2c3e50;
      font-family: 'Montserrat', sans-serif;
    }

    /* Card informativo */
    .info-card {
      background: #fffaf3;
      border-left: 6px solid #e67e22;
      padding: 20px 25px;
      border-radius: 12px;
      font-size: 15px;
      line-height: 1.7;
      color: #2c3e50;
      box-shadow: 0 4px 12px rgba(0,0,0,0.05);
      font-family: 'Poppins', sans-serif;
    }

    .info-card h3 {
      color: #e67e22;
      font-size: 18px;
      margin-bottom: 12px;
      font-weight: 600;
    }

    .info-card ul {
      list-style: none;
      margin-top: 8px;
    }

    .info-card ul li {
      margin-bottom: 6px;
      padding-left: 22px;
      position: relative;
    }

    .info-card ul li::before {
      content: "✔";
      position: absolute;
      left: 0;
      color: #e67e22;
      font-size: 14px;
    }

    .info-card p strong {
      color: #e67e22;
      font-family: 'Montserrat', sans-serif;
    }
  </style>
</head>
<body>
  <div class="contenedor">
    <div class="izquierda">
      <h1>Simulador de Tabla de Amortización</h1>
      <div class="formulario">
        <label for="monto">Valor del consumo:</label>
        <input type="number" id="monto" placeholder="Ej: 5000">

        <label for="meses">Plazo (meses):</label>
        <select id="meses">
          <option value="3">3 meses</option>
          <option value="6">6 meses</option>
          <option value="9">9 meses</option>
          <option value="12">12 meses</option>
        </select>

        <button onclick="generarTabla()">Generar Tabla</button>
      </div>
      <div id="resultado"></div>
    </div>

    <div class="derecha">
      <div class="card-principal">
        <h2>Cuota Mensual Aproximada</h2>
        <p id="cuotaMensual">-</p>
      </div>
      <div class="card">
        <h2>Valor de la compra</h2>
        <p id="valorCompra">-</p>
      </div>
      <div class="info-card">
        <h3>Importante</h3>
        <p>Los valores son aproximados debido a que se deben considerar otros rubros de cobro mensual como:</p>
        <ul>
          <li>Estado de cuenta</li>
          <li>Asistencia</li>
          <li>Desgravamen</li>
          <li>Interés diferido</li>
          <li>Gestión de cobranza</li>
        </ul>
        <p>Si tienen dudas, escribir al <strong>0989081508</strong>.</p>
      </div>
    </div>
  </div>

  <script>
    function generarTabla() {
      const monto = parseFloat(document.getElementById("monto").value);
      const meses = parseInt(document.getElementById("meses").value);
      const interesAnual = 0.156;
      const interesMensual = interesAnual / 12;

      if (isNaN(monto) || monto <= 0) {
        alert("Por favor ingresa un monto válido.");
        return;
      }

      const cuota = monto * (interesMensual * Math.pow(1 + interesMensual, meses)) / (Math.pow(1 + interesMensual, meses) - 1);

      let saldo = monto;
      let tabla = `<table>
        <thead>
          <tr>
            <th>Mes</th>
            <th>Cuota</th>
            <th>Interés</th>
            <th>Capital</th>
            <th>Saldo</th>
          </tr>
        </thead>
        <tbody>`;

      for (let i = 1; i <= meses; i++) {
        let interes = saldo * interesMensual;
        let capital = cuota - interes;
        saldo -= capital;

        tabla += `
          <tr>
            <td>${i}</td>
            <td>$${cuota.toFixed(2)}</td>
            <td>$${interes.toFixed(2)}</td>
            <td>$${capital.toFixed(2)}</td>
            <td>$${saldo > 0 ? saldo.toFixed(2) : 0}</td>
          </tr>`;
      }

      tabla += "</tbody></table>";
      document.getElementById("resultado").innerHTML = tabla;

      // Actualizar cards
      document.getElementById("valorCompra").innerText = "$" + monto.toFixed(2);
      document.getElementById("cuotaMensual").innerText = "$" + cuota.toFixed(2);
    }
  </script>
</body>
</html>
