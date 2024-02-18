<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>


<h2>Enter Array of Integers and Target Value</h2>
<p>Please enter a comma-separated list of integers and a target value to calculate the indices of two numbers that multiply to the target value.</p>

<form action="index.php" method="post">
    <label for="nums">Array of Integers (comma-separated):</label>
    <input type="text" id="nums" name="nums" required><br><br>
    <label for="target">Target Value:</label>
    <input type="number" id="target" name="target" required><br><br>
    <button type="submit">Find Indices</button>
</form>

<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $numsStr = trim($_POST['nums']);
    $target = intval($_POST['target']);

    $nums = explode(',', $numsStr);
    $nums = array_map('intval', $nums);

    $result = twoProduct($nums, $target);

    echo "<h2>Result:</h2>";
    if ($result) {
        echo "Indices of two numbers are <strong>" . $result[0] . "</strong> and <strong>" . $result[1] . "</strong>.<br>";
    } else {
        echo "No valid indices found, please try another set of inputs.";
    }
}

function twoProduct($nums, $target) {
    if (in_array(0, $nums) && in_array($target, $nums)) {
        return [array_search(0, $nums), array_search($target, $nums)];
    }

    foreach ($nums as $i => $num) {
        if($num == 0 || $target%$num != 0) continue;
        if (in_array($target/$num, $nums)) {
            return [$i, array_search($target/$num, $nums)];
        }
    }

    return false;
}
?>

</body>
</html>