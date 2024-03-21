<!DOCTYPE html>
<html>
<head>
    <title>Simple CRUD Application</title>
</head>
<body>

<h2>Create New Item</h2>
<form action="" method="post">
    Name: <input type="text" name="name"><br>
    Description: <input type="text" name="description"><br>
    <input type="submit" name="submit" value="Submit">
</form>

<?php
// MySQL database connection
$host = 'localhost';
$dbname = 'crud';
$username = 'root';
$password = '';

try {
    $pdo = new PDO("mysql:host=$host;dbname=$dbname", $username, $password);
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

    // Create table if not exists
    $pdo->exec("CREATE TABLE IF NOT EXISTS items (
        id INT AUTO_INCREMENT PRIMARY KEY,
        name VARCHAR(255) NOT NULL,
        description TEXT
    )");

    // Function to create a new item
    function createItem($name, $description, $pdo) {
        $stmt = $pdo->prepare("INSERT INTO items (name, description) VALUES (:name, :description)");
        $stmt->execute([':name' => $name, ':description' => $description]);
    }

    // Create new item if form submitted
    if (isset($_POST['submit'])) {
        $name = $_POST['name'];
        $description = $_POST['description'];
        createItem($name, $description, $pdo);
    }

    // Function to read all items
    function readItems($pdo) {
        $stmt = $pdo->query("SELECT * FROM items");
        return $stmt->fetchAll(PDO::FETCH_ASSOC);
    }

    // Read all items
    $items = readItems($pdo);
    if ($items) {
        echo "<h2>All Items</h2>";
        echo "<ul>";
        foreach ($items as $item) {
            echo "<li>Name: {$item['name']}, Description: {$item['description']}</li>";
        }
        echo "</ul>";
    } else {
        echo "<p>No items found.</p>";
    }
} catch (PDOException $e) {
    die("Error: " . $e->getMessage());
}
?>

</body>
</html>
