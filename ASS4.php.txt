<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Palindrome Checker</title>
</head>
<body>
    <h2>Palindrome Checker</h2>
    <form action="" method="post">
        <label for="inputString">Enter a string:</label>
        <input type="text" id="inputString" name="inputString" required>
        <button type="submit">Check Palindrome</button>
    </form>

    <?php
    if ($_SERVER["REQUEST_METHOD"] == "POST") {
        $inputString = $_POST['inputString'];

        if (isPalindrome($inputString)) {
            echo "<p>'$inputString' is a palindrome!</p>";
        } else {
            echo "<p>'$inputString' is not a palindrome.</p>";
        }
    }

    function isPalindrome($str) {
        $cleanStr = preg_replace("/[^A-Za-z0-9]/", '', strtolower($str));
        $reverseStr = strrev($cleanStr);
        return $cleanStr === $reverseStr;
    }
    ?>
</body>
</html>
