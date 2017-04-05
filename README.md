<html>
<head>
</head>

<body>
	<form method="POST" enctype="multipart/form-data">
		<input type="file" name="file" />
		<input type="submit" name="submit" />
	</form>
</body>
</html>

<?php

if(isset($_POST["submit"]))
	{
		$file = $_FILES['file']['tmp_name'];
		
		if($_FILES["file"]["size"] > 0) {
			$handle = fopen($file, "r");
			$c = 0;
			while(($filesop = fgetcsv($handle, 1000, ",")) !== false)
			{
				$name = $filesop[0];
				$email = $filesop[1];
				
				$sql = mysql_query("INSERT INTO csv (name, email) VALUES ('$name','$email')");
				$c = $c + 1;
			}
		}
		
			if($sql){
				echo "You database has imported successfully. You have inserted ". $c ." recoreds";
			}else{
				echo "Sorry! There is some problem.";
			}

	}
	?>
