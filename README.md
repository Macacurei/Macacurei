<!DOCTYPE html>
<html>
<head>
  <title>Planilha de Controle de Contratos</title>
  <style>
    table {
      border-collapse: collapse;
      width: 100%;
    }

    th, td {
      border: 1px solid #ddd;
      padding: 8px;
    }

    th {
      background-color: #f2f2f2;
    }

    .green-button {
      background-color: green;
      color: white;
    }

    .red-button {
      background-color: red;
      color: white;
    }

    .blue-button {
      background-color: blue;
      color: white;
    }
  </style>
</head>
<body>
  <h1>Planilha de Controle de Contratos</h1>

  <input type="text" id="searchInput" placeholder="Pesquisar">

  <table id="contractsTable">
    <tr>
      <th>Nº CONTRATO</th>
      <th>Nº PROCESSO</th>
      <th>EMPRESA</th>
      <th>CREDO</th>
      <th>OBJETO</th>
      <th>EMPENHO</th>
      <th>VALOR</th>
      <th>DATA DE ASSINATURA</th>
      <th>INICIO DA VIGÊNCIA</th>
      <th>FIM DA VIGÊNCIA</th>
      <th>AÇÕES</th>
    </tr>
    <tr>
      <td>12345</td>
      <td>54321</td>
      <td>Empresa A</td>
      <td>Credor A</td>
      <td>Objeto A</td>
      <td>Empenho A</td>
      <td>R$ 1000,00</td>
      <td>01/01/2023</td>
      <td>01/02/2023</td>
      <td>01/01/2024</td>
      <td>
        <button class="green-button" onclick="editRow(this)">Editar</button>
        <button class="red-button" onclick="deleteRow(this)">Excluir</button>
      </td>
    </tr>
  </table>

  <h2>Adicionar Novo Contrato</h2>
  <form id="addContractForm">
    <label for="contractNumber">Nº CONTRATO:</label>
    <input type="text" id="contractNumber" required><br>

    <label for="processNumber">Nº PROCESSO:</label>
    <input type="text" id="processNumber" required><br>

    <label for="company">EMPRESA:</label>
    <input type="text" id="company" required><br>

    <label for="credor">CREDO:</label>
    <input type="text" id="credor" required><br>

    <label for="object">OBJETO:</label>
    <input type="text" id="object" required><br>

    <label for="empenho">EMPENHO:</label>
    <input type="text" id="empenho" required><br>

    <label for="value">VALOR:</label>
    <input type="text" id="value" required><br>

    <label for="signatureDate">DATA DE ASSINATURA:</label>
    <input type="text" id="signatureDate" required><br>

    <label for="startDate">INICIO DA VIGÊNCIA:</label>
    <input type="text" id="startDate" required><br>

    <label for="endDate">FIM DA VIGÊNCIA:</label>
    <input type="text" id="endDate" required><br>

    <label for="pdfFile">ARQUIVO PDF:</label>
    <input type="file" id="pdfFile" required accept="application/pdf"><br>

    <input type="submit" class="blue-button" value="Adicionar">
  </form>

  <h2>Calculadora de Datas</h2>
  <form id="dateCalculatorForm">
    <label for="date">Data:</label>
    <input type="text" id="date" required><br>

    <label for="days">Dias a adicionar:</label>
    <input type="number" id="days"><br>

    <label for="months">Meses a adicionar:</label>
    <input type="number" id="months"><br>

    <input type="submit" class="blue-button" value="Calcular">
  </form>

  <div id="resultContainer"></div>

  <script>
    function editRow(button) {
      var row = button.parentNode.parentNode;
      var cells = row.getElementsByTagName("td");

      for (var i = 0; i < cells.length - 1; i++) {
        var input = document.createElement("input");
        input.type = "text";
        input.value = cells[i].innerText;
        cells[i].innerText = "";
        cells[i].appendChild(input);
      }

      var saveButton = document.createElement("button");
      saveButton.innerHTML = "Salvar";
      saveButton.className = "green-button";
      saveButton.onclick = function() {
        saveRow(this);
      };

      var cancelButton = document.createElement("button");
      cancelButton.innerHTML = "Cancelar";
      cancelButton.className = "red-button";
      cancelButton.onclick = function() {
        cancelEdit(this);
      };

      var actionsCell = cells[cells.length - 1];
      actionsCell.innerHTML = "";
      actionsCell.appendChild(saveButton);
      actionsCell.appendChild(cancelButton);
    }

    function saveRow(button) {
      var row = button.parentNode.parentNode;
      var cells = row.getElementsByTagName("td");

      for (var i = 0; i < cells.length - 1; i++) {
        var input = cells[i].getElementsByTagName("input")[0];
        cells[i].innerText = input.value;
      }

      var editButton = document.createElement("button");
      editButton.innerHTML = "Editar";
      editButton.className = "green-button";
      editButton.onclick = function() {
        editRow(this);
      };

      var deleteButton = document.createElement("button");
      deleteButton.innerHTML = "Excluir";
      deleteButton.className = "red-button";
      deleteButton.onclick = function() {
        deleteRow(this);
      };

      var actionsCell = cells[cells.length - 1];
      actionsCell.innerHTML = "";
      actionsCell.appendChild(editButton);
      actionsCell.appendChild(deleteButton);
    }

    function cancelEdit(button) {
      var row = button.parentNode.parentNode;
      var cells = row.getElementsByTagName("td");

      for (var i = 0; i < cells.length - 1; i++) {
        var input = cells[i].getElementsByTagName("input")[0];
        cells[i].innerText = input.value;
      }

      var editButton = document.createElement("button");
      editButton.innerHTML = "Editar";
      editButton.className = "green-button";
      editButton.onclick = function() {
        editRow(this);
      };

      var deleteButton = document.createElement("button");
      deleteButton.innerHTML = "Excluir";
      deleteButton.className = "red-button";
      deleteButton.onclick = function() {
        deleteRow(this);
      };

      var actionsCell = cells[cells.length - 1];
      actionsCell.innerHTML = "";
      actionsCell.appendChild(editButton);
      actionsCell.appendChild(deleteButton);
    }

    function deleteRow(button) {
      var row = button.parentNode.parentNode;
      row.parentNode.removeChild(row);
    }

    document.getElementById("addContractForm").addEventListener("submit", function(event) {
      event.preventDefault();

      var table = document.getElementById("contractsTable");
      var newRow = table.insertRow(table.rows.length);

      var contractNumber = document.getElementById("contractNumber").value;
      var processNumber = document.getElementById("processNumber").value;
      var company = document.getElementById("company").value;
      var credor = document.getElementById("credor").value;
      var object = document.getElementById("object").value;
      var empenho = document.getElementById("empenho").value;
      var value = document.getElementById("value").value;
      var signatureDate = document.getElementById("signatureDate").value;
      var startDate = document.getElementById("startDate").value;
      var endDate = document.getElementById("endDate").value;
      var pdfFile = document.getElementById("pdfFile").files[0];

      var cell1 = newRow.insertCell(0);
      cell1.innerHTML = contractNumber;

      var cell2 = newRow.insertCell(1);
      cell2.innerHTML = processNumber;

      var cell3 = newRow.insertCell(2);
      cell3.innerHTML = company;

      var cell4 = newRow.insertCell(3);
      cell4.innerHTML = credor;

      var cell5 = newRow.insertCell(4);
      cell5.innerHTML = object;

      var cell6 = newRow.insertCell(5);
      cell6.innerHTML = empenho;

      var cell7 = newRow.insertCell(6);
      cell7.innerHTML = value;

      var cell8 = newRow.insertCell(7);
      cell8.innerHTML = signatureDate;

      var cell9 = newRow.insertCell(8);
      cell9.innerHTML = startDate;

      var cell10 = newRow.insertCell(9);
      cell10.innerHTML = endDate;

      var cell11 = newRow.insertCell(10);
      var editButton = document.createElement("button");
      editButton.innerHTML = "Editar";
      editButton.className = "green-button";
      editButton.onclick = function() {
        editRow(this);
      };

      var deleteButton = document.createElement("button");
      deleteButton.innerHTML = "Excluir";
      deleteButton.className = "red-button";
      deleteButton.onclick = function() {
        deleteRow(this);
      };

      cell11.appendChild(editButton);
      cell11.appendChild(deleteButton);

      // Upload the PDF file here
      var formData = new FormData();
      formData.append("pdf", pdfFile);

      // Make an AJAX request to upload the file
      var xhr = new XMLHttpRequest();
      xhr.open("POST", "/upload", true);
      xhr.onreadystatechange = function() {
        if (xhr.readyState === 4 && xhr.status === 200) {
          console.log("File uploaded successfully!");
        }
      };
      xhr.send(formData);

      document.getElementById("addContractForm").reset();
    });

    document.getElementById("searchInput").addEventListener("keyup", function() {
      var input = document.getElementById("searchInput");
      var filter = input.value.toUpperCase();
      var table = document.getElementById("contractsTable");
      var rows = table.getElementsByTagName("tr");

      for (var i = 1; i < rows.length; i++) {
        var cells = rows[i].getElementsByTagName("td");
        var found = false;

        for (var j = 0; j < cells.length - 1; j++) {
          var cell = cells[j];

          if (cell.innerHTML.toUpperCase().indexOf(filter) > -1) {
            found = true;
            break;
          }
        }

        if (found) {
          rows[i].style.display = "";
        } else {
          rows[i].style.display = "none";
        }
      }
    });

    document.getElementById("dateCalculatorForm").addEventListener("submit", function(event) {
      event.preventDefault();

      var dateInput = document.getElementById("date");
      var daysInput = document.getElementById("days");
      var monthsInput = document.getElementById("months");
      var resultContainer = document.getElementById("resultContainer");

      var date = new Date(dateInput.value);
      var days = parseInt(daysInput.value) || 0;
      var months = parseInt(monthsInput.value) || 0;

      date.setDate(date.getDate() + days);
      date.setMonth(date.getMonth() + months);

      var result = "Nova data: " + date.toDateString();
      resultContainer.innerHTML = result;
    });
  </script>
</body>
</html>
