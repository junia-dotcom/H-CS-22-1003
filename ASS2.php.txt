<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>

    <form action="" method="post">
        <label for="dateInput">Enter the date (YYYY-MM-DD):</label><br>
        <input type="text" id="dateInput" name="dateInput" required><br>
        <button type="submit">Convert</button>
    </form>

    <?php
    if ($_SERVER["REQUEST_METHOD"] == "POST") {
        $dateInput = isset($_POST['dateInput']) ? $_POST['dateInput'] : null;
        
        if (preg_match('/^\d{4}-\d{2}-\d{2}$/', $dateInput)) {
            list($year, $month, $day) = explode('-', $dateInput);
            $year = intval($year);
            $month = intval($month);
            $day = intval($day);
            
            if (checkdate($month, $day, $year)) {
                if ($month == 2 && $day == 29 && !($year % 4 == 0 && ($year % 100 != 0 || $year % 400 == 0))) {
                    echo "<p>Error: February doesn't have 29 days in a non-leap year.</p>";
                } else {
                    $timestamp = mktime(0, 0, 0, $month, $day, $year);
                    $dayOfWeek = date('l', $timestamp);
                    echo "<p>The day of the week for $dateInput is: $dayOfWeek</p>";
                }
            } else {
                echo "<p>Error: Invalid date.</p>";
            }
        } else {
            echo "<p>Error: Invalid date format. Please enter date in YYYY-MM-DD format.</p>";
        }
    }
    ?>

</body>
</html>
