<!DOCTYPE html>
<html>
<head>
    <title>PO & Material Code Collection</title>

    <!-- SheetJS -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
</head>

<body>
<h2>PO and Material Code Form</h2>

<!-- Upload existing Excel -->
<input type="file" id="upload" accept=".xlsx,.xls"><br><br>

<form id="poForm">
    <label>PO Number:</label><br>
    <input type="text" id="po" required><br><br>

    <label>Material Code:</label><br>
    <input type="text" id="material" required><br><br>

    <button type="submit">Append to Excel</button>
</form>

<p id="result"></p>

<script>
let workbook, worksheet, excelData = [];

document.getElementById("upload").addEventListener("change", function(e) {
    const file = e.target.files[0];
    const reader = new FileReader();

    reader.onload = function(event) {
        const data = new Uint8Array(event.target.result);
        workbook = XLSX.read(data, { type: "array" });
        worksheet = workbook.Sheets[workbook.SheetNames[0]];
        excelData = XLSX.utils.sheet_to_json(worksheet, { header: 1 });
    };

    reader.readAsArrayBuffer(file);
});

document.getElementById("poForm").addEventListener("submit", function(e) {
    e.preventDefault();

    if (!excelData.length) {
        alert("Please upload an Excel file first");
        return;
    }

    excelData.push([
        new Date().toLocaleString(),
        document.getElementById("po").value,
        document.getElementById("material").value
    ]);

    const newSheet = XLSX.utils.aoa_to_sheet(excelData);
    const newWB = XLSX.utils.book_new();
    XLSX.utils.book_append_sheet(newWB, newSheet, "PO Data");

    XLSX.writeFile(newWB, "PO_Material_Updated.xlsx");

    document.getElementById("result").innerText =
        "Excel updated & downloaded successfully";

    document.getElementById("poForm").reset();
});
</script>
</body>
</html>
