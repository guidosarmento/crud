<!DOCTYPE html>
<html lang="en">
<head>
<title>CRUD PHP</title>
    <script src="https://code.jquery.com/jquery-3.2.1.min.js"></script>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-beta.3/css/bootstrap.min.css" integrity="sha384-Zug+QiDoJOrZ5t4lssLdxGhVrurbmBWopoEl+M6BdEfwnCJZtKxi1KgxUyJq13dy" crossorigin="anonymous"/>
    <script src="//maxcdn.bootstrapcdn.com/bootstrap/4.0.0-beta.3/js/bootstrap.min.js" integrity="sha384-a5N7Y/aK3qNeh15eJKGWxsqtnX/wWdSZSKp+81YjTmS15nvnvxKHuzaWwXHDli+4" crossorigin="anonymous"></script>
</head>
<body>
<div class = "container">
<h4><div class="text-center text-muted delimiter">Create Read Update & Delete</div></h4>

<!--BOLU NIA FUNSAUN-->
<?php require_once 'process.php'; ?>


<!--HATUDU SAI IHA INDEX PAGE FUNSAUN NE'EBE ITA CRIA IHA PROCESS.PHP-->
	<?php if (isset($_SESSION['message'])): ?>

		<div class="alert alert-<?=$_SESSION['msg_type']?>">
			<?php 
				echo $_SESSION['message'];
				unset($_SESSION['message']);
			?>
		</div>
	<?php endif; ?>
	

<!--BOLU DATABASE-->
<?php
$mysqli = new mysqli('localhost', 'root', '', 'crud') or die(mysqli_error($mysqli));
$result = $mysqli->query("SELECT * FROM data") or die($mysqli->error);
//pre_r( $result );

?>

<!--HATUDU IHA TABELA-->
<div class="row justify-content-center">
  <table class="table">
    <thead>
      <tr>
        <th>Name</th>
        <th>Location</th>
        <th colspan="2">Action</th>
      </tr>
    </thead>
    <?php
    while($row = $result->fetch_assoc()): ?>
            <tr>
				
                <td><?php echo $row['name']; ?></td>
                <td><?php echo $row['location']; ?></td>
                <td>
					<a href="index.php?edit=<?php echo $row['id'];?>"class="btn btn-info">Edit</a>
					<a href="process.php?delete=<?php echo $row['id'];?>"class="btn btn-danger">Delete</a>
				</td>
			
            </tr>
	<?php endwhile; ?>
  </table>
</div>
<?php

function pre_r($array) {
    echo '<pre>';
    print_r($array);
    echo '</pre>';
}

?>
  <div class="row justify-content-center">
    <form action="process.php" method="POST">
	
	<input type="hidden" name="id" value="<?php echo $id; ?>">
		
	<div class="form-group">

		<label>Name</label>
		<input type="text" name="name" class="form-control" value="<?php echo $name; ?>" placeholder="Enter Your Name">
    </div>
    <div class="form-group">
		<label>Location</label>
		<input type="text" name="location" class="form-control" value="<?php echo $location; ?>" placeholder="Enter Your Location">
	</div>
     <div class="form-group">
			<?php if ($update==true): ?>
				<button type="submit" class="btn btn-info" name="update">Update</button>
			<?php else: ?>
				<button type="submit" class="btn btn-primary" name="save">Save</button>
			<?php endif; ?>
    </div>
	</form>
  </div>
  
</div>
</body>
</html>
