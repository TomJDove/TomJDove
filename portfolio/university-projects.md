---
layout: post
title: "University Projects"
date: 2024-02-13
permalink: '/portfolio/university-projects'
---

<p align='justify'>
On this page, I will describe selected projects that I worked on during my studies at the University of Melbourne.
For copyright and academic integrity reasons I cannot share much of the code, as we would often be building on code supplied for the university staff or directly using their ideas.
I will only provide snippets of code that I've written and that doesn't reveal much about the internal details of the assignment.
</p>

## RPG project

**Course:** Object-Oriented Software Development \\
**Programming language:** Java \\
**Concepts:** Object-oriented programming, object-oriented software design, game development (user interfaces, collisions, simple AI)

<center>
<figure>
  <img
  src="https://tomjdove.github.io/TomJDove/assets/uni/titleScreen.png"
  style="width:60%"
  >
  <figcaption>
  The title screen I created for the game.
  </figcaption>
</figure>
</center>

<p align='justify'>
This project was completed as part of the subject Object-Oriented Software Development.
We created a fully playable tile-based RPG game with different characters, enemies and basic combat.
The game was implemented in Java using the <a href="https://slick.ninjacave.com">Slick2D</a> library.
</p>

It's hopefully okay for me to share the class diagram:
<center>
<figure>
  <img
  src="https://tomjdove.github.io/TomJDove/assets/uni/rpg-classes.jpg"
  style="width:100%"
  >
  <figcaption>
  The class diagram for the RPG game.
  </figcaption>
</figure>
</center>

--------------------------------

## Server-based proof-of-work solver for Hashcash mining algorithm

**Course:** Computer Systems \\
**Programming language:** C \\
**Concepts:** TCP servers, multi-threaded programming, socket programming, proof-of-work solver

<p align='justify'>
In this project, which was part of the subject Computer Systems, we implemented a server-based proof-of-work solver for the Hashcash mining algorithm used in Bitcoin.
We wrote a TCP server program that could correctly reply to simple messages received from client programs concurrently.
</p>

<p align='justify'>
One thing the server had to be able to do was verify whether a given solution message was a valid solution.
The following function achieved this:
</p>

```c
int verify_soln(Solnmsg soln)
{
	/* First find the target */
	uint256_t target;
	uint256_init(target);

	getTarget(target, soln);

	/* Concatenate seed and solution. */
	BYTE seedsolution[40];
	memcpy(seedsolution, soln->seed, 32);
	memcpy(seedsolution+32, &(soln->solution), 8);

	/* Double hash the seed|solution. */
	BYTE hash1[SHA256_BLOCK_SIZE], hash2[SHA256_BLOCK_SIZE];
	SHA256_CTX ctx;
	sha256_init(&ctx);
	sha256_update(&ctx, seedsolution, 40);
	sha256_final(&ctx, hash1);
	sha256_init(&ctx);
	sha256_update(&ctx, hash1, SHA256_BLOCK_SIZE);
	sha256_final(&ctx, hash2);

	/* Determine if it's less than target. */
	if (sha256_compare(target, hash2) == 1)
	{
		return 1;
	}
	return 0;
}

```

<p align='justify'>
The server also had to, upon request, find proof-of-work solutions. 
This is, by design, a very labor-intensive process, so the server implements multithreading to distribute the workload and allow it to receive other messages while it is working on finding a proof-of-work solution.
The following function finds the proof-of-work message.
</p>

