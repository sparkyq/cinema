# cinema
<?php include("includes/header.php"); ?>

	<div class="container mregister">
		<div id="login">
			<h1>Реєстрація</h1>
			<form action="register.php" id="registerform" method="post"name="registerform">
				<p><label for="user_login">Повне імя<br>
					<input class="input" id="full_name" name="full_name"size="32"  type="text" value=""></label></p>
					<p><label for="user_pass">E-mail<br>
						<input class="input" id="email" name="email" size="32"type="email" value=""></label></p>
						<p><label for="user_pass">Імя користувача<br>
							<input class="input" id="username" name="username"size="20" type="text" value=""></label></p>
							<p><label for="user_pass">Пароль<br>
								<input class="input" id="password" name="password"size="32"   type="password" value=""></label></p>
								<p class="submit"><input class="button" id="register" name= "register" type="submit" value="Зареєструватись"></p>
								<p class="regtext">Вже зареєстровані? <a href= "login.php">Введіть імя користувача</a>!</p>
							</form>
						</div>
					</div>

					<?php

					if(isset($_POST["register"])){

						if(!empty($_POST['full_name']) && !empty($_POST['email']) && !empty($_POST['username']) && !empty($_POST['password'])) {
							$full_name= htmlspecialchars($_POST['full_name']);
							$email=htmlspecialchars($_POST['email']);
							$username=htmlspecialchars($_POST['username']);
							$password=htmlspecialchars($_POST['password']);
							$query=mysqli_query($con, "SELECT * FROM admin WHERE username='".$username."'");
							$numrows=mysqli_num_rows($query);


							if($numrows==0)
							{
								$sql="INSERT INTO admin
								(full_name, email, username, password)
								VALUES('$full_name','$email', '$username', '$password')";
								$result=mysqli_query($con, $sql);
								if($result){
									$message = "Account Successfully Created";
								} else {
									$message = "Failed to insert data information!";
								}
							} else {
								$message = "That username already exists! Please try another one!";
							}
						} else {
							$message = "All fields are required!";
						}
					}

					$email = filter_var($email, FILTER_SANITIZE_EMAIL);
							if (filter_var($email, FILTER_VALIDATE_EMAIL)) {echo
"OK!";}
else {echo "Будь ласка, повторно введіть електронний
лист!"; }
					?>


					<?php if (!empty($message)) {echo "<p class='error'>" . "MESSAGE: ". $message . "</p>";} ?>

					

					
<?php include("includes/footer.php"); ?>
