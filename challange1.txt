<?php

$Car_rental_Problems = array (
    array ('size' => 'S', 'Capacityofthecar' => 5, 'cost' => 5000),
    array ('size' => 'M', 'Capacityofthecar' => 10, 'cost' => 8000),
    array ('size' => 'L', 'Capacityofthecar' => 15, 'cost' => 12000)
);


function Car_Rental_Problems($seats, $Options) {
   
    $numOptions = count($Options);
    $optimal = array_fill(0, $seats + 1, PHP_INT_MAX);
    $choices = array_fill(0, $seats + 1, ''); 

    $optimal[0] = 0;

   
    for ($i = 1; $i <= $seats; $i++) {
    
        for ($j = 0; $j < $numOptions; $j++) {
            $size = $Options[$j]['size'];
            $capacity = $Options[$j]['Capacityofthecar'];
            $cost = $Options[$j]['cost'];

            if ($i >= $capacity && $optimal[$i - $capacity] + $cost < $optimal[$i]) {
                $optimal[$i] = $optimal[$i - $capacity] + $cost;
                $choices[$i] = "{$size} x " . ($i / $capacity);
            }
        }
    }

    echo "{$choices[$seats]}\n";
    echo "Total = PHP {$optimal[$seats]}\n";
}


if ($argc < 2) {
    echo "Please Input Number Of  seat's: ";
    $seats = trim(fgets(STDIN));
} else {
    $seats = intval($argv[1]);
}


if (!is_numeric($seats) || $seats <= 0) {
    echo "Invalid Input. Please Input Numbers Only.\n";
    exit(1);
}

Car_Rental_Problems($seats, $Car_rental_Problems);
?>