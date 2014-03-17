Google Test / Google Mock 
=

Overview
=

This is a blog to store my notes on the implementation of google-test that I'm using. I'll also be using google-mock to mock up objects as I go. 

General Notes
=

Tests should be independent and repeatable
Its hard to debug when one test fails because of another
Tests should be well organized and reflect the structure of the tested code
Tests should be portable and reusable -- platform negligent
When tests fail, they should provide as much information about the problem as possible. When they fail, it goes to the next test

Basic Concepts
=

Three types of assertion result 

-	success -- passes
-	nonfatal failure -- continues in the test group
-	fatal failure -- will exit the current group

Tests use assertions to verify the tested code's behavior. 

Test case contains one or many tests, and should be grouped in a way that reflects the structure of the code

When multiple tests in case need to share common objects, they should be put into fixture classes

Assertions
=

Google test assertions are macros that resemble function calls

You test a class or function by making assertions about its behavior. When an assertion fails, the test failed and information is printed

Assertions come in pairs that test the same thing but have different effects on the current function. 
ASSERT_* versions generate fatal failures -- will exit the current function

EXPECT_* functions do not generate a complete failure, just go onto the next test

Custom failure message


	ASSERT_EQ(x.size(), y.siz()) << "Vectors x and y are of unequal length"

	for (int i = 0; i < x.size(); ++i) {

		EXPECT_EQ(x[i], y[i]) << "Vectors x and y differ"
	}


Checkout the different assertions online.

Test Fixtures: Using the Same Data Configuration for Multiple Tests
=

writing two or more tests that operate on similar data can use a test fixutre which allows you to reuse the same configuration of objects for several different tests

	1.) Derive from ::testing::Test and start body with protected or public

	2.) Create a setter / getter function for each object that is being tested etc




