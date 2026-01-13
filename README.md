<!DOCTYPE html>
<html>
<head>
    <title>PO & Material Code Collection</title>

    <!-- Excel Library -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
</head>

<body>
    <h2>PO and Material Code Form</h2>

    <form id="poForm">
        <label>PO Number:</label><br>
        <input type="text" id="po" required><br><br>

        <label>Material Code:</label><br>
        <input type="text" id="material" required><br><br>

        <button type="submit">Save to Excel</button>
    </form>

    <p id="result"></p>

    <script>
        // Excel data with header
        let excelData = [
            ["Date", "PO Number", "Material Code"]
        ];

        document.getElementById("poForm").addEventListener("submit", function(e) {
            e.preventDefault();

            const po = document.getElementById("po").value;
            const material = document.getElementById("material").value;

            // Add row
            excelData.push([
                new Date().toLocaleString(),
                po,
                material
            ]);

            // Create Excel file
            const wb = XLSX.utils.book_new();
            const ws = XLSX.utils.aoa_to_sheet(excelData);
            XLSX.utils.book_append_sheet(wb, ws, "PO Data");

            // Download Excel
            XLSX.writeFile(wb, "PO_Material_Data.xlsx");

            document.getElementById("result").innerText =
                "Data saved to Excel successfully";

            document.getElementById("poForm").reset();
        });
    </script>
</body>
</html>
