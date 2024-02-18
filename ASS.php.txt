<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>

    <form action="" method="post">
        <fieldset>
            <legend>Calculate Grade</legend>
            <label for="cgpa">Enter CGPA:</label>
            <input type="number" min="0" max="4" step="0.01" id="cgpa" name="cgpa" required>
            <button type="submit">Convert</button>
        </fieldset>
    </form>
    
    <?php
        if ($_SERVER["REQUEST_METHOD"] == "POST") {
            $cgpa = $_POST['cgpa'];

            echo getGrade($cgpa);
        }

        function getGrade($cgpa) {
            $grade = '';
            
            if ($cgpa >= 4.0) {
                $grade = 'Excellent (A)';
            } elseif ($cgpa >= 3.5 && $cgpa < 4.0) {
                $grade = 'Very Good (B+)';
            } elseif ($cgpa >= 3.0 && $cgpa < 3.5) {
                $grade = 'Good (B)';
            } elseif ($cgpa >= 2.5 && $cgpa < 3.0) {
                $grade = 'Fair (C+)';
            } elseif ($cgpa >= 2.0 && $cgpa < 2.5) {
                $grade = 'Pass (C)';
            } else {
                $grade = 'Fail (F)';
            }
            
            return "CGPA: $cgpa, Grade: $grade";
        }
   
    ?>

</body>
</html>