```c
/* Find a valid proof of work message. */
void find_valid_SOLN(Workmsg work, Solnmsg soln)
{
	int i;
	uint8_t numworkers = work->worker_count;

	/* Difficulty and seed are the same for both */
	memcpy(soln->difficulty, work->difficulty, 4);
	memcpy(soln->seed, work->seed, 32);

	/* Find the worker offset */
	uint64_t offset = get_worker_offset(work->start, numworkers);
	uint64_t initial_nonce = bytes_to_uint64(work->start);

	/* Create soln structs for workers to use */
	struct solnmsg solns[numworkers];

	/* Threads */
	pthread_t workers[numworkers];

	/* Start all the worker threads */
	for (i=0; i < numworkers; i++)
	{
		/* Copy seed and solution into threads soln */
		memcpy(solns[i].difficulty, work->difficulty, 4);
		memcpy(solns[i].seed, work->seed, 32);
		solns[i].isValid = 0;
		/* Add right nonce, with offset */
		uint64_to_bytes(solns[i].solution, initial_nonce + i*offset);

		/* Get to work */
		if(pthread_create(workers+i, NULL, worker_function, (void*)(solns+i)) != 0)
		{
			perror("pthread_create error");
			exit(EXIT_FAILURE);
		}
	}
	
	for (i=0; i<numworkers; i++)
	{
		pthread_join(workers[i], NULL);
		if (solns[i].isValid)
		{
			/* This is the thread with the solution */
			memcpy(soln->solution, solns[i].solution, 8);
		}
	}

	/* Done. */
}
```

--------------------------------

## Simple web application with database backend

**Course:** Database Systems \\
**Programming languages:** PHP, SQL \\
**Concepts:** Web applications, database management

<p align='justify'>
In the subject Database Systems, we created a simple web application that allows the user to submit orders and browse the selection of products for a fictional spatula-making company.
</p>

<p align='justify'>
The web pages were made using HTML, PHP, and SQL.
A database was created using MySQL and populated with some generic data. The webpages were built using HTML with PHP embedded. 
</p>

The following is a sample of code from the order submission page of the website.
It does the following:
1. Connects to the MySQL database.
2. Sanitises the order and customer information that has been submitted by the staff member inputting the order information.
3. Uses SQL to insert the order into the database.
4. Creates a new order line item and adds it to the database.
5. Updates the database to reflect the change in stock after the new order is made. 

```php
<html>
<head><title>Order Submission</title></head>
<body>
<h1> Order Submission </h1>
<p>

<br>

<?php

$con = mysqli_connect(....);

// Check connection
if (mysqli_connect_errno()) {
	echo "Could not connect to MySQL for the following reason: " . mysqli_connect_error();
}

mysqli_query($con, "START TRANSACTION");

// Create a new order
$ResponsibleStaffMember = trim(stripslashes(htmlspecialchars($_POST["ResponsibleStaffMember"])));
$CustomerDetails =  trim(stripslashes(htmlspecialchars($_POST["CustomerDetails"])));

$insertQuery = "INSERT INTO `Order` VALUES (DEFAULT, NOW(), '" . $ResponsibleStaffMember . "', '" . $CustomerDetails . "')";

$orderInsert = mysqli_query($con, $insertQuery);

// Function to check quantity input. It needs to be numeric and non-negative.
function validQuantity($quantity)
{
	if (!is_numeric($quantity))
	{
		echo "<p> Invalid quantity.</p>";
		return false;
	}
	if ((int)$quantity < 0)
	{
		echo "<p>You cannot enter a negative quantity.</p>";
		return false;
	}
	// Need to make sure there are enough spatulas
	

	return true;
}

// Create new order line item 
$orderID = mysqli_insert_id($con);

$noIssues = true; // Variable to tell us if we have a problem
$hasOrdered = false; //Have we actually ordered any spatulas?

$spatulaIDs = mysqli_query($con, "SELECT idSpatula, ProductName, QuantityInStock FROM Spatula");
while (($row= mysqli_fetch_array($spatulaIDs)) and $noIssues and $orderInsert)
{
  	$idSpatula = $row['idSpatula'];
	$quantity = $_POST['order_quantity_' . $idSpatula];
	if (empty($quantity))
		continue;
	$quantityInStock = intval($row['QuantityInStock']);	
	if (validQuantity($quantity))
	{
	  	$enough = $quantity <= $quantityInStock;
	  	// We don't need a line item if they're not ordering any of this spatula
		if ($quantity > 0 and $enough)
		{
		  	// Insert the new line order item
		  	$result1 = mysqli_query($con, "INSERT INTO OrderLineItem VALUES (" . $idSpatula . ", " . $orderID . ", " . $quantity . ")");
			// Update the spatula quantity in the spatula table
			$spatulasLeft = $quantityInStock - intval($quantity);
			$result2 = mysqli_query($con, "UPDATE Spatula SET QuantityInStock = ". $spatulasLeft . " WHERE idSpatula = " . $idSpatula); 
			$noIssues = $result1 and $result2;
			$hasOrdered = true;
		}	
		if (!$enough)
		{
		  	// They ordered more than we have. Tell them.
		 	echo "You requested " . $quantity . " of spatula " .$idSpatula . " '" . $row['ProductName'] . "'. ";
			echo "Unfortunately, we only have " . $quantityInStock . " in stock.";
			$noIssues = false;
		}
	}
	else
	{
	  	// We have an issue - quantity entered is not valid
	  	$noIssues = false;
	}
}

// Is everything okay?
if (!$hasOrdered and $noIssues)
{
	// They didn't actually order anything
	echo "<p> You didn't select any spatulas. </p>";
	$noIssues = false;
}

if ($orderInsert and $noIssues)
{
	// All queries have been successful
	$result = mysqli_query($con, "COMMIT");
	echo "<p> Order submitted successfully. </p>";
}
else
{
  	// No, things are not okay.
  	$result = mysqli_query($con, "ROLLBACK");
	echo "<p> We could not submit your order. Please try again. </p>";
}
	
mysqli_close($con);

?>

<br/>

<!-- Add new order -->
<form method='POST' action='spatulaorder.php'>
<input type ="submit" value="Submit new order" /> 
</form>

</body>
</html>
```

