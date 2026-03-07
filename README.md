# odoo
checking
<?php
session_start();

include("../config/db.php");

if(!isset($_SESSION['admin_id'])){
    header("Location: ../admin_login.php");
    exit();
}

// Get form data
$name = $_POST['name'];
$description = $_POST['description'];
$price = $_POST['price'];
$category = $_POST['category'];
$stock = $_POST['stock'];

// Handle image upload
$image = $_FILES['image']['name'];
$tmp = $_FILES['image']['tmp_name'];
move_uploaded_file($tmp, "../images/".$image);

// Insert into database
$sql = "INSERT INTO products (name, description, price, image, category, stock)
        VALUES ('$name','$description','$price','$image','$category','$stock')";
mysqli_query($conn,$sql);

header("Location: ../admin_panel.php");
exit();
?>
