<!DOCTYPE html>
<html>
<head>
    <title>Data Collection Form</title>
</head>
<body>
    <h2>User Information</h2>

    <form id="dataForm">
        <label>Name:</label><br>
        <input type="text" id="name" required><br><br>

        <label>Email:</label><br>
        <input type="email" id="email" required><br><br>

        <button type="submit">Submit</button>
    </form>

    <p id="message"></p>

    <script>
        document.getElementById("dataForm").addEventListener("submit", async function(e) {
            e.preventDefault();

            const data = {
                name: document.getElementById("name").value,
                email: document.getElementById("email").value
            };

            const response = await fetch("http://localhost:5000/submit", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json"
                },
                body: JSON.stringify(data)
            });

            const result = await response.json();
            document.getElementById("message").innerText = result.message;
        });
    </script>
</body>
</html>