--------------------------------
## Virtual car maze traversal

**Course:** Software Modelling and Design \\
**Programming language:** Java \\
**Concepts:** Object-oriented software design, GRASP, diagrams (class diagrams, sequence diagrams, communication diagrams)

<p align='justify'>
In this group project, we had to design software to control a virtual car and have it traverse a maze filled with traps.
Particular attention had to be paid to following good object-oriented design principles and the design had to be well-documented with static and behavioural models.
The code also had to be extensible to allow it to deal with other trap types and additional traversal strategies.
</p>

The following is the class diagram for our submission:

<center>
<figure>
  <img
  src="https://tomjdove.github.io/TomJDove/assets/uni/car-classes.jpg"
  style="width:100%"
  >
  <figcaption>
  The class diagram for the autocontroller.
  </figcaption>
</figure>
</center>


<!--

## Database Systems

- Assignment 1: Designed database to store all the relevant information to produce food labels for a fictional multinational food company, subject to specific constraints such as 
Used MySQL to create a Physical Data Model.

- Assignment 2: SQL queries

- Assignment 3: Developed a basic web-application with a database backend. Used PHP, MySQL, HTML, and CSS.


## Object-Oriented Software Development

- Project 1: Created a basic graphical game engine using Java. The GUI was implemented with the Slick library.

- Project 2: Expanding on the first project, we had to fully create an RPG game including characters, health bars, items, and basic combat. We had to design the object-oriented software, including UML class diagrams showing all the classes, their relationships, their attributes and primary public methods.


## Software Modelling and Design

- Project A: Implemented an 'Automail' system that simulates the delivering of mail in a building. The task was to create classes that implement the given mail pooling and mail sorting interface and implement strategies that maximise the efficiency of mail delivery.

- Project B: Analysed an existing implementation of a Metro Melbourne simulation that simulates the behaviour of trains and passengers in Melbourne's train system. We then extended the design and implemented new features.

- Project C: Designed, implemented, and tested a virtual car controller that is able to traverse a maze and its traps. It must be able to use three approaches for dealing with dead-ends; U-turn, 3-point turn, and reversing out.

## Computer Systems


- Project A: Implement a program that simulates CPU memory management and process scheduling.

- Project B: Implemented server-based proof-of-work solver for the Hashcash mining algorithm used in bitcoin. Wrote a TCP server program that can correctly reply to simple messages received from client programs concurrently. 


## Design of Algorithms


- Project 1: Implement two algorithms for topological sorting of directed graphs and study their performance.

- Project 2: Hash table implementation, including linear probing as a collision resolution method, universal hashing, and code to intentionally generate collisions for analysis purposes.

-->

