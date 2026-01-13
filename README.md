<!DOCTYPE html>
<html>
<head>
    <title>PO & Material Code Collection</title>
</head>
<body>
    <h2>PO and Material Code Form</h2>

    <form id="poForm">
        <label>PO Number:</label><br>
        <input type="text" id="po" required><br><br>

        <label>Material Code:</label><br>
        <input type="text" id="material" required><br><br>

        <button type="submit">Submit</button>
    </form>

    <p id="result"></p>

    <script>
        document.getElementById("poForm").addEventListener("submit", async function(e) {
            e.preventDefault();

            const data = {
                po_number: document.getElementById("po").value,
                material_code: document.getElementById("material").value
            };

            const response = await fetch("http://localhost:5000/submit", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json"
                },
                body: JSON.stringify(data)
            });

            const result = await response.json();
            document.getElementById("result").innerText = result.message;
        });
    </script>
</body>
</html>

