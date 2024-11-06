<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>User Details Form</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            background-image:url(orsrc4721.jpg)
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
        }
        th {
            background-color: #f2f2f2;
        }
        .btn {
            cursor: pointer;
            padding: 5px 10px;
            margin: 5px;
        }
        .btn-edit {
            background-color: #4CAF50;
            color: white;
        }
        .btn-delete {
            background-color: #f44336;
            color: white;
        }
        #lastEntryDetails {
            display: none;
            margin-top: 20px;
            padding: 10px;
            border: 1px solid #ddd;
            background-color: #f9f9f9;
        }
        img {
            width: 50px;
            height: 50px;
        }
    </style>
</head>
<body>

<h2>User Details Form</h2>
<form id="detailsForm">
    <label for="photo">Upload Photo:</label>
    <input type="file" id="photo" accept="image/*" required><br><br>

    <label for="name">Name:</label>
    <input type="text" id="name" required><br><br>

    <label for="address">Address:</label>
    <input type="text" id="address" required><br><br>

    <label for="aadhaar">Aadhaar Number:</label>
    <input type="text" id="aadhaar" required><br><br>

    <h3>DOCUMENT DETAILS</h3>
    <label for="aadhaarImage">Aadhaar Image:</label>
    <input type="file" id="aadhaarImage" accept="image/*" required><br><br>

    <label for="landDetails">Land Details:</label>
    <input type="text" id="landDetails" required><br><br>
    
    <label for="landImage">Upload Land Image:</label>
    <input type="file" id="landImage" accept="image/*" required><br><br>

    <label for="consentLetter">Letter of Consent:</label>
    <input type="file" id="consentLetter" accept="image/*" required><br><br>

    <button type="submit">Submit</button>
</form>

<h2>Submitted Details</h2>
<table id="detailsTable">
    <thead>
        <tr>
            <th>Photo</th>
            <th>Name</th>
            <th>Address</th>
            <th>Aadhaar Number</th>
            <th>Aadhaar Image</th>
            <th>Land Details</th>
            <th>Land Image</th>
            <th>Letter of Consent</th>
            <th>Actions</th>
        </tr>
    </thead>
    <tbody>
        <!-- Data will be populated here -->
    </tbody>
</table>

<div id="lastEntryDetails">
    <h3>Last Submitted Entry Details</h3>
    <div id="entryDetailsContent"></div>
</div>

<script>
// JavaScript to handle form submission and data display
document.getElementById('detailsForm').addEventListener('submit', function(event) {
    event.preventDefault();

    const photo = document.getElementById('photo').files[0];
    const name = document.getElementById('name').value;
    const address = document.getElementById('address').value;
    const aadhaar = document.getElementById('aadhaar').value;
    const aadhaarImage = document.getElementById('aadhaarImage').files[0];
    const landDetails = document.getElementById('landDetails').value;
    const landImage = document.getElementById('landImage').files[0];
    const consentLetter = document.getElementById('consentLetter').files[0];

    // Create a new row in the table
    const table = document.getElementById('detailsTable').getElementsByTagName('tbody')[0];
    const newRow = table.insertRow();

    const cell1 = newRow.insertCell(0);
    const cell2 = newRow.insertCell(1);
    const cell3 = newRow.insertCell(2);
    const cell4 = newRow.insertCell(3);
    const cell5 = newRow.insertCell(4);
    const cell6 = newRow.insertCell(5);
    const cell7 = newRow.insertCell(6);
    const cell8 = newRow.insertCell(7);
    const cell9 = newRow.insertCell(8);

    // Create image elements for photo and collateral images
    const photoURL = URL.createObjectURL(photo);
    const aadhaarImageURL = URL.createObjectURL(aadhaarImage);
    const landImageURL = URL.createObjectURL(landImage);
    const consentLetterURL = URL.createObjectURL(consentLetter);

    cell1.innerHTML = `<img src="${photoURL}" alt="Photo">`;
    cell2.innerText = name;
    cell3.innerText = address;
    cell4.innerText = aadhaar;
    cell5.innerHTML = `<img src="${aadhaarImageURL}" alt="Aadhaar Image">`;
    cell6.innerText = landDetails;
    cell7.innerHTML = `<img src="${landImageURL}" alt="Land Image">`;
    cell8.innerHTML = `<img src="${consentLetterURL}" alt="Consent Letter">`;
    cell9.innerHTML = `
        <button class="btn btn-edit" onclick="editRow(this)">Edit</button>
        <button class="btn btn-delete" onclick="deleteRow(this)">Delete</button>
        <button class="btn" onclick="viewLastEntry(this)">View</button>
    `;

    // Show the last entry details
    showLastEntry(name, address, aadhaar, photoURL, aadhaarImageURL, landDetails, landImageURL, consentLetterURL);

    // Clear form fields after submission
    document.getElementById('detailsForm').reset();
});

// Function to show the last entry details
function showLastEntry(name, address, aadhaar, photoURL, aadhaarImageURL, landDetails, landImageURL, consentLetterURL) {
    const entryDetailsContent = document.getElementById('entryDetailsContent');
    entryDetailsContent.innerHTML = `
        <p><strong>Name:</strong> ${name}</p>
        <p><strong>Address:</strong> ${address}</p>
        <p><strong>Aadhaar Number:</strong> ${aadhaar}</p>
        <p><strong>Photo:</strong> <img src="${photoURL}" alt="Photo"></p>
        <p><strong>Aadhaar Image:</strong> <img src="${aadhaarImageURL}" alt="Aadhaar Image"></p>
        <p><strong>Land Details:</strong> ${landDetails}</p>
        <p><strong>Land Image:</strong> <img src="${landImageURL}" alt="Land Image"></p>
        <p><strong>Letter of Consent:</strong> <img src="${consentLetterURL}" alt="Consent Letter"></p>
    `;
    document.getElementById('lastEntryDetails').style.display = 'block';
}

// Function to edit a row
function editRow(button) {
    const row = button.parentNode.parentNode;
    const cells = row.getElementsByTagName('td');

    document.getElementById('photo').value = ''; // Note: file inputs cannot be set programmatically
    document.getElementById('name').value = cells[1].innerText;
    document.getElementById('address').value = cells[2].innerText;
    document.getElementById('aadhaar').value = cells[3].innerText;
    document.getElementById('landDetails').value = cells[5].innerText;

    // Remove the row for re-edit
    row.remove();
}

// Function to delete a row
function deleteRow(button) {
    const row = button.parentNode.parentNode;
    row.remove();
}

// Function to view last entry details
function viewLastEntry(button) {
    // Assuming the view button refers to the last submitted row.
    const row = button.parentNode.parentNode;
    const cells = row.getElementsByTagName('td');
    
    const name = cells[1].innerText;
    const address = cells[2].innerText;
    const aadhaar = cells[3].innerText;
    const photo = cells[0].querySelector('img').src;
    const aadhaarImage = cells[4].querySelector('img').src;
    const landDetails = cells[5].innerText;
    const landImage = cells[6].querySelector('img').src;
    const consentLetter = cells[7].querySelector('img').src;

    showLastEntry(name, address, aadhaar, photo, aadhaarImage, landDetails, landImage, consentLetter);
    
}
</script>
</body>
</html>
